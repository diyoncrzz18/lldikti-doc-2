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

## 6. Template Notulen dan Hasil Skenario

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

## 7. Register Penerimaan Kepegawaian

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

## 8. Gate Panduan Pengguna

Setelah kelompok terkait berstatus `Diterima`:

1. tandai fitur yang diterima pada panduan role terkait;
2. selaraskan langkah dengan exact release candidate;
3. catat prasyarat, dampak tindakan, dan batas akses;
4. lakukan review UI dan Bahasa Indonesia;
5. minta penerimaan panduan oleh Kepegawaian;
6. ubah status panduan dari `Draft` menjadi `Diterima` hanya setelah ada evidence.

## 9. Evidence Handling

- Masking wajib diterapkan pada screenshot dan log.
- Jangan unggah dump database, token, credential, NIK, No. KK, atau data pribadi nyata.
- Video/rekaman yang tidak dapat disimpan di repository direferensikan dengan ID penyimpanan dan
  kontrol akses.
- Evidence harus dapat dikaitkan dengan satu exact SHA dan satu sesi.
- Perubahan setelah sesi memerlukan retest; evidence lama tidak boleh dipakai untuk SHA baru tanpa
  analisis dampak.

## 10. Exit Criteria UAT

- [ ] seluruh kelompok release candidate memiliki hasil UAT;
- [ ] setiap kelompok memiliki keputusan resmi;
- [ ] semua defect critical/major ditutup atau menghasilkan keputusan no-go;
- [ ] retest memiliki evidence baru;
- [ ] lima panduan role diselaraskan dengan fitur yang diterima;
- [ ] hasil UAT ditautkan pada checklist go/no-go.

## 11. Referensi

- [Paket Eksekusi Issue #14](../Issue-14-UAT-Release-Readiness.md)
- [Runbook Demo Fitur SIMPEG Fase 1](../Runbook-Demo-Fitur-SIMPEG-Fase-1.md)
- [Tracking Sprint 7](../Tracking-Sprint-1-7/Sprint-7-Stabilization-Regression-UAT.md)
- [Keputusan Evaluasi Meeting](../Keputusan-Evaluasi-Meeting-LLDIKTI-15-Agustus-2026.md)
