# Tracking Role — SIMPEG Fase 1

> **Authorization target — 7 September 2026:** [PATEN dan RBAC](../Keputusan-RBAC-Pemisahan-Capability-Paten-dan-Configurable-7-September-2026.md) menggantikan **hanya klausul authorization** lama yang menyamaratakan self sebagai permission checkbox, universal Super Admin bypass, actor allowlist Switch Role, manual/cancellation Admin-only, dan role guard/default export yang bertentangan. Klausul tersebut **Superseded**; tanggal, checklist, assignment dan evidence implementasi historis di bawah tetap merupakan snapshot saat dicatat. Domain/lifecycle, scope, privacy, state, ledger, append-only dan audit tetap berlaku. Target aktif serta kebutuhan evidence baru ada pada bagian akhir dokumen ini.

Folder ini menampung tracking kesesuaian implementasi untuk **kelima role** SIMPEG terhadap PRD
v1.15, User Stories, dan Panduan Kode. Satu file per role, masing-masing berisi: apa yang **sudah
sesuai** (✅) dan apa yang **belum sesuai** (⚠️/❌) beserta bukti `file:line` dan rujukan task
tracker.

Folder ini menggantikan lima dokumen analisis role terpisah (audit 21–23 Juli 2026). Seluruh
temuan lama direkonsiliasi terakhir terhadap branch `development` @ `1fd99cb` pada 10 Agustus
2026. File role masih mempertahankan tabel audit Juli sebagai kronologi; bagian “Rekonsiliasi
Temuan” pada tiap file menjadi status aktif bila ada pernyataan lama yang bertentangan.

> **Addendum evaluasi 31 Agustus–1 September 2026:** status ikon di bawah adalah bukti implementasi sebelum keputusan terbaru. Kesesuaian baru untuk Atasan Langsung, dua tindakan saat Atasan/PYBMC orang yang sama, permohonan pembatalan dan revisi, penangguhan final, cuti historis, matriks SK PNS/CPNS, dan Reporting Statistik belum boleh dianggap lulus tanpa evidence baru. Lihat [keputusan 31 Agustus–1 September](../Keputusan-Evaluasi-Meeting-LLDIKTI-31-Agustus-2026.md).

> **Addendum RBAC 2 September 2026:** status role lama hanya menunjukkan konfigurasi default/evidence historis. Permission matrix database kini menjadi sumber kebenaran akses fitur. Kesesuaian baru harus membuktikan grant/revoke permission lintas role, scope/masking, `employees.export`, `dokumen_sk.read`, serta invariant Switch Role untuk Super Admin/Admin Kepegawaian. Lihat [keputusan RBAC](../Keputusan-RBAC-dan-Switch-Role-2-September-2026.md).

## Ringkasan Lintas Role

| Role | File | Status | Sorotan |
|---|---|:---:|---|
| Super Admin | [Role-Super-Admin.md](Role-Super-Admin.md) | ⚠️ | Data Master, Hari Libur, dashboard, laporan, masking, immutability, dan audit server-side sudah ditutup. Sisa utama: Pengaturan Sistem, beberapa gap RBAC/integrasi, dan hardening fail-closed menyeluruh |
| Admin Kepegawaian | [Role-Admin-Kepegawaian.md](Role-Admin-Kepegawaian.md) | ⚠️ | Dashboard/laporan/audit utama sudah ditutup; sisa: navigasi lifecycle pegawai, konsistensi tombol vs permission, batas kelola dokumen, dan hardening fail-closed |
| Pimpinan | [Role-Pimpinan.md](Role-Pimpinan.md) | ⚠️→✅ | Read-only UI, laporan, dashboard, dan tren W7 sudah tersedia; sisa: keputusan produk link audit W6 dan verifikasi akhir lintas-role |
| Kepala Bagian | [Role-Kepala-Bagian.md](Role-Kepala-Bagian.md) | ✅ | Paling sesuai; sisa: bersih-bersih kode Dinas Luar (keputusan K-2) dan paginasi EWS |
| Pegawai | [Role-Pegawai.md](Role-Pegawai.md) | ⚠️ | Widget notifikasi dan validasi lintas tahun sudah ditutup; sisa utama dua halaman fungsional yang belum memiliki tautan navigasi |

## Temuan Lintas Role (berlaku untuk lebih dari satu role)

| Temuan | Role terdampak | Rujukan |
|---|---|---|
| Hardening audit fail-closed belum menyeluruh pada CRUD pegawai/import; masking, immutability, dan audit server-side sudah ditutup PR #174 | Super Admin, Admin | Sprint 7 (7.2-9) |
| L3 belum tersedia untuk Admin dan beberapa gap lifecycle/navigasi masih terbuka; export custom/PDF utama sudah ditutup PR #154/#162/#167 | Super Admin, Admin | Backlog role Admin |
| Label `Perlu Perubahan` (istilah resmi: `Perubahan`) di view cuti bersama | Pimpinan, Admin, Pegawai | Task #25 |
| Form ubah password lokal tidak sinkron dengan SSO Keycloak | Semua role | Keputusan produk |

## Cara Memakai

- Status diperbarui setiap kali PR yang menyentuh role terkait di-merge ke `development` — catat
  nomor PR pada baris temuan yang tertutup, pindahkan barisnya ke tabel ✅.
- Temuan baru dari QA/review dimasukkan ke tabel "Belum Sesuai" file role terkait, dengan bukti
  `file:line` dan prioritas.
- Rujukan silang: tracking pekerjaan per sprint ada di folder `../Tracking-Sprint-1-6/`
  (Sprint 1–7); daftar issue resmi di `../Issues-SIMPEG-Fase1.md`; keputusan produk terbaru di
  `../Kickoff-Sprint-6-Kontrak-dan-Keputusan.md`.

## Dokumen Asal yang Dikonsolidasi

| Dokumen lama (dihapus dari folder DOCUMENT) | Menjadi |
|---|---|
| `Analisis-Frontend-Backend-Role-Super-Admin.md` (21 Juli) | Role-Super-Admin.md |
| `Analisis-Kesesuaian-Administrasi-Sistem-Super-Admin.md` (23 Juli) | Role-Super-Admin.md |
| `Analisis-Frontend-Backend-Role-Admin-Kepegawaian.md` (21 Juli) | Role-Admin-Kepegawaian.md |
| `Analisis-Frontend-Role-Pimpinan.md` (21 Juli) | Role-Pimpinan.md |
| `Analisis-Frontend-Role-Kepala-Bagian.md` (21 Juli) | Role-Kepala-Bagian.md |
| `Halaman-dan-Hak-Akses-Role-Pegawai.md` (22 Juli, dokumen target produk) | Role-Pegawai.md |

`Bukti-QA-Kelola-Akses-User-Super-Admin.md` dan `Rencana-Eksekusi-Kelola-Akses-User-Super-Admin.md`
tetap di folder `DOCUMENT` sebagai arsip bukti QA dan rencana eksekusi (bukan dokumen analisis role).


## Target delivery authorization — 7 September 2026

Sumber aktif: [keputusan PATEN dan RBAC](../Keputusan-RBAC-Pemisahan-Capability-Paten-dan-Configurable-7-September-2026.md) dan [User Stories v1.17](../PRD-DLL/User-Stories-SIMPEG-Fase1.md). **Status: target belum dibuktikan; bukan perubahan status checklist historis.**

Koordinasikan seluruh 31 AC pada User Stories v1.17/§10 keputusan; ownership fitur existing tetap. Pisahkan requirement target dari bukti implementasi dan release gate.

- Matrix hanya **🔒 PATEN** dan **⚙️ RBAC**. PATEN ditentukan identity/ownership/assignment/lifecycle/domain; RBAC memakai effective permission matrix lalu canonical scope/privacy/domain. Super Admin tidak mempunyai universal bypass.
- Scope canonical: SA/Admin/Pimpinan global sesuai sensitivitas; Kepala Bagian bawahan langsung; Pegawai self. Filter/ID tidak membypass scope. Dokumen/SK termasuk milik sendiri tetap RBAC dan private-file authorization.
- Export default SA/Admin ON, Pimpinan/Kepala Bagian/Pegawai OFF; semua role dapat grant tanpa perubahan kode. Target Switch Role mengikuti hierarki asli SA → Admin → Pimpinan → Kepala Bagian → Pegawai, hanya ke role lebih rendah, persisten sampai revert.
- Manual/cancellation role-only lama **Superseded** oleh `cuti.manual.manage`/`cuti.cancellation.manage` + scope/domain. Ledger, replay, reservation hold/release/continue, state, lock/concurrency, audit/notifikasi tetap. Reaktivasi K-STATUS-04 tetap effective SA/Admin + `employees.restore`; invariant lifecycle tidak menjadi kategori matrix ketiga.
- Migrasi caller self dan katalog mengikuti §9 keputusan, menjaga grants/pivot existing; tidak otomatis reseed/delete atau mengklaim seluruh key target telah ada.
- Regression perlu grant/revoke lintas role termasuk SA OFF, scope/foreign ID, PATEN tanpa checkbox, lifecycle/ownership/eligibility, dokumen privat, append-only, manual/cancel state/concurrency dan seluruh switch/revert. PostgreSQL untuk DB-sensitive serta browser matrix/menu/direct URL/console; catat SHA/environment/expected/actual/audit tersanitasi.

**Koordinasi SSO:** Issue GitHub aktif [#6](https://github.com/LLDIKTI16/simpeg/issues/6) tetap core SSO (mapping/reuse/non-overwrite role/binding/concurrency/audit/claim-UAT), mengecualikan Switch Role aktif [#7](https://github.com/LLDIKTI16/simpeg/issues/7). PR [#21](https://github.com/LLDIKTI16/simpeg/pull/21) OPEN `d323ca03` saat verifikasi 7 September, bukan bukti 31 AC baru selesai. Nomor #6/#7 backlog historis notifikasi bukan nomor aktif tersebut. Regression lintas modul memerlukan koordinasi terpisah, bukan pemindahan seluruh redesign ke owner SSO; nomor issue/owner/jadwal baru belum ditetapkan. Kewenangan mutasi matrix, anti-lockout dan bootstrap recovery tetap Open Product Decision.
