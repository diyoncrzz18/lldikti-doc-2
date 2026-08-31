# Paket Eksekusi Issue #14 — UAT, Panduan Pengguna, dan Release Readiness

| Field | Nilai |
|---|---|
| Issue | [LLDIKTI16/simpeg#14](https://github.com/LLDIKTI16/simpeg/issues/14) |
| Target final | Akhir Agustus 2026 |
| Status paket | **Executing — belum accepted** |
| PIC utama | Dion Kobi |
| QA dan evidence | Grantly Sorongan |
| Evidence backend/environment | Jordan Sutarto |
| Input panduan UI | Adithian Gunawan |
| Release/merge gate | Adriel Walintukan |
| Terakhir diperbarui | 24 Agustus 2026 |

## 1. Tujuan

Paket ini menjadi indeks tunggal untuk mengeksekusi dan membuktikan acceptance criteria Issue #14.
Dokumen yang tersedia tidak dengan sendirinya membuktikan UAT, restore, rollback, atau keputusan
go/no-go. Status hanya boleh dinaikkan ketika bukti pelaksanaan yang dapat ditelusuri sudah tersedia.

Aturan status paket:

- `Draft`: artefak sedang disusun dan belum siap digunakan sebagai bukti.
- `Siap Diuji`: prasyarat, owner, skenario, dan environment sudah lengkap.
- `Perlu Tindak Lanjut`: pengujian sudah dilakukan tetapi masih ada gap yang harus ditutup.
- `Diterima`: pihak yang berwenang telah menerima hasil dan bukti penerimaan tercatat.
- `Ditolak`: pihak yang berwenang menolak hasil dan alasan penolakan tercatat.

## 2. Daftar Artefak

| Area | Artefak | Status saat ini | Gate berikutnya |
|---|---|---|---|
| UAT | [Rencana dan Register UAT](UAT/Rencana-dan-Register-UAT-SIMPEG.md) | Draft | Tetapkan kelompok revisi, exact SHA, jadwal Zoom, dan peserta |
| Panduan | [Indeks Panduan per Role](Panduan-Role/README.md) | Draft | Review UI, UAT per role, lalu penerimaan Kepegawaian |
| Environment | [Baseline dan Verifikasi Environment](Release/Baseline-dan-Verifikasi-Environment.md) | Draft | Terima kandidat image/PHP/PostgreSQL dari LLDIKTI |
| Recovery | [Backup, Restore, dan Rollback](Release/Backup-Restore-dan-Rollback.md) | Draft | Setujui prosedur, lakukan drill pada environment uji, lampirkan bukti |
| Release gate | [Checklist Go/No-Go](Release/Checklist-Go-No-Go.md) | Draft | Lengkapi semua evidence dan tanda tangan keputusan |

## 3. Traceability Acceptance Criteria

| # | Acceptance criterion | Artefak pembuktian | Status | Evidence aktual |
|---:|---|---|---|---|
| 1 | Zoom retest segera untuk setiap kelompok yang memenuhi DoD | Register UAT §4–§6 | Belum Lulus | Belum ada jadwal dan notulen retest |
| 2 | Penerimaan Kepegawaian per kelompok dengan owner, evidence, dan status resmi | Register UAT §8 | Belum Lulus | Belum ada keputusan penerimaan |
| 3 | Panduan lima role setelah penerimaan | `Panduan-Role/` | Draft | Lima draft tersedia; belum diterima stakeholder |
| 4 | Image/container dan PostgreSQL diperlakukan sebagai dependency eksternal | Dokumen baseline §2–§4 | Lulus pada level kebijakan | Keputusan K-MTG-06.3; kandidat aktual belum diterima |
| 5 | Backup berhasil direstore dan data tervalidasi | Dokumen recovery §3–§6 | Belum Lulus | Drill belum dilaksanakan |
| 6 | Migration, aplikasi, queue, scheduler, dan alur utama terverifikasi | Dokumen baseline §5–§7 | Belum Lulus | Environment kandidat belum ditetapkan |
| 7 | Prosedur dan bukti rollback tersedia | Dokumen recovery §7–§10 | Belum Lulus | Prosedur masih draft; drill belum dilaksanakan |
| 8 | Checklist release lengkap dan keputusan go/no-go | Checklist go/no-go | Belum Lulus | Keputusan belum dibuat |

## 4. Aturan Evidence

Setiap bukti minimal memuat:

1. tanggal dan waktu dalam `Asia/Makassar`;
2. owner/pelaksana;
3. environment dan exact commit SHA;
4. versi image/runtime/database yang diuji;
5. skenario atau perintah yang dijalankan;
6. expected result dan actual result;
7. tautan artefak, log, atau screenshot;
8. data sensitif yang sudah disamarkan;
9. status dan tindak lanjut.

Jangan menyimpan token, credential, Client Secret, NIK, No. KK, dump produksi, atau data pribadi
lain dalam repository. Bukti eksternal yang sensitif cukup direferensikan dengan ID/lokasi akses
terbatas dan ringkasan hasil yang aman.

## 5. Gate Penutupan

Issue #14 hanya boleh ditutup ketika:

- seluruh delapan acceptance criteria berstatus `Lulus`;
- setiap kelompok revisi memiliki keputusan Kepegawaian;
- lima panduan role berstatus `Diterima`;
- backup/restore dan rollback drill memiliki evidence;
- environment kandidat memiliki baseline version yang eksplisit;
- tidak ada defect critical/major yang belum memiliki keputusan;
- checklist go/no-go ditandatangani oleh owner yang berwenang.

Apabila dependency eksternal belum tersedia, status tetap `Executing` atau `Perlu Tindak Lanjut`;
ketiadaan dependency tidak boleh diubah menjadi klaim lulus.

## 6. Sumber Kanonis

- [Keputusan Evaluasi Meeting LLDIKTI 15 Agustus 2026](Keputusan-Evaluasi-Meeting-LLDIKTI-15-Agustus-2026.md)
- [Keputusan Evaluasi SIMPEG Bersama LLDIKTI 31 Agustus 2026](Keputusan-Evaluasi-Meeting-LLDIKTI-31-Agustus-2026.md)
- [User Stories SIMPEG Fase 1 — K-MTG-06](PRD-DLL/User-Stories-SIMPEG-Fase1.md)
- [Tracking Sprint 7](Tracking-Sprint-1-7/Sprint-7-Stabilization-Regression-UAT.md)
- [Runbook Demo Fitur SIMPEG Fase 1](Runbook-Demo-Fitur-SIMPEG-Fase-1.md)
- [Panduan Penulisan Kode SIMPEG](PRD-DLL/Panduan-Penulisan-Kode-SIMPEG.md)
