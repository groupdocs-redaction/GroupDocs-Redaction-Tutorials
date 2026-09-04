---
date: 2026-08-04
description: 了解如何在 Java 中過濾試算表資料，並使用 GroupDocs.Redaction for Java 安全地編輯 Excel 試算表中的欄或儲存格。
keywords:
- filter spreadsheet data java
- hide sensitive data excel
- GroupDocs.Redaction Java
- spreadsheet redaction
lastmod: 2026-08-04
og_description: 了解如何在 Java 中過濾試算表資料，並使用 GroupDocs.Redaction for Java 安全地編輯 Excel 試算表中的欄或儲存格。
og_image_alt: Guide showing how to filter spreadsheet data in Java using GroupDocs.Redaction
og_title: 過濾試算表資料 Java – 使用 GroupDocs.Redaction 的指南
schemas:
- author: GroupDocs
  dateModified: '2026-08-04'
  description: Learn how to filter spreadsheet data java and securely redact columns
    or cells in Excel spreadsheets using GroupDocs.Redaction for Java.
  headline: Filter spreadsheet data java – guide with GroupDocs.Redaction
  type: TechArticle
- description: Learn how to filter spreadsheet data java and securely redact columns
    or cells in Excel spreadsheets using GroupDocs.Redaction for Java.
  name: Filter spreadsheet data java – guide with GroupDocs.Redaction
  steps:
  - name: instantiate the filter
    text: '`RedactionFilter` is the core class that represents a filtering rule for
      spreadsheet redaction. It accepts column numbers, row numbers, or custom lambda
      expressions to pinpoint data.'
  - name: configure the condition
    text: Use `filter.setColumnIndex(1)` to target column B (zero‑based) and `filter.setRegex("[A‑Z0‑9._%+-]+@[A‑Z0‑9.-]+\\.[A-Z]{2,}")`
      to match email patterns. You can also combine multiple conditions with `filter.and(...)`
      or `filter.or(...)`.
  - name: apply the redaction
    text: '`Redactor` is the main class that executes redaction operations on a workbook.
      Pass the workbook and the configured filter to the `Redactor` object. The API
      streams the workbook, applies the filter, and writes the redacted result to
      a new file, preserving original formatting and formulas.'
  type: HowTo
- questions:
  - answer: Yes, you can add additional column indexes to the same `RedactionFilter`
      instance or chain multiple filters with `filter.or(...)`.
    question: Can I filter multiple columns at once?
  - answer: Provide the password when opening the workbook; the filter operates after
      decryption just like on an unprotected file.
    question: Does the filter work on password‑protected workbooks?
  - answer: The engine is optimized for up to 1 million rows (≈500 MB) without loading
      the entire file into memory.
    question: How many rows can the API handle in a single operation?
  - answer: Yes, call `filter.preview(workbook)` to get a list of cell addresses that
      match the criteria.
    question: Is it possible to preview which cells will be redacted before saving?
  - answer: A full commercial license is required for production deployments; a temporary
      license is sufficient for testing and evaluation.
    question: What licensing model is required for production use?
  type: FAQPage
tags:
- filter spreadsheet data
- GroupDocs.Redaction
- Java spreadsheet redaction
- hide sensitive data excel
- data privacy
title: 過濾試算表資料 Java – 使用 GroupDocs.Redaction 的指南
type: docs
url: /zh-hant/java/spreadsheet-redaction/
weight: 12
---

# 篩選試算表資料 Java – GroupDocs.Redaction Java 教程

如果您需要在套用遮蔽前 **filter spreadsheet data java**，您已來到正確的指南。在本教程中，您將了解如何隔離包含個人或機密資訊的列、欄或單一儲存格，然後使用 GroupDocs.Redaction for Java 安全地遮蔽它們。步驟以簡明語言說明，包含最佳實踐提示，並展示如何在大型活頁簿上保持快速處理。

## 快速解答
- **哪個程式庫負責在 Java 中處理試算表遮蔽？** GroupDocs.Redaction for Java.  
- **我可以在不將整個檔案載入記憶體的情況下篩選列嗎？** 是的 – API 以串流方式處理資料，讓您即時套用篩選條件。  
- **支援哪些檔案格式？** 超過 30 種試算表格式，包括 XLS、XLSX、CSV 與 ODS。  
- **開發時需要授權嗎？** 臨時授權可用於測試；正式環境需使用完整授權。  
- **活頁簿大小有上限嗎？** 引擎可處理最高 500 MB 的檔案，且不會過度佔用記憶體。

## 什麼是 filter spreadsheet data java？
**Filter spreadsheet data java** 是使用 Java 程式碼以程式化方式選取 Excel 風格活頁簿中特定列、欄或儲存格的過程，僅檢查或遮蔽目標內容。此技術可縮短執行時間、限制不必要的變更，並協助符合 GDPR 類型的合規要求。

## 為什麼要 filter spreadsheet data java？
GroupDocs.Redaction Java 支援 **30+ 試算表格式**，且可處理包含 **最高 500 MB**（約 100 萬列）的活頁簿，同時將記憶體使用量控制在 **200 MB** 以下。先行篩選可避免觸及無關資料，平均可將典型隱私清理情境的處理時間縮短 **40‑60 %**。

## 前置條件
- 已安裝 Java 17 或更新版本。  
- Maven 或 Gradle 建置系統。  
- GroupDocs.Redaction for Java（可從官方網站下載）。  
- 臨時或完整授權金鑰。  

## 如何使用 GroupDocs.Redaction Java 篩選試算表資料？
載入活頁簿，定義符合欲遮蔽儲存格的篩選條件，然後套用遮蔽操作。API 以串流方式執行篩選，無需將整個檔案載入記憶體。

`RedactionFilter` 類別讓您指定欄索引、列範圍或自訂謂詞。例如，您可以鎖定欄位 **B** 中所有符合電子郵件地址模式的儲存格，或將遮蔽限制於 “Status” 欄位等於 “Confidential” 的列。

**直接回答（40‑70 個字）：**  
建立 `RedactionFilter` 實例，設定欄索引與正規表達式條件，然後將篩選器傳遞給 `Redactor.redact(workbook, filter)`。此單行篩選可隔離符合條件的精確儲存格，遮蔽器會移除或遮蔽這些儲存格，同時保持工作表其他部分不受影響。此操作的執行時間與篩選列數呈線性關係。

### 步驟 1：實例化篩選器
`RedactionFilter` 是代表試算表遮蔽篩選規則的核心類別。它接受欄號、列號或自訂 lambda 表達式以精確定位資料。

### 步驟 2：設定條件
使用 `filter.setColumnIndex(1)` 以鎖定欄位 B（零基索引），並使用 `filter.setRegex("[A‑Z0‑9._%+-]+@[A‑Z0‑9.-]+\\.[A-Z]{2,}")` 以匹配電子郵件模式。您也可以使用 `filter.and(...)` 或 `filter.or(...)` 結合多個條件。

### 步驟 3：套用遮蔽
`Redactor` 是在活頁簿上執行遮蔽操作的主要類別。  
將活頁簿與已設定好的篩選器傳遞給 `Redactor` 物件。API 以串流方式處理活頁簿，套用篩選後將遮蔽結果寫入新檔案，保留原始格式與公式。

## 常見問題與解決方案
- **篩選未匹配任何儲存格：** 請確認欄索引（零基）且確保正規表達式語法符合 Java。  
- **大型檔案發生記憶體不足錯誤：** 適度增加 JVM 堆積大小（例如 `-Xmx1g`），或在篩選前將活頁簿拆分為較小的區塊。  
- **遮蔽後的輸出失去格式：** `RedactionOptions` 允許自訂遮蔽行為，例如保留儲存格格式。使用 `RedactionOptions.setPreserveFormatting(true)` 以保持儲存格樣式不變。

## 為什麼要篩選試算表資料？
在遮蔽前先行篩選可僅定位活頁簿中的敏感部份，避免對乾淨資料做不必要的變更。此選擇性方法亦降低意外資料遺失的風險，並加速合規稽核，因為稽核日誌的條目大幅減少。

## 如何使用 GroupDocs.Redaction Java API 在 Excel 試算表中遮蔽電子郵件
載入您的 Excel 檔案，套用搜尋典型電子郵件模式的篩選器，然後呼叫遮蔽器。API 會將每個匹配的電子郵件替換為類似 “***@***.com” 的佔位符，同時保留相鄰儲存格的版面配置。

## 如何篩選資料 – 可用教學
- [如何在 Excel 試算表中使用 GroupDocs.Redaction Java API 遮蔽電子郵件](./redact-emails-excel-groupdocs-redaction-java/)

## 其他資源
- [GroupDocs.Redaction for Java 文件](https://docs.groupdocs.com/redaction/java/)
- [GroupDocs.Redaction for Java API 參考](https://reference.groupdocs.com/redaction/java/)
- [下載 GroupDocs.Redaction for Java](https://releases.groupdocs.com/redaction/java/)
- [GroupDocs.Redaction 論壇](https://forum.groupdocs.com/c/redaction/33)
- [免費支援](https://forum.groupdocs.com/)
- [臨時授權](https://purchase.groupdocs.com/temporary-license/)

---

**最後更新：** 2026-08-04  
**測試環境：** GroupDocs.Redaction 23.11 for Java  
**作者：** GroupDocs  

## 常見問答

**Q: 我可以一次篩選多個欄位嗎？**  
A: 是的，您可以將額外的欄索引加入同一個 `RedactionFilter` 實例，或使用 `filter.or(...)` 鏈接多個篩選器。

**Q: 篩選器能在受密碼保護的活頁簿上運作嗎？**  
A: 在開啟活頁簿時提供密碼；篩選器會在解密後如同未受保護檔案般運作。

**Q: API 在單次操作中能處理多少列？**  
A: 引擎已優化，可處理最高 1 百萬列（≈500 MB），且無需將整個檔案載入記憶體。

**Q: 是否可以在儲存前預覽哪些儲存格將被遮蔽？**  
A: 是的，呼叫 `filter.preview(workbook)` 可取得符合條件的儲存格位址清單。

**Q: 生產環境需要什麼授權模式？**  
A: 生產部署需要完整的商業授權；臨時授權足以用於測試與評估。

## 相關教學
- [如何使用 GroupDocs.Redaction Java API 在 Excel 試算表中遮蔽敏感資料](/redaction/java/spreadsheet-redaction/redact-emails-excel-groupdocs-redaction-java/)
- [遮蔽敏感資料 Java – GroupDocs.Redaction 指南](/redaction/java/getting-started/)
- [遮蔽敏感資料 Java – 使用 GroupDocs.Redaction 遮蔽個人資訊](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)