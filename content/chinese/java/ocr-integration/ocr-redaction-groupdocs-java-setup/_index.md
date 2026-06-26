---
date: '2026-06-26'
description: 了解如何使用 GroupDocs OCR Redaction 与 Azure OCR 提取扫描 PDF 文本并掩码敏感数据。高效地对社会安全号码进行脱敏并替换
  PDF 中的机密信息。
keywords:
- extract text scanned pdf
- redact social security number
- mask sensitive data pdf
- replace confidential info pdf
schemas:
- author: GroupDocs
  dateModified: '2026-06-26'
  description: Learn how to extract text scanned PDF and mask sensitive data using
    GroupDocs OCR Redaction with Azure OCR. Redact social security number and replace
    confidential info PDF efficiently.
  headline: Extract Text Scanned PDF – Mask Data with GroupDocs OCR
  type: TechArticle
- questions:
  - answer: OCR redaction uses Optical Character Recognition to extract hidden text
      from images or scanned PDFs, then applies redaction rules to mask that text.
    question: What is OCR redaction?
  - answer: Yes, but OCR dramatically improves accuracy on scanned documents where
      native text extraction fails.
    question: Can I use GroupDocs Redaction without Azure OCR?
  - answer: Build and test them incrementally, using Java’s `Pattern` class in a sandbox
      before applying to large documents.
    question: How do I handle complex regex patterns?
  - answer: Large PDFs, overly complex regex, and synchronous OCR calls can slow processing;
      consider batch processing and optimized patterns.
    question: What are typical performance bottlenecks?
  - answer: Absolutely—reach out via the [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33)
      for community help or contact GroupDocs support.
    question: Is support available for implementation issues?
  type: FAQPage
title: 提取扫描 PDF 文本 – 使用 GroupDocs OCR 掩码数据
type: docs
url: /zh/java/ocr-integration/ocr-redaction-groupdocs-java-setup/
weight: 1
---

# 提取扫描 PDF 文本 – 使用 GroupDocs OCR 掩码数据

在当今数据驱动的世界，**从扫描的 PDF 文件中提取文本**并掩码机密信息是不可协商的合规步骤。本教程将指导您使用 GroupDocs Redaction 与 Microsoft Azure OCR 结合，可靠地识别扫描页面上的隐藏文本，并将其替换为安全的占位符，例如 **`[REDACTED]`**。您将了解为何此组合快速、准确，并且适用于生产级工作负载。

## 快速答案
- **“掩码敏感数据”是什么意思？** 它将已识别的机密文本替换为占位符（例如 `[REDACTED]`）。
- **哪个库负责 OCR？** Microsoft Azure OCR connector, used through GroupDocs Redaction.
- **我需要许可证吗？** 免费试用可用于评估；生产环境需要永久许可证。
- **我可以对扫描的 PDF 进行脱敏吗？** 可以——OCR 在应用正则表达式脱敏之前提取隐藏文本。
- **此解决方案仅限 Java 吗？** 示例基于 Java，但 GroupDocs 为 .NET 和其他平台提供了类似的 API。

## 什么是基于 OCR 的脱敏？
基于 OCR 的脱敏首先对每页运行 OCR，将图像转换为可搜索的文本，然后应用正则表达式模式，用类似 `[REDACTED]` 的掩码替换匹配项。此两步流程让您即使在扫描的 PDF 中也能可靠地隐藏个人数据，确保在文档共享或归档之前删除所有敏感字符串。

## 为什么将 GroupDocs Redaction 与 Azure OCR 结合使用？
您应该将 GroupDocs Redaction 与 Azure OCR 结合使用，因为它在印刷文本上提供 **>98 % 的 OCR 准确率**，支持 **50 多种输入和输出格式**，并且能够在 **不将整个文件加载到内存中** 的情况下处理 **数百页的 PDF**，确保合规的快速、可扩展脱敏。该解决方案还 **能够在 8 核服务器上在 2 分钟内处理 1,000 页的 PDF**，使批量作业变得实用。

## 前置条件
- **Java Development Kit (JDK) 8+** 已安装。  
- **Maven**（如果您偏好依赖管理）或手动下载 JAR 的能力。  
- **Microsoft Azure OCR 凭证**（端点和订阅密钥）。  
- 基本的 Java 知识以及对正则表达式的熟悉。

## 为 Java 设置 GroupDocs Redaction

### Maven 设置
将 GroupDocs 仓库和依赖添加到您的 `pom.xml` 中：

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
如果您更喜欢手动管理 JAR，请从 [GroupDocs.Redaction for Java 发布版](https://releases.groupdocs.com/redaction/java/) 获取最新发布版本。

### 许可证获取
- **免费试用** – 免费探索所有功能。  
- **临时许可证** – 延长评估时间。  
- **完整许可证** – 解锁生产就绪功能。

### 基本初始化和设置
`Redactor` 类是执行 OCR 提取并对 PDF 文档应用脱敏规则的核心引擎。

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.RedactorSettings;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.examples.java.helper_classes.MicrosoftAzureOcrConnector;

// Initialize the OCR connector with Microsoft Azure
RedactorSettings settings = new RedactorSettings(new MicrosoftAzureOcrConnector());
```

## 如何使用 OCR 脱敏掩码敏感数据
使用 OCR 脱敏掩码敏感数据的过程包括使用 Azure OCR 设置加载 PDF，定义要隐藏的数据的正则表达式模式，并调用 Redactor 将每个匹配项替换为类似 `[REDACTED]` 的占位符。该库在单一工作流中处理 OCR、模式匹配和 PDF 重写。

### 步骤 1：使用 OCR 设置加载文档
`LoadOptions` 配置 GroupDocs 加载文件的方式，允许您传入如 Azure 等 OCR 连接器。

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;

// Load your document with OCR settings
try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf", 
    new LoadOptions(), settings)) {
    // Further operations will go here
}
```
- **`YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf`** – 替换为您的 PDF 路径。  
- **`settings`** – 包含您之前创建的 Azure OCR 连接器。

### 步骤 2：定义并应用正则表达式脱敏
`ReplacementOptions` 指定在脱敏期间将替换每个正则匹配的文本。

```java
import com.groupdocs.redaction.redactions.RegexRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

// Define the regex for sensitive data (e.g., Social Security Numbers)
RegexRedaction redaction = new RegexRedaction("\\b\\d{3}-\\d{2}-\\d{4}\\b", 
    new ReplacementOptions("[REDACTED]"));

// Apply redaction
redactor.apply(redaction);

// Save the document after redactions
redactor.save(new SaveOptions());
```
- 模式 `\b\d{3}-\d{2}-\d{4}\b` 匹配美国社会安全号码。  
- `ReplacementOptions("[REDACTED]")` 将每个匹配替换为掩码，实质上 **掩码敏感数据**。

## 掩码敏感数据的常见使用场景
1. **法律文档管理** – 在共享草稿前隐藏客户标识符。  
2. **财务报告** – 保护账户号码和交易 ID。  
3. **医疗记录** – 通过脱敏患者标识符遵守 HIPAA。  
4. **政府出版物** – 从公共记录中删除个人数据。  
5. **企业合同** – 在外部审查期间隐藏专有条款。

## 性能技巧
- **优化正则表达式** – 避免过于宽泛的模式导致处理时间增加；精心编写的表达式可将运行时间缩短最多约 40 %。  
- **内存管理** – 及时关闭 `Redactor` 实例（try‑with‑resources 会自动完成）。  
- **异步执行** – 对于批量处理，在独立线程上运行脱敏任务或使用任务队列以保持 UI 响应。

## 故障排除
- **Azure 凭证错误** – 再次检查 `MicrosoftAzureOcrConnector` 中的端点 URL 和订阅密钥。  
- **文档未加载** – 验证文件路径并确保 PDF 未受密码保护（或通过 `LoadOptions` 提供密码）。  
- **未应用脱敏** – 首先使用简单字符串测试正则表达式；在单元测试中使用 `Pattern.compile` 确认匹配。

## 常见问题

**Q: 什么是 OCR 脱敏？**  
A: OCR 脱敏使用光学字符识别从图像或扫描的 PDF 中提取隐藏文本，然后应用脱敏规则对该文本进行掩码处理。

**Q: 我可以在没有 Azure OCR 的情况下使用 GroupDocs Redaction 吗？**  
A: 可以，但在原生文本提取失败的扫描文档上，OCR 能显著提升准确性。

**Q: 我该如何处理复杂的正则表达式模式？**  
A: 逐步构建并测试它们，在将其应用于大型文档之前，在沙箱中使用 Java 的 `Pattern` 类进行验证。

**Q: 常见的性能瓶颈是什么？**  
A: 大型 PDF、过于复杂的正则表达式以及同步 OCR 调用会导致处理变慢；考虑批量处理和优化的模式。

**Q: 是否提供实现问题的支持？**  
A: 当然——通过 [GroupDocs 论坛](https://forum.groupdocs.com/c/redaction/33) 获取社区帮助或联系 GroupDocs 支持。

## 其他资源
- **文档**: https://docs.groupdocs.com/redaction/java/  
- **API 参考**: https://reference.groupdocs.com/redaction/java  
- **下载**: https://releases.groupdocs.com/redaction/java/  
- **GitHub**: https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java  
- **免费支持**: https://forum.groupdocs.com/c/redaction/33  
- **临时许可证**: https://purchase.groupdocs.com/temporary-license/

---

**最后更新：** 2026-06-26  
**测试环境：** GroupDocs.Redaction 24.9 (Java)  
**作者：** GroupDocs  

## 相关教程

- [使用 OCR 的安全 PDF 脱敏 – GroupDocs.Redaction Java](/redaction/java/ocr-integration/)
- [如何使用 GroupDocs.Redaction for Java 脱敏文本](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction/)
- [Java 掩码敏感数据 – 使用 GroupDocs.Redaction 脱敏个人信息](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)