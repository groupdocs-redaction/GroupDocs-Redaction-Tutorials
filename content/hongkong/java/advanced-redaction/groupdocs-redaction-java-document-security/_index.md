---
date: '2026-10-22'
description: 了解如何設定 GroupDocs Redaction Java，然後使用精確詞組 redaction 和 advanced rasterization
  選項來保護文件。
keywords:
- setup groupdocs redaction java
- exact phrase redaction java
- advanced rasterization groupdocs
lastmod: '2026-10-22'
og_description: 設定 GroupDocs Redaction Java 以安全地 redact 精確詞組並套用 advanced rasterization。請依照此步驟指南為
  Java 開發者操作。
og_image_alt: Guide to configure GroupDocs Redaction Java with phrase redaction and
  rasterization
og_title: 設定 GroupDocs Redaction Java 以進行精確詞組 redaction
schemas:
- author: GroupDocs
  dateModified: '2026-10-22'
  description: Learn how to set up GroupDocs Redaction Java, then protect documents
    with exact phrase redaction and advanced rasterization options.
  headline: Setup groupdocs redaction java for exact phrase redaction
  type: TechArticle
- description: Learn how to set up GroupDocs Redaction Java, then protect documents
    with exact phrase redaction and advanced rasterization options.
  name: Setup groupdocs redaction java for exact phrase redaction
  steps:
  - name: '**Load your document** – Use the `Redactor` constructor with the file path.'
    text: '**Load your document** – Use the `Redactor` constructor with the file path.'
  - name: '**Apply the redaction** – Create an `ExactPhraseRedaction` object and pass
      a `ReplacementOptions` instance. The `ExactPhraseRedaction` class is the API
      component that identifies the exact phrase and ties it to the replacement logic.
      `ReplacementOptions` defines the text, symbol, or image that will appear in
      place of the original phrase.'
    text: '**Apply the redaction** – Create an `ExactPhraseRedaction` object and pass
      a `ReplacementOptions` instance. The `ExactPhraseRedaction` class is the API
      component that identifies the exact phrase and ties it to the replacement logic.
      `ReplacementOptions` defines the text, symbol, or image that will appear in
      place of the original phrase.'
  - name: '**Configure save options** – Enable rasterization and add the desired advanced
      options.'
    text: '**Configure save options** – Enable rasterization and add the desired advanced
      options.'
  - name: '**Key configuration options**'
    text: '**Key configuration options**'
  type: HowTo
- questions:
  - answer: Pass any string you like to `ReplacementOptions`; it will replace the
      matched phrase verbatim.
    question: How do I customize the replacement text in exact phrase redaction?
  - answer: Yes, GroupDocs.Redaction supports PDF, PPTX, and several other formats—just
      verify that the specific raster options are available for the chosen type.
    question: Can I use advanced rasterization for non‑DOCX files?
  - answer: Double‑check that the path is absolute or correctly relative to your project’s
      working directory, and ensure the file has read/write permissions.
    question: What if I encounter errors with file paths in my code?
  - answer: Absolutely. Create multiple `ExactPhraseRedaction` instances and apply
      them sequentially before saving.
    question: Is there a way to redact multiple phrases at once?
  - answer: Process the document in sections or use the streaming APIs provided by
      the library to keep memory usage low.
    question: How do I handle large documents efficiently with GroupDocs.Redaction?
  type: FAQPage
tags:
- redaction java
- groupdocs redaction
- document security
- exact phrase redaction
- rasterization
title: 設定 GroupDocs Redaction Java 以進行精確詞組 redaction
type: docs
url: /zh-hant/java/advanced-redaction/groupdocs-redaction-java-document-security/
weight: 1
---

# 設定 groupdocs redaction java 以進行精確短語遮蔽

在現代企業環境中，**設定 groupdocs redaction java** 是保護 PDF、Word 檔案與簡報內機密資訊的首要步驟。無論您是合規主管、開發文件管理系統的程式設計師，或是自動化資料隱私工作流程的 IT 管理員，本指南將說明如何安裝函式庫、遮蔽精確短語，以及套用進階光柵化以產生可分享且防篡改的文件。

## 快速解答
- **精確短語遮蔽的功能是什麼？** 它會將特定字串（例如社會安全號碼）替換為您自訂的文字、遮罩或圖像。  
- **為什麼要使用光柵化？** 光柵化會將每一頁轉換為影像，讓您加入噪點、邊框或灰階，使任何隱藏的資料無法復原。  
- **需要哪個 Maven 版本？** GroupDocs.Redaction 24.9 或更新版本。  
- **可以一次遮蔽多個短語嗎？** 可以——建立多個 `ExactPhraseRedaction` 物件，並在儲存前一次套用。  
- **生產環境是否需要授權？** 試用版可用於測試；正式商業部署必須取得完整授權。

## 什麼是 setup groupdocs redaction java？
Setup groupdocs redaction java 意指將 GroupDocs.Redaction 函式庫加入您的 Java 建置系統，建立指向目標文件的 `Redactor` 實例，並設定遮蔽或儲存選項。`Redactor` 類別是 GroupDocs.Redaction 的核心 API，負責載入文件並協調所有遮蔽操作。函式庫加入 classpath 後，您只需幾行程式碼即可開始遮蔽文字、圖像或整段內容。

## 為什麼使用 GroupDocs Redaction for Java？
GroupDocs.Redaction for Java 提供即開即用、符合 PCI‑DSS 標準的遮蔽功能，支援 **50+ 檔案格式**，且能處理 **最多 500 頁** 的 PDF 而不必一次將整個檔案載入記憶體。內建光柵化、OCR 遮蔽與批次處理，提供企業級安全，同時將大型文件的記憶體使用量控制在 200 MB 以下。

## 前置條件
- Java 8 或更新版本（建議使用 Java 11 以上）  
- Maven 3 或相容的 IDE（IntelliJ IDEA、Eclipse 等）  
- 具備基本的 Java 語法與 Maven 依賴管理概念  

## 設定 GroupDocs.Redaction for Java

### Maven 設定

將以下儲存庫與相依性加入 `pom.xml`，完全照範例寫入：

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

如果您偏好手動方式，可從官方網站取得最新的 JAR 檔案：[GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/)。

### 取得授權

GroupDocs 提供免費試用版供評估使用。正式上線時，請從 GroupDocs 入口網站取得臨時或完整授權。

### 基本初始化與設定

`Redactor` 類別是所有遮蔽工作的入口點。函式庫加入 classpath 後，建立指向欲保護文件的 `Redactor` 實例：

```java
import com.groupdocs.redaction.Redactor;

public class Main {
    public static void main(String[] args) {
        Redactor redactor = new Redactor("path/to/document.docx");
        // Your code here...
        redactor.close();
    }
}
```

## 精確短語遮蔽

此功能讓您以佔位符、遮罩或任何自訂文字取代特定字串。

### 如何實作精確短語遮蔽
要執行精確短語遮蔽，首先以 `Redactor` 實例載入文件，接著建立 `ExactPhraseRedaction` 物件以指定要搜尋的短語。提供 `ReplacementOptions` 物件以定義取代方式，最後在儲存檔案前套用遮蔽。  
`ExactPhraseRedaction` 為辨識文件中特定精確短語並標記為遮蔽的類別。  
`ReplacementOptions` 定義視覺上的取代內容，如自訂文字、符號或圖像，將顯示於被遮蔽的短語位置。

1. **Load your document** – 使用 `Redactor` 建構子並傳入檔案路徑。

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
```

2. **Apply the redaction** – 建立 `ExactPhraseRedaction` 物件並傳入 `ReplacementOptions` 實例。`ExactPhraseRedaction` 類別負責辨識精確短語並與取代邏輯掛鉤。`ReplacementOptions` 定義將取代原始短語的文字、符號或圖像。

```java
try {
    // Replace 'John Doe' with '[personal]'
    redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]"));
} finally {
    redactor.close();
}
```

#### 疑難排解提示
- 請確認檔案路徑正確；錯誤的路徑會拋出 `FileNotFoundException`。  
- Java 字串區分大小寫；若需要不區分大小寫的比對，可使用 `String.equalsIgnoreCase`。

## 進階光柵化選項以安全儲存文件

光柵化會將每一頁轉換為影像，讓您加入灰階、噪點或邊框等視覺安全措施。

### 如何實作進階光柵化
在 `Redactor` 實例上設定儲存選項，開啟光柵化並選擇額外的視覺效果。您可以為每頁加入邊框、噪點、灰階轉換或傾斜，確保任何隱藏資料在渲染後無法復原。

1. **Configure save options** – 開啟光柵化並加入所需的進階選項。

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
try {
    SaveOptions so = new SaveOptions();
    // Set a suffix for output files
    so.setRedactedFileSuffix("_scan");

    // Enable and configure rasterization
    so.getRasterization().setEnabled(true);
    so.getRasterization().addAdvancedOption(AdvancedRasterizationOptions.Border);
    so.getRasterization().addAdvancedOption(AdvancedRasterizationOptions.Noise);
    so.getRasterization().addAdvancedOption(AdvancedRasterizationOptions.Grayscale);
    so.getRasterization().addAdvancedOption(AdvancedRasterizationOptions.Tilt);

    // Save the document
    redactor.save(so);
} finally {
    redactor.close();
}
```

2. **Key configuration options**  
   - `setRedactedFileSuffix` – 為處理過的檔案加上後綴（例如 “_scan”），方便辨識。  
   - `addAdvancedOption` – 選擇視覺效果，如 `Border`、`Noise`、`Grayscale` 與 `Tilt`。

#### 疑難排解提示
- 並非所有格式都支援每項光柵化功能；請以 DOCX、PDF、PPTX 測試確認。  
- 嘗試不同的選項組合，以在安全性與可讀性之間取得平衡。

## 實務應用

| 行業 | 典型使用情境 |
|----------|------------------|
| 法律 | 在分享合約前遮蔽客戶姓名。 |
| 醫療保健 | 隱藏醫療記錄中的患者識別資訊。 |
| 金融 | 在季報中遮蔽帳號。 |
| 人力資源 | 為內部稽核匿名化員工資料。 |
| 出版 | 從手稿中移除禁止使用的短語。 |

## 效能考量

- **記憶體管理：** 大型 PDF 可能佔用大量堆積空間；請提升 JVM `-Xmx` 參數或分段處理文件。  
- **I/O 效率：** 讀寫檔案時使用緩衝串流以降低延遲。  
- **選擇性遮蔽：** 僅對包含敏感資料的頁面執行遮蔽，可加速處理。

## 結論

掌握 **setup groupdocs redaction java** 後，您已擁有一套完整的精確短語遮蔽與進階光柵化工具，能在保護機密資訊的同時維持文件可用性。接下來，可探索其他遮蔽類型（圖像、條碼、正則表達式）或將函式庫整合至更大的文件管理工作流程。

## 常見問題

**Q: 如何自訂精確短語遮蔽的取代文字？**  
A: 將任意字串傳入 `ReplacementOptions`；系統會原樣取代匹配的短語。

**Q: 能否在非 DOCX 檔案上使用進階光柵化？**  
A: 可以，GroupDocs.Redaction 支援 PDF、PPTX 等多種格式——只要確認所選格式支援相應的光柵化選項即可。

**Q: 程式碼中若出現檔案路徑錯誤該怎麼辦？**  
A: 請再次確認路徑是絕對路徑或相對於專案工作目錄的正確路徑，並確保檔案具備讀寫權限。

**Q: 有沒有一次遮蔽多個短語的方法？**  
A: 當然可以。建立多個 `ExactPhraseRedaction` 實例，並在儲存前依序套用。

**Q: 如何有效處理大型文件？**  
A: 可將文件分段處理，或使用函式庫提供的串流 API，以降低記憶體使用量。

**最後更新：** 2026-10-22  
**測試環境：** GroupDocs.Redaction 24.9 for Java  
**作者：** GroupDocs  

**資源**  
- **文件說明：** [GroupDocs.Redaction Java Documentation](https://docs.groupdocs.com/redaction/java/)  
- **API 參考：** [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java)  
- **下載：** [最新版本](https://releases.groupdocs.com/redaction/java/)

## 相關教學

- [Java 遮蔽指南 Groupdocs 文件安全](/redaction/java/text-redaction/java-redaction-guide-groupdocs-document-security/)
- [Groupdocs Redaction Java 光柵化 Word 文件](/redaction/java/document-saving/groupdocs-redaction-java-rasterize-word-docs/)
- [進階日誌記錄 Groupdocs Redaction Java](/redaction/java/advanced-redaction/advanced-logging-groupdocs-redaction-java/)