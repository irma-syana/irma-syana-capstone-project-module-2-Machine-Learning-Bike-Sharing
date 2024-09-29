# <p style="text-align:center;">**BIKE SHARING**</p>
### <p style="text-align:center;">**Capstone Modul 3**</p>
----
<p style="text-align:center;">Irma Lusyana</p>

# Business Problem Understanding
**Context**

Versi modern dari `Bike Sharing` kini memfasilitasi pengguna dapat menyewa sepeda di satu lokasi dan mengembalikannya di lokasi lain. Pengguna sistem ini juga tidak harus mendaftar keanggotaan, sehingga siapapun dapat mengakses dan menikmati layanannya. Pada 2012, ada lebih dari 500 program Bike Sharing di seluruh dunia yang mencakup lebih dari 500 ribu sepeda.

Pasar Bike Sharing di dunia melesat hingga $1.6 miliar atau Rp24 triliun (kurs Rp15.000) pada tahun 2016 atau hampir 3 kali lipat dibandingkan 2013. Dua alasan perkembangan terjadi adalah kebutuhan masyarakat mengatasi kemacetan dan kebutuhan para perusahaan teknologi yang bersedia menginvestasikan nilai besar untuk memahami data tingkah laku user. Secara umum, sistem Bike Sharing sangat diminati karena perannya yang penting meningkatkan mobilitas, mengurangi emisi karbon, dan mempromosikan gaya hidup sehat.

Sistem Bike Sharing yang sudah terdigitalisasi saat ini sudah mengumpulkan data yang berkaitan dengan perilaku pengguna, sehingga dapat dimanfaatkan para analis untuk memprediksikan jumlah pengguna di masa yang akan datang.

[Ledakan Bisnis Bike-Sharing Cina, Bagaimana Kansnya di Indonesia?](https://tirto.id/ledakan-bisnis-bike-sharing-cina-bagaimana-kansnya-di-indonesia-cJh5)

**Problem Statement**

- Perencanaan yang buruk dan persaingan yang ketat menciptakan kekacauan logistic di beberapa daerah
- Industri yang gagal akan menciptakan ‘kuburan sepeda’ menciptakan limbah industry baru

China (2018) mengalami over supply sehingga inventaris begitu banyak tidak terawat dan didayagunakan dengan baik. ["The Vast Bicycle Graveyards of China"](https://www.bbc.com/future/article/20210112-the-vast-bicycle-graveyards-of-china)

**Goals:** 

- Mendefenisikan perilaku penyewa Bike Sharing atas fitur yang tersedia
- Membandingkan beberapa model regresi untuk memperoleh nilai error yang rendah dalam memprediksi jumlah penyewa
- Mengerti tentang model regresi dan memilih model terbaik dalam memprediksi jumlah optimal penyewa sepeda
- Mampu memproyeksikan keuntungan bisnis jika menggunakan machine learning, dibandingkan dengan rule based
- Membuat rekomendasi atas hasil analisa

Rule based sebagai berikut:

- Hari bukan libur sebagai hari kerja yang jumlah penyewanya lebih banyak
    - Senin - Jumat : Hari kerja (cenderung meningkat)
    - Sabtu - Minggu : Akhir Pekan (cenderung berkurang)
- Pengkategorian waktu dibagi menjadi 3, yaitu:
    - Pagi : 06.00 - 12.00 (banyak penyewa)
    - Siang : >12.00 - 18.00 (lebih banyak penyewa)
    - Malam : >18.00 dan <06.00 (sedikit penyewa)
- Suhu semakin tinggi (banyak penyewa)

[potensi penerapan bike sharing](https://repo.itera.ac.id/assets/file_upload/SB2102020004/22116115_20_105950.pdf)

**Analytic Approach:** 

Analisa dilakukan terhadap data dengan menemukan pola dari fitur-fitur yang tersedia, serta bagaimana tiap fitur tersebut mempengaruhi jumlah ketersediaan unit sepeda. Selanjutnya, akan dibangun suatu **model regresi** yang akan membantu dalam menentukan jumlah unit sepeda yang perlu disediakan sehingga berguna untuk optimisasi infrastruktur dan efisiensi biaya operasional.

**Evaluation Metric**

Metric evaluation yang digunakan dalam model regresi guna memprediksi jumlah total penyewaan sepeda:

>- Mean Absolute Error (MAE): Mengukur rata-rata kesalahan absolut antara prediksi dan nilai aktual. Memberikan gambaran sederhana tentang kesalahan rata-rata.
>- Mean Squared Error (MSE): Menghitung rata-rata dari kuadrat kesalahan, memberikan penalti yang lebih besar untuk kesalahan besar.
>- Root Mean Squared Error (RMSE): Akar dari MSE, memberikan hasil dalam unit yang sama dengan target, sehingga lebih mudah diinterpretasikan.
>- Mean Absolute Percentage Error (MAPE): Mengukur kesalahan prediksi dalam persentase, berguna untuk mengetahui seberapa jauh prediksi dari nilai aktual dalam bentuk relatif.
>- R-squared (R²): Mengukur seberapa baik model menjelaskan variasi dalam data. Nilai mendekati 1 menunjukkan model yang baik.

Hasil akhir akan dipilih melalui perbandingan RMSE terbaik karena RMSE memberikan penalti lebih besar daripada kesalahan kecil seperti MSE, tetapi tidak terlalu besar seperti MSE, juga lebih mudah diinterpretasikan.

[perbedaan-mae-mse-rmse-dan-mape](https://www.trivusi.web.id/2023/03/perbedaan-mae-mse-rmse-dan-mape.html)

[RMSE](https://statisticsbyjim.com/regression/root-mean-square-error-rmse/)

**Stakeholder**

Investor/sponsor, Pemerintah lokal, dan Tim operasional layanan (pengadaan)

# Data Understanding

## Penjelasan setiap variable (Data Dictionary)
|Fitur | Deskripsi |
|---- | ---- |
| dteday | Tanggal (yyyy-mm-dd)|
| hum | Kelembaban yang dinormalisasi (dibagi dengan 100)|
| weathersit | Kondisi cuaca (1: Cerah, 2: Kabut, 3: Salju/Hujan Ringan, 4: Hujan/Salju Lebat) |
| holiday | Hari libur atau bukan (1: Ya, 0: Tidak)|
| season | Musim (1: Musim Dingin, 2: Musim Semi, 3: Musim Panas, 4: Musim Gugur)|
| hr | Jam dalam sehari (0 hingga 23)|
| atemp | Suhu rasa yang dinormalisasi dalam Celsius (berkisaran antara tmin=-16, tmax=+50) |
| temp | Suhu yang dinormalisasi dalam Celsius (berkisaran antara tmin=-8, tmax=+39) |
| casual | Jumlah pengguna kasual (pengguna tanpa keanggotaan)|
| registered | Jumlah pengguna terdaftar|
| cnt | Total jumlah sepeda yang disewa, termasuk pengguna kasual dan terdaftar |

## Missing Values
`Tidak ada data kosong` pada dataset

## Variable Numerik
### Statistika Deskriptif
![image](https://github.com/user-attachments/assets/3a793041-0e2e-4925-9047-696f816580ce)

**Pengamatan**

>- Dari hasil statistik data bike-sharing, rata-rata kelembaban udara (hum) tercatat sebesar 0.62. Mayoritas kondisi cuaca berada dalam kategori cerah atau berawan (kategori 1 dan 2). Hari libur tercatat hanya sekitar 3%. Suhu rata-rata (temp) mencapai 0.49, sementara suhu terasa (atemp) sekitar 0.47. Pengguna kasual rata-rata sekitar 35 orang per hari, dan pengguna terdaftar sebanyak 153 orang per hari. Menunjukkan kecenderungan masyarakat memilih untuk mendaftar. Rata-rata total penyewaan sepeda per hari mencapai 189 unit, dengan maksimum 970 unit penyewaan.

Terdapat `nilai minimum 0` pada:
>- Fitur `hum`, menandakan kelembapan sangat rendah atau 0 persen kelembapan
>- Fitur `holiday`, menandakan kondisi tidak libur (pengkategorian)
>- Fitur `atemp`, menandakan kondisi suhu yang sangat dingin -16 degC
>- Fitur `hr`, menandakan aktifitas penggunaan pada jam 0 (tengah malam)
>- Fitur `casual`, menandakan tidak ada pengguna tanpa keanggotaan
>- Fitur `registered`, tidak ada pengguna terdaftar

Nilai 0 pada fitur holiday, hr, casual, registered menunjukkan kondisi wajar, sehingga akan dilakukan `pengecekan pada fitur ham dan atemp`

### Distribusi Data
![image](https://github.com/user-attachments/assets/ee99e45c-8c97-488b-b051-3e0b245bb4e8)

**Pengamatan**
>- hum (Kelembaban): Distribusi kelembaban cukup merata, dengan puncak pada nilai 1.0 (lembab)
>- weathersit (Kondisi Cuaca): Sebagian besar data menunjukkan cuaca kategori 1 (cerah atau berawan ringan).
>- holiday (Hari Libur): Mayoritas data menunjukkan bahwa hari-hari bukan hari libur.
>- season (Musim): Musim tampak terdistribusi merata di seluruh kategori.
>- atemp (Suhu Terasa) dan temp (Suhu): Kedua fitur ini cenderung memiliki pola yang sama, berbentuk seperti lonceng.
>- hr (Jam): Distribusi penyewaan sepeda tampak merata sepanjang hari, dengan peningkatan signifikan pada pukul 21:00.
>- casual (Pengguna Kasual): Mayoritas pengguna kasual melakukan penyewaan kurang dari 50 kali, dengan jumlah yang menurun pada frekuensi lebih tinggi.
registered (Pengguna Terdaftar): Sebagian besar pengguna terdaftar menyewa sepeda dengan frekuensi rendah, dengan distribusi yang menurun untuk pengguna yang lebih sering.
>- cnt (Total Penyewaan): Total penyewaan memiliki distribusi yang serupa dengan pengguna terdaftar, dengan sebagian besar penyewaan di bawah 200 unit per hari.

#### Uji statistika
akan dilakukan uji statistika untuk mengecek normalisasi data dengan menggunakan D’Agostino-Pearson karena dataset memiliki 12ribu baris
![image](https://github.com/user-attachments/assets/b8ef5102-2d24-4511-aa62-d93ab4a4a13c)

### Outliers
![image](https://github.com/user-attachments/assets/209e80bd-5e05-4c2a-acd1-153b7269ebf3)

**Pengamatan**

>- Kelembaban dan suhu: Sebagian besar data berada pada rentang yang normal tanpa banyak outlier.
>- Pengguna kasual dan terdaftar: Terdapat sejumlah outlier dengan jumlah penyewaan yang sangat tinggi, terutama di atas 50 untuk pengguna kasual dan 600 untuk pengguna terdaftar.
>- Total penyewaan: Distribusi total penyewaan sepeda menunjukkan mayoritas berada di bawah 400, dengan beberapa outlier di atas 600.

### Korelasi
![image](https://github.com/user-attachments/assets/5bd7f0e8-9011-4d0d-9db6-d23fb6653d01)

**Pengamatan**
>- Cnt (Total Penyewaan) sangat berkorelasi positif dengan registered (pengguna terdaftar) (0.99) dan casual (pengguna kasual) (0.85). Ini menunjukkan bahwa kedua jenis pengguna secara langsung memengaruhi total penyewaan. Hal itu disebabkan karena cnt merupakan penjumlahan dari data casual dan registered
>- Temp dan atemp juga memiliki korelasi yang kuat dengan cnt (0.42) dan (0.42), menunjukkan bahwa suhu memengaruhi jumlah penyewaan. Terdapat juga korelasi yang positif antara kedua fitur tersebut
>- Hum (Kelembaban) dan weathersit (kondisi cuaca) menunjukkan korelasi negatif dengan cnt, masing-masing sebesar -0.36 dan -0.13, artinya cuaca buruk dan kelembaban tinggi menurunkan jumlah penyewaan. Terlihat juga korelasi yang positif antara hum dan weathershit

### Multikolineartias dengan VIF

![image](https://github.com/user-attachments/assets/f6c5ab70-287b-4b55-9e5a-954860539fb9)
**Pengamatan**

>- atemp (341.08) dan temp (306.85) memiliki nilai VIF yang sangat tinggi, menunjukkan multikolinearitas yang sangat kuat di antara keduanya. Ini berarti kedua variabel ini sangat berkorelasi satu sama lain dan bisa saling menggantikan.
>- hum (12.92), weathersit (7.15), dan season (6.96) juga memiliki VIF tinggi, menunjukkan korelasi yang signifikan dengan variabel lain.
>- registered (3.09) dan casual (2.58) memiliki VIF yang lebih rendah, menunjukkan mereka memiliki korelasi yang lebih sedikit dengan variabel lain.

Variabel dengan VIF tinggi (terutama di atas 10) perlu dievaluasi, dan mungkin ada baiknya mempertimbangkan untuk menghapus salah satunya untuk mengurangi multikolinearitas. Sehingga `atemp` dan `hum` akan di drop.

Variabel`casual`dan `registered` memiliki nilai VIF yang rendah, namun ternyata merupakan informasi yang sama. Sebaiknya di drop karena merupakan overlapping information (redundant) terhadap `cnt`

# Data Cleaning
## Drop data duplicate
## Drop fitur `hum`, `atemp`, `weathersit`, `casual`, dan `registered`
## Split fitur `dteday`
## Drop fitur `dteday`
## Update ketarangan fitur `weathersit`, `holiday`, `season`

# Explanatory data analysis (EDA)
## Jumlah penyewa berdasarkan  musim
![image](https://github.com/user-attachments/assets/fd641f11-b07b-4a6f-85f9-9a41cdec65fb)

## Proporsi penyewa (Libur vs Bukan Libur)
![image](https://github.com/user-attachments/assets/280c595f-271e-4192-be30-78801a6aa41b)

## Jumlah penyewa terhadap fitur lain
![image](https://github.com/user-attachments/assets/586e0b50-2616-42c0-9082-e6d4e5740138)

Jika kita melakukan  perbandingan antara fitur hari, jam, dan suhu terhadap jumlah penyewa, diperoleh hasil sbagai berikut:
>- Jumlah penyewa secara perlahan meningkat dari hari-1 (senin) dan mulai berkurang setelah weekend di hari 6 (Sabtu) dan sangat rendah di hari minggu
>- Jumlah penyewa fulktuatif pada pagi hari (6-12) cenderung lebih tinggi pada jam 7-8, meningkat di siang hari (12-18),  dan berkurang di malam hari (18-6)
>- Jumlah penyewa cenderung meningkat seiring dengan penambahan suhu

![image](https://github.com/user-attachments/assets/1ce4b658-e0d9-4655-8b88-91440c719c82)
>- Jika dilihat berdasarkan jenis musimnya, pada tiap musim cenderung meningkat seiring kenaikan suhu namun kembali turun secara signifikan setelah mencapai suhu tertinggi di tiap musim. 
>- Secara umum, terlihat bahwa penyewa `mendominasi pada suhu tinggi`
>- Musim panas mengalami peningkatan cukup signifikan seiring dengan kenaikan suhu, sementara musim dingin memiliki sedikit variasi/jumlah penyewa yang relatif tetap seiring perubahan suhu.

## Penyewa per Jam (Libur vs Bukan Libur)
![image](https://github.com/user-attachments/assets/3008260b-b0ec-45e7-bf84-9962d4f5014f)
**Pengamatan**

Melalui tiap kesimpulan Explanatory Data Analysis tersebut, kita akan mengasumsikan sebagai berikut:
- Hari bukan libur sebagai hari kerja yang jumlah penyewanya lebih banyak
    - Senin - Jumat : Hari kerja (cenderung meningkat)
    - Sabtu - Minggu : Akhir Pekan (cenderung berkurang)
- Pengkategorian waktu dibagi menjadi 3, yaitu:
    - Pagi : 06.00 - 12.00 (banyak penyewa)
    - Siang : >12.00 - 18.00 (lebih banyak penyewa)
    - Malam : >18.00 dan <06.00 (sedikit penyewa)
- Suhu semakin tinggi (banyak penyewa)

  # Data Preprocessing
![image](https://github.com/user-attachments/assets/81b326c8-e95f-45b1-a411-b4d0ff9c8299)

## Train dan Test Splitting
![image](https://github.com/user-attachments/assets/bd51a2af-236d-441d-a3d3-9f5d7884fc0b)

## Data Preparation
Berdasarkan pertimbangan jumlah data unik diatas, hasil analisa outlier, dan analisa jenis distribusi data (tidak normal), maka:
>- Fitur numerik menggunakan `minmax`
>- Fitur kategorik `day, month, year` encoding dengan `ordinal` untuk efisiensi encoding. Karena ketika menggunakan `binary` proses pengolahan data sangat lama, saya memutuskan untuk menggunakan encoder ini. _Menurut Max Kuhn dan Kjell Johnson  "Feature Engineering and Selection: A Practical Approach for Predictive Models", dijelaskan fitur kategori terbatas 'month, day, dan year' masuk akal secara semantik diencode dalam konteks data._
>- `musim dan ket_libur` menggunakan `onehot` karena fitur tidak memiliki urutan dan unique value <5  

[Serokell Software Development Company](https://serokell.io/blog/feature-engineering-for-machine-learning)

![image](https://github.com/user-attachments/assets/c969cd4c-fd33-462c-b748-7da880672322)

# Modeling
## Rule Based Model (Non ML)
Kita akan membuat rule based/aturan dasar berdasarkan ambang batas tertentu pada kategori `hari & jam`, `bulan, musim & suhu`, keterangan `libur` atas jumlah penyewa:

- Hari & jam:
    - Pada hari kerja jumlah penyewa cenderung meningkat dan cenderung berkurang pada akhir pekan (sabtu & minggu)
    - Jam pagi (06.00 - 12.00) banyak penyewa, siang(>12.00 - 18.00) lebih banyak penyewa, dan malam ( >18.00 dan <06.00) sedikit penyewa
-  Bulan, musim, dan suhu:
    - Musim panas (Juni - Agustus) suhu >30°C, penyewa paling tinggi karena turis menggunakan untuk rekreasi dan harian
    - Musim dingin (Desember - Februari) suhu 0°C - 10°C, penyewa rendah
    - Musim semi (Maret - Mei) dan musim gugur (Sebtember - November) suhu 10°C - 25°C penyewa cenderung tinggi
- Hari kerja pengguna sangat tinggi

note:
- inisiasi_bobot : 1
- highest bobot : 1.5
- lowest bobot : 0.5

![image](https://github.com/user-attachments/assets/7bb99c25-76cf-48ed-b498-b93c0e89cb58)

## Experimen 1: Based Model - Model Tanpa Transformasi Target
Pada base model experimen 1, kita akan membuat beberapa model regresi tanpa transformasi target. Proses ini bekerja langsung pada data asli (baik fitur maupun target) dan model mencoba untuk memprediksi nilai target sesuai skala asli dari data tersebut.
![image](https://github.com/user-attachments/assets/843b0251-a63d-41fa-b0f4-a415852932a0)

**Pengamatan**
- Model `XGBoost Regression`secara konsisten menjadi model yang terbaik di seluruh metrik, baik data pelatihan (train) maupun data pengujian (test)
- Linear Regression memiliki performa terburuk dibandingkan dengan model lainnya, terutama dalam hal MAE, MSE, dan RMSE.
- RandomForest Regression dan DecisionTree Regression juga menunjukkan performa yang baik, tetapi tidak sebaik XGBoost.

- ## Experimen 2: Based Model - Model dengan Transformasi Target
- Pada base model experimen 2, kita membuat beberapa model regresi ditransformasikan dengan  TransformedTargetRegressor yang mmelakukan transformasi logaritmik terhadap target (y), yang kemudian mengembalikan ke skala aslinya menggunakan inverse log (fungsi eksponensial np.exp)
- ![image](https://github.com/user-attachments/assets/51ef898d-264c-4387-b61e-d26e45892423)

- **Pengamatan**

Sama seperti experimen 1, `XGBoost Regression` menjadi model terbaik.

Melalui experimen 1 dan 2, terlihat bahwa model tanpa transformasi memiliki score yang lebih baik dan tidak signifikan terhadap model yang ditransformasi. Artinya, data sudah relatif terdistribusi dengan baik, sehingga pada proses selanjutnya `model dilakukan tanpa proses transformasi`.  

## Experimen 3: Hapus Outlier
![image](https://github.com/user-attachments/assets/eef4c674-3593-4a0a-bbe4-f424c0736306)

![image](https://github.com/user-attachments/assets/e25f7039-903a-419e-b791-c49bc7520811)

## Hasil Eksperimen
![image](https://github.com/user-attachments/assets/359b4ac0-0566-44e2-9785-58ab8823e703)
**Pengamatan**

XGBoost Regression adalah model terbaik di semua eksperimen, baik tanpa transformasi, dengan transformasi, ataupun setelah menghapus outlier.
`Eksperimen Hapus Outlier` menghasilkan RMSE terbaik untuk tiap score train dan test adalah yang dihighlight hijau, sehingga menangani outlier dengan benar dapat meningkatkan prediksi secara signifikan.

## Hyperparameter tuning
![image](https://github.com/user-attachments/assets/30426dbd-a441-4bb7-962c-aac5bf403e39)

## Feature Importance
![image](https://github.com/user-attachments/assets/30da30b6-11ed-4f74-8873-1dd1f4f53cfb)
![image](https://github.com/user-attachments/assets/462af980-f5d8-4f97-afb9-8d5c7abc4e6c)

## Visualisasi Prediksi

![image](https://github.com/user-attachments/assets/c5188127-515a-40f4-bfcd-ea76731739d2)
Residual Plot (kiri):

Residual adalah selisih antara nilai aktual dan nilai prediksi dari model.
Grafik ini menunjukkan residual terhadap prediksi, di mana garis merah adalah garis nol yang merepresentasikan tidak adanya kesalahan prediksi.
Interpretasi:
>- Sebagian besar residual berada di sekitar garis nol, yang berarti model memiliki performa yang baik karena kesalahan prediksinya kecil.
Namun, ada beberapa outlier atau kesalahan besar yang terlihat (di atas dan di bawah residual = ±200), yang menunjukkan adanya data yang tidak diprediksi dengan baik oleh model.
>- Pola acak pada residual menunjukkan bahwa model tidak mengalami heteroskedastisitas (penyebaran kesalahan yang bervariasi) atau pola sistematis tertentu, yang menunjukkan bahwa asumsi homoskedastisitas terpenuhi dan model cukup baik dalam memprediksi.

Aktual vs. Prediksi (kanan):

Grafik ini membandingkan nilai aktual dengan nilai prediksi yang dihasilkan oleh model.
Interpretasi:
>- Titik-titik yang mendekati garis diagonal menunjukkan prediksi yang sangat akurat.
Semakin banyak titik yang berada di dekat garis diagonal ini, semakin baik model dalam memprediksi nilai sebenarnya.
>- Pada grafik ini, sebagian besar titik berada di sekitar garis diagonal, yang mengindikasikan bahwa model cukup baik dalam melakukan prediksi. Namun, terdapat beberapa deviasi di luar garis yang menunjukkan adanya kesalahan prediksi pada beberapa titik.

*Source: Lewis, C. D. (1982). Industrial and business forecasting methods: A practical guide to exponential smoothing and curve fitting

## RMSE pada rentang tertentu
![image](https://github.com/user-attachments/assets/c327b254-21ed-4695-b2d7-b50f75ec6323)
**Pengamatan**

Ternyata model memberikan akurasi yang baik pada rentang 0-200 dengan nilai RMSE <50 atau pada rentang 9 - 48. Akurasi model secara konsisten menurun untuk analisis prediktif pada rentang >200.

# Limitasi
Model tampak bekerja lebih baik pada rentang prediksi 50 - 200. Fitur yang baik menurut model menggunakan XGBoost adalah jam, year, musim, dan suhu. Data yang digunakan dalam analisa ini adalah tahun 2011 - 2012, sementara fitur lainnya dengan range data terbaik adalah sebagai berikut:
| Feature | Range |
|---|---|
| Jam | 06.00 - 10.00 & 15.00 - 18.00 |
| hari | Senin - Sabtu|
| Musim | Panas, semi, gugur|
| Suhu | > 0.7 atau >24.9°C|

## Estimasi Keuntungan
Jika diasumsikan perusahaan memproyeksikan jumlah sepeda yang di sewa menggunakan `rule based atau dengan logika sederhana` dan kemudian `dibandingkan` dengan menggunakan `machine learning` dengan model XGBoost, diperoleh hasil sebagai berikut:
![image](https://github.com/user-attachments/assets/e37a2567-3da7-44e3-b878-ef4769ab6222)
![image](https://github.com/user-attachments/assets/4c238ab4-f518-4166-9d9c-bab1f06fbc87)
![image](https://github.com/user-attachments/assets/af5bac7a-1f08-4973-ad25-211a0bcd24ee)
**Pengamatan**:
Penggunaan machine learning menggunakan XGBoost (tuning Grid search) secara drastis mengurangi _error_ atas prediksi penyewaan sepeda. Diasumsikan nilai sepeda adalah $3.000,00 (kurs Rp16.000) sehingga diperoleh keuntungan atar proyeksi senilai +/- $650 atau Rp10 milliar.

[referensi harga](https://www.businessanalystlearnings.com/business-matters/2022/2/3/how-much-does-it-cost-to-implement-a-bike-share-system-in-2022) 

# **Kesimpulan dan Rekomendasi**
## Kesimpulan
Dari eksperimen yang dilakukan dengan menggunakan XGBoost Regression, analisa jumlah penyewaan sepeda menunjukkan bahwa model XGBoost adalah yang terbaik di semua percobaan, baik tanpa transformasi, dengan transformasi, ataupun setelah menghapus outlier. Berikut poin-poin utama yang mendasari kesimpulan ini:
1. **Pengaruh Penghapusan Outlier**:
Eksperimen Hapus Outlier menghasilkan nilai RMSE terbaik untuk data train dan test. Menangani outlier dengan benar dapat meningkatkan akurasi prediksi secara signifikan.
Penghapusan outlier menunjukkan peningkatan kinerja model, menghasilkan nilai RMSE yang lebih rendah, yang menunjukkan bahwa model lebih baik dalam memprediksi penyewaan sepeda.

2. **Kekuatan Model XGBoost**:
XGBoost menggunakan teknik boosting, di mana model dibangun secara berurutan untuk memperbaiki kesalahan dari model sebelumnya, dengan memanfaatkan gradient descent untuk meminimalkan kesalahan prediksi secara bertahap. XGBoost secara konsisten memberikan score MSE, RMSE, MAPE, MAE, dan r-squared terbaik pada tiap experimen  

3. **Performa Model dengan Grid Search**:
Grid Search CV menghasilkan performa terbaik dengan RMSE 47.69 penyewa untuk train dan 45.59 penyewa untuk test, mengalahkan Randomized Search CV dan model sebelum tuning.
Hal ini menunjukkan bahwa tuning dengan Grid Search memberikan hasil yang lebih akurat dibandingkan metode tuning lainnya, terutama dalam hal meminimalkan kesalahan prediksi.

4. **Feature Importance**:
Fitur yang memiliki pengaruh paling signifikan terhadap prediksi adalah jam, year, dan musim, dengan kontribusi dari fitur lain seperti suhu yang juga berdampak positif dengan importance 0.13 - 0.32
Data menunjukkan adanya peningkatan tren penyewaan dari tahun ke tahun, serta peningkatan penyewaan pada waktu tertentu dalam sehari dan musim tertentu (seperti musim gugur).

5. **Rentang Prediksi Optimum**:
Rentang prediksi optimum terletak pada 0-200, dengan RMSE di bawah 50. Di rentang ini, model bekerja dengan sangat baik, sementara akurasi menurun untuk rentang di atas 200.
Fitur seperti jam, tahun, musim, dan suhu memberikan kontribusi yang signifikan terhadap prediksi model, dan model menunjukkan akurasi yang tinggi di rentang ini.

## Rekomendasi
- Gunakan XGBoost dengan Grid Search Tuning untuk meningkatkan akurasi prediksi penyewaan sepeda, terutama dalam mengatasi outlier.
Fokus pada rentang prediksi 0-200 untuk analisis prediktif yang lebih akurat, karena pada rentang ini RMSE lebih rendah dan prediksi lebih tepat.
- Pertimbangkan faktor jam, tahun, dan musim dalam membuat prediksi, karena faktor-faktor ini memiliki pengaruh yang signifikan pada jumlah penyewaan sepeda.
- Penghapusan outlier secara tepat akan membantu meningkatkan akurasi model lebih jauh dan mengurangi kesalahan prediksi.
- Potensi Keuntungan: Jika proyeksi penyewaan sepeda dilakukan dengan logika sederhana dan dibandingkan dengan prediksi menggunakan machine learning (XGBoost), penggunaan machine learning mampu mengurangi error prediksi, yang berdampak pada potensi keuntungan signifikan, diproyeksikan sekitar Rp10 miliar jika diasumsikan nilai sepeda sebesar $3.000 (kurs Rp16.000).

- # **Save Model**




























