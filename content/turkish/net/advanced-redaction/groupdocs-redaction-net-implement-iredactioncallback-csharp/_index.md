---
date: '2026-03-30'
description: GroupDocs.Redaction .NET'i C#'da IRedactionCallback uygulamasıyla kullanarak
  hassas verileri nasıl kırpacağınızı öğrenin. Adım adım kılavuz, en iyi uygulamalar
  ve gerçek dünya örnekleri.
keywords:
- GroupDocs.Redaction .NET
- Implementing IRedactionCallback
- secure document redaction
title: GroupDocs.Redaction .NET (C#) ile Hassas Verileri Kırpın
type: docs
url: /tr/net/advanced-redaction/groupdocs-redaction-net-implement-iredactioncallback-csharp/
weight: 1
---

# GroupDocs.Redaction .NET (C#) ile Hassas Verileri Kırpma

Bugünün dijital ortamında, yasal, finansal veya İK belgelerinden **redact sensitive data** (hassas verileri kırpma) zorunlu bir gerekliliktir. İster dış inceleme için bir sözleşme hazırlıyor olun, ister raporu kamuya açıklamadan önce temizliyor olun, tek bir kişisel tanımlayıcının eksik olması uyum ihlallerine yol açabilir. GroupDocs.Redaction for .NET, gizli bilginin tam olarak istediğiniz şekilde yok olmasını sağlayan güçlü, programatik bir yol sunar. Bu öğreticide, bir `IRedactionCallback` uygulamasını eklemeyi adım adım göstereceğiz, böylece kırpma iş akışını özelleştirebilir ve her adım üzerinde tam kontrol sahibi olabilirsiniz.

## Hızlı Yanıtlar
- **IRedactionCallback ne işe yarar?** Kırpma olaylarını yakalamanıza, bunları kaydetmenize veya davranışı anında değiştirmenize olanak tanır.  
- **Bir lisansa ihtiyacım var mı?** Deneme sürümü geliştirme için çalışır; kalıcı bir lisans tüm değerlendirme sınırlamalarını kaldırır.  
- **Hangi .NET sürümleri destekleniyor?** .NET Core 3.1+, .NET 5/6, ve .NET Framework 4.6+.  
- **Birden fazla dosyayı işleyebilir miyim?** Evet—mantığı bir döngü içinde sarın veya en iyi performans için toplu işleme kullanın.  
- **Asenkron kırpma mümkün mü?** Yerleşik değil, ancak API çağrılarını `Task.Run` içinde veya diğer async desenlerde çalıştırabilirsiniz.

## Hassas Verileri Kırpma Nedir?
Kırpma, açıklanmaması gereken bilgileri kalıcı olarak kaldırma veya gizleme sürecidir. GroupDocs.Redaction ile tam ifadeler, desenler veya özel kurallar tanımlayabilir ve bunları yer tutucularla (ör. **[REDACTED]**) değiştirebilir, orijinal belge düzenini koruyabilirsiniz.

## IRedactionCallback ile GroupDocs.Redaction Neden Kullanılmalı?
- **Tam denetlenebilirlik:** Callback, gerçekleştirilen her kırpmanın ayrıntılı kaydını sağlar.  
- **Özel işleme:** Metni değiştirin, dış hizmetleri tetikleyin veya iş kurallarını dinamik olarak uygulayın.  
- **Ölçeklenebilir performans:** Callback'leri toplu işleme ile birleştirerek binlerce dosyayı verimli bir şekilde işleyin.

## Önkoşullar
Before we dive in, make sure you have:

- **GroupDocs.Redaction** kütüphanesi (uyumlu sürüm – resmi [documentation page](https://docs.groupdocs.com/redaction/net/) sayfasına bakın).  
- Geliştirme makinenizde .NET Core veya .NET Framework yüklü olmalı.  
- Visual Studio (Community sürümü yeterlidir) veya C# destekleyen herhangi bir IDE.  
- Temel C# bilgisi ve NuGet paket yönetimi konusunda aşinalık.

## .NET için GroupDocs.Redaction Kurulumu
İlk olarak, kütüphaneyi projenize ekleyin. Tercih ettiğiniz yöntemi seçin – CLI, Package Manager Console veya UI. Komutlar orijinal öğreticideki gibi aynı kalır.

### Kurulum Seçenekleri
**.NET CLI:**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager Console:**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI:**  
- Projenizi Visual Studio'da açın.  
- **Manage NuGet Packages** bölümüne gidin.  
- **GroupDocs.Redaction**'ı arayın ve en son kararlı sürümü yükleyin.

### Lisans Alımı
Ürünü denemek için, [buradan](https://purchase.groupdocs.com/temporary-license/) ücretsiz deneme veya geçici lisans talep edin. Üretim ortamında kullanmak için, tüm özelliklerin sınırsız olarak açılması için tam lisans satın alın.

#### Temel Başlatma ve Kurulum
Aşağıda, `Redactor` sınıfı ile bir belge açmak için gereken en temel kod bulunmaktadır. Bu snippet'i değiştirmeyin – sonraki tüm adımların temeli budur.

```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx"; // Replace with actual path

using (Redactor redactor = new Redactor(sourceFile))
{
    // Your redaction logic here
}
```

## Uygulama Kılavuzu
Şimdi temel kurulumu, özel bir `IRedactionCallback` ekleyerek genişleteceğiz. Bu, her kırpma olayını yakalamanıza, bir loga yazmanıza veya anında değiştirme metnini değiştirmenize olanak tanır.

### Bir IRedactionCallback Uygulamasını Bağlama ve Kullanma
Aşağıdaki adımlar, dosya yollarını hazırlamaktan tam ifadeli kırpma uygulamaya kadar tam iş akışını gösterir.

#### Adım 1: Çıktı Dizini ve Kaynak Dosya Yolunu Hazırlama
Kaynak belgenizin bulunduğu yeri tanımlayın. Yolunuzu ortamınıza göre ayarlayın.

```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx"; // Replace with actual path
```

#### Adım 2: Özel Ayarlarla Redactor Örneği Oluşturma
`Redactor`'ı `LoadOptions` ve `RedactorSettings` ile örnekliyoruz. Ayarlar içindeki `RedactionDump`, gerçekleşen her kırpmayı otomatik olarak kaydedecek.

```csharp
using (Redactor redactor = new Redactor(sourceFile, 
    new LoadOptions(), 
    new RedactorSettings(new RedactionDump())))
{
    // Further processing steps will go here
}
```

#### Adım 3: Tam İfade Kırpması Uygulama
Burada **John Doe** ifadesini **[REDACTED]** yer tutucusuyla değiştiriyoruz. Gizlemeniz gereken herhangi bir ifade veya deseni değiştirebilirsiniz.

```csharp
redactor.Apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[REDACTED]")));
```

**Ana nesnelerin açıklaması:**
- `LoadOptions()` – SDK'ye belgeyi nasıl okuyacağını söyler (ör. şifre yönetimi).  
- `RedactorSettings(new RedactionDump())` – denetim amaçlı her kırpmayı kaydeden bir döküm dosyası etkinleştirir.  
- `ReplacementOptions("[REDACTED]")` – eşleşen ifadeyi değiştirecek metni tanımlar.

### Bunun Önemi
`IRedactionCallback` kullanarak, aşağıdaki gibi özel mantıklar ekleyebilirsiniz:
- Kırpma detaylarını uyum veritabanına gönderme.  
- Basit ifade değişimiyle kapsanmayan ek meta verileri maskeleme.  
- İçerik türüne göre dinamik olarak değiştirme metni seçme.

### Sorun Giderme İpuçları
- **Dosya bulunamadı:** `sourceFile` yolunu iki kez kontrol edin ve dosyanın çalışan süreç tarafından erişilebilir olduğundan emin olun.  
- **Callback çalışmıyor:** Sınıfınızın `IRedactionCallback`'in **tüm** üyelerini uyguladığını ve örneğin `Redactor`'a doğru şekilde geçirildiğini doğrulayın.  
- **Performans gecikmesi:** Büyük toplu işlemlerde, mümkün olduğunda aynı `Redactor` örneğini yeniden kullanın ve hemen dispose edin.

## Pratik Uygulamalar
Hassas verileri kırpma birçok sektörde faydalıdır:

1. **Legal Document Processing** – Müşteri adları, dava numaraları veya sosyal güvenlik numaralarını taslakları paylaşmadan önce otomatik olarak kaldırır.  
2. **HR Management Systems** – Denetimler sırasında çalışan sözleşmelerinden kişisel tanımlayıcıları kaldırır.  
3. **Financial Reporting** – Yatırımcıya yönelik PDF'ler oluştururken özel rakamları veya hesap numaralarını gizler.

## Performans Düşünceleri
Onlarca ya da yüzlerce dosya işlenirken uygulamanızın hızlı kalmasını sağlamak için:

- **Toplu İşleme:** Dosyaların bir listesini yükleyin ve çok çekirdek kullanımını sağlamak için kırpma döngüsünü `Parallel.ForEach` içinde çalıştırın.  
- **Bellek Yönetimi:** Her `Redactor`'ı bir `using` bloğu içinde sarın (gösterildiği gibi) ve disposal'ı garanti edin.  
- **Asenkron İşlemler:** SDK kendisi senkron olsa da, işi arka plan iş parçacıklarına veya `Task.Run`'a devrederek UI iş parçacıklarını engellemekten kaçınabilirsiniz.

## Yaygın Sorunlar ve Çözümler

| Sorun | Çözüm |
|-------|----------|
| **“Invalid file format” error** | Belge tipinin desteklendiğinden emin olun (PDF, DOCX, PPTX, vb.). |
| **Callback receives null values** | `RedactorSettings` oluştururken `IRedactionCallback`'in somut bir uygulamasını geçtiğinizden emin olun. |
| **Redaction not applied** | Tam ifadenin belgenin büyük/küçük harf ve boşluk düzeniyle eşleştiğini doğrulayın veya desen tabanlı eşleşme için `RegexRedaction` kullanın. |

## Sıkça Sorulan Sorular

**S: GroupDocs.Redaction için lisans seçenekleri nelerdir?**  
C: Ücretsiz bir deneme ile başlayabilir veya tüm özellikleri keşfetmek için geçici bir lisans talep edebilirsiniz. Üretim için kalıcı veya abonelik lisansı satın alın.

**S: GroupDocs.Redaction'ı birden fazla dosya türünde kullanabilir miyim?**  
C: Evet, PDF, Word, Excel, PowerPoint ve birçok diğer yaygın formatı destekler.

**S: Kırpma sırasında oluşan istisnaları nasıl ele alırım?**  
C: Kırpma mantığınızı `try‑catch` blokları içinde sarın ve istisna detaylarını kaydedin. Callback ayrıca hataları gerçek zamanlı yakalamak için kullanılabilir.

**S: Asenkron işleme için yerleşik destek var mı?**  
C: Çekirdek API senkron olsa da, kırpma çağrılarını asenkron görevler veya arka plan servisleri içinde çalıştırabilirsiniz.

**S: Daha gelişmiş örnekleri nerede bulabilirim?**  
C: [Resmi dokümantasyon](https://docs.groupdocs.com/redaction/net/) ve API referansı kapsamlı kod örnekleri ve senaryo kılavuzları sunar.

## Kaynaklar

- [GroupDocs.Redaction .NET Dokümantasyonu](https://docs.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction .NET API Referansı](https://reference.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction .NET'i İndir](https://releases.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction Forum](https://forum.groupdocs.com/c/redaction/33)
- [Ücretsiz Destek](https://forum.groupdocs.com/)
- [Geçici Lisans](https://purchase.groupdocs.com/temporary-license/)

---

**Son Güncelleme:** 2026-03-30  
**Test Edilen Versiyon:** GroupDocs.Redaction 2.3 (latest at time of writing)  
**Yazar:** GroupDocs