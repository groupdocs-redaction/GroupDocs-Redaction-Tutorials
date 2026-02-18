---
date: '2026-02-18'
description: 學習如何在 Java 中使用 GroupDocs.Redaction、正則表達式過濾移除 PDF 註釋，並以檔名後綴儲存已編輯的文件。
keywords:
- annotation removal java
- groupdocs redaction setup
- regex annotation cleanup
title: 使用 GroupDocs.Redaction 在 Java 中移除 PDF 註釋
type: docs
url: /zh-hant/java/annotation-redaction/master-annotation-removal-java-groupdocs-redaction/
weight: 1
---

# 使用 GroupDocs.Redaction 在 Java 中移除 PDF 註釋

如果您需要快速且可靠地**移除 PDF 註釋**——無論是評論、標記或便利貼——GroupDocs.Redaction for Java 為您提供乾淨的程式化解決方案。本教學將從 Maven 設定說明到基於正則表達式的過濾器，只刪除您指定的註釋，並示範如何**儲存已編輯的文件**，同時在檔名加入後綴，使原始檔保持不變。

## 快速解答
- **什麼函式庫負責註釋刪除？** GroupDocs.Redaction for Java.  
- **哪個關鍵字會觸發移除？** 您自行定義的正則表達式模式（例如 `(?im:(use|show|describe))`）。  
- **我需要授權嗎？** 試用版可用於評估；正式環境需購買商業授權。  
- **我可以將清理後的檔案另存新檔名嗎？** 可以——使用 `SaveOptions.setAddSuffix(true)`。  
- **Maven 是唯一加入函式庫的方式嗎？** 不是，您也可以直接下載 JAR。

## 什麼是移除 PDF 註釋？
移除 PDF 註釋是指以程式方式定位並刪除文件中的標記物件（評論、標記、便利貼）。使用 GroupDocs.Redaction，您可以依文字內容針對這些物件，讓它非常適合**法律文件編輯**、資料匿名化專案，或任何需要乾淨、可分享檔案的工作流程。

## 為何使用 GroupDocs.Redaction 來移除 PDF 註釋？
- **精確度** – 正則表達式讓您精確指定要刪除的註釋。  
- **速度** – 批次處理**多個文件**，無需手動開啟每個檔案。  
- **合規性** – 確保敏感評論不會外洩。  
- **跨格式支援** – 支援 PDF、DOCX、XLSX 等多種格式，讓您在同一平台處理所有辦公文件。

## 前置條件
- Java JDK 1.8 或更新版本。  
- 如 IntelliJ IDEA 或 Eclipse 等 IDE。  
- 具備正則表達式的基本概念。  

## Maven 依賴 GroupDocs

在 `pom.xml` 中加入 GroupDocs 儲存庫與 Redaction 套件：

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

如果您不想使用 Maven，可從官方頁面下載最新的 JAR： [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

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

## 移除 PDF 註釋的逐步指南

### 步驟 1：載入文件

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/ANNOTATED_XLSX");
```

### 步驟 2：套用基於正則表達式的註釋移除

```java
redactor.apply(new DeleteAnnotationRedaction("(?im:(use|show|describe))"));
```

- **說明** – 模式 `(?im:(use|show|describe))` 為不區分大小寫 (`i`) 且多行 (`m`)。它會匹配任何包含 *use*、*show* 或 *describe* 的註釋。

### 步驟 3：設定儲存選項（加入檔名後綴）

```java
SaveOptions saveOptions = new SaveOptions();
saveOptions.setAddSuffix(true);  // Append a suffix to the output filename
saveOptions.setRasterizeToPDF(false);  // Do not convert to PDF format
```

### 步驟 4：儲存並釋放資源（儲存已編輯的文件）

```java
redactor.save(saveOptions, "YOUR_OUTPUT_DIRECTORY/RedactedDocument");
redactor.close();  // Always close the Redactor instance
```

**故障排除提示**  
- 確認您的正則表達式確實匹配您欲刪除的註釋文字。  
- 如果 `save` 呼叫拋出 `IOException`，請再次檢查檔案系統權限。  

## 常見使用情境

1. **Data Anonymization Java** – 在分享資料集前，剔除包含個人識別資訊的審閱者評論。  
2. **Legal Document Redaction** – 自動刪除可能洩漏機密資訊的內部註釋。  
3. **Batch Processing Pipelines** – 將上述步驟整合至 CI/CD 工作，**處理多個文件** 並即時清理產生的報告。  

## 效能考量

- **優化正則表達式** – 複雜的表達式會增加 CPU 時間，尤其在大型 PDF 上。  
- **重複使用 Redactor 實例** 僅在處理同類型多個檔案時使用；否則每個檔案重新建立，以降低記憶體佔用。  
- **效能分析** – 使用 Java 效能分析工具（如 VisualVM）找出批次操作的瓶頸。  

## 常見問題

**Q: 什麼是 GroupDocs.Redaction for Java？**  
A: 這是一個 Java 函式庫，可對多種文件格式的文字、元資料與註釋進行編輯。

**Q: 如何在一次執行中套用多個正則表達式模式？**  
A: 可在單一模式中使用管道符號 (`|`) 結合，或串接多個 `DeleteAnnotationRedaction` 呼叫。

**Q: 此函式庫是否支援非文字格式，如圖像？**  
A: 是的，它可以編輯基於圖像的 PDF 及其他點陣格式，但註釋移除僅適用於支援的向量格式。

**Q: 如果我的文件類型未列在支援清單中該怎麼辦？**  
A: 請檢查最新的[文件說明](https://docs.groupdocs.com/redaction/java/)以獲得更新，或先將檔案轉換為支援的格式。

**Q: 在編輯過程中應如何處理例外情況？**  
A: 將編輯邏輯放在 try‑catch 區塊中，記錄例外細節，並確保在 finally 區塊中呼叫 `redactor.close()`。

## 其他資源

- [Documentation](https://docs.groupdocs.com/redaction/java/)
- [API Reference](https://reference.groupdocs.com/redaction/java)
- [Download GroupDocs.Redaction](https://releases.groupdocs.com/redaction/java/)
- [GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
- [Free Support Forum](https://forum.groupdocs.com/c/redaction/33)

---

**最後更新：** 2026-02-18  
**測試環境：** GroupDocs.Redaction 24.9 for Java  
**作者：** GroupDocs  

---