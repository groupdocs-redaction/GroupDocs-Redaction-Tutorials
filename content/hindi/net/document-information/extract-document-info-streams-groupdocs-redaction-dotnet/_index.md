---
date: '2026-06-11'
description: GroupDocs.Redaction for .NET का उपयोग करके दस्तावेज़ स्ट्रीम से मेटाडेटा
  निकालना सीखें, जिसमें सेटअप, कोड उदाहरण और व्यावहारिक अनुप्रयोग शामिल हैं।
keywords:
- how to extract metadata
- extract document metadata
- extract pdf metadata
- retrieve document size
- prepare output directory
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to extract metadata from document streams using GroupDocs.Redaction
    for .NET, covering setup, code examples, and practical applications.
  headline: How to Extract Metadata from Document Streams Using GroupDocs.Redaction
    .NET
  type: TechArticle
- description: Learn how to extract metadata from document streams using GroupDocs.Redaction
    for .NET, covering setup, code examples, and practical applications.
  name: How to Extract Metadata from Document Streams Using GroupDocs.Redaction .NET
  steps:
  - name: Prepare the source file path
    text: First, ensure the source file exists and that the output folder is ready.
      The helper method below checks the output directory and creates it if needed.
      *Why?* This guarantees a valid path for subsequent file operations and prevents
      `DirectoryNotFoundException`.
  - name: Open the document stream
    text: Using `File.OpenRead()` opens the file as a **read‑only stream**, which
      keeps memory usage low even for gigabyte‑size files. *Why?* Streams enable on‑the‑fly
      processing, allowing you to work with portions of the file rather than the whole
      document.
  - name: Initialise the Redactor with the document stream
    text: '`Redactor` is the primary API object that gives you access to document‑level
      operations, including metadata extraction. `Redactor` represents a single document
      loaded from a stream and exposes methods such as `GetDocumentInfo()` for quick
      property retrieval. *Why?* Instantiating `Redactor` with a st'
  - name: Retrieve document metadata
    text: Calling `GetDocumentInfo()` returns a `DocumentInfo` object that holds the
      file format, page count, and file size. `GetDocumentInfo()` extracts core properties
      (format, page count, size) in a single call, eliminating the need for separate
      parsers. *Why?* This step consolidates all essential metadata
  type: HowTo
- questions:
  - answer: It enables fast, memory‑efficient retrieval of document properties for
      indexing, compliance checks, and automated routing without opening the full
      file.
    question: What is the primary use case for GroupDocs.Redaction’s metadata extraction?
  - answer: Yes, provide the password when constructing the `Redactor` object; the
      API will decrypt the stream internally.
    question: Can I extract metadata from password‑protected files?
  - answer: Absolutely – GroupDocs.Redaction handles over 30 formats, including PDF,
      DOCX, XLSX, PPTX, and common image types.
    question: Does the library support non‑PDF formats like DOCX or XLSX?
  - answer: Streams allow processing of files up to **2 GB** while keeping memory
      consumption under **50 MB**, thanks to on‑the‑fly reading.
    question: How large a document can I process with streams?
  - answer: Visit the [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33)
      for community support, or consult the official documentation for troubleshooting
      tips.
    question: Where can I get help if I run into issues?
  type: FAQPage
title: GroupDocs.Redaction .NET का उपयोग करके दस्तावेज़ स्ट्रीम से मेटाडेटा निकालने
  का तरीका
type: docs
url: /hi/net/document-information/extract-document-info-streams-groupdocs-redaction-dotnet/
weight: 1
---

# GroupDocs.Redaction .NET का उपयोग करके दस्तावेज़ स्ट्रीम से मेटाडेटा निकालना कैसे

क्या आप दस्तावेज़ जानकारी को मैन्युअल रूप से निकालने या बड़े फ़ाइलों से निपटने से थक चुके हैं जो आपके कार्यप्रवाह को धीमा कर देती हैं? **मेटाडेटा कैसे निकालें** जल्दी से एक सामान्य चुनौती है, और .NET के लिए GroupDocs.Redaction लाइब्रेरी स्ट्रीम से सीधे दस्तावेज़ विवरण प्राप्त करने का तेज़, मेमोरी‑कुशल तरीका प्रदान करती है। इस ट्यूटोरियल में, आप सीखेंगे कि लाइब्रेरी को कैसे सेट अप करें, स्ट्रीम से फ़ाइल प्रकार, पेज काउंट और आकार कैसे प्राप्त करें, और आगे की प्रोसेसिंग के लिए आउटपुट फ़ोल्डर कैसे तैयार करें।

## त्वरित उत्तर
- **“extract metadata” क्या मतलब है?** इसका अर्थ है फ़ाइल प्रकार, पेज काउंट और आकार जैसी प्रॉपर्टीज़ को पढ़ना बिना पूरी दस्तावेज़ को मेमोरी में खोलें।  
- **कौन सी लाइब्रेरी इसे संभालती है?** .NET के लिए GroupDocs.Redaction स्ट्रीम‑आधारित मेटाडेटा निष्कर्षण के लिए एक नेटिव API प्रदान करती है।  
- **क्या मुझे लाइसेंस चाहिए?** विकास के लिए एक फ्री ट्रायल काम करता है; प्रोडक्शन के लिए एक कमर्शियल लाइसेंस आवश्यक है।  
- **क्या मैं 1 GB से बड़ी PDFs प्रोसेस कर सकता हूँ?** हाँ – स्ट्रीम आपको पूरी फ़ाइल लोड किए बिना 2 GB तक की फ़ाइलें संभालने देती हैं।  
- **कौन से .NET संस्करण समर्थित हैं?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5+, और .NET 6+.

## स्ट्रीम से मेटाडेटा निष्कर्षण क्या है?
स्ट्रीम से मेटाडेटा निष्कर्षण वह प्रक्रिया है जिसमें दस्तावेज़ प्रॉपर्टीज़ को सीधे `Stream` ऑब्जेक्ट से पढ़ा जाता है, पूरी फ़ाइल लोड करने से बचा जाता है और इस प्रकार मेमोरी और CPU समय बचता है। यह तकनीक बैच प्रोसेसिंग या क्लाउड‑आधारित सेवाओं के लिए आदर्श है जहाँ संसाधन सीमित होते हैं।

## मेटाडेटा निष्कर्षण के लिए GroupDocs.Redaction का उपयोग क्यों करें?
GroupDocs.Redaction **30+ फ़ाइल फ़ॉर्मेट** (PDF, DOCX, XLSX, PPTX और इमेज टाइप सहित) को सपोर्ट करता है और **2 GB** तक के दस्तावेज़ों को प्रोसेस कर सकता है जबकि मेमोरी उपयोग **50 MB** से कम रखता है। इसका `Redactor` API सभी प्रमुख दस्तावेज़ जानकारी प्राप्त करने के लिए एक ही कॉल प्रदान करता है, जिससे कई पार्सर्स की आवश्यकता समाप्त हो जाती है।

## पूर्वापेक्षाएँ
- **GroupDocs.Redaction for .NET** (नवीनतम संस्करण)  
- **.NET Framework** 4.5+ **या** **.NET Core/5+/6+**  
- बेसिक C# ज्ञान और फ़ाइल I/O से परिचितता  
- Visual Studio 2019 या बाद का संस्करण  

## मैं GroupDocs.Redaction for .NET को कैसे सेट अप करूँ?
GroupDocs.Redaction का उपयोग शुरू करने के लिए, आपको पहले लाइब्रेरी को अपने प्रोजेक्ट में जोड़ना होगा। यह .NET CLI, Visual Studio पैकेज मैनेजर, या NuGet UI के माध्यम से किया जा सकता है। वह तरीका चुनें जो आपके कार्यप्रवाह के अनुकूल हो; CLI स्क्रिप्टेबल बिल्ड्स के लिए आदर्श है, जबकि UI संस्करणों और डिपेंडेंसीज़ को ब्राउज़ करने का ग्राफ़िकल तरीका प्रदान करता है।

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI:**
- Visual Studio में NuGet पैकेज मैनेजर खोलें।  
- **"GroupDocs.Redaction"** को खोजें और नवीनतम संस्करण स्थापित करें।

### लाइसेंस प्राप्ति चरण
1. **Free Trial:** सभी फीचर्स को बिना प्रतिबंधों के एक्सप्लोर करने के लिए एक ट्रायल लाइसेंस डाउनलोड करें।  
2. **Temporary License:** विस्तारित टेस्टिंग के लिए [GroupDocs](https://purchase.groupdocs.com/temporary-license/) से एक टेम्पररी लाइसेंस अनुरोध करें।  
3. **Purchase:** प्रोडक्शन के लिए तैयार होने पर एक कमर्शियल लाइसेंस खरीदें।  

अधिक जानकारी के लिए, [GroupDocs वेबसाइट](https://purchase.groupdocs.com/temporary-license/) देखें।

### बेसिक इनिशियलाइज़ेशन और सेटअप
`Redactor` क्लास सभी ऑपरेशन्स का एंट्री पॉइंट है, जिसमें मेटाडेटा निष्कर्षण भी शामिल है।

`Redactor` कोर क्लास है जो एक दस्तावेज़ इंस्टेंस को दर्शाता है और रेडैक्शन, जानकारी प्राप्ति, और फ़ाइल मैनिपुलेशन के मेथड्स प्रदान करता है। इंस्टॉल होने के बाद, आप नीचे दिखाए अनुसार एक `Redactor` ऑब्जेक्ट बना सकते हैं:

```csharp
using (Redactor redactor = new Redactor("your-document-path"))
{
    // Use the redactor here
}
```

अब लाइब्रेरी तैयार है, चलिए इम्प्लीमेंटेशन विवरण में डुबकी लगाते हैं।

## दस्तावेज़ स्ट्रीम से मेटाडेटा कैसे निकालें?
दस्तावेज़ को **रीड‑ओनली स्ट्रीम** के रूप में लोड करें, `Redactor` को इनिशियलाइज़ करें, और मेटाडेटा प्राप्त करने के लिए `GetDocumentInfo()` कॉल करें। यह तरीका पूरी फ़ाइल को मेमोरी में लोड करने से बचाता है, जो बड़े PDFs या सैकड़ों पेज वाले Office दस्तावेज़ों के लिए महत्वपूर्ण है।

**सीधा उत्तर:** फ़ाइल को `File.OpenRead()` से खोलें, स्ट्रीम को `new Redactor(stream)` में पास करें, फिर `redactor.GetDocumentInfo()` कॉल करें – यह मेथड केवल तीन लाइनों के कोड में फ़ाइल प्रकार, पेज काउंट, और आकार वाली ऑब्जेक्ट लौटाता है।

### चरण 1: स्रोत फ़ाइल पथ तैयार करें
सबसे पहले, सुनिश्चित करें कि स्रोत फ़ाइल मौजूद है और आउटपुट फ़ोल्डर तैयार है। नीचे दिया गया हेल्पर मेथड आउटपुट डायरेक्टरी की जाँच करता है और यदि आवश्यक हो तो उसे बनाता है।

```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

*क्यों?* यह बाद के फ़ाइल ऑपरेशन्स के लिए एक वैध पथ सुनिश्चित करता है और `DirectoryNotFoundException` को रोकता है।

### चरण 2: दस्तावेज़ स्ट्रीम खोलें
`File.OpenRead()` का उपयोग करके फ़ाइल को **रीड‑ओनली स्ट्रीम** के रूप में खोला जाता है, जिससे गीगाबाइट‑साइज़ फ़ाइलों के लिए भी मेमोरी उपयोग कम रहता है।

```csharp
using (Stream documentStream = File.OpenRead(sourceFile))
{
    // Proceed to initialize Redactor
}
```

*क्यों?* स्ट्रीम ऑन‑द‑फ्लाई प्रोसेसिंग को सक्षम करती हैं, जिससे आप पूरे दस्तावेज़ के बजाय फ़ाइल के हिस्सों के साथ काम कर सकते हैं।

### चरण 3: दस्तावेज़ स्ट्रीम के साथ Redactor को इनिशियलाइज़ करें
`Redactor` मुख्य API ऑब्जेक्ट है जो आपको दस्तावेज़‑स्तर के ऑपरेशन्स तक पहुँच देता है, जिसमें मेटाडेटा निष्कर्षण भी शामिल है।

`Redactor` एक स्ट्रीम से लोड किए गए एकल दस्तावेज़ को दर्शाता है और `GetDocumentInfo()` जैसे मेथड्स को तेज़ प्रॉपर्टी रिट्रीवल के लिए उजागर करता है।  

```csharp
using (Redactor redactor = new Redactor(documentStream))
{
    // Extract document info next
}
```

*क्यों?* स्ट्रीम के साथ `Redactor` को इंस्टैंशिएट करने से ऑब्जेक्ट मूल फ़ाइल से जुड़ता है बिना पूरी तरह लोड किए।

### चरण 4: दस्तावेज़ मेटाडेटा प्राप्त करें
`GetDocumentInfo()` कॉल करने से एक `DocumentInfo` ऑब्जेक्ट मिलता है जो फ़ाइल फ़ॉर्मेट, पेज काउंट, और फ़ाइल साइज रखता है।

`GetDocumentInfo()` एक ही कॉल में कोर प्रॉपर्टीज़ (फ़ॉर्मेट, पेज काउंट, साइज) निकालता है, जिससे अलग-अलग पार्सर्स की आवश्यकता समाप्त हो जाती है।  

```csharp
IDocumentInfo info = redactor.GetDocumentInfo();
string fileInfo = $"\nFile type: {info.FileType}\nNumber of pages: {info.PageCount}\nDocument size: {info.Size} bytes";
Console.WriteLine(fileInfo);
```

*क्यों?* यह चरण सभी आवश्यक मेटाडेटा को एकत्रित करता है, जिससे उनके गुणों के आधार पर दस्तावेज़ को लॉग, फ़िल्टर या रूट करना आसान हो जाता है।

## प्रोसेस्ड फ़ाइलों के लिए आउटपुट डायरेक्टरी कैसे तैयार करें?
किसी भी प्रोसेस्ड फ़ाइल को लिखने से पहले, सुनिश्चित करें कि लक्ष्य फ़ोल्डर मौजूद है और लिखने योग्य है। प्रोग्रामेटिकली पाथ की जाँच करके और यदि गायब हो तो उसे बनाकर, आप सामान्य रनटाइम एक्सेप्शन जैसे `DirectoryNotFoundException` या परमिशन एरर से बचते हैं। यह सरल चरण आपके कोड को विभिन्न वातावरणों में पोर्टेबल बनाता है, चाहे वह लोकली, सर्वर पर या कंटेनर में चल रहा हो।

**सीधा उत्तर:** फ़ोल्डर की जाँच के लिए `Directory.Exists()` का उपयोग करें और यदि वह मौजूद नहीं है तो `Directory.CreateDirectory()` से बनाएं – यह एक‑लाइन चेक किसी भी राइट ऑपरेशन से पहले वैध पथ सुनिश्चित करता है।

### एक हेल्पर मेथड लागू करें
नीचे दिया गया मेथड चेक‑एंड‑क्रिएट लॉजिक को एन्कैप्सुलेट करता है, और बाद में उपयोग के लिए सत्यापित पाथ लौटाता है।

```csharp
public static class Utils
{
    public static string PrepareOutputDirectory(string sampleDocPath)
    {
        string directory = Path.GetDirectoryName(sampleDocPath);
        
        if (!Directory.Exists(directory))
        {
            Directory.CreateDirectory(directory);
        }
        
        return Path.Combine(directory, "SAMPLE_DOCX.docx");
    }
}
```

*क्यों?* इस लॉजिक को केंद्रीकृत करने से डुप्लिकेशन कम होता है और कोडबेस को मेंटेन करना आसान हो जाता है।

## सामान्य समस्याएँ और समाधान
- **Permission errors:** सुनिश्चित करें कि एप्लिकेशन ऐसे अकाउंट के तहत चल रहा है जिसके पास लक्ष्य फ़ोल्डर में लिखने की अनुमति हो।  
- **Invalid paths:** पाथ सेपरेटर (`\\` Windows पर, `/` Linux/macOS पर) को दोबारा जांचें ताकि `DirectoryNotFoundException` से बचा जा सके।  
- **Large file handling:** स्ट्रीम्स को तुरंत डिस्पोज़ करें (`using` स्टेटमेंट्स) ताकि OS हैंडल्स मुक्त हों और लीक न हो।  

## व्यावहारिक अनुप्रयोग
1. **Automated Document Ingestion:** अपलोड पर मेटाडेटा निकालें, फिर तेज़ सर्च और कंप्लायंस रिपोर्टिंग के लिए इसे डेटाबेस में स्टोर करें।  
2. **Legal & Compliance Audits:** पेज काउंट और फ़ाइल टाइप्स निकालें ताकि दस्तावेज़ आर्काइव करने से पहले नियामक मानकों को पूरा करते हों, यह सत्यापित किया जा सके।  
3. **Enterprise Content Management:** मेटाडेटा का उपयोग करके फ़ाइलों को फ़ोल्डरों में ऑटो‑कैटेगराइज़ करें, जिससे संगठन और रिट्रीवल स्पीड बेहतर हो।  

## प्रदर्शन विचार
- **Memory Management:** हमेशा स्ट्रीम्स को `using` ब्लॉक्स में रैप करें ताकि वे स्वचालित रूप से डिस्पोज़ हो जाएँ।  
- **Batch Processing:** थ्रूपुट और मेमोरी उपयोग को संतुलित करने के लिए दस्तावेज़ों को 10‑20 के समूह में प्रोसेस करें, विशेषकर सीमित‑संसाधन सर्वरों पर।  
- **Parallelism:** स्वतंत्र फ़ाइलों के लिए `Parallel.ForEach` का उपयोग करें, लेकिन कंटेंशन से बचने के लिए CPU और I/O की निगरानी रखें।  

## निष्कर्ष
अब आपके पास GroupDocs.Redaction for .NET का उपयोग करके दस्तावेज़ स्ट्रीम से **मेटाडेटा कैसे निकालें** पर एक पूर्ण, प्रोडक्शन‑रेडी गाइड है। ऊपर दिए गए चरणों का पालन करके, आप फ़ाइल प्रकार, पेज काउंट, और साइज को कुशलता से प्राप्त कर सकते हैं, जबकि मेमोरी उपयोग कम रख सकते हैं और बड़े फ़ाइलों को सहजता से हैंडल कर सकते हैं।

## अगले कदम
- पूर्ण API रेफ़रेंस को [डॉक्यूमेंटेशन](https://docs.groupdocs.com/redaction/net/) में देखें।  
- [GroupDocs Redaction .NET Documentation](https://docs.groupdocs.com/redaction/net/) में गहराई से जाएँ ताकि रेडैक्शन, वाटरमार्किंग, और OCR फीचर्स का अन्वेषण कर सकें।  
- विभिन्न फ़ाइल फ़ॉर्मेट्स (PDF, DOCX, XLSX) के साथ प्रयोग करें ताकि देखें कि मेटाडेटा प्रकारों के अनुसार कैसे बदलता है।  
- निकाले गए मेटाडेटा को अपने मौजूदा दस्तावेज़ प्रबंधन या सर्च समाधान में इंटीग्रेट करें।  

## अक्सर पूछे जाने वाले प्रश्न

**Q: GroupDocs.Redaction की मेटाडेटा निष्कर्षण का मुख्य उपयोग केस क्या है?**  
A: यह फाइल को पूरी तरह खोलें बिना इंडेक्सिंग, कंप्लायंस चेक्स, और ऑटोमेटेड रूटिंग के लिए दस्तावेज़ प्रॉपर्टीज़ को तेज़, मेमोरी‑कुशल तरीके से प्राप्त करने में सक्षम बनाता है।

**Q: क्या मैं पासवर्ड‑प्रोटेक्टेड फ़ाइलों से मेटाडेटा निकाल सकता हूँ?**  
A: हाँ, `Redactor` ऑब्जेक्ट बनाते समय पासवर्ड प्रदान करें; API स्ट्रीम को आंतरिक रूप से डिक्रिप्ट करेगा।

**Q: क्या लाइब्रेरी PDF के अलावा DOCX या XLSX जैसे फॉर्मेट्स को सपोर्ट करती है?**  
A: बिल्कुल – GroupDocs.Redaction 30 से अधिक फ़ॉर्मेट्स को संभालती है, जिसमें PDF, DOCX, XLSX, PPTX, और सामान्य इमेज टाइप्स शामिल हैं।

**Q: स्ट्रीम्स के साथ मैं कितनी बड़ी दस्तावेज़ प्रोसेस कर सकता हूँ?**  
A: स्ट्रीम्स **2 GB** तक की फ़ाइलों को प्रोसेस करने की अनुमति देती हैं, जबकि मेमोरी खपत **50 MB** से कम रहती है, ऑन‑द‑फ्लाई रीडिंग के कारण।

**Q: यदि मुझे समस्याएँ आती हैं तो मैं मदद कहाँ से प्राप्त कर सकता हूँ?**  
A: समुदाय समर्थन के लिए [GroupDocs फ़ोरम](https://forum.groupdocs.com/c/redaction/33) देखें, या ट्रबलशूटिंग टिप्स के लिए आधिकारिक डॉक्यूमेंटेशन पर सलाह लें।

---

**अंतिम अपडेट:** 2026-06-11  
**परीक्षित संस्करण:** GroupDocs.Redaction 23.12 for .NET  
**लेखक:** GroupDocs  

**संसाधन**  
- **डॉक्यूमेंटेशन:** [GroupDocs Redaction .NET Documentation](https://docs.groupdocs.com/redaction/net/)  
- **API रेफ़रेंस:** [GroupDocs Redaction API Reference](https://reference.groupdocs.com/redaction/net)  
- **डाउनलोड:** [Latest GroupDocs Releases](https://releases.groupdocs.com/redaction/net)

## संबंधित ट्यूटोरियल
- [GroupDocs.Redaction .NET API के साथ मास्टर डॉक्यूमेंट मेटाडेटा रिट्रीवल](/redaction/net/document-information/groupdocs-redaction-net-document-metadata-retrieval/)
- [GroupDocs.Redaction for .NET का उपयोग करके डॉक्यूमेंट मेटाडेटा को रेडैक्ट कैसे करें - एक व्यापक गाइड](/redaction/net/metadata-redaction/redact-metadata-groupdocs-redaction-net/)
- [.NET में स्ट्रीम्स का उपयोग करके सुरक्षित डॉक्यूमेंट रेडैक्शन: GroupDocs.Redaction के लिए गाइड](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)