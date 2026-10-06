---
additionalTitle: GroupDocs API References
date: 2026-10-06
description: 了解如何使用 GroupDocs.Redaction for .NET 遮蔽 PDF 頁面、移除 PDF 註釋，以及遮蔽 Excel 儲存格——一個安全、跨平台的文件遮蔽
  API。
keywords:
- how to redact pdf
- remove pdf annotations
- redact excel cells
- redact pdf pages
- load pdf from stream
lastmod: 2026-10-06
linktitle: GroupDocs.Redaction for .NET 教學
og_description: 使用 GroupDocs.Redaction for .NET 快速遮蔽 PDF 頁面。此 API 可移除 PDF 註釋、遮蔽 Excel
  儲存格，並在超過 30 種格式中保護敏感資料。
og_image_alt: Guide to redact PDF pages using GroupDocs.Redaction for .NET
og_title: 如何遮蔽 PDF 頁面 – GroupDocs.Redaction for .NET
schemas:
- author: GroupDocs
  dateModified: '2026-10-06'
  description: Learn how to redact PDF pages, remove PDF annotations, and redact Excel
    cells using GroupDocs.Redaction for .NET – a secure, cross‑platform API for document
    redaction.
  headline: How to redact PDF pages with GroupDocs.Redaction for .NET
  type: TechArticle
- description: Learn how to redact PDF pages, remove PDF annotations, and redact Excel
    cells using GroupDocs.Redaction for .NET – a secure, cross‑platform API for document
    redaction.
  name: How to redact PDF pages with GroupDocs.Redaction for .NET
  steps:
  - name: load the PDF
    text: You can open a file from disk, a memory stream, or a remote source. The
      API accepts both a file path string and a `Stream` object, which is ideal for
      web services that receive uploads.
  - name: define the pages to redact
    text: Pass a list of zero‑based page indexes or a range string such as `"1-3,5"`
      to the `RemovePages` method. The library validates the range and throws a clear
      exception if a page does not exist.
  - name: save the sanitized document
    text: Call `Save` with the desired output format. You can keep the original PDF,
      export to a rasterized PDF, or stream the result directly to the client response.
  type: HowTo
- questions:
  - answer: Yes, the library removes the specified pages while preserving page numbering,
      bookmarks, and cross‑references for the remaining content.
    question: Can I redact PDF pages without affecting the rest of the document’s
      layout?
  - answer: Absolutely. Use `Redactor.RemoveAnnotations()` to strip all annotation
      objects in a single call.
    question: Is it possible to redact PDF annotations only?
  - answer: Load the workbook with `Redactor.LoadExcel(path)`, then call `Redactor.RedactCell(sheetName,
      cellAddress, RedactionMode.Blackout)` and save.
    question: How do I redact Excel cells directly?
  - answer: Yes, you can pass any `System.IO.Stream` to the `Load` method, which is
      ideal for processing files uploaded via ASP.NET Core controllers.
    question: Does GroupDocs.Redaction support loading PDFs from a stream?
  - answer: Metered licensing lets you pay per‑redaction operation, scaling cost‑effectively
      with usage spikes.
    question: What licensing model is recommended for high‑volume production use?
  type: FAQPage
tags:
- pdf redaction
- groupdocs.redaction
- .net document security
- redact pdf pages
title: 如何使用 GroupDocs.Redaction for .NET 遮蔽 PDF 頁面
type: docs
url: /zh-hant/net/
weight: 10
---

# 如何使用 GroupDocs.Redaction for .NET 對 PDF 頁面進行塗抹

如果您需要快速且可靠地 **塗抹 PDF 頁面**，GroupDocs.Redaction for .NET 為您提供功能完整、跨平台的 API，能從超過 30 種檔案格式中移除敏感內容。無論您是在構建合規驅動的工作流程、文件管理入口網站，或是以隱私為先的應用程式，這個函式庫都能永久抹除機密資料，同時保留文件其餘結構。

**GroupDocs.Redaction for .NET 是一個 .NET 函式庫，可永久移除超過 30 種文件格式中的敏感內容。** 它支援高容量處理，能在不將整個文件載入記憶體的情況下處理數百頁的檔案，並提供將文字轉為影像的光柵化選項，以提升安全性。

{{% alert color="primary" %}}
GroupDocs.Redaction for .NET 提供完整的教學與範例套件，協助您在 .NET 應用程式中實作安全的文件塗抹。從基本文字取代到進階的中繼資料清理，這些資源涵蓋塗抹文件中敏感資訊的必要技巧。了解如何從包括 PDF、Word、Excel、PowerPoint 以及影像等各種文件格式中永久移除私人資料，具備精確的控制與完整的機密內容刪除。我們的逐步指南可協助您精通標準與進階的塗抹功能，以符合合規需求並有效保護敏感資訊。
{{% /alert %}}

## 快速解答
- **GroupDocs.Redaction 能否塗抹整個 PDF 頁面？** 是的，您可以使用單一 API 呼叫刪除單頁或頁面範圍。  
- **它是否支援移除 PDF 註解？** 當然可以——註解、評論與標記可一次性剝除。  
- **我能在不轉換為 PDF 的情況下塗抹 Excel 儲存格嗎？** 可以，函式庫直接針對 Excel 工作表。  
- **是否支援從串流載入 PDF？** API 接受 `Stream` 物件，支援記憶體內處理。  
- **相容的 .NET 版本有哪些？** .NET Framework 4.5+、.NET Core 3.1+、.NET 5/6/7。

## 在 PDF 中，塗抹是什麼？
塗抹是指永久移除或遮蔽文件中的敏感內容，使其無法在之後被恢復或檢視。在 PDF 檔案中，塗抹可針對文字、影像、註解或整頁進行，最終產生保留原始版面配置的淨化檔案。

## 為何使用 GroupDocs.Redaction for .NET？
GroupDocs.Redaction for .NET 提供穩健且高效能的解決方案，能處理大型文件，同時確保敏感資料徹底移除，內建光柵化、廣泛的格式支援與詳細的稽核日誌，適合合規驅動的應用程式與企業環境。

- **支援 30+ 種格式** – 包括 PDF、DOCX、XLSX、PPTX、HTML 以及常見影像類型。  
- **可擴展效能** – 在一般伺服器上可於 5 秒內處理 500 頁的 PDF，且不需將整個檔案載入記憶體。  
- **內建光柵化** – 將塗抹的頁面轉為影像，確保不留下隱藏文字。  
- **合規就緒** – 透過稽核追蹤日誌符合 GDPR、HIPAA 與 PCI‑DSS 的要求。

## 前置條件
- .NET Framework 4.5+ **或** .NET Core 3.1+ 已安裝於您的開發機器上。  
- 有效的 GroupDocs.Redaction 授權（提供試用版以供評估）。  
- 取得您欲處理的 PDF、Excel 或 Word 檔案的存取權限。

## 分步說明如何塗抹 PDF 頁面

Redactor 是 GroupDocs.Redaction 的核心類別，用於載入、修改與儲存文件。RemovePages 會從已載入的文件中移除指定的頁面。

載入 PDF、定義要移除的頁面、套用塗抹，最後儲存結果。以下直接說明核心模式：

使用 `Redactor.Load(streamOrPath)` 載入目標 PDF，呼叫 `Redactor.RemovePages(pageNumbers)` 刪除不需要的頁面，最後使用 `Redactor.Save(outputPath)` — 這三步流程可在大多數文件中於一秒內完成塗抹。

### 步驟 1：載入 PDF
您可以從磁碟、記憶體串流或遠端來源開啟檔案。API 同時接受檔案路徑字串與 `Stream` 物件，非常適合接收上傳的 Web 服務。

### 步驟 2：定義要塗抹的頁面
將零基索引的頁面清單或類似 `"1-3,5"` 的範圍字串傳遞給 `RemovePages` 方法。函式庫會驗證範圍，若頁面不存在則拋出明確的例外。

### 步驟 3：儲存已淨化的文件
使用所需的輸出格式呼叫 `Save`。您可以保留原始 PDF、匯出為光柵化 PDF，或直接將結果串流至客戶端回應。

## 常見問題與解決方案
- **問題：** 塗抹似乎已生效，但原始文字仍可搜尋。  
  **解決方案：** 在儲存前啟用光柵化 (`Redactor.Rasterize = true`)；此操作會將頁面轉為影像，移除隱藏文字層。

- **問題：** 大型 PDF 造成 OutOfMemory 例外。  
  **解決方案：** 使用 `Redactor.Load(stream, loadOptions => loadOptions.EnableMemoryOptimization = true)` 以分塊方式處理檔案。

- **問題：** 註解未被移除。  
  **解決方案：** 載入文件後呼叫 `Redactor.RemoveAnnotations()`；此方法會剝除評論、標註與表單欄位。

## 常見問答

**Q: 我能在不影響文件其餘版面配置的情況下塗抹 PDF 頁面嗎？**  
A: 可以，函式庫會移除指定頁面，同時保留頁碼、書籤與交叉參照，供剩餘內容使用。

**Q: 是否可以僅塗抹 PDF 註解？**  
A: 當然可以。使用 `Redactor.RemoveAnnotations()` 於一次呼叫中剝除所有註解物件。

**Q: 如何直接塗抹 Excel 儲存格？**  
A: 使用 `Redactor.LoadExcel(path)` 載入活頁簿，然後呼叫 `Redactor.RedactCell(sheetName, cellAddress, RedactionMode.Blackout)` 並儲存。

**Q: GroupDocs.Redaction 是否支援從串流載入 PDF？**  
A: 是的，您可以將任意 `System.IO.Stream` 傳遞給 `Load` 方法，這對於透過 ASP.NET Core 控制器上傳的檔案處理非常理想。

**Q: 高量產環境建議使用哪種授權模式？**  
A: 計量授權讓您依塗抹操作付費，能隨使用量峰值彈性擴展成本。

**最後更新：** 2026-10-06  
**測試版本：** GroupDocs.Redaction 23.10 for .NET  
**作者：** GroupDocs  

---

### GroupDocs.Redaction for .NET 教學 – 如何塗抹 PDF 頁面

### [入門教學](./getting-started/)

如果您是 GroupDocs.Redaction 新手，請從此開始。本教學將帶您完成安裝、授權，以及在 .NET 中建立第一個塗抹專案。您將學會如何開啟文件、定義簡單的塗抹規則，並儲存已淨化的檔案。

### [進階塗抹技術](./advanced-redaction/)

深入探討自訂塗抹處理程序、策略、回呼與 AI 輔助塗抹。本指南說明如何建構彈性管線，以 **塗抹 PDF 頁面**、處理複雜文件結構，並整合機器學習模型以更智慧地偵測內容。

### [註解塗抹教學](./annotation-redaction/)

註解常包含機密備註。學習如何定位、修改或徹底移除 PDF、Word 檔案及其他支援格式中的註解、評論與審閱標記。

### [文件資訊教學](./document-information/)

了解文件的中繼資料是安全塗抹的第一步。本教學說明如何取得文件屬性、列舉支援的格式，並在套用任何塗抹前產生預覽影像。

### [文件載入教學](./document-loading/)

文件可能位於磁碟、串流或驗證層之後。學習安全載入本機檔案、記憶體串流與受密碼保護文件的最佳實踐。

### [文件儲存教學](./document-saving/)

塗抹完成後，您需要保存已清理的檔案。本指南涵蓋以原始格式儲存、匯出為光柵化 PDF，以及直接將結果串流至客戶端應用程式。

### [格式處理教學](./format-handling/)

GroupDocs.Redaction 支援廣泛的格式。探索如何處理不同檔案類型、建立自訂格式處理程序，並擴充函式庫以涵蓋特定文件標準。

### [影像塗抹教學](./image-redaction/)

影像可能隱藏敏感的視覺資料。學習塗抹特定影像區域、剝除嵌入圖片，並清理影像中繼資料，以確保不留下隱藏資訊。

### [授權與設定教學](./licensing-configuration/)

正確的授權對於正式環境至關重要。本教學示範如何套用授權、設定執行時參數，並實作計量授權以支援可擴展部署。

### [中繼資料塗抹教學](./metadata-redaction/)

中繼資料常洩漏機密細節。依照本指南移除 PDF、Word、Excel 與 PowerPoint 檔案中的文件屬性、隱藏評論與其他中繼資料。

### [OCR 整合教學](./ocr-integration/)

處理掃描 PDF 或影像時，OCR 是必備的。學習整合 OCR 引擎、擷取可搜尋文字，並 **塗抹含有敏感資訊的 PDF 頁面**。

### [頁面塗抹教學](./page-redaction/)

有時您需要刪除整頁。本教學示範如何刪除單一頁面、頁面範圍，及根據內容條件性移除頁面。

### [PDF 專屬塗抹教學](./pdf-specific-redaction/)

PDF 具備層、註解與表單欄位等獨特功能。精通僅限 PDF 的塗抹技術，包括內容過濾與保持文件完整性。

### [光柵化選項教學](./rasterization-options/)

光柵化 PDF 會將內容轉為影像，使資料抽取變得不可能。學習設定噪點、傾斜、灰階與邊框，並了解如何 **儲存光柵化 PDF** 檔案以達到最高安全性。

### [試算表塗抹教學](./spreadsheet-redaction/)

Excel 試算表常包含機密儲存格。本指南說明如何定位並 **塗抹 Excel 儲存格**、隱藏公式，及保護敏感工作表。

### [文字塗抹教學](./text-redaction/)

文字是最常需要保護的資料類型。依照步驟說明執行精確片語匹配、正規表達式塗抹與大小寫敏感搜尋，並了解如何有效 **塗抹 Word 文字**。

## 相關教學

- [如何移除註解 – GroupDocs.Redaction .NET 註解塗抹教學](/redaction/net/annotation-redaction/)
- [如何使用 GroupDocs.Redaction for .NET 移除 PDF 的最後一頁](/redaction/net/page-redaction/remove-last-page-pdf-groupdocs-redaction-net/)
- [如何使用 GroupDocs.Redaction for .NET 塗抹 PDF 並儲存為光柵化 PDF](/redaction/net/document-saving/groupdocs-redaction-net-rasterized-pdfs/)