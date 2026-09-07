# Tracking Sprint 3 — Import & Pelengkap Data Pegawai

> **Authorization target — 7 September 2026:** [PATEN dan RBAC](../Keputusan-RBAC-Pemisahan-Capability-Paten-dan-Configurable-7-September-2026.md) menggantikan **hanya klausul authorization** lama yang menyamaratakan self sebagai permission checkbox, universal Super Admin bypass, actor allowlist Switch Role, manual/cancellation Admin-only, dan role guard/default export yang bertentangan. Klausul tersebut **Superseded**; tanggal, checklist, assignment dan evidence implementasi historis di bawah tetap merupakan snapshot saat dicatat. Domain/lifecycle, scope, privacy, state, ledger, append-only dan audit tetap berlaku. Target aktif serta kebutuhan evidence baru ada pada bagian akhir dokumen ini.

> **Pembaruan kanonis 25 Agustus 2026:** status ✅ soft delete/restore pada tracker ini adalah bukti historis kontrak lama dan berstatus **Superseded**. Ia tidak membuktikan lifecycle status terbaru selesai. Kontrak aktif dan gate baru berada pada [Keputusan Lifecycle dan Status Pegawai](../Keputusan-Lifecycle-Status-Pegawai-25-Agustus-2026.md) serta GitHub Issue #22.

| Field | Detail |
|---|---|
| Periode | 1 – 10 Juli 2026 |
| Cakupan issue | #20 – #25, #51 (`Issues-SIMPEG-Fase1.md`) |
| Pembaruan terakhir | 14 Agustus 2026 |
| Basis verifikasi | Branch `development` @ `ff0e9e1` setelah PR #182 merge; baseline historis verifikasi 26 Juli 2026 |
| Keputusan kanonis terkait | Import Fase 1 hanya template **Data Utama** (keputusan pengguna 22 Juli 2026): membuat record + snapshot saja, tanpa riwayat, tanpa kalkulasi TMT, tanggal pensiun dipertahankan apa adanya. Dikunci test regresi PR #121. |
| Menggantikan | `Analisis-Kesesuaian-Sprint-1-5.md` (dihapus 26 Juli 2026) |

Legend: ✅ selesai pada source · ⚠️ sebagian · ❌ belum selesai. Status source, bukan status tracker `Done`.

## Ringkasan

**Snapshot 14 Agustus: 7 ✅ · 0 ⚠️ · 0 ❌** pada level source untuk kontrak saat itu. Profil mandiri dan keluarga tetap tercatat selesai; klaim soft delete hanya historis/superseded. Gap manual column mapping dan warning pada #21 ditutup melalui **PR #183** yang telah merge ke `development`. Lifecycle baru tetap terbuka sampai seluruh AC 25 Agustus terbukti.

## Status per Issue

| Issue | Deliverable | Status | Bukti & catatan |
|---:|---|:---:|---|
| #20 | Download template import | ✅ | **Ditutup 26 Juli 2026 — PR #130, commit `db3c57b` (menunggu review/merge).** Template Data Utama kini 2 baris contoh: PNS lengkap + PPPK dengan Pangkat/Pensiun kosong (panduan kolom opsional non-PNS); kedua baris ber-marker sehingga tetap di-skip importer. Kontrak `example`→`examples` di action/writer/controller; 2 test pengunci bentuk lama diubah + assertion baru. Ketiadaan template multi-jenis tetap **sengaja tidak ada** (keputusan 22 Juli). |
| #21 | Upload, preview, validasi | ✅ | PR #183 (`4f3f2c3`, exact head `cbf907b`) menutup gap manual mapping: dropdown source→target/`Tidak dipakai`, state mapping batch sebagai sumber kebenaran, penyimpanan sebelum validasi, pencegahan target ganda dan missing required, warning header asing, klasifikasi canonical/ignored, pencocokan error eksak, serta normalisasi UI/backend. Source `Role` dijaga pada UI, Action, dan domain helper agar tidak dapat masuk ke field import. Review exact head menyatakan US-3.2 AC-4/AC-5 PASS dan CI hijau. |
| #22 | Eksekusi import & laporan hasil | ✅ | **Ditutup 26 Juli 2026 — PR #131, commit `e359248` (menunggu review/merge).** Tabel/model baru `import_batches` (id = batch id wizard, pemilik, counter, `row_issues` JSON, status, waktu; retensi permanen); eksekusi merekam batch saat mulai/sukses/gagal **sebelum** file sumber dibersihkan; endpoint `GET /pegawai/import/{batchId}/laporan` (gate role + kepemilikan) menghasilkan CSV ringkasan + rincian baris bermasalah dari database; tombol laporan wizard dialihkan ke server dan `downloadErrorReport()` browser dihapus. Test membuktikan laporan tetap bisa diunduh setelah `Cache::flush()`. Batasan Data Utama tetap dikunci test PR #121. |
| #23 | Profil sendiri read-only | ✅ | Ditutup PR #117: keluarga/pendidikan mandiri hanya GET ber-scope sesi; endpoint & UI mutasi dihapus; test mengunci scope + ketiadaan route mutasi. |
| #24 | CRUD data keluarga | ✅ | FormRequest, Action, soft delete, audit masking NIK keluarga, data scope, API v1, test lengkap. |
| #25 | Lifecycle pegawai | ⚠️ | **Bukti lama superseded:** soft delete, restore, daftar nonaktif, dan Data Backup bukan kontrak aktif. Perlu status-based lifecycle lengkap menurut keputusan 25 Agustus. |
| #51 | Reaktivasi berbasis permission | ⚠️ | Tidak ada hard delete tetap benar; reaktivasi dua role dengan effective `employees.restore`, scheduled transition, global blocking, dan concurrency/audit/notification gate belum dibuktikan oleh bukti lama. |

## Gap dan Tindak Lanjut

1. ~~**US-3.3 AC-5 / K-US-02:**~~ **Tertutup 14 Agustus 2026 — PR #182 (`ff0e9e1`).** Jalur skip untuk NIP yang sudah ada di database hidup dan terverifikasi browser (Playwright: 0 valid, 1 skip, 0 error; tombol import tidak dapat dijalankan untuk berkas tersebut). Batas K-US-02 terjaga: NIP ganda dalam satu berkas tetap error melalui koreksi retroaktif pada kemunculan pertama, email terdaftar tetap error, dan NIP yang menjadi terdaftar di antara validasi dan eksekusi dicatat sebagai skip. Lifecycle lock bersama kini melindungi aksi validasi, antrean, dan penyimpanan mapping dari pembacaan state parsial. Penyelesaian source sebelumnya melalui PR #172 (12 Agustus 2026) dipertahankan.
2. **QA browser:** Laravel Dusk regression untuk mapping sudah tersedia, tetapi belum menjadi quality gate CI dan bukti eksekusi manual penuh belum tercatat. Jalankan Dusk/manual browser regression beserta UAT formal sebelum release candidate.

Rambu: pertahankan batasan keputusan 22 Juli (jangan memulihkan template multi-jenis, jangan membuat riwayat/kalkulasi TMT dari import) — test regresi PR #121 wajib tetap hijau.

## Langkah Proses Tersisa (#20 & #22)

1. Review PR #130 & #131 (Adriel) dan QA/retest (Grantly) sesuai skenario di badan masing-masing PR.
2. Verifikasi PostgreSQL 17 khusus PR #131 (migration + JSON column; test lokal memakai SQLite).
3. Setelah merge, ubah catatan #20/#22 dari "menunggu review/merge" menjadi terkonfirmasi merged.

## Riwayat Perubahan Status

| Tanggal | Perubahan |
|---|---|
| 14 Agustus 2026 | Gap K-US-02 ditutup melalui **PR #182** (`ff0e9e1`): jalur SKIP NIP existing terverifikasi browser via Playwright, lifecycle lock bersama untuk aksi validasi/antrean/mapping, serta regression test kondisi balapan validasi→eksekusi. Melengkapi penyelesaian source PR #172. |
| 20 Juli 2026 | #23 naik ke ✅ (PR #117); #25 tuntas setelah penghapusan hard delete. |
| 22 Juli 2026 | Keputusan import Data Utama menjadi kanonis; temuan "template lanjutan/snapshot riwayat/TMT pasca-import" direklasifikasi **sengaja tidak ada**. PR #121 menambah test regresi batasnya. |
| 26 Juli 2026 (siang) | Verifikasi HEAD `1b2e5b6`: #20–#22 tidak berubah (tak tersentuh PR #122–#128). |
| 26 Juli 2026 (malam) | #20 ditutup via **PR #130** (`db3c57b`) dan #22 via **PR #131** (`e359248`) — keduanya menunggu review/QA. Bebas konflik terhadap development terbaru (termasuk PR #127) via simulasi merge; uji gabungan 38 test lulus. Ditemukan dead code jalur skip NIP duplikat (butuh keputusan kecil). Sisa gap sprint: #21. |
| 11 Agustus 2026 | #21 ditutup pada level source melalui **PR #183** (`4f3f2c3`, exact head `cbf907b`). US-3.2 AC-4/AC-5 dikonfirmasi PASS; enforcement source `Role` tersedia pada UI, backend, dan domain helper. Dusk/manual browser regression serta UAT formal tetap menjadi tindak lanjut QA. |


## Target delivery authorization — 7 September 2026

Sumber aktif: [keputusan PATEN dan RBAC](../Keputusan-RBAC-Pemisahan-Capability-Paten-dan-Configurable-7-September-2026.md) dan [User Stories v1.17](../PRD-DLL/User-Stories-SIMPEG-Fase1.md). **Status: target belum dibuktikan; bukan perubahan status checklist historis.**

Profil self PATEN, import dan mutasi data RBAC, lifecycle tetap; AC-RBAC-PATEN/CONFIG. Reaktivasi tetap invariant K-STATUS-04 effective SA/Admin + employees.restore.

- Matrix hanya **🔒 PATEN** dan **⚙️ RBAC**. PATEN ditentukan identity/ownership/assignment/lifecycle/domain; RBAC memakai effective permission matrix lalu canonical scope/privacy/domain. Super Admin tidak mempunyai universal bypass.
- Scope canonical: SA/Admin/Pimpinan global sesuai sensitivitas; Kepala Bagian bawahan langsung; Pegawai self. Filter/ID tidak membypass scope. Dokumen/SK termasuk milik sendiri tetap RBAC dan private-file authorization.
- Export default SA/Admin ON, Pimpinan/Kepala Bagian/Pegawai OFF; semua role dapat grant tanpa perubahan kode. Target Switch Role mengikuti hierarki asli SA → Admin → Pimpinan → Kepala Bagian → Pegawai, hanya ke role lebih rendah, persisten sampai revert.
- Manual/cancellation role-only lama **Superseded** oleh `cuti.manual.manage`/`cuti.cancellation.manage` + scope/domain. Ledger, replay, reservation hold/release/continue, state, lock/concurrency, audit/notifikasi tetap. Reaktivasi K-STATUS-04 tetap effective SA/Admin + `employees.restore`; invariant lifecycle tidak menjadi kategori matrix ketiga.
- Migrasi caller self dan katalog mengikuti §9 keputusan, menjaga grants/pivot existing; tidak otomatis reseed/delete atau mengklaim seluruh key target telah ada.
- Regression perlu grant/revoke lintas role termasuk SA OFF, scope/foreign ID, PATEN tanpa checkbox, lifecycle/ownership/eligibility, dokumen privat, append-only, manual/cancel state/concurrency dan seluruh switch/revert. PostgreSQL untuk DB-sensitive serta browser matrix/menu/direct URL/console; catat SHA/environment/expected/actual/audit tersanitasi.

**Koordinasi SSO:** Issue GitHub aktif [#6](https://github.com/LLDIKTI16/simpeg/issues/6) tetap core SSO (mapping/reuse/non-overwrite role/binding/concurrency/audit/claim-UAT), mengecualikan Switch Role aktif [#7](https://github.com/LLDIKTI16/simpeg/issues/7). PR [#21](https://github.com/LLDIKTI16/simpeg/pull/21) OPEN `d323ca03` saat verifikasi 7 September, bukan bukti 31 AC baru selesai. Nomor #6/#7 backlog historis notifikasi bukan nomor aktif tersebut. Regression lintas modul memerlukan koordinasi terpisah, bukan pemindahan seluruh redesign ke owner SSO; nomor issue/owner/jadwal baru belum ditetapkan. Kewenangan mutasi matrix, anti-lockout dan bootstrap recovery tetap Open Product Decision.
