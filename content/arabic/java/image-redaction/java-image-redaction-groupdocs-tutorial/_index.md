---
date: '2025-12-29'
description: تعلم كيفية إخفاء صور المستندات الممسوحة ضوئياً باستخدام GroupDocs.Redaction
  للغة Java. دليل خطوة بخطوة يغطي الإعداد، وإخفاء مناطق الصورة، والتحقق.
keywords:
- Java image redaction
- GroupDocs.Redaction for Java
- image area redaction
title: كيفية إخفاء معلومات الصور الممسوحة ضوئياً للوثائق باستخدام GroupDocs في Java
type: docs
url: /ar/java/image-redaction/java-image-redaction-groupdocs-tutorial/
weight: 1
---

# كيفية إخفاء صور المستندات الممسوحة ضوئياً باستخدام GroupDocs في Java

في المشهد الرقمي اليوم، **redact scanned document** يُعد إخفاء صور المستندات الممسوحة ضوئياً أمرًا أساسيًا لحماية الخصوصية وتلبية متطلبات الامتثال. سواء كنت بحاجة إلى إخفاء البيانات الشخصية في عقد ممسوح ضوئيًا أو طمس تفاصيل المريض في صورة طبية، يوضح لك هذا الدليل **how to redact image** بسرعة وبشكل موثوق باستخدام **GroupDocs.Redaction for Java**. سنستعرض كل شيء من إعداد المشروع إلى التحقق من نجاح الإخفاء، حتى تتمكن من دمج الحل في أي تطبيق Java بثقة.

## إجابات سريعة
- **ما المكتبة التي تتعامل مع إخفاء الصور في Java؟** GroupDocs.Redaction for Java  
- **هل يمكنني اختيار لون الإخفاء؟** نعم – أي `java.awt.Color` (مثال: `Color.BLUE`)  
- **هل يلزم وجود ترخيص للإنتاج؟** نعم، يلزم وجود ترخيص GroupDocs صالح  
- **هل سيتم استبدال الصورة الأصلية؟** لا – يتم حفظ النتيجة في ملف جديد  
- **ما إصدار Java المدعوم؟** Java 8+ (متوافق مع إصدارات JDK الحديثة)

## ما هو إخفاء الصور ولماذا نُخفي صور المستندات الممسوحة ضوئياً؟
إخفاء الصور يعني طمس المعلومات البصرية الحساسة بشكل دائم—مثل الأسماء أو الأرقام أو التوقيعات—بحيث لا يمكن استعادتها. عندما تتعامل مع مستندات ممسوحة ضوئيًا، تكون البيانات مدمجة كبيكسلات، مما يجعل أدوات إخفاء النص التقليدية غير فعّالة. باستخدام GroupDocs.Redaction يمكنك استهداف مناطق بيكسلية دقيقة واستبدالها بلون صلب، مما يضمن إزالة المعلومات فعليًا.

## المتطلبات المسبقة
- **JDK 8 أو أحدث** مثبت  
- **Maven** (أو أداة بناء أخرى) لإدارة التبعيات  
- بيئة تطوير متكاملة مثل **IntelliJ IDEA**، **Eclipse**، أو **NetBeans**  
- معرفة أساسية بـ Java وإلمام بملفات الإدخال/الإخراج (I/O)

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
- **تجربة مجانية:** اشترك لتجربة الـ API.  
- **ترخيص مؤقت:** استخدم مفتاحًا مؤقتًا للاختبار المطول.  
- **شراء كامل:** احصل على ترخيص إنتاج للاستخدام غير المحدود.

## دليل التنفيذ
سنقسم التنفيذ إلى ميزتين أساسيتين: **إخفاء منطقة الصورة** (التمويه الفعلي) و**التحقق من حالة الإخفاء** (التأكد من النجاح).

### كيفية إخفاء صور المستندات الممسوحة ضوئياً – الخطوة 1: تهيئة الـ Redactor
أولاً، أنشئ كائن `Redactor` يشير إلى الصورة التي تريد معالجتها.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_JPG");
```

### الخطوة 2: تعريف معلمات الإخفاء
حدد الزاوية العلوية اليسرى (`Point`) والحجم (`Dimension`) للمستطيل الذي تريد إخفائه. في هذا المثال نستخدم تعبئة زرقاء.

```java
// Define the position on the image where redaction starts.
Point samplePoint = new Point(385, 485);

// Define the size of the area to be redacted.
Dimension sampleSize = new Dimension(1793, 2069);
```

### الخطوة 3: تطبيق الإخفاء
أنشئ كائن `ImageAreaRedaction` مع `RegionReplacementOptions` ونفّذه. تُعيد الطريقة كائن `RedactorChangeLog` يُخبرك ما إذا كانت العملية ناجحة.

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

### كيفية التحقق من الإخفاء – فحص الحالة
بعد تطبيق الإخفاء، يمكنك فحص `RedactorChangeLog` للتأكد من أن العملية لم تفشل.

```java
if (result != null && result.getStatus() != RedactionStatus.Failed) {
    System.out.println("Redaction was successful.");
} else {
    System.out.println("Redaction failed.");
}
```

## تطبيقات عملية
- **معالجة المستندات السرية:** طمس البيانات الشخصية تلقائيًا في العقود الممسوحة قبل مشاركتها مع أطراف خارجية.  
- **الوثائق القانونية:** ضمان الامتثال للـ GDPR أو HIPAA عبر إخفاء المعرفات في صور الأدلة.  
- **السجلات الطبية:** حماية خصوصية المرضى بطمس الوجوه أو الملاحظات المكتوبة يدويًا في صور الأشعة.

## اعتبارات الأداء
- **المعالجة الدفعية:** حمّل وأخفِ الصور على دفعات صغيرة للحفاظ على انخفاض استهلاك الذاكرة.  
- **هياكل بيانات فعّالة:** أعد استخدام كائنات `Point` و `Dimension` عند معالجة عدد كبير من الصور.  
- **ابقَ محدثًا:** قم بترقية إلى أحدث إصدار من GroupDocs.Redaction بانتظام للحصول على تحسينات الأداء وإصلاحات الأخطاء.

## المشكلات الشائعة والحلول
| المشكلة | السبب | الحل |
|-------|-------|-----|
| **فشل الإخفاء بحالة `Failed`** | مسار ملف غير صحيح أو تنسيق صورة غير مدعوم | تحقق من وجود الصورة وأنها بتنسيق مدعوم (JPG، PNG، BMP). |
| **ملف الإخراج فارغ** | `redactor.save()` تم استدعاؤه قبل اكتمال الإخفاء | تأكد من أن `apply()` تُعيد حالة نجاح قبل الحفظ. |
| **اللون غير مُطبق** | استخدام لون شفاف | اختر لونًا غير شفاف `Color` (مثال: `Color.BLACK` أو `Color.BLUE`). |

## الأسئلة المتكررة

**س: ما الفرق بين `ImageAreaRedaction` و إخفاء النص؟**  
ج: `ImageAreaRedaction` يعمل على إحداثيات البكسل، بينما إخفاء النص يحلل طبقات OCR لتحديد وإزالة المحتوى النصي.

**س: هل يمكنني إخفاء مناطق متعددة في صورة واحدة؟**  
ج: نعم—استدعِ `redactor.apply()` بشكل متكرر مع كائنات `ImageAreaRedaction` مختلفة قبل الحفظ.

**س: هل يدعم GroupDocs.Redaction صيغ صور أخرى مثل TIFF؟**  
ج: المكتبة تدعم صيغ الرسوم النقطية الشائعة (JPG، PNG، BMP، GIF). بالنسبة لـ TIFF، يجب تحويله إلى صيغة مدعومة أولاً.

**س: كيف يمكنني أتمتة الإخفاء لمجلد من ملفات PDF الممسوحة؟**  
ج: قم بالتكرار على كل صورة صفحة مستخرجة من الـ PDF، طبّق نفس منطق الإخفاء، ثم أعد بناء الـ PDF باستخدام مكتبة PDF.

**س: هل هناك طريقة لمعاينة الإخفاء قبل الحفظ؟**  
ج: يمكنك تحويل الـ `Redactor` إلى `BufferedImage` وعرضه في واجهة Swing أو JavaFX قبل تنفيذ التغييرات.

## الخلاصة
أصبح لديك الآن دليل كامل وجاهز للإنتاج حول **كيفية إخفاء محتوى الصورة**، وبشكل خاص **إخفاء صور المستندات الممسوحة** باستخدام GroupDocs.Redaction for Java. باتباع الخطوات السابقة، يمكنك حماية البيانات البصرية الحساسة عبر مجموعة واسعة من الصناعات. استكشف الـ APIs الإضافية—مثل إخفاء النص أو إخفاء صفحات PDF—لبناء حل شامل لخصوصية البيانات لمؤسستك.

---

**آخر تحديث:** 2025-12-29  
**تم الاختبار مع:** GroupDocs.Redaction 24.9 (Java)  
**المؤلف:** GroupDocs  

**الموارد**  
- [الوثائق](https://docs.groupdocs.com/redaction/java/)  
- [مرجع API](https://reference.groupdocs.com/redaction/java)  
- [تحميل](https://releases.groupdocs.com/redaction/java/)  
- [مستودع GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- [منتدى الدعم المجاني](https://forum.groupdocs.com/c/redaction/33)  
- [ترخيص مؤقت](https://purchase.groupdocs.com/temporary-license/)