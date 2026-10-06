---
additionalTitle: GroupDocs API References
date: 2026-10-06
description: Learn how to redact PDF pages, remove PDF annotations, and redact Excel
  cells using GroupDocs.Redaction for .NET – a secure, cross‑platform API for document
  redaction.
keywords:
- how to redact pdf
- remove pdf annotations
- redact excel cells
- redact pdf pages
- load pdf from stream
lastmod: 2026-10-06
linktitle: GroupDocs.Redaction for .NET Tutorials
og_description: How to redact PDF pages quickly with GroupDocs.Redaction for .NET.
  The API removes PDF annotations, redacts Excel cells, and protects sensitive data
  across 30+ formats.
og_image_alt: Guide to redact PDF pages using GroupDocs.Redaction for .NET
og_title: How to redact PDF pages – GroupDocs.Redaction for .NET
schemas:
- author: GroupDocs
  dateModified: '2026-10-06'
  description: Learn how to redact PDF pages, remove PDF annotations, and redact Excel
    cells using GroupDocs.Redaction for .NET – a secure, cross‑platform API for document
    redaction.
  headline: How to redact PDF pages with GroupDocs.Redaction for .NET
  type: TechArticle
- description: Learn how to redact PDF pages, remove PDF annotations, and redact Excel
    cells using GroupDocs.Redaction for .NET – a secure, cross‑platform API for document
    redaction.
  name: How to redact PDF pages with GroupDocs.Redaction for .NET
  steps:
  - name: load the PDF
    text: You can open a file from disk, a memory stream, or a remote source. The
      API accepts both a file path string and a `Stream` object, which is ideal for
      web services that receive uploads.
  - name: define the pages to redact
    text: Pass a list of zero‑based page indexes or a range string such as `"1-3,5"`
      to the `RemovePages` method. The library validates the range and throws a clear
      exception if a page does not exist.
  - name: save the sanitized document
    text: Call `Save` with the desired output format. You can keep the original PDF,
      export to a rasterized PDF, or stream the result directly to the client response.
  type: HowTo
- questions:
  - answer: Yes, the library removes the specified pages while preserving page numbering,
      bookmarks, and cross‑references for the remaining content.
    question: Can I redact PDF pages without affecting the rest of the document’s
      layout?
  - answer: Absolutely. Use `Redactor.RemoveAnnotations()` to strip all annotation
      objects in a single call.
    question: Is it possible to redact PDF annotations only?
  - answer: Load the workbook with `Redactor.LoadExcel(path)`, then call `Redactor.RedactCell(sheetName,
      cellAddress, RedactionMode.Blackout)` and save.
    question: How do I redact Excel cells directly?
  - answer: Yes, you can pass any `System.IO.Stream` to the `Load` method, which is
      ideal for processing files uploaded via ASP.NET Core controllers.
    question: Does GroupDocs.Redaction support loading PDFs from a stream?
  - answer: Metered licensing lets you pay per‑redaction operation, scaling cost‑effectively
      with usage spikes.
    question: What licensing model is recommended for high‑volume production use?
  type: FAQPage
tags:
- pdf redaction
- groupdocs.redaction
- .net document security
- redact pdf pages
title: How to redact PDF pages with GroupDocs.Redaction for .NET
type: docs
url: /net/
weight: 10
---

# How to redact PDF pages with GroupDocs.Redaction for .NET

If you need to **redact PDF pages** quickly and reliably, GroupDocs.Redaction for .NET gives you a full‑featured, cross‑platform API that removes sensitive content from over 30 file formats. Whether you’re building a compliance‑driven workflow, a document‑management portal, or a privacy‑first application, this library lets you permanently erase confidential data while preserving the rest of the document’s structure.

**GroupDocs.Redaction for .NET is a .NET library that enables permanent removal of sensitive content from more than 30 document formats.** It supports high‑volume processing, can handle multi‑hundred‑page files without loading the entire document into memory, and provides rasterization options that turn text into images for extra security.

{{% alert color="primary" %}}
GroupDocs.Redaction for .NET offers a comprehensive suite of tutorials and examples for implementing secure document redaction in your .NET applications. From basic text replacements to advanced metadata cleansing, these resources cover essential techniques for redacting sensitive information from documents. Learn how to permanently remove private data from various document formats including PDF, Word, Excel, PowerPoint, and images with precise control and complete removal of confidential content. Our step‑by‑step guides help you master both standard and advanced redaction capabilities to meet compliance requirements and protect sensitive information effectively.
{{% /alert %}}

## Quick answers
- **Can GroupDocs.Redaction redact entire PDF pages?** Yes, you can delete single pages or page ranges with a single API call.  
- **Does it support removing PDF annotations?** Absolutely – annotations, comments, and markup can be stripped in one step.  
- **Can I redact Excel cells without converting to PDF?** Yes, the library targets Excel worksheets directly.  
- **Is loading a PDF from a stream supported?** The API accepts `Stream` objects, enabling in‑memory processing.  
- **What .NET versions are compatible?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## What is redaction in the context of PDFs?
Redaction is the permanent removal or obscuring of sensitive content from a document so that it cannot be recovered or viewed later. In PDF files, redaction can target text, images, annotations, or whole pages, and the result is a sanitized file that retains its original layout.

## Why use GroupDocs.Redaction for .NET?
GroupDocs.Redaction for .NET provides a robust, high‑performance solution that can handle large documents while ensuring complete removal of sensitive data, offering built‑in rasterization, extensive format support, and detailed audit logging, making it ideal for compliance‑driven applications and enterprise environments.

- **30+ supported formats** – including PDF, DOCX, XLSX, PPTX, HTML, and common image types.  
- **Scalable performance** – processes 500‑page PDFs in under 5 seconds on a typical server, without loading the whole file into RAM.  
- **Built‑in rasterization** – converts redacted pages to images, guaranteeing that no hidden text remains.  
- **Compliance‑ready** – meets GDPR, HIPAA, and PCI‑DSS requirements with audit‑trail logging.

## Prerequisites
- .NET Framework 4.5+ **or** .NET Core 3.1+ installed on your development machine.  
- A valid GroupDocs.Redaction license (trial available for evaluation).  
- Access to the PDF, Excel, or Word files you intend to process.

## How to redact PDF pages step by step

Redactor is the core class in GroupDocs.Redaction that loads, modifies, and saves documents. RemovePages removes the specified pages from the loaded document.

Load the PDF, define the pages you want to remove, apply the redaction, and save the result. The following direct answer explains the core pattern:

Load the target PDF with `Redactor.Load(streamOrPath)`, call `Redactor.RemovePages(pageNumbers)` to delete the unwanted pages, and finally invoke `Redactor.Save(outputPath)` – this three‑step flow redacts pages in under a second for most documents.

### Step 1: load the PDF
You can open a file from disk, a memory stream, or a remote source. The API accepts both a file path string and a `Stream` object, which is ideal for web services that receive uploads.

### Step 2: define the pages to redact
Pass a list of zero‑based page indexes or a range string such as `"1-3,5"` to the `RemovePages` method. The library validates the range and throws a clear exception if a page does not exist.

### Step 3: save the sanitized document
Call `Save` with the desired output format. You can keep the original PDF, export to a rasterized PDF, or stream the result directly to the client response.

## Common issues and solutions
- **Issue:** Redaction appears to work but the original text is still searchable.  
  **Solution:** Enable rasterization (`Redactor.Rasterize = true`) before saving; this converts the page to an image, removing hidden text layers.  

- **Issue:** Large PDFs cause OutOfMemory exceptions.  
  **Solution:** Use `Redactor.Load(stream, loadOptions => loadOptions.EnableMemoryOptimization = true)` to process the file in chunks.  

- **Issue:** Annotations are not removed.  
  **Solution:** Call `Redactor.RemoveAnnotations()` after loading the document; this method strips comments, highlights, and form fields.

## Frequently asked questions

**Q: Can I redact PDF pages without affecting the rest of the document’s layout?**  
A: Yes, the library removes the specified pages while preserving page numbering, bookmarks, and cross‑references for the remaining content.

**Q: Is it possible to redact PDF annotations only?**  
A: Absolutely. Use `Redactor.RemoveAnnotations()` to strip all annotation objects in a single call.

**Q: How do I redact Excel cells directly?**  
A: Load the workbook with `Redactor.LoadExcel(path)`, then call `Redactor.RedactCell(sheetName, cellAddress, RedactionMode.Blackout)` and save.

**Q: Does GroupDocs.Redaction support loading PDFs from a stream?**  
A: Yes, you can pass any `System.IO.Stream` to the `Load` method, which is ideal for processing files uploaded via ASP.NET Core controllers.

**Q: What licensing model is recommended for high‑volume production use?**  
A: Metered licensing lets you pay per‑redaction operation, scaling cost‑effectively with usage spikes.

---

**Last Updated:** 2026-10-06  
**Tested With:** GroupDocs.Redaction 23.10 for .NET  
**Author:** GroupDocs  

---  

### GroupDocs.Redaction for .NET tutorials – how to redact PDF pages

### [Getting Started Tutorials](./getting-started/)

Start here if you’re new to GroupDocs.Redaction. This tutorial walks you through installation, licensing, and creating your first redaction project in .NET. You’ll see how to open a document, define a simple redaction rule, and save the sanitized file.

### [Advanced Redaction Techniques](./advanced-redaction/)

Dive deeper with custom redaction handlers, policies, callbacks, and AI‑assisted redaction. This guide shows you how to build flexible pipelines that can **redact PDF pages**, handle complex document structures, and integrate machine‑learning models for smarter content detection.

### [Annotation Redaction Tutorials](./annotation-redaction/)

Annotations often contain confidential notes. Learn how to locate, modify, or completely remove annotations, comments, and review markup from PDFs, Word files, and other supported formats.

### [Document Information Tutorials](./document-information/)

Understanding a document’s metadata is the first step to secure redaction. This tutorial explains how to retrieve document properties, enumerate supported formats, and generate preview images before you apply any redaction.

### [Document Loading Tutorials](./document-loading/)

Documents can reside on disk, in streams, or behind authentication layers. Learn the best practices for loading local files, memory streams, and password‑protected documents safely.

### [Document Saving Tutorials](./document-saving/)

After redaction you’ll need to persist the cleaned file. This guide covers saving in the original format, exporting to rasterized PDF, and streaming results directly to a client‑side application.

### [Format Handling Tutorials](./format-handling/)

GroupDocs.Redaction supports a wide range of formats. Explore how to work with different file types, create custom format handlers, and extend the library to cover niche document standards.

### [Image Redaction Tutorials](./image-redaction/)

Images can hide sensitive visual data. Learn to redact specific image regions, strip embedded pictures, and clean image metadata to ensure no hidden information remains.

### [Licensing and Configuration Tutorials](./licensing-configuration/)

Proper licensing is critical for production use. This tutorial shows you how to apply licenses, configure runtime settings, and implement metered licensing for scalable deployments.

### [Metadata Redaction Tutorials](./metadata-redaction/)

Metadata often leaks confidential details. Follow this guide to remove document properties, hidden comments, and other metadata from PDF, Word, Excel, and PowerPoint files.

### [OCR Integration Tutorials](./ocr-integration/)

When dealing with scanned PDFs or images, OCR is essential. Learn to integrate OCR engines, extract searchable text, and then **redact PDF pages** that contain sensitive information.

### [Page Redaction Tutorials](./page-redaction/)

Sometimes you need to eliminate entire pages. This tutorial demonstrates how to delete single pages, page ranges, and conditionally remove pages based on content.

### [PDF‑Specific Redaction Tutorials](./pdf-specific-redaction/)

PDFs have unique features like layers, annotations, and form fields. Master PDF‑only redaction techniques, including content filtering and preserving document integrity.

### [Rasterization Options Tutorials](./rasterization-options/)

Rasterized PDFs turn content into images, making data extraction impossible. Learn to configure noise, tilt, grayscale, and borders, and discover how to **save rasterized PDF** files for maximum security.

### [Spreadsheet Redaction Tutorials](./spreadsheet-redaction/)

Excel spreadsheets often contain confidential cells. This guide shows you how to target and **redact Excel cells**, hide formulas, and protect sensitive worksheets.

### [Text Redaction Tutorials](./text-redaction/)

Text is the most common data type to protect. Follow step‑by‑step instructions for exact‑phrase matching, regular‑expression redaction, and case‑sensitive searches, including how to **redact Word text** efficiently.

## Related Tutorials

- [How to Remove Annotations – Annotation Redaction Tutorials for GroupDocs.Redaction .NET](/redaction/net/annotation-redaction/)
- [How to Remove the Last Page of a PDF Using GroupDocs.Redaction for .NET](/redaction/net/page-redaction/remove-last-page-pdf-groupdocs-redaction-net/)
- [How to Redact PDF and Save as Rasterized PDF with GroupDocs.Redaction for .NET](/redaction/net/document-saving/groupdocs-redaction-net-rasterized-pdfs/)