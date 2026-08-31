# Rencana dan Register UAT SIMPEG Fase 1

| Field | Nilai |
|---|---|
| Terkait | Issue [LLDIKTI16/simpeg#14](https://github.com/LLDIKTI16/simpeg/issues/14) |
| Status | **Draft — UAT belum dilaksanakan** |
| Target | Akhir Agustus 2026 |
| Koordinator | Dion Kobi |
| QA/evidence | Grantly Sorongan |
| Release gate | Adriel Walintukan |

## 1. Tujuan dan Batas

UAT membuktikan bahwa kelompok revisi yang sudah memenuhi Definition of Done dapat digunakan dan
diterima oleh pihak Kepegawaian. UAT bukan pengganti automated test, code review, security review,
atau verifikasi environment. Kelompok yang belum memenuhi DoD tidak boleh dijadwalkan sebagai
kandidat penerimaan.

Dokumen ini tidak mengesahkan penerimaan apa pun. Tabel hasil hanya diisi setelah sesi berlangsung
dan dikonfirmasi oleh pihak yang berwenang.

## 2. Syarat Kelompok Siap Dijadwalkan

Semua syarat berikut wajib dipenuhi:

- [ ] scope kelompok dan issue/PR pembentuknya jelas;
- [ ] seluruh PR yang diperlukan sudah merge pada branch kandidat;
- [ ] exact commit SHA kandidat dicatat;
- [ ] automated test yang relevan lulus;
- [ ] review critical/major selesai;
- [ ] tidak ada blocker keamanan atau data integrity;
- [ ] data dan akun UAT tersedia tanpa memakai data pribadi nyata;
- [ ] skenario, expected result, dan owner tersedia;
- [ ] environment kandidat lolos preflight minimum;
- [ ] perubahan user-visible memiliki catatan smoke performance dan console error;
- [ ] rollback kelompok dipahami sebelum sesi.

Setelah semua syarat dipenuhi, koordinator meminta jadwal Zoom secepatnya dan tidak menunggu rapat
rutin Jumat.

## 3. Usulan Pengelompokan Awal

Pengelompokan ini adalah draft untuk koordinasi. Daftar final wajib disesuaikan dengan issue/PR yang
benar-benar masuk release candidate.

| ID | Kelompok revisi | Cakupan utama | Owner teknis | Status readiness |
|---|---|---|---|---|
| K-01 | Autentikasi dan akses | Keycloak mapping, role internal, permission, switch role, session | Owner PR terkait | Belum Dinilai |
| K-02 | Data pegawai | Data utama, histori append-only, dokumen, import, data master | Owner PR terkait | Belum Dinilai |
| K-03 | Cuti | Pengajuan, chain approval, saldo/pemakaian, dokumen, laporan | Owner PR terkait | Belum Dinilai |
| K-04 | EWS dan notifikasi | Scheduler, alert, follow-up, in-app, email, channel policy | Owner PR terkait | Belum Dinilai |
| K-05 | Dashboard, laporan, dan audit | Dashboard per role, export, masking, audit immutable | Owner PR terkait | Belum Dinilai |
| K-06 | Environment dan recovery | Image, PostgreSQL, migration, queue, scheduler, backup/restore, rollback | Jordan/Adriel | Menunggu Dependency Eksternal |

## 4. Register Kelompok Revisi

Tambahkan satu baris untuk setiap kelompok yang benar-benar diajukan. `Exact SHA` tidak boleh
diganti dengan nama branch karena branch dapat berpindah.

| ID | Issue/PR | Exact SHA | DoD | QA owner | Tanggal siap | Jadwal Zoom | Status jadwal | Evidence readiness |
|---|---|---|---|---|---|---|---|---|
| — | — | — | Belum | — | — | — | Belum Dijadwalkan | — |

Status jadwal yang diperbolehkan:

- `Belum Dijadwalkan`
- `Menunggu Konfirmasi LLDIKTI`
- `Terjadwal`
- `Selesai`
- `Dijadwalkan Ulang`

## 5. Agenda Sesi Zoom

Setiap sesi menggunakan urutan berikut:

1. konfirmasi peserta dan pemberi keputusan;
2. catat environment, exact SHA, dan data uji;
3. jelaskan scope dan batas kelompok;
4. jalankan happy path;
5. jalankan validasi akses/negative path yang penting;
6. tunjukkan dampak mutasi, audit, dan notifikasi bila relevan;
7. catat feedback tanpa mengubah kontrak secara lisan;
8. klasifikasikan defect dan owner tindak lanjut;
9. minta keputusan penerimaan per kelompok;
10. sepakati jadwal retest jika diperlukan.

## 6. Skenario Wajib Addendum Evaluasi 31 Agustus 2026

> Skenario berikut belum dijalankan. Skenario hanya dapat masuk sesi UAT setelah implementasi, review, automated test relevan, dan preflight environment telah lulus. Evidence sebelum addendum tidak dapat dipakai kembali tanpa retest terhadap exact SHA kandidat.

| ID | Kelompok | Skenario | Expected result | Evidence minimum |
|---|---|---|---|---|
| UAT-CUT-31-01 | Cuti | Buat chain dengan nol, satu, dan lebih dari satu Verifikator | Urutan runtime selalu `0..n Verifikator → Atasan Langsung → PYBMC`; jika nol Verifikator, Atasan Langsung menjadi tahap pertama tanpa placeholder kosong | Screenshot chain/snapshot, test PostgreSQL, audit submit |
| UAT-CUT-31-02 | Cuti | Tetapkan Atasan Langsung dan PYBMC ke employee yang sama | Dua tahap, dua tindakan, dua event audit, dan dua entri timeline tetap terjadi | Rekaman langkah, audit masked, hasil test regression |
| UAT-CUT-31-03 | Cuti | Pegawai membatalkan atau merevisi sebelum tindakan approval | Hanya pemohon yang dapat bertindak; request/snapshot tidak dihapus, reservasi diperbarui atomik, audit tercatat | Request/response atau screenshot, ledger, audit |
| UAT-CUT-31-04 | Cuti | Admin Kepegawaian menangguhkan cuti yang telah final `Disetujui` | Alasan wajib; histori tetap ada; koreksi/replay ledger satu kali; Pegawai dapat mengajukan lagi setelah tidak ada pengajuan aktif | Ledger before/after, audit, detail request |
| UAT-CUT-31-05 | Saldo historis | Catat Cuti di Luar SIMPEG lalu buka ringkasan pemakaian | Fakta historis menjadi sumber pemakaian; ringkasan Catat Pemakaian Tahunan read-only; tidak ada hitung ganda | UI smoke, ledger, test anti duplikasi/overlap |
| UAT-CUT-31-06 | Dokumen cuti | Finalkan cuti dan buka PDF/QR | PDF memuat Nama, Jabatan aktual/terkini, dan Peran setiap tahap; QR serta otorisasi dokumen tetap benar | PDF tersanitasi, verifikasi QR, authorization test |
| UAT-CUT-31-07 | Pemulihan downtime | Setelah layanan pulih, catat cuti yang telah diproses dan disetujui manual saat downtime | Fakta final tercatat satu kali; saldo/rollover sinkron; tidak ada approval aktif atau reservasi baru; duplikasi/overlap ditolak | UI smoke, ledger before/after, audit, test PostgreSQL |
| UAT-EMP-31-01 | Dokumen pegawai | Uji PNS, CPNS, lalu transisi CPNS→PNS | PNS memerlukan SK Pengangkatan PNS; CPNS memerlukan SK Pengangkatan CPNS; transisi menandai belum lengkap sampai SK PNS tersedia | Screenshot status kelengkapan, upload/audit, RBAC denial |
| UAT-REP-31-01 | Reporting | Buka Reporting Statistik dengan data/role berbeda | Halaman terpisah dari dashboard/export; chart golongan, jenis jabatan, jabatan, unit, dan jenis kepegawaian mengikuti scope dan empty state | Screenshot desktop/tablet/mobile, test scope/query, console bersih |

Catatan Open Question harus dicatat pada sesi UAT, bukan diasumsikan oleh tester: batas pembatalan setelah Verifikator bertindak masih menunggu keputusan LLDIKTI.

## 7. Template Notulen dan Hasil Skenario

Salin bagian ini untuk setiap sesi.

### Sesi UAT `<ID sesi>`

| Field | Nilai |
|---|---|
| Kelompok revisi | `<ID dan nama>` |
| Tanggal/waktu | `<Asia/Makassar>` |
| Media | Zoom |
| Environment | `<nama environment>` |
| Exact SHA | `<40-character SHA>` |
| Image/runtime/database | `<versi atau digest>` |
| Presenter | `<nama>` |
| QA pencatat | `<nama>` |
| Pemberi keputusan Kepegawaian | `<nama/jabatan>` |
| Peserta lain | `<nama/jabatan>` |

| Skenario | Expected result | Actual result | Status | Evidence | Catatan |
|---|---|---|---|---|---|
| `<ID skenario>` | `<hasil yang diharapkan>` | `<hasil aktual>` | Pass/Fail/Blocked | `<tautan aman>` | `<catatan>` |

### Temuan dan Tindak Lanjut

| ID | Severity | Deskripsi | Owner | Target | Issue/PR tindak lanjut | Status retest |
|---|---|---|---|---|---|---|
| — | — | — | — | — | — | Belum Diretest |

## 8. Register Penerimaan Kepegawaian

Hanya gunakan tiga status keputusan resmi berikut:

- `Diterima`
- `Ditolak`
- `Perlu Tindak Lanjut`

| Kelompok | Tanggal keputusan | Pemberi keputusan | Status | Ringkasan alasan | Evidence notulen | Tindak lanjut/owner | Tanggal retest |
|---|---|---|---|---|---|---|---|
| — | — | — | Perlu Tindak Lanjut | UAT belum dilaksanakan | — | Koordinator menjadwalkan sesi setelah DoD | — |

Keputusan tidak boleh diisi berdasarkan kesimpulan implementor. Bila pemberi keputusan belum hadir
atau belum memberikan konfirmasi eksplisit, status tetap `Perlu Tindak Lanjut` dengan alasan yang
sesuai.

## 9. Gate Panduan Pengguna

Setelah kelompok terkait berstatus `Diterima`:

1. tandai fitur yang diterima pada panduan role terkait;
2. selaraskan langkah dengan exact release candidate;
3. catat prasyarat, dampak tindakan, dan batas akses;
4. lakukan review UI dan Bahasa Indonesia;
5. minta penerimaan panduan oleh Kepegawaian;
6. ubah status panduan dari `Draft` menjadi `Diterima` hanya setelah ada evidence.

## 10. Evidence Handling

- Masking wajib diterapkan pada screenshot dan log.
- Jangan unggah dump database, token, credential, NIK, No. KK, atau data pribadi nyata.
- Video/rekaman yang tidak dapat disimpan di repository direferensikan dengan ID penyimpanan dan
  kontrol akses.
- Evidence harus dapat dikaitkan dengan satu exact SHA dan satu sesi.
- Perubahan setelah sesi memerlukan retest; evidence lama tidak boleh dipakai untuk SHA baru tanpa
  analisis dampak.

## 11. Exit Criteria UAT

- [ ] seluruh kelompok release candidate memiliki hasil UAT;
- [ ] setiap kelompok memiliki keputusan resmi;
- [ ] semua defect critical/major ditutup atau menghasilkan keputusan no-go;
- [ ] retest memiliki evidence baru;
- [ ] lima panduan role diselaraskan dengan fitur yang diterima;
- [ ] seluruh skenario addendum evaluasi 31 Agustus yang masuk release candidate memiliki evidence retest;
- [ ] hasil UAT ditautkan pada checklist go/no-go.

## 12. Referensi

- [Paket Eksekusi Issue #14](../Issue-14-UAT-Release-Readiness.md)
- [Runbook Demo Fitur SIMPEG Fase 1](../Runbook-Demo-Fitur-SIMPEG-Fase-1.md)
- [Tracking Sprint 7](../Tracking-Sprint-1-7/Sprint-7-Stabilization-Regression-UAT.md)
- [Keputusan Evaluasi Meeting](../Keputusan-Evaluasi-Meeting-LLDIKTI-15-Agustus-2026.md)
- [Keputusan Evaluasi 31 Agustus 2026](../Keputusan-Evaluasi-Meeting-LLDIKTI-31-Agustus-2026.md)
