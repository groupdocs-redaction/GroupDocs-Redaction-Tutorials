---
title: "How to Redact Text with GroupDocs.Redaction for Java"
description: "Learn how to redact text in Java documents using GroupDocs.Redaction, including how to mask personal information and replace sensitive text."
date: "2026-02-26"
weight: 1
url: "/java/text-redaction/groupdocs-redaction-java-text-redaction/"
keywords:
- text redaction
- GroupDocs Redaction for Java
- sensitive information redaction
type: docs
---

# How to Redact Text in Documents Using GroupDocs.Redaction for Java

In this guide you’ll discover **how to redact text** in Java‑based documents with the help of GroupDocs.Redaction. Whether you need to **mask personal information** or **replace sensitive text** with placeholders, the steps below walk you through a complete, production‑ready solution. By the end of the tutorial you’ll be able to protect privacy, stay compliant, and automate redaction across many file formats.

## Quick Answers
- **What library is used?** GroupDocs.Redaction for Java  
- **Can I mask personal information?** Yes – use exact‑phrase redaction with replacement options.  
- **Is batch processing supported?** Absolutely, you can loop through multiple files with the same Redactor instance.  
- **Do I need a license?** A free trial works for evaluation; a commercial license is required for production.  
- **Which Java version is required?** JDK 8 or higher.

## What is “how to redact text”?
Redaction is the process of permanently removing or obscuring confidential data from a document. With GroupDocs.Redaction you can programmatically locate specific strings, replace them with safe placeholders, and save the sanitized file—all without manual editing.

## Why use GroupDocs.Redaction for Java?
- **Broad format support:** DOCX, PDF, XLSX, PPTX, and more.  
- **High performance:** Optimized for large files and batch operations.  
- **Extensible callbacks:** Hook into redaction events for logging or custom handling.  
- **Compliance‑ready:** Meets GDPR, HIPAA, and other privacy regulations.

## Prerequisites
- **Java Development Kit (JDK):** Version 8 or newer.  
- **IDE:** IntelliJ IDEA, Eclipse, or any Java‑compatible editor.  
- **Maven:** For dependency management.  
- **Basic Java knowledge:** Familiarity with classes, methods, and exception handling.

## Setting Up GroupDocs.Redaction for Java
To start, add the library to your Maven project.

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
If you prefer, grab the latest JAR from [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### License Acquisition
You can start with a **Free Trial**, request a **Temporary License** for extended testing, or purchase a **Commercial License** for production use.

## How to Redact Text in Documents with GroupDocs.Redaction
The following sections walk you through the exact steps needed to **mask personal information** and **replace sensitive text**.

### Step 1: Initialize the Redactor
Create a `Redactor` instance pointing to the document you want to process.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx", new LoadOptions());
```

### Step 2: Apply Exact‑Phrase Redaction
Use `ExactPhraseRedaction` to locate a phrase such as “John Doe” and replace it with a safe placeholder.

```java
redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]"));
```
- **Parameters:**  
  - `"John Doe"` – the exact text to be redacted.  
  - `ReplacementOptions("[personal]")` – the string that will replace the original content, effectively **masking personal information**.

### Step 3: Save the Redacted Document
Persist the changes to a new file or overwrite the original.

```java
redactor.save();
```

### Step 4: Clean Up Resources
Always close the `Redactor` to free native resources.

```java
finally {
    redactor.close();
}
```

## How to Mask Personal Information with a Custom Callback
Sometimes you need more control over what happens when a redaction occurs (e.g., logging, conditional replacement).

### Create a Callback Class
Implement `IRedactionCallback` to receive redaction events.

```java
class RedactionDump implements IRedactionCallback {
    @Override
    public void onRedacted(IRedaction redaction) {
        // Custom processing or logging for each redaction event.
    }
}
```

### Use the Callback When Instantiating Redactor
Pass the callback via `RedactorSettings`.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx", new LoadOptions(), new RedactorSettings(new RedactionDump()));
```

## Practical Applications
- **Legal contracts:** Automatically hide client names, SSNs, or confidential clauses.  
- **Medical records:** **Mask personal information** such as patient identifiers before sharing with third parties.  
- **Corporate communications:** **Replace sensitive text** like internal project codes prior to external distribution.

## Performance Considerations
When processing large or numerous files, keep these tips in mind:

- **Batch processing:** Loop through a collection of files to reduce startup overhead.  
- **Memory management:** Release the `Redactor` after each file; avoid holding many documents in memory simultaneously.  
- **Profiling:** Use Java profilers (e.g., VisualVM) to spot bottlenecks in I/O or redaction logic.

## Frequently Asked Questions
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
- **API Reference:** [GroupDocs API Reference for Java](https://reference.groupdocs.com/redaction/java)  
- **Download:** [GroupDocs.Redaction Downloads](https://releases.groupdocs.com/redaction/java/)  
- **GitHub Repository:** [GroupDocs Redaction GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **Free Support Forum:** [GroupDocs Free Support](https://forum.groupdocs.com/c/redaction/33)  
- **Temporary License Application:** [Apply for a Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Last Updated:** 2026-02-26  
**Tested With:** GroupDocs.Redaction 24.9 for Java  
**Author:** GroupDocs