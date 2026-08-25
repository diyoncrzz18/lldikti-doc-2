# Keputusan Produk — Lifecycle dan Status Pegawai

| Field | Detail |
|---|---|
| Tanggal keputusan | 25 Agustus 2026 |
| Status | **Disetujui — kanonis** |
| Sumber | Keputusan stakeholder untuk sinkronisasi dokumentasi lifecycle/status pegawai pada SIMPEG Issue #22 dan PR #19 |
| Kedudukan | Menggantikan ketentuan terdahulu yang berbeda mengenai soft delete/restore Employee, tanggal efektif masa depan, reaktivasi Super Admin-only, transaksi notifikasi, dan akses akun pegawai Nonaktif |

## K-STATUS-01 — Lifecycle Employee berbasis status

1. Record pegawai tetap berada pada tabel `employees` sepanjang Fase 1. Model Employee tidak memakai `deleted_at` atau Laravel `SoftDeletes`.
2. Fase 1 tidak menyediakan hard delete Employee, halaman/dataset lifecycle **Data Backup**, atau halaman/dataset terpisah **Data Nonaktif**. Pegawai berstatus apa pun dicari pada **Data Pegawai** melalui filter status.
3. Penonaktifan dan pengaktifan kembali adalah perubahan status resmi melalui `ref_status_pegawai`, bukan operasi delete/restore record.
4. Riwayat perubahan status bersifat append-only. Perubahan lama tidak diedit atau dihapus untuk membentuk keadaan baru.

## K-STATUS-02 — Predicate aktif kanonis

1. Sumber kebenaran aktif/nonaktif adalah `ref_status_pegawai.kelompok`, bukan nama status, kode status, atau kolom legacy `status_aktif`.
2. Kelompok `Aktif` dan `Aktif/khusus` sama-sama diperlakukan aktif. Karena itu **Tugas Belajar** tetap aktif.
3. Semua consumer—daftar default, dashboard, EWS, cuti, laporan, lookup, approval, dan kontrol akses akun—wajib memakai semantik tunggal yang diwujudkan melalui `Employee::isActive()` dan `Employee::whereActiveStatus()` atau abstraksi kanonis setara yang sudah disediakan aplikasi.
4. Query literal seperti `where('status_aktif', 'Aktif')`, perbandingan nama `Aktif`, atau daftar kode status lokal tidak boleh menjadi sumber keputusan domain baru.

## K-STATUS-03 — Kontrak perubahan status

Setiap perubahan status resmi wajib memiliki:

- status tujuan yang valid;
- tanggal efektif;
- alasan administratif yang wajib diisi;
- satu riwayat append-only ketika perubahan berlaku;
- snapshot Employee yang konsisten;
- audit kritis yang berhasil ditulis dalam transaksi yang sama.

`status_note` adalah pesan akun opsional yang terpisah dari alasan administratif. Bila penonaktifan tidak memberikan pesan khusus, nilai bawaan adalah:

> AKUN ANDA TELAH DI NONAKTIFKAN, SILAHKAN HUBUNGI ADMIN!!

Nilai `status_note` tidak boleh dipakai sebagai pengganti alasan administratif. Perubahan status umum yang ternyata tidak mengubah status efektif harus berhenti sebagai no-op setelah lock dan tidak boleh membuat histori/audit duplikat atau menimpa `status_note` dengan nilai yang tidak relevan.

## K-STATUS-04 — Otorisasi berbasis role efektif dan permission

1. Penonaktifan mengikuti permission perubahan status yang berlaku pada matriks RBAC.
2. Pengaktifan kembali dapat dilakukan oleh **Super Admin** atau **Admin Kepegawaian** bila role efektif aktor memiliki permission `employees.restore`.
3. Semua gate, `FormRequest::authorize()`, policy, Action, dan service membaca role efektif serta permission efektif yang sama. Raw role asal seperti `$user->role` tidak boleh digabung dengan pemeriksaan role/permission efektif dengan cara yang membuka bypass.
4. Switch role tidak mengubah identitas aktor. Audit mutasi status menyimpan konteks role asli dan role efektif yang digunakan.

## K-STATUS-05 — Blokir global akun pegawai Nonaktif

1. User yang terhubung ke Employee dengan status efektif Nonaktif tidak dapat mengakses route bisnis SIMPEG, tanpa pengecualian berdasarkan role. Aturan ini juga berlaku bila akun linked tersebut memiliki role Super Admin, Admin Kepegawaian, Pimpinan, Kepala Bagian, atau Pegawai.
2. Akses yang tetap diizinkan hanya halaman status akun, logout, dan route teknis autentikasi yang benar-benar diperlukan untuk menyelesaikan atau membersihkan sesi.
3. Middleware/access guard mengevaluasi status efektif sebelum controller dan fail-closed bila relasi status yang diperlukan tidak valid atau tidak dapat ditentukan.
4. Pesan default halaman status akun menggunakan `status_note` di atas, kecuali tersedia pesan khusus yang sah.

## K-STATUS-06 — Tanggal efektif masa depan

1. Tanggal efektif masa depan diperbolehkan.
2. Perubahan masa depan disimpan sebagai transisi terjadwal. Snapshot Employee, predicate aktif, dan akses akun saat ini tidak berubah sebelum tanggal efektif tercapai.
3. Scheduler/job/action menerapkan transisi otomatis ketika tanggal efektif tercapai berdasarkan zona waktu aplikasi `Asia/Makassar`.
4. Eksekusi wajib memakai lock, membaca ulang keadaan setelah lock, idempoten, aman terhadap retry, dan aman terhadap proses bersamaan. Transisi yang sudah berlaku tidak boleh menghasilkan histori, audit, atau notifikasi duplikat.

## K-STATUS-07 — Transaksi, audit, dan notifikasi

1. Mutasi status aktif menggunakan urutan minimum `lockForUpdate → re-check → mutate`.
2. Perubahan snapshot status, pembuatan riwayat append-only, dan audit kritis merupakan satu transaksi logis. Kegagalan audit menggagalkan dan me-roll back perubahan status.
3. Payload audit minimum memuat aktor, status sebelum/sesudah, tanggal efektif, alasan administratif, IP, user agent, timestamp, dan konteks role efektif. Payload tidak menyalin seluruh row Employee dan tidak memuat NIK, No. KK, token, credential, atau data sensitif lain yang tidak diperlukan.
4. Intent notifikasi diterbitkan hanya setelah commit. Kegagalan delivery notifikasi tidak me-roll back status yang sudah sah; retry mengikuti infrastruktur notifikasi.
5. Event `status_pegawai.dinonaktifkan` memakai channel yang dapat dikonfigurasi. Default yang direkomendasikan adalah in-app dan email aktif, tetapi operator tetap dapat mengubah kebijakan channel tanpa mengubah kode domain.

## K-STATUS-08 — Acceptance dan regression minimum

Implementasi belum dapat dinyatakan selesai tanpa bukti untuk:

1. status kelompok `Aktif` dan `Aktif/khusus`, termasuk Tugas Belajar;
2. penonaktifan dan pengaktifan kembali oleh kombinasi role/permission yang sah serta penolakan tanpa permission;
3. role efektif ketika switch role aktif, termasuk pencegahan bypass raw role;
4. blokir route bisnis untuk seluruh role yang linked Employee-nya efektif Nonaktif;
5. pengecualian terbatas untuk halaman status akun, logout, dan route auth teknis;
6. tanggal efektif hari ini, masa lalu yang sah, serta masa depan sebelum dan sesudah scheduler berjalan;
7. retry, dua worker bersamaan, double submit, dan no-op perubahan status yang sama;
8. rollback penuh ketika audit gagal;
9. notifikasi hanya setelah commit dan kegagalan delivery tidak mengubah hasil status;
10. Data Pegawai tetap menjadi satu-satunya surface daftar dengan filter status, tanpa Data Backup/Data Nonaktif;
11. EWS, dashboard, laporan, cuti, dan lookup memakai predicate aktif kanonis yang sama;
12. PostgreSQL feature/integration test serta smoke browser untuk alur utama, aksesibilitas dasar, console error, dan performa halaman.

## Ketentuan yang dinyatakan Superseded

Ketentuan berikut tidak lagi normatif:

- soft delete/restore Employee dan penggunaan `deleted_at`;
- halaman atau dataset lifecycle Data Backup/Data Nonaktif;
- larangan tanggal efektif masa depan;
- pengaktifan kembali yang dibatasi hanya untuk Super Admin;
- pengecualian akses route bisnis berdasarkan role tinggi ketika linked Employee sudah efektif Nonaktif;
- notifikasi yang dikirim di dalam transaksi status sebelum commit;
- query aktif berdasarkan literal `status_aktif = 'Aktif'` atau nama/kode status lokal.

Dokumen tracker, laporan QA, dan catatan implementasi lama boleh mempertahankan istilah tersebut hanya sebagai bukti historis apabila diberi label **Superseded** dan tidak disajikan sebagai kontrak aktif.
