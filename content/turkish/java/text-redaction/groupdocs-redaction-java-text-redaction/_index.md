---
date: '2026-02-26'
description: GroupDocs.Redaction kullanarak Java belgelerindeki metni nasıl karartacağınızı,
  kişisel bilgileri nasıl maskeleyip hassas metni nasıl değiştireceğinizi öğrenin.
keywords:
- text redaction
- GroupDocs Redaction for Java
- sensitive information redaction
title: Java için GroupDocs.Redaction ile Metni Kırpma
type: docs
url: /tr/java/text-redaction/groupdocs-redaction-java-text-redaction/
weight: 1
---

# Java için GroupDocs.Redaction Kullanarak Belgelerde Metin Kırpma (Redact) Nasıl Yapılır

Bu rehberde, GroupDocs.Redaction yardımıyla Java tabanlı belgelerde **metin kırpma** nasıl yapılacağını keşfedeceksiniz. **Kişisel bilgileri maskelemek** ya da **hassas metni** yer tutucularla **değiştirmek** ister misiniz, aşağıdaki adımlar eksiksiz, üretim ortamına hazır bir çözüm sunar. Eğitim sonunda gizliliği koruyabilecek, uyumluluğu sürdürebilecek ve birçok dosya formatında kırpma işlemini otomatikleştirebileceksiniz.

## Quick Answers
- **Hangi kütüphane kullanılıyor?** GroupDocs.Redaction for Java  
- **Kişisel bilgileri maskeleyebilir miyim?** Evet – yer değiştirme seçenekleriyle exact‑phrase kırpma kullanın.  
- **Toplu işleme (batch processing) destekleniyor mu?** Kesinlikle, aynı Redactor örneğiyle birden fazla dosyayı döngüye alabilirsiniz.  
- **Lisans gerekiyor mu?** Değerlendirme için ücretsiz deneme çalışır; üretim için ticari lisans gereklidir.  
- **Hangi Java sürümü gerekiyor?** JDK 8 veya üzeri.

## “Metin kırpma” nedir?
Kırpma, bir belgede gizli verileri kalıcı olarak kaldırma veya gizleme işlemidir. GroupDocs.Redaction ile belirli dizeleri programlı olarak bulabilir, güvenli yer tutucularla değiştirebilir ve temizlenmiş dosyayı kaydedebilirsiniz—tüm bunlar manuel düzenleme gerektirmez.

## Why use GroupDocs.Redaction for Java?
- **Geniş format desteği:** DOCX, PDF, XLSX, PPTX ve daha fazlası.  
- **Yüksek performans:** Büyük dosyalar ve toplu işlemler için optimize edilmiştir.  
- **Genişletilebilir geri çağrılar (callbacks):** Kırpma olaylarına bağlanarak kayıt tutma veya özel işleme yapabilirsiniz.  
- **Uyumluluk‑hazır:** GDPR, HIPAA ve diğer gizlilik düzenlemelerine uygundur.

## Prerequisites
- **Java Development Kit (JDK):** Versiyon 8 veya üzeri.  
- **IDE:** IntelliJ IDEA, Eclipse veya herhangi bir Java uyumlu editör.  
- **Maven:** Bağımlılık yönetimi için.  
- **Temel Java bilgisi:** Sınıflar, metodlar ve istisna yönetimi hakkında bilgi.

## Setting Up GroupDocs.Redaction for Java
Başlamak için, kütüphaneyi Maven projenize ekleyin.

### Maven Setup
`pom.xml` dosyanıza depoyu ve bağımlılığı ekleyin:

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

### Direct Download
İsterseniz, en son JAR dosyasını [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) adresinden edinebilirsiniz.

### License Acquisition
**Free Trial** ile başlayabilir, uzun vadeli test için **Temporary License** talep edebilir veya üretim kullanımı için **Commercial License** satın alabilirsiniz.

## How to Redact Text in Documents with GroupDocs.Redaction
Aşağıdaki bölümler, **kişisel bilgileri maskeleme** ve **hassas metni değiştirme** için gereken adımları size gösterir.

### Step 1: Initialize the Redactor
İşlemek istediğiniz belgeye işaret eden bir `Redactor` örneği oluşturun.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx", new LoadOptions());
```

### Step 2: Apply Exact‑Phrase Redaction
`ExactPhraseRedaction` kullanarak “John Doe” gibi bir ifadeyi bulun ve güvenli bir yer tutucu ile değiştirin.

```java
redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]"));
```
- **Parametreler:**  
  - `"John Doe"` – kırpılacak tam metin.  
  - `ReplacementOptions("[personal]")` – orijinal içeriği değiştirecek dize, etkili bir şekilde **kişisel bilgileri maskeleyerek**.

### Step 3: Save the Redacted Document
Değişiklikleri yeni bir dosyaya kaydedin veya orijinali üzerine yazın.

```java
redactor.save();
```

### Step 4: Clean Up Resources
Yerel kaynakları serbest bırakmak için her zaman `Redactor`'ı kapatın.

```java
finally {
    redactor.close();
}
```

## How to Mask Personal Information with a Custom Callback
Bazen bir kırpma gerçekleştiğinde ne olacağını daha fazla kontrol etmeniz gerekir (ör. kayıt tutma, koşullu değiştirme).

### Create a Callback Class
Kırpma olaylarını almak için `IRedactionCallback` arayüzünü uygulayın.

```java
class RedactionDump implements IRedactionCallback {
    @Override
    public void onRedacted(IRedaction redaction) {
        // Custom processing or logging for each redaction event.
    }
}
```

### Use the Callback When Instantiating Redactor
Geri çağırmayı `RedactorSettings` aracılığıyla geçirin.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx", new LoadOptions(), new RedactorSettings(new RedactionDump()));
```

## Practical Applications
- **Hukuki sözleşmeler:** Müşteri adlarını, SSN'leri veya gizli maddeleri otomatik olarak gizleyin.  
- **Tıbbi kayıtlar:** Üçüncü taraflarla paylaşmadan önce hasta kimlik bilgileri gibi **kişisel bilgileri maskeleyin**.  
- **Kurumsal iletişimler:** Dış dağıtıma önceden iç proje kodları gibi **hassas metinleri değiştirin**.

## Performance Considerations
Büyük veya çok sayıda dosya işlerken aşağıdaki ipuçlarını aklınızda bulundurun:

- **Toplu işleme:** Başlangıç yükünü azaltmak için dosya koleksiyonunu döngüye alın.  
- **Bellek yönetimi:** Her dosyadan sonra `Redactor`'ı serbest bırakın; aynı anda çok sayıda belgeyi bellekte tutmaktan kaçının.  
- **Profil oluşturma:** I/O veya kırpma mantığındaki darboğazları tespit etmek için Java profil araçlarını (ör. VisualVM) kullanın.

## Frequently Asked Questions
**S: GroupDocs.Redaction ile PDF'lerden metin kırpabilir miyim?**  
C: Evet, kütüphane PDF, DOCX, XLSX, PPTX ve birçok diğer formatı destekler.

**S: Kırpma geri alınabilir mi?**  
C: Hayır. Kırpmalar orijinal içeriği kalıcı olarak kaldırır, bu yüzden kaynak dosyanın bir yedeğini tutun.

**S: Çok büyük belgeleri verimli bir şekilde nasıl işlerim?**  
C: Belgeleri parçalara bölerek işleyin, toplu modu kullanın ve profil araçlarıyla bellek kullanımını izleyin.

**S: Başka hangi metin formatları destekleniyor?**  
C: DOCX ve PDF'nin yanı sıra TXT, RTF, XLSX, PPTX ve daha fazlasını kırpabilirsiniz.

**S: GroupDocs.Redaction'ı mevcut iş akışlarına entegre edebilir miyim?**  
C: Kesinlikle. API, web servislerinden, arka plan görevlerinden veya CI/CD boru hatlarından çağrılabilir.

## Resources
- **Dokümantasyon:** [GroupDocs Redaction Java Docs](https://docs.groupdocs.com/redaction/java/)  
- **API Referansı:** [GroupDocs API Reference for Java](https://reference.groupdocs.com/redaction/java)  
- **İndirme:** [GroupDocs.Redaction Downloads](https://releases.groupdocs.com/redaction/java/)  
- **GitHub Deposu:** [GroupDocs Redaction GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **Ücretsiz Destek Forumu:** [GroupDocs Free Support](https://forum.groupdocs.com/c/redaction/33)  
- **Geçici Lisans Başvurusu:** [Apply for a Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Son Güncelleme:** 2026-02-26  
**Test Edilen Sürüm:** GroupDocs.Redaction 24.9 for Java  
**Yazar:** GroupDocs