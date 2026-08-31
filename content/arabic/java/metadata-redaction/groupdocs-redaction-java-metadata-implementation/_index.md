---
date: '2026-03-22'
description: تعلم كيفية مسح البيانات الوصفية وإزالة بيانات المؤلف الوصفية في جافا
  باستخدام GroupDocs. يوضح لك هذا البرنامج التعليمي كيفية حفظ ملفات المستندات الممحوة
  بأمان.
keywords:
- metadata redaction in Java
- GroupDocs Redaction setup
- removing metadata fields
title: 'كيفية مسح البيانات الوصفية في جافا باستخدام GroupDocs: دليل خطوة بخطوة'
type: docs
url: /ar/java/metadata-redaction/groupdocs-redaction-java-metadata-implementation/
weight: 1
---

# كيفية مسح البيانات الوصفية في Java باستخدام GroupDocs

في العالم الرقمي اليوم، حماية المعلومات الحساسة داخل المستندات أمر أساسي، و**معرفة كيفية مسح البيانات الوصفية** تُعد جزءًا رئيسيًا من هذه الحماية. في هذا الدليل ستتعلم كيفية استخدام `EraseMetadataRedaction` لإزالة البيانات الوصفية مثل *Author* و*Manager* من ملفات Word باستخدام GroupDocs.Redaction للـ Java. في نهاية البرنامج التعليمي ستحصل على مستند نظيف وآمن للخصوصية وتعرف كيف **تحفظ المستند المُحَرَّف** للمشاركة الآمنة أو الأرشفة.

## إجابات سريعة
- **ماذا يفعل EraseMetadataRedaction؟** يزيل حقول البيانات الوصفية المحددة من المستند.  
- **أي مكتبة توفر هذه الميزة؟** GroupDocs.Redaction للـ Java.  
- **هل أحتاج إلى ترخيص؟** النسخة التجريبية المجانية تكفي للاختبار؛ الترخيص الدائم مطلوب للإنتاج.  
- **هل يمكنني استهداف حقول متعددة في آنٍ واحد؟** نعم، يمكن دمج الفلاتر باستخدام عامل OR المنطقي.  
- **هل العملية آمنة للاستخدام عبر خيوط متعددة؟** كائنات Redactor لا تُشارك بين الخيوط؛ يُنشأ كائن جديد لكل عملية.

## كيفية مسح البيانات الوصفية في Java
هذا القسم يشرح الخطوات الدقيقة اللازمة **لإزالة بيانات المؤلف** وأي خصائص غير مرغوب فيها من ملفاتك.

### ما هو EraseMetadataRedaction؟
`EraseMetadataRedaction` هو فئة حجب مدمجة تسمح لك بتحديد أي من مدخلات البيانات الوصفية يجب مسحها. تعمل على مجموعة واسعة من صيغ المستندات التي يدعمها GroupDocs.Redaction، مما يضمن عدم تسرب معلومات التأليف المخفية.

### لماذا نستخدم EraseMetadataRedaction مع GroupDocs؟
- **الامتثال** – تلبية متطلبات GDPR، HIPAA، أو سياسات الشركة عبر إزالة المعرفات الشخصية.  
- **الاتساق** – تطبيق نفس منطق الحجب على PDFs، DOCX، PPTX، وأكثر.  
- **الأداء** – يتم تنفيذ الحجب في الذاكرة دون الحاجة إلى أدوات خارجية.  
- **المرونة** – دمج عدة `MetadataFilters` لاستهداف ما تحتاجه بالضبط.

## المتطلبات المسبقة
- Java 8 أو أعلى مثبتة.  
- Maven (أو القدرة على إضافة ملفات JAR يدويًا).  
- GroupDocs.Redaction للـ Java (الإصدار 24.9 أو أحدث).  
- ترخيص تجريبي صالح أو ترخيص دائم من GroupDocs.

## إعداد GroupDocs.Redaction للـ Java

### تثبيت عبر Maven
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
بدلاً من ذلك، حمّل أحدث JAR من [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### الحصول على الترخيص
احصل على نسخة تجريبية مجانية أو اشترِ ترخيصًا مؤقتًا من بوابة GroupDocs. يجب وضع ملف الترخيص في مكان يمكن لتطبيقك تحميله منه (مثلاً جذر الـ classpath).

### التهيئة الأساسية والإعداد
فيما يلي مثال بسيط ينشئ كائن `Redactor` لملف DOCX:

```java
import com.groupdocs.redaction.Redactor;

String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
Redactor redactor = new Redactor(filePath);
```

## كيفية استخدام EraseMetadataRedaction في Java
الأقسام التالية تفصل التنفيذ إلى خطوات واضحة وقابلة للتنفيذ.

### الميزة: تنظيف عناصر بيانات وصفية محددة

#### نظرة عامة
سنقوم بمسح حقلي البيانات الوصفية **Author** و**Manager** باستخدام `EraseMetadataRedaction`. هذا طلب شائع عند مشاركة التقارير الداخلية مع شركاء خارجيين.

#### تنفيذ خطوة بخطوة

##### 1️⃣ تهيئة كائن Redactor
أنشئ كائن `Redactor` يشير إلى المستند الذي تريد تنظيفه:

```java
import com.groupdocs.redaction.Redactor;

String inputFilePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
final Redactor redactor = new Redactor(inputFilePath);
```

##### 2️⃣ تطبيق EraseMetadataRedaction
استخدم فئة `EraseMetadataRedaction` مع `MetadataFilters`. يجمع عامل OR الثنائي (`|`) بين فلاتر `Author` و`Manager` بحيث تُحذف الحقلان في استدعاء واحد:

```java
import com.groupdocs.redaction.redactions.EraseMetadataRedaction;
import com.groupdocs.redaction.MetadataFilters;

try {
    redactor.apply(new EraseMetadataRedaction(MetadataFilters.Author | MetadataFilters.Manager));
} finally {
    redactor.close();
}
```

##### 3️⃣ ضبط خيارات الحفظ
عدّل `SaveOptions` للتحكم في اسم ملف الإخراج وما إذا كان يجب تحويل المستند إلى PDF عبر rasterization:

```java
import com.groupdocs.redaction.options.SaveOptions;

SaveOptions saveOptions = new SaveOptions();
saveOptions.setAddSuffix(true); // Adds "_Redacted" to the file name
saveOptions.setRasterizeToPDF(false);

redactor.save(saveOptions);
```

### حالات الاستخدام الشائعة
1. **المستندات القانونية** – حذف معلومات المؤلف قبل إرسال العقود إلى الطرف المقابل.  
2. **تقارير الشركة** – إزالة أسماء المديرين عند نشر النتائج ربع السنوية للمساهمين.  
3. **ملفات المشاريع** – تنظيف وثائق المشروع الداخلية قبل الأرشفة أو رفعها إلى مستودع عام.

### نصائح استكشاف الأخطاء وإصلاحها
- **الملف غير موجود** – تأكد من أن المسار في `inputFilePath` يشير إلى ملف موجود وأن التطبيق يمتلك صلاحيات القراءة.  
- **حقول البيانات الوصفية مفقودة** – ليست جميع صيغ المستندات تخزن نفس مفاتيح البيانات الوصفية؛ تحقق من خصائص المستند في Office أولًا.  
- **أخطاء الترخيص** – تأكد من تحميل ملف الترخيص بشكل صحيح قبل إنشاء كائن `Redactor`.

## اعتبارات الأداء
- أغلق كائن `Redactor` فورًا (كما هو موضح في كتلة `finally`) لتحرير الموارد الأصلية.  
- تجنّب rasterization للمستندات الكبيرة ما لم تكن بحاجة إلى معاينة PDF؛ قد يؤدي rasterization إلى زيادة استهلاك المعالج والذاكرة بشكل ملحوظ.

## الأسئلة المتكررة

**س1: ما هو حجب البيانات الوصفية؟**  
ج1: حجب البيانات الوصفية يعني إزالة خصائص المستند المخفية (مثل المؤلف، المدير، أو العلامات المخصصة) لمنع الكشف غير المقصود عن معلومات حساسة.

**س2: هل يمكنني استخدام GroupDocs.Redaction لأنواع ملفات أخرى؟**  
ج2: نعم، تدعم المكتبة PDF، DOCX، PPTX، XLSX، والعديد من الصيغ الأخرى.

**س3: كيف أتعامل مع الأخطاء أثناء الحجب؟**  
ج3: ضع استدعاء `apply` داخل كتلة try‑catch ودوماً أغلق `Redactor` في كتلة finally لضمان تحرير الموارد.

**س4: هل يمكن حجب حقول بيانات وصفية مخصصة؟**  
ج4: بالتأكيد. استخدم `MetadataFilters.Custom("YourFieldName")` (أو الـ enum المناسب) لاستهداف أي خاصية مخصصة.

**س5: ما هي أفضل الممارسات لاستخدام GroupDocs.Redaction؟**  
ج5:  
- حمّل الترخيص مبكرًا في تطبيقك.  
- أغلق كائنات `Redactor` بسرعة.  
- استخدم `SaveOptions` لإضافة لاحقة، مع الحفاظ على الملفات الأصلية دون تعديل.  
- اختبر الحجب على نسخة من المستند قبل معالجة دفعات كبيرة.

**س6: هل يدعم EraseMetadataRedaction عمليات الدفعات؟**  
ج6: يمكنك تكرار مجموعة من مسارات الملفات، وإنشاء كائن `Redactor` جديد لكل ملف وتطبيق نفس منطق الحجب.

**س7: هل يمكن دمج EraseMetadataRedaction مع أنواع حجب أخرى؟**  
ج7: نعم، يمكنك ربط عدة كائنات حجب (مثل حجب النص ثم حجب البيانات الوصفية) قبل عملية الحفظ.

## موارد

- **الوثائق**: [GroupDocs Redaction Java Docs](https://docs.groupdocs.com/redaction/java/)  
- **مرجع API**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java)  
- **التحميل**: [Latest Releases](https://releases.groupdocs.com/redaction/java/)  
- **GitHub**: [GroupDocs GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **الدعم المجاني**: [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)  
- **ترخيص مؤقت**: [Acquire a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**آخر تحديث:** 2026-03-22  
**تم الاختبار مع:** GroupDocs.Redaction 24.9 للـ Java  
**المؤلف:** GroupDocs  

---