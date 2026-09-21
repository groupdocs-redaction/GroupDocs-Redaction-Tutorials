---
date: '2026-09-21'
description: 了解如何使用 GroupDocs.Redaction for Java 進行影像遮蔽。逐步指南涵蓋設定、像素層級遮蔽、驗證以及最佳實踐。
keywords:
- how to redact image
- Java image redaction
- GroupDocs.Redaction for Java
- scanned image redaction
- pixel redaction Java
lastmod: '2026-09-21'
og_description: 如何使用 GroupDocs.Redaction for Java 進行影像遮蔽。遵循本指南以在掃描檔案中遮蔽像素資料、選擇顏色並驗證結果——完美符合
  GDPR 與 HIPAA 規範。
og_image_alt: Guide showing Java code that redacts scanned images using GroupDocs.Redaction
og_title: 如何使用 GroupDocs.Redaction for Java 進行影像遮蔽
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
title: 如何使用 GroupDocs.Redaction for Java 進行影像遮蔽
type: docs
url: /zh-hant/java/image-redaction/java-image-redaction-groupdocs-tutorial/
weight: 1
---

# 如何使用 GroupDocs.Redaction for Java 進行圖像遮蔽

在本完整教學中，您將學習**圖像遮蔽**檔案在 Java 中使用 GroupDocs.Redaction。對掃描圖像進行遮蔽是保護個人資料、符合 GDPR、HIPAA 或其他隱私法規，以及確保機密視覺資訊不外洩的重要步驟。我們將逐步說明專案設定、像素級遮蔽設定、安全儲存結果，以及確認遮蔽成功——以對話式、一步一步的方式呈現，您可直接套用於任何 Java 應用程式。

## 快速回答
- **什麼程式庫在 Java 中處理圖像遮蔽？** GroupDocs.Redaction for Java.  
- **我可以選擇遮蔽顏色嗎？** 是 – 任何不透明的 `java.awt.Color`，例如 `Color.BLUE` 或 `Color.BLACK`.  
- **生產環境需要授權嗎？** 是，商業使用必須擁有有效的 GroupDocs 授權。  
- **原始圖像會被覆寫嗎？** 不會 – API 會將遮蔽後的圖像寫入您指定的新檔案。  
- **支援哪個 Java 版本？** Java 8 及以上（撰寫本文時最高支援至 Java 21）。

## 什麼是圖像遮蔽以及為何在 Java 中遮蔽掃描圖像？
圖像遮蔽會永久隱藏視覺資料——如姓名、編號、簽名——透過將像素區域替換為單一實色。與針對可選取文字的文字遮蔽不同，掃描圖像以原始像素儲存資訊，只有基於像素的工具才能保證資料無法復原。使用 GroupDocs.Redaction，您可以精確定位座標、套用任意不透明顏色，並產生一張全新圖像，徹底移除敏感內容。

## 為何使用 GroupDocs.Redaction for Java？
GroupDocs.Redaction 支援 **50 多種圖像格式**（包括 JPG、PNG、BMP、GIF），且憑藉串流架構可在不將整個檔案載入記憶體的情況下處理上百頁的文件。基準測試顯示，300 KB 的掃描 PNG 圖像在一般 2.8 GHz CPU 上可於 120 毫秒內完成遮蔽，適用於批次作業與即時服務。

## 前置條件
- **JDK 8 或更新版本** 已安裝並在 `PATH` 中設定。  
- **Maven**（或 Gradle）用於相依管理。  
- 如 **IntelliJ IDEA**、**Eclipse** 或 **NetBeans** 等 IDE。  
- 具備 Java 檔案 I/O 與 `java.awt` 套件的基本知識。  

## 設定 GroupDocs.Redaction for Java

### Maven 設定
將 GroupDocs 的儲存庫與相依項目加入您的 `pom.xml`：

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

### 直接下載
或者，從官方發行頁面下載最新的 JAR： [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/)。

### 取得授權
- **免費試用：** 註冊試用以探索完整 API。  
- **臨時授權：** 使用臨時金鑰進行延長測試，免付費。  
- **正式購買：** 取得生產授權以無限制部署。  

## 實作指南

我們將實作分為兩個核心功能：**圖像區域遮蔽**（實際遮蔽）與 **遮蔽狀態檢查**（驗證成功）。

### 如何遮蔽掃描文件圖像 – 步驟 1：初始化 Redactor
`Redactor` 是載入圖像並提供遮蔽操作的核心類別。  
建立指向您欲處理之來源圖像的 `Redactor` 實例。

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_JPG");
```

### 步驟 2：定義遮蔽參數
`ImageAreaRedaction` 使用 `Point`（左上角）與 `Dimension`（寬 × 高）來描述要隱藏的矩形區域。在此範例中，我們使用藍色填充。

```java
// Define the position on the image where redaction starts.
Point samplePoint = new Point(385, 485);

// Define the size of the area to be redacted.
Dimension sampleSize = new Dimension(1793, 2069);
```

### 步驟 3：套用遮蔽
`RegionReplacementOptions` 讓您指定填充顏色與可選的邊框。將這些選項傳遞給 `ImageAreaRedaction` 並呼叫 `apply()` 即可執行遮蔽。此方法會回傳 `RedactorChangeLog`，以指示成功或失敗。

```java
RedactorChangeLog result = redactor.apply(
    new ImageAreaRedaction(samplePoint, new RegionReplacementOptions(Color.BLUE, sampleSize))
);

// Check if the redaction was successful and save the output.
if (result.getStatus() != RedactionStatus.Failed) {
    redactor.save("YOUR_OUTPUT_DIRECTORY/redacted_output.jpg");
}
```

### 步驟 4：釋放資源
`Redactor` 實作 `AutoCloseable`。關閉它會釋放本機緩衝區與檔案句柄，防止長時間服務中的記憶體泄漏。

```java
redactor.close();
```

### 如何驗證遮蔽 – 狀態檢查
套用遮蔽後，檢查 `RedactorChangeLog`。`Status.SUCCESS` 表示像素區域已成功替換且無錯誤。您亦可將圖像渲染為 `BufferedImage`，於儲存前進行目視檢查。

```java
if (result != null && result.getStatus() != RedactionStatus.Failed) {
    System.out.println("Redaction was successful.");
} else {
    System.out.println("Redaction failed.");
}
```

## 實務應用
- **機密文件處理：** 在與合作夥伴共享前，於掃描合約中遮蔽個人資料。  
- **法律文件：** 透過遮蔽證據圖像中的識別資訊，確保符合 GDPR 或 HIPAA 規範。  
- **醫療紀錄：** 隱藏放射掃描中患者臉部或手寫註記，同時保留診斷細節。  

## 效能考量
- **批次處理：** 將圖像分批（10–20 張）處理，以將記憶體使用量控制在 200 MB 以下。  
- **物件重用：** 在迭代間重用 `Point` 與 `Dimension` 物件，以減少 GC 壓力。  
- **版本升級：** 更新至最新的 GroupDocs.Redaction 版本，可獲得在 24.10 版中報告的 15 % 速度提升。  

## 常見問題與解決方案
| 問題 | 原因 | 解決方案 |
|------|------|----------|
| **遮蔽失敗，狀態為 `Failed`** | 檔案路徑不正確或圖像格式不支援 | 確認檔案存在且為支援的格式（JPG、PNG、BMP、GIF）。 |
| **輸出檔案為空** | `redactor.save()` 在遮蔽完成前被呼叫 | 確保在呼叫 `save()` 前，`apply()` 已回傳 `Status.SUCCESS`。 |
| **顏色未套用** | 使用了透明的 `Color` | 選擇不透明的顏色，例如 `Color.BLACK` 或 `Color.BLUE`。 |

## 常見問答

**問：`ImageAreaRedaction` 與文字遮蔽有何不同？**  
A: `ImageAreaRedaction` 作用於原始像素座標，而文字遮蔽則解析 OCR 層以定位並移除文字內容。

**問：我可以在同一張圖像中遮蔽多個區域嗎？**  
A: 可以——在儲存最終檔案前，重複呼叫 `redactor.apply()` 並傳入不同的 `ImageAreaRedaction` 物件。

**問：GroupDocs.Redaction 是否支援其他圖像格式，例如 TIFF？**  
A: 此函式庫支援常見的點陣格式（JPG、PNG、BMP、GIF）。若為 TIFF，請先將圖像轉換為支援的格式。

**問：如何自動化處理資料夾內的掃描 PDF 進行遮蔽？**  
A: 將每頁提取為圖像，套用相同的遮蔽邏輯，然後使用如 GroupDocs.Conversion 等 PDF 函式庫重新組合成 PDF。

**問：是否有方法在儲存前預覽遮蔽效果？**  
A: 將 `Redactor` 渲染為 `BufferedImage`，並在 Swing 或 JavaFX UI 中顯示，讓您在提交前確認遮蔽區域。

## 結論
您現在擁有一份完整、可投入生產環境的指南，說明如何使用 GroupDocs.Redaction for Java **遮蔽圖像** 內容，特別是 **在 Java 中遮蔽掃描圖像**。依循上述步驟，即可在金融、法律與醫療等領域保護敏感視覺資料。探索其他 API——如文字遮蔽、PDF 頁面遮蔽或批次資料夾處理——以為貴組織打造端到端的資料隱私管線。

**資源**  
- [文件說明](https://docs.groupdocs.com/redaction/java/)  
- [API 參考](https://reference.groupdocs.com/redaction/java)  
- [下載](https://releases.groupdocs.com/redaction/java/)  
- [GitHub 倉庫](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- [免費支援論壇](https://forum.groupdocs.com/c/redaction/33)  
- [臨時授權](https://purchase.groupdocs.com/temporary-license/) 

---

**最後更新：** 2026-09-21  
**測試環境：** GroupDocs.Redaction 24.9 (Java)  
**作者：** GroupDocs

## 相關教學

- [如何使用 GroupDocs.Redaction 於 Java 進行遮蔽 - 開發者完整指南](/redaction/java/getting-started/implement-java-redaction-groupdocs-redaction-guide/)
- [如何使用 OCR 遮蔽掃描 PDF – GroupDocs.Redaction Java](/redaction/java/ocr-integration/)
- [如何在 Java 中使用 GroupDocs.Redaction 遮蔽文字 – 指南](/redaction/java/text-redaction/text-redaction-java-groupdocs-redaction/)