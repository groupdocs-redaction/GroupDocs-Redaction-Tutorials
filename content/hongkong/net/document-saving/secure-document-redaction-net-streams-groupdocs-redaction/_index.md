---
date: '2026-07-06'
description: 了解如何使用 GroupDocs.Redaction 透過 streams 進行 .net 文件遮蔽。本教學涵蓋設定、從串流載入文件、套用遮蔽以及安全儲存。
keywords:
- redact documents .net
- load document from stream
- GroupDocs.Redaction streams
schemas:
- author: GroupDocs
  dateModified: '2026-07-06'
  description: Learn how to redact documents .net using streams with GroupDocs.Redaction.
    This tutorial covers setup, load document from stream, applying redactions, and
    saving securely.
  headline: Redact documents .net using Streams – GroupDocs.Redaction Guide
  type: TechArticle
- description: Learn how to redact documents .net using streams with GroupDocs.Redaction.
    This tutorial covers setup, load document from stream, applying redactions, and
    saving securely.
  name: Redact documents .net using Streams – GroupDocs.Redaction Guide
  steps:
  - name: '**Free Trial** – download a trial from [GroupDocs](https://purchase.groupdocs.com/temporary-license/).'
    text: '**Free Trial** – download a trial from [GroupDocs](https://purchase.groupdocs.com/temporary-license/).'
  - name: '**Temporary License** – request a short‑term key for evaluation.'
    text: '**Temporary License** – request a short‑term key for evaluation.'
  - name: '**Full Purchase** – obtain a permanent license for production workloads.'
    text: '**Full Purchase** – obtain a permanent license for production workloads.'
  - name: '**Dispose streams promptly** – `using` statements automatically close streams,
      freeing memory.'
    text: '**Dispose streams promptly** – `using` statements automatically close streams,
      freeing memory.'
  - name: '**Batch processing** – Loop through a collection of files and reuse a single
      `Redactor` instance when format permits, reducing allocation overhead.'
    text: '**Batch processing** – Loop through a collection of files and reuse a single
      `Redactor` instance when format permits, reducing allocation overhead.'
  - name: '**File access denied** – Verify the application’s account has read/write
      permissions on the target folders.'
    text: '**File access denied** – Verify the application’s account has read/write
      permissions on the target folders.'
  - name: '**Redaction not applied** – Ensure the redaction type you chose is compatible
      with the document format (e.g., `DeleteAnnotationRedaction` works for PDF and
      DOCX).'
    text: '**Redaction not applied** – Ensure the redaction type you chose is compatible
      with the document format (e.g., `DeleteAnnotationRedaction` works for PDF and
      DOCX).'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction supports over 70 formats—including PDF, DOCX, XLSX,
      PPTX, and HTML—when using stream‑based APIs.
    question: Which file formats can be processed with streams?
  - answer: Yes, call `redactor.GetRedactedDocument()` to obtain an in‑memory representation
      that you can render or inspect programmatically.
    question: Can I preview redactions before saving?
  - answer: Supply the password when opening the stream via `Redactor` overloads that
      accept `LoadOptions` containing the password.
    question: How does the library handle password‑protected files?
  - answer: The engine can process files up to 2 GB; larger files should be split
      or processed in chunks to stay within memory limits.
    question: Is there a limit on document size?
  - answer: A single license key can be used across multiple environments as long
      as the usage complies with the licensing agreement.
    question: Do I need a separate license for each deployment environment?
  type: FAQPage
title: 使用 Streams 進行 .net 文件遮蔽 – GroupDocs.Redaction 指南
type: docs
url: /zh-hant/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/
weight: 1
---

# 使用串流的 Redact documents .net – 完整指南

Welcome! In this tutorial you’ll discover how to **redact documents .net** securely by leveraging streams with GroupDocs.Redaction. We’ll walk through everything you need—from installing the library, loading a document from stream, applying precise redactions, to saving the result without leaving temporary files on disk.

## 快速解答
- **哪個函式庫負責 .NET 中的文件編輯？** GroupDocs.Redaction for .NET.  
- **我可以直接從串流載入檔案嗎？** Yes—use `FileStream` with the Redactor constructor.  
- **支援哪些格式？** Over 70 input and output formats, including PDF, DOCX, XLSX, PPTX.  
- **生產環境需要授權嗎？** A valid GroupDocs.Redaction license is required for non‑trial use.  
- **大型檔案使用安全嗎？** Stream‑based processing avoids loading the whole file into memory, enabling handling of multi‑gigabyte documents.

## 什麼是 “redact documents .net”？
**“Redact documents .net”** 指的是使用 .NET 函式庫（如 GroupDocs.Redaction）永久移除或遮蔽檔案中敏感內容的過程。這確保機密資料不會以明文形式離開您的系統。此功能常用於法律、金融與醫療保健領域，以符合 GDPR、HIPAA 等隱私法規，確保敏感資料在處理後無法復原。

## 為什麼使用串流進行編輯？
GroupDocs.Redaction 支援 **70+ 檔案格式**，且可處理最高達 **2 GB** 的檔案，而無需完整載入記憶體。串流可減少 I/O 開銷、提升效能，並符合安全最佳實踐，因為資料僅在記憶體中保留短暫的轉換時間。

## 前置條件

- **GroupDocs.Redaction for .NET** – 透過 NuGet 安裝（見下文）。  
- **.NET 6+**（或 .NET Framework 4.6.1+）。  
- Visual Studio 2022 或任何相容的 IDE。  
- 具備基本的 C# 知識以及對 .NET 串流的熟悉度。

## 安裝 GroupDocs.Redaction

您可以使用以下任一指令加入套件：

**.NET CLI**  
```shell
dotnet add package GroupDocs.Redaction
```  

**Package Manager Console**  
```shell
Install-Package GroupDocs.Redaction
```  

或在 NuGet 套件管理員 UI 中找到 “GroupDocs.Redaction”，然後點擊 **Install**。

### 取得授權步驟
1. **免費試用** – 從 [GroupDocs](https://purchase.groupdocs.com/temporary-license/) 下載試用版。  
2. **臨時授權** – 申請短期金鑰以供評估。  
3. **完整購買** – 取得永久授權以用於正式環境。

安裝完成後，於程式碼中初始化函式庫：

```csharp
using GroupDocs.Redaction;
// Initialization code here...
```  

## 如何從串流載入文件？

`FileStream` 提供讀寫磁碟檔案的串流。`Redactor` 類別處理文件並套用編輯規則。將來源檔案載入 `FileStream`，再將串流傳遞給 `Redactor` 建構子。此方式避免將原始檔案寫入暫存位置，且僅在處理期間將資料保留於記憶體中。此方法適用於所有支援的格式，包括 PDF 與 Office 文件。

```csharp
// Directly open the source file as a read‑only stream
using var inputStream = new FileStream(inputPath, FileMode.Open, FileAccess.Read);
```

## 如何使用串流初始化 Redactor？

`Redactor` 類別是操作文件內容的核心引擎。提供輸入串流後，即可在記憶體中進行編輯，無需中間檔案。建立實例後，您可以串接編輯規則、預覽變更，並在提交最終文件前設定光柵化或加密等選項。

```csharp
// Initialise the Redactor with the input stream
using var redactor = new GroupDocs.Redaction.Redactor(inputStream);
```

**Definition anchor:** `GroupDocs.Redaction.Redactor` 是主要的類別，提供在從串流載入的文件上套用、預覽與提交編輯操作的方法。

## 如何套用編輯？

您可以新增多個編輯動作；以下範例會刪除所有註解，這是移除隱藏評論或審閱者備註的常見需求。可結合 `DeleteTextRedaction` 或 `ReplaceTextRedaction` 等其他編輯類型，以移除或遮蔽文件中特定字串、日期或模式。

```csharp
// Apply a predefined redaction that removes every annotation
redactor.Apply(new DeleteAnnotationRedaction());
```

**Definition anchor:** `DeleteAnnotationRedaction` 是內建的編輯規則，會永久刪除文件中的註解物件（如評論、標記與印章）。

## 如何儲存已編輯的文件？

直接儲存至 `FileStream` 可確保輸出一次寫入完成，避免產生不必要的暫存檔。您亦可透過 `SaveOptions` 物件指定輸出格式、壓縮等級與可選的密碼保護，以符合安全需求。最後，關閉輸出串流以釋放檔案句柄，確保檔案完整寫入磁碟。

```csharp
// Prepare the output stream for the redacted file
using var outputStream = new FileStream(outputPath, FileMode.Create, FileAccess.Write);

// Save the modified document; RasterizationOptions disabled to keep text editable
redactor.Save(outputStream, new SaveOptions { RasterizationOptions = null });
```

**Definition anchor:** `SaveOptions` 讓您控制文件的持久化方式，包括光柵化、加密與格式選擇。

## 常見使用情境
- **法律文件處理：** 在與客戶分享草稿前移除機密註解。  
- **GDPR 合規：** 從合約或員工紀錄中移除個人識別資訊。  
- **內部稽核報告：** 隱藏審閱者備註，同時保留核心內容以供分發。

## 大檔案效能建議
1. **及時釋放串流** – `using` 陳述式會自動關閉串流，釋放記憶體。  
2. **批次處理** – 迭代檔案集合，若格式允許則重複使用單一 `Redactor` 實例，以減少分配開銷。  

## 疑難排解

1. **檔案存取被拒** – 確認應用程式帳號對目標資料夾具有讀寫權限。  
2. **編輯未套用** – 確認所選的編輯類型與文件格式相容（例如 `DeleteAnnotationRedaction` 可用於 PDF 與 DOCX）。  

## 常見問題

**Q: 可使用串流處理哪些檔案格式？**  
A: 使用串流 API 時，GroupDocs.Redaction 支援超過 70 種格式，包括 PDF、DOCX、XLSX、PPTX 與 HTML。

**Q: 可以在儲存前預覽編輯結果嗎？**  
A: 可以，呼叫 `redactor.GetRedactedDocument()` 可取得記憶體中的文件表示，您可以以程式方式渲染或檢查。

**Q: 函式庫如何處理受密碼保護的檔案？**  
A: 在使用接受 `LoadOptions`（內含密碼）的 `Redactor` 重載開啟串流時，提供密碼即可。

**Q: 文件大小有上限嗎？**  
A: 引擎可處理最高 2 GB 的檔案；較大的檔案應拆分或分塊處理，以符合記憶體限制。

**Q: 每個部署環境需要單獨的授權嗎？**  
A: 只要使用符合授權協議，一組授權金鑰即可在多個環境中使用。

## 結論
您現在擁有使用 GroupDocs.Redaction 透過串流進行 **redact documents .net** 的完整步驟解決方案。直接從串流載入檔案、套用目標編輯，並在不產生中間產物的情況下儲存，既確保安全又提升效能。可探索其他編輯類型，例如文字取代或中繼資料移除，以符合您的特定合規需求。

---

**最後更新:** 2026-07-06  
**測試環境:** GroupDocs.Redaction 5.0 for .NET  
**作者:** GroupDocs  

## 資源
- [文件說明](https://docs.groupdocs.com/redaction/net/)
- [API 參考](https://reference.groupdocs.com/redaction/net)
- [下載](https://releases.groupdocs.com/redaction/net/)
- [免費支援論壇](https://forum.groupdocs.com/c/redaction/33)
- [臨時授權](https://purchase.groupdocs.com/temporary-license/)

```csharp
string sourceFile = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "sample.docx");
using (Stream stream = File.Open(sourceFile, FileMode.Open, FileAccess.ReadWrite))
{
    // Proceed with document processing...
}
```

```csharp
using (var redactor = new GroupDocs.Redaction.Redactor(stream))
{
    // Apply redactions...
}
```

```csharp
redactor.Apply(new GroupDocs.Redaction.Redactions.DeleteAnnotationRedaction());
```

```csharp
string outputFile = Path.Combine("YOUR_OUTPUT_DIRECTORY", "redacted_sample.docx");
using (Stream streamOut = File.Open(outputFile, FileMode.Create, FileAccess.Write))
{
    redactor.Save(streamOut, new GroupDocs.Redaction.Options.RasterizationOptions { Enabled = false });
}
```

## 相關教學

- [如何使用 GroupDocs.Redaction .NET 載入與編輯文件：完整指南](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [使用 GroupDocs.Redaction for .NET 編輯並儲存文件：完整指南](/redaction/net/document-saving/redact-save-documents-groupdocs-redaction-net/)
- [如何使用 GroupDocs.Redaction .NET 從串流擷取文件中繼資料](/redaction/net/document-information/extract-document-info-streams-groupdocs-redaction-dotnet/)