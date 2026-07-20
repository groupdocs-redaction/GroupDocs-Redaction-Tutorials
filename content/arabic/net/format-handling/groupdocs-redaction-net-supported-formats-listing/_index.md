---
date: '2026-07-20'
description: تعلم كيفية سرد الصيغ باستخدام GroupDocs.Redaction .NET، ودمج الميزة في
  سير عمل المستندات الخاص بك، وتحسين الأداء.
keywords:
- how to list formats
- GroupDocs.Redaction supported formats
- .NET document processing
lastmod: '2026-07-20'
og_description: اكتشف كيفية سرد الصيغ باستخدام GroupDocs.Redaction .NET، شاهد دليل
  خطوة بخطوة، واحصل على نصائح لتحقيق الأداء الأمثل في تطبيقات .NET الخاصة بك.
og_image_alt: Guide showing how to list supported file formats with GroupDocs.Redaction
  in a .NET project
og_title: كيفية سرد الصيغ باستخدام GroupDocs.Redaction .NET
schemas:
- author: GroupDocs
  dateModified: '2026-07-20'
  description: Learn how to list formats using GroupDocs.Redaction .NET, integrate
    the feature into your document workflow, and improve performance.
  headline: How to List Formats with GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to list formats using GroupDocs.Redaction .NET, integrate
    the feature into your document workflow, and improve performance.
  name: How to List Formats with GroupDocs.Redaction .NET
  steps:
  - name: '**Document Management Systems** – Validate uploads against the supported
      list to prevent processing failures.'
    text: '**Document Management Systems** – Validate uploads against the supported
      list to prevent processing failures.'
  - name: '**Content Security** – Apply redaction rules only to file types that the
      engine can safely modify.'
    text: '**Content Security** – Apply redaction rules only to file types that the
      engine can safely modify.'
  - name: '**Batch Processing Pipelines** – Filter large file batches before invoking
      redaction, saving CPU and memory.'
    text: '**Batch Processing Pipelines** – Filter large file batches before invoking
      redaction, saving CPU and memory.'
  - name: '**How do I install GroupDocs.Redaction for .NET?**'
    text: '**How do I install GroupDocs.Redaction for .NET?**'
  - name: '**What are some common issues when retrieving supported formats?**'
    text: '**What are some common issues when retrieving supported formats?**'
  - name: '**Can I use this feature with non‑.NET applications?**'
    text: '**Can I use this feature with non‑.NET applications?**'
  - name: '**How can I optimise performance when using GroupDocs.Redaction?**'
    text: '**How can I optimise performance when using GroupDocs.Redaction?**'
  - name: '**What file types does GroupDocs.Redaction support?**'
    text: '**What file types does GroupDocs.Redaction support?**'
  type: HowTo
- questions:
  - answer: Yes, `FileType.GetSupportedFileFormats()` is static and does not require
      a `Redactor` object.
    question: Can I retrieve the format list without initializing a Redactor instance?
  - answer: The method returns all formats that the library can both read and write;
      each `FileType` includes a `CanRead` and `CanWrite` flag.
    question: Does the list include both input and output formats?
  - answer: GroupDocs releases format updates with each library version; checking
      the list at runtime ensures you always have the latest set.
    question: How often is the supported format list updated?
  - answer: Yes, filter the collection where `format.Extension == ".pdf"` or where
      `format.Name.Contains("PDF")`.
    question: Is there a way to filter only PDF‑compatible formats?
  - answer: The method requires .NET Core 3.1 or later; earlier runtimes are not supported.
    question: Will this approach work on .NET Core 2.1?
  type: FAQPage
tags:
- how to list formats
- GroupDocs.Redaction
- .NET file handling
title: كيفية سرد الصيغ باستخدام GroupDocs.Redaction .NET
type: docs
url: /ar/net/format-handling/groupdocs-redaction-net-supported-formats-listing/
weight: 1
---

# كيفية سرد الصيغ باستخدام GroupDocs.Redaction .NET

إدارة مجموعة واسعة من أنواع المستندات هي حقيقة يومية للمطورين الذين يبنون تطبيقات تركز على المستندات. في هذا البرنامج التعليمي ستتعلم **كيفية سرد الصيغ** التي يمكن لـ GroupDocs.Redaction .NET التعامل معها، حتى تتمكن من التحقق من صحة الملفات قبل المعالجة، وتقديم خيارات دقيقة للمستخدمين، والحفاظ على كفاءة سير العمل الخاص بك.

## المقدمة

تبدأ معالجة المستندات بكفاءة بمعرفة الأنواع الدقيقة للملفات التي تدعمها مكتبتك. توفر GroupDocs.Redaction طريقة مدمجة لاسترجاع هذه المعلومات، مما يتيح لك بناء عناصر واجهة مستخدم ديناميكية، وتطبيق قواعد التحقق، وتجنب الأخطاء أثناء التشغيل. أدناه ستجد كل ما تحتاجه للبدء، من التثبيت إلى مقتطفات الشيفرة العملية ونصائح الأداء.

### إجابات سريعة
- **ماذا يعني “كيفية سرد الصيغ”؟** يشير إلى استرجاع مجموعة امتدادات الملفات التي يمكن لـ GroupDocs.Redaction معالجتها.  
- **هل أحتاج إلى ترخيص؟** نعم، يلزم وجود ترخيص صالح لـ GroupDocs.Redaction للاستخدام في بيئة الإنتاج.  
- **ما إصدارات .NET المدعومة؟** .NET Framework 4.6+، .NET Core 3.1+، .NET 5/6/7.  
- **كم عدد الصيغ المتاحة؟** أكثر من 30 صيغة إدخال وإخراج مدعومة مباشرةً.  
- **هل هناك أي إعدادات خاصة مطلوبة؟** لا يلزم أي إعداد إضافي بخلاف تهيئة المكتبة القياسية.

## ما هو “كيفية سرد الصيغ”

يتضمن ذلك استدعاء API الخاص بـ FileType في المكتبة للحصول على مجموعة حيث يحتوي كل عنصر على امتداد الملف واسم قابل للقراءة من قبل الإنسان. يمكن للمطورين بعد ذلك تكرار هذه المجموعة لبناء قواعد التحقق، تعبئة قوائم منسدلة في الواجهة، أو تسجيل الأنواع المدعومة، مما يضمن معالجة المستندات المتوافقة فقط.

## لماذا نُسرد الصيغ باستخدام GroupDocs.Redaction؟

تدعم GroupDocs.Redaction **أكثر من 30** نوع ملف مميز — بما في ذلك PDF و DOCX و PPTX وصيغ الصور — مما يتيح لك التعامل مع معظم مستندات المؤسسات دون الحاجة إلى محولات طرف ثالث. من خلال سرد هذه الصيغ برمجياً، تلغي التخمين، تقلل من عدد تذاكر الدعم، وتضمن دخول الملفات المتوافقة فقط إلى خط أنابيب المعالجة الخاص بك.

## المتطلبات المسبقة

- **GroupDocs.Redaction for .NET** – قم بتحميل أحدث حزمة من الموقع الرسمي.  
- **.NET Framework أو .NET Core** – متوافق مع بيئة التطوير الخاصة بك.  
- **Visual Studio** (أو أي بيئة تطوير متوافقة مع C#).  
- إلمام أساسي بصياغة C#.

## إعداد GroupDocs.Redaction لـ .NET

### .NET CLI
`dotnet add package GroupDocs.Redaction`

### مدير الحزم
`Install-Package GroupDocs.Redaction`

### واجهة مدير الحزم NuGet
- ابحث عن **“GroupDocs.Redaction”** وقم بتثبيت أحدث نسخة.

### الحصول على الترخيص
توفر GroupDocs نسخة تجريبية مجانية، ترخيصًا مؤقتًا للتقييم، أو خيارات شراء كاملة. زر موقع GroupDocs للحصول على ملف الترخيص المناسب.

### التهيئة الأساسية والإعداد
بعد إضافة الحزمة، استورد مساحة الاسم وأنشئ كائن `Redactor`:

```csharp
using GroupDocs.Redaction;

// Initialize with a license file (replace path as needed)
Redactor redactor = new Redactor("path/to/license/file.lic");
```

## دليل التنفيذ

### كيف يمكنني سرد الصيغ باستخدام GroupDocs.Redaction .NET؟
حمِّل المكتبة، استدعِ المساعد الساكن، ورتب النتائج — ستحصل على مجموعة جاهزة للاستخدام في سطرين فقط من الشيفرة. استخدم `FileType.GetSupportedFileFormats()` لاسترجاع `IEnumerable<FileType>` التي تشمل امتداد كل صيغة واسم العرض، ثم رتبها حسب الامتداد للحصول على قائمة واجهة مستخدم نظيفة.

### استرجاع صيغ الملفات المدعومة

#### نظرة عامة
الهدف هو الحصول على قائمة بأنواع الملفات التي يمكن لـ GroupDocs.Redaction معالجتها، لتسهيل دمجها في منطق التحقق، القوائم المنسدلة في الواجهة، أو آليات التسجيل.

#### تنفيذ خطوة بخطوة

**1. Retrieve Supported File Types**  
`FileType.GetSupportedFileFormats()` تُعيد كل صيغة تتعرف عليها المكتبة. الطريقة جزء من الفئة `GroupDocs.Redaction.FileType`، التي تُغلف بيانات التعريف مثل امتداد الملف والاسم الودي.

**2. Display Supported File Types**  
قم بتكرار المجموعة واطبع كل امتداد وصفي للصيغة. مثال على الشيفرة المضمنة:

```csharp
var formats = FileType.GetSupportedFileFormats()
                      .OrderBy(f => f.Extension);

foreach (var format in formats)
{
    Console.WriteLine($"{format.Extension} – {format.Name}");
}
```

المقتطف يطبع قائمة مرتبة بشكل أنيق مثل “.pdf – Portable Document Format”، مما يجعلها مثالية لتعبئة عناصر الواجهة.

### نصائح استكشاف الأخطاء وإصلاحها
- **Missing Package** – تحقق من مرجع حزمة NuGet وأعد استعادة الحزم إذا لزم الأمر.  
- **Incorrect License Path** – تأكد من نسخ ملف الترخيص إلى دليل الإخراج أو قدم مسارًا مطلقًا.  
- **Unsupported Extension** – إذا لم تُدرج صيغة ما، تأكد من أنك تستخدم أحدث إصدار من المكتبة؛ الإصدارات الأحدث تضيف صيغًا إضافية.

## تطبيقات عملية
فهم صيغ الملفات المدعومة يفتح عدة سيناريوهات واقعية:

1. **أنظمة إدارة المستندات** – تحقق من صحة التحميلات مقابل القائمة المدعومة لتجنب فشل المعالجة.  
2. **أمان المحتوى** – طبق قواعد التمويه فقط على أنواع الملفات التي يمكن للمحرك تعديلها بأمان.  
3. **خطوط أنابيب المعالجة الدفعية** – صَفّ دفعات الملفات الكبيرة قبل استدعاء التمويه، لتوفير CPU والذاكرة.

## اعتبارات الأداء
- **Memory Footprint** – سرد الصيغ عملية خفيفة الوزن؛ لا يتم تحميل أي مستند إلى الذاكرة.  
- **Batch Operations** – عند معالجة مئات الملفات، استرجع قائمة الصيغ مرة واحدة وأعد استخدامها لتجنب الاستدعاءات المتكررة.  
- **Thread Safety** – `FileType.GetSupportedFileFormats()` آمنة للاستخدام عبر الخيوط ويمكن استدعاؤها من مهام متوازية دون مزامنة.

## الخلاصة
أصبح لديك الآن نهج كامل وجاهز للإنتاج **لكيفية سرد الصيغ** باستخدام GroupDocs.Redaction .NET. من خلال دمج هذه الميزة، يمكنك تحسين التحقق، تعزيز تجربة المستخدم، والحفاظ على خطوط أنابيب المستندات قوية.

### الخطوات التالية
- استكشف API الخاص بـ `Redactor` لتطبيق قواعد التمويه بناءً على نوع الملف.  
- اجمع قائمة الصيغ مع قائمة منسدلة في الواجهة لتسهيل اختيار الملفات.  
- راجع دليل الأداء لتحسين وظائف الدُفعات الكبيرة.

## الأسئلة المتكررة

**س: هل يمكنني استرجاع قائمة الصيغ دون تهيئة كائن Redactor؟**  
ج: نعم، `FileType.GetSupportedFileFormats()` ثابت ولا يتطلب كائن `Redactor`.

**س: هل تشمل القائمة صيغ الإدخال والإخراج معًا؟**  
ج: تُعيد الطريقة جميع الصيغ التي يمكن للمكتبة قراءتها وكتابتها؛ كل `FileType` يحتوي على علمي `CanRead` و `CanWrite`.

**س: كم مرة يتم تحديث قائمة الصيغ المدعومة؟**  
ج: تصدر GroupDocs تحديثات الصيغ مع كل نسخة من المكتبة؛ فحص القائمة أثناء التشغيل يضمن حصولك دائمًا على أحدث مجموعة.

**س: هل هناك طريقة لتصفية الصيغ المتوافقة مع PDF فقط؟**  
ج: نعم، صَفّ المجموعة حيث `format.Extension == ".pdf"` أو حيث `format.Name.Contains("PDF")`.

**س: هل سيعمل هذا النهج على .NET Core 2.1؟**  
ج: الطريقة تتطلب .NET Core 3.1 أو أحدث؛ الإصدارات الأقدم غير مدعومة.

## قسم الأسئلة المتكررة
1. **كيف أقوم بتثبيت GroupDocs.Redaction لـ .NET؟**  
   استخدم أمر CLI `dotnet add package GroupDocs.Redaction` أو قم بالتثبيت عبر واجهة مدير الحزم NuGet.  
2. **ما هي بعض المشكلات الشائعة عند استرجاع الصيغ المدعومة؟**  
   تأكد من استعادة جميع الاعتمادات وأنك تستورد مساحة الاسم الصحيحة (`GroupDocs.Redaction`).  
3. **هل يمكنني استخدام هذه الميزة مع تطبيقات غير .NET؟**  
   يركز هذا الدرس على .NET، لكن GroupDocs توفر واجهات برمجة تطبيقات مماثلة للغة Java و Python وغيرها.  
4. **كيف يمكنني تحسين الأداء عند استخدام GroupDocs.Redaction؟**  
   أعد استخدام قائمة الصيغ، تجنب تحميل المستندات بالكامل عند التحقق من التوافق فقط، وراقب استهلاك الذاكرة أثناء عمليات الدُفعات.  
5. **ما هي صيغ الملفات التي يدعمها GroupDocs.Redaction؟**  
   تدعم المكتبة أكثر من 30 صيغة، بما في ذلك PDF و DOCX و PPTX و XLSX و BMP و PNG و JPEG وغيرها. استخدم `FileType.GetSupportedFileFormats()` لعرض القائمة الكاملة.

## الموارد
- [التوثيق](https://docs.groupdocs.com/redaction/net/)
- [مرجع API](https://reference.groupdocs.com/redaction/net)
- [تحميل GroupDocs.Redaction](https://releases.groupdocs.com/redaction/net/)
- [منتدى الدعم المجاني](https://forum.groupdocs.com/c/redaction/33)
- [ترخيص مؤقت](https://purchase.groupdocs.com/temporary-license/)

---

**آخر تحديث:** 2026-07-20  
**تم الاختبار مع:** GroupDocs.Redaction 4.2.0 for .NET  
**المؤلف:** GroupDocs  

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

```csharp
using GroupDocs.Redaction;
// Initialize the Redactor with file path
Redactor redactor = new Redactor("sample.pdf");
```

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using GroupDocs.Redaction;

// Step 1: Use GroupDocs.Redaction API to fetch all supported formats.
IEnumerable<FileType> supportedFileTypes = FileType.GetSupportedFileFormats().OrderBy(f => f.Extension);
```

```csharp
// Step 2: Loop through the list of file types and print details.
foreach (FileType fileType in supportedFileTypes)
{
    Console.WriteLine($"{fileType.Extension} - {fileType.FileFormatName}");
}
```

## دروس ذات صلة

- [دروس معالجة الصيغ لـ GroupDocs.Redaction .NET](/redaction/net/format-handling/)
- [دروس تحميل المستندات باستخدام GroupDocs.Redaction لـ .NET](/redaction/net/document-loading/)
- [دروس حفظ المستندات لـ GroupDocs.Redaction .NET](/redaction/net/document-saving/)