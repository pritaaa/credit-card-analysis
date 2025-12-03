# credit-card-analysis
Project analisis dan machine learning untuk memprediksi kelayakan pengajuan kartu kredit. Project ini dibuat sebagai tugas mata kuliah Data Mining – Tahun 2024.  Dataset digunakan untuk tujuan akademik dan tidak disertakan dalam repository ini karena alasan privasi serta hak cipta.

Project ini bertujuan untuk memprediksi kelayakan kartu kredit nasabah berdasarkan data demografis, finansial, dan status pekerjaan. Model dibangun melalui proses penuh mulai dari pembersihan data hingga evaluasi model.

## 1. Deskripsi Dataset
Dataset memiliki 9709 baris dan 20 kolom, berisi:
- Demografi: Gender, Age, Family_status
- Finansial: Total_income, Years_employed
- Kepemilikan: Own_car, Own_property
- Komunikasi: Phone, Email
- Target: Target (1 = Approved, 0 = Rejected)

## 2. Data Cleaning
- Drop kolom ID (nilai unik, tidak informatif)
- Penggabungan kolom:
Own_car + Own_property = Property
Work_phone + Phone = Num_phone

- Drop kolom Num_children (redundant dengan Num_family)
- Drop kolom Occupation_type (nilai unik terlalu banyak → high cardinality)

## 3. Exploratory Data Analysis (EDA)
Analisis dilakukan terhadap:
- Distribusi numerik (histogram)
- Correlation matrix & heatmap
- Deteksi outlier pada:
Num_family, Total_income, Years_employed, Age, Account_length

## 4. Handling Outliers
Menggunakan Winsorizing (IQR) pada:
- Num_family
- Total_income
- Years_employed
- Outlier diganti ke batas atas & bawah sesuai IQR.
  
## 5. Encoding
Menggunakan Ordinal Encoding untuk kolom kategorikal:
- Income_type
- Education_type
- Family_status
- Housing_type

## 6. Scaling
Dua metode scaling digunakan:
a. Robust Scaler (untuk kolom yang sensitif outlier)
- Num_family
- Total_income
- Years_employed

b. Standard Scaler (untuk kolom yang lebih stabil)
- Age
- Account_length

## 7. Handling Imbalanced Data
Target tidak seimbang → digunakan SMOTE pada data train.
Menyeimbangkan antara kelas 0 dan 1
Mencegah model bias pada mayoritas

## 8. PCA (Dimensionality Reduction)
PCA diterapkan untuk:
- Mengurangi noise
- Mempercepat training
- Mengurangi multicollinearity
- Komponen PCA digunakan sebagai fitur tambahan / pengganti (tergantung hasil varian)

## 9. Modeling
Model yang digunakan:

a. Logistic Regression
Baseline model
Interpretasi mudah

b. Random Forest
Model utama
Menangani nonlinear
Tahan outlier
Bisa melihat feature importance

c. KNN
Pembanding

## 10. Evaluasi Model
Metrik evaluasi:
- Accuracy
- Precision
- Recall
- F1-score
- Confusion Matrix
- Model terbaik dipilih berdasarkan F1-score (karena data imbalanced).

Berdasarkan hasil evaluasi tiga model klasifikasi (Random Forest, Logistic Regression, dan KNN), model dengan performa terbaik adalah Random Forest dengan akurasi 86.65% dan recall 86.65%. Model ini mampu menangkap pola data dengan lebih baik dibandingkan model lainnya, terutama dalam mendeteksi kelas mayoritas. Random Forest dipilih sebagai model terbaik untuk memprediksi persetujuan kartu kredit karena memberikan kombinasi akurasi dan recall yang paling optimal.

## 11. Insight Bisnis

Berdasarkan seluruh analisis:

Nasabah dengan income lebih tinggi, masa kerja panjang, usia produktif, dan stabilitas kepemilikan aset lebih mungkin disetujui kartu kredit. Faktor finansial (Total_income & Years_employed) menjadi penentu utama.
Institusi dapat memprioritaskan calon nasabah dengan profil stabil ini untuk meningkatkan approval rate dan menurunkan risiko kredit.
