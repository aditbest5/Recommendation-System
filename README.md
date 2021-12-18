# Laporan Proyek Machine Learning - Aditya Aprianto

## Project Overview
- **Latar Belakang**

    Film animasi menjadi suatu daya tarik bagi kaum anak-anak, remaja, hingga dewasa. Tidak sedikit juga seseorang yang beranjak dewasa masih mengikuti perkembangan dunia animasi, khususnya anime. Website-website ataupun platform penyedia film anime juga sudah banyak di perangkat android, iOS, ataupun PC. Seringkali setiap kita selesai menonton suatu serial anime, kita akan disuguhkan film anime selanjutnya yang mungkin akan kita tonton. Dibalik itu semua, ada sistem rekomendasi yang berperan penting untuk menyarankan pengguna menonton film anime yang mungkin disukai pengguna. Oleh sebab itu, penulis mencoba untuk membuat sistem rekomendasi untuk menyarankan pengguna menonton sebuah anime dalam sebuah top list.

    Sistem rekomendasi memiliki peran yang penting pada platform aplikasi. Tidak hanya untuk penyedia layanan streaming film saja, tetapi platform aplikasi seperti e-commerce, social media, education, dan lainnya memiliki sistem rekomendasi. Dengan adanya sistem rekomendasi, platform aplikasi dapat memberikan pengalaman yang menyenangkan kepada pengguna. Karena fitur rekomendasi dapat memudahkan pengguna dalam memenuhi kebutuhan mereka serta minat mereka. 
    
    
## Business Understanding

Sebuah platform penyedia layanan streaming anime ingin memberikan suguhan koleksi film anime terbaik mereka kepada pengguna setianya. Dalam memberikan layanan terbaik, sebuah platform penyedia layanan harus menyarankan anime apa saja yang mungkin disukai oleh pengguna menurut data historis mereka. Platform layanan tersebut dapat menggunakan sistem rekomendasi berbasis machine learning dalam merekomendasikan serial anime favorit penggunanya dengan baik. Platform tersebut mempunyai data nama anime, genre anime, user_id, rating, dan lain-lain dalam 2(dua) buah file terpisah yakni anime.csv dan rating.csv. Mereka harus mengolah data tersebut agar bisa membuat model sistem rekomendasi yang tepat kepada pengguna mereka.

### Problem Statements

Berdasarkan latar belakang diatas, berikut rincian masalah yang dapat diselesaikan pada proyek ini :

- Bagaimana cara melakukan pra-pemrosesan data anime.csv dan rating.csv dengan baik?
- Bagaimana cara membuat model _machine learning_ untuk merekemondesikan film anime berdasarkan data pengguna?

### Goals

Adapun tujuan dibuatnya proyek ini, yaitu:
- Melakukan pra-pemrosesan data anime.csv dan rating.csv dengan baik agar dapat digunakan dalam membuat model.
- Membuat sebuah model _machine learning_ yang dapat merekomendasikan film anime kepada pengguna.

### Solution statements
Solusi yang dapat diterapkan untuk proyek ini antara lain:

-   Pada tahap pra-pemrosesan data dapat dilakukan beberapa teknik, diantaranya :

    -   Handling missing value pada data
    -   Melakukan merging / penggabungan kedua dataset kedalam satu dataframe
    -   Melakukan cleaning pada judul anime

- Pada tahap pemodelan dilakukan metode content-based filtering. Content-based filtering mempelajari profil minat pengguna baru berdasarkan data dari objek yang telah dinilai pengguna. Algoritma ini bekerja dengan menyarankan item serupa yang pernah disukai di masa lalu atau sedang dilihat di masa kini kepada pengguna. Semakin banyak informasi yang diberikan pengguna, semakin baik akurasi sistem rekomendasi.



## Data Understanding

Dataset yang saya gunakan pada kasus ini  ada 2 (dua) buah dataset yakni anime.csv dan rating.csv bersumber dari kaggle [Anime Recommendations Database
](https://www.kaggle.com/CooperUnion/anime-recommendations-database). Berkas anime.csv ini berisi informasi anime id, name, genre, type, episodes, rating, dan members.  Terdapat 4 buah data bertipe rasio (tipe data object) dan 3 buah data numerik (tipe data float64 dan int64).  Untuk penjelasan mengenai variabel-variable pada data anime.csv dapat dilihat pada poin-poin berikut yang memiliki dimensi 12294 rows × 7 columns dengan variabel-variabelnya antara lain:

*   anime_id - unique id yang mengidentifikasikan sebuah anime
*   name - nama lengkap anime
*   genre - kategori anime
*   type - movie, TV, OVA, dan lain-lain
*   episodes - berapa banyak episode anime (1 jika movie)
*   rating - rata-rata rating anime kisaran 0-10 
*   members - jumlah member di sebuah komunitas grup anime

Dataset kedua yakni rating.csv. Dataset ini berisi informasi user id, anime id, dan rating. Didalam dataset ini terdapat 3 buah data numerik (tipe data int64).  Untuk penjelasan mengenai variabel-variable pada data rating.csv dapat dilihat pada poin-poin berikut yang memiliki dimensi 7813737 rows × 3 columns dengan variabel-variabelnya antara lain:

*   user_id - non identifiable randomly generated user id.
*   anime_id - anime yang telah dinilai pengguna ini.
*   rating - rating dari 10 yang telah ditetapkan pengguna ini (-1 jika pengguna menontonnya tetapi tidak memberikan peringkat).


### Data Visualization

Dibawah ini merupakan hasil visualisasi top 10 anime berdasarkan jumlah rating :

![Top 10 Anime Rating](https://raw.githubusercontent.com/aditbest5/Recommendation-System/main/File%20Gambar/Top%2010%20anime%20rating.png)

Dibawah ini merupakan adalah hasil visualisasi chart pie dari media streaming:

![Chart Pie](https://raw.githubusercontent.com/aditbest5/Recommendation-System/main/File%20Gambar/Media%20streaming.png)

Dan yang terakhir adalah hasil visualisasi genre word cloud yang memperlihatkan genre terbanyak pada data :

![Word Cloud](https://raw.githubusercontent.com/aditbest5/Recommendation-System/main/File%20Gambar/Word%20cloud.png)



## Data Preparation
Seperti yang telah disebutkan di bagian solution statement, berikut tahapan-tahapan dalam melakukan pra-pemrosesan data:

- **Handling missing value pada data**

    ![Data NaN](https://raw.githubusercontent.com/aditbest5/Recommendation-System/main/File%20Gambar/anime%20null.png)
    
   ![Data NaN](https://raw.githubusercontent.com/aditbest5/Recommendation-System/main/File%20Gambar/rating%20null.png)
    
     Dari data anime.csv terlihat terdapat nilai null pada kolom genre, type, dan rating. Sedangkan pada data rating.csv tidak terdapat nilai null. Oleh karena itu penulis mencoba menghilangkan nilai null pada data anime.csv. Selain menghilangkan nilai null pada kedua dataset, penulis juga melakukan pengecekan pada nilai NaN dan null setelah dilakukan merging dataset.
     
    
 - **Melakukan merging / penggabungan kedua dataset kedalam satu dataframe**

    Merging data dilakukan ketika ada 2 (dua) buah dataset kedalam satu buah dataframe. Merging memudahkan kita untuk mengolah kedua dataset menjadi data yang bersih untuk selanjutnya dimasukkan kedalam sebuah model. Library pandas memiliki fungsi untuk melakukan merging menggunakan _pd.merge_.

 - **Melakukan cleaning pada judul anime**

    Sebelum memasukan data kedalam model, judul anime harus dibersihkan terlebih dahulu agar dapat merekomendasikan sesuai judul terkait. Karena penggunaan sistem rekomendasi ini berdasarkan judul anime dan genre anime yang mirip. Penulis membuat sebuah fungsi baru nameCleaning(text) dan mengembalikan nilai text. 
    
## Modeling

Setelah melakukan pra-pemrosesan data yang baik, pada tahap modeling akan dilakukan metode _content-based filtering_ dengan menggunakan fungsi tfidfvectorizer() dari library sklearn. Rekomendasi berbasis konten bekerja dengan data yang diberikan pengguna, baik secara eksplisit (peringkat) atau implisit (mengklik tautan). Berdasarkan data tersebut, profil pengguna yang kemudian digunakan untuk memberikan saran kepada pengguna. Saat pengguna memberikan lebih banyak masukan atau mengambil tindakan berdasarkan rekomendasi, mesin menjadi lebih akurat. Sedangkan Term Frequency — Inverse Document Frequency atau TF — IDF adalah suatu metode algoritma yang berguna untuk menghitung bobot setiap kata yang umum digunakan. Metode ini juga terkenal efisien, mudah dan memiliki hasil yang akurat. Metode ini akan menghitung nilai Term Frequency (TF) dan Inverse Document Frequency (IDF) pada setiap token (kata) di setiap dokumen dalam korpus. Secara sederhana, metode TF-IDF digunakan untuk mengetahui berapa sering suatu kata muncul di dalam dokumen. Di sini penulis akan menggunakannya pada genre sehingga model dapat merekomendasikan pengguna berdasarkan konten genre.

Selain TF-IDF,  fungsi sigmoid_kernel digunakan untuk menghitung kernel sigmoid antara dua vektor. Kernel sigmoid juga dikenal sebagai tangen hiperbolik, atau Multilayer Perceptron (karena didalam bidang jaringan saraf sering digunakan sebagai fungsi aktivasi neuron).

Setelah penggunaan TF-IDF dan sigmoid_kernel, penulis membuat fungsi anime_rec untuk mendapatkan rekomendasi anime. Fungsi ini mengubah skor kesamaan menjadi daftar menggunakan fungsi enumerate, mengurutkan daftar dan memilih 10 skor teratas untuk rekomendasi. 

Pada tabel dibawah ini menunjukan hasil dari model rekomendasi yang menampilkan 10 film anime yang berkaitan:
|       | Nama Anime                                                                            | Genre                                                         | Rating    |
|------ | --------------------------------------------------------------------------------------| ------------------------------------------------------------- | --------- |
|   0   | One Piece: Episode of Merry - Mou Hitori no Nakama no Monogatari                      |Action, Adventure, Comedy, Drama, Fantasy, Shounen, Super Power|   8.29    |
|   1   | One Piece: Episode of Nami - Koukaishi no Namida to Nakama no Kizuna                  |Action, Adventure, Comedy, Drama, Fantasy, Shounen, Super Power|   8.27    |
|   2   | One Piece: Episode of Sabo - 3 Kyoudai no Kizuna Kiseki no Saikai to Uketsugareru Ishi|Action, Adventure, Comedy, Drama, Fantasy, Shounen, Super Power|   7.78    |
|   3   | One Piece Film: Strong World                                                          |Action, Adventure, Comedy, Drama, Fantasy, Shounen             |   8.42    |
|   4   | One Piece Film: Z	                                                                    |Action, Adventure, Comedy, Drama, Fantasy, Shounen             |   8.39    |
|   5   | One Piece Film: Gold                                                                  |Action, Adventure, Comedy, Drama, Fantasy, Shounen             |   8.32    |
|   6   | One Piece: Heart of Gold                                                              |Action, Adventure, Comedy, Drama, Fantasy, Shounen             |   7.75    |
|   7   | Digimon Frontier                                                                      |Action, Adventure, Comedy, Drama, Fantasy, Shounen             |   7.25    |
|   8   | Digimon Tamers                                                                        |Adventure, Comedy, Drama, Fantasy, Shounen                     |   7.65    |
|   9   | Digimon Savers	                                                                    |Adventure, Comedy, Drama, Fantasy, Shounen                     |   7.1     |

## Evaluation

# Metriks Evaluasi
Pada metode _content-based filtering_ ini penulis menggunakan metriks _precision_. Presisi merupakan metrik biner yang digunakan untuk mengevaluasi model dengan keluaran biner. Precision digunakan untuk menghitung jumlah item rekomendasi yang relevan. Berikut rumus precision pada sistem rekomendasi :

 ![precision_metrics](https://raw.githubusercontent.com/aditbest5/Recommendation-System/main/File%20Gambar/Metrics%20precision.png)
 
 Dari hasil top 10 recommendation didapatkan sebanyak 7 item yang relevan dari 10 item yang direkomendasikan sesuai dengan judul anime dan genre. Jika dihitung dengan metriks _precision_ maka hasilnya seperti berikut :
 
 $$P=7/10$$
 $$P=$$ 70%
 
 Hasil metriks presisi dari sistem rekomendasi yang dibuat sekitar 70%. Hal ini sudah cukup baik dalam merekomendasikan item yang sesuai dengan kebutuhan pengguna.
 
 
