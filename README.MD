# Laporan Proyek Machine Learning - Mohamed

## Project Overview

Pada bagian ini, Kamu perlu menuliskan latar belakang yang relevan dengan proyek yang diangkat.

**Rubrik/Kriteria Tambahan (Opsional)**:
- Jelaskan mengapa dan bagaimana masalah tersebut harus diselesaikan
- Menyertakan hasil riset terkait atau referensi. Referensi yang diberikan harus berasal dari sumber yang kredibel dan author yang jelas.
- Format Referensi dapat mengacu pada penulisan sitasi [IEEE](https://journals.ieeeauthorcenter.ieee.org/wp-content/uploads/sites/7/IEEE_Reference_Guide.pdf), [APA](https://www.mendeley.com/guides/apa-citation-guide/) atau secara umum seperti [di sini](https://penerbitdeepublish.com/menulis-buku-membuat-sitasi-dengan-mudah/)
- Sumber yang bisa digunakan [Scholar](https://scholar.google.com/)

### Referensi

Kurmashov, N., Latuta, K., & Nussipbekov, A. (2015, September). Online book recommendation system. In 2015 Twelve International Conference on Electronics Computer and Computation (ICECCO) (pp. 1-4). IEEE.


--------

## Business Understanding

Pada bagian ini, Anda perlu menjelaskan proses klarifikasi masalah.

Bagian laporan ini mencakup:

### Problem Statements

Menjelaskan pernyataan masalah:
- Pernyataan Masalah 1
- Pernyataan Masalah 2
- Pernyataan Masalah n

### Goals

Menjelaskan tujuan proyek yang menjawab pernyataan masalah:
- Jawaban pernyataan masalah 1
- Jawaban pernyataan masalah 2
- Jawaban pernyataan masalah n

Semua poin di atas harus diuraikan dengan jelas. Anda bebas menuliskan berapa pernyataan masalah dan juga goals yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**:
- Menambahkan bagian “Solution Approach” yang menguraikan cara untuk meraih goals. Bagian ini dibuat dengan ketentuan sebagai berikut: 

    ### Solution statements
    - Mengajukan 2 atau lebih solution approach (algoritma atau pendekatan sistem rekomendasi).

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

#### 2. Ratings.csv
- Jumlah baris : 340556 sampel data
- Jumlah kolom : 8 kolom 
- Kondisi data : 
  - Jumlah missing value : 0
  - Jumlah duplicate value : 0
- Daftar kolom atau fitur :
    1. User-ID : merupakan ID unik dari user
    2. Location : merupakan tempat tinggal atau lokasi dimana user berada
    3. Age : merupakan nilai umur dari user
    
#### 3. Users.csv
- Jumlah baris : 340556 sampel data
- Jumlah kolom : 8 kolom 
- Kondisi data : 
  - Jumlah missing value : 110762
  - Jumlah duplicate value : 0
- Daftar kolom atau fitur :
    1. User-ID : merupakan ID unik dari user
    2. ISBN : merupakan ISBN dari buku
    3. Book-Rating : merupakan rating dari suatu buku dalam rentang 0-10


Terdapat beberapa file dataset yang memiliki missing value, mulai dari skala terkecil seperti pada file Books.csv sebanyak 7  hingga skala terbesar seperti pada  file Ratings.csv sebanyak 110762 , maka perlu untuk melihat distribusi dari data setiap fitur data agar dapat menentukan metode imputasi nilai null yang tepat.

**Rubrik/Kriteria Tambahan (Opsional)**:
- Melakukan beberapa tahapan yang diperlukan untuk memahami data, contohnya teknik visualisasi data beserta insight atau exploratory data analysis.

## Data Preparation
Pada bagian ini Anda menerapkan dan menyebutkan teknik data preparation yang dilakukan. Teknik yang digunakan pada notebook dan laporan harus berurutan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan proses data preparation yang dilakukan
- Menjelaskan alasan mengapa diperlukan tahapan data preparation tersebut.

## Modeling
Tahapan ini membahas mengenai model sisten rekomendasi yang Anda buat untuk menyelesaikan permasalahan. Sajikan top-N recommendation sebagai output.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menyajikan dua solusi rekomendasi dengan algoritma yang berbeda.
- Menjelaskan kelebihan dan kekurangan dari solusi/pendekatan yang dipilih.

## Evaluation
Pada bagian ini Anda perlu menyebutkan metrik evaluasi yang digunakan. Kemudian, jelaskan hasil proyek berdasarkan metrik evaluasi tersebut.

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.

**---Ini adalah bagian akhir laporan---**

_Catatan:_
- _Anda dapat menambahkan gambar, kode, atau tabel ke dalam laporan jika diperlukan. Temukan caranya pada contoh dokumen markdown di situs editor [Dillinger](https://dillinger.io/), [Github Guides: Mastering markdown](https://guides.github.com/features/mastering-markdown/), atau sumber lain di internet. Semangat!_
- Jika terdapat penjelasan yang harus menyertakan code snippet, tuliskan dengan sewajarnya. Tidak perlu menuliskan keseluruhan kode project, cukup bagian yang ingin dijelaskan saja.
