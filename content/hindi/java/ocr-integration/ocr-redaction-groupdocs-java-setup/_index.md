---
date: '2026-06-26'
description: GroupDocs OCR Redaction को Azure OCR के साथ उपयोग करके स्कैन किए गए PDF
  से टेक्स्ट निकालना और संवेदनशील डेटा को मास्क करना सीखें। social security number
  को रिडैक्ट करें और PDF में confidential info को प्रभावी ढंग से बदलें।
keywords:
- extract text scanned pdf
- redact social security number
- mask sensitive data pdf
- replace confidential info pdf
schemas:
- author: GroupDocs
  dateModified: '2026-06-26'
  description: Learn how to extract text scanned PDF and mask sensitive data using
    GroupDocs OCR Redaction with Azure OCR. Redact social security number and replace
    confidential info PDF efficiently.
  headline: Extract Text Scanned PDF – Mask Data with GroupDocs OCR
  type: TechArticle
- questions:
  - answer: OCR redaction uses Optical Character Recognition to extract hidden text
      from images or scanned PDFs, then applies redaction rules to mask that text.
    question: What is OCR redaction?
  - answer: Yes, but OCR dramatically improves accuracy on scanned documents where
      native text extraction fails.
    question: Can I use GroupDocs Redaction without Azure OCR?
  - answer: Build and test them incrementally, using Java’s `Pattern` class in a sandbox
      before applying to large documents.
    question: How do I handle complex regex patterns?
  - answer: Large PDFs, overly complex regex, and synchronous OCR calls can slow processing;
      consider batch processing and optimized patterns.
    question: What are typical performance bottlenecks?
  - answer: Absolutely—reach out via the [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33)
      for community help or contact GroupDocs support.
    question: Is support available for implementation issues?
  type: FAQPage
title: स्कैन किए गए PDF से टेक्स्ट निकालें – GroupDocs OCR के साथ डेटा को मास्क करें
type: docs
url: /hi/java/ocr-integration/ocr-redaction-groupdocs-java-setup/
weight: 1
---

# स्कैन किए गए PDF से टेक्स्ट निकालें – GroupDocs OCR के साथ डेटा को मास्क करें

आज की डेटा‑ड्रिवन दुनिया में, **स्कैन किए गए PDF** फ़ाइलों से टेक्स्ट निकालना और गोपनीय जानकारी को मास्क करना एक अनिवार्य अनुपालन कदम है। यह ट्यूटोरियल आपको GroupDocs Redaction को Microsoft Azure OCR के साथ उपयोग करने के माध्यम से स्कैन किए गए पृष्ठों पर छिपा टेक्स्ट विश्वसनीय रूप से पहचानने और इसे **`[REDACTED]`** जैसे सुरक्षित प्लेसहोल्डर से बदलने की प्रक्रिया दिखाता है। आप देखेंगे कि यह संयोजन तेज़, सटीक और प्रोडक्शन‑ग्रेड वर्कलोड्स के लिए तैयार क्यों है।

## त्वरित उत्तर
- **“mask sensitive data” क्या मतलब है?** यह पहचाने गए गोपनीय टेक्स्ट को एक प्लेसहोल्डर (जैसे `[REDACTED]`) से बदल देता है।  
- **कौन लाइब्रेरी OCR संभालती है?** Microsoft Azure OCR कनेक्टर, जो GroupDocs Redaction के माध्यम से उपयोग किया जाता है।  
- **क्या मुझे लाइसेंस चाहिए?** मूल्यांकन के लिए एक मुफ्त ट्रायल काम करता है; प्रोडक्शन के लिए एक स्थायी लाइसेंस आवश्यक है।  
- **क्या मैं स्कैन किए गए PDFs को रिडैक्ट कर सकता हूँ?** हाँ—OCR छिपा टेक्स्ट निकालता है फिर रेगेक्स रिडैक्शन लागू करता है।  
- **क्या यह समाधान केवल Java के लिए है?** उदाहरण Java‑आधारित है, लेकिन GroupDocs .NET और अन्य प्लेटफ़ॉर्म के लिए समान APIs प्रदान करता है।

## OCR‑आधारित रिडैक्शन क्या है?
OCR‑आधारित रिडैक्शन पहले प्रत्येक पृष्ठ पर OCR चलाता है, छवियों को खोज योग्य टेक्स्ट में बदलता है, फिर रेगेक्स पैटर्न लागू करके मिलान को `[REDACTED]` जैसे मास्क से बदल देता है। यह दो‑चरणीय प्रक्रिया आपको स्कैन किए गए PDFs में भी व्यक्तिगत डेटा को विश्वसनीय रूप से छुपाने की अनुमति देती है, यह सुनिश्चित करते हुए कि कोई भी संवेदनशील स्ट्रिंग दस्तावेज़ को साझा या संग्रहित करने से पहले हटा दी जाए।

## Azure OCR के साथ GroupDocs Redaction क्यों उपयोग करें?
आपको Azure OCR के साथ GroupDocs Redaction का उपयोग करना चाहिए क्योंकि यह **प्रिंटेड टेक्स्ट पर >98 % OCR सटीकता** प्रदान करता है, **50+ इनपुट और आउटपुट फॉर्मेट** का समर्थन करता है, और **पूरे फ़ाइल को मेमोरी में लोड किए बिना कई‑सौ पृष्ठों वाले PDFs को प्रोसेस** कर सकता है, जिससे अनुपालन के लिए तेज़, स्केलेबल रिडैक्शन सुनिश्चित होता है। यह समाधान **8‑कोर सर्वर पर 2 मिनट से कम समय में 1,000‑पृष्ठ PDF को प्रोसेस करने के लिए स्केल** करता है, जिससे बैच जॉब्स व्यावहारिक बनते हैं।

## पूर्वापेक्षाएँ
- **Java Development Kit (JDK) 8+** स्थापित होना चाहिए।  
- **Maven** (यदि आप डिपेंडेंसी मैनेजमेंट पसंद करते हैं) या मैन्युअल रूप से JARs डाउनलोड करने की क्षमता।  
- **Microsoft Azure OCR क्रेडेंशियल्स** (एंडपॉइंट और सब्सक्रिप्शन की)।  
- बुनियादी Java ज्ञान और रेग्युलर एक्सप्रेशन की परिचितता।

## Java के लिए GroupDocs Redaction सेटअप करना

### Maven सेटअप
अपने `pom.xml` में GroupDocs रिपॉजिटरी और डिपेंडेंसी जोड़ें:

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
यदि आप मैन्युअल JAR प्रबंधन पसंद करते हैं, तो नवीनतम रिलीज़ [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) से प्राप्त करें।

### लाइसेंस प्राप्ति
- **Free Trial** – सभी फीचर्स को बिना लागत के एक्सप्लोर करें।  
- **Temporary License** – मूल्यांकन समय बढ़ाएँ।  
- **Full License** – प्रोडक्शन‑रेडी क्षमताओं को अनलॉक करें।

### बेसिक इनिशियलाइज़ेशन और सेटअप
`Redactor` क्लास वह कोर इंजन है जो OCR एक्सट्रैक्शन करता है और PDF दस्तावेज़ों पर रिडैक्शन नियम लागू करता है।  
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.RedactorSettings;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.examples.java.helper_classes.MicrosoftAzureOcrConnector;

// Initialize the OCR connector with Microsoft Azure
RedactorSettings settings = new RedactorSettings(new MicrosoftAzureOcrConnector());
```

## OCR रिडैक्शन के साथ संवेदनशील डेटा को कैसे मास्क करें
OCR रिडैक्शन के साथ संवेदनशील डेटा को मास्क करने में PDF को Azure OCR सेटिंग्स के साथ लोड करना, छिपाने के लिए डेटा के रेगेक्स पैटर्न को परिभाषित करना, और Redactor को बुलाकर प्रत्येक मिलान को `[REDACTED]` जैसे प्लेसहोल्डर से बदलना शामिल है। लाइब्रेरी एक ही वर्कफ़्लो में OCR, पैटर्न मैचिंग, और PDF रीराइटिंग को संभालती है।

### चरण 1: OCR सेटिंग्स के साथ दस्तावेज़ लोड करें
`LoadOptions` यह कॉन्फ़िगर करता है कि GroupDocs फ़ाइल को कैसे लोड करता है, जिससे आप Azure जैसे OCR कनेक्टर पास कर सकते हैं।  
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;

// Load your document with OCR settings
try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf", 
    new LoadOptions(), settings)) {
    // Further operations will go here
}
```
- **`YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf`** – इसे अपने PDF के पथ से बदलें।  
- **`settings`** – इसमें वह Azure OCR कनेक्टर है जो आपने पहले बनाया था।

### चरण 2: रेगेक्स रिडैक्शन को परिभाषित और लागू करें
`ReplacementOptions` वह प्रतिस्थापन टेक्स्ट निर्दिष्ट करता है जो रिडैक्शन के दौरान प्रत्येक रेगेक्स मिलान को बदल देगा।  
```java
import com.groupdocs.redaction.redactions.RegexRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

// Define the regex for sensitive data (e.g., Social Security Numbers)
RegexRedaction redaction = new RegexRedaction("\\b\\d{3}-\\d{2}-\\d{4}\\b", 
    new ReplacementOptions("[REDACTED]"));

// Apply redaction
redactor.apply(redaction);

// Save the document after redactions
redactor.save(new SaveOptions());
```
- पैटर्न `\b\d{3}-\d{2}-\d{4}\b` अमेरिकी सोशल सिक्योरिटी नंबर से मेल खाता है।  
- `ReplacementOptions("[REDACTED]")` प्रत्येक मिलान को मास्क से बदलता है, प्रभावी रूप से **संवेदनशील डेटा को मास्क** करता है।

## संवेदनशील डेटा को मास्क करने के सामान्य उपयोग केस
1. **Legal Document Management** – ड्राफ्ट साझा करने से पहले क्लाइंट पहचानकर्ता को छुपाएँ।  
2. **Financial Reporting** – खाता नंबर और ट्रांज़ैक्शन आईडी की सुरक्षा करें।  
3. **Healthcare Records** – HIPAA का पालन करने के लिए रोगी पहचानकर्ता को रिडैक्ट करें।  
4. **Government Publications** – सार्वजनिक रिकॉर्ड से व्यक्तिगत डेटा हटाएँ।  
5. **Corporate Contracts** – बाहरी समीक्षा के दौरान स्वामित्व शर्तों को छुपाएँ।

## प्रदर्शन टिप्स
- **रेगेक्स को ऑप्टिमाइज़ करें** – बहुत व्यापक पैटर्न से बचें जो प्रोसेसिंग समय बढ़ाते हैं; अच्छी तरह से तैयार अभिव्यक्तियाँ रनटाइम को 40 % तक कम कर सकती हैं।  
- **मेमोरी मैनेजमेंट** – `Redactor` इंस्टेंस को तुरंत बंद करें (try‑with‑resources इसे स्वतः करता है)।  
- **असिंक्रोनस एक्सीक्यूशन** – बड़े पैमाने पर प्रोसेसिंग के लिए, रिडैक्शन जॉब्स को अलग थ्रेड्स पर चलाएँ या UI को रिस्पॉन्सिव रखने के लिए टास्क क्यू का उपयोग करें।

## समस्या निवारण
- **Azure क्रेडेंशियल्स त्रुटि** – `MicrosoftAzureOcrConnector` में एंडपॉइंट URL और सब्सक्रिप्शन की को दोबारा जांचें।  
- **दस्तावेज़ लोड नहीं हो रहा** – फ़ाइल पथ सत्यापित करें और सुनिश्चित करें कि PDF पासवर्ड‑प्रोटेक्टेड नहीं है (या `LoadOptions` के माध्यम से पासवर्ड प्रदान करें)।  
- **कोई रिडैक्शन लागू नहीं हुआ** – पहले अपने रेगेक्स को सरल स्ट्रिंग से टेस्ट करें; मिलान की पुष्टि के लिए यूनिट टेस्ट में `Pattern.compile` का उपयोग करें।

## अक्सर पूछे जाने वाले प्रश्न

**प्रश्न: OCR रिडैक्शन क्या है?**  
**उत्तर:** OCR रिडैक्शन ऑप्टिकल कैरेक्टर रिकग्निशन का उपयोग करके छवियों या स्कैन किए गए PDFs से छिपा टेक्स्ट निकालता है, फिर उस टेक्स्ट को मास्क करने के लिए रिडैक्शन नियम लागू करता है।

**प्रश्न: क्या मैं Azure OCR के बिना GroupDocs Redaction उपयोग कर सकता हूँ?**  
**उत्तर:** हाँ, लेकिन OCR स्कैन किए गए दस्तावेज़ों में जहाँ मूल टेक्स्ट एक्सट्रैक्शन विफल होता है, सटीकता को काफी बढ़ाता है।

**प्रश्न: जटिल रेगेक्स पैटर्न को कैसे संभालूँ?**  
**उत्तर:** उन्हें क्रमिक रूप से बनाएँ और टेस्ट करें, बड़े दस्तावेज़ों पर लागू करने से पहले सैंडबॉक्स में Java के `Pattern` क्लास का उपयोग करें।

**प्रश्न: सामान्य प्रदर्शन बाधाएँ क्या हैं?**  
**उत्तर:** बड़े PDFs, अत्यधिक जटिल रेगेक्स, और सिंक्रोनस OCR कॉल प्रोसेसिंग को धीमा कर सकते हैं; बैच प्रोसेसिंग और ऑप्टिमाइज़्ड पैटर्न पर विचार करें।

**प्रश्न: कार्यान्वयन समस्याओं के लिए समर्थन उपलब्ध है?**  
**उत्तर:** बिल्कुल—समुदाय सहायता के लिए [GroupDocs फोरम](https://forum.groupdocs.com/c/redaction/33) पर संपर्क करें या GroupDocs समर्थन से जुड़ें।

## अतिरिक्त संसाधन
- **डॉक्यूमेंटेशन**: https://docs.groupdocs.com/redaction/java/  
- **API रेफ़रेंस**: https://reference.groupdocs.com/redaction/java  
- **डाउनलोड**: https://releases.groupdocs.com/redaction/java/  
- **GitHub**: https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java  
- **फ्री सपोर्ट**: https://forum.groupdocs.com/c/redaction/33  
- **टेम्पररी लाइसेंस**: https://purchase.groupdocs.com/temporary-license/

---

**अंतिम अपडेट:** 2026-06-26  
**परीक्षित संस्करण:** GroupDocs.Redaction 24.9 (Java)  
**लेखक:** GroupDocs  

## संबंधित ट्यूटोरियल्स

- [OCR का उपयोग करके सुरक्षित PDF रिडैक्शन – GroupDocs.Redaction Java](/redaction/java/ocr-integration/)
- [GroupDocs.Redaction for Java के साथ टेक्स्ट को रिडैक्ट कैसे करें](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction/)
- [Java में संवेदनशील डेटा को मास्क करें – GroupDocs.Redaction के साथ व्यक्तिगत जानकारी को रिडैक्ट करें](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)