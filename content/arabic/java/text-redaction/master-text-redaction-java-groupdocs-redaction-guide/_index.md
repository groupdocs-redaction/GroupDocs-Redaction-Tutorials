---
date: '2026-08-20'
description: اكتشف كيفية إخفاء النص باستخدام regex في Java مع GroupDocs.Redaction.
  يوضح لك هذا الدليل خطوة بخطوة كيفية تطبيق regex، وتكوين خيارات الحفظ، وحماية البيانات
  الحساسة.
keywords:
- how to redact text
- mask credit card numbers
- remove social security numbers
- redact pdf java
lastmod: '2026-08-20'
og_description: تعلم كيفية إخفاء النص في Java باستخدام GroupDocs.Redaction. يشرح هذا
  الدليل إخفاء النص باستخدام regex، وتكوين خيارات الحفظ، ونصائح الأداء لحماية البيانات
  الحساسة.
og_image_alt: Guide showing Java code to redact text using GroupDocs.Redaction
og_title: كيفية إخفاء النص في Java باستخدام GroupDocs.Redaction
schemas:
- author: GroupDocs
  dateModified: '2026-08-20'
  description: Discover how to redact text using regex in Java with GroupDocs.Redaction.
    This step‑by‑step tutorial shows you how to apply regex, configure save options,
    and protect sensitive data.
  headline: 'How to redact text in Java with GroupDocs.Redaction: A complete guide'
  type: TechArticle
- description: Discover how to redact text using regex in Java with GroupDocs.Redaction.
    This step‑by‑step tutorial shows you how to apply regex, configure save options,
    and protect sensitive data.
  name: 'How to redact text in Java with GroupDocs.Redaction: A complete guide'
  steps:
  - name: import required classes
    text: 'The following imports give you access to the redaction API:'
  - name: initialize redactor and apply regex pattern
    text: '`RegexRedaction` represents a redaction rule based on a regular‑expression
      pattern. The pattern you provide determines which text fragments are replaced.
      - **Regex explanation**: The pattern `\b\d{3}-\d{2}-\d{4}\b` matches U.S. Social
      Security numbers (three digits, a dash, two digits, a dash, four '
  - name: configure save options
    text: '`SaveOptions` controls how the redacted file is written. Adding a suffix
      makes it clear which files have been processed, while preserving the original
      format avoids unwanted conversion. - **Save options**: `setAddSuffix(true)`
      automatically appends “_redacted” to the output filename, preventing acci'
  - name: customize additional save settings
    text: 'You can further tailor the output—such as preserving metadata or flattening
      annotations—by adjusting the `SaveOptions` object. - **Key configuration**:
      Setting `setPreserveMetadata(true)` retains original document properties, which
      is often required for compliance audits.'
  type: HowTo
- questions:
  - answer: It automatically appends a suffix (e.g., `_redacted`) to the output filename,
      making it obvious which files have been processed.
    question: What is the purpose of `setAddSuffix(true)` in SaveOptions?
  - answer: Absolutely. Any valid Java regular expression can be supplied to `RegexRedaction`
      to target emails, phone numbers, custom IDs, etc.
    question: Can I use regex patterns other than numbers for text redaction?
  - answer: Wrap the redaction logic in a try‑catch block, log the exception, and
      always close the `Redactor` in a finally clause to release resources.
    question: How should I handle errors during redaction?
  - answer: Yes. GroupDocs.Redaction works with PDF, DOCX, PPTX, and many other formats.
    question: Is PDF redaction supported?
  - answer: Use batch processing, keep regex patterns simple, and monitor memory usage
      with profiling tools.
    question: What are best practices for large‑scale redaction projects?
  type: FAQPage
tags:
- text redaction
- GroupDocs.Redaction
- Java document processing
- regex redaction
- PDF redaction
title: 'كيفية إخفاء النص في Java باستخدام GroupDocs.Redaction: دليل شامل'
type: docs
url: /ar/java/text-redaction/master-text-redaction-java-groupdocs-redaction-guide/
weight: 1
---

# كيفية حذف النص في Java باستخدام GroupDocs.Redaction: دليل كامل

في عالم الرقمية السريع اليوم، **كيفية حذف النص** في المستندات هي سؤال يواجهه العديد من المطورين. سواء كنت تحمي البيانات الشخصية، أو تلتزم باللوائح، أو ببساطة تنظف المسودات، يوجهك هذا الدليل لاستخدام GroupDocs.Redaction للـ Java لتطبيق **الحذف القائم على regex بسرعة وأمان**. ستتعلم لماذا يعتبر الحذف مهمًا، وكيفية تكوين المكتبة، ونصائح الممارسات المثلى لمعالجة عالية الأداء.

## إجابات سريعة
- **ما هو الغرض الأساسي من GroupDocs.Redaction؟** يوفر API موثوق لتحديد وإخفاء النص الحسّاس في أكثر من 50 صيغة مستند.  
- **كيف يمكنني تطبيق regex للحذف؟** أنشئ كائن `RegexRedaction` بالنمط الخاص بك ومرره إلى طريقة `Redactor.apply()`.  
- **هل أحتاج إلى ترخيص؟** الإصدار التجريبي المجاني يكفي للتطوير؛ الترخيص المدفوع يفتح جميع الميزات للإنتاج.  
- **هل يمكنني حذف ملفات PDF وكذلك ملفات DOCX؟** نعم—GroupDocs.Redaction يدعم PDF وDOCX وPPTX والعديد من الصيغ الأخرى.  
- **ما هي أفضل طريقة لتحسين الأداء؟** أغلق كائنات `Redactor` بسرعة، حافظ على بساطة أنماط regex، وعالج الملفات على دفعات.

## ما هو حذف النص ولماذا هو مهم؟
حذف النص يزيل أو يغطي بشكل دائم المعلومات الحسّاسة من المستند، مما يضمن أن البيانات السرية—مثل أرقام الضمان الاجتماعي، تفاصيل بطاقات الائتمان، أو السجلات الطبية—لا يمكن استعادتها أو رؤيتها من قبل أطراف غير مخوّلة. يتم ذلك عن طريق الكتابة فوق الأحرف الأصلية أو استبدالها بقناع، بحيث لا يمكن استخراج المحتوى المخفي عبر النسخ‑اللصق أو أدوات OCR. هذا يضمن الامتثال للوائح الخصوصية ويحمي الأفراد من سرقة الهوية أو خروقات البيانات.

## لماذا نستخدم regex لحذف النص؟
تسمح لك التعبيرات النمطية (regex) بتعريف أنماط مرنة تتطابق مع مجموعة واسعة من صيغ البيانات (مثل أرقام الهواتف، أرقام بطاقات الائتمان). باستخدام regex مع GroupDocs.Redaction تحصل على تحكم دقيق فيما يتم إخفاؤه، مع الحفاظ على تنفيذ مختصر وقابل للصيانة.

## المتطلبات المسبقة
قبل أن نبدأ، تأكد من وجود:

- **Java Development Kit (JDK)** مثبت (Java 8 أو أحدث).  
- إلمام أساسي بصياغة Java والتعبيرات النمطية.  
- بيئة تطوير متكاملة مثل **IntelliJ IDEA** أو **Eclipse** لتشغيل وتصحيح الكود.  

## إعداد GroupDocs.Redaction للـ Java
أولاً، أضف المكتبة إلى مشروعك.

### إعداد Maven
إذا كنت تستخدم Maven، أدرج ما يلي في ملف `pom.xml` الخاص بك:

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

### تحميل مباشر
بدلاً من ذلك، قم بتحميل أحدث ملف JAR من [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### التهيئة الأساسية
`Redactor` هو الفئة الأساسية التي تفتح المستند، تطبق قواعد الحذف، وتكتب الناتج.

بمجرد توفر المكتبة، يمكنك البدء في حذف المستندات:

```java
// Import the necessary classes from GroupDocs.Redaction
import com.groupdocs.redaction.Redactor;

public class RedactionExample {
    public static void main(String[] args) {
        // Initialize the redactor with your document path
        final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
        // Ensure you close resources after operations
        try { /* Your code here */ } finally { redactor.close(); }
    }
}
```

## كيفية حذف النص باستخدام regex في Java؟
تتضمن العملية تحميل الملف المصدر إلى كائن `Redactor`، إنشاء قاعدة `RegexRedaction` التي تحدد النمط المراد مطابقةه، تطبيق القاعدة باستخدام `redactor.apply()`، وأخيرًا حفظ المستند المعدل باستخدام `SaveOptions`. باتباع هذه الخطوات يمكنك تحديد وإخفاء أي سلاسل حسّاسة عبر الصيغ المدعومة بثقة.

فئة `Redactor` هي المكوّن الأساسي الذي يفتح المستند، يطبق قواعد الحذف، ويكتب ملف الإخراج. تدير الموارد داخليًا، لذا يجب إغلاقها بعد المعالجة لتحرير الذاكرة.

### الخطوة 1: استيراد الفئات المطلوبة
الاستيرادات التالية تمنحك الوصول إلى API الحذف:

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.redactions.RegexRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;
```

### الخطوة 2: تهيئة الـ redactor وتطبيق نمط regex
`RegexRedaction` تمثل قاعدة حذف تعتمد على نمط تعبير نمطي. النمط الذي تقدمه يحدد أي أجزاء من النص سيتم استبدالها.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
try {
    // Define a regex pattern to find sequences of numbers and apply a replacement color.
    // The pattern: Two digits, optional whitespace, two more digits, non-digit characters,
    // followed by six digits.
    redactor.apply(new RegexRedaction("\\d{2}\\s*\\d{2}[^\\d]*\\d{6}", 
        new ReplacementOptions(java.awt.Color.BLUE)));
```

- **شرح regex**: النمط `\b\d{3}-\d{2}-\d{4}\b` يطابق أرقام الضمان الاجتماعي الأمريكية (ثلاثة أرقام، شرطة، رقمين، شرطة، أربعة أرقام). `ReplacementOptions` يتيح لك اختيار تغطية سوداء صلبة أو قناع نص مخصص.

### الخطوة 3: تكوين خيارات الحفظ
`SaveOptions` تتحكم في طريقة كتابة الملف المحذوف. إضافة لاحقة تجعل من الواضح أي الملفات تم معالجتها، مع الحفاظ على الصيغة الأصلية لتجنب التحويل غير المرغوب فيه.

```java
    // Configure save options
    SaveOptions saveOptions = new SaveOptions();
    saveOptions.setAddSuffix(true);  // Adds suffix to indicate processing
    saveOptions.setRasterizeToPDF(false);  // Preserves original format

    // Save the redacted document
    redactor.save(saveOptions);
} finally {
    redactor.close();  // Always close resources to prevent memory leaks
}
```

- **خيارات الحفظ**: `setAddSuffix(true)` يضيف تلقائيًا “_redacted” إلى اسم ملف الإخراج، مما يمنع الكتابة فوق الملفات عن طريق الخطأ.

### الخطوة 4: تخصيص إعدادات الحفظ الإضافية
يمكنك تعديل الإخراج أكثر—مثل الحفاظ على البيانات الوصفية أو تسطيح التعليقات التوضيحية—عن طريق تعديل كائن `SaveOptions`.

```java
import com.groupdocs.redaction.options.SaveOptions;

SaveOptions saveOptions = new SaveOptions();
saveOptions.setAddSuffix(true);  // Indicates processing by adding a suffix
saveOptions.setRasterizeToPDF(false);  // Keeps original format intact
```

- **التكوين الرئيسي**: ضبط `setPreserveMetadata(true)` يحتفظ بخصائص المستند الأصلية، وهو ما يُطلب غالبًا في عمليات التدقيق للامتثال.

## تطبيقات عملية
سيناريوهات واقعية حيث **كيفية حذف النص** أمر أساسي:

1. **المستندات القانونية** – إخفاء معرفات العملاء قبل مشاركة المسودات مع مستشارين خارجيين.  
2. **السجلات الطبية** – تغطية أسماء المرضى، أرقام الهوية، أو أرقام الصحة للبقاء متوافقًا مع HIPAA.  
3. **التقارير المالية** – إزالة أرقام الحسابات السرية عند توزيع ملخصات ربع السنة.  

## اعتبارات الأداء
- **إدارة الذاكرة**: دائمًا استدعِ `redactor.close()` لتحرير مقبض الملف والموارد الأصلية.  
- **regex فعال**: الأنماط الأبسط تعمل أسرع؛ تجنّب التتبع الخلفي الزائد باستخدام مجموعات ذرية عندما يكون ذلك ممكنًا.  
- **معالجة دفعات**: لمجموعات المستندات الكبيرة، عالج الملفات على دفعات من 20 إلى 50 للحفاظ على استهلاك الذاكرة ثابتًا.

## المشكلات الشائعة والحلول
| المشكلة | الحل |
|-------|----------|
| **Regex يطابق أكثر من اللازم** | اختبر نمطك باستخدام أداة اختبار regex على الإنترنت وقم بتضييق فئات الأحرف. |
| **تعارض اسم ملف الإخراج** | استخدم `setAddSuffix(true)` أو قدم مسار إخراج مخصص عبر `saveOptions.setOutputPath()`. |
| **تسرب الذاكرة في ملفات PDF الكبيرة** | عالج ملفات PDF صفحةً بصفحة أو زد حجم heap للـ JVM (`-Xmx2g`). |

## الأسئلة المتكررة

**س: ما هو الغرض من `setAddSuffix(true)` في SaveOptions؟**  
ج: يضيف تلقائيًا لاحقة (مثل `_redacted`) إلى اسم ملف الإخراج، مما يجعل من الواضح أي الملفات تم معالجتها.

**س: هل يمكنني استخدام أنماط regex غير الأرقام لحذف النص؟**  
ج: بالتأكيد. أي تعبير نمطي Java صالح يمكن تمريره إلى `RegexRedaction` لاستهداف البريد الإلكتروني، أرقام الهواتف، المعرفات المخصصة، إلخ.

**س: كيف يجب أن أتعامل مع الأخطاء أثناء عملية الحذف؟**  
ج: غلف منطق الحذف داخل كتلة try‑catch، سجّل الاستثناء، وتأكد دائمًا من إغلاق `Redactor` في كتلة finally لتحرير الموارد.

**س: هل يدعم حذف PDF؟**  
ج: نعم. GroupDocs.Redaction يعمل مع PDF وDOCX وPPTX والعديد من الصيغ الأخرى.

**س: ما هي أفضل الممارسات لمشاريع الحذف على نطاق واسع؟**  
ج: استخدم معالجة الدفعات، حافظ على بساطة أنماط regex، وراقب استهلاك الذاكرة باستخدام أدوات التحليل.

## موارد إضافية
- **التوثيق**: [GroupDocs Redaction Documentation](https://docs.groupdocs.com/redaction/java/)  
- **مرجع API**: [GroupDocs API Reference](https://apireference.groupdocs.com/redaction/java)

---

**آخر تحديث:** 2026-08-20  
**تم الاختبار مع:** GroupDocs.Redaction 24.9 للـ Java  
**المؤلف:** GroupDocs

## دروس ذات صلة

- [Mask Sensitive Data Java – GroupDocs.Redaction Guide](/redaction/java/getting-started/)
- [Mask Sensitive Data Java – Redact Personal Info with GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)
- [How to Redact PDF with Aspose OCR and Java - Implementing Regex Patterns using GroupDocs.Redaction](/redaction/java/ocr-integration/aspose-ocr-java-pdf-redaction/)