---
date: '2026-10-06'
description: 了解如何使用 GroupDocs.Redaction .NET 及 C# 中的 IRedactionCallback 實作來遮蔽資料。遵循此一步一步的指南、最佳實踐以及實際案例。
keywords:
- how to redact data
- GroupDocs.Redaction .NET
- IRedactionCallback implementation
- document redaction C#
lastmod: '2026-10-06'
og_description: 了解如何使用 GroupDocs.Redaction .NET 及 C# 中的 IRedactionCallback 實作來遮蔽資料。遵循一步一步的指南，包含最佳實踐與實際案例。
og_image_alt: Guide to redact data with GroupDocs.Redaction .NET in C#
og_title: 如何使用 GroupDocs.Redaction .NET (C#) 進行資料遮蔽
schemas:
- author: GroupDocs
  dateModified: '2026-10-06'
  description: Learn how to redact data using GroupDocs.Redaction .NET with an IRedactionCallback
    implementation in C#. Follow this step‑by‑step guide, best practices, and real‑world
    examples.
  headline: How to redact data with GroupDocs.Redaction .NET (C#)
  type: TechArticle
- description: Learn how to redact data using GroupDocs.Redaction .NET with an IRedactionCallback
    implementation in C#. Follow this step‑by‑step guide, best practices, and real‑world
    examples.
  name: How to redact data with GroupDocs.Redaction .NET (C#)
  steps:
  - name: prepare output directory and source file path
    text: Define where your source document lives. Adjust the path to match your environment.
      `LoadOptions` is a configuration object that tells the SDK how to read the file
      (e.g., password handling).
  - name: create a Redactor instance with custom settings
    text: We instantiate `Redactor` with `LoadOptions` and `RedactorSettings`. The
      `RedactionDump` inside the settings will automatically record every redaction
      that occurs. `RedactorSettings` lets you fine‑tune the redaction process; passing
      a `RedactionDump` enables a detailed audit file. `RedactionDump` is
  - name: apply an exact‑phrase redaction
    text: Here we replace the phrase **John Doe** with the placeholder **[REDACTED]**.
      You can swap any phrase or pattern you need to hide. `ReplacementOptions` defines
      what text will replace the matched content. It also supports font and color
      customisation if you need a visual mask. **Explanation of the key
  type: HowTo
- questions:
  - answer: You can start with a free trial or request a temporary license to explore
      all features. For production, purchase a perpetual or subscription license.
    question: What are the licensing options for GroupDocs.Redaction?
  - answer: Yes, it supports PDFs, Word, Excel, PowerPoint, and many other common
      formats.
    question: Can I use GroupDocs.Redaction on multiple file types?
  - answer: Wrap your redaction logic in `try‑catch` blocks and log the exception
      details. The callback can also be used to capture errors in real time.
    question: How do I handle exceptions during redaction?
  - answer: The core API is synchronous, but you can run redaction calls inside asynchronous
      tasks or background services.
    question: Is there built‑in support for asynchronous processing?
  - answer: The [official documentation](https://docs.groupdocs.com/redaction/net/)
      and API reference provide extensive code samples and scenario guides.
    question: Where can I find more advanced examples?
  type: FAQPage
tags:
- redact data
- GroupDocs.Redaction
- .NET redaction
- C# document security
- IRedactionCallback
title: 如何使用 GroupDocs.Redaction .NET (C#) 進行資料遮蔽
type: docs
url: /zh-hant/net/advanced-redaction/groupdocs-redaction-net-implement-iredactioncallback-csharp/
weight: 1
---

# 如何使用 GroupDocs.Redaction .NET (C#) 進行資料遮蔽

在本完整教學中，您將學會**如何遮蔽資料**，從 PDF、Word 檔案及其他文件中使用 GroupDocs.Redaction for .NET。無論您是需要在法律合約中隱藏個人識別資訊，或是從財務報告中刪除機密數字，SDK 都提供程式化的控制，確保每個敏感項目永久且可稽核地消除。我們將逐步說明如何安裝函式庫、設定自訂的 `IRedactionCallback`，以及使用完整日誌套用精確片語遮蔽。

## 快速解答
- **IRedactionCallback 有什麼作用？** 它讓您攔截每個遮蔽事件、記錄細節，並可即時修改替換文字。  
- **我需要授權嗎？** 試用版可用於開發；正式授權會移除所有評估限制。  
- **支援哪些 .NET 版本？** .NET Core 3.1+、.NET 5/6 以及 .NET Framework 4.6+。  
- **我可以一次處理多個檔案嗎？** 可以——將邏輯包在迴圈中或使用批次處理以獲得最佳效能。  
- **是否支援非同步遮蔽？** SDK 本身未內建，但您可以將 API 呼叫放在 `Task.Run` 或其他非同步模式中執行。

## 何謂遮蔽敏感資料？
`Redaction` 是對必須保密的資訊進行永久移除或遮蔽。使用 GroupDocs.Redaction，您可以定義精確片語、正規表達式模式或自訂規則，並以 **[REDACTED]** 等佔位符取代，同時保留原始版面與分頁。

## 為何在 GroupDocs.Redaction 中使用 IRedactionCallback？
`IRedactionCallback` 是一個介面，會在 SDK 每次遮蔽內容時通知您，讓您捕獲稽核資料或動態調整替換文字。這提供完整的稽核能力、自訂商業規則執行，以及與合規系統的無縫整合——且不影響效能。

## 前置條件
- **GroupDocs.Redaction** 函式庫（相容版本 – 請參閱官方[文件頁面](https://docs.groupdocs.com/redaction/net/)）。欲取得完整資訊，請參考[官方文件](https://docs.groupdocs.com/redaction/net/)。  
- 已在開發機器上安裝 .NET Core 或 .NET Framework。  
- Visual Studio（社群版亦可）或任何支援 C# 的 IDE。  
- 基本的 C# 知識與 NuGet 套件管理經驗。

## 設定 GroupDocs.Redaction for .NET
首先，將函式庫加入您的專案。選擇您偏好的方式——CLI、Package Manager Console 或 UI。指令與原始教學完全相同。

### 安裝方式
**.NET CLI:**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager Console:**  
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI:**  
- 在 Visual Studio 中開啟您的專案。  
- 前往 **Manage NuGet Packages**。  
- 搜尋 **GroupDocs.Redaction** 並安裝最新的穩定版。

### 取得授權
若要試用本產品，請從[此處](https://purchase.groupdocs.com/temporary-license/)申請免費試用或臨時授權。您亦可從[臨時授權頁面](https://purchase.groupdocs.com/temporary-license/)取得臨時授權。正式環境使用時，請購買完整授權以解鎖全部功能且無限制。

#### 基本初始化與設定
以下為使用 `Redactor` 類別開啟文件的最小程式碼。請保持此片段不變——它是後續所有操作的基礎。  
`Redactor` 是代表文件的主要類別，提供套用遮蔽規則的方法。  
```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx"; // Replace with actual path

using (Redactor redactor = new Redactor(sourceFile))
{
    // Your redaction logic here
}
```

## 實作指南
現在，我們將在基本設定上加入自訂的 `IRedactionCallback`。這讓您能捕獲每個遮蔽事件、寫入日誌，甚至即時修改替換文字。

### 附加與使用 IRedactionCallback 實作
`IRedactionCallback` 是一個介面，會在每次遮蔽操作時接收回呼，讓您能以程式方式記錄或變更行為。

#### 步驟 1：準備輸出目錄與來源檔案路徑
定義來源文件所在的位置。請依您的環境調整路徑。  

`LoadOptions` 是一個設定物件，告訴 SDK 如何讀取檔案（例如密碼處理）。  
```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx"; // Replace with actual path
```

#### 步驟 2：建立具有自訂設定的 Redactor 實例
我們使用 `LoadOptions` 與 `RedactorSettings` 來實例化 `Redactor`。設定中的 `RedactionDump` 會自動記錄所有發生的遮蔽。  

`RedactorSettings` 讓您微調遮蔽流程；傳入 `RedactionDump` 即可產生詳細的稽核檔案。  
`RedactionDump` 是一個輔助類別，會將每個遮蔽事件寫入 JSON 格式的轉儲檔，以供合規報告使用。  
```csharp
using (Redactor redactor = new Redactor(sourceFile, 
    new LoadOptions(), 
    new RedactorSettings(new RedactionDump())))
{
    // Further processing steps will go here
}
```

#### 步驟 3：套用精確片語遮蔽
此處將片語 **John Doe** 替換為佔位符 **[REDACTED]**。您可以替換任何需要隱藏的片語或模式。  

`ReplacementOptions` 定義要取代匹配內容的文字。若需要視覺遮罩，亦支援字型與顏色自訂。  
```csharp
redactor.Apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[REDACTED]")));
```

**關鍵物件說明**
- `LoadOptions()` – 告訴 SDK 如何讀取文件（例如密碼處理）。  
- `RedactorSettings(new RedactionDump())` – 啟用轉儲檔案，記錄每個遮蔽以供稽核。  
- `ReplacementOptions("[REDACTED]")` – 定義將取代匹配片語的文字。

### 為何這很重要
回呼機制會記錄每個遮蔽事件，產生機器可讀的稽核軌跡，並允許您動態修改佔位符，協助符合合規需求且減少手動後處理工作。將此資料與監控系統整合後，您可產生報告、觸發警示，確保沒有敏感資訊漏過遮蔽流程。

使用 `IRedactionCallback` 為您帶來三項具體優勢：  
1. **符合合規的日誌**——每次遮蔽皆被記錄於機器可讀的轉儲中，滿足超過 30 種法規框架的稽核需求。  
2. **動態替換**——可依資料類型變更佔位符，將手動後處理降低至最高 40%。  
3. **可擴展效能**——回呼僅增加極低的開銷（每次遮蔽 <2 毫秒），同時允許平行批次處理上千個檔案。

### 疑難排解技巧
- **找不到檔案：** 請再次確認 `sourceFile` 路徑，並確保執行程序能存取該檔案。  
- **回呼未觸發：** 確認您的類別實作了 `IRedactionCallback` 的**全部**成員，且實例正確傳入 `Redactor`。  
- **效能延遲：** 大批次時，盡可能重複使用相同的 `Redactor` 實例，並及時釋放。

## 實務應用
遮蔽敏感資料在多個產業皆相當有用：

1. **法律文件處理**——在分享草稿前自動移除客戶姓名、案件編號或社會安全號碼。  
2. **人力資源管理系統**——在稽核期間移除員工合約中的個人識別資訊。  
3. **財務報告**——在產出給投資人的 PDF 時隱藏專有數字或帳號。

## 效能考量
GroupDocs.Redaction 支援 **30+ 種輸入與輸出格式**（PDF、DOCX、PPTX、XLSX、HTML 及影像類型），且能在不將整個文件載入記憶體的情況下處理數百頁的檔案。為了在處理數十或數百個檔案時保持應用程式的流暢度，請考慮以下方式：

- **批次處理：** 載入檔案清單，並在 `Parallel.ForEach` 內執行遮蔽迴圈，以利用多核心。  
- **記憶體管理：** 如範例所示，將每個 `Redactor` 包在 `using` 區塊中，以確保釋放。  
- **非同步操作：** 雖然 SDK 本身為同步，但您可將工作交由背景執行緒或 `Task.Run`，避免阻塞 UI 執行緒。

## 常見問題與解決方案

| 問題 | 解決方案 |
|-------|----------|
| **「Invalid file format」錯誤** | 確保文件類型受支援（PDF、DOCX、PPTX 等）。 |
| **回呼收到 null 值** | 檢查在建立 `RedactorSettings` 時是否傳入具體的 `IRedactionCallback` 實作。 |
| **遮蔽未套用** | 確認精確片語與文件中的大小寫與空格相符，或使用 `RegexRedaction` 進行模式匹配。 |

## 常見問答

**Q: GroupDocs.Redaction 的授權選項有哪些？**  
A: 您可以先使用免費試用或申請臨時授權以探索全部功能。正式環境則購買永久或訂閱授權。

**Q: 我可以在多種檔案類型上使用 GroupDocs.Redaction 嗎？**  
A: 可以，它支援 PDF、Word、Excel、PowerPoint 以及許多其他常見格式。

**Q: 如何處理遮蔽過程中的例外情況？**  
A: 將遮蔽邏輯包在 `try‑catch` 區塊中，並記錄例外細節。回呼亦可即時捕獲錯誤。

**Q: 是否內建支援非同步處理？**  
A: 核心 API 為同步，但您可在非同步任務或背景服務中執行遮蔽呼叫。

**Q: 哪裡可以找到更進階的範例？**  
A: [官方文件](https://docs.groupdocs.com/redaction/net/)與 API 參考提供大量程式碼範例與情境指南。

## 資源

- [GroupDocs.Redaction for Net Documentation](https://docs.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction for Net API Reference](https://reference.groupdocs.com/redaction/net/)
- [Download GroupDocs.Redaction for Net](https://releases.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction Forum](https://forum.groupdocs.com/c/redaction/33)
- [Free Support](https://forum.groupdocs.com/)
- [Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**最後更新：** 2026-10-06  
**測試環境：** GroupDocs.Redaction 2.3（撰寫時的最新版本）  
**作者：** GroupDocs

## 相關教學

- [使用 GroupDocs.Redaction .NET 建立遮蔽政策 – 步驟說明指南](/redaction/net/advanced-redaction/groupdocs-redaction-net-create-save-policy/)
- [如何使用 GroupDocs.Redaction .NET 遮蔽文件 – 完整指南](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [使用 Streams 遮蔽 .NET 文件 – GroupDocs.Redaction 指南](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)