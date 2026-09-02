---
date: '2026-06-06'
description: تعلم كيفية استرجاع البيانات الوصفية واستخراج بيانات وصفية للوثائق باستخدام
  GroupDocs.Redaction .NET، مما يتيح إدارة مستندات قوية والامتثال.
keywords:
- how to retrieve metadata
- extract document metadata
- get document properties
- read file metadata
- get document size
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to retrieve metadata and extract document metadata using
    GroupDocs.Redaction .NET, enabling robust document management and compliance.
  headline: How to Retrieve Metadata with GroupDocs.Redaction .NET API
  type: TechArticle
- description: Learn how to retrieve metadata and extract document metadata using
    GroupDocs.Redaction .NET, enabling robust document management and compliance.
  name: How to Retrieve Metadata with GroupDocs.Redaction .NET API
  steps:
  - name: Prepare Your Document Path
    text: 'Define the absolute or relative path to the target file: Replace `YOUR_DOCUMENT_DIRECTORY`
      with the folder that contains your document.'
  - name: Initialize Redactor Instance
    text: 'Create a `Redactor` object that provides access to metadata methods:'
  - name: Retrieve Document Information
    text: 'Call `GetDocumentInfo()` on the `Redactor` instance to pull all available
      properties: The returned object includes file type, number of pages, and file
      size.'
  - name: Display Document Details
    text: 'Output the information to the console or UI. The sample code (commented
      for standalone runs) demonstrates how to print each property:'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction reads metadata from more than 50 formats, including
      PDF, DOCX, XLSX, PPTX, HTML, and common image types.
    question: Which document formats can I extract metadata from?
  - answer: Pass the password to the `Redactor` constructor; the API will decrypt
      the file before extracting metadata.
    question: How do I handle password‑protected files?
  - answer: While there is no hard limit, files larger than 2 GB may require additional
      memory tuning; performance remains linear with file size.
    question: Is there a limit to the size of files I can process?
  - answer: Yes—iterate over a collection of file paths and call `GetDocumentInfo()`
      for each; the library is thread‑safe for parallel execution.
    question: Can I retrieve metadata in a batch operation?
  - answer: A free trial license is sufficient for development and testing; a commercial
      license is required for production deployments.
    question: Do I need a license for development builds?
  type: FAQPage
title: كيفية استرجاع البيانات الوصفية باستخدام GroupDocs.Redaction .NET API
type: docs
url: /ar/net/document-information/groupdocs-redaction-net-document-metadata-retrieval/
weight: 1
---

# كيفية استرجاع البيانات الوصفية باستخدام GroupDocs.Redaction .NET

في عصرنا الرقمي اليوم، **كيفية استرجاع البيانات الوصفية** من ملف هي خطوة أساسية لأي تطبيق يركز على المستندات. سواء كنت بحاجة إلى قراءة بيانات وصفية للملف لتدقيق الامتثال، أو استخراج خصائص المستند للفهرسة، أو ببساطة عرض حجم المستند في واجهة المستخدم، فإن GroupDocs.Redaction .NET يوفر لك واجهة برمجة تطبيقات مختصرة للقيام بذلك في بضع أسطر من C#. يشرح هذا الدليل العملية بالكامل، من إعداد البيئة إلى عرض المعلومات المستخرجة، حتى تتمكن من بدء استخراج البيانات الوصفية للمستند فورًا.

## إجابات سريعة
- **ما هي الطريقة الأساسية للحصول على البيانات الوصفية؟** استدعِ `Redactor.GetDocumentInfo()` على كائن `Redactor`.  
- **ما الصيغ المدعومة؟** أكثر من 50 صيغة إدخال وإخراج، بما في ذلك PDF و DOCX و XLSX و PPTX وأنواع الصور.  
- **هل أحتاج إلى ترخيص للتطوير؟** ترخيص تجريبي مجاني يكفي للاختبار؛ الترخيص الكامل مطلوب للإنتاج.  
- **هل يمكنني معالجة ملفات كبيرة؟** نعم—GroupDocs.Redaction يتعامل مع مستندات مئات الصفحات دون تحميل الملف بالكامل في الذاكرة.  
- **هل يتوفر دعم غير متزامن؟** يمكن تغليف واجهة البرمجة في نمط غير متزامن للحفاظ على استجابة خيوط واجهة المستخدم.

## ما هو استرجاع البيانات الوصفية في GroupDocs.Redaction؟
استرجاع البيانات الوصفية هو عملية الوصول إلى خصائص المستند المدمجة—مثل نوع الملف، عدد الصفحات، والحجم—من خلال واجهة برمجة التطبيقات الخاصة بالمكتبة. من خلال استخراج هذه الخصائص، يمكن للمطورين تقييم خصائص المستند برمجيًا، دعم الفهرسة، فرض قواعد الامتثال، واتخاذ قرارات مستنيرة بشأن خطوات المعالجة اللاحقة.

## كيفية استرجاع بيانات المستند الوصفية؟
فئة `Redactor` هي الواجهة الأساسية لتحميل وفحص المستندات في GroupDocs.Redaction.  
`GetDocumentInfo()` هي طريقة تُعيد كائن `DocumentInfo` يحتوي على البيانات الوصفية للمستند.  

حمّل ملفك باستخدام `new Redactor("path/to/file")` واستدعِ `GetDocumentInfo()`—ستُعيد الاستدعاء كائن `DocumentInfo` يحتوي على النوع، عدد الصفحات، الحجم، وغيرها من الخصائص. يعمل هذا النهج ذو الخطوتين مع أي صيغة مدعومة ولا يتطلب أي تكوين إضافي. يمكنك بعد ذلك قراءة الحقول مثل `FileType` و `PageCount` و `FileSize` لعرضها أو تسجيلها.

## المتطلبات المسبقة
- **GroupDocs.Redaction .NET** الإصدار 21.6 أو أحدث.  
- .NET Framework 4.7.2 +, .NET Core 3.1 +, أو .NET 5/6+.  
- معرفة أساسية بـ C# وبيئة تطوير متكاملة (IDE) مثل Visual Studio أو Rider أو غيرها.

## إعداد GroupDocs.Redaction لـ .NET
البدء مع GroupDocs.Redaction سهل. قم بتثبيت الحزمة باستخدام إحدى الطرق التالية:

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

أو، استخدم **واجهة مدير الحزم NuGet**: ابحث ببساطة عن “GroupDocs.Redaction” وانقر **Install**.

### الحصول على الترخيص
لتجربة GroupDocs.Redaction، يمكنك الحصول على ترخيص تجريبي مجاني. للاستخدام المستمر في التطوير أو الإنتاج، اشترِ ترخيصًا كاملاً أو اطلب ترخيصًا مؤقتًا من الموقع الرسمي.

بعد التثبيت، قم بتهيئة المكتبة كما يلي:

```csharp
using GroupDocs.Redaction;
```

## دليل التنفيذ

### ميزة الحصول على معلومات المستند
تركز هذه الميزة على استخراج البيانات الوصفية الحيوية من المستندات باستخدام GroupDocs.Redaction .NET. اتبع الخطوات التالية:

#### الخطوة 1: إعداد مسار المستند الخاص بك
حدد المسار المطلق أو النسبي للملف المستهدف:

```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY\\SampleDocx.docx";
```

استبدل `YOUR_DOCUMENT_DIRECTORY` بالمجلد الذي يحتوي على المستند الخاص بك.

#### الخطوة 2: تهيئة كائن Redactor
أنشئ كائن `Redactor` الذي يوفر الوصول إلى طرق البيانات الوصفية:

```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // Further operations will be performed here
}
```

#### الخطوة 3: استرجاع معلومات المستند
استدعِ `GetDocumentInfo()` على كائن `Redactor` لجلب جميع الخصائص المتاحة:

```csharp
IDocumentInfo info = redactor.GetDocumentInfo();
```

الكائن المعاد يتضمن نوع الملف، عدد الصفحات، وحجم الملف.

#### الخطوة 4: عرض تفاصيل المستند
اطبع المعلومات إلى وحدة التحكم أو واجهة المستخدم. يوضح كود العينة (معلق للتنفيذ المستقل) كيفية طباعة كل خاصية:

```csharp
Console.WriteLine($"File type: {info.FileType}\\
Number of pages: {info.PageCount}\\
Document size: {info.SizeInBytes} bytes");
```

### لماذا تستخدم GroupDocs.Redaction لاستخراج البيانات الوصفية؟
GroupDocs.Redaction يدعم **أكثر من 50 صيغة ملف** ويمكنه معالجة مستندات يصل حجمها إلى **2 جيجابايت** مع الحفاظ على استهلاك الذاكرة أقل من **100 ميجابايت** للأعباء النموذجية. تستخرج المكتبة البيانات الوصفية دون تحميل المستند بالكامل، مما يوفر استجابات سريعة—غالبًا أقل من **200 مللي ثانية** لملف PDF مكوّن من 100 صفحة على خادم عادي.

### المشكلات الشائعة والحلول
- **مسار ملف غير صحيح** – تحقق من سلسلة المسار وتأكد من أن الملف قابل للوصول من العملية الجارية.  
- **صيغة غير مدعومة** – راجع قائمة الصيغ؛ إذا كانت صيغة مفقودة، فكر في تحويلها أولاً.  
- **عنق زجاجة في الأداء** – بالنسبة للملفات الكبيرة جدًا، فعّل خيارات البث أو عالج الصفحات على دفعات لتقليل استهلاك الذاكرة.

## التطبيقات العملية
فهم البيانات الوصفية للمستند يتيح عدة سيناريوهات واقعية:

1. **أنظمة إدارة المستندات (DMS)** – أتمتة التصنيف والفهرسة بناءً على النوع أو الحجم أو عدد الصفحات.  
2. **تدقيق الامتثال** – تحقق من أن الملفات السرية تحتوي على البيانات الوصفية المطلوبة قبل الأرشفة.  
3. **ترحيل البيانات** – جمع الملفات حسب الخصائص لتسهيل مهام الترحيل الضخم.

## اعتبارات الأداء
- **استخدام موارد فعال** – استخدم كائن `Redactor` داخل كتلة `using` لضمان التخلص السليم.  
- **أنماط غير متزامنة** – غلف استدعاءات البيانات الوصفية بـ `Task.Run` أو نفّذ أطر غير متزامنة للحفاظ على استجابة خيوط الواجهة في تطبيقات سطح المكتب أو الويب.

## الأسئلة المتكررة

**س: ما هي صيغ المستند التي يمكنني استخراج البيانات الوصفية منها؟**  
ج: يقرأ GroupDocs.Redaction البيانات الوصفية من أكثر من 50 صيغة، بما في ذلك PDF و DOCX و XLSX و PPTX و HTML وأنواع الصور الشائعة.

**س: كيف أتعامل مع الملفات المحمية بكلمة مرور؟**  
ج: مرّر كلمة المرور إلى مُنشئ `Redactor`؛ ستقوم واجهة البرمجة بفك تشفير الملف قبل استخراج البيانات الوصفية.

**س: هل هناك حد لحجم الملفات التي يمكنني معالجتها؟**  
ج: رغم عدم وجود حد ثابت، قد تتطلب الملفات التي يزيد حجمها عن 2 جيجابايت ضبطًا إضافيًا للذاكرة؛ يبقى الأداء خطيًا مع حجم الملف.

**س: هل يمكنني استرجاع البيانات الوصفية في عملية دفعة؟**  
ج: نعم—قم بالتكرار على مجموعة من مسارات الملفات واستدعِ `GetDocumentInfo()` لكل منها؛ المكتبة آمنة للخطوط المتعددة للتنفيذ المتوازي.

**س: هل أحتاج إلى ترخيص لبنيات التطوير؟**  
ج: الترخيص التجريبي المجاني يكفي للتطوير والاختبار؛ الترخيص التجاري مطلوب للنشر في بيئة الإنتاج.

## الموارد
- [التوثيق](https://docs.groupdocs.com/redaction/net/)  
- [مرجع API](https://reference.groupdocs.com/redaction/net)  
- [تحميل](https://releases.groupdocs.com/redaction/net/)  
- [منتدى الدعم المجاني](https://forum.groupdocs.com/c/redaction/33)  
- [معلومات الترخيص المؤقت](https://purchase.groupdocs.com/temporary-license/)

## الخلاصة
أصبح لديك الآن دليل كامل خطوة بخطوة حول **كيفية استرجاع البيانات الوصفية** باستخدام GroupDocs.Redaction .NET. من خلال الاستفادة من طريقة `Redactor.GetDocumentInfo()`، يمكنك قراءة بيانات الملف بسرعة، دعم سير عمل الامتثال، وتعزيز أي خط أنابيب لمعالجة المستندات. استكشف ميزات Redaction الإضافية—مثل إخفاء المحتوى، إضافة العلامات المائية، وتحويل المستندات—لبناء حل إدارة مستندات متكامل.

---

**آخر تحديث:** 2026-06-06  
**تم الاختبار مع:** GroupDocs.Redaction .NET 21.6 (latest at time of writing)  
**المؤلف:** GroupDocs  

## دروس ذات صلة
- [كيفية استخراج بيانات المستند الوصفية من التدفقات باستخدام GroupDocs.Redaction .NET](/redaction/net/document-information/extract-document-info-streams-groupdocs-redaction-dotnet/)
- [كيفية إخفاء بيانات المستند الوصفية باستخدام GroupDocs.Redaction لـ .NET - دليل شامل](/redaction/net/metadata-redaction/redact-metadata-groupdocs-redaction-net/)
- [دروس تحميل المستندات مع GroupDocs.Redaction لـ .NET](/redaction/net/document-loading/)