---
date: '2026-02-26'
description: 了解如何使用 GroupDocs.Redaction Java 進行文字遮蔽，並以光柵化 PDF 儲存，支援精確片語取代與自訂 PDF 設定。
keywords:
- GroupDocs.Redaction Java
- text redaction Java
- rasterized PDF conversion
title: 如何使用 GroupDocs.Redaction Java 進行文字遮蔽
type: docs
url: /zh-hant/java/text-redaction/groupdocs-redaction-java-tutorial-text-redaction-rasterized-pdf/
weight: 1
---

 use Chinese punctuation. But keep as natural.

Let's produce.

# 如何使用 GroupDocs.Redaction Java 進行文字遮蔽

在當今以資料為驅動的世界中，**如何安全且高效地遮蔽文件中的文字** 是開發人員與合規人員共同關注的重點。無論您需要隱藏個人識別資訊、機密客戶資料，或是內部專案代碼，GroupDocs.Redaction for Java 都提供可靠的方式來定位精確片語，並以安全的覆蓋層取代它們。本教學同時說明 **如何儲存為光柵化 PDF**，將每一頁轉換為符合歸檔標準的影像式 PDF。

## 快速答覆
- **主要的遮蔽類別是什麼？** `Redactor`  
- **可以用彩色覆蓋層取代片語嗎？** 可以，使用 `ExactPhraseRedaction` 與 `ReplacementOptions`。  
- **如何產生光柵化 PDF？** 透過 `SaveOptions.getRasterization().setEnabled(true)` 啟用光柵化。  
- **範例中使用哪個 PDF 合規等級？** `PdfComplianceLevel.PdfA1a`。  
- **正式環境需要授權嗎？** 生產部署必須使用有效的 GroupDocs.Redaction 授權。

## 在 Java 中「如何遮蔽文字」是什麼？
遮蔽是永久移除或隱蔽檔案中敏感內容的過程。使用 GroupDocs.Redaction，您可以以程式方式搜尋精確片語（例如姓名或 ID），並以紅色覆蓋層、黑色方框或任何自訂視覺元素取代，確保原始資料無法被還原。

## 為什麼選擇 GroupDocs.Redaction for Java？
- **精確片語匹配** 可消除誤判。  
- **內建光柵化** 讓您建立符合 PDF/A 標準、僅含影像的 PDF，適合長期保存。  
- **跨格式支援** 可處理 DOCX、PDF、PPTX 等多種文件類型，讓相同程式碼可套用於不同文件。  
- **效能導向 API** 能批次處理大量文件，同時保持低記憶體使用。

## 前置條件
在開始之前，請確保您已具備以下項目：

- **GroupDocs.Redaction for Java**（v24.9 或更新版本）。  
- **Java Development Kit (JDK) 8+**。  
- 如 IntelliJ IDEA、Eclipse 或 NetBeans 等 IDE。  
- 用於相依管理的 Maven。

### 必要的函式庫與相依性
- **GroupDocs.Redaction for Java** – 在 `pom.xml` 中加入儲存庫與相依性（請參考下方程式碼區塊）。  
- **可選**：您偏好的其他日誌函式庫。

### 知識前置
- 基本的 Java 語法與檔案 I/O。  
- 熟悉 Maven 的 `pom.xml` 結構。

## 設定 GroupDocs.Redaction for Java
### Maven 設定
在 `pom.xml` 檔案中加入儲存庫與相依性：

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
或者，您也可以直接從 [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) 下載最新版本。

### 取得授權
- **免費試用** – 無需授權金鑰即可探索 API。  
- **臨時授權** – 用於延長評估。  
- **正式授權** – 生產環境必須使用。

### 基本初始化與設定
以下程式碼示範如何建立指向範例 DOCX 檔案的 `Redactor` 實例：

```java
import com.groupdocs.redaction.Redactor;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
```

## 如何遮蔽文字 – 精確片語範例
### 步驟 1：匯入必要類別
這些匯入讓您能使用遮蔽引擎與取代選項：

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.ReplacementOptions;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
```

### 步驟 2：建立並套用遮蔽
以下程式碼會搜尋片語 **“John Doe”**，並以紅色覆蓋層取代：

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
try {
    RedactorChangeLog result = redactor.apply(new ExactPhraseRedaction(
        "John Doe", new ReplacementOptions(java.awt.Color.RED)));
    
    if (result.getStatus() != RedactionStatus.Failed) {
        // Successfully redacted the text
    }
} finally { 
    redactor.close(); 
}
```

**為什麼重要：**`ReplacementOptions` 讓您控制遮蔽的視覺樣式，確保被隱藏的內容無法透過複製貼上或 OCR 復原。

## 如何儲存為光柵化 PDF
### 步驟 1：匯入 SaveOptions 類別
這些類別可設定 PDF 輸出，包括光柵化與合規等級：

```java
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.options.PdfComplianceLevel;
```

### 步驟 2：配置並套用儲存選項
完成遮蔽後，您可以將文件匯出為光柵化 PDF。以下範例僅對第 5 頁進行光柵化，並強制使用 PDF/A‑1a 合規：

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
try {
    SaveOptions options = new SaveOptions();

    // Enable rasterization for converting pages into images.
    options.getRasterization().setEnabled(true);
    
    // Set the starting page and count for rasterization.
    options.getRasterization().setPageIndex(5);
    options.getRasterization().setPageCount(1);

    // Define PDF compliance level.
    options.getRasterization().setCompliance(PdfComplianceLevel.PdfA1a);

    // Append a suffix to avoid filename conflicts.
    options.setAddSuffix(true);

    // Save the document with these configurations.
    redactor.save(options);
} finally { 
    redactor.close(); 
}
```

**關鍵點：**光柵化 PDF **會將每一頁轉換為影像**，從而移除隱藏的文字層，使文件防篡改——非常適合法律歸檔。

## 實務應用
1. **敏感資料遮蔽** – 在分享合約前自動隱藏個人識別資訊。  
2. **文件歸檔** – 將最終報告轉換為光柵化 PDF/A，以符合長期合規需求。  
3. **批次內容更新** – 透過單一腳本在數百個檔案中取代過時術語。

## 效能考量
- **在每次操作後關閉 `Redactor`**，以釋放檔案句柄與記憶體。  
- **批次處理** – 載入檔案清單並迴圈處理，盡可能重複使用同一個 `Redactor` 實例。  
- **資源監控** – 使用 Java 效能分析工具觀察 CPU 與堆積使用情況，確保大規模遮蔽時的穩定性。

## 常見問題

**Q: 如何在 Maven 專案中安裝 GroupDocs.Redaction？**  
A: 如 Maven 設定章節所示，將 GroupDocs 儲存庫與 `groupdocs-redaction` 相依性加入 `pom.xml`。

**Q: 能否使用此函式庫遮蔽 PDF 檔案的文字？**  
A: 可以，GroupDocs.Redaction 支援 PDF、DOCX、PPTX 以及其他多種格式。

**Q: 若找不到精確片語會發生什麼？**  
A: `RedactorChangeLog` 會回傳 `Failed` 狀態。請確認片語的拼寫與大小寫是否正確。

**Q: 如何有效處理超大型文件？**  
A: 將文件分段處理，只在需要的頁面啟用光柵化，且務必在完成後關閉 `Redactor` 以釋放資源。

**Q: 能否針對特定頁範圍儲存光柵化 PDF？**  
A: 完全可以。使用 `options.getRasterization().setPageIndex()` 與 `setPageCount()` 來指定要光柵化的頁面。

## 結論
現在您已掌握 **如何使用 GroupDocs.Redaction Java 進行文字遮蔽** 以及 **如何儲存為光柵化 PDF** 的完整流程。依循本指南，您可以保護敏感資訊、符合合規要求，並在生產環境中維持高效能。

**後續步驟**  
- 透過 [官方文件](https://docs.groupdocs.com/redaction/java/) 深入探索 API。  
- 嘗試其他遮蔽類型（例如 `RegexRedaction`、`ImageRedaction`）。  
- 加入 [GroupDocs 支援論壇](https://forum.groupdocs.com/c/redaction/33) 與社群交流技巧與最佳實踐。

---

**最後更新：** 2026-02-26  
**測試環境：** GroupDocs.Redaction Java 24.9  
**作者：** GroupDocs