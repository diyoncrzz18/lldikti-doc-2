# Checklist Go/No-Go SIMPEG Fase 1

| Field | Nilai |
|---|---|
| Terkait | Issue [LLDIKTI16/simpeg#14](https://github.com/LLDIKTI16/simpeg/issues/14) |
| Target final | Akhir Agustus 2026 |
| Status | **NO-GO sementara — evidence wajib belum lengkap** |
| Release gate | Adriel Walintukan |

## 1. Identitas Kandidat

| Field | Nilai |
|---|---|
| Release candidate | Belum diisi |
| Exact commit SHA | Belum diisi |
| Image digest | Belum diisi |
| PHP/Laravel | Belum diisi |
| PostgreSQL | Belum diisi |
| Environment kandidat | Belum diisi |
| Tanggal evaluasi | Belum diisi |
| Owner environment | Belum diisi |

Branch name tidak cukup sebagai identitas kandidat. Exact SHA dan image digest wajib dicatat.

## 2. Gate Wajib

| ID | Gate | Owner | Evidence wajib | Status | Catatan |
|---|---|---|---|---|---|
| G-01 | Seluruh kelompok revisi memenuhi DoD | Owner issue/PR + QA | PR, CI, review, exact SHA | Belum Lulus | Kandidat belum dikunci |
| G-02 | Zoom/UAT dan penerimaan Kepegawaian | Dion + Grantly | Register UAT dan keputusan per kelompok | Belum Lulus | UAT belum dilaksanakan |
| G-03 | Panduan lima role diterima | Dion + Adithian | Lima panduan dan evidence penerimaan | Belum Lulus | Panduan masih draft |
| G-04 | Baseline environment terverifikasi | Jordan + Adriel | Inventaris runtime/image/database dan hasil smoke | Belum Lulus | Dependency eksternal belum lengkap |
| G-05 | Backup/restore drill lulus | Jordan + LLDIKTI | Backup ID, checksum, restore matrix | Belum Lulus | Drill belum dilaksanakan |
| G-06 | Migration, app, queue, scheduler, alur utama lulus | Jordan + Grantly | Log/perintah/skenario pada kandidat | Belum Lulus | Kandidat belum tersedia |
| G-07 | Rollback procedure dan drill lulus | Adriel + LLDIKTI | Runbook disetujui dan drill record | Belum Lulus | Keputusan infrastruktur belum tersedia |
| G-08 | Tidak ada critical/major tanpa keputusan | QA + Release Gate | Defect register dan retest | Belum Lulus | Full regression/UAT belum selesai |

Semua gate bersifat fail-closed. Satu gate `Belum Lulus` menghasilkan keputusan `NO-GO`.

## 3. Acceptance Criteria Issue #14

| # | Acceptance criterion | Status | Evidence |
|---:|---|---|---|
| 1 | Zoom retest segera setelah kelompok memenuhi DoD | Belum Lulus | [Register UAT](../UAT/Rencana-dan-Register-UAT-SIMPEG.md) |
| 2 | Hasil penerimaan per kelompok | Belum Lulus | Register UAT §8 |
| 3 | Panduan lima role setelah penerimaan | Belum Lulus | [Indeks Panduan Role](../Panduan-Role/README.md) |
| 4 | Dependency image/PostgreSQL tidak otomatis menjadi baseline | Lulus pada level kebijakan | [Baseline Environment](Baseline-dan-Verifikasi-Environment.md) |
| 5 | Backup direstore dan data tervalidasi | Belum Lulus | [Backup/Restore](Backup-Restore-dan-Rollback.md) |
| 6 | Migration, aplikasi, queue, scheduler, alur utama lulus | Belum Lulus | Baseline Environment §5–§7 |
| 7 | Rollback terdokumentasi dan memiliki evidence | Belum Lulus | Backup/Restore §7–§10 |
| 8 | Checklist lengkap dan keputusan go/no-go | Belum Lulus | Dokumen ini |

## 4. Defect dan Known Issues

| ID | Severity | Ringkasan | Owner | Status | Keputusan release | Evidence/retest |
|---|---|---|---|---|---|---|
| — | — | Full regression/UAT belum dijalankan | Grantly/Dion | Open | NO-GO sampai selesai | — |

Aturan:

- defect critical atau major harus ditutup dan diretest, atau menghasilkan keputusan `NO-GO`;
- defect minor yang diterima harus memiliki owner, target, dampak, dan persetujuan eksplisit;
- status tidak boleh diturunkan untuk melewati gate.

## 5. Security dan Data Protection

- [ ] authorization backend diuji untuk guest dan role tanpa izin;
- [ ] data scope per role diuji;
- [ ] NIK/No. KK tidak tampil mentah pada audit/export/evidence yang tidak berwenang;
- [ ] token, secret, credential, dan raw Keycloak payload tidak tercatat;
- [ ] dokumen pegawai hanya tersedia melalui storage/route terproteksi;
- [ ] Audit Log immutable dan mutasi penting tercatat;
- [ ] tidak ada manual login produksi;
- [ ] WhatsApp tetap fail-closed sampai dependency resmi terverifikasi.

## 6. Operasional

- [ ] maintenance/cutover window disetujui;
- [ ] operator dan peer checker ditunjuk;
- [ ] backup ID dan lokasi aman tercatat;
- [ ] queue/scheduler cutover sequence disetujui;
- [ ] monitoring log/health tersedia;
- [ ] komunikasi insiden dan escalation path tersedia;
- [ ] RPO/RTO disetujui;
- [ ] rollback trigger dipahami semua operator.

## 7. Ringkasan Keputusan

| Field | Nilai |
|---|---|
| Keputusan | **NO-GO sementara** |
| Alasan | UAT, penerimaan, baseline kandidat, restore, rollback, dan evidence runtime belum lengkap |
| Exact SHA yang diputus | Belum ada |
| Baseline environment | Belum ada |
| Known issues yang diterima | Belum ada |
| Tanggal keputusan | Belum ditetapkan |

`NO-GO sementara` adalah status readiness, bukan penolakan produk. Status berubah menjadi `GO` hanya
setelah semua gate lulus dan penandatangan memberikan keputusan eksplisit.

## 8. Sign-off

| Peran | Nama | Keputusan | Tanggal | Evidence/tanda tangan |
|---|---|---|---|---|
| Koordinator UAT | Dion Kobi | Belum | — | — |
| QA | Grantly Sorongan | Belum | — | — |
| Backend/environment | Jordan Sutarto | Belum | — | — |
| Input UI/panduan | Adithian Gunawan | Belum | — | — |
| Release gate | Adriel Walintukan | Belum | — | — |
| Pihak Kepegawaian/LLDIKTI | Belum diisi | Belum | — | — |

## 9. Referensi

- [Paket Eksekusi Issue #14](../Issue-14-UAT-Release-Readiness.md)
- [Rencana dan Register UAT](../UAT/Rencana-dan-Register-UAT-SIMPEG.md)
- [Panduan per Role](../Panduan-Role/README.md)
- [Baseline Environment](Baseline-dan-Verifikasi-Environment.md)
- [Backup, Restore, dan Rollback](Backup-Restore-dan-Rollback.md)
