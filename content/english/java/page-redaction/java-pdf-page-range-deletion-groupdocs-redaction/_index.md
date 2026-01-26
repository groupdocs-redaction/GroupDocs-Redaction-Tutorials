---
title: "How to Redact PDF: Delete Page Ranges in Java with GroupDocs"
description: "Discover how to redact PDF files by removing page ranges in Java using GroupDocs.Redaction. Learn load pdf java, batch delete pdf pages, and remove pdf page range efficiently."
date: "2026-01-26"
weight: 1
url: "/java/page-redaction/java-pdf-page-range-deletion-groupdocs-redaction/"
keywords:
- Java PDF page range deletion
- GroupDocs.Redaction for Java
- document redaction
type: docs
---

# How to Redact PDF: Delete Page Ranges in Java with GroupDocs

Removing sensitive or redundant pages from a PDF is a common task for developers who need to **how to redact pdf** documents in an automated way. In this tutorial you’ll learn a step‑by‑step approach to load a PDF in Java, delete a specific page range, and save the cleaned file using GroupDocs.Redaction. The instructions are written for developers familiar with Maven and Java IDEs, but we’ll walk through every detail so you can follow along confidently.

## Quick Answers
- **What is the primary purpose of GroupDocs.Redaction?** To programmatically remove or mask content—including whole pages—from PDF and other document formats.  
- **Which method removes a page range?** `RemovePageRedaction` combined with `Redactor.apply()`.  
- **Do I need a license?** A temporary or trial license is required for full functionality.  
- **Can I load a PDF from any folder?** Yes, just provide the full file path to `Redactor`.  
- **Is batch delete pdf pages supported?** You can loop `RemovePageRedaction` calls to delete multiple ranges in one run.

## What is “how to redact pdf”?
Redacting a PDF means permanently removing or obscuring content so it cannot be recovered. With GroupDocs.Redaction you can target text, images, metadata, and entire pages—making it ideal for compliance, privacy, and document customization.

## Why Use GroupDocs.Redaction for Java?
- **High performance** on large files.  
- **Simple API** that integrates with Maven projects.  
- **Built‑in safety**: redactions are irreversible, ensuring compliance.  
- **Cross‑platform** support for Windows, Linux, and macOS.

## Prerequisites
- JDK 8 or newer installed.  
- Maven‑compatible IDE (IntelliJ IDEA, Eclipse, etc.).  
- Access to a GroupDocs.Redaction license (free trial works for testing).  

## Setting Up GroupDocs.Redaction for Java

### Installation

**Maven Setup** – add the repository and dependency to your `pom.xml`:

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

**Direct Download** – you can also get the JAR from the official releases page: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### License Acquisition
Obtain a free trial or temporary license here: [GroupDocs' official site](https://purchase.groupdocs.com/temporary-license/).

### Basic Initialization and Setup
Once the library is on your classpath, initialize the redactor:

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;

// Define your document path.
String documentPath = "YOUR_DOCUMENT_DIRECTORY/your-document.pdf";

LoadOptions loadOptions = new LoadOptions();
final Redactor redactor = new Redactor(documentPath, loadOptions);
```

## Implementation Guide – Removing a Specific PDF Page Range

### Step 1: Load the Document
First, load a multi‑page PDF that you want to edit:

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.examples.java.Constants;

final Redactor redactor = new Redactor(Constants.MULTIPAGE_PDF);
```

### Step 2: Check Page Count and Define the Range
Make sure the document contains enough pages before attempting removal:

```java
import com.groupdocs.redaction.IDocumentInfo;
import com.groupdocs.redaction.redactions.RemovePageRedaction;

IDocumentInfo info = redactor.getDocumentInfo();
int startIndex = 1, pagesToDelete = 1;

if (info.getPageCount() >= 2) {
    // Proceed with the page removal process
}
```

### Step 3: Apply the Redaction
Use `RemovePageRedaction` to specify which pages to delete. This is the core of **how to redact pdf** by page range:

```java
redactor.apply(new RemovePageRedaction(0, startIndex, pagesToDelete));
```

The parameters `startIndex` and `pagesToDelete` define the page range. In this example we delete a single page starting at index 1.

### Step 4: Save the Modified Document
Configure the save options and write the new file:

```java
import com.groupdocs.redaction.options.SaveOptions;

SaveOptions saveOptions = new SaveOptions();
saveOptions.setAddSuffix(true);
saveOptions.setRasterizeToPDF(false);

redactor.save(saveOptions);
```

#### Troubleshooting Tips
- Verify that `startIndex` and `pagesToDelete` are within the document’s page count.  
- Wrap the redaction calls in a try‑catch block to handle `IOException` or `RedactionException`.  
- Always close the `Redactor` instance (or use try‑with‑resources) to free native resources.

### Loading a Document from a Custom Path
If you need to work with PDFs stored outside the project directory, simply pass the full path:

```java
String documentPath = "YOUR_DOCUMENT_DIRECTORY/your-document.pdf";
LoadOptions loadOptions = new LoadOptions();
final Redactor redactor = new Redactor(documentPath, loadOptions);
```

## Practical Applications

1. **Data Privacy Compliance** – Remove confidential pages before sharing files with external partners.  
2. **Document Customization** – Produce tailored versions of a contract by deleting sections irrelevant to a specific client.  
3. **Automated Workflows** – Integrate page‑range removal into batch processing pipelines (the “batch delete pdf pages” scenario).  

## Performance Considerations
- Dispose of the `Redactor` object promptly to avoid memory leaks, especially with large PDFs.  
- If you need to delete multiple, non‑contiguous ranges, call `apply` repeatedly or loop over a list of `RemovePageRedaction` instances.  

## Conclusion
You now have a complete, production‑ready method for **how to redact pdf** files by removing specific page ranges in Java. By following the steps above, you can incorporate page‑range redaction into any Java‑based document workflow, ensuring compliance and delivering cleaner, purpose‑built PDFs.

**Next Steps**
- Explore other redaction types such as text masking or image removal.  
- Combine page deletion with metadata cleaning for a fully sanitized document.  

---

## Frequently Asked Questions

**Q: What is GroupDocs.Redaction?**  
A: A Java library that enables programmatic removal, masking, and redaction of content—including entire pages—from PDF and other document formats.

**Q: Can I remove pages from a single‑page PDF?**  
A: No. The library requires at least two pages to perform a page‑removal operation.

**Q: How do I handle exceptions when working with Redactor?**  
A: Use try‑finally or try‑with‑resources to guarantee that `redactor.dispose()` is called, preventing resource leaks.

**Q: What if I need to delete multiple consecutive pages?**  
A: Adjust `pagesToDelete` to the number of pages you want to remove, or call `RemovePageRedaction` repeatedly for separate ranges.

**Q: Where can I find more advanced redaction techniques?**  
A: Check the official documentation: [GroupDocs documentation](https://docs.groupdocs.com/redaction/java/).

---

**Last Updated:** 2026-01-26  
**Tested With:** GroupDocs.Redaction 24.9 for Java  
**Author:** GroupDocs  

## Resources

- [Documentation](https://docs.groupdocs.com/redaction/java/)
- [API Reference](https://reference.groupdocs.com/redaction/java)
- [Download](https://releases.groupdocs.com/redaction/java/)
- [GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
- [Free Support Forum](https://forum.groupdocs.com/c/redaction/33)
- [Temporary License](https://purchase.groupdocs.com/temporary-license/)

---