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
    * K-Nearest Neighbor (KNN) adalah algoritma sederhana yang mengklasifikasikan data atau kasus baru berdasarkan ukuran kesamaan. Hal ini sebagian besar digunakan untuk mengklasifikasikan titik data berdasarkan tetangga terdekatnya sebagai acuan.[[4](https://towardsdatascience.com/a-simple-introduction-to-k-nearest-neighbors-algorithm-b3519ed98e)]
    * Random Forest adalah algoritma machine learning yang kuat yang dapat digunakan untuk berbagai tugas termasuk regresi dan klasifikasi. Ini adalah metode ensemble, yang berarti bahwa model random forest terdiri dari banyak decision tree kecil, yang disebut estimator, yang masing-masing menghasilkan prediksi mereka sendiri. Random forest menggabungkan prediksi estimator untuk menghasilkan prediksi yang lebih akurat .[[5](https://deepai.org/machine-learning-glossary-and-terms/random-forest)]
    * Support Vector Machine (SVM) adalah algoritma yang digunakan untuk menemukan hyperplane dalam ruang N-dimensi (N - jumlah fitur) yang secara jelas mengklasifikasikan titik data. SVM dapat digunakan untuk menyelesaikan permasalahan klasifikasi, regresi, dan pendeteksian outlier.[[6](https://towardsdatascience.com/support-vector-machine-introduction-to-machine-learning-algorithms-934a444fca47)]
    * Naive Bayes adalah model machine learning probabilistik yang digunakan untuk tugas klasifikasi. Inti dari classifier ini didasarkan pada teorema Bayes.[[7](https://towardsdatascience.com/naive-bayes-classifier-81d512f50a7c)]
    * Extra trees classifier adalah sejumlah besar pohon keputusan yang belum dipangkas dari kumpulan data pelatihan. Prediksi dibuat dengan merata-ratakan prediksi pohon keputusan dalam kasus regresi atau menggunakan suara terbanyak dalam kasus klasifikasi.[[8](https://machinelearningmastery.com/extra-trees-ensemble-with-python/)]
  
## Data Understanding
Paragraf awal bagian ini menjelaskan informasi mengenai data yang Anda gunakan dalam proyek. Sertakan juga sumber atau tautan untuk mengunduh dataset. Contoh: [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/Restaurant+%26+consumer+data).

Selanjutnya uraikanlah seluruh variabel atau fitur pada data. Sebagai contoh:  

### Variabel-variabel pada Restaurant UCI dataset adalah sebagai berikut:
- accepts : merupakan jenis pembayaran yang diterima pada restoran tertentu.
- cuisine : merupakan jenis masakan yang disajikan pada restoran.
- dst

**Rubrik/Kriteria Tambahan (Opsional)**:
- Melakukan beberapa tahapan yang diperlukan untuk memahami data, contohnya teknik visualisasi data atau exploratory data analysis.

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

