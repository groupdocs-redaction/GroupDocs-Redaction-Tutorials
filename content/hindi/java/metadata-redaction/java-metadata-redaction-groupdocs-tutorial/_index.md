---
date: '2026-09-26'
description: GroupDocs के साथ Java में मेटाडेटा को रिडैक्ट करना सीखें, गोपनीय दस्तावेज़
  मेटाडेटा को सुरक्षित रूप से हटाते हुए मूल फ़ॉर्मेट को अपरिवर्तित रखें।
keywords:
- how to redact metadata
- GroupDocs Redaction Java
- secure document processing
- metadata removal Java
lastmod: '2026-09-26'
og_description: GroupDocs के साथ Java में मेटाडेटा को रिडैक्ट करने का तरीका – एक चरण‑दर‑चरण
  गाइड जो आपको सुरक्षित रूप से गोपनीय दस्तावेज़ मेटाडेटा हटाने और मूल फ़ॉर्मेट को
  बनाए रखने का दिखाता है।
og_image_alt: Guide showing metadata redaction using GroupDocs in Java
og_title: GroupDocs के साथ Java में मेटाडेटा को कैसे रिडैक्ट करें
schemas:
- author: GroupDocs
  dateModified: '2026-09-26'
  description: Learn how to redact metadata with GroupDocs in Java, securely removing
    confidential document metadata while keeping the original format intact.
  headline: How to redact metadata with GroupDocs in Java
  type: TechArticle
- description: Learn how to redact metadata with GroupDocs in Java, securely removing
    confidential document metadata while keeping the original format intact.
  name: How to redact metadata with GroupDocs in Java
  steps:
  - name: import necessary classes
    text: These imports give you access to the redaction engine, save options, and
      metadata utilities.
  - name: initialize redactor
    text: Instantiate the `Redactor` with the path to your source file.
  - name: configure metadata search and redaction
    text: Create a `MetadataSearchRedaction` that looks for the exact string **"Company
      Ltd."** and replaces it with **"--company--"**. The `setFilter` call limits
      the operation to the *Company* metadata field only.
  - name: apply the redaction
    text: Run the redaction against the opened document.
  - name: save with custom options
    text: '`SaveOptions` allows you to specify output format, file naming, and other
      saving parameters for the redacted document. Configure `SaveOptions` so the
      redacted file gets a “_Redacted” suffix while preserving its original format.'
  - name: release resources
    text: Always close the `Redactor` to free native resources and avoid memory leaks.
  type: HowTo
- questions:
  - answer: It’s a powerful library that enables you to redact text, metadata, and
      images in documents using Java applications.
    question: What is GroupDocs.Redaction for Java?
  - answer: Yes, but with limitations. A free trial or temporary license allows full
      access for testing purposes.
    question: Can I use GroupDocs.Redaction without purchasing a license?
  - answer: Use `SaveOptions` to specify your requirements, such as avoiding rasterization
      when saving to PDF.
    question: How do I ensure document formats are preserved during redaction?
  - answer: It supports a wide range, including Word, Excel, PowerPoint, PDF, and
      many more.
    question: What types of documents can be redacted using GroupDocs.Redaction?
  - answer: Visit the [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33)
      for assistance.
    question: Where can I find support if I run into issues?
  type: FAQPage
tags:
- metadata redaction
- GroupDocs
- Java document security
- redaction tutorial
title: GroupDocs के साथ Java में मेटाडेटा को कैसे रिडैक्ट करें
type: docs
url: /hi/java/metadata-redaction/java-metadata-redaction-groupdocs-tutorial/
weight: 1
---

# GroupDocs के साथ Java में मेटाडेटा को कैसे रेडैक्ट करें

इस व्यापक ट्यूटोरियल में आप GroupDocs.Redaction for Java का उपयोग करके Word, PDF और कई अन्य दस्तावेज़ प्रकारों से **मेटाडेटा को कैसे रेडैक्ट करें** सीखेंगे। गाइड के अंत तक आप किसी भी Java‑आधारित सेवा में मेटाडेटा रेडैक्शन को एम्बेड कर सकेंगे, जिससे कंपनी के नाम, लेखक, या कस्टम प्रॉपर्टीज़ जैसी गोपनीय जानकारी आपके संगठन से बाहर नहीं जाएगी।

## त्वरित उत्तर
- **MetadataSearchRedaction क्या करता है?** यह विशिष्ट मेटाडेटा फ़ील्ड्स को खोजता है और उनके मानों को कस्टम टेक्स्ट से बदल देता है।  
- **कौन सी लाइब्रेरी आवश्यक है?** GroupDocs.Redaction for Java (v24.9 या नया)।  
- **क्या मुझे लाइसेंस चाहिए?** मूल्यांकन के लिए एक मुफ्त ट्रायल काम करता है; उत्पादन के लिए पूर्ण लाइसेंस आवश्यक है।  
- **क्या मैं मूल फ़ाइल फ़ॉर्मेट रख सकता हूँ?** हाँ—`SaveOptions` का उपयोग करके मूल फ़ॉर्मेट को संरक्षित रखें।  
- **क्या यह तरीका थ्रेड‑सेफ़ है?** प्रत्येक `Redactor` इंस्टेंस स्वतंत्र है, इसलिए आप दस्तावेज़ों को समानांतर में प्रोसेस कर सकते हैं।

## GroupDocs के साथ मेटाडेटा को कैसे रेडैक्ट करें?
`Redactor` वह मुख्य क्लास है जो दस्तावेज़ को लोड करता है और रेडैक्शन ऑपरेशन्स प्रदान करता है।  
`Redactor` इंस्टेंस के साथ अपने स्रोत दस्तावेज़ को लोड करें, एक `MetadataSearchRedaction` कॉन्फ़िगर करें जो उस सटीक मेटाडेटा कुंजी को लक्षित करता है जिसे आप साफ़ करना चाहते हैं, रेडैक्शन लागू करें, और अंत में `SaveOptions` का उपयोग करके फ़ाइल को सहेजें। यह पूरा वर्कफ़्लो कुछ ही लाइनों में व्यक्त किया जा सकता है और किसी भी समर्थित फ़ॉर्मेट, DOCX से PDF और उससे आगे, के लिए काम करता है।

## GroupDocs के साथ मेटाडेटा रेडैक्शन क्या है?
`MetadataSearchRedaction` एक विशेषीकृत क्लास है जो आपको किसी विशेष मेटाडेटा प्रॉपर्टी (जैसे *Company*, *Author*) को लक्षित करने और उसकी सामग्री को एक प्लेसहोल्डर से बदलने की अनुमति देता है। यह तब आदर्श है जब आपको बाहरी साझेदारों के साथ दस्तावेज़ साझा करने से पहले कॉर्पोरेट डेटा को अनाम बनाना हो। रेडैक्शन प्रक्रिया अन्य दस्तावेज़ तत्वों को नहीं बदलती, जिससे मेटाडेटा हटाने के बाद भी दृश्य लेआउट और सामग्री अपरिवर्तित रहती है।

## GroupDocs के साथ मेटाडेटा रेडैक्शन क्यों उपयोग करें?
GroupDocs के साथ मेटाडेटा रेडैक्शन दस्तावेज़ों से संवेदनशील जानकारी को हटाने का एक विश्वसनीय तरीका प्रदान करता है, जबकि उनके मूल स्वरूप और संरचना को बनाए रखता है। मेटाडेटा फ़ील्ड्स पर ध्यान केंद्रित करके, आप दृश्य सामग्री को बदले बिना या आकस्मिक डेटा लीक के जोखिम के बिना जल्दी से गोपनीयता मानकों का पालन कर सकते हैं।

- **सटीकता** – केवल उन फ़ील्ड्स को रेडैक्ट करें जिन्हें आप निर्दिष्ट करते हैं, दस्तावेज़ के बाकी हिस्से को अनछुआ छोड़ते हुए।  
- **अनुपालन** – छिपे हुए पहचानकर्ताओं को हटाकर GDPR, HIPAA, और अन्य गोपनीयता नियमों को पूरा करने में मदद करता है।  
- **ऑटोमेशन‑तैयार** – बैच प्रोसेसिंग पाइपलाइन या माइक्रो‑सर्विसेज़ में सहजता से फिट होता है।  
- **विस्तृत फ़ॉर्मेट समर्थन** – GroupDocs.Redaction **50+ इनपुट और आउटपुट फ़ॉर्मेट** (जैसे DOCX, PDF, PPTX, XLSX, और इमेज टाइप्स) का समर्थन करता है और पूरी दस्तावेज़ को मेमोरी में लोड किए बिना सैकड़ों पृष्ठों वाली फ़ाइलों को प्रोसेस कर सकता है।

## पूर्वापेक्षाएँ
- **GroupDocs.Redaction for Java** ≥ 24.9।  
- आपके मशीन पर Java 8 या नया स्थापित होना चाहिए।  
- IntelliJ IDEA या Eclipse जैसे IDE (वैकल्पिक लेकिन अनुशंसित)।  
- Maven की बुनियादी जानकारी (या मैन्युअल रूप से JAR जोड़ने की क्षमता)।

## GroupDocs.Redaction for Java सेटअप करना

`pom.xml` में रिपॉज़िटरी और डिपेंडेंसी जोड़ें। यह चरण सुनिश्चित करता है कि Maven लाइब्रेरी को स्वचालित रूप से डाउनलोड कर सके।

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

*वैकल्पिक रूप से, आप आधिकारिक रिलीज़ पेज से सीधे JAR डाउनलोड कर सकते हैं:*  
[GroupDocs.Redaction for Java रिलीज़](https://releases.groupdocs.com/redaction/java/)

### लाइसेंस प्राप्त करना
- **फ्री ट्रायल** – सभी फीचर को एक्सप्लोर करने के लिए ट्रायल लाइसेंस डाउनलोड करें।  
- **टेम्पररी लाइसेंस** – विस्तारित परीक्षण के लिए उपयोग करें।  
- **पूर्ण लाइसेंस** – प्रोडक्शन डिप्लॉयमेंट के लिए आवश्यक।

## बेसिक इनिशियलाइज़ेशन
`Redactor` एक दस्तावेज़ को लोड करता है और विभिन्न रेडैक्शन लागू करने के लिए मेथड्स प्रदान करता है।  
उस दस्तावेज़ की ओर इशारा करने वाला `Redactor` इंस्टेंस बनाएं जिसे आप प्रोसेस करना चाहते हैं।

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

## इम्प्लीमेंटेशन गाइड

### चरण 1: आवश्यक क्लासेस इम्पोर्ट करें
ये इम्पोर्ट्स आपको रेडैक्शन इंजन, सेव ऑप्शन्स, और मेटाडेटा यूटिलिटीज़ तक पहुंच प्रदान करते हैं।

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.redactions.MetadataFilters;
import com.groupdocs.redaction.redactions.MetadataSearchRedaction;
```

### चरण 2: रेडैक्टर को इनिशियलाइज़ करें
`Redactor` को अपने स्रोत फ़ाइल के पाथ के साथ इंस्टैंशिएट करें।

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

### चरण 3: मेटाडेटा सर्च और रेडैक्शन कॉन्फ़िगर करें
एक `MetadataSearchRedaction` बनाएं जो सटीक स्ट्रिंग **"Company Ltd."** को खोजे और उसे **"--company--"** से बदल दे। `setFilter` कॉल ऑपरेशन को केवल *Company* मेटाडेटा फ़ील्ड तक सीमित करता है।

```java
MetadataSearchRedaction redaction = new MetadataSearchRedaction("Company Ltd.", "--company--");
redaction.setFilter(MetadataFilters.Company);
```

### चरण 4: रेडैक्शन लागू करें
खुले हुए दस्तावेज़ पर रेडैक्शन चलाएँ।

```java
redactor.apply(redaction);
```

### चरण 5: कस्टम ऑप्शन्स के साथ सेव करें
`SaveOptions` आपको रेडैक्टेड दस्तावेज़ के लिए आउटपुट फ़ॉर्मेट, फ़ाइल नामकरण, और अन्य सेव पैरामीटर्स निर्दिष्ट करने की अनुमति देता है।  
`SaveOptions` को इस प्रकार कॉन्फ़िगर करें कि रेडैक्टेड फ़ाइल को “_Redacted” सफ़िक्स मिले और मूल फ़ॉर्मेट बना रहे।

```java
SaveOptions tmp0 = new SaveOptions();
tmp0.setAddSuffix(true);  // Adds "_Redacted" to file name
tmp0.setRasterizeToPDF(false);  // Keeps original format

redactor.save(tmp0);
```

### चरण 6: रिसोर्सेज़ रिलीज़ करें
नेटीव रिसोर्सेज़ को मुक्त करने और मेमोरी लीक से बचने के लिए हमेशा `Redactor` को बंद करें।

```java
finally {
    redactor.close();
}
```

## सामान्य समस्याएँ और समाधान
- **FileNotFoundException** – `Redactor` को पास किए गए पाथ को दोबारा जांचें। विश्वसनीयता के लिए एब्सोल्यूट पाथ या `Paths.get(...)` का उपयोग करें।  
- **कोई बदलाव नहीं दिख रहा** – सुनिश्चित करें कि आप जिस मेटाडेटा फ़ील्ड को लक्षित कर रहे हैं उसमें वास्तव में खोज स्ट्रिंग मौजूद है; मेटाडेटा डिफ़ॉल्ट रूप से केस‑सेंसिटिव होता है।  
- **बड़े फ़ाइलों पर मेमोरी समाप्ति त्रुटियाँ** – दस्तावेज़ों को छोटे बैच में प्रोसेस करें और प्रत्येक फ़ाइल के बाद तुरंत `redactor.close()` कॉल करें।

## व्यावहारिक अनुप्रयोग
1. **कानूनी दस्तावेज़ीकरण** – थर्ड पार्टी को कॉन्ट्रैक्ट भेजने से पहले क्लाइंट कंपनी के नाम हटाएँ।  
2. **वित्तीय रिपोर्टिंग** – ऑडिट फ़ाइलों में आंतरिक पहचानकर्ताओं को अनाम बनाएं।  
3. **सहयोगी प्रोजेक्ट्स** – बाहरी विक्रेताओं के साथ ड्राफ्ट साझा करते समय स्वामित्व वाली जानकारी की सुरक्षा करें।

## प्रदर्शन संबंधी विचार
- **मेमोरी प्रबंधन** – लाइब्रेरी पूरे दस्तावेज़ को मेमोरी में रखती है; प्रत्येक फ़ाइल के बाद `Redactor` को बंद करना आवश्यक है।  
- **बैच प्रोसेसिंग** – हाई‑वॉल्यूम परिदृश्यों के लिए, फ़ाइलों के संग्रह पर लूप करें और एक ही `SaveOptions` इंस्टेंस को पुन: उपयोग करें।  
- **अपडेटेड रहें** – नई रिलीज़ में प्रदर्शन सुधार और बग फिक्सेस होते हैं; हमेशा नवीनतम स्थिर संस्करण को लक्ष्य रखें।

## अक्सर पूछे जाने वाले प्रश्न

**Q: GroupDocs.Redaction for Java क्या है?**  
A: यह एक शक्तिशाली लाइब्रेरी है जो आपको Java एप्लिकेशन का उपयोग करके दस्तावेज़ों में टेक्स्ट, मेटाडेटा और इमेजेज़ को रेडैक्ट करने में सक्षम बनाती है।

**Q: क्या मैं लाइसेंस खरीदे बिना GroupDocs.Redaction का उपयोग कर सकता हूँ?**  
A: हाँ, लेकिन सीमाओं के साथ। एक फ्री ट्रायल या टेम्पररी लाइसेंस परीक्षण उद्देश्यों के लिए पूरी पहुंच प्रदान करता है।

**Q: रेडैक्शन के दौरान दस्तावेज़ फ़ॉर्मेट को कैसे संरक्षित रखूँ?**  
A: `SaveOptions` का उपयोग करके अपनी आवश्यकताओं को निर्दिष्ट करें, जैसे PDF में सेव करते समय रास्टराइज़ेशन से बचना।

**Q: GroupDocs.Redaction का उपयोग करके किन प्रकार के दस्तावेज़ों को रेडैक्ट किया जा सकता है?**  
A: यह Word, Excel, PowerPoint, PDF और कई अन्य सहित व्यापक रेंज का समर्थन करता है।

**Q: यदि मुझे समस्याएँ आती हैं तो मैं समर्थन कहाँ पा सकता हूँ?**  
A: सहायता के लिए [GroupDocs सपोर्ट फ़ोरम](https://forum.groupdocs.com/c/redaction/33) पर जाएँ।

**Q: क्या MetadataSearchRedaction एन्क्रिप्टेड दस्तावेज़ों के साथ काम करता है?**  
A: हाँ। उपयुक्त पासवर्ड के साथ `Redactor` कन्स्ट्रक्टर का उपयोग करके दस्तावेज़ लोड करें जो पासवर्ड पैरामीटर स्वीकार करता है।

**Q: क्या मैं एक ही रन में कई मेटाडेटा रेडैक्शन को चेन कर सकता हूँ?**  
A: बिल्कुल। कई `MetadataSearchRedaction` ऑब्जेक्ट बनाएं, विभिन्न फ़िल्टर सेट करें, और सहेजने से पहले क्रमिक रूप से लागू करें।

**Q: क्या सेव करने से पहले रेडैक्शन का प्रीव्यू देखना संभव है?**  
A: आप `redactor.getRedactions()` को कॉल करके पेंडिंग रेडैक्शन की सूची प्राप्त कर सकते हैं और उन्हें प्रोग्रामेटिकली निरीक्षण कर सकते हैं।

## अतिरिक्त संसाधन
- **डॉक्यूमेंटेशन**: विस्तृत गाइड्स के लिए देखें [GroupDocs डॉक्यूमेंटेशन](https://docs.groupdocs.com/redaction/java/)।  
- **API रेफ़रेंस**: पूरी API रेफ़रेंस के लिए देखें [GroupDocs API रेफ़रेंस](https://reference.groupdocs.com/redaction/java)।  
- **लाइब्रेरी डाउनलोड**: नवीनतम रिलीज़ के लिए देखें [GroupDocs डाउनलोड्स](https://releases.groupdocs.com/redaction/java/)।  
- **सोर्स कोड**: देखें और योगदान दें [GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)।  
- **सपोर्ट**: मुफ्त सपोर्ट चैनल के माध्यम से मदद प्राप्त करें [GroupDocs सपोर्ट फ़ोरम](https://forum.groupdocs.com/c/redaction/33)।

---

**अंतिम अपडेट:** 2026-09-26  
**परीक्षित संस्करण:** GroupDocs.Redaction 24.9 for Java  
**लेखक:** GroupDocs

## संबंधित ट्यूटोरियल

- [Groupdocs Redaction Java दस्तावेज़ मेटाडेटा एक्सट्रैक्शन](/redaction/java/metadata-redaction/groupdocs-redaction-java-document-metadata-extraction/)
- [metadata टेक्स्ट जावा बदलें – GroupDocs के साथ सुरक्षित रेडैक्शन](/redaction/java/metadata-redaction/java-redaction-metadata-text-replacement-guide/)
- [Groupdocs Redaction Java का उपयोग करके दस्तावेज़ जानकारी प्राप्त करें](/redaction/java/document-information/retrieve-document-info-using-groupdocs-redaction-java/)