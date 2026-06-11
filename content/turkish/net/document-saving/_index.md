---
date: 2026-06-11
description: GroupDocs.Redaction for .NET kullanarak kırpılmış dosyaları dışa aktarmayı,
  çıktı klasörlerini yapılandırmayı, rasterleştirilmiş PDF'ler oluşturmayı ve akışlara
  kaydetmeyi öğrenin.
keywords:
- how to export redacted
- configure output folder
- create rasterized pdf
- save rasterized pdf
- convert redacted to pdf
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to export redacted files, configure output folders, create
    rasterized PDFs, and save to streams using GroupDocs.Redaction for .NET.
  headline: How to Export Redacted Documents with GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to export redacted files, configure output folders, create
    rasterized PDFs, and save to streams using GroupDocs.Redaction for .NET.
  name: How to Export Redacted Documents with GroupDocs.Redaction .NET
  steps:
  - name: Install the NuGet Package
    text: 'Add the latest GroupDocs.Redaction package to your project:'
  - name: Load the Document and Define Redactions
    text: Create a `Redactor` instance, load the file, and specify the regions you
      want to hide. The `Redactor` class provides the core functionality for loading
      documents and applying redaction rules.
  - name: Choose the Export Method
    text: '#### Export in Original Format'
  type: HowTo
- questions:
  - answer: Yes, GroupDocs.Redaction can convert most input types to PDF, DOCX, XLSX,
      PPTX, or rasterized PDF, covering over 30 formats.
    question: Can I export to a format that wasn’t originally supported?
  - answer: By rendering each page as a flat image, any hidden text layers are removed,
      making it impossible to extract the original content.
    question: How does rasterization protect redacted data?
  - answer: Absolutely – you can call `Apply` repeatedly or pass a collection of `RedactionOptions`
      to process many patterns in one pass. `RedactionOptions` defines the settings
      for a single redaction operation, such as region and replacement type.
    question: Is it possible to chain multiple redaction rules?
  - answer: The `Redactor` implements `IDisposable`; wrap it in a `using` block or
      call `Dispose()` to release file handles promptly. `IDisposable` is an interface
      that provides a mechanism for releasing unmanaged resources.
    question: Do I need to close the Redactor object?
  - answer: GroupDocs.Redaction is validated on .NET Framework 4.6+, .NET Core 3.1+,
      and .NET 5/6/7.
    question: What .NET runtimes are officially tested?
  type: FAQPage
title: GroupDocs.Redaction .NET ile Kırpılmış Belgeleri Nasıl Dışa Aktarılır
type: docs
url: /tr/net/document-saving/
weight: 3
---

# Redacted Belgeleri GroupDocs.Redaction .NET ile Nasıl Dışa Aktarılır

Bu kapsamlı rehberde, GroupDocs.Redaction for .NET kullanarak **kırpılmış** içeriği güvenli ve verimli bir şekilde nasıl dışa aktaracağınızı keşfedeceksiniz. Orijinal dosya türünü korumanız, belgeyi rasterleştirilmiş bir PDF olarak kilitlemeniz veya sonucu doğrudan bellekte akıtmanız gerekse, her seçeneği net, sohbet tarzı açıklamalar ve gerçek dünya ipuçlarıyla adım adım gösteriyoruz. Bu öğreticinin sonunda, uyumluluk odaklı herhangi bir senaryo için doğru dışa aktarma stratejisini seçebileceksiniz.

## Hızlı Yanıtlar
- **Hangi formatlara dışa aktarabilirim?** GroupDocs.Redaction tarafından desteklenen 30+ yerel formatın yanı sıra maksimum güvenlik için rasterleştirilmiş PDF.  
- **Akış için lisansa ihtiyacım var mı?** Evet, üretim akışı için geçerli bir GroupDocs.Redaction lisansı gereklidir.  
- **Özel bir çıktı klasörü ayarlayabilir miyim?** Kesinlikle – bunu yapılandırmak için `OutputPath` özelliğini veya `SaveOptions`'ı kullanın.  
- **Büyük dosyalar için rasterleştirme güvenli mi?** Dosyanın tamamını belleğe yüklemeden 500 sayfaya kadar belgeleri işleyebilir.  
- **Hangi .NET sürümleri destekleniyor?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.

## GroupDocs.Redaction Nedir?
GroupDocs.Redaction, PDF, Word, Excel, PowerPoint, görüntüler ve birçok diğer formatta hassas bilgileri programlı olarak kaldıran veya maskeleyen bir .NET kütüphanesidir. Kırpma bölgelerini tanımlamak, politikaları uygulamak ve sonunda temizlenmiş belgeyi dışa aktarmak için yüksek seviyeli bir API sunar. Bu, kırpma yeteneklerini herhangi bir .NET uygulamasına kolayca entegre etmeyi sağlar.

## Neden Kırpılmış Belgeler Rasterleştirilmiş PDF Olarak Dışa Aktarılır?
Rasterleştirilmiş PDF'ler her sayfayı düz bir görüntüye dönüştürerek daha sonra çıkarılabilecek gizli metin katmanlarını ortadan kaldırır. Bu format, kırpılmış içeriğin geri alınamayacağını garanti eder ve GDPR ve HIPAA gibi katı düzenleyici standartları karşılar. GroupDocs.Redaction, görsel bütünlüğü korurken güvenliği sağlayan 300 dpi'ye kadar rasterleştirilmiş PDF'ler üretebilir.

## Kırpılmış Belgeler Nasıl Dışa Aktarılır?
Kaynak dosyayı yükleyin, kırpma kurallarınızı uygulayın ve ardından uygun kaydetme yöntemini çağırın—orijinal format için `Save`, yalnızca görüntü PDF'leri için `SaveAsRasterizedPdf` veya bellek içi işleme için `SaveToStream`. Aşağıda adım adım iş akışı verilmiştir. Her yöntem, kırpılmış içeriğin kalıcı olarak kaldırılmasını sağlarken istenen çıktı formatını korur.

### Adım 1: NuGet Paketini Yükleyin
Projenize en son GroupDocs.Redaction paketini ekleyin:

```bash
dotnet add package GroupDocs.Redaction
```

### Adım 2: Belgeyi Yükleyin ve Kırpmaları Tanımlayın
`Redactor` örneği oluşturun, dosyayı yükleyin ve gizlemek istediğiniz bölgeleri belirtin. `Redactor` sınıfı, belgeleri yükleme ve kırpma kurallarını uygulama temel işlevselliğini sağlar.

```csharp
using GroupDocs.Redaction;
using GroupDocs.Redaction.Options;

// Load the document
var redactor = Redactor.Create("SensitiveReport.docx");

// Define a redaction for a specific text pattern
redactor.Apply(new RedactionOptions
{
    SearchPattern = "SSN: \\d{3}-\\d{2}-\\d{4}",
    RedactionColor = System.Drawing.Color.Black,
    RedactionType = RedactionType.Image
});
```

### Adım 3: Dışa Aktarma Yöntemini Seçin
#### Orijinal Formatta Dışa Aktar
```csharp
redactor.Save("RedactedReport.docx");
```

#### Rasterleştirilmiş PDF Olarak Dışa Aktar
```csharp
var rasterOptions = new RasterizationOptions { Dpi = 300 };
redactor.SaveAsRasterizedPdf("RedactedReport.pdf", rasterOptions);
```

#### Bellek Akışına Dışa Aktar (web API'leri için ideal)
```csharp
using var stream = new MemoryStream();
redactor.Save(stream, SaveOptions.CreatePdf());
stream.Position = 0; // Reset for reading
```

`Save` yöntemi kırpılmış belgeyi orijinal formatında bir dosyaya yazar. `SaveAsRasterizedPdf` her sayfanın bir görüntü olarak render edildiği bir PDF oluşturur ve gizli metinleri kaldırır. `SaveToStream` kırpılmış dosyayı bir bellek akışı olarak döndürür ve web yanıtları için uygundur.

## Çıktı Klasörü Nasıl Yapılandırılır?
`Redactor` üzerindeki `OutputPath` özelliğini ayarlayın veya istediğiniz dizini içeren özel bir `SaveOptions` nesnesi geçirin. `OutputPath`, `Redactor`'un çıktı dosyalarının yazıldığı dizini belirten bir özelliktir. `SaveOptions`, çıktı klasörü dahil olmak üzere çeşitli kaydetme parametrelerini özelleştirmenizi sağlar. Bu, tüm dışa aktarılan dosyaların öngörülebilir bir konuma yerleştirilmesini sağlayarak toplu işleme boru hatlarını basitleştirir. Çalışma alanınızı düzenli tutmak için belge türüne göre alt klasörler de belirtebilirsiniz.

```csharp
var options = SaveOptions.CreatePdf();
options.OutputPath = @"C:\RedactedOutputs\";
redactor.Save(options);
```

## Yaygın Sorunlar ve Çözümler
- **Kırpma uygulanmadı:** Arama deseninin belge metniyle tam olarak eşleştiğini doğrulayın; gerekirse `RegexOptions.IgnoreCase` kullanın. `RegexOptions`, büyük/küçük harf duyarlılığı gibi düzenli ifade eşleştirme davranışını kontrol eden bir enumerasyondur.  
- **Büyük dosyalar bellek baskısına neden oluyor:** `SaveToStream` kullanarak akış modunu etkinleştirin ve tüm belge üzerinde `Save` çağrısından kaçının.  
- **Rasterleştirilmiş PDF bulanık görünüyor:** Görüntü kalitesini artırmak için `RasterizationOptions` içinde DPI'yi (ör. 300–600) yükseltin. `RasterizationOptions`, rasterleştirilmiş PDF çıktısı için DPI ve görüntü formatı gibi parametreleri ayarlamanızı sağlar.

## Sıkça Sorulan Sorular

**S: Orijinal olarak desteklenmeyen bir formata dışa aktarabilir miyim?**  
C: Evet, GroupDocs.Redaction çoğu giriş türünü PDF, DOCX, XLSX, PPTX veya rasterleştirilmiş PDF'ye dönüştürebilir ve 30'dan fazla formatı kapsar.

**S: Rasterleştirme kırpılmış verileri nasıl korur?**  
C: Her sayfayı düz bir görüntü olarak render ederek gizli metin katmanları kaldırılır, böylece orijinal içeriğin çıkarılması imkânsız hale gelir.

**S: Birden fazla kırpma kuralını zincirleme yapmak mümkün mü?**  
C: Kesinlikle – `Apply` metodunu tekrar tekrar çağırabilir veya birden çok deseni tek seferde işlemek için `RedactionOptions` koleksiyonunu geçirebilirsiniz. `RedactionOptions`, bölge ve değiştirme türü gibi tek bir kırpma işlemi için ayarları tanımlar.

**S: Redactor nesnesini kapatmam gerekiyor mu?**  
C: `Redactor`, `IDisposable` arayüzünü uygular; bir `using` bloğu içinde sarın veya dosya tutucularını hızlıca serbest bırakmak için `Dispose()` çağırın. `IDisposable`, yönetilmeyen kaynakları serbest bırakma mekanizması sağlayan bir arayüzdür.

**S: Hangi .NET çalışma zamanları resmi olarak test edilmiştir?**  
C: GroupDocs.Redaction, .NET Framework 4.6+, .NET Core 3.1+ ve .NET 5/6/7 üzerinde doğrulanmıştır.

## Ek Kaynaklar

### Mevcut Eğitimler

- [GroupDocs.Redaction for .NET Kullanarak Belgeleri Rasterleştirilmiş PDF Olarak Kaydetme: Tam Kılavuz](./groupdocs-redaction-net-rasterized-pdfs/)
- [.NET'te Çıktı Dizinini Uygulama: GroupDocs.Redaction ile Kapsamlı Kılavuz](./implement-output-directory-groupdocs-redaction-dotnet/)
- [GroupDocs.Redaction for .NET ile Belgeleri Kırpma ve Kaydetme: Tam Kılavuz](./redact-save-documents-groupdocs-redaction-net/)
- [GroupDocs.Redaction .NET Kullanarak Kırpılmış Belgeleri Orijinal Formatta Kaydetme](./save-redacted-docs-original-format-groupdocs-redaction-net/)
- [.NET'te Akış Kullanarak Güvenli Belge Kırpma: GroupDocs.Redaction İçin Kılavuz](./secure-document-redaction-net-streams-groupdocs-redaction/)

### Faydalı Bağlantılar

- [GroupDocs.Redaction for .NET Dokümantasyonu](https://docs.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction for .NET API Referansı](https://reference.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction for .NET İndirme](https://releases.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction Forum](https://forum.groupdocs.com/c/redaction/33)
- [Ücretsiz Destek](https://forum.groupdocs.com/)
- [Geçici Lisans](https://purchase.groupdocs.com/temporary-license/)

---

**Son Güncelleme:** 2026-06-11  
**Test Edilen Versiyon:** GroupDocs.Redaction 23.11 for .NET  
**Yazar:** GroupDocs  

## İlgili Eğitimler

- [GroupDocs.Redaction .NET Kullanarak Kırpılmış Belgeleri Orijinal Formatta Kaydetme](/redaction/net/document-saving/save-redacted-docs-original-format-groupdocs-redaction-net/)
- [GroupDocs.Redaction for .NET Kullanarak Belgeleri Rasterleştirilmiş PDF Olarak Kaydetme: Tam Kılavuz](/redaction/net/document-saving/groupdocs-redaction-net-rasterized-pdfs/)
- [.NET'te Akış Kullanarak Güvenli Belge Kırpma: GroupDocs.Redaction İçin Kılavuz](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)