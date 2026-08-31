---
date: '2026-03-22'
description: 學習如何在 Java 中使用 GroupDocs.Redaction 讀取檔案元資料、取得檔案類型以及獲取頁數。一步一步的指引，附有程式碼範例。
keywords:
- GroupDocs.Redaction Java
- document metadata extraction
- Java stream APIs
title: Java 讀取檔案元資料 – 使用 GroupDocs.Redaction 的檔案類型
type: docs
url: /zh-hant/java/metadata-redaction/groupdocs-redaction-java-document-metadata-extraction/
weight: 1
---

# java 讀取檔案中繼資料 – 使用 GroupDocs.Redaction 取得檔案類型 (Java)

在現代的 Java 應用程式中，快速 **java read file metadata**——尤其是檔案類型、頁數、大小以及任何自訂屬性——對於建立可靠的文件管理或資料分析流程至關重要。本教學將帶領您使用 GroupDocs.Redaction 讀取這些屬性，說明 **how to get file type java**，並展示如何 **java get page count** 以及 **read file size java**，以乾淨且支援串流的方式。

## 快速解答
- **如何在 Java 中取得文件的檔案類型？** 使用 `redactor.getDocumentInfo().getFileType()`。  
- **哪個函式庫同時處理中繼資料擷取與遮蔽？** GroupDocs.Redaction for Java。  
- **開發時需要授權嗎？** 免費試用版可用於評估；正式環境需購買永久授權。  
- **我也可以取得頁數嗎？** 可以，對 `IDocumentInfo` 物件呼叫 `getPageCount()`。  
- **此方法是否相容於 Java 8 以上？** 完全相容——GroupDocs.Redaction 支援 Java 8 及更新版本。

## 使用 GroupDocs.Redaction 讀取檔案中繼資料 (java read file metadata)

了解 **java read file metadata** 的步驟，可協助您決定在應用程式中的哪個位置放置此邏輯——無論是驗證上傳的微服務，或是索引大型文件集合的批次工作。

### 什麼是 “get file type java” 以及為何重要？
當您對文件呼叫 `getFileType()` 時，函式庫會檢查檔案標頭並回傳友好的列舉值（例如 **DOCX**、**PDF**、**XLSX**）。了解確切的類型可讓您將檔案導向正確的處理流程、執行安全政策，或僅僅向最終使用者顯示正確資訊。

### 為何使用 GroupDocs.Redaction 讀取文件屬性 (java read document properties)？
- **一站式解決方案：** 遮蔽、metadata 擷取與格式轉換皆在同一個 API 中。  
- **支援串流：** 直接使用 `InputStream`，因此可從磁碟、網路或雲端儲存處理檔案，無需暫存檔。  
- **效能優化：** 記憶體佔用最小，關閉 `Redactor` 實例時會自動清理資源。

## 前置條件
1. **GroupDocs.Redaction for Java**（版本 24.9 或更新）。  
2. JDK 8 或更新版本。  
3. 基本的 Java 知識與檔案 I/O 串流的使用經驗。  

## 設定 GroupDocs.Redaction for Java

### Maven 安裝
將以下儲存庫與相依性加入您的 `pom.xml`：

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
或者，直接從 [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) 下載最新版本。

### 取得授權
- **免費試用：** 適合評估 API。  
- **臨時授權：** 官方網站提供，適用於短期測試。  
- **正式授權：** 準備投入生產時購買。

## 基本初始化 (Java)

```java
import com.groupdocs.redaction.Redactor;
import java.io.FileInputStream;

FileInputStream stream = new FileInputStream("path/to/your/Sample.docx");
final Redactor redactor = new Redactor(stream);
// Proceed with document operations...
```

## 逐步指南：取得中繼資料

### 步驟 1：開啟檔案串流
首先為目標文件建立 `InputStream`：

```java
FileInputStream stream = new FileInputStream("YOUR_DOCUMENT_DIRECTORY/Sample.docx");
```

### 步驟 2：初始化 Redactor
使用該串流建立 `Redactor` 實例。此物件可讓您存取文件的中繼資料。

```java
final Redactor redactor = new Redactor(stream);
```

### 步驟 3：取得文件資訊
呼叫 `getDocumentInfo()` 以取得 `IDocumentInfo` 物件。在此您可以 **java read file metadata**、**java get document type**、**java get page count**，甚至 **read file size java**。

```java
try {
    IDocumentInfo info = redactor.getDocumentInfo();
    
    // Display document information (uncomment as needed)
    System.out.println("\
File type: " + info.getFileType() +
           "\
Number of pages: " + info.getPageCount() + 
           "\
Document size: " + info.getSize() + " bytes");
} finally {
    redactor.close();
    stream.close();
}
```

> **小技巧：** 僅在需要在主控台輸出時才取消註解 `System.out.println` 行；在正式環境保持註解可減少 I/O 開銷。

### 步驟 4：關閉資源
務必在 `finally` 區塊（如範例所示）中關閉 `Redactor` 與串流，以避免記憶體洩漏，特別是在平行處理大量文件時。

## 實務應用 (java read document properties)

1. **文件管理系統：** 依類型、頁數與大小自動分類檔案。  
2. **資料分析管線：** 將中繼資料輸入儀表板以供報表使用。  
3. **內容創作平台：** 在下載或預覽前向最終使用者顯示檔案細節。  

## 效能考量
- 使用 **緩衝串流** (`BufferedInputStream`) 處理大型檔案，以提升 I/O 效能。  
- 及時釋放資源（對 `Redactor` 與串流皆呼叫 `close()`）。  
- 批次處理時，考慮在每個執行緒中重複使用單一 `Redactor` 實例，以減少物件建立開銷。  

## 常見問題與解決方案

| 症狀 | 可能原因 | 解決方案 |
|---------|--------------|-----|
| `FileNotFoundException` | 路徑不正確或檔案遺失 | 確認絕對/相對路徑及檔案權限。 |
| `LicenseException` | 未載入有效授權 | 在建立 `Redactor` 前載入試用或正式授權。 |
| `OutOfMemoryError` on large PDFs | 未使用緩衝串流或同時處理過多檔案 | 改用 `BufferedInputStream` 並限制同時執行的執行緒數量。 |

## 常見問答

**Q: GroupDocs.Redaction 的用途是什麼？**  
A: 主要用於遮蔽敏感內容，同時也提供強大的 API 以 **java read document properties**（如檔案類型與頁數）取得文件屬性。

**Q: 我可以將 GroupDocs.Redaction 與其他 Java 框架一起使用嗎？**  
A: 可以，該函式庫可無縫整合於 Spring、Jakarta EE，甚至純 Java SE 專案。

**Q: 如何有效處理非常大的文件？**  
A: 將檔案串流包裝在 `BufferedInputStream`，及時關閉資源，並考慮以串流方式處理文件，而非一次載入整個文件至記憶體。

**Q: 此函式庫是否支援非英語文件？**  
A: 當然支援——GroupDocs.Redaction 內建支援多種語言與字元集。

**Q: 取得中繼資料時常見的陷阱是什麼？**  
A: 缺少授權、檔案路徑錯誤，以及忘記關閉串流是最常見的問題。請務必遵循上方示範的資源清理模式。

## 結論
您現在已擁有完整且可投入生產環境的 **java read file metadata**、讀取其他文件屬性以及 **java get page count** 的解決方案，皆透過 GroupDocs.Redaction 實作。將這些程式碼片段整合至現有服務，即可即時掌握系統中每份文件的資訊。

**下一步**  
- 嘗試 `IDocumentInfo` 所提供的其他中繼資料欄位。  
- 將中繼資料擷取與遮蔽工作流程結合，實現端到端的文件安全。  
- 探索高流量環境的批次處理模式。  

**資源**  
- [文件說明](https://docs.groupdocs.com/redaction/java/)  
- [API 參考文件](https://reference.groupdocs.com/redaction/java)  
- [下載 GroupDocs.Redaction for Java](https://releases.groupdocs.com/redaction/java/)  
- [GitHub 程式庫](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- [免費支援論壇](https://forum.groupdocs.com/c/redaction/33)  
- [臨時授權資訊](https://purchase.groupdocs.com/temporary-license/)  

---

**最後更新：** 2026-03-22  
**測試環境：** GroupDocs.Redaction 24.9 for Java  
**作者：** GroupDocs