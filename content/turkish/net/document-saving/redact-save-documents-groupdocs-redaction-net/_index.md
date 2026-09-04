---
date: '2026-07-20'
description: GroupDocs.Redaction for .NET kullanarak belgeleri nasıl kırpacağınızı,
  hassas bilgileri nasıl gizleyeceğinizi ve kırpılmış dosyaları memory stream'e nasıl
  kaydedeceğinizi öğrenin.
keywords:
- how to redact documents
- redact sensitive information
- redact specific text
- save to memory stream
- save redacted document
lastmod: '2026-07-20'
og_description: GroupDocs.Redaction for .NET ile belgeleri nasıl kırpacağınızı öğrenin.
  Hassas bilgileri gizlemek ve kırpılmış dosyayı memory stream'e kaydetmek için bu
  adım adım kılavuzu izleyin.
og_image_alt: 'Developer guide: Redact and save documents using GroupDocs.Redaction
  for .NET'
og_title: GroupDocs.Redaction for .NET ile Belgeleri Kırpma
schemas:
- author: GroupDocs
  dateModified: '2026-07-20'
  description: Learn how to redact documents, hide sensitive information, and save
    redacted files to a memory stream using GroupDocs.Redaction for .NET.
  headline: How to Redact Documents with GroupDocs.Redaction for .NET – A Complete
    Guide
  type: TechArticle
- description: Learn how to redact documents, hide sensitive information, and save
    redacted files to a memory stream using GroupDocs.Redaction for .NET.
  name: How to Redact Documents with GroupDocs.Redaction for .NET – A Complete Guide
  steps:
  - name: '**Load** – Create a `Redactor` instance pointing to your file.'
    text: '**Load** – Create a `Redactor` instance pointing to your file.'
  - name: '**Apply** – Call `Apply` with an `ExactPhraseRedaction` (or other redaction
      type).'
    text: '**Apply** – Call `Apply` with an `ExactPhraseRedaction` (or other redaction
      type).'
  - name: '**Inspect** – Review `RedactorChangeLog` to confirm how many matches were
      found and replaced.'
    text: '**Inspect** – Review `RedactorChangeLog` to confirm how many matches were
      found and replaced.'
  type: HowTo
- questions:
  - answer: Yes—GroupDocs.Redaction treats PDF, DOCX, PPTX, and many image formats
      uniformly; simply point `Redactor` at a PDF file.
    question: Can I redact PDF files using the same API?
  - answer: Absolutely—once redacted, the content is permanently removed, regardless
      of subsequent conversions.
    question: Does the redaction survive after converting the document to another
      format?
  - answer: Use `RedactionOptions` to set the overlay color, opacity, or replace text
      with a custom string.
    question: How do I customize the redaction appearance?
  - answer: Yes—`RegexRedaction` lets you define patterns such as credit‑card numbers
      or email addresses.
    question: Is it possible to redact using regular expressions?
  - answer: .NET Framework 4.6+, .NET Core 3.1+, .NET 5, .NET 6, and .NET 7.
    question: What .NET versions are officially supported?
  type: FAQPage
tags:
- redact documents
- GroupDocs.Redaction
- .NET document processing
- C# redaction tutorial
title: GroupDocs.Redaction for .NET ile Belgeleri Kırpma – Tam Bir Kılavuz
type: docs
url: /tr/net/document-saving/redact-save-documents-groupdocs-redaction-net/
weight: 1
---

# GroupDocs.Redaction for .NET ile Belgeleri Kırpma

Modern kurumsal ortamlarda, **belge kırpma** kişisel verileri, ticari sırları ve uyumlulukla ilgili bilgileri korumak için kritik bir beceridir. Bu kılavuz, Word, PDF veya görüntü dosyalarındaki hassas bilgileri kırpma ve ardından kırpılmış çıktıyı doğrudan bir bellek akışına (memory stream) kaydetme sürecini adım adım gösterir—hepsi GroupDocs.Redaction for .NET ile.

## Hızlı Yanıtlar
- **Redaction ne yapar?** Seçilen içeriği kalıcı olarak bir yer tutucu ile değiştirir veya kaldırır, böylece verinin asla geri alınamamasını sağlar.  
- **Hangi formatlar destekleniyor?** 30'dan fazla dosya türü, PDF, DOCX, PPTX ve yaygın görüntü formatları dahil.  
- **Disk'e yazmadan kırpma yapabilir miyim?** Evet—sonucu `MemoryStream`'e kaydederek bellek içi işleme yapabilirsiniz.  
- **Üretim için lisansa ihtiyacım var mı?** Üretim kullanımında tam lisans gereklidir; değerlendirme için ücretsiz deneme mevcuttur.  
- **.NET Core ile uyumlu mu?** Kesinlikle—GroupDocs.Redaction, .NET Framework 4.6+, .NET Core 3.1+ ve .NET 5/6/7 ile çalışır.

## Belge Kırpma Nedir?
Belge kırpma, gizli metin, görüntü ve meta verileri kalıcı olarak kaldırır veya gizler, böylece gizli içeriğin daha sonra geri alınamaması, görüntülenememesi veya çıkarılamaması sağlanır. Hassas öğeler, siyah bir dikdörtgen veya özel metin gibi bir yer tutucu ile değiştirilir ve belge yapısı güncellenerek kırpılmış verinin geri alınamaz olması sağlanır.

## Belgeleri Kırpmak İçin GroupDocs.Redaction Neden Kullanılmalı?
GroupDocs.Redaction, **30+ dosya formatını** destekler ve tüm belgeyi belleğe yüklemeden **2 GB**'a kadar dosyaları işleyebilir, birçok rakibe göre **%30 daha hızlı işleme süresi** sunar. API'si, tek bir metod çağrısıyla tam ifadeli, düzenli ifade ya da görüntü tabanlı kırpmalar uygulamanıza olanak tanır; bu da .NET geliştiricileri için en verimli seçenektir.

## Önkoşullar
- **GroupDocs.Redaction** NuGet paketi (en son sürüm).  
- .NET Framework 4.6+ **veya** .NET Core 3.1+ yüklü.  
- Visual Studio 2022 gibi C# uyumlu bir IDE.  
- Temel C# bilgisi ve dosya I/O'ya aşinalık.

### Gerekli Kütüphaneler ve Sürümler
- **GroupDocs.Redaction** – en yeni kırpma algoritmalarına ve güvenlik yamalarına erişmek için her zaman en yeni sürümü kullanın.  
- **System.IO** – akış (stream) yönetimi için (yerleşik .NET).

### Lisans Edinme Adımları
- **Ücretsiz Deneme:** GroupDocs web sitesinde 30 günlük deneme için kaydolun.  
- **Geçici Lisans:** geliştirme testleri için geçici bir anahtar isteyin.  
- **Tam Lisans:** sınırsız kullanım için üretim lisansı satın alın.

## Temel Başlatma ve Kurulum
`Redactor` sınıfı, GroupDocs.Redaction'da tüm kırpma işlemlerinin giriş noktasıdır. NuGet paketini kurduktan sonra, `Redactor`'ı kaynak belgenin yolu ile örnekleyebilirsiniz.

```csharp
using GroupDocs.Redaction;
using System.IO;

// Initialize Redactor with the source file path
Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

## Bir Belgede Belirli Metni Nasıl Kırparız?
Belirli bir metni kırpmak için, kaynak dosyayı bir `Redactor` örneğiyle yükleyin, ardından gizlemek istediğiniz tam dizeyi hedefleyen bir `ExactPhraseRedaction` uygulayın. API belgeyi tarar, her eşleşmeyi seçilen kaplamayla değiştirir ve değişiklikleri bir değişiklik günlüğüne kaydeder; böylece kaydetmeden önce kırpmayı doğrulayabilirsiniz.

```csharp
RedactorChangeLog result = redactor.Apply(new ExactPhraseRedaction("John Doe"));
```

`ExactPhraseRedaction` sınıfı, tam ifadenin her oluşumunu siyah bir dikdörtgen (veya yapılandırdığınız herhangi bir özel yer tutucu) ile değiştirir.  

**Adım‑Adım:**
1. **Yükle** – Dosyanıza işaret eden bir `Redactor` örneği oluşturun.  
2. **Uygula** – `ExactPhraseRedaction` (veya başka bir kırpma türü) ile `Apply` metodunu çağırın.  
3. **İncele** – `RedactorChangeLog`'u gözden geçirerek kaç eşleşmenin bulunduğunu ve değiştirildiğini doğrulayın.  

## Kırpılmış Bir Belgeyi Bellek Akışına (Memory Stream) Nasıl Kaydederiz?
`MemoryStream`, verileri bellekte saklayan bir .NET akışıdır ve disk I/O olmadan hızlı okuma/yazma sağlar. `Save` metodunu kullanarak kırpılmış çıktıyı bir `MemoryStream`'e yönlendirebilir, ardından bu akışı ağ üzerinden gönderebilir, bir veritabanına kaydedebilir veya geçici dosya oluşturmadan doğrudan bir API uç noktasından döndürebilirsiniz.

```csharp
using (MemoryStream stream = new MemoryStream())
{
    // Save the redacted document directly into the stream
    redactor.Save(stream);
    // Optionally reset the stream position for downstream consumers
    stream.Position = 0;
    // The stream now contains the redacted file ready for use
}
```

**Önemli Noktalar:**
- `Save` metodu, kırpılmış çıktıyı `MemoryStream` dahil herhangi bir `Stream` uygulamasına yazar.  
- Geçici dosyalar oluşturulmaz, bu da güvenlik ve performansı artırır.  
- Bunu ASP.NET Core'un `FileStreamResult`'ı ile birleştirerek dosyayı doğrudan tarayıcıya döndürebilirsiniz.

## Yaygın Tuzaklar ve Çözümler
| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Kırpma uygulanmadı** | İfade büyük/küçük harf durumu kaynaktakiyle farklıdır. | Esnek eşleşme için `ExactPhraseRedaction("John Doe", caseSensitive: false)` kullanın veya düzenli ifade kırpması uygulayın. |
| **Büyük dosyalar OutOfMemory hatasına neden olur** | Tüm dosyayı belleğe yüklemeye çalışmak. | GroupDocs.Redaction verileri dahili olarak akıtır; dosyaları parçalar halinde işleyen en son sürümü kullandığınızdan emin olun. |
| **Kaydedilen dosya bozuk** | Göndermeden önce akış sıfırlanmadı. | `redactor.Save(stream)` işleminden sonra, okumadan veya döndürmeden önce `stream.Position = 0` ayarlayın. |

## Sıkça Sorulan Sorular

**S: Aynı API'yi kullanarak PDF dosyalarını kırpabilir miyim?**  
**C:** Evet—GroupDocs.Redaction PDF, DOCX, PPTX ve birçok görüntü formatını aynı şekilde işler; sadece `Redactor`'ı bir PDF dosyasına yönlendirin.

**S: Belge başka bir formata dönüştürüldükten sonra kırpma korunur mu?**  
**C:** Kesinlikle—kırpıldıktan sonra içerik kalıcı olarak kaldırılır, sonraki dönüşümlere bakılmaksızın.

**S: Kırpma görünümünü nasıl özelleştirebilirim?**  
**C:** `RedactionOptions` kullanarak kaplama rengini, opaklığını ayarlayabilir veya metni özel bir dizeyle değiştirebilirsiniz.

**S: Düzenli ifadeler kullanarak kırpma yapmak mümkün mü?**  
**C:** Evet—`RegexRedaction` kredi kartı numaraları veya e-posta adresleri gibi desenleri tanımlamanıza olanak tanır.

**S: Resmi olarak hangi .NET sürümleri destekleniyor?**  
**C:** .NET Framework 4.6+, .NET Core 3.1+, .NET 5, .NET 6 ve .NET 7.

---

**Son Güncelleme:** 2026-07-20  
**Test Edilen Versiyon:** GroupDocs.Redaction 23.12 for .NET  
**Yazar:** GroupDocs  

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
using (Redactor redactor = new Redactor(sourceFile))
{
    // Continue to apply redactions...
}
```

## İlgili Eğitimler

- [GroupDocs.Redaction .NET ile Belgeleri Yükleme ve Kırpma: Tam Kılavuz](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [GroupDocs.Redaction .NET ile Kırpılmış Belgeleri Orijinal Formatta Kaydet](/redaction/net/document-saving/save-redacted-docs-original-format-groupdocs-redaction-net/)
- [.NET'te Akışlar Kullanarak Güvenli Belge Kırpma: GroupDocs.Redaction İçin Kılavuz](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)