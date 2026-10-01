---
date: '2026-10-01'
description: Learn how to remove author metadata and save redacted document files
  in Java using GroupDocs Redaction.
images:
- /java/metadata-redaction/groupdocs-redaction-java-metadata-implementation/og-image.png
keywords:
- remove author metadata
- save redacted document
- groupdocs metadata removal
lastmod: '2026-10-01'
og_description: Learn how to remove author metadata and save redacted document files
  in Java using GroupDocs Redaction. Follow the step‑by‑step guide.
og_image_alt: Guide showing Java code to remove author metadata using GroupDocs Redaction
og_title: How to remove author metadata in Java with GroupDocs
schemas:
- author: GroupDocs
  dateModified: '2026-10-01'
  description: Learn how to remove author metadata and save redacted document files
    in Java using GroupDocs Redaction.
  headline: How to remove author metadata in Java with GroupDocs
  type: TechArticle
- description: Learn how to remove author metadata and save redacted document files
    in Java using GroupDocs Redaction.
  name: How to remove author metadata in Java with GroupDocs
  steps:
  - name: '**Legal documents** – Redact author information before sending contracts
      to opposing counsel.'
    text: '**Legal documents** – Redact author information before sending contracts
      to opposing counsel.'
  - name: '**Corporate reports** – Remove manager names when publishing quarterly
      results to shareholders.'
    text: '**Corporate reports** – Remove manager names when publishing quarterly
      results to shareholders.'
  - name: '**Project files** – Clean up internal project documentation before archiving
      or uploading to a public repository.'
    text: '**Project files** – Clean up internal project documentation before archiving
      or uploading to a public repository.'
  type: HowTo
- questions:
  - answer: It removes selected metadata fields from a document.
    question: What does EraseMetadataRedaction do?
  - answer: GroupDocs.Redaction for Java.
    question: Which library provides this feature?
  - answer: A free trial works for testing; a permanent license is required for production.
    question: Do I need a license?
  - answer: Yes, combine filters with a logical OR.
    question: Can I target multiple fields at once?
  - answer: Redactor instances are not shared across threads; create a new instance
      per operation.
    question: Is the process thread‑safe?
  type: FAQPage
tags:
- metadata redaction
- GroupDocs
- Java document processing
title: How to remove author metadata in Java with GroupDocs
type: docs
url: /java/metadata-redaction/groupdocs-redaction-java-metadata-implementation/
weight: 1
---

# How to remove author metadata in Java with GroupDocs

In today’s digital landscape, protecting sensitive information hidden inside documents is a must‑have practice. **Removing author metadata** prevents accidental disclosure of personal or corporate identifiers. This tutorial shows you, step by step, how to use `EraseMetadataRedaction` from GroupDocs.Redaction for Java to strip out fields such as *Author* and *Manager* from Word files, and then **save redacted document** copies safely for sharing or archiving.

## Quick answers
- **What does EraseMetadataRedaction do?** It removes selected metadata fields from a document.  
- **Which library provides this feature?** GroupDocs.Redaction for Java.  
- **Do I need a license?** A free trial works for testing; a permanent license is required for production.  
- **Can I target multiple fields at once?** Yes, combine filters with a logical OR.  
- **Is the process thread‑safe?** Redactor instances are not shared across threads; create a new instance per operation.

## What is EraseMetadataRedaction?
`EraseMetadataRedaction` is a built‑in redaction class that lets you specify which metadata entries should be erased. It works on a wide range of document formats supported by GroupDocs.Redaction, ensuring that hidden authoring information never leaks. You can target standard properties such as Author, Manager, and also custom metadata fields, providing comprehensive privacy protection.

## Why use EraseMetadataRedaction with GroupDocs?
GroupDocs.Redaction supports **over 100 input and output formats** and can process documents up to 500 pages without loading the entire file into memory. Using this class gives you a single, high‑performance API to meet GDPR, HIPAA, or internal compliance requirements while keeping your codebase simple.

## Prerequisites
- Java 8 or higher installed.  
- Maven (or the ability to add JARs manually).  
- GroupDocs.Redaction for Java (version 24.9 or later).  
- A valid GroupDocs trial or permanent license.

## Setting up GroupDocs.Redaction for Java

### Maven installation
Add the GroupDocs repository and dependency to your **pom.xml**:

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

### License acquisition
Obtain a free trial or purchase a temporary license from the GroupDocs portal. The license file should be placed where your application can load it (e.g., classpath root).

### Basic initialization and setup
Below is a minimal example that creates a `Redactor` instance for a DOCX file:

```java
import com.groupdocs.redaction.Redactor;

String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
Redactor redactor = new Redactor(filePath);
```

## How to use EraseMetadataRedaction in Java
The following sections break down the implementation into clear, actionable steps.

### Feature: clean specific metadata items

#### Overview
We will erase the **Author** and **Manager** metadata fields using `EraseMetadataRedaction`. This is a common requirement when sharing internal reports with external partners.

#### Step‑by‑step implementation

##### 1️⃣ Initialize the Redactor object
`Redactor` is the core class that loads a document, applies redaction objects, and writes the result. Create a new instance for each file you process:

```java
import com.groupdocs.redaction.Redactor;

String inputFilePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
final Redactor redactor = new Redactor(inputFilePath);
```

##### 2️⃣ Apply EraseMetadataRedaction
`MetadataFilters` provides predefined filters for common metadata keys such as Author and Manager.  
`EraseMetadataRedaction` removes metadata entries that match the supplied `MetadataFilters`. The bitwise OR (`|`) combines the `Author` and `Manager` filters so both fields are removed in one call:

```java
import com.groupdocs.redaction.redactions.EraseMetadataRedaction;
import com.groupdocs.redaction.MetadataFilters;

try {
    redactor.apply(new EraseMetadataRedaction(MetadataFilters.Author | MetadataFilters.Manager));
} finally {
    redactor.close();
}
```

##### 3️⃣ Configure save options
`SaveOptions` lets you specify the output file name, format, and other saving parameters.  
`SaveOptions` lets you control the output file name, format, and whether the document should be rasterized to PDF. Adding a suffix keeps the original file untouched:

```java
import com.groupdocs.redaction.options.SaveOptions;

SaveOptions saveOptions = new SaveOptions();
saveOptions.setAddSuffix(true); // Adds "_Redacted" to the file name
saveOptions.setRasterizeToPDF(false);

redactor.save(saveOptions);
```

## Common use cases
1. **Legal documents** – Redact author information before sending contracts to opposing counsel.  
2. **Corporate reports** – Remove manager names when publishing quarterly results to shareholders.  
3. **Project files** – Clean up internal project documentation before archiving or uploading to a public repository.

## Troubleshooting tips
- **File not found** – Verify the path in `inputFilePath` points to an existing file and that the application has read permissions.  
- **Missing metadata fields** – Not all document types store the same metadata keys; check the document’s properties in Office first.  
- **License errors** – Ensure the license file is correctly loaded before creating the `Redactor` instance.

## Performance considerations
- Close the `Redactor` object promptly (as shown in the `finally` block) to free native resources.  
- Avoid rasterizing large documents unless you need a PDF preview; rasterization can increase CPU and memory usage by up to 3× for 300‑page files.

## Frequently asked questions

**Q1: What is metadata redaction?**  
A1: Metadata redaction involves removing hidden document properties (like author, manager, or custom tags) to prevent accidental disclosure of sensitive information.

**Q2: Can I use GroupDocs.Redaction for other file types?**  
A2: Yes, the library supports PDF, DOCX, PPTX, XLSX, and many more formats—over 100 in total.

**Q3: How do I handle errors during redaction?**  
A3: Wrap the `apply` call in a try‑catch block and always close the `Redactor` in a finally clause to ensure resources are released.

**Q4: Is it possible to redact custom metadata fields?**  
A5: Absolutely. Use `MetadataFilters.Custom("YourFieldName")` to target any custom property stored in the document.

**Q5: What are best practices for using GroupDocs.Redaction?**  
A5:  
- Load the license early in your application.  
- Close `Redactor` objects promptly.  
- Use `SaveOptions` to add a suffix, keeping original files untouched.  
- Test redaction on a copy of the document before processing batches.

**Q6: Does EraseMetadataRedaction support batch operations?**  
A6: You can loop over a collection of file paths, creating a new `Redactor` for each file and applying the same redaction logic.

**Q7: Can I combine EraseMetadataRedaction with other redaction types?**  
A7: Yes, you can chain multiple redaction objects (e.g., text redaction followed by metadata redaction) before saving.

## Resources

- **Documentation**: [GroupDocs Redaction Java Docs](https://docs.groupdocs.com/redaction/java/)  
- **API reference**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java)  
- **Download**: [Latest Releases](https://releases.groupdocs.com/redaction/java/)  
- **GitHub**: [GroupDocs GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **Free support**: [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)  
- **Temporary license**: [Acquire a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**Last Updated:** 2026-10-01  
**Tested With:** GroupDocs.Redaction 24.9 for Java  
**Author:** GroupDocs

## Related Tutorials

- [Groupdocs Redaction Java Document Metadata Extraction](/redaction/java/metadata-redaction/groupdocs-redaction-java-document-metadata-extraction/)
- [How to Remove Metadata Java Using GroupDocs.Redaction](/redaction/java/metadata-redaction/metadata-redaction-groupdocs-java-guide/)
- [Retrieve Document Info Using Groupdocs Redaction Java](/redaction/java/document-information/retrieve-document-info-using-groupdocs-redaction-java/)