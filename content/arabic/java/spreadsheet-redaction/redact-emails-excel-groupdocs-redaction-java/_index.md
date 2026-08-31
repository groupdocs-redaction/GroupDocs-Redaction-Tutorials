---
date: '2026-02-24'
description: تعلم كيفية إخفاء البيانات الحساسة وتغطية عناوين البريد الإلكتروني في
  جداول إكسل باستخدام واجهة برمجة تطبيقات GroupDocs.Redaction للغة Java.
keywords:
- Redact Emails in Excel
- GroupDocs.Redaction Java API
- Automate Email Redaction
title: كيفية إخفاء البيانات الحساسة في جداول إكسل باستخدام واجهة برمجة تطبيقات GroupDocs.Redaction
  للـ Java
type: docs
url: /ar/java/spreadsheet-redaction/redact-emails-excel-groupdocs-redaction-java/
weight: 1
---

# كيفية إخفاء البيانات الحساسة في جداول إكسل باستخدام GroupDocs.Redaction Java API

في عالم اليوم القائم على البيانات، **إخفاء البيانات الحساسة** مثل عناوين البريد الإلكتروني من دفاتر إكسل مهارة أساسية لأي شخص يتعامل مع المعلومات الشخصية. سواء كنت تُعد تقريرًا لعميل، أو تشارك البيانات مع شريك، أو تقوم ببساطة بتنظيف مجموعة بيانات، فإن إخفاء عناوين البريد الإلكتروني يساعدك على الالتزام بـ GDPR و CCPA وغيرها من اللوائح المتعلقة بالخصوصية. في هذا الدرس ستتعلم كيفية استخدام مكتبة GroupDocs.Redaction Java لتحديد واستبدال قيم البريد الإلكتروني تلقائيًا في عمود معين من ملف إكسل.

**ما ستتعلمه**
- كيفية إعداد GroupDocs.Redaction لـ Java في مشروع Maven.  
- تقنيات استهداف ورقة عمل وعمود معين.  
- كيفية **إخفاء عناوين البريد الإلكتروني** باستخدام نمط تعبير منتظم.  
- أفضل الممارسات لحفظ الملف المُخفى مع الحفاظ على الأصل سليمًا.

دعنا نتأكد من أن بيئة التطوير جاهزة قبل الغوص في الشيفرة.

## إجابات سريعة
- **ماذا يعني “إخفاء البيانات الحساسة”؟** يعني إزالة أو إخفاء المعلومات الشخصية القابلة للتعريف (PII) من المستند بشكل دائم.  
- **أي مكتبة تتعامل مع الإخفاء؟** GroupDocs.Redaction for Java.  
- **هل أحتاج إلى ترخيص؟** نسخة تجريبية مجانية تكفي للاختبار؛ الترخيص الدائم مطلوب للإنتاج.  
- **هل يمكنني اختيار نص الاستبدال؟** نعم، يمكنك تحديد أي عنصر نائب، مثل “[customer email]”.  
- **هل هذه الطريقة آمنة لجداول إكسل الكبيرة؟** نعم، عندما تتبع نصائح الأداء الموجودة في الدليل.

## المتطلبات المسبقة

للمتابعة، ستحتاج إلى:
- Java Development Kit (JDK) 8 أو أعلى.  
- معرفة أساسية بـ Java وإلمام بـ Maven.  
- الوصول إلى مكتبة GroupDocs.Redaction (قابلة للتنزيل عبر Maven أو الرابط المباشر).

## إعداد GroupDocs.Redaction لـ Java

يتم توزيع GroupDocs.Redaction لـ Java عبر مستودع Maven، مما يجعل التكامل سهلًا.

**إعداد Maven**  
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

**تحميل مباشر**  
بدلاً من ذلك، يمكنك تنزيل أحدث نسخة من GroupDocs.Redaction لـ Java من [GroupDocs.Redaction releases](https://releases.groupdocs.com/redaction/java/).

### الحصول على الترخيص

تقدم GroupDocs نسخة تجريبية مجانية تتيح لك تقييم الـ API. للمشاريع المستمرة، ستحتاج إما إلى ترخيص مؤقت أو ترخيص كامل:
- **نسخة تجريبية مجانية:** تقييم بميزات محدودة.  
- **ترخيص مؤقت:** قدم طلبًا على [موقع GroupDocs](https://purchase.groupdocs.com/temporary-license/).  
- **ترخيص كامل:** اشترِ لاستخدام غير مقيد في الإنتاج.

### التهيئة الأساسية

ابدأ بإنشاء كائن `Redactor` يشير إلى ملف إكسل الخاص بك:

```java
import com.groupdocs.redaction.Redactor;

public class RedactEmails {
    public static void main(String[] args) {
        // Initialize the redactor with your document path
        try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_XLSX")) {
            // Your redaction logic will go here
        }
    }
}
```

## دليل التنفيذ

فيما يلي دليل خطوة بخطوة يوضح كيفية **إخفاء البيانات الحساسة** من عمود معين.

### تحميل المستند

أولاً، افتح دفتر العمل باستخدام `Redactor` الذي أنشأته للتو:

```java
import com.groupdocs.redaction.Redactor;

public class RedactEmails {
    public static void main(String[] args) {
        try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_XLSX")) {
            // Proceed to the next steps for redaction
        }
    }
}
```

### إعداد مرشح

`CellFilter` يتيح لك تضييق نطاق الإخفاء إلى ورقة عمل وعمود معين. في هذا المثال نستهدف العمود B (الفهرس 1) في ورقة **Customers**:

```java
import com.groupdocs.redaction.redactions.CellFilter;

// Create and configure the filter
CellFilter filter = new CellFilter();
filter.setColumnIndex(1); // Targeting the second column (index starts at 0)
filter.setWorkSheetName("Customers"); // Specify the worksheet name
```

### تعريف نمط البريد الإلكتروني

يُستخدم تعبير منتظم لاكتشاف عناوين البريد الإلكتروني. النمط أدناه يطابق معظم صيغ البريد الشائعة:

```java
import java.util.regex.Pattern;

// Define regex pattern for matching emails
Pattern expression = Pattern.compile("^\\w+([-+.']\\w+)*@\\w+([-.]\\w+)*\\.\\w+([-.]\\w+)*$");
```

### تطبيق الإخفاء

الآن اجمع بين المرشح والنمط وخيار الاستبدال لـ **إخفاء عناوين البريد الإلكتروني**. كائن `ReplacementOptions` يتيح لك تحديد نص العنصر النائب الذي سيظهر في الخلايا المُخفية.

```java
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.RedactorChangeLog;
import com.groupdocs.redaction.redactions.CellColumnRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

// Apply redaction
RedactorChangeLog result = redactor.apply(new CellColumnRedaction(filter, expression, new ReplacementOptions("[customer email]")));

// Save changes if successful
if (result.getStatus() != RedactionStatus.Failed) {
    SaveOptions saveOptions = new SaveOptions();
    saveOptions.setAddSuffix(true); // Add a suffix to the saved file name
    redactor.save(saveOptions);
}
```

### نصائح استكشاف الأخطاء وإصلاحها
- **دقة التعبير المنتظم:** اختبر التعبير المنتظم الخاص بك ضد مجموعة متنوعة من عينات البريد الإلكتروني لضمان أنه يلتقط جميع الصيغ التي تتوقعها.  
- **فهرس العمود:** تذكر أن فهرسة الأعمدة تبدأ من 0؛ تحقق مرة أخرى من الفهرس للعمود الذي تنوي إخفاءه.  
- **اسم ورقة العمل:** الاسم حساس لحالة الأحرف؛ استخدم الاسم الدقيق للورقة كما يظهر في إكسل.

## لماذا إخفاء البيانات الحساسة؟

- **الامتثال:** الالتزام بـ GDPR و CCPA ومتطلبات الخصوصية الخاصة بالصناعة.  
- **تقليل المخاطر:** منع الكشف غير المقصود عن المعرفات الشخصية عند مشاركة الملفات خارجيًا.  
- **حوكمة البيانات:** الحفاظ على سجل تدقيق نظيف عن طريق إزالة PII بشكل دائم من مجموعات البيانات المؤرشفة.

## تطبيقات عملية

1. **الامتثال لخصوصية البيانات:** إزالة عناوين البريد الإلكتروني تلقائيًا قبل إرسال جداول إكسل إلى الشركاء.  
2. **التدقيق الداخلي:** إخفاء هوية بيانات العملاء أثناء المراجعات الداخلية.  
3. **خطوط تقارير:** دمج خطوة الإخفاء في وظائف إنشاء التقارير المجدولة.

## اعتبارات الأداء

- **المعالجة الدفعية:** إذا كنت بحاجة إلى إخفاء العديد من الملفات، عالجها تسلسليًا وأعد استخدام كائن `Redactor` حيثما أمكن.  
- **إدارة الذاكرة:** أغلق `Redactor` باستخدام كتلة try‑with‑resources (كما هو موضح) لتحرير الموارد الأصلية بسرعة.  
- **مجموعات البيانات الكبيرة:** بالنسبة لدفاتر العمل التي تحتوي على آلاف الصفوف، فكر في تصفية الصفوف قبل الإخفاء لتقليل الحمل.

## الأسئلة المتكررة

**س: ماذا لو لم يتطابق تعبير البريد الإلكتروني مع جميع الصيغ؟**  
ج: عدّل النمط لتضمين أحرف إضافية أو استخدم تعبيرًا أكثر تساهلاً، ثم أعد تشغيل الإخفاء.

**س: هل يمكنني إخفاء أعمدة متعددة في آن واحد؟**  
ج: نعم. أنشئ `CellFilter` منفصل لكل عمود واستدعِ `redactor.apply` لكل مرشح.

**س: هل GroupDocs.Redaction مناسب لملفات إكسل الكبيرة جدًا؟**  
ج: نعم، فهو يتعامل مع الحجم بشكل جيد، خاصةً عندما تعالج الأوراق واحدة تلو الأخرى وتحرر الموارد بعد كل ملف.

**س: كيف أتعامل مع الأخطاء أثناء الإخفاء؟**  
ج: تحقق من حالة `RedactorChangeLog`؛ الحالة غير الفاشلة تعني أن العملية نجحت. سجّل أي فشل للتصحيح.

**س: هل يمكنني تخصيص نص الاستبدال؟**  
ج: بالطبع. مرّر أي سلسلة نصية إلى `ReplacementOptions`، مثل “[redacted]” أو رمز مُولد.

## الموارد

- [الوثائق](https://docs.groupdocs.com/redaction/java/)
- [مرجع API](https://reference.groupdocs.com/redaction/java)
- [تحميل GroupDocs.Redaction](https://releases.groupdocs.com/redaction/java/)
- [مستودع GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
- [منتدى الدعم المجاني](https://forum.groupdocs.com/c/redaction/33)
- [معلومات الترخيص المؤقت](https://purchase.groupdocs.com/temporary-license/)

---

**آخر تحديث:** 2026-02-24  
**تم الاختبار مع:** GroupDocs.Redaction 24.9 for Java  
**المؤلف:** GroupDocs