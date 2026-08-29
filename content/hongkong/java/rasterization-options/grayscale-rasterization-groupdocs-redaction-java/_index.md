---
date: '2026-05-17'
description: 了解如何使用 GroupDocs.Redaction for Java 將 PDF 光柵化為灰階，套用灰階濾鏡，並確保您的文件安全且高品質。
keywords:
- how to rasterize pdf
- java pdf to image
- apply grayscale filter pdf
schemas:
- author: GroupDocs
  dateModified: '2026-05-17'
  description: Learn how to rasterize PDF to grayscale using GroupDocs.Redaction for
    Java, apply a grayscale filter, and keep your documents secure and high‑quality.
  headline: How to rasterize PDF to grayscale with GroupDocs.Redaction Java – Secure
    and Optimize Your Documents
  type: TechArticle
- questions:
  - answer: In GroupDocs.Redaction, the grayscale option is tied to rasterization,
      which ensures consistent results and adds a security layer.
    question: Can I convert documents to grayscale without rasterization?
  - answer: All major formats supported by GroupDocs.Redaction—including DOCX, PDF,
      XLSX, PPTX, RTF, and more than 100 others—can be rasterized and converted to
      grayscale.
    question: What document formats support grayscale rasterization?
  - answer: Yes. Text‑heavy files may grow, while image‑heavy files might shrink.
      DPI settings have the biggest impact.
    question: Will rasterization affect the file size of my documents?
  - answer: No. Rasterization is one‑way; keep a backup of the original if you need
      to revert.
    question: Is it possible to reverse the grayscale rasterization process?
  - answer: Use a higher DPI (300 + for print quality) and choose PDF as the output
      format for best archival results.
    question: How can I optimize the quality of grayscale rasterized documents?
  type: FAQPage
title: 如何使用 GroupDocs.Redaction Java 將 PDF 光柵化為灰階 – 確保文件安全與最佳化
type: docs
url: /zh-hant/java/rasterization-options/grayscale-rasterization-groupdocs-redaction-java/
weight: 1
---

# 如何使用 GroupDocs.Redaction Java 將 PDF 光柵化為灰階

如果您需要將 **光柵化 PDF** 為灰階，同時保持文件安全、外觀專業且易於歸檔，您來對地方了。在本教學中，我們將逐步說明如何使用 GroupDocs.Redaction for Java，將彩色的 DOCX、PDF 或其他支援的檔案轉換為乾淨的灰階光柵化版本。您將了解光柵化如何增添安全層、如何設定函式庫，以及如何有效管理資源——全部以友善的步驟說明方式呈現。

## 快速解答
- **灰階光柵化的作用是什麼？** 它會將每一頁轉換為高解析度的影像，然後套用灰階濾鏡，去除所有顏色資訊。  
- **為什麼要使用 GroupDocs.Redaction 來完成此操作？** 它將遮蔽安全性與光柵化選項結合於一個易於使用的 API 中。  
- **支援哪些格式？** DOCX、PDF、XLSX、PPTX、RTF 以及超過 100 種其他格式。  
- **需要授權嗎？** 生產環境需要有效的 GroupDocs.Redaction 授權；測試可使用免費試用版。  
- **需要哪個版本的 Java？** JDK 8 或更高版本。

## 如何將 PDF 光柵化為灰階？

使用 `new Redactor("path/to/file")` 載入來源文件，透過 `RasterizationOptions` 啟用光柵化，加入灰階進階選項，然後呼叫 `save()`——整個轉換只需幾行簡潔的程式碼。此方法可確保每一頁都變成基於影像的黑白 PDF，防止文字被選取，並確保列印時外觀一致。

## 什麼是 **create grayscale pdf**？

建立灰階 PDF 意味著將原始文件的所有視覺元素轉換為灰階色調。這樣產生的檔案較小、適合列印，能消除顏色干擾，且因內容已轉為影像而帶來微弱的安全效益。

## 為什麼在 GroupDocs.Redaction 中使用灰階光柵化？

光柵化會將每一頁轉為影像，這表示文字無法被複製或編輯，且視覺輸出在各種印表機和檢視器上保持一致。GroupDocs.Redaction 支援 **超過 100 種輸入與輸出格式**——包括 DOCX、XLSX、PPTX、HTML 以及各類影像格式——因此您可以對幾乎所有處理的文件套用相同的工作流程。

## 前置條件

- Java Development Kit (JDK) 8 或更新版本。可使用 `java -version` 進行驗證。  
- 具備 IDE（IntelliJ IDEA、Eclipse 或 NetBeans）以便更輕鬆地編寫程式碼與除錯。  
- 透過 Maven 或 Gradle 加入 GroupDocs.Redaction for Java。  
- 一個範例文件（例如多頁的 DOCX），可安全進行實驗。  
- 足夠的磁碟空間以存放光柵化輸出（光柵檔案可能比原始檔案大）。

## 匯入套件

以下的匯入語句會載入範例所需的核心 Redactor 與光柵化類別。

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.options.RasterizationOptions;
import com.groupdocs.redaction.options.AdvancedRasterizationOptions;
```

## 步驟 1：初始化 Redactor 物件

`Redactor` 類別是 GroupDocs.Redaction 中所有文件處理操作的入口。建立實例即可載入、編輯與儲存文件。

```java
final Redactor redactor = new Redactor(Constants.MULTIPAGE_SAMPLE_DOCX);
```

將 `Constants.MULTIPAGE_SAMPLE_DOCX` 替換為您想要轉換為灰階 PDF 的檔案路徑。

## 步驟 2：設定儲存選項

`SaveOptions` 類別定義了處理後文件寫入磁碟的方式，包括格式與檔名。

```java
SaveOptions so = new SaveOptions();
so.setRedactedFileSuffix("_scan");
```

輸出檔案名稱將為 `yourfile_scan.pdf`（或您之後指定的格式）。

## 步驟 3：啟用光柵化

`RasterizationOptions` 物件可在儲存前將每一頁以影像方式渲染。

```java
so.getRasterization().setEnabled(true);
```

## 步驟 4：套用灰階轉換

`AdvancedRasterizationOptions.Grayscale` 是一個旗標，強制光柵化影像僅使用灰階色調。

```java
so.getRasterization().addAdvancedOption(AdvancedRasterizationOptions.Grayscale);
```

## 步驟 5：執行文件轉換

呼叫 `save()` 會執行完整的處理流程並寫入輸出檔案。

```java
redactor.save(so);
```

此行程式碼執行後，您會在磁碟上看到一個已完整光柵化、灰階化，且以 `_scan` 為後綴的檔案。

## 步驟 6：正確的資源管理

`close()` 方法會釋放本機資源並刪除暫存檔案。

```java
finally { redactor.close(); }
```

在現代 Java 中，您也可以使用 try‑with‑resources 模式，自動關閉 `Redactor`：

```java
try (Redactor redactor = new Redactor(Constants.MULTIPAGE_SAMPLE_DOCX)) {
    // Your processing code here
}
// Automatic cleanup happens here
```

兩種方式皆安全；後者更為簡潔。

## 進階設定選項

### 調整 DPI 以平衡品質或檔案大小

較高的 DPI 可產生更銳利的影像（適合列印），較低的 DPI 則可減少檔案大小。常見的平衡是螢幕檢視使用 150 DPI，列印就緒的 PDF 使用 300 DPI。

```java
saveOptions.getRasterization().setDpi(300); // High quality for printing
// or
saveOptions.getRasterization().setDpi(150); // Balanced quality and size
```

### 選擇輸出格式

您可以將光柵化結果強制輸出為特定容器格式，例如 PDF、TIFF 或 PNG。PDF 是最常用的歸檔格式。

```java
saveOptions.setRasterizationFormat(RasterizationFormat.PDF);
```

## 常見使用情境

- **法律文件歸檔** – 建立不可編輯的不可變灰階 PDF。  
- **列印就緒報告** – 確保大量列印時的黑白輸出一致。  
- **合規工作流程** – 結合遮蔽與灰階光柵化，以符合嚴格的資料隱私法規。

## 常見問題與解決方案

| 問題 | 發生原因 | 解決方式 |
|-------|----------------|-----|
| 輸出檔案大於預期 | DPI 設定過高或影像壓縮未啟用 | 降低 DPI（例如 150）或在 `RasterizationOptions` 中啟用壓縮。 |
| 文字顯示模糊 | 原始字體大小的 DPI 不足 | 將 DPI 提升至 300 或更高。 |
| 處理大型文件時拋出 `OutOfMemoryError` | 整個文件一次載入記憶體 | 使用串流 API，或在支援的情況下分批處理頁面。 |
| 未套用灰階 | 進階選項未正確加入 | 確認在呼叫 `save()` 前已執行 `addAdvancedOption(AdvancedRasterizationOptions.Grayscale)`。 |

## 常見問答

**Q: 我可以在不進行光柵化的情況下將文件轉換為灰階嗎？**  
A: 在 GroupDocs.Redaction 中，灰階選項與光柵化相連，確保結果一致且增添安全層。

**Q: 什麼文件格式支援灰階光柵化？**  
A: 所有 GroupDocs.Redaction 支援的主要格式——包括 DOCX、PDF、XLSX、PPTX、RTF，以及超過 100 種其他格式——皆可光柵化並轉換為灰階。

**Q: 光柵化會影響我的文件檔案大小嗎？**  
A: 會。文字密集的檔案可能會變大，影像密集的檔案可能會縮小。DPI 設定的影響最大。

**Q: 能否還原灰階光柵化的過程？**  
A: 不能。光柵化是單向的；如需還原，請保留原始檔案的備份。

**Q: 如何優化灰階光柵化文件的品質？**  
A: 使用較高的 DPI（列印品質建議 300 +），並選擇 PDF 作為輸出格式，以獲得最佳的歸檔效果。

## 結論

您現在已掌握使用 GroupDocs.Redaction for Java **將 PDF 光柵化為灰階** 的完整生產就緒方案。透過啟用光柵化、加入灰階進階選項，並負責任地管理資源，您可以產生安全、適合列印的文件，符合合規標準，且在任何檢視器上外觀一致。

---

**最後更新：** 2026-05-17  
**測試環境：** GroupDocs.Redaction 23.11 for Java  
**作者：** GroupDocs  

## 目標關鍵字：

**主要關鍵字（最高優先級）：**  
how to rasterize pdf

**次要關鍵字（支援）：**  
java pdf to image, apply grayscale filter pdf

## 相關教學

- [GroupDocs.Redaction Java 的光柵化選項教學](/redaction/java/rasterization-options/)
- [如何在 Java 中使用 GroupDocs Redaction：Word 文件的預光柵化](/redaction/java/rasterization-options/groupdocs-redaction-java-pre-rasterization-word-docs/)
- [Java 自訂噪點光柵化：使用 GroupDocs.Redaction 保護敏感資訊](/redaction/java/rasterization-options/java-groupdocs-redaction-custom-noise-rasterization/)