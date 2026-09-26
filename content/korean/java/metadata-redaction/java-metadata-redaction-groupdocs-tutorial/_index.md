---
date: '2026-09-26'
description: Java에서 GroupDocs를 사용하여 metadata를 편집하는 방법을 배워보세요. 기밀 문서 metadata를 안전하게
  제거하면서 원본 format을 그대로 유지합니다.
keywords:
- how to redact metadata
- GroupDocs Redaction Java
- secure document processing
- metadata removal Java
lastmod: '2026-09-26'
og_description: Java에서 GroupDocs를 사용하여 metadata를 편집하는 방법 – 기밀 문서 metadata를 안전하게 제거하고
  원본 format을 유지하는 단계별 가이드
og_image_alt: Guide showing metadata redaction using GroupDocs in Java
og_title: Java에서 GroupDocs를 사용하여 metadata를 편집하는 방법
schemas:
- author: GroupDocs
  dateModified: '2026-09-26'
  description: Learn how to redact metadata with GroupDocs in Java, securely removing
    confidential document metadata while keeping the original format intact.
  headline: How to redact metadata with GroupDocs in Java
  type: TechArticle
- description: Learn how to redact metadata with GroupDocs in Java, securely removing
    confidential document metadata while keeping the original format intact.
  name: How to redact metadata with GroupDocs in Java
  steps:
  - name: import necessary classes
    text: These imports give you access to the redaction engine, save options, and
      metadata utilities.
  - name: initialize redactor
    text: Instantiate the `Redactor` with the path to your source file.
  - name: configure metadata search and redaction
    text: Create a `MetadataSearchRedaction` that looks for the exact string **"Company
      Ltd."** and replaces it with **"--company--"**. The `setFilter` call limits
      the operation to the *Company* metadata field only.
  - name: apply the redaction
    text: Run the redaction against the opened document.
  - name: save with custom options
    text: '`SaveOptions` allows you to specify output format, file naming, and other
      saving parameters for the redacted document. Configure `SaveOptions` so the
      redacted file gets a “_Redacted” suffix while preserving its original format.'
  - name: release resources
    text: Always close the `Redactor` to free native resources and avoid memory leaks.
  type: HowTo
- questions:
  - answer: It’s a powerful library that enables you to redact text, metadata, and
      images in documents using Java applications.
    question: What is GroupDocs.Redaction for Java?
  - answer: Yes, but with limitations. A free trial or temporary license allows full
      access for testing purposes.
    question: Can I use GroupDocs.Redaction without purchasing a license?
  - answer: Use `SaveOptions` to specify your requirements, such as avoiding rasterization
      when saving to PDF.
    question: How do I ensure document formats are preserved during redaction?
  - answer: It supports a wide range, including Word, Excel, PowerPoint, PDF, and
      many more.
    question: What types of documents can be redacted using GroupDocs.Redaction?
  - answer: Visit the [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33)
      for assistance.
    question: Where can I find support if I run into issues?
  type: FAQPage
tags:
- metadata redaction
- GroupDocs
- Java document security
- redaction tutorial
title: Java에서 GroupDocs를 사용하여 metadata를 편집하는 방법
type: docs
url: /ko/java/metadata-redaction/java-metadata-redaction-groupdocs-tutorial/
weight: 1
---

# GroupDocs를 사용하여 Java에서 메타데이터를 삭제하는 방법

이 포괄적인 튜토리얼에서는 GroupDocs.Redaction for Java를 사용하여 Word, PDF 및 기타 많은 문서 유형에서 **메타데이터를 삭제하는 방법**을 배웁니다. 가이드가 끝날 때쯤이면 메타데이터 삭제를 모든 Java 기반 서비스에 삽입할 수 있게 되어, 회사 이름, 저자 또는 사용자 정의 속성과 같은 기밀 정보가 조직을 떠나지 않도록 보장합니다.

## 빠른 답변
- **MetadataSearchRedaction은 무엇을 하나요?** 특정 메타데이터 필드를 검색하고 해당 값을 사용자 정의 텍스트로 교체합니다.  
- **필요한 라이브러리는 무엇인가요?** GroupDocs.Redaction for Java (v24.9 이상).  
- **라이선스가 필요합니까?** 평가용으로는 무료 체험판을 사용할 수 있으며, 프로덕션에서는 정식 라이선스가 필요합니다.  
- **원본 파일 형식을 유지할 수 있나요?** 예—`SaveOptions`를 사용하여 원본 형식을 보존합니다.  
- **이 접근 방식이 스레드 안전한가요?** 각 `Redactor` 인스턴스는 독립적이므로 문서를 병렬로 처리할 수 있습니다.

## GroupDocs를 사용하여 메타데이터를 삭제하는 방법?
`Redactor`는 문서를 로드하고 삭제 작업을 제공하는 핵심 클래스입니다.  
`Redactor` 인스턴스로 소스 문서를 로드하고, 삭제하려는 정확한 메타데이터 키를 대상으로 하는 `MetadataSearchRedaction`을 구성한 뒤, 삭제를 적용하고 마지막으로 `SaveOptions`를 사용해 파일을 저장합니다. 이 전체 워크플로는 몇 줄의 코드만으로 표현할 수 있으며, DOCX부터 PDF까지 지원되는 모든 형식에서 작동합니다.

## GroupDocs에서 메타데이터 삭제란 무엇인가요?
`MetadataSearchRedaction`은 특정 메타데이터 속성(예: *Company*, *Author*)을 대상으로 하여 그 내용을 플레이스홀더로 교체할 수 있는 특수 클래스입니다. 외부 파트너와 문서를 공유하기 전에 기업 데이터를 익명화해야 할 때 이상적입니다. 삭제 과정은 다른 문서 요소를 변경하지 않으며, 메타데이터가 제거된 후에도 시각적 레이아웃과 내용이 그대로 유지됩니다.

## GroupDocs와 함께 메타데이터 삭제를 사용하는 이유는?
GroupDocs를 사용한 메타데이터 삭제는 문서에서 민감한 정보를 제거하면서 원본 외관과 구조를 유지하는 신뢰할 수 있는 방법을 제공합니다. 메타데이터 필드에만 집중함으로써 눈에 보이는 내용을 수정하거나 우발적인 데이터 유출 위험 없이 빠르게 개인정보 보호 표준을 준수할 수 있습니다.

- **정밀도** – 지정한 필드만 삭제하고 문서의 나머지는 그대로 둡니다.  
- **규정 준수** – 숨겨진 식별자를 제거하여 GDPR, HIPAA 및 기타 개인정보 보호 규정을 충족하는 데 도움을 줍니다.  
- **자동화 준비** – 배치 처리 파이프라인이나 마이크로서비스에 원활히 통합됩니다.  
- **다양한 형식 지원** – GroupDocs.Redaction은 **50개 이상의 입력 및 출력 형식**(DOCX, PDF, PPTX, XLSX 및 이미지 유형 포함)을 지원하며 전체 문서를 메모리에 로드하지 않고도 수백 페이지 파일을 처리할 수 있습니다.

## 전제 조건
- **GroupDocs.Redaction for Java** ≥ 24.9.  
- Java 8 또는 그 이상이 머신에 설치되어 있어야 합니다.  
- IntelliJ IDEA 또는 Eclipse와 같은 IDE(선택 사항이지만 권장).  
- Maven에 대한 기본적인 이해(또는 JAR를 수동으로 추가할 수 있는 능력).  

## GroupDocs.Redaction for Java 설정

`pom.xml`에 저장소와 의존성을 추가합니다. 이 단계는 Maven이 라이브러리를 자동으로 다운로드하도록 보장합니다.

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

*또는 공식 릴리스 페이지에서 JAR를 직접 다운로드할 수도 있습니다:*  
[GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/)

### 라이선스 획득
- **무료 체험** – 모든 기능을 탐색할 수 있는 체험 라이선스를 다운로드합니다.  
- **임시 라이선스** – 장기 테스트에 사용합니다.  
- **정식 라이선스** – 프로덕션 배포에 필요합니다.

## 기본 초기화
`Redactor`는 문서를 로드하고 다양한 삭제를 적용할 수 있는 메서드를 제공합니다.  
처리하려는 문서를 가리키는 `Redactor` 인스턴스를 생성합니다.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

## 구현 가이드

### 단계 1: 필요한 클래스 가져오기
이러한 import는 삭제 엔진, 저장 옵션 및 메타데이터 유틸리티에 접근할 수 있게 해줍니다.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.redactions.MetadataFilters;
import com.groupdocs.redaction.redactions.MetadataSearchRedaction;
```

### 단계 2: Redactor 초기화
`Redactor`를 소스 파일 경로와 함께 인스턴스화합니다.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

### 단계 3: 메타데이터 검색 및 삭제 구성
정확히 **"Company Ltd."** 문자열을 찾고 **"--company--"** 로 교체하는 `MetadataSearchRedaction`을 생성합니다. `setFilter` 호출은 작업을 *Company* 메타데이터 필드에만 제한합니다.

```java
MetadataSearchRedaction redaction = new MetadataSearchRedaction("Company Ltd.", "--company--");
redaction.setFilter(MetadataFilters.Company);
```

### 단계 4: 삭제 적용
열린 문서에 대해 삭제를 실행합니다.

```java
redactor.apply(redaction);
```

### 단계 5: 사용자 지정 옵션으로 저장
`SaveOptions`를 사용하면 삭제된 문서의 출력 형식, 파일 명명 및 기타 저장 매개변수를 지정할 수 있습니다.  
삭제된 파일에 원본 형식을 유지하면서 “_Redacted” 접미사가 붙도록 `SaveOptions`를 구성합니다.

```java
SaveOptions tmp0 = new SaveOptions();
tmp0.setAddSuffix(true);  // Adds "_Redacted" to file name
tmp0.setRasterizeToPDF(false);  // Keeps original format

redactor.save(tmp0);
```

### 단계 6: 리소스 해제
네이티브 리소스를 해제하고 메모리 누수를 방지하기 위해 항상 `Redactor`를 닫으세요.

```java
finally {
    redactor.close();
}
```

## 일반적인 문제 및 해결책
- **FileNotFoundException** – `Redactor`에 전달한 경로를 다시 확인하세요. 절대 경로나 `Paths.get(...)`를 사용하면 신뢰성이 높아집니다.  
- **변경 사항이 없음** – 대상 메타데이터 필드에 실제로 검색 문자열이 포함되어 있는지 확인하세요; 메타데이터는 기본적으로 대소문자를 구분합니다.  
- **대용량 파일에서 메모리 부족 오류** – 문서를 작은 배치로 처리하고 각 파일 후에 `redactor.close()`를 즉시 호출하세요.

## 실용적인 적용 사례
1. **법률 문서** – 계약서를 제3자에게 보내기 전에 클라이언트 회사 이름을 제거합니다.  
2. **재무 보고** – 감사 파일의 내부 식별자를 익명화합니다.  
3. **협업 프로젝트** – 외부 벤더와 초안을 공유할 때 독점 정보를 보호합니다.

## 성능 고려 사항
- **메모리 관리** – 라이브러리는 전체 문서를 메모리에 보관합니다; 각 파일 후에 `Redactor`를 닫는 것이 필수적입니다.  
- **배치 처리** – 대량 시나리오에서는 파일 컬렉션을 순회하고 단일 `SaveOptions` 인스턴스를 재사용합니다.  
- **업데이트 유지** – 새로운 릴리스는 성능 개선 및 버그 수정을 제공하므로 항상 최신 안정 버전을 목표로 하세요.

## 자주 묻는 질문

**Q: GroupDocs.Redaction for Java란 무엇인가요?**  
A: Java 애플리케이션을 사용하여 문서의 텍스트, 메타데이터 및 이미지를 삭제할 수 있는 강력한 라이브러리입니다.

**Q: 라이선스를 구매하지 않고 GroupDocs.Redaction을 사용할 수 있나요?**  
A: 예, 하지만 제한이 있습니다. 무료 체험판이나 임시 라이선스를 사용하면 테스트 목적으로 전체 기능에 접근할 수 있습니다.

**Q: 삭제 중에 문서 형식이 유지되도록 하려면 어떻게 해야 하나요?**  
A: PDF로 저장할 때 래스터화 방지와 같은 요구 사항을 지정하려면 `SaveOptions`를 사용하세요.

**Q: GroupDocs.Redaction을 사용하여 어떤 유형의 문서를 삭제할 수 있나요?**  
A: Word, Excel, PowerPoint, PDF 등 다양한 문서를 지원합니다.

**Q: 문제가 발생하면 어디에서 지원을 받을 수 있나요?**  
A: 지원을 위해 [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) 를 방문하세요.

**Q: MetadataSearchRedaction이 암호화된 문서에서도 작동하나요?**  
A: 예. 비밀번호 매개변수를 받는 `Redactor` 생성자를 사용해 적절한 비밀번호로 문서를 로드하면 됩니다.

**Q: 한 번에 여러 메타데이터 삭제를 연쇄적으로 적용할 수 있나요?**  
A: 물론입니다. 여러 `MetadataSearchRedaction` 객체를 생성하고, 서로 다른 필터를 설정한 뒤 저장하기 전에 순차적으로 적용하세요.

**Q: 저장하기 전에 삭제를 미리 볼 수 있나요?**  
A: `redactor.getRedactions()`를 호출하여 보류 중인 삭제 목록을 가져오고 프로그래밍 방식으로 검사할 수 있습니다.

## 추가 자료
- **문서**: [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/)에서 자세한 가이드를 확인하세요.  
- **API 레퍼런스**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java)에서 전체 API 레퍼런스를 확인하세요.  
- **라이브러리 다운로드**: [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/)에서 최신 릴리스를 받으세요.  
- **소스 코드**: [GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)에서 확인하고 기여하세요.  
- **지원**: 무료 지원 채널인 [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33)에서 도움을 받으세요.

---

**마지막 업데이트:** 2026-09-26  
**테스트 환경:** GroupDocs.Redaction 24.9 for Java  
**작성자:** GroupDocs

## 관련 튜토리얼

- [Groupdocs Redaction Java 문서 메타데이터 추출](/redaction/java/metadata-redaction/groupdocs-redaction-java-document-metadata-extraction/)
- [metadata 텍스트 교체 java – GroupDocs와 함께하는 보안 삭제](/redaction/java/metadata-redaction/java-redaction-metadata-text-replacement-guide/)
- [Groupdocs Redaction Java를 사용한 문서 정보 가져오기](/redaction/java/document-information/retrieve-document-info-using-groupdocs-redaction-java/)