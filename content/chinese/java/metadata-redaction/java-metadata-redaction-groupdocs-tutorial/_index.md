---
date: '2026-09-26'
description: 了解如何在 Java 中使用 GroupDocs 对 metadata 进行 redact，安全地删除 confidential 文档 metadata，同时保持原始格式不变。
keywords:
- how to redact metadata
- GroupDocs Redaction Java
- secure document processing
- metadata removal Java
lastmod: '2026-09-26'
og_description: 如何在 Java 中使用 GroupDocs 对 metadata 进行 redact – 一份 step‑by‑step 指南，展示如何安全地剥除
  confidential 文档 metadata 并保持原始格式。
og_image_alt: Guide showing metadata redaction using GroupDocs in Java
og_title: 如何在 Java 中使用 GroupDocs 对 metadata 进行 redact
schemas:
- author: GroupDocs
  dateModified: '2026-09-26'
  description: Learn how to redact metadata with GroupDocs in Java, securely removing
    confidential document metadata while keeping the original format intact.
  headline: How to redact metadata with GroupDocs in Java
  type: TechArticle
- description: Learn how to redact metadata with GroupDocs in Java, securely removing
    confidential document metadata while keeping the original format intact.
  name: How to redact metadata with GroupDocs in Java
  steps:
  - name: import necessary classes
    text: These imports give you access to the redaction engine, save options, and
      metadata utilities.
  - name: initialize redactor
    text: Instantiate the `Redactor` with the path to your source file.
  - name: configure metadata search and redaction
    text: Create a `MetadataSearchRedaction` that looks for the exact string **"Company
      Ltd."** and replaces it with **"--company--"**. The `setFilter` call limits
      the operation to the *Company* metadata field only.
  - name: apply the redaction
    text: Run the redaction against the opened document.
  - name: save with custom options
    text: '`SaveOptions` allows you to specify output format, file naming, and other
      saving parameters for the redacted document. Configure `SaveOptions` so the
      redacted file gets a “_Redacted” suffix while preserving its original format.'
  - name: release resources
    text: Always close the `Redactor` to free native resources and avoid memory leaks.
  type: HowTo
- questions:
  - answer: It’s a powerful library that enables you to redact text, metadata, and
      images in documents using Java applications.
    question: What is GroupDocs.Redaction for Java?
  - answer: Yes, but with limitations. A free trial or temporary license allows full
      access for testing purposes.
    question: Can I use GroupDocs.Redaction without purchasing a license?
  - answer: Use `SaveOptions` to specify your requirements, such as avoiding rasterization
      when saving to PDF.
    question: How do I ensure document formats are preserved during redaction?
  - answer: It supports a wide range, including Word, Excel, PowerPoint, PDF, and
      many more.
    question: What types of documents can be redacted using GroupDocs.Redaction?
  - answer: Visit the [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33)
      for assistance.
    question: Where can I find support if I run into issues?
  type: FAQPage
tags:
- metadata redaction
- GroupDocs
- Java document security
- redaction tutorial
title: 如何在 Java 中使用 GroupDocs 对 metadata 进行 redact
type: docs
url: /zh/java/metadata-redaction/java-metadata-redaction-groupdocs-tutorial/
weight: 1
---

# 如何使用 GroupDocs 在 Java 中编辑元数据

在本综合教程中，您将学习**如何编辑元数据**，从 Word、PDF 以及许多其他文档类型使用 GroupDocs.Redaction for Java。完成本指南后，您将能够将元数据编辑嵌入任何基于 Java 的服务，确保公司名称、作者或自定义属性等机密信息永不离开您的组织。

## 快速答案
- **MetadataSearchRedaction 是做什么的？** 它搜索特定的元数据字段并将其值替换为自定义文本。  
- **需要哪个库？** GroupDocs.Redaction for Java (v24.9 或更高)。  
- **我需要许可证吗？** 免费试用可用于评估；生产环境需要完整许可证。  
- **可以保留原始文件格式吗？** 可以——使用 `SaveOptions` 保持原始格式。  
- **此方法是线程安全的吗？** 每个 `Redactor` 实例是独立的，您可以并行处理文档。

## 如何使用 GroupDocs 编辑元数据？
`Redactor` 是加载文档并提供编辑操作的核心类。使用 `Redactor` 实例加载源文档，配置针对您想要清除的特定元数据键的 `MetadataSearchRedaction`，应用编辑，最后使用 `SaveOptions` 保存文件。整个工作流只需几行代码即可实现，并适用于任何受支持的格式，从 DOCX 到 PDF 及更高。

## 什么是使用 GroupDocs 的元数据编辑？
`MetadataSearchRedaction` 是一个专用类，允许您定位特定的元数据属性（例如 *Company*、*Author*）并将其内容替换为占位符。当需要在向外部合作伙伴共享文档之前对企业数据进行匿名化时，它非常理想。编辑过程不会更改文档的其他元素，确保在删除元数据后视觉布局和内容保持完整。

## 为什么使用 GroupDocs 进行元数据编辑？
使用 GroupDocs 进行元数据编辑提供了一种可靠的方法，从文档中剥离敏感信息，同时保留其原始外观和结构。通过专注于元数据字段，您可以快速符合隐私标准，而无需修改可见内容或冒着意外数据泄露的风险。

- **精确性** – 仅编辑您指定的字段，文档其余部分保持不变。  
- **合规性** – 通过删除隐藏标识符，帮助满足 GDPR、HIPAA 等隐私法规。  
- **自动化准备** – 可无缝集成到批处理流水线或微服务中。  
- **广泛的格式支持** – GroupDocs.Redaction 支持 **50+ 输入和输出格式**（包括 DOCX、PDF、PPTX、XLSX 以及图像类型），并且能够在不将整个文档加载到内存的情况下处理数百页的文件。

## 前置条件
- **GroupDocs.Redaction for Java** ≥ 24.9。  
- 已在机器上安装 Java 8 或更高版本。  
- 如 IntelliJ IDEA 或 Eclipse 等 IDE（可选，但推荐）。  
- 对 Maven 有基本了解（或能够手动添加 JAR）。

## 为 Java 设置 GroupDocs.Redaction

将仓库和依赖添加到您的 `pom.xml`。此步骤确保 Maven 能自动下载该库。

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

*或者，您可以直接从官方发布页面下载 JAR：*  
[GroupDocs.Redaction for Java 发布](https://releases.groupdocs.com/redaction/java/)

### 许可证获取
- **免费试用** – 下载试用许可证以探索所有功能。  
- **临时许可证** – 用于延长测试。  
- **完整许可证** – 生产部署所需。

## 基本初始化
`Redactor` 加载文档并提供应用各种编辑的方法。创建指向您要处理的文档的 `Redactor` 实例。

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

## 实现指南

### 步骤 1：导入必要的类
这些导入使您能够访问编辑引擎、保存选项和元数据工具。

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.redactions.MetadataFilters;
import com.groupdocs.redaction.redactions.MetadataSearchRedaction;
```

### 步骤 2：初始化 Redactor
使用源文件路径实例化 `Redactor`。

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

### 步骤 3：配置元数据搜索和编辑
创建一个 `MetadataSearchRedaction`，查找精确字符串 **"Company Ltd."** 并将其替换为 **"--company--"**。`setFilter` 调用将操作限制仅针对 *Company* 元数据字段。

```java
MetadataSearchRedaction redaction = new MetadataSearchRedaction("Company Ltd.", "--company--");
redaction.setFilter(MetadataFilters.Company);
```

### 步骤 4：应用编辑
对已打开的文档运行编辑。

```java
redactor.apply(redaction);
```

### 步骤 5：使用自定义选项保存
`SaveOptions` 允许您为编辑后的文档指定输出格式、文件命名和其他保存参数。配置 `SaveOptions` 使编辑后的文件在保留原始格式的同时添加 “_Redacted” 后缀。

```java
SaveOptions tmp0 = new SaveOptions();
tmp0.setAddSuffix(true);  // Adds "_Redacted" to file name
tmp0.setRasterizeToPDF(false);  // Keeps original format

redactor.save(tmp0);
```

### 步骤 6：释放资源
始终关闭 `Redactor` 以释放本机资源并避免内存泄漏。

```java
finally {
    redactor.close();
}
```

## 常见问题及解决方案
- **FileNotFoundException** – 再次检查传递给 `Redactor` 的路径。使用绝对路径或 `Paths.get(...)` 以确保可靠性。  
- **未观察到更改** – 确认您目标的元数据字段确实包含搜索字符串；元数据默认区分大小写。  
- **大文件内存不足错误** – 将文档分成更小的批次处理，并在每个文件后及时调用 `redactor.close()`。

## 实际应用
1. **法律文档** – 在将合同发送给第三方之前删除客户公司名称。  
2. **财务报告** – 对审计文件中的内部标识符进行匿名化。  
3. **协作项目** – 在与外部供应商共享草稿时保护专有信息。

## 性能考虑因素
- **内存管理** – 该库将整个文档加载到内存中；在每个文件处理后关闭 `Redactor` 至关重要。  
- **批处理** – 对于高吞吐场景，遍历文件集合并复用单个 `SaveOptions` 实例。  
- **保持更新** – 新版本带来性能改进和错误修复；始终使用最新的稳定版本。

## 常见问题

**Q: 什么是 GroupDocs.Redaction for Java？**  
A: 它是一个强大的库，能够使用 Java 应用程序对文档中的文本、元数据和图像进行编辑。

**Q: 我可以在不购买许可证的情况下使用 GroupDocs.Redaction 吗？**  
A: 可以，但有一定限制。免费试用或临时许可证可用于测试并提供完整访问权限。

**Q: 如何确保在编辑过程中保持文档格式？**  
A: 使用 `SaveOptions` 指定需求，例如在保存为 PDF 时避免光栅化。

**Q: 使用 GroupDocs.Redaction 可以编辑哪些类型的文档？**  
A: 它支持广泛的文档类型，包括 Word、Excel、PowerPoint、PDF 等等。

**Q: 如果遇到问题，我可以在哪里获取支持？**  
A: 访问 [GroupDocs 支持论坛](https://forum.groupdocs.com/c/redaction/33) 获取帮助。

**Q: MetadataSearchRedaction 能处理加密文档吗？**  
A: 能。使用接受密码参数的 `Redactor` 构造函数加载带有相应密码的文档。

**Q: 我可以在一次运行中链式执行多个元数据编辑吗？**  
A: 完全可以。创建多个 `MetadataSearchRedaction` 对象，设置不同的过滤器，并在保存前依次应用它们。

**Q: 是否可以在保存前预览编辑？**  
A: 您可以调用 `redactor.getRedactions()` 获取待编辑列表，并以编程方式检查它们。

## 其他资源
- **文档**：在 [GroupDocs 文档](https://docs.groupdocs.com/redaction/java/) 中查看详细指南。  
- **API 参考**：在 [GroupDocs API 参考](https://reference.groupdocs.com/redaction/java) 查看完整的 API 参考。  
- **下载库**：从 [GroupDocs 下载](https://releases.groupdocs.com/redaction/java/) 获取最新发布。  
- **源代码**：在 [GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java) 查看并贡献代码。  
- **支持**：通过 [GroupDocs 支持论坛](https://forum.groupdocs.com/c/redaction/33) 的免费支持渠道获取帮助。

---

**最后更新：** 2026-09-26  
**测试环境：** GroupDocs.Redaction 24.9 for Java  
**作者：** GroupDocs

## 相关教程

- [Groupdocs Redaction Java 文档元数据提取](/redaction/java/metadata-redaction/groupdocs-redaction-java-document-metadata-extraction/)
- [替换元数据文本 Java – 使用 GroupDocs 的安全编辑](/redaction/java/metadata-redaction/java-redaction-metadata-text-replacement-guide/)
- [使用 Groupdocs Redaction Java 检索文档信息](/redaction/java/document-information/retrieve-document-info-using-groupdocs-redaction-java/)