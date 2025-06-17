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

### Result Detail
```
import and preprocess
   Preprocess
EDA
   Bedroom
   Bathroom
   Carport
   Land Area
   Building Area
   Price
Encoding, Split Train Test
   Location

HASIL:

Training
   Linear Regression
      Base Model
         Cross-Validation Metrics:
         MAE  : 1671103611.33
         RMSE : 3496460247.51
         R2   : 0.5428

         Test Set Metrics:
         MAE  : 1541513473.09
         RMSE : 2943302175.87
         R2   : 0.5272
      With Scaler
         Cross-Validation Metrics:
         MAE  : 1671103608.91
         RMSE : 3496460248.20
         R2   : 0.5428

         Test Set Metrics:
         MAE  : 1541513479.01
         RMSE : 2943302176.74
         R2   : 0.5272
      With scaler, buang Outlier
         Jumlah baris outlier yang dideteksi: 277
         Persentase outlier: 5.37%

         Cross-Validation Metrics:
         MAE  : 1372546762.07
         RMSE : 2623212111.93
         R2   : 0.6184

         Test Set Metrics:
         MAE  : 1632748576.74
         RMSE : 4182154262.22
         R2   : 0.0454

   Decision Tree Regressor
      Hyperparameter tuning
         Best RMSE: 2997202390.9068117
         Best params: {'max_depth': 41, 'min_samples_split': 2, 'min_samples_leaf': 16, 'max_features': None, 'criterion': 'poisson'}
      with best parameters
         Cross-Validation Metrics:
         MAE  : 1333280670.05
         RMSE : 2997202390.91
         R2   : 0.6639

         Test Set Metrics:
         MAE  : 1209891026.09
         RMSE : 2614703125.40
         R2   : 0.6269
      With Scaler
         Cross-Validation Metrics:
         MAE  : 1333405165.17
         RMSE : 2997253635.27
         R2   : 0.6638

         Test Set Metrics:
         MAE  : 1209836804.55
         RMSE : 2614697029.76
         R2   : 0.6269
      With scaler, buang outlier
        Jumlah baris outlier yang dideteksi: 277
        Persentase outlier: 5.37%

        Cross-Validation Metrics:
        MAE  : 1112151526.55
        RMSE : 2403835853.26
        R2   : 0.6766

        Test Set Metrics:
        MAE  : 1205544685.42
        RMSE : 2694785556.31
        R2   : 0.6037

   Random Forest Regressor
      Hyperparameter Tuning
        Best RMSE: 2783568579.1139116
        Best params: {'n_estimators': 600, 'max_depth': 23, 'min_samples_split': 6, 'min_samples_leaf': 1, 'max_features': 'sqrt', 'bootstrap': False, 'criterion': 'squared_error'}
      With best parameters
        Cross-Validation Metrics:
        MAE  : 1130692690.56
        RMSE : 2783568579.11
        R2   : 0.7108

        Test Set Metrics:
        MAE  : 999826708.51
        RMSE : 2510380720.66
        R2   : 0.6561
      With Scaler
        Cross-Validation Metrics:
        MAE  : 1130770659.73
        RMSE : 2782762069.09
        R2   : 0.7110

        Test Set Metrics:
        MAE  : 1000226467.67
        RMSE : 2511810011.76
        R2   : 0.6557
      with scaler, buang outlier
        Jumlah baris outlier yang dideteksi: 277
        Persentase outlier: 5.37%

        Cross-Validation Metrics:
        MAE  : 913276892.22
        RMSE : 2136695947.43
        R2   : 0.7449

        Test Set Metrics:
        MAE  : 1043166735.61
        RMSE : 2494403723.68
        R2   : 0.6604

   XGBoost Regressor (Gradient Boosting)
      Hyperparameter Tuning
        Best RMSE: 2789652011.327607
        Best params: {'n_estimators': 1000, 'max_depth': 15, 'learning_rate': 0.0035924660731297894, 'subsample': 0.8322288990426941, 'colsample_bytree': 0.8816714316111716, 'min_child_weight': 4, 'gamma': 8.665124272099087, 'reg_alpha': 9.980313002398312, 'reg_lambda': 0.7187922425549057}
      With best parameters
        Cross-Validation Metrics:
        MAE  : 1141005241.67
        RMSE : 2801860650.34
        R2   : 0.7069

        Test Set Metrics:
        MAE  : 1022383623.86
        RMSE : 2334140273.17
        R2   : 0.7027
      with scaler
        Cross-Validation Metrics:
        MAE  : 1141005241.67
        RMSE : 2801860650.34
        R2   : 0.7069

        Test Set Metrics:
        MAE  : 1022383623.86
        RMSE : 2334140273.17
        R2   : 0.7027
      with scaler, buang outlier
        Jumlah baris outlier yang dideteksi: 277
        Persentase outlier: 5.37%

        Cross-Validation Metrics:
        MAE  : 935629451.30
        RMSE : 2191455971.72
        R2   : 0.7309

        Test Set Metrics:
        MAE  : 1045984969.17
        RMSE : 2496525990.96
        R2   : 0.6598

   k-Nearest Neighbors Regressor
      Hyperparameter Tuning
        Best RMSE: 2970191218.149553
        Best parameters: {'n_neighbors': 16, 'weights': 'distance', 'p': 1, 'leaf_size': 39}
      With best parameters
        Cross-Validation Metrics:
        MAE  : 1068215771.32
        RMSE : 2970191218.15
        R2   : 0.6696

        Test Set Metrics:
        MAE  : 1005345034.44
        RMSE : 3070544232.63
        R2   : 0.4854
      with scaler
        Cross-Validation Metrics:
        MAE  : 1238325310.84
        RMSE : 3066220059.11
        R2   : 0.6488

        Test Set Metrics:
        MAE  : 1091233276.30
        RMSE : 2605610427.76
        R2   : 0.6295
      with scaler, buang outlier
        Jumlah baris outlier yang dideteksi: 277
        Persentase outlier: 5.37%

        Cross-Validation Metrics:
        MAE  : 1018035437.30
        RMSE : 2400909526.49
        R2   : 0.6803

        Test Set Metrics:
        MAE  : 1137102002.46
        RMSE : 2701064924.28
        R2   : 0.6018
```

---

👥 TEAM MEMBERS

- Timothy Hosia Budianto (5025211098)
- Dimas Aria Pujangga (5025211212)
- Armadya Hermawan (5025211243)
- Daffa Saskara (5025211249)
