---
date: '2026-08-09'
description: 了解如何使用 GroupDocs.Redaction Java API 在 Excel 电子表格中隐藏个人数据并掩码电子邮件地址。
keywords:
- how to hide personal data
- mask email addresses excel
- GroupDocs.Redaction Java
- Excel redaction tutorial
lastmod: '2026-08-09'
og_description: 逐步了解如何使用 GroupDocs.Redaction Java API 在 Excel 文件中隐藏个人数据并掩码电子邮件地址——一种快速、安全的
  GDPR 合规解决方案。
og_image_alt: Guide showing Java code that redacts email addresses in an Excel spreadsheet
og_title: 如何使用 GroupDocs Java 在 Excel 中隐藏个人数据
schemas:
- author: GroupDocs
  dateModified: '2026-08-09'
  description: Learn how to hide personal data and mask email addresses in Excel spreadsheets
    using the GroupDocs.Redaction Java API.
  headline: How to hide personal data in Excel with GroupDocs Java
  type: TechArticle
- description: Learn how to hide personal data and mask email addresses in Excel spreadsheets
    using the GroupDocs.Redaction Java API.
  name: How to hide personal data in Excel with GroupDocs Java
  steps:
  - name: '**Partner data exchange** – Automatically strip customer emails before
      sending spreadsheets to vendors.'
    text: '**Partner data exchange** – Automatically strip customer emails before
      sending spreadsheets to vendors.'
  - name: '**Internal audit preparation** – Anonymize employee data during compliance
      reviews.'
    text: '**Internal audit preparation** – Anonymize employee data during compliance
      reviews.'
  - name: '**Scheduled reporting** – Embed the redaction step into nightly batch jobs
      that generate distribution‑ready reports.'
    text: '**Scheduled reporting** – Embed the redaction step into nightly batch jobs
      that generate distribution‑ready reports.'
  type: HowTo
- questions:
  - answer: Extend the pattern to include additional allowed characters (e.g., “+”
      or “_”) and test against a larger sample set, then re‑run the redaction.
    question: My regex still misses some corporate email formats. What should I do?
  - answer: Yes. Create a separate `CellFilter` for each column and invoke `redactor.apply`
      for each filter sequentially.
    question: Can I redact more than one column in a single pass?
  - answer: The library processes sheets incrementally, so files up to several gigabytes
      can be redacted as long as you enable streaming and close the `Redactor` after
      each file.
    question: Is GroupDocs.Redaction able to handle Excel files larger than 1 GB?
  - answer: Inspect the `RedactorChangeLog` returned by `apply`; a non‑failed status
      indicates success, while any errors are listed with line numbers and cell references.
    question: How do I capture redaction results or errors?
  - answer: Absolutely. Build the placeholder string dynamically (e.g., `"[redacted:"
      + UUID.randomUUID() + "]"`) and pass it to `ReplacementOptions`.
    question: Can I use a custom placeholder that includes a unique token per row?
  type: FAQPage
tags:
- hide personal data
- GroupDocs.Redaction
- Java Excel processing
- data privacy
title: 如何使用 GroupDocs Java 在 Excel 中隐藏个人数据
url: /zh/java/spreadsheet-redaction/redact-emails-excel-groupdocs-redaction-java/
weight: 1
---

# 如何在 Excel 中使用 GroupDocs Java 隐藏个人数据

在本指南中，您将学习**如何隐藏个人数据**——具体而言是电子邮件地址——通过使用 GroupDocs.Redaction Java API 对 Excel 工作簿进行处理。无论您需要遵守 GDPR、CCPA 或内部隐私政策，此方法都可以安全地自动化脱敏，保持原始文件不变，并生成可供分发的干净版本。

## 快速答案
- **“隐藏个人数据”是什么意思？** 它指的是永久性地掩盖或删除文件中的个人可识别信息（PII），使其不再可读取。  
- **哪个库执行脱敏？** GroupDocs.Redaction for Java。  
- **运行示例是否需要许可证？** 免费试用可用于测试；商业使用需要生产级许可证。  
- **我可以自定义占位符文本吗？** 可以——您可以将电子邮件替换为任意字符串，例如 “[redacted email]”。  
- **此方法适用于大型电子表格吗？** 适用，只要您遵循“性能考虑”章节中的性能提示。

## 什么是隐藏个人数据？
**隐藏个人数据**指对任何能够直接或间接识别个人的信息（如姓名、电话号码或电子邮件地址）进行不可逆的删除或掩盖。此过程确保生成的文件无法用于重新识别主体。

## 为什么使用 GroupDocs.Redaction for Java？
GroupDocs.Redaction 支持 **30 多种输入和输出格式**，并且能够在不将整个文件加载到内存的情况下处理 **多达 500,000 行** 的工作簿，与朴素的文件解析方案相比，可实现 **最高 80 % 的内存占用降低**。这些量化的优势使其成为企业级数据隐私流水线的首选。

## 前置条件
- Java Development Kit (JDK) 8 或更高版本。  
- 基本了解 Maven 构建文件。  
- 获取 GroupDocs.Redaction Java 库（可通过 Maven 或官方发布页面下载）。

## 设置 GroupDocs.Redaction for Java

### 如何将 GroupDocs.Redaction 添加到 Maven 项目中？
将 GroupDocs 仓库和 Redaction 依赖添加到您的 `pom.xml` 文件中（参见 [GroupDocs.Redaction releases](https://releases.groupdocs.com/redaction/java/)）。然后运行 `mvn clean install` 拉取构件。

```text
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
```

### 如何获取 GroupDocs.Redaction 的许可证？
GroupDocs 提供三种授权选项（参见 [GroupDocs’ website](https://purchase.groupdocs.com/temporary-license/)）：

- **免费试用** – 功能受限的评估，无需信用卡。  
- **临时许可证** – 从 GroupDocs 网站获取的 30 天评估密钥。  
- **完整许可证** – 通过销售门户购买的永久生产许可证。

```text
```java
import com.groupdocs.redaction.Redactor;

public class RedactEmails {
    public static void main(String[] args) {
        // Initialize the redactor with your document path
        try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_XLSX")) {
            // Your redaction logic will go here
        }
    }
}
```
```

## 实施指南

### 如何为 Excel 文件创建 Redactor 实例？
`Redactor` 类是加载文档并提供脱敏操作的主要入口点。  
实例化一个指向源工作簿的 `Redactor` 对象。`Redactor` 类是所有脱敏操作的入口点；它将文件加载到受管理的内存结构中，同时保持原始文件在磁盘上。

```text
```java
import com.groupdocs.redaction.Redactor;

public class RedactEmails {
    public static void main(String[] args) {
        try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_XLSX")) {
            // Proceed to the next steps for redaction
        }
    }
}
```
```

### 如何将脱敏限制在单个工作表和列上？
`CellFilter` 类允许您指定应检查脱敏的工作表和列。使用 `CellFilter` 来指定目标工作表名称和列索引。`CellFilter` 类在脱敏引擎评估之前过滤单元格，确保仅处理预期的单元格。

```text
```java
import com.groupdocs.redaction.redactions.CellFilter;

// Create and configure the filter
CellFilter filter = new CellFilter();
filter.setColumnIndex(1); // Targeting the second column (index starts at 0)
filter.setWorkSheetName("Customers"); // Specify the worksheet name
```
```

### 如何定义匹配大多数电子邮件地址的正则表达式模式？
`java.util.regex` 中的 `Pattern` 类表示用于匹配文本的编译正则表达式。创建一个包含捕获典型电子邮件格式的正则表达式的 `Pattern` 对象。下面的模式匹配大多数符合 RFC‑5322 的地址，同时忽略格式错误的字符串。

```text
```java
import java.util.regex.Pattern;

// Define regex pattern for matching emails
Pattern expression = Pattern.compile("^\\w+([-+.']\\w+)*@\\w+([-.]\\w+)*\\.\\w+([-.]\\w+)*$");
```
```

### 如何应用脱敏并用占位符替换电子邮件？
`ReplacementOptions` 类定义匹配内容的替换方式，例如占位符文本。将过滤器、模式和 `ReplacementOptions` 实例组合使用。`ReplacementOptions` 类允许您设置将在每个脱敏单元格中出现的确切占位符文本。

```text
```java
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.RedactorChangeLog;
import com.groupdocs.redaction.redactions.CellColumnRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

// Apply redaction
RedactorChangeLog result = redactor.apply(new CellColumnRedaction(filter, expression, new ReplacementOptions("[customer email]")));

// Save changes if successful
if (result.getStatus() != RedactionStatus.Failed) {
    SaveOptions saveOptions = new SaveOptions();
    saveOptions.setAddSuffix(true); // Add a suffix to the saved file name
    redactor.save(saveOptions);
}
```
```

## 常见陷阱与故障排除

- **正则表达式未覆盖所有情况** – 在代表性的数据样本上测试该表达式，并根据需要调整字符类。  
- **列索引错误** – 请记住列索引从 0 开始；列 B 的索引是 1。  
- **工作表名称区分大小写** – 使用 Excel 中显示的确切工作表名称；“Customers” ≠ “customers”。  
- **资源泄漏** – 将 `Redactor` 包装在 try‑with‑resources 块中（如示例所示），以确保本地资源及时释放。

## 为什么在 Excel 中隐藏个人数据？
在 Excel 中隐藏个人数据会删除所有个人可识别信息，确保文件无法用于追踪个人。这保护了隐私，满足监管要求，并防止在与外部方共享电子表格或公开发布数据时意外泄露。

- **合规监管** – 满足 GDPR、CCPA 以及行业特定的隐私要求。  
- **风险缓解** – 防止在与外部合作伙伴共享文件时意外暴露 PII。  
- **审计准备** – 通过永久删除归档数据集中的敏感值，保持干净、不可变的审计轨迹。

## 实际应用

1. **合作伙伴数据交换** – 在将电子表格发送给供应商之前自动剥离客户电子邮件。  
2. **内部审计准备** – 在合规审查期间对员工数据进行匿名化处理。  
3. **定时报告** – 将脱敏步骤嵌入生成可分发报告的夜间批处理作业中。

## 性能考虑

- **批量处理** – 在多个文件之间复用单个 `Redactor` 实例，以减少 JVM 开销。  
- **内存管理** – API 一次处理一个工作表；对于超过 100 MB 的工作簿，分块处理行以保持堆使用量低。  
- **大数据集** – 处理超过 10 万行的文件时，启用流式模式（在 24.9 版中可用），将内存消耗保持在 200 MB 以下。

## 常见问题

**问：我的正则仍然遗漏了一些公司电子邮件格式。我该怎么办？**  
**答：** 将模式扩展以包含更多允许的字符（例如 “+” 或 “_”），并在更大的样本集上进行测试，然后重新运行脱敏。

**问：我能在一次运行中脱敏多个列吗？**  
**答：** 可以。为每一列创建单独的 `CellFilter`，并依次对每个过滤器调用 `redactor.apply`。

**问：GroupDocs.Redaction 能处理大于 1 GB 的 Excel 文件吗？**  
**答：** 该库增量处理工作表，只要启用流式模式并在每个文件处理后关闭 `Redactor`，即可对数 GB 大小的文件进行脱敏。

**问：我如何获取脱敏结果或错误？**  
**答：** 检查 `apply` 返回的 `RedactorChangeLog`；非失败状态表示成功，任何错误都会列出行号和单元格引用。

**问：我能使用包含每行唯一标记的自定义占位符吗？**  
**答：** 完全可以。动态构建占位符字符串（例如 `"[redacted:" + UUID.randomUUID() + "]"`），并将其传递给 `ReplacementOptions`。

## 附加资源

- [Documentation](https://docs.groupdocs.com/redaction/java/)
- [API Reference](https://reference.groupdocs.com/redaction/java)
- [Download GroupDocs.Redaction](https://releases.groupdocs.com/redaction/java/)
- [GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
- [Free Support Forum](https://forum.groupdocs.com/c/redaction/33)
- [Temporary License Information](https://purchase.groupdocs.com/temporary-license/)

---

**最后更新：** 2026-08-09  
**测试环境：** GroupDocs.Redaction 24.9 for Java  
**作者：** GroupDocs

## 相关教程

- [如何在电子表格中筛选数据 – GroupDocs.Redaction Java](/redaction/java/spreadsheet-redaction/)
- [在 Java 中掩码敏感数据 – 使用 GroupDocs.Redaction 脱敏个人信息](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)
- [在 Java 中掩码敏感数据 – GroupDocs.Redaction 指南](/redaction/java/getting-started/)