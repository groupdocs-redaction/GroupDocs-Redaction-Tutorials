---
date: '2026-10-06'
description: تعلم كيفية إخفاء البيانات الحساسة باستخدام GroupDocs.Redaction .NET.
  يوضح لك هذا الدليل step‑by‑step كيفية إنشاء وتطبيق وحفظ redaction policy بصيغة XML.
keywords:
- redact sensitive data
- mask confidential information
- groupdocs redaction .net
lastmod: '2026-10-06'
og_description: تعلم كيفية إخفاء البيانات الحساسة باستخدام GroupDocs.Redaction .NET.
  يوضح لك هذا الدليل step‑by‑step كيفية إنشاء وتطبيق وحفظ redaction policy بصيغة XML.
og_image_alt: Tutorial showing how to redact sensitive data in documents with GroupDocs.Redaction
  for .NET
og_title: كيفية إخفاء البيانات الحساسة باستخدام GroupDocs.Redaction .NET
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
title: كيفية إخفاء البيانات الحساسة باستخدام GroupDocs.Redaction .NET
type: docs
url: /ar/net/advanced-redaction/groupdocs-redaction-net-create-save-policy/
weight: 1
---

# كيفية إخفاء البيانات الحساسة باستخدام GroupDocs.Redaction .NET

حماية المعلومات السرية داخل العقود والبيانات المالية أو سجلات المرضى هي متطلب غير قابل للتفاوض للتطبيقات الحديثة. في هذا الدليل ستتعلم **كيفية إخفاء البيانات الحساسة** باستخدام GroupDocs.Redaction لـ .NET، بدءًا من تثبيت SDK إلى تعريف سياسات XML القابلة لإعادة الاستخدام التي يمكن تطبيقها على أي نوع من المستندات.

## إجابات سريعة
- **ماذا يعني “إنشاء سياسة إخفاء”？** إنها عملية تعريف القواعد (نص، تعبيرات regex، صور، إلخ) التي تخبر GroupDocs.Redaction كيفية إخفاء أو استبدال المحتوى السري.  
- **أي مكتبة أحتاج؟** GroupDocs.Redaction لـ .NET، متوفرة عبر NuGet.  
- **هل أحتاج إلى ترخيص؟** الإصدار التجريبي المجاني يكفي للتطوير؛ الترخيص الدائم مطلوب للإنتاج.  
- **هل يمكنني إعادة استخدام السياسة؟** نعم—بعد حفظها كملف XML يمكنك تحميلها لاحقًا وتطبيقها على أي مستند.  
- **ما إصدارات .NET المدعومة؟** .NET Framework 4.5+، .NET Core 3.1+، .NET 5/6/7.

## ما هي سياسة الإخفاء؟

سياسة الإخفاء هي مجموعة من القواعد التي تحدد *ما* يجب إزالته أو استبداله و*كيف* يجب أن يبدو الاستبدال. من خلال إنشاء السياسة مرة واحدة، يمكنك تطبيق معايير أمان متسقة على كل مستند يتم معالجته بواسطة تطبيقك.

## كيف تعمل سياسة الإخفاء؟

قم بتحميل مستند باستخدام محرك `Redactor`، أرفق قاعدة أو أكثر للإخفاء، ثم استدعِ `Apply`. يقوم المحرك بمسح المستند، إخفاء المحتوى المطابق، ويمكنه اختياريًا إنشاء ملف جديد. يمكن تصدير مجموعة القواعد نفسها إلى XML، مما يتيح لك إعادة استخدام السياسة دون إعادة تجميع الكود.

## لماذا تستخدم GroupDocs.Redaction لإنشاء سياسة إخفاء؟

يوفر GroupDocs.Redaction مجموعة شاملة من الميزات التي تبسط إنشاء وإدارة وتنفيذ سياسات الإخفاء، مما يضمن حماية بيانات متسقة عبر أنواع المستندات المتنوعة مع تقديم أداء عالي وتكامل سهل مع تطبيقات .NET الحالية للفرق والمؤسسات.

- **دعم صيغ واسع** – يتعامل SDK مع أكثر من 30 نوعًا من الملفات، بما في ذلك PDF، DOCX، XLSX، PPTX، وصيغ الصور، ويمكنه معالجة ملفات تصل إلى 2 GB دون تحميل الملف بالكامل في الذاكرة.  
- **دقة برمجية** – تعريف عبارات دقيقة، تعبيرات عادية، أو منطق مخصص لاستهداف البيانات التي تحتاج إلى إخفائها فقط.  
- **سياسات XML قابلة لإعادة الاستخدام** – تصدير قواعدك مرة واحدة ومشاركتها عبر الفرق أو الخدمات أو الميكرو‑خدمات.  
- **محرك محسّن للأداء** – تعالج المكتبة مستندات مئات الصفحات في أقل من ثانية على عتاد الخادم المعتاد، مما يجعلها مناسبة لخطوط الأنابيب ذات الإنتاجية العالية.

## المتطلبات المسبقة
- مكتبة GroupDocs.Redaction المتوافقة مع بيئة تشغيل .NET الخاصة بك.  
- Visual Studio، VS Code، أو أي بيئة تطوير تدعم C#.  
- إلمام أساسي بـ C# وبنية مشروع .NET.

## إعداد GroupDocs.Redaction لـ .NET

أولاً، أضف المكتبة إلى مشروعك.

**استخدام .NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**استخدام Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```  

أو ابحث عن “GroupDocs.Redaction” في واجهة NuGet Package Manager وقم بتثبيتها من هناك.

### الحصول على الترخيص
- ابدأ بـ **الإصدار التجريبي المجاني** لاستكشاف الميزات.  
- اطلب **ترخيصًا مؤقتًا** للاختبار المطول، ثم اشترِ ترخيصًا كاملًا للاستخدام في الإنتاج.

### التهيئة الأساسية
أضف مساحة الاسم إلى ملف المصدر الخاص بك:

```csharp
using GroupDocs.Redaction;
```  

فئة `Redactor` هي المحرك الأساسي الذي يحمل مستندًا ويطبق قواعد الإخفاء.

## كيفية إنشاء سياسة إخفاء خطوة بخطوة

فيما يلي دليل كامل يوضح كيفية بناء سياسة إخفاء برمجيًا، تكوين قواعدها، تطبيقها على مستند، وأخيرًا حفظ السياسة كملف XML لإعادة الاستخدام في المستقبل، مما يضمن إخفاءً متسقًا عبر مشاريع وأنواع مستندات متعددة.

### الخطوة 1: إعداد دليل المستندات الخاص بك
```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
```  
*استبدل `"YOUR_DOCUMENT_DIRECTORY"` بالمجلد الذي يحتوي على المستندات التي تريد حمايتها.*

### الخطوة 2: تحميل المستند
```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // Further code will go here
}
```  
كائن `Redactor` يفتح الملف ويدير دورة حياته.

### الخطوة 3: تعريف عمليات الإخفاء
ExactPhraseRedaction يحدد قاعدة تستبدل عبارة محددة، بينما يستخدم `RegexRedaction` تعبيرًا عاديًا لمطابقة الأنماط.  
```csharp
var redactions = new List<Redaction>
{
    new ExactPhraseRedaction("Sensitive Phrase", new ReplacementOptions("[REDACTED]")),
    new RegexRedaction(@"\d{4}-\d{2}-\d{2}", new ReplacementOptions("[DATE REDACTED]"))
};
```  
هنا نقوم بإنشاء قاعدتين:  
1. **ExactPhraseRedaction** – يستبدل عبارة معروفة بـ “[REDACTED]”.  
2. **RegexRedaction** – يجد التواريخ بصيغة `YYYY‑MM‑DD` ويستبدلها بـ “[DATE REDACTED]”.

### الخطوة 4: تطبيق عمليات الإخفاء
```csharp
redactor.Apply(redactions);
```  
جميع القواعد المعرفة تُنفّذ على المستند المفتوح في مرور واحد.

### الخطوة 5: حفظ السياسة كملف XML
```csharp
string policyFile = "policy.xml";
redactor.SavePolicy(policyFile, new SaveOptions());
```  
ملف XML يخزن تعريفات الإخفاء، مما يتيح لك إعادة استخدام نفس السياسة دون إعادة كتابة الكود.

## التطبيقات العملية

- **المكاتب القانونية** يمكنها إخفاء أرقام القضايا وأسماء العملاء قبل مشاركة المسودات.  
- **أقسام المالية** تقوم بإخفاء أرقام الحسابات أو تواريخ المعاملات في التقارير.  
- **مقدمو الرعاية الصحية** يضمنون الامتثال لـ HIPAA عن طريق إزالة معرّفات المرضى.

## نصائح الأداء

- افتح **مستندًا واحدًا في كل مرة** للحفاظ على انخفاض استهلاك الذاكرة.  
- اكتب **تعبيرات عادية فعّالة**؛ تجنّب الأنماط الواسعة جدًا التي تزيد من زمن المعالجة.  
- حافظ على تحديث المكتبة **للاستفادة من تحسينات الأداء وأنواع الإخفاء الجديدة**.

## المشكلات الشائعة والحلول

| المشكلة | سبب حدوثها | كيفية الإصلاح |
|-------|----------------|------------|
| **استثناء IO عند إعداد الدليل** | مسار غير صحيح أو عدم وجود أذونات كتابة | تحقق من وجود المجلد وأن التطبيق لديه أذونات القراءة/الكتابة. |
| **Regex لا يطابق النص المتوقع** | النمط صارم جدًا أو يفتقد أحرف الهروب | اختبر الـ regex باستخدام أداة اختبار عبر الإنترنت؛ عدّل الكميات أو أضف أحرف الهروب للرموز الخاصة. |
| **ملف السياسة غير مُنشأ** | `SavePolicy` تم استدعاؤه قبل تطبيق الإخفاءات أو بمسار غير صالح | تأكد من أن دليل الإخراج قابل للكتابة واستدعِ `SavePolicy` بعد `Apply`. |

## الأسئلة المتكررة

**س: هل يمكنني تحميل سياسة XML موجودة بدلاً من بناء واحدة برمجيًا؟**  
نعم—استخدم `redactor.LoadPolicy("policy.xml")` لاستيراد سياسة محفوظة مسبقًا.

**س: هل يدعم GroupDocs.Redaction ملفات PDF محمية بكلمة مرور؟**  
بالطبع. مرّر كلمة المرور إلى مُنشئ `Redactor`: `new Redactor(sourceFile, "password")`.

**س: هل يمكن إخفاء الصور أو البيانات الوصفية؟**  
توفر SDK فئات `ImageRedaction` و `MetadataRedaction` لهذه السيناريوهات.

**س: كيف أتعامل مع مستندات كبيرة (مئات الميجابايت)؟**  
عالجها على أجزاء أو استخدم واجهة برمجة التطبيقات المتدفقة لتقليل استهلاك الذاكرة؛ يمكن للمحرك معالجة ملفات تصل إلى 2 GB دون تحميل الملف بالكامل إلى الذاكرة.

**س: ما نموذج الترخيص المطلوب للاستخدام التجاري؟**  
يتطلب الترخيص المدفوع للنشر في بيئات الإنتاج؛ الترخيص التجريبي يكفي للتطوير والاختبار.

## الخاتمة

أصبح لديك الآن **سياسة إخفاء** كاملة وقابلة لإعادة الاستخدام يمكنك تطبيقها على أي مستند باستخدام GroupDocs.Redaction لـ .NET. من خلال تصدير السياسة إلى XML، تبسط التحديثات المستقبلية وتضمن حماية بيانات متسقة عبر مؤسستك.

### الخطوات التالية
- جرّب أنواع إخفاء إضافية مثل `ImageRedaction` أو `MetadataRedaction`.  
- دمج منطق تحميل السياسة في سير عمل إدارة المستندات الخاص بك لتطبيق الإخفاء تلقائيًا.  
- استكشف مرجع API الخاص بـ **GroupDocs.Redaction** للتخصيص المتقدم.

---

**Last Updated:** 2026-10-06  
**Tested With:** GroupDocs.Redaction 5.8 for .NET  
**Author:** GroupDocs  

**الموارد**  
- [التوثيق](https://docs.groupdocs.com/redaction/net/)  
- [مرجع API](https://reference.groupdocs.com/redaction/net)  
- [تحميل](https://releases.groupdocs.com/redaction/net/)  
- [منتدى الدعم المجاني](https://forum.groupdocs.com/c/redaction/33)  
- [طلب ترخيص مؤقت](https://purchase.groupdocs.com/temporary-license/)

## دروس ذات صلة

- [إخفاء البيانات الحساسة باستخدام GroupDocs.Redaction .NET (C#)](/redaction/net/advanced-redaction/groupdocs-redaction-net-implement-iredactioncallback-csharp/)  
- [تنفيذ إخفاء المستند باستخدام GroupDocs.Redaction .NET: دليل خطوة بخطوة](/redaction/net/getting-started/implement-document-redaction-groupdocs-redaction-net/)  
- [كيفية إخفاء المستندات باستخدام GroupDocs.Redaction .NET – دليل شامل](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)