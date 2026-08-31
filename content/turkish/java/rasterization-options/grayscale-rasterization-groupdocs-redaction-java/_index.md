---
date: '2026-05-17'
description: GroupDocs.Redaction for Java kullanarak PDF'yi grayscale'e rasterize
  etmeyi, bir grayscale filtresi uygulamayı ve belgelerinizi güvenli ve yüksek kalitede
  tutmayı öğrenin.
keywords:
- how to rasterize pdf
- java pdf to image
- apply grayscale filter pdf
schemas:
- author: GroupDocs
  dateModified: '2026-05-17'
  description: Learn how to rasterize PDF to grayscale using GroupDocs.Redaction for
    Java, apply a grayscale filter, and keep your documents secure and high‑quality.
  headline: How to rasterize PDF to grayscale with GroupDocs.Redaction Java – Secure
    and Optimize Your Documents
  type: TechArticle
- questions:
  - answer: In GroupDocs.Redaction, the grayscale option is tied to rasterization,
      which ensures consistent results and adds a security layer.
    question: Can I convert documents to grayscale without rasterization?
  - answer: All major formats supported by GroupDocs.Redaction—including DOCX, PDF,
      XLSX, PPTX, RTF, and more than 100 others—can be rasterized and converted to
      grayscale.
    question: What document formats support grayscale rasterization?
  - answer: Yes. Text‑heavy files may grow, while image‑heavy files might shrink.
      DPI settings have the biggest impact.
    question: Will rasterization affect the file size of my documents?
  - answer: No. Rasterization is one‑way; keep a backup of the original if you need
      to revert.
    question: Is it possible to reverse the grayscale rasterization process?
  - answer: Use a higher DPI (300 + for print quality) and choose PDF as the output
      format for best archival results.
    question: How can I optimize the quality of grayscale rasterized documents?
  type: FAQPage
title: GroupDocs.Redaction Java ile PDF'yi grayscale'e rasterize etme – Belgelerinizi
  Güvenli Hale Getirin ve Optimize Edin
type: docs
url: /tr/java/rasterization-options/grayscale-rasterization-groupdocs-redaction-java/
weight: 1
---

# GroupDocs.Redaction Java ile PDF'yi gri tonlamaya rasterleştirme

PDF'yi **rasterleştirmeniz** gerektiğinde, belgelerinizi güvende, profesyonel görünümlü ve arşivlemeye kolay tutmak istiyorsanız doğru yerdesiniz. Bu öğreticide, renkli DOCX, PDF veya diğer desteklenen dosyaları GroupDocs.Redaction for Java kullanarak temiz, gri tonlamalı rasterleştirilmiş bir sürüme dönüştürmek için tam adımları göstereceğiz. Rasterleştirmenin neden bir güvenlik katmanı eklediğini, kütüphaneyi nasıl yapılandıracağınızı ve kaynakları nasıl verimli yöneteceğinizi anlayacaksınız — hepsi dostane, adım adım bir tarzda sunulacak.

## Hızlı Cevaplar
- **Gri tonlamalı rasterleştirme ne yapar?** Her sayfayı yüksek çözünürlüklü bir görüntüye dönüştürür ve ardından bir gri tonlama filtresi uygular, tüm renk bilgilerini kaldırır.  
- **Bunun için GroupDocs.Redaction neden kullanılmalı?** Kırpma güvenliğini rasterleştirme seçenekleriyle tek bir, kullanımı kolay API'de birleştirir.  
- **Hangi formatlar destekleniyor?** DOCX, PDF, XLSX, PPTX, RTF ve 100'den fazla diğer format.  
- **Lisans gerekiyor mu?** Üretim için geçerli bir GroupDocs.Redaction lisansı gereklidir; test için ücretsiz deneme sürümü mevcuttur.  
- **Hangi Java sürümü gerekiyor?** JDK 8 veya üzeri.

## PDF'yi gri tonlamaya nasıl rasterleştirirsiniz?

`new Redactor("path/to/file")` ile kaynak belgenizi yükleyin, `RasterizationOptions` aracılığıyla rasterleştirmeyi etkinleştirin, gri tonlama gelişmiş seçeneğini ekleyin ve `save()` metodunu çağırın — dönüşüm birkaç kısa satırda gerçekleşir. Bu yaklaşım, her sayfanın görüntü tabanlı, siyah‑beyaz bir PDF olmasını sağlar, metin seçimini engeller ve tutarlı bir baskıya hazır görünüm sunar.

## **create grayscale pdf** nedir?

Gri tonlamalı bir PDF oluşturmak, orijinal belgenin tüm görsel öğelerini gri tonlara dönüştürmek anlamına gelir. Sonuç, renk kaynaklı dikkat dağıtıcıları ortadan kaldıran ve içeriğin artık görüntü tabanlı olması nedeniyle hafif bir güvenlik faydası ekleyen daha küçük, baskıya uygun bir dosyadır.

## GroupDocs.Redaction ile gri tonlamalı rasterleştirme neden kullanılmalı?

Rasterleştirme, her sayfayı bir görüntüye dönüştürür; bu da metnin kopyalanamaması veya düzenlenememesi anlamına gelir ve görsel çıktı yazıcılar ve görüntüleyiciler arasında tutarlı kalır. GroupDocs.Redaction **100'den fazla giriş ve çıkış formatını** destekler — DOCX, XLSX, PPTX, HTML ve görüntü türleri dahil — böylece neredeyse her belgeye aynı iş akışını uygulayabilirsiniz.

## Önkoşullar

- Java Development Kit (JDK) 8 veya daha yeni. `java -version` komutuyla doğrulayın.  
- Kodlamayı ve hata ayıklamayı kolaylaştırmak için bir IDE (IntelliJ IDEA, Eclipse veya NetBeans).  
- Maven veya Gradle aracılığıyla eklenmiş GroupDocs.Redaction for Java.  
- Güvenle deneyebileceğiniz bir örnek belge (ör. çok sayfalı bir DOCX).  
- Rasterleştirilmiş çıktı için yeterli disk alanı (raster dosyaları kaynak dosyadan daha büyük olabilir).

## Paketleri İçe Aktar

Aşağıdaki içe aktarmalar, örnek için gerekli temel Redactor ve rasterleştirme sınıflarını getirir.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.options.RasterizationOptions;
import com.groupdocs.redaction.options.AdvancedRasterizationOptions;
```

## Adım 1: Redactor Nesnesini Başlat

`Redactor` sınıfı, GroupDocs.Redaction'daki tüm belge‑işleme işlemleri için giriş noktasıdır. Bir örnek oluşturmak, belgeleri yükleme, düzenleme ve kaydetme kapısını açar.

```java
final Redactor redactor = new Redactor(Constants.MULTIPAGE_SAMPLE_DOCX);
```

`Constants.MULTIPAGE_SAMPLE_DOCX` ifadesini gri tonlamalı PDF'ye dönüştürmek istediğiniz dosyanın yolu ile değiştirin.

## Adım 2: Kaydetme Seçeneklerini Yapılandır

`SaveOptions` sınıfı, işlenen belgenin diske nasıl yazılacağını, format ve dosya adı dahil, tanımlar.

```java
SaveOptions so = new SaveOptions();
so.setRedactedFileSuffix("_scan");
```

Çıktı `yourfile_scan.pdf` olarak adlandırılacak (veya daha sonra belirttiğiniz format).

## Adım 3: Rasterleştirmeyi Etkinleştir

`RasterizationOptions` nesnesi, kaydetmeden önce her sayfanın görüntü tabanlı oluşturulmasını sağlar.

```java
so.getRasterization().setEnabled(true);
```

## Adım 4: Gri Tonlama Dönüşümünü Uygula

`AdvancedRasterizationOptions.Grayscale` rasterleştirilmiş görüntünün yalnızca gri tonları kullanmasını zorlayan bir bayraktır.

```java
so.getRasterization().addAdvancedOption(AdvancedRasterizationOptions.Grayscale);
```

## Adım 5: Belge Dönüşümünü Gerçekleştir

`save()` çağrısı, tam işleme hattını çalıştırır ve çıktı dosyasını yazar.

```java
redactor.save(so);
```

Bu satır çalıştıktan sonra, tamamen rasterleştirilmiş, gri tonlamalı ve `_scan` ekiyle kaydedilmiş yeni bir dosyayı diskte bulacaksınız.

## Adım 6: Doğru Kaynak Yönetimi

`close()` metodu, yerel kaynakları serbest bırakır ve geçici dosyaları siler.

```java
finally { redactor.close(); }
```

Modern Java için, `Redactor`ı otomatik olarak kapatan try‑with‑resources desenini de kullanabilirsiniz:

```java
try (Redactor redactor = new Redactor(Constants.MULTIPAGE_SAMPLE_DOCX)) {
    // Your processing code here
}
// Automatic cleanup happens here
```

Her iki yaklaşım da güvenlidir; ikincisi daha özlüdür.

## Gelişmiş Yapılandırma Seçenekleri

### Kalite veya Boyut İçin DPI Ayarla

Daha yüksek DPI, daha keskin görüntüler sağlar (baskı için iyidir), düşük DPI ise dosya boyutunu azaltır. Yaygın bir denge, ekranda görüntüleme için 150 DPI ve baskıya hazır PDF'ler için 300 DPI'dir.

```java
saveOptions.getRasterization().setDpi(300); // High quality for printing
// or
saveOptions.getRasterization().setDpi(150); // Balanced quality and size
```

### Çıktı Formatı Seç

Rasterleştirilmiş sonucu PDF, TIFF veya PNG gibi belirli bir konteyner formatına zorlayabilirsiniz. PDF, en yaygın kullanılan arşiv formatıdır.

```java
saveOptions.setRasterizationFormat(RasterizationFormat.PDF);
```

## Yaygın Kullanım Senaryoları

- **Hukuki belge arşivleme** – düzenlenemeyen değiştirilemez gri tonlamalı PDF'ler oluşturun.  
- **Baskıya hazır raporlar** – toplu baskı için tutarlı siyah‑beyaz çıktı sağlayın.  
- **Uyumluluk iş akışları** – sıkı veri gizliliği düzenlemelerine uymak için kırpma ile gri tonlamalı rasterleştirmeyi birleştirin.

## Yaygın Sorunlar ve Çözümler

| Sorun | Neden Oluşur | Çözüm |
|-------|--------------|-------|
| Çıktı dosyası beklenenden büyük | DPI çok yüksek ayarlandı veya görüntü sıkıştırması devre dışı | DPI'yi düşürün (ör. 150) veya `RasterizationOptions` içinde sıkıştırmayı etkinleştirin. |
| Metin bulanık görünüyor | Orijinal yazı tipi boyutu için yetersiz DPI | DPI'yi 300 veya daha yüksek bir değere artırın. |
| İşlem büyük belgelerde `OutOfMemoryError` hatası verir | Tüm belge belleğe yükleniyor | Destekleniyorsa akış API'lerini kullanın veya sayfaları toplu işleyin. |
| Gri tonlama uygulanmadı | Gelişmiş seçenek doğru eklenmedi | `save()`'den önce `addAdvancedOption(AdvancedRasterizationOptions.Grayscale)` çağrıldığını doğrulayın. |

## Sıkça Sorulan Sorular

**Q: Belgeleri rasterleştirme olmadan gri tonlamaya dönüştürebilir miyim?**  
**A: GroupDocs.Redaction'da gri tonlama seçeneği rasterleştirmeye bağlıdır; bu, tutarlı sonuçlar sağlar ve bir güvenlik katmanı ekler.**

**Q: Hangi belge formatları gri tonlamalı rasterleştirmeyi destekliyor?**  
**A: GroupDocs.Redaction tarafından desteklenen tüm büyük formatlar — DOCX, PDF, XLSX, PPTX, RTF ve 100'den fazla diğer format — rasterleştirilebilir ve gri tonlamaya dönüştürülebilir.**

**Q: Rasterleştirme belgelerimin dosya boyutunu etkileyecek mi?**  
**A: Evet. Metin ağırlıklı dosyalar büyüyebilir, görüntü ağırlıklı dosyalar ise küçülebilir. DPI ayarları en büyük etkiye sahiptir.**

**Q: Gri tonlamalı rasterleştirme sürecini tersine çevirmek mümkün mü?**  
**A: Hayır. Rasterleştirme tek yönlüdür; geri dönmeniz gerekirse orijinali yedekleyin.**

**Q: Gri tonlamalı rasterleştirilmiş belgelerin kalitesini nasıl optimize edebilirim?**  
**A: Baskı kalitesi için daha yüksek DPI (300 +) kullanın ve en iyi arşiv sonuçları için PDF'yi çıktı formatı olarak seçin.**

## Sonuç

Artık GroupDocs.Redaction for Java kullanarak **PDF'yi gri tonlamaya rasterleştirmek** için eksiksiz, üretim‑hazır bir tarifiniz var. Rasterleştirmeyi etkinleştirerek, gri tonlama gelişmiş seçeneğini ekleyerek ve kaynakları sorumlu bir şekilde yöneterek, uyumluluk standartlarını karşılayan ve herhangi bir görüntüleyicide tutarlı görünen güvenli, baskıya uygun belgeler üretebilirsiniz.

---

**Son Güncelleme:** 2026-05-17  
**Test Edilen Versiyon:** GroupDocs.Redaction 23.11 for Java  
**Yazar:** GroupDocs  

## HEDEF ANAHTAR KELİMELER:

**Birincil Anahtar Kelime (EN YÜKSEK ÖNCELİK):**
how to rasterize pdf

**İkincil Anahtar Kelimeler (DESTEKLEYİCİ):**
java pdf to image, apply grayscale filter pdf

## İlgili Öğreticiler

- [GroupDocs.Redaction Java için Rasterleştirme Seçenekleri Öğreticileri](/redaction/java/rasterization-options/)
- [GroupDocs Redaction for Java nasıl kullanılır: Word Belgelerinde Ön‑Rasterleştirme](/redaction/java/rasterization-options/groupdocs-redaction-java-pre-rasterization-word-docs/)
- [Java'da Özel Gürültü Rasterleştirme: Hassas Bilgileri GroupDocs.Redaction ile Güvence Altına Alın](/redaction/java/rasterization-options/java-groupdocs-redaction-custom-noise-rasterization/)