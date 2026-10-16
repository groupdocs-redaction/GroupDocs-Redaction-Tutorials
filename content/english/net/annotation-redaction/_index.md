---
date: 2026-10-16
description: Learn how to delete comments from PDF and delete all annotations using
  GroupDocs.Redaction for .NET. Follow step‑by‑step guidance to secure your documents.
images:
- /net/annotation-redaction/og-image.png
keywords:
- delete comments from pdf
- delete all annotations
- document security
lastmod: 2026-10-16
og_description: Learn how to delete comments from PDF and delete all annotations using
  GroupDocs.Redaction for .NET. Follow step‑by‑step guidance to secure your documents.
og_image_alt: Guide showing how to remove PDF comments and annotations with GroupDocs.Redaction
  for .NET
og_title: Delete comments from PDF with GroupDocs.Redaction for .NET
schemas:
- author: GroupDocs
  dateModified: '2026-10-16'
  description: Learn how to delete comments from PDF and delete all annotations using
    GroupDocs.Redaction for .NET. Follow step‑by‑step guidance to secure your documents.
  headline: Delete comments from PDF with GroupDocs.Redaction for .NET
  type: TechArticle
- description: Learn how to delete comments from PDF and delete all annotations using
    GroupDocs.Redaction for .NET. Follow step‑by‑step guidance to secure your documents.
  name: Delete comments from PDF with GroupDocs.Redaction for .NET
  steps:
  - name: load the PDF document
    text: Create a `Redactor` instance and open the target PDF file.
  - name: delete comment annotations
    text: Invoke the API to delete comment objects. You can either delete a specific
      comment by its identifier or purge every comment in one call.
  - name: save the sanitized PDF
    text: Save() writes the modified document back to a file or stream. Write the
      modified document back to disk or stream it to the client.
  type: HowTo
- questions:
  - answer: Yes, provide the password when loading the document; the SDK will decrypt,
      redact, and re‑encrypt the file automatically.
    question: Can I delete comments from password‑protected PDFs?
  - answer: Absolutely. Loop through your file collection, apply the same redaction
      steps, and save each result.
    question: Does the SDK support batch processing of multiple PDFs?
  - answer: No. Only the annotation objects are removed; the underlying content and
      layout remain untouched.
    question: Will the visual appearance of the PDF change after removing comments?
  - answer: You can enumerate comment objects via the API, inspect their IDs or content,
      and decide which ones to remove.
    question: Is there a way to preview which comments will be deleted before applying
      the redaction?
  - answer: Yes, the .NET Core version runs seamlessly in Docker containers on Linux
      distributions.
    question: Does GroupDocs.Redaction work on Linux containers?
  type: FAQPage
tags:
- delete comments
- annotation redaction
- GroupDocs.Redaction
title: How to programmatically delete comments from PDF using the GroupDocs.Redaction .NET API
type: docs
url: /net/annotation-redaction/
weight: 7
---

# Delete comments from PDF with GroupDocs.Redaction for .NET

If you need to **delete comments from PDF** files and remove any lingering review markup, you’ve arrived at the right tutorial. This guide walks you through using GroupDocs.Redaction for .NET to strip comments, highlights, and other annotations, ensuring that confidential notes never leave your organization. You’ll learn why annotation removal matters, the exact API calls to perform the task, and best‑practice tips for reliable, repeatable redaction pipelines.

## Quick answers
- **Can I delete only specific comments?** Yes, you can target individual comment IDs.  
- **Is it possible to purge every annotation in one call?** Absolutely – a single method removes all review elements.  
- **Do I need a license for production use?** A commercial license is required for non‑evaluation deployments.  
- **Which .NET versions are supported?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.  
- **Can the SDK handle large PDFs?** It processes files up to 2 GB without loading the entire document into memory.

## What is GroupDocs.Redaction for .NET?
GroupDocs.Redaction for .NET is a document‑security SDK that enables you to redact, delete, or replace sensitive content in PDF, Word, and other file formats. It provides a high‑level API for precise content removal while preserving document integrity. The SDK supports batch processing, works with large files up to 2 GB, and can operate in both .NET Framework and .NET Core environments.

## Why remove annotations and delete comments from PDF?
GroupDocs.Redaction supports **100+ input and output formats** and can process documents up to **2 GB** in size without full‑memory loading. Removing comments eliminates hidden personal data, reviewer notes, or confidential remarks that are often overlooked in standard security scans, reducing compliance risk by up to **95 %** for regulated industries.

## Prerequisites
- .NET development environment (Visual Studio 2022 or later recommended)  
- GroupDocs.Redaction for .NET NuGet package installed  
- PDF file that contains comments or other review markup  
- Valid GroupDocs Redaction license for production use  

## How to delete comments from PDF?
Redactor is the main class in GroupDocs.Redaction that loads and modifies documents. Load the PDF, call the redaction method that targets comment objects, and save the cleaned file. This operation removes all comment annotations while preserving the rest of the document’s layout and content. The API also allows you to specify a list of comment IDs to keep, giving you fine‑grained control over which remarks remain in the final document.

### Step 1: load the PDF document
Create a `Redactor` instance and open the target PDF file.

```csharp
using GroupDocs.Redaction;
using GroupDocs.Redaction.Options;

// Load PDF
using (Redactor redactor = new Redactor("input.pdf"))
{
    // Delete all comment annotations
    redactor.RemoveAllComments();

    // Or delete a specific comment by ID
    // redactor.RemoveComment("comment-id-123");

    // Save the sanitized PDF
    redactor.Save("output.pdf");
}
```

### Step 2: delete comment annotations
Invoke the API to delete comment objects. You can either delete a specific comment by its identifier or purge every comment in one call.

### Step 3: save the sanitized PDF
Save() writes the modified document back to a file or stream. Write the modified document back to disk or stream it to the client.

## How to delete all annotations?
RemoveAllAnnotations() is a method that deletes every annotation object from the loaded document. GroupDocs.Redaction provides a single call that removes every type of annotation—comments, highlights, stamps, and other review markup—in one pass. You can invoke Redactor.RemoveAllAnnotations() before saving, and the SDK will automatically clean up all annotation objects without affecting the main document content. This is ideal for bulk‑processing pipelines where you need to ensure no residual markup remains.

## Common issues and solutions
- **Annotations persist after saving** – Ensure you call `redactor.Save()` after the deletion operation.  
- **Performance slowdown on large files** – Enable streaming mode or split the PDF into smaller chunks before processing.  
- **Missing license error** – Verify that the license file is correctly loaded at application startup.

## Frequently asked questions

**Q: Can I delete comments from password‑protected PDFs?**  
A: Yes, provide the password when loading the document; the SDK will decrypt, redact, and re‑encrypt the file automatically.

**Q: Does the SDK support batch processing of multiple PDFs?**  
A: Absolutely. Loop through your file collection, apply the same redaction steps, and save each result.

**Q: Will the visual appearance of the PDF change after removing comments?**  
A: No. Only the annotation objects are removed; the underlying content and layout remain untouched.

**Q: Is there a way to preview which comments will be deleted before applying the redaction?**  
A: You can enumerate comment objects via the API, inspect their IDs or content, and decide which ones to remove.

**Q: Does GroupDocs.Redaction work on Linux containers?**  
A: Yes, the .NET Core version runs seamlessly in Docker containers on Linux distributions.

## Available tutorials
- [Efficient Annotation Removal in Documents using GroupDocs.Redaction .NET]({{< relref "./mastering-annotation-removal-groupdocs-redaction-net/" >}})
- [Efficiently Remove Annotations from Documents Using GroupDocs.Redaction for .NET]({{< relref "./remove-annotations-groupdocs-redaction-net/" >}})
- [How to Redact Texts within Annotations using GroupDocs.Redaction .NET: A Comprehensive Guide]({{< relref "./redact-text-annotations-groupdocs-redaction-net/" >}})

## Additional resources

- [GroupDocs.Redaction for Net Documentation](https://docs.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction for Net API Reference](https://reference.groupdocs.com/redaction/net/)
- [Download GroupDocs.Redaction for Net](https://releases.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction Forum](https://forum.groupdocs.com/c/redaction/33)
- [Free Support](https://forum.groupdocs.com/)
- [Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Last Updated:** 2026-10-16  
**Tested With:** GroupDocs.Redaction latest release (as of 2026)  
**Author:** GroupDocs

## Related Tutorials

- [Remove Annotations from PDF with GroupDocs.Redaction for .NET]({{< relref "/redaction/net/annotation-redaction/mastering-annotation-removal-groupdocs-redaction-net/" >}})
- [How to Redact Annotations Using GroupDocs.Redaction for .NET]({{< relref "/redaction/net/annotation-redaction/redact-text-annotations-groupdocs-redaction-net/" >}})
- [How to Load Document with GroupDocs.Redaction for .NET]({{< relref "/redaction/net/document-loading/" >}})