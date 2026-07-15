---
date: '2026-03-30'
description: تعلم كيفية إخفاء البيانات الحساسة باستخدام GroupDocs.Redaction .NET مع
  تنفيذ IRedactionCallback في C#. دليل خطوة‑بخطوة، أفضل الممارسات، وأمثلة من الواقع.
keywords:
- GroupDocs.Redaction .NET
- Implementing IRedactionCallback
- secure document redaction
title: إزالة البيانات الحساسة باستخدام GroupDocs.Redaction .NET (C#)
type: docs
url: /ar/net/advanced-redaction/groupdocs-redaction-net-implement-iredactioncallback-csharp/
weight: 1
---

# حذف البيانات الحساسة باستخدام GroupDocs.Redaction .NET (C#)

في المشهد الرقمي اليوم، **حذف البيانات الحساسة** من المستندات القانونية أو المالية أو الموارد البشرية هو مطلب غير قابل للتفاوض. سواء كنت تُعد عقدًا للمراجعة الخارجية أو تُنقِّي تقريرًا قبل إصداره للجمهور، فإن فقدان معرف شخصي واحد يمكن أن يؤدي إلى خروقات في الامتثال. يمنحك GroupDocs.Redaction لـ .NET طريقة برمجية قوية لضمان اختفاء كل قطعة من المعلومات السرية بالضبط كما تحتاج. في هذا البرنامج التعليمي سنستعرض ربط تنفيذ `IRedactionCallback`، لتتمكن من تخصيص سير عمل الحذف والحفاظ على التحكم الكامل في كل خطوة.

## إجابات سريعة
- **ما الذي يفعله IRedactionCallback؟** يتيح لك اعتراض أحداث الحذف، تسجيلها، أو تعديل السلوك أثناء التنفيذ.  
- **هل أحتاج إلى ترخيص؟** النسخة التجريبية تعمل للتطوير؛ الترخيص الدائم يزيل جميع حدود التقييم.  
- **ما إصدارات .NET المدعومة؟** .NET Core 3.1+، .NET 5/6، و .NET Framework 4.6+.  
- **هل يمكنني معالجة ملفات متعددة؟** نعم—قم بلف المنطق داخل حلقة أو استخدم المعالجة الدفعية لأفضل أداء.  
- **هل الحذف غير المتزامن ممكن؟** غير مدمج، لكن يمكنك تشغيل استدعاءات API داخل `Task.Run` أو أنماط async أخرى.

## ما هو حذف البيانات الحساسة؟
الحذف هو عملية إزالة أو إخفاء المعلومات بشكل دائم التي لا يجب كشفها. باستخدام GroupDocs.Redaction، يمكنك تحديد عبارات دقيقة، أنماط، أو قواعد مخصصة واستبدالها بعلامات نائبة (مثل **[REDACTED]**) مع الحفاظ على تخطيط المستند الأصلي.

## لماذا تستخدم GroupDocs.Redaction مع IRedactionCallback؟
- **قابلية التدقيق الكاملة:** يمنحك الـ callback سجلًا مفصلاً لكل عملية حذف تم تنفيذها.  
- **معالجة مخصصة:** استبدل النص، شغّل خدمات خارجية، أو فرض قواعد الأعمال ديناميكيًا.  
- **أداء قابل للتوسع:** اجمع بين الـ callbacks والمعالجة الدفعية للتعامل مع آلاف الملفات بكفاءة.

## المتطلبات المسبقة
قبل أن نبدأ، تأكد من وجود ما يلي:

- مكتبة **GroupDocs.Redaction** (الإصدار المتوافق – راجع صفحة [documentation page](https://docs.groupdocs.com/redaction/net/) الرسمية).  
- .NET Core أو .NET Framework مثبت على جهاز التطوير الخاص بك.  
- Visual Studio (الإصدار المجتمعي يكفي) أو أي بيئة تطوير تدعم C#.  
- معرفة أساسية بـ C# وإلمام بإدارة حزم NuGet.

## إعداد GroupDocs.Redaction لـ .NET
أولاً، أضف المكتبة إلى مشروعك. اختر الطريقة التي تفضّلها – سطر الأوامر CLI، Package Manager Console، أو الواجهة الرسومية UI. الأوامر تبقى كما هي في البرنامج التعليمي الأصلي.

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
لتجربة المنتج، اطلب نسخة تجريبية مجانية أو ترخيصًا مؤقتًا من [here](https://purchase.groupdocs.com/temporary-license/). للاستخدام الإنتاجي، اشترِ ترخيصًا كاملًا لفتح جميع المميزات دون حدود.

#### التهيئة الأساسية والإعداد
فيما يلي الحد الأدنى من الشيفرة التي تحتاجها لفتح مستند باستخدام فئة `Redactor`. احتفظ بهذا المقتطف كما هو – فهو الأساس لكل ما يلي.

```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx"; // Replace with actual path

using (Redactor redactor = new Redactor(sourceFile))
{
    // Your redaction logic here
}
```

## دليل التنفيذ
الآن سنوسّع الإعداد الأساسي بإضافة `IRedactionCallback` مخصص. يتيح لك ذلك التقاط كل حدث حذف، كتابته إلى سجل، أو حتى تعديل نص الاستبدال في الوقت الفعلي.

### ربط واستخدام تنفيذ IRedactionCallback
الخطوات التالية توضح سير العمل الكامل، من إعداد مسارات الملفات إلى تطبيق حذف عبارة دقيقة.

#### الخطوة 1: إعداد دليل الإخراج ومسار ملف المصدر
عرّف مكان وجود المستند المصدر. عدّل المسار ليتناسب مع بيئتك.

```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx"; // Replace with actual path
```

#### الخطوة 2: إنشاء كائن Redactor بإعدادات مخصصة
ننشئ `Redactor` باستخدام `LoadOptions` و `RedactorSettings`. سيسجل `RedactionDump` داخل الإعدادات كل عملية حذف تلقائيًا.

```csharp
using (Redactor redactor = new Redactor(sourceFile, 
    new LoadOptions(), 
    new RedactorSettings(new RedactionDump())))
{
    // Further processing steps will go here
}
```

#### الخطوة 3: تطبيق حذف عبارة دقيقة
هنا نستبدل العبارة **John Doe** بالعلامة النائبة **[REDACTED]**. يمكنك استبدال أي عبارة أو نمط تحتاج إلى إخفائه.

```csharp
redactor.Apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[REDACTED]")));
```

**شرح الكائنات الرئيسية:**
- `LoadOptions()` – يحدد للـ SDK كيفية قراءة المستند (مثل معالجة كلمة المرور).  
- `RedactorSettings(new RedactionDump())` – يفعّل ملف تفريغ يسجل كل عملية حذف لأغراض التدقيق.  
- `ReplacementOptions("[REDACTED]")` – يحدد النص الذي سيستبدل العبارة المطابقة.

### لماذا هذا مهم
باستخدام `IRedactionCallback`، يمكنك توصيل منطق مخصص مثل:
- إرسال تفاصيل الحذف إلى قاعدة بيانات الامتثال.  
- إخفاء بيانات تعريفية إضافية لا يغطيها استبدال العبارة البسيط.  
- اختيار نص الاستبدال ديناميكيًا بناءً على نوع المحتوى.

### نصائح استكشاف الأخطاء وإصلاحها
- **الملف غير موجود:** تحقق من مسار `sourceFile` وتأكد من أن الملف قابل للوصول من العملية الجارية.  
- **الـ Callback لا يعمل:** تأكد من أن فئتك تنفّذ **جميع** أعضاء `IRedactionCallback` وأن المثيل يُمرّر بشكل صحيح إلى `Redactor`.  
- **بطء الأداء:** للدفعات الكبيرة، أعد استخدام نفس مثيل `Redactor` قدر الإمكان وتأكد من تحريره فور الانتهاء.

## تطبيقات عملية
حذف البيانات الحساسة مفيد عبر العديد من الصناعات:

1. **معالجة المستندات القانونية** – حذف تلقائي لأسماء العملاء، أرقام القضايا، أو أرقام الضمان الاجتماعي قبل مشاركة المسودات.  
2. **أنظمة إدارة الموارد البشرية** – إزالة المعرفات الشخصية من عقود الموظفين أثناء التدقيق.  
3. **التقارير المالية** – إخفاء الأرقام السرية أو أرقام الحسابات عند إنشاء ملفات PDF موجهة للمستثمرين.

## اعتبارات الأداء
للحفاظ على سرعة تطبيقك عند معالجة العشرات أو المئات من الملفات:

- **المعالجة الدفعية:** حمّل قائمة بالملفات وشغّل حلقة الحذف داخل `Parallel.ForEach` لاستغلال الأنوية المتعددة.  
- **إدارة الذاكرة:** ضع كل `Redactor` داخل كتلة `using` (كما هو موضح) لضمان تحرير الموارد.  
- **العمليات غير المتزامنة:** رغم أن SDK متزامن، يمكنك تفويض العمل إلى خيوط خلفية أو `Task.Run` لتجنب حجب خيوط الواجهة.

## المشكلات الشائعة والحلول
| المشكلة | الحل |
|-------|----------|
| **خطأ “Invalid file format”** | تأكد من أن نوع المستند مدعوم (PDF, DOCX, PPTX, إلخ). |
| **Callback يستقبل قيمًا فارغة (null)** | تحقق من أنك تمرّر تنفيذًا ملموسًا لـ `IRedactionCallback` عند إنشاء `RedactorSettings`. |
| **لم يتم تطبيق الحذف** | تأكد من أن العبارة الدقيقة تتطابق مع حالة وحروف المسافة في المستند، أو استخدم `RegexRedaction` للمطابقة النمطية. |

## الأسئلة المتكررة

**س: ما هي خيارات الترخيص لـ GroupDocs.Redaction؟**  
ج: يمكنك البدء بنسخة تجريبية مجانية أو طلب ترخيص مؤقت لاستكشاف جميع المميزات. للإنتاج، اشترِ ترخيصًا دائمًا أو اشتراكًا.

**س: هل يمكنني استخدام GroupDocs.Redaction على أنواع ملفات متعددة؟**  
ج: نعم، يدعم PDF، Word، Excel، PowerPoint، والعديد من الصيغ الشائعة الأخرى.

**س: كيف أتعامل مع الاستثناءات أثناء الحذف؟**  
ج: ضع منطق الحذف داخل كتل `try‑catch` وسجّل تفاصيل الاستثناء. يمكن أيضًا للـ callback التقاط الأخطاء في الوقت الفعلي.

**س: هل هناك دعم مدمج للمعالجة غير المتزامنة؟**  
ج: الواجهة الأساسية متزامنة، لكن يمكنك تشغيل استدعاءات الحذف داخل مهام غير متزامنة أو خدمات خلفية.

**س: أين يمكنني العثور على أمثلة متقدمة؟**  
ج: توفر [official documentation](https://docs.groupdocs.com/redaction/net/) ومرجع API عينات شيفرة واسعة ودلائل سيناريوهات.

## الموارد

- [GroupDocs.Redaction for Net Documentation](https://docs.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction for Net API Reference](https://reference.groupdocs.com/redaction/net/)
- [Download GroupDocs.Redaction for Net](https://releases.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction Forum](https://forum.groupdocs.com/c/redaction/33)
- [Free Support](https://forum.groupdocs.com/)
- [Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**آخر تحديث:** 2026-03-30  
**تم الاختبار مع:** GroupDocs.Redaction 2.3 (أحدث نسخة وقت الكتابة)  
**المؤلف:** GroupDocs