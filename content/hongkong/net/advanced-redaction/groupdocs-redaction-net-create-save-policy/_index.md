---
date: '2026-10-06'
description: 了解如何使用 GroupDocs.Redaction .NET 遮蔽敏感資料。本分步指南將示範如何建立、套用及以 XML 格式儲存遮蔽政策。
keywords:
- redact sensitive data
- mask confidential information
- groupdocs redaction .net
lastmod: '2026-10-06'
og_description: 了解如何使用 GroupDocs.Redaction .NET 遮蔽敏感資料。本分步指南將示範如何建立、套用及以 XML 格式儲存遮蔽政策。
og_image_alt: Tutorial showing how to redact sensitive data in documents with GroupDocs.Redaction
  for .NET
og_title: 如何使用 GroupDocs.Redaction .NET 遮蔽敏感資料
schemas:
- author: GroupDocs
  dateModified: '2026-10-06'
  description: Learn how to redact sensitive data with GroupDocs.Redaction .NET. This
    step‑by‑step guide shows you how to create, apply, and save a redaction policy
    as XML.
  headline: How to redact sensitive data using GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to redact sensitive data with GroupDocs.Redaction .NET. This
    step‑by‑step guide shows you how to create, apply, and save a redaction policy
    as XML.
  name: How to redact sensitive data using GroupDocs.Redaction .NET
  steps:
  - name: prepare your document directory
    text: '*Replace `"YOUR_DOCUMENT_DIRECTORY"` with the folder that holds the documents
      you want to protect.*'
  - name: load the document
    text: The `Redactor` object opens the file and manages its lifecycle.
  - name: define the redactions
    text: 'ExactPhraseRedaction defines a rule that replaces a specific phrase, while
      `RegexRedaction` uses a regular expression to match patterns. Here we create
      two rules: 1. **ExactPhraseRedaction** – replaces a known phrase with “[REDACTED]”.
      2. **RegexRedaction** – finds dates in `YYYY‑MM‑DD` format and r'
  - name: apply the redactions
    text: All defined rules are executed against the opened document in one pass.
  - name: save the policy as an XML file
    text: The XML file stores the redaction definitions, allowing you to reuse the
      same policy without rewriting code.
  type: HowTo
- questions:
  - answer: Yes—use `redactor.LoadPolicy("policy.xml")` to import a previously saved
      policy.
    question: Can I load an existing XML policy instead of building one programmatically?
  - answer: 'Absolutely. Pass the password to the `Redactor` constructor: `new Redactor(sourceFile,
      "password")`.'
    question: Does GroupDocs.Redaction support password‑protected PDFs?
  - answer: The SDK provides `ImageRedaction` and `MetadataRedaction` classes for
      those scenarios.
    question: Is it possible to redact images or metadata?
  - answer: Process them in chunks or use the streaming API to reduce memory footprint;
      the engine can handle files up to 2 GB without loading the whole file into RAM.
    question: How do I handle large documents (hundreds of MB)?
  - answer: A paid license is required for production deployments; a trial license
      is fine for development and testing.
    question: What licensing model is required for commercial use?
  type: FAQPage
tags:
- redact sensitive data
- groupdocs redaction
- .net document security
- xml policy
- document redaction
title: 如何使用 GroupDocs.Redaction .NET 遮蔽敏感資料
type: docs
url: /zh-hant/net/advanced-redaction/groupdocs-redaction-net-create-save-policy/
weight: 1
---

# 如何使用 GroupDocs.Redaction .NET 遮蔽敏感資料

在合約、財務報表或病歷等文件中保護機密資訊是現代應用程式的必須條件。本指南將教您如何使用 GroupDocs.Redaction for .NET **遮蔽敏感資料**，從安裝 SDK 到定義可重複使用的 XML 政策，適用於任何文件類型。

## 快速解答
- **「create redaction policy」是什麼意思？** 這是定義規則（文字、正規表達式、影像等）的過程，告訴 GroupDocs.Redaction 如何隱藏或取代機密內容。  
- **我需要哪個函式庫？** GroupDocs.Redaction for .NET，可透過 NuGet 取得。  
- **我需要授權嗎？** 免費試用可用於開發；正式環境需購買永久授權。  
- **我可以重複使用政策嗎？** 可以——將政策儲存為 XML 後，可在之後載入並套用至任何文件。  
- **支援哪些 .NET 版本？** .NET Framework 4.5+、.NET Core 3.1+、.NET 5/6/7。

## 什麼是遮蔽政策？

遮蔽政策是一組規則的集合，用於指定 *要移除或取代什麼* 以及 *取代的樣式*。只要建立一次政策，即可對應用程式處理的每份文件套用一致的安全標準。

## 遮蔽政策如何運作？

使用 `Redactor` 引擎載入文件，附加一個或多個遮蔽規則，然後呼叫 `Apply`。引擎會掃描文件，遮蔽符合的內容，並可選擇輸出新檔案。同一組規則可匯出為 XML，讓您在不重新編譯程式碼的情況下重複使用政策。

## 為何使用 GroupDocs.Redaction 來建立遮蔽政策？

GroupDocs.Redaction 提供完整的功能集合，簡化遮蔽政策的建立、管理與執行，確保在各種文件類型間提供一致的資料保護，同時具備高效能，且易於整合至現有的 .NET 應用程式，適合團隊與組織使用。

- **廣泛的格式支援** – SDK 可處理超過 30 種檔案類型，包括 PDF、DOCX、XLSX、PPTX 以及影像格式，且可在不將整個檔案載入記憶體的情況下處理高達 2 GB 的檔案。  
- **程式化的精準度** – 定義精確的片語、正規表達式或自訂邏輯，只針對需要遮蔽的資料。  
- **可重複使用的 XML 政策** – 一次匯出規則，即可在團隊、服務或微服務間共享。  
- **效能優化的引擎** – 此函式庫在一般伺服器硬體上可於一秒內處理數百頁的文件，適用於高吞吐量的工作流程。

## 前置條件
- 與您的 .NET 執行環境相容的 GroupDocs.Redaction 函式庫。  
- Visual Studio、VS Code 或任何支援 C# 的 IDE。  
- 具備 C# 與 .NET 專案結構的基本知識。

## 設定 GroupDocs.Redaction for .NET

首先，將函式庫加入您的專案。

**使用 .NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**使用套件管理員**  
```powershell
Install-Package GroupDocs.Redaction
```  

或在 NuGet 套件管理員 UI 中搜尋 “GroupDocs.Redaction”，並從那裡安裝。

### 授權取得
- 先使用 **免費試用** 來探索功能。  
- 申請 **臨時授權** 以進行延長測試，之後購買正式授權以供生產環境使用。

### 基本初始化
在您的來源檔案中加入命名空間：

The `Redactor` class is the core engine that loads a document and applies redaction rules.  
```csharp
using GroupDocs.Redaction;
```  

`Redactor` 類別是核心引擎，用於載入文件並套用遮蔽規則。  
The `Redactor` class is GroupDocs.Redaction's core engine that loads a document and applies redaction rules.

## 如何一步步建立遮蔽政策

以下是一個完整的操作說明，示範如何以程式方式建立遮蔽政策、設定規則、套用至文件，最後將政策保存為 XML 檔以供未來重複使用，確保在多個專案與文件類型間保持一致的遮蔽效果。

### 步驟 1：準備文件目錄
```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
```  
*將 `"YOUR_DOCUMENT_DIRECTORY"` 替換為存放您欲保護文件的資料夾。*

### 步驟 2：載入文件
```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // Further code will go here
}
```  
`Redactor` 物件會開啟檔案並管理其生命週期。

### 步驟 3：定義遮蔽規則
ExactPhraseRedaction 定義一個取代特定片語的規則，而 `RegexRedaction` 使用正規表達式來匹配模式。  
```csharp
var redactions = new List<Redaction>
{
    new ExactPhraseRedaction("Sensitive Phrase", new ReplacementOptions("[REDACTED]")),
    new RegexRedaction(@"\d{4}-\d{2}-\d{2}", new ReplacementOptions("[DATE REDACTED]"))
};
```  
此處我們建立兩個規則：
1. **ExactPhraseRedaction** – 將已知片語取代為 “[REDACTED]”。  
2. **RegexRedaction** – 找出 `YYYY‑MM‑DD` 格式的日期，並取代為 “[DATE REDACTED]”。

### 步驟 4：套用遮蔽規則
```csharp
redactor.Apply(redactions);
```  
所有已定義的規則會在一次處理中對已開啟的文件執行。

### 步驟 5：將政策保存為 XML 檔
```csharp
string policyFile = "policy.xml";
redactor.SavePolicy(policyFile, new SaveOptions());
```  
XML 檔案儲存遮蔽定義，讓您無需重新編寫程式碼即可重複使用相同的政策。

## 實務應用

- **法律事務所** 可在分享草稿前遮蔽案件編號與客戶姓名。  
- **財務部門** 在報告中遮蔽帳號或交易日期。  
- **醫療機構** 透過移除患者識別資訊以確保符合 HIPAA 規範。

## 效能建議

- 同時僅 **開啟一份文件**，以降低記憶體使用量。  
- 撰寫 **高效的正規表達式**；避免過於寬鬆的模式，以免增加處理時間。  
- 保持函式庫 **最新**，以獲得效能提升與新遮蔽類型的支援。

## 常見問題與解決方案

| 問題 | 發生原因 | 解決方法 |
|------|----------|----------|
| **準備目錄時的 IO 例外** | 路徑錯誤或缺少寫入權限 | 確認資料夾存在且應用程式具備讀寫權限。 |
| **正規表達式未匹配預期文字** | 模式過於嚴格或缺少跳脫字元 | 使用線上測試工具測試正規表達式；調整量詞或跳脫特殊字元。 |
| **政策檔未建立** | `SavePolicy` 在套用遮蔽前被呼叫，或路徑無效 | 確保輸出目錄可寫，並在 `Apply` 後呼叫 `SavePolicy`。 |

## 常見問答

**問：我可以載入已存在的 XML 政策，而不是以程式方式建立嗎？**  
答：可以——使用 `redactor.LoadPolicy("policy.xml")` 匯入先前儲存的政策。

**問：GroupDocs.Redaction 支援受密碼保護的 PDF 嗎？**  
答：當然支援。將密碼傳入 `Redactor` 建構子，例如 `new Redactor(sourceFile, "password")`。

**問：可以遮蔽影像或中繼資料嗎？**  
答：SDK 提供 `ImageRedaction` 與 `MetadataRedaction` 類別以應對此類情況。

**問：如何處理大型文件（數百 MB）？**  
答：可分塊處理或使用串流 API 以減少記憶體佔用；引擎可在不將整個檔案載入記憶體的情況下處理高達 2 GB 的檔案。

**問：商業使用需要什麼授權模式？**  
答：正式部署需購買付費授權；開發與測試階段可使用試用授權。

## 結論

您現在已擁有完整且可重複使用的 **遮蔽政策**，可使用 GroupDocs.Redaction for .NET 套用於任何文件。將政策匯出為 XML 後，可簡化未來的更新，並確保整個組織的資料保護一致性。

### 後續步驟
- 嘗試其他遮蔽類型，例如 `ImageRedaction` 或 `MetadataRedaction`。  
- 將政策載入邏輯整合至文件管理工作流程，以實現自動遮蔽。  
- 探索 **GroupDocs.Redaction** API 參考文件，以進行進階客製化。

---

**Last Updated:** 2026-10-06  
**Tested With:** GroupDocs.Redaction 5.8 for .NET  
**Author:** GroupDocs  

**資源**  
- [Documentation](https://docs.groupdocs.com/redaction/net/)  
- [API Reference](https://reference.groupdocs.com/redaction/net)  
- [Download](https://releases.groupdocs.com/redaction/net/)  
- [Free Support Forum](https://forum.groupdocs.com/c/redaction/33)  
- [Temporary License Application](https://purchase.groupdocs.com/temporary-license/)

## 相關教學

- [使用 GroupDocs.Redaction .NET (C#) 遮蔽敏感資料](/redaction/net/advanced-redaction/groupdocs-redaction-net-implement-iredactioncallback-csharp/)  
- [使用 GroupDocs.Redaction .NET 實作文件遮蔽：一步一步指南](/redaction/net/getting-started/implement-document-redaction-groupdocs-redaction-net/)  
- [如何使用 GroupDocs.Redaction .NET 遮蔽文件 – 完整指南](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)