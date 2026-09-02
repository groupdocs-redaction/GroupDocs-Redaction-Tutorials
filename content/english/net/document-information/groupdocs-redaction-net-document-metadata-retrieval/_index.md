---
title: "How to Retrieve Metadata with GroupDocs.Redaction .NET API"
description: "Learn how to retrieve metadata and extract document metadata using GroupDocs.Redaction .NET, enabling robust document management and compliance."
date: "2026-06-06"
weight: 1
url: "/net/document-information/groupdocs-redaction-net-document-metadata-retrieval/"
keywords:
- how to retrieve metadata
- extract document metadata
- get document properties
- read file metadata
- get document size
type: docs
schemas:
- type: TechArticle
  headline: How to Retrieve Metadata with GroupDocs.Redaction .NET API
  description: Learn how to retrieve metadata and extract document metadata using
    GroupDocs.Redaction .NET, enabling robust document management and compliance.
  dateModified: '2026-06-06'
  author: GroupDocs
- type: HowTo
  name: How to Retrieve Metadata with GroupDocs.Redaction .NET API
  description: Learn how to retrieve metadata and extract document metadata using
    GroupDocs.Redaction .NET, enabling robust document management and compliance.
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
- type: FAQPage
  questions:
  - question: Which document formats can I extract metadata from?
    answer: GroupDocs.Redaction reads metadata from more than 50 formats, including
      PDF, DOCX, XLSX, PPTX, HTML, and common image types.
  - question: How do I handle password‑protected files?
    answer: Pass the password to the `Redactor` constructor; the API will decrypt
      the file before extracting metadata.
  - question: Is there a limit to the size of files I can process?
    answer: While there is no hard limit, files larger than 2 GB may require additional
      memory tuning; performance remains linear with file size.
  - question: Can I retrieve metadata in a batch operation?
    answer: Yes—iterate over a collection of file paths and call `GetDocumentInfo()`
      for each; the library is thread‑safe for parallel execution.
  - question: Do I need a license for development builds?
    answer: A free trial license is sufficient for development and testing; a commercial
      license is required for production deployments.
---

# How to Retrieve Metadata with GroupDocs.Redaction .NET

In today's digital age, **how to retrieve metadata** from a file is a fundamental step for any document‑centric application. Whether you need to read file metadata for compliance audits, extract document properties for indexing, or simply display the document size in a UI, GroupDocs.Redaction .NET gives you a concise API to do it in just a few lines of C#. This tutorial walks you through the entire process, from environment setup to displaying the retrieved information, so you can start extracting document metadata right away.

## Quick Answers
- **What is the primary method to get metadata?** Call `Redactor.GetDocumentInfo()` on a `Redactor` instance.  
- **Which formats are supported?** Over 50 input and output formats, including PDF, DOCX, XLSX, PPTX, and image types.  
- **Do I need a license for development?** A free trial license works for testing; a full license is required for production.  
- **Can I process large files?** Yes—GroupDocs.Redaction handles multi‑hundred‑page documents without loading the entire file into memory.  
- **Is async support available?** The API can be wrapped in async patterns to keep UI threads responsive.

## What is metadata retrieval in GroupDocs.Redaction?
Metadata retrieval is the process of accessing a document’s built‑in properties—such as file type, page count, and size—through the library’s API. By extracting these properties, developers can programmatically assess document characteristics, support indexing, enforce compliance rules, and make informed decisions about further processing steps.

## How to Retrieve Document Metadata?
The `Redactor` class is the primary interface for loading and inspecting documents in GroupDocs.Redaction.  
`GetDocumentInfo()` is a method that returns a `DocumentInfo` object containing the document’s metadata.  

Load your file with `new Redactor("path/to/file")` and invoke `GetDocumentInfo()`—the call returns a `DocumentInfo` object containing type, page count, size, and other properties. This two‑step approach works for any supported format and requires no additional configuration. You can then read fields like `FileType`, `PageCount`, and `FileSize` to display or log the information.

## Prerequisites

- **GroupDocs.Redaction .NET** version 21.6 or newer.  
- .NET Framework 4.7.2 +, .NET Core 3.1 +, or .NET 5/6+.  
- Basic C# knowledge and a development IDE (Visual Studio, Rider, etc.).

## Setting Up GroupDocs.Redaction for .NET

Getting started with GroupDocs.Redaction is straightforward. Install the package using one of the following methods:

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

Or, use the **NuGet Package Manager UI**: Simply search for “GroupDocs.Redaction” and click **Install**.

### License Acquisition

To try out GroupDocs.Redaction, you can obtain a free trial license. For ongoing development or production use, purchase a full license or request a temporary license from the official site.

Once installed, initialize the library as follows:

```csharp
using GroupDocs.Redaction;
```

## Implementation Guide

### Get Document Information Feature

This feature focuses on extracting vital metadata from documents using GroupDocs.Redaction .NET. Follow these steps:

#### Step 1: Prepare Your Document Path

Define the absolute or relative path to the target file:

```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY\\SampleDocx.docx";
```

Replace `YOUR_DOCUMENT_DIRECTORY` with the folder that contains your document.

#### Step 2: Initialize Redactor Instance

Create a `Redactor` object that provides access to metadata methods:

```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // Further operations will be performed here
}
```

#### Step 3: Retrieve Document Information

Call `GetDocumentInfo()` on the `Redactor` instance to pull all available properties:

```csharp
IDocumentInfo info = redactor.GetDocumentInfo();
```

The returned object includes file type, number of pages, and file size.

#### Step 4: Display Document Details

Output the information to the console or UI. The sample code (commented for standalone runs) demonstrates how to print each property:

```csharp
Console.WriteLine($"File type: {info.FileType}\\
Number of pages: {info.PageCount}\\
Document size: {info.SizeInBytes} bytes");
```

### Why Use GroupDocs.Redaction for Metadata Extraction?
GroupDocs.Redaction supports **50+ file formats** and can process documents up to **2 GB** in size while keeping memory consumption under **100 MB** for typical workloads. The library extracts metadata without fully loading the document, delivering fast responses—often under **200 ms** for a 100‑page PDF on standard server hardware.

### Common Issues and Solutions

- **Incorrect file path** – Verify the path string and ensure the file is accessible to the running process.  
- **Unsupported format** – Check the format list; if a format is missing, consider converting it first.  
- **Performance bottlenecks** – For very large files, enable streaming options or process pages in batches to limit memory usage.

## Practical Applications

Understanding a document's metadata enables several real‑world scenarios:

1. **Document Management Systems (DMS)** – Automate categorization and indexing based on type, size, or page count.  
2. **Compliance Auditing** – Verify that confidential files contain required metadata before archiving.  
3. **Data Migration** – Group files by properties to streamline bulk migration tasks.  

## Performance Considerations

- **Efficient Resource Usage** – Use the `Redactor` instance within a `using` block to guarantee proper disposal.  
- **Asynchronous Patterns** – Wrap metadata calls in `Task.Run` or implement async wrappers to keep UI threads responsive in desktop or web apps.

## Frequently Asked Questions

**Q: Which document formats can I extract metadata from?**  
A: GroupDocs.Redaction reads metadata from more than 50 formats, including PDF, DOCX, XLSX, PPTX, HTML, and common image types.

**Q: How do I handle password‑protected files?**  
A: Pass the password to the `Redactor` constructor; the API will decrypt the file before extracting metadata.

**Q: Is there a limit to the size of files I can process?**  
A: While there is no hard limit, files larger than 2 GB may require additional memory tuning; performance remains linear with file size.

**Q: Can I retrieve metadata in a batch operation?**  
A: Yes—iterate over a collection of file paths and call `GetDocumentInfo()` for each; the library is thread‑safe for parallel execution.

**Q: Do I need a license for development builds?**  
A: A free trial license is sufficient for development and testing; a commercial license is required for production deployments.

## Resources

- [Documentation](https://docs.groupdocs.com/redaction/net/)  
- [API Reference](https://reference.groupdocs.com/redaction/net)  
- [Download](https://releases.groupdocs.com/redaction/net/)  
- [Free Support Forum](https://forum.groupdocs.com/c/redaction/33)  
- [Temporary License Information](https://purchase.groupdocs.com/temporary-license/)

## Conclusion

You now have a complete, step‑by‑step guide on **how to retrieve metadata** using GroupDocs.Redaction .NET. By leveraging the `Redactor.GetDocumentInfo()` method, you can quickly read file metadata, support compliance workflows, and enhance any document‑processing pipeline. Explore additional Redaction features—such as content redaction, watermarking, and document conversion—to build a fully featured document management solution.

---

**Last Updated:** 2026-06-06  
**Tested With:** GroupDocs.Redaction .NET 21.6 (latest at time of writing)  
**Author:** GroupDocs  

---

## Related Tutorials

- [How to Extract Document Metadata from Streams Using GroupDocs.Redaction .NET](/redaction/net/document-information/extract-document-info-streams-groupdocs-redaction-dotnet/)
- [How to Redact Document Metadata Using GroupDocs.Redaction for .NET - A Comprehensive Guide](/redaction/net/metadata-redaction/redact-metadata-groupdocs-redaction-net/)
- [Document Loading Tutorials with GroupDocs.Redaction for .NET](/redaction/net/document-loading/)
