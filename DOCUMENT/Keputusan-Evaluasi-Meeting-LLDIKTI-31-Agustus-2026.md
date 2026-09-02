# Keputusan Produk — Evaluasi SIMPEG Bersama LLDIKTI

| Field | Detail |
|---|---|
| **Tanggal keputusan dokumentasi** | 31 Agustus 2026; klarifikasi pembatalan dan alasan konfigurasi 1 September 2026; klarifikasi duplikasi lintas peran 2 September 2026 |
| **Status** | **Disetujui** — melengkapi dan menggantikan keputusan terdahulu pada area yang disebutkan di dokumen ini |
| **Dasar** | Notulen *Evaluasi Projek SIMPEG bersama Mahasiswa Magang Univ Klabat*, klarifikasi stakeholder 31 Agustus 2026, jawaban tertulis LLDIKTI 1 September 2026 mengenai permohonan pembatalan cuti, keputusan pengguna 1 September 2026 mengenai kewajiban alasan konfigurasi chain, serta keputusan pengguna 2 September 2026 mengenai duplikasi aktor lintas peran |
| **Dokumen produk terkait** | [PRD SIMPEG Fase 1 Core v1.16](PRD-DLL/PRD-SIMPEG-Fase1-Core.md) dan [User Stories SIMPEG Fase 1 v1.16](PRD-DLL/User-Stories-SIMPEG-Fase1.md); snapshot yang berlaku saat rapat 31 Agustus adalah v1.12 |
| **Dokumen keputusan terdahulu** | [Keputusan Evaluasi Meeting LLDIKTI 15 Agustus 2026](Keputusan-Evaluasi-Meeting-LLDIKTI-15-Agustus-2026.md) dan [Keputusan Cuti Saldo Tahap 0](Keputusan-Cuti-Saldo-Tahap-0.md) |

> Dokumen ini menjaga keputusan 15–25 Agustus sebagai riwayat. Hanya butir yang secara eksplisit disebut **digantikan** di bawah yang tidak lagi menjadi kontrak aktif. Nama teknis yang sudah ada, seperti role, route, atau field `kepala_bagian`, **tidak** otomatis berubah hanya karena label bisnis diubah; perubahan schema atau RBAC memerlukan keputusan tersendiri.

> **Pembaruan RBAC 2 September 2026:** role yang disebut pada dokumen ini menggambarkan konfigurasi/default pada saat keputusan 31 Agustus dicatat. Permission matrix database kini menjadi sumber kebenaran. Hak generic, termasuk pengelolaan fitur dan baca dokumen, dapat diassign atau dicabut dengan scope/policy; hanya business invariant eksplisit seperti Switch Role yang memakai pembatas role asli. Lihat [Keputusan RBAC Configurable dan Switch Role](Keputusan-RBAC-dan-Switch-Role-2-September-2026.md).

## K-MTG-10.1 — Terminologi dan chain approval cuti

1. Urutan kanonis approval cuti adalah **nol atau lebih Verifikator → Atasan Langsung → PYBMC**.
2. **Atasan Langsung** adalah peran bisnis cuti yang ditetapkan secara eksplisit per pegawai. Ia tidak identik dengan nama jabatan struktural Kepala Bagian; pejabat dengan jabatan lain dapat menjadi Atasan Langsung bila ditetapkan pada konfigurasi pegawai tersebut.
3. UI dan dokumen bisnis cuti wajib memakai label **Atasan Langsung**, bukan **Kepala Bagian**. Bila tidak ada Verifikator, chain dimulai langsung pada Atasan Langsung tanpa menampilkan label atau placeholder “tanpa verifikator”.
4. Bila orang yang sama mengisi lebih dari satu **peran berbeda**, snapshot tetap menyimpan setiap tahap dan orang tersebut wajib melakukan satu tindakan terpisah untuk setiap peran yang sedang aktif. Aturan ini berlaku untuk kombinasi Verifikator–Atasan Langsung, Verifikator–PYBMC, Atasan Langsung–PYBMC, maupun satu orang yang mengisi ketiga peran.
5. Orang yang sama tidak boleh diulang pada **peran yang sama** dalam satu chain, misalnya menjadi dua Verifikator. Konfigurasi seperti ini ditolak sebelum disimpan dengan pesan yang dapat ditindaklanjuti; sistem tidak membuat lalu melewati tahap tersebut saat runtime.
6. Ketentuan lama yang menyatakan chain `Verifikator → Kepala Bagian → PYBMC`, atau meminta sistem melewati tahap hanya karena pegawainya sudah bertindak pada peran sebelumnya, digantikan oleh keputusan ini pada surface bisnis dan acceptance criteria baru.
7. Pada konfigurasi chain, **Alasan Perubahan Chain Pegawai** dan **Alasan Backfill** bersifat opsional. **Alasan Penerapan Chain ke Unit** dan **Alasan PYBMC Global** tetap wajib karena berdampak massal atau luas. Audit tetap mencatat aktor, nilai sebelum/sesudah, dan metadata aksi meskipun alasan opsional tidak diisi.

## K-MTG-10.2 — Pembatalan, revisi, dan penangguhan cuti

1. Selama pengajuan belum memperoleh keputusan final PYBMC, Pegawai dapat mengajukan **permohonan pembatalan tersendiri** dengan alasan wajib. Pegawai tidak membatalkan pengajuan utama secara langsung.
2. Saat permohonan pembatalan dikirim, approval pengajuan utama ditahan dan reservasi saldo tetap dipertahankan. Hanya satu permohonan pembatalan aktif yang dapat diproses untuk pengajuan yang sama.
3. Admin Kepegawaian yang berwenang menerima notifikasi dan memutus permohonan tersebut. Jika disetujui, pengajuan utama menjadi batal dan reservasi saldo dilepas secara atomik. Jika tidak disetujui, approval utama dilanjutkan dari tahap sebelumnya dengan tindakan approval yang sudah ada tetap tercatat.
4. Permohonan, keputusan Admin, perubahan status, dan mutasi reservasi wajib tercatat pada audit serta tidak menghapus pengajuan, snapshot, timeline, atau histori. Pegawai menerima notifikasi hasil keputusan pembatalan.
5. Revisi langsung hanya tersedia sebelum ada tindakan approval. Setelah Verifikator atau approver lain bertindak, perubahan data dilakukan dengan meminta pembatalan; setelah pembatalan disetujui, Pegawai membuat pengajuan baru yang memulai chain dari awal.
6. Cuti yang sudah berstatus final `Disetujui` tidak boleh dihapus dan tidak memakai permohonan pembatalan Pegawai. Admin Kepegawaian dapat menetapkannya menjadi `Ditangguhkan` dengan alasan wajib, menjaga histori dan audit, serta menjalankan koreksi/replay ledger secara atomik agar pemakaian final tidak tersisa keliru.
7. Permohonan pembatalan merupakan form/record tersendiri di SIMPEG dan tidak menambah kewajiban dokumen PDF pembatalan.

## K-MTG-10.3 — Sumber pemakaian cuti historis

1. **Cuti di Luar SIMPEG** atau cuti manual adalah satu sumber fakta pemakaian tahunan historis/transisi untuk N-2, N-1, dan tahun berjalan sebelum go-live, serta untuk cuti yang telah diproses dan disetujui secara manual ketika layanan SIMPEG mengalami downtime setelah go-live.
2. Halaman **Catat Pemakaian Tahunan** hanya menampilkan agregat hasil sumber fakta tersebut. Input angka pemakaian langsung pada halaman ringkasan dinonaktifkan agar saldo dan rollover tidak terhitung ganda.
3. Cuti operasional baru diproses melalui pengajuan cuti SIMPEG normal. Ketika layanan downtime, proses manual harus diselesaikan dan disetujui di luar sistem; setelah SIMPEG pulih, Admin Kepegawaian mencatatnya sebagai fakta final melalui Cuti di Luar SIMPEG. Entri manual tidak boleh dipakai sebagai jalan pintas ketika SIMPEG tersedia atau untuk pengajuan yang belum memperoleh persetujuan di luar SIMPEG.
4. Nomor dokumen dan dokumen pendukung cuti manual tetap opsional. Bila diberikan, berkas wajib divalidasi dan disimpan privat; perubahan atau koreksi tetap beralasan, teraudit, dan tidak melakukan hard delete.

## K-MTG-10.4 — Formulir dan dokumen cuti

1. Formulir/PDF cuti menampilkan **Nama**, **Jabatan**, dan **Peran** pada setiap pihak approval.
2. Jabatan yang ditampilkan adalah jabatan aktual/terkini yang relevan pada saat dokumen dibuat. Peran menggunakan `Verifikator`, `Atasan Langsung`, atau `PYBMC`, bukan sekadar label “Pejabat”.
3. Tata letak formulir menyediakan pemisah ruang yang jelas antara kop surat dan tabel isi tanpa mengubah kewajiban QR verifikasi atau privasi dokumen.

## K-MTG-10.5 — Kelengkapan dokumen PNS dan CPNS

1. PNS wajib memiliki **SK Pengangkatan PNS**; CPNS wajib memiliki **SK Pengangkatan CPNS**. Kewajiban SK Pangkat terbaru, SK Jabatan terbaru, dan SK KGB terbaru tetap mengikuti matriks dokumen aktif yang telah disetujui.
2. Saat jenis pegawai berubah dari CPNS menjadi PNS, sistem mengevaluasi ulang kelengkapan terhadap matriks PNS. Status kelengkapan menjadi belum lengkap sampai SK Pengangkatan PNS tersedia.
3. Pengelolaan matriks dan berkas tetap dibatasi untuk Super Admin/Admin Kepegawaian sesuai permission; Fase 1 tidak menambahkan self-service dokumen oleh Pegawai.
4. Butir K-MTG-08.5–08.6 pada keputusan 21/24 Agustus yang menyatakan kewajiban PNS dan CPNS sama persis digantikan oleh ketentuan ini.

## K-MTG-10.6 — Reporting Statistik Kepegawaian

1. Fase 1 menambah halaman **Reporting Statistik Kepegawaian** yang terpisah dari Data Master, dashboard ringkas, dan ekspor Excel/PDF.
2. Halaman menyajikan agregat/chart yang minimal dapat dianalisis berdasarkan golongan, jenis jabatan, jabatan, unit kerja, dan jenis kepegawaian.
3. Akses, scope data, dan masking mengikuti akses dashboard/laporan yang sudah berlaku. Agregasi dilakukan di database dengan query terikat/bounded; halaman tidak memuat keseluruhan data pegawai ke browser untuk menghitung statistik.

## Invarian yang tidak berubah

- Audit Log tetap immutable; usulan retensi 90 hari tidak ditetapkan sebagai aturan produk oleh keputusan ini.
- Alasan tetap wajib untuk keputusan cuti non-persetujuan, termasuk `Perubahan`, `Ditangguhkan`, dan `Tidak Disetujui`.
- Channel notifikasi tetap mengikuti konfigurasi global. Preferensi notifikasi per pengguna belum menjadi requirement Fase 1.
- Kegagalan WhatsApp `422` adalah temuan integrasi yang ditangani melalui kontrak/provider; bukan perubahan status atau aturan domain cuti.
- Bootstrap Super Admin hanya berlaku bagi pengguna pertama ketika sistem belum memiliki user. Pengguna berikutnya mengikuti pemetaan email/data pegawai dan RBAC; mereka tidak otomatis menjadi Super Admin.
- EWS kenaikan pangkat tetap dihitung dari TMT/SK pangkat terakhir ditambah empat tahun.

## Klarifikasi yang telah ditutup

- Batas pembatalan setelah Verifikator bertindak telah diputuskan pada 1 September 2026: Pegawai mengajukan permohonan pembatalan beralasan, approval utama ditahan, dan Admin Kepegawaian menyetujui atau menolak pembatalan tersebut.
- Perlakuan pegawai yang sama pada beberapa peran telah diputuskan pada 2 September 2026: setiap peran tetap memerlukan tindakan tersendiri, sedangkan pengulangan pegawai pada peran yang sama ditolak saat konfigurasi.

## Batas implementasi yang tetap berlaku

- Perubahan label bisnis tidak mengesahkan migrasi role `kepala_bagian`, route `/kepala-bagian/*`, service legacy, atau field `kepala_bagian_id`.

## Dampak dokumentasi dan delivery

- PRD dan User Stories aktif v1.16 telah menyelaraskan keputusan 31 Agustus–2 September, termasuk addendum RBAC dan klarifikasi duplikasi lintas peran; v1.12 dipertahankan sebagai snapshot sejarah rapat.
- Backlog, tracker sprint/role, panduan pengguna, runbook, serta skenario UAT wajib menambahkan pekerjaan dan pengujian baru; evidence lama tidak boleh diklaim sebagai bukti penerimaan keputusan ini.
- Implementasi baru hanya dapat dinyatakan selesai setelah test PostgreSQL, audit, authorization/data scope, browser smoke, dan UAT yang relevan tersedia.
