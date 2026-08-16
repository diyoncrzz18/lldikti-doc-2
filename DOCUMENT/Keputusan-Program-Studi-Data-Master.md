# Keputusan Program Studi sebagai Data Referensi

| Field | Detail |
|---|---|
| Tanggal keputusan | 17 Agustus 2026 |
| Cakupan | SIMPEG Fase 1 |
| User story utama | US-8.5 · Kelola Reference Tables |
| User story terdampak | US-2.1, US-2.2, US-2.4, US-2.5, US-3.1, US-3.4 |

## Latar Belakang

Program Studi sebelumnya hanya disimpan sebagai snapshot teks pada
`employees.prodi_pendidikan_terakhir` dan `education_histories.jurusan`. Keputusan baru
ini menetapkan Program Studi sebagai data referensi yang dikelola pada Data Master agar
pilihan pada data pegawai dan riwayat pendidikan konsisten tanpa menghilangkan
kompatibilitas data lama maupun file import yang sudah digunakan tim.

## Keputusan

1. `ref_program_studi` menjadi reference table kelolaan US-8.5 kesembilan dan
   ditampilkan sebagai tab Program Studi pada `/data-master`.
   `ref_notification_channels` tetap dikelola pada halaman khusus channel notifikasi.
2. Program Studi dan Jenjang Pendidikan merupakan dua referensi terpisah. Fase 1 tidak
   menetapkan relasi langsung antara `ref_program_studi` dan
   `ref_jenjang_pendidikan` karena aturan satu Program Studi hanya berlaku untuk satu
   jenjang belum diputuskan.
3. `ref_program_studi` memakai UUID, nama, dan status aktif. Nama dijaga unik setelah
   trim, penyatuan spasi berulang, serta perbandingan tanpa membedakan kapitalisasi.
4. `employees.program_studi_id` dan `education_histories.program_studi_id` merupakan
   foreign key nullable dengan perilaku `nullOnDelete`. Kolom snapshot lama tetap
   dipertahankan untuk kompatibilitas.
5. Migrasi awal membuat referensi dari gabungan nilai nonkosong
   `employees.prodi_pendidikan_terakhir` dan `education_histories.jurusan`,
   menggabungkan duplikat setelah normalisasi, lalu menghubungkan kembali record asal.
6. Form tambah hanya menerima referensi aktif. Form edit tetap menampilkan referensi
   nonaktif yang sedang digunakan agar data lama dapat dipertahankan atau diperbaiki,
   tetapi tidak boleh memilih referensi nonaktif lain untuk data baru.
7. Pemilihan referensi menyinkronkan snapshot. Perubahan nama referensi juga
   menyinkronkan snapshot pegawai dan riwayat pendidikan yang terhubung. Pengosongan
   Program Studi pegawai harus dilakukan melalui intent eksplisit agar snapshot import
   yang belum direkonsiliasi tidak hilang tanpa sengaja.
8. Referensi yang sedang dipakai tidak dapat dihapus; Super Admin dapat
   menonaktifkannya. Referensi yang belum dipakai dapat dihapus permanen sesuai pola
   lifecycle Data Master. Seluruh mutasi tetap tercatat pada audit log.
9. Mutasi Program Studi hanya tersedia bagi role `super_admin` yang juga memiliki
   permission `reference_tables.manage`. Role gate dan permission gate merupakan
   pertahanan berlapis dan harus ditegakkan pada backend.
10. Import Data Utama tetap menerima `Prodi Pendidikan Terakhir` sebagai teks snapshot.
    Import tidak mencari, membuat, atau menghubungkan `ref_program_studi`; rekonsiliasi
    otomatis import membutuhkan keputusan produk terpisah.
11. Tampilan detail Admin, profil pegawai, dan detail Pimpinan memprioritaskan nama dari
    relasi Program Studi, lalu memakai snapshot lama sebagai fallback. Permukaan
    Pimpinan tetap read-only.

## Sumber Data dan Pemeliharaan

- Sumber katalog awal adalah snapshot Program Studi yang sudah tersimpan ketika migrasi
  dijalankan.
- Setelah migrasi, penambahan dan pemeliharaan nama dilakukan oleh Super Admin melalui
  Data Master.
- Daftar resmi tambahan dari LLDIKTI dapat dimasukkan melalui Data Master; keputusan ini
  tidak mengizinkan pembuatan master secara otomatis dari file import baru.

## Skenario Verifikasi Minimum

- migrasi fresh dan existing, termasuk deduplikasi nama berdasarkan spasi dan kapitalisasi;
- create, update, aktif/nonaktif, delete protection, dan audit Data Master;
- penolakan role/permission yang tidak berhak;
- tambah/edit pegawai dan riwayat pendidikan, termasuk referensi nonaktif yang sedang dipakai;
- sinkronisasi rename, fallback snapshot, dan pengosongan eksplisit;
- import snapshot-only tanpa side effect pada master;
- detail Admin, Pegawai, dan Pimpinan tetap menampilkan data dengan benar dan aman.
