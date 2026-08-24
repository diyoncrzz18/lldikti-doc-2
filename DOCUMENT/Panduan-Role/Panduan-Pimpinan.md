# Panduan Penggunaan — Pimpinan

| Field | Nilai |
|---|---|
| Role internal | `pimpinan` |
| Status | **Draft — belum diterima Kepegawaian** |
| Cakupan | Monitoring organisasi, keputusan akhir cuti, EWS, dan laporan read-only |

## 1. Prasyarat

- Akun sudah dipetakan ke pegawai aktif dengan role internal `pimpinan`.
- Pegawai Pimpinan ditetapkan sebagai PYBMC/final approver sesuai konfigurasi yang berlaku.
- Pengajuan hanya muncul setelah tahap sebelumnya selesai dan Pimpinan menjadi approver aktif.

## 2. Fitur dan Langkah Utama

| Fitur | Langkah ringkas | Dampak tindakan |
|---|---|---|
| Dashboard Pimpinan | Buka `/pimpinan/dashboard` dan periksa ringkasan organisasi | Menampilkan agregat organisasi tanpa memberi hak mutasi data pegawai |
| Data Pegawai | Gunakan daftar/filter dan buka detail pegawai | Akses read-only sesuai scope dan masking; tidak mengubah data utama/histori |
| Persetujuan Cuti | Buka `/pimpinan/cuti`, cari pengajuan aktif, baca detail, lalu pilih keputusan | Keputusan final dapat memotong saldo, menghasilkan dokumen, notifikasi, dan audit |
| EWS | Buka EWS organisasi dan filter alert | Memantau kondisi organisasi; EWS bukan keputusan otomatis |
| Laporan | Buka laporan nominatif/kepangkatan, gunakan filter, periksa preview, dan unduh | Menghasilkan salinan data fixed-format sesuai batas akses |
| Notifikasi | Buka inbox, pilih notifikasi, lalu tandai dibaca | Mengubah status baca milik user dan mengarahkan ke record terkait |

## 3. Alur Keputusan Akhir Cuti

1. Buka `/pimpinan/cuti`.
2. Periksa ringkasan pengajuan yang menunggu keputusan Anda.
3. Cari dan buka pengajuan.
4. Periksa pegawai, jenis cuti, periode, hari kerja, alasan, saldo, lampiran, dan timeline.
5. Pastikan tahap sebelumnya selesai dan Anda adalah approver aktif.
6. Pilih salah satu keputusan resmi.
7. Untuk selain `Disetujui`, isi alasan yang jelas.
8. Konfirmasi tindakan.
9. Periksa status akhir, notifikasi, dokumen, dan Audit Log.

Dampak keputusan:

| Keputusan | Dampak |
|---|---|
| `Disetujui` | Menyelesaikan chain, memotong saldo tahunan sesuai hasil sistem, membuat dokumen, dan memberi notifikasi |
| `Perubahan` | Mengembalikan pengajuan untuk diperbaiki; saldo tidak dipotong final |
| `Ditangguhkan` | Menyimpan alasan penangguhan; saldo tidak dipotong final |
| `Tidak Disetujui` | Menutup pengajuan tanpa pemotongan saldo dan melepaskan alokasi |

## 4. Batas Akses dan Larangan

- Detail pegawai bersifat read-only; jangan mencari jalur mutasi di luar menu resmi.
- Keputusan hanya boleh dilakukan ketika user menjadi approver aktif.
- Jangan menggunakan istilah `Ditolak`; label resminya `Tidak Disetujui`.
- Jangan membuat keputusan berdasarkan EWS saja; EWS adalah indikator untuk verifikasi administratif.
- Jangan mengekspor data kontak pribadi atau identitas sensitif yang tidak diperlukan.
- Jangan membagikan lampiran cuti kepada pihak di luar kewenangan.

## 5. Troubleshooting

| Gejala | Pemeriksaan |
|---|---|
| Pengajuan tidak muncul | Periksa tahap sebelumnya, snapshot approver, status pengajuan, dan akun pegawai Pimpinan |
| Tombol keputusan tidak ada | Pastikan Anda approver aktif dan pengajuan belum diputus |
| Saldo belum berubah | Saldo hanya dipotong setelah keputusan final `Disetujui` |
| Laporan kosong | Periksa periode, filter, status pegawai, dan scope data |

## 6. Penerimaan Panduan

| Field | Nilai |
|---|---|
| Exact SHA yang diuji | Belum diisi |
| Tanggal UAT | Belum diisi |
| Pemberi keputusan | Belum diisi |
| Status | Perlu Tindak Lanjut — UAT belum dilaksanakan |
| Evidence | Belum ada |
