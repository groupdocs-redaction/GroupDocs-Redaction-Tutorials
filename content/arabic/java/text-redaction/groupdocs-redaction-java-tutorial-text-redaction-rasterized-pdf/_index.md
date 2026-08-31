---
date: '2026-02-26'
description: تعلم كيفية إخفاء النص باستخدام GroupDocs.Redaction Java وحفظه كملف PDF
  رستر مع استبدال العبارة بدقة وإعدادات PDF مخصصة.
keywords:
- GroupDocs.Redaction Java
- text redaction Java
- rasterized PDF conversion
title: كيفية إخفاء النص باستخدام GroupDocs.Redaction Java
type: docs
url: /ar/java/text-redaction/groupdocs-redaction-java-tutorial-text-redaction-rasterized-pdf/
weight: 1
---

# كيفية إخفاء النص باستخدام GroupDocs.Redaction Java

في عالم اليوم القائم على البيانات، **how to redact text** في مستند بأمان وكفاءة هو مصدر قلق رئيسي للمطورين ومسؤولي الامتثال على حد سواء. سواء كنت بحاجة إلى إخفاء المعرفات الشخصية، أو تفاصيل العملاء السرية، أو رموز المشاريع الداخلية، فإن GroupDocs.Redaction for Java يوفر لك طريقة موثوقة لتحديد العبارات الدقيقة واستبدالها بطبقات آمنة. يوضح هذا البرنامج التعليمي أيضًا **how to save as rasterized PDF**، مما يحول كل صفحة إلى PDF قائم على الصور يفي بمعايير الأرشفة.

## إجابات سريعة
- **ما هي الفئة الأساسية للإخفاء؟** `Redactor`  
- **هل يمكنني استبدال عبارة بطبقة ملونة؟** نعم، باستخدام `ExactPhraseRedaction` و `ReplacementOptions`.  
- **كيف يمكنني إنشاء PDF مُرصّص؟** تمكين الرصّ عبر `SaveOptions.getRasterization().setEnabled(true)`.  
- **ما هو مستوى الامتثال PDF المستخدم في المثال؟** `PdfComplianceLevel.PdfA1a`.  
- **هل أحتاج إلى ترخيص للاستخدام في الإنتاج؟** يلزم وجود ترخيص GroupDocs.Redaction صالح لعمليات النشر في بيئة الإنتاج.

## ما هو “how to redact text” في Java؟
الإخفاء هو عملية إزالة أو إخفاء المحتوى الحساس من ملف بشكل دائم. باستخدام GroupDocs.Redaction، يمكنك البحث برمجياً عن عبارة دقيقة—مثل اسم أو معرف—واستبدالها بطبقة حمراء، أو صندوق أسود، أو أي عنصر بصري مخصص، مما يضمن عدم إمكانية استعادة البيانات الأصلية.

## لماذا تستخدم GroupDocs.Redaction للـ Java؟
- **مطابقة العبارة الدقيقة** تُزيل الإيجابيات الكاذبة.  
- **الرصّ المدمج** يتيح لك إنشاء ملفات PDF/A متوافقة، بصور فقط، للتخزين طويل الأمد.  
- **دعم صيغ متعددة** يعمل مع DOCX و PDF و PPTX وغيرها، بحيث يمكنك تطبيق نفس الشيفرة عبر أنواع المستندات.  
- **واجهة برمجة تطبيقات مركزة على الأداء** تتيح لك معالجة دفعات من المستندات الكبيرة مع الحفاظ على استهلاك الذاكرة منخفضًا.

## المتطلبات المسبقة
قبل البدء، تأكد من وجود ما يلي:
- **GroupDocs.Redaction للـ Java** (الإصدار 24.9 أو أحدث).  
- **مجموعة تطوير جافا (JDK) 8+**.  
- بيئة تطوير متكاملة مثل IntelliJ IDEA أو Eclipse أو NetBeans.  
- Maven لإدارة التبعيات.  

### المكتبات والتبعيات المطلوبة
- **GroupDocs.Redaction للـ Java** – أضف المستودع والتبعية إلى ملف `pom.xml` الخاص بك (انظر كتلة الشيفرة أدناه).  
- **اختياري**: أي مكتبات تسجيل إضافية تفضلها.

### متطلبات المعرفة
- أساسيات صياغة جافا وإدخال/إخراج الملفات.  
- الإلمام ببنية `pom.xml` الخاصة بـ Maven.

## إعداد GroupDocs.Redaction للـ Java
### إعداد Maven
أضف المستودع والتبعية إلى ملف `pom.xml` الخاص بك:

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
بدلاً من ذلك، يمكنك تنزيل أحدث إصدار مباشرةً من [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### الحصول على الترخيص
- **تجربة مجانية** – استكشف الواجهة البرمجية دون مفتاح ترخيص.  
- **ترخيص مؤقت** – استخدمه للتقييم الموسع.  
- **ترخيص كامل** – مطلوب لبيئات الإنتاج.

### التهيئة الأساسية والإعداد
فيما يلي الحد الأدنى من الشيفرة لإنشاء كائن `Redactor` يشير إلى ملف DOCX تجريبي:

```java
import com.groupdocs.redaction.Redactor;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
```

## كيفية إخفاء النص – مثال العبارة الدقيقة
### الخطوة 1: استيراد الفئات المطلوبة
تتيح لك هذه الاستيرادات الوصول إلى محرك الإخفاء وخيارات الاستبدال:

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.ReplacementOptions;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
```

### الخطوة 2: إنشاء وتطبيق الإخفاء
المقتطف التالي يبحث عن العبارة **“John Doe”** ويستبدلها بطبقة حمراء:

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

**لماذا هذا مهم:** يتيح لك `ReplacementOptions` التحكم في النمط البصري للإخفاء، مما يضمن عدم إمكانية استعادة المحتوى المخفي عبر النسخ واللصق أو OCR.

## كيفية حفظ PDF مُرصّص
### الخطوة 1: استيراد فئات SaveOptions
تتيح لك هذه الفئات تكوين مخرجات PDF، بما في ذلك الرصّ ومستويات الامتثال:

```java
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.options.PdfComplianceLevel;
```

### الخطوة 2: تكوين وتطبيق خيارات الحفظ
بعد الإخفاء، يمكنك تصدير المستند كملف PDF مُرصّص. المثال أدناه يرّصّ الصفحة 5 فقط ويجبر الامتثال لـ PDF/A‑1a:

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

**نقطة رئيسية:** رصّ PDF **يحوّل كل صفحة إلى صورة**، مما يزيل طبقات النص المخفي ويجعل المستند مقاومًا للعبث—مثالي للأرشفة القانونية.

## تطبيقات عملية
1. **إخفاء البيانات الحساسة** – إخفاء المعرفات الشخصية تلقائيًا قبل مشاركة العقود.  
2. **أرشفة المستندات** – تحويل التقارير النهائية إلى PDF/A مُرصّص للامتثال طويل الأمد.  
3. **تحديث المحتوى بالجملة** – استبدال المصطلحات القديمة عبر مئات الملفات باستخدام سكريبت واحد.

## اعتبارات الأداء
- **إغلاق `Redactor`** بعد كل عملية لتحرير مقابض الملفات والذاكرة.  
- **معالجة دفعات** – تحميل قائمة من الملفات والتكرار عبرها، وإعادة استخدام كائن `Redactor` واحد عندما يكون ذلك ممكنًا.  
- **مراقبة الموارد** – استخدم أدوات تحليل الأداء في جافا لمراقبة استهلاك المعالج والذاكرة أثناء الإخفاءات على نطاق واسع.

## الأسئلة المتكررة

**س: كيف أقوم بتثبيت GroupDocs.Redaction في مشروع Maven؟**  
ج: أضف مستودع GroupDocs وتبعيات `groupdocs-redaction` إلى ملف `pom.xml` الخاص بك كما هو موضح في قسم إعداد Maven.

**س: هل يمكنني إخفاء النص من ملفات PDF باستخدام هذه المكتبة؟**  
ج: نعم، يدعم GroupDocs.Redaction ملفات PDF و DOCX و PPTX والعديد من الصيغ الأخرى.

**س: ماذا يحدث إذا لم يتم العثور على العبارة الدقيقة؟**  
ج: سيُعيد `RedactorChangeLog` حالة `Failed`. تحقق من تهجئة العبارة وحساسيتها لحالة الأحرف.

**س: كيف يمكنني معالجة المستندات الكبيرة جدًا بكفاءة؟**  
ج: عالجها في نطاقات صفحات أصغر، فعّل الرصّ فقط عند الحاجة، وتأكد دائمًا من إغلاق `Redactor` لتحرير الموارد.

**س: هل يمكن حفظ ملفات PDF مُرصّصة بنطاقات صفحات محددة؟**  
ج: بالتأكيد. استخدم `options.getRasterization().setPageIndex()` و `setPageCount()` لاستهداف الصفحات المحددة التي تريد رصّها.

## الخلاصة
أصبح لديك الآن دليل شامل من البداية إلى النهاية حول **how to redact text** باستخدام GroupDocs.Redaction Java و **save as rasterized PDF**. باتباع هذه الخطوات، يمكنك حماية المعلومات الحساسة، وتلبية متطلبات الامتثال، والحفاظ على أداء عالي في أحمال الإنتاج.

**الخطوات التالية**  
- تعمق أكثر في الواجهة البرمجية من خلال استكشاف [الوثائق الرسمية](https://docs.groupdocs.com/redaction/java/).  
- جرب أنواع إخفاء أخرى (مثل `RegexRedaction`، `ImageRedaction`).  
- انضم إلى المجتمع في [منتدى دعم GroupDocs](https://forum.groupdocs.com/c/redaction/33) للحصول على نصائح وأفضل الممارسات.

---

**آخر تحديث:** 2026-02-26  
**تم الاختبار مع:** GroupDocs.Redaction Java 24.9  
**المؤلف:** GroupDocs