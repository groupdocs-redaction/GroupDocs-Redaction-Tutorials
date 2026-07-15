---
title: "How to Load Document with GroupDocs.Redaction for .NET"
description: "Learn how to load document, including from streams and password‑protected files, using GroupDocs.Redaction for .NET."
date: 2026-06-11
keywords:
  - how to load document
  - redact password protected pdf
  - load password protected file
  - load document from stream
weight: 2
url: "/net/document-loading/"
type: docs
schemas:
- type: TechArticle
  headline: How to Load Document with GroupDocs.Redaction for .NET
  description: Learn how to load document, including from streams and password‑protected
    files, using GroupDocs.Redaction for .NET.
  dateModified: '2026-06-11'
  author: GroupDocs
- type: FAQPage
  questions:
  - question: Can I load DOCX files the same way I load PDFs?
    answer: Yes—GroupDocs.Redaction automatically detects the DOCX format when you
      pass the file path or stream, so no extra code is needed.
  - question: Does the library support loading files from Azure Blob Storage?
    answer: Absolutely. Retrieve the blob as a byte array or stream and feed it to
      the `RedactionEngine` constructor.
  - question: What happens if I provide the wrong password?
    answer: The constructor throws a `PasswordIncorrectException`. Catch this exception
      to prompt the user for the correct password.
  - question: Is it possible to load multiple documents simultaneously?
    answer: Yes—each `RedactionEngine` instance is independent and thread‑safe, allowing
      parallel processing in background services.
  - question: Do I need to dispose of the RedactionEngine manually?
    answer: The engine implements `IDisposable`. Call `Dispose()` or wrap it in a
      `using` block to release file handles promptly.
---

# How to Load Document with GroupDocs.Redaction for .NET

In this guide you’ll discover **how to load document** files into GroupDocs.Redaction for .NET from a variety of sources—local disk, memory streams, and even password‑protected files. Whether you’re building a redaction service, an automated compliance pipeline, or a simple desktop utility, mastering these loading techniques lets you prepare any document for secure redaction quickly and reliably.

## Quick Answers
- **What is the first step?** Install the GroupDocs.Redaction NuGet package and add the `using GroupDocs.Redaction;` namespace.  
- **Can I load a PDF from a stream?** Yes—pass a `MemoryStream` containing the PDF bytes to the `RedactionEngine` constructor.  
- **How do I open a password‑protected file?** Provide the password as a second argument when creating the `RedactionEngine`.  
- **Is there a limit on file size?** GroupDocs.Redaction processes files up to 2 GB without loading the entire file into memory.  
- **Do I need a license for development?** A temporary license works for testing; a full license is required for production deployments.

## How to Load Document?
`RedactionEngine` is the core class that loads and prepares documents for redaction. Load a document by creating a `RedactionEngine` instance with the file path (or stream) and, if necessary, the password. This single‑line call reads the file, validates the format, and builds the internal document model ready for redaction. For example, loading a PDF from disk is as simple as `new RedactionEngine("sample.pdf")`. When a password is required, use `new RedactionEngine("secret.pdf", "MyPassword")`. Loading from a stream follows the same pattern with a `MemoryStream` argument.

## What is GroupDocs.Redaction?
GroupDocs.Redaction is a .NET library that enables developers to locate and permanently remove sensitive content from PDF, DOCX, PPTX, and over 30 other file formats. It offers pixel‑perfect redaction, OCR support, and batch processing, making it ideal for compliance‑driven applications that require reliable and secure data protection across many document types.

## Why Use GroupDocs.Redaction for Document Loading?
GroupDocs.Redaction provides a high‑performance, low‑memory streaming engine that can handle large files up to 2 GB, while also supporting password‑protected documents out‑of‑the‑box. This combination of speed, flexibility, and security makes it the preferred choice for developers who need to load documents quickly and safely before applying redaction rules.

- **Broad format support:** Handles **30+** document types, including PDF, Word, Excel, PowerPoint, and image files.  
- **High‑performance streaming:** Processes files up to **2 GB** using a low‑memory streaming engine, eliminating the need for full file loading.  
- **Password handling:** Seamlessly opens **password‑protected PDFs and Office files** with a single method overload, reducing code complexity.  
- **Thread‑safe API:** Allows concurrent loading of multiple documents in multi‑threaded services without race conditions.

## Prerequisites
- .NET 6.0 or later (the library also supports .NET Core 3.1 and .NET Framework 4.6.1+).  
- A valid GroupDocs.Redaction license (temporary license for testing).  
- Access to the document files you intend to redact (local path, byte array, or stream).

## Loading Documents from Different Sources

### Load from Local Disk
Provide the absolute or relative path to the file when constructing the engine. The library automatically detects the format and prepares it for redaction.

### Load from a Memory Stream
Read the file into a `byte[]`, wrap it in a `MemoryStream`, and pass the stream to the constructor. This approach is perfect for web APIs that receive files as uploads.

### Load Password‑Protected Files
When a document is encrypted, supply the password as the second argument. The engine decrypts the file on the fly and makes the content available for redaction without additional steps.

## Common Issues and Solutions

- **Error: “File format not supported.”**  
  Verify that the file extension matches a supported format and that the file isn’t corrupted. GroupDocs.Redaction supports over 30 formats; consult the API reference for the full list.

- **Password‑related exception.**  
  Ensure the password string is correct and that the file actually requires a password. Passing an empty string to a protected file will trigger an authentication error.

- **Out‑of‑memory for very large files.**  
  Use the streaming overload (`RedactionEngine(Stream)`) instead of loading the file by path. This keeps memory usage low even for multi‑hundred‑page PDFs.

## Frequently Asked Questions

**Q: Can I load DOCX files the same way I load PDFs?**  
A: Yes—GroupDocs.Redaction automatically detects the DOCX format when you pass the file path or stream, so no extra code is needed.

**Q: Does the library support loading files from Azure Blob Storage?**  
A: Absolutely. Retrieve the blob as a byte array or stream and feed it to the `RedactionEngine` constructor.

**Q: What happens if I provide the wrong password?**  
A: The constructor throws a `PasswordIncorrectException`. Catch this exception to prompt the user for the correct password.

**Q: Is it possible to load multiple documents simultaneously?**  
A: Yes—each `RedactionEngine` instance is independent and thread‑safe, allowing parallel processing in background services.

**Q: Do I need to dispose of the RedactionEngine manually?**  
A: The engine implements `IDisposable`. Call `Dispose()` or wrap it in a `using` block to release file handles promptly.

## Additional Resources

- [How to Load and Redact Documents Using GroupDocs.Redaction .NET&#58; A Complete Guide](./groupdocs-redaction-net-load-redact-documents/)
- [How to Securely Redact Password-Protected Documents Using GroupDocs.Redaction in .NET](./secure-redact-password-protected-documents-groupdocs-redaction-net/)
- [GroupDocs.Redaction for Net Documentation](https://docs.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction for Net API Reference](https://reference.groupdocs.com/redaction/net/)
- [Download GroupDocs.Redaction for Net](https://releases.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction Forum](https://forum.groupdocs.com/c/redaction/33)
- [Free Support](https://forum.groupdocs.com/)
- [Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Last Updated:** 2026-06-11  
**Tested With:** GroupDocs.Redaction 5.5 for .NET  
**Author:** GroupDocs

## Related Tutorials

- [How to Load and Redact Documents Using GroupDocs.Redaction .NET: A Complete Guide](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [Redact and Save Documents with GroupDocs.Redaction for .NET: A Complete Guide](/redaction/net/document-saving/redact-save-documents-groupdocs-redaction-net/)
