---
date: '2026-08-20'
description: 了解如何在 Java 中使用 GroupDocs.Redaction 通过 regex 对文本进行 redact。此分步教程展示了如何应用
  regex、配置 save options，以及保护 sensitive data。
keywords:
- how to redact text
- mask credit card numbers
- remove social security numbers
- redact pdf java
lastmod: '2026-08-20'
og_description: 了解如何在 Java 中使用 GroupDocs.Redaction 对文本进行 redact。本指南解释了 regex redact、save‑option
  配置以及保护 sensitive data 的 performance tips。
og_image_alt: Guide showing Java code to redact text using GroupDocs.Redaction
og_title: 如何在 Java 中使用 GroupDocs.Redaction 对文本进行 redact
schemas:
- author: GroupDocs
  dateModified: '2026-08-20'
  description: Discover how to redact text using regex in Java with GroupDocs.Redaction.
    This step‑by‑step tutorial shows you how to apply regex, configure save options,
    and protect sensitive data.
  headline: 'How to redact text in Java with GroupDocs.Redaction: A complete guide'
  type: TechArticle
- description: Discover how to redact text using regex in Java with GroupDocs.Redaction.
    This step‑by‑step tutorial shows you how to apply regex, configure save options,
    and protect sensitive data.
  name: 'How to redact text in Java with GroupDocs.Redaction: A complete guide'
  steps:
  - name: import required classes
    text: 'The following imports give you access to the redaction API:'
  - name: initialize redactor and apply regex pattern
    text: '`RegexRedaction` represents a redaction rule based on a regular‑expression
      pattern. The pattern you provide determines which text fragments are replaced.
      - **Regex explanation**: The pattern `\b\d{3}-\d{2}-\d{4}\b` matches U.S. Social
      Security numbers (three digits, a dash, two digits, a dash, four '
  - name: configure save options
    text: '`SaveOptions` controls how the redacted file is written. Adding a suffix
      makes it clear which files have been processed, while preserving the original
      format avoids unwanted conversion. - **Save options**: `setAddSuffix(true)`
      automatically appends “_redacted” to the output filename, preventing acci'
  - name: customize additional save settings
    text: 'You can further tailor the output—such as preserving metadata or flattening
      annotations—by adjusting the `SaveOptions` object. - **Key configuration**:
      Setting `setPreserveMetadata(true)` retains original document properties, which
      is often required for compliance audits.'
  type: HowTo
- questions:
  - answer: It automatically appends a suffix (e.g., `_redacted`) to the output filename,
      making it obvious which files have been processed.
    question: What is the purpose of `setAddSuffix(true)` in SaveOptions?
  - answer: Absolutely. Any valid Java regular expression can be supplied to `RegexRedaction`
      to target emails, phone numbers, custom IDs, etc.
    question: Can I use regex patterns other than numbers for text redaction?
  - answer: Wrap the redaction logic in a try‑catch block, log the exception, and
      always close the `Redactor` in a finally clause to release resources.
    question: How should I handle errors during redaction?
  - answer: Yes. GroupDocs.Redaction works with PDF, DOCX, PPTX, and many other formats.
    question: Is PDF redaction supported?
  - answer: Use batch processing, keep regex patterns simple, and monitor memory usage
      with profiling tools.
    question: What are best practices for large‑scale redaction projects?
  type: FAQPage
tags:
- text redaction
- GroupDocs.Redaction
- Java document processing
- regex redaction
- PDF redaction
title: 如何在 Java 中使用 GroupDocs.Redaction 对文本进行 redact：完整指南
type: docs
url: /zh/java/text-redaction/master-text-redaction-java-groupdocs-redaction-guide/
weight: 1
---

# 如何在 Java 中使用 GroupDocs.Redaction 对文本进行编辑：完整指南

在当今快速发展的数字世界中，文档中**如何编辑文本**是许多开发者面临的问题。无论是保护个人数据、遵守法规，还是仅仅清理草稿，本指南将带您使用 GroupDocs.Redaction for Java **快速且安全地应用基于正则表达式的编辑**。您将了解编辑的重要性、如何配置库以及高性能处理的最佳实践技巧。

## 快速答案
- **GroupDocs.Redaction 的主要目的是什么？** 它提供可靠的 API 来定位并遮蔽超过 50 种文档格式中的敏感文本。  
- **如何使用正则表达式进行编辑？** 创建一个带有模式的 `RegexRedaction` 对象，并将其传递给 `Redactor.apply()` 方法。  
- **我需要许可证吗？** 免费试用可用于开发；付费许可证可解锁生产环境的全部功能。  
- **我可以编辑 PDF 以及 DOCX 文件吗？** 是的——GroupDocs.Redaction 支持 PDF、DOCX、PPTX 以及许多其他格式。  
- **提升性能的最佳方法是什么？** 及时关闭 `Redactor` 实例，保持正则表达式模式简洁，并批量处理文件。  

## 什么是文本编辑以及为什么重要？
文本编辑永久性地删除或遮蔽文档中的敏感信息，确保诸如社会保障号码、信用卡详情或医疗记录等机密数据无法被未授权方恢复或查看。它通过覆盖原始字符或用掩码替换来实现，使隐藏的内容无法通过复制粘贴或 OCR 工具提取。这确保了对隐私法规的合规性，并保护个人免受身份盗窃或数据泄露的风险。

## 为什么使用正则表达式进行文本编辑？
正则表达式让您能够定义灵活的模式，以匹配各种数据格式（例如电话号码、信用卡号码）。在 GroupDocs.Redaction 中使用正则表达式可让您精确控制要隐藏的内容，同时保持实现简洁且易于维护。

## 前置条件
在开始之前，请确保您已具备以下条件：

- **Java Development Kit (JDK)** 已安装（Java 8 或更高）。  
- 对 Java 语法和正则表达式有基本了解。  
- 一个 IDE，例如 **IntelliJ IDEA** 或 **Eclipse**，用于运行和调试代码。  

## 为 Java 设置 GroupDocs.Redaction
首先，将库添加到您的项目中。

### Maven 设置
如果您使用 Maven，请将以下内容插入到您的 `pom.xml` 中：

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

### 基本初始化
`Redactor` 是核心类，用于打开文档、应用编辑规则并写入输出。

库可用后，您可以开始编辑文档：

```java
// Import the necessary classes from GroupDocs.Redaction
import com.groupdocs.redaction.Redactor;

public class RedactionExample {
    public static void main(String[] args) {
        // Initialize the redactor with your document path
        final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
        // Ensure you close resources after operations
        try { /* Your code here */ } finally { redactor.close(); }
    }
}
```

## 如何在 Java 中使用正则表达式编辑文本？
该过程包括将源文件加载到 `Redactor` 实例中，创建定义匹配模式的 `RegexRedaction` 规则，使用 `redactor.apply()` 应用该规则，最后使用 `SaveOptions` 保存修改后的文档。遵循这些步骤，您可以可靠地定位并遮蔽所有受支持格式中的敏感字符串。

`Redactor` 类是核心组件，负责打开文档、应用编辑规则并写入输出文件。它在内部管理资源，因此处理完后必须关闭以释放内存。

### 步骤 1：导入所需类
以下导入语句为您提供对编辑 API 的访问：

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.redactions.RegexRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;
```

### 步骤 2：初始化 redactor 并应用正则表达式模式
`RegexRedaction` 表示基于正则表达式模式的编辑规则。您提供的模式决定了哪些文本片段会被替换。

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
try {
    // Define a regex pattern to find sequences of numbers and apply a replacement color.
    // The pattern: Two digits, optional whitespace, two more digits, non-digit characters,
    // followed by six digits.
    redactor.apply(new RegexRedaction("\\d{2}\\s*\\d{2}[^\\d]*\\d{6}", 
        new ReplacementOptions(java.awt.Color.BLUE)));
```

- **正则表达式说明**：模式 `\b\d{3}-\d{2}-\d{4}\b` 匹配美国社会保障号码（三位数字、一个破折号、两位数字、一个破折号、四位数字）。`ReplacementOptions` 允许您选择实心黑色覆盖或自定义文本掩码。

### 步骤 3：配置保存选项
`SaveOptions` 控制编辑后文件的写入方式。添加后缀可以清晰标识哪些文件已被处理，同时保留原始格式可避免不必要的转换。

```java
    // Configure save options
    SaveOptions saveOptions = new SaveOptions();
    saveOptions.setAddSuffix(true);  // Adds suffix to indicate processing
    saveOptions.setRasterizeToPDF(false);  // Preserves original format

    // Save the redacted document
    redactor.save(saveOptions);
} finally {
    redactor.close();  // Always close resources to prevent memory leaks
}
```

- **保存选项**：`setAddSuffix(true)` 会自动在输出文件名后追加 “_redacted”，防止意外覆盖。

### 步骤 4：自定义其他保存设置
您可以通过调整 `SaveOptions` 对象进一步定制输出，例如保留元数据或扁平化注释。

```java
import com.groupdocs.redaction.options.SaveOptions;

SaveOptions saveOptions = new SaveOptions();
saveOptions.setAddSuffix(true);  // Indicates processing by adding a suffix
saveOptions.setRasterizeToPDF(false);  // Keeps original format intact
```

- **关键配置**：设置 `setPreserveMetadata(true)` 可保留原始文档属性，这在合规审计中常常是必需的。

## 实际应用
在实际场景中，**如何编辑文本** 是必不可少的：

1. **法律文件** – 在与外部律师共享草稿之前隐藏客户标识符。  
2. **医疗记录** – 掩码患者姓名、ID 或健康号码，以符合 HIPAA 要求。  
3. **财务报告** – 在分发季度摘要时删除机密账户号码。  

## 性能考虑因素
- **内存管理**：始终调用 `redactor.close()` 以释放文件句柄和本地资源。  
- **高效正则表达式**：更简洁的模式运行更快；尽可能使用原子组以避免过度回溯。  
- **批量处理**：对于大型文档集，分批处理（每批 20–50 个文件）以保持堆内存使用可预测。  

## 常见问题及解决方案
| 问题 | 解决方案 |
|-------|----------|
| **正则匹配过多** | 使用在线正则测试工具测试您的模式并缩小字符类范围。 |
| **输出文件名冲突** | 使用 `setAddSuffix(true)` 或通过 `saveOptions.setOutputPath()` 提供自定义输出路径。 |
| **大型 PDF 内存泄漏** | 逐页处理 PDF 或增加 JVM 堆大小 (`-Xmx2g`)。 |

## 常见问题

**问：`setAddSuffix(true)` 在 SaveOptions 中的作用是什么？**  
答：它会自动在输出文件名后追加后缀（例如 `_redacted`），以明确哪些文件已被处理。

**问：我可以使用除数字之外的正则模式进行文本编辑吗？**  
答：当然可以。任何有效的 Java 正则表达式都可以提供给 `RegexRedaction`，用于定位电子邮件、电话号码、自定义 ID 等。

**问：在编辑过程中应如何处理错误？**  
答：将编辑逻辑放在 try‑catch 块中，记录异常，并始终在 finally 子句中关闭 `Redactor` 以释放资源。

**问：是否支持 PDF 编辑？**  
答：是的。GroupDocs.Redaction 支持 PDF、DOCX、PPTX 以及许多其他格式。

**问：大规模编辑项目的最佳实践是什么？**  
答：使用批量处理，保持正则模式简洁，并使用分析工具监控内存使用情况。

## 附加资源
- **文档**：[GroupDocs Redaction Documentation](https://docs.groupdocs.com/redaction/java/)  
- **API 参考**：[GroupDocs API Reference](https://apireference.groupdocs.com/redaction/java)

---

**最后更新：** 2026-08-20  
**测试环境：** GroupDocs.Redaction 24.9 for Java  
**作者：** GroupDocs

## 相关教程

- [掩码敏感数据 Java – GroupDocs.Redaction 指南](/redaction/java/getting-started/)
- [掩码敏感数据 Java – 使用 GroupDocs.Redaction 编辑个人信息](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)
- [如何使用 Aspose OCR 和 Java 编辑 PDF - 使用 GroupDocs.Redaction 实现正则模式](/redaction/java/ocr-integration/aspose-ocr-java-pdf-redaction/)