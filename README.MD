# Laporan Proyek Machine Learning - Sistem Rekomendasi Film  
-- Mohammad Harry Khomas Saputra --

## Project Overview  

Sistem rekomendasi film adalah elemen krusial dalam industri hiburan modern, memungkinkan pengalaman pengguna yang lebih personal. Sistem ini membantu platform seperti Netflix, Disney+, dan WeTV dalam meningkatkan keterlibatan pengguna serta kepuasan pelanggan.  

Dengan ribuan pilihan film yang tersedia, pengguna sering merasa kewalahan dalam memilih. Hal ini menciptakan kebutuhan akan sistem rekomendasi yang efektif untuk menyederhanakan proses dan meningkatkan kepuasan pengguna.  

Proyek ini bertujuan untuk membangun sistem rekomendasi berbasis algoritma machine learning, termasuk **Content-Based Filtering** dan **Collaborative Filtering**. Sistem ini dirancang untuk memahami preferensi pengguna berdasarkan data historis mereka dan memberikan rekomendasi yang relevan serta personal.

## Business Understanding  

### Problem Statements  

- Bagaimana memberikan rekomendasi film yang sesuai dengan preferensi pengguna berdasarkan data historis?  
- Bagaimana meningkatkan akurasi rekomendasi sistem untuk memberikan pengalaman pengguna yang optimal?  

### Goals  

- Mengembangkan sistem rekomendasi menggunakan algoritma Content-Based Filtering dan Collaborative Filtering.  
- Mengukur performa sistem menggunakan metrik seperti precision dan RMSE untuk memastikan rekomendasi yang relevan.  
- Meningkatkan pengalaman pengguna melalui rekomendasi yang lebih personal dan akurat.  

### Solution Approach  

1. **Content-Based Filtering**:  
   - Memanfaatkan metadata film (genre, deskripsi) untuk memberikan rekomendasi berdasarkan kesamaan dengan film yang pernah disukai pengguna.  
2. **Collaborative Filtering**:  
   - Menggunakan data historis dari interaksi pengguna untuk merekomendasikan film berdasarkan pola preferensi pengguna lain yang serupa.  

## Data Understanding  

Dataset yang digunakan adalah **Movie Recommendation Data** dari Kaggle. Dataset ini terdiri dari beberapa variabel:  

- **links**: Daftar tautan film yang berisi `movieId`, `imdbId`, dan `tmdbId`.  
- **movies**: Informasi tentang film seperti `movieId`, `title`, dan `genres`.  
- **ratings**: Data penilaian dari pengguna terhadap film tertentu.  
- **tags**: Kata kunci yang ditambahkan pengguna untuk menggambarkan film.  

Tahapan eksplorasi data dilakukan melalui:  

- Melihat hubungan antar variabel berdasarkan ID (`movieId` dan `userId`).  
- Menggabungkan variabel film menggunakan `movie_all` dan variabel pengguna menggunakan `user_all`.  

## Data Preparation  

Berikut adalah langkah-langkah dalam mempersiapkan data:  

1. **Mengatasi Missing Value**: Menghapus data yang kosong untuk memastikan kualitas dataset.  
2. **Membagi Data**: Membagi dataset menjadi data pelatihan (80%) dan validasi (20%).  
3. **Menggabungkan Variabel**: Menggabungkan beberapa variabel berdasarkan ID unik.  
4. **Mengurutkan Data**: Mengurutkan data berdasarkan `movieId` secara ascending.  
5. **Mengatasi Duplikasi Data**: Menghapus data yang memiliki nilai atau isi yang sama.  
6. **Konversi Data ke List**: Mengubah data menjadi bentuk list untuk kebutuhan pemodelan.  
7. **Membuat Dictionary**: Membuat dictionary dari data film dan pengguna.  
8. **TfidfVectorizer**: Melakukan pembobotan teks untuk metadata film.  
9. **Preprocessing**: Menghilangkan masalah yang dapat mengganggu analisis data.  
10. **Mapping Data**: Memetakan data untuk menciptakan hubungan antar variabel.  

## Modeling and Results  

Proses modeling menggunakan dua algoritma:  

1. **Content-Based Filtering**:  
   - Menggunakan metadata seperti genre untuk memberikan rekomendasi film berdasarkan kesamaan dengan film yang pernah disukai.  

   **Hasil:**  
   - Pengguna menyukai film *Jumanji (1995)* yang bergenre Adventure, Children, dan Fantasy.  
   - Rekomendasi Top 5:  
     - Chronicles of Narnia: The Lion, the Witch and the Wardrobe  
     - Harry Potter and the Sorcerer’s Stone  
     - Chronicles of Narnia: Prince Caspian  
     - Lemony Snicket’s A Series of Unfortunate Events  
     - The Lord of the Rings (1978)  

2. **Collaborative Filtering**:  
   - Menggunakan data rating dari pengguna lain dengan pola preferensi serupa untuk memberikan rekomendasi.  

   **Hasil:**  
   - Rekomendasi Top 10: Film bergenre Comedy dan Drama dengan rating tinggi.  

## Evaluation  

### Evaluasi untuk Content-Based Filtering  

- Film yang direkomendasikan termasuk *Jumanji (1995)* dengan genre Adventure, Children, dan Fantasy.  
- Precision sistem: 60% (3 dari 5 film yang direkomendasikan memiliki genre yang mirip).  

### Evaluasi untuk Collaborative Filtering  

- Menggunakan metrik RMSE (Root Mean Squared Error) untuk evaluasi model.  
- RMSE mencerminkan tingkat kesalahan prediksi model, dengan hasil RMSE yang lebih kecil menunjukkan akurasi yang lebih tinggi.  

**Kesimpulan**:  
Sistem rekomendasi ini mampu memberikan hasil yang relevan dan meningkatkan pengalaman pengguna melalui pendekatan Content-Based Filtering dan Collaborative Filtering.
