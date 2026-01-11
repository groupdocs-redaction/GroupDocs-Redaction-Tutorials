---
date: '2026-01-08'
description: 學習如何在 Java 中使用 GroupDocs.Redaction 的 MetadataSearchRedaction，以安全地刪除敏感文件的元資料。
keywords:
- metadata redaction Java
- GroupDocs Redaction tutorial
- secure document metadata
title: 如何在 Java 中使用 GroupDocs 的 MetadataSearchRedaction
type: docs
url: /zh-hant/java/metadata-redaction/java-metadata-redaction-groupdocs-tutorial/
weight: 1
---

# 如何在 Java 中使用 GroupDocs 的 MetadataSearchRedaction

在本完整指南中，您將了解 **如何使用 MetadataSearchRedaction** 以移除機密的中繼資料——例如公司名稱——從 Word、PDF 以及其他文件格式，使用 GroupDocs.Redaction for Java。完成本教學後，您將能將中繼資料遮蔽整合到任何基於 Java 的工作流程中，並確保敏感資訊安全。

## 快速解答
- **MetadataSearchRedaction 的功能是什麼？** 它會搜尋特定的中繼資料欄位，並將其值替換為自訂文字。  
- **需要哪個函式庫？** GroupDocs.Redaction for Java（v24.9 或更新版本）。  
- **我需要授權嗎？** 免費試用可用於評估；正式環境需購買完整授權。  
- **可以保留原始檔案格式嗎？** 可以——使用 `SaveOptions` 以保留原始格式。  
- **此方法是執行緒安全的嗎？** 每個 `Redactor` 實例彼此獨立，您可以平行處理文件。

## MetadataSearchRedaction 是什麼？
`MetadataSearchRedaction` 是一個專門的遮蔽類別，讓您針對特定的中繼資料屬性（例如 *Company*、*Author*）並以佔位符取代其內容。當您需要在與外部合作夥伴共享文件前匿名化公司資料時，這非常理想。

## 為何使用 MetadataSearchRedaction 進行中繼資料遮蔽？
- **精確度** – 只遮蔽您指定的欄位，文件其餘部分保持不變。  
- **合規性** – 透過移除隱藏識別碼，協助符合 GDPR、HIPAA 以及其他隱私法規。  
- **自動化就緒** – 可無縫整合至批次處理管線或微服務。

## 前置條件
- **GroupDocs.Redaction for Java** ≥ 24.9。  
- 已在機器上安裝 Java 8 或更新版本。  
- 如 IntelliJ IDEA 或 Eclipse 等 IDE（非必須但建議使用）。  
- 基本了解 Maven（或能手動加入 JAR）。

## 設定 GroupDocs.Redaction for Java
將儲存庫與相依性加入您的 `pom.xml`。此步驟可確保 Maven 能自動下載函式庫。

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

*或者，您也可以直接從官方發布頁面下載 JAR：*  
[GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/)

### 取得授權
- **免費試用** – 下載試用授權以探索全部功能。  
- **臨時授權** – 用於延長測試。  
- **完整授權** – 正式部署時必須。

## 基本初始化
建立指向您欲處理文件的 `Redactor` 實例。

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

## 實作指南

### 步驟 1：匯入必要的類別
這些匯入讓您能使用遮蔽引擎、儲存選項與中繼資料工具。

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.redactions.MetadataFilters;
import com.groupdocs.redaction.redactions.MetadataSearchRedaction;
```

### 步驟 2：初始化 Redactor
以來源檔案路徑建立 `Redactor` 實例。

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

### 步驟 3：設定中繼資料搜尋與遮蔽
建立一個 `MetadataSearchRedaction`，搜尋精確字串 **"Company Ltd."**，並以 **"--company--"** 取代。`setFilter` 呼叫將操作限制於 *Company* 中繼資料欄位。

```java
MetadataSearchRedaction redaction = new MetadataSearchRedaction("Company Ltd.", "--company--");
redaction.setFilter(MetadataFilters.Company);
```

### 步驟 4：套用遮蔽
對已開啟的文件執行遮蔽。

```java
redactor.apply(redaction);
```

### 步驟 5：使用自訂選項儲存
設定 `SaveOptions`，使遮蔽後的檔案在保留原始格式的同時，加上 “_Redacted” 後綴。

```java
SaveOptions tmp0 = new SaveOptions();
tmp0.setAddSuffix(true);  // Adds "_Redacted" to file name
	tmp0.setRasterizeToPDF(false);  // Keeps original format

redactor.save(tmp0);
```

### 步驟 6：釋放資源
務必關閉 `Redactor`，釋放原生資源並避免記憶體洩漏。

```java
finally {
    redactor.close();
}
```

## 常見問題與解決方案
- **FileNotFoundException** – 再次確認傳遞給 `Redactor` 的路徑。使用絕對路徑或 `Paths.get(...)` 以提升可靠性。  
- **未觀察到變更** – 確認您目標的中繼資料欄位實際包含搜尋字串；預設情況下中繼資料區分大小寫。  
- **大型檔案發生記憶體不足錯誤** – 將文件分成較小批次處理，並在每個檔案處理完畢後即時呼叫 `redactor.close()`。

## 實務應用
1. **法律文件** – 在將合約發送給第三方前，移除客戶公司名稱。  
2. **財務報告** – 匿名化審計檔案中的內部識別碼。  
3. **協作專案** – 在與外部供應商共享草稿時，保護專有資訊。

## 效能考量
- **記憶體管理** – 函式庫會將整個文件載入記憶體；在每個檔案處理完畢後關閉 `Redactor` 為必要步驟。  
- **批次處理** – 在高量情境下，遍歷檔案集合並重複使用單一 `SaveOptions` 實例。  
- **保持更新** – 新版本會帶來效能調整與錯誤修正；請始終使用最新穩定版。

## 結論
您現在已了解 **如何使用 MetadataSearchRedaction** 以安全地從文件中移除公司中繼資料，使用 GroupDocs.Redaction for Java。將這些步驟納入您的文件處理管線，以確保合規並保護敏感資訊。

**後續步驟**
- 嘗試其他中繼資料欄位，如 *Author* 或 *Creator*。  
- 將中繼資料遮蔽與文字或影像遮蔽結合，以達到完整解決方案。  

## 常見問答區
1. **什麼是 GroupDocs.Redaction for Java？**  
   - 它是一個功能強大的函式庫，讓您能在 Java 應用程式中對文件的文字、中繼資料與影像進行遮蔽。  
2. **我可以在未購買授權的情況下使用 GroupDocs.Redaction 嗎？**  
   - 可以，但會有使用限制。免費試用或臨時授權可在測試時取得完整功能。  
3. **如何確保在遮蔽過程中保留文件格式？**  
   - 使用 `SaveOptions` 指定需求，例如避免將文件光柵化為 PDF。  
4. **使用 GroupDocs.Redaction 可以遮蔽哪些類型的文件？**  
   - 它支援多種格式，包括 Word、Excel、PowerPoint、PDF 等等。  
5. **如果遇到問題，該去哪裡尋求支援？**  
   - 前往 [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) 取得協助。  

## 常見問題
**Q: MetadataSearchRedaction 能處理加密文件嗎？**  
A: 能。使用接受密碼參數的 `Redactor` 建構子，載入帶有相應密碼的文件。

**Q: 我可以在一次執行中串接多個中繼資料遮蔽嗎？**  
A: 當然可以。建立多個 `MetadataSearchRedaction` 物件，設定不同的過濾條件，並在儲存前依序套用。

**Q: 是否可以在儲存前預覽遮蔽結果？**  
A: 您可以呼叫 `redactor.getRedactions()`，取得待處理遮蔽的清單，並以程式方式檢查。

## 資源
- **文件說明**：於 [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/) 探索詳細指南。  
- **API 參考**：在 [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java) 查看完整 API 參考。  
- **下載函式庫**：從 [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/) 取得最新版本。  
- **原始碼**：於 [GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java) 檢視與貢獻。  
- **支援**：透過 [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) 的免費支援渠道取得協助。  

---

**最後更新：** 2026-01-08  
**測試環境：** GroupDocs.Redaction 24.9 for Java  
**作者：** GroupDocs