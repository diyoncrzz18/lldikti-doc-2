# Ringkasan Rapat untuk Evaluasi Projek SIMPEG bersama Mahasiswa Magang Univ Klabat

> Senin, 31 Agustus 2026 · 10.26–12.21 WITA (1 jam 55 menit)

> Ringkasan ini bersifat interpretatif. Jika terdapat perbedaan redaksi, keputusan produk dan PRD kanonis menjadi acuan. Istilah dan kesimpulan di bawah telah diselaraskan kembali terhadap transkrip lengkap dan klarifikasi stakeholder.

## Rekap cepat

Pertemuan difokuskan untuk menunjukkan kemajuan dan fungsionalitas SIMPEG pada lima role: Super Admin, Admin Kepegawaian, Kepala Bagian, Pimpinan, dan Pegawai. Dion mempresentasikan manajemen pegawai, import data, dokumen, cuti, approval chain, notifikasi, EWS, dashboard, dan laporan. Evaluasi menghasilkan perubahan utama pada terminologi **Atasan Langsung**, lifecycle cuti, sumber pemakaian historis, isi formulir cuti, validasi SK Pengangkatan PNS/CPNS, dan Reporting Statistik. Demo juga menemukan kegagalan integrasi WhatsApp `422` yang harus ditangani sebagai masalah provider, bukan perubahan aturan domain.

## Langkah selanjutnya

### dion

- Ubah seluruh label bisnis approval cuti dari **Kepala Bagian** menjadi **Atasan Langsung**, tanpa otomatis mengganti nama role, route, atau field teknis lama.
- Pertahankan urutan `0..n Verifikator → Atasan Langsung → PYBMC`; jika Atasan Langsung dan PYBMC adalah orang yang sama, pejabat tersebut tetap melakukan dua tindakan terpisah.
- Perbarui formulir/PDF agar setiap pihak approval menampilkan **Nama**, **Jabatan**, dan **Peran**, serta rapikan jarak antara kop surat dan tabel.
- Konfirmasikan kepada LLDIKTI batas pembatalan/revisi setelah Verifikator bertindak. Sampai ada keputusan, batas aman yang tercatat adalah sebelum tindakan approval pertama.
- Jangan menghapus cuti final `Disetujui`. Admin Kepegawaian menggunakan status `Ditangguhkan` dengan alasan wajib, histori/audit tetap terjaga, dan saldo dikoreksi melalui ledger.
- Jadikan **Cuti di Luar SIMPEG** sebagai satu sumber fakta untuk data historis/transisi dan pemulihan setelah downtime; halaman **Catat Pemakaian Tahunan** hanya menampilkan agregat read-only.
- Pertahankan flow SIMPEG sebagai jalur operasional normal. Ketika layanan downtime, proses manual harus selesai di luar sistem dan baru dicatat sebagai fakta final setelah SIMPEG pulih.
- Selidiki dan selesaikan kegagalan integrasi WhatsApp `422` berdasarkan kontrak parameter/template provider.
- Tambahkan halaman **Reporting Statistik Kepegawaian** yang terpisah dari Data Master, dashboard, dan export nominatif.
- Pertahankan EWS kenaikan pangkat berdasarkan TMT/SK pangkat terakhir ditambah empat tahun.
- Validasi SK Pengangkatan terhadap status aktif: CPNS memerlukan SK Pengangkatan CPNS dan PNS memerlukan SK Pengangkatan PNS.
- Siapkan evaluasi lanjutan dan pengujian sebelum target peluncuran; penyebutan Oktober pada rapat merupakan sasaran, bukan keputusan tanggal go-live final.

## Ringkasan

### Kemajuan Pengembangan Aplikasi Simpeg

Dion mendemonstrasikan kemajuan SIMPEG dengan lima role: Super Admin, Admin Kepegawaian, Kepala Bagian, Pimpinan, dan Pegawai. Aplikasi mencakup manajemen pegawai, import Excel, dokumen, perhitungan cuti, serta approval chain yang dapat dikonfigurasi. Demonstrasi juga menunjukkan detail pegawai, perubahan status, dokumen wajib, dan pembatasan akses berdasarkan role/permission.

### Demo Sistem Manajemen Cuti

Dion mendemonstrasikan perhitungan saldo dan pengajuan cuti. Kontrak approval yang diklarifikasi adalah `0..n Verifikator → Atasan Langsung → PYBMC`, dengan notifikasi melalui channel yang dikonfigurasi. Sistem juga melacak saldo, menghasilkan PDF dengan QR verifikasi, serta menyediakan EWS untuk event kepegawaian.

### Sistem Pemberitahuan dan Akses Global

Tim membahas konfigurasi channel notifikasi global dan manajemen akses. **Hanya pengguna pertama sistem**, ketika belum ada user sama sekali, yang menjadi Super Admin untuk bootstrap. Pengguna berikutnya dipetakan melalui email/data pegawai dan RBAC yang berlaku; mereka tidak otomatis menjadi Super Admin. Data master dapat dikelola secara terkontrol dan perubahan penting dicatat dalam audit log.

### Diskusi Proses Pengajuan Cuti

Tim membahas kemampuan Pegawai untuk membatalkan atau merevisi pengajuan. Batas setelah Verifikator bertindak tetapi sebelum Atasan Langsung masih menunggu konfirmasi LLDIKTI. Cuti final `Disetujui` tidak dihapus; Admin Kepegawaian dapat menetapkannya `Ditangguhkan` dengan alasan, histori, audit, dan koreksi ledger. Setelah tidak ada pengajuan aktif, Pegawai dapat mengajukan kembali melalui alur normal.

### Kebijakan dan Konfigurasi Cuti

Pertemuan membedakan penangguhan saat pengajuan masih aktif dari penangguhan administratif setelah cuti final disetujui. Penangguhan final harus membalik pemakaian melalui ledger secara atomik tanpa menghapus histori. Untuk EWS kenaikan pangkat, dasar perhitungan tetap TMT/SK pangkat terakhir ditambah empat tahun.

### Tinjauan EWS dan Notifikasi

Tim mengonfirmasi EWS kenaikan pangkat memakai TMT/SK pangkat terakhir sebagai titik awal, kemudian menambahkan empat tahun. Demo WhatsApp menghasilkan respons `422`; tindak lanjutnya adalah memeriksa parameter, template, dan kontrak provider. Konfigurasi channel tetap global; preferensi per pengguna tidak ditetapkan sebagai requirement Fase 1.

### Alur Persetujuan Cuti

Atasan Langsung merupakan peran bisnis yang ditetapkan per pegawai dan dapat dijalankan Kepala Bagian, Kepala Lembaga, atau pejabat lain yang sah. Rantai persetujuan adalah `0..n Verifikator → Atasan Langsung → PYBMC`. Atasan Langsung dan PYBMC tetap merupakan dua tahap meskipun dijalankan orang yang sama. Seluruh tahap yang bertindak ditampilkan berurutan pada PDF.

### Pembaruan Formulir dan Dokumentasi Cuti

Formulir/PDF menampilkan **Nama**, **Jabatan**, dan **Peran** setiap pihak approval. Jabatan mengikuti jabatan aktual yang relevan, termasuk jabatan struktural, fungsional, atau pelaksana. Verifikator bersifat opsional, tetapi setiap Verifikator yang terlibat tetap muncul pada PDF. Fakta Cuti di Luar SIMPEG memengaruhi saldo dan rollover sesuai jenis cutinya.

### Pembaruan Pencatatan Cuti Tahunan

Hasil akhir diskusi menetapkan **Cuti di Luar SIMPEG** sebagai satu pintu pencatatan fakta historis/transisi dan pemulihan setelah downtime. Halaman **Catat Pemakaian Tahunan** tidak menerima angka langsung; halaman tersebut hanya menampilkan agregat yang dihitung dari fakta pemakaian. Saat SIMPEG normal setelah go-live, pengajuan baru wajib memakai alur SIMPEG.

### Implementasi Pelacakan Cuti

Pemakaian historis dan cuti yang diproses manual selama downtime dicatat per kejadian agar dapat diaudit dan dihitung tepat satu kali. Hanya Admin Kepegawaian berwenang dengan permission yang sesuai yang mencatat fakta tersebut. Perubahan status pegawai dan unggah dokumen tetap dibatasi untuk Super Admin/Admin Kepegawaian. Kelengkapan SK Pengangkatan harus cocok dengan status aktif CPNS atau PNS.

### Konfigurasi Rangkaian Persetujuan

Tim membahas penyalinan konfigurasi persetujuan kepada anggota unit agar Admin tidak menyusun Verifikator satu per satu. Chain runtime tetap disimpan per pegawai; template hanya menyalin konfigurasi dan tidak menjadi resolver paralel. Pertemuan lanjutan direncanakan untuk evaluasi progres, sedangkan Oktober disebut sebagai sasaran peluncuran yang masih bergantung pada perbaikan, testing, dan UAT.
