---
date: '2026-02-26'
description: 學習如何使用 GroupDocs.Redaction 在 Java 文件中進行文字遮蔽，包括如何遮蔽個人資訊及取代敏感文字。
keywords:
- text redaction
- GroupDocs Redaction for Java
- sensitive information redaction
title: 如何使用 GroupDocs.Redaction for Java 進行文字遮蔽
type: docs
url: /zh-hant/java/text-redaction/groupdocs-redaction-java-text-redaction/
weight: 1
---

.

# 如何使用 GroupDocs.Redaction for Java 對文件進行文字遮蔽

在本指南中，您將學會 **如何在基於 Java 的文件中遮蔽文字**，藉助 GroupDocs.Redaction。無論是 **遮蔽個人資訊** 還是 **以佔位符取代敏感文字**，以下步驟將帶您完成一個完整、可投入生產的解決方案。完成本教學後，您即可保護隱私、遵循合規要求，並在多種檔案格式間自動化執行遮蔽。

## 快速答覆
- **使用的函式庫是什麼？** GroupDocs.Redaction for Java  
- **我可以遮蔽個人資訊嗎？** 可以 – 使用精確片語遮蔽並搭配取代選項。  
- **支援批次處理嗎？** 當然，您可以使用同一個 Redactor 實例迴圈處理多個檔案。  
- **需要授權嗎？** 免費試用可用於評估；正式上線需購買商業授權。  
- **需要哪個 Java 版本？** JDK 8 或以上。

## 什麼是「文字遮蔽」？
文字遮蔽是指永久移除或隱蔽文件中機密資料的過程。使用 GroupDocs.Redaction，您可以程式化地定位特定字串、以安全的佔位符取代，並儲存已淨化的檔案——全程不需手動編輯。

## 為何選擇 GroupDocs.Redaction for Java？
- **廣泛的格式支援：** DOCX、PDF、XLSX、PPTX 等。  
- **高效能：** 為大型檔案與批次作業進行最佳化。  
- **可擴充的回呼機制：** 可於遮蔽事件掛鉤以進行日誌記錄或自訂處理。  
- **合規就緒：** 符合 GDPR、HIPAA 及其他隱私法規。

## 前置條件
- **Java Development Kit (JDK)：** 8 版或更新。  
- **IDE：** IntelliJ IDEA、Eclipse 或任何支援 Java 的編輯器。  
- **Maven：** 用於相依管理。  
- **基本的 Java 知識：** 了解類別、方法與例外處理。

## 設定 GroupDocs.Redaction for Java
首先，將函式庫加入您的 Maven 專案。

### Maven 設定
在 `pom.xml` 檔案中加入儲存庫與相依性：

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
若您偏好手動方式，可從 [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) 下載最新 JAR。

### 授權取得
您可以先使用 **Free Trial**，或申請 **Temporary License** 以延長測試，亦可購買 **Commercial License** 於正式環境使用。

## 使用 GroupDocs.Redaction 在文件中遮蔽文字
以下章節將一步步說明如何 **遮蔽個人資訊** 與 **取代敏感文字**。

### 步驟 1：初始化 Redactor
建立指向欲處理文件的 `Redactor` 實例。

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx", new LoadOptions());
```

### 步驟 2：套用精確片語遮蔽
使用 `ExactPhraseRedaction` 來定位如 “John Doe” 的片語，並以安全的佔位符取代。

```java
redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]"));
```
- **參數說明：**  
  - `"John Doe"` – 要被遮蔽的精確文字。  
  - `ReplacementOptions("[personal]")` – 用以取代原始內容的字串，實際上 **遮蔽個人資訊**。

### 步驟 3：儲存已遮蔽的文件
將變更寫入新檔或覆寫原檔。

```java
redactor.save();
```

### 步驟 4：清理資源
務必關閉 `Redactor` 以釋放本機資源。

```java
finally {
    redactor.close();
}
```

## 使用自訂回呼遮蔽個人資訊
有時您需要在遮蔽發生時執行更多控制（例如記錄、條件取代）。

### 建立回呼類別
實作 `IRedactionCallback` 以接收遮蔽事件。

```java
class RedactionDump implements IRedactionCallback {
    @Override
    public void onRedacted(IRedaction redaction) {
        // Custom processing or logging for each redaction event.
    }
}
```

### 在建立 Redactor 時使用回呼
透過 `RedactorSettings` 傳入回呼實例。

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx", new LoadOptions(), new RedactorSettings(new RedactionDump()));
```

## 實務應用
- **法律合約：** 自動隱藏客戶姓名、社會安全號碼或機密條款。  
- **醫療紀錄：** 在與第三方共享前 **遮蔽個人資訊** 如患者識別碼。  
- **企業通訊：** 在對外發佈前 **取代敏感文字** 如內部專案代號。

## 效能考量
處理大型或大量檔案時，請留意以下建議：

- **批次處理：** 迴圈處理檔案集合以減少啟動開銷。  
- **記憶體管理：** 每處理完一個檔案即釋放 `Redactor`，避免同時保留過多文件於記憶體。  
- **效能分析：** 使用 Java 效能分析工具（如 VisualVM）找出 I/O 或遮蔽邏輯的瓶頸。

## 常見問題
**Q: 可以使用 GroupDocs.Redaction 來遮蔽 PDF 內的文字嗎？**  
A: 可以，函式庫支援 PDF、DOCX、XLSX、PPTX 等多種格式。

**Q: 遮蔽後可以復原嗎？**  
A: 不行。遮蔽會永久移除原始內容，請保留來源檔的備份。

**Q: 如何有效處理極大型文件？**  
A: 可將文件分段處理、使用批次模式，並透過效能分析工具監控記憶體使用。

**Q: 支援哪些其他文字格式？**  
A: 除了 DOCX 與 PDF，還可遮蔽 TXT、RTF、XLSX、PPTX 等。

**Q: 能將 GroupDocs.Redaction 整合到既有工作流程嗎？**  
A: 完全可以。API 可從 Web 服務、背景工作或 CI/CD 流程中呼叫。

## 資源
- **文件說明：** [GroupDocs Redaction Java Docs](https://docs.groupdocs.com/redaction/java/)  
- **API 參考：** [GroupDocs API Reference for Java](https://reference.groupdocs.com/redaction/java)  
- **下載：** [GroupDocs.Redaction Downloads](https://releases.groupdocs.com/redaction/java/)  
- **GitHub 程式庫：** [GroupDocs Redaction GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **免費支援論壇：** [GroupDocs Free Support](https://forum.groupdocs.com/c/redaction/33)  
- **臨時授權申請：** [Apply for a Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**最後更新：** 2026-02-26  
**測試環境：** GroupDocs.Redaction 24.9 for Java  
**作者：** GroupDocs