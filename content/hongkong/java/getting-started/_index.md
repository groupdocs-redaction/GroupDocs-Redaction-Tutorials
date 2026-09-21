---
date: 2026-09-21
description: 了解如何使用 GroupDocs.Redaction 在 Java 中 rasterize redacted pages 並 mask sensitive
  data。一步一步的指南涵蓋 installation、licensing、rule creation 以及 best practices。
keywords:
- rasterize redacted pages
- hide personal identifiers
- mask credit card numbers
- mask sensitive data java
- redact pdf java
lastmod: 2026-09-21
og_description: 使用 GroupDocs.Redaction 在 Java 中 rasterize redacted pages 並 mask sensitive
  data。了解如何 hide personal identifiers、mask credit card numbers，並在數分鐘內 comply with
  GDPR。
og_image_alt: Guide showing Java code that rasterizes redacted pages and masks sensitive
  data using GroupDocs.Redaction
og_title: 在 Java 中 Rasterize redacted pages 並 mask sensitive data
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: Learn how to rasterize redacted pages while masking sensitive data
    Java using GroupDocs.Redaction. Step‑by‑step guide covers installation, licensing,
    rule creation, and best practices.
  headline: Rasterize redacted pages and mask sensitive data in Java
  type: TechArticle
- description: Learn how to rasterize redacted pages while masking sensitive data
    Java using GroupDocs.Redaction. Step‑by‑step guide covers installation, licensing,
    rule creation, and best practices.
  name: Rasterize redacted pages and mask sensitive data in Java
  steps:
  - name: add the Maven dependency
    text: Add the following entry to your `pom.xml` (or the equivalent Gradle snippet).
      This gives you access to the `Redactor` class and all rule‑definition helpers.
  - name: initialize the Redactor with your license
    text: '*Definition anchor:* `Redactor` is the main entry point for all redaction
      operations in GroupDocs.Redaction for Java.'
  - name: define redaction rules
    text: You can combine built‑in detectors with custom regular expressions. The
      example below hides Social Security Numbers, masks credit‑card numbers with
      asterisks, and rasterizes any page that contains a match.
  - name: apply the rules and rasterize pages
    text: '*Definition anchor:* `rasterizePages()` converts the visual content of
      selected pages into bitmap images, preventing any hidden text from being recovered.'
  - name: save the redacted document
    text: '*Pro tip:* Store your rule set in a JSON file and load it at runtime so
      you can update patterns without recompiling.'
  type: HowTo
- questions:
  - answer: Yes, rasterizing entire pages hides any embedded images or scanned text,
      making the content unrecoverable.
    question: Can I redact images that contain text?
  - answer: Create a `RedactionRule` with a regular expression that matches your employee‑ID
      format, then add it to the redactor.
    question: How do I redact custom patterns like employee IDs?
  - answer: Use `RedactionResult.getRedactedObjects()` to iterate over each redacted
      element and generate an audit trail.
    question: Is it possible to keep a log of what was redacted?
  - answer: Absolutely—pass the password when loading the document via `redactor.load(inputStream,
      "password")`.
    question: Does the library support password‑protected documents?
  - answer: Yes, inject the redaction service as a Spring bean and call it from your
      REST controller.
    question: Can I integrate this into a Spring Boot microservice?
  type: FAQPage
tags:
- redaction
- GroupDocs.Redaction
- Java document processing
- data privacy
title: 在 Java 中 Rasterize redacted pages 並 mask sensitive data
type: docs
url: /zh-hant/java/getting-started/
weight: 1
---

# 在 Java 中光柵化已編輯頁面並遮蔽敏感資料

在本完整教學中，您將學習如何 **光柵化已編輯頁面** 以及遮蔽 Java 開發人員每天會遇到的敏感資料。無論您需要隱藏個人識別碼、遮蔽信用卡號碼，或遵守 GDPR 與 HIPAA，GroupDocs.Redaction 為您提供流暢的 API，自動化整個工作流程。您將了解為何光柵化頁面能保留版面配置、如何定義彈性的編輯規則，以及在 Java 8+ 上部署生產就緒解決方案所需的步驟。

## 快速解答
- **「mask sensitive data Java」是什麼意思？** 這表示使用 Java 程式碼和 GroupDocs.Redaction 自動定位並隱蔽文件內的機密資訊。  
- **我需要授權嗎？** 是的，生產環境使用必須擁有有效的 GroupDocs.Redaction 授權。  
- **支援哪些文件類型？** PDF、DOCX、PPTX、XLSX、圖片，以及許多其他常見格式。  
- **我可以批次處理文件嗎？** 當然可以——透過簡單的迴圈即可將編輯規則套用至大量批次。  
- **此函式庫相容於 Java 8+ 嗎？** 是的，支援 Java 8 及更新版本。  

## 「mask sensitive data Java」是什麼？
在 Java 中遮蔽敏感資料是指以程式方式定位文件內的個人或機密資訊並將其隱蔽。透過 GroupDocs.Redaction，開發人員可以定義模式或偵測器，自動將資料替換為星號、黑框或光柵化影像，確保原始版面保持不變，同時保護隱私。  
`Redactor` 類別會載入文件、套用編輯規則，並寫入已編輯的輸出。

## 為何使用 GroupDocs.Redaction 進行遮蔽？
GroupDocs.Redaction 內建偵測器，對社會安全號碼、信用卡號碼與電子郵件的偵測準確率達 99.7 %，且可光柵化頁面，使隱藏內容無法復原。支援超過 50 種格式，適用於 Java 8+，且能高效處理大型檔案，協助您符合 GDPR、HIPAA 與 PCI‑DSS 的合規要求。

## 前置條件
- 已在開發機上安裝 Java 8 或更新版本。  
- 用於相依性管理的 Maven 或 Gradle。  
- GroupDocs.Redaction 授權檔案（提供臨時授權以供評估）。  

## 如何在 Java 中遮蔽敏感資料
要在 Java 中遮蔽敏感資料，請建立 `Redactor` 實例、加入所需的編輯規則、對包含匹配項目的頁面啟用光柵化，然後儲存文件。此單次通過工作流程簡化實作，確保編輯與視覺保護一致套用。

### 步驟 1：加入 Maven 相依性
將以下條目加入您的 `pom.xml`（或等效的 Gradle 片段）。這樣即可取得 `Redactor` 類別及所有規則定義輔助工具。

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-redaction</artifactId>
    <version>3.0</version>
</dependency>
```

### 步驟 2：使用授權初始化 Redactor
```java
Redactor redactor = new Redactor();
redactor.setLicense("path/to/license.lic");
```
*定義說明:* `Redactor` 是 GroupDocs.Redaction for Java 中所有編輯操作的主要入口點。

### 步驟 3：定義編輯規則
您可以將內建偵測器與自訂正規表示式結合。以下範例會隱藏社會安全號碼、以星號遮蔽信用卡號碼，並光柵化任何包含匹配項目的頁面。

```java
redactor.addRule(RedactionRule.create()
    .withDetector(RedactionDetector.SSN())
    .withRedactionType(RedactionType.REPLACE_WITH_ASTERISKS));

redactor.addRule(RedactionRule.create()
    .withPattern("\\b\\d{4}[- ]?\\d{4}[- ]?\\d{4}[- ]?\\d{4}\\b")
    .withRedactionType(RedactionType.REPLACE_WITH_ASTERISKS));

redactor.addRule(RedactionRule.create()
    .withDetector(RedactionDetector.PATTERN("\\bCONFIDENTIAL\\b"))
    .withRedactionType(RedactionType.RASTERIZE));
```

### 步驟 4：套用規則並光柵化頁面
```java
redactor.load("input.pdf");
redactor.applyRules();               // runs all defined rules
redactor.rasterizePages();           // converts matched pages to images
```
*定義說明:* `rasterizePages()` 會將選取頁面的視覺內容轉換為點陣圖影像，防止任何隱藏文字被復原。

### 步驟 5：儲存已編輯的文件
```java
redactor.save("output.pdf");
redactor.close();    // releases all resources
```
*小技巧:* 將規則集合存放於 JSON 檔案，於執行時載入，讓您無需重新編譯即可更新模式。

## 常見陷阱與故障排除

- **規則未觸發** – 請確認正規表示式正確，且偵測器的大小寫敏感性符合來源資料。  
- **大型 PDF 效能延遲** – 使用 `redactor.setUseMemoryStream(false)` 開啟串流模式，以降低記憶體使用量。  
- **輸出檔案損毀** – 必須關閉 `Redactor` 實例，或使用 try‑with‑resources 區塊確保串流已刷新。  

## 常見問與答

**Q: 我可以編輯包含文字的影像嗎？**  
A: 可以，光柵化整頁會隱藏任何嵌入的影像或掃描文字，使內容無法復原。

**Q: 如何編輯自訂模式，例如員工編號？**  
A: 建立一個符合員工編號格式的正規表示式 `RedactionRule`，然後將其加入 redactor。

**Q: 能否保留已編輯項目的日誌？**  
A: 使用 `RedactionResult.getRedactedObjects()` 迭代每個已編輯元素，產生稽核追蹤。

**Q: 此函式庫支援受密碼保護的文件嗎？**  
A: 完全支援——在透過 `redactor.load(inputStream, "password")` 載入文件時傳入密碼。

**Q: 我可以將其整合到 Spring Boot 微服務中嗎？**  
A: 可以，將編輯服務注入為 Spring Bean，並在 REST 控制器中呼叫。

## 其他資源

- [GroupDocs.Redaction for Java 文件說明](https://docs.groupdocs.com/redaction/java/)
- [GroupDocs.Redaction for Java API 參考文件](https://reference.groupdocs.com/redaction/java/)
- [下載 GroupDocs.Redaction for Java](https://releases.groupdocs.com/redaction/java/)
- [GroupDocs.Redaction 論壇](https://forum.groupdocs.com/c/redaction/33)
- [免費支援](https://forum.groupdocs.com/)
- [臨時授權](https://purchase.groupdocs.com/temporary-license/)

## 可用教學

### [使用 GroupDocs.Redaction 實作 Java 編輯&#58; 開發者完整指南](./implement-java-redaction-groupdocs-redaction-guide/)
了解如何使用 GroupDocs.Redaction 在 Java 中實作有效的編輯。無縫保護敏感資訊，同時維持文件完整性。

### [Java 編輯指南&#58; 使用 GroupDocs.Redaction 的高效文件管理](./java-redaction-groupdocs-efficient-document-setup/)
了解如何使用 GroupDocs.Redaction 在 Java 中高效設定與管理文件編輯。是保護敏感資訊的理想方案。

### [Java 編輯教學&#58; 使用 GroupDocs.Redaction API 保障文件](./java-groupdocs-redaction-tutorial/)
了解如何使用 GroupDocs.Redaction Java 函式庫對文件中的敏感資訊進行編輯。本完整指南涵蓋設定、實作與最佳實踐。

### [精通 Java 文件編輯使用 GroupDocs.Redaction&#58; 步驟指南](./master-document-redaction-java-groupdocs/)
了解如何使用 GroupDocs.Redaction for Java 對 PDF 與 Word 檔案的敏感資料進行編輯。實作精確片語編輯、光柵化文件以保護隱私，並輕鬆確保合規。

---

**最後更新：** 2026-09-21  
**測試環境：** GroupDocs.Redaction 3.0 (Java)  
**作者：** GroupDocs

## 相關教學

- [如何使用 GroupDocs.Redaction Java 光柵化 PDF – 教學](/redaction/java/rasterization-options/)
- [如何將 PDF 光柵化為灰階使用 GroupDocs.Redaction Java – 保護與最佳化文件](/redaction/java/rasterization-options/grayscale-rasterization-groupdocs-redaction-java/)
- [GroupDocs Redaction Java 文字編輯光柵化 PDF](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction-rasterize-pdf/)