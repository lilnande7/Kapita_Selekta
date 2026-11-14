# 🛡️ Deteksi Manipulasi Citra Berbasis AI Generatif (Hybrid Laplacian Variance & OCR)

![Python Version](https://img.shields.io/badge/python-3.9%2B-blue.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)
![Status](https://img.shields.io/badge/status-Research%20%2F%20Thesis-orange.svg)
![Institution](https://img.shields.io/badge/FASILKOM-Universitas%20Esa%20Unggul-red.svg)

Proyek Tugas Akhir (TA) di Fakultas Ilmu Komputer (FASILKOM), Universitas Esa Unggul. Sistem ini mengimplementasikan pendekatan **hibrida aliran ganda (*dual-stream*)** yang mengombinasikan analisis fitur spasial tingkat rendah (*Laplacian Variance*) dengan pengenalan semantik teks tingkat tinggi (*Optical Character Recognition* / OCR) untuk mendeteksi citra sintetis atau dokumen manipulatif buatan model *Generative AI* (seperti Stable Diffusion, Midjourney, DALL-E).

---

## 📌 Latar Belakang & Novelty

Metode deteksi tunggal sering kali mengalami kelemahan fatal:
1. **Piksel/Spasial murni:** Memiliki *False Positive Rate* (FPR) tinggi — citra asli yang mengalami *blur* fotografis atau kompresi alami sering salah diklasifikasikan sebagai AI.
2. **Semantik/Teks murni:** Mengabaikan jejak artefak *denoising* pada latar belakang gambar jika citra tidak didominasi teks.

**Solusi Hibrida Kami:**
Sistem ini menggunakan validasi silang (*cross-validation*) secara efisien tanpa memerlukan komputasi berat berbasis *Deep Learning* berlapis. Skor variansi spasial mendeteksi keburaman lokal, sementara mesin OCR mengevaluasi halusinasi tipografi (*gibberish text*).

---

## 📄 Alur Sistem & Arsitektur

<img width="2169" height="7385" alt="Laplacian OCR Manipulation Detection Pipeline-2026-11-14-125958" src="https://github.com/user-attachments/assets/3226c2bc-8128-4884-b37b-04b33dfc526c" />

---

## 🛠️ Fitur Utama

- 🔍 **Dual-Stream Extraction:** Ekstraksi ketajaman piksel spasial & validasi koherensi karakter teks secara paralel.
- ⚡ **Ringan & Cepat:** Bebas *heavy deep-learning inference*, cocok untuk eksekusi pada perangkat *edge* maupun server standar.
- 🎯 **Penekanan False Positive:** Memvalidasi citra asli yang buram agar tidak dilabeli secara salah sebagai AI.
- 📊 **Visualisasi Interaktif:** Menyorot area *bounding box* teks terdeteksi anomali serta menampilkan peta tepi (*edge map*).
- 📑 **Pelaporan PDF:** Ekspor ringkasan hasil analisis forensik digital ke format PDF/CSV.

---

## 🚀 Panduan Instalasi & Penggunaan

### Prasyarat
- Python 3.9 atau lebih baru
- [Tesseract OCR Engine](https://github.com/tesseract-ocr/tesseract) terpasang pada sistem operasi Anda.

### Step 1: Clone Repository
```bash
git clone https://github.com/username/deteksi-citra-ai-hibrida.git
cd deteksi-citra-ai-hibrida
```

### Step 2: Virtual Environment & Dependency Installation
```bash
# Membuat virtual environment
python -m venv venv

# Aktivasi venv (Windows)
venv\Scripts\activate
# Aktivasi venv (Linux/MacOS)
source venv/bin/activate

# Instalasi library pendukung
pip install -r requirements.txt
```

### Step 3: Jalankan Aplikasi (Web Dashboard)
```bash
python app.py
```
Akses aplikasi melalui peramban web di `http://localhost:5000` (atau port yang tertera pada konsol).

---

## 📊 Dataset & Evaluasi

Dataset yang digunakan mencakup citra hibrida kasual yang memuat elemen teks (infografis, *screenshot* web, meme, dan dokumen digital).

| Metrik Evaluasi | Target Minimum |
| :--- | :--- |
| **Akurasi (F1-Score)** | `[ISI DATA]%` |
| **False Positive Rate (FPR)** | `< [ISI DATA]%` |
| **Processing Time** | `< [ISI DATA] Detik/Gambar` |

---

## 📚 Referensi Jurnal (SLR Baseline)

1. **Lu, P. et al. (2026).** *SDA-Det: A subpixel-aware dual-domain artifact detector for AI-generated image detection.* Expert Systems with Applications.
2. **Ji, Y. et al. (2024).** *An Approach for Detecting AIGC Text Hallucinations Based on Knowledge Graph.* IEEE BDAI.
3. **Hossain, Md. Z. et al. (2025).** *FUSE: Unifying Spectral and Semantic Cues for Robust AI-Generated Image Detection.* IEEE ICCIT.
4. **Dachawar, M. et al. (2026).** *TRUESIGHT: A Two-Stage, Interpretable AI System for High-Fidelity Detection of Synthetically Generated Images.*

---

## ✒️ Penulis & Kontributor

- **Nama:** [Fernanda]
- **NIM:** [20230801118]
- **Program Studi:** Teknik Informatika
- **Fakultas:** Ilmu Komputer, Universitas Esa Unggul

---

## 📜 Lisensi
****
