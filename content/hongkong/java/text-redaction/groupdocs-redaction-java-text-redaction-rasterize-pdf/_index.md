---
date: '2026-02-24'
description: 了解如何使用 GroupDocs.Redaction for Java 進行文字遮蔽，並將其儲存為光柵化 PDF，以獲得安全且不可編輯的文件。
keywords:
- text redaction Java
- save as rasterized PDF
- GroupDocs.Redaction Java
title: 如何使用 GroupDocs.Java 進行文字遮蔽並儲存光柵化 PDF
type: docs
url: /zh-hant/java/text-redaction/groupdocs-redaction-java-text-redaction-rasterize-pdf/
weight: 1
---

# 如何使用 GroupDocs.Redaction Java 進行文字遮蔽並儲存光柵化 PDF

保護文件中的敏感資訊至關重要。無論您需要遮蔽個人姓名或製作檔案的安全版本，GroupDocs.Redaction for Java 都能簡化這些工作。快速 **遮蔽文字** 並 **儲存為光柵化 PDF** 是合規應用的常見需求，本指南將逐步說明如何完成。

## 快速解答
- **「遮蔽文字」是什麼意思？** 它會取代或移除敏感字串，使其無法被閱讀或復原。  
- **哪個函式庫負責此工作？** GroupDocs.Redaction for Java 提供內建的遮蔽與光柵化功能。  
- **我需要授權嗎？** 免費試用可用於測試；正式環境需購買永久授權。  
- **能否一步將 DOCX 轉換為光柵化 PDF？** 可以——先執行遮蔽，然後使用啟用光柵化的 `SaveOptions`。  
- **輸出真的無法編輯嗎？** 光柵化的 PDF 以影像形式呈現，防止文字擷取或修改。

## 什麼是文字遮蔽？
文字遮蔽是永久移除或隱蔽文件中敏感資訊（例如個人識別碼、財務資料或機密條款）的過程。與一般的搜尋取代不同，遮蔽可確保被隱藏的內容無法復原。

## 為什麼使用 GroupDocs.Redaction for Java？
- **內建遮蔽類型**（精確字串、正則表達式、影像等）  
- **一鍵光柵化**，即可產生安全的 PDF  
- **跨格式支援**（DOCX、PPTX、XLSX、PDF 等）  
- **開發者友善的 API**，可整合至現有的 Java 專案  

## 前置條件
在開始之前，請確保您已具備以下條件：

1. **Java Development Kit (JDK 11 或更新版本)** 以及 IntelliJ IDEA 或 Eclipse 等 IDE。  
2. **GroupDocs.Redaction 程式庫**（版本 24.9 或更新）。  
3. **基本的 Java 知識**——您將撰寫少量程式碼片段。  

## 設定 GroupDocs.Redaction for Java

### Maven 安裝
將 GroupDocs 儲存庫與相依性加入您的 `pom.xml`：

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
如果您不使用 Maven，也可以從官方發行頁面下載 JAR 檔案：[GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/)。

#### 取得授權
- **免費試用** – 無償探索 API。  
- **臨時授權** – 適合長時間測試。  
- **正式授權** – 生產環境部署必須。  

### 基本初始化
使用 `Redactor` 類別開啟文件：

```java
import com.groupdocs.redaction.Redactor;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

## 實作指南

### 如何在 Java 中遮蔽文字
以下示範精確字串遮蔽，非常適合移除已知的識別資訊，例如個人姓名。

#### 步驟 1：匯入所需類別
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;
```

#### 步驟 2：套用精確字串遮蔽
以下程式碼會將所有 **「John Doe」** 的出現替換為佔位字 **[personal]**：

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
try {
    redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]"));
} finally { 
    redactor.close(); 
}
```

**為什麼這樣有效：**  
- `ExactPhraseRedaction` 針對字面字串 “John Doe”。  
- `ReplacementOptions` 告訴引擎要插入什麼內容以取代原始文字。

**技巧與常見陷阱**  
- 仔細檢查文件路徑；路徑錯誤會拋出 `FileNotFoundException`。  
- 確認 Java 程序對輸出資料夾具有寫入權限。

### 如何儲存為光柵化 PDF
完成遮蔽後，您可能希望得到不可編輯的 PDF。光柵化會將每頁轉換為影像，從而移除選取或編輯文字的可能性。

#### 步驟 1：匯入 `SaveOptions`
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
```

#### 步驟 2：設定並儲存光柵化 PDF
```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
try {
    SaveOptions tmp0 = new SaveOptions();
    tmp0.setAddSuffix(false);
    tmp0.setRasterizeToPDF(true);

    redactor.save(tmp0);
} finally { 
    redactor.close(); 
}
```

**說明：**  
- `setAddSuffix(false)` 保留原始檔名（若需要可啟用以加入 “_redacted”）。  
- `setRasterizeToPDF(true)` 告訴 GroupDocs 將每頁渲染為 PDF 內的影像，確保文件 **不可編輯**。

**故障排除**  
- 若光柵化失敗，請確認 Java 執行環境已包含 PDF 渲染相依性（已隨程式庫捆綁）。  

## 實務應用
1. **法律文件處理** – 在與對方律師共享前遮蔽客戶姓名。  
2. **人力資源紀錄管理** – 在內部報告中隱藏員工編號。  
3. **財務報告** – 在發佈審計摘要時保護帳號。  

您可以將這些步驟串接成自動化工作流程，將 GroupDocs.Redaction 與文件管理系統或雲端儲存桶結合。

## 效能考量
- **批次處理：** 處理大量檔案時重複使用同一個 `Redactor` 實例，以降低開銷。  
- **記憶體管理：** 對於大型文件，在每次 `redactor.close()` 後呼叫 `System.gc()`，或將處理放在獨立的 JVM 中執行。  
- **保持相依性更新：** 新版常包含 PDF 光柵化的效能優化。  

## 常見問題與解決方案

| 問題 | 解決方案 |
|-------|----------|
| *找不到檔案* | 驗證絕對路徑，並確保伺服器上存在該檔案。 |
| *權限被拒* | 以足夠的作業系統權限執行 JVM，或變更輸出資料夾的 ACL。 |
| *光柵化產生空白頁面* | 確認來源文件不是已經是光柵圖像；使用最新版本的程式庫。 |
| *遮蔽後仍留下隱藏文字* | 使用帶有 `ReplacementOptions` 的 `ExactPhraseRedaction`；避免使用簡單的搜尋取代方法。 |

## 常見問答

**Q：什麼是精確字串遮蔽？**  
A：它會將特定字串（例如姓名）替換為佔位字，確保原始文字無法復原。

**Q：光柵化 PDF 如何提升安全性？**  
A：光柵化的 PDF 會將每頁渲染為影像，防止文字選取、複製或編輯。

**Q：能否一次處理多個檔案？**  
A：可以——遍歷檔案路徑清單，對每個文件重複使用相同的 `Redactor` 設定。

**Q：可以整合雲端嗎？**  
A：當然可以。您可以從 AWS S3、Azure Blob 或 Google Cloud Storage 讀寫串流，直接傳遞給 API。

**Q：新手常見的陷阱是什麼？**  
A：忘記關閉 `Redactor`（會鎖定檔案）以及使用缺乏光柵化支援的舊版程式庫。

## 資源

- **文件說明**： [GroupDocs Redaction Java Documentation](https://docs.groupdocs.com/redaction/java/)  
- **API 參考**： [GroupDocs Redaction API Reference](https://reference.groupdocs.com/redaction/java)  
- **下載**： [Latest Releases](https://releases.groupdocs.com/redaction/java/)  
- **GitHub**： [GroupDocs.Redaction GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **免費支援**： [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)  
- **臨時授權**： [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license/) 

---

**最後更新：** 2026-02-24  
**測試環境：** GroupDocs.Redaction 24.9 for Java  
**作者：** GroupDocs