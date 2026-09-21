---
date: '2026-09-21'
description: 了解如何使用 GroupDocs.Redaction for Java 对图像进行脱敏。分步指南涵盖设置、pixel‑level redaction、验证和最佳实践。
keywords:
- how to redact image
- Java image redaction
- GroupDocs.Redaction for Java
- scanned image redaction
- pixel redaction Java
lastmod: '2026-09-21'
og_description: 如何使用 GroupDocs.Redaction for Java 对图像进行脱敏。按照本指南在扫描文件中遮蔽像素数据、选择颜色并验证结果——完美满足
  GDPR 和 HIPAA 合规要求。
og_image_alt: Guide showing Java code that redacts scanned images using GroupDocs.Redaction
og_title: 如何使用 GroupDocs.Redaction for Java 对图像进行脱敏
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: Learn how to redact image with GroupDocs.Redaction for Java. Step‑by‑step
    guide covers setup, pixel‑level redaction, verification, and best practices.
  headline: How to redact image using GroupDocs.Redaction for Java
  type: TechArticle
- description: Learn how to redact image with GroupDocs.Redaction for Java. Step‑by‑step
    guide covers setup, pixel‑level redaction, verification, and best practices.
  name: How to redact image using GroupDocs.Redaction for Java
  steps:
  - name: define redaction parameters
    text: '`ImageAreaRedaction` works with a `Point` (top‑left corner) and a `Dimension`
      (width × height) that describe the rectangle to hide. In this example we use
      a blue fill color.'
  - name: apply redaction
    text: '`RegionReplacementOptions` lets you specify the fill color and optional
      border. Passing these options to `ImageAreaRedaction` and invoking `apply()`
      performs the masking. The method returns a `RedactorChangeLog` that indicates
      success or failure.'
  - name: release resources
    text: '`Redactor` implements `AutoCloseable`. Closing it frees native buffers
      and file handles, preventing memory leaks in long‑running services.'
  type: HowTo
- questions:
  - answer: '`ImageAreaRedaction` works on raw pixel coordinates, while text redaction
      parses OCR layers to locate and remove textual content.'
    question: What is the difference between `ImageAreaRedaction` and text redaction?
  - answer: Yes—call `redactor.apply()` repeatedly with different `ImageAreaRedaction`
      objects before saving the final file.
    question: Can I redact multiple regions in a single image?
  - answer: The library supports common raster formats (JPG, PNG, BMP, GIF). For TIFF,
      convert the image to a supported format first.
    question: Does GroupDocs.Redaction support other image formats like TIFF?
  - answer: Extract each page as an image, apply the same redaction logic, then rebuild
      the PDF using a PDF library such as GroupDocs.Conversion.
    question: How do I automate redaction for a folder of scanned PDFs?
  - answer: Render the `Redactor` to a `BufferedImage` and display it in a Swing or
      JavaFX UI, allowing you to confirm the masked area before committing.
    question: Is there a way to preview the redaction before saving?
  type: FAQPage
tags:
- image redaction
- GroupDocs
- Java
- document privacy
- data protection
title: 如何使用 GroupDocs.Redaction for Java 对图像进行脱敏
type: docs
url: /zh/java/image-redaction/java-image-redaction-groupdocs-tutorial/
weight: 1
---

# 如何使用 GroupDocs.Redaction for Java 对图像进行编辑

在本综合教程中，您将学习 **如何在 Java 中编辑图像** 文件，使用 GroupDocs.Redaction。对扫描图像进行编辑是保护个人数据、满足 GDPR、HIPAA 或其他隐私法规以及确保机密视觉信息不泄露的关键步骤。我们将带您完成项目设置、像素级编辑配置、安全保存结果以及确认编辑成功的全过程，全部以对话式、逐步的风格呈现，您可以将其复制到任何 Java 应用程序中。

## 快速答案
- **什么库在 Java 中处理图像编辑？** GroupDocs.Redaction for Java。  
- **我可以选择编辑颜色吗？** 可以——任何不透明的 `java.awt.Color`，例如 `Color.BLUE` 或 `Color.BLACK`。  
- **生产环境需要许可证吗？** 是的，商业使用必须拥有有效的 GroupDocs 许可证。  
- **原始图像会被覆盖吗？** 不会——API 会将编辑后的图像写入您指定的新文件。  
- **支持哪个 Java 版本？** Java 8 及更高版本（截至撰写时支持到 Java 21）。

## 什么是图像编辑以及为什么要编辑扫描的图像（Java）？
图像编辑通过用纯色替换像素区域，永久遮蔽视觉数据——姓名、号码、签名等。与针对可选字符的文本编辑不同，扫描图像以原始像素形式存储信息，只有基于像素的工具才能确保数据无法恢复。使用 GroupDocs.Redaction，您可以精准定位坐标，应用任意不透明颜色，并生成一个新图像，彻底移除敏感内容。

## 为什么使用 GroupDocs.Redaction for Java？
GroupDocs.Redaction 支持 **50+ 图像格式**（包括 JPG、PNG、BMP、GIF），并且能够在不将整个文件加载到内存的情况下处理数百页文档，这得益于其流式架构。基准测试显示，300 KB 的扫描 PNG 在典型 2.8 GHz CPU 上的编辑时间不足 120 ms，适用于批处理任务和实时服务。

## 前置条件
在开始之前，请确保您已具备：

- **JDK 8 或更高版本** 已安装并在 `PATH` 中配置。  
- **Maven**（或 Gradle）用于依赖管理。  
- 如 **IntelliJ IDEA**、**Eclipse** 或 **NetBeans** 等 IDE。  
- 对 Java 文件 I/O 和 `java.awt` 包有基本了解。  

## 设置 GroupDocs.Redaction for Java

### Maven 设置
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
或者，从官方发布页面下载最新 JAR： [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/)。

### 许可证获取
- **免费试用：** 注册试用以探索完整 API。  
- **临时许可证：** 使用临时密钥进行无限期测试，免费。  
- **正式购买：** 获取生产许可证以实现无限部署。

## 实现指南

我们将实现分为两个核心功能：**图像区域编辑**（实际遮蔽）和 **编辑状态检查**（验证成功）。

### 如何编辑扫描文档图像 – 步骤 1：初始化编辑器
`Redactor` 是加载图像并提供编辑操作的核心类。  
创建指向要处理的源图像的 `Redactor` 实例。

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_JPG");
```

### 步骤 2：定义编辑参数
`ImageAreaRedaction` 使用 `Point`（左上角）和 `Dimension`（宽×高）描述要隐藏的矩形区域。本例使用蓝色填充。

```java
// Define the position on the image where redaction starts.
Point samplePoint = new Point(385, 485);

// Define the size of the area to be redacted.
Dimension sampleSize = new Dimension(1793, 2069);
```

### 步骤 3：应用编辑
`RegionReplacementOptions` 让您指定填充颜色和可选边框。将这些选项传递给 `ImageAreaRedaction` 并调用 `apply()` 执行遮蔽。该方法返回一个 `RedactorChangeLog`，指示成功或失败。

```java
RedactorChangeLog result = redactor.apply(
    new ImageAreaRedaction(samplePoint, new RegionReplacementOptions(Color.BLUE, sampleSize))
);

// Check if the redaction was successful and save the output.
if (result.getStatus() != RedactionStatus.Failed) {
    redactor.save("YOUR_OUTPUT_DIRECTORY/redacted_output.jpg");
}
```

### 步骤 4：释放资源
`Redactor` 实现了 `AutoCloseable`。关闭它可释放本机缓冲区和文件句柄，防止长时间运行的服务出现内存泄漏。

```java
redactor.close();
```

### 如何验证编辑 – 状态检查
编辑完成后，检查 `RedactorChangeLog`。`Status.SUCCESS` 值表明像素区域已成功替换且无错误。您还可以将图像渲染为 `BufferedImage`，在保存前进行目视检查。

```java
if (result != null && result.getStatus() != RedactionStatus.Failed) {
    System.out.println("Redaction was successful.");
} else {
    System.out.println("Redaction failed.");
}
```

## 实际应用
- **机密文档处理：** 在与合作伙伴共享之前，对扫描的合同中的个人数据进行遮蔽。  
- **法律文档：** 通过编辑证据图像中的标识符，确保符合 GDPR 或 HIPAA。  
- **医疗记录：** 隐藏放射扫描中的患者面部或手写笔记，同时保留诊断细节。  

## 性能考虑
- **批量处理：** 将图像分批（10–20 张）处理，以保持内存使用低于 200 MB。  
- **对象复用：** 在迭代中复用 `Point` 和 `Dimension` 对象，以降低 GC 压力。  
- **版本更新：** 升级到最新的 GroupDocs.Redaction 版本，可获得在 24.10 版中报告的 15 % 速度提升。  

## 常见问题与解决方案
| 问题 | 原因 | 解决方案 |
|------|------|----------|
| **编辑失败，状态为 `Failed`** | 文件路径不正确或不支持的图像格式 | 确认文件存在且为支持的格式（JPG、PNG、BMP、GIF）。 |
| **输出文件为空** | `redactor.save()` 在编辑完成前被调用 | 在调用 `save()` 前确保 `apply()` 返回 `Status.SUCCESS`。 |
| **颜色未应用** | 使用了透明的 `Color` | 选择不透明的颜色，例如 `Color.BLACK` 或 `Color.BLUE`。 |

## 常见问题

**Q: `ImageAreaRedaction` 与文本编辑有什么区别？**  
A: `ImageAreaRedaction` 在原始像素坐标上工作，而文本编辑会解析 OCR 层以定位并移除文本内容。

**Q: 我可以在单个图像中编辑多个区域吗？**  
A: 可以——在保存最终文件之前，重复调用 `redactor.apply()`，并传入不同的 `ImageAreaRedaction` 对象。

**Q: GroupDocs.Redaction 是否支持 TIFF 等其他图像格式？**  
A: 该库支持常见光栅格式（JPG、PNG、BMP、GIF）。对于 TIFF，请先将图像转换为受支持的格式。

**Q: 如何为一文件夹的扫描 PDF 自动化编辑？**  
A: 将每页提取为图像，应用相同的编辑逻辑，然后使用如 GroupDocs.Conversion 的 PDF 库重新生成 PDF。

**Q: 是否有办法在保存前预览编辑效果？**  
A: 将 `Redactor` 渲染为 `BufferedImage` 并在 Swing 或 JavaFX UI 中显示，允许您在提交前确认遮蔽区域。

## 结论
您现在拥有一份完整、可投入生产的 **如何编辑图像** 内容指南，特别是 **如何使用 GroupDocs.Redaction for Java 编辑扫描图像**。按照上述步骤，您可以在金融、法律和医疗等领域保护敏感视觉数据。探索更多 API——如文本编辑、PDF 页面编辑或批量文件夹处理——以构建面向组织的端到端数据隐私管道。

**资源**  
- [文档](https://docs.groupdocs.com/redaction/java/)  
- [API 参考](https://reference.groupdocs.com/redaction/java)  
- [下载](https://releases.groupdocs.com/redaction/java/)  
- [GitHub 仓库](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- [免费支持论坛](https://forum.groupdocs.com/c/redaction/33)  
- [临时许可证](https://purchase.groupdocs.com/temporary-license/) 

---

**最后更新：** 2026-09-21  
**测试环境：** GroupDocs.Redaction 24.9 (Java)  
**作者：** GroupDocs

## 相关教程

- [如何使用 GroupDocs.Redaction 对 Java 进行编辑 - 开发者完整指南](/redaction/java/getting-started/implement-java-redaction-groupdocs-redaction-guide/)
- [如何使用 OCR 编辑扫描的 PDF – GroupDocs.Redaction Java](/redaction/java/ocr-integration/)
- [如何使用 GroupDocs.Redaction 在 Java 中编辑文本 – 指南](/redaction/java/text-redaction/text-redaction-java-groupdocs-redaction/)