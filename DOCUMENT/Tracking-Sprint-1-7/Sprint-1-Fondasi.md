# Tracking Sprint 1 — Fondasi

> **Authorization target — 7 September 2026:** [PATEN dan RBAC](../Keputusan-RBAC-Pemisahan-Capability-Paten-dan-Configurable-7-September-2026.md) menggantikan **hanya klausul authorization** lama yang menyamaratakan self sebagai permission checkbox, universal Super Admin bypass, actor allowlist Switch Role, manual/cancellation Admin-only, dan role guard/default export yang bertentangan. Klausul tersebut **Superseded**; tanggal, checklist, assignment dan evidence implementasi historis di bawah tetap merupakan snapshot saat dicatat. Domain/lifecycle, scope, privacy, state, ledger, append-only dan audit tetap berlaku. Target aktif serta kebutuhan evidence baru ada pada bagian akhir dokumen ini.

> **Addendum RBAC 2 September 2026:** status Sprint 1 adalah snapshot implementasi historis. Kontrak aktif menuntut permission matrix configurable sebagai sumber kebenaran, larangan allowlist role-permission, permission export/dokumen yang granular, dan invariant Switch Role baru. Tindak lanjut dilacak pada Addendum 2 September di `Issues-SIMPEG-Fase1.md` serta UAT K-01.

| Field | Detail |
|---|---|
| Periode | 8 – 20 Juni 2026 |
| Cakupan issue | #1 – #12 (`Issues-SIMPEG-Fase1.md`) |
| Pembaruan terakhir | 10 Agustus 2026 |
| Basis verifikasi | Branch `development` @ `54ab90d` setelah PR #176 |
| Menggantikan | `Analisis-Kesesuaian-Sprint-1-5.md` (dokumen monolitik lama, dihapus 26 Juli 2026) |

Legend: ✅ selesai pada source · ⚠️ sebagian (ada gap requirement/kualitas) · ❌ belum selesai/tidak sesuai. Ikon menyatakan status source; status tracker `Done` tetap membutuhkan review PR, QA/retest, dan evidence.

## Ringkasan

**7 ✅ · 5 ⚠️ · 0 ❌.** Fondasi (auth, notifikasi, design system, reference tables, testing framework) berdiri. Masking NIK/No. KK dan immutability audit telah ditutup PR #174. Issue #5 tetap ⚠️ hanya karena perluasan kebijakan audit fail-closed untuk CRUD pegawai/import belum selesai menyeluruh.

### Rekonsiliasi issue #5 — 10 Agustus 2026

- ✅ PR #174 (`037e137`) menyelesaikan masking NIK/No. KK pada tulis dan baca audit serta menegakkan immutability melalui guard model dan trigger PostgreSQL.
- ⚠️ PR #176 (`54ab90d`) menyelesaikan event wajib US-7.1 AC-1 dan memperkeras mutasi yang disentuh, tetapi belum menutup seluruh CRUD pegawai/import maupun dokumentasi kebijakan dan regression test rollback.
- Baris status issue di bawah dipertahankan sebagai kronologi audit sebelum PR #174/#176; rekonsiliasi ini yang berlaku untuk status terkini.

## Arsip Status per Issue — snapshot sebelum PR #174/#176

| Issue | Deliverable | Status | Bukti & catatan |
|---:|---|:---:|---|
| #1 | Setup Laravel & environment | ⚠️ | Laravel 12, PostgreSQL 17, queue, compose, Pint, PHPStan, helper Podman tersedia. Sisa: PHP lokal 8.3 vs CI 8.4, evidence deployment Podman production belum ada. |
| #2 | Keycloak SSO & middleware | ⚠️ | Controller/Action callback-logout-redirect, middleware, config Socialite, test tersedia. Sisa: login IdP nyata belum diuji (credential belum diterima); keputusan bootstrap first-mapped employee perlu didokumentasikan. |
| #3 | Logout & session management | ⚠️ | Logout POST + invalidasi session + audit tersedia. **Gap terverifikasi:** route GET `/logout` (`routes/web.php:54-55`) tetap memutasi session tanpa CSRF — hapus route GET atau jadikan halaman konfirmasi POST. |
| #4 | Mapping user Keycloak & RBAC | ✅ | Ditutup commit #109; diperkuat besar-besaran PR #126 (`users.employee_id` canonical, strict audit rollback, uniqueness PostgreSQL `23505`). QA UA-40…47 lulus (`Bukti-QA-Kelola-Akses-User-Super-Admin.md`). |
| #5 | Audit log | ⚠️ | Migration, model, `AuditService`, audit auth & mutasi tersedia. **Gap terverifikasi (P0):** (a) NIK/No. KK bisa tersimpan plaintext — `UpdateEmployeeAction` memakai `toArray()` untuk old/new values, cast `encrypted` terdekripsi saat serialisasi, tanpa test masking; (b) model `AuditLog` tanpa guard `updating`/`deleting`; (c) `AuditService::log()` fail-open (varian strict `logOrFail()` baru ada sejak PR #124 dan baru dipakai 3 dari 36 call-site). |
| #6 | Notifikasi in-app backend | ✅ | Migration/model, service, action inbox/read/unread, controller API, test tersedia. |
| #7 | Bell icon notifikasi | ✅ | Komponen bell, endpoint, dan JavaScript aplikasi tersedia. |
| #8 | Design system & layout master | ✅ | Layout, komponen UI/form reusable, Tailwind/Vite, UI Bahasa Indonesia. |
| #9 | Reusable Blade components | ⚠️ | Komponen utama tersedia. **Gap terverifikasi:** `resources/views/components/README.md` tidak ada; `design-system.md:984-1000` stale (mendokumentasikan struktur folder yang tidak ada). |
| #10 | CRUD Hari Libur & cuti bersama | ✅ | API v1 + Action + FormRequest + audit + `HariLiburCrudTest` sudah benar. Ditutup PR #166 (`9be633d`): controller web menjadi adapter HTTP tipis, data statis dan audit session `dynamic_audit_logs` dihapus, mutasi web memakai FormRequest + Action DB dengan audit resmi, serta filter/pencarian/paginasi dijalankan di database. Evidence: `HariLiburWebPageTest` (23 test) termasuk regresi dampak pada kalkulasi hari kerja cuti, regresi PostgreSQL 17, dan smoke test browser Super Admin 7 Agustus 2026. |
| #11 | Migration/seeder reference tables | ✅ | PR #118: hierarchy `ref_unit_kerja`, lifecycle jabatan (`default_bup`, `is_active`), katalog 10 status pegawai, `ref_notification_channels`; seeder idempoten + test. |
| #12 | Setup testing framework | ✅ | PHPUnit + Dusk, smoke test browser, helper, `phpunit.dusk.xml`, dokumentasi; evidence PostgreSQL 17 dari test fokus + CI. |

## Gap Terbuka (urutan prioritas)

1. **P1 — Logout GET tanpa CSRF** (#3).
2. **P1 — Perluas audit fail-closed** (#5): tetapkan daftar mutation wajib `logOrFail()` untuk sisa CRUD pegawai/import, dokumentasikan kebijakan, dan tambah regression test rollback.
3. **P2 — README komponen** (#9) dan perapian `design-system.md`.
4. **Proses** — samakan PHP lokal/CI, uji login IdP nyata saat credential diterima, evidence Podman production.

## Riwayat Perubahan Status

| Tanggal | Perubahan |
|---|---|
| 10 Agustus 2026 | PR #174 menutup masking identitas dan immutability audit. PR #176 menutup event wajib US-7.1 AC-1 serta memperluas strict audit secara parsial. Issue #5 tetap ⚠️ hanya untuk hardening fail-closed CRUD pegawai/import dan kebijakan/test rollback. |
| 22 Juli 2026 | Baseline audit (HEAD `9a27caa`): #4/#6/#7/#8/#11/#12 ✅, sisanya ⚠️. |
| 23–26 Juli 2026 | #4 diperkuat PR #126 + QA lulus penuh. `logOrFail()` (audit strict) tersedia sejak PR #124 — #5 tetap ⚠️ karena adopsi masih sempit dan masking NIK/No. KK belum ada. Verifikasi 26 Juli mengonfirmasi #3, #9, #10 belum berubah. |
| 7 Agustus 2026 | #10 ditutup PR #166 (`9be633d`): halaman web Hari Libur memakai `ref_hari_libur` dengan audit resmi dan query sisi server. Evidence test otomatis, regresi PostgreSQL 17, dan smoke test browser tersedia sehingga status naik menjadi ✅. Ringkasan sprint menjadi 7 ✅ · 5 ⚠️ · 0 ❌. |


## Target delivery authorization — 7 September 2026

Sumber aktif: [keputusan PATEN dan RBAC](../Keputusan-RBAC-Pemisahan-Capability-Paten-dan-Configurable-7-September-2026.md) dan [User Stories v1.17](../PRD-DLL/User-Stories-SIMPEG-Fase1.md). **Status: target belum dibuktikan; bukan perubahan status checklist historis.**

Auth/matrix, self notifications, hari libur dan Switch Role; AC-RBAC-PATEN, AC-RBAC-CONFIG, AC-SWITCH.

- Matrix hanya **🔒 PATEN** dan **⚙️ RBAC**. PATEN ditentukan identity/ownership/assignment/lifecycle/domain; RBAC memakai effective permission matrix lalu canonical scope/privacy/domain. Super Admin tidak mempunyai universal bypass.
- Scope canonical: SA/Admin/Pimpinan global sesuai sensitivitas; Kepala Bagian bawahan langsung; Pegawai self. Filter/ID tidak membypass scope. Dokumen/SK termasuk milik sendiri tetap RBAC dan private-file authorization.
- Export default SA/Admin ON, Pimpinan/Kepala Bagian/Pegawai OFF; semua role dapat grant tanpa perubahan kode. Target Switch Role mengikuti hierarki asli SA → Admin → Pimpinan → Kepala Bagian → Pegawai, hanya ke role lebih rendah, persisten sampai revert.
- Manual/cancellation role-only lama **Superseded** oleh `cuti.manual.manage`/`cuti.cancellation.manage` + scope/domain. Ledger, replay, reservation hold/release/continue, state, lock/concurrency, audit/notifikasi tetap. Reaktivasi K-STATUS-04 tetap effective SA/Admin + `employees.restore`; invariant lifecycle tidak menjadi kategori matrix ketiga.
- Migrasi caller self dan katalog mengikuti §9 keputusan, menjaga grants/pivot existing; tidak otomatis reseed/delete atau mengklaim seluruh key target telah ada.
- Regression perlu grant/revoke lintas role termasuk SA OFF, scope/foreign ID, PATEN tanpa checkbox, lifecycle/ownership/eligibility, dokumen privat, append-only, manual/cancel state/concurrency dan seluruh switch/revert. PostgreSQL untuk DB-sensitive serta browser matrix/menu/direct URL/console; catat SHA/environment/expected/actual/audit tersanitasi.

**Koordinasi SSO:** Issue GitHub aktif [#6](https://github.com/LLDIKTI16/simpeg/issues/6) tetap core SSO (mapping/reuse/non-overwrite role/binding/concurrency/audit/claim-UAT), mengecualikan Switch Role aktif [#7](https://github.com/LLDIKTI16/simpeg/issues/7). PR [#21](https://github.com/LLDIKTI16/simpeg/pull/21) OPEN `d323ca03` saat verifikasi 7 September, bukan bukti 31 AC baru selesai. Nomor #6/#7 backlog historis notifikasi bukan nomor aktif tersebut. Regression lintas modul memerlukan koordinasi terpisah, bukan pemindahan seluruh redesign ke owner SSO; nomor issue/owner/jadwal baru belum ditetapkan. Kewenangan mutasi matrix, anti-lockout dan bootstrap recovery tetap Open Product Decision.
