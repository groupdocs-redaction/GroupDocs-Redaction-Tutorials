---
date: '2026-11-02'
description: Maven, streaming load, annotation deletion ve save options kullanarak
  GroupDocs redaction Java öğreticisinde dosya adına ek eklemeyi öğrenin.
keywords:
- groupdocs redaction java tutorial
- add suffix filename java
- document redaction workflow
- groupdocs maven dependency
- java inputstream redaction
lastmod: '2026-11-02'
og_description: GroupDocs redaction Java öğreticisinde dosya adına ek eklemeyi öğrenin.
  Adım adım Maven kurulumu, streaming load ve save options izleyin.
og_image_alt: Guide showing Java code to add suffix to redacted filenames using GroupDocs
  Redaction
og_title: GroupDocs redaction Java'da dosya adına ek ekleme
schemas:
- author: GroupDocs
  dateModified: '2026-11-02'
  description: Learn how to add suffix to filename in a GroupDocs redaction Java tutorial
    using Maven, streaming load, annotation deletion, and save options.
  headline: How to add suffix to filename in GroupDocs redaction Java
  type: TechArticle
- description: Learn how to add suffix to filename in a GroupDocs redaction Java tutorial
    using Maven, streaming load, annotation deletion, and save options.
  name: How to add suffix to filename in GroupDocs redaction Java
  steps:
  - name: '1: Create InputStream'
    text: '- **Why:** Using `InputStream` allows you to handle documents stored in
      various locations—cloud buckets, databases, or in‑memory buffers—without first
      writing them to disk. This approach is essential when you need to **load document
      from stream** in micro‑service architectures.'
  - name: '1: Apply DeleteAnnotationRedaction'
    text: '- **Why:** This step ensures that any sensitive annotations (comments,
      highlights, or hidden notes) are stripped from the document, enhancing privacy
      and compliance.'
  - name: '1: Configure SaveOptions'
    text: '- **Why:** Customizing save options allows flexible output formats and
      naming conventions. Enabling `setAddSuffix(true)` **adds suffix to filename**,
      making it clear that the file has been redacted.'
  type: HowTo
- questions:
  - answer: Yes, the library supports PDFs, DOCX, PPTX, XLSX, and many other formats.
    question: Can I redact PDF documents using GroupDocs.Redaction?
  - answer: Use streaming (`load document from stream`) and close resources promptly
      to keep memory usage low.
    question: What is the best way to handle large files with GroupDocs.Redaction?
  - answer: The API automatically adds a default suffix (e.g., “_redacted”). For custom
      suffixes, rename the output file after saving.
    question: Is it possible to customize the suffix text?
  - answer: Visit the [Temporary License page](https://purchase.groupdocs.com/temporary-license/)
      and follow the instructions.
    question: How do I obtain a temporary license for GroupDocs.Redaction?
  - answer: Join the [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33)
      for expert assistance.
    question: Where can I get help if I encounter issues?
  type: FAQPage
tags:
- groupdocs redaction
- java tutorial
- maven dependency
- document redaction
title: GroupDocs redaction Java'da dosya adına ek ekleme
type: docs
url: /tr/java/advanced-redaction/master-document-redaction-groupdocs-redaction-java/
weight: 1
---

# GroupDocs Redaction Java'da dosya adına sonek ekleme

Bu **groupdocs redaction java tutorial**'da, GroupDocs.Redaction ile belgeleri karartırken çıktı dosya adına otomatik olarak bir sonek eklemeyi öğreneceksiniz. Sonek eklemek manuel yeniden adlandırmayı ortadan kaldırır, karartılmamış dosyaların sızdırılma riskini azaltır ve adlandırma kurallarına dayalı CI/CD boru hatlarına sorunsuz şekilde uyar. Kılavuz, Maven kurulumu, akış belge yükleme, ek açıklama kaldırma ve kaydetme seçeneklerini yapılandırma adımlarını—kısa ve üretim‑hazır kodla—size gösterir.

## Hızlı cevaplar
- **“add suffix to filename” ne yapar?**  
  Sonek seçeneğini etkinleştirdiğinizde, SDK otomatik olarak önceden tanımlanmış bir dizeyi (varsayılan olarak “_redacted”) çıktı dosyasının uzantıdan önceki temel adına ekler. Bu, hangi dosyaların işlendiğini hemen gösterir, orijinal içeriğin yanlışlıkla dağıtılmasını önlemeye yardımcı olur ve adlandırma desenlerine dayalı sonraki otomasyonu basitleştirir.  
- **Bir belgeyi akıştan (stream) yükleyebilir miyim?**  
  Evet—GroupDocs.Redaction, herhangi bir `InputStream`'den yüklemeyi destekler, bulut depolama veya bellek içi işleme için mükemmeldir.  
- **Bu özellik için lisansa ihtiyacım var mı?**  
  Ücretsiz deneme, temel karartma için çalışır; geçici veya tam lisans, sonek işleme dahil tüm gelişmiş seçeneklerin kilidini açar.  
- **Hangi formatlar destekleniyor?**  
  Kütüphane DOCX, PDF, PPTX, XLSX ve daha birçok formatı işler.  
- **PDF çıktısı için rasterleştirme gerekli mi?**  
  Rasterleştirme isteğe bağlıdır; belgeyi ekstra güvenlik için düzleştirmeniz gerektiğinde etkinleştirin.

## “add suffix to filename” ne yapar?

Sonek seçeneğini etkinleştirdiğinizde, SDK otomatik olarak önceden tanımlanmış bir dizeyi (varsayılan olarak “_redacted”) çıktı dosyasının uzantıdan önceki temel adına ekler. Bu, hangi dosyaların işlendiğini hemen gösterir, orijinal içeriğin yanlışlıkla dağıtılmasını önlemeye yardımcı olur ve adlandırma desenlerine dayalı sonraki otomasyonu basitleştirir.

## Bu görev için neden GroupDocs.Redaction kullanılmalı?

GroupDocs.Redaction, otomatik sonek ekleme, akış desteği ve toplu işleme gibi esnek dosya işleme seçenekleriyle karartma eylemlerini birleştiren yüksek performanslı bir Java API'si sunar. 50'den fazla giriş ve çıkış formatını destekler ve tüm dosyayı belleğe yüklemeden çok sayfalı belgeleri işleyebilir, düşük bellek kullanımı ve hızlı yürütme sağlar.

## Önkoşullar

- **Java Development Kit (JDK):** Versiyon 8 veya üzeri.  
- **GroupDocs.Redaction Library:** Karartma görevleri için çekirdek kütüphane.  
- **IDE:** IntelliJ IDEA, Eclipse veya herhangi bir Java‑uyumlu editör.  
- **Maven:** Bağımlılık yönetimi için.  

### Bilgi önkoşulları
Java I/O ve temel nesne‑yönelimli kavramlara aşina olmak, örnekleri daha kolay takip etmenizi sağlar.

## Java için GroupDocs.Redaction kurulumu

### Maven kurulumu
`pom.xml` dosyanıza aşağıdaki yapılandırmayı ekleyerek Maven üzerinden GroupDocs kütüphanelerine erişin:

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
Alternatif olarak, en son sürümü doğrudan [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) adresinden indirin.

### Lisans edinimi
1. **Free trial:** Sınırlama olmadan temel işlevselliğe erişim.  
2. **Temporary license:** Gelişmiş özellikleri keşfetmek için geçici lisans alın.  
3. **Purchase:** Uzun vadeli kullanım için tam lisans satın almayı düşünün.

#### Temel başlatma ve kurulum
Gerekli içe aktarmaları ekleyerek projenizi başlatın:

```java
import com.groupdocs.redaction.Redactor;
```

Bu kurulumla, belge karartma işlevlerini uygulamaya hazır olacaksınız.

## Uygulama rehberi

### Özellik 1: belgeyi akıştan yükleme
**Genel Bakış:** Belgeleri işleme için bir `InputStream` içine nasıl yükleyeceğinizi öğrenin.

`InputStream`, bayt akışını temsil eden bir Java I/O sınıfıdır ve dosyalardan, ağ bağlantılarından veya diğer kaynaklardan tüm içeriği belleğe yüklemeden veri okumanıza olanak tanır.

#### Adım 1.1: inputstream oluşturma

```java
import java.io.FileInputStream;
import java.io.InputStream;

try (InputStream stream = new FileInputStream("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    final Redactor redactor = new Redactor(stream);
    try {
        // Document is now loaded and ready for further processing
    } finally {
        redactor.close();
    }
}
```

- **Neden:** `InputStream` kullanmak, belgeleri çeşitli konumlardan—bulut depoları, veritabanları veya bellek içi tamponlar—diskte önceden kaydetmeden işlemeyi sağlar. Bu yaklaşım, mikro‑servis mimarilerinde **load document from stream** gerektiğinde esastır.

### Özellik 2: ek açıklama silme karartması uygulama
**Genel Bakış:** `DeleteAnnotationRedaction` kullanarak belgenizden ek açıklamaları kaldırın.

`DeleteAnnotationRedaction`, belgede bulunan tüm ek açıklamaları—yorumlar, vurgulamalar ve notlar gibi—kaldıran bir karartma işlemidir.

#### Adım 2.1: deleteannotationredaction uygulama

```java
import com.groupdocs.redaction.redactions.DeleteAnnotationRedaction;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply the DeleteAnnotationRedaction to remove annotations from the document
    redactor.apply(new DeleteAnnotationRedaction());
}
```

- **Neden:** Bu adım, hassas ek açıklamaların (yorumlar, vurgulamalar veya gizli notlar) belgeden temizlenmesini sağlar, gizliliği ve uyumluluğu artırır.

### Özellik 3: belgeyi seçeneklerle kaydetme
**Genel Bakış:** İşlenmiş belgenizi rasterleştirme ve **add suffix filename java** gibi belirli seçeneklerle nasıl kaydedeceğinizi öğrenin.

`SaveOptions`, karartılmış belgenin nasıl yazılacağını kontrol eden ayarları kapsar; format, rasterleştirme ve adlandırma kuralları dahil.

#### Adım 3.1: saveoptions yapılandırma

```java
import java.io.ByteArrayOutputStream;
import com.groupdocs.redaction.options.SaveOptions;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply necessary redactions before saving
    redactor.apply(new DeleteAnnotationRedaction());
    try (ByteArrayOutputStream bA = new ByteArrayOutputStream()) {
        SaveOptions options = new SaveOptions();
        options.setRasterizeToPDF(true);  // Option to rasterize document to PDF format
        options.setAddSuffix(true);      // Option to add a suffix to the saved file name
        redactor.save(bA, options.getRasterization());
    }
}
```

- **Neden:** Kaydetme seçeneklerini özelleştirmek, esnek çıktı formatları ve adlandırma kuralları sağlar. `setAddSuffix(true)` etkinleştirildiğinde **adds suffix to filename**, dosyanın karartıldığını açıkça gösterir.

## Belge kaydederken suffix filename java nasıl eklenir?

`Redactor` sınıfı, bir belgeyi yükleyen ve karartma işlemlerini uygulayan temel bileşendir. `SaveOptions`, karartılmış belgenin nasıl kaydedileceğini tanımlar; format, rasterleştirme ve adlandırma kuralları dahil. Bir `Redactor` örneği oluşturun, gerekli karartmaları uygulayın, ardından `setAddSuffix(true)` ile bir `SaveOptions` nesnesi yapılandırın. `redactor.save(outputPath, options)` çağrısını yapın. SDK, dosya adına otomatik olarak “_redacted” (veya yapılandırılmış sonek) ekler, böylece dosyayı manuel olarak yeniden adlandırmanız gerekmez.

## GroupDocs Maven bağımlılığı genel bakışı

**groupdocs maven dependency**, tek bir `<dependency>` girişiyle tüm Redaction SDK'sını projenize getirir. Geçişli bağımlılıkları yönetir, kütüphaneleri güncel tutar ve derleme otomasyonunu basitleştirir. `pom.xml` içinde bağımlılığı bildirerek, manuel JAR yönetiminden kaçınır ve en son güvenlik yamalarıyla uyumluluğu sağlarsınız.

## Sonek eklemenin önemi

Sonek eklemek, bir dosyanın işlendiğine dair anında görsel bir doğrulama sağlar; bu, denetim izleri, otomatik iş akışları ve düzenleyici uyumluluk için kritiktir. Betikler karartılmış dosyaları filtreleyebilir, orijinal içeriğin yanlışlıkla dağıtılmasını önler ve temizlenmiş belgelerin net etiketlenmesini gerektiren birçok sektör standardını karşılar.

## Pratik uygulamalar

Bu gerçek dünya kullanım senaryolarını keşfedin:

1. **Hukuki belge karartma:** Müşteri paylaşımından önce sözleşmeleri güvenli hale getirin.  
2. **Tıbbi kayıt yönetimi:** Klinik verileri korurken hasta kimlik bilgilerini koruyun.  
3. **Finansal raporlama:** Dış denetimler sırasında hassas sayıları gizli tutun.  
4. **CRM entegrasyonu:** Üçüncü taraf araçlara dışa aktarım öncesinde müşteri verilerini otomatik olarak karartın.  
5. **İş birliği araçları:** Paylaşılan taslakların gizli yorumları veya meta verileri asla ortaya çıkarmadığından emin olun.

## Performans değerlendirmeleri

### Performansı optimize etme
- Akışı kullanın (`load document from stream`) tüm dosyaları belleğe yüklemekten kaçınmak için.  
- `Redactor` örneklerini hızlıca kapatarak kaynakları serbest bırakın.  

### Kaynak kullanımı yönergeleri
- Toplu çalıştırmalar sırasında CPU ve belleği izleyin.  
- Orta boyutlu dosyalarla çalışırken bellek içi kaydetmeler için `ByteArrayOutputStream` tercih edin.  

### Java bellek yönetimi için en iyi uygulamalar
- Aynı tipte birden fazla dosya işlerken `Redactor` nesnelerini yeniden kullanın.  
- `close()` metodunu bir `try‑with‑resources` bloğunda çağırarak sızıntıları önleyin.

## Yaygın sorunlar ve çözümler
| Issue | Cause | Fix |
|-------|-------|-----|
| **Sonek görünmüyor** | `setAddSuffix(false)` veya eksik çağrı | `save()`'den önce `options.setAddSuffix(true)` ayarlandığından emin olun. |
| **Büyük DOCX'te OutOfMemoryError** | Tüm dosyanın belleğe yüklenmesi | `InputStream` yüklemeye geçin (Özellik 1'e bakın). |
| **Ek açıklamalar hâlâ görünür** | Kaydetmeden önce karartma uygulanmamış | `save()`'den önce `redactor.apply(new DeleteAnnotationRedaction())` çağırın. |
| **PDF rasterleştirme uygulanmadı** | `setRasterizeToPDF(false)` veya atlanmış | Düzleştirilmiş PDF gerektiğinde `options.setRasterizeToPDF(true)` ayarlayın. |

## Sıkça sorulan sorular

**S: GroupDocs.Redaction ile PDF belgelerini karartabilir miyim?**  
C: Evet, kütüphane PDF, DOCX, PPTX, XLSX ve birçok diğer formatı destekler.

**S: GroupDocs.Redaction ile büyük dosyaları yönetmenin en iyi yolu nedir?**  
C: Akışı kullanın (`load document from stream`) ve bellek kullanımını düşük tutmak için kaynakları hızlıca kapatın.

**S: Sonek metnini özelleştirmek mümkün mü?**  
C: API, varsayılan bir sonek (ör. “_redacted”) otomatik ekler. Özel sonekler için, kaydettikten sonra çıktı dosyasını yeniden adlandırın.

**S: GroupDocs.Redaction için geçici lisansı nasıl elde edebilirim?**  
C: [Temporary License page](https://purchase.groupdocs.com/temporary-license/) adresini ziyaret edin ve talimatları izleyin.

**S: Sorunlarla karşılaşırsam nereden yardım alabilirim?**  
C: Uzman desteği için [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) forumuna katılın.

## Kaynaklar
- **Documentation:** Ayrıntılı kılavuzları [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/) adresinde keşfedin.  
- **API reference:** Kapsamlı API detaylarına [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java) adresinden erişin.  
- **Download:** En son sürümü [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/) adresinden alın.  
- **GitHub repository:** Katkıda bulunabilir veya kaynak kodunu [GroupDocs GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java) adresinde inceleyebilirsiniz.

---

**Son Güncelleme:** 2026-11-02  
**Test Edilen Versiyon:** GroupDocs.Redaction 24.9 for Java  
**Yazar:** GroupDocs  

## İlgili öğreticiler

- [Word'ü PDF'ye Dönüştür ve Karartılmış Belgeleri GroupDocs.Redaction Java ile Kaydet](/redaction/java/document-saving/)
- [GroupDocs.Redaction ile Java'da Belge Sayfalarını Önizleme](/redaction/java/document-loading/)
- [GroupDocs.Redaction Java için İleri Düzey Karartma Teknikleri](/redaction/java/advanced-redaction/)