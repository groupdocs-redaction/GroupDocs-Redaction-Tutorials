---
date: '2026-06-01'
description: GroupDocs.Redaction for .NET ile belgelerden hassas bilgileri redact
  etmeyi ve açıklamaları kaldırmayı öğrenin, compliance ve data privacy sağlayarak.
keywords:
- redact sensitive information
- how to remove annotations
- remove excel annotations
schemas:
- author: GroupDocs
  dateModified: '2026-06-01'
  description: Learn how to redact sensitive information and how to remove annotations
    from documents with GroupDocs.Redaction for .NET, ensuring compliance and data
    privacy.
  headline: How to Redact Sensitive Information and Remove Annotations Using GroupDocs.Redaction
    for .NET
  type: TechArticle
- description: Learn how to redact sensitive information and how to remove annotations
    from documents with GroupDocs.Redaction for .NET, ensuring compliance and data
    privacy.
  name: How to Redact Sensitive Information and Remove Annotations Using GroupDocs.Redaction
    for .NET
  steps:
  - name: Prepare Source and Output File Paths
    text: 'First, define the locations of your input document and the folder where
      the redacted file will be saved. Ensure the output directory exists; otherwise
      the operation will fail. *Definition anchor:* `Path.Combine` is a .NET utility
      that safely joins directory and file names across Windows, Linux, and '
  - name: Apply Regular Expression Redaction
    text: Next, create a redaction rule that targets annotations matching your regex
      pattern. *Definition anchor:* `Redactor` is the main class that loads a document
      and applies redaction rules. *Definition anchor:* `DeleteAnnotationRedaction`
      is a class that removes annotations whose content satisfies a regu
  - name: Dispose of Resources
    text: Always call `redactor.Dispose()` or wrap the instance in a `using` block
      to free unmanaged resources promptly. *Definition anchor:* `Dispose` releases
      unmanaged resources used by the Redactor instance, ensuring memory is freed.
  type: HowTo
- questions:
  - answer: Yes—by loading the `.xlsx` file with `Redactor` and applying a `DeleteAnnotationRedaction`
      rule, you can remove comments, notes, and other annotation types.
    question: Can GroupDocs.Redaction redact annotations in Excel workbooks?
  - answer: Prefix the pattern with `(?i)` or use the `RegexOptions.IgnoreCase` flag
      when constructing the `DeleteAnnotationRedaction`.
    question: How do I make regex patterns case‑insensitive?
  - answer: Absolutely. Set `SaveOptions.Prefix` or `SaveOptions.Suffix` to prepend
      or append text to the generated file name.
    question: Is it possible to customize the output file name?
  - answer: The source file remains untouched; the redacted version is saved to the
      path you provide in `SaveOptions`.
    question: What happens to the original document after redaction?
  - answer: Yes—GroupDocs.Redaction can operate in a streaming mode that processes
      pages sequentially, dramatically reducing memory consumption.
    question: Does the library support streaming for very large PDFs?
  type: FAQPage
title: GroupDocs.Redaction for .NET Kullanarak Hassas Bilgileri redact Etme ve Açıklamaları
  Kaldırma
type: docs
url: /tr/net/annotation-redaction/remove-annotations-groupdocs-redaction-net/
weight: 1
---

# GroupDocs.Redaction for .NET Kullanarak Hassas Bilgileri Kırp ve Açıklamaları Kaldır

Belgelerdeki gizli verileri yönetmek, geliştiriciler, denetçiler ve hukuk ekipleri için günlük bir zorluktur. **Hassas bilgileri kırp** hızlı ve güvenilir bir şekilde GroupDocs.Redaction for .NET ile, 30'dan fazla dosya formatında çalışan ve tüm belgeyi belleğe yüklemeden 2 GB'a kadar dosyaları işleyebilen bir kütüphanedir. Bu öğretici, paketin kurulumu ve düzenli ifadelerle belirli açıklamaları kaldırmaya kadar tam iş akışını adım adım gösterir—böylece kişisel verileri koruyabilir ve GDPR ve HIPAA gibi düzenlemelere uyum sağlayabilirsiniz.

## Hızlı Yanıtlar
- **GroupDocs.Redaction ne yapar?** Metin, görüntü ve açıklamaları programlı olarak kaldırır veya maskeleştirir, özel verileri korur.  
- **Hangi dosya türleri destekleniyor?** PDF, DOCX, XLSX, PPTX ve görüntü dosyaları dahil 30'dan fazla format.  
- **Geliştirme için lisansa ihtiyacım var mı?** Test için ücretsiz deneme çalışır; üretim için kalıcı bir lisans gereklidir.  
- **Büyük dosyaları verimli bir şekilde işleyebilir miyim?** Evet—toplu işleme ve akış, çok sayfalı belgelerde bellek kullanımını azaltır.  
- **.NET 6 ve .NET Core ile uyumlu mu?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5+ ve .NET 6+ üzerinde tam destek.

## “Hassas bilgileri kırp” nedir?
*Hassas bilgileri kırp* bir belgeden kişisel veya gizli verileri kalıcı olarak kaldırmak veya gizlemek anlamına gelir, böylece bir daha geri alınamaz. Buna isimler, kimlik numaraları, finansal detaylar veya bir bireyi tanımlayabilecek diğer veriler dahildir. Kırpma işlemi, GDPR, HIPAA ve CCPA gibi düzenlemelere uyumu sağlar, veri sızıntılarını önler ve belgelerin dış taraflarla güvenli bir şekilde paylaşılmasına olanak tanır.

## Neden GroupDocs.Redaction for .NET Kullanmalısınız?
GroupDocs.Redaction **nicel faydalar** sunar: 30'dan fazla giriş ve çıkış formatını destekler, tam belge yüklemesi olmadan 2 GB'a kadar belge işleyebilir ve standart bir sunucuda dakikada 10 000 açıklamayı kırpabilir. Bu sayılar, onu piyasadaki en yüksek performanslı ve çok yönlü kırpma motorlarından biri yapar.

## Önkoşullar
Başlamadan önce, aşağıdakilere sahip olduğunuzu doğrulayın:

- **GroupDocs.Redaction for .NET** (sürüm 20.7 veya daha yeni).  
- Visual Studio 2022 veya uyumlu herhangi bir IDE.  
- Temel C# bilgisi ve düzenli ifadelerle aşinalık.  

### Gerekli Kütüphaneler
- **GroupDocs.Redaction for .NET** – NuGet üzerinden kurun (Kurulum bölümüne bakın).  

### Ortam Kurulum Gereksinimleri
- .NET Framework 4.5+ **veya** .NET Core 3.1+.  
- Kaynak belgelerin bulunduğu dosya sistemine erişim.  

## Kurulum – Açıklamaları Nasıl Kaldırılır (adım 1)
Kütüphaneyi projenize aşağıdaki komutlardan herhangi birini kullanarak ekleyebilirsiniz. Öğreticiyi koddan arındırmak için kod blokları eklenmemiştir.

**.NET CLI:**  
Terminalde `dotnet add package GroupDocs.Redaction --version 20.7.*` komutunu çalıştırın.

**Package Manager Console:**  
`Install-Package GroupDocs.Redaction -Version 20.7.*` komutunu yürütün.

**NuGet Package Manager UI:**  
“GroupDocs.Redaction” aratın ve **Install** (Yükle) düğmesine tıklayın.

### Lisans Edinme
Tam işlevselliği açmak için, [GroupDocs](https://purchase.groupdocs.com/temporary-license/) adresinden bir deneme veya geçici lisans alın. Üretim kullanımı için aynı portal üzerinden kalıcı bir lisans satın alın.

## Uygulama Kılavuzu – Düzenli İfadeler Kullanarak Açıklamaları Nasıl Kaldırılır
### Genel Bakış
Bu bölüm, belirli bir desenle eşleşen **açıklamaları nasıl kaldırılır** konusunu açıklar—çalışan isimlerini, gizli notları veya herhangi bir özel işareti temizlemek için mükemmeldir.

### Adım 1: Kaynak ve Çıktı Dosya Yollarını Hazırlayın
İlk olarak, giriş belgenizin konumunu ve kırpılmış dosyanın kaydedileceği klasörü tanımlayın. Çıktı dizini mevcut olduğundan emin olun; aksi takdirde işlem başarısız olur.

*Tanım bağlantısı:* `Path.Combine`, Windows, Linux ve macOS üzerinde dizin ve dosya adlarını güvenli bir şekilde birleştiren bir .NET yardımcı programıdır.

### Adım 2: Düzenli İfade Kırpmasını Uygulayın
Sonra, regex deseninizle eşleşen açıklamaları hedefleyen bir kırpma kuralı oluşturun.

*Tanım bağlantısı:* `Redactor`, bir belgeyi yükleyen ve kırpma kurallarını uygulayan ana sınıftır.  
*Tanım bağlantısı:* `DeleteAnnotationRedaction`, içeriği bir düzenli ifade filtresiyle eşleşen açıklamaları kaldıran sınıftır.  
*Tanım bağlantısı:* `SaveOptions`, çıktının nasıl yazılacağını kontrol etmenizi sağlar—sonek ekleme, çıktı formatını seçme ve dosyayı vektör tabanlı tutmak için rasterizasyonu devre dışı bırakma.

**Doğrudan cevap:** Kaynak belgeyi `Redactor redactor = new Redactor(sourcePath);` ile yükleyin, regex'inizi kullanarak bir `DeleteAnnotationRedaction` ekleyin, ardından `redactor.Save(outputPath, new SaveOptions { Suffix = "_redacted", Rasterize = false });` çağrısını yapın. Bu tek satırlık akış, eşleşen açıklamaları kaldırır ve orijinali değiştirmeden yeni bir dosya yazar.

### Adım 3: Kaynakları Serbest Bırakın
Her zaman `redactor.Dispose()` çağırın veya örneği bir `using` bloğu içinde sararak yönetilmeyen kaynakları hızlıca serbest bırakın.  
*Tanım bağlantısı:* `Dispose`, Redactor örneği tarafından kullanılan yönetilmeyen kaynakları serbest bırakır, böylece bellek boşaltılır.

## Açıklama Kaldırma İçin Dosya Yolu Hazırlama – Excel Açıklamaları Nasıl Kaldırılır
Örnek PDF'lere odaklansa da, aynı yaklaşım Excel dosyaları (`.xlsx`) için de çalışır. Doğru yol yönetimi “dosya bulunamadı” hatalarını önler.

*Tanım bağlantısı:* `PrepareOutputDirectory`, bir klasörün varlığını kontrol eden ve eksikse oluşturan yardımcı bir yöntemdir.

Aynı yardımcı programı formatlar arasında yeniden kullanarak, Excel çalışma kitaplarından, Word belgelerinden veya PowerPoint sunumlarından **açıklamaları nasıl kaldırılır** minimal kod değişiklikleriyle yapabilirsiniz.

## Pratik Uygulamalar
1. **Veri Gizliliği Uyumu** – Kişisel tanımlayıcıları temizleyerek GDPR, HIPAA veya CCPA gereksinimlerini karşılamak için kırpmayı otomatikleştirin.  
2. **Hukuki Belge Hazırlığı** – Sözleşmeleri dış taraflarla paylaşmadan önce gizli yorumları kaldırın.  
3. **Kurumsal Veri Yönetimi** – İç raporları programlı olarak temizleyin, böylece yalnızca onaylanmış bilgiler organizasyondan çıkartılır.

## Performans Düşünceleri – Açıklamaları Verimli Bir Şekilde Nasıl Kaldırılır
- **Verimli Bellek Yönetimi:** Her dosyayı işledikten hemen sonra `Redactor` nesnelerini serbest bırakın.  
- **Toplu İşleme:** Bir klasördeki belgeler üzerinde döngü yapın ve aynı kırpma kuralını her dosyaya uygulayın; bu, kütüphaneyi tekrar tekrar açıp kapatmaya göre yükü azaltır.  
- **Optimizasyonlu Düzenli İfadeler:** Yakalama grupları kullanmayın ve geri izlemeye dayalı ağır desenlerden kaçının. Örneğin, eşleşmeyi hızlandırmak için `.*EmployeeID.*` yerine `\bEmployeeID:\s*\d{4,6}\b` tercih edin.

## Yaygın Sorunlar ve Çözümler
- **Büyük Dosyalar Takılıyor:** Belgeyi bölümlere ayırın veya `RedactorSettings` içindeki `MaxMemoryUsage` ayarını artırın.  
- **Regex Eşleşmiyor:** Desenin büyük/küçük harf duyarsızlığı için `(?i)` bayrağını içerdiğini doğrulayın veya yerleştirmeden önce çevrimiçi bir regex test aracıyla deneyin.  
- **Çıktı Dosyası Orijinali Üzerine Yazıyor:** Her zaman farklı bir çıktı yolu belirtin veya otomatik olarak “_redacted” eklemek için `SaveOptions.Suffix` kullanın.

## Sık Sorulan Sorular (Yeni)

**S: GroupDocs.Redaction Excel çalışma kitaplarındaki açıklamaları kırpabilir mi?**  
C: Evet—`.xlsx` dosyasını `Redactor` ile yükleyip bir `DeleteAnnotationRedaction` kuralı uygulayarak yorumları, notları ve diğer açıklama türlerini kaldırabilirsiniz.

**S: Regex desenlerini büyük/küçük harf duyarsız nasıl yaparım?**  
C: Desenin önüne `(?i)` ekleyin veya `DeleteAnnotationRedaction` oluştururken `RegexOptions.IgnoreCase` bayrağını kullanın.

**S: Çıktı dosya adını özelleştirmek mümkün mü?**  
C: Kesinlikle. Oluşturulan dosya adına metin eklemek için `SaveOptions.Prefix` veya `SaveOptions.Suffix` ayarlayın.

**S: Kırpma işleminden sonra orijinal belge ne olur?**  
C: Kaynak dosya dokunulmaz kalır; kırpılmış sürüm `SaveOptions` içinde belirttiğiniz yola kaydedilir.

**S: Kütüphane çok büyük PDF'ler için akış desteği sunuyor mu?**  
C: Evet—GroupDocs.Redaction, sayfaları sırayla işleyen bir akış modunda çalışabilir, böylece bellek tüketimini büyük ölçüde azaltır.

## SSS Bölümü
1. **Büyük belgeleri verimli bir şekilde nasıl yönetirim?**  
   - Mümkünse belgeleri daha küçük bölümlere ayırarak işleyin ve düzenli ifadelerin performans için optimize edildiğinden emin olun.  
2. **GroupDocs.Redaction'ı Excel dışındaki diğer dosya formatlarıyla kullanabilir miyim?**  
   - Evet, PDF, Word ve daha fazlası dahil çeşitli formatları destekler.  
3. **Kırpma işleminden sonra orijinal belge ne olur?**  
   - Orijinal belge, üzerine kaydedilmediği sürece değişmez; değişiklikleri her zaman yeni bir dosyaya veya kopyaya kaydedin.  
4. **GroupDocs.Redaction ile çıktı dosya adını özelleştirmek mümkün mü?**  
   - Evet, `SaveOptions`'ı özelleştirilmiş sonekler veya ön ekler ekleyecek şekilde değiştirin.  
5. **Regex desenlerinin büyük/küçük harf duyarsız olduğundan nasıl emin olurum?**  
   - Desenlerde `(i)` gibi değiştiriciler kullanarak büyük/küçük harf duyarsızlığını sağlayın.

## Kaynaklar
- [Dokümantasyon](https://docs.groupdocs.com/redaction/net/)
- [API Referansı](https://reference.groupdocs.com/redaction/net)
- [GroupDocs.Redaction'ı İndir](https://releases.groupdocs.com/redaction/net/)
- [Ücretsiz Destek Forumu](https://forum.groupdocs.com/c/redaction/33)
- [Geçici Lisans Talebi](https://purchase.groupdocs.com/temporary-license/)

Bu kılavuzu izleyerek, artık GroupDocs.Redaction for .NET kullanarak herhangi bir desteklenen belge türünden **hassas bilgileri kırp** ve **açıklamaları nasıl kaldırılır** güçlü bir yönteme sahipsiniz. Adımları uygulayın, birkaç örnek dosya ile test edin ve mantığı daha büyük belge‑işleme hattınıza entegre ederek maksimum güvenlik sağlayın.

---

**Son Güncelleme:** 2026-06-01  
**Test Edilen Versiyon:** GroupDocs.Redaction 20.7 for .NET  
**Yazar:** GroupDocs  

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

```csharp
string sourceFile = @"YOUR_DOCUMENT_DIRECTORY\AnnotatedDocument.xlsx";
var saveOptions = new SaveOptions { AddSuffix = true, RasterizeToPDF = false };
```

```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // This regex matches the phrase "John Doe" in a case-insensitive manner.
    redactor.Apply(new DeleteAnnotationRedaction("(?im:John Doe)"));
    
    // Save changes to a new file with a suffix indicating it's been redacted.
    var outputFile = redactor.Save(saveOptions);
}
```

```csharp
using System.IO;

public class Utils
{
    public static string PrepareOutputDirectory(string fileName)
    {
        var documentDirectory = Path.Combine(Directory.GetCurrentDirectory(), "YOUR_DOCUMENT_DIRECTORY");
        var filePath = Path.Combine(documentDirectory, fileName);

        Directory.CreateDirectory(documentDirectory);
        return filePath;
    }
}
```

## İlgili Öğreticiler

- [GroupDocs.Redaction .NET Kullanarak Belgeleri Yükleme ve Kırpma: Tam Kılavuz](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [GroupDocs.Redaction for .NET ile Belgeleri Kırp ve Kaydet: Tam Kılavuz](/redaction/net/document-saving/redact-save-documents-groupdocs-redaction-net/)
- [GroupDocs.Redaction Kullanarak .NET Belgelerinde Tam İfadeleri Kırp](/redaction/net/text-redaction/guide-redact-exact-phrases-groupdocs-redaction-dotnet/)