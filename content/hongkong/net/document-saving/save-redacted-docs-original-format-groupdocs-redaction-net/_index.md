---
date: '2026-07-06'
description: 了解如何使用 GroupDocs.Redaction for .NET 在保留原始格式的同時儲存已遮蔽文件。請遵循此一步一步的指南，快速且安全地執行遮蔽。
keywords:
- save redacted document
- GroupDocs.Redaction .NET
- document redaction tutorial
schemas:
- author: GroupDocs
  dateModified: '2026-07-06'
  description: Learn how to save a redacted document while preserving its original
    format with GroupDocs.Redaction for .NET. Follow this step‑by‑step guide for fast,
    secure redaction.
  headline: Save Redacted Document in Original Format Using GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to save a redacted document while preserving its original
    format with GroupDocs.Redaction for .NET. Follow this step‑by‑step guide for fast,
    secure redaction.
  name: Save Redacted Document in Original Format Using GroupDocs.Redaction .NET
  steps:
  - name: Initialize the Redactor
    text: 'Create an instance of the `Redactor` class with your document’s file path:'
  - name: Apply Exact Phrase Redaction
    text: '`ExactPhraseRedaction` is a built‑in redaction type that searches for an
      exact string and replaces it with a black rectangle or custom text.'
  - name: Configure Save Options
    text: '`SaveOptions` lets you keep the source file type, specify a suffix, and
      control memory usage.'
  - name: Save and Output
    text: 'Call the `Save` method with the configured options to write the redacted
      file to disk:'
  type: HowTo
- questions:
  - answer: Over 30 formats, including PDF, DOCX, PPTX, XLSX, and common image types
      such as PNG and JPEG.
    question: What file types can GroupDocs.Redaction handle?
  - answer: Yes – the `Redactor` class provides a `GetRedactions()` method that returns
      a collection you can render in a UI.
    question: Is it possible to preview redactions before saving?
  - answer: Absolutely. Supply the password when constructing the `Redactor` instance
      to unlock the file.
    question: Can I redact password‑protected documents?
  - answer: Yes – the NuGet package is compatible with .NET Framework 4.7.2+, .NET
      Core 3.1+, and .NET 5/6+.
    question: Does the library support .NET Core and .NET 5/6?
  - answer: Purchase a license through the GroupDocs website; a temporary trial license
      is available for evaluation.
    question: How do I obtain a production license?
  type: FAQPage
title: 使用 GroupDocs.Redaction .NET 以原始格式儲存已遮蔽文件
type: docs
url: /zh-hant/net/document-saving/save-redacted-docs-original-format-groupdocs-redaction-net/
weight: 1
---

# 使用 GroupDocs.Redaction .NET 將已編輯文件保存為原始格式

Redacting sensitive data is a common compliance requirement, but you don’t want to lose the look and feel of the original file. **This tutorial shows you how to save a redacted document while keeping its original format intact** using GroupDocs.Redaction for .NET. You’ll get a ready‑to‑run solution that works with PDFs, Word files, and more.

## 快速解答
- **什麼是保存已編輯文件的最快方法？** 使用 `Redactor` 載入檔案，套用 `ExactPhraseRedaction`，然後以保留原始檔案類型的 `SaveOptions` 呼叫 `Save`。  
- **支援哪些格式？** 超過 30 種格式，包括 PDF、DOCX、PPTX 以及各類影像格式。  
- **試用是否需要授權？** 需要 – 從 GroupDocs 入口網站取得臨時授權。  
- **可以為儲存的檔案加上自訂字尾嗎？** 當然可以 – 將 `SaveOptions.Suffix` 設為任意字串（例如日期）。  
- **大型檔案處理是否節省記憶體？** 是 – GroupDocs.Redaction 以串流方式處理資料，從不將整個檔案載入記憶體。  

## 什麼是「保存已編輯文件」？
*保存已編輯文件* 指將已修改的檔案寫回儲存空間，同時保留原始的版面配置、檔案類型與中繼資料。GroupDocs.Redaction 只需一次呼叫即可完成，免除手動格式轉換的需求。此過程亦會保留嵌入的資源，如字型、影像與文件屬性，確保輸出與來源檔案在外觀上完全相同，僅差異於已移除的內容。

## 為何使用 GroupDocs.Redaction for .NET？
GroupDocs.Redaction 支援 **30+ 種輸入與輸出格式**，且可處理最高 **500 MB** 的檔案而不需將整份文件載入記憶體，較傳統的檔案重寫方式提升 **20‑30 %** 的效能。其 API 完全受管，不需外部軟體，且符合 GDPR、HIPAA 以及其他法規要求。

## 前置條件
- **GroupDocs.Redaction for .NET** – 核心函式庫（最新穩定版）。  
- **.NET 6+** 或 **.NET Framework 4.7.2+** 已安裝於開發機器上。  
- 具備基本的 C# 知識，並熟悉 Visual Studio 或您偏好的 IDE。

### 必要的函式庫與相依性
- **GroupDocs.Redaction for .NET**：套用編輯所必需的函式庫。

### 環境設定需求
- 確認您的專案目標為受支援的 .NET 執行環境。請參閱官方 GroupDocs 文件以取得確切的版本對照表。

### 知識前置條件
- 了解 C# 語法、檔案 I/O 以及例外處理。

## 設定 GroupDocs.Redaction for .NET

### 安裝說明
**使用 .NET CLI：**  
```shell
dotnet add package GroupDocs.Redaction
```  

**使用 Package Manager Console：**  
```powershell
Install-Package GroupDocs.Redaction
```  

**透過 NuGet Package Manager UI：**  
- 在 Visual Studio 中開啟 NuGet 套件管理員。  
- 搜尋 **"GroupDocs.Redaction"** 並安裝最新版本。

### 取得授權
先使用免費試用版測試功能。若有需要，可前往 GroupDocs 官方網站申請臨時授權。若需長期使用，請考慮於其網站購買正式授權。

安裝並取得授權後，於程式碼檔案中引用 GroupDocs.Redaction 命名空間：  
```csharp
using GroupDocs.Redaction;
```  

## 實作指南

### 建立與設定 Redactor
`Redactor` 類別是載入文件並執行編輯操作的核心元件。  

#### 步驟 1：初始化 Redactor  
以文件路徑建立 `Redactor` 類別的實例：  
```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY"; // Replace with actual path.
using (Redactor redactor = new Redactor(sourceFile))
{
    ...
}
```  

#### 步驟 2：套用 Exact Phrase Redaction  
`ExactPhraseRedaction` 為內建的編輯類型，會搜尋精確字串並以黑色矩形或自訂文字取代。  
```csharp
// This replaces all instances of "John Doe" with "[personal]".
redactor.Apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]"));
```  

### 保存已編輯的文件
在保留原始格式的同時加入字尾，由 `SaveOptions` 處理。  

#### 步驟 3：設定 Save Options  
`SaveOptions` 讓您保留來源檔案類型、指定字尾，並控制記憶體使用。  
```csharp
var saveOptions = new SaveOptions() 
{
    AddSuffix = true,                  // Adds a suffix like "2023-10-12" to indicate modification.
    RasterizeToPDF = false,           // Ensures the document remains in its original format.
    RedactedFileSuffix = DateTime.Now.ToShortDateString()
};
```  

#### 步驟 4：保存與輸出  
呼叫 `Save` 方法並傳入設定好的選項，即可將已編輯的檔案寫入磁碟：  
```csharp
var outputFile = redactor.Save(saveOptions);
Console.WriteLine($"\nSource document was redacted successfully.\nFile saved to {outputFile}.\n");
```  

### 如何在保留原始格式的同時保存已編輯文件？
使用 `new Redactor("source.pdf")` 載入來源檔案，套用一項或多項編輯，設定 `SaveOptions` 以保留原始格式並加入字尾（例如 “_redacted”），最後呼叫 `redactor.Save("output.pdf", saveOptions)`。此單一步驟工作流程確保輸出在版面、字型與中繼資料上與輸入檔案相同，同時永久移除已編輯的內容。

### 常見問題與解決方案
- **文件無法載入** – 檢查檔案路徑並確保程式具有讀取權限。  
- **編輯失敗** – 再次確認精確字串的拼寫與大小寫；必要時使用 `IgnoreCase = true`。  
- **輸出檔案損毀** – 確認 `SaveOptions` 與來源格式相符；格式不匹配可能導致結果損毀。  

## 實務應用
GroupDocs.Redaction .NET 在受規範的產業中表現卓越：

1. **法律文件管理** – 在分享合約前自動移除客戶姓名、社會安全號碼或案件編號。  
2. **醫療資料隱私** – 在醫療記錄中遮蔽患者識別資訊，以符合 HIPAA 規範。  
3. **財務報告** – 在發佈季報前移除機密帳號，以保護資訊。  

## 效能考量
處理大型檔案（數百 MB）時，請遵循以下最佳實踐：

- 使用簡潔的搜尋模式以降低 CPU 使用率。  
- 盡快釋放 `Redactor` 實例（使用 `using` 區塊）以釋放非受控資源。  
- 設定 `SaveOptions.Streaming = true` 以降低記憶體佔用。  

## 結論
您現在已掌握完整且可投入生產的方式，使用 GroupDocs.Redaction for .NET **在原始格式中保存已編輯文件**。依循上述步驟，即可將安全的編輯功能整合至任何 .NET 工作流程，確保合規同時不犧牲文件的完整性。

探索進階功能，如批次編輯、自訂編輯形狀，以及與雲端儲存的整合，以進一步擴充您的解決方案。

## 常見問答

**Q: GroupDocs.Redaction 能處理哪些檔案類型？**  
A: 超過 30 種格式，包括 PDF、DOCX、PPTX、XLSX，以及常見的影像類型如 PNG 與 JPEG。

**Q: 是否可以在保存前預覽編輯結果？**  
A: 可以 – `Redactor` 類別提供 `GetRedactions()` 方法，回傳可於 UI 中呈現的編輯集合。

**Q: 能編輯受密碼保護的文件嗎？**  
A: 完全可以。於建立 `Redactor` 實例時提供密碼，即可解鎖檔案。

**Q: 此函式庫是否支援 .NET Core 與 .NET 5/6？**  
A: 支援 – NuGet 套件相容於 .NET Framework 4.7.2+、.NET Core 3.1+ 以及 .NET 5/6+。

**Q: 如何取得正式授權？**  
A: 透過 GroupDocs 官網購買授權；亦提供臨時試用授權供評估使用。

## 資源
- **文件**： [GroupDocs Redaction .NET Documentation](https://docs.groupdocs.com/redaction/net/)  
- **API 參考**： [API Reference](https://reference.groupdocs.com/redaction/net)  
- **下載**： [GroupDocs Releases for .NET](https://releases.groupdocs.com/redaction/net/)  
- **免費支援**： [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)  
- **臨時授權**： [Get a Temporary License](https://purchase.groupdocs.com/temporary-license/)  

---

**最後更新：** 2026-07-06  
**測試環境：** GroupDocs.Redaction 2.0.0 for .NET  
**作者：** GroupDocs

## 相關教學

- [GroupDocs.Redaction .NET 文件保存教學](/redaction/net/document-saving/)  
- [使用串流於 .NET 安全文件編輯：GroupDocs.Redaction 指南](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)  
- [如何使用 GroupDocs.Redaction for .NET 將文件保存為光柵化 PDF：完整指南](/redaction/net/document-saving/groupdocs-redaction-net-rasterized-pdfs/)