---
date: '2026-03-22'
description: GroupDocs를 사용하여 Java에서 메타데이터를 삭제하고 저자 메타데이터를 제거하는 방법을 배워보세요. 이 튜토리얼에서는
  편집된 문서 파일을 안전하게 저장하는 방법을 보여줍니다.
keywords:
- metadata redaction in Java
- GroupDocs Redaction setup
- removing metadata fields
title: 'GroupDocs와 함께 Java에서 메타데이터 삭제 방법: 단계별 가이드'
type: docs
url: /ko/java/metadata-redaction/groupdocs-redaction-java-metadata-implementation/
weight: 1
---

# Java에서 GroupDocs를 사용하여 메타데이터 삭제하는 방법

오늘날 디지털 환경에서 문서 내부의 민감한 정보를 보호하는 것은 필수이며, **메타데이터 삭제 방법을 아는 것**은 이러한 보호의 핵심 요소입니다. 이 가이드에서는 `EraseMetadataRedaction`을 사용하여 Word 파일에서 *Author*와 *Manager*와 같은 메타데이터를 제거하는 방법을 GroupDocs.Redaction for Java와 함께 배웁니다. 튜토리얼을 마치면 깔끔하고 프라이버시가 보장된 문서를 얻고, **삭제된 문서** 파일을 안전하게 공유하거나 보관하는 방법을 알게 됩니다.

## 빠른 답변
- **EraseMetadataRedaction은 무엇을 하나요?** 선택한 메타데이터 필드를 문서에서 제거합니다.  
- **어떤 라이브러리가 이 기능을 제공하나요?** GroupDocs.Redaction for Java.  
- **라이선스가 필요합니까?** 테스트용 무료 체험판을 사용할 수 있으며, 프로덕션 환경에서는 영구 라이선스가 필요합니다.  
- **여러 필드를 한 번에 지정할 수 있나요?** 예, 논리 OR을 사용해 필터를 결합하면 됩니다.  
- **프로세스가 스레드‑안전한가요?** Redactor 인스턴스는 스레드 간에 공유되지 않으며, 작업당 새 인스턴스를 생성해야 합니다.

## Java에서 메타데이터 삭제하는 방법
이 섹션에서는 **작성자 메타데이터** 및 기타 원하지 않는 속성을 파일에서 **제거**하는 정확한 단계를 안내합니다.

### EraseMetadataRedaction이란?
`EraseMetadataRedaction`은 삭제할 메타데이터 항목을 지정할 수 있는 내장 레다션 클래스입니다. GroupDocs.Redaction이 지원하는 다양한 문서 형식에서 작동하여 숨겨진 작성자 정보를 누출되지 않도록 합니다.

### GroupDocs와 함께 EraseMetadataRedaction을 사용하는 이유
- **규정 준수** – GDPR, HIPAA 또는 기업 정책에 따라 개인 식별자를 제거합니다.  
- **일관성** – PDF, DOCX, PPTX 등 여러 형식에 동일한 레다션 로직을 적용합니다.  
- **성능** – 외부 도구 없이 메모리 내에서 레다션이 수행됩니다.  
- **유연성** – 여러 `MetadataFilters`를 결합해 정확히 필요한 항목만 타깃팅합니다.

## 사전 요구 사항
- Java 8 이상 설치  
- Maven(또는 JAR를 수동으로 추가할 수 있는 환경)  
- GroupDocs.Redaction for Java (버전 24.9 이상)  
- 유효한 GroupDocs 체험판 또는 영구 라이선스

## GroupDocs.Redaction for Java 설정

### Maven 설치
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
또는 [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/)에서 최신 JAR를 다운로드합니다.

### 라이선스 획득
무료 체험판을 받거나 GroupDocs 포털에서 임시 라이선스를 구매합니다. 라이선스 파일은 애플리케이션이 로드할 수 있는 위치(예: 클래스패스 루트)에 배치해야 합니다.

### 기본 초기화 및 설정
다음은 DOCX 파일에 대해 `Redactor` 인스턴스를 생성하는 최소 예제입니다:

```java
import com.groupdocs.redaction.Redactor;

String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
Redactor redactor = new Redactor(filePath);
```

## Java에서 EraseMetadataRedaction 사용 방법
아래 섹션에서는 구현을 명확하고 실행 가능한 단계로 나눕니다.

### 기능: 특정 메타데이터 항목 정리

#### 개요
`EraseMetadataRedaction`을 사용해 **Author**와 **Manager** 메타데이터 필드를 삭제합니다. 이는 내부 보고서를 외부 파트너와 공유할 때 흔히 요구되는 작업입니다.

#### 단계별 구현

##### 1️⃣ Redactor 객체 초기화
정리하려는 문서를 가리키는 `Redactor` 인스턴스를 생성합니다:

```java
import com.groupdocs.redaction.Redactor;

String inputFilePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
final Redactor redactor = new Redactor(inputFilePath);
```

##### 2️⃣ EraseMetadataRedaction 적용
`EraseMetadataRedaction` 클래스와 `MetadataFilters`를 함께 사용합니다. 비트 OR(`|`) 연산자를 사용해 `Author`와 `Manager` 필터를 결합하면 두 필드를 한 번에 삭제할 수 있습니다:

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
`SaveOptions`를 조정해 출력 파일 이름과 문서를 PDF로 래스터화할지 여부를 제어합니다:

```java
import com.groupdocs.redaction.options.SaveOptions;

SaveOptions saveOptions = new SaveOptions();
saveOptions.setAddSuffix(true); // Adds "_Redacted" to the file name
saveOptions.setRasterizeToPDF(false);

redactor.save(saveOptions);
```

### 일반 사용 사례
1. **법률 문서** – 계약서를 상대 변호사에게 보내기 전에 작성자 정보를 레다션합니다.  
2. **기업 보고서** – 분기 실적을 주주에게 공개할 때 관리자 이름을 제거합니다.  
3. **프로젝트 파일** – 내부 프로젝트 문서를 보관하거나 공개 저장소에 업로드하기 전에 정리합니다.

### 문제 해결 팁
- **파일을 찾을 수 없음** – `inputFilePath`가 실제 파일을 가리키는지, 애플리케이션에 읽기 권한이 있는지 확인합니다.  
- **메타데이터 필드가 없음** – 모든 문서 형식이 동일한 메타데이터 키를 저장하는 것은 아니므로, 먼저 Office에서 문서 속성을 확인합니다.  
- **라이선스 오류** – `Redactor` 인스턴스를 만들기 전에 라이선스 파일이 올바르게 로드되었는지 확인합니다.

## 성능 고려 사항
- `finally` 블록에 표시된 대로 `Redactor` 객체를 즉시 닫아 네이티브 리소스를 해제합니다.  
- PDF 미리보기가 필요하지 않은 경우 큰 문서를 래스터화하지 마세요. 래스터화는 CPU와 메모리 사용량을 크게 증가시킬 수 있습니다.

## 자주 묻는 질문

**Q1: 메타데이터 레다션이란 무엇인가요?**  
A1: 메타데이터 레다션은 작성자, 관리자 또는 사용자 정의 태그와 같은 숨겨진 문서 속성을 제거해 민감한 정보가 우연히 노출되는 것을 방지하는 작업입니다.

**Q2: GroupDocs.Redaction을 다른 파일 형식에도 사용할 수 있나요?**  
A2: 예, 이 라이브러리는 PDF, DOCX, PPTX, XLSX 등 다양한 형식을 지원합니다.

**Q3: 레다션 중 오류를 어떻게 처리하나요?**  
A3: `apply` 호출을 try‑catch 블록으로 감싸고, `finally` 절에서 항상 `Redactor`를 닫아 리소스가 해제되도록 합니다.

**Q4: 사용자 정의 메타데이터 필드를 레다션할 수 있나요?**  
A4: 물론입니다. `MetadataFilters.Custom("YourFieldName")`(또는 해당 열거형)를 사용해 원하는 사용자 정의 속성을 타깃팅합니다.

**Q5: GroupDocs.Redaction 사용 시 권장 사항은 무엇인가요?**  
A5:  
- 애플리케이션 시작 시 라이선스를 먼저 로드합니다.  
- `Redactor` 객체를 즉시 닫습니다.  
- `SaveOptions`에 접미사를 추가해 원본 파일을 그대로 유지합니다.  
- 배치 처리 전에 반드시 문서 복사본으로 레다션을 테스트합니다.

**Q6: EraseMetadataRedaction이 배치 작업을 지원하나요?**  
A6: 파일 경로 컬렉션을 순회하면서 각 파일마다 새 `Redactor`를 생성하고 동일한 레다션 로직을 적용하면 됩니다.

**Q7: EraseMetadataRedaction을 다른 레다션 유형과 결합할 수 있나요?**  
A7: 예, 텍스트 레다션 후 메타데이터 레다션과 같이 여러 레다션 객체를 체인으로 연결한 뒤 저장할 수 있습니다.

## 리소스

- **문서**: [GroupDocs Redaction Java Docs](https://docs.groupdocs.com/redaction/java/)  
- **API 레퍼런스**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java)  
- **다운로드**: [Latest Releases](https://releases.groupdocs.com/redaction/java/)  
- **GitHub**: [GroupDocs GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **무료 지원**: [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)  
- **임시 라이선스**: [Acquire a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**마지막 업데이트:** 2026-03-22  
**테스트 환경:** GroupDocs.Redaction 24.9 for Java  
**작성자:** GroupDocs  

---