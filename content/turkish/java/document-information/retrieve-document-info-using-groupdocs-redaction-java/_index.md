---
date: '2026-09-06'
description: GroupDocs.Redaction for Java ile dosya uzantısını almayı, belge boyutunu,
  sayfa sayısını ve PDF meta verilerini nasıl alacağınızı öğrenin. Java uygulamanızın
  belge işleme yeteneğini bugün artırın.
keywords:
- java get file extension
- java file type detection
- get document size java
- get page count java
- read pdf metadata java
lastmod: '2026-09-06'
og_description: GroupDocs.Redaction for Java ile dosya uzantısını, belge boyutunu,
  sayfa sayısını ve PDF meta verilerini nasıl alacağınızı keşfedin. Basit kod, hızlı
  sonuçlar.
og_image_alt: Guide showing Java code to extract file type, size, and page count using
  GroupDocs.Redaction
og_title: GroupDocs.Redaction kullanarak Java'da dosya uzantısını nasıl alırız
schemas:
- author: GroupDocs
  dateModified: '2026-09-06'
  description: Learn how to java get file extension, retrieve document size, page
    count, and PDF metadata with GroupDocs.Redaction for Java. Boost your Java app's
    document handling today.
  headline: How to java get file extension using GroupDocs.Redaction
  type: TechArticle
- description: Learn how to java get file extension, retrieve document size, page
    count, and PDF metadata with GroupDocs.Redaction for Java. Boost your Java app's
    document handling today.
  name: How to java get file extension using GroupDocs.Redaction
  steps:
  - name: import necessary classes
    text: 'Add the required imports at the top of your Java file:'
  - name: initialize the redactor
    text: The `Redactor` class is the core engine that opens a document and provides
      access to its metadata.
  - name: retrieve and display document info
    text: '`IDocumentInfo` provides the metadata you need. Call `getDocumentInfo()`
      once and then query the three properties. The three `System.out.println` statements
      output the file type, page count, and size in bytes—exactly the data you need
      for downstream processing.'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction is a Java library that enables redaction, metadata
      extraction, and format‑agnostic document processing across more than 50 file
      types.
    question: What is GroupDocs.Redaction?
  - answer: Yes, `IDocumentInfo` returns PDF version, encryption status, and basic
      metadata without extra code.
    question: Can I retrieve metadata from PDF files?
  - answer: Enclose the `getDocumentInfo()` call in a `try‑catch` block and handle
      `RedactionException` to manage corrupted or unsupported files.
    question: How do I handle exceptions when retrieving document info?
  - answer: File type, number of pages, size in bytes, PDF version, encryption flag,
      and basic author/creation metadata.
    question: What kind of information can I get about a document?
  - answer: Yes, instantiate a separate `Redactor` for each file inside a thread pool
      and reuse the same JVM to achieve high throughput.
    question: Is there support for batch‑processing many documents efficiently?
  type: FAQPage
tags:
- document metadata
- GroupDocs.Redaction
- Java file handling
title: GroupDocs.Redaction kullanarak Java'da dosya uzantısını nasıl alırız
type: docs
url: /tr/java/document-information/retrieve-document-info-using-groupdocs-redaction-java/
weight: 1
---

# GroupDocs.Redaction kullanarak java dosya uzantısını nasıl alırız

Modern Java uygulamalarında kullanıcı tarafından yüklenen dosyaları işleyenlerde, dosyanın tam türünü erken bilmek—**java get file extension**—yönlendirme, güvenlik ve kaynak planlaması için çok önemlidir. Bu öğreticide, java dosya uzantısını nasıl alacağınızı, belge boyutunu, sayfa sayısını ve hatta PDF meta verilerini GroupDocs.Redaction kütüphanesini kullanarak nasıl alacağınızı göstereceğiz. Sonunda, ihtiyacınız olan tüm temel özellikleri döndüren tek bir düşük bellekli çağrınız olacak.

## Hızlı cevaplar
- **Dosya türünü döndüren yöntem nedir?** `IDocumentInfo.getFileType()`
- **Sayfa sayısını nasıl alabilirim?** `IDocumentInfo.getPageCount()`
- **Hangi çağrı belge boyutunu bayt olarak verir?** `IDocumentInfo.getSize()`
- **Örneği çalıştırmak için lisansa ihtiyacım var mı?** A trial or temporary license works for evaluation.
- **Hangi Java sürümü gereklidir?** Java 8 or higher.

## “java get file extension” nedir?
**java get file extension**, Java’da bir belgeden dosya formatını (ör. DOCX, PDF) programlı olarak çıkarmak anlamına gelir. GroupDocs.Redaction bu bilgiyi `IDocumentInfo` arayüzü aracılığıyla sunar, böylece tek bir yöntem çağrısı uzantı dizesini döndürür.

## Metaveri çıkarımı için GroupDocs.Redaction neden kullanılmalı?
GroupDocs.Redaction, **50+** giriş formatından—PDF, DOCX, XLSX, PPTX ve görüntü türleri dahil—tüm dosyayı belleğe yüklemeden meta verileri okuyabilir. Tipik bir sunucuda 300 sayfalık bir PDF’i 200 ms’nin altında işleyerek RAM kullanımını 20 MB’nin altında tutar. Bu performans‑optimize yaklaşım, tüm desteklenen formatlarda tutarlı sonuçlar elde ederken toplu işleri ölçeklendirmenizi sağlar.

## Önkoşullar
- Java 8 veya daha yeni bir sürüm kurulu.
- Maven uyumlu bir IDE (IntelliJ IDEA, Eclipse vb.).
- GroupDocs.Redaction lisansına erişim (ücretsiz deneme veya geçici lisans).

## Java için GroupDocs.Redaction kurulumu

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
Alternatif olarak, en son sürümü [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) adresinden indirin.

#### Lisans edinme
- **Free trial:** Kütüphaneyi değerlendirmek için ücretsiz deneme ile başlayın.  
- **Temporary license:** Uzun vadeli değerlendirme için geçici bir lisans edinin.  
- **Purchase:** İhtiyacınıza uygunsa satın almayı düşünün.

## Gerçek dünya projelerinde java dosya uzantısını almanın önemi
Bir belgenin türünü yükleme anında bilmek, dosyaları doğru işleme hattına yönlendirmenizi sağlar—PDF’ler kırpma, Word dosyaları dönüştürme, görüntüler OCR için. Ayrıca güvenlik kontrollerini (çalıştırılabilir dosyaları engelleme) ve belge yönetim sistemlerinde doğru UI simgelerini mümkün kılar.

## java dosya uzantısını alma, belge boyutunu alma ve sayfa sayısını alma
Dosya türünü, boyutunu ve sayfa sayısını tek bir `IDocumentInfo` çağrısıyla alabilirsiniz. Bu çağrı yalnızca belge başlığını okur, bu yüzden büyük dosyalar bile hızlı ve minimum bellek kullanımıyla işlenir. Bu hafif yaklaşım, daha fazla işlem kararı vermeden önce yalnızca özet bilgilerin gerektiği toplu işleme için idealdir. `IDocumentInfo` arayüzü, tam belgeyi yüklemeden dosya türü, sayfa sayısı ve boyut gibi meta verileri sağlar.

### Adım 1: gerekli sınıfları içe aktar
Add the required imports at the top of your Java file:

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.domain.IDocumentInfo;
```

### Adım 2: redaktörü başlat
The `Redactor` class is the core engine that opens a document and provides access to its metadata.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
try {
    // Code for retrieving information will go here.
} finally {
    redactor.close();
}
```

### Adım 3: belge bilgisini al ve göster
`IDocumentInfo` provides the metadata you need. Call `getDocumentInfo()` once and then query the three properties.

```java
// Retrieve document information
IDocumentInfo info = redactor.getDocumentInfo();

// Output document type, page count, and size in bytes
System.out.println("File Type: " + info.getFileType());
System.out.println("Page Count: " + info.getPageCount());
System.out.println("Size (Bytes): " + info.getSize());
```

Üç `System.out.println` ifadesi dosya türünü, sayfa sayısını ve bayt cinsinden boyutu çıktılar—tam olarak sonraki işlemler için ihtiyacınız olan veriler.

## Java’da pdf meta verilerini alma
`Redactor` ile PDF’i yükleyin ve `getDocumentInfo()` çağırın. Aynı yöntem, sürüm ve şifreleme durumu gibi PDF’ye özgü alanları döndürür, bu yüzden ekstra kod gerekmez. Döndürülen `IDocumentInfo` nesnesi ayrıca sürüm numarası, şifreleme bayrağı ve standart meta veriler (yazar, başlık, oluşturma tarihi) gibi PDF’ye özgü alanları içerir. Bu özelliklere doğrudan getter metodlarıyla erişebilir, PDF detaylarını ek bir ayrıştırma yapmadan görüntüleyebilir veya kaydedebilirsiniz.

## Yaygın kullanım senaryoları
1. **Belge yönetim sistemleri:** Dosyaları depolamadan önce tür veya boyuta göre otomatik sınıflandırın.  
2. **İçerik işleme hatları:** Sayfa sayısına göre farklı işleme stratejileri seçin (ör. büyük PDF’leri toplu kırpma vs. küçük Word belgeleri).  
3. **Dijital varlık kütüphaneleri:** Kullanıcılara dosyayı açmadan belge özelliklerinin hızlı ön izlemelerini gösterin.

## Yaygın sorunlar ve çözümler
- **Dosya bulunamadı:** `Redactor`'a gönderdiğiniz mutlak veya göreli yolu doğrulayın.  
- **Desteklenmeyen format:** Belgenizin uzantısının GroupDocs.Redaction tarafından desteklenen 50+ format arasında listelendiğinden emin olun.  
- **Lisans hataları:** Geçerli bir deneme veya kalıcı lisans kullanın; aksi takdirde API bir lisanslama istisnası fırlatır.

## Sorun giderme ipuçları (belge meta verilerini okuma java)
- Meta veri çağrılarını `try‑catch` bloğuna sararak bozuk dosyaları sorunsuz şekilde ele alın.  
- Meta verileri okumadan önce şifreli PDF’leri tespit etmek için `redactor.isEncrypted()` (varsa) kullanın.  
- Çok sayıda dosya işlenirken bir thread‑pool yeniden kullanın ve her `Redactor` örneğini dosya‑tanıtıcı sızıntılarını önlemek için hemen kapatın.

## Performans değerlendirmeleri
Büyük toplu işlemlerle çalışırken:
- Dosya tanıtıcılarının zamanında serbest bırakılmasını sağlamak için her belgeyi `try‑with‑resources` bloğunda açın.  
- Sadece ihtiyacınız olan meta verileri önbelleğe alın; gerekmedikçe tam belge içeriğini yüklemekten kaçının.

## Sıkça sorulan sorular
**S: GroupDocs.Redaction nedir?**  
C: GroupDocs.Redaction, 50'den fazla dosya türü üzerinde kırpma, meta veri çıkarımı ve format‑bağımsız belge işleme sağlayan bir Java kütüphanesidir.

**S: PDF dosyalarından meta veri alabilir miyim?**  
C: Evet, `IDocumentInfo` ek kod olmadan PDF sürümü, şifreleme durumu ve temel meta verileri döndürür.

**S: Belge bilgisi alırken istisnaları nasıl ele alırım?**  
C: `getDocumentInfo()` çağrısını bir `try‑catch` bloğuna sarın ve bozuk veya desteklenmeyen dosyaları yönetmek için `RedactionException`'ı yakalayın.

**S: Bir belge hakkında ne tür bilgiler alabilirim?**  
C: Dosya türü, sayfa sayısı, bayt cinsinden boyut, PDF sürümü, şifreleme bayrağı ve temel yazar/oluşturma meta verileri.

**S: Birçok belgeyi verimli bir şekilde toplu işleme desteği var mı?**  
C: Evet, bir thread pool içinde her dosya için ayrı bir `Redactor` örneği oluşturun ve yüksek verimlilik için aynı JVM'yi yeniden kullanın.

## Sonuç
Artık GroupDocs.Redaction kullanarak **java dosya uzantısını alma**, **belge boyutunu alma java**, **sayfa sayısını alma java** ve **pdf meta verilerini alma java** konularını biliyorsunuz. Bu kod parçacıklarını Java uygulamalarınıza entegre ederek belge işleme konusunda daha akıllı kararlar alın, performansı artırın ve daha zengin kullanıcı deneyimleri sunun.

---

**Last Updated:** 2026-09-06  
**Tested With:** GroupDocs.Redaction 24.9 for Java  
**Author:** GroupDocs  

**Kaynaklar**  
- **Dokümantasyon:** [GroupDocs Redaction Java Documentation](https://docs.groupdocs.com/redaction/java/)  
- **API referansı:** [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java)  
- **İndirme:** [GroupDocs.Redaction for Java Downloads](https://releases.groupdocs.com/redaction/java/)  
- **GitHub:** [GroupDocs GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **Ücretsiz destek:** [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)  
- **Geçici lisans:** [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license/)

```java
import com.groupdocs.redaction.Redactor;

// Initialize Redactor with the path to your document
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

## İlgili Eğitimler

- [java dosya meta verilerini okuma – GroupDocs.Redaction ile dosya türü](/redaction/java/metadata-redaction/groupdocs-redaction-java-document-metadata-extraction/)
- [Önizleme ve Belge Sayfa Sayısını Oluşturma – GroupDocs Java](/redaction/java/document-information/)
- [Java için GroupDocs.Redaction ile Sayfa Önizleme – Kapsamlı Rehber](/redaction/java/document-loading/load-preview-document-pages-groupdocs-redaction-java/)