# Panduan Penggunaan — Super Admin

| Field | Nilai |
|---|---|
| Role internal | `super_admin` |
| Status | **Draft — belum diterima Kepegawaian** |
| Cakupan | Administrasi sistem dan seluruh kemampuan operasional Admin Kepegawaian |

## 1. Prasyarat

- Akun Keycloak sudah dipetakan ke user dan pegawai aktif SIMPEG.
- Role internal user adalah `super_admin` dengan permission yang sesuai.
- Reference data, unit, Kepala Bagian, dan konfigurasi approval yang diperlukan sudah tersedia.
- Gunakan environment dan data uji yang disetujui untuk UAT; jangan memakai data pribadi nyata.

## 2. Fitur dan Langkah Utama

| Fitur | Langkah ringkas | Dampak tindakan |
|---|---|---|
| Kelola Akses User | Buka **Kelola Akses User**, cari pegawai, isi identifier Keycloak, pilih role internal, lalu simpan | Mengubah kemampuan user di SIMPEG dan menghasilkan Audit Log |
| Role & Permission | Buka **Role & Permission**, periksa role dan permission, ubah hanya berdasarkan keputusan yang disetujui | Dapat memperluas atau mencabut akses; salah konfigurasi dapat mengunci alur operasional |
| Data Master | Buka **Data Master**, pilih referensi, tambah/ubah/nonaktifkan sesuai dependency | Mengubah pilihan kanonis yang dipakai form, perhitungan, dan laporan |
| Data Pegawai | Cari pegawai, tambah atau ubah data utama, tambahkan riwayat berdasarkan SK, dan kelola status aktif | Mutasi pegawai dan riwayat tercatat dalam audit; histori kepegawaian bersifat append-only |
| Import Pegawai | Unduh template, unggah CSV/Excel, petakan kolom, validasi, periksa preview, lalu jalankan import | Dapat membuat banyak pegawai; baris import diklasifikasikan imported/skipped/failed |
| Konfigurasi Approval Cuti | Buka **Konfigurasi Approval Cuti**, tetapkan verifikator, Kepala Bagian, dan PYBMC sesuai urutan kanonis | Hanya pengajuan baru yang memakai konfigurasi baru; snapshot pengajuan berjalan tidak berubah |
| Channel Notifikasi | Buka **Channel Notifikasi**, periksa kill-switch dan kebijakan event | Mengaktifkan atau menonaktifkan intent per channel; tidak mengaktifkan provider yang belum tersedia |
| Konfigurasi EWS | Buka **Konfigurasi EWS**, ubah parameter yang disetujui, lalu simpan | Memengaruhi alert yang dibentuk scheduler dan penerima notifikasi |
| Audit Log | Buka **Audit Log**, filter aktivitas, lalu buka detail | Akses baca untuk traceability; record audit tidak boleh diubah atau dihapus |
| Laporan/Export | Pilih filter dan kolom aman, periksa preview, lalu unduh Excel atau PDF | Menghasilkan salinan data; NIK/No. KK tidak boleh masuk export tanpa kebutuhan dan persetujuan eksplisit |

## 3. Alur Kelola Akses User

1. Pastikan pegawai target benar dan aktif.
2. Buka `/user-management`.
3. Cari pegawai berdasarkan nama, NIP, atau atribut yang tersedia.
4. Masukkan identifier Keycloak kanonis; jangan menyalin token atau claim mentah.
5. Pilih role internal yang sudah disetujui.
6. Simpan dan periksa pesan hasil.
7. Verifikasi role/permission efektif.
8. Periksa Audit Log tanpa mengekspos identifier mentah.

Jika identifier sudah digunakan pegawai lain atau mapping ambigu, hentikan proses dan eskalasi;
jangan memindahkan mapping secara manual melalui database.

## 4. Alur Konfigurasi Approval Cuti

1. Pastikan pegawai, verifikator, Kepala Bagian, dan PYBMC aktif.
2. Atur rantai `0..N verifikator → Kepala Bagian → PYBMC`.
3. Ketua Tim, bila digunakan, dicatat sebagai verifikator.
4. Simpan dan periksa preview rantai.
5. Buat pengajuan uji baru untuk membuktikan runtime.
6. Jangan mengubah snapshot pengajuan yang sudah berjalan.

## 5. Batas Akses dan Larangan

- Jangan memberi akses berdasarkan role claim Keycloak.
- Jangan membuat login manual produksi.
- Jangan melakukan hard delete pegawai.
- Jangan mengedit histori kepegawaian lama; tambahkan record baru berdasarkan dokumen resmi.
- Jangan mengubah saldo cuti secara langsung; koreksi dilakukan melalui sumber pemakaian dan
  rekalkulasi yang diaudit.
- Jangan mengaktifkan WhatsApp tanpa dependency resmi.
- Jangan mengubah atau menghapus Audit Log.
- Jangan memasukkan NIK, No. KK, token, atau credential ke screenshot/evidence.

## 6. Troubleshooting

| Gejala | Pemeriksaan |
|---|---|
| User mendapat 403 | Periksa mapping user–pegawai, status aktif, role internal, dan permission |
| Konfigurasi cuti tidak dapat disimpan | Periksa urutan, approver aktif, tepat satu Kepala Bagian, dan PYBMC terakhir |
| Email tidak terkirim | Periksa kebijakan channel, queue worker, failed jobs, dan konfigurasi mail tanpa membuka credential |
| EWS tidak muncul | Periksa histori/TMT, konfigurasi periode, scheduler, deduplikasi, dan scope penerima |
| Audit tidak ditemukan | Periksa actor, waktu, model, filter, serta apakah mutasi berhasil di-commit |

## 7. Penerimaan Panduan

| Field | Nilai |
|---|---|
| Exact SHA yang diuji | Belum diisi |
| Tanggal UAT | Belum diisi |
| Pemberi keputusan | Belum diisi |
| Status | Perlu Tindak Lanjut — UAT belum dilaksanakan |
| Evidence | Belum ada |
