---
date: '2026-06-01'
description: GroupDocs.Redaction for Java के साथ अंतिम PDF पृष्ठ को हटाने का तरीका
  जानें। चरण‑दर‑चरण मार्गदर्शिका, कोड स्निपेट्स, और pdf page count java तथा अंतिम
  PDF पृष्ठ हटाने के लिए सर्वोत्तम प्रथाएँ।
keywords:
- delete last pdf page
- pdf page count java
- remove final pdf page
schemas:
- author: GroupDocs
  dateModified: '2026-06-01'
  description: Learn how to delete the last PDF page with GroupDocs.Redaction for
    Java. Step‑by‑step guide, code snippets, and best practices for pdf page count
    java and remove final pdf page.
  headline: How to Delete the Last PDF Page Using GroupDocs.Redaction in Java
  type: TechArticle
- description: Learn how to delete the last PDF page with GroupDocs.Redaction for
    Java. Step‑by‑step guide, code snippets, and best practices for pdf page count
    java and remove final pdf page.
  name: How to Delete the Last PDF Page Using GroupDocs.Redaction in Java
  steps:
  - name: '**Maven Setup**'
    text: '**Maven Setup**'
  - name: '**Direct Download**'
    text: '**Direct Download**'
  - name: '**Maven Configuration**'
    text: '**Maven Configuration**'
  - name: '**Direct Download Setup**'
    text: '**Direct Download Setup**'
  - name: '**Pre‑Publication Editing** – Remove draft or placeholder pages before
      releasing a report.'
    text: '**Pre‑Publication Editing** – Remove draft or placeholder pages before
      releasing a report.'
  - name: '**Archival Optimization** – Trim trailing blank pages to reduce storage
      costs for large document archives.'
    text: '**Archival Optimization** – Trim trailing blank pages to reduce storage
      costs for large document archives.'
  - name: '**Confidentiality** – Strip out a cover page that contains sensitive metadata
      before distribution.'
    text: '**Confidentiality** – Strip out a cover page that contains sensitive metadata
      before distribution.'
  - name: '**Automated Report Generation** – Generate PDFs programmatically and drop
      the automatically added summary page.'
    text: '**Automated Report Generation** – Generate PDFs programmatically and drop
      the automatically added summary page.'
  - name: '**Workflow Integration** – Embed the deletion step into CI/CD pipelines
      that handle document generation.'
    text: '**Workflow Integration** – Embed the deletion step into CI/CD pipelines
      that handle document generation.'
  type: HowTo
- questions:
  - answer: It provides a programmatic way to redact, edit, and manipulate sensitive
      content in PDFs and many other document formats without needing Microsoft Office
      installed.
    question: What is the primary use case for GroupDocs.Redaction?
  - answer: Yes—use `RemovePageRedaction` with a range (e.g., `new RemovePageRedaction(5,
      2)`) to delete two pages starting from page 5.
    question: Can I delete multiple pages at once?
  - answer: Absolutely. Pass the password to the `Redactor` constructor or set it
      via `redactor.setPassword("yourPassword")` before performing any operations.
    question: Does the library support password‑protected PDFs?
  - answer: It streams pages, allowing you to process PDFs with hundreds of pages
      while keeping memory usage low; typical processing of a 500‑page file uses under
      200 MB of RAM.
    question: How does GroupDocs.Redaction handle large files?
  - answer: Visit the [GroupDocs website](https://purchase.groupdocs.com/temporary-license/)
      to request a trial license that unlocks all API features for 30 days.
    question: Where can I obtain a temporary license for testing?
  type: FAQPage
title: Java में GroupDocs.Redaction का उपयोग करके अंतिम PDF पृष्ठ कैसे हटाएँ
type: docs
url: /hi/java/page-redaction/remove-last-page-pdf-groupdocs-redaction-java/
weight: 1
---

# Java में GroupDocs.Redaction का उपयोग करके अंतिम PDF पृष्ठ कैसे हटाएँ

एक दस्तावेज़ से अनचाहे **अंतिम PDF पृष्ठ** को हटाना एक थकाऊ मैन्युअल प्रक्रिया हो सकती है, विशेष रूप से जब आपको स्वचालित पाइपलाइन में दर्जनों फ़ाइलों को संभालना हो। **GroupDocs.Redaction for Java** के साथ, आप कुछ ही कोड लाइनों में अंतिम PDF पृष्ठ को हटा सकते हैं, दस्तावेज़ के बाकी हिस्से को अपरिवर्तित रख सकते हैं, और आवश्यक होने पर संपादन क्षमता बनाए रख सकते हैं। यह ट्यूटोरियल आपको सभी आवश्यक जानकारी प्रदान करता है—ऑपरेशन क्यों महत्वपूर्ण है, सटीक API कॉल्स, और सामान्य समस्याओं से बचने के व्यावहारिक टिप्स।

## त्वरित उत्तर
- **अंतिम PDF पृष्ठ को हटाने वाली लाइब्रेरी कौन सी है?** GroupDocs.Redaction for Java.  
- **क्या मुझे लाइसेंस चाहिए?** बेसिक टेस्ट के लिए ट्रायल काम करता है; प्रोडक्शन के लिए पूर्ण लाइसेंस आवश्यक है।  
- **क्या मैं हटाने से पहले PDF पृष्ठ गिनती जांच सकता हूँ?** हाँ—`redactor.getDocumentInfo().getPageCount()` का उपयोग करें।  
- **क्या हटाने के बाद मूल PDF संपादन योग्य रहता है?** संपादन क्षमता बनाए रखने के लिए `saveOptions.setRasterizeToPDF(false)` सेट करें।  
- **कौन सा Java संस्करण समर्थित है?** JDK 8 या उसके बाद का।

## “अंतिम PDF पृष्ठ हटाएँ” क्या है?
*अंतिम PDF पृष्ठ को हटाना* का मतलब है प्रोग्रामेटिक रूप से PDF फ़ाइल के अंतिम पृष्ठ को हटाना जबकि शेष सामग्री, मेटाडेटा और वैकल्पिक संपादन क्षमता को संरक्षित रखना। यह ऑपरेशन तब उपयोगी होता है जब अंतिम पृष्ठ में ड्राफ्ट नोट्स, प्लेसहोल्डर, या गोपनीय जानकारी हो जो अंतिम वितरण का हिस्सा नहीं होना चाहिए। इसे प्रोग्रामेटिक रूप से हटाने से मैन्युअल त्रुटियों से बचा जा सकता है, बैच प्रोसेसिंग तेज़ होती है, और फ़ाइल आकार को संग्रहण और ट्रांसमिशन के लिए अनुकूल रखा जाता है।

## इस कार्य के लिए GroupDocs.Redaction का उपयोग क्यों करें?
GroupDocs.Redaction **50+ इनपुट और आउटपुट फ़ॉर्मेट** का समर्थन करता है, **सैकड़ों पृष्ठों वाले PDF** को पूरी फ़ाइल को मेमोरी में लोड किए बिना प्रोसेस कर सकता है, और एक समर्पित `RemovePageRedaction` API प्रदान करता है जो बिल्ट‑इन सुरक्षा जांचों के साथ पृष्ठ‑सटीक हटाने की गारंटी देता है। अतिरिक्त रूप से, लाइब्रेरी मजबूत लाइसेंसिंग, विस्तृत दस्तावेज़ीकरण, और रेडैक्शन के बाद PDF को खोज योग्य और संपादन योग्य रखने की क्षमता प्रदान करती है, जिससे यह एंटरप्राइज़‑ग्रेड दस्तावेज़ पाइपलाइन के लिए विश्वसनीय विकल्प बन जाता है।

## पूर्वापेक्षाएँ
शुरू करने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित हैं:

- **Java Development Kit (JDK) 8 या बाद का** आपके मशीन पर स्थापित हो।  
- **Maven** (या मैन्युअल रूप से JAR फ़ाइलें जोड़ने की क्षमता) निर्भरता प्रबंधन के लिए।  
- एक **GroupDocs.Redaction लाइसेंस** (प्रयोग के लिए ट्रायल ठीक है)।  
- Java सिंटैक्स और प्रोजेक्ट संरचना की बुनियादी परिचितता।

### आवश्यक लाइब्रेरी और निर्भरताएँ
1. **Maven सेटअप**  
   - सुनिश्चित करें कि Maven आपके मशीन पर स्थापित है।  
   - अपने `pom.xml` फ़ाइल में निम्न कॉन्फ़िगरेशन जोड़ें ताकि GroupDocs.Redaction शामिल हो सके:

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

विस्तृत API उपयोग के लिए देखें [GroupDocs Redaction Java Documentation](https://docs.groupdocs.com/redaction/java/) और [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java)। नवीनतम संस्करणों के लिए [Latest Releases](https://releases.groupdocs.com/redaction/java/) देखें।

2. **सीधा डाउनलोड**  
   - वैकल्पिक रूप से, नवीनतम संस्करण को [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) से डाउनलोड करें।  
   - आप स्रोत कोड को [GroupDocs Redaction for Java](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java) पर देख सकते हैं और [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) पर प्रश्न पूछ सकते हैं।

### पर्यावरण सेटअप आवश्यकताएँ
- `JAVA_HOME` को JDK 8+ इंस्टॉलेशन की ओर इंगित करना सुनिश्चित करें।  
- आपका IDE (IntelliJ, Eclipse, VS Code) उसी JDK संस्करण का उपयोग करने के लिए कॉन्फ़िगर होना चाहिए।

### ज्ञान पूर्वापेक्षाएँ
- बुनियादी Java प्रोग्रामिंग अवधारणाएँ (क्लास, ऑब्जेक्ट, एक्सेप्शन हैंडलिंग)।  
- Maven के `pom.xml` की समझ उपयोगी है लेकिन यदि आप सीधे JAR विधि पसंद करते हैं तो अनिवार्य नहीं है।

## Java के लिए GroupDocs.Redaction सेटअप
GroupDocs.Redaction का उपयोग करने के लिए अपने प्रोजेक्ट को सेटअप करने में लाइब्रेरी जोड़ना और लाइसेंस कॉन्फ़िगर करना शामिल है।

### इंस्टॉलेशन जानकारी
1. **Maven कॉन्फ़िगरेशन**  
   - पिछले सेक्शन से रिपॉजिटरी और डिपेंडेंसी स्निपेट को अपने `pom.xml` में जोड़ें।

2. **सीधा डाउनलोड सेटअप**  
   - [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) से JAR फ़ाइल डाउनलोड करें।  
   - JAR को अपने प्रोजेक्ट के बिल्ड पाथ (जैसे, `libs/` फ़ोल्डर) में जोड़ें।

### लाइसेंस प्राप्ति
- GroupDocs सीमित कार्यक्षमता के साथ एक मुफ्त ट्रायल प्रदान करता है।  
- [GroupDocs वेबसाइट](https://purchase.groupdocs.com/temporary-license/) पर एक अस्थायी लाइसेंस प्राप्त करें या पूर्ण लाइसेंस खरीदें।  
- लाइसेंसिंग विवरण के लिए देखें [GroupDocs' licensing page](https://purchase.groupdocs.com/temporary-license/) या सीधे [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license/)।

## कार्यान्वयन गाइड
अब जब सब कुछ तैयार है, चलिए GroupDocs.Redaction का उपयोग करके **अंतिम PDF पृष्ठ हटाने** की सुविधा लागू करते हैं।

### GroupDocs.Redaction का उपयोग करके अंतिम PDF पृष्ठ कैसे हटाएँ?
`Redactor` इंस्टेंस के साथ PDF लोड करें, सत्यापित करें कि दस्तावेज़ में कम से कम एक पृष्ठ है, अंतिम पृष्ठ को लक्षित करने के लिए `RemovePageRedaction` लागू करें, `SaveOptions` कॉन्फ़िगर करें, और अंत में संशोधित फ़ाइल को सहेजें। यह संपूर्ण प्रवाह दस से कम Java कोड लाइनों में किया जा सकता है।

#### चरण‑दर‑चरण कार्यान्वयन

##### **चरण 1: Redactor को प्रारंभ करें**
`Redactor` वह मुख्य क्लास है जो PDF दस्तावेज़ का प्रतिनिधित्व करता है और रेडैक्शन तथा पृष्ठ हेरफेर के लिए मेथड्स प्रदान करता है।

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/multipage.pdf");
```

यह लाइन PDF को खोलती है और आगे के ऑपरेशन्स के लिए तैयार करती है।

##### **चरण 2: PDF पृष्ठ गिनती जांचें**
`DocumentInfo.getPageCount()` कुल पृष्ठों की संख्या लौटाता है, जिससे आप हटाने का प्रयास करने से पहले सुरक्षित रूप से यह सत्यापित कर सकते हैं कि अंतिम पृष्ठ मौजूद है।

```java
if (redactor.getDocumentInfo().getPageCount() >= 1) {
    // Proceed with removal if true
}
```

यदि गिनती शून्य है, तो `IndexOutOfBoundsException` से बचने के लिए ऑपरेशन को रोक देना चाहिए।

##### **चरण 3: RemovePageRedaction लागू करें**
`RemovePageRedaction` एक क्लास है जो शून्य‑आधारित इंडेक्स या मूल संदर्भ के आधार पर पृष्ठ हटाता है।

```java
redactor.apply(new RemovePageRedaction(PageSeekOrigin.End, -1));
```

- `PageSeekOrigin.End` निर्दिष्ट करता है कि पृष्ठ इंडेक्स दस्तावेज़ के अंत से गिना जाता है।  
- `-1` ऑफ़सेट ठीक एक पृष्ठ—अंतिम पृष्ठ—हटाता है।

##### **चरण 4: SaveOptions कॉन्फ़िगर करें**
`SaveOptions` नियंत्रित करता है कि संपादित PDF डिस्क पर कैसे लिखा जाता है और आपको संपादन क्षमता बनाए रखने देता है।

```java
SaveOptions saveOptions = new SaveOptions();
saveOptions.setAddSuffix(true); // Adds a suffix to the filename
saveOptions.setRasterizeToPDF(false); // Retains PDF editability
```

आप आउटपुट फ़ाइलनाम में एक प्रत्यय (जैसे, `_trimmed`) जोड़ सकते हैं ताकि मूल फ़ाइल को ओवरराइट करने से बचा जा सके।

##### **चरण 5: संशोधित दस्तावेज़ सहेजें**
`redactor.save(outputPath, saveOptions)` को कॉल करके परिवर्तन सहेजें। यह एक नया PDF लिखता है जिसमें अब अंतिम पृष्ठ नहीं रहता।

```java
redactor.save(saveOptions);
```

##### **चरण 6: संसाधनों को बंद करें**
नेटीव संसाधनों को मुक्त करने और मेमोरी लीक से बचने के लिए हमेशा `Redactor` इंस्टेंस को बंद करें।

```java
finally {
    redactor.close();
}
```

#### समस्या निवारण टिप्स
- **गलत फ़ाइल पथ** – दोबारा जाँचें कि इनपुट PDF पथ पूर्ण (absolute) है या आपके कार्य निर्देशिका के सापेक्ष सही है।  
- **शून्य‑पृष्ठ दस्तावेज़** – पृष्ठ‑गिनती जांच रनटाइम त्रुटि को रोकती है; यदि यह `0` लौटाता है, तो एक चेतावनी लॉग करें और हटाने के चरण को छोड़ दें।  
- **लाइसेंस त्रुटियाँ** – सुनिश्चित करें कि लाइसेंस फ़ाइल क्लासपाथ में रखी गई है या `License.setLicense("path/to/license")` के माध्यम से प्रदान की गई है।

## व्यावहारिक अनुप्रयोग
अंतिम पृष्ठ को हटाना कई वास्तविक‑दुनिया परिदृश्यों में उपयोगी है:

1. **प्रकाशन‑पूर्व संपादन** – रिपोर्ट जारी करने से पहले ड्राफ्ट या प्लेसहोल्डर पृष्ठ हटाएँ।  
2. **आर्काइव अनुकूलन** – बड़े दस्तावेज़ आर्काइव के संग्रहण लागत को कम करने के लिए अंत के खाली पृष्ठों को ट्रिम करें।  
3. **गोपनीयता** – वितरण से पहले संवेदनशील मेटाडेटा वाले कवर पृष्ठ को हटाएँ।  
4. **स्वचालित रिपोर्ट जनरेशन** – प्रोग्रामेटिक रूप से PDF बनाएं और स्वचालित रूप से जोड़े गए सारांश पृष्ठ को हटाएँ।  
5. **वर्कफ़्लो एकीकरण** – दस्तावेज़ जनरेशन को संभालने वाले CI/CD पाइपलाइन में हटाने के चरण को एम्बेड करें।

## प्रदर्शन विचार
GroupDocs.Redaction के साथ बड़े PDF प्रोसेस करते समय, इन टिप्स को ध्यान में रखें:

- **मेमोरी प्रबंधन** – `Redactor` को तुरंत बंद करें; लाइब्रेरी पृष्ठों को स्ट्रीम करती है बजाय पूरी फ़ाइल को मेमोरी में लोड करने के।  
- **रास्टराइज़ेशन** – यदि आउटपुट को खोज योग्य और संपादन योग्य रखना है तो रास्टराइज़ेशन (`setRasterizeToPDF(false)`) को निष्क्रिय करें।  
- **JVM हीप** – 200 MB से बड़े PDF के लिए कम से कम **2 GB** हीप (`-Xmx2g`) आवंटित करें ताकि `OutOfMemoryError` से बचा जा सके।  
- **बैच प्रोसेसिंग** – संभव हो तो कई फ़ाइलों के लिए एक ही `Redactor` इंस्टेंस पुनः उपयोग करें ताकि इनिशियलाइज़ेशन ओवरहेड कम हो।  
- प्रदर्शन‑संबंधी अपडेट के लिए [Latest Releases](https://releases.groupdocs.com/redaction/java/) देखें।

## निष्कर्ष
अब आपके पास Java में GroupDocs.Redaction का उपयोग करके **अंतिम PDF पृष्ठ हटाने** के लिए एक पूर्ण, प्रोडक्शन‑तैयार समाधान है। ऊपर दिए गए चरणों का पालन करके, आप इस क्षमता को किसी भी बैकएंड सेवा, बैच जॉब, या डेस्कटॉप एप्लिकेशन में एकीकृत कर सकते हैं, जिससे हर बार साफ़, आकार‑अनुकूलित PDF सुनिश्चित हो।  

अगले चरण में, टेक्स्ट रेडैक्शन, इमेज रिमूवल, और मेटाडेटा सैनिटाइज़ेशन जैसी अन्य रेडैक्शन सुविधाओं का अन्वेषण करें ताकि एक पूर्ण‑विशेषताओं वाला दस्तावेज़‑गोपनीयता पाइपलाइन बनाया जा सके।

## अक्सर पूछे जाने वाले प्रश्न

**प्रश्न: GroupDocs.Redaction का मुख्य उपयोग केस क्या है?**  
**उत्तर:** यह PDF और कई अन्य दस्तावेज़ फ़ॉर्मेट में संवेदनशील सामग्री को रेडैक्ट, संपादित और हेरफेर करने का प्रोग्रामेटिक तरीका प्रदान करता है, बिना Microsoft Office स्थापित किए।

**प्रश्न: क्या मैं एक साथ कई पृष्ठ हटा सकता हूँ?**  
**उत्तर:** हाँ—`RemovePageRedaction` को रेंज के साथ उपयोग करें (उदाहरण के लिए, `new RemovePageRedaction(5, 2)`) ताकि पृष्ठ 5 से शुरू होकर दो पृष्ठ हटाए जा सकें।

**प्रश्न: क्या लाइब्रेरी पासवर्ड‑सुरक्षित PDFs को समर्थन देती है?**  
**उत्तर:** बिल्कुल। किसी भी ऑपरेशन से पहले पासवर्ड को `Redactor` कन्स्ट्रक्टर में पास करें या `redactor.setPassword("yourPassword")` के माध्यम से सेट करें।

**प्रश्न: GroupDocs.Redaction बड़े फ़ाइलों को कैसे संभालता है?**  
**उत्तर:** यह पृष्ठों को स्ट्रीम करता है, जिससे आप सैकड़ों पृष्ठों वाले PDF को प्रोसेस कर सकते हैं जबकि मेमोरी उपयोग कम रहता है; 500‑पृष्ठ फ़ाइल की सामान्य प्रोसेसिंग 200 MB से कम RAM उपयोग करती है।

**प्रश्न: परीक्षण के लिए अस्थायी लाइसेंस कहाँ प्राप्त कर सकता हूँ?**  
**उत्तर:** सभी API सुविधाओं को 30 दिनों के लिए अनलॉक करने वाला ट्रायल लाइसेंस प्राप्त करने के लिए [GroupDocs वेबसाइट](https://purchase.groupdocs.com/temporary-license/) पर जाएँ।

---

**अंतिम अपडेट:** 2026-06-01  
**परीक्षित संस्करण:** GroupDocs.Redaction 24.9 for Java  
**लेखक:** GroupDocs  

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

## संबंधित ट्यूटोरियल

- [GroupDocs.Redaction का उपयोग करके कुशल Java PDF पृष्ठ रेंज डिलीशन](/redaction/java/page-redaction/java-pdf-page-range-deletion-groupdocs-redaction/)
- [GroupDocs.Redaction Java के साथ पृष्ठ प्रीव्यू कैसे करें – एक व्यापक गाइड](/redaction/java/document-loading/load-preview-document-pages-groupdocs-redaction-java/)
- [GroupDocs.Redaction for Java के साथ PDF दस्तावेज़ कैसे रेडैक्ट करें - चरण‑दर‑चरण गाइड](/redaction/java/advanced-redaction/master-redaction-groupdocs-java-guide/)