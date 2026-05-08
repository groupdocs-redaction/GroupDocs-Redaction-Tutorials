---
date: '2026-02-13'
description: تعلم كيفية إنشاء ملف PDF بالأبيض والأسود باستخدام GroupDocs.Redaction
  للغة Java، وتحويل PDF إلى أبيض وأسود بأمان مع الحفاظ على جودة المستند.
keywords:
- GroupDocs.Redaction
- Java
- Document Processing
title: كيفية إنشاء ملف PDF بالأبيض والأسود باستخدام GroupDocs.Redaction Java – أمان
  وتحسين مستنداتك
type: docs
url: /ar/java/rasterization-options/grayscale-rasterization-groupdocs-redaction-java/
weight: 1
---

 produce final content.# GroupDocs.Redaction Java: دليل الترصيص بتدرج الرمادي

## Introduction

إذا كنت بحاجة إلى **create grayscale pdf** مع الحفاظ على أمان مستنداتك ومظهرها الاحترافي، فأنت في المكان الصحيح. في هذا الدرس سنستعرض الخطوات الدقيقة لتحويل ملفات DOCX، PDF أو أي ملفات مدعومة أخرى الملونة إلى نسخة نظيفة ومُرصّصة بتدرج الرمادي باستخدام GroupDocs.Redaction للـ Java. ستتعلم لماذا يضيف الترصيص طبقة أمان إضافية، وكيفية تكوين المكتبة، وكيفية إدارة الموارد بكفاءة—كل ذلك بأسلوب حواري خطوة بخطوة.

## Quick Answers
- **ماذا يفعل الترصيص بتدرج الرمادي؟** يحول كل صفحة من المستند إلى صورة عالية الدقة ثم يطبق مرشح تدرج الرمادي، مما يزيل جميع معلومات اللون.  
- **لماذا نستخدم GroupDocs.Redaction لهذا؟** يجمع بين أمان الحذف مع خيارات الترصيص القوية في واجهة برمجة تطبيقات واحدة.  
- **ما الصيغ المدعومة؟** DOCX، PDF، XLSX، PPTX، RTF والعديد غيرها.  
- **هل أحتاج إلى ترخيص؟** يلزم وجود ترخيص صالح لـ GroupDocs.Redaction للاستخدام في الإنتاج؛ تتوفر نسخة تجريبية للاختبار.  
- **ما نسخة Java المطلوبة؟** JDK 8 أو أعلى.

## What is **create grayscale pdf**?

إنشاء PDF بتدرج الرمادي يعني تحويل كل عنصر بصري في المستند الأصلي إلى درجات من الرمادي. النتيجة هي ملف أصغر ومناسب للطباعة يزيل المشتتات المتعلقة بالألوان ويضيف فائدة أمان طفيفة لأن المحتوى يصبح الآن معتمدًا على الصور.

## Why use grayscale rasterization with GroupDocs.Redaction?

- **أمان معزز** – لا يمكن تحديد الصفحات المرصّصة أو نسخها أو تحريرها كنص.  
- **مظهر متسق** – تُزال الألوان، مما يمنح مظهرًا موحدًا واحترافيًا.  
- **دعم صيغ واسع** – تعمل نفس الواجهة مع DOCX، PDF، PPTX، وغير ذلك.  
- **تحكم دقيق** – يمكنك ضبط DPI، صيغة الإخراج، والخيارات المتقدمة مثل تحويل إلى تدرج الرمادي.

## Prerequisites

- مجموعة تطوير Java (JDK) 8 أو أحدث. تحقق باستخدام `java -version`.  
- بيئة تطوير متكاملة (IDE) مثل IntelliJ IDEA أو Eclipse أو NetBeans لتسهيل كتابة الكود وتصحيح الأخطاء.  
- إضافة GroupDocs.Redaction للـ Java عبر Maven أو Gradle.  
- مستند تجريبي (مثال: DOCX متعدد الصفحات) يمكنك تجربة التغييرات عليه بأمان.  
- مساحة كافية على القرص للإخراج المرصّص (قد تكون ملفات الرستر أكبر من المصدر).

## Import Packages

إعداد الاستيرادات الصحيحة يشبه تنظيم صندوق الأدوات قبل بدء المشروع. الاستيرادات التالية تمنحك الوصول إلى الفئة الأساسية Redactor وخيارات الترصيص التي سنحتاجها.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.options.RasterizationOptions;
import com.groupdocs.redaction.options.AdvancedRasterizationOptions;
```

## Step 1: Initialize the Redactor Object

إنشاء مثيل `Redactor` يفتح الباب أمام جميع إمكانيات معالجة المستندات.

```java
final Redactor redactor = new Redactor(Constants.MULTIPAGE_SAMPLE_DOCX);
```

استبدل `Constants.MULTIPAGE_SAMPLE_DOCX` بالمسار إلى الملف الذي تريد تحويله إلى PDF بتدرج الرمادي.

## Step 2: Configure Save Options

`SaveOptions` يحدد كيفية كتابة الملف النهائي. إضافة لاحقة تساعدك على الحفاظ على الملف الأصلي دون تعديل.

```java
SaveOptions so = new SaveOptions();
so.setRedactedFileSuffix("_scan");
```

سيُسمى الناتج `yourfile_scan.docx` (أو الصيغة التي تحددها لاحقًا).

## Step 3: Enable Rasterization

تشغيل الترصيص يخبر المحرك بتمثيل كل صفحة كصورة قبل الحفظ.

```java
so.getRasterization().setEnabled(true);
```

الترصيص هو الأساس لإنشاء PDF بتدرج الرمادي لأنه يحول المستند إلى تمثيل مبني على الصور.

## Step 4: Apply Grayscale Conversion

الآن نضيف مرشح تدرج الرمادي إلى خط أنابيب الترصيص.

```java
so.getRasterization().addAdvancedOption(AdvancedRasterizationOptions.Grayscale);
```

هذا الخيار يجبر كل بكسل على أن يُرسم بدرجات من الرمادي، مما يمنحك نتيجة **create grayscale pdf** التي تبحث عنها.

## Step 5: Execute the Document Transformation

استدعاء `save` ينفّذ سلسلة المعالجة بالكامل.

```java
redactor.save(so);
```

بعد تنفيذ هذا السطر، ستجد ملفًا جديدًا على القرص يكون مُرصّصًا بالكامل، بتدرج الرمادي، ومُحفظًا باللاحقة `_scan`.

## Step 6: Proper Resource Management

تنظيف الموارد يمنع حجز الملفات وتسرب الذاكرة.

```java
finally { redactor.close(); }
```

في Java الحديثة يمكنك أيضًا استخدام نمط try‑with‑resources، الذي يغلق `Redactor` تلقائيًا:

```java
try (Redactor redactor = new Redactor(Constants.MULTIPAGE_SAMPLE_DOCX)) {
    // Your processing code here
}
// Automatic cleanup happens here
```

كلا النهجين آمان؛ الأخير أكثر اختصارًا.

## Advanced Configuration Options

### Adjust DPI for Quality or Size

قيمة DPI أعلى تنتج صورًا أكثر وضوحًا (مناسب للطباعة)، بينما DPI أقل يقلل حجم الملف.

```java
saveOptions.getRasterization().setDpi(300); // High quality for printing
// or
saveOptions.getRasterization().setDpi(150); // Balanced quality and size
```

### Choose an Output Format

يمكنك إجبار النتيجة المرصّصة على أن تكون بصيغة حاوية محددة، مثل PDF.

```java
saveOptions.setRasterizationFormat(RasterizationFormat.PDF);
```

## Common Use Cases

- **أرشفة المستندات القانونية** – إنشاء ملفات PDF بتدرج الرمادي غير قابلة للتعديل.  
- **تقارير جاهزة للطباعة** – ضمان إخراج أبيض‑أسود متسق للطباعة الضخمة.  
- **سير عمل الامتثال** – دمج الحذف مع الترصيص بتدرج الرمادي لتلبية اللوائح الصارمة لحماية البيانات.

## Common Issues and Solutions

| المشكلة | سبب حدوثه | الحل |
|-------|----------------|-----|
| ملف الإخراج أكبر من المتوقع | تم ضبط DPI عالي جدًا أو تم تعطيل ضغط الصورة | خفض DPI (مثلاً 150) أو تمكين الضغط في `RasterizationOptions`. |
| النص يبدو غير واضح | DPI غير كافٍ لحجم الخط الأصلي | زيادة DPI إلى 300 أو أعلى. |
| العملية ترمي `OutOfMemoryError` على المستندات الكبيرة | تم تحميل المستند بالكامل في الذاكرة | استخدم واجهات برمجة التطبيقات المتدفقة أو عالج الصفحات على دفعات إذا كان ذلك مدعومًا. |
| لم يتم تطبيق تدرج الرمادي | الخيار المتقدم لم يُضاف بشكل صحيح | تحقق من استدعاء `addAdvancedOption(AdvancedRasterizationOptions.Grayscale)` قبل `save()`. |

## Frequently Asked Questions

**س: هل يمكنني تحويل المستندات إلى تدرج الرمادي دون الترصيص؟**  
ج: في GroupDocs.Redaction، خيار تدرج الرمادي مرتبط بالترصيص، مما يضمن نتائج متسقة ويضيف أمانًا.

**س: ما هي صيغ المستندات التي تدعم الترصيص بتدرج الرمادي؟**  
ج: جميع الصيغ الرئيسية المدعومة من GroupDocs.Redaction—بما في ذلك DOCX، PDF، XLSX، PPTX، RTF، وغيرها—يمكن ترصيصها وتحويلها إلى تدرج الرمادي.

**س: هل سيؤثر الترصيص على حجم ملفات المستندات؟**  
ج: نعم. قد تزداد حجم الملفات التي تحتوي على نصوص كثيرة، بينما قد يقل حجم الملفات التي تحتوي على صور كثيرة. إعدادات DPI هي الأكثر تأثيرًا.

**س: هل يمكن عكس عملية الترصيص بتدرج الرمادي؟**  
ج: لا. الترصيص عملية أحادية الاتجاه؛ احتفظ بنسخة احتياطية من الأصل إذا كنت بحاجة للعودة.

**س: كيف يمكنني تحسين جودة المستندات المرصّصة بتدرج الرمادي؟**  
ج: استخدم DPI أعلى (300 + لجودة الطباعة) واختر صيغة إخراج مناسبة (PDF شائعة للأرشفة).

## Conclusion

أصبح لديك الآن وصفة كاملة وجاهزة للإنتاج لإنشاء ملفات **create grayscale pdf** باستخدام GroupDocs.Redaction للـ Java. من خلال تمكين الترصيص، وإضافة الخيار المتقدم لتدرج الرمادي، وإدارة الموارد بشكل مسؤول، يمكنك إنتاج مستندات آمنة ومناسبة للطباعة تلبي معايير الامتثال.

---

**آخر تحديث:** 2026-02-13  
**تم الاختبار مع:** GroupDocs.Redaction 23.11 للـ Java  
**المؤلف:** GroupDocs