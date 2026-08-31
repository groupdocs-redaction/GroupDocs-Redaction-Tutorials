---
date: '2026-03-22'
description: 學習如何在 Java 中使用 GroupDocs 執行元資料遮蔽，透過 GroupDocs.Redaction 安全地移除機密文件的元資料。
keywords:
- metadata redaction Java
- GroupDocs Redaction tutorial
- secure document metadata
title: 如何在 Java 中使用 GroupDocs 執行元資料遮蔽
type: docs
url: /zh-hant/java/metadata-redaction/java-metadata-redaction-groupdocs-tutorial/
weight: 1
---

# 如何在 Java 中使用 GroupDocs 執行中繼資料遮蔽

在本完整指南中，您將了解 **如何在 Java 中使用 GroupDocs 進行中繼資料遮蔽**，以從 Word、PDF 及其他文件格式中剝除機密中繼資料（例如公司名稱），使用 GroupDocs.Redaction for Java。完成本教學後，您即可將中繼資料遮蔽整合至任何基於 Java 的工作流程，確保敏感資訊安全。

## 快速解答
- **MetadataSearchRedaction 的功能是什麼？** 它會搜尋特定的中繼資料欄位，並以自訂文字取代其值。  
- **需要哪個程式庫？** GroupDocs.Redaction for Java（v24.9 或更新版本）。  
- **需要授權嗎？** 免費試用可用於評估；正式環境需購買完整授權。  
- **可以保留原始檔案格式嗎？** 可以——使用 `SaveOptions` 即可保留原始格式。  
- **此方法是執行緒安全的嗎？** 每個 `Redactor` 實例互相獨立，您可以平行處理文件。

## 什麼是使用 GroupDocs 的中繼資料遮蔽？
`MetadataSearchRedaction` 是一個專門的類別，可讓您針對特定的中繼資料屬性（例如 *Company*、*Author*）進行搜尋，並以佔位文字取代其內容。當您需要在與外部合作夥伴共享文件前匿名化公司資料時，這個功能相當理想。

## 為什麼要使用 GroupDocs 的中繼資料遮蔽？
- **精準** – 只遮蔽您指定的欄位，文件其餘部分保持不變。  
- **合規** – 透過移除隱藏識別碼，協助符合 GDPR、HIPAA 及其他隱私法規。  
- **自動化就緒** – 可無縫嵌入批次處理管線或微服務。

## 前置條件
- **GroupDocs.Redaction for Java** ≥ 24.9。  
- 已在機器上安裝 Java 8 或更新版本。  
- 建議使用 IntelliJ IDEA 或 Eclipse 等 IDE（非必須）。  
- 具備基本的 Maven 使用經驗（或能手動加入 JAR）。

## 設定 GroupDocs.Redaction for Java
將儲存庫與相依性加入 `pom.xml`。此步驟可讓 Maven 自動下載程式庫。

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

*或者，您也可以直接從官方發行頁面下載 JAR：*  
[GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/)

### 取得授權
- **免費試用** – 下載試用授權以探索全部功能。  
- **臨時授權** – 用於延長測試。  
- **正式授權** – 生產環境必須使用。

## 基本初始化
建立指向欲處理文件的 `Redactor` 實例。

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

## 實作指南

### 步驟 1：匯入必要類別
這些匯入讓您可以使用遮蔽引擎、儲存選項與中繼資料工具。

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.redactions.MetadataFilters;
import com.groupdocs.redaction.redactions.MetadataSearchRedaction;
```

### 步驟 2：初始化 Redactor
以來源檔案路徑建立 `Redactor`。

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

### 步驟 3：設定中繼資料搜尋與遮蔽
建立 `MetadataSearchRedaction`，搜尋精確字串 **"Company Ltd."**，並以 **"--company--"** 取代。`setFilter` 呼叫將操作限制於 *Company* 中繼資料欄位。

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
設定 `SaveOptions`，讓遮蔽後的檔案在原檔名後加上 “_Redacted” 後綴，同時保留原始格式。

```java
SaveOptions tmp0 = new SaveOptions();
tmp0.setAddSuffix(true);  // Adds "_Redacted" to file name
tmp0.setRasterizeToPDF(false);  // Keeps original format

redactor.save(tmp0);
```

### 步驟 6：釋放資源
務必關閉 `Redactor`，以釋放原生資源並避免記憶體洩漏。

```java
finally {
    redactor.close();
}
```

## 常見問題與解決方案
- **FileNotFoundException** – 再次確認傳給 `Redactor` 的路徑，建議使用絕對路徑或 `Paths.get(...)` 提高可靠性。  
- **未看到變更** – 確認您目標的中繼資料欄位確實包含搜尋字串；預設情況下中繼資料是區分大小寫的。  
- **大型檔案記憶體不足** – 將文件分批處理，並在每個檔案處理完畢後立即呼叫 `redactor.close()`。

## 實務應用
1. **法律文件** – 在將合約寄給第三方前移除客戶公司名稱。  
2. **財務報告** – 匿名化審計檔案中的內部識別碼。  
3. **協作專案** – 與外部供應商共享草稿時保護專有資訊。

## 效能考量
- **記憶體管理** – 程式庫會將整個文件載入記憶體；每處理完一個檔案後務必關閉 `Redactor`。  
- **批次處理** – 大量情境下，可遍歷檔案集合並重複使用單一 `SaveOptions` 實例。  
- **保持更新** – 新版會帶來效能調整與錯誤修正，請始終以最新穩定版為目標。

## 結論
您現在已掌握 **如何在 Java 中使用 GroupDocs 進行中繼資料遮蔽**，可安全地從文件中剝除公司中繼資料。將這些步驟納入文件處理管線，即可確保合規並保護敏感資訊。

**後續建議**
- 嘗試其他中繼資料欄位，如 *Author* 或 *Creator*。  
- 結合文字或影像遮蔽，打造全方位的遮蔽解決方案。

## FAQ 區段
1. **什麼是 GroupDocs.Redaction for Java？**  
   - 這是一套功能強大的程式庫，讓您能在 Java 應用程式中遮蔽文件的文字、 中繼資料與影像。  
2. **可以在不購買授權的情況下使用 GroupDocs.Redaction 嗎？**  
   - 可以，但會有功能限制。免費試用或臨時授權可供測試使用。  
3. **如何確保在遮蔽過程中保留文件格式？**  
   - 使用 `SaveOptions` 指定需求，例如避免將 PDF 轉為光柵化。  
4. **哪些類型的文件可以使用 GroupDocs.Redaction 進行遮蔽？**  
   - 支援多種格式，包括 Word、Excel、PowerPoint、PDF 等。  
5. **遇到問題時該向哪裡尋求支援？**  
   - 前往 [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) 取得協助。

## 常見問答
**Q: MetadataSearchRedaction 能處理加密文件嗎？**  
A: 能。使用接受密碼參數的 `Redactor` 建構子，載入文件時提供相應密碼。

**Q: 可以在一次執行中串接多個中繼資料遮蔽嗎？**  
A: 完全可以。建立多個 `MetadataSearchRedaction` 物件，設定不同的過濾條件，然後依序套用再儲存。

**Q: 能在儲存前預覽遮蔽結果嗎？**  
A: 您可以呼叫 `redactor.getRedactions()` 取得待執行的遮蔽清單，並以程式方式檢查。

## 資源
- **文件說明**：在 [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/) 查看詳細指南。  
- **API 參考**：前往 [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java) 查閱完整 API。  
- **下載程式庫**：從 [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/) 取得最新發行版。  
- **原始碼**：在 [GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java) 瀏覽與貢獻。  
- **支援**：透過免費支援頻道 [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) 取得協助。

---

**最後更新：** 2026-03-22  
**測試環境：** GroupDocs.Redaction 24.9 for Java  
**作者：** GroupDocs  

---