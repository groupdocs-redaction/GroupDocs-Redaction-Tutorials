---
date: '2026-08-09'
description: GroupDocs.Redaction Java API का उपयोग करके Excel स्प्रेडशीट्स में व्यक्तिगत
  डेटा को छुपाना और ईमेल पते को मास्क करना सीखें।
keywords:
- how to hide personal data
- mask email addresses excel
- GroupDocs.Redaction Java
- Excel redaction tutorial
lastmod: '2026-08-09'
og_description: GroupDocs.Redaction Java API का उपयोग करके Excel फ़ाइलों में व्यक्तिगत
  डेटा को छुपाने और ईमेल पते को मास्क करने के चरण‑दर‑चरण तरीके को जानें – GDPR अनुपालन
  के लिए एक तेज़, सुरक्षित समाधान।
og_image_alt: Guide showing Java code that redacts email addresses in an Excel spreadsheet
og_title: GroupDocs Java के साथ Excel में व्यक्तिगत डेटा को कैसे छुपाएँ
schemas:
- author: GroupDocs
  dateModified: '2026-08-09'
  description: Learn how to hide personal data and mask email addresses in Excel spreadsheets
    using the GroupDocs.Redaction Java API.
  headline: How to hide personal data in Excel with GroupDocs Java
  type: TechArticle
- description: Learn how to hide personal data and mask email addresses in Excel spreadsheets
    using the GroupDocs.Redaction Java API.
  name: How to hide personal data in Excel with GroupDocs Java
  steps:
  - name: '**Partner data exchange** – Automatically strip customer emails before
      sending spreadsheets to vendors.'
    text: '**Partner data exchange** – Automatically strip customer emails before
      sending spreadsheets to vendors.'
  - name: '**Internal audit preparation** – Anonymize employee data during compliance
      reviews.'
    text: '**Internal audit preparation** – Anonymize employee data during compliance
      reviews.'
  - name: '**Scheduled reporting** – Embed the redaction step into nightly batch jobs
      that generate distribution‑ready reports.'
    text: '**Scheduled reporting** – Embed the redaction step into nightly batch jobs
      that generate distribution‑ready reports.'
  type: HowTo
- questions:
  - answer: Extend the pattern to include additional allowed characters (e.g., “+”
      or “_”) and test against a larger sample set, then re‑run the redaction.
    question: My regex still misses some corporate email formats. What should I do?
  - answer: Yes. Create a separate `CellFilter` for each column and invoke `redactor.apply`
      for each filter sequentially.
    question: Can I redact more than one column in a single pass?
  - answer: The library processes sheets incrementally, so files up to several gigabytes
      can be redacted as long as you enable streaming and close the `Redactor` after
      each file.
    question: Is GroupDocs.Redaction able to handle Excel files larger than 1 GB?
  - answer: Inspect the `RedactorChangeLog` returned by `apply`; a non‑failed status
      indicates success, while any errors are listed with line numbers and cell references.
    question: How do I capture redaction results or errors?
  - answer: Absolutely. Build the placeholder string dynamically (e.g., `"[redacted:"
      + UUID.randomUUID() + "]"`) and pass it to `ReplacementOptions`.
    question: Can I use a custom placeholder that includes a unique token per row?
  type: FAQPage
tags:
- hide personal data
- GroupDocs.Redaction
- Java Excel processing
- data privacy
title: GroupDocs Java के साथ Excel में व्यक्तिगत डेटा को कैसे छुपाएँ
url: /hi/java/spreadsheet-redaction/redact-emails-excel-groupdocs-redaction-java/
weight: 1
---

# Excel में व्यक्तिगत डेटा को छिपाने के लिए GroupDocs Java के साथ कैसे करें

इस गाइड में आप सीखेंगे **व्यक्तिगत डेटा को कैसे छिपाएँ**—विशेष रूप से ईमेल पते—Excel वर्कबुक में GroupDocs.Redaction Java API का उपयोग करके। चाहे आपको GDPR, CCPA, या आंतरिक गोपनीयता नीतियों का पालन करना हो, यहाँ दिखाया गया तरीका आपको सुरक्षित रूप से रेडैक्शन को स्वचालित करने, मूल फ़ाइल को अपरिवर्तित रखने, और वितरण के लिए तैयार एक साफ़ संस्करण बनाने की अनुमति देता है।

## त्वरित उत्तर
- **“व्यक्तिगत डेटा को छिपाना” क्या मतलब है?** इसका अर्थ है फ़ाइल से व्यक्तिगत पहचान योग्य जानकारी (PII) को स्थायी रूप से मास्क या हटाना ताकि उसे अब पढ़ा न जा सके।  
- **कौन सी लाइब्रेरी रेडैक्शन करती है?** GroupDocs.Redaction for Java।  
- **क्या उदाहरण चलाने के लिए लाइसेंस चाहिए?** परीक्षण के लिए एक मुफ्त ट्रायल काम करता है; व्यावसायिक उपयोग के लिए प्रोडक्शन‑ग्रेड लाइसेंस आवश्यक है।  
- **क्या मैं प्लेसहोल्डर टेक्स्ट को कस्टमाइज़ कर सकता हूँ?** हाँ—आप ईमेल को किसी भी स्ट्रिंग जैसे “[redacted email]” से बदल सकते हैं।  
- **क्या यह विधि बड़े स्प्रेडशीट्स के लिए उपयुक्त है?** हाँ, जब आप “Performance considerations” सेक्शन में दिए गए प्रदर्शन सुझावों का पालन करते हैं।

## व्यक्तिगत डेटा को छिपाना क्या है?
**व्यक्तिगत डेटा को छिपाना** का अर्थ है किसी भी जानकारी को अपरिवर्तनीय रूप से हटाना या मास्क करना जो सीधे या अप्रत्यक्ष रूप से किसी व्यक्ति की पहचान कर सके, जैसे नाम, फोन नंबर, या ईमेल पते। यह प्रक्रिया सुनिश्चित करती है कि परिणामी फ़ाइल का उपयोग विषय की पुनः पहचान करने के लिए नहीं किया जा सके।

## GroupDocs.Redaction for Java का उपयोग क्यों करें?
GroupDocs.Redaction **30+ इनपुट और आउटपुट फॉर्मेट्स** का समर्थन करता है और **500,000 पंक्तियों** तक की वर्कबुक को पूरी फ़ाइल को मेमोरी में लोड किए बिना प्रोसेस कर सकता है, जिससे साधारण फ़ाइल‑पार्सिंग समाधान की तुलना में **80 % तक मेमोरी‑फुटप्रिंट में कमी** मिलती है। ये मापनीय लाभ इसे एंटरप्राइज़‑ग्रेड डेटा‑प्राइवेसी पाइपलाइन के लिए शीर्ष विकल्प बनाते हैं।

## पूर्वापेक्षाएँ
- Java Development Kit (JDK) 8 या उससे नया।  
- Maven बिल्ड फ़ाइलों की बुनियादी समझ।  
- GroupDocs.Redaction Java लाइब्रेरी तक पहुँच (Maven या आधिकारिक रिलीज़ पेज से डाउनलोड योग्य)。

## GroupDocs.Redaction for Java को सेट अप करना

### Maven प्रोजेक्ट में GroupDocs.Redaction कैसे जोड़ें?
अपने `pom.xml` फ़ाइल में GroupDocs रिपॉजिटरी और Redaction डिपेंडेंसी जोड़ें (देखें [GroupDocs.Redaction releases](https://releases.groupdocs.com/redaction/java/))। फिर आर्टिफैक्ट्स को प्राप्त करने के लिए `mvn clean install` चलाएँ।

```text
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
```

### GroupDocs.Redaction के लिए लाइसेंस कैसे प्राप्त करें?
GroupDocs तीन लाइसेंस विकल्प प्रदान करता है (देखें [GroupDocs’ website](https://purchase.groupdocs.com/temporary-license/))：

- **Free trial** – सीमित‑फ़ीचर मूल्यांकन, कोई क्रेडिट‑कार्ड आवश्यक नहीं।  
- **Temporary license** – GroupDocs वेबसाइट से प्राप्त 30‑दिन का मूल्यांकन कुंजी।  
- **Full license** – बिक्री पोर्टल के माध्यम से खरीदा गया स्थायी प्रोडक्शन लाइसेंस।

```text
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
```

## कार्यान्वयन गाइड

### Excel फ़ाइल के लिए Redactor इंस्टेंस कैसे बनाएं?
`Redactor` क्लास मुख्य एंट्री पॉइंट है जो दस्तावेज़ को लोड करता है और रेडैक्शन ऑपरेशन्स प्रदान करता है।  
एक `Redactor` ऑब्जेक्ट बनाएं जो स्रोत वर्कबुक की ओर इशारा करता हो। `Redactor` क्लास सभी रेडैक्शन ऑपरेशन्स के लिए एंट्री पॉइंट है; यह फ़ाइल को एक प्रबंधित मेमोरी स्ट्रक्चर में लोड करता है जबकि मूल फ़ाइल डिस्क पर अपरिवर्तित रहती है।

```text
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
```

### रेडैक्शन को एक ही वर्कशीट और कॉलम तक कैसे सीमित करें?
`CellFilter` क्लास आपको यह निर्दिष्ट करने देता है कि कौन सी वर्कशीट और कॉलम(स) को रेडैक्शन के लिए जांचा जाना चाहिए। लक्ष्य शीट नाम और कॉलम इंडेक्स निर्दिष्ट करने के लिए `CellFilter` का उपयोग करें। `CellFilter` क्लास रेडैक्शन इंजन द्वारा मूल्यांकन से पहले सेल्स को फ़िल्टर करता है, जिससे केवल इच्छित सेल्स प्रोसेस होते हैं।

```text
```java
import com.groupdocs.redaction.redactions.CellFilter;

// Create and configure the filter
CellFilter filter = new CellFilter();
filter.setColumnIndex(1); // Targeting the second column (index starts at 0)
filter.setWorkSheetName("Customers"); // Specify the worksheet name
```
```

### अधिकांश ईमेल पतों से मेल खाने वाला रेगुलर‑एक्सप्रेशन पैटर्न कैसे परिभाषित करें?
`java.util.regex` की `Pattern` क्लास एक संकलित रेगुलर‑एक्सप्रेशन को दर्शाती है जिसका उपयोग टेक्स्ट से मेल खाने के लिए किया जाता है। एक `Pattern` ऑब्जेक्ट बनाएं जिसमें वह रेगेक्स हो जो सामान्य ईमेल फ़ॉर्मेट को कैप्चर करे। नीचे दिया गया पैटर्न RFC‑5322‑अनुरूप अधिकांश पतों से मेल खाता है जबकि गलत स्ट्रिंग्स को अनदेखा करता है।

```text
```java
import java.util.regex.Pattern;

// Define regex pattern for matching emails
Pattern expression = Pattern.compile("^\\w+([-+.']\\w+)*@\\w+([-.]\\w+)*\\.\\w+([-.]\\w+)*$");
```
```

### रेडैक्शन लागू करें और ईमेल को प्लेसहोल्डर से कैसे बदलें?
`ReplacementOptions` क्लास यह परिभाषित करती है कि मेल खाए हुए कंटेंट को कैसे बदला जाएगा, जैसे प्लेसहोल्डर टेक्स्ट। फ़िल्टर, पैटर्न, और एक `ReplacementOptions` इंस्टेंस को मिलाएँ। `ReplacementOptions` क्लास आपको प्रत्येक रेडैक्टेड सेल में दिखाई देने वाला सटीक प्लेसहोल्डर टेक्स्ट सेट करने की अनुमति देती है।

```text
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
```

## सामान्य समस्याएँ और ट्रबलशूटिंग

- **Regex सभी मामलों को नहीं पकड़ता** – अपने डेटा के प्रतिनिधि नमूने के खिलाफ अभिव्यक्ति का परीक्षण करें और आवश्यकतानुसार कैरेक्टर क्लासेस को समायोजित करें।  
- **गलत कॉलम इंडेक्स** – याद रखें कि कॉलम इंडेक्सिंग 0 से शुरू होती है; कॉलम B का इंडेक्स 1 है।  
- **वर्कशीट नाम केस‑सेंसिटिविटी** – Excel में दिखाए गए सटीक शीट नाम का उपयोग करें; “Customers” ≠ “customers”。  
- **रिसोर्स लीक** – `Redactor` को try‑with‑resources ब्लॉक में रखें (जैसा दिखाया गया है) ताकि नेटिव रिसोर्सेज तुरंत रिलीज़ हो जाएँ।

## Excel में व्यक्तिगत डेटा को छिपाने का कारण क्या है?
Excel में व्यक्तिगत डेटा को छिपाने से सभी व्यक्तिगत पहचान योग्य जानकारी हट जाती है, जिससे फ़ाइल का उपयोग व्यक्तियों को ट्रेस करने के लिए नहीं किया जा सकता। यह गोपनीयता की रक्षा करता है, नियामक आवश्यकताओं को पूरा करता है, और बाहरी पक्षों के साथ स्प्रेडशीट साझा करने या डेटा सार्वजनिक रूप से प्रकाशित करने पर आकस्मिक लीक को रोकता है।

- **नियामक अनुपालन** – GDPR, CCPA, और उद्योग‑विशिष्ट गोपनीयता मानकों को पूरा करें।  
- **जोखिम शमन** – बाहरी साझेदारों के साथ फ़ाइलें साझा करने पर PII के आकस्मिक एक्सपोज़र को रोकें।  
- **ऑडिट तैयारियों** – संवेदनशील मानों को स्थायी रूप से हटाकर एक साफ़, अपरिवर्तनीय ऑडिट ट्रेल रखें।

## व्यावहारिक अनुप्रयोग

1. **पार्टनर डेटा एक्सचेंज** – विक्रेताओं को स्प्रेडशीट भेजने से पहले ग्राहक ईमेल को स्वचालित रूप से हटाएँ।  
2. **आंतरिक ऑडिट तैयारी** – अनुपालन समीक्षाओं के दौरान कर्मचारी डेटा को अनाम बनाएँ।  
3. **निर्धारित रिपोर्टिंग** – रेडैक्शन चरण को रात के बैच जॉब्स में एम्बेड करें जो वितरण‑तैयार रिपोर्ट बनाते हैं।

## प्रदर्शन विचार

- **बैच प्रोसेसिंग** – कई फ़ाइलों में एक ही `Redactor` इंस्टेंस को पुनः उपयोग करें ताकि JVM ओवरहेड कम हो।  
- **मेमोरी प्रबंधन** – API एक समय में एक वर्कशीट प्रोसेस करता है; 100 MB से बड़ी वर्कबुक के लिए, पंक्तियों को चंक्स में प्रोसेस करें ताकि हीप उपयोग कम रहे।  
- **बड़े डेटा सेट** – >100 k पंक्तियों वाली फ़ाइलों को संभालते समय, स्ट्रीमिंग मोड सक्षम करें (संस्करण 24.9 में उपलब्ध) ताकि मेमोरी खपत 200 MB से कम रहे।

## अक्सर पूछे जाने वाले प्रश्न

**प्रश्न: मेरा regex अभी भी कुछ कॉर्पोरेट ईमेल फ़ॉर्मेट्स को मिस कर रहा है। मुझे क्या करना चाहिए?**  
**उत्तर:** पैटर्न को अतिरिक्त अनुमत अक्षरों (जैसे “+” या “_”) को शामिल करने के लिए विस्तारित करें और बड़े नमूना सेट के खिलाफ परीक्षण करें, फिर रेडैक्शन को पुनः चलाएँ।

**प्रश्न: क्या मैं एक ही पास में एक से अधिक कॉलम को रेडैक्ट कर सकता हूँ?**  
**उत्तर:** हाँ। प्रत्येक कॉलम के लिए एक अलग `CellFilter` बनाएं और प्रत्येक फ़िल्टर को क्रमिक रूप से `redactor.apply` द्वारा लागू करें।

**प्रश्न: क्या GroupDocs.Redaction 1 GB से बड़ी Excel फ़ाइलों को संभाल सकता है?**  
**उत्तर:** लाइब्रेरी शीट्स को क्रमिक रूप से प्रोसेस करती है, इसलिए कई गीगाबाइट तक की फ़ाइलें रेडैक्ट की जा सकती हैं बशर्ते आप स्ट्रीमिंग सक्षम करें और प्रत्येक फ़ाइल के बाद `Redactor` को बंद करें।

**प्रश्न: मैं रेडैक्शन परिणाम या त्रुटियों को कैसे कैप्चर करूँ?**  
**उत्तर:** `apply` द्वारा लौटाए गए `RedactorChangeLog` की जाँच करें; गैर‑विफल स्थिति सफलता दर्शाती है, जबकि त्रुटियाँ लाइन नंबर और सेल रेफ़रेंस के साथ सूचीबद्ध होती हैं।

**प्रश्न: क्या मैं एक कस्टम प्लेसहोल्डर उपयोग कर सकता हूँ जिसमें प्रत्येक पंक्ति के लिए एक यूनिक टोकन हो?**  
**उत्तर:** बिल्कुल। प्लेसहोल्डर स्ट्रिंग को डायनामिक रूप से बनाएं (जैसे `"[redacted:" + UUID.randomUUID() + "]"`) और इसे `ReplacementOptions` को पास करें।

## अतिरिक्त संसाधन

- [दस्तावेज़ीकरण](https://docs.groupdocs.com/redaction/java/)
- [API रेफ़रेंस](https://reference.groupdocs.com/redaction/java)
- [GroupDocs.Redaction डाउनलोड करें](https://releases.groupdocs.com/redaction/java/)
- [GitHub रिपॉजिटरी](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
- [फ़्री सपोर्ट फ़ोरम](https://forum.groupdocs.com/c/redaction/33)
- [टेम्पररी लाइसेंस जानकारी](https://purchase.groupdocs.com/temporary-license/)

---

**अंतिम अपडेट:** 2026-08-09  
**परीक्षित संस्करण:** GroupDocs.Redaction 24.9 for Java  
**लेखक:** GroupDocs

## संबंधित ट्यूटोरियल

- [स्प्रेडशीट में डेटा फ़िल्टर कैसे करें – GroupDocs.Redaction Java](/redaction/java/spreadsheet-redaction/)
- [सेंसिटिव डेटा को मास्क करें Java – GroupDocs.Redaction के साथ व्यक्तिगत जानकारी को रेडैक्ट करें](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)
- [सेंसिटिव डेटा को मास्क करें Java – GroupDocs.Redaction गाइड](/redaction/java/getting-started/)