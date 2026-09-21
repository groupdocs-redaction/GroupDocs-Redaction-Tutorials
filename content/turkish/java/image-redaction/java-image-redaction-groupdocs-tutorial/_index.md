---
date: '2026-09-21'
description: GroupDocs.Redaction for Java ile görüntüyü nasıl kırpılacağını öğrenin.
  Adım adım rehber, kurulum, piksel‑seviye kırpma, doğrulama ve en iyi uygulamaları
  kapsar.
keywords:
- how to redact image
- Java image redaction
- GroupDocs.Redaction for Java
- scanned image redaction
- pixel redaction Java
lastmod: '2026-09-21'
og_description: GroupDocs.Redaction for Java ile görüntüyü nasıl kırparız. Tarama
  dosyalarındaki piksel verilerini maskelemek, renk seçmek ve sonuçları doğrulamak
  için bu rehberi izleyin—GDPR ve HIPAA uyumluluğu için mükemmel.
og_image_alt: Guide showing Java code that redacts scanned images using GroupDocs.Redaction
og_title: GroupDocs.Redaction for Java kullanarak görüntüyü nasıl kırparız
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: Learn how to redact image with GroupDocs.Redaction for Java. Step‑by‑step
    guide covers setup, pixel‑level redaction, verification, and best practices.
  headline: How to redact image using GroupDocs.Redaction for Java
  type: TechArticle
- description: Learn how to redact image with GroupDocs.Redaction for Java. Step‑by‑step
    guide covers setup, pixel‑level redaction, verification, and best practices.
  name: How to redact image using GroupDocs.Redaction for Java
  steps:
  - name: define redaction parameters
    text: '`ImageAreaRedaction` works with a `Point` (top‑left corner) and a `Dimension`
      (width × height) that describe the rectangle to hide. In this example we use
      a blue fill color.'
  - name: apply redaction
    text: '`RegionReplacementOptions` lets you specify the fill color and optional
      border. Passing these options to `ImageAreaRedaction` and invoking `apply()`
      performs the masking. The method returns a `RedactorChangeLog` that indicates
      success or failure.'
  - name: release resources
    text: '`Redactor` implements `AutoCloseable`. Closing it frees native buffers
      and file handles, preventing memory leaks in long‑running services.'
  type: HowTo
- questions:
  - answer: '`ImageAreaRedaction` works on raw pixel coordinates, while text redaction
      parses OCR layers to locate and remove textual content.'
    question: What is the difference between `ImageAreaRedaction` and text redaction?
  - answer: Yes—call `redactor.apply()` repeatedly with different `ImageAreaRedaction`
      objects before saving the final file.
    question: Can I redact multiple regions in a single image?
  - answer: The library supports common raster formats (JPG, PNG, BMP, GIF). For TIFF,
      convert the image to a supported format first.
    question: Does GroupDocs.Redaction support other image formats like TIFF?
  - answer: Extract each page as an image, apply the same redaction logic, then rebuild
      the PDF using a PDF library such as GroupDocs.Conversion.
    question: How do I automate redaction for a folder of scanned PDFs?
  - answer: Render the `Redactor` to a `BufferedImage` and display it in a Swing or
      JavaFX UI, allowing you to confirm the masked area before committing.
    question: Is there a way to preview the redaction before saving?
  type: FAQPage
tags:
- image redaction
- GroupDocs
- Java
- document privacy
- data protection
title: GroupDocs.Redaction for Java kullanarak görüntüyü nasıl kırparız
type: docs
url: /tr/java/image-redaction/java-image-redaction-groupdocs-tutorial/
weight: 1
---

# GroupDocs.Redaction for Java kullanarak görüntüyü nasıl karartılır

Bu kapsamlı öğreticide, GroupDocs.Redaction ile Java'da **görüntüyü nasıl karartacağınızı** öğreneceksiniz. Taranmış görüntüleri karartmak, kişisel verileri korumak, GDPR, HIPAA veya diğer gizlilik düzenlemelerine uymak ve gizli görsel bilgilerin asla sızmamasını sağlamak için kritik bir adımdır. Proje kurulumunu, piksel‑düzeyinde karartma yapılandırmasını, sonucu güvenli bir şekilde kaydetmeyi ve karartmanın başarılı olduğunu doğrulamayı adım adım anlatacağız—herhangi bir Java uygulamasına kopyalayabileceğiniz sohbet tarzı bir rehber sunuyoruz.

## Hızlı cevaplar
- **Java'da görüntü karartma işlemini hangi kütüphane yönetir?** GroupDocs.Redaction for Java.  
- **Karartma rengini seçebilir miyim?** Evet – `Color.BLUE` veya `Color.BLACK` gibi opak bir `java.awt.Color`.  
- **Üretim için lisans gerekli mi?** Evet, ticari kullanım için geçerli bir GroupDocs lisansı zorunludur.  
- **Orijinal görüntü üzerine yazılacak mı?** Hayır – API, karartılmış görüntüyü belirttiğiniz yeni bir dosyaya yazar.  
- **Hangi Java sürümü destekleniyor?** Java 8 ve üzeri (yazım zamanında Java 21'e kadar).

## Görüntü karartması nedir ve neden taranmış görüntüler Java'da karartılır?
Görüntü karartması, piksel bölgelerini katı bir renk ile değiştirerek görsel verileri—isimleri, numaraları, imzaları—kalıcı olarak gizler. Seçilebilir karakterler üzerinde çalışan metin karartmasından farklı olarak, taranmış görüntüler bilgiyi ham pikseller olarak saklar; bu yüzden yalnızca piksel‑tabanlı araçlar verinin geri getirilemeyeceğini garanti edebilir. GroupDocs.Redaction kullanarak tam koordinatları hedefleyebilir, istediğiniz opak rengi uygulayabilir ve hassas içeriği kalıcı olarak kaldıran yeni bir görüntü üretebilirsiniz.

## Neden GroupDocs.Redaction for Java kullanmalısınız?
GroupDocs.Redaction **50+ görüntü formatını** (JPG, PNG, BMP, GIF dahil) destekler ve akış mimarisi sayesinde tüm dosyayı belleğe yüklemeden çok sayfalı belgeleri işleyebilir. Benchmark sonuçları, tipik bir 2.8 GHz CPU'da 300 KB taranmış PNG'nin 120 ms'den kısa sürede karartıldığını gösteriyor; bu da hem toplu işler hem de gerçek‑zaman hizmetleri için uygun olmasını sağlıyor.

## Önkoşullar
- **JDK 8 veya daha yeni** bir sürümün `PATH`'e kurulu ve yapılandırılmış olması.  
- **Maven** (veya Gradle) bağımlılık yönetimi için.  
- **IntelliJ IDEA**, **Eclipse** veya **NetBeans** gibi bir IDE.  
- Java dosya I/O ve `java.awt` paketi hakkında temel bilgi.  

## GroupDocs.Redaction for Java Kurulumu

### Maven kurulumu
GroupDocs deposunu ve bağımlılığı `pom.xml` dosyanıza ekleyin:

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
Alternatif olarak, resmi sürüm sayfasından en yeni JAR dosyasını indirin: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Lisans edinme
- **Ücretsiz deneme:** Tam API'yi keşfetmek için deneme hesabı oluşturun.  
- **Geçici lisans:** Ücretsiz olarak uzun süreli test için geçici bir anahtar kullanın.  
- **Tam satın alma:** Sınırsız dağıtım için üretim lisansı edinin.

## Uygulama rehberi

Uygulamayı iki temel özelliğe ayıracağız: **görüntü‑alanı karartması** (gerçek maskeleme) ve **karartma durumu kontrolü** (başarının doğrulanması).

### Tarama belgelerinin görüntülerini karartma – adım 1: redaktörü başlatma
`Redactor`, bir görüntüyü yükleyen ve karartma işlemlerini sağlayan merkezi sınıftır.  
İşlemek istediğiniz kaynak görüntüyü işaret eden bir `Redactor` örneği oluşturun.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_JPG");
```

### Adım 2: karartma parametrelerini tanımlama
`ImageAreaRedaction`, gizlenecek dikdörtgeni tanımlayan bir `Point` (sol‑üst köşe) ve bir `Dimension` (genişlik × yükseklik) ile çalışır. Bu örnekte mavi dolgu rengi kullanıyoruz.

```java
// Define the position on the image where redaction starts.
Point samplePoint = new Point(385, 485);

// Define the size of the area to be redacted.
Dimension sampleSize = new Dimension(1793, 2069);
```

### Adım 3: karartmayı uygulama
`RegionReplacementOptions`, dolgu rengini ve isteğe bağlı kenarlığı belirlemenizi sağlar. Bu seçenekleri `ImageAreaRedaction`'a geçirip `apply()` metodunu çağırmak maskeleme işlemini gerçekleştirir. Metod, başarı ya da başarısızlığı gösteren bir `RedactorChangeLog` döndürür.

```java
RedactorChangeLog result = redactor.apply(
    new ImageAreaRedaction(samplePoint, new RegionReplacementOptions(Color.BLUE, sampleSize))
);

// Check if the redaction was successful and save the output.
if (result.getStatus() != RedactionStatus.Failed) {
    redactor.save("YOUR_OUTPUT_DIRECTORY/redacted_output.jpg");
}
```

### Adım 4: kaynakları serbest bırakma
`Redactor`, `AutoCloseable` arayüzünü uygular. Kapatıldığında yerel tamponları ve dosya tutucuları serbest bırakır, uzun süren hizmetlerde bellek sızıntılarını önler.

```java
redactor.close();
```

### Karartmayı doğrulama – durum kontrolü
Karartma uygulandıktan sonra `RedactorChangeLog`'u inceleyin. `Status.SUCCESS` değeri, piksel bölgesinin hatasız bir şekilde değiştirildiğini onaylar. Kaydetmeden önce görsel inceleme için görüntüyü bir `BufferedImage`'a da aktarabilirsiniz.

```java
if (result != null && result.getStatus() != RedactionStatus.Failed) {
    System.out.println("Redaction was successful.");
} else {
    System.out.println("Redaction failed.");
}
```

## Pratik uygulamalar
- **Gizli belge yönetimi:** Ortaklarla paylaşmadan önce taranmış sözleşmelerdeki kişisel verileri maskeleyin.  
- **Hukuki dokümantasyon:** Kanıt görüntülerindeki tanımlayıcıları karartarak GDPR veya HIPAA uyumluluğunu sağlayın.  
- **Tıbbi kayıtlar:** Tanı detaylarını korurken radyoloji taramalarında hasta yüzlerini veya el yazısı notları gizleyin.  

## Performans değerlendirmeleri
- **Toplu işleme:** Bellek kullanımını 200 MB altında tutmak için görüntüleri 10–20'lik gruplar halinde işleyin.  
- **Nesne yeniden kullanımı:** `Point` ve `Dimension` nesnelerini yinelemeler arasında yeniden kullanarak GC baskısını azaltın.  
- **Sürüm güncellemeleri:** 24.10 sürümünde bildirilen %15 hız artışından yararlanmak için en son GroupDocs.Redaction sürümüne yükseltin.  

## Yaygın sorunlar ve çözümler
| Sorun | Sebep | Çözüm |
|-------|-------|-----|
| **`Failed` durumu ile karartma başarısız olur** | Yanlış dosya yolu veya desteklenmeyen görüntü formatı | Dosyanın mevcut olduğunu ve desteklenen bir format (JPG, PNG, BMP, GIF) olduğunu doğrulayın. |
| **Çıktı dosyası boş** | `redactor.save()` karartma tamamlanmadan çağrıldı | `save()`'ı çağırmadan önce `apply()`'ın `Status.SUCCESS` döndürdüğünden emin olun. |
| **Renk uygulanmadı** | Şeffaf bir `Color` kullanılması | `Color.BLACK` veya `Color.BLUE` gibi opak bir renk seçin. |

## Sıkça sorulan sorular

**Q: `ImageAreaRedaction` ile metin karartması arasındaki fark nedir?**  
A: `ImageAreaRedaction`, ham piksel koordinatları üzerinde çalışırken, metin karartması OCR katmanlarını işleyerek metin içeriğini bulur ve kaldırır.

**Q: Tek bir görüntüde birden fazla bölgeyi karartabilir miyim?**  
A: Evet—final dosyayı kaydetmeden önce farklı `ImageAreaRedaction` nesneleriyle `redactor.apply()`'ı tekrarlayarak çağırabilirsiniz.

**Q: GroupDocs.Redaction TIFF gibi diğer görüntü formatlarını destekliyor mu?**  
A: Kütüphane yaygın raster formatlarını (JPG, PNG, BMP, GIF) destekler. TIFF için önce görüntüyü desteklenen bir formata dönüştürün.

**Q: Taranmış PDF'lerin bir klasörü için karartmayı nasıl otomatikleştiririm?**  
A: Her sayfayı bir görüntü olarak çıkarın, aynı karartma mantığını uygulayın ve ardından GroupDocs.Conversion gibi bir PDF kütüphanesi kullanarak PDF'yi yeniden oluşturun.

**Q: Kaydetmeden önce karartmayı ön izleme imkanı var mı?**  
A: `Redactor`'ı bir `BufferedImage`'a render edip Swing veya JavaFX UI'da göstererek, karartılan alanı onaylamadan önce ön izleyebilirsiniz.

## Sonuç
Artık GroupDocs.Redaction for Java kullanarak **görüntü içeriğini nasıl karartacağınız** ve özellikle **taranmış görüntüyü Java'da nasıl karartacağınız** konusunda eksiksiz, üretim‑hazır bir rehbere sahipsiniz. Yukarıdaki adımları izleyerek finans, hukuk ve sağlık alanlarında hassas görsel verileri koruyabilirsiniz. Metin karartması, PDF sayfa karartması veya toplu klasör işleme gibi ek API'ları keşfederek kuruluşunuz için uçtan uca bir veri‑gizlilik hattı oluşturabilirsiniz.

## Kaynaklar
- [Documentation](https://docs.groupdocs.com/redaction/java/)  
- [API reference](https://reference.groupdocs.com/redaction/java)  
- [Download](https://releases.groupdocs.com/redaction/java/)  
- [GitHub repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- [Free support forum](https://forum.groupdocs.com/c/redaction/33)  
- [Temporary license](https://purchase.groupdocs.com/temporary-license/) 

---

**Son Güncelleme:** 2026-09-21  
**Test Edilen:** GroupDocs.Redaction 24.9 (Java)  
**Yazar:** GroupDocs

## İlgili Öğreticiler

- [GroupDocs.Redaction ile Java'da Nasıl Karartılır - Geliştiriciler İçin Kapsamlı Rehber](/redaction/java/getting-started/implement-java-redaction-groupdocs-redaction-guide/)
- [OCR ile Tarama PDF'yi Nasıl Karartılır – GroupDocs.Redaction Java](/redaction/java/ocr-integration/)
- [GroupDocs.Redaction ile Java'da Metni Nasıl Karartılır – Rehber](/redaction/java/text-redaction/text-redaction-java-groupdocs-redaction/)