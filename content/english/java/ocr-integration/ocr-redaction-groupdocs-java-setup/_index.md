---
title: "Extract Text Scanned PDF – Mask Data with GroupDocs OCR"
description: "Learn how to extract text scanned PDF and mask sensitive data using GroupDocs OCR Redaction with Azure OCR. Redact social security number and replace confidential info PDF efficiently."
date: "2026-06-26"
weight: 1
url: "/java/ocr-integration/ocr-redaction-groupdocs-java-setup/"
keywords:
  - extract text scanned pdf
  - redact social security number
  - mask sensitive data pdf
  - replace confidential info pdf
type: docs
schemas:
- type: TechArticle
  headline: Extract Text Scanned PDF – Mask Data with GroupDocs OCR
  description: Learn how to extract text scanned PDF and mask sensitive data using
    GroupDocs OCR Redaction with Azure OCR. Redact social security number and replace
    confidential info PDF efficiently.
  dateModified: '2026-06-26'
  author: GroupDocs
- type: FAQPage
  questions:
  - question: What is OCR redaction?
    answer: OCR redaction uses Optical Character Recognition to extract hidden text
      from images or scanned PDFs, then applies redaction rules to mask that text.
  - question: Can I use GroupDocs Redaction without Azure OCR?
    answer: Yes, but OCR dramatically improves accuracy on scanned documents where
      native text extraction fails.
  - question: How do I handle complex regex patterns?
    answer: Build and test them incrementally, using Java’s `Pattern` class in a sandbox
      before applying to large documents.
  - question: What are typical performance bottlenecks?
    answer: Large PDFs, overly complex regex, and synchronous OCR calls can slow processing;
      consider batch processing and optimized patterns.
  - question: Is support available for implementation issues?
    answer: Absolutely—reach out via the [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33)
      for community help or contact GroupDocs support.
---

# Extract Text Scanned PDF – Mask Data with GroupDocs OCR

In today’s data‑driven world, **extracting text from scanned PDF** files and masking confidential information is a non‑negotiable compliance step. This tutorial walks you through using GroupDocs Redaction together with Microsoft Azure OCR to reliably recognize hidden text on scanned pages and replace it with a safe placeholder such as **`[REDACTED]`**. You’ll see why this combo is fast, accurate, and ready for production‑grade workloads.

## Quick Answers
- **What does “mask sensitive data” mean?** It replaces identified confidential text with a placeholder (e.g., `[REDACTED]`).  
- **Which library handles OCR?** Microsoft Azure OCR connector, used through GroupDocs Redaction.  
- **Do I need a license?** A free trial works for evaluation; a permanent license is required for production.  
- **Can I redact scanned PDFs?** Yes—OCR extracts the hidden text before applying regex redactions.  
- **Is this solution Java‑only?** The example is Java‑based, but GroupDocs provides similar APIs for .NET and other platforms.

## What is OCR‑Based Redaction?
OCR‑Based Redaction first runs OCR on each page, turning images into searchable text, then applies regex patterns to replace matches with a mask such as `[REDACTED]`. This two‑step process lets you reliably hide personal data even in scanned PDFs, ensuring that any sensitive strings are removed before the document is shared or archived.

## Why Use GroupDocs Redaction with Azure OCR?
You should use GroupDocs Redaction with Azure OCR because it delivers **>98 % OCR accuracy on printed text**, supports **50+ input and output formats**, and can process **multi‑hundred-page PDFs without loading the entire file into memory**, ensuring fast, scalable redaction for compliance. The solution also **scales to process a 1,000‑page PDF in under 2 minutes on an 8‑core server**, making batch jobs practical.

## Prerequisites
- **Java Development Kit (JDK) 8+** installed.  
- **Maven** (if you prefer dependency management) or the ability to download JARs manually.  
- **Microsoft Azure OCR credentials** (endpoint and subscription key).  
- Basic Java knowledge and familiarity with regular expressions.

## Setting Up GroupDocs Redaction for Java

### Maven Setup
Add the GroupDocs repository and dependency to your `pom.xml`:

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
If you prefer manual JAR management, grab the latest release from [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### License Acquisition
- **Free Trial** – explore all features without cost.  
- **Temporary License** – extend evaluation time.  
- **Full License** – unlock production‑ready capabilities.

### Basic Initialization and Setup
The `Redactor` class is the core engine that performs OCR extraction and applies redaction rules to PDF documents.  
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.RedactorSettings;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.examples.java.helper_classes.MicrosoftAzureOcrConnector;

// Initialize the OCR connector with Microsoft Azure
RedactorSettings settings = new RedactorSettings(new MicrosoftAzureOcrConnector());
```

## How to Mask Sensitive Data with OCR Redaction
Masking sensitive data with OCR Redaction involves loading the PDF with Azure OCR settings, defining regex patterns for the data you want to hide, and invoking the Redactor to replace each match with a placeholder like `[REDACTED]`. The library handles OCR, pattern matching, and PDF rewriting in a single workflow.

### Step 1: Load the Document with OCR Settings
`LoadOptions` configures how GroupDocs loads a file, allowing you to pass OCR connectors such as Azure.  
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;

// Load your document with OCR settings
try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf", 
    new LoadOptions(), settings)) {
    // Further operations will go here
}
```
- **`YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf`** – replace with the path to your PDF.  
- **`settings`** – contains the Azure OCR connector you created earlier.

### Step 2: Define and Apply Regex Redactions
`ReplacementOptions` specifies the replacement text that will substitute each regex match during redaction.  
```java
import com.groupdocs.redaction.redactions.RegexRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

// Define the regex for sensitive data (e.g., Social Security Numbers)
RegexRedaction redaction = new RegexRedaction("\\b\\d{3}-\\d{2}-\\d{4}\\b", 
    new ReplacementOptions("[REDACTED]"));

// Apply redaction
redactor.apply(redaction);

// Save the document after redactions
redactor.save(new SaveOptions());
```
- The pattern `\b\d{3}-\d{2}-\d{4}\b` matches U.S. Social Security Numbers.  
- `ReplacementOptions("[REDACTED]")` swaps each match with the mask, effectively **masking sensitive data**.

## Common Use Cases for Masking Sensitive Data
1. **Legal Document Management** – hide client identifiers before sharing drafts.  
2. **Financial Reporting** – protect account numbers and transaction IDs.  
3. **Healthcare Records** – comply with HIPAA by redacting patient identifiers.  
4. **Government Publications** – remove personal data from public records.  
5. **Corporate Contracts** – conceal proprietary terms during external reviews.

## Performance Tips
- **Optimize regex** – avoid overly broad patterns that increase processing time; well‑crafted expressions can cut runtime by up to 40 %.  
- **Memory Management** – close the `Redactor` instance promptly (try‑with‑resources does this automatically).  
- **Asynchronous Execution** – for bulk processing, run redaction jobs on separate threads or use a task queue to keep the UI responsive.

## Troubleshooting
- **Azure credentials error** – double‑check the endpoint URL and subscription key in `MicrosoftAzureOcrConnector`.  
- **Document not loading** – verify the file path and ensure the PDF isn’t password‑protected (or supply the password via `LoadOptions`).  
- **No redactions applied** – test your regex with a simple string first; use `Pattern.compile` in a unit test to confirm matches.

## Frequently Asked Questions

**Q: What is OCR redaction?**  
A: OCR redaction uses Optical Character Recognition to extract hidden text from images or scanned PDFs, then applies redaction rules to mask that text.

**Q: Can I use GroupDocs Redaction without Azure OCR?**  
A: Yes, but OCR dramatically improves accuracy on scanned documents where native text extraction fails.

**Q: How do I handle complex regex patterns?**  
A: Build and test them incrementally, using Java’s `Pattern` class in a sandbox before applying to large documents.

**Q: What are typical performance bottlenecks?**  
A: Large PDFs, overly complex regex, and synchronous OCR calls can slow processing; consider batch processing and optimized patterns.

**Q: Is support available for implementation issues?**  
A: Absolutely—reach out via the [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33) for community help or contact GroupDocs support.

## Additional Resources
- **Documentation**: https://docs.groupdocs.com/redaction/java/  
- **API Reference**: https://reference.groupdocs.com/redaction/java  
- **Download**: https://releases.groupdocs.com/redaction/java/  
- **GitHub**: https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java  
- **Free Support**: https://forum.groupdocs.com/c/redaction/33  
- **Temporary License**: https://purchase.groupdocs.com/temporary-license/

---

**Last Updated:** 2026-06-26  
**Tested With:** GroupDocs.Redaction 24.9 (Java)  
**Author:** GroupDocs  

---

## Related Tutorials

- [Secure PDF Redaction using OCR – GroupDocs.Redaction Java](/redaction/java/ocr-integration/)
- [How to Redact Text with GroupDocs.Redaction for Java](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction/)
- [Mask Sensitive Data Java – Redact Personal Info with GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)
