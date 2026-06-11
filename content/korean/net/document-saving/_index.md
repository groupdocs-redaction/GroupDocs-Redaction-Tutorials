---
date: 2026-06-11
description: GroupDocs.Redaction for .NET를 사용하여 마스킹된 파일을 내보내고, 출력 폴더를 구성하며, 래스터화된
  PDF를 생성하고, 스트림에 저장하는 방법을 배웁니다.
keywords:
- how to export redacted
- configure output folder
- create rasterized pdf
- save rasterized pdf
- convert redacted to pdf
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to export redacted files, configure output folders, create
    rasterized PDFs, and save to streams using GroupDocs.Redaction for .NET.
  headline: How to Export Redacted Documents with GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to export redacted files, configure output folders, create
    rasterized PDFs, and save to streams using GroupDocs.Redaction for .NET.
  name: How to Export Redacted Documents with GroupDocs.Redaction .NET
  steps:
  - name: Install the NuGet Package
    text: 'Add the latest GroupDocs.Redaction package to your project:'
  - name: Load the Document and Define Redactions
    text: Create a `Redactor` instance, load the file, and specify the regions you
      want to hide. The `Redactor` class provides the core functionality for loading
      documents and applying redaction rules.
  - name: Choose the Export Method
    text: '#### Export in Original Format'
  type: HowTo
- questions:
  - answer: Yes, GroupDocs.Redaction can convert most input types to PDF, DOCX, XLSX,
      PPTX, or rasterized PDF, covering over 30 formats.
    question: Can I export to a format that wasn’t originally supported?
  - answer: By rendering each page as a flat image, any hidden text layers are removed,
      making it impossible to extract the original content.
    question: How does rasterization protect redacted data?
  - answer: Absolutely – you can call `Apply` repeatedly or pass a collection of `RedactionOptions`
      to process many patterns in one pass. `RedactionOptions` defines the settings
      for a single redaction operation, such as region and replacement type.
    question: Is it possible to chain multiple redaction rules?
  - answer: The `Redactor` implements `IDisposable`; wrap it in a `using` block or
      call `Dispose()` to release file handles promptly. `IDisposable` is an interface
      that provides a mechanism for releasing unmanaged resources.
    question: Do I need to close the Redactor object?
  - answer: GroupDocs.Redaction is validated on .NET Framework 4.6+, .NET Core 3.1+,
      and .NET 5/6/7.
    question: What .NET runtimes are officially tested?
  type: FAQPage
title: GroupDocs.Redaction .NET를 사용하여 마스킹된 문서 내보내는 방법
type: docs
url: /ko/net/document-saving/
weight: 3
---

# GroupDocs.Redaction .NET를 사용하여 편집된 문서 내보내는 방법

이 포괄적인 가이드에서는 GroupDocs.Redaction for .NET을 사용하여 **편집된 콘텐츠를 안전하고 효율적으로 내보내는 방법**을 알아봅니다. 원본 파일 형식을 유지하거나 문서를 래스터화된 PDF로 잠그거나 결과를 메모리에서 직접 스트리밍해야 하는 경우, 명확하고 대화형 설명과 실제 팁을 통해 모든 옵션을 안내합니다. 이 튜토리얼을 마치면 모든 규정 준수 시나리오에 맞는 적절한 내보내기 전략을 선택할 수 있게 됩니다.

## 빠른 답변
- **어떤 형식으로 내보낼 수 있나요?** GroupDocs.Redaction이 지원하는 30개 이상의 기본 형식과 최대 보안을 위한 래스터화 PDF를 모두 지원합니다.  
- **스트리밍에 라이선스가 필요합니까?** 예, 프로덕션 스트리밍을 위해서는 유효한 GroupDocs.Redaction 라이선스가 필요합니다.  
- **사용자 지정 출력 폴더를 설정할 수 있나요?** 물론입니다 – `OutputPath` 속성이나 `SaveOptions`를 사용하여 구성하십시오.  
- **대용량 파일에 래스터화가 안전한가요?** 전체 파일을 메모리에 로드하지 않고도 500페이지까지의 문서를 처리합니다.  
- **지원되는 .NET 버전은 무엇인가요?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.

## GroupDocs.Redaction이란?
GroupDocs.Redaction은 PDF, Word, Excel, PowerPoint, 이미지 및 기타 다양한 형식에서 민감한 정보를 프로그래밍 방식으로 제거하거나 마스킹하는 .NET 라이브러리입니다. 편집 영역을 정의하고 정책을 적용한 뒤 정리된 문서를 내보내는 고수준 API를 제공합니다. 이를 통해 모든 .NET 애플리케이션에 편집 기능을 손쉽게 통합할 수 있습니다.

## 왜 편집된 문서를 래스터화 PDF로 내보내야 할까요?
래스터화 PDF는 각 페이지를 평면 이미지로 변환하여 나중에 추출될 수 있는 숨겨진 텍스트 레이어를 제거합니다. 이 형식은 편집된 콘텐츠가 복구될 수 없음을 보장하며 GDPR 및 HIPAA와 같은 엄격한 규제 표준을 충족합니다. GroupDocs.Redaction은 시각적 품질을 유지하면서 보안을 보장하기 위해 최대 300 dpi까지 래스터화 PDF를 생성할 수 있습니다.

## 편집된 문서를 내보내는 방법
소스 파일을 로드하고 편집 규칙을 적용한 다음 적절한 저장 메서드를 호출합니다—원본 형식은 `Save`, 이미지 전용 PDF는 `SaveAsRasterizedPdf`, 메모리 내 처리는 `SaveToStream`을 사용합니다. 아래는 단계별 워크플로우입니다. 각 메서드는 원하는 출력 형식을 유지하면서 편집된 콘텐츠를 영구적으로 제거합니다.

### 단계 1: NuGet 패키지 설치
프로젝트에 최신 GroupDocs.Redaction 패키지를 추가합니다:

```bash
dotnet add package GroupDocs.Redaction
```

### 단계 2: 문서 로드 및 편집 정의
`Redactor` 인스턴스를 생성하고 파일을 로드한 뒤 숨기려는 영역을 지정합니다. `Redactor` 클래스는 문서를 로드하고 편집 규칙을 적용하는 핵심 기능을 제공합니다.

```csharp
using GroupDocs.Redaction;
using GroupDocs.Redaction.Options;

// Load the document
var redactor = Redactor.Create("SensitiveReport.docx");

// Define a redaction for a specific text pattern
redactor.Apply(new RedactionOptions
{
    SearchPattern = "SSN: \\d{3}-\\d{2}-\\d{4}",
    RedactionColor = System.Drawing.Color.Black,
    RedactionType = RedactionType.Image
});
```

### 단계 3: 내보내기 방법 선택
#### 원본 형식으로 내보내기
```csharp
redactor.Save("RedactedReport.docx");
```

#### 래스터화 PDF로 내보내기
```csharp
var rasterOptions = new RasterizationOptions { Dpi = 300 };
redactor.SaveAsRasterizedPdf("RedactedReport.pdf", rasterOptions);
```

#### 메모리 스트림으로 내보내기 (웹 API에 이상적)
```csharp
using var stream = new MemoryStream();
redactor.Save(stream, SaveOptions.CreatePdf());
stream.Position = 0; // Reset for reading
```

`Save` 메서드는 편집된 문서를 원본 형식의 파일로 기록합니다. `SaveAsRasterizedPdf`는 각 페이지를 이미지로 렌더링하여 숨겨진 텍스트를 제거한 PDF를 생성합니다. `SaveToStream`은 편집된 파일을 메모리 스트림으로 반환하여 웹 응답에 적합합니다.

## 출력 폴더를 구성하는 방법?
`Redactor`의 `OutputPath` 속성을 설정하거나 원하는 디렉터리를 포함하는 사용자 지정 `SaveOptions` 객체를 전달합니다. `OutputPath`는 `Redactor`의 속성으로 출력 파일이 기록되는 디렉터리를 지정합니다. `SaveOptions`를 사용하면 출력 폴더를 포함한 다양한 저장 매개변수를 사용자 정의할 수 있습니다. 이를 통해 모든 내보낸 파일이 예측 가능한 위치에 저장되어 배치 처리 파이프라인을 단순화합니다. 또한 문서 유형별로 하위 폴더를 지정하여 작업 공간을 정리할 수 있습니다.

```csharp
var options = SaveOptions.CreatePdf();
options.OutputPath = @"C:\RedactedOutputs\";
redactor.Save(options);
```

## 일반적인 문제와 해결책
- **편집이 적용되지 않음:** 검색 패턴이 문서 텍스트와 정확히 일치하는지 확인하고, 필요하면 `RegexOptions.IgnoreCase`를 사용하십시오. `RegexOptions`는 대소문자 구분과 같은 정규식 매칭 동작을 제어하는 열거형입니다.  
- **대용량 파일으로 메모리 압박 발생:** `SaveToStream`을 사용하여 스트리밍 모드를 활성화하고 전체 문서에 `Save`를 호출하는 것을 피하십시오.  
- **래스터화 PDF가 흐릿함:** 이미지 품질을 향상시키기 위해 `RasterizationOptions`에서 DPI를 높이십시오(예: 300–600). `RasterizationOptions`는 래스터화 PDF 출력에 대한 DPI 및 이미지 형식과 같은 매개변수를 설정할 수 있게 합니다.

## 자주 묻는 질문

**Q: 원래 지원되지 않던 형식으로 내보낼 수 있나요?**  
A: 예, GroupDocs.Redaction은 대부분의 입력 유형을 PDF, DOCX, XLSX, PPTX 또는 래스터화 PDF로 변환할 수 있으며 30개 이상의 형식을 지원합니다.

**Q: 래스터화가 편집된 데이터를 어떻게 보호하나요?**  
A: 각 페이지를 평면 이미지로 렌더링함으로써 숨겨진 텍스트 레이어가 제거되어 원본 콘텐츠를 추출할 수 없게 됩니다.

**Q: 여러 편집 규칙을 연속해서 적용할 수 있나요?**  
A: 물론입니다 – `Apply`를 반복 호출하거나 `RedactionOptions` 컬렉션을 전달하여 한 번에 여러 패턴을 처리할 수 있습니다. `RedactionOptions`는 영역 및 교체 유형과 같은 단일 편집 작업의 설정을 정의합니다.

**Q: Redactor 객체를 닫아야 하나요?**  
A: `Redactor`는 `IDisposable`을 구현하므로 `using` 블록으로 감싸거나 `Dispose()`를 호출하여 파일 핸들을 즉시 해제하십시오. `IDisposable`은 관리되지 않는 리소스를 해제하는 메커니즘을 제공하는 인터페이스입니다.

**Q: 공식적으로 테스트된 .NET 런타임은 무엇인가요?**  
A: GroupDocs.Redaction은 .NET Framework 4.6+, .NET Core 3.1+, 및 .NET 5/6/7에서 검증되었습니다.

## 추가 리소스

### 사용 가능한 튜토리얼
- [GroupDocs.Redaction for .NET를 사용하여 래스터화 PDF로 문서 저장하는 방법: 완전 가이드](./groupdocs-redaction-net-rasterized-pdfs/)
- [GroupDocs.Redaction와 함께 .NET에서 출력 디렉터리 구현하기: 종합 가이드](./implement-output-directory-groupdocs-redaction-dotnet/)
- [GroupDocs.Redaction for .NET를 사용하여 문서 편집 및 저장: 완전 가이드](./redact-save-documents-groupdocs-redaction-net/)
- [GroupDocs.Redaction .NET를 사용하여 원본 형식으로 편집된 문서 저장](./save-redacted-docs-original-format-groupdocs-redaction-net/)
- [.NET에서 스트림을 사용한 안전한 문서 편집: GroupDocs.Redaction 가이드](./secure-document-redaction-net-streams-groupdocs-redaction/)

### 유용한 링크
- [GroupDocs.Redaction for .NET 문서](https://docs.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction for .NET API 레퍼런스](https://reference.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction for .NET 다운로드](https://releases.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction 포럼](https://forum.groupdocs.com/c/redaction/33)
- [무료 지원](https://forum.groupdocs.com/)
- [임시 라이선스](https://purchase.groupdocs.com/temporary-license/)

---

**마지막 업데이트:** 2026-06-11  
**테스트 환경:** GroupDocs.Redaction 23.11 for .NET  
**작성자:** GroupDocs  

## 관련 튜토리얼
- [GroupDocs.Redaction .NET를 사용하여 원본 형식으로 편집된 문서 저장](/redaction/net/document-saving/save-redacted-docs-original-format-groupdocs-redaction-net/)
- [GroupDocs.Redaction for .NET를 사용하여 래스터화 PDF로 문서 저장하는 방법: 완전 가이드](/redaction/net/document-saving/groupdocs-redaction-net-rasterized-pdfs/)
- [.NET에서 스트림을 사용한 안전한 문서 편집: GroupDocs.Redaction 가이드](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)