---
date: '2026-02-16'
description: 學習如何使用 GroupDocs.Redaction for Java 進行頁面預覽與產生文件縮圖（Java）。一步一步的設定、程式碼與疑難排解。
keywords:
- GroupDocs.Redaction Java tutorial
- preview document page Java
- PNG preview generation Java
title: 如何使用 GroupDocs.Redaction Java 預覽頁面 – 完整指南
type: docs
url: /zh-hant/java/document-loading/load-preview-document-pages-groupdocs-redaction-java/
weight: 1
---

# 如何使用 GroupDocs.Redaction Java 預覽頁面

在當今快速變化的商業環境中，快速 **預覽頁面** 在文件中可能決定工作流程的順暢與否。無論您需要為文件管理系統生成快速縮圖，或想在網站入口顯示單頁，GroupDocs.Redaction for Java 提供可靠且安全的方式來產生高品質的 PNG 預覽。本教學將帶您完成載入文件、設定預覽選項，以及建立可嵌入任何位置的 **document thumbnail java**。

## 快速解答
- **「preview page」是什麼意思？** 產生特定文件頁面的影像（例如 PNG），而不需開啟完整檔案。  
- **建議使用哪種格式？** PNG 為無損格式，最適合作為文件縮圖。  
- **需要授權嗎？** 免費試用可用於評估；正式環境需購買永久授權。  
- **可以同時預覽多個頁面嗎？** 可以—使用 `setPageNumbers` 並傳入頁碼陣列。  
- **主要相依性是什麼？** Java 8 以上、GroupDocs.Redaction 函式庫，以及 Maven（可選）。

## 介紹

在當今的數位時代，有效處理文件加工對各種規模的企業皆相當重要。無論是馬上隱藏敏感資訊或僅預覽特定頁面，合適的工具都能節省時間並確保安全。本教學將向您介紹 GroupDocs.Redaction for Java 的強大功能，重點在於載入文件並產生特定頁面的 PNG 預覽。

**您將學會**
- 如何設定與配置 GroupDocs.Redaction for Java  
- 使用 `Redactor` 高效載入文件  
- 使用 `PreviewOptions` 產生特定頁面的 PNG 預覽（**how to preview page** 的核心）  
- 在實作過程中排除常見問題  

在開始實作此功能之前，先來了解前置條件。

## 前置條件

在開始之前，請確保您的環境已正確設定以使用 GroupDocs.Redaction for Java。這包括安裝必要的函式庫以及具備 Java 程式設計的基本概念。

### 必要的函式庫與相依性
- **GroupDocs.Redaction**：適用於 Java 的強大文件處理函式庫。  
- **Java Development Kit (JDK)**：請確保已安裝 JDK 8 或更新版本。

### 環境設定需求
- 如 IntelliJ IDEA、Eclipse 等 IDE，或任何能處理 Java 專案的文字編輯器。  
- 若偏好使用 Maven 進行相依性管理，請先完成 Maven 設定。

### 知識前置條件
- 具備 Java 程式設計與檔案 I/O 操作的基本認識。  
- 熟悉 Maven 用於管理專案相依性（可選）。

## 設定 GroupDocs.Redaction for Java

開始使用 GroupDocs.Redaction 非常簡單。您可以透過 Maven 或直接下載最新版本將此強大函式庫加入專案。

### Maven 設定
在您的 `pom.xml` 檔案中加入以下內容：

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
或者，從 [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) 下載最新版本。

### 取得授權步驟
1. **免費試用**：先使用免費試用版以探索 GroupDocs.Redaction 的功能。  
2. **臨時授權**：若需要超過試用期的時間或功能，可取得臨時授權。  
3. **購買**：考慮購買永久授權以供長期使用與支援。

#### 基本初始化與設定
要開始使用 GroupDocs.Redaction，請透過指定文件路徑來初始化 `Redactor` 類別：

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

## 實作指南

環境設定完成後，讓我們一步步實作載入文件並預覽特定頁面的功能。

### 載入與預覽文件頁面

#### 概述
本節說明如何使用 GroupDocs.Redaction for Java 產生文件中特定頁面的 PNG 預覽。這正是 **how to preview page** 的核心，亦非常適合用於建立 **document thumbnail java** 供 UI 預覽或歸檔索引使用。

##### 步驟 1：設定目標頁碼
首先指定要預覽的頁碼：

```java
int testPageNumber = 1;
```

此行將 `testPageNumber` 設為 1，表示將產生第一頁的預覽。

##### 步驟 2：定義輸出檔案路徑
指定產生的 PNG 檔案儲存位置。使用佔位符以產生動態檔名：

```java
final String previewFileName = "YOUR_OUTPUT_DIRECTORY_page%d.png";
```

此格式字串可根據頁碼動態設定檔名，非常適合在迴圈中產生多個縮圖。

##### 步驟 3：設定預覽選項
設定 `PreviewOptions` 以定義預覽的產生與儲存方式。實作 `ICreatePageStream` 介面以自訂串流建立：

```java
PreviewOptions options = new PreviewOptions(new ICreatePageStream() {
    @Override
    public java.io.OutputStream createPageStream(int pageNumber) {
        try {
            return new java.io.FileOutputStream(java.lang.String.format(previewFileName, pageNumber));
        } catch (Exception e) {
            // Handle exceptions related to file stream creation
            e.printStackTrace();
            return null;
        }
    }
});
options.setPreviewFormat(PreviewFormats.PNG);
options.setPageNumbers(new int[] { testPageNumber });
```

- **ICreatePageStream**：允許為每個頁面建立自訂輸出串流。  
- **setPreviewFormat**：指定預覽的格式；PNG 最適合作為 **document thumbnail java**。  
- **setPageNumbers**：定義要產生預覽的頁碼（此處僅產生您選取的那一頁）。

#### 疑難排解技巧
- 確認輸出目錄已存在且應用程式具有寫入權限。  
- 捕獲並記錄任何 `IOException` 以診斷路徑相關問題。  
- 若預覽為空白，請確保來源文件未受密碼保護或未損毀。

## 實務應用

以下是產生 **document thumbnail java** 可能有幫助的實務情境：

1. **文件審閱** – 在文件管理系統 (DMS) 中快速產生大型合約的縮圖以供審閱。  
2. **Web 應用程式** – 在入口網站顯示單頁預覽，無需讓使用者下載整個檔案。  
3. **歸檔系統** – 為已歸檔的檔案建立視覺參考，讓日後更容易找對文件。

## 效能考量

為了在處理大型檔案時保持應用程式的回應性：

- 將文件分塊處理或以串流方式讀取，以避免一次載入整個檔案至記憶體。  
- 根據預期的文件大小調整 JVM 堆積大小（`-Xmx`）。  
- 在同一文件的多頁預覽時，重複使用 `Redactor` 實例。

遵循 Java 記憶體管理的最佳實踐，可協助維持最佳效能。

## 常見問題與解決方案

| 問題 | 原因 | 解決方案 |
|-------|-------|----------|
| **FileNotFoundException** 在儲存 PNG 時 | 輸出目錄不存在或路徑錯誤 | 在預覽前以程式方式建立目錄 (`new File(path).mkdirs()`)。 |
| **OutOfMemoryError** 發生於大型 PDF | 整個文件被載入記憶體 | 使用具串流選項的 `Redactor`，或增加 JVM 堆積大小。 |
| **Blank preview image**（空白預覽圖） | 不支援的頁面內容（例如已加密） | 確保在預覽前已解密文件，或透過 `Redactor` 提供密碼。 |

## 結論

在本教學中，我們介紹了使用 GroupDocs.Redaction for Java 進行 **how to preview page** 以及產生 **document thumbnail java** 的方法。透過上述步驟，您現在應能將頁面預覽功能整合至自己的應用程式中，提升使用者體驗，並簡化文件工作流程。

**後續步驟**
- 嘗試不同的文件格式（PDF、DOCX、PPTX）。  
- 將預覽產生與隱私遮蔽結合，以顯示「前後」快照。  
- 探索批次處理，以為整個文件集合建立縮圖。  

準備好提升您的文件處理流程了嗎？立即開始實作，親自體驗 GroupDocs.Redaction for Java 的強大功能！

## 常見問答

**Q1：GroupDocs.Redaction for Java 的用途是什麼？**  
A1：它是一個功能強大的函式庫，可在 Java 應用程式中對各種格式的文件進行遮蔽、註解與預覽。

**Q2：建立頁面串流時如何處理例外？**  
A2：務必在檔案操作周圍加入例外處理，以管理檔案存取錯誤或無效路徑等問題。

**Q3：能同時預覽多個頁面嗎？**  
A3：可以，使用 `setPageNumbers` 並傳入整數陣列即可指定多頁。

**Q4：產生 PNG 預覽有何好處？**  
A4：PNG 提供無損壓縮與高畫質，非常適合作為文件縮圖。

**Q5：GroupDocs.Redaction 可以免費使用嗎？**  
A5：您可以先使用免費試用版，取得臨時授權，或依需求購買完整授權。

## 資源
- **文件說明**：[GroupDocs Redaction Documentation](https://docs.groupdocs.com/redaction/java/)  
- **API 參考**：[API Reference](https://reference.groupdocs.com/redaction/java)  
- **最新發佈**：[Latest Releases](https://releases.groupdocs.com/redaction/java/)  
- **GitHub 倉庫**：[GroupDocs GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **免費支援**：[GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)  
- **取得臨時授權**：[Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**最後更新：** 2026-02-16  
**測試環境：** GroupDocs.Redaction 24.9 for Java  
**作者：** GroupDocs