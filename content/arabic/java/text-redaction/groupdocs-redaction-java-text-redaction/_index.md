---
date: '2026-08-14'
description: كيفية إخفاء النص في مستندات Java باستخدام GroupDocs.Redaction – إخفاء
  المعلومات الشخصية واستبدال النص الحساس بكفاءة.
keywords:
- how to redact text
- GroupDocs Redaction Java
- text redaction Java
- mask personal information
lastmod: '2026-08-14'
og_description: تتيح لك طريقة إخفاء النص باستخدام GroupDocs.Redaction لـ Java إخفاء
  البيانات الشخصية بشكل دائم واستبدال السلاسل الحساسة عبر PDFs و DOCX وغيرها، مما
  يضمن الامتثال لـ GDPR و HIPAA.
og_image_alt: 'Guide: redact text in Java using GroupDocs.Redaction library'
og_title: كيفية إخفاء النص باستخدام GroupDocs.Redaction لـ Java
schemas:
- author: GroupDocs
  dateModified: '2026-08-14'
  description: How to redact text in Java documents using GroupDocs.Redaction – mask
    personal information and replace sensitive text efficiently.
  headline: How to redact text with GroupDocs.Redaction for Java
  type: TechArticle
- description: How to redact text in Java documents using GroupDocs.Redaction – mask
    personal information and replace sensitive text efficiently.
  name: How to redact text with GroupDocs.Redaction for Java
  steps:
  - name: initialize the redactor
    text: '`Redactor` is the core class that loads a document, applies redaction rules,
      and writes the output.'
  - name: apply exact‑phrase redaction
    text: '`ExactPhraseRedaction` searches for an exact string match, while `ReplacementOptions`
      defines how the matched text should be replaced. - **Parameters:** - `"John
      Doe"` – the exact text to be redacted. - `ReplacementOptions("[personal]")`
      – the string that will replace the original content, effective'
  - name: save the redacted document
    text: '`Redactor.save` writes the modified document to a new file or overwrites
      the original, preserving the original format.'
  - name: clean up resources
    text: Always call `Redactor.close()` to release native resources and avoid memory
      leaks.
  type: HowTo
- questions:
  - answer: Yes, the library supports PDF, DOCX, XLSX, PPTX, and many other formats.
    question: Can I redact text from PDFs using GroupDocs.Redaction?
  - answer: No. Redactions permanently remove the original content, so keep a backup
      of the source file.
    question: Is a redaction reversible?
  - answer: Process them in chunks, use batch mode, and monitor memory usage with
      profiling tools.
    question: How do I handle very large documents efficiently?
  - answer: Besides DOCX and PDF, you can redact TXT, RTF, XLSX, PPTX, and more.
    question: What other text formats are supported?
  - answer: Absolutely. The API can be called from web services, background jobs,
      or CI/CD pipelines.
    question: Can I integrate GroupDocs.Redaction into existing workflows?
  type: FAQPage
tags:
- text redaction
- GroupDocs.Redaction
- Java document processing
- privacy compliance
- redaction API
title: كيفية إخفاء النص باستخدام GroupDocs.Redaction لـ Java
type: docs
url: /ar/java/text-redaction/groupdocs-redaction-java-text-redaction/
weight: 1
---

# كيفية حذف النص باستخدام GroupDocs.Redaction للـ Java

في هذا البرنامج التعليمي ستتعلم **كيفية حذف النص** في المستندات المعتمدة على Java باستخدام GroupDocs.Redaction. سترى كيفية إخفاء المعلومات الشخصية، واستبدال السلاسل الحساسة ببدائل آمنة، ومعالجة ملفات متعددة بطريقة صديقة للدفعات. في النهاية ستحصل على حل جاهز للإنتاج يحمي الخصوصية، ويلبي متطلبات GDPR/HIPAA، ويتكامل بسلاسة مع تطبيقات Java الحالية.

## إجابات سريعة
- **ما المكتبة المستخدمة؟** GroupDocs.Redaction for Java.  
- **هل يمكنني إخفاء المعلومات الشخصية؟** نعم – استخدم حذف العبارة الدقيقة مع خيارات الاستبدال.  
- **هل يتم دعم المعالجة الدفعية؟** بالتأكيد، يمكنك التكرار عبر ملفات متعددة باستخدام نفس كائن Redactor.  
- **هل أحتاج إلى ترخيص؟** تجربة مجانية تعمل للتقييم؛ يلزم ترخيص تجاري للإنتاج.  
- **ما نسخة Java المطلوبة؟** JDK 8 أو أعلى.

## ما هو “كيفية حذف النص”؟
الحذف الدائم يزيل أو يغطي البيانات السرية من المستند بشكل دائم. باستخدام GroupDocs.Redaction يمكنك تحديد سلاسل معينة، واستبدالها ببدائل آمنة، وحفظ الملف المنقّى — كل ذلك دون تحرير يدوي.

## لماذا تستخدم GroupDocs.Redaction للـ Java؟
GroupDocs.Redaction للـ Java يدعم **أكثر من 50 تنسيقًا للإدخال والإخراج** (بما في ذلك PDF، DOCX، XLSX، PPTX، TXT، RTF) ويمكنه معالجة ملفات مئات الصفحات دون تحميل المستند بالكامل في الذاكرة، مما يوفر عمليات دفعية عالية الإنتاجية على أجهزة الخادم القياسية.

## المتطلبات المسبقة
- **Java Development Kit (JDK):** الإصدار 8 أو أحدث.  
- **IDE:** IntelliJ IDEA، Eclipse، أو أي محرر متوافق مع Java.  
- **Maven:** لإدارة التبعيات.  
- **معرفة أساسية بـ Java:** الإلمام بالفئات، والطرق، ومعالجة الاستثناءات.

## إعداد GroupDocs.Redaction للـ Java
لبدء، أضف المكتبة إلى مشروع Maven الخاص بك.

### إعداد Maven
أضف المستودع والتبعيات إلى ملف `pom.xml` الخاص بك:

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
إذا كنت تفضل، احصل على أحدث JAR من [GroupDocs Redaction Java Docs](https://releases.groupdocs.com/redaction/java/).

### الحصول على الترخيص
يمكنك البدء بـ **Free Trial**، طلب **Temporary License** للاختبار الموسع، أو شراء **Commercial License** للاستخدام في الإنتاج.

## كيفية حذف النص في المستندات باستخدام GroupDocs.Redaction

الأقسام التالية ترشدك عبر الخطوات الدقيقة اللازمة **لإخفاء المعلومات الشخصية** و**استبدال النص الحسّاس**.

### الخطوة 1: تهيئة الـ Redactor
`Redactor` هو الفئة الأساسية التي تقوم بتحميل المستند، وتطبيق قواعد الحذف، وكتابة الناتج.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx", new LoadOptions());
```

### الخطوة 2: تطبيق حذف العبارة الدقيقة
`ExactPhraseRedaction` يبحث عن تطابق نصي دقيق، بينما `ReplacementOptions` يحدد كيفية استبدال النص المطابق.

```java
redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]"));
```
- **المعلمات:**  
  - `"John Doe"` – النص الدقيق الذي سيتم حذفه.  
  - `ReplacementOptions("[personal]")` – السلسلة التي ستحل محل المحتوى الأصلي، مما يؤدي فعليًا إلى **إخفاء المعلومات الشخصية**.

### الخطوة 3: حفظ المستند المحذوف
`Redactor.save` يكتب المستند المعدل إلى ملف جديد أو يستبدل الأصلي، مع الحفاظ على التنسيق الأصلي.

```java
redactor.save();
```

### الخطوة 4: تنظيف الموارد
دائمًا استدعِ `Redactor.close()` لتحرير الموارد الأصلية وتجنب تسرب الذاكرة.

```java
finally {
    redactor.close();
}
```

## كيفية إخفاء المعلومات الشخصية باستخدام رد نداء مخصص
يتيح لك رد النداء المخصص الاستجابة لكل حدث حذف — مفيد للتسجيل، والاستبدالات الشرطية، أو سجلات التدقيق.

### إنشاء فئة رد نداء
`IRedactionCallback` يحدد الطرق التي تُستدعى قبل وبعد كل عملية حذف.

```java
class RedactionDump implements IRedactionCallback {
    @Override
    public void onRedacted(IRedaction redaction) {
        // Custom processing or logging for each redaction event.
    }
}
```

### استخدام رد النداء عند إنشاء Redactor
مرّر تنفيذ رد النداء الخاص بك عبر `RedactorSettings` حتى يعرف المحرك استدعائه أثناء المعالجة.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx", new LoadOptions(), new RedactorSettings(new RedactionDump()));
```

## التطبيقات العملية
- **العقود القانونية:** إخفاء أسماء العملاء، أرقام الضمان الاجتماعي، أو البنود السرية تلقائيًا قبل مشاركة المسودات.  
- **السجلات الطبية:** **إخفاء المعلومات الشخصية** مثل معرفات المرضى عند تصدير السجلات إلى شركاء البحث.  
- **الاتصالات المؤسسية:** **استبدال النص الحسّاس** مثل رموز المشاريع الداخلية قبل التوزيع الخارجي، لضمان عدم حدوث تسريبات غير مقصودة.

## اعتبارات الأداء
عند معالجة ملفات كبيرة أو عديدة، احرص على مراعاة النصائح التالية:
- **المعالجة الدفعية:** التكرار عبر مجموعة من الملفات لتقليل عبء بدء التشغيل.  
- **إدارة الذاكرة:** تحرير `Redactor` بعد كل ملف؛ تجنّب الاحتفاظ بالعديد من المستندات في الذاكرة في آن واحد.  
- **التحليل (Profiling):** استخدم أدوات تحليل Java (مثل VisualVM) لتحديد نقاط الاختناق في عمليات الإدخال/الإخراج أو منطق الحذف.

## الأسئلة المتكررة
**س: هل يمكنني حذف النص من ملفات PDF باستخدام GroupDocs.Redaction؟**  
ج: نعم، المكتبة تدعم PDF، DOCX، XLSX، PPTX، والعديد من الصيغ الأخرى.

**س: هل يمكن عكس عملية الحذف؟**  
ج: لا. عمليات الحذف تزيل المحتوى الأصلي بشكل دائم، لذا احتفظ بنسخة احتياطية من الملف الأصلي.

**س: كيف يمكنني التعامل مع المستندات الكبيرة جدًا بكفاءة؟**  
ج: عالجها على أجزاء، استخدم الوضع الدفعي، وراقب استهلاك الذاكرة باستخدام أدوات التحليل.

**س: ما هي صيغ النص الأخرى المدعومة؟**  
ج: بالإضافة إلى DOCX و PDF، يمكنك حذف TXT، RTF، XLSX، PPTX، وأكثر.

**س: هل يمكنني دمج GroupDocs.Redaction في سير العمل الحالي؟**  
ج: بالتأكيد. يمكن استدعاء الـ API من خدمات الويب، أو الوظائف الخلفية، أو خطوط أنابيب CI/CD.

## الموارد
- **التوثيق:** [وثائق GroupDocs Redaction Java](https://docs.groupdocs.com/redaction/java/)  
- **مرجع API:** [مرجع GroupDocs API للـ Java](https://reference.groupdocs.com/redaction/java)  
- **تحميل:** [تنزيلات GroupDocs.Redaction](https://releases.groupdocs.com/redaction/java/)  
- **مستودع GitHub:** [GroupDocs Redaction على GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **منتدى الدعم المجاني:** [الدعم المجاني من GroupDocs](https://forum.groupdocs.com/c/redaction/33)  
- **طلب ترخيص مؤقت:** [التقدم بطلب للحصول على ترخيص مؤقت](https://purchase.groupdocs.com/temporary-license/)

---

**آخر تحديث:** 2026-08-14  
**تم الاختبار مع:** GroupDocs.Redaction 24.9 for Java  
**المؤلف:** GroupDocs

## الدروس ذات الصلة

- [إخفاء البيانات الحساسة Java – دليل GroupDocs.Redaction](/redaction/java/getting-started/)
- [إخفاء البيانات الحساسة Java – حذف المعلومات الشخصية باستخدام GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)
- [تحرير المستندات المحمية بكلمة مرور Java - حذف المستندات باستخدام GroupDocs.Redaction](/redaction/java/document-loading/groupdocs-redaction-java-password-documents/)