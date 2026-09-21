---
date: '2026-09-21'
description: GroupDocs.Redaction for Java를 사용하여 이미지를 마스킹하는 방법을 배웁니다. 단계별 가이드에서는 setup,
  pixel‑level redaction, verification, best practices를 다룹니다.
keywords:
- how to redact image
- Java image redaction
- GroupDocs.Redaction for Java
- scanned image redaction
- pixel redaction Java
lastmod: '2026-09-21'
og_description: GroupDocs.Redaction for Java를 사용하여 이미지를 마스킹하는 방법. 이 가이드를 따라 scanned
  files에서 pixel data를 mask하고, 색상을 선택하며, 결과를 verify하세요—GDPR 및 HIPAA compliance에 최적입니다.
og_image_alt: Guide showing Java code that redacts scanned images using GroupDocs.Redaction
og_title: GroupDocs.Redaction for Java를 사용하여 이미지 마스킹하는 방법
schemas:
- author: GroupDocs
  dateModified: '2026-09-21'
  description: Learn how to redact image with GroupDocs.Redaction for Java. Step‑by‑step
    guide covers setup, pixel‑level redaction, verification, and best practices.
  headline: How to redact image using GroupDocs.Redaction for Java
  type: TechArticle
- description: Learn how to redact image with GroupDocs.Redaction for Java. Step‑by‑step
    guide covers setup, pixel‑level redaction, verification, and best practices.
  name: How to redact image using GroupDocs.Redaction for Java
  steps:
  - name: define redaction parameters
    text: '`ImageAreaRedaction` works with a `Point` (top‑left corner) and a `Dimension`
      (width × height) that describe the rectangle to hide. In this example we use
      a blue fill color.'
  - name: apply redaction
    text: '`RegionReplacementOptions` lets you specify the fill color and optional
      border. Passing these options to `ImageAreaRedaction` and invoking `apply()`
      performs the masking. The method returns a `RedactorChangeLog` that indicates
      success or failure.'
  - name: release resources
    text: '`Redactor` implements `AutoCloseable`. Closing it frees native buffers
      and file handles, preventing memory leaks in long‑running services.'
  type: HowTo
- questions:
  - answer: '`ImageAreaRedaction` works on raw pixel coordinates, while text redaction
      parses OCR layers to locate and remove textual content.'
    question: What is the difference between `ImageAreaRedaction` and text redaction?
  - answer: Yes—call `redactor.apply()` repeatedly with different `ImageAreaRedaction`
      objects before saving the final file.
    question: Can I redact multiple regions in a single image?
  - answer: The library supports common raster formats (JPG, PNG, BMP, GIF). For TIFF,
      convert the image to a supported format first.
    question: Does GroupDocs.Redaction support other image formats like TIFF?
  - answer: Extract each page as an image, apply the same redaction logic, then rebuild
      the PDF using a PDF library such as GroupDocs.Conversion.
    question: How do I automate redaction for a folder of scanned PDFs?
  - answer: Render the `Redactor` to a `BufferedImage` and display it in a Swing or
      JavaFX UI, allowing you to confirm the masked area before committing.
    question: Is there a way to preview the redaction before saving?
  type: FAQPage
tags:
- image redaction
- GroupDocs
- Java
- document privacy
- data protection
title: GroupDocs.Redaction for Java를 사용하여 이미지 마스킹하는 방법
type: docs
url: /ko/java/image-redaction/java-image-redaction-groupdocs-tutorial/
weight: 1
---

# GroupDocs.Redaction for Java를 사용하여 이미지 가리기

이 포괄적인 튜토리얼에서는 GroupDocs.Redaction을 사용하여 Java에서 **이미지를 가리는 방법**을 배웁니다. 스캔된 이미지를 가리는 것은 개인 데이터를 보호하고 GDPR, HIPAA 또는 기타 개인정보 보호 규정을 충족시키며 기밀 시각 정보가 유출되지 않도록 하는 중요한 단계입니다. 프로젝트 설정, 픽셀 수준 가리기 구성, 결과 안전하게 저장, 가리기가 성공했는지 확인하는 과정을 단계별 대화식 스타일로 안내하므로 Java 애플리케이션에 그대로 복사하여 사용할 수 있습니다.

## 빠른 답변
- **Java에서 이미지 가리기를 처리하는 라이브러리는 무엇인가요?** GroupDocs.Redaction for Java.  
- **가리기 색상을 선택할 수 있나요?** 예 – `java.awt.Color`의 불투명 색상이면 `Color.BLUE` 또는 `Color.BLACK`와 같이 사용할 수 있습니다.  
- **프로덕션에 라이선스가 필요합니까?** 예, 상업적 사용을 위해서는 유효한 GroupDocs 라이선스가 필수입니다.  
- **원본 이미지가 덮어쓰기 되나요?** 아니오 – API는 지정한 새 파일에 가려진 이미지를 기록합니다.  
- **지원되는 Java 버전은 무엇인가요?** Java 8 이상 (작성 시점 기준 Java 21까지).

## 이미지 가리기란 무엇이며 왜 스캔된 이미지를 Java에서 가려야 하나요?
이미지 가리기는 픽셀 영역을 단색으로 교체하여 시각 데이터(이름, 번호, 서명 등)를 영구적으로 가립니다. 선택 가능한 문자에 대해 작동하는 텍스트 가리기와 달리, 스캔된 이미지는 원시 픽셀로 정보를 저장하므로 픽셀 기반 도구만이 데이터를 복구할 수 없도록 보장합니다. GroupDocs.Redaction을 사용하면 정확한 좌표를 지정하고 불투명 색상을 적용하여 민감한 내용을 영구적으로 제거한 새 이미지를 만들 수 있습니다.

## 왜 GroupDocs.Redaction for Java를 사용하나요?
GroupDocs.Redaction은 **50개 이상의 이미지 형식**(JPG, PNG, BMP, GIF 포함)을 지원하고 스트리밍 아키텍처 덕분에 전체 파일을 메모리에 로드하지 않고도 수백 페이지 문서를 처리할 수 있습니다. 벤치마크에 따르면 300 KB 스캔 PNG 파일을 일반적인 2.8 GHz CPU에서 120 ms 미만에 가릴 수 있어 배치 작업과 실시간 서비스 모두에 적합합니다.

## 전제 조건
시작하기 전에 다음이 준비되어 있어야 합니다:

- **JDK 8 이상**이 설치되고 `PATH`에 설정되어 있음.  
- **Maven**(또는 Gradle)으로 의존성 관리.  
- **IntelliJ IDEA**, **Eclipse**, **NetBeans** 중 하나의 IDE.  
- Java 파일 I/O와 `java.awt` 패키지에 대한 기본 지식.  

## GroupDocs.Redaction for Java 설정

### Maven 설정
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
또는 공식 릴리스 페이지에서 최신 JAR를 다운로드하세요: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### 라이선스 획득
- **무료 체험:** 전체 API를 체험할 수 있는 트라이얼에 가입하세요.  
- **임시 라이선스:** 비용 없이 확장 테스트를 위한 임시 키를 사용하세요.  
- **정식 구매:** 무제한 배포를 위한 프로덕션 라이선스를 획득하세요.

## 구현 가이드

우리는 구현을 두 가지 핵심 기능으로 나눕니다: **이미지 영역 가리기**(실제 마스킹)와 **가리기 상태 확인**(성공 여부 검증).

### 스캔된 문서 이미지 가리기 – 단계 1: Redactor 초기화
`Redactor`는 이미지를 로드하고 가리기 작업을 제공하는 핵심 클래스입니다.  
처리하려는 원본 이미지 경로를 가리키는 `Redactor` 인스턴스를 생성합니다.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_JPG");
```

### 단계 2: 가리기 매개변수 정의
`ImageAreaRedaction`은 사각형을 정의하기 위해 `Point`(좌상단)와 `Dimension`(너비 × 높이)을 사용합니다. 이 예제에서는 파란색 채우기를 사용합니다.

```java
// Define the position on the image where redaction starts.
Point samplePoint = new Point(385, 485);

// Define the size of the area to be redacted.
Dimension sampleSize = new Dimension(1793, 2069);
```

### 단계 3: 가리기 적용
`RegionReplacementOptions`를 사용해 채우기 색상과 선택적 테두리를 지정합니다. 이 옵션을 `ImageAreaRedaction`에 전달하고 `apply()`를 호출하면 마스킹이 수행됩니다. 메서드는 성공 여부를 나타내는 `RedactorChangeLog`를 반환합니다.

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
`Redactor`는 `AutoCloseable`을 구현합니다. 닫으면 네이티브 버퍼와 파일 핸들이 해제되어 장기 실행 서비스에서 메모리 누수를 방지합니다.

```java
redactor.close();
```

### 가리기 검증 – 상태 확인
가리기를 적용한 후 `RedactorChangeLog`를 검사합니다. `Status.SUCCESS` 값은 픽셀 영역이 오류 없이 교체되었음을 확인합니다. 저장하기 전에 `BufferedImage`로 렌더링해 시각적으로 검증할 수도 있습니다.

```java
if (result != null && result.getStatus() != RedactionStatus.Failed) {
    System.out.println("Redaction was successful.");
} else {
    System.out.println("Redaction failed.");
}
```

## 실용적인 적용 사례
- **기밀 문서 처리:** 파트너와 공유하기 전에 스캔 계약서의 개인 데이터를 마스킹합니다.  
- **법률 문서:** 증거 이미지에서 식별자를 가려 GDPR 또는 HIPAA 준수를 보장합니다.  
- **의료 기록:** 진단 세부 정보를 유지하면서 방사선 스캔에서 환자 얼굴이나 손글씨 메모를 숨깁니다.  

## 성능 고려 사항
- **배치 처리:** 메모리 사용량을 200 MB 이하로 유지하려면 10–20장씩 그룹으로 이미지 처리합니다.  
- **객체 재사용:** 반복 시 `Point`와 `Dimension` 객체를 재사용해 GC 압력을 줄입니다.  
- **버전 업데이트:** 최신 GroupDocs.Redaction 릴리스로 업그레이드하면 버전 24.10에서 보고된 15 % 속도 향상을 얻을 수 있습니다.  

## 일반적인 문제 및 해결책

| 문제 | 원인 | 해결책 |
|-------|-------|-----|
| **`Failed` 상태로 가리기가 실패함** | 잘못된 파일 경로나 지원되지 않는 이미지 형식 | 파일이 존재하고 지원되는 형식(JPG, PNG, BMP, GIF)인지 확인하십시오. |
| **출력 파일이 비어 있음** | `redactor.save()`가 가리기가 완료되기 전에 호출됨 | `apply()`가 `Status.SUCCESS`를 반환한 후에 `save()`를 호출하도록 하세요. |
| **색상이 적용되지 않음** | 투명 `Color` 사용 | `Color.BLACK` 또는 `Color.BLUE`와 같은 불투명 색상을 선택하세요. |

## 자주 묻는 질문

**Q: `ImageAreaRedaction`과 텍스트 가리기의 차이점은 무엇인가요?**  
A: `ImageAreaRedaction`은 원시 픽셀 좌표에서 작동하고, 텍스트 가리기는 OCR 레이어를 파싱해 텍스트 내용을 찾아 제거합니다.

**Q: 하나의 이미지에서 여러 영역을 가릴 수 있나요?**  
A: 예—최종 파일을 저장하기 전에 서로 다른 `ImageAreaRedaction` 객체를 사용해 `redactor.apply()`를 여러 번 호출하면 됩니다.

**Q: GroupDocs.Redaction이 TIFF와 같은 다른 이미지 형식을 지원하나요?**  
A: 라이브러리는 일반적인 래스터 형식(JPG, PNG, BMP, GIF)을 지원합니다. TIFF는 먼저 지원되는 형식으로 변환해야 합니다.

**Q: 스캔된 PDF 폴더에 대한 가리기를 자동화하려면 어떻게 해야 하나요?**  
A: 각 페이지를 이미지로 추출하고 동일한 가리기 로직을 적용한 뒤, GroupDocs.Conversion과 같은 PDF 라이브러리를 사용해 PDF를 재구성합니다.

**Q: 저장하기 전에 가리기를 미리 볼 수 있는 방법이 있나요?**  
A: `Redactor`를 `BufferedImage`로 렌더링하고 Swing 또는 JavaFX UI에 표시하면 저장 전 마스킹 영역을 확인할 수 있습니다.

## 결론
이제 **이미지를 가리는 방법**과 특히 GroupDocs.Redaction for Java를 사용해 **스캔된 이미지를 Java에서 가리는 방법**에 대한 완전하고 프로덕션 준비된 가이드를 확보했습니다. 위 단계들을 따르면 금융, 법률, 의료 분야에서 민감한 시각 데이터를 보호할 수 있습니다. 텍스트 가리기, PDF 페이지 가리기, 폴더 일괄 처리 등 추가 API를 탐색해 조직 전체의 데이터 프라이버시 파이프라인을 구축해 보세요.

**리소스**  
- [문서](https://docs.groupdocs.com/redaction/java/)  
- [API 레퍼런스](https://reference.groupdocs.com/redaction/java)  
- [다운로드](https://releases.groupdocs.com/redaction/java/)  
- [GitHub 저장소](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- [무료 지원 포럼](https://forum.groupdocs.com/c/redaction/33)  
- [임시 라이선스](https://purchase.groupdocs.com/temporary-license/) 

---

**마지막 업데이트:** 2026-09-21  
**테스트 환경:** GroupDocs.Redaction 24.9 (Java)  
**작성자:** GroupDocs

## 관련 튜토리얼

- [Java에서 GroupDocs.Redaction으로 가리기 - 개발자를 위한 포괄적인 가이드](/redaction/java/getting-started/implement-java-redaction-groupdocs-redaction-guide/)
- [OCR와 함께 스캔된 PDF 가리기 – GroupDocs.Redaction Java](/redaction/java/ocr-integration/)
- [Java에서 GroupDocs.Redaction으로 텍스트 가리기 – 가이드](/redaction/java/text-redaction/text-redaction-java-groupdocs-redaction/)