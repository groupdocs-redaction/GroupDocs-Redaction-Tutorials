---
date: 2026-07-15
description: 了解如何使用 GroupDocs.Redaction for .NET 建立自訂遮蔽處理程式並新增檔案格式支援。
keywords:
- create custom redaction handler
- add new file format
- GroupDocs.Redaction format handling
lastmod: 2026-07-15
og_description: 使用 GroupDocs.Redaction for .NET 建立自訂遮蔽處理程式並新增檔案格式支援。探索延伸格式處理的逐步指南。
og_image_alt: Guide to creating a custom redaction handler in GroupDocs.Redaction
  for .NET
og_title: 建立自訂遮蔽處理程式 – GroupDocs.Redaction .NET
schemas:
- author: GroupDocs
  dateModified: '2026-07-15'
  description: Learn how to create custom redaction handler and add new file format
    support using GroupDocs.Redaction for .NET.
  headline: Create Custom Redaction Handler in GroupDocs.Redaction .NET
  type: TechArticle
tags:
- redaction handler
- GroupDocs.Redaction
- .NET document processing
- custom format extension
title: 在 GroupDocs.Redaction .NET 中建立自訂遮蔽處理程式
type: docs
url: /zh-hant/net/format-handling/
weight: 14
---

# 在 GroupDocs.Redaction .NET 中建立自訂遮蔽處理程式

擴充 GroupDocs.Redaction 功能，透過我們為 .NET 開發人員提供的格式處理教學。在此中心您將學習如何 **建立自訂遮蔽處理程式** 與 **新增檔案格式** 支援、處理純文字文件，並以程式方式處理各種文件類型。這些指南包含可直接執行的 C# 範例，讓您快速擴大應用程式可保護的檔案範圍。

## 快速概覽

- **What you’ll gain:** 能夠遮蔽自訂內容類型並支援額外的檔案副檔名，無需等待產品更新。  
- **Who it’s for:** 為需要嚴格隱私控制的文件為中心解決方案的 .NET 開發人員。  
- **Prerequisites:** .NET 6+（或 .NET Framework 4.7.2+）、有效的 GroupDocs.Redaction 授權，以及基本的 C# 知識。  

## 什麼是自訂遮蔽處理程式？

**custom redaction handler** 是一個使用者自訂的元件，告訴 GroupDocs.Redaction 如何定位、解讀以及遮蔽未被內建模式涵蓋的內容。透過實作此處理程式，您即可完全掌控專有資料格式或獨特的業務識別碼。

## 如何建立自訂遮蔽處理程式？

**IRedactionHandler** 是一個定義自訂遮蔽邏輯合約的介面。  
**Redactor** 是管理遮蔽操作的核心類別。  
**AddHandler** 用於在 Redactor 實例中註冊自訂處理程式。  
**Redact** 依據已設定的處理程式執行遮蔽。  

載入 Redaction 引擎、註冊您的處理程式，並呼叫遮蔽程序——全部只需三個簡潔步驟。首先，實作 `IRedactionHandler` 介面，加入掃描文件中自訂標記的邏輯。接著，透過 `AddHandler` 將處理程式加入 `Redactor` 實例。最後，呼叫 `Redact` 套用變更。此模式適用於 PDF、影像以及任何支援的格式，讓您能保護標準模式無法偵測的資料。

## 如何新增檔案格式？

**SupportedFormats** 是一個保存 Redaction 引擎可辨識檔案副檔名的集合。透過擴充 `SupportedFormats` 集合，可向 Redaction 引擎註冊新檔案副檔名。提供一個解析器，將輸入檔案轉換為 GroupDocs.Redaction 可處理的格式，然後將副檔名對應至您的解析器。註冊後，引擎會將新格式視為原生類型，實現全域無縫的遮蔽。

## 為何使用 GroupDocs.Redaction 進行自訂格式處理？

GroupDocs.Redaction 支援 **70+ 輸入與輸出格式**，且可在不將整個文件載入記憶體的情況下處理高達 **2 GB** 的檔案，提供企業環境下高吞吐量的遮蔽。其可擴充的架構讓您在 30 分鐘內即能插入自訂處理程式，縮短開發時間，並免除第三方前置處理工具的需求。

## 可用教學

### [在 GroupDocs.Redaction .NET 中擴充檔案類型：自訂擴充功能的逐步指南](./extend-groupdocs-redaction-net-custom-extensions/)
了解如何使用 GroupDocs.Redaction for .NET 透過自訂擴充功能擴充支援的檔案類型，確保在各種格式下安全的文件遮蔽。

### [使用 GroupDocs.Redaction .NET 實作支援檔案格式清單](./groupdocs-redaction-net-supported-formats-listing/)
了解如何使用 GroupDocs.Redaction .NET 列出支援的檔案格式，簡化文件管理系統，並優化效能。

## 其他資源

- [GroupDocs.Redaction for Net 文件說明](https://docs.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction for Net API 參考](https://reference.groupdocs.com/redaction/net/)
- [下載 GroupDocs.Redaction for Net](https://releases.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction 論壇](https://forum.groupdocs.com/c/redaction/33)
- [免費支援](https://forum.groupdocs.com/)
- [臨時授權](https://purchase.groupdocs.com/temporary-license/)

---

**最後更新：** 2026-07-15  
**測試環境：** GroupDocs.Redaction 23.12 for .NET  
**作者：** GroupDocs

## 相關教學

- [在 GroupDocs.Redaction .NET 中擴充檔案類型：自訂擴充功能的逐步指南](/redaction/net/format-handling/extend-groupdocs-redaction-net-custom-extensions/)
- [使用 GroupDocs.Redaction .NET 實作支援檔案格式清單](/redaction/net/format-handling/groupdocs-redaction-net-supported-formats-listing/)
- [GroupDocs.Redaction .NET 格式處理教學](/redaction/net/format-handling/)