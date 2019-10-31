# Menambang Data Spasial Fasilitas Kesehatan dengan R
(Materi Meet-up IDJN, 31 Oktober 2019)

<b>Background</b>

Proses pencarian data lokasi fasilitas kesehatan di Indonesia terbilang cukup panjang. Di awal pengerjaan proyek liputan kolaborasi ini, kita telah mencoba menambang data rumah sakit dari OpenstreetMap. Dari sana, kita mendapatkan sekitar 1.000 titik lokasi rumah sakit di Indonesia.

Data itu kemudian kita verifikasi dengan data dari Kementerian Kesehatan. Kita menemukan ada perbedaan jumlah. Lalu, kita sepakati untuk pakai data dari Kemenkes, dengan catatan, melakukan <b>geocoding</b>. Saya mencoba melakukan geocoding otomatis, namun, titiknya tak sesuai alamat. Jalan lainnya, geocoding manual, satu per satu. Dan itu pasti melelahkan.

Hari ini, kita coba cara lain dan mungkin saja kita beruntung. 

Indonesia punya kebijkan baru soal one map policy. Jadi, ada portal khusus yang menyimpan semua data spasial. Sayangnya, akses ke portal itu terbatas, dan tidak ada fasilitas untuk mendapatkan data mentahnya. 

Untungnya, data itu disimpan di server ArcGIS dan (masih) terbuka. Data yang tersimpan di server itu, bisa kita panggil lewat REpresentational State Transfer Application Protocol Interface, singkatnya, <b>REST API</b>. 

Cara kerjanya, REST client (kita) akan mengakses data ke REST server. Masing-masing data itu dibedakan oleh sebuah global ID atau URIs (Universal Resource Identifiers). Sederhananya, kita bisa request ke server untuk ngasi datanya dalam format tertentu. Kita bisa melakukannya dengan R.

Kalau belum install dan paham prinsip dasar R, baca di sini [https://idjnetwork.org/2019/tutorial/langkah-langkah-dasar-untuk-belajar-r/]

<b>Langkah-langkahnya:<b>

Install package bernama 'devtools'. Fungsinya, untuk menginstall GitHub.
```
install.packages("devtools")
library(devtools)
```
Install GitHub "younghah/esri2sf" 
```
install_github("yonghah/esri2sf")
library("esri2sf")
```
Simpan global data ID (dalam hal ini link url dari layer yang kita inginkan)
```
url <- "https://portal.ina-sdi.or.id/arcgis/rest/services/Lingkungan_Terbangun/RBI_50K_Fasilitas_Kesehatan/MapServer/1"
```
Simpan dalam bentuk dataframe
```
rumahsakit <- esri2sf(url)
```
Bikin plot sederhana
```
plot(rumahsakit)
```
Simpan dalam format csv 
```
write.csv(rumahsakit, file = "rumahsakit.csv")
```
Data spasial dalam format CSV akan muncul di folder
