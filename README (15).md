
# Laporan Proyek Machine Learning - Febrie Tsani Sovranita




## Project Overview

Membaca buku merupakan salah satu cara utama dalam memperluas pengetahuan dan wawasan seseorang. Namun, di tengah kemajuan teknologi informasi yang semakin pesat, budaya membaca di Indonesia masih tergolong rendah. Berdasarkan studi “Most Littered Nation In The World” yang  dilakukan  oleh  Central Connecticut State University pada maret 2016, Indonesia dinyatakan menduduki  peringkat  ke - 60  dari 61 Negara  soal  minat  membaca [1].Menurut UNESCO, hanya 0,001% masyarakat Indonesia yang memiliki kebiasaan membaca secara rutin [2]. Tantangan lain yang muncul adalah sulitnya menemukan buku yang sesuai dengan preferensi individu, terutama karena banyaknya pilihan yang tersedia dan kurangnya sistem pendukung yang dapat mengarahkan pembaca kepada bahan bacaan yang relevan. Oleh karena itu, sistem rekomendasi menjadi solusi penting untuk membantu pengguna dalam menemukan buku yang sesuai dengan minat dan kebutuhannya.

Penerapan sistem rekomendasi telah terbukti efektif dalam beberapa penelitian sebelumnya. Dalam penelitian yang dilakukan oleh [3],sistem rekomendasi berbasis content-based filtering diterapkan pada perpustakaan sekolah. Penelitian ini memanfaatkan algoritma TF-IDF dan cosine similarity untuk menghitung tingkat kemiripan antar buku, dan hasilnya menunjukkan bahwa sistem mampu memberikan rekomendasi yang relevan dengan nilai cosine similarity tertinggi mencapai 0,358. Penelitian lain oleh [4] mengembangkan sistem rekomendasi berbasis content-based filtering dengan pendekatan prototyping. Sistem ini menggunakan 25 sampel buku dari Penerbit Haru, dengan perhitungan TF-IDF dan cosine similarity terhadap delapan atribut seperti genre, sinopsis, dan penulis. Hasilnya menunjukkan akurasi similarity hingga 0,6 untuk rekomendasi yang paling relevan.

Berdasarkan studi-studi sebelumnya, pada penelitian ini diusulkan pendekatan dengan menggunakan collaborative filtering dan content-based filtering, untuk membandingkan efektivitas kedua pendekatan ini dalam memberikan rekomendasi buku. Pendekatan content-based filtering akan digunakan untuk memberikan rekomendasi berdasarkan kesamaan atribut buku seperti judul, penulis, dan genre. Sementara itu, pendekatan collaborative filtering akan dimanfaatkan untuk mengidentifikasi pola preferensi antar pengguna, sehingga sistem dapat merekomendasikan buku yang disukai oleh pengguna dengan profil serupa. Tujuan dari menggunakan kedua metode ini adalah untuk membandingkan seberapa efektif dan akurat masing-masing metode dalam memberikan rekomendasi buku, serta menemukan keuntungan dan kekurangan dari tiap metode. Penelitian ini diharapkan dapat memberikan kontribusi nyata dalam pengembangan sistem rekomendasi buku yang lebih personal, relevan, dan bermanfaat untuk meningkatkan minat baca di Indonesia dengan melakukan evaluasi terhadap kinerja algoritma dan hasil rekomendasi yang dihasilkan.


## Bussisnes Understanding

Bagian laporan ini mencakup:
### Problem Statements
Menjelaskan pernyataan masalah latar belakang:
- Bagaimana cara membantu pengguna menemukan buku yang sesuai dengan minat dan preferensi mereka di tengah banyaknya pilihan yang tersedia?
- Metode rekomendasi buku mana yang lebih efektif dan akurat dalam memberikan rekomendasi yang relevan: content-based filtering atau collaborative filtering?



### Goals

Menjelaskan tujuan dari pernyataan masalah:
- Mengembangkan sistem rekomendasi buku yang mampu memberikan rekomendasi yang relevan dan personal sesuai dengan preferensi pengguna.
- Membandingkan efektivitas dan akurasi antara metode content-based filtering dan collaborative filtering dalam konteks rekomendasi buku.
- Menemukan kelebihan dan kekurangan masing-masing metode untuk memberikan rekomendasi yang optimal.



### Solution Statement 
Untuk mencapai tujuan tersebut, penelitian ini mengajukan dua pendekatan solusi utama sebagai berikut:
- Content-Based Filtering
Pendekatan ini akan merekomendasikan buku berdasarkan kesamaan atribut buku yang telah disukai atau dibaca oleh pengguna sebelumnya. Atribut yang digunakan meliputi judul, penulis, genre, sinopsis, dan fitur lain yang relevan. Algoritma seperti TF-IDF dan cosine similarity akan digunakan untuk mengukur tingkat kemiripan antar buku sehingga sistem dapat menyarankan buku dengan karakteristik yang mirip dengan preferensi pengguna.
- Collaborative Filtering
Pendekatan ini akan memanfaatkan pola preferensi dan interaksi antar pengguna untuk memberikan rekomendasi. Sistem akan mengidentifikasi pengguna dengan profil atau perilaku membaca yang serupa, kemudian merekomendasikan buku yang disukai oleh pengguna lain dalam kelompok tersebut. Pendekatan ini memungkinkan sistem untuk memberikan rekomendasi yang bersifat lebih personal dan berdasarkan komunitas pengguna.




## Data Understanding

### Data Loading

Dataset yang digunakan terdiri dari tiga file utama: Books.csv, Ratings.csv, dan Users.csv. Dataset Books.csv berisi 271.360 data buku, mencakup informasi seperti ISBN, judul, penulis, tahun terbit, penerbit, dan URL gambar. Ratings.csv memuat 1.149.780 data penilaian buku oleh pengguna, dengan kolom User-ID, ISBN, dan Book-Rating (skala 0–10). Sementara itu, Users.csv mencakup 278.858 data profil pengguna yang terdiri dari User-ID, lokasi, dan usia. Ketiga dataset ini saling mendukung dan dapat digunakan untuk membangun sistem rekomendasi buku serta analisis perilaku pengguna. Adapun dataset yang didapat berasal dari datset publik yaitu Kaggle

Sumber data: https://www.kaggle.com/datasets/arashnic/book-recommendation-dataset/data?select=Users.csv


**Dataset Users**

| User-ID | Location                           | Age  |
|---------|------------------------------------|------|
| 1       | nyc, new york, usa                 | NaN  |
| 2       | stockton, california, usa          | 18.0 |
| 3       | moscow, yukon territory, russia    | NaN  |
| 4       | porto, v.n.gaia, portugal          | 17.0 |
| 5       | farnborough, hants, united kingdom | NaN  |
| ...     | ...                                | ...  |
| 278854  | portland, oregon, usa              | NaN  |
| 278855  | tacoma, washington, united kingdom | 50.0 |
| 278856  | brampton, ontario, canada          | NaN  |
| 278857  | knoxville, tennessee, usa          | NaN  |
| 278858  | dublin, n/a, ireland               | NaN  |

278858 rows × 3 columns

`Users.csv`: Mengandung data pengguna. Perhatikan bahwa ID pengguna (User-ID) telah dianonimkan dan dipetakan ke bilangan bulat. Data demografis (Location, Age) disediakan jika tersedia. Jika tidak, bidang-bidang ini berisi nilai NULL.

**Dataset Ratings**

| User-ID | ISBN         | Book-Rating |
|---------|--------------|-------------|
| 276725  | 034545104X   | 0           |
| 276726  | 0155061224   | 5           |
| 276727  | 0446520802   | 0           |
| 276729  | 052165615X   | 3           |
| 276729  | 0521795028   | 6           |
| ...     | ...          | ...         |
| 276704  | 1563526298   | 9           |
| 276706  | 0679447156   | 0           |
| 276709  | 0515107662   | 10          |
| 276721  | 0590442449   | 10          |
| 276723  | 05162443314  | 8           |

1149780 rows × 3 columns

`Ratings.csv`: Mengandung informasi peringkat buku. Peringkat (Book-Rating) dapat bersifat eksplisit, yang diekspresikan pada skala 1-10 (nilai yang lebih tinggi menunjukkan apresiasi yang lebih tinggi), atau implisit, yang diekspresikan dengan angka 0.

**Dataset Books**

| ISBN        | Book-Title                                      | Book-Author             | Year | Publisher                                | Image-URL-S                                      |
|-------------|--------------------------------------------------|--------------------------|------|-------------------------------------------|--------------------------------------------------|
| 0195153448  | Classical Mythology                              | Mark P. O. Morford       | 2002 | Oxford University Press                   | http://images.amazon.com/images/P/0195153448.0... |
| 0002005018  | Clara Callan                                     | Richard Bruce Wright     | 2001 | HarperFlamingo Canada                     | http://images.amazon.com/images/P/0002005018.0... |
| 0060973129  | Decision in Normandy                             | Carlo D'Este             | 1991 | HarperPerennial                           | http://images.amazon.com/images/P/0060973129.0... |
| 0374157065  | Flu: The Story of the Great Influenza Pandemic…  | Gina Bari Kolata         | 1999 | Farrar Straus Giroux                      | http://images.amazon.com/images/P/0374157065.0... |
| 0393045218  | The Mummies of Urumchi                           | E. J. W. Barber           | 1999 | W. W. Norton & Company                    | http://images.amazon.com/images/P/0393045218.0... |
| ...         | ...                                              | ...                      | ...  | ...                                       | ...                                              |
| 0440400988  | There's a Bat in Bunk Five                       | Paula Danziger            | 1988 | Random House Childrens Pub (Mm)          | http://images.amazon.com/images/P/0440400988.0... |
| 0525447644  | From One to One Hundred                          | Teri Sloat                | 1991 | Dutton Books                              | http://images.amazon.com/images/P/0525447644.0... |
| 006008667X  | Lily Dale: The True Story…                       | Christine Wicker          | 2004 | HarperSanFrancisco                        | http://images.amazon.com/images/P/006008667X.0... |
| 0192126040  | Republic (World's Classics)                      | Plato                     | 1996 | Oxford University Press                   | http://images.amazon.com/images/P/0192126040.0... |
| 0767409752  | A Guided Tour of Rene Descartes' Meditations…    | Christopher Biffle        | 2000 | McGraw-Hill Humanities/Social Sciences…  | http://images.amazon.com/images/P/0767409752.0... |

271360 rows × 8 columns

`Books.csv`: Buku diidentifikasi berdasarkan ISBN masing-masing. ISBN yang tidak valid telah dihapus dari dataset. Selain itu, beberapa informasi berbasis konten juga disediakan (Judul Buku, Penulis Buku, Tahun Terbit, Penerbit), yang diperoleh dari Amazon Web Services. Perlu dicatat bahwa jika ada beberapa penulis, hanya penulis pertama yang disediakan. URL yang mengarah ke gambar sampul juga disediakan, dalam tiga varian berbeda (URL Gambar-S, URL Gambar-M, URL Gambar-L), yaitu kecil, sedang, dan besar. URL-URL ini mengarah ke situs web Amazon.


### Exploratory Data Analysis (EDA)

#### Univariate Exploratory Data Analysis

Tahapan deskripsi variabel dimulai dengan mengidentifikasi variabel-variabel yang akan digunakan dalam penelitian atau analisis.

#### Deskripsi Variabel

**Dataset Users**

| #   | Column    | Non-Null Count | Dtype    |
|-----|-----------|----------------|----------|
| 0   | User-ID   | 278858         | int64    |
| 1   | Location  | 278858         | object   |
| 2   | Age       | 168096         | float64  |

Keterangan Dataset:

`User-ID`: ID unik untuk setiap pengguna. Digunakan untuk mengidentifikasi pengguna.

`Location`: Informasi lokasi pengguna dalam format "kota, provinsi, negara".

`Age`: Usia pengguna dalam satuan tahun.

**Distribusi Statistik Dataset Users**

| Statistic | User-ID       | Age         |
|-----------|---------------|-------------|
| count     | 278858.00000  | 168096.00000|
| mean      | 139429.50000  | 34.75143    |
| std       | 80499.51502   | 14.42810    |
| min       | 1.00000       | 0.00000     |
| 25%       | 69715.25000   | 24.00000    |
| 50%       | 139429.50000  | 32.00000    |
| 75%       | 209143.75000  | 44.00000    |
| max       | 278858.00000  | 244.00000   |

Berdasarkan statistik deskriptif kolom User-ID dan Age, terdapat beberapa insight penting terkait data pengguna. Rata-rata usia pengguna adalah sekitar 34,75 tahun dengan standar deviasi sebesar 14,43, yang menunjukkan variasi usia yang cukup lebar. Namun, terdapat nilai usia minimum sebesar 0 tahun dan maksimum mencapai 244 tahun, yang secara logika tidak valid dan menunjukkan adanya data outlier atau kesalahan input.

**Jumlah Baris dan Kolom Dataset Users**

![Image](https://github.com/user-attachments/assets/27206e35-e29e-4d18-8ecc-ca244a10f4af)


jumlah baris dan kolom pada Dataset Users terdiri dari 278858 baris dan 3 kolom

**Menampilkan nilai unik pada dataset users**

![Image](https://github.com/user-attachments/assets/97f1e689-12dd-4d09-9a3b-07294f21342b)

Berdasarkan hasil ouput diatas didapat bahwa setiap pengguna memiliki ID unik, dengan total 278.858 nilai berbeda pada kolom User-ID, menandakan tidak ada duplikasi data. Kolom Location memiliki 57.339 nilai unik yang sangat beragam, namun tidak konsisten, seperti adanya entri tidak lengkap atau format yang tidak baku.
kolom Age memiliki 166 nilai unik, termasuk nilai tidak valid dan banyak data kosong (NaN)

**Memeriksa nilai Null pada Dataset Users**

![Image](https://github.com/user-attachments/assets/83f093c9-58fa-46f8-a47b-49b1de886d27)

Dapat dilihat hasil output diatas menunjukkan bahwa pada dataset user memiliki nilai null pada kolom Age sebesar 110762

**Memeriksa nilai duplikat pada Dataset Users**

![Image](https://github.com/user-attachments/assets/95b94474-9f20-4931-b998-4e61711e9c8c)

Dapat dilihat hasil output diatas menunjukkan bahwa pada dataset user tidak memiliki nilai duplikat

**Memeriksa Outlier pada dataset Users**

![Image](https://github.com/user-attachments/assets/23fa8638-9eb4-4300-b693-1550ada99b7a)

Berdasarkan hasil visualisasi diatas menunjukkan bahwa Pada plot User-ID, distribusi terlihat merata tanpa outlier yang mencolok, mengindikasikan bahwa ID pengguna tersebar secara acak tanpa pola tertentu. Sementara itu, pada plot Age, terdapat banyak outlier terutama di atas usia 80 tahun, bahkan hingga lebih dari 200 tahun, yang kemungkinan merupakan data tidak valid atau kesalahan input. Mayoritas pengguna berada di rentang usia 20 hingga 50 tahun.



**Dataset Ratings**

| #   | Column      | Non-Null Count | Dtype  |
|-----|-------------|----------------|--------|
| 0   | User-ID     | 1,149,780      | int64  |
| 1   | ISBN        | 1,149,780      | object |
| 2   | Book-Rating | 1,149,780      | int64  |

Keterangan Dataset:

`User-ID`: Merupakan ID unik untuk setiap pengguna. Kolom ini menunjukkan siapa yang memberikan rating.

`ISBN`: Merupakan kode unik buku (International Standard Book Number) yang digunakan untuk mengidentifikasi setiap buku yang diberi rating.

`Book-Rating`: Berisi nilai rating yang diberikan pengguna terhadap suatu buku. Nilainya biasanya berada dalam rentang tertentu (misalnya 0–10)

**Distribusi Statistik Dataset Ratings**

| Statistic | User-ID       | Book-Rating     |
|-----------|---------------|-----------------|
| count     | 1.149780e+06  | 1.149780e+06    |
| mean      | 1.403864e+05  | 2.866950e+00    |
| std       | 8.056228e+04  | 3.854184e+00    |
| min       | 2.000000e+00  | 0.000000e+00    |
| 25%       | 7.034500e+04  | 0.000000e+00    |
| 50%       | 1.410100e+05  | 0.000000e+00    |
| 75%       | 2.110280e+05  | 7.000000e+00    |
| max       | 2.788540e+05  | 1.000000e+01    |

berdasarkan distribusi statistik ratings menunjukkan bahwa lebih dari 50% pengguna memberi nilai 0, dengan rata-rata rating hanya 2,87, menandakan banyak pengguna tidak memberikan penilaian eksplisit atau memberi nilai rendah. Rating berkisar antara 0–10, tetapi hanya sebagian kecil yang memberi nilai tinggi (di atas 7). 

**Jumlah Baris dan Kolom Dataset Ratings**

![Image](https://github.com/user-attachments/assets/0a4965e9-9220-47c1-9958-3dc7d7fe7575)


jumlah baris dan kolom pada Dataset Ratings terdiri dari 1149780 baris dan 3 kolom

**Menampilkan nilai unik pada dataset Ratings**

![Image](https://github.com/user-attachments/assets/6a15cd27-7c63-430d-9332-4a72a336318d)


Hasil output diatas menunjukkan bahwa Dataset df_ratings memiliki 105.283 pengguna unik (User-ID) dan 340.556 buku unik (ISBN), menunjukkan cakupan interaksi yang luas antara pengguna dan buku. Terdapat 11 nilai rating berbeda dari 0 hingga 10, yang mengindikasikan skala penilaian diskret. Banyaknya rating 0 memperkuat temuan sebelumnya bahwa sebagian besar pengguna mungkin tidak memberikan rating eksplisit.

**Memeriksa nilai Null pada Dataset Ratings**

![Image](https://github.com/user-attachments/assets/af81d2fc-9032-4255-a977-68fa41a56303)

Dapat dilihat hasil output diatas menunjukkan bahwa pada dataset ratings tidak memiliki nilai null

**Memeriksa nilai duplikat pada Dataset Ratings**

![Image](https://github.com/user-attachments/assets/7c1565b7-41ae-4efd-9e94-423605d2531a)

Dapat dilihat hasil output diatas menunjukkan bahwa pada dataset ratings tidak memiliki nilai duplikat


**Memeriksa Outlier pada dataset Ratings**

![Image](https://github.com/user-attachments/assets/391ef57a-162b-43fe-a92f-31bbee38b0d7)


Berdasarkan visualisasi diatas didapat bahwa User-ID menunjukkan distribusi yang merata tanpa outlier signifikan, menandakan bahwa pengguna tersebar cukup seimbang dalam dataset. Book-Rating didominasi oleh nilai 0, yang terlihat dari kotak boxplot yang sangat dekat dengan nilai 0 dan hampir tidak menunjukkan persebaran ke atas.

**Dataset Books**

| #   | Column               | Non-Null Count   | Dtype  |
|-----|----------------------|------------------|--------|
| 0   | ISBN                 | 271360 non-null  | object |
| 1   | Book-Title           | 271360 non-null  | object |
| 2   | Book-Author          | 271358 non-null  | object |
| 3   | Year-Of-Publication  | 271360 non-null  | object |
| 4   | Publisher            | 271358 non-null  | object |
| 5   | Image-URL-S          | 271360 non-null  | object |
| 6   | Image-URL-M          | 271360 non-null  | object |
| 7   | Image-URL-L          | 271357 non-null  | object |

Keterangan Dataset:

`ISBN`: Kode unik untuk setiap buku, digunakan sebagai pengenal utama.

`Book-Title`: Judul buku.

`Book-Author`: Nama penulis buku. Terdapat 2 data yang hilang (missing).

`Year-Of-Publication`: Tahun terbit buku. Bertipe object, kemungkinan mengandung data tidak konsisten atau tidak valid.

`Publisher`: Nama penerbit buku. Terdapat 2 data yang hilang.

`Image-URL-S/M/L`: Tautan ke gambar sampul buku dalam ukuran kecil (S), sedang (M), dan besar (L). Kolom Image-URL-L

**Distribusi Statistik Dataset Books**

|                        | ISBN     | Book-Title     | Book-Author     | Year-Of-Publication | Publisher  | Image-URL-S | Image-URL-M | Image-URL-L |
|------------------------|----------|----------------|------------------|----------------------|------------|-------------|-------------|-------------|
| **count**              | 271360   | 271360         | 271358           | 271360               | 271358     | 271360      | 271360      | 271357      |
| **unique**             | 271360   | 242135         | 102022           | 202                  | 16807      | 271044      | 271044      | 271041      |
| **top**                | 020130998X | Selected Poems | Agatha Christie | 2002                 | Harlequin  | http://images.amazon.com/images/P/042509474X.0... | http://images.amazon.com/images/P/042509474X.0... | http://images.amazon.com/images/P/006091985X.0... |
| **freq**               | 1        | 27             | 632              | 13903                | 7535       | 2           | 2           | 2           |


Dataset buku ini terdiri dari 271.360 entri unik berdasarkan ISBN, dengan 242.135 judul berbeda. Beberapa judul muncul lebih dari sekali, kemungkinan karena perbedaan edisi. Penulis paling produktif adalah Agatha Christie dengan 632 buku, sementara tahun terbit terbanyak adalah 2002 (13.903 buku). Penerbit paling sering muncul adalah Harlequin dengan 7.535 buku. 

**Jumlah Baris dan Kolom Dataset Books**

![Image](https://github.com/user-attachments/assets/65892d3a-d125-4e2f-a0d0-701e9e42cfc4)


jumlah baris dan kolom pada Dataset Books terdiri dari 271360 baris dan 8 kolom


**Menampilkan nilai unik pada dataset Books**

![Image](https://github.com/user-attachments/assets/bad536aa-71e5-4e42-96d0-3dfbbffc9767)

![Image](https://github.com/user-attachments/assets/4ad6e6e8-99c6-4ea7-b5a3-17269dc87a64)

![Image](https://github.com/user-attachments/assets/d59909b9-991a-4f91-8973-f53aa2fd65d5)


Berdasarkan hasil output diatas terdapat 271.360 ISBN unik yang menunjukkan setiap entri merupakan buku berbeda. Namun, hanya terdapat 242.135 judul unik, mengindikasikan adanya duplikasi judul karena edisi atau format berbeda. Penulis buku sangat beragam, dengan lebih dari 102.000 penulis unik, menandakan variasi konten yang luas. Tahun terbit mencakup 202 nilai unik, didominasi oleh tahun 2000-an. Publisher pun sangat beragam (16.808 penerbit), tetapi beberapa penerbit besar sering muncul.

**Memeriksa nilai Null pada Dataset Books**

![Image](https://github.com/user-attachments/assets/3b97d4f0-b861-4e3a-9e60-3761ccc9fa54)


Berdasarkan hasil output diatas menunjukkan bahwa dataset book memiliki nilai null pada kolom Book-Author terdiri dari 2, Publisher terdiri dari 2 nilai null, Image-URL-L terdiri dari 3 nilai null

**Memeriksa nilai duplikat pada Dataset Books**

![Image](https://github.com/user-attachments/assets/63d77bb1-023e-465f-8dae-bcf3b8c77367)

Dapat dilihat hasil output diatas menunjukkan bahwa pada dataset book tidak memiliki nilai duplikat


#### Distribusi Rating Buku

![Image](https://github.com/user-attachments/assets/5efaf862-070b-4089-8796-3edb84462fe4)

Insight:

mayoritas pengguna memberikan rating 0, yang jumlahnya sangat dominan dibanding rating lain. Hal ini menunjukkan bahwa sebagian besar entri dalam data merupakan ulasan kosong atau belum memberikan rating sebenarnya. Di luar itu, rating paling umum berada pada rentang tinggi, terutama rating 8, 10, dan 7, yang mengindikasikan bahwa pengguna cenderung memberikan penilaian positif terhadap buku yang mereka baca. Rating rendah seperti 1–4 sangat jarang diberikan, menandakan bias positif atau kecenderungan hanya memberi rating jika menyukai buku tersebut


#### Top 10 Publisher berdasarkan jumlah buku terbit

![Image](https://github.com/user-attachments/assets/70ecc5e0-1c0a-4758-a022-ff5d4dddcc3b)


Insight:

Berdasarkan grafik di atas, dapat disimpulkan bahwa Harlequin merupakan penerbit dengan jumlah buku terbanyak, dengan mengungguli penerbit lainnya di daftar 10 besar. Silhouette dan Pocket menempati posisi kedua dan ketiga, namun selisih jumlah buku yang diterbitkan dengan Harlequin cukup signifikan. Secara umum, dominasi Harlequin menunjukkan konsistensi dan kapasitas produksi yang sangat tinggi dibandingkan kompetitornya


#### Top 10 Penulis berdasarkan ratings

![Image](https://github.com/user-attachments/assets/d5c310cf-7a83-45bb-b1a3-01a64db923e0)

Insight:

Berdasarkan grafik "Top 10 Penulis Berdasarkan Total Rating", Stephen King menempati posisi teratas dengan total rating yang jauh lebih tinggi dibandingkan penulis lain, menunjukkan popularitas dan pengaruhnya yang sangat besar di antara pembaca.


#### Distribusi Umur Pengguna

![Image](https://github.com/user-attachments/assets/0f48ffb6-5f87-4cff-9bff-5079e51d4131)

Insight:

Berdasarkan visualisasi diatas menunjukkan bahwa mayoritas pengguna berada pada rentang usia 20 hingga 35 tahun, dengan puncak jumlah pengguna sekitar usia 25 tahun. Setelah usia 35, jumlah pengguna menurun secara bertahap, dan sangat sedikit pengguna yang berusia di atas 60 tahun.

#### Jumlah Rating per User

![Image](https://github.com/user-attachments/assets/a32e04e0-d82c-415f-9e43-9472db1f652a)

Insight:

Jumlah rating per pengguna menunjukkan pola distribusi yang sangat tidak merata, di mana sebagian besar pengguna hanya memberikan satu rating. Semakin sedikit pengguna yang memberikan rating dalam jumlah lebih banyak, dan hanya segelintir pengguna yang sangat aktif memberikan puluhan hingga ratusan rating.


















## Data Preparation

Pada titik ini, berbagai metode persiapan data digunakan secara berurutan untuk menjamin kualitas data yang bersih dan kesiapan data untuk proses pemodelan sistem rekomendasi. Langkah – langkah tahapan data preparation sebagai berikut:

### Menghapus Kolom Umur dari Dataset df_users

```bash
df_users = df_users.drop(columns=['Age'], errors='ignore')

```
proses penghapusan kolom age ini mengunakan teknik Feature Dropping. Kolom Age dihapus karena pada analisis ini informasi umur tidak digunakan atau mungkin tidak konsisten. Alasannya Menghilangkan atribut yang tidak relevan dapat meningkatkan efisiensi proses analisis dan mencegah gangguan pada model akibat data yang tidak dibutuhkan.

### Menggabungkan Dataset Buku dan Rating

```bash
books_data = df_book.merge(df_ratings, on="ISBN")

```
Dataset df_book dan df_ratings digabung berdasarkan kolom ISBN sebagai identifier dengan menggunakan teknik data merging/join. Alasan, Penggabungan ini penting untuk menggabungkan informasi metadata buku dengan data rating pengguna agar bisa dianalisis bersama.


### Menyalin Data dan Menghapus Nilai Kosong (NaN)

```bash
df = books_data.copy()
df.dropna(inplace=True)
df.reset_index(drop=True, inplace=True)
```

Data hasil merge disalin agar data mentah tetap utuh. Kemudian, baris yang mengandung nilai kosong dihapus. Adapun Alasan menghapus baris dengan nilai kosong yaitu untuk mencegah error atau bias pada proses pemodelan, terutama jika missing value tidak dapat diimputasi secara bermakna. teknik yang digunakan yaitu Missing Value Handling

### Menghapus Kolom Tidak Relevan

```bash
df.drop(columns=["ISBN", "Year-Of-Publication", "Image-URL-S", "Image-URL-M","Image-URL-L"], inplace=True)
```

Kolom-kolom yang tidak diperlukan seperti gambar dan tahun publikasi dihapus dari dataset (Feature Elimination). karena alasanya Kolom tersebut tidak berkontribusi terhadap prediksi atau analisis dalam studi ini, sehingga penghapusannya dapat menyederhanakan data. 


### Menyaring Data Berdasarkan Nilai Rating

```bash
df = df[df["Book-Rating"] != 0]
```

Rating dengan nilai 0 disaring karena dianggap tidak merepresentasikan evaluasi nyata dari pengguna. Adapun alasannya yaitu Rating nol biasanya digunakan sebagai placeholder atau default, bukan penilaian yang sah. Penghapusannya meningkatkan kualitas data. Teknik yang digunakan yaitu Data Filtering

### Normalisasi Teks pada Judul Buku

```bash
df["Book-Title"] = df["Book-Title"].apply(lambda x: re.sub(r"[^\w\s]", " ", x).strip())
```

Karakter non-alfanumerik dihapus dari judul buku untuk menyederhanakan teks. Adapun Alasannya yaitu Normalisasi ini berguna dalam analisis berbasis teks seperti content-based filtering, agar teks lebih seragam dan mudah diproses. 

### Membagi Dataset Menjadi Data Latih dan Uji

```bash
train_df, test_df = train_test_split(df, test_size=0.2, random_state=42)
```

Dataset dibagi menjadi 80% data latih dan 20% data uji untuk keperluan validasi model.

### Hasil output setelah proses Data Preparation

![Image](https://github.com/user-attachments/assets/1f88daec-2a3a-4fdb-8d21-5c8b2f8aa342)


Hasil output diatas merupakan isi dataset df setelah dilakukan proses data preparation, terdapat kolom Book-Title, Book-Author, Publisher, User-ID, Book-Rating








## Modeling

Sistem rekomendasi digunakan untuk membantu pengguna menemukan item yang relevan secara efisien. Dalam konteks ini, sistem dikembangkan untuk memberikan rekomendasi buku secara personal kepada pengguna berdasarkan riwayat interaksi dan/atau kemiripan konten buku.

### Collaborative Filtering (CF) 
```bash
# Membuat pivot matrix dan menghitung similarity antar pengguna
users_pivot = new_train_df.pivot_table(index='User-ID', columns='Book-Title', values='Book-Rating').fillna(0)
similarity = cosine_similarity(users_pivot)

# Fungsi untuk menemukan pengguna mirip
def user_based(data, user_id):
    index = np.where(users_pivot.index == user_id)[0][0]
    similar_users = list(enumerate(similarity[index]))
    similar_users = sorted(similar_users, key=lambda x: x[1], reverse=True)[1:6]
    return [users_pivot.index[i[0]] for i in similar_users]
```

Collaborative Filtering memanfaatkan data rating dari pengguna untuk merekomendasikan item berdasarkan kesamaan perilaku pengguna. Pada pendekatan ini digunakan pendekatan user-based CF dengan cosine similarity.

Adapun cara kerja dari penerapan CF kedalam sistem rekomendasi buku sebagai berikut:
- Filter pengguna yang memiliki jumlah interaksi cukup (lebih dari 200 buku).
- Bangun matriks pivot (user vs buku).
- Hitung kemiripan antar pengguna dengan cosine similarity.
- Ambil buku dari pengguna yang paling mirip, yang belum dibaca oleh pengguna target.
- Tampilkan Top-N rekomendasi.

#### Hasil Top-N Rekomendasi Collaborative Filtering (CF)

![Image](https://github.com/user-attachments/assets/5b2d45a2-205b-4a17-a683-89c387230be2)

Berdasarkan buku-buku favorit user ID 107784, terlihat bahwa user ID 107784 menyukai bacaan dengan muatan edukatif, isu sosial-lingkungan, dan narasi personal yang kuat. user ID 107784 tertarik pada kisah nyata, reflektif, dan penuh makna seperti The Price of Loyalty dan Silent Spring, serta menghargai pengetahuan umum seperti dalam The Handy Geography Answer Book. Rekomendasi yang diberikan sangat relevan, seperti NEEDLES dan Endless Steppe yang merupakan memoar perjuangan hidup, serta Small Sacrifices yang mengangkat kisah nyata penuh konflik moral. Ini menunjukkan bahwa user ID 107784 cenderung memilih buku yang menyentuh sisi emosional, memberi wawasan mendalam, dan memicu empati serta pemikiran kritis.



### Content-Based Filtering (CBF)
```bash
vectorizer = TfidfVectorizer(stop_words='english')
tfidf_matrix = vectorizer.fit_transform(unique_books["combined_features"])
cosine_sim = cosine_similarity(tfidf_matrix[idx], tfidf_matrix).flatten()
similar_indices = cosine_sim.argsort()[::-1][1:top_n + 1]
```
Pendekatan ini merekomendasikan buku berdasarkan kemiripan konten seperti judul, penulis, dan penerbit, menggunakan teknik TF-IDF vectorization dan cosine similarity.

Adapun cara kerja dari penerapan CBF kedalam sistem rekomendasi buku sebagai berikut:
- Gabungkan fitur konten menjadi satu string.
- Terapkan TF-IDF untuk representasi vektor fitur konten.
- Hitung cosine similarity antar buku.
- Tampilkan Top-N buku dengan kemiripan tertinggi terhadap buku input.

#### Hasil Top-N Rekomendasi Content-Based Filtering (CBF)

![Image](https://github.com/user-attachments/assets/34f5a11b-d588-4e68-a863-ca8cd5964b9f)

Dari hasil Top-N recommendation berbasis content-based filtering (CBF) untuk buku The Street Lawyer, dapat diperoleh beberapa insight penting. Semua buku yang direkomendasikan merupakan karya John Grisham, menunjukkan bahwa sistem merekomendasikan buku dengan atribut penulis yang sama, yang konsisten dengan prinsip content-based filtering yang mengandalkan kemiripan fitur konten. Skor kemiripan tertinggi (0.82) dimiliki oleh Street Lawyer itu sendiri, diikuti oleh judul-judul lain yang relevan seperti The Testament, A Time to Kill, The Client, dan The Partner, yang juga bergenre legal thriller dan memiliki tema hukum serupa. Rating bintang yang relatif tinggi (antara 7.0 hingga 8.03) pada buku-buku ini mengindikasikan bahwa rekomendasi tidak hanya didasarkan pada kemiripan konten, tetapi juga pada kualitas buku yang cukup baik. Hal ini menggarisbawahi keunggulan content-based filtering dalam memberikan rekomendasi yang personal dan relevan berdasarkan karakteristik buku yang sudah disukai pengguna, khususnya dalam konteks genre dan penulis yang sama.


### Kelebihan dan Kekurangan dari Setiap pendekatan


| Pendekatan              | Kelebihan                                                                 | Kekurangan                                                                  |
|-------------------------|---------------------------------------------------------------------------|-----------------------------------------------------------------------------|
| **Collaborative Filtering** |  Personalisasi tinggi karena berbasis interaksi nyata.                 |  Tidak bisa bekerja untuk pengguna/item baru (*cold-start*).              |
|                         |  Menemukan preferensi laten pengguna.                                   |  Butuh data interaksi besar.                                              |
| **Content-Based Filtering** |  Bisa merekomendasikan item baru (selama ada kontennya).               |  Rekomendasi bisa monoton (hanya mirip konten).                           |
|                         |  Tidak tergantung pada pengguna lain.                                   |  Tidak belajar dari perilaku pengguna (kurang adaptif terhadap selera).   |






## Evaluation

### Collaborative Filtering (CF)

**Mean Squared Error (MSE)**
Mean Squared Error (MSE) adalah metrik evaluasi yang umum digunakan dalam statistik dan machine
learning untuk mengukur seberapa akurat sebuah model regresi dalam memprediksi nilai numerik. MSE
menghitung selisih antara nilai prediksi model dan nilai sebenarnya dari data, kemudian mengkuadratkan selisih tersebut agar tidak ada selisih yang bernilai negatif. Kemudian, selisih kuadrat dijumlahkan dan diambil rata-rata dari semua sampel data. Persamaan Mean Squared Error adalah sebagai berikut:

![Image](https://github.com/user-attachments/assets/dacafdd2-a1cc-4e18-bd43-759ef53d618c)

di mana N adalah jumlah sampel data, 𝑦𝑛 adalah nilai sebenarnya dari data ke-n, dan ŷ𝑛 adalah nilai prediksi dari model untuk data ke-n.


**Root Mean Squared Error (RMSE)**
Root Mean Squared Error (MSE) juga disebut Root Mean Squared Deviation (RMSD). RMSE dibangun di atas MSE, Root Mean Squared Error (RMSE) adalah cara standar untuk mengukur kesalahan suatu model dalam memprediksi data kuantitatif. RMSE adalah akar kuadrat dari Mean Squared Error (MSE) dan mengukur besarnya kesalahan dalam satuan yang sama dengan variabel keluaran.

Mengambil akar kuadrat membantu memecahkan banyak kelemahan yang dihadapi dengan MSE: 
- Metrik berada dalam unit yang sama dengan variabel dependen.
- Kesalahan besar diberi penalti besar.
- Hukuman atas kesalahan kecil diberikan pada tingkat yang lebih rendah.
- Kurang rentan terhadap outlier.

Rumus RMSE dihitung sebagai akar kuadrat dari rata-rata selisih kuadrat antara nilai prediksi dan nilai aktual menggunakan rumus berikut:

![Image](https://github.com/user-attachments/assets/2e6d7ed7-a632-4341-9262-7d4fe6e06f81)

Seperti MSE, RMSE selalu non-negatif, dan RMSE yang lebih rendah lebih baik.
RMSE dinyatakan dalam satuan yang sama dengan variabel target, membuatnya lebih mudah ditafsirkan daripada MSE.
Ini menghukum kesalahan yang lebih besar, yang dapat berguna saat kesalahan signifikan tidak diinginkan.

### Content-Based Filtering (CBF)

**Precision@N**
untuk Content-Based Filtering menggunakan matriks evaluasi Precision@N. Precision mengukur proporsi item yang direkomendasikan yang benar-benar relevan bagi pengguna. Dalam konteks sistem rekomendasi, precision@N didefinisikan sebagai:


![Image](https://github.com/user-attachments/assets/15687c83-5fbe-4c49-8c41-5592445bb97b)

Dalam implementasi CBF ini, sistem menghitung kesamaan konten antar buku berdasarkan fitur gabungan (seperti judul, penulis, dan penerbit) menggunakan TF-IDF dan cosine similarity. Untuk setiap judul input, sistem menghasilkan N rekomendasi teratas.

### Hasil evaluasi model

1. Collaborative Filtering (CF)

![Image](https://github.com/user-attachments/assets/7063de37-7877-49dc-bfa3-814c27e13dcc)


Berdasarkan hasil evaluasi model Collaborative Filtering dengan pendekatan user-based yang efisien (menggunakan precomputed similarity matrix), diperoleh nilai Mean Squared Error (MSE) sebesar 5.5969 dan Root Mean Squared Error (RMSE) sebesar 2.3658. Nilai RMSE ini menunjukkan bahwa rata-rata kesalahan prediksi rating buku terhadap nilai aktual berada dalam rentang ±2.37 skala rating.



2. Content-Based Filtering (CBF)

![Image](https://github.com/user-attachments/assets/428ee5d2-c658-42a0-93df-f7f6abb0ee62)

Berdasarkan hasil evaluasi model Content-Based Filtering dengan metrik Precision@5, diperoleh nilai sebesar 0.0667 atau sekitar 6,67%. Artinya, dari setiap 5 rekomendasi buku yang diberikan oleh sistem, rata-rata hanya 1 dari 15 yang benar-benar relevan berdasarkan preferensi pengguna yang menyukai buku serupa. Nilai precision yang rendah ini menunjukkan bahwa model belum mampu secara efektif mengidentifikasi item serupa yang relevan bagi pengguna. Perbaikan bisa dilakukan dengan menambahkan fitur konten yang lebih kaya, seperti sinopsis atau ulasan, atau menggabungkan pendekatan hybrid untuk meningkatkan akurasi rekomendasi.




**Kesimpulan**

Sistem rekomendasi menjadi solusi penting untuk masalah eksplorasi rekomendasi buku karena membantu pengguna menemukan buku yang sesuai dengan preferensi pribadi mereka di antara banyak pilihan. Content-Based Filtering (CBF) dan Collaborative Filtering (CF) adalah dua metode utama yang digunakan untuk mencapai tujuan busisness understanding.

Hasil evaluasi menunjukkan bahwa Collaborative Filtering memiliki performa yang lebih baik dengan nilai RMSE sebesar 2.3658, menandakan kemampuan prediksi yang lebih akurat terhadap rating pengguna. Sebaliknya, Content-Based Filtering menunjukkan precision@5 yang rendah (0.0667), yang mengindikasikan bahwa rekomendasi yang diberikan kurang relevan terhadap preferensi aktual pengguna. Hal ini menggarisbawahi keterbatasan CBF dalam memahami konteks preferensi pengguna secara komprehensif, terutama saat informasi konten buku terbatas atau mirip secara tekstual namun tidak relevan secara pengalaman pembaca.

Maka, Collaborative Filtering lebih efektif untuk personalisasi rekomendasi karena memanfaatkan pola perilaku pengguna lain yang serupa, memungkinkan sistem memberikan rekomendasi berdasarkan kolektivitas pengalaman. Namun demikian, CBF tetap memiliki keunggulan dalam mengatasi cold-start problem untuk buku baru.




## Referensi


[1]	U. Jamaludin, R. A. Pribadi, and Y. M. Rahmah, “OPTIMALISASI GERAKA LITERASI SEKOLAH DENGAN POJOK BACA TERHADAP MINAT BACA PESERTA DIDIK KELAS VA SD NEGERI RAWU,” Didaktik : Jurnal Ilmiah PGSD FKIP Universitas Mandiri, 2023, Accessed: Jun. 05, 2025. [Online]. Available: https://journal.stkipsubang.ac.id/index.php/didaktik/article/view/1097/1053

[2]	H. Yuliansyah, “OPTIMALISASI PEMANFAATAN PERPUSTAKAAN SEKOLAH SEBAGAI  UPAYA MENINGKATKAN LITERASI BAHASA  DI SDN NGAGLIK 04 KOTA BATU,” Jurnal Pendidikan Taman Widya Humaniora (JPTWH), May 2023, Accessed: Jun. 05, 2025. [Online]. Available: https://jurnal.widyahumaniora.org/index.php/jptwh/article/view/183

[3]	R. Ardiansyah, M. Ari Bianto, and B. D. Saputra, “Sistem Rekomendasi Buku Perpustakaan Sekolah menggunakan Metode Content-Based Filtering,” Jurnal CoSciTech (Computer Science and Information Technology), vol. 4, no. 2, pp. 510–518, Oct. 2023, doi: 10.37859/coscitech.v4i2.5131.

[4]	Asa Dilla Safitri, Vihi Atina, and Anisatul Farida, “Sistem rekomendasi buku menggunakan metode content-based filtering,” INFOTECH : Jurnal Informatika & Teknologi, vol. 5, no. 2, pp. 218–227, Dec. 2024, doi: 10.37373/infotech.v5i2.1302.



**---Ini adalah bagian akhir laporan---**