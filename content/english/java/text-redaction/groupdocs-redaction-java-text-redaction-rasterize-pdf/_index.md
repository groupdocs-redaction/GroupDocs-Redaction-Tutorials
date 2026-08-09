---
date: '2026-08-09'
description: Learn how to create non editable PDF files by redacting text and rasterizing
  PDFs using GroupDocs.Redaction for Java.
images:
- /java/text-redaction/groupdocs-redaction-java-text-redaction-rasterize-pdf/og-image.png
keywords:
- create non editable pdf
- how to redact text java
- GroupDocs.Redaction Java
- rasterized PDF Java
- document security Java
lastmod: '2026-08-09'
og_description: Create non editable PDF files by redacting text and rasterizing PDFs
  using GroupDocs.Redaction for Java. Follow a step‑by‑step guide with tips, pitfalls,
  and FAQs.
og_image_alt: Guide showing how to redact text and generate a non‑editable rasterized
  PDF using GroupDocs.Redaction for Java
og_title: Create non editable PDF with GroupDocs.Redaction Java
schemas:
- author: GroupDocs
  dateModified: '2026-08-09'
  description: Learn how to create non editable PDF files by redacting text and rasterizing
    PDFs using GroupDocs.Redaction for Java.
  headline: How to create non editable PDF with GroupDocs.Redaction Java
  type: TechArticle
- description: Learn how to create non editable PDF files by redacting text and rasterizing
    PDFs using GroupDocs.Redaction for Java.
  name: How to create non editable PDF with GroupDocs.Redaction Java
  steps:
  - name: Import the required classes
    text: '`ExactPhraseRedaction` is a redaction rule that targets a literal string.
      `ReplacementOptions` tells the engine what placeholder to insert instead of
      the original text.'
  - name: Apply exact phrase redaction
    text: 'The following snippet replaces every occurrence of **“John Doe”** with
      the placeholder **[personal]**: **Why this works:** - `ExactPhraseRedaction`
      targets the literal string “John Doe”. - `ReplacementOptions` tells the engine
      what to insert instead of the original text. **Tips & common pitfalls** -'
  - name: Import `SaveOptions`
    text: '`SaveOptions` configures how the document is saved, including rasterization
      and file‑naming options.'
  - name: Configure and save the rasterized PDF
    text: The snippet below disables the automatic “_redacted” suffix, enables rasterization,
      and writes the output file. **Explanation:** - `setAddSuffix(false)` keeps the
      original file name (you can enable it to add “_redacted”). - `setRasterizeToPDF(true)`
      tells GroupDocs to render each page as an image in
  type: HowTo
- questions:
  - answer: It replaces a specific string (e.g., a name) with a placeholder, ensuring
      the original text cannot be recovered.
    question: What is an exact phrase redaction?
  - answer: Rasterized PDFs render each page as an image, preventing text selection,
      copying, or editing.
    question: How does rasterizing a PDF improve security?
  - answer: Yes—loop over a list of file paths, reusing the same `Redactor` configuration
      for each document.
    question: Can I process multiple files in one run?
  - answer: Absolutely. You can read/write streams from AWS S3, Azure Blob, or Google
      Cloud Storage and feed them directly to the API.
    question: Is cloud integration possible?
  - answer: Forgetting to close the `Redactor` (which locks files) and using an outdated
      library version that lacks rasterization support.
    question: What are typical pitfalls for newcomers?
  type: FAQPage
tags:
- create non editable pdf
- GroupDocs.Redaction
- Java document redaction
- rasterized PDF
- compliance
title: How to create non editable PDF with GroupDocs.Redaction Java
type: docs
url: /java/text-redaction/groupdocs-redaction-java-text-redaction-rasterize-pdf/
weight: 1
---

# How to create non editable PDF with GroupDocs.Redaction Java

In many regulated industries you must deliver documents that cannot be altered or copied. The most reliable way to guarantee this is to **create non editable PDF** files by redacting sensitive text first and then rasterizing the entire document. GroupDocs.Redaction for Java gives you a single‑line API to perform both steps, so you can meet compliance requirements without building a custom PDF engine.

## Quick answers
- **What does “redact text” mean?** It permanently removes or masks sensitive strings so they cannot be read or recovered.  
- **Which library handles the job?** GroupDocs.Redaction for Java provides built‑in redaction and rasterization features.  
- **Do I need a license?** A free trial works for testing; a permanent license is required for production.  
- **Can I convert DOCX to a rasterized PDF in one step?** Yes – apply redaction first, then use `SaveOptions` with rasterization enabled.  
- **Is the output truly non‑editable?** Rasterized PDFs are rendered as images, preventing text extraction or modification.

## What is text redaction?
Text redaction permanently removes or obscures confidential information—such as personal identifiers, financial data, or legal clauses—from a document. Unlike a simple find‑replace, redaction guarantees that the hidden content cannot be recovered by any tool. By erasing the original characters and optionally replacing them with a placeholder, redaction ensures that the sensitive data is unrecoverable and the document remains readable for authorized users.

## Why use GroupDocs.Redaction for Java?
GroupDocs.Redaction for Java offers a comprehensive set of features that simplify secure document processing. It supports a wide range of file formats, provides multiple redaction types, and includes one‑click rasterization to lock down PDFs. The library is optimized for performance, works on both Windows and Linux, and integrates easily with existing Java applications, making it a reliable choice for enterprises that need to protect sensitive information at scale.

## Prerequisites
- Java Development Kit (JDK 11 or newer) and an IDE such as IntelliJ IDEA or Eclipse.  
- GroupDocs.Redaction library (version 24.9 or later).  
- Basic Java knowledge—you’ll write only a few short snippets.

## Setting up GroupDocs.Redaction for Java

### Maven installation
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

### Direct download
If Maven isn’t your thing, you can grab the JAR from the official release page: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

#### License acquisition
- **Free trial** – explore the API without a cost.  
- **Temporary license** – ideal for extended testing.  
- **Full license** – required for production deployments.

## Basic initialization
`Redactor` is GroupDocs.Redaction's core class that loads and modifies a document in memory. After you import the namespace, instantiate the `Redactor` with the path to your source file, then you’re ready to apply redaction rules.

```java
import com.groupdocs.redaction.Redactor;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

## Implementation guide

## How to create non editable PDF in Java?
Load the source document, apply the desired redaction rules, and then save the result with rasterization enabled. This three‑step flow—load, redact, rasterize—produces a PDF that cannot be edited, copied, or searched, satisfying the strictest compliance standards. By converting each page to an image, the final file eliminates any hidden text layers that could be extracted later.

## How to redact text in Java
Below we walk through an exact‑phrase redaction, which is perfect for removing known identifiers such as a person’s name. The process involves importing the necessary classes, defining a redaction rule, and applying it to the document before saving.

### Step 1: Import the required classes
`ExactPhraseRedaction` is a redaction rule that targets a literal string. `ReplacementOptions` tells the engine what placeholder to insert instead of the original text.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;
```

### Step 2: Apply exact phrase redaction
The following snippet replaces every occurrence of **“John Doe”** with the placeholder **[personal]**:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
try {
    redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]"));
} finally { 
    redactor.close(); 
}
```

**Why this works:**  
- `ExactPhraseRedaction` targets the literal string “John Doe”.  
- `ReplacementOptions` tells the engine what to insert instead of the original text.

**Tips & common pitfalls**  
- Double‑check the document path; a wrong path triggers a `FileNotFoundException`.  
- Ensure the Java process has write permission for the output folder.

## How to save as rasterized PDF
After redaction, you’ll likely want a non‑editable PDF. Rasterization converts every page into an image, removing the ability to select or edit text. This step ensures that the final PDF behaves like a scanned document, making it resistant to text extraction tools and accidental modifications.

### Step 1: Import `SaveOptions`
`SaveOptions` configures how the document is saved, including rasterization and file‑naming options.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
```

### Step 2: Configure and save the rasterized PDF
The snippet below disables the automatic “_redacted” suffix, enables rasterization, and writes the output file.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
try {
    SaveOptions tmp0 = new SaveOptions();
    tmp0.setAddSuffix(false);
    tmp0.setRasterizeToPDF(true);

    redactor.save(tmp0);
} finally { 
    redactor.close(); 
}
```

**Explanation:**  
- `setAddSuffix(false)` keeps the original file name (you can enable it to add “_redacted”).  
- `setRasterizeToPDF(true)` tells GroupDocs to render each page as an image inside a PDF, guaranteeing the document is **non‑editable**.

**Troubleshooting**  
- If rasterization fails, verify that the Java runtime includes the PDF rendering dependencies (they’re bundled with the library).

## Practical applications
1. **Legal document processing** – redact client names before sharing with opposing counsel.  
2. **HR record management** – hide employee IDs in internal reports.  
3. **Financial reporting** – protect account numbers when distributing audit summaries.  

You can chain these steps into an automated workflow, linking GroupDocs.Redaction with a document management system or a cloud storage bucket.

## Performance considerations
- **Batch processing:** Reuse a single `Redactor` instance when handling many files to reduce overhead by up to 40 %.  
- **Memory management:** For large documents, call `System.gc()` after each `redactor.close()` or run the process in a separate JVM.  
- **Keep dependencies updated:** New releases often contain performance tweaks for PDF rasterization, including a 20 % speed boost for multi‑core systems.

## Common issues and solutions
| Issue | Solution |
|-------|----------|
| *File not found* | Verify the absolute path and ensure the file exists on the server. |
| *Permission denied* | Run the JVM with sufficient OS permissions or change the output folder’s ACLs. |
| *Rasterization produces blank pages* | Confirm that the source document isn’t already a raster image; use the latest library version. |
| *Redaction leaves hidden text* | Use `ExactPhraseRedaction` with `ReplacementOptions`; avoid simple find‑replace methods. |

## Frequently asked questions

**Q: What is an exact phrase redaction?**  
A: It replaces a specific string (e.g., a name) with a placeholder, ensuring the original text cannot be recovered.

**Q: How does rasterizing a PDF improve security?**  
A: Rasterized PDFs render each page as an image, preventing text selection, copying, or editing.

**Q: Can I process multiple files in one run?**  
A: Yes—loop over a list of file paths, reusing the same `Redactor` configuration for each document.

**Q: Is cloud integration possible?**  
A: Absolutely. You can read/write streams from AWS S3, Azure Blob, or Google Cloud Storage and feed them directly to the API.

**Q: What are typical pitfalls for newcomers?**  
A: Forgetting to close the `Redactor` (which locks files) and using an outdated library version that lacks rasterization support.

## Resources
- **Documentation:** [GroupDocs Redaction Java Documentation](https://docs.groupdocs.com/redaction/java/)  
- **API reference:** [GroupDocs Redaction API Reference](https://reference.groupdocs.com/redaction/java)  
- **Download:** [Latest Releases](https://releases.groupdocs.com/redaction/java/)  
- **GitHub:** [GroupDocs.Redaction GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **Free support:** [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)  
- **Temporary license:** [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Last Updated:** 2026-08-09  
**Tested With:** GroupDocs.Redaction 24.9 for Java  
**Author:** GroupDocs  

---

## Related Tutorials

- [How to create grayscale pdf with GroupDocs.Redaction Java – Secure and Optimize Your Documents](/redaction/java/rasterization-options/grayscale-rasterization-groupdocs-redaction-java/)
- [Mastering Document Security in Java: Exact Phrase Redaction and Advanced Rasterization with GroupDocs.Redaction](/redaction/java/advanced-redaction/groupdocs-redaction-java-document-security/)
- [How to Convert DOCX to Image & Redact Word Documents Using GroupDocs Redaction Java](/redaction/java/document-saving/groupdocs-redaction-java-rasterize-word-docs/)