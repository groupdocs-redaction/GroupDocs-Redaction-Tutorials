---
date: '2026-08-20'
description: تعلم كيفية إخفاء النص في مستندات Java باستخدام GroupDocs.Redaction، مع
  تغطية exact‑phrase، regex، color replacement، annotation و metadata redaction لضمان
  الامتثال الآمن.
keywords:
- how to redact text
- replace text with color
- GroupDocs.Redaction Java
- Java document security
- document redaction library
lastmod: '2026-08-20'
og_description: تعلم كيفية إخفاء النص في مستندات Java باستخدام GroupDocs.Redaction،
  مع تغطية exact‑phrase، regex، color replacement، annotation و metadata redaction.
og_image_alt: Guide showing Java code redacting text with GroupDocs.Redaction
og_title: كيفية إخفاء النص في مستندات Java باستخدام GroupDocs.Redaction
schemas:
- author: GroupDocs
  dateModified: '2026-08-20'
  description: Learn how to redact text in Java documents using GroupDocs.Redaction,
    covering exact‑phrase, regex, color replacement, annotation and metadata redaction
    for secure compliance.
  headline: How to redact text in Java documents with GroupDocs.Redaction
  type: TechArticle
- description: Learn how to redact text in Java documents using GroupDocs.Redaction,
    covering exact‑phrase, regex, color replacement, annotation and metadata redaction
    for secure compliance.
  name: How to redact text in Java documents with GroupDocs.Redaction
  steps:
  - name: '**Add the Maven dependency** (or include the JAR).'
    text: '**Add the Maven dependency** (or include the JAR).'
  - name: '**Configure your license** by calling `License.setLicense("path/to/license.lic")`
      early in your application.'
    text: '**Configure your license** by calling `License.setLicense("path/to/license.lic")`
      early in your application.'
  - name: '**Create a `Redactor` instance** pointing at the source document.'
    text: '**Create a `Redactor` instance** pointing at the source document.'
  - name: '**Initialize the Redactor** with the document you want to process:'
    text: '**Initialize the Redactor** with the document you want to process:'
  - name: '**Define the exact‑phrase rule** and apply it:'
    text: '**Define the exact‑phrase rule** and apply it:'
  - name: '**Save the redacted file** to your output folder:'
    text: '**Save the redacted file** to your output folder:'
  - name: 'Load the document:'
    text: 'Load the document:'
  - name: 'Create a regex rule and apply it:'
    text: 'Create a regex rule and apply it:'
  - name: 'Save the result:'
    text: 'Save the result:'
  - name: 'Load the document:'
    text: 'Load the document:'
  type: HowTo
- questions:
  - answer: Yes. Create each redaction object, call `redactor.apply()` for each, then
      save once.
    question: Can I combine multiple redaction rules in a single pass?
  - answer: Absolutely. Pass the password to the `Redactor` constructor that accepts
      a `LoadOptions` object.
    question: Does GroupDocs.Redaction support password‑protected files?
  - answer: You can call `redactor.preview()` to generate a temporary view that highlights
      the areas to be redacted.
    question: Is it possible to preview redactions before saving?
  - answer: DOCX, PDF, PPTX, XLSX, PNG, JPEG, BMP, and many more—over 30 formats in
      total.
    question: What file formats are supported?
  - answer: Use the metadata erasure feature, remove annotations, and apply exact‑phrase
      or regex redactions to all personal data fields.
    question: How do I ensure the redacted document complies with GDPR?
  type: FAQPage
tags:
- text redaction
- GroupDocs.Redaction
- Java document security
- regex redaction
- metadata removal
title: كيفية إخفاء النص في مستندات Java باستخدام GroupDocs.Redaction
type: docs
url: /ar/java/text-redaction/java-redaction-guide-groupdocs-document-security/
weight: 1
---

# كيف يتم إخفاء النص في مستندات Java باستخدام GroupDocs.Redaction

في التطبيقات الحديثة، **كيفية إخفاء النص** داخل ملفات PDF أو Word أو الصور هي متطلب شائع للامتثال والخصوصية. سواء كنت بحاجة إلى إخفاء المعرفات الشخصية، أو إزالة التعليقات التوضيحية السرية، أو حذف البيانات الوصفية، فإن GroupDocs.Redaction للـ Java يوفّر لك طريقة برمجية نظيفة لتحقيق **أمان مستندات Java**. يشرح هذا الدليل كل خطوة أساسية — من إعداد المكتبة إلى تطبيق إخفاءات العبارة الدقيقة، regex، الإخفاء بناءً على اللون، التعليقات التوضيحية، والبيانات الوصفية — بحيث يمكنك دمج الإخفاء مباشرةً في خدمات الخلفية الخاصة بك.

## إجابات سريعة
- **ما المكتبة التي تتعامل مع إخفاء مستندات Java؟** GroupDocs.Redaction للـ Java.  
- **هل يمكنني استبدال النص باللون بدلاً من حذفه؟** نعم، استخدم ميزة “استبدال النص باللون”.  
- **هل أحتاج إلى ترخيص للاستخدام في الإنتاج؟** يلزم ترخيص مؤقت أو مدفوع للحصول على الوظائف الكاملة.  
- **ما إصدارات Java المدعومة؟** JDK 8 أو أعلى.  
- **هل Maven هو الطريقة الوحيدة لإضافة المكتبة؟** يُفضَّل Maven، لكن يمكنك أيضًا تنزيل ملف JAR يدويًا.

## ما هو “كيفية إخفاء النص” في Java؟
**الإخفاء يزيل أو يغطي المحتوى الحساس بشكل دائم بحيث لا يمكن استعادته.** في Java، تقوم بتحميل الملف، تعريف ما تريد إخفائه، تطبيق الإخفاء، وحفظ النسخة المنقاة. يضمن ذلك أن أي مستهلك لاحق يرى المستند المنظف فقط.

## لماذا نستخدم GroupDocs.Redaction للـ Java؟
حمّل ملفك، عرّف قاعدة، ويتولى SDK كل الجهد. يدعم GroupDocs.Redaction **أكثر من 30 صيغة** — بما في ذلك DOCX، PDF، PPTX، XLSX، PNG، JPEG، BMP — ويعالج المستندات الكبيرة عبر بنية تعتمد على التدفق. يوفّر إخفاءات العبارة الدقيقة، regex، الإخفاء باللون، التعليقات التوضيحية، والبيانات الوصفية، مما يمنحك تحكمًا دقيقًا لتلبية GDPR، HIPAA، وغيرها من اللوائح.

## المتطلبات المسبقة
- **مجموعة تطوير Java (JDK) 8+** مثبتة على جهازك.  
- **Maven** لإدارة الاعتمادات (أو يمكنك تنزيل ملف JAR يدويًا).  

### المكتبات والاعتمادات المطلوبة
أضف مستودع GroupDocs واعتماد Redaction إلى ملف `pom.xml` الخاص بك:

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

يمكنك أيضًا تنزيل أحدث ملف JAR من صفحة الإصدارات الرسمية: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### الحصول على الترخيص
للاستخدام في الإنتاج، احصل على ترخيص مؤقت أو كامل. تتوفر نسخة تجريبية مجانية لأغراض التقييم.

## إعداد GroupDocs.Redaction للـ Java
1. **أضف اعتماد Maven** (أو أدرج ملف JAR).  
2. **قم بتكوين الترخيص** عبر استدعاء `License.setLicense("path/to/license.lic")` مبكرًا في تطبيقك.  
   `License` هو الصنف المستخدم لتحميل وتطبيق ملف ترخيص GroupDocs Redaction.  
3. **أنشئ كائن `Redactor`** يشير إلى المستند المصدر.

**الصنف `Redactor` هو المحرك الأساسي الذي يحمل، يعدّل، ويحفظ المستندات بطريقة فعّالة في الذاكرة.** بمجرد حصولك على كائن `Redactor`، يمكنك ربط عدة قواعد إخفاء قبل حفظ النتيجة.

الآن أنت جاهز للبدء في الإخفاء.

## دليل التنفيذ

### إخفاء العبارة الدقيقة
استبدل عبارة محددة (مثل اسم شخص) بنص نائب.

#### كيف يعمل إخفاء العبارة الدقيقة؟
`ExactPhraseRedaction` يمثل قاعدة تزيل أو تستبدل سلسلة نصية دقيقة. حمّل المستند، أنشئ قاعدة `ExactPhraseRedaction` التي تستهدف السلسلة المحددة، طبّق القاعدة، واحفظ الناتج. يقوم SDK تلقائيًا بمسح النص المطابق مع الحفاظ على التخطيط.

1. **ابدأ الـ Redactor** بالمستند الذي تريد معالجته:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. **عرّف قاعدة العبارة الدقيقة** وطبّقها:

```java
ExactPhraseRedaction redaction = new ExactPhraseRedaction(
    "John Doe", 
    new ReplacementOptions("[Client]"));

redactor.apply(redaction);
```

3. **احفظ الملف المُخفى** إلى مجلد الإخراج الخاص بك:

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Redaction applied successfully.");
}
```

### إخفاء regex مع استبدال النص
استخدم التعابير النمطية لتحديد أنماط مثل أرقام السيريال واستبدالها برمز عام.

#### كيف يعمل إخفاء regex مع الاستبدال؟
`RegexRedaction` يعرّف قاعدة تعتمد على تعبير نمطي للعثور على النص المطابق وتعديله. تزود محرك الإخفاء كائن `RegexRedaction` يحتوي على النمط وسلسلة الاستبدال. يقوم المحرك بمسح المستند، يستبدل كل تطابق، ويحافظ على التنسيق المحيط.

1. حمّل المستند:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. أنشئ قاعدة regex وطبّقها:

```java
RegexRedaction redaction = new RegexRedaction(
    "Redaction",
    new ReplacementOptions("[Product]"));

redactor.apply(redaction);
```

3. احفظ النتيجة:

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Redaction applied successfully.");
}
```

### إخفاء regex مع استبدال اللون
بدلاً من حذف النص، يمكنك **استبدال النص باللون** لإخفائه بصريًا مع إبقاء الأحرف الأساسية في الملف.

#### كيف يختلف الإخفاء باللون عن الحذف؟
يقوم SDK بطلاء النص المطابق باللون المختار، مما يجعله غير قابل للقراءة بالعين المجردة لكنه لا يزال موجودًا في تدفق الملف. هذا مفيد عندما تحتاج إلى الحفاظ على بنية المستند للمعالجة اللاحقة.

1. حمّل المستند:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. عرّف نمط regex وحدد لون الاستبدال (مثلاً أزرق):

```java
RegexRedaction redaction = new RegexRedaction(
    "\d{2}\s*\d{2}[^\\d]*\d{6}", 
    new ReplacementOptions(Color.BLUE));

redactor.apply(redaction);
```

3. احفظ الملف المحدث:

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Redaction applied successfully.");
}
```

### إخفاء التعليقات التوضيحية (حذفها)
إزالة جميع التعليقات التوضيحية (التعليقات، التظليل، إلخ) من المستند للحصول على نسخة نهائية أنظف.

#### كيف تُزيل التعليقات التوضيحية في خطوة واحدة؟
`AnnotationRedaction` هي قاعدة تزيل التعليقات التوضيحية مثل التعليقات، التظليل، والطوابع. أنشئ قاعدة `AnnotationRedaction` التي تستهدف جميع أنواع التعليقات، طبّقها، واحفظ التغييرات.

1. حمّل ملفك:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. طبّق قاعدة حذف التعليقات:

```java
DeleteAnnotationRedaction redaction = new DeleteAnnotationRedaction();

redactor.apply(redaction);
```

3. احفظ التغييرات:

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Annotations deleted successfully.");
}
```

### إخفاء البيانات الوصفية
إزالة كل قطعة من البيانات الوصفية (المؤلف، تاريخ الإنشاء، الخصائص المخصصة) لحماية الخصوصية وتلبية معايير الامتثال.

#### كيف يضمن مسح البيانات الوصفية الخصوصية؟
`MetadataRedaction` يمسح الحقول المدمجة والمخصصة للبيانات الوصفية من المستند. تقوم قاعدة `MetadataRedaction` بمسح جميع الحقول، مما يضمن عدم بقاء أي معرفات مخفية في حزمة خصائص الملف.

1. افتح المستند:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. طبّق قاعدة مسح البيانات الوصفية:

```java
EraseMetadataRedaction redaction = new EraseMetadataRedaction(MetadataFilters.All);

redactor.apply(redaction);
```

3. احفظ المستند المنقّى:

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Metadata erased successfully.");
}
```

## تطبيقات عملية (لماذا هذا مهم)
- **إعداد المستندات القانونية** – إخفاء أسماء العملاء قبل مشاركة المسودات مع الطرف المقابل.  
- **الامتثال الصحي** – إزالة معرفات المرضى للبقاء متوافقًا مع HIPAA دون تعديل يدوي.  
- **حماية بيانات الشركات** – إخفاء الأرقام المالية أو الأسرار التجارية في التقارير الداخلية قبل توزيعها.  

أتمتة هذه الخطوات تقلل الجهد اليدوي، تقضي على الأخطاء البشرية، وتضمن امتثالًا ثابتًا عبر آلاف الملفات.

## اعتبارات الأداء
- **استخدام التدفق بدلاً من التحميل الكامل** – للملفات الكبيرة، استخدم مُنشئات `Redactor` التي تقبل `InputStream` لتجنب تحميل المستند بالكامل في الذاكرة.  
- **تجميع نمط regex مسبقًا** عندما تقوم بتطبيق نفس الإخفاء مرارًا؛ هذا يقلل استهلاك المعالج بنسبة تصل إلى 30 %.  
- **مراقبة ذاكرة JVM** – الإخفاء قد يكون كثيف الذاكرة؛ فكر في زيادة حجم الكومة (`-Xmx2g`) لمعالجة دفعات من الأرشيفات متعددة الجيجابايت.

## المشكلات الشائعة & استكشاف الأخطاء
| العَرَض | السبب المحتمل | الحل |
|---------|--------------|-----|
| لا توجد تغييرات بعد `apply` | مسار الملف غير صحيح أو الملف مقفل | تحقق من مسار الملف وتأكد من عدم فتح المستند في مكان آخر |
| regex لا يتطابق | خطأ في صياغة النمط | اختبر regex باستخدام أداة اختبار على الإنترنت؛ تأكد من هروب الشرطات المائلة بشكل صحيح |
| استبدال اللون غير مرئي | تنسيق الإخراج لا يدعم لون النص (مثل نص عادي) | استخدم صيغة مثل DOCX أو PDF التي تحتفظ بالتنسيق |
| خطأ ترخيص أثناء التشغيل | ملف الترخيص مفقود أو غير صالح | ضع ملف `.lic` في دليل يمكن الوصول إليه واستدعِ `License.setLicense` قبل أي استخدام للـ Redactor |

## الأسئلة المتكررة

**س: هل يمكنني دمج عدة قواعد إخفاء في تمريرة واحدة؟**  
ج: نعم. أنشئ كل كائن إخفاء، استدعِ `redactor.apply()` لكلٍ منها، ثم احفظ مرة واحدة.

**س: هل يدعم GroupDocs.Redaction الملفات المحمية بكلمة مرور؟**  
ج: بالتأكيد. مرّر كلمة المرور إلى مُنشئ `Redactor` الذي يقبل كائن `LoadOptions`.

**س: هل يمكن معاينة الإخفاءات قبل الحفظ؟**  
ج: يمكنك استدعاء `redactor.preview()` لتوليد عرض مؤقت يبرز المناطق التي ستُخفى.

**س: ما صيغ الملفات المدعومة؟**  
ج: DOCX، PDF، PPTX، XLSX، PNG، JPEG، BMP، والعديد غيرها — أكثر من 30 صيغة إجمالاً.

**س: كيف أضمن أن المستند المُخفى يتوافق مع GDPR؟**  
ج: استخدم ميزة مسح البيانات الوصفية، أزل التعليقات التوضيحية، وطبق إخفاءات العبارة الدقيقة أو regex على جميع حقول البيانات الشخصية.

## الخلاصة
أصبح لديك الآن دليل شامل من البداية إلى النهاية حول **كيفية إخفاء النص** في مستندات Java باستخدام GroupDocs.Redaction. باتباع الخطوات الخاصة بالعبارة الدقيقة، regex، الإخفاء باللون، التعليقات التوضيحية، والبيانات الوصفية، يمكنك تحقيق **أمان مستندات Java** قوي مع الحفاظ على نظافة وصيانة الكود. دمج هذه المقاطع في خدماتك الحالية، أتمتة المعالجة الدفعة، والبقاء متوافقًا مع لوائح الخصوصية.

---

**آخر تحديث:** 2026-08-20  
**تم الاختبار مع:** GroupDocs.Redaction 24.9 للـ Java  
**المؤلف:** GroupDocs

## دروس ذات صلة

- [replace metadata text java – Secure Redaction with GroupDocs](/redaction/java/metadata-redaction/java-redaction-metadata-text-replacement-guide/)
- [How to Redact Images in Word Documents Using GroupDocs.Redaction for Java – A Comprehensive Guide](/redaction/java/image-redaction/redact-images-word-docs-groupdocs-redaction-java/)
- [How to Redact Documents with GroupDocs Redaction Java License from File Path – A Step‑by‑Step Guide](/redaction/java/licensing-configuration/implement-groupdocs-redaction-java-license-file-path/)