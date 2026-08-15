# Transkrip Meeting Evaluasi Pengembangan SIMPEG bersama LLDIKTI

## Informasi rekaman

- **Sumber:** `videoplayback.mp4`
- **Durasi:** 01:17:35
- **Bahasa:** Bahasa Indonesia
- **Tanggal rapat:** tidak disebutkan secara eksplisit dalam rekaman
- **Tanggal transkripsi:** 14 Agustus 2026
- **Mesin transkripsi:** Faster-Whisper, model `small`, pemrosesan lokal
- **Pihak yang terdengar:** perwakilan LLDIKTI, Dion Kobi sebagai presenter, dan tim magang Universitas Klabat

> **Catatan akurasi:** Transkrip ini dibersihkan dari hasil pengenalan suara otomatis dan mempertahankan urutan serta timestamp rekaman. Label pembicara tidak diberikan karena rekaman tidak diproses dengan diarization dan beberapa suara tidak dapat diidentifikasi secara pasti. Istilah domain yang jelas telah dinormalisasi; bagian yang tumpang tindih atau tidak terdengar ditandai tanpa ditebak.

## Pembukaan

**[00:00:02]** Selamat siang, adek-adek magang ini Klabat sekalian. Terima kasih sudah menghadiri evaluasi rutin kita untuk progres pengembangan aplikasi.

**[00:00:14]** Jadi hari ini sebelum kita mulai, mari kita panjatkan doa menurut keyakinan kita masing-masing berdoa di mulai, berdoa selesai.

**[00:00:39]** Baik, jadi kurang lebih kita sudah hampir sebulan yang lalu ya pertemuan terakhir. Jadi kali ini saya ingin ngecek progres untuk sejauh ini sudah sampai di mana.

**[00:00:52]** Jadi mungkin kita bisa langsung saja. Kita ingin ngeliat dan mungkin ngasih sedikit evaluasi barang kali ada. Jadi siapa yang akan presentasi dari Dion nya?

**[00:01:01]** Ya, nanti.

**[00:01:04]** Baik, untuk kali ini saya serahkan kepada Dion. Silakan Dion mempresentasikan dan mendemonstrasikan apa yang sudah dilakukan sejauh ini.

**[00:01:12]** Oke, sebentar saya.

**[00:01:18]** Terima kasih.

## Pemaparan progres dan dashboard

**[00:02:18]** Oke Pak, jadi untuk sistem kami saat ini, untuk progresnya kurang lebih sudah 90 persen.

**[00:02:37]** Dan untuk Sprint 6 itu sudah selesai. Nah kami di Sprint 7 ini fokus di full testing dengan fix bugs.

**[00:02:50]** Jadi fokus di Sprint 7 untuk testing. Jadi yang pertama itu di bagian dashboard seperti ini sudah menggunakan real data yang diambil.

**[00:03:05]** Dari kenaikan pangkat, posisi pegawai, status cuti, ini ada distribusi golongan juga, daftar EWS aktif, trend pegawai dengan aktivitas terkini.

## Data pegawai dan impor

**[00:03:17]** Nah yang pertama itu di data pegawai. Nah untuk data pegawai ini untuk menampakan dia ada dua.

**[00:03:29]** Yang pertama itu tambah manual. Nah tambah manual dengan ada tambah menggunakan import.

**[00:03:39]** Untuk impor, di sini sudah kami sediakan template dalam bentuk Excel.

**[00:03:50]** Jadi bisa langsung diunduh di sini. Nah untuk template-nya itu kurang lebih seperti yang Bapak kirimkan terakhir.

**[00:04:04]** Nah kami mengikuti template itu. Nah ini kurang lebih seperti template-nya.

**[00:04:13]** Nah kemudian dia ketika diunggah. Nah kurang lebih seperti ini.

**[00:04:33]** Oke kita lanjut validasi. Nah di sini saya sengaja tambahkan satu data yang sudah ada.

**[00:04:43]** Nah jadi ini ada error karena email ini sudah ada sebelumnya. Jadi perlu di validasi ulang.

**[00:04:52]** Itu data yang sudah ada. Statusnya masih `skip` karena pada data ini terdapat NIP yang terduplikasi.

**[00:05:03]** Jadi kalau kita ubah, status-nya sudah siap, siap diimpor.

**[00:05:17]** Ini proses import-nya apa? Pake job yang di belakang?

**[00:05:25]** Iya, Pak. Oke, datanya sudah berhasil diimpor.

**[00:05:46]** Kemudian di bagian detail pegawai lebih seperti ini. Jadi setiap pegawai itu nanti bisa ditaruh di sini untuk kepala bagiannya.

**[00:06:05]** Dan juga untuk edit pegawai. Nah untuk edit profil itu dia di sini.

**[00:06:18]** Di sini ada data keluarga, data kontak, dan berkas.

**[00:06:28]** Ada SK pangkat, SK jabatan, SK KGB, dan SK pengangkatan.

**[00:06:35]** Nah ini juga sudah drop-down. Nah ini semua bisa di custom sendiri dari Data Master.

**[00:06:43]** Jadi sudah kami buat flexible untuk jabatan juga.

**[00:06:51]** Jenis jabatan dan eselon juga sudah ada. [Contoh berikutnya tidak terdengar jelas.]

**[00:06:59]** Untuk pegawai yang sudah lengkap. Oke ini boleh tambahkan keluarga.

**[00:07:18]** Kemudian ini ada kepangkatan, jabatan.

**[00:07:25]** Kemudian ada KGB, ukuman disiplin, pendidikan.

**[00:07:30]** Nah ini pengangkatan dengan ini dokumen SK dari pegawai ini.

**[00:07:37]** Dokumen SK itu bisa ditambahkan sendiri ya?

**[00:07:47]** Iya bisa bisa.

**[00:07:50]** Dia ada nanya sendiri atau dari profilnya?

**[00:07:52]** Untuk dokumen SK itu sendiri dia di edit pegawai sini.

**[00:08:00]** Itu hanya admin yang bisa menamakan. Nah ini dokumen SK.

**[00:08:06]** SK pangkat, SK jabatan, SK KGB dengan pengangkatan.

**[00:08:12]** Berarti unggahan filenya hanya sebatas itu atau ada yang lain?

**[00:08:15]** Nah sebenarnya ada satu lagi. Cuman belum ditambahkan itu dokumen lainnya.

**[00:08:26]** Disini?

**[00:08:28]** Belum ditambahkan dokumen ini.

**[00:08:36]** Di sini ijazah, KTP, atau dokumen lainnya bisa ditambahkan.

**[00:08:44]** Nah ini rcp dokumen.

**[00:08:50]** Kemudian untuk statusnya.

**[00:08:54]** Nah kalau sudah lengkap, lebih sure ini bisa langsung di cek juga.

**[00:09:02]** Nah ini track yang di bagian ekspor pegawai sudah dibuat flexible juga.

**[00:09:18]** Jadi bisa di custom.

**[00:09:20]** Nah sebenarnya dari data pegawai ini sudah bisa diekspor.

**[00:09:23]** Cuman yang diekspor itu data yang sudah di data default.

**[00:09:31]** Nah dia hasilnya sekurang lebih sure ini.

**[00:09:34]** Kalau yang dari data pegawai, cuman kalau mau di custom juga bisa.

**[00:09:40]** Di custom hanya mau ambil nip nama pegawai golongan buat batan.

**[00:09:49]** Nah previewnya ada di bawah sini.

**[00:09:52]** Nah ini boleh PDF dan boleh Excel.

**[00:09:58]** [Bagian ini tidak terdengar jelas.]

**[00:10:02]** Punggung seperti ini untuk export.

## Alur pengajuan cuti

**[00:10:07]** Terus kita lanjut di flow pengajuan tutuan.

**[00:10:24]** Jadi disini saya sudah buka 5 role di 5 browser beda.

**[00:10:30]** Ayo untuk profil.

**[00:10:36]** Nah jadi untuk sekarang yang kita buat, pegawai itu belum bisa update profil.

**[00:10:42]** Jadi yang di fase satu itu untuk edit profil pegawai kepangkatan itu semua dari admin.

**[00:10:53]** Jadi yang boleh itu admin kepegawaian dengan super admin.

**[00:10:59]** Nah jadi mau coba flow cuti dulu.

**[00:11:06]** Nah flow pertama itu dari cuti yang kita harus input ini dulu.

**[00:11:15]** Administrasi saldo awal.

**[00:11:22]** Nah jadi untuk yang berasaran meeting kemarin ada pendaftaran saldo awal.

**[00:11:31]** N2 itu maksimal 6.

**[00:11:33]** Ini 6 kalau yang tahun saat ini maksimal 12 ya lah.

**[00:11:39]** Ya betul.

**[00:11:42]** Untuk pegawai.

**[00:11:57]** Nah untuk pegawai disini ketika dia ajukan cuti.

**[00:12:10]** Dan sini sudah ada dia punya saldo tersedia.

**[00:12:17]** Nah untuk cuti sendiri berdasarkan dari hasil meeting terakhir itu.

**[00:12:26]** Untuk saldo cuti ini yang dipotong di cuti tahunan.

**[00:12:34]** Di cuti tahunan untuk yang saldo cuti.

**[00:12:39]** Nah untuk flow cuti sakit atau melahirkan itu dia mau di verifikasi lagi dari.

**[00:12:51]** Untuk sistemnya seperti apa.

**[00:12:56]** Apakah nanti dia akan dipotong juga?

**[00:12:58]** Ada saldo tersendiri?

**[00:13:04]** Engga-engga kalau saldo itu cuma untuk cuti tahunan kalau yang cuti sakit,.

**[00:13:10]** Cuti melahirkan, cuti alasan benda itu enggak mau motong saldo cuti.

**[00:13:13]** Oh iya.

**[00:13:14]** Jadi sudah sesuai flow yang saat ini.

**[00:13:17]** Jadi cuma cuti tahunan saja yang pakai potongan saldo.

**[00:13:21]** Nah untuk cuti sendiri dia ketika pegawai mengajukan cuti.

**[00:13:27]** Kemudian dia ada di hari libur itu enggak akan terpotong di ini.

**[00:13:33]** Iya enggak akan terpotong karena cuti itu potongannya di hari kerjato.

**[00:13:37]** Jadi kalau misalnya dia ngambil cuti-nya rabuk-krabuk berarti satu minggungnya enggak masuk.

**[00:13:41]** Ya betul.

**[00:13:45]** Ini testing dari sini.

**[00:14:04]** Oh iya sudah tengah 17.

**[00:14:06]** Tapi ini sudah menghitung hari libur juga enggak?

**[00:14:08]** Iya sudah sudah.

**[00:14:10]** Sudah ya.

**[00:14:11]** Ada tabel masternya juga kan hari liburnya kemarin.

**[00:14:13]** Hari libur sudah sudah.

**[00:14:15]** Sudah ada tabel master.

**[00:14:28]** Nah ini untuk pilampir ini dibuat optional ya.

**[00:14:31]** Iya optional.

**[00:14:34]** Nah ini untuk proses persetujuannya itu di konfigurasi dulu.

**[00:14:47]** Nah ini belum bisa mengajukan cuti karena data temen-temen pengangkatan.

**[00:14:51]** Pegawai ini belum ditambahkan untuk pegawai itu sendiri.

## Konfigurasi rantai persetujuan cuti

**[00:15:13]** Nah di sini untuk konfigurasi ada konfigurasi profil cuti ini juga harus di set-up di awal.

**[00:15:20]** Cuma yang sebelumnya itu sudah saya set-up.

**[00:15:24]** Jadi PYBMC itu bisa ditambahkan di sini.

**[00:15:32]** Nah itu bisa di apply ke global.

**[00:15:36]** Jadi PYBMC, misalnya [nama kurang jelas].

**[00:15:40]** Nah di sini.

**[00:16:04]** Nah jadi semua perubahan di sini ada yang tercatat di perubahan konfigurasi.

**[00:16:11]** Oke ini sudah berhasil.

**[00:16:14]** Nah sekarang cari main yang pegawai yang tadi.

**[00:16:24]** Nah untuk pegawai ini dia kepala bagiannya sudah ditetapkan.

**[00:16:34]** Nah kalau belum bisa ditambahkan dari sini juga.

**[00:16:37]** Untuk kepala bagiannya sih itu siapa?

**[00:16:41]** Siapa?

**[00:16:42]** Kalau masalah yang kepala bagian ini diset-nya pas di profil tadi ya?

**[00:16:47]** Iya di profil.

**[00:16:49]** Jadi untuk user yang sudah ada kepala bagian ketika di backfill dia akan muncul.

**[00:17:00]** Kalau diubah lagi di sini berarti dia pengaruh lagi yang di profil ya?

**[00:17:05]** Ya di profil juga akan ikut terubah.

**[00:17:08]** Cuma kalau misalnya di profil sudah ada.

**[00:17:12]** Di sini dia sudah ada nanti seperti ini.

**[00:17:17]** Jadi sudah tidak perlu diubah lagi.

**[00:17:19]** Nah ini kepala bagiannya.

**[00:17:28]** Kemudian bisa juga ditambahkan verifikator.

**[00:17:33]** Mungkin dari tim di kepagawain.

**[00:17:39]** Nah ini bisa ditambahkan tim unit kerja.

**[00:17:45]** Kemudian kalau misalnya tidak mau ditambahkan dia langsung ke PYBMC.

**[00:17:51]** Bisa digunakan PYBMC global.

**[00:17:55]** Itu [nama kurang jelas] sendiri.

**[00:17:57]** Kalau backfill chain itu apa?

**[00:18:10]** Untuk bagian `backfill chain`, Jordan yang mengerjakan.

**[00:18:22]** Kalau yang ke kepala bagian itu itu yang kepala bagian kain apa?

**[00:18:29]** Jadi kalau kepala bagian sudah di set di profil tadi.

**[00:18:34]** Di bagian cuti ketika jalankan backfill chain.

**[00:18:38]** Dia langsung mengambil kepala bagian dari masing-masing pegawai sudah di set.

**[00:18:44]** Terus langsung masukkan ke chain of profil pegawai.

**[00:18:48]** Pegawai yang chain of profil cuti.

**[00:18:52]** Jadi sudah manual seksual satu per satu.

**[00:18:57]** Jadi otomatis.

**[00:18:59]** Langsung di ibaranya seperti diimpor otomatis.

**[00:19:02]** Siapa verifikatornya gitu?

**[00:19:05]** Kalau verifikatornya itu ditambah manual.

**[00:19:07]** Sama yang diambil itu kepala bagian yang masing-masing pegawai.

**[00:19:12]** Yang sudah di set di profil di awal.

**[00:19:16]** Berarti nanti perantai approvalnya ini kepala bagian.

**[00:19:22]** Verifikator dulu baru kepala bagian kan?

**[00:19:26]** Ya kalau ini kepala bagian terus ke verifikator.

**[00:19:31]** Oke.

**[00:19:53]** Tapi kalau misalnya dia tidak tambah verifikator lagi.

**[00:19:57]** Itu otomatis langsung ke kepala bagian.

**[00:20:02]** Kalau tidak tambah verifikator langsung ke kepala bagian.

**[00:20:06]** Tapi flow-nya gini nih.

**[00:20:09]** Kalau misalnya ada yang mau ngajuin cuti itu kan.

**[00:20:13]** Flow-nya masuknya ke kepagawain dulu.

**[00:20:16]** Baru ke kepala bagian.

**[00:20:17]** Ke kepala bagian itu kan biasanya ke kepala bagian umum itu.

**[00:20:22]** Biasanya sebelum [nama kurang jelas].

**[00:20:25]** Nah kepala bagian juga ini ada dua kategori ini.

**[00:20:29]** Ada yang masuknya ketua tim kerja.

**[00:20:31]** Tapi kalau ketua tim kerja harus masuk verifikator biasa gak apa-apa.

**[00:20:34]** Tetapi Kepala Bagian tetap berada satu tingkat di bawah [nama kurang jelas].

**[00:20:39]** Kalau dari alurnya sekarang kan diusulkan.

**[00:20:42]** Kepala bagian validasi dulu terus verifikator kan.

**[00:20:45]** Kalau posisinya verifikatornya kepegawaian kan di baratnya gak bertingkat jadinya.

**[00:20:50]** Jadi udah naik ke kepala bagian ke bossnya tapi turun lagi ke pegawai gitu kan.

**[00:20:54]** Padahal sebenarnya dibalik gitu.

**[00:20:56]** Harusnya dari stuck dulu yang ditentukan entah itu kepegawaian.

**[00:20:59]** Ke ketua timnya baru ke kepala bagian.

**[00:21:03]** Karena kepala bagian itu tingkatannya dibawa dari kepala lembaga gitu.

**[00:21:06]** Berarti flow-nya ke verifikator dulu ya.

**[00:21:11]** Ya betul.

**[00:21:12]** Verifikator dulu karena kan nanti meskipun nanti ada.

**[00:21:16]** Deset-desetnya ketua tim kerja itu kan kalau posisinya di balik.

**[00:21:21]** Tinggal ditambahin aja di bagian verifikator gitu kan.

**[00:21:23]** Tetap pun jujunya kalau udah valid pasti maksudnya ke kepala bagian gitu kan.

**[00:21:28]** Oke lanjut.

**[00:21:35]** Flow-nya di balik ya dari verifikator dulu baru ke kepala bagian.

**[00:21:40]** Verifikator dulu karena verifikator ini kan dinamis dia sifatnya.

**[00:21:43]** Itu verifikator itu penjaga gerbang awal gitu.

**[00:21:45]** Ke kepala bagian itu udah hampir pasti lah.

**[00:21:47]** Barannya atasannya pegawai itu.

**[00:21:50]** Ya berarti.

**[00:21:58]** Nah untuk flow- cuti kita coba dengan cuti.

**[00:22:08]** Kalau tim itu kita saja.

**[00:22:10]** Di bagian yang sudah ada.

## Usulan fitur switch role

**[00:22:22]** Oh yang untuk flow- cuti begini.

**[00:22:34]** Sebenarnya sudah dibuat sih.

**[00:22:36]** Ini saja dia nanti di simpaknya itu kalau yang misalnya rolinya sebagai super admin.

**[00:22:49]** Itu ditambahin fitur ini aja fitur change role.

**[00:22:53]** Jadi ditambah user-nya itu ditambahin kolom temporary user.

**[00:22:57]** Sama temporary permission gitu kan.

**[00:23:00]** Temporary role menurutnya.

**[00:23:02]** Jadinya kalau misalnya itu memudahkan buat demo-demo juga.

**[00:23:05]** Atau mengetes fitur gitu kan jadinya dari super admin itu.

**[00:23:08]** Tinggal ganti-ganti role aja dari satu menu gitu.

**[00:23:10]** Jadi di menu drop-down user itu tinggal pilih ganti role.

**[00:23:14]** Nah itu dia bakal ngisi di bagian kolom temporary role.

**[00:23:19]** Sama temporary permission gitu.

**[00:23:22]** Jadinya nanti kalau misalnya mau refer-troll-nya lagi.

**[00:23:26]** Atau mau di-set ke dev-out ke role bawahannya itu.

**[00:23:28]** Nggak bakal mengganggu gitu.

**[00:23:31]** Kalau sekarang kan cas-nya dia 5 akun terpisah.

**[00:23:35]** Iya 5 akun terpisah.

**[00:23:37]** Dia kan agak bingung kalau di demo.

**[00:23:39]** Kalau misalnya mau di-testing juga kan harus log-in.

**[00:23:42]** Log-out log-in log-out lagi gitu kan.

**[00:23:44]** Nah nanti kalau buat di user-nya itu.

**[00:23:47]** Ditambahin aja fitur ini fitur switch role.

**[00:23:50]** Jadi switch role-nya itu nanti logikannya dia.

**[00:23:53]** Kalau misalnya dia ganti role itu nanti.

**[00:23:55]** Otomatis dia bakal pre-fill ke kolom temporary role.

**[00:23:59]** Sama temporary user.

**[00:24:00]** Jadi sekalipun dia log-out dia log-in lagi.

**[00:24:02]** Role-nya masih sama gitu tapi dia bisa di-revert.

**[00:24:04]** Kalau misalnya dia role-nya di-revert.

**[00:24:06]** Itu bakal dikosongin temporary role.

**[00:24:08]** Sama temporary permission gitu.

**[00:24:10]** Nanti dia bakal nge-check kan.

**[00:24:12]** Untuk develop-ment ya pak?

**[00:24:15]** Ya development sama production juga.

**[00:24:17]** Karena kan misalnya nih kalau.

**[00:24:20]** Pegawai ngelaporin bak eh ini kan.

**[00:24:22]** Di perspektif mereka di perspektif pegawai gitu kan.

**[00:24:25]** Kan agak ribet juga minta eh coba kirimin.

**[00:24:27]** User-nya password gitu kan.

**[00:24:29]** Nah kalau misalnya dari super admin ada switch role-nya kan.

**[00:24:31]** Bisa memposisikan diri dia itu sebagai.

**[00:24:33]** Pegawai gitu kan.

**[00:24:36]** Dia bisa langsung nge-check gitu.

**[00:24:40]** Oke pak.

**[00:24:43]** Pakai lanjut di.

**[00:24:45]** Flow-lajuan cuti.

**[00:24:47]** Nah ini untuk flow-nya.

**[00:24:51]** Yang kami sudah buat seperti ini.

**[00:24:53]** Di cuti tahunan.

**[00:24:55]** Setelah berhasil ini.

**[00:25:23]** Dari.

**[00:25:25]** Kepala bagian yang.

**[00:25:27]** Menyetujui.

**[00:25:31]** Ini sudah berat.

**[00:25:38]** Nah ini kemudian.

**[00:25:41]** Di fase dua dari.

**[00:25:43]** PYBMC.

**[00:25:53]** Untuk PYBMC itu cuman.

**[00:25:55]** Itu ya Pak?

**[00:25:58]** Nah iya itu biasanya pimpinan tertinggi.

**[00:26:00]** Oh iya.

**[00:26:33]** Ini berhasil.

**[00:26:38]** Jadi setelah.

**[00:26:40]** Dua tahap ini disetujui.

**[00:26:44]** Seluruhnya otomatis akan terpotong.

**[00:26:52]** Oke kalau bisa seperti ini.

**[00:27:00]** Kemudian.

## EWS dan Data Master

**[00:27:02]** Untuk.

**[00:27:04]** EWS sendiri sudah.

**[00:27:07]** Nah EWS sendiri kalau yang kami buat sekarang.

**[00:27:10]** Dia masih.

**[00:27:12]** Ini ya dari notif.

**[00:27:15]** Dari notif via app.

**[00:27:17]** Nah untuk yang dari email.

**[00:27:19]** Itu belum.

**[00:27:20]** Kenal rencana di akhirnya.

**[00:27:22]** Nah untuk EWS ini bisa di.

**[00:27:26]** Setting di konfigurasi EWS.

**[00:27:29]** Nah jadi ada untuk.

**[00:27:32]** Kenakan pangkat KGB.

**[00:27:34]** BUP Pensin Global.

**[00:27:36]** Masa pungkat PPPK dengan.

**[00:27:38]** Milestone Satyalancana.

**[00:27:40]** Nah ini bisa untuk.

**[00:27:43]** Peringatannya dia.

**[00:27:45]** Bisa di setting Amin 3.

**[00:27:47]** Amin 2 atau Amin 1.

**[00:27:50]** Itu dari setting ini untuk.

**[00:27:52]** EWS.

**[00:28:00]** Nah ini EWS yang masuk.

**[00:28:02]** Nanti akan masuk di.

**[00:28:05]** Alaman EWS active.

**[00:28:08]** Kemudian.

**[00:28:12]** Data Master-nya yang ini.

**[00:28:16]** Yang sudah kami buat.

**[00:28:19]** Untuk data master dari.

**[00:28:22]** Golongan pangkat.

**[00:28:24]** Ini boleh mau tambah atau mau di update.

**[00:28:26]** Boleh.

**[00:28:27]** Dan di sejabatan.

**[00:28:31]** Yang sejabatan itu sendiri.

**[00:28:33]** Eselon.

**[00:28:37]** Dia ada status.

**[00:28:39]** Status pegawai.

**[00:28:42]** Ini bisa di custom sini.

**[00:28:44]** Dan jenis cuti.

**[00:28:47]** Agama.

**[00:28:52]** Ini ada juga jajang pedidikan.

**[00:28:54]** Unit kerja dengan.

**[00:28:56]** Hari libur.

**[00:28:58]** Data master.

**[00:29:07]** Dia.

**[00:29:08]** Beda menu hari libur yang di.

**[00:29:13]** Referensi dengan yang di.

**[00:29:15]** Sebelah kiri itu apa?

**[00:29:18]** Yang di sini Pak.

**[00:29:21]** Nah yang di sini.

**[00:29:32]** Di sini dia.

**[00:29:34]** Hari libur yang sudah ada sebelumnya.

**[00:29:36]** Dari.

**[00:29:38]** Dari misalnya untuk.

**[00:29:40]** Sebenarnya ini.

**[00:29:42]** Kepercanaannya mau dibikin dia.

**[00:29:44]** Kayak table calendars gitu Pak.

**[00:29:46]** Tungan.

**[00:29:49]** Yang awal.

**[00:29:51]** Ini masih yang awal kami terapkan sebetulnya.

**[00:29:53]** Dia bersama kayak yang di data master.

**[00:29:55]** Kayak.

**[00:29:57]** Tampilanannya saja.

## Hari libur, akses pengguna, SSO, dan WhatsApp Business

**[00:30:00]** Berarti dia sama aja ini ya?

**[00:30:02]** Ini yang mau di hapus status dari data master.

**[00:30:04]** Yang mau di pindah ke sini atau bagaimana?

**[00:30:06]** Yang dari data master.

**[00:30:09]** Nanti ketika di update.

**[00:30:11]** Dia akan masuk di hari libur ini.

**[00:30:19]** Oh ini aja di.

**[00:30:21]** Hari libur itu di lepas dari data.

**[00:30:23]** Masternya, di taruh di hari libur.

**[00:30:25]** Di bagian atasnya itu.

**[00:30:27]** Bikin modelan calendar.

**[00:30:29]** Di bawahnya tabelnya gitu.

**[00:30:31]** Jadi kan lebih informatif.

**[00:30:35]** Oke.

**[00:30:37]** Modian.

**[00:30:45]** Ini untuk.

**[00:30:53]** Keloal access user.

**[00:30:56]** Ini untuk.

**[00:30:58]** Keycloak ID nya tercatat.

**[00:31:00]** Di sini.

**[00:31:03]** Nah untuk email.

**[00:31:10]** Pilihan.

**[00:31:12]** Pilihan.

**[00:31:14]** Pilihan.

**[00:31:18]** Pilihan.

**[00:31:21]** Pilihan.

**[00:31:23]** Nah untuk email.

**[00:31:25]** Dari Grantly.

**[00:31:27]** Yang ingin.

**[00:31:35]** Confirmasi lebih langsung.

**[00:31:37]** Bagian.

**[00:31:39]** SSO kan.

**[00:31:41]** Yang diminta kan nanti.

**[00:31:43]** SSO nya itu kan di mapping.

**[00:31:45]** Berdasarkan email nya.

**[00:31:47]** Nah.

**[00:31:49]** Berarti.

**[00:31:51]** Di SSO menurut.

**[00:31:53]** Dari pandangan kami di SSO nya.

**[00:31:55]** Di itu ada email.

**[00:31:57]** Nah kami.

**[00:31:59]** Saat ini belum bisa.

**[00:32:02]** Implementasikan full.

**[00:32:04]** Untuk SSO nya karena.

**[00:32:06]** Di akun yang.

**[00:32:08]** Diberikan kepada kami itu belum punya email.

**[00:32:10]** Di SSO.

**[00:32:12]** Nah ini butuh confirmasi ulang ke.

**[00:32:14]** Apakah.

**[00:32:16]** Kami butuh email yang.

**[00:32:18]** Di akun kami ini butuh.

**[00:32:20]** Email yang sudah terdaftar.

**[00:32:22]** SSO untuk nanti.

**[00:32:24]** Kami tes full untuk login dan.

**[00:32:26]** Akan dimaping otomatis.

**[00:32:30]** Boleh-boleh nanti di email nya.

**[00:32:32]** Dikirim aja nanti.

**[00:32:34]** Saya isi dari SSO nya.

**[00:32:36]** Email nya sekalian.

**[00:32:38]** Nama ini daftar, daftar role nya.

**[00:32:40]** Soalnya kan nanti pun di mapping juga kan role nya.

**[00:32:42]** Jadi role default nya pegawai itu kan.

**[00:32:44]** Mau di set langsung dari SSO gitu kalau.

**[00:32:46]** Misalnya dia pegawai nanti.

**[00:32:48]** Biar pas di login kan dia langsung.

**[00:32:50]** Otomatis mapping gitu kan.

**[00:32:52]** Selain email apalagi.

**[00:32:54]** Apa mungkin nomor HP gitu ya.

**[00:32:57]** Nomor HP.

**[00:32:59]** Kalau di SSO.

**[00:33:01]** Itu punya datang.

**[00:33:03]** Untuk nomor HP mimpan.

**[00:33:05]** Itu ada cuman dia.

**[00:33:07]** Jadi custom attribute.

**[00:33:09]** Jadinya kalau misalnya sudah saya.

**[00:33:11]** Tambahkan misalnya itu nanti.

**[00:33:13]** Sebelum login itu kan bisa.

**[00:33:15]** Di capture dulu kan.

**[00:33:17]** Respon yang dikasih sama dari.

**[00:33:19]** SSO nya, nanti kalian bisa mapping aja.

**[00:33:21]** Dari situ, udah tanya.

**[00:33:23]** Nanti bisa kelihatan kalau.

**[00:33:25]** Misalnya dia ada nomor HP nya.

**[00:33:27]** Itu masuknya di objek mana gitu.

**[00:33:29]** Objeknya apa kayaknya apa gitu.

**[00:33:36]** Terus untuk yang apa.

**[00:33:38]** Ini kan nanti mau sekalian.

**[00:33:40]** Diintegrasikan dengan.

**[00:33:42]** WhatsApp business juga.

**[00:33:44]** Nah di WhatsApp business itu kenapa saya.

**[00:33:46]** Minta undur di terakhir itu karena.

**[00:33:48]** Harus dibikin template dulu.

**[00:33:50]** Jadi template nya itu, template pesan yang mau dikirim.

**[00:33:52]** Itu kan mau butuh di approve.

**[00:33:54]** Dari pihak meta langsung gitu ya.

**[00:33:56]** Nah nanti kalian kalau misalnya mau dibikin.

**[00:33:58]** Template.

**[00:34:00]** Bikin notifikasi buat WA.

**[00:34:02]** Itu disediakan juga ini ya.

**[00:34:04]** Dalam bentuk dokumen aja misalnya.

**[00:34:06]** Model pesan WA.

**[00:34:08]** Itu seperti apa sekaligus.

**[00:34:10]** Variable nya gitu.

**[00:34:12]** Karena itu mau diinputkan nanti.

**[00:34:14]** Ke pengusulan template pesannya.

**[00:34:16]** Nanti kalau integrasi ke WA nya itu dia bukan.

**[00:34:18]** Bukan kita ngisi.

**[00:34:20]** Pesan biasa tapi lebih kayak kita.

**[00:34:22]** Ngarahin ke template mana variable apa yang kita.

**[00:34:24]** Lempar gitu.

**[00:34:27]** Jadi nanti kalau misalnya sudah ada.

**[00:34:30]** Gambaran notifikasi.

**[00:34:32]** WhatsApp nya pesannya seperti apa.

**[00:34:34]** Itu nanti dikirim saja entah itu dalam.

**[00:34:36]** Bentuk PDF atau apa biar nanti saya.

**[00:34:38]** Buatkan template nya nanti saya.

**[00:34:40]** Kirim balik ininya.

**[00:34:42]** Template ID nya.

**[00:34:45]** Dengan gimana cara.

**[00:34:47]** Pasang nya gitu biar nanti kalian bisa.

**[00:34:49]** Testing-testing gitu yang penting.

**[00:34:51]** Template nya ada dulu gitu template bakunya.

**[00:34:53]** Barang kali misalnya dia ada.

**[00:34:55]** 3 model pesan 4 model pesan itu gak apa-apa.

**[00:34:57]** Karena perlu saya ajukan.

**[00:34:59]** Dulu kan dia sistemnya template.

**[00:35:01]** Jadi gak sebatas.

**[00:35:03]** Kita kirim pesan terus langsung.

**[00:35:05]** Dari WA nya ngirim gak itu lebih.

**[00:35:07]** Kayak template dulu yang diterima dari.

**[00:35:09]** WA nya itu cuman variable-variable.

**[00:35:11]** Variable dari.

**[00:35:13]** Template nya gitu.

**[00:35:18]** Jika memakan 3.

**[00:35:31]** Okay, next apa lagi.

**[00:35:35]** Selanjutnya.

## Validasi pengajuan cuti

**[00:35:45]** Terus untuk pengajuan cuti itu.

**[00:35:47]** Tadi coba bukan menurut pengajuan cuti.

**[00:35:49]** Dia.

**[00:35:51]** Oh yang pengajuan cuti.

**[00:35:54]** Nah.

**[00:35:56]** Ini coba ajukan cuti baru.

**[00:35:58]** Ini tadi.

**[00:36:01]** Katanya ada validasi ya kalau misalnya.

**[00:36:03]** Saldo nya belum di.

**[00:36:05]** Ini belum diisi.

**[00:36:07]** Oh ada.

**[00:36:09]** Nggak.

**[00:36:26]** Bawa.

**[00:37:04]** Ini yang di validasi.

**[00:37:06]** Kalau misalnya.

**[00:37:08]** Saldo cuti nya sudah lewat.

**[00:37:10]** Dengan yang di.

**[00:37:12]** Lintas tahun.

**[00:37:15]** Nah untuk cuti lintas tahun itu juga.

**[00:37:18]** Gak bisa ya.

**[00:37:20]** Dibuat.

**[00:37:28]** Ya.

**[00:37:32]** Di december.

**[00:37:35]** Nah ini.

**[00:37:49]** Nah ini dia.

**[00:37:53]** Tahun kalender.

**[00:37:55]** Jadi harus dibuat.

**[00:37:58]** Cuti terpisah.

**[00:38:02]** Terima kasih.

**[00:38:10–00:39:55]** [Bagian demonstrasi tidak terdengar jelas; terdapat jeda dan pengulangan singkat.]

**[00:39:58]** Nah terus ini.

## Pembahasan kuota dan saldo cuti

**[00:40:00]** Perhitungan cutinya.

**[00:40:02]** Ini kenapa bisa sampai 20 hari itu.

**[00:40:04]** Nah yang 20 hari ini.

**[00:40:08]** Dia akan.

**[00:40:10]** Terpotong dari.

**[00:40:12]** Yang n2 dulu.

**[00:40:15]** N2 kan tadi.

**[00:40:17]** N1.

**[00:40:19]** N6.

**[00:40:21]** Yang.

**[00:40:23]** Tahun saat ini yang n itu dia.

**[00:40:25]** 8.

**[00:40:27]** Jadi totalnya 20.

**[00:40:29]** Jadi maksimal.

**[00:40:31]** Cuti tahunan itu dia.

**[00:40:33]** 24.

**[00:40:35]** Dari tahun n2 yang 1.

**[00:40:37]** Dengan tahun saat ini.

**[00:40:40]** Tapi kaya n2 nya dia ada.

**[00:40:42]** Misalnya n2 nya itu dia ada sisa cutinya.

**[00:40:44]** Berapa gitu.

**[00:40:47]** Coba lihat menu.

**[00:40:49]** Menu administratif kuota cuti dulu deh.

**[00:40:51]** Saldo cuti.

**[00:40:55]** Nah coba set.

**[00:40:58]** Satu pegawai.

**[00:41:08]** Yang sebenernya.

**[00:41:14]** Nah yang ini.

**[00:41:16]** Yang.

**[00:41:23]** Jadi dia.

**[00:41:49]** Yang kami buat itu dia.

**[00:41:51]** Untuk.

**[00:41:53]** Pemutungannya nanti.

**[00:41:55]** Akan diambil dari yang n2 dulu.

**[00:41:57]** Dia dari.

**[00:41:59]** Belakang ke depan.

**[00:42:01]** Yang n2 setelah yang ini.

**[00:42:03]** Sudah habis.

**[00:42:05]** Baru akan dipotong dari yang n1.

**[00:42:07]** Baru yang tahun sekarang.

**[00:42:10]** Bentar-bentar.

**[00:42:12]** Ini gimana.

**[00:42:14]** Saya bacanya ini.

**[00:42:16]** Saya lihat sisa.

**[00:42:18]** Kuota cutinya itu di mana?

**[00:42:21]** Kalau di menu sini.

**[00:42:24]** Nah kalau yang di sini.

**[00:42:26]** Itu belum ada ya.

**[00:42:30]** Dari sini.

**[00:42:33]** Yang itu.

**[00:42:35]** Mungkin nanti akan ditambahkan.

**[00:42:37]** Nah ini berarti angka-angka yang ditaruh disini.

**[00:42:39]** Apakah kuota cuti yang terpakai.

**[00:42:41]** Atau sisa kuota cuti.

**[00:42:43]** Ini.

**[00:42:47]** Konfigurasi cuti awal.

**[00:42:52]** Untuk saldo awal.

**[00:42:54]** Saldo awal.

**[00:42:56]** Berarti dia dapatnya di 2024.

**[00:42:58]** Sisa 6 gitu.

**[00:43:00]** Karena.

**[00:43:02]** Nanti untuk.

**[00:43:04]** Setiap pegawai akan diinputkan untuk.

**[00:43:06]** Saldo awalnya.

**[00:43:10]** Jadi.

**[00:43:12]** Untuk cuti ini.

**[00:43:15]** Dia memang peritungannya agak tricky.

**[00:43:17]** Tadi kuota cutinya bisa sampai 20 hari.

**[00:43:19]** 20 kan itu sebenarnya.

**[00:43:21]** Tidak lajim itu.

**[00:43:23]** Jadi misalnya kalau dia.

**[00:43:25]** Kalau di posisi UI nya yang sekarang ya.

**[00:43:27]** Dia sisa cuti kan.

**[00:43:29]** 2024, 6 nih.

**[00:43:31]** 2025, 6.

**[00:43:33]** Nah besi selain tahun berjalan ini.

**[00:43:35]** Angka dari mana di input sendiri apa.

**[00:43:37]** Pertungan atau gimana.

**[00:43:42]** Nah kalau yang besi selain tahun berjalan.

**[00:43:44]** Dia.

**[00:43:47]** Setiap tahun itu.

**[00:43:49]** Akan diambil otomatis 12.

**[00:43:51]** Nah jadi dia.

**[00:43:55]** Setiap masuk ke tahun baru.

**[00:43:57]** Di januari awal.

**[00:43:59]** Nah dia untuk.

**[00:44:01]** Cutinya itu otomatis.

**[00:44:03]** Akan 12.

**[00:44:05]** Cuman kalau yang untuk.

**[00:44:07]** Konfigurasi awal karena ini sudah.

**[00:44:09]** Masuk di pertengganan tahun.

**[00:44:11]** Akan di inputkan untuk sisa saldo yang tahun ini.

**[00:44:13]** Karena akan ditambahkan.

**[00:44:15]** Untuk pendaftaran saldo awal.

**[00:44:17]** Di besi selain tahun saat imbul.

**[00:44:19]** Tapi nanti untuk yang.

**[00:44:25]** Di tahun 2027.

**[00:44:27]** Januari itu.

**[00:44:29]** Saldo nya akan otomatis.

**[00:44:31]** Di update jadi.

**[00:44:33]** Maksimal 12.

**[00:44:40]** Bentar ya.

**[00:44:43]** Jadi ini.

**[00:44:52]** Logikanya.

**[00:44:55]** Setiap tahun kan.

**[00:44:57]** Kalau gawa itu pasti dapat.

**[00:44:59]** Jata cuti 12 kan.

**[00:45:01]** Dari baik dari.

**[00:45:03]** 2024-2025.

**[00:45:05]** 2026.

**[00:45:07]** Nah kalau dia.

**[00:45:09]** 2 tahun berturut-turut di 2024-2025.

**[00:45:11]** Dia yang gak ambil cuti itu kan.

**[00:45:13]** Logikanya dia dapat 24.

**[00:45:15]** Kalau ditambah dengan tahun sekarang.

**[00:45:17]** Kuota cutinya berarti berapa? 36, kan?

**[00:45:19]** Nah tapi.

**[00:45:21]** Kuota cuti itu di aturnya cuman.

**[00:45:23]** Maksimal 24.

**[00:45:25]** Kalau di 2024.

**[00:45:27]** Dengan 2025 itu dia.

**[00:45:29]** Tidak pernah ambil cuti sama sekali.

**[00:45:31]** Nah posisinya kan ini.

**[00:45:33]** Besi selain yang 2024 itu kan udah 6.

**[00:45:35]** Ya kan.

**[00:45:37]** Berarti tangannya kan.

**[00:45:39]** Dia udah ambil cuti 6 hari dong.

**[00:45:41]** Karena sisanya 6.

**[00:45:43]** Nah itu dia berarti di tahun.

**[00:45:45]** 2026 nya dia cuman bisa.

**[00:45:47]** Klaim 6 dari tahun sebelumnya.

**[00:45:49]** Tapi bukan tahun-tahun sebelumnya.

**[00:45:51]** Tapi cuman tahun sebelumnya.

**[00:45:53]** Jadi dia rollovernya.

**[00:45:55]** Kalau misalnya dia udah ambil 6.

**[00:45:57]** Di 2024 berarti.

**[00:45:59]** Kuota cuti dia di 2025.

**[00:46:01]** Itu kan dia dapet.

**[00:46:02]** Besi selainnya 12 ya kan.

**[00:46:04]** Ditambah 6.

**[00:46:07]** Nah itu kalau kuota rollover-nya.

**[00:46:09]** Maksimalnya itu cuman bisa 18 hari.

**[00:46:11]** Di klaim jadi meskipun dia di besi selainnya.

**[00:46:13]** Itu dia nyesaknya 8 hari.

**[00:46:15]** Di 2025-nya itu.

**[00:46:17]** Karena yang di rollovernya cuman 6.

**[00:46:19]** Berarti yang ke bawah yang 3.

**[00:46:21]** Kalau dia sisanya 8 berarti 2-nya.

**[00:46:23]** Nggak ke bawah gitu kan.

**[00:46:24]** Karena yang bisa di klaim cuman 2.

**[00:46:26]** Jadi perhitungan di tahun 2025.

**[00:46:28]** Pasti 12 tambah.

**[00:46:29]** Sisak kuota rollover-nya di tahun kemarin.

**[00:46:31]** Jadi kalau misalnya.

**[00:46:33]** Tahun kemarinya itu dia sisanya 4.

**[00:46:35]** Itu berarti di rollovernya di 2025.

**[00:46:37]** Itu jadi berapa.

**[00:46:41]** Jadi berapa.

**[00:46:42]** Jadi pada kuota tahun 2024.

**[00:46:46]** Dia sisak cutinya itu 4.

**[00:46:48]** Di 2025.

**[00:46:50]** Total cutinya berapa berarti.

**[00:46:56]** 16.

**[00:46:58]** Karena yang ke bawah 4.

**[00:47:00]** Kalau misalnya 2024.

**[00:47:02]** Dia sisak cuti.

**[00:47:04]** 12 misalnya dia nggak ngambil sama sekali.

**[00:47:07]** Di 2025 berarti kuota cutinya berapa.

**[00:47:09]** 18.

**[00:47:13]** Berapa?

**[00:47:15]** 18.

**[00:47:16]** Nah 18.

**[00:47:18]** Nah dia berarti kuota cutinya kan 18.

**[00:47:20]** Kalau dia nggak ngambil cuti lagi.

**[00:47:22]** Di 2025 misalnya.

**[00:47:24]** Tapi di 2024 kan dia sudah ngambil.

**[00:47:26]** Cuti 6.

**[00:47:28]** Jadi 2024 itu sisak kuota hanya 6.

**[00:47:30]** Di 2025 itu karena 18.

**[00:47:32]** Dia nggak ngambil cuti sama sekali.

**[00:47:34]** Jadi kuota cutinya di 2025.

**[00:47:36]** Tetap 18.

**[00:47:37]** Di 2026 berarti kuota cutinya berapa.

**[00:47:39]** Jadi.

**[00:47:44]** 26.

**[00:47:46]** 24.

**[00:47:47]** 24.

**[00:47:48–00:48:08]** [Percakapan tumpang tindih; angka yang disebut tidak dapat dipastikan.]

**[00:48:08]** 10.

**[00:48:09]** Berarti tetap maksimalnya di 24 ya Pak.

**[00:48:12]** Enggak.

**[00:48:13]** Di 2026-nya berarti dia 18.

**[00:48:16]** Karena dia udah ngambil cuti di nmin2 kan.

**[00:48:20]** 2024 dia sisak cutinya 6.

**[00:48:22]** Di 2025 dia.

**[00:48:24]** Sisanya kan masih 12.

**[00:48:26]** Ditambah 6 hari yang di-rollover, sehingga totalnya 18.

**[00:48:29]** Nah di 2026 dia kan memang dapatnya 12.

**[00:48:32]** Ya kan.

**[00:48:33]** Tapi kan karena dia sudah pernah ambil cuti.

**[00:48:36]** Di nmin2.

**[00:48:37]** Karena sisanya 6.

**[00:48:38]** Jadi meskipun.

**[00:48:39]** Sisanya di tahun sebelumnya 18.

**[00:48:41]** Di tahun 2026.

**[00:48:42]** Kuota cutinya tetap 18 lagi.

**[00:48:44]** Dia baru 2024.

**[00:48:46]** Kalau memang di 2024.

**[00:48:47]** Dia kok sisak kuota cutinya 12.

**[00:48:49]** Di 2025 dia.

**[00:48:50]** Sisak kuota cutinya 12 juga.

**[00:48:52]** Dia nggak ngambil kan.

**[00:48:53]** Baru di 2026.

**[00:48:54]** Dia dapat 24.

**[00:48:59]** Berarti dia 24 itu.

**[00:49:01]** Ketika yang n2 dengan n1.

**[00:49:03]** Dia nggak ngambil sama sekali ya.

**[00:49:04]** Iya betul.

**[00:49:05]** Kalau misalnya.

**[00:49:06]** Dia cuma ngambil 1 hari aja.

**[00:49:07]** Itu tetap rollover.

**[00:49:09]** Di n2 n1.

**[00:49:11]** Itu tetap di 2026 sekarang.

**[00:49:13]** 18 gitu.

**[00:49:15]** Oh 18 tetap.

**[00:49:22]** Nah itu baiknya ditampilin aja.

**[00:49:24]** Di pendataan saldo awal ini.

**[00:49:26]** Jadi.

**[00:49:27]** Pas dia nginput.

**[00:49:29]** Misalnya biasanya kuota di 2024.

**[00:49:31]** Sisak 4.

**[00:49:32]** Berarti di 2025 itu.

**[00:49:34]** Dia dapatnya.

**[00:49:37]** 16 kan.

**[00:49:40]** 16.

**[00:49:41]** Usahakan yang di kuota tahun berjalan itu.

**[00:49:43]** Nggak perlu di input lagi.

**[00:49:45]** Makanya ini kalau misalnya.

**[00:49:47]** Casnya ini kita pake.

**[00:49:49]** Dari 2024 kan memang agak.

**[00:49:51]** Bingung tapi senggaknya.

**[00:49:52]** Tetap kalian.

**[00:49:54]** Kayak dijadikan cas aja gitu.

**[00:49:56]** Karena perhitungan cuti ini.

**[00:49:58]** Agak bahaya kalau misalnya dia.

**[00:50:00]** Misleading gitu kan.

**[00:50:01]** Karena kuota cutinya itu.

**[00:50:02]** Kalau sampai 20 itu.

**[00:50:03]** Itu udah janggal sebenarnya.

**[00:50:05]** Karena maksimalnya itu 18.

**[00:50:06]** Berapapun sisak kuota cuti.

**[00:50:08]** Di tahun sebelumnya.

**[00:50:09]** Tetap yang di kelem itu cuma 6 gitu.

**[00:50:37]** Jadi mau dia.

**[00:50:40]** Mau dia di 2024.

**[00:50:42]** Dia kuota cutinya mungkin.

**[00:50:44]** Masih 12 di 2025.

**[00:50:46]** Dia ambil kuota cuti cuma 1 hari saja.

**[00:50:48]** Beratikan sisanya berapa.

**[00:50:50]** 17 kan.

**[00:50:52]** Karena dia udah ambil 1 hari.

**[00:50:54]** 11 ditambah 6 dari tahun sebelumnya kan.

**[00:50:56]** Nah di 2026.

**[00:50:58]** Kalau dia tidak pake ya.

**[00:51:00]** Dia ditariknya juga di rollover-nya.

**[00:51:01]** Cuma tetap 6 juga.

**[00:51:02]** Berarti 18 gitu.

**[00:51:03]** Makanya agak sayang-sayang.

**[00:51:05]** Kalau nggak dipake kalau cutunya.

**[00:51:07]** Jadi kalian.

**[00:51:13]** Tanpa satu kolom aja dulu buat simulasi.

**[00:51:15]** Simulasi perhitungan.

**[00:51:17]** Misalnya kalau di impusnya.

**[00:51:18]** 2024.

**[00:51:21]** Berapa ya.

**[00:51:22]** Perhitungannya jangan pake sistem.

**[00:51:24]** Saldo cuti dulu.

**[00:51:25]** Tapi kuota yang diambil.

**[00:51:27]** Jadi tanpa satu kolom dulu buat kalian.

**[00:51:29]** Hitung-hitung gitu kan.

**[00:51:30]** Buat pastikan perhitungan kuotanya bener.

**[00:51:32]** Karena tiap tahun itu.

**[00:51:34]** Pegawai itu dapet 12 hari cuti.

**[00:51:36]** Nah buat mempermudah perhitungan kan.

**[00:51:37]** Kalau misalnya tiap tahun itu udah pasti 12.

**[00:51:40]** Beratikan kalian tinggal.

**[00:51:42]** Ngitung berapa hari.

**[00:51:44]** Cuti yang udah kepake gitu kan.

**[00:51:47]** Jadi 2024 kan cutinya 12.

**[00:51:50]** Nah tinggal di input misalnya dia udah pakenya.

**[00:51:52]** Berapa 6.

**[00:51:53]** Beratikan sisa 6.

**[00:51:54]** Nah di 2025 dia hitung kan.

**[00:51:56]** Pasti 12 tambah 6 jadi 18.

**[00:51:58]** Nah itu sisa kuota cutinya.

**[00:51:59]** Kalau misalnya dia yang inputnya.

**[00:52:01]** Terpake udah 5 misalnya.

**[00:52:03]** Beratikan sisa 13.

**[00:52:05]** Nah di tahun selacunya juga gitu.

**[00:52:06]** Pasti di rollover-nya cuma 6.

**[00:52:07]** 6 tanpa 12 lagi gitu.

**[00:52:10]** Soalnya kalau kalian.

**[00:52:12]** Coba ngitungnya pake saldo awal.

**[00:52:14]** Kan agak bingung buat dibikin skenario nya kan.

**[00:52:16]** Nah ini coba dibalik dulu.

**[00:52:18]** Skenario nya itu setiap tahun itu.

**[00:52:20]** Udah pasti dapet 12 gitu.

**[00:52:22]** Jadi kalau misalnya N1N2.

**[00:52:24]** Di 2026 kalau dia gak ngambil.

**[00:52:26]** Di N1N2 beratikan kuota tahun itu.

**[00:52:28]** Kan 12 ya kan.

**[00:52:30]** Nah kuota tiap tahun itu di 2024 kan.

**[00:52:32]** Dia gak ngambil berarti 6 ya kan.

**[00:52:34]** Di 2025 dia dapet 6 juga.

**[00:52:36]** Beratikan ditotakan 12.

**[00:52:38]** Tambah 6 tambah 6 kan merapat 24 kan.

**[00:52:41]** Nah gitu.

**[00:52:43]** Jadi berpikirnya di balik aja.

**[00:52:47]** Jadi pake sistem.

**[00:52:49]** Berapa yang udah di klaim.

**[00:52:51]** Nah itu bakal ketemu kok saldo.

**[00:52:53]** Saldo cutinya berapa.

**[00:52:56]** Jadi kalau untuk perhitungan saldo cuti yang.

**[00:52:58]** Di input kan.

**[00:52:59]** Dia udah cuti berapa hari.

**[00:53:01]** Sebelumnya gitu kalau misalnya.

**[00:53:03]** Tahun ini 0 yang berarti.

**[00:53:05]** Biar nanti sisa kuota cutinya itu di hitung.

**[00:53:07]** Bisistem.

**[00:53:08]** Paham.

**[00:53:13]** Apa deh yang masih membingungkan.

**[00:53:15]** Terus kalau yang.

**[00:53:25]** Koreksis saldo itu apa koreksis saldo.

**[00:53:27]** Nah itu kalau misalnya.

**[00:53:30]** Ada yang.

**[00:53:33]** Di N2.

**[00:53:35]** Kayak salah input gitu.

**[00:53:37]** Jadi ini ada yang di koreksis.

**[00:53:39]** Nah ini sebenarnya.

**[00:53:41]** Dia gak perlu.

**[00:53:43]** Kalau misalnya dia hitungannya udah berapa hari.

**[00:53:45]** Yang di klaim cutinya kan.

**[00:53:47]** Jadi gak perlu di koreksis karena perhitungannya kan.

**[00:53:49]** Pasti bisistem kan.

**[00:53:50]** Kalau pun dia ada selisi tinggal di.

**[00:53:52]** Di edit manual lagi misalnya dari 6.

**[00:53:55]** Sebenarnya dia udah klaim 5 tapi ke inputnya 6.

**[00:53:57]** Tinggal diganti otomatiskan saldo cutinya bakal.

**[00:53:59]** Menyesuaikan sendirinya gitu kan.

**[00:54:19]** Berarti inputannya nanti.

**[00:54:21]** Cuma 1.

**[00:54:23]** Dia otomatis di hitung.

**[00:54:25]** Iya di hitung.

**[00:54:27]** Jadi di rumusnya itu tinggal di patok.

**[00:54:29]** Lewat.

**[00:54:31]** Lewat back end aja gitu.

**[00:54:33]** Jadi kalau misalnya di hitungannya.

**[00:54:35]** N min 2 nya kan 2024 dia udah.

**[00:54:37]** Berapa yang sudah diklaim nanti akan dihitung otomatis.

**[00:54:39]** Berkurang tuh.

**[00:54:41]** Nanti yang dari n min 2 itu bakal.

**[00:54:43]** Di akumulasi lagi ke 2025.

**[00:54:45]** Estimasi kuota cutinya akan terlihat.

**[00:54:47]** Berarti nanti.

**[00:54:49]** Tinggal diinput lagi kuota cuti yang terpakai.

**[00:54:51]** Kuota cuti yang kepake di 2025 berapa gitu kan.

**[00:54:53]** Itu kan pasti ke hitung otomatis semua kan.

**[00:54:55]** Jadi berjenjang jadinya.

**[00:54:58]** Kalau pun ada yang gak sesuai itu kan.

**[00:55:00]** Berarti tinggal.

**[00:55:02]** Kalau ada yang gak sesuai itu berarti ada.

**[00:55:04]** Klaim cuti yang.

**[00:55:06]** Masih kurang atau lebih gitu.

**[00:55:09]** Iya kan.

**[00:55:12]** Kalau pakai sistem sisa kuota cuti.

**[00:55:14]** Itu kan berarti inputan manual.

**[00:55:16]** Nah itu gimana kita mau validasi.

**[00:55:18]** Berarti kan hujungnya tetap kita hitung sendiri.

**[00:55:20]** Tapi kalau misalnya dia inputannya per.

**[00:55:22]** Berapa kuota cuti yang udah di klaim.

**[00:55:24]** Kalau misalnya yang tahun berjalan kan.

**[00:55:26]** 2026 itu kan gak apa-apa.

**[00:55:28]** Bisistem aja gitu kan jadi kalau cuti.

**[00:55:30]** Cuti yang udah di klaim di 2026.

**[00:55:32]** Kita bisa input manual nanti dia ngitung.

**[00:55:34]** Cuti yang udah terpakai itu berapa dari sana gitu.

**[00:55:36]** Tapi kalau 2025-2024.

**[00:55:38]** Karena lampau itu gak apa-apa.

**[00:55:40]** Dari admin kepegawainya input.

**[00:55:42]** 2024 itu dia udah.

**[00:55:44]** Cuti berapa hari, 2025 itu dia.

**[00:55:46]** Cuti berapa hari gitu.

**[00:55:48]** Nanti bakal kelihatan saldo cutinya berapa.

**[00:55:53]** Paham kan.

**[00:55:56]** Iya berarti yang di inputkan itu dia.

**[00:55:58]** Sudah cuti berapa hari.

**[00:56:00]** Iya tinggal.

**[00:56:02]** Dia udah klaim cutinya berapa hari yang lampau ya.

**[00:56:04]** Yang lampau kalau yang 2026 kan.

**[00:56:06]** Dia gak perlu di hitung karena kan udah tahun.

**[00:56:08]** Berjalan itu nanti dia di tahun.

## Input cuti manual dan migrasi data berjalan

**[00:56:10]** Berjalan itu kan dia ngitungnya.

**[00:56:12]** Berdasarkan.

**[00:56:14]** Usulan cuti, nah dia ajuan cuti itu kan.

**[00:56:16]** Bisa input manual juga kan.

**[00:56:18]** Tapi di alur.

**[00:56:20]** Ajuan cuti itu.

**[00:56:22]** Ada form ini gak yang input manual.

**[00:56:24]** Kalau tadi kan saya baru liat.

**[00:56:26]** Yang ajuannya itu butuh.

**[00:56:28]** Validasi kan.

**[00:56:30]** Gimana kalau.

**[00:56:32]** Casenya itu cutinya itu.

**[00:56:34]** Udah pernah di klaim.

**[00:56:36]** Tapi masih manual dan akhirnya mau di inputkan ke aplikasi.

**[00:56:38]** Gitu kan, itu udah ada forumnya belum.

**[00:56:40]** Yang forumnya itu soal.

**[00:56:48]** Ada yang ada.

**[00:56:52]** Sorry bapak bisa diulang yang itu.

**[00:56:55]** Yang mana.

**[00:56:57]** Yang di forum cuti.

**[00:56:59]** Nah forum cuti sekarang itu kan.

**[00:57:01]** Masih baik usulan kan.

**[00:57:03]** Jadi pegawai usul.

**[00:57:05]** Terus di validasi, di setuju.

**[00:57:07]** Nah casenya itu gimana.

**[00:57:09]** Kalau misalnya pegawainya ini.

**[00:57:11]** Udah pernah cuti di tahun berjalan ini.

**[00:57:13]** Tapi dia masih ikut mekanisme manual.

**[00:57:15]** Ini kan kemungkinan di implementasinya.

**[00:57:17]** Kalau bukan agustus september gitu kan.

**[00:57:19]** Dari januari sampai agustus kan.

**[00:57:21]** Pasti mereka ada usulan cuti di tahun berjalan.

**[00:57:23]** Tapi mekanisme nya masih manual kan.

**[00:57:25]** Nah itu kan kalau misalnya mau.

**[00:57:27]** Ikut prosedur yang sekarang pakai form yang sekarang kan.

**[00:57:29]** Itu berarti harus di validasi-validasi dulu.

**[00:57:31]** Padahal kan mereka udah.

**[00:57:33]** Ke klaim cutinya ya kan.

**[00:57:35]** Nah berarti kan harus ada forum ini.

**[00:57:37]** Forum penginputan cuti manual.

**[00:57:39]** Jadinya.

**[00:57:41]** Dokumen pendukungnya itu bakal wajib di input.

**[00:57:43]** Nah dia itu cutinya berapa hari.

**[00:57:45]** Dan itu langsung otomatis gitu gak perlu validasi lagi.

**[00:57:47]** Langsung ke input cutinya gitu.

**[00:57:49]** Cuma admin kepegawainya bisa input.

**[00:57:51]** Itu kan biar bisa kahitung.

**[00:57:53]** Di tahun ini dia udah berapa cuti.

**[00:57:55]** Nanti dia bakal di akumulasi dengan usulan cuti.

**[00:57:57]** Dari sistem yang udah berjalan.

**[00:57:59]** Ngerti kan?

**[00:58:01]** Ya untuk yang itu belum kami tambahkan sih.

**[00:58:03]** Bak.

**[00:58:05]** Untuk me input tahun sekarang.

**[00:58:07]** Iya.

**[00:58:09]** Soalnya dia.

**[00:58:11]** Bakal bergenjang karena kan.

**[00:58:13]** Kuota cutinya ini kan mau dibaliknya paradigman.

**[00:58:15]** Iya bukan lagi inputan berapa sisa.

**[00:58:17]** Kuota tapi.

**[00:58:19]** Berapa yang udah di klaim ya kan.

**[00:58:21]** Di 2026 kan kita gak bisa.

**[00:58:23]** Ngotak-kantik lagi gitu tahun berjalannya.

**[00:58:25]** Ya kan semenjak sistemnya di implementasi.

**[00:58:27]** Yang kita bisa gitu kan cuma yang.

**[00:58:29]** 2 tahun sebelumnya ya kan.

**[00:58:31]** Nah.

**[00:58:33]** Kalau misalnya dibaliknya.

**[00:58:35]** Itu itu gimana kita bisa ngitung.

**[00:58:37]** Berapa hari yang udah ke klaim.

**[00:58:39]** Dari periode januari sampai Agustus.

**[00:58:41]** Kalau tidak ada form manual iya kan.

**[00:58:43]** Jadi bakal bergenjang itu.

**[00:58:45]** Jadi kalau di hitungnya cuma berdasarkan.

**[00:58:47]** Dari usulan cuti sekarang.

**[00:58:49]** Berarti ibaratnya.

**[00:58:51]** Preset dari nol lagi dong.

**[00:58:54]** Cuma usulan yang masuk di sistem.

**[00:58:56]** Yang bisa yang kehitung.

**[00:58:58]** Klaim cutinya iya kan.

**[00:59:00]** Nah makanya untuk mengatisi pasti itu.

**[00:59:02]** Ada form usus penginputan.

**[00:59:04]** Cuti manual gitu.

**[00:59:06]** Dia gak apa-apa dia pake flow tapi flow nya itu langsung.

**[00:59:08]** Otomatis aja gitu dia langsung disetujui semua.

**[00:59:10]** Kalau dari admin kepegawaian yang input.

**[00:59:12]** Jadi bukan sistem usulan tapi sistem.

**[00:59:15]** Penginputan.

**[00:59:17]** Penginputan yang lampau gitu.

**[00:59:20]** Berarti itu hanya proses untuk tahun.

**[00:59:22]** Saat ini?

**[00:59:24]** Enggak jadi.

**[00:59:26]** Untuk form penginputan.

**[00:59:28]** Cuti manual itu gak apa-apa dibuka aja.

**[00:59:30]** Tapi yang disini itu cuma dari admin kepegawaian.

**[00:59:32]** Toh itu.

**[00:59:34]** Dari kepegawaian.

**[00:59:36]** Karena itu kan mengatisi pasti barangkali kan dari sistemnya.

**[00:59:38]** Mungkin ada masalah dari server nya.

**[00:59:40]** Akhirnya kan si pengnya gak bisa jalan gitu kan.

**[00:59:42]** Tapi ini mati pegawai-pegawai ini.

**[00:59:44]** Butuh cuti gitu kan akhirnya mereka.

**[00:59:46]** Muslinya lewat manual nah.

**[00:59:48]** Kalau saat sistemnya jalan kan dari.

**[00:59:50]** Admin kepegawaian kan tinggal input lagi gitu kan.

**[00:59:52]** Ya.

**[00:59:56]** Jadi tuh.

**[00:59:58]** Kes-kes yang bisa saja terjadi.

**[01:00:00]** Makanya tetap yang form manual itu.

**[01:00:02]** Tetap ada gitu.

**[01:00:04]** Ternyata.

**[01:00:06]** Nanti ke depan-ke depannya.

**[01:00:08]** Kalau misalnya untuk saldo awal kayak gini.

**[01:00:10]** Itu kan kalau tahun mau.

**[01:00:12]** Tahunnya bakal berganti gitu kan.

**[01:00:14]** Itu gak apa-apa tetap.

**[01:00:16]** Tiap pegawainya masih bisa diubah.

**[01:00:18]** Saldo cutinya tapi cuman wewinannya.

**[01:00:20]** Dari kepegawaian toh gitu.

**[01:00:22]** Barangkali ada perhitungannya keliru atau gimana gitu.

**[01:00:24]** Kalau pun.

**[01:00:26]** Meskipun fiturnya itu gak bakal kepake.

**[01:00:28]** Tapi tetap disediain aja gitu.

**[01:00:30]** Buat pengeditan kuota cuti manual.

**[01:00:32]** Misalnya claim cutinya itu.

**[01:00:34]** Keliru.

**[01:00:36]** Dari kepegawainya paling kan tinggal.

**[01:00:38]** Di input aja lewat pengajuan form.

**[01:00:40]** Manual itu kan otomatis kan angkanya.

**[01:00:42]** Pasti berubah gitu ya kan.

**[01:00:44]** Misalnya ini 2024 atau 2025 gitu.

**[01:00:46]** Cuman kan.

**[01:00:48]** Kalau posisinya sekarang gak mungkin.

**[01:00:50]** Dong dari kepegawainya itu mau langsung input.

**[01:00:52]** Semua makanya di antisipasinya.

**[01:00:54]** Biar sistem cutinya bisa jalan.

**[01:00:56]** Paling di input manual dulu gitu kan.

**[01:00:58]** Angkanya gitu.

**[01:01:03]** Paham kan.

**[01:01:05]** Atau ada pertanyaan.

**[01:01:08]** Jadi gitu memang cutinya.

**[01:01:10]** Agak tricky.

**[01:01:12]** Jadinya harus disamakan dulu.

**[01:01:14]** Persepsinya.

**[01:01:16]** Tambah form inputan manual.

**[01:01:21]** Form inputan manual cuti.

**[01:01:23]** Jadi bukan pengajuan cuti tapi input cuti lah.

**[01:01:25]** Berarti yang akan.

**[01:01:30]** Di inputkan nanti cuti yang.

**[01:01:32]** Sudah terpakai.

**[01:01:34]** Oleh pegawai.

**[01:01:36]** Dan itu jangan.

**[01:01:38]** Cuman buat tahun 2026 toh.

**[01:01:40]** Gak menutup kemungkinan mungkin.

**[01:01:41]** 2024 juga tetap bakal di input.

**[01:01:43]** Karena buat ini kan kebutuhan administratif.

**[01:01:45]** Di input gitu.

**[01:01:46]** Jadi yang buat saldo.

**[01:01:50]** Saldo itu kan.

**[01:01:52]** Otomatis nol nih kalau misalnya.

**[01:01:54]** Pegawainya.

**[01:01:55]** Input cutinya.

**[01:01:57]** Acclaim cutinya di 2024 misalnya itu kan.

**[01:01:59]** Angkanya bakal berubah ya kan.

**[01:02:01]** Bakal berubah otomatis cuman kan.

**[01:02:03]** Tetap nanti ini kan disini sekarang ada.

**[01:02:05]** Fitur koreksi nah itu fitur koreksinya itu kan.

**[01:02:07]** Bisa langsung manual dari kepegawainya dari saldo cutinya.

**[01:02:09]** Misalnya yang baru ke input.

**[01:02:11]** Baru 1 gitu kan nah sistemnya kan.

**[01:02:13]** Otomatis ngetung sisa saldo cutinya itu kan.

**[01:02:16]** Sisa cuman 1 doa yang gitu kan yang.

**[01:02:18]** Kepake berarti sisa 11.

**[01:02:20]** Yang padahal dia masih ada 6 lagi.

**[01:02:22]** Nah itu kepegawainya masih bisa aja dia.

**[01:02:24]** Ngotang ngetik di bagian.

**[01:02:25]** Pendataran saldo nya ini di inputkan.

**[01:02:27]** Mungkin dia udah acclaim nya 6 tapi yang.

**[01:02:29]** Ke upload kan baru 1 gitu.

**[01:02:31]** Nanti kalau misalnya dari.

**[01:02:33]** Pengajuan cuti eh dari.

**[01:02:35]** Tambah cuti manual nya ini udah.

**[01:02:37]** Lengkap itu kan nanti tinggal dari.

**[01:02:39]** Kepegawainya koreksi aja angkanya yang.

**[01:02:41]** Di ini kan yang di saldo.

**[01:02:43]** Berapa yang kepake jadi misalnya ada.

**[01:02:45]** Tombol buat ngetung.

**[01:02:47]** Berapa berasarkan.

**[01:02:49]** Yang inputan cuti udah masuk gitu.

**[01:02:52]** Jadi dia gak perlu hitung manual lagi jadi.

**[01:02:54]** Ada otomatis nya jadi bisa nginput manual.

**[01:02:56]** Bisa juga langsung kayak menarik data gitu.

**[01:02:58]** Berapa sih cuti yang diklaim.

**[01:03:00]** Di tahun ini gitu jadi angkanya.

**[01:03:02]** Otomatis keisi gitu paham kan.

**[01:03:04]** Oke pak.

**[01:03:06]** Jadi koreksi saldo ini gak perlu ya sebenarnya.

**[01:03:11]** Itu nanti kita tambahkan.

**[01:03:16]** Jadi.

## Rangkuman koreksi

**[01:03:18]** Apa-apa hari ini kurang lebih.

**[01:03:20]** Yang jadi.

**[01:03:22]** Koreksi.

**[01:03:23]** Coba dirangkum dulu.

**[01:03:25]** Yang pertama di.

**[01:03:28]** Dicut ya.

**[01:03:32]** Dari yang penginputan manual.

**[01:03:35]** Kemudian.

**[01:03:36]** Penginputan saldo.

**[01:03:39]** Di.

**[01:03:43]** N2 itu.

**[01:03:45]** Jadi akan di hitung otomatis nanti.

**[01:03:48]** Dia berjenjang.

**[01:03:50]** Kemudian.

**[01:03:52]** Hari libur.

**[01:03:54]** Nanti ini hanya.

**[01:03:58]** Diatur dari.

**[01:04:00]** Selama hari libur.

**[01:04:02]** Buat kalender.

**[01:04:04]** Kemudian.

**[01:04:07]** Email.

**[01:04:11]** Email.

**[01:04:13]** Email yang akan.

**[01:04:16]** Kami.

**[01:04:18]** Untuk lakuin testing.

**[01:04:20]** Switch role.

**[01:04:22]** Apa lagi.

**[01:04:25]** Switch role.

**[01:04:28]** Boleh switch role.

**[01:04:30]** Yang super admin juga.

**[01:04:32]** Boleh switch role.

**[01:04:34]** Nanti ada.

**[01:04:36]** Testing.

**[01:04:38]** Kemudian.

**[01:04:40]** Ada yang.

**[01:04:42]** Grantly mau bertanya.

**[01:04:46]** Cuman walaupun masih yang bagian switch role.

**[01:04:48]** Itu.

**[01:04:49]** Dari super admin.

**[01:04:51]** Bisa.

**[01:04:53]** Switch role.

**[01:04:54]** Pegawai atau.

**[01:04:56]** Super admin bisa berperan sebagai.

**[01:04:58]** Role tersebut.

**[01:05:00]** Contoh dia bisa.

**[01:05:02]** Masuk ke pegawai A.

**[01:05:04]** Dan menjadi seperti A.

**[01:05:06]** Atau dia switch role.

**[01:05:09]** Dia bukan.

**[01:05:11]** Bukan impersonate.

**[01:05:13]** Sebagai pegawainya tapi impersonate.

**[01:05:15]** Sebagai rollnya gitu.

**[01:05:18]** Jadi cuma base role.

**[01:05:21]** Tapi itu nanti diikatnya itu jangan.

**[01:05:23]** Berasarkan role super adminnya.

**[01:05:25]** Tapi.

**[01:05:26]** Dibikin aja permission gitu.

**[01:05:28]** Ini kan udah sistem permission kan.

**[01:05:30]** Jadi kalau misalnya.

**[01:05:32]** Pegawainya itu yang penting dia ada.

**[01:05:34]** Permission untuk switch role.

**[01:05:36]** Dia juga bisa memakan switch role.

**[01:05:38]** Buat.

**[01:05:39]** Gonta ganti aksesnya jadi bukan.

**[01:05:41]** Bukan impersonate sebagai pegawainya tapi.

**[01:05:43]** Impersonate sebagai rollnya gitu.

**[01:05:45]** Rollnya sebagai apa.

**[01:05:47]** Bisa.

**[01:05:51]** Jadi kalau misalnya mau.

**[01:05:54]** Mau demo atau mau dibagin itu.

**[01:05:57]** Misalnya ada masalah di bagian fiturnya.

**[01:05:59]** Pegawai dan itu kan pasti.

**[01:06:01]** Ada berapa.

**[01:06:03]** Chair uday yang cuman muncul.

**[01:06:05]** Di tampilan pegawai kan.

**[01:06:07]** Nah daripada mau lock out lagi terus minta.

**[01:06:09]** Usian yang password terus di pegawainya kan itu agar.

**[01:06:11]** Ribet nah super admin itu bisa.

**[01:06:13]** Tinggal ganti-ganti aja rollnya rollnya sebagai.

**[01:06:15]** Pegawai.

**[01:06:16]** Karena kan super adminnya juga kan bagian dari.

**[01:06:18]** Pegawai sebenarnya kan.

**[01:06:20]** Jadi kalau misalnya dia mau switch role.

**[01:06:22]** Mau tes fitur di pimpinan ya dia tinggal.

**[01:06:24]** Switch role aja sebagai pimpinan gitu.

**[01:06:26]** Terus yang tadi apa.

## Penataan dokumen pegawai

**[01:06:38]** Dokumen SK yang belum ini ya yang.

**[01:06:40]** Penginputan belum.

**[01:06:43]** Belum ditambahin ya fiturnya apa.

**[01:06:45]** Udah ada tadi.

**[01:06:47]** Dokumen SK sudah pak.

**[01:06:49]** Udah ya.

**[01:06:50]** Ini aja.

**[01:06:52]** Gini.

**[01:06:53]** Dokumen SK ini kan ini.

**[01:06:55]** Hamburannya.

**[01:06:59]** Nah ini ditaruh di bagian.

**[01:07:01]** Data pegawai coba buka data pegawai.

**[01:07:03]** Nah buka.

**[01:07:05]** Buka profilnya.

**[01:07:12]** Nah.

**[01:07:16]** Dia.

**[01:07:18]** Bagusnya langsung ditambahin di sini aja.

**[01:07:20]** Jadi memang ada dua tempat.

**[01:07:22]** Ada tempat untuk dokumen SK yang.

**[01:07:24]** Memang langsung mau dicari ada juga yang.

**[01:07:26]** Perpegawainya.

**[01:07:28]** Jadi kan ini.

**[01:07:32]** Satu pintu semua kan kalau misalnya.

**[01:07:34]** Dia ini dia baru upload KTP.

**[01:07:36]** Terus dia mau upload KK kan.

**[01:07:38]** Kudupindah menuk lagi gitu kan itu.

**[01:07:40]** Eksperihnya kan kurang bagus nanti.

**[01:07:42]** Padahal di sini kan bisa aja dia.

**[01:07:44]** Tinggal langsung tambah aja.

**[01:07:46]** Muncul pop up modal.

**[01:07:48]** Pilih jenis dokumennya apa profil nya udah langsung.

**[01:07:50]** Nambah di sini gitu kan.

**[01:07:52]** Lebih gampang buat dikontrol kalau misalnya dia.

**[01:07:54]** Mau nama-nama dokumen selain yang SK-SK ini.

**[01:07:56]** Cuman itu.

**[01:08:02]** Baiknya kalau ditampilan dokumen SK.

**[01:08:04]** Per pegawai ini di.

**[01:08:06]** Dibuat tabel terpisah yang.

**[01:08:08]** Dokumen lainnya dari sepegawa.

**[01:08:10]** Atau dokumen tambahan dengan yang SK-SK yang.

**[01:08:12]** Wajib di input nih kaya kenaikan pangkat.

**[01:08:14]** Jabatan pengelola itu kan.

**[01:08:16]** Memang bagian dari diwired mereka kan.

**[01:08:18]** Baiknya itu dipisah tabelnya.

**[01:08:20]** Jadi ada tabel khusus yang dokumen.

**[01:08:22]** Mandatori dokumen wajib di atas.

**[01:08:24]** Terus dokumen lainnya dibawah jadi biar lebih.

**[01:08:26]** Gampang buat nyari gitu.

**[01:08:28]** Oh iya.

**[01:08:30]** Kati yang SK ini bisa.

**[01:08:32]** Sendiri yang.

**[01:08:34]** Jadi gak nyampur nih kayak KTP sama SK-SK.

**[01:08:36]** Itu kan dokumen desmi lah kalau KTP itu kan.

**[01:08:38]** Lebih kena tadi atau dokumen lainnya gitu kan.

**[01:08:40]** Itu ditaruh aja tabelnya dibawah.

**[01:08:42]** Nah ini kan kaya.

**[01:08:44]** Kepangkatan kan udah ada nih tambari wajat.

**[01:08:46]** Nah di dokumen SK nya itu tinggal dibikin.

**[01:08:48]** Serupa juga tinggal ada pop up modelnya.

**[01:08:50]** Ini.

**[01:08:52]** Bisa.

**[01:08:57]** Bisa.

**[01:09:08]** Itu kan.

**[01:09:10]** Yang dokumen lainnya itu.

**[01:09:12]** Dibuat terpisah.

**[01:09:14]** Oh iya.

**[01:09:17]** Nah gak pas yang bagian dokumen SK.

**[01:09:19]** Itu.

**[01:09:21]** Bisa langsung.

**[01:09:23]** Di kawai tentu.

**[01:09:25]** Tapi.

**[01:09:27]** Ini dokumen lain.

**[01:09:30]** Tapi itu baru SK.

**[01:09:32]** Jadi untuk.

**[01:09:34]** Dokumen lainnya seperti KTP.

**[01:09:36]** Atau dan lain-lain.

**[01:09:38]** Nah itu memang ditambahkan manual itu.

**[01:09:40]** Masih di alaman.

**[01:09:42]** Dokumen itu nak.

**[01:09:44]** Tadi kan memang kalau di dokumen SK itu ditampilannya.

**[01:09:46]** Itu kan ada tab-tap nya lagi dibawah kan.

**[01:09:48]** Saya lihat tadi.

**[01:09:50]** Itu kan mereket tambahkannya disitu.

**[01:09:52]** Nah memang itu yang saya tanyakan tadi kan.

**[01:09:54]** Untuk dokumen lainnya kan gak ada.

**[01:09:56]** Ininya gak ada penambahannya gitu cuman.

**[01:09:58]** Ibaratnya di halaman.

**[01:10:00]** Profilnya si pegawai yang tadi bukan.

**[01:10:02]** Nyantambilan ini itu.

**[01:10:04]** Cuman diunggah.

**[01:10:06]** Itu dokumen yang udah ada tab-tap nya.

**[01:10:08]** Yang dokumen lainnya kan gak ada tab-nya disitu kan.

**[01:10:10]** Jadi biar sekalian aja disitu.

**[01:10:15]** Dokumen untuk menu.

**[01:10:17]** Dan SK gak apa-apa.

**[01:10:18]** Tetap disitu aja itu buat.

**[01:10:20]** Akses super admin.

**[01:10:21]** Atau ke pegawainya kan buat.

**[01:10:23]** Mungkin barangkali dia langsung mau nyari gitu kan.

**[01:10:25]** Oke terus yang.

## Template WhatsApp dan target revisi

**[01:10:32]** WA jangan lupa ya.

**[01:10:34]** Yang tempat lihat pesan WA.

**[01:10:36]** Dibikin aja variabelnya butuh variabel apa.

**[01:10:38]** Datanya apa.

**[01:10:39]** Jadi biar sekalian diusulin gitu.

**[01:10:41]** Kalau model tampilan pesannya seperti apa.

**[01:10:46]** Misalnya dia.

**[01:10:48]** Mau naik pangkat pesannya itu seperti apa.

**[01:10:50]** Satyalancana itu pesannya seperti apa.

**[01:10:52]** Butuh apa yang ditampilkan.

**[01:10:54]** Kayak nama atau apa-apa.

**[01:10:55]** Karena variabel itu yang mau.

**[01:10:56]** Dipasing dari aplikasinya kan.

**[01:10:58]** Oke ada lagi.

**[01:11:05]** Waktu saat ini.

**[01:11:09]** Untuk yang.

**[01:11:13]** Sekarang.

**[01:11:15]** Yang ini dulu.

**[01:11:18]** Oke.

**[01:11:20]** Targetnya kapan tuh.

**[01:11:23]** Perbaikannya.

**[01:11:25]** Lagi ini deh.

**[01:11:27]** Kalau akhir bulan ini bisa.

**[01:11:29]** Bebas tergantung.

**[01:11:31]** Tergantung dari kalian soalnya kan.

**[01:11:33]** Kalian juga kan mau dikejar ini juga kan.

**[01:11:35]** Masih ada satu lagi nih.

**[01:11:37]** Yang sakit.

**[01:11:39]** Jadi kalian menyesuaikan aja kalau misalnya.

**[01:11:41]** Yang.

**[01:11:43]** Revisi hari ini udah clear.

**[01:11:45]** Dengan mungkin ada beberapa tambahan.

**[01:11:47]** Langsung kontak aja minta buat zoom.

**[01:11:49]** Gak harus dihari jumat.

**[01:11:51]** Hari-hari biasa juga gak apa-apa gitu biar nanti.

**[01:11:53]** Segera langsung dicek gitu kan.

**[01:11:56]** Oke siapa oke siapa.

**[01:11:58]** Ini estimasinya targetnya.

**[01:12:00]** Apaan nih maksudnya kelar-kelar.

**[01:12:02]** Tuntasnya.

**[01:12:05]** Untuk yang.

**[01:12:07]** Awalnya.

**[01:12:09]** Kecana di tanggal 20 ini.

**[01:12:11]** Tuman.

**[01:12:13]** Kalau di saat ini mungkin akan selesai.

**[01:12:15]** Di akhir bulan ini.

**[01:12:17]** Akhir 2 minggu lagi berarti.

**[01:12:19]** Iya secepatnya.

**[01:12:21]** Jadi kalau misalnya.

**[01:12:23]** Ada.

**[01:12:25]** Tanggapan lain atau mungkin.

**[01:12:27]** Yang masukannya udah kelar gak apa-apa.

**[01:12:29]** Kita ases main aja mau diajak sumpah.

**[01:12:31]** Cuma sejam 2 jam daripada.

**[01:12:33]** Kalian langsung kerjain semua.

**[01:12:35]** Terus ternyata malah.

**[01:12:37]** Clearo gitu kan ujungnya kan.

**[01:12:39]** Balik lagi gitu kan.

**[01:12:42]** Oke.

**[01:12:44]** Soalnya yang.

**[01:12:46]** Yang.

**[01:12:48]** Next projectnya juga ini.

**[01:12:50]** Kayanya bisa lebih sederhana.

**[01:12:52]** Cuman nanti nanti.

**[01:12:54]** Udah kelar simpeklah.

**[01:12:56]** Kita bahas.

**[01:12:58]** Ini bisa kelar dulu karena.

**[01:13:00]** Sekalipun aplikasinya ini kelar kan.

**[01:13:02]** Masih harus.

**[01:13:04]** Di demo ini ya kan.

**[01:13:06]** Kalau misalnya dari.

**[01:13:08]** Apa di demoin ke dari pihak.

**[01:13:10]** Kepegawainya juga udah oke.

**[01:13:12]** Nah itu kalian kan.

**[01:13:14]** Masih harus lanjut bikin ininya juga.

**[01:13:16]** Bikin panduan nya kan.

**[01:13:18]** Panduan yang terdalam.

**[01:13:20]** Bentuk PDF atau apa jadi.

**[01:13:22]** Guide lainnya.

**[01:13:25]** Buat masing-masing role itu.

**[01:13:27]** Fiturnya apa saja cara.

**[01:13:29]** Pakenya gimana itu pengaruhnya kemana.

**[01:13:31]** Itu kan memang harus ada guide nya sebelum kita.

**[01:13:33]** Balik ke next project gitu.

## Dokumentasi, deployment, dan penutupan

**[01:13:35]** Oh iya.

**[01:13:37]** Sekalian juga ini kan.

**[01:13:39]** Di ini kalian.

**[01:13:41]** Kerjainya masih di repo development kan ya.

**[01:13:43]** Iya.

**[01:13:45]** Itu kalian.

**[01:13:47]** Sebagian besar kerjainya di.

**[01:13:49]** Di linuxnya apa di windowsnya.

**[01:13:51]** Di platform.

**[01:13:54]** Platform pengemalan kalian nih.

**[01:13:56]** Windows ya.

**[01:14:02]** Windows.

**[01:14:04]** Kamis semua windows ya.

**[01:14:06]** Windows ya.

**[01:14:08]** Kemarin saya udah.

**[01:14:10]** Cek kan yang bagian kontainernya.

**[01:14:12]** Kalian tuh.

**[01:14:14]** Nah itu sebenarnya kalau untuk kontainernya PHP itu kan.

**[01:14:16]** Sebenarnya udah ada image sendiri.

**[01:14:18]** Jadi paling nanti.

**[01:14:20]** Paling entar atau besok itu.

**[01:14:22]** Model kontainernya itu bakal.

**[01:14:24]** Bakal saya ubah.

**[01:14:26]** Nanti saya push di development.

**[01:14:28]** Nanti saya inputkan di group gitu.

**[01:14:30]** Jadi image nya berubah.

**[01:14:33]** Yang jelasinnya aja data-data.

**[01:14:35]** Kalian yang tadi itu kan data sidar semua kan.

**[01:14:37]** Gak ada yang kayak di input manual atau apa kan.

**[01:14:39]** Ya kan.

**[01:14:43]** Iya pak.

**[01:14:45]** Iya kan.

**[01:14:47]** Kalau bikin obah di aparat.

**[01:14:49]** Ini tenang.

**[01:14:52]** Kalau tadi kan ada obah.

**[01:14:54]** Karena model kontainernya.

**[01:14:57]** Mau saya ubah dikit itu.

**[01:14:59]** Jadi kemungkinan paling kalian sedih lagi gitu kan.

**[01:15:01]** Kalau pun kalian mau backup juga gak apa-apa.

**[01:15:04]** Backup terus restore lagi gak apa-apa.

**[01:15:06]** Soalnya buat ini.

**[01:15:08]** Karena udah mulai dipengujung kan.

**[01:15:10]** Jadinya saya juga perlu siapkan.

**[01:15:12]** Apa.

**[01:15:14]** DevOps nya gitu kan.

**[01:15:16]** Biar kalau pun kaliannya udah.

**[01:15:18]** Udah kelar.

**[01:15:20]** Saya tinggal deploy aja gitu.

**[01:15:22]** Udah gak perlu banyak kontainer.

**[01:15:24]** Soalnya tadi pas saya cek juga kan.

**[01:15:26]** Kayak misalnya Nginx nya.

**[01:15:28]** Ada konfigurasi nya sendiri terus.

**[01:15:30]** Deploy dock apa.

**[01:15:32]** Kontainerisasi nya juga sendiri.

**[01:15:34]** Nah itu kan.

**[01:15:36]** Di kontainer kalian itu.

**[01:15:38]** Untuk PHP nya itu.

**[01:15:40]** Baratnya kalian pakai image nya dari debian.

**[01:15:42]** Terus di install 1x1.

**[01:15:44]** Nah itu kan buat meminimalisir itu.

**[01:15:46]** Saya kan memang udah ada image sendiri.

**[01:15:48]** Itu sempat bikin image sendiri yang tinggal langsung di deploy.

**[01:15:50]** Jadi paling itu aja yang saya ganti gitu.

**[01:15:52]** Dengan paling.

**[01:15:54]** Nge-upgrade sedikit.

**[01:15:56]** Versi PostgreSQL nya gitu.

**[01:15:58]** Selebihnya sih tetep sama aja.

**[01:16:00]** Jadi biar kalian saya beritahukan dulu.

**[01:16:02]** Biar kalian gak kaget gitu.

**[01:16:04]** Tiba-tiba pas mungkin nge-push ada yang bener.

**[01:16:06]** Atau apa gitu cuma itu aja yang saya ubah sih.

**[01:16:08]** Oke.

**[01:16:11]** Oke boleh pak.

**[01:16:13]** Ada lagi, ada pertanyaan lagi.

**[01:16:15]** Atau mungkin dari.

**[01:16:17]** Dari [nama kurang jelas].

**[01:16:23]** Cukup kayaknya cukup.

**[01:16:26]** Aman ya.

**[01:16:29]** Dari kalian mungkin.

**[01:16:31]** Gak ada lagi.

**[01:16:33]** Akhir mungkin.

**[01:16:35]** Dokumentasi.

**[01:16:37]** Oke siap.

**[01:16:40–01:16:58]** [Percakapan penutup singkat tidak terdengar jelas.]

**[01:16:59]** Oke sudah pak.

**[01:17:01]** Oke, terima kasih, Dion.

**[01:17:03]** Teman-teman yang lain juga ditunggu.

**[01:17:05]** Update nya.

**[01:17:07]** Nanti mungkin yang setelah.

**[01:17:09]** Kita akan meeting ulang.

**[01:17:11]** Iya gak apa-apa misalnya.

**[01:17:13]** Barangkali kalian yang lebih cepat gak harus nunggu hari jumat lagi gitu.

**[01:17:15]** Di kabarnya.

**[01:17:17]** Kapan bisa zoom gitu.

**[01:17:19]** Saya bisa luangkan waktu kalau buat zoom.

**[01:17:21]** Yang penting kalian tidak sampai.

**[01:17:23]** Kejauhan salah arahnya gitu kan.

**[01:17:25]** Saya ingat lain waktu juga.

**[01:17:28]** Oke terima kasih ya teman-teman ya.

**[01:17:30]** Terima kasih pak.

**[01:17:32]** Saya Ijin Pamit, selamat bertugas.

**[01:17:34]** Kembali.
