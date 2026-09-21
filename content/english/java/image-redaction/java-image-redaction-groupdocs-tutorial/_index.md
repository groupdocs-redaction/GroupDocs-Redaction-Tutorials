---
date: '2026-09-21'
description: Learn how to redact image with GroupDocs.Redaction for Java. Step‑by‑step
  guide covers setup, pixel‑level redaction, verification, and best practices.
images:
- /java/image-redaction/java-image-redaction-groupdocs-tutorial/og-image.png
keywords:
- how to redact image
- Java image redaction
- GroupDocs.Redaction for Java
- scanned image redaction
- pixel redaction Java
lastmod: '2026-09-21'
og_description: How to redact image with GroupDocs.Redaction for Java. Follow this
  guide to mask pixel data in scanned files, choose colors, and verify results—perfect
  for GDPR and HIPAA compliance.
og_image_alt: Guide showing Java code that redacts scanned images using GroupDocs.Redaction
og_title: How to redact image using GroupDocs.Redaction for Java
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: Learn how to redact image with GroupDocs.Redaction for Java. Step‑by‑step
    guide covers setup, pixel‑level redaction, verification, and best practices.
  headline: How to redact image using GroupDocs.Redaction for Java
  type: TechArticle
- description: Learn how to redact image with GroupDocs.Redaction for Java. Step‑by‑step
    guide covers setup, pixel‑level redaction, verification, and best practices.
  name: How to redact image using GroupDocs.Redaction for Java
  steps:
  - name: define redaction parameters
    text: '`ImageAreaRedaction` works with a `Point` (top‑left corner) and a `Dimension`
      (width × height) that describe the rectangle to hide. In this example we use
      a blue fill color.'
  - name: apply redaction
    text: '`RegionReplacementOptions` lets you specify the fill color and optional
      border. Passing these options to `ImageAreaRedaction` and invoking `apply()`
      performs the masking. The method returns a `RedactorChangeLog` that indicates
      success or failure.'
  - name: release resources
    text: '`Redactor` implements `AutoCloseable`. Closing it frees native buffers
      and file handles, preventing memory leaks in long‑running services.'
  type: HowTo
- questions:
  - answer: '`ImageAreaRedaction` works on raw pixel coordinates, while text redaction
      parses OCR layers to locate and remove textual content.'
    question: What is the difference between `ImageAreaRedaction` and text redaction?
  - answer: Yes—call `redactor.apply()` repeatedly with different `ImageAreaRedaction`
      objects before saving the final file.
    question: Can I redact multiple regions in a single image?
  - answer: The library supports common raster formats (JPG, PNG, BMP, GIF). For TIFF,
      convert the image to a supported format first.
    question: Does GroupDocs.Redaction support other image formats like TIFF?
  - answer: Extract each page as an image, apply the same redaction logic, then rebuild
      the PDF using a PDF library such as GroupDocs.Conversion.
    question: How do I automate redaction for a folder of scanned PDFs?
  - answer: Render the `Redactor` to a `BufferedImage` and display it in a Swing or
      JavaFX UI, allowing you to confirm the masked area before committing.
    question: Is there a way to preview the redaction before saving?
  type: FAQPage
tags:
- image redaction
- GroupDocs
- Java
- document privacy
- data protection
title: How to redact image using GroupDocs.Redaction for Java
type: docs
url: /java/image-redaction/java-image-redaction-groupdocs-tutorial/
weight: 1
---

# How to redact image using GroupDocs.Redaction for Java

In this comprehensive tutorial you’ll learn **how to redact image** files in Java with GroupDocs.Redaction. Redacting scanned images is a crucial step for protecting personal data, meeting GDPR, HIPAA, or other privacy regulations, and ensuring that confidential visual information never leaks. We’ll walk you through project setup, configuring pixel‑level redaction, saving the result safely, and confirming that the redaction succeeded—all presented in a conversational, step‑by‑step style you can copy into any Java application.

## Quick answers
- **What library handles image redaction in Java?** GroupDocs.Redaction for Java.  
- **Can I choose the redaction color?** Yes – any opaque `java.awt.Color` such as `Color.BLUE` or `Color.BLACK`.  
- **Is a license required for production?** Yes, a valid GroupDocs license is mandatory for commercial use.  
- **Will the original image be overwritten?** No – the API writes the redacted image to a new file you specify.  
- **What Java version is supported?** Java 8 and newer (up to Java 21 at the time of writing).

## What is image redaction and why redact scanned image java?
Image redaction permanently obscures visual data—names, numbers, signatures—by replacing pixel regions with a solid color. Unlike text redaction, which works on selectable characters, scanned images store information as raw pixels, so only pixel‑based tools can guarantee that the data cannot be recovered. Using GroupDocs.Redaction you can target exact coordinates, apply any opaque color, and produce a new image that removes the sensitive content for good.

## Why use GroupDocs.Redaction for Java?
GroupDocs.Redaction supports **50+ image formats** (including JPG, PNG, BMP, GIF) and can process multi‑hundred‑page documents without loading the entire file into memory, thanks to its streaming architecture. Benchmarks show that a 300 KB scanned PNG is redacted in under 120 ms on a typical 2.8 GHz CPU, making it suitable for both batch jobs and real‑time services.

## Prerequisites
Before you begin, ensure you have:

- **JDK 8 or newer** installed and configured in your `PATH`.  
- **Maven** (or Gradle) for dependency management.  
- An IDE such as **IntelliJ IDEA**, **Eclipse**, or **NetBeans**.  
- Basic familiarity with Java file I/O and the `java.awt` package.  

## Setting up GroupDocs.Redaction for Java

### Maven setup
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
Alternatively, download the latest JAR from the official release page: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### License acquisition
- **Free trial:** Sign up for a trial to explore the full API.  
- **Temporary license:** Use a temporary key for extended testing without cost.  
- **Full purchase:** Obtain a production license for unlimited deployment.

## Implementation guide

We’ll split the implementation into two core features: **image‑area redaction** (the actual masking) and **redaction status check** (verifying success).

### How to redact scanned document images – step 1: initialize the redactor
`Redactor` is the central class that loads an image and provides redaction operations.  
Create a `Redactor` instance that points to the source image you want to process.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_JPG");
```

### Step 2: define redaction parameters
`ImageAreaRedaction` works with a `Point` (top‑left corner) and a `Dimension` (width × height) that describe the rectangle to hide. In this example we use a blue fill color.

```java
// Define the position on the image where redaction starts.
Point samplePoint = new Point(385, 485);

// Define the size of the area to be redacted.
Dimension sampleSize = new Dimension(1793, 2069);
```

### Step 3: apply redaction
`RegionReplacementOptions` lets you specify the fill color and optional border. Passing these options to `ImageAreaRedaction` and invoking `apply()` performs the masking. The method returns a `RedactorChangeLog` that indicates success or failure.

```java
RedactorChangeLog result = redactor.apply(
    new ImageAreaRedaction(samplePoint, new RegionReplacementOptions(Color.BLUE, sampleSize))
);

// Check if the redaction was successful and save the output.
if (result.getStatus() != RedactionStatus.Failed) {
    redactor.save("YOUR_OUTPUT_DIRECTORY/redacted_output.jpg");
}
```

### Step 4: release resources
`Redactor` implements `AutoCloseable`. Closing it frees native buffers and file handles, preventing memory leaks in long‑running services.

```java
redactor.close();
```

### How to verify the redaction – status check
After applying the redaction, inspect the `RedactorChangeLog`. A `Status.SUCCESS` value confirms that the pixel region was replaced without error. You can also render the image to a `BufferedImage` for visual inspection before saving.

```java
if (result != null && result.getStatus() != RedactionStatus.Failed) {
    System.out.println("Redaction was successful.");
} else {
    System.out.println("Redaction failed.");
}
```

## Practical applications
- **Confidential document handling:** Mask personal data in scanned contracts before sharing with partners.  
- **Legal documentation:** Ensure GDPR or HIPAA compliance by redacting identifiers in evidence images.  
- **Medical records:** Hide patient faces or handwritten notes in radiology scans while preserving diagnostic details.  

## Performance considerations
- **Batch processing:** Process images in groups of 10–20 to keep memory usage under 200 MB.  
- **Object reuse:** Reuse `Point` and `Dimension` objects across iterations to reduce GC pressure.  
- **Version updates:** Upgrade to the latest GroupDocs.Redaction release to benefit from a 15 % speed improvement reported in version 24.10.  

## Common issues & solutions
| Issue | Cause | Fix |
|-------|-------|-----|
| **Redaction fails with `Failed` status** | Incorrect file path or unsupported image format | Verify the file exists and is a supported format (JPG, PNG, BMP, GIF). |
| **Output file is empty** | `redactor.save()` called before redaction completes | Ensure `apply()` returns `Status.SUCCESS` before invoking `save()`. |
| **Color not applied** | Using a transparent `Color` | Choose an opaque color such as `Color.BLACK` or `Color.BLUE`. |

## Frequently asked questions

**Q: What is the difference between `ImageAreaRedaction` and text redaction?**  
A: `ImageAreaRedaction` works on raw pixel coordinates, while text redaction parses OCR layers to locate and remove textual content.

**Q: Can I redact multiple regions in a single image?**  
A: Yes—call `redactor.apply()` repeatedly with different `ImageAreaRedaction` objects before saving the final file.

**Q: Does GroupDocs.Redaction support other image formats like TIFF?**  
A: The library supports common raster formats (JPG, PNG, BMP, GIF). For TIFF, convert the image to a supported format first.

**Q: How do I automate redaction for a folder of scanned PDFs?**  
A: Extract each page as an image, apply the same redaction logic, then rebuild the PDF using a PDF library such as GroupDocs.Conversion.

**Q: Is there a way to preview the redaction before saving?**  
A: Render the `Redactor` to a `BufferedImage` and display it in a Swing or JavaFX UI, allowing you to confirm the masked area before committing.

## Conclusion
You now have a complete, production‑ready guide on **how to redact image** content and, specifically, how to **redact scanned image java** using GroupDocs.Redaction for Java. By following the steps above you can protect sensitive visual data across finance, legal, and healthcare domains. Explore additional APIs—such as text redaction, PDF page redaction, or bulk folder processing—to build an end‑to‑end data‑privacy pipeline for your organization.

**Resources**  
- [Documentation](https://docs.groupdocs.com/redaction/java/)  
- [API reference](https://reference.groupdocs.com/redaction/java)  
- [Download](https://releases.groupdocs.com/redaction/java/)  
- [GitHub repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- [Free support forum](https://forum.groupdocs.com/c/redaction/33)  
- [Temporary license](https://purchase.groupdocs.com/temporary-license/) 

---

**Last Updated:** 2026-09-21  
**Tested with:** GroupDocs.Redaction 24.9 (Java)  
**Author:** GroupDocs

## Related Tutorials

- [How to Redact Java with GroupDocs.Redaction - A Comprehensive Guide for Developers](/redaction/java/getting-started/implement-java-redaction-groupdocs-redaction-guide/)
- [How to Redact Scanned PDF with OCR – GroupDocs.Redaction Java](/redaction/java/ocr-integration/)
- [How to Redact Text in Java with GroupDocs.Redaction – Guide](/redaction/java/text-redaction/text-redaction-java-groupdocs-redaction/)