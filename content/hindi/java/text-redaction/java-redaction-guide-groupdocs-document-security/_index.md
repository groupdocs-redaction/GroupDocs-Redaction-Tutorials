---
date: '2026-08-20'
description: GroupDocs.Redaction का उपयोग करके Java दस्तावेज़ों में टेक्स्ट को रीडैक्ट
  करना सीखें, जिसमें exact‑phrase, regex, color replacement, annotation और metadata
  redaction शामिल हैं, सुरक्षित अनुपालन के लिए।
keywords:
- how to redact text
- replace text with color
- GroupDocs.Redaction Java
- Java document security
- document redaction library
lastmod: '2026-08-20'
og_description: GroupDocs.Redaction का उपयोग करके Java दस्तावेज़ों में टेक्स्ट को
  रीडैक्ट करना सीखें, जिसमें exact‑phrase, regex, color replacement, annotation और
  metadata redaction शामिल हैं।
og_image_alt: Guide showing Java code redacting text with GroupDocs.Redaction
og_title: GroupDocs.Redaction के साथ Java दस्तावेज़ों में टेक्स्ट को कैसे रीडैक्ट
  करें
schemas:
- author: GroupDocs
  dateModified: '2026-08-20'
  description: Learn how to redact text in Java documents using GroupDocs.Redaction,
    covering exact‑phrase, regex, color replacement, annotation and metadata redaction
    for secure compliance.
  headline: How to redact text in Java documents with GroupDocs.Redaction
  type: TechArticle
- description: Learn how to redact text in Java documents using GroupDocs.Redaction,
    covering exact‑phrase, regex, color replacement, annotation and metadata redaction
    for secure compliance.
  name: How to redact text in Java documents with GroupDocs.Redaction
  steps:
  - name: '**Add the Maven dependency** (or include the JAR).'
    text: '**Add the Maven dependency** (or include the JAR).'
  - name: '**Configure your license** by calling `License.setLicense("path/to/license.lic")`
      early in your application.'
    text: '**Configure your license** by calling `License.setLicense("path/to/license.lic")`
      early in your application.'
  - name: '**Create a `Redactor` instance** pointing at the source document.'
    text: '**Create a `Redactor` instance** pointing at the source document.'
  - name: '**Initialize the Redactor** with the document you want to process:'
    text: '**Initialize the Redactor** with the document you want to process:'
  - name: '**Define the exact‑phrase rule** and apply it:'
    text: '**Define the exact‑phrase rule** and apply it:'
  - name: '**Save the redacted file** to your output folder:'
    text: '**Save the redacted file** to your output folder:'
  - name: 'Load the document:'
    text: 'Load the document:'
  - name: 'Create a regex rule and apply it:'
    text: 'Create a regex rule and apply it:'
  - name: 'Save the result:'
    text: 'Save the result:'
  - name: 'Load the document:'
    text: 'Load the document:'
  type: HowTo
- questions:
  - answer: Yes. Create each redaction object, call `redactor.apply()` for each, then
      save once.
    question: Can I combine multiple redaction rules in a single pass?
  - answer: Absolutely. Pass the password to the `Redactor` constructor that accepts
      a `LoadOptions` object.
    question: Does GroupDocs.Redaction support password‑protected files?
  - answer: You can call `redactor.preview()` to generate a temporary view that highlights
      the areas to be redacted.
    question: Is it possible to preview redactions before saving?
  - answer: DOCX, PDF, PPTX, XLSX, PNG, JPEG, BMP, and many more—over 30 formats in
      total.
    question: What file formats are supported?
  - answer: Use the metadata erasure feature, remove annotations, and apply exact‑phrase
      or regex redactions to all personal data fields.
    question: How do I ensure the redacted document complies with GDPR?
  type: FAQPage
tags:
- text redaction
- GroupDocs.Redaction
- Java document security
- regex redaction
- metadata removal
title: GroupDocs.Redaction के साथ Java दस्तावेज़ों में टेक्स्ट को कैसे रीडैक्ट करें
type: docs
url: /hi/java/text-redaction/java-redaction-guide-groupdocs-document-security/
weight: 1
---

# GroupDocs.Redaction के साथ Java दस्तावेज़ों में टेक्स्ट को कैसे रेडैक्ट करें

आधुनिक अनुप्रयोगों में, **how to redact text** PDFs, Word फ़ाइलों, या छवियों के भीतर एक सामान्य आवश्यकता है अनुपालन और गोपनीयता के लिए। चाहे आपको व्यक्तिगत पहचानकर्ता छिपाने हों, गोपनीय एनोटेशन हटाने हों, या मेटाडेटा हटाना हो, GroupDocs.Redaction for Java आपको एक साफ़, प्रोग्रामेटिक तरीका देता है **java document security** हासिल करने के लिए। यह ट्यूटोरियल आपको हर आवश्यक चरण के माध्यम से ले जाता है—लाइब्रेरी सेटअप से लेकर exact‑phrase, regex, color‑based, annotation, और metadata रेडैक्शन लागू करने तक—ताकि आप रेडैक्शन को सीधे अपने बैकएंड सर्विसेज़ में एम्बेड कर सकें।

## त्वरित उत्तर
- **Java दस्तावेज़ रेडैक्शन को संभालने वाली लाइब्रेरी कौन सी है?** GroupDocs.Redaction for Java.  
- **क्या मैं टेक्स्ट को हटाने के बजाय रंग से बदल सकता हूँ?** हाँ, “replace text with color” फीचर का उपयोग करें।  
- **क्या उत्पादन उपयोग के लिए लाइसेंस चाहिए?** पूर्ण कार्यक्षमता के लिए एक अस्थायी या भुगतान किया गया लाइसेंस आवश्यक है।  
- **कौन से Java संस्करण समर्थित हैं?** JDK 8 या उससे ऊपर।  
- **क्या लाइब्रेरी जोड़ने का एकमात्र तरीका Maven है?** Maven की सिफारिश की जाती है, लेकिन आप JAR को मैन्युअल रूप से भी डाउनलोड कर सकते हैं।

## Java में “how to redact text” क्या है?
**Redaction permanently removes or obscures sensitive content so it cannot be recovered.** Java में, आप फ़ाइल लोड करते हैं, क्या छिपाना है परिभाषित करते हैं, रेडैक्शन लागू करते हैं, और साफ़ किया हुआ संस्करण सहेजते हैं। यह सुनिश्चित करता है कि कोई भी डाउनस्ट्रीम कंज्यूमर केवल साफ़ किया हुआ दस्तावेज़ देखे।

## GroupDocs.Redaction for Java का उपयोग क्यों करें?
फ़ाइल लोड करें, नियम परिभाषित करें, और SDK भारी काम संभालता है। GroupDocs.Redaction **30+ formats** का समर्थन करता है—जिसमें DOCX, PDF, PPTX, XLSX, PNG, JPEG, BMP शामिल हैं—और स्ट्रीम‑आधारित आर्किटेक्चर के माध्यम से बड़े दस्तावेज़ों को प्रोसेस करता है। यह exact‑phrase, regex, color‑based, annotation, और metadata रेडैक्शन प्रदान करता है, जिससे GDPR, HIPAA, और अन्य नियमों को पूरा करने के लिए सूक्ष्म नियंत्रण मिलता है।

## पूर्वापेक्षाएँ
- **Java Development Kit (JDK) 8+** आपके मशीन पर स्थापित होना चाहिए।  
- **Maven** निर्भरताओं के प्रबंधन के लिए (या आप JAR को मैन्युअल रूप से डाउनलोड कर सकते हैं)।  

### आवश्यक लाइब्रेरी और निर्भरताएँ
अपने `pom.xml` में GroupDocs रिपॉज़िटरी और Redaction निर्भरता जोड़ें:

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

आप आधिकारिक रिलीज़ पेज से नवीनतम JAR भी डाउनलोड कर सकते हैं: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/)।

### लाइसेंस प्राप्ति
उत्पादन उपयोग के लिए, एक अस्थायी या पूर्ण लाइसेंस प्राप्त करें। मूल्यांकन उद्देश्यों के लिए एक मुफ्त ट्रायल उपलब्ध है।

## GroupDocs.Redaction for Java सेटअप करना
1. **Add the Maven dependency** (or include the JAR).  
2. **Configure your license** by calling `License.setLicense("path/to/license.lic")` early in your application.  
   `License` वह क्लास है जो GroupDocs Redaction लाइसेंस फ़ाइल को लोड और लागू करने के लिए उपयोग होती है।  
3. **Create a `Redactor` instance** pointing at the source document.

**The `Redactor` class is the core engine that loads, modifies, and saves documents in a memory‑efficient way.** एक बार जब आपके पास `Redactor` ऑब्जेक्ट हो, तो आप परिणाम को सहेजने से पहले कई रेडैक्शन नियमों को चेन कर सकते हैं।

अब आप रेडैक्शन शुरू करने के लिए तैयार हैं।

## कार्यान्वयन गाइड

### सटीक वाक्यांश रेडैक्शन
एक विशिष्ट वाक्यांश (जैसे, किसी व्यक्ति का नाम) को प्लेसहोल्डर टेक्स्ट से बदलें।

#### सटीक‑वाक्यांश रेडैक्शन कैसे काम करता है?
`ExactPhraseRedaction` एक नियम का प्रतिनिधित्व करता है जो एक विशिष्ट सटीक टेक्स्ट स्ट्रिंग को हटाता या बदलता है। दस्तावेज़ लोड करें, एक `ExactPhraseRedaction` नियम बनाएं जो सटीक स्ट्रिंग को लक्षित करता है, नियम लागू करें, और आउटपुट सहेजें। SDK स्वचालित रूप से मिलते टेक्स्ट को ब्लैंक कर देता है जबकि लेआउट बरकरार रहता है।

1. **Initialize the Redactor** with the document you want to process:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. **Define the exact‑phrase rule** and apply it:

```java
ExactPhraseRedaction redaction = new ExactPhraseRedaction(
    "John Doe", 
    new ReplacementOptions("[Client]"));

redactor.apply(redaction);
```

3. **Save the redacted file** to your output folder:

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Redaction applied successfully.");
}
```

### रेजेक्स रेडैक्शन टेक्स्ट रिप्लेसमेंट के साथ
सीरियल नंबर जैसे पैटर्न को खोजने और उन्हें एक सामान्य टोकन से बदलने के लिए नियमित अभिव्यक्तियों (regex) का उपयोग करें।

#### रिप्लेसमेंट के साथ रेजेक्स रेडैक्शन कैसे काम करता है?
`RegexRedaction` एक नियम को परिभाषित करता है जो नियमित अभिव्यक्ति के आधार पर मिलते टेक्स्ट को खोजता और संशोधित करता है। आप एक `RegexRedaction` ऑब्जेक्ट प्रदान करते हैं जिसमें पैटर्न और रिप्लेसमेंट स्ट्रिंग होती है। इंजन दस्तावेज़ को स्कैन करता है, प्रत्येक मिलान को बदलता है, और आसपास के फ़ॉर्मेट को बरकरार रखता है।

1. Load the document:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. Create a regex rule and apply it:

```java
RegexRedaction redaction = new RegexRedaction(
    "Redaction",
    new ReplacementOptions("[Product]"));

redactor.apply(redaction);
```

3. Save the result:

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Redaction applied successfully.");
}
```

### रंग प्रतिस्थापन के साथ रेजेक्स रेडैक्शन
टेक्स्ट को हटाने के बजाय आप **replace text with color** का उपयोग करके दृश्य रूप से उसे अस्पष्ट कर सकते हैं जबकि मूल अक्षर फ़ाइल में बने रहते हैं।

#### रंग‑आधारित रेडैक्शन हटाने से कैसे अलग है?
SDK मिलते टेक्स्ट को चुने हुए रंग से पेंट करता है, जिससे वह मानव आँखों के लिए अपठनीय हो जाता है लेकिन फ़ाइल स्ट्रीम में अभी भी मौजूद रहता है। यह तब उपयोगी होता है जब आपको डाउनस्ट्रीम प्रोसेसिंग के लिए दस्तावेज़ संरचना बनाए रखनी होती है।

1. Load the document:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. Define a regex pattern and set the replacement color (e.g., blue):

```java
RegexRedaction redaction = new RegexRedaction(
    "\d{2}\s*\d{2}[^\\d]*\d{6}", 
    new ReplacementOptions(Color.BLUE));

redactor.apply(redaction);
```

3. Save the updated file:

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Redaction applied successfully.");
}
```

### एनोटेशन हटाने का रेडैक्शन
एक दस्तावेज़ से सभी एनोटेशन (टिप्पणियाँ, हाइलाइट, आदि) हटाएँ ताकि अंतिम संस्करण साफ़ हो।

#### एक कदम में एनोटेशन कैसे हटाएँ?
`AnnotationRedaction` एक नियम है जो टिप्पणियाँ, हाइलाइट और स्टैम्प जैसे एनोटेशन को हटाता है। एक `AnnotationRedaction` नियम बनाएं जो हर एनोटेशन प्रकार को लक्षित करे, इसे लागू करें, और परिवर्तन सहेजें।

1. Load your file:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. Apply the annotation‑deletion rule:

```java
DeleteAnnotationRedaction redaction = new DeleteAnnotationRedaction();

redactor.apply(redaction);
```

3. Persist the changes:

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Annotations deleted successfully.");
}
```

### मेटाडेटा मिटाने का रेडैक्शन
गोपनीयता की रक्षा करने और अनुपालन मानकों को पूरा करने के लिए सभी मेटाडेटा (लेखक, निर्माण तिथि, कस्टम प्रॉपर्टीज़) हटाएँ।

#### मेटाडेटा मिटाने से गोपनीयता कैसे सुनिश्चित होती है?
`MetadataRedaction` दस्तावेज़ से बिल्ट‑इन और कस्टम मेटाडेटा फ़ील्ड को साफ़ करता है। `MetadataRedaction` नियम बिल्ट‑इन और कस्टम मेटाडेटा फ़ील्ड को मिटा देता है, जिससे फ़ाइल की प्रॉपर्टी बैग में कोई छिपा पहचानकर्ता नहीं रहता।

1. Open the document:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. Apply the metadata‑erasure rule:

```java
EraseMetadataRedaction redaction = new EraseMetadataRedaction(MetadataFilters.All);

redactor.apply(redaction);
```

3. Save the sanitized document:

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Metadata erased successfully.");
}
```

## व्यावहारिक अनुप्रयोग (यह क्यों महत्वपूर्ण है)
- **Legal document preparation** – विरोधी वकील को ड्राफ्ट साझा करने से पहले क्लाइंट के नाम रेडैक्ट करें।  
- **Healthcare compliance** – रोगी पहचानकर्ताओं को हटाएँ ताकि HIPAA‑अनुपालन बना रहे बिना मैन्युअल एडिटिंग के।  
- **Corporate data protection** – आंतरिक रिपोर्टों में वित्तीय आंकड़े या ट्रेड सीक्रेट्स को वितरण से पहले छिपाएँ।  

इन चरणों को स्वचालित करने से मैन्युअल प्रयास कम होता है, मानव त्रुटि समाप्त होती है, और हजारों फ़ाइलों में निरंतर अनुपालन सुनिश्चित होता है।

## प्रदर्शन संबंधी विचार
- **Stream instead of load** – बड़े फ़ाइलों के लिए `Redactor` कंस्ट्रक्टर्स का उपयोग करें जो `InputStream` स्वीकार करते हैं, ताकि पूरी दस्तावेज़ को मेमोरी में लोड करने से बचा जा सके।  
- **Pre‑compile regex patterns** जब आप समान रेडैक्शन बार‑बार चलाते हैं; इससे CPU ओवरहेड 30 % तक कम हो जाता है।  
- **Monitor JVM heap** – रेडैक्शन मेमोरी‑गहन हो सकता है; मल्टी‑गिगाबाइट आर्काइव्स के बैच प्रोसेसिंग के लिए हीप साइज (`-Xmx2g`) बढ़ाने पर विचार करें।  

## सामान्य समस्याएँ और ट्रबलशूटिंग
| लक्षण | संभावित कारण | समाधान |
|---------|--------------|-----|
| `apply` के बाद कोई परिवर्तन नहीं | गलत दस्तावेज़ पथ या फ़ाइल लॉक | फ़ाइल पथ की जाँच करें और सुनिश्चित करें कि दस्तावेज़ कहीं और खुला नहीं है |
| रेगेक्स नहीं मिल रहा | पैटर्न सिंटैक्स त्रुटि | ऑनलाइन टेस्टर से रेगेक्स टेस्ट करें; बैकस्लैश को सही ढंग से एस्केप करें |
| रंग प्रतिस्थापन दिखाई नहीं दे रहा | आउटपुट फ़ॉर्मेट टेक्स्ट रंग को सपोर्ट नहीं करता (जैसे, प्लेन टेक्स्ट) | ऐसी फ़ॉर्मेट का उपयोग करें जैसे DOCX या PDF जो स्टाइलिंग को बरकरार रखता है |
| रनटाइम पर लाइसेंस त्रुटि | लाइसेंस फ़ाइल गायब या अमान्य | `.lic` फ़ाइल को पहुंच योग्य डायरेक्टरी में रखें और किसी भी Redactor उपयोग से पहले `License.setLicense` कॉल करें |

## अक्सर पूछे जाने वाले प्रश्न

**Q: क्या मैं एक ही पास में कई रेडैक्शन नियमों को संयोजित कर सकता हूँ?**  
A: हाँ। प्रत्येक रेडैक्शन ऑब्जेक्ट बनाएं, प्रत्येक के लिए `redactor.apply()` कॉल करें, फिर एक बार सहेजें।

**Q: क्या GroupDocs.Redaction पासवर्ड‑प्रोटेक्टेड फ़ाइलों को सपोर्ट करता है?**  
A: बिल्कुल। पासवर्ड को `Redactor` कंस्ट्रक्टर में पास करें जो `LoadOptions` ऑब्जेक्ट स्वीकार करता है।

**Q: क्या सहेजने से पहले रेडैक्शन का प्रीव्यू देखना संभव है?**  
A: आप `redactor.preview()` कॉल करके एक अस्थायी व्यू बना सकते हैं जो रेडैक्ट किए जाने वाले क्षेत्रों को हाइलाइट करता है।

**Q: कौन से फ़ाइल फ़ॉर्मेट समर्थित हैं?**  
A: DOCX, PDF, PPTX, XLSX, PNG, JPEG, BMP, और कई अन्य—कुल मिलाकर 30 से अधिक फ़ॉर्मेट।

**Q: कैसे सुनिश्चित करूँ कि रेडैक्ट किया गया दस्तावेज़ GDPR के अनुरूप है?**  
A: मेटाडेटा इरेज़र फीचर का उपयोग करें, एनोटेशन हटाएँ, और सभी व्यक्तिगत डेटा फ़ील्ड पर सटीक‑वाक्यांश या रेगेक्स रेडैक्शन लागू करें।

## निष्कर्ष
आपके पास अब GroupDocs.Redaction का उपयोग करके Java दस्तावेज़ों में **how to redact text** पर एक पूर्ण, एंड‑टू‑एंड गाइड है। सटीक‑वाक्यांश, रेगेक्स, रंग‑आधारित, एनोटेशन, और मेटाडेटा रेडैक्शन के चरणों का पालन करके आप मजबूत **java document security** प्राप्त कर सकते हैं जबकि अपना कोड साफ़ और रखरखाव योग्य बना सकते हैं। इन स्निपेट्स को अपनी मौजूदा सर्विसेज़ में इंटीग्रेट करें, बैच प्रोसेसिंग को स्वचालित करें, और गोपनीयता नियमों के साथ अनुपालन बनाए रखें।

---

**अंतिम अपडेट:** 2026-08-20  
**परीक्षित संस्करण:** GroupDocs.Redaction 24.9 for Java  
**लेखक:** GroupDocs

## संबंधित ट्यूटोरियल

- [replace metadata text java – Secure Redaction with GroupDocs](/redaction/java/metadata-redaction/java-redaction-metadata-text-replacement-guide/)
- [How to Redact Images in Word Documents Using GroupDocs.Redaction for Java – A Comprehensive Guide](/redaction/java/image-redaction/redact-images-word-docs-groupdocs-redaction-java/)
- [How to Redact Documents with GroupDocs Redaction Java License from File Path – A Step‑by‑Step Guide](/redaction/java/licensing-configuration/implement-groupdocs-redaction-java-license-file-path/)