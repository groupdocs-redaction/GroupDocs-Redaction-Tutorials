---
title: "How to Redact Text with GroupDocs.Redaction Java"
description: "Learn how to redact text using GroupDocs.Redaction Java and save as rasterized PDF with exact phrase replacement and custom PDF settings."
date: "2026-02-26"
weight: 1
url: "/java/text-redaction/groupdocs-redaction-java-tutorial-text-redaction-rasterized-pdf/"
keywords:
- GroupDocs.Redaction Java
- text redaction Java
- rasterized PDF conversion
type: docs
---
# How to Redact Text with GroupDocs.Redaction Java

In today’s data‑driven world, **how to redact text** in a document safely and efficiently is a top concern for developers and compliance officers alike. Whether you need to hide personal identifiers, confidential client details, or internal project codes, GroupDocs.Redaction for Java gives you a reliable way to locate exact phrases and replace them with secure overlays. This tutorial also shows you **how to save as rasterized PDF**, turning each page into an image‑based PDF that meets archival standards.

## Quick Answers
- **What is the primary class for redaction?** `Redactor`  
- **Can I replace a phrase with a colored overlay?** Yes, using `ExactPhraseRedaction` and `ReplacementOptions`.  
- **How do I generate a rasterized PDF?** Enable rasterization via `SaveOptions.getRasterization().setEnabled(true)`.  
- **Which PDF compliance level is used in the example?** `PdfComplianceLevel.PdfA1a`.  
- **Do I need a license for production use?** A valid GroupDocs.Redaction license is required for production deployments.

## What is “how to redact text” in Java?
Redaction is the process of permanently removing or obscuring sensitive content from a file. With GroupDocs.Redaction, you can programmatically search for an exact phrase—such as a name or ID—and replace it with a red overlay, a black box, or any custom visual element, ensuring the original data cannot be recovered.

## Why Use GroupDocs.Redaction for Java?
- **Exact phrase matching** eliminates false positives.  
- **Built‑in rasterization** lets you create PDF/A‑compliant, image‑only PDFs for long‑term storage.  
- **Cross‑format support** works with DOCX, PDF, PPTX, and more, so you can apply the same code across document types.  
- **Performance‑focused API** lets you batch‑process large document sets while keeping memory usage low.

## Prerequisites
Before diving in, make sure you have the following:

- **GroupDocs.Redaction for Java** (v24.9 or newer).  
- **Java Development Kit (JDK) 8+**.  
- An IDE such as IntelliJ IDEA, Eclipse, or NetBeans.  
- Maven for dependency management.  

### Required Libraries and Dependencies
- **GroupDocs.Redaction for Java** – add the repository and dependency to your `pom.xml` (see code block below).  
- **Optional**: Any additional logging libraries you prefer.

### Knowledge Prerequisites
- Basic Java syntax and file I/O.  
- Familiarity with Maven’s `pom.xml` structure.  

## Setting Up GroupDocs.Redaction for Java
### Maven Setup
Add the repository and dependency to your `pom.xml` file:

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

### Direct Download
Alternatively, you can download the latest version directly from [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### License Acquisition
- **Free Trial** – explore the API without a license key.  
- **Temporary License** – use for extended evaluation.  
- **Full License** – required for production environments.

### Basic Initialization and Setup
Below is the minimal code to create a `Redactor` instance pointing at a sample DOCX file:

```java
import com.groupdocs.redaction.Redactor;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
```

## How to Redact Text – Exact Phrase Example
### Step 1: Import Required Classes
These imports give you access to the redaction engine and replacement options:

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.ReplacementOptions;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
```

### Step 2: Create and Apply the Redaction
The following snippet searches for the phrase **“John Doe”** and replaces it with a red overlay:

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

**Why this matters:** `ReplacementOptions` lets you control the visual style of the redaction, ensuring the hidden content cannot be recovered by copy‑paste or OCR.

## How to Save as Rasterized PDF
### Step 1: Import SaveOptions Classes
These classes let you configure PDF output, including rasterization and compliance levels:

```java
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.options.PdfComplianceLevel;
```

### Step 2: Configure and Apply Saving Options
After redacting, you can export the document as a rasterized PDF. The example below rasterizes page 5 only and forces PDF/A‑1a compliance:

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

**Key point:** Rasterizing a PDF **converts each page to an image**, which removes hidden text layers and makes the document tamper‑proof—ideal for legal archiving.

## Practical Applications
1. **Sensitive Data Redaction** – Automatically hide personal identifiers before sharing contracts.  
2. **Document Archiving** – Convert finalized reports to rasterized PDF/A for long‑term compliance.  
3. **Bulk Content Update** – Replace outdated terminology across hundreds of files with a single script.

## Performance Considerations
- **Close the `Redactor`** after each operation to release file handles and memory.  
- **Batch Processing** – Load a list of files and loop through them, reusing a single `Redactor` instance when possible.  
- **Monitor Resources** – Use Java profiling tools to watch CPU and heap usage during large‑scale redactions.

## Frequently Asked Questions

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
You now have a complete, end‑to‑end guide on **how to redact text** with GroupDocs.Redaction Java and **save as rasterized PDF**. By following these steps, you can protect sensitive information, meet compliance requirements, and maintain high performance in production workloads.

**Next Steps**  
- Dive deeper into the API by exploring the [official documentation](https://docs.groupdocs.com/redaction/java/).  
- Experiment with other redaction types (e.g., `RegexRedaction`, `ImageRedaction`).  
- Join the community on the [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) for tips and best practices.

---

**Last Updated:** 2026-02-26  
**Tested With:** GroupDocs.Redaction Java 24.9  
**Author:** GroupDocs