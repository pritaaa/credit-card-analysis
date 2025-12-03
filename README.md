# credit-card-analysis
Project analisis &amp; machine learning untuk memprediksi kelayakan pengajuan kartu kredit. Project ini dibuat sebagai tugas mata kuliah Data Mining – Tahun 2024.  Dataset digunakan untuk tujuan akademik dan tidak disertakan dalam repository ini karena alasan privasi serta hak cipta.


📌 README – Credit Card Approval Prediction

Machine Learning Classification | Data Cleaning | EDA | Feature Engineering | SMOTE | PCA | Modeling

Project ini bertujuan untuk memprediksi kelayakan kartu kredit nasabah berdasarkan data demografis, finansial, dan status pekerjaan. Model dibangun melalui proses penuh mulai dari pembersihan data hingga evaluasi model.

🧩 1. Deskripsi Dataset

Dataset memiliki 9709 baris dan 20 kolom, berisi:

Demografi: Gender, Age, Family_status

Finansial: Total_income, Years_employed

Kepemilikan: Own_car, Own_property

Komunikasi: Phone, Email

Target: Target (1 = Approved, 0 = Rejected)

🧹 2. Data Cleaning

✔ Drop kolom ID (nilai unik, tidak informatif)
✔ Penggabungan kolom:

Own_car + Own_property → Property

Work_phone + Phone → Num_phone

✔ Drop kolom Num_children (redundant dengan Num_family)
✔ Drop kolom Occupation_type (nilai unik terlalu banyak → high cardinality)

🔍 3. Exploratory Data Analysis (EDA)

Analisis dilakukan terhadap:

Distribusi numerik (histogram)

Correlation matrix & heatmap

Deteksi outlier pada:
Num_family, Total_income, Years_employed, Age, Account_length

✂️ 4. Handling Outliers

Menggunakan Winsorizing (IQR) pada:

Num_family

Total_income

Years_employed

Outlier diganti ke batas atas & bawah sesuai IQR.

🔠 5. Encoding

Menggunakan Ordinal Encoding untuk kolom kategorikal:

Income_type

Education_type

Family_status

Housing_type

📏 6. Scaling

Dua metode scaling digunakan:

✅ Robust Scaler (untuk kolom yang sensitif outlier)

Num_family

Total_income

Years_employed

✅ Standard Scaler (untuk kolom yang lebih stabil)

Age

Account_length

⚖️ 7. Handling Imbalanced Data

Target tidak seimbang → digunakan SMOTE pada data train.

Menyeimbangkan antara kelas 0 dan 1

Mencegah model bias pada mayoritas

🧠 8. PCA (Dimensionality Reduction)

PCA diterapkan untuk:

Mengurangi noise

Mempercepat training

Mengurangi multicollinearity

Komponen PCA digunakan sebagai fitur tambahan / pengganti (tergantung hasil varian)

🏗️ 9. Modeling

Model yang digunakan:

1️⃣ Logistic Regression

Baseline model

Interpretasi mudah

2️⃣ Random Forest

Model utama

Menangani nonlinear

Tahan outlier

Bisa melihat feature importance

3️⃣ KNN (opsional)

Pembanding

Performa tergantung scaling

📊 10. Evaluasi Model

Metrik evaluasi:

Accuracy

Precision

Recall

F1-score

Confusion Matrix

Model terbaik dipilih berdasarkan F1-score (karena data imbalanced).

📈 11. Dashboard (Google Data Studio / Looker Studio)
❓ Dashboard menjawab pertanyaan:

Berapa persentase pelanggan yang disetujui kartu kredit?

Customer persona seperti apa yang paling sering disetujui?

Income vs age vs approval rate

Status keluarga dan rumah → pengaruh ke approval

Jenis income mana yang paling berpengaruh?

Total income distribution

Years employed vs approval

📦 Data mana yang dipakai untuk dashboard?

👉 Gunakan data SEBELUM SMOTE

Alasannya:

SMOTE membuat data sintetis → tidak representatif untuk dashboard

Dashboard = insight bisnis → harus real data

Modeling = boleh pakai SMOTE, tapi visualisasi = data asli
