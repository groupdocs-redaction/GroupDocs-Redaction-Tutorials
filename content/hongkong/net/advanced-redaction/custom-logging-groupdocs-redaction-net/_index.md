---
date: '2026-10-01'
description: 了解如何在 GroupDocs.Redaction for .NET 中實作自訂記錄器 c#，啟用詳細的自訂記錄，並更輕鬆完成合規報告。
keywords:
- custom logger c#
- implement custom logger
- save redacted document
- custom logger .net core
- log warnings c#
lastmod: '2026-10-01'
og_description: 在 GroupDocs.Redaction for .NET 中實作自訂記錄器 c#，以捕捉詳細日誌、儲存已編輯文件而不進行光柵化，並符合合規需求。
og_image_alt: Guide showing how to add a custom logger to GroupDocs.Redaction in a
  .NET application
og_title: 在 GroupDocs.Redaction for .NET 中實作自訂記錄器 c#
schemas:
- author: GroupDocs
  dateModified: '2026-10-01'
  description: Learn how to implement a custom logger c# in GroupDocs.Redaction for
    .NET, enabling detailed custom logging .net and easier compliance reporting.
  headline: Implement custom logger c# in GroupDocs.Redaction for .NET
  type: TechArticle
- description: Learn how to implement a custom logger c# in GroupDocs.Redaction for
    .NET, enabling detailed custom logging .net and easier compliance reporting.
  name: Implement custom logger c# in GroupDocs.Redaction for .NET
  steps:
  - name: Define a custom logger class (log warnings c#)
    text: The `CustomLogger` class implements `ILogger`. CustomLogger is a user‑defined
      class that implements the `ILogger` interface to capture redaction events. **Definition
      anchor:** `CustomLogger` is a user‑defined implementation of the `ILogger` interface
      that records redaction events. **Explanation:** T
  - name: Prepare file paths and open the source document
    text: '**Definition anchor:** `Redactor` is the primary class in GroupDocs.Redaction
      that performs redaction operations on a PDF document. **Why this matters:**
      Using utility methods keeps your code clean and guarantees the output folder
      exists before you attempt to **save redacted document**.'
  - name: Apply redactions while using the custom logger
    text: '**Direct answer:** The redaction workflow starts by creating a `Redactor`
      instance with `RedactorSettings(logger)`, then applying redaction objects, checking
      `logger.HasErrors`, and finally calling `redactor.Save` with rasterization disabled.
      This pattern ensures every step is logged and that you on'
  type: HowTo
- questions:
  - answer: Custom logging captures detailed redaction events, satisfies audit requirements,
      and simplifies troubleshooting by exposing errors and warnings in real time.
    question: What is the purpose of custom logging with GroupDocs.Redaction?
  - answer: Implement `LogError` in your `CustomLogger` class; the `HasErrors` flag
      lets you abort processing if a critical issue is detected.
    question: How do I handle errors using a custom logger?
  - answer: Yes—you can forward log messages to CRM, ERP, or centralized monitoring
      tools by extending the logger methods.
    question: Can custom logging be integrated with other systems?
  - answer: Missing method overrides, forgetting to pass `RedactorSettings(logger)`,
      and insufficient file permissions are the most frequent issues.
    question: What are common pitfalls when implementing custom logging?
  - answer: Detailed logs provide real‑time visibility, streamline debugging, and
      generate the audit trails required by regulations such as GDPR and HIPAA.
    question: How does custom logging improve document redaction workflows?
  type: FAQPage
tags:
- custom logger
- GroupDocs.Redaction
- .NET logging
- document redaction
title: 在 GroupDocs.Redaction for .NET 中實作自訂記錄器 c#
type: docs
url: /zh-hant/net/advanced-redaction/custom-logging-groupdocs-redaction-net/
weight: 1
---

# 在 GroupDocs.Redaction for .NET 中實作自訂記錄器 C#

有效管理文件遮蔽至關重要，尤其在處理敏感資訊時更是如此。在本指南中，您將學習 **如何在 GroupDocs.Redaction for .NET 中實作自訂記錄器 C#**，讓您全面掌控記錄、錯誤處理與稽核追蹤。完成教學後，您將能捕捉警告、錯誤與資訊訊息，將記錄器整合至現有的 .NET 記錄框架，並在不進行光柵化的情況下儲存已遮蔽的文件。

## 快速解答
- **自訂記錄器 C# 有什麼作用？** 它在遮蔽過程中捕捉錯誤、警告與資訊訊息，提供可搜尋的稽核追蹤。  
- **哪個函式庫提供 ILogger 介面？** GroupDocs.Redaction for .NET 提供 `ILogger` 介面。  
- **我可以在不進行光柵化的情況下儲存已遮蔽的文件嗎？** 可以 – 呼叫 `redactor.Save(..., new Options.RasterizationOptions { Enabled = false })`。  
- **正式環境使用需要授權嗎？** 正式環境需要完整授權；可使用試用授權進行評估。  
- **此方法相容於 .NET Core / .NET 6 以上嗎？** 完全相容 – 同一套 API 可在 .NET Framework、.NET Core、.NET 5 及 .NET 6 上運作。

## 什麼是自訂記錄器 C#？

**自訂記錄器 C#** 是一個實作 GroupDocs.Redaction 所提供的 `ILogger` 介面的類別。它允許您將記錄訊息導向任意位置——如主控台、檔案、資料庫或外部監控系統，同時提供對整體遮蔽工作流程的清晰概觀。

## 為何在 GroupDocs.Redaction 中使用自訂記錄 .NET？

為您的遮蔽流程加上詳細且可搜尋的記錄，以符合監管稽核需求並加速除錯。GroupDocs.Redaction 支援 **70 多種輸入與輸出格式**，且可在不將整個檔案載入記憶體的情況下處理最多 500 頁的文件，因此設計良好的記錄器幾乎不會增加負擔，同時提供寶貴的可見性。

## 前置條件
- 已安裝 GroupDocs.Redaction for .NET（請參閱下方的 **Installation** 章節）。  
- .NET 開發環境（Visual Studio、VS Code 或 .NET CLI）。  
- 基本的 C# 知識與檔案串流概念。  

## 安裝

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
搜尋 **"GroupDocs.Redaction"** 並安裝最新版本。

## 取得授權
- **免費試用：** 使用臨時授權測試 API。  
- **臨時授權：** 在有限期間內取得完整功能存取。  
- **購買：** 取得永久授權以供正式環境部署。  

## 步驟指南

### 如何在 .NET Core 中實作自訂記錄器？

將 `CustomLogger` 類別載入您的 .NET Core 專案，並將其連接至 `RedactorSettings`。此記錄器在 .NET Framework、.NET 5 與 .NET 6 上的運作方式相同，您可以在所有平台間共用相同程式碼。

### 步驟 1：定義自訂記錄器類別（記錄警告 C#）

`CustomLogger` 類別實作 `ILogger`。  
CustomLogger 是使用者自訂的類別，實作 `ILogger` 介面以捕捉遮蔽事件。  
```csharp
using System;
using GroupDocs.Redaction;

class CustomLogger : ILogger
{
    public bool HasErrors { get; private set; }

    // Log errors encountered during processing.
    public void LogError(string message)
    {
        Console.WriteLine("Error: " + message);
        HasErrors = true;
    }

    // Log warnings that may not be critical but need attention.
    public void LogWarning(string message)
    {
        Console.WriteLine("Warning: " + message);
    }

    // Log informational messages for tracking normal operations.
    public void LogInfo(string message)
    {
        Console.WriteLine("Info: " + message);
    }
}
```  

**定義說明：** `CustomLogger` 是 `ILogger` 介面的使用者自訂實作，用於記錄遮蔽事件。  
**說明：** `HasErrors` 標誌協助您決定是否繼續處理。這三個方法對應於大多數遮蔽情境中需要的三個記錄層級。

### 步驟 2：準備檔案路徑並開啟來源文件

```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
string outputFile = Utils.GetOutputFile(sourceFile);
```  

**定義說明：** `Redactor` 是 GroupDocs.Redaction 中執行 PDF 文件遮蔽操作的主要類別。  
**重要性說明：** 使用工具方法可保持程式碼整潔，並確保在嘗試 **儲存已遮蔽文件** 前，輸出資料夾已存在。

### 步驟 3：在使用自訂記錄器的同時套用遮蔽

```csharp
using (Stream stream = File.Open(sourceFile, FileMode.Open, FileAccess.ReadWrite))
{
    var logger = new CustomLogger();
    
    using (Redactor redactor = new Redactor(stream, new LoadOptions(), new RedactorSettings(logger)))
    {
        // Apply a redaction to the document.
        redactor.Apply(new DeleteAnnotationRedaction());
        
        if (!logger.HasErrors)
        {
            using (Stream streamOut = File.Open(outputFile, FileMode.OpenOrCreate, FileAccess.ReadWrite))
            {
                // Save changes without rasterizing the output.
                redactor.Save(streamOut, new Options.RasterizationOptions { Enabled = false });
            }
        }
    }
}
```  

**直接回答：** 遮蔽工作流程從使用 `RedactorSettings(logger)` 建立 `Redactor` 實例開始，接著套用遮蔽物件，檢查 `logger.HasErrors`，最後以停用光柵化的方式呼叫 `redactor.Save`。此模式確保每個步驟皆被記錄，且僅在未發生錯誤時才持久化乾淨的文件。  

**說明：**  
1. 透過 `RedactorSettings(logger)` 實例化 `Redactor`，將您的 `CustomLogger` 連結進去。  
2. 套用遮蔽後，程式碼會檢查 `logger.HasErrors`。若未發生錯誤，則儲存文件——示範了在不進行光柵化的情況下 **儲存已遮蔽文件** 的邏輯。

## 常見問題與除錯
- **缺少記錄輸出：** 確認每個 `Log*` 方法皆正確覆寫。  
- **檔案存取例外：** 確保應用程式對來源與輸出路徑皆具讀寫權限。  
- **記錄器未連接：** `RedactorSettings(logger)` 參數是必要的，若省略則會停用自訂記錄。

## 實務應用
1. **合規報告：** 將記錄條目匯出為 CSV 或資料庫，以作為稽核追蹤。  
2. **錯誤追蹤：** 透過掃描 `LogError` 輸出快速定位問題檔案。  
3. **工作流程自動化：** 當呼叫 `LogWarning` 時觸發後續流程（例如通知合規主管）。

## 效能考量
- **及時釋放串流** 以釋放記憶體，特別是在處理大量批次時。  
- **監控 CPU 與記憶體** 使用情況於大量遮蔽時；可考慮平行處理文件，同時注意記錄器的同步問題。  
- **保持更新：** 新版 GroupDocs.Redaction 常包含效能最佳化與額外的記錄掛鉤。

## 結論

透過實作 **自訂記錄器 C#**，您可深入了解遮蔽流程的每個步驟，讓符合合規標準與除錯變得更簡單。此方法與 GroupDocs.Redaction for .NET 完美結合，且可延伸整合至您已使用的任何 .NET 記錄框架。

---

## 常見問答

**Q: 使用 GroupDocs.Redaction 的自訂記錄有何目的？**  
A: 自訂記錄捕捉詳細的遮蔽事件，滿足稽核需求，並透過即時顯示錯誤與警告簡化除錯。

**Q: 如何使用自訂記錄器處理錯誤？**  
A: 在 `CustomLogger` 類別中實作 `LogError`；`HasErrors` 標誌讓您在偵測到關鍵問題時中止處理。

**Q: 自訂記錄能整合至其他系統嗎？**  
A: 可以——透過擴充記錄器方法，將記錄訊息轉發至 CRM、ERP 或集中式監控工具。

**Q: 實作自訂記錄時常見的陷阱是什麼？**  
A: 常見問題包括遺漏方法覆寫、忘記傳入 `RedactorSettings(logger)`，以及檔案權限不足。

**Q: 自訂記錄如何提升文件遮蔽工作流程？**  
A: 詳細的記錄提供即時可見性，簡化除錯，並產生符合 GDPR、HIPAA 等法規要求的稽核追蹤。

## 資源

- **文件說明：** [GroupDocs.Redaction .NET Documentation](https://docs.groupdocs.com/redaction/net/)  
- **API 參考：** [GroupDocs.Redaction API Reference](https://reference.groupdocs.com/redaction/net)  
- **下載：** [GroupDocs.Redaction for .NET](https://downloads.groupdocs.com/redaction/net)

---

**最後更新：** 2026-10-01  
**測試環境：** GroupDocs.Redaction 23.11 for .NET  
**作者：** GroupDocs  

---

## 相關教學

- [如何使用 GroupDocs.Redaction for .NET 載入文件](/redaction/net/document-loading/)  
- [如何使用 GroupDocs.Redaction .NET 匯出已遮蔽文件](/redaction/net/document-saving/)  
- [使用 GroupDocs.Redaction .NET 實作文件遮蔽&#58; 逐步指南](/redaction/net/getting-started/implement-document-redaction-groupdocs-redaction-net/)