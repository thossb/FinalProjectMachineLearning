# FinalProjectMachineLearning

## 🎯 GOAL (Tujuan)

### Primary Goal:
- Memprediksi harga rumah di Kota Bandung menggunakan machine learning
- Membantu masyarakat menemukan hunian sesuai anggaran di tengah kenaikan harga properti

### Technical Goals:
- Membandingkan performa 5 algoritma ML yang berbeda
- Menguji 3 skenario optimasi untuk setiap model
- Mencari kombinasi terbaik model + preprocessing untuk akurasi tertinggi

---

## 📊 DATASET
- Source: Kaggle - "Daftar Harga Rumah Bandung"
- Size: ±7,600 baris, 8 kolom
- Target: price (harga rumah dalam Rupiah)
- Features: bedroom, bathroom, carport, land_area, building_area, location, certificate, facing

---

## 🔄 WORKFLOW LENGKAP

### 1. Import & Preprocess
python
- Data loading dan basic cleaning
- Handle missing values
- Data type conversion


### 2. Exploratory Data Analysis (EDA)
- Bedroom - Distribusi jumlah kamar tidur
- Bathroom - Distribusi jumlah kamar mandi  
- Carport - Analisis kapasitas parkir
- Land Area - Distribusi luas tanah
- Building Area - Distribusi luas bangunan
- Price - Analisis target variable (distribusi, outlier)

### 3. Encoding & Train-Test Split
- Location Encoding - Transform categorical location ke numerical
- Train-Test Split - Bagi data untuk training dan testing

### 4. Model Training (5 Algoritma)
```
#### A. Linear Regression

├── Base Model (tanpa preprocessing)
├── With Scaler (normalisasi data)
└── With Scaler + Remove Outliers


#### B. Decision Tree Regressor

├── Hyperparameter Tuning (Optuna)
├── With Best Parameters
├── With Scaler
└── With Scaler + Remove Outliers


#### C. Random Forest Regressor ⭐ (Yang sedang kita bahas)

├── Hyperparameter Tuning (Optuna - 50 trials)
├── With Best Parameters  
├── With Scaler
└── With Scaler + Remove Outliers


#### D. XGBoost Regressor (Gradient Boosting)

├── Hyperparameter Tuning
├── With Best Parameters
├── With Scaler
└── With Scaler + Remove Outliers


#### E. k-Nearest Neighbors Regressor

├── Hyperparameter Tuning
├── With Best Parameters
├── With Scaler
└── With Scaler + Remove Outliers
```

---

🧪 3 SKENARIO PENGUJIAN
1. Hyperparameter Tuning
Bandingkan model default vs tuned
Gunakan Optuna untuk optimasi otomatis dengan 50 trials
Cari kombinasi parameter terbaik untuk setiap algoritma

2. Normalisasi
Bandingkan with scaler vs without scaler
Penting untuk algoritma sensitif terhadap skala (KNN, Linear Regression)
Gunakan StandardScaler untuk standardisasi features

3. Remove Outliers
Bandingkan with outliers vs cleaned data
Buang data ekstrem yang dapat mengganggu model
Kombinasi dengan scaler untuk preprocessing lengkap

---
## 📊 HASIL

### 🥇 RANKING BERDASARKAN TEST SET R²

| Rank | Model | Skenario | Test R² | Test RMSE (Miliar) | Test MAE (Miliar) |
|------|-------|----------|---------|-------------------|-------------------|
| 🏆 1 | **XGBoost** | **With Best Params** | **0.7027** | **2.33** | **1.02** |
| 🥈 2 | Random Forest | With Best Params | 0.6561 | 2.51 | 1.00 |
| 🥉 3 | Random Forest | With Scaler + Outliers | 0.6604 | 2.49 | 1.04 |
| 4 | XGBoost | With Scaler + Outliers | 0.6598 | 2.50 | 1.05 |
| 5 | KNN | With Scaler | 0.6295 | 2.61 | 1.09 |
| 6 | Decision Tree | With Best Params | 0.6269 | 2.61 | 1.21 |

**Outlier Detection:** 277 baris (5.37%) dari total dataset

---

👥 TEAM MEMBERS

- Timothy Hosia Budianto (5025211098)
- Dimas Aria Pujangga (5025211212)
- Armadya Hermawan (5025211243)
- Daffa Saskara (5025211249)
