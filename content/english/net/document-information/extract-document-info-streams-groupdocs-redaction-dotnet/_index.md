---
title: "How to Extract Metadata from Document Streams Using GroupDocs.Redaction .NET"
description: "Learn how to extract metadata from document streams using GroupDocs.Redaction for .NET, covering setup, code examples, and practical applications."
date: "2026-06-11"
weight: 1
url: "/net/document-information/extract-document-info-streams-groupdocs-redaction-dotnet/"
keywords:
  - how to extract metadata
  - extract document metadata
  - extract pdf metadata
  - retrieve document size
  - prepare output directory
type: docs
schemas:
- type: TechArticle
  headline: How to Extract Metadata from Document Streams Using GroupDocs.Redaction
    .NET
  description: Learn how to extract metadata from document streams using GroupDocs.Redaction
    for .NET, covering setup, code examples, and practical applications.
  dateModified: '2026-06-11'
  author: GroupDocs
- type: HowTo
  name: How to Extract Metadata from Document Streams Using GroupDocs.Redaction .NET
  description: Learn how to extract metadata from document streams using GroupDocs.Redaction
    for .NET, covering setup, code examples, and practical applications.
  steps:
  - name: Prepare the source file path
    text: First, ensure the source file exists and that the output folder is ready.
      The helper method below checks the output directory and creates it if needed.
      *Why?* This guarantees a valid path for subsequent file operations and prevents
      `DirectoryNotFoundException`.
  - name: Open the document stream
    text: Using `File.OpenRead()` opens the file as a **read‑only stream**, which
      keeps memory usage low even for gigabyte‑size files. *Why?* Streams enable on‑the‑fly
      processing, allowing you to work with portions of the file rather than the whole
      document.
  - name: Initialise the Redactor with the document stream
    text: '`Redactor` is the primary API object that gives you access to document‑level
      operations, including metadata extraction. `Redactor` represents a single document
      loaded from a stream and exposes methods such as `GetDocumentInfo()` for quick
      property retrieval. *Why?* Instantiating `Redactor` with a st'
  - name: Retrieve document metadata
    text: Calling `GetDocumentInfo()` returns a `DocumentInfo` object that holds the
      file format, page count, and file size. `GetDocumentInfo()` extracts core properties
      (format, page count, size) in a single call, eliminating the need for separate
      parsers. *Why?* This step consolidates all essential metadata
- type: FAQPage
  questions:
  - question: What is the primary use case for GroupDocs.Redaction’s metadata extraction?
    answer: It enables fast, memory‑efficient retrieval of document properties for
      indexing, compliance checks, and automated routing without opening the full
      file.
  - question: Can I extract metadata from password‑protected files?
    answer: Yes, provide the password when constructing the `Redactor` object; the
      API will decrypt the stream internally.
  - question: Does the library support non‑PDF formats like DOCX or XLSX?
    answer: Absolutely – GroupDocs.Redaction handles over 30 formats, including PDF,
      DOCX, XLSX, PPTX, and common image types.
  - question: How large a document can I process with streams?
    answer: Streams allow processing of files up to **2 GB** while keeping memory
      consumption under **50 MB**, thanks to on‑the‑fly reading.
  - question: Where can I get help if I run into issues?
    answer: Visit the [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33)
      for community support, or consult the official documentation for troubleshooting
      tips.
---
# How to Extract Metadata from Document Streams Using GroupDocs.Redaction .NET

Are you tired of manually extracting document information or dealing with large files that slow down your workflow? **How to extract metadata** quickly is a common challenge, and the GroupDocs.Redaction library for .NET offers a fast, memory‑efficient way to retrieve document details directly from streams. In this tutorial, you’ll learn how to set up the library, pull file type, page count, and size from a stream, and prepare an output folder for further processing.

## Quick Answers
- **What does “extract metadata” mean?** It means reading properties like file type, page count, and size without opening the full document in memory.  
- **Which library handles this?** GroupDocs.Redaction for .NET provides a native API for stream‑based metadata extraction.  
- **Do I need a license?** A free trial works for development; a commercial license is required for production.  
- **Can I process PDFs larger than 1 GB?** Yes – streams let you handle files up to 2 GB without loading the whole file.  
- **What .NET versions are supported?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5+, and .NET 6+.

## What is metadata extraction from streams?
Metadata extraction from streams is the process of reading document properties directly from a `Stream` object, avoiding full file loading and thus saving memory and CPU time. This technique is ideal for batch processing or cloud‑based services where resources are limited.

## Why use GroupDocs.Redaction for metadata extraction?
GroupDocs.Redaction supports **30+ file formats** (including PDF, DOCX, XLSX, PPTX, and image types) and can process documents up to **2 GB** in size while keeping memory usage under **50 MB**. Its `Redactor` API provides a single call to retrieve all key document information, eliminating the need for multiple parsers.

## Prerequisites

- **GroupDocs.Redaction for .NET** (latest version)  
- **.NET Framework** 4.5+ **or** **.NET Core/5+/6+**  
- Basic C# knowledge and familiarity with file I/O  
- Visual Studio 2019 or later

## How do I set up GroupDocs.Redaction for .NET?
To begin using GroupDocs.Redaction, you first need to add the library to your project. This can be done via the .NET CLI, the Visual Studio Package Manager, or the NuGet UI. Choose the approach that fits your workflow; the CLI is ideal for scriptable builds, while the UI offers a graphical way to browse versions and dependencies.

**.NET CLI**
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI:**
- Open NuGet Package Manager in Visual Studio.  
- Search for **"GroupDocs.Redaction"** and install the latest version.

### License Acquisition Steps
1. **Free Trial:** Download a trial license to explore all features without restrictions.  
2. **Temporary License:** Request a temporary license from [GroupDocs](https://purchase.groupdocs.com/temporary-license/) for extended testing.  
3. **Purchase:** When ready for production, buy a commercial license.  

For more information, visit the [GroupDocs website](https://purchase.groupdocs.com/temporary-license/).

### Basic Initialization and Setup
The `Redactor` class is the entry point for all operations, including metadata extraction.

`Redactor` is the core class that represents a document instance and provides methods for redaction, information retrieval, and file manipulation. Once installed, you can create a `Redactor` object as shown below:

```csharp
using (Redactor redactor = new Redactor("your-document-path"))
{
    // Use the redactor here
}
```

Now that the library is ready, let’s dive into the implementation details.

## How to extract metadata from a document stream?
Load the document as a **read‑only stream**, initialise the `Redactor`, and call `GetDocumentInfo()` to retrieve the metadata in a single step. This approach avoids loading the entire file into memory, which is crucial for large PDFs or multi‑hundred‑page Office documents.

**Direct answer:** Open the file with `File.OpenRead()`, pass the stream to `new Redactor(stream)`, then call `redactor.GetDocumentInfo()` – the method returns an object containing file type, page count, and size in just three lines of code.

### Step 1: Prepare the source file path
First, ensure the source file exists and that the output folder is ready. The helper method below checks the output directory and creates it if needed.

```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

*Why?* This guarantees a valid path for subsequent file operations and prevents `DirectoryNotFoundException`.

### Step 2: Open the document stream
Using `File.OpenRead()` opens the file as a **read‑only stream**, which keeps memory usage low even for gigabyte‑size files.

```csharp
using (Stream documentStream = File.OpenRead(sourceFile))
{
    // Proceed to initialize Redactor
}
```

*Why?* Streams enable on‑the‑fly processing, allowing you to work with portions of the file rather than the whole document.

### Step 3: Initialise the Redactor with the document stream
`Redactor` is the primary API object that gives you access to document‑level operations, including metadata extraction.

`Redactor` represents a single document loaded from a stream and exposes methods such as `GetDocumentInfo()` for quick property retrieval.  

```csharp
using (Redactor redactor = new Redactor(documentStream))
{
    // Extract document info next
}
```

*Why?* Instantiating `Redactor` with a stream ties the object to the underlying file without fully loading it.

### Step 4: Retrieve document metadata
Calling `GetDocumentInfo()` returns a `DocumentInfo` object that holds the file format, page count, and file size.

`GetDocumentInfo()` extracts core properties (format, page count, size) in a single call, eliminating the need for separate parsers.  

```csharp
IDocumentInfo info = redactor.GetDocumentInfo();
string fileInfo = $"\nFile type: {info.FileType}\nNumber of pages: {info.PageCount}\nDocument size: {info.Size} bytes";
Console.WriteLine(fileInfo);
```

*Why?* This step consolidates all essential metadata, making it easy to log, filter, or route documents based on their characteristics.

## How to prepare an output directory for processed files?
Before writing any processed files, ensure that the destination folder exists and is writable. By programmatically checking the path and creating it when missing, you avoid common runtime exceptions such as `DirectoryNotFoundException` or permission errors. This simple step also makes your code portable across environments, whether running locally, on a server, or within a container.

**Direct answer:** Use `Directory.Exists()` to check for the folder and `Directory.CreateDirectory()` to create it if it does not exist – this single‑line check guarantees a valid path before any write operation.

### Implement a helper method
The method below encapsulates the check‑and‑create logic, returning the verified path for later use.

```csharp
public static class Utils
{
    public static string PrepareOutputDirectory(string sampleDocPath)
    {
        string directory = Path.GetDirectoryName(sampleDocPath);
        
        if (!Directory.Exists(directory))
        {
            Directory.CreateDirectory(directory);
        }
        
        return Path.Combine(directory, "SAMPLE_DOCX.docx");
    }
}
```

*Why?* Centralising this logic reduces duplication and makes the codebase easier to maintain.

## Common Issues and Solutions
- **Permission errors:** Ensure the application runs under an account with write access to the target folder.  
- **Invalid paths:** Double‑check path separators (`\\` on Windows, `/` on Linux/macOS) to avoid `DirectoryNotFoundException`.  
- **Large file handling:** Dispose of streams promptly (`using` statements) to free OS handles and prevent leaks.

## Practical Applications
1. **Automated Document Ingestion:** Extract metadata on upload, then store it in a database for fast search and compliance reporting.  
2. **Legal & Compliance Audits:** Pull page counts and file types to verify that documents meet regulatory standards before archiving.  
3. **Enterprise Content Management:** Use metadata to auto‑categorise files into folders, improving organization and retrieval speed.

## Performance Considerations
- **Memory Management:** Always wrap streams in `using` blocks so they are disposed automatically.  
- **Batch Processing:** Process documents in groups of 10‑20 to balance throughput and memory usage, especially on limited‑resource servers.  
- **Parallelism:** Leverage `Parallel.ForEach` for independent files, but monitor CPU and I/O to avoid contention.

## Conclusion
You now have a complete, production‑ready guide on **how to extract metadata** from document streams using GroupDocs.Redaction for .NET. By following the steps above, you can efficiently retrieve file type, page count, and size while keeping memory usage low and handling large files gracefully.

**Next Steps**
- Review the full API reference in the [documentation](https://docs.groupdocs.com/redaction/net/).  
- Dive deeper into the [GroupDocs Redaction .NET Documentation](https://docs.groupdocs.com/redaction/net/) to explore redaction, watermarking, and OCR features.  
- Experiment with different file formats (PDF, DOCX, XLSX) to see how metadata varies across types.  
- Integrate the extracted metadata into your existing document management or search solution.

## Frequently Asked Questions

**Q: What is the primary use case for GroupDocs.Redaction’s metadata extraction?**  
A: It enables fast, memory‑efficient retrieval of document properties for indexing, compliance checks, and automated routing without opening the full file.

**Q: Can I extract metadata from password‑protected files?**  
A: Yes, provide the password when constructing the `Redactor` object; the API will decrypt the stream internally.

**Q: Does the library support non‑PDF formats like DOCX or XLSX?**  
A: Absolutely – GroupDocs.Redaction handles over 30 formats, including PDF, DOCX, XLSX, PPTX, and common image types.

**Q: How large a document can I process with streams?**  
A: Streams allow processing of files up to **2 GB** while keeping memory consumption under **50 MB**, thanks to on‑the‑fly reading.

**Q: Where can I get help if I run into issues?**  
A: Visit the [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33) for community support, or consult the official documentation for troubleshooting tips.

---

**Last Updated:** 2026-06-11  
**Tested With:** GroupDocs.Redaction 23.12 for .NET  
**Author:** GroupDocs  

**Resources**  
- **Documentation:** [GroupDocs Redaction .NET Documentation](https://docs.groupdocs.com/redaction/net/)  
- **API Reference:** [GroupDocs Redaction API Reference](https://reference.groupdocs.com/redaction/net)  
- **Download:** [Latest GroupDocs Releases](https://releases.groupdocs.com/redaction/net)

## Related Tutorials

- [Master Document Metadata Retrieval with GroupDocs.Redaction .NET API](/redaction/net/document-information/groupdocs-redaction-net-document-metadata-retrieval/)
- [How to Redact Document Metadata Using GroupDocs.Redaction for .NET - A Comprehensive Guide](/redaction/net/metadata-redaction/redact-metadata-groupdocs-redaction-net/)
- [Secure Document Redaction in .NET Using Streams: A Guide for GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)
