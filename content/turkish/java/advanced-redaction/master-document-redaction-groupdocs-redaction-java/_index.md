---
date: '2026-05-22'
description: GroupDocs Maven bağımlılığını kullanarak belgeleri karartırken java dosya
  adı son ekini nasıl ekleyeceğinizi öğrenin. Streaming load, annotation deletion
  ve save options içerir.
keywords:
- add suffix filename java
- groupdocs redaction java
- document redaction workflow
schemas:
- author: GroupDocs
  dateModified: '2026-05-22'
  description: Learn how to add suffix filename java using the GroupDocs Maven dependency
    while redacting documents. Includes streaming load, annotation deletion, and save
    options.
  headline: Add suffix filename java with GroupDocs Maven
  type: TechArticle
- description: Learn how to add suffix filename java using the GroupDocs Maven dependency
    while redacting documents. Includes streaming load, annotation deletion, and save
    options.
  name: Add suffix filename java with GroupDocs Maven
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
title: GroupDocs Maven ile java dosya adı son ekini ekle
type: docs
url: /tr/java/advanced-redaction/master-document-redaction-groupdocs-redaction-java/
weight: 1
---

# GroupDocs Maven ile java dosya adına ek ek ekle

Gizli verileri kırpma sadece mücadelenin yarısıdır—kaydedilen dosyanın işlendiğini açıkça gösterdiğinden de emin olmalısınız. **GroupDocs Maven bağımlılığını kullanmak bunu basitleştirir**, çıktı dosya adına sadece birkaç satır kodla bir ek eklemenizi sağlar. **add suffix filename java** yöntemi, kırpılmış dosyalarınızı anında etiketleyen tek satırlık bir yapılandırmadır ve uyumluluğunuzu ve denetim hazırlığınızı artırır.

## Hızlı Yanıtlar
- **“add suffix to filename” ne yapar?**  
  Çıktı dosya adına özel bir ek (ör. “_redacted”) ekler, böylece işlenmiş dosyaları anında tanımlayabilirsiniz.  
- **Belgeyi akıştan yükleyebilir miyim?**  
  Evet—GroupDocs.Redaction, herhangi bir `InputStream`'den yüklemeyi destekler, bulut depolama veya bellek içi işleme için mükemmeldir.  
- **Bu özellik için lisansa ihtiyacım var mı?**  
  Ücretsiz deneme temel kırpma için çalışır; geçici veya tam lisans, ek ekleme dahil tüm gelişmiş seçeneklerin kilidini açar.  
- **Hangi formatlar destekleniyor?**  
  Kütüphane DOCX, PDF, PPTX, XLSX ve daha birçok formatı işler.  
- **PDF çıktısı için rasterizasyon gerekli mi?**  
  Rasterizasyon isteğe bağlıdır; belgeyi ekstra güvenlik için düzleştirmeniz gerektiğinde etkinleştirin.

## add suffix filename java nedir?
**add suffix filename java** tekniği, kaydetme işlemi sırasında dosya adına önceden tanımlı bir dize ekleyerek belgeyi kırpılmış olarak işaretler. Bu basit konvansiyon, orijinal, kırpılmamış dosyaların yanlışlıkla dağıtılmasını önler ve otomatik iş akışlarıyla sorunsuz bir şekilde bütünleşir.

## Bu görev için neden GroupDocs.Redaction kullanılmalı?
GroupDocs.Redaction, **add suffix filename java** gibi dosya işleme seçeneklerini kırpma eylemleriyle birleştirmenizi sağlayan akıcı bir Java API'si sunar. SDK, **50+ giriş ve çıkış formatı** destekler ve tüm dosyayı belleğe yüklemeden çok sayfalı belgeleri işleyebilir, böylece yüksek hız ve düşük bellek tüketimi sağlar.

## Önkoşullar

- **Java Development Kit (JDK):** Sürüm 8 veya üzeri.  
- **GroupDocs.Redaction Library:** Kırpma görevleri için temel kütüphane.  
- **IDE:** IntelliJ IDEA, Eclipse veya herhangi bir Java‑uyumlu editör.  
- **Maven:** Bağımlılık yönetimi için.  

### Bilgi Önkoşulları
Java I/O ve temel nesne‑yönelimli kavramlara aşina olmak, örnekleri daha kolay takip etmenizi sağlar.

## Java için GroupDocs.Redaction Kurulumu
### Maven Kurulumu
GroupDocs kütüphanelerine Maven aracılığıyla erişmek için `pom.xml` dosyanıza aşağıdaki yapılandırmayı ekleyin:

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
Alternatif olarak, en son sürümü doğrudan [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) adresinden indirebilirsiniz.

### Lisans Edinme
1. **Ücretsiz Deneme:** Temel işlevselliğe kısıtlama olmadan erişin.  
2. **Geçici Lisans:** Gelişmiş özellikleri keşfetmek için geçici bir lisans alın.  
3. **Satın Alma:** Uzun vadeli kullanım için tam lisans satın almayı düşünün.

#### Temel Başlatma ve Kurulum
Gerekli ithalatları ekleyerek projenizi başlatın:

```java
import com.groupdocs.redaction.Redactor;
```

Bu kurulumla, belge kırpma işlevlerini uygulamaya hazır olacaksınız.

## Uygulama Kılavuzu

### Özellik 1: Belgeyi Akıştan Yükleme
**Overview:** İşleme için belgeleri bir `InputStream` içine nasıl yükleyeceğinizi öğrenin.

#### Adım Adım Uygulama
##### Adım 1.1: InputStream Oluşturma

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

- **Why:** `InputStream` kullanmak, belgeleri çeşitli konumlardan—bulut kovaları, veritabanları veya bellek içi tamponlar—diskte önceden kaydetmeden yönetmenizi sağlar. Bu yaklaşım, mikro‑servis mimarilerinde **load document from stream** gerektiğinde esastır.

### Özellik 2: Açıklama Silme Kırpması Uygulama
**Overview:** `DeleteAnnotationRedaction` kullanarak belgenizden açıklamaları kaldırın.

#### Adım Adım Uygulama
##### Adım 2.1: DeleteAnnotationRedaction Uygulama

```java
import com.groupdocs.redaction.redactions.DeleteAnnotationRedaction;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply the DeleteAnnotationRedaction to remove annotations from the document
    redactor.apply(new DeleteAnnotationRedaction());
}
```

- **Why:** Bu adım, hassas açıklamaların (yorumlar, vurgulamalar veya gizli notlar) belgeden temizlenmesini sağlayarak gizliliği ve uyumluluğu artırır.

### Özellik 3: Seçeneklerle Belgeyi Kaydet
**Overview:** Rasterizasyon ve **add suffix filename java** gibi belirli seçeneklerle işlenmiş belgenizi nasıl kaydedeceğinizi öğrenin.

#### Adım Adım Uygulama
##### Adım 3.1: SaveOptions Yapılandırma

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

- **Why:** Kaydetme seçeneklerini özelleştirmek, esnek çıktı formatları ve adlandırma kuralları sağlar. `setAddSuffix(true)` etkinleştirildiğinde **adds suffix to filename**, dosyanın kırpılmış olduğunu açıkça gösterir.

## Belge kaydederken add suffix filename java nasıl eklenir?
`Redactor`, bir belgeyi yükleyen ve kırpma işlemlerini uygulayan ana sınıftır.  
`setAddSuffix`, `SaveOptions` sınıfının bir yöntemi olup çıktı dosya adına otomatik ek ekleme özelliğini etkinleştirir.  

`Redactor` örneğinizi yükleyin, istediğiniz kırpmaları uygulayın ve ardından `setAddSuffix(true)` etkinleştirilmiş `SaveOptions` ile `save()` metodunu çağırın. Bu tek yapılandırma, dosya adına “_redacted” (veya varsayılan ek) ekleyerek manuel yeniden adlandırmayı ortadan kaldırır ve insan hatasını azaltır. İşlem, belge boyutuna göre O(n) sürede tamamlanır ve tüm desteklenen formatlarda çalışır.

## groupdocs maven bağımlılığı Genel Bakış
**groupdocs maven dependency**, tek bir `<dependency>` satırıyla tüm Redaction SDK'sını projenize getirir. Geçişli bağımlılıkları yönetir, kütüphaneleri güncel tutar ve derleme otomasyonunu basitleştirir. `pom.xml` içinde bağımlılığı bildirerek manuel JAR yönetiminden kaçınır ve en son güvenlik yamalarıyla uyumluluğu sağlarsınız.

## Neden Ek Ekleme Önemlidir
Ek eklemek, bir belgenin işlendiğine dair anlık görsel onay sağlar; bu, denetim izleri, otomatik iş akışları ve sektörler arası düzenleyici uyumluluk için kritiktir.

- **Denetlenebilirlik:** Ekipler hangi dosyaların dağıtılmaya uygun olduğunu hemen görebilir.  
- **Otomasyon:** Betikler ek ile dosyaları filtreleyebilir, orijinal belgelerin yanlışlıkla işlenmesini önler.  
- **Uyumluluk:** Birçok düzenleme, temizlenmiş belgelerin net bir şekilde etiketlenmesini zorunlu kılar.  

## Pratik Uygulamalar
Bu gerçek‑dünya senaryolarını keşfedin:

1. **Hukuki Belge Kırpması:** Müşteri paylaşımından önce sözleşmeleri güvence altına alın.  
2. **Tıbbi Kayıt İşleme:** Klinik verileri korurken hasta kimlik bilgilerini gizleyin.  
3. **Finansal Raporlama:** Dış denetimler sırasında hassas rakamları gizli tutun.  
4. **CRM Entegrasyonu:** Üçüncü taraf araçlara dışa aktarım öncesi müşteri verilerini otomatik olarak kırpın.  
5. **İşbirliği Araçları:** Paylaşılan taslakların gizli yorum veya meta verileri asla ortaya çıkmasın.

## Performans Düşünceleri
### Performansı Optimize Etme
- Akış (`load document from stream`) kullanarak tüm dosyayı belleğe yüklemekten kaçının.  
- `Redactor` örneklerini hızlıca kapatarak kaynakları serbest bırakın.  

### Kaynak Kullanım Kılavuzları
- Toplu çalıştırmalarda CPU ve bellek kullanımını izleyin.  
- Küçük dosya boyutlarıyla çalışırken bellek içi kaydetmeler için `ByteArrayOutputStream` tercih edin.  

### Java Bellek Yönetimi için En İyi Uygulamalar
- Aynı tipte birden fazla dosya işliyorsanız `Redactor` nesnelerini yeniden kullanın.  
- Sızıntıları önlemek için `try‑with‑resources` bloğunda `close()` çağrısını yapın.  

## Yaygın Sorunlar ve Çözümler
| Sorun | Neden | Çözüm |
|-------|-------|-----|
| **Ek görünmüyor** | `setAddSuffix(false)` veya eksik çağrı | `save()` öncesinde `options.setAddSuffix(true)` ayarlandığından emin olun. |
| **Büyük DOCX'te OutOfMemoryError** | Dosyanın bütününün belleğe yüklenmesi | `InputStream` yüklemeye geçin (bkz. Özellik 1). |
| **Açıklamalar hâlâ görünür** | Kaydetmeden önce kırpma uygulanmamış | `save()` öncesinde `redactor.apply(new DeleteAnnotationRedaction())` çağırın. |
| **PDF rasterizasyonu uygulanmadı** | `setRasterizeToPDF(false)` veya atlanmış | Düzleştirilmiş PDF gerektiğinde `options.setRasterizeToPDF(true)` ayarlayın. |

## Sık Sorulan Sorular

**S: PDF belgelerini GroupDocs.Redaction ile kırpabilir miyim?**  
C: Evet, kütüphane PDF, DOCX, PPTX, XLSX ve birçok diğer formatı destekler.

**S: GroupDocs.Redaction ile büyük dosyaları nasıl yönetirim?**  
C: Akış (`load document from stream`) kullanın ve kaynakları hızlıca kapatarak bellek kullanımını düşük tutun.

**S: Ek metnini özelleştirmek mümkün mü?**  
C: API varsayılan olarak “_redacted” gibi bir ek ekler. Özel ekler için, kaydetme sonrası çıktı dosyasını yeniden adlandırmanız gerekir.

**S: GroupDocs.Redaction için geçici lisans nasıl alınır?**  
C: [Geçici Lisans sayfasını](https://purchase.groupdocs.com/temporary-license/) ziyaret edin ve yönergeleri izleyin.

**S: Sorun yaşarsam nereden destek alabilirim?**  
C: Uzman yardımı için [GroupDocs Destek Forumuna](https://forum.groupdocs.com/c/redaction/33) katılabilirsiniz.

## Kaynaklar
- **Documentation:** Ayrıntılı kılavuzları [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/) adresinde keşfedin.  
- **API Reference:** Kapsamlı API detayları için [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java) sayfasına bakın.  
- **Download:** En yeni sürümü [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/) üzerinden alın.  
- **GitHub Repository:** Kaynak kodını incelemek veya katkıda bulunmak için [GroupDocs GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java) adresini ziyaret edin.

**Last Updated:** 2026-05-22  
**Tested With:** GroupDocs.Redaction 24.9 for Java  
**Author:** GroupDocs  

{< /blocks/products/pf/tutorial-page-section >}
{< /blocks/products/pf/main-container >}
{< /blocks/products/pf/main-wrap-class >}
{< blocks/products/products-backtop-button >}

## İlgili Öğreticiler

- [Convert Word to PDF and Save Redacted Documents with GroupDocs.Redaction Java](/redaction/java/document-saving/)
- [Preview Document Pages Java Loading with GroupDocs.Redaction](/redaction/java/document-loading/)
- [Advanced Redaction Techniques for GroupDocs.Redaction Java](/redaction/java/advanced-redaction/)