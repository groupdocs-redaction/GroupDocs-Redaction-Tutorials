---
date: '2026-08-09'
description: تعلم كيفية إخفاء البيانات الشخصية وإخفاء عناوين البريد الإلكتروني في
  جداول Excel باستخدام GroupDocs.Redaction Java API.
keywords:
- how to hide personal data
- mask email addresses excel
- GroupDocs.Redaction Java
- Excel redaction tutorial
lastmod: '2026-08-09'
og_description: اكتشف خطوة بخطوة كيفية إخفاء البيانات الشخصية وإخفاء عناوين البريد
  الإلكتروني في ملفات Excel باستخدام GroupDocs.Redaction Java API – حل سريع وآمن للامتثال
  لـ GDPR.
og_image_alt: Guide showing Java code that redacts email addresses in an Excel spreadsheet
og_title: كيفية إخفاء البيانات الشخصية في Excel باستخدام GroupDocs Java
schemas:
- author: GroupDocs
  dateModified: '2026-08-09'
  description: Learn how to hide personal data and mask email addresses in Excel spreadsheets
    using the GroupDocs.Redaction Java API.
  headline: How to hide personal data in Excel with GroupDocs Java
  type: TechArticle
- description: Learn how to hide personal data and mask email addresses in Excel spreadsheets
    using the GroupDocs.Redaction Java API.
  name: How to hide personal data in Excel with GroupDocs Java
  steps:
  - name: '**Partner data exchange** – Automatically strip customer emails before
      sending spreadsheets to vendors.'
    text: '**Partner data exchange** – Automatically strip customer emails before
      sending spreadsheets to vendors.'
  - name: '**Internal audit preparation** – Anonymize employee data during compliance
      reviews.'
    text: '**Internal audit preparation** – Anonymize employee data during compliance
      reviews.'
  - name: '**Scheduled reporting** – Embed the redaction step into nightly batch jobs
      that generate distribution‑ready reports.'
    text: '**Scheduled reporting** – Embed the redaction step into nightly batch jobs
      that generate distribution‑ready reports.'
  type: HowTo
- questions:
  - answer: Extend the pattern to include additional allowed characters (e.g., “+”
      or “_”) and test against a larger sample set, then re‑run the redaction.
    question: My regex still misses some corporate email formats. What should I do?
  - answer: Yes. Create a separate `CellFilter` for each column and invoke `redactor.apply`
      for each filter sequentially.
    question: Can I redact more than one column in a single pass?
  - answer: The library processes sheets incrementally, so files up to several gigabytes
      can be redacted as long as you enable streaming and close the `Redactor` after
      each file.
    question: Is GroupDocs.Redaction able to handle Excel files larger than 1 GB?
  - answer: Inspect the `RedactorChangeLog` returned by `apply`; a non‑failed status
      indicates success, while any errors are listed with line numbers and cell references.
    question: How do I capture redaction results or errors?
  - answer: Absolutely. Build the placeholder string dynamically (e.g., `"[redacted:"
      + UUID.randomUUID() + "]"`) and pass it to `ReplacementOptions`.
    question: Can I use a custom placeholder that includes a unique token per row?
  type: FAQPage
tags:
- hide personal data
- GroupDocs.Redaction
- Java Excel processing
- data privacy
title: كيفية إخفاء البيانات الشخصية في Excel باستخدام GroupDocs Java
url: /ar/java/spreadsheet-redaction/redact-emails-excel-groupdocs-redaction-java/
weight: 1
---

# كيفية إخفاء البيانات الشخصية في Excel باستخدام GroupDocs Java

في هذا الدليل ستتعلم **كيفية إخفاء البيانات الشخصية**—وبشكل خاص عناوين البريد الإلكتروني—في دفاتر عمل Excel باستخدام واجهة برمجة تطبيقات GroupDocs.Redaction للغة Java. سواء كنت بحاجة للامتثال لـ GDPR أو CCPA أو سياسات الخصوصية الداخلية، فإن النهج الموضح هنا يتيح لك أتمتة عملية الإزالة بأمان، والحفاظ على الملف الأصلي دون تعديل، وإنتاج نسخة نظيفة جاهزة للتوزيع.

## إجابات سريعة
- **ماذا يعني “إخفاء البيانات الشخصية”?** يعني ذلك إخفاء أو إزالة المعلومات التي يمكن التعرف على هوية الشخص (PII) من الملف بشكل دائم بحيث لا يمكن قراءتها بعد ذلك.  
- **ما المكتبة التي تقوم بعملية الإزالة؟** GroupDocs.Redaction للغة Java.  
- **هل أحتاج إلى ترخيص لتشغيل المثال؟** نسخة تجريبية مجانية تكفي للاختبار؛ يتطلب الاستخدام التجاري ترخيصًا من فئة الإنتاج.  
- **هل يمكنني تخصيص نص العنصر النائب؟** نعم—يمكنك استبدال عناوين البريد الإلكتروني بأي سلسلة مثل “[redacted email]”.  
- **هل الطريقة مناسبة لجداول البيانات الكبيرة؟** نعم، عند اتباع نصائح الأداء في قسم “اعتبارات الأداء”.

## ما هو إخفاء البيانات الشخصية؟
**إخفاء البيانات الشخصية** يشير إلى الإزالة أو الإخفاء غير القابل للعكس لأي معلومات يمكنها تحديد هوية الفرد مباشرة أو غير مباشرة، مثل الأسماء، أرقام الهواتف، أو عناوين البريد الإلكتروني. تضمن هذه العملية عدم إمكانية استخدام الملف الناتج لإعادة التعرف على الشخص.

## لماذا نستخدم GroupDocs.Redaction للغة Java؟
يدعم GroupDocs.Redaction **أكثر من 30 صيغة إدخال وإخراج** ويمكنه معالجة دفاتر العمل التي تحتوي على **ما يصل إلى 500,000 صف** دون تحميل الملف بالكامل في الذاكرة، مما يحقق **تقليل استهلاك الذاكرة بنسبة تصل إلى 80 %** مقارنةً بحلول تحليل الملفات البسيطة. تجعل هذه الفوائد القابلة للقياس اختيارًا مفضلاً لسلاسل معالجة خصوصية البيانات على مستوى المؤسسات.

## المتطلبات المسبقة
- مجموعة تطوير جافا (JDK) 8 أو أحدث.  
- إلمام أساسي بملفات بناء Maven.  
- الوصول إلى مكتبة GroupDocs.Redaction للغة Java (قابلة للتنزيل عبر Maven أو صفحة الإصدار الرسمية).

## إعداد GroupDocs.Redaction للغة Java

### كيف أضيف GroupDocs.Redaction إلى مشروع Maven؟
أضف مستودع GroupDocs واعتماد Redaction إلى ملف `pom.xml` الخاص بك (انظر [إصدارات GroupDocs.Redaction](https://releases.groupdocs.com/redaction/java/)). ثم نفّذ الأمر `mvn clean install` لجلب الحزم.

```text
```xml
<repositories>
   <repository>
      <id>repository.groupdocs.com</id>
      <name>GroupDocs Repository</name>
      <url>https://releases.groupdocs.com/redaction/java/</url>
   </repository>
</repositories>

<dependencies>
   <dependency>
      <groupId>com.groupdocs</groupId>
      <artifactId>groupdocs-redaction</artifactId>
      <version>24.9</version>
   </dependency>
</dependencies>
```
```

### كيف يمكنني الحصول على ترخيص لـ GroupDocs.Redaction؟
تقدم GroupDocs ثلاث خيارات للترخيص (انظر [موقع GroupDocs](https://purchase.groupdocs.com/temporary-license/)):
- **نسخة تجريبية مجانية** – تقييم بميزات محدودة، لا يتطلب بطاقة ائتمان.  
- **ترخيص مؤقت** – مفتاح تقييم لمدة 30 يومًا يتم الحصول عليه من موقع GroupDocs.  
- **ترخيص كامل** – ترخيص إنتاج دائم يتم شراؤه عبر بوابة المبيعات.

```text
```java
import com.groupdocs.redaction.Redactor;

public class RedactEmails {
    public static void main(String[] args) {
        // Initialize the redactor with your document path
        try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_XLSX")) {
            // Your redaction logic will go here
        }
    }
}
```
```

## دليل التنفيذ

### كيف أنشئ كائن Redactor لملف Excel؟
فئة `Redactor` هي نقطة الدخول الرئيسية التي تقوم بتحميل المستند وتوفر عمليات الإزالة.  
أنشئ كائن `Redactor` يشير إلى دفتر العمل المصدر. فئة `Redactor` هي نقطة الدخول لجميع عمليات الإزالة؛ فهي تقوم بتحميل الملف إلى بنية ذاكرة مُدارة مع الحفاظ على الملف الأصلي على القرص.

```text
```java
import com.groupdocs.redaction.Redactor;

public class RedactEmails {
    public static void main(String[] args) {
        try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_XLSX")) {
            // Proceed to the next steps for redaction
        }
    }
}
```
```

### كيف يمكنني حصر الإزالة على ورقة عمل واحدة وعمود واحد؟
تتيح لك فئة `CellFilter` تحديد ورقة العمل و(الأعمدة) التي يجب فحصها للإزالة. استخدم `CellFilter` لتحديد اسم الورقة المستهدفة ورقم العمود. تقوم فئة `CellFilter` بترشيح الخلايا قبل أن يقوم محرك الإزالة بتقييمها، مما يضمن معالجة الخلايا المقصودة فقط.

```text
```java
import com.groupdocs.redaction.redactions.CellFilter;

// Create and configure the filter
CellFilter filter = new CellFilter();
filter.setColumnIndex(1); // Targeting the second column (index starts at 0)
filter.setWorkSheetName("Customers"); // Specify the worksheet name
```
```

### كيف أحدد نمط تعبير منتظم يطابق معظم عناوين البريد الإلكتروني؟
تمثل فئة `Pattern` من `java.util.regex` تعبيرًا منتظمًا مُجمعًا يُستخدم لمطابقة النص. أنشئ كائن `Pattern` باستخدام تعبير regex يلتقط صيغ البريد الإلكتروني النموذجية. النمط أدناه يطابق غالبية العناوين المتوافقة مع RFC‑5322 مع تجاهل السلاسل غير الصالحة.

```text
```java
import java.util.regex.Pattern;

// Define regex pattern for matching emails
Pattern expression = Pattern.compile("^\\w+([-+.']\\w+)*@\\w+([-.]\\w+)*\\.\\w+([-.]\\w+)*$");
```
```

### كيف أطبق الإزالة وأستبدل عناوين البريد الإلكتروني بنص بديل؟
تحدد فئة `ReplacementOptions` كيفية استبدال المحتوى المطابق، مثل نص العنصر النائب. اجمع بين الفلتر والنمط وكائن `ReplacementOptions`. تتيح لك فئة `ReplacementOptions` تعيين نص العنصر النائب الدقيق الذي سيظهر في كل خلية مُزالة.

```text
```java
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.RedactorChangeLog;
import com.groupdocs.redaction.redactions.CellColumnRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

// Apply redaction
RedactorChangeLog result = redactor.apply(new CellColumnRedaction(filter, expression, new ReplacementOptions("[customer email]")));

// Save changes if successful
if (result.getStatus() != RedactionStatus.Failed) {
    SaveOptions saveOptions = new SaveOptions();
    saveOptions.setAddSuffix(true); // Add a suffix to the saved file name
    redactor.save(saveOptions);
}
```
```

## الأخطاء الشائعة واستكشاف الأخطاء

- **التعبير النمطي لا يلتقط جميع الحالات** – اختبر النمط على عينة تمثيلية من بياناتك وعدّل فئات الأحرف حسب الحاجة.  
- **رقم العمود غير صحيح** – تذكر أن ترقيم الأعمدة يبدأ من 0؛ العمود B هو الفهرس 1.  
- **حساسية حالة اسم ورقة العمل** – استخدم الاسم الدقيق للورقة كما هو في Excel؛ “Customers” ≠ “customers”.  
- **تسرب الموارد** – احط `Redactor` بكتلة try‑with‑resources (كما هو موضح) لضمان تحرير الموارد الأصلية بسرعة.

## لماذا نُخفي البيانات الشخصية في Excel؟
إخفاء البيانات الشخصية في Excel يزيل أي معلومات تعريفية شخصية، مما يضمن عدم إمكانية استخدام الملف لتتبع الأفراد. يحمي ذلك الخصوصية، ويلبي المتطلبات التنظيمية، ويمنع التسريبات العرضية عند مشاركة جداول البيانات مع أطراف خارجية أو نشر البيانات علنًا.

- **الامتثال التنظيمي** – تلبية متطلبات GDPR وCCPA واللوائح الخاصة بالخصوصية في الصناعة.  
- **تخفيف المخاطر** – منع الكشف العرضي عن المعلومات الشخصية عند مشاركة الملفات مع شركاء خارجيين.  
- **الاستعداد للتدقيق** – الحفاظ على سجل تدقيق نظيف وغير قابل للتغيير عن طريق إزالة القيم الحساسة بشكل دائم من مجموعات البيانات المؤرشفة.

## تطبيقات عملية

1. **تبادل بيانات الشركاء** – حذف عناوين البريد الإلكتروني للعملاء تلقائيًا قبل إرسال جداول البيانات إلى البائعين.  
2. **تحضير التدقيق الداخلي** – إخفاء هوية بيانات الموظفين أثناء مراجعات الامتثال.  
3. **التقارير المجدولة** – دمج خطوة الإزالة في وظائف الدفعات الليلية التي تُنشئ تقارير جاهزة للتوزيع.

## اعتبارات الأداء

- **المعالجة الدفعية** – إعادة استخدام كائن `Redactor` واحد عبر ملفات متعددة لتقليل عبء JVM.  
- **إدارة الذاكرة** – تقوم الواجهة البرمجية بمعالجة أوراق العمل واحدةً تلو الأخرى؛ بالنسبة لدفاتر العمل التي تتجاوز 100 ميغابايت، عالج الصفوف على دفعات للحفاظ على استهلاك الذاكرة منخفضًا.  
- **مجموعات البيانات الكبيرة** – عند التعامل مع ملفات تحتوي على أكثر من 100 ألف صف، فعّل وضع البث (متاح في الإصدار 24.9) للحفاظ على استهلاك الذاكرة تحت 200 ميغابايت.

## الأسئلة المتكررة

**س: لا يزال التعبير النمطي الخاص بي يفوت بعض صيغ البريد الإلكتروني المؤسسية. ماذا أفعل؟**  
ج: قم بتوسيع النمط ليشمل أحرفًا مسموحًا إضافية (مثل “+” أو “_”) واختبره على مجموعة عينات أكبر، ثم أعد تشغيل عملية الإزالة.

**س: هل يمكنني إزالة أكثر من عمود في عملية واحدة؟**  
ج: نعم. أنشئ `CellFilter` منفصل لكل عمود واستدعِ `redactor.apply` لكل فلتر على التوالي.

**س: هل يستطيع GroupDocs.Redaction التعامل مع ملفات Excel أكبر من 1 جيجابايت؟**  
ج: تقوم المكتبة بمعالجة الأوراق بشكل تدريجي، لذا يمكن إزالة ملفات تصل إلى عدة جيجابايت طالما فعلت وضع البث وأغلقت `Redactor` بعد كل ملف.

**س: كيف ألتقط نتائج الإزالة أو الأخطاء؟**  
ج: افحص `RedactorChangeLog` الذي تُعيده `apply`؛ الحالة غير الفاشلة تشير إلى النجاح، بينما تُدرج أي أخطاء مع أرقام الأسطر وإشارات الخلايا.

**س: هل يمكنني استخدام عنصر نائب مخصص يتضمن رمزًا فريدًا لكل صف؟**  
ج: بالتأكيد. أنشئ سلسلة العنصر النائب ديناميكيًا (مثال: `"[redacted:" + UUID.randomUUID() + "]"`) ومرّرها إلى `ReplacementOptions`.

## موارد إضافية

- [التوثيق](https://docs.groupdocs.com/redaction/java/)
- [مرجع API](https://reference.groupdocs.com/redaction/java)
- [تحميل GroupDocs.Redaction](https://releases.groupdocs.com/redaction/java/)
- [مستودع GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
- [منتدى الدعم المجاني](https://forum.groupdocs.com/c/redaction/33)
- [معلومات الترخيص المؤقت](https://purchase.groupdocs.com/temporary-license/)

---

**آخر تحديث:** 2026-08-09  
**تم الاختبار مع:** GroupDocs.Redaction 24.9 للغة Java  
**المؤلف:** GroupDocs

## دروس ذات صلة

- [كيفية تصفية البيانات في جداول البيانات – GroupDocs.Redaction Java](/redaction/java/spreadsheet-redaction/)
- [إخفاء البيانات الحساسة Java – إزالة المعلومات الشخصية باستخدام GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)
- [إخفاء البيانات الحساسة Java – دليل GroupDocs.Redaction](/redaction/java/getting-started/)