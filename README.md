# HABER KATEGORİLERİNİ TAHMİN ETMEK

Bu kod, bir haber başlığı ve kısa açıklamadan oluşan bir veri kümesindeki haber kategorilerini tahmin etmek için bir dizi makine öğrenimi modelini eğitiyor. Önce veriyi yüklüyor, ön işleme adımları uyguluyor, ardından farklı model ve vektörleştirme stratejileri kullanarak sınıflandırma yapılıyor. Sonuçları değerlendirmek için sınıflandırma raporları kullanılıyor.
<br/>

## Projeyi Geliştirenler

Mehmet Fatih Kuru<br/>
Karya Korkmazyiğit

## Kullanılan Kütüphaneler



|  | **Kütüphane İsimleri** |  |
| -------------------------------| -------------------------------| -------------------------------|
| numpy (np)      | pandas (pd) | scikit-learn |
| spacy      | sklearn.pipeline      |   sklearn.preprocessing |
| sklearn.naive_bayes.MultinomialNB | sklearn.naive_bayes.MultinomialNB      |    sklearn.linear_model.LogisticRegression |
| sklearn.model_selection.train_test_split      | sklearn.metrics.classification_report | sklearn.feature_extraction.text.CountVectorizer |

<br/>
<br/>

# VERİ SETİ'NİN OLUŞTURULMASI

Veri kümesi kaggle'dan çekilen ve istenilen kategorilerde yapılmış haberlerden oluşacaktır. Çektiğimiz veri kümesi aşağıda gösterildiği gibi çok büyük ve çok fazla kategori içermektedir. 

![kategori_icerik_sayisi](https://github.com/Fatihgn/Haber_Kategori_Tahmin/assets/116540800/d9fe4838-7156-4518-b056-2edb74b32437)




Veri kümesini küçültmek için, 5 kategori (POLITICS,WELLNESS,ENTERTAINMENT,TRAVEL,STYLE & BEAUTY) seçilmiştir ve her kategori için 5000 kayıt seçilmiştir. Bu kategorilerdeki veriler ile model eğitileceği için bu verilerin düzgün veriler olması gerekir. Bu yüzden verilerin çekilmeden önce boş olup olmaması gibi kontroller yapılmıştır.
  
## Veri seti'nde Bulunan Kategorilerdeki Haber Sayıları:

![indir](https://github.com/Fatihgn/Haber_Kategori_Tahmin/assets/116540800/fc2b2552-2139-4722-a7e1-fbd968746f68)


  

## Oluşturulmuş Olan Veri seti'nin Görseli:

![25000verilistesi](https://github.com/Fatihgn/Haber_Kategori_Tahmin/assets/116540800/fbb4dee5-846d-4dd2-bfd0-f5aac49fef0f)

<br/>
<br/>

# MODELİN OLUŞTURULMAYA BAŞLANMASI
## Etiketleme

Haberlerin kategorileri kelime şeklinde kayıtlı olduğu için bu kategoriler 0, 1, 2, 3, 4 gibi bilgisayarın anlayabileceği bir formata dönüştürülmelidir.

Target adında yeni bir kolon açılarak kategorisi entertainment olan haberler için 0 rakamı, kategorisi politics olan haberler için 1 rakamı, kategorisi style & beauty olan haberler için 2 rakamı, kategorisi travel olan haberler için 3 rakamı ve kategorisi wellness olan haberler için 4 rakamı target olarak eklenmiştir.

![taget](https://github.com/Fatihgn/Haber_Kategori_Tahmin/assets/116540800/d714e008-8beb-424e-a736-2428b31160f8)


## Veri setinin düzenlenmesi
Makine öğrenmesi için başlık ve kısa açıklama sütunlarını yeni bir 'text' sütununda birleştirilmiştir. 

Ardından aşağıda gösterildiği gibi veri kümesi eğitim ve test setlerine bölünmüştür.

![xytest](https://github.com/Fatihgn/Haber_Kategori_Tahmin/assets/116540800/762e6b08-fb52-444b-aaea-4f67f4ed9e5b)

SpaCy'nin İngilizce dil modelini yüklenmiştir. Stop words ve noktalama işaretlerini filtreleyen ve lemmaları çıkaran bir işleme fonksiyonu tanımlanmıştır.


## Modellerin Eğitilmesi
Daha önceden parçalanmış olan X_train ve y_train verileri gönderilerek modeller eğitilmiştir. Modelleri eğitmek için sklearn kütüphanesi kullanılmıştır.

![cls1](https://github.com/Fatihgn/Haber_Kategori_Tahmin/assets/116540800/a72e175f-f131-419e-b90e-c308fd1a3f7d)

<br/>
<br/>

# KATEGORİLERE GÖRE BAŞARI DAĞILIMLARI
Kategorilere göre modellerin test verisetindeki başarı dağılımları classification_report() fonksiyonu kullanılarak hesaplanmıştır. Alınan sonuçlar aşağıda bulunmaktadır.

![test](https://github.com/Fatihgn/Haber_Kategori_Tahmin/assets/116540800/f0aa1c1b-7f09-4756-bc10-e8fcadcd28d4)


Gördüğünüz gibi MultinomialNB ve n_grams=(1,3) kullandığımızda cls2'den en iyi sonuç (%91 doğruluk) alınmaktadır.


