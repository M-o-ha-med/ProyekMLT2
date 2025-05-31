# Laporan Proyek Machine Learning - Mohamed

## Project Overview

Perkembangan teknologi informasi yang pesat telah mendorong digitalisasi di berbagai bidang, termasuk dalam dunia literasi dan perbukuan. Saat ini, banyak platform digital yang menyediakan ribuan hingga jutaan judul buku dalam berbagai genre, yang tentunya dapat membingungkan pengguna dalam memilih bacaan yang sesuai dengan minat dan kebutuhannya. Dalam konteks inilah sistem rekomendasi memiliki peran penting sebagai alat bantu untuk menyaring informasi dan memberikan saran personalisasi kepada pengguna.

Dilansir dari situs statista, penjualan ebooks atau buku elektronik dan audiobook meningkat secara signifikan dari tahun ke tahun dan diperkirakan akan terus meningkat hingga tahun 2029 yang menunjukkan pertumbuhan positif dan meningkatnya minat baca masyarakat di indonesia[1][2].

Sistem rekomendasi telah menjadi komponen utama dalam berbagai layanan digital seperti e-commerce, layanan streaming, hingga perpustakaan digital. Maka dari itu diperlukan pengembangan sistem rekomendasi yang dapat membantu meningkatkan penjualan buku baik itu ebook ataupun audiobook dengan memberikan rekomendasi yang relevan sesuai dengan preferensi dari pelanggan.

Sistem rekomendasi yang dibuat akan menggunakan dua pendekatan, yaitu collaborative filtering dan content-based filtering
penelitian terdahulu menunjukkan bahwa penerapan sistem rekomendasi untuk penjualan buku terbukti berhasil dalam meningkatkan jumlah penjualan buku secara signifikan [3][4].

**Rubrik/Kriteria Tambahan (Opsional)**:
- Jelaskan mengapa dan bagaimana masalah tersebut harus diselesaikan
- Menyertakan hasil riset terkait atau referensi. Referensi yang diberikan harus berasal dari sumber yang kredibel dan author yang jelas.
- Format Referensi dapat mengacu pada penulisan sitasi [IEEE](https://journals.ieeeauthorcenter.ieee.org/wp-content/uploads/sites/7/IEEE_Reference_Guide.pdf), [APA](https://www.mendeley.com/guides/apa-citation-guide/) atau secara umum seperti [di sini](https://penerbitdeepublish.com/menulis-buku-membuat-sitasi-dengan-mudah/)
- Sumber yang bisa digunakan [Scholar](https://scholar.google.com/)

### Referensi

[1] Statista, "Audiobooks - Indonesia," [Online]. Available: https://www.statista.com/outlook/amo/media/books/audiobooks/indonesia. [Accessed: 29-May-2025].

[2] Statista, "E-books - Indonesia," [Online]. Available: https://www.statista.com/outlook/amo/media/books/ebooks/indonesia. [Accessed: 29-May-2025].

[3] Kurmashov, N., Latuta, K., & Nussipbekov, A. (2015, September). Online book recommendation system. In 2015 Twelve International Conference on Electronics Computer and Computation (ICECCO) (pp. 1-4). IEEE.

[4] Rajpurkar, S., Bhatt, D., Malhotra, P., Rajpurkar, M. S. S., & Bhatt, M. D. R. (2015). Book recommendation system. International Journal for Innovative Research in Science & Technology, 1(11), 314-316.



--------

## Business Understanding

### Problem Statements

Menjelaskan pernyataan masalah:
- pendekatan manakah yang lebih efektif dalam membuat sistem rekomendasi ? apakah menggunakan collaborive filtering atau content-based filtering ?
- metrik apa saja yang akan digunakan dalam mengukur performa dari dua sistem rekomendasi ?
- apa saja kekurangan dan kelebihan dari sistem rekomendasi berdasarkan pendekatan collaborative filtering dan content-based filtering ? 

### Goals

Menjelaskan tujuan proyek yang menjawab pernyataan masalah:
- Untuk membuat sistem rekomendasi berdasarkan pendekatan collaborative filtering dan content-based filtering.
- Untuk mencari sistem rekomendasi terbaik berdasarkan pengukuran performa menggunakan metrik precision@k, recall@k dan precision.
- Untuk mengetahui kekurangan dan kelebihan dari sistem rekomendasi berdasarkan pendekatan collaborative filtering dan content-based filtering.

Semua poin di atas harus diuraikan dengan jelas. Anda bebas menuliskan berapa pernyataan masalah dan juga goals yang diinginkan.

### Solution statements
- Membuat dua model sistem rekomendasi menggunakan LightFM
- Membandingkan efektivitas kedua model menggunakan metrik pengukuran seperti precision@k, recall@k , dan precision.
- Melakukan evaluasi berdasarkan hasil pengukuran metrik untuk menentukan kelebihan serta kekurangan dari kedua model.

## Data Understanding
Dataset yang digunakan dalam proyek kali ini berasal dari kaggle, yaitu [Book Recommendation Dataset by Möbius - kaggle](https://www.kaggle.com/datasets/arashnic/book-recommendation-dataset). Terdapat 3 file dataset didalamnya berikut adalah daftar file-file dibawah ini : 

#### 1. Books.csv
- Jumlah baris : 271360 sampel data
- Jumlah kolom : 8 kolom 
- Kondisi data : 
  - Jumlah missing value : 7
  - Jumlah duplicate value : 0
- Daftar kolom atau fitur :
    1. ISBN : merupakan ISBN dari buku
    2. Book-Title : merupakan judul dari buku
    3. Book-Author : merupakan nama lengkap dari penulis
    4. Year-Of-Publication : merupakan tahun suatu buku diterbitkan
    5. Publisher : merupakan nama penerbit
    6. Image-URL-S : Thumbnail cover buku dalam ukuran kecil (S), menggunakan amazon link
    7. Image-URL-M : Thumbnail cover buku dalam ukuran sedang (M), menggunakan amazon link
    8. Image-URL-L : Thumbnail cover buku dalam ukuran besar (L), menggunakan amazon link
- Struktur data
    ```python
    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 271360 entries, 0 to 271359
    Data columns (total 8 columns):
     #   Column               Non-Null Count   Dtype 
    ---  ------               --------------   ----- 
     0   ISBN                 271360 non-null  object
     1   Book-Title           271360 non-null  object
     2   Book-Author          271358 non-null  object
     3   Year-Of-Publication  271360 non-null  object
     4   Publisher            271358 non-null  object
     5   Image-URL-S          271360 non-null  object
     6   Image-URL-M          271360 non-null  object
     7   Image-URL-L          271357 non-null  object
    dtypes: object(8)
    memory usage: 16.6+ MB
    ```

#### 2. Users.csv
- Jumlah baris : 340556 sampel data
- Jumlah kolom : 3 kolom 
- Kondisi data : 
  - Jumlah missing value : 110762
  - Jumlah duplicate value : 0
- Daftar kolom atau fitur :
    1. User-ID : merupakan ID unik dari user
    2. Location : merupakan tempat tinggal atau lokasi dimana user berada
    3. Age : merupakan nilai umur dari user
- Struktur data
    ```python
    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 278858 entries, 0 to 278857
    Data columns (total 3 columns):
     #   Column    Non-Null Count   Dtype  
    ---  ------    --------------   -----  
     0   User-ID   278858 non-null  int64  
     1   Location  278858 non-null  object 
     2   Age       168096 non-null  float64
    dtypes: float64(1), int64(1), object(1)
    memory usage: 6.4+ MB
    ```

    
#### 3. Ratings.csv
- Jumlah baris : 1149780 sampel data
- Jumlah kolom : 3 kolom 
- Kondisi data : 
  - Jumlah missing value : 0
  - Jumlah duplicate value : 0
- Daftar kolom atau fitur :
    1. User-ID : merupakan ID unik dari user
    2. ISBN : merupakan ISBN dari buku
    3. Book-Rating : merupakan rating dari suatu buku dalam rentang 0-10
- Struktur data
    ```python
    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 1149780 entries, 0 to 1149779
    Data columns (total 3 columns):
     #   Column       Non-Null Count    Dtype 
    ---  ------       --------------    ----- 
     0   User-ID      1149780 non-null  int64 
     1   ISBN         1149780 non-null  object
     2   Book-Rating  1149780 non-null  int64 
    dtypes: int64(2), object(1)
    memory usage: 26.3+ MB
    ```

Terdapat beberapa file dataset yang memiliki missing value, mulai dari skala terkecil seperti pada file Books.csv sebanyak 7 hingga skala terbesar seperti pada  file Users.csv sebanyak 110762 , maka perlu untuk melihat distribusi dari data setiap fitur data agar dapat menentukan metode imputasi nilai null yang tepat.

## Exploratory Data Analysis (EDA)

### Books.csv
#### Jumlah Data Null

| Kolom                 | Jumlah Null |
|-----------------------|--------------|
| ISBN                  | 0            |
| Book-Title            | 0            |
| Book-Author           | 2            |
| Year-Of-Publication   | 0            |
| Publisher             | 2            |
| Image-URL-S           | 0            |
| Image-URL-M           | 0            |
| Image-URL-L           | 3            |

#### Jumlah Data Duplikat

| Deskripsi              | Jumlah |
|------------------------|--------|
| Duplikasi pada dataset | 0      |

### Jumlah Data Null

| Kolom                 | Jumlah Null |
|-----------------------|--------------|
| ISBN                  | 0            |
| Book-Title            | 0            |
| Book-Author           | 2            |
| Year-Of-Publication   | 0            |
| Publisher             | 2            |
| Image-URL-S           | 0            |
| Image-URL-M           | 0            |
| Image-URL-L           | 3            |

### Jumlah Data Duplikat

| Deskripsi              | Jumlah |
|------------------------|--------|
| Duplikasi pada dataset | 0      |

### Jumlah Data Null

| Kolom                 | Jumlah Null |
|-----------------------|--------------|
| ISBN                  | 0            |
| Book-Title            | 0            |
| Book-Author           | 2            |
| Year-Of-Publication   | 0            |
| Publisher             | 2            |
| Image-URL-S           | 0            |
| Image-URL-M           | 0            |
| Image-URL-L           | 3            |

### Jumlah Data Duplikat

| Deskripsi              | Jumlah |
|------------------------|--------|
| Duplikasi pada dataset | 0      |


**Rubrik/Kriteria Tambahan (Opsional)**:
- Melakukan beberapa tahapan yang diperlukan untuk memahami data, contohnya teknik visualisasi data beserta insight atau exploratory data analysis.

## Data Preparation
Pada bagian ini Anda menerapkan dan menyebutkan teknik data preparation yang dilakukan. Teknik yang digunakan pada notebook dan laporan harus berurutan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan proses data preparation yang dilakukan
- Menjelaskan alasan mengapa diperlukan tahapan data preparation tersebut.

## Modeling
### Collaborative Filtering (LightFM + WARP-KOS)
Model ini menggunakan interaksi historis antara pengguna dan buku dalam bentuk implicit feedback (misalnya rating), tanpa menggunakan informasi konten buku. LightFM digunakan sebagai algoritma dengan loss function WARP-KOS yang mengutamakan performa ranking.

$$\hat{r}_{u,i} = \mathbf{p}_u^\top \mathbf{q}_i + b_u + b_i$$

**Keterangan:**

* $\hat{r}_{u,i}$ = skor prediksi untuk interaksi antara user $u$ dan item $i$
* $\mathbf{p}_u$ = vektor representasi laten untuk user $u$
* $\mathbf{q}_i$ = vektor representasi laten untuk item $i$
* $b_u$ = bias untuk user $u$
* $b_i$ = bias untuk item $i$

---

Loss function WARP-KOS (Weighted Approximate-Rank Pairwise - k-Order Statistic):

![WARP-KOS Loss](https://latex.codecogs.com/png.image?\dpi{150}&space;\mathcal{L}=-\sum_{(u,i,j)}\log\sigma(\hat{r}_{u,i}-\hat{r}_{u,j}))



**Keterangan:**

* $\mathcal{L}$ = total loss yang diminimalkan selama training
* $\sigma$ = fungsi sigmoid
* $\hat{r}_{u,i}$ = skor prediksi user $u$ terhadap item positif $i$
* $\hat{r}_{u,j}$ = skor prediksi user $u$ terhadap item negatif $j$
* $i \in \text{positive items}$, $j \in \text{negative samples}$

WARP-KOS bekerja dengan men-sampling item negatif $j$ hingga ditemukan satu yang skor prediksinya lebih tinggi dari item positif $i$, lalu menghitung loss berdasarkan perbedaan skor.

#### Kelebihan

* Efektif untuk data dengan interaksi yang sparse
* Tidak memerlukan metadata atau fitur konten tambahan
* Fokus pada peningkatan ranking item relevan

#### Kekurangan

* Tidak dapat menangani cold-start item atau user baru
* Bergantung pada interaksi historis yang cukup untuk performa optimal

---

### Content-Based Filtering (LightFM + WARP-KOS)

Model ini juga menggunakan LightFM dengan WARP-KOS, namun ditambahkan fitur konten dari item seperti judul, penulis, atau kategori buku. Fitur-fitur ini digunakan untuk membuat representasi tambahan item sehingga memungkinkan sistem merekomendasikan buku berdasarkan kemiripan konten.

$$ \hat{r}_{u,i} = \mathbf{p}_u^\top \mathbf{q}_i + b_u + b_i $$

**Keterangan:**

* $\hat{r}_{u,i}$ = skor prediksi untuk interaksi antara user $u$ dan item $i$
* $\mathbf{p}_u$ = vektor representasi laten untuk user $u$
* $\mathbf{q}_i$ = vektor representasi laten untuk item $i$
* $b_u$ = bias untuk user $u$
* $b_i$ = bias untuk item $i$

---

Loss function WARP-KOS (Weighted Approximate-Rank Pairwise - k-Order Statistic):

![WARP-KOS Loss](https://latex.codecogs.com/png.image?\dpi{150}&space;\mathcal{L}=-\sum_{(u,i,j)}\log\sigma(\hat{r}_{u,i}-\hat{r}_{u,j}))



**Keterangan:**

* $\mathcal{L}$ = total loss yang diminimalkan selama training
* $\sigma$ = fungsi sigmoid
* $\hat{r}_{u,i}$ = skor prediksi user $u$ terhadap item positif $i$
* $\hat{r}_{u,j}$ = skor prediksi user $u$ terhadap item negatif $j$
* $i \in \text{positive items}$, $j \in \text{negative samples}$

WARP-KOS bekerja dengan men-sampling item negatif $j$ hingga ditemukan satu yang skor prediksinya lebih tinggi dari item positif $i$, lalu menghitung loss berdasarkan perbedaan skor.


#### Kelebihan

* Dapat memberikan rekomendasi untuk item baru (cold-start)
* Tidak bergantung pada interaksi antar pengguna
* Dapat menjelaskan alasan rekomendasi karena berdasarkan fitur nyata

#### Kekurangan

* Bergantung pada kualitas dan kelengkapan data konten
* Rentan terhadap overspecialization jika fitur terlalu terbatas

---
#### Top-N Recommendation Output

Contoh hasil top-5 rekomendasi untuk pengguna:

1. "Angels and Demons" by Dan Brown
2. "The Da Vinci Code" by Dan Brown
3. "Digital Fortress"
4. "Deception Point"
5. "Inferno"

#### Tentang WARP-KOS

WARP-KOS merupakan loss function yang dirancang untuk memaksimalkan ranking item yang relevan. Loss ini bekerja dengan memilih item negatif secara acak hingga ditemukan satu yang lebih tinggi skornya daripada item positif, dan menghitung loss berdasarkan estimasi ranking tersebut. Loss ini sangat efisien untuk skenario top-N recommendation dan ranking-based learning.

---

#### Kesimpulan

Kedua model menggunakan algoritma yang sama yaitu LightFM dengan WARP-KOS, namun dengan pendekatan fitur yang berbeda. Model pertama (Collaborative) unggul dari segi precision, sementara model kedua (Content-Based) unggul dari sisi recall. Pemilihan model dapat disesuaikan dengan tujuan sistem rekomendasi, dan kombinasi dari keduanya bisa dipertimbangkan untuk meningkatkan performa sistem.


### Evaluation

#### Precision\@K

$$\text{Precision@K} = \frac{|\text{Recommended items} \cap \text{Relevant items}|}{K}$$

**Keterangan:**

* $\text{Recommended items}$ = daftar item yang direkomendasikan oleh sistem
* $\text{Relevant items}$ = daftar item yang benar-benar relevan berdasarkan data ground truth
* $K$ = jumlah item rekomendasi teratas yang dievaluasi
* Precision\@K mengukur seberapa banyak dari $K$ rekomendasi yang benar-benar relevan

---

#### Recall\@K

$$\text{Recall@K} = \frac{|\text{Recommended items} \cap \text{Relevant items}|}{|\text{Relevant items}|}$$

**Keterangan:**

* $|\text{Relevant items}|$ = total jumlah item relevan untuk user tersebut
* Recall\@K mengukur seberapa banyak item relevan yang berhasil ditemukan dari seluruh item relevan yang tersedia

#### Hasil Evaluasi

| Model                                        | Precision\@K     | Recall\@K             |
| -------------------------------------------- |------------------|-----------------------|
| Collaborative Filtering (LightFM + WARP-KOS) | 0.24222705       | 0.9596145774803346    |
| Content-Based Filtering (LightFM + WARP-KOS) | 0.2263196        | 0.9290151944489016    |

#### Interpretasi

* Collaborative Filtering memberikan precision lebih tinggi, yang menunjukkan bahwa model ini memberikan lebih banyak rekomendasi yang relevan dalam daftar teratas.
* Content-Based Filtering memiliki recall yang lebih tinggi, menunjukkan cakupan yang lebih luas terhadap item relevan.
* Kedua pendekatan saling melengkapi dan bisa digabungkan untuk pendekatan hybrid.

