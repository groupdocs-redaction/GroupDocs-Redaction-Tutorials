---
date: '2026-08-31'
description: GroupDocs.Redaction for Java를 사용하여 PDF를 레드랙션하는 방법을 배우고, redaction policies를
  만들고, annotations를 제거하며, metadata를 programmatic하고 compliant한 방식으로 삭제하는 방법을 알아보세요.
keywords:
- how to redact pdf
- erase metadata pdf
- remove annotations java
- GroupDocs.Redaction Java
- document redaction
lastmod: '2026-08-31'
og_description: GroupDocs.Redaction for Java를 사용하여 PDF를 레드랙션하는 방법. policies를 만들고,
  annotations를 제거하며, metadata를 빠르고 안전하게 삭제합니다.
og_image_alt: Guide showing how to redact PDF files with GroupDocs.Redaction in Java
og_title: GroupDocs.Redaction for Java를 사용하여 PDF를 레드랙션하는 방법
schemas:
- author: GroupDocs
  dateModified: '2026-08-31'
  description: Learn how to redact PDF using GroupDocs.Redaction for Java, create
    redaction policies, remove annotations, and erase metadata in a programmatic,
    compliant way.
  headline: How to redact PDF with GroupDocs.Redaction for Java
  type: TechArticle
- description: Learn how to redact PDF using GroupDocs.Redaction for Java, create
    redaction policies, remove annotations, and erase metadata in a programmatic,
    compliant way.
  name: How to redact PDF with GroupDocs.Redaction for Java
  steps:
  - name: configure redactions
    text: 'Configure the redactions using different classes provided by GroupDocs.Redaction:'
  - name: save redaction policy
    text: 'Save the configured policy as an XML file:'
  - name: create exact phrase redaction
    text: 'Implement an exact phrase redaction:'
  - name: create regex redaction
    text: 'Define a regex‑based redaction:'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction is a Java library that programmatically removes or
      replaces sensitive content in PDFs and other document formats.
    question: What is GroupDocs.Redaction?
  - answer: Add the Maven dependency, obtain a trial license, and follow the initialization
      steps shown above.
    question: How do I get started with GroupDocs.Redaction?
  - answer: Yes—use exact‑phrase redactions, regular‑expression redactions, or the
      built‑in metadata removal classes.
    question: Can I customize redaction patterns in GroupDocs.Redaction?
  - answer: Absolutely—save your `RedactionPolicy` as an XML file and load it later
      for batch processing.
    question: Is it possible to save and reuse redaction configurations?
  - answer: Apply only required redactions, tune Java heap size, and craft efficient
      regex patterns to minimise CPU usage.
    question: What are the best practices for optimizing performance with GroupDocs.Redaction?
  type: FAQPage
tags:
- redact PDF
- GroupDocs.Redaction
- Java document processing
- erase metadata pdf
- remove annotations java
title: GroupDocs.Redaction for Java를 사용하여 PDF를 레드랙션하는 방법
type: docs
url: /ko/java/advanced-redaction/master-redaction-groupdocs-java-guide/
weight: 1
---

# GroupDocs.Redaction for Java를 사용한 PDF 마스킹 방법

오늘날 데이터‑드리븐 세계에서 PDF 파일 내부의 기밀 정보를 보호하는 것은 절대 양보할 수 없는 요구사항입니다. 이 튜토리얼에서는 GroupDocs.Redaction for Java를 사용하여 PDF 문서를 프로그래밍 방식으로 **PDF 마스킹 방법**을 보여주며, 정책 생성, 주석 제거 및 메타데이터 삭제를 다룹니다. 여러 PDF에 적용할 수 있는 재사용 가능한 XML 마스킹 정책을 얻어 GDPR, HIPAA 및 기타 규정을 준수할 수 있습니다.

## 빠른 답변
- **GroupDocs.Redaction의 주요 목적은 무엇입니까?** PDF 및 기타 문서 형식에서 민감한 콘텐츠를 프로그래밍 방식으로 마스킹합니다.  
- **Java로 주석을 제거할 수 있나요?** 예—`DeleteAnnotationRedaction` 클래스를 사용합니다 (remove annotations java).  
- **개발에 라이선스가 필요합니까?** 테스트용으로는 무료 체험 또는 임시 라이선스로 충분하지만, 프로덕션에서는 정식 라이선스가 필요합니다.  
- **지원되는 Java 버전은 무엇입니까?** JDK 8 이상.  
- **XML 정책 파일은 어디에서 찾을 수 있나요?** 코드에서 출력 경로를 정의하고 `policy.save(...)`를 호출합니다.

`DeleteAnnotationRedaction` 클래스는 주석, 강조 표시 또는 스탬프와 같은 주석 객체를 PDF에서 제거합니다.  
`RedactionPolicy` 클래스는 XML 파일에 저장하거나 로드할 수 있는 마스킹 규칙 컬렉션을 나타냅니다.

## 마스킹 정책이란 무엇이며 마스킹 정책을 만드는 방법은?
마스킹 정책은 XML 기반 규칙 집합으로, GroupDocs.Redaction에 PDF에서 숨기거나 삭제하거나 교체할 텍스트, 패턴, 주석 또는 메타데이터를 정확히 지정합니다. 정책을 한 번 정의하고 XML 파일로 저장하면 코드를 다시 작성하지 않고도 여러 PDF에 동일한 **민감한 정보 마스킹**을 적용할 수 있습니다.

## Java용 GroupDocs.Redaction을 사용하는 이유는?
GroupDocs.Redaction은 **메모리 효율적인 엔진**으로 500페이지가 넘는 파일도 150 MB 이하의 RAM으로 처리합니다. DOCX, XLSX, PPTX, HTML 및 일반 이미지 형식을 포함한 **30개 이상의 입력 및 출력 형식**을 지원하며 GDPR 및 HIPAA에 대한 내장 컴플라이언스 기능을 제공합니다. 또한 라이브러리는 정확한 구문, 정규식, 주석 및 메타데이터 마스킹에 대한 세밀한 제어를 제공하여 Java 개발자에게 가장 다재다능한 솔루션이 됩니다.

## 사전 요구 사항
- **라이브러리 및 종속성** – Maven을 통해 프로젝트에 GroupDocs.Redaction을 추가하거나 JAR 파일을 직접 다운로드합니다.  
- **Java 환경** – JDK 8 이상 설치 및 구성.  
- **기본 지식** – Java 문법 및 정규식에 익숙하면 정책 생성 속도가 빨라집니다.

## Java용 GroupDocs.Redaction 설정

### 설치 정보
**Maven:**  
GroupDocs.Redaction을 Maven에 통합하려면 `pom.xml`에 다음을 추가합니다:

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

**직접 다운로드:**  
또는 최신 버전을 [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/)에서 다운로드합니다.

### 라이선스 획득
무료 체험으로 시작하거나 임시 라이선스를 받아 모든 기능을 살펴볼 수 있습니다. 장기 사용을 위해서는 정식 라이선스를 구매하십시오.

**기본 초기화:**  
프로젝트에서 GroupDocs.Redaction을 초기화하려면:

```java
import com.groupdocs.redaction.Redactor;

public class RedactionSetup {
    public static void main(String[] args) {
        // Initialize the Redactor object with your document path
        try (Redactor redactor = new Redactor("path/to/your/document.pdf")) {
            // Perform operations here
        }
    }
}
```

## 구현 가이드

### 마스킹 정책 만들기: 마스킹 정책 생성 및 저장
마스킹 구성을 로드하고 원하는 마스킹 객체를 추가한 뒤 정책을 XML 파일로 저장합니다. 이 두 단계 프로세스를 통해 매번 정책을 재구성하지 않고도 여러 PDF에 동일한 규칙을 재사용할 수 있습니다.

#### 개요
이 기능을 사용하면 정확한 구문, 정규식, 메타데이터 삭제와 같은 다양한 유형의 마스킹을 구성할 수 있습니다. 그런 다음 이러한 구성을 XML 파일로 저장하여 나중에 사용할 수 있습니다.

##### 단계 1: 마스킹 구성
GroupDocs.Redaction에서 제공하는 다양한 클래스를 사용하여 마스킹을 구성합니다:

```java
import com.groupdocs.redaction.RedactionPolicy;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
import com.groupdocs.redaction.redactions.RegexRedaction;
import com.groupdocs.redaction.redactions.DeleteAnnotationRedaction;
import com.groupdocs.redaction.redactions.EraseMetadataRedaction;
import com.groupdocs.redaction.options.ReplacementOptions;
import java.awt.Color;

// Configure redactions
RedactionPolicy policy = new RedactionPolicy(new Redaction[] {
    // Exact Phrase Redaction replaces "Redaction" with "[Product]"
    new ExactPhraseRedaction("Redaction", new ReplacementOptions("[Product]")),
    
    // Regex Redaction searches for specific patterns and replaces them with a blue rectangle
    new RegexRedaction("\\d{2}\\s*\\d{2}[^\\d]*\\d{6}", new ReplacementOptions(Color.BLUE)),
    
    // Delete Annotation Redaction removes all annotations
    new DeleteAnnotationRedaction(),
    
    // Erase Metadata Redaction deletes all metadata
    new EraseMetadataRedaction(MetadataFilters.All)
});
```

##### 단계 2: 마스킹 정책 저장
구성된 정책을 XML 파일로 저장합니다:

```java
// Define your output directory path
String outputPath = YOUR_DOCUMENT_DIRECTORY + "YOUR_OUTPUT_DIRECTORY/POLICY_SAVE.xml";
policy.save(outputPath);
```

### Java에서 주석 제거: 정확한 구문 마스킹 구성
PDF를 로드하고 숨기려는 정확한 구문을 정의한 뒤 마스킹을 정책에 연결합니다. 해당 구문은 검은 상자 또는 사용자 정의 텍스트로 교체됩니다.

#### 개요
이 기능은 특정 구문을 마스킹 대상으로 지정하고, 미리 정의된 텍스트로 교체합니다.

##### 단계 1: 정확한 구문 마스킹 생성
정확한 구문 마스킹을 구현합니다:

```java
import com.groupdocs.redaction.Redaction;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
import com.groupdocs.redaction.options.ReplacementOptions;

// Configure the redaction for a specific phrase
Redaction exactPhraseRedaction = new ExactPhraseRedaction(
    "Redaction", // Phrase to be redacted
    new ReplacementOptions("[Product]") // Replacement text
);
```

### Java에서 주석 제거: 정규식 마스킹 구성
정규식을 사용하여 사회보장번호나 신용카드 형식과 같은 패턴을 찾아 자동으로 교체하거나 삭제합니다.

#### 개요
정규식을 사용하여 문서 내 패턴을 식별하고 교체합니다.

##### 단계 1: 정규식 마스킹 생성
정규식 기반 마스킹을 정의합니다:

```java
import com.groupdocs.redaction.Redaction;
import com.groupdocs.redaction.redactions.RegexRedaction;
import com.groupdocs.redaction.options.ReplacementOptions;
import java.awt.Color;

// Implement regex redaction for pattern matching
Redaction regexRedaction = new RegexRedaction(
    "\\d{2}\\s*\\d{2}[^\\d]*\\d{6}", // Pattern to match
    new ReplacementOptions(Color.BLUE) // Replace matches with blue rectangle
);
```

## 실용적인 적용 사례
1. **기밀 문서 관리** – 법률 및 인사 문서에서 이름, 사회보장번호, 재무 데이터와 같은 **민감한 정보 마스킹**을 자동으로 수행합니다.  
2. **컴플라이언스 자동화** – 고객 커뮤니케이션에서 개인 식별자를 제거하여 GDPR, HIPAA 및 기타 규제 요구사항을 충족합니다.  
3. **테스트용 데이터 익명화** – 정규식 기반 마스킹을 적용하여 문서 구조를 유지하면서 테스트 데이터 세트를 익명화합니다.

## 성능 고려 사항
- **마스킹 최적화** – 처리 시간을 최소화하려면 필요한 마스킹만 적용합니다.  
- **메모리 관리** – Java 힙 사용량을 모니터링합니다; GroupDocs.Redaction은 전체 파일을 메모리에 로드하지 않고 페이지를 스트리밍합니다.  
- **효율적인 정규식 패턴** – 과도한 백트래킹 및 CPU 부하를 피하기 위해 간결한 정규식을 작성합니다.

## 일반적인 문제 및 해결책
| 문제 | 원인 | 해결 방법 |
|-------|-------|-----|
| 마스킹이 적용되지 않음 | 잘못된 구문 또는 대소문자 구분 | 대소문자 구분 없는 옵션을 사용하거나 정확한 텍스트 문자열을 확인하십시오 |
| 주석이 남아 있음 | `DeleteAnnotationRedaction`이 정책에 추가되지 않음 | 정책 배열에 `new DeleteAnnotationRedaction()`을 추가하십시오 |
| 대용량 PDF 처리 속도 저하 | 불필요한 정규식 스캔 | 정규식 범위를 제한하거나 패턴 적용 전에 페이지를 사전 필터링하십시오 |

## 자주 묻는 질문

**Q: GroupDocs.Redaction이란 무엇인가요?**  
A: GroupDocs.Redaction은 PDF 및 기타 문서 형식에서 민감한 콘텐츠를 프로그래밍 방식으로 제거하거나 교체하는 Java 라이브러리입니다.

**Q: GroupDocs.Redaction을 어떻게 시작하나요?**  
A: Maven 의존성을 추가하고 체험 라이선스를 획득한 뒤 위에 표시된 초기화 단계를 따라 진행합니다.

**Q: GroupDocs.Redaction에서 마스킹 패턴을 맞춤 설정할 수 있나요?**  
A: 예—정확한 구문 마스킹, 정규식 마스킹 또는 내장 메타데이터 제거 클래스를 사용할 수 있습니다.

**Q: 마스킹 구성을 저장하고 재사용할 수 있나요?**  
A: 물론입니다—`RedactionPolicy`를 XML 파일로 저장하고 나중에 배치 처리에 로드하면 됩니다.

**Q: GroupDocs.Redaction의 성능을 최적화하기 위한 모범 사례는 무엇인가요?**  
A: 필요한 마스킹만 적용하고 Java 힙 크기를 조정하며 효율적인 정규식 패턴을 작성하여 CPU 사용량을 최소화합니다.

## 리소스
- [문서](https://docs.groupdocs.com/redaction/java/)
- [API 레퍼런스](https://reference.groupdocs.com/redaction/java)
- [다운로드](https://releases.groupdocs.com/redaction/java/)
- [GitHub 저장소](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
- [무료 지원 포럼](https://forum.groupdocs.com/c/redaction/33)
- [임시 라이선스](https://purchase.groupdocs.com/temporary-license/)

---

**마지막 업데이트:** 2026-08-31  
**테스트 환경:** GroupDocs.Redaction 24.9 for Java  
**작성자:** GroupDocs

## 관련 튜토리얼

- [GroupDocs.Redaction Java를 사용한 주석 제거 방법](/redaction/java/annotation-redaction/)
- [GroupDocs.Redaction을 사용한 메타데이터 마스킹 Java 방법](/redaction/java/metadata-redaction/)
- [Java에서 PDF 마스킹 – GroupDocs.Redaction을 위한 PDF 전용 마스킹 튜토리얼](/redaction/java/pdf-specific-redaction/)