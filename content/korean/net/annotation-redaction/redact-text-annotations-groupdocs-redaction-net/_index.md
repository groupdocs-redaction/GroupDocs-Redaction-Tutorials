---
date: '2026-05-27'
description: GroupDocs.Redaction for .NET를 사용하여 PDF의 주석을 삭제하는 방법을 배우고, 설정, 정규식 삭제
  및 성능 팁을 다룹니다.
keywords:
- how to redact annotations
- apply redaction to pdf
- pdf annotation redaction
schemas:
- author: GroupDocs
  dateModified: '2026-05-27'
  description: Learn how to redact annotations in PDFs with GroupDocs.Redaction for
    .NET, covering setup, regex redaction, and performance tips.
  headline: How to Redact Annotations Using GroupDocs.Redaction for .NET
  type: TechArticle
- description: Learn how to redact annotations in PDFs with GroupDocs.Redaction for
    .NET, covering setup, regex redaction, and performance tips.
  name: How to Redact Annotations Using GroupDocs.Redaction for .NET
  steps:
  - name: Create a Redactor instance (definition anchor)
    text: '`Redactor` is the entry point for all redaction operations; you pass the
      source file path to its constructor.'
  - name: Define your regular expression (definition anchor)
    text: '`Regex` is the .NET class that evaluates patterns; you can enable case‑insensitivity
      (`i`) and multi‑line mode (`m`) directly in the pattern. - `(?im...)`: Enables
      case‑insensitivity (`i`) and multi‑line search (`m`).'
  - name: Apply the redaction (definition anchor)
    text: '`AnnotationRedaction` is a specialized rule that scans annotation objects
      and replaces matching text with a black rectangle. **Explanation:** - **Parameters:**
      The regex pattern tells the engine which text to target. - **Return Values:**
      This method modifies the document in place; no return value is'
  - name: Save the redacted document (definition anchor)
    text: '`Redactor.Save` writes the modified file to disk, preserving the original
      format unless you specify otherwise.'
  type: HowTo
- questions:
  - answer: Yes. Open the document with `Redactor(string path, string password)` and
      then apply your redaction rules as usual.
    question: Can I redact annotations in password‑protected PDFs?
  - answer: The API works on a copy in memory; the original file remains unchanged
      until you explicitly call `Save`.
    question: Does GroupDocs.Redaction modify the original file?
  - answer: All standard PDF annotation types—including comments, highlights, and
      sticky notes—are fully supported.
    question: How many annotation types are supported?
  - answer: Use `Redactor.GetRedactedDocument()` to retrieve an in‑memory stream and
      render it in your UI for a quick preview.
    question: Is there a way to preview redactions before saving?
  - answer: The library can handle files up to **2 GB**; larger files should be split
      before processing.
    question: What is the maximum file size I can process?
  type: FAQPage
title: GroupDocs.Redaction for .NET를 사용하여 주석을 삭제하는 방법
type: docs
url: /ko/net/annotation-redaction/redact-text-annotations-groupdocs-redaction-net/
weight: 1
---

# GroupDocs.Redaction for .NET을 사용하여 주석을 삭제하는 방법

If you need to **주석을 삭제하는 방법** in PDF or Word files, you’ve come to the right place. This guide walks you through installing GroupDocs.Redaction for .NET, configuring regex‑based annotation redaction, and optimizing performance for large‑scale workloads. By the end, you’ll be able to hide sensitive comments, notes, and other metadata with just a few lines of C# code.

## 빠른 답변
- **어떤 라이브러리가 주석 삭제를 처리합니까?** GroupDocs.Redaction for .NET.  
- **정규식을 사용할 수 있나요?** 예 – the API accepts full .NET regex syntax.  
- **개발에 라이선스가 필요합니까?** A free trial works for testing; a paid license is required for production.  
- **.NET 6 및 .NET Core와 호환됩니까?** Fully supported on .NET Framework 4.5+, .NET Core 3.1+, and .NET 6+.  
- **대용량 파일에서 삭제 속도는 어떻습니까?** Optimized patterns can process 500‑page PDFs in under 5 seconds on a typical server.

## 주석 삭제란 무엇입니까?
Annotation redaction permanently removes or obscures text that resides within document comments, notes, sticky notes, and other metadata objects. By erasing this hidden information, the technique guarantees that confidential data cannot be extracted or viewed, even when the file is distributed or opened in other applications, thereby maintaining privacy and compliance.

## PDF 주석에 삭제를 적용하는 이유는?
GroupDocs.Redaction supports **30개 이상의 문서 형식** and can handle files up to **2 GB** without loading the entire content into memory. Using built‑in regex engines reduces processing time by up to **70 %** compared with manual string searches, making it ideal for high‑volume legal or financial workflows.

## 사전 요구 사항

Before you begin, verify the following:

- **GroupDocs.Redaction** library (latest NuGet version).  
- A compatible **.NET** runtime (Framework 4.5+, .NET Core 3.1+, .NET 5/6).  
- An IDE such as **Visual Studio 2022** or **VS Code**.  
- Basic C# knowledge and familiarity with regular expressions.  

## GroupDocs.Redaction을 사용하여 주석을 삭제하는 방법?

Load your source document, define a regex pattern, apply an `AnnotationRedaction`, and save the result—all in a concise, three‑step flow. The following sections break each step down with clear explanations and the exact code placeholders you’ll replace with your own values.

### 1단계 – .NET CLI를 통해 라이브러리 설치
**답변:** Run `dotnet add package GroupDocs.Redaction` in your project folder; the CLI will download the latest stable package and update your project file automatically.  

```bash
dotnet add package GroupDocs.Redaction
```

### 2단계 – 패키지 관리자 콘솔을 통해 라이브러리 설치
**답변:** In Visual Studio’s Package Manager Console, execute `Install-Package GroupDocs.Redaction`; the command resolves dependencies and adds the reference to your project.  

```powershell
Install-Package GroupDocs.Redaction
```

### 3단계 – Redactor 초기화 (definition anchor)
The `Redactor` class is the core engine that loads a document and applies redaction rules.  

```csharp
using System;
using GroupDocs.Redaction.Redactions;

namespace DocumentRedaction
{
    class Program
    {
        static void Main(string[] args)
        {
            string sourceFile = @"YOUR_DOCUMENT_DIRECTORY\annotated.xlsx"; // Replace with actual document path.
            
            using (Redactor redactor = new Redactor(sourceFile))
            {
                // Your redaction logic will go here.
            }
        }
    }
}
```

## 주석 삭제 적용

### 1단계: Redactor 인스턴스 생성 (definition anchor)
`Redactor` is the entry point for all redaction operations; you pass the source file path to its constructor.  

```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // Further processing will occur here.
}
```

### 2단계: 정규식 정의 (definition anchor)
`Regex` is the .NET class that evaluates patterns; you can enable case‑insensitivity (`i`) and multi‑line mode (`m`) directly in the pattern.  

```csharp
string pattern = "(?im:john)";
```
- `(?im...)`: 대소문자 구분 없음(`i`) 및 다중 행 검색(`m`)을 활성화합니다.

### 3단계: 삭제 적용 (definition anchor)
`AnnotationRedaction` is a specialized rule that scans annotation objects and replaces matching text with a black rectangle.  

```csharp
redactor.Apply(new AnnotationRedaction(pattern));
```

**설명:**  
- **Parameters:** 정규식 패턴은 엔진에 대상 텍스트를 알려줍니다.  
- **Return Values:** 이 메서드는 문서를 제자리에서 수정하며, 반환값이 필요하지 않습니다.

### 4단계: 삭제된 문서 저장 (definition anchor)
`Redactor.Save` writes the modified file to disk, preserving the original format unless you specify otherwise.  

```csharp
guardedRedactor.Save();
```

## 일반적인 문제 및 해결책
- **일치 항목 없음:** Double‑check your regex syntax; use an online tester with the same .NET engine.  
- **파일 접근 오류:** Ensure the application has read/write permissions for the source and destination folders.  
- **성능 병목:** For documents larger than 500 pages, batch‑process them in parallel and reuse a single `Redactor` instance where possible.

## 자주 묻는 질문

**Q: 비밀번호로 보호된 PDF에서 주석을 삭제할 수 있나요?**  
A: Yes. Open the document with `Redactor(string path, string password)` and then apply your redaction rules as usual.

**Q: GroupDocs.Redaction이 원본 파일을 수정합니까?**  
A: The API works on a copy in memory; the original file remains unchanged until you explicitly call `Save`.

**Q: 지원되는 주석 유형은 몇 개입니까?**  
A: All standard PDF annotation types—including comments, highlights, and sticky notes—are fully supported.

**Q: 저장하기 전에 삭제를 미리 볼 수 있는 방법이 있나요?**  
A: Use `Redactor.GetRedactedDocument()` to retrieve an in‑memory stream and render it in your UI for a quick preview.

**Q: 처리할 수 있는 최대 파일 크기는 얼마입니까?**  
A: The library can handle files up to **2 GB**; larger files should be split before processing.

## FAQ 섹션

1. **GroupDocs.Redaction이란?**  
   - It's a .NET library for redacting sensitive information from various document formats.

2. **복잡한 주석을 어떻게 처리합니까?**  
   - Use advanced regular expressions and test them thoroughly before applying to critical documents.

3. **삭제를 되돌릴 수 있나요?**  
   - Once saved, changes are permanent; always back up your original files.

4. **기존 애플리케이션에 GroupDocs.Redaction을 통합할 수 있나요?**  
   - Yes, its API allows seamless integration with other .NET‑based systems.

5. **GroupDocs.Redaction이 지원하는 형식은 무엇입니까?**  
   - It supports a wide range of document types including Word, PDF, Excel, and more.

## 리소스

- [GroupDocs Redaction 문서](https://docs.groupdocs.com/redaction/net/)
- [API 레퍼런스](https://reference.groupdocs.com/redaction/net)
- [GroupDocs.Redaction 다운로드](https://releases.groupdocs.com/redaction/net/)
- [무료 지원 포럼](https://forum.groupdocs.com/c/redaction/33)
- [임시 라이선스 획득](https://purchase.groupdocs.com/temporary-license/) 

---

**마지막 업데이트:** 2026-05-27  
**테스트 환경:** GroupDocs.Redaction 23.10 for .NET  
**작성자:** GroupDocs

## 관련 튜토리얼

- [GroupDocs.Redaction for .NET을 사용하여 문서에서 주석을 효율적으로 제거하기](/redaction/net/annotation-redaction/remove-annotations-groupdocs-redaction-net/)
- [GroupDocs.Redaction .NET용 주석 삭제 튜토리얼](/redaction/net/annotation-redaction/)
- [GroupDocs.Redaction .NET을 사용하여 문서를 로드하고 삭제하는 방법: 완전 가이드](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)