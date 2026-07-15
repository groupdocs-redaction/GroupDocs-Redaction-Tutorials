---
title: "How to Export Redacted Documents with GroupDocs.Redaction .NET"
description: "Learn how to export redacted files, configure output folders, create rasterized PDFs, and save to streams using GroupDocs.Redaction for .NET."
weight: 3
url: "/net/document-saving/"
type: docs
date: 2026-06-11
keywords:
  - how to export redacted
  - configure output folder
  - create rasterized pdf
  - save rasterized pdf
  - convert redacted to pdf
schemas:
- type: TechArticle
  headline: How to Export Redacted Documents with GroupDocs.Redaction .NET
  description: Learn how to export redacted files, configure output folders, create
    rasterized PDFs, and save to streams using GroupDocs.Redaction for .NET.
  dateModified: '2026-06-11'
  author: GroupDocs
- type: HowTo
  name: How to Export Redacted Documents with GroupDocs.Redaction .NET
  description: Learn how to export redacted files, configure output folders, create
    rasterized PDFs, and save to streams using GroupDocs.Redaction for .NET.
  steps:
  - name: Install the NuGet Package
    text: 'Add the latest GroupDocs.Redaction package to your project:'
  - name: Load the Document and Define Redactions
    text: Create a `Redactor` instance, load the file, and specify the regions you
      want to hide. The `Redactor` class provides the core functionality for loading
      documents and applying redaction rules.
  - name: Choose the Export Method
    text: '#### Export in Original Format'
- type: FAQPage
  questions:
  - question: Can I export to a format that wasn’t originally supported?
    answer: Yes, GroupDocs.Redaction can convert most input types to PDF, DOCX, XLSX,
      PPTX, or rasterized PDF, covering over 30 formats.
  - question: How does rasterization protect redacted data?
    answer: By rendering each page as a flat image, any hidden text layers are removed,
      making it impossible to extract the original content.
  - question: Is it possible to chain multiple redaction rules?
    answer: Absolutely – you can call `Apply` repeatedly or pass a collection of `RedactionOptions`
      to process many patterns in one pass. `RedactionOptions` defines the settings
      for a single redaction operation, such as region and replacement type.
  - question: Do I need to close the Redactor object?
    answer: The `Redactor` implements `IDisposable`; wrap it in a `using` block or
      call `Dispose()` to release file handles promptly. `IDisposable` is an interface
      that provides a mechanism for releasing unmanaged resources.
  - question: What .NET runtimes are officially tested?
    answer: GroupDocs.Redaction is validated on .NET Framework 4.6+, .NET Core 3.1+,
      and .NET 5/6/7.
---
# How to Export Redacted Documents with GroupDocs.Redaction .NET

In this comprehensive guide you’ll discover **how to export redacted** content safely and efficiently using GroupDocs.Redaction for .NET. Whether you need to keep the original file type, lock down the document as a rasterized PDF, or stream the result directly in memory, we walk you through every option with clear, conversational explanations and real‑world tips. By the end of this tutorial you’ll be able to choose the right export strategy for any compliance‑driven scenario.

## Quick Answers
- **What formats can I export to?** Any of the 30+ native formats supported by GroupDocs.Redaction, plus rasterized PDF for maximum security.  
- **Do I need a license for streaming?** Yes, a valid GroupDocs.Redaction license is required for production streaming.  
- **Can I set a custom output folder?** Absolutely – use the `OutputPath` property or `SaveOptions` to configure it.  
- **Is rasterization safe for large files?** It handles documents up to 500 pages without loading the whole file into memory.  
- **Which .NET versions are supported?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.

## What is GroupDocs.Redaction?
GroupDocs.Redaction is a .NET library that programmatically removes or masks sensitive information from PDFs, Word, Excel, PowerPoint, images, and many other formats. It offers a high‑level API for defining redaction regions, applying policies, and finally exporting the cleaned document. This makes it easy to integrate redaction capabilities into any .NET application.

## Why Export Redacted Documents as Rasterized PDFs?
Rasterized PDFs convert every page into a flat image, eliminating hidden text layers that could be extracted later. This format guarantees that redacted content cannot be recovered, meeting strict regulatory standards such as GDPR and HIPAA. GroupDocs.Redaction can produce rasterized PDFs up to 300 dpi, preserving visual fidelity while ensuring security.

## How to Export Redacted Documents?
Load the source file, apply your redaction rules, then call the appropriate save method—either `Save` for original format, `SaveAsRasterizedPdf` for image‑only PDFs, or `SaveToStream` for in‑memory handling. Below is the step‑by‑step workflow. Each method ensures that the redacted content is permanently removed while preserving the desired output format.

### Step 1: Install the NuGet Package
Add the latest GroupDocs.Redaction package to your project:

```bash
dotnet add package GroupDocs.Redaction
```

### Step 2: Load the Document and Define Redactions
Create a `Redactor` instance, load the file, and specify the regions you want to hide. The `Redactor` class provides the core functionality for loading documents and applying redaction rules.

```csharp
using GroupDocs.Redaction;
using GroupDocs.Redaction.Options;

// Load the document
var redactor = Redactor.Create("SensitiveReport.docx");

// Define a redaction for a specific text pattern
redactor.Apply(new RedactionOptions
{
    SearchPattern = "SSN: \\d{3}-\\d{2}-\\d{4}",
    RedactionColor = System.Drawing.Color.Black,
    RedactionType = RedactionType.Image
});
```

### Step 3: Choose the Export Method
#### Export in Original Format
```csharp
redactor.Save("RedactedReport.docx");
```

#### Export as Rasterized PDF
```csharp
var rasterOptions = new RasterizationOptions { Dpi = 300 };
redactor.SaveAsRasterizedPdf("RedactedReport.pdf", rasterOptions);
```

#### Export to a Memory Stream (ideal for web APIs)
```csharp
using var stream = new MemoryStream();
redactor.Save(stream, SaveOptions.CreatePdf());
stream.Position = 0; // Reset for reading
```

The `Save` method writes the redacted document to a file in its original format. `SaveAsRasterizedPdf` creates a PDF where each page is rendered as an image, removing any hidden text. `SaveToStream` returns the redacted file as a memory stream, suitable for web responses.

## How to Configure an Output Folder?
Set the `OutputPath` property on the `Redactor` or pass a custom `SaveOptions` object that includes the desired directory. `OutputPath` is a property of the `Redactor` that specifies the directory where output files are written. `SaveOptions` allows you to customize various saving parameters, including the output folder. This ensures all exported files land in a predictable location, simplifying batch processing pipelines. You can also specify subfolders per document type to keep your workspace organized.

```csharp
var options = SaveOptions.CreatePdf();
options.OutputPath = @"C:\RedactedOutputs\";
redactor.Save(options);
```

## Common Issues and Solutions
- **Redaction not applied:** Verify that the search pattern matches the document text exactly; use `RegexOptions.IgnoreCase` if needed. `RegexOptions` is an enumeration that controls regular expression matching behavior, such as case sensitivity.  
- **Large files cause memory pressure:** Enable streaming mode by using `SaveToStream` and avoid calling `Save` on the whole document.  
- **Rasterized PDF looks blurry:** Increase the DPI in `RasterizationOptions` (e.g., 300–600) to improve image quality. `RasterizationOptions` lets you set parameters like DPI and image format for rasterized PDF output.

## Frequently Asked Questions

**Q: Can I export to a format that wasn’t originally supported?**  
A: Yes, GroupDocs.Redaction can convert most input types to PDF, DOCX, XLSX, PPTX, or rasterized PDF, covering over 30 formats.

**Q: How does rasterization protect redacted data?**  
A: By rendering each page as a flat image, any hidden text layers are removed, making it impossible to extract the original content.

**Q: Is it possible to chain multiple redaction rules?**  
A: Absolutely – you can call `Apply` repeatedly or pass a collection of `RedactionOptions` to process many patterns in one pass. `RedactionOptions` defines the settings for a single redaction operation, such as region and replacement type.

**Q: Do I need to close the Redactor object?**  
A: The `Redactor` implements `IDisposable`; wrap it in a `using` block or call `Dispose()` to release file handles promptly. `IDisposable` is an interface that provides a mechanism for releasing unmanaged resources.

**Q: What .NET runtimes are officially tested?**  
A: GroupDocs.Redaction is validated on .NET Framework 4.6+, .NET Core 3.1+, and .NET 5/6/7.

## Additional Resources

### Available Tutorials

- [How to Save Documents as Rasterized PDFs Using GroupDocs.Redaction for .NET&#58; A Complete Guide](./groupdocs-redaction-net-rasterized-pdfs/)
- [Implementing Output Directory in .NET with GroupDocs.Redaction&#58; A Comprehensive Guide](./implement-output-directory-groupdocs-redaction-dotnet/)
- [Redact and Save Documents with GroupDocs.Redaction for .NET&#58; A Complete Guide](./redact-save-documents-groupdocs-redaction-net/)
- [Save Redacted Documents in Original Format Using GroupDocs.Redaction .NET](./save-redacted-docs-original-format-groupdocs-redaction-net/)
- [Secure Document Redaction in .NET Using Streams&#58; A Guide for GroupDocs.Redaction](./secure-document-redaction-net-streams-groupdocs-redaction/)

### Helpful Links

- [GroupDocs.Redaction for Net Documentation](https://docs.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction for Net API Reference](https://reference.groupdocs.com/redaction/net/)
- [Download GroupDocs.Redaction for Net](https://releases.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction Forum](https://forum.groupdocs.com/c/redaction/33)
- [Free Support](https://forum.groupdocs.com/)
- [Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Last Updated:** 2026-06-11  
**Tested With:** GroupDocs.Redaction 23.11 for .NET  
**Author:** GroupDocs  

---

## Related Tutorials

- [Save Redacted Documents in Original Format Using GroupDocs.Redaction .NET](/redaction/net/document-saving/save-redacted-docs-original-format-groupdocs-redaction-net/)
- [How to Save Documents as Rasterized PDFs Using GroupDocs.Redaction for .NET: A Complete Guide](/redaction/net/document-saving/groupdocs-redaction-net-rasterized-pdfs/)
- [Secure Document Redaction in .NET Using Streams: A Guide for GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)
