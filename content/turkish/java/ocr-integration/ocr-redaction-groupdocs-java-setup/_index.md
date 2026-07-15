---
date: '2026-06-26'
description: GroupDocs OCR Redaction ve Azure OCR kullanarak tarama PDF'lerinden metin
  çıkarmayı ve hassas verileri maskeleme yöntemlerini öğrenin. Redact social security
  number ve gizli bilgileri PDF'de verimli bir şekilde değiştirin.
keywords:
- extract text scanned pdf
- redact social security number
- mask sensitive data pdf
- replace confidential info pdf
schemas:
- author: GroupDocs
  dateModified: '2026-06-26'
  description: Learn how to extract text scanned PDF and mask sensitive data using
    GroupDocs OCR Redaction with Azure OCR. Redact social security number and replace
    confidential info PDF efficiently.
  headline: Extract Text Scanned PDF – Mask Data with GroupDocs OCR
  type: TechArticle
- questions:
  - answer: OCR redaction uses Optical Character Recognition to extract hidden text
      from images or scanned PDFs, then applies redaction rules to mask that text.
    question: What is OCR redaction?
  - answer: Yes, but OCR dramatically improves accuracy on scanned documents where
      native text extraction fails.
    question: Can I use GroupDocs Redaction without Azure OCR?
  - answer: Build and test them incrementally, using Java’s `Pattern` class in a sandbox
      before applying to large documents.
    question: How do I handle complex regex patterns?
  - answer: Large PDFs, overly complex regex, and synchronous OCR calls can slow processing;
      consider batch processing and optimized patterns.
    question: What are typical performance bottlenecks?
  - answer: Absolutely—reach out via the [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33)
      for community help or contact GroupDocs support.
    question: Is support available for implementation issues?
  type: FAQPage
title: Tarama PDF'lerinden Metin Çıkar – GroupDocs OCR ile Verileri Maskele
type: docs
url: /tr/java/ocr-integration/ocr-redaction-groupdocs-java-setup/
weight: 1
---

# Taranmış PDF'den Metin Çıkarma – GroupDocs OCR ile Verileri Maskeleme

Bugünün veri odaklı dünyasında, **taranmış PDF** dosyalarından metin çıkarmak ve gizli bilgileri maskelemek, tartışmasız bir uyumluluk adımıdır. Bu öğretici, GroupDocs Redaction'ı Microsoft Azure OCR ile birlikte kullanarak taranmış sayfalardaki gizli metni güvenilir bir şekilde tanımanıza ve **`[REDACTED]`** gibi güvenli bir yer tutucu ile değiştirmenize yardımcı olur. Bu kombinasyonun neden hızlı, doğru ve üretim‑hazır iş yükleri için hazır olduğunu göreceksiniz.

## Hızlı Yanıtlar
- **“mask sensitive data” ne anlama geliyor?** Belirlenen gizli metni bir yer tutucu ile değiştirir (ör. `[REDACTED]`).  
- **Hangi kütüphane OCR'ı yönetir?** Microsoft Azure OCR bağlayıcısı, GroupDocs Redaction aracılığıyla kullanılır.  
- **Bir lisansa ihtiyacım var mı?** Değerlendirme için ücretsiz deneme çalışır; üretim için kalıcı bir lisans gereklidir.  
- **Taranmış PDF'leri kırpabilir miyim?** Evet—OCR, regex kırpmaları uygulamadan önce gizli metni çıkarır.  
- **Bu çözüm sadece Java mı?** Örnek Java tabanlıdır, ancak GroupDocs .NET ve diğer platformlar için benzer API'ler sunar.

## OCR‑Tabanlı Kırpma Nedir?
OCR‑Tabanlı Kırpma, önce her sayfada OCR çalıştırarak görüntüleri aranabilir metne dönüştürür, ardından regex desenlerini uygulayarak eşleşmeleri `[REDACTED]` gibi bir maske ile değiştirir. Bu iki adımlı süreç, taranmış PDF'lerde bile kişisel verileri güvenilir bir şekilde gizlemenizi sağlar ve belge paylaşılmadan veya arşivlenmeden önce tüm hassas dizelerin kaldırıldığından emin olur.

## Neden GroupDocs Redaction'ı Azure OCR ile Kullanmalısınız?
GroupDocs Redaction'ı Azure OCR ile kullanmalısınız çünkü **baskı metinlerinde >%98 OCR doğruluğu** sağlar, **50+ giriş ve çıkış formatını** destekler ve **tüm dosyayı belleğe yüklemeden çok sayfalı PDF'leri** işleyebilir, bu da uyumluluk için hızlı ve ölçeklenebilir kırpma sağlar. Çözüm ayrıca **8 çekirdekli bir sunucuda 1.000 sayfalık PDF'yi 2 dakikadan kısa sürede işleyebilecek** şekilde ölçeklenir, bu da toplu işler için pratiktir.

## Önkoşullar
- **Java Development Kit (JDK) 8+** yüklü.  
- **Maven** (bağımlılık yönetimini tercih ediyorsanız) veya JAR'ları manuel olarak indirme yeteneği.  
- **Microsoft Azure OCR kimlik bilgileri** (uç nokta ve abonelik anahtarı).  
- Temel Java bilgisi ve düzenli ifadelerle (regex) aşinalık.

## Java için GroupDocs Redaction Kurulumu

### Maven Kurulumu
`pom.xml` dosyanıza GroupDocs deposunu ve bağımlılığı ekleyin:

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
Manuel JAR yönetimini tercih ediyorsanız, en son sürümü [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) adresinden alın.

### Lisans Edinme
- **Ücretsiz Deneme** – tüm özellikleri ücretsiz keşfedin.  
- **Geçici Lisans** – değerlendirme süresini uzatın.  
- **Tam Lisans** – üretim‑hazır yeteneklerin kilidini açın.

### Temel Başlatma ve Kurulum
`Redactor` sınıfı, OCR çıkarımı yapan ve PDF belgelerine kırpma kurallarını uygulayan temel motorudur.  
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.RedactorSettings;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.examples.java.helper_classes.MicrosoftAzureOcrConnector;

// Initialize the OCR connector with Microsoft Azure
RedactorSettings settings = new RedactorSettings(new MicrosoftAzureOcrConnector());
```

## OCR Kırpma ile Hassas Verileri Nasıl Maskeleyebilirsiniz
OCR Kırpma ile hassas verileri maskelemek, PDF'yi Azure OCR ayarlarıyla yüklemeyi, gizlemek istediğiniz veri için regex desenlerini tanımlamayı ve Redactor'ı her eşleşmeyi `[REDACTED]` gibi bir yer tutucu ile değiştirmek için çağırmayı içerir. Kütüphane, OCR, desen eşleştirme ve PDF yeniden yazımını tek bir iş akışında yönetir.

### Adım 1: Belgeyi OCR Ayarlarıyla Yükleyin
`LoadOptions`, GroupDocs'un bir dosyayı nasıl yükleyeceğini yapılandırır ve Azure gibi OCR bağlayıcılarını geçirmenize olanak tanır.  
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;

// Load your document with OCR settings
try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf", 
    new LoadOptions(), settings)) {
    // Further operations will go here
}
```
- **`YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf`** – PDF'nizin yoluyla değiştirin.  
- **`settings`** – daha önce oluşturduğunuz Azure OCR bağlayıcısını içerir.

### Adım 2: Regex Kırpmalarını Tanımlayın ve Uygulayın
`ReplacementOptions`, kırpma sırasında her regex eşleşmesini değiştirecek yedek metni belirler.  
```java
import com.groupdocs.redaction.redactions.RegexRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

// Define the regex for sensitive data (e.g., Social Security Numbers)
RegexRedaction redaction = new RegexRedaction("\\b\\d{3}-\\d{2}-\\d{4}\\b", 
    new ReplacementOptions("[REDACTED]"));

// Apply redaction
redactor.apply(redaction);

// Save the document after redactions
redactor.save(new SaveOptions());
```
- `\b\d{3}-\d{2}-\d{4}\b` deseni, ABD Sosyal Güvenlik Numaralarını eşleştirir.  
- `ReplacementOptions("[REDACTED]")` her eşleşmeyi maske ile değiştirir, etkili bir şekilde **hassas verileri maskeleme** sağlar.

## Hassas Verileri Maskeleme İçin Yaygın Kullanım Senaryoları
1. **Hukuki Belge Yönetimi** – taslakları paylaşmadan önce müşteri kimlik bilgilerini gizleyin.  
2. **Finansal Raporlama** – hesap numaralarını ve işlem kimliklerini koruyun.  
3. **Sağlık Kayıtları** – HIPAA'ya uyum sağlamak için hasta kimlik bilgilerini kırpın.  
4. **Kamu Yayınları** – kamu kayıtlarından kişisel verileri kaldırın.  
5. **Kurumsal Sözleşmeler** – dış incelemeler sırasında özel şartları gizleyin.

## Performans İpuçları
- **Regex'i optimize edin** – işlem süresini artıran çok geniş desenlerden kaçının; iyi tasarlanmış ifadeler çalışma süresini %40'a kadar azaltabilir.  
- **Bellek Yönetimi** – `Redactor` örneğini hızlıca kapatın (try‑with‑resources bunu otomatik yapar).  
- **Asenkron Çalıştırma** – toplu işlem için kırpma işlerini ayrı iş parçacıklarında çalıştırın veya UI'nin yanıt vermesini sağlamak için bir görev kuyruğu kullanın.

## Sorun Giderme
- **Azure kimlik bilgileri hatası** – `MicrosoftAzureOcrConnector` içinde uç nokta URL'sini ve abonelik anahtarını iki kez kontrol edin.  
- **Belge yüklenmıyor** – dosya yolunu doğrulayın ve PDF'nin şifre korumalı olmadığından emin olun (veya şifreyi `LoadOptions` ile sağlayın).  
- **Kırpma uygulanmadı** – regex'inizi önce basit bir dizeyle test edin; eşleşmeleri doğrulamak için bir birim testte `Pattern.compile` kullanın.

## Sıkça Sorulan Sorular

**S: OCR kırpması nedir?**  
C: OCR kırpması, Görüntü Tanıma (Optical Character Recognition) kullanarak görüntülerden veya taranmış PDF'lerden gizli metni çıkarır, ardından bu metni maskelemek için kırpma kurallarını uygular.

**S: Azure OCR olmadan GroupDocs Redaction kullanabilir miyim?**  
C: Evet, ancak OCR, yerel metin çıkarımının başarısız olduğu taranmış belgelerde doğruluğu büyük ölçüde artırır.

**S: Karmaşık regex desenlerini nasıl yönetirim?**  
C: Desenleri adım adım oluşturup test edin, büyük belgelere uygulamadan önce bir sandbox'ta Java’nın `Pattern` sınıfını kullanın.

**S: Tipik performans darboğazları nelerdir?**  
C: Büyük PDF'ler, aşırı karmaşık regex'ler ve senkron OCR çağrıları işlemi yavaşlatabilir; toplu işleme ve optimize edilmiş desenleri düşünün.

**S: Uygulama sorunları için destek mevcut mu?**  
C: Kesinlikle—topluluk yardımı için [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33) üzerinden iletişime geçin veya GroupDocs desteğiyle irtibata geçin.

## Ek Kaynaklar
- **Dokümantasyon**: https://docs.groupdocs.com/redaction/java/  
- **API Referansı**: https://reference.groupdocs.com/redaction/java  
- **İndirme**: https://releases.groupdocs.com/redaction/java/  
- **GitHub**: https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java  
- **Ücretsiz Destek**: https://forum.groupdocs.com/c/redaction/33  
- **Geçici Lisans**: https://purchase.groupdocs.com/temporary-license/

---

**Son Güncelleme:** 2026-06-26  
**Test Edilen Versiyon:** GroupDocs.Redaction 24.9 (Java)  
**Yazar:** GroupDocs  

## İlgili Öğreticiler

- [OCR Kullanarak Güvenli PDF Kırpma – GroupDocs.Redaction Java](/redaction/java/ocr-integration/)
- [GroupDocs.Redaction for Java ile Metin Kırpma](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction/)
- [Java’da Hassas Verileri Maskele – GroupDocs.Redaction ile Kişisel Bilgileri Kırpma](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)