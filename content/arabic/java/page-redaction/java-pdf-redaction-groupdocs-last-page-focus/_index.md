---
date: '2026-04-20'
description: تعلم كيفية تعديل الصفحة الأخيرة من ملف PDF باستخدام GroupDocs.Redaction
  للغة Java، واستبدال النص في PDF باستخدام Java وإخفاء البيانات الحساسة في PDF بفعالية.
keywords:
- redact last page pdf
- replace text pdf java
- hide sensitive data pdf
title: تعتيم الصفحة الأخيرة من ملف PDF باستخدام GroupDocs.Redaction للغة Java
type: docs
url: /ar/java/page-redaction/java-pdf-redaction-groupdocs-last-page-focus/
weight: 1
---

# إخفاء الصفحة الأخيرة من PDF باستخدام GroupDocs.Redaction للـ Java

في المشهد الرقمي اليوم، يعتبر **redact last page pdf** للملفات أمرًا أساسيًا لحماية المعلومات السرية والامتثال للوائح الخصوصية. يشرح هذا الدليل كيفية استخدام GroupDocs.Redaction للـ Java لاستهداف الصفحة الأخيرة من PDF وإخفاء البيانات الحساسة في مناطق محددة. في النهاية، ستكون قادرًا على استبدال النص بأسلوب pdf java وإخفاء البيانات الحساسة في PDF أينما ظهرت.

## إجابات سريعة
- **What is the primary goal?** الهدف الأساسي هو إخفاء الصفحة الأخيرة من PDF ومناطق محددة داخلها.  
- **Which library is used?** المكتبة المستخدمة هي GroupDocs.Redaction للـ Java.  
- **Do I need a license?** ترخيص تجريبي أو مؤقت يكفي للاختبار؛ يلزم الحصول على ترخيص كامل للإنتاج.  
- **What Java version is required?** Java 8 أو أعلى مع دعم Maven.  
- **Can I target other pages?** نعم، يمكن تعديل الفلاتر لنطاق أي صفحات أخرى.

## ما هو إخفاء محتوى PDF؟
الإخفاء يعني إزالة المحتوى أو تغطيته بشكل دائم من PDF بحيث لا يمكن استعادته. عندما تقوم بـ **redact last page pdf**، تضمن أن أي معلومات سرية على الصفحة الأخيرة مخفية تمامًا.

## لماذا نستخدم GroupDocs.Redaction للـ Java؟
يوفر GroupDocs.Redaction مجموعة غنية من الفلاتر—نطاق الصفحات، الفلاتر القائمة على المنطقة، والفلاتر القائمة على النص—التي تسمح لك بالتحكم بدقة فيما يتم إزالته. وهو مفيد بشكل خاص لـ:

- **Replacing text pdf java** دون تعديل باقي المستند.  
- **Hiding sensitive data pdf** مثل المعرفات الشخصية، الأرقام المالية، أو البنود القانونية.  
- أتمتة فحوصات الامتثال عبر دفعات كبيرة من المستندات.

## المتطلبات المسبقة
- **Java Development Kit (JDK) 8+** مثبت.  
- **Maven** لإدارة الاعتمادات.  
- الوصول إلى ترخيص **GroupDocs.Redaction** (تجريبي، مؤقت، أو مُشتَرَى).  

## إعداد GroupDocs.Redaction للـ Java

### إعداد Maven
أضف المستودع والاعتماد إلى ملف `pom.xml` الخاص بك:

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
إذا كنت تفضل عدم استخدام Maven، احصل على أحدث JAR من الموقع الرسمي: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

#### خطوات الحصول على الترخيص
- **Free Trial:** اختبار جميع الميزات دون التزام.  
- **Temporary License:** للاستخدام في المشاريع قصيرة الأمد أو التقييمات.  
- **Purchase:** إلغاء القيود واستخدام غير محدود ودعم أولوي.

## التهيئة الأساسية
أولاً، أنشئ كائن `Redactor` يشير إلى ملف PDF الخاص بك:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_PDF");
```

هذا الكائن هو نقطة الدخول لجميع عمليات الإخفاء.

## كيفية إخفاء الصفحة الأخيرة من PDF – دليل خطوة بخطوة

### الميزة 1: إخفاء مناطق محددة في الصفحة الأخيرة

#### الخطوة 1: تحميل مستند PDF
```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_PDF");
```

#### الخطوة 2: استرجاع معلومات الصفحة
```java
IDocumentInfo info = redactor.getDocumentInfo();
PageInfo lastPage = info.getPages().get(info.getPageCount() - 1);
```
معرفة أبعاد الصفحة الأخيرة يتيح لك تحديد إحداثيات دقيقة.

#### الخطوة 3: تعريف خيارات الاستبدال
```java
ReplacementOptions options = new ReplacementOptions("[secret]");
```
هنا نختار نص العنصر النائب الذي سيستبدل المحتوى المُخفى.

#### الخطوة 4: إعداد الفلاتر للإخفاء المستهدف
```java
options.setFilters(new RedactionFilter[] {
    new PageRangeFilter(PageSeekOrigin.End, 0, 1),
    new PageAreaFilter(
        new java.awt.Point(0, lastPage.getHeight() / 2),
        new java.awt.Dimension(lastPage.getWidth(), lastPage.getHeight() / 2)
    )
});
```
- `PageRangeFilter` يختار **الصفحة الأخيرة**.  
- `PageAreaFilter` يقتصر العملية على النصف السفلي من تلك الصفحة.

#### الخطوة 5: تطبيق الإخفاء (replace text pdf java)
```java
RedactorChangeLog result = redactor.apply(new ExactPhraseRedaction("bibliography", false, options));
```
يتم استبدال كلمة “bibliography” بـ “[secret]” فقط داخل المنطقة المحددة.

#### الخطوة 6: التحقق من النجاح والحفظ
```java
if (result.getStatus() != RedactionStatus.Failed) {
    redactor.save("YOUR_OUTPUT_DIRECTORY/redacted_output.pdf");
}
```
تحقق دائمًا من الحالة قبل كتابة ملف الإخراج.

#### الخطوة 7: تنظيف الموارد
```java
redactor.close();
```
إغلاق كائن `Redactor` يحرر الذاكرة ومقابض الملفات.

### الميزة 2: تصفية نطاق الصفحات للإخفاءات

#### الخطوة 1: تحميل مستند PDF
```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_PDF");
```

#### الخطوة 2: الوصول إلى معلومات المستند
```java
IDocumentInfo info = redactor.getDocumentInfo();
```

#### الخطوة 3: إنشاء فلتر نطاق الصفحات (hide sensitive data pdf)
```java
PageRangeFilter pageRangeFilter = new PageRangeFilter(PageSeekOrigin.End, 0, 1);
```
هذا الفلتر يعزل الصفحة الأخيرة، مما يتيح لك تطبيق أي منطق إخفاء تحتاجه.

### الميزة 3: إخفاء قائم على المنطقة في صفحات PDF

#### الخطوة 1: تحميل مستند PDF
```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_PDF");
```

#### الخطوة 2: الحصول على تفاصيل الصفحة
```java
IDocumentInfo info = redactor.getDocumentInfo();
PageInfo lastPage = info.getPages().get(info.getPageCount() - 1);
```

#### الخطوة 3: تعريف فلتر المنطقة (hide sensitive data pdf)
```java
PageAreaFilter areaFilter = new PageAreaFilter(
    new java.awt.Point(0, lastPage.getHeight() / 2),
    new java.awt.Dimension(lastPage.getWidth(), lastPage.getHeight() / 2)
);
```
يستهدف الفلتر النصف السفلي من الصفحة الأخيرة—مثالي لإزالة التذييلات أو التوقيعات.

#### الخطوة 4: تحرير الموارد
```java
redactor.close();
```

## تطبيقات عملية
- **الوثائق القانونية:** إخفاء أسماء العملاء أو أرقام القضايا في الصفحة الأخيرة قبل المشاركة.  
- **التقارير المالية:** إخفاء أرقام الحسابات أو الملخصات السرية.  
- **السجلات الصحية:** إزالة معرفات المرضى للامتثال لـ HIPAA.  
- **المسودات قبل الإصدار:** إخفاء الأقسام التي لا تزال قيد المراجعة.

## نصائح للأداء
- **إعادة استخدام كائن `Redactor`** عند معالجة عدة ملفات PDF في دفعة واحدة.  
- **إغلاق الكائن فورًا** لتجنب تسرب الذاكرة، خاصة مع الملفات الكبيرة.  
- **اختبار على عينة** قبل التشغيل على المستندات الإنتاجية للتحقق من إحداثيات الفلاتر.

## الأسئلة المتكررة

**س: هل يمكن إخفاء عدة صفحات في آن واحد؟**  
ج: نعم. عدّل معلمات `PageRangeFilter` لتشمل أي نطاق (مثال: `new PageRangeFilter(1, 5)` للصفحات 1‑5).

**س: هل تدعم المكتبة ملفات PDF محمية بكلمة مرور؟**  
ج: بالتأكيد. مرّر كلمة المرور إلى مُنشئ `Redactor` لفتح الملفات المشفرة.

**س: كيف يمكن تغيير لون الإخفاء أو الطبقة العلوية؟**  
ج: استخدم `ReplacementOptions` لتحديد صورة مخصصة أو لون أو نص كطبقة علوية.

**س: هل الإخفاء دائم؟**  
ج: نعم. المحتوى المُزال لا يُخزن في ملف PDF الناتج، مما يجعله غير قابل للاسترجاع.

**س: ماذا لو احتجت إلى إخفاء بناءً على أنماط regex؟**  
ج: يوفر GroupDocs.Redaction `RegexRedaction` الذي يعمل بطريقة مشابهة لـ `ExactPhraseRedaction`.

---

**آخر تحديث:** 2026-04-20  
**تم الاختبار مع:** GroupDocs.Redaction 24.9 للـ Java  
**المؤلف:** GroupDocs