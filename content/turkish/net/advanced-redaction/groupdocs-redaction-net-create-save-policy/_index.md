---
date: '2026-10-06'
description: GroupDocs.Redaction .NET ile hassas verileri nasıl kırpacağınızı öğrenin.
  Bu adım adım kılavuz, bir kırpma politikasını XML olarak nasıl oluşturacağınızı,
  uygulayacağınızı ve kaydedeceğinizi gösterir.
keywords:
- redact sensitive data
- mask confidential information
- groupdocs redaction .net
lastmod: '2026-10-06'
og_description: GroupDocs.Redaction .NET ile hassas verileri nasıl kırpacağınızı öğrenin.
  Bu adım adım kılavuz, bir kırpma politikasını XML olarak nasıl oluşturacağınızı,
  uygulayacağınızı ve kaydedeceğinizi gösterir.
og_image_alt: Tutorial showing how to redact sensitive data in documents with GroupDocs.Redaction
  for .NET
og_title: GroupDocs.Redaction .NET ile hassas verileri nasıl kırpılır
schemas:
- author: GroupDocs
  dateModified: '2026-10-06'
  description: Learn how to redact sensitive data with GroupDocs.Redaction .NET. This
    step‑by‑step guide shows you how to create, apply, and save a redaction policy
    as XML.
  headline: How to redact sensitive data using GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to redact sensitive data with GroupDocs.Redaction .NET. This
    step‑by‑step guide shows you how to create, apply, and save a redaction policy
    as XML.
  name: How to redact sensitive data using GroupDocs.Redaction .NET
  steps:
  - name: prepare your document directory
    text: '*Replace `"YOUR_DOCUMENT_DIRECTORY"` with the folder that holds the documents
      you want to protect.*'
  - name: load the document
    text: The `Redactor` object opens the file and manages its lifecycle.
  - name: define the redactions
    text: 'ExactPhraseRedaction defines a rule that replaces a specific phrase, while
      `RegexRedaction` uses a regular expression to match patterns. Here we create
      two rules: 1. **ExactPhraseRedaction** – replaces a known phrase with “[REDACTED]”.
      2. **RegexRedaction** – finds dates in `YYYY‑MM‑DD` format and r'
  - name: apply the redactions
    text: All defined rules are executed against the opened document in one pass.
  - name: save the policy as an XML file
    text: The XML file stores the redaction definitions, allowing you to reuse the
      same policy without rewriting code.
  type: HowTo
- questions:
  - answer: Yes—use `redactor.LoadPolicy("policy.xml")` to import a previously saved
      policy.
    question: Can I load an existing XML policy instead of building one programmatically?
  - answer: 'Absolutely. Pass the password to the `Redactor` constructor: `new Redactor(sourceFile,
      "password")`.'
    question: Does GroupDocs.Redaction support password‑protected PDFs?
  - answer: The SDK provides `ImageRedaction` and `MetadataRedaction` classes for
      those scenarios.
    question: Is it possible to redact images or metadata?
  - answer: Process them in chunks or use the streaming API to reduce memory footprint;
      the engine can handle files up to 2 GB without loading the whole file into RAM.
    question: How do I handle large documents (hundreds of MB)?
  - answer: A paid license is required for production deployments; a trial license
      is fine for development and testing.
    question: What licensing model is required for commercial use?
  type: FAQPage
tags:
- redact sensitive data
- groupdocs redaction
- .net document security
- xml policy
- document redaction
title: GroupDocs.Redaction .NET ile hassas verileri nasıl kırpılır
type: docs
url: /tr/net/advanced-redaction/groupdocs-redaction-net-create-save-policy/
weight: 1
---

# GroupDocs.Redaction .NET kullanarak hassas verileri nasıl karartılır

Sözleşmeler, finansal raporlar veya hasta kayıtları içindeki gizli bilgileri korumak, modern uygulamalar için pazarlık edilemez bir gereksinimdir. Bu rehberde, .NET için GroupDocs.Redaction ile **hassas verileri nasıl karartacağınızı** SDK'yı kurmaktan, herhangi bir belge türüne uygulanabilen yeniden kullanılabilir XML politikalarını tanımlamaya kadar öğreneceksiniz.

## Hızlı cevaplar
- **“create redaction policy” ne anlama geliyor?** Bu, GroupDocs.Redaction'a gizli içeriği nasıl gizleyeceğini veya değiştireceğini söyleyen kurallar (metin, regex, görüntüler vb.) tanımlama sürecidir.  
- **Hangi kütüphaneye ihtiyacım var?** GroupDocs.Redaction for .NET, NuGet üzerinden temin edilebilir.  
- **Bir lisansa ihtiyacım var mı?** Geliştirme için ücretsiz deneme sürümü yeterlidir; üretim için kalıcı bir lisans gereklidir.  
- **Politikayı yeniden kullanabilir miyim?** Evet—XML olarak kaydedildikten sonra daha sonra yükleyebilir ve herhangi bir belgeye uygulayabilirsiniz.  
- **Hangi .NET sürümleri destekleniyor?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## Bir karartma politikası nedir?

Bir karartma politikası, *ne*yin kaldırılacağını veya değiştirileceğini ve *değiştirmenin* nasıl görüneceğini belirten kurallar koleksiyonudur. Politikayı bir kez oluşturarak, uygulamanız tarafından işlenen her belgeye tutarlı güvenlik standartları uygulayabilirsiniz.

## Bir karartma politikası nasıl çalışır?

`Redactor` motoru ile bir belge yükleyin, bir veya daha fazla karartma kuralı ekleyin ve ardından `Apply` metodunu çağırın. Motor belgeyi tarar, eşleşen içeriği maskeleyerek isteğe bağlı olarak yeni bir dosya oluşturur. Aynı kural seti XML olarak dışa aktarılabilir, böylece politikayı kodu yeniden derlemeden yeniden kullanabilirsiniz.

## Karartma politikası oluşturmak için neden GroupDocs.Redaction kullanılmalı?

GroupDocs.Redaction, karartma politikalarının oluşturulmasını, yönetilmesini ve yürütülmesini basitleştiren kapsamlı bir özellik seti sunar; farklı belge türlerinde tutarlı veri koruması sağlar, yüksek performans sunar ve ekipler ve organizasyonlar için mevcut .NET uygulamalarına kolay entegrasyon sağlar.

- **Geniş format desteği** – SDK, PDF, DOCX, XLSX, PPTX ve görüntü formatları dahil 30+ dosya türünü işleyebilir ve tüm dosyayı belleğe yüklemeden 2 GB'a kadar dosyaları işleyebilir.  
- **Programatik hassasiyet** – gizlemeniz gereken veriye yalnızca odaklanmak için kesin ifadeler, düzenli ifadeler veya özel mantık tanımlayın.  
- **Yeniden kullanılabilir XML politikaları** – kurallarınızı bir kez dışa aktarın ve ekipler, hizmetler veya mikro‑servisler arasında paylaşın.  
- **Performans‑optimize edilmiş motor** – kütüphane, tipik sunucu donanımında bir saniyeden kısa sürede çok sayfalı belgeleri işleyerek yüksek‑verimli hatlar için uygundur.

## Önkoşullar
- GroupDocs.Redaction kütüphanesi, .NET çalışma ortamınızla uyumlu olmalıdır.  
- Visual Studio, VS Code veya C# destekleyen herhangi bir IDE.  
- C# ve .NET proje yapısına temel aşinalık.

## GroupDocs.Redaction for .NET kurulumu

İlk olarak, kütüphaneyi projenize ekleyin.

**.NET CLI kullanarak**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Paket Yöneticisi kullanarak**  
```powershell
Install-Package GroupDocs.Redaction
```  

Veya NuGet Paket Yöneticisi UI'sinde “GroupDocs.Redaction”ı arayın ve oradan kurun.

### Lisans edinimi
- Özellikleri keşfetmek için **ücretsiz deneme** ile başlayın.  
- **Geçici lisans** isteyin, ardından üretim kullanımı için tam lisans satın alın.

### Temel başlatma
Kaynak dosyanıza ad alanını ekleyin:

`Redactor` sınıfı, bir belgeyi yükleyen ve karartma kurallarını uygulayan temel motorudur.  
```csharp
using GroupDocs.Redaction;
```  

`Redactor` sınıfı, GroupDocs.Redaction'ın bir belgeyi yükleyen ve karartma kurallarını uygulayan temel motorudur.

## Adım adım bir karartma politikası nasıl oluşturulur

Aşağıda, programlı olarak bir karartma politikası oluşturmayı, kurallarını yapılandırmayı, bir belgeye uygulamayı ve sonunda politikayı gelecekteki yeniden kullanım için bir XML dosyası olarak kalıcı hale getirmeyi gösteren eksiksiz bir rehber bulunmaktadır; bu, birden fazla proje ve belge türü arasında tutarlı karartma sağlar.

### Adım 1: belge dizininizi hazırlayın
```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
```  
*`"YOUR_DOCUMENT_DIRECTORY"` ifadesini korumak istediğiniz belgeleri içeren klasörle değiştirin.*

### Adım 2: belgeyi yükleyin
```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // Further code will go here
}
```  
`Redactor` nesnesi dosyayı açar ve yaşam döngüsünü yönetir.

### Adım 3: karartmaları tanımlayın
ExactPhraseRedaction, belirli bir ifadeyi değiştiren bir kural tanımlar, `RegexRedaction` ise desenleri eşleştirmek için bir düzenli ifade kullanır.  
```csharp
var redactions = new List<Redaction>
{
    new ExactPhraseRedaction("Sensitive Phrase", new ReplacementOptions("[REDACTED]")),
    new RegexRedaction(@"\d{4}-\d{2}-\d{2}", new ReplacementOptions("[DATE REDACTED]"))
};
```  
Burada iki kural oluşturuyoruz:  
1. **ExactPhraseRedaction** – bilinen bir ifadeyi “[REDACTED]” ile değiştirir.  
2. **RegexRedaction** – `YYYY‑MM‑DD` formatındaki tarihleri bulur ve “[DATE REDACTED]” ile değiştirir.

### Adım 4: karartmaları uygulayın
```csharp
redactor.Apply(redactions);
```  
Tanımlanan tüm kurallar, açılan belgeye tek bir geçişte uygulanır.

### Adım 5: politikayı bir XML dosyası olarak kaydedin
```csharp
string policyFile = "policy.xml";
redactor.SavePolicy(policyFile, new SaveOptions());
```  
XML dosyası karartma tanımlarını saklar, böylece aynı politikayı kodu yeniden yazmadan yeniden kullanabilirsiniz.

## Pratik uygulamalar

- **Hukuk firmaları**, taslakları paylaşmadan önce dava numaralarını ve müşteri adlarını karartabilir.  
- **Finans departmanları**, raporlarda hesap numaralarını veya işlem tarihlerini maskeleyebilir.  
- **Sağlık hizmeti sağlayıcıları**, hasta tanımlayıcılarını kaldırarak HIPAA uyumluluğunu sağlar.

## Performans ipuçları

- **Bir belgeyi aynı anda** açın, böylece bellek kullanımı düşük kalır.  
- **Verimli düzenli ifadeler** yazın; işleme süresini artıran çok geniş desenlerden kaçının.  
- Kütüphaneyi **güncel tutun**; böylece performans iyileştirmelerinden ve yeni karartma türlerinden faydalanabilirsiniz.

## Yaygın sorunlar ve çözümler

| Sorun | Neden oluşur | Çözüm |
|-------|--------------|-------|
| **Dizin hazırlanırken IO istisnası** | Yanlış yol veya yazma izinlerinin eksik olması | Klasörün var olduğunu ve uygulamanın okuma/yazma izinlerine sahip olduğunu doğrulayın. |
| **Regex beklenen metni eşleştirmiyor** | Desen çok katı veya kaçış karakterleri eksik | Regex'i çevrimiçi bir test aracıyla deneyin; miktar belirleyicileri ayarlayın veya özel karakterleri kaçırın. |
| **Politika dosyası oluşturulmadı** | `SavePolicy` karartmalar uygulanmadan önce veya geçersiz bir yol ile çağrıldığında | Çıktı dizininin yazılabilir olduğundan emin olun ve `Apply` sonrası `SavePolicy`'yi çağırın. |

## Sıkça sorulan sorular

**S:** Programlı olarak bir XML politikası oluşturmak yerine mevcut bir XML politikasını yükleyebilir miyim?  
A: Evet—önceden kaydedilmiş bir politikayı içe aktarmak için `redactor.LoadPolicy("policy.xml")` kullanın.

**S:** GroupDocs.Redaction şifre korumalı PDF'leri destekliyor mu?  
A: Kesinlikle. Şifreyi `Redactor` yapıcısına geçirin: `new Redactor(sourceFile, "password")`.

**S:** Görüntüleri veya meta verileri karartmak mümkün mü?  
A: SDK, bu senaryolar için `ImageRedaction` ve `MetadataRedaction` sınıflarını sağlar.

**S:** Büyük belgelerle (yüzlerce MB) nasıl başa çıkılır?  
A: Bölümler halinde işleyin veya bellek ayak izini azaltmak için akış API'sini kullanın; motor, tüm dosyayı RAM'e yüklemeden 2 GB'a kadar dosyaları işleyebilir.

**S:** Ticari kullanım için hangi lisans modeli gereklidir?  
A: Üretim dağıtımları için ücretli bir lisans gereklidir; geliştirme ve test için deneme lisansı yeterlidir.

## Sonuç

Artık GroupDocs.Redaction for .NET ile herhangi bir belgeye uygulayabileceğiniz eksiksiz, yeniden kullanılabilir bir **karartma politikası**na sahipsiniz. Politikayı XML olarak dışa aktararak gelecekteki güncellemeleri basitleştirir ve organizasyonunuzda tutarlı veri koruması sağlarsınız.

### Sonraki adımlar
- `ImageRedaction` veya `MetadataRedaction` gibi ek karartma türleriyle deney yapın.  
- Politika yükleme mantığını belge‑yönetim iş akışınıza entegre ederek otomatik karartma sağlayın.  
- **GroupDocs.Redaction** API referansını ileri düzey özelleştirme için keşfedin.

---

**Son Güncelleme:** 2026-10-06  
**Test Edilen:** GroupDocs.Redaction 5.8 for .NET  
**Yazar:** GroupDocs  

**Kaynaklar**  
- [Dokümantasyon](https://docs.groupdocs.com/redaction/net/)  
- [API Referansı](https://reference.groupdocs.com/redaction/net)  
- [İndirme](https://releases.groupdocs.com/redaction/net/)  
- [Ücretsiz Destek Forumu](https://forum.groupdocs.com/c/redaction/33)  
- [Geçici Lisans Başvurusu](https://purchase.groupdocs.com/temporary-license/)

## İlgili Eğitimler

- [GroupDocs.Redaction .NET (C#) ile Hassas Verileri Karartın](/redaction/net/advanced-redaction/groupdocs-redaction-net-implement-iredactioncallback-csharp/)
- [GroupDocs.Redaction .NET Kullanarak Belge Karartma Uygulaması: Adım Adım Kılavuz](/redaction/net/getting-started/implement-document-redaction-groupdocs-redaction-net/)
- [GroupDocs.Redaction .NET ile Belgeleri Nasıl Karartılır – Tam Kılavuz](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)