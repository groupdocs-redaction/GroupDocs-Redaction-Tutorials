---
date: '2026-03-22'
description: تعلم كيفية تعديل الصور الممسوحة ضوئياً باستخدام Java مع GroupDocs.Redaction.
  يغطي هذا الدليل خطوة بخطوة الإعداد، تعديل منطقة الصورة، والتحقق.
keywords:
- Java image redaction
- GroupDocs.Redaction for Java
- image area redaction
title: كيفية إخفاء صورة ممسوحة ضوئياً باستخدام جافا وGroupDocs
type: docs
url: /ar/java/image-redaction/java-image-redaction-groupdocs-tutorial/
weight: 1
---

# كيفية تعديل (redact) صورة ممسوحة ضوئياً باستخدام Java وGroupDocs

في المشهد الرقمي اليوم، **redact scanned image java** أمر أساسي لحماية الخصوصية وتلبية متطلبات الامتثال. سواء كنت بحاجة إلى إخفاء البيانات الشخصية في عقد ممسوح ضوئياً أو إخفاء تفاصيل المريض في صورة طبية، يوضح لك هذا الدليل **how to redact image** المحتوى بسرعة وموثوقية باستخدام **GroupDocs.Redaction for Java**. سنستعرض كل شيء بدءًا من إعداد المشروع إلى التحقق من نجاح عملية التعديل، حتى تتمكن من دمج الحل في أي تطبيق Java بثقة.

## إجابات سريعة
- **ما المكتبة التي تتعامل مع تعديل الصور في Java؟** GroupDocs.Redaction for Java  
- **هل يمكنني اختيار لون التعديل؟** نعم – أي `java.awt.Color` (مثال: `Color.BLUE`)  
- **هل يلزم وجود ترخيص للإنتاج؟** نعم، يلزم وجود ترخيص GroupDocs صالح  
- **هل سيتم استبدال الصورة الأصلية؟** لا – يتم حفظ النتيجة في ملف جديد  
- **ما نسخة Java المدعومة؟** Java 8+ (متوافقة مع إصدارات JDK الحديثة)

## ما هو تعديل الصورة ولماذا نحتاج إلى redact scanned image java؟
تعديل الصورة يعني إخفاء المعلومات البصرية الحساسة بشكل دائم—مثل الأسماء، الأرقام، أو التوقيعات—بحيث لا يمكن استعادتها. عندما تتعامل مع مستندات ممسوحة ضوئياً، تكون البيانات مدمجة كبيكسلات، مما يجعل أدوات تعديل النص التقليدية غير فعّالة. باستخدام GroupDocs.Redaction يمكنك استهداف مناطق بيكسلية دقيقة واستبدالها بلون صلب، مما يضمن إزالة المعلومات تمامًا.

## المتطلبات المسبقة
- **JDK 8 أو أحدث** مثبت  
- **Maven** (أو أداة بناء أخرى) لإدارة الاعتمادات  
- بيئة تطوير متكاملة مثل **IntelliJ IDEA**، **Eclipse**، أو **NetBeans**  
- معرفة أساسية بـ Java وإلمام بعمليات I/O للملفات  

## إعداد GroupDocs.Redaction لـ Java

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
بدلاً من ذلك، قم بتحميل أحدث ملف JAR من صفحة الإصدارات الرسمية: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### الحصول على الترخيص
- **Free Trial:** سجّل للحصول على نسخة تجريبية لاستكشاف الـ API.  
- **Temporary License:** استخدم مفتاحًا مؤقتًا للاختبار الموسع.  
- **Full Purchase:** احصل على ترخيص إنتاج لاستخدام غير محدود.

## دليل التنفيذ

سنقسم التنفيذ إلى ميزتين أساسيتين: **Image Area Redaction** (الإخفاء الفعلي) و**Redaction Status Check** (التحقق من النجاح).

### كيفية تعديل صور المستندات الممسوحة – الخطوة 1: تهيئة الـ Redactor
أولاً، أنشئ كائن `Redactor` يشير إلى الصورة التي تريد معالجتها.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_JPG");
```

### الخطوة 2: تعريف معلمات التعديل
حدد الزاوية العلوية اليسرى (`Point`) وحجم (`Dimension`) المستطيل الذي تريد إخفائه. في هذا المثال نستخدم تعبئة زرقاء.

```java
// Define the position on the image where redaction starts.
Point samplePoint = new Point(385, 485);

// Define the size of the area to be redacted.
Dimension sampleSize = new Dimension(1793, 2069);
```

### الخطوة 3: تطبيق التعديل
أنشئ كائن `ImageAreaRedaction` مع `RegionReplacementOptions` ونفّذ العملية. تُعيد الطريقة كائن `RedactorChangeLog` يُخبرك ما إذا كانت العملية ناجحة.

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
دائمًا أغلق الـ `Redactor` عند الانتهاء لتحرير الموارد الأصلية.

```java
redactor.close();
```

### كيفية التحقق من التعديل – فحص الحالة
بعد تطبيق التعديل، يمكنك فحص `RedactorChangeLog` للتأكد من أن العملية لم تفشل.

```java
if (result != null && result.getStatus() != RedactionStatus.Failed) {
    System.out.println("Redaction was successful.");
} else {
    System.out.println("Redaction failed.");
}
```

## تطبيقات عملية
- **Confidential Document Handling:** إخفاء البيانات الشخصية تلقائيًا في العقود الممسوحة قبل مشاركتها مع أطراف خارجية.  
- **Legal Documentation:** ضمان الامتثال للـ GDPR أو HIPAA عبر تعديل المعرفات في صور الأدلة.  
- **Medical Records:** حماية خصوصية المرضى بإخفاء الوجوه أو الملاحظات المكتوبة يدويًا في صور الأشعة.

## اعتبارات الأداء
- **Batch Processing:** حمّل وعدّل الصور على دفعات صغيرة للحفاظ على استهلاك الذاكرة منخفضًا.  
- **Efficient Data Structures:** أعد استخدام كائنات `Point` و `Dimension` عند معالجة عدد كبير من الصور.  
- **Stay Updated:** قم بترقية GroupDocs.Redaction إلى أحدث نسخة بانتظام للحصول على تحسينات الأداء وإصلاحات الأخطاء.

## المشكلات الشائعة والحلول
| Issue | Cause | Fix |
|-------|-------|-----|
| **Redaction fails with `Failed` status** | مسار ملف غير صحيح أو تنسيق صورة غير مدعوم | تحقق من وجود الصورة وأنها بتنسيق مدعوم (JPG, PNG, BMP). |
| **Output file is empty** | تم استدعاء `redactor.save()` قبل إكمال عملية التعديل | تأكد من أن `apply()` تُعيد حالة نجاح قبل الحفظ. |
| **Color not applied** | استخدام لون شفاف | اختر لونًا غير شفاف `Color` (مثال: `Color.BLACK` أو `Color.BLUE`). |

## الأسئلة المتكررة

**س: ما الفرق بين `ImageAreaRedaction` وتعديل النص؟**  
ج: يعمل `ImageAreaRedaction` على إحداثيات البيكسل، بينما يقوم تعديل النص بتحليل طبقات OCR لتحديد وإزالة المحتوى النصي.

**س: هل يمكنني تعديل مناطق متعددة في صورة واحدة؟**  
ج: نعم—استدعِ `redactor.apply()` مرارًا مع كائنات `ImageAreaRedaction` مختلفة قبل الحفظ.

**س: هل يدعم GroupDocs.Redaction صيغ صور أخرى مثل TIFF؟**  
ج: المكتبة تدعم صيغ الرسوم النقطية الشائعة (JPG, PNG, BMP, GIF). بالنسبة لـ TIFF، يجب تحويلها إلى صيغة مدعومة أولاً.

**س: كيف يمكنني أتمتة تعديل مجموعة من ملفات PDF الممسوحة؟**  
ج: قم بالتكرار على كل صورة صفحة مستخرجة من الـ PDF، طبّق نفس منطق التعديل، ثم أعد بناء الـ PDF باستخدام مكتبة PDF.

**س: هل هناك طريقة لمعاينة التعديل قبل الحفظ؟**  
ج: يمكنك تحويل الـ `Redactor` إلى `BufferedImage` وعرضه في واجهة Swing أو JavaFX قبل تنفيذ التغييرات نهائيًا.

## الخلاصة
الآن لديك دليل كامل وجاهز للإنتاج حول **how to redact image**، وبشكل خاص حول **redact scanned image java** باستخدام GroupDocs.Redaction for Java. باتباع الخطوات أعلاه، يمكنك حماية البيانات البصرية الحساسة عبر مجموعة واسعة من الصناعات. استكشف الـ APIs الإضافية—مثل تعديل النص أو تعديل صفحات PDF—لبناء حل شامل لخصوصية البيانات لمؤسستك.

**الموارد**  
- [Documentation](https://docs.groupdocs.com/redaction/java/)  
- [API Reference](https://reference.groupdocs.com/redaction/java)  
- [Download](https://releases.groupdocs.com/redaction/java/)  
- [GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- [Free Support Forum](https://forum.groupdocs.com/c/redaction/33)  
- [Temporary License](https://purchase.groupdocs.com/temporary-license/) 

---

**آخر تحديث:** 2026-03-22  
**تم الاختبار على:** GroupDocs.Redaction 24.9 (Java)  
**المؤلف:** GroupDocs