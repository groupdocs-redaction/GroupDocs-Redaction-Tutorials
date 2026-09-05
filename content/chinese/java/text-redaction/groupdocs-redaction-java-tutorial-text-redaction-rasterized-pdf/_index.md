---
date: '2026-08-20'
description: 了解如何使用 GroupDocs.Redaction Java 对文本进行脱敏、保存为 rasterized PDF、替换精确短语并应用自定义
  PDF 设置。
keywords:
- how to redact text
- save pdf as image
- convert pdf to image
lastmod: '2026-08-20'
og_description: 如何使用 GroupDocs.Redaction Java 对文本进行脱敏。本指南展示了精确短语替换、rasterized PDF
  创建以及 PDF/A‑1a 合规的简易步骤。
og_image_alt: Guide showing GroupDocs.Redaction Java code to redact text and create
  rasterized PDF
og_title: 如何使用 GroupDocs.Redaction Java 库对文本进行脱敏
schemas:
- author: GroupDocs
  dateModified: '2026-08-20'
  description: Learn how to redact text with GroupDocs.Redaction Java, save as rasterized
    PDF, replace exact phrases, and apply custom PDF settings.
  headline: How to redact text with GroupDocs.Redaction Java
  type: TechArticle
- description: Learn how to redact text with GroupDocs.Redaction Java, save as rasterized
    PDF, replace exact phrases, and apply custom PDF settings.
  name: How to redact text with GroupDocs.Redaction Java
  steps:
  - name: '**Sensitive data redaction** – automatically hide personal identifiers
      before sharing contracts.'
    text: '**Sensitive data redaction** – automatically hide personal identifiers
      before sharing contracts.'
  - name: '**Document archiving** – convert finalized reports to rasterized PDF/A
      for long‑term compliance.'
    text: '**Document archiving** – convert finalized reports to rasterized PDF/A
      for long‑term compliance.'
  - name: '**Bulk content update** – replace outdated terminology across hundreds
      of files with a single script.'
    text: '**Bulk content update** – replace outdated terminology across hundreds
      of files with a single script.'
  type: HowTo
- questions:
  - answer: Add the GroupDocs repository and the `groupdocs-redaction` dependency
      to your `pom.xml` as shown in the Maven Setup section.
    question: How do I install GroupDocs.Redaction in a Maven project?
  - answer: Yes, GroupDocs.Redaction supports PDF, DOCX, PPTX, and many other formats.
    question: Can I redact text from PDF files using this library?
  - answer: The `RedactorChangeLog` will return a status of `Failed`. Verify the phrase’s
      spelling and case sensitivity.
    question: What happens if the exact phrase isn’t found?
  - answer: Process them in smaller page ranges, enable rasterization only where needed,
      and always close the `Redactor` to free resources.
    question: How can I handle very large documents efficiently?
  - answer: Absolutely. Use `options.getRasterization().setPageIndex()` and `setPageCount()`
      to target the exact pages you want to rasterize.
    question: Is it possible to save rasterized PDFs with specific page ranges?
  type: FAQPage
tags:
- text redaction
- GroupDocs.Redaction
- Java PDF processing
title: 如何使用 GroupDocs.Redaction Java 对文本进行脱敏
type: docs
url: /zh/java/text-redaction/groupdocs-redaction-java-tutorial-text-redaction-rasterized-pdf/
weight: 1
---

# 如何使用 GroupDocs.Redaction Java 对文本进行编辑

在现代应用程序中，**如何编辑文本** 在文档中，同时保持工作流快速且合规，是开发人员、审计员和合规官员经常面临的挑战。本教程将指导您使用 GroupDocs.Redaction for Java 来定位精确短语，用安全的覆盖层替换它们，最终将结果导出为栅格化的 PDF/A‑1a 文档——非常适合归档或法律分发。

## 快速答案
- **主要的编辑类是什么？** `Redactor`  
- **我可以用彩色覆盖层替换短语吗？** 是的，使用 `ExactPhraseRedaction` 和 `ReplacementOptions`。  
- **如何生成栅格化的 PDF？** 通过 `SaveOptions.getRasterization().setEnabled(true)` 启用栅格化。  
- **示例中使用的 PDF 合规级别是什么？** `PdfComplianceLevel.PdfA1a`。  
- **生产环境是否需要许可证？** 生产部署需要有效的 GroupDocs.Redaction 许可证。

## 在 Java 中，“如何编辑文本”是什么？
`Redaction` 是对文件中敏感内容的永久删除或遮蔽，使其之后无法恢复或读取。使用 GroupDocs.Redaction，您可以以编程方式搜索精确短语——例如社会保障号码或机密项目代码——并将其替换为红色覆盖层、黑色方框或任何自定义可视元素，确保原始数据不可恢复。

## 为什么使用 GroupDocs.Redaction for Java？
GroupDocs.Redaction 支持 **30 多种输入和输出格式**（PDF、DOCX、PPTX、XLSX、HTML 以及图像类型），并且能够在不将整个文件加载到内存中的情况下处理数百页的文档。其精确短语匹配算法相比通用关键字搜索可将误报率降低超过 95%，内置的栅格化引擎还能让您生成完全基于图像的 PDF/A‑1a 文件，以实现长期保存。

## 前提条件
- **GroupDocs.Redaction for Java** (v24.9 或更新版本)。  
- **Java Development Kit (JDK) 8+**。  
- IDE，例如 IntelliJ IDEA、Eclipse 或 NetBeans。  
- 用于依赖管理的 Maven。  

### 必需的库和依赖项
- GroupDocs.Redaction for Java – 将仓库和依赖添加到您的 `pom.xml`（参见 Maven 设置部分）。  
- 可选：您喜欢的任何日志框架（SLF4J、Log4j 等）。

### 知识前提
- 基本的 Java 语法和文件 I/O。  
- 熟悉 Maven 的 `pom.xml` 结构。

## 设置 GroupDocs.Redaction for Java
### Maven 设置
Add the GroupDocs repository and the `groupdocs-redaction` dependency to your `pom.xml` file:

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
或者，您可以直接从 [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) 下载最新版本。

### 许可证获取
- **免费试用** – 在没有许可证密钥的情况下探索 API。  
- **临时许可证** – 用于延长评估。  
- **正式许可证** – 生产环境所需。  

### 基本初始化和设置
`Redactor` 类是所有编辑操作的入口点。它加载文档，应用编辑规则，并保存结果。

```java
import com.groupdocs.redaction.Redactor;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
```

## 如何编辑文本 – 精确短语示例
`Redactor` 是加载文档并应用编辑规则的主要类。`ExactPhraseRedaction` 定义了匹配特定字符串的规则。此示例演示了加载文件、创建 `ExactPhraseRedaction` 规则并在单一步骤中执行编辑，为开发人员提供了简洁的工作流，同时确保原始内容被永久遮蔽。

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.ReplacementOptions;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
```

## 如何保存为栅格化 PDF
`SaveOptions` 是控制文档保存方式的配置对象。通过启用其栅格化功能并选择 PDF/A‑1a 合规性，您可以生成仅图像的 PDF，其中每页都以位图形式渲染，满足归档标准并防止文本提取。

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
try {
    RedactorChangeLog result = redactor.apply(new ExactPhraseRedaction(
        "John Doe", new ReplacementOptions(java.awt.Color.RED)));
    
    if (result.getStatus() != RedactionStatus.Failed) {
        // Successfully redacted the text
    }
} finally { 
    redactor.close(); 
}
```

## 实际应用
1. **敏感数据编辑** – 在共享合同之前自动隐藏个人标识符。  
2. **文档归档** – 将最终报告转换为栅格化 PDF/A，以实现长期合规。  
3. **批量内容更新** – 使用单个脚本替换数百个文件中的过时术语。  

## 性能考虑因素
- **在每次操作后关闭 `Redactor`** 以释放文件句柄和内存。  
- **批处理** – 加载文件列表并循环处理，尽可能复用单个 `Redactor` 实例。  
- **监控资源** – 使用 Java 性能分析工具监视大规模编辑期间的 CPU 和堆使用情况。  

## 常见问题

**Q: 如何在 Maven 项目中安装 GroupDocs.Redaction？**  
A: 如 Maven 设置部分所示，将 GroupDocs 仓库和 `groupdocs-redaction` 依赖添加到您的 `pom.xml` 中。

**Q: 我可以使用此库对 PDF 文件进行编辑吗？**  
A: 可以，GroupDocs.Redaction 支持 PDF、DOCX、PPTX 等多种格式。

**Q: 如果未找到精确短语会怎样？**  
A: `RedactorChangeLog` 将返回 `Failed` 状态。请检查短语的拼写和大小写敏感性。

**Q: 如何高效处理非常大的文档？**  
A: 将其分成较小的页范围处理，仅在需要时启用栅格化，并始终关闭 `Redactor` 以释放资源。

**Q: 是否可以将栅格化 PDF 保存为特定页范围？**  
A: 完全可以。使用 `options.getRasterization().setPageIndex()` 和 `setPageCount()` 来指定要栅格化的确切页面。

## 结论
您现在拥有了一份完整的、端到端的指南，介绍如何使用 GroupDocs.Redaction Java **编辑文本** 并 **保存为栅格化 PDF**。遵循这些步骤，您可以保护敏感信息，满足严格的合规标准，并在大规模下保持 Java 服务的性能。

**接下来的步骤**  
- 通过浏览 [official documentation](https://docs.groupdocs.com/redaction/java/) 更深入地了解 API。  
- 尝试其他编辑类型，如 `RegexRedaction` 和 `ImageRedaction`。  
- 加入 [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) 社区，获取技巧和最佳实践。

---

**最后更新：** 2026-08-20  
**测试版本：** GroupDocs.Redaction Java 24.9  
**作者：** GroupDocs

```java
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.options.PdfComplianceLevel;
```

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
try {
    SaveOptions options = new SaveOptions();

    // Enable rasterization for converting pages into images.
    options.getRasterization().setEnabled(true);
    
    // Set the starting page and count for rasterization.
    options.getRasterization().setPageIndex(5);
    options.getRasterization().setPageCount(1);

    // Define PDF compliance level.
    options.getRasterization().setCompliance(PdfComplianceLevel.PdfA1a);

    // Append a suffix to avoid filename conflicts.
    options.setAddSuffix(true);

    // Save the document with these configurations.
    redactor.save(options);
} finally { 
    redactor.close(); 
}
```

## 相关教程

- [如何使用 GroupDocs.Redaction for Java 编辑文本](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction/)
- [Java 文本编辑教程：使用 GroupDocs.Redaction 的指南](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction-guide/)