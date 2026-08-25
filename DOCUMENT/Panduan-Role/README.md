# Panduan Penggunaan SIMPEG per Role

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
| Kepala Bagian | [Panduan Kepala Bagian](Panduan-Kepala-Bagian.md) | Draft | Belum ada |
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

- Keycloak mengautentikasi identitas; role dan permission SIMPEG menentukan akses.
- Akun tanpa role internal yang valid tidak memperoleh akses SIMPEG.
- Tombol yang tersembunyi bukan satu-satunya pengaman; backend tetap menolak aksi tanpa izin.
- Jangan membagikan token, password, NIK, No. KK, atau dokumen pegawai kepada pihak yang tidak
  berwenang.
- Audit Log tidak boleh diedit atau dihapus melalui aplikasi.
- Employee tidak dihapus atau dipindahkan pada Fase 1; lifecycle menggunakan perubahan status resmi pada Data Pegawai, tanpa Data Backup/Data Nonaktif.
- Kelompok status `Aktif` dan `Aktif/khusus` sama-sama aktif. User linked ke Employee efektif Nonaktif hanya dapat membuka halaman status akun, logout, dan route auth teknis yang diperlukan, tanpa pengecualian role.
- Keputusan cuti resmi adalah `Disetujui`, `Perubahan`, `Ditangguhkan`, dan `Tidak Disetujui`.
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
