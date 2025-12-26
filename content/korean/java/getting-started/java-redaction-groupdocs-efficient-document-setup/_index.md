---
date: '2025-12-26'
description: GroupDocs.Redaction을 사용하여 Java에서 출력 폴더를 생성하고 문서 레드랙션을 적용하는 방법을 배웁니다.
  단계별 설정, 코드 예제 및 모범 사례.
keywords:
- Java Redaction
- GroupDocs.Redaction Setup
- Document Redaction
title: 'GroupDocs.Redaction용 Java 가이드: 출력 폴더 만들기'
type: docs
url: /ko/java/getting-started/java-redaction-groupdocs-efficient-document-setup/
weight: 1
---

# GroupDocs.Redaction용 Java 출력 폴더 생성 가이드

오늘날 디지털 시대에 문서 내부의 민감한 정보를 보호하는 것은 최우선 과제입니다. 이 튜토리얼에서는 **출력 폴더를 Java에서 생성하는 방법**을 보여주고, 이후 GroupDocs.Redaction을 사용해 기밀 데이터를 빠르고 안정적으로 숨기는 방법을 안내합니다. 환경 설정, 폴더 생성, 레드액션 구현, 성능 팁을 단계별로 살펴보며 개인, 금융, 비즈니스 기록을 자신 있게 보호할 수 있습니다.

## 빠른 답변
- **첫 번째 단계는 무엇인가요?** Java에서 출력 폴더를 생성하고 GroupDocs.Redaction 라이브러리를 추가합니다.  
- **필요한 라이브러리 버전은?** GroupDocs.Redaction 24.9 이상.  
- **라이선스가 필요한가요?** 테스트용 무료 체험판으로 충분하지만, 운영 환경에서는 유료 라이선스가 필요합니다.  
- **원본 문서 형식을 유지할 수 있나요?** 예—저장 시 rasterization을 비활성화하면 됩니다.  
- **대용량 파일에도 적합한가요?** 메모리 튜닝을 적절히 하면 가능합니다.

## “create output folder java”란?
Java에서 출력 폴더를 생성한다는 것은 디렉터리 존재 여부를 프로그래밍적으로 확인하고, 없을 경우 생성하여 처리된 파일을 저장할 전용 위치를 마련하는 것을 의미합니다. 이 단계는 레드액션된 문서를 원본과 분리하고 프로젝트를 체계적으로 관리하는 데 도움이 됩니다.

## GroupDocs.Redaction와 함께 출력 폴더를 생성해야 하는 이유
- **관심사의 분리:** 원본 파일과 레드액션 파일을 명확히 구분합니다.  
- **확장성:** 여러 문서를 한 곳에 배치해 배치 처리에 용이합니다.  
- **규정 준수:** 정제된 버전만 저장함으로써 감사 추적을 간소화합니다.  
- **성능:** 파일 시스템 혼잡을 줄여 I/O 속도를 향상시킬 수 있습니다.

## 사전 요구 사항
시작하기 전에 다음 항목을 준비하세요:

- **GroupDocs.Redaction Library** – 버전 24.9 이상.  
- **Java Development Kit (JDK)** – 버전 8 이상.  
- IntelliJ IDEA 또는 Eclipse와 같은 Java IDE.  
- 의존성 관리를 위한 Maven 설치.  
- 파일 처리에 익숙한 기본 Java 지식.

## Java용 GroupDocs.Redaction 설정
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

수동으로 다운로드하려면 공식 릴리스 페이지에서 최신 JAR를 받으세요: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### 라이선스 획득 단계
먼저 무료 체험판으로 API를 살펴보고, 운영 환경이 준비되면 GroupDocs 포털에서 임시 또는 정식 라이선스를 발급받으세요.

## 구현 가이드

### 출력 폴더 생성 방법
출력 위치를 정리하는 것은 깔끔한 레드액션 워크플로우의 기본입니다. 아래 예제에서는 사용자가 정의한 기본 디렉터리 안에 `HelloWorld`라는 폴더를 생성합니다.

#### 문서 디렉터리 설정
다음 코드 스니펫은 폴더 존재 여부를 확인하고, 없으면 생성합니다. 또한 레드액션 문서의 경로를 준비합니다.

```java
import java.io.File;

public class DocumentDirectorySetup {
    public static void main(String[] args) throws Exception {
        // Define the path to your document directory and create it if it doesn't exist
        File outputFolder = new File("YOUR_DOCUMENT_DIRECTORY/HelloWorld");
        if (!outputFolder.exists()) {
            outputFolder.mkdirs();
        }
        File outputFile = new File(outputFolder, "redacted_document.docx");
    }
}
```

- **중요 이유:** 프로그램matically 폴더를 생성함으로써 레드액션 단계가 항상 유효한 대상 경로를 갖게 되어 `FileNotFoundException` 오류를 방지합니다.

### 레드액션 적용
출력 폴더가 준비되었으니 이제 원본 파일을 로드하고 레드액션을 적용한 뒤, 방금 만든 폴더에 결과를 저장합니다.

#### 레드액션 코드
```java
import com.groupdocs.redaction.Redactor;
import java.io.FileOutputStream;

public class RedactionApplication {
    public static void main(String[] args) throws Exception {
        // Initialize the redactor with a sample document path
        final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample_document.docx");
        
        try {
            // Apply an exact phrase redaction to replace "John Doe" with a red color
            RedactorChangeLog result = redactor.apply(new ExactPhraseRedaction(
                "John Doe", 
                new ReplacementOptions(java.awt.Color.RED)
            ));
            
            // Save the document to the specified output file path
            final FileOutputStream stream = new FileOutputStream("YOUR_OUTPUT_DIRECTORY/redacted_document.docx");
            try {
                // Disable rasterization options for saving in original format
                RasterizationOptions rasterOptions = new RasterizationOptions();
                rasterOptions.setEnabled(false);
                redactor.save(stream, rasterOptions);
            } finally {
                stream.close();
            }
        } finally {
            redactor.close();
        }
    }
}
```

- **설명:** `Redactor`가 `sample_document.docx`를 로드하고, 정확히 “John Doe”라는 구문을 찾아 빨간 오버레이로 교체한 뒤, 앞서 만든 폴더에 결과를 씁니다. rasterization을 비활성화하면 원본 DOCX 레이아웃이 유지됩니다.

#### 문제 해결 팁
- **경로 오류:** `YOUR_DOCUMENT_DIRECTORY`와 `YOUR_OUTPUT_DIRECTORY`가 실제 존재하는 위치를 가리키는지 다시 확인하세요.  
- **버전 충돌:** Maven 의존성이 다운로드한 라이브러리 버전과 일치하는지 확인하세요.  
- **라이선스 오류:** 라이선스가 없거나 유효하지 않으면 런타임 시 예외가 발생합니다.

## 실무 적용 사례
**출력 폴더를 Java에서 생성하고 GroupDocs.Redaction을 사용하는** 실제 시나리오는 다음과 같습니다:

1. **규정 관리:** 계약서에서 개인 정보를 자동으로 삭제하고 보관합니다.  
2. **재무 보고:** 외부 감사인에게 공유되는 분기 보고서에서 계좌 번호를 숨깁니다.  
3. **의료 기록:** HIPAA 요구사항을 충족하기 위해 의료 문서에서 환자 식별자를 제거합니다.

## 성능 고려 사항
- **메모리 관리:** 매우 큰 DOCX 또는 PDF 파일은 전체를 메모리에 로드하지 않도록 스트리밍 API를 활용합니다.  
- **배치 처리:** 파일 목록을 순회하면서 가능한 경우 동일 `Redactor` 인스턴스를 재사용합니다.  
- **JVM 튜닝:** 50 MB 이상 파일을 자주 처리한다면 힙 크기를 (`-Xmx2g`) 늘립니다.

## 결론
이제 **Java에서 출력 폴더를 생성하고** GroupDocs.Redaction을 통합해 원본 형식을 유지하면서 정밀한 레드액션을 적용하는 방법을 알게 되었습니다. 이 워크플로우는 규정 준수를 돕고 민감 데이터를 효율적으로 보호합니다.

자세한 내용은 공식 문서를 참고하세요: [GroupDocs documentation](https://docs.groupdocs.com/redaction/java/).

## FAQ 섹션
1. **GroupDocs.Redaction을 어떻게 시작하나요?**  
   위에 표시된 Maven 의존성을 추가하고, 출력 폴더를 만든 뒤 예시와 같이 `Redactor`를 인스턴스화하면 됩니다.  

2. **대용량 문서를 효율적으로 처리할 수 있나요?**  
   네—메모리를 적절히 관리하고 rasterization을 비활성화하면 큰 파일도 과도한 오버헤드 없이 처리할 수 있습니다.  

3. **운영 환경에서 라이선스가 필수인가요?**  
   평가용 무료 체험판은 충분하지만, 상업적 배포에는 유료 라이선스가 필요합니다.  

4. **지원되는 파일 형식은 무엇인가요?**  
   GroupDocs.Redaction은 DOCX, PDF, PPTX, XLSX 및 여러 이미지 형식을 지원합니다.  

5. **여러 파일에 대한 레드액션을 자동화하려면?**  
   디렉터리 내 파일을 순회하는 루프에 레드액션 로직을 넣고, 동일한 출력 폴더 패턴을 재사용하면 됩니다.

---

**마지막 업데이트:** 2025-12-26  
**테스트 환경:** GroupDocs.Redaction 24.9  
**작성자:** GroupDocs