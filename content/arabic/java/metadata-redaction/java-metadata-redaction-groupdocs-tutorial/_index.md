---
date: '2026-09-26'
description: تعلم كيفية إزالة metadata باستخدام GroupDocs في Java، مع حذف metadata
  للوثائق document confidential بأمان مع الحفاظ على original format دون تغيير.
keywords:
- how to redact metadata
- GroupDocs Redaction Java
- secure document processing
- metadata removal Java
lastmod: '2026-09-26'
og_description: كيفية إزالة metadata باستخدام GroupDocs في Java – دليل خطوة بخطوة
  يوضح لك كيفية حذف metadata للوثائق document confidential بأمان والحفاظ على original
  format.
og_image_alt: Guide showing metadata redaction using GroupDocs in Java
og_title: كيفية إزالة metadata باستخدام GroupDocs في Java
schemas:
- author: GroupDocs
  dateModified: '2026-09-26'
  description: Learn how to redact metadata with GroupDocs in Java, securely removing
    confidential document metadata while keeping the original format intact.
  headline: How to redact metadata with GroupDocs in Java
  type: TechArticle
- description: Learn how to redact metadata with GroupDocs in Java, securely removing
    confidential document metadata while keeping the original format intact.
  name: How to redact metadata with GroupDocs in Java
  steps:
  - name: import necessary classes
    text: These imports give you access to the redaction engine, save options, and
      metadata utilities.
  - name: initialize redactor
    text: Instantiate the `Redactor` with the path to your source file.
  - name: configure metadata search and redaction
    text: Create a `MetadataSearchRedaction` that looks for the exact string **"Company
      Ltd."** and replaces it with **"--company--"**. The `setFilter` call limits
      the operation to the *Company* metadata field only.
  - name: apply the redaction
    text: Run the redaction against the opened document.
  - name: save with custom options
    text: '`SaveOptions` allows you to specify output format, file naming, and other
      saving parameters for the redacted document. Configure `SaveOptions` so the
      redacted file gets a “_Redacted” suffix while preserving its original format.'
  - name: release resources
    text: Always close the `Redactor` to free native resources and avoid memory leaks.
  type: HowTo
- questions:
  - answer: It’s a powerful library that enables you to redact text, metadata, and
      images in documents using Java applications.
    question: What is GroupDocs.Redaction for Java?
  - answer: Yes, but with limitations. A free trial or temporary license allows full
      access for testing purposes.
    question: Can I use GroupDocs.Redaction without purchasing a license?
  - answer: Use `SaveOptions` to specify your requirements, such as avoiding rasterization
      when saving to PDF.
    question: How do I ensure document formats are preserved during redaction?
  - answer: It supports a wide range, including Word, Excel, PowerPoint, PDF, and
      many more.
    question: What types of documents can be redacted using GroupDocs.Redaction?
  - answer: Visit the [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33)
      for assistance.
    question: Where can I find support if I run into issues?
  type: FAQPage
tags:
- metadata redaction
- GroupDocs
- Java document security
- redaction tutorial
title: كيفية إزالة metadata باستخدام GroupDocs في Java
type: docs
url: /ar/java/metadata-redaction/java-metadata-redaction-groupdocs-tutorial/
weight: 1
---

# كيفية حذف بيانات التعريف باستخدام GroupDocs في Java

في هذا الدرس الشامل ستتعلم **كيفية حذف بيانات التعريف** من Word و PDF والعديد من أنواع المستندات الأخرى باستخدام GroupDocs.Redaction للغة Java. بنهاية الدليل ستكون قادرًا على دمج حذف بيانات التعريف في أي خدمة مبنية على Java، مما يضمن أن المعلومات السرية مثل أسماء الشركات والمؤلفين أو الخصائص المخصصة لا تغادر مؤسستك.

## إجابات سريعة
- **ماذا يفعل MetadataSearchRedaction؟** يبحث عن حقول بيانات التعريف المحددة ويستبدل قيمها بنص مخصص.  
- **ما المكتبة المطلوبة؟** GroupDocs.Redaction for Java (v24.9 or newer).  
- **هل أحتاج إلى ترخيص؟** الإصدار التجريبي المجاني يعمل للتقييم؛ الترخيص الكامل مطلوب للإنتاج.  
- **هل يمكنني الاحتفاظ بتنسيق الملف الأصلي؟** نعم—استخدم `SaveOptions` للحفاظ على التنسيق الأصلي.  
- **هل هذا النهج آمن للخطوط المتعددة؟** كل مثيل من `Redactor` مستقل، لذا يمكنك معالجة المستندات بشكل متوازي.

## كيفية حذف بيانات التعريف باستخدام GroupDocs؟
`Redactor` هو الفئة الأساسية التي تقوم بتحميل المستند وتوفر عمليات حذف مختلفة.  
حمّل مستند المصدر باستخدام مثيل `Redactor`، قم بتهيئة `MetadataSearchRedaction` التي تستهدف مفتاح بيانات التعريف المحدد الذي تريد تنظيفه، طبّق الحذف، وأخيرًا احفظ الملف باستخدام `SaveOptions`. يمكن التعبير عن سير العمل بالكامل في بضع أسطر فقط ويعمل مع أي تنسيق مدعوم، من DOCX إلى PDF وما بعده.

## ما هو حذف بيانات التعريف باستخدام GroupDocs؟
`MetadataSearchRedaction` هي فئة متخصصة تتيح لك استهداف خاصية بيانات تعريف معينة (مثل *Company*، *Author*) واستبدال محتواها ببديل. إنها مثالية عندما تحتاج إلى إخفاء هوية البيانات المؤسسية قبل مشاركة المستندات مع شركاء خارجيين. عملية الحذف لا تغير عناصر المستند الأخرى، مما يضمن بقاء التخطيط البصري والمحتوى كما هو بعد إزالة بيانات التعريف.

## لماذا نستخدم حذف بيانات التعريف باستخدام GroupDocs؟
يوفر حذف بيانات التعريف باستخدام GroupDocs طريقة موثوقة لإزالة المعلومات الحساسة من المستندات مع الحفاظ على مظهرها الأصلي وبنيتها. من خلال التركيز على حقول بيانات التعريف، يمكنك الامتثال بسرعة لمعايير الخصوصية دون تعديل المحتوى الظاهر أو تعريض نفسك لتسريبات بيانات غير مقصودة.

- **Precision** – احذف فقط الحقول التي تحددها، مع ترك باقي المستند دون تعديل.  
- **Compliance** – يساعد على تلبية متطلبات GDPR و HIPAA وغيرها من لوائح الخصوصية عن طريق إزالة المعرفات المخفية.  
- **Automation‑ready** – يندمج بسلاسة في خطوط معالجة الدفعات أو الخدمات المصغرة.  
- **Broad format support** – يدعم GroupDocs.Redaction **أكثر من 50 تنسيقًا للإدخال والإخراج** (بما في ذلك DOCX و PDF و PPTX و XLSX وأنواع الصور) ويمكنه معالجة ملفات مئات الصفحات دون تحميل المستند بالكامل في الذاكرة.

## المتطلبات المسبقة
- **GroupDocs.Redaction for Java** ≥ 24.9.  
- Java 8 أو أحدث مثبت على جهازك.  
- بيئة تطوير متكاملة (IDE) مثل IntelliJ IDEA أو Eclipse (اختياري لكن يُنصح به).  
- إلمام أساسي بـ Maven (أو القدرة على إضافة ملفات JAR يدويًا).  

## إعداد GroupDocs.Redaction للغة Java

أضف المستودع والاعتماد إلى ملف `pom.xml` الخاص بك. تضمن هذه الخطوة أن Maven يمكنه تنزيل المكتبة تلقائيًا.

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

*بدلاً من ذلك، يمكنك تنزيل ملف JAR مباشرةً من صفحة الإصدار الرسمية:*  
[إصدارات GroupDocs.Redaction للغة Java](https://releases.groupdocs.com/redaction/java/)

### الحصول على الترخيص
- **Free trial** – قم بتنزيل ترخيص تجريبي لاستكشاف جميع الميزات.  
- **Temporary license** – استخدمه للاختبار الموسع.  
- **Full license** – مطلوب للنشر في بيئات الإنتاج.

## التهيئة الأساسية
`Redactor` يحمل مستندًا ويكشف عن طرق لتطبيق عمليات حذف مختلفة.  
أنشئ مثيل `Redactor` يشير إلى المستند الذي تريد معالجته.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

## دليل التنفيذ

### الخطوة 1: استيراد الفئات الضرورية
تمنحك هذه الاستيرادات الوصول إلى محرك الحذف، خيارات الحفظ، وأدوات بيانات التعريف.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.redactions.MetadataFilters;
import com.groupdocs.redaction.redactions.MetadataSearchRedaction;
```

### الخطوة 2: تهيئة الـ Redactor
أنشئ مثيل `Redactor` مع مسار ملف المصدر الخاص بك.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

### الخطوة 3: تكوين بحث بيانات التعريف والحذف
أنشئ `MetadataSearchRedaction` يبحث عن السلسلة الدقيقة **"Company Ltd."** ويستبدلها بـ **"--company--"**. تستدعي `setFilter` لتقصر العملية على حقل بيانات التعريف *Company* فقط.

```java
MetadataSearchRedaction redaction = new MetadataSearchRedaction("Company Ltd.", "--company--");
redaction.setFilter(MetadataFilters.Company);
```

### الخطوة 4: تطبيق الحذف
نفّذ عملية الحذف على المستند المفتوح.

```java
redactor.apply(redaction);
```

### الخطوة 5: الحفظ باستخدام خيارات مخصصة
`SaveOptions` يتيح لك تحديد تنسيق الإخراج، تسمية الملف، وغيرها من معلمات الحفظ للمستند المحذوف.  
قم بتكوين `SaveOptions` بحيث يحصل الملف المحذوف على لاحقة “_Redacted” مع الحفاظ على تنسيقه الأصلي.

```java
SaveOptions tmp0 = new SaveOptions();
tmp0.setAddSuffix(true);  // Adds "_Redacted" to file name
tmp0.setRasterizeToPDF(false);  // Keeps original format

redactor.save(tmp0);
```

### الخطوة 6: تحرير الموارد
دائمًا أغلق `Redactor` لتحرير الموارد الأصلية وتجنب تسرب الذاكرة.

```java
finally {
    redactor.close();
}
```

## المشكلات الشائعة والحلول
- **FileNotFoundException** – تحقق مرة أخرى من المسار الذي تمرره إلى `Redactor`. استخدم مسارات مطلقة أو `Paths.get(...)` للموثوقية.  
- **No changes observed** – تأكد من أن حقل بيانات التعريف المستهدف يحتوي فعليًا على سلسلة البحث؛ بيانات التعريف حساسة لحالة الأحرف بشكل افتراضي.  
- **Out‑of‑memory errors on large files** – عالج المستندات على دفعات أصغر واستدعِ `redactor.close()` فورًا بعد كل ملف.

## التطبيقات العملية
1. **Legal documentation** – إزالة أسماء شركات العملاء قبل إرسال العقود إلى أطراف ثالثة.  
2. **Financial reporting** – إخفاء الهوية للمعرفات الداخلية في ملفات التدقيق.  
3. **Collaborative projects** – حماية المعلومات المملوكة عند مشاركة المسودات مع البائعين الخارجيين.

## اعتبارات الأداء
- **Memory management** – تحتفظ المكتبة بالمستند بالكامل في الذاكرة؛ إغلاق `Redactor` بعد كل ملف أمر أساسي.  
- **Batch processing** – في سيناريوهات الأحجام الكبيرة، قم بالتكرار عبر مجموعة من الملفات وأعد استخدام مثيل واحد من `SaveOptions`.  
- **Stay updated** – الإصدارات الجديدة تجلب تحسينات في الأداء وإصلاحات الأخطاء؛ استهدف دائمًا أحدث نسخة مستقرة.

## الأسئلة المتكررة

**س: ما هو GroupDocs.Redaction للغة Java؟**  
A: إنها مكتبة قوية تتيح لك حذف النصوص وبيانات التعريف والصور في المستندات باستخدام تطبيقات Java.

**س: هل يمكنني استخدام GroupDocs.Redaction دون شراء ترخيص؟**  
A: نعم، ولكن مع قيود. يتيح الإصدار التجريبي المجاني أو الترخيص المؤقت الوصول الكامل لأغراض الاختبار.

**س: كيف أضمن الحفاظ على تنسيقات المستندات أثناء الحذف؟**  
A: استخدم `SaveOptions` لتحديد متطلباتك، مثل تجنب التحويل إلى صورة rasterization عند الحفظ إلى PDF.

**س: ما هي أنواع المستندات التي يمكن حذفها باستخدام GroupDocs.Redaction؟**  
A: تدعم مجموعة واسعة، بما في ذلك Word و Excel و PowerPoint و PDF والعديد غيرها.

**س: أين يمكنني العثور على الدعم إذا واجهت مشاكل؟**  
A: قم بزيارة [منتدى دعم GroupDocs](https://forum.groupdocs.com/c/redaction/33) للحصول على المساعدة.

**س: هل يعمل MetadataSearchRedaction مع المستندات المشفرة؟**  
A: نعم. حمّل المستند باستخدام كلمة المرور المناسبة عبر مُنشئ `Redactor` الذي يقبل معامل كلمة المرور.

**س: هل يمكنني ربط عدة عمليات حذف بيانات تعريف في تشغيل واحد؟**  
A: بالطبع. أنشئ عدة كائنات `MetadataSearchRedaction`، عيّن فلاتر مختلفة، وطبقها تسلسليًا قبل الحفظ.

**س: هل يمكن معاينة عمليات الحذف قبل الحفظ؟**  
A: يمكنك استدعاء `redactor.getRedactions()` للحصول على قائمة بالحذف المعلق وتفقدها برمجيًا.

## موارد إضافية
- **Documentation**: استكشف أدلة مفصلة في [وثائق GroupDocs](https://docs.groupdocs.com/redaction/java/).  
- **API reference**: تحقق من مرجع API الكامل على [مرجع API الخاص بـ GroupDocs](https://reference.groupdocs.com/redaction/java).  
- **Download library**: احصل على أحدث إصدار من [تنزيلات GroupDocs](https://releases.groupdocs.com/redaction/java/).  
- **Source code**: عرض والمساهمة على [GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java).  
- **Support**: احصل على المساعدة عبر قناة الدعم المجانية في [منتدى دعم GroupDocs](https://forum.groupdocs.com/c/redaction/33).

---

**آخر تحديث:** 2026-09-26  
**تم الاختبار مع:** GroupDocs.Redaction 24.9 للغة Java  
**المؤلف:** GroupDocs

## دروس ذات صلة

- [استخراج بيانات تعريف المستند باستخدام Groupdocs Redaction Java](/redaction/java/metadata-redaction/groupdocs-redaction-java-document-metadata-extraction/)
- [استبدال نص بيانات التعريف Java – حذف آمن باستخدام GroupDocs](/redaction/java/metadata-redaction/java-redaction-metadata-text-replacement-guide/)
- [استرجاع معلومات المستند باستخدام Groupdocs Redaction Java](/redaction/java/document-information/retrieve-document-info-using-groupdocs-redaction-java/)