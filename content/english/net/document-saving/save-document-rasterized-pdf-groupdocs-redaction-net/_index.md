---
title: "How to Save a Document as Rasterized PDF Using GroupDocs.Redaction in .NET&#58; A Complete Guide"
description: "Learn how to use GroupDocs.Redaction in .NET to redact and save documents securely as rasterized PDFs, ensuring privacy and compliance."
date: "2025-05-16"
weight: 1
url: "/net/document-saving/save-document-rasterized-pdf-groupdocs-redaction-net/"
keywords:
- GroupDocs.Redaction
- Net
- Document Processing

---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}
# How to Save a Document as a Rasterized PDF Using GroupDocs.Redaction in .NET

## Introduction

Protecting sensitive information by converting it into secure, non-editable formats is essential for maintaining privacy and compliance. This tutorial guides you through saving documents as rasterized PDFs using GroupDocs.Redaction in .NET.

**What You'll Learn:**
- Implement exact phrase redactions.
- Save documents as rasterized PDFs securely.
- Configure security and quality settings.
- Troubleshoot common implementation issues.

Let's start with the prerequisites!

### Prerequisites

Ensure you have:
- **Required Libraries:** GroupDocs.Redaction library. Install using one of these methods:
  - **.NET CLI**: Run `dotnet add package GroupDocs.Redaction`
  - **Package Manager Console**: Execute `Install-Package GroupDocs.Redaction`
  - **NuGet Package Manager UI**: Search for "GroupDocs.Redaction" and install the latest version.

- **Environment Setup:** A .NET development environment (Visual Studio recommended).

- **Knowledge Prerequisites:** Basic understanding of C# and .NET, with familiarity in handling file I/O operations.

### Setting Up GroupDocs.Redaction for .NET

**License Acquisition:**

1. Obtain a trial or temporary license to test full capabilities.
2. Purchase a license from the official website for production use.

**Basic Initialization and Setup:**

Add the necessary using directives at the top of your file:

```csharp
using GroupDocs.Redaction;
using GroupDocs.Redaction.Options;
```

## Implementation Guide

### Feature 1: Exact Phrase Redaction

#### Overview

Search for specific text within a document and redact it, replacing sensitive information with an alternative string like "[personal]".

#### Step-by-Step Implementation

**Step 1:** Prepare Your Environment

Set up your output directory and source file paths:

```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY\Sample.docx");
```

**Step 2:** Apply Exact Phrase Redaction

Load the document using a `Redactor` object, then apply an exact phrase redaction.

```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // Replace "John Doe" with "[personal]"
    redactor.Apply(new ExactPhraseRedaction("John Doe\
{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}