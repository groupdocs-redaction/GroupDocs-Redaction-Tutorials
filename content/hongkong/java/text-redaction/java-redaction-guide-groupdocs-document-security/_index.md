---
date: '2026-03-04'
description: 學習如何使用 GroupDocs.Redaction for Java 進行文字遮蔽、以顏色取代文字，並確保 Java 文件的安全性。提供逐步指南與程式碼範例。
keywords:
- Java Document Redaction
- GroupDocs.Redaction for Java
- text redaction in Java
title: 如何使用 GroupDocs.Redaction 在 Java 文件中遮蔽文字
type: docs
url: /zh-hant/java/text-redaction/java-redaction-guide-groupdocs-document-security/
weight: 1
---

# 如何在 Java 文件中使用 GroupDocs.Redaction 進行文字遮蔽

在現代應用程式中，**如何遮蔽文字**（例如 PDF、Word 檔或圖片）是合規與隱私的常見需求。無論是要隱藏個人識別資訊、移除機密註解，或是剔除中繼資料，GroupDocs.Redaction for Java 都提供了乾淨、程式化的方式來實現 **java document security**。本教學將帶您逐步完成所有必要步驟——從設定函式庫到套用精確片語、正規表示式、顏色、註解與中繼資料的遮蔽。

## 快速回答
- **哪個函式庫負責 Java 文件遮蔽？** GroupDocs.Redaction for Java。  
- **可以用顏色取代文字而不是直接刪除嗎？** 可以，使用「replace text with color」功能。  
- **正式環境需要授權嗎？** 需要臨時或付費授權才能完整使用所有功能。  
- **支援哪些 Java 版本？** JDK 8 或以上。  
- **只能用 Maven 加入函式庫嗎？** 建議使用 Maven，也可以手動下載 JAR。

## 什麼是 Java 中的「how to redact text」？
遮蔽（Redaction）是指永久移除或隱蔽文件中敏感內容，使其無法被復原。在 Java 中，通常會載入檔案、定義要隱藏的項目、套用遮蔽，最後儲存已清理的版本。

## 為什麼使用 GroupDocs.Redaction for Java？
- **完整格式支援** – 支援 DOCX、PDF、PPTX、圖片等多種檔案。  
- **細緻控制** – 可依精確片語、正規表示式、顏色、註解或中繼資料進行遮蔽。  
- **效能優化** – 基於串流的處理方式降低大型檔案的記憶體使用。  
- **內建合規** – 協助符合 GDPR、HIPAA 以及其他隱私法規。

## 前置條件
- **已安裝 Java Development Kit (JDK) 8+**。  
- **Maven** 用於相依管理（或自行下載 JAR）。

### 必要函式庫與相依項目
在 `pom.xml` 中加入 GroupDocs 儲存庫與 Redaction 相依項目：

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

您也可以從官方發行頁面下載最新 JAR： [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/)。

### 授權取得
正式環境使用時，請取得臨時或正式授權。亦提供免費試用供評估使用。

## 設定 GroupDocs.Redaction for Java
1. **加入 Maven 相依項目**（或加入 JAR）。  
2. **設定授權**，在應用程式啟動時呼叫 `License.setLicense("path/to/license.lic")`。  
3. **建立 `Redactor` 實例**，指向來源文件。

完成以上步驟，即可開始進行遮蔽。

## 實作指南

### 精確片語遮蔽
將特定片語（例如某人的姓名）替換為佔位文字。

#### 步驟說明
1. **以文件初始化 Redactor**：

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. **定義精確片語規則並套用**：

```java
ExactPhraseRedaction redaction = new ExactPhraseRedaction(
    "John Doe", 
    new ReplacementOptions("[Client]"));

redactor.apply(redaction);
```

3. **將遮蔽後的檔案儲存至輸出資料夾**：

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Redaction applied successfully.");
}
```

### 正規表示式遮蔽並取代文字
使用正規表示式找出序號等模式，並以通用代碼取代。

#### 步驟說明
1. 載入文件：

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. 建立正規表示式規則並套用：

```java
RegexRedaction redaction = new RegexRedaction(
    "Redaction",
    new ReplacementOptions("[Product]"));

redactor.apply(redaction);
```

3. 儲存結果：

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Redaction applied successfully.");
}
```

### 正規表示式遮蔽並以顏色取代
不刪除文字，而是 **replace text with color**，以視覺方式遮蔽，同時保留底層字元。

#### 步驟說明
1. 載入文件：

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. 定義正規表示式模式並設定取代顏色（例如藍色）：

```java
RegexRedaction redaction = new RegexRedaction(
    "\d{2}\s*\d{2}[^\\d]*\d{6}", 
    new ReplacementOptions(Color.BLUE));

redactor.apply(redaction);
```

3. 儲存更新後的檔案：

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Redaction applied successfully.");
}
```

### 刪除註解遮蔽
移除文件中所有註解（評論、標記等），讓最終版本更乾淨。

#### 步驟說明
1. 載入檔案：

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. 套用註解刪除規則：

```java
DeleteAnnotationRedaction redaction = new DeleteAnnotationRedaction();

redactor.apply(redaction);
```

3. 持久化變更：

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Annotations deleted successfully.");
}
```

### 擦除中繼資料遮蔽
移除所有中繼資料（作者、建立日期、自訂屬性），以保護隱私並符合合規標準。

#### 步驟說明
1. 開啟文件：

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. 套用中繼資料擦除規則：

```java
EraseMetadataRedaction redaction = new EraseMetadataRedaction(MetadataFilters.All);

redactor.apply(redaction);
```

3. 儲存已清理的文件：

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Metadata erased successfully.");
}
```

## 實務應用（為何重要）
- **法律文件製作** – 在分享草稿前遮蔽客戶姓名。  
- **醫療合規** – 移除病患識別資訊，以符合 HIPAA。  
- **企業資料保護** – 隱藏財務數字或商業機密於內部報告。  

將這些遮蔽步驟整合到現有工作流程，可自動化隱私保護，降低意外資料外洩風險。

## 效能考量
- **使用串流而非一次載入** – 大檔案建議使用接受 `InputStream` 的 `Redactor` 建構子，以免一次將整個文件載入記憶體。  
- **預先編譯正規表示式**，在重複執行相同遮蔽時可減少 CPU 開銷。  
- **監控 JVM 堆積** – 遮蔽可能消耗大量記憶體，批次處理時可考慮調整堆積大小。

## 常見問題與除錯
| 症狀 | 可能原因 | 解決方式 |
|------|----------|----------|
| `apply` 後沒有變更 | 文件路徑錯誤或檔案被鎖定 | 確認檔案路徑，並確保文件未被其他程式開啟 |
| 正規表示式未匹配 | 模式語法錯誤 | 使用線上測試工具測試正規表示式，並正確轉義反斜線 |
| 顏色取代未顯示 | 輸出格式不支援文字顏色（如純文字） | 改用支援樣式的格式，如 DOCX 或 PDF |
| 執行時授權錯誤 | 授權檔遺失或無效 | 將 `.lic` 檔放在可存取的目錄，並於任何 Redactor 使用前呼叫 `License.setLicense` |

## 常見問答

**Q: 可以在一次執行中結合多個遮蔽規則嗎？**  
A: 可以。建立每個遮蔽物件，分別呼叫 `redactor.apply()`，最後一次儲存即可。

**Q: GroupDocs.Redaction 支援受密碼保護的檔案嗎？**  
A: 完全支援。將密碼傳入接受 `LoadOptions` 物件的 `Redactor` 建構子。

**Q: 能在儲存前預覽遮蔽效果嗎？**  
A: 可以呼叫 `redactor.preview()`，產生暫時的視圖，顯示即將被遮蔽的區域。

**Q: 支援哪些檔案格式？**  
A: DOCX、PDF、PPTX、XLSX、圖片（PNG、JPEG、BMP）等多種格式。

**Q: 如何確保遮蔽後的文件符合 GDPR？**  
A: 使用中繼資料擦除功能、移除註解，並對所有個人資料欄位套用精確片語或正規表示式遮蔽。

## 結論
您現在已掌握使用 GroupDocs.Redaction 於 Java 文件中 **how to redact text** 的完整端對端指南。透過精確片語、正規表示式、顏色、註解與中繼資料等多種遮蔽方式，您可以實現強大的 **java document security**，同時保持程式碼簡潔易維護。將這些範例整合至現有服務、實現批次自動化，並持續符合隱私法規的要求。

---

**最後更新：** 2026-03-04  
**測試環境：** GroupDocs.Redaction 24.9 for Java  
**作者：** GroupDocs