---
date: 2026-08-04
description: 了解如何使用 GroupDocs.Redaction for Java 过滤电子表格数据 Java，并安全地对 Excel 电子表格中的列或单元格进行遮蔽。
keywords:
- filter spreadsheet data java
- hide sensitive data excel
- GroupDocs.Redaction Java
- spreadsheet redaction
lastmod: 2026-08-04
og_description: 了解如何使用 GroupDocs.Redaction for Java 过滤电子表格数据 Java，并安全地对 Excel 电子表格中的列或单元格进行遮蔽。
og_image_alt: Guide showing how to filter spreadsheet data in Java using GroupDocs.Redaction
og_title: 过滤电子表格数据 Java – 使用 GroupDocs.Redaction 的指南
schemas:
- author: GroupDocs
  dateModified: '2026-08-04'
  description: Learn how to filter spreadsheet data java and securely redact columns
    or cells in Excel spreadsheets using GroupDocs.Redaction for Java.
  headline: Filter spreadsheet data java – guide with GroupDocs.Redaction
  type: TechArticle
- description: Learn how to filter spreadsheet data java and securely redact columns
    or cells in Excel spreadsheets using GroupDocs.Redaction for Java.
  name: Filter spreadsheet data java – guide with GroupDocs.Redaction
  steps:
  - name: instantiate the filter
    text: '`RedactionFilter` is the core class that represents a filtering rule for
      spreadsheet redaction. It accepts column numbers, row numbers, or custom lambda
      expressions to pinpoint data.'
  - name: configure the condition
    text: Use `filter.setColumnIndex(1)` to target column B (zero‑based) and `filter.setRegex("[A‑Z0‑9._%+-]+@[A‑Z0‑9.-]+\\.[A-Z]{2,}")`
      to match email patterns. You can also combine multiple conditions with `filter.and(...)`
      or `filter.or(...)`.
  - name: apply the redaction
    text: '`Redactor` is the main class that executes redaction operations on a workbook.
      Pass the workbook and the configured filter to the `Redactor` object. The API
      streams the workbook, applies the filter, and writes the redacted result to
      a new file, preserving original formatting and formulas.'
  type: HowTo
- questions:
  - answer: Yes, you can add additional column indexes to the same `RedactionFilter`
      instance or chain multiple filters with `filter.or(...)`.
    question: Can I filter multiple columns at once?
  - answer: Provide the password when opening the workbook; the filter operates after
      decryption just like on an unprotected file.
    question: Does the filter work on password‑protected workbooks?
  - answer: The engine is optimized for up to 1 million rows (≈500 MB) without loading
      the entire file into memory.
    question: How many rows can the API handle in a single operation?
  - answer: Yes, call `filter.preview(workbook)` to get a list of cell addresses that
      match the criteria.
    question: Is it possible to preview which cells will be redacted before saving?
  - answer: A full commercial license is required for production deployments; a temporary
      license is sufficient for testing and evaluation.
    question: What licensing model is required for production use?
  type: FAQPage
tags:
- filter spreadsheet data
- GroupDocs.Redaction
- Java spreadsheet redaction
- hide sensitive data excel
- data privacy
title: 过滤电子表格数据 Java – 使用 GroupDocs.Redaction 的指南
type: docs
url: /zh/java/spreadsheet-redaction/
weight: 12
---

# 过滤电子表格数据 java – GroupDocs.Redaction Java 教程

如果您需要在应用遮蔽之前**filter spreadsheet data java**，您来对了指南。在本教程中，您将了解如何隔离包含个人或机密信息的行、列或单元格，然后使用 GroupDocs.Redaction for Java 安全地进行遮蔽。步骤以通俗语言解释，包含最佳实践提示，并展示如何在大型工作簿上保持快速处理。

## 快速答案
- **哪个库在 Java 中处理电子表格遮蔽？** GroupDocs.Redaction for Java.  
- **我可以在不将整个文件加载到内存的情况下过滤行吗？** Yes – the API streams data and lets you apply filters on the fly.  
- **支持哪些文件格式？** Over 30 spreadsheet formats, including XLS, XLSX, CSV, and ODS.  
- **开发是否需要许可证？** A temporary license works for testing; a full license is required for production.  
- **工作簿大小是否有限制？** The engine can process files up to 500 MB without excessive memory consumption.

## 什么是 filter spreadsheet data java？
**Filter spreadsheet data java** 是一种使用 Java 代码以编程方式选择 Excel 样式工作簿中的特定行、列或单元格的过程，以便仅检查或遮蔽目标内容。此技术可降低运行时间，限制不必要的更改，并帮助满足 GDPR 类合规性。

## 为什么要过滤 filter spreadsheet data java？
GroupDocs.Redaction Java 支持 **30+ 电子表格格式**，并且能够处理包含 **最高 500 MB**（约 100 万行）的工作簿，同时将内存使用保持在 **200 MB** 以下。通过先进行过滤，您可以避免触及无关数据，从而在典型的隐私清理场景中平均将处理时间缩短 **40‑60 %**。

## 前置条件
- 已安装 Java 17 或更高版本。  
- Maven 或 Gradle 构建系统。  
- GroupDocs.Redaction for Java（可从官方网站下载）。  
- 临时或正式许可证密钥。  

## 如何使用 GroupDocs.Redaction Java 过滤电子表格中的数据？
加载工作簿，定义匹配要遮蔽单元格的过滤器，然后执行遮蔽操作。API 以流式方式执行过滤，因此您无需将整个文件保存在 RAM 中。

`RedactionFilter` 类允许您指定列索引、行范围或自定义谓词。例如，您可以针对列 **B** 中包含电子邮件地址模式的每个单元格，或将遮蔽限制在“Status”列等于“Confidential”的行上。

**Direct answer (40‑70 words):**  
创建一个 `RedactionFilter` 实例，设置列索引和正则表达式条件，然后将过滤器传递给 `Redactor.redact(workbook, filter)`。此单行过滤器会隔离匹配您标准的确切单元格，遮蔽器会删除或掩码这些单元格，同时保持工作表的其余部分不受影响。该操作相对于过滤的行数以线性时间完成。

### 步骤 1：实例化过滤器
`RedactionFilter` 是表示电子表格遮蔽过滤规则的核心类。它接受列号、行号或自定义 lambda 表达式来精准定位数据。

### 步骤 2：配置条件
使用 `filter.setColumnIndex(1)` 来定位列 B（从零开始），并使用 `filter.setRegex("[A‑Z0‑9._%+-]+@[A‑Z0‑9.-]+\\.[A-Z]{2,}")` 来匹配电子邮件模式。您还可以使用 `filter.and(...)` 或 `filter.or(...)` 组合多个条件。

### 步骤 3：应用遮蔽
`Redactor` 是在工作簿上执行遮蔽操作的主要类。  
将工作簿和配置好的过滤器传递给 `Redactor` 对象。API 会流式处理工作簿，应用过滤器，并将遮蔽结果写入新文件，保留原始格式和公式。

## 常见问题及解决方案
- **过滤器未匹配到任何单元格：** 验证列索引（从零开始），并确保正则表达式语法对 Java 正确。  
- **大文件出现内存不足错误：** 适度增加 JVM 堆大小（例如 `-Xmx1g`），或在过滤前将工作簿拆分为更小的块。  
- **遮蔽输出失去格式：** `RedactionOptions` 允许自定义遮蔽行为，例如保留单元格格式。使用 `RedactionOptions.setPreserveFormatting(true)` 可保持单元格样式完整。

## 为什么要过滤电子表格数据？
在遮蔽之前进行过滤仅隔离工作簿的敏感部分，这意味着您可以避免对干净数据进行不必要的更改。这种选择性方法还降低了意外数据丢失的风险，并加快了合规审计，因为审计日志的条目大幅减少。

## 如何使用 GroupDocs.Redaction Java API 在 Excel 电子表格中遮蔽电子邮件
加载您的 Excel 文件，应用查找典型电子邮件模式的过滤器，然后调用遮蔽器。API 将每个匹配的电子邮件替换为类似 “***@***.com” 的占位符，同时保留周围单元格的布局。

## 如何过滤数据 – 可用教程
- [如何在 Excel 电子表格中使用 GroupDocs.Redaction Java API 遮蔽电子邮件](./redact-emails-excel-groupdocs-redaction-java/)

## 其他资源
- [GroupDocs.Redaction for Java 文档](https://docs.groupdocs.com/redaction/java/)
- [GroupDocs.Redaction for Java API 参考](https://reference.groupdocs.com/redaction/java/)
- [下载 GroupDocs.Redaction for Java](https://releases.groupdocs.com/redaction/java/)
- [GroupDocs.Redaction 论坛](https://forum.groupdocs.com/c/redaction/33)
- [免费支持](https://forum.groupdocs.com/)
- [临时许可证](https://purchase.groupdocs.com/temporary-license/)

---

**最后更新：** 2026-08-04  
**测试环境：** GroupDocs.Redaction 23.11 for Java  
**作者：** GroupDocs  

## 常见问题
**Q: 我可以一次过滤多个列吗？**  
A: 是的，您可以向同一个 `RedactionFilter` 实例添加额外的列索引，或使用 `filter.or(...)` 链接多个过滤器。

**Q: 过滤器能在受密码保护的工作簿上工作吗？**  
A: 打开工作簿时提供密码；过滤器在解密后工作，和未受保护的文件一样。

**Q: API 在单次操作中能处理多少行？**  
A: 引擎针对最高 1 百万行（≈500 MB）进行优化，无需将整个文件加载到内存中。

**Q: 是否可以在保存前预览将被遮蔽的单元格？**  
A: 可以，调用 `filter.preview(workbook)` 可获取匹配条件的单元格地址列表。

**Q: 生产使用需要什么许可模式？**  
A: 生产部署需要完整的商业许可证；临时许可证足以用于测试和评估。

## 相关教程
- [如何使用 GroupDocs.Redaction Java API 在 Excel 电子表格中遮蔽敏感数据](/redaction/java/spreadsheet-redaction/redact-emails-excel-groupdocs-redaction-java/)
- [Mask Sensitive Data Java – GroupDocs.Redaction 指南](/redaction/java/getting-started/)
- [Mask Sensitive Data Java – 使用 GroupDocs.Redaction 遮蔽个人信息](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)