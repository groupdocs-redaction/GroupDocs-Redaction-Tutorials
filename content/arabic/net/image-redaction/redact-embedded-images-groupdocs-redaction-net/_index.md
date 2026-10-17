---
date: '2026-10-16'
description: تعلم كيفية استخدام GroupDocs لإزالة الصور المدمجة في مستندات Word باستخدام
  GroupDocs.Redaction .NET API، مع الحفاظ على سلامة البيانات الحساسة.
keywords:
- how to use groupdocs
- hide pictures word
- redactor word document
- redact images word
- word image masking
lastmod: '2026-10-16'
og_description: كيفية استخدام GroupDocs لإزالة الصور المدمجة في مستندات Word باستخدام
  .NET API. احمِ الصور السرية بسرعة وموثوقية.
og_image_alt: Guide showing GroupDocs.Redaction .NET API redacting images in a Word
  file
og_title: كيفية استخدام GroupDocs لإزالة الصور في Word باستخدام .NET
schemas:
- author: GroupDocs
  dateModified: '2026-10-16'
  description: Learn how to use GroupDocs to redact embedded images in Word documents
    using the GroupDocs.Redaction .NET API, keeping sensitive data safe.
  headline: How to use GroupDocs to redact images in Word with .NET
  type: TechArticle
- description: Learn how to use GroupDocs to redact embedded images in Word documents
    using the GroupDocs.Redaction .NET API, keeping sensitive data safe.
  name: How to use GroupDocs to redact images in Word with .NET
  steps:
  - name: '**Confidential reports:** Redact logos or charts before external distribution.'
    text: '**Confidential reports:** Redact logos or charts before external distribution.'
  - name: '**Legal briefs:** Hide client photographs or scanned IDs that contain personal
      data.'
    text: '**Legal briefs:** Hide client photographs or scanned IDs that contain personal
      data.'
  - name: '**Business contracts:** Mask proprietary diagrams that reveal trade secrets.'
    text: '**Business contracts:** Mask proprietary diagrams that reveal trade secrets.'
  - name: '**Government releases:** Remove sensitive satellite images from public
      PDFs generated from Word.'
    text: '**Government releases:** Remove sensitive satellite images from public
      PDFs generated from Word.'
  type: HowTo
- questions:
  - answer: Yes, iterate over each picture node and call `ImageAreaRedaction` for
      every region you need to hide.
    question: Can I redact multiple pictures in one pass?
  - answer: Absolutely. Provide the password when constructing the `Redactor` object,
      and the library will open the document securely.
    question: Does GroupDocs.Redaction support password‑protected Word files?
  - answer: The API handles DOC, DOCX, RTF, HTML, PDF, and over 20 other formats,
      allowing you to build a universal redaction service.
    question: What file formats can I process besides DOCX?
  - answer: Use a temporary license from the GroupDocs portal; it enables full functionality
      for 30 days without watermarks.
    question: How do I test the redaction without a license?
  - answer: Visit the [GroupDocs Free Support](https://forum.groupdocs.com/c/redaction/33)
      forum for community assistance or contact GroupDocs sales for enterprise support.
    question: Where can I get help if I run into problems?
  type: FAQPage
tags:
- redact images
- GroupDocs.Redaction
- .NET document security
title: كيفية استخدام GroupDocs لإزالة الصور في Word باستخدام .NET
type: docs
url: /ar/net/image-redaction/redact-embedded-images-groupdocs-redaction-net/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام GroupDocs لإزالة الصور في Word باستخدام .NET

عندما تحتاج إلى حماية الصور السرية في ملف Microsoft Word، يصبح **كيفية استخدام GroupDocs** هو السؤال الأول. يشرح هذا البرنامج التعليمي كل خطوة مطلوبة لتحديد، إخفاء، وإزالة الصور المدمجة بشكل دائم بحيث لا تتسرب المعلومات الحساسة.

## إجابات سريعة
- **هل يمكن لـ GroupDocs إزالة جميع الصور تلقائيًا؟** نعم، يمكنك التكرار عبر كل صورة وتطبيق `ImageAreaRedaction`.
- **ما إصدارات .NET المدعومة؟** .NET Framework 4.5+، .NET Core 3.1+، .NET 5/6/7.
- **هل أحتاج إلى ترخيص للتطوير؟** النسخة التجريبية المجانية تعمل للاختبار؛ يلزم ترخيص دائم للإنتاج.
- **هل سيتم الحفاظ على التخطيط الأصلي؟** تحافظ الـ API على النص والتنسيق دون تغيير أثناء إفراغ منطقة الصورة.
- **ما مدى سرعة العملية؟** يمكن لـ GroupDocs.Redaction معالجة مستندات مكوّنة من 200 صفحة في أقل من ثانيتين على خادم عادي.

## ما هو GroupDocs.Redaction؟
GroupDocs.Redaction هي مكتبة .NET تتيح إزالة النصوص، الصور، والبيانات الوصفية برمجيًا عبر أكثر من 20 تنسيق مستند. تقوم بمعالجة الملفات دون الحاجة إلى تثبيت Microsoft Office، مما يجعلها مثالية لأتمتة الخوادم. توفر واجهات برمجة تطبيقات (APIs) لإزالة النصوص، الصور، والبيانات الوصفية، وتدعم المعالجة الدفعية، أنماط الإزالة المخصصة، وتقرير الامتثال.

## لماذا نستخدم GroupDocs لإزالة الصور في Word؟
تدعم المكتبة **أكثر من 20 تنسيق إدخال وإخراج** ويمكنها إزالة الصور في المستندات حتى حجم 500 ميغابايت دون تحميل الملف بالكامل في الذاكرة. يضمن الخوارزمية المدمجة `ImageAreaRedaction` أن المنطقة التي تم إزالتها لا يمكن استعادتها، مما يلتزم بمعايير الامتثال الصارمة.

## المتطلبات المسبقة
- .NET Framework 4.5+ **أو** .NET Core 3.1+ مثبت.
- معرفة أساسية بـ C# وإلمام بهياكل ملفات Word.
- الوصول إلى حزمة NuGet **GroupDocs.Redaction** (نسخة تجريبية مجانية أو مرخصة).

## كيفية إعداد GroupDocs.Redaction لـ .NET

### كيفية تثبيت GroupDocs.Redaction عبر .NET CLI؟
نفّذ الأمر التالي في مجلد المشروع الخاص بك: `dotnet add package GroupDocs.Redaction`. يضيف هذا أحدث إصدار مستقر إلى ملف المشروع.

```bash
dotnet add package GroupDocs.Redaction
```

### كيفية تثبيت GroupDocs.Redaction باستخدام Package Manager؟
نفّذ `Install-Package GroupDocs.Redaction` في وحدة تحكم Package Manager.

```powershell
Install-Package GroupDocs.Redaction
```

### كيفية الحصول على ترخيص مؤقت وتطبيقه؟
يمكنك طلب ترخيص مؤقت من صفحة [رخصة مؤقتة](https://purchase.groupdocs.com/temporary-license/).  
يسمح لك الترخيص المؤقت بتقييم مجموعة الميزات الكاملة دون علامات مائية. بعد الشراء، ضع ملف الترخيص في مشروعك وحمّله كما هو موضح:

```csharp
using GroupDocs.Redaction;
```

## كيفية إزالة الصور المدمجة في مستند Word؟
لإزالة الصور، تقوم بتحميل المستند باستخدام كائن Redactor، وتحديد كل صورة، وتعريف المنطقة التي تريد إخفاءها، وتطبيق ImageAreaRedaction. تقوم الـ API بالكتابة فوق البكسلات المحددة، مما يضمن عدم إمكانية استعادة المحتوى البصري الأصلي، مع الحفاظ على التخطيط والنص المحيط.

### كيفية إعداد مسارات المصدر والإخراج؟
حدد المسارات المطلقة للمستند الأصلي والنتيجة التي تم إزالتها قبل إنشاء أي كائنات.

```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/LOREMIPSUM_PDF";
string outputFile = "YOUR_OUTPUT_DIRECTORY/redacted_output.docx";
```

### كيفية إنشاء وتكوين كائن Redactor؟
Redactor هو الفئة الأساسية التي تقوم بتحميل المستند وتنفيذ عمليات الإزالة.  
أنشئ مثيلًا من `Redactor` باستخدام المستند الخاص بك:

```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // Code for redaction will go here
}
```

### كيفية تحديد الإحداثيات وتطبيق إزالة منطقة الصورة؟
`ImageAreaRedaction` هي طريقة تقوم بإخفاء منطقة مستطيلة من الصورة بلون صلب.  
حدد النقطة العليا اليسرى (`samplePoint`) وحجم (`sampleSize`) المنطقة التي تريد إخفاءها، ثم استدعِ `ImageAreaRedaction`. تقوم هذه الطريقة بالكتابة فوق البكسلات المحددة بلون صلب.

```csharp
Point samplePoint = new Point(516, 311);
Size sampleSize = new Size(170, 35);

RedactorChangeLog result = redactor.Apply(new ImageAreaRedaction(
    samplePoint,
    new RegionReplacementOptions(Color.Blue, sampleSize)
));
```

### كيفية التحقق من نتيجة الإزالة وحفظ الملف؟
بعد استدعاء `Redactor.Apply()`, افحص كائن `Result`. إذا كان `IsSuccess` صحيحًا، اكتب المستند المعدل إلى مسار الإخراج.

```csharp
if (result.Status != RedactionStatus.Failed)
{
    var savedOutputFile = redactor.Save();
    Console.WriteLine($"Redacted document saved as: {savedOutputFile}");
}
```

## المشكلات الشائعة ونصائح استكشاف الأخطاء
- **أخطاء الإحداثيات:** تأكد من أن قيم X/Y داخل حدود الصورة؛ وإلا ستطرح الـ API استثناء `ArgumentOutOfRangeException`.
- **الترخيص مفقود:** تنتهي صلاحية الترخيص التجريبي بعد 30 يومًا؛ استبدله بترخيص دائم لتجنب فشل التشغيل.
- **تنسيق غير مدعوم:** تحقق من أن امتداد الملف من بين أكثر من 20 تنسيقًا المذكورة في الوثائق؛ قد تحتاج ملفات `.doc` القديمة إلى تحويل إلى `.docx` أولاً.

## تطبيقات عملية
1. **تقارير سرية:** إزالة الشعارات أو المخططات قبل التوزيع الخارجي.
2. **مذكرات قانونية:** إخفاء صور العملاء أو بطاقات الهوية الممسوحة التي تحتوي على بيانات شخصية.
3. **عقود تجارية:** إخفاء المخططات المملوكة التي تكشف أسرارًا تجارية.
4. **إصدارات حكومية:** إزالة الصور الفضائية الحساسة من ملفات PDF العامة المولدة من Word.

## اعتبارات الأداء
- عالج المستندات بشكل تسلسلي عند التعامل مع دفعات كبيرة للحفاظ على انخفاض استهلاك الذاكرة.
- استخدم `RedactorOptions` لتحديد عدد الخيوط إذا كنت تعمل على خادم محدود الموارد.
- تخلص من كائن `Redactor` بسرعة باستخدام `using` لتحرير الموارد غير المُدارة.

## الخلاصة
أنت الآن تعرف **كيفية استخدام GroupDocs** لإزالة الصور المدمجة في ملفات Word بشكل موثوق باستخدام API الخاص بـ .NET. باتباع الخطوات أعلاه، يمكنك دمج هذه القدرة في أي خط أنابيب لمعالجة المستندات، مما يضمن أن الصور السرية لا تغادر مؤسستك.  
للتعمق أكثر، جرب أنواع إزالة أخرى (نص، بيانات وصفية) ودمج المكتبة في خدمات الويب، العمال الخلفيين، أو Azure Functions.

## الأسئلة الشائعة

**س: هل يمكنني إزالة عدة صور في عملية واحدة؟**  
ج: نعم، قم بالتكرار عبر كل عقدة صورة واستدعِ `ImageAreaRedaction` لكل منطقة تحتاج إلى إخفائها.

**س: هل يدعم GroupDocs.Redaction ملفات Word المحمية بكلمة مرور؟**  
ج: بالتأكيد. قدم كلمة المرور عند إنشاء كائن `Redactor`، وستفتح المكتبة المستند بأمان.

**س: ما هي صيغ الملفات التي يمكنني معالجتها بخلاف DOCX؟**  
ج: تتعامل الـ API مع DOC، DOCX، RTF، HTML، PDF، وأكثر من 20 صيغة أخرى، مما يتيح لك بناء خدمة إزالة شاملة.

**س: كيف يمكنني اختبار الإزالة دون ترخيص؟**  
ج: استخدم ترخيصًا مؤقتًا من بوابة GroupDocs؛ يتيح لك ذلك جميع الوظائف لمدة 30 يومًا دون علامات مائية.

**س: أين يمكنني الحصول على المساعدة إذا واجهت مشاكل؟**  
ج: زر منتدى [دعم GroupDocs المجاني](https://forum.groupdocs.com/c/redaction/33) للحصول على مساعدة المجتمع أو تواصل مع مبيعات GroupDocs للحصول على دعم مؤسسي.

## موارد إضافية
- **الوثائق:** [وثائق GroupDocs Redaction](https://docs.groupdocs.com/redaction/net/)
- **مرجع API:** [مرجع API لـ GroupDocs](https://reference.groupdocs.com/redaction/net)
- **التنزيل:** [الإصدارات الأخيرة](https://releases.groupdocs.com/redaction/net/)

---

**آخر تحديث:** 2026-10-16  
**تم الاختبار مع:** GroupDocs.Redaction 23.12 لـ .NET  
**المؤلف:** GroupDocs

## دروس ذات صلة
- [كيفية إزالة المستندات باستخدام GroupDocs.Redaction .NET – دليل كامل](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [إزالة وحفظ المستندات باستخدام GroupDocs Redaction Net](/redaction/net/document-saving/redact-save-documents-groupdocs-redaction-net/)
- [إتقان إزالة العبارات الدقيقة حساسة لحالة الأحرف باستخدام GroupDocs.Redaction .NET لأمان المستندات](/redaction/net/text-redaction/groupdocs-redaction-net-case-sensitive-exact-phrase-redaction/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}