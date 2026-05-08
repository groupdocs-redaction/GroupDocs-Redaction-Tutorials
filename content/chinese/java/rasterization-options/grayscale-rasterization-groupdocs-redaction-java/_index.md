---
date: '2026-02-13'
description: 了解如何使用 GroupDocs.Redaction for Java 创建灰度 PDF，安全地将 PDF 转换为灰度，同时保持文档质量。
keywords:
- GroupDocs.Redaction
- Java
- Document Processing
title: 如何使用 GroupDocs.Redaction Java 创建灰度 PDF – 保护并优化您的文档
type: docs
url: /zh/java/rasterization-options/grayscale-rasterization-groupdocs-redaction-java/
weight: 1
---

# GroupDocs.Redaction Java：灰度光栅化指南

## 介绍

如果您需要在保持文档安全且专业外观的同时 **创建灰度 PDF** 文件，那么您来对地方了。在本教程中，我们将逐步演示如何使用 GroupDocs.Redaction for Java 将彩色的 DOCX、PDF 或其他受支持的文件转换为干净的灰度光栅化版本。您将了解光栅化为何能增加额外的安全层、如何配置库以及如何高效管理资源——全部以对话式、一步一步的方式进行。

## 快速回答
- **灰度光栅化的作用是什么？** 它将文档的每一页转换为高分辨率图像，然后应用灰度滤镜，去除所有颜色信息。  
- **为什么要使用 GroupDocs.Redaction 来实现？** 它在单一 API 中结合了编辑遮蔽安全性和强大的光栅化选项。  
- **支持哪些格式？** DOCX、PDF、XLSX、PPTX、RTF 等众多格式。  
- **是否需要许可证？** 生产环境使用需要有效的 GroupDocs.Redaction 许可证；提供试用版用于测试。  
- **需要哪个 Java 版本？** JDK 8 或更高版本。

## 什么是 **create grayscale pdf**？

创建灰度 PDF 意味着将原始文档的每个视觉元素转换为灰色调。其结果是一个更小、适合打印的文件，消除了颜色带来的干扰，并因内容变为基于图像而带来轻微的安全优势。

## 为什么在 GroupDocs.Redaction 中使用灰度光栅化？

- **增强的安全性** – 光栅化的页面无法被选中、复制或编辑为文本。  
- **一致的外观** – 颜色被去除，呈现统一、专业的外观。  
- **广泛的格式支持** – 同一 API 可用于 DOCX、PDF、PPTX 等。  
- **精细的控制** – 您可以调整 DPI、输出格式以及诸如灰度转换等高级选项。

## 前置条件

- Java Development Kit (JDK) 8 或更高版本。使用 `java -version` 验证。  
- 一个 IDE（IntelliJ IDEA、Eclipse 或 NetBeans），以便更轻松地编码和调试。  
- 通过 Maven 或 Gradle 添加 GroupDocs.Redaction for Java。  
- 一个示例文档（例如多页 DOCX），您可以安全地进行实验。  
- 足够的磁盘空间用于光栅化输出（光栅文件可能比源文件更大）。

## 导入包

设置正确的导入就像在项目开始前整理工具箱。以下导入为您提供对核心 Redactor 类和我们将需要的光栅化选项的访问。

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.options.RasterizationOptions;
import com.groupdocs.redaction.options.AdvancedRasterizationOptions;
```

## 步骤 1：初始化 Redactor 对象

创建 `Redactor` 实例即可开启所有文档处理功能的大门。

```java
final Redactor redactor = new Redactor(Constants.MULTIPAGE_SAMPLE_DOCX);
```

将 `Constants.MULTIPAGE_SAMPLE_DOCX` 替换为您想要转换为灰度 PDF 的文件路径。

## 步骤 2：配置保存选项

`SaveOptions` 定义最终文件的写入方式。添加后缀有助于保持原始文件不变。

```java
SaveOptions so = new SaveOptions();
so.setRedactedFileSuffix("_scan");
```

输出文件将命名为 `yourfile_scan.docx`（或您随后指定的格式）。

## 步骤 3：启用光栅化

开启光栅化后，引擎将在保存前将每页渲染为图像。

```java
so.getRasterization().setEnabled(true);
```

光栅化是创建灰度 PDF 的基础，因为它将文档转换为基于图像的表示。

## 步骤 4：应用灰度转换

现在我们向光栅化管道添加灰度滤镜。

```java
so.getRasterization().addAdvancedOption(AdvancedRasterizationOptions.Grayscale);
```

此选项强制每个像素以灰度渲染，为您提供所需的 **create grayscale pdf** 结果。

## 步骤 5：执行文档转换

`save` 调用会运行整个处理链。

```java
redactor.save(so);
```

此行执行后，您将在磁盘上找到一个全光栅化、灰度化并带有 `_scan` 后缀的新文件。

## 步骤 6：正确的资源管理

清理资源可防止文件锁定和内存泄漏。

```java
finally { redactor.close(); }
```

对于现代 Java，您也可以使用 try‑with‑resources 模式，它会自动关闭 `Redactor`：

```java
try (Redactor redactor = new Redactor(Constants.MULTIPAGE_SAMPLE_DOCX)) {
    // Your processing code here
}
// Automatic cleanup happens here
```

两种方法都安全；后者更简洁。

## 高级配置选项

### 调整 DPI 以平衡质量或大小

更高的 DPI 可产生更清晰的图像（适合打印），而较低的 DPI 可减小文件大小。

```java
saveOptions.getRasterization().setDpi(300); // High quality for printing
// or
saveOptions.getRasterization().setDpi(150); // Balanced quality and size
```

### 选择输出格式

您可以将光栅化结果强制为特定的容器格式，例如 PDF。

```java
saveOptions.setRasterizationFormat(RasterizationFormat.PDF);
```

## 常见使用场景

- **法律文档归档** – 创建不可编辑的不可变灰度 PDF。  
- **可直接打印的报告** – 确保批量打印时的黑白输出一致。  
- **合规工作流** – 将编辑遮蔽与灰度光栅化相结合，以满足严格的数据隐私法规。

## 常见问题及解决方案

| 问题 | 原因 | 解决方案 |
|------|------|----------|
| 输出文件比预期更大 | DPI 设置过高或未启用图像压缩 | 降低 DPI（例如 150）或在 `RasterizationOptions` 中启用压缩。 |
| 文本模糊 | 原始字体大小的 DPI 不足 | 将 DPI 提高到 300 或更高。 |
| 在大型文档上抛出 `OutOfMemoryError` | 整个文档加载到内存中 | 使用流式 API，或如果支持则分批处理页面。 |
| 未应用灰度 | 高级选项未正确添加 | 确认在 `save()` 之前调用 `addAdvancedOption(AdvancedRasterizationOptions.Grayscale)`。 |

## 常见问答

**问：我可以在不进行光栅化的情况下将文档转换为灰度吗？**  
**答：在 GroupDocs.Redaction 中，灰度选项与光栅化绑定，这确保了结果一致并增加了安全性。**

**问：哪些文档格式支持灰度光栅化？**  
**答：GroupDocs.Redaction 支持的所有主要格式——包括 DOCX、PDF、XLSX、PPTX、RTF 等——都可以光栅化并转换为灰度。**

**问：光栅化会影响文档的文件大小吗？**  
**答：会。文字密集的文件可能会增大，而图片密集的文件可能会缩小。DPI 设置影响最大。**

**问：是否可以逆转灰度光栅化过程？**  
**答：不能。光栅化是单向的；如果需要恢复，请保留原始文件的备份。**

**问：如何优化灰度光栅化文档的质量？**  
**答：使用更高的 DPI（打印质量建议 300 +），并选择合适的输出格式（PDF 常用于归档）。**

## 结论

现在，您已经拥有使用 GroupDocs.Redaction for Java **创建灰度 PDF** 文件的完整、可投入生产的方案。通过启用光栅化、添加灰度高级选项并负责任地管理资源，您可以生成安全、适合打印的文档，满足合规标准。

---

**最后更新：** 2026-02-13  
**测试环境：** GroupDocs.Redaction 23.11 for Java  
**作者：** GroupDocs