---
date: '2026-04-20'
description: GroupDocs.Redaction for Java를 사용하여 PDF 마지막 페이지를 편집하고, PDF 텍스트를 교체하며,
  민감한 데이터를 효율적으로 숨기는 방법을 배우세요.
keywords:
- redact last page pdf
- replace text pdf java
- hide sensitive data pdf
title: Java용 GroupDocs.Redaction으로 PDF 마지막 페이지 가리기
type: docs
url: /ko/java/page-redaction/java-pdf-redaction-groupdocs-last-page-focus/
weight: 1
---

# PDF 마지막 페이지 가리기 - GroupDocs.Redaction for Java

오늘날 디지털 환경에서는 **redact last page pdf** 파일을 가리는 것이 기밀 정보를 보호하고 개인정보 보호 규정을 준수하는 데 필수적입니다. 이 튜토리얼에서는 GroupDocs.Redaction for Java를 사용하여 PDF의 마지막 페이지를 대상으로 특정 영역의 민감한 데이터를 숨기는 방법을 안내합니다. 끝까지 진행하면 텍스트 pdf java 스타일을 교체하고 민감한 데이터 pdf를 어디서든 자신 있게 숨길 수 있게 됩니다.

## 빠른 답변
- **What is the primary goal?** PDF의 마지막 페이지와 그 안의 특정 영역을 가리는 것입니다.  
- **Which library is used?** GroupDocs.Redaction for Java.  
- **Do I need a license?** 테스트용으로는 체험판 또는 임시 라이선스로 충분하지만, 운영 환경에서는 정식 라이선스가 필요합니다.  
- **What Java version is required?** Maven 지원이 포함된 Java 8 이상.  
- **Can I target other pages?** 예, 동일한 필터를 조정하여任意 페이지 범위에 적용할 수 있습니다.

## PDF를 가리기란 무엇인가요?
가리기는 PDF에서 내용을 영구적으로 제거하거나 가려서 복구할 수 없도록 만드는 것을 의미합니다. **redact last page pdf** 를 수행하면 마지막 페이지의 모든 기밀 정보가 완전히 숨겨집니다.

## 왜 GroupDocs.Redaction for Java를 사용하나요?
GroupDocs.Redaction은 페이지 범위, 영역 기반, 텍스트 기반 필터 등 풍부한 필터 세트를 제공하여 제거되는 내용을 정확히 제어할 수 있습니다. 특히 다음과 같은 경우에 유용합니다:
- **Replacing text pdf java** 스타일을 문서의 다른 부분을 변경하지 않고 교체합니다.  
- **Hiding sensitive data pdf** 예: 개인 식별자, 재무 수치, 법적 조항 등.  
- 대량 문서 배치에 대한 규정 준수 검사를 자동화합니다.

## 전제 조건
- **Java Development Kit (JDK) 8+** 가 설치되어 있어야 합니다.  
- **Maven** 은 의존성 관리를 위해 필요합니다.  
- **GroupDocs.Redaction** 라이선스(체험판, 임시, 구매)를 사용할 수 있어야 합니다.  

## GroupDocs.Redaction for Java 설정

### Maven 설정
다음과 같이 `pom.xml`에 저장소와 의존성을 추가합니다:

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
Maven을 사용하지 않으려면 공식 사이트에서 최신 JAR 파일을 다운로드하세요: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

#### 라이선스 획득 단계
- **Free Trial:** 약정 없이 모든 기능을 테스트합니다.  
- **Temporary License:** 단기 프로젝트나 평가에 사용합니다.  
- **Purchase:** 무제한 사용 및 우선 지원을 활성화합니다.

## 기본 초기화
먼저, PDF 파일을 가리키는 `Redactor` 인스턴스를 생성합니다:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_PDF");
```

이 객체는 모든 가리기 작업의 진입점입니다.

## 마지막 페이지 PDF 가리기 – 단계별 가이드

### 기능 1: 마지막 페이지의 특정 영역 가리기

#### 단계 1: PDF 문서 로드
```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_PDF");
```

#### 단계 2: 페이지 정보 가져오기
```java
IDocumentInfo info = redactor.getDocumentInfo();
PageInfo lastPage = info.getPages().get(info.getPageCount() - 1);
```
마지막 페이지의 크기를 알면 정확한 좌표를 정의할 수 있습니다.

#### 단계 3: 교체 옵션 정의
```java
ReplacementOptions options = new ReplacementOptions("[secret]");
```
여기서는 가려진 내용을 대체할 자리 표시자 텍스트를 선택합니다.

#### 단계 4: 목표 가리기를 위한 필터 설정
```java
options.setFilters(new RedactionFilter[] {
    new PageRangeFilter(PageSeekOrigin.End, 0, 1),
    new PageAreaFilter(
        new java.awt.Point(0, lastPage.getHeight() / 2),
        new java.awt.Dimension(lastPage.getWidth(), lastPage.getHeight() / 2)
    )
});
```
- `PageRangeFilter` 가 **마지막 페이지**를 선택합니다.  
- `PageAreaFilter` 가 해당 페이지의 하반부에만 작업을 제한합니다.

#### 단계 5: 가리기 적용 (replace text pdf java)
```java
RedactorChangeLog result = redactor.apply(new ExactPhraseRedaction("bibliography", false, options));
```
문구 “bibliography” 가 정의된 영역 내에서만 “[secret]” 로 교체됩니다.

#### 단계 6: 성공 확인 및 저장
```java
if (result.getStatus() != RedactionStatus.Failed) {
    redactor.save("YOUR_OUTPUT_DIRECTORY/redacted_output.pdf");
}
```
출력 파일을 쓰기 전에 항상 상태를 확인하세요.

#### 단계 7: 리소스 정리
```java
redactor.close();
```
`Redactor` 를 닫으면 메모리와 파일 핸들이 해제됩니다.

### 기능 2: 가리기를 위한 페이지 범위 필터링

#### 단계 1: PDF 문서 로드
```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_PDF");
```

#### 단계 2: 문서 정보 접근
```java
IDocumentInfo info = redactor.getDocumentInfo();
```

#### 단계 3: 페이지 범위 필터 생성 (hide sensitive data pdf)
```java
PageRangeFilter pageRangeFilter = new PageRangeFilter(PageSeekOrigin.End, 0, 1);
```
이 필터는 마지막 페이지를 분리하여 필요한 모든 가리기 로직을 적용할 수 있게 합니다.

### 기능 3: PDF 페이지의 영역 기반 가리기

#### 단계 1: PDF 문서 로드
```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_PDF");
```

#### 단계 2: 페이지 상세 정보 가져오기
```java
IDocumentInfo info = redactor.getDocumentInfo();
PageInfo lastPage = info.getPages().get(info.getPageCount() - 1);
```

#### 단계 3: 영역 필터 정의 (hide sensitive data pdf)
```java
PageAreaFilter areaFilter = new PageAreaFilter(
    new java.awt.Point(0, lastPage.getHeight() / 2),
    new java.awt.Dimension(lastPage.getWidth(), lastPage.getHeight() / 2)
);
```
이 필터는 마지막 페이지의 하반부를 대상으로 하며, 바닥글이나 서명을 제거하는 데 적합합니다.

#### 단계 4: 리소스 해제
```java
redactor.close();
```

## 실용적인 적용 사례
- **Legal Documents:** 공유 전 마지막 페이지에서 클라이언트 이름이나 사건 번호를 가립니다.  
- **Financial Reports:** 계좌 번호나 기밀 요약을 숨깁니다.  
- **Healthcare Records:** HIPAA 준수를 위해 환자 식별자를 제거합니다.  
- **Pre‑Release Drafts:** 아직 검토 중인 섹션을 가립니다.

## 성능 팁
- **Reuse the `Redactor`** 배치에서 여러 PDF를 처리할 때 재사용합니다.  
- **Close the object promptly** 특히 큰 파일의 경우 메모리 누수를 방지하기 위해 객체를 즉시 닫습니다.  
- **Test on a sample** 프로덕션 문서에 적용하기 전에 샘플에서 필터 좌표를 확인합니다.

## 자주 묻는 질문

**Q: 여러 페이지를 한 번에 가릴 수 있나요?**  
A: 예. `PageRangeFilter` 매개변수를 조정하여 원하는 범위(예: 페이지 1‑5에 대해 `new PageRangeFilter(1, 5)`)를 포함할 수 있습니다.

**Q: 라이브러리가 비밀번호로 보호된 PDF를 지원하나요?**  
A: 물론입니다. 암호화된 파일을 열려면 `Redactor` 생성자에 비밀번호를 전달하면 됩니다.

**Q: 가리기 색상이나 오버레이를 어떻게 변경하나요?**  
A: `ReplacementOptions` 를 사용하여 사용자 정의 이미지, 색상 또는 텍스트 오버레이를 지정합니다.

**Q: 가리기가 영구적인가요?**  
A: 예. 제거된 내용은 출력 PDF에 어디에도 저장되지 않아 복구할 수 없습니다.

**Q: 정규식 패턴을 기반으로 가려야 하면 어떻게 하나요?**  
A: GroupDocs.Redaction은 `RegexRedaction` 을 제공하며, 이는 `ExactPhraseRedaction` 과 유사하게 작동합니다.

---

**마지막 업데이트:** 2026-04-20  
**테스트 환경:** GroupDocs.Redaction 24.9 for Java  
**작성자:** GroupDocs