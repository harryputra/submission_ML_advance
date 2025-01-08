# Sistem Rekomendasi Film

Proyek ini bertujuan untuk mengembangkan sistem rekomendasi film menggunakan pendekatan **Content-Based Filtering** dan **Collaborative Filtering**. Sistem ini membantu pengguna menemukan film sesuai preferensi mereka, meningkatkan pengalaman pengguna, serta mendukung loyalitas pelanggan.

## Table of Contents

- [Overview](#overview)
- [Business Understanding](#business-understanding)
- [Goals](#goals)
- [Solution Approach](#solution-approach)
- [Dataset](#dataset)
- [Data Understanding](#data-understanding)
- [Exploratory Data Analysis (EDA)](#exploratory-data-analysis-eda)
- [Data Preparation](#data-preparation)
- [Modeling and Result](#modeling-and-result)
- [Getting Recommendations](#getting-recommendations)
- [Installation](#installation)
- [Usage](#usage)
- [License](#license)

---

## Overview

Sistem rekomendasi adalah elemen penting dalam industri hiburan modern untuk menyarankan film relevan berdasarkan preferensi pengguna. Proyek ini menggunakan algoritma **Content-Based Filtering** untuk menganalisis metadata film dan **Collaborative Filtering** untuk memahami pola interaksi pengguna.

---

## Business Understanding

### Problem Statements
- Bagaimana merekomendasikan film yang sesuai dengan preferensi pengguna berdasarkan data historis?
- Bagaimana meningkatkan akurasi rekomendasi film?

### Goals
- Membangun sistem rekomendasi berbasis data historis dan kategori konten.
- Meningkatkan akurasi rekomendasi melalui algoritma filtering.
- Mengukur keberhasilan sistem menggunakan metrik evaluasi seperti **Precision** dan **RMSE**.

---

## Solution Approach

1. **Content-Based Filtering**  
   Menggunakan metadata seperti genre untuk memberikan rekomendasi berdasarkan kesamaan.
2. **Collaborative Filtering**  
   Menganalisis pola interaksi pengguna untuk menyarankan film berdasarkan preferensi pengguna lain.

---

## Dataset

Dataset yang digunakan: [Movie Recommendation Dataset](https://www.kaggle.com/datasets/rohan4050/movie-recommendation-data).

### Informasi Dataset
- **links.csv**: 9,742 baris, 3 kolom.
- **movies.csv**: 9,742 baris, 3 kolom.
- **ratings.csv**: 100,836 baris, 4 kolom.
- **tags.csv**: 14,531 baris, 4 kolom.

---

## Data Understanding

### Missing Value
- **tags.csv** memiliki nilai kosong pada kolom `tag`.
- Dataset lainnya tidak memiliki nilai kosong.

### Outliers
- Rentang rating valid adalah **0.5 hingga 5.0**.

### Struktur Dataset
- **links.csv**: Kolom `movieId`, `imdbId`, dan `tmdbId`.
- **movies.csv**: Kolom `movieId`, `title`, dan `genres`.
- **ratings.csv**: Kolom `userId`, `movieId`, `rating`, dan `timestamp`.
- **tags.csv**: Kolom `userId`, `movieId`, `tag`, dan `timestamp`.

---

## Exploratory Data Analysis (EDA)

- **Distribusi Rating**: Menggunakan histogram untuk memvisualisasikan distribusi rating.
- **Analisis Genre**: Menampilkan jumlah kemunculan setiap genre dalam dataset film.
- **Gabungan Dataset**: Dataset digabungkan berdasarkan kolom `movieId` untuk analisis komprehensif.

---

## Data Preparation

1. **Mengatasi Missing Value**  
   - Menghapus nilai kosong pada dataset.
2. **Menggabungkan Dataset**  
   - Menggabungkan dataset `ratings`, `movies`, dan `tags`.
3. **Normalisasi Data**  
   - Mengubah rating menjadi rentang 0-1 untuk proses pelatihan.
4. **Pembagian Dataset**  
   - 80% untuk pelatihan, 20% untuk validasi.

---

## Modeling and Result

### Model RecommenderNet
Model ini menggunakan embedding untuk merepresentasikan pengguna dan film dalam ruang vektor berdimensi rendah.

- **Arsitektur**: Menggunakan layer embedding untuk `userId` dan `movieId`.
- **Optimasi**: Binary Crossentropy dan Adam Optimizer.
- **Evaluasi**: Menggunakan RMSE.

### Visualisasi Performansi
Menampilkan tren RMSE pada data pelatihan dan validasi untuk mengukur performa model.

---

## Getting Recommendations

1. **Input Data Pengguna**  
   - Menentukan film yang belum ditonton oleh pengguna tertentu.
2. **Prediksi dan Rekomendasi**  
   - Menggunakan Cosine Similarity untuk menghitung kesamaan antar film.
   - Memberikan 10 rekomendasi film dengan skor tertinggi.

---

## Installation

1. Clone repositori:
   ```bash
   git clone https://github.com/username/movie-recommendation-system.git
   cd movie-recommendation-system
