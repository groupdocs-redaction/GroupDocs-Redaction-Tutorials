---
date: '2026-10-22'
description: GroupDocs Redaction Java를 설정하는 방법을 배우고, 정확한 구문 가리기와 고급 rasterization
  옵션으로 문서를 보호하세요.
keywords:
- setup groupdocs redaction java
- exact phrase redaction java
- advanced rasterization groupdocs
lastmod: '2026-10-22'
og_description: groupdocs redaction java를 사용해 정확한 구문을 안전하게 가리고 고급 rasterization을 적용하세요.
  Java developers를 위한 step‑by‑step guide를 따라보세요.
og_image_alt: Guide to configure GroupDocs Redaction Java with phrase redaction and
  rasterization
og_title: 정확한 구문 가리기를 위한 groupdocs redaction java 설정
schemas:
- author: GroupDocs
  dateModified: '2026-10-22'
  description: Learn how to set up GroupDocs Redaction Java, then protect documents
    with exact phrase redaction and advanced rasterization options.
  headline: Setup groupdocs redaction java for exact phrase redaction
  type: TechArticle
- description: Learn how to set up GroupDocs Redaction Java, then protect documents
    with exact phrase redaction and advanced rasterization options.
  name: Setup groupdocs redaction java for exact phrase redaction
  steps:
  - name: '**Load your document** – Use the `Redactor` constructor with the file path.'
    text: '**Load your document** – Use the `Redactor` constructor with the file path.'
  - name: '**Apply the redaction** – Create an `ExactPhraseRedaction` object and pass
      a `ReplacementOptions` instance. The `ExactPhraseRedaction` class is the API
      component that identifies the exact phrase and ties it to the replacement logic.
      `ReplacementOptions` defines the text, symbol, or image that will appear in
      place of the original phrase.'
    text: '**Apply the redaction** – Create an `ExactPhraseRedaction` object and pass
      a `ReplacementOptions` instance. The `ExactPhraseRedaction` class is the API
      component that identifies the exact phrase and ties it to the replacement logic.
      `ReplacementOptions` defines the text, symbol, or image that will appear in
      place of the original phrase.'
  - name: '**Configure save options** – Enable rasterization and add the desired advanced
      options.'
    text: '**Configure save options** – Enable rasterization and add the desired advanced
      options.'
  - name: '**Key configuration options**'
    text: '**Key configuration options**'
  type: HowTo
- questions:
  - answer: Pass any string you like to `ReplacementOptions`; it will replace the
      matched phrase verbatim.
    question: How do I customize the replacement text in exact phrase redaction?
  - answer: Yes, GroupDocs.Redaction supports PDF, PPTX, and several other formats—just
      verify that the specific raster options are available for the chosen type.
    question: Can I use advanced rasterization for non‑DOCX files?
  - answer: Double‑check that the path is absolute or correctly relative to your project’s
      working directory, and ensure the file has read/write permissions.
    question: What if I encounter errors with file paths in my code?
  - answer: Absolutely. Create multiple `ExactPhraseRedaction` instances and apply
      them sequentially before saving.
    question: Is there a way to redact multiple phrases at once?
  - answer: Process the document in sections or use the streaming APIs provided by
      the library to keep memory usage low.
    question: How do I handle large documents efficiently with GroupDocs.Redaction?
  type: FAQPage
tags:
- redaction java
- groupdocs redaction
- document security
- exact phrase redaction
- rasterization
title: 정확한 구문 가리기를 위한 groupdocs redaction java 설정
type: docs
url: /ko/java/advanced-redaction/groupdocs-redaction-java-document-security/
weight: 1
---

# 정확한 구문 삭제를 위한 GroupDocs Redaction Java 설정

현대 기업 환경에서 **setup groupdocs redaction java**는 PDF, Word 파일 및 프레젠테이션 내부의 기밀 정보를 보호하기 위한 필수 첫 단계입니다. 컴플라이언스 담당자이든, 문서 관리 시스템을 구축하는 개발자이든, 데이터 프라이버시 워크플로를 자동화하는 IT 관리자이든, 이 가이드는 라이브러리를 설치하고, 정확한 구문을 삭제하며, 고급 래스터화를 적용하여 공유 준비가 된 변조 방지 문서를 생성하는 방법을 보여줍니다.

## 빠른 답변
- **정확한 구문 삭제는 무엇을 하나요?** 특정 문자열(예: 사회보장 번호)을 사용자 정의 텍스트, 마스크 또는 지정한 이미지로 교체합니다.  
- **왜 래스터화를 사용하나요?** 래스터화는 각 페이지를 이미지로 변환하여 노이즈, 테두리 또는 그레이스케일을 추가해 숨겨진 데이터를 복구할 수 없게 만듭니다.  
- **필요한 Maven 버전은?** GroupDocs.Redaction 24.9 이상.  
- **한 번에 여러 구문을 삭제할 수 있나요?** 예 – 여러 `ExactPhraseRedaction` 객체를 생성하고 저장하기 전에 적용합니다.  
- **프로덕션에 라이선스가 필요합니까?** 테스트용 트라이얼은 작동하지만, 상업적 배포에는 정식 라이선스가 필수입니다.  

## setup groupdocs redaction java이란?
Setup groupdocs redaction java는 GroupDocs.Redaction 라이브러리를 Java 빌드 시스템에 추가하고, 대상 문서를 가리키는 `Redactor` 인스턴스를 생성하며, 삭제 또는 저장 옵션을 구성하는 것을 의미합니다. `Redactor` 클래스는 문서를 로드하고 모든 삭제 작업을 조정하는 GroupDocs.Redaction의 핵심 API입니다. 라이브러리가 클래스패스에 추가되면 몇 줄의 코드만으로 텍스트, 이미지 또는 전체 섹션을 삭제할 수 있습니다.

## Java용 GroupDocs Redaction을 사용하는 이유는?
Java용 GroupDocs.Redaction은 즉시 사용 가능한 PCI‑DSS 호환 삭제 기능을 제공하며, **50개 이상의 파일 형식**을 처리하고 전체 파일을 메모리에 로드하지 않고도 **최대 500페이지**의 PDF를 처리할 수 있습니다. 내장 래스터화, OCR 기반 삭제 및 배치 처리를 제공하여 대기업 수준의 보안을 제공하면서 대용량 문서의 메모리 사용량을 200 MB 이하로 유지합니다.

## 전제 조건
- Java 8 이상 (Java 11 + 권장)  
- Maven 3 또는 호환 IDE (IntelliJ IDEA, Eclipse 등)  
- Java 구문 및 Maven 의존성 관리에 대한 기본 지식  

## Java용 GroupDocs.Redaction 설정

### Maven 설정

다음과 같이 `pom.xml`에 저장소와 의존성을 정확히 추가하십시오:

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

수동 방식을 선호한다면 공식 사이트에서 최신 JAR 파일을 다운로드하십시오: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### 라이선스 획득

GroupDocs는 평가용 무료 트라이얼을 제공합니다. 프로덕션 작업을 위해서는 GroupDocs 포털에서 임시 또는 정식 라이선스를 획득하십시오.

### 기본 초기화 및 설정

`Redactor` 클래스는 모든 삭제 작업의 진입점입니다. 라이브러리가 클래스패스에 추가되면 보호하려는 문서를 가리키는 `Redactor` 인스턴스를 생성하십시오:

```java
import com.groupdocs.redaction.Redactor;

public class Main {
    public static void main(String[] args) {
        Redactor redactor = new Redactor("path/to/document.docx");
        // Your code here...
        redactor.close();
    }
}
```

## 정확한 구문 삭제

이 기능을 사용하면 특정 문자열을 자리 표시자, 마스크 또는 정의한 사용자 지정 텍스트로 교체할 수 있습니다.

### 정확한 구문 삭제 구현 방법
정확한 구문 삭제를 적용하려면 먼저 `Redactor` 인스턴스로 문서를 로드한 다음, 찾을 구문을 지정하는 `ExactPhraseRedaction` 객체를 생성합니다. 구문이 어떻게 교체될지 정의하는 `ReplacementOptions` 객체를 제공하고, 마지막으로 파일을 저장하기 전에 삭제를 적용합니다.  
`ExactPhraseRedaction`은 문서에서 특정 정확한 구문을 식별하고 삭제 대상으로 표시하는 클래스입니다.  
`ReplacementOptions`는 삭제된 구문 대신 표시될 사용자 정의 텍스트, 기호 또는 이미지와 같은 시각적 교체 내용을 정의합니다.

1. **문서를 로드합니다** – 파일 경로와 함께 `Redactor` 생성자를 사용합니다.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
```

2. **삭제를 적용합니다** – `ExactPhraseRedaction` 객체를 생성하고 `ReplacementOptions` 인스턴스를 전달합니다. `ExactPhraseRedaction` 클래스는 정확한 구문을 식별하고 교체 로직에 연결하는 API 구성 요소이며, `ReplacementOptions`는 원래 구문 대신 표시될 텍스트, 기호 또는 이미지를 정의합니다.

```java
try {
    // Replace 'John Doe' with '[personal]'
    redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]"));
} finally {
    redactor.close();
}
```

#### 문제 해결 팁
- 파일 경로를 확인하십시오; 잘못된 경로는 `FileNotFoundException`을 발생시킵니다.  
- Java 문자열은 대소문자를 구분합니다; 대소문자 구분 없이 매칭하려면 `String.equalsIgnoreCase` 로직을 사용하십시오.  

## 보안 문서 저장을 위한 고급 래스터화 옵션

래스터화는 각 페이지를 이미지로 변환하여 그레이스케일, 노이즈 또는 테두리와 같은 시각적 보안 조치를 추가할 수 있게 합니다.

### 고급 래스터화 구현 방법
고급 래스터화를 활성화하려면 `Redactor` 인스턴스의 저장 옵션을 구성하여 래스터화를 켜고 추가 시각 효과를 선택합니다. 페이지마다 테두리, 노이즈, 그레이스케일 변환 또는 기울기를 추가하여 렌더링 후 숨겨진 데이터가 복구 불가능하도록 할 수 있습니다.  

1. **저장 옵션을 구성합니다** – 래스터화를 활성화하고 원하는 고급 옵션을 추가합니다.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
try {
    SaveOptions so = new SaveOptions();
    // Set a suffix for output files
    so.setRedactedFileSuffix("_scan");

    // Enable and configure rasterization
    so.getRasterization().setEnabled(true);
    so.getRasterization().addAdvancedOption(AdvancedRasterizationOptions.Border);
    so.getRasterization().addAdvancedOption(AdvancedRasterizationOptions.Noise);
    so.getRasterization().addAdvancedOption(AdvancedRasterizationOptions.Grayscale);
    so.getRasterization().addAdvancedOption(AdvancedRasterizationOptions.Tilt);

    // Save the document
    redactor.save(so);
} finally {
    redactor.close();
}
```

2. **핵심 구성 옵션**  
   - `setRedactedFileSuffix` – 예: “_scan”과 같은 접미사를 추가하여 처리된 파일을 쉽게 식별할 수 있습니다.  
   - `addAdvancedOption` – `Border`, `Noise`, `Grayscale`, `Tilt`와 같은 시각 효과를 선택합니다.  

#### 문제 해결 팁
- 모든 형식이 모든 래스터화 기능을 지원하는 것은 아니므로 DOCX, PDF, PPTX로 테스트하여 확인하십시오.  
- 보안과 가독성의 균형을 맞추기 위해 다양한 옵션 조합을 실험하십시오.  

## 실용적인 적용 사례

| 산업 | 전형적인 사용 사례 |
|------|-------------------|
| 법률 | 계약을 공유하기 전에 고객 이름을 삭제합니다. |
| 의료 | 의료 기록에서 환자 식별자를 숨깁니다. |
| 재무 | 분기 보고서에서 계좌 번호를 마스킹합니다. |
| 인사 | 내부 감사용으로 직원 세부 정보를 익명화합니다. |
| 출판 | 원고에서 금지된 구문을 제거합니다. |

## 성능 고려 사항

- **메모리 관리:** 대용량 PDF는 많은 힙 공간을 차지할 수 있으므로 JVM `-Xmx` 플래그를 늘리거나 문서를 청크로 처리하십시오.  
- **I/O 효율성:** 파일을 읽고 쓸 때 버퍼드 스트림을 사용하여 지연을 줄이십시오.  
- **선택적 삭제:** 민감한 데이터가 포함된 페이지에만 삭제를 적용하여 처리 속도를 높이십시오.  

## 결론

**setup groupdocs redaction java**를 마스터함으로써 이제 정확한 구문 삭제와 고급 래스터화를 위한 강력한 툴킷을 보유하게 되었습니다. 이러한 기능을 통해 문서 사용성을 유지하면서 기밀 정보를 보호할 수 있습니다. 다음 단계로 이미지, 바코드, 정규식 등 다른 삭제 유형을 탐색하거나 라이브러리를 더 큰 문서 관리 워크플로에 통합하십시오.

## 자주 묻는 질문

**Q: 정확한 구문 삭제에서 교체 텍스트를 어떻게 사용자 정의하나요?**  
A: 원하는 문자열을 `ReplacementOptions`에 전달하면 일치하는 구문을 그대로 교체합니다.

**Q: 비 DOCX 파일에도 고급 래스터화를 사용할 수 있나요?**  
A: 예, GroupDocs.Redaction은 PDF, PPTX 및 기타 여러 형식을 지원합니다—선택한 형식에 해당 래스터 옵션이 있는지 확인하십시오.

**Q: 코드에서 파일 경로 오류가 발생하면 어떻게 해야 하나요?**  
A: 경로가 절대 경로나 프로젝트 작업 디렉터리에 대해 올바르게 상대적인지 다시 확인하고, 파일에 읽기/쓰기 권한이 있는지 확인하십시오.

**Q: 한 번에 여러 구문을 삭제할 방법이 있나요?**  
A: 물론입니다. 여러 `ExactPhraseRedaction` 인스턴스를 생성하고 저장하기 전에 순차적으로 적용하십시오.

**Q: GroupDocs.Redaction으로 대용량 문서를 효율적으로 처리하려면 어떻게 해야 하나요?**  
A: 문서를 섹션별로 처리하거나 라이브러리에서 제공하는 스트리밍 API를 사용하여 메모리 사용량을 낮게 유지하십시오.

---

**마지막 업데이트:** 2026-10-22  
**테스트 환경:** GroupDocs.Redaction 24.9 for Java  
**작성자:** GroupDocs  

**리소스**  
- **문서:** [GroupDocs.Redaction Java Documentation](https://docs.groupdocs.com/redaction/java/)  
- **API 레퍼런스:** [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java)  
- **다운로드:** [Latest Release](https://releases.groupdocs.com/redaction/java/)

## 관련 튜토리얼

- [Java Redaction Guide Groupdocs Document Security](/redaction/java/text-redaction/java-redaction-guide-groupdocs-document-security/)
- [Groupdocs Redaction Java Word 문서 래스터화](/redaction/java/document-saving/groupdocs-redaction-java-rasterize-word-docs/)
- [고급 로깅 Groupdocs Redaction Java](/redaction/java/advanced-redaction/advanced-logging-groupdocs-redaction-java/)