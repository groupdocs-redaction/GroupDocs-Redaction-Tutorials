---
date: '2026-06-01'
description: تعلم كيفية حذف الصفحة الأخيرة من ملف PDF باستخدام GroupDocs.Redaction
  لـ Java. دليل خطوة بخطوة، مقتطفات كود، وأفضل الممارسات لـ pdf page count java وإزالة
  الصفحة الأخيرة من PDF.
keywords:
- delete last pdf page
- pdf page count java
- remove final pdf page
schemas:
- author: GroupDocs
  dateModified: '2026-06-01'
  description: Learn how to delete the last PDF page with GroupDocs.Redaction for
    Java. Step‑by‑step guide, code snippets, and best practices for pdf page count
    java and remove final pdf page.
  headline: How to Delete the Last PDF Page Using GroupDocs.Redaction in Java
  type: TechArticle
- description: Learn how to delete the last PDF page with GroupDocs.Redaction for
    Java. Step‑by‑step guide, code snippets, and best practices for pdf page count
    java and remove final pdf page.
  name: How to Delete the Last PDF Page Using GroupDocs.Redaction in Java
  steps:
  - name: '**Maven Setup**'
    text: '**Maven Setup**'
  - name: '**Direct Download**'
    text: '**Direct Download**'
  - name: '**Maven Configuration**'
    text: '**Maven Configuration**'
  - name: '**Direct Download Setup**'
    text: '**Direct Download Setup**'
  - name: '**Pre‑Publication Editing** – Remove draft or placeholder pages before
      releasing a report.'
    text: '**Pre‑Publication Editing** – Remove draft or placeholder pages before
      releasing a report.'
  - name: '**Archival Optimization** – Trim trailing blank pages to reduce storage
      costs for large document archives.'
    text: '**Archival Optimization** – Trim trailing blank pages to reduce storage
      costs for large document archives.'
  - name: '**Confidentiality** – Strip out a cover page that contains sensitive metadata
      before distribution.'
    text: '**Confidentiality** – Strip out a cover page that contains sensitive metadata
      before distribution.'
  - name: '**Automated Report Generation** – Generate PDFs programmatically and drop
      the automatically added summary page.'
    text: '**Automated Report Generation** – Generate PDFs programmatically and drop
      the automatically added summary page.'
  - name: '**Workflow Integration** – Embed the deletion step into CI/CD pipelines
      that handle document generation.'
    text: '**Workflow Integration** – Embed the deletion step into CI/CD pipelines
      that handle document generation.'
  type: HowTo
- questions:
  - answer: It provides a programmatic way to redact, edit, and manipulate sensitive
      content in PDFs and many other document formats without needing Microsoft Office
      installed.
    question: What is the primary use case for GroupDocs.Redaction?
  - answer: Yes—use `RemovePageRedaction` with a range (e.g., `new RemovePageRedaction(5,
      2)`) to delete two pages starting from page 5.
    question: Can I delete multiple pages at once?
  - answer: Absolutely. Pass the password to the `Redactor` constructor or set it
      via `redactor.setPassword("yourPassword")` before performing any operations.
    question: Does the library support password‑protected PDFs?
  - answer: It streams pages, allowing you to process PDFs with hundreds of pages
      while keeping memory usage low; typical processing of a 500‑page file uses under
      200 MB of RAM.
    question: How does GroupDocs.Redaction handle large files?
  - answer: Visit the [GroupDocs website](https://purchase.groupdocs.com/temporary-license/)
      to request a trial license that unlocks all API features for 30 days.
    question: Where can I obtain a temporary license for testing?
  type: FAQPage
title: كيفية حذف الصفحة الأخيرة من ملف PDF باستخدام GroupDocs.Redaction في Java
type: docs
url: /ar/java/page-redaction/remove-last-page-pdf-groupdocs-redaction-java/
weight: 1
---

# كيفية حذف الصفحة الأخيرة من PDF باستخدام GroupDocs.Redaction في Java

إزالة **الصفحة الأخيرة من PDF** غير المرغوب فيها من مستند PDF يمكن أن تكون عملية يدوية مرهقة، خاصةً عندما تحتاج إلى معالجة العشرات من الملفات في خط أنابيب آلي. باستخدام **GroupDocs.Redaction for Java**، يمكنك حذف الصفحة الأخيرة من PDF ببضع أسطر من الشيفرة فقط، مع الحفاظ على باقي المستند كما هو، والحفاظ على قابلية التحرير عند الحاجة. يشرح هذا الدليل كل ما تحتاجه—لماذا هذه العملية مهمة، واستدعاءات API الدقيقة، ونصائح عملية لتجنب الأخطاء الشائعة.

## إجابات سريعة
- **ما المكتبة التي يمكنها حذف الصفحة الأخيرة من PDF؟** GroupDocs.Redaction for Java.  
- **هل أحتاج إلى ترخيص؟** الإصدار التجريبي يعمل للاختبارات الأساسية؛ الترخيص الكامل مطلوب للإنتاج.  
- **هل يمكنني التحقق من عدد صفحات PDF قبل الإزالة؟** نعم—استخدم `redactor.getDocumentInfo().getPageCount()`.  
- **هل يظل PDF الأصلي قابلاً للتحرير بعد الإزالة؟** اضبط `saveOptions.setRasterizeToPDF(false)` للحفاظ على قابلية التحرير.  
- **ما نسخة Java المدعومة؟** JDK 8 أو أحدث.

## ما معنى “حذف الصفحة الأخيرة من PDF”؟
*حذف الصفحة الأخيرة من PDF* يعني إزالة الصفحة النهائية من ملف PDF برمجيًا مع الحفاظ على المحتوى المتبقي والبيانات الوصفية وإمكانية التحرير الاختيارية. هذه العملية مفيدة عندما تحتوي الصفحة الأخيرة على ملاحظات مسودة أو عنصر نائب أو معلومات سرية لا ينبغي أن تكون جزءًا من النسخة النهائية. بإزالتها برمجيًا تتجنب الأخطاء اليدوية، وتسرّع المعالجة الدفعية، وتحافظ على حجم الملف مثاليًا للتخزين والنقل.

## لماذا تستخدم GroupDocs.Redaction لهذه المهمة؟
يدعم GroupDocs.Redaction **أكثر من 50 تنسيقًا للمدخلات والمخرجات**، ويمكنه معالجة **ملفات PDF متعددة المئات من الصفحات** دون تحميل الملف بالكامل في الذاكرة، ويوفر API مخصصًا `RemovePageRedaction` يضمن إزالة دقيقة للصفحات مع فحوصات أمان مدمجة. بالإضافة إلى ذلك، توفر المكتبة ترخيصًا قويًا، وثائقًا شاملة، وإمكانية الحفاظ على قابلية البحث والتحرير في ملفات PDF بعد الإزالة، مما يجعلها خيارًا موثوقًا لأنابيب المستندات على مستوى المؤسسات.

## المتطلبات المسبقة
قبل البدء، تأكد من وجود ما يلي:

- **Java Development Kit (JDK) 8 أو أحدث** مثبت على جهازك.  
- **Maven** (أو القدرة على إضافة ملفات JAR يدويًا) لإدارة التبعيات.  
- **ترخيص GroupDocs.Redaction** (الإصدار التجريبي يكفي للتجربة).  
- إلمام أساسي بصياغة Java وبنية المشروع.

### المكتبات والاعتمادات المطلوبة
1. **إعداد Maven**  
   - تأكد من تثبيت Maven على جهازك.  
   - أضف التكوين التالي في ملف `pom.xml` الخاص بك لتضمين GroupDocs.Redaction:

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

للاطلاع على تفاصيل استخدام API، راجع [GroupDocs Redaction Java Documentation](https://docs.groupdocs.com/redaction/java/) و[GroupDocs API Reference](https://reference.groupdocs.com/redaction/java). تحقق من [Latest Releases](https://releases.groupdocs.com/redaction/java/) للحصول على إصدارات أحدث.

2. **تحميل مباشر**  
   - بدلاً من ذلك، قم بتحميل أحدث نسخة من [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).  
   - يمكنك أيضًا عرض الشيفرة المصدرية على [GroupDocs Redaction for Java](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java) وطرح الأسئلة في [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33).

### متطلبات إعداد البيئة
- تحقق من أن `JAVA_HOME` يشير إلى تثبيت JDK 8+.
- يجب أن يكون IDE الخاص بك (IntelliJ، Eclipse، VS Code) مُعدًا لاستخدام نفس نسخة JDK.

### المتطلبات المعرفية
- مفاهيم برمجة Java الأساسية (الفئات، الكائنات، معالجة الاستثناءات).  
- فهم `pom.xml` الخاص بـ Maven مفيد لكنه ليس إلزاميًا إذا كنت تفضل طريقة JAR المباشرة.

## إعداد GroupDocs.Redaction للغة Java
يتضمن إعداد مشروعك لاستخدام GroupDocs.Redaction إضافة المكتبة وتكوين الترخيص.

### معلومات التثبيت
1. **تكوين Maven**  
   - أضف المستودع ومقتطف الاعتماد من القسم السابق إلى ملف `pom.xml` الخاص بك.

2. **إعداد التحميل المباشر**  
   - قم بتحميل ملف JAR من [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).  
   - أضف ملف JAR إلى مسار بناء مشروعك (مثلاً، مجلد `libs/`).

### الحصول على الترخيص
- تقدم GroupDocs نسخة تجريبية مجانية بوظائف محدودة.  
- احصل على ترخيص مؤقت أو اشترِ ترخيصًا كاملاً من [موقع GroupDocs](https://purchase.groupdocs.com/temporary-license/).  
- للحصول على تفاصيل الترخيص راجع [صفحة ترخيص GroupDocs](https://purchase.groupdocs.com/temporary-license/) أو مباشرة [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license/).

## دليل التنفيذ
الآن بعد أن كل شيء جاهز، دعنا ننفذ الميزة **لحذف الصفحة الأخيرة من PDF** باستخدام GroupDocs.Redaction.

### كيف أحذف الصفحة الأخيرة من PDF باستخدام GroupDocs.Redaction؟
قم بتحميل PDF باستخدام كائن `Redactor`، تحقق من أن المستند يحتوي على صفحة واحدة على الأقل، طبّق `RemovePageRedaction` المستهدف للصفحة النهائية، اضبط `SaveOptions`، وأخيرًا احفظ الملف المعدل. يمكن إنجاز هذا التدفق بالكامل بأقل من عشر أسطر من شيفرة Java.

#### تنفيذ خطوة بخطوة

##### **الخطوة 1: تهيئة Redactor**
`Redactor` هو الفئة الأساسية التي تمثل مستند PDF وتوفر طرقًا للإزالة وتلاعب الصفحات.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/multipage.pdf");
```

هذا السطر يفتح ملف PDF ويجهزه للعمليات اللاحقة.

##### **الخطوة 2: التحقق من عدد صفحات PDF**
`DocumentInfo.getPageCount()` يُعيد العدد الكلي للصفحات، مما يتيح لك التحقق بأمان من وجود صفحة أخيرة قبل محاولة الإزالة.

```java
if (redactor.getDocumentInfo().getPageCount() >= 1) {
    // Proceed with removal if true
}
```

إذا كان العدد صفرًا، يجب إلغاء العملية لتجنب حدوث `IndexOutOfBoundsException`.

##### **الخطوة 3: تطبيق RemovePageRedaction**
`RemovePageRedaction` هي فئة تزيل الصفحات بناءً على فهرس يبدأ من الصفر أو مرجع أصل.

```java
redactor.apply(new RemovePageRedaction(PageSeekOrigin.End, -1));
```

- `PageSeekOrigin.End` يحدد أن فهرس الصفحة يُحسب من نهاية المستند.  
- الإزاحة `-1` تزيل صفحة واحدة بالضبط — الصفحة النهائية.

##### **الخطوة 4: ضبط SaveOptions**
`SaveOptions` يتحكم في كيفية كتابة PDF المعدل إلى القرص ويسمح لك بالحفاظ على قابلية التحرير.

```java
SaveOptions saveOptions = new SaveOptions();
saveOptions.setAddSuffix(true); // Adds a suffix to the filename
saveOptions.setRasterizeToPDF(false); // Retains PDF editability
```

يمكنك أيضًا إضافة لاحقة إلى اسم ملف الإخراج (مثلاً، `_trimmed`) لتجنب الكتابة فوق الملف الأصلي.

##### **الخطوة 5: حفظ المستند المعدل**
احفظ التغييرات عن طريق استدعاء `redactor.save(outputPath, saveOptions)`. هذا يكتب PDF جديد لا يحتوي على الصفحة الأخيرة.

```java
redactor.save(saveOptions);
```

##### **الخطوة 6: إغلاق الموارد**
دائمًا أغلق كائن `Redactor` لتحرير الموارد الأصلية وتجنب تسرب الذاكرة.

```java
finally {
    redactor.close();
}
```

#### نصائح استكشاف الأخطاء وإصلاحها
- **مسار ملف غير صحيح** – تحقق مرة أخرى من أن مسار PDF المدخل هو مسار مطلق أو نسبي بشكل صحيح بالنسبة إلى دليل العمل الخاص بك.  
- **مستند بلا صفحات** – فحص عدد الصفحات يمنع حدوث خطأ وقت التشغيل؛ إذا أعاد `0`، سجّل تحذيرًا وتخطى خطوة الإزالة.  
- **أخطاء الترخيص** – تأكد من وضع ملف الترخيص في مسار الفئة (classpath) أو توفيره عبر `License.setLicense("path/to/license")`.

## تطبيقات عملية
حذف الصفحة النهائية مفيد في العديد من السيناريوهات الواقعية:

1. **تحرير ما قبل النشر** – إزالة صفحات المسودة أو العناصر النائبة قبل إصدار التقرير.  
2. **تحسين الأرشفة** – قص الصفحات الفارغة المتبقية لتقليل تكاليف التخزين لأرشيفات المستندات الكبيرة.  
3. **السرية** – إزالة صفحة الغلاف التي تحتوي على بيانات وصفية حساسة قبل التوزيع.  
4. **إنشاء تقارير آلية** – إنشاء ملفات PDF برمجيًا وإزالة صفحة الملخص التي تُضاف تلقائيًا.  
5. **تكامل سير العمل** – دمج خطوة الحذف في خطوط أنابيب CI/CD التي تتعامل مع إنشاء المستندات.

## اعتبارات الأداء
عند معالجة ملفات PDF الكبيرة باستخدام GroupDocs.Redaction، ضع هذه النصائح في الاعتبار:

- **إدارة الذاكرة** – أغلق `Redactor` بسرعة؛ المكتبة تبث الصفحات بدلاً من تحميل الملف بالكامل في الذاكرة.  
- **التصوير النقطي** – عطل التصوير النقطي (`setRasterizeToPDF(false)`) إذا كنت تحتاج إلى أن يبقى الناتج قابلًا للبحث والتحرير.  
- **ذاكرة JVM** – بالنسبة لملفات PDF التي تتجاوز 200 MB، خصص على الأقل **2 GB** من الذاكرة (`-Xmx2g`) لتجنب `OutOfMemoryError`.  
- **المعالجة الدفعية** – أعد استخدام كائن `Redactor` واحد لعدة ملفات عندما يكون ذلك ممكنًا لتقليل عبء التهيئة.  
- تحقق من [Latest Releases](https://releases.groupdocs.com/redaction/java/) للحصول على تحديثات متعلقة بالأداء.

## الخلاصة
الآن لديك حل كامل وجاهز للإنتاج **لحذف الصفحة الأخيرة من PDF** باستخدام GroupDocs.Redaction في Java. باتباع الخطوات السابقة، يمكنك دمج هذه القدرة في أي خدمة خلفية، أو مهمة دفعية، أو تطبيق سطح مكتب، مما يضمن ملفات PDF نظيفة ومُحسّنة الحجم في كل مرة.

بعد ذلك، استكشف ميزات الإزالة الأخرى مثل إزالة النصوص، وإزالة الصور، وتنقية البيانات الوصفية لبناء خط أنابيب خصوصية مستندات متكامل.

## الأسئلة المتكررة

**س: ما هو الاستخدام الأساسي لـ GroupDocs.Redaction؟**  
ج: يوفر طريقة برمجية لإزالة وتحرير ومعالجة المحتوى الحساس في ملفات PDF والعديد من صيغ المستندات الأخرى دون الحاجة إلى تثبيت Microsoft Office.

**س: هل يمكنني حذف عدة صفحات مرة واحدة؟**  
ج: نعم—استخدم `RemovePageRedaction` مع نطاق (مثلاً، `new RemovePageRedaction(5, 2)`) لحذف صفحتين بدءًا من الصفحة 5.

**س: هل تدعم المكتبة ملفات PDF المحمية بكلمة مرور؟**  
ج: بالتأكيد. مرّر كلمة المرور إلى مُنشئ `Redactor` أو اضبطها عبر `redactor.setPassword("yourPassword")` قبل تنفيذ أي عملية.

**س: كيف يتعامل GroupDocs.Redaction مع الملفات الكبيرة؟**  
ج: يقوم ببث الصفحات، مما يتيح لك معالجة ملفات PDF بمئات الصفحات مع الحفاظ على استهلاك منخفض للذاكرة؛ عادةً معالجة ملف مكوّن من 500 صفحة يستخدم أقل من 200 MB من RAM.

**س: من أين يمكنني الحصول على ترخيص مؤقت للاختبار؟**  
ج: زر [موقع GroupDocs](https://purchase.groupdocs.com/temporary-license/) لطلب ترخيص تجريبي يفتح جميع ميزات API لمدة 30 يومًا.

---
**آخر تحديث:** 2026-06-01  
**تم الاختبار مع:** GroupDocs.Redaction 24.9 for Java  
**المؤلف:** GroupDocs  

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

## دروس ذات صلة

- [حذف نطاق صفحات PDF في Java بفعالية باستخدام GroupDocs.Redaction](/redaction/java/page-redaction/java-pdf-page-range-deletion-groupdocs-redaction/)
- [كيفية معاينة الصفحة باستخدام GroupDocs.Redaction Java – دليل شامل](/redaction/java/document-loading/load-preview-document-pages-groupdocs-redaction-java/)
- [كيفية إخفاء مستندات PDF باستخدام GroupDocs.Redaction للغة Java - دليل خطوة بخطوة](/redaction/java/advanced-redaction/master-redaction-groupdocs-java-guide/)