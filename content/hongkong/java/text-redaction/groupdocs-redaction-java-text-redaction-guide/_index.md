---
date: '2026-08-09'
description: 了解如何使用 GroupDocs.Redaction 對 Java 文件進行塗抹。本分步教學涵蓋 Maven 設定、彩色矩形取代，以及安全文件處理的最佳實踐。
keywords:
- how to redact java
- GroupDocs.Redaction Java
- java text redaction
lastmod: '2026-08-09'
og_description: 了解如何使用 GroupDocs.Redaction 對 Java 文件進行塗抹。跟隨完整範例，包含 Maven 配置、彩色矩形取代以及效能技巧。
og_image_alt: 'Guide: redact Java documents with GroupDocs.Redaction using colored
  rectangle replacement'
og_title: 如何使用 GroupDocs.Redaction 對 Java 文件進行塗抹
schemas:
- author: GroupDocs
  dateModified: '2026-08-09'
  description: Learn how to redact Java documents using GroupDocs.Redaction. This
    step‑by‑step tutorial covers Maven setup, colored‑rectangle replacement, and best
    practices for secure document handling.
  headline: How to redact Java documents with GroupDocs.Redaction
  type: TechArticle
- description: Learn how to redact Java documents using GroupDocs.Redaction. This
    step‑by‑step tutorial covers Maven setup, colored‑rectangle replacement, and best
    practices for secure document handling.
  name: How to redact Java documents with GroupDocs.Redaction
  steps:
  - name: import required classes
    text: 'First, bring the necessary GroupDocs classes into scope:'
  - name: initialize the redactor
    text: 'Instantiate the `Redactor` with the path to your source document:'
  - name: define the phrase and replacement options
    text: '`ExactPhraseRedaction` represents a redaction rule that searches for an
      exact text phrase and replaces it with the specified style. `ReplacementOptions`
      lets you configure how the redacted area appears, such as color, overlay mode,
      and border width. Tell the engine which exact phrase to hide and wha'
  - name: save the redacted document
    text: 'Write the changes back to disk (or to a stream for further processing):
      > **Warning:** Wrap the above calls in a `try‑catch` block to handle `IOException`
      or `RedactionException` and ensure resources are released.'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction is a Java library that enables you to permanently
      remove or mask sensitive information from documents, images, and PDFs.
    question: What is GroupDocs.Redaction?
  - answer: Use any `java.awt.Color` constant or create a custom RGB color with `new
      Color(r, g, b)` and pass it to `ReplacementOptions`.
    question: How do I choose the color for redaction?
  - answer: Yes, you can chain several `ExactPhraseRedaction` objects or mix different
      redaction types before calling `save`.
    question: Can I apply multiple redactions in one document?
  - answer: GroupDocs.Redaction supports over 30 formats—including PDF, PPTX, XLSX,
      and common image types—so you can redact virtually any file you encounter. See
      the [API Reference](https://reference.groupdocs.com/redaction/java) for the
      full list.
    question: What if my document is not a `.docx` file?
  - answer: Wrap your redaction logic in a `try‑catch` block that catches `IOException`
      and `RedactionException`. Always call `redactor.close()` in a `finally` block
      or use try‑with‑resources to release native resources.
    question: How do I handle errors during redaction?
  type: FAQPage
tags:
- redact Java
- GroupDocs.Redaction
- document security
- Java redaction tutorial
title: 如何使用 GroupDocs.Redaction 對 Java 文件進行塗抹
type: docs
url: /zh-hant/java/text-redaction/groupdocs-redaction-java-text-redaction-guide/
weight: 1
---

# 如何使用 GroupDocs.Redaction 進行 Java 文件的遮蔽

在當今快速變遷的數位世界，**如何在 Java 中遮蔽文件**對於需要在 Office 檔案、PDF 或影像中隱藏機密資訊的任何人而言都是必備技能。無論您是在準備法律合約、財務報表，或是人力資源檔案，掌握使用可靠函式庫進行文字遮蔽都能為您節省時間，並確保符合隱私法規。本指南將逐步說明從將 GroupDocs.Redaction 加入 Maven 專案，到使用彩色矩形取代敏感片語的完整流程。

## 快速回答
- **本教學涵蓋什麼內容？** 完整的端對端範例，示範如何使用 GroupDocs.Redaction for Java 以彩色矩形遮蔽文字。  
- **使用哪個函式庫版本？** GroupDocs.Redaction 24.9（或閱讀時的最新發行版）。  
- **需要授權嗎？** 開發階段使用免費試用或臨時授權即可；正式上線需購買商業授權。  
- **可以自行選擇矩形顏色嗎？** 可以——在 `ReplacementOptions` 中使用任意 `java.awt.Color` 值。  
- **適用於大型文件嗎？** 只要適當配置記憶體與資源釋放，即可在不將整個檔案載入記憶體的情況下，順利處理高達 500 MB 的多兆位元檔案。

## 什麼是 Java 文字遮蔽？
Java 文字遮蔽是指永久移除或遮蔽文件內的敏感文字，使檔案可安全分享。GroupDocs.Redaction 會掃描文件，將辨識出的文字以實心顏色圖形取代，並保留原始版面配置，確保最終的 PDF 或 Office 檔案外觀專業，且隱藏的資料無法復原。

## 為何在 Java 中使用 GroupDocs.Redaction 進行文字遮蔽？
GroupDocs.Redaction 提供單一呼叫 API，能在保護機密資訊的同時維持視覺忠實度。它支援 **30+ 種格式**，如 DOCX、PDF、PPTX、XLSX、PNG、JPEG 與 BMP，幾乎所有常見檔案類型皆可使用。引擎以串流方式處理檔案，允許在 **500 MB** 內的文件進行遮蔽而不必一次載入全部內容，提升效能並減少伺服器負載。

## 前置條件
- **必備函式庫**：加入 GroupDocs.Redaction for Java 版本 24.9（或更新版本）。  
- **開發環境**：Java 8 以上，Maven（或任何支援 Maven 的 IDE）。  
- **基本技能**：熟悉 Java 檔案 I/O 與例外處理。

## 設定 GroupDocs.Redaction for Java
您可以透過 Maven 或直接下載 JAR 檔的方式將函式庫加入專案。

### Maven 設定
在 `pom.xml` 中加入儲存庫與相依性：

```xml
<repositories>
    <repository>
        <id>groupdocs-repo</id>
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
或是從 [GroupDocs.Redaction for Java 版本發行頁面](https://releases.groupdocs.com/redaction/java/) 下載最新 JAR。

**取得授權**  
先使用免費試用或申請臨時授權，再升級至付費方案。

## 基本初始化與設定
`Redactor` 是 GroupDocs.Redaction 的核心類別，負責載入並操作文件以執行遮蔽作業。

建立指向欲保護文件的 `Redactor` 實例：

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

> **專業提示：** 保持原始檔案不被修改；`Redactor` 會在記憶體中處理副本，必要時可隨時回復。

## 實作指南：以彩色矩形遮蔽文字
以下提供逐步說明，示範 **如何在 Java 中遮蔽文字**，透過實心顏色矩形取代目標片語。

### 步驟 1：匯入必要類別
先將所需的 GroupDocs 類別引入程式碼範圍：

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;
```

### 步驟 2：初始化 Redactor
以來源文件路徑建立 `Redactor`：

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

### 步驟 3：定義片語與取代選項
`ExactPhraseRedaction` 代表一條遮蔽規則，會搜尋精確文字片語並以指定樣式取代。  
`ReplacementOptions` 讓您設定遮蔽區域的外觀，如顏色、覆蓋模式與邊框寬度。

告訴引擎要隱藏哪個精確片語，以及使用哪種顏色矩形：

```java
redactor.apply(new ExactPhraseRedaction(
    "John Doe",
    new ReplacementOptions(java.awt.Color.RED)
));
```

*此處的 `"John Doe"` 為您想要遮蔽的敏感文字。您可自行替換為任意字串，甚至正規表達式。*

### 步驟 4：儲存遮蔽後的文件
將變更寫回磁碟（或寫入串流以供後續處理）：

```java
redactor.save("YOUR_DOCUMENT_DIRECTORY/redacted_sample.docx");
```

> **警告：** 請將上述呼叫包在 `try‑catch` 區塊中，以處理 `IOException` 或 `RedactionException`，並確保資源正確釋放。

## 實務應用
1. **法律文件製作** – 在分享草稿前隱藏客戶姓名或案件編號。  
2. **財務報告** – 在季報中遮蔽帳號或專有公式。  
3. **人力資源文件** – 匯出人事檔案時保護員工識別碼。

您可以將此工作流程整合至更大的文件管理系統，透過 REST 端點觸發，或於夜間排程批次遮蔽。

## 效能考量
- **記憶體配置** – 為大型 DOCX/PDF 檔案配置足夠的堆積空間（`-Xmx2g` 或更高）。  
- **物件生命週期** – 及時呼叫 `redactor.close()`（或使用 try‑with‑resources）以釋放本機資源。  
- **批次處理** – 若可能，重複使用同一個 `Redactor` 實例處理多個文件，以降低開銷。

## 結論
您現在已掌握一套 **如何在 Java 中遮蔽文件** 的完整教學，從 Maven 設定到以彩色矩形遮蔽敏感片語皆有說明。依循本步驟即可安全地在任何支援的文件格式中遮蔽文字，符合隱私法規，同時保持工作流程高效。

**後續建議**  
- 嘗試其他遮蔽類型，如影像遮蔽或基於正規表達式的片語匹配。  
- 結合 GroupDocs.Viewer，在儲存前先預覽變更。  
- 探索完整 API，以批次處理資料夾或整合雲端儲存服務。

## 常見問題

**Q: 什麼是 GroupDocs.Redaction？**  
A: GroupDocs.Redaction 是一套 Java 函式庫，可永久移除或遮蔽文件、影像與 PDF 中的敏感資訊。

**Q: 如何選擇遮蔽顏色？**  
A: 使用任意 `java.awt.Color` 常數，或以 `new Color(r, g, b)` 建立自訂 RGB 顏色，並傳入 `ReplacementOptions`。

**Q: 可以在同一文件中套用多個遮蔽嗎？**  
A: 可以，您可以串接多個 `ExactPhraseRedaction` 物件，或混合不同遮蔽類型後再呼叫 `save`。

**Q: 若文件不是 `.docx` 格式該怎麼辦？**  
A: GroupDocs.Redaction 支援超過 30 種格式，包括 PDF、PPTX、XLSX 以及常見影像類型，幾乎可以遮蔽您遇到的任何檔案。完整列表請參考 [API 參考文件](https://reference.groupdocs.com/redaction/java)。

**Q: 如何處理遮蔽過程中的錯誤？**  
A: 將遮蔽邏輯包在 `try‑catch` 區塊中，捕捉 `IOException` 與 `RedactionException`。務必在 `finally` 區塊呼叫 `redactor.close()`，或使用 try‑with‑resources 釋放本機資源。

---

**最後更新：** 2026-08-09  
**測試環境：** GroupDocs.Redaction 24.9 for Java  
**作者：** GroupDocs  

**資源**  
- **文件說明：** [GroupDocs.Redaction Java 文件說明](https://docs.groupdocs.com/redaction/java/)  
- **API 參考：** [GroupDocs Redaction API 參考文件](https://reference.groupdocs.com/redaction/java)  
- **下載最新版本：** [GroupDocs Redaction for Java 版本發行頁面](https://releases.groupdocs.com/redaction/java/)  
- **GitHub 倉庫：** [GroupDocs GitHub 頁面](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **免費支援論壇：** [GroupDocs Redaction 論壇](https://forum.groupdocs.com/c/redaction/33)  
- **臨時授權申請：** [取得您的臨時授權](https://purchase.groupdocs.com/temporary-license/)

## 相關教學

- [如何使用檔案路徑設定 GroupDocs Redaction Java 授權 – 步驟說明](/redaction/java/licensing-configuration/implement-groupdocs-redaction-java-license-file-path/)
- [編輯受密碼保護的文件 Java – 使用 GroupDocs.Redaction 進行遮蔽](/redaction/java/document-loading/groupdocs-redaction-java-password-documents/)
- [遮蔽敏感資料 Java – 使用 GroupDocs.Redaction 遮蔽個人資訊](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)