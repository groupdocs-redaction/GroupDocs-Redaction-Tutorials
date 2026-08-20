---
date: '2026-08-20'
description: Discover how to redact text using regex in Java with GroupDocs.Redaction.
  This step‑by‑step tutorial shows you how to apply regex, configure save options,
  and protect sensitive data.
images:
- /java/text-redaction/master-text-redaction-java-groupdocs-redaction-guide/og-image.png
keywords:
- how to redact text
- mask credit card numbers
- remove social security numbers
- redact pdf java
lastmod: '2026-08-20'
og_description: Learn how to redact text in Java using GroupDocs.Redaction. This guide
  explains regex redaction, save‑option configuration, and performance tips for protecting
  sensitive data.
og_image_alt: Guide showing Java code to redact text using GroupDocs.Redaction
og_title: How to redact text in Java with GroupDocs.Redaction
schemas:
- author: GroupDocs
  dateModified: '2026-08-20'
  description: Discover how to redact text using regex in Java with GroupDocs.Redaction.
    This step‑by‑step tutorial shows you how to apply regex, configure save options,
    and protect sensitive data.
  headline: 'How to redact text in Java with GroupDocs.Redaction: A complete guide'
  type: TechArticle
- description: Discover how to redact text using regex in Java with GroupDocs.Redaction.
    This step‑by‑step tutorial shows you how to apply regex, configure save options,
    and protect sensitive data.
  name: 'How to redact text in Java with GroupDocs.Redaction: A complete guide'
  steps:
  - name: import required classes
    text: 'The following imports give you access to the redaction API:'
  - name: initialize redactor and apply regex pattern
    text: '`RegexRedaction` represents a redaction rule based on a regular‑expression
      pattern. The pattern you provide determines which text fragments are replaced.
      - **Regex explanation**: The pattern `\b\d{3}-\d{2}-\d{4}\b` matches U.S. Social
      Security numbers (three digits, a dash, two digits, a dash, four '
  - name: configure save options
    text: '`SaveOptions` controls how the redacted file is written. Adding a suffix
      makes it clear which files have been processed, while preserving the original
      format avoids unwanted conversion. - **Save options**: `setAddSuffix(true)`
      automatically appends “_redacted” to the output filename, preventing acci'
  - name: customize additional save settings
    text: 'You can further tailor the output—such as preserving metadata or flattening
      annotations—by adjusting the `SaveOptions` object. - **Key configuration**:
      Setting `setPreserveMetadata(true)` retains original document properties, which
      is often required for compliance audits.'
  type: HowTo
- questions:
  - answer: It automatically appends a suffix (e.g., `_redacted`) to the output filename,
      making it obvious which files have been processed.
    question: What is the purpose of `setAddSuffix(true)` in SaveOptions?
  - answer: Absolutely. Any valid Java regular expression can be supplied to `RegexRedaction`
      to target emails, phone numbers, custom IDs, etc.
    question: Can I use regex patterns other than numbers for text redaction?
  - answer: Wrap the redaction logic in a try‑catch block, log the exception, and
      always close the `Redactor` in a finally clause to release resources.
    question: How should I handle errors during redaction?
  - answer: Yes. GroupDocs.Redaction works with PDF, DOCX, PPTX, and many other formats.
    question: Is PDF redaction supported?
  - answer: Use batch processing, keep regex patterns simple, and monitor memory usage
      with profiling tools.
    question: What are best practices for large‑scale redaction projects?
  type: FAQPage
tags:
- text redaction
- GroupDocs.Redaction
- Java document processing
- regex redaction
- PDF redaction
title: 'How to redact text in Java with GroupDocs.Redaction: A complete guide'
type: docs
url: /java/text-redaction/master-text-redaction-java-groupdocs-redaction-guide/
weight: 1
---

# How to redact text in Java with GroupDocs.Redaction: A complete guide

In today’s fast‑moving digital world, **how to redact text** in documents is a question many developers face. Whether you’re protecting personal data, complying with regulations, or simply cleaning up drafts, this guide walks you through using GroupDocs.Redaction for Java to **apply regex‑based redaction quickly and safely**. You’ll learn why redaction matters, how to configure the library, and best‑practice tips for high‑performance processing.

## Quick answers
- **What is the primary purpose of GroupDocs.Redaction?** It provides a reliable API to locate and mask sensitive text in more than 50 document formats.  
- **How do I apply regex for redaction?** Create a `RegexRedaction` object with your pattern and pass it to the `Redactor.apply()` method.  
- **Do I need a license?** A free trial works for development; a paid license unlocks full features for production.  
- **Can I redact PDFs as well as DOCX files?** Yes—GroupDocs.Redaction supports PDF, DOCX, PPTX, and many other formats.  
- **What’s the best way to improve performance?** Close `Redactor` instances promptly, keep regex patterns simple, and process files in batches.

## What is text redaction and why does it matter?
Text redaction permanently removes or obscures sensitive information from a document, ensuring that confidential data—such as social security numbers, credit‑card details, or medical records—cannot be recovered or viewed by unauthorized parties. It works by overwriting the original characters or replacing them with a mask, so the hidden content cannot be extracted by copy‑paste or OCR tools. This ensures compliance with privacy regulations and protects individuals from identity theft or data breaches.

## Why use regex for text redaction?
Regular expressions let you define flexible patterns that match a wide range of data formats (e.g., phone numbers, credit‑card numbers). Using regex with GroupDocs.Redaction gives you precise control over what gets hidden, while keeping the implementation concise and maintainable.

## Prerequisites
Before we dive in, make sure you have:

- **Java Development Kit (JDK)** installed (Java 8 or newer).  
- Basic familiarity with Java syntax and regular expressions.  
- An IDE such as **IntelliJ IDEA** or **Eclipse** to run and debug the code.  

## Setting up GroupDocs.Redaction for Java
First, add the library to your project.

### Maven setup
If you use Maven, insert the following into your `pom.xml`:

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
Alternatively, download the latest JAR from [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### Basic initialization
`Redactor` is the core class that opens a document, applies redaction rules, and writes the output.

Once the library is available, you can start redacting documents:

```java
// Import the necessary classes from GroupDocs.Redaction
import com.groupdocs.redaction.Redactor;

public class RedactionExample {
    public static void main(String[] args) {
        // Initialize the redactor with your document path
        final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
        // Ensure you close resources after operations
        try { /* Your code here */ } finally { redactor.close(); }
    }
}
```

## How to redact text using regex in Java?
The process involves loading the source file into a `Redactor` instance, creating a `RegexRedaction` rule that defines the pattern to match, applying the rule with `redactor.apply()`, and finally saving the modified document using `SaveOptions`. By following these steps you can reliably locate and mask any sensitive strings across supported formats.

The `Redactor` class is the core component that opens a document, applies redaction rules, and writes the output file. It manages resources internally, so you must close it after processing to free memory.

### Step 1: import required classes
The following imports give you access to the redaction API:

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.redactions.RegexRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;
```

### Step 2: initialize redactor and apply regex pattern
`RegexRedaction` represents a redaction rule based on a regular‑expression pattern. The pattern you provide determines which text fragments are replaced.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
try {
    // Define a regex pattern to find sequences of numbers and apply a replacement color.
    // The pattern: Two digits, optional whitespace, two more digits, non-digit characters,
    // followed by six digits.
    redactor.apply(new RegexRedaction("\\d{2}\\s*\\d{2}[^\\d]*\\d{6}", 
        new ReplacementOptions(java.awt.Color.BLUE)));
```

- **Regex explanation**: The pattern `\b\d{3}-\d{2}-\d{4}\b` matches U.S. Social Security numbers (three digits, a dash, two digits, a dash, four digits). `ReplacementOptions` lets you choose a solid black overlay or a custom text mask.

### Step 3: configure save options
`SaveOptions` controls how the redacted file is written. Adding a suffix makes it clear which files have been processed, while preserving the original format avoids unwanted conversion.

```java
    // Configure save options
    SaveOptions saveOptions = new SaveOptions();
    saveOptions.setAddSuffix(true);  // Adds suffix to indicate processing
    saveOptions.setRasterizeToPDF(false);  // Preserves original format

    // Save the redacted document
    redactor.save(saveOptions);
} finally {
    redactor.close();  // Always close resources to prevent memory leaks
}
```

- **Save options**: `setAddSuffix(true)` automatically appends “_redacted” to the output filename, preventing accidental overwrites.

### Step 4: customize additional save settings
You can further tailor the output—such as preserving metadata or flattening annotations—by adjusting the `SaveOptions` object.

```java
import com.groupdocs.redaction.options.SaveOptions;

SaveOptions saveOptions = new SaveOptions();
saveOptions.setAddSuffix(true);  // Indicates processing by adding a suffix
saveOptions.setRasterizeToPDF(false);  // Keeps original format intact
```

- **Key configuration**: Setting `setPreserveMetadata(true)` retains original document properties, which is often required for compliance audits.

## Practical applications
Real‑world scenarios where **how to redact text** is essential:

1. **Legal documents** – Hide client identifiers before sharing drafts with external counsel.  
2. **Medical records** – Mask patient names, IDs, or health numbers to stay HIPAA‑compliant.  
3. **Financial reports** – Remove confidential account numbers when distributing quarterly summaries.  

## Performance considerations
- **Memory management**: Always call `redactor.close()` to release file handles and native resources.  
- **Efficient regex**: Simpler patterns run faster; avoid excessive back‑tracking by using atomic groups when possible.  
- **Batch processing**: For large document sets, process files in batches of 20–50 to keep heap usage predictable.

## Common issues and solutions
| Issue | Solution |
|-------|----------|
| **Regex matches too much** | Test your pattern with an online regex tester and narrow the character classes. |
| **Output file name conflict** | Use `setAddSuffix(true)` or provide a custom output path via `saveOptions.setOutputPath()`. |
| **Memory leak on large PDFs** | Process PDFs page‑by‑page or increase JVM heap size (`-Xmx2g`). |

## Frequently asked questions

**Q: What is the purpose of `setAddSuffix(true)` in SaveOptions?**  
A: It automatically appends a suffix (e.g., `_redacted`) to the output filename, making it obvious which files have been processed.

**Q: Can I use regex patterns other than numbers for text redaction?**  
A: Absolutely. Any valid Java regular expression can be supplied to `RegexRedaction` to target emails, phone numbers, custom IDs, etc.

**Q: How should I handle errors during redaction?**  
A: Wrap the redaction logic in a try‑catch block, log the exception, and always close the `Redactor` in a finally clause to release resources.

**Q: Is PDF redaction supported?**  
A: Yes. GroupDocs.Redaction works with PDF, DOCX, PPTX, and many other formats.

**Q: What are best practices for large‑scale redaction projects?**  
A: Use batch processing, keep regex patterns simple, and monitor memory usage with profiling tools.

## Additional resources
- **Documentation**: [GroupDocs Redaction Documentation](https://docs.groupdocs.com/redaction/java/)  
- **API reference**: [GroupDocs API Reference](https://apireference.groupdocs.com/redaction/java)

---

**Last Updated:** 2026-08-20  
**Tested With:** GroupDocs.Redaction 24.9 for Java  
**Author:** GroupDocs

## Related Tutorials

- [Mask Sensitive Data Java – GroupDocs.Redaction Guide](/redaction/java/getting-started/)
- [Mask Sensitive Data Java – Redact Personal Info with GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)
- [How to Redact PDF with Aspose OCR and Java - Implementing Regex Patterns using GroupDocs.Redaction](/redaction/java/ocr-integration/aspose-ocr-java-pdf-redaction/)