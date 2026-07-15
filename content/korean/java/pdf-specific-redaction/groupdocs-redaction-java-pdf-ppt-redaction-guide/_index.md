---
date: '2026-07-01'
description: Java에서 GroupDocs.Redaction을 사용하여 PDF 및 PowerPoint 파일을 삭제하는 방법을 배웁니다.
  pdf redaction java, how to redact ppt, and batch processing에 대한 단계별 가이드.
keywords:
- how to redact pdf
- pdf redaction java
- how to redact ppt
- redact confidential data
- batch pdf redaction
schemas:
- author: GroupDocs
  dateModified: '2026-07-01'
  description: Learn how to redact PDF and PowerPoint files in Java using GroupDocs.Redaction.
    Step‑by‑step guide for pdf redaction java, how to redact ppt, and batch processing.
  headline: How to Redact PDF and PPT Text with GroupDocs for Java
  type: TechArticle
- description: Learn how to redact PDF and PowerPoint files in Java using GroupDocs.Redaction.
    Step‑by‑step guide for pdf redaction java, how to redact ppt, and batch processing.
  name: How to Redact PDF and PPT Text with GroupDocs for Java
  steps:
  - name: Configure Replacement Options
    text: '- **Text Redaction** – replace the matched word with a placeholder such
      as “█”. - **Image Redaction** – overlay a solid red rectangle on image areas
      to obscure visual data.'
  - name: Apply Redactions
    text: '`PageAreaRedaction` is an operation that applies redaction to specified
      page areas. Run the `PageAreaRedaction` operation to perform both text and image
      redactions in one pass:'
  - name: Cleanup Resources
    text: 'Always close the `Redactor` to free native resources and avoid memory leaks:'
  type: HowTo
- questions:
  - answer: Redaction permanently removes the data from the file structure, while
      hiding only changes the visual layer.
    question: What is the difference between pdf text redaction and simply hiding
      text?
  - answer: Yes – provide the password when constructing the `Redactor` instance.
    question: Can I use GroupDocs.Redaction to redact password‑protected PDFs?
  - answer: Use `redactor.save("output.pdf")` to a temporary location and open the
      file for review.
    question: Is there a way to preview redaction results before saving?
  - answer: Absolutely – the same API works across 20+ supported document types.
    question: Does the library support other formats like DOCX or XLSX?
  - answer: Visit the community forum at [GroupDocs Free Support](https://forum.groupdocs.com/c/redaction/33)
      for assistance.
    question: Where can I get help if I run into problems?
  type: FAQPage
title: GroupDocs for Java를 사용하여 PDF 및 PPT 텍스트를 삭제하는 방법
type: docs
url: /ko/java/pdf-specific-redaction/groupdocs-redaction-java-pdf-ppt-redaction-guide/
weight: 1
---

# GroupDocs for Java를 사용하여 PDF 및 PPT 텍스트 가리기

오늘날 빠르게 움직이는 디지털 세계에서 **how to redact pdf** 파일은 기밀 데이터를 보호하기 위한 필수 단계입니다. 법률 계약서, 재무 보고서, 기업 파워포인트 자료를 다루든, 공유하기 전에 민감한 정보를 숨길 신뢰할 수 있는 방법이 필요합니다. 이 튜토리얼에서는 **GroupDocs.Redaction for Java**를 사용하여 PDF 및 PPT 파일의 마지막 페이지 또는 슬라이드에서 텍스트와 이미지를 가리는 방법을 안내하고, 배치 작업을 위한 확장 방법을 보여줍니다.

## 빠른 답변
- **pdf 텍스트 가리기란 무엇인가요?** 기밀 텍스트와 이미지를 영구적으로 제거하거나 마스킹하여 복구할 수 없게 합니다.  
- **Java에서 이를 지원하는 라이브러리는 무엇인가요?** GroupDocs.Redaction for Java는 PDF, PPT, DOCX, XLSX 등 다양한 형식을 위한 통합 API를 제공합니다.  
- **라이선스가 필요합니까?** 무료 체험판으로 평가할 수 있으며, 실제 운영에는 정식 라이선스가 필요합니다.  
- **같은 코드로 PDF와 PPT를 모두 가릴 수 있나요?** 예 – 동일한 `Redactor` 클래스가 두 형식을 모두 처리합니다.  
- **필요한 Java 버전은 무엇인가요?** JDK 8 이상.

## PDF 텍스트 가리기란 무엇인가요?
**PDF 텍스트 가리기는 PDF 문서에서 선택된 내용을 영구적으로 삭제하거나 가려서 복구하거나 볼 수 없게 합니다.** 단순히 숨기는 것과 달리, 가리기는 파일 구조에서 데이터를 제거하여 GDPR 및 HIPAA와 같은 개인정보 보호 규정을 준수합니다.

## 왜 GroupDocs.Redaction for Java를 사용해야 하나요?
GroupDocs.Redaction은 **20개 이상의 입력 및 출력 형식**을 지원합니다 – PDF, PPT, DOCX, XLSX 및 일반 이미지 형식을 포함하며 – 전체 파일을 메모리에 로드하지 않고 수백 페이지 문서를 처리할 수 있습니다. API는 세밀한 영역 제어, 자동 구문 감지를 위한 내장 정규식 엔진, 그리고 다중 코어 서버에서 배치 작업으로 확장 가능한 스레드 안전 설계를 제공합니다.

## 전제 조건
- **GroupDocs.Redaction for Java** (Maven 또는 직접 다운로드 가능).  
- **JDK 8+**가 개발 머신에 설치 및 구성되어 있어야 합니다.  
- **Maven**(또는 JAR를 수동으로 클래스패스에 추가할 수 있는 환경).  
- Java I/O 및 정규식에 대한 기본적인 이해.

## GroupDocs.Redaction for Java 설정
### Maven 설정
Add the GroupDocs repository and dependency to your `pom.xml`:

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
Maven을 사용하고 싶지 않다면, 최신 JAR를 [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/)에서 다운로드하십시오.

### 라이선스 획득
- **Free Trial** – 비용 없이 핵심 기능을 탐색할 수 있습니다.  
- **Temporary License** – 체험 기간 이후 테스트를 연장할 수 있습니다.  
- **Full License** – 상업적 배포에 필요합니다.

### 기본 초기화
`Redactor`는 문서를 나타내는 핵심 클래스이며 모든 가리기 작업을 노출합니다. 처리하려는 문서를 가리키는 `Redactor` 인스턴스를 생성합니다:

```java
import com.groupdocs.redaction.Redactor;
// Initialize the Redactor object
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/YOUR_FILE.pdf");
```

## 구현 가이드
### GroupDocs.Redaction을 사용하여 PDF Java 문서를 가리는 방법
PDF를 로드하고, 정규식 패턴을 정의하고, 교체 옵션을 구성한 뒤, 하나의 유창한 워크플로우로 가리기를 적용합니다. 이 방법을 사용하면 마지막 페이지의 오른쪽 절반 텍스트를 가리고, 감지된 이미지 위에 고정 사각형을 오버레이할 수 있습니다.

#### Step 1: Load the Document
```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/LOREMIPSUM_PDF");
```

#### Step 2: Define a Regex Pattern for Text Matching
```java
// Compile regex pattern to match specific text
java.util.regex.Pattern rx = java.util.regex.Pattern.compile("urna");
```

#### Step 3: Configure Replacement Options
- **Text Redaction** – 일치하는 단어를 “█”와 같은 자리 표시자로 교체합니다.  
- **Image Redaction** – 이미지 영역에 고정된 빨간 사각형을 오버레이하여 시각 데이터를 가립니다.

```java
ReplacementOptions optionsText = new ReplacementOptions("[redarea]");
optionsText.setFilters(new RedactionFilter[] {
    new PageRangeFilter(PageSeekOrigin.End, 0, 1), // Target the last page
    new PageAreaFilter(new java.awt.Point(300, 0), new java.awt.Dimension(300, 840)) // Right half of the page
});
```

```java
RegionReplacementOptions optionsImg = new RegionReplacementOptions(java.awt.Color.RED, new java.awt.Dimension(100, 100));
```

#### Step 4: Apply Redactions
`PageAreaRedaction`은 지정된 페이지 영역에 가리기를 적용하는 작업입니다.  
`PageAreaRedaction` 작업을 실행하여 텍스트와 이미지 가리기를 한 번에 수행합니다:

```java
RedactorChangeLog result = redactor.apply(new PageAreaRedaction(rx, optionsText, optionsImg));

if (result.getStatus() != RedactionStatus.Failed) {
    redactor.save("YOUR_OUTPUT_DIRECTORY/output.pdf");
}
```

#### Step 5: Cleanup Resources
항상 `Redactor`를 닫아 네이티브 리소스를 해제하고 메모리 누수를 방지하십시오:

```java
finally {
    redactor.close();
}
```

### 동일한 접근 방식으로 PPT 슬라이드를 가리는 방법?
워크플로우는 PDF 단계와 동일하며, 파일 확장자만 다릅니다. PPTX를 로드하고 동일한 정규식 및 영역 필터를 적용한 뒤, 가려진 프레젠테이션을 저장합니다.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/LOREMIPSUM_PPT");
```

## 실제 적용 사례
- **Legal Document Preparation** – 법원에 제출하기 전에 고객 이름, 사건 번호, 기밀 조항 등을 가립니다.  
- **Financial Reporting** – PDF와 슬라이드에서 계좌 번호, 이익률, 독점 공식 등을 숨깁니다.  
- **HR Audits** – 대량 문서 내보내기에서 직원 식별자를 제거하여 개인정보 보호법을 준수합니다.

## 성능 고려 사항
- **Close resources promptly** – 특히 대량 배치를 처리할 때 메모리 사용량을 낮게 유지하기 위해 리소스를 즉시 닫습니다.  
- **Optimize regex patterns** – 전체 문서를 불필요하게 스캔하는 과도하게 넓은 표현을 피합니다.  
- **Batch processing** – 스레드 풀을 사용하고 파일당 하나의 `Redactor` 인스턴스를 재사용하여 다중 코어 서버에서 처리량을 향상시킵니다.

## 일반적인 문제 및 해결책
`PageRangeFilter` 및 `PageAreaFilter`와 같은 필터는 특정 페이지 또는 영역에만 가리기를 제한합니다.

| 문제 | 원인 | 해결 방법 |
|-------|-------|-----|
| *Redaction not applied* | 필터가 잘못된 페이지/영역을 대상으로 함 | `PageRangeFilter` 및 `PageAreaFilter` 좌표를 확인하십시오. |
| *OutOfMemoryError* | 대용량 파일을 열어 둠 | 파일을 순차적으로 처리하거나 JVM 힙(`-Xmx`)을 늘리십시오. |
| *Regex matches unwanted text* | 패턴이 너무 일반적임 | 정규식을 다듬거나 단어 경계(`\b`)를 사용하십시오. |

## 자주 묻는 질문

**Q: pdf 텍스트 가리기와 단순히 텍스트를 숨기는 것의 차이점은 무엇인가요?**  
A: 가리기는 파일 구조에서 데이터를 영구적으로 제거하지만, 숨기기는 시각 레이어만 변경합니다.

**Q: GroupDocs.Redaction을 사용하여 비밀번호로 보호된 PDF를 가릴 수 있나요?**  
A: 예 – `Redactor` 인스턴스를 생성할 때 비밀번호를 제공하면 됩니다.

**Q: 저장하기 전에 가리기 결과를 미리 볼 수 있는 방법이 있나요?**  
A: 임시 위치에 `redactor.save("output.pdf")`를 사용해 저장하고 파일을 열어 검토하십시오.

**Q: 라이브러리가 DOCX나 XLSX와 같은 다른 형식을 지원하나요?**  
A: 물론입니다 – 동일한 API가 20개 이상의 지원 문서 형식에서 작동합니다.

**Q: 문제가 발생했을 때 어디에서 도움을 받을 수 있나요?**  
A: 지원이 필요하면 [GroupDocs Free Support](https://forum.groupdocs.com/c/redaction/33) 커뮤니티 포럼을 방문하십시오.

**마지막 업데이트:** 2026-07-01  
**테스트 환경:** GroupDocs.Redaction 24.9 for Java  
**작성자:** GroupDocs

## 관련 튜토리얼

- [GroupDocs.Redaction을 사용한 Java 텍스트 가리기 방법: 완전 가이드](/redaction/java/text-redaction/master-text-redaction-java-groupdocs-redaction-guide/)
- [how redact pdf java – GroupDocs.Redaction을 위한 PDF 전용 가리기 튜토리얼](/redaction/java/pdf-specific-redaction/)
- [Mask Sensitive Data Java – GroupDocs.Redaction으로 개인 정보 가리기](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)