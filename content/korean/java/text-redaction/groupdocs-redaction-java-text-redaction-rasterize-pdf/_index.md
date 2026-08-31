---
date: '2026-02-24'
description: GroupDocs.Redaction for Java를 사용하여 텍스트를 가리고, 보안이 강화된 편집 불가능한 문서를 위해 래스터화된
  PDF로 저장하는 방법을 배워보세요.
keywords:
- text redaction Java
- save as rasterized PDF
- GroupDocs.Redaction Java
title: GroupDocs.Java를 사용하여 텍스트를 가리고 래스터화된 PDF를 저장하는 방법
type: docs
url: /ko/java/text-redaction/groupdocs-redaction-java-text-redaction-rasterize-pdf/
weight: 1
---

# 텍스트 삭제 및 래스터화된 PDF 저장 방법 (GroupDocs.Redaction Java 사용)

문서에서 민감한 정보를 보호하는 것은 필수적입니다. 개인 이름을 삭제하거나 파일의 보안 버전을 준비해야 할 경우, GroupDocs.Redaction for Java가 이러한 작업을 간소화합니다. **텍스트 삭제**를 빠르게 수행하고 **래스터화된 PDF로 저장**하는 것은 규정 준수 중심 애플리케이션에서 흔히 요구되는 작업이며, 이 가이드에서는 정확한 방법을 보여줍니다.

## 빠른 답변
- **“텍스트 삭제”는 무엇을 의미하나요?** 민감한 문자열을 교체하거나 제거하여 읽히거나 복구될 수 없게 합니다.  
- **어떤 라이브러리가 작업을 처리하나요?** GroupDocs.Redaction for Java가 내장된 삭제 및 래스터화 기능을 제공합니다.  
- **라이선스가 필요하나요?** 무료 체험판으로 테스트가 가능하며, 프로덕션에서는 정식 라이선스가 필요합니다.  
- **DOCX를 한 번에 래스터화된 PDF로 변환할 수 있나요?** 예 – 먼저 삭제를 적용한 뒤 `SaveOptions`에 래스터화 옵션을 활성화합니다.  
- **출력이 정말 편집 불가능한가요?** 래스터화된 PDF는 이미지로 렌더링되어 텍스트 추출이나 수정이 불가능합니다.

## 텍스트 삭제란?
텍스트 삭제는 개인 식별자, 재무 데이터, 기밀 조항 등 민감한 정보를 문서에서 영구적으로 제거하거나 가리는 과정입니다. 단순한 찾기‑바꾸기와 달리, 삭제는 숨겨진 내용이 복구될 수 없도록 보장합니다.

## 왜 GroupDocs.Redaction for Java를 사용하나요?
- **내장된 삭제 유형** (정확 구문, 정규식, 이미지 등)  
- **원클릭 래스터화**로 보안 PDF 생성  
- **다중 포맷 지원** (DOCX, PPTX, XLSX, PDF 등)  
- **개발자 친화적인 API**가 기존 Java 프로젝트와 통합 가능

## 사전 요구 사항
시작하기 전에 다음을 확인하세요:

1. **Java Development Kit (JDK 11 이상)** 및 IntelliJ IDEA 또는 Eclipse와 같은 IDE.  
2. **GroupDocs.Redaction 라이브러리** (버전 24.9 이상).  
3. **기본 Java 지식** – 몇 개의 짧은 코드 조각을 작성하게 됩니다.  

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
Maven이 익숙하지 않다면, 공식 릴리스 페이지에서 JAR 파일을 다운로드할 수 있습니다: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

#### 라이선스 획득
- **Free Trial** – 비용 없이 API를 탐색합니다.  
- **Temporary License** – 장기 테스트에 이상적입니다.  
- **Full License** – 프로덕션 배포에 필요합니다.

### 기본 초기화
`Redactor` 클래스로 문서를 엽니다:

```java
import com.groupdocs.redaction.Redactor;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

## 구현 가이드

### Java에서 텍스트 삭제 방법
아래에서는 정확 구문 삭제를 단계별로 설명합니다. 이는 사람 이름과 같이 알려진 식별자를 제거하는 데 적합합니다.

#### 단계 1: 필요한 클래스 가져오기
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;
```

#### 단계 2: 정확 구문 삭제 적용
다음 스니펫은 **“John Doe”** 모든 발생을 자리표시자 **[personal]** 로 교체합니다:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
try {
    redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]"));
} finally { 
    redactor.close(); 
}
```

**왜 이렇게 동작하나요:**  
- `ExactPhraseRedaction`은 문자열 “John Doe”를 그대로 대상으로 합니다.  
- `ReplacementOptions`는 원본 텍스트 대신 삽입할 내용을 엔진에 알려줍니다.

**팁 및 일반적인 함정**  
- 문서 경로를 다시 확인하세요; 잘못된 경로는 `FileNotFoundException`을 발생시킵니다.  
- Java 프로세스가 출력 폴더에 대한 쓰기 권한을 가지고 있는지 확인하세요.

### 래스터화된 PDF로 저장하는 방법
삭제 후에는 편집이 불가능한 PDF가 필요할 가능성이 높습니다. 래스터화는 각 페이지를 이미지로 변환하여 텍스트 선택이나 편집을 차단합니다.

#### 단계 1: `SaveOptions` 가져오기
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
```

#### 단계 2: 래스터화된 PDF 구성 및 저장
```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
try {
    SaveOptions tmp0 = new SaveOptions();
    tmp0.setAddSuffix(false);
    tmp0.setRasterizeToPDF(true);

    redactor.save(tmp0);
} finally { 
    redactor.close(); 
}
```

**Explanation:**  
- `setAddSuffix(false)`는 원본 파일 이름을 유지합니다(“_redacted”를 추가하려면 true로 설정).  
- `setRasterizeToPDF(true)`는 GroupDocs에게 PDF 내부에 각 페이지를 이미지로 렌더링하도록 지시하여 문서가 **편집 불가능**하도록 보장합니다.

**문제 해결**  
- 래스터화가 실패하면 Java 런타임에 PDF 렌더링 종속성이 포함되어 있는지 확인하세요(라이브러리에 번들되어 있습니다).  

## 실용적인 적용 사례
1. **Legal Document Processing** – 상대 변호사와 공유하기 전에 고객 이름을 삭제합니다.  
2. **HR Record Management** – 내부 보고서에서 직원 ID를 숨깁니다.  
3. **Financial Reporting** – 감사 요약을 배포할 때 계좌 번호를 보호합니다.  

이 단계들을 자동화 워크플로우에 연결하여 GroupDocs.Redaction을 문서 관리 시스템이나 클라우드 스토리지 버킷과 연동할 수 있습니다.

## 성능 고려 사항
- **Batch Processing:** 많은 파일을 처리할 때 단일 `Redactor` 인스턴스를 재사용하여 오버헤드를 줄입니다.  
- **Memory Management:** 대용량 문서의 경우 `redactor.close()` 후 `System.gc()`를 호출하거나 별도 JVM에서 실행합니다.  
- **Keep Dependencies Updated:** 최신 릴리스에는 PDF 래스터화에 대한 성능 개선이 포함되는 경우가 많습니다.

## 일반적인 문제 및 해결책
| Issue | Solution |
|-------|----------|
| *File not found* | 절대 경로를 확인하고 서버에 파일이 존재하는지 확인하세요. |
| *Permission denied* | 충분한 OS 권한으로 JVM을 실행하거나 출력 폴더의 ACL을 변경하세요. |
| *Rasterization produces blank pages* | 원본 문서가 이미 래스터 이미지인지 확인하고 최신 라이브러리 버전을 사용하세요. |
| *Redaction leaves hidden text* | `ExactPhraseRedaction`과 `ReplacementOptions`를 사용하고 단순 찾기‑바꾸기 방법은 피하세요. |

## 자주 묻는 질문

**Q: 정확 구문 삭제란 무엇인가요?**  
A: 특정 문자열(예: 이름)을 자리표시자로 교체하여 원본 텍스트가 복구될 수 없게 합니다.

**Q: PDF를 래스터화하면 보안이 어떻게 향상되나요?**  
A: 래스터화된 PDF는 각 페이지를 이미지로 렌더링하므로 텍스트 선택, 복사 또는 편집이 불가능합니다.

**Q: 한 번에 여러 파일을 처리할 수 있나요?**  
A: 예—파일 경로 목록을 순회하면서 동일한 `Redactor` 구성을 재사용하면 됩니다.

**Q: 클라우드 연동이 가능한가요?**  
A: 물론입니다. AWS S3, Azure Blob, Google Cloud Storage 등에서 스트림을 읽고 쓰며 API에 직접 전달할 수 있습니다.

**Q: 초보자가 흔히 겪는 함정은 무엇인가요?**  
A: `Redactor`를 닫지 않아 파일이 잠기게 되는 경우와, 래스터화 지원이 없는 구버전 라이브러리를 사용하는 경우가 있습니다.

## 리소스

- **Documentation**: [GroupDocs Redaction Java Documentation](https://docs.groupdocs.com/redaction/java/)  
- **API Reference**: [GroupDocs Redaction API Reference](https://reference.groupdocs.com/redaction/java)  
- **Download**: [Latest Releases](https://releases.groupdocs.com/redaction/java/)  
- **GitHub**: [GroupDocs.Redaction GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **Free Support**: [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)  
- **Temporary License**: [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license/) 

---

**Last Updated:** 2026-02-24  
**Tested With:** GroupDocs.Redaction 24.9 for Java  
**Author:** GroupDocs