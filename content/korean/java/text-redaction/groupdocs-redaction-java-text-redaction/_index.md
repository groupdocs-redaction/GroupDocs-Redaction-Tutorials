---
date: '2026-02-26'
description: GroupDocs.Redaction을 사용해 Java 문서의 텍스트를 삭제하는 방법을 배우고, 개인 정보를 마스킹하고 민감한
  텍스트를 교체하는 방법을 포함합니다.
keywords:
- text redaction
- GroupDocs Redaction for Java
- sensitive information redaction
title: Java용 GroupDocs.Redaction을 사용하여 텍스트를 가리는 방법
type: docs
url: /ko/java/text-redaction/groupdocs-redaction-java-text-redaction/
weight: 1
---

# How to Redact Text in Documents Using GroupDocs.Redaction for Java

이 가이드에서는 GroupDocs.Redaction을 활용하여 Java 기반 문서에서 **텍스트를 가릴(레드랙트) 방법**을 알아봅니다. 개인 정보를 **마스킹**하거나 **민감한 텍스트를 플레이스홀더로 교체**해야 할 때, 아래 단계들을 따라 하면 완전한 프로덕션 수준 솔루션을 구현할 수 있습니다. 튜토리얼을 마치면 프라이버시를 보호하고, 규정을 준수하며, 다양한 파일 형식에 대해 자동으로 레드랙션을 수행할 수 있게 됩니다.

## Quick Answers
- **What library is used?** GroupDocs.Redaction for Java  
- **Can I mask personal information?** Yes – use exact‑phrase redaction with replacement options.  
- **Is batch processing supported?** Absolutely, you can loop through multiple files with the same Redactor instance.  
- **Do I need a license?** A free trial works for evaluation; a commercial license is required for production.  
- **Which Java version is required?** JDK 8 or higher.

## What is “how to redact text”?
레드랙션은 문서에서 기밀 데이터를 영구적으로 제거하거나 가리는 과정입니다. GroupDocs.Redaction을 사용하면 특정 문자열을 프로그래밍 방식으로 찾아 안전한 플레이스홀더로 교체하고, 수동 편집 없이 정제된 파일을 저장할 수 있습니다.

## Why use GroupDocs.Redaction for Java?
- **Broad format support:** DOCX, PDF, XLSX, PPTX, and more.  
- **High performance:** Optimized for large files and batch operations.  
- **Extensible callbacks:** Hook into redaction events for logging or custom handling.  
- **Compliance‑ready:** Meets GDPR, HIPAA, and other privacy regulations.

## Prerequisites
- **Java Development Kit (JDK):** Version 8 or newer.  
- **IDE:** IntelliJ IDEA, Eclipse, or any Java‑compatible editor.  
- **Maven:** For dependency management.  
- **Basic Java knowledge:** Familiarity with classes, methods, and exception handling.

## Setting Up GroupDocs.Redaction for Java
시작하려면 Maven 프로젝트에 라이브러리를 추가합니다.

### Maven Setup
`pom.xml` 파일에 저장소와 의존성을 추가합니다:

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

### Direct Download
원한다면 [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/)에서 최신 JAR 파일을 다운로드하세요.

### License Acquisition
**Free Trial**로 시작하거나, 테스트 기간 연장을 위한 **Temporary License**를 요청하거나, 프로덕션 사용을 위한 **Commercial License**를 구매할 수 있습니다.

## How to Redact Text in Documents with GroupDocs.Redaction
다음 섹션에서는 **개인 정보를 마스킹**하고 **민감한 텍스트를 교체**하는 데 필요한 정확한 단계들을 안내합니다.

### Step 1: Initialize the Redactor
처리하려는 문서를 가리키는 `Redactor` 인스턴스를 생성합니다.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx", new LoadOptions());
```

### Step 2: Apply Exact‑Phrase Redaction
`ExactPhraseRedaction`을 사용하여 “John Doe”와 같은 구문을 찾아 안전한 플레이스홀더로 교체합니다.

```java
redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]"));
```
- **Parameters:**  
  - `"John Doe"` – 레드랙트할 정확한 텍스트.  
  - `ReplacementOptions("[personal]")` – 원본 내용을 교체할 문자열로, **개인 정보를 마스킹**합니다.

### Step 3: Save the Redacted Document
변경 사항을 새 파일에 저장하거나 원본을 덮어씁니다.

```java
redactor.save();
```

### Step 4: Clean Up Resources
항상 `Redactor`를 닫아 네이티브 리소스를 해제합니다.

```java
finally {
    redactor.close();
}
```

## How to Mask Personal Information with a Custom Callback
레드랙션이 발생했을 때(예: 로깅, 조건부 교체) 더 많은 제어가 필요할 때가 있습니다.

### Create a Callback Class
레드랙션 이벤트를 받기 위해 `IRedactionCallback`을 구현합니다.

```java
class RedactionDump implements IRedactionCallback {
    @Override
    public void onRedacted(IRedaction redaction) {
        // Custom processing or logging for each redaction event.
    }
}
```

### Use the Callback When Instantiating Redactor
`RedactorSettings`을 통해 콜백을 전달합니다.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx", new LoadOptions(), new RedactorSettings(new RedactionDump()));
```

## Practical Applications
- **Legal contracts:** 자동으로 클라이언트 이름, SSN, 기밀 조항 등을 숨깁니다.  
- **Medical records:** 제3자와 공유하기 전에 환자 식별자와 같은 **개인 정보를 마스킹**합니다.  
- **Corporate communications:** 외부 배포 전에 내부 프로젝트 코드와 같은 **민감한 텍스트를 교체**합니다.

## Performance Considerations
대용량 파일이나 다수의 파일을 처리할 때는 다음 팁을 참고하세요:

- **Batch processing:** 파일 컬렉션을 순회하여 시작 오버헤드를 줄입니다.  
- **Memory management:** 각 파일 처리 후 `Redactor`를 해제하고, 동시에 많은 문서를 메모리에 보관하지 않도록 합니다.  
- **Profiling:** Java 프로파일러(예: VisualVM)를 사용해 I/O 또는 레드랙션 로직의 병목을 파악합니다.

## Frequently Asked Questions
**Q: Can I redact text from PDFs using GroupDocs.Redaction?**  
A: Yes, the library supports PDF, DOCX, XLSX, PPTX, and many other formats.

**Q: Is a redaction reversible?**  
A: No. Redactions permanently remove the original content, so keep a backup of the source file.

**Q: How do I handle very large documents efficiently?**  
A: Process them in chunks, use batch mode, and monitor memory usage with profiling tools.

**Q: What other text formats are supported?**  
A: Besides DOCX and PDF, you can redact TXT, RTF, XLSX, PPTX, and more.

**Q: Can I integrate GroupDocs.Redaction into existing workflows?**  
A: Absolutely. The API can be called from web services, background jobs, or CI/CD pipelines.

## Resources
- **Documentation:** [GroupDocs Redaction Java Docs](https://docs.groupdocs.com/redaction/java/)  
- **API Reference:** [GroupDocs API Reference for Java](https://reference.groupdocs.com/redaction/java)  
- **Download:** [GroupDocs.Redaction Downloads](https://releases.groupdocs.com/redaction/java/)  
- **GitHub Repository:** [GroupDocs Redaction GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **Free Support Forum:** [GroupDocs Free Support](https://forum.groupdocs.com/c/redaction/33)  
- **Temporary License Application:** [Apply for a Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**Last Updated:** 2026-02-26  
**Tested With:** GroupDocs.Redaction 24.9 for Java  
**Author:** GroupDocs