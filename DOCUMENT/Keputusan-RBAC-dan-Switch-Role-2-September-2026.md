# Keputusan Produk — RBAC Configurable dan Switch Role

| Field | Detail |
|---|---|
| **Tanggal keputusan** | 2 September 2026 |
| **Status** | **Disetujui; sebagian Superseded 7 September 2026** sesuai penanda per bagian di bawah |
| **Kedudukan** | Melengkapi serta menggantikan K-MTG-03 dan OQ-MTG-03 pada area yang bertentangan. Keputusan 15 Agustus tetap dipertahankan sebagai riwayat **Superseded**. |
| **Dokumen produk terkait** | [PRD SIMPEG Fase 1 Core](PRD-DLL/PRD-SIMPEG-Fase1-Core.md), [User Stories](PRD-DLL/User-Stories-SIMPEG-Fase1.md), dan [Backlog Issues](PRD-DLL/Issues-SIMPEG-Fase1.md) |

> **Otoritas terbaru:** [Keputusan PATEN dan RBAC 7 September 2026](Keputusan-RBAC-Pemisahan-Capability-Paten-dan-Configurable-7-September-2026.md). Hanya capability delegated/admin termasuk matrix RBAC. Self/ownership, assignment approval, dan aksi sistem/domain adalah PATEN; lifecycle, scope, masking, workflow, dan audit tetap wajib. Riwayat K-RBAC-01/02/04 dipertahankan secara spesifik, bukan dinyatakan seluruhnya obsolete.

## K-RBAC-01 — Permission matrix sebagai sumber kebenaran

> **Superseded sebagian 7 September 2026:** cakupan kata “seluruh permission” pada butir 1–2 tidak berlaku bagi capability PATEN. Butir tersebut berlaku untuk RBAC saja, termasuk Super Admin yang tidak memiliki bypass. Butir 4 tidak lagi mengesahkan role gate pembatalan/manual ataupun allowlist aktor Switch Role lama. Butir 6–7 tetap berlaku; export configurable untuk seluruh role dengan default ON hanya Super Admin/Admin Kepegawaian dan OFF Pimpinan/Kepala Bagian/Pegawai, selalu mengikuti scope, masking, dan allowlist kolom.

1. Assignment dan pencabutan seluruh permission aplikasi dilakukan melalui **permission matrix RBAC di database**. Seeder hanya menetapkan konfigurasi awal yang dapat berubah; ia bukan kontrak otorisasi permanen.
2. Backend wajib membaca permission efektif secara dinamis dari role efektif dan permission matrix terkini pada setiap request. Role, claim Keycloak, menu, atau default seeder tidak boleh menjadi bypass maupun penolakan tambahan atas permission yang sudah diberikan.
3. Policy, middleware, FormRequest, Action, dan service tidak boleh mengandung allowlist role-permission yang mengunci permission ke role tertentu. `CutiPermissionMatrixPolicy` atau abstraksi serupa hanya boleh mengevaluasi permission efektif dan business rule domain yang relevan.
4. Coarse role gate hanya diperbolehkan bila keputusan produk ini atau keputusan produk lain menyatakan **business invariant** secara eksplisit. Gate tersebut harus ditulis sebagai pengecualian, diuji fail-closed, dan tidak boleh dijadikan pola umum untuk fitur configurable.
5. Dokumentasi hak akses per role harus diberi label **Default permission / konfigurasi awal**. Tabel tersebut menjelaskan seeding atau penggunaan umum, bukan hard authorization contract.
6. Hak baca dokumen dan arsip mengikuti permission efektif. Contohnya, role Pimpinan yang diberi `dokumen_sk.read` dapat mengakses dokumen sesuai data scope dan masking. Hak mutasi dokumen tetap dipisahkan dari hak baca dengan permission mutasi yang relevan.
7. Export pegawai harus memakai permission granular `employees.export`. `employees.read` hanya memberi hak baca sesuai scope dan tidak otomatis memberi hak mengunduh raw export. Filter, masking, dan allowlist kolom tetap berlaku setelah permission export diberikan.

## K-RBAC-02 — Switch Role sebagai business invariant

> **Riwayat Superseded 7 September 2026 untuk butir 2–3 dan kelengkapan matrix butir 6.** Otoritas aktif adalah permission efektif `users.switch_role` + target lebih rendah pada hierarki seluruh role: Super Admin → Admin Kepegawaian → Pimpinan → Kepala Bagian → Pegawai. Pimpinan dapat menarget Kepala Bagian/Pegawai dan Kepala Bagian dapat menarget Pegawai bila permission diberikan. Pegawai tidak mempunyai target lebih rendah. Butir 4–5, larangan same/higher/unknown/chained switch, identitas asli, ownership/scope asli, persistence, revert, dan audit tetap berlaku. Tabel dua role di bawah adalah snapshot historis, bukan matrix aktif lengkap.

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

## K-RBAC-04 — Permohonan pembatalan cuti sebagai business invariant

> **Riwayat Superseded 7 September 2026 untuk kolom batas role dan butir 1–2/4 yang mengunci aktor.** `cuti.cancellation.manage` sekarang RBAC yang dapat diberikan/dicabut dari role mana pun. Default historis Admin Kepegawaian tidak menjadi batas permanen. Authority keputusan/pembacaan alasan privat adalah permission tersebut + canonical scope + validasi request pending, parent state, transisi, reservasi, locking, audit, dan notifikasi. Privasi alasan tetap dibatasi pada pemohon dan pengelola berizin sesuai scope. Butir 3 tetap memisahkan monitoring/configuration dari keputusan pembatalan, tetapi `cuti.create` untuk pemohon kini PATEN/domain dan tidak bergantung checkbox. Butir dan tabel lama berikut dipertahankan sebagai bukti keputusan 4 September, bukan AC aktif.

**Penyelarasan dokumentasi 4 September 2026:** key dan batas otorisasi berikut berasal dari spec implementasi pembatalan/revisi bertanggal 3 September 2026 yang telah disetujui pengguna. Ini mencatat keputusan engineering tersebut pada matriks kanonis, bukan mengklaim stakeholder menetapkan nama teknis permission saat rapat.

| Operasi | Permission efektif | Batas domain | Default permission / konfigurasi awal |
|---|---|---|---|
| Membuka antrean dan alasan pembatalan, serta menyetujui atau menolak permohonan | `cuti.cancellation.manage` | Role **efektif** `admin_kepegawaian`; keputusan hanya untuk permohonan yang masih pending | Admin Kepegawaian saja; Super Admin tidak mendapatkannya otomatis |

1. Ini merupakan pengecualian business invariant terhadap gate permission-only pada K-RBAC-01: hanya Admin Kepegawaian yang berwenang memutus permohonan pembatalan. Backend memeriksa role efektif **dan** permission efektif; role asli maupun nama role saja tidak memberi bypass.
2. Permission tetap dikelola melalui matrix database dan dibaca terkini. Pencabutannya dari Admin Kepegawaian menutup akses pada request berikutnya; pemberiannya kepada role efektif lain tidak melewati invariant ini. Ketentuan ini bukan allowlist umum untuk permission cuti lainnya.
3. `cuti.configure`, `cuti.read_all`, dan permission approval utama tidak menggantikan `cuti.cancellation.manage`. Monitoring pengajuan tidak otomatis memberi hak membaca alasan pembatalan privat atau memutusnya. Hak pemohon untuk mengajukan pembatalan dengan `cuti.create` dan membaca alasan miliknya tetap tunduk pada ownership/data scope.
4. Verifikasi mencakup Admin berizin, Admin tanpa permission, role efektif lain walaupun diberi permission, simulasi role, serta pemeriksaan ulang pada Action. Alasan pembatalan hanya boleh terbaca oleh pemohon dan Admin Kepegawaian yang berwenang; audit dan notifikasi tetap mengikuti kontrak privasi pembatalan.

## OPEN PRODUCT DECISION

- Keputusan ini belum menetapkan nama permission/aktor yang berwenang memutasi matrix RBAC, kebijakan anti-lockout, maupun bootstrap recovery. Sebelum implementasi mengubah gate atau recovery tersebut, stakeholder perlu mengesahkan kontraknya. Tidak ada role yang otomatis memiliki hak mengubah matrix hanya berdasarkan nama role.

## Dampak dokumentasi dan delivery

- K-MTG-03 dan OQ-MTG-03 pada keputusan 15 Agustus menjadi riwayat **Superseded** pada area Switch Role.
- Pada 2 September, PRD dan User Stories dinaikkan ke v1.15. Snapshot tersebut dipertahankan sebagai histori; kontrak aktif PATEN/RBAC kini mengikuti keputusan 7 September dan dokumen v1.17.
- Issue, tracker, panduan, runbook, UAT, serta catatan QA lama harus menaut ke keputusan ini tanpa menulis ulang fakta historis implementasi.
- Perubahan produk tidak membuktikan implementasi. Penutupan hanya dapat dilakukan setelah test authorization, data scope, audit, PostgreSQL, dan browser/UAT yang relevan tersedia.
