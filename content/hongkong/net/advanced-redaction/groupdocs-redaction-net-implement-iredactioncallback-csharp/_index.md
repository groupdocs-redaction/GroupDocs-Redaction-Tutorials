---
date: '2026-03-30'
description: 學習如何使用 GroupDocs.Redaction .NET 及 C# 中的 IRedactionCallback 實作來隱匿敏感資料。一步一步的指南、最佳實踐與實際案例。
keywords:
- GroupDocs.Redaction .NET
- Implementing IRedactionCallback
- secure document redaction
title: 使用 GroupDocs.Redaction .NET (C#) 隱去敏感資料
type: docs
url: /zh-hant/net/advanced-redaction/groupdocs-redaction-net-implement-iredactioncallback-csharp/
weight: 1
---

# 使用 GroupDocs.Redaction .NET (C#) 進行敏感資料遮蔽

在當今的數位環境中，**遮蔽敏感資料**於法律、金融或人力資源文件是不可協商的需求。無論您是為外部審查準備合約，或在公開發佈前清理報告，遺漏任何個人識別資訊都可能導致合規違規。GroupDocs.Redaction for .NET 為您提供強大且可程式化的方式，確保每一筆機密資訊都能以您所需的方式徹底消除。在本教學中，我們將示範如何附加 `IRedactionCallback` 實作，讓您自訂遮蔽工作流程，並全面掌控每一步。

## 快速解答
- **IRedactionCallback 的功能是什麼？** 它讓您即時攔截遮蔽事件、記錄日誌，或動態修改行為。  
- **我需要授權嗎？** 試用版可用於開發；永久授權會移除所有評估限制。  
- **支援哪些 .NET 版本？** .NET Core 3.1+、.NET 5/6 以及 .NET Framework 4.6+。  
- **我可以一次處理多個檔案嗎？** 可以——將邏輯包在迴圈中或使用批次處理以獲得最佳效能。  
- **是否支援非同步遮蔽？** SDK 本身未內建，但您可以將 API 呼叫放在 `Task.Run` 或其他非同步模式中執行。  

## 什麼是遮蔽敏感資料？
遮蔽是永久移除或隱蔽必須不被揭露的資訊的過程。使用 GroupDocs.Redaction，您可以定義精確的片語、模式或自訂規則，並以佔位符（例如 **[REDACTED]**）取代，同時保留原始文件的版面配置。

## 為何在 GroupDocs.Redaction 中使用 IRedactionCallback？
- **完整稽核能力：** 回呼會提供每一次遮蔽操作的詳細日誌。  
- **自訂處理：** 替換文字、觸發外部服務，或動態執行業務規則。  
- **可擴展效能：** 結合回呼與批次處理，可有效處理成千上萬的檔案。  

## 前置條件
在深入之前，請確保您已具備：

- **GroupDocs.Redaction** 函式庫（相容版本 – 請參閱官方[文件頁面](https://docs.groupdocs.com/redaction/net/)）。  
- 已在開發機器上安裝 .NET Core 或 .NET Framework。  
- Visual Studio（社群版亦可）或任何支援 C# 的 IDE。  
- 基本的 C# 知識以及熟悉 NuGet 套件管理。  

## 設定 GroupDocs.Redaction for .NET
首先，將函式庫加入您的專案。選擇您偏好的方式——CLI、Package Manager Console 或 UI。指令與原始教學完全相同。

### 安裝方式
**.NET CLI：**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager Console：**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet 套件管理員 UI：**
- 在 Visual Studio 中開啟您的專案。  
- 前往 **Manage NuGet Packages**。  
- 搜尋 **GroupDocs.Redaction** 並安裝最新的穩定版本。  

### 取得授權
若要試用此產品，請從[此處](https://purchase.groupdocs.com/temporary-license/)申請免費試用或臨時授權。正式上線時，購買完整授權即可解除所有功能限制。

#### 基本初始化與設定
以下是使用 `Redactor` 類別開啟文件所需的最小程式碼。請保持此片段不變——它是後續所有操作的基礎。

```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx"; // Replace with actual path

using (Redactor redactor = new Redactor(sourceFile))
{
    // Your redaction logic here
}
```

## 實作指南
現在，我們將在基本設定上加入自訂的 `IRedactionCallback`。這讓您能捕捉每一次遮蔽事件、寫入日誌，甚至即時修改取代文字。

### 附加與使用 IRedactionCallback 實作
以下步驟展示完整工作流程，從準備檔案路徑到套用精確片語遮蔽。

#### 步驟 1：準備輸出目錄與來源檔案路徑
定義來源文件所在位置。請依您的環境調整路徑。

```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx"; // Replace with actual path
```

#### 步驟 2：使用自訂設定建立 Redactor 實例
我們以 `LoadOptions` 與 `RedactorSettings` 來實例化 `Redactor`。設定中的 `RedactionDump` 會自動記錄所有發生的遮蔽。

```csharp
using (Redactor redactor = new Redactor(sourceFile, 
    new LoadOptions(), 
    new RedactorSettings(new RedactionDump())))
{
    // Further processing steps will go here
}
```

#### 步驟 3：套用精確片語遮蔽
此處我們將片語 **John Doe** 替換為佔位符 **[REDACTED]**。您可以替換任何需要隱藏的片語或模式。

```csharp
redactor.Apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[REDACTED]")));
```

**關鍵物件說明：**
- `LoadOptions()` – 告訴 SDK 如何讀取文件（例如密碼處理）。  
- `RedactorSettings(new RedactionDump())` – 啟用一個轉儲檔案，用於記錄每一次遮蔽以供稽核。  
- `ReplacementOptions("[REDACTED]")` – 定義將取代匹配片語的文字。  

### 為何這很重要
透過使用 `IRedactionCallback`，您可以插入自訂邏輯，例如：
- 將遮蔽細節傳送至合規資料庫。  
- 隱蔽簡單片語取代未涵蓋的其他中繼資料。  
- 根據內容類型動態選擇取代文字。  

### 疑難排解技巧
- **找不到檔案：** 請再次確認 `sourceFile` 路徑，並確保執行程序能存取該檔案。  
- **回呼未觸發：** 確認您的類別實作了 `IRedactionCallback` 的**所有**成員，且實例正確傳遞給 `Redactor`。  
- **效能延遲：** 大量批次時，盡可能重複使用相同的 `Redactor` 實例，並及時釋放。  

## 實務應用
遮蔽敏感資料在多個產業皆相當有用：
1. **法律文件處理** – 在分享草稿前自動移除客戶姓名、案件編號或社會安全號碼。  
2. **人力資源管理系統** – 在審計期間移除員工合約中的個人識別資訊。  
3. **財務報告** – 產生面向投資者的 PDF 時隱蔽專有數字或帳號。  

## 效能考量
為了在處理數十或數百個檔案時保持應用程式的流暢度：
- **批次處理：** 載入檔案清單，並在 `Parallel.ForEach` 中執行遮蔽迴圈，以利用多核心。  
- **記憶體管理：** 如示範般將每個 `Redactor` 包在 `using` 區塊中，以確保釋放。  
- **非同步操作：** 雖然 SDK 本身為同步，但您可將工作移至背景執行緒或 `Task.Run`，以避免阻塞 UI 執行緒。  

## 常見問題與解決方案
| 問題 | 解決方案 |
|-------|----------|
| **「無效的檔案格式」錯誤** | 確保文件類型受支援（如 PDF、DOCX、PPTX 等）。 |
| **回呼收到 null 值** | 檢查在建立 `RedactorSettings` 時是否傳入了 `IRedactionCallback` 的具體實作。 |
| **遮蔽未套用** | 確認精確片語的大小寫與空格與文件相符，或使用 `RegexRedaction` 進行模式匹配。 |

## 常見問與答

**Q: GroupDocs.Redaction 的授權選項有哪些？**  
A: 您可以先使用免費試用或申請臨時授權以探索所有功能。正式環境則需購買永久或訂閱授權。

**Q: 我可以在多種檔案類型上使用 GroupDocs.Redaction 嗎？**  
A: 可以，它支援 PDF、Word、Excel、PowerPoint 以及許多其他常見格式。

**Q: 在遮蔽過程中如何處理例外情況？**  
A: 將遮蔽邏輯包在 `try‑catch` 區塊中，並記錄例外細節。回呼亦可即時捕捉錯誤。

**Q: 是否內建支援非同步處理？**  
A: 核心 API 為同步，但您可在非同步任務或背景服務中執行遮蔽呼叫。

**Q: 在哪裡可以找到更進階的範例？**  
A: 請參閱[官方文件](https://docs.groupdocs.com/redaction/net/)與 API 參考，內含豐富的程式碼範例與情境指南。

## 資源

- [GroupDocs.Redaction for Net 文件](https://docs.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction for Net API 參考](https://reference.groupdocs.com/redaction/net/)
- [下載 GroupDocs.Redaction for Net](https://releases.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction 論壇](https://forum.groupdocs.com/c/redaction/33)
- [免費支援](https://forum.groupdocs.com/)
- [臨時授權](https://purchase.groupdocs.com/temporary-license/)

---

**最後更新：** 2026-03-30  
**測試版本：** GroupDocs.Redaction 2.3（撰寫時的最新版本）  
**作者：** GroupDocs