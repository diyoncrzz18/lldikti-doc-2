# Panduan Penggunaan — Atasan Langsung

> File dan role internal tetap bernama `kepala_bagian` sebagai fakta teknis yang sudah ada. Pada alur cuti, istilah bisnis yang digunakan adalah **Atasan Langsung** dan penugasan ini tidak terbatas pada pemegang jabatan struktural Kepala Bagian.

| Field | Nilai |
|---|---|
| Role internal | `kepala_bagian` |
| Status | **Draft — belum diterima Kepegawaian** |
| Cakupan | Bawahan langsung/unit, tahap approval sebagai Atasan Langsung, EWS bawahan, dan notifikasi |

## 1. Prasyarat

- Akun sudah dipetakan ke pegawai aktif dengan role internal `kepala_bagian`.
- Mapping Atasan Langsung terhadap bawahan aktif sudah benar.
- Pengajuan cuti memiliki snapshot chain dan tahap Atasan Langsung sedang aktif.

## 2. Fitur dan Langkah Utama

| Fitur | Langkah ringkas | Dampak tindakan |
|---|---|---|
| Dashboard Atasan Langsung | Buka `/kepala-bagian/dashboard` | Menampilkan ringkasan bawahan, cuti menunggu, dan EWS sesuai scope |
| Daftar Bawahan | Buka `/kepala-bagian/bawahan`, cari pegawai, lalu buka detail | Akses baca terbatas pada bawahan yang dipetakan |
| Cuti Bawahan | Buka `/kepala-bagian/cuti`, cari pengajuan aktif, baca detail, lalu pilih keputusan sebagai Atasan Langsung | Dapat meneruskan chain, meminta perubahan, menangguhkan, atau menghentikan pengajuan sesuai keputusan |
| EWS Bawahan | Buka halaman EWS role `kepala_bagian` | Memantau alert bawahan; tidak otomatis mengubah data kepegawaian |
| Notifikasi | Buka inbox dan pilih event terkait | Mengarahkan ke record yang berada dalam scope dan menandai notifikasi dibaca |

## 3. Alur Pemeriksaan Cuti Bawahan

1. Buka `/kepala-bagian/cuti`.
2. Cari berdasarkan nama, periode, status, atau alasan.
3. Buka detail pengajuan.
4. Periksa identitas, unit, jenis cuti, periode, hari kerja, alasan, lampiran, saldo, dan timeline.
5. Pastikan Anda adalah approver aktif pada tahap Atasan Langsung.
6. Pilih keputusan resmi dan isi alasan bila diperlukan.
7. Konfirmasi tindakan.
8. Periksa perpindahan tahap, notifikasi, dan Audit Log.

Jika dipilih `Disetujui` pada tahap non-final, pengajuan diteruskan ke tahap berikutnya dan saldo belum
dipotong final. Pemotongan saldo hanya terjadi setelah keputusan final `Disetujui`.

## 4. Batas Akses dan Larangan

- Hanya melihat bawahan yang berada dalam scope mapping aktif.
- Tidak mengubah data utama atau histori pegawai.
- Tidak memutus pengajuan ketika bukan approver aktif.
- Tidak menganggap tahap Atasan Langsung selalu tahap pertama; Verifikator dapat berada sebelumnya.
- Tidak memberikan keputusan final bila masih ada PYBMC setelah tahap Atasan Langsung.
- Bila Anda juga menjadi PYBMC untuk pengajuan yang sama, selesaikan tindakan Atasan Langsung terlebih dahulu. Sistem tetap menampilkan tindakan PYBMC berikutnya sebagai peran terpisah.
- Tidak menggunakan EWS sebagai dasar keputusan otomatis.
- Tidak mengunduh atau membagikan lampiran di luar kewenangan.

## 5. Troubleshooting

| Gejala | Pemeriksaan |
|---|---|
| Bawahan tidak muncul | Periksa mapping Atasan Langsung, status aktif, dan unit/penugasan efektif |
| Pengajuan tidak muncul | Periksa snapshot chain, tahap aktif, dan apakah verifikator sebelumnya sudah selesai |
| Tombol keputusan tidak tersedia | Pastikan tahap aktif milik Anda dan status pengajuan masih dapat diproses |
| EWS kosong | Periksa histori/TMT bawahan, scheduler, jenis alert, dan scope |

## 6. Penerimaan Panduan

| Field | Nilai |
|---|---|
| Exact SHA yang diuji | Belum diisi |
| Tanggal UAT | Belum diisi |
| Pemberi keputusan | Belum diisi |
| Status | Perlu Tindak Lanjut — UAT belum dilaksanakan |
| Evidence | Belum ada |
