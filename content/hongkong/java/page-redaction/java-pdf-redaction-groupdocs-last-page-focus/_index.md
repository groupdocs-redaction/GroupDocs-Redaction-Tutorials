---
date: '2026-01-24'
description: 學習如何使用 GroupDocs.Redaction for Java 進行 PDF 敏感資訊遮蔽，針對最後一頁的特定區域，以確保隱私與合規。
keywords:
- Java PDF Redaction
- GroupDocs.Redaction
- PDF Area Redaction
title: 如何使用 Java 與 GroupDocs.Redaction 進行 PDF 敏感資訊遮蔽：針對最後一頁與特定區域
type: docs
url: /zh-hant/java/page-redaction/java-pdf-redaction-groupdocs-last-page-focus/
weight: 1
---

# 如何發佈前清理報告，本教學的步驟都會提供清晰、實作性的指引，協助您完成合規的遮蔽作業。

## 快速答覆
- **使用的函式庫是什麼？** GroupDocs.Redaction for Java.  
- **我可以只針對最後一頁嗎？** 可以，使用 `PageRangeFilter` 搭配 `PageSeekOrigin.End 使用接受座標與尺寸  
- **程式碼是否相容於 Java 17？** 完全相容 – 此函式庫支援現代 JDK 版本。

## 什麼是 PDF 敏感資訊遮蔽，為什麼重要？

遮蔽會永久移除或遮蓋 PDF 中的敏感內容，確保被隱藏的資料24裝 Java Development Kit (JDK)  
   - 如 IntelliJ IDEA 或 Eclipse 等 IDE  

2. **環境設定**  
   - 已設定 Maven 以管理相依性  

3. **基礎知識**  
   - 熟悉 Java 語法與檔案處理  

## 設定 GroupDocs.Redaction（Java 版）

您可以透過 Maven 或直接下載 JAR 檔的方式，將函式庫加入專案中。

### Maven 設定
在 `pom.xml` 檔案中加入以下內容，即可將 GroupDocs.Redaction 作為相依性加入：

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

#### 取得授權步驟
- **免費試用：** 在未提供授權金鑰的情況下測試 API。  
- **臨時授權：** 使用時間限制的金鑰，在開發期間取得完整功能。  
- **購買授權：** 取得永久授權以用於正式環境。  

### 基本初始化
首先建立指向欲處理 PDF 的 `Redactor` 實例：

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_PDF");
```

## 如何遮蔽 PDF – 在最後一頁實作區域式遮蔽

以下為逐步說明，完整展示 **如何遮蔽 PDF** 內容於最後一頁，並將作業限制於指定的矩形區域。

### 功能 1：在 PDF 頁面上遮蔽特定區域

**概述：** 此功能可僅在最後一頁的選定區域內遮蔽文字，其他部分保持不變。

#### 步驟 1：載入 PDF 文件
```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_PDF");
```

#### 步驟 2：取得文件頁面的資訊
```java
IDocumentInfo info = redactor.getDocumentInfo();
PageInfo lastPage = info.getPages().get(info.getPageCount() - 1);
```

#### 步驟 3：定義遮蔽的取代選項
```java
ReplacementOptions options = new ReplacementOptions("[secret]");
```

#### 步驟 4：設定過濾器以指定要遮蔽的區域
```java
options.setFilters(new RedactionFilter[] {
    new PageRangeFilter(PageSeekOrigin.End, 0, 1),
    new PageAreaFilter(
        new java.awt.Point(0, lastPage.getHeight() / 2),
        new java.awt.Dimension(lastPage.getWidth(), lastPage.getHeight() / 2)
    )
});
```

#### 步驟 5：套用遮蔽
```java
RedactorChangeLog result = redactor.apply(new ExactPhraseRedaction("bibliography", false, options));
```

#### 步驟 6：檢查遮蔽是否成功並儲存變更
```java
if (result.getStatus() != RedactionStatus.Failed) {
    redactor.save("YOUR_OUTPUT_DIRECTORY/redacted_output.pdf");
}
```

#### 步驟 7：關閉 Redactor 以釋放資源
```java
redactor.close();
```

### 功能 2：使用頁面範圍過濾進行遮蔽

**概述：** 當需要將遮蔽限制於特定頁面（例如多頁合約的最後一頁）時使用此功能。

#### 步驟 1：載入 PDF 文件
```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_PDF");
```

#### 步驟 2：取得文件頁面的資訊
```java
IDocumentInfo info = redactor.getDocumentInfo();
```

#### 步驟 3：定義頁面範圍過濾器以鎖定特定頁面
```java
PageRangeFilter pageRangeFilter = new PageRangeFilter(PageSeekOrigin.End, 0, 1);
```

### 功能 3：在 PDF 頁面上使用區域式遮蔽

**概述：** 此方法透過指定精確的矩形，提供像素級的控制以隱藏內容。

#### 步驟 1：載入 PDF 文件
```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_PDF");
```

#### 步驟 2：取得文件頁面的資訊
```java
IDocumentInfo info = redactor.getDocumentInfo();
PageInfo lastPage = info.getPages().get(info.getPageCount() - 1);
```

#### 步驟 3：定義區域過濾器以指定要遮蔽的頁面區段
```java
PageAreaFilter areaFilter = new PageAreaFilter(
    new java.awt.Point(0, lastPage.getHeight() / 2),
    new java.awt.Dimension(lastPage.getWidth(), lastPage.getHeight() / 2)
);
```

#### 步驟 4：關閉 Redactor 以釋放資源
```java
redactor.close();
```

## 實務應用

- **法律文件清理：** 在分享草稿前移除客戶姓名或案件編號。  
- **財務報告：** 在季報中遮蔽帳號或個人識別資訊。  
- **醫療紀錄：** 匯出 PDF 用於研究時，確保 PHI 被隱藏。  
- **預發佈審查：** 隱藏仍在開發中的章節，同時讓審閱者看到文件其餘部分。  

## 效能建議

- **重複使用 Redactor 實例：** 若批次處理多個 PDF，保持單一 `Redactor` 物件存活，並在檔案間重設。  
- **及時釋放：** 必須呼叫 `close()` 以釋放原生資源。  
- **先在樣本驗證：** 先於小型測試檔執行遮蔽，以確認過濾器幾何形狀，再進行大規模處理。  

## 常見問題與解決方案

| 問題 | 原因 | 解決方式 |
|-------|-------|-----|
| 未產生輸出檔案 | `result.getStatus()` 回傳 `Failed` | 檢查主控台的例外細節；確保取代文字有效且過濾器正確定義。 |
| 遮蔽覆蓋整頁 | `PageAreaFilter` 尺寸不正確 | 驗證 `lastPage.getHeight()` 與 `lastPage.getWidth()` 的值；相應調整 `Point` 與 `Dimension`。 |
| 授權錯誤 | 授權見問答

**Q: 我可以遮蔽圖片或圖形，而不只是文字嗎？**  
A: 可以。使用 `ExactImageRedaction`，或結合文字與圖片過濾器以遮蔽視覺元素。

**Q: 遮蔽在支援編輯的 PDF 閱讀器中仍然有效嗎？**  
A: 完全有效。遮蔽會永久移除底層內容，任何標準 PDF 編輯器都無法復原。

**Q: 如何遮蔽受密碼保護的 PDF？**  
A: 使用接受包含密碼的 `LoadOptions` 物件的 `Redactor` 建構子，載入帶密碼的文件。

**Q: 是否可以串接多個過濾器（例如頁面範圍 + 區域）？**  
A: 可以。將 `RedactionFilter` 陣列傳入 `options.setFilters()`，如範例所示。

**Q: 支援哪些 Java 版本？**  
A: GroupDocs.Redaction 24.9 支援 Java 8 至 Java 21，包括 LTS 版本。

## 結論

您現在已擁有一套完整、可投入生產的 **如何使用 Java 進行 PDF 敏感資訊遮蔽** 指南。透過頁面範圍與區域過濾器，您可以精準移除敏感資料，同時保留文件其餘部分的完整性。可嘗試不同的過濾器，將工作流程整合至現有的文件管線，並遵守資料隱私法規。

---

**最後更新：** 2026-01-24  
**測試環境：** GroupDocs.Redaction 24.9  
**作者：** GroupDocs