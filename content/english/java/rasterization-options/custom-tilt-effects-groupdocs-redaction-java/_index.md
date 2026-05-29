---
title: "Apply custom tilt effect with GroupDocs.Redaction Java"
description: "Learn how to apply custom tilt effect to documents using GroupDocs.Redaction for Java, with step‑by‑step code and performance tips."
date: "2026-02-11"
weight: 1
url: "/java/rasterization-options/custom-tilt-effects-groupdocs-redaction-java/"
keywords:
- custom tilt effects
- GroupDocs.Redaction Java
- document rasterization
type: docs
---

# Apply custom tilt effect with GroupDocs.Redaction Java

Enhancing a document’s visual appeal by **applying a custom tilt effect** during rasterization can make reports, marketing materials, or archival scans stand out. In this tutorial you’ll discover why this effect matters, how to configure it with GroupDocs.Redaction for Java, and practical tips to keep performance smooth.

## Quick Answers
- **What does the tilt effect do?** It rotates each rasterized page by a random angle within a defined range, creating a dynamic, slightly skewed look.  
- **Which library provides this feature?** GroupDocs.Redaction for Java (version 24.9 or newer).  
- **Do I need a license?** A free trial works for evaluation; a permanent or temporary license is required for production.  
- **Is it memory‑intensive?** It adds some CPU overhead, but proper memory settings keep it efficient even for large files.  
- **Can I customize the angle range?** Yes – use `minAngle` and `maxAngle` parameters in the rasterization options.

## What is a custom tilt effect?

A custom tilt effect is a visual transformation applied while converting each page of a document into an image. By specifying minimum and maximum angles, the rasterizer randomly tilts pages, giving the final output an artistic, “hand‑held” feel.

## Why apply custom tilt effect with GroupDocs.Redaction?

- **Engagement:** Tilted pages catch the reader’s eye, perfect for presentations or marketing brochures.  
- **Branding:** Adds a unique visual signature without altering the original content.  
- **Flexibility:** You control the angle range, enabling subtle or dramatic tilts.  
- **Integration:** The effect is built into GroupDocs.Redaction’s rasterization pipeline, so you don’t need external image‑processing tools.

## Prerequisites

- Java 8 or later installed.  
- Maven (or another build tool) to manage dependencies.  
- GroupDocs.Redaction 24.9 or newer (the tutorial uses the latest release).  
- Basic familiarity with Java file handling.

## Setting Up GroupDocs.Redaction for Java

### Installation Information

**Maven**

Include GroupDocs.Redaction in your Maven project by adding the following repository and dependency to your `pom.xml` file:

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

**Direct Download**

Alternatively, download the latest version directly from [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

#### License Acquisition

To fully utilize GroupDocs.Redaction:

- **Free Trial** – explore core features at no cost.  
- **Temporary License** – request a time‑limited key for full evaluation via [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/).  
- **Purchase** – obtain a permanent license for production use.

### Basic Initialization and Setup

To start, import the required classes and create a `Redactor` instance pointing at your source document:

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;

// Set the path to your document directory
String documentPath = "YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX";

// Initialize a Redactor with the specified document
Redactor redactor = new Redactor(documentPath);
```

## How to apply custom tilt effect during rasterization

### Overview of the feature

GroupDocs.Redaction lets you enable rasterization and inject advanced options such as a tilt effect. By configuring `AdvancedRasterizationOptions.Tilt` you control the angle range applied to each page.

### Step‑by‑step implementation

#### Step 1: Initialize Redactor and Save Options

```java
import com.groupdocs.redaction.options.AdvancedRasterizationOptions;
import java.util.HashMap;

Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
SaveOptions saveOptions = new SaveOptions();
```

#### Step 2: Configure Tilt Effect Settings

Enable rasterization and define the tilt angle boundaries:

```java
saveOptions.getRasterization().setEnabled(true);
HashMap<String, String> tiltSettings = new HashMap<>();
tiltSettings.put("minAngle", "15"); // Set the minimum angle for the tilt effect
	tiltSettings.put("maxAngle", "30"); // Set the maximum angle for the tilt effect

saveOptions.getRasterization().addAdvancedOption(
    AdvancedRasterizationOptions.Tilt, 
    tiltSettings
);
```

#### Step 3: Save Document with Tilt Effect

Run the redaction process and output the rasterized, tilted document:

```java
redactor.save("OUTPUT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX_scan", saveOptions);
```

### Explanation of parameters

- **minAngle** – the smallest rotation (in degrees) that can be applied to a page.  
- **maxAngle** – the largest rotation (in degrees) allowed.  
Adjust these values to achieve subtle or pronounced tilts.

#### Troubleshooting Tips

- Verify that the source and output directories are writable by the JVM.  
- Confirm you are using GroupDocs.Redaction 24.9 or newer; older versions lack the `Tilt` option.  
- If the output looks overly distorted, reduce the `maxAngle` value.

## Practical Applications

1. **Creative Document Presentation** – add a dynamic look to slide decks or client proposals.  
2. **Marketing Materials** – make brochures and flyers feel more hand‑crafted.  
3. **Digital Archives** – give historical scans a subtle, stylized appearance for online exhibitions.

## Performance Considerations

### Optimizing Performance

- **Memory Management:** Allocate sufficient heap space (`-Xmx2g` or higher) when processing multi‑page PDFs.  
- **I/O Efficiency:** Batch process files and reuse a single `Redactor` instance where possible.

### Best Practices for Java Memory Management

- Invoke `System.gc()` sparingly; rely on the JVM’s garbage collector.  
- Close streams promptly (GroupDocs.Redaction handles most cleanup internally).

## Common Issues and Solutions

| Issue | Likely Cause | Solution |
|-------|--------------|----------|
| Tilt not applied | Rasterization disabled | Ensure `saveOptions.getRasterization().setEnabled(true);` |
| Output file empty | Incorrect output path | Verify the directory exists and has write permissions |
| Unexpected angles | `minAngle` > `maxAngle` | Swap values so `minAngle` ≤ `maxAngle` |

## Frequently Asked Questions

**Q: What is GroupDocs.Redaction Java used for?**  
A: It redacts sensitive content while preserving document layout and also supports advanced rasterization features like the tilt effect.

**Q: How do I apply a tilt effect in my document using GroupDocs?**  
A: By enabling rasterization and adding the `Tilt` advanced option with `minAngle` and `maxAngle` parameters, as shown in the code samples.

**Q: Can I use GroupDocs.Redaction for free?**  
A: Yes, a free trial is available. For production use, obtain a temporary or permanent license.

**Q: What are the benefits of using a tilt effect in documents?**  
A: It enhances visual appeal, adds a creative touch, and can help differentiate marketing or presentation materials.

**Q: Are there any limitations to applying custom effects with GroupDocs.Redaction Java?**  
A: Very large files may increase processing time and memory usage; proper resource allocation mitigates this.

## Resources
- [GroupDocs Redaction Documentation](https://docs.groupdocs.com/redaction/java/)
- [API Reference](https://reference.groupdocs.com/redaction/java)
- [Download GroupDocs.Redaction for Java](https://releases.groupdocs.com/redaction/java/)
- [GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
- [Free Support Forum](https://forum.groupdocs.com/c/redaction/33)
- [Temporary License Application](https://purchase.groupdocs.com/temporary-license/)

---

**Last Updated:** 2026-02-11  
**Tested With:** GroupDocs.Redaction 24.9 for Java  
**Author:** GroupDocs  

---