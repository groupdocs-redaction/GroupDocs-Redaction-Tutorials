---
date: '2026-01-08'
description: GroupDocs.Redaction के साथ जावा में MetadataSearchRedaction का उपयोग
  करना सीखें ताकि संवेदनशील दस्तावेज़ मेटाडेटा को सुरक्षित रूप से रीडैक्ट किया जा
  सके।
keywords:
- metadata redaction Java
- GroupDocs Redaction tutorial
- secure document metadata
title: GroupDocs के साथ जावा में MetadataSearchRedaction का उपयोग कैसे करें
type: docs
url: /hi/java/metadata-redaction/java-metadata-redaction-groupdocs-tutorial/
weight: 1
---

# Java में GroupDocs के साथ MetadataSearchRedaction का उपयोग कैसे करें

## त्वरित उत्तर
- **MetadataSearchRedaction क्या करता है?** यह विशिष्ट मेटाडेटा फ़ील्ड्स को खोजता है और उनके मानों को कस्टम टेक्स्ट से बदल देता है।  
- **कौन सी लाइब्रेरी आवश्यक है?** GroupDocs.Redaction for Java (v24.9 या नया)।  
- **क्या मुझे लाइसेंस चाहिए?** मूल्यांकन के लिए एक फ्री ट्रायल काम करता है; उत्पादन के लिए पूर्ण लाइसेंस आवश्यक है।  
- **क्या मैं मूल फ़ाइल फ़ॉर्मेट रख सकता हूँ?** हाँ—`SaveOptions` का उपयोग करके मूल फ़ॉर्मेट को संरक्षित रखें।  
- **क्या यह तरीका थ्रेड‑सेफ़ है?** प्रत्येक `Redactor` इंस्टेंस स्वतंत्र है, इसलिए आप दस्तावेज़ों को समानांतर में प्रोसेस कर सकते हैं।

## MetadataSearchRedaction क्या है?
`MetadataSearchRedaction` एक विशेष रेडैक्शन क्लास है जो आपको किसी विशिष्ट मेटाडेटा प्रॉपर्टी (जैसे *Company*, *Author*) को लक्षित करने और उसकी सामग्री को प्लेसहोल्डर से बदलने की अनुमति देता है। यह तब आदर्श है जब आपको बाहरी साझेदारों के साथ दस्तावेज़ साझा करने से पहले कॉरपोरेट डेटा को गुमनाम करना हो।

## मेटाडेटा रेडैक्शन के लिए MetadataSearchRedaction का उपयोग क्यों करें?
- **सटीकता** – केवल उन फ़ील्ड्स को रेडैक्ट करें जिन्हें आप निर्दिष्ट करते हैं, दस्तावेज़ के बाकी हिस्से को अपरिवर्तित छोड़ें।  
- **अनुपालन** – छिपे हुए पहचानकर्ताओं को हटाकर GDPR, HIPAA और अन्य गोपनीयता नियमों को पूरा करने में मदद करता है।  
- **ऑटोमेशन‑तैयार** – बैच प्रोसेसिंग पाइपलाइन या माइक्रो‑सर्विसेज़ में सहजता से फिट बैठता है।

## पूर्वापेक्षाएँ
- **GroupDocs.Redaction for Java** ≥ 24.9।  
- Java 8 या नया आपके मशीन पर स्थापित हो।  
- IntelliJ IDEA या Eclipse जैसे IDE (वैकल्पिक लेकिन अनुशंसित)।  
- Maven की बुनियादी समझ (या मैन्युअल रूप से JAR जोड़ने की क्षमता)।

## GroupDocs.Redaction for Java सेट अप करना
`pom.xml` में रिपॉजिटरी और डिपेंडेंसी जोड़ें। यह कदम सुनिश्चित करता है कि Maven लाइब्रेरी को स्वचालित रूप से डाउनलोड कर सके।

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

### लाइसेंस प्राप्ति
- **फ्री ट्रायल** – सभी फीचर्स को एक्सप्लोर करने के लिए ट्रायल लाइसेंस डाउनलोड करें।  
- **अस्थायी लाइसेंस** – विस्तारित परीक्षण के लिए उपयोग करें।  
- **पूर्ण लाइसेंस** – उत्पादन तैनाती के लिए आवश्यक है।

## बेसिक इनिशियलाइज़ेशन
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

### चरण 2: Redactor को इनिशियलाइज़ करें
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
`SaveOptions` को इस प्रकार कॉन्फ़िगर करें कि रेडैक्टेड फ़ाइल को “_Redacted” उपसर्ग मिले और मूल फ़ॉर्मेट बरकरार रहे।

```java
SaveOptions tmp0 = new SaveOptions();
tmp0.setAddSuffix(true);  // Adds "_Redacted" to file name
	tmp0.setRasterizeToPDF(false);  // Keeps original format

redactor.save(tmp0);
```

### चरण 6: रिसोर्सेज़ रिलीज़ करें
नेटीव रिसोर्सेज़ को मुक्त करने और मेमोरी लीक्स से बचने के लिए हमेशा `Redactor` को बंद करें।

```java
finally {
    redactor.close();
}
```

## सामान्य समस्याएँ और समाधान
- **FileNotFoundException** – `Redactor` को पास किए गए पाथ को दोबारा जांचें। विश्वसनीयता के लिए एब्सोल्यूट पाथ या `Paths.get(...)` का उपयोग करें।  
- **कोई बदलाव नहीं दिख रहा** – सुनिश्चित करें कि लक्षित मेटाडेटा फ़ील्ड में वास्तव में खोज स्ट्रिंग मौजूद है; डिफ़ॉल्ट रूप से मेटाडेटा केस‑सेंसिटिव होता है।  
- **बड़ी फ़ाइलों पर मेमोरी समाप्ति त्रुटियाँ** – दस्तावेज़ों को छोटे बैच में प्रोसेस करें और प्रत्येक फ़ाइल के बाद तुरंत `redactor.close()` कॉल करें।

## व्यावहारिक अनुप्रयोग
1. **कानूनी दस्तावेज़ीकरण** – तीसरे पक्ष को अनुबंध भेजने से पहले क्लाइंट कंपनी नाम हटाएँ।  
2. **वित्तीय रिपोर्टिंग** – ऑडिट फ़ाइलों में आंतरिक पहचानकर्ताओं को गुमनाम बनाएँ।  
3. **सहयोगी प्रोजेक्ट्स** – बाहरी विक्रेताओं के साथ ड्राफ्ट साझा करते समय स्वामित्व वाली जानकारी की सुरक्षा करें।

## प्रदर्शन संबंधी विचार
- **मेमोरी प्रबंधन** – लाइब्रेरी पूरे दस्तावेज़ को मेमोरी में रखती है; प्रत्येक फ़ाइल के बाद `Redactor` को बंद करना आवश्यक है।  
- **बैच प्रोसेसिंग** – उच्च‑वॉल्यूम परिदृश्यों के लिए, फ़ाइलों के संग्रह पर लूप करें और एक ही `SaveOptions` इंस्टेंस को पुन: उपयोग करें।  
- **अपडेटेड रहें** – नई रिलीज़ में प्रदर्शन सुधार और बग फिक्स होते हैं; हमेशा नवीनतम स्थिर संस्करण को लक्ष्य बनाएं।

## निष्कर्ष
अब आप जानते हैं **कैसे MetadataSearchRedaction का उपयोग करें** ताकि GroupDocs.Redaction for Java का उपयोग करके दस्तावेज़ों से कंपनी मेटाडेटा को सुरक्षित रूप से हटाया जा सके। इन चरणों को अपने दस्तावेज़‑प्रोसेसिंग पाइपलाइन में शामिल करें ताकि आप अनुपालन में रहें और संवेदनशील जानकारी की सुरक्षा कर सकें।

**आगे के कदम**
- *Author* या *Creator* जैसे अन्य मेटाडेटा फ़ील्ड्स के साथ प्रयोग करें।  
- पूरा‑कवरेज समाधान के लिए मेटाडेटा रेडैक्शन को टेक्स्ट या इमेज रेडैक्शन के साथ मिलाएँ।  

## FAQ अनुभाग
1. **GroupDocs.Redaction for Java क्या है?**  
   - यह एक शक्तिशाली लाइब्रेरी है जो आपको जावा एप्लिकेशन का उपयोग करके दस्तावेज़ों में टेक्स्ट, मेटाडेटा और इमेज को रेडैक्ट करने की सुविधा देती है।  
2. **क्या मैं लाइसेंस खरीदे बिना GroupDocs.Redaction का उपयोग कर सकता हूँ?**  
   - हाँ, लेकिन सीमाओं के साथ। फ्री ट्रायल या अस्थायी लाइसेंस परीक्षण उद्देश्यों के लिए पूर्ण एक्सेस देता है।  
3. **रेडैक्शन के दौरान दस्तावेज़ फ़ॉर्मेट को कैसे संरक्षित रखूँ?**  
   - अपनी आवश्यकताओं को निर्दिष्ट करने के लिए `SaveOptions` का उपयोग करें, जैसे PDF में रास्टराइज़ेशन से बचना।  
4. **GroupDocs.Redaction का उपयोग करके किन प्रकार के दस्तावेज़ रेडैक्ट किए जा सकते हैं?**  
   - यह कई प्रकार के दस्तावेज़ों को सपोर्ट करता है, जिसमें Word, Excel, PowerPoint, PDF और कई अन्य शामिल हैं।  
5. **जहाँ समस्या आएँ तो सहायता कहाँ मिल सकती है?**  
   - सहायता के लिए [GroupDocs सपोर्ट फ़ोरम](https://forum.groupdocs.com/c/redaction/33) देखें।  

## अक्सर पूछे जाने वाले प्रश्न
**प्र: क्या MetadataSearchRedaction एन्क्रिप्टेड दस्तावेज़ों के साथ काम करता है?**  
उ: हाँ। `Redactor` कंस्ट्रक्टर जो पासवर्ड पैरामीटर स्वीकार करता है, उसका उपयोग करके उपयुक्त पासवर्ड के साथ दस्तावेज़ लोड करें।

**प्र: क्या मैं एक ही रन में कई मेटाडेटा रेडैक्शन को चेन कर सकता हूँ?**  
उ: बिल्कुल। कई `MetadataSearchRedaction` ऑब्जेक्ट बनाएं, अलग-अलग फ़िल्टर सेट करें, और सेव करने से पहले उन्हें क्रमिक रूप से लागू करें।

**प्र: क्या सेव करने से पहले रेडैक्शन का प्रीव्यू देखना संभव है?**  
उ: आप `redactor.getRedactions()` कॉल करके पेंडिंग रेडैक्शन की सूची प्राप्त कर सकते हैं और उन्हें प्रोग्रामेटिकली जांच सकते हैं।

## संसाधन
- **Documentation**: विस्तृत गाइड के लिए देखें [GroupDocs दस्तावेज़ीकरण](https://docs.groupdocs.com/redaction/java/)।  
- **API Reference**: पूरी API रेफ़रेंस के लिए देखें [GroupDocs API रेफ़रेंस](https://reference.groupdocs.com/redaction/java)।  
- **Download Library**: नवीनतम रिलीज़ के लिए पहुँचें [GroupDocs डाउनलोड्स](https://releases.groupdocs.com/redaction/java/)।  
- **Source Code**: देखें और योगदान दें [GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)।  
- **Support**: मुफ्त सपोर्ट चैनल के लिए देखें [GroupDocs सपोर्ट फ़ोरम](https://forum.groupdocs.com/c/redaction/33)।

---

**Last Updated:** 2026-01-08  
**Tested With:** GroupDocs.Redaction 24.9 for Java  
**Author:** GroupDocs