---
date: '2026-07-06'
description: تعلم كيفية حفظ مستند مُحَرَّف مع الحفاظ على صيغته الأصلية باستخدام GroupDocs.Redaction
  لـ .NET. اتبع هذا الدليل خطوة بخطوة للحصول على تحرير سريع وآمن.
keywords:
- save redacted document
- GroupDocs.Redaction .NET
- document redaction tutorial
schemas:
- author: GroupDocs
  dateModified: '2026-07-06'
  description: Learn how to save a redacted document while preserving its original
    format with GroupDocs.Redaction for .NET. Follow this step‑by‑step guide for fast,
    secure redaction.
  headline: Save Redacted Document in Original Format Using GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to save a redacted document while preserving its original
    format with GroupDocs.Redaction for .NET. Follow this step‑by‑step guide for fast,
    secure redaction.
  name: Save Redacted Document in Original Format Using GroupDocs.Redaction .NET
  steps:
  - name: Initialize the Redactor
    text: 'Create an instance of the `Redactor` class with your document’s file path:'
  - name: Apply Exact Phrase Redaction
    text: '`ExactPhraseRedaction` is a built‑in redaction type that searches for an
      exact string and replaces it with a black rectangle or custom text.'
  - name: Configure Save Options
    text: '`SaveOptions` lets you keep the source file type, specify a suffix, and
      control memory usage.'
  - name: Save and Output
    text: 'Call the `Save` method with the configured options to write the redacted
      file to disk:'
  type: HowTo
- questions:
  - answer: Over 30 formats, including PDF, DOCX, PPTX, XLSX, and common image types
      such as PNG and JPEG.
    question: What file types can GroupDocs.Redaction handle?
  - answer: Yes – the `Redactor` class provides a `GetRedactions()` method that returns
      a collection you can render in a UI.
    question: Is it possible to preview redactions before saving?
  - answer: Absolutely. Supply the password when constructing the `Redactor` instance
      to unlock the file.
    question: Can I redact password‑protected documents?
  - answer: Yes – the NuGet package is compatible with .NET Framework 4.7.2+, .NET
      Core 3.1+, and .NET 5/6+.
    question: Does the library support .NET Core and .NET 5/6?
  - answer: Purchase a license through the GroupDocs website; a temporary trial license
      is available for evaluation.
    question: How do I obtain a production license?
  type: FAQPage
title: حفظ المستند المُحَرَّف بالصيغة الأصلية باستخدام GroupDocs.Redaction .NET
type: docs
url: /ar/net/document-saving/save-redacted-docs-original-format-groupdocs-redaction-net/
weight: 1
---

# حفظ المستند الممحو في تنسيقه الأصلي باستخدام GroupDocs.Redaction .NET

إزالة البيانات الحساسة هي متطلب شائع للامتثال، لكنك لا تريد فقدان مظهر وشعور الملف الأصلي. **يوضح لك هذا البرنامج التعليمي كيفية حفظ مستند ممحو مع الحفاظ على تنسيقه الأصلي** باستخدام GroupDocs.Redaction لـ .NET. ستحصل على حل جاهز للتنفيذ يعمل مع ملفات PDF، وملفات Word، وأكثر.

## إجابات سريعة
- **ما هي أسرع طريقة لحفظ مستند ممحو؟** قم بتحميل الملف باستخدام `Redactor`، ثم تطبيق `ExactPhraseRedaction`، ثم استدعاء `Save` مع `SaveOptions` التي تحافظ على نوع الملف الأصلي.  
- **ما هي الصيغ المدعومة؟** أكثر من 30 صيغة، بما في ذلك PDF و DOCX و PPTX وأنواع الصور.  
- **هل أحتاج إلى ترخيص للاستخدام التجريبي؟** نعم – احصل على ترخيص مؤقت من بوابة GroupDocs.  
- **هل يمكنني إضافة لاحقة مخصصة للملف المحفوظ؟** بالتأكيد – اضبط `SaveOptions.Suffix` على أي سلسلة (مثلاً، تاريخ).  
- **هل معالجة الملفات الكبيرة فعّالة من حيث الذاكرة؟** نعم – يقوم GroupDocs.Redaction ببث البيانات ولا يحمل الملف بالكامل في الذاكرة.

## ما هو “حفظ المستند الممحو”؟
*حفظ مستند ممحو* يعني كتابة الملف المعدل مرة أخرى إلى التخزين مع الحفاظ على التخطيط الأصلي، نوع الملف، والبيانات الوصفية. يتعامل GroupDocs.Redaction مع ذلك في استدعاء واحد، مما يلغي الحاجة إلى تحويل الصيغ يدويًا. العملية تحتفظ أيضًا بالموارد المضمنة مثل الخطوط، الصور، وخصائص المستند، مما يضمن أن المخرجات تبدو مطابقة للمصدر باستثناء المحتوى المزال.

## لماذا نستخدم GroupDocs.Redaction لـ .NET؟
يدعم GroupDocs.Redaction **أكثر من 30 صيغة إدخال وإخراج** ويمكنه معالجة ملفات تصل إلى **500 ميغابايت** دون تحميل المستند بالكامل في الذاكرة، مما يحقق **زيادة في الأداء بنسبة 20‑30 %** مقارنةً بأساليب إعادة كتابة الملفات البسيطة. واجهته البرمجية (API) مُدارة بالكامل، لا تتطلب أي برنامج خارجي، وتلتزم بـ GDPR و HIPAA وغيرها من اللوائح.

## المتطلبات المسبقة
- **GroupDocs.Redaction for .NET** – المكتبة الأساسية (أحدث نسخة مستقرة).  
- **.NET 6+** أو **.NET Framework 4.7.2+** مثبتة على جهاز التطوير الخاص بك.  
- معرفة أساسية بـ C# وإلمام بـ Visual Studio أو بيئة التطوير المتكاملة المفضلة لديك.

### المكتبات والاعتمادات المطلوبة
- **GroupDocs.Redaction for .NET**: أساسية لتطبيق عمليات الحذف.

### متطلبات إعداد البيئة
تحقق من أن مشروعك يستهدف بيئة تشغيل .NET مدعومة. راجع وثائق GroupDocs الرسمية للحصول على مصفوفات الإصدارات الدقيقة.

### متطلبات المعرفة المسبقة
فهم بنية C#، عمليات إدخال/إخراج الملفات، ومعالجة الاستثناءات.

## إعداد GroupDocs.Redaction لـ .NET

### تعليمات التثبيت
**باستخدام .NET CLI:**  
```shell
dotnet add package GroupDocs.Redaction
```  

**باستخدام Package Manager Console:**  
```powershell
Install-Package GroupDocs.Redaction
```  

**عبر واجهة مستخدم NuGet Package Manager:**  
- افتح مدير الحزم NuGet في Visual Studio.  
- ابحث عن **"GroupDocs.Redaction"** وقم بتثبيت أحدث نسخة.

### الحصول على الترخيص
ابدأ بتجربة مجانية لاختبار الميزات. زر موقع GroupDocs لطلب ترخيص مؤقت إذا لزم الأمر. للاستخدام طويل الأمد، فكر في شراء ترخيص من موقعهم.

بعد التثبيت والترخيص، استورد مساحة الأسماء GroupDocs.Redaction في ملفات الكود الخاصة بك:  
```csharp
using GroupDocs.Redaction;
```  

## دليل التنفيذ

### إنشاء وتكوين Redactor
فئة `Redactor` هي المكوّن الأساسي الذي يحمل المستند ويطبق عمليات الحذف.  

#### الخطوة 1: تهيئة Redactor
أنشئ مثالًا من فئة `Redactor` باستخدام مسار ملف المستند الخاص بك:  
```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY"; // Replace with actual path.
using (Redactor redactor = new Redactor(sourceFile))
{
    ...
}
```  

#### الخطوة 2: تطبيق Exact Phrase Redaction
`ExactPhraseRedaction` هو نوع حذف مدمج يبحث عن سلسلة مطابقة تمامًا ويستبدلها بمستطيل أسود أو نص مخصص.  
```csharp
// This replaces all instances of "John Doe" with "[personal]".
redactor.Apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]"));
```  

### حفظ المستند الممحو
الحفاظ على التنسيق الأصلي مع إضافة لاحقة يتم عبر `SaveOptions`.  

#### الخطوة 3: تكوين خيارات الحفظ
`SaveOptions` يتيح لك الحفاظ على نوع ملف المصدر، تحديد لاحقة، والتحكم في استخدام الذاكرة.  
```csharp
var saveOptions = new SaveOptions() 
{
    AddSuffix = true,                  // Adds a suffix like "2023-10-12" to indicate modification.
    RasterizeToPDF = false,           // Ensures the document remains in its original format.
    RedactedFileSuffix = DateTime.Now.ToShortDateString()
};
```  

#### الخطوة 4: الحفظ والإخراج
استدعِ طريقة `Save` مع الخيارات المكوّنة لكتابة الملف الممحو إلى القرص:  
```csharp
var outputFile = redactor.Save(saveOptions);
Console.WriteLine($"\nSource document was redacted successfully.\nFile saved to {outputFile}.\n");
```  

### كيفية حفظ مستند ممحو مع الحفاظ على تنسيقه الأصلي؟
حمّل ملف المصدر باستخدام `new Redactor("source.pdf")`، طبّق عملية أو أكثر من عمليات الحذف، قم بتكوين `SaveOptions` للحفاظ على التنسيق الأصلي وإضافة لاحقة (مثلاً، “_redacted”)، ثم استدعِ `redactor.Save("output.pdf", saveOptions)`. يضمن هذا التدفق خطوة واحدة أن المخرجات تحتفظ بنفس التخطيط، الخطوط، والبيانات الوصفية لملف الإدخال، بينما يتم إزالة المحتوى الممحو بشكل دائم.

### المشكلات الشائعة والحلول
- **المستند لا يتم تحميله** – تحقق من مسار الملف وتأكد من أن العملية لديها أذونات القراءة.  
- **فشل الحذف** – تحقق مرة أخرى من تهجئة العبارة الدقيقة وحساسية الحالة؛ استخدم `IgnoreCase = true` إذا لزم الأمر.  
- **ملف الإخراج تالف** – تأكد من أن `SaveOptions` يتطابق مع تنسيق المصدر؛ الأنواع غير المتطابقة قد تتلف النتيجة.

## التطبيقات العملية
يبرز GroupDocs.Redaction .NET في الصناعات المنظمة:
1. **إدارة المستندات القانونية** – إزالة أسماء العملاء، أرقام الضمان الاجتماعي، أو أرقام القضايا تلقائيًا قبل مشاركة العقود.  
2. **خصوصية البيانات الصحية** – إخفاء معرفات المرضى في السجلات الطبية للبقاء متوافقًا مع HIPAA.  
3. **التقارير المالية** – إزالة أرقام الحسابات السرية من التقارير ربع السنوية قبل التوزيع.

## اعتبارات الأداء
عند التعامل مع ملفات كبيرة (مئات الميجابايت)، اتبع أفضل الممارسات التالية:
- استخدم أنماط بحث مختصرة لتقليل دورات المعالج.  
- حرّر كائنات `Redactor` فورًا (باستخدام كتلة `using`) لتحرير الموارد غير المُدارة.  
- استفد من `SaveOptions.Streaming = true` للحفاظ على استهلاك الذاكرة منخفضًا.

## الخلاصة
أصبح لديك الآن طريقة كاملة وجاهزة للإنتاج **لحفظ مستند ممحو** بتنسيقه الأصلي باستخدام GroupDocs.Redaction لـ .NET. باتباع الخطوات أعلاه، يمكنك دمج الحذف الآمن في أي سير عمل .NET، مما يضمن الامتثال دون التضحية بدقة المستند. استكشف الميزات المتقدمة مثل الحذف الجماعي، أشكال الحذف المخصصة، والتكامل مع التخزين السحابي لتوسيع حلك أكثر.

## الأسئلة المتكررة

**س: ما هي أنواع الملفات التي يمكن لـ GroupDocs.Redaction التعامل معها؟**  
ج: أكثر من 30 صيغة، بما في ذلك PDF و DOCX و PPTX و XLSX وأنواع الصور الشائعة مثل PNG و JPEG.

**س: هل يمكن معاينة عمليات الحذف قبل الحفظ؟**  
ج: نعم – توفر فئة `Redactor` طريقة `GetRedactions()` التي تُعيد مجموعة يمكنك عرضها في واجهة المستخدم.

**س: هل يمكنني حذف مستندات محمية بكلمة مرور؟**  
ج: بالتأكيد. قدم كلمة المرور عند إنشاء كائن `Redactor` لفتح الملف.

**س: هل تدعم المكتبة .NET Core و .NET 5/6؟**  
ج: نعم – حزمة NuGet متوافقة مع .NET Framework 4.7.2+، .NET Core 3.1+، و .NET 5/6+.

**س: كيف أحصل على ترخيص إنتاج؟**  
ج: اشترِ ترخيصًا عبر موقع GroupDocs؛ ترخيص تجريبي مؤقت متاح للتقييم.

## الموارد
- **الوثائق**: [توثيق GroupDocs Redaction .NET](https://docs.groupdocs.com/redaction/net/)  
- **مرجع API**: [مرجع API](https://reference.groupdocs.com/redaction/net)  
- **التنزيل**: [إصدارات GroupDocs لـ .NET](https://releases.groupdocs.com/redaction/net/)  
- **دعم مجاني**: [منتدى GroupDocs](https://forum.groupdocs.com/c/redaction/33)  
- **ترخيص مؤقت**: [احصل على ترخيص مؤقت](https://purchase.groupdocs.com/temporary-license/)

---

**آخر تحديث:** 2026-07-06  
**تم الاختبار مع:** GroupDocs.Redaction 2.0.0 for .NET  
**المؤلف:** GroupDocs

## دروس ذات صلة
- [دروس حفظ المستندات لـ GroupDocs.Redaction .NET](/redaction/net/document-saving/)  
- [حذف المستندات بأمان في .NET باستخدام التدفقات: دليل لـ GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)  
- [كيفية حفظ المستندات كملفات PDF مُرصّصة باستخدام GroupDocs.Redaction لـ .NET: دليل كامل](/redaction/net/document-saving/groupdocs-redaction-net-rasterized-pdfs/)