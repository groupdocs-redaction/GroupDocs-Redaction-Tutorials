---
date: '2026-07-20'
description: تعلم كيفية حذف المعلومات الحساسة من المستندات، وإخفاء البيانات الحساسة،
  وحفظ الملفات المحذوفة إلى تدفق الذاكرة باستخدام GroupDocs.Redaction لـ .NET.
keywords:
- how to redact documents
- redact sensitive information
- redact specific text
- save to memory stream
- save redacted document
lastmod: '2026-07-20'
og_description: كيفية حذف المعلومات الحساسة من المستندات باستخدام GroupDocs.Redaction
  لـ .NET. اتبع هذا الدليل خطوة بخطوة لإخفاء البيانات الحساسة وحفظ الملف المحذوف إلى
  تدفق الذاكرة.
og_image_alt: 'Developer guide: Redact and save documents using GroupDocs.Redaction
  for .NET'
og_title: كيفية حذف المعلومات الحساسة من المستندات باستخدام GroupDocs.Redaction لـ
  .NET
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
title: كيفية حذف المعلومات الحساسة من المستندات باستخدام GroupDocs.Redaction لـ .NET
  – دليل كامل
type: docs
url: /ar/net/document-saving/redact-save-documents-groupdocs-redaction-net/
weight: 1
---

# كيفية تمويه المستندات باستخدام GroupDocs.Redaction لـ .NET

في بيئات المؤسسات الحديثة، **كيفية تمويه المستندات** مهارة حاسمة لحماية البيانات الشخصية، الأسرار التجارية، والمعلومات المتعلقة بالامتثال. يوضح هذا الدليل كيفية تمويه المعلومات الحساسة من ملفات Word أو PDF أو الصور ثم حفظ الناتج المتموي مباشرةً إلى تدفق الذاكرة—كل ذلك باستخدام GroupDocs.Redaction لـ .NET.

## إجابات سريعة
- **ما الذي يفعله التمويه؟** إنه يستبدل المحتوى المحدد بشكل دائم ببديل أو يزيله، مما يضمن عدم إمكانية استعادة البيانات.  
- **ما الصيغ المدعومة؟** أكثر من 30 نوع ملف، بما في ذلك PDF و DOCX و PPTX وصيغ الصور الشائعة.  
- **هل يمكنني تمويه دون الكتابة إلى القرص؟** نعم—احفظ النتيجة في `MemoryStream` للمعالجة داخل الذاكرة.  
- **هل أحتاج إلى ترخيص للإنتاج؟** يلزم ترخيص كامل للاستخدام في الإنتاج؛ يتوفر تجربة مجانية للتقييم.  
- **هل هو متوافق مع .NET Core؟** بالتأكيد—GroupDocs.Redaction يعمل مع .NET Framework 4.6+، .NET Core 3.1+، و .NET 5/6/7.

## ما هو تمويه المستند؟
تمويه المستند يزيل أو يغطي بشكل دائم النصوص، الصور، والبيانات الوصفية السرية من الملف، مما يضمن أن المحتوى المخفي لا يمكن استعادته أو عرضه أو استخراجه لاحقًا. يستبدل العناصر الحساسة ببديل مثل مستطيل أسود أو نص مخصص، ويحدث بنية المستند بحيث يصبح البيانات المتموية غير قابلة للاسترجاع.

## لماذا تستخدم GroupDocs.Redaction لتمويه المستندات؟
GroupDocs.Redaction يدعم **أكثر من 30 صيغة ملف** ويمكنه معالجة ملفات تصل إلى **2 جيجابايت** دون تحميل المستند بالكامل في الذاكرة، مما يحقق **سرعة معالجة أعلى بنسبة 30 ٪** مقارنةً بالعديد من المنافسين. يتيح API الخاص به تطبيق تمويهات بالعبارة الدقيقة، أو التعبير النمطي، أو الصور بنقرة واحدة، مما يجعله الخيار الأكثر كفاءة لمطوري .NET.

## المتطلبات المسبقة
- **حزمة GroupDocs.Redaction** على NuGet (أحدث إصدار).  
- .NET Framework 4.6+ **أو** .NET Core 3.1+ مثبت.  
- بيئة تطوير متوافقة مع C# مثل Visual Studio 2022.  
- معرفة أساسية بـ C# وإلمام بملفات الإدخال/الإخراج.

### المكتبات المطلوبة والإصدارات
- **GroupDocs.Redaction** – استخدم دائمًا أحدث إصدار للوصول إلى أحدث خوارزميات التمويه وتصحيحات الأمان.  
- **System.IO** – لمعالجة التدفقات (مضمن في .NET).

### خطوات الحصول على الترخيص
- **تجربة مجانية:** اشترك على موقع GroupDocs للحصول على تجربة لمدة 30 يومًا.  
- **ترخيص مؤقت:** اطلب مفتاحًا مؤقتًا لاختبار التطوير.  
- **ترخيص كامل:** اشترِ ترخيصًا للإنتاج لاستخدام غير محدود.

## التهيئة الأساسية والإعداد
فئة `Redactor` هي نقطة الدخول لجميع عمليات التمويه في GroupDocs.Redaction. بعد تثبيت حزمة NuGet، تقوم بإنشاء كائن `Redactor` مع مسار المستند المصدر.

```csharp
using GroupDocs.Redaction;
using System.IO;

// Initialize Redactor with the source file path
Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

## كيف تمويه نص محدد في مستند؟
لتمويه نص محدد، حمّل الملف المصدر باستخدام كائن `Redactor`، ثم طبّق `ExactPhraseRedaction` يستهدف السلسلة الدقيقة التي تريد إخفاءها. يقوم API بمسح المستند، يستبدل كل تطابق بالغطاء المختار، ويسجل التغييرات في سجل التغييرات، مما يتيح لك التحقق من التمويه قبل الحفظ.

```csharp
RedactorChangeLog result = redactor.Apply(new ExactPhraseRedaction("John Doe"));
```

الفئة `ExactPhraseRedaction` تستبدل كل ظهور للعبارة الدقيقة بمستطيل أسود (أو أي بديل مخصص تقوم بتكوينه).  

**خطوة‑بخطوة:**
1. **تحميل** – أنشئ كائن `Redactor` يشير إلى ملفك.  
2. **تطبيق** – استدعِ `Apply` مع `ExactPhraseRedaction` (أو نوع تمويه آخر).  
3. **فحص** – راجع `RedactorChangeLog` لتأكيد عدد التطابقات التي تم العثور عليها واستبدالها.  

## كيف تحفظ مستندًا تمويهًا إلى MemoryStream؟
`MemoryStream` هو تدفق .NET يخزن البيانات في الذاكرة، مما يسمح بالقراءة/الكتابة السريعة دون عمليات إدخال/إخراج على القرص. باستخدام طريقة `Save`، يمكنك توجيه الناتج المتموي إلى `MemoryStream`، والذي يمكن بعد ذلك إرساله عبر الشبكة، تخزينه في قاعدة بيانات، أو إرجاعه مباشرةً من نقطة نهاية API دون إنشاء ملفات مؤقتة.

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

**نقاط رئيسية:**
- طريقة `Save` تكتب الناتج المتموي إلى أي تنفيذ لـ `Stream`، بما في ذلك `MemoryStream`.  
- لا يتم إنشاء ملفات مؤقتة، مما يحسن الأمان والأداء.  
- يمكنك دمج ذلك مع `FileStreamResult` في ASP.NET Core لإرجاع الملف مباشرةً إلى المتصفح.

## المشكلات الشائعة والحلول
| المشكلة | سبب حدوثها | الحل |
|-------|----------------|-----|
| **لم يتم تطبيق التمويه** | حالة الأحرف في العبارة تختلف عن المصدر. | استخدم `ExactPhraseRedaction("John Doe", caseSensitive: false)` أو تمويه باستخدام تعبير عادي للحصول على مطابقة مرنة. |
| **الملفات الكبيرة تسبب نفاد الذاكرة** | محاولة تحميل الملف بالكامل إلى الذاكرة. | GroupDocs.Redaction يبث البيانات داخليًا؛ تأكد من أنك تستخدم أحدث إصدار يعالج الملفات على شكل قطع. |
| **الملف المحفوظ تالف** | لم يتم إعادة تعيين التدفق قبل الإرسال. | بعد `redactor.Save(stream)`، اضبط `stream.Position = 0` قبل القراءة أو الإرجاع. |

## الأسئلة المتكررة

**س: هل يمكنني تمويه ملفات PDF باستخدام نفس الـ API؟**  
ج: نعم—GroupDocs.Redaction يتعامل مع PDF و DOCX و PPTX والعديد من صيغ الصور بشكل موحد؛ فقط وجه `Redactor` إلى ملف PDF.

**س: هل يبقى التمويه بعد تحويل المستند إلى صيغة أخرى؟**  
ج: بالتأكيد—بمجرد تمويه المحتوى، يتم إزالته بشكل دائم، بغض النظر عن التحويلات اللاحقة.

**س: كيف يمكنني تخصيص مظهر التمويه؟**  
ج: استخدم `RedactionOptions` لتعيين لون التغطية، الشفافية، أو استبدال النص بسلسلة مخصصة.

**س: هل يمكن تمويه باستخدام تعبيرات عادية؟**  
ج: نعم—`RegexRedaction` يتيح لك تعريف أنماط مثل أرقام بطاقات الائتمان أو عناوين البريد الإلكتروني.

**س: ما إصدارات .NET المدعومة رسميًا؟**  
ج: .NET Framework 4.6+، .NET Core 3.1+، .NET 5، .NET 6، و .NET 7.

---

**آخر تحديث:** 2026-07-20  
**تم الاختبار مع:** GroupDocs.Redaction 23.12 لـ .NET  
**المؤلف:** GroupDocs  

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

## دروس ذات صلة

- [كيفية تحميل وتمويه المستندات باستخدام GroupDocs.Redaction .NET: دليل كامل](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [حفظ المستندات المتموية بالتنسيق الأصلي باستخدام GroupDocs.Redaction .NET](/redaction/net/document-saving/save-redacted-docs-original-format-groupdocs-redaction-net/)
- [تمويه المستندات بأمان في .NET باستخدام التدفقات: دليل لـ GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)