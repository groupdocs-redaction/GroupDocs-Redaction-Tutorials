---
date: '2026-02-08'
description: 學習如何使用 GroupDocs OCR Redaction 結合 Microsoft Azure OCR 來遮蔽敏感資料並編輯 PDF
  Java 檔案。
keywords:
- OCR-based redactions Java
- GroupDocs Redaction setup
- regex-based text redaction
title: 使用 GroupDocs OCR 修訂功能遮蔽 PDF 中的敏感資料
type: docs
url: /zh-hant/java/ocr-integration/ocr-redaction-groupdocs-java-setup/
weight: 1
---

# 在 PDF 中使用 GroupDocs OCR 修飾遮蔽敏感資料

在當今的數位環境中，保護個人及機密資訊是首要任務。在本教學中，**您將學習如何在 PDF 檔案中遮蔽敏感資料**，方法是結合 GroupDocs Redaction 與 Microsoft Azure OCR。此方式可在掃描頁面上提供可靠的文字辨識，並讓您**精準修飾 PDF Java**文件，確保符合隱私法規。

## 快速解答
- **「遮蔽敏感資料」是什麼意思？** 它會將已識別的機密文字取代為佔位符（例如 `[REDACTED]`）。  
- **哪個函式庫負責 OCR？** Microsoft Azure OCR 連接器，透過 GroupDocs Redaction 使用。  
- **我需要授權嗎？** 免費試用可用於評估；正式上線需購買永久授權。  
- **我可以修飾掃描的 PDF 嗎？** 可以——OCR 會在套用正則表達式修飾前提取隱藏文字。  
- **此解決方案僅限 Java 嗎？** 範例基於 Java，但 GroupDocs 亦提供 .NET 及其他平台的相似 API。

## 什麼是 OCR 基於的修飾？

OCR 基於的修飾會先對文件的每一頁執行光學字符辨識（Optical Character Recognition），將文字影像轉換為可搜尋的字串。文字可搜尋後，您即可套用正規表達式（regex）規則來定位敏感資訊——例如社會安全號碼、信用卡號碼或個人識別碼，並以遮蔽字串（如 **`[REDACTED]`**）取代。

## 為何使用 GroupDocs Redaction 搭配 Azure OCR？

- **高精準度**，適用於掃描的 PDF 與影像。  
- **無縫的 Java 整合**，透過 Maven 或直接下載 JAR。  
- **彈性的 regex 引擎**，讓您為任何資料類型自訂模式。  
- **可擴充**，適用於大量文件批次，並提供非同步處理選項。

## 前置條件
- **Java Development Kit (JDK) 8+** 已安裝。  
- **Maven**（若您偏好相依性管理）或能手動下載 JAR。  
- **Microsoft Azure OCR 憑證**（端點與訂閱金鑰）。  
- 基本的 Java 知識與正則表達式的熟悉度。

## 設定 GroupDocs Redaction（Java 版）

### Maven 設定
Add the GroupDocs repository and dependency to your `pom.xml`:

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
如果您偏好手動管理 JAR，請從 [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) 取得最新版本。

### 取得授權
- **Free Trial** – 免費試用，探索所有功能。  
- **Temporary License** – 延長評估期限。  
- **Full License** – 解鎖正式環境的全部功能。

### 基本初始化與設定
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.RedactorSettings;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.examples.java.helper_classes.MicrosoftAzureOcrConnector;

// Initialize the OCR connector with Microsoft Azure
RedactorSettings settings = new RedactorSettings(new MicrosoftAzureOcrConnector());
```

## 如何使用 OCR 修飾遮蔽敏感資料

### 步驟 1：使用 OCR 設定載入文件
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;

// Load your document with OCR settings
try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf", 
    new LoadOptions(), settings)) {
    // Further operations will go here
}
```
- **`YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf`** – 請替換為您的 PDF 路徑。  
- **`LoadOptions`** – 預設載入；如有需要可自行客製化。  
- **`settings`** – 包含先前建立的 Azure OCR 連接器。

### 步驟 2：定義並套用 Regex 修飾
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
- 模式 `\b\d{3}-\d{2}-\d{4}\b` 可匹配美國社會安全號碼（SSN）。  
- `ReplacementOptions("[REDACTED]")` 會將每個匹配項替換為遮蔽字串，從而 **遮蔽敏感資料**。

## 常見的敏感資料遮蔽使用情境
1. **Legal Document Management** – 在分享草稿前隱藏客戶識別碼。  
2. **Financial Reporting** – 保護帳號與交易編號。  
3. **Healthcare Records** – 依照 HIPAA 規範修飾患者識別資訊。  
4. **Government Publications** – 從公開紀錄中移除個人資料。  
5. **Corporate Contracts** – 在外部審查時隱藏專有條款。

## 效能最佳化建議
- **優化 regex** – 避免過於寬泛的模式，以免增加處理時間。  
- **記憶體管理** – 及時關閉 `Redactor` 實例（使用 try‑with‑resources 會自動完成）。  
- **非同步執行** – 大量處理時，將修飾工作放在獨立執行緒或使用任務佇列。

## 疑難排解
- **Azure 憑證錯誤** – 請再次確認 `MicrosoftAzureOcrConnector` 中的端點 URL 與訂閱金鑰。  
- **文件未載入** – 檢查檔案路徑，並確保 PDF 未受密碼保護（或透過 `LoadOptions` 提供密碼）。  
- **未套用修飾** – 先以簡單字串測試 regex；可在單元測試中使用 `Pattern.compile` 以確認匹配結果。

## 常見問與答

**Q: 什麼是 OCR 修飾？**  
A: OCR 修飾利用光學字符辨識（Optical Character Recognition）從影像或掃描的 PDF 中提取隱藏文字，然後套用修飾規則將該文字遮蔽。

**Q: 可以在不使用 Azure OCR 的情況下使用 GroupDocs Redaction 嗎？**  
A: 可以，但在原生文字提取失敗的掃描文件上，OCR 能顯著提升精準度。

**Q: 如何處理複雜的 regex 模式？**  
A: 請逐步建構與測試，可在沙盒環境使用 Java 的 `Pattern` 類別，確認無誤後再套用至大型文件。

**Q: 常見的效能瓶頸是什麼？**  
A: 大型 PDF、過於複雜的 regex 以及同步的 OCR 呼叫都會拖慢處理速度；建議使用批次處理與最佳化的模式。

**Q: 是否提供實作問題的支援？**  
A: 當然可以——可透過 [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33) 向社群求助，或直接聯絡 GroupDocs 支援團隊。

## 其他資源
- **文件說明**: https://docs.groupdocs.com/redaction/java/  
- **API 參考**: https://reference.groupdocs.com/redaction/java  
- **下載**: https://releases.groupdocs.com/redaction/java/  
- **GitHub**: https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java  
- **免費支援**: https://forum.groupdocs.com/c/redaction/33  
- **臨時授權**: https://purchase.groupdocs.com/temporary-license/

---

**最後更新：** 2026-02-08  
**測試環境：** GroupDocs.Redaction 24.9 (Java)  
**作者：** GroupDocs  

---