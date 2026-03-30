---
date: '2026-03-30'
description: 學習如何在 .NET 中使用 GroupDocs.Redaction 建立遮蔽政策。本教學將示範如何建構、套用及將遮蔽政策儲存為 XML
  檔案。
keywords:
- GroupDocs.Redaction .NET
- create redaction policy
- save XML policy
title: 使用 GroupDocs.Redaction .NET 建立遮蔽政策 – 逐步指引
type: docs
url: /zh-hant/net/advanced-redaction/groupdocs-redaction-net-create-save-policy/
weight: 1
---

# 使用 GroupDocs.Redaction .NET 建立遮蔽政策

在現代應用程式中，保護文件內的機密資料是必備的安全措施。無論您處理合約、財務報表或病人紀錄，通常都需要**建立遮蔽政策**，自動遮蔽或移除敏感資訊。本指南將帶您完整走過整個流程——安裝程式庫、定義遮蔽、套用遮蔽，最後將政策儲存為 XML 檔案，以便在不同專案中重複使用。

## 快速解答
- **「建立遮蔽政策」是什麼意思？** 它是定義規則（文字、正則表達式、圖像等）的過程，告訴 GroupDocs.Redaction 如何隱藏或取代機密內容。  
- **我需要哪個程式庫？** GroupDocs.Redaction for .NET（可透過 NuGet 取得）。  
- **我需要授權嗎？** 免費試用可用於開發；正式環境需要永久授權。  
- **我可以重複使用此政策嗎？** 可以——儲存為 XML 後，您可以稍後載入並套用於任何文件。  
- **支援哪些 .NET 版本？** .NET Framework 4.5 以上、.NET Core 3.1 以上、.NET 5/6/7。

## 什麼是遮蔽政策？

遮蔽政策是一組規則的集合，指定*要*移除或取代的內容以及*取代後*的顯示方式。只要建立一次政策，即可在應用程式處理的每份文件上套用一致的安全標準。

## 為什麼使用 GroupDocs.Redaction 來建立遮蔽政策？

- **完整文件格式支援** – Word、PDF、Excel、PowerPoint 等多種格式。  
- **程式化控制** – 定義精確片語、正則表達式，甚至自訂邏輯。  
- **可重複使用的 XML 政策** – 將規則匯出一次，即可在團隊或服務間共享。  
- **效能優化的引擎** – 高效處理大型檔案，並能隨工作負載擴展。

## 前置條件

- **GroupDocs.Redaction** 程式庫（相容於您的 .NET 執行環境）。  
- Visual Studio、VS Code 或任何支援 C# 的 IDE。  
- 具備 C# 與 .NET 專案結構的基本知識。

## 設定 GroupDocs.Redaction for .NET

首先，將程式庫加入您的專案。

**使用 .NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**使用套件管理員**  
```powershell
Install-Package GroupDocs.Redaction
```

或在 NuGet 套件管理員 UI 中搜尋「GroupDocs.Redaction」並從那裡安裝。

### 取得授權
- 先使用**免費試用**來探索功能。  
- 申請**臨時授權**以進行更長時間的測試，之後購買正式授權以供生產環境使用。

### 基本初始化
在您的原始檔案中加入命名空間：

```csharp
using GroupDocs.Redaction;
```

## 如何使用 GroupDocs.Redaction .NET 建立遮蔽政策

以下為逐步說明，展示如何建立並保存遮蔽政策。

### 步驟 1：準備文件目錄
```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
```
*將 `"YOUR_DOCUMENT_DIRECTORY"` 替換為保存您欲保護文件的資料夾路徑。*

### 步驟 2：載入文件
```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // Further code will go here
}
```
`Redactor` 物件會開啟檔案並管理其生命週期。

### 步驟 3：定義遮蔽
```csharp
var redactions = new List<Redaction>
{
    new ExactPhraseRedaction("Sensitive Phrase", new ReplacementOptions("[REDACTED]")),
    new RegexRedaction(@"\d{4}-\d{2}-\d{2}", new ReplacementOptions("[DATE REDACTED]"))
};
```
此處我們建立兩條規則：
1. **ExactPhraseRedaction** – 將已知片語替換為「[REDACTED]」。  
2. **RegexRedaction** – 找出 `YYYY‑MM‑DD` 格式的日期，並替換為「[DATE REDACTED]」。

### 步驟 4：套用遮蔽
```csharp
redactor.Apply(redactions);
```
所有已定義的規則會一次性套用於已開啟的文件。

### 步驟 5：將政策儲存為 XML 檔案
```csharp
string policyFile = "policy.xml";
redactor.SavePolicy(policyFile, new SaveOptions());
```
此 XML 檔案保存遮蔽定義，讓您無需重新編寫程式碼即可重複使用相同的政策。

## 實務應用

- **法律事務所** 可在分享草稿前遮蔽案件編號與客戶姓名。  
- **財務部門** 在報告中遮蔽帳號或交易日期。  
- **醫療機構** 透過移除患者識別資訊以確保符合 HIPAA 規範。

## 效能建議

- 同時僅**開啟一份文件**以降低記憶體使用量。  
- 撰寫**高效的正則表達式**；避免過於寬鬆的模式以免增加處理時間。  
- 保持程式庫**最新**，以獲得效能提升與新遮蔽類型。

## 常見問題與解決方案

| 問題 | 發生原因 | 解決方法 |
|-------|----------------|------------|
| **準備目錄時的 IO 例外** | 路徑錯誤或缺少寫入權限 | 確認資料夾存在且應用程式具備讀寫權限。 |
| **正則表達式未匹配預期文字** | 模式過於嚴格或缺少跳脫字元 | 使用線上測試工具測試正則表達式；調整量詞或跳脫特殊字元。 |
| **政策檔案未建立** | `SavePolicy` 在套用遮蔽之前呼叫，或路徑無效 | 確保輸出目錄可寫，且在 `Apply` 後呼叫 `SavePolicy`。 |

## 常見問答

**Q: 我可以載入已存在的 XML 政策，而不是以程式方式建立嗎？**  
A: 可以——使用 `redactor.LoadPolicy("policy.xml")` 來匯入先前儲存的政策。

**Q: GroupDocs.Redaction 支援受密碼保護的 PDF 嗎？**  
A: 當然支援。將密碼傳入 `Redactor` 建構子：`new Redactor(sourceFile, "password")`。

**Q: 可以遮蔽圖像或中繼資料嗎？**  
A: 程式庫提供 `ImageRedaction` 與 `MetadataRedaction` 類別以應對此類情況。

**Q: 如何處理大型文件（數百 MB）？**  
A: 將其分塊處理或使用串流 API 以減少記憶體佔用；若遇到 OutOfMemory 錯誤，也可考慮增加 JVM 堆積大小。

**Q: 商業使用需要什麼授權模式？**  
A: 正式部署需購買授權；開發與測試階段可使用試用授權。

## 結論

您現在擁有完整且可重複使用的**遮蔽政策**，可透過 GroupDocs.Redaction for .NET 套用於任何文件。將政策匯出為 XML 可簡化未來的更新，並確保整個組織的資料保護一致性。

### 後續步驟
- 嘗試其他遮蔽類型，例如 `ImageRedaction` 或 `MetadataRedaction`。  
- 將政策載入邏輯整合至文件管理工作流程，以實現自動遮蔽。  
- 探索 **GroupDocs.Redaction** API 參考文件，以進行進階客製化。

---

**最後更新：** 2026-03-30  
**測試環境：** GroupDocs.Redaction 5.8 for .NET  
**作者：** GroupDocs  

**資源**  
- [文件說明](https://docs.groupdocs.com/redaction/net/)  
- [API 參考](https://reference.groupdocs.com/redaction/net)  
- [下載](https://releases.groupdocs.com/redaction/net/)  
- [免費支援論壇](https://forum.groupdocs.com/c/redaction/33)  
- [臨時授權申請](https://purchase.groupdocs.com/temporary-license/)