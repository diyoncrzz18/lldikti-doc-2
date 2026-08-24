# Panduan Penggunaan — Admin Kepegawaian

| Field | Nilai |
|---|---|
| Role internal | `admin_kepegawaian` |
| Status | **Draft — belum diterima Kepegawaian** |
| Cakupan | Operasional data pegawai, cuti, dokumen, EWS, laporan, dan audit sesuai permission |

## 1. Prasyarat

- Akun sudah dipetakan ke pegawai aktif dengan role internal Admin Kepegawaian.
- Reference data dan unit kerja yang diperlukan sudah tersedia.
- Dokumen sumber tersedia untuk perubahan data kepegawaian atau koreksi pemakaian cuti.
- File import mengikuti template resmi dan tidak memuat data di luar kebutuhan.

## 2. Fitur dan Langkah Utama

| Fitur | Langkah ringkas | Dampak tindakan |
|---|---|---|
| Data Pegawai | Cari/tambah/ubah data utama, tetapkan Kepala Bagian, dan tambahkan riwayat berdasarkan SK | Mengubah data operasional pegawai dan memengaruhi scope, EWS, serta laporan |
| Dokumen & SK | Unggah berkas, isi metadata, periksa dampak, dan unduh sesuai permission | Menyimpan dokumen ke storage terproteksi; file dan metadata menjadi bagian profil pegawai |
| Import Pegawai | Unduh template, unggah, petakan kolom, validasi preview, lalu eksekusi | Membuat banyak data utama; tidak membuat histori pangkat/jabatan/KGB secara otomatis |
| Administrasi Pemakaian Cuti | Cari pegawai, catat atau perbaiki sumber pemakaian dengan alasan dan dokumen | Menjalankan rekalkulasi saldo serta ledger; histori lama tetap dipertahankan |
| Monitoring dan Rekap Cuti | Gunakan filter, buka detail, periksa alur, saldo, dan status | Akses monitoring; Admin tidak otomatis menjadi approver |
| EWS dan Follow-up | Buka EWS aktif, periksa alert, tindak lanjuti berdasarkan dokumen resmi | Memperbarui lifecycle alert dan dapat menghasilkan notifikasi/audit |
| Laporan dan Export | Pilih filter/kolom aman, periksa preview, lalu unduh | Menghasilkan data untuk kebutuhan administrasi; data sensitif tetap dibatasi |
| Audit Log | Filter dan buka detail aktivitas | Membuktikan actor, waktu, aksi, dan perubahan; record bersifat immutable |

## 3. Alur Data Pegawai dan Riwayat

1. Cari pegawai untuk mencegah duplikasi NIP/email.
2. Isi data utama menggunakan reference table yang tersedia.
3. Simpan dan periksa validasi.
4. Untuk pangkat, jabatan, KGB, pengangkatan, atau pendidikan, gunakan menu tambah riwayat.
5. Unggah dokumen SK yang sesuai dan isi tanggal efektif.
6. Jangan mengedit record histori lama untuk mengganti keadaan terkini.
7. Periksa Audit Log setelah mutasi penting.

Penonaktifan pegawai harus mempertahankan data dan memungkinkan pemulihan. Fase 1 tidak menyediakan
penghapusan permanen pegawai.

## 4. Alur Import Pegawai

1. Unduh template resmi.
2. Isi data utama sesuai header dan referensi kanonis.
3. Unggah file CSV/Excel.
4. Petakan header sumber ke field tujuan.
5. Pastikan tidak ada target ganda dan field wajib sudah dipetakan.
6. Jalankan validasi dan baca klasifikasi valid/skip/error.
7. Eksekusi hanya setelah preview sesuai.
8. Unduh laporan hasil dan tindak lanjuti baris gagal.

Import tidak membuat histori kepegawaian atau EWS. Histori ditambahkan melalui alur resmi berbasis
dokumen setelah pegawai tersedia.

## 5. Alur Administrasi Pemakaian Cuti

1. Buka `/cuti/administrasi-saldo` dan cari pegawai.
2. Periksa saldo aktual, pemakaian, alokasi, dan ledger.
3. Catat pemakaian tahunan atau entri manual sesuai dokumen sumber.
4. Untuk koreksi, pilih record yang benar dan isi alasan wajib.
5. Unggah dokumen pendukung.
6. Simpan, lalu periksa hasil replay/rekalkulasi dan audit.

Tidak tersedia direct balance override. Koreksi memperbaiki sumber pemakaian dan menghitung ulang
saldo secara deterministik.

## 6. Batas Akses dan Larangan

- Tidak mengelola role/permission sistem atau konfigurasi khusus Super Admin.
- Tidak otomatis menjadi approver cuti hanya karena berperan sebagai Admin.
- Tidak melakukan keputusan final jika tidak menjadi approver aktif pada snapshot.
- Tidak mengedit histori lama atau menghapus pegawai permanen.
- Tidak mengubah saldo langsung tanpa sumber, alasan, dokumen, dan audit.
- Tidak mengekspos NIK, No. KK, token, atau credential pada export/evidence.
- Tidak mengaktifkan provider WhatsApp.

## 7. Troubleshooting

| Gejala | Pemeriksaan |
|---|---|
| Pegawai ditolak sebagai duplikat | Cocokkan NIP, email kanonis, dan laporan import sebelum mencoba ulang |
| Baris import menjadi skip | Periksa NIP existing; skip bukan error dan tidak membuat pegawai baru |
| Saldo tidak sesuai | Periksa sumber pemakaian, alokasi pengajuan aktif, urutan kronologis, dan hasil rekalkulasi |
| Riwayat tidak muncul | Periksa dokumen, tanggal efektif, reference, dan apakah record baru berhasil dibuat |
| Tidak dapat membuka menu | Periksa role dan permission; jangan meminta bypass route |

## 8. Penerimaan Panduan

| Field | Nilai |
|---|---|
| Exact SHA yang diuji | Belum diisi |
| Tanggal UAT | Belum diisi |
| Pemberi keputusan | Belum diisi |
| Status | Perlu Tindak Lanjut — UAT belum dilaksanakan |
| Evidence | Belum ada |
