---
date: '2025-12-17'
description: GroupDocs.Redaction for Java kullanarak dosya adına son ek eklemeyi ve
  belgelere ait hassas bilgileri kırpmayı öğrenin. Belge güvenliğini ve gizliliğini
  etkili bir şekilde artırın.
keywords:
- document redaction Java
- GroupDocs.Redaction tutorial
- secure document handling
title: Java'da GroupDocs.Redaction ile Belgeleri Kırparken Dosya Adına Sonek Nasıl
  Eklenir
type: docs
url: /tr/java/advanced-redaction/master-document-redaction-groupdocs-redaction-java/
weight: 1
---

# Java ile GroupDocs.Redaction Kullanarak Belgeleri Kırparken Dosya Adına Sonek Ekleme

Gizli verileri kırpmak sadece mücadelenin yarısıdır—kaydedilen dosyanın işlendiğini açıkça gösterdiğinden de emin olmanız gerekir. Bu rehberde kırpılmış bir belgeyi kaydederken **dosya adına sonek ekleme** yöntemini, ayrıca GroupDocs.Redaction for Java kullanarak yükleme, açıklama ekleme ve kaydetme işlemlerini öğreneceksiniz. Hukuki sözleşmeler, tıbbi kayıtlar veya finansal raporlar gibi verileri koruyor olsanız da, bu adımlar iş akışınızı hem güvenli hem de denetlenebilir tutar.

## Hızlı Yanıtlar
- **“add suffix to filename” ne yapar?**  
  Çıktı dosya adına (örneğin “_redacted”) gibi özel bir sonek ekler, böylece işlenmiş dosyaları anında tanımlayabilirsiniz.  
- **Bir belgeyi akıştan (stream) yükleyebilir miyim?**  
  Evet—GroupDocs.Redaction, herhangi bir `InputStream`'den yüklemeyi destekler; bulut depolama veya bellek içi işleme için mükemmeldir.  
- **Bu özellik için lisansa ihtiyacım var mı?**  
  Temel kırpma için ücretsiz deneme çalışır; geçici veya tam lisans, sonek işleme dahil tüm gelişmiş seçeneklerin kilidini açar.  
- **Hangi formatlar destekleniyor?**  
  Kütüphane DOCX, PDF, PPTX, XLSX ve daha birçok formatı işler.  
- **PDF çıktısı için rasterizasyon gerekli mi?**  
  Rasterizasyon isteğe bağlıdır; belgeyi ekstra güvenlik için düzleştirmeniz gerektiğinde etkinleştirin.  

## Dosya Adına Sonek Eklemek Nedir?
Sonek eklemek, bir dosyanın kırpma işleminden geçtiğini gösteren basit bir adlandırma kuralıdır. Orijinal, kırpılmamış sürümlerin yanlışlıkla paylaşılmasını önler ve otomatik boru hatlarının işleme durumunu izlemesine yardımcı olur.

## Bu Görev İçin Neden GroupDocs.Redaction Kullanmalı?
GroupDocs.Redaction, kırpma işlemlerini dosya‑işleme seçenekleriyle—**dosya adına sonek ekleme** gibi—birkaç satır kodla birleştirmenizi sağlayan akıcı bir Java API'si sunar. Bu, geliştirme süresini tasarruf ettirir ve manuel hataların riskini azaltır.

## Ön Koşullar

- **Java Development Kit (JDK):** Sürüm 8 veya üzeri.  
- **GroupDocs.Redaction Kütüphanesi:** Kırpma görevleri için temel kütüphane.  
- **IDE:** IntelliJ IDEA, Eclipse veya herhangi bir Java uyumlu editör.  
- **Maven:** Bağımlılık yönetimi için.  

### Bilgi Ön Koşulları
Java I/O ve temel nesne‑yönelimliramlara aşina olmak, örnekleri daha kolay takip etmenizi sağlar.

## GroupDocs.Redaction'ı Java İçin Kurma

### Maven Kurulumu
`pom.xml` dosyanıza aşağıdaki yapılandırmayı ekleyerek Maven üzerinden GroupDocs kütüphanelerine erişebilirsiniz:

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
1. **Ücretsiz Deneme:** Temel işlevselliğe sınırsız erişim.  
2. **Geçici Lisans:** Gelişmiş özellikleri keşfetmek için geçici lisans alın.  
3. **Satın Alma:** Uzun vadeli kullanım için tam lisans satın almayı düşünün.

#### Temel Başlatma ve Kurulum
Gerekli importları ekleyerek projenizi başlatın:

```java
import com.groupdocs.redaction.Redactor;
```

Bu kurulumla, belge kırpma işlevlerini uygulamaya hazır olacaksınız.

## Uygulama Kılavuzu

### Özellik 1: Belgeyi Akıştan Yükleme
**Genel Bakış:** Belgeleri işleme için bir `InputStream` içine nasıl yükleyeceğinizi öğrenin.

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

- **Neden:** `InputStream` kullanmak, belgeleri çeşitli formatlarda sorunsuz bir şekilde yönetmenizi sağlar; bu, bulut veya mikro‑servis senaryolarında **belgeyi akıştan yüklemeniz** gerektiğinde kritiktir.

### Özellik 2: Açıklama Silme Kırpması Uygulama
**Genel Bakış:** `DeleteAnnotationRedaction` kullanarak belgenizdeki açıklamaları kaldırın.

#### Adım Adım Uygulama
##### Adım 2.1: DeleteAnnotationRedaction Uygulama

```java
import com.groupdocs.redaction.redactions.DeleteAnnotationRedaction;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply the DeleteAnnotationRedaction to remove annotations from the document
    redactor.apply(new DeleteAnnotationRedaction());
}
```

- **Neden:** Bu adım, hassas açıklamaların kaldırılmasını sağlar ve belge gizliliğini artırır.

### Özellik 3: Seçeneklerle Belgeyi Kaydetme
**Genel Bakış:** İşlenmiş belgenizi rasterizasyon ve **dosya adına sonek ekleme** gibi belirli seçeneklerle nasıl kaydedeceğinizi öğrenin.

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

## Sonek Eklemenin Önemi
- **Denetlenebilirlik:** Ekipler, hangi dosyaların dağıtılmaya güvenli olduğunu anında görebilir.  
- **Otomasyon:** Betikler, sonek ile dosyaları filtreleyebilir ve orijinal belgelerin yanlışlıkla işlenmesini önler.  
- **Uyumluluk:** Birçok düzenleme, temizlenmiş belgelerin açıkça etiketlenmesini gerektirir.

## Pratik Uygulamalar
Bu gerçek dünya kullanım örneklerini inceleyin:

1. **Hukuki Belge Kırpması:** Müşteri paylaşımından önce sözleşmeleri güvence altına alın.  
2. **Tıbbi Kayıt İşleme:** Hasta kimlik bilgilerini koruyun.  
3. **Finansal Raporlama:** Hassas rakamları gizli tutun.  
4. **CRM Entegrasyonu:** Müşteri verilerini dışa aktarmadan önce otomatik olarak kırpın.  
5. **İşbirliği Araçları:** Paylaşılan taslakların gizli yorumları ortaya çıkarmadığından emin olun.

## Performans Düşünceleri

### Performansı Optimize Etme
- Akış (`load document from stream`) kullanarak tüm dosyaları belleğe yüklemekten kaçının.  
- `Redactor` örneklerini hızlıca kapatarak kaynakları serbest bırakın.

### Kaynak Kullanım Rehberi
- Toplu çalıştırmalar sırasında CPU ve bellek kullanımını izleyin.  
- Orta boyutlu dosyalarla çalışırken bellek içi kaydetmeler için `ByteArrayOutputStream` tercih edin.

### Java Bellek Yönetimi İçin En İyi Uygulamalar
- Aynı tipte birden fazla dosya işlenirken `Redactor` nesnelerini yeniden kullanın.  
- Sızıntıları önlemek için `close()` metodunu bir `finally` bloğunda veya try‑with‑resources içinde çağırın.

## Yaygın Sorunlar ve Çözümler

| Sorun | Neden | Çözüm |
|-------|-------|-----|
| **Sonek görünmüyor** | `setAddSuffix(false)` veya eksik çağrı | `save()`'den önce `options.setAddSuffix(true)` ayarlandığından emin olun. |
| **Büyük DOCX'te OutOfMemoryError** | Tüm dosyanın belleğe yüklenmesi | `InputStream` yüklemeye geçin (Bkz. Özellik 1). |
| **Açıklamalar hâlâ görünür** | Kaydetmeden önce kırpma uygulanmamış | `save()`'den önce `redactor.apply(new DeleteAnnotationRedaction())` çağırın. |
| **PDF rasterizasyonu uygulanmadı** | `setRasterizeToPDF(false)` veya atlanmış | Düzleştirilmiş PDF gerektiğinde `options.setRasterizeToPDF(true)` ayarlayın. |

## Sıkça Sorulan Sorular

**S: PDF belgelerini GroupDocs.Redaction ile kırpabilir miyim?**  
C: Evet, kütüphane PDF, DOCX, PPTX, XLSX ve birçok diğer formatı destekler.

**S: GroupDocs.Redaction ile büyük dosyaları yönetmenin en iyi yolu nedir?**  
C: Akış (`load document from stream`) kullanın ve bellek kullanımını düşük tutmak için kaynakları hızlıca kapatın.

**S: Sonek metnini özelleştirmek mümkün mü?**  
C: API otomatik olarak varsayılan bir sonek ekler (örneğin “_redacted”). Özel sonekler için, kaydetme sonrası çıktı dosyasını yeniden adlandırabilirsiniz.

**S: GroupDocs.Redaction için geçici bir lisans nasıl alınır?**  
C: [Geçici Lisans sayfasını](https://purchase.groupdocs.com/temporary-license/) ziyaret edin ve talimatları izleyin.

**S: Sorunlarla karşılaştığımda nereden yardım alabilirim?**  
C: Uzman desteği için [GroupDocs Destek Forumuna](https://forum.groupdocs.com/c/redaction/33) katılın.

## Kaynaklar
- **Dokümantasyon:** Ayrıntılı kılavuzları [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/) adresinde inceleyin.  
- **API Referansı:** Kapsamlı API detaylarına [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java) üzerinden ulaşın.  
- **İndirme:** En son sürümü [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/) adresinden alın.  
- **GitHub Deposu:** Kaynak koduna katkıda bulunmak veya incelemek için [GroupDocs GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java) adresini ziyaret edin.

---

**Son Güncelleme:** 2025-12-17  
**Test Edilen Sürüm:** GroupDocs.Redaction 24.9 for Java  
**Yazar:** GroupDocs  

---