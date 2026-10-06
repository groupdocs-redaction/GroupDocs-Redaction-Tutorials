---
date: '2026-10-06'
description: Learn how to redact sensitive data with GroupDocs.Redaction .NET. This
  step‑by‑step guide shows you how to create, apply, and save a redaction policy as
  XML.
images:
- /net/advanced-redaction/groupdocs-redaction-net-create-save-policy/og-image.png
keywords:
- redact sensitive data
- mask confidential information
- groupdocs redaction .net
lastmod: '2026-10-06'
og_description: Learn how to redact sensitive data with GroupDocs.Redaction .NET.
  This step‑by‑step guide shows you how to create, apply, and save a redaction policy
  as XML.
og_image_alt: Tutorial showing how to redact sensitive data in documents with GroupDocs.Redaction
  for .NET
og_title: How to redact sensitive data using GroupDocs.Redaction .NET
schemas:
- author: GroupDocs
  dateModified: '2026-10-06'
  description: Learn how to redact sensitive data with GroupDocs.Redaction .NET. This
    step‑by‑step guide shows you how to create, apply, and save a redaction policy
    as XML.
  headline: How to redact sensitive data using GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to redact sensitive data with GroupDocs.Redaction .NET. This
    step‑by‑step guide shows you how to create, apply, and save a redaction policy
    as XML.
  name: How to redact sensitive data using GroupDocs.Redaction .NET
  steps:
  - name: prepare your document directory
    text: '*Replace `"YOUR_DOCUMENT_DIRECTORY"` with the folder that holds the documents
      you want to protect.*'
  - name: load the document
    text: The `Redactor` object opens the file and manages its lifecycle.
  - name: define the redactions
    text: 'ExactPhraseRedaction defines a rule that replaces a specific phrase, while
      `RegexRedaction` uses a regular expression to match patterns. Here we create
      two rules: 1. **ExactPhraseRedaction** – replaces a known phrase with “[REDACTED]”.
      2. **RegexRedaction** – finds dates in `YYYY‑MM‑DD` format and r'
  - name: apply the redactions
    text: All defined rules are executed against the opened document in one pass.
  - name: save the policy as an XML file
    text: The XML file stores the redaction definitions, allowing you to reuse the
      same policy without rewriting code.
  type: HowTo
- questions:
  - answer: Yes—use `redactor.LoadPolicy("policy.xml")` to import a previously saved
      policy.
    question: Can I load an existing XML policy instead of building one programmatically?
  - answer: 'Absolutely. Pass the password to the `Redactor` constructor: `new Redactor(sourceFile,
      "password")`.'
    question: Does GroupDocs.Redaction support password‑protected PDFs?
  - answer: The SDK provides `ImageRedaction` and `MetadataRedaction` classes for
      those scenarios.
    question: Is it possible to redact images or metadata?
  - answer: Process them in chunks or use the streaming API to reduce memory footprint;
      the engine can handle files up to 2 GB without loading the whole file into RAM.
    question: How do I handle large documents (hundreds of MB)?
  - answer: A paid license is required for production deployments; a trial license
      is fine for development and testing.
    question: What licensing model is required for commercial use?
  type: FAQPage
tags:
- redact sensitive data
- groupdocs redaction
- .net document security
- xml policy
- document redaction
title: How to redact sensitive data using GroupDocs.Redaction .NET
type: docs
url: /net/advanced-redaction/groupdocs-redaction-net-create-save-policy/
weight: 1
---

# How to redact sensitive data using GroupDocs.Redaction .NET

Protecting confidential information inside contracts, financial statements, or patient records is a non‑negotiable requirement for modern applications. In this guide you’ll learn **how to redact sensitive data** with GroupDocs.Redaction for .NET, from installing the SDK to defining reusable XML policies that can be applied across any document type.

## Quick answers
- **What does “create redaction policy” mean?** It’s the process of defining rules (text, regex, images, etc.) that tell GroupDocs.Redaction how to hide or replace confidential content.  
- **Which library do I need?** GroupDocs.Redaction for .NET, available via NuGet.  
- **Do I need a license?** A free trial works for development; a permanent license is required for production.  
- **Can I reuse the policy?** Yes—once saved as XML you can load it later and apply it to any document.  
- **What .NET versions are supported?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## What is a redaction policy?

A redaction policy is a collection of rules that specify *what* should be removed or replaced and *how* the replacement should look. By creating a policy once, you can apply consistent security standards to every document processed by your application.

## How does a redaction policy work?

Load a document with the `Redactor` engine, attach one or more redaction rules, and then invoke `Apply`. The engine scans the document, masks the matched content, and optionally outputs a new file. The same set of rules can be exported to XML, allowing you to reuse the policy without recompiling code.

## Why use GroupDocs.Redaction to create a redaction policy?

GroupDocs.Redaction provides a comprehensive set of features that simplify the creation, management, and execution of redaction policies, ensuring consistent data protection across diverse document types while delivering high performance and easy integration into existing .NET applications for teams and organizations.

- **Broad format support** – the SDK handles 30+ file types, including PDF, DOCX, XLSX, PPTX, and image formats, and can process files up to 2 GB without loading the entire file into memory.  
- **Programmatic precision** – define exact phrases, regular expressions, or custom logic to target only the data you need to hide.  
- **Reusable XML policies** – export your rules once and share them across teams, services, or micro‑services.  
- **Performance‑optimized engine** – the library processes multi‑hundred‑page documents in under a second on typical server hardware, making it suitable for high‑throughput pipelines.

## Prerequisites
- GroupDocs.Redaction library compatible with your .NET runtime.  
- Visual Studio, VS Code, or any IDE that supports C#.  
- Basic familiarity with C# and .NET project structure.

## Setting up GroupDocs.Redaction for .NET

First, add the library to your project.

**Using .NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Using Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```  

Or search for “GroupDocs.Redaction” in the NuGet Package Manager UI and install it from there.

### License acquisition
- Start with a **free trial** to explore the features.  
- Request a **temporary license** for extended testing, then purchase a full license for production use.

### Basic initialization
Add the namespace to your source file:

The `Redactor` class is the core engine that loads a document and applies redaction rules.  
```csharp
using GroupDocs.Redaction;
```  

The `Redactor` class is GroupDocs.Redaction's core engine that loads a document and applies redaction rules.

## How to create a redaction policy step by step

Below is a complete walkthrough that demonstrates how to programmatically build a redaction policy, configure its rules, apply them to a document, and finally persist the policy as an XML file for future reuse, ensuring consistent redaction across multiple projects and document types.

### Step 1: prepare your document directory
```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
```  
*Replace `"YOUR_DOCUMENT_DIRECTORY"` with the folder that holds the documents you want to protect.*

### Step 2: load the document
```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // Further code will go here
}
```  
The `Redactor` object opens the file and manages its lifecycle.

### Step 3: define the redactions
ExactPhraseRedaction defines a rule that replaces a specific phrase, while `RegexRedaction` uses a regular expression to match patterns.  
```csharp
var redactions = new List<Redaction>
{
    new ExactPhraseRedaction("Sensitive Phrase", new ReplacementOptions("[REDACTED]")),
    new RegexRedaction(@"\d{4}-\d{2}-\d{2}", new ReplacementOptions("[DATE REDACTED]"))
};
```  
Here we create two rules:  
1. **ExactPhraseRedaction** – replaces a known phrase with “[REDACTED]”.  
2. **RegexRedaction** – finds dates in `YYYY‑MM‑DD` format and replaces them with “[DATE REDACTED]”.

### Step 4: apply the redactions
```csharp
redactor.Apply(redactions);
```  
All defined rules are executed against the opened document in one pass.

### Step 5: save the policy as an XML file
```csharp
string policyFile = "policy.xml";
redactor.SavePolicy(policyFile, new SaveOptions());
```  
The XML file stores the redaction definitions, allowing you to reuse the same policy without rewriting code.

## Practical applications

- **Legal firms** can redact case numbers and client names before sharing drafts.  
- **Finance departments** mask account numbers or transaction dates in reports.  
- **Healthcare providers** ensure HIPAA compliance by removing patient identifiers.  

## Performance tips

- Open **one document at a time** to keep memory usage low.  
- Write **efficient regular expressions**; avoid overly broad patterns that increase processing time.  
- Keep the library **up‑to‑date** to benefit from performance improvements and new redaction types.

## Common issues and solutions

| Issue | Why it happens | How to fix |
|-------|----------------|------------|
| **IO exception when preparing the directory** | Wrong path or missing write permissions | Verify the folder exists and the application has read/write rights. |
| **Regex does not match expected text** | Pattern is too strict or missing escape characters | Test the regex with an online tester; adjust quantifiers or escape special characters. |
| **Policy file not created** | `SavePolicy` called before applying redactions or with an invalid path | Ensure the output directory is writable and call `SavePolicy` after `Apply`. |

## Frequently asked questions

**Q: Can I load an existing XML policy instead of building one programmatically?**  
A: Yes—use `redactor.LoadPolicy("policy.xml")` to import a previously saved policy.

**Q: Does GroupDocs.Redaction support password‑protected PDFs?**  
A: Absolutely. Pass the password to the `Redactor` constructor: `new Redactor(sourceFile, "password")`.

**Q: Is it possible to redact images or metadata?**  
A: The SDK provides `ImageRedaction` and `MetadataRedaction` classes for those scenarios.

**Q: How do I handle large documents (hundreds of MB)?**  
A: Process them in chunks or use the streaming API to reduce memory footprint; the engine can handle files up to 2 GB without loading the whole file into RAM.

**Q: What licensing model is required for commercial use?**  
A: A paid license is required for production deployments; a trial license is fine for development and testing.

## Conclusion

You now have a complete, reusable **redaction policy** that you can apply to any document with GroupDocs.Redaction for .NET. By exporting the policy to XML, you simplify future updates and ensure consistent data protection across your organization.

### Next steps
- Experiment with additional redaction types such as `ImageRedaction` or `MetadataRedaction`.  
- Integrate the policy loading logic into your document‑management workflow for automated redaction.  
- Explore the **GroupDocs.Redaction** API reference for advanced customization.

---

**Last Updated:** 2026-10-06  
**Tested With:** GroupDocs.Redaction 5.8 for .NET  
**Author:** GroupDocs  

**Resources**  
- [Documentation](https://docs.groupdocs.com/redaction/net/)  
- [API Reference](https://reference.groupdocs.com/redaction/net)  
- [Download](https://releases.groupdocs.com/redaction/net/)  
- [Free Support Forum](https://forum.groupdocs.com/c/redaction/33)  
- [Temporary License Application](https://purchase.groupdocs.com/temporary-license/)

## Related Tutorials

- [Redact Sensitive Data with GroupDocs.Redaction .NET (C#)](/redaction/net/advanced-redaction/groupdocs-redaction-net-implement-iredactioncallback-csharp/)
- [Implement Document Redaction Using GroupDocs.Redaction .NET&#58; A Step‑By‑Step Guide](/redaction/net/getting-started/implement-document-redaction-groupdocs-redaction-net/)
- [How to Redact Documents with GroupDocs.Redaction .NET – A Complete Guide](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)