# Panduan Penggunaan — Pegawai

| Field | Nilai |
|---|---|
| Role internal | `pegawai` |
| Status | **Draft — belum diterima Kepegawaian** |
| Cakupan | Data pribadi read-only, pengajuan cuti, saldo, notifikasi, dan EWS pribadi |

## 1. Prasyarat

- Akun Keycloak sudah dipetakan ke satu pegawai aktif.
- Role internal user adalah `pegawai`.
- Kepala Bagian dan approval chain sudah dikonfigurasi.
- Saldo/pemakaian cuti yang diperlukan sudah tersedia dan periode pengajuan valid.

## 2. Fitur dan Langkah Utama

| Fitur | Langkah ringkas | Dampak tindakan |
|---|---|---|
| Dashboard Pribadi | Buka `/dashboard` | Menampilkan ringkasan profil, saldo, pengajuan, EWS, dan notifikasi milik sendiri |
| Profil Saya | Buka `/dashboard/profil` | Akses baca data sendiri; tidak mengubah data kepegawaian pada Fase 1 |
| Pengajuan Cuti | Buka `/dashboard/cuti/create`, isi form, periksa hari kerja/saldo/chain, lalu kirim | Membuat pengajuan, mengalokasikan saldo sementara, memberi notifikasi approver, dan mencatat audit |
| Riwayat Cuti | Buka `/dashboard/cuti`, gunakan filter, lalu buka detail | Menampilkan status, timeline, alasan keputusan, lampiran, dan dokumen milik sendiri |
| Saldo Cuti Saya | Buka `/dashboard/cuti/saldo` | Menampilkan hak, pemakaian, alokasi, dan sisa hasil perhitungan sistem |
| Notifikasi | Buka `/notifications`, pilih notifikasi, lalu tandai dibaca | Mengubah status baca notifikasi milik sendiri dan membuka record terkait |
| EWS Pribadi | Buka EWS pada dashboard/halaman yang tersedia | Menampilkan pengingat pribadi; bukan keputusan administrasi otomatis |

## 3. Alur Mengajukan Cuti

1. Buka `/dashboard/cuti/create`.
2. Pilih jenis cuti dan tahun saldo yang sesuai.
3. Isi tanggal mulai dan selesai.
4. Tunggu sistem menghitung hari kerja.
5. Isi alasan, alamat selama cuti, dan nomor telepon.
6. Unggah lampiran jika diwajibkan jenis cuti.
7. Periksa saldo aktual, saldo yang masih dapat diajukan, dan tahapan persetujuan.
8. Kirim pengajuan.
9. Buka detail untuk memastikan status dan tahap aktif.

Setelah dikirim, saldo belum dipotong final tetapi dapat dialokasikan agar tidak dipakai ganda.
Saldo dipotong hanya setelah keputusan final `Disetujui`.

## 4. Menangani Keputusan

| Status | Tindakan Pegawai |
|---|---|
| `Disetujui` | Periksa detail, saldo, notifikasi, dan unduh formulir bila tersedia |
| `Perubahan` | Baca alasan, perbaiki tanggal/alasan/kontak/lampiran, lalu kirim ulang melalui aksi resmi |
| `Ditangguhkan` | Baca alasan dan tunggu/tindak lanjuti sesuai arahan; saldo tidak dipotong final |
| `Tidak Disetujui` | Baca alasan; pengajuan selesai dan alokasi saldo dilepas |

## 5. Batas Akses dan Larangan

- Hanya melihat data, dokumen, cuti, notifikasi, saldo, dan EWS milik sendiri.
- Tidak mengedit data utama atau histori kepegawaian pada Fase 1.
- Tidak mengubah saldo cuti.
- Tidak melihat atau memutus pengajuan pegawai lain kecuali memiliki penugasan approver yang sah.
- Tidak mengirim ulang pengajuan tanpa menggunakan aksi resubmit resmi.
- Tidak membagikan formulir, token verifikasi, atau lampiran kepada pihak yang tidak berwenang.

## 6. Troubleshooting

| Gejala | Pemeriksaan |
|---|---|
| Form tidak dapat dibuka | Periksa mapping pegawai aktif, role, dan permission pengajuan |
| Chain belum tersedia | Hubungi Admin/Super Admin untuk memeriksa Kepala Bagian, verifikator, dan PYBMC |
| Hari kerja salah | Periksa tanggal, weekend, hari libur, dan larangan lintas tahun |
| Saldo tidak cukup | Periksa pemakaian final, alokasi pengajuan aktif, dan tahun saldo |
| Tidak dapat kirim ulang | Pastikan status `Perubahan` dan gunakan tombol resubmit pada detail pengajuan |
| Notifikasi tidak membuka record | Pastikan record milik sendiri dan sesi masih aktif |

## 7. Penerimaan Panduan

| Field | Nilai |
|---|---|
| Exact SHA yang diuji | Belum diisi |
| Tanggal UAT | Belum diisi |
| Pemberi keputusan | Belum diisi |
| Status | Perlu Tindak Lanjut — UAT belum dilaksanakan |
| Evidence | Belum ada |
