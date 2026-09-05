---
date: '2026-08-20'
description: GroupDocs.Redaction के साथ Java में regex का उपयोग करके टेक्स्ट को रिडैक्ट
  करने का तरीका जानें। यह चरण‑दर‑चरण ट्यूटोरियल दिखाता है कि कैसे regex लागू करें,
  save options को कॉन्फ़िगर करें, और संवेदनशील डेटा की सुरक्षा करें।
keywords:
- how to redact text
- mask credit card numbers
- remove social security numbers
- redact pdf java
lastmod: '2026-08-20'
og_description: GroupDocs.Redaction का उपयोग करके Java में टेक्स्ट को रिडैक्ट करना
  सीखें। यह गाइड regex रिडैक्शन, save‑option कॉन्फ़िगरेशन, और संवेदनशील डेटा की सुरक्षा
  के लिए प्रदर्शन टिप्स को समझाता है।
og_image_alt: Guide showing Java code to redact text using GroupDocs.Redaction
og_title: GroupDocs.Redaction के साथ Java में टेक्स्ट को रिडैक्ट करने का तरीका
schemas:
- author: GroupDocs
  dateModified: '2026-08-20'
  description: Discover how to redact text using regex in Java with GroupDocs.Redaction.
    This step‑by‑step tutorial shows you how to apply regex, configure save options,
    and protect sensitive data.
  headline: 'How to redact text in Java with GroupDocs.Redaction: A complete guide'
  type: TechArticle
- description: Discover how to redact text using regex in Java with GroupDocs.Redaction.
    This step‑by‑step tutorial shows you how to apply regex, configure save options,
    and protect sensitive data.
  name: 'How to redact text in Java with GroupDocs.Redaction: A complete guide'
  steps:
  - name: import required classes
    text: 'The following imports give you access to the redaction API:'
  - name: initialize redactor and apply regex pattern
    text: '`RegexRedaction` represents a redaction rule based on a regular‑expression
      pattern. The pattern you provide determines which text fragments are replaced.
      - **Regex explanation**: The pattern `\b\d{3}-\d{2}-\d{4}\b` matches U.S. Social
      Security numbers (three digits, a dash, two digits, a dash, four '
  - name: configure save options
    text: '`SaveOptions` controls how the redacted file is written. Adding a suffix
      makes it clear which files have been processed, while preserving the original
      format avoids unwanted conversion. - **Save options**: `setAddSuffix(true)`
      automatically appends “_redacted” to the output filename, preventing acci'
  - name: customize additional save settings
    text: 'You can further tailor the output—such as preserving metadata or flattening
      annotations—by adjusting the `SaveOptions` object. - **Key configuration**:
      Setting `setPreserveMetadata(true)` retains original document properties, which
      is often required for compliance audits.'
  type: HowTo
- questions:
  - answer: It automatically appends a suffix (e.g., `_redacted`) to the output filename,
      making it obvious which files have been processed.
    question: What is the purpose of `setAddSuffix(true)` in SaveOptions?
  - answer: Absolutely. Any valid Java regular expression can be supplied to `RegexRedaction`
      to target emails, phone numbers, custom IDs, etc.
    question: Can I use regex patterns other than numbers for text redaction?
  - answer: Wrap the redaction logic in a try‑catch block, log the exception, and
      always close the `Redactor` in a finally clause to release resources.
    question: How should I handle errors during redaction?
  - answer: Yes. GroupDocs.Redaction works with PDF, DOCX, PPTX, and many other formats.
    question: Is PDF redaction supported?
  - answer: Use batch processing, keep regex patterns simple, and monitor memory usage
      with profiling tools.
    question: What are best practices for large‑scale redaction projects?
  type: FAQPage
tags:
- text redaction
- GroupDocs.Redaction
- Java document processing
- regex redaction
- PDF redaction
title: 'GroupDocs.Redaction के साथ Java में टेक्स्ट को रिडैक्ट करने का तरीका: एक पूर्ण
  गाइड'
type: docs
url: /hi/java/text-redaction/master-text-redaction-java-groupdocs-redaction-guide/
weight: 1
---

# Java में GroupDocs.Redaction के साथ टेक्स्ट को रीडैक्ट कैसे करें: एक संपूर्ण गाइड

आज की तेज़ गति वाली डिजिटल दुनिया में, दस्तावेज़ों में **टेक्स्ट को रीडैक्ट कैसे करें** कई डेवलपर्स के सामने एक प्रश्न है। चाहे आप व्यक्तिगत डेटा की सुरक्षा कर रहे हों, नियमों का पालन कर रहे हों, या सिर्फ़ ड्राफ्ट को साफ़ कर रहे हों, यह गाइड आपको Java के लिए GroupDocs.Redaction का उपयोग करके **रेगेक्स-आधारित रीडैक्शन को जल्दी और सुरक्षित रूप से लागू करने** के माध्यम से ले जाता है। आप सीखेंगे कि रीडैक्शन क्यों महत्वपूर्ण है, लाइब्रेरी को कैसे कॉन्फ़िगर करें, और उच्च-प्रदर्शन प्रोसेसिंग के लिए सर्वश्रेष्ठ‑प्रैक्टिस टिप्स।

## त्वरित उत्तर
- **GroupDocs.Redaction का मुख्य उद्देश्य क्या है?** यह 50 से अधिक दस्तावेज़ फ़ॉर्मैट में संवेदनशील टेक्स्ट को खोजने और मास्क करने के लिए एक विश्वसनीय API प्रदान करता है।  
- **मैं रीडैक्शन के लिए रेगेक्स कैसे लागू करूँ?** अपने पैटर्न के साथ एक `RegexRedaction` ऑब्जेक्ट बनाएं और इसे `Redactor.apply()` मेथड में पास करें।  
- **क्या मुझे लाइसेंस की जरूरत है?** विकास के लिए एक मुफ्त ट्रायल काम करता है; उत्पादन के लिए एक पेड लाइसेंस सभी सुविधाओं को अनलॉक करता है।  
- **क्या मैं PDFs के साथ-साथ DOCX फ़ाइलों को भी रीडैक्ट कर सकता हूँ?** हाँ—GroupDocs.Redaction PDF, DOCX, PPTX और कई अन्य फ़ॉर्मैट्स को सपोर्ट करता है।  
- **प्रदर्शन सुधारने का सबसे अच्छा तरीका क्या है?** `Redactor` इंस्टेंस को तुरंत बंद करें, रेगेक्स पैटर्न को सरल रखें, और फ़ाइलों को बैच में प्रोसेस करें।

## टेक्स्ट रीडैक्शन क्या है और यह क्यों महत्वपूर्ण है?
टेक्स्ट रीडैक्शन दस्तावेज़ से संवेदनशील जानकारी को स्थायी रूप से हटाता या अस्पष्ट करता है, यह सुनिश्चित करता है कि गोपनीय डेटा—जैसे सामाजिक सुरक्षा नंबर, क्रेडिट‑कार्ड विवरण, या मेडिकल रिकॉर्ड—अनधिकृत पक्षों द्वारा पुनः प्राप्त या देखा न जा सके। यह मूल अक्षरों को ओवरराइट करके या उन्हें एक मास्क से बदलकर काम करता है, इसलिए छिपी सामग्री को कॉपी‑पेस्ट या OCR टूल्स द्वारा निकाला नहीं जा सकता। यह गोपनीयता नियमों के अनुपालन को सुनिश्चित करता है और व्यक्तियों को पहचान चोरी या डेटा उल्लंघन से बचाता है।

## टेक्स्ट रीडैक्शन के लिए रेगेक्स का उपयोग क्यों करें?
रेगुलर एक्सप्रेशन आपको लचीले पैटर्न परिभाषित करने की अनुमति देते हैं जो विभिन्न डेटा फ़ॉर्मैट (जैसे फ़ोन नंबर, क्रेडिट‑कार्ड नंबर) से मेल खाते हैं। GroupDocs.Redaction के साथ रेगेक्स का उपयोग करने से आप यह सटीक नियंत्रण प्राप्त करते हैं कि क्या छिपाया जाए, जबकि कार्यान्वयन संक्षिप्त और रखरखाव योग्य रहता है।

## पूर्वापेक्षाएँ
शुरू करने से पहले, सुनिश्चित करें कि आपके पास है:

- **Java Development Kit (JDK)** स्थापित है (Java 8 या नया)।  
- Java सिंटैक्स और रेगुलर एक्सप्रेशन की बुनियादी परिचितता।  
- **IntelliJ IDEA** या **Eclipse** जैसे IDE कोड चलाने और डिबग करने के लिए।

## Java के लिए GroupDocs.Redaction सेटअप करना
सबसे पहले, लाइब्रेरी को अपने प्रोजेक्ट में जोड़ें।

### Maven सेटअप
यदि आप Maven उपयोग करते हैं, तो अपने `pom.xml` में निम्नलिखित जोड़ें:

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

### सीधे डाउनलोड
वैकल्पिक रूप से, नवीनतम JAR को [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) से डाउनलोड करें।

### बेसिक इनिशियलाइज़ेशन
`Redactor` वह मुख्य क्लास है जो दस्तावेज़ खोलता है, रीडैक्शन नियम लागू करता है, और आउटपुट लिखता है।

लाइब्रेरी उपलब्ध होने के बाद, आप दस्तावेज़ों को रीडैक्ट करना शुरू कर सकते हैं:

```java
// Import the necessary classes from GroupDocs.Redaction
import com.groupdocs.redaction.Redactor;

public class RedactionExample {
    public static void main(String[] args) {
        // Initialize the redactor with your document path
        final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
        // Ensure you close resources after operations
        try { /* Your code here */ } finally { redactor.close(); }
    }
}
```

## Java में रेगेक्स का उपयोग करके टेक्स्ट को रीडैक्ट कैसे करें?
प्रक्रिया में स्रोत फ़ाइल को `Redactor` इंस्टेंस में लोड करना, एक `RegexRedaction` नियम बनाना जो मिलान करने वाला पैटर्न परिभाषित करता है, नियम को `redactor.apply()` से लागू करना, और अंत में `SaveOptions` का उपयोग करके संशोधित दस्तावेज़ को सहेजना शामिल है। इन चरणों का पालन करके आप समर्थित फ़ॉर्मैट्स में किसी भी संवेदनशील स्ट्रिंग को विश्वसनीय रूप से खोज और मास्क कर सकते हैं।

`Redactor` क्लास वह मुख्य घटक है जो दस्तावेज़ खोलता है, रीडैक्शन नियम लागू करता है, और आउटपुट फ़ाइल लिखता है। यह आंतरिक रूप से संसाधनों का प्रबंधन करता है, इसलिए प्रोसेसिंग के बाद मेमोरी मुक्त करने के लिए इसे बंद करना आवश्यक है।

### चरण 1: आवश्यक क्लासेस इम्पोर्ट करें
निम्नलिखित इम्पोर्ट्स आपको रीडैक्शन API तक पहुंच प्रदान करते हैं:

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.redactions.RegexRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;
```

### चरण 2: रेडाक्टर को इनिशियलाइज़ करें और रेगेक्स पैटर्न लागू करें
`RegexRedaction` एक रेगुलर‑एक्सप्रेशन पैटर्न पर आधारित रीडैक्शन नियम को दर्शाता है। आप जो पैटर्न प्रदान करते हैं, वह तय करता है कि कौन से टेक्स्ट फ्रैगमेंट बदल दिए जाएंगे।

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
try {
    // Define a regex pattern to find sequences of numbers and apply a replacement color.
    // The pattern: Two digits, optional whitespace, two more digits, non-digit characters,
    // followed by six digits.
    redactor.apply(new RegexRedaction("\\d{2}\\s*\\d{2}[^\\d]*\\d{6}", 
        new ReplacementOptions(java.awt.Color.BLUE)));
```

- **रेगेक्स व्याख्या**: पैटर्न `\b\d{3}-\d{2}-\d{4}\b` अमेरिकी सामाजिक सुरक्षा नंबर (तीन अंक, एक डैश, दो अंक, एक डैश, चार अंक) से मेल खाता है। `ReplacementOptions` आपको ठोस काली ओवरले या कस्टम टेक्स्ट मास्क चुनने की अनुमति देता है।

### चरण 3: सेव ऑप्शन्स कॉन्फ़िगर करें
`SaveOptions` नियंत्रित करता है कि रीडैक्टेड फ़ाइल कैसे लिखी जाए। एक सफ़िक्स जोड़ने से यह स्पष्ट होता है कि कौन सी फ़ाइलें प्रोसेस हुई हैं, जबकि मूल फ़ॉर्मैट को बनाए रखने से अनचाही रूपांतरण से बचा जा सकता है।

```java
    // Configure save options
    SaveOptions saveOptions = new SaveOptions();
    saveOptions.setAddSuffix(true);  // Adds suffix to indicate processing
    saveOptions.setRasterizeToPDF(false);  // Preserves original format

    // Save the redacted document
    redactor.save(saveOptions);
} finally {
    redactor.close();  // Always close resources to prevent memory leaks
}
```

- **सेव ऑप्शन**: `setAddSuffix(true)` स्वचालित रूप से आउटपुट फ़ाइलनाम में “_redacted” जोड़ता है, जिससे आकस्मिक ओवरराइट से बचा जा सके।

### चरण 4: अतिरिक्त सेव सेटिंग्स को कस्टमाइज़ करें
आप `SaveOptions` ऑब्जेक्ट को समायोजित करके आउटपुट को और अधिक अनुकूलित कर सकते हैं—जैसे मेटाडाटा को संरक्षित करना या एनोटेशन को फ्लैट करना।

```java
import com.groupdocs.redaction.options.SaveOptions;

SaveOptions saveOptions = new SaveOptions();
saveOptions.setAddSuffix(true);  // Indicates processing by adding a suffix
saveOptions.setRasterizeToPDF(false);  // Keeps original format intact
```

- **मुख्य कॉन्फ़िगरेशन**: `setPreserveMetadata(true)` सेट करने से मूल दस्तावेज़ गुण संरक्षित रहते हैं, जो अक्सर अनुपालन ऑडिट के लिए आवश्यक होते हैं।

## व्यावहारिक अनुप्रयोग
वास्तविक‑दुनिया के परिदृश्य जहाँ **टेक्स्ट को रीडैक्ट कैसे करें** आवश्यक है:

1. **कानूनी दस्तावेज़** – बाहरी वकील के साथ ड्राफ्ट साझा करने से पहले क्लाइंट पहचानकर्ता छिपाएँ।  
2. **मेडिकल रिकॉर्ड** – रोगी के नाम, आईडी, या हेल्थ नंबर को मास्क करें ताकि HIPAA‑अनुपालन बना रहे।  
3. **वित्तीय रिपोर्ट** – त्रैमासिक सारांश वितरित करते समय गोपनीय खाता नंबर हटाएँ।  

## प्रदर्शन संबंधी विचार
- **मेमोरी प्रबंधन**: फ़ाइल हैंडल और नेटिव संसाधनों को मुक्त करने के लिए हमेशा `redactor.close()` कॉल करें।  
- **कुशल रेगेक्स**: सरल पैटर्न तेज़ चलते हैं; संभव हो तो एटॉमिक ग्रुप्स का उपयोग करके अत्यधिक बैक‑ट्रैकिंग से बचें।  
- **बैच प्रोसेसिंग**: बड़े दस्तावेज़ सेट के लिए, हीप उपयोग को पूर्वानुमेय रखने हेतु 20–50 फ़ाइलों के बैच में प्रोसेस करें।  

## सामान्य समस्याएँ और समाधान
| समस्या | समाधान |
|-------|----------|
| **रेगेक्स बहुत अधिक मिलान करता है** | अपने पैटर्न को ऑनलाइन रेगेक्स टेस्टर से टेस्ट करें और कैरेक्टर क्लासेस को संकीर्ण करें। |
| **आउटपुट फ़ाइल नाम संघर्ष** | `setAddSuffix(true)` का उपयोग करें या `saveOptions.setOutputPath()` के माध्यम से कस्टम आउटपुट पाथ प्रदान करें। |
| **बड़े PDFs पर मेमोरी लीक** | PDFs को पेज‑बाय‑पेज प्रोसेस करें या JVM हीप साइज बढ़ाएँ (`-Xmx2g`)। |

## अक्सर पूछे जाने वाले प्रश्न

**प्रश्न: SaveOptions में `setAddSuffix(true)` का उद्देश्य क्या है?**  
**उत्तर:** यह स्वचालित रूप से आउटपुट फ़ाइलनाम में एक सफ़िक्स (जैसे, `_redacted`) जोड़ता है, जिससे यह स्पष्ट हो जाता है कि कौन सी फ़ाइलें प्रोसेस हुई हैं।

**प्रश्न: क्या मैं टेक्स्ट रीडैक्शन के लिए संख्याओं के अलावा अन्य रेगेक्स पैटर्न उपयोग कर सकता हूँ?**  
**उत्तर:** बिल्कुल। कोई भी वैध Java रेगुलर एक्सप्रेशन `RegexRedaction` को प्रदान किया जा सकता है ताकि ईमेल, फ़ोन नंबर, कस्टम आईडी आदि को लक्षित किया जा सके।

**प्रश्न: रीडैक्शन के दौरान त्रुटियों को कैसे संभालूँ?**  
**उत्तर:** रीडैक्शन लॉजिक को try‑catch ब्लॉक में रखें, अपवाद को लॉग करें, और हमेशा `Redactor` को finally क्लॉज़ में बंद करें ताकि संसाधन मुक्त हो सकें।

**प्रश्न: क्या PDF रीडैक्शन समर्थित है?**  
**उत्तर:** हाँ। GroupDocs.Redaction PDF, DOCX, PPTX और कई अन्य फ़ॉर्मैट्स के साथ काम करता है।

**प्रश्न: बड़े‑पैमाने पर रीडैक्शन प्रोजेक्ट्स के लिए सर्वश्रेष्ठ प्रैक्टिस क्या हैं?**  
**उत्तर:** बैच प्रोसेसिंग का उपयोग करें, रेगेक्स पैटर्न को सरल रखें, और प्रोफ़ाइलिंग टूल्स के साथ मेमोरी उपयोग की निगरानी करें।

## अतिरिक्त संसाधन
- **डॉक्यूमेंटेशन**: [GroupDocs Redaction Documentation](https://docs.groupdocs.com/redaction/java/)  
- **API रेफ़रेंस**: [GroupDocs API Reference](https://apireference.groupdocs.com/redaction/java)

---

**अंतिम अपडेट:** 2026-08-20  
**परीक्षित संस्करण:** GroupDocs.Redaction 24.9 for Java  
**लेखक:** GroupDocs

## संबंधित ट्यूटोरियल

- [संवेदनशील डेटा को मास्क करें Java – GroupDocs.Redaction गाइड](/redaction/java/getting-started/)
- [संवेदनशील डेटा को मास्क करें Java – GroupDocs.Redaction के साथ व्यक्तिगत जानकारी को रीडैक्ट करें](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)
- [Aspose OCR और Java के साथ PDF को रीडैक्ट कैसे करें - GroupDocs.Redaction का उपयोग करके रेगेक्स पैटर्न लागू करना](/redaction/java/ocr-integration/aspose-ocr-java-pdf-redaction/)