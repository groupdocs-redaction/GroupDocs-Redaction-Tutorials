---
date: '2026-08-09'
description: GroupDocs.Redaction Java API'yi kullanarak Excel elektronik tablolarında
  kişisel verileri gizlemeyi ve e‑posta adreslerini maskelemeyi öğrenin.
keywords:
- how to hide personal data
- mask email addresses excel
- GroupDocs.Redaction Java
- Excel redaction tutorial
lastmod: '2026-08-09'
og_description: GroupDocs.Redaction Java API'yi kullanarak Excel dosyalarında kişisel
  verileri gizleme ve e‑posta adreslerini maskeleme konusunda adım adım keşfedin –
  GDPR uyumluluğu için hızlı ve güvenli bir çözüm.
og_image_alt: Guide showing Java code that redacts email addresses in an Excel spreadsheet
og_title: GroupDocs Java ile Excel'de kişisel verileri gizleme
schemas:
- author: GroupDocs
  dateModified: '2026-08-09'
  description: Learn how to hide personal data and mask email addresses in Excel spreadsheets
    using the GroupDocs.Redaction Java API.
  headline: How to hide personal data in Excel with GroupDocs Java
  type: TechArticle
- description: Learn how to hide personal data and mask email addresses in Excel spreadsheets
    using the GroupDocs.Redaction Java API.
  name: How to hide personal data in Excel with GroupDocs Java
  steps:
  - name: '**Partner data exchange** – Automatically strip customer emails before
      sending spreadsheets to vendors.'
    text: '**Partner data exchange** – Automatically strip customer emails before
      sending spreadsheets to vendors.'
  - name: '**Internal audit preparation** – Anonymize employee data during compliance
      reviews.'
    text: '**Internal audit preparation** – Anonymize employee data during compliance
      reviews.'
  - name: '**Scheduled reporting** – Embed the redaction step into nightly batch jobs
      that generate distribution‑ready reports.'
    text: '**Scheduled reporting** – Embed the redaction step into nightly batch jobs
      that generate distribution‑ready reports.'
  type: HowTo
- questions:
  - answer: Extend the pattern to include additional allowed characters (e.g., “+”
      or “_”) and test against a larger sample set, then re‑run the redaction.
    question: My regex still misses some corporate email formats. What should I do?
  - answer: Yes. Create a separate `CellFilter` for each column and invoke `redactor.apply`
      for each filter sequentially.
    question: Can I redact more than one column in a single pass?
  - answer: The library processes sheets incrementally, so files up to several gigabytes
      can be redacted as long as you enable streaming and close the `Redactor` after
      each file.
    question: Is GroupDocs.Redaction able to handle Excel files larger than 1 GB?
  - answer: Inspect the `RedactorChangeLog` returned by `apply`; a non‑failed status
      indicates success, while any errors are listed with line numbers and cell references.
    question: How do I capture redaction results or errors?
  - answer: Absolutely. Build the placeholder string dynamically (e.g., `"[redacted:"
      + UUID.randomUUID() + "]"`) and pass it to `ReplacementOptions`.
    question: Can I use a custom placeholder that includes a unique token per row?
  type: FAQPage
tags:
- hide personal data
- GroupDocs.Redaction
- Java Excel processing
- data privacy
title: GroupDocs Java ile Excel'de kişisel verileri gizleme
url: /tr/java/spreadsheet-redaction/redact-emails-excel-groupdocs-redaction-java/
weight: 1
---

# Excel'de Kişisel Verileri Gizleme - GroupDocs Java

Bu kılavuzda **kişisel verileri gizleme** yöntemini—özellikle e‑posta adreslerini—Excel çalışma kitaplarında GroupDocs.Redaction Java API'sını kullanarak öğreneceksiniz. GDPR, CCPA veya dahili gizlilik politikalarına uymanız gerektiğinde, burada gösterilen yaklaşım, kırmızı çizim işlemini güvenli bir şekilde otomatikleştirmenizi, orijinal dosyayı dokunulmaz tutmanızı ve dağıtıma hazır temiz bir sürüm üretmenizi sağlar.

## Hızlı cevaplar
- **“Kişisel verileri gizleme” ne anlama geliyor?** Bir dosyadan kişisel olarak tanımlanabilir bilgileri (PII) kalıcı olarak maskeleme veya kaldırma anlamına gelir, böylece artık okunamaz.  
- **Kırmızı çizim işlemini hangi kütüphane gerçekleştiriyor?** GroupDocs.Redaction for Java.  
- **Örneği çalıştırmak için lisansa ihtiyacım var mı?** Test için ücretsiz deneme yeterlidir; ticari kullanım için üretim‑düzeyi lisans gereklidir.  
- **Yer tutucu metni özelleştirebilir miyim?** Evet—e‑postaları “[redacted email]” gibi istediğiniz herhangi bir dizeyle değiştirebilirsiniz.  
- **Yöntem büyük elektronik tablolar için uygun mu?** Evet, “Performans hususları” bölümündeki ipuçlarını izlerseniz uygundur.

## Kişisel verileri gizleme nedir?
**Kişisel verileri gizleme**, bir bireyi doğrudan veya dolaylı olarak tanımlayabilecek herhangi bir bilginin (isim, telefon numarası, e‑posta adresi vb.) geri döndürülemez şekilde kaldırılması veya maskelemesidir. Bu süreç, ortaya çıkan dosyanın konu kişiyi yeniden tanımlamak için kullanılamamasını sağlar.

## Neden GroupDocs.Redaction for Java kullanmalı?
GroupDocs.Redaction **30+ giriş ve çıkış formatını** destekler ve **500.000 satıra kadar** çalışma kitabını tüm dosyayı belleğe yüklemeden işleyebilir; bu da geleneksel dosya‑parçalama çözümlerine kıyasla **%80’e varan bellek ayak izi azaltması** sağlar. Bu ölçülebilir faydalar, onu kurumsal‑düzey veri‑gizliliği boru hatları için birincil seçim yapar.

## Önkoşullar
- Java Development Kit (JDK) 8 veya üzeri.  
- Maven yapı dosyalarına temel aşinalık.  
- GroupDocs.Redaction Java kütüphanesine erişim (Maven üzerinden veya resmi sürüm sayfasından indirilebilir).

## GroupDocs.Redaction for Java kurulumu

### Maven projesine GroupDocs.Redaction nasıl eklenir?
GroupDocs deposunu ve Redaction bağımlılığını `pom.xml` dosyanıza ekleyin (bkz. [GroupDocs.Redaction releases](https://releases.groupdocs.com/redaction/java/)). Ardından `mvn clean install` komutunu çalıştırarak artefaktları indirin.

```text
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
```

### GroupDocs.Redaction için lisans nasıl alınır?
GroupDocs üç lisans seçeneği sunar (bkz. [GroupDocs’ website](https://purchase.groupdocs.com/temporary-license/)):

- **Ücretsiz deneme** – sınırlı özellikli değerlendirme, kredi kartı gerektirmez.  
- **Geçici lisans** – GroupDocs web sitesinden alınan 30‑günlük değerlendirme anahtarı.  
- **Tam lisans** – satış portalı üzerinden satın alınan kalıcı üretim lisansı.

```text
```java
import com.groupdocs.redaction.Redactor;

public class RedactEmails {
    public static void main(String[] args) {
        // Initialize the redactor with your document path
        try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_XLSX")) {
            // Your redaction logic will go here
        }
    }
}
```
```

## Uygulama rehberi

### Excel dosyası için Redactor örneği nasıl oluşturulur?
`Redactor` sınıfı, bir belgeyi yükleyen ve kırmızı çizim işlemlerini sağlayan ana giriş noktasını temsil eder.  
Kaynak çalışma kitabına işaret eden bir `Redactor` nesnesi oluşturun. `Redactor` sınıfı, tüm kırmızı çizim işlemleri için giriş noktasıdır; dosyayı yönetilen bir bellek yapısına yüklerken orijinal dosyayı diskte tutar.

```text
```java
import com.groupdocs.redaction.Redactor;

public class RedactEmails {
    public static void main(String[] args) {
        try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_XLSX")) {
            // Proceed to the next steps for redaction
        }
    }
}
```
```

### Kırmızı çizimi tek bir çalışma sayfası ve sütunla sınırlamak nasıl yapılır?
`CellFilter` sınıfı, kırmızı çizim için incelenecek çalışma sayfası ve sütun(lar)ı belirtmenizi sağlar. Hedef sayfa adını ve sütun indeksini belirlemek için bir `CellFilter` kullanın. `CellFilter` sınıfı, kırmızı çizim motoru değerlendirmeden önce hücreleri filtreler, böylece yalnızca istenen hücreler işlenir.

```text
```java
import com.groupdocs.redaction.redactions.CellFilter;

// Create and configure the filter
CellFilter filter = new CellFilter();
filter.setColumnIndex(1); // Targeting the second column (index starts at 0)
filter.setWorkSheetName("Customers"); // Specify the worksheet name
```
```

### Çoğu e‑posta adresine uyan bir düzenli ifade deseni nasıl tanımlanır?
`java.util.regex` paketinden `Pattern` sınıfı, metni eşleştirmek için derlenmiş bir düzenli ifadeyi temsil eder. Tipik e‑posta formatlarını yakalayan bir regex ile bir `Pattern` nesnesi oluşturun. Aşağıdaki desen, RFC‑5322‑uyumlu adreslerin büyük çoğunluğunu yakalar ve hatalı dizeleri görmezden gelir.

```text
```java
import java.util.regex.Pattern;

// Define regex pattern for matching emails
Pattern expression = Pattern.compile("^\\w+([-+.']\\w+)*@\\w+([-.]\\w+)*\\.\\w+([-.]\\w+)*$");
```
```

### Kırmızı çizimi uygulayıp e‑postaları bir yer tutucu ile nasıl değiştiririm?
`ReplacementOptions` sınıfı, eşleşen içeriğin nasıl değiştirileceğini (ör. yer tutucu metni) tanımlar. Filtre, desen ve bir `ReplacementOptions` örneğini birleştirin. `ReplacementOptions` sınıfı, her kırmızı çizili hücrede görünecek kesin yer tutucu metni ayarlamanızı sağlar.

```text
```java
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.RedactorChangeLog;
import com.groupdocs.redaction.redactions.CellColumnRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

// Apply redaction
RedactorChangeLog result = redactor.apply(new CellColumnRedaction(filter, expression, new ReplacementOptions("[customer email]")));

// Save changes if successful
if (result.getStatus() != RedactionStatus.Failed) {
    SaveOptions saveOptions = new SaveOptions();
    saveOptions.setAddSuffix(true); // Add a suffix to the saved file name
    redactor.save(saveOptions);
}
```
```

## Yaygın hatalar ve sorun giderme

- **Regex tüm durumları yakalamıyor** – İfadenizi veri örneklerinizle test edin ve karakter sınıflarını gerektiği gibi ayarlayın.  
- **Yanlış sütun indeksi** – Sütun indekslemesinin 0’dan başladığını unutmayın; B sütunu indeks 1’dir.  
- **Çalışma sayfası adı büyük/küçük harf duyarlılığı** – Excel’de görülen tam sayfa adını kullanın; “Customers” ≠ “customers”.  
- **Kaynak sızıntıları** – `Redactor`ı bir try‑with‑resources bloğunda (örnekte gösterildiği gibi) sararak yerel kaynakların zamanında serbest bırakılmasını sağlayın.

## Excel'de kişisel verileri neden gizlemelisiniz?
Excel'de kişisel verileri gizlemek, herhangi bir kişisel tanımlayıcı bilgiyi kaldırarak dosyanın bireyleri izlemek için kullanılmasını engeller. Bu, gizliliği korur, yasal gereklilikleri karşılar ve dış taraflarla paylaşılan ya da kamuoyunda yayınlanan elektronik tabloların yanlışlıkla sızmasını önler.

- **Yasal uyumluluk** – GDPR, CCPA ve sektöre özgü gizlilik zorunluluklarını karşılayın.  
- **Risk azaltma** – Dosyaları dış ortaklarla paylaşırken PII’nın istem dışı ortaya çıkmasını önleyin.  
- **Denetim hazırlığı** – Hassas değerleri kalıcı olarak kaldırarak temiz, değiştirilemez bir denetim izi tutun.

## Pratik uygulamalar

1. **Ortak veri değişimi** – Müşteri e‑postalarını otomatik olarak temizleyerek elektronik tabloları satıcılara gönderin.  
2. **İç denetim hazırlığı** – Uyumluluk incelemeleri sırasında çalışan verilerini anonimleştirin.  
3. **Planlı raporlama** – Dağıtıma hazır raporlar üreten gece toplu işlerine kırmızı çizim adımını ekleyin.

## Performans hususları

- **Toplu işleme** – Birden fazla dosya için tek bir `Redactor` örneği yeniden kullanarak JVM yükünü azaltın.  
- **Bellek yönetimi** – API, çalışma sayfalarını tek tek işler; 100 MB’dan büyük çalışma kitapları için satırları parçalar halinde işleyerek yığın kullanımını düşük tutun.  
- **Büyük veri setleri** – 100 k satırdan fazla dosyalarla çalışırken (sürüm 24.9’da mevcut) akış modunu etkinleştirerek bellek tüketimini 200 MB’ın altında tutun.

## Sıkça sorulan sorular

**S: Regex hâlâ bazı kurumsal e‑posta formatlarını kaçırıyor. Ne yapmalıyım?**  
C: Ek izin verilen karakterleri (ör. “+” veya “_”) içerecek şekilde deseni genişletin, daha büyük bir örnek setiyle test edin ve ardından kırmızı çizimi yeniden çalıştırın.

**S: Tek bir geçişte birden fazla sütunu kırmızı çizebilir miyim?**  
C: Evet. Her sütun için ayrı bir `CellFilter` oluşturup `redactor.apply` metodunu sırasıyla çağırın.

**S: GroupDocs.Redaction 1 GB’dan büyük Excel dosyalarını işleyebilir mi?**  
C: Kütüphane sayfaları artımlı olarak işler, bu yüzden akış modunu etkinleştirip her dosyadan sonra `Redactor`ı kapattığınız sürece birkaç gigabayta kadar dosyalar kırmızı çizilebilir.

**S: Kırmızı çizim sonuçlarını veya hataları nasıl yakalarım?**  
C: `apply` tarafından döndürülen `RedactorChangeLog` nesnesini inceleyin; başarısız olmayan bir durum başarıyı gösterir, hatalar ise satır numaraları ve hücre referanslarıyla listelenir.

**S: Her satır için benzersiz bir token içeren özel bir yer tutucu kullanabilir miyim?**  
C: Kesinlikle. Yer tutucu dizesini dinamik olarak oluşturun (ör. `"[redacted:" + UUID.randomUUID() + "]"`) ve `ReplacementOptions`a iletin.

## Ek kaynaklar

- [Documentation](https://docs.groupdocs.com/redaction/java/)
- [API Reference](https://reference.groupdocs.com/redaction/java)
- [Download GroupDocs.Redaction](https://releases.groupdocs.com/redaction/java/)
- [GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
- [Free Support Forum](https://forum.groupdocs.com/c/redaction/33)
- [Temporary License Information](https://purchase.groupdocs.com/temporary-license/)

---

**Son Güncelleme:** 2026-08-09  
**Test Edilen Versiyon:** GroupDocs.Redaction 24.9 for Java  
**Yazar:** GroupDocs

## İlgili Eğitimler

- [How to Filter Data in Spreadsheets – GroupDocs.Redaction Java](/redaction/java/spreadsheet-redaction/)
- [Mask Sensitive Data Java – Redact Personal Info with GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)
- [Mask Sensitive Data Java – GroupDocs.Redaction Guide](/redaction/java/getting-started/)