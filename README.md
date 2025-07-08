# System Recomendation Produk Amazon

![image](https://github.com/user-attachments/assets/0b37f45f-9de9-4fe1-bd86-5c83425f6343)

---------------------------------------------

## **Latar Belakang**

Seiring berkembangnya e-commerce, konsumen kini dihadapkan dengan **jutaan produk** yang tersedia secara daring. Platform seperti Amazon menyediakan berbagai kategori barang mulai dari elektronik, fashion, buku, hingga kebutuhan rumah tangga. Namun, banyaknya pilihan ini sering kali membuat pengguna merasa kewalahan dalam menentukan produk yang sesuai dengan preferensi mereka. Untuk menjawab tantangan ini, sistem rekomendasi hadir sebagai solusi penting untuk menyaring dan menyajikan produk yang paling relevan kepada setiap pengguna.

**Sistem rekomendasi** telah menjadi elemen vital dalam meningkatkan pengalaman pengguna, loyalitas pelanggan, serta mendorong pertumbuhan penjualan di berbagai platform digital. Salah satu dataset yang populer untuk mengembangkan sistem semacam ini adalah **Amazon Product Dataset**, yang berisi informasi ulasan, metadata produk, serta interaksi pengguna dengan produk.

Dalam proyek ini, dikembangkan sebuah sistem rekomendasi produk menggunakan tiga pendekatan utama:

1. **Content-Based Filtering (CBF)**
   Pendekatan ini merekomendasikan produk berdasarkan **kesamaan fitur konten produk** (misalnya: deskripsi, kategori, merek), yang dibandingkan dengan produk yang disukai pengguna sebelumnya.

2. **Collaborative Filtering (CF)**
   Pendekatan ini memanfaatkan **pola interaksi antar pengguna** dan produk (seperti ulasan atau rating) untuk menemukan kesamaan preferensi antar pengguna, bahkan tanpa melihat isi produk itu sendiri.

3. **Hybrid Recommendation System**
   Sistem ini menggabungkan keunggulan dari metode CBF dan CF untuk menghasilkan rekomendasi yang lebih **personal, akurat, dan tahan terhadap cold-start problem**, baik pada sisi pengguna baru maupun produk baru.

Dengan membandingkan dan mengimplementasikan ketiga pendekatan tersebut, proyek ini bertujuan untuk menghasilkan sistem rekomendasi produk yang **efisien dan responsif terhadap kebutuhan pengguna**, serta mendemonstrasikan bagaimana sistem rekomendasi dapat dioptimalkan untuk platform berskala besar seperti Amazon.

---------------------------------------------

## **Business Understanding**

### **1. Problem Statements**

* Pengguna Amazon menghadapi kesulitan dalam menemukan produk yang sesuai dengan preferensi mereka di tengah jutaan produk yang tersedia.
* Sistem pencarian tradisional sering kali tidak cukup personal, sehingga pengguna harus melakukan banyak pencarian manual.
* Rekomendasi produk yang tidak relevan atau terlalu umum dapat menurunkan pengalaman pengguna dan mengurangi tingkat konversi penjualan.
* Belum ada sistem rekomendasi yang secara optimal menggabungkan informasi dari fitur produk dan perilaku pengguna secara bersamaan untuk menghasilkan rekomendasi yang akurat.

### **2. Goals**

* Membangun dan membandingkan **tiga pendekatan sistem rekomendasi**:

  * **Content-Based Filtering (CBF)**
  * **Collaborative Filtering (CF)**
  * **Hybrid Recommendation System**
* Meningkatkan relevansi dan personalisasi rekomendasi produk untuk pengguna berdasarkan **riwayat interaksi dan informasi produk**.
* Mengatasi **masalah cold-start** pada pengguna atau produk baru melalui pendekatan hybrid.
* Memberikan insight tentang efektivitas tiap metode rekomendasi dalam konteks data skala besar seperti Amazon.

### **3. Solution Statements**

* Menggunakan **Amazon Product Dataset** yang mencakup metadata produk, ulasan, dan interaksi pengguna sebagai dasar pembuatan sistem rekomendasi.
* Mengimplementasikan metode:

  * **CBF** dengan memanfaatkan fitur seperti deskripsi produk dan kategori menggunakan teknik NLP dan vektorisasi teks (misal: TF-IDF).
  * **CF** menggunakan pendekatan user-item interaction berbasis matrix factorization atau nearest neighbors.
  * **Hybrid model** untuk menggabungkan hasil dari CBF dan CF sehingga dapat saling melengkapi.
* Mengevaluasi dan membandingkan kinerja masing-masing model dengan metrik seperti **precision, recall, MAP, dan hit rate**, guna menentukan pendekatan terbaik untuk implementasi nyata.

---------------------------------------------

## **Data Understanding**

### **Sumber Dataset**

Dataset yang digunakan dalam proyek ini diperoleh dari platform **Kaggle**, dengan nama:
📎 **Amazon Sales Dataset**
📍Link: [https://www.kaggle.com/datasets/karkavelrajaj/amazon-sales-dataset](https://www.kaggle.com/datasets/karkavelrajaj/amazon-sales-dataset)

Dataset ini berisi lebih dari **1.000 data produk Amazon** beserta **ulasan dan penilaian pengguna**, yang diambil dari situs resmi Amazon. Dataset ini menyediakan informasi penting untuk membangun sistem rekomendasi berdasarkan **konten produk** dan **perilaku pengguna**.

### **Deskripsi Fitur**

Berikut adalah penjelasan setiap kolom dalam dataset:

| Nama Kolom            | Deskripsi                                                       |
| --------------------- | --------------------------------------------------------------- |
| `product_id`          | ID unik untuk setiap produk                                     |
| `product_name`        | Nama lengkap produk                                             |
| `category`            | Kategori atau jenis produk (misalnya: elektronik, fashion, dsb) |
| `discounted_price`    | Harga produk setelah diskon                                     |
| `actual_price`        | Harga asli sebelum diskon                                       |
| `discount_percentage` | Persentase diskon produk                                        |
| `rating`              | Rata-rata rating produk (misalnya: 4.5)                         |
| `rating_count`        | Jumlah pengguna yang memberikan rating                          |
| `about_product`       | Deskripsi lengkap produk                                        |
| `user_id`             | ID unik pengguna yang memberikan ulasan                         |
| `user_name`           | Nama pengguna                                                   |
| `review_id`           | ID ulasan                                                       |
| `review_title`        | Judul singkat ulasan                                            |
| `review_content`      | Isi lengkap dari ulasan pengguna                                |
| `img_link`            | URL gambar produk                                               |
| `product_link`        | URL ke halaman resmi produk di Amazon                           |

### **Kegunaan Fitur untuk Sistem Rekomendasi**

| Fitur                       | Relevansi untuk Model Rekomendasi                                   |
| --------------------------- | ------------------------------------------------------------------- |
| `about_product`, `category` | Digunakan untuk **Content-Based Filtering (CBF)**                   |
| `user_id`, `product_id`     | Digunakan untuk **Collaborative Filtering (CF)**                    |
| `rating`, `rating_count`    | Digunakan untuk bobot interaksi pada CF atau evaluasi rating produk |
| `review_content`            | Digunakan untuk analisis teks atau penambahan konteks konten        |


### **Observasi Awal**

* Data cukup lengkap untuk membangun sistem rekomendasi berbasis **CBF dan CF**.
* Informasi `user_id` dan `product_id` memungkinkan kita membentuk **user-item interaction matrix**.
* Kolom deskriptif seperti `about_product` dan `review_content` dapat diolah dengan teknik **NLP** seperti **TF-IDF** untuk mengukur kesamaan antar produk.

---------------------------------------------

## **Sistem Rekomendasi dengan Content-Based Filtering**

### **Pendekatan Content-Based Filtering**

Content-Based Filtering (CBF) adalah metode sistem rekomendasi yang bekerja dengan cara **membandingkan kesamaan konten** antar produk. Dalam proyek ini, sistem dibangun menggunakan **representasi teks gabungan** dari kolom `product_name`, `category`, `about_product`, dan `review_content`, kemudian dihitung kemiripannya menggunakan metode **TF-IDF dan cosine similarity**.

### **Tahapan Implementasi**

#### Seleksi Fitur

Memilih fitur-fitur penting yang mendeskripsikan produk, serta membuang kolom yang tidak digunakan dalam perhitungan kesamaan.

#### Feature Engineering

* Menggabungkan teks dari berbagai kolom menjadi `combined_text`.
* Melakukan **TF-IDF vectorization** terhadap teks tersebut.
* Menggunakan **cosine similarity** untuk menghitung kemiripan antar produk.

#### Mendapatkan Rekomendasi

* Input berupa nama produk dari pengguna.
* Sistem mencari `product_id` dari nama tersebut.
* Mengambil 10 produk paling mirip berdasarkan skor similarity tertinggi.

### **Hasil Uji Coba Sistem Rekomendasi**

**Input Produk:**
`Sounce Fast Phone Charging Cable & Data Sync USB Cable Compatible for iPhone 13, 12,11, X, 8, 7, 6, 5, iPad Air, Pro, Mini & iOS Devices`
**Product ID:** `B096MSW6CT`

**Hasil Rekomendasi Produk Serupa:**

| No              | Produk yang Direkomendasikan  | Kategori Utama         | Subkategori | Harga  |
| --------------- | ----------------------------- | ---------------------- | ----------- | ------ |
| 1               | Sounce Fast Phone Charging... | Computers\&Accessories | USBCables   | 999.0  |
| 2               | SWAPKART Fast Charging Cable  | Computers\&Accessories | USBCables   | 499.0  |
| 3               | Syncwire LTG to USB Cable...  | Computers\&Accessories | USBCables   | 1999.0 |
| 4               | Wayona Nylon Braided USB...   | Computers\&Accessories | USBCables   | 1099.0 |
| 5               | FLiX (Beetel USB to Type C... | Computers\&Accessories | USBCables   | 299.0  |
| *(dan lainnya)* |                               |                        |             |        |


### **Analisis dan Observasi**

* Semua produk yang direkomendasikan berasal dari **kategori dan subkategori yang sama**, yaitu kabel USB dan aksesori komputer.
* Produk memiliki deskripsi dan kata kunci serupa, seperti "Fast Charging", "USB Cable", dan kompatibilitas dengan berbagai seri iPhone/iPad.
* Hal ini menunjukkan bahwa sistem mampu **menangkap kesamaan konten secara akurat**.

### **Kesimpulan CBF**

* Model berhasil memberikan rekomendasi yang **relevan dan konsisten** terhadap produk input.
* CBF cocok digunakan saat informasi produk lengkap tersedia, namun memiliki keterbatasan pada produk baru tanpa ulasan (cold-start).
* Sistem ini dapat ditingkatkan dengan menambahkan bobot terhadap ulasan atau rating dalam perhitungan.

---------------------------------------------


## **Sistem Rekomendasi dengan Collaborative Filtering**

### **Pendekatan Collaborative Filtering**

Collaborative Filtering (CF) adalah pendekatan rekomendasi yang memanfaatkan **interaksi antara pengguna dan item** (produk), dalam hal ini melalui data rating yang diberikan pengguna. Model ini tidak memerlukan informasi detail tentang produk, melainkan mengandalkan **pola perilaku pengguna** untuk memprediksi produk yang disukai.

---

### **Tahapan Implementasi**

#### Seleksi Fitur

Memilih fitur utama untuk CF, yakni:

* `user_id` (ID pengguna)
* `product_id` (ID produk)
* `rating` (nilai interaksi pengguna terhadap produk)

#### Label Encoding

* Mengubah `user_id` dan `product_id` ke dalam bentuk numerik untuk kebutuhan embedding layer.

#### Feature Mapping

* Mapping ulang ID pengguna dan produk agar bisa digunakan dalam model rekomendasi berbasis neural network.

#### Model Training

* Model dibangun menggunakan pendekatan pembelajaran mendalam (deep learning) dengan teknik matrix factorization berbasis embedding layer untuk `user` dan `item`.
* Proses training dilakukan untuk mempelajari vektor representasi dari pengguna dan produk.


### **Hasil Rekomendasi**

**Rekomendasi produk untuk pengguna**
Menampilkan user ID dan daftar produk dengan rating tinggi berdasarkan interaksi historis:

```text
Users: AHDFR3PDKEBV72HXRL3RJJLS3YYA, AHYUZ2BLKNN6UJLFYWCXCEFZTOVQ, ...
Produk dengan rating tinggi:
- TP-Link AC600 USB Adapter → rating: 4.4
- TP-LINK AC1300 Archer T3U Plus → rating: 4.4
```

**Top 10 Produk yang Direkomendasikan**:

| Produk                              | Subkategori       | Rating |
| ----------------------------------- | ----------------- | ------ |
| LG 43” 4K UHD Smart TV              | SmartTelevisions  | 4.3    |
| MI 55” 5X Series 4K Smart TV        | SmartTelevisions  | 4.3    |
| MI 10000mAh Power Bank Pocket Pro   | PowerBanks        | 4.3    |
| Redmi Note 11 Smartphone            | Smartphones       | 4.1    |
| Zebronics Bluetooth Speaker         | BluetoothSpeakers | 3.9    |
| JBL Infinity Fuze Pint Mini Speaker | OutdoorSpeakers   | 4.1    |
| Fire-Boltt Ring Pro Smartwatch      | SmartWatches      | 4.0    |
| HP Deskjet 2723 AIO Printer         | Printers          | 3.6    |
| AGARO Royal Electric Kettle         | ElectricKettles   | 4.3    |
| IKEA Milk Frother                   | MilkFrothers      | 3.6    |


### **Analisis dan Observasi**

* Model berhasil memberikan rekomendasi berdasarkan **pola preferensi pengguna**, tanpa melihat isi/konten produk.
* Produk-produk yang direkomendasikan menunjukkan kecenderungan pengguna terhadap **elektronik rumah tangga dan gadget**.
* Terdapat variasi kategori dan subkategori, menunjukkan kemampuan model menangkap **kemiripan perilaku antar pengguna**.


### **Kesimpulan Collaborative Filtering**

* CF efektif dalam memberikan rekomendasi personalisasi berbasis histori pengguna.
* Tidak bergantung pada deskripsi produk, tapi perlu data interaksi yang cukup (rating).
* Rentan terhadap masalah **cold start** (produk/akun baru tanpa riwayat interaksi).

---------------------------------------------

## **Sistem Rekomendasi dengan Hybrid Filtering**

### **Pendekatan Hybrid Filtering**

**Hybrid Filtering** merupakan gabungan dari dua pendekatan utama dalam sistem rekomendasi, yaitu:

* **Content-Based Filtering (CBF)**: Menggunakan kemiripan konten dari produk seperti nama, deskripsi, dan kategori.
* **Collaborative Filtering (CF)**: Berdasarkan perilaku pengguna seperti rating yang diberikan terhadap produk tertentu.

Dengan mengombinasikan kedua pendekatan ini, sistem dapat memaksimalkan akurasi dan relevansi rekomendasi—menyelesaikan kekurangan dari masing-masing pendekatan (misalnya: *cold-start problem* pada CF atau kurangnya kontekstualisasi pada CBF).


### **Implementasi Hybrid Filtering**

#### Fungsi Hybrid Recommendation

Fungsi utama yang digunakan adalah `hybrid_recommendation(product_id, content_sim_matrix, products, top_n=10)` dengan alur sebagai berikut:

1. **Content-Based Filtering**
   Menghitung produk yang mirip dengan `product_id` berdasarkan *cosine similarity* pada vektor fitur (hasil TF-IDF dari teks gabungan produk).

2. **Collaborative Filtering**
   Mengambil rekomendasi dari sistem CF berdasarkan produk yang memiliki rating tinggi dari pengguna dengan pola yang serupa.

3. **Penggabungan**
   Indeks hasil dari CBF dan CF digabungkan, duplikasi dihapus, dan daftar akhir produk ditampilkan sebagai rekomendasi hybrid.


### **Hasil Rekomendasi Hybrid**

**Contoh Produk yang Dicari:**

> "Wayona Nylon Braided USB to Lightning Fast Charging and Data Sync Cable Compatible for iPhone 13, 12,11, X, 8, 7, 6, 5, iPad Air, Pro, Mini (3 FT Pack of 1, Grey)"

🔽 **Rekomendasi Hybrid Top 10:**

| Produk ID  | Nama Produk                                               | Kategori         | Sub-Kategori     | Rating |
| ---------- | --------------------------------------------------------- | ---------------- | ---------------- | ------ |
| B0B3XY5YT4 | LG 43” 4K UHD Smart LED TV 43UQ7500PSF                    | SmartTelevisions | SmartTelevisions | 4.3    |
| B07JPJJZ2H | Wayona Nylon Braided Lightning USB Data Sync Cable (Grey) | USBCables        | USBCables        | 4.2    |
| B0187F2IOK | Bajaj HM-01 Powerful 250W Hand Mixer                      | HandMixers       | HandMixers       | 4.4    |
| B07JW1Y6XV | Wayona Nylon Braided 3A Lightning to USB A Cable (Black)  | USBCables        | USBCables        | 4.2    |
| B078G6ZF5Z | Oraimo 18W Dual Output Super Fast Charger                 | WallChargers     | WallChargers     | 4.0    |
| B09MKG4ZCM | Xiaomi Mi 4A Dual Band Wi-Fi Router                       | Routers          | Routers          | 4.0    |
| B08DPLCM6T | LG 32” HD Ready Smart LED TV                              | SmartTelevisions | SmartTelevisions | 4.3    |
| B0BF57RN3K | Fire-Boltt Ninja Call Pro Plus Smartwatch                 | SmartWatches     | SmartWatches     | 4.2    |
| B0B2DJDCPX | SWAPKART Fast Charging Cable for iOS Devices (White)      | USBCables        | USBCables        | 3.9    |
| B07LGT55SJ | Wayona USB Nylon Braided Charging Cable (Red, Black)      | USBCables        | USBCables        | 4.2    |

### **Analisis dan Observasi**

* Produk yang direkomendasikan memiliki **kemiripan konten** (kategori, deskripsi) dan juga **rating yang mirip** dengan produk yang dicari.
* Kategori yang sering muncul: **USBCables**, **SmartTelevisions**, **SmartWatches** — menunjukkan sistem hybrid memperhatikan konteks dan preferensi pengguna serupa.
* Meningkatkan cakupan rekomendasi dibanding hanya menggunakan salah satu metode saja.

### **Kesimpulan Hybrid Filtering**

* Sistem hybrid memberikan **rekomendasi yang lebih akurat dan relevan**, karena memanfaatkan keunggulan dari content-based dan collaborative filtering sekaligus.
* Dapat mengatasi **masalah cold-start** (produk baru/tidak punya rating) dan tetap mempertahankan konteks isi produk.
* Cocok digunakan untuk platform e-commerce seperti Amazon yang memiliki **data besar dan beragam interaksi pengguna**.


---------------------------------------------

## **Kesimpulan**

1. **Metode Content-Based Filtering (CBF):**

   * Mampu memberikan rekomendasi berdasarkan kemiripan konten produk seperti nama, kategori, dan deskripsi produk.
   * Tidak membutuhkan data interaksi antar pengguna, sehingga efektif untuk mengatasi masalah *cold-start* pada produk baru.
   * Kelemahannya adalah cenderung menghasilkan rekomendasi yang homogen dan kurang mempertimbangkan preferensi dari pengguna lain.

2. **Metode Collaborative Filtering (CF):**

   * Mengandalkan pola perilaku pengguna seperti rating dan ulasan untuk memberikan rekomendasi yang lebih personal.
   * Cocok digunakan ketika data interaksi pengguna cukup banyak dan beragam.
   * Memiliki kelemahan pada kasus *cold-start*, khususnya ketika terdapat pengguna atau produk baru yang belum memiliki cukup data interaksi.

3. **Metode Hybrid Filtering:**

   * Menggabungkan pendekatan CBF dan CF untuk menghasilkan sistem rekomendasi yang lebih komprehensif dan akurat.
   * Mampu memanfaatkan kekuatan analisis konten dan perilaku pengguna secara bersamaan.
   * Memberikan hasil rekomendasi yang lebih relevan, bervariasi, dan bersifat personal, serta mampu mengatasi kekurangan dari kedua metode individu.

4. **Perbandingan dan Hasil Evaluasi:**

   * Content-Based Filtering unggul dalam mengidentifikasi produk dengan fitur yang serupa, namun kurang adaptif terhadap selera pengguna lain.
   * Collaborative Filtering unggul dalam mengenali preferensi pengguna melalui data interaksi, tetapi kurang efektif untuk produk baru.
   * Hybrid Filtering menjadi metode paling optimal karena mampu mengatasi keterbatasan kedua metode lainnya dan menghasilkan rekomendasi yang lebih baik secara keseluruhan.

5. **Kesimpulan Umum:**

   * Sistem rekomendasi berbasis Hybrid Filtering direkomendasikan sebagai pendekatan terbaik untuk platform e-commerce karena mampu memberikan rekomendasi yang lebih personal, relevan, dan robust dalam berbagai kondisi data.
