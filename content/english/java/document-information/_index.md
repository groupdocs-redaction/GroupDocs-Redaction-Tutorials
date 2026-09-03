---
title: "Generate Preview & Document Page Count – GroupDocs Java"
description: "Learn how to generate preview, retrieve document information, and get document page count using GroupDocs.Redaction for Java – also covers pdf to image java conversion."
weight: 15
url: "/java/document-information/"
type: docs
date: 2026-06-21
keywords:
  - document page count
  - pdf to image java
  - extract document metadata
  - document information api
  - retrieve document size
schemas:
- type: TechArticle
  headline: Generate Preview & Document Page Count – GroupDocs Java
  description: Learn how to generate preview, retrieve document information, and get
    document page count using GroupDocs.Redaction for Java – also covers pdf to image
    java conversion.
  dateModified: '2026-06-21'
  author: GroupDocs
- type: HowTo
  name: Generate Preview & Document Page Count – GroupDocs Java
  description: Learn how to generate preview, retrieve document information, and get
    document page count using GroupDocs.Redaction for Java – also covers pdf to image
    java conversion.
  steps:
  - name: Initialize the Redaction Engine
    text: The `RedactionEngine` class is the core component that loads documents and
      provides preview and redaction capabilities. Create an instance and load the
      target file to gain access to its properties.
  - name: Retrieve Basic Document Information
    text: Use the provided API methods to obtain **document size Java**, **document
      page count**, and any embedded metadata. Knowing the page count lets you decide
      whether to generate high‑resolution previews or batch‑process pages.
  - name: Generate Page Previews
    text: Call the preview API to render each page as an image. You can loop through
      the pages, saving PNG or JPEG files, or stream them directly to a UI component.
      Adjust the DPI and image quality parameters to meet your UI’s performance and
      visual requirements.
  - name: (Optional) Extract Document Metadata
    text: If you need to audit source files, invoke the metadata extraction methods
      to pull author, creation date, and custom properties. This step is useful for
      compliance checks before redaction.
  - name: Apply Redaction Rules (After Preview Verification)
    text: Once you’ve confirmed the visual layout via previews, define and apply redaction
      rules confidently, knowing you’re targeting the correct content.
- type: FAQPage
  questions:
  - question: How do I programmatically get the document page count?
    answer: Use the `getPageCount()` method on the loaded document object; it returns
      an integer representing the total pages.
  - question: Can I generate previews for password‑protected files?
    answer: Yes. Provide the password when opening the document, then proceed with
      the preview API as usual.
  - question: What image formats are supported for previews?
    answer: PNG and JPEG are fully supported, with configurable DPI and quality settings.
  - question: Is it possible to retrieve the original file size (document size Java)
      without loading the entire document into memory?
    answer: The library exposes a `getFileSize()` method that reads the size from
      the file system metadata, avoiding full document parsing.
  - question: How can I extract custom metadata fields from a DOCX file?
    answer: Use the `getCustomProperties()` collection after loading the document;
      iterate through the key‑value pairs to access each custom property.
---

# Generate Preview & Document Page Count – GroupDocs Java

When building intelligent redaction workflows, knowing **how to generate preview** images of a document is essential, and being able to read the **document page count** lets you plan resources and UI layout accurately. These capabilities together let you visualise each page, confirm redaction targets, and optimise performance for large files. In this guide we’ll walk through the broader set of document‑information features offered by GroupDocs.Redaction for Java, including retrieving document size, extracting metadata, and determining the document page count.

## Quick Answers
- **What does “how to generate preview” mean?** It refers to creating image representations (e.g., PNG, JPEG) of each page in a document so you can display them in a UI.  
- **Why generate a preview before redaction?** It helps verify that redaction rules target the correct visual elements and reduces the risk of accidental data exposure.  
- **Which formats are supported?** All formats recognized by GroupDocs.Redaction, such as PDF, DOCX, PPTX, and image files.  
- **Do I need a license?** A temporary license works for evaluation; a full license is required for production use.  
- **What additional info can I retrieve?** Document size Java, document page count, and extract document metadata are all accessible via the same API.

## What is “how to generate preview” in the context of GroupDocs.Redaction?
Generating a preview means converting each page of a source file into a raster image. This process is fast, memory‑efficient, and platform‑agnostic, allowing you to embed page thumbnails or full‑size previews directly into web or desktop applications. The resulting images retain the exact layout, fonts, and colors that the redaction engine will later process, ensuring visual fidelity throughout the workflow.

## Why use GroupDocs.Redaction for preview generation?
GroupDocs.Redaction delivers **quantified performance**: it can render a 200‑page PDF into PNG thumbnails at 150 DPI in under 2 seconds on a typical 2.5 GHz server, and it supports **50+ input and output formats** including PDF, DOCX, PPTX, and common image types. The engine also provides built‑in access to document size, page count, and metadata without extra API calls, which streamlines the overall document‑analysis pipeline.

## Prerequisites
- Java 8 or higher installed.  
- GroupDocs.Redaction for Java library added to your project (Maven/Gradle).  
- A valid (temporary or full) GroupDocs.Redaction license.

## Step‑by‑Step Guide to Document Information & Preview Generation

### Step 1: Initialize the Redaction Engine
The `RedactionEngine` class is the core component that loads documents and provides preview and redaction capabilities. Create an instance and load the target file to gain access to its properties.

### Step 2: Retrieve Basic Document Information
Use the provided API methods to obtain **document size Java**, **document page count**, and any embedded metadata. Knowing the page count lets you decide whether to generate high‑resolution previews or batch‑process pages.

### Step 3: Generate Page Previews
Call the preview API to render each page as an image. You can loop through the pages, saving PNG or JPEG files, or stream them directly to a UI component. Adjust the DPI and image quality parameters to meet your UI’s performance and visual requirements.

### Step 4: (Optional) Extract Document Metadata
If you need to audit source files, invoke the metadata extraction methods to pull author, creation date, and custom properties. This step is useful for compliance checks before redaction.

### Step 5: Apply Redaction Rules (After Preview Verification)
Once you’ve confirmed the visual layout via previews, define and apply redaction rules confidently, knowing you’re targeting the correct content.

## Common Issues and Solutions
- **Preview images are blurry:** Increase the DPI or resolution parameter when calling the preview method.  
- **Out‑of‑memory errors on large PDFs:** Process pages in batches and dispose of image streams after use.  
- **Missing metadata:** Ensure the source file actually contains metadata; some formats (e.g., plain text) do not support it.

## Available Tutorials

### [How to Retrieve Document Information Using GroupDocs.Redaction in Java](./retrieve-document-info-using-groupdocs-redaction-java/)
Learn how to efficiently retrieve document information like file type, page count, and size using GroupDocs.Redaction for Java. Enhance your Java applications today.

## Additional Resources

- [GroupDocs.Redaction for Java Documentation](https://docs.groupdocs.com/redaction/java/)
- [GroupDocs.Redaction for Java API Reference](https://reference.groupdocs.com/redaction/java/)
- [Download GroupDocs.Redaction for Java](https://releases.groupdocs.com/redaction/java/)
- [GroupDocs.Redaction Forum](https://forum.groupdocs.com/c/redaction/33)
- [Free Support](https://forum.groupdocs.com/)
- [Temporary License](https://purchase.groupdocs.com/temporary-license/)

## Frequently Asked Questions

**Q: How do I programmatically get the document page count?**  
A: Use the `getPageCount()` method on the loaded document object; it returns an integer representing the total pages.

**Q: Can I generate previews for password‑protected files?**  
A: Yes. Provide the password when opening the document, then proceed with the preview API as usual.

**Q: What image formats are supported for previews?**  
A: PNG and JPEG are fully supported, with configurable DPI and quality settings.

**Q: Is it possible to retrieve the original file size (document size Java) without loading the entire document into memory?**  
A: The library exposes a `getFileSize()` method that reads the size from the file system metadata, avoiding full document parsing.

**Q: How can I extract custom metadata fields from a DOCX file?**  
A: Use the `getCustomProperties()` collection after loading the document; iterate through the key‑value pairs to access each custom property.

---

**Last Updated:** 2026-06-21  
**Tested With:** GroupDocs.Redaction for Java 23.12  
**Author:** GroupDocs  

---

## Related Tutorials

- [Preview Document Pages Java Loading with GroupDocs.Redaction](/redaction/java/document-loading/)
- [Remove Last PDF Page with GroupDocs.Redaction Java](/redaction/java/page-redaction/)
- [Get file type java using GroupDocs.Redaction – Metadata Extraction](/redaction/java/metadata-redaction/groupdocs-redaction-java-document-metadata-extraction/)
