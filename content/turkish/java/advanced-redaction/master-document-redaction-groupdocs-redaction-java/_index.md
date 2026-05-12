---
date: '2026-02-16'
description: Java'da belgeleri kırparken dosya adlarına bir sonek eklemek için GroupDocs
  Maven bağımlılığını nasıl kullanacağınızı öğrenin. Akıştan yükleme, ek açıklama
  silme ve kaydetme seçeneklerini içerir.
keywords:
- document redaction Java
- GroupDocs.Redaction tutorial
- secure document handling
title: groupdocs maven bağımlılığı – Java'da dosya adına son ek ekle
type: docs
url: /tr/java/advanced-redaction/master-document-redaction-groupdocs-redaction-java/
weight: 1
---

# Java'da GroupDocs.Redaction ile Belgeleri Kırparken Dosya Adına Sonek Ekleme

Gizli verileri kırpmak sadece mücadelenin yarısıdır—kaydedilen dosyanın işlendiğini açıkça gösterdiğinden de emin olmanız gerekir. **groupdocs maven bağımlılığını kullanmak bunu basitleştirir**, sadece birkaç satır kodla çıktı dosyasının adına bir sonek eklemenizi sağlar. Bu rehberde, kırpılmış bir belgeyi kaydederken dosya adına sonek eklemeyi, ayrıca GroupDocs.Redaction for Java kullanarak belgeyi yüklemeyi, açıklama eklemeyi ve kaydetmeyi öğreneceksiniz. Hukuki sözleşmeler, tıbbi kayıtlar veya finansal raporlar gibi belgeleri korurken, bu adımlar iş akışınızı hem güvenli hem de denetlenebilir tutar.

## Hızlı Yanıtlar
- **“add suffix to filename” ne yapar?**  
  Çıktı dosya adına (ör. “_redacted”) gibi özel bir sonek ekler, böylece işlenmiş dosyaları anında tanımlayabilirsiniz.  
- **Bir belgeyi akıştan (stream) yükleyebilir miyim?**  
  Evet—GroupDocs.Redaction herhangi bir `InputStream`'den yüklemeyi destekler, bulut depolama veya bellek içi işleme için mükemmeldir.  
- **Bu özellik için lisansa ihtiyacım var mı?**  
  Temel kırpma için ücretsiz deneme çalışır; geçici veya tam lisans, sonek işleme dahil tüm gelişmiş seçeneklerin kilidini açar.  
- **Hangi formatlar destekleniyor?**  
  Kütüphane DOCX, PDF, PPTX, XLSX ve daha birçok formatı işler.  
- **PDF çıktısı için rasterizasyon gerekli mi?**  
  Rasterizasyon isteğe bağlıdır; belgeyi ekstra güvenlik için düzleştirmeniz gerektiğinde etkinleştirin.

## Dosya Adına Sonek Eklemek Nedir?
Sonek eklemek, bir dosyanın kırpma işleminden geçtiğini gösteren basit bir adlandırma kuralıdır. Orijinal, kırpılmamış sürümlerin yanlışlıkla paylaşılmasını önler ve otomatik iş akışlarının işleme durumunu izlemesine yardımcı olur.

## Bu Görev İçin GroupDocs.Redaction Neden Kullanılmalı?
GroupDocs.Redaction, kırpma işlemlerini dosya‑işleme seçenekleriyle—örneğin **dosya adına sonek ekleme**—birkaç satır kodla birleştirmenizi sağlayan akıcı bir Java API'si sunar. Bu, geliştirme süresini tasarruf ettirir ve manuel hataların riskini azaltır.

## Önkoşullar

- **Java Development Kit (JDK):** Versiyon 8 veya üzeri.  
- **GroupDocs.Redaction Library:** Kırpma görevleri için çekirdek kütüphane.  
- **IDE:** IntelliJ IDEA, Eclipse veya herhangi bir Java‑uyumlu editör.  
- **Maven:** Bağımlılık yönetimi için.  

### Bilgi Önkoşulları
Java I/O ve temel nesne‑yönelimli kavramlara aşina olmak, örnekleri daha kolay takip etmenizi sağlar.

## Java için GroupDocs.Redaction Kurulumu
### Maven Kurulumu
GroupDocs kütüphanelerine Maven üzerinden erişmek için `pom.xml` dosyanıza aşağıdaki yapılandırmayı ekleyin:

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
Alternatif olarak, en yeni sürümü doğrudan [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) adresinden indirebilirsiniz.

### Lisans Edinme
1. **Free Trial:** Temel işlevselliğe sınırsız erişim.  
2. **Temporary License:** Gelişmiş özellikleri keşfetmek için geçici bir lisans alın.  
3. **Purchase:** Uzun vadeli kullanım için tam lisans satın almayı düşünün.

#### Temel Başlatma ve Kurulum
Gerekli içe aktarmaları ekleyerek projenizi başlatın:

```java
import com.groupdocs.redaction.Redactor;
```

Bu kurulumla, belge kırpma işlevlerini uygulamaya hazır olacaksınız.

## Uygulama Kılavuzu

### Özellik 1: Belgeyi Akıştan Yükleme
**Genel Bakış:** İşleme için belgeleri bir `InputStream` içine nasıl yükleyeceğinizi öğrenin.

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

- **Neden:** `InputStream` kullanmak, belgeleri çeşitli formatlarda sorunsuz bir şekilde yönetmenizi sağlar; bu, bulut ya da mikro‑servis senaryolarında **belgeyi akıştan yüklemeniz** gerektiğinde önemlidir.

### Özellik 2: Açıklama Silme Kırpması Uygulama
**Genel Bakış:** `DeleteAnnotationRedaction` kullanarak belgenizdeki açıklamaları kaldırın.

#### Adım Adım Uygulama
##### Adım 2.1: DeleteAnnotationRedaction Uygula

```java
import com.groupdocs.redaction.redactions.DeleteAnnotationRedaction;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply the DeleteAnnotationRedaction to remove annotations from the document
    redactor.apply(new DeleteAnnotationRedaction());
}
```

- **Neden:** Bu adım, hassas açıklamaların kaldırılmasını sağlayarak belge gizliliğini artırır.

### Özellik 3: Seçeneklerle Belgeyi Kaydetme
**Genel Bakış:** Rasterizasyon ve **dosya adına sonek ekleme** gibi belirli seçeneklerle işlenmiş belgenizi nasıl kaydedeceğinizi öğrenin.

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

- **Neden:** Kaydetme seçeneklerini özelleştirmek, esnek çıktı formatları ve adlandırma kuralları sağlar. `setAddSuffix(true)` etkinleştirildiğinde **dosya adına sonek eklenir**, böylece dosyanın kırpıldığını açıkça gösterir.

## groupdocs maven dependency Genel Bakış
**groupdocs maven dependency**, tek bir `<dependency>` girişiyle tüm Redaction SDK'sını projenize getirir. Geçişli bağımlılıkları yönetir, kütüphaneleri güncel tutar ve derleme otomasyonunu basitleştirir. `pom.xml` içinde bağımlılığı bildirerek manuel JAR yönetiminden kaçınır ve en yeni güvenlik yamalarıyla uyumluluğu sağlarsınız.

## Sonek Eklemenin Önemi
- **Denetlenebilirlik:** Ekipler hangi dosyaların dağıtılmaya güvenli olduğunu anında görebilir.  
- **Otomasyon:** Betikler, sonek ile dosyaları filtreleyebilir, orijinal belgelerin yanlışlıkla işlenmesini önler.  
- **Uyumluluk:** Birçok düzenleme, temizlenmiş belgelerin net bir şekilde etiketlenmesini gerektirir.  

## Pratik Uygulamalar
Bu gerçek dünya kullanım senaryolarını keşfedin:
1. **Hukuki Belge Kırpma:** Müşteri paylaşımından önce sözleşmeleri güvence altına alın.  
2. **Tıbbi Kayıt Yönetimi:** Hasta kimlik bilgilerini koruyun.  
3. **Finansal Raporlama:** Hassas rakamları gizli tutun.  
4. **CRM Entegrasyonu:** Müşteri verilerini dışa aktarmadan önce otomatik olarak kırpın.  
5. **İşbirliği Araçları:** Paylaşılan taslakların gizli yorumları ortaya çıkarmadığından emin olun.

## Performans Hususları
### Performansı Optimize Etme
- Akış kullanın (`load document from stream`) bütün dosyaları belleğe yüklemekten kaçınmak için.  
- `Redactor` örneklerini hızlıca kapatarak kaynakları serbest bırakın.

### Kaynak Kullanım Kılavuzları
- Toplu çalıştırmalar sırasında CPU ve belleği izleyin.  
- Orta ölçekli dosya boyutlarıyla çalışırken bellek içi kaydetmeler için `ByteArrayOutputStream` tercih edin.

### Java Bellek Yönetimi İçin En İyi Uygulamalar
- Aynı tipte birden fazla dosya işlerken `Redactor` nesnelerini yeniden kullanın.  
- Bellek sızıntılarını önlemek için `try‑with‑resources` bloğunda `close()` çağırın.

## Yaygın Sorunlar ve Çözümler
| Sorun | Neden | Çözüm |
|-------|-------|-----|
| **Sonek görünmüyor** | `setAddSuffix(false)` veya eksik çağrı | `save()`'den önce `options.setAddSuffix(true)` ayarlandığından emin olun. |
| **Büyük DOCX'te OutOfMemoryError** | Tüm dosyanın belleğe yüklenmesi | `InputStream` yüklemeye geçin (Bkz. Özellik 1). |
| **Açıklamalar hâlâ görünür** | Kırpma kaydetmeden önce uygulanmadı | `save()`'den önce `redactor.apply(new DeleteAnnotationRedaction())` çağırın. |
| **PDF rasterizasyonu uygulanmadı** | `setRasterizeToPDF(false)` veya atlanmış | Düzleştirilmiş PDF gerektiğinde `options.setRasterizeToPDF(true)` ayarlayın. |

## Sıkça Sorulan Sorular

**S: GroupDocs.Redaction ile PDF belgelerini kırpabilir miyim?**  
C: Evet, kütüphane PDF, DOCX, PPTX, XLSX ve birçok diğer formatı destekler.

**S: GroupDocs.Redaction ile büyük dosyaları yönetmenin en iyi yolu nedir?**  
C: Bellek kullanımını düşük tutmak için akış (`load document from stream`) kullanın ve kaynakları hızlıca kapatın.

**S: Sonek metnini özelleştirmek mümkün mü?**  
C: API otomatik olarak varsayılan bir sonek (ör. “_redacted”) ekler. Özel sonekler için, kaydettikten sonra çıktı dosyasını yeniden adlandırabilirsiniz.

**S: GroupDocs.Redaction için geçici bir lisans nasıl alınır?**  
C: [Temporary License page](https://purchase.groupdocs.com/temporary-license/) adresini ziyaret edin ve talimatları izleyin.

**S: Sorun yaşarsam nereden yardım alabilirim?**  
C: Uzman desteği için [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) forumuna katılın.

## Kaynaklar
- **Dokümantasyon:** Ayrıntılı kılavuzları [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/) adresinde inceleyin.  
- **API Referansı:** Kapsamlı API detaylarını [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java) adresinde bulun.  
- **İndirme:** En son sürümü [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/) adresinden alın.  
- **GitHub Deposu:** Katkıda bulunmak veya kaynak kodu incelemek için [GroupDocs GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java) adresine gidin.

---

**Last Updated:** 2026-02-16  
**Tested With:** GroupDocs.Redaction 24.9 for Java  
**Author:** GroupDocs