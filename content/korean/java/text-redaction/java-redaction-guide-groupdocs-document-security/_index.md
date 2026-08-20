---
date: '2026-08-20'
description: GroupDocs.Redaction을 사용하여 Java 문서에서 텍스트를 삭제하는 방법을 배우세요. exact‑phrase,
  regex, color replacement, annotation 및 metadata redaction을 포함하여 보안 준수를 위한 기능을 다룹니다.
keywords:
- how to redact text
- replace text with color
- GroupDocs.Redaction Java
- Java document security
- document redaction library
lastmod: '2026-08-20'
og_description: GroupDocs.Redaction을 사용하여 Java 문서에서 텍스트를 삭제하는 방법을 배우세요. exact‑phrase,
  regex, color replacement, annotation 및 metadata redaction을 포함합니다.
og_image_alt: Guide showing Java code redacting text with GroupDocs.Redaction
og_title: GroupDocs.Redaction을 사용하여 Java 문서에서 텍스트를 삭제하는 방법
schemas:
- author: GroupDocs
  dateModified: '2026-08-20'
  description: Learn how to redact text in Java documents using GroupDocs.Redaction,
    covering exact‑phrase, regex, color replacement, annotation and metadata redaction
    for secure compliance.
  headline: How to redact text in Java documents with GroupDocs.Redaction
  type: TechArticle
- description: Learn how to redact text in Java documents using GroupDocs.Redaction,
    covering exact‑phrase, regex, color replacement, annotation and metadata redaction
    for secure compliance.
  name: How to redact text in Java documents with GroupDocs.Redaction
  steps:
  - name: '**Add the Maven dependency** (or include the JAR).'
    text: '**Add the Maven dependency** (or include the JAR).'
  - name: '**Configure your license** by calling `License.setLicense("path/to/license.lic")`
      early in your application.'
    text: '**Configure your license** by calling `License.setLicense("path/to/license.lic")`
      early in your application.'
  - name: '**Create a `Redactor` instance** pointing at the source document.'
    text: '**Create a `Redactor` instance** pointing at the source document.'
  - name: '**Initialize the Redactor** with the document you want to process:'
    text: '**Initialize the Redactor** with the document you want to process:'
  - name: '**Define the exact‑phrase rule** and apply it:'
    text: '**Define the exact‑phrase rule** and apply it:'
  - name: '**Save the redacted file** to your output folder:'
    text: '**Save the redacted file** to your output folder:'
  - name: 'Load the document:'
    text: 'Load the document:'
  - name: 'Create a regex rule and apply it:'
    text: 'Create a regex rule and apply it:'
  - name: 'Save the result:'
    text: 'Save the result:'
  - name: 'Load the document:'
    text: 'Load the document:'
  type: HowTo
- questions:
  - answer: Yes. Create each redaction object, call `redactor.apply()` for each, then
      save once.
    question: Can I combine multiple redaction rules in a single pass?
  - answer: Absolutely. Pass the password to the `Redactor` constructor that accepts
      a `LoadOptions` object.
    question: Does GroupDocs.Redaction support password‑protected files?
  - answer: You can call `redactor.preview()` to generate a temporary view that highlights
      the areas to be redacted.
    question: Is it possible to preview redactions before saving?
  - answer: DOCX, PDF, PPTX, XLSX, PNG, JPEG, BMP, and many more—over 30 formats in
      total.
    question: What file formats are supported?
  - answer: Use the metadata erasure feature, remove annotations, and apply exact‑phrase
      or regex redactions to all personal data fields.
    question: How do I ensure the redacted document complies with GDPR?
  type: FAQPage
tags:
- text redaction
- GroupDocs.Redaction
- Java document security
- regex redaction
- metadata removal
title: GroupDocs.Redaction을 사용하여 Java 문서에서 텍스트를 삭제하는 방법
type: docs
url: /ko/java/text-redaction/java-redaction-guide-groupdocs-document-security/
weight: 1
---

# GroupDocs.Redaction을 사용한 Java 문서에서 텍스트 가리기

현대 애플리케이션에서는 PDF, Word 파일 또는 이미지 내부의 **텍스트 가리기**가 규정 준수와 개인 정보 보호를 위해 자주 요구됩니다. 개인 식별자를 숨기거나, 기밀 주석을 제거하거나, 메타데이터를 삭제해야 할 때, GroupDocs.Redaction for Java는 **java document security**를 달성할 수 있는 깔끔하고 프로그래밍 방식의 방법을 제공합니다. 이 튜토리얼은 라이브러리 설정부터 정확 구문, 정규식, 색상 기반, 주석 및 메타데이터 가리기 적용까지 모든 필수 단계를 안내하므로 백엔드 서비스에 가리기 기능을 직접 삽입할 수 있습니다.

## 빠른 답변
- **Java 문서 가리기를 처리하는 라이브러리는 무엇입니까?** GroupDocs.Redaction for Java.  
- **텍스트를 삭제하는 대신 색상으로 교체할 수 있나요?** 예, “replace text with color” 기능을 사용하십시오.  
- **프로덕션 사용에 라이선스가 필요합니까?** 전체 기능을 사용하려면 임시 또는 유료 라이선스가 필요합니다.  
- **지원되는 Java 버전은 무엇입니까?** JDK 8 or higher.  
- **라이브러리를 추가하는 유일한 방법이 Maven입니까?** Maven이 권장되지만 JAR를 수동으로 다운로드할 수도 있습니다.

## Java에서 “텍스트 가리기”란 무엇인가요?
**Redaction은 민감한 콘텐츠를 영구적으로 제거하거나 가려서 복구할 수 없도록 합니다.** Java에서는 파일을 로드하고, 숨길 내용을 정의한 뒤, 가리기를 적용하고, 정제된 버전을 저장합니다. 이를 통해 하위 소비자는 정리된 문서만 보게 됩니다.

## Java용 GroupDocs.Redaction을 사용하는 이유
파일을 로드하고 규칙을 정의하면 SDK가 무거운 작업을 처리합니다. GroupDocs.Redaction은 **30+ formats**—DOCX, PDF, PPTX, XLSX, PNG, JPEG, BMP 등을 포함—를 지원하며 스트림 기반 아키텍처를 통해 대용량 문서를 처리합니다. 정확 구문, 정규식, 색상 기반, 주석 및 메타데이터 가리기를 제공하여 GDPR, HIPAA 등 규정을 충족할 수 있는 세밀한 제어를 제공합니다.

## 사전 요구 사항
- **Java Development Kit (JDK) 8+** 가 머신에 설치되어 있어야 합니다.  
- **Maven** 은 의존성 관리를 위해 필요합니다 (또는 JAR를 수동으로 다운로드할 수 있습니다).  

### 필요한 라이브러리 및 종속성
`pom.xml`에 GroupDocs 저장소와 Redaction 종속성을 추가합니다:

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

또한 공식 릴리스 페이지에서 최신 JAR를 다운로드할 수 있습니다: [GroupDocs.Redaction for Java 릴리스](https://releases.groupdocs.com/redaction/java/).

### 라이선스 획득
프로덕션 사용을 위해 임시 또는 전체 라이선스를 획득하십시오. 평가용 무료 체험판을 사용할 수 있습니다.

## Java용 GroupDocs.Redaction 설정
1. **Maven 종속성을 추가** (또는 JAR를 포함).  
2. **라이선스를 구성** 하려면 애플리케이션 초기에 `License.setLicense("path/to/license.lic")` 를 호출합니다.  
   `License`는 GroupDocs Redaction 라이선스 파일을 로드하고 적용하는 데 사용되는 클래스입니다.  
3. **소스 문서를 가리키는 `Redactor` 인스턴스를 생성** 합니다.

**`Redactor` 클래스는 메모리 효율적인 방식으로 문서를 로드, 수정 및 저장하는 핵심 엔진입니다.** `Redactor` 객체를 만든 후에는 결과를 저장하기 전에 여러 가리기 규칙을 체인처럼 연결할 수 있습니다.

이제 가리기를 시작할 준비가 되었습니다.

## 구현 가이드

### 정확 구문 가리기
특정 구문(예: 사람 이름)을 자리 표시자 텍스트로 교체합니다.

#### 정확 구문 가리기는 어떻게 작동합니까?
`ExactPhraseRedaction`은 특정 정확한 텍스트 문자열을 제거하거나 교체하는 규칙을 나타냅니다. 문서를 로드하고, 정확한 문자열을 목표로 하는 `ExactPhraseRedaction` 규칙을 생성한 뒤, 규칙을 적용하고 출력을 저장합니다. SDK는 레이아웃을 유지하면서 일치하는 텍스트를 자동으로 공백 처리합니다.

1. **프로세스할 문서로 Redactor 초기화**:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. **정확 구문 규칙 정의** 및 적용:

```java
ExactPhraseRedaction redaction = new ExactPhraseRedaction(
    "John Doe", 
    new ReplacementOptions("[Client]"));

redactor.apply(redaction);
```

3. **출력 폴더에 가리기 파일 저장**:

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Redaction applied successfully.");
}
```

### 텍스트 교체가 포함된 정규식 가리기
정규식을 사용해 일련 번호와 같은 패턴을 찾아 일반 토큰으로 교체합니다.

#### 교체가 포함된 정규식 가리기는 어떻게 작동합니까?
`RegexRedaction`은 정규식을 기반으로 일치하는 텍스트를 찾아 수정하는 규칙을 정의합니다. 패턴과 교체 문자열을 포함하는 `RegexRedaction` 객체를 제공하면 엔진이 문서를 스캔하여 모든 일치를 교체하고 주변 서식을 유지합니다.

1. 문서 로드:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. 정규식 규칙 생성 및 적용:

```java
RegexRedaction redaction = new RegexRedaction(
    "Redaction",
    new ReplacementOptions("[Product]"));

redactor.apply(redaction);
```

3. 결과 저장:

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Redaction applied successfully.");
}
```

### 색상 교체가 포함된 정규식 가리기
텍스트를 삭제하는 대신 **replace text with color** 기능을 사용해 시각적으로 가릴 수 있으며, 기본 문자는 그대로 유지됩니다.

#### 색상 기반 가리기가 삭제와 다른 점은 무엇입니까?
SDK는 일치하는 텍스트에 선택한 색상을 칠해 인간의 눈으로는 읽을 수 없게 만들지만 파일 스트림에는 여전히 존재합니다. 이는 하위 처리에서 문서 구조를 유지해야 할 때 유용합니다.

1. 문서 로드:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. 정규식 패턴 정의 및 교체 색상 설정(예: 파란색):

```java
RegexRedaction redaction = new RegexRedaction(
    "\d{2}\s*\d{2}[^\\d]*\d{6}", 
    new ReplacementOptions(Color.BLUE));

redactor.apply(redaction);
```

3. 업데이트된 파일 저장:

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Redaction applied successfully.");
}
```

### 주석 삭제 가리기
문서에서 모든 주석(댓글, 강조 표시 등)을 제거해 보다 깔끔한 최종 버전을 만듭니다.

#### 한 번에 주석을 제거하는 방법은?
`AnnotationRedaction`은 댓글, 강조 표시, 스탬프와 같은 주석을 제거하는 규칙입니다. 모든 주석 유형을 목표로 하는 `AnnotationRedaction` 규칙을 생성하고 적용한 뒤 변경 사항을 영구화합니다.

1. 파일 로드:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. 주석 삭제 규칙 적용:

```java
DeleteAnnotationRedaction redaction = new DeleteAnnotationRedaction();

redactor.apply(redaction);
```

3. 변경 사항 영구화:

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Annotations deleted successfully.");
}
```

### 메타데이터 삭제 가리기
작성자, 생성 날짜, 사용자 정의 속성 등 모든 메타데이터를 제거해 프라이버시를 보호하고 규정 준수를 충족합니다.

#### 메타데이터 삭제가 프라이버시를 보장하는 방법은?
`MetadataRedaction`은 문서에서 내장 및 사용자 정의 메타데이터 필드를 모두 삭제합니다. `MetadataRedaction` 규칙은 내장 및 사용자 정의 메타데이터 필드를 지워 파일 속성에 숨겨진 식별자가 남지 않도록 합니다.

1. 문서 열기:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. 메타데이터 삭제 규칙 적용:

```java
EraseMetadataRedaction redaction = new EraseMetadataRedaction(MetadataFilters.All);

redactor.apply(redaction);
```

3. 정제된 문서 저장:

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Metadata erased successfully.");
}
```

## 실용적인 적용 사례 (왜 중요한가)
- **법률 문서 준비** – 상대 변호사와 초안을 공유하기 전에 클라이언트 이름을 가립니다.  
- **헬스케어 규정 준수** – 환자 식별자를 제거하여 HIPAA 규정을 수동 편집 없이 준수합니다.  
- **기업 데이터 보호** – 내부 보고서 배포 전에 재무 수치나 영업 비밀을 숨깁니다.  

이러한 단계를 자동화하면 수작업 노력을 줄이고 인간 오류를 없애며 수천 개 파일에 걸쳐 일관된 규정 준수를 보장합니다.

## 성능 고려 사항
- **로드 대신 스트림 사용** – 대용량 파일의 경우 전체 문서를 메모리에 로드하지 않도록 `InputStream`을 받는 `Redactor` 생성자를 사용합니다.  
- **정규식 패턴 사전 컴파일** 동일한 가리기를 반복 실행할 때 CPU 부하를 최대 30 %까지 줄일 수 있습니다.  
- **JVM 힙 모니터링** – 가리기는 메모리를 많이 사용하므로 다중 기가바이트 아카이브 배치 처리 시 힙 크기(`-Xmx2g`)를 늘리는 것을 고려하십시오.  

## 일반적인 문제 및 해결 방법
| 증상 | 가능한 원인 | 해결 방법 |
|---------|--------------|-----|
| apply 후 변경 사항 없음 | 잘못된 파일 경로 또는 파일이 잠겨 있음 | 파일 경로를 확인하고 문서가 다른 곳에서 열려 있지 않은지 확인하십시오 |
| 정규식이 일치하지 않음 | 패턴 구문 오류 | 온라인 테스트 도구로 정규식을 테스트하고 백슬래시를 올바르게 이스케이프하십시오 |
| 색상 교체가 보이지 않음 | 출력 형식이 텍스트 색상을 지원하지 않음(예: 일반 텍스트) | 스타일을 유지하는 DOCX 또는 PDF와 같은 형식을 사용하십시오 |
| 런타임 라이선스 오류 | 라이선스 파일이 없거나 유효하지 않음 | `.lic` 파일을 접근 가능한 디렉터리에 두고 Redactor 사용 전에 `License.setLicense` 를 호출하십시오 |

## 자주 묻는 질문

**Q: 한 번에 여러 가리기 규칙을 결합할 수 있나요?**  
A: 예. 각 가리기 객체를 만든 뒤 각각 `redactor.apply()` 를 호출하고 한 번에 저장합니다.

**Q: GroupDocs.Redaction이 비밀번호로 보호된 파일을 지원합니까?**  
A: 물론 지원합니다. `LoadOptions` 객체를 받는 `Redactor` 생성자에 비밀번호를 전달하면 됩니다.

**Q: 저장하기 전에 가리기 결과를 미리 볼 수 있나요?**  
A: `redactor.preview()` 를 호출하면 가리기 영역을 강조 표시한 임시 뷰를 생성할 수 있습니다.

**Q: 지원되는 파일 형식은 무엇입니까?**  
A: DOCX, PDF, PPTX, XLSX, PNG, JPEG, BMP 등 30가지가 넘는 형식을 지원합니다.

**Q: 가리기 문서가 GDPR을 준수하도록 하려면 어떻게 해야 하나요?**  
A: 메타데이터 삭제 기능을 사용하고, 주석을 제거하며, 모든 개인 데이터 필드에 정확 구문 또는 정규식 가리기를 적용하십시오.

## 결론
이제 GroupDocs.Redaction을 사용해 Java 문서에서 **텍스트 가리기 방법**에 대한 완전한 엔드‑투‑엔드 가이드를 보유하게 되었습니다. 정확 구문, 정규식, 색상 기반, 주석 및 메타데이터 가리기 단계를 따라 하면 **java document security**를 견고하게 구현하면서 코드를 깔끔하고 유지 보수하기 쉬운 상태로 유지할 수 있습니다. 이러한 스니펫을 기존 서비스에 통합하고 배치 처리를 자동화하여 개인정보 보호 규정을 준수하십시오.

---

**마지막 업데이트:** 2026-08-20  
**테스트 환경:** GroupDocs.Redaction 24.9 for Java  
**작성자:** GroupDocs

## 관련 튜토리얼

- [metadata 텍스트 교체 java – GroupDocs와 함께하는 보안 가리기](/redaction/java/metadata-redaction/java-redaction-metadata-text-replacement-guide/)
- [Java용 GroupDocs.Redaction을 사용하여 워드 문서의 이미지 가리기 – 종합 가이드](/redaction/java/image-redaction/redact-images-word-docs-groupdocs-redaction-java/)
- [파일 경로에서 GroupDocs Redaction Java 라이선스로 문서 가리기 – 단계별 가이드](/redaction/java/licensing-configuration/implement-groupdocs-redaction-java-license-file-path/)