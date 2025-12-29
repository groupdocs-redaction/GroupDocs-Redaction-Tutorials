---
date: '2025-12-29'
description: GroupDocs.Redaction for Java kullanarak taranmış belge görüntülerini
  nasıl kırpacağınızı öğrenin. Kurulum, görüntü alanı kırpma ve doğrulama konularını
  kapsayan adım adım rehber.
keywords:
- Java image redaction
- GroupDocs.Redaction for Java
- image area redaction
title: GroupDocs ile Java'da Tarama Belgesi Görüntülerini Nasıl Kırpılır?
type: docs
url: /tr/java/image-redaction/java-image-redaction-groupdocs-tutorial/
weight: 1
---

# Tarama Belgesi Görüntülerini GroupDocs ile Java'da Nasıl Kırpılır

Günümüz dijital ortamında, **tarama belgesini kırpmak** görüntüleri, gizliliği korumak ve uyumluluk gereksinimlerini karşılamak için gereklidir. İster bir tarama sözleşmesindeki kişisel verileri gizlemeniz, ister tıbbi bir görüntüdeki hasta detaylarını örtmeniz gerekse, bu öğretici **görüntüyü nasıl kırpılır** içeriğini **GroupDocs.Redaction for Java** kullanarak hızlı ve güvenilir bir şekilde nasıl yapacağınızı gösterir.

## Hızlı Yanıtlar
- **Java'da görüntü kırpma işlemini hangi kütüphane yönetir?** GroupDocs.Redaction for Java  
- **Kırpma rengini seçebilir miyim?** Yes – any `java.awt.Color` (e.g., `Color.BLUE`)  
- **Üretim için lisans gerekli mi?** Yes, a valid GroupDocs license is needed  
- **Orijinal görüntü üzerine yazılacak mı?** No – you save the result to a new file  
- **Hangi Java sürümü destekleniyor?** Java 8+ (compatible with modern JDKs)

## Görüntü kırpma nedir ve neden tarama belgesi görüntüleri kırpılır?
Görüntü kırpma, isimler, numaralar veya imzalar gibi hassas görsel bilgileri kalıcı olarak gizlemek anlamına gelir; böylece bu bilgiler geri alınamaz. Tarama belgeleriyle çalıştığınızda, veri pikseller olarak gömülüdür ve bu da geleneksel metin kırpma araçlarını etkisiz kılar. GroupDocs.Redaction kullanarak tam piksel bölgelerini hedefleyebilir ve bunları katı bir renk ile değiştirebilirsiniz; bu, bilginin gerçekten kaldırılmasını sağlar.

## Önkoşullar
- **JDK 8 veya daha yeni** yüklü  
- **Maven** (veya başka bir yapı aracı) bağımlılık yönetimi için  
- **IntelliJ IDEA**, **Eclipse** veya **NetBeans** gibi bir IDE  
- Temel Java bilgisi ve dosya I/O'ya aşinalık  

## GroupDocs.Redaction for Java Kurulumu

### Maven Kurulumu
Add the GroupDocs repository and dependency to your `pom.xml`:

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
Alternatif olarak, resmi sürüm sayfasından en son JAR'ı indirin: [GroupDocs.Redaction for Java sürümleri](https://releases.groupdocs.com/redaction/java/).

### Lisans Edinme
- **Ücretsiz Deneme:** API'yi keşfetmek için bir deneme kaydı oluşturun.  
- **Geçici Lisans:** Uzun süreli test için geçici bir anahtar kullanın.  
- **Tam Satın Alma:** Sınırsız kullanım için bir üretim lisansı edinin.  

## Uygulama Kılavuzu

Uygulamayı iki temel özelliğe ayıracağız: **Image Area Redaction** (gerçek maskeleme) ve **Redaction Status Check** (başarının doğrulanması).

### Tarama belgesi görüntülerini kırpma – Adım 1: Redactor'ı Başlatma
İlk olarak, işlemek istediğiniz görüntüyü işaret eden bir `Redactor` örneği oluşturun.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_JPG");
```

### Adım 2: Kırpma Parametrelerini Tanımlama
Gizlemek istediğiniz dikdörtgenin sol‑üst köşesini (`Point`) ve boyutunu (`Dimension`) belirtin. Bu örnekte mavi bir dolgu kullanıyoruz.

```java
// Define the position on the image where redaction starts.
Point samplePoint = new Point(385, 485);

// Define the size of the area to be redacted.
Dimension sampleSize = new Dimension(1793, 2069);
```

### Adım 3: Kırpmayı Uygulama
`RegionReplacementOptions` ile bir `ImageAreaRedaction` nesnesi oluşturun ve çalıştırın. Metot, işlemin başarılı olup olmadığını belirten bir `RedactorChangeLog` döndürür.

```java
RedactorChangeLog result = redactor.apply(
    new ImageAreaRedaction(samplePoint, new RegionReplacementOptions(Color.BLUE, sampleSize))
);

// Check if the redaction was successful and save the output.
if (result.getStatus() != RedactionStatus.Failed) {
    redactor.save("YOUR_OUTPUT_DIRECTORY/redacted_output.jpg");
}
```

### Adım 4: Kaynakları Serbest Bırakma
İşiniz bittiğinde her zaman `Redactor`'ı kapatarak yerel kaynakları serbest bırakın.

```java
redactor.close();
```

### Kırpmayı Doğrulama – Durum Kontrolü
Kırpmayı uyguladıktan sonra, işlemin başarısız olmadığını doğrulamak için `RedactorChangeLog`'u inceleyebilirsiniz.

```java
if (result != null && result.getStatus() != RedactionStatus.Failed) {
    System.out.println("Redaction was successful.");
} else {
    System.out.println("Redaction failed.");
}
```

## Pratik Uygulamalar
- **Gizli Belge İşleme:** Tarama sözleşmelerindeki kişisel verileri, dış taraflarla paylaşmadan önce otomatik olarak maskeleyin.  
- **Hukuki Belgeler:** Kanıt görüntülerindeki tanımlayıcıları kırparak GDPR veya HIPAA uyumluluğunu sağlayın.  
- **Tıbbi Kayıtlar:** Radyoloji görüntülerindeki yüzleri veya el yazısı notları gizleyerek hasta gizliliğini koruyun.

## Performans Düşünceleri
- **Toplu İşleme:** Bellek kullanımını düşük tutmak için görüntüleri küçük partiler halinde yükleyip kırpın.  
- **Verimli Veri Yapıları:** Birçok görüntü işlenirken `Point` ve `Dimension` nesnelerini yeniden kullanın.  
- **Güncel Kalın:** Performans iyileştirmeleri ve hata düzeltmeleri için düzenli olarak en son GroupDocs.Redaction sürümüne yükseltin.

## Yaygın Sorunlar ve Çözümler

| Sorun | Neden | Çözüm |
|-------|-------|-----|
| **`Failed` durumu ile kırpma başarısız olur** | Yanlış dosya yolu veya desteklenmeyen görüntü formatı | Görüntünün mevcut olduğunu ve desteklenen bir formatta (JPG, PNG, BMP) olduğunu doğrulayın. |
| **Çıktı dosyası boş** | `redactor.save()` kırpma tamamlanmadan çağrıldı | `apply()`'ın başarılı bir durum döndürdüğünden emin olun, ardından kaydedin. |
| **Renk uygulanmadı** | Şeffaf bir renk kullanmak | Opak bir `Color` seçin (ör. `Color.BLACK` veya `Color.BLUE`). |

## Sıkça Sorulan Sorular

**Q: `ImageAreaRedaction` ile metin kırpması arasındaki fark nedir?**  
A: `ImageAreaRedaction` piksel koordinatları üzerinde çalışırken, metin kırpması OCR katmanlarını ayrıştırarak metin içeriğini bulur ve kaldırır.

**Q: Tek bir görüntüde birden fazla bölgeyi kırpabilir miyim?**  
A: Evet—kaydetmeden önce farklı `ImageAreaRedaction` nesneleriyle `redactor.apply()`'ı tekrarlayarak çağırabilirsiniz.

**Q: GroupDocs.Redaction TIFF gibi diğer görüntü formatlarını destekliyor mu?**  
A: Kütüphane yaygın raster formatlarını (JPG, PNG, BMP, GIF) destekler. TIFF için önce desteklenen bir formata dönüştürün.

**Q: Tarama PDF'lerinin bir klasörü için kırpmayı nasıl otomatikleştiririm?**  
A: PDF'den çıkarılan her sayfa görüntüsü üzerinde yineleyin, aynı kırpma mantığını uygulayın ve ardından bir PDF kütüphanesi kullanarak PDF'i yeniden oluşturun.

**Q: Kaydetmeden önce kırpmayı önizleme imkanı var mı?**  
A: `Redactor`'ı bir `BufferedImage`'a render ederek Swing veya JavaFX UI'de değişiklikleri onaylamadan önce görüntüleyebilirsiniz.

## Sonuç
Artık **görüntüyü nasıl kırpılır** içeriği ve özellikle GroupDocs.Redaction for Java kullanarak **tarama belgesi görüntülerini nasıl kırpılır** konusunda eksiksiz, üretim‑hazır bir kılavuza sahipsiniz. Yukarıdaki adımları izleyerek, çeşitli sektörlerde hassas görsel verileri koruyabilirsiniz. Metin kırpma veya PDF sayfa kırpma gibi ek API'ları keşfederek kuruluşunuz için kapsamlı bir veri‑gizliliği çözümü oluşturun.

---

**Son Güncelleme:** 2025-12-29  
**Test Edilen Sürüm:** GroupDocs.Redaction 24.9 (Java)  
**Yazar:** GroupDocs  

**Kaynaklar**  
- [Dokümantasyon](https://docs.groupdocs.com/redaction/java/)  
- [API Referansı](https://reference.groupdocs.com/redaction/java)  
- [İndirme](https://releases.groupdocs.com/redaction/java/)  
- [GitHub Deposu](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- [Ücretsiz Destek Forumu](https://forum.groupdocs.com/c/redaction/33)  
- [Geçici Lisans](https://purchase.groupdocs.com/temporary-license/)