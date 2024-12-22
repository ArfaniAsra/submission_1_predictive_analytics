# Laporan Proyek Machine Learning - Muhammd Arfani Asra

## Domain Proyek

### Latar Belakang

Peningkatan konsumsi energi terbarukan telah menjadi salah satu prioritas utama dalam mitigasi perubahan iklim. Menurut laporan International Renewable Energy Agency (IRENA), pangsa energi terbarukan dalam total konsumsi energi global diproyeksikan mencapai 50% pada tahun 2050 untuk mencapai target nol emisi karbon bersih (*net-zero emissions*) [IRENA, 2023](https://www.irena.org/). Rumah tangga, sebagai konsumen utama energi, memiliki peran signifikan dalam transisi ini.

Namun, tingkat adopsi energi terbarukan bervariasi di antara rumah tangga, bergantung pada berbagai faktor seperti lokasi geografis, tingkat pendapatan, dan jenis energi yang tersedia. Sebuah studi oleh Hajra Amir (2024) [Kaggle](https://www.kaggle.com/datasets/hajraamir21/global-renewable-energy-usage-2020-2024) menunjukkan bahwa preferensi dan penggunaan energi rumah tangga dapat mencerminkan pola yang dapat dikelompokkan.

Mengapa memahami pola ini penting? Dengan segmentasi rumah tangga, penyedia layanan energi dapat:
1. Mengidentifikasi kelompok rumah tangga yang membutuhkan insentif untuk mengadopsi energi terbarukan.
2. Merancang strategi distribusi energi yang lebih efisien dan sesuai kebutuhan.
3. Mendukung kebijakan pemerintah dalam meningkatkan aksesibilitas energi terbarukan.

Proyek ini bertujuan untuk mengelompokkan rumah tangga berdasarkan pola penggunaan energi mereka, menggunakan data yang mencakup berbagai wilayah dan jenis energi terbarukan dari tahun 2020 hingga 2024. Dengan pendekatan ini, diharapkan hasil proyek dapat memberikan wawasan strategis untuk meningkatkan efisiensi energi secara global.

---

## Business Understanding

### Problem Statements
1. Bagaimana pola penggunaan energi rumah tangga dapat dikelompokkan berdasarkan sumber energi terbarukan?
2. Apakah terdapat perbedaan signifikan dalam pola konsumsi energi rumah tangga di berbagai wilayah geografis?
3. Faktor apa saja yang membedakan rumah tangga dalam segmen-segmen yang dihasilkan?

### Goals
1. Mengidentifikasi kelompok-kelompok rumah tangga dengan pola penggunaan energi yang serupa.
2. Memahami karakteristik utama yang membedakan setiap kelompok rumah tangga berdasarkan faktor seperti sumber energi, lokasi, dan tingkat pendapatan.
3. Memberikan wawasan yang dapat digunakan penyedia layanan energi untuk meningkatkan efisiensi distribusi energi terbarukan.

### Solution Statement

Untuk mencapai tujuan proyek, dilakukan pendekatan berikut:

1. **Exploratory Data Analysis (EDA)**:
   - Mengeksplorasi distribusi konsumsi energi bulanan, ukuran rumah tangga, tingkat pendapatan, dan penggunaan energi berdasarkan sumber energi.
   - Visualisasi data dengan teknik seperti histogram, boxplot, atau scatter plot untuk memahami hubungan antar fitur.

2. **Clustering dengan Algoritma Machine Learning**:
   - Menerapkan algoritma **KMeans** untuk melakukan segmentasi rumah tangga berdasarkan pola penggunaan energi.
   - Menentukan jumlah klaster optimal menggunakan **Elbow Method** dan **Silhouette Score**.
   - Membandingkan hasil dengan algoritma clustering lain seperti **Hierarchical Clustering** untuk validasi lebih lanjut.

3. **Analisis dan Visualisasi Klaster**:
   - Menginterpretasikan hasil klaster dengan menganalisis distribusi fitur dalam setiap klaster.
   - Menggunakan PCA (Principal Component Analysis) untuk visualisasi klaster dalam ruang berdimensi rendah.

Solusi yang diterapkan dievaluasi menggunakan metrik seperti **Silhouette Score** dan **Davies-Bouldin Index** untuk menilai kualitas klaster yang dihasilkan.

---

## Data Understanding

### Karakteristik Dataset
Dataset berisi 1000 entri dengan 12 kolom yang mencakup berbagai informasi tentang rumah tangga dan pola konsumsi energi mereka. Berikut adalah rincian setiap kolom:

1. **Household_ID**: ID unik untuk setiap rumah tangga.
2. **Region**: Wilayah geografis rumah tangga (misalnya, North America, Europe, Africa).
3. **Country**: Negara tempat rumah tangga berada.
4. **Energy_Source**: Jenis energi terbarukan yang digunakan (Hydro, Wind, Biomass, Geothermal, Solar).
5. **Monthly_Usage_kWh**: Jumlah konsumsi energi bulanan dalam kWh.
6. **Year**: Tahun pencatatan data.
7. **Household_Size**: Jumlah anggota dalam rumah tangga.
8. **Income_Level**: Tingkat pendapatan rumah tangga (Low, Middle, High).
9. **Urban_Rural**: Lokasi rumah tangga, apakah di area perkotaan (Urban) atau pedesaan (Rural).
10. **Adoption_Year**: Tahun adopsi energi terbarukan oleh rumah tangga.
11. **Subsidy_Received**: Indikator apakah rumah tangga menerima subsidi untuk energi terbarukan (Yes/No).
12. **Cost_Savings_USD**: Jumlah penghematan biaya dalam USD karena penggunaan energi terbarukan.

### Statistik Deskriptif
- **Monthly_Usage_kWh**:
  - Rata-rata: 767.3 kWh
  - Minimum: 50.74 kWh
  - Maksimum: 1497.34 kWh
- **Household_Size**:
  - Rata-rata: 4.48 anggota
  - Minimum: 1 anggota
  - Maksimum: 8 anggota
- **Cost_Savings_USD**:
  - Rata-rata: $248.39
  - Minimum: $10.42
  - Maksimum: $499.83

### Distribusi Data
1. **Energy_Source**: Lima kategori utama dengan distribusi sebagai berikut:
   - Hydro: 227 rumah tangga
   - Wind: 203 rumah tangga
   - Biomass: 189 rumah tangga
   - Geothermal: 195 rumah tangga
   - Solar: 186 rumah tangga

2. **Region**: Enam wilayah utama dengan distribusi sebagai berikut:
   - North America: 210 rumah tangga
   - Europe: 173 rumah tangga
   - Asia: 165 rumah tangga
   - Africa: 157 rumah tangga
   - South America: 150 rumah tangga
   - Australia: 145 rumah tangga

3. **Income_Level**:
   - Low: 308 rumah tangga
   - Middle: 358 rumah tangga
   - High: 334 rumah tangga

### Catatan Penting
- Tidak ada nilai null pada dataset, sehingga tidak diperlukan penanganan nilai yang hilang.
- Data kategorikal (seperti Income_Level, Energy_Source) akan diencoding untuk kebutuhan modeling.
- Data numerik (seperti Monthly_Usage_kWh, Cost_Savings_USD) akan dinormalisasi untuk memastikan performa algoritma clustering optimal.

Dataset ini memiliki variasi yang cukup untuk menghasilkan segmentasi yang informatif dan bermanfaat bagi analisis lebih lanjut.

---

## Data Preparation

### Langkah-Langkah Data Preparation
1. **Encoding Data Kategorikal**:
   - Menggunakan Label Encoding untuk fitur seperti Income_Level, Urban_Rural, dan Subsidy_Received.
   - Menggunakan One-Hot Encoding untuk fitur seperti Region dan Energy_Source.

2. **Normalisasi Data Numerik**:
   - Normalisasi diterapkan pada fitur numerik seperti Monthly_Usage_kWh, Household_Size, dan Cost_Savings_USD menggunakan StandardScaler.

3. **Feature Engineering**:
   - Menambahkan fitur baru seperti Cost_Savings_Per_kWh (rasio penghematan biaya terhadap konsumsi energi bulanan) dan Energy_Usage_Per_Member (konsumsi energi per anggota rumah tangga).

### Alasan Data Preparation
- Encoding diperlukan untuk mengubah data kategorikal menjadi format numerik yang dapat dipahami oleh algoritma machine learning.
- Normalisasi memastikan semua fitur memiliki skala yang seragam, penting untuk algoritma clustering yang sensitif terhadap skala data.
- Feature Engineering membantu menambahkan dimensi baru yang dapat memperkuat hasil klasterisasi.

---

## Modeling

### Algoritma yang Digunakan
1. **KMeans Clustering**:
   - Menentukan jumlah klaster optimal menggunakan Elbow Method dan Silhouette Score.
   - Hasil menunjukkan bahwa K=2 adalah jumlah klaster optimal.

2. **Hierarchical Clustering**:
   - Menggunakan metode Ward untuk membentuk klaster secara hierarkis.
   - Memberikan hasil yang konsisten dengan KMeans, dengan evaluasi tambahan melalui dendrogram.

### Evaluasi Model
- **Silhouette Score**:
  - KMeans: 0.857
  - Hierarchical Clustering: 0.857
- **Davies-Bouldin Index**:
  - KMeans: 0.101
  - Hierarchical Clustering: 0.101

Kedua algoritma menunjukkan kualitas klaster yang baik, tetapi Hierarchical Clustering memberikan interpretasi tambahan melalui visualisasi dendrogram.

---

## Evaluation

### Hasil Evaluasi
1. **Kualitas Klaster**:
   - Klaster memiliki separasi dan kohesi yang baik, didukung oleh metrik evaluasi seperti Silhouette Score yang tinggi dan Davies-Bouldin Index yang rendah.

2. **Distribusi Fitur per Klaster**:
   - Klaster 0: Rumah tangga dengan konsumsi energi rendah hingga sedang dan efisiensi biaya lebih rendah.
   - Klaster 1: Rumah tangga dengan konsumsi energi tinggi tetapi efisiensi biaya yang sangat baik.

3. **Visualisasi**:
   - PCA menunjukkan separasi klaster yang jelas dalam ruang berdimensi rendah.
   - Dendrogram memberikan interpretasi tambahan untuk Hierarchical Clustering.

### Interpretasi Metrik
- **Silhouette Score** mengukur kohesi internal dan separasi antar klaster. Nilai mendekati 1 menunjukkan klaster yang sangat baik.
- **Davies-Bouldin Index** mengukur jarak antar klaster. Nilai mendekati 0 menunjukkan separasi antar klaster yang signifikan.

---

## Kesimpulan

### Temuan Utama
1. **Pola Konsumsi Energi**:
   - Rumah tangga berhasil dikelompokkan ke dalam dua klaster utama:
     - **Klaster 0**: Didominasi oleh rumah tangga dengan konsumsi energi rendah hingga sedang dan efisiensi biaya yang lebih rendah.
     - **Klaster 1**: Rumah tangga dengan konsumsi energi tinggi tetapi memiliki efisiensi biaya yang jauh lebih baik.

2. **Distribusi Geografis**:
   - Klaster 0 lebih sering ditemukan di wilayah dengan infrastruktur energi terbatas.
   - Klaster 1 mendominasi wilayah dengan infrastruktur energi maju, seperti Eropa dan Amerika Utara.

3. **Karakteristik Klaster**:
   - Faktor utama yang membedakan klaster meliputi: tingkat pendapatan (*Income
