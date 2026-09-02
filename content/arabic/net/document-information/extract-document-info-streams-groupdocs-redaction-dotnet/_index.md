---
date: '2026-06-11'
description: تعلم كيفية استخراج البيانات الوصفية من تدفقات المستندات باستخدام GroupDocs.Redaction
  لـ .NET، مع تغطية الإعداد، أمثلة الشيفرة، والتطبيقات العملية.
keywords:
- how to extract metadata
- extract document metadata
- extract pdf metadata
- retrieve document size
- prepare output directory
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to extract metadata from document streams using GroupDocs.Redaction
    for .NET, covering setup, code examples, and practical applications.
  headline: How to Extract Metadata from Document Streams Using GroupDocs.Redaction
    .NET
  type: TechArticle
- description: Learn how to extract metadata from document streams using GroupDocs.Redaction
    for .NET, covering setup, code examples, and practical applications.
  name: How to Extract Metadata from Document Streams Using GroupDocs.Redaction .NET
  steps:
  - name: Prepare the source file path
    text: First, ensure the source file exists and that the output folder is ready.
      The helper method below checks the output directory and creates it if needed.
      *Why?* This guarantees a valid path for subsequent file operations and prevents
      `DirectoryNotFoundException`.
  - name: Open the document stream
    text: Using `File.OpenRead()` opens the file as a **read‑only stream**, which
      keeps memory usage low even for gigabyte‑size files. *Why?* Streams enable on‑the‑fly
      processing, allowing you to work with portions of the file rather than the whole
      document.
  - name: Initialise the Redactor with the document stream
    text: '`Redactor` is the primary API object that gives you access to document‑level
      operations, including metadata extraction. `Redactor` represents a single document
      loaded from a stream and exposes methods such as `GetDocumentInfo()` for quick
      property retrieval. *Why?* Instantiating `Redactor` with a st'
  - name: Retrieve document metadata
    text: Calling `GetDocumentInfo()` returns a `DocumentInfo` object that holds the
      file format, page count, and file size. `GetDocumentInfo()` extracts core properties
      (format, page count, size) in a single call, eliminating the need for separate
      parsers. *Why?* This step consolidates all essential metadata
  type: HowTo
- questions:
  - answer: It enables fast, memory‑efficient retrieval of document properties for
      indexing, compliance checks, and automated routing without opening the full
      file.
    question: What is the primary use case for GroupDocs.Redaction’s metadata extraction?
  - answer: Yes, provide the password when constructing the `Redactor` object; the
      API will decrypt the stream internally.
    question: Can I extract metadata from password‑protected files?
  - answer: Absolutely – GroupDocs.Redaction handles over 30 formats, including PDF,
      DOCX, XLSX, PPTX, and common image types.
    question: Does the library support non‑PDF formats like DOCX or XLSX?
  - answer: Streams allow processing of files up to **2 GB** while keeping memory
      consumption under **50 MB**, thanks to on‑the‑fly reading.
    question: How large a document can I process with streams?
  - answer: Visit the [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33)
      for community support, or consult the official documentation for troubleshooting
      tips.
    question: Where can I get help if I run into issues?
  type: FAQPage
title: كيفية استخراج البيانات الوصفية من تدفقات المستندات باستخدام GroupDocs.Redaction
  .NET
type: docs
url: /ar/net/document-information/extract-document-info-streams-groupdocs-redaction-dotnet/
weight: 1
---

# كيفية استخراج البيانات الوصفية من تدفقات المستندات باستخدام GroupDocs.Redaction .NET

هل سئمت من استخراج معلومات المستند يدويًا أو التعامل مع ملفات كبيرة تبطئ سير عملك؟ **كيفية استخراج البيانات الوصفية** بسرعة هو تحدٍ شائع، وتوفر مكتبة GroupDocs.Redaction لـ .NET طريقة سريعة وفعّالة في الذاكرة لاسترجاع تفاصيل المستند مباشرةً من التدفقات. في هذا الدرس، ستتعلم كيفية إعداد المكتبة، واستخلاص نوع الملف، عدد الصفحات، والحجم من تدفق، وتحضير مجلد إخراج للمعالجة اللاحقة.

## إجابات سريعة
- **ماذا يعني “extract metadata”؟** يعني قراءة الخصائص مثل نوع الملف، عدد الصفحات، والحجم دون فتح المستند بالكامل في الذاكرة.  
- **أي مكتبة تتعامل مع ذلك؟** توفر GroupDocs.Redaction لـ .NET واجهة برمجة تطبيقات أصلية لاستخراج البيانات الوصفية بناءً على التدفق.  
- **هل أحتاج إلى ترخيص؟** نسخة تجريبية مجانية تعمل للتطوير؛ يتطلب الترخيص التجاري للإنتاج.  
- **هل يمكنني معالجة ملفات PDF أكبر من 1 GB؟** نعم – تسمح التدفقات بمعالجة ملفات تصل إلى 2 GB دون تحميل الملف بالكامل.  
- **ما إصدارات .NET المدعومة؟** .NET Framework 4.5+، .NET Core 3.1+، .NET 5+، و .NET 6+.

## ما هو استخراج البيانات الوصفية من التدفقات؟
استخراج البيانات الوصفية من التدفقات هو عملية قراءة خصائص المستند مباشرةً من كائن `Stream`، متجنّبًا تحميل الملف بالكامل وبالتالي توفير الذاكرة ووقت وحدة المعالجة المركزية. هذه التقنية مثالية للمعالجة الدفعية أو الخدمات السحابية حيث الموارد محدودة.

## لماذا نستخدم GroupDocs.Redaction لاستخراج البيانات الوصفية؟
يدعم GroupDocs.Redaction **أكثر من 30 تنسيق ملف** (بما في ذلك PDF، DOCX، XLSX، PPTX، وأنواع الصور) ويمكنه معالجة مستندات يصل حجمها إلى **2 GB** مع الحفاظ على استهلاك الذاكرة أقل من **50 MB**. توفر واجهة برمجة تطبيقات `Redactor` استدعاءً واحدًا لاسترجاع جميع معلومات المستند الرئيسية، مما يلغي الحاجة إلى عدة محللات.

## المتطلبات المسبقة
- **GroupDocs.Redaction for .NET** (الإصدار الأحدث)  
- **.NET Framework** 4.5+ **أو** **.NET Core/5+/6+**  
- معرفة أساسية بـ C# وإلمام بعمليات إدخال/إخراج الملفات  
- Visual Studio 2019 أو أحدث

## كيف أقوم بإعداد GroupDocs.Redaction لـ .NET؟
لبدء استخدام GroupDocs.Redaction، تحتاج أولاً إلى إضافة المكتبة إلى مشروعك. يمكن القيام بذلك عبر .NET CLI، أو مدير الحزم في Visual Studio، أو واجهة NuGet. اختر النهج الذي يناسب سير عملك؛ فالـ CLI مثالي للبناء القابل للبرمجة، بينما توفر الواجهة الرسومية طريقة لتصفح الإصدارات والاعتمادات.

**.NET CLI**
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**
```powershell
Install-Package GroupDocs.Redaction
```

**واجهة مدير حزم NuGet:**
- افتح مدير حزم NuGet في Visual Studio.  
- ابحث عن **"GroupDocs.Redaction"** وقم بتثبيت الإصدار الأحدث.

### خطوات الحصول على الترخيص
1. **نسخة تجريبية مجانية:** قم بتحميل ترخيص تجريبي لاستكشاف جميع الميزات دون قيود.  
2. **ترخيص مؤقت:** اطلب ترخيصًا مؤقتًا من [GroupDocs](https://purchase.groupdocs.com/temporary-license/) للاختبار الموسع.  
3. **شراء:** عندما تكون جاهزًا للإنتاج، اشترِ ترخيصًا تجاريًا.  

لمزيد من المعلومات، زر [موقع GroupDocs](https://purchase.groupdocs.com/temporary-license/).

### التهيئة الأساسية والإعداد
فئة `Redactor` هي نقطة الدخول لجميع العمليات، بما في ذلك استخراج البيانات الوصفية.

`Redactor` هي الفئة الأساسية التي تمثل نسخة من المستند وتوفر طرقًا للتعتيم، استرجاع المعلومات، ومعالجة الملفات. بمجرد التثبيت، يمكنك إنشاء كائن `Redactor` كما هو موضح أدناه:

```csharp
using (Redactor redactor = new Redactor("your-document-path"))
{
    // Use the redactor here
}
```

الآن بعد أن أصبحت المكتبة جاهزة، دعنا نتعمق في تفاصيل التنفيذ.

## كيفية استخراج البيانات الوصفية من تدفق مستند؟
حمّل المستند كـ **تدفق للقراءة فقط**، قم بتهيئة `Redactor`، واستدعِ `GetDocumentInfo()` لاسترجاع البيانات الوصفية في خطوة واحدة. هذه الطريقة تتجنب تحميل الملف بالكامل في الذاكرة، وهو أمر حاسم للملفات الكبيرة PDF أو مستندات Office ذات مئات الصفحات.

**الإجابة المباشرة:** افتح الملف باستخدام `File.OpenRead()`، مرّر التدفق إلى `new Redactor(stream)`، ثم استدعِ `redactor.GetDocumentInfo()` – تُعيد الطريقة كائنًا يحتوي على نوع الملف، عدد الصفحات، والحجم في ثلاث أسطر من الشيفرة فقط.

### الخطوة 1: تحضير مسار ملف المصدر
أولاً، تأكد من وجود ملف المصدر وأن مجلد الإخراج جاهز. الطريقة المساعدة أدناه تتحقق من دليل الإخراج وتنشئه إذا لزم الأمر.

```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

*لماذا؟* يضمن ذلك مسارًا صالحًا للعمليات اللاحقة على الملفات ويمنع حدوث `DirectoryNotFoundException`.

### الخطوة 2: فتح تدفق المستند
استخدام `File.OpenRead()` يفتح الملف كـ **تدفق للقراءة فقط**، مما يحافظ على انخفاض استهلاك الذاكرة حتى للملفات بحجم الجيجابايت.

```csharp
using (Stream documentStream = File.OpenRead(sourceFile))
{
    // Proceed to initialize Redactor
}
```

*لماذا؟* تمكّن التدفقات المعالجة الفورية، مما يسمح لك بالعمل على أجزاء من الملف بدلاً من المستند بالكامل.

### الخطوة 3: تهيئة Redactor باستخدام تدفق المستند
`Redactor` هو كائن API الأساسي الذي يمنحك الوصول إلى عمليات مستوى المستند، بما في ذلك استخراج البيانات الوصفية.

`Redactor` يمثل مستندًا واحدًا تم تحميله من تدفق ويكشف عن طرق مثل `GetDocumentInfo()` لاسترجاع الخصائص بسرعة.  

```csharp
using (Redactor redactor = new Redactor(documentStream))
{
    // Extract document info next
}
```

*لماذا؟* إنشاء كائن `Redactor` باستخدام تدفق يربط الكائن بالملف الأساسي دون تحميله بالكامل.

### الخطوة 4: استرجاع بيانات المستند الوصفية
استدعاء `GetDocumentInfo()` يُعيد كائن `DocumentInfo` يحتوي على تنسيق الملف، عدد الصفحات، وحجم الملف.

`GetDocumentInfo()` يستخرج الخصائص الأساسية (التنسيق، عدد الصفحات، الحجم) في استدعاء واحد، مما يلغي الحاجة إلى محللات منفصلة.  

```csharp
IDocumentInfo info = redactor.GetDocumentInfo();
string fileInfo = $"\nFile type: {info.FileType}\nNumber of pages: {info.PageCount}\nDocument size: {info.Size} bytes";
Console.WriteLine(fileInfo);
```

*لماذا؟* تجمع هذه الخطوة جميع البيانات الوصفية الأساسية، مما يجعل من السهل تسجيلها، تصفيتها، أو توجيه المستندات بناءً على خصائصها.

## كيفية تحضير دليل الإخراج للملفات المعالجة؟
قبل كتابة أي ملفات معالجة، تأكد من وجود مجلد الوجهة وأنه قابل للكتابة. من خلال التحقق برمجيًا من المسار وإنشائه إذا كان مفقودًا، تتجنب استثناءات التشغيل الشائعة مثل `DirectoryNotFoundException` أو أخطاء الأذونات. هذه الخطوة البسيطة تجعل الشيفرة قابلة للنقل عبر البيئات، سواءً كانت تعمل محليًا، على خادم، أو داخل حاوية.

**الإجابة المباشرة:** استخدم `Directory.Exists()` للتحقق من وجود المجلد و`Directory.CreateDirectory()` لإنشائه إذا لم يكن موجودًا – يضمن هذا الفحص ذو السطر الواحد مسارًا صالحًا قبل أي عملية كتابة.

### تنفيذ طريقة مساعدة
الطريقة أدناه تُجسد منطق الفحص والإنشاء، وتعيد المسار المُتحقق لاستخدامه لاحقًا.

```csharp
public static class Utils
{
    public static string PrepareOutputDirectory(string sampleDocPath)
    {
        string directory = Path.GetDirectoryName(sampleDocPath);
        
        if (!Directory.Exists(directory))
        {
            Directory.CreateDirectory(directory);
        }
        
        return Path.Combine(directory, "SAMPLE_DOCX.docx");
    }
}
```

*لماذا؟* يساهم تجميع هذا المنطق في تقليل التكرار وجعل قاعدة الشيفرة أسهل في الصيانة.

## المشكلات الشائعة والحلول
- **أخطاء الأذونات:** تأكد من أن التطبيق يعمل تحت حساب يملك صلاحية كتابة على المجلد المستهدف.  
- **مسارات غير صالحة:** تحقق مرة أخرى من فواصل المسار (`\\` على Windows، `/` على Linux/macOS) لتجنب `DirectoryNotFoundException`.  
- **معالجة الملفات الكبيرة:** حرّر التدفقات فورًا (`using` statements) لتحرير مقابض نظام التشغيل ومنع التسرب.

## التطبيقات العملية
1. **استيعاب المستندات تلقائيًا:** استخراج البيانات الوصفية عند التحميل، ثم تخزينها في قاعدة بيانات للبحث السريع وتقرير الامتثال.  
2. **التدقيق القانوني والامتثال:** سحب عدد الصفحات وأنواع الملفات للتحقق من أن المستندات تفي بالمعايير التنظيمية قبل الأرشفة.  
3. **إدارة محتوى المؤسسة:** استخدام البيانات الوصفية لتصنيف الملفات تلقائيًا إلى مجلدات، مما يحسن التنظيم وسرعة الاسترجاع.

## اعتبارات الأداء
- **إدارة الذاكرة:** احرص دائمًا على تغليف التدفقات بكتل `using` حتى يتم تحريرها تلقائيًا.  
- **المعالجة الدفعية:** عالج المستندات في مجموعات من 10‑20 لتحقيق توازن بين الإنتاجية واستهلاك الذاكرة، خاصةً على الخوادم ذات الموارد المحدودة.  
- **التوازي:** استخدم `Parallel.ForEach` للملفات المستقلة، لكن راقب وحدة المعالجة المركزية وإدخال/إخراج البيانات لتجنب التنافس.

## الخلاصة
أصبح لديك الآن دليل كامل وجاهز للإنتاج حول **كيفية استخراج البيانات الوصفية** من تدفقات المستندات باستخدام GroupDocs.Redaction لـ .NET. باتباع الخطوات أعلاه، يمكنك استرجاع نوع الملف، عدد الصفحات، والحجم بكفاءة مع الحفاظ على استهلاك منخفض للذاكرة ومعالجة الملفات الكبيرة بسلاسة.

**الخطوات التالية**
- راجع مرجع API الكامل في [التوثيق](https://docs.groupdocs.com/redaction/net/).  
- تعمق أكثر في [توثيق GroupDocs Redaction .NET](https://docs.groupdocs.com/redaction/net/) لاستكشاف ميزات التعتيم، العلامات المائية، و OCR.  
- جرّب صيغ ملفات مختلفة (PDF، DOCX، XLSX) لترى كيف تختلف البيانات الوصفية بين الأنواع.  
- دمج البيانات الوصفية المستخرجة في نظام إدارة المستندات أو البحث الحالي لديك.

## الأسئلة المتكررة

**س: ما هو الاستخدام الأساسي لاستخراج البيانات الوصفية في GroupDocs.Redaction؟**  
ج: يتيح استرجاعًا سريعًا وفعّالًا في الذاكرة لخصائص المستند للفهرسة، فحص الامتثال، والتوجيه الآلي دون فتح الملف بالكامل.

**س: هل يمكنني استخراج البيانات الوصفية من الملفات المحمية بكلمة مرور؟**  
ج: نعم، قدم كلمة المرور عند إنشاء كائن `Redactor`؛ ستقوم الواجهة بفك تشفير التدفق داخليًا.

**س: هل تدعم المكتبة صيغًا غير PDF مثل DOCX أو XLSX؟**  
ج: بالتأكيد – يدعم GroupDocs.Redaction أكثر من 30 تنسيقًا، بما في ذلك PDF، DOCX، XLSX، PPTX، وأنواع الصور الشائعة.

**س: ما هو الحد الأقصى لحجم المستند الذي يمكنني معالجته باستخدام التدفقات؟**  
ج: تسمح التدفقات بمعالجة ملفات يصل حجمها إلى **2 GB** مع الحفاظ على استهلاك الذاكرة أقل من **50 MB**، بفضل القراءة الفورية.

**س: أين يمكنني الحصول على المساعدة إذا واجهت مشاكل؟**  
ج: زر [منتدى GroupDocs](https://forum.groupdocs.com/c/redaction/33) للحصول على دعم المجتمع، أو راجع التوثيق الرسمي للحصول على نصائح استكشاف الأخطاء.

---

**آخر تحديث:** 2026-06-11  
**تم الاختبار مع:** GroupDocs.Redaction 23.12 for .NET  
**المؤلف:** GroupDocs  

**الموارد**  
- **التوثيق:** [GroupDocs Redaction .NET Documentation](https://docs.groupdocs.com/redaction/net/)  
- **مرجع API:** [GroupDocs Redaction API Reference](https://reference.groupdocs.com/redaction/net)  
- **تحميل:** [Latest GroupDocs Releases](https://releases.groupdocs.com/redaction/net)

## دروس ذات صلة

- [إتقان استرجاع بيانات المستند الوصفية باستخدام GroupDocs.Redaction .NET API](/redaction/net/document-information/groupdocs-redaction-net-document-metadata-retrieval/)
- [كيفية تعتيم بيانات المستند الوصفية باستخدام GroupDocs.Redaction لـ .NET - دليل شامل](/redaction/net/metadata-redaction/redact-metadata-groupdocs-redaction-net/)
- [تعتيم المستند بأمان في .NET باستخدام التدفقات: دليل لـ GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)