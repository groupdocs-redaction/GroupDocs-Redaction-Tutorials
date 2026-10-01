---
date: '2026-10-01'
description: Java में GroupDocs Redaction का उपयोग करके लेखक मेटाडेटा हटाना और संशोधित
  दस्तावेज़ फ़ाइलें सहेजना सीखें।
keywords:
- remove author metadata
- save redacted document
- groupdocs metadata removal
lastmod: '2026-10-01'
og_description: Java में GroupDocs Redaction का उपयोग करके लेखक मेटाडेटा हटाना और
  संशोधित दस्तावेज़ फ़ाइलें सहेजना सीखें। चरण‑दर‑चरण मार्गदर्शिका का पालन करें।
og_image_alt: Guide showing Java code to remove author metadata using GroupDocs Redaction
og_title: Java में GroupDocs के साथ लेखक मेटाडेटा कैसे हटाएँ
schemas:
- author: GroupDocs
  dateModified: '2026-10-01'
  description: Learn how to remove author metadata and save redacted document files
    in Java using GroupDocs Redaction.
  headline: How to remove author metadata in Java with GroupDocs
  type: TechArticle
- description: Learn how to remove author metadata and save redacted document files
    in Java using GroupDocs Redaction.
  name: How to remove author metadata in Java with GroupDocs
  steps:
  - name: '**Legal documents** – Redact author information before sending contracts
      to opposing counsel.'
    text: '**Legal documents** – Redact author information before sending contracts
      to opposing counsel.'
  - name: '**Corporate reports** – Remove manager names when publishing quarterly
      results to shareholders.'
    text: '**Corporate reports** – Remove manager names when publishing quarterly
      results to shareholders.'
  - name: '**Project files** – Clean up internal project documentation before archiving
      or uploading to a public repository.'
    text: '**Project files** – Clean up internal project documentation before archiving
      or uploading to a public repository.'
  type: HowTo
- questions:
  - answer: It removes selected metadata fields from a document.
    question: What does EraseMetadataRedaction do?
  - answer: GroupDocs.Redaction for Java.
    question: Which library provides this feature?
  - answer: A free trial works for testing; a permanent license is required for production.
    question: Do I need a license?
  - answer: Yes, combine filters with a logical OR.
    question: Can I target multiple fields at once?
  - answer: Redactor instances are not shared across threads; create a new instance
      per operation.
    question: Is the process thread‑safe?
  type: FAQPage
tags:
- metadata redaction
- GroupDocs
- Java document processing
title: Java में GroupDocs के साथ लेखक मेटाडेटा कैसे हटाएँ
type: docs
url: /hi/java/metadata-redaction/groupdocs-redaction-java-metadata-implementation/
weight: 1
---

# जावा में GroupDocs के साथ लेखक मेटाडेटा कैसे हटाएँ

आज के डिजिटल परिदृश्य में, दस्तावेज़ों के भीतर छिपी संवेदनशील जानकारी की सुरक्षा एक आवश्यक अभ्यास है। **लेखक मेटाडेटा हटाने** से व्यक्तिगत या कॉर्पोरेट पहचानकर्ताओं का आकस्मिक खुलासा रोकता है। यह ट्यूटोरियल आपको चरण दर चरण दिखाता है कि जावा के लिए GroupDocs.Redaction से `EraseMetadataRedaction` का उपयोग करके Word फ़ाइलों से *Author* और *Manager* जैसे फ़ील्ड को कैसे हटाएँ, और फिर **रेडैक्टेड दस्तावेज़** की प्रतियों को सुरक्षित रूप से साझा करने या संग्रहित करने के लिए कैसे सहेजें।

## त्वरित उत्तर
- **EraseMetadataRedaction क्या करता है?** यह दस्तावेज़ से चयनित मेटाडेटा फ़ील्ड को हटाता है।  
- **कौन सी लाइब्रेरी यह सुविधा प्रदान करती है?** GroupDocs.Redaction for Java.  
- **क्या मुझे लाइसेंस चाहिए?** परीक्षण के लिए एक मुफ्त ट्रायल काम करता है; उत्पादन के लिए एक स्थायी लाइसेंस आवश्यक है।  
- **क्या मैं एक साथ कई फ़ील्ड लक्षित कर सकता हूँ?** हाँ, लॉजिकल OR के साथ फ़िल्टर को संयोजित करें।  
- **क्या प्रक्रिया थ्रेड‑सेफ़ है?** Redactor इंस्टेंस थ्रेड्स के बीच साझा नहीं किए जाते; प्रत्येक ऑपरेशन के लिए एक नया इंस्टेंस बनाएँ।

## EraseMetadataRedaction क्या है?
`EraseMetadataRedaction` एक अंतर्निहित रेडैक्शन क्लास है जो आपको यह निर्दिष्ट करने देता है कि कौन से मेटाडेटा एंट्रीज़ को हटाया जाना चाहिए। यह GroupDocs.Redaction द्वारा समर्थित विभिन्न दस्तावेज़ फ़ॉर्मेट्स पर काम करता है, यह सुनिश्चित करते हुए कि छिपी हुई लेखन जानकारी कभी लीक न हो। आप मानक प्रॉपर्टीज़ जैसे Author, Manager, और कस्टम मेटाडेटा फ़ील्ड को भी लक्षित कर सकते हैं, जिससे व्यापक गोपनीयता सुरक्षा मिलती है।

## GroupDocs के साथ EraseMetadataRedaction क्यों उपयोग करें?
GroupDocs.Redaction **100 से अधिक इनपुट और आउटपुट फ़ॉर्मेट्स** का समर्थन करता है और पूरी फ़ाइल को मेमोरी में लोड किए बिना 500 पृष्ठों तक के दस्तावेज़ों को प्रोसेस कर सकता है। इस क्लास का उपयोग करने से आपको एकल, उच्च‑प्रदर्शन API मिलता है जो GDPR, HIPAA, या आंतरिक अनुपालन आवश्यकताओं को पूरा करता है जबकि आपका कोडबेस सरल रहता है।

## पूर्वापेक्षाएँ
- Java 8 या उससे ऊपर स्थापित होना चाहिए।  
- Maven (या मैन्युअली JAR जोड़ने की क्षमता)।  
- GroupDocs.Redaction for Java (संस्करण 24.9 या बाद)।  
- एक वैध GroupDocs ट्रायल या स्थायी लाइसेंस।

## जावा के लिए GroupDocs.Redaction सेटअप करना

### Maven इंस्टॉलेशन
अपने **pom.xml** में GroupDocs रिपॉजिटरी और डिपेंडेंसी जोड़ें:

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

### डायरेक्ट डाउनलोड
वैकल्पिक रूप से, नवीनतम JAR को [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) से डाउनलोड करें।

### लाइसेंस प्राप्त करना
GroupDocs पोर्टल से एक मुफ्त ट्रायल प्राप्त करें या अस्थायी लाइसेंस खरीदें। लाइसेंस फ़ाइल को उस स्थान पर रखें जहाँ आपका एप्लिकेशन इसे लोड कर सके (जैसे, classpath रूट)।

### बुनियादी इनिशियलाइज़ेशन और सेटअप
नीचे एक न्यूनतम उदाहरण है जो DOCX फ़ाइल के लिए `Redactor` इंस्टेंस बनाता है:

```java
import com.groupdocs.redaction.Redactor;

String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
Redactor redactor = new Redactor(filePath);
```

## जावा में EraseMetadataRedaction का उपयोग कैसे करें
निम्नलिखित अनुभाग कार्यान्वयन को स्पष्ट, क्रियात्मक चरणों में विभाजित करते हैं।

### फीचर: विशिष्ट मेटाडेटा आइटम साफ़ करें

#### अवलोकन
हम `EraseMetadataRedaction` का उपयोग करके **Author** और **Manager** मेटाडेटा फ़ील्ड को हटाएंगे। यह बाहरी साझेदारों के साथ आंतरिक रिपोर्ट साझा करते समय एक सामान्य आवश्यकता है।

#### चरण‑दर‑चरण कार्यान्वयन

##### 1️⃣ Redactor ऑब्जेक्ट को इनिशियलाइज़ करें
`Redactor` वह मुख्य क्लास है जो दस्तावेज़ लोड करता है, रेडैक्शन ऑब्जेक्ट्स लागू करता है, और परिणाम लिखता है। आप जिस प्रत्येक फ़ाइल को प्रोसेस करते हैं, उसके लिए एक नया इंस्टेंस बनाएँ:

```java
import com.groupdocs.redaction.Redactor;

String inputFilePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
final Redactor redactor = new Redactor(inputFilePath);
```

##### 2️⃣ EraseMetadataRedaction लागू करें
`MetadataFilters` सामान्य मेटाडेटा कुंजियों जैसे Author और Manager के लिए पूर्वनिर्धारित फ़िल्टर प्रदान करता है।  
`EraseMetadataRedaction` उन मेटाडेटा एंट्रीज़ को हटाता है जो प्रदान किए गए `MetadataFilters` से मेल खाती हैं। बिटवाइज़ OR (`|`) `Author` और `Manager` फ़िल्टर को मिलाता है ताकि दोनों फ़ील्ड एक कॉल में हटाए जा सकें:

```java
import com.groupdocs.redaction.redactions.EraseMetadataRedaction;
import com.groupdocs.redaction.MetadataFilters;

try {
    redactor.apply(new EraseMetadataRedaction(MetadataFilters.Author | MetadataFilters.Manager));
} finally {
    redactor.close();
}
```

##### 3️⃣ सहेजने के विकल्प कॉन्फ़िगर करें
`SaveOptions` आपको आउटपुट फ़ाइल नाम, फ़ॉर्मेट, और अन्य सहेजने पैरामीटर निर्दिष्ट करने देता है।  
`SaveOptions` आपको आउटपुट फ़ाइल नाम, फ़ॉर्मेट, और यह नियंत्रित करने देता है कि दस्तावेज़ को PDF में रास्टराइज़ किया जाना चाहिए या नहीं। एक उपसर्ग जोड़ने से मूल फ़ाइल अपरिवर्तित रहती है:

```java
import com.groupdocs.redaction.options.SaveOptions;

SaveOptions saveOptions = new SaveOptions();
saveOptions.setAddSuffix(true); // Adds "_Redacted" to the file name
saveOptions.setRasterizeToPDF(false);

redactor.save(saveOptions);
```

## सामान्य उपयोग केस
1. **Legal documents** – विरोधी counsel को अनुबंध भेजने से पहले लेखक जानकारी को रेडैक्ट करें।  
2. **Corporate reports** – शेयरधारकों को त्रैमासिक परिणाम प्रकाशित करते समय मैनेजर नाम हटाएँ।  
3. **Project files** – सार्वजनिक रिपॉजिटरी में अपलोड या आर्काइव करने से पहले आंतरिक प्रोजेक्ट दस्तावेज़ साफ़ करें।  

## समस्या निवारण टिप्स
- **File not found** – `inputFilePath` में दिया गया पथ मौजूद फ़ाइल की ओर इशारा करता है और एप्लिकेशन के पास पढ़ने की अनुमति है, यह सत्यापित करें।  
- **Missing metadata fields** – सभी दस्तावेज़ प्रकार समान मेटाडेटा कुंजियाँ नहीं रखते; पहले Office में दस्तावेज़ की प्रॉपर्टीज़ जांचें।  
- **License errors** – `Redactor` इंस्टेंस बनाने से पहले लाइसेंस फ़ाइल सही तरीके से लोड हुई है, यह सुनिश्चित करें।  

## प्रदर्शन संबंधी विचार
- `Redactor` ऑब्जेक्ट को तुरंत बंद करें (जैसा कि `finally` ब्लॉक में दिखाया गया है) ताकि मूल संसाधन मुक्त हो सकें।  
- बड़े दस्तावेज़ों को रास्टराइज़ करने से बचें जब तक कि आपको PDF प्रीव्यू की आवश्यकता न हो; रास्टराइज़ेशन 300‑पृष्ठ फ़ाइलों के लिए CPU और मेमोरी उपयोग को 3 गुना तक बढ़ा सकता है।  

## अक्सर पूछे जाने वाले प्रश्न

**Q1: मेटाडेटा रेडैक्शन क्या है?**  
A1: मेटाडेटा रेडैक्शन में छिपी दस्तावेज़ प्रॉपर्टीज़ (जैसे author, manager, या कस्टम टैग) को हटाना शामिल है ताकि संवेदनशील जानकारी का आकस्मिक खुलासा न हो।

**Q2: क्या मैं GroupDocs.Redaction को अन्य फ़ाइल प्रकारों के लिए उपयोग कर सकता हूँ?**  
A2: हाँ, लाइब्रेरी PDF, DOCX, PPTX, XLSX, और कई अन्य फ़ॉर्मेट्स—कुल मिलाकर 100 से अधिक—को सपोर्ट करती है।

**Q3: रेडैक्शन के दौरान त्रुटियों को कैसे संभालूँ?**  
A3: `apply` कॉल को try‑catch ब्लॉक में रखें और हमेशा `Redactor` को finally क्लॉज़ में बंद करें ताकि संसाधन रिलीज़ हो सकें।

**Q4: क्या कस्टम मेटाडेटा फ़ील्ड को रेडैक्ट करना संभव है?**  
A5: बिल्कुल। किसी भी कस्टम प्रॉपर्टी को लक्षित करने के लिए `MetadataFilters.Custom("YourFieldName")` का उपयोग करें।

**Q5: GroupDocs.Redaction का उपयोग करने के सर्वोत्तम अभ्यास क्या हैं?**  
A5:  
- अपने एप्लिकेशन में लाइसेंस को जल्दी लोड करें।  
- `Redactor` ऑब्जेक्ट्स को तुरंत बंद करें।  
- मूल फ़ाइलों को अपरिवर्तित रखने के लिए `SaveOptions` के साथ उपसर्ग जोड़ें।  
- बैच प्रोसेसिंग से पहले दस्तावेज़ की एक कॉपी पर रेडैक्शन का परीक्षण करें।

**Q6: क्या EraseMetadataRedaction बैच ऑपरेशन्स को सपोर्ट करता है?**  
A6: आप फ़ाइल पाथ्स के संग्रह पर लूप कर सकते हैं, प्रत्येक फ़ाइल के लिए नया `Redactor` बनाते हुए और समान रेडैक्शन लॉजिक लागू करते हुए।

**Q7: क्या मैं EraseMetadataRedaction को अन्य रेडैक्शन प्रकारों के साथ संयोजित कर सकता हूँ?**  
A7: हाँ, आप सहेजने से पहले कई रेडैक्शन ऑब्जेक्ट्स (जैसे, टेक्स्ट रेडैक्शन के बाद मेटाडेटा रेडैक्शन) को श्रृंखलाबद्ध कर सकते हैं।

## संसाधन

- **डॉक्यूमेंटेशन**: [GroupDocs Redaction Java Docs](https://docs.groupdocs.com/redaction/java/)  
- **API संदर्भ**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java)  
- **डाउनलोड**: [Latest Releases](https://releases.groupdocs.com/redaction/java/)  
- **GitHub**: [GroupDocs GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **नि:शुल्क समर्थन**: [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)  
- **अस्थायी लाइसेंस**: [Acquire a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**अंतिम अपडेट:** 2026-10-01  
**परिक्षित संस्करण:** GroupDocs.Redaction 24.9 for Java  
**लेखक:** GroupDocs

## संबंधित ट्यूटोरियल

- [Groupdocs Redaction Java दस्तावेज़ मेटाडेटा निष्कर्षण](/redaction/java/metadata-redaction/groupdocs-redaction-java-document-metadata-extraction/)  
- [GroupDocs.Redaction का उपयोग करके जावा में मेटाडेटा कैसे हटाएँ](/redaction/java/metadata-redaction/metadata-redaction-groupdocs-java-guide/)  
- [Groupdocs Redaction जावा का उपयोग करके दस्तावेज़ जानकारी प्राप्त करें](/redaction/java/document-information/retrieve-document-info-using-groupdocs-redaction-java/)