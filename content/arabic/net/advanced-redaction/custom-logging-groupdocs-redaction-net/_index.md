---
date: '2026-03-28'
description: تعلم كيفية تنفيذ مسجل مخصص بلغة C# في GroupDocs.Redaction لـ .NET، مما
  يتيح تسجيل مخصص مفصل في .NET وتسهيل إعداد تقارير الامتثال.
keywords:
- custom logger c#
- custom logging .net
- save redacted document
- log warnings c#
title: تنفيذ مسجل مخصص C# في GroupDocs.Redaction لـ .NET
type: docs
url: /ar/net/advanced-redaction/custom-logging-groupdocs-redaction-net/
weight: 1
---

# تنفيذ مسجل مخصص c# في GroupDocs.Redaction لـ .NET

إدارة عمليات إخفاء المستندات بكفاءة أمر حاسم، خاصةً عند التعامل مع معلومات حساسة. في هذا الدليل ستتعلم **كيفية تنفيذ مسجل مخصص c#** مع GroupDocs.Redaction لـ .NET، مما يمنحك سيطرة كاملة على التسجيل، ومعالجة الأخطاء، وسجلات التدقيق.

## إجابات سريعة
- **ماذا يفعل مسجل مخصص c#؟** يلتقط الأخطاء والتحذيرات والرسائل المعلوماتية أثناء الإخفاء.  
- **أي مكتبة توفر واجهة ILogger؟** GroupDocs.Redaction لـ .NET.  
- **هل يمكنني حفظ المستند المُخفى دون التحويل إلى نقطية؟** نعم – استخدم `redactor.Save(..., new Options.RasterizationOptions { Enabled = false })`.  
- **هل أحتاج إلى ترخيص للاستخدام في الإنتاج؟** يلزم ترخيص كامل للإنتاج؛ يتوفر نسخة تجريبية للتقييم.  
- **هل هذا النهج متوافق مع .NET Core / .NET 6+؟** بالتأكيد – نفس الـ API يعمل عبر .NET Framework و .NET Core/5/6.

## ما هو مسجل مخصص c#؟
مسجل مخصص **c#** هو فئة تقوم بتنفيذ واجهة `ILogger` التي توفرها GroupDocs.Redaction. يتيح لك توجيه رسائل السجل إلى أي مكان تحتاجه—الكونسول، الملف، قاعدة البيانات، أو أنظمة المراقبة الخارجية—مع توفير رؤية واضحة لسير عمل الإخفاء.

## لماذا استخدام تسجيل مخصص .net مع GroupDocs.Redaction؟
- **الامتثال والتدقيق:** السجلات التفصيلية تلبي المتطلبات التنظيمية.  
- **رؤية الأخطاء:** `LogError` و `LogWarning` يقدمان لك رد فعل فوري على المشكلات.  
- **مرونة التكامل:** تحويل السجلات إلى أطر تسجيل .NET الموجودة (Serilog، NLog، إلخ).

## المتطلبات المسبقة
- **GroupDocs.Redaction لـ .NET** مثبت (انظر التثبيت أدناه).  
- بيئة تطوير .NET (Visual Studio، VS Code، أو سطر الأوامر).  
- معرفة أساسية بـ C# وإلمام بتدفقات الملفات.

## التثبيت

**.NET CLI**
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
ابحث عن **"GroupDocs.Redaction"** وقم بتثبيت أحدث نسخة.

## الحصول على الترخيص
- **نسخة تجريبية مجانية:** اختبار الـ API بترخيص مؤقت.  
- **ترخيص مؤقت:** الحصول على الوصول الكامل للميزات لفترة محدودة.  
- **شراء:** الحصول على ترخيص دائم للنشر في بيئات الإنتاج.

## دليل خطوة بخطوة

### الخطوة 1: تعريف فئة مسجل مخصص (log warnings c#)

إنشاء فئة تقوم بتنفيذ `ILogger`. ستقوم هذه الفئة بالتقاط الأخطاء والتحذيرات والرسائل المعلوماتية.

```csharp
using System;
using GroupDocs.Redaction;

class CustomLogger : ILogger
{
    public bool HasErrors { get; private set; }

    // Log errors encountered during processing.
    public void LogError(string message)
    {
        Console.WriteLine("Error: " + message);
        HasErrors = true;
    }

    // Log warnings that may not be critical but need attention.
    public void LogWarning(string message)
    {
        Console.WriteLine("Warning: " + message);
    }

    // Log informational messages for tracking normal operations.
    public void LogInfo(string message)
    {
        Console.WriteLine("Info: " + message);
    }
}
```

**شرح:** علم `HasErrors` يساعدك على اتخاذ قرار ما إذا كنت ستستمر في المعالجة. الطرق الثلاثة تتطابق مع مستويات السجل الثلاث التي ستحتاجها في معظم سيناريوهات الإخفاء.

### الخطوة 2: إعداد مسارات الملفات وفتح المستند المصدر

```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
string outputFile = Utils.GetOutputFile(sourceFile);
```

**لماذا هذا مهم:** استخدام طرق المساعدة يحافظ على نظافة الكود ويضمن وجود مجلد الإخراج قبل محاولة **حفظ المستند المُخفى**.

### الخطوة 3: تطبيق الإخفاءات أثناء استخدام المسجل المخصص

```csharp
using (Stream stream = File.Open(sourceFile, FileMode.Open, FileAccess.ReadWrite))
{
    var logger = new CustomLogger();
    
    using (Redactor redactor = new Redactor(stream, new LoadOptions(), new RedactorSettings(logger)))
    {
        // Apply a redaction to the document.
        redactor.Apply(new DeleteAnnotationRedaction());
        
        if (!logger.HasErrors)
        {
            using (Stream streamOut = File.Open(outputFile, FileMode.OpenOrCreate, FileAccess.ReadWrite))
            {
                // Save changes without rasterizing the output.
                redactor.Save(streamOut, new Options.RasterizationOptions { Enabled = false });
            }
        }
    }
}
```

**شرح:**  
1. يتم إنشاء كائن `Redactor` باستخدام `RedactorSettings(logger)`، مما يربط `CustomLogger` الخاص بك.  
2. بعد تطبيق الإخفاء، يتحقق الكود من `logger.HasErrors`. إذا لم تحدث أخطاء، يتم حفظ المستند—مما يوضح منطق **حفظ المستند المُخفى** دون التحويل إلى نقطية.

### المشكلات الشائعة وإصلاح الأخطاء
- **غياب مخرجات السجل:** تأكد من أن كل طريقة `Log*` تم تجاوزها بشكل صحيح.  
- **استثناءات الوصول إلى الملفات:** تأكد من أن التطبيق يمتلك صلاحيات القراءة/الكتابة لكل من مسارات المصدر والإخراج.  
- **المسجل غير موصول:** معامل `RedactorSettings(logger)` أساسي؛ إهماله يعطل التسجيل المخصص.

## التطبيقات العملية
1. **تقارير الامتثال:** تصدير سجلات السجل إلى CSV أو قاعدة بيانات لسجلات التدقيق.  
2. **تتبع الأخطاء:** تحديد الملفات المشكلة بسرعة عبر فحص مخرجات `LogError`.  
3. **أتمتة سير العمل:** تشغيل عمليات لاحقة (مثل إبلاغ مسؤول الامتثال) عند استدعاء `LogWarning`.

## اعتبارات الأداء
- **تخلص من التدفقات بسرعة** لتحرير الذاكرة، خاصةً عند معالجة دفعات كبيرة.  
- **راقب وحدة المعالجة المركزية والذاكرة** أثناء الإخفاءات الضخمة؛ فكر في معالجة المستندات بشكل متوازي مع مزامنة دقيقة للمسجل.  
- **ابقَ محدثًا:** الإصدارات الأحدث من GroupDocs.Redaction غالبًا ما تتضمن تحسينات في الأداء وإضافات لسجلات إضافية.

## الخلاصة

من خلال تنفيذ **مسجل مخصص c#**، تحصل على رؤية دقيقة لكل خطوة في خط أنابيب الإخفاء، مما يسهل الالتزام بمعايير الامتثال وتصحيح المشكلات. النهج المعروض هنا يعمل بسلاسة مع GroupDocs.Redaction لـ .NET ويمكن توسيعه للتكامل مع أي إطار تسجيل .NET تستخدمه بالفعل.

---

## الأسئلة المتكررة

**س: ما هو هدف التسجيل المخصص مع GroupDocs.Redaction؟**  
ج: يساعد التسجيل المخصص في تتبع وإدارة الإخفاءات للامتثال، وتتبع الأخطاء، وتحسين سير العمل.

**س: كيف أتعامل مع الأخطاء باستخدام مسجل مخصص؟**  
ج: نفّذ `LogError` في فئة `CustomLogger` الخاصة بك؛ علم `HasErrors` يتيح لك إيقاف المعالجة إذا لزم الأمر.

**س: هل يمكن دمج التسجيل المخصص مع أنظمة أخرى؟**  
ج: نعم، يمكنك توجيه رسائل السجل إلى أنظمة CRM أو ERP أو أدوات المراقبة المركزية عن طريق توسيع طرق المسجل.

**س: ما هي بعض المشكلات الشائعة عند تنفيذ التسجيل المخصص؟**  
ج: تنفيذ طرق غير صحيح، فقدان `RedactorSettings(logger)`، ومشكلات صلاحيات الملفات هي الأكثر شيوعًا.

**س: كيف يحسن التسجيل المخصص سير عمل إخفاء المستندات؟**  
ج: السجلات التفصيلية توفر رؤية في الوقت الحقيقي، تبسط استكشاف الأخطاء، وتلبي متطلبات التدقيق.

## الموارد

- **الوثائق:** [GroupDocs.Redaction .NET Documentation](https://docs.groupdocs.com/redaction/net/)  
- **مرجع API:** [GroupDocs.Redaction API Reference](https://reference.groupdocs.com/redaction/net)  
- **تحميل:** [GroupDocs.Redaction for .NET](https://downloads.groupdocs.com/redaction/net)

---

**آخر تحديث:** 2026-03-28  
**تم الاختبار مع:** GroupDocs.Redaction 23.11 لـ .NET  
**المؤلف:** GroupDocs