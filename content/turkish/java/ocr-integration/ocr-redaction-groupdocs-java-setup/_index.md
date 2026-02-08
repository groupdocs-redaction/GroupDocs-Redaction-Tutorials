---
date: '2026-02-08'
description: GroupDocs OCR Redaction'ı Microsoft Azure OCR ile kullanarak hassas verileri
  nasıl maskeleyeceğinizi ve PDF Java dosyalarını nasıl kırpacağınızı öğrenin.
keywords:
- OCR-based redactions Java
- GroupDocs Redaction setup
- regex-based text redaction
title: GroupDocs OCR Redaction ile PDF'lerde Hassas Verileri Maskele
type: docs
url: /tr/java/ocr-integration/ocr-redaction-groupdocs-java-setup/
weight: 1
---

# PDF'lerde Hassas Verileri Maskeleme için GroupDocs OCR Redaction

Günümüz dijital ortamında, kişisel ve gizli bilgileri korumak en önemli önceliktir. Bu öğreticide, **PDF dosyalarındaki hassas verileri nasıl maskeleyebileceğinizi** GroupDocs Redaction ile Microsoft Azure OCR'ı birleştirerek öğreneceksiniz. Bu yaklaşım, taranmış sayfalarda güvenilir metin tanıma sağlar ve **PDF Java** belgelerini hassas bir şekilde redakte etmenize olanak tanır, böylece gizlilik düzenlemelerine uyumu temin eder.

## Hızlı Yanıtlar
- **“Mask sensitive data” ne anlama geliyor?** Belirlenen gizli metni bir yer tutucu ile değiştirir (ör. `[REDACTED]`).  
- **Hangi kütüphane OCR'ı yönetir?** Microsoft Azure OCR bağlayıcısı, GroupDocs Redaction aracılığıyla kullanılır.  
- **Lisans gerekli mi?** Değerlendirme için ücretsiz deneme çalışır; üretim için kalıcı bir lisans gerekir.  
- **Taranmış PDF'leri redakte edebilir miyim?** Evet—OCR, regex redaksiyonları uygulamadan önce gizli metni çıkarır.  
- **Bu çözüm sadece Java mı?** Örnek Java tabanlıdır, ancak GroupDocs .NET ve diğer platformlar için benzer API'ler sunar.

## OCR‑Tabanlı Redaksiyon Nedir?
OCR‑tabanlı redaksiyon, önce bir belgenin her sayfasında Optik Karakter Tanıma (OCR) çalıştırarak metin görüntülerini aranabilir dizelere dönüştürür. Metin aranabilir hale geldiğinde, hassas bilgileri—örneğin Sosyal Güvenlik Numaraları, kredi kartı numaraları veya kişisel tanımlayıcılar—bulmak için düzenli ifade (regex) kuralları uygulayabilir ve bunları **`[REDACTED]`** gibi bir maske ile değiştirebilirsiniz.

## Neden GroupDocs Redaction ile Azure OCR Kullanmalı?
- **Yüksek doğruluk** taranmış PDF'lerde ve görüntülerde.  
- **Kesintisiz Java entegrasyonu** Maven veya doğrudan JAR indirme yoluyla.  
- **Esnek regex motoru** herhangi bir veri türü için özel desenler tanımlamanıza olanak tanır.  
- **Ölçeklenebilir** büyük belge grupları için, eşzamanlı olmayan işleme seçenekleriyle.

## Önkoşullar
- **Java Development Kit (JDK) 8+** yüklü.  
- **Maven** (bağımlılık yönetimini tercih ediyorsanız) veya JAR'ları manuel olarak indirme yeteneği.  
- **Microsoft Azure OCR kimlik bilgileri** (uç nokta ve abonelik anahtarı).  
- Temel Java bilgisi ve düzenli ifadeler (regex) konusunda aşinalık.

## Java için GroupDocs Redaction Kurulumu

### Maven Kurulumu
GroupDocs deposunu ve bağımlılığını `pom.xml` dosyanıza ekleyin:

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
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.RedactorSettings;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.examples.java.helper_classes.MicrosoftAzureOcrConnector;

// Initialize the OCR connector with Microsoft Azure
RedactorSettings settings = new RedactorSettings(new MicrosoftAzureOcrConnector());
```

## OCR Redaksiyon ile Hassas Verileri Nasıl Maskeleyeceksiniz

### Adım 1: Belgeyi OCR Ayarlarıyla Yükleyin
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;

// Load your document with OCR settings
try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf", 
    new LoadOptions(), settings)) {
    // Further operations will go here
}
```
- **`YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf`** – PDF dosyanızın yolu ile değiştirin.  
- **`LoadOptions`** – varsayılan yükleme; gerekirse özelleştirebilirsiniz.  
- **`settings`** – daha önce oluşturduğunuz Azure OCR bağlayıcısını içerir.

### Adım 2: Regex Redaksiyonlarını Tanımlayın ve Uygulayın
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
- `\b\d{3}-\d{2}-\d{4}\b` deseni, ABD Sosyal Güvenlik Numaralarına (SSN) eşleşir.  
- `ReplacementOptions("[REDACTED]")` her eşleşmeyi maske ile değiştirir, böylece etkili bir şekilde **hassas verileri maskelemiş** olur.

## Hassas Verileri Maskeleme İçin Yaygın Kullanım Senaryoları
1. **Hukuki Belge Yönetimi** – taslakları paylaşmadan önce müşteri kimlik bilgilerini gizleyin.  
2. **Finansal Raporlama** – hesap numaralarını ve işlem kimliklerini koruyun.  
3. **Sağlık Kayıtları** – HIPAA'ya uyum sağlamak için hasta kimlik bilgilerini redakte edin.  
4. **Kamu Yayınları** – kamu kayıtlarından kişisel verileri kaldırın.  
5. **Kurumsal Sözleşmeler** – dış incelemeler sırasında özel şartları gizleyin.

## Performans İpuçları
- **Regex'i optimize edin** – işleme süresini artıran çok geniş desenlerden kaçının.  
- **Bellek Yönetimi** – `Redactor` örneğini hemen kapatın (try‑with‑resources bunu otomatik yapar).  
- **Eşzamanlı Olmayan Çalıştırma** – toplu işlem için redaksiyon işleri ayrı iş parçacıklarında çalıştırın veya bir görev kuyruğu kullanın.

## Sorun Giderme
- **Azure kimlik bilgisi hatası** – `MicrosoftAzureOcrConnector` içinde uç nokta URL'sini ve abonelik anahtarını iki kez kontrol edin.  
- **Belge yüklenmıyor** – dosya yolunu doğrulayın ve PDF'in şifre korumalı olmadığından emin olun (ya da şifreyi `LoadOptions` ile sağlayın).  
- **Redaksiyon uygulanmadı** – regex'inizi önce basit bir dizeyle test edin; eşleşmeleri doğrulamak için birim testte `Pattern.compile` kullanın.

## Sıkça Sorulan Sorular

**S: OCR redaksiyon nedir?**  
C: OCR redaksiyon, görüntülerden veya taranmış PDF'lerden gizli metni çıkarmak için Optik Karakter Tanıma (OCR) kullanır, ardından bu metni maskelemek için redaksiyon kuralları uygular.

**S: Azure OCR olmadan GroupDocs Redaction kullanabilir miyim?**  
C: Evet, ancak OCR, yerel metin çıkarımının başarısız olduğu taranmış belgelerde doğruluğu büyük ölçüde artırır.

**S: Karmaşık regex desenlerini nasıl yönetirim?**  
C: Bunları adım adım oluşturup test edin; büyük belgelere uygulamadan önce bir sandbox ortamında Java’nın `Pattern` sınıfını kullanın.

**S: Tipik performans darboğazları nelerdir?**  
C: Büyük PDF'ler, çok karmaşık regex'ler ve eşzamanlı OCR çağrıları işleme süresini yavaşlatabilir; toplu işleme ve optimize edilmiş desenleri düşünün.

**S: Uygulama sorunları için destek mevcut mu?**  
C: Kesinlikle—topluluk yardımı için [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33) üzerinden ulaşın veya GroupDocs desteğiyle iletişime geçin.

## Ek Kaynaklar
- **Dokümantasyon**: https://docs.groupdocs.com/redaction/java/  
- **API Referansı**: https://reference.groupdocs.com/redaction/java  
- **İndirme**: https://releases.groupdocs.com/redaction/java/  
- **GitHub**: https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java  
- **Ücretsiz Destek**: https://forum.groupdocs.com/c/redaction/33  
- **Geçici Lisans**: https://purchase.groupdocs.com/temporary-license/

---

**Son Güncelleme:** 2026-02-08  
**Test Edilen Versiyon:** GroupDocs.Redaction 24.9 (Java)  
**Yazar:** GroupDocs