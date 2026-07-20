---
date: '2026-07-20'
description: GroupDocs.Redaction .NET를 사용하여 형식을 나열하는 방법을 배우고, 이 기능을 문서 워크플로에 통합하며,
  성능을 향상시키세요.
keywords:
- how to list formats
- GroupDocs.Redaction supported formats
- .NET document processing
lastmod: '2026-07-20'
og_description: GroupDocs.Redaction .NET를 사용하여 형식을 나열하는 방법을 알아보고, 단계별 가이드를 확인하며, .NET
  애플리케이션에서 최적 성능을 위한 팁을 얻으세요.
og_image_alt: Guide showing how to list supported file formats with GroupDocs.Redaction
  in a .NET project
og_title: GroupDocs.Redaction .NET를 사용하여 형식 나열하는 방법
schemas:
- author: GroupDocs
  dateModified: '2026-07-20'
  description: Learn how to list formats using GroupDocs.Redaction .NET, integrate
    the feature into your document workflow, and improve performance.
  headline: How to List Formats with GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to list formats using GroupDocs.Redaction .NET, integrate
    the feature into your document workflow, and improve performance.
  name: How to List Formats with GroupDocs.Redaction .NET
  steps:
  - name: '**Document Management Systems** – Validate uploads against the supported
      list to prevent processing failures.'
    text: '**Document Management Systems** – Validate uploads against the supported
      list to prevent processing failures.'
  - name: '**Content Security** – Apply redaction rules only to file types that the
      engine can safely modify.'
    text: '**Content Security** – Apply redaction rules only to file types that the
      engine can safely modify.'
  - name: '**Batch Processing Pipelines** – Filter large file batches before invoking
      redaction, saving CPU and memory.'
    text: '**Batch Processing Pipelines** – Filter large file batches before invoking
      redaction, saving CPU and memory.'
  - name: '**How do I install GroupDocs.Redaction for .NET?**'
    text: '**How do I install GroupDocs.Redaction for .NET?**'
  - name: '**What are some common issues when retrieving supported formats?**'
    text: '**What are some common issues when retrieving supported formats?**'
  - name: '**Can I use this feature with non‑.NET applications?**'
    text: '**Can I use this feature with non‑.NET applications?**'
  - name: '**How can I optimise performance when using GroupDocs.Redaction?**'
    text: '**How can I optimise performance when using GroupDocs.Redaction?**'
  - name: '**What file types does GroupDocs.Redaction support?**'
    text: '**What file types does GroupDocs.Redaction support?**'
  type: HowTo
- questions:
  - answer: Yes, `FileType.GetSupportedFileFormats()` is static and does not require
      a `Redactor` object.
    question: Can I retrieve the format list without initializing a Redactor instance?
  - answer: The method returns all formats that the library can both read and write;
      each `FileType` includes a `CanRead` and `CanWrite` flag.
    question: Does the list include both input and output formats?
  - answer: GroupDocs releases format updates with each library version; checking
      the list at runtime ensures you always have the latest set.
    question: How often is the supported format list updated?
  - answer: Yes, filter the collection where `format.Extension == ".pdf"` or where
      `format.Name.Contains("PDF")`.
    question: Is there a way to filter only PDF‑compatible formats?
  - answer: The method requires .NET Core 3.1 or later; earlier runtimes are not supported.
    question: Will this approach work on .NET Core 2.1?
  type: FAQPage
tags:
- how to list formats
- GroupDocs.Redaction
- .NET file handling
title: GroupDocs.Redaction .NET를 사용하여 형식 나열하는 방법
type: docs
url: /ko/net/format-handling/groupdocs-redaction-net-supported-formats-listing/
weight: 1
---

# GroupDocs.Redaction .NET에서 형식 목록 가져오기

다양한 문서 유형을 관리하는 것은 문서 중심 애플리케이션을 구축하는 개발자에게 일상적인 현실입니다. 이 튜토리얼에서는 GroupDocs.Redaction .NET이 처리할 수 있는 **형식 목록 가져오기** 방법을 배우게 되며, 이를 통해 파일을 처리하기 전에 검증하고, 사용자에게 정확한 옵션을 제공하며, 워크플로우를 효율적으로 유지할 수 있습니다.

## 소개

효율적인 문서 처리는 라이브러리가 정확히 어떤 파일 유형을 지원하는지 아는 것에서 시작됩니다. GroupDocs.Redaction은 이 정보를 가져오는 내장 메서드를 제공하여 동적 UI 요소를 구축하고, 검증 규칙을 적용하며, 런타임 오류를 방지할 수 있게 합니다. 아래에서는 설치부터 실용적인 코드 스니펫 및 성능 팁까지, 바로 시작하는 데 필요한 모든 내용을 확인할 수 있습니다.

### 빠른 답변
- **“형식 목록 가져오기”는 무엇을 의미하나요?** GroupDocs.Redaction이 처리할 수 있는 파일 확장자 컬렉션을 가져오는 것을 의미합니다.  
- **라이선스가 필요합니까?** 예, 프로덕션 사용을 위해서는 유효한 GroupDocs.Redaction 라이선스가 필요합니다.  
- **지원되는 .NET 버전은 무엇인가요?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.  
- **사용 가능한 형식은 몇 개인가요?** 기본 제공으로 30개 이상의 입력 및 출력 형식을 지원합니다.  
- **특별한 설정이 필요합니까?** 표준 라이브러리 초기화 외에 추가 설정은 필요하지 않습니다.

## “형식 목록 가져오기”란 무엇인가요?

이는 라이브러리의 FileType API를 호출하여 각 항목에 파일 확장자와 사람이 읽을 수 있는 이름이 포함된 컬렉션을 얻는 것을 의미합니다. 개발자는 이 컬렉션을 반복하여 검증 규칙을 만들거나, UI 드롭다운을 채우거나, 지원되는 형식을 로그에 기록함으로써 호환 가능한 문서만 처리하도록 할 수 있습니다.

## GroupDocs.Redaction에서 형식 목록을 가져와야 하는 이유

GroupDocs.Redaction은 PDF, DOCX, PPTX 및 이미지 형식을 포함한 **30개 이상의** 고유 파일 유형을 지원하므로 대부분의 엔터프라이즈 문서를 서드파티 변환기 없이 처리할 수 있습니다. 이러한 형식을 프로그래밍 방식으로 나열하면 추측을 없애고, 지원 티켓을 감소시키며, 호환되지 않는 파일이 처리 파이프라인에 들어가는 것을 방지할 수 있습니다.

## 전제 조건

- **GroupDocs.Redaction for .NET** – 공식 사이트에서 최신 패키지를 다운로드합니다.  
- **.NET Framework 또는 .NET Core** – 개발 환경과 호환되는 버전.  
- **Visual Studio** (또는 C#을 지원하는 IDE).  
- C# 구문에 대한 기본적인 이해.

## GroupDocs.Redaction for .NET 설정

### .NET CLI
`dotnet add package GroupDocs.Redaction`

### 패키지 관리자
`Install-Package GroupDocs.Redaction`

### NuGet 패키지 관리자 UI
- **“GroupDocs.Redaction”**을 검색하고 최신 버전을 설치합니다.

### 라이선스 획득
GroupDocs는 무료 체험, 평가용 임시 라이선스, 정식 구매 옵션을 제공합니다. 적절한 라이선스 파일을 얻으려면 GroupDocs 웹사이트를 방문하세요.

### 기본 초기화 및 설정
패키지를 추가한 후 네임스페이스를 참조하고 `Redactor` 인스턴스를 생성합니다:

```csharp
using GroupDocs.Redaction;

// Initialize with a license file (replace path as needed)
Redactor redactor = new Redactor("path/to/license/file.lic");
```

## 구현 가이드

### GroupDocs.Redaction .NET에서 형식 목록을 가져오는 방법은?
라이브러리를 로드하고 정적 헬퍼를 호출한 뒤 결과를 정렬하면 두 줄의 코드만으로 바로 사용할 수 있는 컬렉션을 얻을 수 있습니다. `FileType.GetSupportedFileFormats()`를 사용하여 각 형식의 확장자와 표시 이름을 포함하는 `IEnumerable<FileType>`을 가져온 다음, 확장자별로 정렬하여 깔끔한 UI 목록을 만들 수 있습니다.

### 지원되는 파일 형식 가져오기

#### 개요
목표는 GroupDocs.Redaction이 처리할 수 있는 파일 유형 목록을 확보하여 검증 로직, UI 드롭다운 또는 로깅 메커니즘에 통합하는 것입니다.

#### 단계별 구현

**1. 지원되는 파일 유형 가져오기**  
`FileType.GetSupportedFileFormats()`는 라이브러리가 인식하는 모든 형식을 반환합니다. 이 메서드는 파일 확장자와 친숙한 이름과 같은 메타데이터를 캡슐화한 `GroupDocs.Redaction.FileType` 클래스의 일부입니다.

**2. 지원되는 파일 유형 표시하기**  
컬렉션을 반복하면서 각 형식의 확장자와 설명을 출력합니다. 인라인 코드 예시:

```csharp
var formats = FileType.GetSupportedFileFormats()
                      .OrderBy(f => f.Extension);

foreach (var format in formats)
{
    Console.WriteLine($"{format.Extension} – {format.Name}");
}
```

이 스니펫은 “.pdf – Portable Document Format”과 같이 정렬된 목록을 출력하므로 UI 요소를 채우기에 적합합니다.

### 문제 해결 팁
- **패키지 누락** – NuGet 패키지 참조를 확인하고 필요 시 패키지를 복원합니다.  
- **잘못된 라이선스 경로** – 라이선스 파일이 출력 디렉터리에 복사되었는지 또는 절대 경로를 제공했는지 확인합니다.  
- **지원되지 않는 확장자** – 형식이 목록에 없으면 최신 라이브러리 버전을 사용하고 있는지 확인합니다. 최신 릴리스에서는 추가 형식이 포함됩니다.

## 실용적인 적용 사례
지원되는 파일 형식을 이해하면 여러 실제 시나리오에서 활용할 수 있습니다:

1. **문서 관리 시스템** – 업로드를 지원 목록과 대조하여 처리 실패를 방지합니다.  
2. **콘텐츠 보안** – 엔진이 안전하게 수정할 수 있는 파일 유형에만 레드랙션 규칙을 적용합니다.  
3. **배치 처리 파이프라인** – 레드랙션을 호출하기 전에 대량 파일을 필터링하여 CPU와 메모리를 절약합니다.

## 성능 고려 사항
- **메모리 사용량** – 형식 목록을 나열하는 작업은 가벼운 연산이며 문서를 메모리로 로드하지 않습니다.  
- **배치 작업** – 수백 개 파일을 처리할 때 형식 목록을 한 번만 가져와 재사용하면 중복 호출을 피할 수 있습니다.  
- **스레드 안전성** – `FileType.GetSupportedFileFormats()`는 스레드 안전하며 동시 작업에서 동기화 없이 호출할 수 있습니다.

## 결론
이제 GroupDocs.Redaction .NET을 사용하여 **형식 목록을 가져오는** 완전하고 프로덕션 준비된 방법을 알게 되었습니다. 이 기능을 통합하면 검증을 강화하고 사용자 경험을 개선하며 문서 파이프라인을 견고하게 유지할 수 있습니다.

### 다음 단계
- 파일 유형에 따라 레드랙션 규칙을 적용하려면 `Redactor` API를 탐색합니다.  
- 형식 목록을 프런트엔드 드롭다운과 결합하여 원활한 파일 선택을 구현합니다.  
- 대규모 배치 작업을 최적화하기 위한 성능 가이드를 검토합니다.

## 자주 묻는 질문

**Q: Redactor 인스턴스를 초기화하지 않고도 형식 목록을 가져올 수 있나요?**  
A: 예, `FileType.GetSupportedFileFormats()`는 정적 메서드이며 `Redactor` 객체가 필요하지 않습니다.

**Q: 목록에 입력 및 출력 형식이 모두 포함되어 있나요?**  
A: 이 메서드는 라이브러리가 읽고 쓸 수 있는 모든 형식을 반환합니다; 각 `FileType`에는 `CanRead`와 `CanWrite` 플래그가 포함됩니다.

**Q: 지원되는 형식 목록은 얼마나 자주 업데이트되나요?**  
A: GroupDocs는 각 라이브러리 버전마다 형식 업데이트를 제공하므로, 런타임에 목록을 확인하면 항상 최신 세트를 확보할 수 있습니다.

**Q: PDF와 호환되는 형식만 필터링할 방법이 있나요?**  
A: 예, `format.Extension == ".pdf"` 또는 `format.Name.Contains("PDF")`와 같이 컬렉션을 필터링하면 됩니다.

**Q: 이 접근 방식이 .NET Core 2.1에서도 작동하나요?**  
A: 해당 메서드는 .NET Core 3.1 이상이 필요하며, 이전 런타임은 지원되지 않습니다.

## FAQ 섹션
1. **GroupDocs.Redaction for .NET을 어떻게 설치하나요?**  
   CLI 명령 `dotnet add package GroupDocs.Redaction`을 사용하거나 NuGet 패키지 관리자 UI를 통해 설치합니다.  
2. **지원되는 형식을 가져올 때 흔히 발생하는 문제는 무엇인가요?**  
   모든 종속성이 복원되었는지, 올바른 네임스페이스(`GroupDocs.Redaction`)를 참조하고 있는지 확인합니다.  
3. **이 기능을 .NET이 아닌 애플리케이션에서도 사용할 수 있나요?**  
   이 튜토리얼은 .NET에 초점을 맞추지만, GroupDocs는 Java, Python 등 다른 플랫폼용 유사 API를 제공합니다.  
4. **GroupDocs.Redaction 사용 시 성능을 최적화하려면 어떻게 해야 하나요?**  
   형식 목록을 재사용하고, 호환성만 확인할 때 전체 문서를 로드하지 않으며, 배치 작업 중 메모리 사용량을 모니터링합니다.  
5. **GroupDocs.Redaction이 지원하는 파일 유형은 무엇인가요?**  
   라이브러리는 PDF, DOCX, PPTX, XLSX, BMP, PNG, JPEG 등을 포함한 30개 이상의 형식을 지원합니다. 전체 목록은 `FileType.GetSupportedFileFormats()`를 통해 확인하세요.

## 리소스
- [문서](https://docs.groupdocs.com/redaction/net/)
- [API 레퍼런스](https://reference.groupdocs.com/redaction/net)
- [GroupDocs.Redaction 다운로드](https://releases.groupdocs.com/redaction/net/)
- [무료 지원 포럼](https://forum.groupdocs.com/c/redaction/33)
- [임시 라이선스](https://purchase.groupdocs.com/temporary-license/)

---

**마지막 업데이트:** 2026-07-20  
**테스트 환경:** GroupDocs.Redaction 4.2.0 for .NET  
**작성자:** GroupDocs  

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

```csharp
using GroupDocs.Redaction;
// Initialize the Redactor with file path
Redactor redactor = new Redactor("sample.pdf");
```

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using GroupDocs.Redaction;

// Step 1: Use GroupDocs.Redaction API to fetch all supported formats.
IEnumerable<FileType> supportedFileTypes = FileType.GetSupportedFileFormats().OrderBy(f => f.Extension);
```

```csharp
// Step 2: Loop through the list of file types and print details.
foreach (FileType fileType in supportedFileTypes)
{
    Console.WriteLine($"{fileType.Extension} - {fileType.FileFormatName}");
}
```

## 관련 튜토리얼

- [GroupDocs.Redaction .NET용 형식 처리 튜토리얼](/redaction/net/format-handling/)
- [GroupDocs.Redaction for .NET 문서 로드 튜토리얼](/redaction/net/document-loading/)
- [GroupDocs.Redaction .NET 문서 저장 튜토리얼](/redaction/net/document-saving/)