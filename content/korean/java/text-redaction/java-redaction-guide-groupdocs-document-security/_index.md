---
date: '2026-03-04'
description: GroupDocs.Redaction for Java를 사용하여 텍스트를 가리고, 텍스트를 색상으로 교체하며, Java 문서
  보안을 보장하는 방법을 배웁니다. 코드 예제가 포함된 단계별 가이드.
keywords:
- Java Document Redaction
- GroupDocs.Redaction for Java
- text redaction in Java
title: GroupDocs.Redaction을 사용하여 Java 문서에서 텍스트를 가리는 방법
type: docs
url: /ko/java/text-redaction/java-redaction-guide-groupdocs-document-security/
weight: 1
---

# GroupDocs.Redaction을 사용한 Java 문서에서 텍스트 가리기 방법

현대 애플리케이션에서는 PDF, Word 파일 또는 이미지 내부의 **텍스트 가리기**가 규정 준수와 개인 정보 보호를 위해 자주 요구됩니다. 개인 식별자를 숨기거나, 기밀 주석을 제거하거나, 메타데이터를 삭제해야 할 경우, GroupDocs.Redaction for Java은 **java document security**를 구현할 수 있는 깔끔하고 프로그래밍 가능한 방법을 제공합니다. 이 튜토리얼에서는 라이브러리 설정부터 정확한 구문, 정규식, 색상 기반, 주석 및 메타데이터 가리기 적용까지 모든 필수 단계를 안내합니다.

## 빠른 답변
- **Java 문서 가리기를 처리하는 라이브러리는?** GroupDocs.Redaction for Java.  
- **텍스트를 삭제하지 않고 색상으로 교체할 수 있나요?** 예, “replace text with color” 기능을 사용하면 됩니다.  
- **프로덕션 사용에 라이선스가 필요합니까?** 전체 기능을 사용하려면 임시 또는 유료 라이선스가 필요합니다.  
- **지원되는 Java 버전은?** JDK 8 이상.  
- **라이브러리를 추가하는 방법은 Maven만 있나요?** Maven이 권장되지만 JAR를 직접 다운로드하여 사용할 수도 있습니다.

## Java에서 “텍스트 가리기”란?
가리기는 문서에서 민감한 내용을 영구적으로 제거하거나 가려서 복구할 수 없도록 하는 과정입니다. Java에서는 일반적으로 파일을 로드하고, 숨길 대상을 정의한 뒤, 가리기를 적용하고, 정제된 버전을 저장하는 흐름을 따릅니다.

## 왜 GroupDocs.Redaction for Java를 사용해야 할까요?
- **포괄적인 포맷 지원** – DOCX, PDF, PPTX, 이미지 등 다양한 형식을 처리합니다.  
- **세밀한 제어** – 정확한 구문, 정규식, 색상, 주석 또는 메타데이터별로 가릴 수 있습니다.  
- **성능 최적화** – 스트림 기반 처리로 대용량 파일의 메모리 사용량을 최소화합니다.  
- **내장된 규정 준수** – GDPR, HIPAA 등 개인정보 보호 규정을 충족하도록 돕습니다.

## 사전 요구 사항
- **Java Development Kit (JDK) 8+** 가 설치되어 있어야 합니다.  
- **Maven** 으로 의존성을 관리하거나, JAR를 직접 다운로드할 수 있습니다.  

### 필수 라이브러리 및 의존성
`pom.xml`에 GroupDocs 저장소와 Redaction 의존성을 추가합니다:

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

또는 공식 릴리스 페이지에서 최신 JAR를 다운로드할 수 있습니다: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### 라이선스 획득
프로덕션 사용을 위해서는 임시 또는 정식 라이선스를 받아야 합니다. 평가용 무료 체험판도 제공됩니다.

## GroupDocs.Redaction for Java 설정하기
1. **Maven 의존성을 추가**(또는 JAR를 포함)합니다.  
2. **라이선스를 설정**하려면 애플리케이션 초기에 `License.setLicense("path/to/license.lic")` 를 호출합니다.  
3. **Redactor 인스턴스**를 생성하여 소스 문서를 지정합니다.

이제 가리기 작업을 시작할 준비가 되었습니다.

## 구현 가이드

### 정확한 구문 가리기
특정 구문(예: 사람 이름)을 자리표시자 텍스트로 교체합니다.

#### 단계별
1. **Redactor 초기화** – 처리할 문서를 지정합니다:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. **정확한 구문 규칙**을 정의하고 적용합니다:

```java
ExactPhraseRedaction redaction = new ExactPhraseRedaction(
    "John Doe", 
    new ReplacementOptions("[Client]"));

redactor.apply(redaction);
```

3. **가린 파일을 저장** – 출력 폴더에 저장합니다:

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Redaction applied successfully.");
}
```

### 텍스트 교체가 포함된 정규식 가리기
정규식을 사용해 일련 번호와 같은 패턴을 찾아 일반 토큰으로 교체합니다.

#### 단계별
1. 문서를 로드합니다:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. 정규식 규칙을 만들고 적용합니다:

```java
RegexRedaction redaction = new RegexRedaction(
    "Redaction",
    new ReplacementOptions("[Product]"));

redactor.apply(redaction);
```

3. 결과를 저장합니다:

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Redaction applied successfully.");
}
```

### 색상 교체가 포함된 정규식 가리기
텍스트를 삭제하는 대신 **텍스트를 색상으로 교체**하여 시각적으로 가리면서도 원본 문자는 유지할 수 있습니다.

#### 단계별
1. 문서를 로드합니다:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. 정규식 패턴을 정의하고 교체 색상(예: 파란색)을 설정합니다:

```java
RegexRedaction redaction = new RegexRedaction(
    "\d{2}\s*\d{2}[^\\d]*\d{6}", 
    new ReplacementOptions(Color.BLUE));

redactor.apply(redaction);
```

3. 업데이트된 파일을 저장합니다:

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Redaction applied successfully.");
}
```

### 주석 삭제 가리기
문서에서 모든 주석(코멘트, 하이라이트 등)을 제거하여 깔끔한 최종 버전을 만듭니다.

#### 단계별
1. 파일을 로드합니다:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. 주석 삭제 규칙을 적용합니다:

```java
DeleteAnnotationRedaction redaction = new DeleteAnnotationRedaction();

redactor.apply(redaction);
```

3. 변경 사항을 영구 저장합니다:

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Annotations deleted successfully.");
}
```

### 메타데이터 삭제 가리기
프라이버시 보호와 규정 준수를 위해 저자, 생성 날짜, 사용자 정의 속성 등 모든 메타데이터를 제거합니다.

#### 단계별
1. 문서를 엽니다:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. 메타데이터 삭제 규칙을 적용합니다:

```java
EraseMetadataRedaction redaction = new EraseMetadataRedaction(MetadataFilters.All);

redactor.apply(redaction);
```

3. 정제된 문서를 저장합니다:

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Metadata erased successfully.");
}
```

## 실용적인 적용 사례 (왜 중요한가)
- **법률 문서 준비** – 초안 공유 전 클라이언트 이름을 가립니다.  
- **헬스케어 규정 준수** – 환자 식별자를 삭제해 HIPAA를 만족합니다.  
- **기업 데이터 보호** – 내부 보고서에서 재무 수치나 영업 비밀을 숨깁니다.  

이러한 가리기 단계를 기존 워크플로에 통합하면 개인정보 보호 자동화와 데이터 유출 위험 감소에 크게 기여합니다.

## 성능 고려 사항
- **스트림 사용** – 대용량 파일은 `Redactor` 생성자에 `InputStream`을 전달해 전체 문서를 메모리에 로드하지 않도록 합니다.  
- **정규식 사전 컴파일** – 동일한 가리기를 반복 실행할 경우 CPU 부하를 줄일 수 있습니다.  
- **JVM 힙 모니터링** – 가리기 작업은 메모리를 많이 사용하므로 배치 처리 시 힙 크기 확대를 고려하십시오.

## 일반적인 문제 및 해결 방법
| 증상 | 가능 원인 | 해결 방법 |
|------|-----------|-----------|
| `apply` 후 변화가 없음 | 잘못된 파일 경로나 파일이 잠김 | 파일 경로를 확인하고 문서가 다른 프로그램에서 열려 있지 않은지 확인 |
| 정규식이 매치되지 않음 | 패턴 구문 오류 | 온라인 정규식 테스트 도구로 패턴을 검증하고 역슬래시를 올바르게 이스케이프 |
| 색상 교체가 보이지 않음 | 출력 포맷이 텍스트 색상을 지원하지 않음 (예: plain text) | 스타일을 유지하는 DOCX 또는 PDF 형식으로 저장 |
| 런타임에 라이선스 오류 | 라이선스 파일이 없거나 잘못됨 | `.lic` 파일을 접근 가능한 디렉터리에 배치하고 `License.setLicense` 를 Redactor 사용 전에 호출 |

## 자주 묻는 질문

**Q: 한 번에 여러 가리기 규칙을 적용할 수 있나요?**  
A: 예. 각 가리기 객체를 생성하고 각각 `redactor.apply()` 를 호출한 뒤 한 번에 저장하면 됩니다.

**Q: 비밀번호가 설정된 파일을 지원하나요?**  
A: 물론입니다. `LoadOptions` 객체를 받는 `Redactor` 생성자에 비밀번호를 전달하면 됩니다.

**Q: 저장하기 전에 가리기 결과를 미리 볼 수 있나요?**  
A: `redactor.preview()` 를 호출하면 가리기 영역을 강조한 임시 뷰를 생성할 수 있습니다.

**Q: 지원되는 파일 형식은 무엇인가요?**  
A: DOCX, PDF, PPTX, XLSX, 이미지(PNG, JPEG, BMP) 등 다수의 포맷을 지원합니다.

**Q: 가리기 문서가 GDPR을 준수하도록 하려면?**  
A: 메타데이터 삭제 기능을 사용하고, 주석을 제거하며, 개인 데이터 필드에 정확한 구문 또는 정규식 가리기를 적용하면 됩니다.

## 결론
이제 GroupDocs.Redaction을 활용해 **Java 문서에서 텍스트를 가리는** 전체 과정을 숙지했습니다. 정확한 구문, 정규식, 색상 기반, 주석 및 메타데이터 가리기 단계를 따라 하면 **java document security**를 강력히 구현하면서도 코드 유지 보수성을 높일 수 있습니다. 이 스니펫들을 기존 서비스에 통합하고 배치 처리 자동화를 구현해 개인정보 보호 규정을 지속적으로 만족하십시오.

---

**마지막 업데이트:** 2026-03-04  
**테스트 환경:** GroupDocs.Redaction 24.9 for Java  
**작성자:** GroupDocs