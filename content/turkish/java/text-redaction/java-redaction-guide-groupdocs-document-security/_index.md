---
date: '2026-08-20'
description: Java belgelerinde metni GroupDocs.Redaction kullanarak nasıl redact edeceğinizi
  öğrenin; exact‑phrase, regex, color replacement, annotation ve metadata redaction'ı
  kapsayan güvenli uyumluluk için.
keywords:
- how to redact text
- replace text with color
- GroupDocs.Redaction Java
- Java document security
- document redaction library
lastmod: '2026-08-20'
og_description: Java belgelerinde metni GroupDocs.Redaction kullanarak nasıl redact
  edeceğinizi öğrenin; exact‑phrase, regex, color replacement, annotation ve metadata
  redaction.
og_image_alt: Guide showing Java code redacting text with GroupDocs.Redaction
og_title: Java belgelerinde metni GroupDocs.Redaction ile nasıl redact ederiz
schemas:
- author: GroupDocs
  dateModified: '2026-08-20'
  description: Learn how to redact text in Java documents using GroupDocs.Redaction,
    covering exact‑phrase, regex, color replacement, annotation and metadata redaction
    for secure compliance.
  headline: How to redact text in Java documents with GroupDocs.Redaction
  type: TechArticle
- description: Learn how to redact text in Java documents using GroupDocs.Redaction,
    covering exact‑phrase, regex, color replacement, annotation and metadata redaction
    for secure compliance.
  name: How to redact text in Java documents with GroupDocs.Redaction
  steps:
  - name: '**Add the Maven dependency** (or include the JAR).'
    text: '**Add the Maven dependency** (or include the JAR).'
  - name: '**Configure your license** by calling `License.setLicense("path/to/license.lic")`
      early in your application.'
    text: '**Configure your license** by calling `License.setLicense("path/to/license.lic")`
      early in your application.'
  - name: '**Create a `Redactor` instance** pointing at the source document.'
    text: '**Create a `Redactor` instance** pointing at the source document.'
  - name: '**Initialize the Redactor** with the document you want to process:'
    text: '**Initialize the Redactor** with the document you want to process:'
  - name: '**Define the exact‑phrase rule** and apply it:'
    text: '**Define the exact‑phrase rule** and apply it:'
  - name: '**Save the redacted file** to your output folder:'
    text: '**Save the redacted file** to your output folder:'
  - name: 'Load the document:'
    text: 'Load the document:'
  - name: 'Create a regex rule and apply it:'
    text: 'Create a regex rule and apply it:'
  - name: 'Save the result:'
    text: 'Save the result:'
  - name: 'Load the document:'
    text: 'Load the document:'
  type: HowTo
- questions:
  - answer: Yes. Create each redaction object, call `redactor.apply()` for each, then
      save once.
    question: Can I combine multiple redaction rules in a single pass?
  - answer: Absolutely. Pass the password to the `Redactor` constructor that accepts
      a `LoadOptions` object.
    question: Does GroupDocs.Redaction support password‑protected files?
  - answer: You can call `redactor.preview()` to generate a temporary view that highlights
      the areas to be redacted.
    question: Is it possible to preview redactions before saving?
  - answer: DOCX, PDF, PPTX, XLSX, PNG, JPEG, BMP, and many more—over 30 formats in
      total.
    question: What file formats are supported?
  - answer: Use the metadata erasure feature, remove annotations, and apply exact‑phrase
      or regex redactions to all personal data fields.
    question: How do I ensure the redacted document complies with GDPR?
  type: FAQPage
tags:
- text redaction
- GroupDocs.Redaction
- Java document security
- regex redaction
- metadata removal
title: Java belgelerinde metni GroupDocs.Redaction ile nasıl redact ederiz
type: docs
url: /tr/java/text-redaction/java-redaction-guide-groupdocs-document-security/
weight: 1
---

# GroupDocs.Redaction ile Java belgelerinde metni karalamak

Modern uygulamalarda, PDF, Word dosyaları veya görüntüler içinde **metni nasıl karalanır** gereksinimi uyumluluk ve gizlilik için sıkça ortaya çıkar. Kişisel tanımlayıcıları gizlemeniz, gizli notları kaldırmanız veya meta verileri temizlemeniz gerekse, GroupDocs.Redaction for Java, **java document security** elde etmeniz için temiz, programatik bir yol sunar. Bu öğretici, kütüphaneyi kurmaktan exact‑phrase, regex, renk‑bazlı, açıklama ve meta veri karalamalarına kadar her temel adımı size gösterir—böylece karalamayı doğrudan arka uç hizmetlerinize entegre edebilirsiniz.

## Hızlı yanıtlar
- **Java belge karalama işlemini hangi kütüphane yönetir?** GroupDocs.Redaction for Java.  
- **Metni kaldırmak yerine renk ile değiştirebilir miyim?** Evet, “metni renk ile değiştir” özelliğini kullanın.  
- **Üretim kullanımında lisansa ihtiyacım var mı?** Tam işlevsellik için geçici veya ücretli bir lisans gereklidir.  
- **Hangi Java sürümleri destekleniyor?** JDK 8 ve üzeri.  
- **Kütüphaneyi eklemenin tek yolu Maven mi?** Maven önerilir, ancak JAR dosyasını manuel olarak da indirebilirsiniz.

## Java’da “metni nasıl karalanır” nedir?
**Karalama, hassas içeriği kalıcı olarak kaldırır veya gizler, böylece geri getirilemez.** Java’da bir dosya yüklersiniz, gizlenecek şeyi tanımlarsınız, karalamayı uygularsınız ve temizlenmiş sürümü kaydedersiniz. Bu, sonraki tüketicilerin yalnızca temizlenmiş belgeyi görmesini sağlar.

## Neden GroupDocs.Redaction for Java kullanmalısınız?
Dosyanızı yükleyin, bir kural tanımlayın ve SDK ağır işi halleder. GroupDocs.Redaction **30+ format**ı destekler—DOCX, PDF, PPTX, XLSX, PNG, JPEG, BMP dahil—ve büyük belgeleri akış‑tabanlı mimariyle işler. Exact‑phrase, regex, renk‑bazlı, açıklama ve meta veri karalamalarını sunar, GDPR, HIPAA ve diğer düzenlemelere uyum sağlamak için ayrıntılı kontrol sağlar.

## Önkoşullar
- **Java Development Kit (JDK) 8+** makinenizde kurulu olmalı.  
- **Maven** bağımlılık yönetimi için (veya JAR dosyasını manuel olarak indirebilirsiniz).  

### Gerekli kütüphaneler ve bağımlılıklar
`pom.xml` dosyanıza GroupDocs deposunu ve Redaction bağımlılığını ekleyin:

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

Ayrıca resmi sürüm sayfasından en son JAR dosyasını indirebilirsiniz: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Lisans edinme
Üretim kullanımı için geçici veya tam lisans edinin. Değerlendirme amaçlı ücretsiz deneme mevcuttur.

## GroupDocs.Redaction for Java Kurulumu
1. **Maven bağımlılığını ekleyin** (veya JAR dosyasını dahil edin).  
2. **Lisansınızı yapılandırın** uygulamanızın başında `License.setLicense("path/to/license.lic")` çağrısı yaparak.  
   `License`, bir GroupDocs Redaction lisans dosyasını yüklemek ve uygulamak için kullanılan sınıftır.  
3. **Kaynak belgeye işaret eden bir `Redactor` örneği oluşturun**.

**`Redactor` sınıfı, belgeleri bellek‑verimli bir şekilde yükleyen, değiştiren ve kaydeden çekirdek motorudur.** Bir `Redactor` nesnesine sahip olduğunuzda, sonucu kalıcı hale getirmeden önce birden fazla karalama kuralını zincirleyebilirsiniz.

Artık karalamaya başlamaya hazırsınız.

## Uygulama rehberi

### Tam ifade karalama
Belirli bir ifadeyi (ör. bir kişinin adı) yer tutucu metinle değiştirin.

#### Tam ifade karalama nasıl çalışır?
`ExactPhraseRedaction`, belirli bir metin dizesini kaldıran veya değiştiren bir kuralı temsil eder. Belgeyi yükleyin, tam dizeyi hedefleyen bir `ExactPhraseRedaction` kuralı oluşturun, kuralı uygulayın ve çıktıyı kaydedin. SDK, eşleşen metni otomatik olarak boş bırakır ve düzeni korur.

1. **Redactor'ı** işlemek istediğiniz belgeyle başlatın:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. **Tam ifade kuralını** tanımlayın ve uygulayın:

```java
ExactPhraseRedaction redaction = new ExactPhraseRedaction(
    "John Doe", 
    new ReplacementOptions("[Client]"));

redactor.apply(redaction);
```

3. **Karalanmış dosyayı** çıktı klasörünüze kaydedin:

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Redaction applied successfully.");
}
```

### Metin değiştirme ile Regex karalama
Seri numaraları gibi desenleri bulmak için düzenli ifadeler kullanın ve bunları genel bir token ile değiştirin.

#### Değiştirme ile regex karalama nasıl çalışır?
`RegexRedaction`, eşleşen metni bulmak ve değiştirmek için bir düzenli ifadeye dayalı bir kural tanımlar. Deseni ve değiştirme dizesini içeren bir `RegexRedaction` nesnesi sağlarsınız. Motor belgeyi tarar, her eşleşmeyi değiştirir ve çevresindeki biçimlendirmeyi korur.

1. Belgeyi yükleyin:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. Bir regex kuralı oluşturun ve uygulayın:

```java
RegexRedaction redaction = new RegexRedaction(
    "Redaction",
    new ReplacementOptions("[Product]"));

redactor.apply(redaction);
```

3. Sonucu kaydedin:

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Redaction applied successfully.");
}
```

### Renk değiştirme ile Regex karalama
Metni silmek yerine, **metni renk ile değiştirebilir** ve alttaki karakterleri koruyarak görsel olarak gizleyebilirsiniz.

#### Renk‑bazlı karalama silmeden nasıl farklıdır?
SDK, eşleşen metni seçilen renkle boyar, insan gözüyle okunamaz hale getirir ancak dosya akışında hâlâ bulunur. Bu, sonraki işleme için belge yapısını korumanız gerektiğinde faydalıdır.

1. Belgeyi yükleyin:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. Bir regex deseni tanımlayın ve değiştirme rengini ayarlayın (ör. mavi):

```java
RegexRedaction redaction = new RegexRedaction(
    "\d{2}\s*\d{2}[^\\d]*\d{6}", 
    new ReplacementOptions(Color.BLUE));

redactor.apply(redaction);
```

3. Güncellenmiş dosyayı kaydedin:

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Redaction applied successfully.");
}
```

### Açıklama silme karalaması
Daha temiz bir son sürüm için bir belgedeki tüm açıklamaları (yorumlar, vurgulamalar vb.) kaldırın.

#### Açıklamaları tek adımda nasıl kaldırabilirsiniz?
`AnnotationRedaction`, yorumlar, vurgulamalar ve damgalar gibi açıklamaları kaldıran bir kuraldır. Her açıklama türünü hedefleyen bir `AnnotationRedaction` kuralı oluşturun, uygulayın ve değişiklikleri kalıcı hale getirin.

1. Dosyanızı yükleyin:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. Açıklama‑silme kuralını uygulayın:

```java
DeleteAnnotationRedaction redaction = new DeleteAnnotationRedaction();

redactor.apply(redaction);
```

3. Değişiklikleri kalıcı hale getirin:

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Annotations deleted successfully.");
}
```

### Meta veri silme karalaması
Gizliliği korumak ve uyum standartlarını karşılamak için her türlü meta veriyi (yazar, oluşturma tarihi, özel özellikler) kaldırın.

#### Meta veri silme gizliliği nasıl garanti eder?
`MetadataRedaction`, belgedeki yerleşik ve özel meta veri alanlarını temizler. `MetadataRedaction` kuralı, yerleşik ve özel meta veri alanlarını siler, dosyanın özellik çantasında gizli kimlik belirteci kalmadığından emin olur.

1. Belgeyi açın:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. Meta veri‑silme kuralını uygulayın:

```java
EraseMetadataRedaction redaction = new EraseMetadataRedaction(MetadataFilters.All);

redactor.apply(redaction);
```

3. Temizlenmiş belgeyi kaydedin:

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Metadata erased successfully.");
}
```

## Pratik uygulamalar (neden önemlidir)
- **Hukuki belge hazırlığı** – Taslakları karşı taraf avukatıyla paylaşmadan önce müşteri adlarını karalayın.  
- **Sağlık hizmeti uyumu** – Hasta kimlik bilgilerini kaldırarak HIPAA uyumlu kalın, manuel düzenleme yapmadan.  
- **Kurumsal veri koruması** – Dağıtımdan önce iç raporlarda finansal rakamları veya ticari sırları gizleyin.  

Bu adımları otomatikleştirmek manuel çabayı azaltır, insan hatasını ortadan kaldırır ve binlerce dosya boyunca tutarlı uyumu sağlar.

## Performans değerlendirmeleri
- **Yüklemek yerine akış kullanın** – Büyük dosyalar için, tüm belgeyi belleğe yüklemekten kaçınmak amacıyla `InputStream` kabul eden `Redactor` yapıcılarını kullanın.  
- **Regex desenlerini ön‑derleyin** aynı karalamayı tekrar tekrar çalıştırdığınızda; bu CPU yükünü %30’a kadar azaltır.  
- **JVM yığınını izleyin** – Karalama bellek yoğun olabilir; çok‑gigabayt arşivlerin toplu işlenmesi için yığın boyutunu (`-Xmx2g`) artırmayı düşünün.  

## Yaygın sorunlar ve çözüm yolları
| Semptom | Muhtemel neden | Çözüm |
|---------|----------------|-------|
| `apply` sonrası değişiklik yok | Yanlış belge yolu veya dosya kilitli | Dosya yolunu doğrulayın ve belgenin başka bir yerde açık olmadığından emin olun |
| Regex eşleşmiyor | Desen sözdizimi hatası | Regex'i çevrimiçi bir test aracıyla deneyin; ters eğik çizgileri doğru kaçırın |
| Renk değiştirme görünmüyor | Çıktı formatı metin rengini desteklemiyor (ör. düz metin) | Stil koruyan DOCX veya PDF gibi bir format kullanın |
| Çalışma zamanında lisans hatası | Lisans dosyası eksik veya geçersiz | `.lic` dosyasını erişilebilir bir dizine koyun ve herhangi bir Redactor kullanımdan önce `License.setLicense` çağırın |

## Sıkça sorulan sorular

**S: Birden fazla karalama kuralını tek bir geçişte birleştirebilir miyim?**  
C: Evet. Her karalama nesnesini oluşturun, her biri için `redactor.apply()` çağırın, ardından bir kez kaydedin.

**S: GroupDocs.Redaction şifre‑korumalı dosyaları destekliyor mu?**  
C: Kesinlikle. Şifreyi `LoadOptions` nesnesi kabul eden `Redactor` yapıcısına iletin.

**S: Kaydetmeden önce karalamaları önizlemek mümkün mü?**  
C: `redactor.preview()` çağırarak karalanacak alanları vurgulayan geçici bir görünüm oluşturabilirsiniz.

**S: Hangi dosya formatları destekleniyor?**  
C: DOCX, PDF, PPTX, XLSX, PNG, JPEG, BMP ve daha birçok—toplamda 30’dan fazla format.

**S: Karalanmış belgenin GDPR’ye uygunluğunu nasıl sağlarsınız?**  
C: Meta veri silme özelliğini kullanın, açıklamaları kaldırın ve tüm kişisel veri alanlarına exact‑phrase veya regex karalamaları uygulayın.

## Sonuç
Artık GroupDocs.Redaction kullanarak Java belgelerinde **metni nasıl karalanır** konusunda eksiksiz, uçtan uca bir rehbere sahipsiniz. Exact‑phrase, regex, renk‑bazlı, açıklama ve meta veri karalamaları için adımları izleyerek güçlü **java document security** elde edebilir, kodunuzu temiz ve sürdürülebilir tutabilirsiniz. Bu kod parçacıklarını mevcut hizmetlerinize entegre edin, toplu işleme otomasyonunu sağlayın ve gizlilik düzenlemelerine uyumlu kalın.

---

**Son Güncelleme:** 2026-08-20  
**Test Edilen:** GroupDocs.Redaction 24.9 for Java  
**Yazar:** GroupDocs

## İlgili Eğitimler

- [metadata metnini java ile değiştir – GroupDocs ile Güvenli Karalama](/redaction/java/metadata-redaction/java-redaction-metadata-text-replacement-guide/)
- [GroupDocs.Redaction for Java kullanarak Word belgelerindeki görüntüleri nasıl karalarsınız – Kapsamlı Rehber](/redaction/java/image-redaction/redact-images-word-docs-groupdocs-redaction-java/)
- [GroupDocs Redaction Java Lisansı dosya yolundan belge karalama – Adım Adım Rehber](/redaction/java/licensing-configuration/implement-groupdocs-redaction-java-license-file-path/)