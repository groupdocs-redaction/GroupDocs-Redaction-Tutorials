---
date: '2026-10-01'
description: تعلم كيفية إزالة بيانات تعريف المؤلف وحفظ ملفات المستندات المموهة في
  Java باستخدام GroupDocs Redaction.
keywords:
- remove author metadata
- save redacted document
- groupdocs metadata removal
lastmod: '2026-10-01'
og_description: تعلم كيفية إزالة بيانات تعريف المؤلف وحفظ ملفات المستندات المموهة
  في Java باستخدام GroupDocs Redaction. اتبع الدليل خطوة بخطوة.
og_image_alt: Guide showing Java code to remove author metadata using GroupDocs Redaction
og_title: كيفية إزالة بيانات تعريف المؤلف في Java باستخدام GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-10-01'
  description: Learn how to remove author metadata and save redacted document files
    in Java using GroupDocs Redaction.
  headline: How to remove author metadata in Java with GroupDocs
  type: TechArticle
- description: Learn how to remove author metadata and save redacted document files
    in Java using GroupDocs Redaction.
  name: How to remove author metadata in Java with GroupDocs
  steps:
  - name: '**Legal documents** – Redact author information before sending contracts
      to opposing counsel.'
    text: '**Legal documents** – Redact author information before sending contracts
      to opposing counsel.'
  - name: '**Corporate reports** – Remove manager names when publishing quarterly
      results to shareholders.'
    text: '**Corporate reports** – Remove manager names when publishing quarterly
      results to shareholders.'
  - name: '**Project files** – Clean up internal project documentation before archiving
      or uploading to a public repository.'
    text: '**Project files** – Clean up internal project documentation before archiving
      or uploading to a public repository.'
  type: HowTo
- questions:
  - answer: It removes selected metadata fields from a document.
    question: What does EraseMetadataRedaction do?
  - answer: GroupDocs.Redaction for Java.
    question: Which library provides this feature?
  - answer: A free trial works for testing; a permanent license is required for production.
    question: Do I need a license?
  - answer: Yes, combine filters with a logical OR.
    question: Can I target multiple fields at once?
  - answer: Redactor instances are not shared across threads; create a new instance
      per operation.
    question: Is the process thread‑safe?
  type: FAQPage
tags:
- metadata redaction
- GroupDocs
- Java document processing
title: كيفية إزالة بيانات تعريف المؤلف في Java باستخدام GroupDocs
type: docs
url: /ar/java/metadata-redaction/groupdocs-redaction-java-metadata-implementation/
weight: 1
---

# كيفية إزالة بيانات تعريف المؤلف في Java باستخدام GroupDocs

في المشهد الرقمي اليوم، حماية المعلومات الحساسة المخفية داخل المستندات هي ممارسة ضرورية. **إزالة بيانات تعريف المؤلف** تمنع الكشف العرضي عن المعرفات الشخصية أو المؤسسية. يوضح لك هذا الدليل، خطوة بخطوة، كيفية استخدام `EraseMetadataRedaction` من GroupDocs.Redaction for Java لإزالة الحقول مثل *Author* و *Manager* من ملفات Word، ثم **حفظ نسخ المستند المُحذوف** بأمان للمشاركة أو الأرشفة.

## إجابات سريعة
- **ما الذي يفعله EraseMetadataRedaction؟** يزيل حقول البيانات الوصفية المحددة من المستند.  
- **أي مكتبة توفر هذه الميزة؟** GroupDocs.Redaction for Java.  
- **هل أحتاج إلى ترخيص؟** النسخة التجريبية المجانية تعمل للاختبار؛ يلزم ترخيص دائم للإنتاج.  
- **هل يمكنني استهداف حقول متعددة في آن واحد؟** نعم، يمكن دمج الفلاتر باستخدام OR منطقي.  
- **هل العملية آمنة في بيئة متعددة الخيوط؟** لا يتم مشاركة كائنات Redactor عبر الخيوط؛ أنشئ كائنًا جديدًا لكل عملية.

## ما هو EraseMetadataRedaction؟
`EraseMetadataRedaction` هي فئة حجب مدمجة تتيح لك تحديد أي من إدخالات البيانات الوصفية يجب محوها. تعمل على مجموعة واسعة من صيغ المستندات المدعومة من قبل GroupDocs.Redaction، مما يضمن عدم تسرب معلومات المؤلف المخفية. يمكنك استهداف الخصائص القياسية مثل Author و Manager، وكذلك حقول البيانات الوصفية المخصصة، مما يوفر حماية شاملة للخصوصية.

## لماذا تستخدم EraseMetadataRedaction مع GroupDocs؟
GroupDocs.Redaction يدعم **أكثر من 100 صيغة إدخال وإخراج** ويمكنه معالجة مستندات تصل إلى 500 صفحة دون تحميل الملف بالكامل في الذاكرة. استخدام هذه الفئة يمنحك واجهة برمجة تطبيقات واحدة عالية الأداء لتلبية متطلبات GDPR أو HIPAA أو الامتثال الداخلي مع الحفاظ على بساطة قاعدة الكود الخاصة بك.

## المتطلبات المسبقة
- Java 8 أو أعلى مثبت.  
- Maven (أو القدرة على إضافة ملفات JAR يدويًا).  
- GroupDocs.Redaction for Java (الإصدار 24.9 أو أحدث).  
- ترخيص تجريبي صالح من GroupDocs أو ترخيص دائم.

## إعداد GroupDocs.Redaction لـ Java

### تثبيت Maven
أضف مستودع GroupDocs والاعتماد إلى ملف **pom.xml** الخاص بك:

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
بدلاً من ذلك، قم بتنزيل أحدث ملف JAR من [GroupDocs Redaction Java Docs](https://releases.groupdocs.com/redaction/java/).

### الحصول على الترخيص
احصل على نسخة تجريبية مجانية أو اشترِ ترخيصًا مؤقتًا من بوابة GroupDocs. يجب وضع ملف الترخيص في مكان يمكن لتطبيقك تحميله منه (مثلاً، جذر classpath).

### التهيئة الأساسية والإعداد
فيما يلي مثال بسيط ينشئ كائن `Redactor` لملف DOCX:

```java
import com.groupdocs.redaction.Redactor;

String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
Redactor redactor = new Redactor(filePath);
```

## كيفية استخدام EraseMetadataRedaction في Java
الأقسام التالية تقسم التنفيذ إلى خطوات واضحة وقابلة للتنفيذ.

### الميزة: تنظيف عناصر البيانات الوصفية المحددة

#### نظرة عامة
سنقوم بحذف حقول البيانات الوصفية **Author** و **Manager** باستخدام `EraseMetadataRedaction`. هذا طلب شائع عند مشاركة التقارير الداخلية مع شركاء خارجيين.

#### تنفيذ خطوة بخطوة

##### 1️⃣ تهيئة كائن Redactor
`Redactor` هي الفئة الأساسية التي تقوم بتحميل المستند، وتطبيق كائنات الحجب، وكتابة النتيجة. أنشئ كائنًا جديدًا لكل ملف تقوم بمعالجته:

```java
import com.groupdocs.redaction.Redactor;

String inputFilePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
final Redactor redactor = new Redactor(inputFilePath);
```

##### 2️⃣ تطبيق EraseMetadataRedaction
`MetadataFilters` توفر فلاتر معرفة مسبقًا لمفاتيح البيانات الوصفية الشائعة مثل Author و Manager.  
`EraseMetadataRedaction` يزيل إدخالات البيانات الوصفية التي تتطابق مع `MetadataFilters` المقدمة. يجمع عامل OR البتّي (`|`) فلاتر `Author` و `Manager` بحيث يتم حذف كلا الحقلين في استدعاء واحد:

```java
import com.groupdocs.redaction.redactions.EraseMetadataRedaction;
import com.groupdocs.redaction.MetadataFilters;

try {
    redactor.apply(new EraseMetadataRedaction(MetadataFilters.Author | MetadataFilters.Manager));
} finally {
    redactor.close();
}
```

##### 3️⃣ تكوين خيارات الحفظ
`SaveOptions` يتيح لك تحديد اسم ملف الإخراج، الصيغة، وغيرها من معلمات الحفظ.  
`SaveOptions` يتيح لك التحكم في اسم ملف الإخراج، الصيغة، وما إذا كان يجب تحويل المستند إلى PDF. إضافة لاحقة تحافظ على الملف الأصلي دون تعديل:

```java
import com.groupdocs.redaction.options.SaveOptions;

SaveOptions saveOptions = new SaveOptions();
saveOptions.setAddSuffix(true); // Adds "_Redacted" to the file name
saveOptions.setRasterizeToPDF(false);

redactor.save(saveOptions);
```

## حالات الاستخدام الشائعة
1. **الوثائق القانونية** – حذف معلومات المؤلف قبل إرسال العقود إلى المحاميين الخصمين.  
2. **التقارير المؤسسية** – إزالة أسماء المديرين عند نشر النتائج الفصلية للمساهمين.  
3. **ملفات المشاريع** – تنظيف وثائق المشروع الداخلية قبل الأرشفة أو رفعها إلى مستودع عام.

## نصائح استكشاف الأخطاء وإصلاحها
- **الملف غير موجود** – تحقق من أن المسار في `inputFilePath` يشير إلى ملف موجود وأن التطبيق يمتلك أذونات القراءة.  
- **حقول البيانات الوصفية المفقودة** – ليست جميع أنواع المستندات تخزن نفس مفاتيح البيانات الوصفية؛ تحقق من خصائص المستند في Office أولاً.  
- **أخطاء الترخيص** – تأكد من تحميل ملف الترخيص بشكل صحيح قبل إنشاء كائن `Redactor`.

## اعتبارات الأداء
- أغلق كائن `Redactor` بسرعة (كما هو موضح في كتلة `finally`) لتحرير الموارد الأصلية.  
- تجنب تحويل المستندات الكبيرة إلى صور ما لم تحتاج إلى معاينة PDF؛ يمكن أن يزيد التحويل من استهلاك المعالج والذاكرة حتى 3 أضعاف للملفات التي تتألف من 300 صفحة.

## الأسئلة المتكررة

**س1: ما هو حجب البيانات الوصفية؟**  
ج1: حجب البيانات الوصفية يتضمن إزالة خصائص المستند المخفية (مثل author أو manager أو العلامات المخصصة) لمنع الكشف العرضي عن المعلومات الحساسة.

**س2: هل يمكنني استخدام GroupDocs.Redaction لأنواع ملفات أخرى؟**  
ج2: نعم، تدعم المكتبة صيغ PDF و DOCX و PPTX و XLSX والعديد من الصيغ الأخرى—أكثر من 100 صيغ إجمالاً.

**س3: كيف أتعامل مع الأخطاء أثناء الحجب؟**  
ج3: ضع استدعاء `apply` داخل كتلة try‑catch وتأكد دائمًا من إغلاق `Redactor` في كتلة finally لضمان تحرير الموارد.

**س4: هل يمكن حجب حقول البيانات الوصفية المخصصة؟**  
ج5: بالتأكيد. استخدم `MetadataFilters.Custom("YourFieldName")` لاستهداف أي خاصية مخصصة مخزنة في المستند.

**س5: ما هي أفضل الممارسات لاستخدام GroupDocs.Redaction؟**  
ج5:  
- حمّل الترخيص مبكرًا في تطبيقك.  
- أغلق كائنات `Redactor` بسرعة.  
- استخدم `SaveOptions` لإضافة لاحقة، مع الحفاظ على الملفات الأصلية دون تعديل.  
- اختبر الحجب على نسخة من المستند قبل معالجة الدفعات.

**س6: هل يدعم EraseMetadataRedaction عمليات الدفعات؟**  
ج6: يمكنك التكرار عبر مجموعة من مسارات الملفات، وإنشاء `Redactor` جديد لكل ملف وتطبيق نفس منطق الحجب.

**س7: هل يمكنني دمج EraseMetadataRedaction مع أنواع حجب أخرى؟**  
ج7: نعم، يمكنك ربط عدة كائنات حجب (مثل حجب النص يليه حجب البيانات الوصفية) قبل الحفظ.

## الموارد
- **التوثيق**: [GroupDocs Redaction Java Docs](https://docs.groupdocs.com/redaction/java/)  
- **مرجع API**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java)  
- **التنزيل**: [Latest Releases](https://releases.groupdocs.com/redaction/java/)  
- **GitHub**: [GroupDocs GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **الدعم المجاني**: [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)  
- **ترخيص مؤقت**: [Acquire a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**آخر تحديث:** 2026-10-01  
**تم الاختبار مع:** GroupDocs.Redaction 24.9 for Java  
**المؤلف:** GroupDocs

## دروس ذات صلة
- [استخراج بيانات تعريف المستند باستخدام Groupdocs Redaction Java](/redaction/java/metadata-redaction/groupdocs-redaction-java-document-metadata-extraction/)
- [كيفية إزالة البيانات الوصفية في Java باستخدام GroupDocs.Redaction](/redaction/java/metadata-redaction/metadata-redaction-groupdocs-java-guide/)
- [استرجاع معلومات المستند باستخدام Groupdocs Redaction Java](/redaction/java/document-information/retrieve-document-info-using-groupdocs-redaction-java/)