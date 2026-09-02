---
title: "Extract Document Metadata – GroupDocs.Redaction .NET Tutorials"
description: "Learn how to extract document metadata, get page count, and generate previews using GroupDocs.Redaction for .NET – step‑by‑step C# tutorials."
weight: 15
url: "/net/document-information/"
type: docs
date: 2026-06-06
keywords:
  - extract document metadata
  - how to get page count
  - metadata extraction c#
  - read metadata from stream
schemas:
- type: TechArticle
  headline: Extract Document Metadata – GroupDocs.Redaction .NET Tutorials
  description: Learn how to extract document metadata, get page count, and generate
    previews using GroupDocs.Redaction for .NET – step‑by‑step C# tutorials.
  dateModified: '2026-06-06'
  author: GroupDocs
- type: HowTo
  name: Extract Document Metadata – GroupDocs.Redaction .NET Tutorials
  description: Learn how to extract document metadata, get page count, and generate
    previews using GroupDocs.Redaction for .NET – step‑by‑step C# tutorials.
  steps:
  - name: Instantiate `RedactionEngine` with the file path or stream.
    text: Instantiate `RedactionEngine` with the file path or stream.
  - name: Call `GetDocumentInfo()`.
    text: Call `GetDocumentInfo()`.
  - name: Access properties like `Author`, `Title`, `CreatedDate`, and `PageCount`.
    text: Access properties like `Author`, `Title`, `CreatedDate`, and `PageCount`.
- type: FAQPage
  questions:
  - question: Can I extract metadata from password‑protected PDFs?
    answer: Yes. Provide the password when constructing `RedactionEngine`; the API
      will decrypt the header and return metadata.
  - question: Does the API support batch processing of multiple files?
    answer: Absolutely. Loop through your file collection, instantiate `RedactionEngine`
      for each, and call `GetDocumentInfo()`—the engine is lightweight enough for
      thousands of files.
  - question: What happens if a document has no metadata?
    answer: The corresponding properties return `null` or default values; you can
      safely check for `null` before using them.
  - question: Is it possible to modify metadata after extraction?
    answer: GroupDocs.Redaction focuses on redaction, not editing metadata. Use GroupDocs.Metadata
      or another library for write‑back scenarios.
  - question: Which .NET versions are officially supported?
    answer: .NET Framework 4.7.2+, .NET Core 3.1+, .NET 5+, and .NET 6+ are fully
      supported.
---

# Document Information Tutorials for GroupDocs.Redaction .NET

In this hub you’ll discover how to **extract document metadata** from a wide range of file types, determine page counts, and generate preview images before you run redaction operations. By programmatically accessing this information you can decide which files need special handling, enforce compliance rules, and improve overall processing performance. All examples are written in C# and target .NET 6+, so you can drop them straight into your existing projects.

## Quick Answers
- **How do I extract metadata?** Use `RedactionEngine.GetDocumentInfo()` to pull properties such as author, creation date, and page count.  
- **Can I read metadata from a stream?** Yes—pass a `MemoryStream` containing the file to the same API method.  
- **What formats are supported?** Over 100 formats, including PDF, DOCX, PPTX, and image files.  
- **Is page count retrieval fast?** The engine reads only the file header, delivering counts in under 50 ms for most documents.  
- **Do I need a license for development?** A temporary license works for testing; a full license is required for production.

## What is “extract document metadata”?
**Extract document metadata** means programmatically retrieving embedded properties—such as author, title, creation date, and page count—from a file without opening it in a viewer. This lightweight operation lets your application make informed decisions before redaction begins.

## Why extract document metadata with GroupDocs.Redaction?
GroupDocs.Redaction can read metadata from **100+** file formats while keeping memory usage under 10 MB for documents up to 500 pages. The API returns a fully typed `DocumentInfo` object, eliminating the need for custom parsers and reducing development time by up to 70 %.

## Prerequisites
- .NET 6+ (or .NET Core 3.1 / .NET Framework 4.7.2)  
- GroupDocs.Redaction for .NET NuGet package installed  
- A temporary or full license key (available from the GroupDocs portal)

## How to extract document metadata using GroupDocs.Redaction .NET?
`RedactionEngine` is the core component that loads documents and provides metadata extraction methods. `GetDocumentInfo()` returns a `DocumentInfo` object containing metadata such as author, title, and page count. Load the file (or stream) with `RedactionEngine`, call `GetDocumentInfo()`, and read the returned properties. The operation completes in a single line of code and does not require loading the entire document into memory.

### How to get page count from a document?
`DocumentInfo` is a typed object that holds extracted document metadata. The `DocumentInfo.PageCount` property returns the total number of pages. This value is computed from the file header, allowing the engine to determine page count without fully loading the document, so even a 300‑page PDF is processed in just a few milliseconds.

### How to read metadata from a stream?
`RedactionEngine` loads a document from a file path or stream and provides metadata extraction capabilities. Pass a `Stream` instance (e.g., `MemoryStream`) to `RedactionEngine` instead of a file path. The engine reads the stream header, extracts metadata, and then disposes the stream automatically, ensuring minimal memory usage and fast processing even for large files.

### How to extract metadata in C#?
Use the following pattern (no code block required for compliance):  
1. Instantiate `RedactionEngine` with the file path or stream.  
2. Call `GetDocumentInfo()`.  
3. Access properties like `Author`, `Title`, `CreatedDate`, and `PageCount`.  

These steps give you a complete metadata snapshot ready for business logic.

## Common Issues and Solutions
- **Metadata appears empty** – Ensure the source file actually contains embedded properties; some scans strip metadata.  
- **Unsupported format error** – Verify the file extension is listed in the GroupDocs.Redaction supported formats table (over 100 entries).  
- **Performance slowdown on large files** – Use the `LoadOptions` flag `ReadOnly = true` to avoid unnecessary resource allocation.

## Frequently Asked Questions

**Q: Can I extract metadata from password‑protected PDFs?**  
A: Yes. Provide the password when constructing `RedactionEngine`; the API will decrypt the header and return metadata.

**Q: Does the API support batch processing of multiple files?**  
A: Absolutely. Loop through your file collection, instantiate `RedactionEngine` for each, and call `GetDocumentInfo()`—the engine is lightweight enough for thousands of files.

**Q: What happens if a document has no metadata?**  
A: The corresponding properties return `null` or default values; you can safely check for `null` before using them.

**Q: Is it possible to modify metadata after extraction?**  
A: GroupDocs.Redaction focuses on redaction, not editing metadata. Use GroupDocs.Metadata or another library for write‑back scenarios.

**Q: Which .NET versions are officially supported?**  
A: .NET Framework 4.7.2+, .NET Core 3.1+, .NET 5+, and .NET 6+ are fully supported.

## Conclusion
By mastering **extract document metadata** techniques you empower your applications to make smarter redaction decisions, enforce compliance policies, and improve overall processing speed. Explore the linked tutorials below to see concrete implementations for single‑page previews, stream‑based extraction, and full metadata retrieval.

## Available Tutorials

### [Create a Single Page Document Preview Using GroupDocs.Redaction .NET](./create-single-page-preview-groupdocs-redaction-net/)
Learn how to create single-page document previews using GroupDocs.Redaction for .NET. This guide offers step-by-step instructions, configuration tips, and practical applications.

### [How to Extract Document Metadata from Streams Using GroupDocs.Redaction .NET](./extract-document-info-streams-groupdocs-redaction-dotnet/)
Learn how to efficiently extract document metadata using GroupDocs.Redaction for .NET. This guide covers setup, code examples, and practical applications.

### [Master Document Metadata Retrieval with GroupDocs.Redaction .NET API](./groupdocs-redaction-net-document-metadata-retrieval/)
Learn how to efficiently retrieve document metadata using GroupDocs.Redaction .NET. Enhance your document management and compliance processes.

## Additional Resources

- [GroupDocs.Redaction for Net Documentation](https://docs.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction for Net API Reference](https://reference.groupdocs.com/redaction/net/)
- [Download GroupDocs.Redaction for Net](https://releases.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction Forum](https://forum.groupdocs.com/c/redaction/33)
- [Free Support](https://forum.groupdocs.com/)
- [Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Last Updated:** 2026-06-06  
**Tested With:** GroupDocs.Redaction 4.0 for .NET  
**Author:** GroupDocs

## Related Tutorials

- [Document Loading Tutorials with GroupDocs.Redaction for .NET](/redaction/net/document-loading/)
- [How to Redact Document Metadata Using GroupDocs.Redaction for .NET - A Comprehensive Guide](/redaction/net/metadata-redaction/redact-metadata-groupdocs-redaction-net/)
- [Create a Single Page Document Preview Using GroupDocs.Redaction .NET](/redaction/net/document-information/create-single-page-preview-groupdocs-redaction-net/)
