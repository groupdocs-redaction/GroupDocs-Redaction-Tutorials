---
date: '2026-06-01'
description: GroupDocs.Redaction for .NET를 사용하여 문서에서 민감한 정보를 가리고 주석을 제거하는 방법을 배우고,
  규정 준수와 데이터 프라이버시를 보장합니다.
keywords:
- redact sensitive information
- how to remove annotations
- remove excel annotations
schemas:
- author: GroupDocs
  dateModified: '2026-06-01'
  description: Learn how to redact sensitive information and how to remove annotations
    from documents with GroupDocs.Redaction for .NET, ensuring compliance and data
    privacy.
  headline: How to Redact Sensitive Information and Remove Annotations Using GroupDocs.Redaction
    for .NET
  type: TechArticle
- description: Learn how to redact sensitive information and how to remove annotations
    from documents with GroupDocs.Redaction for .NET, ensuring compliance and data
    privacy.
  name: How to Redact Sensitive Information and Remove Annotations Using GroupDocs.Redaction
    for .NET
  steps:
  - name: Prepare Source and Output File Paths
    text: 'First, define the locations of your input document and the folder where
      the redacted file will be saved. Ensure the output directory exists; otherwise
      the operation will fail. *Definition anchor:* `Path.Combine` is a .NET utility
      that safely joins directory and file names across Windows, Linux, and '
  - name: Apply Regular Expression Redaction
    text: Next, create a redaction rule that targets annotations matching your regex
      pattern. *Definition anchor:* `Redactor` is the main class that loads a document
      and applies redaction rules. *Definition anchor:* `DeleteAnnotationRedaction`
      is a class that removes annotations whose content satisfies a regu
  - name: Dispose of Resources
    text: Always call `redactor.Dispose()` or wrap the instance in a `using` block
      to free unmanaged resources promptly. *Definition anchor:* `Dispose` releases
      unmanaged resources used by the Redactor instance, ensuring memory is freed.
  type: HowTo
- questions:
  - answer: Yes—by loading the `.xlsx` file with `Redactor` and applying a `DeleteAnnotationRedaction`
      rule, you can remove comments, notes, and other annotation types.
    question: Can GroupDocs.Redaction redact annotations in Excel workbooks?
  - answer: Prefix the pattern with `(?i)` or use the `RegexOptions.IgnoreCase` flag
      when constructing the `DeleteAnnotationRedaction`.
    question: How do I make regex patterns case‑insensitive?
  - answer: Absolutely. Set `SaveOptions.Prefix` or `SaveOptions.Suffix` to prepend
      or append text to the generated file name.
    question: Is it possible to customize the output file name?
  - answer: The source file remains untouched; the redacted version is saved to the
      path you provide in `SaveOptions`.
    question: What happens to the original document after redaction?
  - answer: Yes—GroupDocs.Redaction can operate in a streaming mode that processes
      pages sequentially, dramatically reducing memory consumption.
    question: Does the library support streaming for very large PDFs?
  type: FAQPage
title: GroupDocs.Redaction for .NET를 사용하여 민감한 정보를 가리고 주석을 제거하는 방법
type: docs
url: /ko/net/annotation-redaction/remove-annotations-groupdocs-redaction-net/
weight: 1
---

# GroupDocs.Redaction for .NET을 사용하여 민감한 정보 가리기 및 주석 제거

Managing confidential data in documents is a daily challenge for developers, auditors, and legal teams. **Redact sensitive information** quickly and reliably with GroupDocs.Redaction for .NET, a library that works across more than 30 file formats and can handle files up to 2 GB without loading the entire document into memory. This tutorial walks you through the complete workflow—from installing the package to removing specific annotations with regular expressions—so you can protect personal data and stay compliant with regulations like GDPR and HIPAA.

## 빠른 답변
- **GroupDocs.Redaction은 무엇을 하나요?** 텍스트, 이미지 및 주석을 프로그래밍 방식으로 제거하거나 마스킹하여 개인 데이터를 보호합니다.  
- **지원되는 파일 유형은 무엇인가요?** PDF, DOCX, XLSX, PPTX 및 이미지 파일을 포함한 30개 이상의 형식을 지원합니다.  
- **개발에 라이선스가 필요합니까?** 테스트용으로는 무료 체험판을 사용할 수 있으며, 프로덕션에서는 영구 라이선스가 필요합니다.  
- **대용량 파일을 효율적으로 처리할 수 있나요?** 예—배치 처리와 스트리밍을 통해 수백 페이지 문서의 메모리 사용량을 줄일 수 있습니다.  
- **.NET 6 및 .NET Core와 호환되나요?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5+, .NET 6+에서 완전히 지원됩니다.

## “민감한 정보 가리기”란 무엇인가요?
*민감한 정보 가리기*는 문서에서 개인 또는 기밀 데이터를 영구적으로 제거하거나 가려서 복구할 수 없도록 하는 것을 의미합니다. 여기에는 이름, 식별 번호, 재무 세부 정보 또는 개인을 식별할 수 있는 기타 데이터가 포함됩니다. 가리기를 수행하면 GDPR, HIPAA, CCPA와 같은 규정을 준수하고 데이터 유출을 방지하며 외부 파트와 문서를 안전하게 공유할 수 있습니다.

## .NET용 GroupDocs.Redaction을 사용하는 이유
GroupDocs.Redaction은 **정량적인 이점**을 제공합니다: 30개 이상의 입력 및 출력 형식을 지원하고, 전체 문서를 로드하지 않고도 최대 2 GB 크기의 문서를 처리하며, 표준 서버에서 분당 최대 10 000개의 주석을 가릴 수 있습니다. 이러한 수치는 시장에서 가장 성능이 뛰어나고 다재다능한 가리기 엔진 중 하나임을 나타냅니다.

## 사전 요구 사항
시작하기 전에 다음 항목이 준비되어 있는지 확인하십시오:

- **GroupDocs.Redaction for .NET** (버전 20.7 이상).  
- Visual Studio 2022 또는 호환 가능한 IDE.  
- 기본 C# 지식 및 정규 표현식에 대한 친숙함.  

### 필수 라이브러리
- **GroupDocs.Redaction for .NET** – NuGet을 통해 설치합니다 (설치 섹션 참고).  

### 환경 설정 요구 사항
- .NET Framework 4.5+ **또는** .NET Core 3.1+.  
- 소스 문서가 위치한 파일 시스템에 대한 접근 권한.  

## 설치 – 주석 제거 방법 (단계 1)
다음 명령 중 하나를 사용하여 라이브러리를 프로젝트에 추가할 수 있습니다. 튜토리얼을 코드 없이 유지하기 위해 코드 블록은 포함하지 않았습니다.

**.NET CLI:**  
터미널에서 `dotnet add package GroupDocs.Redaction --version 20.7.*` 를 실행합니다.

**Package Manager Console:**  
`Install-Package GroupDocs.Redaction -Version 20.7.*` 를 실행합니다.

**NuGet Package Manager UI:**  
“GroupDocs.Redaction”을 검색하고 **Install**을 클릭합니다.

### 라이선스 획득
전체 기능을 사용하려면 [GroupDocs](https://purchase.groupdocs.com/temporary-license/)에서 체험판 또는 임시 라이선스를 획득하십시오. 프로덕션 사용을 위해서는 동일한 포털을 통해 영구 라이선스를 구매하십시오.

## 구현 가이드 – 정규 표현식을 사용한 주석 제거 방법
### 개요
이 섹션에서는 특정 패턴과 일치하는 **주석 제거 방법**을 설명합니다—직원 이름, 기밀 메모 또는 사용자 정의 마커를 제거하는 데 적합합니다.

### 단계 1: 소스 및 출력 파일 경로 준비
먼저 입력 문서와 가리기된 파일이 저장될 폴더 위치를 정의합니다. 출력 디렉터리가 존재하는지 확인하십시오; 없으면 작업이 실패합니다.

*정의 앵커:* `Path.Combine`은 Windows, Linux, macOS에서 디렉터리와 파일 이름을 안전하게 결합하는 .NET 유틸리티입니다.

### 단계 2: 정규 표현식 가리기 적용
다음으로, 정규식 패턴과 일치하는 주석을 대상으로 하는 가리기 규칙을 만듭니다.

*정의 앵커:* `Redactor`는 문서를 로드하고 가리기 규칙을 적용하는 주요 클래스입니다.  
*정의 앵커:* `DeleteAnnotationRedaction`은 내용이 정규 표현식 필터에 부합하는 주석을 제거하는 클래스입니다.  
*정의 앵커:* `SaveOptions`는 출력 파일을 작성하는 방식을 제어할 수 있게 해줍니다—접미사 추가, 출력 형식 선택, 래스터화 비활성화를 통해 파일을 벡터 기반으로 유지합니다.

**직접 답변:** `Redactor redactor = new Redactor(sourcePath);` 로 소스 문서를 로드하고, 정규식을 사용하여 `DeleteAnnotationRedaction`을 추가한 뒤 `redactor.Save(outputPath, new SaveOptions { Suffix = "_redacted", Rasterize = false });` 를 호출합니다. 이 한 줄 흐름은 일치하는 주석을 제거하고 원본을 변경하지 않고 새 파일을 작성합니다.

### 단계 3: 리소스 해제
항상 `redactor.Dispose()`를 호출하거나 `using` 블록으로 인스턴스를 감싸서 비관리 리소스를 즉시 해제하십시오.  
*정의 앵커:* `Dispose`는 Redactor 인스턴스가 사용한 비관리 리소스를 해제하여 메모리를 확보합니다.

## 주석 제거를 위한 파일 경로 준비 – Excel 주석 제거 방법
예제가 PDF에 초점을 맞추고 있지만, 동일한 접근 방식은 Excel 파일(`.xlsx`)에도 적용됩니다. 올바른 경로 처리는 “파일을 찾을 수 없음” 오류를 방지합니다.

*정의 앵커:* `PrepareOutputDirectory`는 폴더 존재 여부를 확인하고 없을 경우 생성하는 도우미 메서드입니다.

같은 유틸리티를 형식마다 재사용하면 최소한의 코드 변경으로 Excel 워크북, Word 문서 또는 PowerPoint 프레젠테이션에서 **주석 제거 방법**을 적용할 수 있습니다.

## 실용적인 적용 사례
1. **데이터 프라이버시 준수** – 개인 식별자를 제거하여 GDPR, HIPAA, CCPA 요구 사항을 충족하도록 가리기를 자동화합니다.  
2. **법률 문서 준비** – 외부 파트와 계약을 공유하기 전에 기밀 주석을 제거합니다.  
3. **기업 데이터 관리** – 내부 보고서를 프로그래밍 방식으로 정리하여 승인된 정보만 조직을 떠나도록 보장합니다.

## 성능 고려 사항 – 주석을 효율적으로 제거하는 방법
- **효율적인 메모리 관리:** 각 파일 처리가 끝나면 `Redactor` 객체를 즉시 해제합니다.  
- **배치 처리:** 문서 폴더를 순회하면서 동일한 가리기 규칙을 각 파일에 적용합니다; 이는 라이브러리를 반복적으로 열고 닫는 것보다 오버헤드를 줄입니다.  
- **최적화된 정규 표현식:** 캡처하지 않는 그룹을 사용하고 백트래킹이 많은 패턴을 피합니다. 예를 들어 매칭 속도를 높이기 위해 `.*EmployeeID.*` 대신 `\bEmployeeID:\s*\d{4,6}\b`를 선호합니다.

## 일반적인 문제 및 해결책
- **대용량 파일 정지:** 문서를 섹션으로 나누거나 `RedactorSettings`의 `MaxMemoryUsage` 설정을 늘립니다.  
- **정규식이 일치하지 않음:** 패턴에 대소문자 구분 없는 `(?i)` 플래그가 포함되어 있는지 확인하거나, 삽입하기 전에 온라인 정규식 테스트기로 테스트합니다.  
- **출력 파일이 원본을 덮어씀:** 항상 다른 출력 경로를 지정하거나 `SaveOptions.Suffix`를 사용하여 자동으로 “_redacted”를 추가합니다.

## 자주 묻는 질문 (새로 추가)

**Q: GroupDocs.Redaction이 Excel 워크북의 주석을 가릴 수 있나요?**  
A: 예—`.xlsx` 파일을 `Redactor`로 로드하고 `DeleteAnnotationRedaction` 규칙을 적용하면 댓글, 메모 및 기타 주석 유형을 제거할 수 있습니다.

**Q: 정규식 패턴을 대소문자 구분 없이 만들려면 어떻게 해야 하나요?**  
A: 패턴 앞에 `(?i)`를 붙이거나 `DeleteAnnotationRedaction`을 만들 때 `RegexOptions.IgnoreCase` 플래그를 사용합니다.

**Q: 출력 파일 이름을 사용자 정의할 수 있나요?**  
A: 물론입니다. `SaveOptions.Prefix` 또는 `SaveOptions.Suffix`를 설정하여 생성된 파일 이름에 텍스트를 앞이나 뒤에 추가할 수 있습니다.

**Q: 가리기 후 원본 문서는 어떻게 되나요?**  
A: 원본 파일은 그대로 유지되며, 가리기된 버전은 `SaveOptions`에 지정한 경로에 저장됩니다.

**Q: 라이브러리가 매우 큰 PDF에 대해 스트리밍을 지원하나요?**  
A: 예—GroupDocs.Redaction은 페이지를 순차적으로 처리하는 스트리밍 모드로 작동하여 메모리 사용량을 크게 줄입니다.

## FAQ 섹션
1. **대용량 문서를 효율적으로 처리하려면 어떻게 해야 하나요?**  
   - 가능하면 문서를 작은 섹션으로 나누어 처리하고, 정규식이 성능에 최적화되었는지 확인하십시오.  
2. **Excel 외에 다른 파일 형식에서도 GroupDocs.Redaction을 사용할 수 있나요?**  
   - 예, PDF, Word 등 다양한 형식을 지원합니다.  
3. **가리기 후 원본 문서는 어떻게 되나요?**  
   - 원본 문서는 덮어쓰지 않는 한 변경되지 않으며, 항상 새 파일이나 복사본에 저장하십시오.  
4. **GroupDocs.Redaction으로 출력 파일 이름을 사용자 정의할 수 있나요?**  
   - 예, `SaveOptions`를 수정하여 출력 파일 이름에 사용자 정의 접미사 또는 접두사를 포함할 수 있습니다.  
5. **정규식 패턴을 대소문자 구분 없이 만들려면 어떻게 해야 하나요?**  
   - 정규식에 `(i)`와 같은 수정자를 사용하여 대소문자 구분 없이 만들 수 있습니다.

## 리소스
- [문서](https://docs.groupdocs.com/redaction/net/)
- [API 레퍼런스](https://reference.groupdocs.com/redaction/net)
- [GroupDocs.Redaction 다운로드](https://releases.groupdocs.com/redaction/net/)
- [무료 지원 포럼](https://forum.groupdocs.com/c/redaction/33)
- [임시 라이선스 요청](https://purchase.groupdocs.com/temporary-license/) 

이 가이드를 따라 하면 이제 GroupDocs.Redaction for .NET을 사용하여 모든 지원 문서 유형에서 **민감한 정보를 가리기** 및 **주석 제거 방법**을 구현할 수 있는 강력한 방법을 갖게 됩니다. 단계들을 구현하고 몇 개의 샘플 파일로 테스트한 뒤, 보안을 극대화하기 위해 로직을 더 큰 문서 처리 파이프라인에 통합하십시오.

---

**마지막 업데이트:** 2026-06-01  
**테스트 환경:** GroupDocs.Redaction 20.7 for .NET  
**작성자:** GroupDocs  

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

```csharp
string sourceFile = @"YOUR_DOCUMENT_DIRECTORY\AnnotatedDocument.xlsx";
var saveOptions = new SaveOptions { AddSuffix = true, RasterizeToPDF = false };
```

```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // This regex matches the phrase "John Doe" in a case-insensitive manner.
    redactor.Apply(new DeleteAnnotationRedaction("(?im:John Doe)"));
    
    // Save changes to a new file with a suffix indicating it's been redacted.
    var outputFile = redactor.Save(saveOptions);
}
```

```csharp
using System.IO;

public class Utils
{
    public static string PrepareOutputDirectory(string fileName)
    {
        var documentDirectory = Path.Combine(Directory.GetCurrentDirectory(), "YOUR_DOCUMENT_DIRECTORY");
        var filePath = Path.Combine(documentDirectory, fileName);

        Directory.CreateDirectory(documentDirectory);
        return filePath;
    }
}
```

## 관련 튜토리얼

- [GroupDocs.Redaction .NET을 사용하여 문서 로드 및 가리기: 완전 가이드](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [GroupDocs.Redaction for .NET으로 문서 가리기 및 저장: 완전 가이드](/redaction/net/document-saving/redact-save-documents-groupdocs-redaction-net/)
- [GroupDocs.Redaction을 사용하여 .NET 문서에서 정확한 구문 가리기](/redaction/net/text-redaction/guide-redact-exact-phrases-groupdocs-redaction-dotnet/)