# Keputusan Produk — Evaluasi Meeting LLDIKTI

| Field | Detail |
|---|---|
| Tanggal keputusan dokumentasi | 15 Agustus 2026 |
| Status | **Disetujui** — menjadi acuan Fase 1 sampai ada keputusan yang lebih baru |
| Dasar | Rekaman dan [Transkrip Meeting LLDIKTI](Transkrip-Meeting-LLDIKTI.md), terutama 00:19:22–00:21:45, 00:22:22–00:24:36, 00:30:21–00:35:13, 00:42:52–01:03:16, dan 01:04:49–01:16:08 |
| Pengesahan dokumentasi | Pengguna mengonfirmasi pada 15 Agustus 2026 bahwa dokumentasi harus mengikuti hasil meeting |
| Kedudukan | Ketentuan di dokumen lain yang berbeda pada area yang dicakup di bawah **digantikan** oleh keputusan ini |

## K-MTG-01 — Chain approval cuti dan saldo tahunan

1. Untuk pengajuan cuti biasa, urutan chain adalah **satu atau lebih verifikator dinamis → Kepala Bagian → PYBMC**. Ketua Tim Kerja, bila dibutuhkan, ditempatkan sebagai verifikator; bukan setelah Kepala Bagian. Jika tidak ada verifikator, chain dimulai dari Kepala Bagian lalu diteruskan ke PYBMC.
2. Kuota dasar cuti tahunan adalah **12 hari kerja setiap tahun**. Rollover dari N-1 maksimal **6 hari**. Total tahun berjalan dapat menjadi **24 hari** hanya bila pegawai tidak memakai cuti tahunan pada N-2 dan N-1; bila ada pemakaian satu hari atau lebih pada salah satu dari dua tahun itu, total maksimum tahun berjalan adalah **18 hari**.
3. Pendaftaran data awal dan rekonsiliasi historis memakai **jumlah cuti yang telah dipakai/diklaim per tahun**, bukan saldo/sisa cuti. Sistem menghitung sisa, rollover, dan total hak secara berjenjang dari penggunaan tersebut. Admin tidak menjadikan saldo sisa sebagai sumber hitung utama.
4. Admin Kepegawaian memerlukan form **input cuti manual** untuk cuti yang telah diproses di luar SIMPEG, termasuk cuti historis, cuti pada tahun berjalan sebelum go-live, dan cuti ketika sistem tidak tersedia. Hanya Admin Kepegawaian yang dapat menginputnya; dokumen pendukung wajib; catatan langsung diakui sebagai cuti yang telah disetujui di luar SIMPEG tanpa menjalankan usulan atau approval ulang; dan pemakaian tersebut wajib ikut menghitung saldo serta rollover.
5. Koreksi administratif dilakukan melalui koreksi data pemakaian/entri cuti manual dan perhitungan ulang sistem. Audit wajib merekam aktor, alasan, dokumen, nilai sebelum/sesudah, dan waktu perubahan.
6. **Direct balance override tidak tersedia**, termasuk sebagai jalur break-glass Fase 1. Jika saldo tidak sesuai, Admin Kepegawaian memperbaiki sumber pemakaian atau entri cuti manual, lalu sistem menghitung ulang secara atomik.
7. Input cuti manual hanya merekam cuti yang telah terjadi/disetujui di luar SIMPEG. Jumlah hari kerja dihitung sistem; duplikasi dan periode yang overlap dengan cuti aktif pegawai yang sama ditolak; koreksi mempertahankan riwayat lama melalui pembatalan/versi pengganti, bukan hard delete.
8. Konsumsi saldo memakai hak tertua yang masih sah terlebih dahulu: N-2, kemudian N-1, lalu tahun berjalan. Hak lama yang masih tersisa kedaluwarsa pada akhir tahun penggunaannya.
9. Koreksi backdated menghitung ulang secara kronologis mulai dari transaksi yang dikoreksi sampai seluruh transaksi setelahnya. Sistem tidak menambal saldo akhir secara langsung.
10. PNS dan PPPK memakai mesin hitung 12/18/24 yang sama. Untuk PPPK, total maksimum 18 mensyaratkan masa perjanjian kerja di atas 2 tahun dan total maksimum 24 mensyaratkan masa perjanjian kerja di atas 3 tahun; kesamaan angka tidak menghapus syarat kelayakan berdasarkan jenis pegawai.

## K-MTG-02 — Atribut Keycloak dan role default Pegawai

1. Mapping SSO memakai email Keycloak sebagai atribut utama. LLDIKTI melengkapi email akun uji dan menyediakan daftar role akun uji.
2. Saat email telah cocok dengan pegawai lokal, role default **Pegawai** dari SSO menginisialisasi role internal Pegawai secara otomatis agar akun dapat langsung dimapping saat login pertama. Role internal yang sudah tersimpan tetap menjadi sumber keputusan akses pada request berikutnya.
3. Nomor telepon Keycloak dapat dipetakan bila LLDIKTI menyediakannya sebagai custom attribute. Nama claim/objek aktual tidak boleh ditebak; implementasi membaca kontrak respons yang diberikan LLDIKTI.
4. Role selain default Pegawai, permission, dan semua otorisasi fitur tetap dikelola serta dievaluasi oleh SIMPEG. Tidak ada claim Keycloak yang langsung memberikan permission aplikasi di luar inisialisasi default Pegawai di atas.

## K-MTG-03 — Switch role berbasis permission

1. Pada Fase 1, switch role hanya tersedia bagi **Super Admin** yang juga memiliki permission khusus, untuk kebutuhan demo, pengujian, dan dukungan di development maupun production.
2. Switch role adalah simulasi **role**, bukan impersonasi identitas/pegawai lain. Identitas aktor, kepemilikan data, dan jejak audit tidak berubah.
3. `temporary_role` disimpan secara persisten sehingga tetap berlaku setelah logout/login sampai aktor melakukan revert. Permission efektif selalu diturunkan secara dinamis dari role tujuan; `temporary_permission` tidak boleh menjadi snapshot permanen atau sumber kebenaran otorisasi. Perubahan permission role tujuan berlaku pada request berikutnya.
4. Matriks Fase 1 bersifat eksplisit: Super Admin dapat beralih ke Admin Kepegawaian, Pimpinan, Kepala Bagian, atau Pegawai. Switch ke Super Admin, role yang sama, atau role di luar allowlist ditolak fail-closed. Perubahan, penggunaan, dan revert wajib diaudit serta seluruh endpoint tetap memeriksa permission efektif di backend.

## K-MTG-04 — Hari libur dan dokumen pegawai

1. Hari Libur dikelola pada menu/halaman tersendiri, tidak lagi sebagai tab Data Master. Halaman menampilkan kalender di bagian atas dan tabel hari libur di bawahnya.
2. Dari profil pegawai, Admin Kepegawaian dapat langsung mengunggah dokumen tambahan melalui pemilihan jenis dokumen. Tampilan memisahkan dokumen wajib/SK pada tabel atas dari dokumen tambahan, seperti KTP, KK, dan ijazah, pada tabel bawah.
3. Menu dokumen terpusat tetap dipertahankan untuk Super Admin/Admin Kepegawaian ketika perlu mencari dokumen lintas pegawai.

## K-MTG-05 — Persiapan WhatsApp Business

1. Tim menyusun dokumen template WhatsApp untuk setiap jenis notifikasi yang akan diajukan, berisi contoh pesan dan daftar variabel payload. Contoh minimal mencakup EWS kenaikan pangkat dan Satyalancana.
2. LLDIKTI mengajukan template kepada Meta dan mengembalikan template ID beserta petunjuk pemasangan. Setelah itu integrasi dapat diuji dengan pola pemilihan template dan pengisian variabel, bukan pengiriman teks bebas.
3. Aktivasi adapter/provider WhatsApp tidak dilakukan sebelum template ID dan petunjuk layanan diterima dari LLDIKTI.
4. WhatsApp Business merupakan keluaran wajib hasil evaluasi meeting dan harus siap paling lambat pada target penyelesaian akhir Agustus 2026. Provider final, kontrak API, credential, template ID, bahasa, tombol, nomor uji, serta sandbox tetap diperlakukan sebagai dependency implementasi dari LLDIKTI/provider, bukan Open Question produk baru.

## K-MTG-06 — Validasi revisi dan deployment

1. Target penyelesaian direvisi dari rencana tanggal 20 menjadi **akhir Agustus 2026**, dengan evaluasi Zoom segera setelah satu kelompok revisi siap; tidak perlu menunggu rapat rutin hari Jumat.
2. Setelah penerimaan fitur oleh Kepegawaian, tim menyusun panduan penggunaan per role yang menerangkan fitur, langkah penggunaan, dan dampak aksi.
3. LLDIKTI akan memperbarui image PHP/container pada branch `development` dan dapat menaikkan versi PostgreSQL sedikit. Sebelum lingkungan baru dipakai sebagai acuan, data perlu dapat dibackup dan direstore, lalu aplikasi, migrasi, queue, dan scheduler diverifikasi kembali.

## K-MTG-07 — Penutupan Open Questions addendum

| Field | Detail |
|---|---|
| Tanggal keputusan lanjutan | 18 Agustus 2026 |
| Sumber persetujuan | Konfirmasi langsung pengguna pada pembahasan [Issue SIMPEG #221](https://github.com/LLDIKTI-XVI-TEAM/SIMPEG/issues/221) |
| Kedudukan | Mengikat dan menggantikan status Open Question pada addendum 15 Agustus 2026 |

1. **OQ-MTG-01 — Decided:** permission efektif switch role diturunkan secara dinamis dari role tujuan; snapshot `temporary_permission` tidak menjadi sumber otorisasi.
2. **OQ-MTG-02 — Decided:** direct balance override tidak tersedia. Koreksi selalu memperbaiki sumber pemakaian/entri manual dan menghitung ulang.
3. **OQ-MTG-03 — Decided:** hanya Super Admin ber-permission khusus yang dapat switch ke Admin Kepegawaian, Pimpinan, Kepala Bagian, atau Pegawai.
4. **OQ-MTG-04 — Decided:** input cuti manual khusus Admin Kepegawaian, dengan dokumen wajib, kalkulasi hari kerja oleh sistem, penolakan duplikasi/overlap, dan koreksi auditabel tanpa hard delete.
5. **OQ-MTG-05 — Decided:** bucket tertua yang masih sah dikonsumsi lebih dahulu; expiry terjadi pada akhir tahun penggunaan; koreksi backdated memicu rekalkulasi kronologis. PNS dan PPPK memakai mesin 12/18/24 yang sama; PPPK memerlukan masa perjanjian di atas 2 tahun untuk maksimum 18 dan di atas 3 tahun untuk maksimum 24.
6. **OQ-MTG-06 — Decided:** WhatsApp Business wajib siap dalam target akhir Agustus. Detail provider dan artefak layanan diteruskan sebagai dependency implementasi #214/#215, bukan pertanyaan produk terbuka.
7. **OQ-MTG-07 — Decided:** target penyelesaian final adalah **akhir Agustus 2026**. Target ini tidak dipecah menjadi tanggal teknis tambahan pada acceptance criteria.

## K-MTG-08 — Dokumen wajib, berkas SK, dan arsip dokumen terpusat

| Field | Detail |
|---|---|
| Tanggal keputusan lanjutan | 21 Agustus 2026 |
| Sumber persetujuan | Konfirmasi pengguna setelah klarifikasi dengan pihak terkait LLDIKTI pada review PR #218 |
| Kedudukan | Mengikat; melengkapi dan menggantikan K-MTG-04.2–04.3 pada bagian yang berbeda |

1. Ketentuan dokumen wajib/SK tidak boleh di-hardcode sebagai empat dokumen yang sama untuk seluruh pegawai. Admin Kepegawaian mengelola **matriks dokumen wajib berdasarkan jenis pegawai** sehingga tiap jenis, misalnya PNS, CPNS, atau PPPK sesuai data referensi yang tersedia, dapat memiliki daftar SK wajib yang berbeda.
2. Matriks aktif menjadi sumber tampilan dan penilaian kelengkapan dokumen wajib pada profil pegawai. Dokumen tambahan tetap dikelola terpisah dari daftar SK wajib.
3. Sifat append-only pada riwayat kepangkatan, jabatan, dan KGB berlaku pada **record substantifnya**. Data riwayat yang sudah tersimpan tidak dapat diedit atau dihapus. Namun, berkas lampiran SK pada record tersebut **boleh diganti** tanpa mengubah data substantif, `is_latest`, atau dasar kalkulasi riwayat. Penggantian berkas tetap melewati validasi upload dan wajib diaudit.
4. Arsip dokumen terpusat untuk Super Admin/Admin Kepegawaian bersifat **read-only**: digunakan untuk pencarian lintas pegawai, melihat detail, dan mengunduh berkas yang berwenang diakses. Arsip ini tidak menyediakan unggah, penggantian, penghapusan, atau perubahan metadata dokumen. Semua kontrol dokumen/SK dilakukan dari halaman detail/profil pegawai.

## Dampak dokumentasi

- [PRD SIMPEG Fase 1](PRD-DLL/PRD-SIMPEG-Fase1-Core.md), [User Stories](PRD-DLL/User-Stories-SIMPEG-Fase1.md), [Issues](PRD-DLL/Issues-SIMPEG-Fase1.md), serta tracker peran dan sprint yang terdampak telah diperbarui untuk K-MTG-08. [Panduan Penulisan Kode](PRD-DLL/Panduan-Penulisan-Kode-SIMPEG.md) tetap menjadi acuan arsitektur, keamanan, dan QA tanpa mengubah keputusan produk ini.
- Pencatatan keputusan tidak menjadi bukti penyelesaian fitur. Status implementasi setiap butir tetap ditentukan oleh bukti code review, test, dan QA yang sesuai.



## K-MTG-05A — Katalog template WhatsApp Business SIMPEG

> **Status:** Disiapkan oleh tim SIMPEG, belum diajukan/disetujui Meta, dan belum diimplementasikan. Katalog ini menerjemahkan arahan meeting untuk menyiapkan sekitar tiga sampai empat model pesan; LLDIKTI tetap menjadi pihak yang mengajukan template dan mengembalikan template ID/petunjuk integrasi.

| Kode rancangan | Model template | Event yang dicakup | Penerima | Variabel minimum |
|---|---|---|---|---|
| `simpeg_cuti_perlu_tindakan` | Cuti — Perlu Tindakan | Pengajuan cuti masuk ke verifikator, Kepala Bagian, atau PYBMC aktif | Aktor pada step aktif | nama_pegawai, jenis_cuti, tanggal_mulai, tanggal_selesai, jumlah_hari, tautan_detail |
| `simpeg_cuti_status` | Cuti — Perubahan Status | Keputusan `Disetujui`, `Perubahan`, `Ditangguhkan`, atau `Tidak Disetujui` | Pegawai pemohon | nama_pegawai, jenis_cuti, status, keterangan, tautan_detail |
| `simpeg_ews_pengingat` | EWS — Pengingat Kepegawaian | Kenaikan Pangkat, KGB, Pensiun, Kontrak PPPK, dan Satyalancana | Pegawai terkait dan/atau Admin Kepegawaian | nama_pegawai, jenis_peringatan, tanggal_target, sisa_waktu, tautan_detail |
| `simpeg_notifikasi_sistem` | Notifikasi Sistem | Pesan operasional di luar cuti/EWS bila kemudian disetujui | Penerima sesuai event | judul, ringkasan, tautan_detail |

1. Tiga model pertama adalah katalog minimum yang perlu disiapkan. Model `simpeg_notifikasi_sistem` bersifat opsional dan tidak diajukan bila belum ada event yang disetujui.
2. Jika Meta/Qontak tidak menerima generalisasi format atau variabel sebuah model, model tersebut dipecah per event dengan isi dan variabel yang telah disetujui, tanpa mengubah domain event SIMPEG.
3. Kontrak akhir mengikuti template ID, nama variabel, bahasa, dan konfigurasi tombol URL yang diberikan LLDIKTI setelah persetujuan Meta/Qontak.
4. Template OTP yang terdapat pada baseline Qontak tidak termasuk katalog SIMPEG saat ini karena autentikasi SIMPEG memakai Keycloak SSO; OTP hanya dapat ditambahkan melalui keputusan produk terpisah.
