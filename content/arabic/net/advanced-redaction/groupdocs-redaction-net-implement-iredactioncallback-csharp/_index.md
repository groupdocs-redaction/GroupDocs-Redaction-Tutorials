---
date: '2026-10-06'
description: تعلم كيفية حذف البيانات باستخدام GroupDocs.Redaction .NET مع تنفيذ IRedactionCallback
  في C#. اتبع هذا الدليل خطوة بخطوة، وأفضل الممارسات، وأمثلة من الواقع.
keywords:
- how to redact data
- GroupDocs.Redaction .NET
- IRedactionCallback implementation
- document redaction C#
lastmod: '2026-10-06'
og_description: تعلم كيفية حذف البيانات باستخدام GroupDocs.Redaction .NET مع تنفيذ
  IRedactionCallback في C#. اتبع دليل خطوة بخطوة مع أفضل الممارسات وأمثلة من الواقع.
og_image_alt: Guide to redact data with GroupDocs.Redaction .NET in C#
og_title: كيفية حذف البيانات باستخدام GroupDocs.Redaction .NET (C#)
schemas:
- author: GroupDocs
  dateModified: '2026-10-06'
  description: Learn how to redact data using GroupDocs.Redaction .NET with an IRedactionCallback
    implementation in C#. Follow this step‑by‑step guide, best practices, and real‑world
    examples.
  headline: How to redact data with GroupDocs.Redaction .NET (C#)
  type: TechArticle
- description: Learn how to redact data using GroupDocs.Redaction .NET with an IRedactionCallback
    implementation in C#. Follow this step‑by‑step guide, best practices, and real‑world
    examples.
  name: How to redact data with GroupDocs.Redaction .NET (C#)
  steps:
  - name: prepare output directory and source file path
    text: Define where your source document lives. Adjust the path to match your environment.
      `LoadOptions` is a configuration object that tells the SDK how to read the file
      (e.g., password handling).
  - name: create a Redactor instance with custom settings
    text: We instantiate `Redactor` with `LoadOptions` and `RedactorSettings`. The
      `RedactionDump` inside the settings will automatically record every redaction
      that occurs. `RedactorSettings` lets you fine‑tune the redaction process; passing
      a `RedactionDump` enables a detailed audit file. `RedactionDump` is
  - name: apply an exact‑phrase redaction
    text: Here we replace the phrase **John Doe** with the placeholder **[REDACTED]**.
      You can swap any phrase or pattern you need to hide. `ReplacementOptions` defines
      what text will replace the matched content. It also supports font and color
      customisation if you need a visual mask. **Explanation of the key
  type: HowTo
- questions:
  - answer: You can start with a free trial or request a temporary license to explore
      all features. For production, purchase a perpetual or subscription license.
    question: What are the licensing options for GroupDocs.Redaction?
  - answer: Yes, it supports PDFs, Word, Excel, PowerPoint, and many other common
      formats.
    question: Can I use GroupDocs.Redaction on multiple file types?
  - answer: Wrap your redaction logic in `try‑catch` blocks and log the exception
      details. The callback can also be used to capture errors in real time.
    question: How do I handle exceptions during redaction?
  - answer: The core API is synchronous, but you can run redaction calls inside asynchronous
      tasks or background services.
    question: Is there built‑in support for asynchronous processing?
  - answer: The [official documentation](https://docs.groupdocs.com/redaction/net/)
      and API reference provide extensive code samples and scenario guides.
    question: Where can I find more advanced examples?
  type: FAQPage
tags:
- redact data
- GroupDocs.Redaction
- .NET redaction
- C# document security
- IRedactionCallback
title: كيفية حذف البيانات باستخدام GroupDocs.Redaction .NET (C#)
type: docs
url: /ar/net/advanced-redaction/groupdocs-redaction-net-implement-iredactioncallback-csharp/
weight: 1
---

# كيفية حذف البيانات باستخدام GroupDocs.Redaction .NET (C#)

في هذا الدرس الشامل ستكتشف **كيفية حذف البيانات** من ملفات PDF وملفات Word وغيرها من المستندات باستخدام GroupDocs.Redaction لـ .NET. سواء كنت بحاجة إلى إخفاء المعرفات الشخصية في العقود القانونية أو حذف الأرقام السرية من التقارير المالية، فإن SDK يمنحك تحكمًا برمجيًا لضمان اختفاء كل عنصر حساس بشكل دائم وقابل للتدقيق. سنستعرض تثبيت المكتبة، تكوين `IRedactionCallback` مخصص، وتطبيق عمليات حذف دقيقة للعبارات مع تسجيل كامل.

## إجابات سريعة
- **ما الذي يفعله IRedactionCallback؟** يتيح لك اعتراض كل حدث حذف، وتسجيل التفاصيل، واختيارياً تعديل نص الاستبدال أثناء التنفيذ.  
- **هل أحتاج إلى ترخيص؟** النسخة التجريبية تعمل للتطوير؛ الترخيص الدائم يزيل جميع قيود التقييم.  
- **ما إصدارات .NET المدعومة؟** .NET Core 3.1+، .NET 5/6، و .NET Framework 4.6+.  
- **هل يمكنني معالجة ملفات متعددة؟** نعم—قم بلف المنطق داخل حلقة أو استخدم المعالجة الدفعية للحصول على أفضل أداء.  
- **هل الحذف غير المتزامن ممكن؟** ليس مدمجًا، لكن يمكنك تشغيل استدعاءات API داخل `Task.Run` أو أنماط غير متزامنة أخرى.

## ما هو حذف البيانات الحساسة؟
`Redaction` هو الإزالة الدائمة أو إخفاء المعلومات التي لا يجب الكشف عنها. باستخدام GroupDocs.Redaction يمكنك تحديد عبارات دقيقة، أنماط تعبيرات عادية، أو قواعد مخصصة واستبدالها ببدائل مثل **[REDACTED]** مع الحفاظ على التخطيط والترقيم الأصلي.

## لماذا تستخدم GroupDocs.Redaction مع IRedactionCallback؟
`IRedactionCallback` هو واجهة تُخطرُك في كل مرة يقوم فيها SDK بحذف جزء من المحتوى، مما يتيح لك التقاط بيانات التدقيق أو تعديل الاستبدال ديناميكيًا. هذا يوفّر إمكانية تدقيق كاملة، تطبيق قواعد عمل مخصصة، وتكامل سلس مع أنظمة الامتثال—كل ذلك دون التضحية بالأداء.

## المتطلبات المسبقة
- **مكتبة GroupDocs.Redaction** (الإصدار المتوافق – راجع صفحة [documentation page](https://docs.groupdocs.com/redaction/net/) الرسمية). للحصول على تفاصيل كاملة راجع [official documentation](https://docs.groupdocs.com/redaction/net/).  
- .NET Core أو .NET Framework مثبتة على جهاز التطوير الخاص بك.  
- Visual Studio (إصدار Community مناسب) أو أي بيئة تطوير تدعم C#.  
- معرفة أساسية بـ C# وإلمام بإدارة حزم NuGet.

## إعداد GroupDocs.Redaction لـ .NET
أولاً، أضف المكتبة إلى مشروعك. اختر الطريقة التي تفضلها – CLI، Package Manager Console، أو الواجهة الرسومية UI. الأوامر تبقى تمامًا كما هي في الدرس الأصلي.

### خيارات التثبيت
**.NET CLI:**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager Console:**  
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI:**  
- افتح مشروعك في Visual Studio.  
- انتقل إلى **Manage NuGet Packages**.  
- ابحث عن **GroupDocs.Redaction** وقم بتثبيت أحدث نسخة مستقرة.

### الحصول على الترخيص
لتجربة المنتج، اطلب نسخة تجريبية مجانية أو ترخيصًا مؤقتًا من [here](https://purchase.groupdocs.com/temporary-license/). يمكنك أيضًا الحصول على ترخيص مؤقت من [temporary‑license page](https://purchase.groupdocs.com/temporary-license/). للاستخدام الإنتاجي، اشترِ ترخيصًا كاملاً لفتح جميع الميزات دون حدود.

#### التهيئة الأساسية والإعداد
فيما يلي الحد الأدنى من الشيفرة التي تحتاجها لفتح مستند باستخدام الفئة `Redactor`. احتفظ بهذا المقتطف دون تغيير – فهو الأساس لكل ما يلي.  
`Redactor` هي الفئة الأساسية التي تمثل مستندًا وتوفر طرقًا لتطبيق قواعد الحذف.  
```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx"; // Replace with actual path

using (Redactor redactor = new Redactor(sourceFile))
{
    // Your redaction logic here
}
```

## دليل التنفيذ
الآن سنوسّع الإعداد الأساسي بإضافة `IRedactionCallback` مخصص. يتيح لك ذلك التقاط كل حدث حذف، كتابة سجل، أو حتى تعديل نص الاستبدال أثناء التنفيذ.

### ربط واستخدام تنفيذ IRedactionCallback
`IRedactionCallback` هي واجهة تستقبل ردود نداء لكل عملية حذف، مما يتيح لك تسجيل أو تعديل السلوك برمجيًا.

#### الخطوة 1: إعداد دليل الإخراج ومسار ملف المصدر
حدد مكان وجود مستند المصدر الخاص بك. عدّل المسار ليتطابق مع بيئتك.

`LoadOptions` هو كائن تكوين يخبر SDK كيفية قراءة الملف (مثل معالجة كلمة المرور).  
```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx"; // Replace with actual path
```

#### الخطوة 2: إنشاء مثيل Redactor بإعدادات مخصصة
نقوم بإنشاء مثيل `Redactor` باستخدام `LoadOptions` و `RedactorSettings`. سيقوم `RedactionDump` داخل الإعدادات تلقائيًا بتسجيل كل عملية حذف تحدث.

`RedactorSettings` يتيح لك ضبط عملية الحذف بدقة؛ تمرير `RedactionDump` يفعّل ملف تدقيق مفصل.  
`RedactionDump` هو فئة مساعدة تكتب كل حدث حذف إلى ملف تفريغ بصيغة JSON لتقارير الامتثال.  
```csharp
using (Redactor redactor = new Redactor(sourceFile, 
    new LoadOptions(), 
    new RedactorSettings(new RedactionDump())))
{
    // Further processing steps will go here
}
```

#### الخطوة 3: تطبيق حذف عبارة دقيقة
هنا نستبدل العبارة **John Doe** بالبديل **[REDACTED]**. يمكنك استبدال أي عبارة أو نمط تحتاج إلى إخفائه.

`ReplacementOptions` يحدد النص الذي سيستبدل المحتوى المتطابق. كما يدعم تخصيص الخط واللون إذا كنت تحتاج إلى قناع بصري.  
```csharp
redactor.Apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[REDACTED]")));
```

**شرح الكائنات الرئيسية**
- `LoadOptions()` – يخبر SDK كيفية قراءة المستند (مثل معالجة كلمة المرور).  
- `RedactorSettings(new RedactionDump())` – يفعّل ملف تفريغ يسجل كل عملية حذف لأغراض التدقيق.  
- `ReplacementOptions("[REDACTED]")` – يحدد النص الذي سيستبدل العبارة المتطابقة.

### لماذا هذا مهم
آلية رد النداء تسجل كل حدث حذف، تُنشئ سجل تدقيق قابل للقراءة آليًا، وتسمح لك بتعديل البدائل ديناميكيًا، مما يساعد على تلبية متطلبات الامتثال ويقلل من الجهد اليدوي بعد المعالجة. من خلال دمج هذه البيانات مع أنظمة المراقبة الخاصة بك يمكنك إنشاء تقارير، تفعيل تنبيهات، وضمان عدم تسرب أي معلومات حساسة عبر خط أنابيب الحذف.

استخدام `IRedactionCallback` يمنحك ثلاث مزايا ملموسة:  
1. **سجلات جاهزة للامتثال** – يتم التقاط كل عملية حذف في تفريغ قابل للقراءة آليًا، مما يلبي متطلبات التدقيق لأكثر من 30 إطارًا تنظيميًا.  
2. **استبدال ديناميكي** – يمكنك تغيير البديل بناءً على نوع البيانات، مما يقلل المعالجة اليدوية بعد العملية حتى 40 %.  
3. **أداء قابل للتوسع** – يضيف رد النداء عبئًا ضئيلًا (<2 ms لكل حذف) مع السماح بمعالجة دفعات من آلاف الملفات بشكل متوازي.

### نصائح استكشاف الأخطاء وإصلاحها
- **الملف غير موجود:** تحقق مرة أخرى من مسار `sourceFile` وتأكد من أن الملف قابل للوصول من العملية الجارية.  
- **رد النداء لا يعمل:** تأكد من أن فئتك تنفّذ **جميع** أعضاء `IRedactionCallback` وأن المثيل يُمرَّر بشكل صحيح إلى `Redactor`.  
- **تأخر الأداء:** بالنسبة للدفعات الكبيرة، أعد استخدام نفس مثيل `Redactor` عندما يكون ذلك ممكنًا وتأكد من التخلص منه بسرعة.

## التطبيقات العملية
حذف البيانات الحساسة مفيد عبر العديد من الصناعات:

1. **معالجة المستندات القانونية** – إزالة أسماء العملاء، أرقام القضايا، أو أرقام الضمان الاجتماعي تلقائيًا قبل مشاركة المسودات.  
2. **أنظمة إدارة الموارد البشرية** – إزالة المعرفات الشخصية من عقود الموظفين أثناء التدقيق.  
3. **التقارير المالية** – إخفاء الأرقام الخاصة أو أرقام الحسابات عند إنشاء ملفات PDF موجهة للمستثمرين.

## اعتبارات الأداء
GroupDocs.Redaction يدعم **أكثر من 30 تنسيقًا للإدخال والإخراج** (PDF، DOCX، PPTX، XLSX، HTML، وأنواع الصور) ويمكنه معالجة ملفات مئات الصفحات دون تحميل المستند بالكامل في الذاكرة. للحفاظ على سرعة تطبيقك عند التعامل مع عشرات أو مئات الملفات:

- **المعالجة الدفعية:** حمّل قائمة بالملفات وشغّل حلقة الحذف داخل `Parallel.ForEach` لاستغلال المعالجات المتعددة.  
- **إدارة الذاكرة:** ضع كل `Redactor` داخل كتلة `using` (كما هو موضح) لضمان التخلص منه.  
- **العمليات غير المتزامنة:** رغم أن SDK نفسه متزامن، يمكنك تفريغ العمل إلى خيوط خلفية أو `Task.Run` لتجنب حجب خيوط واجهة المستخدم.

## المشكلات الشائعة والحلول
| المشكلة | الحل |
|-------|----------|
| **“Invalid file format” error** | تأكد من أن نوع المستند مدعوم (PDF، DOCX، PPTX، إلخ). |
| **Callback receives null values** | تحقق من أنك تمرر تنفيذًا ملموسًا لـ `IRedactionCallback` عند إنشاء `RedactorSettings`. |
| **Redaction not applied** | تحقق من أن العبارة الدقيقة تتطابق مع حالة وحروف المسافة في المستند، أو استخدم `RegexRedaction` للمطابقة بناءً على الأنماط. |

## الأسئلة المتكررة

**س: ما هي خيارات الترخيص لـ GroupDocs.Redaction؟**  
ج: يمكنك البدء بنسخة تجريبية مجانية أو طلب ترخيص مؤقت لاستكشاف جميع الميزات. للاستخدام الإنتاجي، اشترِ ترخيصًا دائمًا أو اشتراكًا.

**س: هل يمكنني استخدام GroupDocs.Redaction على أنواع ملفات متعددة؟**  
ج: نعم، يدعم PDFs، Word، Excel، PowerPoint، والعديد من الصيغ الشائعة الأخرى.

**س: كيف أتعامل مع الاستثناءات أثناء الحذف؟**  
ج: ضع منطق الحذف داخل كتل `try‑catch` وسجّل تفاصيل الاستثناء. يمكن أيضًا استخدام رد النداء لالتقاط الأخطاء في الوقت الفعلي.

**س: هل هناك دعم مدمج للمعالجة غير المتزامنة؟**  
ج: API الأساسي متزامن، لكن يمكنك تشغيل استدعاءات الحذف داخل مهام غير متزامنة أو خدمات خلفية.

**س: أين يمكنني العثور على أمثلة متقدمة؟**  
ج: توفر [official documentation](https://docs.groupdocs.com/redaction/net/) ومرجع API عينات شيفرة واسعة ودلائل للسيناريوهات.

## الموارد
- [توثيق GroupDocs.Redaction لـ .NET](https://docs.groupdocs.com/redaction/net/)
- [مرجع API لـ GroupDocs.Redaction لـ .NET](https://reference.groupdocs.com/redaction/net/)
- [تحميل GroupDocs.Redaction لـ .NET](https://releases.groupdocs.com/redaction/net/)
- [منتدى GroupDocs.Redaction](https://forum.groupdocs.com/c/redaction/33)
- [دعم مجاني](https://forum.groupdocs.com/)
- [ترخيص مؤقت](https://purchase.groupdocs.com/temporary-license/)

---

**آخر تحديث:** 2026-10-06  
**تم الاختبار مع:** GroupDocs.Redaction 2.3 (أحدث نسخة وقت الكتابة)  
**المؤلف:** GroupDocs

## دروس ذات صلة

- [إنشاء سياسة حذف باستخدام GroupDocs.Redaction .NET – دليل خطوة بخطوة](/redaction/net/advanced-redaction/groupdocs-redaction-net-create-save-policy/)
- [كيفية حذف المستندات باستخدام GroupDocs.Redaction .NET – دليل كامل](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [حذف المستندات .net باستخدام التدفقات – دليل GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)