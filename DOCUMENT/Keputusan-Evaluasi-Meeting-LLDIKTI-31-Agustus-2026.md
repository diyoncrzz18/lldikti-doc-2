# Keputusan Produk — Evaluasi SIMPEG Bersama LLDIKTI

| Field | Detail |
|---|---|
| **Tanggal keputusan dokumentasi** | 31 Agustus 2026 |
| **Status** | **Disetujui** — melengkapi dan menggantikan keputusan terdahulu pada area yang disebutkan di dokumen ini |
| **Dasar** | Notulen *Evaluasi Projek SIMPEG bersama Mahasiswa Magang Univ Klabat* yang disampaikan pengguna pada 31 Agustus 2026 |
| **Dokumen produk terkait** | [PRD SIMPEG Fase 1 Core v1.12](PRD-DLL/PRD-SIMPEG-Fase1-Core.md) dan [User Stories SIMPEG Fase 1 v1.12](PRD-DLL/User-Stories-SIMPEG-Fase1.md) |
| **Dokumen keputusan terdahulu** | [Keputusan Evaluasi Meeting LLDIKTI 15 Agustus 2026](Keputusan-Evaluasi-Meeting-LLDIKTI-15-Agustus-2026.md) dan [Keputusan Cuti Saldo Tahap 0](Keputusan-Cuti-Saldo-Tahap-0.md) |

> Dokumen ini menjaga keputusan 15–25 Agustus sebagai riwayat. Hanya butir yang secara eksplisit disebut **digantikan** di bawah yang tidak lagi menjadi kontrak aktif. Nama teknis yang sudah ada, seperti role, route, atau field `kepala_bagian`, **tidak** otomatis berubah hanya karena label bisnis diubah; perubahan schema atau RBAC memerlukan keputusan tersendiri.

## K-MTG-10.1 — Terminologi dan chain approval cuti

1. Urutan kanonis approval cuti adalah **nol atau lebih Verifikator → Atasan Langsung → PYBMC**.
2. **Atasan Langsung** adalah peran bisnis cuti yang ditetapkan secara eksplisit per pegawai. Ia tidak identik dengan nama jabatan struktural Kepala Bagian; pejabat dengan jabatan lain dapat menjadi Atasan Langsung bila ditetapkan pada konfigurasi pegawai tersebut.
3. UI dan dokumen bisnis cuti wajib memakai label **Atasan Langsung**, bukan **Kepala Bagian**. Bila tidak ada Verifikator, chain dimulai langsung pada Atasan Langsung tanpa menampilkan label atau placeholder “tanpa verifikator”.
4. Bila Atasan Langsung dan PYBMC menunjuk orang yang sama, snapshot tetap menyimpan **dua tahap berbeda** dan orang tersebut tetap menyelesaikan dua tindakan terpisah sesuai peran yang sedang aktif. Aturan umum untuk mencegah/menolak duplikasi approver tetap berlaku bagi kombinasi tahap lain.
5. Ketentuan lama yang menyatakan chain `Verifikator → Kepala Bagian → PYBMC`, atau meminta sistem melewati pasangan Atasan Langsung/PYBMC yang orangnya sama, digantikan oleh keputusan ini pada surface bisnis dan acceptance criteria baru.

## K-MTG-10.2 — Pembatalan, revisi, dan penangguhan cuti

1. Pegawai dapat membatalkan atau merevisi pengajuan melalui aksi resmi sebelum terdapat tindakan approval pada pengajuan tersebut. Pengajuan aktif yang belum dibatalkan/revisi tetap mencegah pengajuan aktif baru yang bertabrakan.
2. Cuti yang sudah berstatus final `Disetujui` tidak boleh dihapus. Admin Kepegawaian dapat menetapkannya menjadi `Ditangguhkan` dengan alasan wajib, menjaga histori dan audit, serta menjalankan koreksi/replay ledger secara atomik agar pemakaian final tidak tersisa keliru.
3. Setelah tidak ada pengajuan aktif, Pegawai dapat mengajukan cuti baru melalui alur normal. Pengubahan status administrasi tidak boleh menghapus snapshot approval atau jejak keputusan sebelumnya.
4. Keputusan ini membedakan `Ditangguhkan` ketika pengajuan masih dalam approval—reservasi tetap mengikuti status pengajuan aktif—dari penangguhan administratif atas cuti yang sudah final disetujui, yang membutuhkan koreksi pemakaian final melalui ledger.

## K-MTG-10.3 — Sumber pemakaian cuti historis

1. **Cuti di Luar SIMPEG** atau cuti manual adalah satu sumber fakta pemakaian tahunan historis/transisi untuk N-2, N-1, dan tahun berjalan sebelum go-live.
2. Halaman **Catat Pemakaian Tahunan** hanya menampilkan agregat hasil sumber fakta tersebut. Input angka pemakaian langsung pada halaman ringkasan dinonaktifkan agar saldo dan rollover tidak terhitung ganda.
3. Cuti operasional baru diproses melalui pengajuan cuti SIMPEG normal. Entri manual tidak boleh dipakai sebagai jalan pintas untuk pengajuan baru yang belum memperoleh persetujuan di luar SIMPEG.
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

## Open question yang tetap harus dikonfirmasi sebelum implementasi

1. **Batas pembatalan/revisi:** notulen menekankan waktu sebelum persetujuan Atasan Langsung, sedangkan PRD merekam batas aman sebelum tindakan approval pertama. Perlu konfirmasi apakah Pegawai masih boleh membatalkan setelah Verifikator bertindak tetapi sebelum Atasan Langsung.
2. **Pengecualian downtime setelah go-live:** keputusan 15/20 Agustus mengizinkan fakta cuti manual saat layanan tidak tersedia. Keputusan ini menekankan data historis/transisi dan penggunaan alur normal untuk cuti baru. Perlu konfirmasi apakah pengecualian downtime tetap berlaku.
3. **RBAC dan schema legacy:** perubahan label bisnis tidak mengesahkan migrasi role `kepala_bagian`, route `/kepala-bagian/*`, service legacy, atau field `kepala_bagian_id`.

## Dampak dokumentasi dan delivery

- PRD dan User Stories v1.12 sudah menjadi kontrak produk yang telah diselaraskan.
- Backlog, tracker sprint/role, panduan pengguna, runbook, serta skenario UAT wajib menambahkan pekerjaan dan pengujian baru; evidence lama tidak boleh diklaim sebagai bukti penerimaan keputusan ini.
- Implementasi baru hanya dapat dinyatakan selesai setelah test PostgreSQL, audit, authorization/data scope, browser smoke, dan UAT yang relevan tersedia.
