# Tracking Role: Pimpinan

> **Authorization target — 7 September 2026:** [PATEN dan RBAC](../Keputusan-RBAC-Pemisahan-Capability-Paten-dan-Configurable-7-September-2026.md) menggantikan **hanya klausul authorization** lama yang menyamaratakan self sebagai permission checkbox, universal Super Admin bypass, actor allowlist Switch Role, manual/cancellation Admin-only, dan role guard/default export yang bertentangan. Klausul tersebut **Superseded**; tanggal, checklist, assignment dan evidence implementasi historis di bawah tetap merupakan snapshot saat dicatat. Domain/lifecycle, scope, privacy, state, ledger, append-only dan audit tetap berlaku. Target aktif serta kebutuhan evidence baru ada pada bagian akhir dokumen ini.

| Field | Nilai |
|---|---|
| Role internal | `pimpinan` |
| Tanggal analisis ulang | 27 Juli 2026 |
| Basis verifikasi | Branch `development` @ `e82b527` (sesudah PR #121–#131, termasuk perbaikan dashboard PR #125) |
| Dokumen asal (dikonsolidasi ke file ini) | `Analisis-Frontend-Role-Pimpinan.md` — audit 21 Juli 2026 |
| Acuan produk | PRD v1.15 (dashboard seluruh pegawai, PYBMC/approver final, data pegawai read-only, laporan), US-4.6, US-5.2, US-8.1, US-8.6, US-9.1B, L1/L1b/L2/L3 |
| Status keseluruhan | ⚠️ **Sebagian besar sesuai** — inti operasional lengkap; sisa: akurasi tren W7, konsistensi label, dan 1 keputusan produk |

> **Addendum 31 Agustus 2026:** verifikasi Pimpinan harus mencakup chain yang dapat memiliki Atasan Langsung/PYBMC dengan aktor sama, output formulir Nama–Jabatan–Peran, dan scope Reporting Statistik bila role ini diberi akses. Bukti implementasi sebelum addendum tidak menutup kriteria tersebut.

## Ringkasan

Audit 21 Juli menemukan 6 kelompok masalah besar (UI tidak read-only, jalur laporan ganda, filter
kurang, dashboard tidak akurat, search EWS mati, konflik dokumen audit log). Verifikasi ulang
27 Juli menunjukkan **mayoritas sudah ditutup** — terutama oleh perbaikan dashboard (PR #125) dan
konsolidasi laporan Pimpinan. Yang tersisa bersifat terlokalisir.

## ✅ Sudah Sesuai (terverifikasi 27 Juli)

| # | Area | Bukti |
|---|---|---|
| 1 | Keputusan cuti final US-4.6 — hanya approver step aktif, 4 label resmi tanpa `Tolak`, catatan wajib untuk non-`Disetujui`, audit + notifikasi + pengurangan saldo + bukti QR | `ListPimpinanLeavesAction`, `LeaveApprovalService` |
| 2 | Detail pegawai Pimpinan read-only — NIK keluarga tidak tampil, ARIA + navigasi keyboard pada tab | `pimpinan.pegawai.show` |
| 3 | **Data Pegawai benar-benar read-only dari UI** (dulu ❌ P1) — Tambah/Import/Edit/checkbox bulk/Export Excel dibungkus `@if(!$isReadOnly)`; Pimpinan mendapat link "Laporan Pegawai" sebagai gantinya | `admin/pegawai/index.blade.php:364-413,495,619-631,695`; flag di `PimpinanEmployeeController.php:75` |
| 4 | **Sidebar laporan menunjuk jalur Pimpinan** (dulu ❌ P1 — dua jalur membingungkan) — menu kini ke `pimpinan.laporan.pegawai`, `pimpinan.laporan.cuti`, `pimpinan.laporan.kepangkatan` | `components/layouts/app.blade.php:210-216` |
| 5 | **Filter laporan custom lengkap sesuai US-9.1B** (dulu ❌ P1) — Unit Kerja, Jenis Pegawai, Jabatan kini tersedia di samping Nama/NIP, Golongan, Status, periode pensiun | `pimpinan/laporan/pegawai.blade.php:108-186` |
| 6 | Dashboard W5 distribusi golongan penuh `I/a–IV/e` (dulu ❌ digabung per angka romawi) | `BuildPimpinanDashboardAction.php:129-133` |
| 7 | Dashboard W2 kenaikan pangkat "Golongan (Asal → Tujuan)" (dulu satu kolom) | `BuildPimpinanDashboardAction.php:87-97`, `pimpinan/dashboard.blade.php:190,210-216` |
| 8 | KPI EWS Aktif memakai total sebenarnya, preview 5 baris terpisah (dulu ter-cap 5) | `BuildPimpinanDashboardAction.php:117-118` |
| 9 | Kartu W1 menaut ke daftar pegawai Pimpinan (dulu `href="#"`) | `pimpinan/dashboard.blade.php:125` |
| 10 | Pencarian EWS berfungsi server-side — nama/NIP difilter sebelum paginasi (dulu param diabaikan) | `PimpinanEwsController.php:14,19-26` |
| 11 | `per_page` EWS di-whitelist 10/25/50; markup `<p>…</span>` invalid sudah hilang | `PimpinanEwsController.php:29-30`, `pimpinan/ews/index.blade.php:62-66,82` |
| 12 | Laporan cuti & laporan kepangkatan (Excel/PDF fixed) jalur Pimpinan, teruji | `PimpinanReportController`, `ExportRankHistoryPdfAction` |

## ⚠️ Belum Sesuai / Sisa Pekerjaan

| # | Prioritas | Temuan (terverifikasi 27 Juli) | Tindak lanjut |
|---|:---:|---|---|
| 1 | P1 | **W7 belum tren historis sebenarnya** — filter status kini lewat `tanggal_pensiun` (perbaikan parsial), tetapi basis titik bulanan masih `whereDate('created_at','<=',akhir bulan)` (`BuildPimpinanDashboardAction.php:26-39`); angka bulan lampau terdistorsi oleh kapan record diinput, bukan kondisi kepegawaian saat itu | Task tracker #24 |
| 2 | P2 | **Label `Perlu Perubahan`** masih dipakai di `pimpinan/cuti/index.blade.php:15` (juga `admin/cuti/index.blade.php:17`, `admin/cuti/show.blade.php:305`); istilah resmi keputusan adalah `Perubahan` | Task tracker #25 |
| 3 | Keputusan produk | **Link audit log dari W6** — PRD/US-8.1 meminta link ke audit detail, sedangkan sidebar mengecualikan `audit-log` bagi Pimpinan. Belum diputuskan: beri akses read-only ter-masking, atau revisi kriteria W6 jadi ringkasan saja. Belum masuk keputusan kickoff K-1/K-3 | Eskalasi ke pemilik produk (bersama task #15) |

## Catatan Kualitas Kode (P2–P3, belum diverifikasi ulang 27 Juli)

Temuan audit 21 Juli berikut bersifat non-blocking dan belum dicek ulang; validasi saat menyentuh file terkait:

- Eager loading detail pegawai Pimpinan memuat relasi/reference yang tidak dirender view.
- Pratinjau laporan cuti/kepangkatan memuat seluruh Collection lalu `forPage()` di memori.
- Kalkulasi SVG tren W7 masih di Blade — layak dipindah ke view model saat W7 diperbaiki (gabungkan dengan task #24).

## Riwayat Temuan Audit 21 Juli → Kondisi Sekarang

| Temuan lama | Kondisi 27 Juli |
|---|---|
| ❌ P1 UI Data Pegawai tidak read-only | ✅ Diperbaiki |
| ❌ P1 Sidebar → laporan generik; halaman custom tak terjangkau | ✅ Diperbaiki (sidebar → `pimpinan.laporan.*`) |
| ❌ P1 Filter custom kurang (unit/jenis/jabatan) | ✅ Diperbaiki |
| ❌ P1 Laporan generik bocor kontak & pegawai nonaktif | Tidak lagi ditautkan untuk Pimpinan; closure `laporan.pegawai` sendiri masih hidup di area Admin — lihat `Role-Admin-Kepegawaian.md` (task #18) |
| ❌ P1 Modal custom di halaman generik mati | Berpindah cakupan ke Admin (task #20) — jalur Pimpinan kini memakai form custom sendiri |
| ❌ W5 golongan digabung, W7 tren, KPI EWS cap 5, W2 satu kolom, W1 `#` | ✅ Semua diperbaiki kecuali **W7** (parsial — baris ⚠️ #1) |
| ⚠️ Search EWS mati, HTML invalid, per_page bebas | ✅ Ketiganya diperbaiki |
| ⚠️ Istilah `Perlu Perubahan` | ⚠️ Masih (baris ⚠️ #2) |
| Konflik dokumen link audit W6 | ⚠️ Masih menunggu keputusan produk (baris ⚠️ #3) |


## Target delivery authorization — 7 September 2026

Sumber aktif: [keputusan PATEN dan RBAC](../Keputusan-RBAC-Pemisahan-Capability-Paten-dan-Configurable-7-September-2026.md) dan [User Stories v1.17](../PRD-DLL/User-Stories-SIMPEG-Fase1.md). **Status: target belum dibuktikan; bukan perubahan status checklist historis.**

Scope canonical role ini: **global sesuai sensitivitas**. `employees.export` default **OFF**; grant/revoke matrix tetap efektif dan seluruh output mengikuti scope/filter/privacy. `users.switch_role` configurable; bila ON target: **Kepala Bagian/Pegawai**; same/higher/invalid/chained ditolak. Permission tidak mengganti identitas/employee ownership dengan user lain. PATEN self/assignment yang sah tidak membutuhkan checkbox; manual dan cancellation memakai permission + scope/domain, bukan allowlist role permanen.

- Matrix hanya **🔒 PATEN** dan **⚙️ RBAC**. PATEN ditentukan identity/ownership/assignment/lifecycle/domain; RBAC memakai effective permission matrix lalu canonical scope/privacy/domain. Super Admin tidak mempunyai universal bypass.
- Scope canonical: SA/Admin/Pimpinan global sesuai sensitivitas; Kepala Bagian bawahan langsung; Pegawai self. Filter/ID tidak membypass scope. Dokumen/SK termasuk milik sendiri tetap RBAC dan private-file authorization.
- Export default SA/Admin ON, Pimpinan/Kepala Bagian/Pegawai OFF; semua role dapat grant tanpa perubahan kode. Target Switch Role mengikuti hierarki asli SA → Admin → Pimpinan → Kepala Bagian → Pegawai, hanya ke role lebih rendah, persisten sampai revert.
- Manual/cancellation role-only lama **Superseded** oleh `cuti.manual.manage`/`cuti.cancellation.manage` + scope/domain. Ledger, replay, reservation hold/release/continue, state, lock/concurrency, audit/notifikasi tetap. Reaktivasi K-STATUS-04 tetap effective SA/Admin + `employees.restore`; invariant lifecycle tidak menjadi kategori matrix ketiga.
- Migrasi caller self dan katalog mengikuti §9 keputusan, menjaga grants/pivot existing; tidak otomatis reseed/delete atau mengklaim seluruh key target telah ada.
- Regression perlu grant/revoke lintas role termasuk SA OFF, scope/foreign ID, PATEN tanpa checkbox, lifecycle/ownership/eligibility, dokumen privat, append-only, manual/cancel state/concurrency dan seluruh switch/revert. PostgreSQL untuk DB-sensitive serta browser matrix/menu/direct URL/console; catat SHA/environment/expected/actual/audit tersanitasi.

**Koordinasi SSO:** Issue GitHub aktif [#6](https://github.com/LLDIKTI16/simpeg/issues/6) tetap core SSO (mapping/reuse/non-overwrite role/binding/concurrency/audit/claim-UAT), mengecualikan Switch Role aktif [#7](https://github.com/LLDIKTI16/simpeg/issues/7). PR [#21](https://github.com/LLDIKTI16/simpeg/pull/21) OPEN `d323ca03` saat verifikasi 7 September, bukan bukti 31 AC baru selesai. Nomor #6/#7 backlog historis notifikasi bukan nomor aktif tersebut. Regression lintas modul memerlukan koordinasi terpisah, bukan pemindahan seluruh redesign ke owner SSO; nomor issue/owner/jadwal baru belum ditetapkan. Kewenangan mutasi matrix, anti-lockout dan bootstrap recovery tetap Open Product Decision.
