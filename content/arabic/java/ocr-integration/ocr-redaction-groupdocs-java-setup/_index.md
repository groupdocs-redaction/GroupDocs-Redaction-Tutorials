---
date: '2026-06-26'
description: تعلم كيفية استخراج النص من ملفات PDF الممسوحة ضوئياً وإخفاء البيانات
  الحساسة باستخدام GroupDocs OCR Redaction مع Azure OCR. قم بحجب رقم الضمان الاجتماعي
  واستبدال المعلومات السرية في PDF بكفاءة.
keywords:
- extract text scanned pdf
- redact social security number
- mask sensitive data pdf
- replace confidential info pdf
schemas:
- author: GroupDocs
  dateModified: '2026-06-26'
  description: Learn how to extract text scanned PDF and mask sensitive data using
    GroupDocs OCR Redaction with Azure OCR. Redact social security number and replace
    confidential info PDF efficiently.
  headline: Extract Text Scanned PDF – Mask Data with GroupDocs OCR
  type: TechArticle
- questions:
  - answer: OCR redaction uses Optical Character Recognition to extract hidden text
      from images or scanned PDFs, then applies redaction rules to mask that text.
    question: What is OCR redaction?
  - answer: Yes, but OCR dramatically improves accuracy on scanned documents where
      native text extraction fails.
    question: Can I use GroupDocs Redaction without Azure OCR?
  - answer: Build and test them incrementally, using Java’s `Pattern` class in a sandbox
      before applying to large documents.
    question: How do I handle complex regex patterns?
  - answer: Large PDFs, overly complex regex, and synchronous OCR calls can slow processing;
      consider batch processing and optimized patterns.
    question: What are typical performance bottlenecks?
  - answer: Absolutely—reach out via the [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33)
      for community help or contact GroupDocs support.
    question: Is support available for implementation issues?
  type: FAQPage
title: استخراج النص من ملفات PDF الممسوحة ضوئياً – إخفاء البيانات باستخدام GroupDocs
  OCR
type: docs
url: /ar/java/ocr-integration/ocr-redaction-groupdocs-java-setup/
weight: 1
---

# استخراج النص من ملفات PDF الممسوحة ضوئياً – إخفاء البيانات باستخدام GroupDocs OCR

في عالم اليوم القائم على البيانات، **استخراج النص من ملفات PDF الممسوحة ضوئياً** وإخفاء المعلومات السرية خطوة لا يمكن التفاوض عليها للامتثال. يشرح هذا الدليل كيفية استخدام GroupDocs Redaction مع Microsoft Azure OCR للتعرف بثقة على النص المخفي في الصفحات الممسوحة واستبداله ببديل آمن مثل **`[REDACTED]`**. ستلاحظ لماذا هذه المجموعة سريعة ودقيقة وجاهزة لأحمال العمل من مستوى الإنتاج.

## إجابات سريعة
- **ماذا يعني “إخفاء البيانات الحساسة”؟** إنه يستبدل النص السري المحدد ببديل (مثل `[REDACTED]`).  
- **أي مكتبة تتعامل مع OCR؟** Microsoft Azure OCR connector, used through GroupDocs Redaction.  
- **هل أحتاج إلى ترخيص؟** نسخة تجريبية مجانية تعمل للتقييم؛ الترخيص الدائم مطلوب للإنتاج.  
- **هل يمكنني إخفاء (تعتيم) ملفات PDF الممسوحة ضوئياً؟** نعم—يقوم OCR باستخراج النص المخفي قبل تطبيق عمليات التعتيق باستخدام regex.  
- **هل هذا الحل مخصص لجافا فقط؟** المثال مبني على جافا، لكن GroupDocs توفر واجهات برمجة تطبيقات مماثلة لـ .NET وغيرها من المنصات.

## ما هو التعتيق القائم على OCR؟
يقوم التعتيق القائم على OCR أولاً بتشغيل OCR على كل صفحة، محولاً الصور إلى نص قابل للبحث، ثم يطبق أنماط regex لاستبدال التطابقات ببديل مثل `[REDACTED]`. تسمح لك هذه العملية ذات الخطوتين بإخفاء البيانات الشخصية بثقة حتى في ملفات PDF الممسوحة، مما يضمن إزالة أي سلاسل حساسة قبل مشاركة أو أرشفة المستند.

## لماذا تستخدم GroupDocs Redaction مع Azure OCR؟
يجب عليك استخدام GroupDocs Redaction مع Azure OCR لأنه يوفر **دقة OCR تزيد عن 98 % للنص المطبوع**، يدعم **أكثر من 50 تنسيق إدخال وإخراج**، ويمكنه معالجة **ملفات PDF مئات الصفحات دون تحميل الملف بالكامل في الذاكرة**، مما يضمن تعتيقًا سريعًا وقابلًا للتوسع للامتثال. كما أن الحل **يستطيع معالجة ملف PDF مكون من 1,000 صفحة في أقل من دقيقتين على خادم بثمانية أنوية**، مما يجعل وظائف الدُفعات عملية.

## المتطلبات المسبقة
- **Java Development Kit (JDK) 8+** مثبت.  
- **Maven** (إذا كنت تفضل إدارة الاعتمادات) أو القدرة على تنزيل ملفات JAR يدويًا.  
- **Microsoft Azure OCR credentials** (نقطة النهاية ومفتاح الاشتراك).  
- معرفة أساسية بجافا وإلمام بالتعابير النمطية (regular expressions).

## إعداد GroupDocs Redaction لجافا

### إعداد Maven
أضف مستودع GroupDocs والاعتماد إلى ملف `pom.xml` الخاص بك:

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

### التحميل المباشر
إذا كنت تفضل إدارة ملفات JAR يدويًا، احصل على أحدث إصدار من [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### الحصول على الترخيص
- **Free Trial** – استكشاف جميع الميزات بدون تكلفة.  
- **Temporary License** – تمديد فترة التقييم.  
- **Full License** – إتاحة قدرات جاهزة للإنتاج.

### التهيئة الأساسية والإعداد
فئة `Redactor` هي المحرك الأساسي الذي يقوم باستخراج OCR وتطبيق قواعد التعتيق على مستندات PDF.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.RedactorSettings;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.examples.java.helper_classes.MicrosoftAzureOcrConnector;

// Initialize the OCR connector with Microsoft Azure
RedactorSettings settings = new RedactorSettings(new MicrosoftAzureOcrConnector());
```

## كيفية إخفاء البيانات الحساسة باستخدام التعتيق عبر OCR
يتضمن إخفاء البيانات الحساسة باستخدام التعتيق عبر OCR تحميل ملف PDF بإعدادات Azure OCR، تعريف أنماط regex للبيانات التي تريد إخفاءها، واستدعاء Redactor لاستبدال كل تطابق ببديل مثل `[REDACTED]`. تتولى المكتبة عملية OCR، مطابقة الأنماط، وإعادة كتابة PDF في سير عمل واحد.

### الخطوة 1: تحميل المستند بإعدادات OCR
`LoadOptions` يحدد كيفية تحميل GroupDocs للملف، مما يتيح لك تمرير موصلات OCR مثل Azure.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;

// Load your document with OCR settings
try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf", 
    new LoadOptions(), settings)) {
    // Further operations will go here
}
```
- **`YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf`** – استبدله بمسار ملف PDF الخاص بك.  
- **`settings`** – يحتوي على موصل Azure OCR الذي أنشأته مسبقًا.

### الخطوة 2: تعريف وتطبيق تعتيقات Regex
`ReplacementOptions` يحدد نص الاستبدال الذي سيحل محل كل تطابق regex أثناء التعتيق.

```java
import com.groupdocs.redaction.redactions.RegexRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

// Define the regex for sensitive data (e.g., Social Security Numbers)
RegexRedaction redaction = new RegexRedaction("\\b\\d{3}-\\d{2}-\\d{4}\\b", 
    new ReplacementOptions("[REDACTED]"));

// Apply redaction
redactor.apply(redaction);

// Save the document after redactions
redactor.save(new SaveOptions());
```
- النمط `\b\d{3}-\d{2}-\d{4}\b` يطابق أرقام الضمان الاجتماعي الأمريكية.  
- `ReplacementOptions("[REDACTED]")` يستبدل كل تطابق بالبديل، مما يؤدي فعليًا إلى **إخفاء البيانات الحساسة**.

## حالات الاستخدام الشائعة لإخفاء البيانات الحساسة
1. **Legal Document Management** – إخفاء معرفات العملاء قبل مشاركة المسودات.  
2. **Financial Reporting** – حماية أرقام الحسابات ومعرفات المعاملات.  
3. **Healthcare Records** – الامتثال لـ HIPAA عبر تعتيم معرفات المرضى.  
4. **Government Publications** – إزالة البيانات الشخصية من السجلات العامة.  
5. **Corporate Contracts** – إخفاء الشروط الملكية أثناء المراجعات الخارجية.

## نصائح الأداء
- **Optimize regex** – تجنب الأنماط الواسعة جدًا التي تزيد من وقت المعالجة؛ التعبيرات المصممة جيدًا يمكن أن تقلل زمن التنفيذ حتى 40 %.  
- **Memory Management** – أغلق كائن `Redactor` فورًا (try‑with‑resources يقوم بذلك تلقائيًا).  
- **Asynchronous Execution** – للمعالجة الجماعية، نفّذ وظائف التعتيق على خيوط منفصلة أو استخدم طابور مهام للحفاظ على استجابة واجهة المستخدم.

## استكشاف الأخطاء وإصلاحها
- **Azure credentials error** – تحقق مرة أخرى من عنوان URL لنقطة النهاية ومفتاح الاشتراك في `MicrosoftAzureOcrConnector`.  
- **Document not loading** – تحقق من مسار الملف وتأكد من أن PDF غير محمي بكلمة مرور (أو قدم كلمة المرور عبر `LoadOptions`).  
- **No redactions applied** – اختبر regex الخاص بك باستخدام سلسلة بسيطة أولاً؛ استخدم `Pattern.compile` في اختبار وحدة لتأكيد التطابقات.

## الأسئلة المتكررة

**س: ما هو التعتيق عبر OCR؟**  
ج: يستخدم التعتيق عبر OCR تقنية التعرف الضوئي على الأحرف لاستخراج النص المخفي من الصور أو ملفات PDF الممسوحة، ثم يطبق قواعد التعتيق لإخفاء ذلك النص.

**س: هل يمكنني استخدام GroupDocs Redaction بدون Azure OCR؟**  
ج: نعم، لكن OCR يحسن الدقة بشكل كبير في المستندات الممسوحة حيث يفشل استخراج النص الأصلي.

**س: كيف أتعامل مع أنماط regex المعقدة؟**  
ج: قم ببنائها واختبارها تدريجيًا، باستخدام فئة `Pattern` في جافا داخل بيئة اختبار قبل تطبيقها على مستندات كبيرة.

**س: ما هي عنق الزجاجة الشائعة في الأداء؟**  
ج: ملفات PDF الكبيرة، regex المعقدة جدًا، والاتصالات المتزامنة مع OCR يمكن أن تبطئ المعالجة؛ فكر في المعالجة الدُفعية والأنماط المحسّنة.

**س: هل يتوفر دعم لمشكلات التنفيذ؟**  
ج: بالتأكيد—تواصل عبر [منتدى GroupDocs](https://forum.groupdocs.com/c/redaction/33) للحصول على مساعدة المجتمع أو اتصل بدعم GroupDocs.

## موارد إضافية
- **Documentation**: https://docs.groupdocs.com/redaction/java/  
- **API Reference**: https://reference.groupdocs.com/redaction/java  
- **Download**: https://releases.groupdocs.com/redaction/java/  
- **GitHub**: https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java  
- **Free Support**: https://forum.groupdocs.com/c/redaction/33  
- **Temporary License**: https://purchase.groupdocs.com/temporary-license/

---

**آخر تحديث:** 2026-06-26  
**تم الاختبار مع:** GroupDocs.Redaction 24.9 (Java)  
**المؤلف:** GroupDocs  

## دروس ذات صلة

- [تعتيم PDF الآمن باستخدام OCR – GroupDocs.Redaction Java](/redaction/java/ocr-integration/)
- [كيفية تعتيم النص باستخدام GroupDocs.Redaction لجافا](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction/)
- [إخفاء البيانات الحساسة جافا – تعتيم المعلومات الشخصية باستخدام GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)