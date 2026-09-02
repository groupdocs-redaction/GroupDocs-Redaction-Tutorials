---
date: '2026-06-01'
description: GroupDocs.Redaction for Java के साथ टिल्ट इफ़ेक्ट का उपयोग कैसे करें,
  जिसमें चरण‑दर‑चरण कोड, प्रदर्शन टिप्स, और अनुकूलन विकल्प शामिल हैं।
keywords:
- how to use tilt
- custom tilt effects
- GroupDocs.Redaction Java
- document rasterization
schemas:
- author: GroupDocs
  dateModified: '2026-06-01'
  description: Learn how to use tilt effect with GroupDocs.Redaction for Java, including
    step‑by‑step code, performance tips, and customization options.
  headline: How to Use Tilt Effect with GroupDocs.Redaction Java
  type: TechArticle
- description: Learn how to use tilt effect with GroupDocs.Redaction for Java, including
    step‑by‑step code, performance tips, and customization options.
  name: How to Use Tilt Effect with GroupDocs.Redaction Java
  steps:
  - name: Initialize Redactor and Save Options
    text: First, create a `Redactor` instance pointing at your source file, then prepare
      `SaveOptions` that will hold the rasterization configuration.
  - name: Configure Tilt Effect Settings
    text: Enable rasterization and define the tilt angle boundaries. The `AdvancedRasterizationOptions.Tilt`
      object lets you set `minAngle` and `maxAngle` in degrees, controlling how much
      each page can rotate.
  - name: Save Document with Tilt Effect
    text: Run the redaction process and output the rasterized, tilted document. The
      `save` call writes each page as an image (PNG by default) while applying the
      random tilt you specified.
  type: HowTo
- questions:
  - answer: It redacts sensitive content while preserving document layout and also
      supports advanced rasterization features like the tilt effect.
    question: What is GroupDocs.Redaction Java used for?
  - answer: By enabling rasterization and adding the `Tilt` advanced option with `minAngle`
      and `maxAngle` parameters, as shown in the code samples.
    question: How do I apply a tilt effect in my document using GroupDocs?
  - answer: Yes, a free trial is available. For production use, obtain a temporary
      or permanent license.
    question: Can I use GroupDocs.Redaction for free?
  - answer: It enhances visual appeal, adds a creative touch, and can help differentiate
      marketing or presentation materials.
    question: What are the benefits of using a tilt effect in documents?
  - answer: Very large files may increase processing time and memory usage; proper
      resource allocation mitigates this.
    question: Are there any limitations to applying custom effects with GroupDocs.Redaction
      Java?
  type: FAQPage
title: GroupDocs.Redaction Java के साथ टिल्ट इफ़ेक्ट का उपयोग कैसे करें
type: docs
url: /hi/java/rasterization-options/custom-tilt-effects-groupdocs-redaction-java/
weight: 1
---

# GroupDocs.Redaction Java के साथ टिल्ट इफ़ेक्ट का उपयोग कैसे करें

इस ट्यूटोरियल में आप **टिल्ट का उपयोग कैसे करें** यह जानेंगे जिससे आपके रास्टराइज़्ड दस्तावेज़ों को एक गतिशील, हाथ‑से‑धरा हुआ लुक मिलेगा, आधुनिक प्रस्तुतियों के लिए यह इफ़ेक्ट क्यों महत्वपूर्ण है, और GroupDocs.Redaction for Java में आपको कौन-से सेटिंग्स चाहिए। हम पूरी प्रक्रिया को समझाएंगे—लाइब्रेरी को इंस्टॉल करने से लेकर प्रदर्शन को फाइन‑ट्यून करने तक—ताकि आप वास्तविक प्रोजेक्ट्स में टिल्ट इफ़ेक्ट को आत्मविश्वास से लागू कर सकें।

## त्वरित उत्तर
- **टिल्ट इफ़ेक्ट क्या करता है?** यह प्रत्येक रास्टराइज़्ड पेज को परिभाषित रेंज के भीतर एक रैंडम कोण से घुमाता है, जिससे एक गतिशील, हल्का तिरछा लुक बनता है।  
- **कौन सी लाइब्रेरी यह फीचर प्रदान करती है?** GroupDocs.Redaction for Java (संस्करण 24.9 या नया)।  
- **क्या मुझे लाइसेंस चाहिए?** मूल्यांकन के लिए एक फ्री ट्रायल काम करता है; उत्पादन के लिए स्थायी या अस्थायी लाइसेंस आवश्यक है।  
- **क्या यह मेमोरी‑गहन है?** यह कुछ CPU ओवरहेड जोड़ता है, लेकिन उचित मेमोरी सेटिंग्स से यह बड़े फ़ाइलों के लिए भी कुशल रहता है।  
- **क्या मैं कोण रेंज को कस्टमाइज़ कर सकता हूँ?** हाँ – रास्टराइज़ेशन विकल्पों में `minAngle` और `maxAngle` पैरामीटर का उपयोग करें।

## कस्टम टिल्ट इफ़ेक्ट क्या है?
कस्टम टिल्ट इफ़ेक्ट एक दृश्य परिवर्तन है जो दस्तावेज़ के प्रत्येक पेज को छवि में बदलते समय लागू किया जाता है। न्यूनतम और अधिकतम कोण निर्दिष्ट करके, रास्टराइज़र पेजों को रैंडम रूप से टिल्ट करता है, जिससे अंतिम आउटपुट को एक कलात्मक, “हाथ‑से‑धरा” महसूस होता है। यह इफ़ेक्ट विशेष रूप से उपयोगी है जब आप मानक PDFs के कठोर, पूरी तरह संरेखित लुक को तोड़ना चाहते हैं और उसमें व्यक्तिगत स्पर्श जोड़ना चाहते हैं।

## GroupDocs.Redaction के साथ कस्टम टिल्ट इफ़ेक्ट क्यों लागू करें?
GroupDocs.Redaction **70+ इनपुट और आउटपुट फॉर्मैट** के लिए रास्टराइज़ेशन का समर्थन करता है और **2,000 पेज** तक के PDFs को पूरी फ़ाइल को मेमोरी में लोड किए बिना प्रोसेस कर सकता है। इसकी बिल्ट‑इन टिल्ट विकल्प का उपयोग करने से आप थर्ड‑पार्टी इमेज लाइब्रेरीज़ से बचते हैं, इंटीग्रेशन जटिलता कम होती है, और पूरे वर्कफ़्लो को एक ही, अच्छी तरह परीक्षण किए गए SDK में रख सकते हैं।

- **एंगेजमेंट:** टिल्टेड पेज पाठक की नजर पकड़ते हैं, प्रस्तुतियों या मार्केटिंग ब्रोशर्स के लिए उपयुक्त।  
- **ब्रांडिंग:** मूल सामग्री को बदले बिना एक अनूठी दृश्य हस्ताक्षर जोड़ता है।  
- **लचीलापन:** आप कोण रेंज को नियंत्रित करते हैं, जिससे सूक्ष्म या नाटकीय टिल्ट संभव होते हैं।  
- **इंटीग्रेशन:** यह इफ़ेक्ट GroupDocs.Redaction के रास्टराइज़ेशन पाइपलाइन में निर्मित है, इसलिए आपको बाहरी इमेज‑प्रोसेसिंग टूल्स की आवश्यकता नहीं है।

## पूर्वापेक्षाएँ
- Java 8 या बाद का स्थापित हो।  
- Maven (या कोई अन्य बिल्ड टूल) डिपेंडेंसीज़ को मैनेज करने के लिए।  
- GroupDocs.Redaction 24.9 या नया (ट्यूटोरियल नवीनतम रिलीज़ का उपयोग करता है)।  
- Java फ़ाइल हैंडलिंग का बुनियादी ज्ञान।

## GroupDocs.Redaction for Java सेटअप करना

### इंस्टॉलेशन जानकारी

**Maven**

अपने Maven प्रोजेक्ट में GroupDocs.Redaction को शामिल करने के लिए नीचे दिया गया रिपॉज़िटरी और डिपेंडेंसी अपने `pom.xml` फ़ाइल में जोड़ें:

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

**सीधा डाउनलोड**

वैकल्पिक रूप से, नवीनतम संस्करण सीधे [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) से डाउनलोड करें।

#### लाइसेंस प्राप्ति

GroupDocs.Redaction का पूर्ण उपयोग करने के लिए:

- **फ्री ट्रायल** – बिना लागत के कोर फीचर्स का अन्वेषण करें।  
- **अस्थायी लाइसेंस** – पूर्ण मूल्यांकन के लिए समय‑सीमित कुंजी का अनुरोध [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/) के माध्यम से करें।  
- **खरीदें** – उत्पादन उपयोग के लिए स्थायी लाइसेंस प्राप्त करें।

### बुनियादी इनिशियलाइज़ेशन और सेटअप

`Redactor` क्लास GroupDocs.Redaction में सभी रेडैक्शन और रास्टराइज़ेशन ऑपरेशन्स के लिए एंट्री पॉइंट है। यह दस्तावेज़ लोडिंग, प्रोसेसिंग और सेविंग को मैनेज करता है, जिससे संसाधन स्वचालित रूप से रिलीज़ हो जाते हैं।

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;

// Set the path to your document directory
String documentPath = "YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX";

// Initialize a Redactor with the specified document
Redactor redactor = new Redactor(documentPath);
```

## रास्टराइज़ेशन के दौरान कस्टम टिल्ट इफ़ेक्ट कैसे लागू करें
अपनी स्रोत फ़ाइल लोड करें, रास्टराइज़ेशन सक्षम करें, इच्छित टिल्ट रेंज सेट करें, और फिर परिवर्तित दस्तावेज़ को सेव करें—सभी कुछ संक्षिप्त चरणों में। यह अवलोकन पूरी वर्कफ़्लो को समझाता है, ताकि आप ठीक-ठीक जान सकें कि कौन से ऑब्जेक्ट बनाना है, कौन से विकल्प कॉन्फ़िगर करने हैं, और विस्तृत कोड देखने से पहले सेव ऑपरेशन को कैसे कॉल करें।

### चरण‑दर‑चरण कार्यान्वयन

#### चरण 1: Redactor को इनिशियलाइज़ करें और Save Options सेट करें
पहले, अपनी स्रोत फ़ाइल की ओर इशारा करता हुआ `Redactor` इंस्टेंस बनाएं, फिर `SaveOptions` तैयार करें जो रास्टराइज़ेशन कॉन्फ़िगरेशन रखेगा।

```java
import com.groupdocs.redaction.options.AdvancedRasterizationOptions;
import java.util.HashMap;

Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
SaveOptions saveOptions = new SaveOptions();
```

#### चरण 2: टिल्ट इफ़ेक्ट सेटिंग्स कॉन्फ़िगर करें
रास्टराइज़ेशन सक्षम करें और टिल्ट कोण सीमाएँ निर्धारित करें। `AdvancedRasterizationOptions.Tilt` ऑब्जेक्ट आपको डिग्री में `minAngle` और `maxAngle` सेट करने देता है, जिससे प्रत्येक पेज कितनी घुमाव कर सकता है, नियंत्रित होता है।

```java
saveOptions.getRasterization().setEnabled(true);
HashMap<String, String> tiltSettings = new HashMap<>();
tiltSettings.put("minAngle", "15"); // Set the minimum angle for the tilt effect
	tiltSettings.put("maxAngle", "30"); // Set the maximum angle for the tilt effect

saveOptions.getRasterization().addAdvancedOption(
    AdvancedRasterizationOptions.Tilt, 
    tiltSettings
);
```

#### चरण 3: टिल्ट इफ़ेक्ट के साथ दस्तावेज़ को सेव करें
रेडैक्शन प्रोसेस चलाएँ और रास्टराइज़्ड, टिल्टेड दस्तावेज़ आउटपुट करें। `save` कॉल प्रत्येक पेज को एक इमेज (डिफ़ॉल्ट रूप से PNG) के रूप में लिखता है, जबकि आपने निर्दिष्ट किया हुआ रैंडम टिल्ट लागू करता है।

```java
redactor.save("OUTPUT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX_scan", saveOptions);
```

### पैरामीटरों की व्याख्या
- **minAngle** – पेज पर लागू किया जा सकने वाला सबसे छोटा घुमाव (डिग्री में)।  
- **maxAngle** – अनुमति दिया गया सबसे बड़ा घुमाव (डिग्री में)।  
इन मानों को समायोजित करके सूक्ष्म या स्पष्ट टिल्ट प्राप्त करें।

#### समस्या निवारण टिप्स
- सत्यापित करें कि स्रोत और आउटपुट डायरेक्टरी JVM द्वारा लिखने योग्य हैं।  
- पुष्टि करें कि आप GroupDocs.Redaction 24.9 या नया उपयोग कर रहे हैं; पुराने संस्करणों में `Tilt` विकल्प नहीं होता।  
- यदि आउटपुट बहुत अधिक विकृत दिखता है, तो `maxAngle` मान को घटाएँ।

## व्यावहारिक अनुप्रयोग
1. **रचनात्मक दस्तावेज़ प्रस्तुति** – स्लाइड डेक या क्लाइंट प्रस्तावों में गतिशील लुक जोड़ें।  
2. **मार्केटिंग सामग्री** – ब्रोशर्स और फ्लायर्स को अधिक हाथ‑से‑बनाया हुआ महसूस कराएँ।  
3. **डिजिटल अभिलेख** – ऐतिहासिक स्कैन को ऑनलाइन प्रदर्शनों के लिए सूक्ष्म, स्टाइलिश रूप दें।

## प्रदर्शन संबंधी विचार

### प्रदर्शन का अनुकूलन
- **मेमोरी प्रबंधन:** मल्टी‑पेज PDFs प्रोसेस करते समय पर्याप्त हीप स्पेस (`-Xmx2g` या अधिक) आवंटित करें।  
- **I/O दक्षता:** फ़ाइलों को बैच प्रोसेस करें और जहाँ संभव हो एक ही `Redactor` इंस्टेंस को पुनः उपयोग करें।

### जावा मेमोरी मैनेजमेंट के लिए सर्वोत्तम प्रैक्टिसेज
- `System.gc()` को कम ही उपयोग करें; JVM के गार्बेज कलेक्टर पर भरोसा रखें।  
- स्ट्रीम्स को तुरंत बंद करें (GroupDocs.Redaction अधिकांश क्लीनअप आंतरिक रूप से संभालता है)।

## सामान्य समस्याएँ और समाधान
| समस्या | संभावित कारण | समाधान |
|-------|--------------|----------|
| टिल्ट लागू नहीं हुआ | रास्टराइज़ेशन अक्षम | Ensure `saveOptions.getRasterization().setEnabled(true);` |
| आउटपुट फ़ाइल खाली | गलत आउटपुट पथ | Verify the directory exists and has write permissions |
| अनपेक्षित कोण | `minAngle` > `maxAngle` | Swap values so `minAngle` ≤ `maxAngle` |

## अक्सर पूछे जाने वाले प्रश्न

**Q: GroupDocs.Redaction Java का उपयोग किस लिए किया जाता है?**  
A: यह संवेदनशील सामग्री को रेडैक्ट करता है जबकि दस्तावेज़ लेआउट को बनाए रखता है और टिल्ट इफ़ेक्ट जैसे उन्नत रास्टराइज़ेशन फीचर भी समर्थन करता है।

**Q: मैं अपने दस्तावेज़ में GroupDocs का उपयोग करके टिल्ट इफ़ेक्ट कैसे लागू करूँ?**  
A: रास्टराइज़ेशन सक्षम करके और `Tilt` एडवांस्ड विकल्प को `minAngle` और `maxAngle` पैरामीटर के साथ जोड़कर, जैसा कि कोड उदाहरणों में दिखाया गया है।

**Q: क्या मैं GroupDocs.Redaction को मुफ्त में उपयोग कर सकता हूँ?**  
A: हाँ, एक फ्री ट्रायल उपलब्ध है। उत्पादन उपयोग के लिए अस्थायी या स्थायी लाइसेंस प्राप्त करें।

**Q: दस्तावेज़ों में टिल्ट इफ़ेक्ट उपयोग करने के क्या लाभ हैं?**  
A: यह दृश्य आकर्षण बढ़ाता है, रचनात्मक स्पर्श जोड़ता है, और मार्केटिंग या प्रस्तुति सामग्री को अलग करने में मदद कर सकता है।

**Q: GroupDocs.Redaction Java के साथ कस्टम इफ़ेक्ट लागू करने में कोई सीमाएँ हैं?**  
A: बहुत बड़ी फ़ाइलें प्रोसेसिंग समय और मेमोरी उपयोग बढ़ा सकती हैं; उचित संसाधन आवंटन इससे बचाता है।

## संसाधन
- [GroupDocs Redaction दस्तावेज़ीकरण](https://docs.groupdocs.com/redaction/java/)
- [API रेफ़रेंस](https://reference.groupdocs.com/redaction/java)
- [GroupDocs.Redaction for Java डाउनलोड करें](https://releases.groupdocs.com/redaction/java/)
- [GitHub रिपॉज़िटरी](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
- [फ़्री सपोर्ट फ़ोरम](https://forum.groupdocs.com/c/redaction/33)
- [अस्थायी लाइसेंस आवेदन](https://purchase.groupdocs.com/temporary-license/)

**अंतिम अपडेट:** 2026-06-01  
**परीक्षित संस्करण:** GroupDocs.Redaction 24.9 for Java  
**लेखक:** GroupDocs  

## संबंधित ट्यूटोरियल
- [GroupDocs.Redaction Java के लिए रास्टराइज़ेशन विकल्प ट्यूटोरियल](/redaction/java/rasterization-options/)
- [जावा में कस्टम नॉइज़ रास्टराइज़ेशन: GroupDocs.Redaction के साथ संवेदनशील जानकारी सुरक्षित करें](/redaction/java/rasterization-options/java-groupdocs-redaction-custom-noise-rasterization/)
- [GroupDocs Redaction for Java का उपयोग कैसे करें: वर्ड दस्तावेज़ों में प्री‑रास्टराइज़ेशन](/redaction/java/rasterization-options/groupdocs-redaction-java-pre-rasterization-word-docs/)