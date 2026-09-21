---
date: '2026-09-21'
description: 了解如何使用 GroupDocs.Redaction 获取 file type java 并读取 file metadata java。Extract
  page count、file size，并高效地 process streams。
keywords:
- get file type java
- read file metadata java
- java get page count
- read file size java
- metadata extraction java
lastmod: '2026-09-21'
og_description: 使用 GroupDocs.Redaction 快速获取 file type java 并读取 file metadata java。本指南展示了如何
  extract page count、size 等更多信息。
og_image_alt: Guide to extracting file type and metadata in Java with GroupDocs.Redaction
og_title: 使用 GroupDocs.Redaction 获取 file type java 并读取 metadata
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: Learn how to get file type java and read file metadata java using GroupDocs.Redaction.
    Extract page count, file size, and process streams efficiently.
  headline: Get file type java and read metadata with GroupDocs.Redaction
  type: TechArticle
- description: Learn how to get file type java and read file metadata java using GroupDocs.Redaction.
    Extract page count, file size, and process streams efficiently.
  name: Get file type java and read metadata with GroupDocs.Redaction
  steps:
  - name: open a file stream
    text: Start by creating an `InputStream` for the target document. Using a buffered
      stream improves I/O performance for large files.
  - name: initialize the Redactor
    text: Create a `Redactor` instance using the stream. This object gives you access
      to the document’s metadata.
  - name: retrieve document information
    text: '**`IDocumentInfo` provides properties such as file type, page count, size,
      and custom metadata.** > **Pro tip:** Uncomment the `System.out.println` lines
      only when you need console output; keeping them commented in production reduces
      I/O overhead.'
  - name: close resources
    text: Always close the `Redactor` and the stream in a `finally` block (as shown)
      to avoid memory leaks, especially when processing many documents in parallel.
  type: HowTo
- questions:
  - answer: Primarily for redacting sensitive content, it also provides robust APIs
      to **java read document properties** such as file type and page count.
    question: What is GroupDocs.Redaction used for?
  - answer: Yes, the library works seamlessly with Spring, Jakarta EE, and plain Java
      SE projects.
    question: Can I use GroupDocs.Redaction with other Java frameworks?
  - answer: Wrap the file stream in a `BufferedInputStream`, close resources promptly,
      and process files in a streaming fashion rather than loading the entire document
      into memory.
    question: How do I handle very large documents efficiently?
  - answer: Absolutely—GroupDocs.Redaction handles multiple languages and character
      sets out of the box.
    question: Does the library support non‑English documents?
  - answer: Missing licenses, incorrect file paths, and forgetting to close streams
      are the most common. Always follow the resource‑cleanup pattern shown above.
    question: What are typical pitfalls when extracting metadata?
  type: FAQPage
tags:
- get file type
- GroupDocs.Redaction
- Java metadata extraction
- document processing
- Java file handling
title: 使用 GroupDocs.Redaction 获取 file type java 并读取 metadata
type: docs
url: /zh/java/metadata-redaction/groupdocs-redaction-java-document-metadata-extraction/
weight: 1
---

# 获取文件类型 java 并使用 GroupDocs.Redaction 读取元数据

## 快速答案
- **如何在 Java 中获取文档的文件类型？** 调用 `redactor.getDocumentInfo().getFileType()`。  
- **哪个库既能提取元数据又支持脱敏？** GroupDocs.Redaction for Java 在单一 API 中提供这两种功能。  
- **开发是否需要许可证？** 免费试用可用于评估；生产环境需要正式许可证。  
- **我还能获取页数吗？** 可以——在 `IDocumentInfo` 对象上使用 `getPageCount()`。  
- **此方法是否兼容 Java 8+？** 当然——GroupDocs.Redaction 支持 Java 8 及更高版本。

## 什么是 “get file type java” 以及它为何重要？
`getFileType()` 返回一个友好的枚举，标识确切的文档格式（例如 PDF、DOCX、XLSX）。了解精确的类型使您的应用能够自动将文件路由到相应的处理流水线，根据格式强制安全策略，生成正确的缩略图，并在 UI 列表中向最终用户展示准确的信息。

## 为什么在 java 中使用 GroupDocs.Redaction 读取文档属性？
GroupDocs.Redaction 是一个 **一体化解决方案**，在单一、流式友好的 API 下处理脱敏、元数据提取和格式转换。它支持 **45+ 种输入和输出格式**，能够在不将整个文档加载到内存的情况下处理数百页的文件，并在 `Redactor` 实例关闭时自动释放资源。

## 前置条件
- GroupDocs.Redaction for Java（版本 24.9 或更高）。  
- JDK 8 或更高。  
- 基本的 Java 知识以及对文件 I/O 流的熟悉。

## 为 Java 设置 GroupDocs.Redaction

### Maven 安装
将仓库和依赖添加到您的 `pom.xml` 中：

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

### 直接下载
或者，直接从 [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) 下载最新版本。

### 许可证获取
- **免费试用：** 适合评估 API。  
- **临时许可证：** 官方网站提供，适用于短期测试。  
- **正式许可证：** 当您准备投入生产使用时购买。

## 基本初始化（Java）

**`Redactor` 是打开文档流并提供元数据、脱敏和转换功能的核心类。**  

```java
import com.groupdocs.redaction.Redactor;
import java.io.FileInputStream;

FileInputStream stream = new FileInputStream("path/to/your/Sample.docx");
final Redactor redactor = new Redactor(stream);
// Proceed with document operations...
```

## 检索元数据的分步指南

### 步骤 1：打开文件流
首先为目标文档创建一个 `InputStream`。使用缓冲流可以提升大文件的 I/O 性能。

```java
FileInputStream stream = new FileInputStream("YOUR_DOCUMENT_DIRECTORY/Sample.docx");
```

### 步骤 2：初始化 Redactor
使用该流创建 `Redactor` 实例。该对象可让您访问文档的元数据。

```java
final Redactor redactor = new Redactor(stream);
```

### 步骤 3：检索文档信息
**`IDocumentInfo` 提供文件类型、页数、大小和自定义元数据等属性。**  

```java
try {
    IDocumentInfo info = redactor.getDocumentInfo();
    
    // Display document information (uncomment as needed)
    System.out.println("\
File type: " + info.getFileType() +
           "\
Number of pages: " + info.getPageCount() + 
           "\
Document size: " + info.getSize() + " bytes");
} finally {
    redactor.close();
    stream.close();
}
```

> **专业提示：** 仅在需要控制台输出时取消注释 `System.out.println` 行；在生产环境保持注释可降低 I/O 开销。

### 步骤 4：关闭资源
始终在 `finally` 块中关闭 `Redactor` 和流（如示例所示），以避免内存泄漏，尤其是在并行处理大量文档时。

## 实际应用（java 读取文档属性）

1. 文档管理系统：按类型、页数和大小自动编目文件。  
2. 数据分析流水线：将元数据输入仪表盘进行报告。  
3. 内容创作平台：在下载或预览前向最终用户展示文件详情。

## 性能考虑
- 对大文件使用 **缓冲流** (`BufferedInputStream`) 以提升 I/O 速度。  
- 及时释放资源（对 `Redactor` 和流都调用 `close()`）。  
- 批量处理时，考虑在每个线程中复用单个 `Redactor` 实例，以降低对象创建开销。

## 常见问题与解决方案
| 症状 | 可能原因 | 解决方案 |
|---------|--------------|-----|
| `FileNotFoundException` | 路径不正确或文件缺失 | 检查绝对/相对路径及文件权限。 |
| `LicenseException` | 未加载有效许可证 | 在创建 `Redactor` 前加载试用或正式许可证。 |
| `OutOfMemoryError`（大 PDF） | 使用未缓冲的流或同时处理大量文件 | 改用 `BufferedInputStream` 并限制并发线程数。 |

## 常见问答

**Q: GroupDocs.Redaction 的用途是什么？**  
A: 主要用于脱敏敏感内容，同时也提供强大的 API 以 **java 读取文档属性**，如文件类型和页数。

**Q: 我可以将 GroupDocs.Redaction 与其他 Java 框架一起使用吗？**  
A: 可以，库可无缝集成到 Spring、Jakarta EE 和普通 Java SE 项目中。

**Q: 如何高效处理超大文档？**  
A: 将文件流包装在 `BufferedInputStream` 中，及时关闭资源，并以流式方式处理文件，而不是将整个文档加载到内存。

**Q: 该库是否支持非英文文档？**  
A: 当然——GroupDocs.Redaction 开箱即支持多语言和字符集。

**Q: 提取元数据时常见的陷阱有哪些？**  
A: 缺少许可证、文件路径错误以及忘记关闭流是最常见的问题。始终遵循上面展示的资源清理模式。

## 结论
您现在拥有使用 GroupDocs.Redaction 完整的、可投入生产的 **get file type java**、读取其他文档属性以及 **java get page count** 的方案。将这些代码片段集成到现有服务中，您即可即时获取系统中每个流转文档的可视化信息。

**后续步骤**  
- 探索 `IDocumentInfo` 暴露的其他字段。  
- 将元数据提取与脱敏工作流结合，实现端到端的文档安全。  
- 研究高吞吐量环境的批处理模式。

**资源**  
- [文档](https://docs.groupdocs.com/redaction/java/)  
- [API 参考](https://reference.groupdocs.com/redaction/java)  
- [下载 GroupDocs.Redaction for Java](https://releases.groupdocs.com/redaction/java/)  
- [GitHub 仓库](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- [免费支持论坛](https://forum.groupdocs.com/c/redaction/33)  
- [临时许可证信息](https://purchase.groupdocs.com/temporary-license/)  

---

**最后更新：** 2026-09-21  
**测试环境：** GroupDocs.Redaction 24.9 for Java  
**作者：** GroupDocs

## 相关教程

- [使用 Groupdocs Redaction Java 检索文档信息](/redaction/java/document-information/retrieve-document-info-using-groupdocs-redaction-java/)
- [生成预览和文档页数 – GroupDocs Java](/redaction/java/document-information/)
- [如何使用 GroupDocs.Redaction 在 Java 中脱敏元数据](/redaction/java/metadata-redaction/)