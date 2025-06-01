
# Laporan Proyek Machine Learning - Febrie Tsani Sovranita




## Project Overview

Steam merupakan salah satu platform distribusi game digital terbesar di dunia, pada tahun 2020 steam menyumbang 21% dari pendapatan pasar game global, mencapai US$33,9 miliar, dengan peningkatan tahunan 6,7% dibandingkan tahun sebelumnya. Dari tahun 2016 hingga 2018, tingkat pertumbuhan tahunan komposit rata-rata pengguna terdaftar global Steam mencapai 54% [1]. Dengan banyaknya pilihan game, pengguna sering mengalami kesulitan menemukan game yang sesuai dengan minat dan preferensi mereka [2]. Sehingga sistem rekomendasi menjadi sangat penting untuk membantu proses penemuan game yang relevan dan sesuai dengan minat pengguna. Tanpa bantuan sistem rekomendasi yang andal, pengguna cenderung mengalami decision fatigue (kelelahan dalam pengambilan Keputusan) yang pada gilirannya mengurangi minat mereka dalam bermain game. Hal ini tidak hanya berdampak pada pengalaman pengguna, tetapi juga pada potensi pendapatan pengembang game.

Studi sebelumnya telah mengusulkan berbagai sistem rekomendasi untuk mengatasi masalah tersebut. Seperti penelitian [3] mengubah data perilaku implisit, seperti durasi bermain, menjadi preferensi eksplisit dengan menggunakan metode collaborative filtering. Kemudian mereka menguji beberapa algoritma, termasuk SVD++, SlopeOne, dan KNN, dan menemukan hasil yang cukup baik. Sementara itu, penelitian [2] mengembangkan sistem rekomendasi berbasis content-based filtering dengan menggunakan Cosine Similarity, yang ditanamkan dalam aplikasi Flutter. Hasil penelitian mereka menunjukkan tingkat akurasi yang tinggi dan tingkat penerimaan pengguna yang tinggi berdasarkan Model Penerimaan Teknologi (TAM).

Berdasarkan penelitian sebelumnya, pada penelitian ini diusulkan pendekatan dengan menggunakan collaborative filtering dan content-based filtering, untuk membandingkan efektivitas kedua pendekatan ini dalam memberikan rekomendasi game pada platform Steam. Tujuan dari penggunaan kedua pendekatan ini adalah untuk mengevaluasi secara objektif keunggulan dan keterbatasan masing-masing pendekatan dalam hal data pengguna dan metadata game yang tersedia. Collaborative filtering digunakan untuk merekomendasikan game berdasarkan kesamaan preferensi antar pengguna, sedangkan content-based filtering memanfaatkan fitur-fitur atau tag game yang mirip dengan game yang telah dimainkan pengguna. Dengan menganalisis performa dari masing-masing metode, penelitian ini bertujuan untuk memberikan wawasan yang lebih dalam mengenai metode rekomendasi yang paling sesuai untuk diterapkan di platform dengan karakteristik seperti Steam

## Bussisnes Understanding

Bagian laporan ini mencakup:
### Problem Statements
Menjelaskan pernyataan masalah latar belakang:
- Bagaimana cara menggunakan algoritma Collaborative Filtering dan Content-Based Filtering untuk membuat sistem rekomendasi game yang efektif??
- Algoritma mana yang lebih baik untuk memberikan rekomendasi yang tepat dan membantu pengguna memilih game yang tepat serta mengurangi kebingungan pengguna?
Alzheimer?

### Goals

Menjelaskan tujuan dari pernyataan masalah:
- Membangun sistem rekomendasi game dengan menggunakan dua algoritma, yaitu Collaborative Filtering dan Content-Based Filtering.
- Membandingkan performa kedua algoritma dalam memberikan rekomendasi yang sesuai dengan preferensi pengguna.
- Menentukan Menentukan metode rekomendasi terbaik untuk meningkatkan kepuasan pengguna dan potensi pendapatan pengembang game di Steam


### Solution Statement 
Untuk mengatasi masalah tersebut, proyek ini menggunakan pendekatan berikut:
- Melakukan pengolahan data interaksi pengguna dan metadata game secara efisien untuk membangun model rekomendasi.
- Mengimplementasikan algoritma Collaborative Filtering untuk merekomendasikan game berdasarkan pola preferensi pengguna lain yang serupa.
- Menggunakan algoritma Content-Based Filtering untuk merekomendasikan game yang memiliki kemiripan fitur dengan game yang sudah dimainkan pengguna.
- Melakukan evaluasi dan perbandingan performa kedua algoritma menggunakan metrik akurasi dan relevansi rekomendasi.




## Data Understanding

### Data Loading
Pada tahap ini dilakukan proses mengambil dan memuat data mentah ke lingkungan pemrosesan agar siap untuk dieksplorasi, dibersihkan, dan diolah lebih lanjut dalam tahapan Machine Learning.

![Image](https://github.com/user-attachments/assets/cf8d1d81-226b-4aa9-8df4-dc4b9373eefc)

| user_id  | products | reviews |
|----------|----------|---------|
| 7360263  | 359      | 0       |
| 14020781 | 156      | 1       |
| 8762579  | 329      | 4       |
| 4820647  | 176      | 4       |
| 5167327  | 98       | 2       |
| ...      | ...      | ...     |
| 5047430  | 6        | 0       |
| 5048153  | 0        | 0       |
| 5059205  | 31       | 0       |
| 5074363  | 0        | 0       |
| 5081164  | 0        | 0       |

14306064 rows × 3 columns

`users.csv`: tabel informasi publik profil pengguna: jumlah produk yang dibeli dan ulasan yang diterbitkan.

![Image](https://github.com/user-attachments/assets/b15ac14d-4406-4029-ba57-fec3d2e5dfbc)

| app_id   | title                                    | date_release | win   | mac   | linux | rating         | positive_ratio | user_reviews | price_final | price_original | discount | steam_deck |
|----------|------------------------------------------|--------------|-------|-------|--------|----------------|----------------|---------------|--------------|----------------|----------|-------------|
| 13500    | Prince of Persia: Warrior Within™        | 2008-11-21   | True  | False | False  | Very Positive  | 84             | 2199          | 9.99         | 9.99           | 0.0      | True        |
| 22364    | BRINK: Agents of Change                  | 2011-08-03   | True  | False | False  | Positive       | 85             | 21            | 2.99         | 2.99           | 0.0      | True        |
| 113020   | Monaco: What's Yours Is Mine             | 2013-04-24   | True  | True  | True   | Very Positive  | 92             | 3722          | 14.99        | 14.99          | 0.0      | True        |
| 226560   | Escape Dead Island                       | 2014-11-18   | True  | False | False  | Mixed          | 61             | 873           | 14.99        | 14.99          | 0.0      | True        |
| 249050   | Dungeon of the ENDLESS™                  | 2014-10-27   | True  | True  | False  | Very Positive  | 88             | 8784          | 11.99        | 11.99          | 0.0      | True        |
| ...      | ...                                      | ...          | ...   | ...   | ...    | ...            | ...            | ...           | ...          | ...            | ...      | ...         |
| 2296380  | I Expect You To Die 3: Cog in the Machine| 2023-09-28   | True  | False | False  | Very Positive  | 96             | 101           | 22.00        | 0.00           | 0.0      | True        |
| 1272080  | PAYDAY 3                                 | 2023-09-21   | True  | False | False  | Mostly Negative| 38             | 29458         | 40.00        | 0.00           | 0.0      | True        |
| 1402110  | Eternights                                | 2023-09-11   | True  | False | False  | Very Positive  | 89             | 1128          | 30.00        | 0.00           | 0.0      | True        |
| 2272250  | Forgive Me Father 2                      | 2023-10-19   | True  | False | False  | Very Positive  | 95             | 82            | 17.00        | 0.00           | 0.0      | True        |
| 2488510  | FatalZone                                | 2023-10-23   | True  | False | False  | Very Positive  | 88             | 144           | 4.00         | 0.00           | 0.0      | True        |


50872 rows × 13 columns

`games.csv`: tabel informasi tentang permainan (atau add-on) yang mencakup peringkat, harga dalam dolar AS ($), tanggal rilis, dan sebagainya. Informasi tambahan non-tabel tentang permainan, seperti deskripsi dan tag, terdapat dalam berkas metadata.

![Image](https://github.com/user-attachments/assets/b7e05989-6b43-4048-9749-62ee182d3690)

| app_id  | helpful | funny | date       | is_recommended | hours | user_id  | review_id  |
|---------|---------|-------|------------|----------------|-------|----------|------------|
| 975370  | 0       | 0     | 2022-12-12 | True           | 36.3  | 51580    | 0          |
| 304390  | 4       | 0     | 2017-02-17 | False          | 11.5  | 2586     | 1          |
| 1085660 | 2       | 0     | 2019-11-17 | True           | 336.5 | 253880   | 2          |
| 703080  | 0       | 0     | 2022-09-23 | True           | 27.4  | 259432   | 3          |
| 526870  | 0       | 0     | 2021-01-10 | True           | 7.9   | 23869    | 4          |
| ...     | ...     | ...   | ...        | ...            | ...   | ...      | ...        |
| 633230  | 0       | 0     | 2021-02-15 | True           | 41.0  | 1606890  | 41154789   |
| 758870  | 8       | 0     | 2019-07-18 | False          | 8.0   | 1786254  | 41154790   |
| 696170  | 3       | 10    | 2018-03-26 | False          | 2.0   | 6370324  | 41154791   |
| 696170  | 0       | 0     | 2018-06-11 | True           | 4.0   | 1044289  | 41154792   |
| 1089980 | 2       | 0     | 2020-09-16 | True           | 14.0  | 13971935 | 41154793   |

41154794 rows × 8 columns

`recommendations.csv`: tabel ulasan pengguna: apakah pengguna merekomendasikan suatu produk. Tabel ini mewakili hubungan banyak-ke-banyak antara entitas game dan entitas pengguna.

![Image](https://github.com/user-attachments/assets/8fba467b-50ef-491a-be17-3de7f731ebf9)

| app_id  | description                                                                                              | tags                                                    |
|---------|----------------------------------------------------------------------------------------------------------|---------------------------------------------------------|
| 13500   | Enter the dark underworld of Prince of Persia ...                                                        | [Action, Adventure, Parkour, Third Person, Gre...       |
| 22364   |                                                                                                          | [Action]                                                |
| 113020  | Monaco: What's Yours Is Mine is a single player ...                                                     | [Co-op, Stealth, Indie, Heist, Local Co-Op, St...      |
| 226560  | Escape Dead Island is a Survival-Mystery adventure ...                                                  | [Zombies, Adventure, Survival, Action, Third P...      |
| 249050  | Dungeon of the Endless is a Rogue-Like Dungeon ...                                                     | [Roguelike, Strategy, Tower Defense, Pixel Gra...      |


50872 rows x 3 columns

`games_metadata.json`: File ini merupakan kumpulan metadata game di platform Steam yang dapat digunakan untuk berbagai keperluan analisis


### Exploratory Data Analysis (EDA)

#### Univariate Exploratory Data Analysis
Univariate Exploratory Data Analysis (EDA) fokus untuk menganalisis satu variabel saja secara mendalam, baik itu numerik maupun kategorikal.

#### Deskripsi variabel

karena dataset terlalu banyak maka kita lakukan pengurangan data terlebih dahulu agar tidak crash saat pengurangan dataset

Source code dibawah ini merupakan perwakilan yang merepresentasikan baris kode untuk pengurangan data
```bash
# ========== Parámeters ==========
SAMPLE_FRAC   = 0.03      # 3%
RANDOM_STATE  = 42        # untuk reproducibility

# ========== 1. Sampling pada users ==========
sample_users = (
    df_users['user_id']
    .drop_duplicates()
    .sample(frac=SAMPLE_FRAC, random_state=RANDOM_STATE)
)
df_users = df_users[df_users['user_id'].isin(sample_users)]

# ========== 2. Sampling pada games ==========
sample_games = (
    df_game['app_id']
    .drop_duplicates()
    .sample(frac=SAMPLE_FRAC, random_state=RANDOM_STATE)
)
df_game = df_game[df_game['app_id'].isin(sample_games)]

# ========== 3. Sampling pada recommendations ==========
# (metode per-user agar semua interaksi user terpilih tetap utuh)
df_recomend = df_recomend[df_recomend['user_id'].isin(sample_users)]

# ========== 4. Sampling pada metadata ==========
df_metadata = df_metadata[df_metadata['app_id'].isin(df_game['app_id'])]

```
Source code diatas melakukan pengambilan sampel (sampling) 3% data dari dataset besar agar tidak terjadi crash saat pemrosesan. Sampling dilakukan pada data users dan games secara acak dengan random_state agar hasilnya konsisten. Selanjutnya, data recommendations disaring supaya hanya berisi interaksi dari user yang terpilih, dan metadata disesuaikan dengan games yang tersisa. Hasilnya, ukuran dataset berkurang drastis dari jutaan baris menjadi ratusan ribu atau ribuan, sehingga lebih mudah dan cepat diolah tanpa kehilangan keterkaitan antar data.

```bash
# ───── Hitung Selisih Rows & Persentase Removal ─────
datasets = [
    ("users",       orig_users_shape[0],    df_users.shape[0]),
    ("games",       orig_games_shape[0],    df_game.shape[0]),
    ("recomend",    orig_recomend_shape[0], df_recomend.shape[0]),
    ("metadata",    orig_metadata_shape[0], df_metadata.shape[0]),
]

print(f"{'Dataset':<12}{'Orig Rows':>10}{'Sampl Rows':>12}{'Removed':>10}{'Removed %':>12}")
for name, orig, samp in datasets:
    removed = orig - samp
    pct     = removed / orig * 100
    print(f"{name:<12}{orig:>10,}{samp:>12,}{removed:>10,}{pct:>11.2f}%")
```
Fungsi source code diatas adalah untuk menghitung dan menampilkan perbedaan jumlah baris (rows) antara dataset sebelum dan sesudah proses sampling, serta menghitung persentase data yang dihapus dari masing-masing tabel (users, games, recomend, dan metadata).


**Tabel users**
| No | Column   | Non-Null Count | Dtype |
|----|----------|----------------|-------|
| 0  | user_id  | 429,182        | int64 |
| 1  | products | 429,182        | int64 |
| 2  | reviews  | 429,182        | int64 |

Keterangan dataset:

`user_id`: 	ID unik yang merepresentasikan masing-masing pengguna Steam.

`products`: ID game (product ID), biasanya sesuai dengan app_id dari games_metadata.json. Ini menunjukkan game apa yang dimainkan atau dimiliki oleh pengguna.

`reviews`: Nilai ulasan atau bentuk implicit feedback.

**Distribusi Statistik tabel user**
| Statistik | user_id       | products     | reviews      |
|-----------|---------------|--------------|--------------|
| count     | 429,182       | 429,182.000  | 429,182.000  |
| mean      | 7,151,162.000 | 116.307      | 2.894        |
| std       | 4,130,738.000 | 243.396      | 7.798        |
| min       | 9.000         | 0.000        | 0.000        |
| 25%       | 3,571,235.000 | 23.000       | 1.000        |
| 50%       | 7,152,088.000 | 56.000       | 1.000        |
| 75%       | 10,727,780.000| 127.000      | 3.000        |
| max       | 14,306,030.000| 19,641.000   | 1,347.000    |

user_id tersebar luas dari 9 hingga sekitar 14 juta, yang kemungkinan hanya sebagai ID unik. Rata-rata user memiliki 116 produk dengan variasi tinggi (std 243), kebanyakan antara 23-56 produk, namun ada outlier dengan hampir 20 ribu produk. Untuk review, rata-rata sekitar 2.9 dengan median 1, menunjukkan mayoritas user memberi sedikit review, tapi ada juga outlier dengan hingga 1347 review.


![Image](https://github.com/user-attachments/assets/cdab7ba6-a5d6-4cec-b1d5-1f7828bc47c9)

gambar diatas merupakan Jumlah baris dan kolom pada dataset user setelah dilakukan proses pengurangan data menjadi 429182 baris dan 3 kolom.

**Menampilkan nilai unik pada tabel user**
![Image](https://github.com/user-attachments/assets/3de458b4-a65a-485f-973b-d6a46841da0d)

berdasatkan hasil output diatas, didapat bahwa terdapat 429.182 user unik, menandakan bahwa data ini mencakup populasi pengguna yang cukup besar. Kolom products memiliki 2.564 nilai unik, menunjukkan variasi yang luas dalam jumlah game yang dimiliki oleh pengguna, dari hanya beberapa hingga ribuan. Sementara itu, kolom reviews menunjukkan 225 nilai unik, yang mencerminkan tingkat aktivitas yang sangat beragam dalam memberikan ulasan


**Memeriksa outlier pada tabel user**
![Image](https://github.com/user-attachments/assets/f4e71c7f-1624-48f5-bde5-3e489bec66ee)

berdasarkan visualisasi diatas didapat bahwa distribusi data untuk variabel products dan reviews sangat terdistribusi ke kanan (right-skewed), dengan banyak outlier bernilai tinggi. Mayoritas user hanya memiliki sedikit produk dan ulasan, sementara sebagian kecil user memiliki jumlah yang sangat tinggi, yang kemungkinan merupakan power users atau akun bisnis. Sebaliknya, variabel user_id terdistribusi lebih merata tanpa outlier, hanya menunjukkan rentang identifikasi pengguna.

**Memeriksa nilai null pada tabel user**
![Image](https://github.com/user-attachments/assets/f7e02b2d-00d9-4532-8b57-5621f0c8a364)

Dapat dilihat hasil output diatas menunjukkan bahwa pada tabel user tidak memiliki nilai null

**Memeriksa nilai duplikat pada tabel user**
![Image](https://github.com/user-attachments/assets/a0448153-478a-49f4-b8b1-d157bd39d070)

Dapat dilihat hasil output diatas menunjukkan bahwa pada tabel user tidak memiliki nilai yang duplikat


**Tabel games**

| Column          | Non-Null Count | Dtype    |
|-----------------|----------------|----------|
| app_id          | 1526 non-null  | int64    |
| title           | 1526 non-null  | object   |
| date_release    | 1526 non-null  | object   |
| win             | 1526 non-null  | bool     |
| mac             | 1526 non-null  | bool     |
| linux           | 1526 non-null  | bool     |
| rating          | 1526 non-null  | object   |
| positive_ratio  | 1526 non-null  | int64    |
| user_reviews    | 1526 non-null  | int64    |
| price_final     | 1526 non-null  | float64  |
| price_original  | 1526 non-null  | float64  |
| discount        | 1526 non-null  | float64  |
| steam_deck      | 1526 non-null  | bool     |

Keterangan dataset:

- `app_id`: Merupakan ID unik yang digunakan untuk mengidentifikasi masing-masing aplikasi atau game di platform Steam. ID ini berfungsi sebagai identifikasi utama dalam dataset.

- `title`: Menunjukkan judul atau nama dari game atau aplikasi yang terdapat di Steam. Kolom ini merepresentasikan identitas produk secara eksplisit.

- `date_release`: Berisi informasi tanggal rilis resmi dari game. Tanggal ini masih dalam format string dan disarankan untuk dikonversi ke format datetime agar memudahkan analisis berdasarkan waktu.

- `win`: Menyatakan apakah game tersebut tersedia untuk pengguna sistem operasi Windows. Nilai True menunjukkan ketersediaan, sedangkan False menunjukkan ketidaksediaan.

- `mac`: Menyatakan apakah game tersedia untuk sistem operasi macOS. Kolom ini penting untuk mengetahui dukungan lintas platform bagi pengguna Apple.

- `linux`: Menyatakan apakah game tersedia untuk sistem operasi Linux. Hal ini berguna dalam menganalisis kompatibilitas game dengan sistem operasi open-source.

- `rating`: Berisi kategori penilaian dari pengguna, seperti “Very Positive”, “Mixed”, dan sebagainya. Informasi ini menggambarkan persepsi umum pengguna terhadap game.

- `positive_ratio`: Menunjukkan persentase ulasan positif dari total ulasan pengguna. Nilainya dinyatakan dalam bentuk bilangan bulat antara 0 hingga 100, yang merefleksikan tingkat kepuasan pengguna.

- `user_reviews`: Menyajikan jumlah total ulasan yang diberikan oleh pengguna untuk masing-masing game. Nilai ini dapat digunakan untuk mengukur popularitas atau tingkat engagement.

- `price_final`: Merupakan harga akhir game setelah diberlakukan diskon. Nilai ini mencerminkan harga aktual yang harus dibayar oleh konsumen pada saat itu.

- `price_original`: Menunjukkan harga asli game sebelum adanya potongan harga. Informasi ini dapat digunakan untuk menghitung nilai diskon dan strategi harga.

- `discount`: Menunjukkan besar persentase potongan harga yang diterapkan terhadap harga asli game. Nilai disajikan dalam bentuk desimal, misalnya 0.3 berarti diskon 30%.

- `steam_deck`: Menyatakan apakah game tersebut kompatibel dengan perangkat Steam Deck.


**Distribusi Statistik tabel games**
| Statistik | app_id     | positive_ratio | user_reviews | price_final | price_original | discount |
|-----------|------------|----------------|---------------|--------------|----------------|----------|
| count     | 1526       | 1526.000000    | 1526.000000   | 1526.000000  | 1526.000000    | 1526.000000 |
| mean      | 1035186.0  | 76.470511      | 1373.802752   | 8.282294     | 8.452156       | 5.209043 |
| std       | 613898.1   | 18.386206      | 11682.819764  | 11.310108    | 11.477209      | 18.186688 |
| min       | 20         | 9.0            | 10.0          | 0.000000     | 0.000000       | 0.000000 |
| 25%       | 520932.5   | 66.0           | 19.0          | 0.990000     | 0.990000       | 0.000000 |
| 50%       | 926495.0   | 80.5           | 49.0          | 4.990000     | 4.990000       | 0.000000 |
| 75%       | 1508320.0  | 90.0           | 199.25        | 9.990000     | 10.740000      | 0.000000 |
| max       | 2576800.0  | 100.0          | 335623.0      | 199.990000   | 199.990000     | 90.000000 |


berdasarkan hasil output diatas didapat bahwa mayoritas game memiliki rasio ulasan positif yang tinggi, dengan nilai rata-rata 76,47 dan median 80,5, menunjukkan bahwa sebagian besar game diterima dengan baik oleh pengguna. Namun, distribusi jumlah ulasan pengguna sangat tidak merata, dengan rata-rata 1.373 ulasan namun nilai maksimum mencapai 335.623, menandakan adanya outlier atau game sangat populer. Harga akhir dan harga asli game secara umum cukup rendah (median keduanya sekitar $4,99), tetapi terdapat game premium dengan harga hingga $199,99.


![Image](https://github.com/user-attachments/assets/04c97e81-5b73-4303-b499-c9387cb91000)

jumlah baris dan kolom pada tabel users terdiri dari 11526 baris dan 13 kolom

**Menampilkan nilai unik pada tabel games**
```bash
# Menampilkan nilai unik pada tabel game
for column in df_game.columns:
    unique_vals = df_game[column].unique()
    print(f"Kolom: '{column}'")
    print(f"Jumlah nilai unik: {len(unique_vals)}")
    print(f"Nilai unik (maksimal 15 ditampilkan): {unique_vals[:15]}")
    print('-' * 50)

```

![Image](https://github.com/user-attachments/assets/b0c233e0-325d-47f4-8744-abbb068a843f)

Berdasarkan visualisasi diatas didapat bahwa terdapat 1.526 game yang masing-masing memiliki ID (app_id) dan judul (title) yang unik. Game-gamenya dirilis pada 1.132 tanggal berbeda, menunjukkan variasi waktu rilis yang cukup besar. Mayoritas game mendukung platform Windows, sementara dukungan untuk macOS dan Linux lebih terbatas. Kategori rating pengguna terdiri dari 9 jenis, didominasi oleh ulasan positif seperti "Very Positive" dan "Mostly Positive". Rasio ulasan positif memiliki 88 variasi, menunjukkan beragam persepsi pengguna terhadap game. Jumlah ulasan pengguna sangat bervariasi, mulai dari 10 hingga ratusan ribu, dengan 506 nilai unik. Harga akhir (price_final) dan harga asli (price_original) juga beragam, mencerminkan banyaknya model harga dan diskon yang tersedia. Diskon memiliki 29 nilai unik, dengan beberapa game bahkan mendapatkan potongan hingga 90%. Terakhir, sekitar setengah dari game terdata kompatibel dengan Steam Deck.


**Memeriksa Outlier pada Tabel games**

![Image](https://github.com/user-attachments/assets/4b6c4768-e47c-4aa5-a1b8-e09dff2f933e)

Berdasarkan visualisasi diatas didapat bahwa sebagian besar fitur numerik dalam dataset memiliki outlier. Pada user_reviews, price_final, price_original, dan discount, terlihat banyak nilai ekstrem di atas batas atas (upper whisker), mengindikasikan distribusi yang sangat miring ke kanan (right-skewed). Sebaliknya, positive_ratio relatif simetris dengan sebaran utama antara 60–95. Variabel app_id hanya digunakan sebagai identifikasi sehingga distribusinya tidak memberikan insight analitis.


**Memeriksa nilai null pada tabel games**
![Image](https://github.com/user-attachments/assets/21e0de46-f2b6-414d-b5e5-c09745343909)

Dapat dilihat hasil output diatas menunjukkan bahwa pada tabel games tidak memiliki nilai null

**Memeriksa nilai duplikat pada tabel games**
![Image](https://github.com/user-attachments/assets/34159229-2efa-448c-9ccc-ce800af279d9)

Dapat dilihat hasil output diatas menunjukkan bahwa pada tabel games tidak memiliki nilai yang duplikat

**Tabel recommendations**

| No | Kolom           | Non-Null Count   | Tipe Data  |
|----|------------------|------------------|------------|
| 0  | app_id           | 1,242,152         | int64      |
| 1  | helpful          | 1,242,152         | int64      |
| 2  | funny            | 1,242,152         | int64      |
| 3  | date             | 1,242,152         | object     |
| 4  | is_recommended   | 1,242,152         | bool       |
| 5  | hours            | 1,242,152         | float64    |
| 6  | user_id          | 1,242,152         | int64      |
| 7  | review_id        | 1,242,152         | int64      |

Keterangan dataset:

- `app_id`: ID unik dari game yang diulas oleh pengguna. Kolom ini berfungsi sebagai penghubung antara review dan data game terkait.

- `helpful`: Menunjukkan jumlah pengguna lain yang menandai ulasan tersebut sebagai "membantu". Nilai ini memberikan indikasi seberapa berguna ulasan tersebut bagi komunitas.

- `funny` : Menggambarkan jumlah pengguna yang menganggap ulasan tersebut lucu. Kolom ini mencerminkan elemen hiburan dalam ulasan.

- `date`: Berisi tanggal kapan ulasan dibuat atau dipublikasikan. Informasi ini berguna untuk analisis waktu dan tren ulasan.

- `is_recommended`: Nilai boolean (True atau False) yang menunjukkan apakah pengguna merekomendasikan game tersebut atau tidak. Ini merupakan sinyal utama dari kepuasan pengguna terhadap game.

- `hours`: Total jam yang telah dihabiskan oleh pengguna untuk bermain game sebelum memberikan ulasan. Kolom ini dapat digunakan untuk melihat korelasi antara waktu bermain dan kepuasan.

- `user_id`: ID unik dari pengguna yang memberikan ulasan. Kolom ini digunakan untuk mengidentifikasi perilaku atau preferensi pengguna tertentu.

- `review_id`: ID unik untuk setiap ulasan. Kolom ini berfungsi sebagai identifier utama untuk setiap entri review agar tidak terjadi duplikasi atau kebingungan saat pengolahan data.


**Distribusi Statistik tabel recommendations**
| Kolom       | Count        | Mean        | Std Dev     | Min        | 25%        | 50%        | 75%        | Max        |
|-------------|--------------|-------------|-------------|------------|------------|------------|------------|------------|
| app_id      | 1,242,152    | 602,243.01  | 471,462.42  | 10         | 254,700    | 435,150    | 926,990    | 2,245,890  |
| helpful     | 1,242,152    | 3.20        | 41.88       | 0          | 0          | 0          | 0          | 14,636     |
| funny       | 1,242,152    | 1.08        | 28.64       | 0          | 0          | 0          | 0          | 13,991     |
| hours       | 1,242,152    | 100.35      | 175.83      | 0.00       | 7.80       | 27.20      | 99.00      | 999.90     |
| user_id     | 1,242,152    | 7,450,054.45| 4,019,415.41| 9          | 4,288,410  | 7,551,240  | 10,980,260 | 14,306,020 |
| review_id   | 1,242,152    | 20,608,210.76| 11,862,279.66| 19        | 10,342,140 | 20,649,100 | 30,891,570 | 41,154,720 |

Berdasarkan hasil output diatas didapat bahwa sebagian besar pengguna hanya memberikan sedikit jam bermain dan interaksi terhadap ulasan. Median jam bermain (hours) hanya sekitar 27.2 jam, dengan mayoritas ulasan tidak mendapatkan tanda “helpful” atau “funny” (nilai 0 pada kuartil 25%, 50%, dan 75%). Namun, terdapat beberapa outlier ekstrem, seperti ulasan dengan lebih dari 14.000 tanda “helpful” atau jam bermain hingga 999 jam. Ini menunjukkan distribusi yang sangat tidak merata, di mana hanya sedikit pengguna atau ulasan yang sangat aktif atau populer

![Image](https://github.com/user-attachments/assets/ba4846ac-9d01-4315-8a3c-a5b87e9a05ef)

jumlah baris dan kolom pada tabel recommendatios terdiri dari 1242152 baris dan 8 kolom

**Menampilkan nilai unik pada tabel recommendations**
![Image](https://github.com/user-attachments/assets/5cb963e4-3d70-42ae-a9f7-a7b3e425f9a6)

Berdasarkan hasil output diatas didapat bahwa dataset ini memiliki 23.748 game unik (app_id) dan lebih dari 1,2 juta ulasan berbeda (review_id). Sebagian besar ulasan memiliki interaksi yang rendah dari pengguna lain, terlihat dari nilai helpful dan funny yang sebagian besar mendekati nol, meskipun terdapat beberapa nilai ekstrem (misalnya 246 dan 329). Terdapat 4.400 tanggal berbeda yang menunjukkan ulasan berasal dari periode waktu yang panjang, serta hanya dua kategori pada kolom is_recommended, yaitu True dan False. Waktu bermain (hours) sangat bervariasi hingga 10.000 nilai unik, mencerminkan perilaku pengguna yang sangat beragam.


**Pengurangan baris data pada tabel recommendations untuk proses EDA**

Untuk mengecek outlier pada dataset tabel recommendatios, kita harus mengambil beberapa sampel yang representatif dikarenakan dataset recommendations memiliki data yang sangat begitu banyak, sehingga akan memakan waktu komputasi yang lama dan berpontensi untuk crash

```bash
df_sample_recomend = pd.read_csv("/content/Submisiion 2/recommendations.csv", skiprows=lambda i: i > 0 and random.random() > 0.01)
```

Kode tersebut digunakan untuk membaca file CSV bernama recommendations.csv dengan memuat hanya sebagian kecil data secara acak, yaitu sekitar 1% dari keseluruhan baris, agar proses pembacaan data tidak membebani memori komputer.

![Image](https://github.com/user-attachments/assets/acd9258b-4161-4f80-a611-573177e02086)

jumlah baris dan kolom pada dataset df_sample_recomend terdiri dari 410308 baris dan 8 kolom

**Memeriksa outlier pada tabel recommendations**
![Image](https://github.com/user-attachments/assets/3d21d24f-da21-4000-b4cd-2ef8643232b0)

Berdasarkan visualisasi diatas didapat bahwa kolom app_id, user_id, dan review_id memiliki sebaran yang cukup merata tanpa banyak outlier signifikan. Sebaliknya, kolom helpful, funny, dan terutama hours menunjukkan distribusi yang sangat skewed ke kanan, dengan banyak outlier ekstrem—menandakan bahwa hanya sebagian kecil pengguna yang memberikan review sangat membantu, lucu, atau memainkan game dalam durasi yang sangat lama.

**Memeriksa nilai null pada tabel recommendations**
![Image](https://github.com/user-attachments/assets/193c5711-253e-4aa4-8d54-6225ed85a7ad)

Dapat dilihat hasil output diatas menunjukkan bahwa pada tabel recommendations tidak memiliki nilai null

**Memeriksa nilai duplikat pada tabel recommendations**
![Image](https://github.com/user-attachments/assets/8baaf70d-15d5-47a8-9d6f-c3b6fdf9e28a)

Dapat dilihat hasil output diatas menunjukkan bahwa pada tabel recommendations tidak memiliki nilai duplikat


**Tabel games_metadata.json**
| No. | Kolom       | Non-Null Count | Tipe Data |
|-----|-------------|----------------|-----------|
| 1   | app_id      | 1526 non-null  | int64     |
| 2   | description | 1526 non-null  | object    |
| 3   | tags        | 1526 non-null  | object    |

Keterangan dataset:
- `app_id`: ID unik untuk setiap game.
- `description`: Deskripsi teks dari game, biasanya menjelaskan fitur, gameplay, dan latar belakangnya.
- `tags`: Kumpulan tag atau label yang menggambarkan genre, tema, atau fitur spesifik dari game (misalnya "Multiplayer", "Action", "Indie").

**Memeriksa nilai null pada tabel games_metadata**

![Image](https://github.com/user-attachments/assets/69cfbf95-7e74-4835-8792-19702dcf5022)


Dapat dilihat hasil output diatas menunjukkan bahwa pada tabel games_metadata tidak memiliki nilai null

**Memeriksa nilai duplikat pada tabel games_metadata**

![Image](https://github.com/user-attachments/assets/3cc40e02-8731-4400-82ba-b89c061f4ff4)

Dapat dilihat hasil output diatas menunjukkan bahwa pada tabel games_metadata tidak memiliki nilai duplikat


**Distribusi Jam Bermain (Normal dan Log Scale)**

![Image](https://github.com/user-attachments/assets/4a6200ff-8648-4249-a9d1-1a62f2d90398)

Insight:

Visualisasi di atas menunjukkan distribusi jam bermain game oleh pengguna dalam dua skala: normal dan logaritmik. Pada skala normal (kiri), distribusi sangat miring ke kanan (right-skewed), dengan sebagian besar pengguna bermain dalam waktu singkat, sementara sebagian kecil memiliki jam bermain yang sangat tinggi. Skala logaritmik (kanan) mengungkapkan bahwa distribusi lebih menyerupai bentuk log-normal, di mana mayoritas pengguna bermain antara 1 hingga 100 jam.


**Trend Jumlah Review per tahun**
![Image](https://github.com/user-attachments/assets/b9c25388-f7e1-4ee5-bc70-330147dd0412)

Insight:

Berdasarkan hasil visualisasi diatas didapat bahwa tren jumlah review game per tahun dari 2010 hingga 2022. Terlihat adanya peningkatan signifikan sejak 2014, dengan lonjakan tajam mulai tahun 2019 hingga mencapai puncaknya pada 2022. Hal ini mengindikasikan pertumbuhan pengguna dan aktivitas komunitas yang semakin besar

**10 game terpopuler berdasarkan jumlah user review**
![Image](https://github.com/user-attachments/assets/79562f38-c199-42b7-804d-162cae071bf2)

Insight:

Berdasarkan hasil visualisasi diatas menunjukkan 10 game terpopuler berdasarkan jumlah review. Game Brawlhalla menempati posisi teratas dengan jumlah review tertinggi, disusul oleh Z1 Battle Royale dan theHunter: Call of the Wild™. Hal ini menunjukkan bahwa game dengan elemen multiplayer kompetitif atau open-world memiliki tingkat interaksi pengguna yang tinggi.

**Aktivitas user (jumlah review per user)**
![Image](https://github.com/user-attachments/assets/4c8ae560-7b81-468c-8e4e-e0a37d2a5870)

Insight:

Berdasarkan hasil visualisasi diatas menunjukkan distribusi jumlah review yang ditulis per pengguna dalam skala logaritmik. Mayoritas besar pengguna hanya menulis satu review, ditunjukkan oleh lonjakan tajam di angka 1. Jumlah pengguna menurun drastis seiring bertambahnya jumlah review yang ditulis, yang berarti hanya sebagian kecil pengguna yang aktif memberikan banyak ulasan.

**Distribusi Jumlah Game yang Dimiliki**
![Image](https://github.com/user-attachments/assets/9930d3a3-b720-46d8-b7c7-961e9326c234)

Insight:

Berdasarkan hasil visualisasi diatas menunjukkan sebagian besar pengguna hanya memberikan review untuk sedikit game, dengan jumlah pengguna menurun drastis seiring bertambahnya jumlah game yang mereka review. Ini mengindikasikan bahwa interaksi pengguna terhadap game bersifat terbatas, di mana hanya segelintir pengguna yang mengeksplorasi atau mereview banyak game.


**Distribusi harga game**
![Image](https://github.com/user-attachments/assets/e9bb1d33-baee-468c-93f7-1a5bc849c940)

Insight:

Berdasarkan hasil visualisasi diatas menunjukkan sebagian besar game memiliki harga yang sangat rendah, bahkan mendekati nol, menunjukkan dominasi game gratis atau murah di platform. Semakin tinggi harga, jumlah game yang tersedia semakin sedikit, dengan sangat sedikit game yang dibanderol di atas $50.

**Tahun Rilis**
![Image](https://github.com/user-attachments/assets/19d424c9-59e6-43b4-b21b-57f64ed1c8dc)

Insight:

Berdasarkan hasil visualisasi diatas menunjukkan tren jumlah game yang dirilis per tahun. Terlihat peningkatan signifikan sejak tahun 2014, dengan puncak rilis terjadi pada tahun 2021 dan 2022, masing-masing mendekati 200 judul game. Setelah itu, terjadi penurunan pada tahun 2023. 


**Distribusi platform game**

![Image](https://github.com/user-attachments/assets/cd36d5ea-ada1-4a05-b2fa-e58e6a502eab)

Insight:

Berdasarkan hasil visualisasi diatas menunjukkan jumlah game yang mendukung platform Windows jauh lebih banyak dibandingkan dengan Mac dan Linux. 


**Analisis Kesamaan variabel isi kolom dari setiap dataset**

Berdasarkan hasil Exploratory Data Analysis dari keempat dataset didapat bahwa dataset `users`, `games`, `recommendations`, dan `games_metadata.json`. Keempatnya saling terhubung melalui kolom kunci seperti `user_id` dan `app_id`, yang memungkinkan penggabungan data untuk membangun model rekomendasi yang efektif.

Kolom `user_id` menghubungkan data pengguna dengan aktivitas review, sementara `app_id` mengaitkan setiap review dengan informasi game, termasuk judul, tanggal rilis, sistem operasi, rating, serta deskripsi dan tag. Kolom hours mencerminkan waktu bermain sebagai indikator minat, dan `is_recommended` berfungsi sebagai label eksplisit untuk evaluasi.







## Data Preparation

Pada titik ini, berbagai metode persiapan data digunakan secara berurutan untuk menjamin kualitas data yang tinggi dan kesiapan data untuk proses pemodelan sistem rekomendasi. Langkah – langkah tahapan data preparation sebagai berikut:

### Format dan Ekstraksi Tanggal Rilis Game
```bash
df_game['date_release'] = pd.to_datetime(df_game['date_release'], errors='coerce')
df_game['release_year'] = df_game['date_release'].dt.year.fillna(0).astype(int)
```
Kolom date_release pada dataset df_game dikonversi menjadi tipe data datetime menggunakan pd.to_datetime. Selanjutnya, diambil tahun rilis dari tanggal tersebut dan disimpan di kolom baru release_year.
Alasannya yaitu supaya memudahkan analisis dan pemrosesan berdasarkan tahun rilis serta menangani data tanggal yang tidak valid (errors='coerce' akan mengubah nilai tidak valid menjadi NaT).

### Validasi dan Normalisasi Format Tags
```bash
df_metadata['tags'] = df_metadata['tags'].apply(lambda x: x if isinstance(x, list) else [])
```

Pada dataset metadata (df_metadata), kolom tags dipastikan berisi list agar konsisten. Jika ada nilai yang bukan list, diubah menjadi list kosong.
Alasannya yaitu supaya memudahkan proses manipulasi dan ekstraksi fitur tags yang berbentuk list.

### Filtering Game Berdasarkan Metadata
```bash
valid_game_ids = set(df_metadata['app_id'])
df_game = df_game[df_game['app_id'].isin(valid_game_ids)].reset_index(drop=True)
```

Dataset game difilter hanya untuk menyertakan game yang memiliki metadata terkait, berdasarkan kecocokan app_id.
Alasannya yaitu supaya hanya data yang lengkap dan valid yang digunakan untuk analisis dan pemodelan, menghindari missing value dan inkonsistensi.

### Pembuatan Fitur untuk Collaborative Filtering (CF)
```bash
df_cf = df_recomend[['user_id', 'app_id', 'is_recommended', 'hours']].copy()
df_cf['adjusted_hours'] = df_cf.apply(
    lambda row: row['hours'] * 1.25 if row['is_recommended'] else row['hours'] * 0.75,
    axis=1
)
```

Subset kolom penting (user_id, app_id, is_recommended, dan hours) disalin dari dataset interaksi pengguna (df_recomend). Kemudian dibuat kolom baru adjusted_hours yang mengubah durasi bermain sesuai dengan rekomendasi (dikalikan 1.25 jika direkomendasikan, dan 0.75 jika tidak).
Alasannya yaitu mengutamakan jam bermain untuk game yang direkomendasikan memungkinkan model CF untuk lebih peka terhadap preferensi pengguna.

### Encoding User dan Game ID
```bash
user_id_map = {id_: idx for idx, id_ in enumerate(df_cf['user_id'].unique())}
app_id_map = {id_: idx for idx, id_ in enumerate(df_cf['app_id'].unique())}

encoded_data = pd.DataFrame({
    'user_encoded': df_cf['user_id'].map(user_id_map),
    'app_encoded': df_cf['app_id'].map(app_id_map),
    'hours': df_cf['hours'],
    'adjusted_hours': df_cf['adjusted_hours'],
    'is_recommended': df_cf['is_recommended']
})
```

User dan game (app_id) yang berbentuk ID asli diubah menjadi indeks numerik menggunakan mapping dictionary. Alasan yaitu format numerik diperlukan untuk input model machine learning agar efisien dan kompatibel.


### Normalisasi Fitur Jam Bermain
```bash
scaler_hours = MinMaxScaler()
scaler_adjusted = MinMaxScaler()
encoded_data['hours_scaled'] = scaler_hours.fit_transform(encoded_data[['hours']])
encoded_data['adjusted_hours_scaled'] = scaler_adjusted.fit_transform(encoded_data[['adjusted_hours']])
```

Kolom hours dan adjusted_hours dinormalisasi ke rentang 0-1 menggunakan MinMaxScaler. Alasan yaitu skala fitur yang seragam penting untuk kestabilan dan performa model, menghindari dominasi fitur dengan skala besar.

### Train-Test Split untuk Collaborative Filtering
```bash
X = encoded_data[['user_encoded', 'app_encoded']].values
y = encoded_data['adjusted_hours_scaled'].values
train_X, test_X, train_y, test_y = train_test_split(X, y, test_size=0.2, random_state=42)
```

Data dibagi menjadi data latih dan data uji dengan proporsi 80:20 menggunakan train_test_split untuk evaluasi model. Alasannya yaitu memastikan model dapat diuji performanya pada data yang belum pernah dilihat.

### Penggabungan Dataset Game dan Metadata untuk Content-Based Filtering (CBF)
```bash
df_cbf = pd.merge(df_game, df_metadata[['app_id', 'description', 'tags']], on='app_id', how='left')
```
Dataset game (df_game) digabung dengan metadata (df_metadata) berdasarkan app_id untuk mendapatkan informasi lengkap berupa deskripsi dan tags. Alasan yaitu Menggabungkan informasi konten agar fitur konten bisa diekstrak dan digunakan untuk rekomendasi berbasis konten.

### Pembersihan dan Normalisasi Tags
```bash
df_cbf['tags'] = df_cbf['tags'].apply(lambda x: [tag.strip().replace(' ', '_') for tag in x])
df_cbf['tags_str'] = df_cbf['tags'].apply(lambda x: ' '.join(x) if x else 'no_tags')
```
Tags dibersihkan dengan menghilangkan spasi dan menggabungkannya menjadi string tunggal (tags_str).
Alasan yaitu supaya memudahkan proses vektorisasi teks dan representasi fitur tags secara konsisten.

### Penggabungan Konten Teks
```bash
df_cbf['content_text'] = df_cbf['tags_str'] + ' ' + df_cbf['description'].fillna('') + ' ' + df_cbf['title'].fillna('')
```

Semua konten teks dari tags, deskripsi, dan judul digabung menjadi satu kolom content_text untuk proses ekstraksi fitur teks. Alasannya yaitu menyediakan sumber data teks komprehensif untuk ekstraksi fitur yang kaya pada CBF.

### Pemetaan Rating ke Skor Numerik
```bash
rating_map = {
    'Overwhelmingly Positive': 5, 'Very Positive': 4, 'Positive': 3, 'Mildly Positive': 2,
    'Mixed': 1, 'Mildly Negative': -1, 'Negative': -2, 'Very Negative': -3, 'Overwhelmingly Negative': -4
}
df_cbf['rating'] = df_cbf['rating'].map(rating_map).fillna(0)
```

Rating game yang berbentuk teks diubah menjadi skor numerik menggunakan mapping yang sudah ditentukan. Alasannya yaitu Fitur numerik lebih mudah diolah dalam proses pembelajaran mesin.

### Ekstraksi Fitur TF-IDF untuk Deskripsi dan Tags
```bash
tfidf_desc = TfidfVectorizer(stop_words='english', max_df=1.0, max_features=100, min_df=5, ngram_range=(1, 2))
description_tfidf = tfidf_desc.fit_transform(df_cbf['description'].fillna(''))

tfidf_tags = TfidfVectorizer()
tags_tfidf = tfidf_tags.fit_transform(df_cbf['tags_str'])
```

Menggunakan TfidfVectorizer untuk mengubah kolom deskripsi dan tags menjadi representasi matriks TF-IDF. Alasannya yaitu mengubah teks menjadi fitur numerik yang merepresentasikan pentingnya kata dalam dokumen untuk pembelajaran.


### Normalisasi Fitur Numerik Lainnya
```bash
num_cols = ['rating', 'positive_ratio', 'user_reviews', 'price_final']
df_cbf[num_cols] = df_cbf[num_cols].fillna(0)
num_scaled = MinMaxScaler().fit_transform(df_cbf[num_cols])
sparse_num = csr_matrix(num_scaled)
```

Fitur numerik tambahan seperti rating, positive_ratio, user_reviews, dan price_final dinormalisasi menggunakan MinMaxScaler dan diubah menjadi sparse matrix. Alasannya yaitu menyamakan skala fitur numerik agar tidak mendominasi fitur lain saat penggabungan.



### Penggabungan Semua Fitur untuk CBF
```bash
combined_feature = hstack([description_tfidf, tags_tfidf, sparse_num])
```

Fitur teks (deskripsi dan tags) dan fitur numerik digabungkan menjadi satu matriks fitur gabungan menggunakan fungsi hstack. Alasannya yaitu untuk mengkombinasikan berbagai jenis fitur untuk menghasilkan representasi lengkap dari konten game.

### Perhitungan Similaritas Kosinus
```bash
cosine_sim = cosine_similarity(combined_feature, combined_feature)
```

Similaritas antar game dihitung menggunakan cosine similarity dari matriks fitur gabungan. Alasannya yaitu agar memungkinkan pengukuran kemiripan antar game berdasarkan konten, yang menjadi dasar rekomendasi content-based.

### Mapping Indeks dan ID Game
```bash
index_to_appid = dict(enumerate(df_cbf['app_id']))
appid_to_index = {v: k for k, v in index_to_appid.items()}
```

Membuat mapping dua arah antara indeks dan app_id untuk mempermudah pencarian dan pengambilan data dalam proses rekomendasi. Alasannya yaitu untuk memudahkan operasi lookup saat mengakses hasil similarity dan rekomendasi.
## Modeling



### Collaborative Filtering (CF) dengan Deep Learning Embedding

```bash
# Embedding layers
user_embedding = Embedding(input_dim=n_users, output_dim=embedding_size)(user_input)
app_embedding = Embedding(input_dim=n_apps, output_dim=embedding_size)(app_input)

# Flatten and concatenate
user_vec = Flatten()(user_embedding)
app_vec = Flatten()(app_embedding)
x = Concatenate()([user_vec, app_vec])
x = Dense(128, activation='relu')(x)
x = Dropout(0.2)(x)
x = Dense(64, activation='relu')(x)
output = Dense(1)(x)

model = Model(inputs=[user_input, app_input], outputs=output)
model.compile(optimizer='adam', loss='mse')
```

Tujuan Penerapan Collaborative Filtering pada sistem rekomendasi game pada steam ini adalah untuk memberikan rekomendasi game berdasarkan interaksi pengguna (user-game interaction), seperti apakah game direkomendasikan dan durasi bermain.

Cara kerja penggunaan model deep learning sebagai berikut:
**Arsitektur Model**
Embedding Layer, Membuat vektor representasi pengguna (user_embedding) dan aplikasi (app_embedding) dengan dimensi 32
Concatenation, Menggabungkan vektor pengguna dan aplikasi
Deep Layers: Jaringan neural dengan 128 dan 64 neuron dengan aktivasi ReLU
Regularisasi, Dropout 20% untuk mencegah overfitting
Output, Prediksi rating dengan aktivasi linear
**Proses Training**
Menggunakan loss function MSE dan optimizer Adam
Early stopping dengan patiens 3 epoch untuk optimalisasi waktu training
Validasi 10% data training


### Content-Based Filtering (CBF)

```bash
# Embedding layers
def recommend_cbf_top_n(app_id, n=5):
    if app_id not in appid_to_index:
        print("="*80)
        print(f"❌ Maaf, App ID {app_id} tidak ditemukan dalam database.")
        print("🔍 Pastikan App ID yang dimasukkan benar.")
        print("📌 Berikut beberapa contoh App ID yang tersedia:")

        sample_games = df_cbf[['app_id', 'title']].sample(5, random_state=42)
        for _, row in sample_games.iterrows():
            print(f"→ {row['app_id']} : {row['title']}")

        print("="*80)
        return None

    idx = appid_to_index[app_id]
    sim_scores = list(enumerate(cosine_sim[idx]))
    sim_scores = sorted(sim_scores, key=lambda x: x[1], reverse=True)

    top_indices = [i for i, _ in sim_scores[1:n+1]]
    top_apps = df_cbf.iloc[top_indices]

    main_title = df_cbf.iloc[idx]['title']
```

Tujuan Penerapan Content-Based Filtering (CBF) yaitu Memberikan rekomendasi berdasarkan kemiripan konten game (deskripsi, tags, rating, dsb).
Cara kerja penggunaan Content-Based Filtering pada sistem rekomendasi game sebagai berikut:
dimulai dengang menggunakan pendekatan menggunakan representasi teks (deskripsi dan tags) dalam bentuk TF-IDF vectorization. Menggabungkan fitur numerik seperti rating, jumlah review, dan harga setelah normalisasi. Menghitung cosine similarity antar game berdasarkan fitur konten gabungan.
Selanjutnya Daftar game yang paling mirip dengan game yang dipilih pengguna berdasarkan kemiripan konten. Terakhir Menampilkan N game dengan skor kemiripan tertinggi terhadap game input.

### Top-N Recommendation Output

**Collaborative filtering**

Jika user ditemukan, sistem memprediksi dan merekomendasikan game yang paling sesuai dengan preferensi historis pengguna.
Jika user tidak ditemukan (cold-start), sistem memberikan rekomendasi default berdasarkan popularitas (positive_ratio tertinggi).
berikut hasil outputnya:

![Image](https://github.com/user-attachments/assets/bda5e900-563d-40be-b076-e663328ad803)


**Content-Based Filtering**
Rekomendasi didasarkan pada kemiripan konten game yang sudah diketahui pengguna. Contohnya, jika pengguna menyukai game dengan app_id=826540 (Audio Trip), sistem akan menampilkan 5 game lain yang paling mirip dari sisi konten.
berikut hasil outputnya:

![Image](https://github.com/user-attachments/assets/54360617-3891-4439-b2c9-e43a2e97eb57)


### Kelebihan dan Kekurangan dari Setiap pendekatan


| Pendekatan             | Kelebihan                                                                                  | Kekurangan                                                                                  |
|-----------------------|--------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------|
| **Collaborative Filtering** | - Menggunakan interaksi pengguna nyata sehingga rekomendasi personalisasi tinggi.         | - Masalah cold start untuk pengguna atau item baru (data interaksi sedikit atau tidak ada). |
|                       | - Bisa menangkap preferensi laten yang tidak terlihat dari konten.                         | - Memerlukan data interaksi yang cukup banyak.                                             |
|                       | - Fleksibel dan dapat ditingkatkan dengan deep learning.                                  | - Model memerlukan waktu pelatihan dan tuning yang cukup.                                  |
| **Content-Based Filtering** | - Tidak bergantung pada data interaksi pengguna.                                         | - Rekomendasi cenderung terbatas pada konten yang mirip dan bisa menghasilkan rekomendasi monoton. |
|                       | - Dapat merekomendasikan item baru selama metadata konten tersedia.                       | - Kurang bisa menangkap preferensi laten pengguna.                                         |
|                       | - Mudah dijelaskan karena berdasarkan kemiripan konten.                                   | - Kualitas rekomendasi bergantung pada kualitas metadata.                                  |


Analisis Hasil Didapat bahwa:
- Collaborative Filtering menawarkan rekomendasi personalisasi yang lebih kuat yang didasarkan pada pola interaksi pengguna, yang ideal untuk platform dengan banyak data interaksi, tetapi memiliki keterbatasan pada awal yang dingin.

- Content-Based Filtering lebih baik untuk cold-start dan item baru, memberikan saran berdasarkan kemiripan konten, tetapi kurang variatif dan bisa terlalu "sempit".




## Evaluation

### Content-Based Filtering (CBF)

**Precision@N**
untuk Content-Based Filtering menggunakan matriks evaluasi Precision@N. Precision mengukur proporsi item yang direkomendasikan yang benar-benar relevan bagi pengguna. Dalam konteks sistem rekomendasi, precision@N didefinisikan sebagai:


![Image](https://github.com/user-attachments/assets/15687c83-5fbe-4c49-8c41-5592445bb97b)

Precision@N mengukur fraksi item yang direkomendasikan yang relevan untuk pengguna. Dalam implementasi CBF ini, relevansi ditentukan berdasarkan kesamaan genre antara game target dengan game yang direkomendasikan. Metrik ini sangat penting untuk sistem rekomendasi karena precision yang tinggi berarti lebih sedikit rekomendasi yang tidak relevan, yang kritis untuk menjaga kepercayaan dan kepuasan pengguna

### Collaborative Filtering (CF)

**Mean Absolute Error (MAE)**
Suatu metode dan perhitungan diperlukan untuk mengevaluasi kinerja sistem rekomendasi untuk mengukur kualitas prediksi yang dibuat oleh sistem.Salah satu teknik statistika yang digunakan untuk mengevaluasi akurasi suatu sistem adalah Mean Absolute Error (MAE). Ini dilakukan dengan membandingkan nilai hasil prediksi dengan nilai sesungguhnya pada data uji; semakin rendah nilai MAE, semakin akurat prediksi yang dihasilkan. Persamaan Mean Absolute Error adalah sebagai berikut:

![Image](https://github.com/user-attachments/assets/dde5a974-c885-4382-92b5-471d14c7639d)

dimana n adalah jumlah observasi, y_i adalah nilai aktual, dan ŷ_i adalah nilai prediksi. MSE memberikan bobot lebih besar pada error yang besar dibandingkan error yang kecil, sehingga lebih sensitif terhadap outlier.


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


### Hasil evaluasi model

1. Content-Based Filtering (CBF)

![Image](https://github.com/user-attachments/assets/310601ce-7826-40ad-babf-75a437c01464)


Berdasarkan hasil output diatas menunjukkan performa yang sangat baik. Berdasarkan evaluasi menggunakan metrik Precision@5 untuk App ID 826540, model berhasil merekomendasikan 5 game teratas yang semuanya memiliki genre yang relevan dengan game input. Dengan nilai precision sebesar 1.00, ini berarti 100% dari rekomendasi yang diberikan sesuai dengan preferensi genre pengguna, menandakan bahwa sistem CBF mampu memberikan rekomendasi yang sangat akurat dan relevan. 

2. Collaborative Filtering (CF)

![Image](https://github.com/user-attachments/assets/1bd93a0f-3392-41ab-941f-43d3722d6774)


Hasil pelatihan model Collaborative Filtering (CF) menunjukkan kemampuan prediksi rating pada data uji yang sangat baik. Menurut evaluasi yang dilakukan menggunakan metrik kesalahan rata-rata kuadrat (MSE) dan kesalahan dasar rata-rata kuadrat (RMSE), model memiliki nilai MSE sebesar 0,0196 dan RMSE sebesar 0,1402. Nilai MSE yang rendah menunjukkan bahwa rata-rata kuadrat selisih antara nilai aktual dan prediksi sangat kecil, dan nilai RMSE yang sekitar 0,14 menunjukkan bahwa rata-rata kesalahan prediksi model agak kecil dan akurat. Oleh karena itu, model Collaborative Filtering ini efektif dalam menghasilkan prediksi rating yang hampir sama dengan nilai sebenarnya; sebagai hasilnya, model dapat diandalkan untuk membuat rekomendasi yang tepat berdasarkan pola interaksi pengguna.

![Image](https://github.com/user-attachments/assets/b1e20996-1398-41c5-9082-4f5ff07285ff)

Visualisasi diatas menunjukkan kurva loss (Mean Squared Error - MSE) selama proses pelatihan model machine learning, dengan dua garis:

* Train Loss (Biru): Menunjukkan seberapa besar kesalahan model pada data pelatihan.
* Validation Loss (Oranye): Menunjukkan kesalahan model saat diuji pada data validasi (data yang tidak dilihat saat pelatihan).

Seperti yang ditunjukkan oleh visualisasi kTraining dan Validation Loss, model mengalami overfitting. Meskipun Train loss terus menurun, validation loss stagnan dan sedikit meningkat setelah fase pertama, menunjukkan bahwa model hanya belajar dari data pelatihan tanpa mampu menggeneralisasi ke data baru. Titik optimal pelatihan kemungkinan akan tercapai lebih awal, dan adanya jarak yang lebar antara kehilangan train dan validasi menunjukkan bahwa kemampuan generalisasi rendah. Ada kemungkinan bahwa hal ini disebabkan oleh model yang terlalu kompleks atau data yang terlalu sedikit dan sparsity tinggi; kedua kondisi ini biasanya terjadi saat menggunakan filter kolaboratif.

Sebagai langkah penelitian selanjutnya, disarankan untuk:
1. menerapkan  early stopping dengan modifikasi parameter lebih baik agar pelatihan berhenti saat performa validasi tidak membaik
2. menambahkan regularisasi, seperti dropout atau L2
3. menyederhanakan arsitektur model
4. mengtuning hyperparameter
5. mengevaluasi dan memperluas jumlah dan kualitas data, misalnya dengan memfilter pengguna atau item yang terlalu jarang muncul untuk mengurangi sparsity.


**Kesimpulan**
Dari hasil evaluasi, tidak ada satu algoritma yang mutlak lebih baik secara umum karena keduanya memiliki keunggulan dan keterbatasan masing-masing:

- Collaborative Filtering (CF) menggunakan data interaksi pengguna untuk memberikan rekomendasi yang sangat personal dengan akurasi prediksi yang baik (RMSE 0.1402). Namun, CF mengalami kesulitan pada pengguna atau item baru (cold start).

- Content-Based Filtering (CBF) merekomendasikan game berdasarkan kemiripan konten seperti genre dan deskripsi, dengan precision@5 sebesar 1.00, menunjukkan rekomendasi yang relevan secara konten. Kelemahannya, rekomendasi cenderung monoton dan terbatas pada fitur yang ada

Pendekatan hybrid yang menggabungkan CF dan CBF adalah solusi terbaik untuk sistem rekomendasi game yang efektif di masa depan dan membantu pengguna memilih game yang tepat tanpa kebingungan. Pendekatan hybrid memanfaatkan personalisasi CF dan kemampuan cold start CBF untuk mengatasi keterbatasan masing-masing metode.


## Referensi


[1]	S. Batra, V. Sharma, X. Wang, Y. Wang, and Y. Sun, “STEAM RECOMMENDATION SYSTEM Group 1,” arxiv.org, 2022, Accessed: May 31, 2025. [Online]. Available: https://arxiv.org/pdf/2305.04890

[2]	B. R. Nugraha and A. Waworuntu, “Leveraging Content-Based Filtering for Personalized Game Recommendations: A Flutter-Based Mobile Application Development,” Ultimatics : Jurnal Teknik Informatika, vol. 16, no. 2, p. 149, 2024, Accessed: May 31, 2025. [Online]. Available: https://www.researchgate.net/publication/391629222_Leveraging_Content-Based_Filtering_for_Personalized_Game_Recommendations_A_Flutter-Based_Mobile_Application_Development

[3]	R. Bunga, F. Batista, and R. Ribeiro, “From Implicit Preferences to Ratings: Video Games Recommendation based on Collaborative Filtering,” in International Joint Conference on Knowledge Discovery, Knowledge Engineering and Knowledge Management, IC3K - Proceedings, Science and Technology Publications, Lda, 2021, pp. 209–216. doi: 10.5220/0010655900003064.


**---Ini adalah bagian akhir laporan---**