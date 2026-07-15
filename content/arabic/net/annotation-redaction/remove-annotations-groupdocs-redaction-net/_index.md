---
date: '2026-06-01'
description: تعلم كيفية إخفاء المعلومات الحساسة وكيفية إزالة التعليقات من المستندات
  باستخدام GroupDocs.Redaction for .NET، مع ضمان الامتثال وخصوصية البيانات.
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
title: كيفية إخفاء المعلومات الحساسة وإزالة التعليقات باستخدام GroupDocs.Redaction
  for .NET
type: docs
url: /ar/net/annotation-redaction/remove-annotations-groupdocs-redaction-net/
weight: 1
---

# إزالة المعلومات الحساسة وإزالة التعليقات التوضيحية باستخدام GroupDocs.Redaction لـ .NET

إدارة البيانات السرية في المستندات تمثل تحديًا يوميًا للمطورين والمدققين والفرق القانونية. **Redact sensitive information** بسرعة وبشكل موثوق باستخدام GroupDocs.Redaction لـ .NET، وهي مكتبة تعمل عبر أكثر من 30 تنسيق ملف ويمكنها التعامل مع ملفات تصل إلى 2 GB دون تحميل المستند بالكامل في الذاكرة. يشرح هذا البرنامج التعليمي سير العمل الكامل — من تثبيت الحزمة إلى إزالة التعليقات التوضيحية المحددة باستخدام التعابير النمطية — حتى تتمكن من حماية البيانات الشخصية والبقاء متوافقًا مع اللوائح مثل GDPR و HIPAA.

## إجابات سريعة
- **ماذا يفعل GroupDocs.Redaction؟** يقوم بإزالة أو إخفاء النصوص والصور والتعليقات التوضيحية برمجيًا لحماية البيانات الخاصة.  
- **ما أنواع الملفات المدعومة؟** أكثر من 30 تنسيقًا، بما في ذلك PDF و DOCX و XLSX و PPTX وملفات الصور.  
- **هل أحتاج إلى ترخيص للتطوير؟** نسخة تجريبية مجانية تعمل للاختبار؛ يلزم ترخيص دائم للإنتاج.  
- **هل يمكنني معالجة الملفات الكبيرة بكفاءة؟** نعم — المعالجة الدفعية والبث يقللان من استهلاك الذاكرة للمستندات التي تتضمن مئات الصفحات.  
- **هل هو متوافق مع .NET 6 و .NET Core؟** مدعوم بالكامل على .NET Framework 4.5+، .NET Core 3.1+، .NET 5+، و .NET 6+.

## ما هو “redact sensitive information”؟
*Redact sensitive information* يعني إزالة أو إخفاء البيانات الشخصية أو السرية من المستند بشكل دائم بحيث لا يمكن استعادتها. يشمل ذلك الأسماء، أرقام الهوية، التفاصيل المالية، أو أي بيانات أخرى قد تحدد هوية فرد. يضمن تنفيذ الإزالة الالتزام باللوائح مثل GDPR و HIPAA و CCPA، ويمنع تسرب البيانات، ويسمح بمشاركة المستندات بأمان مع الأطراف الخارجية.

## لماذا تستخدم GroupDocs.Redaction لـ .NET؟
GroupDocs.Redaction يقدم **quantified benefits**: يدعم أكثر من 30 تنسيق إدخال وإخراج، يعالج المستندات حتى حجم 2 GB دون تحميل كامل المستند، ويمكنه إزالة ما يصل إلى 10 000 تعليق توضيحي في الدقيقة على خادم قياسي. تجعل هذه الأرقام منه أحد أكثر محركات الإزالة كفاءة وتنوعًا في السوق.

## المتطلبات المسبقة
قبل البدء، تأكد من أن لديك ما يلي:

- **GroupDocs.Redaction for .NET** (الإصدار 20.7 أو أحدث).  
- Visual Studio 2022 أو أي بيئة تطوير متكاملة متوافقة.  
- معرفة أساسية بـ C# وإلمام بالتعابير النمطية.  

### المكتبات المطلوبة
- **GroupDocs.Redaction for .NET** – تثبيت عبر NuGet (انظر قسم التثبيت).

### متطلبات إعداد البيئة
- .NET Framework 4.5+ **or** .NET Core 3.1+.  
- الوصول إلى نظام الملفات حيث توجد المستندات المصدر.

## التثبيت – كيفية إزالة التعليقات التوضيحية (الخطوة 1)
يمكنك إضافة المكتبة إلى مشروعك باستخدام أي من الأوامر التالية. لا يتم إضافة كتل شفرة للحفاظ على البرنامج التعليمي خاليًا من الشيفرة.

**.NET CLI:**  
شغّل `dotnet add package GroupDocs.Redaction --version 20.7.*` في الطرفية.

**Package Manager Console:**  
نفّذ `Install-Package GroupDocs.Redaction -Version 20.7.*`.

**NuGet Package Manager UI:**  
ابحث عن “GroupDocs.Redaction” وانقر **Install**.

### الحصول على الترخيص
لإلغاء قفل الوظائف الكاملة، احصل على ترخيص تجريبي أو مؤقت من [GroupDocs](https://purchase.groupdocs.com/temporary-license/). للاستخدام في الإنتاج، اشترِ ترخيصًا دائمًا عبر نفس البوابة.

## دليل التنفيذ – كيفية إزالة التعليقات التوضيحية باستخدام التعابير النمطية
### نظرة عامة
يشرح هذا القسم كيفية **how to remove annotations** التي تتطابق مع نمط محدد — مثالي لإزالة أسماء الموظفين، الملاحظات السرية، أو أي علامة مخصصة.

### الخطوة 1: إعداد مسارات ملف المصدر والإخراج
أولاً، حدد مواقع مستند الإدخال والمجلد الذي سيُحفظ فيه الملف المُحَرَّف. تأكد من وجود دليل الإخراج؛ وإلا سيفشل العملية.

*Definition anchor:* `Path.Combine` هي أداة .NET تُدمج بأمان أسماء الأدلة والملفات عبر Windows و Linux و macOS.

### الخطوة 2: تطبيق إزالة باستخدام التعابير النمطية
بعد ذلك، أنشئ قاعدة إزالة تستهدف التعليقات التوضيحية التي تتطابق مع نمط regex الخاص بك.

*Definition anchor:* `Redactor` هو الفئة الرئيسية التي تُحمِّل مستندًا وتطبق قواعد الإزالة.  
*Definition anchor:* `DeleteAnnotationRedaction` هي فئة تُزيل التعليقات التوضيحية التي يطابق محتواها مرشح التعابير النمطية.  
*Definition anchor:* `SaveOptions` يتيح لك التحكم في كيفية كتابة ملف الإخراج — إضافة لاحقة، اختيار تنسيق الإخراج، وتعطيل التحويل إلى نقطية للحفاظ على الملف كمتجه.

**Direct answer:** حمّل المستند المصدر باستخدام `Redactor redactor = new Redactor(sourcePath);`، أضف `DeleteAnnotationRedaction` باستخدام regex الخاص بك، ثم استدعِ `redactor.Save(outputPath, new SaveOptions { Suffix = "_redacted", Rasterize = false });`. هذه العملية ذات السطر الواحد تُزيل التعليقات المتطابقة وتكتب ملفًا جديدًا دون تعديل الأصلي.

### الخطوة 3: تحرير الموارد
دائمًا استدعِ `redactor.Dispose()` أو غلف الكائن داخل كتلة `using` لتحرير الموارد غير المُدارة بسرعة.  
*Definition anchor:* `Dispose` يُحرّر الموارد غير المُدارة المستخدمة بواسطة كائن Redactor، مما يضمن تحرير الذاكرة.

## إعداد مسار الملف لإزالة التعليقات التوضيحية – كيفية إزالة تعليقات Excel
على الرغم من أن المثال يركز على ملفات PDF، فإن النهج نفسه يعمل مع ملفات Excel (`.xlsx`). التعامل السليم مع المسارات يمنع أخطاء “الملف غير موجود”.

*Definition anchor:* `PrepareOutputDirectory` هي طريقة مساعدة تتحقق من وجود المجلد وتُنشئه إذا كان مفقودًا.

من خلال إعادة استخدام الأداة نفسها عبر الصيغ، يمكنك **how to remove annotations** من دفاتر عمل Excel، مستندات Word، أو عروض PowerPoint مع أقل تغييرات في الشيفرة.

## التطبيقات العملية
1. **Data Privacy Compliance** – أتمتة الإزالة لتلبية متطلبات GDPR أو HIPAA أو CCPA عن طريق حذف المعرفات الشخصية.  
2. **Legal Document Preparation** – إزالة التعليقات السرية قبل مشاركة العقود مع الأطراف الخارجية.  
3. **Corporate Data Management** – تنظيف التقارير الداخلية برمجيًا، مع ضمان خروج المعلومات المعتمدة فقط من المؤسسة.

## اعتبارات الأداء – كيفية إزالة التعليقات التوضيحية بكفاءة
- **Efficient Memory Management:** حرّر كائنات `Redactor` بمجرد الانتهاء من معالجة كل ملف.  
- **Batch Processing:** كرّر عبر مجلد من المستندات وطبق قاعدة الإزالة نفسها على كل ملف؛ هذا يقلل من العبء مقارنة بفتح وإغلاق المكتبة بشكل متكرر.  
- **Optimized Regular Expressions:** استخدم مجموعات غير ملتقطة وتجنب الأنماط التي تتطلب تتبع رجوع كثيف. على سبيل المثال، فضل `\bEmployeeID:\s*\d{4,6}\b` على `.*EmployeeID.*` لتسريع المطابقة.

## المشكلات الشائعة والحلول
- **Large Files Stall:** قسّم المستند إلى أقسام أو زد إعداد `MaxMemoryUsage` في `RedactorSettings`.  
- **Regex Not Matching:** تحقق من أن النمط يتضمن العلامة `(?i)` لتجاهل حالة الأحرف، أو اختبره باستخدام أداة اختبار regex على الإنترنت قبل تضمينه.  
- **Output File Overwrites Original:** دائمًا حدد مسار إخراج مختلف أو استخدم `SaveOptions.Suffix` لإضافة “_redacted” تلقائيًا.

## الأسئلة المتكررة (جديدة)

**س: هل يمكن لـ GroupDocs.Redaction إزالة التعليقات التوضيحية في دفاتر عمل Excel؟**  
ج: نعم — بتحميل ملف `.xlsx` باستخدام `Redactor` وتطبيق قاعدة `DeleteAnnotationRedaction`، يمكنك إزالة التعليقات والملاحظات وأنواع التعليقات الأخرى.

**س: كيف أجعل أنماط regex غير حساسة لحالة الأحرف؟**  
ج: أضف البادئة `(?i)` إلى النمط أو استخدم العلامة `RegexOptions.IgnoreCase` عند إنشاء `DeleteAnnotationRedaction`.

**س: هل يمكن تخصيص اسم ملف الإخراج؟**  
ج: بالتأكيد. اضبط `SaveOptions.Prefix` أو `SaveOptions.Suffix` لإضافة نص قبل أو بعد اسم الملف المُولد.

**س: ماذا يحدث للمستند الأصلي بعد الإزالة؟**  
ج: يبقى ملف المصدر دون تعديل؛ يتم حفظ النسخة المُحَرَّفة إلى المسار الذي تحدده في `SaveOptions`.

**س: هل تدعم المكتبة البث للملفات PDF الكبيرة جدًا؟**  
ج: نعم — يمكن لـ GroupDocs.Redaction العمل في وضع البث الذي يعالج الصفحات تسلسليًا، مما يقلل استهلاك الذاكرة بشكل كبير.

## قسم الأسئلة المتكررة
1. **كيف أتعامل مع المستندات الكبيرة بكفاءة؟**  
   - عالج المستندات في أقسام أصغر إذا أمكن، وتأكد من تحسين التعابير النمطية للأداء.  
2. **هل يمكنني استخدام GroupDocs.Redaction مع صيغ ملفات أخرى غير Excel؟**  
   - نعم، يدعم مجموعة متنوعة من الصيغ بما في ذلك PDF و Word وغيرها.  
3. **ماذا يحدث للمستند الأصلي بعد الإزالة؟**  
   - يبقى المستند الأصلي دون تغيير ما لم يتم حفظه فوقه؛ احفظ دائمًا التغييرات في ملف جديد أو نسخة.  
4. **هل يمكن تخصيص اسم ملف الإخراج باستخدام GroupDocs.Redaction؟**  
   - نعم، عدّل `SaveOptions` لتضمين لاحقات أو بادئات مخصصة لأسماء ملفات الإخراج.  
5. **كيف أضمن أن أنماط regex غير حساسة لحالة الأحرف؟**  
   - استخدم معدلات مثل `(i)` في التعابير النمطية لجعلها غير حساسة لحالة الأحرف.

## الموارد
- [التوثيق](https://docs.groupdocs.com/redaction/net/)
- [مرجع API](https://reference.groupdocs.com/redaction/net)
- [تحميل GroupDocs.Redaction](https://releases.groupdocs.com/redaction/net/)
- [منتدى الدعم المجاني](https://forum.groupdocs.com/c/redaction/33)
- [طلب ترخيص مؤقت](https://purchase.groupdocs.com/temporary-license/)

باتباع هذا الدليل، لديك الآن طريقة قوية لـ **redact sensitive information** و **how to remove annotations** من أي نوع مستند مدعوم باستخدام GroupDocs.Redaction لـ .NET. نفّذ الخطوات، اختبرها مع بعض الملفات التجريبية، ودمج المنطق في خط أنابيب معالجة المستندات الأكبر لضمان أقصى مستوى من الأمان.

**آخر تحديث:** 2026-06-01  
**تم الاختبار مع:** GroupDocs.Redaction 20.7 لـ .NET  
**المؤلف:** GroupDocs  

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

## دروس ذات صلة

- [كيفية تحميل وإزالة المستندات باستخدام GroupDocs.Redaction .NET&#58; دليل كامل](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [إزالة وحفظ المستندات باستخدام GroupDocs.Redaction لـ .NET&#58; دليل كامل](/redaction/net/document-saving/redact-save-documents-groupdocs-redaction-net/)
- [إزالة العبارات الدقيقة في مستندات .NET باستخدام GroupDocs.Redaction](/redaction/net/text-redaction/guide-redact-exact-phrases-groupdocs-redaction-dotnet/)