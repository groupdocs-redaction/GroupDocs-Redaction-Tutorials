---
date: '2026-08-14'
description: How to redact text in Java documents using GroupDocs.Redaction – mask
  personal information and replace sensitive text efficiently.
images:
- /java/text-redaction/groupdocs-redaction-java-text-redaction/og-image.png
keywords:
- how to redact text
- GroupDocs Redaction Java
- text redaction Java
- mask personal information
lastmod: '2026-08-14'
og_description: How to redact text with GroupDocs.Redaction for Java lets you permanently
  mask personal data and replace sensitive strings across PDFs, DOCX, and more, ensuring
  GDPR and HIPAA compliance.
og_image_alt: 'Guide: redact text in Java using GroupDocs.Redaction library'
og_title: How to redact text with GroupDocs.Redaction for Java
schemas:
- author: GroupDocs
  dateModified: '2026-08-14'
  description: How to redact text in Java documents using GroupDocs.Redaction – mask
    personal information and replace sensitive text efficiently.
  headline: How to redact text with GroupDocs.Redaction for Java
  type: TechArticle
- description: How to redact text in Java documents using GroupDocs.Redaction – mask
    personal information and replace sensitive text efficiently.
  name: How to redact text with GroupDocs.Redaction for Java
  steps:
  - name: initialize the redactor
    text: '`Redactor` is the core class that loads a document, applies redaction rules,
      and writes the output.'
  - name: apply exact‑phrase redaction
    text: '`ExactPhraseRedaction` searches for an exact string match, while `ReplacementOptions`
      defines how the matched text should be replaced. - **Parameters:** - `"John
      Doe"` – the exact text to be redacted. - `ReplacementOptions("[personal]")`
      – the string that will replace the original content, effective'
  - name: save the redacted document
    text: '`Redactor.save` writes the modified document to a new file or overwrites
      the original, preserving the original format.'
  - name: clean up resources
    text: Always call `Redactor.close()` to release native resources and avoid memory
      leaks.
  type: HowTo
- questions:
  - answer: Yes, the library supports PDF, DOCX, XLSX, PPTX, and many other formats.
    question: Can I redact text from PDFs using GroupDocs.Redaction?
  - answer: No. Redactions permanently remove the original content, so keep a backup
      of the source file.
    question: Is a redaction reversible?
  - answer: Process them in chunks, use batch mode, and monitor memory usage with
      profiling tools.
    question: How do I handle very large documents efficiently?
  - answer: Besides DOCX and PDF, you can redact TXT, RTF, XLSX, PPTX, and more.
    question: What other text formats are supported?
  - answer: Absolutely. The API can be called from web services, background jobs,
      or CI/CD pipelines.
    question: Can I integrate GroupDocs.Redaction into existing workflows?
  type: FAQPage
tags:
- text redaction
- GroupDocs.Redaction
- Java document processing
- privacy compliance
- redaction API
title: How to redact text with GroupDocs.Redaction for Java
type: docs
url: /java/text-redaction/groupdocs-redaction-java-text-redaction/
weight: 1
---

# How to redact text with GroupDocs.Redaction for Java

In this tutorial you’ll learn **how to redact text** in Java‑based documents using GroupDocs.Redaction. You’ll see how to mask personal information, replace sensitive strings with safe placeholders, and process multiple files in a batch‑friendly way. By the end you’ll have a production‑ready solution that protects privacy, meets GDPR/HIPAA requirements, and integrates smoothly into existing Java applications.

## Quick answers
- **What library is used?** GroupDocs.Redaction for Java.  
- **Can I mask personal information?** Yes – use exact‑phrase redaction with replacement options.  
- **Is batch processing supported?** Absolutely, you can loop through multiple files with the same Redactor instance.  
- **Do I need a license?** A free trial works for evaluation; a commercial license is required for production.  
- **Which Java version is required?** JDK 8 or higher.

## What is “how to redact text”?

Redaction permanently removes or obscures confidential data from a document. With GroupDocs.Redaction you can locate specific strings, replace them with safe placeholders, and save the sanitized file—all without manual editing.

## Why use GroupDocs.Redaction for Java?

GroupDocs.Redaction for Java supports **50+ input and output formats** (including PDF, DOCX, XLSX, PPTX, TXT, RTF) and can process multi‑hundred‑page files without loading the entire document into memory, delivering high‑throughput batch operations on standard server hardware.

## Prerequisites
- **Java Development Kit (JDK):** Version 8 or newer.  
- **IDE:** IntelliJ IDEA, Eclipse, or any Java‑compatible editor.  
- **Maven:** For dependency management.  
- **Basic Java knowledge:** Familiarity with classes, methods, and exception handling.

## Setting up GroupDocs.Redaction for Java
To start, add the library to your Maven project.

### Maven setup
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

### Direct download
If you prefer, grab the latest JAR from [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### License acquisition
You can begin with a **Free Trial**, request a **Temporary License** for extended testing, or purchase a **Commercial License** for production use.

## How to redact text in documents with GroupDocs.Redaction

The following sections walk you through the exact steps needed to **mask personal information** and **replace sensitive text**.

### Step 1: initialize the redactor

`Redactor` is the core class that loads a document, applies redaction rules, and writes the output.  

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx", new LoadOptions());
```

### Step 2: apply exact‑phrase redaction

`ExactPhraseRedaction` searches for an exact string match, while `ReplacementOptions` defines how the matched text should be replaced.

```java
redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]"));
```
- **Parameters:**  
  - `"John Doe"` – the exact text to be redacted.  
  - `ReplacementOptions("[personal]")` – the string that will replace the original content, effectively **masking personal information**.

### Step 3: save the redacted document

`Redactor.save` writes the modified document to a new file or overwrites the original, preserving the original format.

```java
redactor.save();
```

### Step 4: clean up resources

Always call `Redactor.close()` to release native resources and avoid memory leaks.

```java
finally {
    redactor.close();
}
```

## How to mask personal information with a custom callback

A custom callback lets you react to each redaction event—useful for logging, conditional replacements, or audit trails.

### Create a callback class

`IRedactionCallback` defines methods that are invoked before and after each redaction operation.

```java
class RedactionDump implements IRedactionCallback {
    @Override
    public void onRedacted(IRedaction redaction) {
        // Custom processing or logging for each redaction event.
    }
}
```

### Use the callback when instantiating Redactor

Pass your callback implementation via `RedactorSettings` so the engine knows to invoke it during processing.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx", new LoadOptions(), new RedactorSettings(new RedactionDump()));
```

## Practical applications
- **Legal contracts:** Automatically hide client names, SSNs, or confidential clauses before sharing drafts.  
- **Medical records:** **Mask personal information** such as patient identifiers when exporting records to research partners.  
- **Corporate communications:** **Replace sensitive text** like internal project codes prior to external distribution, ensuring no accidental leaks.

## Performance considerations
When processing large or numerous files, keep these tips in mind:

- **Batch processing:** Loop through a collection of files to reduce startup overhead.  
- **Memory management:** Release the `Redactor` after each file; avoid holding many documents in memory simultaneously.  
- **Profiling:** Use Java profilers (e.g., VisualVM) to spot bottlenecks in I/O or redaction logic.

## Frequently asked questions
**Q: Can I redact text from PDFs using GroupDocs.Redaction?**  
A: Yes, the library supports PDF, DOCX, XLSX, PPTX, and many other formats.

**Q: Is a redaction reversible?**  
A: No. Redactions permanently remove the original content, so keep a backup of the source file.

**Q: How do I handle very large documents efficiently?**  
A: Process them in chunks, use batch mode, and monitor memory usage with profiling tools.

**Q: What other text formats are supported?**  
A: Besides DOCX and PDF, you can redact TXT, RTF, XLSX, PPTX, and more.

**Q: Can I integrate GroupDocs.Redaction into existing workflows?**  
A: Absolutely. The API can be called from web services, background jobs, or CI/CD pipelines.

## Resources
- **Documentation:** [GroupDocs Redaction Java Docs](https://docs.groupdocs.com/redaction/java/)  
- **API reference:** [GroupDocs API Reference for Java](https://reference.groupdocs.com/redaction/java)  
- **Download:** [GroupDocs.Redaction Downloads](https://releases.groupdocs.com/redaction/java/)  
- **GitHub repository:** [GroupDocs Redaction GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **Free support forum:** [GroupDocs Free Support](https://forum.groupdocs.com/c/redaction/33)  
- **Temporary license application:** [Apply for a Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Last Updated:** 2026-08-14  
**Tested With:** GroupDocs.Redaction 24.9 for Java  
**Author:** GroupDocs

## Related Tutorials

- [Mask Sensitive Data Java – GroupDocs.Redaction Guide](/redaction/java/getting-started/)
- [Mask Sensitive Data Java – Redact Personal Info with GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)
- [Edit Password-Protected Docs Java - Redact Documents Using GroupDocs.Redaction](/redaction/java/document-loading/groupdocs-redaction-java-password-documents/)