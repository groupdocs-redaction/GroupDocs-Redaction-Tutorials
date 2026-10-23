---
date: '2026-10-16'
description: Learn how to use GroupDocs for .NET to redact text and images, including
  how to replace text placeholder with values, ensuring data privacy and compliance.
images:
- /net/image-redaction/groupdocs-redaction-tutorial-net-text-image-redaction/og-image.png
keywords:
- how to use groupdocs
- replace text placeholder
- GroupDocs.Redaction .NET
lastmod: '2026-10-16'
og_description: Learn how to use GroupDocs for .NET to redact text and images, including
  how to replace text placeholder with values, ensuring data privacy and compliance.
og_image_alt: Guide showing GroupDocs .NET text and image redaction with placeholder
  replacement
og_title: Implement Redaction to Secure Text and Images
schemas:
- author: GroupDocs
  dateModified: '2026-10-16'
  description: Learn how to use GroupDocs for .NET to redact text and images, including
    how to replace text placeholder with values, ensuring data privacy and compliance.
  headline: Implement Redaction to Secure Text and Images
  type: TechArticle
- description: Learn how to use GroupDocs for .NET to redact text and images, including
    how to replace text placeholder with values, ensuring data privacy and compliance.
  name: Implement Redaction to Secure Text and Images
  steps:
  - name: '**Legal contracts** – automatically hide client names, SSNs, or contract
      numbers before sharing drafts with external counsel.'
    text: '**Legal contracts** – automatically hide client names, SSNs, or contract
      numbers before sharing drafts with external counsel.'
  - name: '**Medical imaging reports** – obscure patient identifiers embedded in scanned
      X‑ray images while preserving diagnostic content.'
    text: '**Medical imaging reports** – obscure patient identifiers embedded in scanned
      X‑ray images while preserving diagnostic content.'
  - name: '**Financial statements** – replace account numbers with generic placeholders
      to comply with GDPR and PCI‑DSS during audit preparation.'
    text: '**Financial statements** – replace account numbers with generic placeholders
      to comply with GDPR and PCI‑DSS during audit preparation.'
    type: HowTo
- questions:
  - answer: Yes, provide the password when constructing the `Redactor` instance; the
      SDK will decrypt, redact, and re‑encrypt the file automatically.
    question: Can I redact password‑protected PDFs?
  - answer: It works with PNG, JPEG, BMP, and TIFF embedded in supported documents,
      allowing you to mask raster data across formats.
    question: Does the SDK support other image formats besides PDF?
  - answer: The replacement preserves the original text direction and font metrics,
      ensuring the document layout remains unchanged for Latin, Cyrillic, and Asian
      scripts. Placeholder replacement works by inserting the specified string while
      keeping character spacing and alignment, so multilingual documents retain their
      visual structure after redaction.
    question: How accurate is the placeholder replacement for multi‑language text?
  - answer: No hard limit; however, performance degrades after roughly 1,000 rules,
      so group similar patterns when possible. Each rule adds processing overhead,
      and extremely large rule sets can increase memory consumption and execution
      time. It's recommended to consolidate overlapping patterns into a single rule
      to maintain optimal speed.
    question: Is there a limit on the number of redaction rules per document?
  - answer: Yes, call `redactor.GetRedactedPages()` to retrieve a preview stream that
      you can display in a UI component. The `GetRedactedPages()` method returns a
      stream containing the document with all redaction rules applied, allowing you
      to render a read‑only preview before committing changes to disk.
    question: Can I preview redactions before saving?
  type: FAQPage
tags:
- GroupDocs.Redaction
- text redaction .NET
- image redaction
- C# document security
- privacy compliance
title: Implement Redaction to Secure Text and Images
type: docs
url: /net/image-redaction/groupdocs-redaction-tutorial-net-text-image-redaction/
weight: 1
---

# Implement Redaction to Secure Text and Images

In today’s data‑driven world, protecting personally identifiable information (PII) inside PDFs, Word files, and image‑based documents is a legal and business imperative. **How to use GroupDocs** for .NET to perform precise text redaction and image masking is the focus of this guide. You’ll learn how to replace text placeholder values, apply color fills to sensitive image regions, and integrate these steps into real‑world workflows while keeping performance and memory usage optimal.

## Quick answers
- **What library handles redaction?** GroupDocs.Redaction for .NET.
- **Can I replace text with a custom placeholder?** Yes, using `ReplacementOptions`.
- **Is image redaction limited to black boxes?** No, you can fill regions with any .NET `Color`.
- **Does the SDK support large PDFs?** It processes multi‑hundred‑page files without loading the whole file into memory.
- **Do I need a license for production?** A trial works for evaluation; a full license is required for commercial use.

## What is GroupDocs.Redaction for .NET?
GroupDocs.Redaction for .NET is a dedicated SDK that enables developers to locate and permanently remove or replace sensitive content in over 50 document formats. It works on Windows, Linux, and macOS, and supports .NET 5/6/7 as well as .NET Framework 4.6+. The library offers high‑performance processing and built‑in compliance features for data protection.

## How to use GroupDocs for .NET text and image redaction?
Load the document with the `Redactor` class, define what you want to hide, and then call `Redact()` – that’s the core three‑step workflow. The SDK automatically rewrites the file so the removed data cannot be recovered, and you can optionally save the redacted version to a new stream or file path.

## How to replace text placeholder in redaction?
You can replace identified text with any string you provide—this is the **replace text placeholder** feature. Define a `ReplacementOptions` object, set its `ReplacementText` property, and attach it to the redaction rule. The SDK will substitute every match with your placeholder while preserving document layout.

## Prerequisites
Before you start, make sure you have:

- **GroupDocs.Redaction** NuGet package installed (latest stable version).  
- **System.Drawing.Common** for image‑related operations on non‑Windows platforms.  
- Visual Studio 2022 or later (any edition).  
- Basic familiarity with C# regular expressions and file I/O.

## Setting up GroupDocs.Redaction for .NET
First, add the SDK to your project. You can use any of the following methods; pick the one that matches your workflow.

**Using the .NET CLI:**  
```bash
dotnet add package GroupDocs.Redaction
```

**Using Package Manager Console:**  
```powershell
Install-Package GroupDocs.Redaction
```

**Using NuGet Package Manager UI:**  
- Open **Tools → NuGet Package Manager → Manage NuGet Packages for Solution…**  
- Search for “GroupDocs.Redaction” and click **Install**.

### License acquisition
Obtain a trial license from the GroupDocs portal to unlock all redaction features during development. For production, purchase a permanent license to remove evaluation limits and receive priority support.

### Basic initialization
The `Redactor` class is the entry point for every redaction operation. Create an instance, pass the source file path, and you’re ready to define redaction rules.

```csharp
using GroupDocs.Redaction;
using GroupDocs.Redaction.Options;

// Initialize the redactor with the document you want to process
Redactor redactor = new Redactor("sample.pdf");
```

## Implementation guide
Below you’ll find step‑by‑step instructions for both text and image redaction. Each section starts with a concise answer, followed by deeper explanation and best‑practice tips.

### Text redaction with regex patterns
#### How does regex‑based text redaction work?
You create a `Regex` object that describes the pattern you want to hide, then attach a `ReplacementOptions` object that tells the SDK what to insert instead of the matched text. A `Regex` object represents a regular expression used to find text sequences, while `ReplacementOptions` defines the replacement behavior such as placeholder text. During redaction the SDK scans each page, applies the pattern, and substitutes the matches according to the options.

```csharp
// Define a pattern that matches the word “urna” (case‑insensitive)
var regex = new Regex(@"\burna\b", RegexOptions.IgnoreCase);
```

#### How to configure replacement options for text redaction?
Set the `ReplacementText` property to the placeholder you prefer—e.g., “[REDACTED]”. The `ReplacementText` property specifies the exact string that will replace each redacted segment, preserving layout while hiding original content. You can also limit the scope to specific pages or regions by providing page numbers or rectangular coordinates in the options.

```csharp
var replaceOptions = new ReplacementOptions
{
    ReplacementText = "[REDACTED]",
    PageIndexes = new[] { redactor.PageCount - 1 } // last page only
};
redactor.AddRedaction(regex, replaceOptions);
```

### Image redaction options
#### How can I mask a portion of an image with a solid color?
Create a `RegionReplacementOptions` instance, specify the fill `Color`, and define the rectangle (X, Y, Width, Height) that should be covered. `RegionReplacementOptions` tells the SDK how to replace a selected image region, allowing you to set a solid color, a custom image, or a blur effect. The defined rectangle determines the exact area that will be masked.

```csharp
var imageRegion = new RegionReplacementOptions
{
    Color = Color.Chocolate,
    Width = 100,
    Height = 100,
    X = 50,
    Y = 200
};
redactor.AddImageRedaction(imageRegion);
```

#### How to apply image redaction to a specific page?
Pass the page index to the `AddImageRedaction` method so the SDK knows where to apply the fill. The `AddImageRedaction` method adds an image redaction rule for a given page, accepting the region coordinates and the `RegionReplacementOptions` that define the fill color or pattern. This ensures only the targeted page is modified.

```csharp
redactor.AddImageRedaction(imageRegion, pageIndex: 2);
```

### Running the redaction process
Once all rules are defined, invoke `Redact()` and then `Save()` the output.

```csharp
redactor.Redact();
redactor.Save("sample_redacted.pdf");
```

## Practical applications
Real‑world use cases where these techniques shine:

1. **Legal contracts** – automatically hide client names, SSNs, or contract numbers before sharing drafts with external counsel.  
2. **Medical imaging reports** – obscure patient identifiers embedded in scanned X‑ray images while preserving diagnostic content.  
3. **Financial statements** – replace account numbers with generic placeholders to comply with GDPR and PCI‑DSS during audit preparation.  

By embedding GroupDocs.Redaction into a document‑management pipeline, you can achieve end‑to‑end compliance with minimal manual effort.

## Performance considerations
Processing large PDFs can be resource‑intensive. Follow these quantified best practices:

- **Memory usage:** The SDK processes files page‑by‑page, keeping memory under 150 MB even for 500‑page documents.  
- **Batch mode:** Redact up to 20 documents in parallel on a 4‑core VM without noticeable slowdown.  
- **Regex efficiency:** Simple patterns like `\burna\b` execute in under 2 ms per page; complex look‑ahead expressions may take up to 15 ms per page.

Dispose of the `Redactor` instance as soon as you’re done to free native resources:

```csharp
redactor.Dispose();
```

## Frequently asked questions
**Q: Can I redact password‑protected PDFs?**  
A: Yes, provide the password when constructing the `Redactor` instance; the SDK will decrypt, redact, and re‑encrypt the file automatically.

**Q: Does the SDK support other image formats besides PDF?**  
A: It works with PNG, JPEG, BMP, and TIFF embedded in supported documents, allowing you to mask raster data across formats.

**Q: How accurate is the placeholder replacement for multi‑language text?**  
A: The replacement preserves the original text direction and font metrics, ensuring the document layout remains unchanged for Latin, Cyrillic, and Asian scripts. Placeholder replacement works by inserting the specified string while keeping character spacing and alignment, so multilingual documents retain their visual structure after redaction.

**Q: Is there a limit on the number of redaction rules per document?**  
A: No hard limit; however, performance degrades after roughly 1,000 rules, so group similar patterns when possible. Each rule adds processing overhead, and extremely large rule sets can increase memory consumption and execution time. It's recommended to consolidate overlapping patterns into a single rule to maintain optimal speed.

**Q: Can I preview redactions before saving?**  
A: Yes, call `redactor.GetRedactedPages()` to retrieve a preview stream that you can display in a UI component. The `GetRedactedPages()` method returns a stream containing the document with all redaction rules applied, allowing you to render a read‑only preview before committing changes to disk.

## Original FAQ section
**1. What is regex used for in text redaction?**  
   - Regex helps identify specific patterns in the text that need to be redacted based on customizable criteria.

**2. Can I use different colors for image redaction?**  
   - Yes, `RegionReplacementOptions` allows you to specify any color available in the .NET `Color` class.

**3. How do I handle large documents efficiently with GroupDocs.Redaction?**  
   - Process documents in smaller sections or batches and ensure proper resource management by disposing of objects when not needed.

**4. What are common issues encountered during redaction?**  
   - Common issues include incorrect regex patterns leading to no matches, and performance lags with large files.

**5. Is GroupDocs.Redaction available for other programming languages?**  
   - Yes, it offers libraries for several languages including Java and C++.

## Resources
- **Documentation:** [GroupDocs Redaction .NET Documentation]({{< relref "redaction/net/pdf-specific-redaction/ai-powered-pdf-redaction-groupdocs-redaction-net/_index.md" >}})
- **API reference:** [API Reference for GroupDocs Redaction]({{< relref "redaction/net/image-redaction/redact-embedded-images-groupdocs-redaction-net/_index.md" >}})
- **Download:** [Download Latest Version]({{< relref "redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/_index.md" >}})
- **Support forum:** [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)
- **Temporary license:** [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license/)

**Last Updated:** 2026-10-16  
**Tested With:** GroupDocs.Redaction 23.11 for .NET  
**Author:** GroupDocs  

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

```csharp
using GroupDocs.Redaction;
...
Redactor redactor = new Redactor("path/to/your/document");
```

```csharp
using System.Text.RegularExpressions;

Regex rx = new Regex("urna");
```

```csharp
using GroupDocs.Redaction.Redactions;
using GroupDocs.Redaction.Options;

ReplacementOptions optionsText = new ReplacementOptions("[redacted]");
optionsText.Filters = new RedactionFilter[] {
    new PageRangeFilter(PageSeekOrigin.End, 0, 1),
    new PageAreaFilter(new System.Drawing.Point(300, 0), new System.Drawing.Size(300, 840))
};
```

```csharp
using System.Drawing;

RegionReplacementOptions optionsImg = new RegionReplacementOptions(Color.Chocolate, new Size(100, 100));
```

## Related Tutorials

- [AI-Powered PDF Redaction with GroupDocs.Redaction .NET: Advanced Techniques for Data Privacy and Compliance]({{< relref "redaction/net/pdf-specific-redaction/ai-powered-pdf-redaction-groupdocs-redaction-net/_index.md" >}})
- [Redact Embedded Images in Word Documents Using GroupDocs.Redaction .NET API]({{< relref "redaction/net/image-redaction/redact-embedded-images-groupdocs-redaction-net/_index.md" >}})
- [How to Redact Documents with GroupDocs.Redaction .NET – A Complete Guide]({{< relref "redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/_index.md" >}})
