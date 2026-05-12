---
date: '2026-02-16'
description: 學習如何使用 GroupDocs Maven 依賴項在 Java 中對文件進行遮蔽時為檔案名添加後綴。包括從串流載入、刪除註釋以及保存選項。
keywords:
- document redaction Java
- GroupDocs.Redaction tutorial
- secure document handling
title: groupdocs Maven 依賴 – 在 Java 中為檔案名稱加上後綴
type: docs
url: /zh-hant/java/advanced-redaction/master-document-redaction-groupdocs-redaction-java/
weight: 1
---

# 如何在使用 GroupDocs.Redaction 於 Java 進行文件遮蔽時為檔名添加後綴

遮蔽機密資料只是成功的一半——您還必須確保儲存的檔案能清楚顯示已經過處理。**使用 groupdocs maven 依賴可讓此工作變得簡單**，只需幾行程式碼即可為輸出檔名添加後綴。本指南將教您在儲存已遮蔽文件時如何為檔名添加後綴，同時示範如何使用 GroupDocs.Redaction for Java 進行載入、註解與儲存。無論是保護法律合約、醫療紀錄或財務報告，這些步驟都能確保您的工作流程既安全又可稽核。

## 快速解答
- **「add suffix to filename」的作用是什麼？**  
  它會在輸出檔名後附加自訂後綴（例如「_redacted」），讓您能立即辨識已處理的檔案。  
- **我可以從串流載入文件嗎？**  
  可以——GroupDocs.Redaction 支援從任何 `InputStream` 載入，非常適合雲端儲存或記憶體內處理。  
- **此功能需要授權嗎？**  
  免費試用版即可執行基本遮蔽；臨時或正式授權則會解鎖所有進階功能，包括後綴處理。  
- **支援哪些格式？**  
  此函式庫可處理 DOCX、PDF、PPTX、XLSX 等多種格式。  
- **PDF 輸出需要光柵化嗎？**  
  光柵化為可選項目；當您需要將文件平面化以提升安全性時可啟用。  

## 為檔名添加後綴是什麼？
在檔名後添加後綴是一種簡單的命名慣例，用以表示該檔案已完成遮蔽。它可防止原始未遮蔽版本被誤傳，並協助自動化流水線追蹤處理狀態。

## 為什麼在此任務中使用 GroupDocs.Redaction？
GroupDocs.Redaction 提供流暢的 Java API，讓您能在僅幾行程式碼內結合遮蔽操作與檔案處理選項——例如 **為檔名添加後綴**。這可節省開發時間並降低人工錯誤的風險。

## 前置條件
- **Java Development Kit (JDK)：** 8 版或以上。  
- **GroupDocs.Redaction Library：** 用於遮蔽任務的核心函式庫。  
- **IDE：** IntelliJ IDEA、Eclipse 或任何相容 Java 的編輯器。  
- **Maven：** 用於相依性管理。  

### 知識前提  
熟悉 Java I/O 與基本物件導向概念，將有助於更容易理解範例。

## 設定 GroupDocs.Redaction（Java）

### Maven 設定  
在您的 `pom.xml` 檔案中加入以下設定，即可透過 Maven 取得 GroupDocs 函式庫：

```xml
<repositories>
   <repository>
      <id>repository.groupdocs.com</id>
      <name>GroupDocs Repository</name>
      <url>https://releases.groupdocs.com/redaction/java/</url>
   </repository>
</repositories>

<dependencies>
   <dependency>
      <groupId>com.groupdocs</groupId>
      <artifactId>groupdocs-redaction</artifactId>
      <version>24.9</version>
   </dependency>
</dependencies>
```

### 直接下載  
或者，直接從 [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) 下載最新版本。

### 取得授權  
1. **免費試用：** 無限制存取基本功能。  
2. **臨時授權：** 取得臨時授權以探索進階功能。  
3. **購買：** 長期使用時，建議購買正式授權。

#### 基本初始化與設定  
透過加入必要的匯入語句來初始化您的專案：

```java
import com.groupdocs.redaction.Redactor;
```

完成上述設定後，您即可開始實作文件遮蔽功能。

## 實作指南

### 功能 1：從串流載入文件  
**概觀：** 了解如何將文件載入 `InputStream` 以進行處理。

#### 步驟實作  
##### 步驟 1.1：建立 InputStream

```java
import java.io.FileInputStream;
import java.io.InputStream;

try (InputStream stream = new FileInputStream("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    final Redactor redactor = new Redactor(stream);
    try {
        // Document is now loaded and ready for further processing
    } finally {
        redactor.close();
    }
}
```

- **原因：** 使用 `InputStream` 可無縫處理以各種格式儲存的文件，這在雲端或微服務情境下需要 **從串流載入文件** 時尤為重要。

### 功能 2：套用註解刪除遮蔽  
**概觀：** 使用 `DeleteAnnotationRedaction` 移除文件中的註解。

#### 步驟實作  
##### 步驟 2.1：套用 DeleteAnnotationRedaction

```java
import com.groupdocs.redaction.redactions.DeleteAnnotationRedaction;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply the DeleteAnnotationRedaction to remove annotations from the document
    redactor.apply(new DeleteAnnotationRedaction());
}
```

- **原因：** 此步驟確保移除所有敏感註解，提升文件隱私。

### 功能 3：使用選項儲存文件  
**概觀：** 了解如何使用特定選項（如光柵化與 **為檔名添加後綴**）儲存已處理的文件。

#### 步驟實作  
##### 步驟 3.1：設定 SaveOptions

```java
import java.io.ByteArrayOutputStream;
import com.groupdocs.redaction.options.SaveOptions;

try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX")) {
    // Apply necessary redactions before saving
    redactor.apply(new DeleteAnnotationRedaction());
    try (ByteArrayOutputStream bA = new ByteArrayOutputStream()) {
        SaveOptions options = new SaveOptions();
        options.setRasterizeToPDF(true);  // Option to rasterize document to PDF format
        options.setAddSuffix(true);      // Option to add a suffix to the saved file name
        redactor.save(bA, options.getRasterization());
    }
}
```

- **原因：** 自訂儲存選項可提供彈性的輸出格式與命名慣例。啟用 `setAddSuffix(true)` **會為檔名添加後綴**，讓人一目了然該檔案已被遮蔽。

## groupdocs maven 依賴概述
**groupdocs maven 依賴** 只需在 `pom.xml` 中加入單一 `<dependency>` 條目，即可將整個 Redaction SDK 引入專案。它會處理傳遞相依性、保持函式庫為最新版本，並簡化建置自動化。透過在 `pom.xml` 中聲明此相依性，您可免除手動管理 JAR，且確保與最新安全修補程式相容。

## 為什麼添加後綴很重要
- **可稽核性：** 團隊能立即辨識哪些檔案可安全分發。  
- **自動化：** 腳本可依後綴過濾檔案，防止誤處理原始文件。  
- **合規性：** 多項法規要求對已清理的文件進行明確標示。  

## 實務應用
探索以下實務案例：  
1. **法律文件遮蔽：** 在與客戶共享前保護合約。  
2. **醫療紀錄處理：** 保護患者身分識別資訊。  
3. **財務報告：** 保持敏感數字機密。  
4. **CRM 整合：** 匯出前自動遮蔽客戶資料。  
5. **協作工具：** 確保共享草稿不會暴露隱藏評論。  

## 效能考量

### 效能最佳化
- 使用串流（`load document from stream`）以避免將整個檔案載入記憶體。  
- 及時關閉 `Redactor` 實例以釋放資源。

### 資源使用指導原則
- 在批次執行期間監控 CPU 與記憶體使用情況。  
- 處理較小檔案時，建議使用 `ByteArrayOutputStream` 進行記憶體內儲存。

### Java 記憶體管理最佳實踐
- 在處理多個相同類型檔案時重複使用 `Redactor` 物件。  
- 在 `try‑with‑resources` 區塊中呼叫 `close()`，以防止記憶體洩漏。

## 常見問題與解決方案

| 問題 | 原因 | 解決方案 |
|-------|-------|-----|
| **後綴未顯示** | `setAddSuffix(false)` 或遺漏呼叫 | 確保在 `save()` 前設定 `options.setAddSuffix(true)`。 |
| **大型 DOCX 發生 OutOfMemoryError** | 將整個檔案載入記憶體 | 改為使用 `InputStream` 載入（參見功能 1）。 |
| **註解仍然可見** | 在儲存前未套用遮蔽 | 在 `save()` 前呼叫 `redactor.apply(new DeleteAnnotationRedaction())`。 |
| **PDF 未套用光柵化** | `setRasterizeToPDF(false)` 或未設定 | 需要平面化 PDF 時，設定 `options.setRasterizeToPDF(true)`。 |

## 常見問答

**Q：我可以使用 GroupDocs.Redaction 遮蔽 PDF 文件嗎？**  
A：可以，函式庫支援 PDF、DOCX、PPTX、XLSX 及其他多種格式。

**Q：使用 GroupDocs.Redaction 處理大型檔案的最佳方式是什麼？**  
A：使用串流（`load document from stream`）並及時關閉資源，以降低記憶體使用量。

**Q：可以自訂後綴文字嗎？**  
A：API 會自動加入預設後綴（例如「_redacted」）。若需自訂後綴，可在儲存後重新命名輸出檔案。

**Q：如何取得 GroupDocs.Redaction 的臨時授權？**  
A：前往 [Temporary License page](https://purchase.groupdocs.com/temporary-license/) 並依照說明操作。

**Q：如果遇到問題，該向哪裡尋求協助？**  
A：加入 [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) 取得專家協助。

## 資源
- **文件說明：** 前往 [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/) 探索詳細指南。  
- **API 參考：** 在 [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java) 查看完整 API 細節。  
- **下載：** 從 [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/) 取得最新版本。  
- **GitHub 程式庫：** 前往 [GroupDocs GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java) 參與貢獻或瀏覽原始碼。

---

**最後更新：** 2026-02-16  
**測試環境：** GroupDocs.Redaction 24.9 for Java  
**作者：** GroupDocs