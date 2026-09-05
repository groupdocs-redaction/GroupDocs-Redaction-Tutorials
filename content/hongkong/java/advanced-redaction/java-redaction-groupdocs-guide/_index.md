---
date: '2026-08-31'
description: 了解如何在 Java 文件中使用 GroupDocs.Redaction 遮蔽敏感資料。一步一步的指南涵蓋政策、批次處理以及保留原始格式。
keywords:
- redact sensitive data
- process multiple files
- secure document processing
- save redacted document
lastmod: '2026-08-31'
og_description: 了解如何在 Java 文件中使用 GroupDocs.Redaction 遮蔽敏感資料。本指南逐步說明政策、批次處理與保留原始格式的做法。
og_image_alt: Guide showing how to redact sensitive data in Java using GroupDocs.Redaction
og_title: 在 Java 中使用 GroupDocs.Redaction 遮蔽敏感資料
schemas:
- author: GroupDocs
  dateModified: '2026-08-31'
  description: Learn how to redact sensitive data in Java documents using GroupDocs.Redaction.
    Step‑by‑step guide covers policies, batch processing, and preserving original
    formatting.
  headline: Redact sensitive data in Java with GroupDocs.Redaction
  type: TechArticle
- description: Learn how to redact sensitive data in Java documents using GroupDocs.Redaction.
    Step‑by‑step guide covers policies, batch processing, and preserving original
    formatting.
  name: Redact sensitive data in Java with GroupDocs.Redaction
  steps:
  - name: '**Legal document processing** – redact client identifiers before sharing
      drafts.'
    text: '**Legal document processing** – redact client identifiers before sharing
      drafts.'
  - name: '**Healthcare data management** – remove patient details to stay HIPAA‑compliant.'
    text: '**Healthcare data management** – remove patient details to stay HIPAA‑compliant.'
  - name: '**Financial reporting** – hide account numbers when distributing reports.'
    text: '**Financial reporting** – hide account numbers when distributing reports.'
  - name: '**Contract review** – protect proprietary clauses during negotiations.'
    text: '**Contract review** – protect proprietary clauses during negotiations.'
  - name: '**Email archiving** – ensure privacy compliance when storing corporate
      email archives.'
    text: '**Email archiving** – ensure privacy compliance when storing corporate
      email archives.'
  type: HowTo
- questions:
  - answer: It means handling, redacting, and storing files so that confidential data
      is protected throughout the entire workflow.
    question: What does secure document processing mean?
  - answer: Yes—by iterating over a folder you can apply the same redaction policy
      to every document automatically.
    question: Can I process multiple files in one run?
  - answer: Create a redaction policy that defines the patterns or objects to hide,
      then run the `Redactor` with that policy.
    question: How do I redact sensitive data?
  - answer: A valid GroupDocs.Redaction license is required for production; a trial
      license is available for evaluation.
    question: Do I need a license for production?
  - answer: Set `RasterizationOptions.setEnabled(false)` to keep the original file
      format unchanged.
    question: Can I save the redacted document without rasterization?
  type: FAQPage
tags:
- redact sensitive data
- GroupDocs.Redaction
- Java document processing
- batch redaction
title: 在 Java 中使用 GroupDocs.Redaction 遮蔽敏感資料
type: docs
url: /zh-hant/java/advanced-redaction/java-redaction-groupdocs-guide/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Java 中使用 GroupDocs.Redaction 進行敏感資料遮蔽

**GroupDocs.Redaction** 是一個 Java 函式庫，可程式化地從超過 70 種文件格式中移除機密資訊，同時保持原始版面不變。在本教學中，您將學習如何在 Java 應用程式中 **遮蔽敏感資料**、將遮蔽政策套用至一批檔案，並在不失去格式的情況下儲存結果。

## 快速解答
- **什麼是安全文件處理？** 這表示在整個工作流程中處理、遮蔽與儲存檔案，以確保機密資料受到保護。  
- **我可以一次處理多個檔案嗎？** 可以——透過遍歷資料夾，您可以自動將相同的遮蔽政策套用至每個文件。  
- **如何遮蔽敏感資料？** 建立一個定義要隱藏之模式或物件的遮蔽政策，然後使用 `Redactor` 執行該政策。  
- **生產環境是否需要授權？** 生產環境必須使用有效的 GroupDocs.Redaction 授權；可使用試用授權進行評估。  
- **我可以在不光柵化的情況下儲存遮蔽文件嗎？** 設定 `RasterizationOptions.setEnabled(false)` 以保持原始檔案格式不變。

## 如何使用 GroupDocs.Redaction 在 Java 文件中遮蔽敏感資料？

載入您的遮蔽政策，對目錄中的每個檔案執行，並儲存輸出——只需幾個簡潔步驟。GroupDocs.Redaction 的 API 允許批次處理文件，保留版面同時安全移除您指定的資料，並提供控制光柵化、輸出格式與效能特性的選項。

### 為何在 Java 中使用 GroupDocs.Redaction？

GroupDocs.Redaction 支援 **70 多種輸入與輸出格式**（PDF、DOCX、PPTX、影像等），讓您定義精細的政策，以針對特定文字、影像或中繼資料。此函式庫能有效率地處理批次，且您可切換光柵化，以保留原始格式或將頁面轉為影像以增強安全性。

### 前置條件
- **Java Development Kit (JDK) 8 或以上** 已安裝。  
- **Maven** 或其他建置工具，用於管理相依性。  
- 具備基本的 Java 知識與檔案 I/O 的熟悉度。  

### 設定 GroupDocs.Redaction（Java）

#### Maven 設定
在您的 `pom.xml` 中加入以下相依性：

```xml
<!-- Maven dependency placeholder -->
```
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

#### 直接下載
或者，從 [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) 下載最新的 JAR。

### 取得授權

試用授權可用於開發，但生產部署需要將永久授權檔案放置於應用程式的 resources 資料夾中，並在執行時引用。

### 基本初始化與設定

匯入所需類別並建立 `Redactor` 實例。**Redactor** 是執行文件遮蔽作業的主要類別。

```java
// Initialization code placeholder
```
```java
import com.groupdocs.redaction.*;
```

## 實作指南

### 什麼是遮蔽政策？

遮蔽政策是一組可重複使用的規則，告訴 Redactor 哪些文字模式、影像或中繼資料需要隱藏或刪除。您只需定義一次，即可套用至任意數量的文件，確保所有處理檔案的一致合規性。

```java
RedactionPolicy policy = RedactionPolicy.load("YOUR_POLICY_FILE_PATH");
```

### 載入並套用遮蔽政策

**從 XML 或 JSON 檔案載入政策**，並 **套用至資料夾中的每個文件**：

```java
// Load and apply policy code placeholder
```
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

### 批次處理多個檔案

遍歷目錄，使用 `Redactor` 開啟每個檔案，並套用相同的政策：

```java
// Batch processing code placeholder
```
```java
File inputFile = new File("YOUR_DOCUMENT_DIRECTORY/input.docx");
```

### 使用光柵化選項儲存處理後的文件

#### 為輸入檔案初始化 Redactor

開啟目標檔案以進行遮蔽：

```java
// Open file code placeholder
```
```java
try (Redactor redactor = new Redactor(inputFile.getPath())) {
    try (FileOutputStream fileStream = new FileOutputStream(outputFileDirectory.getPath() + "/processed_output.docx")) {
        RasterizationOptions options = new RasterizationOptions();
        options.setEnabled(false);  // Example option to disable rasterization
        redactor.save(fileStream, options);
    }
}
```

#### 使用光柵化選項儲存

設定 `RasterizationOptions` 以保留原始格式或將頁面轉為影像，然後儲存：

```java
// Save options code placeholder
```

**主要選項**  
- `setEnabled(false)` – 保留原始檔案類型。  
- `setResolution(150)` – 在光柵化為影像時設定 DPI 為 150。  

### 如何在不失去格式的情況下儲存遮蔽文件？

在呼叫 `save` 之前將光柵化旗標設為 `false`。這會指示 GroupDocs.Redaction 以與來源相同的格式寫入輸出，確保表格、字型與版面保持不變，同時仍套用所需的遮蔽。

### 實務應用

1. **法律文件處理** – 在分享草稿前遮蔽客戶識別碼。  
2. **醫療資料管理** – 移除患者細節以符合 HIPAA 規範。  
3. **財務報告** – 發布報告時隱藏帳號。  
4. **合約審查** – 在談判過程中保護專有條款。  
5. **電子郵件歸檔** – 在儲存公司郵件歸檔時確保隱私合規。  

### 效能考量

- **資源管理** – 必須始終關閉 `Redactor` 以釋放記憶體。  
- **批次處理** – 以 10‑20 個檔案為一組處理，以平衡速度與記憶體使用。  
- **最佳化政策** – 僅限制所需的模式；過寬的模式會增加處理時間。  

### 常見陷阱與故障排除

- **缺少授權例外** – 確認授權檔案路徑正確且檔案可讀取。  
- **不支援的檔案類型** – 檢查支援格式清單；不支援的檔案會拋出 `UnsupportedFormatException`。  
- **大型 PDF 記憶體不足錯誤** – 增加 JVM 堆積大小（`-Xmx2g`）或在遮蔽前將 PDF 拆分為較小的片段。  

## 常見問題

**Q:** 我如何使用單一指令處理多個檔案？  
**A:** 使用「套用政策至文件」範例中示範的目錄遍歷迴圈；它會自動遮蔽指定資料夾中的每個檔案。  

**Q:** 「遮蔽敏感資料」實際上會移除什麼？  
**A:** 政策可以針對純文字模式、影像或中繼資料，根據您的設定將其替換為黑框或完全移除。  

**Q:** 有沒有方法在套用前預覽遮蔽政策？  
**A:** 有——呼叫 `redactor.preview(policy)`（若支援）即可產生預覽 PDF，顯示將被隱藏的內容。  

**Q:** 我如何在不失去原始格式的情況下儲存遮蔽文件？  
**A:** 如示範所示，將 `RasterizationOptions.setEnabled(false)` 設定為 false；這會保留檔案的原生格式，同時仍套用遮蔽。  

**Q:** 開發測試是否需要授權？  
**A:** 開發階段使用臨時或試用授權即可；生產部署則需完整授權。  

## 資源

- [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) – 下載最新的 JAR 檔案。  
- [GroupDocs.Redaction Java Docs](https://docs.groupdocs.com/redaction/java/) – 官方文件與使用範例。  
- [API Reference](https://reference.groupdocs.com/redaction/java) – 詳細的類別與方法參考。  
- [Latest Releases](https://releases.groupdocs.com/redaction/java/) – 查看版本歷史與變更紀錄。  
- [Source Code on GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java) – 探索開源儲存庫。  
- [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33) – 社群支援與討論。  

## 結論

遵循本指南，您即可使用 GroupDocs.Redaction 強大的政策引擎與批次處理功能，安全且大規模地 **遮蔽 Java 文件中的敏感資料**。根據合規需求調整政策，優化光柵化設定以提升效能，並將工作流程整合至任何基於 Java 的後端服務。

---

**最後更新：** 2026-08-31  
**測試環境：** GroupDocs.Redaction 24.9 for Java  
**作者：** GroupDocs

## 相關教學

- [如何使用檔案路徑的 GroupDocs Redaction Java 授權遮蔽文件 – 步驟指南](/redaction/java/licensing-configuration/implement-groupdocs-redaction-java-license-file-path/)
- [在 Java 中遮蔽敏感資料 – GroupDocs.Redaction 指南](/redaction/java/getting-started/)
- [如何使用 GroupDocs.Redaction 在 Java 文件中遮蔽文字](/redaction/java/text-redaction/java-redaction-guide-groupdocs-document-security/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}