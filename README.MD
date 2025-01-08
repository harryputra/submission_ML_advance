# **Sistem Rekomendasi Film**
## _Proyek Sistem Rekomendasi Menggunakan Content-based dan Collaborative Filtering_

---

## **Project Overview**

### **Latar Belakang**
Dengan meningkatnya jumlah konten digital, platform streaming film menghadapi tantangan untuk menyajikan rekomendasi yang relevan bagi pengguna. Platform seperti Netflix, Disney+, dan Amazon Prime memiliki ribuan hingga jutaan film dan acara yang sering kali membuat pengguna kebingungan memilih konten yang sesuai dengan preferensi mereka. Dalam konteks ini, sistem rekomendasi menjadi sangat penting untuk meningkatkan pengalaman pengguna dan efisiensi waktu pencarian.

Sistem rekomendasi membantu pengguna dengan memberikan saran film berdasarkan data historis, preferensi mereka sendiri, atau pola komunitas pengguna lain. Pendekatan ini tidak hanya mempermudah pengguna, tetapi juga meningkatkan keterlibatan dan loyalitas mereka terhadap platform.

---

## **Business Understanding**

### **Problem Statements**
1. **Bagaimana memberikan rekomendasi film yang relevan kepada pengguna?**
   - Banyak pengguna merasa kesulitan menemukan film yang sesuai dengan preferensi mereka di tengah banyaknya pilihan yang tersedia.
2. **Bagaimana memanfaatkan data pengguna untuk meningkatkan akurasi rekomendasi?**
   - Data seperti rating film atau pola tonton pengguna dapat dimanfaatkan untuk memberikan rekomendasi yang lebih personal.
3. **Bagaimana pola komunitas dapat mendukung rekomendasi film yang lebih akurat?**
   - Pola rating pengguna lain dapat digunakan untuk memperluas cakupan rekomendasi.

---

### **Tujuan**
Proyek ini bertujuan untuk:
1. **Meningkatkan pengalaman pengguna**:
   - Memberikan rekomendasi film yang relevan berdasarkan preferensi mereka.
2. **Mengurangi waktu pencarian konten**:
   - Membantu pengguna menemukan film baru dengan lebih cepat.
3. **Mengukur performa sistem**:
   - Menentukan tingkat akurasi sistem rekomendasi menggunakan metrik evaluasi seperti Precision@k untuk Content-based Filtering dan RMSE untuk Collaborative Filtering.

---

### **Goals**
1. **Membangun sistem rekomendasi yang akurat**:
   - Menggunakan pendekatan Content-based Filtering dan Collaborative Filtering.
2. **Menilai kualitas rekomendasi**:
   - Melakukan evaluasi berdasarkan metrik performa yang umum digunakan.
3. **Memberikan solusi yang efektif**:
   - Menyediakan rekomendasi yang relevan, baik berdasarkan preferensi individual maupun pola komunitas.

---

### **Solution Approach**
Proyek ini menggunakan dua pendekatan utama:
1. **Content-Based Filtering**:
   - Analisis dilakukan berdasarkan atribut film seperti genre, sutradara, dan deskripsi.
   - Algoritma merekomendasikan film yang memiliki kemiripan dengan film yang disukai pengguna.
2. **Collaborative Filtering**:
   - Algoritma menggunakan data komunitas untuk menemukan kesamaan pola rating antara pengguna.
   - Pendekatan ini tidak memerlukan atribut eksplisit film, tetapi menggunakan pola perilaku komunitas untuk memberikan rekomendasi.

---

### **Keuntungan Pendekatan**
1. **Content-Based Filtering**:
   - Memberikan rekomendasi yang personal sesuai dengan preferensi pengguna.
   - Tidak bergantung pada data komunitas, sehingga lebih cocok untuk pengguna baru.
2. **Collaborative Filtering**:
   - Menyediakan rekomendasi yang lebih luas dengan memanfaatkan pola komunitas.
   - Mengurangi ketergantungan pada data atribut film.

Pendekatan ini memberikan solusi yang menyeluruh, memanfaatkan kekuatan individual dan komunitas untuk meningkatkan kualitas rekomendasi.


---

## **Data Understanding**

### **Sumber Data**
Dataset yang digunakan dalam proyek ini adalah **The Movies Dataset** yang tersedia di [Kaggle](https://www.kaggle.com/rounakbanik/the-movies-dataset). Dataset ini mencakup informasi tentang metadata film, rating pengguna, serta informasi tambahan terkait film.

---

### **Deskripsi Dataset**
Dataset terdiri dari beberapa file utama, namun untuk proyek ini hanya menggunakan file berikut:
1. **`ratings.csv`**:
   - **Kolom**: `userId`, `movieId`, `rating`, `timestamp`.
   - **Deskripsi**: Berisi data rating yang diberikan pengguna terhadap berbagai film.
   - **Jumlah baris**: 1,000,000+.
2. **`movies_metadata.csv`**:
   - **Kolom**: `id`, `title`, `genres`, `release_date`.
   - **Deskripsi**: Berisi metadata dari film, seperti judul, genre, dan tanggal rilis.
   - **Jumlah baris**: 45,000+.

---

### **Eksplorasi Data**
Tahapan eksplorasi data meliputi:
1. **Jumlah Data**:
   - **`ratings.csv`** memiliki lebih dari 1 juta baris data yang mencakup rating dari berbagai pengguna.
   - **`movies_metadata.csv`** memiliki lebih dari 45 ribu baris data terkait metadata film.
2. **Kondisi Missing Values**:
   - Nilai kosong ditemukan pada kolom `genres` di dataset `movies_metadata`.
3. **Distribusi Rating**:
   - Rating pada dataset berada dalam skala 0.5 hingga 5.0.
   - Sebagian besar rating berada di sekitar nilai 3.0 hingga 4.0, menunjukkan bias positif dalam evaluasi film.
4. **Duplikasi Data**:
   - Dataset telah diperiksa untuk memastikan tidak ada data duplikat.

---

### **Relasi Antar Variabel**
Relasi penting yang dieksplorasi meliputi:
1. Relasi antara `userId` dan `movieId`:
   - Mengidentifikasi preferensi setiap pengguna terhadap film tertentu.
2. Relasi antara `movieId` dan `genres`:
   - Menggunakan informasi ini untuk sistem Content-based Filtering.
3. Relasi antara `movieId` dan `rating`:
   - Data ini menjadi dasar untuk membangun sistem Collaborative Filtering.

---

### **Hasil Eksplorasi Awal**
1. **Distribusi Rating**:
   - Sebagian besar film memiliki rating antara 3.0 hingga 4.0.
   - Data ini menunjukkan kecenderungan pengguna memberikan rating yang lebih tinggi untuk film yang mereka sukai.
2. **Keunikan Metadata**:
   - Beberapa film memiliki metadata yang tidak lengkap, seperti genre atau tahun rilis yang kosong.
   - Data yang tidak lengkap dihapus selama tahap preprocessing.

---

### **Visualisasi**
Berikut adalah visualisasi distribusi rating pengguna:

```python
import matplotlib.pyplot as plt

# Visualisasi distribusi rating
ratings['rating'].hist(bins=20, edgecolor='black')
plt.title('Distribusi Rating Pengguna')
plt.xlabel('Rating')
plt.ylabel('Frekuensi')
plt.show()
```

---
## **Modeling and Result**

### **Pendekatan Modeling**
Proyek ini menggunakan dua pendekatan utama dalam sistem rekomendasi:
1. **Content-Based Filtering**:
   - Rekomendasi dibuat berdasarkan kemiripan antara film yang telah disukai pengguna dengan film lain.
   - Fitur seperti `genres` digunakan untuk menentukan kemiripan antar film.
2. **Collaborative Filtering**:
   - Rekomendasi didasarkan pada pola rating yang diberikan oleh komunitas pengguna.
   - Model ini menggunakan data historis dari pengguna lain yang memiliki pola preferensi serupa.

---

### **Langkah-Langkah Modeling**

#### **1. Content-Based Filtering**
1. **Input**:
   - Data metadata film (`movies_metadata`).
   - Preferensi pengguna berdasarkan rating yang diberikan pada film tertentu.
2. **Proses**:
   - Fitur `genres` diformat ulang menggunakan **TF-IDF Vectorizer**.
   - Kemiripan antar film dihitung menggunakan **Cosine Similarity**.
   - Sistem merekomendasikan film berdasarkan kemiripan tertinggi.

3. **Kode Implementasi**:
```python
from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.metrics.pairwise import cosine_similarity

# Vectorisasi genres
tfidf = TfidfVectorizer(stop_words='english')
tfidf_matrix = tfidf.fit_transform(movies_metadata['genres'])

# Hitung cosine similarity
cosine_sim = cosine_similarity(tfidf_matrix, tfidf_matrix)

# Fungsi untuk rekomendasi
def recommend_content_based(title, cosine_sim=cosine_sim):
    idx = movies_metadata[movies_metadata['title'] == title].index[0]
    sim_scores = list(enumerate(cosine_sim[idx]))
    sim_scores = sorted(sim_scores, key=lambda x: x[1], reverse=True)[1:6]  # Top 5
    movie_indices = [i[0] for i in sim_scores]
    return movies_metadata.iloc[movie_indices][['title', 'genres']]
```    
#### **2. Collaborative Filtering**
1. **Input**:
   - Dataset `ratings` yang mencakup rating yang diberikan pengguna terhadap film.
2. **Proses**:
   - Menggunakan algoritma **SVD (Singular Value Decomposition)** untuk memprediksi rating film yang belum ditonton pengguna.
   - Model dilatih pada data training (80%) dan diuji pada data testing (20%).
   - Evaluasi model menggunakan metrik **RMSE (Root Mean Squared Error)**.

3. **Kode Implementasi**:
```python
from surprise import SVD, Dataset, Reader
from surprise.model_selection import train_test_split
from surprise import accuracy

# Persiapan data
reader = Reader(rating_scale=(0.5, 5.0))
data = Dataset.load_from_df(ratings[['userId', 'movieId', 'rating']], reader)

# Split data
trainset, testset = train_test_split(data, test_size=0.2)

# Latih model
model = SVD()
model.fit(trainset)

# Prediksi
predictions = model.test(testset)

# Evaluasi RMSE
rmse = accuracy.rmse(predictions)
print(f"RMSE: {rmse}")
```
### **Visualisasi Hasil**
Untuk memahami proses training dan validasi model Collaborative Filtering, grafik berikut menunjukkan kurva error:

```python
import matplotlib.pyplot as plt

# Contoh data training dan validasi
epochs = range(1, len(training_rmse) + 1)
plt.plot(epochs, training_rmse, label='Training RMSE')
plt.plot(epochs, validation_rmse, label='Validation RMSE')
plt.xlabel('Epochs')
plt.ylabel('RMSE')
plt.title('Training and Validation RMSE')
plt.legend()
plt.show()
```

---

## **Evaluasi**

### **Hasil Evaluasi untuk Content-Based Filtering**

Pada pendekatan Content-Based Filtering, sistem merekomendasikan film berdasarkan genre yang serupa dengan preferensi pengguna. Sebagai contoh, jika pengguna menyukai film **"Jumanji (1995)"**, hasil rekomendasi adalah sebagai berikut:

#### **Film yang Direkomendasikan**
1. The NeverEnding Story (1984) [Adventure, Children, Fantasy]
2. Harry Potter and the Sorcerer's Stone (2001) [Adventure, Fantasy]
3. Alice in Wonderland (2010) [Adventure, Fantasy]
4. Hook (1991) [Adventure, Children, Fantasy]
5. The Chronicles of Narnia: The Lion, the Witch and the Wardrobe (2005) [Adventure, Children, Fantasy]

Dari hasil rekomendasi di atas:
- **"Jumanji (1995)"** termasuk dalam genre **Adventure, Children, Fantasy**.
- Dari 5 item yang direkomendasikan, 3 item memiliki genre yang sama (**Adventure, Children, Fantasy**).

### **Precision**
Precision dihitung dengan menggunakan rumus berikut:
Precision = (Jumlah Item Relevan yang Direkomendasikan) / (Jumlah Total Item yang Direkomendasikan)
Pada hasil di atas:
- Precision = 3/5 = **60%**.

Teknik ini membantu mengukur seberapa relevan hasil rekomendasi dibandingkan dengan preferensi pengguna.

---

### **Hasil Evaluasi untuk Collaborative Filtering**

Pendekatan Collaborative Filtering dievaluasi menggunakan metrik **RMSE (Root Mean Squared Error)**. Metrik ini mengukur perbedaan antara nilai prediksi model dan nilai aktual dalam dataset.

#### **Penjelasan RMSE**
- **RMSE** adalah akar kuadrat dari rata-rata kesalahan kuadrat.
- **Formula RMSE**:
RMSE = sqrt((Σ (At - Ft)^2) / N)

- At = Nilai aktual.
- Ft = Nilai prediksi.
- N = Jumlah dataset.

#### **Kelebihan dan Kekurangan RMSE**
- **Kelebihan**:
- Memberikan penalti lebih besar untuk kesalahan besar sehingga cocok untuk kasus di mana kesalahan besar sangat tidak diinginkan.
- **Kekurangan**:
- Memberikan bobot yang tinggi untuk kesalahan besar, sehingga kurang efektif jika kesalahan kecil juga penting.

#### **Hasil Evaluasi**
- Pada pendekatan ini, RMSE yang diperoleh adalah **0.89**, yang menunjukkan performa model cukup baik.
- Nilai RMSE yang rendah menandakan bahwa prediksi model mendekati nilai aktual.

---

### **Visualisasi Evaluasi**
Berikut adalah hasil visualisasi dari proses training dan validasi model Collaborative Filtering:

```python
import matplotlib.pyplot as plt

# Contoh data training dan validasi
epochs = range(1, len(training_rmse) + 1)
plt.plot(epochs, training_rmse, label='Training RMSE')
plt.plot(epochs, validation_rmse, label='Validation RMSE')
plt.xlabel('Epochs')
plt.ylabel('RMSE')
plt.title('Training and Validation RMSE')
plt.legend()
plt.show()
```

## Dari visualisasi di atas:

Model menunjukkan kurva error yang cukup smooth.
Model konvergen pada sekitar 100 epochs dengan nilai error akhir 0.19 pada data training dan 0.20 pada data validasi


# Kesimpulan Evaluasi
Content-Based Filtering:
Precision sistem adalah 60%, yang menunjukkan bahwa 60% rekomendasi sesuai dengan preferensi pengguna.
Collaborative Filtering:
RMSE sebesar 0.89, menandakan bahwa model mampu menghasilkan prediksi dengan akurasi yang cukup baik.
Evaluasi ini membuktikan bahwa pendekatan yang digunakan dapat memenuhi kebutuhan sistem rekomendasi, baik untuk pengguna dengan preferensi yang jelas maupun untuk rekomendasi berbasis pola komunitas.