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

## K-MTG-02 — Atribut Keycloak dan role default Pegawai

1. Mapping SSO memakai email Keycloak sebagai atribut utama. LLDIKTI melengkapi email akun uji dan menyediakan daftar role akun uji.
2. Saat email telah cocok dengan pegawai lokal, role default **Pegawai** dari SSO menginisialisasi role internal Pegawai secara otomatis agar akun dapat langsung dimapping saat login pertama. Role internal yang sudah tersimpan tetap menjadi sumber keputusan akses pada request berikutnya.
3. Nomor telepon Keycloak dapat dipetakan bila LLDIKTI menyediakannya sebagai custom attribute. Nama claim/objek aktual tidak boleh ditebak; implementasi membaca kontrak respons yang diberikan LLDIKTI.
4. Role selain default Pegawai, permission, dan semua otorisasi fitur tetap dikelola serta dievaluasi oleh SIMPEG. Tidak ada claim Keycloak yang langsung memberikan permission aplikasi di luar inisialisasi default Pegawai di atas.

## K-MTG-03 — Switch role berbasis permission

1. Sistem menyediakan switch role bagi aktor yang memiliki permission khusus untuk kebutuhan demo, pengujian, dan dukungan, di development maupun production.
2. Switch role adalah simulasi **role**, bukan impersonasi identitas/pegawai lain. Identitas aktor, kepemilikan data, dan jejak audit tidak berubah.
3. Role efektif sementara dan permission efektif sementara disimpan secara persisten (`temporary_role` dan `temporary_permission`) sehingga tetap berlaku setelah logout/login sampai aktor melakukan revert. Revert mengosongkan nilai sementara dan mengembalikan role asli.
4. Target role dibatasi pada role yang lebih rendah dari role asli aktor. Perubahan, penggunaan, dan revert wajib diaudit serta seluruh endpoint tetap memeriksa permission efektif di backend.

## K-MTG-04 — Hari libur dan dokumen pegawai

1. Hari Libur dikelola pada menu/halaman tersendiri, tidak lagi sebagai tab Data Master. Halaman menampilkan kalender di bagian atas dan tabel hari libur di bawahnya.
2. Dari profil pegawai, Admin Kepegawaian dapat langsung mengunggah dokumen tambahan melalui pemilihan jenis dokumen. Tampilan memisahkan dokumen wajib/SK pada tabel atas dari dokumen tambahan, seperti KTP, KK, dan ijazah, pada tabel bawah.
3. Menu dokumen terpusat tetap dipertahankan untuk Super Admin/Admin Kepegawaian ketika perlu mencari dokumen lintas pegawai.

## K-MTG-05 — Persiapan WhatsApp Business

1. Tim menyusun dokumen template WhatsApp untuk setiap jenis notifikasi yang akan diajukan, berisi contoh pesan dan daftar variabel payload. Contoh minimal mencakup EWS kenaikan pangkat dan Satyalancana.
2. LLDIKTI mengajukan template kepada Meta dan mengembalikan template ID beserta petunjuk pemasangan. Setelah itu integrasi dapat diuji dengan pola pemilihan template dan pengisian variabel, bukan pengiriman teks bebas.
3. Aktivasi adapter/provider WhatsApp tidak dilakukan sebelum template ID dan petunjuk layanan diterima dari LLDIKTI.

## K-MTG-06 — Validasi revisi dan deployment

1. Target penyelesaian direvisi dari rencana tanggal 20 menjadi **akhir Agustus 2026**, dengan evaluasi Zoom segera setelah satu kelompok revisi siap; tidak perlu menunggu rapat rutin hari Jumat.
2. Setelah penerimaan fitur oleh Kepegawaian, tim menyusun panduan penggunaan per role yang menerangkan fitur, langkah penggunaan, dan dampak aksi.
3. LLDIKTI akan memperbarui image PHP/container pada branch `development` dan dapat menaikkan versi PostgreSQL sedikit. Sebelum lingkungan baru dipakai sebagai acuan, data perlu dapat dibackup dan direstore, lalu aplikasi, migrasi, queue, dan scheduler diverifikasi kembali.

## Dampak dokumentasi

- [PRD SIMPEG Fase 1](PRD-DLL/PRD-SIMPEG-Fase1-Core.md), [User Stories](PRD-DLL/User-Stories-SIMPEG-Fase1.md), [Issues](PRD-DLL/Issues-SIMPEG-Fase1.md), [Panduan Penulisan Kode](PRD-DLL/Panduan-Penulisan-Kode-SIMPEG.md), dan [Keputusan Cuti Saldo Tahap 0](Keputusan-Cuti-Saldo-Tahap-0.md) merujuk keputusan ini sebagai addendum terbaru.
- Fitur yang muncul dari keputusan ini ditandai **belum diimplementasikan** sampai ada bukti code review, test, dan QA yang sesuai.



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
