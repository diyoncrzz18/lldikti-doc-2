# Keputusan Produk — Pemisahan Capability PATEN dan RBAC

| Field | Detail |
|---|---|
| Tanggal keputusan | **7 September 2026** |
| Status | **Disetujui pengguna — kontrak target Fase 1**, bukan bukti implementasi atau penerimaan UAT |
| Dasar | Keputusan eksplisit pengguna setelah review [PR #21](https://github.com/LLDIKTI16/simpeg/pull/21) |
| Kedudukan | Addendum yang menggantikan klausul bertentangan secara terbatas; keputusan dan bukti historis tetap disimpan |
| Dokumen terkait | [Keputusan RBAC 2 September](Keputusan-RBAC-dan-Switch-Role-2-September-2026.md), [PRD](PRD-DLL/PRD-SIMPEG-Fase1-Core.md), [User Stories](PRD-DLL/User-Stories-SIMPEG-Fase1.md), [Issues](PRD-DLL/Issues-SIMPEG-Fase1.md), [Panduan Kode](PRD-DLL/Panduan-Penulisan-Kode-SIMPEG.md) |

## 1. Hierarki keputusan dan batas perubahan

Urutan sumber adalah keputusan stakeholder/addendum terbaru yang disetujui → PRD Core → User Stories/acceptance criteria → dekomposisi Issues → panduan kode → tracker dan evidence historis. Addendum ini menjadi authority terbaru hanya untuk klasifikasi capability, authorization RBAC, default export, dan Switch Role yang diatur di bawah.

Ini adalah perubahan dokumentasi. Keberadaan addendum tidak membuktikan bahwa kode, migration, permission database, UI matrix, ataupun pengujian telah mengikuti target. Scope SSO pada Issue #6 tidak berubah menjadi seluruh redesign RBAC. Identitas Keycloak, binding user–employee, dan inisialisasi role internal tetap mengikuti kontrak SSO; claim tidak memberikan elevated role atau melewati authorization.

## 2. Dua kategori capability

Klasifikasi produk dan UI hanya **🔒 PATEN** dan **⚙️ RBAC**. Tidak ada kategori UI ketiga. Pemeriksaan scope, ownership, masking, workflow, assignment, lifecycle, dan domain invariant adalah lapisan authorization yang tetap berlaku, bukan kategori matrix tambahan.

- **PATEN:** capability melekat pada identitas, ownership, self-service dasar, assignment workflow, lifecycle, data scope, atau aturan perhitungan/domain. Tidak memerlukan checkbox Role & Permission dan tidak dapat dicabut hanya dengan mengubah matrix role. PATEN tidak menghapus autentikasi, binding, atau kelayakan domain.
- **RBAC:** capability administratif/delegatif yang dapat diberikan atau dicabut melalui database permission matrix. Lolos permission berarti boleh menggunakan capability; bukan izin untuk semua data atau semua mutasi.

Alur PATEN: authenticated user → identity/employee binding yang diperlukan → ownership/assignment/workflow/lifecycle/domain eligibility → capability yang diizinkan. Inbox tetap dimiliki user; kalender global tidak menciptakan syarat binding Employee baru. Blokir lifecycle akun yang berlaku tidak boleh dilewati oleh kedua capability tersebut.

## 3. Matrix PATEN

| Capability | Key teknis existing terkait | Authority target dan batas |
|---|---|---|
| Lihat profil sendiri | `employees.read_self` | User linked Employee dan lifecycle valid; hanya profil sendiri |
| Baca riwayat sendiri | Konteks self pada `employee_histories.read` | Ownership Employee; permission tersebut hanya untuk cross-employee pada target |
| Baca keluarga sendiri | Konteks self pada `employee_families.read` | Ownership Employee; tidak memberi self-edit atau akses keluarga orang lain |
| Baca notifikasi sendiri | `notifications.read` | Ownership user penerima; tidak membuka inbox user lain |
| Tandai notifikasi sendiri dibaca | `notifications.update` | Ownership user penerima; hanya operasi status baca yang sah |
| Lihat hari libur | `hari_libur.read` | Kalender global bagi authenticated user sesuai lifecycle; mutasi tetap RBAC |
| Ajukan cuti sendiri | `cuti.create` | Employee linked/aktif, jenis pegawai, masa kerja, eligibility jenis cuti, saldo jika berlaku, chain siap, tanggal/durasi, overlap, dan aturan cuti kanonis |
| Lihat cuti sendiri | `cuti.read_own` | Owner Employee pengajuan adalah Employee aktor |
| Lihat saldo cuti sendiri | Konteks self pada `cuti.balance.read` | Ownership dan kalkulasi domain; tanpa override saldo |
| Bertindak pada approval cuti yang ditugaskan | `cuti.approve` dan key stage historis | Aktor ditugaskan pada active approval step dan workflow memungkinkan tindakan; tidak mengizinkan request lain |
| Generate bukti/formulir otomatis | `cuti.proof.generate` untuk proses otomatis | Aksi sistem/domain dalam final approval yang sah; berbeda dari manual regenerate |

Hak pemohon mengajukan permohonan pembatalan atau revisi miliknya mengikuti ownership dan state cuti yang telah disetujui, bukan checkbox `cuti.create`. Keputusan atas permohonan pembatalan tetap capability RBAC yang berbeda. PATEN pengajuan tidak berarti semua role atau semua Employee otomatis eligible, termasuk ketentuan cuti Kepala Lembaga dan jenis pegawai yang telah diatur.

Self-service PATEN di sini hanya kemampuan yang tercantum. Ia tidak otomatis memberi hak mengedit profil/riwayat/keluarga sendiri, mengunggah dokumen sendiri, atau bypass `dokumen_sk.*`. Capability mutasi RBAC, bila diberikan, tetap harus melewati scope dan batas domain Fase 1 yang relevan.

## 4. Matrix RBAC target

Semua key di bawah adalah **⚙️ RBAC**, tersedia untuk konfigurasi seluruh role. Domain immutable/append-only tetap dapat menolak operasi meskipun key update/delete diberikan. Tidak ada default ON baru yang diasumsikan hanya karena permission tercantum pada tabel.

| Kelompok | Permission target | Konteks dan batas | Default yang disahkan di addendum ini |
|---|---|---|---|
| Pegawai | `employees.read`, `employees.create`, `employees.update`, `employees.import`, `employees.deactivate` | Cross-employee/administrasi sesuai canonical scope; tidak ada hard delete Employee | Tidak menetapkan default baru |
| Reaktivasi | `employees.restore` | **Aktifkan kembali Pegawai Nonaktif**; permission efektif dan domain lifecycle K-STATUS-04 tetap diperiksa, termasuk role efektif Super Admin/Admin Kepegawaian; bukan restore soft-delete | Tidak menetapkan default baru |
| Export pegawai | `employees.export` | Semua role configurable; scope, filter, masking, dan column allowlist tetap wajib | Super Admin ON; Admin Kepegawaian ON; Pimpinan OFF; Kepala Bagian OFF; Pegawai OFF |
| Riwayat | `employee_histories.read`, `employee_histories.create`, `employee_histories.update`, `employee_histories.delete`, `employee_histories.export` | Read cross-employee; mutability tetap menurut jenis riwayat/domain append-only | Tidak menetapkan default baru |
| Keluarga | `employee_families.read`, `employee_families.create`, `employee_families.update`, `employee_families.delete` | Read cross-employee dan mutasi yang sah, dengan scope/ownership | Tidak menetapkan default baru |
| Disiplin | `discipline_records.read`, `discipline_records.create`, `discipline_records.delete` | Scope, privacy, audit, dan mutability domain tetap berlaku | Tidak menetapkan default baru |
| Dokumen/SK | `dokumen_sk.read`, `dokumen_sk.create`, `dokumen_sk.update`, `dokumen_sk.delete` | Employee scope, private-file authorization, kategori, masking; tidak membuka seluruh arsip | Tidak menetapkan default baru |
| Referensi | `reference_tables.manage`, `sk_requirements.manage` | Referensi terpakai dan konfigurasi matriks SK tetap terlindungi | Tidak menetapkan default baru |
| Hari libur | `hari_libur.create`, `hari_libur.update`, `hari_libur.delete` | Mutasi kalender, validasi, dependency, audit | Tidak menetapkan default baru |
| Audit | `audit_logs.read` | Baca berizin, scope/privacy; audit immutable | Tidak menetapkan default baru |
| EWS | `ews.read`, `ews.configure` | Scope alert, parameter domain, lifecycle dan audit | Tidak menetapkan default baru |
| Cuti administratif | `cuti.read_all`, `cuti.configure`, `cuti.manual.manage`, `cuti.cancellation.manage`, `cuti.kepala_lembaga_documents.manage` | Monitoring/konfigurasi/fakta manual/keputusan pembatalan/dokumen administratif, dengan state dan scope domain | Tidak menetapkan default baru |
| Penangguhan cuti final | `cuti.administrative_postponement.manage` | Penangguhan seluruh periode sebelum tanggal mulai WITA; permission efektif, canonical scope, alasan wajib, reversal atomik, histori/audit dan privacy tetap berlaku | Default hanya Admin Kepegawaian; configurable untuk seluruh role, termasuk Super Admin yang tidak memperoleh izin otomatis |
| Saldo administratif | `cuti.balance.read` dalam konteks cross-employee | Key existing dipertahankan untuk baca saldo administratif; self dipisahkan menjadi PATEN | Tidak menetapkan default baru |
| Dukungan user | `users.switch_role` | Permission dan target lebih rendah pada hierarki; tanpa impersonasi | Tidak menetapkan default baru |

Default sah terdahulu yang tidak digantikan tetap menjadi konfigurasi awal saja. Assignment aktual harus dibaca dari database; tabel role historis bukan izin menanam ulang seluruh grant/revoke. Default cuti manual/pembatalan pada Admin Kepegawaian, misalnya, tidak menjadi larangan untuk grant ke role lain. Default export di atas menggantikan tabel lama yang menempatkan Pimpinan sebagai penerima default export pegawai.

## 5. Permission vs Data Scope

Untuk RBAC, alur wajib adalah permission efektif → canonical scope → ownership yang relevan → privacy/masking → domain → response/mutation. `employees.read` tidak berarti membaca seluruh pegawai dan tidak memberi export. `employees.export` tidak berarti export seluruh pegawai.

| Konteks aktor | Canonical employee scope |
|---|---|
| Super Admin / Admin Kepegawaian / Pimpinan | Global sesuai kontrak domain dan field sensitivity yang berlaku; permission tetap wajib untuk capability RBAC |
| Kepala Bagian | Bawahan langsung dalam mapping/penugasan efektif yang sah; bukan seluruh unit hanya karena ID unit diketahui |
| Pegawai | Diri sendiri |

Scope ini tidak memberi permission secara otomatis. Input employee ID asing, daftar ID eksplisit, filter, query, dan route binding harus diiriskan dengan scope di backend. Mengetahui ID dokumen atau Employee bukan authority. Access approval yang ditugaskan memakai konteks PATEN assignment, bukan grant global `employees.read` atau `cuti.read_all`.

Alur export: `employees.export` ON → canonical employee scope → filters/ID yang sah → masking/privacy → column allowlist → Excel/PDF. PDF tetap fixed-format, Excel custom tetap sesuai kontrak laporan. Role default OFF dapat memperoleh capability melalui matrix tanpa perubahan kode dan tanpa perluasan scope.

## 6. Permission efektif dan Super Admin

Seeder/migration adalah **default configuration**, sedangkan role efektif → `role_permissions`/permission matrix database adalah **effective permission** pada setiap request RBAC. Super Admin memperoleh default saat bootstrap/seeding, bukan semua permission selamanya.

Contoh wajib: `employees.export` default ON pada Super Admin; bila operator berwenang mencabutnya, `hasPermission('employees.export')` bernilai false dan export ditolak. Tidak ada generic `role == super_admin → true`, OR raw role, maupun kontrak `PROTECTED_ROLES = super_admin` yang melewati pencabutan permission. UI mengikuti hasil backend dan bukan pengaman tunggal.

Pencabutan permission RBAC tidak boleh mematikan capability PATEN yang identity/ownership/lifecycle/domain-nya sah. Sebaliknya, invalid binding, akun/Employee nonaktif atau invalid, assignment asing, dan workflow tidak valid tetap ditolak. Employee tidak dihapus; kelompok `Aktif` dan `Aktif/khusus` serta transisi terjadwal mengikuti [keputusan lifecycle](Keputusan-Lifecycle-Status-Pegawai-25-Agustus-2026.md). Reaktivasi dengan `employees.restore` tetap membuat transisi resmi, histori, dan audit. K-STATUS-04 mempertahankan domain lifecycle role efektif Super Admin/Admin Kepegawaian; keputusan ini tidak secara eksplisit mencabutnya. Kategorinya tetap RBAC, dan pencabutan permission menolak reaktivasi pada kedua role tersebut. Grant kepada role lain tidak mengalahkan domain lifecycle ini; tidak ada kategori UI ketiga atau pola allowlist generik baru.

## 7. Cuti manual dan keputusan pembatalan

### 7.1 Cuti manual

`cuti.manual.manage` ON memberi akses capability kepada role yang diberi permission, kemudian backend memeriksa scope, fakta persetujuan luar SIMPEG, duplikasi/overlap, dokumen opsional yang tervalidasi/privat, transaksi, audit, ledger/replay dan source of truth. Tidak ada hardcoded Admin Kepegawaian-only. Fakta manual tetap hanya untuk historis/transisi atau pemulihan downtime, bukan jalan pintas ketika layanan tersedia; tidak membuat approval/reservasi baru. Koreksi tetap mempertahankan histori/snapshot.

### 7.2 Keputusan pembatalan

`cuti.cancellation.manage` ON memberi akses capability tanpa syarat role efektif Admin Kepegawaian. Backend tetap memeriksa cancellation record ada dan pending, parent request berada pada state valid, transition setuju/tolak sah, scope, reservation, locking/concurrency, audit dan notifikasi. Actor tanpa permission tetap ditolak termasuk Super Admin.

Approval utama ditahan dan reservation dipertahankan saat pembatalan pending. Persetujuan membatalkan parent serta melepas reservation secara atomik; penolakan melanjutkan active step yang sama tanpa mengulang tindakan terdahulu. Alasan privat hanya dapat dibaca pemohon serta actor yang berizin dan lulus scope/state yang relevan; grant bukan akses bebas ke seluruh alasan. Permission monitoring/configuration tidak menggantikan permission pembatalan.

Penangguhan administratif atas cuti final tetap flow terpisah. Batas [6 September](Keputusan-Evaluasi-Meeting-LLDIKTI-31-Agustus-2026.md#cakupan-awal-penangguhan-administratif--6-september-2026) sebelum tanggal mulai WITA dan pembalikan seluruh periode tidak diubah.

**Penyelarasan kontrak implementasi 8 September 2026:** key `cuti.administrative_postponement.manage` dan default hanya Admin Kepegawaian mengikuti rancangan penangguhan final yang disetujui pengguna pada 6 September, bukan klaim bahwa nama teknis permission disebutkan stakeholder saat rapat. Grant/revoke melalui matrix tidak melewati canonical employee scope; permission monitoring, pembatalan pra-final, maupun role Super Admin bukan pengganti izin khusus ini. Alasan administratif hanya terlihat bagi pemohon atau pengelola berizin yang lulus scope, termasuk ketika membaca Audit Log. Permission `audit_logs.read` tetap diperlukan untuk membuka audit, tetapi tidak otomatis membuka alasan privat; snapshot audit tetap disimpan utuh dan immutable. QR publik hanya menampilkan status/waktu penangguhan, tanpa alasan administratif. Penangguhan setelah tanggal mulai atau pemakaian parsial tetap di luar cakupan awal.

## 8. Switch Role melalui RBAC dan hierarki

`users.switch_role` adalah RBAC untuk seluruh role. Permission efektif memberi capability; target divalidasi terhadap hierarki role asli berikut:

| Role asli | Target lebih rendah yang valid bila permission ON |
|---|---|
| Super Admin | Admin Kepegawaian, Pimpinan, Kepala Bagian, Pegawai |
| Admin Kepegawaian | Pimpinan, Kepala Bagian, Pegawai |
| Pimpinan | Kepala Bagian, Pegawai |
| Kepala Bagian | Pegawai |
| Pegawai | Tidak ada target lebih rendah; tidak dapat melakukan switch |

Permission OFF menolak switch untuk semua role. Target sama, lebih tinggi, tidak dikenal, Super Admin dari role lebih rendah, dan chained switch ditolak. `temporary_role` tetap persisten sampai revert; selama simulasi permission efektif berasal dari matrix target terkini. `user.id`, identitas asli, `employee_id`, ownership dan data scope tetap sesuai kontrak simulasi aktor asli, tanpa impersonation atau mengambil Employee orang lain. Audit switch, mutasi/keputusan penting, dan revert menyimpan actor asli dan konteks role aman. `temporary_permission` bukan authority alternatif.

## 9. Transisi katalog dan migration

Pemeriksaan read-only katalog lokal `database/seeders/RbacSeeder.php` dan migration pada baseline aplikasi `c2578e8045ec3b9650482af055077cf011897f7a` mengonfirmasi key legacy self, `employees.restore`, dan `cuti.balance.read`. Baseline lokal berbeda dari head PR #21; ini inventaris nama, bukan audit implementasi PR atau database deployment. Tidak ada perubahan aplikasi/database dilakukan oleh pembaruan dokumen ini.

| Permission existing/konteks | Target | Migration/deprecation note |
|---|---|---|
| `employees.read_self` | PATEN profil | Lepas ketergantungan matrix setelah regression binding/lifecycle; deprecate checkbox, bukan langsung hapus data |
| `employee_histories.read` pada self | PATEN self | Pertahankan key RBAC untuk cross-employee; pisahkan route/policy sesuai ownership |
| `employee_families.read` pada self | PATEN self | Pertahankan key RBAC untuk cross-employee; tidak membuka self mutation |
| `notifications.read` | PATEN self | Ownership route menjadi authority; key legacy dipensiunkan dari matrix target |
| `notifications.update` | PATEN self | Mark-read hanya milik user; deprecate checkbox sesudah regression |
| `hari_libur.read` | PATEN kalender | Read authenticated sesuai lifecycle; key mutasi tetap RBAC |
| `cuti.create` | PATEN/domain | Submit/revisi/permohonan pembatalan sendiri tetap memakai eligibility dan workflow |
| `cuti.read_own` | PATEN ownership | Tidak mematikan akses sendiri saat checkbox dicabut |
| `cuti.balance.read` | PATEN self; RBAC cross-employee | Gunakan key existing untuk konteks administratif; self route tidak mensyaratkannya. Tidak menciptakan key baru |
| `cuti.approve` | PATEN assignment/state | Tidak menjadi delegated generic approval; key legacy dipensiunkan dari matrix target |
| `cuti.approve_stage1`, `cuti.approve_stage2`, `cuti.approve_stage3` | PATEN assignment/state | Key stage ditemukan pada katalog lama; hilangkan ketergantungan matrix setelah seluruh stage/snapshot regression |
| `cuti.proof.generate` otomatis | PATEN aksi sistem | Artifact otomatis bagian final approval; manual regenerate bila memang diperlukan harus dipisahkan dengan kontrak administratif tersendiri |

Key target yang eksplisit disetujui pengguna tetapi tidak ditemukan pada seeder/migration baseline lokal tersebut adalah `employees.export`, `employee_histories.export`, `discipline_records.delete`, `dokumen_sk.read/create/update/delete`, dan `ews.read/configure`. Ini nama target yang disahkan, bukan klaim sudah ada pada database aktual atau usulan nama baru dari penulis. Implementasi wajib merekonsiliasi katalog aktif sebelum migration.

`cuti.configure_chain` dan `cuti.balance.reconcile` juga ada pada katalog lokal. Keduanya tetap dicatat sebagai nama teknis existing untuk konfigurasi chain/rekonsiliasi administratif yang tunduk RBAC dan domain; addendum tidak memerintahkan penghapusan atau merger otomatis dengan `cuti.configure`/`cuti.manual.manage`. Jangan membuat capability UI duplikat hanya karena alias teknis; kebutuhan konsolidasi ditelusuri dari caller saat implementasi.

Tahapan implementasi: inventaris katalog/assignment/caller aktual → pisahkan PATEN dan cross-employee → dokumentasikan migration yang menjaga grant/revoke existing → jalankan regression → sinkronkan UI matrix → deprecate key yang tidak dipakai. Jangan DELETE permission/pivot langsung atau reseed seluruh assignment agar cocok dengan tabel default. Rencana rollout dan pemulihan migration harus direview sebelum mutasi database.

## 10. Acceptance criteria dan regression

Seluruh AC berikut wajib dipetakan di [User Stories](PRD-DLL/User-Stories-SIMPEG-Fase1.md) dan [Issues](PRD-DLL/Issues-SIMPEG-Fase1.md). Statusnya **belum diverifikasi oleh tugas dokumentasi ini**.

| ID | Expected result yang harus dibuktikan |
|---|---|
| AC-RBAC-PATEN-01 | Profil sendiri tetap dapat dibaca tanpa configurable self permission jika binding/lifecycle sah |
| AC-RBAC-PATEN-02 | History/family sendiri memakai ownership; cross-employee memakai RBAC dan scope |
| AC-RBAC-PATEN-03 | Inbox/mark-read sendiri memakai ownership; notifikasi user lain ditolak |
| AC-RBAC-PATEN-04 | Read hari libur PATEN; create/update/delete tetap RBAC |
| AC-RBAC-PATEN-05 | Submit/read-own/self-balance cuti tidak dapat dicabut lewat matrix; seluruh eligibility/domain tetap berlaku |
| AC-RBAC-PATEN-06 | Approval hanya active assignment/state; permission approval tidak membuka request asing |
| AC-RBAC-CONFIG-01 | Setiap request RBAC membaca role efektif dan matrix database terkini |
| AC-RBAC-CONFIG-02 | Tidak ada universal Super Admin bypass generic permission |
| AC-RBAC-CONFIG-03 | Seeder/migration hanya initial configuration yang dapat diubah setelah deployment |
| AC-RBAC-CONFIG-04 | Grant/revoke generic permission Super Admin benar-benar mengubah akses efektif |
| AC-EXPORT-01 | `employees.read` saja tidak mengizinkan export |
| AC-EXPORT-02 | `employees.export` configurable untuk seluruh role |
| AC-EXPORT-03 | Default SA/Admin ON; Pimpinan/Kepala Bagian/Pegawai OFF |
| AC-EXPORT-04 | Role default OFF dapat diberi export melalui matrix tanpa perubahan kode |
| AC-EXPORT-05 | Export yang diizinkan tetap mengikuti canonical employee scope |
| AC-EXPORT-06 | Foreign Employee ID maupun filter tidak dapat melewati scope |
| AC-EXPORT-07 | Masking/privacy/column allowlist tetap diterapkan sesudah permission lolos |
| AC-DOC-01 | `dokumen_sk.read/create/update/delete` configurable RBAC |
| AC-DOC-02 | Raw role allowlist tidak membatalkan granted permission; privacy/domain eksplisit tetap berlaku |
| AC-DOC-03 | Dokumen dibaca menurut scope, private-file authorization, kategori dan masking |
| AC-CUTI-MANUAL-01 | `cuti.manual.manage` configurable lewat matrix |
| AC-CUTI-MANUAL-02 | Grant ke role selain default efektif tanpa perubahan kode |
| AC-CUTI-MANUAL-03 | Validasi fakta, ledger/replay dan audit tetap wajib |
| AC-CUTI-CANCEL-01 | `cuti.cancellation.manage` configurable lewat matrix |
| AC-CUTI-CANCEL-02 | Tidak ada effective Admin Kepegawaian-only permanen |
| AC-CUTI-CANCEL-03 | State, transition, locking, reservation, audit dan notification tetap enforced |
| AC-SWITCH-01 | `users.switch_role` configurable RBAC |
| AC-SWITCH-02 | Permission ON hanya memberi target lebih rendah menurut hierarki role asli |
| AC-SWITCH-03 | Same/higher/invalid target ditolak |
| AC-SWITCH-04 | Chained switch ditolak sampai revert |
| AC-SWITCH-05 | Identitas/employee ownership dan data scope simulasi tidak berubah menjadi milik user lain |

Regression minimum memakai PostgreSQL untuk perilaku DB-sensitive: Super Admin permission ON/allowed dan OFF/denied; export default Admin ON, Pimpinan OFF lalu grant/global scope sah, Kepala Bagian grant/bawahan saja, Pegawai grant/self saja; foreign ID/filter denial; PATEN tanpa key self pada role matrix tetap tersedia; negative lifecycle/ownership/eligibility; hierarchy Switch Role seluruh role termasuk revoke/persistence/revert/chained denial; manual/cancellation grant dan revoke pada role selain default serta invalid state/concurrency/audit rollback. Generate proof otomatis harus tetap terjadi pada final approval sah tanpa checkbox `cuti.proof.generate`; legacy manual regenerate tidak diasumsikan tersedia. Grant history update/delete tidak boleh meloloskan mutasi record immutable.

Browser regression memeriksa matrix hanya dua kategori, self capability tidak menjadi checkbox, menu sesuai permission, scope data, denied direct URL, dan tidak ada console error. Exact SHA, environment, expected/actual, audit tersanitasi, serta hasil test dicatat; automated pass tidak menjadi penerimaan UAT.

## 11. Klausul yang disupersede

| Sumber/klausul lama | Bagian yang digantikan | Kontrak pengganti |
|---|---|---|
| K-RBAC-01 butir 1–5 (2 September) | Penyamarataan seluruh capability sebagai configurable permission dan contoh role invariant yang bertentangan | §2–6: PATEN terpisah, RBAC dinamis tanpa bypass; scope/domain tetap |
| K-RBAC-02 butir 2–3, matrix butir 6, batas aktor butir 7 | Hanya original Super Admin/Admin Kepegawaian dapat switch | §8: permission + lower-role hierarchy seluruh role; identitas/persistence/audit/larangan chained tetap |
| K-RBAC-04 tabel dan butir 1–4 | Keputusan/alasan pembatalan terkunci effective Admin Kepegawaian; self terkait checkbox `cuti.create` | §3 dan §7.2: pemohon PATEN; keputusan RBAC + scope/state/domain |
| Evaluasi 15 Agustus K-MTG-01.4; Cuti Saldo K-CUT-05; PRD Addendum 24 butir 6; US-4.13 | Mutasi fakta cuti manual eksklusif Admin Kepegawaian | §7.1: delegated `cuti.manual.manage`; fakta/snapshot/ledger/audit tidak berubah |
| Evaluasi 31 Agustus K-MTG-10.2 dan penegasan 4 September | Pembatas role permanen pada aktor keputusan pembatalan | §7.2; state/hold/release/continue tetap berlaku |
| PRD Addendum 27; US-1.6; issue/AC/UAT Switch Role 2 September | Penolakan Pimpinan/Kepala Bagian meskipun diberi permission | §8 dan AC-SWITCH-01–05 |
| Tabel default export Pimpinan dan role guard permanen pada laporan | Default ON Pimpinan atau export hanya role tertentu | §4–5: ON hanya SA/Admin sebagai default; all-role configurable dengan scope |
| Contoh self permission dan generic Super Admin bypass pada panduan/QA/tracker | Matrix sebagai syarat self; role Super Admin selalu allowed | §2–6 dan §9; fakta hasil test lama tidak ditulis ulang |

Keputusan lama tidak seluruhnya obsolete. State cuti, saldo, histori, dokumen privat, workflow assignment, lifecycle termasuk K-STATUS-04, serta audit yang tidak bertentangan tetap berlaku. Nama teknis role `kepala_bagian` tidak diganti oleh addendum ini.

## 12. Koordinasi delivery dan pertanyaan terbuka

[Issue #6 aktif](https://github.com/LLDIKTI16/simpeg/issues/6) tetap core SSO: mapping deterministik, reuse user–employee, role internal non-overwrite, binding, concurrency, audit, serta dependency claim/UAT. [Issue #7 aktif](https://github.com/LLDIKTI16/simpeg/issues/7) adalah rujukan koordinasi Switch Role yang disebut Issue #6. Nomor #6/#7 pada backlog historis dokumen tidak otomatis menunjuk issue GitHub aktif tersebut.

Regression lintas modul akibat keputusan ini perlu slice koordinasi tersendiri yang menaut AC di §10 dan area terdampak PR #21; jangan otomatis memindahkan seluruh redesign ke owner SSO, membuat nomor issue/owner baru, atau menyatakan PR tersebut sudah menyelesaikannya.

**OPEN PRODUCT DECISION:** siapa/nama permission yang boleh memutasi matrix RBAC, anti-lockout policy, dan bootstrap recovery belum ditetapkan. Tidak ada asumsi proteksi permanen Super Admin, recovery bypass, ataupun grant administratif otomatis. Default role lain yang tidak secara eksplisit disahkan tidak dibuat oleh addendum ini. Jika manual regenerate artifact memang diperlukan, capability/nama permission administratifnya harus ditetapkan setelah kebutuhan serta katalog aktual diperiksa; dokumen ini tidak mengada-adakan fitur tersebut.

## 13. Pembacaan evidence dan salinan historis

Tracker, laporan QA, notulen, transkrip dan contoh kode bertanggal lama mempertahankan fakta saat dicatat. Klausul authorization yang bertentangan dengan §2–8 adalah **Superseded untuk kontrak target**, bukan bukti hasil test terbaru. Raw transcript `Transkrip-Meeting-LLDIKTI-raw.json` dan `Evaluasi Projek SIMPEG bersama Mahasiswa Magang Univ Klabat.txt` adalah sumber ucapan historis yang tidak ditulis ulang sebagai keputusan 7 September.

Salinan `Runbook-Demo-Fitur-SIMPEG-Fase-1.docx` adalah **arsip panduan 31 Agustus — klausul authorization Superseded**, bukan runbook target 7 September. Panduan aktif target adalah [runbook Markdown](Runbook-Demo-Fitur-SIMPEG-Fase-1.md) beserta addendum ini. Arsip Word dipertahankan untuk jejak historis; tidak menjadi bukti UI atau prosedur RBAC baru telah tersedia.
