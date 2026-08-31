---
date: '2026-03-22'
description: 學習如何使用 GroupDocs 在 Java 中抹除元資料及移除作者元資料。本教學示範如何安全地儲存已遮蔽的文件檔案。
keywords:
- metadata redaction in Java
- GroupDocs Redaction setup
- removing metadata fields
title: 如何在 Java 中使用 GroupDocs 抹除元資料：逐步指南
type: docs
url: /zh-hant/java/metadata-redaction/groupdocs-redaction-java-metadata-implementation/
weight: 1
---

# 如何在 Java 中使用 GroupDocs 抹除 Metadata

在當今的數位世界中，保護文件內的敏感資訊至關重要，而**了解如何抹除 metadata**是其中關鍵的一環。本指南將教您如何使用 `EraseMetadataRedaction` 從 Word 檔案中剔除 *Author* 與 *Manager* 等 metadata，藉由 GroupDocs.Redaction for Java。完成本教學後，您將擁有一份乾淨且保障隱私的文件，並知道如何**儲存已抹除的文件**以供安全分享或存檔。

## 快速解答
- **EraseMetadataRedaction 的功能是什麼？** 它會從文件中移除選取的 metadata 欄位。  
- **哪個程式庫提供此功能？** GroupDocs.Redaction for Java。  
- **需要授權嗎？** 免費試用可用於測試；正式環境需購買永久授權。  
- **可以一次針對多個欄位嗎？** 可以，使用邏輯 OR 結合過濾條件。  
- **此程序是執行緒安全的嗎？** Redactor 實例不會在執行緒間共享；每次操作請建立新實例。

## 如何在 Java 中抹除 Metadata
本節將逐步說明如何**移除作者 metadata**以及其他不需要的屬性。

### 什麼是 EraseMetadataRedaction？
`EraseMetadataRedaction` 是內建的抹除類別，讓您指定要抹除的 metadata 項目。它支援 GroupDocs.Redaction 所支援的多種文件格式，確保隱藏的作者資訊不會外洩。

### 為什麼要在 GroupDocs 中使用 EraseMetadataRedaction？
- **合規** – 透過移除個人識別資訊，以符合 GDPR、HIPAA 或公司政策。  
- **一致性** – 在 PDF、DOCX、PPTX 等多種格式上套用相同的抹除邏輯。  
- **效能** – 抹除在記憶體中執行，無需外部工具。  
- **彈性** – 結合多個 `MetadataFilters` 以精準定位所需項目。

## 前置條件
- 已安裝 Java 8 或以上版本。  
- Maven（或能手動加入 JAR）。  
- GroupDocs.Redaction for Java（版本 24.9 或更新）。  
- 有效的 GroupDocs 試用或永久授權。

## 設定 GroupDocs.Redaction for Java

### Maven 安裝
將 GroupDocs 儲存庫與相依性加入您的 **pom.xml**：

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
或者，從 [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) 下載最新的 JAR。

### 取得授權
從 GroupDocs 入口網站取得免費試用或購買臨時授權。授權檔案需放置於應用程式可載入的位置（例如 classpath 根目錄）。

### 基本初始化與設定
以下是一個最小範例，示範如何為 DOCX 檔案建立 `Redactor` 實例：

```java
import com.groupdocs.redaction.Redactor;

String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
Redactor redactor = new Redactor(filePath);
```

## 如何在 Java 中使用 EraseMetadataRedaction
以下各節將把實作步驟拆解為清晰、可執行的步驟。

### 功能：清除特定 Metadata 項目

#### 概述
我們將使用 `EraseMetadataRedaction` 抹除 **Author** 與 **Manager** 兩個 metadata 欄位。這在將內部報告分享給外部合作夥伴時是常見需求。

#### 步驟實作

##### 1️⃣ 初始化 Redactor 物件
建立指向欲清理文件的 `Redactor` 實例：

```java
import com.groupdocs.redaction.Redactor;

String inputFilePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
final Redactor redactor = new Redactor(inputFilePath);
```

##### 2️⃣ 套用 EraseMetadataRedaction
使用 `EraseMetadataRedaction` 類別搭配 `MetadataFilters`。位元 OR (`|`) 可將 `Author` 與 `Manager` 過濾條件結合，於一次呼叫中移除兩個欄位：

```java
import com.groupdocs.redaction.redactions.EraseMetadataRedaction;
import com.groupdocs.redaction.MetadataFilters;

try {
    redactor.apply(new EraseMetadataRedaction(MetadataFilters.Author | MetadataFilters.Manager));
} finally {
    redactor.close();
}
```

##### 3️⃣ 設定 Save Options
調整 `SaveOptions` 以控制輸出檔名，以及文件是否要 rasterize 成 PDF：

```java
import com.groupdocs.redaction.options.SaveOptions;

SaveOptions saveOptions = new SaveOptions();
saveOptions.setAddSuffix(true); // Adds "_Redacted" to the file name
saveOptions.setRasterizeToPDF(false);

redactor.save(saveOptions);
```

### 常見使用情境
1. **法律文件** – 在將合約送給對方律師前抹除作者資訊。  
2. **企業報告** – 發佈季報給股東時移除經理姓名。  
3. **專案檔案** – 在存檔或上傳至公共倉庫前清理內部專案文件。

### 疑難排解技巧
- **找不到檔案** – 確認 `inputFilePath` 所指路徑的檔案確實存在，且應用程式具有讀取權限。  
- **缺少 metadata 欄位** – 並非所有文件類型都儲存相同的 metadata 鍵值；請先在 Office 中檢查文件屬性。  
- **授權錯誤** – 在建立 `Redactor` 實例前，確保授權檔案已正確載入。

## 效能考量
- 盡快關閉 `Redactor` 物件（如 `finally` 區塊所示），以釋放原生資源。  
- 除非需要 PDF 預覽，否則避免對大型文件進行 rasterize；此操作會大幅提升 CPU 與記憶體使用量。

## 常見問與答

**Q1: 什麼是 metadata 抹除？**  
A1: metadata 抹除是指移除文件中隱藏的屬性（如 author、manager 或自訂標籤），以防止敏感資訊意外外洩。

**Q2: 我可以在其他檔案類型上使用 GroupDocs.Redaction 嗎？**  
A2: 可以，該程式庫支援 PDF、DOCX、PPTX、XLSX 等多種格式。

**Q3: 如何處理抹除過程中的錯誤？**  
A3: 將 `apply` 呼叫包在 try‑catch 區塊，並在 finally 子句中始終關閉 `Redactor`，以確保釋放資源。

**Q4: 能否抹除自訂的 metadata 欄位？**  
A4: 當然可以。使用 `MetadataFilters.Custom("YourFieldName")`（或相應的列舉）即可針對任意自訂屬性。

**Q5: 使用 GroupDocs.Redaction 的最佳實踐是什麼？**  
A5:  
- 於應用程式啟動時即載入授權。  
- 盡快關閉 `Redactor` 物件。  
- 使用 `SaveOptions` 加上副檔名，以保留原始檔案。  
- 在批次處理前，先於文件副本上測試抹除效果。

**Q6: EraseMetadataRedaction 支援批次操作嗎？**  
A6: 可以，對檔案路徑集合進行迴圈，為每個檔案建立新的 `Redactor`，並套用相同的抹除邏輯。

**Q7: 能否將 EraseMetadataRedaction 與其他抹除類型結合使用？**  
A7: 可以，在儲存之前串接多個抹除物件（例如先文字抹除再進行 metadata 抹除）。

## 資源
- **文件說明**: [GroupDocs Redaction Java Docs](https://docs.groupdocs.com/redaction/java/)  
- **API 參考**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java)  
- **下載**: [Latest Releases](https://releases.groupdocs.com/redaction/java/)  
- **GitHub**: [GroupDocs GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **免費支援**: [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)  
- **臨時授權**: [Acquire a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**最後更新：** 2026-03-22  
**測試環境：** GroupDocs.Redaction 24.9 for Java  
**作者：** GroupDocs