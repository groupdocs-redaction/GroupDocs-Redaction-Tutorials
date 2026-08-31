---
date: '2026-03-28'
description: GroupDocs.Redaction for .NET में कस्टम लॉगर C# को कैसे लागू करें, जिससे
  विस्तृत कस्टम लॉगिंग और आसान अनुपालन रिपोर्टिंग संभव हो।
keywords:
- custom logger c#
- custom logging .net
- save redacted document
- log warnings c#
title: .NET के लिए GroupDocs.Redaction में कस्टम लॉगर C# लागू करें
type: docs
url: /hi/net/advanced-redaction/custom-logging-groupdocs-redaction-net/
weight: 1
---

# GroupDocs.Redaction के लिए .NET में कस्टम लॉगर c# लागू करें

दस्तावेज़ रिडैक्शन को कुशलतापूर्वक प्रबंधित करना अत्यंत महत्वपूर्ण है, विशेष रूप से संवेदनशील जानकारी को संभालते समय। इस गाइड में आप GroupDocs.Redaction for .NET के साथ **कस्टम लॉगर c# को कैसे लागू करें** सीखेंगे, जिससे आपको लॉगिंग, त्रुटि प्रबंधन और ऑडिट ट्रेल्स पर पूर्ण नियंत्रण मिलेगा।

## त्वरित उत्तर
- **कस्टम लॉगर c# क्या करता है?** यह रिडैक्शन के दौरान त्रुटियों, चेतावनियों और सूचना संदेशों को कैप्चर करता है।  
- **कौन सी लाइब्रेरी ILogger इंटरफ़ेस प्रदान करती है?** GroupDocs.Redaction for .NET।  
- **क्या मैं रास्टराइज़ेशन के बिना रिडैक्टेड दस्तावेज़ सहेज सकता हूँ?** हाँ – `redactor.Save(..., new Options.RasterizationOptions { Enabled = false })` का उपयोग करें।  
- **क्या उत्पादन उपयोग के लिए लाइसेंस की आवश्यकता है?** उत्पादन के लिए पूर्ण लाइसेंस आवश्यक है; मूल्यांकन के लिए एक ट्रायल उपलब्ध है।  
- **क्या यह तरीका .NET Core / .NET 6+ के साथ संगत है?** बिल्कुल – वही API .NET Framework और .NET Core/5/6 में काम करता है।

## कस्टम लॉगर c# क्या है?
एक **कस्टम लॉगर c#** वह क्लास है जो GroupDocs.Redaction द्वारा प्रदान किए गए `ILogger` इंटरफ़ेस को लागू करता है। यह आपको लॉग संदेशों को जहाँ भी आवश्यक हो—कंसोल, फ़ाइल, डेटाबेस, या बाहरी मॉनिटरिंग सिस्टम—पर रूट करने की सुविधा देता है, साथ ही रिडैक्शन वर्कफ़्लो का स्पष्ट दृश्य प्रदान करता है।

## GroupDocs.Redaction के साथ कस्टम लॉगिंग .net क्यों उपयोग करें?
- **अनुपालन एवं ऑडिटिंग:** विस्तृत लॉग नियामक आवश्यकताओं को पूरा करते हैं।  
- **त्रुटि दृश्यता:** `LogError` और `LogWarning` समस्याओं पर तुरंत प्रतिक्रिया देते हैं।  
- **एकीकरण लचीलापन:** लॉग को मौजूदा .NET लॉगिंग फ्रेमवर्क (Serilog, NLog, आदि) में फ़ॉरवर्ड करें।  

## पूर्वापेक्षाएँ
- **GroupDocs.Redaction for .NET** स्थापित हो (नीचे इंस्टॉलेशन देखें)।  
- एक .NET विकास वातावरण (Visual Studio, VS Code, या CLI)।  
- बेसिक C# ज्ञान और फ़ाइल स्ट्रीम्स की परिचितता।  

## इंस्टॉलेशन

**.NET CLI**
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
**"GroupDocs.Redaction"** को खोजें और नवीनतम संस्करण स्थापित करें।

## लाइसेंस प्राप्ति
- **फ्री ट्रायल:** अस्थायी लाइसेंस के साथ API का परीक्षण करें।  
- **टेम्पररी लाइसेंस:** सीमित अवधि के लिए सभी फीचर एक्सेस प्राप्त करें।  
- **खरीद:** उत्पादन डिप्लॉयमेंट के लिए स्थायी लाइसेंस प्राप्त करें।

## चरण‑दर‑चरण गाइड

### चरण 1: कस्टम लॉगर क्लास परिभाषित करें (log warnings c#)
`ILogger` को लागू करने वाली क्लास बनाएं। यह क्लास त्रुटियों, चेतावनियों और सूचना संदेशों को कैप्चर करेगी।

```csharp
using System;
using GroupDocs.Redaction;

class CustomLogger : ILogger
{
    public bool HasErrors { get; private set; }

    // Log errors encountered during processing.
    public void LogError(string message)
    {
        Console.WriteLine("Error: " + message);
        HasErrors = true;
    }

    // Log warnings that may not be critical but need attention.
    public void LogWarning(string message)
    {
        Console.WriteLine("Warning: " + message);
    }

    // Log informational messages for tracking normal operations.
    public void LogInfo(string message)
    {
        Console.WriteLine("Info: " + message);
    }
}
```

**व्याख्या:** `HasErrors` फ़्लैग आपको यह तय करने में मदद करता है कि प्रोसेसिंग जारी रखनी है या नहीं। ये तीन मेथड्स अधिकांश रिडैक्शन परिदृश्यों में आवश्यक तीन लॉग लेवल्स के अनुरूप हैं।

### चरण 2: फ़ाइल पाथ तैयार करें और स्रोत दस्तावेज़ खोलें
```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
string outputFile = Utils.GetOutputFile(sourceFile);
```

**यह क्यों महत्वपूर्ण है:** यूटिलिटी मेथड्स का उपयोग आपके कोड को साफ़ रखता है और यह सुनिश्चित करता है कि आउटपुट फ़ोल्डर मौजूद हो, इससे पहले कि आप **रिडैक्टेड दस्तावेज़ सहेजें**।

### चरण 3: कस्टम लॉगर का उपयोग करते हुए रिडैक्शन लागू करें
```csharp
using (Stream stream = File.Open(sourceFile, FileMode.Open, FileAccess.ReadWrite))
{
    var logger = new CustomLogger();
    
    using (Redactor redactor = new Redactor(stream, new LoadOptions(), new RedactorSettings(logger)))
    {
        // Apply a redaction to the document.
        redactor.Apply(new DeleteAnnotationRedaction());
        
        if (!logger.HasErrors)
        {
            using (Stream streamOut = File.Open(outputFile, FileMode.OpenOrCreate, FileAccess.ReadWrite))
            {
                // Save changes without rasterizing the output.
                redactor.Save(streamOut, new Options.RasterizationOptions { Enabled = false });
            }
        }
    }
}
```

**व्याख्या:**  
1. `Redactor` को `RedactorSettings(logger)` के साथ इंस्टैंशिएट किया जाता है, जिससे आपका `CustomLogger` जुड़ता है।  
2. रिडैक्शन लागू करने के बाद, कोड `logger.HasErrors` की जाँच करता है। यदि कोई त्रुटि नहीं हुई, तो दस्तावेज़ सहेजा जाता है—जो **रिडैक्टेड दस्तावेज़ सहेजें** लॉजिक को रास्टराइज़ेशन के बिना दर्शाता है।

### सामान्य कठिनाइयाँ और समस्या निवारण
- **लॉग आउटपुट गायब:** सुनिश्चित करें कि प्रत्येक `Log*` मेथड सही तरीके से ओवरराइड किया गया है।  
- **फ़ाइल एक्सेस अपवाद:** सुनिश्चित करें कि एप्लिकेशन के पास स्रोत और आउटपुट पाथ दोनों के लिए पढ़ने/लिखने की अनुमति है।  
- **लॉगर नहीं जुड़ा:** `RedactorSettings(logger)` पैरामीटर आवश्यक है; इसे छोड़ने से कस्टम लॉगिंग निष्क्रिय हो जाती है।

## व्यावहारिक अनुप्रयोग
1. **अनुपालन रिपोर्टिंग:** ऑडिट ट्रेल्स के लिए लॉग एंट्रीज़ को CSV या डेटाबेस में एक्सपोर्ट करें।  
2. **त्रुटि ट्रैकिंग:** `LogError` आउटपुट को स्कैन करके समस्याग्रस्त फ़ाइलें जल्दी ढूँढ़ें।  
3. **वर्कफ़्लो ऑटोमेशन:** जब `LogWarning` कॉल किया जाए तो डाउनस्ट्रीम प्रोसेस (जैसे, अनुपालन अधिकारी को सूचित करना) ट्रिगर करें।

## प्रदर्शन संबंधी विचार
- **स्ट्रीम्स को तुरंत डिस्पोज़ करें** ताकि मेमोरी मुक्त हो, विशेषकर बड़े बैच प्रोसेसिंग के समय।  
- **CPU और मेमोरी की निगरानी** करें जब बड़े पैमाने पर रिडैक्शन हो; लॉगर सिंक्रोनाइज़ेशन का ध्यान रखते हुए समानांतर में दस्तावेज़ प्रोसेस करने पर विचार करें।  
- **अपडेट रहें:** GroupDocs.Redaction के नए संस्करण अक्सर प्रदर्शन अनुकूलन और अतिरिक्त लॉगिंग हुक शामिल करते हैं।

## निष्कर्ष
**कस्टम लॉगर c#** को लागू करके, आपको रिडैक्शन पाइपलाइन के हर चरण में विस्तृत अंतर्दृष्टि मिलती है, जिससे अनुपालन मानकों को पूरा करना और समस्याओं का डीबग करना आसान हो जाता है। यहाँ दिखाया गया तरीका GroupDocs.Redaction for .NET के साथ सहजता से काम करता है और इसे किसी भी .NET लॉगिंग फ्रेमवर्क के साथ एकीकृत किया जा सकता है जिसे आप पहले से उपयोग कर रहे हैं।

---

## अक्सर पूछे जाने वाले प्रश्न

**Q: GroupDocs.Redaction के साथ कस्टम लॉगिंग का उद्देश्य क्या है?**  
A: कस्टम लॉगिंग अनुपालन, त्रुटि ट्रैकिंग और वर्कफ़्लो अनुकूलन के लिए रिडैक्शन को ट्रैक और प्रबंधित करने में मदद करती है।

**Q: कस्टम लॉगर का उपयोग करके त्रुटियों को कैसे संभालें?**  
A: अपने `CustomLogger` क्लास में `LogError` लागू करें; `HasErrors` फ़्लैग आवश्यक होने पर प्रोसेसिंग को रोकने की अनुमति देता है।

**Q: क्या कस्टम लॉगिंग को अन्य सिस्टमों के साथ एकीकृत किया जा सकता है?**  
A: हाँ, लॉगर मेथड्स को विस्तारित करके आप लॉग संदेशों को CRM, ERP या केंद्रीकृत मॉनिटरिंग टूल्स में फ़ॉरवर्ड कर सकते हैं।

**Q: कस्टम लॉगिंग लागू करते समय सामान्य कठिनाइयाँ क्या हैं?**  
A: गलत मेथड इम्प्लीमेंटेशन, `RedactorSettings(logger)` का अभाव, और फ़ाइल अनुमति समस्याएँ सबसे अधिक होती हैं।

**Q: कस्टम लॉगिंग दस्तावेज़ रिडैक्शन वर्कफ़्लो को कैसे सुधारती है?**  
A: विस्तृत लॉग रियल‑टाइम दृश्यता प्रदान करते हैं, समस्या निवारण को सरल बनाते हैं, और ऑडिट आवश्यकताओं को पूरा करते हैं।

## संसाधन
- **डॉक्यूमेंटेशन:** [GroupDocs.Redaction .NET Documentation](https://docs.groupdocs.com/redaction/net/)
- **API रेफ़रेंस:** [GroupDocs.Redaction API Reference](https://reference.groupdocs.com/redaction/net)
- **डाउनलोड:** [GroupDocs.Redaction for .NET](https://downloads.groupdocs.com/redaction/net)

---

**अंतिम अपडेट:** 2026-03-28  
**परीक्षण किया गया:** GroupDocs.Redaction 23.11 for .NET  
**लेखक:** GroupDocs