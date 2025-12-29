---
date: '2025-12-29'
description: GroupDocs.Redaction for Java를 사용하여 스캔된 문서 이미지의 민감 정보를 삭제하는 방법을 배웁니다.
  설정, 이미지 영역 삭제 및 검증을 포함한 단계별 가이드.
keywords:
- Java image redaction
- GroupDocs.Redaction for Java
- image area redaction
title: Java와 GroupDocs를 사용하여 스캔된 문서 이미지 가리기
type: docs
url: /ko/java/image-redaction/java-image-redaction-groupdocs-tutorial/
weight: 1
---

# Java에서 GroupDocs를 사용하여 스캔된 문서 이미지 가리기

오늘날 디지털 환경에서 **스캔된 문서 가리기** 이미지는 개인 정보 보호와 규정 준수를 위해 필수적입니다. 스캔된 계약서에서 개인 데이터를 숨기거나 의료 이미지에서 환자 정보를 가려야 할 경우, 이 튜토리얼에서는 **GroupDocs.Redaction for Java**를 사용하여 **이미지를 가리는 방법**을 빠르고 안정적으로 보여줍니다. 프로젝트 설정부터 가리기가 성공했는지 확인하는 과정까지 모두 안내하므로, 어떤 Java 애플리케이션에도 자신 있게 솔루션을 통합할 수 있습니다.

## 빠른 답변
- **Java에서 이미지 가리기를 처리하는 라이브러리는 무엇인가요?** GroupDocs.Redaction for Java  
- **가리기 색상을 선택할 수 있나요?** Yes – any `java.awt.Color` (e.g., `Color.BLUE`)  
- **프로덕션에 라이선스가 필요합니까?** Yes, a valid GroupDocs license is needed  
- **원본 이미지가 덮어쓰기 되나요?** No – you save the result to a new file  
- **지원되는 Java 버전은 무엇인가요?** Java 8+ (compatible with modern JDKs)

## 이미지 가리기란 무엇이며 왜 스캔된 문서 이미지를 가려야 하나요?
이미지 가리기는 이름, 번호, 서명 등과 같은 민감한 시각 정보를 영구적으로 가려 복구할 수 없게 만드는 것을 의미합니다. 스캔된 문서를 다룰 때 데이터가 픽셀 형태로 삽입되어 있기 때문에 기존 텍스트 가리기 도구로는 효과가 없습니다. GroupDocs.Redaction을 사용하면 정확한 픽셀 영역을 지정하고 단색으로 교체하여 정보가 완전히 제거되도록 할 수 있습니다.

## 사전 요구 사항
- **JDK 8 이상**이 설치되어 있음  
- **Maven**(또는 다른 빌드 도구)을 사용한 의존성 관리  
- **IntelliJ IDEA**, **Eclipse**, **NetBeans**와 같은 IDE  
- 기본 Java 지식 및 파일 I/O에 대한 이해  

## Java용 GroupDocs.Redaction 설정

### Maven 설정
GroupDocs 저장소와 의존성을 `pom.xml`에 추가합니다:

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
또는 공식 릴리스 페이지에서 최신 JAR을 다운로드합니다: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### 라이선스 획득
- **Free Trial:** API를 체험하기 위해 트라이얼에 등록하세요.  
- **Temporary License:** 장기 테스트를 위해 임시 키를 사용하세요.  
- **Full Purchase:** 무제한 사용을 위한 프로덕션 라이선스를 구매하세요.

## 구현 가이드

구현을 두 가지 핵심 기능으로 나눕니다: **Image Area Redaction**(실제 마스킹)와 **Redaction Status Check**(성공 여부 확인).

### 스캔된 문서 이미지를 가리는 방법 – 단계 1: Redactor 초기화
먼저, 처리하려는 이미지에 대한 `Redactor` 인스턴스를 생성합니다.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_JPG");
```

### 단계 2: 가리기 매개변수 정의
가리려는 사각형의 좌상단(`Point`)과 크기(`Dimension`)를 지정합니다. 이 예제에서는 파란색 채우기를 사용합니다.

```java
// Define the position on the image where redaction starts.
Point samplePoint = new Point(385, 485);

// Define the size of the area to be redacted.
Dimension sampleSize = new Dimension(1793, 2069);
```

### 단계 3: 가리기 적용
`RegionReplacementOptions`와 함께 `ImageAreaRedaction` 객체를 생성하고 실행합니다. 이 메서드는 작업 성공 여부를 알려주는 `RedactorChangeLog`를 반환합니다.

```java
RedactorChangeLog result = redactor.apply(
    new ImageAreaRedaction(samplePoint, new RegionReplacementOptions(Color.BLUE, sampleSize))
);

// Check if the redaction was successful and save the output.
if (result.getStatus() != RedactionStatus.Failed) {
    redactor.save("YOUR_OUTPUT_DIRECTORY/redacted_output.jpg");
}
```

### 단계 4: 리소스 해제
작업이 끝나면 항상 `Redactor`를 닫아 네이티브 리소스를 해제합니다.

```java
redactor.close();
```

### 가리기 검증 방법 – 상태 확인
가리기를 적용한 후, `RedactorChangeLog`를 검사하여 작업이 실패하지 않았는지 확인할 수 있습니다.

```java
if (result != null && result.getStatus() != RedactionStatus.Failed) {
    System.out.println("Redaction was successful.");
} else {
    System.out.println("Redaction failed.");
}
```

## 실용적인 적용 사례
- **Confidential Document Handling:** 외부 파트와 공유하기 전에 스캔된 계약서에서 개인 데이터를 자동으로 마스킹합니다.  
- **Legal Documentation:** 증거 이미지에서 식별자를 가려 GDPR 또는 HIPAA 준수를 보장합니다.  
- **Medical Records:** 방사선 이미지에서 얼굴이나 손글씨를 가려 환자 프라이버시를 보호합니다.

## 성능 고려 사항
- **Batch Processing:** 메모리 사용량을 낮게 유지하기 위해 이미지를 작은 배치로 로드하고 가립니다.  
- **Efficient Data Structures:** 다수의 이미지를 처리할 때 `Point`와 `Dimension` 객체를 재사용합니다.  
- **Stay Updated:** 성능 향상 및 버그 수정을 위해 최신 GroupDocs.Redaction 버전으로 정기적으로 업그레이드합니다.

## 일반적인 문제 및 해결책

| 문제 | 원인 | 해결 방법 |
|-------|-------|-----|
| **`Failed` 상태로 가리기 실패** | 잘못된 파일 경로 또는 지원되지 않는 이미지 형식 | 이미지가 존재하고 지원되는 형식(JPG, PNG, BMP)인지 확인합니다. |
| **출력 파일이 비어 있음** | `redactor.save()`가 가리기가 완료되기 전에 호출됨 | `apply()`가 성공 상태를 반환한 후에 저장하도록 합니다. |
| **색상이 적용되지 않음** | 투명 색상을 사용함 | 불투명 `Color`를 선택합니다(예: `Color.BLACK` 또는 `Color.BLUE`). |

## 자주 묻는 질문

**Q:** `ImageAreaRedaction`와 텍스트 가리기의 차이점은 무엇인가요?  
A: `ImageAreaRedaction`은 픽셀 좌표에서 작동하고, 텍스트 가리기는 OCR 레이어를 파싱하여 텍스트 내용을 찾아 제거합니다.

**Q:** 단일 이미지에서 여러 영역을 가릴 수 있나요?  
A: Yes—call `redactor.apply()` repeatedly with different `ImageAreaRedaction` objects before saving.

**Q:** GroupDocs.Redaction이 TIFF와 같은 다른 이미지 형식을 지원하나요?  
A: The library supports common raster formats (JPG, PNG, BMP, GIF). For TIFF, convert to a supported format first.

**Q:** 스캔된 PDF 폴더에 대한 가리기를 자동화하려면 어떻게 해야 하나요?  
A: Iterate over each page image extracted from the PDF, apply the same redaction logic, and then rebuild the PDF using a PDF library.

**Q:** 저장하기 전에 가리기를 미리 볼 수 있는 방법이 있나요?  
A: You can render the `Redactor` to a `BufferedImage` and display it in a Swing or JavaFX UI before committing the changes.

## 결론
이제 **이미지를 가리는 방법**과 특히 GroupDocs.Redaction for Java를 사용하여 **스캔된 문서** 이미지를 가리는 방법에 대한 완전하고 프로덕션 준비된 가이드를 갖추었습니다. 위 단계들을 따라 하면 다양한 산업 분야에서 민감한 시각 데이터를 보호할 수 있습니다. 텍스트 가리기나 PDF 페이지 가리기와 같은 추가 API를 탐색하여 조직을 위한 포괄적인 데이터 프라이버시 솔루션을 구축해 보세요.

---

**마지막 업데이트:** 2025-12-29  
**테스트 환경:** GroupDocs.Redaction 24.9 (Java)  
**작성자:** GroupDocs  

**리소스**  
- [문서](https://docs.groupdocs.com/redaction/java/)  
- [API 레퍼런스](https://reference.groupdocs.com/redaction/java)  
- [다운로드](https://releases.groupdocs.com/redaction/java/)  
- [GitHub 저장소](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- [무료 지원 포럼](https://forum.groupdocs.com/c/redaction/33)  
- [임시 라이선스](https://purchase.groupdocs.com/temporary-license/)