---
date: '2026-10-01'
description: Java에서 GroupDocs Redaction을 사용하여 작성자 메타데이터를 제거하고 편집된 문서 파일을 저장하는 방법을
  배웁니다.
keywords:
- remove author metadata
- save redacted document
- groupdocs metadata removal
lastmod: '2026-10-01'
og_description: Java에서 GroupDocs Redaction을 사용하여 작성자 메타데이터를 제거하고 편집된 문서 파일을 저장하는 방법을
  배웁니다. 단계별 가이드를 따라 보세요.
og_image_alt: Guide showing Java code to remove author metadata using GroupDocs Redaction
og_title: Java에서 GroupDocs를 사용하여 작성자 메타데이터 제거하는 방법
schemas:
- author: GroupDocs
  dateModified: '2026-10-01'
  description: Learn how to remove author metadata and save redacted document files
    in Java using GroupDocs Redaction.
  headline: How to remove author metadata in Java with GroupDocs
  type: TechArticle
- description: Learn how to remove author metadata and save redacted document files
    in Java using GroupDocs Redaction.
  name: How to remove author metadata in Java with GroupDocs
  steps:
  - name: '**Legal documents** – Redact author information before sending contracts
      to opposing counsel.'
    text: '**Legal documents** – Redact author information before sending contracts
      to opposing counsel.'
  - name: '**Corporate reports** – Remove manager names when publishing quarterly
      results to shareholders.'
    text: '**Corporate reports** – Remove manager names when publishing quarterly
      results to shareholders.'
  - name: '**Project files** – Clean up internal project documentation before archiving
      or uploading to a public repository.'
    text: '**Project files** – Clean up internal project documentation before archiving
      or uploading to a public repository.'
  type: HowTo
- questions:
  - answer: It removes selected metadata fields from a document.
    question: What does EraseMetadataRedaction do?
  - answer: GroupDocs.Redaction for Java.
    question: Which library provides this feature?
  - answer: A free trial works for testing; a permanent license is required for production.
    question: Do I need a license?
  - answer: Yes, combine filters with a logical OR.
    question: Can I target multiple fields at once?
  - answer: Redactor instances are not shared across threads; create a new instance
      per operation.
    question: Is the process thread‑safe?
  type: FAQPage
tags:
- metadata redaction
- GroupDocs
- Java document processing
title: Java에서 GroupDocs를 사용하여 작성자 메타데이터 제거하는 방법
type: docs
url: /ko/java/metadata-redaction/groupdocs-redaction-java-metadata-implementation/
weight: 1
---

# Java에서 GroupDocs를 사용하여 작성자 메타데이터 제거하기

오늘날 디지털 환경에서는 문서에 숨겨진 민감한 정보를 보호하는 것이 필수적인 실천입니다. **작성자 메타데이터 제거**는 개인 또는 기업 식별자의 우발적인 노출을 방지합니다. 이 튜토리얼에서는 GroupDocs.Redaction for Java의 `EraseMetadataRedaction`을 사용하여 Word 파일에서 *Author* 및 *Manager*와 같은 필드를 삭제하고, **redacted document** 사본을 안전하게 저장하여 공유하거나 보관하는 방법을 단계별로 보여줍니다.

## 빠른 답변
- **EraseMetadataRedaction은 무엇을 하나요?** 문서에서 선택된 메타데이터 필드를 제거합니다.  
- **이 기능을 제공하는 라이브러리는?** GroupDocs.Redaction for Java.  
- **라이선스가 필요합니까?** 무료 체험으로 테스트가 가능하며, 프로덕션에서는 영구 라이선스가 필요합니다.  
- **한 번에 여러 필드를 대상으로 할 수 있나요?** 예, 논리 OR을 사용해 필터를 결합하면 됩니다.  
- **프로세스가 스레드 안전한가요?** Redactor 인스턴스는 스레드 간에 공유되지 않으며, 작업당 새 인스턴스를 생성해야 합니다.

## EraseMetadataRedaction이란?
`EraseMetadataRedaction`은 어떤 메타데이터 항목을 삭제할지 지정할 수 있는 내장 레드랙션 클래스입니다. GroupDocs.Redaction이 지원하는 다양한 문서 형식에서 작동하여 숨겨진 작성자 정보가 유출되지 않도록 보장합니다. Author, Manager와 같은 표준 속성뿐만 아니라 사용자 정의 메타데이터 필드도 대상으로 지정할 수 있어 포괄적인 개인정보 보호를 제공합니다.

## GroupDocs와 함께 EraseMetadataRedaction을 사용하는 이유
GroupDocs.Redaction은 **100개 이상의 입력 및 출력 형식**을 지원하며, 전체 파일을 메모리에 로드하지 않고도 최대 500페이지 문서를 처리할 수 있습니다. 이 클래스를 사용하면 GDPR, HIPAA 또는 내부 규정 요구사항을 충족하면서도 코드베이스를 간단하게 유지할 수 있는 단일 고성능 API를 제공받습니다.

## 사전 요구 사항
- Java 8 이상 설치.  
- Maven(또는 JAR를 수동으로 추가할 수 있는 환경).  
- GroupDocs.Redaction for Java (버전 24.9 이상).  
- 유효한 GroupDocs 체험 또는 영구 라이선스.

## GroupDocs.Redaction for Java 설정

### Maven 설치
**pom.xml**에 GroupDocs 저장소와 의존성을 추가합니다:

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
또는 최신 JAR를 [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/)에서 다운로드합니다.

### 라이선스 획득
GroupDocs 포털에서 무료 체험을 받거나 임시 라이선스를 구매합니다. 라이선스 파일은 애플리케이션이 로드할 수 있는 위치(예: 클래스패스 루트)에 배치해야 합니다.

### 기본 초기화 및 설정
다음은 DOCX 파일에 대한 `Redactor` 인스턴스를 생성하는 최소 예제입니다:

```java
import com.groupdocs.redaction.Redactor;

String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
Redactor redactor = new Redactor(filePath);
```

## Java에서 EraseMetadataRedaction 사용 방법
다음 섹션에서는 구현을 명확하고 실행 가능한 단계로 나눕니다.

### 기능: 특정 메타데이터 항목 정리

#### 개요
`EraseMetadataRedaction`을 사용하여 **Author**와 **Manager** 메타데이터 필드를 삭제합니다. 이는 내부 보고서를 외부 파트너와 공유할 때 흔히 요구되는 작업입니다.

#### 단계별 구현

##### 1️⃣ Redactor 객체 초기화
`Redactor`는 문서를 로드하고 레드랙션 객체를 적용한 뒤 결과를 기록하는 핵심 클래스입니다. 처리하는 각 파일마다 새 인스턴스를 생성합니다:

```java
import com.groupdocs.redaction.Redactor;

String inputFilePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
final Redactor redactor = new Redactor(inputFilePath);
```

##### 2️⃣ EraseMetadataRedaction 적용
`MetadataFilters`는 Author와 Manager와 같은 일반 메타데이터 키에 대한 사전 정의된 필터를 제공합니다.  
`EraseMetadataRedaction`은 제공된 `MetadataFilters`와 일치하는 메타데이터 항목을 제거합니다. 비트 OR(`|`) 연산자를 사용해 `Author`와 `Manager` 필터를 결합하면 한 번의 호출로 두 필드를 모두 삭제할 수 있습니다:

```java
import com.groupdocs.redaction.redactions.EraseMetadataRedaction;
import com.groupdocs.redaction.MetadataFilters;

try {
    redactor.apply(new EraseMetadataRedaction(MetadataFilters.Author | MetadataFilters.Manager));
} finally {
    redactor.close();
}
```

##### 3️⃣ 저장 옵션 구성
`SaveOptions`를 사용하면 출력 파일 이름, 형식 및 기타 저장 매개변수를 지정할 수 있습니다.  
`SaveOptions`를 통해 출력 파일 이름, 형식 및 문서를 PDF로 래스터화할지 여부를 제어할 수 있습니다. 접미사를 추가하면 원본 파일을 그대로 유지합니다:

```java
import com.groupdocs.redaction.options.SaveOptions;

SaveOptions saveOptions = new SaveOptions();
saveOptions.setAddSuffix(true); // Adds "_Redacted" to the file name
saveOptions.setRasterizeToPDF(false);

redactor.save(saveOptions);
```

## 일반적인 사용 사례
1. **법률 문서** – 계약서를 상대 변호사에게 보내기 전에 작성자 정보를 레드랙션합니다.  
2. **기업 보고서** – 분기 실적을 주주에게 공개할 때 관리자 이름을 삭제합니다.  
3. **프로젝트 파일** – 아카이브하거나 공개 저장소에 업로드하기 전에 내부 프로젝트 문서를 정리합니다.

## 문제 해결 팁
- **파일을 찾을 수 없음** – `inputFilePath`에 지정된 경로가 존재하는 파일을 가리키는지와 애플리케이션에 읽기 권한이 있는지 확인합니다.  
- **메타데이터 필드 누락** – 모든 문서 유형이 동일한 메타데이터 키를 저장하는 것은 아니므로, 먼저 Office에서 문서 속성을 확인합니다.  
- **라이선스 오류** – `Redactor` 인스턴스를 생성하기 전에 라이선스 파일이 올바르게 로드되었는지 확인합니다.

## 성능 고려 사항
- `finally` 블록에 표시된 대로 `Redactor` 객체를 즉시 닫아 네이티브 리소스를 해제합니다.  
- PDF 미리보기가 필요하지 않은 한 큰 문서를 래스터화하지 마세요. 래스터화는 300페이지 파일의 경우 CPU와 메모리 사용량을 최대 3배까지 증가시킬 수 있습니다.

## 자주 묻는 질문

**Q1: 메타데이터 레드랙션이란?**  
A1: 메타데이터 레드랙션은 숨겨진 문서 속성(예: author, manager 또는 사용자 정의 태그)을 제거하여 민감한 정보가 우발적으로 노출되는 것을 방지하는 작업입니다.

**Q2: GroupDocs.Redaction을 다른 파일 유형에도 사용할 수 있나요?**  
A2: 예, 라이브러리는 PDF, DOCX, PPTX, XLSX 등 100개가 넘는 다양한 형식을 지원합니다.

**Q3: 레드랙션 중 오류를 어떻게 처리하나요?**  
A3: `apply` 호출을 try‑catch 블록으로 감싸고, `finally` 절에서 항상 `Redactor`를 닫아 리소스가 해제되도록 합니다.

**Q4: 사용자 정의 메타데이터 필드를 레드랙션할 수 있나요?**  
A5: 물론 가능합니다. `MetadataFilters.Custom("YourFieldName")`를 사용해 문서에 저장된任意의 사용자 정의 속성을 대상으로 지정할 수 있습니다.

**Q5: GroupDocs.Redaction 사용 시 모범 사례는 무엇인가요?**  
A5:  
- 애플리케이션 시작 시 라이선스를 먼저 로드합니다.  
- `Redactor` 객체를 즉시 닫습니다.  
- `SaveOptions`를 사용해 접미사를 추가하여 원본 파일을 그대로 유지합니다.  
- 배치 처리를 하기 전에 문서 복사본으로 레드랙션을 테스트합니다.

**Q6: EraseMetadataRedaction이 배치 작업을 지원하나요?**  
A6: 파일 경로 컬렉션을 반복하면서 각 파일마다 새 `Redactor`를 생성하고 동일한 레드랙션 로직을 적용할 수 있습니다.

**Q7: EraseMetadataRedaction을 다른 레드랙션 유형과 결합할 수 있나요?**  
A7: 예, 저장하기 전에 여러 레드랙션 객체를 체인처럼 연결할 수 있습니다(예: 텍스트 레드랙션 후 메타데이터 레드랙션).

## 리소스

- **문서**: [GroupDocs Redaction Java Docs](https://docs.groupdocs.com/redaction/java/)  
- **API 레퍼런스**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java)  
- **다운로드**: [Latest Releases](https://releases.groupdocs.com/redaction/java/)  
- **GitHub**: [GroupDocs GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **무료 지원**: [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)  
- **임시 라이선스**: [Acquire a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**마지막 업데이트:** 2026-10-01  
**테스트 환경:** GroupDocs.Redaction 24.9 for Java  
**작성자:** GroupDocs

## 관련 튜토리얼

- [Groupdocs Redaction Java 문서 메타데이터 추출](/redaction/java/metadata-redaction/groupdocs-redaction-java-document-metadata-extraction/)
- [GroupDocs.Redaction을 사용한 Java 메타데이터 제거 방법](/redaction/java/metadata-redaction/metadata-redaction-groupdocs-java-guide/)
- [Groupdocs Redaction Java를 사용한 문서 정보 검색](/redaction/java/document-information/retrieve-document-info-using-groupdocs-redaction-java/)