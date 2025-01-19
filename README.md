# Data-Analyse-and-Machine-Learning-Project-on-Recipe-Dataset

Bu repository, tarif veri seti üzerinde keşifsel veri analizi (EDA), temel modelleme ve kümeleme gerçekleştiren bir Python not defteri olan `Recipe-Dataset-Analyse.ipynb` dosyasını içerir. Projenin amacı, tariflere ait verileri analiz ederek içgörüler elde etmek, tariflerin özelliklerine göre kümeler oluşturmak ve modeller aracılığıyla verilerin davranışını anlamaktır.

Proje Sunum Video Linki: (https://www.youtube.com/watch?v=mrljEQmxPBA&ab_channel=EsranurSevilmi%C5%9F)
## İçindekiler

- [Genel Bakış](#genel-bakış)
- [Veri](#veri)
- [Not Defteri İncelemesi](#not-defteri-incelemesi)
- [Temel Bulgular ve Sonuç](#temel-bulgular-ve-sonuç)
- [Kullanım](#kullanım)
- [Bağımlılıklar](#bağımlılıklar)


---

## Genel Bakış

Bu projede, tarif veri seti kullanılarak veri analizi ve makine öğrenimi teknikleri uygulanmıştır. Çalışmanın temel aşamaları şunlardır:

- **Keşifsel Veri Analizi (EDA):** Veri setindeki trendlerin ve kalıpların görselleştirilmesi.
- **Veri Temizleme ve Ön İşleme:** Eksik değerlerin giderilmesi, aykırı değerlerin yönetimi ve özellik mühendisliği.
- **Temel Modelleme:** Farklı regresyon modellerinin performanslarının değerlendirilmesi.
- **Kümeleme Analizi:** Tariflerin benzerliklerine göre gruplandırılması ve kümeler arasındaki farklılıkların incelenmesi.

---

## Veri

Kullanılan veri seti, [Recipe Dataset with Images, Tags, and Ratings](https://www.kaggle.com/datasets/seungyeonhan1/recipe-dataset-with-images-tags-and-ratings) adresinden alınmıştır. Veri seti, tariflere ilişkin şu bilgileri içermektedir:

- **Başlık (Title):** Tarif isimleri.
- **Değerlendirme (Ratings):** Kullanıcı değerlendirme puanları ve yorum sayıları.
- **İçindekiler (Ingredients):** Tarifin malzemeleri.
- **Etiketler (Tags):** Özel durumlar (örneğin vegan, glütensiz, keto vb.).
- **Talimatlar (Instructions):** Tariflerin hazırlanış yöntemleri.
- **Pişirme Süresi ve Porsiyon:** Tarifin hazırlanma süresi ve porsiyon miktarı.

---

## Not Defteri İncelemesi

Not defteri aşağıdaki adımları içermektedir:

1. **Veri Yükleme ve İnceleme:**
   - Veri seti yüklendi, incelendi ve eksik değerler tespit edildi.
2. **Veri Temizleme ve Ön İşleme:**
   - Eksik değerler giderildi.
   - Aykırı değerler Winsorization yöntemiyle sınırlandırıldı.
   - Etiketler one-hot encoding yöntemiyle sayısallaştırıldı.
3. **EDA (Keşifsel Veri Analizi):**
   - Değerlendirme puanları ve özelliklerin dağılımları görselleştirildi.
   - Özellikler arası korelasyon incelendi.
4. **Modelleme:**
   - Linear Regression, Gradient Boosting ve Random Forest modelleri değerlendirildi.
5. **Kümeleme:**
   - Tarifler hiyerarşik kümeleme yöntemiyle gruplandırıldı.
   - Küme özellikleri detaylıca analiz edildi.

---

## Temel Bulgular ve Sonuç

### 1. Kümeleme Bulguları:
Veri kümesi 3 gruba ayrılmıştır:

| Küme | Ortalama Puan | Standart Sapma | Ortalama Değerlendirme Sayısı| Öne Çıkan Özellikler                   |
|------|---------------|----------------|-----------------------|-----------------------------------------------|
| 1    | 4.20          | 0.40           | 18.79                 | Vegan, Vejetaryen, Glütensiz                  |
| 2    | 3.85          | 0.59           | 17.64                 | Kosher, Pescatarian, Düşük Şeker İçeriği      |
| 3    | 4.21          | 0.39           | 23.41                 | Yüksek Derecelendirme, Nötresiz, Keto         |

- Kümeleme analizi, tariflerin spesifik diyet gereksinimlerine ve puanlarına göre farklı gruplara ayrılabileceğini göstermiştir.
- Küme 3, genellikle yüksek derecelendirme puanlarına ve daha fazla yorum sayısına sahiptir.

### 2. Modelleme Performansı:
Regresyon modellerinin doğruluk oranları oldukça düşüktür:

| Model                      | Doğruluk (%) | MSE    | R²     |
|----------------------------|--------------|--------|--------|
| Linear Regression          | 1.2          | 0.153  | 0.012  |
| Gradient Boosting Regressor| 0.9          | 0.154  | 0.009  |
| Random Forest Regressor    | 0.4          | 0.155  | 0.004  |

- Modeller, derecelendirme puanlarını tahmin etmede düşük başarı göstermiştir. Bunun temel nedenleri, veri setindeki etiketlerin ve derecelendirme puanlarının çok fazla varyans göstermesi olabilir.

### 3. Genel Değerlendirme:
- Hiyerarşik kümeleme, tariflerin gruplandırılmasında anlamlı bir araç olarak öne çıkmıştır.
- Öne çıkan özelliklerin belirlenmesi, tariflerin diyet gereksinimlerine göre gruplandırılmasını kolaylaştırmıştır.
- Modelleme sonuçlarının iyileştirilmesi için daha fazla özellik mühendisliği yapılması önerilmektedir.

---
## Kullanım

1.  Bu repository'i yerel makinenize klonlayın.
2.  Python 3.6+ sürümünün yüklü olduğundan emin olun.
3.  pip install -r requirements.txt komutunu kullanarak gerekli paketleri yükleyin.
4.  Jupyter'da Recipe-Dataset-Analyse.ipynb not defterini açın ve çalıştırın.

## Bağımlılıklar

*   pandas
*   numpy
*   matplotlib
*   seaborn
*   scikit-learn
*   scipy

Bunları aşağıdaki komutu kullanarak yükleyebilirsiniz:

````bash
pip install pandas numpy matplotlib seaborn scikit-learn 

