---
date: '2026-08-20'
description: تعلم كيفية إخفاء النص باستخدام GroupDocs.Redaction Java، حفظه كملف PDF
  مُرسم، استبدال العبارات الدقيقة، وتطبيق إعدادات PDF مخصصة.
keywords:
- how to redact text
- save pdf as image
- convert pdf to image
lastmod: '2026-08-20'
og_description: كيفية إخفاء النص باستخدام GroupDocs.Redaction Java. يوضح لك هذا الدليل
  استبدال العبارات الدقيقة، إنشاء PDF مُرسم، والامتثال لمعيار PDF/A‑1a في بضع خطوات.
og_image_alt: Guide showing GroupDocs.Redaction Java code to redact text and create
  rasterized PDF
og_title: كيفية إخفاء النص باستخدام مكتبة GroupDocs.Redaction Java
schemas:
- author: GroupDocs
  dateModified: '2026-08-20'
  description: Learn how to redact text with GroupDocs.Redaction Java, save as rasterized
    PDF, replace exact phrases, and apply custom PDF settings.
  headline: How to redact text with GroupDocs.Redaction Java
  type: TechArticle
- description: Learn how to redact text with GroupDocs.Redaction Java, save as rasterized
    PDF, replace exact phrases, and apply custom PDF settings.
  name: How to redact text with GroupDocs.Redaction Java
  steps:
  - name: '**Sensitive data redaction** – automatically hide personal identifiers
      before sharing contracts.'
    text: '**Sensitive data redaction** – automatically hide personal identifiers
      before sharing contracts.'
  - name: '**Document archiving** – convert finalized reports to rasterized PDF/A
      for long‑term compliance.'
    text: '**Document archiving** – convert finalized reports to rasterized PDF/A
      for long‑term compliance.'
  - name: '**Bulk content update** – replace outdated terminology across hundreds
      of files with a single script.'
    text: '**Bulk content update** – replace outdated terminology across hundreds
      of files with a single script.'
  type: HowTo
- questions:
  - answer: Add the GroupDocs repository and the `groupdocs-redaction` dependency
      to your `pom.xml` as shown in the Maven Setup section.
    question: How do I install GroupDocs.Redaction in a Maven project?
  - answer: Yes, GroupDocs.Redaction supports PDF, DOCX, PPTX, and many other formats.
    question: Can I redact text from PDF files using this library?
  - answer: The `RedactorChangeLog` will return a status of `Failed`. Verify the phrase’s
      spelling and case sensitivity.
    question: What happens if the exact phrase isn’t found?
  - answer: Process them in smaller page ranges, enable rasterization only where needed,
      and always close the `Redactor` to free resources.
    question: How can I handle very large documents efficiently?
  - answer: Absolutely. Use `options.getRasterization().setPageIndex()` and `setPageCount()`
      to target the exact pages you want to rasterize.
    question: Is it possible to save rasterized PDFs with specific page ranges?
  type: FAQPage
tags:
- text redaction
- GroupDocs.Redaction
- Java PDF processing
title: كيفية إخفاء النص باستخدام GroupDocs.Redaction Java
type: docs
url: /ar/java/text-redaction/groupdocs-redaction-java-tutorial-text-redaction-rasterized-pdf/
weight: 1
---

# كيفية إخفاء النص باستخدام GroupDocs.Redaction Java

في التطبيقات الحديثة، **كيفية إخفاء النص** في مستند مع الحفاظ على سير العمل سريعًا ومتوافقًا يمثل تحديًا شائعًا للمطورين والمراجعين ومسؤولي الامتثال. يوضح هذا الدرس كيفية استخدام GroupDocs.Redaction للـ Java لتحديد العبارات الدقيقة، استبدالها بطبقات آمنة، وأخيرًا تصدير النتيجة كملف PDF/A‑1a مُرصّص—مثالي للأرشفة أو التوزيع القانوني.

## إجابات سريعة
- **ما هي الفئة الأساسية للتنقيح؟** `Redactor`  
- **هل يمكنني استبدال عبارة بطبقة ملونة؟** نعم، باستخدام `ExactPhraseRedaction` و `ReplacementOptions`.  
- **كيف يمكنني إنشاء PDF مُرصّص؟** فعل الرصّ عبر `SaveOptions.getRasterization().setEnabled(true)`.  
- **ما هو مستوى امتثال PDF المستخدم في المثال؟** `PdfComplianceLevel.PdfA1a`.  
- **هل أحتاج إلى ترخيص للاستخدام في الإنتاج؟** يلزم وجود ترخيص صالح لـ GroupDocs.Redaction للاستخدام في بيئات الإنتاج.

## ما هو “كيفية إخفاء النص” في Java؟
`Redaction` هو الإزالة الدائمة أو إخفاء المحتوى الحساس من ملف بحيث لا يمكن استعادته أو قراءته لاحقًا. باستخدام GroupDocs.Redaction يمكنك برمجيًا البحث عن عبارة دقيقة—مثل رقم الضمان الاجتماعي أو رمز مشروع سري—واستبدالها بطبقة حمراء، صندوق أسود، أو أي عنصر بصري مخصص، مما يضمن أن البيانات الأصلية لا يمكن استرجاعها.

## لماذا نستخدم GroupDocs.Redaction للـ Java؟
يدعم GroupDocs.Redaction **أكثر من 30 تنسيقًا للمدخلات والإخراج** (PDF، DOCX، PPTX، XLSX، HTML، وأنواع الصور) ويمكنه معالجة مستندات مئات الصفحات دون تحميل الملف بالكامل في الذاكرة. يقلل خوارزمية مطابقة العبارات الدقيقة الإيجابيات الزائفة بأكثر من 95 % مقارنةً ببحث الكلمات المفتاحية العامة، وتتيح محرك الرصّ المدمج إنتاج ملفات PDF/A‑1a تعتمد بالكامل على الصور للحفظ طويل الأمد.

## المتطلبات المسبقة
قبل البدء، تأكد من وجود:

- **GroupDocs.Redaction للـ Java** (الإصدار 24.9 أو أحدث).  
- **Java Development Kit (JDK) 8+**.  
- بيئة تطوير متكاملة مثل IntelliJ IDEA أو Eclipse أو NetBeans.  
- Maven لإدارة الاعتمادات.  

### المكتبات والاعتمادات المطلوبة
- GroupDocs.Redaction للـ Java – أضف المستودع والاعتماد `groupdocs-redaction` إلى ملف `pom.xml` الخاص بك (انظر قسم إعداد Maven).  
- اختياري: أي إطار تسجيل تفضله (SLF4J، Log4j، إلخ).

### المتطلبات المعرفية
- أساسيات صياغة Java وإدخال/إخراج الملفات.  
- الإلمام ببنية `pom.xml` الخاصة بـ Maven.

## إعداد GroupDocs.Redaction للـ Java
### إعداد Maven
أضف مستودع GroupDocs واعتماد `groupdocs-redaction` إلى ملف `pom.xml` الخاص بك:

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
بدلاً من ذلك، يمكنك تنزيل أحدث نسخة مباشرةً من [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### الحصول على الترخيص
- **نسخة تجريبية مجانية** – استكشف الـ API دون مفتاح ترخيص.  
- **ترخيص مؤقت** – للاستخدام في تقييم ممتد.  
- **ترخيص كامل** – مطلوب لبيئات الإنتاج.

### التهيئة الأساسية والإعداد
الفئة `Redactor` هي نقطة الدخول لجميع عمليات التنقيح. تقوم بتحميل المستند، تطبيق قواعد التنقيح، وحفظ النتيجة.

```java
import com.groupdocs.redaction.Redactor;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
```

## كيفية إخفاء النص – مثال العبارة الدقيقة
`Redactor` هي الفئة الأساسية التي تحمل المستند وتطبق قواعد التنقيح. `ExactPhraseRedaction` تُعرّف قاعدة تطابق سلسلة محددة. يوضح هذا المثال كيفية تحميل ملف، إنشاء قاعدة `ExactPhraseRedaction`، وتنفيذ التنقيح في خطوة واحدة، موفرًا سير عمل مختصر للمطورين مع ضمان إخفاء المحتوى الأصلي بشكل دائم.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.ReplacementOptions;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
```

## كيفية حفظ كملف PDF مُرصّص
`SaveOptions` هو كائن الإعدادات الذي يتحكم في طريقة حفظ المستند. عبر تفعيل ميزة الرصّ واختيار امتثال PDF/A‑1a، يمكنك إنتاج PDF يعتمد على الصور فقط حيث يتم تمثيل كل صفحة كصورة نقطية، مما يفي بمعايير الأرشفة ويمنع استخراج النص.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
try {
    RedactorChangeLog result = redactor.apply(new ExactPhraseRedaction(
        "John Doe", new ReplacementOptions(java.awt.Color.RED)));
    
    if (result.getStatus() != RedactionStatus.Failed) {
        // Successfully redacted the text
    }
} finally { 
    redactor.close(); 
}
```

## التطبيقات العملية
1. **إخفاء البيانات الحساسة** – إخفاء المعرفات الشخصية تلقائيًا قبل مشاركة العقود.  
2. **أرشفة المستندات** – تحويل التقارير النهائية إلى PDF/A مُرصّص للامتثال طويل الأمد.  
3. **تحديث المحتوى بالجملة** – استبدال المصطلحات القديمة عبر مئات الملفات باستخدام سكريبت واحد.

## اعتبارات الأداء
- **إغلاق `Redactor`** بعد كل عملية لتحرير مقبض الملف والذاكرة.  
- **المعالجة الدفعية** – تحميل قائمة من الملفات وتكرارها، مع إعادة استخدام نسخة واحدة من `Redactor` عندما يكون ذلك ممكنًا.  
- **مراقبة الموارد** – استخدم أدوات تحليل Java لمتابعة استهلاك المعالج والذاكرة أثناء عمليات التنقيح واسعة النطاق.

## الأسئلة المتكررة

**س: كيف يمكنني تثبيت GroupDocs.Redaction في مشروع Maven؟**  
ج: أضف مستودع GroupDocs واعتماد `groupdocs-redaction` إلى ملف `pom.xml` كما هو موضح في قسم إعداد Maven.

**س: هل يمكنني إخفاء النص من ملفات PDF باستخدام هذه المكتبة؟**  
ج: نعم، يدعم GroupDocs.Redaction PDF، DOCX، PPTX، والعديد من الصيغ الأخرى.

**س: ماذا يحدث إذا لم يتم العثور على العبارة الدقيقة؟**  
ج: سيعيد `RedactorChangeLog` حالة `Failed`. تحقق من تهجئة العبارة وحساسيتها لحالة الأحرف.

**س: كيف يمكنني التعامل مع مستندات ضخمة جدًا بكفاءة؟**  
ج: عالجها على نطاقات صفحات أصغر، فعل الرصّ فقط عند الحاجة، وتأكد دائمًا من إغلاق `Redactor` لتحرير الموارد.

**س: هل يمكن حفظ ملفات PDF مُرصّصة بنطاقات صفحات محددة؟**  
ج: بالطبع. استخدم `options.getRasterization().setPageIndex()` و `setPageCount()` لاستهداف الصفحات المطلوبة للرصّ.

## الخلاصة
أصبح لديك الآن دليل شامل من البداية إلى النهاية حول **كيفية إخفاء النص** باستخدام GroupDocs.Redaction Java و**كيفية حفظه كملف PDF مُرصّص**. باتباع هذه الخطوات، يمكنك حماية المعلومات الحساسة، الالتزام بمعايير الامتثال الصارمة، والحفاظ على أداء خدمات Java على نطاق واسع.

**الخطوات التالية**  
- تعمق أكثر في الـ API عبر استكشاف [الوثائق الرسمية](https://docs.groupdocs.com/redaction/java/).  
- جرب أنواع تنقيح أخرى مثل `RegexRedaction` و `ImageRedaction`.  
- انضم إلى المجتمع على [منتدى دعم GroupDocs](https://forum.groupdocs.com/c/redaction/33) للحصول على نصائح وأفضل الممارسات.

---

**Last Updated:** 2026-08-20  
**Tested With:** GroupDocs.Redaction Java 24.9  
**Author:** GroupDocs

```java
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.options.PdfComplianceLevel;
```

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
try {
    SaveOptions options = new SaveOptions();

    // Enable rasterization for converting pages into images.
    options.getRasterization().setEnabled(true);
    
    // Set the starting page and count for rasterization.
    options.getRasterization().setPageIndex(5);
    options.getRasterization().setPageCount(1);

    // Define PDF compliance level.
    options.getRasterization().setCompliance(PdfComplianceLevel.PdfA1a);

    // Append a suffix to avoid filename conflicts.
    options.setAddSuffix(true);

    // Save the document with these configurations.
    redactor.save(options);
} finally { 
    redactor.close(); 
}
```

## دروس ذات صلة

- [How to Redact Text with GroupDocs.Redaction for Java](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction/)
- [Java Text Redaction Tutorial: Guide with GroupDocs.Redaction](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction-guide/)