# Panduan Penggunaan — Super Admin

| Field | Nilai |
|---|---|
| Role internal | `super_admin` |
| Status | **Draft — belum diterima Kepegawaian** |
| Cakupan | Default permission administrasi sistem dan kemampuan operasional Admin Kepegawaian; akses aktual mengikuti permission efektif dan scope |

## 1. Prasyarat

- Akun Keycloak sudah dipetakan ke user dan pegawai aktif SIMPEG.
- Role internal user adalah `super_admin` dengan permission yang sesuai.
- Reference data, unit, Atasan Langsung, dan konfigurasi approval yang diperlukan sudah tersedia.
- Gunakan environment dan data uji yang disetujui untuk UAT; jangan memakai data pribadi nyata.

## 2. Fitur dan Langkah Utama

| Fitur | Langkah ringkas | Dampak tindakan |
|---|---|---|
| Kelola Akses User | Buka **Kelola Akses User**, cari pegawai, isi identifier Keycloak, pilih role internal, lalu simpan | Mengubah kemampuan user di SIMPEG dan menghasilkan Audit Log |
| Role & Permission | Buka **Role & Permission**, periksa default dan permission efektif, ubah hanya berdasarkan keputusan yang disetujui | Permission matrix mengatur grant/revoke; role bukan hard authorization contract dan salah konfigurasi dapat mengunci alur operasional |
| Switch Role | Bila memiliki `users.switch_role`, pilih target lebih rendah yang diizinkan lalu revert setelah selesai | Menyimulasikan role efektif tanpa mengganti identitas, `employee_id`, ownership, atau scope aktor asli; seluruh aksi teraudit |
| Data Master | Buka **Data Master**, pilih referensi, tambah/ubah/nonaktifkan sesuai dependency | Mengubah pilihan kanonis yang dipakai form, perhitungan, dan laporan |
| Data Pegawai | Cari pegawai, tambah/ubah data utama, tambahkan riwayat, dan kelola status langsung atau terjadwal | Mutasi status mempertahankan Employee, membuat histori append-only/audit, serta memengaruhi akses dan EWS ketika efektif |
| Import Pegawai | Unduh template, unggah CSV/Excel, petakan kolom, validasi, periksa preview, lalu jalankan import | Dapat membuat banyak pegawai; baris import diklasifikasikan imported/skipped/failed |
| Konfigurasi Approval Cuti | Buka **Konfigurasi Approval Cuti**, tetapkan Verifikator, Atasan Langsung, dan PYBMC sesuai urutan kanonis | Hanya pengajuan baru yang memakai konfigurasi baru; snapshot pengajuan berjalan tidak berubah |
| Channel Notifikasi | Buka **Channel Notifikasi**, periksa kill-switch dan kebijakan event | Mengaktifkan atau menonaktifkan intent per channel; tidak mengaktifkan provider yang belum tersedia |
| Konfigurasi EWS | Buka **Konfigurasi EWS**, ubah parameter yang disetujui, lalu simpan | Memengaruhi alert yang dibentuk scheduler dan penerima notifikasi |
| Audit Log | Buka **Audit Log**, filter aktivitas, lalu buka detail | Akses baca untuk traceability; record audit tidak boleh diubah atau dihapus |
| Laporan/Export | Pilih filter dan kolom aman, periksa preview, lalu unduh Excel atau PDF | Menghasilkan salinan data; NIK/No. KK tidak boleh masuk export tanpa kebutuhan dan persetujuan eksplisit |
| Reporting Statistik Kepegawaian | Buka halaman reporting, pilih filter yang diizinkan, lalu baca chart/agregat | Menampilkan statistik teragregasi sesuai scope; bukan Data Master atau pengganti export detail |

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

1. Pastikan pegawai, Verifikator, Atasan Langsung, dan PYBMC aktif.
2. Atur rantai `0..N Verifikator → Atasan Langsung → PYBMC`.
3. Ketua Tim, bila digunakan, dicatat sebagai verifikator.
4. Bila kelompok Verifikator kosong, pastikan preview dimulai dari Atasan Langsung tanpa label placeholder.
5. Bila Atasan Langsung dan PYBMC adalah orang yang sama, pastikan preview tetap memperlihatkan dua peran/tahap yang membutuhkan dua tindakan.
6. Simpan dan periksa preview rantai.
7. Buat pengajuan uji baru untuk membuktikan runtime.
8. Jangan mengubah snapshot pengajuan yang sudah berjalan.

## 5. Batas Akses dan Larangan

- Jangan memberi akses berdasarkan role claim Keycloak.
- Jangan membuat login manual produksi.
- Jangan melakukan hard delete pegawai.
- Jangan menggunakan Data Backup/Data Nonaktif; seluruh lifecycle ada pada filter status Data Pegawai.
- Reaktivasi tetap memerlukan permission efektif `employees.restore`. Role Super Admin tidak menjadi bypass.
- Jangan mengandalkan raw role asal ketika switch role aktif; seluruh aksi mengikuti role/permission efektif.
- Switch Role hanya dapat dimulai oleh Super Admin atau Admin Kepegawaian dengan `users.switch_role`; Pimpinan, Kepala Bagian, dan Pegawai tetap ditolak. Jangan memilih role sama/lebih tinggi/Super Admin atau melakukan chained switch sebelum revert.
- Jangan menganggap default Super Admin sebagai alasan untuk menolak permission valid pada role lain; gunakan permission efektif dan business invariant yang terdokumentasi.
- Jangan mengedit histori kepegawaian lama; tambahkan record baru berdasarkan dokumen resmi.
- Jangan mengubah saldo cuti secara langsung; koreksi dilakukan melalui sumber pemakaian dan
  rekalkulasi yang diaudit.
- Jangan mengaktifkan WhatsApp tanpa dependency resmi.
- Jangan mengubah atau menghapus Audit Log.
- Jangan memasukkan NIK, No. KK, token, atau credential ke screenshot/evidence.

## 6. Troubleshooting

| Gejala | Pemeriksaan |
|---|---|
| User hanya dapat membuka status akun | Employee linked efektif Nonaktif; blokir route bisnis berlaku untuk seluruh role. Periksa dasar administrasi dan reaktivasi resmi bila sah |
| Reaktivasi ditolak | Periksa role efektif dan permission `employees.restore`; jangan bypass melalui raw role atau database |
| Konfigurasi cuti tidak dapat disimpan | Periksa urutan, approver aktif, tepat satu Atasan Langsung, dan PYBMC terakhir; pasangan Atasan/PYBMC yang orangnya sama tetap dua tahap |
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
