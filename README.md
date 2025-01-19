# Data-Analyse-and-Machine-Learning-Project-on-Recipe-Dataset
Data Analyse and Machine Learning on Recipe Dataset.
# Tarif Veri Seti Analizi ve Kümeleme

Bu depo, bir tarif veri seti üzerinde keşifsel veri analizi (EDA), temel modelleme ve kümeleme gerçekleştiren bir Python not defteri (`Recipe-Dataset-Analyse.ipynb`) içerir. Amaç, verilerden içgörüler elde etmek ve tarif kümeleri oluşturmaktır.

## İçindekiler

*   [Genel Bakış](#genel-bakış)
*   [Veri](#veri)
*   [Not Defteri İncelemesi](#not-defteri-incelemesi)
*   [Temel Bulgular](#temel-bulgular)
*   [Depodaki Dosyalar](#depodaki-dosyalar)
*   [Kullanım](#kullanım)
*   [Bağımlılıklar](#bağımlılıklar)
*   [Sonraki Adımlar](#sonraki-adımlar)
*   [Lisans](#lisans)
*   [Yazar](#yazar)

## Genel Bakış

Bu proje, özelliklerini anlamak ve gizli kalıpları ortaya çıkarmak için bir tarif veri setini analiz eder. Not defteri şunları kapsar:
* Veri Yükleme ve Temizleme
* Keşifsel Veri Analizi (EDA)
* Tahmini modeller oluşturma ve test etme.
* Hiyerarşik kümeleme kullanarak kümeleme analizi yapma.
* Küme kalitesini ve özellik önemini değerlendirme ve analiz etme.

## Veri

Bu analizde kullanılan veri seti, `recipes_images.json` adlı bir JSON dosyasında saklanır. Bu dosya, aşağıdakiler de dahil olmak üzere tarif bilgilerini içerir:

*   Tarif başlıkları
*   Açıklamalar
*   İçindekiler
*   Pişirme süresi
*   Porsiyon sayıları
*   Yayın tarihi
*   Resim dosyası adı
*   Talimatlar
*   Değerlendirmeler
*   Çeşitli etiketler (tür, mutfak, içerik, öğün, özel durumlar, ekipman vb.)

## Not Defteri İncelemesi

`Recipe-Dataset-Analyse.ipynb` not defteri aşağıdaki adımları gerçekleştirir:

1.  **Veri Yükleme ve İlk İnceleme:**
    *   `recipes_images.json` dosyasını yükler.
    *   JSON verilerini pandas DataFrame'ine dönüştürür.
    *   `df.info()` kullanarak veri seti hakkında temel bilgileri (sütunlar, veri türleri, null değerler) görüntüler.
2.  **Veri Filtreleme ve Seçimi:**
    *   Analiz için ilgili sütunları (`title`, `ratings.rating`, `ratings.count`, `tags.special-consideration`) seçer.
    *   Seçilen sütunlarla yeni bir DataFrame (`df_filtered`) oluşturur.
3.  **Veri Temizleme ve Ön İşleme:**
    *   `ratings.rating` ve `ratings.count` sütunlarındaki eksik değerleri ortalama ile doldurmak için `SimpleImputer` kullanır.
    *   `tags.special-consideration` değeri eksik olan satırları siler.
    *    `tags.special-consideration` sütunundaki özel durumları birleştirerek tek bir stringe dönüştürür ve one-hot encoding uygular ve orijinal sütunu siler.
    *   Aykırı değerleri ele almak için `ratings.rating` sütununu %5 ve %95'lik yüzdelik dilimlerde sınırlandırır (winsorization).
    *   `ratings.count` değeri medyanın üzerinde olanlar için yeni bir ikili özellik (`high_ratings_count`) oluşturur.
4.  **Keşifsel Veri Analizi (EDA):**
    *   `ratings.rating` ve `ratings.count` dağılımlarını histogramlar ve yoğunluk grafikleri ile görselleştirir.
    *   İkili özelliklerin (özel durumlardan oluşturulan) sıklığını bir çubuk grafikte görüntüler.
    *   İkili özelliklerin korelasyon matrisini bir ısı haritası ile görselleştirir.
5.  **Temel Modelleme:**
    *   One-hot encoding yapılmış `special considerations` sütunları ile hedef olarak da `ratings.rating` sütununu kullanarak bir model oluşturur.
    *   Veriyi eğitim ve test kümelerine ayırır.
    *   Aşağıdaki regresyon modellerini eğitmek ve performanslarını değerlendirmek için bir fonksiyon tanımlar ve doğruluk (1-MSE/Varyans) puanlarını hesaplar.
        *   Linear Regression (Doğrusal Regresyon)
        *   Gradient Boosting Regressor (Gradyan Artırma Regresyonu)
        *   Random Forest Regressor (Rastgele Orman Regresyonu)
6.  **Kümeleme Analizi:**
    *   Tariflerdeki kümeleri belirlemek için öklid uzaklığı kullanarak 'ward' yöntemiyle hiyerarşik kümeleme uygular.
    *   Aşağıdakileri kullanarak kümeleri görselleştirir:
        *   Küme sayısını belirlemeye yardımcı olmak için bir dendrogram
        *   Boyut indirgeme için PCA kullanan bir saçılım grafiği
        *   Özellik ortalamalarının kümeler arasındaki ısı haritası
        *   Küme bazında derecelendirme dağılımının kutu grafiği
    *   Verinin ne kadar iyi kümelendiğini belirlemek için Siluet Skoru, Calinski-Harabasz İndeksi ve Davies-Bouldin İndeksi gibi kümeleme kalite metriklerini hesaplar ve yazdırır.
    *    Her kümedeki en belirgin ilk 5 özelliği yazdırır.

## Temel Bulgular

*   Veri seti, çeşitli etiketlere ve özel durumlara sahip çok çeşitli tarifler içerir.
*   Değerlendirme dağılımının çarpık olduğu görülmektedir.
*  Winsorization, puanlardaki aykırı değerlerin etkisini azaltmaya yardımcı olur.
*   Farklı kümeleme algoritmaları, her küme için farklı bir kalite ve farklı tarifler sunmaktadır.
*    Tanımlanan modellerin doğruluk oranı yaklaşık %1 seviyesinde olup, performansları iyi değildir.

## Depodaki Dosyalar

*   `Recipe-Dataset-Analyse.ipynb`: Veri analizi ve modelleme için tüm kodu içeren Jupyter Not Defteri.
*   `data/recipes/recipes_images.json`: Ham JSON veri seti.

## Kullanım

1.  Bu depoyu yerel makinenize klonlayın.
2.  Python 3.6+ sürümünün yüklü olduğundan emin olun.
3.  `pip install -r requirements.txt` komutunu kullanarak gerekli paketleri yükleyin.
4.  Jupyter'da `Recipe-Dataset-Analyse.ipynb` not defterini açın ve çalıştırın.

## Bağımlılıklar

*   `pandas`
*   `numpy`
*   `matplotlib`
*   `seaborn`
*   `scikit-learn`
*   `scipy`

Bunları aşağıdaki komutu kullanarak yükleyebilirsiniz:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn scipy
