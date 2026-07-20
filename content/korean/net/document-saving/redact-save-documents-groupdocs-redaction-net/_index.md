---
date: '2026-07-20'
description: GroupDocs.Redaction for .NET을 사용하여 문서를 레드랙션하고, 민감한 정보를 숨기며, 레드랙션된 파일을
  메모리 스트림에 저장하는 방법을 배웁니다.
keywords:
- how to redact documents
- redact sensitive information
- redact specific text
- save to memory stream
- save redacted document
lastmod: '2026-07-20'
og_description: GroupDocs.Redaction for .NET을 사용하여 문서를 레드랙션하는 방법. 단계별 가이드를 따라 민감한
  정보를 숨기고 레드랙션된 파일을 메모리 스트림에 저장하세요.
og_image_alt: 'Developer guide: Redact and save documents using GroupDocs.Redaction
  for .NET'
og_title: GroupDocs.Redaction for .NET을 사용한 문서 레드랙션 방법
schemas:
- author: GroupDocs
  dateModified: '2026-07-20'
  description: Learn how to redact documents, hide sensitive information, and save
    redacted files to a memory stream using GroupDocs.Redaction for .NET.
  headline: How to Redact Documents with GroupDocs.Redaction for .NET – A Complete
    Guide
  type: TechArticle
- description: Learn how to redact documents, hide sensitive information, and save
    redacted files to a memory stream using GroupDocs.Redaction for .NET.
  name: How to Redact Documents with GroupDocs.Redaction for .NET – A Complete Guide
  steps:
  - name: '**Load** – Create a `Redactor` instance pointing to your file.'
    text: '**Load** – Create a `Redactor` instance pointing to your file.'
  - name: '**Apply** – Call `Apply` with an `ExactPhraseRedaction` (or other redaction
      type).'
    text: '**Apply** – Call `Apply` with an `ExactPhraseRedaction` (or other redaction
      type).'
  - name: '**Inspect** – Review `RedactorChangeLog` to confirm how many matches were
      found and replaced.'
    text: '**Inspect** – Review `RedactorChangeLog` to confirm how many matches were
      found and replaced.'
  type: HowTo
- questions:
  - answer: Yes—GroupDocs.Redaction treats PDF, DOCX, PPTX, and many image formats
      uniformly; simply point `Redactor` at a PDF file.
    question: Can I redact PDF files using the same API?
  - answer: Absolutely—once redacted, the content is permanently removed, regardless
      of subsequent conversions.
    question: Does the redaction survive after converting the document to another
      format?
  - answer: Use `RedactionOptions` to set the overlay color, opacity, or replace text
      with a custom string.
    question: How do I customize the redaction appearance?
  - answer: Yes—`RegexRedaction` lets you define patterns such as credit‑card numbers
      or email addresses.
    question: Is it possible to redact using regular expressions?
  - answer: .NET Framework 4.6+, .NET Core 3.1+, .NET 5, .NET 6, and .NET 7.
    question: What .NET versions are officially supported?
  type: FAQPage
tags:
- redact documents
- GroupDocs.Redaction
- .NET document processing
- C# redaction tutorial
title: GroupDocs.Redaction for .NET을 사용한 문서 레드랙션 방법 – 완전 가이드
type: docs
url: /ko/net/document-saving/redact-save-documents-groupdocs-redaction-net/
weight: 1
---

# GroupDocs.Redaction for .NET을 사용하여 문서 가리기 방법

현대 기업 환경에서 **문서 가리기**는 개인 데이터, 영업 비밀 및 규정 준수와 관련된 정보를 보호하기 위한 중요한 기술입니다. 이 가이드는 Word, PDF 또는 이미지 파일에서 민감한 정보를 가린 후, 결과를 메모리 스트림에 직접 저장하는 방법을 단계별로 안내합니다—모두 GroupDocs.Redaction for .NET을 사용합니다.

## 빠른 답변
- **가리기는 무엇을 하나요?** 선택한 내용을 영구적으로 자리표시자로 교체하거나 제거하여 데이터가 절대 복구되지 않도록 합니다.  
- **지원되는 형식은 무엇인가요?** PDF, DOCX, PPTX 및 일반 이미지 형식을 포함한 30가지 이상의 파일 유형을 지원합니다.  
- **디스크에 쓰지 않고 가릴 수 있나요?** 예—결과를 `MemoryStream`에 저장하여 메모리 내에서 처리할 수 있습니다.  
- **프로덕션에 라이선스가 필요합니까?** 프로덕션 사용을 위해서는 정식 라이선스가 필요하며, 평가용 무료 체험판을 이용할 수 있습니다.  
- **.NET Core와 호환되나요?** 물론입니다—GroupDocs.Redaction은 .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7과 모두 작동합니다.

## 문서 가리기란 무엇인가요?
문서 가리기는 파일에서 기밀 텍스트, 이미지 및 메타데이터를 영구적으로 제거하거나 가려서 숨겨진 내용이 이후에 복구, 조회 또는 추출될 수 없도록 합니다. 민감한 요소를 검은 사각형이나 사용자 정의 텍스트와 같은 자리표시자로 교체하고, 문서 구조를 업데이트하여 가려진 데이터가 복구 불가능하도록 합니다.

## 문서 가리기에 GroupDocs.Redaction을 사용해야 하는 이유
GroupDocs.Redaction은 **30개 이상의 파일 형식**을 지원하고 전체 문서를 메모리에 로드하지 않고 **2 GB**까지의 파일을 처리할 수 있어, 많은 경쟁 제품에 비해 **30 % 빠른 처리 시간**을 제공합니다. API를 사용하면 정확한 구문, 정규식 또는 이미지 기반 가리기를 단일 메서드 호출로 적용할 수 있어 .NET 개발자에게 가장 효율적인 선택입니다.

## 사전 요구 사항
- **GroupDocs.Redaction** NuGet 패키지(최신 버전).  
- .NET Framework 4.6+ **또는** .NET Core 3.1+ 설치.  
- Visual Studio 2022와 같은 C# 호환 IDE.  
- 기본적인 C# 지식 및 파일 I/O에 대한 이해.

### 필요한 라이브러리 및 버전
- **GroupDocs.Redaction** – 최신 가리기 알고리즘 및 보안 패치를 사용하려면 항상 최신 릴리스를 사용하세요.  
- **System.IO** – 스트림 처리를 위한 (내장 .NET) 라이브러리.

### 라이선스 획득 단계
- **무료 체험:** GroupDocs 웹사이트에서 30일 체험판에 가입하세요.  
- **임시 라이선스:** 개발 테스트용 임시 키를 요청하세요.  
- **정식 라이선스:** 무제한 사용을 위한 프로덕션 라이선스를 구매하세요.

## 기본 초기화 및 설정
`Redactor` 클래스는 GroupDocs.Redaction에서 모든 가리기 작업의 진입점입니다. NuGet 패키지를 설치한 후, 소스 문서 경로를 사용해 `Redactor`를 인스턴스화합니다.

```csharp
using GroupDocs.Redaction;
using System.IO;

// Initialize Redactor with the source file path
Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

## 문서에서 특정 텍스트를 가리는 방법은?
특정 텍스트를 가리려면 `Redactor` 인스턴스로 소스 파일을 로드한 뒤, 숨기려는 정확한 문자열을 대상으로 하는 `ExactPhraseRedaction`을 적용합니다. API가 문서를 스캔하여 각 일치를 선택한 오버레이로 교체하고, 변경 로그에 기록하여 저장하기 전에 가리기 결과를 확인할 수 있습니다.

```csharp
RedactorChangeLog result = redactor.Apply(new ExactPhraseRedaction("John Doe"));
```

`ExactPhraseRedaction` 클래스는 정확한 구문의 모든 발생을 검은 사각형(또는 구성한 사용자 정의 자리표시자)으로 교체합니다.  

**단계별:**
1. **로드** – 파일을 가리키는 `Redactor` 인스턴스를 생성합니다.  
2. **적용** – `ExactPhraseRedaction`(또는 다른 가리기 유형)과 함께 `Apply`를 호출합니다.  
3. **검토** – `RedactorChangeLog`를 검토하여 발견되고 교체된 일치 항목 수를 확인합니다.  

## 가려진 문서를 메모리 스트림에 저장하는 방법은?
`MemoryStream`은 데이터를 메모리에 저장하는 .NET 스트림으로, 디스크 I/O 없이 빠른 읽기/쓰기가 가능합니다. `Save` 메서드를 사용하면 가려진 출력을 `MemoryStream`에 직접 전달할 수 있으며, 이를 네트워크로 전송하거나 데이터베이스에 저장하거나 API 엔드포인트에서 임시 파일 없이 직접 반환할 수 있습니다.

```csharp
using (MemoryStream stream = new MemoryStream())
{
    // Save the redacted document directly into the stream
    redactor.Save(stream);
    // Optionally reset the stream position for downstream consumers
    stream.Position = 0;
    // The stream now contains the redacted file ready for use
}
```

**핵심 포인트:**
- `Save` 메서드는 `MemoryStream`을 포함한 모든 `Stream` 구현에 가려진 출력을 기록합니다.  
- 임시 파일이 생성되지 않아 보안 및 성능이 향상됩니다.  
- 이를 ASP.NET Core의 `FileStreamResult`와 결합하면 파일을 브라우저에 직접 반환할 수 있습니다.

## 일반적인 함정 및 해결책
| 문제 | 발생 원인 | 해결 방법 |
|-------|----------------|-----|
| **가리기가 적용되지 않음** | 구문의 대소문자가 원본과 다릅니다. | `ExactPhraseRedaction("John Doe", caseSensitive: false)`를 사용하거나 유연한 매칭을 위해 정규식 가리기를 사용하세요. |
| **대용량 파일로 인해 OutOfMemory 발생** | 전체 파일을 메모리에 로드하려고 시도했습니다. | GroupDocs.Redaction은 데이터를 내부적으로 스트리밍합니다; 파일을 청크 단위로 처리하는 최신 버전을 사용하고 있는지 확인하세요. |
| **저장된 파일이 손상됨** | 전송 전에 스트림이 초기화되지 않았습니다. | `redactor.Save(stream)` 후에, 읽거나 반환하기 전에 `stream.Position = 0`을 설정하세요. |

## 자주 묻는 질문

**Q: 동일한 API로 PDF 파일을 가릴 수 있나요?**  
A: 예—GroupDocs.Redaction은 PDF, DOCX, PPTX 및 다양한 이미지 형식을 동일하게 처리하므로 `Redactor`를 PDF 파일에 지정하기만 하면 됩니다.

**Q: 문서를 다른 형식으로 변환한 후에도 가리기가 유지되나요?**  
A: 물론입니다—가리면 내용이 영구적으로 제거되어 이후 변환과 관계없이 유지됩니다.

**Q: 가리기 외관을 어떻게 맞춤 설정하나요?**  
A: `RedactionOptions`를 사용하여 오버레이 색상, 불투명도 설정하거나 텍스트를 사용자 정의 문자열로 교체할 수 있습니다.

**Q: 정규식을 사용해 가릴 수 있나요?**  
A: 예—`RegexRedaction`을 사용하면 신용카드 번호나 이메일 주소와 같은 패턴을 정의할 수 있습니다.

**Q: 공식적으로 지원되는 .NET 버전은 무엇인가요?**  
A: .NET Framework 4.6+, .NET Core 3.1+, .NET 5, .NET 6, .NET 7.

---

**마지막 업데이트:** 2026-07-20  
**테스트 환경:** GroupDocs.Redaction 23.12 for .NET  
**작성자:** GroupDocs  

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
using (Redactor redactor = new Redactor(sourceFile))
{
    // Continue to apply redactions...
}
```

## 관련 튜토리얼

- [GroupDocs.Redaction .NET을 사용하여 문서를 로드하고 가리는 방법&#58; 완전 가이드](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [GroupDocs.Redaction .NET을 사용하여 원본 형식으로 가려진 문서 저장](/redaction/net/document-saving/save-redacted-docs-original-format-groupdocs-redaction-net/)
- [.NET에서 스트림을 사용한 안전한 문서 가리기&#58; GroupDocs.Redaction 가이드](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)