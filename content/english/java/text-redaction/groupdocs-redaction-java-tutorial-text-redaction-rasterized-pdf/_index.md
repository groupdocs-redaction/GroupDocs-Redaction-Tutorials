---
date: '2026-08-20'
description: Learn how to redact text with GroupDocs.Redaction Java, save as rasterized
  PDF, replace exact phrases, and apply custom PDF settings.
images:
- /java/text-redaction/groupdocs-redaction-java-tutorial-text-redaction-rasterized-pdf/og-image.png
keywords:
- how to redact text
- save pdf as image
- convert pdf to image
lastmod: '2026-08-20'
og_description: How to redact text with GroupDocs.Redaction Java. This guide shows
  you exact phrase replacement, rasterized PDF creation, and PDF/A‑1a compliance in
  a few steps.
og_image_alt: Guide showing GroupDocs.Redaction Java code to redact text and create
  rasterized PDF
og_title: How to redact text with GroupDocs.Redaction Java library
schemas:
- author: GroupDocs
  dateModified: '2026-08-20'
  description: Learn how to redact text with GroupDocs.Redaction Java, save as rasterized
    PDF, replace exact phrases, and apply custom PDF settings.
  headline: How to redact text with GroupDocs.Redaction Java
  type: TechArticle
- description: Learn how to redact text with GroupDocs.Redaction Java, save as rasterized
    PDF, replace exact phrases, and apply custom PDF settings.
  name: How to redact text with GroupDocs.Redaction Java
  steps:
  - name: '**Sensitive data redaction** – automatically hide personal identifiers
      before sharing contracts.'
    text: '**Sensitive data redaction** – automatically hide personal identifiers
      before sharing contracts.'
  - name: '**Document archiving** – convert finalized reports to rasterized PDF/A
      for long‑term compliance.'
    text: '**Document archiving** – convert finalized reports to rasterized PDF/A
      for long‑term compliance.'
  - name: '**Bulk content update** – replace outdated terminology across hundreds
      of files with a single script.'
    text: '**Bulk content update** – replace outdated terminology across hundreds
      of files with a single script.'
  type: HowTo
- questions:
  - answer: Add the GroupDocs repository and the `groupdocs-redaction` dependency
      to your `pom.xml` as shown in the Maven Setup section.
    question: How do I install GroupDocs.Redaction in a Maven project?
  - answer: Yes, GroupDocs.Redaction supports PDF, DOCX, PPTX, and many other formats.
    question: Can I redact text from PDF files using this library?
  - answer: The `RedactorChangeLog` will return a status of `Failed`. Verify the phrase’s
      spelling and case sensitivity.
    question: What happens if the exact phrase isn’t found?
  - answer: Process them in smaller page ranges, enable rasterization only where needed,
      and always close the `Redactor` to free resources.
    question: How can I handle very large documents efficiently?
  - answer: Absolutely. Use `options.getRasterization().setPageIndex()` and `setPageCount()`
      to target the exact pages you want to rasterize.
    question: Is it possible to save rasterized PDFs with specific page ranges?
  type: FAQPage
tags:
- text redaction
- GroupDocs.Redaction
- Java PDF processing
title: How to redact text with GroupDocs.Redaction Java
type: docs
url: /java/text-redaction/groupdocs-redaction-java-tutorial-text-redaction-rasterized-pdf/
weight: 1
---

# How to redact text with GroupDocs.Redaction Java

In modern applications, **how to redact text** in a document while keeping the workflow fast and compliant is a frequent challenge for developers, auditors, and compliance officers. This tutorial walks you through using GroupDocs.Redaction for Java to locate exact phrases, replace them with secure overlays, and finally export the result as a rasterized PDF/A‑1a document—perfect for archival or legal distribution.

## Quick answers
- **What is the primary class for redaction?** `Redactor`  
- **Can I replace a phrase with a colored overlay?** Yes, using `ExactPhraseRedaction` and `ReplacementOptions`.  
- **How do I generate a rasterized PDF?** Enable rasterization via `SaveOptions.getRasterization().setEnabled(true)`.  
- **Which PDF compliance level is used in the example?** `PdfComplianceLevel.PdfA1a`.  
- **Do I need a license for production use?** A valid GroupDocs.Redaction license is required for production deployments.

## What is “how to redact text” in Java?
`Redaction` is the permanent removal or obscuring of sensitive content from a file so that it cannot be recovered or read later. With GroupDocs.Redaction you programmatically search for an exact phrase—such as a social‑security number or a confidential project code—and replace it with a red overlay, black box, or any custom visual element, guaranteeing that the original data is unrecoverable.

## Why use GroupDocs.Redaction for Java?
GroupDocs.Redaction supports **30+ input and output formats** (PDF, DOCX, PPTX, XLSX, HTML, and image types) and can process multi‑hundred‑page documents without loading the entire file into memory. Its exact‑phrase matching algorithm reduces false positives by > 95 % compared with generic keyword searches, and the built‑in rasterization engine lets you produce PDF/A‑1a files that are fully image‑based for long‑term preservation.

## Prerequisites
Before you start, ensure you have:

- **GroupDocs.Redaction for Java** (v24.9 or newer).  
- **Java Development Kit (JDK) 8+**.  
- An IDE such as IntelliJ IDEA, Eclipse, or NetBeans.  
- Maven for dependency management.  

### Required libraries and dependencies
- GroupDocs.Redaction for Java – add the repository and dependency to your `pom.xml` (see the Maven setup section).  
- Optional: any logging framework you prefer (SLF4J, Log4j, etc.).

### Knowledge prerequisites
- Basic Java syntax and file I/O.  
- Familiarity with Maven’s `pom.xml` structure.

## Setting up GroupDocs.Redaction for Java
### Maven setup
Add the GroupDocs repository and the `groupdocs-redaction` dependency to your `pom.xml` file:

```xml
<repositories>
   <repository>
      <id>repository.groupdocs.com</id>
      <name>GroupDocs Repository</name>
      <url>https://releases.groupdocs.com/redaction/java/</url>
   </repository>
</repositories>

<dependencies>
   <dependency>
      <groupId>com.groupdocs</groupId>
      <artifactId>groupdocs-redaction</artifactId>
      <version>24.9</version>
   </dependency>
</dependencies>
```

### Direct download
Alternatively, you can download the latest version directly from [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### License acquisition
- **Free trial** – explore the API without a license key.  
- **Temporary license** – use for extended evaluation.  
- **Full license** – required for production environments.

### Basic initialization and setup
The `Redactor` class is the entry point for all redaction operations. It loads a document, applies redaction rules, and saves the result.

```java
import com.groupdocs.redaction.Redactor;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
```

## How to redact text – exact phrase example
Redactor is the primary class that loads a document and applies redaction rules. ExactPhraseRedaction defines a rule that matches a specific string. This example demonstrates loading a file, creating an ExactPhraseRedaction rule, and executing the redaction in a single step, providing a concise workflow for developers while ensuring the original content is permanently obscured.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.ReplacementOptions;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
```

## How to save as rasterized PDF
SaveOptions is the configuration object that controls how a document is saved. By enabling its rasterization feature and selecting PDF/A‑1a compliance, you can produce an image‑only PDF where each page is rendered as a bitmap, meeting archival standards and preventing text extraction.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
try {
    RedactorChangeLog result = redactor.apply(new ExactPhraseRedaction(
        "John Doe", new ReplacementOptions(java.awt.Color.RED)));
    
    if (result.getStatus() != RedactionStatus.Failed) {
        // Successfully redacted the text
    }
} finally { 
    redactor.close(); 
}
```

## Practical applications
1. **Sensitive data redaction** – automatically hide personal identifiers before sharing contracts.  
2. **Document archiving** – convert finalized reports to rasterized PDF/A for long‑term compliance.  
3. **Bulk content update** – replace outdated terminology across hundreds of files with a single script.

## Performance considerations
- **Close the `Redactor`** after each operation to release file handles and memory.  
- **Batch processing** – load a list of files and loop through them, reusing a single `Redactor` instance when possible.  
- **Monitor resources** – use Java profiling tools to watch CPU and heap usage during large‑scale redactions.

## Frequently asked questions

**Q: How do I install GroupDocs.Redaction in a Maven project?**  
A: Add the GroupDocs repository and the `groupdocs-redaction` dependency to your `pom.xml` as shown in the Maven Setup section.

**Q: Can I redact text from PDF files using this library?**  
A: Yes, GroupDocs.Redaction supports PDF, DOCX, PPTX, and many other formats.

**Q: What happens if the exact phrase isn’t found?**  
A: The `RedactorChangeLog` will return a status of `Failed`. Verify the phrase’s spelling and case sensitivity.

**Q: How can I handle very large documents efficiently?**  
A: Process them in smaller page ranges, enable rasterization only where needed, and always close the `Redactor` to free resources.

**Q: Is it possible to save rasterized PDFs with specific page ranges?**  
A: Absolutely. Use `options.getRasterization().setPageIndex()` and `setPageCount()` to target the exact pages you want to rasterize.

## Conclusion
You now have a complete, end‑to‑end guide on **how to redact text** with GroupDocs.Redaction Java and **save as rasterized PDF**. By following these steps, you can protect sensitive information, meet strict compliance standards, and keep your Java services performant at scale.

**Next steps**  
- Dive deeper into the API by exploring the [official documentation](https://docs.groupdocs.com/redaction/java/).  
- Experiment with other redaction types such as `RegexRedaction` and `ImageRedaction`.  
- Join the community on the [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) for tips and best practices.

---

**Last Updated:** 2026-08-20  
**Tested With:** GroupDocs.Redaction Java 24.9  
**Author:** GroupDocs

```java
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.options.PdfComplianceLevel;
```

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
try {
    SaveOptions options = new SaveOptions();

    // Enable rasterization for converting pages into images.
    options.getRasterization().setEnabled(true);
    
    // Set the starting page and count for rasterization.
    options.getRasterization().setPageIndex(5);
    options.getRasterization().setPageCount(1);

    // Define PDF compliance level.
    options.getRasterization().setCompliance(PdfComplianceLevel.PdfA1a);

    // Append a suffix to avoid filename conflicts.
    options.setAddSuffix(true);

    // Save the document with these configurations.
    redactor.save(options);
} finally { 
    redactor.close(); 
}
```

## Related Tutorials

- [How to Redact Text with GroupDocs.Redaction for Java](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction/)
- [Java Text Redaction Tutorial: Guide with GroupDocs.Redaction](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction-guide/)