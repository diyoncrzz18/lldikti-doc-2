# Notulen Meeting Evaluasi Pengembangan SIMPEG bersama LLDIKTI

## Informasi rapat

| Item | Keterangan |
|---|---|
| Sumber | `videoplayback.mp4` |
| Durasi | 01:17:35 |
| Tanggal rapat | Tidak disebutkan secara eksplisit dalam rekaman |
| Jenis rapat | Evaluasi rutin, demo progres, dan pembahasan koreksi pengembangan SIMPEG |
| Instansi/pihak | Perwakilan LLDIKTI dan tim magang Universitas Klabat |
| Presenter yang teridentifikasi | Dion Kobi |

> Catatan: beberapa nama dan suara tidak dapat diidentifikasi secara pasti. Butir keputusan di bawah mengikuti isi rekaman, sedangkan bagian yang bertentangan dengan dokumen kanonis ditempatkan sebagai pertanyaan terbuka dan belum boleh dijadikan dasar implementasi tanpa konfirmasi.

## Agenda

1. Pemeriksaan progres pengembangan aplikasi.
2. Demo dashboard dan data pegawai.
3. Demo impor data pegawai dan validasinya.
4. Demo pengajuan serta persetujuan cuti.
5. Demo EWS, Data Master, hari libur, dan Kelola Akses User.
6. Pembahasan SSO, notifikasi WhatsApp Business, kuota cuti, dokumen pegawai, deployment, dan target penyelesaian.

## Ringkasan eksekutif

Tim menyampaikan progres aplikasi sekitar 90%. Sprint 6 disebut telah selesai, sedangkan Sprint 7 berfokus pada full testing dan perbaikan bug. Demo mencakup dashboard berbasis data nyata, penambahan dan impor pegawai, profil serta dokumen pegawai, ekspor, pengajuan cuti dengan beberapa role, EWS, Data Master, dan pengelolaan akses pengguna.

Pihak LLDIKTI memberi koreksi utama pada urutan persetujuan cuti, perhitungan kuota cuti tahunan, kebutuhan input cuti manual, tampilan hari libur, kemudahan pengujian lintas role, penataan dokumen pegawai, dan persiapan template pesan WhatsApp Business. Tim juga masih membutuhkan akun SSO yang memiliki email agar alur login dan mapping dapat diuji penuh.

Target awal disebut tanggal 20, tetapi tim memperkirakan penyelesaian dapat bergeser ke akhir bulan. Pihak LLDIKTI meminta tim tidak menunggu jadwal rutin hari Jumat apabila revisi sudah siap; rapat Zoom singkat dapat dijadwalkan lebih cepat agar pengerjaan tidak berjalan terlalu jauh ke arah yang keliru.

## Hasil demo dan pembahasan

### 1. Progres, dashboard, dan data pegawai

- Progres keseluruhan disampaikan sekitar 90%.
- Sprint 6 disebut sudah selesai; Sprint 7 difokuskan pada testing dan perbaikan bug.
- Dashboard disebut telah menggunakan data nyata, antara lain kenaikan pangkat, komposisi/status pegawai, status cuti, distribusi golongan, EWS aktif, tren pegawai, dan aktivitas terbaru.
- Pegawai dapat ditambahkan secara manual atau melalui impor Excel.
- Template impor mengikuti template terakhir yang diberikan pihak LLDIKTI.
- Validasi impor mendeteksi email yang sudah terdaftar dan NIP yang terduplikasi. Proses impor berjalan sebagai background job.
- Profil pegawai memuat data keluarga, kontak, berkas, kepangkatan, jabatan, KGB, hukuman disiplin, pendidikan, pengangkatan, dan dokumen SK.
- Data pegawai dapat diekspor menggunakan kolom default atau pilihan kolom khusus, dalam format PDF atau Excel.

### 2. Pengajuan dan persetujuan cuti

- Pegawai belum dapat mengubah profil sendiri pada tahap ini; perubahan profil dilakukan oleh Admin Kepegawaian atau Super Admin.
- Saldo cuti hanya dipotong untuk Cuti Tahunan. Cuti Sakit, Cuti Melahirkan, dan Cuti Karena Alasan Penting tidak memotong saldo tahunan.
- Perhitungan durasi cuti menggunakan hari kerja dan mengecualikan akhir pekan serta hari libur.
- Pengajuan cuti yang melintasi tahun kalender harus dipecah menjadi pengajuan terpisah.
- Lampiran pada contoh pengajuan disebut opsional.
- Rantai persetujuan dapat memuat verifikator dinamis, Kepala Bagian, dan PYBMC sebagai persetujuan akhir.
- Arah urutan yang diminta dalam rapat adalah verifikator terlebih dahulu, kemudian Kepala Bagian, lalu PYBMC. Verifikator diposisikan sebagai pemeriksa awal, sedangkan Kepala Bagian merupakan atasan pegawai.
- Saldo tahunan dipotong setelah seluruh tahapan persetujuan selesai dan pengajuan disetujui.

### 3. Kuota dan saldo cuti tahunan

- Setiap pegawai memperoleh jatah dasar 12 hari per tahun.
- Sisa tahun sebelumnya yang dapat dibawa ke tahun berikutnya dibatasi maksimal 6 hari.
- Dalam contoh rapat, kuota normal tahun berjalan menjadi maksimal 18 hari: 12 hari tahun berjalan ditambah maksimal 6 hari rollover.
- Kuota 24 hari hanya berlaku pada kondisi pegawai tidak mengambil cuti selama dua tahun berturut-turut. Bila pegawai mengambil cuti walaupun hanya satu hari pada periode tersebut, contoh pembahasan mengarah kembali ke maksimum 18 hari.
- Pihak LLDIKTI meminta pendekatan input diubah: Admin Kepegawaian memasukkan jumlah cuti yang sudah dipakai/diklaim pada tahun lampau, lalu sistem menghitung sisa serta rollover secara berjenjang.
- Perhitungan disarankan diuji terlebih dahulu dengan tabel/simulasi agar kasus 2024, 2025, dan 2026 dapat divalidasi sebelum dipakai sebagai saldo operasional.
- Diperlukan form input cuti manual untuk mencatat cuti yang sudah diproses di luar sistem, termasuk cuti pada tahun berjalan sebelum SIMPEG digunakan atau saat sistem tidak tersedia.
- Input cuti manual dilakukan oleh Admin Kepegawaian, dapat mewajibkan dokumen pendukung, dan tidak perlu melalui proses usulan serta persetujuan ulang karena cutinya sudah pernah disahkan di luar sistem.
- Sistem perlu dapat menghitung ulang saldo dari data cuti yang telah dimasukkan, sembari tetap menyediakan koreksi administratif yang terkontrol bila data belum lengkap.

### 4. EWS, Data Master, dan hari libur

- EWS saat demo masih berfokus pada notifikasi dalam aplikasi; notifikasi email disebut direncanakan pada bagian akhir pengembangan.
- Konfigurasi EWS mencakup kenaikan pangkat, KGB, BUP/pensiun, masa kontrak PPPK, dan Satyalancana, dengan periode peringatan yang dapat dikonfigurasi.
- Data Master yang didemonstrasikan mencakup golongan/pangkat, jenis jabatan, eselon, status pegawai, jenis cuti, agama, jenjang pendidikan, unit kerja, dan hari libur.
- Tampilan hari libur diminta tidak terduplikasi di Data Master dan menu terpisah. Arahan UI adalah menempatkannya pada satu halaman hari libur dengan kalender di bagian atas dan tabel di bawah.

### 5. SSO dan akses pengguna

- Tim belum dapat menguji integrasi SSO secara penuh karena akun uji yang diberikan belum memiliki email.
- Pihak LLDIKTI meminta tim mengirim daftar email dan daftar role akun uji agar atributnya dapat dilengkapi pada SSO.
- Nomor telepon disebut dapat tersedia sebagai custom attribute dan perlu diperiksa dari respons SSO sebelum dibuat mapping.
- Dibahas usulan fitur `switch role` agar pengguna yang memiliki permission khusus dapat menguji tampilan role lain tanpa login/logout berulang.
- Usulan tersebut adalah berpindah pada level role, bukan menyamar sebagai pegawai tertentu. Rekaman menyebut penggunaan temporary role dan temporary permission yang dapat dikembalikan ke role semula.

### 6. Notifikasi WhatsApp Business

- Integrasi WhatsApp Business membutuhkan template pesan yang lebih dahulu disetujui oleh Meta.
- Tim diminta menyusun dokumen template untuk setiap jenis notifikasi beserta variabel datanya, misalnya nama pegawai, jenis peringatan, kenaikan pangkat, atau Satyalancana.
- Pihak LLDIKTI akan mengajukan template, lalu mengembalikan template ID serta petunjuk pemasangannya agar dapat diuji dari aplikasi.

### 7. Dokumen pegawai

- Unggah dokumen diminta tersedia langsung dari profil pegawai agar pengguna tidak harus berpindah menu.
- Dokumen wajib/SK disarankan dipisahkan secara visual dari dokumen tambahan seperti KTP, KK, atau ijazah.
- Menu dokumen terpusat tetap dapat dipertahankan untuk akses Admin Kepegawaian atau Super Admin dan pencarian lintas pegawai.

### 8. Dokumentasi, target, dan deployment

- Setelah aplikasi diterima oleh pihak kepegawaian, tim masih harus membuat panduan penggunaan per role yang menjelaskan fitur, cara penggunaan, dan dampak setiap aksi.
- Target awal disebut tanggal 20, sedangkan estimasi yang disampaikan saat rapat adalah akhir bulan.
- Tim diminta segera meminta Zoom apabila suatu kelompok revisi telah selesai; tidak perlu menunggu pertemuan rutin berikutnya.
- Pihak LLDIKTI menyampaikan rencana memperbarui model container/deployment pada branch `development`, menggunakan image PHP yang telah disiapkan, menyederhanakan container, dan sedikit memperbarui versi PostgreSQL.
- Tim diingatkan menyiapkan backup/restore data apabila diperlukan sebelum perubahan container.

## Arah perbaikan yang terdengar jelas

| No. | Arah perbaikan | Pihak yang disebut/diindikasikan | Target yang disebut |
|---:|---|---|---|
| 1 | Ubah urutan approval menjadi verifikator → Kepala Bagian → PYBMC. | Tim pengembang | Secepatnya, sebelum evaluasi lanjutan |
| 2 | Tambahkan form input cuti manual oleh Admin Kepegawaian. | Tim pengembang | Bersama revisi modul cuti |
| 3 | Ubah dasar pendataan saldo awal menjadi jumlah cuti yang sudah dipakai/diklaim, lalu hitung sisa dan rollover oleh sistem. | Tim pengembang | Bersama revisi modul cuti |
| 4 | Buat simulasi kasus kuota 2024–2026 untuk memvalidasi rumus 12/18/24 hari. | Tim pengembang | Sebelum rumus dipakai sebagai saldo operasional |
| 5 | Satukan pengelolaan hari libur dalam tampilan kalender dan tabel. | Tim pengembang | Pada revisi UI berikutnya |
| 6 | Kirim daftar email dan role akun uji SSO. | Tim magang kepada pihak LLDIKTI | Tidak disebutkan |
| 7 | Lengkapi email/atribut akun uji SSO. | Pihak LLDIKTI | Setelah daftar diterima |
| 8 | Rancang `switch role` berbasis permission dan mekanisme kembali ke role semula. | Tim pengembang | Untuk demo, pengujian, dan dukungan |
| 9 | Susun template WhatsApp beserta variabel untuk setiap jenis notifikasi. | Tim pengembang | Sebelum integrasi WhatsApp diuji |
| 10 | Ajukan template ke Meta dan berikan template ID/petunjuk integrasi. | Pihak LLDIKTI | Setelah dokumen template diterima |
| 11 | Tambahkan unggah dokumen dari profil dan pisahkan dokumen wajib dari dokumen tambahan. | Tim pengembang | Pada revisi modul pegawai |
| 12 | Susun panduan penggunaan per role. | Tim magang | Sebelum handover/berpindah ke proyek berikutnya |
| 13 | Ubah image/container deployment dan informasikan perubahan pada tim. | Pihak LLDIKTI | Dalam waktu dekat menurut rekaman |
| 14 | Jadwalkan evaluasi Zoom segera setelah revisi siap. | Tim magang dan pihak LLDIKTI | Tidak harus menunggu hari Jumat |

## Open question dan kebutuhan keputusan stakeholder

Butir berikut terdengar dalam rapat, tetapi bertentangan dengan atau belum ditetapkan secara lengkap dalam dokumen kanonis. Jangan langsung diimplementasikan sebagai keputusan final tanpa pencatatan keputusan produk.

1. **Sumber role saat SSO:** rekaman membahas role default dari SSO, sedangkan aturan kanonis menyatakan Keycloak hanya mengautentikasi identitas dan role/permission SIMPEG harus berasal dari database internal. Perlu dipastikan apakah yang dimaksud hanya data bantu untuk mapping awal atau benar-benar sumber otorisasi.

2. **`Switch role` pada production:** rekaman mengusulkan temporary role/permission yang persisten setelah login ulang dan dapat dipakai pada production. Diperlukan keputusan keamanan mengenai siapa yang berhak, batas role tujuan, audit log, masa berlaku, session handling, larangan privilege escalation, dan cara fail-closed.

3. **WhatsApp Business dalam Fase 1:** dokumen kanonis menempatkan aktivasi production sebagai fitur future/configurable kecuali layanan dan credential disediakan secara eksplisit. Rekaman menunjukkan pihak LLDIKTI bersedia mengurus template dan template ID, tetapi perlu konfirmasi apakah ini menjadi perubahan scope resmi.

4. **Rumus kuota 12/18/24 hari:** rapat memberi contoh rinci, tetapi rumus perlu ditulis sebagai keputusan kanonis berikut tabel kasus, urutan konsumsi saldo, perilaku rollover, dan pengaruh cuti satu hari pada N-2/N-1. Hindari implementasi hanya dari interpretasi audio.

5. **Input cuti manual:** perlu kontrak formal mengenai status final, tanggal keputusan, approver historis, dokumen wajib, audit, notifikasi, koreksi, dan pengaruh ledger agar tidak menciptakan jalan pintas persetujuan untuk pengajuan baru.

6. **Target penyelesaian:** dokumen proyek menyebut target tanggal 20, sedangkan rekaman mengarah ke akhir bulan. Tanggal final perlu dikonfirmasi.

7. **Perubahan container dan PostgreSQL:** perlu sinkronisasi versi, prosedur backup/restore, konfigurasi environment, dan bukti uji PostgreSQL sebelum perubahan branch menjadi acuan tim.

## Penutup

Pihak LLDIKTI meminta tim memberikan pembaruan lebih cepat ketika revisi siap dan bersedia meluangkan waktu untuk evaluasi Zoom di luar jadwal rutin. Rapat ditutup dengan ucapan terima kasih dan permintaan agar tim tidak mengerjakan terlalu jauh tanpa validasi arah.



---

## Status Keputusan Setelah Konfirmasi Dokumentasi — 15 Agustus 2026

Pengguna mengonfirmasi bahwa dokumentasi harus mengikuti hasil meeting. Karena itu, butir pada bagian **Open question dan kebutuhan keputusan stakeholder** yang menyangkut urutan approval, model pendataan saldo, input cuti manual, switch role, mapping atribut SSO, tampilan Hari Libur, dokumen pegawai, template WhatsApp, target penyelesaian, dan perubahan deployment **tidak lagi berstatus usulan terbuka**. Ketetapan penggantinya dicatat pada [Keputusan Evaluasi Meeting LLDIKTI](Keputusan-Evaluasi-Meeting-LLDIKTI-15-Agustus-2026.md).

Batas faktual tetap berlaku: nama claim custom attribute Keycloak, template ID WhatsApp, credential/provider layanan, serta versi image/container dan PostgreSQL belum disebutkan dalam rekaman. Nilai tersebut harus diisi dari artefak yang diberikan LLDIKTI, tanpa menebaknya.
