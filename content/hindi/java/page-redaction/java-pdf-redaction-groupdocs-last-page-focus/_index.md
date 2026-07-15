---
date: '2026-04-20'
description: GroupDocs.Redaction for Java का उपयोग करके अंतिम पृष्ठ PDF को कैसे रेडैक्ट
  करें, PDF में टेक्स्ट को बदलें और संवेदनशील डेटा को कुशलतापूर्वक छुपाएँ।
keywords:
- redact last page pdf
- replace text pdf java
- hide sensitive data pdf
title: GroupDocs.Redaction for Java का उपयोग करके PDF के अंतिम पृष्ठ को रीडैक्ट करें
type: docs
url: /hi/java/page-redaction/java-pdf-redaction-groupdocs-last-page-focus/
weight: 1
---

# PDF की अंतिम पृष्ठ को रिडैक्ट करें GroupDocs.Redaction for Java के साथ

आज के डिजिटल परिदृश्य में, **redact last page pdf** फ़ाइलें गोपनीय जानकारी की सुरक्षा और गोपनीयता नियमों का पालन करने के लिए आवश्यक हैं। यह ट्यूटोरियल आपको GroupDocs.Redaction for Java का उपयोग करके PDF के अंतिम पृष्ठ को लक्षित करने और विशिष्ट क्षेत्रों में संवेदनशील डेटा को छिपाने की प्रक्रिया दिखाता है। अंत तक, आप टेक्स्ट pdf java शैली को बदलने और जहाँ भी आवश्यक हो, संवेदनशील डेटा pdf को आत्मविश्वास से छिपाने में सक्षम होंगे।

## त्वरित उत्तर
- **मुख्य लक्ष्य क्या है?** PDF के अंतिम पृष्ठ और उसके भीतर के विशिष्ट क्षेत्रों को रिडैक्ट करना।  
- **कौनसी लाइब्रेरी उपयोग की गई है?** GroupDocs.Redaction for Java।  
- **क्या मुझे लाइसेंस की आवश्यकता है?** परीक्षण के लिए ट्रायल या टेम्पररी लाइसेंस काम करता है; उत्पादन के लिए पूर्ण लाइसेंस आवश्यक है।  
- **कौनसा Java संस्करण आवश्यक है?** Maven समर्थन के साथ Java 8 या उससे ऊपर।  
- **क्या मैं अन्य पृष्ठों को लक्षित कर सकता हूँ?** हाँ, वही फ़िल्टर किसी भी पृष्ठ रेंज के लिए समायोजित किए जा सकते हैं।

## PDF को रिडैक्ट करना क्या है?
Redaction का अर्थ है PDF से सामग्री को स्थायी रूप से हटाना या अस्पष्ट करना ताकि उसे पुनः प्राप्त नहीं किया जा सके। जब आप **redact last page pdf** करते हैं, तो आप सुनिश्चित करते हैं कि अंतिम पृष्ठ पर कोई भी गोपनीय जानकारी पूरी तरह से छिपी रहे।

## GroupDocs.Redaction for Java का उपयोग क्यों करें?
GroupDocs.Redaction पेज‑रेंज, एरिया‑बेस्ड और टेक्स्ट‑बेस्ड जैसे समृद्ध फ़िल्टर सेट प्रदान करता है, जिससे आप सटीक रूप से नियंत्रित कर सकते हैं कि क्या हटाया जाए। यह विशेष रूप से उपयोगी है:

- **Replacing text pdf java** शैली को दस्तावेज़ के बाकी हिस्से को बदले बिना बदलना।  
- **Hiding sensitive data pdf** जैसे व्यक्तिगत पहचानकर्ता, वित्तीय आंकड़े, या कानूनी क्लॉज़।  
- बड़े दस्तावेज़ बैचों में अनुपालन जांच को स्वचालित करना।

## पूर्वापेक्षाएँ
- **Java Development Kit (JDK) 8+** स्थापित है।  
- **Maven** निर्भरता प्रबंधन के लिए।  
- **GroupDocs.Redaction** लाइसेंस तक पहुँच (ट्रायल, टेम्पररी, या खरीदा हुआ)।  

## GroupDocs.Redaction for Java की सेटअप

### Maven सेटअप
अपने `pom.xml` में रिपॉज़िटरी और डिपेंडेंसी जोड़ें:

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
यदि आप Maven का उपयोग नहीं करना चाहते, तो आधिकारिक साइट से नवीनतम JAR प्राप्त करें: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/)।

#### लाइसेंस प्राप्ति चरण
- **Free Trial:** बिना प्रतिबद्धता के सभी फीचर परीक्षण करें।  
- **Temporary License:** अल्पकालिक प्रोजेक्ट या मूल्यांकन के लिए उपयोग करें।  
- **Purchase:** असीमित उपयोग और प्राथमिकता समर्थन अनलॉक करें।

## बुनियादी प्रारंभिककरण
सबसे पहले, एक `Redactor` इंस्टेंस बनाएं जो आपके PDF फ़ाइल की ओर संकेत करता हो:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_PDF");
```

यह ऑब्जेक्ट सभी रिडैक्शन ऑपरेशनों का प्रवेश बिंदु है।

## PDF की अंतिम पृष्ठ को रिडैक्ट करने के चरण‑दर‑चरण मार्गदर्शक

### फीचर 1: अंतिम पृष्ठ पर विशिष्ट क्षेत्रों को रिडैक्ट करना

#### चरण 1: PDF दस्तावेज़ लोड करें
```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_PDF");
```

#### चरण 2: पृष्ठ जानकारी प्राप्त करें
```java
IDocumentInfo info = redactor.getDocumentInfo();
PageInfo lastPage = info.getPages().get(info.getPageCount() - 1);
```
अंतिम पृष्ठ के आयाम जानने से आप सटीक निर्देशांक निर्धारित कर सकते हैं।

#### चरण 3: प्रतिस्थापन विकल्प निर्धारित करें
```java
ReplacementOptions options = new ReplacementOptions("[secret]");
```
यहाँ हम वह प्लेसहोल्डर टेक्स्ट चुनते हैं जो रिडैक्टेड सामग्री को बदल देगा।

#### चरण 4: लक्षित रिडैक्शन के लिए फ़िल्टर सेट करें
```java
options.setFilters(new RedactionFilter[] {
    new PageRangeFilter(PageSeekOrigin.End, 0, 1),
    new PageAreaFilter(
        new java.awt.Point(0, lastPage.getHeight() / 2),
        new java.awt.Dimension(lastPage.getWidth(), lastPage.getHeight() / 2)
    )
});
```
- `PageRangeFilter` **last page** को चुनता है।  
- `PageAreaFilter` उस पृष्ठ के निचले आधे हिस्से तक ऑपरेशन को सीमित करता है।

#### चरण 5: रिडैक्शन लागू करें (replace text pdf java)
```java
RedactorChangeLog result = redactor.apply(new ExactPhraseRedaction("bibliography", false, options));
```
वाक्यांश “bibliography” को केवल निर्धारित क्षेत्र के भीतर “[secret]” से बदल दिया जाता है।

#### चरण 6: सफलता की पुष्टि करें और सहेजें
```java
if (result.getStatus() != RedactionStatus.Failed) {
    redactor.save("YOUR_OUTPUT_DIRECTORY/redacted_output.pdf");
}
```
आउटपुट फ़ाइल लिखने से पहले हमेशा स्थिति जाँचें।

#### चरण 7: संसाधनों को साफ़ करें
```java
redactor.close();
```
`Redactor` को बंद करने से मेमोरी और फ़ाइल हैंडल मुक्त हो जाते हैं।

### फीचर 2: रिडैक्शन के लिए पृष्ठ रेंज फ़िल्टरिंग

#### चरण 1: PDF दस्तावेज़ लोड करें
```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_PDF");
```

#### चरण 2: दस्तावेज़ जानकारी तक पहुँचें
```java
IDocumentInfo info = redactor.getDocumentInfo();
```

#### चरण 3: पृष्ठ रेंज फ़िल्टर बनाएं (hide sensitive data pdf)
```java
PageRangeFilter pageRangeFilter = new PageRangeFilter(PageSeekOrigin.End, 0, 1);
```
यह फ़िल्टर अंतिम पृष्ठ को अलग करता है, जिससे आप आवश्यक कोई भी रिडैक्शन लॉजिक लागू कर सकते हैं।

### फीचर 3: PDF पृष्ठों पर एरिया‑बेस्ड रिडैक्शन

#### चरण 1: PDF दस्तावेज़ लोड करें
```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_PDF");
```

#### चरण 2: पृष्ठ विवरण प्राप्त करें
```java
IDocumentInfo info = redactor.getDocumentInfo();
PageInfo lastPage = info.getPages().get(info.getPageCount() - 1);
```

#### चरण 3: एरिया फ़िल्टर निर्धारित करें (hide sensitive data pdf)
```java
PageAreaFilter areaFilter = new PageAreaFilter(
    new java.awt.Point(0, lastPage.getHeight() / 2),
    new java.awt.Dimension(lastPage.getWidth(), lastPage.getHeight() / 2)
);
```
फ़िल्टर अंतिम पृष्ठ के निचले आधे हिस्से को लक्षित करता है—फ़ूटर या सिग्नेचर हटाने के लिए आदर्श।

#### चरण 4: संसाधन मुक्त करें
```java
redactor.close();
```

## व्यावहारिक अनुप्रयोग
- **Legal Documents:** अंतिम पृष्ठ पर क्लाइंट नाम या केस नंबर को साझा करने से पहले रिडैक्ट करें।  
- **Financial Reports:** खाता नंबर या गोपनीय सारांश को छुपाएँ।  
- **Healthcare Records:** HIPAA के अनुरूप रोगी पहचानकर्ता हटाएँ।  
- **Pre‑Release Drafts:** अभी समीक्षा में मौजूद अनुभागों को छुपाएँ।

## प्रदर्शन सुझाव
- **Reuse the `Redactor`** जब आप बैच में कई PDFs प्रोसेस कर रहे हों।  
- **Close the object promptly** मेमोरी लीक से बचने के लिए, विशेषकर बड़े फ़ाइलों के साथ।  
- **Test on a sample** उत्पादन दस्तावेज़ों पर चलाने से पहले फ़िल्टर निर्देशांक की पुष्टि करने के लिए।

## अक्सर पूछे जाने वाले प्रश्न

**Q: क्या मैं एक साथ कई पृष्ठों को रिडैक्ट कर सकता हूँ?**  
A: हाँ। `PageRangeFilter` पैरामीटर को समायोजित करके किसी भी रेंज (उदाहरण के लिए `new PageRangeFilter(1, 5)` पृष्ठ 1‑5 के लिए) शामिल कर सकते हैं।

**Q: क्या लाइब्रेरी पासवर्ड‑प्रोटेक्टेड PDFs का समर्थन करती है?**  
A: बिल्कुल। एन्क्रिप्टेड फ़ाइलें खोलने के लिए पासवर्ड को `Redactor` कंस्ट्रक्टर में पास करें।

**Q: रिडैक्शन का रंग या ओवरले कैसे बदलूँ?**  
A: कस्टम इमेज, रंग, या टेक्स्ट ओवरले निर्दिष्ट करने के लिए `ReplacementOptions` का उपयोग करें।

**Q: क्या रिडैक्शन स्थायी है?**  
A: हाँ। हटाई गई सामग्री आउटपुट PDF में कहीं भी संग्रहीत नहीं रहती, जिससे वह पुनः प्राप्त नहीं की जा सकती।

**Q: यदि मुझे regex पैटर्न के आधार पर रिडैक्ट करना हो तो क्या करें?**  
A: GroupDocs.Redaction `RegexRedaction` प्रदान करता है, जो `ExactPhraseRedaction` के समान कार्य करता है।

---

**अंतिम अद्यतन:** 2026-04-20  
**Tested With:** GroupDocs.Redaction 24.9 for Java  
**Author:** GroupDocs