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

### Exploratory Data Analysis:

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

![kategorikal](https://github.com/user-attachments/assets/2f6884c6-2b90-4818-9e6b-5a098f90fb86)

#### Analisis Fitur Numerik

Gambar di bawah menunjukkan **heatmap korelasi** antara tiga fitur numerik dalam dataset, yaitu `math score`, `reading score`, dan `writing score`.

![numerik](https://github.com/user-attachments/assets/a1cbc6f8-dd04-43ef-b76d-a019d194df89)

- **Reading score dan writing score** memiliki korelasi yang sangat kuat sebesar **0.95**, yang menunjukkan bahwa siswa yang baik dalam membaca cenderung juga baik dalam menulis.
- **Math score** juga memiliki korelasi positif yang kuat dengan **reading score (0.80)** dan **writing score (0.78)**, meskipun sedikit lebih rendah dibandingkan korelasi antara reading dan writing.

Seluruh fitur numerik menunjukkan hubungan yang cukup kuat satu sama lain, yang mengindikasikan bahwa performa akademik siswa di satu mata pelajaran cenderung sejalan dengan mata pelajaran lainnya. Korelasi ini bisa menjadi pertimbangan dalam proses feature selection atau ketika mengembangkan model prediktif.

## Data Preparation
Pada tahap ini dilakukan beberapa proses persiapan data sebelum digunakan dalam pemodelan. Proses-proses tersebut dilakukan secara berurutan untuk memastikan data dalam kondisi yang optimal. Berikut adalah tahapan-tahapan data preparation yang telah dilakukan:

### Encoding Fitur Kategorikal
```
df_score_enc = df_score.copy()

education_categories = [
    'some high school',
    'high school',
    'associate\'s degree',
    'some college',
    'bachelor\'s degree',
    'master\'s degree'
]

oe = OrdinalEncoder(categories=[education_categories])
df_score_enc['parental level of education'] = oe.fit_transform(df_score_enc[['parental level of education']])

df_score_enc = pd.get_dummies(df_score_enc, columns=[
    'gender',
    'race/ethnicity',
    'lunch',
    'test preparation course'
])
```

**Ordinal Encoding** diterapkan pada kolom `parental level of education` karena memiliki sifat ordinal, di mana tingkat pendidikan dapat diasumsikan memiliki urutan tertentu. Sementara itu, kolom-kolom seperti `gender`, `race/ethnicity`, `lunch`, dan `test preparation course` dikonversi menggunakan **One-Hot Encoding** karena bersifat nominal atau tidak memiliki urutan. Hasil encoding ini memungkinkan seluruh fitur kategorikal diubah ke dalam format numerik yang sesuai untuk proses modeling.

### Transformasi Target Variabel
```
df_score_enc['reading_cat'] = pd.cut(
    df_score_enc['reading score'],
    bins=[0, 60, 80, 100],
    labels=['Low', 'Medium', 'High']
)


le = LabelEncoder()
df_score_enc['reading_cat'] = le.fit_transform(df_score_enc['reading_cat'])

```

Variabel `reading_cat` merupakan hasil kategorisasi dari nilai `reading score` pada dataset. Nilai ini diklasifikasikan ke dalam tiga kategori berdasarkan rentang skor sebagai berikut:
* Low: **Nilai `0 ≤ score ≤ 60`**
* Medium: **Nilai `60 < score ≤ 80`**
* High: **Nilai `80 < score ≤ 100`**

### Split Data (Training dan Testing)
```
X = df_score_enc.drop('reading score', axis=1)
y = df_score_enc['reading_cat']

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42,
)
```

**Data Splitting** bertujuan untuk memisahkan dataset menjadi dua bagian: data latih (80% training set) dan data uji (20% test set).

## Modeling
Pada tahap ini dilakukan proses pemodelan menggunakan beberapa algoritma machine learning untuk menyelesaikan masalah klasifikasi tingkat kemampuan membaca (`reading_cat`). Model-model yang digunakan antara lain:

### 1. **Extreme Gradient Boosting (XGBoost)**

**Deskripsi:**  
XGBoost adalah algoritma boosting yang menggabungkan banyak pohon keputusan secara iteratif untuk memperbaiki kesalahan dari model sebelumnya. XGBoost terkenal karena efisiensinya dan performa yang tinggi, terutama pada dataset yang kompleks dan besar.

**Kelebihan:**
- Performa prediksi yang sangat baik, terutama untuk data tabular.
- Mampu menangani missing value secara otomatis.
- Mendukung paralelisasi sehingga proses training menjadi lebih cepat.
- Memiliki berbagai parameter tuning untuk meningkatkan akurasi.

**Kekurangan:**
- Cenderung kompleks dan memerlukan tuning parameter yang cukup banyak.
- Interpretasi model tidak sesederhana model linear atau decision tree tunggal.

### 2. **Naive Bayes (NB)**

**Deskripsi:**  
Naive Bayes adalah algoritma klasifikasi berbasis probabilistik yang menggunakan Teorema Bayes dengan asumsi independensi antar fitur.

**Kelebihan:**
- Cepat dalam proses training dan prediksi.
- Performa baik pada dataset dengan fitur independen.
- Cocok untuk klasifikasi teks dan data bersifat kategorikal.

**Kekurangan:**
- Asumsi independensi antar fitur jarang terpenuhi dalam praktik.
- Tidak cocok untuk fitur yang sangat berkorelasi.

### 3. **Random Forest (RF)**

**Deskripsi:**  
Random Forest adalah algoritma ensemble yang membentuk banyak pohon keputusan (decision tree) dan menggabungkan hasilnya untuk meningkatkan akurasi dan mengurangi overfitting.

**Kelebihan:**
- Mengurangi risiko overfitting dibandingkan decision tree tunggal.
- Dapat menangani data numerik maupun kategorikal.
- Memberikan estimasi pentingnya fitur (feature importance).

**Kekurangan:**
- Model lebih besar dan lebih lambat dibandingkan decision tree tunggal.
- Interpretasi tidak semudah model yang lebih sederhana.

### 4. **Support Vector Machine (SVM)**

**Deskripsi:**  
SVM bekerja dengan mencari hyperplane terbaik yang memisahkan data antar kelas dengan margin maksimal.

**Kelebihan:**
- Efektif pada dataset berdimensi tinggi.
- Dapat digunakan untuk klasifikasi linear maupun non-linear (dengan kernel trick).
- Robust terhadap outlier jika menggunakan kernel yang tepat.

**Kekurangan:**
- Kurang efisien pada dataset besar (komputasi mahal).
- Memerlukan tuning parameter seperti C dan kernel yang sesuai.
- Kurang interpretatif dibandingkan model berbasis pohon.

## Evaluation
Pada tahap ini dilakukan evaluasi terhadap performa model menggunakan beberapa metrik evaluasi klasifikasi, yaitu **accuracy**, **precision**, **recall**, dan **F1-score**. Pemilihan metrik ini disesuaikan dengan konteks permasalahan klasifikasi dalam proyek ini, yang bertujuan mengklasifikasikan skor membaca siswa ke dalam tiga kategori: Low, Medium, dan High.

### Confusion Matrix

**Confusion Matrix** adalah sebuah tabel yang digunakan untuk mengevaluasi performa model klasifikasi. Tabel ini menunjukkan jumlah prediksi yang benar dan salah yang dilakukan oleh model dibandingkan dengan nilai aktual.

Berikut adalah elemen penting dalam confusion matrix:

- **True Positive (TP):** Model memprediksi positif, dan sebenarnya memang positif.
- **True Negative (TN):** Model memprediksi negatif, dan sebenarnya memang negatif.
- **False Positive (FP):** Model memprediksi positif, tapi sebenarnya negatif. *(Type I Error)*
- **False Negative (FN):** Model memprediksi negatif, tapi sebenarnya positif. *(Type II Error)*

![cm](https://github.com/user-attachments/assets/799a95c9-8427-44af-85e0-85ee53f5d723)

**XGBoost**

| Class  | TP  | TN  | FP | FN |
|:------:|:---:|:---:|:--:|:--:|
| Low    | 39  | 159 |  0 |  0 |
| Medium | 68  | 130 |  0 |  0 |
| High   | 91  | 107 |  0 |  0 |

&nbsp;

**Naive Bayes**

| Class  | TP  | TN  | FP | FN |
|:------:|:---:|:---:|:--:|:--:|
| Low    | 39  | 159 |  0 |  0 |
| Medium | 27  | 114 | 16 | 41 |
| High   | 75  |  66 | 41 | 16 |

&nbsp;

**Random Forest**

| Class  | TP  | TN  | FP | FN |
|:------:|:---:|:---:|:--:|:--:|
| Low    | 39  | 159 |  0 |  0 |
| Medium | 68  | 130 |  0 |  0 |
| High   | 91  | 107 |  0 |  0 |

&nbsp;

**SVM**

| Class  | TP  | TN  | FP | FN |
|:------:|:---:|:---:|:--:|:--:|
| Low    | 39  | 159 |  0 |  0 |
| Medium | 60  | 123 |  3 |  8 |
| High   | 88  |  99 |  8 |  3 |

&nbsp;

Kesimpulan:
- **XGBoost** dan **Random Forest**: performa sempurna.
- **SVM**: performa cukup baik, ada sedikit kesalahan.
- **Naive Bayes**: paling banyak error dalam memprediksi kelas Medium dan High.

_Catatan:_
- _Anda dapat menambahkan gambar, kode, atau tabel ke dalam laporan jika diperlukan. Temukan caranya pada contoh dokumen markdown di situs editor [Dillinger](https://dillinger.io/), [Github Guides: Mastering markdown](https://guides.github.com/features/mastering-markdown/), atau sumber lain di internet. Semangat!_
- Jika terdapat penjelasan yang harus menyertakan code snippet, tuliskan dengan sewajarnya. Tidak perlu menuliskan keseluruhan kode project, cukup bagian yang ingin dijelaskan saja.

