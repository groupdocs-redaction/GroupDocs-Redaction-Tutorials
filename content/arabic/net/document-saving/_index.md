---
date: 2026-06-11
description: تعلم كيفية تصدير الملفات المحجوبة، وتكوين مجلدات الإخراج، وإنشاء ملفات
  PDF مُرصَّصة، وحفظها إلى التدفقات باستخدام GroupDocs.Redaction for .NET.
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
title: كيفية تصدير المستندات المحجوبة باستخدام GroupDocs.Redaction .NET
type: docs
url: /ar/net/document-saving/
weight: 3
---

# كيفية تصدير المستندات المُحذوفة باستخدام GroupDocs.Redaction .NET

في هذا الدليل الشامل ستكتشف **كيفية تصدير المحتوى المحذوف** بأمان وكفاءة باستخدام GroupDocs.Redaction لـ .NET. سواء كنت بحاجة إلى الحفاظ على نوع الملف الأصلي، أو تأمين المستند كملف PDF مُرصّص، أو بث النتيجة مباشرة في الذاكرة، سنرشدك عبر كل خيار بشرحات واضحة ومحادثية ونصائح عملية. في نهاية هذا البرنامج التعليمي ستكون قادرًا على اختيار استراتيجية التصدير المناسبة لأي سيناريو مدفوع بالامتثال.

## إجابات سريعة
- **ما الصيغ التي يمكنني التصدير إليها؟** أي من أكثر من 30 صيغة أصلية مدعومة من قبل GroupDocs.Redaction، بالإضافة إلى PDF مُرصّص لأقصى درجات الأمان.  
- **هل أحتاج إلى ترخيص للبث؟** نعم، يلزم وجود ترخيص صالح لـ GroupDocs.Redaction للبث في بيئة الإنتاج.  
- **هل يمكنني تعيين مجلد إخراج مخصص؟** بالتأكيد – استخدم خاصية `OutputPath` أو `SaveOptions` لتكوينه.  
- **هل الرَسْتَرِزيشن آمن للملفات الكبيرة؟** يتعامل مع مستندات تصل إلى 500 صفحة دون تحميل الملف بالكامل في الذاكرة.  
- **ما إصدارات .NET المدعومة؟** .NET Framework 4.6+، .NET Core 3.1+، .NET 5/6/7.

## ما هو GroupDocs.Redaction؟
GroupDocs.Redaction هي مكتبة .NET تقوم بإزالة أو إخفاء المعلومات الحساسة برمجياً من ملفات PDF، Word، Excel، PowerPoint، الصور، والعديد من الصيغ الأخرى. توفر API عالي المستوى لتحديد مناطق الحذف، تطبيق السياسات، وأخيرًا تصدير المستند المنقّى. هذا يجعل من السهل دمج قدرات الحذف في أي تطبيق .NET.

## لماذا تصدير المستندات المحذوفة كملفات PDF مُرصّصة؟
تحوّل ملفات PDF المُرصّصة كل صفحة إلى صورة مسطحة، مما يلغي طبقات النص المخفي التي يمكن استخراجها لاحقًا. يضمن هذا التنسيق عدم إمكانية استعادة المحتوى المحذوف، متوافقًا مع معايير تنظيمية صارمة مثل GDPR وHIPAA. يمكن لـ GroupDocs.Redaction إنتاج ملفات PDF مُرصّصة بدقة تصل إلى 300 dpi، مع الحفاظ على جودة الصورة وضمان الأمان.

## كيفية تصدير المستندات المحذوفة؟
حمّل الملف المصدر، طبّق قواعد الحذف الخاصة بك، ثم استدعِ طريقة الحفظ المناسبة — إما `Save` للصيغة الأصلية، أو `SaveAsRasterizedPdf` لملفات PDF التي تحتوي على صور فقط، أو `SaveToStream` للتعامل في الذاكرة. أدناه سير العمل خطوة بخطوة. كل طريقة تضمن إزالة المحتوى المحذوف بشكل دائم مع الحفاظ على صيغة الإخراج المطلوبة.

### الخطوة 1: تثبيت حزمة NuGet
أضف أحدث حزمة GroupDocs.Redaction إلى مشروعك:

```bash
dotnet add package GroupDocs.Redaction
```

### الخطوة 2: تحميل المستند وتحديد عمليات الحذف
أنشئ كائن `Redactor`، حمّل الملف، وحدد المناطق التي تريد إخفاءها. توفر فئة `Redactor` الوظيفة الأساسية لتحميل المستندات وتطبيق قواعد الحذف.

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

### الخطوة 3: اختيار طريقة التصدير
#### تصدير بالصيغ الأصلية
```csharp
redactor.Save("RedactedReport.docx");
```

#### تصدير كملف PDF مُرصّص
```csharp
var rasterOptions = new RasterizationOptions { Dpi = 300 };
redactor.SaveAsRasterizedPdf("RedactedReport.pdf", rasterOptions);
```

#### تصدير إلى تدفق الذاكرة (مثالي لواجهات برمجة الويب API)
```csharp
using var stream = new MemoryStream();
redactor.Save(stream, SaveOptions.CreatePdf());
stream.Position = 0; // Reset for reading
```

طريقة `Save` تكتب المستند المحذوف إلى ملف بصيغته الأصلية. `SaveAsRasterizedPdf` تُنشئ ملف PDF حيث يتم عرض كل صفحة كصورة، مما يزيل أي نص مخفي. `SaveToStream` تُعيد الملف المحذوف كتدفق ذاكرة، مناسب لاستجابات الويب.

## كيفية تكوين مجلد الإخراج؟
قم بتعيين خاصية `OutputPath` على كائن `Redactor` أو مرّر كائن `SaveOptions` مخصص يتضمن الدليل المطلوب. `OutputPath` هي خاصية في `Redactor` تحدد الدليل الذي تُكتب فيه ملفات الإخراج. تتيح لك `SaveOptions` تخصيص معلمات الحفظ المختلفة، بما في ذلك مجلد الإخراج. يضمن ذلك أن جميع الملفات المصدرة تُحفظ في موقع متوقع، مما يبسط خطوط معالجة الدُفعات. يمكنك أيضًا تحديد مجلدات فرعية حسب نوع المستند للحفاظ على تنظيم مساحة العمل.

```csharp
var options = SaveOptions.CreatePdf();
options.OutputPath = @"C:\RedactedOutputs\";
redactor.Save(options);
```

## المشكلات الشائعة والحلول
- **لم يتم تطبيق الحذف:** تحقق من أن نمط البحث يطابق نص المستند تمامًا؛ استخدم `RegexOptions.IgnoreCase` إذا لزم الأمر. `RegexOptions` هي تعداد يتحكم في سلوك مطابقة التعبيرات النمطية، مثل حساسية الحالة.  
- **الملفات الكبيرة تسبب ضغطًا على الذاكرة:** فعّل وضع البث باستخدام `SaveToStream` وتجنّب استدعاء `Save` على المستند بأكمله.  
- **ملف PDF المُرصّص يبدو غير واضح:** زد قيمة DPI في `RasterizationOptions` (مثلاً 300–600) لتحسين جودة الصورة. `RasterizationOptions` تتيح لك ضبط معلمات مثل DPI وتنسيق الصورة لإخراج PDF مُرصّص.

## الأسئلة المتكررة

**س: هل يمكنني التصدير إلى صيغة لم تكن مدعومة أصلاً؟**  
ج: نعم، يمكن لـ GroupDocs.Redaction تحويل معظم أنواع الإدخال إلى PDF أو DOCX أو XLSX أو PPTX أو PDF مُرصّص، مع تغطية أكثر من 30 صيغة.

**س: كيف يحمي الرَسْتَرِزيشن البيانات المحذوفة؟**  
ج: من خلال تحويل كل صفحة إلى صورة مسطحة، تُزال أي طبقات نص مخفية، مما يجعل استخراج المحتوى الأصلي مستحيلًا.

**س: هل من الممكن ربط عدة قواعد حذف معًا؟**  
ج: بالتأكيد – يمكنك استدعاء `Apply` بشكل متكرر أو تمرير مجموعة من `RedactionOptions` لمعالجة العديد من الأنماط في خطوة واحدة. `RedactionOptions` تُعرّف الإعدادات لعملية حذف واحدة، مثل المنطقة ونوع الاستبدال.

**س: هل يجب إغلاق كائن Redactor؟**  
ج: كائن `Redactor` يطبق `IDisposable`؛ غلفه بكتلة `using` أو استدعِ `Dispose()` لتحرير مقابض الملفات بسرعة. `IDisposable` هي واجهة توفر آلية لتحرير الموارد غير المُدارة.

**س: ما هي أطر عمل .NET التي تم اختبارها رسميًا؟**  
ج: تم التحقق من صحة GroupDocs.Redaction على .NET Framework 4.6+، .NET Core 3.1+، و .NET 5/6/7.

## موارد إضافية

### الدروس المتاحة

- [كيفية حفظ المستندات كملفات PDF مُرصّصة باستخدام GroupDocs.Redaction لـ .NET: دليل كامل](./groupdocs-redaction-net-rasterized-pdfs/)
- [تنفيذ دليل الإخراج في .NET مع GroupDocs.Redaction: دليل شامل](./implement-output-directory-groupdocs-redaction-dotnet/)
- [حذف وحفظ المستندات باستخدام GroupDocs.Redaction لـ .NET: دليل كامل](./redact-save-documents-groupdocs-redaction-net/)
- [حفظ المستندات المحذوفة بالصيغ الأصلية باستخدام GroupDocs.Redaction .NET](./save-redacted-docs-original-format-groupdocs-redaction-net/)
- [حذف المستندات بأمان في .NET باستخدام التدفقات: دليل لـ GroupDocs.Redaction](./secure-document-redaction-net-streams-groupdocs-redaction/)

### روابط مفيدة

- [توثيق GroupDocs.Redaction لـ .NET](https://docs.groupdocs.com/redaction/net/)
- [مرجع API لـ GroupDocs.Redaction لـ .NET](https://reference.groupdocs.com/redaction/net/)
- [تحميل GroupDocs.Redaction لـ .NET](https://releases.groupdocs.com/redaction/net/)
- [منتدى GroupDocs.Redaction](https://forum.groupdocs.com/c/redaction/33)
- [دعم مجاني](https://forum.groupdocs.com/)
- [ترخيص مؤقت](https://purchase.groupdocs.com/temporary-license/)

---

**آخر تحديث:** 2026-06-11  
**تم الاختبار مع:** GroupDocs.Redaction 23.11 لـ .NET  
**المؤلف:** GroupDocs  

## دروس ذات صلة

- [حفظ المستندات المحذوفة بالصيغ الأصلية باستخدام GroupDocs.Redaction .NET](/redaction/net/document-saving/save-redacted-docs-original-format-groupdocs-redaction-net/)
- [كيفية حفظ المستندات كملفات PDF مُرصّصة باستخدام GroupDocs.Redaction لـ .NET: دليل كامل](/redaction/net/document-saving/groupdocs-redaction-net-rasterized-pdfs/)
- [حذف المستندات بأمان في .NET باستخدام التدفقات: دليل لـ GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)