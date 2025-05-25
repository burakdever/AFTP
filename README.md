# 🚗 Araç Fiyat Tahmin Projesi

Bu proje, araçların çeşitli teknik ve görsel özelliklerini kullanarak satış fiyatlarını tahmin etmeyi amaçlamaktadır. Makine öğrenmesi algoritmaları kullanılarak oluşturulan modeller sayesinde, veri analizi ve modelleme pratiği yapılmıştır.

---

## 🔍 Proje Amacı

Verilen bir araç veri setindeki bilgileri kullanarak, **sellingprice** (satış fiyatı) değişkenini tahmin edebilecek gözetimli öğrenme modelleri geliştirmek.

Kullanılan veri seti: [Kaggle - Vehicle Sales Data](https://www.kaggle.com/datasets/syedanwarafridi/vehicle-sales-data)  
Notebook: [Kaggle Notebook Linki](https://www.kaggle.com/code/burakerturk/arac-fiyat-tahmin-projesi)

---

## ⚙️ Teknik Yaklaşım

### 🔧 Veri Ön İşleme

- **Gereksiz Sütun Temizliği:** `vin`, `seller`, `state`, `mmr` gibi analiz için gereksiz sütunlar kaldırıldı.
- **Feature Engineering:** `saledate` ve `year` sütunlarından araç yaşı (`vehicle_age`) hesaplandı.
- **Eksik Veriler:** NaN içeren satırlar temizlendi.
- **Aykırı Değer Temizliği:** `sellingprice` ve `odometer` sütunlarında IQR yöntemi ile filtreleme uygulandı.
- **Yüksek Kardinalite Yönetimi:** Kategori sayısı çok olan sütunlarda (örn. `model`, `trim`) nadir kategoriler gruplanarak **Other_*** şeklinde yeniden etiketlendi.

### 🛠️ Pipeline Yapısı

Scikit-learn pipeline yapısı kullanılarak:

- **Sayısal veriler:** `StandardScaler`
- **Kategorik veriler:** `OneHotEncoder`

---

## 📈 Kullanılan Algoritmalar

Aşağıdaki algoritmalar temel parametrelerle test edilmiştir:

- `Linear Regression` (Baseline)
- `Ridge Regression` (L2 Regularization)
- `Lasso Regression` (L1 Regularization)
- `Decision Tree Regressor` (Sınırlı parametrelerle)

---

## 📊 Model Performansları

| Model               | Test R² Skoru |
|--------------------|---------------|
| **Ridge Regression** | **0.869**        |
| Linear Regression  | 0.869          |
| Lasso Regression   | 0.869          |
| Decision Tree      | 0.776          |

> 🏆 En iyi performansı Ridge Regression göstermiştir.

### 🎯 Ridge Regression - Hiperparametre Optimizasyonu

- `GridSearchCV` ile `alpha` parametresi 7 farklı değer için test edilmiştir.
- En iyi alpha: `0.01`

---

## 🚧 Bilinen Sınırlamalar & Geliştirme Alanları

1. **Model Çeşitliliği Eksikliği:**  
   Sadece temel lineer modeller kullanıldı. Gelecekte:
   - `Random Forest`
   - `Gradient Boosting` gibi yöntemler eklenebilir.

2. **Feature Engineering Gelişimi:**  
   - `marka-model` kombinasyonlarından çıkarım
   - `price categories` gibi türetilmiş değişkenler
   - Zaman bazlı (seasonal) analizler yapılabilir.
