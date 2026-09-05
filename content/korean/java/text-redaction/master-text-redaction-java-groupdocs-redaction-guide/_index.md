---
date: '2026-08-20'
description: Java와 GroupDocs.Redaction을 사용하여 regex로 텍스트를 가리는 방법을 알아보세요. 이 단계별 튜토리얼에서는
  regex 적용 방법, save options 구성 방법, 그리고 sensitive data를 보호하는 방법을 보여줍니다.
keywords:
- how to redact text
- mask credit card numbers
- remove social security numbers
- redact pdf java
lastmod: '2026-08-20'
og_description: Java와 GroupDocs.Redaction을 사용하여 텍스트를 가리는 방법을 배워보세요. 이 가이드에서는 regex
  redaction, save‑option 구성, 그리고 performance tips를 통해 sensitive data를 보호하는 방법을 설명합니다.
og_image_alt: Guide showing Java code to redact text using GroupDocs.Redaction
og_title: Java에서 GroupDocs.Redaction을 사용하여 텍스트를 가리는 방법
schemas:
- author: GroupDocs
  dateModified: '2026-08-20'
  description: Discover how to redact text using regex in Java with GroupDocs.Redaction.
    This step‑by‑step tutorial shows you how to apply regex, configure save options,
    and protect sensitive data.
  headline: 'How to redact text in Java with GroupDocs.Redaction: A complete guide'
  type: TechArticle
- description: Discover how to redact text using regex in Java with GroupDocs.Redaction.
    This step‑by‑step tutorial shows you how to apply regex, configure save options,
    and protect sensitive data.
  name: 'How to redact text in Java with GroupDocs.Redaction: A complete guide'
  steps:
  - name: import required classes
    text: 'The following imports give you access to the redaction API:'
  - name: initialize redactor and apply regex pattern
    text: '`RegexRedaction` represents a redaction rule based on a regular‑expression
      pattern. The pattern you provide determines which text fragments are replaced.
      - **Regex explanation**: The pattern `\b\d{3}-\d{2}-\d{4}\b` matches U.S. Social
      Security numbers (three digits, a dash, two digits, a dash, four '
  - name: configure save options
    text: '`SaveOptions` controls how the redacted file is written. Adding a suffix
      makes it clear which files have been processed, while preserving the original
      format avoids unwanted conversion. - **Save options**: `setAddSuffix(true)`
      automatically appends “_redacted” to the output filename, preventing acci'
  - name: customize additional save settings
    text: 'You can further tailor the output—such as preserving metadata or flattening
      annotations—by adjusting the `SaveOptions` object. - **Key configuration**:
      Setting `setPreserveMetadata(true)` retains original document properties, which
      is often required for compliance audits.'
  type: HowTo
- questions:
  - answer: It automatically appends a suffix (e.g., `_redacted`) to the output filename,
      making it obvious which files have been processed.
    question: What is the purpose of `setAddSuffix(true)` in SaveOptions?
  - answer: Absolutely. Any valid Java regular expression can be supplied to `RegexRedaction`
      to target emails, phone numbers, custom IDs, etc.
    question: Can I use regex patterns other than numbers for text redaction?
  - answer: Wrap the redaction logic in a try‑catch block, log the exception, and
      always close the `Redactor` in a finally clause to release resources.
    question: How should I handle errors during redaction?
  - answer: Yes. GroupDocs.Redaction works with PDF, DOCX, PPTX, and many other formats.
    question: Is PDF redaction supported?
  - answer: Use batch processing, keep regex patterns simple, and monitor memory usage
      with profiling tools.
    question: What are best practices for large‑scale redaction projects?
  type: FAQPage
tags:
- text redaction
- GroupDocs.Redaction
- Java document processing
- regex redaction
- PDF redaction
title: 'Java에서 GroupDocs.Redaction을 사용하여 텍스트를 가리는 방법: 완전 가이드'
type: docs
url: /ko/java/text-redaction/master-text-redaction-java-groupdocs-redaction-guide/
weight: 1
---

# Java에서 GroupDocs.Redaction을 사용하여 텍스트를 가리는 방법: 완전 가이드

오늘날 빠르게 변화하는 디지털 세계에서 문서에서 **텍스트를 가리는 방법**은 많은 개발자가 직면하는 질문입니다. 개인 데이터를 보호하거나 규정을 준수하거나 단순히 초안을 정리할 때, 이 가이드는 Java용 GroupDocs.Redaction을 사용하여 **정규식 기반 가리기를 빠르고 안전하게 적용하는 방법**을 단계별로 안내합니다. 가리기의 중요성, 라이브러리 설정 방법, 고성능 처리를 위한 모범 사례 팁을 배울 수 있습니다.

## 빠른 답변
- **GroupDocs.Redaction의 주요 목적은 무엇인가요?** 50개 이상의 문서 형식에서 민감한 텍스트를 찾고 마스킹하는 신뢰할 수 있는 API를 제공합니다.  
- **정규식을 사용하여 가리기를 적용하려면 어떻게 하나요?** 패턴을 지정한 `RegexRedaction` 객체를 생성하고 이를 `Redactor.apply()` 메서드에 전달합니다.  
- **라이선스가 필요합니까?** 무료 체험판은 개발에 사용할 수 있으며, 유료 라이선스를 구매하면 프로덕션용 전체 기능을 사용할 수 있습니다.  
- **PDF뿐만 아니라 DOCX 파일도 가릴 수 있나요?** 예—GroupDocs.Redaction은 PDF, DOCX, PPTX 및 기타 많은 형식을 지원합니다.  
- **성능을 향상시키는 가장 좋은 방법은 무엇인가요?** `Redactor` 인스턴스를 즉시 닫고, 정규식 패턴을 단순하게 유지하며, 파일을 배치 처리합니다.

## 텍스트 가리기란 무엇이며 왜 중요한가요?
텍스트 가리기는 문서에서 민감한 정보를 영구적으로 제거하거나 가리는 작업으로, 사회보장번호, 신용카드 정보, 의료 기록 등과 같은 기밀 데이터가 무단 사용자에 의해 복구되거나 조회되지 않도록 합니다. 원본 문자를 덮어쓰거나 마스크로 교체함으로써 복사‑붙여넣기나 OCR 도구로 숨겨진 내용을 추출할 수 없게 됩니다. 이는 개인정보 보호 규정을 준수하고 신원 도용이나 데이터 유출로부터 개인을 보호합니다.

## 텍스트 가리기에 정규식을 사용하는 이유는?
정규식을 사용하면 전화번호, 신용카드 번호 등 다양한 데이터 형식에 매칭되는 유연한 패턴을 정의할 수 있습니다. GroupDocs.Redaction과 정규식을 함께 사용하면 숨길 내용을 정확히 제어하면서 구현을 간결하고 유지보수하기 쉽게 만들 수 있습니다.

## 사전 요구 사항
시작하기 전에 다음을 확인하세요:

- **Java Development Kit (JDK)**가 설치되어 있음 (Java 8 이상).  
- Java 구문 및 정규식에 대한 기본적인 이해.  
- 코드를 실행하고 디버깅할 수 있는 **IntelliJ IDEA** 또는 **Eclipse**와 같은 IDE.

## Java용 GroupDocs.Redaction 설정
먼저 라이브러리를 프로젝트에 추가합니다.

### Maven 설정
Maven을 사용하는 경우 `pom.xml`에 다음을 삽입합니다:

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

### 직접 다운로드
또는 최신 JAR 파일을 [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/)에서 다운로드합니다.

### 기본 초기화
`Redactor`는 문서를 열고, 가리기 규칙을 적용하며, 결과를 출력하는 핵심 클래스입니다.

라이브러리를 사용할 수 있게 되면 다음과 같이 문서 가리기를 시작할 수 있습니다:

```java
// Import the necessary classes from GroupDocs.Redaction
import com.groupdocs.redaction.Redactor;

public class RedactionExample {
    public static void main(String[] args) {
        // Initialize the redactor with your document path
        final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
        // Ensure you close resources after operations
        try { /* Your code here */ } finally { redactor.close(); }
    }
}
```

## Java에서 정규식을 사용하여 텍스트를 가리는 방법
이 과정은 소스 파일을 `Redactor` 인스턴스로 로드하고, 매칭 패턴을 정의한 `RegexRedaction` 규칙을 만든 뒤, `redactor.apply()`로 적용하고, 마지막으로 `SaveOptions`를 사용해 수정된 문서를 저장하는 순서로 진행됩니다. 이 단계를 따르면 지원되는 모든 형식에서 민감한 문자열을 신뢰성 있게 찾아 마스크할 수 있습니다.

`Redactor` 클래스는 문서를 열고, 가리기 규칙을 적용하며, 출력 파일을 작성하는 핵심 구성 요소입니다. 내부적으로 리소스를 관리하므로 처리 후에는 반드시 닫아 메모리를 해제해야 합니다.

### 단계 1: 필요한 클래스 가져오기
다음 import 구문을 사용하면 가리기 API에 접근할 수 있습니다:

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.redactions.RegexRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;
```

### 단계 2: Redactor 초기화 및 정규식 패턴 적용
`RegexRedaction`은 정규식 패턴을 기반으로 하는 가리기 규칙을 나타냅니다. 제공하는 패턴에 따라 교체되는 텍스트 조각이 결정됩니다.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
try {
    // Define a regex pattern to find sequences of numbers and apply a replacement color.
    // The pattern: Two digits, optional whitespace, two more digits, non-digit characters,
    // followed by six digits.
    redactor.apply(new RegexRedaction("\\d{2}\\s*\\d{2}[^\\d]*\\d{6}", 
        new ReplacementOptions(java.awt.Color.BLUE)));
```

- **정규식 설명**: 패턴 `\b\d{3}-\d{2}-\d{4}\b`는 미국 사회보장번호(세 자리, 대시, 두 자리, 대시, 네 자리)를 매칭합니다. `ReplacementOptions`를 사용하면 검은색 오버레이나 사용자 정의 텍스트 마스크를 선택할 수 있습니다.

### 단계 3: 저장 옵션 구성
`SaveOptions`는 가려진 파일이 어떻게 기록되는지를 제어합니다. 접미사를 추가하면 어떤 파일이 처리되었는지 명확해지고, 원본 형식을 유지하면 원치 않는 변환을 방지할 수 있습니다.

```java
    // Configure save options
    SaveOptions saveOptions = new SaveOptions();
    saveOptions.setAddSuffix(true);  // Adds suffix to indicate processing
    saveOptions.setRasterizeToPDF(false);  // Preserves original format

    // Save the redacted document
    redactor.save(saveOptions);
} finally {
    redactor.close();  // Always close resources to prevent memory leaks
}
```

- **저장 옵션**: `setAddSuffix(true)`는 출력 파일명에 자동으로 “_redacted”를 추가하여 실수로 파일이 덮어써지는 것을 방지합니다.

### 단계 4: 추가 저장 설정 맞춤화
`SaveOptions` 객체를 조정하여 메타데이터 보존이나 주석 평탄화와 같은 출력을 추가로 맞춤화할 수 있습니다.

```java
import com.groupdocs.redaction.options.SaveOptions;

SaveOptions saveOptions = new SaveOptions();
saveOptions.setAddSuffix(true);  // Indicates processing by adding a suffix
saveOptions.setRasterizeToPDF(false);  // Keeps original format intact
```

- **핵심 구성**: `setPreserveMetadata(true)`를 설정하면 원본 문서 속성이 유지되며, 이는 규정 준수 감사 시 종종 요구됩니다.

## 실제 적용 사례
**텍스트를 가리는 방법**이 필수적인 실제 시나리오:

1. **법률 문서** – 외부 변호사와 초안을 공유하기 전에 클라이언트 식별자를 숨깁니다.  
2. **의료 기록** – 환자 이름, ID 또는 건강 번호를 마스크 처리해 HIPAA 규정을 준수합니다.  
3. **재무 보고서** – 분기 요약을 배포할 때 기밀 계좌 번호를 제거합니다.  

## 성능 고려 사항
- **메모리 관리**: `redactor.close()`를 항상 호출해 파일 핸들과 네이티브 리소스를 해제합니다.  
- **효율적인 정규식**: 단순한 패턴이 더 빠르게 실행됩니다; 가능한 경우 원자 그룹을 사용해 과도한 백트래킹을 피합니다.  
- **배치 처리**: 대량 문서 집합은 20–50개씩 배치 처리해 힙 사용량을 예측 가능하게 유지합니다.

## 일반적인 문제와 해결책
| 문제 | 해결책 |
|-------|----------|
| **정규식이 과도하게 매칭됨** | 온라인 정규식 테스트 도구로 패턴을 검증하고 문자 클래스를 좁히세요. |
| **출력 파일명 충돌** | `setAddSuffix(true)`를 사용하거나 `saveOptions.setOutputPath()`로 사용자 정의 경로를 지정하세요. |
| **대용량 PDF에서 메모리 누수** | PDF를 페이지별로 처리하거나 JVM 힙 크기(`-Xmx2g`)를 늘리세요. |

## 자주 묻는 질문

**Q: SaveOptions에서 `setAddSuffix(true)`의 목적은 무엇인가요?**  
A: 출력 파일명에 자동으로 접미사(예: `_redacted`)를 추가해 어떤 파일이 처리되었는지 명확히 표시합니다.

**Q: 텍스트 가리기에 숫자 외의 정규식 패턴을 사용할 수 있나요?**  
A: 물론입니다. 유효한 Java 정규식을 `RegexRedaction`에 전달하면 이메일, 전화번호, 사용자 정의 ID 등 다양한 데이터를 목표로 할 수 있습니다.

**Q: 가리기 중 오류가 발생하면 어떻게 처리해야 하나요?**  
A: 가리기 로직을 try‑catch 블록으로 감싸고 예외를 로그에 기록한 뒤, finally 절에서 항상 `Redactor`를 닫아 리소스를 해제합니다.

**Q: PDF 가리기가 지원되나요?**  
A: 예. GroupDocs.Redaction은 PDF, DOCX, PPTX 및 기타 많은 형식을 지원합니다.

**Q: 대규모 가리기 프로젝트의 모범 사례는 무엇인가요?**  
A: 배치 처리를 사용하고, 정규식 패턴을 단순하게 유지하며, 프로파일링 도구로 메모리 사용량을 모니터링합니다.

## 추가 자료
- **문서**: [GroupDocs Redaction Documentation](https://docs.groupdocs.com/redaction/java/)  
- **API 레퍼런스**: [GroupDocs API Reference](https://apireference.groupdocs.com/redaction/java)

---

**마지막 업데이트:** 2026-08-20  
**테스트 환경:** GroupDocs.Redaction 24.9 for Java  
**작성자:** GroupDocs

## 관련 튜토리얼

- [Mask Sensitive Data Java – GroupDocs.Redaction Guide](/redaction/java/getting-started/)
- [Mask Sensitive Data Java – Redact Personal Info with GroupDocs.Redaction](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)
- [How to Redact PDF with Aspose OCR and Java - Implementing Regex Patterns using GroupDocs.Redaction](/redaction/java/ocr-integration/aspose-ocr-java-pdf-redaction/)