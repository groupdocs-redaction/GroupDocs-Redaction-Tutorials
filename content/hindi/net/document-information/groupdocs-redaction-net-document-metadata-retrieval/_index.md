---
date: '2026-06-06'
description: GroupDocs.Redaction .NET का उपयोग करके metadata कैसे प्राप्त करें और
  दस्तावेज़ metadata निकालें, जिससे मजबूत दस्तावेज़ प्रबंधन और अनुपालन संभव हो सके।
keywords:
- how to retrieve metadata
- extract document metadata
- get document properties
- read file metadata
- get document size
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to retrieve metadata and extract document metadata using
    GroupDocs.Redaction .NET, enabling robust document management and compliance.
  headline: How to Retrieve Metadata with GroupDocs.Redaction .NET API
  type: TechArticle
- description: Learn how to retrieve metadata and extract document metadata using
    GroupDocs.Redaction .NET, enabling robust document management and compliance.
  name: How to Retrieve Metadata with GroupDocs.Redaction .NET API
  steps:
  - name: Prepare Your Document Path
    text: 'Define the absolute or relative path to the target file: Replace `YOUR_DOCUMENT_DIRECTORY`
      with the folder that contains your document.'
  - name: Initialize Redactor Instance
    text: 'Create a `Redactor` object that provides access to metadata methods:'
  - name: Retrieve Document Information
    text: 'Call `GetDocumentInfo()` on the `Redactor` instance to pull all available
      properties: The returned object includes file type, number of pages, and file
      size.'
  - name: Display Document Details
    text: 'Output the information to the console or UI. The sample code (commented
      for standalone runs) demonstrates how to print each property:'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction reads metadata from more than 50 formats, including
      PDF, DOCX, XLSX, PPTX, HTML, and common image types.
    question: Which document formats can I extract metadata from?
  - answer: Pass the password to the `Redactor` constructor; the API will decrypt
      the file before extracting metadata.
    question: How do I handle password‑protected files?
  - answer: While there is no hard limit, files larger than 2 GB may require additional
      memory tuning; performance remains linear with file size.
    question: Is there a limit to the size of files I can process?
  - answer: Yes—iterate over a collection of file paths and call `GetDocumentInfo()`
      for each; the library is thread‑safe for parallel execution.
    question: Can I retrieve metadata in a batch operation?
  - answer: A free trial license is sufficient for development and testing; a commercial
      license is required for production deployments.
    question: Do I need a license for development builds?
  type: FAQPage
title: GroupDocs.Redaction .NET API के साथ metadata कैसे प्राप्त करें
type: docs
url: /hi/net/document-information/groupdocs-redaction-net-document-metadata-retrieval/
weight: 1
---

# GroupDocs.Redaction .NET के साथ मेटाडेटा कैसे प्राप्त करें

आज के डिजिटल युग में, फ़ाइल से **मेटाडेटा कैसे प्राप्त करें** किसी भी दस्तावेज‑केंद्रित एप्लिकेशन के लिए एक मूलभूत कदम है। चाहे आपको अनुपालन ऑडिट के लिए फ़ाइल मेटाडेटा पढ़ना हो, इंडेक्सिंग के लिए दस्तावेज़ गुण निकालने हों, या UI में दस्तावेज़ का आकार दिखाना हो, GroupDocs.Redaction .NET आपको कुछ ही C# लाइनों में यह करने के लिए एक संक्षिप्त API देता है। यह ट्यूटोरियल आपको पूरे प्रक्रिया के माध्यम से ले जाता है, पर्यावरण सेटअप से लेकर प्राप्त जानकारी को प्रदर्शित करने तक, ताकि आप तुरंत दस्तावेज़ मेटाडेटा निकालना शुरू कर सकें।

## त्वरित उत्तर
- **मेटाडेटा प्राप्त करने की मुख्य विधि क्या है?** `Redactor.GetDocumentInfo()` को `Redactor` इंस्टेंस पर कॉल करें।  
- **कौन से फ़ॉर्मेट समर्थित हैं?** 50 से अधिक इनपुट और आउटपुट फ़ॉर्मेट, जिसमें PDF, DOCX, XLSX, PPTX, और इमेज प्रकार शामिल हैं।  
- **क्या विकास के लिए लाइसेंस आवश्यक है?** परीक्षण के लिए एक फ्री ट्रायल लाइसेंस काम करता है; उत्पादन के लिए पूर्ण लाइसेंस आवश्यक है।  
- **क्या मैं बड़े फ़ाइलों को प्रोसेस कर सकता हूँ?** हाँ—GroupDocs.Redaction कई‑सौ‑पृष्ठों वाले दस्तावेज़ों को पूरी फ़ाइल को मेमोरी में लोड किए बिना संभालता है।  
- **क्या async समर्थन उपलब्ध है?** API को async पैटर्न में रैप किया जा सकता है ताकि UI थ्रेड्स उत्तरदायी रहें।

## GroupDocs.Redaction में मेटाडेटा पुनर्प्राप्ति क्या है?
मेटाडेटा पुनर्प्राप्ति वह प्रक्रिया है जिसमें लाइब्रेरी के API के माध्यम से दस्तावेज़ की अंतर्निहित गुणों—जैसे फ़ाइल प्रकार, पृष्ठ संख्या, और आकार—तक पहुंचा जाता है। इन गुणों को निकालकर, डेवलपर्स प्रोग्रामेटिक रूप से दस्तावेज़ की विशेषताओं का मूल्यांकन कर सकते हैं, इंडेक्सिंग का समर्थन कर सकते हैं, अनुपालन नियमों को लागू कर सकते हैं, और आगे की प्रोसेसिंग चरणों के बारे में सूचित निर्णय ले सकते हैं।

## दस्तावेज़ मेटाडेटा कैसे प्राप्त करें?
`Redactor` क्लास GroupDocs.Redaction में दस्तावेज़ लोड करने और निरीक्षण करने के लिए मुख्य इंटरफ़ेस है।  
`GetDocumentInfo()` एक मेथड है जो `DocumentInfo` ऑब्जेक्ट लौटाता है जिसमें दस्तावेज़ का मेटाडेटा होता है।  

`new Redactor("path/to/file")` के साथ अपनी फ़ाइल लोड करें और `GetDocumentInfo()` को कॉल करें—यह कॉल एक `DocumentInfo` ऑब्जेक्ट लौटाता है जिसमें प्रकार, पृष्ठ संख्या, आकार, और अन्य गुण होते हैं। यह दो‑चरणीय दृष्टिकोण किसी भी समर्थित फ़ॉर्मेट के लिए काम करता है और अतिरिक्त कॉन्फ़िगरेशन की आवश्यकता नहीं होती। फिर आप `FileType`, `PageCount`, और `FileSize` जैसे फ़ील्ड पढ़कर जानकारी प्रदर्शित या लॉग कर सकते हैं।

## पूर्वापेक्षाएँ
- **GroupDocs.Redaction .NET** संस्करण 21.6 या नया।  
- .NET Framework 4.7.2 +, .NET Core 3.1 +, या .NET 5/6+।  
- बुनियादी C# ज्ञान और एक विकास IDE (Visual Studio, Rider, आदि)।  

## .NET के लिए GroupDocs.Redaction सेटअप
GroupDocs.Redaction के साथ शुरूआत करना सरल है। पैकेज को निम्नलिखित तरीकों में से किसी एक से इंस्टॉल करें:

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

या, **NuGet Package Manager UI** का उपयोग करें: बस “GroupDocs.Redaction” खोजें और **Install** पर क्लिक करें।

### लाइसेंस प्राप्ति
GroupDocs.Redaction को आज़माने के लिए, आप एक फ्री ट्रायल लाइसेंस प्राप्त कर सकते हैं। निरंतर विकास या उत्पादन उपयोग के लिए, पूर्ण लाइसेंस खरीदें या आधिकारिक साइट से एक अस्थायी लाइसेंस का अनुरोध करें।

इंस्टॉल करने के बाद, लाइब्रेरी को निम्नानुसार इनिशियलाइज़ करें:
```csharp
using GroupDocs.Redaction;
```

## कार्यान्वयन गाइड
### दस्तावेज़ जानकारी फ़ीचर प्राप्त करें
यह फ़ीचर GroupDocs.Redaction .NET का उपयोग करके दस्तावेज़ों से महत्वपूर्ण मेटाडेटा निकालने पर केंद्रित है। इन चरणों का पालन करें:

#### चरण 1: अपने दस्तावेज़ पथ को तैयार करें
लक्षित फ़ाइल के लिए पूर्ण या सापेक्ष पथ निर्धारित करें:
```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY\\SampleDocx.docx";
```

`YOUR_DOCUMENT_DIRECTORY` को उस फ़ोल्डर से बदलें जिसमें आपका दस्तावेज़ है।

#### चरण 2: Redactor इंस्टेंस को इनिशियलाइज़ करें
`Redactor` ऑब्जेक्ट बनाएं जो मेटाडेटा मेथड्स तक पहुंच प्रदान करता है:
```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // Further operations will be performed here
}
```

#### चरण 3: दस्तावेज़ जानकारी प्राप्त करें
`Redactor` इंस्टेंस पर `GetDocumentInfo()` को कॉल करें ताकि सभी उपलब्ध गुण प्राप्त हों:
```csharp
IDocumentInfo info = redactor.GetDocumentInfo();
```

वापसी वाला ऑब्जेक्ट फ़ाइल प्रकार, पृष्ठों की संख्या, और फ़ाइल आकार शामिल करता है।

#### चरण 4: दस्तावेज़ विवरण प्रदर्शित करें
जानकारी को कंसोल या UI में आउटपुट करें। सैंपल कोड (स्टैंडअलोन रन के लिए टिप्पणी किया गया) दिखाता है कि प्रत्येक गुण को कैसे प्रिंट किया जाए:
```csharp
Console.WriteLine($"File type: {info.FileType}\\
Number of pages: {info.PageCount}\\
Document size: {info.SizeInBytes} bytes");
```

### मेटाडेटा निष्कर्षण के लिए GroupDocs.Redaction क्यों उपयोग करें?
GroupDocs.Redaction **50+ फ़ाइल फ़ॉर्मेट** का समर्थन करता है और **2 GB** तक के दस्तावेज़ों को प्रोसेस कर सकता है, जबकि सामान्य वर्कलोड के लिए मेमोरी उपयोग **100 MB** से कम रहता है। लाइब्रेरी दस्तावेज़ को पूरी तरह लोड किए बिना मेटाडेटा निकालती है, तेज़ प्रतिक्रिया देती है—मानक सर्वर हार्डवेयर पर 100‑पृष्ठ PDF के लिए अक्सर **200 ms** से कम।

### सामान्य समस्याएँ और समाधान
- **गलत फ़ाइल पथ** – पथ स्ट्रिंग की जाँच करें और सुनिश्चित करें कि फ़ाइल चल रहे प्रोसेस के लिए सुलभ है।  
- **असमर्थित फ़ॉर्मेट** – फ़ॉर्मेट सूची देखें; यदि कोई फ़ॉर्मेट अनुपलब्ध है, तो पहले उसे कन्वर्ट करने पर विचार करें।  
- **प्रदर्शन बाधाएँ** – बहुत बड़ी फ़ाइलों के लिए, स्ट्रीमिंग विकल्प सक्षम करें या मेमोरी उपयोग को सीमित करने के लिए पृष्ठों को बैच में प्रोसेस करें।  

## व्यावहारिक अनुप्रयोग
दस्तावेज़ के मेटाडेटा को समझने से कई वास्तविक‑दुनिया के परिदृश्य संभव होते हैं:
1. **Document Management Systems (DMS)** – प्रकार, आकार, या पृष्ठ संख्या के आधार पर वर्गीकरण और इंडेक्सिंग को स्वचालित करें।  
2. **Compliance Auditing** – आर्काइव करने से पहले यह सत्यापित करें कि गोपनीय फ़ाइलों में आवश्यक मेटाडेटा मौजूद है।  
3. **Data Migration** – फ़ाइलों को गुणों के आधार पर समूहित करें ताकि बड़े पैमाने पर माइग्रेशन कार्य सुगम हो सके।  

## प्रदर्शन विचार
- **कुशल संसाधन उपयोग** – `Redactor` इंस्टेंस को `using` ब्लॉक के भीतर उपयोग करें ताकि उचित डिस्पोज़ल सुनिश्चित हो सके।  
- **असिंक्रोनस पैटर्न** – मेटाडेटा कॉल्स को `Task.Run` में रैप करें या async रैपर लागू करें ताकि डेस्कटॉप या वेब ऐप्स में UI थ्रेड्स उत्तरदायी रहें।  

## अक्सर पूछे जाने वाले प्रश्न
**प्रश्न: मैं किन दस्तावेज़ फ़ॉर्मेट से मेटाडेटा निकाल सकता हूँ?**  
A: GroupDocs.Redaction 50 से अधिक फ़ॉर्मेट से मेटाडेटा पढ़ता है, जिसमें PDF, DOCX, XLSX, PPTX, HTML, और सामान्य इमेज प्रकार शामिल हैं।

**प्रश्न: पासवर्ड‑सुरक्षित फ़ाइलों को कैसे संभालूँ?**  
A: `Redactor` कंस्ट्रक्टर में पासवर्ड पास करें; API मेटाडेटा निकालने से पहले फ़ाइल को डिक्रिप्ट कर देगा।

**प्रश्न: मैं कितनी बड़ी फ़ाइलें प्रोसेस कर सकता हूँ?**  
A: हालाँकि कोई कठोर सीमा नहीं है, 2 GB से बड़ी फ़ाइलों को अतिरिक्त मेमोरी ट्यूनिंग की आवश्यकता हो सकती है; प्रदर्शन फ़ाइल आकार के साथ रैखिक रहता है।

**प्रश्न: क्या मैं बैच ऑपरेशन में मेटाडेटा प्राप्त कर सकता हूँ?**  
A: हाँ—फ़ाइल पाथ्स के संग्रह पर इटरेट करें और प्रत्येक के लिए `GetDocumentInfo()` कॉल करें; लाइब्रेरी समानांतर निष्पादन के लिए थ्रेड‑सेफ़ है।

**प्रश्न: विकास बिल्ड्स के लिए क्या मुझे लाइसेंस चाहिए?**  
A: विकास और परीक्षण के लिए फ्री ट्रायल लाइसेंस पर्याप्त है; उत्पादन डिप्लॉयमेंट के लिए वाणिज्यिक लाइसेंस आवश्यक है।

## संसाधन
- [दस्तावेज़ीकरण](https://docs.groupdocs.com/redaction/net/)  
- [API संदर्भ](https://reference.groupdocs.com/redaction/net)  
- [डाउनलोड](https://releases.groupdocs.com/redaction/net/)  
- [नि:शुल्क समर्थन फ़ोरम](https://forum.groupdocs.com/c/redaction/33)  
- [अस्थायी लाइसेंस जानकारी](https://purchase.groupdocs.com/temporary-license/)  

## निष्कर्ष
अब आपके पास GroupDocs.Redaction .NET का उपयोग करके **मेटाडेटा कैसे प्राप्त करें** पर एक पूर्ण, चरण‑दर‑चरण गाइड है। `Redactor.GetDocumentInfo()` मेथड का उपयोग करके, आप जल्दी से फ़ाइल मेटाडेटा पढ़ सकते हैं, अनुपालन वर्कफ़्लो का समर्थन कर सकते हैं, और किसी भी दस्तावेज़‑प्रोसेसिंग पाइपलाइन को सुधार सकते हैं। अतिरिक्त Redaction सुविधाओं—जैसे कंटेंट रिडैक्शन, वॉटरमार्किंग, और दस्तावेज़ रूपांतरण—की खोज करें ताकि एक पूर्ण विशेषताओं वाला दस्तावेज़ प्रबंधन समाधान बना सकें।

---

**अंतिम अपडेट:** 2026-06-06  
**परीक्षण किया गया:** GroupDocs.Redaction .NET 21.6 (latest at time of writing)  
**लेखक:** GroupDocs  

## संबंधित ट्यूटोरियल
- [GroupDocs.Redaction .NET का उपयोग करके स्ट्रीम से दस्तावेज़ मेटाडेटा कैसे निकालें](/redaction/net/document-information/extract-document-info-streams-groupdocs-redaction-dotnet/)
- [GroupDocs.Redaction for .NET का उपयोग करके दस्तावेज़ मेटाडेटा को रिडैक्ट कैसे करें - एक व्यापक गाइड](/redaction/net/metadata-redaction/redact-metadata-groupdocs-redaction-net/)
- [GroupDocs.Redaction for .NET के साथ दस्तावेज़ लोडिंग ट्यूटोरियल](/redaction/net/document-loading/)