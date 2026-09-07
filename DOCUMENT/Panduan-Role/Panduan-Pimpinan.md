# Panduan Penggunaan — Pimpinan

> **Kontrak target 7 September 2026:** [Keputusan PATEN dan RBAC](../Keputusan-RBAC-Pemisahan-Capability-Paten-dan-Configurable-7-September-2026.md) menggantikan batas authorization lama pada panduan ini. Capability personal/assignment/domain adalah **🔒 PATEN**; capability delegated/admin adalah **⚙️ RBAC**. Role contoh menggambarkan konfigurasi awal, bukan allowlist permanen. Perubahan ini belum membuktikan implementasi atau UAT lulus.

| Field | Nilai |
|---|---|
| Role internal | `pimpinan` |
| Status | **Draft — belum diterima Kepegawaian** |
| Cakupan | Default permission untuk monitoring organisasi, keputusan akhir cuti, EWS, dan laporan read-only; akses aktual mengikuti permission efektif serta scope |

## 1. Prasyarat

- Akun sudah dipetakan ke pegawai aktif dengan role internal `pimpinan`.
- Pegawai Pimpinan ditetapkan sebagai PYBMC/final approver sesuai konfigurasi yang berlaku.
- Pengajuan hanya muncul setelah tahap sebelumnya selesai dan Pimpinan menjadi approver aktif.

## 2. Fitur dan Langkah Utama

| Fitur | Langkah ringkas | Dampak tindakan |
|---|---|---|
| Dashboard Pimpinan | Buka `/pimpinan/dashboard` dan periksa ringkasan organisasi | Menampilkan agregat organisasi tanpa memberi hak mutasi data pegawai |
| Data Pegawai | Gunakan daftar/filter dan buka detail pegawai | Skenario baca mengikuti scope dan masking; mutasi memerlukan permission RBAC terkait dan invariant domain |
| Persetujuan Cuti | Buka `/pimpinan/cuti`, cari pengajuan aktif, baca detail, lalu pilih keputusan | Keputusan final dapat memotong saldo, menghasilkan dokumen, notifikasi, dan audit |
| EWS | Buka EWS organisasi dan filter alert | Memantau kondisi organisasi; EWS bukan keputusan otomatis |
| Laporan | Buka laporan sesuai permission; unduh nominatif hanya bila `employees.export` diberikan, dan riwayat sesuai `employee_histories.export` | `employees.export` default OFF; grant tetap mengikuti scope global kanonis, masking/privacy, dan allowlist kolom |
| Reporting Statistik Kepegawaian | Buka halaman reporting dan pilih filter yang diizinkan | Menampilkan chart/agregat sesuai scope; bukan jalur mutasi atau export detail |
| Notifikasi | Buka inbox, pilih notifikasi, lalu tandai dibaca | Mengubah status baca milik user dan mengarahkan ke record terkait |

## 3. Alur Keputusan Akhir Cuti

1. Buka `/pimpinan/cuti`.
2. Periksa ringkasan pengajuan yang menunggu keputusan Anda.
3. Cari dan buka pengajuan.
4. Periksa pegawai, jenis cuti, periode, hari kerja, alasan, saldo, lampiran, dan timeline.
5. Pastikan tahap sebelumnya selesai dan Anda adalah approver aktif.
6. Pilih salah satu keputusan resmi.
7. Untuk selain `Disetujui`, isi alasan yang jelas.
8. Konfirmasi tindakan.
9. Periksa status akhir, notifikasi, dokumen, dan Audit Log.
10. Bila Anda juga ditetapkan sebagai Atasan Langsung untuk pengajuan yang sama, pastikan tindakan Atasan Langsung dan tindakan PYBMC tercatat sebagai dua tahap terpisah.

Dampak keputusan:

| Keputusan | Dampak |
|---|---|
| `Disetujui` | Menyelesaikan chain, memotong saldo tahunan sesuai hasil sistem, membuat dokumen, dan memberi notifikasi |
| `Perubahan` | Mengembalikan pengajuan untuk diperbaiki; saldo tidak dipotong final |
| `Ditangguhkan` | Menyimpan alasan penangguhan; saldo tidak dipotong final |
| `Tidak Disetujui` | Menutup pengajuan tanpa pemotongan saldo dan melepaskan alokasi |

Formulir yang dihasilkan setelah keputusan final memuat Nama, Jabatan, dan Peran setiap pihak approval. Periksa data tersebut melalui jalur dokumen yang berwenang tanpa membagikan lampiran kepada pihak di luar scope.

## 4. Batas Akses dan Larangan

- Akses baca administratif memerlukan permission dan scope. Mutasi hanya bila permission RBAC terkait diberikan dan domain mengizinkan; jangan mencari jalur bypass di luar aksi resmi.
- Keputusan hanya boleh dilakukan ketika user menjadi approver aktif.
- Jangan menggunakan istilah `Ditolak`; label resminya `Tidak Disetujui`.
- Jangan membuat keputusan berdasarkan EWS saja; EWS adalah indikator untuk verifikasi administratif.
- Jangan mengekspor data kontak pribadi atau identitas sensitif yang tidak diperlukan.
- Jangan membagikan lampiran cuti kepada pihak di luar kewenangan.
- Permission tambahan seperti `dokumen_sk.read` atau `employees.export` tetap tunduk pada scope/masking; grant/revoke harus efektif. Pimpinan dengan `users.switch_role` dapat memilih Kepala Bagian/Pegawai, tanpa same/higher/unknown/chained switch atau perubahan identitas/ownership/scope asli.
- Approval final assigned pada active step dan proof otomatis adalah PATEN/domain. Profil/riwayat/keluarga/notifikasi/cuti/saldo sendiri serta baca Hari Libur tetap PATEN sesuai lifecycle/domain, bukan checkbox role.

## 5. Troubleshooting

| Gejala | Pemeriksaan |
|---|---|
| Pengajuan tidak muncul | Periksa tahap sebelumnya, snapshot approver, status pengajuan, dan akun pegawai Pimpinan |
| Tombol keputusan tidak ada | Pastikan Anda approver aktif dan pengajuan belum diputus |
| Saldo belum berubah | Saldo hanya dipotong setelah keputusan final `Disetujui` |
| Laporan kosong | Periksa periode, filter, status pegawai, dan scope data |

## 6. Penerimaan Panduan

| Field | Nilai |
|---|---|
| Exact SHA yang diuji | Belum diisi |
| Tanggal UAT | Belum diisi |
| Pemberi keputusan | Belum diisi |
| Status | Perlu Tindak Lanjut — UAT belum dilaksanakan |
| Evidence | Belum ada |
