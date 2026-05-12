---
date: '2026-02-16'
description: GroupDocs.Redaction for Java kullanarak sayfayı önizleme ve belge küçük
  resmi oluşturmayı öğrenin. Adım adım kurulum, kod ve sorun giderme.
keywords:
- GroupDocs.Redaction Java tutorial
- preview document page Java
- PNG preview generation Java
title: GroupDocs.Redaction Java ile Sayfayı Önizleme – Kapsamlı Bir Rehber
type: docs
url: /tr/java/document-loading/load-preview-document-pages-groupdocs-redaction-java/
weight: 1
---

}} etc. Keep them.

Make sure we didn't translate any URLs.

Now produce final answer.# GroupDocs.Redaction Java ile Sayfa Önizleme Nasıl Yapılır

Bugünün hızlı tempolu iş ortamında, bir belgede **how to preview page** nasıl yapılır hızlı bir şekilde fark yaratabilir, sorunsuz bir iş akışı ile bir darboğaz arasında. İster bir belge yönetim sistemi için hızlı bir küçük resim (thumbnail) ihtiyacınız olsun, ister bir web portalında tek bir sayfayı göstermek isteyin, GroupDocs.Redaction for Java, yüksek kaliteli PNG önizlemeler oluşturmak için güvenilir, güvenli bir yol sunar. Bu öğretici, bir belgeyi yükleme, önizleme seçeneklerini yapılandırma ve ihtiyacınız olan yere gömebileceğiniz bir **document thumbnail java** oluşturma sürecini adım adım gösterir.

## Hızlı Yanıtlar
- **“preview page” ne anlama geliyor?** Belirli bir belge sayfasının tam dosyayı açmadan bir görüntüsünü (ör. PNG) oluşturmak.  
- **Hangi format önerilir?** PNG kayıpsızdır ve belge küçük resimleri için idealdir.  
- **Lisans gerekli mi?** Değerlendirme için ücretsiz deneme çalışır; üretim için kalıcı bir lisans gereklidir.  
- **Birden fazla sayfayı önizleyebilir miyim?** Evet—sayfa indeksleri dizisiyle `setPageNumbers` kullanın.  
- **Ana bağımlılıklar nelerdir?** Java 8+, GroupDocs.Redaction kütüphanesi ve Maven (isteğe bağlı).  

## Giriş

Bugünün dijital dünyasında, belge işleme işlemlerini verimli bir şekilde yönetmek, her ölçekten işletme için hayati öneme sahiptir. Hassas bilgileri gizlemek ya da sadece belirli sayfaları önizlemek olsun, doğru araçlara sahip olmak zaman kazandırır ve güvenliği sağlar. Bu öğretici, GroupDocs.Redaction for Java'nın güçlü yeteneklerini tanıtarak, bir belgeyi yükleme ve belirli bir sayfanın PNG önizlemesini oluşturma konularına odaklanır.

**Öğrenecekleriniz**
- GroupDocs.Redaction for Java'ı kurma ve yapılandırma  
- `Redactor` kullanarak belgeleri verimli bir şekilde yükleme  
- `PreviewOptions` ile belirli sayfaların PNG önizlemelerini oluşturma (**how to preview page**'in temeli)  
- Uygulama sırasında yaygın sorunları giderme  

Bu özelliği uygulamaya koymadan önce önkoşullara göz atalım.

## Önkoşullar

Başlamadan önce, ortamınızın GroupDocs.Redaction for Java ile çalışacak şekilde düzgün bir şekilde ayarlandığından emin olun. Bu, gerekli kütüphanelerin kurulmasını ve Java programlamaya temel bir anlayışa sahip olmayı içerir.

### Gerekli Kütüphaneler ve Bağımlılıklar
- **GroupDocs.Redaction**: Java için sağlam bir belge işleme kütüphanesidir.  
- **Java Development Kit (JDK)**: JDK 8 veya daha yeni bir sürümünün yüklü olduğundan emin olun.

### Ortam Kurulum Gereksinimleri
- IntelliJ IDEA, Eclipse gibi bir IDE veya Java projelerini yönetebilen herhangi bir metin düzenleyici.  
- Bağımlılık yönetimini Maven üzerinden yapmak isterseniz Maven kurulumu.

### Bilgi Önkoşulları
- Java programlaması ve dosya I/O işlemlerine temel bir anlayış.  
- Maven ile proje bağımlılıklarını yönetmeye aşina olmak (isteğe bağlı).

## GroupDocs.Redaction for Java Kurulumu

GroupDocs.Redaction ile başlamak basittir. Bu güçlü kütüphaneyi projenize Maven kullanarak ya da doğrudan en son sürümü indirerek ekleyebilirsiniz.

### Maven Yapılandırması
pom.xml dosyanıza aşağıdakileri ekleyin:

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
Alternatif olarak, en son sürümü [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) adresinden indirebilirsiniz.

### Lisans Edinme Adımları
1. **Ücretsiz Deneme**: GroupDocs.Redaction özelliklerini keşfetmek için ücretsiz deneme ile başlayın.  
2. **Geçici Lisans**: Deneme süresinin ötesinde daha fazla zaman veya işlevsellik gerekiyorsa geçici bir lisans edinin.  
3. **Satın Alma**: Uzun vadeli kullanım ve destek için bir lisans satın almayı düşünün.

#### Temel Başlatma ve Kurulum
GroupDocs.Redaction'ı kullanmaya başlamak için, `Redactor` sınıfını belgenizin yolunu belirterek başlatın:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

## Uygulama Kılavuzu

Ortamınızı kurduğunuza göre, bir belgeyi yükleme ve belirli bir sayfayı önizleme özelliğini uygulamaya nasıl geçeceğinizi adım adım inceleyelim.

### Belge Sayfasını Yükleme ve Önizleme

#### Genel Bakış
Bu bölüm, GroupDocs.Redaction for Java kullanarak bir belgedeki belirli bir sayfanın PNG önizlemesini nasıl oluşturacağınızı gösterir. Bu, **how to preview page**'in özüdür ve UI önizlemeleri veya arşiv indeksleri için **document thumbnail java** oluşturmakta özellikle kullanışlıdır.

##### Adım 1: Hedef Sayfa Numarasını Ayarlama
Önizleme yapmak istediğiniz sayfayı belirleyerek başlayın:

```java
int testPageNumber = 1;
```

Bu, `testPageNumber` değerini 1 olarak ayarlar; yani ilk sayfanın önizlemesi oluşturulacak.

##### Adım 2: Çıktı Dosya Yolunu Tanımlama
Oluşturulan PNG dosyasının nereye kaydedileceğini belirtin. Dinamik dosya adları için yer tutucular kullanın:

```java
final String previewFileName = "YOUR_OUTPUT_DIRECTORY_page%d.png";
```

##### Adım 3: Önizleme Seçeneklerini Yapılandırma
`PreviewOptions`'ı, önizlemenin nasıl oluşturulup kaydedileceğini tanımlamak için ayarlayın. Özel akış oluşturmak için `ICreatePageStream` arayüzünü uygulayın:

```java
PreviewOptions options = new PreviewOptions(new ICreatePageStream() {
    @Override
    public java.io.OutputStream createPageStream(int pageNumber) {
        try {
            return new java.io.FileOutputStream(java.lang.String.format(previewFileName, pageNumber));
        } catch (Exception e) {
            // Handle exceptions related to file stream creation
            e.printStackTrace();
            return null;
        }
    }
});
options.setPreviewFormat(PreviewFormats.PNG);
options.setPageNumbers(new int[] { testPageNumber });
```

- **ICreatePageStream**: Her sayfa için özel bir çıktı akışı oluşturmanıza olanak tanır.  
- **setPreviewFormat**: Önizlemenin formatını belirler; PNG, bir **document thumbnail java** için idealdir.  
- **setPageNumbers**: Hangi sayfaların önizleme olarak oluşturulacağını tanımlar (burada sadece seçtiğiniz sayfa).

#### Sorun Giderme İpuçları
- Çıktı dizininin mevcut olduğunu ve uygulamanın yazma iznine sahip olduğunu doğrulayın.  
- Yol ile ilgili sorunları teşhis etmek için `IOException` yakalayıp kaydedin.  
- Önizleme boş ise, kaynak belgenin şifre korumalı veya bozuk olmadığından emin olun.

## Pratik Uygulamalar

**document thumbnail java** oluşturmanın faydalı olabileceği bazı gerçek dünya senaryoları:

1. **Belge İncelemesi** – Büyük sözleşmeleri bir DMS içinde hızlıca incelemek için küçük resimler oluşturun.  
2. **Web Uygulamaları** – Kullanıcıları tüm dosyayı indirmeye zorlamadan bir portalda tek sayfa önizlemesi gösterin.  
3. **Arşiv Sistemleri** – Arşivlenmiş dosyalar için görsel referanslar oluşturun, böylece doğru belgeyi daha sonra bulmak kolaylaşsın.

## Performans Düşünceleri
Büyük dosyalar işlenirken uygulamanızın yanıt vermeye devam etmesi için:

- Belgeleri parçalar halinde işleyin veya akış olarak okuyun, böylece tüm dosya belleğe yüklenmez.  
- Beklenen belge boyutuna göre JVM yığın boyutunu (`-Xmx`) ayarlayın.  
- Aynı belgeden birden fazla sayfa önizlenirken `Redactor` örneğini yeniden kullanın.  

Java bellek yönetimi en iyi uygulamalarını izlemek, optimal performansı korumaya yardımcı olur.

## Yaygın Sorunlar ve Çözümler
| Sorun | Neden | Çözüm |
|-------|-------|----------|
| **FileNotFoundException** PNG kaydedilirken | Çıktı dizini mevcut değil veya yol yanlış | Önizleme yapmadan önce dizini programatik olarak oluşturun (`new File(path).mkdirs()`). |
| **OutOfMemoryError** büyük PDF'lerde | Tüm belge belleğe yüklendi | `Redactor`'ı akış seçenekleriyle kullanın veya JVM yığınını artırın. |
| **Boş önizleme görüntüsü** | Desteklenmeyen sayfa içeriği (ör. şifreli) | Önizleme yapmadan önce belgenin şifresinin kaldırıldığından emin olun veya şifreyi `Redactor` aracılığıyla sağlayın. |

## Sonuç
Bu öğreticide, GroupDocs.Redaction for Java kullanarak **how to preview page** ve **document thumbnail java** oluşturmayı ele aldık. Sağlanan adımlarla, artık sayfa önizleme işlevini kendi uygulamalarınıza entegre edebilir, kullanıcı deneyimini iyileştirebilir ve belge iş akışlarını hızlandırabilirsiniz.

**Sonraki Adımlar**
- Farklı belge formatları (PDF, DOCX, PPTX) ile deneyler yapın.  
- Önizleme oluşturmayı gizleme (redaction) ile birleştirerek “öncesi‑sonrası” görüntülerini gösterin.  
- Tüm belge koleksiyonları için küçük resimler oluşturmak üzere toplu işleme keşfedin.  

Belge işleme hatlarınızı geliştirmeye hazır mısınız? Bugün uygulamaya başlayın ve GroupDocs.Redaction for Java'nın gücünü deneyimleyin!

## SSS Bölümü

**S1: GroupDocs.Redaction for Java ne için kullanılır?**  
C1: Java uygulamaları içinde çeşitli formatlarda belgeleri gizlemek, açıklama eklemek ve önizlemek için güçlü bir kütüphanedir.

**S2: Sayfa akışları oluştururken istisnaları nasıl yönetirim?**  
C2: Dosya işlemleri etrafında her zaman istisna yönetimi ekleyin; böylece dosya erişim hataları veya geçersiz yollar gibi sorunları yönetebilirsiniz.

**S3: Aynı anda birden fazla sayfayı önizleyebilir miyim?**  
C3: Evet, bir tam sayı dizisiyle `setPageNumbers` kullanarak birden fazla sayfa belirtebilirsiniz.

**S4: PNG önizlemeleri oluşturmanın faydaları nelerdir?**  
C4: PNG formatı kayıpsız sıkıştırma ve yüksek kalite sunar, bu da belge küçük resimleri için idealdir.

**S5: GroupDocs.Redaction ücretsiz mi?**  
C5: Ücretsiz deneme ile başlayabilir, geçici bir lisans edinebilir veya ihtiyacınıza göre tam bir lisans satın alabilirsiniz.

## Kaynaklar
- **Dokümantasyon**: [GroupDocs Redaction Documentation](https://docs.groupdocs.com/redaction/java/)  
- **API Referansı**: [API Reference](https://reference.groupdocs.com/redaction/java)  
- **İndirme**: [Latest Releases](https://releases.groupdocs.com/redaction/java/)  
- **GitHub Deposu**: [GroupDocs GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **Ücretsiz Destek**: [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)  
- **Geçici Lisans**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Son Güncelleme:** 2026-02-16  
**Test Edilen Sürüm:** GroupDocs.Redaction 24.9 for Java  
**Yazar:** GroupDocs