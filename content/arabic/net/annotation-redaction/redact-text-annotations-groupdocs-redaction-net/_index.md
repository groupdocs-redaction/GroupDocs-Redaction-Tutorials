---
date: '2026-05-27'
description: تعلم كيفية حذف التعليقات التوضيحية في ملفات PDF باستخدام GroupDocs.Redaction
  for .NET، مع تغطية الإعداد، حذف باستخدام التعبيرات النمطية، ونصائح الأداء.
keywords:
- how to redact annotations
- apply redaction to pdf
- pdf annotation redaction
schemas:
- author: GroupDocs
  dateModified: '2026-05-27'
  description: Learn how to redact annotations in PDFs with GroupDocs.Redaction for
    .NET, covering setup, regex redaction, and performance tips.
  headline: How to Redact Annotations Using GroupDocs.Redaction for .NET
  type: TechArticle
- description: Learn how to redact annotations in PDFs with GroupDocs.Redaction for
    .NET, covering setup, regex redaction, and performance tips.
  name: How to Redact Annotations Using GroupDocs.Redaction for .NET
  steps:
  - name: Create a Redactor instance (definition anchor)
    text: '`Redactor` is the entry point for all redaction operations; you pass the
      source file path to its constructor.'
  - name: Define your regular expression (definition anchor)
    text: '`Regex` is the .NET class that evaluates patterns; you can enable case‑insensitivity
      (`i`) and multi‑line mode (`m`) directly in the pattern. - `(?im...)`: Enables
      case‑insensitivity (`i`) and multi‑line search (`m`).'
  - name: Apply the redaction (definition anchor)
    text: '`AnnotationRedaction` is a specialized rule that scans annotation objects
      and replaces matching text with a black rectangle. **Explanation:** - **Parameters:**
      The regex pattern tells the engine which text to target. - **Return Values:**
      This method modifies the document in place; no return value is'
  - name: Save the redacted document (definition anchor)
    text: '`Redactor.Save` writes the modified file to disk, preserving the original
      format unless you specify otherwise.'
  type: HowTo
- questions:
  - answer: Yes. Open the document with `Redactor(string path, string password)` and
      then apply your redaction rules as usual.
    question: Can I redact annotations in password‑protected PDFs?
  - answer: The API works on a copy in memory; the original file remains unchanged
      until you explicitly call `Save`.
    question: Does GroupDocs.Redaction modify the original file?
  - answer: All standard PDF annotation types—including comments, highlights, and
      sticky notes—are fully supported.
    question: How many annotation types are supported?
  - answer: Use `Redactor.GetRedactedDocument()` to retrieve an in‑memory stream and
      render it in your UI for a quick preview.
    question: Is there a way to preview redactions before saving?
  - answer: The library can handle files up to **2 GB**; larger files should be split
      before processing.
    question: What is the maximum file size I can process?
  type: FAQPage
title: كيفية حذف التعليقات التوضيحية باستخدام GroupDocs.Redaction for .NET
type: docs
url: /ar/net/annotation-redaction/redact-text-annotations-groupdocs-redaction-net/
weight: 1
---

# كيفية حذف التعليقات التوضيحية باستخدام GroupDocs.Redaction لـ .NET

إذا كنت بحاجة إلى **كيفية حذف التعليقات التوضيحية** في ملفات PDF أو Word، فقد وجدت المكان المناسب. يشرح هذا الدليل طريقة تثبيت GroupDocs.Redaction لـ .NET، وتكوين حذف التعليقات التوضيحية القائم على تعبيرات regex، وتحسين الأداء لأحمال العمل الكبيرة. في النهاية، ستتمكن من إخفاء التعليقات الحساسة والملاحظات والبيانات الوصفية الأخرى ببضع أسطر فقط من كود C#.

## إجابات سريعة
- **أي مكتبة تتعامل مع حذف التعليقات التوضيحية؟** GroupDocs.Redaction for .NET.  
- **هل يمكنني استخدام التعبيرات النمطية؟** نعم – الـ API يقبل صsyntax regex كامل لـ .NET.  
- **هل أحتاج إلى ترخيص للتطوير؟** النسخة التجريبية المجانية تعمل للاختبار؛ الترخيص المدفوع مطلوب للإنتاج.  
- **هل هو متوافق مع .NET 6 و .NET Core؟** مدعوم بالكامل على .NET Framework 4.5+، .NET Core 3.1+، و .NET 6+.  
- **ما مدى سرعة الحذف في الملفات الكبيرة؟** الأنماط المحسّنة يمكنها معالجة ملفات PDF مكوّنة من 500 صفحة في أقل من 5 ثوانٍ على خادم عادي.

## ما هو حذف التعليقات التوضيحية؟
حذف التعليقات التوضيحية يزيل أو يغطي بشكل دائم النص الموجود داخل تعليقات المستند، الملاحظات، الملاحظات اللاصقة، وغيرها من كائنات البيانات الوصفية. من خلال محو هذه المعلومات المخفية، تضمن التقنية عدم إمكانية استخراج أو عرض البيانات السرية، حتى عندما يتم توزيع الملف أو فتحه في تطبيقات أخرى، مما يحافظ على الخصوصية والامتثال.

## لماذا تطبيق الحذف على تعليقات PDF التوضيحية؟
يدعم GroupDocs.Redaction **أكثر من 30 تنسيق مستند** ويمكنه معالجة ملفات تصل إلى **2 GB** دون تحميل المحتوى بالكامل في الذاكرة. استخدام محركات regex المدمجة يقلل من وقت المعالجة بنسبة تصل إلى **70 %** مقارنةً بالبحث اليدوي عن السلاسل، مما يجعله مثالياً لتدفقات العمل القانونية أو المالية ذات الحجم الكبير.

## المتطلبات المسبقة

قبل البدء، تأكد من التالي:

- مكتبة **GroupDocs.Redaction** (أحدث نسخة على NuGet).  
- بيئة تشغيل **.NET** متوافقة (Framework 4.5+، .NET Core 3.1+، .NET 5/6).  
- بيئة تطوير متكاملة مثل **Visual Studio 2022** أو **VS Code**.  
- معرفة أساسية بـ C# وإلمام بالتعبيرات النمطية.

## كيفية حذف التعليقات التوضيحية باستخدام GroupDocs.Redaction؟

حمّل المستند المصدر، عرّف نمط regex، طبّق `AnnotationRedaction`، واحفظ النتيجة — كل ذلك في تدفق مختصر من ثلاث خطوات. الأقسام التالية تفصل كل خطوة مع شروحات واضحة والمواضع الدقيقة لكود ستستبدلها بالقيم الخاصة بك.

### الخطوة 1 – تثبيت المكتبة عبر .NET CLI
**الإجابة:** نفّذ `dotnet add package GroupDocs.Redaction` في مجلد المشروع؛ سيقوم CLI بتحميل أحدث حزمة مستقرة وتحديث ملف المشروع تلقائيًا.  

```bash
dotnet add package GroupDocs.Redaction
```

### الخطوة 2 – تثبيت المكتبة عبر Package Manager Console
**الإجابة:** في Package Manager Console داخل Visual Studio، نفّذ `Install-Package GroupDocs.Redaction`؛ سيقوم الأمر بحل الاعتمادات وإضافة المرجع إلى مشروعك.  

```powershell
Install-Package GroupDocs.Redaction
```

### الخطوة 3 – تهيئة Redactor (تعريف المرجع)
فئة `Redactor` هي المحرك الأساسي الذي يحمل المستند ويطبق قواعد الحذف.  

```csharp
using System;
using GroupDocs.Redaction.Redactions;

namespace DocumentRedaction
{
    class Program
    {
        static void Main(string[] args)
        {
            string sourceFile = @"YOUR_DOCUMENT_DIRECTORY\annotated.xlsx"; // Replace with actual document path.
            
            using (Redactor redactor = new Redactor(sourceFile))
            {
                // Your redaction logic will go here.
            }
        }
    }
}
```

## تطبيق حذف التعليقات التوضيحية

### الخطوة 1: إنشاء مثيل Redactor (تعريف المرجع)
`Redactor` هو نقطة الدخول لجميع عمليات الحذف؛ تمرّر مسار الملف المصدر إلى المُنشئ الخاص به.  

```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // Further processing will occur here.
}
```

### الخطوة 2: تعريف التعبير النمطي الخاص بك (تعريف المرجع)
`Regex` هي الفئة في .NET التي تقيم الأنماط؛ يمكنك تمكين عدم حساسية الحالة (`i`) ووضع متعدد الأسطر (`m`) مباشرةً في النمط.  

```csharp
string pattern = "(?im:john)";
```
- `(?im...)`: يفعّل عدم حساسية الحالة (`i`) والبحث متعدد الأسطر (`m`).

### الخطوة 3: تطبيق الحذف (تعريف المرجع)
`AnnotationRedaction` هي قاعدة متخصصة تقوم بمسح كائنات التعليقات التوضيحية وتستبدل النص المتطابق بمستطيل أسود.  

```csharp
redactor.Apply(new AnnotationRedaction(pattern));
```

**شرح:**  
- **المعلمات:** نمط regex يخبر المحرك بالنص المستهدف.  
- **قيمة الإرجاع:** هذه الطريقة تعدّل المستند في مكانه؛ لا تحتاج إلى قيمة إرجاع.

### الخطوة 4: حفظ المستند المحذوف (تعريف المرجع)
`Redactor.Save` يكتب الملف المعدل إلى القرص، مع الحفاظ على التنسيق الأصلي ما لم تحدد غير ذلك.  

```csharp
guardedRedactor.Save();
```

## المشكلات الشائعة والحلول
- **لم يتم العثور على أي تطابق:** تحقق مرة أخرى من صياغة regex؛ استخدم أداة اختبار عبر الإنترنت بنفس محرك .NET.  
- **أخطاء الوصول إلى الملف:** تأكد من أن التطبيق يمتلك صلاحيات القراءة/الكتابة للمجلدات المصدر والوجهة.  
- **عنق زجاجة في الأداء:** بالنسبة للمستندات التي تتجاوز 500 صفحة، عالجها دفعات متوازية وأعد استخدام مثيل `Redactor` واحد حيثما أمكن.

## الأسئلة المتكررة

**س: هل يمكنني حذف التعليقات التوضيحية في ملفات PDF محمية بكلمة مرور؟**  
ج: نعم. افتح المستند باستخدام `Redactor(string path, string password)` ثم طبّق قواعد الحذف كالمعتاد.

**س: هل يقوم GroupDocs.Redaction بتعديل الملف الأصلي؟**  
ج: الـ API يعمل على نسخة في الذاكرة؛ يبقى الملف الأصلي دون تغيير حتى تقوم باستدعاء `Save` صراحةً.

**س: كم عدد أنواع التعليقات التوضيحية المدعومة؟**  
ج: جميع أنواع التعليقات التوضيحية القياسية في PDF — بما في ذلك التعليقات، التظليل، والملاحظات اللاصقة — مدعومة بالكامل.

**س: هل هناك طريقة لمعاينة الحذف قبل الحفظ؟**  
ج: استخدم `Redactor.GetRedactedDocument()` لاسترجاع تدفق في الذاكرة وعرضه في واجهة المستخدم لمعاينة سريعة.

**س: ما هو الحد الأقصى لحجم الملف الذي يمكن معالجته؟**  
ج: يمكن للمكتبة معالجة ملفات تصل إلى **2 GB**؛ يجب تقسيم الملفات الأكبر قبل المعالجة.

## قسم الأسئلة المتكررة

1. **ما هو GroupDocs.Redaction؟**  
   - إنها مكتبة .NET لحذف المعلومات الحساسة من صيغ المستندات المتنوعة.

2. **كيف أتعامل مع التعليقات التوضيحية المعقدة؟**  
   - استخدم تعبيرات نمطية متقدمة واختبرها بدقة قبل تطبيقها على المستندات الحساسة.

3. **هل يمكن التراجع عن الحذف؟**  
   - بمجرد الحفظ، تصبح التغييرات دائمة؛ احرص دائمًا على عمل نسخة احتياطية من ملفاتك الأصلية.

4. **هل يمكن دمج GroupDocs.Redaction في التطبيقات الحالية؟**  
   - نعم، يتيح الـ API دمجًا سلسًا مع الأنظمة الأخرى المبنية على .NET.

5. **ما الصيغ التي يدعمها GroupDocs.Redaction؟**  
   - يدعم مجموعة واسعة من أنواع المستندات بما في ذلك Word، PDF، Excel، وأكثر.

## الموارد

- [توثيق GroupDocs Redaction](https://docs.groupdocs.com/redaction/net/)
- [مرجع API](https://reference.groupdocs.com/redaction/net)
- [تحميل GroupDocs.Redaction](https://releases.groupdocs.com/redaction/net/)
- [منتدى الدعم المجاني](https://forum.groupdocs.com/c/redaction/33)
- [الحصول على ترخيص مؤقت](https://purchase.groupdocs.com/temporary-license/) 

---

**آخر تحديث:** 2026-05-27  
**تم الاختبار مع:** GroupDocs.Redaction 23.10 لـ .NET  
**المؤلف:** GroupDocs

## دروس ذات صلة

- [إزالة التعليقات التوضيحية من المستندات بفعالية باستخدام GroupDocs.Redaction لـ .NET](/redaction/net/annotation-redaction/remove-annotations-groupdocs-redaction-net/)
- [دروس حذف التعليقات التوضيحية لـ GroupDocs.Redaction .NET](/redaction/net/annotation-redaction/)
- [كيفية تحميل وحذف المستندات باستخدام GroupDocs.Redaction .NET: دليل كامل](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)