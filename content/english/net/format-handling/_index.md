---
date: 2026-07-15
description: Learn how to create custom redaction handler and add new file format
  support using GroupDocs.Redaction for .NET.
images:
- /net/format-handling/og-image.png
keywords:
- create custom redaction handler
- add new file format
- GroupDocs.Redaction format handling
lastmod: 2026-07-15
og_description: Create custom redaction handler and add new file format support with
  GroupDocs.Redaction for .NET. Discover step‑by‑step guides for extending format
  handling.
og_image_alt: Guide to creating a custom redaction handler in GroupDocs.Redaction
  for .NET
og_title: Create Custom Redaction Handler – GroupDocs.Redaction .NET
schemas:
- author: GroupDocs
  dateModified: '2026-07-15'
  description: Learn how to create custom redaction handler and add new file format
    support using GroupDocs.Redaction for .NET.
  headline: Create Custom Redaction Handler in GroupDocs.Redaction .NET
  type: TechArticle
tags:
- redaction handler
- GroupDocs.Redaction
- .NET document processing
- custom format extension
title: Create Custom Redaction Handler in GroupDocs.Redaction .NET
type: docs
url: /net/format-handling/
weight: 14
---

# Create Custom Redaction Handler in GroupDocs.Redaction .NET

Extend GroupDocs.Redaction capabilities with our format handling tutorials for .NET developers. In this hub you’ll learn how to **create custom redaction handler** and **add new file format** support, work with plain‑text documents, and programmatically handle diverse document types. These guides include ready‑to‑run C# examples, so you can quickly broaden the range of files your application can secure.

## Quick Overview

- **What you’ll gain:** Ability to redact custom content types and support additional file extensions without waiting for product updates.  
- **Who it’s for:** .NET developers building document‑centric solutions that require strict privacy controls.  
- **Prerequisites:** .NET 6+ (or .NET Framework 4.7.2+), a valid GroupDocs.Redaction license, and basic C# knowledge.  

## What is a custom redaction handler?

A **custom redaction handler** is a user‑defined component that tells GroupDocs.Redaction how to locate, interpret, and redact content that isn’t covered by the built‑in patterns. By implementing this handler you gain full control over proprietary data formats or unique business identifiers.

## How to create custom redaction handler?

**IRedactionHandler** is an interface that defines the contract for custom redaction logic.  
**Redactor** is the core class that manages redaction operations.  
**AddHandler** registers a custom handler with the Redactor instance.  
**Redact** executes the redaction based on the configured handlers.  

Load the Redaction engine, register your handler, and invoke the redaction process – all in three concise steps. First, implement the `IRedactionHandler` interface with logic that scans the document for your custom tokens. Then, add the handler to the `Redactor` instance via `AddHandler`. Finally, call `Redact` to apply the changes. This pattern works for PDFs, images, and any supported format, allowing you to protect data that standard patterns miss.

## How to add new file format?

**SupportedFormats** is a collection that holds the file extensions recognized by the Redaction engine. Register a new file extension with the Redaction engine by extending the `SupportedFormats` collection. Provide a parser that converts the incoming file into a format GroupDocs.Redaction can process, then map the extension to your parser. Once registered, the engine treats the new format like any native type, enabling seamless redaction across the board.

## Why use GroupDocs.Redaction for custom format handling?

GroupDocs.Redaction supports **70+ input and output formats** and can process files up to **2 GB** without loading the entire document into memory, delivering high‑throughput redaction in enterprise environments. Its extensible architecture lets you plug in custom handlers in under 30 minutes, reducing development time and eliminating the need for third‑party preprocessing tools.

## Available Tutorials

### [Extend File Types in GroupDocs.Redaction .NET: A Step‑By‑Step Guide to Custom Extensions](./extend-groupdocs-redaction-net-custom-extensions/)
Learn how to extend supported file types with custom extensions using GroupDocs.Redaction for .NET, ensuring secure document redaction across diverse formats.

### [Implementing Supported File Format Listing with GroupDocs.Redaction .NET](./groupdocs-redaction-net-supported-formats-listing/)
Learn how to use GroupDocs.Redaction .NET to list supported file formats, streamline document management systems, and optimize performance.

## Additional Resources

- [GroupDocs.Redaction for Net Documentation](https://docs.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction for Net API Reference](https://reference.groupdocs.com/redaction/net/)
- [Download GroupDocs.Redaction for Net](https://releases.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction Forum](https://forum.groupdocs.com/c/redaction/33)
- [Free Support](https://forum.groupdocs.com/)
- [Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Last Updated:** 2026-07-15  
**Tested With:** GroupDocs.Redaction 23.12 for .NET  
**Author:** GroupDocs

## Related Tutorials

- [Extend File Types in GroupDocs.Redaction .NET: A Step-by-Step Guide to Custom Extensions](/redaction/net/format-handling/extend-groupdocs-redaction-net-custom-extensions/)
- [Implementing Supported File Format Listing with GroupDocs.Redaction .NET](/redaction/net/format-handling/groupdocs-redaction-net-supported-formats-listing/)
- [Format Handling Tutorials for GroupDocs.Redaction .NET](/redaction/net/format-handling/)