# BUSINESS REQUIREMENTS DOCUMENT (BRD)

**Nama Proyek:** Sistem Deteksi Manipulasi Citra Berbasis AI Generatif (Hibrida Laplacian Variance & OCR)
**Disusun Oleh:** Fernanda - Business Analyst, FASILKOM Universitas Esa Unggul
**Tanggal:** 22 Oktober 2026

---

## 1. Executive Summary
Maraknya penggunaan *Generative AI* untuk membuat citra sintetis atau memanipulasi gambar asli telah menimbulkan masalah serius terkait integritas informasi, penipuan digital, dan misinformasi. Sistem verifikasi manual saat ini kewalahan menghadapi volume dan tingkat realisme citra buatan AI. 

Proyek ini bertujuan untuk membangun sistem deteksi manipulasi citra otomatis menggunakan pendekatan hibrida yang menggabungkan analisis piksel/spasial (*Laplacian Variance*) untuk mendeteksi anomali tekstur, dan analisis semantik (*Optical Character Recognition* / OCR) untuk mendeteksi halusinasi teks. Solusi ini diharapkan dapat memberikan alat bantu bagi institusi media, platform digital, dan lembaga forensik dalam memverifikasi keaslian citra secara cepat dan terukur.

## 2. Business Objectives & Success Metrics
**Business Objectives (Tujuan SMART):**
* Menyediakan sistem otomasi deteksi citra buatan AI yang mampu memproses dan mengklasifikasikan gambar dalam waktu kurang dari `[ISI DATA]` detik per gambar pada akhir kuartal `[ISI DATA]`.
* Mengurangi beban kerja tim verifikasi manual atau moderator konten sebesar `[ISI DATA]`% setelah sistem diimplementasikan secara penuh.

**Success Metrics (Indikator Keberhasilan):**
* **Akurasi Sistem:** Mencapai akurasi deteksi (F1-Score) minimal `[ISI DATA]`% pada *dataset* pengujian.
* **Tingkat False Positive:** Mempertahankan *False Positive Rate* (FPR) di bawah `[ISI DATA]`% untuk menghindari gambar asli (terutama yang buram alami) ditandai sebagai manipulasi.
* **Adoption Rate:** Sistem berhasil diujicobakan pada setidaknya `[ISI DATA]` skenario penggunaan oleh pengguna akhir (misal: moderator).

## 3. Scope
**In-Scope (Termasuk dalam Cakupan):**
* Pengembangan modul ekstraksi fitur spasial menggunakan algoritma *Laplacian Variance*.
* Pengembangan modul analisis anomali teks menggunakan OCR terintegrasi.
* Pembuatan algoritma *fusion* (penggabungan) skor dari kedua modul untuk hasil klasifikasi akhir (Asli vs. Manipulasi AI).
* Antarmuka pengguna (UI) berbasis web untuk mengunggah gambar dan melihat hasil analisis.
* Pelaporan hasil deteksi (skor keyakinan, area anomali teks).

**Out-of-Scope (Di Luar Cakupan):**
* Deteksi manipulasi pada file audio atau video (Deepfake video).
* Deteksi manipulasi citra tradisional (misal: *copy-move* atau *splicing* manual) yang tidak melibatkan AI Generatif, kecuali berdampak pada *Laplacian Variance*.
* Pembuatan model *Generative AI* itu sendiri (sistem ini hanya berfungsi sebagai detektor).
* Analisis forensik perangkat keras sumber gambar (kamera atau sensor).

## 4. Stakeholder Analysis

| Stakeholder | Peran | Kepentingan | Influence (Pengaruh) |
| :--- | :--- | :--- | :--- |
| **Dosen Pembimbing** | Pengawas & Evaluator Akademik | Memastikan proyek memenuhi standar Tugas Akhir FASILKOM, validitas metodologi | Tinggi |
| **Peneliti (Mahasiswa)** | Pengembang Utama | Menyelesaikan proyek tepat waktu, merancang sistem, mencapai target akurasi | Tinggi |
| **Moderator Konten / Jurnalis** | End-User (Pengguna Akhir) | Membutuhkan *tools* yang mudah digunakan dan cepat untuk memverifikasi gambar | Sedang |
| **Pakar Forensik Digital** | Subject Matter Expert (SME) | Memastikan hasil deteksi relevan dengan standar pembuktian digital | Sedang |
| **FASILKOM Esa Unggul** | Sponsor / Institusi | Publikasi riset berkualitas, inovasi teknologi terapan | Tinggi |

## 5. Functional Requirements (FR)

| ID | Nama Fitur | Deskripsi Kebutuhan Fungsional |
| :--- | :--- | :--- |
| **FR-01** | Unggah Gambar | Sistem harus memungkinkan pengguna mengunggah gambar dengan format standar (JPG, PNG, WEBP) hingga ukuran `[ISI DATA]` MB. |
| **FR-02** | Validasi Format | Sistem harus menolak file yang tidak sesuai dengan ekstensi yang diizinkan dan memberikan pesan *error*. |
| **FR-03** | Ekstraksi *Laplacian Variance* | Sistem harus dapat menghitung nilai variansi Laplacian dari gambar yang diunggah untuk mengukur ketajaman/blur. |
| **FR-04** | Segmentasi Teks (OCR) | Sistem harus dapat mendeteksi dan mengekstraksi teks (*bounding box* dan *string*) dari gambar menggunakan modul OCR. |
| **FR-05** | Analisis Halusinasi Teks | Sistem harus mengevaluasi teks hasil OCR untuk mencari anomali struktural atau kata tidak bermakna (indikasi halusinasi AI). |
| **FR-06** | Hibridisasi Skor | Sistem harus memiliki logika/algoritma yang menggabungkan skor anomali Laplacian dan skor anomali OCR. |
| **FR-07** | Klasifikasi Akhir | Sistem harus mengeluarkan keputusan biner (Asli / Manipulasi AI Generatif) berdasarkan ambang batas (threshold) skor hibrida. |
| **FR-08** | Tampilan Skor Keyakinan | Sistem harus menampilkan skor *Confidence Level* (dalam persentase) atas hasil klasifikasi. |
| **FR-09** | Visualisasi *Bounding Box* | Sistem harus menampilkan gambar asli dengan penanda kotak pada area teks yang dicurigai sebagai halusinasi AI. |
| **FR-10** | *Dashboard* Pengguna | Sistem harus menyediakan halaman utama yang menampilkan riwayat gambar yang pernah dianalisis oleh pengguna sesi tersebut. |
| **FR-11** | Unduh Laporan | Pengguna dapat mengunduh hasil analisis (status, skor, *bounding box*) dalam bentuk file PDF/CSV. |
| **FR-12** | *Clear Data* | Pengguna dapat menghapus gambar dan hasil analisis dari layar antarmuka untuk menjaga privasi. |
| **FR-13** | Pengaturan *Threshold* (Admin) | Sistem harus menyediakan antarmuka khusus (opsional) untuk menyesuaikan nilai ambang batas Laplacian dan OCR. |
| **FR-14** | API Endpoint | Sistem harus menyediakan *RESTful API endpoint* dasar untuk menerima gambar dan mengembalikan respons JSON berupa hasil analisis. |
| **FR-15** | *Error Handling* | Sistem harus menampilkan pesan responsif jika proses ekstraksi fitur gagal (misal: *timeout* atau gambar rusak). |

## 6. Non-Functional Requirements (NFR)
* **Performance:** Waktu respons sistem dari pengunggahan gambar hingga hasil ditampilkan tidak boleh melebihi `[ISI DATA]` detik dalam kondisi beban normal.
* **Security:** Sistem tidak menyimpan gambar yang diunggah secara permanen (otomatis dihapus dalam `[ISI DATA]` jam) untuk menjamin privasi pengguna.
* **Usability:** Antarmuka harus *responsive* dan dapat diakses dengan baik melalui perangkat *desktop* maupun perangkat bergerak (*mobile*).
* **Reliability:** Sistem harus memiliki *uptime* minimal `[ISI DATA]`% selama masa pengujian operasional.

## 7. Business Process As-Is vs To-Be
**As-Is (Kondisi Saat Ini):**
Pengguna (jurnalis atau moderator) menerima gambar yang dicurigai. Mereka harus mengecek metadata secara manual, melakukan penelusuran gambar terbalik (*reverse image search*), dan memperbesar gambar untuk mencari keanehan teks secara visual. Proses ini memakan waktu lama, subjektif, dan sering gagal mendeteksi gambar AI terbaru yang halus.

**To-Be (Kondisi Setelah Sistem Ada):**
Pengguna mengunggah gambar ke sistem web. Dalam beberapa detik, sistem otomatis menjalankan analisis *Laplacian Variance* (mendeteksi *blur/smoothness* tidak wajar) dan OCR (menemukan teks acak/halusinasi). Sistem langsung menyajikan kesimpulan, skor probabilitas manipulasi, dan menyorot area teks yang bermasalah, mempercepat pengambilan keputusan secara objektif.

## 8. Assumptions & Constraints
**Asumsi:**
* *Dataset* yang digunakan untuk menentukan ambang batas (*threshold*) mewakili kualitas gambar di dunia nyata.
* Gambar yang dianalisis memiliki area tekstur atau elemen teks; gambar solid color murni mungkin mengurangi efektivitas pendekatan hibrida ini.
* Pengguna memiliki koneksi internet yang stabil untuk mengakses aplikasi berbasis web.

**Kendala (Constraints):**
* Keterbatasan sumber daya komputasi (*hardware*) mahasiswa untuk menguji dan menjalankan model pada skala data yang sangat masif (Big Data).
* Kinerja modul OCR bergantung pada pustaka/API pihak ketiga yang digunakan (misal: Tesseract atau EasyOCR) dan dipengaruhi oleh resolusi gambar masukan.

## 9. Risk Register

| ID | Risiko | Probabilitas | Dampak | Mitigasi |
| :--- | :--- | :--- | :--- | :--- |
| **R01** | Kegagalan OCR pada *font* unik/gambar resolusi rendah (menghasilkan *False Positive* halusinasi) | Tinggi | Sedang | Menerapkan *preprocessing* peningkat kontras sebelum OCR dan melatih *threshold* OCR yang toleran. |
| **R02** | Gambar asli berkualitas rendah terdeteksi sebagai AI karena skor Laplacian rendah. | Sedang | Tinggi | Penggunaan bobot dinamis pada algoritma Hibrida; tidak hanya mengandalkan satu parameter mutlak. |
| **R03** | Server/Layanan sistem kelebihan beban saat memproses gambar berukuran sangat besar. | Sedang | Sedang | Menerapkan pembatasan ukuran file maksimal (FR-01) dan *auto-resizing* di sisi *backend*. |
| **R04** | Perubahan pola algoritma AI Generatif terbaru (*diffusion models*) yang mampu menghasilkan teks sempurna. | Rendah | Tinggi | Merancang sistem dengan arsitektur modular agar model deteksi teks/bahasa dapat di-*update* ke depannya. |

## 10. Acceptance Criteria
* Sistem dinyatakan berhasil jika mampu menerima *input* gambar, memprosesnya melalui dua modul (Laplacian dan OCR), dan menghasilkan skor akhir.
* Akurasi pengujian metrik fungsional mencapai batas toleransi yang disepakati bersama Dosen Pembimbing (misal F1-Score sesuai *Success Metrics*).
* Semua *Functional Requirements* (FR-01 hingga FR-15) telah diuji dan berfungsi (*Pass*) pada skenario *User Acceptance Testing* (UAT).
* Dokumen pendukung (panduan instalasi dan penggunaan) tersedia dengan lengkap.
```eof

Dokumen BRD di atas telah disusun dengan pendekatan profesional yang standar digunakan dalam analisis sistem. Placeholder `[ISI DATA]` sudah disiapkan di bagian matriks kesuksesan dan persyaratan non-fungsional agar Anda bisa mengisinya dengan parameter terukur yang spesifik sesuai kesepakatan dengan Dosen Pembimbing.
