---
date: '2026-03-20'
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

# 如何使用 GroupDocs.Redaction 获取 Java 文件类型

检索文档的关键细节——例如 **file type**、页数和大小——是构建以文档为中心的 Java 应用程序时的常见需求。在本教程中，您将学习如何使用 GroupDocs.Redaction 库 **get file type java**，以及如何 **get document size java**、**get page count java**，甚至 **retrieve pdf metadata java**。提前了解文件类型可以帮助您决定采用哪种处理路径，而大小和页数信息则有助于高效管理资源。

## 快速答案
- **哪个方法返回文件类型？** `IDocumentInfo.getFileType()`
- **如何获取页数？** `IDocumentInfo.getPageCount()`
- **哪个调用返回文档大小（字节）？** `IDocumentInfo.getSize()`
- **运行示例是否需要许可证？** 试用版或临时许可证可用于评估。  
- **需要哪个 Java 版本？** Java 8 或更高。

## 什么是 “get file type java”
该短语指在 Java 中以编程方式从文档中提取文件格式（例如 DOCX、PDF）。GroupDocs.Redaction 通过 `IDocumentInfo` 接口公开此信息，使其只需一行代码即可获取。

## 为什么使用 GroupDocs.Redaction 提取元数据？
- **广泛的格式支持：** 处理 PDF、DOCX、XLSX、PPTX 等多种格式。  
- **简洁的 API：** 一行调用即可返回文件类型、页数和大小。  
- **性能优化：** 仅加载所需的元数据，保持低内存使用。  
- **一致的结果：** 在所有受支持的文件扩展名上表现相同，因此您也可以在 **java get file extension** 场景中依赖它。

## 前提条件
- 已安装 Java 8 或更高版本。  
- 兼容 Maven 的 IDE（IntelliJ IDEA、Eclipse 等）。  
- 拥有 GroupDocs.Redaction 许可证（免费试用或临时许可证）。

## 为 Java 设置 GroupDocs.Redaction

要在 Java 项目中使用 GroupDocs.Redaction 库，请按照以下安装步骤操作：

**Maven 安装**

在您的 `pom.xml` 文件中添加以下仓库和依赖：

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
- **Free Trial（免费试用）：** 先使用免费试用版评估库。  
- **Temporary License（临时许可证）：** 获取临时许可证以进行更长时间的评估。  
- **Purchase（购买）：** 如符合需求，可考虑购买。

安装完成后，初始化并设置 GroupDocs.Redaction：

```java
import com.groupdocs.redaction.Redactor;

// Initialize Redactor with the path to your document
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

## 为什么在实际项目中获取文件类型（java）很重要
提前了解文档的类型可以让您将文件路由到正确的处理流水线，例如将 PDF 发送到脱敏工作流，将 Word 文件发送到转换服务，或将图像发送到 OCR 引擎。它还帮助您执行安全策略（阻止可执行文件）并在文档管理系统中提供准确的 UI 图标。

## 如何获取文件类型（java）、文档大小（java）和页数（java）

库已准备就绪后，让我们逐步演示获取所需信息的具体步骤。

### 步骤 1：导入必要的类

确保在 Java 文件顶部导入所需的类：

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.domain.IDocumentInfo;
```

### 步骤 2：初始化 Redactor

创建一个 `Redactor` 实例，指定文档的路径。该对象使您能够与文件交互并提取元数据。

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
try {
    // Code for retrieving information will go here.
} finally {
    redactor.close();
}
```

### 步骤 3：检索并显示文档信息

调用 `getDocumentInfo()` 获取 `IDocumentInfo` 对象。通过该对象，您可以在一次调用中 **get file type java**、**get document size java** 和 **get page count java**。

```java
// Retrieve document information
IDocumentInfo info = redactor.getDocumentInfo();

// Output document type, page count, and size in bytes
System.out.println("File Type: " + info.getFileType());
System.out.println("Page Count: " + info.getPageCount());
System.out.println("Size (Bytes): " + info.getSize());
```

这三个 `System.out.println` 语句分别输出文件类型、页数和字节大小——正是下游处理所需的信息。

## 如何检索 PDF 元数据（java）

如果源文档是 PDF，使用相同的 `IDocumentInfo` 调用即可返回 PDF 特有的元数据（例如 PDF 版本、加密状态）。无需额外代码，只需使用相同的 `getDocumentInfo()` 方法。

## 常见使用场景
1. **文档管理系统：** 在存储之前自动按类型或大小对文件进行分类。  
2. **内容处理流水线：** 根据页数选择不同的处理策略（例如，对大 PDF 批量脱敏，对小 Word 文档单独处理）。  
3. **数字资产库：** 向用户展示文档属性的快速预览，无需打开文件。

## 常见问题及解决方案
- **File not found（文件未找到）：** 检查传递给 `Redactor` 的绝对或相对路径。  
- **Unsupported format（不支持的格式）：** 确认文档的扩展名受 GroupDocs.Redaction 支持。  
- **License errors（许可证错误）：** 使用有效的试用或永久许可证，否则 API 将抛出许可证异常。

## 故障排除技巧（读取文档元数据 java）
- 在 `try‑catch` 块中包装元数据调用，以优雅地处理损坏的文件。  
- 使用 `redactor.isEncrypted()`（如果可用）在读取元数据前检测加密的 PDF。  
- 处理大量文件时，复用线程池并及时关闭每个 `Redactor` 实例，以避免文件句柄泄漏。

## 性能考虑

处理大批量时：

- 在 `try‑with‑resources` 块中打开每个文档，以确保及时释放文件句柄。  
- 仅缓存所需的元数据；除非必要，避免加载完整文档内容。

## 结论

现在您已经了解如何使用 GroupDocs.Redaction **get file type java**、**get document size java**、**get page count java** 和 **retrieve pdf metadata java**。将这些代码片段集成到您的 Java 应用程序中，以便在文档处理上做出更智能的决策，提升性能，并提供更丰富的用户体验。

## 常见问答

**Q1: 什么是 GroupDocs.Redaction？**  
A1: 它是一个用于在 Java 应用程序中脱敏和管理文档信息的库。

**Q2: 我可以检索 PDF 文件的元数据吗？**  
A2: 可以，库支持包括 PDF 在内的多种文件格式。

**Q3: 检索文档信息时如何处理异常？**  
A3: 使用 try‑catch 块优雅地管理可能的错误。

**Q4: 我可以获取文档哪些信息？**  
A4: 文件类型、页数以及字节大小等细节均可获取。

**Q5: 除了 Word 文档外，还支持其他文件格式吗？**  
A5: 是的，GroupDocs.Redaction 支持包括 PDF、Excel 文件等多种文件类型。

## 其他常见问题

**Q: API 是否在元数据中返回 PDF 版本（例如 1.7）？**  
A: `IDocumentInfo` 对象包含基本的 PDF 特性；若需详细的版本信息，可通过 Redactor API 查询 PDF‑specific 属性。

**Q: 能否在不将整个文档加载到内存的情况下检索元数据？**  
A: 可以，`getDocumentInfo()` 只读取获取元数据所需的头部信息，保持低内存占用。

**Q: 是否可以高效地批量处理大量文档？**  
A: 为每个文档的处理创建独立的 `Redactor` 实例，并复用线程池以并行化工作负载。

**资源**
- **文档：** [GroupDocs Redaction Java Documentation](https://docs.groupdocs.com/redaction/java/)  
- **API 参考：** [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java)  
- **下载：** [GroupDocs.Redaction for Java Downloads](https://releases.groupdocs.com/redaction/java/)  
- **GitHub：** [GroupDocs GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **免费支持：** [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)  
- **临时许可证：** [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license/)  

---

**最后更新：** 2026-03-20  
**测试环境：** GroupDocs.Redaction 24.9 for Java  
**作者：** GroupDocs