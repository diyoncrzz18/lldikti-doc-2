# Tracking Sprint 2 — Data Pegawai Core

> **Authorization target — 7 September 2026:** [PATEN dan RBAC](../Keputusan-RBAC-Pemisahan-Capability-Paten-dan-Configurable-7-September-2026.md) menggantikan **hanya klausul authorization** lama yang menyamaratakan self sebagai permission checkbox, universal Super Admin bypass, actor allowlist Switch Role, manual/cancellation Admin-only, dan role guard/default export yang bertentangan. Klausul tersebut **Superseded**; tanggal, checklist, assignment dan evidence implementasi historis di bawah tetap merupakan snapshot saat dicatat. Domain/lifecycle, scope, privacy, state, ledger, append-only dan audit tetap berlaku. Target aktif serta kebutuhan evidence baru ada pada bagian akhir dokumen ini.

| Field | Detail |
|---|---|
| Periode | 21 – 30 Juni 2026 |
| Cakupan issue | #13 – #19 (`Issues-SIMPEG-Fase1.md`) |
| Pembaruan terakhir | 11 Agustus 2026 |
| Basis verifikasi | Branch `development` @ `71d2dae` setelah PR #180 merge; baseline append-only historis PR #129 |
| Menggantikan | `Analisis-Kesesuaian-Sprint-1-5.md` (dihapus 26 Juli 2026) |

Legend: ✅ selesai pada source · ⚠️ sebagian · ❌ belum selesai. Status source, bukan status tracker `Done`.

## Ringkasan

**7 ✅ · 0 ⚠️ · 0 ❌** — Sprint 2 tuntas pada level source. Baseline append-only riwayat diselesaikan melalui PR #129, sedangkan gap UI BUG-01 yang ditemukan kemudian ditutup oleh **PR #180** dan telah merge ke `development`. Full browser/E2E submit multipart tetap dicatat sebagai tindak lanjut QA non-blocking, bukan gap requirement pada source.

## Status per Issue

| Issue | Deliverable | Status | Bukti & catatan |
|---:|---|:---:|---|
| #13 | Migration tabel utama pegawai | ✅ | Model/relasi, UUID, index, cast enkripsi (`nik`, `no_kk`), migration sinkron PRD. |
| #14 | Form tambah pegawai multi-tab | ✅ | `StoreEmployeeRequest`, `CreateEmployeeAction`, view multi-tab, validasi upload, storage, audit, test. |
| #15 | Form edit pegawai | ✅ | FormRequest/Action, penggantian berkas/foto, audit, test. (Catatan lintas-sprint: payload audit `toArray()` membawa risiko NIK/No. KK plaintext — ditangani sebagai gap Issue #5 Sprint 1, bukan gap issue ini.) |
| #16 | Halaman daftar pegawai | ✅ | Search, filter, sort, pagination, eager loading, default aktif, RBAC, test. Status kelengkapan dokumen kini 4-nilai (`kosong/tersedia/tidak_lengkap/lengkap`) + 8 test tambahan. |
| #17 | Halaman detail pegawai bertab | ✅ | Data relasi lengkap, tab, informasi kalkulasi EWS, dan test detail tersedia. BUG-01 terkait kontrol tambah riwayat ditutup PR #180 (`71d2dae`): ketiga tab riwayat memiliki tombol tambah yang digate permission `employee_histories.create`, modal menyediakan Upload SK, dan tanggal riwayat Jabatan diformat untuk tampilan. |
| #18 | Riwayat pangkat/jabatan/KGB append-only | ✅ | Baseline append-only ditutup PR #129 (`2e58c8c`): request menolak id riwayat lama, Action selalu membuat record baru, dan form edit tidak memutasi data substantif riwayat existing. Sesuai keputusan produk 21 Agustus 2026, penggantian berkas SK saja diperbolehkan selama tidak mengubah data substantif, `is_latest`, atau dasar kalkulasi serta tetap tervalidasi dan teraudit. PR #180 (`71d2dae`, exact head `9c1c1e9`) menutup gap UI dengan kontrol tambah Kepangkatan/Jabatan/KGB, multipart Upload SK, dan integrasi ke backend existing yang mempertahankan `is_latest`, kalkulasi TMT, audit CREATE, serta dokumen SK. Review exact head menyatakan US-2.4 AC-2 dan US-2.6 AC-1 sampai AC-5 PASS. |
| #19 | Riwayat hukuman disiplin | ✅ | Ditutup PR #117 (`32ada6b`): route DELETE/action/permission/tombol hapus dihilangkan; `DeleteDocumentAction` menolak dokumen yang dipakai riwayat disiplin; test mengunci route lama 404/405 + record tetap tersimpan. |

## Gap Terbuka

Tidak ada gap requirement yang teridentifikasi pada source Sprint 2 setelah PR #180 merge. Tindak lanjut proses yang masih perlu dijaga:

1. Tambahkan regression browser/E2E untuk alur lengkap `buka modal → pilih file SK → submit multipart → riwayat tersimpan → dokumen SK terbentuk → baris baru tampil`.
2. Jalankan regression/UAT formal Sprint 7 terhadap penambahan riwayat, `is_latest`, kalkulasi TMT, audit, akses permission, dan keterhubungan dokumen SK.
3. Pertahankan verifikasi PostgreSQL 17 untuk transaksi, UUID, relasi dokumen, dan audit sebelum release candidate.

Keputusan produk terkait (bila dibutuhkan kelak): mekanisme "koreksi resmi" riwayat (edit ber-alasan + audit) adalah perubahan PRD dan harus diputuskan eksplisit — cara koreksi saat ini adalah menambah record baru yang benar.

## Riwayat Perubahan Status

| Tanggal | Perubahan |
|---|---|
| 20 Juli 2026 | #19 naik ke ✅ (PR #117). |
| 22 Juli 2026 | Baseline audit: #13–#17, #19 ✅; #18 ⚠️ (append-only tidak absolut). |
| 26 Juli 2026 | #18 ditutup (commit `2e58c8c`) dan diajukan sebagai **PR #129** ke `development` — Sprint 2 tuntas di level source, menunggu review/QA. |
| 11 Agustus 2026 | BUG-01 ditutup melalui **PR #180** (`71d2dae`): kontrol tambah riwayat, Upload SK, multipart submission, label baris baru, dan format tanggal Jabatan masuk ke `development`. US-2.4 AC-2 serta US-2.6 AC-1 sampai AC-5 dikonfirmasi PASS pada source; full E2E submit dicatat sebagai follow-up QA non-blocking. |


## Target delivery authorization — 7 September 2026

Sumber aktif: [keputusan PATEN dan RBAC](../Keputusan-RBAC-Pemisahan-Capability-Paten-dan-Configurable-7-September-2026.md) dan [User Stories v1.17](../PRD-DLL/User-Stories-SIMPEG-Fase1.md). **Status: target belum dibuktikan; bukan perubahan status checklist historis.**

Profil/riwayat/keluarga self PATEN, lintas pegawai dan dokumen/SK RBAC; AC-RBAC-PATEN, AC-DOC, AC-RBAC-CONFIG. Riwayat substantif tetap append-only.

- Matrix hanya **🔒 PATEN** dan **⚙️ RBAC**. PATEN ditentukan identity/ownership/assignment/lifecycle/domain; RBAC memakai effective permission matrix lalu canonical scope/privacy/domain. Super Admin tidak mempunyai universal bypass.
- Scope canonical: SA/Admin/Pimpinan global sesuai sensitivitas; Kepala Bagian bawahan langsung; Pegawai self. Filter/ID tidak membypass scope. Dokumen/SK termasuk milik sendiri tetap RBAC dan private-file authorization.
- Export default SA/Admin ON, Pimpinan/Kepala Bagian/Pegawai OFF; semua role dapat grant tanpa perubahan kode. Target Switch Role mengikuti hierarki asli SA → Admin → Pimpinan → Kepala Bagian → Pegawai, hanya ke role lebih rendah, persisten sampai revert.
- Manual/cancellation role-only lama **Superseded** oleh `cuti.manual.manage`/`cuti.cancellation.manage` + scope/domain. Ledger, replay, reservation hold/release/continue, state, lock/concurrency, audit/notifikasi tetap. Reaktivasi K-STATUS-04 tetap effective SA/Admin + `employees.restore`; invariant lifecycle tidak menjadi kategori matrix ketiga.
- Migrasi caller self dan katalog mengikuti §9 keputusan, menjaga grants/pivot existing; tidak otomatis reseed/delete atau mengklaim seluruh key target telah ada.
- Regression perlu grant/revoke lintas role termasuk SA OFF, scope/foreign ID, PATEN tanpa checkbox, lifecycle/ownership/eligibility, dokumen privat, append-only, manual/cancel state/concurrency dan seluruh switch/revert. PostgreSQL untuk DB-sensitive serta browser matrix/menu/direct URL/console; catat SHA/environment/expected/actual/audit tersanitasi.

**Koordinasi SSO:** Issue GitHub aktif [#6](https://github.com/LLDIKTI16/simpeg/issues/6) tetap core SSO (mapping/reuse/non-overwrite role/binding/concurrency/audit/claim-UAT), mengecualikan Switch Role aktif [#7](https://github.com/LLDIKTI16/simpeg/issues/7). PR [#21](https://github.com/LLDIKTI16/simpeg/pull/21) OPEN `d323ca03` saat verifikasi 7 September, bukan bukti 31 AC baru selesai. Nomor #6/#7 backlog historis notifikasi bukan nomor aktif tersebut. Regression lintas modul memerlukan koordinasi terpisah, bukan pemindahan seluruh redesign ke owner SSO; nomor issue/owner/jadwal baru belum ditetapkan. Kewenangan mutasi matrix, anti-lockout dan bootstrap recovery tetap Open Product Decision.
