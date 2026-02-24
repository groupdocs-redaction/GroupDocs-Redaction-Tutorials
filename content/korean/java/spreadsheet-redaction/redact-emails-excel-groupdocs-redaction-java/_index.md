---
date: '2026-02-24'
description: GroupDocs.Redaction Java API를 사용하여 Excel 스프레드시트에서 민감한 데이터를 삭제하고 이메일 주소를
  마스킹하는 방법을 배우세요.
keywords:
- Redact Emails in Excel
- GroupDocs.Redaction Java API
- Automate Email Redaction
title: GroupDocs.Redaction Java API를 사용하여 Excel 스프레드시트에서 민감한 데이터 가리기 방법
type: docs
url: /ko/java/spreadsheet-redaction/redact-emails-excel-groupdocs-redaction-java/
weight: 1
---

# Excel 스프레드시트에서 GroupDocs.Redaction Java API를 사용하여 민감한 데이터 가리기

오늘날 데이터 중심의 세상에서 Excel 워크북에서 이메일 주소와 같은 **민감한 데이터 가리기**는 개인 정보를 다루는 모든 사람에게 필수 기술입니다. 클라이언트를 위한 보고서를 준비하든, 파트너와 데이터를 공유하든, 혹은 데이터 세트를 정리하든, 이메일 주소를 마스킹하면 GDPR, CCPA 및 기타 개인정보 보호 규정을 준수하는 데 도움이 됩니다. 이 튜토리얼에서는 GroupDocs.Redaction Java 라이브러리를 사용하여 Excel 파일의 특정 열에서 이메일 값을 자동으로 찾아 교체하는 방법을 배웁니다.

**배우게 될 내용**
- Maven 프로젝트에서 GroupDocs.Redaction for Java을 설정하는 방법.  
- 특정 워크시트와 열을 대상으로 하는 기술.  
- 정규식 패턴을 사용하여 **이메일 주소 마스킹**하는 방법.  
- 원본을 유지하면서 가린 파일을 저장하는 모범 사례.

코드에 들어가기 전에 개발 환경이 준비되었는지 확인해 봅시다.

## 빠른 답변
- **“민감한 데이터 가리기”는 무엇을 의미하나요?** 문서에서 개인 식별 정보(PII)를 영구적으로 제거하거나 마스킹하는 것을 의미합니다.  
- **어떤 라이브러리가 가리기를 처리하나요?** GroupDocs.Redaction for Java.  
- **라이선스가 필요합니까?** 무료 체험판으로 테스트가 가능하며, 프로덕션에서는 정식 라이선스가 필요합니다.  
- **교체 텍스트를 선택할 수 있나요?** 예, “[customer email]”와 같은 임의의 플레이스홀더를 지정할 수 있습니다.  
- **대용량 스프레드시트에서도 이 방법이 안전한가요?** 예, 가이드의 성능 팁을 따르시면 안전합니다.

## 사전 요구 사항

To follow along, you’ll need:

- Java Development Kit (JDK) 8 or higher.  
- Basic Java knowledge and familiarity with Maven.  
- Access to the GroupDocs.Redaction library (downloadable via Maven or direct link).

## GroupDocs.Redaction for Java 설정

GroupDocs.Redaction for Java는 Maven 저장소를 통해 배포되며, 통합이 간단합니다.

**Maven 설정**  
Add the repository and dependency to your `pom.xml` file:

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

**직접 다운로드**  
또는 [GroupDocs.Redaction releases](https://releases.groupdocs.com/redaction/java/)에서 GroupDocs.Redaction for Java 최신 버전을 다운로드할 수 있습니다.

### 라이선스 획득

GroupDocs offers a free trial that lets you evaluate the API. For ongoing projects, you’ll want either a temporary or a full license:

- **Free Trial:** 제한된 기능 평가.  
- **Temporary License:** [GroupDocs’ website](https://purchase.groupdocs.com/temporary-license/)에서 신청.  
- **Full License:** 무제한 프로덕션 사용을 위해 구매.

### 기본 초기화

Start by creating a `Redactor` instance that points to your Excel file:

```java
import com.groupdocs.redaction.Redactor;

public class RedactEmails {
    public static void main(String[] args) {
        // Initialize the redactor with your document path
        try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_XLSX")) {
            // Your redaction logic will go here
        }
    }
}
```

## 구현 가이드

Below is a step‑by‑step walkthrough that shows how to **redact sensitive data** from a specific column.

### 문서 로드

First, open the workbook with the `Redactor` you just created:

```java
import com.groupdocs.redaction.Redactor;

public class RedactEmails {
    public static void main(String[] args) {
        try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_XLSX")) {
            // Proceed to the next steps for redaction
        }
    }
}
```

### 필터 설정

`CellFilter`를 사용하면 가리기 범위를 특정 워크시트와 열로 좁힐 수 있습니다. 이 예제에서는 **Customers** 시트의 B 열(인덱스 1)을 대상으로 합니다:

```java
import com.groupdocs.redaction.redactions.CellFilter;

// Create and configure the filter
CellFilter filter = new CellFilter();
filter.setColumnIndex(1); // Targeting the second column (index starts at 0)
filter.setWorkSheetName("Customers"); // Specify the worksheet name
```

### 이메일 패턴 정의

정규식을 사용하여 이메일 주소를 감지합니다. 아래 패턴은 대부분의 일반적인 이메일 형식에 매치됩니다:

```java
import java.util.regex.Pattern;

// Define regex pattern for matching emails
Pattern expression = Pattern.compile("^\\w+([-+.']\\w+)*@\\w+([-.]\\w+)*\\.\\w+([-.]\\w+)*$");
```

### 가리기 적용

Now combine the filter, pattern, and a replacement option to **mask email addresses**. The `ReplacementOptions` object lets you define the placeholder text that will appear in the redacted cells.

```java
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.RedactorChangeLog;
import com.groupdocs.redaction.redactions.CellColumnRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

// Apply redaction
RedactorChangeLog result = redactor.apply(new CellColumnRedaction(filter, expression, new ReplacementOptions("[customer email]")));

// Save changes if successful
if (result.getStatus() != RedactionStatus.Failed) {
    SaveOptions saveOptions = new SaveOptions();
    saveOptions.setAddSuffix(true); // Add a suffix to the saved file name
    redactor.save(saveOptions);
}
```

### 문제 해결 팁

- **Regex 정확도:** 다양한 이메일 샘플에 정규식을 테스트하여 기대하는 모든 형식을 포착하는지 확인하세요.  
- **열 인덱스:** 열 인덱스는 0부터 시작한다는 점을 기억하고, 가리려는 열의 인덱스를 다시 확인하세요.  
- **워크시트 이름:** 이름은 대소문자를 구분하므로 Excel에 표시된 정확한 시트 이름을 사용하세요.

## 왜 민감한 데이터를 가려야 할까요?

- **컴플라이언스:** GDPR, CCPA 및 산업별 개인정보 보호 규정을 충족합니다.  
- **위험 감소:** 파일을 외부에 공유할 때 개인 식별자가 우연히 노출되는 것을 방지합니다.  
- **데이터 거버넌스:** 보관된 데이터 세트에서 PII를 영구적으로 제거하여 깔끔한 감사 기록을 유지합니다.

## 실용적인 적용 사례

1. **데이터 프라이버시 컴플라이언스:** 파트너에게 스프레드시트를 보내기 전에 이메일 주소를 자동으로 제거합니다.  
2. **내부 감사:** 내부 검토 중에 고객 데이터를 익명화합니다.  
3. **보고 파이프라인:** 정기 보고서 생성 작업에 가리기 단계를 통합합니다.

## 성능 고려 사항

- **배치 처리:** 많은 파일을 가려야 할 경우 순차적으로 처리하고 가능한 경우 `Redactor` 인스턴스를 재사용합니다.  
- **메모리 관리:** `Redactor`를 try‑with‑resources 블록으로 닫아(예시와 같이) 네이티브 리소스를 즉시 해제합니다.  
- **대용량 데이터 세트:** 수천 행이 있는 워크북의 경우 가리기 전에 행을 필터링하여 오버헤드를 줄이는 것을 고려하세요.

## 자주 묻는 질문

**Q: 이메일 정규식이 모든 형식에 매치되지 않으면 어떻게 하나요?**  
A: 패턴에 추가 문자를 포함하거나 더 관대한 표현식을 사용하도록 조정한 뒤 가리기를 다시 실행합니다.

**Q: 여러 열을 한 번에 가릴 수 있나요?**  
A: 예. 각 열에 대해 별도의 `CellFilter`를 만들고 각 필터에 대해 `redactor.apply`를 호출합니다.

**Q: GroupDocs.Redaction이 매우 큰 Excel 파일에 적합한가요?**  
A: 잘 확장됩니다. 특히 시트를 하나씩 처리하고 각 파일 후에 리소스를 해제할 때 효과적입니다.

**Q: 가리기 중 오류를 어떻게 처리하나요?**  
A: `RedactorChangeLog` 상태를 확인합니다; 실패하지 않은 상태는 작업이 성공했음을 의미합니다. 디버깅을 위해 실패를 로그에 기록하세요.

**Q: 교체 텍스트를 맞춤 설정할 수 있나요?**  
A: 물론입니다. `[redacted]`와 같은 문자열이나 생성된 토큰을 `ReplacementOptions`에 전달하면 됩니다.

## 리소스

- [문서](https://docs.groupdocs.com/redaction/java/)  
- [API 레퍼런스](https://reference.groupdocs.com/redaction/java)  
- [GroupDocs.Redaction 다운로드](https://releases.groupdocs.com/redaction/java/)  
- [GitHub 저장소](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- [무료 지원 포럼](https://forum.groupdocs.com/c/redaction/33)  
- [임시 라이선스 정보](https://purchase.groupdocs.com/temporary-license/)

---

**마지막 업데이트:** 2026-02-24  
**테스트 대상:** GroupDocs.Redaction 24.9 for Java  
**작성자:** GroupDocs