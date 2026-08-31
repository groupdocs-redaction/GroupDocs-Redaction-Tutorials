---
date: '2026-03-28'
description: 學習如何在 GroupDocs.Redaction for .NET 中使用 C# 實作自訂記錄器，啟用詳細的自訂日誌記錄，並更輕鬆地完成合規報告。
keywords:
- custom logger c#
- custom logging .net
- save redacted document
- log warnings c#
title: 在 GroupDocs.Redaction for .NET 中實作自訂 C# 記錄器
type: docs
url: /zh-hant/net/advanced-redaction/custom-logging-groupdocs-redaction-net/
weight: 1
---

# 在 GroupDocs.Redaction for .NET 中實作自訂 logger c#

有效管理文件遮蔽至關重要，尤其在處理敏感資訊時。本指南將教您 **如何在 GroupDocs.Redaction for .NET 中實作自訂 logger c#**，讓您全面掌控記錄、錯誤處理與稽核追蹤。

## 快速答案
- **自訂 logger c# 的作用是什麼？** 它會在遮蔽過程中捕獲錯誤、警告與資訊訊息。  
- **哪個函式庫提供 ILogger 介面？** GroupDocs.Redaction for .NET。  
- **我能在不進行光柵化的情況下儲存已遮蔽的文件嗎？** 可以 – 使用 `redactor.Save(..., new Options.RasterizationOptions { Enabled = false })`。  
- **生產環境使用是否需要授權？** 正式版授權是必需的；亦提供試用版供評估使用。  
- **此方法是否相容於 .NET Core / .NET 6+？** 完全相容 – 相同的 API 可在 .NET Framework 及 .NET Core/5/6 上運作。

## 什麼是自訂 logger c#？
**自訂 logger c#** 是一個實作 GroupDocs.Redaction 所提供的 `ILogger` 介面的類別。它讓您能將記錄訊息傳送至任意位置——如主控台、檔案、資料庫或外部監控系統——同時提供清晰的遮蔽工作流程檢視。

## 為何在 GroupDocs.Redaction 中使用自訂 .NET 記錄？
- **合規與稽核：** 詳細的記錄滿足法規要求。  
- **錯誤可見性：** `LogError` 與 `LogWarning` 可即時回饋問題。  
- **整合彈性：** 可將記錄轉發至現有的 .NET 記錄框架（Serilog、NLog 等）。

## 前置條件
- 已安裝 **GroupDocs.Redaction for .NET**（請參閱以下安裝說明）。  
- .NET 開發環境（Visual Studio、VS Code 或 CLI）。  
- 基本的 C# 知識與檔案串流使用經驗。  

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
- **臨時授權：** 在有限期間內取得完整功能。  
- **購買：** 獲得永久授權以供正式部署使用。

## 步驟指南

### 步驟 1：定義自訂 logger 類別（log warnings c#）
建立一個實作 `ILogger` 的類別。此類別會捕獲錯誤、警告與資訊訊息。

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

**說明：** `HasErrors` 旗標可協助您判斷是否繼續處理。這三個方法對應於大多數遮蔽情境中所需的三種記錄層級。

### 步驟 2：準備檔案路徑並開啟來源文件
```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
string outputFile = Utils.GetOutputFile(sourceFile);
```

**為何重要：** 使用工具方法可讓程式碼保持整潔，且在嘗試 **儲存已遮蔽文件** 前確保輸出資料夾已存在。

### 步驟 3：套用遮蔽同時使用自訂 logger
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

**說明：**  
1. 透過 `RedactorSettings(logger)` 建立 `Redactor` 實例，將您的 `CustomLogger` 連結進去。  
2. 套用遮蔽後，程式會檢查 `logger.HasErrors`。若未發生錯誤，則儲存文件——示範了在不進行光柵化的情況下 **儲存已遮蔽文件** 的邏輯。

### 常見陷阱與故障排除
- **缺少記錄輸出：** 確認每個 `Log*` 方法皆正確覆寫。  
- **檔案存取例外：** 確保應用程式對來源與輸出路徑皆具有讀寫權限。  
- **Logger 未正確連接：** `RedactorSettings(logger)` 參數是必要的，若省略則會停用自訂記錄。

## 實務應用
1. **合規報告：** 將記錄條目匯出為 CSV 或資料庫，以供稽核追蹤。  
2. **錯誤追蹤：** 透過掃描 `LogError` 輸出快速定位問題檔案。  
3. **工作流程自動化：** 當呼叫 `LogWarning` 時觸發後續流程（例如通知合規主管）。  

## 效能考量
- **即時釋放串流** 以釋放記憶體，特別是在處理大量批次時。  
- **監控 CPU 與記憶體** 使用情況於大量遮蔽時；可考慮平行處理文件，同時謹慎同步 logger。  
- **保持更新：** 新版 GroupDocs.Redaction 常包含效能優化與額外的記錄掛鉤。  

## 結論
透過實作 **custom logger c#**，您能深入了解遮蔽流程的每個步驟，從而更輕鬆符合合規標準與除錯。此方法與 GroupDocs.Redaction for .NET 完美結合，且可擴充以整合您已使用的任何 .NET 記錄框架。

---

## 常見問答

**Q: 使用 GroupDocs.Redaction 的自訂記錄目的為何？**  
A: 自訂記錄有助於追蹤與管理遮蔽，以符合合規、錯誤追蹤與工作流程最佳化。

**Q: 如何使用自訂 logger 處理錯誤？**  
A: 在 `CustomLogger` 類別中實作 `LogError`；`HasErrors` 旗標可在需要時中止處理。

**Q: 自訂記錄能否與其他系統整合？**  
A: 可以，透過擴充 logger 方法，將記錄訊息轉發至 CRM、ERP 或集中監控工具。

**Q: 實作自訂記錄時常見的陷阱有哪些？**  
A: 方法實作錯誤、缺少 `RedactorSettings(logger)`，以及檔案權限問題是最常見的。

**Q: 自訂記錄如何提升文件遮蔽工作流程？**  
A: 詳細的記錄提供即時可視性、簡化除錯，並滿足稽核需求。

## 資源
- **文件說明：** [GroupDocs.Redaction .NET Documentation](https://docs.groupdocs.com/redaction/net/)
- **API 參考：** [GroupDocs.Redaction API Reference](https://reference.groupdocs.com/redaction/net)
- **下載：** [GroupDocs.Redaction for .NET](https://downloads.groupdocs.com/redaction/net)

---

**最後更新：** 2026-03-28  
**測試環境：** GroupDocs.Redaction 23.11 for .NET  
**作者：** GroupDocs  

---