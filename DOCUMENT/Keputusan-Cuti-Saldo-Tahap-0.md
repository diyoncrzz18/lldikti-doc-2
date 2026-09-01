# Keputusan Tahap 0 — Saldo dan Batas Pengajuan Cuti

| Field | Detail |
|---|---|
| Tanggal keputusan | 27 Juli 2026 |
| Status | **Disetujui** — menjadi acuan implementasi saldo dan batas pengajuan cuti Fase 1 sampai ada keputusan yang lebih baru |
| Disetujui melalui | Persetujuan pengguna pada task Codex: “Setujui keputusan Tahap 0.” |
| Acuan utama | `PRD-SIMPEG-Fase1-Core.md` §9.2–§9.4; `User-Stories-SIMPEG-Fase1.md` US-4.1, US-4.3, dan US-4.6; `Panduan-Penulisan-Kode-SIMPEG.md`; `AGENTS.md` |
| Cakupan | Saldo cuti tahunan saat pengajuan aktif, pengajuan lintas tahun, serta batas jenis cuti yang eksplisit di PRD |
| Di luar cakupan | Integrasi SIASN/BKN, aturan operasional Dosen DPK, aktivasi WhatsApp Business produksi, dan penetapan batas numerik baru yang tidak ditulis di PRD |

---

## K-CUT-01 — Pengajuan aktif mencadangkan hak cuti tahunan tanpa memotong saldo final

### Keputusan

Setiap pengajuan **Cuti Tahunan** yang masih aktif mencadangkan hak cuti sebesar jumlah hari kerjanya. Reservasi **bukan** pemotongan saldo final.

### Aturan penerapan

1. Saldo ledger resmi (`sisa`) dan `terpakai` hanya berubah saat keputusan final **`Disetujui`**, sesuai PRD dan US-4.6.
2. Sistem menghitung `saldo_dapat_diajukan` dari saldo tersedia dikurangi total reservasi aktif milik pegawai pada tahun cuti yang sama.
3. Reservasi aktif berlaku untuk pengajuan dengan status berikut:
   - `menunggu_approval`;
   - `ditangguhkan`;
   - `perlu_perubahan`.
4. Pada `perlu_perubahan`, reservasi tetap terikat pada request yang sama dan dihitung ulang atomik saat Pegawai mengirim ulang pengajuan dengan tanggal/jumlah hari baru.
5. Saat keputusan final `disetujui`, reservasi dikonversi menjadi pemotongan saldo final yang sudah berlaku di ledger. Sistem tidak boleh melakukan pemotongan ganda.
6. Saat `tidak_disetujui`, reservasi dilepas. Jika pada masa depan tersedia pembatalan pengajuan Fase 1 yang sah, pembatalan juga wajib melepas reservasi secara atomik.
7. `ditangguhkan` tidak melepas reservasi sampai ada keputusan atau tindak lanjut yang mengubah statusnya.
8. Form Pegawai wajib membedakan dengan jelas: **Saldo tersedia aktual**, **Dialokasikan untuk pengajuan aktif**, **Masih dapat diajukan**, dan **Sudah terpakai setelah disetujui**.
9. Setiap pembuatan, penyesuaian, konversi, dan pelepasan reservasi harus dapat diaudit; reservasi tidak boleh ditulis sebagai pemakaian cuti final.

### Alasan

- Menutup risiko beberapa pengajuan pending yang totalnya melebihi hak Pegawai.
- Mempertahankan ketentuan bahwa hanya keputusan final `Disetujui` yang mengurangi saldo cuti tahunan.
- Memberi informasi yang jujur pada Pegawai tanpa mencampur hak dasar, koreksi administratif, pemakaian final, dan alokasi sementara.

---

## K-CUT-02 — Batas tahun kalender berlaku untuk semua jenis cuti

### Keputusan

Aturan PRD bahwa **satu pengajuan tidak boleh melewati tahun kalender** berlaku untuk seluruh jenis cuti, tanpa pengecualian, termasuk Cuti Melahirkan dan CLTN.

### Aturan penerapan

1. Rentang Desember–Januari harus dibuat sebagai pengajuan terpisah per tahun kalender.
2. Cuti Melahirkan dan CLTN yang secara keseluruhan dapat berlangsung lebih dari satu tahun tetap dibagi menjadi beberapa pengajuan tahunan.
3. Batas maksimum Cuti Melahirkan dan CLTN dihitung **kumulatif** atas seluruh pengajuan yang merupakan kelanjutan dari kebutuhan cuti yang sama; pemecahan per tahun tidak boleh menjadi cara untuk melewati batas maksimum.
4. Implementasi wajib menyimpan atau menentukan keterkaitan antarpengajuan tersebut secara eksplisit dan auditabel; sistem tidak boleh menyimpulkan keterkaitan dari teks alasan bebas semata.
5. Validasi lintas tahun di `Store` dan `Resubmit` tetap menjadi pengaman backend. Umpan balik di form hanya melengkapi pengalaman pengguna, bukan menggantikan validasi server.

### Alasan

- Mengikuti acceptance criteria PRD dan User Stories secara langsung.
- Menghindari ambiguitas reset kuota, carry-over, serta audit saldo antar tahun.
- Batas durasi maksimum tetap terlindungi meskipun pengajuan harus dipisahkan per tahun.

---

## K-CUT-03 — Batas jenis cuti memakai durasi kalender dan aturan eksplisit PRD

### Keputusan

Batas yang eksplisit dalam PRD diterapkan sebagai aturan server-side yang berbasis tanggal kalender, bukan hitungan hari tetap atau pencocokan nama tampilan jenis cuti.

### Aturan penerapan

| Jenis cuti | Aturan yang disetujui |
|---|---|
| Cuti Tahunan | Maksimum sebesar `saldo_dapat_diajukan` berbasis hari kerja. |
| Cuti Melahirkan | Maksimum 3 bulan kalender secara kumulatif untuk kebutuhan cuti yang sama. |
| Cuti Besar | Hanya PNS dan membutuhkan masa kerja minimal 5 tahun kalender sejak TMT pengangkatan. |
| CLTN | Hanya PNS dan maksimum 3 tahun kalender secara kumulatif untuk kebutuhan cuti yang sama. |
| Cuti Sakit | Tidak ditambah batas numerik baru pada Fase 1. Ketentuan surat dokter/aturan rinci menunggu sumber peraturan yang disahkan. |
| Cuti Karena Alasan Penting | Tidak ditambah batas numerik baru pada Fase 1. Ketentuan rinci menunggu sumber peraturan yang disahkan. |

1. Tanggal mulai dan tanggal selesai diperlakukan sebagai rentang tanggal inklusif.
2. Perhitungan bulan/tahun menggunakan aritmetika kalender; implementasi tidak boleh mengganti 3 bulan menjadi 90 hari atau 3 tahun menjadi 1.095 hari.
3. Implementasi menggunakan metadata kode/reference jenis cuti, bukan `nama` jenis cuti, agar perubahan label UI tidak mengubah penegakan aturan.
4. Aturan yang belum memiliki batas numerik eksplisit di PRD tidak boleh diisi dengan nilai asumsi. Bila peraturan resmi tersedia, keputusan ini harus diperbarui terlebih dahulu sebelum kode diberi batas baru.

### Alasan

- Menerapkan batas yang benar-benar tertulis di PRD tanpa menambah kebijakan legal yang belum disetujui.
- Menghindari kesalahan durasi di bulan dengan panjang berbeda dan tahun kabisat.
- Menjaga reference table sebagai sumber konfigurasi jenis cuti serta validasi server sebagai sumber kebenaran.

---

## Konsekuensi implementasi

1. Tahap 2–3 membangun payload saldo tunggal dan preview saldo berdasarkan tahun `tanggal_mulai`; payload membedakan saldo aktual, reservasi aktif, saldo yang masih dapat diajukan, pemakaian final, serta koreksi administratif.
2. Tahap 4–5 menambahkan model/ledger atau mekanisme reservasi yang append-only dan auditabel, dengan transaksi serta penguncian yang aman terhadap submit paralel.
3. Tahap 4–5 menambahkan keterkaitan eksplisit antarpengajuan untuk penerapan maksimum kumulatif Cuti Melahirkan dan CLTN yang dipisah per tahun.
4. Semua perubahan wajib memiliki Feature/Unit test untuk guest denial, RBAC/data scope, submit valid/tidak valid, perubahan status, audit, atomicity, dan regresi saldo final.
5. Perubahan route/API harus mengikuti pola: `Route -> Middleware/RBAC -> FormRequest -> Controller -> Action -> Service/Model -> Resource/Payload -> Response`.

## Batas yang tetap berlaku

- Label keputusan cuti tetap persis: `Disetujui`, `Perubahan`, `Ditangguhkan`, dan `Tidak Disetujui`.
- Kode tidak boleh memperkenalkan login manual produksi, mutasi saldo tanpa audit, atau akses saldo Pegawai lain dari endpoint Pegawai.
- Pengurangan saldo tahunan hanya terjadi setelah final `Disetujui`; keputusan lain tidak mengurangi saldo final.
- Keputusan ini melengkapi PRD/User Stories untuk area yang sebelumnya ambigu. Jika ada konflik baru, keputusan produk berikutnya harus dicatat sebelum implementasi dilanjutkan.



---

## K-CUT-04 — Pendataan saldo dari cuti yang telah dipakai

> **Status:** Disetujui melalui [Keputusan Evaluasi Meeting LLDIKTI](Keputusan-Evaluasi-Meeting-LLDIKTI-15-Agustus-2026.md), 15 Agustus 2026. Ketentuan ini menggantikan frasa terdahulu yang memperlakukan saldo/sisa sebagai input utama setup awal.

### Keputusan

1. Setiap tahun memberikan hak dasar 12 hari kerja. Untuk migrasi dan rekonsiliasi, Admin Kepegawaian memasukkan **jumlah cuti tahunan yang telah dipakai/diklaim** per tahun, bukan saldo yang tersisa.
2. Sistem menghitung sisa tahun tersebut, carry-over N-1 maksimal 6 hari, dan total hak tahun berjalan secara berjenjang dari pemakaian N-2, N-1, dan tahun berjalan.
3. Hak tahun berjalan menjadi 24 hari hanya bila pemakaian pada N-2 dan N-1 sama dengan nol. Jika terdapat pemakaian pada salah satu dari dua tahun tersebut, total maksimum adalah 18 hari.
4. Koreksi dilakukan dengan memperbaiki data pemakaian atau entri cuti manual dan menjalankan hitung ulang. Saldo sisa bukan nilai administratif yang ditulis bebas sebagai sumber kebenaran.
5. Direct balance override tidak tersedia pada Fase 1. Konsumsi hak memakai bucket tertua yang masih sah dengan urutan N-2, N-1, lalu tahun berjalan; hak lama yang tersisa kedaluwarsa pada akhir tahun penggunaannya.
6. Koreksi backdated menghitung ulang seluruh transaksi setelah titik koreksi secara kronologis dan atomik.
7. PNS dan PPPK memakai mesin ceiling 12/18/24 yang sama. Untuk PPPK, ceiling 18 mensyaratkan masa perjanjian kerja di atas 2 tahun dan ceiling 24 mensyaratkan masa perjanjian kerja di atas 3 tahun.

### Alasan

Penggunaan yang telah diklaim dapat direkonsiliasi dan divalidasi secara berjenjang, sedangkan input saldo sisa membuat asal-usul perhitungan rollover sulit dibuktikan.

## K-CUT-05 — Input cuti manual yang telah disetujui di luar SIMPEG

> **Status:** Disetujui melalui [Keputusan Evaluasi Meeting LLDIKTI](Keputusan-Evaluasi-Meeting-LLDIKTI-15-Agustus-2026.md), dengan revisi keputusan langsung pengguna pada 20 Agustus 2026 (K-MTG-07A). Ketentuan dokumen wajib dari 15 Agustus dipertahankan sebagai jejak historis **Superseded**.

### Keputusan

1. Admin Kepegawaian secara eksklusif dapat mencatat cuti yang telah disetujui dan dijalankan di luar SIMPEG: cuti historis, cuti pada tahun berjalan sebelum go-live, atau cuti saat layanan tidak tersedia.
2. Dokumen pendukung dan nomor dokumen persetujuan bersifat opsional. Bila dokumen diberikan, file wajib tervalidasi ketat dan disimpan privat. **Ketentuan dokumen wajib 15 Agustus telah superseded oleh revisi 20 Agustus 2026.**
3. Entri baru wajib menyimpan snapshot persetujuan historis total 2–10 tahap: 0–8 `verifier`, tepat satu `kepala_bagian`, kemudian tepat satu `pybmc` final. Hasil `verified`, `approved`, atau `final_approved` diturunkan sistem dari jenis tahap dan tidak diinput Admin.
4. Approver dapat berupa pegawai internal atau pejabat eksternal. UUID internal tetap hidden/system, bukan input UX; pejabat eksternal wajib memiliki identitas snapshot yang memadai tanpa dibuatkan akun atau pegawai palsu.
5. Form boleh dimulai dengan chain kosong atau menyalin current chain pegawai. Hasil salinan dapat diedit bagian per bagian dan tidak mengubah sumber; snapshot tersimpan tidak mengikuti perubahan konfigurasi current.
6. Entri tersebut langsung menjadi fakta cuti yang telah disetujui di luar SIMPEG; sistem tidak membuat usulan, approval aktif, reservasi, notifikasi approval, atau bukti approval ulang.
7. Untuk cuti tahunan, entri manual membentuk pemakaian final yang diaudit dan ikut menghitung saldo serta rollover. Ia bukan reservasi aktif K-CUT-01. Jumlah hari kerja dihitung sistem dari periode dan kalender kerja; duplikasi serta overlap dengan cuti aktif pegawai yang sama ditolak.
8. Koreksi entry wajib atomik, menyimpan alasan serta nilai sebelum/sesudah, dan menghitung ulang saldo terkait dengan fakta dan snapshot pengganti. Pembatalan atau perubahan current configuration tidak mengubah snapshot lama; record lama tidak di-hard-delete.
9. Mutasi hanya tersedia bagi role Admin Kepegawaian secara eksklusif dengan permission `cuti.manual.manage`; audit tidak memuat path dokumen privat dan surface baca tetap menjaga privasi serta query bounded.

### Batas

Jalur ini tidak boleh dipakai untuk mempercepat pengajuan baru yang belum memperoleh persetujuan di luar SIMPEG atau sebagai alternatif ketika SIMPEG tersedia. Setelah go-live, jalur ini tetap dapat digunakan untuk mencatat cuti yang telah diproses dan disetujui secara manual saat layanan SIMPEG downtime.

---

## K-CUT-06 — Penyelarasan evaluasi LLDIKTI 31 Agustus dan klarifikasi 1 September 2026

> **Status:** Disetujui melalui [Keputusan Evaluasi SIMPEG Bersama LLDIKTI 31 Agustus 2026](Keputusan-Evaluasi-Meeting-LLDIKTI-31-Agustus-2026.md) dan klarifikasi pembatalan 1 September 2026. Ketentuan ini melengkapi K-CUT-01, K-CUT-04, dan K-CUT-05 tanpa menghapus jejak keputusan sebelumnya.

### Keputusan

1. Label bisnis snapshot dan konfigurasi approval cuti adalah `Verifikator → Atasan Langsung → PYBMC`. Nilai teknis legacy `kepala_bagian` pada data yang sudah ada tetap dapat dipertahankan sebagai representasi internal Atasan Langsung sampai ada keputusan migrasi schema tersendiri.
2. Ketika Atasan Langsung dan PYBMC adalah orang yang sama, keduanya tetap merupakan dua tahap snapshot dan membutuhkan dua tindakan. Sistem tidak boleh melewati tahap kedua hanya karena `approver_employee_id` sama pada pasangan peran tersebut.
3. Selama pengajuan belum final, Pegawai dapat mengirim satu permohonan pembatalan aktif sebagai record tersendiri dengan alasan wajib. Approval utama ditahan, reservasi saldo tetap dipertahankan, dan Admin Kepegawaian menerima notifikasi.
4. Jika Admin Kepegawaian menyetujui pembatalan, pengajuan utama menjadi batal dan reservasi dilepas secara atomik. Jika ditolak, approval dilanjutkan dari tahap sebelumnya. Permohonan, keputusan, dan mutasi saldo diaudit tanpa menghapus request, snapshot, timeline, atau histori; Pegawai menerima notifikasi hasil keputusan.
5. Revisi langsung hanya tersedia sebelum tindakan approval. Setelah ada tindakan, Pegawai meminta pembatalan dan, bila disetujui, membuat pengajuan baru yang memulai chain dari awal.
6. `Ditangguhkan` ketika pengajuan masih aktif tetap mempertahankan reservasi seperti K-CUT-01. Namun, bila cuti yang sudah final `Disetujui` ditetapkan `Ditangguhkan` oleh Admin Kepegawaian dengan alasan wajib, sistem membuat koreksi/replay ledger atomik untuk membalik pemakaian final yang terdampak. Kedua keadaan tersebut tidak boleh disamakan.
7. Cuti di Luar SIMPEG adalah fakta historis/transisi yang menjadi sumber pemakaian tahunan N-2, N-1, dan tahun berjalan sebelum go-live, serta fakta pemulihan untuk cuti yang telah disetujui secara manual ketika SIMPEG downtime setelah go-live. Halaman ringkasan **Catat Pemakaian Tahunan** tidak menerima input angka langsung; ia menampilkan agregat dari fakta pemakaian dan entri manual yang telah tercatat.
8. Saat SIMPEG downtime, proses manual harus selesai dan disetujui di luar sistem. Setelah layanan pulih, Admin Kepegawaian mencatat keputusan tersebut sebagai fakta final melalui Cuti di Luar SIMPEG; sistem tidak membuat approval aktif baru, dan jalur ini tidak boleh dipakai rutin ketika SIMPEG tersedia.

### Konsekuensi verifikasi

- Uji PostgreSQL harus mencakup pasangan Atasan Langsung/PYBMC dengan aktor sama, tanpa melewati salah satu peran.
- Uji pembatalan harus mencakup permohonan setelah Verifikator bertindak, penahanan approval, keputusan setuju/tolak oleh Admin Kepegawaian, pelepasan atau pemertahanan reservasi, audit, serta kelanjutan dari tahap sebelumnya bila ditolak.
- Uji UI harus membuktikan bahwa ringkasan pemakaian tidak dapat diubah langsung dan koreksi hanya berasal dari fakta sumber yang beralasan serta teraudit.
- Uji pemulihan downtime harus membuktikan bahwa fakta final dicatat tepat satu kali setelah layanan pulih, menolak duplikasi/overlap, dan tidak membuat approval aktif atau reservasi baru.
