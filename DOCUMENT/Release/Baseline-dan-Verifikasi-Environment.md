# Baseline dan Verifikasi Environment Kandidat SIMPEG

| Field | Nilai |
|---|---|
| Terkait | Issue [LLDIKTI16/simpeg#14](https://github.com/LLDIKTI16/simpeg/issues/14) |
| Status | **Draft — environment kandidat belum ditetapkan** |
| Evidence backend/environment | Jordan Sutarto |
| Release gate | Adriel Walintukan |

## 1. Tujuan

Dokumen ini mencatat dependency environment dan membuktikan bahwa satu kombinasi exact source,
image/runtime, PostgreSQL, queue, serta scheduler layak dijadikan baseline. Image atau versi baru
tidak menjadi baseline hanya karena tersedia pada branch atau registry.

## 2. Dependency Eksternal

Dependency berikut harus diberikan atau dikonfirmasi oleh LLDIKTI:

- image/digest PHP/container kandidat;
- versi PostgreSQL kandidat;
- registry dan kebijakan penarikan image;
- konfigurasi deployment final;
- pemilik environment dan jendela perubahan;
- lokasi backup dan prosedur recovery yang disetujui;
- credential/secret melalui kanal aman, bukan repository;
- target RPO/RTO dan kewenangan go/no-go.

Status dependency:

| Dependency | Owner | Status | Evidence/keputusan |
|---|---|---|---|
| Image PHP/container kandidat | LLDIKTI | Belum Diterima | — |
| PostgreSQL kandidat | LLDIKTI | Belum Diterima | — |
| Deployment final | LLDIKTI/Release Owner | Belum Ditetapkan | — |
| RPO/RTO | LLDIKTI/Release Owner | Belum Ditetapkan | — |

## 3. Inventaris Kandidat

Isi semua field sebelum verifikasi. Nilai secret tidak boleh dicatat.

| Komponen | Nilai kandidat | Sumber evidence | Diverifikasi oleh | Status |
|---|---|---|---|---|
| Repository | `LLDIKTI16/simpeg` | — | — | Belum |
| Branch/tag | — | — | — | Belum |
| Exact commit SHA | — | — | — | Belum |
| Image name | — | — | — | Belum |
| Image digest | — | — | — | Belum |
| PHP | — | — | — | Belum |
| Laravel | — | — | — | Belum |
| PostgreSQL | — | — | — | Belum |
| Podman/Compose | — | — | — | Belum |
| Nginx | — | — | — | Belum |
| Queue connection | — | Referensi aman tanpa credential | — | Belum |
| Scheduler mode | — | — | — | Belum |
| Storage mode | — | — | — | Belum |
| Timezone aplikasi | `Asia/Makassar` | `php artisan about` | — | Belum |
| Tanggal build/deploy | — | — | — | Belum |

## 4. Gate Sebelum Kandidat Diuji

- [ ] exact SHA dan image digest terkunci;
- [ ] perubahan migration diinventarisasi;
- [ ] dampak schema/data dan rollback dipahami;
- [ ] backup database dan storage tersedia;
- [ ] restore target terpisah tersedia;
- [ ] environment menggunakan PostgreSQL, bukan SQLite;
- [ ] secret disediakan melalui mekanisme environment yang disetujui;
- [ ] queue dan scheduler tidak berjalan pada schema lama selama cutover;
- [ ] akun/data UAT aman tersedia;
- [ ] operator dan pemberi keputusan tersedia.

Jika salah satu gate belum terpenuhi, kandidat belum boleh dijadikan baseline.

## 5. Verifikasi Teknis

Perintah berikut dijalankan dari root repository SIMPEG pada environment kandidat. Sesuaikan wrapper
container dengan deployment resmi tanpa menyalin credential ke output.

### 5.1 Identitas Runtime

```bash
git rev-parse HEAD
podman compose ps
podman compose exec app php artisan about --only=environment
podman compose exec app php artisan migrate:status
```

Evidence yang disimpan:

- exact SHA;
- status container;
- versi runtime;
- environment, timezone, dan debug mode;
- seluruh migration berstatus `Ran`.

### 5.2 Aplikasi

| Pemeriksaan | Expected result | Actual result | Status | Evidence |
|---|---|---|---|---|
| Landing/login | Redirect autentikasi sesuai environment | — | Belum | — |
| Health HTTP utama | Tidak ada 5xx kritis | — | Belum | — |
| Asset CSS/JS | Termuat tanpa 404 | — | Belum | — |
| Storage terproteksi | Dokumen hanya melalui route berotorisasi | — | Belum | — |
| Log aplikasi | Tidak ada error critical baru | — | Belum | — |

### 5.3 Queue

| Pemeriksaan | Expected result | Actual result | Status | Evidence |
|---|---|---|---|---|
| Worker hidup pada image kandidat | Container/process sehat | — | Belum | — |
| Job uji aman diproses | Job selesai tanpa duplikasi | — | Belum | — |
| Retry | Sesuai konfigurasi yang disetujui | — | Belum | — |
| Failed jobs | Tidak ada kegagalan critical yang belum dijelaskan | — | Belum | — |
| Log worker | Tidak ada schema mismatch atau credential exposure | — | Belum | — |

### 5.4 Scheduler

```bash
podman compose exec app php artisan schedule:list
```

| Pemeriksaan | Expected result | Actual result | Status | Evidence |
|---|---|---|---|---|
| Daftar schedule | Task wajib terdaftar | — | Belum | — |
| Scheduler process | Hidup pada image kandidat | — | Belum | — |
| Eksekusi uji | Selesai tanpa duplikasi/error critical | — | Belum | — |
| Timezone | `Asia/Makassar` | — | Belum | — |

## 6. Smoke Alur Utama

Gunakan data sintetis/staging. Jangan menjalankan mutasi uji pada produksi tanpa persetujuan.

| ID | Role/alur | Expected result | Actual result | Status | Evidence |
|---|---|---|---|---|---|
| ENV-01 | Super Admin login dan dashboard | Role/menu sesuai, HTTP 200 | — | Belum | — |
| ENV-02 | Admin Kepegawaian data pegawai | List/filter/detail berfungsi sesuai permission | — | Belum | — |
| ENV-03 | Pegawai membuat pengajuan cuti | Validasi, snapshot, alokasi, audit, dan notifikasi terbentuk | — | Belum | — |
| ENV-04 | Verifikator/Kepala Bagian/Pimpinan | Chain berjalan berurutan sampai keputusan final | — | Belum | — |
| ENV-05 | Saldo cuti | Dipotong hanya setelah final `Disetujui` | — | Belum | — |
| ENV-06 | EWS | Scheduler/dedup/scope/notifikasi sesuai | — | Belum | — |
| ENV-07 | Laporan/export | Preview dan berkas dapat dibuka tanpa data sensitif berlebih | — | Belum | — |
| ENV-08 | Audit | Mutasi penting tercatat dan immutable | — | Belum | — |

## 7. Smoke Browser dan Performa

Untuk setiap halaman user-visible yang diuji, catat:

- URL dan role;
- waktu muat dingin/hangat bila diukur;
- interaksi utama;
- status console error;
- request background/polling;
- lag atau payload besar;
- ukuran viewport desktop dan mobile yang diperiksa.

| URL/role | Interaksi | Console | Lag/polling | Status | Evidence |
|---|---|---|---|---|---|
| — | — | — | — | Belum | — |

## 8. Hasil Kandidat

| Field | Nilai |
|---|---|
| Exact SHA | Belum diisi |
| Image digest | Belum diisi |
| PostgreSQL | Belum diisi |
| Tanggal verifikasi | Belum diisi |
| Verifikator | Belum diisi |
| Critical/major defect | Belum dinilai |
| Status | **Belum Menjadi Baseline** |
| Alasan | Dependency dan verifikasi kandidat belum lengkap |

## 9. Referensi

- [Paket Eksekusi Issue #14](../Issue-14-UAT-Release-Readiness.md)
- [Backup, Restore, dan Rollback](Backup-Restore-dan-Rollback.md)
- [Checklist Go/No-Go](Checklist-Go-No-Go.md)
- [Panduan Penulisan Kode SIMPEG](../PRD-DLL/Panduan-Penulisan-Kode-SIMPEG.md)
