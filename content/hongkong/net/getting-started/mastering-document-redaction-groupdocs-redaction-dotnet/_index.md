---
date: '2026-10-11'
description: 了解如何使用 GroupDocs.Redaction for .NET 來遮蔽 PDF 敏感資訊。一步一步的指南涵蓋設定、程式碼、效能技巧以及實際案例。
keywords:
- redact sensitive information pdf
- how to redact pdf .net
- groupdocs redaction tutorial
- document redaction .net
- redaction best practices
lastmod: '2026-10-11'
og_description: 了解如何使用 GroupDocs.Redaction for .NET 來遮蔽 PDF 敏感資訊。本指南將帶您逐步完成安裝、程式碼編寫與效能優化。
og_image_alt: Screenshot of GroupDocs.Redaction UI showing redacted PDF content
og_title: 如何在 .NET 應用程式中遮蔽 PDF 敏感資訊
schemas:
- author: GroupDocs
  dateModified: '2026-10-11'
  description: Learn how to redact sensitive information pdf using GroupDocs.Redaction
    for .NET. Step‑by‑step guide covers setup, code, performance tips, and real‑world
    use cases.
  headline: How to redact sensitive information pdf in .NET apps
  type: TechArticle
- description: Learn how to redact sensitive information pdf using GroupDocs.Redaction
    for .NET. Step‑by‑step guide covers setup, code, performance tips, and real‑world
    use cases.
  name: How to redact sensitive information pdf in .NET apps
  steps:
  - name: load your document
    text: 'Load your PDF into a `Redactor` instance: **Explanation:** The constructor
      accepts the file path and optional load options, preparing the document for
      further actions.'
  - name: define and apply redaction
    text: 'Create a `TextRedaction` object that describes what text to hide and how
      to replace it: **Explanation:** `TextRedaction` lets you specify a regular expression,
      case‑insensitivity, and replacement text such as “[REDACTED]”. You can also
      choose a black‑box overlay if visual masking is required.'
  - name: save the redacted document
    text: 'Persist the changes to a new file: **Explanation:** Saving creates a fresh
      PDF while leaving the original untouched, which is essential for audit trails.'
  type: HowTo
- questions:
  - answer: Yes – enable OCR via `OcrOptions` and the engine will recognise text inside
      raster images before applying redaction.
    question: Can I redact images that contain text?
  - answer: Absolutely. Supply the password in `LoadOptions` when constructing the
      `Redactor`.
    question: Does GroupDocs.Redaction work with password‑protected PDFs?
  - answer: .NET Framework 4.6+, .NET Core 3.1, .NET 5, .NET 6, and later releases.
    question: What .NET versions are officially supported?
  - answer: Use the `Redactor.ValidateRedaction` method to ensure no hidden text remnants
      remain.
    question: How do I verify that redaction was successful?
  - answer: Yes – iterate through `Directory.GetFiles` and call the redaction routine
      asynchronously for each file.
    question: Is it possible to batch‑process a folder of PDFs?
  type: FAQPage
tags:
- document redaction
- groupdocs.redaction
- .net security
title: 如何在 .NET 應用程式中遮蔽 PDF 敏感資訊
type: docs
url: /zh-hant/net/getting-started/mastering-document-redaction-groupdocs-redaction-dotnet/
weight: 1
---

# 如何在 .NET 應用程式中對 PDF 進行敏感資訊遮蔽

對 PDF 進行敏感資訊遮蔽是任何處理機密文件的組織的關鍵步驟。在本教學中，您將了解如何使用 **GroupDocs.Redaction** 自動定位並隱藏個人資料、法律條款或您選擇的任何文字。完成後，您將擁有一個可在 .NET Core、.NET Framework 以及 .NET 5/6+ 專案中運作的可投入生產的解決方案。

## 快速解答
- **什麼函式庫負責在 .NET 中對 PDF 進行遮蔽？** GroupDocs.Redaction for .NET.  
- **GroupDocs.Redaction 支援多少種格式？** 超過 30 種輸入與輸出格式，包括 PDF、DOCX、PPTX 以及影像。  
- **我能在不將整個檔案載入記憶體的情況下處理 500 頁的 PDF 嗎？** 可以 – API 會串流頁面，將記憶體使用量控制在 100 MB 以下。  
- **開發時需要授權嗎？** 可取得免費的暫時授權以供評估。  
- **是否支援非同步處理？** 最新版本提供 async 方法以實現非阻塞 I/O。

## 什麼是 PDF 敏感資訊遮蔽？

`redact sensitive information pdf` 指的是永久移除或遮蔽 PDF 檔案內的機密文字與資料的過程，使其無法在之後被復原、檢視或擷取。遮蔽會以佔位字元或視覺方塊取代原始內容，以確保符合隱私法規並保護敏感資訊。

## 為什麼在 .NET 中使用 GroupDocs.Redaction？

GroupDocs.Redaction 支援 **50+ 檔案格式**，且可處理高達 **1 GB** 的文件而無需將整個檔案載入記憶體，提供比手動遮蔽工具快 **3 倍** 的處理速度。其內建的 OCR 與模式匹配引擎讓您只需一行程式碼即可針對個人識別碼、信用卡號碼或自訂關鍵字進行遮蔽。

## 前置條件

- 已安裝 .NET Core 3.1、.NET 5、.NET 6 或 .NET Framework 4.6+。  
- Visual Studio 2022（或您偏好的任何 IDE）。  
- 基本的 C# 知識與檔案 I/O 的熟悉度。  
- 取得 **GroupDocs.Redaction** NuGet 套件（請參考以下安裝步驟）。

## 設定 GroupDocs.Redaction 於 .NET

### 安裝套件

**使用 .NET CLI：**  
```bash
dotnet add package GroupDocs.Redaction
```  

**使用 Package Manager：**  
```powershell
Install-Package GroupDocs.Redaction
```  

**透過 NuGet Package Manager UI：**  
在 NuGet 套件管理員中搜尋 “GroupDocs.Redaction”，並安裝最新版本。

### 取得授權

若要在正式環境中使用 GroupDocs.Redaction，您需要授權。您可以：

- 申請 [免費試用](https://purchase.groupdocs.com/temporary-license/) 以探索其功能。  
- 索取暫時授權以進行延長評估。  
- 購買完整授權以獲得無限制使用。

### 基本初始化與設定

第一步是建立一個 `Redactor` 實例，以管理所有遮蔽操作。  
```csharp
using System;
using System.IO;
using GroupDocs.Redaction;

class Program
{
    static void Main()
    {
        // Initialize the Redactor instance with a document path.
        using (Redactor redactor = new Redactor("path/to/your/document.pdf"))
        {
            // Apply your desired redactions here.
            Console.WriteLine("Document ready for redaction!");
        }
    }
}
```  

此物件會載入來源文件、套用遮蔽規則，並寫入輸出。

## 如何在 .NET 中對 PDF 進行敏感資訊遮蔽？

載入目標 PDF、定義遮蔽規則，並儲存結果——只需三個簡潔步驟。`Redactor` 會串流每一頁，即使是大型檔案也能有效處理且不會消耗過多記憶體。此方法確保原始文件保持不變，同時遮蔽後的版本符合安全標準。

### 步驟 1：載入文件

將您的 PDF 載入 `Redactor` 實例：  
```csharp
using (Redactor redactor = new Redactor("path/to/your/document.pdf"))
{
    // Proceed with redactions.
}
```  

**說明：** 建構函式接受檔案路徑與可選的載入選項，為後續操作做好準備。

### 步驟 2：定義並套用遮蔽

建立一個 `TextRedaction` 物件，描述要隱藏的文字以及替換方式：  
```csharp
// Create a text redaction instance specifying the text pattern.
TextRedaction textRedaction = new TextRedaction("sensitive-text", new ReplacementOptions("[REDACTED]"));

// Apply the redaction.
redactor.Apply(textRedaction);
```  

**說明：** `TextRedaction` 允許您指定正規表達式、大小寫不敏感以及替換文字（例如 “[REDACTED]”）。若需要視覺遮蔽，亦可選擇黑盒覆蓋。

### 步驟 3：儲存遮蔽後的文件

將變更持久化至新檔案：  
```csharp
redactor.Save("path/to/redacted/document.pdf");
```  

**說明：** 儲存會產生全新的 PDF，同時保留原始檔案未被修改，這對稽核追蹤至關重要。

## 常見問題與解決方案

`Redactor.RedactAsync` 是一個非同步方法，可在不阻塞呼叫執行緒的情況下執行遮蔽操作，允許對大型文件進行可擴展的處理。

- **遮蔽未套用：** 確認正則表達式模式完全符合目標文字。使用 `RegexOptions.IgnoreCase` 進行大小寫不敏感搜尋。  
- **大型 PDF 的效能瓶頸：** 啟用非同步處理（`Redactor.RedactAsync`）並使用 `Process.GetCurrentProcess().PrivateMemorySize64` 監控記憶體。  
- **掃描 PDF 缺少 OCR：** 在定義遮蔽規則前啟用 `OcrOptions`，將影像轉換為可搜尋的文字。

## 實務應用

GroupDocs.Redaction for .NET 在多種實務情境中表現優異：

1. **法律文件準備** – 在分享草稿前自動去除客戶識別碼。  
2. **資料隱私合規** – 每晚對數千個檔案執行 GDPR 或 HIPAA 的遮蔽政策。  
3. **財務報告** – 在財報發布中隱藏帳號與專有數據。  

這些範例說明了為何堅固的 PDF 遮蔽是現代文件工作流程中不可或缺的一環。

## 效能考量

- **非同步執行** 可減少桌面應用程式的 UI 阻塞，提升 Web 服務的吞吐量。  
- **串流模式** 可降低記憶體佔用；您可在 2 GB RAM 的虛擬機上安全處理 1 GB PDF。  
- **快取** 常用模板可避免重複解析，將批次作業速度提升最高 40 %。

## 常見問答

**Q: 我可以遮蔽含有文字的影像嗎？**  
A: 是的 – 透過 `OcrOptions` 啟用 OCR，引擎會在套用遮蔽前辨識點陣圖影像中的文字。

**Q: GroupDocs.Redaction 能處理受密碼保護的 PDF 嗎？**  
A: 當然可以。於建立 `Redactor` 時於 `LoadOptions` 中提供密碼。

**Q: 官方支援哪些 .NET 版本？**  
A: .NET Framework 4.6+、.NET Core 3.1、.NET 5、.NET 6 以及之後的版本。

**Q: 我要如何驗證遮蔽是否成功？**  
A: 使用 `Redactor.ValidateRedaction` 方法以確保沒有隱藏的文字殘留。

**Q: 能否批次處理資料夾中的 PDF？**  
A: 是的 – 迭代 `Directory.GetFiles`，並對每個檔案以非同步方式呼叫遮蔽例程。

## 資源

- [文件說明](https://docs.groupdocs.com/redaction/net/)
- [API 參考文件](https://reference.groupdocs.com/redaction/net)
- [下載](https://releases.groupdocs.com/redaction/net/)
- [免費支援](https://forum.groupdocs.com/c/redaction/33)
- [暫時授權](https://purchase.groupdocs.com/temporary-license/)

---

**最後更新：** 2026-10-11  
**測試環境：** GroupDocs.Redaction 23.12 for .NET  
**作者：** GroupDocs

## 相關教學

- [如何使用 GroupDocs.Redaction for .NET 遮蔽敏感資訊並移除註解](/redaction/net/annotation-redaction/remove-annotations-groupdocs-redaction-net/)
- [使用 GroupDocs.Redaction .NET：一步步指南](/redaction/net/getting-started/implement-document-redaction-groupdocs-redaction-net/)
- [如何使用 GroupDocs.Redaction for .NET 遮蔽 PDF 並儲存為光柵化 PDF](/redaction/net/document-saving/groupdocs-redaction-net-rasterized-pdfs/)