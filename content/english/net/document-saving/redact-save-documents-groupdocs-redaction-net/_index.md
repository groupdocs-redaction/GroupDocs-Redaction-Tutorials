---
date: '2026-07-20'
description: Learn how to redact documents, hide sensitive information, and save redacted
  files to a memory stream using GroupDocs.Redaction for .NET.
images:
- /net/document-saving/redact-save-documents-groupdocs-redaction-net/og-image.png
keywords:
- how to redact documents
- redact sensitive information
- redact specific text
- save to memory stream
- save redacted document
lastmod: '2026-07-20'
og_description: How to redact documents with GroupDocs.Redaction for .NET. Follow
  this step‑by‑step guide to hide sensitive information and save the redacted file
  to a memory stream.
og_image_alt: 'Developer guide: Redact and save documents using GroupDocs.Redaction
  for .NET'
og_title: How to Redact Documents with GroupDocs.Redaction for .NET
schemas:
- author: GroupDocs
  dateModified: '2026-07-20'
  description: Learn how to redact documents, hide sensitive information, and save
    redacted files to a memory stream using GroupDocs.Redaction for .NET.
  headline: How to Redact Documents with GroupDocs.Redaction for .NET – A Complete
    Guide
  type: TechArticle
- description: Learn how to redact documents, hide sensitive information, and save
    redacted files to a memory stream using GroupDocs.Redaction for .NET.
  name: How to Redact Documents with GroupDocs.Redaction for .NET – A Complete Guide
  steps:
  - name: '**Load** – Create a `Redactor` instance pointing to your file.'
    text: '**Load** – Create a `Redactor` instance pointing to your file.'
  - name: '**Apply** – Call `Apply` with an `ExactPhraseRedaction` (or other redaction
      type).'
    text: '**Apply** – Call `Apply` with an `ExactPhraseRedaction` (or other redaction
      type).'
  - name: '**Inspect** – Review `RedactorChangeLog` to confirm how many matches were
      found and replaced.'
    text: '**Inspect** – Review `RedactorChangeLog` to confirm how many matches were
      found and replaced.'
  type: HowTo
- questions:
  - answer: Yes—GroupDocs.Redaction treats PDF, DOCX, PPTX, and many image formats
      uniformly; simply point `Redactor` at a PDF file.
    question: Can I redact PDF files using the same API?
  - answer: Absolutely—once redacted, the content is permanently removed, regardless
      of subsequent conversions.
    question: Does the redaction survive after converting the document to another
      format?
  - answer: Use `RedactionOptions` to set the overlay color, opacity, or replace text
      with a custom string.
    question: How do I customize the redaction appearance?
  - answer: Yes—`RegexRedaction` lets you define patterns such as credit‑card numbers
      or email addresses.
    question: Is it possible to redact using regular expressions?
  - answer: .NET Framework 4.6+, .NET Core 3.1+, .NET 5, .NET 6, and .NET 7.
    question: What .NET versions are officially supported?
  type: FAQPage
tags:
- redact documents
- GroupDocs.Redaction
- .NET document processing
- C# redaction tutorial
title: How to Redact Documents with GroupDocs.Redaction for .NET – A Complete Guide
type: docs
url: /net/document-saving/redact-save-documents-groupdocs-redaction-net/
weight: 1
---

# How to Redact Documents with GroupDocs.Redaction for .NET

In modern enterprise environments, **how to redact documents** is a critical skill for protecting personal data, trade secrets, and compliance‑related information. This guide walks you through redacting sensitive information from Word, PDF, or image files and then saving the redacted output directly to a memory stream—all with GroupDocs.Redaction for .NET.

## Quick Answers
- **What does redaction do?** It permanently replaces selected content with a placeholder or removes it, ensuring the data can never be recovered.  
- **Which formats are supported?** Over 30 file types, including PDF, DOCX, PPTX, and common image formats.  
- **Can I redact without writing to disk?** Yes—save the result to a `MemoryStream` for in‑memory processing.  
- **Do I need a license for production?** A full license is required for production use; a free trial is available for evaluation.  
- **Is it .NET Core compatible?** Absolutely—GroupDocs.Redaction works with .NET Framework 4.6+, .NET Core 3.1+, and .NET 5/6/7.

## What is Document Redaction?
Document redaction permanently removes or obscures confidential text, images, and metadata from a file, ensuring that the hidden content cannot be recovered, viewed, or extracted later. It replaces the sensitive elements with a placeholder such as a black rectangle or custom text, and updates the document structure so the redacted data is irretrievable.

## Why Use GroupDocs.Redaction to Redact Documents?
GroupDocs.Redaction supports **30+ file formats** and can handle files up to **2 GB** without loading the entire document into memory, delivering a **30 % faster processing time** compared with many competitors. Its API lets you apply exact‑phrase, regular‑expression, or image‑based redactions with a single method call, making it the most efficient choice for .NET developers.

## Prerequisites
- **GroupDocs.Redaction** NuGet package (latest version).  
- .NET Framework 4.6+ **or** .NET Core 3.1+ installed.  
- A C#‑compatible IDE such as Visual Studio 2022.  
- Basic C# knowledge and familiarity with file I/O.

### Required Libraries and Versions
- **GroupDocs.Redaction** – always use the newest release to access the latest redaction algorithms and security patches.  
- **System.IO** – for stream handling (built‑in .NET).

### License Acquisition Steps
- **Free Trial:** Sign up on the GroupDocs website for a 30‑day trial.  
- **Temporary License:** Request a temporary key for development testing.  
- **Full License:** Purchase a production license for unlimited usage.

## Basic Initialization and Setup
The `Redactor` class is the entry point for all redaction operations in GroupDocs.Redaction. After you install the NuGet package, you instantiate `Redactor` with the path to the source document.

```csharp
using GroupDocs.Redaction;
using System.IO;

// Initialize Redactor with the source file path
Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

## How to Redact Specific Text in a Document?
To redact specific text, load the source file with a `Redactor` instance, then apply an `ExactPhraseRedaction` that targets the exact string you want to hide. The API scans the document, replaces each match with the chosen overlay, and records the changes in a change log, allowing you to verify the redaction before saving.

```csharp
RedactorChangeLog result = redactor.Apply(new ExactPhraseRedaction("John Doe"));
```

The `ExactPhraseRedaction` class replaces every occurrence of the exact phrase with a black rectangle (or any custom placeholder you configure).  

**Step‑by‑Step:**
1. **Load** – Create a `Redactor` instance pointing to your file.  
2. **Apply** – Call `Apply` with an `ExactPhraseRedaction` (or other redaction type).  
3. **Inspect** – Review `RedactorChangeLog` to confirm how many matches were found and replaced.  

## How to Save a Redacted Document to a Memory Stream?
`MemoryStream` is a .NET stream that stores data in memory, allowing fast read/write without disk I/O. Using the `Save` method, you can direct the redacted output into a `MemoryStream`, which can then be sent over a network, stored in a database, or returned directly from an API endpoint without creating temporary files.

```csharp
using (MemoryStream stream = new MemoryStream())
{
    // Save the redacted document directly into the stream
    redactor.Save(stream);
    // Optionally reset the stream position for downstream consumers
    stream.Position = 0;
    // The stream now contains the redacted file ready for use
}
```

**Key Points:**
- The `Save` method writes the redacted output to any `Stream` implementation, including `MemoryStream`.  
- No temporary files are created, which improves security and performance.  
- You can combine this with ASP.NET Core’s `FileStreamResult` to return the file directly to a browser.

## Common Pitfalls and Solutions
| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Redaction not applied** | The phrase case differs from the source. | Use `ExactPhraseRedaction("John Doe", caseSensitive: false)` or a regular‑expression redaction for flexible matching. |
| **Large files cause OutOfMemory** | Attempting to load the whole file into memory. | GroupDocs.Redaction streams data internally; ensure you’re using the latest version which processes files in chunks. |
| **Saved file is corrupted** | Stream not reset before sending. | After `redactor.Save(stream)`, set `stream.Position = 0` before reading or returning it. |

## Frequently Asked Questions

**Q: Can I redact PDF files using the same API?**  
A: Yes—GroupDocs.Redaction treats PDF, DOCX, PPTX, and many image formats uniformly; simply point `Redactor` at a PDF file.

**Q: Does the redaction survive after converting the document to another format?**  
A: Absolutely—once redacted, the content is permanently removed, regardless of subsequent conversions.

**Q: How do I customize the redaction appearance?**  
A: Use `RedactionOptions` to set the overlay color, opacity, or replace text with a custom string.

**Q: Is it possible to redact using regular expressions?**  
A: Yes—`RegexRedaction` lets you define patterns such as credit‑card numbers or email addresses.

**Q: What .NET versions are officially supported?**  
A: .NET Framework 4.6+, .NET Core 3.1+, .NET 5, .NET 6, and .NET 7.

---

**Last Updated:** 2026-07-20  
**Tested With:** GroupDocs.Redaction 23.12 for .NET  
**Author:** GroupDocs  

---

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
using (Redactor redactor = new Redactor(sourceFile))
{
    // Continue to apply redactions...
}
```

## Related Tutorials

- [How to Load and Redact Documents Using GroupDocs.Redaction .NET&#58; A Complete Guide](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [Save Redacted Documents in Original Format Using GroupDocs.Redaction .NET](/redaction/net/document-saving/save-redacted-docs-original-format-groupdocs-redaction-net/)
- [Secure Document Redaction in .NET Using Streams&#58; A Guide for GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)