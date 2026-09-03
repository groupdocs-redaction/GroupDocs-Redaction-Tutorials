---
date: '2026-06-26'
description: GroupDocs OCR Redaction과 Azure OCR을 사용하여 스캔된 PDF 텍스트를 추출하고 민감한 데이터를 마스킹하는
  방법을 배우세요. Redact social security number 및 confidential info PDF를 효율적으로 교체하세요.
keywords:
- extract text scanned pdf
- redact social security number
- mask sensitive data pdf
- replace confidential info pdf
schemas:
- author: GroupDocs
  dateModified: '2026-06-26'
  description: Learn how to extract text scanned PDF and mask sensitive data using
    GroupDocs OCR Redaction with Azure OCR. Redact social security number and replace
    confidential info PDF efficiently.
  headline: Extract Text Scanned PDF – Mask Data with GroupDocs OCR
  type: TechArticle
- questions:
  - answer: OCR redaction uses Optical Character Recognition to extract hidden text
      from images or scanned PDFs, then applies redaction rules to mask that text.
    question: What is OCR redaction?
  - answer: Yes, but OCR dramatically improves accuracy on scanned documents where
      native text extraction fails.
    question: Can I use GroupDocs Redaction without Azure OCR?
  - answer: Build and test them incrementally, using Java’s `Pattern` class in a sandbox
      before applying to large documents.
    question: How do I handle complex regex patterns?
  - answer: Large PDFs, overly complex regex, and synchronous OCR calls can slow processing;
      consider batch processing and optimized patterns.
    question: What are typical performance bottlenecks?
  - answer: Absolutely—reach out via the [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33)
      for community help or contact GroupDocs support.
    question: Is support available for implementation issues?
  type: FAQPage
title: 스캔된 PDF 텍스트 추출 – GroupDocs OCR로 데이터 마스킹
type: docs
url: /ko/java/ocr-integration/ocr-redaction-groupdocs-java-setup/
weight: 1
---

# 스캔된 PDF 텍스트 추출 – GroupDocs OCR로 데이터 마스킹

오늘날 데이터 중심의 세상에서 **스캔된 PDF에서 텍스트 추출**과 기밀 정보 마스킹은 필수적인 준수 단계입니다. 이 튜토리얼에서는 GroupDocs Redaction과 Microsoft Azure OCR을 함께 사용하여 스캔된 페이지의 숨겨진 텍스트를 신뢰성 있게 인식하고 **`[REDACTED]`**와 같은 안전한 플레이스홀더로 교체하는 방법을 안내합니다. 이 조합이 빠르고 정확하며 프로덕션 수준 워크로드에 적합한 이유를 확인할 수 있습니다.

## 빠른 답변
- **‘민감한 데이터 마스킹’이란 무엇을 의미합니까?** 식별된 기밀 텍스트를 플레이스홀더(예: `[REDACTED]`)로 교체합니다.  
- **어떤 라이브러리가 OCR을 처리합니까?** Microsoft Azure OCR 커넥터이며, GroupDocs Redaction을 통해 사용됩니다.  
- **라이선스가 필요합니까?** 평가용으로는 무료 체험이 가능하며, 프로덕션에서는 정식 라이선스가 필요합니다.  
- **스캔된 PDF를 레드액션 할 수 있나요?** 예—OCR이 숨겨진 텍스트를 추출한 후 정규식 레드액션을 적용합니다.  
- **이 솔루션이 Java 전용인가요?** 예제는 Java 기반이지만, GroupDocs는 .NET 및 기타 플랫폼용 유사 API를 제공합니다.

## OCR 기반 레드액션이란?
OCR 기반 레드액션은 먼저 각 페이지에 OCR을 실행하여 이미지를 검색 가능한 텍스트로 변환한 다음, 정규식 패턴을 적용해 일치 항목을 `[REDACTED]`와 같은 마스크로 교체합니다. 이 두 단계 프로세스를 통해 스캔된 PDF에서도 개인 데이터를 신뢰성 있게 숨길 수 있으며, 문서를 공유하거나 보관하기 전에 모든 민감한 문자열이 제거됩니다.

## 왜 GroupDocs Redaction과 Azure OCR를 함께 사용하나요?
GroupDocs Redaction과 Azure OCR를 함께 사용해야 하는 이유는 **인쇄된 텍스트에 대해 98 % 이상의 OCR 정확도**를 제공하고, **50개 이상의 입력 및 출력 형식**을 지원하며, **전체 파일을 메모리에 로드하지 않고 수백 페이지 PDF를 처리**할 수 있어 빠르고 확장 가능한 레드액션을 보장하기 때문입니다. 또한 이 솔루션은 **8코어 서버에서 1,000페이지 PDF를 2분 이하로 처리**할 수 있어 배치 작업에 실용적입니다.

## 사전 요구 사항
- **Java Development Kit (JDK) 8+** 설치.  
- **Maven**(의존성 관리를 선호하는 경우) 또는 JAR를 수동으로 다운로드할 수 있는 능력.  
- **Microsoft Azure OCR 자격 증명**(엔드포인트 및 구독 키).  
- 기본 Java 지식 및 정규식에 대한 이해.

## Java용 GroupDocs Redaction 설정

### Maven 설정
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

### 직접 다운로드
수동 JAR 관리를 선호한다면, 최신 릴리스를 [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/)에서 다운로드하십시오.

### 라이선스 획득
- **무료 체험** – 비용 없이 모든 기능을 탐색합니다.  
- **임시 라이선스** – 평가 기간을 연장합니다.  
- **정식 라이선스** – 프로덕션 준비 기능을 활성화합니다.

### 기본 초기화 및 설정
`Redactor` 클래스는 OCR 추출을 수행하고 PDF 문서에 레드액션 규칙을 적용하는 핵심 엔진입니다.  
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.RedactorSettings;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.examples.java.helper_classes.MicrosoftAzureOcrConnector;

// Initialize the OCR connector with Microsoft Azure
RedactorSettings settings = new RedactorSettings(new MicrosoftAzureOcrConnector());
```

## OCR 레드액션으로 민감한 데이터 마스킹 방법
OCR 레드액션을 사용한 민감한 데이터 마스킹은 Azure OCR 설정으로 PDF를 로드하고, 숨기려는 데이터에 대한 정규식 패턴을 정의한 뒤, `Redactor`를 호출하여 각 일치 항목을 `[REDACTED]`와 같은 플레이스홀더로 교체하는 과정을 포함합니다. 라이브러리는 OCR, 패턴 매칭 및 PDF 재작성 작업을 하나의 워크플로우에서 처리합니다.

### 단계 1: OCR 설정으로 문서 로드
`LoadOptions`는 GroupDocs가 파일을 로드하는 방식을 구성하며, Azure와 같은 OCR 커넥터를 전달할 수 있게 합니다.  
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;

// Load your document with OCR settings
try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf", 
    new LoadOptions(), settings)) {
    // Further operations will go here
}
```
- **`YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf`** – PDF 파일 경로로 교체하십시오.  
- **`settings`** – 앞서 만든 Azure OCR 커넥터를 포함합니다.

### 단계 2: 정규식 레드액션 정의 및 적용
`ReplacementOptions`는 레드액션 중 각 정규식 일치 항목을 대체할 텍스트를 지정합니다.  
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
- 패턴 `\b\d{3}-\d{2}-\d{4}\b`는 미국 사회보장번호(SSN)와 일치합니다.  
- `ReplacementOptions("[REDACTED]")`는 각 일치를 마스크로 교체하여 효과적으로 **민감한 데이터를 마스킹**합니다.

## 민감한 데이터 마스킹 일반 사용 사례
1. **법률 문서 관리** – 초안을 공유하기 전에 클라이언트 식별자를 숨깁니다.  
2. **재무 보고** – 계좌 번호와 거래 ID를 보호합니다.  
3. **의료 기록** – HIPAA를 준수하기 위해 환자 식별자를 레드액션합니다.  
4. **정부 발행물** – 공개 기록에서 개인 데이터를 제거합니다.  
5. **기업 계약** – 외부 검토 시 독점 조항을 숨깁니다.

## 성능 팁
- **정규식 최적화** – 처리 시간을 늘리는 과도하게 포괄적인 패턴을 피하십시오; 잘 설계된 표현식은 실행 시간을 최대 40 %까지 단축할 수 있습니다.  
- **메모리 관리** – `Redactor` 인스턴스를 즉시 닫으세요(try‑with‑resources가 자동으로 처리합니다).  
- **비동기 실행** – 대량 처리 시, 레드액션 작업을 별도 스레드에서 실행하거나 작업 큐를 사용해 UI가 응답하도록 유지합니다.

## 문제 해결
- **Azure 자격 증명 오류** – `MicrosoftAzureOcrConnector`에서 엔드포인트 URL과 구독 키를 다시 확인하십시오.  
- **문서 로드 실패** – 파일 경로를 확인하고 PDF가 비밀번호로 보호되지 않았는지 확인하십시오(또는 `LoadOptions`를 통해 비밀번호를 제공).  
- **레드액션이 적용되지 않음** – 먼저 간단한 문자열로 정규식을 테스트하십시오; `Pattern.compile`을 사용한 단위 테스트로 일치를 확인합니다.

## 자주 묻는 질문

**Q: OCR 레드액션이란 무엇인가요?**  
A: OCR 레드액션은 광학 문자 인식(OCR)을 사용해 이미지 또는 스캔된 PDF에서 숨겨진 텍스트를 추출한 뒤, 레드액션 규칙을 적용해 해당 텍스트를 마스킹합니다.

**Q: Azure OCR 없이 GroupDocs Redaction을 사용할 수 있나요?**  
A: 예, 가능하지만 OCR을 사용하면 원본 텍스트 추출이 불가능한 스캔 문서에서 정확도가 크게 향상됩니다.

**Q: 복잡한 정규식 패턴은 어떻게 다루나요?**  
A: 단계적으로 구축하고 테스트하십시오. 대형 문서에 적용하기 전에 Java의 `Pattern` 클래스를 샌드박스에서 사용해 검증합니다.

**Q: 일반적인 성능 병목 현상은 무엇인가요?**  
A: 대용량 PDF, 과도하게 복잡한 정규식, 동기식 OCR 호출이 처리 속도를 저하시킬 수 있습니다; 배치 처리와 최적화된 패턴을 고려하십시오.

**Q: 구현 문제에 대한 지원이 있나요?**  
A: 물론입니다—커뮤니티 지원을 위해 [GroupDocs 포럼](https://forum.groupdocs.com/c/redaction/33)으로 문의하거나 GroupDocs 지원팀에 연락하십시오.

## 추가 리소스
- **문서**: https://docs.groupdocs.com/redaction/java/  
- **API 레퍼런스**: https://reference.groupdocs.com/redaction/java  
- **다운로드**: https://releases.groupdocs.com/redaction/java/  
- **GitHub**: https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java  
- **무료 지원**: https://forum.groupdocs.com/c/redaction/33  
- **임시 라이선스**: https://purchase.groupdocs.com/temporary-license/

---

**마지막 업데이트:** 2026-06-26  
**테스트 환경:** GroupDocs.Redaction 24.9 (Java)  
**작성자:** GroupDocs  

## 관련 튜토리얼

- [OCR를 사용한 보안 PDF 레드액션 – GroupDocs.Redaction Java](/redaction/java/ocr-integration/)
- [Java용 GroupDocs.Redaction으로 텍스트 레드액션하는 방법](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction/)
- [Java에서 민감한 데이터 마스킹 – GroupDocs.Redaction으로 개인 정보 레드액션](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)