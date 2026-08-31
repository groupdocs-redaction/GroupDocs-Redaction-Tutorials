---
date: '2026-08-31'
description: Learn how to redact PDF using GroupDocs.Redaction for Java, create redaction
  policies, remove annotations, and erase metadata in a programmatic, compliant way.
images:
- /java/advanced-redaction/master-redaction-groupdocs-java-guide/og-image.png
keywords:
- how to redact pdf
- erase metadata pdf
- remove annotations java
- GroupDocs.Redaction Java
- document redaction
lastmod: '2026-08-31'
og_description: How to redact PDF using GroupDocs.Redaction for Java. Create policies,
  remove annotations, and erase metadata quickly and securely.
og_image_alt: Guide showing how to redact PDF files with GroupDocs.Redaction in Java
og_title: How to redact PDF with GroupDocs.Redaction for Java
schemas:
- author: GroupDocs
  dateModified: '2026-08-31'
  description: Learn how to redact PDF using GroupDocs.Redaction for Java, create
    redaction policies, remove annotations, and erase metadata in a programmatic,
    compliant way.
  headline: How to redact PDF with GroupDocs.Redaction for Java
  type: TechArticle
- description: Learn how to redact PDF using GroupDocs.Redaction for Java, create
    redaction policies, remove annotations, and erase metadata in a programmatic,
    compliant way.
  name: How to redact PDF with GroupDocs.Redaction for Java
  steps:
  - name: configure redactions
    text: 'Configure the redactions using different classes provided by GroupDocs.Redaction:'
  - name: save redaction policy
    text: 'Save the configured policy as an XML file:'
  - name: create exact phrase redaction
    text: 'Implement an exact phrase redaction:'
  - name: create regex redaction
    text: 'Define a regex‑based redaction:'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction is a Java library that programmatically removes or
      replaces sensitive content in PDFs and other document formats.
    question: What is GroupDocs.Redaction?
  - answer: Add the Maven dependency, obtain a trial license, and follow the initialization
      steps shown above.
    question: How do I get started with GroupDocs.Redaction?
  - answer: Yes—use exact‑phrase redactions, regular‑expression redactions, or the
      built‑in metadata removal classes.
    question: Can I customize redaction patterns in GroupDocs.Redaction?
  - answer: Absolutely—save your `RedactionPolicy` as an XML file and load it later
      for batch processing.
    question: Is it possible to save and reuse redaction configurations?
  - answer: Apply only required redactions, tune Java heap size, and craft efficient
      regex patterns to minimise CPU usage.
    question: What are the best practices for optimizing performance with GroupDocs.Redaction?
  type: FAQPage
tags:
- redact PDF
- GroupDocs.Redaction
- Java document processing
- erase metadata pdf
- remove annotations java
title: How to redact PDF with GroupDocs.Redaction for Java
type: docs
url: /java/advanced-redaction/master-redaction-groupdocs-java-guide/
weight: 1
---

# How to redact PDF with GroupDocs.Redaction for Java

In today’s data‑driven world, protecting confidential information inside PDF files is a non‑negotiable requirement. This tutorial shows **how to redact PDF** documents programmatically with GroupDocs.Redaction for Java, covering policy creation, annotation removal, and metadata erasure. You’ll walk away with a reusable XML redaction policy that can be applied to any number of PDFs, keeping you compliant with GDPR, HIPAA, and other regulations.

## Quick answers
- **What is the primary purpose of GroupDocs.Redaction?** To programmatically redact sensitive content from PDFs and other document formats.  
- **Can I remove annotations with Java?** Yes—use the `DeleteAnnotationRedaction` class (remove annotations java).  
- **Do I need a license for development?** A free trial or temporary license works for testing; a full license is required for production.  
- **Which Java version is supported?** JDK 8 or later.  
- **Where can I find the XML policy file?** You define the output path in your code and call `policy.save(...)`.

The `DeleteAnnotationRedaction` class removes annotation objects such as comments, highlights, or stamps from a PDF.  
The `RedactionPolicy` class represents a collection of redaction rules that can be saved to or loaded from an XML file.

## What is a redaction policy and how to create redaction policy?
A redaction policy is an XML‑based set of rules that tells GroupDocs.Redaction exactly which text, patterns, annotations, or metadata to hide, delete, or replace in a PDF. By defining the policy once and saving it as an XML file, you can apply the same **redact sensitive info** across multiple PDFs without rewriting code.

## Why use GroupDocs.Redaction for Java?
GroupDocs.Redaction processes PDFs with a **memory‑efficient engine** that can handle files exceeding 500 pages while using less than 150 MB of RAM. It supports **30+ input and output formats**, including DOCX, XLSX, PPTX, HTML, and common image types, and offers built‑in compliance features for GDPR and HIPAA. The library also provides fine‑grained control over exact‑phrase, regex, annotation, and metadata redactions, making it the most versatile solution for Java developers.

## Prerequisites
- **Libraries and dependencies** – Add GroupDocs.Redaction to your project via Maven or download the JAR directly.  
- **Java environment** – JDK 8 or newer installed and configured.  
- **Basic knowledge** – Familiarity with Java syntax and regular expressions will speed up policy creation.

## Setting up GroupDocs.Redaction for Java

### Installation information
**Maven:**  
To integrate GroupDocs.Redaction using Maven, add the following to your `pom.xml`:

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

**Direct download:**  
Alternatively, download the latest version from [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### License acquisition
Start with a free trial or obtain a temporary license to explore all features. For long‑term use, purchase a full license.

**Basic initialization:**  
To initialize GroupDocs.Redaction in your project:

```java
import com.groupdocs.redaction.Redactor;

public class RedactionSetup {
    public static void main(String[] args) {
        // Initialize the Redactor object with your document path
        try (Redactor redactor = new Redactor("path/to/your/document.pdf")) {
            // Perform operations here
        }
    }
}
```

## Implementation guide

### How to create redaction policy: create and save redaction policy
Load your redaction configuration, add the desired redaction objects, and persist the policy as an XML file. This two‑step process lets you reuse the same rules across many PDFs without rebuilding the policy each time.

#### Overview
This feature allows you to configure multiple types of redactions, such as exact phrase, regex, and metadata erasures. You can then save these configurations as an XML file for future use.

##### Step 1: configure redactions
Configure the redactions using different classes provided by GroupDocs.Redaction:

```java
import com.groupdocs.redaction.RedactionPolicy;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
import com.groupdocs.redaction.redactions.RegexRedaction;
import com.groupdocs.redaction.redactions.DeleteAnnotationRedaction;
import com.groupdocs.redaction.redactions.EraseMetadataRedaction;
import com.groupdocs.redaction.options.ReplacementOptions;
import java.awt.Color;

// Configure redactions
RedactionPolicy policy = new RedactionPolicy(new Redaction[] {
    // Exact Phrase Redaction replaces "Redaction" with "[Product]"
    new ExactPhraseRedaction("Redaction", new ReplacementOptions("[Product]")),
    
    // Regex Redaction searches for specific patterns and replaces them with a blue rectangle
    new RegexRedaction("\\d{2}\\s*\\d{2}[^\\d]*\\d{6}", new ReplacementOptions(Color.BLUE)),
    
    // Delete Annotation Redaction removes all annotations
    new DeleteAnnotationRedaction(),
    
    // Erase Metadata Redaction deletes all metadata
    new EraseMetadataRedaction(MetadataFilters.All)
});
```

##### Step 2: save redaction policy
Save the configured policy as an XML file:

```java
// Define your output directory path
String outputPath = YOUR_DOCUMENT_DIRECTORY + "YOUR_OUTPUT_DIRECTORY/POLICY_SAVE.xml";
policy.save(outputPath);
```

### How to remove annotations java: configure exact phrase redaction
Load a PDF, define the exact phrase you want to hide, and attach the redaction to the policy. The phrase will be replaced with a black box or custom text.

#### Overview
This feature targets specific phrases for redaction, replacing them with a predefined text.

##### Step 1: create exact phrase redaction
Implement an exact phrase redaction:

```java
import com.groupdocs.redaction.Redaction;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
import com.groupdocs.redaction.options.ReplacementOptions;

// Configure the redaction for a specific phrase
Redaction exactPhraseRedaction = new ExactPhraseRedaction(
    "Redaction", // Phrase to be redacted
    new ReplacementOptions("[Product]") // Replacement text
);
```

### How to remove annotations java: configure regex redaction
Use regular expressions to locate patterns such such as social‑security numbers or credit‑card formats, then replace or delete them automatically.

#### Overview
Use regular expressions to identify and replace patterns in your documents.

##### Step 1: create regex redaction
Define a regex‑based redaction:

```java
import com.groupdocs.redaction.Redaction;
import com.groupdocs.redaction.redactions.RegexRedaction;
import com.groupdocs.redaction.options.ReplacementOptions;
import java.awt.Color;

// Implement regex redaction for pattern matching
Redaction regexRedaction = new RegexRedaction(
    "\\d{2}\\s*\\d{2}[^\\d]*\\d{6}", // Pattern to match
    new ReplacementOptions(Color.BLUE) // Replace matches with blue rectangle
);
```

## Practical applications
1. **Confidential document management** – Automatically **redact sensitive info** such as names, social security numbers, or financial data in legal and HR documents.  
2. **Compliance automation** – Meet GDPR, HIPAA, and other regulatory mandates by stripping personal identifiers from customer communications.  
3. **Data anonymization for testing** – Apply regex‑based redactions to anonymize test datasets while preserving document structure.

## Performance considerations
- **Optimize redaction** – Apply only the redactions you need to keep processing time low.  
- **Memory management** – Monitor Java heap usage; GroupDocs.Redaction streams pages instead of loading the whole file into memory.  
- **Efficient regex patterns** – Write concise regular expressions to avoid excessive backtracking and CPU load.

## Common issues and solutions

| Issue | Cause | Fix |
|-------|-------|-----|
| Redaction not applied | Wrong phrase or case sensitivity | Use case‑insensitive options or verify the exact text string |
| Annotations remain | `DeleteAnnotationRedaction` not added to policy | Add `new DeleteAnnotationRedaction()` to the policy array |
| Slow processing on large PDFs | Unnecessary regex scans | Limit regex scope or pre‑filter pages before applying the pattern |

## Frequently asked questions

**Q: What is GroupDocs.Redaction?**  
A: GroupDocs.Redaction is a Java library that programmatically removes or replaces sensitive content in PDFs and other document formats.

**Q: How do I get started with GroupDocs.Redaction?**  
A: Add the Maven dependency, obtain a trial license, and follow the initialization steps shown above.

**Q: Can I customize redaction patterns in GroupDocs.Redaction?**  
A: Yes—use exact‑phrase redactions, regular‑expression redactions, or the built‑in metadata removal classes.

**Q: Is it possible to save and reuse redaction configurations?**  
A: Absolutely—save your `RedactionPolicy` as an XML file and load it later for batch processing.

**Q: What are the best practices for optimizing performance with GroupDocs.Redaction?**  
A: Apply only required redactions, tune Java heap size, and craft efficient regex patterns to minimise CPU usage.

## Resources
- [Documentation](https://docs.groupdocs.com/redaction/java/)
- [API reference](https://reference.groupdocs.com/redaction/java)
- [Download](https://releases.groupdocs.com/redaction/java/)
- [GitHub repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
- [Free support forum](https://forum.groupdocs.com/c/redaction/33)
- [Temporary license](https://purchase.groupdocs.com/temporary-license/)

---

**Last updated:** 2026-08-31  
**Tested with:** GroupDocs.Redaction 24.9 for Java  
**Author:** GroupDocs

## Related Tutorials

- [How to Remove Annotations with GroupDocs.Redaction Java](/redaction/java/annotation-redaction/)
- [How to Redact Metadata Java with GroupDocs.Redaction](/redaction/java/metadata-redaction/)
- [how redact pdf java – PDF-Specific Redaction Tutorials for GroupDocs.Redaction](/redaction/java/pdf-specific-redaction/)