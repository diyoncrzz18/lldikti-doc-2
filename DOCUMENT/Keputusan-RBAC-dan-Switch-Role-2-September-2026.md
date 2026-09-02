# Keputusan Produk — RBAC Configurable dan Switch Role

| Field | Detail |
|---|---|
| **Tanggal keputusan** | 2 September 2026 |
| **Status** | **Disetujui** — kontrak aktif untuk RBAC dan Switch Role pada Fase 1 |
| **Kedudukan** | Melengkapi serta menggantikan K-MTG-03 dan OQ-MTG-03 pada area yang bertentangan. Keputusan 15 Agustus tetap dipertahankan sebagai riwayat **Superseded**. |
| **Dokumen produk terkait** | [PRD SIMPEG Fase 1 Core](PRD-DLL/PRD-SIMPEG-Fase1-Core.md), [User Stories](PRD-DLL/User-Stories-SIMPEG-Fase1.md), dan [Backlog Issues](PRD-DLL/Issues-SIMPEG-Fase1.md) |

## K-RBAC-01 — Permission matrix sebagai sumber kebenaran

1. Assignment dan pencabutan seluruh permission aplikasi dilakukan melalui **permission matrix RBAC di database**. Seeder hanya menetapkan konfigurasi awal yang dapat berubah; ia bukan kontrak otorisasi permanen.
2. Backend wajib membaca permission efektif secara dinamis dari role efektif dan permission matrix terkini pada setiap request. Role, claim Keycloak, menu, atau default seeder tidak boleh menjadi bypass maupun penolakan tambahan atas permission yang sudah diberikan.
3. Policy, middleware, FormRequest, Action, dan service tidak boleh mengandung allowlist role-permission yang mengunci permission ke role tertentu. `CutiPermissionMatrixPolicy` atau abstraksi serupa hanya boleh mengevaluasi permission efektif dan business rule domain yang relevan.
4. Coarse role gate hanya diperbolehkan bila keputusan produk ini atau keputusan produk lain menyatakan **business invariant** secara eksplisit. Gate tersebut harus ditulis sebagai pengecualian, diuji fail-closed, dan tidak boleh dijadikan pola umum untuk fitur configurable.
5. Dokumentasi hak akses per role harus diberi label **Default permission / konfigurasi awal**. Tabel tersebut menjelaskan seeding atau penggunaan umum, bukan hard authorization contract.
6. Hak baca dokumen dan arsip mengikuti permission efektif. Contohnya, role Pimpinan yang diberi `dokumen_sk.read` dapat mengakses dokumen sesuai data scope dan masking. Hak mutasi dokumen tetap dipisahkan dari hak baca dengan permission mutasi yang relevan.
7. Export pegawai harus memakai permission granular `employees.export`. `employees.read` hanya memberi hak baca sesuai scope dan tidak otomatis memberi hak mengunduh raw export. Filter, masking, dan allowlist kolom tetap berlaku setelah permission export diberikan.

## K-RBAC-02 — Switch Role sebagai business invariant

1. Permission `users.switch_role` tetap dikelola melalui permission matrix RBAC.
2. Hanya user dengan **role asli** `Super Admin` atau `Admin Kepegawaian` dan memiliki `users.switch_role` yang boleh memulai Switch Role. Ini adalah business invariant backend.
3. `Pimpinan`, `Kepala Bagian`, dan `Pegawai` tetap ditolak fail-closed untuk memulai Switch Role, sekalipun permission `users.switch_role` salah ter-assign pada matrix.
4. Switch Role adalah simulasi role, bukan impersonasi identitas: `user.id`, `employee_id`, ownership, dan data scope tetap milik aktor asli. Hanya effective role dan effective permission yang berubah.
5. `temporary_role` disimpan persisten sampai revert. Permission efektif selama simulasi selalu berasal dari konfigurasi terbaru role target; `temporary_permission` bukan sumber kebenaran otorisasi.
6. Matrix target yang disetujui:

| Role asli | Target yang diizinkan |
|---|---|
| Super Admin | Admin Kepegawaian, Pimpinan, Kepala Bagian, Pegawai |
| Admin Kepegawaian | Pimpinan, Kepala Bagian, Pegawai |

7. Sistem menolak switch ke role yang sama, role lebih tinggi, `Super Admin`, role di luar matrix, atau switch berantai ketika `temporary_role` masih aktif. Aktor harus melakukan revert lebih dahulu.
8. Setiap switch, penggunaan role sementara yang menghasilkan mutasi/keputusan penting, dan revert wajib diaudit dengan aktor asli, role asli, role target/effective, waktu, serta konteks aman.

## K-RBAC-03 — Verifikasi dan batas keputusan

1. Bukti implementasi harus menguji assignment dan pencabutan permission pada role yang tidak memiliki default lama, termasuk Pimpinan + `dokumen_sk.read`, Kepala Bagian + `ews.configure`, Pimpinan + `cuti.configure`, dan permission export terpisah dari `employees.read`.
2. Bukti Switch Role wajib menguji izin dan penolakan untuk seluruh kombinasi role asli/target, identitas dan ownership tetap, perubahan matrix target pada request berikutnya, persistence, revert, audit, serta larangan chained switch.
3. Keputusan ini tidak mengubah invariant domain lain yang telah dinyatakan eksplisit, seperti ownership data, status Employee Nonaktif, urutan/snapshot approval cuti, atau syarat approver aktif.

## Open Question yang perlu keputusan stakeholder

- Keputusan ini menetapkan **permission matrix sebagai sumber kebenaran assignment**, tetapi belum menetapkan nama permission/aktor yang berwenang memutasi matrix RBAC itu sendiri maupun kebijakan anti-lockout terakhir. Sebelum implementasi mengubah gate administrasi matrix, stakeholder perlu mengesahkan kontrak tersebut. Sampai itu terjadi, dokumentasi tidak menganggap role tertentu otomatis memiliki hak mengubah matrix hanya berdasarkan nama role.

## Dampak dokumentasi dan delivery

- K-MTG-03 dan OQ-MTG-03 pada keputusan 15 Agustus menjadi riwayat **Superseded** pada area Switch Role.
- PRD dan User Stories dinaikkan ke v1.13 dan menjadi kontrak aktif untuk permission-driven RBAC dan Switch Role.
- Issue, tracker, panduan, runbook, UAT, serta catatan QA lama harus menaut ke keputusan ini tanpa menulis ulang fakta historis implementasi.
- Perubahan produk tidak membuktikan implementasi. Penutupan hanya dapat dilakukan setelah test authorization, data scope, audit, PostgreSQL, dan browser/UAT yang relevan tersedia.
