---
date: '2026-07-20'
description: GroupDocs.Redaction .NET का उपयोग करके फ़ॉर्मैट कैसे सूचीबद्ध करें, इस
  फीचर को अपने दस्तावेज़ वर्कफ़्लो में एकीकृत करें, और प्रदर्शन को बेहतर बनाएं।
keywords:
- how to list formats
- GroupDocs.Redaction supported formats
- .NET document processing
lastmod: '2026-07-20'
og_description: GroupDocs.Redaction .NET का उपयोग करके फ़ॉर्मैट कैसे सूचीबद्ध करें,
  स्टेप‑बाय‑स्टेप गाइड देखें, और अपने .NET एप्लिकेशन्स में इष्टतम प्रदर्शन के लिए
  टिप्स प्राप्त करें।
og_image_alt: Guide showing how to list supported file formats with GroupDocs.Redaction
  in a .NET project
og_title: GroupDocs.Redaction .NET के साथ फ़ॉर्मैट कैसे सूचीबद्ध करें
schemas:
- author: GroupDocs
  dateModified: '2026-07-20'
  description: Learn how to list formats using GroupDocs.Redaction .NET, integrate
    the feature into your document workflow, and improve performance.
  headline: How to List Formats with GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to list formats using GroupDocs.Redaction .NET, integrate
    the feature into your document workflow, and improve performance.
  name: How to List Formats with GroupDocs.Redaction .NET
  steps:
  - name: '**Document Management Systems** – Validate uploads against the supported
      list to prevent processing failures.'
    text: '**Document Management Systems** – Validate uploads against the supported
      list to prevent processing failures.'
  - name: '**Content Security** – Apply redaction rules only to file types that the
      engine can safely modify.'
    text: '**Content Security** – Apply redaction rules only to file types that the
      engine can safely modify.'
  - name: '**Batch Processing Pipelines** – Filter large file batches before invoking
      redaction, saving CPU and memory.'
    text: '**Batch Processing Pipelines** – Filter large file batches before invoking
      redaction, saving CPU and memory.'
  - name: '**How do I install GroupDocs.Redaction for .NET?**'
    text: '**How do I install GroupDocs.Redaction for .NET?**'
  - name: '**What are some common issues when retrieving supported formats?**'
    text: '**What are some common issues when retrieving supported formats?**'
  - name: '**Can I use this feature with non‑.NET applications?**'
    text: '**Can I use this feature with non‑.NET applications?**'
  - name: '**How can I optimise performance when using GroupDocs.Redaction?**'
    text: '**How can I optimise performance when using GroupDocs.Redaction?**'
  - name: '**What file types does GroupDocs.Redaction support?**'
    text: '**What file types does GroupDocs.Redaction support?**'
  type: HowTo
- questions:
  - answer: Yes, `FileType.GetSupportedFileFormats()` is static and does not require
      a `Redactor` object.
    question: Can I retrieve the format list without initializing a Redactor instance?
  - answer: The method returns all formats that the library can both read and write;
      each `FileType` includes a `CanRead` and `CanWrite` flag.
    question: Does the list include both input and output formats?
  - answer: GroupDocs releases format updates with each library version; checking
      the list at runtime ensures you always have the latest set.
    question: How often is the supported format list updated?
  - answer: Yes, filter the collection where `format.Extension == ".pdf"` or where
      `format.Name.Contains("PDF")`.
    question: Is there a way to filter only PDF‑compatible formats?
  - answer: The method requires .NET Core 3.1 or later; earlier runtimes are not supported.
    question: Will this approach work on .NET Core 2.1?
  type: FAQPage
tags:
- how to list formats
- GroupDocs.Redaction
- .NET file handling
title: GroupDocs.Redaction .NET के साथ फ़ॉर्मैट कैसे सूचीबद्ध करें
type: docs
url: /hi/net/format-handling/groupdocs-redaction-net-supported-formats-listing/
weight: 1
---

# GroupDocs.Redaction .NET के साथ फ़ॉर्मेट सूचीबद्ध करने का तरीका

विविध प्रकार के दस्तावेज़ों को प्रबंधित करना उन डेवलपर्स की रोज़मर्रा की वास्तविकता है जो दस्तावेज़‑केंद्रित एप्लिकेशन बनाते हैं। इस ट्यूटोरियल में आप सीखेंगे **फ़ॉर्मेट सूचीबद्ध करने का तरीका** कि GroupDocs.Redaction .NET किन फ़ॉर्मेट को संभाल सकता है, ताकि आप प्रोसेसिंग से पहले फ़ाइलों को वैध कर सकें, उपयोगकर्ताओं को सटीक विकल्प प्रस्तुत कर सकें, और अपने वर्कफ़्लो को कुशल रख सकें।

## परिचय

कुशल दस्तावेज़ हैंडलिंग शुरू होती है यह जानने से कि आपकी लाइब्रेरी ठीक‑ठीक कौन‑से फ़ाइल प्रकारों का समर्थन करती है। GroupDocs.Redaction एक बिल्ट‑इन मेथड प्रदान करता है जो यह जानकारी प्राप्त करता है, जिससे आप डायनामिक UI एलिमेंट बना सकते हैं, वैधता नियम लागू कर सकते हैं, और रन‑टाइम त्रुटियों से बच सकते हैं। नीचे आप सब कुछ पाएँगे जो आपको इंस्टॉलेशन से लेकर व्यावहारिक कोड स्निपेट्स और प्रदर्शन टिप्स तक, शुरू करने के लिए आवश्यक है।

### त्वरित उत्तर
- **“how to list formats” का क्या अर्थ है?** यह GroupDocs.Redaction द्वारा प्रोसेस किए जा सकने वाले फ़ाइल एक्सटेंशन के संग्रह को प्राप्त करने को दर्शाता है।  
- **क्या मुझे लाइसेंस चाहिए?** हाँ, प्रोडक्शन उपयोग के लिए एक वैध GroupDocs.Redaction लाइसेंस आवश्यक है।  
- **कौन‑से .NET संस्करण समर्थित हैं?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7।  
- **कितने फ़ॉर्मेट उपलब्ध हैं?** बॉक्स से बाहर 30 से अधिक इनपुट और आउटपुट फ़ॉर्मेट समर्थित हैं।  
- **क्या कोई विशेष कॉन्फ़िगरेशन आवश्यक है?** मानक लाइब्रेरी इनिशियलाइज़ेशन के अलावा कोई अतिरिक्त कॉन्फ़िगरेशन आवश्यक नहीं है।

## “how to list formats” क्या है?

यह लाइब्रेरी के FileType API को कॉल करके एक संग्रह प्राप्त करने से संबंधित है, जहाँ प्रत्येक एंट्री में फ़ाइल एक्सटेंशन और एक मानव‑पठनीय नाम शामिल होता है। डेवलपर्स फिर इस संग्रह को इटररेट करके वैधता नियम बना सकते हैं, UI ड्रॉपडाउन भर सकते हैं, या समर्थित प्रकारों को लॉग कर सकते हैं, यह सुनिश्चित करते हुए कि केवल संगत दस्तावेज़ प्रोसेस किए जाएँ।

## GroupDocs.Redaction के साथ फ़ॉर्मेट सूचीबद्ध क्यों करें?

GroupDocs.Redaction **30+** विभिन्न फ़ाइल प्रकारों—जैसे PDF, DOCX, PPTX, और इमेज फ़ॉर्मेट—का समर्थन करता है, जिससे आप अधिकांश एंटरप्राइज़ दस्तावेज़ बिना थर्ड‑पार्टी कन्वर्टर्स के संभाल सकते हैं। इन फ़ॉर्मेट को प्रोग्रामेटिकली सूचीबद्ध करके आप अनुमान को समाप्त करते हैं, सपोर्ट टिकट कम करते हैं, और यह सुनिश्चित करते हैं कि केवल संगत फ़ाइलें आपके प्रोसेसिंग पाइपलाइन में प्रवेश करें।

## आवश्यकताएँ

- **GroupDocs.Redaction for .NET** – आधिकारिक साइट से नवीनतम पैकेज डाउनलोड करें।  
- **.NET Framework or .NET Core** – आपके विकास वातावरण के साथ संगत।  
- **Visual Studio** (या कोई भी C#‑संगत IDE)।  
- C# सिंटैक्स की बुनियादी परिचितता।

## GroupDocs.Redaction for .NET सेटअप करना

### .NET CLI
`dotnet add package GroupDocs.Redaction`

### पैकेज मैनेजर
`Install-Package GroupDocs.Redaction`

### NuGet पैकेज मैनेजर UI
- **“GroupDocs.Redaction”** खोजें और नवीनतम संस्करण स्थापित करें।

### लाइसेंस प्राप्ति
GroupDocs एक फ्री ट्रायल, मूल्यांकन के लिए अस्थायी लाइसेंस, या पूर्ण‑खरीद विकल्प प्रदान करता है। उपयुक्त लाइसेंस फ़ाइल प्राप्त करने के लिए GroupDocs वेबसाइट पर जाएँ।

### बुनियादी इनिशियलाइज़ेशन और सेटअप
पैकेज जोड़ने के बाद, नेमस्पेस को रेफ़रेंस करें और एक `Redactor` इंस्टेंस बनाएँ:

```csharp
using GroupDocs.Redaction;

// Initialize with a license file (replace path as needed)
Redactor redactor = new Redactor("path/to/license/file.lic");
```

## कार्यान्वयन गाइड

### मैं GroupDocs.Redaction .NET के साथ फ़ॉर्मेट कैसे सूचीबद्ध करूँ?
लाइब्रेरी लोड करें, स्थैतिक हेल्पर को कॉल करें, और परिणामों को सॉर्ट करें—यह दो लाइनों के कोड में एक तैयार‑उपयोग संग्रह देता है। `FileType.GetSupportedFileFormats()` का उपयोग करके एक `IEnumerable<FileType>` प्राप्त करें जिसमें प्रत्येक फ़ॉर्मेट का एक्सटेंशन और डिस्प्ले नाम शामिल है, फिर UI सूची को साफ़ रखने के लिए एक्सटेंशन के अनुसार क्रमबद्ध करें।

### समर्थित फ़ाइल फ़ॉर्मेट प्राप्त करना

#### अवलोकन
उद्देश्य यह है कि GroupDocs.Redaction द्वारा संभाले जा सकने वाले फ़ाइल प्रकारों की सूची प्राप्त की जाए, जिससे वैधता लॉजिक, UI ड्रॉपडाउन, या लॉगिंग मैकेनिज़्म में एकीकरण आसान हो सके।

#### चरण‑दर‑चरण कार्यान्वयन

**1. Retrieve Supported File Types**  
`FileType.GetSupportedFileFormats()` लाइब्रेरी द्वारा पहचाने गए प्रत्येक फ़ॉर्मेट को लौटाता है। यह मेथड `GroupDocs.Redaction.FileType` क्लास का हिस्सा है, जो फ़ाइल एक्सटेंशन और फ्रेंडली नाम जैसी मेटाडेटा को समेटे हुए है।

**2. Display Supported File Types**  
संग्रह को इटररेट करें और प्रत्येक फ़ॉर्मेट का एक्सटेंशन और विवरण आउटपुट करें। इनलाइन कोड उदाहरण:

```csharp
var formats = FileType.GetSupportedFileFormats()
                      .OrderBy(f => f.Extension);

foreach (var format in formats)
{
    Console.WriteLine($"{format.Extension} – {format.Name}");
}
```

यह स्निपेट “.pdf – Portable Document Format” जैसा व्यवस्थित सूची प्रिंट करता है, जिससे UI एलिमेंट्स को भरना आसान हो जाता है।

### समस्या निवारण टिप्स
- **Missing Package** – NuGet पैकेज रेफ़रेंस की जाँच करें और आवश्यक होने पर पैकेज रीस्टोर करें।  
- **Incorrect License Path** – लाइसेंस फ़ाइल को आउटपुट डायरेक्टरी में कॉपी किया गया है या पूर्ण पाथ प्रदान किया गया है, यह सुनिश्चित करें।  
- **Unsupported Extension** – यदि कोई फ़ॉर्मेट सूचीबद्ध नहीं है, तो सुनिश्चित करें कि आप नवीनतम लाइब्रेरी संस्करण उपयोग कर रहे हैं; नए रिलीज़ अतिरिक्त फ़ॉर्मेट जोड़ते हैं।

## व्यावहारिक अनुप्रयोग
समर्थित फ़ाइल फ़ॉर्मेट को समझना कई वास्तविक‑दुनिया परिदृश्यों को खोलता है:

1. **Document Management Systems** – अपलोड को समर्थित सूची के विरुद्ध वैध करें ताकि प्रोसेसिंग विफलताओं से बचा जा सके।  
2. **Content Security** – रेडैक्शन नियम केवल उन फ़ाइल प्रकारों पर लागू करें जिन्हें इंजन सुरक्षित रूप से संशोधित कर सकता है।  
3. **Batch Processing Pipelines** – बड़े फ़ाइल बैच को रेडैक्शन कॉल करने से पहले फ़िल्टर करें, जिससे CPU और मेमोरी बचती है।

## प्रदर्शन विचार
- **Memory Footprint** – फ़ॉर्मेट सूचीबद्ध करना एक हल्का ऑपरेशन है; यह किसी भी दस्तावेज़ को मेमोरी में लोड नहीं करता।  
- **Batch Operations** – सैकड़ों फ़ाइलों को प्रोसेस करते समय फ़ॉर्मेट सूची को एक बार प्राप्त करें और पुन: उपयोग करें ताकि अनावश्यक कॉल से बचा जा सके।  
- **Thread Safety** – `FileType.GetSupportedFileFormats()` थ्रेड‑सेफ़ है और इसे समानांतर टास्क से सिंक्रोनाइज़ेशन के बिना कॉल किया जा सकता है।

## निष्कर्ष
आप अब GroupDocs.Redaction .NET का उपयोग करके **फ़ॉर्मेट सूचीबद्ध करने** का एक पूर्ण, प्रोडक्शन‑रेडी तरीका जानते हैं। इस फीचर को एकीकृत करके आप वैधता को बेहतर बना सकते हैं, उपयोगकर्ता अनुभव को सुधार सकते हैं, और अपने दस्तावेज़ पाइपलाइन को मजबूत रख सकते हैं।

### अगले कदम
- फ़ाइल प्रकार के आधार पर रेडैक्शन नियम लागू करने के लिए `Redactor` API का अन्वेषण करें।  
- फ़ॉर्मेट सूची को फ्रंट‑एंड ड्रॉपडाउन के साथ मिलाकर सहज फ़ाइल चयन प्रदान करें।  
- बड़े‑पैमाने पर बैच जॉब्स को अनुकूलित करने के लिए प्रदर्शन गाइड की समीक्षा करें।

## अक्सर पूछे जाने वाले प्रश्न

**Q: क्या मैं Redactor इंस्टेंस इनिशियलाइज़ किए बिना फ़ॉर्मेट सूची प्राप्त कर सकता हूँ?**  
A: हाँ, `FileType.GetSupportedFileFormats()` स्थैतिक है और `Redactor` ऑब्जेक्ट की आवश्यकता नहीं रखता।

**Q: क्या सूची में इनपुट और आउटपुट दोनों फ़ॉर्मेट शामिल हैं?**  
A: यह मेथड सभी फ़ॉर्मेट लौटाता है जिन्हें लाइब्रेरी पढ़ और लिख दोनों कर सकती है; प्रत्येक `FileType` में `CanRead` और `CanWrite` फ़्लैग शामिल होते हैं।

**Q: समर्थित फ़ॉर्मेट सूची कितनी बार अपडेट होती है?**  
A: GroupDocs प्रत्येक लाइब्रेरी संस्करण के साथ फ़ॉर्मेट अपडेट जारी करता है; रन‑टाइम पर सूची जाँचने से आप हमेशा नवीनतम सेट प्राप्त करते हैं।

**Q: क्या केवल PDF‑संगत फ़ॉर्मेट को फ़िल्टर करने का कोई तरीका है?**  
A: हाँ, संग्रह को `format.Extension == ".pdf"` या `format.Name.Contains("PDF")` के आधार पर फ़िल्टर करें।

**Q: क्या यह तरीका .NET Core 2.1 पर काम करेगा?**  
A: यह मेथड .NET Core 3.1 या बाद के संस्करणों की आवश्यकता रखता है; पुराने रनटाइम समर्थित नहीं हैं।

## FAQ अनुभाग
1. **मैं GroupDocs.Redaction for .NET कैसे इंस्टॉल करूँ?**  
   CLI कमांड `dotnet add package GroupDocs.Redaction` या NuGet पैकेज मैनेजर UI से स्थापित करें।  
2. **समर्थित फ़ॉर्मेट प्राप्त करने में आम समस्याएँ क्या हैं?**  
   सभी डिपेंडेंसी रीस्टोर किए गए हैं और सही नेमस्पेस (`GroupDocs.Redaction`) रेफ़रेंस किया गया है, यह सुनिश्चित करें।  
3. **क्या मैं इस फीचर को गैर‑.NET एप्लिकेशन में उपयोग कर सकता हूँ?**  
   यह ट्यूटोरियल .NET पर केंद्रित है, लेकिन GroupDocs समान API Java, Python और अन्य प्लेटफ़ॉर्म के लिए भी प्रदान करता है।  
4. **GroupDocs.Redaction का उपयोग करते समय प्रदर्शन कैसे अनुकूलित करूँ?**  
   फ़ॉर्मेट सूची को पुन: उपयोग करें, केवल संगतता जाँच के लिए पूर्ण दस्तावेज़ लोड करने से बचें, और बैच जॉब्स के दौरान मेमोरी उपयोग की निगरानी करें।  
5. **GroupDocs.Redaction किन फ़ाइल प्रकारों का समर्थन करता है?**  
   लाइब्रेरी 30+ फ़ॉर्मेट का समर्थन करती है, जिसमें PDF, DOCX, PPTX, XLSX, BMP, PNG, JPEG आदि शामिल हैं। पूर्ण सूची के लिए `FileType.GetSupportedFileFormats()` का उपयोग करें।

## संसाधन
- [दस्तावेज़ीकरण](https://docs.groupdocs.com/redaction/net/)
- [API रेफ़रेंस](https://reference.groupdocs.com/redaction/net)
- [GroupDocs.Redaction डाउनलोड करें](https://releases.groupdocs.com/redaction/net/)
- [नि:शुल्क समर्थन फ़ोरम](https://forum.groupdocs.com/c/redaction/33)
- [अस्थायी लाइसेंस](https://purchase.groupdocs.com/temporary-license/)

**अंतिम अपडेट:** 2026-07-20  
**परीक्षित संस्करण:** GroupDocs.Redaction 4.2.0 for .NET  
**लेखक:** GroupDocs  

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

```csharp
using GroupDocs.Redaction;
// Initialize the Redactor with file path
Redactor redactor = new Redactor("sample.pdf");
```

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using GroupDocs.Redaction;

// Step 1: Use GroupDocs.Redaction API to fetch all supported formats.
IEnumerable<FileType> supportedFileTypes = FileType.GetSupportedFileFormats().OrderBy(f => f.Extension);
```

```csharp
// Step 2: Loop through the list of file types and print details.
foreach (FileType fileType in supportedFileTypes)
{
    Console.WriteLine($"{fileType.Extension} - {fileType.FileFormatName}");
}
```

## संबंधित ट्यूटोरियल

- [GroupDocs.Redaction .NET के लिए फ़ॉर्मेट हैंडलिंग ट्यूटोरियल](/redaction/net/format-handling/)
- [GroupDocs.Redaction for .NET के साथ डॉक्यूमेंट लोडिंग ट्यूटोरियल](/redaction/net/document-loading/)
- [GroupDocs.Redaction .NET के लिए डॉक्यूमेंट सेविंग ट्यूटोरियल](/redaction/net/document-saving/)