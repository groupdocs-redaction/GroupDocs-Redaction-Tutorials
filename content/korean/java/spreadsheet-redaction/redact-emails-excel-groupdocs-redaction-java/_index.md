---
date: '2026-08-09'
description: GroupDocs.Redaction Java API를 사용하여 Excel 스프레드시트에서 개인 데이터를 숨기고 이메일 주소를
  마스킹하는 방법을 배웁니다.
keywords:
- how to hide personal data
- mask email addresses excel
- GroupDocs.Redaction Java
- Excel redaction tutorial
lastmod: '2026-08-09'
og_description: GroupDocs.Redaction Java API를 사용하여 Excel 파일에서 개인 데이터를 숨기고 이메일 주소를
  마스킹하는 단계별 방법을 확인하세요 – GDPR 준수를 위한 빠르고 안전한 솔루션입니다.
og_image_alt: Guide showing Java code that redacts email addresses in an Excel spreadsheet
og_title: GroupDocs Java를 사용하여 Excel에서 개인 데이터를 숨기는 방법
schemas:
- author: GroupDocs
  dateModified: '2026-08-09'
  description: Learn how to hide personal data and mask email addresses in Excel spreadsheets
    using the GroupDocs.Redaction Java API.
  headline: How to hide personal data in Excel with GroupDocs Java
  type: TechArticle
- description: Learn how to hide personal data and mask email addresses in Excel spreadsheets
    using the GroupDocs.Redaction Java API.
  name: How to hide personal data in Excel with GroupDocs Java
  steps:
  - name: '**Partner data exchange** – Automatically strip customer emails before
      sending spreadsheets to vendors.'
    text: '**Partner data exchange** – Automatically strip customer emails before
      sending spreadsheets to vendors.'
  - name: '**Internal audit preparation** – Anonymize employee data during compliance
      reviews.'
    text: '**Internal audit preparation** – Anonymize employee data during compliance
      reviews.'
  - name: '**Scheduled reporting** – Embed the redaction step into nightly batch jobs
      that generate distribution‑ready reports.'
    text: '**Scheduled reporting** – Embed the redaction step into nightly batch jobs
      that generate distribution‑ready reports.'
  type: HowTo
- questions:
  - answer: Extend the pattern to include additional allowed characters (e.g., “+”
      or “_”) and test against a larger sample set, then re‑run the redaction.
    question: My regex still misses some corporate email formats. What should I do?
  - answer: Yes. Create a separate `CellFilter` for each column and invoke `redactor.apply`
      for each filter sequentially.
    question: Can I redact more than one column in a single pass?
  - answer: The library processes sheets incrementally, so files up to several gigabytes
      can be redacted as long as you enable streaming and close the `Redactor` after
      each file.
    question: Is GroupDocs.Redaction able to handle Excel files larger than 1 GB?
  - answer: Inspect the `RedactorChangeLog` returned by `apply`; a non‑failed status
      indicates success, while any errors are listed with line numbers and cell references.
    question: How do I capture redaction results or errors?
  - answer: Absolutely. Build the placeholder string dynamically (e.g., `"[redacted:"
      + UUID.randomUUID() + "]"`) and pass it to `ReplacementOptions`.
    question: Can I use a custom placeholder that includes a unique token per row?
  type: FAQPage
tags:
- hide personal data
- GroupDocs.Redaction
- Java Excel processing
- data privacy
title: GroupDocs Java를 사용하여 Excel에서 개인 데이터를 숨기는 방법
url: /ko/java/spreadsheet-redaction/redact-emails-excel-groupdocs-redaction-java/
weight: 1
---

# Excel에서 개인 데이터를 숨기는 방법 (GroupDocs Java)

이 가이드에서는 GroupDocs.Redaction Java API를 사용하여 Excel 워크북에서 **개인 데이터를 숨기는 방법**—특히 이메일 주소—을 배우게 됩니다. GDPR, CCPA 또는 내부 프라이버시 정책을 준수해야 할 경우, 여기서 보여주는 접근 방식으로 리다크션을 안전하게 자동화하고 원본 파일은 그대로 두며 배포 준비가 된 깨끗한 버전을 생성할 수 있습니다.

## 빠른 답변
- **“개인 데이터 숨기기”는 무엇을 의미합니까?** 파일에서 개인 식별 정보(PII)를 영구적으로 마스킹하거나 제거하여 더 이상 읽을 수 없게 만드는 것을 의미합니다.  
- **어떤 라이브러리가 리다크션을 수행합니까?** Java용 GroupDocs.Redaction.  
- **예제를 실행하려면 라이선스가 필요합니까?** 테스트용으로는 무료 체험판으로 충분하지만, 상업적 사용을 위해서는 프로덕션 등급 라이선스가 필요합니다.  
- **플레이스홀더 텍스트를 사용자 정의할 수 있나요?** 예, 이메일을 “[redacted email]”와 같은 문자열로 교체할 수 있습니다.  
- **이 방법이 대형 스프레드시트에 적합한가요?** 예, “성능 고려 사항” 섹션의 팁을 따르면 가능합니다.

## 개인 데이터 숨기기란?
**개인 데이터 숨기기**는 이름, 전화번호, 이메일 주소 등 개인을 직접 또는 간접적으로 식별할 수 있는 정보를 영구적으로 제거하거나 마스킹하는 것을 의미합니다. 이 과정은 결과 파일이 대상자를 재식별하는 데 사용될 수 없도록 보장합니다.

## Java용 GroupDocs.Redaction을 사용하는 이유
GroupDocs.Redaction은 **30개 이상의 입력 및 출력 형식**을 지원하며 **최대 500,000행**까지의 워크북을 전체 파일을 메모리에 로드하지 않고 처리할 수 있어, 순수 파일 파싱 솔루션에 비해 **메모리 사용량을 최대 80 %**까지 줄여줍니다. 이러한 정량적 이점은 엔터프라이즈급 데이터 프라이버시 파이프라인에 최적의 선택이 됩니다.

## 사전 요구 사항
- Java Development Kit (JDK) 8 이상.  
- Maven 빌드 파일에 대한 기본적인 이해.  
- GroupDocs.Redaction Java 라이브러리에 대한 접근 (Maven 또는 공식 릴리스 페이지에서 다운로드 가능).

## Java용 GroupDocs.Redaction 설정

### Maven 프로젝트에 GroupDocs.Redaction을 추가하려면 어떻게 하나요?
Add the GroupDocs repository and the Redaction dependency to your `pom.xml` file (see [GroupDocs.Redaction releases](https://releases.groupdocs.com/redaction/java/)). Then run `mvn clean install` to pull the artifacts.

```text
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
```

### GroupDocs.Redaction 라이선스를 어떻게 얻나요?
GroupDocs offers three licensing options (see [GroupDocs’ website](https://purchase.groupdocs.com/temporary-license/)):

- **무료 체험** – 제한된 기능 평가, 신용카드 필요 없음.  
- **임시 라이선스** – GroupDocs 웹사이트에서 얻는 30일 평가 키.  
- **정식 라이선스** – 판매 포털을 통해 구매하는 영구적인 프로덕션 라이선스.

```text
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
```

## 구현 가이드

### Excel 파일에 대한 Redactor 인스턴스를 생성하려면 어떻게 하나요?
The `Redactor` class is the main entry point that loads a document and provides redaction operations.  
Instantiate a `Redactor` object pointing at the source workbook. The `Redactor` class is the entry point for all redaction operations; it loads the file into a managed memory structure while keeping the original file on disk.

```text
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
```

### 리다크션을 단일 워크시트와 열로 제한하려면 어떻게 하나요?
The `CellFilter` class lets you specify which worksheet and column(s) should be examined for redaction. Use a `CellFilter` to specify the target sheet name and column index. The `CellFilter` class filters cells before the redaction engine evaluates them, ensuring only the intended cells are processed.

```text
```java
import com.groupdocs.redaction.redactions.CellFilter;

// Create and configure the filter
CellFilter filter = new CellFilter();
filter.setColumnIndex(1); // Targeting the second column (index starts at 0)
filter.setWorkSheetName("Customers"); // Specify the worksheet name
```
```

### 대부분의 이메일 주소와 일치하는 정규식 패턴을 정의하려면 어떻게 하나요?
The `Pattern` class from `java.util.regex` represents a compiled regular‑expression used to match text. Create a `Pattern` object with a regex that captures typical email formats. The pattern below matches the majority of RFC‑5322‑compliant addresses while ignoring malformed strings.

```text
```java
import java.util.regex.Pattern;

// Define regex pattern for matching emails
Pattern expression = Pattern.compile("^\\w+([-+.']\\w+)*@\\w+([-.]\\w+)*\\.\\w+([-.]\\w+)*$");
```
```

### 리다크션을 적용하고 이메일을 플레이스홀더로 교체하려면 어떻게 하나요?
The `ReplacementOptions` class defines how matched content will be replaced, such as the placeholder text. Combine the filter, pattern, and a `ReplacementOptions` instance. The `ReplacementOptions` class lets you set the exact placeholder text that will appear in each redacted cell.

```text
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
```

## 일반적인 함정 및 문제 해결
- **Regex does not catch all cases** – Test the expression against a representative sample of your data and adjust character classes as needed.  
- **Incorrect column index** – Remember that column indexing starts at 0; column B is index 1.  
- **Worksheet name case‑sensitivity** – Use the exact sheet name as shown in Excel; “Customers” ≠ “customers”.  
- **Resource leaks** – Wrap the `Redactor` in a try‑with‑resources block (as shown) to ensure native resources are released promptly.

## Excel에서 개인 데이터를 숨기는 이유
Excel에서 개인 데이터를 숨기면 모든 개인 식별 정보를 제거하여 파일이 개인을 추적하는 데 사용될 수 없게 됩니다. 이는 프라이버시를 보호하고 규제 요구 사항을 충족하며 외부 파트너와 스프레드시트를 공유하거나 데이터를 공개할 때 우발적인 유출을 방지합니다.

- **Regulatory compliance** – Satisfy GDPR, CCPA, and industry‑specific privacy mandates.  
- **Risk mitigation** – Prevent accidental exposure of PII when sharing files with external partners.  
- **Audit readiness** – Keep a clean, immutable audit trail by permanently removing sensitive values from archived datasets.

## 실용적인 적용 사례
1. **Partner data exchange** – Automatically strip customer emails before sending spreadsheets to vendors.  
2. **Internal audit preparation** – Anonymize employee data during compliance reviews.  
3. **Scheduled reporting** – Embed the redaction step into nightly batch jobs that generate distribution‑ready reports.

## 성능 고려 사항
- **Batch processing** – Reuse a single `Redactor` instance across multiple files to reduce JVM overhead.  
- **Memory management** – The API processes worksheets one at a time; for workbooks exceeding 100 MB, process rows in chunks to keep heap usage low.  
- **Large datasets** – When handling files with >100 k rows, enable streaming mode (available in version 24.9) to keep memory consumption under 200 MB.

## 자주 묻는 질문
**Q: My regex still misses some corporate email formats. What should I do?**  
A: Extend the pattern to include additional allowed characters (e.g., “+” or “_”) and test against a larger sample set, then re‑run the redaction.

**Q: Can I redact more than one column in a single pass?**  
A: Yes. Create a separate `CellFilter` for each column and invoke `redactor.apply` for each filter sequentially.

**Q: Is GroupDocs.Redaction able to handle Excel files larger than 1 GB?**  
A: The library processes sheets incrementally, so files up to several gigabytes can be redacted as long as you enable streaming and close the `Redactor` after each file.

**Q: How do I capture redaction results or errors?**  
A: Inspect the `RedactorChangeLog` returned by `apply`; a non‑failed status indicates success, while any errors are listed with line numbers and cell references.

**Q: Can I use a custom placeholder that includes a unique token per row?**  
A: Absolutely. Build the placeholder string dynamically (e.g., `"[redacted:" + UUID.randomUUID() + "]"`) and pass it to `ReplacementOptions`.

## 추가 리소스
- [문서](https://docs.groupdocs.com/redaction/java/)
- [API 레퍼런스](https://reference.groupdocs.com/redaction/java)
- [GroupDocs.Redaction 다운로드](https://releases.groupdocs.com/redaction/java/)
- [GitHub 저장소](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
- [무료 지원 포럼](https://forum.groupdocs.com/c/redaction/33)
- [임시 라이선스 정보](https://purchase.groupdocs.com/temporary-license/)

---

**마지막 업데이트:** 2026-08-09  
**테스트 환경:** GroupDocs.Redaction 24.9 for Java  
**작성자:** GroupDocs

## 관련 튜토리얼
- [스프레드시트에서 데이터 필터링 방법 – GroupDocs.Redaction Java](/redaction/java/spreadsheet-redaction/)
- [민감 데이터 마스킹 Java – GroupDocs.Redaction으로 개인 정보 리다크션](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)
- [민감 데이터 마스킹 Java – GroupDocs.Redaction 가이드](/redaction/java/getting-started/)