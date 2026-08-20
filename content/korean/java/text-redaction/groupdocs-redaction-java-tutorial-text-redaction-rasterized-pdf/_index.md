---
date: '2026-08-20'
description: GroupDocs.Redaction Java를 사용하여 텍스트를 가리는 방법을 배우고, rasterized PDF로 저장하고,
  exact phrases를 교체하며, custom PDF settings를 적용하는 방법을 알아보세요.
keywords:
- how to redact text
- save pdf as image
- convert pdf to image
lastmod: '2026-08-20'
og_description: GroupDocs.Redaction Java를 사용하여 텍스트를 가리는 방법. 이 가이드는 exact phrase replacement,
  rasterized PDF creation, 그리고 PDF/A‑1a compliance를 몇 단계로 보여줍니다.
og_image_alt: Guide showing GroupDocs.Redaction Java code to redact text and create
  rasterized PDF
og_title: GroupDocs.Redaction Java 라이브러리를 사용하여 텍스트를 가리는 방법
schemas:
- author: GroupDocs
  dateModified: '2026-08-20'
  description: Learn how to redact text with GroupDocs.Redaction Java, save as rasterized
    PDF, replace exact phrases, and apply custom PDF settings.
  headline: How to redact text with GroupDocs.Redaction Java
  type: TechArticle
- description: Learn how to redact text with GroupDocs.Redaction Java, save as rasterized
    PDF, replace exact phrases, and apply custom PDF settings.
  name: How to redact text with GroupDocs.Redaction Java
  steps:
  - name: '**Sensitive data redaction** – automatically hide personal identifiers
      before sharing contracts.'
    text: '**Sensitive data redaction** – automatically hide personal identifiers
      before sharing contracts.'
  - name: '**Document archiving** – convert finalized reports to rasterized PDF/A
      for long‑term compliance.'
    text: '**Document archiving** – convert finalized reports to rasterized PDF/A
      for long‑term compliance.'
  - name: '**Bulk content update** – replace outdated terminology across hundreds
      of files with a single script.'
    text: '**Bulk content update** – replace outdated terminology across hundreds
      of files with a single script.'
  type: HowTo
- questions:
  - answer: Add the GroupDocs repository and the `groupdocs-redaction` dependency
      to your `pom.xml` as shown in the Maven Setup section.
    question: How do I install GroupDocs.Redaction in a Maven project?
  - answer: Yes, GroupDocs.Redaction supports PDF, DOCX, PPTX, and many other formats.
    question: Can I redact text from PDF files using this library?
  - answer: The `RedactorChangeLog` will return a status of `Failed`. Verify the phrase’s
      spelling and case sensitivity.
    question: What happens if the exact phrase isn’t found?
  - answer: Process them in smaller page ranges, enable rasterization only where needed,
      and always close the `Redactor` to free resources.
    question: How can I handle very large documents efficiently?
  - answer: Absolutely. Use `options.getRasterization().setPageIndex()` and `setPageCount()`
      to target the exact pages you want to rasterize.
    question: Is it possible to save rasterized PDFs with specific page ranges?
  type: FAQPage
tags:
- text redaction
- GroupDocs.Redaction
- Java PDF processing
title: GroupDocs.Redaction Java로 텍스트 가리기 방법
type: docs
url: /ko/java/text-redaction/groupdocs-redaction-java-tutorial-text-redaction-rasterized-pdf/
weight: 1
---

# GroupDocs.Redaction Java로 텍스트 가리기

현대 애플리케이션에서 문서의 **텍스트 가리기**를 수행하면서 워크플로를 빠르고 규정 준수하게 유지하는 것은 개발자, 감사인 및 컴플라이언스 담당자에게 빈번한 과제입니다. 이 튜토리얼에서는 GroupDocs.Redaction for Java를 사용하여 정확한 구문을 찾고, 보안 오버레이로 교체한 다음, 결과를 래스터화된 PDF/A‑1a 문서로 내보내는 방법을 단계별로 안내합니다—아카이브 또는 법적 배포에 적합합니다.

## 빠른 답변
- **Redaction의 기본 클래스는 무엇인가요?** `Redactor`  
- **색상 오버레이로 구문을 교체할 수 있나요?** 예, `ExactPhraseRedaction` 및 `ReplacementOptions`를 사용합니다.  
- **래스터화된 PDF를 생성하려면 어떻게 해야 하나요?** `SaveOptions.getRasterization().setEnabled(true)`를 통해 래스터화를 활성화합니다.  
- **예제에서 사용된 PDF 컴플라이언스 수준은 무엇인가요?** `PdfComplianceLevel.PdfA1a`.  
- **프로덕션 사용에 라이선스가 필요합니까?** 프로덕션 배포에는 유효한 GroupDocs.Redaction 라이선스가 필요합니다.

## Java에서 텍스트 가리기란?
`Redaction`은 파일에서 민감한 내용을 영구적으로 제거하거나 가리는 것으로, 이후 복구하거나 읽을 수 없게 합니다. GroupDocs.Redaction을 사용하면 정확한 구문(예: 사회보장번호 또는 기밀 프로젝트 코드)을 프로그래밍 방식으로 검색하고, 빨간 오버레이, 검은 박스 또는 사용자 정의 시각 요소로 교체하여 원본 데이터가 복구되지 않도록 보장합니다.

## Java용 GroupDocs.Redaction을 사용하는 이유
GroupDocs.Redaction은 **30개 이상의 입력 및 출력 포맷**(PDF, DOCX, PPTX, XLSX, HTML 및 이미지 형식)을 지원하며 전체 파일을 메모리에 로드하지 않고 수백 페이지 문서를 처리할 수 있습니다. 정확한 구문 매칭 알고리즘은 일반 키워드 검색에 비해 95 % 이상 false positive를 감소시키며, 내장된 래스터화 엔진을 통해 장기 보존을 위한 완전 이미지 기반 PDF/A‑1a 파일을 생성할 수 있습니다.

## 사전 요구 사항
- **GroupDocs.Redaction for Java** (v24.9 이상).  
- **Java Development Kit (JDK) 8+**.  
- IntelliJ IDEA, Eclipse, NetBeans와 같은 IDE.  
- 의존성 관리를 위한 Maven.  

### 필수 라이브러리 및 의존성
- GroupDocs.Redaction for Java – 리포지토리와 의존성을 `pom.xml`에 추가합니다 (Maven 설정 섹션 참고).  
- 선택 사항: 선호하는 로깅 프레임워크(SLF4J, Log4j 등).  

### 지식 사전 요구 사항
- 기본 Java 문법 및 파일 I/O.  
- Maven의 `pom.xml` 구조에 대한 이해.  

## GroupDocs.Redaction for Java 설정
### Maven 설정
Add the GroupDocs repository and the `groupdocs-redaction` dependency to your `pom.xml` file:

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
Alternatively, you can download the latest version directly from [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### 라이선스 획득
- **무료 체험** – 라이선스 키 없이 API를 탐색합니다.  
- **임시 라이선스** – 장기 평가에 사용합니다.  
- **전체 라이선스** – 프로덕션 환경에 필요합니다.  

### 기본 초기화 및 설정
`Redactor` 클래스는 모든 가리기 작업의 진입점입니다. 문서를 로드하고, 가리기 규칙을 적용한 뒤 결과를 저장합니다.

```java
import com.groupdocs.redaction.Redactor;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
```

## 텍스트 가리기 – 정확한 구문 예제
`Redactor`는 문서를 로드하고 가리기 규칙을 적용하는 기본 클래스입니다. `ExactPhraseRedaction`은 특정 문자열과 일치하는 규칙을 정의합니다. 이 예제는 파일을 로드하고, `ExactPhraseRedaction` 규칙을 생성한 뒤, 한 단계로 가리기를 실행하는 방법을 보여주며, 개발자를 위한 간결한 워크플로를 제공하면서 원본 콘텐츠를 영구적으로 가립니다.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.ReplacementOptions;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
```

## 래스터화된 PDF로 저장하는 방법
`SaveOptions`는 문서 저장 방식을 제어하는 설정 객체입니다. 래스터화 기능을 활성화하고 PDF/A‑1a 컴플라이언스를 선택하면 각 페이지가 비트맵으로 렌더링되는 이미지 전용 PDF를 생성하여 아카이브 표준을 충족하고 텍스트 추출을 방지할 수 있습니다.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
try {
    RedactorChangeLog result = redactor.apply(new ExactPhraseRedaction(
        "John Doe", new ReplacementOptions(java.awt.Color.RED)));
    
    if (result.getStatus() != RedactionStatus.Failed) {
        // Successfully redacted the text
    }
} finally { 
    redactor.close(); 
}
```

## 실용적인 적용 사례
1. **민감 데이터 가리기** – 계약서를 공유하기 전에 개인 식별자를 자동으로 숨깁니다.  
2. **문서 아카이빙** – 최종 보고서를 장기 컴플라이언스를 위해 래스터화된 PDF/A로 변환합니다.  
3. **대량 콘텐츠 업데이트** – 수백 개 파일의 오래된 용어를 하나의 스크립트로 교체합니다.  

## 성능 고려 사항
- **`Redactor`를 닫아** 각 작업 후 파일 핸들과 메모리를 해제합니다.  
- **배치 처리** – 파일 목록을 로드하고 반복하며, 가능하면 단일 `Redactor` 인스턴스를 재사용합니다.  
- **리소스 모니터링** – 대규모 가리기 작업 중 CPU와 힙 사용량을 확인하려면 Java 프로파일링 도구를 사용합니다.  

## 자주 묻는 질문

**Q: Maven 프로젝트에 GroupDocs.Redaction을 어떻게 설치하나요?**  
A: Maven 설정 섹션에 표시된 대로 GroupDocs 리포지토리와 `groupdocs-redaction` 의존성을 `pom.xml`에 추가합니다.

**Q: 이 라이브러리를 사용해 PDF 파일의 텍스트를 가릴 수 있나요?**  
A: 예, GroupDocs.Redaction은 PDF, DOCX, PPTX 등 다양한 포맷을 지원합니다.

**Q: 정확한 구문을 찾지 못하면 어떻게 되나요?**  
A: `RedactorChangeLog`는 `Failed` 상태를 반환합니다. 구문의 철자와 대소문자를 확인하세요.

**Q: 매우 큰 문서를 효율적으로 처리하려면 어떻게 해야 하나요?**  
A: 작은 페이지 범위로 나누어 처리하고, 필요할 때만 래스터화를 활성화하며, 항상 `Redactor`를 닫아 리소스를 해제합니다.

**Q: 특정 페이지 범위로 래스터화된 PDF를 저장할 수 있나요?**  
A: 물론입니다. `options.getRasterization().setPageIndex()`와 `setPageCount()`를 사용해 래스터화하려는 정확한 페이지를 지정하세요.

## 결론
이제 GroupDocs.Redaction Java를 사용한 **텍스트 가리기**와 **래스터화된 PDF 저장**에 대한 완전한 엔드‑투‑엔드 가이드를 보유하게 되었습니다. 이 단계를 따르면 민감 정보를 보호하고, 엄격한 컴플라이언스 표준을 충족하며, 규모에 맞게 Java 서비스를 효율적으로 유지할 수 있습니다.

**다음 단계**  
- API를 더 깊이 탐색하려면 [공식 문서](https://docs.groupdocs.com/redaction/java/)를 확인하세요.  
- `RegexRedaction` 및 `ImageRedaction`과 같은 다른 가리기 유형을 실험해 보세요.  
- 팁과 모범 사례를 위해 [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) 커뮤니티에 참여하세요.

---

**마지막 업데이트:** 2026-08-20  
**테스트 환경:** GroupDocs.Redaction Java 24.9  
**작성자:** GroupDocs

```java
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.options.PdfComplianceLevel;
```

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
try {
    SaveOptions options = new SaveOptions();

    // Enable rasterization for converting pages into images.
    options.getRasterization().setEnabled(true);
    
    // Set the starting page and count for rasterization.
    options.getRasterization().setPageIndex(5);
    options.getRasterization().setPageCount(1);

    // Define PDF compliance level.
    options.getRasterization().setCompliance(PdfComplianceLevel.PdfA1a);

    // Append a suffix to avoid filename conflicts.
    options.setAddSuffix(true);

    // Save the document with these configurations.
    redactor.save(options);
} finally { 
    redactor.close(); 
}
```

## 관련 튜토리얼

- [GroupDocs.Redaction for Java로 텍스트 가리기](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction/)
- [Java 텍스트 가리기 튜토리얼: GroupDocs.Redaction 가이드](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction-guide/)