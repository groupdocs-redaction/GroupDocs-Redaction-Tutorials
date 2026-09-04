---
date: '2026-08-09'
description: 了解如何使用 GroupDocs.Redaction Java API 在 Excel 試算表中隱藏個人資料並遮蔽電子郵件地址。
keywords:
- how to hide personal data
- mask email addresses excel
- GroupDocs.Redaction Java
- Excel redaction tutorial
lastmod: '2026-08-09'
og_description: 一步一步了解如何使用 GroupDocs.Redaction Java API 在 Excel 檔案中隱藏個人資料並遮蔽電子郵件地址——快速且安全的
  GDPR 合規解決方案。
og_image_alt: Guide showing Java code that redacts email addresses in an Excel spreadsheet
og_title: 如何使用 GroupDocs Java 在 Excel 中隱藏個人資料
schemas:
- author: GroupDocs
  dateModified: '2026-08-09'
  description: Learn how to hide personal data and mask email addresses in Excel spreadsheets
    using the GroupDocs.Redaction Java API.
  headline: How to hide personal data in Excel with GroupDocs Java
  type: TechArticle
- description: Learn how to hide personal data and mask email addresses in Excel spreadsheets
    using the GroupDocs.Redaction Java API.
  name: How to hide personal data in Excel with GroupDocs Java
  steps:
  - name: '**Partner data exchange** – Automatically strip customer emails before
      sending spreadsheets to vendors.'
    text: '**Partner data exchange** – Automatically strip customer emails before
      sending spreadsheets to vendors.'
  - name: '**Internal audit preparation** – Anonymize employee data during compliance
      reviews.'
    text: '**Internal audit preparation** – Anonymize employee data during compliance
      reviews.'
  - name: '**Scheduled reporting** – Embed the redaction step into nightly batch jobs
      that generate distribution‑ready reports.'
    text: '**Scheduled reporting** – Embed the redaction step into nightly batch jobs
      that generate distribution‑ready reports.'
  type: HowTo
- questions:
  - answer: Extend the pattern to include additional allowed characters (e.g., “+”
      or “_”) and test against a larger sample set, then re‑run the redaction.
    question: My regex still misses some corporate email formats. What should I do?
  - answer: Yes. Create a separate `CellFilter` for each column and invoke `redactor.apply`
      for each filter sequentially.
    question: Can I redact more than one column in a single pass?
  - answer: The library processes sheets incrementally, so files up to several gigabytes
      can be redacted as long as you enable streaming and close the `Redactor` after
      each file.
    question: Is GroupDocs.Redaction able to handle Excel files larger than 1 GB?
  - answer: Inspect the `RedactorChangeLog` returned by `apply`; a non‑failed status
      indicates success, while any errors are listed with line numbers and cell references.
    question: How do I capture redaction results or errors?
  - answer: Absolutely. Build the placeholder string dynamically (e.g., `"[redacted:"
      + UUID.randomUUID() + "]"`) and pass it to `ReplacementOptions`.
    question: Can I use a custom placeholder that includes a unique token per row?
  type: FAQPage
tags:
- hide personal data
- GroupDocs.Redaction
- Java Excel processing
- data privacy
title: 如何使用 GroupDocs Java 在 Excel 中隱藏個人資料
url: /zh-hant/java/spreadsheet-redaction/redact-emails-excel-groupdocs-redaction-java/
weight: 1
---

# 如何在 Excel 中使用 GroupDocs Java 隱藏個人資料

在本指南中，您將學習**如何隱藏個人資料**——具體而言是電子郵件地址——於 Excel 活頁簿，透過使用 GroupDocs.Redaction Java API。無論您需要遵守 GDPR、CCPA 或內部隱私政策，此方法皆可讓您安全地自動化遮蔽，保持原始檔案不變，並產生可供分發的乾淨版本。

## 快速回答
- **什麼是「隱藏個人資料」？** 這表示永久遮蔽或移除檔案中的個人可識別資訊（PII），使其無法再被讀取。  
- **哪個函式庫執行遮蔽？** GroupDocs.Redaction for Java。  
- **執行範例是否需要授權？** 免費試用可用於測試；商業使用則需正式授權。  
- **我可以自訂佔位文字嗎？** 可以——您可以將電子郵件替換為任何字串，例如「[redacted email]」。  
- **此方法適用於大型試算表嗎？** 可以，只要遵循「Performance considerations」章節中的效能建議。

## 什麼是隱藏個人資料？
**隱藏個人資料**指的是對任何能直接或間接識別個人的資訊（例如姓名、電話號碼或電子郵件地址）進行不可逆的移除或遮蔽。此程序確保產生的檔案無法用於重新識別該對象。

## 為什麼使用 GroupDocs.Redaction for Java？
GroupDocs.Redaction 支援 **30 多種輸入與輸出格式**，且能在不將整個檔案載入記憶體的情況下處理 **最多 500,000 行** 的活頁簿，與傳統檔案解析方案相比，可實現 **最高 80 % 的記憶體佔用減少**。這些具體的效益使其成為企業級資料隱私管線的首選。

## 前置條件
- Java Development Kit (JDK) 8 或更新版本。  
- 具備 Maven 建置檔的基本認識。  
- 取得 GroupDocs.Redaction Java 函式庫（可透過 Maven 或官方發行頁面下載）。

## 設定 GroupDocs.Redaction for Java

### 如何將 GroupDocs.Redaction 加入 Maven 專案？
將 GroupDocs 儲存庫與 Redaction 相依性加入您的 `pom.xml` 檔案（參見 [GroupDocs.Redaction releases](https://releases.groupdocs.com/redaction/java/)）。然後執行 `mvn clean install` 下載相應的套件。

```text
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
```

### 如何取得 GroupDocs.Redaction 的授權？
GroupDocs 提供三種授權選項（參見 [GroupDocs’ website](https://purchase.groupdocs.com/temporary-license/)）：

- **免費試用** – 功能受限的評估版，無需信用卡。  
- **臨時授權** – 從 GroupDocs 網站取得的 30 天評估金鑰。  
- **完整授權** – 透過銷售入口購買的永久生產授權。

```text
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
```

## 實作指南

### 如何為 Excel 檔案建立 Redactor 實例？
`Redactor` 類別是載入文件並提供遮蔽操作的主要入口點。  
建立指向來源活頁簿的 `Redactor` 物件。`Redactor` 類別是所有遮蔽操作的入口點；它將檔案載入受管理的記憶體結構，同時保持原始檔案於磁碟上。

```text
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
```

### 如何將遮蔽限制於單一工作表與欄位？
`CellFilter` 類別讓您指定要檢查遮蔽的工作表與欄位。使用 `CellFilter` 來設定目標工作表名稱與欄位索引。`CellFilter` 會在遮蔽引擎評估之前過濾儲存格，確保僅處理預期的儲存格。

```text
```java
import com.groupdocs.redaction.redactions.CellFilter;

// Create and configure the filter
CellFilter filter = new CellFilter();
filter.setColumnIndex(1); // Targeting the second column (index starts at 0)
filter.setWorkSheetName("Customers"); // Specify the worksheet name
```
```

### 如何定義匹配大多數電子郵件地址的正規表達式模式？
`java.util.regex` 中的 `Pattern` 類別代表已編譯的正規表達式，用於匹配文字。建立一個包含典型電子郵件格式的正則表達式 `Pattern` 物件。以下模式可匹配大多符合 RFC‑5322 標準的地址，同時忽略格式錯誤的字串。

```text
```java
import java.util.regex.Pattern;

// Define regex pattern for matching emails
Pattern expression = Pattern.compile("^\\w+([-+.']\\w+)*@\\w+([-.]\\w+)*\\.\\w+([-.]\\w+)*$");
```
```

### 如何套用遮蔽並以佔位文字取代電子郵件？
`ReplacementOptions` 類別定義匹配內容的取代方式，例如佔位文字。將過濾器、模式與 `ReplacementOptions` 實例結合。`ReplacementOptions` 允許您設定每個被遮蔽儲存格將顯示的精確佔位文字。

```text
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
```

## 常見問題與故障排除
- **正規表達式未涵蓋所有情況** – 請以具代表性的資料樣本測試此表達式，並視需要調整字元類別。  
- **欄位索引錯誤** – 請記得欄位索引從 0 開始；B 欄的索引為 1。  
- **工作表名稱大小寫敏感** – 請使用 Excel 中顯示的完整工作表名稱；“Customers” ≠ “customers”。  
- **資源泄漏** – 如範例所示，將 `Redactor` 包裹在 try‑with‑resources 區塊中，以確保本機資源即時釋放。

## 為什麼在 Excel 中隱藏個人資料？
在 Excel 中隱藏個人資料可移除所有可識別個人的資訊，確保檔案無法被用於追蹤個人。這可保護隱私、符合規範要求，並防止在與外部單位共享試算表或公開資料時發生意外洩漏。

- **法規遵循** – 滿足 GDPR、CCPA 以及行業特定的隱私規範。  
- **風險緩解** – 防止在與外部合作夥伴共享檔案時意外暴露個人可識別資訊 (PII)。  
- **審計就緒** – 透過永久移除存檔資料集中的敏感值，保留乾淨且不可變更的審計軌跡。

## 實務應用
1. **合作夥伴資料交換** – 在將試算表發送給供應商前，自動剔除客戶電子郵件。  
2. **內部審計準備** – 在合規審查期間匿名化員工資料。  
3. **排程報告** – 將遮蔽步驟嵌入每晚的批次工作，以產生可供分發的報告。

## 效能考量
- **批次處理** – 在多個檔案間重複使用單一 `Redactor` 實例，以減少 JVM 開銷。  
- **記憶體管理** – API 會一次處理一個工作表；對於超過 100 MB 的活頁簿，請分批處理列以保持堆積使用量低。  
- **大型資料集** – 處理超過 100 k 列的檔案時，啟用串流模式（在 24.9 版提供），以將記憶體消耗控制在 200 MB 以下。

## 常見問答
**Q: 我的正規表達式仍遺漏某些公司郵件格式。該怎麼辦？**  
A: 擴充模式以包含其他允許的字元（例如 “+” 或 “_”），並以更大的樣本集測試，之後重新執行遮蔽。

**Q: 我能在一次執行中遮蔽多個欄位嗎？**  
A: 可以。為每個欄位建立獨立的 `CellFilter`，並依序對每個過濾器呼叫 `redactor.apply`。

**Q: GroupDocs.Redaction 能處理大於 1 GB 的 Excel 檔案嗎？**  
A: 函式庫會逐步處理工作表，只要啟用串流模式並在每個檔案處理完畢後關閉 `Redactor`，即可遮蔽數 GB 大小的檔案。

**Q: 我要如何取得遮蔽結果或錯誤資訊？**  
A: 檢查 `apply` 回傳的 `RedactorChangeLog`；非失敗狀態表示成功，任何錯誤會以行號與儲存格參考列出。

**Q: 我能使用包含每列唯一代碼的自訂佔位文字嗎？**  
A: 當然可以。動態建立佔位字串（例如 `"[redacted:" + UUID.randomUUID() + "]"`），並傳入 `ReplacementOptions`。

## 其他資源
- [文件說明](https://docs.groupdocs.com/redaction/java/)
- [API 參考](https://reference.groupdocs.com/redaction/java)
- [下載 GroupDocs.Redaction](https://releases.groupdocs.com/redaction/java/)
- [GitHub 程式庫](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
- [免費支援論壇](https://forum.groupdocs.com/c/redaction/33)
- [臨時授權資訊](https://purchase.groupdocs.com/temporary-license/)

---

**最後更新：** 2026-08-09  
**測試環境：** GroupDocs.Redaction 24.9 for Java  
**作者：** GroupDocs

## 相關教學
- [如何在試算表中篩選資料 – GroupDocs.Redaction Java](/redaction/java/spreadsheet-redaction/)
- [在 Java 中遮蔽敏感資料 – 使用 GroupDocs.Redaction 進行個人資訊遮蔽](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)
- [在 Java 中遮蔽敏感資料 – GroupDocs.Redaction 指南](/redaction/java/getting-started/)