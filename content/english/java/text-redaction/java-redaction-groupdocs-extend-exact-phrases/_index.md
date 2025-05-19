---
title: "Java Redaction with GroupDocs&#58; Extending and Applying Exact Phrases for Text Redaction"
description: "Learn how to extend supported file extensions and perform exact phrase redactions using GroupDocs.Redaction for Java. Enhance your document processing capabilities effortlessly."
date: "2025-05-16"
weight: 1
url: "/java/text-redaction/java-redaction-groupdocs-extend-exact-phrases/"
keywords:
- GroupDocs.Redaction
- Java
- Document Processing

---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}
# Implementing Java Redaction: Extending and Applying Exact Phrases with GroupDocs Redaction

## Introduction

Struggling to handle custom file types like `.dump` in your document processing workflow? Need a reliable way to redact sensitive information seamlessly? With GroupDocs.Redaction for Java, these challenges become straightforward tasks. This guide walks you through extending supported file extensions and performing exact phrase redactions using GroupDocs.Redaction.

**What You'll Learn:**
- Extending supported file extensions in GroupDocs.Redaction.
- Applying exact phrase redaction on documents with ease.
- Setting up and configuring GroupDocs.Redaction for Java projects.

## Prerequisites

Before implementing these features, ensure you have:

### Required Libraries, Versions, and Dependencies
- **GroupDocs.Redaction**: Version 24.9 or later.
- **Java Development Kit (JDK)**: JDK 8 or higher.
  
### Environment Setup Requirements
- A Java development environment with Maven installed.
### Knowledge Prerequisites
- Basic understanding of Java programming.
- Familiarity with document processing concepts and redactions.

## Setting Up GroupDocs.Redaction for Java

To get started, integrate GroupDocs.Redaction into your project using Maven or direct download methods:

**Maven Setup**

Add the following configuration to your `pom.xml` file:
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
Alternatively, download the latest version from [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### License Acquisition Steps
1. **Free Trial**: Start with a free trial to explore GroupDocs.Redaction.
2. **Temporary License**: Obtain a temporary license for extended evaluation.
3. **Purchase**: Acquire a full license to unlock all features.

**Basic Initialization and Setup**
Once the library is included in your project, initialize it as follows:
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.configuration.DocumentFormatConfiguration;
import com.groupdocs.redaction.configuration.RedactorConfiguration;
import com.groupdocs.redaction.integration.DocumentFormatInstance;

// Obtain default configuration for redactions
RedactorConfiguration config = DocumentFormatInstance.getDefaultConfiguration();
```
## Implementation Guide

### Extend Supported File Extensions

#### Overview
This feature enables you to extend the list of supported file extensions, allowing GroupDocs.Redaction to process custom files like `.dump`.

#### Step-by-Step Implementation
**Step 1: Obtain Default Configuration for Redactions**
```java
RedactorConfiguration config = DocumentFormatInstance.getDefaultConfiguration();
```
Here, we retrieve the default configuration essential for setting up document processing capabilities.

**Step 2: Retrieve Settings for a File Format**
```java
DocumentFormatConfiguration settings = config.findFormat(".txt");
```
We target existing configurations (e.g., `.txt`) to extend their functionality.

**Step 3: Extend Supported Extensions by Adding .dump**
```java
settings.setExtensionFilter(settings.getExtensionFilter() + \
{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}