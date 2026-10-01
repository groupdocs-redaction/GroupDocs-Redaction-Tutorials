---
date: '2026-10-01'
description: 了解如何使用 GroupDocs Redaction 在 Java 中删除 author metadata 并保存 redacted document
  files。
keywords:
- remove author metadata
- save redacted document
- groupdocs metadata removal
lastmod: '2026-10-01'
og_description: 了解如何使用 GroupDocs Redaction 在 Java 中删除 author metadata 并保存 redacted
  document files。Follow the step‑by‑step guide.
og_image_alt: Guide showing Java code to remove author metadata using GroupDocs Redaction
og_title: 如何在 Java 中使用 GroupDocs 删除 author metadata
schemas:
- author: GroupDocs
  dateModified: '2026-10-01'
  description: Learn how to remove author metadata and save redacted document files
    in Java using GroupDocs Redaction.
  headline: How to remove author metadata in Java with GroupDocs
  type: TechArticle
- description: Learn how to remove author metadata and save redacted document files
    in Java using GroupDocs Redaction.
  name: How to remove author metadata in Java with GroupDocs
  steps:
  - name: '**Legal documents** – Redact author information before sending contracts
      to opposing counsel.'
    text: '**Legal documents** – Redact author information before sending contracts
      to opposing counsel.'
  - name: '**Corporate reports** – Remove manager names when publishing quarterly
      results to shareholders.'
    text: '**Corporate reports** – Remove manager names when publishing quarterly
      results to shareholders.'
  - name: '**Project files** – Clean up internal project documentation before archiving
      or uploading to a public repository.'
    text: '**Project files** – Clean up internal project documentation before archiving
      or uploading to a public repository.'
  type: HowTo
- questions:
  - answer: It removes selected metadata fields from a document.
    question: What does EraseMetadataRedaction do?
  - answer: GroupDocs.Redaction for Java.
    question: Which library provides this feature?
  - answer: A free trial works for testing; a permanent license is required for production.
    question: Do I need a license?
  - answer: Yes, combine filters with a logical OR.
    question: Can I target multiple fields at once?
  - answer: Redactor instances are not shared across threads; create a new instance
      per operation.
    question: Is the process thread‑safe?
  type: FAQPage
tags:
- metadata redaction
- GroupDocs
- Java document processing
title: 如何在 Java 中使用 GroupDocs 删除 author metadata
type: docs
url: /zh/java/metadata-redaction/groupdocs-redaction-java-metadata-implementation/
weight: 1
---

# 如何在 Java 中使用 GroupDocs 删除作者元数据

在当今的数字环境中，保护文档中隐藏的敏感信息是必不可少的做法。**删除作者元数据**可以防止个人或公司标识信息的意外泄露。本教程将逐步演示如何使用 GroupDocs.Redaction for Java 中的 `EraseMetadataRedaction` 来删除 Word 文件中的 *Author* 和 *Manager* 等字段，并且 **安全保存已编辑文档** 副本以便共享或归档。

## 快速答案
- **EraseMetadataRedaction 的作用是什么？** 它会删除文档中选定的元数据字段。  
- **哪个库提供此功能？** GroupDocs.Redaction for Java。  
- **我需要许可证吗？** 免费试用可用于测试；生产环境需要永久许可证。  
- **我可以一次定位多个字段吗？** 可以，使用逻辑 OR 组合过滤器。  
- **该过程是线程安全的吗？** Redactor 实例不会在线程间共享；每次操作都创建新实例。

## 什么是 EraseMetadataRedaction？

`EraseMetadataRedaction` 是内置的编辑类，允许您指定要删除的元数据条目。它适用于 GroupDocs.Redaction 支持的多种文档格式，确保隐藏的作者信息不会泄露。您可以定位诸如 Author、Manager 等标准属性，也可以删除自定义元数据字段，提供全面的隐私保护。

## 为什么在 GroupDocs 中使用 EraseMetadataRedaction？

GroupDocs.Redaction 支持 **超过 100 种输入和输出格式**，并且能够在不将整个文件加载到内存的情况下处理高达 500 页的文档。使用此类可为您提供一个高性能的 API，以满足 GDPR、HIPAA 或内部合规要求，同时保持代码库简洁。

## 前提条件
- 已安装 Java 8 或更高版本。  
- Maven（或手动添加 JAR 的能力）。  
- GroupDocs.Redaction for Java（版本 24.9 或更高）。  
- 有效的 GroupDocs 试用版或永久许可证。

## 为 Java 设置 GroupDocs.Redaction

### Maven 安装
将 GroupDocs 仓库和依赖添加到您的 **pom.xml**：

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
或者，从 [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) 下载最新的 JAR。

### 获取许可证
从 GroupDocs 门户获取免费试用或购买临时许可证。许可证文件应放置在应用程序能够加载的位置（例如，classpath 根目录）。

### 基本初始化和设置
下面是一个最小示例，创建用于 DOCX 文件的 `Redactor` 实例：

```java
import com.groupdocs.redaction.Redactor;

String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
Redactor redactor = new Redactor(filePath);
```

## 如何在 Java 中使用 EraseMetadataRedaction

以下章节将实现过程分解为清晰、可操作的步骤。

### 功能：清理特定元数据项

#### 概述
我们将使用 `EraseMetadataRedaction` 删除 **Author** 和 **Manager** 元数据字段。这是在向外部合作伙伴共享内部报告时的常见需求。

#### 步骤实现

##### 1️⃣ 初始化 Redactor 对象
`Redactor` 是加载文档、应用编辑对象并写入结果的核心类。为每个要处理的文件创建一个新实例：

```java
import com.groupdocs.redaction.Redactor;

String inputFilePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
final Redactor redactor = new Redactor(inputFilePath);
```

##### 2️⃣ 应用 EraseMetadataRedaction
`MetadataFilters` 为常见的元数据键（如 Author 和 Manager）提供预定义过滤器。  
`EraseMetadataRedaction` 删除与提供的 `MetadataFilters` 匹配的元数据条目。位运算 OR (`|`) 将 `Author` 和 `Manager` 过滤器组合，使两者在一次调用中被删除：

```java
import com.groupdocs.redaction.redactions.EraseMetadataRedaction;
import com.groupdocs.redaction.MetadataFilters;

try {
    redactor.apply(new EraseMetadataRedaction(MetadataFilters.Author | MetadataFilters.Manager));
} finally {
    redactor.close();
}
```

##### 3️⃣ 配置保存选项
`SaveOptions` 允许您指定输出文件名、格式以及其他保存参数。  
`SaveOptions` 让您控制输出文件名、格式，以及文档是否应栅格化为 PDF。添加后缀可保持原始文件不被修改：

```java
import com.groupdocs.redaction.options.SaveOptions;

SaveOptions saveOptions = new SaveOptions();
saveOptions.setAddSuffix(true); // Adds "_Redacted" to the file name
saveOptions.setRasterizeToPDF(false);

redactor.save(saveOptions);
```

## 常见用例
1. **法律文件** – 在向对方律师发送合同前删除作者信息。  
2. **公司报告** – 在向股东发布季度业绩时删除经理姓名。  
3. **项目文件** – 在归档或上传到公共仓库之前清理内部项目文档。

## 故障排除技巧
- **文件未找到** – 验证 `inputFilePath` 中的路径指向现有文件，并且应用程序具有读取权限。  
- **缺少元数据字段** – 并非所有文档类型都存储相同的元数据键；请先在 Office 中检查文档属性。  
- **许可证错误** – 在创建 `Redactor` 实例之前，确保正确加载许可证文件。

## 性能考虑
- 及时关闭 `Redactor` 对象（如 `finally` 块中所示），以释放本机资源。  
- 除非需要 PDF 预览，否则避免栅格化大型文档；栅格化可能导致 300 页文件的 CPU 和内存使用率提升至原来的 3 倍。

## 常见问题

**Q1: 什么是元数据编辑？**  
A1: 元数据编辑涉及删除隐藏的文档属性（如作者、经理或自定义标签），以防止敏感信息意外泄露。

**Q2: 我可以将 GroupDocs.Redaction 用于其他文件类型吗？**  
A2: 可以，库支持 PDF、DOCX、PPTX、XLSX 等众多格式——总计超过 100 种。

**Q3: 如何处理编辑过程中的错误？**  
A3: 将 `apply` 调用放在 try‑catch 块中，并始终在 finally 子句中关闭 `Redactor`，以确保释放资源。

**Q4: 能否编辑自定义元数据字段？**  
A5: 当然。使用 `MetadataFilters.Custom("YourFieldName")` 可定位文档中存储的任何自定义属性。

**Q5: 使用 GroupDocs.Redaction 的最佳实践是什么？**  
A5:  
- 在应用程序启动时尽早加载许可证。  
- 及时关闭 `Redactor` 对象。  
- 使用 `SaveOptions` 添加后缀，保持原始文件不被修改。  
- 在批量处理前在文档副本上测试编辑。

**Q6: EraseMetadataRedaction 支持批量操作吗？**  
A6: 您可以遍历文件路径集合，为每个文件创建新的 `Redactor` 并应用相同的编辑逻辑。

**Q7: 我可以将 EraseMetadataRedaction 与其他编辑类型结合使用吗？**  
A7: 可以，在保存之前链式调用多个编辑对象（例如，先进行文本编辑，再进行元数据编辑）。

## 资源

- **文档**: [GroupDocs Redaction Java Docs](https://docs.groupdocs.com/redaction/java/)  
- **API 参考**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java)  
- **下载**: [Latest Releases](https://releases.groupdocs.com/redaction/java/)  
- **GitHub**: [GroupDocs GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **免费支持**: [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)  
- **临时许可证**: [Acquire a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**最后更新：** 2026-10-01  
**测试环境：** GroupDocs.Redaction 24.9 for Java  
**作者：** GroupDocs

## 相关教程

- [Groupdocs Redaction Java 文档元数据提取](/redaction/java/metadata-redaction/groupdocs-redaction-java-document-metadata-extraction/)
- [如何使用 GroupDocs.Redaction 删除 Java 元数据](/redaction/java/metadata-redaction/metadata-redaction-groupdocs-java-guide/)
- [使用 Groupdocs Redaction Java 检索文档信息](/redaction/java/document-information/retrieve-document-info-using-groupdocs-redaction-java/)