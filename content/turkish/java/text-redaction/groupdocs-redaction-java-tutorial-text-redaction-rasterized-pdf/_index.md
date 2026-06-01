---
date: '2026-02-26'
description: GroupDocs.Redaction Java kullanarak metni nasıl karartacağınızı öğrenin
  ve tam ifade değişimi ile özel PDF ayarlarıyla rasterleştirilmiş PDF olarak kaydedin.
keywords:
- GroupDocs.Redaction Java
- text redaction Java
- rasterized PDF conversion
title: GroupDocs.Redaction Java ile Metni Kırpma
type: docs
url: /tr/java/text-redaction/groupdocs-redaction-java-tutorial-text-redaction-rasterized-pdf/
weight: 1
---

# GroupDocs.Redaction Java ile Metin Nasıl Kırpılır

Günümüzün veri odaklı dünyasında, bir belgede **metni nasıl kırpılır** güvenli ve verimli bir şekilde, geliştiriciler ve uyumluluk sorumluları için en önemli konulardan biridir. Kişisel tanımlayıcıları, gizli müşteri detaylarını veya dahili proje kodlarını gizlemeniz gerekse, GroupDocs.Redaction for Java, kesin ifadeleri bulup güvenli kaplamalarla değiştirmek için güvenilir bir yol sunar. Bu öğreticide ayrıca **rasterleştirilmiş PDF olarak nasıl kaydedilir** gösterilir; her sayfayı arşiv standartlarına uygun bir görüntü‑tabanlı PDF'ye dönüştürür.

## Hızlı Yanıtlar
- **Kırpma için birincil sınıf nedir?** `Redactor`  
- **Bir ifadeyi renkli bir kaplamayla değiştirebilir miyim?** Evet, `ExactPhraseRedaction` ve `ReplacementOptions` kullanarak.  
- **Rasterleştirilmiş bir PDF nasıl oluşturulur?** `SaveOptions.getRasterization().setEnabled(true)` ile rasterleştirme etkinleştirilir.  
- **Örnekte hangi PDF uyumluluk seviyesi kullanılıyor?** `PdfComplianceLevel.PdfA1a`.  
- **Üretim kullanımında lisansa ihtiyacım var mı?** Üretim dağıtımları için geçerli bir GroupDocs.Redaction lisansı gereklidir.

## Java’da “metni nasıl kırpılır” nedir?
Kırpma, bir dosyadan hassas içeriği kalıcı olarak kaldırma veya gizleme sürecidir. GroupDocs.Redaction ile, bir isim veya kimlik gibi kesin bir ifadeyi programlı olarak arayabilir ve kırmızı bir kaplama, siyah bir kutu veya herhangi bir özel görsel öğe ile değiştirebilirsiniz; böylece orijinal verinin kopyala‑yapıştır veya OCR ile geri alınması mümkün olmaz.

## Neden GroupDocs.Redaction for Java Kullanılmalı?
- **Kesin ifade eşleşmesi** yanlış pozitifleri ortadan kaldırır.  
- **Yerleşik rasterleştirme** uzun vadeli depolama için PDF/A uyumlu, yalnızca görüntü içeren PDF'ler oluşturmanızı sağlar.  
- **Çapraz format desteği** DOCX, PDF, PPTX ve daha fazlası ile çalışır, böylece aynı kodu farklı belge tiplerinde uygulayabilirsiniz.  
- **Performansa odaklı API** büyük belge setlerini toplu işleyebilmenizi sağlar ve bellek kullanımını düşük tutar.

## Önkoşullar
İçeriğe başlamadan önce aşağıdakilere sahip olduğunuzdan emin olun:

- **GroupDocs.Redaction for Java** (v24.9 veya daha yeni).  
- **Java Development Kit (JDK) 8+**.  
- IntelliJ IDEA, Eclipse veya NetBeans gibi bir IDE.  
- Bağımlılık yönetimi için Maven.

### Gerekli Kütüphaneler ve Bağımlılıklar
- **GroupDocs.Redaction for Java** – depo ve bağımlılığı `pom.xml` dosyanıza ekleyin (aşağıdaki kod bloğuna bakın).  
- **İsteğe bağlı**: Tercih ettiğiniz ek günlükleme kütüphaneleri.

### Bilgi Önkoşulları
- Temel Java sözdizimi ve dosya G/Ç.  
- Maven'in `pom.xml` yapısına aşinalık.

## GroupDocs.Redaction for Java Kurulumu
### Maven Kurulumu
`pom.xml` dosyanıza depo ve bağımlılığı ekleyin:

```xml
<repositories>
   <repository>
      <id>repository.groupdocs.com</id>
      <name>GroupDocs Repository</name>
      <url>https://releases.groupdocs.com/redaction/java/</url>
   </repository>
</repositories>

<dependencies>
   <dependency>
      <groupId>com.groupdocs</groupId>
      <artifactId>groupdocs-redaction</artifactId>
      <version>24.9</version>
   </dependency>
</dependencies>
```

### Doğrudan İndirme
Alternatif olarak, en son sürümü doğrudan [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) adresinden indirebilirsiniz.

### Lisans Edinimi
- **Ücretsiz Deneme** – lisans anahtarı olmadan API'yi keşfedin.  
- **Geçici Lisans** – uzun süreli değerlendirme için kullanın.  
- **Tam Lisans** – üretim ortamları için gereklidir.

### Temel Başlatma ve Kurulum
Aşağıda örnek bir DOCX dosyasına işaret eden bir `Redactor` örneği oluşturmak için en temel kod yer almaktadır:

```java
import com.groupdocs.redaction.Redactor;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
```

## Metni Kırpma – Kesin İfade Örneği
### Adım 1: Gerekli Sınıfları İçe Aktarın
Bu içe aktarmalar, kırpma motoru ve değiştirme seçeneklerine erişmenizi sağlar:

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.ReplacementOptions;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
```

### Adım 2: Kırpmayı Oluşturun ve Uygulayın
Aşağıdaki kod parçacığı **“John Doe”** ifadesini arar ve kırmızı bir kaplama ile değiştirir:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
try {
    RedactorChangeLog result = redactor.apply(new ExactPhraseRedaction(
        "John Doe", new ReplacementOptions(java.awt.Color.RED)));
    
    if (result.getStatus() != RedactionStatus.Failed) {
        // Successfully redacted the text
    }
} finally { 
    redactor.close(); 
}
```

**Neden önemli:** `ReplacementOptions` kırpmanın görsel stilini kontrol etmenizi sağlar, gizli içeriğin kopyala‑yapıştır veya OCR ile geri alınamamasını temin eder.

## Rasterleştirilmiş PDF Olarak Kaydetme
### Adım 1: SaveOptions Sınıflarını İçe Aktarın
Bu sınıflar PDF çıktısını yapılandırmanıza olanak tanır; rasterleştirme ve uyumluluk seviyeleri dahil.

```java
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.options.PdfComplianceLevel;
```

### Adım 2: Kaydetme Seçeneklerini Yapılandırın ve Uygulayın
Kırpma işleminden sonra belgeyi rasterleştirilmiş bir PDF olarak dışa aktarabilirsiniz. Aşağıdaki örnek yalnızca 5. sayfayı rasterleştirir ve PDF/A‑1a uyumluluğunu zorlar:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
try {
    SaveOptions options = new SaveOptions();

    // Enable rasterization for converting pages into images.
    options.getRasterization().setEnabled(true);
    
    // Set the starting page and count for rasterization.
    options.getRasterization().setPageIndex(5);
    options.getRasterization().setPageCount(1);

    // Define PDF compliance level.
    options.getRasterization().setCompliance(PdfComplianceLevel.PdfA1a);

    // Append a suffix to avoid filename conflicts.
    options.setAddSuffix(true);

    // Save the document with these configurations.
    redactor.save(options);
} finally { 
    redactor.close(); 
}
```

**Ana nokta:** Bir PDF'i rasterleştirmek **her sayfayı bir görüntüye dönüştürür**, gizli metin katmanlarını kaldırır ve belgeyi müdahaleye karşı dayanıklı hâle getirir—hukuki arşivleme için idealdir.

## Pratik Uygulamalar
1. **Hassas Veri Kırpma** – Sözleşmeleri paylaşmadan önce kişisel tanımlayıcıları otomatik olarak gizler.  
2. **Belge Arşivleme** – Tamamlanmış raporları uzun vadeli uyumluluk için rasterleştirilmiş PDF/A'ya dönüştürür.  
3. **Toplu İçerik Güncelleme** – Yüzlerce dosyada eski terminolojiyi tek bir betikle değiştirir.

## Performans Düşünceleri
- **Her işlem sonrası `Redactor`'ı kapatın** dosya tutamaçlarını ve belleği serbest bırakmak için.  
- **Toplu İşleme** – Dosya listesini yükleyin ve döngüyle işleyin, mümkün olduğunda tek bir `Redactor` örneğini yeniden kullanın.  
- **Kaynakları İzleme** – Büyük ölçekli kırpma işlemleri sırasında CPU ve yığın kullanımını izlemek için Java profil araçlarını kullanın.

## Sık Sorulan Sorular

**S: Maven projesine GroupDocs.Redaction nasıl kurulur?**  
C: Maven Kurulumu bölümünde gösterildiği gibi GroupDocs deposunu ve `groupdocs-redaction` bağımlılığını `pom.xml` dosyanıza ekleyin.

**S: Bu kütüphane ile PDF dosyalarından metin kırpabilir miyim?**  
C: Evet, GroupDocs.Redaction PDF, DOCX, PPTX ve birçok diğer formatı destekler.

**S: Kesin ifade bulunamazsa ne olur?**  
C: `RedactorChangeLog` `Failed` durumunu döndürür. İfadenin yazımını ve büyük/küçük harf duyarlılığını kontrol edin.

**S: Çok büyük belgeleri verimli bir şekilde nasıl yönetebilirim?**  
C: Belgeleri daha küçük sayfa aralıklarında işleyin, rasterleştirmeyi yalnızca gerektiğinde etkinleştirin ve her zaman `Redactor`'ı kapatarak kaynakları serbest bırakın.

**S: Rasterleştirilmiş PDF'leri belirli sayfa aralıklarıyla kaydetmek mümkün mü?**  
C: Kesinlikle. Rasterleştirmek istediğiniz sayfaları hedeflemek için `options.getRasterization().setPageIndex()` ve `setPageCount()` kullanın.

## Sonuç
Artık GroupDocs.Redaction Java ile **metni nasıl kırpılır** ve **rasterleştirilmiş PDF olarak nasıl kaydedilir** konusunda eksiksiz, uçtan uca bir rehbere sahipsiniz. Bu adımları izleyerek hassas bilgileri koruyabilir, uyumluluk gereksinimlerini karşılayabilir ve üretim ortamlarında yüksek performansı sürdürebilirsiniz.

**Sonraki Adımlar**  
- API'yi daha derinlemesine keşfetmek için [resmi dokümantasyonu](https://docs.groupdocs.com/redaction/java/) inceleyin.  
- Diğer kırpma türleriyle (ör. `RegexRedaction`, `ImageRedaction`) deney yapın.  
- İpuçları ve en iyi uygulamalar için [GroupDocs Destek Forumuna](https://forum.groupdocs.com/c/redaction/33) katılın.

---

**Last Updated:** 2026-02-26  
**Tested With:** GroupDocs.Redaction Java 24.9  
**Author:** GroupDocs