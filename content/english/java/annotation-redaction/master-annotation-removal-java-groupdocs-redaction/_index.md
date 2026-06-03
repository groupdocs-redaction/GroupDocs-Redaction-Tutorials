---
title: "Remove PDF Annotations in Java with GroupDocs.Redaction"
description: "Learn how to remove PDF annotations in Java using GroupDocs.Redaction, regex filtering, and save the redacted document with a filename suffix."
date: "2026-02-18"
weight: 1
url: "/java/annotation-redaction/master-annotation-removal-java-groupdocs-redaction/"
keywords:
- annotation removal java
- groupdocs redaction setup
- regex annotation cleanup
type: docs
---

# Remove PDF Annotations in Java with GroupDocs.Redaction

If you need to **remove PDF annotations** quickly and reliably—whether they’re comments, highlights, or sticky notes—GroupDocs.Redaction for Java gives you a clean, programmatic solution. In this tutorial we’ll walk through everything from Maven setup to a regex‑based filter that deletes only the annotations you target, and we’ll show you how to **save the redacted document** with an added filename suffix so the original stays untouched.

## Quick Answers
- **What library handles annotation deletion?** GroupDocs.Redaction for Java.  
- **Which keyword triggers removal?** A regular‑expression pattern you define (e.g., `(?im:(use|show|describe))`).  
- **Do I need a license?** A trial works for evaluation; a commercial license is required for production.  
- **Can I save the cleaned file with a new name?** Yes—use `SaveOptions.setAddSuffix(true)`.  
- **Is Maven the only way to add the library?** No, you can also download the JAR directly.

## What is remove PDF annotations?
Removing PDF annotations means programmatically locating and deleting markup objects (comments, highlights, sticky notes) from a document. With GroupDocs.Redaction you can target these objects by their text content, making it perfect for **legal document redaction**, data‑anonymization projects, or any workflow that requires a clean, share‑ready file.

## Why use remove PDF annotations with GroupDocs.Redaction?
- **Precision** – Regex lets you specify exactly which notes to erase.  
- **Speed** – Process **multiple documents** in a batch without opening each manually.  
- **Compliance** – Ensure sensitive comments never leave your organization.  
- **Cross‑format support** – Works with PDF, DOCX, XLSX, and more, so you can handle all your office files in one place.

## Prerequisites
- Java JDK 1.8 or newer.  
- An IDE such as IntelliJ IDEA or Eclipse.  
- Basic familiarity with regular expressions.  

## Maven Dependency GroupDocs

Add the GroupDocs repository and the Redaction artifact to your `pom.xml`:

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

### Direct Download (alternative)

If you prefer not to use Maven, grab the latest JAR from the official page: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

#### License Acquisition Steps
1. **Free Trial** – Download the trial to explore core features.  
2. **Temporary License** – Request a temporary key for full‑feature testing.  
3. **Purchase** – Obtain a commercial license for production use.

## Basic Initialization and Setup

The following snippet shows how to create a `Redactor` instance and configure basic save options:

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;

public class InitializeRedaction {
    public static void main(String[] args) throws Exception {
        // Load the document using Redactor
        final Redactor redactor = new Redactor("path/to/your/document");
        
        try {
            // Perform your redaction operations here
            
            // Save options can be customized as needed
            SaveOptions saveOptions = new SaveOptions();
            saveOptions.setAddSuffix(true);  // Example option: Add suffix to filename
            
            // Save the modified document
            redactor.save(saveOptions, "path/to/output/document");
        } finally {
            redactor.close();  // Always close resources to prevent memory leaks
        }
    }
}
```

## Step‑by‑Step Guide to Remove PDF Annotations

### Step 1: Load Your Document

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/ANNOTATED_XLSX");
```

### Step 2: Apply Regex‑Based Annotation Removal

```java
redactor.apply(new DeleteAnnotationRedaction("(?im:(use|show|describe))"));
```

- **Explanation** – The pattern `(?im:(use|show|describe))` is case‑insensitive (`i`) and multiline (`m`). It matches any annotation containing *use*, *show*, or *describe*.

### Step 3: Configure Save Options (add filename suffix)

```java
SaveOptions saveOptions = new SaveOptions();
saveOptions.setAddSuffix(true);  // Append a suffix to the output filename
saveOptions.setRasterizeToPDF(false);  // Do not convert to PDF format
```

### Step 4: Save and Release Resources (save redacted document)

```java
redactor.save(saveOptions, "YOUR_OUTPUT_DIRECTORY/RedactedDocument");
redactor.close();  // Always close the Redactor instance
```

**Troubleshooting Tips**  
- Verify that your regex actually matches the annotation text you intend to delete.  
- Double‑check file system permissions if the `save` call throws an `IOException`.  

## Common Use Cases

1. **Data Anonymization Java** – Strip out reviewer comments that contain personal identifiers before sharing datasets.  
2. **Legal Document Redaction** – Automatically delete internal notes that could expose privileged information.  
3. **Batch Processing Pipelines** – Integrate the above steps into a CI/CD job that **processes multiple documents** and cleans up generated reports on the fly.  

## Performance Considerations

- **Optimize regex patterns** – Complex expressions can increase CPU time, especially on large PDFs.  
- **Reuse Redactor instances** only when processing multiple files of the same type; otherwise, instantiate per file to keep memory footprints low.  
- **Profile** – Use Java profiling tools (e.g., VisualVM) to spot bottlenecks in bulk operations.

## Frequently Asked Questions

**Q: What is GroupDocs.Redaction for Java?**  
A: It’s a Java library that lets you redact text, metadata, and annotations across many document formats.

**Q: How can I apply multiple regex patterns in one pass?**  
A: Combine them with the pipe (`|`) operator inside a single pattern or chain multiple `DeleteAnnotationRedaction` calls.

**Q: Does the library support non‑text formats like images?**  
A: Yes, it can redact image‑based PDFs and other raster formats, though annotation removal is only applicable to supported vector formats.

**Q: What if my document type isn’t listed as supported?**  
A: Check the latest [Documentation](https://docs.groupdocs.com/redaction/java/) for updates, or convert the file to a supported format first.

**Q: How should I handle exceptions during redaction?**  
A: Wrap redaction logic in try‑catch blocks, log the exception details, and ensure `redactor.close()` runs in a finally clause.

## Additional Resources

- [Documentation](https://docs.groupdocs.com/redaction/java/)
- [API Reference](https://reference.groupdocs.com/redaction/java)
- [Download GroupDocs.Redaction](https://releases.groupdocs.com/redaction/java/)
- [GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
- [Free Support Forum](https://forum.groupdocs.com/c/redaction/33)

---

**Last Updated:** 2026-02-18  
**Tested With:** GroupDocs.Redaction 24.9 for Java  
**Author:** GroupDocs  

---