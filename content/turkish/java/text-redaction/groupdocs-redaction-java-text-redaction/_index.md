---
date: '2026-08-14'
description: GroupDocs.Redaction kullanarak Java belgelerinde metni nasıl gizlenir
  – kişisel bilgileri maskele ve hassas metni etkili bir şekilde değiştir.
keywords:
- how to redact text
- GroupDocs Redaction Java
- text redaction Java
- mask personal information
lastmod: '2026-08-14'
og_description: GroupDocs.Redaction for Java ile metin gizleme, PDFs, DOCX ve daha
  fazlası üzerinde kişisel verileri kalıcı olarak maskelemenizi ve hassas dizeleri
  değiştirmenizi sağlar, GDPR ve HIPAA uyumluluğunu temin eder.
og_image_alt: 'Guide: redact text in Java using GroupDocs.Redaction library'
og_title: GroupDocs.Redaction for Java ile metin nasıl gizlenir
schemas:
- author: GroupDocs
  dateModified: '2026-08-14'
  description: How to redact text in Java documents using GroupDocs.Redaction – mask
    personal information and replace sensitive text efficiently.
  headline: How to redact text with GroupDocs.Redaction for Java
  type: TechArticle
- description: How to redact text in Java documents using GroupDocs.Redaction – mask
    personal information and replace sensitive text efficiently.
  name: How to redact text with GroupDocs.Redaction for Java
  steps:
  - name: initialize the redactor
    text: '`Redactor` is the core class that loads a document, applies redaction rules,
      and writes the output.'
  - name: apply exact‑phrase redaction
    text: '`ExactPhraseRedaction` searches for an exact string match, while `ReplacementOptions`
      defines how the matched text should be replaced. - **Parameters:** - `"John
      Doe"` – the exact text to be redacted. - `ReplacementOptions("[personal]")`
      – the string that will replace the original content, effective'
  - name: save the redacted document
    text: '`Redactor.save` writes the modified document to a new file or overwrites
      the original, preserving the original format.'
  - name: clean up resources
    text: Always call `Redactor.close()` to release native resources and avoid memory
      leaks.
  type: HowTo
- questions:
  - answer: Yes, the library supports PDF, DOCX, XLSX, PPTX, and many other formats.
    question: Can I redact text from PDFs using GroupDocs.Redaction?
  - answer: No. Redactions permanently remove the original content, so keep a backup
      of the source file.
    question: Is a redaction reversible?
  - answer: Process them in chunks, use batch mode, and monitor memory usage with
      profiling tools.
    question: How do I handle very large documents efficiently?
  - answer: Besides DOCX and PDF, you can redact TXT, RTF, XLSX, PPTX, and more.
    question: What other text formats are supported?
  - answer: Absolutely. The API can be called from web services, background jobs,
      or CI/CD pipelines.
    question: Can I integrate GroupDocs.Redaction into existing workflows?
  type: FAQPage
tags:
- text redaction
- GroupDocs.Redaction
- Java document processing
- privacy compliance
- redaction API
title: GroupDocs.Redaction for Java ile metin nasıl gizlenir
type: docs
url: /tr/java/text-redaction/groupdocs-redaction-java-text-redaction/
weight: 1
---

# GroupDocs.Redaction for Java ile metni nasıl kırpılır

Bu öğreticide, GroupDocs.Redaction kullanarak Java‑tabanlı belgelerde **metni nasıl kırpacağınızı** öğreneceksiniz. Kişisel bilgileri maskeleme, hassas dizeleri güvenli yer tutucularla değiştirme ve birden fazla dosyayı toplu‑iş dostu bir şekilde işleme yollarını göreceksiniz. Sonunda, gizliliği koruyan, GDPR/HIPAA gereksinimlerini karşılayan ve mevcut Java uygulamalarına sorunsuz bir şekilde entegre olan üretim hazır bir çözümünüz olacak.

## Hızlı cevaplar
- **Hangi kütüphane kullanılıyor?** GroupDocs.Redaction for Java.  
- **Kişisel bilgileri maskeleyebilir miyim?** Yes – use exact‑phrase redaction with replacement options.  
- **Toplu işleme destekleniyor mu?** Absolutely, you can loop through multiple files with the same Redactor instance.  
- **Lisans gerekli mi?** A free trial works for evaluation; a commercial license is required for production.  
- **Hangi Java sürümü gerekiyor?** JDK 8 or higher.

## “Metni nasıl kırpılır” nedir?
Kırpma, bir belgedeki gizli verileri kalıcı olarak kaldırır veya gizler. GroupDocs.Redaction ile belirli dizeleri bulabilir, güvenli yer tutucularla değiştirebilir ve temizlenmiş dosyayı kaydedebilirsiniz—tüm bunlar manuel düzenleme gerektirmez.

## Neden GroupDocs.Redaction for Java kullanmalı?
GroupDocs.Redaction for Java, **50+ giriş ve çıkış formatını** (PDF, DOCX, XLSX, PPTX, TXT, RTF dahil) destekler ve tüm belgeyi belleğe yüklemeden çok sayfalı dosyaları işleyebilir, standart sunucu donanımında yüksek verimli toplu işlemler sunar.

## Önkoşullar
- **Java Development Kit (JDK):** Versiyon 8 veya daha yeni.  
- **IDE:** IntelliJ IDEA, Eclipse veya herhangi bir Java‑uyumlu editör.  
- **Maven:** Bağımlılık yönetimi için.  
- **Temel Java bilgisi:** Sınıflar, metodlar ve istisna yönetimi konularına aşina olmak.

## GroupDocs.Redaction for Java Kurulumu
Başlamak için, kütüphaneyi Maven projenize ekleyin.

### Maven kurulumu
Add the repository and dependency to your `pom.xml` file:

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
İsterseniz, en son JAR dosyasını [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) adresinden alın.

### Lisans edinimi
Bir **Ücretsiz Deneme** ile başlayabilir, genişletilmiş test için **Geçici Lisans** talep edebilir veya üretim kullanımı için **Ticari Lisans** satın alabilirsiniz.

## GroupDocs.Redaction ile belgelerde metni nasıl kırparız

Aşağıdaki bölümler, **kişisel bilgileri maskeleme** ve **hassas metni değiştirme** için gereken adımları size gösterir.

### Adım 1: redaktörü başlatma
`Redactor`, bir belgeyi yükleyen, kırpma kurallarını uygulayan ve çıktıyı yazan temel sınıftır.  

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx", new LoadOptions());
```

### Adım 2: tam ifadeli kırpma uygulama
`ExactPhraseRedaction`, tam bir dize eşleşmesini arar, `ReplacementOptions` ise eşleşen metnin nasıl değiştirileceğini tanımlar.

```java
redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]"));
```
- **Parametreler:**  
  - `"John Doe"` – kırpılacak tam metin.  
  - `ReplacementOptions("[personal]")` – orijinal içeriği değiştirecek dize, etkili bir şekilde **kişisel bilgileri maskeleyerek**.

### Adım 3: kırpılmış belgeyi kaydetme
`Redactor.save`, değiştirilmiş belgeyi yeni bir dosyaya yazar veya orijinali üzerine yazar, orijinal formatı korur.  

```java
redactor.save();
```

### Adım 4: kaynakları temizleme
Her zaman `Redactor.close()` çağırarak yerel kaynakları serbest bırakın ve bellek sızıntılarını önleyin.  

```java
finally {
    redactor.close();
}
```

## Özel bir geri arama ile kişisel bilgileri nasıl maskeleme
Özel bir geri arama, her kırpma olayına yanıt vermenizi sağlar—günlükleme, koşullu değişiklikler veya denetim izleri için faydalıdır.

### Geri arama sınıfı oluşturma
`IRedactionCallback`, her kırpma işleminden önce ve sonra çağrılan metodları tanımlar.  

```java
class RedactionDump implements IRedactionCallback {
    @Override
    public void onRedacted(IRedaction redaction) {
        // Custom processing or logging for each redaction event.
    }
}
```

### Redactor örneklenirken geri aramayı kullanma
Geri arama uygulamanızı `RedactorSettings` aracılığıyla geçirin, böylece motor işlem sırasında onu çağırır.  

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx", new LoadOptions(), new RedactorSettings(new RedactionDump()));
```

## Pratik uygulamalar
- **Hukuki sözleşmeler:** Taslakları paylaşmadan önce müşteri adlarını, SSN'leri veya gizli maddeleri otomatik olarak gizleyin.  
- **Tıbbi kayıtlar:** **Kişisel bilgileri maskeleyin** (örneğin hasta kimlikleri) kayıtları araştırma ortaklarına dışa aktarırken.  
- **Kurumsal iletişim:** **Hassas metni değiştirin** (örneğin iç proje kodları) dış dağıtımdan önce, kazara sızıntıları önlemek için.

## Performans hususları
Büyük veya çok sayıda dosya işlenirken, şu ipuçlarını aklınızda tutun:
- **Toplu işleme:** Başlangıç yükünü azaltmak için dosya koleksiyonunu döngüyle işleyin.  
- **Bellek yönetimi:** Her dosyadan sonra `Redactor`'ı serbest bırakın; aynı anda çok sayıda belgeyi bellekte tutmaktan kaçının.  
- **Profil oluşturma:** I/O veya kırpma mantığındaki darboğazları tespit etmek için Java profil araçlarını (ör. VisualVM) kullanın.

## Sıkça sorulan sorular
**Q: PDF'lerden metin kırpabilir miyim GroupDocs.Redaction kullanarak?**  
A: Evet, kütüphane PDF, DOCX, XLSX, PPTX ve birçok diğer formatı destekler.  

**Q: Kırpma geri döndürülebilir mi?**  
A: Hayır. Kırpmalar orijinal içeriği kalıcı olarak kaldırır, bu yüzden kaynak dosyanın bir yedeğini tutun.  

**Q: Çok büyük belgeleri verimli bir şekilde nasıl yönetirim?**  
A: Belgeleri parçalara bölerek işleyin, toplu modu kullanın ve profil araçlarıyla bellek kullanımını izleyin.  

**Q: Başka hangi metin formatları destekleniyor?**  
A: DOCX ve PDF dışında, TXT, RTF, XLSX, PPTX ve daha fazlasını kırpabilirsiniz.  

**Q: GroupDocs.Redaction'ı mevcut iş akışlarına entegre edebilir miyim?**  
A: Kesinlikle. API, web servislerinden, arka plan görevlerinden veya CI/CD boru hatlarından çağrılabilir.  

## Kaynaklar
- **Dokümantasyon:** [GroupDocs Redaction Java Docs](https://docs.groupdocs.com/redaction/java/)  
- **API referansı:** [GroupDocs API Reference for Java](https://reference.groupdocs.com/redaction/java)  
- **İndirme:** [GroupDocs.Redaction Downloads](https://releases.groupdocs.com/redaction/java/)  
- **GitHub deposu:** [GroupDocs Redaction GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **Ücretsiz destek forumu:** [GroupDocs Free Support](https://forum.groupdocs.com/c/redaction/33)  
- **Geçici lisans başvurusu:** [Apply for a Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Son Güncelleme:** 2026-08-14  
**Test Edilen Versiyon:** GroupDocs.Redaction 24.9 for Java  
**Yazar:** GroupDocs

## İlgili Öğreticiler

- [Hassas Verileri Maskele Java – GroupDocs.Redaction Kılavuzu](/redaction/java/getting-started/)
- [Hassas Verileri Maskele Java – GroupDocs.Redaction ile Kişisel Bilgileri Kırpma](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)
- [Parola Korumalı Belgeleri Düzenle Java - GroupDocs.Redaction Kullanarak Belgeleri Kırpma](/redaction/java/document-loading/groupdocs-redaction-java-password-documents/)