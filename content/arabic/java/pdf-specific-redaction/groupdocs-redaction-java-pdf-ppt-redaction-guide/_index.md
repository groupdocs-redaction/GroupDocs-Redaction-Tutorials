---
date: '2026-07-01'
description: تعلم كيفية حذف النص من ملفات PDF و PowerPoint في Java باستخدام GroupDocs.Redaction.
  دليل خطوة بخطوة لتقنية حذف النص من PDF باستخدام Java، كيفية حذف النص من PPT، ومعالجة
  الدفعات.
keywords:
- how to redact pdf
- pdf redaction java
- how to redact ppt
- redact confidential data
- batch pdf redaction
schemas:
- author: GroupDocs
  dateModified: '2026-07-01'
  description: Learn how to redact PDF and PowerPoint files in Java using GroupDocs.Redaction.
    Step‑by‑step guide for pdf redaction java, how to redact ppt, and batch processing.
  headline: How to Redact PDF and PPT Text with GroupDocs for Java
  type: TechArticle
- description: Learn how to redact PDF and PowerPoint files in Java using GroupDocs.Redaction.
    Step‑by‑step guide for pdf redaction java, how to redact ppt, and batch processing.
  name: How to Redact PDF and PPT Text with GroupDocs for Java
  steps:
  - name: Configure Replacement Options
    text: '- **Text Redaction** – replace the matched word with a placeholder such
      as “█”. - **Image Redaction** – overlay a solid red rectangle on image areas
      to obscure visual data.'
  - name: Apply Redactions
    text: '`PageAreaRedaction` is an operation that applies redaction to specified
      page areas. Run the `PageAreaRedaction` operation to perform both text and image
      redactions in one pass:'
  - name: Cleanup Resources
    text: 'Always close the `Redactor` to free native resources and avoid memory leaks:'
  type: HowTo
- questions:
  - answer: Redaction permanently removes the data from the file structure, while
      hiding only changes the visual layer.
    question: What is the difference between pdf text redaction and simply hiding
      text?
  - answer: Yes – provide the password when constructing the `Redactor` instance.
    question: Can I use GroupDocs.Redaction to redact password‑protected PDFs?
  - answer: Use `redactor.save("output.pdf")` to a temporary location and open the
      file for review.
    question: Is there a way to preview redaction results before saving?
  - answer: Absolutely – the same API works across 20+ supported document types.
    question: Does the library support other formats like DOCX or XLSX?
  - answer: Visit the community forum at [GroupDocs Free Support](https://forum.groupdocs.com/c/redaction/33)
      for assistance.
    question: Where can I get help if I run into problems?
  type: FAQPage
title: كيفية حذف النص من ملفات PDF و PPT باستخدام GroupDocs للـ Java
type: docs
url: /ar/java/pdf-specific-redaction/groupdocs-redaction-java-pdf-ppt-redaction-guide/
weight: 1
---

# كيفية إخفاء نص PDF و PPT باستخدام GroupDocs للـ Java

في عالمنا الرقمي سريع الحركة اليوم، **how to redact pdf** ملفات هي خطوة لا يمكن التفاوض عليها لحماية البيانات السرية. سواء كنت تتعامل مع عقد قانوني، أو بيان مالي، أو عرض PowerPoint للشركة، فأنت بحاجة إلى طريقة موثوقة لإخفاء المعلومات الحساسة قبل المشاركة. يوضح هذا الدليل كيفية استخدام **GroupDocs.Redaction for Java** لإخفاء النصوص والصور في الصفحة أو الشريحة الأخيرة من ملفات PDF و PPT، ويظهر لك كيفية توسيع العملية لتشغيل دفعات متعددة.

## إجابات سريعة
- **What is pdf text redaction?** إنه يزيل أو يغطي النصوص والصور السرية بشكل دائم بحيث لا يمكن استعادتها.  
- **Which library supports this in Java?** توفر GroupDocs.Redaction for Java واجهة برمجة تطبيقات موحدة لـ PDF و PPT و DOCX و XLSX وأكثر.  
- **Do I need a license?** نسخة تجريبية مجانية للتقييم؛ يتطلب الاستخدام في الإنتاج ترخيصًا كاملاً.  
- **Can I redact both PDF and PPT with the same code?** نعم – تتعامل فئة `Redactor` نفسها مع كلا الصيغتين.  
- **What Java version is required?** JDK 8 أو أعلى.

## ما هو إخفاء نص PDF
**PDF text redaction permanently deletes or obscures selected content in a PDF document so it cannot be recovered or viewed.** على عكس الإخفاء البسيط، يزيل الإخفاء البيانات من بنية الملف، مما يضمن الامتثال للوائح الخصوصية مثل GDPR و HIPAA.

## لماذا تستخدم GroupDocs.Redaction للـ Java؟
تدعم GroupDocs.Redaction **20+ input and output formats** – بما في ذلك PDF و PPT و DOCX و XLSX وأنواع الصور الشائعة – ويمكنها معالجة مستندات مئات الصفحات دون تحميل الملف بالكامل في الذاكرة. توفر الواجهة تحكمًا دقيقًا في المناطق، ومحرك regex مدمج لاكتشاف العبارات تلقائيًا، وتصميمًا آمنًا للخطوط يتيح تشغيل دفعات على خوادم متعددة النوى.

## المتطلبات المسبقة
- **GroupDocs.Redaction for Java** (متاح عبر Maven أو تحميل مباشر).  
- **JDK 8+** مثبت ومُعد على جهاز التطوير الخاص بك.  
- **Maven** (أو القدرة على إضافة ملفات JAR يدويًا إلى classpath).  
- إلمام أساسي بـ Java I/O والتعابير النمطية.

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

### تحميل مباشر
إذا كنت تفضل عدم استخدام Maven، احصل على أحدث JAR من [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### الحصول على الترخيص
- **Free Trial** – استكشاف الميزات الأساسية دون تكلفة.  
- **Temporary License** – تمديد الاختبار بعد فترة التجربة.  
- **Full License** – مطلوب للنشر التجاري.

### التهيئة الأساسية
`Redactor` هي الفئة الأساسية التي تمثل مستندًا وتوفر جميع عمليات الإخفاء. أنشئ مثيل `Redactor` يشير إلى المستند الذي تريد معالجته:

```java
import com.groupdocs.redaction.Redactor;
// Initialize the Redactor object
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/YOUR_FILE.pdf");
```

## دليل التنفيذ
### كيفية إخفاء مستندات PDF Java باستخدام GroupDocs.Redaction؟
حمّل ملف PDF، عرّف نمط regex، اضبط خيارات الاستبدال، وطبق الإخفاء في سير عمل واحد متسلسل. يتيح لك هذا النهج إخفاء النص في النصف الأيمن من الصفحة الأخيرة وتغطية أي صور مكتشفة بمستطيل صلب.

#### الخطوة 1: تحميل المستند
```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/LOREMIPSUM_PDF");
```

#### الخطوة 2: تعريف نمط Regex لمطابقة النص
```java
// Compile regex pattern to match specific text
java.util.regex.Pattern rx = java.util.regex.Pattern.compile("urna");
```

#### الخطوة 3: تكوين خيارات الاستبدال
- **Text Redaction** – استبدال الكلمة المطابقة ببديل مثل “█”.  
- **Image Redaction** – تغطية منطقة الصورة بمستطيل أحمر صلب لإخفاء البيانات البصرية.

```java
ReplacementOptions optionsText = new ReplacementOptions("[redarea]");
optionsText.setFilters(new RedactionFilter[] {
    new PageRangeFilter(PageSeekOrigin.End, 0, 1), // Target the last page
    new PageAreaFilter(new java.awt.Point(300, 0), new java.awt.Dimension(300, 840)) // Right half of the page
});
```

```java
RegionReplacementOptions optionsImg = new RegionReplacementOptions(java.awt.Color.RED, new java.awt.Dimension(100, 100));
```

#### الخطوة 4: تطبيق الإخفاءات
`PageAreaRedaction` هي عملية تطبق الإخفاء على مناطق صفحات محددة.  
قم بتشغيل عملية `PageAreaRedaction` لتنفيذ كل من إخفاءات النص والصورة في خطوة واحدة:

```java
RedactorChangeLog result = redactor.apply(new PageAreaRedaction(rx, optionsText, optionsImg));

if (result.getStatus() != RedactionStatus.Failed) {
    redactor.save("YOUR_OUTPUT_DIRECTORY/output.pdf");
}
```

#### الخطوة 5: تنظيف الموارد
دائمًا أغلق كائن `Redactor` لتحرير الموارد الأصلية وتجنب تسرب الذاكرة:

```java
finally {
    redactor.close();
}
```

### كيفية إخفاء شرائح PPT باستخدام نفس النهج؟
يتطابق سير العمل مع خطوات PDF؛ فقط يتغير امتداد الملف. حمّل ملف PPTX، طبّق نفس regex ومرشحات المناطق، ثم احفظ العرض المجهول.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/LOREMIPSUM_PPT");
```

## التطبيقات العملية
- **Legal Document Preparation** – إخفاء أسماء العملاء، أرقام القضايا، أو البنود السرية قبل تقديمها للمحاكم.  
- **Financial Reporting** – إخفاء أرقام الحسابات، هوامش الأرباح، أو الصيغ المملوكة في ملفات PDF والعروض.  
- **HR Audits** – إزالة معرفات الموظفين من تصديرات المستندات الجماعية للامتثال لقوانين الخصوصية.

## اعتبارات الأداء
- **Close resources promptly** للحفاظ على انخفاض استهلاك الذاكرة، خاصة عند معالجة دفعات كبيرة.  
- **Optimize regex patterns** – تجنّب التعبيرات العامة الواسعة التي تفحص المستند بأكمله دون حاجة.  
- **Batch processing** – استخدم مجموعة من الخيوط وأعد استخدام مثيل `Redactor` واحد لكل ملف لتحسين الإنتاجية على الخوادم متعددة النوى.

## المشكلات الشائعة والحلول
| المشكلة | السبب | الحل |
|-------|-------|-----|
| *Redaction not applied* | Filters target the wrong page/area | Verify `PageRangeFilter` and `PageAreaFilter` coordinates. |
| *OutOfMemoryError* | Large files kept open | Process files sequentially or increase JVM heap (`-Xmx`). |
| *Regex matches unwanted text* | Pattern too generic | Refine the regex or use word boundaries (`\b`). |

## الأسئلة المتكررة

**س: ما الفرق بين إخفاء نص PDF وإخفاء النص ببساطة؟**  
ج: الإخفاء يزيل البيانات من بنية الملف بشكل دائم، بينما الإخفاء البسيط يغيّر الطبقة البصرية فقط.

**س: هل يمكنني استخدام GroupDocs.Redaction لإخفاء ملفات PDF محمية بكلمة مرور؟**  
ج: نعم – قدم كلمة المرور عند إنشاء مثيل `Redactor`.

**س: هل هناك طريقة لمعاينة نتائج الإخفاء قبل الحفظ؟**  
ج: استخدم `redactor.save("output.pdf")` إلى موقع مؤقت وافتح الملف للمراجعة.

**س: هل تدعم المكتبة صيغًا أخرى مثل DOCX أو XLSX؟**  
ج: بالتأكيد – تعمل الواجهة نفسها عبر أكثر من 20 نوع مستند مدعوم.

**س: أين يمكنني الحصول على المساعدة إذا واجهت مشاكل؟**  
ج: زر منتدى المجتمع على [GroupDocs Free Support](https://forum.groupdocs.com/c/redaction/33) للحصول على المساعدة.

**آخر تحديث:** 2026-07-01  
**تم الاختبار مع:** GroupDocs.Redaction 24.9 للـ Java  
**المؤلف:** GroupDocs

## دروس ذات صلة

- [How to Redact Text in Java with GroupDocs.Redaction: A Complete Guide](/redaction/java/text-redaction/master-text-redaction-java-groupdocs-redaction-guide/)
- [how redact pdf java – PDF-Specific Redaction Tutorials for GroupDocs.Redaction](/redaction/java/pdf-specific-redaction/)
- [Mask Sensitive Data Java – Redact Personal Info with GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)