# Breast Cancer Recurrence Prediction using Artificial Neural Networks
## Yapay Sinir Ağları Kullanılarak Meme Kanseri Nüksünün Tahmin Edilmesi
[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![TensorFlow](https://img.shields.io/badge/TensorFlow-2.x-orange.svg)](https://www.tensorflow.org/)
[![Keras](https://img.shields.io/badge/Keras-API-red.svg)](https://keras.io/)
[![Scikit-Learn](https://img.shields.io/badge/scikit--learn-Machine%20Learning-orange.svg)](https://scikit-learn.org/)
English [EN] | Türkçe [TR]

<p align="center">
  <strong>Figure 1.</strong> Overview of the Breast Cancer Prediction System. [EN]<br>
  <strong>Şekil 1.</strong> Meme Kanseri Tahmin Sistemine genel bakış. [TR]
</p>

## Abstract [EN]
This study examines the performance of Artificial Neural Networks (ANN) in predicting the recurrence and survival rates of breast cancer patients within an academic framework. Two distinct deep learning models (Model A and Model B) were evaluated using the open-access GBSG dataset. Model B specifically focused on a clinical approach by excluding future data variables and optimizing a medical threshold to prioritize patient safety (maximizing recall). This project was developed as a final project for the Computational Intelligence course.

## Özet [TR]
Bu çalışma, akademik bir çerçevede meme kanseri hastalarının nüks ve sağkalım oranlarını tahmin etmede Yapay Sinir Ağlarının (YSA) performansını incelemektedir. Açık erişimli GBSG veri seti kullanılarak iki farklı derin öğrenme modeli (Model A ve Model B) değerlendirilmiştir. Model B, geleceğe dair verileri hariç tutarak ve hasta güvenliğini önceleyen (recall değerini maksimize eden) bir tıbbi eşik (threshold) optimize ederek tamamen klinik bir yaklaşıma odaklanmıştır. Bu proje, Hesaplamalı Zeka dersi final projesi kapsamında geliştirilmiştir.

---

## Objective / Amaç

**[EN]** The primary objective of this study is to design an ANN model capable of binary classification (Survival/No Recurrence vs. Death/Recurrence) with maximum accuracy. Furthermore, it aims to establish a clinically realistic model by excluding the Recurrence-Free Survival Time (`rfstime`) variable to mimic real-world diagnostic scenarios.

**[TR]** Bu çalışmanın temel amacı, ikili sınıflandırma (Yaşıyor/Nüks Yok vs. Ölüm/Nüks Var) yapabilen ve maksimum doğruluğa sahip bir YSA modeli tasarlamaktır. Ayrıca, gerçek dünyadaki teşhis senaryolarını taklit etmek amacıyla Nükssüz Sağkalım Süresi (`rfstime`) değişkenini dışarıda bırakarak klinik olarak gerçekçi bir model oluşturmak hedeflenmiştir.

---

## Methodology / Metodoloji

**[EN]** The study utilized a comprehensive Deep Learning methodology:
- **Dataset:** 686 samples with 11 features (Age, Tumor Size, Grade, Nodes, PGR, ER, etc.)
- **Preprocessing:** Log transformations for skewed features, feature engineering (PGR*ER interactions), and Standard Scaling.
- **Model Architecture:** A 3-hidden-layer Sequential ANN (128->64->32 neurons) incorporating L2 Regularization, Batch Normalization, and Dropout to prevent overfitting.
- **Evaluation:** The models were compared against a Logistic Regression baseline. SHAP (SHapley Additive exPlanations) was used for feature importance analysis.

**[TR]** Çalışmada kapsamlı bir Derin Öğrenme metodolojisi kullanılmıştır:
- **Veri Seti:** 11 özelliğe sahip 686 örnek (Yaş, Tümör Boyutu, Derece, Lenf Nodu, PGR, ER vb.)
- **Ön İşleme:** Çarpık dağılımlı özellikler için Log dönüşümleri, özellik mühendisliği (PGR*ER etkileşimleri) ve Standart Ölçeklendirme (Standard Scaling).
- **Model Mimarisi:** Aşırı öğrenmeyi (overfitting) önlemek için L2 Regularizasyonu, Batch Normalization ve Dropout içeren 3 gizli katmanlı (128->64->32 nöron) ardışık YSA.
- **Değerlendirme:** Modeller, temel bir Lojistik Regresyon modeliyle karşılaştırılmıştır. Özellik önem analizi için SHAP kullanılmıştır.

---

## Key Findings / Ana Bulgular

### 1. Classification Performance
- **Model A (`rfstime` included):** Achieved the highest accuracy but suffers from data leakage as survival time is a future variable.
- **Model B (`rfstime` excluded):** Provided realistic clinical performance. By optimizing the medical threshold, the False Negative rate was significantly reduced.

### 2. Clinical Threshold Optimization
- Instead of using the default `0.5` threshold, Model B's decision boundary was optimized to achieve a **Recall ≥ 0.75**. This is crucial in medicine to ensure high-risk patients are not misclassified as low-risk.

### 3. Feature Importance (SHAP)
- Feature analysis revealed that **Progesterone Receptor (PGR)**, **Tumor Size**, and **Number of Nodes** had the most significant impact on the model's prediction of recurrence.

<p align="center">
  <img src="assets/image6.png" alt="Model Evaluation" width="45%">
  <img src="assets/image7.png" alt="Confusion Matrix" width="45%">
</p>
<p align="center">
  <em>Figure 2. Sample Training Loss/Accuracy and Confusion Matrix Outputs from the models.</em>
</p>

---

## Results Summary / Sonuç Özeti

| Model | Setup | Threshold | Accuracy | Precision | Recall | ROC-AUC |
|-------|-------|-----------|----------|-----------|--------|---------|
| **Logistic Reg. (Baseline)** | `rfstime` excluded | 0.50 | Moderate | Moderate | Moderate | Moderate |
| **Model A** | `rfstime` included | 0.50 | **Highest** | **Highest** | High | **Highest** |
| **Model B (Clinical)** | `rfstime` excluded | **Optimized** | High | Moderate | **≥ 0.75** | High |

*(Exact metric values can be found in the project report and Jupyter Notebook outputs).*

---

## Conclusion / Sonuç

**[EN]** This study demonstrates that Artificial Neural Networks can be effectively employed for breast cancer recurrence prediction. The findings indicate that:
1. While including time-to-event variables (`rfstime`) artificially boosts accuracy, it does not reflect realistic diagnostic conditions.
2. Clinical Threshold Optimization is vital; sacrificing slight overall accuracy to maximize Recall ensures that critical cases are not missed.
3. Complex deep learning models with appropriate regularization (Dropout, Batch Norm) outperform baseline linear classifiers in capturing complex interactions between biological markers (like PGR and ER).

**[TR]** Bu çalışma, Yapay Sinir Ağlarının meme kanseri nüks tahmininde etkili bir şekilde kullanılabileceğini göstermektedir. Bulgular şunları işaret etmektedir:
1. Zamana bağlı değişkenlerin (`rfstime`) dahil edilmesi doğruluğu yapay olarak artırsa da, gerçekçi teşhis koşullarını yansıtmaz.
2. Klinik Eşik Optimizasyonu (Threshold Optimization) hayati önem taşır; Recall değerini maksimize etmek için genel doğruluktan bir miktar feda etmek, kritik vakaların gözden kaçırılmamasını sağlar.
3. Uygun düzenleme (Dropout, Batch Norm) tekniklerine sahip karmaşık derin öğrenme modelleri, biyolojik belirteçler arasındaki karmaşık etkileşimleri yakalamada temel doğrusal sınıflandırıcılardan daha iyi performans gösterir.

---

### How to Run / Kurulum
```bash
pip install numpy pandas matplotlib seaborn scikit-learn tensorflow keras shap kagglehub
jupyter notebook breast_cancer_ann_final.ipynb
```
