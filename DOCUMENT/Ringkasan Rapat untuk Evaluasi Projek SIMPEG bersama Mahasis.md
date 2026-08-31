# Ringkasan Rapat untuk Evaluasi Projek SIMPEG bersama Mahasiswa Magang Univ Klabat

> Senin, 31 Agustus 2026 · 10.26–12.21 WITA (1 jam 55 menit)

## Rekap cepat

Pertemuan difokuskan untuk menunjukkan kemajuan dan fungsionalitas pengembangan aplikasi SIMPEG, yang mencakup lima peran pengguna: super admin, admin, staf, kepala bagian, dan karyawan. Dion mempresentasikan fitur utama aplikasi termasuk manajemen personil, impor data karyawan, proses aplikasi cuti, alur kerja persetujuan, dan sistem peringatan dini untuk promosi dan perpanjangan kontrak. Tim membahas modifikasi penting termasuk mengubah label "Kepala Bagian" menjadi "Pengawas Langsung" dalam formulir cuti, menambahkan bidang nama karyawan, dan menyempurnakan sistem perhitungan kuota cuti. Beberapa masalah teknis ditangani termasuk masalah saluran pemberitahuan (terutama integrasi WhatsApp dengan kode kesalahan 422), kemampuan pelaporan data master, dan penanganan catatan cuti di luar sistem SIMPEG. Diskusi juga mencakup manajemen akses pengguna, persyaratan pengunggahan dokumen, dan alur proses verifikasi untuk persetujuan cuti.

## Langkah selanjutnya

### dion

- Merancang ulang formulir cuti PDF untuk memasukkan nama pejabat (bukan hanya peran) dan mengganti label "Kepala Bagian" dengan "Pengawas Langsung" dalam alur persetujuan.
- Menerapkan logika untuk pembatalan dan revisi cuti: memungkinkan karyawan untuk membatalkan atau merevisi aplikasi cuti mereka hanya sebelum disetujui oleh atasan langsung; setelah persetujuan, hanya Admin Staf yang dapat menangguhkan atau melarang cuti, yang memungkinkan karyawan untuk mengajukan permohonan kembali.
- Sesuaikan perhitungan kuota cuti hanya berdasarkan fitur "Leave out Simpeg", menonaktifkan input manual dari catatan penggunaan tahunan untuk menghindari duplikasi data.
- Selidiki dan selesaikan masalah dengan saluran pemberitahuan Whatsapp (error 422) untuk aplikasi cuti.
- Tambahkan fitur pelaporan di bagian Master Data untuk menampilkan statistik dalam bentuk bagan untuk setiap kategori (misalnya, peringkat, posisi).
- Menerapkan templat atau fitur pengaturan massal untuk konfigurasi persetujuan cuti untuk memungkinkan pengaturan verifikasi untuk sekelompok karyawan (misalnya, oleh tim kerja) alih-alih satu per satu.
- Pastikan bahwa Sistem Peringatan Dini (EWS) untuk promosi didasarkan pada SK yang diinput terakhir (dokumen penunjukan), bukan periode empat tahun yang tetap.
- Memvalidasi bahwa dokumen SK wajib (penunjukan, pangkat, posisi) sesuai dengan status karyawan saat ini (misalnya, PNS, PPPK) dan diunggah dengan benar.
- Bersiaplah untuk pertemuan berikutnya pada hari Jumat, 11 September, dan bertujuan untuk peluncuran sistem pada bulan Oktober.

## Ringkasan

### Kemajuan Pengembangan Aplikasi Simpeg

Dion mendemonstrasikan kemajuan pengembangan aplikasi simpeg, yang hampir lengkap dengan lima peran pengguna termasuk super admin, admin, staf, kepala bagian, dan karyawan. Aplikasi ini mencakup fitur untuk manajemen personalia, entri data karyawan dengan template Excel, manajemen dokumen, pelacakan cuti dengan perhitungan otomatis, dan alur kerja persetujuan yang dapat dikonfigurasi. Demonstrasi menunjukkan bagaimana sistem menangani detail karyawan, perubahan status, dokumen wajib, dan meninggalkan aplikasi dengan pengaturan otorisasi yang tepat.

### Tinggalkan Demo Sistem Manajemen

Dion mendemonstrasikan sistem manajemen cuti, menjelaskan cara memasukkan saldo cuti karyawan dan memproses permintaan cuti melalui antarmuka admin. Dia menunjukkan alur kerja persetujuan di mana permintaan pertama pergi ke Kepala Departemen, kemudian ke PBMC untuk persetujuan akhir, dengan pemberitahuan dikirim melalui aplikasi, email, dan WhatsApp. Sistem ini mencakup fitur untuk melacak saldo cuti, menghasilkan formulir cuti PDF dengan barcode, dan mengelola Sistem Peringatan Dini untuk tonggak pencapaian karyawan seperti promosi dan perpanjangan kontrak.

### Sistem Pemberitahuan dan Akses Global

Tim membahas implementasi saluran pemberitahuan global dan sistem manajemen akses pengguna. Mereka mengklarifikasi bahwa ketika karyawan masuk untuk pertama kalinya, peran dan izin mereka secara otomatis dipetakan berdasarkan data yang diimpor sebelumnya, dengan pengguna baru mulai sebagai administrator super. Diskusi mencakup bagaimana data master dapat dikelola secara fleksibel, termasuk posisi karyawan, eselon kantor, jenis cuti, dan konfigurasi liburan, dengan semua aktivitas sistem dicatat dalam log audit.

### Tinggalkan Diskusi Proses Aplikasi

Tim membahas proses aplikasi cuti dan fungsionalitas sistem. Abd mengajukan pertanyaan tentang penamaan liburan, persyaratan formulir cuti, dan kemampuan karyawan untuk memodifikasi atau membatalkan permintaan cuti. Kelompok tersebut mengklarifikasi bahwa karyawan dapat memodifikasi aplikasi sebelum persetujuan, tetapi setelah disetujui, hanya administrator staf yang dapat melarang atau menghapusnya, dan karyawan tidak dapat mengirimkan kembali permintaan yang sama setelah penghapusan.

### Tinggalkan Kebijakan dan Konfigurasi Sistem

Pertemuan tersebut membahas kebijakan cuti dan konfigurasi sistem. Dion dan Abd mengklarifikasi bahwa ketika aplikasi cuti karyawan ditangguhkan, itu tidak dihitung terhadap saldo cuti yang disetujui dan kembali ke status sebelumnya. Memang menjelaskan berbagai jenis janji SK, termasuk transfer SK ke SK dan konfigurasi promosi sistem peringatan dini (EWS), mencatat bahwa periode promosi default adalah empat tahun berdasarkan SK yang diinput terakhir.

### Tinjauan Sistem Promosi dan Pemberitahuan

Tim membahas penentuan promosi dan peringkat berdasarkan masukan SK terakhir daripada kerangka waktu empat tahun. Mereka meninjau kemampuan sistem data master untuk pelaporan karyawan khusus, termasuk penyaringan berdasarkan peringkat, posisi, dan departemen. Diskusi juga membahas masalah saluran pemberitahuan, di mana Dion melaporkan bahwa hanya meninggalkan pemberitahuan yang gagal dikirim dengan benar, dengan kode kesalahan 422, dan Sidik menyarankan untuk memeriksa parameter dan mempertimbangkan apakah akan mempertahankan pengaturan pemberitahuan global atau khusus pengguna.

### Tinggalkan Alur Kerja Proses Persetujuan

Diskusi berfokus pada proses persetujuan cuti dan peran yang terlibat dalam alur kerja persetujuan. Sidik_LLDikti dan Abd mengklarifikasi bahwa ada dua kemungkinan pengawas langsung untuk kepala bagian: baik Kepala Departemen atau Kepala LLDikti. Mereka menentukan bahwa aliran persetujuan harus mempertahankan dua langkah yang berbeda - pertama melalui verifier atau supervisor langsung, kemudian ke PBMC - daripada digabungkan menjadi satu langkah. Kelompok ini mengkonfirmasi bahwa semua persetujuan, termasuk verifikasi, akan muncul secara berurutan pada formulir cuti PDF terlepas dari apakah verifikasi tambahan terlibat dalam proses tersebut.

### Tinggalkan Pembaruan Sistem Dokumentasi

Tim membahas cara yang tepat untuk mendokumentasikan posisi pejabat dalam catatan cuti, menentukan bahwa nama harus ditambahkan sebagai kolom sambil berfokus pada posisi struktural pejabat daripada gelar kantor khusus mereka. Mereka mengklarifikasi bahwa verifikasi harus ditandai sebagai opsional karena mereka bukan informasi yang diperlukan, dan sistem harus secara otomatis menghitung kuota cuti berdasarkan input data. Diskusi juga membahas bagaimana menangani catatan cuti di luar sistem SIMPEG, memastikan bahwa input manual untuk cuti di luar SIMPEG tidak akan mempengaruhi perhitungan kuota otomatis.

### Pembaruan Proses Rekaman Cuti Tahunan

Sidik menjelaskan proses pencatatan penggunaan tahunan dan cuti di luar sistem simpeg, menjelaskan bahwa penggunaan tahunan harus dicatat terlebih dahulu, diikuti dengan cuti di luar sistem. Abd mengklarifikasi bahwa sistem harus menangkap data historis dan aplikasi cuti di masa depan, dengan pemahaman bahwa daun di luar simpeg tidak akan lagi diproses ke depan. Diskusi difokuskan pada memastikan semua data cuti yang relevan, termasuk aplikasi masa lalu, dicatat dengan benar dalam sistem.

### Tinggalkan Implementasi Sistem Pelacakan

Tim membahas penerapan sistem pelacakan cuti di mana perhitungan akan didasarkan pada cuti yang diambil di luar sistem yang ada, membutuhkan input manual untuk akuntabilitas yang lebih besar. Mereka mengklarifikasi bahwa hanya administrator yang berwenang (super admin dan admin pagawea) yang dapat mengubah status karyawan dan mengunggah dokumen, bukan karyawan itu sendiri. Diskusi juga mencakup persyaratan validasi untuk dokumen SK (penunjukan), terutama untuk kategori peringkat yang berbeda seperti CPNS, PNS, dan PPPK, memastikan dokumentasi lengkap dipertahankan bahkan ketika status karyawan berubah.

### Pelaksanaan Arus Verifikasi Karyawan

Tim membahas penerapan sistem aliran verifikasi untuk persetujuan karyawan, dengan LLDIKTI XVI mengusulkan pendekatan berbasis template di mana tim dapat menggunakan proses verifikasi standar daripada membuat jalur verifikasi individual untuk setiap karyawan. Sidik_LLDikti menyarankan agar atasan secara langsung menetapkan verifier dan mengusulkan penerapan alur verifikasi yang sama kepada semua karyawan dalam satu unit kerja. Tim setuju untuk menargetkan peluncuran pada bulan Oktober, dengan pertemuan tindak lanjut dijadwalkan untuk Jumat depan (11) untuk mengevaluasi kemajuan dan mempersiapkan implementasi.