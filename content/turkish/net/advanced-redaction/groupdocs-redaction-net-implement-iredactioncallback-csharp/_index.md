---
date: '2026-10-06'
description: GroupDocs.Redaction .NET'i C#'da IRedactionCallback uygulamasıyla kullanarak
  verileri nasıl kırparacağınızı öğrenin. Bu adım adım kılavuzu, en iyi uygulamaları
  ve gerçek dünya örneklerini izleyin.
keywords:
- how to redact data
- GroupDocs.Redaction .NET
- IRedactionCallback implementation
- document redaction C#
lastmod: '2026-10-06'
og_description: GroupDocs.Redaction .NET'i C#'da IRedactionCallback uygulamasıyla
  kullanarak verileri nasıl kırparacağınızı öğrenin. En iyi uygulamalar ve gerçek
  dünya örnekleriyle adım adım bir kılavuzu izleyin.
og_image_alt: Guide to redact data with GroupDocs.Redaction .NET in C#
og_title: GroupDocs.Redaction .NET (C#) ile verileri nasıl kırparız
schemas:
- author: GroupDocs
  dateModified: '2026-10-06'
  description: Learn how to redact data using GroupDocs.Redaction .NET with an IRedactionCallback
    implementation in C#. Follow this step‑by‑step guide, best practices, and real‑world
    examples.
  headline: How to redact data with GroupDocs.Redaction .NET (C#)
  type: TechArticle
- description: Learn how to redact data using GroupDocs.Redaction .NET with an IRedactionCallback
    implementation in C#. Follow this step‑by‑step guide, best practices, and real‑world
    examples.
  name: How to redact data with GroupDocs.Redaction .NET (C#)
  steps:
  - name: prepare output directory and source file path
    text: Define where your source document lives. Adjust the path to match your environment.
      `LoadOptions` is a configuration object that tells the SDK how to read the file
      (e.g., password handling).
  - name: create a Redactor instance with custom settings
    text: We instantiate `Redactor` with `LoadOptions` and `RedactorSettings`. The
      `RedactionDump` inside the settings will automatically record every redaction
      that occurs. `RedactorSettings` lets you fine‑tune the redaction process; passing
      a `RedactionDump` enables a detailed audit file. `RedactionDump` is
  - name: apply an exact‑phrase redaction
    text: Here we replace the phrase **John Doe** with the placeholder **[REDACTED]**.
      You can swap any phrase or pattern you need to hide. `ReplacementOptions` defines
      what text will replace the matched content. It also supports font and color
      customisation if you need a visual mask. **Explanation of the key
  type: HowTo
- questions:
  - answer: You can start with a free trial or request a temporary license to explore
      all features. For production, purchase a perpetual or subscription license.
    question: What are the licensing options for GroupDocs.Redaction?
  - answer: Yes, it supports PDFs, Word, Excel, PowerPoint, and many other common
      formats.
    question: Can I use GroupDocs.Redaction on multiple file types?
  - answer: Wrap your redaction logic in `try‑catch` blocks and log the exception
      details. The callback can also be used to capture errors in real time.
    question: How do I handle exceptions during redaction?
  - answer: The core API is synchronous, but you can run redaction calls inside asynchronous
      tasks or background services.
    question: Is there built‑in support for asynchronous processing?
  - answer: The [official documentation](https://docs.groupdocs.com/redaction/net/)
      and API reference provide extensive code samples and scenario guides.
    question: Where can I find more advanced examples?
  type: FAQPage
tags:
- redact data
- GroupDocs.Redaction
- .NET redaction
- C# document security
- IRedactionCallback
title: GroupDocs.Redaction .NET (C#) ile verileri nasıl kırparız
type: docs
url: /tr/net/advanced-redaction/groupdocs-redaction-net-implement-iredactioncallback-csharp/
weight: 1
---

# GroupDocs.Redaction .NET (C#) ile verileri nasıl karartılır

Bu kapsamlı öğreticide, GroupDocs.Redaction for .NET kullanarak PDF'ler, Word dosyaları ve diğer belgelerden **verileri nasıl karartılır** keşfedeceksiniz. Hukuki sözleşmelerde kişisel tanımlayıcıları gizlemeniz ya da finansal raporlardan gizli rakamları temizlemeniz gerektiğinde, SDK size programatik kontrol sağlayarak her hassas öğenin kalıcı ve denetlenebilir şekilde yok olmasını garantiler. Kütüphaneyi kurma, özel bir `IRedactionCallback` yapılandırma ve tam günlükleme ile tam ifadeli karartma uygulama adımlarını göstereceğiz.

## Hızlı cevaplar
- **IRedactionCallback ne işe yarar?** Her karartma olayını yakalamanızı, ayrıntıları günlüğe kaydetmenizi ve isteğe bağlı olarak yer değiştirme metnini anında değiştirmenizi sağlar.  
- **Bir lisansa ihtiyacım var mı?** Deneme sürümü geliştirme için çalışır; kalıcı bir lisans tüm değerlendirme sınırlamalarını kaldırır.  
- **Hangi .NET sürümleri destekleniyor?** .NET Core 3.1+, .NET 5/6 ve .NET Framework 4.6+.  
- **Birden fazla dosyayı işleyebilir miyim?** Evet—mantığı bir döngü içinde sarabilir veya en iyi performans için toplu işleme kullanabilirsiniz.  
- **Asenkron karartma mümkün mü?** Yerleşik değildir, ancak API çağrılarını `Task.Run` içinde veya diğer async desenlerde çalıştırabilirsiniz.

## Hassas verileri karartma nedir?
`Redaction`, açıklanmaması gereken bilgilerin kalıcı olarak kaldırılması veya gizlenmesidir. GroupDocs.Redaction ile tam ifadeler, düzenli ifade kalıpları veya özel kurallar tanımlayabilir ve bunları **[REDACTED]** gibi yer tutucularla değiştirirken orijinal düzen ve sayfalama korunur.

## IRedactionCallback ile GroupDocs.Redaction neden kullanılır?
`IRedactionCallback`, SDK bir içerik parçasını kararttığında sizi bilgilendiren bir arayüzdür; denetim verilerini yakalamanıza veya yer değiştirmeyi dinamik olarak ayarlamanıza olanak tanır. Bu, tam denetlenebilirlik, özel iş kuralı uygulaması ve uyumluluk sistemleriyle sorunsuz entegrasyon sağlar—performanstan ödün vermeden.

## Önkoşullar
- **GroupDocs.Redaction** kütüphanesi (uyumlu sürüm – resmi [dokümantasyon sayfası](https://docs.groupdocs.com/redaction/net/) ). Tam detaylar için [resmi dokümantasyon](https://docs.groupdocs.com/redaction/net/) adresine bakın.  
- Geliştirme makinenizde .NET Core veya .NET Framework yüklü olmalıdır.  
- Visual Studio (Community sürümü yeterlidir) veya C# destekleyen herhangi bir IDE.  
- Temel C# bilgisi ve NuGet paket yönetimi konusunda aşinalık.

## .NET için GroupDocs.Redaction kurulumu
İlk olarak, kütüphaneyi projenize ekleyin. Tercih ettiğiniz yöntemi seçin – CLI, Package Manager Console veya UI. Komutlar orijinal öğreticideki gibi aynı kalır.

### Kurulum seçenekleri
**.NET CLI:**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager Console:**  
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI:**  
- Visual Studio'da projenizi açın.  
- **Manage NuGet Packages** seçeneğine gidin.  
- **GroupDocs.Redaction** aratın ve en son stabil sürümü kurun.

### Lisans edinimi
Ürünü denemek için, [buradan](https://purchase.groupdocs.com/temporary-license/) ücretsiz deneme veya geçici lisans talep edin. Ayrıca [geçici lisans sayfası](https://purchase.groupdocs.com/temporary-license/) üzerinden geçici lisans alabilirsiniz. Üretim kullanımında, tüm özelliklerin sınırsız olarak açılması için tam lisans satın alın.

#### Temel başlatma ve kurulum
Aşağıda `Redactor` sınıfı ile bir belge açmak için gereken minimum kod bulunmaktadır. Bu snippet'i değiştirmeyin – sonraki tüm adımların temeli budur.  
`Redactor`, bir belgeyi temsil eden ve karartma kurallarını uygulayan yöntemler sağlayan temel sınıftır.  
```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx"; // Replace with actual path

using (Redactor redactor = new Redactor(sourceFile))
{
    // Your redaction logic here
}
```

## Uygulama rehberi
Şimdi temel kurulumu, özel bir `IRedactionCallback` ekleyerek genişleteceğiz. Bu, her karartma olayını yakalamanıza, bir loga yazmanıza veya yer değiştirme metnini anında değiştirmenize olanak tanır.

### IRedactionCallback uygulamasını ekleme ve kullanma
`IRedactionCallback`, her karartma işlemi için geri arama (callback) alan bir arayüzdür; böylece programatik olarak günlük tutabilir veya davranışı değiştirebilirsiniz.

#### Adım 1: çıktı dizinini ve kaynak dosya yolunu hazırlama
Kaynak belgenizin nerede olduğunu tanımlayın. Yolunu ortamınıza göre ayarlayın.

`LoadOptions`, SDK'ya dosyayı nasıl okuyacağını (örneğin, şifre yönetimi) söyleyen bir yapılandırma nesnesidir.  
```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx"; // Replace with actual path
```

#### Adım 2: özel ayarlarla Redactor örneği oluşturma
`Redactor`'ı `LoadOptions` ve `RedactorSettings` ile örnekliyoruz. Ayarlar içindeki `RedactionDump`, gerçekleşen her karartmayı otomatik olarak kaydeder.

`RedactorSettings`, karartma sürecini ince ayar yapmanıza olanak tanır; bir `RedactionDump` geçirildiğinde detaylı bir denetim dosyası etkinleştirilir.  
`RedactionDump`, her karartma olayını uyumluluk raporlaması için JSON formatında bir döküm dosyasına yazan yardımcı bir sınıftır.  
```csharp
using (Redactor redactor = new Redactor(sourceFile, 
    new LoadOptions(), 
    new RedactorSettings(new RedactionDump())))
{
    // Further processing steps will go here
}
```

#### Adım 3: tam ifadeli karartma uygulama
Burada **John Doe** ifadesini **[REDACTED]** yer tutucusuyla değiştiriyoruz. Gizlemeniz gereken herhangi bir ifade veya deseni değiştirebilirsiniz.

`ReplacementOptions`, eşleşen içeriğin neyle değiştirileceğini tanımlar. Görsel maske ihtiyacınız varsa font ve renk özelleştirmesini de destekler.  
```csharp
redactor.Apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[REDACTED]")));
```

**Ana nesnelerin açıklaması**
- `LoadOptions()` – SDK'ya belgeyi nasıl okuyacağını (örneğin, şifre yönetimi) söyler.  
- `RedactorSettings(new RedactionDump())` – denetim amaçlı her karartmayı kaydeden bir döküm dosyası etkinleştirir.  
- `ReplacementOptions("[REDACTED]")` – eşleşen ifadeyi değiştirecek metni tanımlar.

### Bunun önemi
Geri arama mekanizması her karartma olayını kaydeder, makine tarafından okunabilir bir denetim izi oluşturur ve yer tutucuları dinamik olarak değiştirmenize izin verir; bu, uyumluluk gereksinimlerini karşılamaya yardımcı olur ve manuel sonrası işlem çabasını azaltır. Bu veriyi izleme sistemlerinizle entegre ederek raporlar oluşturabilir, uyarılar tetikleyebilir ve hiçbir hassas bilginin karartma hattından kaçmadığından emin olabilirsiniz.

`IRedactionCallback` kullanmak size üç somut avantaj sağlar:
1. **Uyumluluk‑hazır günlükler** – her karartma, makine‑okunur bir dökümde yakalanır ve 30+ düzenleyici çerçeve için denetim gereksinimlerini karşılar.  
2. **Dinamik yer değiştirme** – veri tipine göre yer tutucuyu değiştirebilir, manuel sonrası işlemi %40'a kadar azaltabilirsiniz.  
3. **Ölçeklenebilir performans** – geri arama, her karartma için <2 ms gibi ihmal edilebilir bir ek yük eklerken, binlerce dosyayı paralel olarak toplu olarak işleyebilmenizi sağlar.

### Sorun giderme ipuçları
- **Dosya bulunamadı:** `sourceFile` yolunu iki kez kontrol edin ve dosyanın çalışan süreç tarafından erişilebilir olduğundan emin olun.  
- **Callback çalışmıyor:** Sınıfınızın `IRedactionCallback`'in **tüm** üyelerini uyguladığını ve örneğin `Redactor`'a doğru şekilde geçirildiğini doğrulayın.  
- **Performans gecikmesi:** Büyük toplular için mümkün olduğunca aynı `Redactor` örneğini yeniden kullanın ve zamanında dispose edin.

## Pratik uygulamalar
Hassas verileri karartmak birçok sektörde faydalıdır:
1. **Hukuki belge işleme** – Taslakları paylaşmadan önce müşteri adlarını, dava numaralarını veya sosyal güvenlik numaralarını otomatik olarak kaldırın.  
2. **İK yönetim sistemleri** – Denetimler sırasında çalışan sözleşmelerinden kişisel tanımlayıcıları kaldırın.  
3. **Finansal raporlama** – Yatırımcıya yönelik PDF'ler oluştururken özel rakamları veya hesap numaralarını gizleyin.

## Performans değerlendirmeleri
GroupDocs.Redaction **30+ giriş ve çıkış formatını** (PDF, DOCX, PPTX, XLSX, HTML ve görüntü türleri) destekler ve tüm belgeyi belleğe yüklemeden çok sayfalı dosyaları işleyebilir. Onlarca veya yüzlerce dosya işlenirken uygulamanızın hızlı kalması için:
- **Toplu işleme:** Dosya listesini yükleyin ve karartma döngüsünü çok çekirdekli kullanım için `Parallel.ForEach` içinde çalıştırın.  
- **Bellek yönetimi:** Her `Redactor`'ı bir `using` bloğu içinde sarın (gösterildiği gibi) ve doğru şekilde dispose edilmesini sağlayın.  
- **Asenkron işlemler:** SDK kendisi senkron olsa da, işi arka plan iş parçacıklarına veya `Task.Run`'a aktararak UI iş parçacıklarını engellemekten kaçınabilirsiniz.

## Yaygın sorunlar ve çözümler
| Sorun | Çözüm |
|-------|----------|
| **“Geçersiz dosya formatı” hatası** | Belge tipinin desteklendiğinden (PDF, DOCX, PPTX, vb.) emin olun. |
| **Callback null değerler alıyor** | `RedactorSettings` oluştururken `IRedactionCallback`'in somut bir uygulamasını geçtiğinizden emin olun. |
| **Karartma uygulanmadı** | Tam ifadenin belgenin büyük/küçük harf ve boşluklarıyla eşleştiğini doğrulayın veya desen tabanlı eşleşme için `RegexRedaction` kullanın. |

## Sıkça sorulan sorular
**Q:** GroupDocs.Redaction için lisans seçenekleri nelerdir?  
**A:** Ücretsiz deneme ile başlayabilir veya tüm özellikleri keşfetmek için geçici lisans talep edebilirsiniz. Üretim için kalıcı veya abonelik lisansı satın alın.

**Q:** GroupDocs.Redaction'ı birden fazla dosya türünde kullanabilir miyim?  
**A:** Evet, PDF, Word, Excel, PowerPoint ve birçok diğer yaygın formatı destekler.

**Q:** Karartma sırasında istisnaları nasıl ele alırım?  
**A:** Karartma mantığınızı `try‑catch` blokları içinde sarın ve istisna detaylarını günlüğe kaydedin. Callback aynı zamanda hataları gerçek zamanlı yakalamak için kullanılabilir.

**Q:** Asenkron işleme için yerleşik destek var mı?  
**A:** Çekirdek API senkron olsa da, karartma çağrılarını asenkron görevler veya arka plan servisleri içinde çalıştırabilirsiniz.

**Q:** Daha gelişmiş örnekleri nerede bulabilirim?  
**A:** [Resmi dokümantasyon](https://docs.groupdocs.com/redaction/net/) ve API referansı kapsamlı kod örnekleri ve senaryo kılavuzları sunar.

## Kaynaklar
- [GroupDocs.Redaction .NET Dokümantasyonu](https://docs.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction .NET API Referansı](https://reference.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction .NET'i İndir](https://releases.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction Forumu](https://forum.groupdocs.com/c/redaction/33)
- [Ücretsiz Destek](https://forum.groupdocs.com/)
- [Geçici Lisans](https://purchase.groupdocs.com/temporary-license/)

---

**Son Güncelleme:** 2026-10-06  
**Test Edilen Versiyon:** GroupDocs.Redaction 2.3 (latest at time of writing)  
**Yazar:** GroupDocs

## İlgili Öğreticiler
- [GroupDocs.Redaction .NET ile Karartma Politikası Oluşturma – Adım Adım Kılavuz](/redaction/net/advanced-redaction/groupdocs-redaction-net-create-save-policy/)
- [GroupDocs.Redaction .NET ile Belgeleri Karartma – Tam Kılavuz](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [Akışlar Kullanarak .NET Belgelerini Karartma – GroupDocs.Redaction Kılavuzu](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)