# Prosedur dan Evidence Backup, Restore, dan Rollback SIMPEG

| Field | Nilai |
|---|---|
| Terkait | Issue [LLDIKTI16/simpeg#14](https://github.com/LLDIKTI16/simpeg/issues/14) |
| Status | **Draft — drill belum dilaksanakan** |
| Environment yang diizinkan untuk draft drill | Environment uji terisolasi |
| Production action | Memerlukan persetujuan eksplisit LLDIKTI/Release Owner |

## 1. Tujuan dan Prinsip Keselamatan

Prosedur ini membuktikan bahwa data dan aplikasi dapat dipulihkan sebelum environment baru menjadi
baseline. Pembuatan dokumen bukan bukti bahwa backup, restore, atau rollback sudah berhasil.

Prinsip wajib:

- jangan menjalankan restore atau rollback destruktif pada produksi tanpa persetujuan eksplisit;
- target restore harus diidentifikasi dan diverifikasi sebagai environment uji terisolasi;
- jangan menggunakan `migrate:fresh`, `migrate:refresh`, atau `migrate:reset` pada data nyata;
- backup database dan storage harus berasal dari titik waktu yang sama atau memiliki catatan selisih;
- credential dan dump tidak disimpan dalam repository;
- NIK, No. KK, token, dan data pribadi tidak ditampilkan dalam evidence;
- operator berbeda melakukan peer-check terhadap target sebelum restore.

## 2. Keputusan yang Masih Diperlukan

| Keputusan | Owner | Status | Evidence |
|---|---|---|---|
| Lokasi dan retensi backup | LLDIKTI | Belum Diputuskan | — |
| Encryption dan akses backup | LLDIKTI | Belum Diputuskan | — |
| RPO | LLDIKTI/Release Owner | Belum Diputuskan | — |
| RTO | LLDIKTI/Release Owner | Belum Diputuskan | — |
| Operator produksi | LLDIKTI | Belum Ditunjuk | — |
| Strategi rollback schema | LLDIKTI + tim aplikasi | Belum Disetujui | — |
| Strategi rollback image | LLDIKTI + tim aplikasi | Belum Disetujui | — |

Sampai keputusan tersedia, dokumen ini hanya boleh dipakai untuk menyiapkan dan menjalankan drill
pada environment uji yang disetujui.

## 3. Preflight Backup

| Pemeriksaan | Nilai/hasil | Status | Pemeriksa |
|---|---|---|---|
| Environment sumber | — | Belum | — |
| Exact SHA aplikasi | — | Belum | — |
| Image digest | — | Belum | — |
| PostgreSQL source version | — | Belum | — |
| Database name | — | Belum | — |
| Storage root yang termasuk | — | Belum | — |
| Ruang penyimpanan cukup | — | Belum | — |
| Target backup absolut terverifikasi | — | Belum | — |
| Encryption/access control siap | — | Belum | — |
| Waktu konsistensi disetujui | — | Belum | — |

## 4. Pembuatan Backup

Operator menjalankan prosedur infrastruktur yang disetujui untuk:

1. menetapkan ID backup dan waktu mulai;
2. menghentikan atau mengendalikan mutasi sesuai strategi konsistensi;
3. membuat backup PostgreSQL dalam format yang mendukung restore teruji;
4. membuat backup storage privat aplikasi;
5. membuat checksum;
6. mencatat ukuran, durasi, exit status, dan lokasi aman;
7. mengaktifkan kembali layanan hanya setelah konsistensi dikonfirmasi.

Perintah final tidak ditetapkan di sini sampai topology, container name, database role, storage,
serta kebijakan LLDIKTI dikonfirmasi. Perintah lokal pada README SIMPEG tidak boleh diasumsikan
sebagai prosedur produksi.

### Record Backup

| Field | Nilai |
|---|---|
| Backup ID | Belum diisi |
| Environment sumber | Belum diisi |
| Exact SHA/image digest | Belum diisi |
| PostgreSQL | Belum diisi |
| Mulai/selesai | Belum diisi |
| Database artifact reference | Belum diisi |
| Storage artifact reference | Belum diisi |
| Checksum reference | Belum diisi |
| Ukuran | Belum diisi |
| Operator/peer checker | Belum diisi |
| Status | Belum Dilaksanakan |

## 5. Preflight Restore

Sebelum restore:

- [ ] target adalah environment uji terisolasi;
- [ ] nama host/database/volume target diperiksa oleh dua orang;
- [ ] target bukan production dan bukan workspace/source repository;
- [ ] versi PostgreSQL kompatibel atau strategi upgrade disetujui;
- [ ] artifact dan checksum backup valid;
- [ ] secret target tersedia melalui kanal aman;
- [ ] aplikasi/worker/scheduler target dihentikan agar tidak menulis selama restore;
- [ ] target kosong atau penggantian datanya telah disetujui secara eksplisit;
- [ ] rencana pembersihan data uji tersedia.

## 6. Restore dan Validasi Data

Urutan restore:

1. catat keadaan target sebelum tindakan;
2. hentikan app, queue, dan scheduler target;
3. restore database menggunakan prosedur yang disetujui;
4. restore storage privat ke target yang sudah diverifikasi;
5. validasi checksum/manifest storage;
6. jalankan pemeriksaan schema dan constraint;
7. mulai aplikasi tanpa menerima traffic umum;
8. verifikasi data dan alur dengan query agregat yang tidak mengekspos PII;
9. aktifkan queue dan scheduler setelah schema dinyatakan kompatibel;
10. simpan evidence hasil.

### Matriks Validasi Restore

| ID | Pemeriksaan | Expected result | Actual result | Status | Evidence |
|---|---|---|---|---|---|
| RST-01 | Checksum artifact | Cocok dengan record backup | — | Belum | — |
| RST-02 | PostgreSQL dapat dibuka | Koneksi berhasil tanpa error critical | — | Belum | — |
| RST-03 | Migration status | Tidak ada migration tak terduga | — | Belum | — |
| RST-04 | Jumlah tabel/constraint | Sesuai manifest sumber | — | Belum | — |
| RST-05 | Row count agregat | Sesuai toleransi/titik waktu backup | — | Belum | — |
| RST-06 | User–employee mapping | Relasi valid tanpa orphan | — | Belum | — |
| RST-07 | Dokumen/storage | Manifest cocok; akses hanya berotorisasi | — | Belum | — |
| RST-08 | Audit Log | Record tersedia dan immutable | — | Belum | — |
| RST-09 | Aplikasi | Login dan halaman utama berfungsi | — | Belum | — |
| RST-10 | Queue/scheduler | Berfungsi tanpa duplikasi/error schema | — | Belum | — |

## 7. Trigger Rollback

Rollback dipertimbangkan apabila terjadi salah satu kondisi berikut:

- migration gagal atau menghasilkan kehilangan/integrity error;
- aplikasi mengalami error critical pada alur utama;
- queue/scheduler menghasilkan kegagalan berulang atau duplikasi data;
- akses/otorisasi menjadi lebih longgar dari kontrak;
- dokumen/storage tidak dapat diakses secara aman;
- restore/verifikasi data tidak lulus;
- performance degradation menghambat layanan utama;
- release owner menetapkan `NO-GO`.

## 8. Rencana Rollback Kandidat

Rencana final wajib disesuaikan dengan perubahan release dan disetujui sebelum deploy.

1. hentikan traffic/mutasi sesuai keputusan incident commander;
2. hentikan queue dan scheduler versi kandidat;
3. catat error, exact SHA, image digest, dan waktu keputusan;
4. pilih strategi rollback yang sudah disetujui:
   - kembali ke image aplikasi sebelumnya tanpa rollback data; atau
   - pulihkan database/storage dari backup bila perubahan data tidak kompatibel;
5. jangan menjalankan rollback migration generik tanpa analisis migration tertentu;
6. jalankan image baseline sebelumnya yang digest-nya sudah dicatat;
7. verifikasi aplikasi, migration/schema, queue, scheduler, storage, dan alur utama;
8. buka traffic hanya setelah release owner menyetujui;
9. catat actual recovery time dan data loss window;
10. buat tindak lanjut defect dan post-incident review.

## 9. Rollback Drill Record

| Field | Nilai |
|---|---|
| Drill ID | Belum diisi |
| Environment | Belum diisi |
| Skenario kegagalan | Belum diisi |
| Baseline sebelum kandidat | Belum diisi |
| Kandidat yang dibatalkan | Belum diisi |
| Waktu keputusan rollback | Belum diisi |
| Waktu layanan pulih | Belum diisi |
| Actual RTO/RPO | Belum diisi |
| Operator/peer checker | Belum diisi |
| Evidence | Belum diisi |
| Status | Belum Dilaksanakan |

## 10. Exit Criteria Recovery

- [ ] keputusan infrastruktur pada §2 selesai;
- [ ] backup database dan storage berhasil dengan checksum;
- [ ] restore pada environment uji berhasil;
- [ ] seluruh validasi RST-01 sampai RST-10 lulus;
- [ ] rollback drill berhasil;
- [ ] actual RTO/RPO dicatat dan diterima;
- [ ] prosedur final direview LLDIKTI/Release Owner;
- [ ] evidence ditautkan pada checklist go/no-go.

## 11. Referensi

- [Baseline dan Verifikasi Environment](Baseline-dan-Verifikasi-Environment.md)
- [Checklist Go/No-Go](Checklist-Go-No-Go.md)
- [Paket Eksekusi Issue #14](../Issue-14-UAT-Release-Readiness.md)
