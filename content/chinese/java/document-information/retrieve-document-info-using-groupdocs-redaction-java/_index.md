---
date: '2025-12-20'
description: 了解如何使用 GroupDocs.Redaction for Java 获取文件类型、获取文档大小以及检索 PDF 元数据。立即提升您的
  Java 应用的文档处理能力。
keywords:
- get file type java
- get document size java
- retrieve pdf metadata java
- get page count java
- GroupDocs Redaction library setup Java
title: 如何在 Java 中使用 GroupDocs.Redaction 获取文件类型
type: docs
url: /zh/java/document-information/retrieve-document-info-using-groupdocs-redaction-java/
weight: 1
---

# 如何使用 GroupDocs.Redaction 获取文件类型（Java）

检索文档的关键细节——如 **文件类型**、页数和大小——是构建以文档为中心的 Java 应用程序时的常见需求。在本教程中，你将学习如何 **获取文件类型（Java）**，以及如何 **获取文档大小（Java）**、**获取页数（Java）**，甚至 **检索 PDF 元数据（Java）**，全部使用 GroupDocs.Redaction 库。

## 快速回答
- **哪个方法返回文件类型？** `IDocumentInfo.getFileType()`
- **如何获取页数？** `IDocumentInfo.getPageCount()`
- **哪个调用返回文档大小（字节）？** `IDocumentInfo.getSize()`
- **运行示例是否需要许可证？** 试用或临时许可证即可用于评估。
- **需要哪个 Java 版本？** Java 8 或更高。

## 什么是 “get file type java”？
该短语指在 Java 中以编程方式从文档中提取文件格式（例如 DOCX、PDF）。GroupDocs.Redaction 通过 `IDocumentInfo` 接口公开此信息。

## 为什么使用 GroupDocs.Redaction 提取元数据？
- **广泛的格式支持：** 支持 PDF、DOCX、XLSX、PPTX 等多种格式。  
- **简洁的 API：** 一行调用即可返回文件类型、页数和大小。  
- **性能优化：** 仅加载所需的元数据，保持内存占用低。

## 前置条件
- 已安装 Java 8 或更高版本。  
- 支持 Maven 的 IDE（IntelliJ IDEA、Eclipse 等）。  
- 拥有 GroupDocs.Redaction 许可证（免费试用或临时许可证）。

## 为 Java 设置 GroupDocs.Redaction

要在 Java 项目中使用 GroupDocs.Redaction 库，请按照以下安装步骤操作：

**Maven 安装**

在 `pom.xml` 文件中添加以下仓库和依赖：

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

**直接下载**

或者，从 [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) 下载最新版本。

### 许可证获取
- **免费试用：** 开始免费试用以评估库。  
- **临时许可证：** 获取临时许可证以进行更长时间的评估。  
- **购买：** 如符合需求，可考虑购买正式许可证。

安装完成后，初始化并设置 GroupDocs.Redaction：

```java
import com.groupdocs.redaction.Redactor;

// Initialize Redactor with the path to your document
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

## 如何获取文件类型（Java）、文档大小（Java）和页数（Java）

库准备就绪后，下面逐步演示如何检索所需信息。

### 步骤 1：导入必要的类

在 Java 文件顶部确保导入所需的类：

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.domain.IDocumentInfo;
```

### 步骤 2：初始化 Redactor

创建 `Redactor` 实例，并指定文档路径。该对象使你能够与文件交互并提取元数据。

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
try {
    // Code for retrieving information will go here.
} finally {
    redactor.close();
}
```

### 步骤 3：检索并显示文档信息

调用 `getDocumentInfo()` 获取 `IDocumentInfo` 对象。通过该对象即可 **获取文件类型（Java）**、**获取文档大小（Java）** 和 **获取页数（Java）**，一次调用即可完成。

```java
// Retrieve document information
IDocumentInfo info = redactor.getDocumentInfo();

// Output document type, page count, and size in bytes
System.out.println("File Type: " + info.getFileType());
System.out.println("Page Count: " + info.getPageCount());
System.out.println("Size (Bytes): " + info.getSize());
```

这三个 `System.out.println` 语句分别输出文件类型、页数以及字节大小——正是后续处理所需的全部信息。

## 如何检索 PDF 元数据（Java）

如果源文档是 PDF，`IDocumentInfo` 的相同调用会返回 PDF 特有的元数据（例如 PDF 版本、加密状态）。无需额外代码，只需使用相同的 `getDocumentInfo()` 方法即可。

## 常见问题及解决方案
- **文件未找到：** 检查传递给 `Redactor` 的绝对或相对路径是否正确。  
- **不受支持的格式：** 确认文档扩展名受 GroupDocs.Redaction 支持。  
- **许可证错误：** 使用有效的试用或正式许可证，否则 API 将抛出许可证异常。  

## 实际应用

了解如何 **获取文件类型（Java）** 以及相关元数据，可打开以下场景的大门：

1. **文档管理系统：** 在存储前根据类型或大小自动分类文件。  
2. **内容处理流水线：** 根据页数选择不同的处理策略。  
3. **数字资产库：** 为用户提供文档属性的快速预览。

## 性能考虑

处理大批量文件时：

- 在 `try‑with‑resources` 块中打开每个文档，以确保及时释放文件句柄。  
- 仅缓存所需的元数据；除非必要，避免加载完整文档内容。  

## 结论

现在，你已经掌握了使用 GroupDocs.Redaction **获取文件类型（Java）**、**获取文档大小（Java）**、**获取页数（Java）** 以及 **检索 PDF 元数据（Java）** 的方法。将这些代码片段集成到你的 Java 应用中，以实现更智能的文档处理决策。

## 常见问题解答

**Q1: 什么是 GroupDocs.Redaction？**  
A1: 它是一个用于在 Java 应用程序中进行文档脱敏和管理信息的库。

**Q2: 我可以从 PDF 文件中检索元数据吗？**  
A2: 可以，库支持包括 PDF 在内的多种文件格式。

**Q3: 检索文档信息时如何处理异常？**  
A3: 使用 try‑catch 块来优雅地管理可能出现的错误。

**Q4: 我可以获取哪些文档信息？**  
A4: 文件类型、页数以及字节大小等细节均可获取。

**Q5: 除了 Word 文档外，还支持其他格式吗？**  
A5: 支持，包括 PDF、Excel、PowerPoint 等多种文件类型。

## 其他常见问题

**Q: API 是否会返回 PDF 版本（例如 1.7）作为元数据的一部分？**  
A: `IDocumentInfo` 对象包含基本的 PDF 特性；如需详细的版本信息，可通过 Redactor API 查询 PDF‑specific 属性。

**Q: 能否在不加载整个文档到内存的情况下检索元数据？**  
A: 可以，`getDocumentInfo()` 只读取所需的头部信息，从而保持低内存占用。

**Q: 是否可以高效地批量处理大量文档？**  
A: 为每个文档创建独立的 `Redactor` 实例，并使用线程池并行处理，可实现高效批量操作。

---

**Last Updated:** 2025-12-20  
**Tested With:** GroupDocs.Redaction 24.9 for Java  
**Author:** GroupDocs  

**资源**  
- **文档：** [GroupDocs Redaction Java Documentation](https://docs.groupdocs.com/redaction/java/)  
- **API 参考：** [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java)  
- **下载：** [GroupDocs.Redaction for Java Downloads](https://releases.groupdocs.com/redaction/java/)  
- **GitHub：** [GroupDocs GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **免费支持：** [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)  
- **临时许可证：** [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license/)