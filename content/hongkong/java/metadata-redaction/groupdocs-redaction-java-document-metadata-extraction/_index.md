---
date: '2026-01-06'
description: 了解如何使用 GroupDocs.Redaction for Java 取得檔案類型、讀取文件屬性以及取得頁數。提供帶程式碼的逐步指南。
keywords:
- GroupDocs.Redaction Java
- document metadata extraction
- Java stream APIs
title: 使用 GroupDocs.Redaction 取得 Java 檔案類型 – 中繼資料擷取
type: docs
url: /zh-hant/java/metadata-redaction/groupdocs-redaction-java-document-metadata-extraction/
weight: 1
---

# 取得檔案類型（Java）並使用 GroupDocs.Redaction 在 Java 中擷取文件中繼資料

在現代的 Java 應用程式中，能夠快速 **取得檔案類型（Java）**，並擷取其他有用的文件屬性，例如頁數、大小以及自訂中繼資料，對於構建穩健的文件管理或資料分析流程至關重要。本教學將完整說明如何使用 GroupDocs.Redaction 讀取文件屬性、為何它是此任務的首選函式庫，以及如何將解決方案乾淨地整合到您的程式碼基礎中。

## 快速解答
- **如何在 Java 中取得文件的檔案類型？** 使用 `redactor.getDocumentInfo().getFileType()`。
- **哪個函式庫同時處理中繼資料擷取與遮蔽？** GroupDocs.Redaction for Java。
- **開發時需要授權嗎？** 免費試用可用於評估；正式環境需購買永久授權。
- **我也可以取得頁數嗎？** 可以，呼叫 `IDocumentInfo` 物件的 `getPageCount()`。
- **此方法相容於 Java 8+ 嗎？** 完全相容——GroupDocs.Redaction 支援 Java 8 及更新版本。

## 什麼是「取得檔案類型（Java）」以及為何它很重要？
當您對文件呼叫 `getFileType()` 時，函式庫會檢查檔案標頭並回傳友好的列舉值（例如 **DOCX**、**PDF**、**XLSX**）。了解確切的類型可讓您將檔案導向正確的處理流程、執行安全政策，或僅僅向最終使用者顯示正確的資訊。

## 為何使用 GroupDocs.Redaction 讀取 Java 文件屬性？
- **全方位解決方案：** 遮蔽、 中繼資料擷取 與 格式轉換 均在同一 API 下完成。  
- **串流友好：** 直接支援 `InputStream`，可從磁碟、網路或雲端儲存處理檔案，無需暫存檔。  
- **效能優化：** 記憶體佔用極小，關閉 `Redactor` 實例時會自動釋放資源。

## 前置條件
1. **GroupDocs.Redaction for Java**（版本 24.9 或更新）。  
2. JDK 8 或更新版本。  
3. 基本的 Java 知識與檔案 I/O 串流的使用經驗。

## 設定 GroupDocs.Redaction for Java

### Maven 安裝
將以下儲存庫與相依性加入 `pom.xml`：

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
- **Free Trial：** 適合評估 API。  
- **Temporary License：** 官方網站提供短期測試授權。  
- **Full License：** 準備投入正式環境時購買。

## 基本初始化（Java）

```java
import com.groupdocs.redaction.Redactor;
import java.io.FileInputStream;

FileInputStream stream = new FileInputStream("path/to/your/Sample.docx");
final Redactor redactor = new Redactor(stream);
// Proceed with document operations...
```

## 如何使用 GroupDocs.Redaction 取得檔案類型（Java）

### 步驟 1：開啟檔案串流
先為目標文件建立 `InputStream`：

```java
FileInputStream stream = new FileInputStream("YOUR_DOCUMENT_DIRECTORY/Sample.docx");
```

### 步驟 2：初始化 Redactor
使用該串流建立 `Redactor` 實例。此物件可讓您存取文件的中繼資料。

```java
final Redactor redactor = new Redactor(stream);
```

### 步驟 3：取得文件資訊
呼叫 `getDocumentInfo()` 取得 `IDocumentInfo` 物件。這裡您可以 **取得檔案類型（Java）**、讀取其他屬性，甚至 **取得頁數（Java）**。

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

> **專業提示：** 只有在需要在主控台輸出時才取消註解 `System.out.println` 行；在正式環境中保持註解可減少 I/O 開銷。

### 步驟 4：關閉資源
務必在 `finally` 區塊（如範例所示）中關閉 `Redactor` 與串流，以避免記憶體洩漏，特別是在平行處理大量文件時。

## 實務應用（Java 讀取文件屬性）
1. **Document Management Systems：** 依類型、頁數與大小自動目錄化檔案。  
2. **Data‑Analytics Pipelines：** 將中繼資料輸入儀表板以供報表分析。  
3. **Content‑Creation Platforms：** 在下載或預覽前向最終使用者顯示檔案詳細資訊。

## 效能考量
- 使用 **緩衝串流**（`BufferedInputStream`）處理大型檔案，以提升 I/O 效率。  
- 立即釋放資源（同時 `close()` `Redactor` 與串流）。  
- 批次處理時，可考慮每個執行緒重複使用同一個 `Redactor` 實例，以減少物件建立開銷。

## 常見問題與解決方案

| 症狀 | 可能原因 | 解決方法 |
|---------|--------------|-----|
| `FileNotFoundException` | 路徑不正確或檔案遺失 | 確認絕對/相對路徑以及檔案權限。 |
| `LicenseException` | 未載入有效授權 | 在建立 `Redactor` 前載入試用或正式授權。 |
| `OutOfMemoryError` on large PDFs | 未使用緩衝串流或同時處理過多檔案 | 改用 `BufferedInputStream`，並限制同時執行的執行緒數量。 |

## 常見問答

**Q: GroupDocs.Redaction 的主要用途是什麼？**  
A: 主要用於遮蔽敏感內容，同時也提供強大的 API 讓您 **在 Java 中讀取文件屬性**，例如檔案類型與頁數。

**Q: 我可以將 GroupDocs.Redaction 與其他 Java 框架一起使用嗎？**  
A: 可以，函式庫可無縫整合於 Spring、Jakarta EE，甚至純 Java SE 專案。

**Q: 如何有效處理極大型文件？**  
A: 將檔案串流包裝成 `BufferedInputStream`，及時關閉資源，並考慮以串流方式處理，而非一次載入整個文件至記憶體。

**Q: 函式庫支援非英文文件嗎？**  
A: 完全支援——GroupDocs.Redaction 內建多語言與字元集的處理能力。

**Q: 擷取中繼資料時常見的陷阱是什麼？**  
A: 常見問題包括缺少授權、檔案路徑錯誤、忘記關閉串流。請務必遵循上方示範的資源清理模式。

## 結論
您現在已掌握使用 GroupDocs.Redaction **取得檔案類型（Java）**、讀取其他文件屬性，以及 **取得頁數（Java）** 的完整、可投入生產的作法。將這些程式碼片段整合至現有服務，即可即時掌握系統中每一份文件的資訊。

**下一步**  
- 嘗試 `IDocumentInfo` 所提供的其他中繼資料欄位。  
- 結合中繼資料擷取與遮蔽工作流程，實現端對端的文件安全。  
- 探索高吞吐量環境的批次處理模式。

---  
**Last Updated:** 2026-01-06  
**Tested With:** GroupDocs.Redaction 24.9 for Java  
**Author:** GroupDocs  

**Resources**  
- [Documentation](https://docs.groupdocs.com/redaction/java/)  
- [API Reference](https://reference.groupdocs.com/redaction/java)  
- [Download GroupDocs.Redaction for Java](https://releases.groupdocs.com/redaction/java/)  
- [GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- [Free Support Forum](https://forum.groupdocs.com/c/redaction/33)  
- [Temporary License Information](https://purchase.groupdocs.com/temporary-license/)