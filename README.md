# Final-Project-Kelompok-5-J.A.R.V.I.S

## HR Analytics: Job Change of Data Scientists

Dataset: https://www.kaggle.com/datasets/arashnic/hr-analytics-job-change-of-data-scientists

### Konteks dan Konten
Sebuah perusahaan yang bergerak di bidang Big Data dan Data Science ingin merekrut ilmuwan data di antara orang-orang yang berhasil lulus beberapa kursus yang diadakan oleh perusahaan. Banyak orang mendaftar untuk pelatihan mereka. Perusahaan ingin mengetahui kandidat mana yang benar-benar ingin bekerja untuk perusahaan setelah pelatihan atau mencari pekerjaan baru karena membantu **mengurangi biaya dan waktu serta kualitas pelatihan atau perencanaan kursus dan kategorisasi kandidat.** Informasi terkait demografi, pendidikan, pengalaman ada di tangan dari pendaftaran dan pendaftaran kandidat.

Dataset ini dirancang untuk memahami faktor-faktor yang menyebabkan seseorang meninggalkan pekerjaan saat ini untuk penelitian SDM juga. Dengan model yang menggunakan kredensial, demografi, data pengalaman saat ini, Anda akan **memprediksi kemungkinan seorang kandidat untuk mencari pekerjaan baru atau akan bekerja untuk perusahaan, serta menginterpretasikan faktor-faktor yang memengaruhi keputusan karyawan.**

### Inspirasi
* Memprediksi probabilitas seorang kandidat akan bekerja untuk perusahaan
* Menafsirkan model sedemikian rupa sehingga menggambarkan fitur mana yang memengaruhi keputusan kandidat

### Daftar Isi
1. STAGE 1 EDA, INSIGHTS, AND VISUALIZATION
    * Data Exploration
    * Business-Insight
2. STAGE 2 DATA PREPROCESSING
    * Data Cleansing
    * Feature Enginering
3. STAGE 3 MACHINE LEARNING MODELLING AND EVALUATION
    * Modelling
    * Feature Importance

### STAGE 1 EDA, INSIGHTS, AND VISUALIZATION
#### A. Data Exploration
Hasil Pengamatan:
1. Data ini terdiri dari 19158 baris
2. Sebagian besarnya adalah kategorikal
3. Presentase missing value terbesar yaitu company_type, company_size, gender, dan major_discipline
4. Tampak beberapa kolom masih memiliki null/missing values (Non-Null Count < jumlah baris
5. Sepertinya terdapat kolom yang bisa ditindak lanjut : experience, company_size, dan last_new_job
6. Data numerik tidak terdapat missing values

#### B. Business-Insight
Setelah dilakukan EDA, didapatkan beberapa bussiness insight :
1. City Development Index :
    * Kandidat dengan CDI rendah (0,66) cenderung memiliki keinginan untuk mencari pekerjaan baru
    * Kandidat dengan CDI tinggi (0.9) cenderung sangat tidak tertarik mencari pekerjaan baru
2. Training Hours :
    * Kandidat dengan training hours kurang lebih 20 jam memiliki kecenderungan untuk mencari pekerjaan baru
    * Dapat dilihat jumlah waktu course yang diikuti kandidat adalah sekitar 46-48 jam
    * Semakin banyak jumlah training hours maka semakin sedikit kecenderungan untuk mencari pekerjaan baru
3. Gender :
    * 88.9% kandidat laki-laki cenderung mencari pekerjaan baru
    * Hanya 9.62% kandidat perempuan yang cenderung akan mencari pekerjaan baru
4. Company Type :
    * Kandidat dari Company Type Pvt Ltd paling banyak ingin mencari pekerjaan baru, yaitu sebesar 74.17%
5. Education Level :
    * Kandidat dengan education level graduate paling banyak mencari pekerjaan baru yaitu sebesar 69.44%
6. Major Discipline :
    * Kandidat dengan Major discipline STEM (Science Technology Engineering Math) paling banyak mencari pekerjaan baru yaitu sebesar 89.66%
7. Relevant Experience :
    * 61.98% kandidat dengan relevant experience cenderung akan mencari pekerjaan baru
    * 38.02% kandidat dengan non-relevant experience cenderung akan mencari pekerjaan baru
8. Experience - kandidat yang cenderung akan mencari pekerjaan baru adalah kandidat dengan total experience:
    * Di atas 20 tahun experience (10.58%)
    * 3 tahun experience(9.61%)
    * 4 tahun experience(10.05%)
9. Last New Job :
    * Kandidat yang memiliki perbedaan 1 tahun antara pekerjaan lama dan pekerjaannya sekarang cenderung akan mencari pekerjaan baru (45.97%)

### STAGE 2 DATA PREPROCESSING
#### A. Data Cleansing
1. Handle Missing Values: mengisi kolom kosong menggunakan mice iterative imputer
2. Handle Duplicated Data: menghapus 49 row yang duplicate
3. Handle Outlier: 
    * Outlier Detection Technique: menggunakan 3 teknik yaitu: Visualizing the Data, Z Score, dan IQR Method
    * Dealing with Outliers: menggunakan Imputation
4. Feature Transformation: 
    * Log Transformation: feature training_hours memiliki distribusi right-skewed, perlu diubah ke distribusi normal
    * Standarisasi dan Normalisasi: feature training_hours, feature city_development_index karena distribusi datanya sudah mendekati normal
5. Feature Encoding: feature kategorikal yang memiliki urutan dan feature yang memiliki dua unique value diubah menjadi numerik dengan pendekatan Label Encoder. Sedangkan feature kategorikal lainnya diubah menggunakan teknik One Hot Encoding
6. Handle Class Imbalance: menggunakan teknik SMOTE dan SVM SMOTE

#### B. Feature Enginering
1. Feature Selection: dari hasil heatmap correlation, maka disimpulkan bahwa feature yang akan dihapus adalah enrollee_id karena feature ini merupakan unique keys, sehingga kita tidak memerlukannya dalam proses model machine learning
2. Feature Extraction: kita dapat melakukan feature extraction pada kolom yang cardinal valuenya tinggi yaitu experience dan company size dengan melakukan pengelompokan yang lebih sederhana
3. Additional Feature
    * Backgroud kandidat: Age, Marital status, Number of dependences, Previous Salary, Kenaikan gaji, Rata-rata jam kerja, GPA
    * Training Score: Training satisfaction, Training absent, Last training evaluation

### STAGE 3 MACHINE LEARNING MODELLING AND EVALUATION
#### A. Modelling
##### Base Model
Setelah dilakukan Base Model, didapatkan hasil:
1.	LogisticRegression : 0.728807
2.	LinearSVM : 0.730900
3.	rbfSVM : 0.766091
4.	KNearestNeighbors : 0.707483
5.	**RandomForestClassifier : 0.788462**
6.	DecisionTree : 0.714809
7.	**GradientBoostingClassifier : 0.795133**
8.	GaussianNB : 0.720304

##### Model Hyperparameter Tuning
Ada dua model yang di hyperparameter tuning, yaitu: Tuning Gradient Boosting Classifier dan Tuning Random Forest Classifier
Setelah dilakukan Model Hyperparameter Tuning, didapatkan hasil:
1. RandomForest : 0.786238
2. RandomForet_ht : 0.786499
3. **GradientBoosting : 0.795133**
4. GradientBoosting_ht : 0.782444

#### B. Feature Importance
Berdasarkan grafik, akan dilakukan feature selection dengan mengurangi feature training_hours_norm, training_hours_std, dan major_discipline_No Major. Lalu akan dilakukan modeling dari awal kembali untuk mengecek hasil dari Gradient Boosting dan feature selection. **Dari hasil remodelling, didapatkan accuracy final sebesar 0.796572475.** Hasil ini meningkat dari hasil Gradient Boosting sebelumnya yaitu sebesar 0.795133. (meningkat 0.14%)
