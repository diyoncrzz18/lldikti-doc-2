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
| Data Pegawai | Cari/tambah/ubah data utama, tetapkan Atasan Langsung, dan tambahkan riwayat berdasarkan SK | Mengubah data operasional pegawai dan memengaruhi scope, EWS, serta laporan |
| Lifecycle Status | Dari Data Pegawai pilih Ubah Status/Nonaktifkan/Aktifkan Kembali, isi status tujuan, tanggal efektif, dan alasan administratif | Transisi langsung/terjadwal mengubah snapshot, histori, akses akun, EWS, dan notifikasi ketika efektif; reaktivasi memerlukan `employees.restore` |
| Dokumen & SK | Unggah berkas, isi metadata, periksa dampak, dan unduh sesuai permission | Menyimpan dokumen ke storage terproteksi; matriks membedakan SK Pengangkatan PNS dan SK Pengangkatan CPNS |
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

Untuk PNS, periksa SK Pengangkatan PNS; untuk CPNS, periksa SK Pengangkatan CPNS. Saat status berubah dari CPNS menjadi PNS, evaluasi kembali kelengkapan matriks PNS dan unggah SK Pengangkatan PNS bila belum tersedia. Pegawai tidak mengunggah dokumen sendiri pada Fase 1.

Penonaktifan mempertahankan record Employee. Tidak ada hard delete, Data Backup, atau Data Nonaktif.
Semua status ditemukan melalui filter Data Pegawai. Kelompok `Aktif` dan `Aktif/khusus`, termasuk
Tugas Belajar, tetap aktif. Tanggal masa depan boleh dipilih dan tidak mengubah akses sebelum efektif.
Pengaktifan kembali adalah perubahan status resmi dan hanya tersedia bila role efektif memiliki
`employees.restore`.

Alasan administratif selalu wajib. Pesan akun `status_note` terpisah dan opsional; bila kosong pada
penonaktifan, sistem memakai `AKUN ANDA TELAH DI NONAKTIFKAN, SILAHKAN HUBUNGI ADMIN!!`.

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
3. Gunakan entri **Cuti di Luar SIMPEG** untuk fakta historis/transisi yang sudah disetujui atau cuti yang diproses manual ketika layanan downtime; halaman **Catat Pemakaian Tahunan** hanya dibaca sebagai agregat dan bukan tempat memasukkan angka langsung.
4. Untuk koreksi, pilih fakta sumber yang benar dan isi alasan wajib.
5. Nomor dokumen dan dokumen pendukung bersifat opsional; bila diberikan, unggah file tervalidasi pada storage privat.
6. Simpan, lalu periksa hasil replay/rekalkulasi dan audit.
7. Untuk cuti yang sudah final `Disetujui` tetapi harus dibatalkan secara administratif, gunakan aksi `Ditangguhkan`, isi alasan wajib, dan periksa koreksi ledger serta histori.

Tidak tersedia direct balance override. Koreksi memperbaiki sumber pemakaian dan menghitung ulang
saldo secara deterministik. Setelah downtime, catat hanya cuti yang proses manualnya sudah selesai dan
disetujui di luar sistem. Jangan memakai Cuti di Luar SIMPEG sebagai jalur rutin ketika SIMPEG tersedia.

## 6. Alur Menangani Permohonan Pembatalan Cuti

1. Buka notifikasi permohonan pembatalan dan periksa pengajuan serta alasan Pegawai.
2. Pastikan pengajuan belum final dan approval utamanya sedang ditahan.
3. Pilih keputusan **Setujui Pembatalan** atau **Tolak Pembatalan** melalui aksi resmi.
4. Jika disetujui, pastikan usulan menjadi batal, reservasi saldo dilepas, dan histori tetap tersedia.
5. Jika ditolak, pastikan approval dilanjutkan dari tahap sebelumnya dan tindakan yang sudah ada tidak hilang.
6. Periksa audit dan notifikasi hasil kepada Pegawai. Jangan menghapus pengajuan atau membuat dokumen PDF pembatalan yang tidak dipersyaratkan.

Permohonan ini berbeda dari cuti final `Disetujui`. Cuti final tetap ditangani melalui aksi administratif
`Ditangguhkan` dengan alasan wajib dan koreksi ledger.

## 7. Batas Akses dan Larangan

- Tidak mengelola role/permission sistem atau konfigurasi khusus Super Admin.
- Tidak otomatis menjadi approver cuti hanya karena berperan sebagai Admin.
- Tidak melakukan keputusan final jika tidak menjadi approver aktif pada snapshot.
- Tidak mengedit histori lama atau menghapus pegawai permanen.
- Tidak memakai Data Backup/Data Nonaktif atau menganggap reaktivasi sebagai restore record terhapus.
- Tidak mencoba reaktivasi tanpa `employees.restore`, sekalipun role asal memiliki privilege lebih tinggi saat switch role aktif.
- Tidak mengubah saldo langsung tanpa sumber, alasan, dokumen, dan audit.
- Tidak mengekspos NIK, No. KK, token, atau credential pada export/evidence.
- Tidak mengaktifkan provider WhatsApp.

## 8. Troubleshooting

| Gejala | Pemeriksaan |
|---|---|
| Pegawai ditolak sebagai duplikat | Cocokkan NIP, email kanonis, dan laporan import sebelum mencoba ulang |
| Baris import menjadi skip | Periksa NIP existing; skip bukan error dan tidak membuat pegawai baru |
| Saldo tidak sesuai | Periksa sumber pemakaian, alokasi pengajuan aktif, urutan kronologis, dan hasil rekalkulasi |
| Riwayat tidak muncul | Periksa dokumen, tanggal efektif, reference, dan apakah record baru berhasil dibuat |
| Tidak dapat membuka menu | Periksa role dan permission; jangan meminta bypass route |
| Akun hanya melihat status Nonaktif | Status efektif Employee linked sudah tidak aktif; periksa histori/alasan dan lakukan reaktivasi resmi bila sah. Role tinggi tidak membypass blokir |

## 9. Penerimaan Panduan

| Field | Nilai |
|---|---|
| Exact SHA yang diuji | Belum diisi |
| Tanggal UAT | Belum diisi |
| Pemberi keputusan | Belum diisi |
| Status | Perlu Tindak Lanjut — UAT belum dilaksanakan |
| Evidence | Belum ada |
