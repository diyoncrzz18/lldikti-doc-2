# Tracking Role: Admin Kepegawaian

> **Authorization target — 7 September 2026:** [PATEN dan RBAC](../Keputusan-RBAC-Pemisahan-Capability-Paten-dan-Configurable-7-September-2026.md) menggantikan **hanya klausul authorization** lama yang menyamaratakan self sebagai permission checkbox, universal Super Admin bypass, actor allowlist Switch Role, manual/cancellation Admin-only, dan role guard/default export yang bertentangan. Klausul tersebut **Superseded**; tanggal, checklist, assignment dan evidence implementasi historis di bawah tetap merupakan snapshot saat dicatat. Domain/lifecycle, scope, privacy, state, ledger, append-only dan audit tetap berlaku. Target aktif serta kebutuhan evidence baru ada pada bagian akhir dokumen ini.

> **Pembaruan kanonis 25 Agustus 2026:** seluruh penyebutan soft delete/restore, Data Backup, atau Data Nonaktif di bawah adalah snapshot audit kontrak lama dan berstatus **Superseded**. Lifecycle aktif mengikuti [Keputusan Lifecycle dan Status Pegawai](../Keputusan-Lifecycle-Status-Pegawai-25-Agustus-2026.md): satu Data Pegawai berfilter status; reaktivasi tersedia bagi Admin Kepegawaian ketika role efektif memiliki `employees.restore`.

| Field | Nilai |
|---|---|
| Role internal | `admin_kepegawaian` |
| Tanggal analisis ulang | 10 Agustus 2026 |
| Basis verifikasi | Branch `development` @ `1fd99cb` setelah PR #177 |
| Dokumen asal (dikonsolidasi ke file ini) | `Analisis-Frontend-Backend-Role-Admin-Kepegawaian.md` — audit 21 Juli 2026 |
| Acuan produk | PRD v1.15; bagian soft delete/restore superseded oleh keputusan lifecycle 25 Agustus 2026 |
| Status keseluruhan | ⚠️ **Belum sepenuhnya sesuai** — dari 4 gap utama audit lama, 1 sudah tuntas (set atasan); lifecycle nonaktif, laporan, dan audit-sensitif masih terbuka |

> **Addendum 31 Agustus–1 September 2026:** Admin Kepegawaian memerlukan kerja baru untuk memutus permohonan pembatalan cuti dan melanjutkan atau membatalkan flow secara auditabel, penangguhan cuti final dengan replay ledger, pengelolaan fakta cuti historis tanpa input angka langsung pada ringkasan, serta kelengkapan SK Pengangkatan yang membedakan PNS/CPNS. Status lama bukan bukti penerimaan kriteria ini.

> **Addendum 2 September 2026:** Admin Kepegawaian dapat menjadi actor asli Switch Role hanya bila memiliki `users.switch_role`; targetnya terbatas pada Pimpinan, Kepala Bagian, atau Pegawai. Akses fitur lain tetap berasal dari permission matrix efektif, bukan nama role default.

## Ringkasan

Audit 21 Juli menyimpulkan 4 gap utama: (1) penetapan atasan hanya Super Admin, (2) soft
delete/restore tidak bisa dituntaskan dari UI Admin, (3) laporan L1/L1b/L3 belum memenuhi kontrak,
(4) audit pegawai berisiko menyimpan NIK/No. KK plaintext. Verifikasi ulang 27 Juli: **gap 1 sudah
ditutup penuh**, gap 2 membaik di lapisan route tapi memburuk di navigasi, gap 3 dan 4 masih
terbuka dan sudah terpetakan ke task tracker Sprint 6–7.

## Rekonsiliasi Temuan — 10 Agustus 2026

Bagian audit 27 Juli di bawah dipertahankan sebagai kronologi. Temuan yang sudah ditutup:

- masking NIK/No. KK dan audit log server-side/immutable selesai melalui PR #174;
- Dashboard Admin data nyata dan tren W7 selesai melalui PR #150/#158/#164;
- export pegawai custom/PDF dan penerusan filter selesai melalui PR #154/#162/#167;
- event audit wajib US-7.1 AC-1 selesai melalui PR #176.

Hardening fail-closed CRUD pegawai/import, navigasi lifecycle pegawai, batas pengelolaan dokumen, dan keputusan password lokal/Keycloak tetap terbuka. Status baru ini menggantikan baris lama yang masih menyebut dashboard dummy, PDF belum ada, atau audit tanpa masking.

## ✅ Sudah Sesuai (terverifikasi 27 Juli)

| # | Area | Bukti |
|---|---|---|
| 1 | **Penetapan atasan/Kepala Bagian oleh Admin** (dulu ❌ P1 — bertentangan langsung dengan PRD) — route web + API kini `role:super_admin,admin_kepegawaian` + `permission:employees.update`, UI form tampil untuk Admin, memakai `AssignSupervisorRequest`, dan audit-nya `logOrFail()` | `routes/web.php:344-347`, `routes/api/v1/pegawai.php:137-140`, `admin/pegawai/show.blade.php:28-30,877`, `PegawaiController.php:604` |
| 2 | RBAC halaman — sidebar menyembunyikan menu privilese Super Admin; route konfigurasi menolak Admin | `AdminKepegawaianAccessTest` |
| 3 | Daftar/tambah/edit/detail pegawai dengan data & reference nyata, filter + pagination backend | `ListEmployeesAction`, `StoreEmployeeRequest`/`UpdateEmployeeRequest` |
| 4 | **Append-only riwayat ditegakkan dari form web** — id riwayat lama ditolak, action selalu membuat record baru | PR #129 |
| 5 | Import pegawai — wizard unggah→preview→validasi→eksekusi, template 2 baris contoh PNS+PPPK (PR #130), laporan hasil import permanen + CSV per-baris (PR #131) dengan kontrol kepemilikan batch | `EmployeeImportController::report()`, `EmployeeImportReportTest` |
| 6 | Tambah riwayat pangkat/jabatan/KGB via API kini ber-FormRequest (dulu `Request` mentah) | `StoreRankHistoryRequest`, `StorePositionHistoryRequest`, `StoreKgbHistoryRequest` |
| 7 | Dokumen inti — upload/edit metadata/detail/download sesuai permission | `DokumenController` (kecuali destroy/check-impact, lihat ⚠️ #4) |
| 8 | Monitoring cuti (bukan approver otomatis — sesuai PRD), rekap saldo + ledger + koreksi ber-audit, dokumen eksternal Kepala Lembaga, laporan cuti PDF/Excel fixed | `Actions/Cuti/*`, permission `cuti.read_all`, `cuti.kepala_lembaga_documents.manage` |
| 9 | EWS aktif + follow-up + pembaruan flag kinerja/Satyalancana dari detail pegawai | `ListActiveEwsAlertsAction`, `EmployeeSatyalancanaEligibilityTest` |
| 10 | **Email EWS Satyalancana** (dulu ❌ P1) — resolusi channel kini dari tabel `notification_event_channels`; `ews.satyalancana` ter-seed in-app + email | `NotificationChannelResolver.php:24-33`, `ReferenceSeeder.php:258` |
| 11 | Inbox notifikasi — paginator, tandai dibaca, ownership, CSRF | `notifications.index` |
| 12 | Audit log dapat dibaca Admin sesuai permission (kualitas halamannya lihat ⚠️ #6) | `routes/web.php:485-491` |

## Arsip ❌ / ⚠️ Belum Sesuai — snapshot 27 Juli 2026

| # | Prioritas | Temuan (terverifikasi 27 Juli) | Tindak lanjut |
|---|:---:|---|---|
| 1 | P0 | **Audit update pegawai bocor NIK/No. KK plaintext** — `UpdateEmployeeAction.php:35,349` masih `toArray()`; create sudah aman (`getRawOriginal()`) | Task tracker #2, Sprint 7 (7.2-1) |
| 2 | P1 | **Superseded sebagai kontrak aktif:** temuan route `data-nonaktif`, restore, dan Data Backup merekam implementasi lama. Pekerjaan aktif adalah satu Data Pegawai berfilter status, reaktivasi Super Admin/Admin Kepegawaian dengan effective `employees.restore`, serta blokir linked account Nonaktif lintas role | GitHub Issue #22 + keputusan lifecycle 25 Agustus 2026 |
| 3 | P1 | **Tombol Ubah Status / Hapus ke Backup disembunyikan dari Admin** — Blade masih cek `role === 'super_admin'` (`admin/pegawai/index.blade.php:632,673`) padahal route `pegawai.destroy`/`bulkDestroy` mengizinkan Admin ber-permission `employees.deactivate` (`routes/web.php:326-332`); UI dan route tidak konsisten | Backlog P1 (keputusan: tampilkan sesuai permission) |
| 4 | P1 | **Dokumen destroy/check-impact masih super_admin-only** (`routes/web.php:468-475`) — PRD menyebut Admin "mengelola dokumen"; batas kata *mengelola* belum pernah diputuskan resmi | Eskalasi keputusan produk (dicatat sejak audit 21 Juli) |
| 5 | P1 | **Dashboard Admin masih dummy kecuali panel EWS** — statistik/distribusi/cuti/pegawai/audit/hari-libur hardcoded di Blade | Task tracker #16 (Issue #39); kontrak K-3 sudah tersedia |
| 6 | P0/P2 | **Halaman Audit Log** — semua record `->get()` ke browser, filter/paginasi Alpine, payload tanpa masking | Sprint 7 (7.1-1); guard immutable = task #3 |
| 7 | P1 | **Laporan pegawai belum memenuhi L1/L1b/L3** — (a) preview masih closure lama yang memuat pegawai nonaktif + `email_pribadi`/`no_hp` ke browser; pengganti (`ExportPegawaiPreviewAction` + `LaporanController`) sudah ditulis tapi belum di-wire ke route; (b) modal custom Excel mati (state Alpine tidak didefinisikan); (c) PDF nominatif L1 belum ada; (d) L3 riwayat kenaikan pangkat belum punya route/menu untuk Admin (hanya `pimpinan.*`) | Task tracker #18, #20, #19 (Issue #42); L3-Admin perlu diangkat ke backlog |
| 8 | P2 | **Import: `validate` masih inline `$request->validate()`, `execute` tanpa validasi input** (`EmployeeImportController.php:57-63,73`) | Backlog P2 |
| 9 | P2 | **Endpoint web tambah riwayat pendidikan** (`pegawai.riwayat.store`) masih `Request` mentah dan `StoreEmployeeHistoryAction` tidak memvalidasi input (jalur pangkat/jabatan/KGB sudah ditutup dengan exception) | Backlog P2 |
| 10 | P2 | Form ubah password lokal di Profil — tidak sinkron dengan SSO Keycloak, tanpa audit | Keputusan produk (sama dengan Super Admin ⚠️ #16) |

## Riwayat Temuan Audit 21 Juli → Kondisi Sekarang

| Gap utama audit lama | Kondisi 27 Juli |
|---|---|
| ❌ Penetapan atasan Super Admin-only | ✅ Diperbaiki penuh (route + UI + FormRequest + audit strict) |
| ❌ Soft delete/restore tak tersentuh dari UI | ⚠️ Route dibuka untuk Admin; ❌ navigasi justru hilang untuk semua role — perlu menu/tautan |
| ❌ Laporan L1/L1b/L3 | ❌ Masih — preview/PII/modal/PDF L1 (task #18–#20), L3-Admin belum ada |
| ❌ Audit NIK/No. KK plaintext | ⚠️ Create aman; ❌ update masih (task #2) |
| ❌ Email Satyalancana | ✅ Diperbaiki (channel berbasis DB) |
| ⚠️ Riwayat via `Request` mentah | ✅ API pangkat/jabatan/KGB ber-FormRequest; ⚠️ sisa endpoint web pendidikan |


## Target delivery authorization — 7 September 2026

Sumber aktif: [keputusan PATEN dan RBAC](../Keputusan-RBAC-Pemisahan-Capability-Paten-dan-Configurable-7-September-2026.md) dan [User Stories v1.17](../PRD-DLL/User-Stories-SIMPEG-Fase1.md). **Status: target belum dibuktikan; bukan perubahan status checklist historis.**

Scope canonical role ini: **global sesuai sensitivitas**. `employees.export` default **ON**; grant/revoke matrix tetap efektif dan seluruh output mengikuti scope/filter/privacy. `users.switch_role` configurable; bila ON target: **Pimpinan/Kepala Bagian/Pegawai**; same/higher/invalid/chained ditolak. Permission tidak mengganti identitas/employee ownership dengan user lain. PATEN self/assignment yang sah tidak membutuhkan checkbox; manual dan cancellation memakai permission + scope/domain, bukan allowlist role permanen.

- Matrix hanya **🔒 PATEN** dan **⚙️ RBAC**. PATEN ditentukan identity/ownership/assignment/lifecycle/domain; RBAC memakai effective permission matrix lalu canonical scope/privacy/domain. Super Admin tidak mempunyai universal bypass.
- Scope canonical: SA/Admin/Pimpinan global sesuai sensitivitas; Kepala Bagian bawahan langsung; Pegawai self. Filter/ID tidak membypass scope. Dokumen/SK termasuk milik sendiri tetap RBAC dan private-file authorization.
- Export default SA/Admin ON, Pimpinan/Kepala Bagian/Pegawai OFF; semua role dapat grant tanpa perubahan kode. Target Switch Role mengikuti hierarki asli SA → Admin → Pimpinan → Kepala Bagian → Pegawai, hanya ke role lebih rendah, persisten sampai revert.
- Manual/cancellation role-only lama **Superseded** oleh `cuti.manual.manage`/`cuti.cancellation.manage` + scope/domain. Ledger, replay, reservation hold/release/continue, state, lock/concurrency, audit/notifikasi tetap. Reaktivasi K-STATUS-04 tetap effective SA/Admin + `employees.restore`; invariant lifecycle tidak menjadi kategori matrix ketiga.
- Migrasi caller self dan katalog mengikuti §9 keputusan, menjaga grants/pivot existing; tidak otomatis reseed/delete atau mengklaim seluruh key target telah ada.
- Regression perlu grant/revoke lintas role termasuk SA OFF, scope/foreign ID, PATEN tanpa checkbox, lifecycle/ownership/eligibility, dokumen privat, append-only, manual/cancel state/concurrency dan seluruh switch/revert. PostgreSQL untuk DB-sensitive serta browser matrix/menu/direct URL/console; catat SHA/environment/expected/actual/audit tersanitasi.

**Koordinasi SSO:** Issue GitHub aktif [#6](https://github.com/LLDIKTI16/simpeg/issues/6) tetap core SSO (mapping/reuse/non-overwrite role/binding/concurrency/audit/claim-UAT), mengecualikan Switch Role aktif [#7](https://github.com/LLDIKTI16/simpeg/issues/7). PR [#21](https://github.com/LLDIKTI16/simpeg/pull/21) OPEN `d323ca03` saat verifikasi 7 September, bukan bukti 31 AC baru selesai. Nomor #6/#7 backlog historis notifikasi bukan nomor aktif tersebut. Regression lintas modul memerlukan koordinasi terpisah, bukan pemindahan seluruh redesign ke owner SSO; nomor issue/owner/jadwal baru belum ditetapkan. Kewenangan mutasi matrix, anti-lockout dan bootstrap recovery tetap Open Product Decision.
