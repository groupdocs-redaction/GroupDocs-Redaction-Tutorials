---
date: '2026-07-20'
description: Learn how to list formats using GroupDocs.Redaction .NET, integrate the
  feature into your document workflow, and improve performance.
images:
- /net/format-handling/groupdocs-redaction-net-supported-formats-listing/og-image.png
keywords:
- how to list formats
- GroupDocs.Redaction supported formats
- .NET document processing
lastmod: '2026-07-20'
og_description: Discover how to list formats using GroupDocs.Redaction .NET, see a
  step‑by‑step guide, and get tips for optimal performance in your .NET applications.
og_image_alt: Guide showing how to list supported file formats with GroupDocs.Redaction
  in a .NET project
og_title: How to List Formats with GroupDocs.Redaction .NET
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
title: How to List Formats with GroupDocs.Redaction .NET
type: docs
url: /net/format-handling/groupdocs-redaction-net-supported-formats-listing/
weight: 1
---

# How to List Formats with GroupDocs.Redaction .NET

Managing a wide variety of document types is a daily reality for developers building document‑centric applications. In this tutorial you’ll learn **how to list formats** that GroupDocs.Redaction .NET can handle, so you can validate files before processing, present users with accurate options, and keep your workflow efficient.

## Introduction

Efficient document handling starts with knowing exactly which file types your library supports. GroupDocs.Redaction provides a built‑in method to retrieve this information, letting you build dynamic UI elements, enforce validation rules, and avoid runtime errors. Below you’ll find everything you need to get up and running, from installation to practical code snippets and performance tips.

### Quick Answers
- **What does “how to list formats” mean?** It refers to retrieving the collection of file extensions that GroupDocs.Redaction can process.  
- **Do I need a license?** Yes, a valid GroupDocs.Redaction license is required for production use.  
- **Which .NET versions are supported?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.  
- **How many formats are available?** Over 30 input and output formats are supported out‑of‑the‑box.  
- **Is any special configuration needed?** No extra configuration is required beyond standard library initialization.

## What is “how to list formats”?

It involves calling the library’s FileType API to obtain a collection where each entry contains the file extension and a human‑readable name. Developers can then iterate this collection to build validation rules, populate UI dropdowns, or log supported types, ensuring only compatible documents are processed.

## Why list formats with GroupDocs.Redaction?

GroupDocs.Redaction supports **30+** distinct file types—including PDF, DOCX, PPTX, and image formats—allowing you to handle most enterprise documents without third‑party converters. By programmatically listing these formats you eliminate guesswork, reduce support tickets, and ensure that only compatible files enter your processing pipeline.

## Prerequisites

- **GroupDocs.Redaction for .NET** – download the latest package from the official site.  
- **.NET Framework or .NET Core** – compatible with your development environment.  
- **Visual Studio** (or any C#‑compatible IDE).  
- Basic familiarity with C# syntax.

## Setting Up GroupDocs.Redaction for .NET

### .NET CLI
`dotnet add package GroupDocs.Redaction`

### Package Manager
`Install-Package GroupDocs.Redaction`

### NuGet Package Manager UI
- Search for **“GroupDocs.Redaction”** and install the latest version.

### License Acquisition
GroupDocs offers a free trial, a temporary license for evaluation, or full‑purchase options. Visit the GroupDocs website to obtain the appropriate license file.

### Basic Initialization and Setup
After adding the package, reference the namespace and create a `Redactor` instance:

```csharp
using GroupDocs.Redaction;

// Initialize with a license file (replace path as needed)
Redactor redactor = new Redactor("path/to/license/file.lic");
```

## Implementation Guide

### How do I list formats with GroupDocs.Redaction .NET?
Load the library, call the static helper, and sort the results—this gives you a ready‑to‑use collection in just two lines of code. Use `FileType.GetSupportedFileFormats()` to retrieve a `IEnumerable<FileType>` that includes each format’s extension and display name, then order by extension for a clean UI list.

### Retrieving Supported File Formats

#### Overview
The goal is to obtain a list of file types that GroupDocs.Redaction can handle, facilitating integration into validation logic, UI dropdowns, or logging mechanisms.

#### Step‑by‑Step Implementation

**1. Retrieve Supported File Types**  
`FileType.GetSupportedFileFormats()` returns every format the library recognizes. The method is part of the `GroupDocs.Redaction.FileType` class, which encapsulates metadata such as file extension and friendly name.

**2. Display Supported File Types**  
Iterate over the collection and output each format’s extension and description. Inline code example:

```csharp
var formats = FileType.GetSupportedFileFormats()
                      .OrderBy(f => f.Extension);

foreach (var format in formats)
{
    Console.WriteLine($"{format.Extension} – {format.Name}");
}
```

The snippet prints a neatly ordered list like “.pdf – Portable Document Format”, making it perfect for populating UI elements.

### Troubleshooting Tips
- **Missing Package** – Verify the NuGet package reference and restore packages if needed.  
- **Incorrect License Path** – Ensure the license file is copied to the output directory or provide an absolute path.  
- **Unsupported Extension** – If a format isn’t listed, confirm you’re using the latest library version; newer releases add additional formats.

## Practical Applications
Understanding supported file formats unlocks several real‑world scenarios:

1. **Document Management Systems** – Validate uploads against the supported list to prevent processing failures.  
2. **Content Security** – Apply redaction rules only to file types that the engine can safely modify.  
3. **Batch Processing Pipelines** – Filter large file batches before invoking redaction, saving CPU and memory.

## Performance Considerations
- **Memory Footprint** – Listing formats is a lightweight operation; it does not load any document into memory.  
- **Batch Operations** – When processing hundreds of files, retrieve the format list once and reuse it to avoid redundant calls.  
- **Thread Safety** – `FileType.GetSupportedFileFormats()` is thread‑safe and can be called from parallel tasks without synchronization.

## Conclusion
You now have a complete, production‑ready approach for **how to list formats** using GroupDocs.Redaction .NET. By integrating this feature, you can enhance validation, improve user experience, and keep your document pipelines robust.

### Next Steps
- Explore the `Redactor` API to apply redaction rules based on file type.  
- Combine the format list with a front‑end dropdown for seamless file selection.  
- Review the performance guide to optimise large‑scale batch jobs.

## Frequently Asked Questions

**Q: Can I retrieve the format list without initializing a Redactor instance?**  
A: Yes, `FileType.GetSupportedFileFormats()` is static and does not require a `Redactor` object.

**Q: Does the list include both input and output formats?**  
A: The method returns all formats that the library can both read and write; each `FileType` includes a `CanRead` and `CanWrite` flag.

**Q: How often is the supported format list updated?**  
A: GroupDocs releases format updates with each library version; checking the list at runtime ensures you always have the latest set.

**Q: Is there a way to filter only PDF‑compatible formats?**  
A: Yes, filter the collection where `format.Extension == ".pdf"` or where `format.Name.Contains("PDF")`.

**Q: Will this approach work on .NET Core 2.1?**  
A: The method requires .NET Core 3.1 or later; earlier runtimes are not supported.

## FAQ Section
1. **How do I install GroupDocs.Redaction for .NET?**  
   Use the CLI command `dotnet add package GroupDocs.Redaction` or install via the NuGet Package Manager UI.  
2. **What are some common issues when retrieving supported formats?**  
   Ensure all dependencies are restored and that you are referencing the correct namespace (`GroupDocs.Redaction`).  
3. **Can I use this feature with non‑.NET applications?**  
   This tutorial focuses on .NET, but GroupDocs provides similar APIs for Java, Python, and other platforms.  
4. **How can I optimise performance when using GroupDocs.Redaction?**  
   Reuse the format list, avoid loading full documents when only checking compatibility, and monitor memory usage during batch jobs.  
5. **What file types does GroupDocs.Redaction support?**  
   The library supports 30+ formats, including PDF, DOCX, PPTX, XLSX, BMP, PNG, JPEG, and many more. Use `FileType.GetSupportedFileFormats()` to view the full list.

## Resources
- [Documentation](https://docs.groupdocs.com/redaction/net/)
- [API Reference](https://reference.groupdocs.com/redaction/net)
- [Download GroupDocs.Redaction](https://releases.groupdocs.com/redaction/net/)
- [Free Support Forum](https://forum.groupdocs.com/c/redaction/33)
- [Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Last Updated:** 2026-07-20  
**Tested With:** GroupDocs.Redaction 4.2.0 for .NET  
**Author:** GroupDocs  

---

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

## Related Tutorials

- [Format Handling Tutorials for GroupDocs.Redaction .NET](/redaction/net/format-handling/)
- [Document Loading Tutorials with GroupDocs.Redaction for .NET](/redaction/net/document-loading/)
- [Document Saving Tutorials for GroupDocs.Redaction .NET](/redaction/net/document-saving/)