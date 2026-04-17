---
date: '2026-03-20'
description: 了解如何使用 GroupDocs.Redaction for Java 取得檔案類型、獲取文件大小以及檢索 PDF 元資料。立即提升您的
  Java 應用程式的文件處理能力。
keywords:
- get file type java
- get document size java
- retrieve pdf metadata java
- get page count java
- GroupDocs Redaction library setup Java
title: 如何使用 GroupDocs.Redaction 取得 Java 檔案類型
type: docs
url: /zh-hant/java/document-information/retrieve-document-info-using-groupdocs-redaction-java/
weight: 1
---

# 如何在 Java 中使用 GroupDocs.Redaction 取得檔案類型

取得文件的關鍵資訊——例如 **檔案類型**、頁數與大小——是建置以文件為中心的 Java 應用程式時的常見需求。在本教學中，您將學會如何 **取得檔案類型 (Java)**，以及如何 **取得文件大小 (Java)**、**取得頁數 (Java)**，甚至 **取得 PDF 中繼資料 (Java)**，皆透過 GroupDocs.Redaction 函式庫。提前知道檔案類型可讓您決定後續的處理流程，而大小與頁數資訊則有助於有效管理資源。

## 快速回答
- **哪個方法會回傳檔案類型？** `IDocumentInfo.getFileType()`
- **如何取得頁數？** `IDocumentInfo.getPageCount()`
- **哪個呼叫會提供文件大小（位元組）？** `IDocumentInfo.getSize()`
- **執行範例是否需要授權？** 試用或臨時授權即可用於評估。
- **需要哪個版本的 Java？** Java 8 或更高。

## 「get file type java」是什麼？
此詞彙指的是在 Java 中以程式方式從文件中提取檔案格式（例如 DOCX、PDF）。GroupDocs.Redaction 透過 `IDocumentInfo` 介面公開此資訊，只需一行程式碼即可取得。

## 為何使用 GroupDocs.Redaction 進行中繼資料擷取？
- **廣泛的格式支援：** 支援 PDF、DOCX、XLSX、PPTX 等多種檔案。
- **簡易 API：** 單行呼叫即可回傳檔案類型、頁數與大小。
- **效能最佳化：** 僅載入所需的中繼資料，降低記憶體使用。
- **結果一致：** 在所有支援的副檔名上表現相同，亦可用於 **java get file extension** 的情境。

## 前置條件
- 已安裝 Java 8 或更新版本。
- 支援 Maven 的 IDE（IntelliJ IDEA、Eclipse 等）。
- 取得 GroupDocs.Redaction 授權（免費試用或臨時授權）。

## 設定 GroupDocs.Redaction（Java）

若要在 Java 專案中使用 GroupDocs.Redaction 函式庫，請依照以下安裝步驟操作：

**Maven 安裝**

將以下儲存庫與相依性加入 `pom.xml` 檔案：

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

或者，從 [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) 下載最新版本。

### 取得授權
- **免費試用：** 先使用免費試用版評估函式庫。  
- **臨時授權：** 取得臨時授權以延長評估時間。  
- **購買：** 若符合需求，可考慮購買授權。

安裝完成後，初始化並設定 GroupDocs.Redaction：

```java
import com.groupdocs.redaction.Redactor;

// Initialize Redactor with the path to your document
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

## 為何在實務專案中取得檔案類型 (Java) 重要
提前了解文件的類型，可讓您將檔案導向正確的處理流程——例如將 PDF 送入遮蔽工作流、將 Word 檔案送至轉換服務，或將影像送至 OCR 引擎。此舉亦有助於執行安全政策（阻擋可執行檔），以及在文件管理系統中提供正確的 UI 圖示。

## 如何取得檔案類型 (Java)、文件大小 (Java) 與頁數 (Java)

現在函式庫已就緒，讓我們一步步說明如何取得所需資訊。

### 步驟 1：匯入必要的類別

確保在 Java 檔案的最上方匯入所需的類別：

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.domain.IDocumentInfo;
```

### 步驟 2：初始化 Redactor

建立 `Redactor` 實例，並指定文件路徑。此物件可讓您與檔案互動並擷取中繼資料。

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
try {
    // Code for retrieving information will go here.
} finally {
    redactor.close();
}
```

### 步驟 3：取得並顯示文件資訊

呼叫 `getDocumentInfo()` 以取得 `IDocumentInfo` 物件。透過此物件，您可在一次呼叫中 **取得檔案類型 (Java)**、**取得文件大小 (Java)** 與 **取得頁數 (Java)**。

```java
// Retrieve document information
IDocumentInfo info = redactor.getDocumentInfo();

// Output document type, page count, and size in bytes
System.out.println("File Type: " + info.getFileType());
System.out.println("Page Count: " + info.getPageCount());
System.out.println("Size (Bytes): " + info.getSize());
```

這三個 `System.out.println` 陳述式會分別輸出檔案類型、頁數以及位元組大小——正是後續處理所需的資訊。

## 如何取得 PDF 中繼資料 (Java)

若來源文件為 PDF，相同的 `IDocumentInfo` 呼叫會回傳 PDF 專屬的中繼資料（例如 PDF 版本、加密狀態）。無需額外程式碼，只要使用相同的 `getDocumentInfo()` 方法即可。

## 常見使用情境
1. **文件管理系統：** 在儲存前依檔案類型或大小自動分類。  
2. **內容處理管線：** 根據頁數選擇不同的處理策略（例如批次遮蔽大型 PDF 與小型 Word 文件）。  
3. **數位資產庫：** 讓使用者在不開啟檔案的情況下快速預覽文件屬性。

## 常見問題與解決方案
- **找不到檔案：** 請確認傳遞給 `Redactor` 的絕對或相對路徑是否正確。  
- **不支援的格式：** 確認您的文件副檔名受到 GroupDocs.Redaction 支援。  
- **授權錯誤：** 使用有效的試用或永久授權，否則 API 會拋出授權例外。

## 疑難排解技巧（讀取文件中繼資料 Java）
- 將中繼資料呼叫包在 `try‑catch` 區塊中，以優雅地處理損毀的檔案。  
- 使用 `redactor.isEncrypted()`（若支援）於讀取中繼資料前偵測 PDF 是否加密。  
- 處理大量檔案時，重複使用執行緒池，並及時關閉每個 `Redactor` 實例，以避免檔案句柄洩漏。

## 效能考量
處理大批量文件時：

- 在 `try‑with‑resources` 區塊中開啟每個文件，以確保及時釋放檔案句柄。  
- 只快取所需的中繼資料；除非必要，避免載入完整文件內容。

## 結論
現在您已瞭解如何使用 GroupDocs.Redaction **取得檔案類型 (Java)**、**取得文件大小 (Java)**、**取得頁數 (Java)**，以及 **取得 PDF 中繼資料 (Java)**。將這些程式碼片段整合至您的 Java 應用程式，可更智慧地處理文件、提升效能，並提供更豐富的使用者體驗。

## 常見問答

**Q1: 什麼是 GroupDocs.Redaction？**  
A1: 它是一套用於在 Java 應用程式中遮蔽與管理文件資訊的函式庫。

**Q2: 我可以從 PDF 檔案取得中繼資料嗎？**  
A2: 可以，該函式庫支援多種檔案格式，包括 PDF。

**Q3: 取得文件資訊時如何處理例外？**  
A3: 使用 try‑catch 區塊以優雅地管理可能的錯誤。

**Q4: 我可以取得哪些文件資訊？**  
A4: 包括檔案類型、頁數以及位元組大小等細節。

**Q5: 除了 Word 文件外，是否支援其他檔案格式？**  
A5: 有，GroupDocs.Redaction 支援多種檔案類型，包括 PDF、Excel 等。

## 其他常見問答

**Q: API 會在中繼資料中回傳 PDF 版本（例如 1.7）嗎？**  
A: `IDocumentInfo` 物件包含基本的 PDF 特性；若需更詳細的版本資訊，可透過 Redactor API 查詢 PDF 專屬屬性。

**Q: 能否在不將整個文件載入記憶體的情況下取得中繼資料？**  
A: 可以，`getDocumentInfo()` 只讀取取得中繼資料所需的標頭資訊，降低記憶體使用。

**Q: 是否能有效率地批次處理大量文件？**  
A: 為每個文件建立獨立的 `Redactor` 實例，並重複使用執行緒池以平行化工作負載。

**資源**  
- **Documentation:** [GroupDocs Redaction Java Documentation](https://docs.groupdocs.com/redaction/java/)  
- **API Reference:** [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java)  
- **Download:** [GroupDocs.Redaction for Java Downloads](https://releases.groupdocs.com/redaction/java/)  
- **GitHub:** [GroupDocs GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **Free Support:** [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)  
- **Temporary License:** [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license/)  

---

**最後更新：** 2026-03-20  
**測試環境：** GroupDocs.Redaction 24.9 for Java  
**作者：** GroupDocs