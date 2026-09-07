# Panduan Penggunaan SIMPEG per Role

> **Kontrak target 7 September 2026:** [Keputusan PATEN dan RBAC](../Keputusan-RBAC-Pemisahan-Capability-Paten-dan-Configurable-7-September-2026.md) menggantikan batas authorization lama pada panduan ini. Capability personal/assignment/domain adalah **🔒 PATEN**; capability delegated/admin adalah **⚙️ RBAC**. Role contoh menggambarkan konfigurasi awal, bukan allowlist permanen. Perubahan ini belum membuktikan implementasi atau UAT lulus.

| Field | Nilai |
|---|---|
| Terkait | Issue [LLDIKTI16/simpeg#14](https://github.com/LLDIKTI16/simpeg/issues/14) |
| Status paket | **Draft — belum diterima Kepegawaian** |
| Bahasa antarmuka | Bahasa Indonesia |
| Target final | Akhir Agustus 2026 |

## Daftar Panduan

| Role | Panduan | Status | Evidence penerimaan |
|---|---|---|---|
| Super Admin | [Panduan Super Admin](Panduan-Super-Admin.md) | Draft | Belum ada |
| Admin Kepegawaian | [Panduan Admin Kepegawaian](Panduan-Admin-Kepegawaian.md) | Draft | Belum ada |
| Pimpinan | [Panduan Pimpinan](Panduan-Pimpinan.md) | Draft | Belum ada |
| Atasan Langsung (role teknis `kepala_bagian`) | [Panduan Kepala Bagian](Panduan-Kepala-Bagian.md) | Draft | Belum ada |
| Pegawai | [Panduan Pegawai](Panduan-Pegawai.md) | Draft | Belum ada |

## Kontrak Isi

Setiap panduan memuat:

- fitur utama yang tersedia;
- langkah penggunaan alur utama;
- prasyarat sebelum tindakan;
- dampak tindakan;
- batas akses dan hal yang dilarang;
- troubleshooting ringkas;
- record penerimaan.

Panduan baru boleh berstatus `Diterima` setelah fitur terkait diterima dalam UAT, langkah diperiksa
pada exact release candidate, dan pihak Kepegawaian memberikan konfirmasi eksplisit.

## Aturan Umum Seluruh Role

- Keycloak mengautentikasi identitas. PATEN mengikuti identity/employee binding, ownership, assignment, lifecycle, dan domain; RBAC mengikuti effective role → permission matrix terkini. Super Admin tidak memiliki universal bypass dan revoke permission RBAC harus menutup aksesnya.
- Permission fitur dapat diassign atau dicabut melalui matrix. Contohnya `dokumen_sk.read`, `ews.configure`, `cuti.configure`, dan `employees.export` tetap tunduk pada backend, data scope, masking, serta business invariant eksplisit.
- Switch Role memerlukan `users.switch_role` dan target lebih rendah pada hierarki Super Admin → Admin Kepegawaian → Pimpinan → Kepala Bagian → Pegawai. Pegawai tidak mempunyai target lebih rendah. Same/higher/unknown/chained switch ditolak; identitas, employee binding, ownership, dan scope aktor asli tetap.
- Profil/riwayat/keluarga sendiri, inbox/mark-read sendiri, baca Hari Libur, submit/read-own/saldo cuti sendiri adalah PATEN selama lifecycle/domain valid. Approval berasal dari active step/assignment; proof otomatis adalah PATEN sistem. Keduanya tidak dipengaruhi checkbox legacy.
- Akses cross-employee memerlukan RBAC (`employees.read`, `employee_histories.read`, `employee_families.read`, `cuti.read_all`, atau `cuti.balance.read`) sesuai capability. Permission tidak memperluas scope: role global mengikuti scope global kanonis, Kepala Bagian hanya bawahan sah, dan Pegawai self.
- `employees.export` tersedia untuk seluruh role: default ON Super Admin/Admin Kepegawaian, OFF Pimpinan/Kepala Bagian/Pegawai. Grant/revoke harus efektif; filter, explicit IDs, masking/privacy, dan column allowlist tetap tunduk scope.
- `cuti.manual.manage` dan `cuti.cancellation.manage` dapat didelegasikan melalui matrix; tidak ada invariant Admin Kepegawaian-only. Ledger/replay, workflow, locking, reservasi, audit, serta notifikasi tetap wajib.
- Seluruh `dokumen_sk.read/create/update/delete` tetap RBAC dengan scope dan private-file authorization; ownership saja tidak memberi hak mutasi dokumen. `ews.read/configure`, `audit_logs.read`, dan mutasi Hari Libur juga tetap RBAC.
- Kewenangan pengelola matrix, anti-lockout, dan bootstrap recovery adalah **OPEN PRODUCT DECISION**; daftar menu demo bukan pemberian hak baru.
- Akun tanpa role internal yang valid tidak memperoleh akses SIMPEG.
- Tombol yang tersembunyi bukan satu-satunya pengaman; backend tetap menolak aksi tanpa izin.
- Jangan membagikan token, password, NIK, No. KK, atau dokumen pegawai kepada pihak yang tidak
  berwenang.
- Audit Log tidak boleh diedit atau dihapus melalui aplikasi.
- Employee tidak dihapus atau dipindahkan pada Fase 1; lifecycle menggunakan perubahan status resmi pada Data Pegawai, tanpa Data Backup/Data Nonaktif.
- Kelompok status `Aktif` dan `Aktif/khusus` sama-sama aktif. User linked ke Employee efektif Nonaktif hanya dapat membuka halaman status akun, logout, dan route auth teknis yang diperlukan, tanpa pengecualian role.
- Keputusan cuti resmi adalah `Disetujui`, `Perubahan`, `Ditangguhkan`, dan `Tidak Disetujui`.
- Pada alur cuti, urutan bisnis adalah `0..n Verifikator → Atasan Langsung → PYBMC`. Nama role/route teknis lama tidak berubah hanya karena label bisnis ini.
- Panduan ini mengikuti [Keputusan Evaluasi SIMPEG Bersama LLDIKTI 31 Agustus 2026](../Keputusan-Evaluasi-Meeting-LLDIKTI-31-Agustus-2026.md). Semua langkah baru tetap berstatus draft sampai tersedia evidence UAT pada release candidate yang tepat.
- WhatsApp Business tidak boleh dinyatakan aktif sebelum provider, credential, template ID, nomor
  uji, dan sandbox resmi tersedia serta terverifikasi.
- PDF bersifat fixed-format. Custom PDF bebas dan tanda tangan elektronik tersertifikasi bukan scope
  Fase 1.

## Sumber

- [Runbook Demo Fitur SIMPEG Fase 1](../Runbook-Demo-Fitur-SIMPEG-Fase-1.md)
- [Tracking Role](../Tracking-Role/README.md)
- [PRD SIMPEG Fase 1](../PRD-DLL/PRD-SIMPEG-Fase1-Core.md)
- [User Stories SIMPEG Fase 1](../PRD-DLL/User-Stories-SIMPEG-Fase1.md)
- [Keputusan Lifecycle dan Status Pegawai](../Keputusan-Lifecycle-Status-Pegawai-25-Agustus-2026.md)
- [Keputusan RBAC Configurable dan Switch Role](../Keputusan-RBAC-dan-Switch-Role-2-September-2026.md)
