---
date: 2026-08-04
description: Java ile elektronik tablo verilerini nasıl filtreleyeceğinizi ve Excel
  elektronik tablolarında sütunları veya hücreleri güvenli bir şekilde redact etmeyi
  GroupDocs.Redaction for Java kullanarak öğrenin.
keywords:
- filter spreadsheet data java
- hide sensitive data excel
- GroupDocs.Redaction Java
- spreadsheet redaction
lastmod: 2026-08-04
og_description: Java ile elektronik tablo verilerini nasıl filtreleyeceğinizi ve Excel
  elektronik tablolarında sütunları veya hücreleri güvenli bir şekilde redact etmeyi
  GroupDocs.Redaction for Java kullanarak öğrenin.
og_image_alt: Guide showing how to filter spreadsheet data in Java using GroupDocs.Redaction
og_title: Java ile elektronik tablo verilerini filtreleme – GroupDocs.Redaction rehberi
schemas:
- author: GroupDocs
  dateModified: '2026-08-04'
  description: Learn how to filter spreadsheet data java and securely redact columns
    or cells in Excel spreadsheets using GroupDocs.Redaction for Java.
  headline: Filter spreadsheet data java – guide with GroupDocs.Redaction
  type: TechArticle
- description: Learn how to filter spreadsheet data java and securely redact columns
    or cells in Excel spreadsheets using GroupDocs.Redaction for Java.
  name: Filter spreadsheet data java – guide with GroupDocs.Redaction
  steps:
  - name: instantiate the filter
    text: '`RedactionFilter` is the core class that represents a filtering rule for
      spreadsheet redaction. It accepts column numbers, row numbers, or custom lambda
      expressions to pinpoint data.'
  - name: configure the condition
    text: Use `filter.setColumnIndex(1)` to target column B (zero‑based) and `filter.setRegex("[A‑Z0‑9._%+-]+@[A‑Z0‑9.-]+\\.[A-Z]{2,}")`
      to match email patterns. You can also combine multiple conditions with `filter.and(...)`
      or `filter.or(...)`.
  - name: apply the redaction
    text: '`Redactor` is the main class that executes redaction operations on a workbook.
      Pass the workbook and the configured filter to the `Redactor` object. The API
      streams the workbook, applies the filter, and writes the redacted result to
      a new file, preserving original formatting and formulas.'
  type: HowTo
- questions:
  - answer: Yes, you can add additional column indexes to the same `RedactionFilter`
      instance or chain multiple filters with `filter.or(...)`.
    question: Can I filter multiple columns at once?
  - answer: Provide the password when opening the workbook; the filter operates after
      decryption just like on an unprotected file.
    question: Does the filter work on password‑protected workbooks?
  - answer: The engine is optimized for up to 1 million rows (≈500 MB) without loading
      the entire file into memory.
    question: How many rows can the API handle in a single operation?
  - answer: Yes, call `filter.preview(workbook)` to get a list of cell addresses that
      match the criteria.
    question: Is it possible to preview which cells will be redacted before saving?
  - answer: A full commercial license is required for production deployments; a temporary
      license is sufficient for testing and evaluation.
    question: What licensing model is required for production use?
  type: FAQPage
tags:
- filter spreadsheet data
- GroupDocs.Redaction
- Java spreadsheet redaction
- hide sensitive data excel
- data privacy
title: Java ile elektronik tablo verilerini filtreleme – GroupDocs.Redaction rehberi
type: docs
url: /tr/java/spreadsheet-redaction/
weight: 12
---

# Elektronik tablo verilerini java ile filtreleme – GroupDocs.Redaction Java öğreticisi

## Hızlı cevaplar
- **Java'da elektronik tablo redaksiyonunu hangi kütüphane yönetir?** GroupDocs.Redaction for Java.  
- **Tüm dosyayı belleğe yüklemeden satırları filtreleyebilir miyim?** Evet – API verileri akış olarak işler ve filtreleri anında uygulamanıza izin verir.  
- **Hangi dosya formatları destekleniyor?** 30'dan fazla elektronik tablo formatı, XLS, XLSX, CSV ve ODS dahil.  
- **Geliştirme için lisansa ihtiyacım var mı?** Test için geçici bir lisans yeterli; üretim için tam lisans gereklidir.  
- **Çalışma kitabı boyutu için bir limit var mı?** Motor, aşırı bellek tüketimi olmadan 500 MB'a kadar dosyaları işleyebilir.

## Filter spreadsheet data java nedir?
**Filter spreadsheet data java**, Java kodu kullanarak bir Excel‑stil çalışma kitabında belirli satırları, sütunları veya hücreleri programlı olarak seçme sürecidir; böylece yalnızca hedeflenen içerik incelenir veya redakte edilir. Bu teknik çalışma süresini azaltır, gereksiz değişiklikleri sınırlar ve GDPR‑benzeri uyumluluğa ulaşmaya yardımcı olur.

## Neden filter spreadsheet data java?
GroupDocs.Redaction Java, **30+ elektronik tablo formatını** destekler ve **500 MB'a kadar** (yaklaşık 1 milyon satır) içeren çalışma kitaplarını, bellek kullanımını **200 MB** altında tutarak işleyebilir. Önce filtreleme yaparak ilgisiz verilere dokunmazsınız, bu da tipik gizlilik temizleme senaryolarında ortalama **%40‑60** işlem süresi tasarrufu sağlar.

## Önkoşullar
- Java 17 veya daha yeni bir sürüm yüklü.  
- Maven veya Gradle yapı sistemi.  
- GroupDocs.Redaction for Java (resmi siteden indirilebilir).  
- Geçici veya tam lisans anahtarı.  

## GroupDocs.Redaction Java kullanarak elektronik tablolarda verileri nasıl filtreleriz?
Çalışma kitabını yükleyin, redakte etmek istediğiniz hücrelerle eşleşen bir filtre tanımlayın ve ardından redaksiyon işlemini uygulayın. API, filtreyi akış (streaming) biçiminde gerçekleştirir, böylece tüm dosyayı RAM'de tutmanız gerekmez.

`RedactionFilter` sınıfı, sütun indekslerini, satır aralıklarını veya özel koşulları belirtmenizi sağlar. Örneğin, **B** sütunundaki e‑posta adresi desenine sahip her hücreyi hedefleyebilir veya “Status” sütunu “Confidential” olan satırlara redaksiyonu sınırlayabilirsiniz.

**Doğrudan yanıt (40‑70 kelime):**  
Bir `RedactionFilter` örneği oluşturun, sütun indeksini ve bir düzenli ifade koşulunu ayarlayın, ardından filtreyi `Redactor.redact(workbook, filter)` metoduna geçirin. Bu tek satırlık filtre, kriterlerinize uyan tam hücreleri izole eder ve redaktör, bunları kaldırır veya maskeleyerek sayfanın geri kalanını dokunulmaz bırakır. İşlem, filtrelenen satırlara göre doğrusal sürede tamamlanır.

### Adım 1: filtreyi örnekleyin
`RedactionFilter`, elektronik tablo redaksiyonu için bir filtreleme kuralını temsil eden temel sınıftır. Veri noktalarını belirlemek için sütun numaralarını, satır numaralarını veya özel lambda ifadelerini kabul eder.

### Adım 2: koşulu yapılandırın
`filter.setColumnIndex(1)` kullanarak B sütununu (sıfır‑tabanlı) hedefleyin ve `filter.setRegex("[A‑Z0‑9._%+-]+@[A‑Z0‑9.-]+\\.[A-Z]{2,}")` ile e‑posta desenlerini eşleştirin. Ayrıca birden fazla koşulu `filter.and(...)` veya `filter.or(...)` ile birleştirebilirsiniz.

### Adım 3: redaksiyonu uygulayın
`Redactor`, bir çalışma kitabı üzerinde redaksiyon işlemlerini yürüten ana sınıftır.  
Çalışma kitabını ve yapılandırılmış filtreyi `Redactor` nesnesine geçirin. API, çalışma kitabını akış olarak işler, filtreyi uygular ve redakte edilmiş sonucu yeni bir dosyaya yazar, özgün biçimlendirme ve formülleri korur.

## Yaygın sorunlar ve çözümler
- **Filtre hiçbir hücreyle eşleşmiyor:** Sütun indeksini (sıfır‑tabanlı) doğrulayın ve düzenli ifade sözdiziminin Java için doğru olduğundan emin olun.  
- **Büyük dosyalarda bellek dışı hatalar:** JVM yığın boyutunu makul bir şekilde artırın (ör. `-Xmx1g`) veya filtrelemeden önce çalışma kitabını daha küçük parçalara bölün.  
- **Redakte edilmiş çıktı biçimlendirmeyi kaybediyor:** `RedactionOptions`, hücre biçimlendirmesini koruma gibi redaksiyon davranışını özelleştirmenizi sağlar. Hücre stillerini korumak için `RedactionOptions.setPreserveFormatting(true)` kullanın.

## Neden elektronik tablo verilerini filtrelemek?
Redaksiyondan önce filtreleme, bir çalışma kitabının yalnızca hassas bölümlerini izole eder; bu da temiz verilere gereksiz değişiklik yapmaktan kaçınmanızı sağlar. Bu seçici yaklaşım, kazara veri kaybı riskini azaltır ve denetim günlüğünde çok daha az giriş bulunduğu için uyumluluk denetimlerini hızlandırır.

## GroupDocs.Redaction Java API kullanarak Excel elektronik tablolarında e‑postaları nasıl redakte ederiz
Excel dosyanızı yükleyin, tipik e‑posta desenini arayan bir filtre uygulayın ve redaktörü çağırın. API, eşleşen her e‑postayı “***@***.com” gibi bir yer tutucu ile değiştirirken çevredeki hücre düzenini korur.

## Veri nasıl filtrelenir – mevcut öğreticiler
- [Excel elektronik tablolarında e‑postaları redakte etme – GroupDocs.Redaction Java API](./redact-emails-excel-groupdocs-redaction-java/)

## Ek kaynaklar
- [GroupDocs.Redaction for Java Belgeleri](https://docs.groupdocs.com/redaction/java/)
- [GroupDocs.Redaction for Java API Referansı](https://reference.groupdocs.com/redaction/java/)
- [GroupDocs.Redaction for Java'ı İndir](https://releases.groupdocs.com/redaction/java/)
- [GroupDocs.Redaction Forum](https://forum.groupdocs.com/c/redaction/33)
- [Ücretsiz Destek](https://forum.groupdocs.com/)
- [Geçici Lisans](https://purchase.groupdocs.com/temporary-license/)

**Son Güncelleme:** 2026-08-04  
**Test Edilen Versiyon:** GroupDocs.Redaction 23.11 for Java  
**Yazar:** GroupDocs  

## Sıkça Sorulan Sorular

**S: Aynı anda birden fazla sütunu filtreleyebilir miyim?**  
C: Evet, aynı `RedactionFilter` örneğine ek sütun indeksleri ekleyebilir veya `filter.or(...)` ile birden fazla filtreyi zincirleyebilirsiniz.

**S: Filtre, şifre korumalı çalışma kitaplarında çalışır mı?**  
C: Çalışma kitabını açarken şifreyi sağlayın; filtre, şifre çözme sonrasında, korumasız bir dosyada olduğu gibi çalışır.

**S: API tek bir işlemde kaç satırı işleyebilir?**  
C: Motor, tüm dosyayı belleğe yüklemeden, 1 milyon satıra (≈500 MB) kadar optimize edilmiştir.

**S: Kaydetmeden önce hangi hücrelerin redakte edileceğini önizlemek mümkün mü?**  
C: Evet, `filter.preview(workbook)` çağırarak kriterlere uyan hücre adreslerinin bir listesini alabilirsiniz.

**S: Üretim kullanımında hangi lisans modeli gereklidir?**  
C: Üretim dağıtımları için tam ticari lisans gerekir; test ve değerlendirme için geçici lisans yeterlidir.

## İlgili Öğreticiler
- [Excel elektronik tablolarında Hassas Verileri Redakte Etme – GroupDocs.Redaction Java API](/redaction/java/spreadsheet-redaction/redact-emails-excel-groupdocs-redaction-java/)
- [Hassas Verileri Maskele Java – GroupDocs.Redaction Kılavuzu](/redaction/java/getting-started/)
- [Hassas Verileri Maskele Java – GroupDocs.Redaction ile Kişisel Bilgileri Redakte Et](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)