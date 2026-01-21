---
date: '2026-01-21'
description: 學習如何使用 GroupDocs.Redaction for Java 結合 Azure OCR，對 PDF 及掃描文件進行 OCR 遮蔽。
keywords:
- OCR-based redactions Java
- GroupDocs Redaction setup
- regex-based text redaction
title: 使用 GroupDocs 與 Azure OCR 進行 OCR 遮蔽 PDF – Java 指南
type: docs
url: /zh-hant/java/ocr-integration/ocr-redaction-groupdocs-java-setup/
weight: 1
---

# 使用 GroupDocs 與 Azure OCR 進行 OCR 隱私遮蔽 PDF – Java 指南

在本完整教學中，您將學會如何在 Java 中 **使用 OCR 隱私遮蔽 PDF**，結合 GroupDocs.Redaction 與 Microsoft Azure OCR。無論是原生 PDF 還是掃描圖像，本指南都會示範如何精確定位並遮蔽敏感資料，協助您 **隱私遮蔽掃描文件**，符合隱私法規要求。

## 快速解答
- **OCR 隱私遮蔽的功能是什麼？** 它會從圖像/PDF 中提取文字，並自動套用遮蔽規則。  
- **哪個函式庫提供遮蔽引擎？** GroupDocs.Redaction for Java。  
- **使用哪項 OCR 服務？** Microsoft Azure OCR 連接器。  
- **需要授權嗎？** 免費試用可用於測試；正式環境需購買永久授權。  
- **能同時遮蔽原生與掃描 PDF 嗎？** 能——OCR 讓掃描文件也能進行遮蔽。

## 什麼是「使用 OCR 隱私遮蔽 PDF」？
使用 OCR 隱私遮蔽 PDF 意指先利用光學字符辨識將視覺文字轉換為可搜尋的字串，然後套用遮蔽模式（例如正則表達式）將該資訊隱藏，避免在檔案分享或儲存時洩漏。

## 為何選擇 GroupDocs.Redaction 搭配 Azure OCR？
- **高準確度**：Azure 雲端 OCR 引擎在掃描頁面上的辨識表現優異。  
- **簡易 Java API**：可直接整合至現有工作流程。  
- **彈性遮蔽規則**：支援正則表達式、關鍵字或自訂邏輯。  
- **合規輸出**：永久移除敏感資料，符合各類法規要求。

## 前置條件
- Java Development Kit (JDK) 8 或更新版本。  
- Maven（或手動下載 JAR 的方式）。  
- 具備 OCR 金鑰的 Microsoft Azure 帳號。  
- 基本的 Java 知識與正則表達式概念。

## 設定 GroupDocs.Redaction for Java

### Maven 設定
在 `pom.xml` 中加入 GroupDocs 的儲存庫與相依性：

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
若不使用 Maven，可從官方發行頁面下載最新 JAR：  
[GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/)

### 授權取得
- **免費試用** – 探索核心功能，無需付款。  
- **暫時授權** – 延長試用期限，適用較大專案。  
- **完整授權** – 解鎖無限制使用與高級支援。

### 基本初始化與設定
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.RedactorSettings;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.examples.java.helper_classes.MicrosoftAzureOcrConnector;

// Initialize the OCR connector with Microsoft Azure
RedactorSettings settings = new RedactorSettings(new MicrosoftAzureOcrConnector());
```

## 如何在 Java 中使用 OCR 隱私遮蔽 PDF

### 步驟 1：以 OCR 設定載入文件
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;

// Load your document with OCR settings
try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf", 
    new LoadOptions(), settings)) {
    // Subsequent redaction steps will be placed here
}
```
- **參數**  
  - `"YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf"` – 目標 PDF 的路徑。  
  - `new LoadOptions()` – 預設載入配置。  
  - `settings` – 包含 Azure OCR 連接器的設定。

### 步驟 2：套用正則表達式遮蔽（例如社會安全號碼）
```java
import com.groupdocs.redaction.redactions.RegexRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

// Define the regex for sensitive data (e.g., Social Security Numbers)
RegexRedaction redaction = new RegexRedaction("\\b\\d{3}-\\d{2}-\\d{4}\\b", 
    new ReplacementOptions("[REDACTED]"));

// Apply redaction
redactor.apply(redaction);

// Save the document after redactions
redactor.save(new SaveOptions());
```
- **正則說明** – `\b\d{3}-\d{2}-\d{4}\b` 會匹配形如 `123-45-6789` 的模式。  
- **ReplacementOptions** – 將偵測到的文字取代為 `[REDACTED]`。

### 常見問題與除錯
- **Azure 憑證** – 請再次確認訂閱金鑰與端點 URL。  
- **檔案路徑** – 確保 PDF 存在且程式具有讀寫權限。  
- **效能** – 大型 PDF 可能需要調整 JVM 堆積大小或改用非同步處理。

## 掃描文件隱私遮蔽的實務案例
1. **法律事務所** – 在分享案件檔案前隱藏客戶身分資訊。  
2. **金融機構** – 在掃描的對帳單中遮蔽帳號。  
3. **醫療機構** – 保護掃描醫療紀錄中的患者 PHI。  
4. **政府機關** – 從公開紀錄 PDF 中移除個人資料。  
5. **企業** – 在第三方審計前清理合約內容。

## 效能小技巧
- 盡量將正則表達式寫得具體，以縮短處理時間。  
- 及時釋放 `Redactor` 實例（如範例所示使用 try‑with‑resources）。  
- 若需批次處理，可考慮佇列作業並以平行執行緒執行。

## 常見問答

**Q: 什麼是 OCR 隱私遮蔽？**  
A: OCR 隱私遮蔽利用光學字符辨識從圖像或掃描 PDF 中提取文字，然後套用遮蔽規則，永久移除該文字。

**Q: 可以不使用 Azure OCR 而使用 GroupDocs.Redaction 嗎？**  
A: 可以，但 OCR 大幅提升掃描文件的準確度，讓您能有效 **隱私遮蔽掃描文件**。

**Q: 如何處理複雜的正則表達式？**  
A: 先以樣本資料測試，使用字界 (`\b`) 防止部分匹配，必要時將大型表達式拆分為多個較簡單的遮蔽規則。

**Q: 常見的效能瓶頸是什麼？**  
A: 大檔案的 OCR 呼叫、過於寬泛的正則表達式，以及記憶體不足。可透過優化正則與擴充資源來改善。

**Q: 若遇到問題該向哪裡尋求協助？**  
A: 可在 GroupDocs 社群論壇發問：  
[GroupDocs forum](https://forum.groupdocs.com/c/redaction/33)

## 其他資源
- **文件說明**：https://docs.groupdocs.com/redaction/java/  
- **API 參考**：https://reference.groupdocs.com/redaction/java  
- **下載頁面**：https://releases.groupdocs.com/redaction/java/  
- **GitHub**：https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java  
- **免費支援**：https://forum.groupdocs.com/c/redaction/33  
- **暫時授權**：https://purchase.groupdocs.com/temporary-license/

---

**最後更新：** 2026-01-21  
**測試環境：** GroupDocs.Redaction 24.9 for Java  
**作者：** GroupDocs