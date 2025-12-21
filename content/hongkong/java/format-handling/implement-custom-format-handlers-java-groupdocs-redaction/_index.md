---
date: '2025-12-21'
description: 學習如何使用 GroupDocs.Redaction 實作自訂格式處理器（Java）並對 Java 文件進行文字遮蔽。有效保護敏感資訊。
keywords:
- implement custom format handlers Java
- apply redactions GroupDocs Redaction
- Java data protection
title: 自訂格式處理程式 Java：使用 GroupDocs.Redaction 實作
type: docs
url: /zh-hant/java/format-handling/implement-custom-format-handlers-java-groupdocs-redaction/
weight: 1
---

# 使用 GroupDocs.Redaction 在 Java 中實作自訂格式處理程式

## 介紹
在當今以資料為驅動的世界，保護敏感資訊至關重要，而 **custom format handler java** 為您提供了處理任何檔案類型的彈性。無論您在處理法律文件、財務記錄或個人資料，確保機密性都可能充滿挑戰。本教學將逐步說明如何為純文字文件實作自訂格式處理程式，並使用 GroupDocs.Redaction 進行遮蔽，讓您能有效保護檔案。

## 快速答覆
- **What is a custom format handler java?** 一個告訴 GroupDocs.Redaction 如何讀取與處理非標準副檔名的外掛程式。  
- **Why use GroupDocs.Redaction for redaction?** 它提供可靠且高效能的遮蔽 API，支援多種文件類型。  
- **Which Java version is required?** 需要 Java 8 或更高版本；開發機必須安裝 JDK。  
- **Do I need a license?** 可使用免費試用版，但正式上線需購買永久授權。  
- **Can I batch‑process files?** 可以——在迴圈中為每個檔案初始化 Redactor，或使用平行串流。

## 您將學習
- 為特定檔案類型註冊 **custom format handler java**。  
- 使用 GroupDocs.Redaction 的 API **redact text java documents**。  
- 資料保護的實務應用案例。  
- 提升效能的調校技巧，讓資源管理更有效率。

## 前置條件
在開始之前，請先確認您具備以下項目：

### 必要的函式庫與版本
- **GroupDocs.Redaction**：版本 24.9 或以上。

### 環境設定需求
- 已安裝 Java Development Kit (JDK)。  
- 使用 IntelliJ IDEA 或 Eclipse 等 IDE 進行程式開發與執行。

### 知識前提
- 具備基本的 Java 程式設計概念。  
- 熟悉 Maven 以管理相依性（雖非必須，但會有幫助）。

確認上述前置條件後，讓我們為您的 Java 專案設定 GroupDocs.Redaction。

## 為 Java 設定 GroupDocs.Redaction
要將 GroupDocs.Redaction 整合至 Java 應用程式，有兩種主要方式：使用 Maven 或直接下載。我們將同時說明兩種做法，確保您無論偏好哪種設定方式都能順利上手。

### 使用 Maven
在您的 `pom.xml` 檔案中加入以下設定：

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
亦可直接從 [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) 下載最新版本。

#### 取得授權步驟
1. **Free Trial**：先使用免費試用版探索功能。  
2. **Temporary License**：取得臨時授權以延長測試時間。  
3. **Purchase**：購買正式授權以獲得完整功能。

### 基本初始化與設定
安裝完成後，請依照下列方式初始化 GroupDocs.Redaction：

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;

public class InitializeRedaction {
    public static void main(String[] args) throws Exception {
        Redactor redactor = new Redactor("path/to/your/document");
        // Perform operations with the redactor instance.
        redactor.close();
    }
}
```

完成 GroupDocs.Redaction 的設定後，我們即可開始實作 **custom format handler java** 並套用遮蔽。

## 實作指南
本章分為兩大功能：自訂格式處理程式註冊與遮蔽套用。請依序完成以下步驟。

### 功能 1：自訂格式處理程式註冊

#### 概觀
註冊 **custom format handler java** 可擴充 GroupDocs.Redaction 的能力，讓它能處理特定文件類型，例如具有自訂副檔名的純文字檔。

#### 實作步驟

##### 步驟 1：匯入必要類別
先匯入設定所需的類別：

```java
import com.groupdocs.redaction.configuration.DocumentFormatConfiguration;
import com.groupdocs.redaction.integration.DocumentFormatInstance;
import com.groupdocs.redaction.examples.java.helper_classes.CustomTextualDocument;
```

##### 步驟 2：設定文件格式
設定文件格式配置，指定哪個副檔名與哪個類別負責處理此自訂格式：

```java
class CustomFormatHandlerRegistration {
    public static void main(String[] args) {
        DocumentFormatConfiguration config = new DocumentFormatConfiguration();
        // Set the file extension for this handler.
        config.setExtensionFilter(".dump");
        // Specify handling by CustomTextualDocument class.
        config.setDocumentType(CustomTextualDocument.class);
        // Add to available formats list.
        DocumentFormatInstance.getDefaultConfiguration().getAvailableFormats().add(config);
    }
}
```

#### 主要設定選項
- `setExtensionFilter`：決定此處理程式適用的檔案副檔名。  
- `setDocumentType`：指定用於處理的文件類別。

### 功能 2：套用遮蔽

#### 概觀
本功能示範如何使用 GroupDocs.Redaction **redact text java documents**，確保敏感資訊被有效遮蔽。

#### 實作步驟

##### 步驟 1：匯入必要類別
匯入執行遮蔽所需的類別：

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;
```

##### 步驟 2：初始化 Redactor 並套用遮蔽
以文件路徑初始化 Redactor，套用所需的遮蔽規則，最後儲存修改後的檔案：

```java
class RedactionApplication {
    public static void main(String[] args) throws Exception {
        final Redactor redactor = new Redactor(YOUR_DOCUMENT_DIRECTORY + "/sample.dump");
        try {
            // Apply an exact phrase redaction.
            redactor.apply(new ExactPhraseRedaction("dolor", false, new ReplacementOptions("[redacted]")));
            // Save the document with a new name.
            redactor.save(new SaveOptions(false, "AnyText"));
        } finally {
            redactor.close();
        }
    }
}
```

#### 疑難排解技巧
- 確認檔案路徑正確且可存取。  
- 若自訂處理程式未能載入，請再次檢查設定是否正確。

## 實務應用
以下列出幾個可將本技術套用於實務的情境：

1. **Legal Document Protection** – 在對外分享文件前，先遮蔽敏感的案件細節。  
2. **Financial Records Security** – 透過遮蔽帳號與個人資訊，安全處理銀行對帳單。  
3. **HR Data Management** – 在審計或外部檢查時保護員工資料。  
4. **Integration with CRM Systems** – 匯出 CRM 報表前自動遮蔽客戶資料。  
5. **Automated Compliance Reporting** – 確保合規文件不會洩漏敏感資料。

## 效能考量
使用 GroupDocs.Redaction 時，請留意以下最佳化建議，以取得最佳效能：

- **Optimize Resource Usage** – 及時關閉資源，避免記憶體浪費。  
- **Batch Processing** – 以批次方式遮蔽多份文件，可降低載入時間。  
- **Profile and Benchmark** – 定期對應用程式進行效能分析，找出瓶頸。

## 常見問題與解決方案

| 問題 | 原因 | 解決方案 |
|------|------|----------|
| 處理程式未被識別 | 副檔名過濾條件不匹配 | 確認 `setExtensionFilter` 完全符合檔案的副檔名（例如 `.dump`）。 |
| 遮蔽未套用 | 字串大小寫敏感 | 在 `ExactPhraseRedaction` 中將 `ignoreCase` 旗標設為 `true`。 |
| 記憶體不足錯誤 | 同時載入大型檔案 | 改為順序處理檔案，或在支援的情況下使用串流 API。 |

## 結論
透過本教學，您應已掌握如何在 Java 中實作 **custom format handler java**，以及如何使用 GroupDocs.Redaction **redact text java documents**。這些技巧對於保護各類文件的敏感資訊相當重要。欲進一步提升能力，請參考下方資源並嘗試不同的使用情境。

### 後續步驟
- 探索其他遮蔽技術，例如基於模式的遮蔽。  
- 將工作流程整合至 CI/CD 管線，以自動執行合規檢查。

## 常見問答

**Q1: What file types can I handle with custom format handlers?**  
A1: 您可以透過指定副檔名與對應的文件類別，為任何檔案類型設定處理程式。

**Q2: How do I obtain a temporary license for GroupDocs.Redaction?**  
A: 前往 [GroupDocs' official site](https://products.groupdocs.com/redaction) 申請臨時授權。

**Q3: Can I process large batches of documents efficiently?**  
A: 可以——請參考「效能考量」中的批次處理建議，並在使用完每個 Redactor 後即時關閉實例。

**Q4: Is it possible to redact PDF files with the same handler?**  
A: GroupDocs.Redaction 已內建 PDF 支援；自訂處理程式通常用於非標準格式（如 `.dump`）。

**Q5: Does the API support asynchronous operations?**  
A: 雖然核心 API 為同步，但您可將呼叫包裝於 Java `CompletableFuture`，或使用平行串流達成並行處理。

---

**Last Updated:** 2025-12-21  
**Tested With:** GroupDocs.Redaction 24.9  
**Author:** GroupDocs