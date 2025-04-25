# Laporan Proyek Machine Learning - Muhammad Azhar Fikri

## Domain Proyek

Proyek ini berfokus pada bidang pendidikan dengan menganalisa kinerja siswa dalam ujian matematika, membaca, dan menulis. 
Data yang digunakan berasal dari dataset **"Students Performance in Exams"** yang tersedia di [Kaggle](https://www.kaggle.com/datasets/spscientist/students-performance-in-exams). 

### Latar Belakang
![pendidikan](https://media.istockphoto.com/id/1260413500/id/foto/anak-anak-belajar-di-luar-ruangan-di-taman.jpg?s=170667a&w=0&k=20&c=sDsnoLgmJst_oBx0y0oXkdsAi3CYjMbHRKtA0c6buIQ=)

Pendidikan merupakan salah satu pilar utama dalam pembangunan sumber daya manusia yang berkualitas. Kinerja siswa dalam ujian sering kali digunakan sebagai indikator utama untuk menilai efektivitas proses pembelajaran dan untuk mengidentifikasi faktor-faktor yang mempengaruhi hasil belajar mereka. Berbagai penelitian telah menunjukkan bahwa faktor-faktor seperti [motivasi belajar, _self-efficacy_, dan latar belakang pendidikan](https://journal.uny.ac.id/index.php/jrpm/article/view/2666) memiliki pengaruh signifikan terhadap prestasi akademik siswa. 

Dengan memahami faktor-faktor yang memengaruhi kinerja siswa, pendidik dan pembuat kebijakan dapat merancang metode yang lebih efektif untuk meningkatkan hasil belajar. Selain itu, wawasan yang didapat dari analisis ini dapat memberikan panduan bagi orang tua untuk mendukung perkembangan akademik anak-anak mereka. [Pendekatan _predictive analysis_ ini diharapkan dapat mengungkap pola dan hubungan yang dapat digunakan untuk meningkatkan kualitas pendidikan](https://arxiv.org/abs/2208.07749) secara menyeluruh.

## Business Understanding
Model ini dikembangkan untuk menganalisis faktor-faktor yang mempengaruhi kinerja siswa dalam ujian matematika, membaca, dan menulis. Dengan memanfaatkan data yang ada, model ini bertujuan untuk memprediksi hasil ujian siswa berdasarkan berbagai variabel seperti `jenis kelamin`, `latar belakang pendidikan orang tua`, serta `makanan` dan `persiapan ujian`.

### Problem Statements
Berdasarkan latar belakang di atas, berikut rincian masalah yang dapat diselesaikan pada proyek ini:
- Apakah terdapat perbedaan performa akademik antara siswa laki-laki dan perempuan (Gender) dalam ujian matematika, membaca, dan menulis?
- Apakah latar belakang orang tua berhubungan langsung dengan performa akademik siswa?
- Bagaimana model ini dapat membantu pendidik dan pembuat kebijakan untuk meningkatkan kualitas pendidikan dan mendukung perkembangan akademik siswa secara lebih personal dan efektif?

### Goals
Tujuan dari proyek ini:
- Mengidentifikasi apakah ada kesenjangan gender dan kebutuhan pendidikan yang berbeda dalam capaian akademik.
- Meneliti hubungan antara latar belakang pendidikan orang tua dalam keberhasilan belajar siswa.
- Meningkatkan hasil belajar siswa secara keseluruhan, serta memberikan rekomendasi yang berbasis data untuk kebijakan pendidikan yang lebih efektif.

### Solution statements
- Melakukan analisis data, baik secara _univariate_ maupun _multivariate_, untuk memahami distribusi dan hubungan antar variabel. Visualisasi data digunakan untuk menggali pola dan mendeteksi _outlier_, serta mengidentifikasi korelasi antar fitur. Proses ini membantu dalam memahami karakteristik data yang akan mempengaruhi hasil prediksi.
- Data _cleaning_ dilakukan untuk menangani nilai yang hilang, data yang tidak konsisten, dan _outlier_.
- Berbagai model machine learning dikembangkan dan dievaluasi untuk memilih model terbaik dalam memprediksi hasil ujian siswa. Beberapa algoritma yang digunakan dalam proyek ini antara lain:
    * **_Extreme Gradient Boosting_ (XGB)**: Algoritma gradient boosting yang efisien dan sangat populer. menggunakan pendekatan ensemble untuk meningkatkan akurasi model dan sangat baik dalam menangani data dengan banyak fitur.
    * **_Naive Bayes_ (NB)**: Model probabilistik yang menggunakan teorema Bayes, yang bekerja dengan asumsi independensi antar fitur.
    * **_Random Forest_ (RF)**: Sebuah metode ensemble yang menggunakan banyak pohon keputusan untuk menghasilkan prediksi yang lebih akurat.
    * **_Support Vector Machine_** (SVM): Algoritma yang mencari hyperplane untuk memisahkan kelas data secara optimal.

## Data Understanding
Pada proyek ini, data yang digunakan berasal dari [Kaggle](https://www.kaggle.com/datasets/spscientist/students-performance-in-exams). Dataset ini berisi informasi tentang hasil ujian siswa dalam tiga mata pelajaran, serta beberapa atribut demografis siswa.

Dataset yang digunakan berformat CSV (Comma-Separated Values) dan terdiri dari **1.000 sampel (baris)** dengan **8 fitur (kolom)**.

Berdasarkan eksplorasi awal, terdapat:
- **3 fitur numerik** bertipe `int64`, yaitu: `math score`, `reading score`, dan `writing score`.
- **5 fitur kategorikal** bertipe `object`, yaitu: `gender`, `race/ethnicity`, `parental level of education`, `lunch`, dan `test preparation course`.

Selain itu, dataset ini **tidak memiliki missing value**, sehingga tidak diperlukan proses imputasi atau penanganan data kosong dalam tahap preprocessing awal.

### Deskripsi Variabel:
- `gender` : jenis kelamin siswa, terdiri dari `male` dan `female`.
- `race/ethnicity` : ras atau etnis siswa, dikategorikan dari `group A` hingga `group E`.
- `parental level of education` : tingkat pendidikan tertinggi yang dicapai oleh orang tua siswa.
- `lunch` : jenis makan siang yang diterima siswa, yaitu `standard` atau `free/reduced`.
- `test preparation course` : status keikutsertaan siswa dalam program persiapan ujian, `completed` atau `none`.
- `math score` : nilai ujian matematika dengan rentang skor `0–100`.
- `reading score` : nilai ujian membaca dengan rentang skor `0–100`.
- `writing score` : nilai ujian menulis dengan rentang skor `0–100`.

###**Exploratory Data Analysis**:
#### Analisis Fitur Kategorikal

Berikut adalah nilai unik dan distribusi frekuensi dari masing-masing fitur kategorikal dalam dataset:

##### 1. Gender
Kolom `gender` memiliki 2 kategori:
- **female**: 510 siswa
- **male**: 478 siswa
Distribusi cukup seimbang antara siswa laki-laki dan perempuan, dengan sedikit lebih banyak siswa perempuan.


##### 2. Race/Ethnicity
Kolom `race/ethnicity` terdiri dari 5 kelompok:
- **group C**: 316 siswa
- **group D**: 261 siswa
- **group B**: 184 siswa
- **group E**: 139 siswa
- **group A**: 88 siswa
Kelompok etnis dengan jumlah terbanyak adalah **group C**, sedangkan yang paling sedikit adalah **group A**.


##### 3. Parental Level of Education
Kolom `parental level of education` memiliki 6 kategori:
- **some college**: 222 siswa
- **associate's degree**: 221 siswa
- **high school**: 193 siswa
- **some high school**: 175 siswa
- **bachelor's degree**: 118 siswa
- **master's degree**: 59 siswa
Mayoritas orang tua siswa memiliki latar belakang pendidikan menengah hingga diploma. Hanya sebagian kecil yang mencapai gelar master.

##### 4. Lunch
Kolom `lunch` memiliki 2 jenis:
- **standard**: 643 siswa
- **free/reduced**: 345 siswa
Sebagian besar siswa menerima makan siang standar. Namun, jumlah siswa yang menerima subsidi juga cukup besar.

##### 5. Test Preparation Course
Kolom `test preparation course` terdiri dari:
- **none**: 631 siswa
- **completed**: 357 siswa
Mayoritas siswa tidak mengikuti kursus persiapan ujian, sementara sebagian lainnya telah menyelesaikannya.

## Data Preparation
Pada bagian ini Anda menerapkan dan menyebutkan teknik data preparation yang dilakukan. Teknik yang digunakan pada notebook dan laporan harus berurutan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan proses data preparation yang dilakukan
- Menjelaskan alasan mengapa diperlukan tahapan data preparation tersebut.

## Modeling
Tahapan ini membahas mengenai model machine learning yang digunakan untuk menyelesaikan permasalahan. Anda perlu menjelaskan tahapan dan parameter yang digunakan pada proses pemodelan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan kelebihan dan kekurangan dari setiap algoritma yang digunakan.
- Jika menggunakan satu algoritma pada solution statement, lakukan proses improvement terhadap model dengan hyperparameter tuning. **Jelaskan proses improvement yang dilakukan**.
- Jika menggunakan dua atau lebih algoritma pada solution statement, maka pilih model terbaik sebagai solusi. **Jelaskan mengapa memilih model tersebut sebagai model terbaik**.

## Evaluation
Pada bagian ini anda perlu menyebutkan metrik evaluasi yang digunakan. Lalu anda perlu menjelaskan hasil proyek berdasarkan metrik evaluasi yang digunakan.

Sebagai contoh, Anda memiih kasus klasifikasi dan menggunakan metrik **akurasi, precision, recall, dan F1 score**. Jelaskan mengenai beberapa hal berikut:
- Penjelasan mengenai metrik yang digunakan
- Menjelaskan hasil proyek berdasarkan metrik evaluasi

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.

**---Ini adalah bagian akhir laporan---**

_Catatan:_
- _Anda dapat menambahkan gambar, kode, atau tabel ke dalam laporan jika diperlukan. Temukan caranya pada contoh dokumen markdown di situs editor [Dillinger](https://dillinger.io/), [Github Guides: Mastering markdown](https://guides.github.com/features/mastering-markdown/), atau sumber lain di internet. Semangat!_
- Jika terdapat penjelasan yang harus menyertakan code snippet, tuliskan dengan sewajarnya. Tidak perlu menuliskan keseluruhan kode project, cukup bagian yang ingin dijelaskan saja.

