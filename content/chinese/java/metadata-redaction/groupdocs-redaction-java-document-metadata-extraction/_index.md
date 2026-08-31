---
date: '2026-03-22'
description: 学习如何使用 GroupDocs.Redaction for Java 在 Java 中读取文件元数据、获取文件类型以及获取页数。一步一步的指南，附代码示例。
keywords:
- GroupDocs.Redaction Java
- document metadata extraction
- Java stream APIs
title: java读取文件元数据 – 使用GroupDocs.Redaction获取文件类型
type: docs
url: /zh/java/metadata-redaction/groupdocs-redaction-java-document-metadata-extraction/
weight: 1
---

# java read file metadata – 使用 GroupDocs.Redaction 在 Java 中获取文件类型

在现代 Java 应用程序中，**java read file metadata** 需要快速完成——尤其是文件类型、页数、大小以及任何自定义属性——这对于构建可靠的文档管理或数据分析流水线至关重要。本教程将指导您使用 GroupDocs.Redaction 读取这些属性，解释 **how to get file type java**，并展示如何以简洁、流式友好的方式 **java get page count** 和 **read file size java**。

## 快速答案
- **如何在 Java 中获取文档的文件类型？** 使用 `redactor.getDocumentInfo().getFileType()`。  
- **哪个库可以同时处理元数据提取和脱敏？** GroupDocs.Redaction for Java。  
- **开发时是否需要许可证？** 免费试用可用于评估；生产环境需要正式许可证。  
- **我还能获取页数吗？** 可以，调用 `IDocumentInfo` 对象的 `getPageCount()` 方法。  
- **此方法是否兼容 Java 8+？** 完全兼容——GroupDocs.Redaction 支持 Java 8 及更高版本。

## 如何使用 GroupDocs.Redaction 读取文件元数据
了解 **java read file metadata** 的步骤有助于您决定在应用程序中何处放置逻辑——无论是用于验证上传的微服务，还是用于索引大型文档集合的批处理作业。

### 什么是 “get file type java”，以及它为何重要？
当您对文档调用 `getFileType()` 时，库会检查文件头并返回一个友好的枚举（例如 **DOCX**、**PDF**、**XLSX**）。了解确切的类型可以让您将文件路由到正确的处理流水线、执行安全策略，或仅仅向终端用户显示准确的信息。

### 为什么在 java read document properties 时使用 GroupDocs.Redaction？
- **一站式解决方案：** 脱敏、元数据提取和格式转换都在同一个 API 下。  
- **流式友好：** 直接使用 `InputStream`，因此可以处理来自磁盘、网络或云存储的文件，而无需临时文件。  
- **性能优化：** 内存占用最小，关闭 `Redactor` 实例时会自动清理资源。  

## 前置条件
1. **GroupDocs.Redaction for Java**（版本 24.9 或更高）。  
2. JDK 8 或更高。  
3. 基本的 Java 知识以及对文件 I/O 流的熟悉。  

## 为 Java 设置 GroupDocs.Redaction

### Maven 安装
Add the repository and dependency to your `pom.xml`:

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
或者直接从 [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) 下载最新版本。

### 许可证获取
- **免费试用：** 适合评估 API。  
- **临时许可证：** 官方网站提供，用于短期测试。  
- **正式许可证：** 当您准备投入生产使用时购买。  

## 基本初始化（Java）

```java
import com.groupdocs.redaction.Redactor;
import java.io.FileInputStream;

FileInputStream stream = new FileInputStream("path/to/your/Sample.docx");
final Redactor redactor = new Redactor(stream);
// Proceed with document operations...
```

## 步骤指南：检索元数据

### 步骤 1：打开文件流
Start by creating an `InputStream` for the target document:

```java
FileInputStream stream = new FileInputStream("YOUR_DOCUMENT_DIRECTORY/Sample.docx");
```

### 步骤 2：初始化 Redactor
Create a `Redactor` instance using the stream. This object gives you access to the document’s metadata.

```java
final Redactor redactor = new Redactor(stream);
```

### 步骤 3：检索文档信息
Call `getDocumentInfo()` to obtain an `IDocumentInfo` object. In this place you can **java read file metadata**, **java get document type**, **java get page count**, and even **read file size java**.

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

> **技巧提示：** 仅在需要控制台输出时取消注释 `System.out.println` 行；在生产环境保持注释可降低 I/O 开销。

### 步骤 4：关闭资源
始终在 `finally` 块中关闭 `Redactor` 和流（如示例所示），以避免内存泄漏，尤其是在并行处理大量文档时。

## 实际应用（java read document properties）

1. **文档管理系统：** 按类型、页数和大小自动编目文件。  
2. **数据分析流水线：** 将元数据输入仪表板进行报告。  
3. **内容创作平台：** 在下载或预览前向终端用户展示文件详情。  

## 性能考虑
- 对大文件使用 **缓冲流**（`BufferedInputStream`）以提升 I/O 速度。  
- 及时释放资源（对 `Redactor` 和流都调用 `close()`）。  
- 批量处理时，考虑在每个线程中复用单个 `Redactor` 实例，以减少对象创建开销。

## 常见问题与解决方案

| 症状 | 可能原因 | 解决方案 |
|------|----------|----------|
| `FileNotFoundException` | 路径不正确或文件缺失 | 验证绝对/相对路径以及文件权限。 |
| `LicenseException` | 未加载有效许可证 | 在创建 `Redactor` 前加载试用或正式许可证。 |
| `OutOfMemoryError` on large PDFs | 未使用缓冲流或同时处理大量文件 | 改用 `BufferedInputStream` 并限制并发线程数。 |

## 常见问答

**问：GroupDocs.Redaction 的用途是什么？**  
**答：** 主要用于脱敏敏感内容，同时提供强大的 API 来 **java read document properties**，例如文件类型和页数。

**问：我可以将 GroupDocs.Redaction 与其他 Java 框架一起使用吗？**  
**答：** 可以，库可无缝集成到 Spring、Jakarta EE，甚至普通的 Java SE 项目中。

**问：如何高效处理超大文档？**  
**答：** 将文件流包装在 `BufferedInputStream` 中，及时关闭资源，并考虑以流式方式处理文件，而不是一次性加载整个文档到内存。

**问：库是否支持非英文文档？**  
**答：** 当然——GroupDocs.Redaction 开箱即支持多种语言和字符集。

**问：提取元数据时常见的陷阱有哪些？**  
**答：** 缺少许可证、文件路径错误以及忘记关闭流是最常见的问题。务必遵循上文展示的资源清理模式。

## 结论
您现在拥有一套完整、可用于生产的 **java read file metadata** 方案，能够读取其他文档属性以及使用 GroupDocs.Redaction 的 **java get page count**。将这些代码片段集成到现有服务中，您即可即时获取系统中每个文档的详细信息。

**后续步骤**  
- 试验 `IDocumentInfo` 暴露的其他元数据字段。  
- 将元数据提取与脱敏工作流结合，实现端到端的文档安全。  
- 探索适用于高并发环境的批处理模式。

**资源**  
- [文档](https://docs.groupdocs.com/redaction/java/)  
- [API 参考](https://reference.groupdocs.com/redaction/java)  
- [下载 GroupDocs.Redaction for Java](https://releases.groupdocs.com/redaction/java/)  
- [GitHub 仓库](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- [免费支持论坛](https://forum.groupdocs.com/c/redaction/33)  
- [临时许可证信息](https://purchase.groupdocs.com/temporary-license/)  

---

**最后更新：** 2026-03-22  
**测试环境：** GroupDocs.Redaction 24.9 for Java  
**作者：** GroupDocs