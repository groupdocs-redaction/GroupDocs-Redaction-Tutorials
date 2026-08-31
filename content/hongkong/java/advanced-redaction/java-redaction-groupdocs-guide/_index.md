---
date: '2026-03-14'
description: 學習如何使用 GroupDocs.Redaction 安全地遮蔽 Java 檔案。本指南涵蓋載入政策、批次處理以及儲存已遮蔽的文件。
keywords:
- Java Redaction
- Secure Document Processing
- GroupDocs.Redaction for Java
title: 如何使用 GroupDocs.Redaction 對 Java 文件進行遮蔽
type: docs
url: /zh-hant/java/advanced-redaction/java-redaction-groupdocs-guide/
weight: 1
---

**Author:** GroupDocs

Translate:

"---\n\n**最後更新：** 2026-03-14  \n**測試環境：** GroupDocs.Redaction 24.9 for Java  \n**作者：** GroupDocs"

Make sure to keep markdown formatting.

Now produce final content.# 如何使用 GroupDocs.Redaction 對 Java 文件進行遮蔽

在本教學中，您將學習 **如何遮蔽 Java** 檔案，高效地使用 GroupDocs.Redaction。無論您在處理法律合約、醫療記錄或財務報表，以下步驟將協助您載入遮蔽政策、批次處理多個文件，並在保持原始格式完整的情況下儲存結果。

## 快速解答
- **安全文件處理是什麼意思？** 它指的是在工作流程中處理、遮蔽及儲存文件，同時保護機密資料。  
- **我可以一次處理多個檔案嗎？** 可以，範例程式會遍歷目錄，對每個檔案套用政策。  
- **如何遮蔽敏感資料？** 定義一個遮蔽政策，指定要隱藏的模式或文字，然後使用 Redactor 套用。  
- **生產環境需要授權嗎？** 需要有效的 GroupDocs.Redaction 授權才能在生產環境使用；可使用試用版進行評估。  
- **我可以在不光柵化的情況下儲存遮蔽文件嗎？** 當然可以——將 `RasterizationOptions.setEnabled(false)` 設為 false，即可保留原始格式。

## 如何使用 GroupDocs.Redaction 遮蔽 Java
安全文件處理涉及自動識別並移除各種檔案類型中的機密資訊，同時保留文件的完整性與可用性。GroupDocs.Redaction 在 Java 中提供程式化的解決方案。

### 為什麼在 Java 中使用 GroupDocs.Redaction？
- **支援完整的檔案格式** – PDF、Word、圖片等。  
- **細緻的政策控制** – 建立精確針對需求的遮蔽政策。  
- **可擴充的批次處理** – 在一次操作中處理多個檔案，減少人工工作。  
- **內建光柵化選項** – 可選擇是否將頁面光柵化以提升安全性。

## 前置條件

在實作 GroupDocs.Redaction for Java 之前，請確保具備以下條件：
- **必要的函式庫**：需要 GroupDocs.Redaction 版本 24.9。  
- **環境設定**：在機器上安裝 Java Development Kit (JDK) 並使用 IntelliJ IDEA 或 Eclipse 等 IDE。  
- **知識前提**：具備 Java 程式設計的基本概念，並熟悉檔案 I/O 操作。

## 設定 GroupDocs.Redaction for Java

要開始使用 GroupDocs.Redaction，請在專案中設定函式庫。設定方式如下：

**Maven 設定：**

將以下設定加入您的 `pom.xml`：

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

**直接下載：**  
或者，從 [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) 下載最新版本。

### 取得授權

為了完整發揮 GroupDocs.Redaction 的功能，建議取得授權。您可以先使用免費試用，或申請臨時授權以深入體驗其特性。

### 基本初始化與設定

安裝函式庫後，於 Java 應用程式中匯入必要的類別以進行初始化：

```java
import com.groupdocs.redaction.*;
```

## 實作指南

本節將說明如何實作兩個關鍵功能：載入並套用遮蔽政策，以及使用特定光柵化選項儲存處理後的文件。

### 載入並套用遮蔽政策

**概述：** 此功能會從檔案載入預先定義的遮蔽政策，並套用至指定目錄中的所有文件。處理後的檔案會依成功或失敗的結果儲存。

#### 步驟 1：初始化 RedactionPolicy

使用以下程式碼載入您的遮蔽政策：

```java
RedactionPolicy policy = RedactionPolicy.load("YOUR_POLICY_FILE_PATH");
```

此步驟相當重要，因為政策定義了文件中敏感資料的遮蔽規則。

#### 步驟 2：將政策套用至文件

遍歷目錄中的每個檔案並套用政策：

```java
for (final File fileEntry : new File("YOUR_DOCUMENT_DIRECTORY").listFiles()) {
    final Redactor redactor = new Redactor(fileEntry.getPath());
    try {
        // Apply the loaded redaction policy
        RedactorChangeLog result = redactor.apply(policy);
        
        // Determine output directory based on processing status
        File resultFolder = new File(result.getStatus() != RedactionStatus.Failed ? "YOUR_OUTPUT_DIRECTORY_DONE" : "YOUR_OUTPUT_DIRECTORY_FAILED");
        
        // Save the processed file
        try (FileOutputStream fileStream = new FileOutputStream(resultFolder.getPath() + "/" + fileEntry.getName())) {
            RasterizationOptions options = new RasterizationOptions();
            options.setEnabled(false);
            redactor.save(fileStream, options);
        }
    } finally {
        redactor.close(); // Ensure resources are released
    }
}
```

**參數說明：**  
- `RedactionPolicy.load()` – 從指定路徑載入政策。  
- `redactor.apply(policy)` – 依照載入的政策執行遮蔽。

### 使用光柵化選項儲存處理後的文件

**概述：** 套用遮蔽後，使用特定的光柵化選項儲存文件，以控制輸出格式與品質。

#### 步驟 1：為輸入檔案初始化 Redactor

開啟檔案以進行處理：

```java
File inputFile = new File("YOUR_DOCUMENT_DIRECTORY/input.docx");
```

#### 步驟 2：使用光柵化選項儲存

儲存處理後的文件，並指定光柵化設定：

```java
try (Redactor redactor = new Redactor(inputFile.getPath())) {
    try (FileOutputStream fileStream = new FileOutputStream(outputFileDirectory.getPath() + "/processed_output.docx")) {
        RasterizationOptions options = new RasterizationOptions();
        options.setEnabled(false);  // Example option to disable rasterization
        redactor.save(fileStream, options);
    }
}
```

**主要設定選項：**  
- `RasterizationOptions` – 控制遮蔽後文件的儲存方式，您可以保留原始格式或轉換為影像以提升安全性。

## 實務應用

1. **法律文件處理** – 在分享草稿前遮蔽客戶敏感資訊。  
2. **醫療資料管理** – 透過遮蔽醫療記錄確保患者機密性。  
3. **財務報告** – 保護與利害關係人共享的報告中的財務資料。  
4. **合約審查** – 在合約談判過程中保護專有條款。  
5. **電子郵件歸檔** – 歸檔商業郵件時遵守隱私合規。

## 效能考量

使用 GroupDocs.Redaction 時，優化效能的方式包括：
- **有效的資源管理** – 確保檔案正確關閉，以釋放系統資源。  
- **批次處理** – 以批次方式處理文件，能有效管理記憶體使用。  
- **優化遮蔽政策** – 只針對必要的遮蔽項目制定政策，以縮短處理時間。

## 常見問題與故障排除

- **缺少授權例外** – 若出現授權錯誤，請確認授權檔案已正確放置，且路徑已在應用程式中設定。  
- **不支援的檔案類型** – 確認檔案格式在支援清單內，否則 Redactor 會拋出 `UnsupportedFormatException`。  
- **大型檔案記憶體不足** – 對於非常大的 PDF，建議增加 JVM 堆積大小 (`-Xmx2g`) 或將檔案分成較小的區塊處理。

## 常見問答

**Q:** 我如何使用單一指令處理多個檔案？  
**A:** 使用「套用政策至文件」範例中示範的目錄遍歷迴圈，會自動處理資料夾內的每個檔案。

**Q:** 「遮蔽敏感資料」實際上會移除什麼？  
**A:** 遮蔽政策可以針對文字模式、圖像或中繼資料，將其以黑框取代或完全移除。

**Q:** 有沒有辦法在套用前預覽遮蔽政策？  
**A:** 有，您可以載入政策後呼叫 `redactor.preview(policy)`（若支援）以產生預覽 PDF。

**Q:** 如何在「儲存遮蔽文件」時不失去原始格式？  
**A:** 如示範，將 `RasterizationOptions.setEnabled(false)` 設為 false，即可保留原始檔案格式。

**Q:** 開發測試需要授權嗎？  
**A:** 開發階段使用臨時或試用授權即可；正式上線則需完整授權。

## 資源

- **文件說明**： [GroupDocs.Redaction Java Docs](https://docs.groupdocs.com/redaction/java/)  
- **API 參考**： [API Reference](https://reference.groupdocs.com/redaction/java)  
- **下載**： [Latest Releases](https://releases.groupdocs.com/redaction/java/)  
- **GitHub**： [Source Code on GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **免費支援**： [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)

---

**最後更新：** 2026-03-14  
**測試環境：** GroupDocs.Redaction 24.9 for Java  
**作者：** GroupDocs