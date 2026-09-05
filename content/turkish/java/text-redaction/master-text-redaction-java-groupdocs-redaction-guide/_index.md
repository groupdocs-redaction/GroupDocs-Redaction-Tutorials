---
date: '2026-08-20'
description: Java'da GroupDocs.Redaction ile regex kullanarak metni nasıl kırpacağınızı
  keşfedin. Bu adım adım öğretici, regex'i nasıl uygulayacağınızı, save options'ı
  nasıl yapılandıracağınızı ve sensitive data'yı nasıl koruyacağınızı gösterir.
keywords:
- how to redact text
- mask credit card numbers
- remove social security numbers
- redact pdf java
lastmod: '2026-08-20'
og_description: Java'da GroupDocs.Redaction kullanarak metni nasıl kırpacağınızı öğrenin.
  Bu rehber, regex kırpma, save‑option yapılandırması ve sensitive data'yı korumak
  için performance tips'i açıklar.
og_image_alt: Guide showing Java code to redact text using GroupDocs.Redaction
og_title: Java'da GroupDocs.Redaction ile Metin Kırpma
schemas:
- author: GroupDocs
  dateModified: '2026-08-20'
  description: Discover how to redact text using regex in Java with GroupDocs.Redaction.
    This step‑by‑step tutorial shows you how to apply regex, configure save options,
    and protect sensitive data.
  headline: 'How to redact text in Java with GroupDocs.Redaction: A complete guide'
  type: TechArticle
- description: Discover how to redact text using regex in Java with GroupDocs.Redaction.
    This step‑by‑step tutorial shows you how to apply regex, configure save options,
    and protect sensitive data.
  name: 'How to redact text in Java with GroupDocs.Redaction: A complete guide'
  steps:
  - name: import required classes
    text: 'The following imports give you access to the redaction API:'
  - name: initialize redactor and apply regex pattern
    text: '`RegexRedaction` represents a redaction rule based on a regular‑expression
      pattern. The pattern you provide determines which text fragments are replaced.
      - **Regex explanation**: The pattern `\b\d{3}-\d{2}-\d{4}\b` matches U.S. Social
      Security numbers (three digits, a dash, two digits, a dash, four '
  - name: configure save options
    text: '`SaveOptions` controls how the redacted file is written. Adding a suffix
      makes it clear which files have been processed, while preserving the original
      format avoids unwanted conversion. - **Save options**: `setAddSuffix(true)`
      automatically appends “_redacted” to the output filename, preventing acci'
  - name: customize additional save settings
    text: 'You can further tailor the output—such as preserving metadata or flattening
      annotations—by adjusting the `SaveOptions` object. - **Key configuration**:
      Setting `setPreserveMetadata(true)` retains original document properties, which
      is often required for compliance audits.'
  type: HowTo
- questions:
  - answer: It automatically appends a suffix (e.g., `_redacted`) to the output filename,
      making it obvious which files have been processed.
    question: What is the purpose of `setAddSuffix(true)` in SaveOptions?
  - answer: Absolutely. Any valid Java regular expression can be supplied to `RegexRedaction`
      to target emails, phone numbers, custom IDs, etc.
    question: Can I use regex patterns other than numbers for text redaction?
  - answer: Wrap the redaction logic in a try‑catch block, log the exception, and
      always close the `Redactor` in a finally clause to release resources.
    question: How should I handle errors during redaction?
  - answer: Yes. GroupDocs.Redaction works with PDF, DOCX, PPTX, and many other formats.
    question: Is PDF redaction supported?
  - answer: Use batch processing, keep regex patterns simple, and monitor memory usage
      with profiling tools.
    question: What are best practices for large‑scale redaction projects?
  type: FAQPage
tags:
- text redaction
- GroupDocs.Redaction
- Java document processing
- regex redaction
- PDF redaction
title: 'Java''da GroupDocs.Redaction ile Metin Kırpma: Tam Bir Rehber'
type: docs
url: /tr/java/text-redaction/master-text-redaction-java-groupdocs-redaction-guide/
weight: 1
---

# Java ile GroupDocs.Redaction'da metin nasıl karalanır: Tam bir rehber

Bugünün hızlı hareket eden dijital dünyasında, **metni nasıl karalanır** sorusu birçok geliştiricinin karşılaştığı bir konudur. Kişisel verileri koruyor, düzenlemelere uyuyor ya da sadece taslakları temizliyor olun, bu rehber GroupDocs.Redaction for Java’yı kullanarak **regex tabanlı karalamayı hızlı ve güvenli bir şekilde uygulayın**. Karalamanın neden önemli olduğunu, kütüphaneyi nasıl yapılandıracağınızı ve yüksek performanslı işleme için en iyi uygulama ipuçlarını öğreneceksiniz.

## Hızlı cevaplar
- **GroupDocs.Redaction'ın birincil amacı nedir?** Bu, 50'den fazla belge formatında hassas metni bulmak ve maskelemek için güvenilir bir API sağlar.  
- **Karalama için regex nasıl uygularım?** Deseninizi içeren bir `RegexRedaction` nesnesi oluşturun ve bunu `Redactor.apply()` metoduna geçirin.  
- **Lisans gerekir mi?** Ücretsiz deneme geliştirme için çalışır; ücretli lisans üretim için tam özellikleri açar.  
- **PDF'leri de DOCX dosyaları gibi karalayabilir miyim?** Evet—GroupDocs.Redaction PDF, DOCX, PPTX ve birçok diğer formatı destekler.  
- **Performansı artırmanın en iyi yolu nedir?** `Redactor` örneklerini hızlıca kapatın, regex desenlerini basit tutun ve dosyaları toplu işleyin.

## Metin karalaması nedir ve neden önemlidir?
Metin karalaması, bir belgeden hassas bilgileri kalıcı olarak kaldırır veya gizler; böylece sosyal güvenlik numaraları, kredi kartı detayları veya tıbbi kayıtlar gibi gizli veriler yetkisiz kişiler tarafından geri alınamaz veya görüntülenemez. Orijinal karakterlerin üzerine yazarak ya da bir maske ile değiştirerek çalışır, bu sayede gizli içerik kopyala‑yapıştır ya da OCR araçlarıyla çıkarılamaz. Bu, gizlilik düzenlemelerine uyumu sağlar ve bireyleri kimlik hırsızlığı ya da veri ihlallerinden korur.

## Metin karalaması için regex neden kullanılır?
Düzenli ifadeler, telefon numaraları, kredi kartı numaraları gibi çeşitli veri formatlarını eşleştiren esnek desenler tanımlamanıza olanak verir. GroupDocs.Redaction ile regex kullanmak, neyin gizleneceği üzerinde kesin kontrol sağlar ve uygulamayı kısa ve sürdürülebilir tutar.

## Önkoşullar
- **Java Development Kit (JDK)** yüklü (Java 8 veya daha yeni).  
- Java sözdizimi ve düzenli ifadeler konusunda temel bilgi.  
- **IntelliJ IDEA** veya **Eclipse** gibi bir IDE, kodu çalıştırmak ve hata ayıklamak için.  

## Java için GroupDocs.Redaction'ı Kurma
İlk olarak, kütüphaneyi projenize ekleyin.

### Maven kurulumu
Maven kullanıyorsanız, aşağıdakileri `pom.xml` dosyanıza ekleyin:

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

### Doğrudan indirme
Alternatif olarak, en son JAR dosyasını [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) adresinden indirin.

### Temel başlatma
`Redactor` bir belgeyi açan, karalama kurallarını uygulayan ve çıktıyı yazan temel sınıftır.

Kütüphane kullanılabilir olduğunda, belgeleri karalamaya başlayabilirsiniz:

```java
// Import the necessary classes from GroupDocs.Redaction
import com.groupdocs.redaction.Redactor;

public class RedactionExample {
    public static void main(String[] args) {
        // Initialize the redactor with your document path
        final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
        // Ensure you close resources after operations
        try { /* Your code here */ } finally { redactor.close(); }
    }
}
```

## Java'da regex kullanarak metni nasıl karalarsınız?
Bu işlem, kaynak dosyayı bir `Redactor` örneğine yüklemeyi, eşleşecek deseni tanımlayan bir `RegexRedaction` kuralı oluşturmayı, kuralı `redactor.apply()` ile uygulamayı ve son olarak değiştirilmiş belgeyi `SaveOptions` kullanarak kaydetmeyi içerir. Bu adımları izleyerek, desteklenen tüm formatlarda hassas dizeleri güvenilir bir şekilde bulabilir ve maskeleyebilirsiniz.

`Redactor` sınıfı, bir belgeyi açan, karalama kurallarını uygulayan ve çıktı dosyasını yazan çekirdek bileşendir. Kaynakları dahili olarak yönetir, bu yüzden işlem sonrası belleği serbest bırakmak için kapatmanız gerekir.

### Adım 1: Gerekli sınıfları içe aktarın
Aşağıdaki içe aktarmalar, karalama API'sine erişim sağlar:

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.redactions.RegexRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;
```

### Adım 2: Redactor'ı başlatın ve regex desenini uygulayın
`RegexRedaction`, düzenli ifade desenine dayalı bir karalama kuralını temsil eder. Sağladığınız desen, hangi metin parçalarının değiştirileceğini belirler.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
try {
    // Define a regex pattern to find sequences of numbers and apply a replacement color.
    // The pattern: Two digits, optional whitespace, two more digits, non-digit characters,
    // followed by six digits.
    redactor.apply(new RegexRedaction("\\d{2}\\s*\\d{2}[^\\d]*\\d{6}", 
        new ReplacementOptions(java.awt.Color.BLUE)));
```

- **Regex açıklaması**: `\b\d{3}-\d{2}-\d{4}\b` deseni ABD Sosyal Güvenlik numaralarını (üç rakam, bir tire, iki rakam, bir tire, dört rakam) eşleştirir. `ReplacementOptions` size katı siyah bir örtü ya da özel bir metin maskesi seçme imkanı verir.

### Adım 3: Kaydetme seçeneklerini yapılandırın
`SaveOptions`, karalanmış dosyanın nasıl yazılacağını kontrol eder. Bir sonek eklemek, hangi dosyaların işlendiğini netleştirirken, orijinal formatı korumak istenmeyen dönüşümleri önler.

```java
    // Configure save options
    SaveOptions saveOptions = new SaveOptions();
    saveOptions.setAddSuffix(true);  // Adds suffix to indicate processing
    saveOptions.setRasterizeToPDF(false);  // Preserves original format

    // Save the redacted document
    redactor.save(saveOptions);
} finally {
    redactor.close();  // Always close resources to prevent memory leaks
}
```

- **Kaydetme seçenekleri**: `setAddSuffix(true)` çıktının dosya adına otomatik olarak “_redacted” ekler, yanlışlıkla üzerine yazılmasını önler.

### Adım 4: Ek kaydetme ayarlarını özelleştirin
`SaveOptions` nesnesini ayarlayarak çıktıyı daha da özelleştirebilirsiniz—örneğin meta verileri korumak ya da ek açıklamaları düzleştirmek gibi.

```java
import com.groupdocs.redaction.options.SaveOptions;

SaveOptions saveOptions = new SaveOptions();
saveOptions.setAddSuffix(true);  // Indicates processing by adding a suffix
saveOptions.setRasterizeToPDF(false);  // Keeps original format intact
```

- **Ana yapılandırma**: `setPreserveMetadata(true)` ayarı, orijinal belge özelliklerini korur; bu genellikle uyumluluk denetimleri için gereklidir.

## Pratik uygulamalar
Metin karalamayı **nasıl yapacağınız**ın kritik olduğu gerçek dünya senaryoları:

1. **Hukuki belgeler** – Taslakları dış avukata paylaşmadan önce müşteri kimlik bilgilerini gizleyin.  
2. **Tıbbi kayıtlar** – Hasta adlarını, kimliklerini veya sağlık numaralarını maskelerek HIPAA uyumluluğunu sağlayın.  
3. **Finansal raporlar** – Çeyrek özetlerini dağıtırken gizli hesap numaralarını kaldırın.  

## Performans değerlendirmeleri
- **Bellek yönetimi**: Dosya tutamaçlarını ve yerel kaynakları serbest bırakmak için her zaman `redactor.close()` çağırın.  
- **Verimli regex**: Daha basit desenler daha hızlı çalışır; mümkün olduğunda atomik gruplar kullanarak aşırı geri izlemeyi önleyin.  
- **Toplu işleme**: Büyük belge setleri için, yığın kullanımını öngörülebilir tutmak amacıyla dosyaları 20–50 arası gruplar halinde işleyin.

## Yaygın sorunlar ve çözümler
| Sorun | Çözüm |
|-------|----------|
| **Regex çok fazla eşleşiyor** | Deseninizi çevrimiçi bir regex test cihazı ile test edin ve karakter sınıflarını daraltın. |
| **Çıktı dosya adı çakışması** | `setAddSuffix(true)` kullanın veya `saveOptions.setOutputPath()` ile özel bir çıktı yolu sağlayın. |
| **Büyük PDF'lerde bellek sızıntısı** | PDF'leri sayfa sayfa işleyin veya JVM yığın boyutunu artırın (`-Xmx2g`). |

## Sıkça sorulan sorular

**S: SaveOptions içinde `setAddSuffix(true)` amacının ne olduğu?**  
C: Çıktı dosya adına otomatik olarak bir sonek (ör. `_redacted`) ekler, hangi dosyaların işlendiğini açıkça gösterir.

**S: Metin karalaması için sayı dışındaki regex desenlerini kullanabilir miyim?**  
C: Kesinlikle. `RegexRedaction`a e-posta, telefon numarası, özel kimlik gibi herhangi bir geçerli Java düzenli ifadesi sağlayabilirsiniz.

**S: Karalama sırasında hataları nasıl yönetmeliyim?**  
C: Karalama mantığını bir try‑catch bloğuna sarın, istisnayı kaydedin ve her zaman `Redactor`ı finally bloğunda kapatarak kaynakları serbest bırakın.

**S: PDF karalama destekleniyor mu?**  
C: Evet. GroupDocs.Redaction PDF, DOCX, PPTX ve birçok diğer formatla çalışır.

**S: Büyük ölçekli karalama projeleri için en iyi uygulamalar nelerdir?**  
C: Toplu işleme kullanın, regex desenlerini basit tutun ve bellek kullanımını profil araçlarıyla izleyin.

## Ek kaynaklar
- **Dokümantasyon**: [GroupDocs Redaction Documentation](https://docs.groupdocs.com/redaction/java/)  
- **API referansı**: [GroupDocs API Reference](https://apireference.groupdocs.com/redaction/java)

---

**Son Güncelleme:** 2026-08-20  
**Test Edilen Versiyon:** GroupDocs.Redaction 24.9 for Java  
**Yazar:** GroupDocs

## İlgili Eğitimler

- [Hassas Verileri Maskele Java – GroupDocs.Redaction Rehberi](/redaction/java/getting-started/)
- [Hassas Verileri Maskele Java – GroupDocs.Redaction ile Kişisel Bilgileri Karala](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)
- [Aspose OCR ve Java ile PDF Nasıl Karalanır - GroupDocs.Redaction Kullanarak Regex Desenlerini Uygulama](/redaction/java/ocr-integration/aspose-ocr-java-pdf-redaction/)