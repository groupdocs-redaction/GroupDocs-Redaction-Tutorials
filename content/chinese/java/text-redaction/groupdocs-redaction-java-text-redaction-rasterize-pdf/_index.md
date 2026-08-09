---
date: '2026-08-09'
description: 了解如何使用 GroupDocs.Redaction for Java 通过 redacting text 和 rasterizing PDFs
  来创建 non editable PDF 文件。
keywords:
- create non editable pdf
- how to redact text java
- GroupDocs.Redaction Java
- rasterized PDF Java
- document security Java
lastmod: '2026-08-09'
og_description: 使用 GroupDocs.Redaction for Java 通过 redacting text 和 rasterizing PDFs
  创建 non editable PDF 文件。遵循 step‑by‑step guide，了解 tips、pitfalls 和 FAQs。
og_image_alt: Guide showing how to redact text and generate a non‑editable rasterized
  PDF using GroupDocs.Redaction for Java
og_title: 使用 GroupDocs.Redaction Java 创建 non editable PDF
schemas:
- author: GroupDocs
  dateModified: '2026-08-09'
  description: Learn how to create non editable PDF files by redacting text and rasterizing
    PDFs using GroupDocs.Redaction for Java.
  headline: How to create non editable PDF with GroupDocs.Redaction Java
  type: TechArticle
- description: Learn how to create non editable PDF files by redacting text and rasterizing
    PDFs using GroupDocs.Redaction for Java.
  name: How to create non editable PDF with GroupDocs.Redaction Java
  steps:
  - name: Import the required classes
    text: '`ExactPhraseRedaction` is a redaction rule that targets a literal string.
      `ReplacementOptions` tells the engine what placeholder to insert instead of
      the original text.'
  - name: Apply exact phrase redaction
    text: 'The following snippet replaces every occurrence of **“John Doe”** with
      the placeholder **[personal]**: **Why this works:** - `ExactPhraseRedaction`
      targets the literal string “John Doe”. - `ReplacementOptions` tells the engine
      what to insert instead of the original text. **Tips & common pitfalls** -'
  - name: Import `SaveOptions`
    text: '`SaveOptions` configures how the document is saved, including rasterization
      and file‑naming options.'
  - name: Configure and save the rasterized PDF
    text: The snippet below disables the automatic “_redacted” suffix, enables rasterization,
      and writes the output file. **Explanation:** - `setAddSuffix(false)` keeps the
      original file name (you can enable it to add “_redacted”). - `setRasterizeToPDF(true)`
      tells GroupDocs to render each page as an image in
  type: HowTo
- questions:
  - answer: It replaces a specific string (e.g., a name) with a placeholder, ensuring
      the original text cannot be recovered.
    question: What is an exact phrase redaction?
  - answer: Rasterized PDFs render each page as an image, preventing text selection,
      copying, or editing.
    question: How does rasterizing a PDF improve security?
  - answer: Yes—loop over a list of file paths, reusing the same `Redactor` configuration
      for each document.
    question: Can I process multiple files in one run?
  - answer: Absolutely. You can read/write streams from AWS S3, Azure Blob, or Google
      Cloud Storage and feed them directly to the API.
    question: Is cloud integration possible?
  - answer: Forgetting to close the `Redactor` (which locks files) and using an outdated
      library version that lacks rasterization support.
    question: What are typical pitfalls for newcomers?
  type: FAQPage
tags:
- create non editable pdf
- GroupDocs.Redaction
- Java document redaction
- rasterized PDF
- compliance
title: 如何使用 GroupDocs.Redaction Java 创建 non editable PDF
type: docs
url: /zh/java/text-redaction/groupdocs-redaction-java-text-redaction-rasterize-pdf/
weight: 1
---

# 如何使用 GroupDocs.Redaction Java 创建不可编辑的 PDF

在许多受监管的行业中，您必须交付不可被修改或复制的文档。确保这一点的最可靠方法是先对敏感文本进行 **创建不可编辑的 PDF** 文件，然后对整个文档进行光栅化。GroupDocs.Redaction for Java 为您提供单行 API 来执行这两个步骤，从而无需构建自定义 PDF 引擎即可满足合规要求。

## 快速答案
- **“redact text” 是什么意思？** 它永久删除或遮蔽敏感字符串，使其无法被读取或恢复。  
- **哪个库负责此工作？** GroupDocs.Redaction for Java 提供内置的脱敏和光栅化功能。  
- **我需要许可证吗？** 免费试用可用于测试；生产环境需要永久许可证。  
- **我能在一步中将 DOCX 转换为光栅化的 PDF 吗？** 可以——先进行脱敏，然后使用启用光栅化的 `SaveOptions`。  
- **输出真的不可编辑吗？** 光栅化的 PDF 以图像形式呈现，防止文本提取或修改。

## 什么是文本脱敏？
文本脱敏永久删除或遮蔽机密信息——例如个人标识符、财务数据或法律条款——从文档中。不同于简单的查找替换，脱敏确保隐藏的内容无法被任何工具恢复。通过擦除原始字符并可选地用占位符替代，脱敏保证敏感数据不可恢复，且文档对授权用户仍可阅读。

## 为什么使用 GroupDocs.Redaction for Java？
GroupDocs.Redaction for Java 提供全面的功能集，简化安全文档处理。它支持多种文件格式，提供多种脱敏类型，并包含一键光栅化以锁定 PDF。该库针对性能进行优化，可在 Windows 和 Linux 上运行，并能轻松集成到现有的 Java 应用程序中，是需要大规模保护敏感信息的企业的可靠选择。

## 前置条件
- Java Development Kit (JDK 11 或更高) 和如 IntelliJ IDEA 或 Eclipse 的 IDE。  
- GroupDocs.Redaction 库（版本 24.9 或更高）。  
- 基本的 Java 知识——您只需编写少量简短代码片段。

## 设置 GroupDocs.Redaction for Java

### Maven 安装
将 GroupDocs 仓库和依赖添加到您的 `pom.xml`：

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
如果您不使用 Maven，也可以从官方发布页面获取 JAR： [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/)。

#### 许可证获取
- **免费试用** – 免费探索 API。  
- **临时许可证** – 适合长期测试。  
- **完整许可证** – 生产部署所需。

## 基本初始化
`Redactor` 是 GroupDocs.Redaction 的核心类，用于在内存中加载和修改文档。导入命名空间后，使用源文件路径实例化 `Redactor`，即可准备好应用脱敏规则。

```java
import com.groupdocs.redaction.Redactor;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

## 实施指南

## 如何在 Java 中创建不可编辑的 PDF？
加载源文档，应用所需的脱敏规则，然后在启用光栅化的情况下保存结果。这个三步流程——加载、脱敏、光栅化——生成的 PDF 无法编辑、复制或搜索，满足最严格的合规标准。通过将每页转换为图像，最终文件消除了任何可能被后续提取的隐藏文本层。

## 如何在 Java 中脱敏文本
下面我们演示精确短语脱敏，非常适合删除已知标识符，如个人姓名。该过程包括导入必要的类、定义脱敏规则，并在保存前将其应用于文档。

### 步骤 1：导入所需类
`ExactPhraseRedaction` 是针对字面字符串的脱敏规则。`ReplacementOptions` 指定引擎在原始文本位置插入的占位符。

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;
```

### 步骤 2：应用精确短语脱敏
以下代码片段将所有出现的 **“John Doe”** 替换为占位符 **[personal]**：

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
try {
    redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]"));
} finally { 
    redactor.close(); 
}
```

**为什么这样有效：**  
- `ExactPhraseRedaction` 针对字面字符串 “John Doe”。  
- `ReplacementOptions` 告诉引擎在原始文本位置插入什么。

**提示与常见陷阱**  
- 仔细检查文档路径；路径错误会触发 `FileNotFoundException`。  
- 确保 Java 进程对输出文件夹具有写入权限。

## 如何保存为光栅化 PDF
脱敏后，您可能需要一个不可编辑的 PDF。光栅化将每页转换为图像，去除选择或编辑文本的能力。此步骤确保最终 PDF 像扫描件一样，抵御文本提取工具和意外修改。

### 步骤 1：导入 `SaveOptions`
`SaveOptions` 配置文档的保存方式，包括光栅化和文件命名选项。

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
```

### 步骤 2：配置并保存光栅化 PDF
下面的代码片段禁用自动的 “_redacted” 后缀，启用光栅化，并写入输出文件。

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
try {
    SaveOptions tmp0 = new SaveOptions();
    tmp0.setAddSuffix(false);
    tmp0.setRasterizeToPDF(true);

    redactor.save(tmp0);
} finally { 
    redactor.close(); 
}
```

**说明：**  
- `setAddSuffix(false)` 保持原始文件名（可启用以添加 “_redacted”）。  
- `setRasterizeToPDF(true)` 告诉 GroupDocs 将每页渲染为 PDF 中的图像，确保文档 **不可编辑**。

**故障排除**  
- 如果光栅化失败，请确认 Java 运行时包含 PDF 渲染依赖（这些已随库打包）。

## 实际应用
1. **法律文件处理** – 在与对方律师共享之前脱敏客户姓名。  
2. **人力资源记录管理** – 在内部报告中隐藏员工编号。  
3. **财务报告** – 在分发审计摘要时保护账号信息。  

您可以将这些步骤串联成自动化工作流，将 GroupDocs.Redaction 与文档管理系统或云存储桶集成。

## 性能考虑因素
- **批量处理：** 处理大量文件时复用单个 `Redactor` 实例，可将开销降低至 40 %。  
- **内存管理：** 对于大文档，在每次 `redactor.close()` 后调用 `System.gc()`，或在单独的 JVM 中运行该过程。  
- **保持依赖更新：** 新版本通常包含 PDF 光栅化的性能改进，包括对多核系统的 20 % 加速。

## 常见问题及解决方案
| Issue | Solution |
|-------|----------|
| *未找到文件* | 验证绝对路径并确保服务器上存在该文件。 |
| *权限被拒绝* | 以足够的操作系统权限运行 JVM，或更改输出文件夹的 ACL。 |
| *光栅化产生空白页* | 确认源文档不是已经是光栅图像；使用最新的库版本。 |
| *脱敏后仍有隐藏文本* | 使用带 `ReplacementOptions` 的 `ExactPhraseRedaction`；避免使用简单的查找替换方法。 |

## 常见问题
**问：什么是精确短语脱敏？**  
答：它将特定字符串（例如姓名）替换为占位符，确保原始文本无法恢复。

**问：光栅化 PDF 如何提升安全性？**  
答：光栅化的 PDF 将每页渲染为图像，防止文本选择、复制或编辑。

**问：我能一次处理多个文件吗？**  
答：可以——遍历文件路径列表，对每个文档复用相同的 `Redactor` 配置。

**问：可以进行云集成吗？**  
答：完全可以。您可以从 AWS S3、Azure Blob 或 Google Cloud Storage 读取/写入流，并直接传递给 API。

**问：新手常见的陷阱有哪些？**  
答：忘记关闭 `Redactor`（会锁定文件）以及使用缺少光栅化支持的旧版库。

## 资源
- **文档：** [GroupDocs Redaction Java Documentation](https://docs.groupdocs.com/redaction/java/)  
- **API 参考：** [GroupDocs Redaction API Reference](https://reference.groupdocs.com/redaction/java)  
- **下载：** [Latest Releases](https://releases.groupdocs.com/redaction/java/)  
- **GitHub：** [GroupDocs.Redaction GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **免费支持：** [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)  
- **临时许可证：** [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**最后更新：** 2026-08-09  
**测试环境：** GroupDocs.Redaction 24.9 for Java  
**作者：** GroupDocs  

## 相关教程
- [如何使用 GroupDocs.Redaction Java 创建灰度 PDF – 安全与优化文档](/redaction/java/rasterization-options/grayscale-rasterization-groupdocs-redaction-java/)
- [精通 Java 文档安全：精确短语脱敏与高级光栅化，使用 GroupDocs.Redaction](/redaction/java/advanced-redaction/groupdocs-redaction-java-document-security/)
- [如何将 DOCX 转换为图像并使用 GroupDocs Redaction Java 脱敏 Word 文档](/redaction/java/document-saving/groupdocs-redaction-java-rasterize-word-docs/)