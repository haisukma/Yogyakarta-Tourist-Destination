# Laporan Proyek Machine Learning - Diajeng Mahai Sukma

## Project Overview
Dalam era digital yang semakin pesat, industri pariwisata mengalami transformasi yang signifikan. Jumlah destinasi wisata yang semakin beragam, serta volume informasi yang melimpah membuat wisatawan seringkali kebingungan dalam memilih destinasi yang sesuai dengan minat dan preferensinya. Di sinilah peran sistem rekomendasi menjadi sangat krusial. Sistem rekomendasi dapat membantu wisatawan menemukan destinasi wisata yang relevan dan menarik, sehingga meningkatkan kepuasan wisatawan dan memaksimalkan pengalaman berwisata.

Proyek sistem rekomendasi destinasi wisata di Yogyakarta menggunakan pendekatan collaborative filtering memiliki potensi yang sangat besar untuk memberikan manfaat bagi berbagai pihak, termasuk:
- Wisatawan, Sistem dapat memberikan rekomendasi destinasi wisata yang sesuai dengan preferensi dan minat individu, sehingga pengalaman wisata menjadi lebih menyenangkan dan memuaskan
- Pemerintah Daerah, Sistem dapat membantu mempromosikan destinasi wisata yang kurang populer, sehingga distribusi kunjungan wisatawan menjadi lebih merata.
- Pemilik Usaha Pariwisata, Dengan adanya rekomendasi dari sistem, diharapkan dapat meningkatkan jumlah pengunjung ke tempat wisata atau usaha pariwisata yang mereka miliki.

## Business Understanding
Sebelum menentukan daftar tujuan perjalanan, seseorang perlu memiliki gambaran umum tentang tempat-tempat tersebut. Yogyakarta punya destinasi wisata yang lebih dari cukup, tapi bagaimana situasi pariwisatanya pasca-COVID-19? Pada bulan Oktober 2021, sektor pariwisata di Indonesia kembali bangkit setelah jeda pandemi. Proyek ini berisi destinasi wisata terpopuler di Yogyakarta berdasarkan pengguna lokal, rating, dan tempat.

## Latar Belakang Pemilihan Masalah
Pemilihan masalah ini didasarkan pada beberapa faktor:
- Potensi pariwisata Yogyakarta: Yogyakarta merupakan salah satu destinasi wisata favorit di Indonesia. Dengan membuat sistem rekomendasi, diharapkan dapat meningkatkan daya tarik Yogyakarta sebagai destinasi wisata.
- Perkembangan teknologi: Kemajuan teknologi informasi memungkinkan pengembangan sistem rekomendasi yang lebih canggih dan personal.
- Kebutuhan pengguna: Banyak pengguna yang mencari rekomendasi tempat wisata yang sesuai dengan minat dan preferensi mereka.

Selain itu, pemilihan masalah ini juga relevan dengan:
- Peningkatan persaingan di sektor pariwisata: Dengan semakin banyaknya pilihan destinasi wisata, setiap daerah perlu memberikan nilai tambah agar tetap menarik minat wisatawan.
- Perkembangan teknologi informasi dan komunikasi: Penggunaan smartphone dan internet semakin meluas, sehingga sistem rekomendasi berbasis online menjadi sangat relevan.

## Problem Statement
- Bagaimana membangun sebuah sistem yang dapat memberikan rekomendasi destinasi wisata di Yogyakarta secara personal kepada pengguna, berdasarkan preferensi dan perilaku pengguna lainnya yang memiliki minat serupa?
- Bagaimana meningkatkan visibilitas destinasi wisata yang kurang populer di Yogyakarta melalui sistem rekomendasi yang efektif?

## Goals
- Membantu pengguna menemukan destinasi wisata yang sesuai dengan minat dan preferensi mereka secara cepat dan efisien.
- Membantu mempromosikan destinasi wisata di Yogyakarta, terutama destinasi yang kurang populer.

## Data Understanding
Dalam proyek ini penulis mengambil 3 dataset dari situs [Kaggle](https://www.kaggle.com/code/rizkymuhamad/yogyakarta-tourist-destination/input?select=tourism_rating.csv) yang kemudian dataset tersebut digabungkan untuk menambah informasi. Berikut rincian dataset: 
1. Tourism_with_Id.csv yang berisi informasi 5 kota besar di Indonesia, untuk kasus ini hanya Yogyakarta yang akan digunakan. Dataset ini berisi 126 baris yang terdiri dari 11 kolom:
- Place_Id : Sebagai identitas unik untuk setiap tempat wisata
- Place_Name : Nama resmi atau nama populer dari tempat wisata
- Description : Deskripsi singkat mengenai tempat wisata, seperti sejarah, keunikan, atau aktivitas yang bisa dilakukan
- Category :  Klasifikasi tempat wisata berdasarkan jenisnya
- City : Kota atau wilayah di mana tempat wisata berada
- Price : Harga tiket masuk ke tempat wisata
- Rating : Penilaian rata-rata yang diberikan oleh pengunjung sebelumnya
- Time Minutes : Estimasi waktu yang dibutuhkan untuk mengunjungi tempat wisata
- Coordinate : Koordinat geografis dari tempat wisata
- Latitude : Koordinat lintang dari tempat wisata
- Longitude : Koordinat bujur dari tempat wisata
Kondisi dataset ini masih terdapat 66 missing value pada kolom time minutes.
2. User.csv yang berisi informasi pengguna untuk membuat fitur rekomendasi. Dataset ini berisi 300 baris yang terdiri dari 3 kolom: 
- User_Id : Identitas unik yang diberikan kepada setiap pengguna sistem
- Location : Informasi mengenai lokasi atau kota tempat tinggal pengguna
- Age : Usia dari pengguna
3. Tourism_rating yang berisi informasi pengguna, destinasi wisata, dan rating untuk membuat sistem rekomendasi berdasarkan rating. Dataset ini berisi 10000 baris yang terdiri dari 3 kolom:
- User_Id : Identitas unik yang diberikan kepada setiap pengguna sistem
- Place_Id : Identitas unik yang diberikan kepada setiap tempat wisata
- Rating : Nilai numerik yang diberikan oleh pengguna untuk menilai suatu tempat wisata

Pada tahap ini juga dilakukan Exploratory Data Analysis yang berguna untuk memahami karakteristik data.Terdapat beberapa insight yang menarik dari tahapan ini yaitu:
- Top 3 Destinasi dengan rating tertinggi yaitu Taman Sungai Mudal, Pantai Ngandong, Pantai Kesirat.
- Kategori pariwisata dengan rating tertinggi yaitu Taman Hiburan.
- Sebagian besar pengunjung berusia antara 25 hingga 35 tahun.
- Asal pengunjung paling banyak dari daerah Bekasi

## Data Preparation
Pra-pemrosesan data dilakukan untuk memastikan kualitas dan kesesuaian data sebelum dilakukan pemodelan. Langkah-langkah yang dilakukan meliputi:
1. Penghapusan kolom unnamed: 11 dan unnamed: 12 karena tidak memiliki informasi yang relevan dan berpotensi mengganggu proses modeling.
2. Melakukan merge dengan tujuan utamanya adalah untuk menambahkan informasi tambahan.
3. Encoding fitur kategorikal, fitur-fitur kategorikal seperti kota_asal dan kategori_pariwisata diubah menjadi representasi numerik.
4. Pembagian Data, Data dibagi menjadi data latih (80%) dan data uji (20%) secara acak. Data latih digunakan untuk melatih model, sedangkan data uji digunakan untuk mengevaluasi kinerja model.

Dengan melakukan preparation data, diharapkan model yang dibangun dapat memberikan hasil prediksi yang lebih akurat dan reliabel.

## Modeling
Disini penulis menggunakan model RecommenderNet. RecommenderNet adalah model yang kuat dan fleksibel untuk membangun sistem rekomendasi yang efektif. Dengan kemampuannya untuk mengatasi masalah cold-start, memberikan rekomendasi yang lebih personal, dan menangani dataset besar, model ini telah menjadi pilihan populer dalam berbagai aplikasi rekomendasi.

Komponen Utama RecommenderNet:
1. Embedding User dan Item:
- Layer Embedding Pengguna: Menerjemahkan setiap pengguna ke dalam representasi vektor padat dalam ruang dimensi rendah. Embedding ini menangkap preferensi dan perilaku pengguna.
- Layer Embedding Item: Menerjemahkan setiap item (dalam hal ini, destinasi wisata) ke dalam representasi vektor padat. Embedding ini menangkap karakteristik item.
2. Layer Dot Product:
Menghitung dot product antara vektor pengguna dan item. Operasi ini mengukur kesamaan antara preferensi pengguna dan karakteristik item.
3. Layer Bias:
- Bias Pengguna: Menangkap tingkat preferensi keseluruhan pengguna.
- Bias Item: Menangkap popularitas keseluruhan item.
4. Fungsi Aktivasi:
Sigmoid: Output akhir dilewatkan melalui fungsi aktivasi sigmoid untuk menghasilkan skor probabilitas, yang menunjukkan kemungkinan pengguna menyukai item tertentu.
5. Optimizer: Adam dengan learning_rate sebesar 0.0004
6. Loss Function: Binary Crossentropy

Berdasarkan profil user 157 yang mungkin menyukai wisata alam dan memiliki anggaran menengah, model RecommenderNet merekomendasikan 7 destinasi wisata berikut:
| No | Place Name  |  Category | Entrace Fee  |  Rating |
|---|---|---|---|---|
| 1 | Pantai Baron          | Bahari        | 10000       | 4.4    |
| 2 | Pintoe Langit Dahromo | Cagar Alam    | 2500        | 4.4    |
| 3 | Pantai Wediombo       | Bahari        | 5000        | 4.5    |
| 4 | Pantai Sedahan        | Bahari        | 5000        | 4.5    |
| 5 | Desa Wisata Pulesari  | Taman Hiburan | 0           | 4.4    |
| 6 | Taman Sungai Mudal    | Cagar Alam    | 10000       | 4.6    |
| 7 | Pantai Congot         | Bahari        | 3000        | 4.3    |

## Evaluasi
Pada tahap evaluasi digunakan metrik Root Mean Square Error, yang merupakan metrik yang digunakan untuk mengukur rata-rata perbedaan antara nilai prediksi model dengan nilai aktual. Nilai RMSE yang lebih kecil menunjukkan bahwa model memiliki akurasi yang lebih baik.

RMSE Train = 0.3915: Nilai RMSE pada data latih menunjukkan bahwa rata-rata kesalahan prediksi model pada data yang telah digunakan untuk melatih model adalah 0.3915.

RMSE Validation = 0.3490: Nilai RMSE pada data validasi (atau data uji) menunjukkan bahwa rata-rata kesalahan prediksi model pada data yang belum pernah dilihat sebelumnya adalah 0.3490.

Berdasarkan nilai RMSE, dapat disimpulkan bahwa:
Model telah berhasil dilatih: Nilai loss yang terus menurun menunjukkan bahwa model telah belajar dari data.

Dampak dari model yang telah penulis buat mampu menjawab problem statement yang ada yaitu :
- Dengan model RecomenderNet dapat dibangun sebuah sistem yang dapat memberikan rekomendasi destinasi wisata di Yogyakarta secara personal kepada pengguna, berdasarkan preferensi dan perilaku pengguna lainnya yang memiliki minat serupa.
- Model ini dapat meningkatkan visibilitas destinasi wisata yang kurang populer di Yogyakarta.
