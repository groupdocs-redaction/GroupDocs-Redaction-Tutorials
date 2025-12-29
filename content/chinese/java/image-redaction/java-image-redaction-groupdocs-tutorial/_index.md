---
date: '2025-12-29'
description: 了解如何使用 GroupDocs.Redaction for Java 对扫描的文档图像进行编辑。一步一步的指南，涵盖设置、图像区域编辑以及验证。
keywords:
- Java image redaction
- GroupDocs.Redaction for Java
- image area redaction
title: 如何使用 GroupDocs 在 Java 中对扫描的文档图像进行脱敏
type: docs
url: /zh/java/image-redaction/java-image-redaction-groupdocs-tutorial/
weight: 1
---

# 如何使用 GroupDocs 在 Java 中编辑扫描文档图像

在当今的数字环境中，对**编辑扫描文档**图像是保护隐私和满足合规要求的关键。无论您需要在扫描的合同中隐藏个人数据，还是在医学图像中遮蔽患者信息，本教程将向您展示如何使用 **GroupDocs.Redaction for Java** 快速且可靠地**如何编辑图像**内容。我们将从项目设置一直讲解到验证编辑是否成功，帮助您自信地将该解决方案集成到任何 Java 应用程序中。

## 快速答案
- **什么库在 Java 中处理图像编辑？** GroupDocs.Redaction for Java  
- **我可以选择编辑颜色吗？** Yes – any `java.awt.Color` (e.g., `Color.BLUE`)  
- **生产环境需要许可证吗？** Yes, a valid GroupDocs license is needed  
- **原始图像会被覆盖吗？** No – you save the result to a new file  
- **支持的 Java 版本是什么？** Java 8+ (compatible with modern JDKs)

## 什么是图像编辑以及为何要编辑扫描文档图像？
图像编辑指永久遮蔽敏感的视觉信息——例如姓名、号码或签名——使其无法恢复。处理扫描文档时，数据以像素形式嵌入，这使得传统的文本编辑工具失效。使用 GroupDocs.Redaction 可以精准定位像素区域并用纯色替代，确保信息被真正删除。

## 前置条件
- **JDK 8 或更高** 已安装  
- **Maven**（或其他构建工具）用于依赖管理  
- 如 **IntelliJ IDEA**、**Eclipse** 或 **NetBeans** 的 IDE  
- 基本的 Java 知识以及对文件 I/O 的熟悉  

## 设置 GroupDocs.Redaction for Java

### Maven 设置
在您的 `pom.xml` 中添加 GroupDocs 仓库和依赖：

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
或者，从官方发布页面下载最新的 JAR： [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/)。

### 许可证获取
- **免费试用：** 注册试用以探索 API。  
- **临时许可证：** 使用临时密钥进行扩展测试。  
- **完整购买：** 获取生产许可证以无限制使用。  

## 实现指南
我们将实现分为两个核心功能：**图像区域编辑**（实际遮蔽）和**编辑状态检查**（验证成功）。

### 如何编辑扫描文档图像 – 步骤 1：初始化 Redactor
首先，创建指向要处理图像的 `Redactor` 实例。

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_JPG");
```

### 步骤 2：定义编辑参数
指定要隐藏矩形的左上角 (`Point`) 和大小 (`Dimension`)。在本例中我们使用蓝色填充。

```java
// Define the position on the image where redaction starts.
Point samplePoint = new Point(385, 485);

// Define the size of the area to be redacted.
Dimension sampleSize = new Dimension(1793, 2069);
```

### 步骤 3：应用编辑
使用 `RegionReplacementOptions` 创建 `ImageAreaRedaction` 对象并执行。该方法返回 `RedactorChangeLog`，告知操作是否成功。

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
完成后务必关闭 `Redactor` 以释放本地资源。

```java
redactor.close();
```

### 如何验证编辑 – 状态检查
应用编辑后，您可以检查 `RedactorChangeLog` 以确认操作未失败。

```java
if (result != null && result.getStatus() != RedactionStatus.Failed) {
    System.out.println("Redaction was successful.");
} else {
    System.out.println("Redaction failed.");
}
```

## 实际应用
- **机密文档处理：** 在与外部方共享之前，自动在扫描的合同中遮蔽个人数据。  
- **法律文档：** 通过编辑证据图像中的标识符，确保符合 GDPR 或 HIPAA。  
- **医疗记录：** 通过遮蔽放射图像中的面部或手写笔记，保护患者隐私。  

## 性能考虑
- **批量处理：** 将图像分小批次加载并编辑，以保持低内存使用。  
- **高效数据结构：** 在处理大量图像时复用 `Point` 和 `Dimension` 对象。  
- **保持更新：** 定期升级到最新的 GroupDocs.Redaction 版本，以获得性能提升和错误修复。  

## 常见问题与解决方案

| 问题 | 原因 | 解决方案 |
|-------|-------|-----|
| **编辑失败，状态为 `Failed`** | 文件路径错误或不支持的图像格式 | 确认图像存在且为支持的格式（JPG、PNG、BMP）。 |
| **输出文件为空** | `redactor.save()` 在编辑完成前被调用 | 确保 `apply()` 在保存前返回成功状态。 |
| **颜色未应用** | 使用了透明颜色 | 选择不透明的 `Color`（例如 `Color.BLACK` 或 `Color.BLUE`）。 |

## 常见问答

**Q: `ImageAreaRedaction` 与文本编辑有什么区别？**  
A: `ImageAreaRedaction` 基于像素坐标工作，而文本编辑会解析 OCR 层以定位并删除文本内容。

**Q: 我可以在单个图像中编辑多个区域吗？**  
A: 可以——在保存之前，使用不同的 `ImageAreaRedaction` 对象多次调用 `redactor.apply()`。

**Q: GroupDocs.Redaction 是否支持 TIFF 等其他图像格式？**  
A: 该库支持常见的光栅格式（JPG、PNG、BMP、GIF）。对于 TIFF，请先转换为受支持的格式。

**Q: 如何为一文件夹的扫描 PDF 自动化编辑？**  
A: 遍历从 PDF 中提取的每页图像，应用相同的编辑逻辑，然后使用 PDF 库重新生成 PDF。

**Q: 是否有办法在保存前预览编辑效果？**  
A: 您可以将 `Redactor` 渲染为 `BufferedImage`，并在 Swing 或 JavaFX 界面中显示，以在提交更改前预览。

## 结论
现在，您已经拥有一份完整、可投入生产的指南，介绍了 **如何编辑图像** 内容，以及使用 GroupDocs.Redaction for Java **编辑扫描文档** 图像的具体方法。按照上述步骤，您可以在各行各业保护敏感的视觉数据。探索其他 API——如文本编辑或 PDF 页面编辑——以为您的组织构建全面的数据隐私解决方案。

---

**最后更新：** 2025-12-29  
**测试环境：** GroupDocs.Redaction 24.9 (Java)  
**作者：** GroupDocs  

**资源**  
- [文档](https://docs.groupdocs.com/redaction/java/)  
- [API 参考](https://reference.groupdocs.com/redaction/java)  
- [下载](https://releases.groupdocs.com/redaction/java/)  
- [GitHub 仓库](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- [免费支持论坛](https://forum.groupdocs.com/c/redaction/33)  
- [临时许可证](https://purchase.groupdocs.com/temporary-license/)