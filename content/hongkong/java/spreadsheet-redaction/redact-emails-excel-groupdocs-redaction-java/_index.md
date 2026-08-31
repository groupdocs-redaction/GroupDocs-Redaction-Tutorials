---
date: '2026-02-24'
description: 學習如何使用 GroupDocs.Redaction Java API 在 Excel 試算表中刪除敏感資料並遮蔽電郵地址。
keywords:
- Redact Emails in Excel
- GroupDocs.Redaction Java API
- Automate Email Redaction
title: 如何使用 GroupDocs.Redaction Java API 在 Excel 試算表中遮蔽敏感資料
type: docs
url: /zh-hant/java/spreadsheet-redaction/redact-emails-excel-groupdocs-redaction-java/
weight: 1
---

# 如何使用 GroupDocs.Redaction Java API 在 Excel 試算表中遮蔽敏感資料

在當今以數據為驅動的世界中，**遮蔽敏感資料**（例如 Excel 活頁簿中的電郵地址）是處理個人資訊者必備的技能。無論是為客戶準備報告、與合作夥伴共享資料，或僅僅是清理資料集，遮蔽電郵地址都有助於遵守 GDPR、CCPA 以及其他隱私法規。在本教學中，你將學習如何使用 GroupDocs.Redaction Java 程式庫，自動定位並取代 Excel 檔案中特定欄位的電郵值。

**你將學到**
- 如何在 Maven 專案中設定 GroupDocs.Redaction for Java。  
- 定位特定工作表與欄位的技巧。  
- 如何使用正則表達式模式**遮蔽電郵地址**。  
- 在保留原始檔案的同時，儲存已遮蔽檔案的最佳實踐。

在深入程式碼之前，先確保你的開發環境已就緒。

## 快速解答
- **「遮蔽敏感資料」是什麼意思？** 指永久移除或遮蔽文件中的個人可識別資訊 (PII)。  
- **哪個程式庫負責遮蔽？** GroupDocs.Redaction for Java。  
- **我需要授權嗎？** 免費試用可用於測試；正式環境需購買永久授權。  
- **我可以自行選擇取代文字嗎？** 可以，你可以指定任何佔位符，例如「[customer email]」。  
- **這種方法對大型試算表安全嗎？** 安全，只要遵循指南中的效能建議。

## 前置條件

要跟隨本教學，你需要：

- Java Development Kit (JDK) 8 或以上。  
- 基本的 Java 知識並熟悉 Maven。  
- 取得 GroupDocs.Redaction 程式庫（可透過 Maven 或直接下載連結）。

## 設定 GroupDocs.Redaction for Java

GroupDocs.Redaction for Java 透過 Maven 套件庫發佈，讓整合變得相當簡單。

**Maven 設定**  
將儲存庫與相依性加入你的 `pom.xml` 檔案：

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

**直接下載**  
或者，你也可以從 [GroupDocs.Redaction releases](https://releases.groupdocs.com/redaction/java/) 下載最新的 GroupDocs.Redaction for Java 版本。

### 取得授權

GroupDocs 提供免費試用讓你評估 API。對於持續性的專案，你可能需要臨時授權或正式授權：

- **Free Trial（免費試用）:** 功能受限的評估。  
- **Temporary License（臨時授權）:** 可於 [GroupDocs’ website](https://purchase.groupdocs.com/temporary-license/) 申請。  
- **Full License（正式授權）:** 購買後可無限制於正式環境使用。

### 基本初始化

先建立指向 Excel 檔案的 `Redactor` 實例：

```java
import com.groupdocs.redaction.Redactor;

public class RedactEmails {
    public static void main(String[] args) {
        // Initialize the redactor with your document path
        try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_XLSX")) {
            // Your redaction logic will go here
        }
    }
}
```

## 實作指南

以下為逐步說明，展示如何從特定欄位**遮蔽敏感資料**。

### 載入文件

首先，使用剛才建立的 `Redactor` 開啟活頁簿：

```java
import com.groupdocs.redaction.Redactor;

public class RedactEmails {
    public static void main(String[] args) {
        try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_XLSX")) {
            // Proceed to the next steps for redaction
        }
    }
}
```

### 設定過濾條件

`CellFilter` 讓你將遮蔽範圍縮小至特定工作表與欄位。在此範例中，我們針對 **Customers** 工作表的 B 欄（索引 1）進行遮蔽：

```java
import com.groupdocs.redaction.redactions.CellFilter;

// Create and configure the filter
CellFilter filter = new CellFilter();
filter.setColumnIndex(1); // Targeting the second column (index starts at 0)
filter.setWorkSheetName("Customers"); // Specify the worksheet name
```

### 定義電郵模式

使用正則表達式偵測電郵地址。以下模式可匹配大多數常見的電郵格式：

```java
import java.util.regex.Pattern;

// Define regex pattern for matching emails
Pattern expression = Pattern.compile("^\\w+([-+.']\\w+)*@\\w+([-.]\\w+)*\\.\\w+([-.]\\w+)*$");
```

### 套用遮蔽

現在結合過濾條件、模式與取代選項，以**遮蔽電郵地址**。`ReplacementOptions` 物件允許你定義在被遮蔽儲存格中顯示的佔位文字。

```java
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.RedactorChangeLog;
import com.groupdocs.redaction.redactions.CellColumnRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

// Apply redaction
RedactorChangeLog result = redactor.apply(new CellColumnRedaction(filter, expression, new ReplacementOptions("[customer email]")));

// Save changes if successful
if (result.getStatus() != RedactionStatus.Failed) {
    SaveOptions saveOptions = new SaveOptions();
    saveOptions.setAddSuffix(true); // Add a suffix to the saved file name
    redactor.save(saveOptions);
}
```

### 疑難排解技巧
- **正則表達式準確度：** 在各種電郵樣本上測試你的正則表達式，確保能捕捉所有預期的格式。  
- **欄位索引：** 記得欄位索引從 0 開始；請再次確認欲遮蔽欄位的索引。  
- **工作表名稱：** 名稱區分大小寫，請使用 Excel 中顯示的完整工作表名稱。

## 為什麼要遮蔽敏感資料？

- **合規性：** 符合 GDPR、CCPA 以及各行業的隱私規範。  
- **風險降低：** 防止在外部分享檔案時意外洩露個人識別資訊。  
- **資料治理：** 透過永久移除已存檔資料集中的 PII，維持乾淨的稽核紀錄。

## 實務應用

1. **資料隱私合規：** 在將試算表發送給合作夥伴前自動移除電郵地址。  
2. **內部稽核：** 在內部審查時匿名化客戶資料。  
3. **報告流程：** 將遮蔽步驟整合至排程報告產生工作中。

## 效能考量

- **批次處理：** 若需遮蔽多個檔案，請依序處理並盡可能重複使用 `Redactor` 實例。  
- **記憶體管理：** 使用 try‑with‑resources 區塊（如範例所示）關閉 `Redactor`，即時釋放原生資源。  
- **大型資料集：** 對於擁有數千列的活頁簿，建議在遮蔽前先過濾列以降低負擔。

## 常見問題

**Q: 如果我的電郵正則表達式未能匹配所有格式怎麼辦？**  
A: 調整模式以包含更多字元，或使用更寬鬆的表達式，然後重新執行遮蔽。

**Q: 我可以一次遮蔽多個欄位嗎？**  
A: 可以。為每個欄位建立獨立的 `CellFilter`，並對每個過濾條件呼叫 `redactor.apply`。

**Q: GroupDocs.Redaction 適用於非常大的 Excel 檔案嗎？**  
A: 表現良好，特別是當你一次處理單一工作表並在每個檔案處理完畢後釋放資源時。

**Q: 在遮蔽過程中發生錯誤該如何處理？**  
A: 檢查 `RedactorChangeLog` 的狀態；非失敗狀態即表示操作成功。將任何失敗情況記錄下來以便除錯。

**Q: 我可以自訂取代文字嗎？**  
A: 當然可以。將任意字串傳入 `ReplacementOptions`，例如「[redacted]」或產生的代碼。

## 資源

- [Documentation](https://docs.groupdocs.com/redaction/java/)  
- [API Reference](https://reference.groupdocs.com/redaction/java)  
- [Download GroupDocs.Redaction](https://releases.groupdocs.com/redaction/java/)  
- [GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- [Free Support Forum](https://forum.groupdocs.com/c/redaction/33)  
- [Temporary License Information](https://purchase.groupdocs.com/temporary-license/)

---

**最後更新：** 2026-02-24  
**測試環境：** GroupDocs.Redaction 24.9 for Java  
**作者：** GroupDocs