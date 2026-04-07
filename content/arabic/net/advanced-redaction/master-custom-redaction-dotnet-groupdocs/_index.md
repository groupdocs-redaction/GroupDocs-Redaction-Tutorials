---
date: '2026-04-07'
description: تعلم كيفية تعديل ملفات PDF في .NET باستخدام GroupDocs.Redaction، إزالة
  النص من PDF، وحفظ ملف PDF المعدل بأمان.
keywords:
- how to redact pdf
- remove text pdf
- redact medical records
- save redacted pdf
title: كيفية إخفاء محتوى PDF في .NET باستخدام GroupDocs.Redaction
type: docs
url: /ar/net/advanced-redaction/master-custom-redaction-dotnet-groupdocs/
weight: 1
---

# كيفية إخفاء محتوى PDF في .NET باستخدام GroupDocs.Redaction

في عالمنا الرقمي سريع الحركة اليوم، **how to redact PDF** هو سؤال يطرحه العديد من المطورين. سواء كنت تحمي بيانات العملاء، أو تزيل البنود السرية من العقود القانونية، أو ببساطة تحذف النص غير المرغوب فيه من تقرير، فإن إتقان إخفاء محتوى PDF في .NET يمنحك سيطرة كاملة على الخصوصية. يوضح هذا الدليل كل خطوة لاستخدام GroupDocs.Redaction لـ **remove text PDF**، **redact medical records**، و **save redacted PDF** بأمان.

## إجابات سريعة
- **ما المكتبة التي تتعامل مع إخفاء PDF في .NET؟** GroupDocs.Redaction for .NET.  
- **هل يمكنني إخفاء عبارات محددة فقط؟** نعم – استخدم التعبيرات النمطية (regular expressions) أو معالج مخصص.  
- **هل تحتاج إلى ترخيص للاستخدام في الإنتاج؟** يلزم وجود ترخيص GroupDocs صالح للاستخدام في الإنتاج.  
- **هل سيتم الحفاظ على تخطيط الصفحة الأصلي؟** يحافظ محرك الإخفاء على تخطيط الصفحة كما هو أثناء إخفاء المحتوى.  
- **كيف أحفظ الملف النهائي؟** استدعِ `Redactor.Save` مع كائن `SaveOptions` لإنشاء ملف PDF مَحْجُوب.

## ما هو إخفاء PDF ولماذا هو مهم؟
إخفاء PDF يزيل أو يغطي المعلومات الحساسة بشكل دائم بحيث لا يمكن استعادتها. على عكس الإخفاء البسيط، يقوم الإخفاء بالكتابة فوق البيانات الأساسية، مما يضمن الامتثال للأنظمة مثل GDPR، HIPAA، وPCI‑DSS. باستخدام GroupDocs.Redaction، يمكنك أتمتة هذه العملية مباشرةً من تطبيقات .NET الخاصة بك.

## المتطلبات المسبقة
قبل أن نبدأ، تأكد من توفر ما يلي:

- **GroupDocs.Redaction for .NET** (الوصول إلى المكتبة).  
- **.NET Framework 4.6+** أو **.NET Core 3.1+** (أي بيئة تشغيل .NET حديثة).  
- بيئة تطوير متوافقة مع C# مثل Visual Studio أو VS Code.  
- معرفة أساسية بالتعبيرات النمطية (regular expressions) لتطابق الأنماط.

## إعداد GroupDocs.Redaction لـ .NET
أولاً، أضف المكتبة إلى مشروعك.

**.NET CLI**
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
ابحث عن “GroupDocs.Redaction” وقم بتثبيت أحدث نسخة.

### خطوات الحصول على الترخيص
- **Free Trial**: احصل على ترخيص مؤقت لاستكشاف جميع الميزات.  
- **Purchase**: للاستخدام طويل الأمد، اشترِ اشتراكًا من [GroupDocs](https://purchase.groupdocs.com/).

بعد تثبيت الحزمة، يمكنك إنشاء كائن `Redactor` يشير إلى ملف PDF الذي تريد معالجته.

## كيفية إخفاء PDF باستخدام معالجات مخصصة
يوفر الإخفاء المخصص تحكمًا دقيقًا، وهو مثالي للسيناريوهات مثل **redact medical records** حيث تحتاج إلى استهداف أنماط محددة.

### تنفيذ خطوة بخطوة

#### الخطوة 1: تحديد مسارات المصدر والوجهة
```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/LOREMIPSUM_PDF.pdf";
```

#### الخطوة 2: بناء تعبير نمطي وخيارات الاستبدال  
هنا نستخدم نمط بسيط `.*` لتوضيح العملية؛ استبدله بتعبير نمطي أكثر دقة لحالات الاستخدام الفعلية (مثل رقم الضمان الاجتماعي، أرقام بطاقات الائتمان).
```csharp
Regex regex = new Regex(".*");
ReplacementOptions optionsText = new ReplacementOptions("[replaced]");
optionsText.CustomRedaction = new TextRedactor();
```

#### الخطوة 3: إنشاء الإخفاء وتطبيقه  
كائن `PageAreaRedaction` يربط التعبير النمطي بالمعالج المخصص.
```csharp
var textRedaction = new PageAreaRedaction(regex, optionsText);
var redactions = new Redaction[] { textRedaction };

using (Redactor redactor = new Redactor(sourceFile))
{
    RedactorChangeLog result = redactor.Apply(redactions);
    if (result.Status != RedactionStatus.Failed)
    {
        var outputFile = redactor.Save(new Options.SaveOptions(false, "Custom_Redaction_Result"));
        // Output file saved to YOUR_OUTPUT_DIRECTORY.
    }
    else
    {
        Console.WriteLine("Custom redaction failed");
    }
}
```

#### الخطوة 4: تنفيذ معالج إخفاء مخصص  
المعالج يتيح لك إعادة كتابة النص المتطابق بالضبط كما تحتاج.
```csharp
public class TextRedactor : ICustomRedactionHandler
{
    public CustomRedactionResult Redact(CustomRedactionContext context)
    {
        CustomRedactionResult result = new CustomRedactionResult();
        
        try
        {
            Regex regex = new Regex(@"Lorem ipsum");
            if (regex.IsMatch(context.Text))
            {
                string redactedText = regex.Replace(context.Text, "[redacted‑custom]");
                result.Apply = true;
                result.Text = redactedText;
            }
        }
        catch (System.Exception ex)
        {
            result.Apply = false;
        }

        return result;
    }
}
```

### لماذا تستخدم معالجًا مخصصًا؟
- **الدقة** – استهدف فقط العبارات الدقيقة التي تحتاجها.  
- **المرونة** – استبدل النص بسلاسل مخصصة، أقنعة، أو حتى صور.  
- **الامتثال** – تأكد من أن البيانات المزالة لا يمكن استعادتها، بما يتوافق مع المعايير القانونية.

#### نصائح استكشاف الأخطاء وإصلاحها
- تحقق مرة أخرى من صياغة التعبير النمطي؛ خطأ صغير قد يتسبب في تخطي النص المقصود.  
- تأكد من أن التطبيق يمتلك أذونات القراءة/الكتابة للمجلدات المصدر والمخرجات.  
- استخدم `RedactorChangeLog` لفحص الصفحات التي تم تعديلها.

## حالات الاستخدام العملية

| السيناريو | كيف يساعد الإخفاء |
|----------|---------------------|
| **المستندات القانونية** | إخفاء أسماء العملاء، أرقام القضايا، أو البنود السرية قبل المشاركة. |
| **التقارير المالية** | إزالة أرقام الحسابات، الأرصدة، أو الصيغ المملوكة. |
| **السجلات الطبية** | **Redact medical records** للامتثال لـ HIPAA أثناء مشاركة دراسات الحالة. |
| **المذكرات الداخلية** | إزالة رموز المشاريع الداخلية أو كلمات المرور من ملفات PDF المرسلة خارجيًا. |
| **أنظمة إدارة المستندات** | أتمتة تطبيق الخصوصية عبر مكتبات المستندات الكبيرة. |

## اعتبارات الأداء
- **معالجة على دفعات** – بالنسبة لملفات PDF الكبيرة جدًا، عالج الصفحات على دفعات للحفاظ على انخفاض استهلاك الذاكرة.  
- **تعبير نمطي فعال** – يفضَّل استخدام تعبيرات نمطية مُجمَّعة (`new Regex(pattern, RegexOptions.Compiled)`) لتسريع المطابقة.  
- **تحرير الموارد بسرعة** – غلف `Redactor` بكتلة `using` (كما هو موضح) لتحرير مقابض الملفات فورًا.  

## الخلاصة
أصبح لديك الآن سير عمل كامل وجاهز للإنتاج لإخفاء ملفات **how to redact PDF** في .NET باستخدام GroupDocs.Redaction. من خلال الاستفادة من المعالجات المخصصة، يمكنك **remove text PDF**، **redact medical records**، و **save redacted PDF** بنواتج تلبي متطلبات الخصوصية الصارمة.

### الخطوات التالية
- استكشف المزيد في [توثيق GroupDocs](https://docs.groupdocs.com/redaction/net/).  
- جرّب أنماط regex أكثر تعقيدًا (مثل أرقام بطاقات الائتمان، عناوين البريد الإلكتروني).  
- دمج خدمة الإخفاء في خط أنابيب إدارة المستندات الحالي لديك.

## الأسئلة المتكررة

**س: هل يمكنني إخفاء ملفات PDF المحمية بكلمة مرور؟**  
ج: نعم. افتح المستند باستخدام كلمة المرور المناسبة قبل إنشاء كائن `Redactor`.

**س: هل يدعم GroupDocs.Redaction إخفاء الصور؟**  
ج: بالتأكيد. يمكنك تعريف مناطق إخفاء تعتمد على الصور إلى جانب إخفاء النص.

**س: كيف أضمن أن ملف PDF المَحْجُوب يتوافق مع HIPAA؟**  
ج: استخدم معالجًا مخصصًا لاستهداف أنماط PHI، وتحقق من `RedactorChangeLog`، واحتفظ بسجلات تدقيق لإجراءات الإخفاء.

**س: ماذا لو احتجت إلى إخفاء آلاف ملفات PDF تلقائيًا؟**  
ج: أنشئ معالج دفعات يتنقل عبر الملفات، يطبق نفس قواعد الإخفاء، ويكتب النتائج إلى مجلد إخراج مخصص.

**س: هل هناك طريقة لمعاينة الإخفاءات قبل الحفظ؟**  
ج: يمكنك استدعاء `Redactor.GetRedactionPreview()` (متاح في الإصدارات الأحدث) لإنشاء صورة معاينة لكل صفحة.

## الموارد
- **Documentation**: [GroupDocs Redaction Documentation](https://docs.groupdocs.com/redaction/net/)
- **API Reference**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction/net)
- **Download**: [GroupDocs Releases](https://releases.groupdocs.com/redaction/net/)
- **Free Support**: [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)
- **Temporary License**: [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**آخر تحديث:** 2026-04-07  
**تم الاختبار مع:** GroupDocs.Redaction 23.7 for .NET  
**المؤلف:** GroupDocs