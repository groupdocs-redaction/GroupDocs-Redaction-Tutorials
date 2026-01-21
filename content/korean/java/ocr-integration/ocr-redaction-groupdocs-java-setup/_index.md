---
date: '2026-01-21'
description: Azure OCR 통합을 사용한 Java용 GroupDocs.Redaction으로 OCR을 이용해 PDF를 편집하고 스캔한
  문서를 편집하는 방법을 배워보세요.
keywords:
- OCR-based redactions Java
- GroupDocs Redaction setup
- regex-based text redaction
title: GroupDocs와 Azure OCR을 활용한 OCR PDF 편집 – Java 가이드
type: docs
url: /ko/java/ocr-integration/ocr-redaction-groupdocs-java-setup/
weight: 1
---

# GroupDocs 및 Azure OCR을 사용한 OCR 기반 PDF 가리기 – Java 가이드

이 포괄적인 튜토리얼에서는 Java에서 **OCR을 사용하는 방법을 알아봅니다. GroupDocs.Redaction과 Microsoft Azure OCR을 결합하여, 네이티브 PDF든 스캔된 이미지든 민감한 데이터를 정확히 찾아 이미지/PDF에서 텍스트를 추출하고 가리기 규칙을 자동으로 적용합니다.  
- **가리기 엔진을 제공하는 라이브러리는?** Java용 GroupDocs.Redaction.  
- OCR 커넥터.  
- **라이선스가 필요한가요?** 테스트용 무료 체험판을 사용할 수 있으며, 프로덕션에서는 정식 라이선스가 필요합니다.  
- **네이티브 PDF와 스캔된 PDF 모두 가릴 수 있나요?** 네 – OCR을 통해 스캔된 문서도 가릴 수 있습니다.

## “OCR을 사용한 PDF 가리기”란?
OCR을 사용한 PDF 가리기는 광학 문자 인식을 통해 시각적인 텍스트를 검색 가능한 문자열로 변환한 뒤, 가리기 패턴(예: 정규식)을 적용해 해당 정보를 파일이 공유되거나 저장되기 전에 숨기는 작업을 의미합니다.

## GroupDocs.Redaction과 Azure OCR을 함께 사용하는 이유
- **Azure 기반 OCR 엔진** 덕분에 스캔 페이지에서 높은 정확도 제공.  
- **간단한 Java API** 로 기존 워크플로에 직접 통합 가능.  
- **유연한 가리기 규칙** – 정규식, 키워드 또는 사용자 정의 로직 지원.  
- **규정 준수 준비** 된 출력물로 민감 데이터를 영구 삭제.

## Prerequisites
- Java Development Kit (JDK) 8 이상.  
- Maven(또는 JAR 수동 다운로드 옵션).  
- OCR 자격 증명이 포함된 Microsoft Azure 계정.  
- 기본 Java 지식 및 정규식에 대한 이해.

## Setting Up GroupDocs.Redaction for Java

### Maven Setup
`pom.xml`에 GroupDocs 저장소와 의존성을 추가합니다:

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
Maven을 사용하지 않으려면 공식 릴리스 페이지에서 최신 JAR를 다운로드하세요: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### License Acquisition
- **Free Trial** – 핵심 기능을 제한 없이 체험.  
- **Temporary License** – 대규모 프로젝트를 위한 체험 기간 연장.  
- **Full License** – 무제한 사용 및 프리미엄 지원 제공.

### Basic Initialization and Setup
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.RedactorSettings;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.examples.java.helper_classes.MicrosoftAzureOcrConnector;

// Initialize the OCR connector with Microsoft Azure
RedactorSettings settings = new RedactorSettings(new MicrosoftAzureOcrConnector());
```

## How to redact PDF with OCR in Java

### Step 1: Load the Document with OCR Settings
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;

// Load your document with OCR settings
try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf", 
    new LoadOptions(), settings)) {
    // Subsequent redaction steps will be placed here
}
```
- **Parameters**  
  - `"YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf"` – 대상 PDF 경로.  
  - `new LoadOptions()` – 기본 로드 구성.  
  - `settings` – Azure OCR 커넥터를 포함합니다.

### Step 2: Apply Regex Redactions (e.g., Social Security Numbers)
```java
import com.groupdocs.redaction.redactions.RegexRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

// Define the regex for sensitive data (e.g., Social Security Numbers)
RegexRedaction redaction = new RegexRedaction("\\b\\d{3}-\\d{2}-\\d{4}\\b", 
    new ReplacementOptions("[REDACTED]"));

// Apply redaction
redactor.apply(redaction);

// Save the document after redactions
redactor.save(new SaveOptions());
```
- **Regex Explanation** – `와 같은 패턴을/  
- **Performance** – 대용량 PDF는 힙 크기 확대 또는 비동기 처리 필요할 수 있습니다.

## Practical Use Cases for Redacting Scanned Documents
1. **Legal firms** – 사례 파일을 공유하기 전에 고객 마스킹합니다.  
3. **Healthcare providers** – 스캔된 의료 기록에서 환자 PHI를 보호합니다.  
4. **Government agencies** – 공개 기록 PDF에서 개인 데이터를 제거합니다.  
5. **Enterprises** – 제3자 감사 전에 계약서를 정리합니다.

## Performance Tips
- 정규식 패턴을 가능한 한 구체적으로 `Redactor` 인스턴스를 즉시 해제하세요(예시와 같이 try‑with‑resources 사용).  
- 배치Q: What is OCR redaction?**  
A: OCR 가리기는 광학 문자 인식을 사용해 이미지 또는 스캔된 PDF에서 텍스트를 추출한 뒤, 가리기 규칙을 적용해 해당 텍스트를 영구적으로 제거합니다.

**Q: Can I use GroupDocs.Redaction without Azure OCR?**  
A: 가능하지만, OCR을 사용하면 스캔된 문서에 대한 정확도가 크게 향상되어 **스캔된 문서 가리기**를 효과적으로 수행할 수 있습니다.

**Q: How do I handle complex regex patterns?**  
A: 샘플 데이터로 패턴을 테스트하고, 부분 매치를 방지하기 위해 단어 경계(`\b`)를 사용하며, 복잡한 표현식은 여러 개의 단순 가리기로 나누는 것을 고려하세요.

**Q: What are typical performance bottlenecks?**  
A: 대용량 파일에 대한 무거운 OCR 호출, 과도하게 넓은 정규식, 메모리 부족 등이 주요 병목 현상입니다. 정규식을 최적화하고 리소스를 확장해 개선하세요.

**Q: Where can I get help if I run into issues?**  
A: GroupDocs 커뮤니티 포럼에 질문을 올리세요: [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33).

## Additional Resources
- **Documentation**: https://docs.groupdocs.com/redaction/java/
- **API Reference**: https://reference.groupdocs.com/redaction/java
- **Download**: https://releases.groupdocs.com/redaction/java/
- **GitHub**: https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java
- **Free Support**: https://forum.groupdocs.com/c/redaction/33
- **Temporary License**: https://purchase.groupdocs.com/temporary-license/

---

**Last Updated:** 2026-01-21  
**Tested With:** GroupDocs.Redaction 24.9 for Java  
**Author:** GroupDocs