---
date: '2026-04-01'
description: 學習如何在 .NET 中使用 GroupDocs.Redaction 進行文件遮蔽。本教學涵蓋自訂格式處理程式、精確詞組遮蔽，以及如何安全地對法律合約進行遮蔽。
keywords:
- redact documents .net
- redact legal contracts
- GroupDocs.Redaction custom handler
title: 如何在 .NET 中使用 GroupDocs.Redaction 進行文件遮蔽 – 逐步指南
type: docs
url: /zh-hant/net/advanced-redaction/mastering-document-redaction-dotnet-groupdocs-redaction/
weight: 1
---

# 精通 .NET 中的文件遮蔽（Redaction）使用 GroupDocs.Redaction

## 介紹
在當今資料驅動的世界，快速且安全地 **redact documents .net** 已成為處理敏感資訊的開發者必備的技能。無論是保護法律合約中的客戶資料、在醫療紀錄中隱藏病患資訊，或是在報告中隱匿財務數字，可靠的遮蔽解決方案都能讓您的應用程式符合規範，並維護使用者的隱私。

GroupDocs.Redaction for .NET 提供完整的 API，讓您註冊自訂格式處理器，並在不轉換原始檔案格式的情況下執行精確片語遮蔽。本文將逐步說明如何有效 **redact documents .net**，從環境設定到實務案例皆有涵蓋。

### 快速答覆
- **哪個函式庫支援 .NET 遮蔽？** GroupDocs.Redaction for .NET  
- **可以遮蔽法律合約嗎？** 可以 – 使用精確片語遮蔽針對合約條款。  
- **生產環境需要授權嗎？** 需要商業授權才能使用完整功能。  
- **支援哪些 .NET 版本？** .NET Framework 4.5+、.NET Core 3.1+、.NET 5/6+。  
- **會保留原始文件的中繼資料嗎？** 會，精確片語遮蔽會保留中繼資料。

## 什麼是「redact documents .net」？
**redact documents .net** 指的是以程式方式在檔案中定位並移除或遮蔽敏感文字，同時保持文件其他部分不變。GroupDocs.Redaction 提供乾淨且高效能的 API，直接在 PDF、Word、純文字及其他多種格式上執行此操作。

## 為何使用 GroupDocs.Redaction 來遮蔽法律合約？
- **精準度** – 可針對精確片語或模式，特別適合合約條款。  
- **無格式轉換** – 保留原始版面與中繼資料，對法律合規至關重要。  
- **可擴充** – 可批次處理大量合約，且不會消耗過多記憶體。  

## 前置條件
在開始之前，請確保您已具備以下條件：

### 必要的函式庫與相依性
- **GroupDocs.Redaction for .NET** – 透過 .NET CLI 或 NuGet 套件管理員安裝。  
- **C# 開發環境** – 建議使用 Visual Studio（Community 或以上版本）。

### 環境設定需求
- .NET Framework 4.5+ **或** .NET Core/5+/6+。  
- 安裝 NuGet 套件時需要系統管理員權限（若有需要）。

### 知識前置條件
- 基本的 C# 語法與專案結構。  
- 了解文件處理概念（如檔案串流、文字搜尋）。

## 設定 GroupDocs.Redaction for .NET
要開始使用 GroupDocs.Redaction，必須先將函式庫加入專案。

**安裝步驟：**  
使用 **.NET CLI**，加入套件：
```bash
dotnet add package GroupDocs.Redaction
```

使用 **Package Manager**，執行：
```powershell
Install-Package GroupDocs.Redaction
```

或者在 Visual Studio 的 NuGet 套件管理員 UI 中，搜尋 **"GroupDocs.Redaction"** 並安裝最新版本。

### 授權取得
- **免費試用** – 無需授權即可評估核心功能。  
- **臨時授權** – 取得限時金鑰以測試完整功能。  
- **購買授權** – 取得商業授權以供正式上線使用。

**基本初始化：**  
```csharp
using GroupDocs.Redaction;

// Initialize Redactor with file path
Redactor redactor = new Redactor("path/to/your/document");
```
此程式碼示範如何建立 `Redactor` 實例，作為所有遮蔽操作的入口點。

## 實作指南
我們將實作分為兩個核心功能：**自訂格式處理器註冊** 與 **精確片語遮蔽**。兩者皆是處理包含專有或純文字格式的 **redact documents .net** 時不可或缺的步驟。

### 功能 1：自訂格式處理器註冊
#### 概觀
註冊自訂格式處理器可讓 GroupDocs.Redaction 知曉如何處理非標準檔案類型（例如 `.dump`）。當您需要 **redact legal contracts** 且檔案儲存於自訂文字格式時，此功能特別有用。

#### 實作步驟
##### 步驟 1：定義設定  
設定 GroupDocs.Redaction 所需的參數。
```csharp
using System;
using GroupDocs.Redaction.Configuration;

string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
var config = new DocumentFormatConfiguration()
{
    ExtensionFilter = ".dump",
    DocumentType = typeof(CustomTextualDocument)
};
```
- **ExtensionFilter** – 要處理的檔案副檔名。  
- **DocumentType** – 實作處理邏輯的自訂文件類別。

##### 步驟 2：註冊格式處理器  
將設定加入可用格式清單。
```csharp
RedactorConfiguration.GetInstance().AvailableFormats.Add(config);
```
現在任何 `.dump` 檔案在 `Redactor` 開啟時，都會使用 `CustomTextualDocument` 進行處理。

### 功能 2：遮蔽應用
#### 概觀
精確片語遮蔽讓您在不改變文件其他內容的前提下，精準定位並遮蔽特定字串（如合約條款）。

#### 實作步驟
##### 步驟 1：初始化 Redactor  
使用 `Redactor` 實例載入文件。
```csharp
using GroupDocs.Redaction;

string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
using (Redactor redactor = new Redactor(sourceFile))
{
    // Continue with redaction...
}
```

##### 步驟 2：套用精確片語遮蔽  
使用 `ExactPhraseRedaction` 取代目標文字。
```csharp
redactor.Apply(new ExactPhraseRedaction("dolor", false, new ReplacementOptions("[redacted]")));
```
- **"dolor"** – 您想要遮蔽的片語（請自行替換）。  
- **false** – 不分大小寫搜尋；若需區分大小寫請設為 `true`。  
- **ReplacementOptions** – 定義遮蔽後文字的外觀。

##### 步驟 3：儲存變更  
將遮蔽後的檔案寫入磁碟，必要時可變更格式。
```csharp
var outputFile = redactor.Save(new SaveOptions(false, "AnyText"));
```
`outputFile` 目前指向已儲存的遮蔽文件路徑。

## 實務應用
GroupDocs.Redaction 可整合至多種工作流程：

1. **法律文件管理** – 在與第三方共享前自動 **redact legal contracts**。  
2. **醫療資料保護** – 在醫療紀錄中遮蔽病患識別資訊。  
3. **財務報告** – 匿去個人與財務細節。  
4. **內部稽核** – 在外部審查前剔除專有資訊。

## 效能考量
- **分段處理** – 對於極大檔案，建議分段處理以降低記憶體使用。  
- **保持更新** – 新版常包含效能最佳化，請保持 NuGet 套件為最新。  
- **資源監控** – 在批次遮蔽時監測 CPU 與 RAM 使用，特別是在規格較低的伺服器上。

## 常見問題與解決方案
| 問題 | 原因 | 解決方案 |
|------|------|----------|
| **遮蔽未生效** | 大小寫敏感旗標設定錯誤 | 將 `ExactPhraseRedaction` 的第三個參數設為 `true` 以啟用大小寫敏感匹配。 |
| **輸出檔案損毀** | 使用了過時的 SaveOptions 設定 | 依照上方示範使用最新的 `SaveOptions` 建構子。 |
| **自訂格式未被識別** | 設定未加入 `AvailableFormats` | 確認在開啟檔案前已執行 `RedactorConfiguration.GetInstance().AvailableFormats.Add(config);`。 |

## 常見問答
**Q: 什麼是自訂格式處理器？**  
A: 它是一組設定，告訴 GroupDocs.Redaction 如何解讀與處理非標準檔案類型，從而在專有格式上執行遮蔽。

**Q: 可以在不改變文件中繼資料的情況下進行遮蔽嗎？**  
A: 可以。精確片語遮蔽會保留原始中繼資料，維持文件的稽核軌跡。

**Q: GroupDocs.Redaction 可以免費使用嗎？**  
A: 提供免費試用，但正式生產環境需購買授權才能使用完整功能。

**Q: 大小寫敏感如何影響遮蔽結果？**  
A: 設為 `true` 時僅匹配完全相同大小寫的文字；設為 `false` 時則不分大小寫，能捕捉更多變形。

**Q: 可以在商業應用中使用 GroupDocs.Redaction 嗎？**  
A: 當然可以。取得有效的商業授權後，即可在任何 .NET 產品中嵌入遮蔽功能。

## 資源
- [GroupDocs.Redaction for Net Documentation](https://docs.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction for Net API Reference](https://reference.groupdocs.com/redaction/net/)
- [Download GroupDocs.Redaction for Net](https://releases.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction Forum](https://forum.groupdocs.com/c/redaction/33)
- [Free Support](https://forum.groupdocs.com/)
- [Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**最後更新：** 2026-04-01  
**測試環境：** GroupDocs.Redaction 5.3 for .NET  
**作者：** GroupDocs  

---