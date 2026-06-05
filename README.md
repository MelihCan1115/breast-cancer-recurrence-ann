# Breast Cancer Recurrence Prediction using Artificial Neural Networks
[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![TensorFlow](https://img.shields.io/badge/TensorFlow-2.x-orange.svg)](https://www.tensorflow.org/)
[![Keras](https://img.shields.io/badge/Keras-API-red.svg)](https://keras.io/)
[![Scikit-Learn](https://img.shields.io/badge/scikit--learn-Machine%20Learning-orange.svg)](https://scikit-learn.org/)
## Proje Özeti
Bu proje **GBSG (Kaggle)** meme kanseri veri seti üzerinde **Yapay Sinir Ağları (YSA/ANN)** kullanılarak hastaların hastalığı tekrar geçirme (nüks) veya yaşam kaybı riskini tahmin etmeye yönelik bir **ikili sınıflandırma (Binary Classification)** çalışmasıdır.
Bu proje kapsamında iki farklı YSA modeli geliştirilmiş ve karşılaştırılmıştır:
- **Model A:** Tüm özelliklerin kullanıldığı temel model (Zaman/`rfstime` verisi dahil).
- **Model B:** Gelecekteki zaman bilgisinin modele verilmediği, daha gerçekçi ve **klinik bir tıbbi eşik (threshold)** optimizasyonu içeren model (`rfstime` hariç).
## Veri Seti
Kullanılan veri seti: [Breast Cancer Dataset (GBSG - Kaggle)](https://www.kaggle.com/datasets/utkarshx27/breast-cancer-dataset-used-royston-and-altman) [Son Erişim: 5 Haziran 2026]
Veri seti **686 örnek** ve **11 özellikten** oluşmaktadır.
**Girdi Özellikleri (Features):**
- `Yaş` (Age)
- `Menopoz Durumu` (Menopausal Status)
- `Tümör Boyutu` (Tumor Size)
- `Derece` (Grade)
- `Lenf Nodu Sayısı` (Nodes)
- `pgr` (Progesteron Reseptörü)
- `er` (Östrojen Reseptörü)
- `Hormonal Tedavi Durumu` (Hormonal Therapy)
- `rfstime` (Nükssüz Sağkalım Süresi - *Sadece Model A'da kullanıldı*)
**Çıktı / Hedef (Target):**
- `status`: İkili (Binary) değişken.
  - `0` = Hayatta ve Nüks Yok
  - `1` = Ölüm veya Nüks Var
## Geliştirilen Yapay Sinir Ağı Mimarisi
Proje kapsamında **TensorFlow / Keras** altyapısı ile derin öğrenme modelleri kurulmuştur. Model mimarisinde aşırı öğrenmeyi (overfitting) engellemek ve stabilizasyonu artırmak için çeşitli teknikler kullanılmıştır.
**Model Mimarisi Detayları:**
- **Giriş Katmanı:** Özellik sayısına bağlı input layer.
- **Gizli Katmanlar (Hidden Layers):** 
  - 1. Katman: 128 Nöron (ReLU) + L2 Regularization
  - Batch Normalization + Dropout (0.4)
  - 2. Katman: 64 Nöron (ReLU) + L2 Regularization
  - Batch Normalization + Dropout (0.3)
  - 3. Katman: 32 Nöron (ReLU)
- **Çıktı Katmanı:** 1 Nöron (Sigmoid Aktivasyon Fonksiyonu)
- **Optimizer:** Adam Optimizer
- **Kayıp Fonksiyonu (Loss):** Binary Crossentropy
## Performans Değerlendirmesi
Modellerin performansı; **Accuracy, Precision, Recall, F1-Score ve ROC-AUC** metrikleri kullanılarak hesaplanmış ve bir "Baseline" modeli olan Logistic Regression ile karşılaştırılmıştır. 
Özellikle **Model B**'de tıp alanında hastalığı kaçırmamanın (False Negative oranını düşürmenin) önemi göz önüne alınarak, **Recall değerini (≥0.75)** maksimize edecek optimal bir tıbbi eşik (threshold) belirlenmiştir. Ayrıca **SHAP (SHapley Additive exPlanations)** analizi ile modelin kararlarında hangi özelliklerin ne kadar etkili olduğu (Feature Importance) incelenmiştir.
## Kurulum ve Çalıştırma
### Gereksinimler
Projeyi yerel makinenizde çalıştırmak için gerekli kütüphaneleri kurun:
```bash
pip install numpy pandas matplotlib seaborn scikit-learn tensorflow keras shap kagglehub
```
### Projeyi Çalıştırma
Jupyter Notebook'u başlatın ve `breast_cancer_ann_final.ipynb` dosyasını çalıştırın:
```bash
jupyter notebook
```
## Dosya Yapısı
- `breast_cancer_ann_final.ipynb`: Veri ön işleme, Model A & B'nin eğitimi, test edilmesi, metriklerin hesaplanması ve görselleştirmelerin yer aldığı ana Jupyter Notebook dosyası.
- `README.md`: Proje açıklama dosyası.
- *Rapor dosyaları (.docx, .pdf)*: Projenin akademik formatta yazılmış raporları.
Bu proje Hesaplamalı Zeka dersi final projesi kapsamında geliştirilmiştir.
