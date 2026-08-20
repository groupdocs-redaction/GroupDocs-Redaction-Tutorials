---
date: '2026-08-20'
description: Learn how to redact text in Java documents using GroupDocs.Redaction,
  covering exact‑phrase, regex, color replacement, annotation and metadata redaction
  for secure compliance.
images:
- /java/text-redaction/java-redaction-guide-groupdocs-document-security/og-image.png
keywords:
- how to redact text
- replace text with color
- GroupDocs.Redaction Java
- Java document security
- document redaction library
lastmod: '2026-08-20'
og_description: Learn how to redact text in Java documents using GroupDocs.Redaction,
  covering exact‑phrase, regex, color replacement, annotation and metadata redaction.
og_image_alt: Guide showing Java code redacting text with GroupDocs.Redaction
og_title: How to redact text in Java documents with GroupDocs.Redaction
schemas:
- author: GroupDocs
  dateModified: '2026-08-20'
  description: Learn how to redact text in Java documents using GroupDocs.Redaction,
    covering exact‑phrase, regex, color replacement, annotation and metadata redaction
    for secure compliance.
  headline: How to redact text in Java documents with GroupDocs.Redaction
  type: TechArticle
- description: Learn how to redact text in Java documents using GroupDocs.Redaction,
    covering exact‑phrase, regex, color replacement, annotation and metadata redaction
    for secure compliance.
  name: How to redact text in Java documents with GroupDocs.Redaction
  steps:
  - name: '**Add the Maven dependency** (or include the JAR).'
    text: '**Add the Maven dependency** (or include the JAR).'
  - name: '**Configure your license** by calling `License.setLicense("path/to/license.lic")`
      early in your application.'
    text: '**Configure your license** by calling `License.setLicense("path/to/license.lic")`
      early in your application.'
  - name: '**Create a `Redactor` instance** pointing at the source document.'
    text: '**Create a `Redactor` instance** pointing at the source document.'
  - name: '**Initialize the Redactor** with the document you want to process:'
    text: '**Initialize the Redactor** with the document you want to process:'
  - name: '**Define the exact‑phrase rule** and apply it:'
    text: '**Define the exact‑phrase rule** and apply it:'
  - name: '**Save the redacted file** to your output folder:'
    text: '**Save the redacted file** to your output folder:'
  - name: 'Load the document:'
    text: 'Load the document:'
  - name: 'Create a regex rule and apply it:'
    text: 'Create a regex rule and apply it:'
  - name: 'Save the result:'
    text: 'Save the result:'
  - name: 'Load the document:'
    text: 'Load the document:'
  type: HowTo
- questions:
  - answer: Yes. Create each redaction object, call `redactor.apply()` for each, then
      save once.
    question: Can I combine multiple redaction rules in a single pass?
  - answer: Absolutely. Pass the password to the `Redactor` constructor that accepts
      a `LoadOptions` object.
    question: Does GroupDocs.Redaction support password‑protected files?
  - answer: You can call `redactor.preview()` to generate a temporary view that highlights
      the areas to be redacted.
    question: Is it possible to preview redactions before saving?
  - answer: DOCX, PDF, PPTX, XLSX, PNG, JPEG, BMP, and many more—over 30 formats in
      total.
    question: What file formats are supported?
  - answer: Use the metadata erasure feature, remove annotations, and apply exact‑phrase
      or regex redactions to all personal data fields.
    question: How do I ensure the redacted document complies with GDPR?
  type: FAQPage
tags:
- text redaction
- GroupDocs.Redaction
- Java document security
- regex redaction
- metadata removal
title: How to redact text in Java documents with GroupDocs.Redaction
type: docs
url: /java/text-redaction/java-redaction-guide-groupdocs-document-security/
weight: 1
---

# How to redact text in Java documents with GroupDocs.Redaction

In modern applications, **how to redact text** inside PDFs, Word files, or images is a frequent requirement for compliance and privacy. Whether you need to hide personal identifiers, remove confidential annotations, or strip metadata, GroupDocs.Redaction for Java gives you a clean, programmatic way to achieve **java document security**. This tutorial walks you through every essential step—from setting up the library to applying exact‑phrase, regex, color‑based, annotation, and metadata redactions—so you can embed redaction directly into your backend services.

## Quick answers
- **What library handles Java document redaction?** GroupDocs.Redaction for Java.  
- **Can I replace text with color instead of removing it?** Yes, use the “replace text with color” feature.  
- **Do I need a license for production use?** A temporary or paid license is required for full functionality.  
- **Which Java versions are supported?** JDK 8 or higher.  
- **Is Maven the only way to add the library?** Maven is recommended, but you can also download the JAR manually.

## What is “how to redact text” in Java?
**Redaction permanently removes or obscures sensitive content so it cannot be recovered.** In Java, you load a file, define what to hide, apply the redaction, and save the sanitized version. This ensures that any downstream consumer sees only the cleaned‑up document.

## Why use GroupDocs.Redaction for Java?
Load your file, define a rule, and the SDK handles the heavy lifting. GroupDocs.Redaction supports **30+ formats**—including DOCX, PDF, PPTX, XLSX, PNG, JPEG, BMP—and processes large documents via stream‑based architecture. It offers exact‑phrase, regex, color‑based, annotation, and metadata redaction, providing fine‑grained control to meet GDPR, HIPAA, and other regulations.

## Prerequisites
- **Java Development Kit (JDK) 8+** installed on your machine.  
- **Maven** for dependency management (or you can download the JAR manually).  

### Required libraries and dependencies
Add the GroupDocs repository and the Redaction dependency to your `pom.xml`:

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

You can also download the latest JAR from the official release page: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### License acquisition
For production use, obtain a temporary or full license. A free trial is available for evaluation purposes.

## Setting up GroupDocs.Redaction for Java
1. **Add the Maven dependency** (or include the JAR).  
2. **Configure your license** by calling `License.setLicense("path/to/license.lic")` early in your application.  
   `License` is the class used to load and apply a GroupDocs Redaction license file.  
3. **Create a `Redactor` instance** pointing at the source document.

**The `Redactor` class is the core engine that loads, modifies, and saves documents in a memory‑efficient way.** Once you have a `Redactor` object, you can chain multiple redaction rules before persisting the result.

Now you’re ready to start redacting.

## Implementation guide

### Exact phrase redaction
Replace a specific phrase (e.g., a person's name) with placeholder text.

#### How does exact‑phrase redaction work?
`ExactPhraseRedaction` represents a rule that removes or replaces a specific exact text string. Load the document, create an `ExactPhraseRedaction` rule that targets the exact string, apply the rule, and save the output. The SDK automatically blanks out the matched text while preserving layout.

1. **Initialize the Redactor** with the document you want to process:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. **Define the exact‑phrase rule** and apply it:

```java
ExactPhraseRedaction redaction = new ExactPhraseRedaction(
    "John Doe", 
    new ReplacementOptions("[Client]"));

redactor.apply(redaction);
```

3. **Save the redacted file** to your output folder:

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Redaction applied successfully.");
}
```

### Regex redaction with text replacement
Use regular expressions to locate patterns such as serial numbers and replace them with a generic token.

#### How does regex redaction with replacement work?
`RegexRedaction` defines a rule based on a regular expression to find and modify matching text. You provide a `RegexRedaction` object that contains the pattern and the replacement string. The engine scans the document, substitutes every match, and keeps the surrounding formatting intact.

1. Load the document:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. Create a regex rule and apply it:

```java
RegexRedaction redaction = new RegexRedaction(
    "Redaction",
    new ReplacementOptions("[Product]"));

redactor.apply(redaction);
```

3. Save the result:

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Redaction applied successfully.");
}
```

### Regex redaction with color replacement
Instead of deleting text, you can **replace text with color** to visually obscure it while keeping the underlying characters.

#### How does color‑based redaction differ from deletion?
The SDK paints the matched text with the chosen color, making it unreadable to the human eye but still present in the file stream. This is useful when you need to retain document structure for downstream processing.

1. Load the document:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. Define a regex pattern and set the replacement color (e.g., blue):

```java
RegexRedaction redaction = new RegexRedaction(
    "\d{2}\s*\d{2}[^\\d]*\d{6}", 
    new ReplacementOptions(Color.BLUE));

redactor.apply(redaction);
```

3. Save the updated file:

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Redaction applied successfully.");
}
```

### Delete annotation redaction
Strip all annotations (comments, highlights, etc.) from a document for a cleaner final version.

#### How to remove annotations in one step?
`AnnotationRedaction` is a rule that removes annotations such as comments, highlights, and stamps. Create an `AnnotationRedaction` rule that targets every annotation type, apply it, and persist the changes.

1. Load your file:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. Apply the annotation‑deletion rule:

```java
DeleteAnnotationRedaction redaction = new DeleteAnnotationRedaction();

redactor.apply(redaction);
```

3. Persist the changes:

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Annotations deleted successfully.");
}
```

### Erase metadata redaction
Remove every piece of metadata (author, creation date, custom properties) to protect privacy and meet compliance standards.

#### How does metadata erasure guarantee privacy?
`MetadataRedaction` clears built‑in and custom metadata fields from the document. The `MetadataRedaction` rule wipes built‑in and custom metadata fields, ensuring that no hidden identifiers remain in the file’s property bag.

1. Open the document:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. Apply the metadata‑erasure rule:

```java
EraseMetadataRedaction redaction = new EraseMetadataRedaction(MetadataFilters.All);

redactor.apply(redaction);
```

3. Save the sanitized document:

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Metadata erased successfully.");
}
```

## Practical applications (why this matters)
- **Legal document preparation** – Redact client names before sharing drafts with opposing counsel.  
- **Healthcare compliance** – Remove patient identifiers to stay HIPAA‑compliant without manual editing.  
- **Corporate data protection** – Hide financial figures or trade secrets in internal reports before distribution.  

Automating these steps reduces manual effort, eliminates human error, and ensures consistent compliance across thousands of files.

## Performance considerations
- **Stream instead of load** – For large files, use `Redactor` constructors that accept `InputStream` to avoid loading the entire document into memory.  
- **Pre‑compile regex patterns** when you run the same redaction repeatedly; this cuts CPU overhead by up to 30 %.  
- **Monitor JVM heap** – Redaction can be memory‑intensive; consider increasing the heap size (`-Xmx2g`) for batch processing of multi‑gigabyte archives.  

## Common issues & troubleshooting
| Symptom | Likely cause | Fix |
|---------|--------------|-----|
| No changes after `apply` | Wrong document path or file locked | Verify the file path and ensure the document isn’t opened elsewhere |
| Regex not matching | Pattern syntax error | Test the regex with an online tester; escape backslashes properly |
| Color replacement not visible | Output format doesn’t support text color (e.g., plain text) | Use a format like DOCX or PDF that retains styling |
| License error at runtime | License file missing or invalid | Place the `.lic` file in a reachable directory and call `License.setLicense` before any Redactor usage |

## Frequently asked questions

**Q: Can I combine multiple redaction rules in a single pass?**  
A: Yes. Create each redaction object, call `redactor.apply()` for each, then save once.

**Q: Does GroupDocs.Redaction support password‑protected files?**  
A: Absolutely. Pass the password to the `Redactor` constructor that accepts a `LoadOptions` object.

**Q: Is it possible to preview redactions before saving?**  
A: You can call `redactor.preview()` to generate a temporary view that highlights the areas to be redacted.

**Q: What file formats are supported?**  
A: DOCX, PDF, PPTX, XLSX, PNG, JPEG, BMP, and many more—over 30 formats in total.

**Q: How do I ensure the redacted document complies with GDPR?**  
A: Use the metadata erasure feature, remove annotations, and apply exact‑phrase or regex redactions to all personal data fields.

## Conclusion
You now have a complete, end‑to‑end guide on **how to redact text** in Java documents using GroupDocs.Redaction. By following the steps for exact‑phrase, regex, color‑based, annotation, and metadata redactions, you can achieve robust **java document security** while keeping your code clean and maintainable. Integrate these snippets into your existing services, automate batch processing, and stay compliant with privacy regulations.

---

**Last Updated:** 2026-08-20  
**Tested with:** GroupDocs.Redaction 24.9 for Java  
**Author:** GroupDocs

## Related Tutorials

- [replace metadata text java – Secure Redaction with GroupDocs](/redaction/java/metadata-redaction/java-redaction-metadata-text-replacement-guide/)
- [How to Redact Images in Word Documents Using GroupDocs.Redaction for Java – A Comprehensive Guide](/redaction/java/image-redaction/redact-images-word-docs-groupdocs-redaction-java/)
- [How to Redact Documents with GroupDocs Redaction Java License from File Path – A Step‑by‑Step Guide](/redaction/java/licensing-configuration/implement-groupdocs-redaction-java-license-file-path/)