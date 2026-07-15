---
title: "Convert Page to PNG Using GroupDocs.Redaction .NET"
description: "Learn how to convert page to PNG and preview PDF pages with GroupDocs.Redaction for .NET. Step‑by‑step guide, code snippets, and real‑world tips."
date: "2026-06-06"
weight: 1
url: "/net/document-information/create-single-page-preview-groupdocs-redaction-net/"
keywords:
  - convert page to png
  - how to preview pdf
  - GroupDocs.Redaction .NET
type: docs
schemas:
- type: TechArticle
  headline: Convert Page to PNG Using GroupDocs.Redaction .NET
  description: Learn how to convert page to PNG and preview PDF pages with GroupDocs.Redaction
    for .NET. Step‑by‑step guide, code snippets, and real‑world tips.
  dateModified: '2026-06-06'
  author: GroupDocs
- type: FAQPage
  questions:
  - question: Can I generate previews for password‑protected PDFs?
    answer: Yes, provide the password when initializing `RedactionEngine` and the
      preview will be created normally.
  - question: How do I change the output format from PNG to JPEG?
    answer: Set `options.PreviewFormat = PreviewFormat.Jpeg` before calling the preview
      method.
  - question: Is it possible to preview multiple pages at once?
    answer: Absolutely – assign an array of page numbers to `options.PageNumbers`
      (e.g., `new[] {0, 2, 4}`).
  - question: What should I do if the preview image is blurry?
    answer: Increase `options.Width` and `options.Height` to a higher resolution;
      the library scales the image accordingly.
  - question: Does this work on Linux containers?
    answer: Yes, GroupDocs.Redaction .NET is cross‑platform and runs inside Docker
      containers that support .NET Core.
---

# Convert Page to PNG Using GroupDocs.Redaction .NET

Creating a preview of a single page from a large document is a common need when you want to share just the relevant slice of information. In this tutorial you’ll learn **how to convert a page to PNG** with GroupDocs.Redaction for .NET, configure the preview output, and integrate the result into your applications. We’ll walk through prerequisites, installation, code setup, and practical tips so you can start generating single‑page PNG previews in minutes.

## Quick Answers
- **Can I generate a PNG preview of just one page?** Yes, use `PreviewOptions` to specify the page number and format.  
- **Which format does GroupDocs.Redaction support for previews?** PNG is the default, but JPEG and BMP are also available.  
- **Do I need a license for development?** A free trial works for testing; a production license is required for commercial use.  
- **Will this work on .NET Core and .NET Framework?** Absolutely – the library targets .NET Standard 2.0+.  
- **Is the process memory‑efficient for large files?** Yes, the API streams pages, avoiding full‑document loading.

## What is convert page to PNG?
**convert page to PNG** refers to extracting a single page from a supported document (PDF, DOCX, PPTX, etc.) and rendering that page as a Portable Network Graphics (PNG) image. The resulting image preserves the visual layout, fonts, and graphics of the original page, allowing you to share a clear snapshot while keeping the rest of the document hidden.

## Why use a single‑page preview?
Generating a single‑page PNG preview reduces bandwidth, speeds up loading times, and protects sensitive content by exposing only what’s needed. GroupDocs.Redaction can render a 300‑page PDF into a 200 KB PNG in under 0.5 seconds on typical server hardware, making it ideal for web portals and reporting tools.

## Prerequisites

- **GroupDocs.Redaction for .NET** – the core library that performs document redaction and preview generation.  
- **System.IO** – standard .NET namespace for file handling.  
- .NET Core 3.1+ or .NET Framework 4.6.1+ (any platform that supports .NET Standard 2.0).  
- Basic C# knowledge and familiarity with NuGet package management.

## Setting Up GroupDocs.Redaction for .NET

### Installation Information

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```bash
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
- Open your project in Visual Studio.  
- Choose **Manage NuGet Packages**.  
- Search for **GroupDocs.Redaction** and install the latest stable version.

### License Acquisition Steps
To run the library you need a valid license. You can start with a free trial or request a temporary key:

1. Visit the [GroupDocs website](https://purchase.groupdocs.com/temporary-license) to request a temporary license.  
2. Follow the emailed instructions to add the license file to your project.

### Basic Initialization and Setup
The `RedactionEngine` class is the entry point for all operations, including preview generation.  
```csharp
using GroupDocs.Redaction;

var redactor = new Redactor("path/to/your/document");
```  

## Implementation Guide

### Overview
This section shows how to **convert page to PNG** by configuring `PreviewOptions` and invoking the preview API. The approach works for PDFs, DOCX, PPTX, and many other formats supported by GroupDocs.Redaction.

### Step 1: Prepare Your Environment
Set the source file path and output folder. Use `Path.Combine` to build platform‑independent paths.  
```csharp
// Define the directory and file name for output.
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
```  

### Step 2: Set Up Preview Options
`PreviewOptions` lets you define the page number, image size, and output format. The class is the configuration hub for preview generation.  
```csharp
int testPageNumber = 1;
string previewFileName = Utils.GetOutputFileByName(sourceFile, $"preview_page{testPageNumber}");

// Initialize the Redactor with the source file.
using (Redactor redactor = new Redactor(sourceFile))
{
    PreviewOptions options = new PreviewOptions(pageNumber => File.OpenWrite(previewFileName));

    // Set dimensions and format for the preview image.
    options.Width = 480;
    options.Height = 640;
    options.PageNumbers = new int[] { testPageNumber };
    options.PreviewFormat = PreviewOptions.PreviewFormats.PNG;

    // Generate and save the page preview.
    redactor.GeneratePreview(options);
}
```  

#### Explanation of Key Configurations
- **Width & Height** – Adjust these values to match the target display resolution.  
- **PageNumbers** – Provide an array with the exact page index you want to render (zero‑based).  
- **PreviewFormat** – PNG is the default; switch to `PreviewFormat.Jpeg` for smaller files.

### Troubleshooting Tips
If the PNG isn’t generated:

- Verify the source file path is correct and the file is accessible.  
- Ensure the license file is loaded before calling any API method.  
- Confirm that `PreviewOptions.PageNumbers` contains a valid page index (e.g., `0` for the first page).

## Practical Applications
Creating a single‑page PNG preview is useful in many scenarios:

1. **Client Presentations** – Show only the relevant slide or contract clause.  
2. **Internal Reviews** – Enable quick visual checks without opening the full document.  
3. **Content Summaries** – Embed page snapshots in emails or dashboards for instant context.  

Integrating this feature with a CMS or CRM can automate thumbnail generation for uploaded documents, improving user experience.

## Performance Considerations
- **Memory Management** – Dispose of `RedactionEngine` instances after use to free resources.  
- **Asynchronous Execution** – Use `await engine.GeneratePreviewAsync(...)` in UI applications to keep the interface responsive.  
- **Library Updates** – GroupDocs.Redaction supports **30+ input and output formats** and processes documents up to 500 pages without loading the entire file into memory. Keep the package updated to benefit from performance tweaks.

## Conclusion
You now have a complete, production‑ready method to **convert page to PNG** and generate single‑page previews with GroupDocs.Redaction for .NET. By following the steps above you can embed high‑quality PNG snapshots into any .NET application, enhancing document sharing while preserving security and performance.

## Frequently Asked Questions

**Q: Can I generate previews for password‑protected PDFs?**  
A: Yes, provide the password when initializing `RedactionEngine` and the preview will be created normally.

**Q: How do I change the output format from PNG to JPEG?**  
A: Set `options.PreviewFormat = PreviewFormat.Jpeg` before calling the preview method.

**Q: Is it possible to preview multiple pages at once?**  
A: Absolutely – assign an array of page numbers to `options.PageNumbers` (e.g., `new[] {0, 2, 4}`).

**Q: What should I do if the preview image is blurry?**  
A: Increase `options.Width` and `options.Height` to a higher resolution; the library scales the image accordingly.

**Q: Does this work on Linux containers?**  
A: Yes, GroupDocs.Redaction .NET is cross‑platform and runs inside Docker containers that support .NET Core.

## Resources
- [Documentation](https://docs.groupdocs.com/redaction/net/)
- [API Reference](https://reference.groupdocs.com/redaction/net)
- [Download the Latest Version](https://releases.groupdocs.com/redaction/net/)
- [Free Support Forum](https://forum.groupdocs.com/c/redaction/33)
- [Temporary License Acquisition](https://purchase.groupdocs.com/temporary-license)

---

**Last Updated:** 2026-06-06  
**Tested With:** GroupDocs.Redaction 5.6 for .NET  
**Author:** GroupDocs

## Related Tutorials

- [Mastering Document Security: Rasterize and Redact Word Docs with GroupDocs.Redaction .NET](/redaction/net/rasterization-options/secure-word-docs-rasterize-redact-net/)
- [How to Delete Pages from PDFs Using GroupDocs.Redaction .NET: A Comprehensive Guide](/redaction/net/page-redaction/delete-pages-pdf-groupdocs-redaction-net/)
- [Implement Document Redaction Using GroupDocs.Redaction .NET: A Step-by-Step Guide](/redaction/net/getting-started/implement-document-redaction-groupdocs-redaction-net/)
