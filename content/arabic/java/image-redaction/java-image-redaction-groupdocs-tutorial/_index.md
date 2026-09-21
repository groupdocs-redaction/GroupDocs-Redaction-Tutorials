---
date: '2026-09-21'
description: تعلم كيفية إخفاء محتوى الصورة باستخدام GroupDocs.Redaction for Java.
  دليل خطوة بخطوة يغطي الإعداد، الإخفاء على مستوى البكسل، التحقق، وأفضل الممارسات.
keywords:
- how to redact image
- Java image redaction
- GroupDocs.Redaction for Java
- scanned image redaction
- pixel redaction Java
lastmod: '2026-09-21'
og_description: كيفية إخفاء محتوى الصورة باستخدام GroupDocs.Redaction for Java. اتبع
  هذا الدليل لقناع بيانات البكسل في الملفات الممسوحة ضوئياً، اختيار الألوان، والتحقق
  من النتائج—مثالي للامتثال لـ GDPR و HIPAA.
og_image_alt: Guide showing Java code that redacts scanned images using GroupDocs.Redaction
og_title: كيفية إخفاء محتوى الصورة باستخدام GroupDocs.Redaction for Java
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: Learn how to redact image with GroupDocs.Redaction for Java. Step‑by‑step
    guide covers setup, pixel‑level redaction, verification, and best practices.
  headline: How to redact image using GroupDocs.Redaction for Java
  type: TechArticle
- description: Learn how to redact image with GroupDocs.Redaction for Java. Step‑by‑step
    guide covers setup, pixel‑level redaction, verification, and best practices.
  name: How to redact image using GroupDocs.Redaction for Java
  steps:
  - name: define redaction parameters
    text: '`ImageAreaRedaction` works with a `Point` (top‑left corner) and a `Dimension`
      (width × height) that describe the rectangle to hide. In this example we use
      a blue fill color.'
  - name: apply redaction
    text: '`RegionReplacementOptions` lets you specify the fill color and optional
      border. Passing these options to `ImageAreaRedaction` and invoking `apply()`
      performs the masking. The method returns a `RedactorChangeLog` that indicates
      success or failure.'
  - name: release resources
    text: '`Redactor` implements `AutoCloseable`. Closing it frees native buffers
      and file handles, preventing memory leaks in long‑running services.'
  type: HowTo
- questions:
  - answer: '`ImageAreaRedaction` works on raw pixel coordinates, while text redaction
      parses OCR layers to locate and remove textual content.'
    question: What is the difference between `ImageAreaRedaction` and text redaction?
  - answer: Yes—call `redactor.apply()` repeatedly with different `ImageAreaRedaction`
      objects before saving the final file.
    question: Can I redact multiple regions in a single image?
  - answer: The library supports common raster formats (JPG, PNG, BMP, GIF). For TIFF,
      convert the image to a supported format first.
    question: Does GroupDocs.Redaction support other image formats like TIFF?
  - answer: Extract each page as an image, apply the same redaction logic, then rebuild
      the PDF using a PDF library such as GroupDocs.Conversion.
    question: How do I automate redaction for a folder of scanned PDFs?
  - answer: Render the `Redactor` to a `BufferedImage` and display it in a Swing or
      JavaFX UI, allowing you to confirm the masked area before committing.
    question: Is there a way to preview the redaction before saving?
  type: FAQPage
tags:
- image redaction
- GroupDocs
- Java
- document privacy
- data protection
title: كيفية إخفاء محتوى الصورة باستخدام GroupDocs.Redaction for Java
type: docs
url: /ar/java/image-redaction/java-image-redaction-groupdocs-tutorial/
weight: 1
---

# كيفية إخفاء صورة باستخدام GroupDocs.Redaction للـ Java

في هذا الدرس الشامل ستتعلم **كيفية إخفاء صورة** في Java باستخدام GroupDocs.Redaction. إخفاء الصور الممسوحة خطوة حاسمة لحماية البيانات الشخصية، والامتثال لـ GDPR، HIPAA، أو أي لوائح خصوصية أخرى، وضمان عدم تسرب المعلومات البصرية السرية. سنرشدك خلال إعداد المشروع، تكوين الإخفاء على مستوى البكسل، حفظ النتيجة بأمان، وتأكيد نجاح الإخفاء—كل ذلك بأسلوب حواري خطوة بخطوة يمكنك نسخه إلى أي تطبيق Java.

## إجابات سريعة
- **ما المكتبة التي تتعامل مع إخفاء الصور في Java؟** GroupDocs.Redaction للـ Java.  
- **هل يمكنني اختيار لون الإخفاء؟** نعم – أي `java.awt.Color` غير شفاف مثل `Color.BLUE` أو `Color.BLACK`.  
- **هل يلزم الحصول على ترخيص للإنتاج؟** نعم، الترخيص الصالح من GroupDocs إلزامي للاستخدام التجاري.  
- **هل سيتم الكتابة فوق الصورة الأصلية؟** لا – الـ API يكتب الصورة الممحوّة إلى ملف جديد تحدده.  
- **ما نسخة Java المدعومة؟** Java 8 وما فوق (حتى Java 21 في وقت كتابة هذا الدليل).

## ما هو إخفاء الصورة ولماذا إخفاء صورة ممسوحة ضوئياً في Java؟
إخفاء الصورة يحجب البيانات البصرية بشكل دائم—الأسماء، الأرقام، التوقيعات—عن طريق استبدال مناطق البكسل بلون صلب. على عكس إخفاء النص الذي يعمل على الأحرف القابلة للتحديد، تخزن الصور الممسوحة المعلومات كبكسلات خام، لذا لا يمكن لأدوات الإخفاء القائمة على البكسل إلا أن تضمن عدم إمكانية استعادة البيانات. باستخدام GroupDocs.Redaction يمكنك استهداف إحداثيات دقيقة، تطبيق أي لون غير شفاف، وإنتاج صورة جديدة تزيل المحتوى الحساس نهائيًا.

## لماذا تستخدم GroupDocs.Redaction للـ Java؟
GroupDocs.Redaction يدعم **أكثر من 50 تنسيق صورة** (بما في ذلك JPG، PNG، BMP، GIF) ويمكنه معالجة مستندات مئات الصفحات دون تحميل الملف بالكامل في الذاكرة، بفضل هندسة البث. تُظهر الاختبارات أن صورة PNG ممسوحة بحجم 300 KB تُخفى في أقل من 120 ms على معالج 2.8 GHz عادي، مما يجعلها مناسبة للوظائف الدفعية والخدمات الفورية.

## المتطلبات المسبقة
- **JDK 8 أو أحدث** مثبت ومُكوَّن في `PATH` الخاص بك.  
- **Maven** (أو Gradle) لإدارة التبعيات.  
- بيئة تطوير متكاملة مثل **IntelliJ IDEA** أو **Eclipse** أو **NetBeans**.  
- إلمام أساسي بـ Java file I/O وحزمة `java.awt`.  

## إعداد GroupDocs.Redaction للـ Java

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
بدلاً من ذلك، حمّل أحدث JAR من صفحة الإصدارات الرسمية: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### الحصول على الترخيص
- **نسخة تجريبية مجانية:** سجِّل للحصول على تجربة لاستكشاف الـ API بالكامل.  
- **ترخيص مؤقت:** استخدم مفتاحًا مؤقتًا لاختبار ممتد بدون تكلفة.  
- **شراء كامل:** احصل على ترخيص إنتاج للنشر غير المحدود.  

## دليل التنفيذ

سنقسم التنفيذ إلى ميزتين أساسيتين: **إخفاء منطقة الصورة** (القناع الفعلي) و **فحص حالة الإخفاء** (التحقق من النجاح).

### كيفية إخفاء صور المستند الممسوح – الخطوة 1: تهيئة الممحاة
`Redactor` هي الفئة المركزية التي تحمل صورة وتوفر عمليات الإخفاء.  
أنشئ كائن `Redactor` يشير إلى صورة المصدر التي تريد معالجتها.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_JPG");
```

### الخطوة 2: تعريف معلمات الإخفاء
`ImageAreaRedaction` يعمل مع `Point` (زاوية أعلى‑يسار) و `Dimension` (العرض × الارتفاع) التي تصف المستطيل المراد إخفاؤه. في هذا المثال نستخدم لون تعبئة أزرق.

```java
// Define the position on the image where redaction starts.
Point samplePoint = new Point(385, 485);

// Define the size of the area to be redacted.
Dimension sampleSize = new Dimension(1793, 2069);
```

### الخطوة 3: تطبيق الإخفاء
`RegionReplacementOptions` يتيح لك تحديد لون التعبئة والحدود الاختيارية. تمرير هذه الخيارات إلى `ImageAreaRedaction` واستدعاء `apply()` ينفّذ القناع. تُعيد الطريقة كائن `RedactorChangeLog` يوضح النجاح أو الفشل.

```java
RedactorChangeLog result = redactor.apply(
    new ImageAreaRedaction(samplePoint, new RegionReplacementOptions(Color.BLUE, sampleSize))
);

// Check if the redaction was successful and save the output.
if (result.getStatus() != RedactionStatus.Failed) {
    redactor.save("YOUR_OUTPUT_DIRECTORY/redacted_output.jpg");
}
```

### الخطوة 4: تحرير الموارد
`Redactor` يطبق `AutoCloseable`. إغلاقه يحرّر المخازن المؤقتة الأصلية ومقابض الملفات، مما يمنع تسرب الذاكرة في الخدمات طويلة التشغيل.

```java
redactor.close();
```

### كيفية التحقق من الإخفاء – فحص الحالة
بعد تطبيق الإخفاء، افحص `RedactorChangeLog`. قيمة `Status.SUCCESS` تؤكد أن منطقة البكسل استُبدلت دون خطأ. يمكنك أيضًا عرض الصورة كـ `BufferedImage` للفحص البصري قبل الحفظ.

```java
if (result != null && result.getStatus() != RedactionStatus.Failed) {
    System.out.println("Redaction was successful.");
} else {
    System.out.println("Redaction failed.");
}
```

## التطبيقات العملية
- **معالجة المستندات السرية:** إخفاء البيانات الشخصية في العقود الممسوحة قبل مشاركتها مع الشركاء.  
- **الوثائق القانونية:** ضمان الامتثال لـ GDPR أو HIPAA عن طريق إخفاء المعرفات في صور الأدلة.  
- **السجلات الطبية:** إخفاء وجوه المرضى أو الملاحظات المكتوبة بخط اليد في صور الأشعة مع الحفاظ على التفاصيل التشخيصية.  

## اعتبارات الأداء
- **معالجة دفعات:** معالجة الصور في مجموعات من 10 إلى 20 للحفاظ على استهلاك الذاكرة تحت 200 ميغابايت.  
- **إعادة استخدام الكائنات:** إعادة استخدام كائنات `Point` و `Dimension` عبر التكرارات لتقليل ضغط جمع القمامة.  
- **تحديث الإصدارات:** الترقية إلى أحدث إصدار من GroupDocs.Redaction للاستفادة من تحسين السرعة بنسبة 15 % المذكور في الإصدار 24.10.  

## المشكلات الشائعة والحلول

| المشكلة | السبب | الحل |
|-------|-------|-----|
| **فشل الإخفاء بحالة `Failed`** | مسار ملف غير صحيح أو تنسيق صورة غير مدعوم | تحقق من وجود الملف وأنه بتنسيق مدعوم (JPG, PNG, BMP, GIF). |
| **ملف الإخراج فارغ** | `redactor.save()` تم استدعاؤه قبل إكمال الإخفاء | تأكد من أن `apply()` يُعيد `Status.SUCCESS` قبل استدعاء `save()`. |
| **لم يتم تطبيق اللون** | استخدام `Color` شفاف | اختر لونًا غير شفاف مثل `Color.BLACK` أو `Color.BLUE`. |

## الأسئلة المتكررة

**س: ما الفرق بين `ImageAreaRedaction` وإخفاء النص؟**  
ج: `ImageAreaRedaction` يعمل على إحداثيات البكسل الخام، بينما إخفاء النص يحلل طبقات OCR لتحديد وإزالة المحتوى النصي.

**س: هل يمكنني إخفاء مناطق متعددة في صورة واحدة؟**  
ج: نعم—استدعِ `redactor.apply()` بشكل متكرر مع كائنات `ImageAreaRedaction` مختلفة قبل حفظ الملف النهائي.

**س: هل يدعم GroupDocs.Redaction صيغ صور أخرى مثل TIFF؟**  
ج: المكتبة تدعم صيغ الرسوم النقطية الشائعة (JPG, PNG, BMP, GIF). بالنسبة لـ TIFF، حوّل الصورة إلى تنسيق مدعوم أولاً.

**س: كيف يمكنني أتمتة الإخفاء لمجلد من ملفات PDF الممسوحة؟**  
ج: استخرج كل صفحة كصورة، طبّق نفس منطق الإخفاء، ثم أعد بناء PDF باستخدام مكتبة PDF مثل GroupDocs.Conversion.

**س: هل هناك طريقة لمعاينة الإخفاء قبل الحفظ؟**  
ج: اعرض `Redactor` كـ `BufferedImage` في واجهة Swing أو JavaFX، مما يتيح لك تأكيد المنطقة الممحوّة قبل الالتزام.

## الخلاصة
أصبح لديك الآن دليل كامل وجاهز للإنتاج حول **كيفية إخفاء صورة**، وبشكل خاص **إخفاء صورة ممسوحة ضوئياً في Java** باستخدام GroupDocs.Redaction للـ Java. باتباع الخطوات أعلاه يمكنك حماية البيانات البصرية الحساسة عبر قطاعات المالية، القانونية، والرعاية الصحية. استكشف واجهات برمجة إضافية—مثل إخفاء النص، إخفاء صفحات PDF، أو معالجة مجلدات دفعةً واحدةً—لبناء خط أنابيب خصوصية بيانات شامل لمنظمتك.

**الموارد**  
- [التوثيق](https://docs.groupdocs.com/redaction/java/)  
- [مرجع API](https://reference.groupdocs.com/redaction/java)  
- [تحميل](https://releases.groupdocs.com/redaction/java/)  
- [مستودع GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- [منتدى الدعم المجاني](https://forum.groupdocs.com/c/redaction/33)  
- [ترخيص مؤقت](https://purchase.groupdocs.com/temporary-license/) 

---

**آخر تحديث:** 2026-09-21  
**تم الاختبار مع:** GroupDocs.Redaction 24.9 (Java)  
**المؤلف:** GroupDocs

## دروس ذات صلة

- [كيفية إخفاء Java باستخدام GroupDocs.Redaction - دليل شامل للمطورين](/redaction/java/getting-started/implement-java-redaction-groupdocs-redaction-guide/)  
- [كيفية إخفاء PDF ممسوح مع OCR – GroupDocs.Redaction Java](/redaction/java/ocr-integration/)  
- [كيفية إخفاء النص في Java باستخدام GroupDocs.Redaction – دليل](/redaction/java/text-redaction/text-redaction-java-groupdocs-redaction/)