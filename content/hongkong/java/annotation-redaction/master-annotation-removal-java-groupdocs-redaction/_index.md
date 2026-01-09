---
date: '2025-12-19'
description: 學習如何使用 GroupDocs.Redaction 及正則表達式在 Java 中刪除註釋。透過我們的完整指南，簡化文件管理。
keywords:
- annotation removal java
- groupdocs redaction setup
- regex annotation cleanup
title: 如何在 Java 中使用 GroupDocs.Redaction 刪除註釋
type: docs
url: /zh-hant/java/annotation-redaction/master-annotation-removal-java-groupdocs-redaction/
weight: 1
---

# 如何在 Java 中使用 GroupDocs.Redaction 刪除註釋

如果你曾經卡在嘗試從 PDF、Word 檔或 Excel 表格中 **刪除註釋**，就會知道手動清理有多耗時。幸運的是，GroupDocs.Redaction for Java 為你提供程式化的方式，只需幾行程式碼即可剔除不需要的備註、評論或標記。本指南將帶你逐步了解所需的一切——從設定 Maven 相依性到套用基於正則表達式的過濾器，只刪除你目標的註釋。

## 快速解答
- **什麼函式庫負責註釋刪除？** GroupDocs.Redaction for Java.  
- **哪個關鍵字會觸發移除？** 你自行定義的正則表達式模式（例如 `(?im:(use|show|describe))`）。  
- **我需要授權嗎？** 試用版可用於評估；正式環境需購買商業授權。  
- **我可以將清理後的檔案另存新檔名嗎？** 可以——使用 `SaveOptions.setAddSuffix(true)`。  
- **Maven 是唯一加入函式庫的方式嗎？** 不是，你也可以直接下載 JAR。

## 在 Java 中「如何刪除註釋」是什麼意思？
刪除註釋指的是以程式方式定位並移除文件中的標記物件（評論、突顯、便利貼）。使用 GroupDocs.Redaction，你可以依文字內容來鎖定這些物件，非常適合 **data anonymization java** 專案、**legal document redaction**，或任何需要乾淨、可分享檔案的工作流程。

## 為什麼使用 GroupDocs.Redaction 來移除註釋？
- **精準度** – 正則表達式讓你精確指定要刪除的註釋。  
- **速度** – 批次處理數百個檔案，無需手動開啟每個檔案。  
- **合規性** – 確保敏感評論不會外洩。  
- **跨格式支援** – 支援 PDF、DOCX、XLSX 等多種格式。

## 前置條件
- Java JDK 1.8 或更新版本。  
- 如 IntelliJ IDEA 或 Eclipse 等 IDE。  
- 基本的正則表達式概念。

## Maven 相依性設定（GroupDocs）

在你的 `pom.xml` 中加入 GroupDocs 儲存庫與 Redaction 套件：

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

### 直接下載（備選）

如果不想使用 Maven，可從官方頁面取得最新的 JAR： [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/)。

#### 取得授權步驟
1. **免費試用** – 下載試用版以體驗核心功能。  
2. **臨時授權** – 申請臨時金鑰以完整測試功能。  
3. **購買** – 取得商業授權以供正式使用。

## 基本初始化與設定

以下程式碼示範如何建立 `Redactor` 實例並設定基本的儲存選項：

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;

public class InitializeRedaction {
    public static void main(String[] args) throws Exception {
        // Load the document using Redactor
        final Redactor redactor = new Redactor("path/to/your/document");
        
        try {
            // Perform your redaction operations here
            
            // Save options can be customized as needed
            SaveOptions saveOptions = new SaveOptions();
            saveOptions.setAddSuffix(true);  // Example option: Add suffix to filename
            
            // Save the modified document
            redactor.save(saveOptions, "path/to/output/document");
        } finally {
            redactor.close();  // Always close resources to prevent memory leaks
        }
    }
}
```

## 步驟說明：刪除註釋

### 步驟 1：載入文件

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/ANNOTATED_XLSX");
```

### 步驟 2：套用基於正則表達式的註釋移除

```java
redactor.apply(new DeleteAnnotationRedaction("(?im:(use|show|describe))"));
```

- **說明** – 模式 `(?im:(use|show|describe))` 為不區分大小寫 (`i`) 且多行模式 (`m`)。它會匹配任何包含 *use*、*show* 或 *describe* 的註釋。

### 步驟 3：設定儲存選項

```java
SaveOptions saveOptions = new SaveOptions();
saveOptions.setAddSuffix(true);  // Append a suffix to the output filename
saveOptions.setRasterizeToPDF(false);  // Do not convert to PDF format
```

### 步驟 4：儲存並釋放資源

```java
redactor.save(saveOptions, "YOUR_OUTPUT_DIRECTORY/RedactedDocument");
redactor.close();  // Always close the Redactor instance
```

**故障排除提示**  
- 確認你的正則表達式確實匹配欲刪除的註釋文字。  
- 若 `save` 呼叫拋出 `IOException`，請再次檢查檔案系統權限。

## 移除註釋（Java）— 常見使用情境
1. **Data Anonymization Java** – 在分享資料集前，剔除包含個人識別資訊的審閱者評論。  
2. **Legal Document Redaction** – 自動刪除可能洩漏特權資訊的內部備註。  
3. **批次處理管線** – 將上述步驟整合至 CI/CD 工作，以即時清理產生的報告。  

## 儲存已編輯文件 — 最佳實踐
- **加入後綴** (`setAddSuffix(true)`) 以保留原始檔，同時明確標示已編輯的版本。  
- **避免光柵化**，除非需要平面化的 PDF；保留原生格式可維持可搜尋性。  
- **及時關閉 Redactor**，釋放原生記憶體，防止長時間服務的記憶體洩漏。

## 效能考量
- **優化正則表達式** – 複雜的模式會增加 CPU 時間，尤其在大型 PDF 上。  
- **重複使用 Redactor 實例** 僅在處理同類型多個文件時使用；否則每個檔案重新建立，以降低記憶體佔用。  
- **效能分析** – 使用 Java 效能分析工具（如 VisualVM）找出批次操作的瓶頸。

## 常見問答
**Q: 什麼是 GroupDocs.Redaction for Java？**  
A: 這是一個 Java 函式庫，可對多種文件格式的文字、元資料與註釋進行編輯遮蔽。

**Q: 如何在一次執行中套用多個正則表達式？**  
A: 在單一模式中使用管道符號 (`|`) 結合，或連續呼叫多個 `DeleteAnnotationRedaction`。

**Q: 函式庫是否支援非文字格式，如影像？**  
A: 支援，可對基於影像的 PDF 及其他點陣格式進行編輯遮蔽，但註釋移除僅適用於支援的向量格式。

**Q: 若我的文件類型未列在支援清單中該怎麼辦？**  
A: 查看最新的 [Documentation](https://docs.groupdocs.com/redaction/java/) 以取得更新，或先將檔案轉換為支援的格式。

**Q: 在編輯遮蔽過程中應如何處理例外？**  
A: 將遮蔽邏輯包於 try‑catch 區塊，記錄例外細節，並確保在 finally 區塊中呼叫 `redactor.close()`。

## 其他資源
- [文件說明文件](https://docs.groupdocs.com/redaction/java/)  
- [API 參考手冊](https://reference.groupdocs.com/redaction/java)  
- [下載 GroupDocs.Redaction](https://releases.groupdocs.com/redaction/java/)  
- [GitHub 程式庫](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- [免費支援論壇](https://forum.groupdocs.com/c/redaction/33)

---

**最後更新：** 2025-12-19  
**測試版本：** GroupDocs.Redaction 24.9 for Java  
**作者：** GroupDocs