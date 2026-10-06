---
date: '2026-10-06'
description: GroupDocs.Redaction .NET के साथ संवेदनशील डेटा को कैसे रेडैक्ट करें,
  जानें। यह कदम-दर-कदम गाइड आपको दिखाता है कि रेडैक्शन नीति को XML के रूप में कैसे
  बनाएं, लागू करें और सहेजें।
keywords:
- redact sensitive data
- mask confidential information
- groupdocs redaction .net
lastmod: '2026-10-06'
og_description: GroupDocs.Redaction .NET के साथ संवेदनशील डेटा को कैसे रेडैक्ट करें,
  जानें। यह कदम-दर-कदम गाइड आपको दिखाता है कि रेडैक्शन नीति को XML के रूप में कैसे
  बनाएं, लागू करें और सहेजें।
og_image_alt: Tutorial showing how to redact sensitive data in documents with GroupDocs.Redaction
  for .NET
og_title: GroupDocs.Redaction .NET का उपयोग करके संवेदनशील डेटा को कैसे रेडैक्ट करें
schemas:
- author: GroupDocs
  dateModified: '2026-10-06'
  description: Learn how to redact sensitive data with GroupDocs.Redaction .NET. This
    step‑by‑step guide shows you how to create, apply, and save a redaction policy
    as XML.
  headline: How to redact sensitive data using GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to redact sensitive data with GroupDocs.Redaction .NET. This
    step‑by‑step guide shows you how to create, apply, and save a redaction policy
    as XML.
  name: How to redact sensitive data using GroupDocs.Redaction .NET
  steps:
  - name: prepare your document directory
    text: '*Replace `"YOUR_DOCUMENT_DIRECTORY"` with the folder that holds the documents
      you want to protect.*'
  - name: load the document
    text: The `Redactor` object opens the file and manages its lifecycle.
  - name: define the redactions
    text: 'ExactPhraseRedaction defines a rule that replaces a specific phrase, while
      `RegexRedaction` uses a regular expression to match patterns. Here we create
      two rules: 1. **ExactPhraseRedaction** – replaces a known phrase with “[REDACTED]”.
      2. **RegexRedaction** – finds dates in `YYYY‑MM‑DD` format and r'
  - name: apply the redactions
    text: All defined rules are executed against the opened document in one pass.
  - name: save the policy as an XML file
    text: The XML file stores the redaction definitions, allowing you to reuse the
      same policy without rewriting code.
  type: HowTo
- questions:
  - answer: Yes—use `redactor.LoadPolicy("policy.xml")` to import a previously saved
      policy.
    question: Can I load an existing XML policy instead of building one programmatically?
  - answer: 'Absolutely. Pass the password to the `Redactor` constructor: `new Redactor(sourceFile,
      "password")`.'
    question: Does GroupDocs.Redaction support password‑protected PDFs?
  - answer: The SDK provides `ImageRedaction` and `MetadataRedaction` classes for
      those scenarios.
    question: Is it possible to redact images or metadata?
  - answer: Process them in chunks or use the streaming API to reduce memory footprint;
      the engine can handle files up to 2 GB without loading the whole file into RAM.
    question: How do I handle large documents (hundreds of MB)?
  - answer: A paid license is required for production deployments; a trial license
      is fine for development and testing.
    question: What licensing model is required for commercial use?
  type: FAQPage
tags:
- redact sensitive data
- groupdocs redaction
- .net document security
- xml policy
- document redaction
title: GroupDocs.Redaction .NET का उपयोग करके संवेदनशील डेटा को कैसे रेडैक्ट करें
type: docs
url: /hi/net/advanced-redaction/groupdocs-redaction-net-create-save-policy/
weight: 1
---

# GroupDocs.Redaction .NET का उपयोग करके संवेदनशील डेटा को कैसे रेडैक्ट करें

संविदाओं, वित्तीय विवरणों या रोगी रिकॉर्ड में गोपनीय जानकारी की सुरक्षा आधुनिक अनुप्रयोगों के लिए एक अपरिवर्तनीय आवश्यकता है। इस गाइड में आप GroupDocs.Redaction for .NET के साथ **संवेदनशील डेटा को कैसे रेडैक्ट करें** सीखेंगे, SDK को स्थापित करने से लेकर पुन: उपयोग योग्य XML नीतियों को परिभाषित करने तक, जिन्हें किसी भी दस्तावेज़ प्रकार पर लागू किया जा सकता है।

## त्वरित उत्तर
- **“create redaction policy” का क्या अर्थ है?** यह नियमों (पाठ, regex, छवियों, आदि) को परिभाषित करने की प्रक्रिया है जो GroupDocs.Redaction को गोपनीय सामग्री को छिपाने या बदलने के लिए बताती है।  
- **मुझे कौनसी लाइब्रेरी चाहिए?** GroupDocs.Redaction for .NET, NuGet के माध्यम से उपलब्ध।  
- **क्या मुझे लाइसेंस चाहिए?** विकास के लिए एक मुफ्त ट्रायल काम करता है; उत्पादन के लिए एक स्थायी लाइसेंस आवश्यक है।  
- **क्या मैं नीति को पुन: उपयोग कर सकता हूँ?** हाँ—एक बार XML के रूप में सहेजने के बाद आप इसे बाद में लोड कर सकते हैं और किसी भी दस्तावेज़ पर लागू कर सकते हैं।  
- **कौनसे .NET संस्करण समर्थित हैं?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## रेडैक्शन नीति क्या है?
एक रेडैक्शन नीति नियमों का संग्रह है जो यह निर्धारित करता है कि *क्या* हटाया या बदला जाना चाहिए और *कैसे* प्रतिस्थापन दिखना चाहिए। एक बार नीति बनाकर, आप अपने अनुप्रयोग द्वारा प्रोसेस किए गए प्रत्येक दस्तावेज़ पर सुसंगत सुरक्षा मानकों को लागू कर सकते हैं।

## रेडैक्शन नीति कैसे काम करती है?
`Redactor` इंजन के साथ एक दस्तावेज़ लोड करें, एक या अधिक रेडैक्शन नियम संलग्न करें, और फिर `Apply` को कॉल करें। इंजन दस्तावेज़ को स्कैन करता है, मेल खाती सामग्री को मास्क करता है, और वैकल्पिक रूप से एक नई फ़ाइल आउटपुट करता है। समान नियमों का सेट XML में निर्यात किया जा सकता है, जिससे आप कोड को पुनः संकलित किए बिना नीति को पुन: उपयोग कर सकते हैं।

## रेडैक्शन नीति बनाने के लिए GroupDocs.Redaction का उपयोग क्यों करें?
GroupDocs.Redaction एक व्यापक फीचर सेट प्रदान करता है जो रेडैक्शन नीतियों के निर्माण, प्रबंधन और निष्पादन को सरल बनाता है, विविध दस्तावेज़ प्रकारों में सुसंगत डेटा सुरक्षा सुनिश्चित करता है, साथ ही उच्च प्रदर्शन और मौजूदा .NET अनुप्रयोगों में आसान एकीकरण प्रदान करता है, जिससे टीमों और संगठनों को लाभ मिलता है।

- **विस्तृत फ़ॉर्मेट समर्थन** – SDK 30+ फ़ाइल प्रकारों को संभालता है, जिसमें PDF, DOCX, XLSX, PPTX, और छवि फ़ॉर्मेट शामिल हैं, और पूरी फ़ाइल को मेमोरी में लोड किए बिना 2 GB तक की फ़ाइलों को प्रोसेस कर सकता है।  
- **प्रोग्रामेटिक सटीकता** – सटीक वाक्यांश, नियमित अभिव्यक्तियाँ, या कस्टम लॉजिक परिभाषित करें ताकि केवल वह डेटा लक्षित किया जा सके जिसे आप छिपाना चाहते हैं।  
- **पुन: उपयोग योग्य XML नीतियां** – अपने नियमों को एक बार निर्यात करें और उन्हें टीमों, सेवाओं, या माइक्रो‑सेवाओं के बीच साझा करें।  
- **प्रदर्शन‑अनुकूलित इंजन** – लाइब्रेरी सामान्य सर्वर हार्डवेयर पर एक सेकंड से कम समय में सैकड़ों पृष्ठों वाले दस्तावेज़ों को प्रोसेस करती है, जिससे यह उच्च‑थ्रूपुट पाइपलाइन के लिए उपयुक्त बनती है।

## आवश्यकताएँ
- GroupDocs.Redaction लाइब्रेरी जो आपके .NET रनटाइम के साथ संगत हो।  
- Visual Studio, VS Code, या कोई भी IDE जो C# को सपोर्ट करता हो।  
- C# और .NET प्रोजेक्ट संरचना की बुनियादी परिचितता।

## .NET के लिए GroupDocs.Redaction सेटअप करना

पहले, लाइब्रेरी को अपने प्रोजेक्ट में जोड़ें।

**.NET CLI का उपयोग करके**  
```bash
dotnet add package GroupDocs.Redaction
```  

**पैकेज मैनेजर का उपयोग करके**  
```powershell
Install-Package GroupDocs.Redaction
```  

या NuGet पैकेज मैनेजर UI में “GroupDocs.Redaction” खोजें और वहाँ से इसे इंस्टॉल करें।

### लाइसेंस प्राप्ति
- फ़ीचर का अन्वेषण करने के लिए **मुफ़्त ट्रायल** से शुरू करें।  
- विस्तारित परीक्षण के लिए **अस्थायी लाइसेंस** का अनुरोध करें, फिर उत्पादन उपयोग के लिए पूर्ण लाइसेंस खरीदें।

### बुनियादी प्रारंभिककरण
अपने स्रोत फ़ाइल में नेमस्पेस जोड़ें:

`Redactor` क्लास वह कोर इंजन है जो दस्तावेज़ को लोड करता है और रेडैक्शन नियम लागू करता है।  
```csharp
using GroupDocs.Redaction;
```  

`Redactor` क्लास GroupDocs.Redaction का कोर इंजन है जो दस्तावेज़ को लोड करता है और रेडैक्शन नियम लागू करता है।

## चरण‑दर‑चरण रेडैक्शन नीति कैसे बनाएं

नीचे एक पूर्ण walkthrough दिया गया है जो दिखाता है कि प्रोग्रामेटिक रूप से रेडैक्शन नीति कैसे बनाएं, उसके नियमों को कॉन्फ़िगर करें, उन्हें दस्तावेज़ पर लागू करें, और अंत में नीति को भविष्य में पुन: उपयोग के लिए XML फ़ाइल के रूप में सहेजें, जिससे कई प्रोजेक्ट और दस्तावेज़ प्रकारों में सुसंगत रेडैक्शन सुनिश्चित हो।

### चरण 1: अपना दस्तावेज़ निर्देशिका तैयार करें
```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
```  
*`"YOUR_DOCUMENT_DIRECTORY"` को उस फ़ोल्डर से बदलें जिसमें वे दस्तावेज़ हैं जिन्हें आप सुरक्षित करना चाहते हैं।*

### चरण 2: दस्तावेज़ लोड करें
```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // Further code will go here
}
```  
`Redactor` ऑब्जेक्ट फ़ाइल को खोलता है और उसके जीवनचक्र को प्रबंधित करता है।

### चरण 3: रेडैक्शन परिभाषित करें
ExactPhraseRedaction एक नियम परिभाषित करता है जो एक विशिष्ट वाक्यांश को बदलता है, जबकि `RegexRedaction` पैटर्न से मेल खाने के लिए नियमित अभिव्यक्ति का उपयोग करता है।  
```csharp
var redactions = new List<Redaction>
{
    new ExactPhraseRedaction("Sensitive Phrase", new ReplacementOptions("[REDACTED]")),
    new RegexRedaction(@"\d{4}-\d{2}-\d{2}", new ReplacementOptions("[DATE REDACTED]"))
};
```  
यहाँ हम दो नियम बनाते हैं:
1. **ExactPhraseRedaction** – ज्ञात वाक्यांश को “[REDACTED]” से बदलता है।  
2. **RegexRedaction** – `YYYY‑MM‑DD` फ़ॉर्मेट में तिथियों को खोजता है और उन्हें “[DATE REDACTED]” से बदलता है।

### चरण 4: रेडैक्शन लागू करें
```csharp
redactor.Apply(redactions);
```  
सभी परिभाषित नियम एक ही पास में खुले दस्तावेज़ पर लागू होते हैं।

### चरण 5: नीति को XML फ़ाइल के रूप में सहेजें
```csharp
string policyFile = "policy.xml";
redactor.SavePolicy(policyFile, new SaveOptions());
```  
XML फ़ाइल रेडैक्शन परिभाषाओं को संग्रहीत करती है, जिससे आप कोड को फिर से लिखे बिना वही नीति पुन: उपयोग कर सकते हैं।

## व्यावहारिक अनुप्रयोग
- **कानूनी फर्में** ड्राफ्ट साझा करने से पहले केस नंबर और क्लाइंट नामों को रेडैक्ट कर सकती हैं।  
- **वित्त विभाग** रिपोर्ट में खाता नंबर या लेनदेन तिथियों को मास्क कर सकते हैं।  
- **स्वास्थ्य सेवा प्रदाता** रोगी पहचानकर्ता हटाकर HIPAA अनुपालन सुनिश्चित करते हैं।

## प्रदर्शन सुझाव
- **एक समय में एक दस्तावेज़** खोलें ताकि मेमोरी उपयोग कम रहे।  
- **प्रभावी नियमित अभिव्यक्तियाँ** लिखें; अत्यधिक व्यापक पैटर्न से बचें जो प्रोसेसिंग समय बढ़ाते हैं।  
- लाइब्रेरी को **अप‑टू‑डेट** रखें ताकि प्रदर्शन सुधार और नई रेडैक्शन प्रकारों का लाभ मिल सके।

## सामान्य समस्याएँ और समाधान
| समस्या | यह क्यों होता है | समाधान |
|-------|----------------|--------|
| **डायरेक्टरी तैयार करते समय IO अपवाद** | गलत पथ या लिखने की अनुमति नहीं है | फ़ोल्डर मौजूद है और एप्लिकेशन के पास पढ़ने/लिखने के अधिकार हैं, यह सत्यापित करें। |
| **Regex अपेक्षित टेक्स्ट से मेल नहीं खाता** | पैटर्न बहुत सख्त है या एस्केप कैरेक्टर गायब हैं | ऑनलाइन टेस्टर से regex का परीक्षण करें; क्वांटिफायर या विशेष कैरेक्टर को एस्केप करके समायोजित करें। |
| **नीति फ़ाइल नहीं बनी** | `SavePolicy` को रेडैक्शन लागू करने से पहले या अमान्य पथ के साथ कॉल किया गया | सुनिश्चित करें कि आउटपुट डायरेक्टरी लिखने योग्य है और `Apply` के बाद `SavePolicy` को कॉल करें। |

## अक्सर पूछे जाने वाले प्रश्न
**प्रश्न: क्या मैं प्रोग्रामेटिक रूप से बनाने के बजाय मौजूदा XML नीति लोड कर सकता हूँ?**  
उत्तर: हाँ—पहले सहेजी गई नीति को आयात करने के लिए `redactor.LoadPolicy("policy.xml")` का उपयोग करें।

**प्रश्न: क्या GroupDocs.Redaction पासवर्ड‑सुरक्षित PDFs को सपोर्ट करता है?**  
उत्तर: बिल्कुल। पासवर्ड को `Redactor` कंस्ट्रक्टर में पास करें: `new Redactor(sourceFile, "password")`।

**प्रश्न: क्या छवियों या मेटाडेटा को रेडैक्ट करना संभव है?**  
उत्तर: SDK इन परिदृश्यों के लिए `ImageRedaction` और `MetadataRedaction` क्लास प्रदान करता है।

**प्रश्न: मैं बड़े दस्तावेज़ (सैकड़ों MB) को कैसे संभालूँ?**  
उत्तर: उन्हें भागों में प्रोसेस करें या मेमोरी फुटप्रिंट कम करने के लिए स्ट्रीमिंग API का उपयोग करें; इंजन पूरी फ़ाइल को RAM में लोड किए बिना 2 GB तक की फ़ाइलों को संभाल सकता है।

**प्रश्न: व्यावसायिक उपयोग के लिए कौनसा लाइसेंस मॉडल आवश्यक है?**  
उत्तर: उत्पादन परिनियोजन के लिए भुगतान किया गया लाइसेंस आवश्यक है; विकास और परीक्षण के लिए ट्रायल लाइसेंस पर्याप्त है।

## निष्कर्ष
अब आपके पास एक पूर्ण, पुन: उपयोग योग्य **रेडैक्शन नीति** है जिसे आप GroupDocs.Redaction for .NET के साथ किसी भी दस्तावेज़ पर लागू कर सकते हैं। नीति को XML में निर्यात करके, आप भविष्य के अपडेट को सरल बनाते हैं और अपने संगठन में सुसंगत डेटा सुरक्षा सुनिश्चित करते हैं।

### अगले कदम
- `ImageRedaction` या `MetadataRedaction` जैसे अतिरिक्त रेडैक्शन प्रकारों के साथ प्रयोग करें।  
- स्वचालित रेडैक्शन के लिए अपनी दस्तावेज़‑प्रबंधन वर्कफ़्लो में नीति लोड करने की लॉजिक को एकीकृत करें।  
- उन्नत अनुकूलन के लिए **GroupDocs.Redaction** API रेफ़रेंस का अन्वेषण करें।

---

**अंतिम अपडेट:** 2026-10-06  
**परीक्षित संस्करण:** GroupDocs.Redaction 5.8 for .NET  
**लेखक:** GroupDocs  

**संसाधन**  
- [दस्तावेज़ीकरण](https://docs.groupdocs.com/redaction/net/)  
- [API रेफ़रेंस](https://reference.groupdocs.com/redaction/net)  
- [डाउनलोड](https://releases.groupdocs.com/redaction/net/)  
- [नि:शुल्क समर्थन फ़ोरम](https://forum.groupdocs.com/c/redaction/33)  
- [अस्थायी लाइसेंस आवेदन](https://purchase.groupdocs.com/temporary-license/)

## संबंधित ट्यूटोरियल
- [GroupDocs.Redaction .NET (C#) के साथ संवेदनशील डेटा को रेडैक्ट करें](/redaction/net/advanced-redaction/groupdocs-redaction-net-implement-iredactioncallback-csharp/)
- [GroupDocs.Redaction .NET का उपयोग करके दस्तावेज़ रेडैक्शन लागू करें: चरण‑दर‑चरण गाइड](/redaction/net/getting-started/implement-document-redaction-groupdocs-redaction-net/)
- [GroupDocs.Redaction .NET के साथ दस्तावेज़ों को रेडैक्ट कैसे करें – एक पूर्ण गाइड](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)