---
date: '2026-02-13'
description: 了解如何使用 GroupDocs.Redaction for Java 建立灰階 PDF，安全地將 PDF 轉換為灰階，同時保留文件品質。
keywords:
- GroupDocs.Redaction
- Java
- Document Processing
title: 如何使用 GroupDocs.Redaction Java 建立灰階 PDF – 保護並優化您的文件
type: docs
url: /zh-hant/java/rasterization-options/grayscale-rasterization-groupdocs-redaction-java/
weight: 1
---

 sure markdown formatting preserved.

Now produce final content with all translations.

Check for any missing items: code block placeholders remain. Ensure no extra spaces.

Proceed to final.# GroupDocs.Redaction Java：灰階光柵化指南

## 介紹

如果您需要 **create grayscale pdf** 檔案，同時保持文件的安全與專業外觀，您來對地方了。在本教學中，我們將逐步說明如何使用 GroupDocs.Redaction for Java，將彩色的 DOCX、PDF 或其他支援的檔案轉換為乾淨的灰階光柵化版本。您將了解光柵化如何提供額外的安全層、如何設定函式庫，以及如何有效管理資源——全部以對話式、一步一步的方式呈現。

## 快速解答
- **What does grayscale rasterization do?** 它會將文件的每一頁轉換為高解析度的影像，然後套用灰階濾鏡，移除所有顏色資訊。  
- **Why use GroupDocs.Redaction for this?** 它將遮蔽安全性與強大的光柵化選項結合於同一個 API。  
- **Which formats are supported?** 支援 DOCX、PDF、XLSX、PPTX、RTF 等多種格式。  
- **Do I need a license?** 生產環境需要有效的 GroupDocs.Redaction 授權；測試可使用試用版。  
- **What Java version is required?** JDK 8 或以上。

## 什麼是 **create grayscale pdf**？

建立灰階 PDF 意味著將原始文件的所有視覺元素轉換為灰階色調。這樣產生的檔案較小、適合列印，能消除與顏色相關的干擾，且因內容已成為影像，還能提供微弱的安全效益。

## 為何在 GroupDocs.Redaction 中使用灰階光柵化？

- **Enhanced security** – 光柵化的頁面無法被選取、複製或編輯為文字。  
- **Consistent appearance** – 顏色被移除，呈現統一且專業的外觀。  
- **Broad format support** – 同一個 API 可支援 DOCX、PDF、PPTX 等多種格式。  
- **Fine‑tuned control** – 您可以調整 DPI、輸出格式，以及如灰階轉換等進階選項。

## 前置條件

- Java Development Kit (JDK) 8 或更新版本。可使用 `java -version` 進行驗證。  
- 任何 IDE（IntelliJ IDEA、Eclipse 或 NetBeans）以便更輕鬆地編寫與除錯程式。  
- 透過 Maven 或 Gradle 加入 GroupDocs.Redaction for Java。  
- 一個範例文件（例如多頁的 DOCX），可安全進行實驗。  
- 足夠的磁碟空間以存放光柵化輸出（光柵檔案可能比原檔案大）。

## 匯入套件

設定正確的匯入就像在專案開始前整理工具箱。以下的匯入讓您能使用核心的 Redactor 類別以及我們需要的光柵化選項。

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.options.RasterizationOptions;
import com.groupdocs.redaction.options.AdvancedRasterizationOptions;
```

## 步驟 1：初始化 Redactor 物件

建立 `Redactor` 實例即可開啟所有文件處理功能的大門。

```java
final Redactor redactor = new Redactor(Constants.MULTIPAGE_SAMPLE_DOCX);
```

將 `Constants.MULTIPAGE_SAMPLE_DOCX` 替換為您想要轉換為灰階 PDF 的檔案路徑。

## 步驟 2：設定儲存選項

`SaveOptions` 定義最終檔案的寫入方式。加入副檔名可協助保留原始檔案。

```java
SaveOptions so = new SaveOptions();
so.setRedactedFileSuffix("_scan");
```

輸出檔案將命名為 `yourfile_scan.docx`（或您之後指定的格式）。

## 步驟 3：啟用光柵化

啟用光柵化會指示引擎在儲存前將每頁渲染為影像。

```java
so.getRasterization().setEnabled(true);
```

光柵化是建立灰階 PDF 的基礎，因為它將文件轉換為影像為主的表示方式。

## 步驟 4：套用灰階轉換

現在我們將灰階濾鏡加入光柵化流程中。

```java
so.getRasterization().addAdvancedOption(AdvancedRasterizationOptions.Grayscale);
```

此選項會強制每個像素以灰階色調渲染，為您產生想要的 **create grayscale pdf** 結果。

## 步驟 5：執行文件轉換

`save` 呼叫會執行整個處理鏈。

```java
redactor.save(so);
```

此行程式碼執行完畢後，您會在磁碟上看到一個已完整光柵化、灰階化，且以 `_scan` 為副檔名的檔案。

## 步驟 6：正確的資源管理

清理資源可防止檔案鎖定與記憶體洩漏。

```java
finally { redactor.close(); }
```

對於現代 Java，您也可以使用 try‑with‑resources 模式，自動關閉 `Redactor`：

```java
try (Redactor redactor = new Redactor(Constants.MULTIPAGE_SAMPLE_DOCX)) {
    // Your processing code here
}
// Automatic cleanup happens here
```

兩種方式皆安全；後者較為簡潔。

## 進階設定選項

### 調整 DPI 以取得品質或大小

較高的 DPI 可產生更銳利的影像（適合列印），較低的 DPI 則可減少檔案大小。

```java
saveOptions.getRasterization().setDpi(300); // High quality for printing
// or
saveOptions.getRasterization().setDpi(150); // Balanced quality and size
```

### 選擇輸出格式

您可以將光柵化結果強制輸出為特定的容器格式，例如 PDF。

```java
saveOptions.setRasterizationFormat(RasterizationFormat.PDF);
```

## 常見使用情境

- **Legal document archiving** – 建立不可編輯的不可變灰階 PDF，以作法律文件存檔。  
- **Print‑ready reports** – 確保大量列印時的黑白輸出一致。  
- **Compliance workflows** – 結合遮蔽與灰階光柵化，以符合嚴格的資料隱私法規。

## 常見問題與解決方案

| 問題 | 發生原因 | 解決方式 |
|-------|----------------|-----|
| 輸出檔案比預期大 | DPI 設定過高或未啟用影像壓縮 | 降低 DPI（例如 150）或在 `RasterizationOptions` 中啟用壓縮。 |
| 文字模糊 | 原始字體大小的 DPI 不足 | 將 DPI 提升至 300 或更高。 |
| 處理大型文件時拋出 `OutOfMemoryError` | 整個文件一次載入記憶體 | 使用串流 API，或若支援則分批處理頁面。 |
| 未套用灰階 | 未正確加入進階選項 | 確認在 `save()` 前呼叫 `addAdvancedOption(AdvancedRasterizationOptions.Grayscale)`。 |

## 常見問答

**Q: 我可以在不使用光柵化的情況下將文件轉換為灰階嗎？**  
A: 在 GroupDocs.Redaction 中，灰階選項與光柵化相連，確保結果一致且提升安全性。

**Q: 哪些文件格式支援灰階光柵化？**  
A: 所有 GroupDocs.Redaction 支援的主要格式——包括 DOCX、PDF、XLSX、PPTX、RTF 等——皆可光柵化並轉換為灰階。

**Q: 光柵化會影響文件的檔案大小嗎？**  
A: 會。文字密集的檔案可能變大，影像密集的檔案可能變小。DPI 設定影響最大。

**Q: 能否逆轉灰階光柵化的過程？**  
A: 不能。光柵化是單向的；如需回復，請保留原始檔案的備份。

**Q: 如何優化灰階光柵化文件的品質？**  
A: 使用較高的 DPI（列印品質建議 300 以上）並選擇適當的輸出格式（PDF 常用於存檔）。

## 結論

您現在已掌握使用 GroupDocs.Redaction for Java 產生 **create grayscale pdf** 檔案的完整、可投入生產的作法。透過啟用光柵化、加入灰階進階選項，並負責任地管理資源，即可產生安全、適合列印的文件，符合合規標準。

---

**最後更新：** 2026-02-13  
**測試環境：** GroupDocs.Redaction 23.11 for Java  
**作者：** GroupDocs