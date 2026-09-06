---
date: '2026-09-06'
description: GroupDocs.Redaction for Java के साथ java में फ़ाइल एक्सटेंशन प्राप्त
  करना, दस्तावेज़ का आकार, पृष्ठ गिनती और PDF मेटाडेटा पुनः प्राप्त करना सीखें। आज
  ही अपने Java ऐप की दस्तावेज़ हैंडलिंग को बढ़ाएँ।
keywords:
- java get file extension
- java file type detection
- get document size java
- get page count java
- read pdf metadata java
lastmod: '2026-09-06'
og_description: GroupDocs.Redaction for Java के साथ java में फ़ाइल एक्सटेंशन, दस्तावेज़
  आकार, पृष्ठ गिनती और PDF मेटाडेटा कैसे प्राप्त करें जानें। सरल कोड, तेज़ परिणाम।
og_image_alt: Guide showing Java code to extract file type, size, and page count using
  GroupDocs.Redaction
og_title: GroupDocs.Redaction का उपयोग करके java में फ़ाइल एक्सटेंशन कैसे प्राप्त
  करें
schemas:
- author: GroupDocs
  dateModified: '2026-09-06'
  description: Learn how to java get file extension, retrieve document size, page
    count, and PDF metadata with GroupDocs.Redaction for Java. Boost your Java app's
    document handling today.
  headline: How to java get file extension using GroupDocs.Redaction
  type: TechArticle
- description: Learn how to java get file extension, retrieve document size, page
    count, and PDF metadata with GroupDocs.Redaction for Java. Boost your Java app's
    document handling today.
  name: How to java get file extension using GroupDocs.Redaction
  steps:
  - name: import necessary classes
    text: 'Add the required imports at the top of your Java file:'
  - name: initialize the redactor
    text: The `Redactor` class is the core engine that opens a document and provides
      access to its metadata.
  - name: retrieve and display document info
    text: '`IDocumentInfo` provides the metadata you need. Call `getDocumentInfo()`
      once and then query the three properties. The three `System.out.println` statements
      output the file type, page count, and size in bytes—exactly the data you need
      for downstream processing.'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction is a Java library that enables redaction, metadata
      extraction, and format‑agnostic document processing across more than 50 file
      types.
    question: What is GroupDocs.Redaction?
  - answer: Yes, `IDocumentInfo` returns PDF version, encryption status, and basic
      metadata without extra code.
    question: Can I retrieve metadata from PDF files?
  - answer: Enclose the `getDocumentInfo()` call in a `try‑catch` block and handle
      `RedactionException` to manage corrupted or unsupported files.
    question: How do I handle exceptions when retrieving document info?
  - answer: File type, number of pages, size in bytes, PDF version, encryption flag,
      and basic author/creation metadata.
    question: What kind of information can I get about a document?
  - answer: Yes, instantiate a separate `Redactor` for each file inside a thread pool
      and reuse the same JVM to achieve high throughput.
    question: Is there support for batch‑processing many documents efficiently?
  type: FAQPage
tags:
- document metadata
- GroupDocs.Redaction
- Java file handling
title: GroupDocs.Redaction का उपयोग करके java में फ़ाइल एक्सटेंशन कैसे प्राप्त करें
type: docs
url: /hi/java/document-information/retrieve-document-info-using-groupdocs-redaction-java/
weight: 1
---

# GroupDocs.Redaction का उपयोग करके जावा में फ़ाइल एक्सटेंशन कैसे प्राप्त करें

आधुनिक जावा अनुप्रयोगों में जो उपयोगकर्ता‑अपलोड की गई फ़ाइलों को प्रोसेस करते हैं, फ़ाइल प्रकार को जल्दी‑से‑जल्दी जानना — **java get file extension** — रूटिंग, सुरक्षा, और संसाधन योजना के लिए आवश्यक है। यह ट्यूटोरियल आपको दिखाता है कि जावा में फ़ाइल एक्सटेंशन कैसे प्राप्त करें, दस्तावेज़ का आकार, पृष्ठ गिनती, और यहाँ तक कि GroupDocs.Redaction लाइब्रेरी का उपयोग करके PDF मेटाडेटा कैसे प्राप्त करें। अंत तक, आपके पास एक ही, कम‑मेमोरी कॉल होगा जो सभी आवश्यक प्रमुख गुण लौटाता है।

## त्वरित उत्तर
- **फ़ाइल प्रकार लौटाने वाली विधि कौन सी है?** `IDocumentInfo.getFileType()`
- **मैं पृष्ठ गिनती कैसे प्राप्त कर सकता हूँ?** `IDocumentInfo.getPageCount()`
- **कौन सा कॉल दस्तावेज़ का आकार बाइट्स में देता है?** `IDocumentInfo.getSize()`
- **क्या नमूना चलाने के लिए लाइसेंस की आवश्यकता है?** परीक्षण या अस्थायी लाइसेंस मूल्यांकन के लिए काम करता है।
- **कौन सा जावा संस्करण आवश्यक है?** Java 8 या उससे ऊपर।

## “java get file extension” क्या है?
**java get file extension** का मतलब जावा में प्रोग्रामेटिक रूप से दस्तावेज़ से फ़ाइल फ़ॉर्मेट (जैसे DOCX, PDF) निकालना है। GroupDocs.Redaction इस जानकारी को `IDocumentInfo` इंटरफ़ेस के माध्यम से उजागर करता है, इसलिए एक ही मेथड कॉल एक्सटेंशन स्ट्रिंग लौटाती है।

## मेटाडेटा निष्कर्षण के लिए GroupDocs.Redaction क्यों उपयोग करें?
GroupDocs.Redaction **50+** इनपुट फ़ॉर्मेट्स—जैसे PDF, DOCX, XLSX, PPTX, और इमेज प्रकार—से मेटाडेटा पढ़ सकता है, बिना पूरी फ़ाइल को मेमोरी में लोड किए। यह सामान्य सर्वर पर 300‑पृष्ठ PDF को 200 ms से कम समय में प्रोसेस करता है, RAM उपयोग को 20 MB से नीचे रखता है। यह प्रदर्शन‑ऑप्टिमाइज़्ड दृष्टिकोण आपको बैच जॉब्स को स्केल करने देता है जबकि सभी समर्थित फ़ॉर्मेट्स में सुसंगत परिणाम बनाए रखता है।

## पूर्वापेक्षाएँ
- Java 8 या उससे नया स्थापित हो।
- Maven‑संगत IDE (IntelliJ IDEA, Eclipse, आदि)।
- GroupDocs.Redaction लाइसेंस तक पहुंच (फ़्री ट्रायल या अस्थायी लाइसेंस)।

## जावा के लिए GroupDocs.Redaction सेटअप करना

### Maven इंस्टॉलेशन
`pom.xml` फ़ाइल में रिपॉजिटरी और डिपेंडेंसी जोड़ें:

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
वैकल्पिक रूप से, नवीनतम संस्करण [GroupDocs.Redaction जावा रिलीज़](https://releases.groupdocs.com/redaction/java/) से डाउनलोड करें।

#### लाइसेंस प्राप्ति
- **फ़्री ट्रायल:** लाइब्रेरी का मूल्यांकन करने के लिए फ़्री ट्रायल से शुरू करें।  
- **अस्थायी लाइसेंस:** विस्तारित मूल्यांकन के लिए अस्थायी लाइसेंस प्राप्त करें।  
- **खरीद:** यदि यह आपकी आवश्यकताओं के अनुरूप है तो खरीदने पर विचार करें।

## वास्तविक‑विश्व प्रोजेक्ट्स में java get file extension क्यों महत्वपूर्ण है
अपलोड के समय दस्तावेज़ के प्रकार को जानना आपको फ़ाइलों को सही प्रोसेसिंग पाइपलाइन में रूट करने देता है—PDF को रिडैक्शन, Word फ़ाइलों को कन्वर्ज़न, इमेज को OCR के लिए। यह सुरक्षा जाँच (एक्जीक्यूटेबल फ़ाइलों को ब्लॉक करना) और दस्तावेज़ प्रबंधन सिस्टम में सटीक UI आइकन भी सक्षम करता है।

## java get file extension, get document size java, और get page count java कैसे करें
आप `IDocumentInfo` की एक ही कॉल से फ़ाइल प्रकार, आकार, और पृष्ठ गिनती प्राप्त कर सकते हैं। यह कॉल केवल दस्तावेज़ हेडर पढ़ती है, इसलिए बड़ी फ़ाइलें भी तेज़ी से और न्यूनतम मेमोरी ओवरहेड के साथ प्रोसेस होती हैं। यह हल्का दृष्टिकोण बैच प्रोसेसिंग के लिए आदर्श है जहाँ आगे की कार्रवाई तय करने से पहले केवल सारांश जानकारी आवश्यक होती है। `IDocumentInfo` इंटरफ़ेस फ़ाइल प्रकार, पृष्ठ गिनती, और आकार जैसी मेटाडेटा प्रदान करता है बिना पूरे दस्तावेज़ को लोड किए।

### चरण 1: आवश्यक क्लासेज़ इम्पोर्ट करें
अपने जावा फ़ाइल के शीर्ष पर आवश्यक इम्पोर्ट जोड़ें:

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.domain.IDocumentInfo;
```

### चरण 2: रेडैक्टर को इनिशियलाइज़ करें
`Redactor` क्लास वह कोर इंजन है जो दस्तावेज़ खोलता है और उसकी मेटाडेटा तक पहुंच प्रदान करता है।

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
try {
    // Code for retrieving information will go here.
} finally {
    redactor.close();
}
```

### चरण 3: दस्तावेज़ जानकारी प्राप्त करें और प्रदर्शित करें
`IDocumentInfo` वह मेटाडेटा प्रदान करता है जिसकी आपको आवश्यकता है। `getDocumentInfo()` को एक बार कॉल करें और फिर तीन गुणों को क्वेरी करें।

```java
// Retrieve document information
IDocumentInfo info = redactor.getDocumentInfo();

// Output document type, page count, and size in bytes
System.out.println("File Type: " + info.getFileType());
System.out.println("Page Count: " + info.getPageCount());
System.out.println("Size (Bytes): " + info.getSize());
```

तीन `System.out.println` स्टेटमेंट्स फ़ाइल प्रकार, पृष्ठ गिनती, और बाइट्स में आकार आउटपुट करते हैं—बिल्कुल वही डेटा जो आपको डाउनस्ट्रीम प्रोसेसिंग के लिए चाहिए।

## pdf मेटाडेटा java कैसे प्राप्त करें
`Redactor` के साथ PDF लोड करें और `getDocumentInfo()` कॉल करें। वही मेथड PDF‑विशिष्ट फ़ील्ड जैसे संस्करण और एन्क्रिप्शन स्थिति लौटाता है, इसलिए अतिरिक्त कोड की आवश्यकता नहीं है। लौटाया गया `IDocumentInfo` ऑब्जेक्ट भी PDF‑विशिष्ट फ़ील्ड जैसे संस्करण संख्या, एन्क्रिप्शन फ़्लैग, और मानक मेटाडेटा (लेखक, शीर्षक, निर्माण तिथि) शामिल करता है। आप इन प्रॉपर्टीज़ को सीधे गेटर मेथड्स से एक्सेस कर सकते हैं, जिससे अतिरिक्त पार्सिंग के बिना PDF विवरण दिखा या लॉग कर सकते हैं।

## सामान्य उपयोग केस
1. **डॉक्यूमेंट मैनेजमेंट सिस्टम:** फ़ाइलों को प्रकार या आकार के आधार पर स्टोर करने से पहले ऑटो‑कैटेगराइज़ करें।  
2. **कंटेंट प्रोसेसिंग पाइपलाइन:** पृष्ठ गिनती के आधार पर विभिन्न प्रोसेसिंग रणनीतियां चुनें (जैसे, बड़े PDFs को बैच‑रिडैक्ट बनाम छोटे Word डॉक्यूमेंट)।  
3. **डिजिटल एसेट लाइब्रेरीज़:** फ़ाइल खोलें बिना उपयोगकर्ताओं को दस्तावेज़ गुणों का त्वरित प्रीव्यू दिखाएँ।

## सामान्य समस्याएँ और समाधान
- **फ़ाइल नहीं मिली:** आप `Redactor` को जो absolute या relative पाथ पास कर रहे हैं उसे सत्यापित करें।  
- **असमर्थित फ़ॉर्मेट:** सुनिश्चित करें कि आपके दस्तावेज़ का एक्सटेंशन GroupDocs.Redaction द्वारा समर्थित 50+ फ़ॉर्मेट्स में सूचीबद्ध है।  
- **लाइसेंस त्रुटियाँ:** वैध ट्रायल या स्थायी लाइसेंस उपयोग करें; अन्यथा API लाइसेंसिंग एक्सेप्शन फेंकेगा।

## ट्रबलशूटिंग टिप्स (read document metadata java)
- मेटाडेटा कॉल्स को `try‑catch` ब्लॉक में रैप करें ताकि भ्रष्ट फ़ाइलों को सुगमता से संभाला जा सके।  
- मेटाडेटा पढ़ने से पहले एन्क्रिप्टेड PDFs का पता लगाने के लिए `redactor.isEncrypted()` (यदि उपलब्ध हो) का उपयोग करें।  
- कई फ़ाइलों को प्रोसेस करते समय, थ्रेड‑पूल को पुनः उपयोग करें और प्रत्येक `Redactor` इंस्टेंस को तुरंत बंद करें ताकि फ़ाइल‑हैंडल लीक न हो।

## प्रदर्शन विचार
बड़े बैचों को संभालते समय:
- प्रत्येक दस्तावेज़ को `try‑with‑resources` ब्लॉक में खोलें ताकि फ़ाइल हैंडल्स का समय पर रिलीज़ सुनिश्चित हो।  
- केवल आवश्यक मेटाडेटा को कैश करें; जब तक आवश्यक न हो, पूरे दस्तावेज़ की सामग्री लोड करने से बचें।

## अक्सर पूछे जाने वाले प्रश्न
**प्रश्न: GroupDocs.Redaction क्या है?**  
**उत्तर:** GroupDocs.Redaction एक जावा लाइब्रेरी है जो रिडैक्शन, मेटाडेटा निष्कर्षण, और 50 से अधिक फ़ाइल प्रकारों में फ़ॉर्मेट‑अज्ञेय दस्तावेज़ प्रोसेसिंग सक्षम करती है।

**प्रश्न: क्या मैं PDF फ़ाइलों से मेटाडेटा प्राप्त कर सकता हूँ?**  
**उत्तर:** हाँ, `IDocumentInfo` अतिरिक्त कोड के बिना PDF संस्करण, एन्क्रिप्शन स्थिति, और बुनियादी मेटाडेटा लौटाता है।

**प्रश्न: दस्तावेज़ जानकारी प्राप्त करते समय अपवादों को कैसे संभालें?**  
**उत्तर:** `getDocumentInfo()` कॉल को `try‑catch` ब्लॉक में रखें और `RedactionException` को संभालें ताकि भ्रष्ट या असमर्थित फ़ाइलों को प्रबंधित किया जा सके।

**प्रश्न: मैं दस्तावेज़ के बारे में किस प्रकार की जानकारी प्राप्त कर सकता हूँ?**  
**उत्तर:** फ़ाइल प्रकार, पृष्ठों की संख्या, बाइट्स में आकार, PDF संस्करण, एन्क्रिप्शन फ़्लैग, और बुनियादी लेखक/निर्माण मेटाडेटा।

**प्रश्न: क्या कई दस्तावेज़ों को कुशलतापूर्वक बैच‑प्रोसेस करने का समर्थन है?**  
**उत्तर:** हाँ, थ्रेड पूल के भीतर प्रत्येक फ़ाइल के लिए अलग `Redactor` बनाएं और उच्च थ्रूपुट प्राप्त करने के लिए वही JVM पुनः उपयोग करें।

## निष्कर्ष
अब आप जानते हैं कि GroupDocs.Redaction का उपयोग करके **java get file extension**, **get document size java**, **get page count java**, और **retrieve pdf metadata java** कैसे किया जाता है। इन स्निपेट्स को अपने जावा अनुप्रयोगों में एकीकृत करें ताकि दस्तावेज़ हैंडलिंग के बारे में अधिक समझदार निर्णय ले सकें, प्रदर्शन में सुधार करें, और उपयोगकर्ता अनुभव को समृद्ध बना सकें।

---

**अंतिम अपडेट:** 2026-09-06  
**परीक्षित संस्करण:** GroupDocs.Redaction 24.9 for Java  
**लेखक:** GroupDocs  

**संसाधन**
- **दस्तावेज़ीकरण:** [GroupDocs Redaction जावा दस्तावेज़ीकरण](https://docs.groupdocs.com/redaction/java/)  
- **API रेफ़रेंस:** [GroupDocs API रेफ़रेंस](https://reference.groupdocs.com/redaction/java)  
- **डाउनलोड:** [GroupDocs.Redaction जावा डाउनलोड्स](https://releases.groupdocs.com/redaction/java/)  
- **GitHub:** [GroupDocs GitHub रिपॉज़िटरी](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **फ़्री सपोर्ट:** [GroupDocs फ़ोरम](https://forum.groupdocs.com/c/redaction/33)  
- **अस्थायी लाइसेंस:** [अस्थायी लाइसेंस प्राप्त करें](https://purchase.groupdocs.com/temporary-license/)

```java
import com.groupdocs.redaction.Redactor;

// Initialize Redactor with the path to your document
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

## संबंधित ट्यूटोरियल
- [java फ़ाइल मेटाडेटा पढ़ें – GroupDocs.Redaction के साथ फ़ाइल प्रकार](/redaction/java/metadata-redaction/groupdocs-redaction-java-document-metadata-extraction/)
- [प्रिव्यू और दस्तावेज़ पेज काउंट जेनरेट करें – GroupDocs जावा](/redaction/java/document-information/)
- [GroupDocs.Redaction जावा के साथ पेज प्रिव्यू कैसे करें – एक व्यापक गाइड](/redaction/java/document-loading/load-preview-document-pages-groupdocs-redaction-java/)