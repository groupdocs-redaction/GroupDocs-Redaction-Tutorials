---
date: '2026-10-06'
description: GroupDocs.Redaction .NET를 사용하여 민감한 데이터를 마스킹하는 방법을 배웁니다. 이 단계별 가이드는 마스킹
  정책을 XML로 생성, 적용 및 저장하는 방법을 보여줍니다.
keywords:
- redact sensitive data
- mask confidential information
- groupdocs redaction .net
lastmod: '2026-10-06'
og_description: GroupDocs.Redaction .NET를 사용하여 민감한 데이터를 마스킹하는 방법을 배웁니다. 이 단계별 가이드는
  마스킹 정책을 XML로 생성, 적용 및 저장하는 방법을 보여줍니다.
og_image_alt: Tutorial showing how to redact sensitive data in documents with GroupDocs.Redaction
  for .NET
og_title: GroupDocs.Redaction .NET를 사용하여 민감한 데이터를 마스킹하는 방법
schemas:
- author: GroupDocs
  dateModified: '2026-10-06'
  description: Learn how to redact sensitive data with GroupDocs.Redaction .NET. This
    step‑by‑step guide shows you how to create, apply, and save a redaction policy
    as XML.
  headline: How to redact sensitive data using GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to redact sensitive data with GroupDocs.Redaction .NET. This
    step‑by‑step guide shows you how to create, apply, and save a redaction policy
    as XML.
  name: How to redact sensitive data using GroupDocs.Redaction .NET
  steps:
  - name: prepare your document directory
    text: '*Replace `"YOUR_DOCUMENT_DIRECTORY"` with the folder that holds the documents
      you want to protect.*'
  - name: load the document
    text: The `Redactor` object opens the file and manages its lifecycle.
  - name: define the redactions
    text: 'ExactPhraseRedaction defines a rule that replaces a specific phrase, while
      `RegexRedaction` uses a regular expression to match patterns. Here we create
      two rules: 1. **ExactPhraseRedaction** – replaces a known phrase with “[REDACTED]”.
      2. **RegexRedaction** – finds dates in `YYYY‑MM‑DD` format and r'
  - name: apply the redactions
    text: All defined rules are executed against the opened document in one pass.
  - name: save the policy as an XML file
    text: The XML file stores the redaction definitions, allowing you to reuse the
      same policy without rewriting code.
  type: HowTo
- questions:
  - answer: Yes—use `redactor.LoadPolicy("policy.xml")` to import a previously saved
      policy.
    question: Can I load an existing XML policy instead of building one programmatically?
  - answer: 'Absolutely. Pass the password to the `Redactor` constructor: `new Redactor(sourceFile,
      "password")`.'
    question: Does GroupDocs.Redaction support password‑protected PDFs?
  - answer: The SDK provides `ImageRedaction` and `MetadataRedaction` classes for
      those scenarios.
    question: Is it possible to redact images or metadata?
  - answer: Process them in chunks or use the streaming API to reduce memory footprint;
      the engine can handle files up to 2 GB without loading the whole file into RAM.
    question: How do I handle large documents (hundreds of MB)?
  - answer: A paid license is required for production deployments; a trial license
      is fine for development and testing.
    question: What licensing model is required for commercial use?
  type: FAQPage
tags:
- redact sensitive data
- groupdocs redaction
- .net document security
- xml policy
- document redaction
title: GroupDocs.Redaction .NET를 사용하여 민감한 데이터를 마스킹하는 방법
type: docs
url: /ko/net/advanced-redaction/groupdocs-redaction-net-create-save-policy/
weight: 1
---

# GroupDocs.Redaction .NET을 사용하여 민감한 데이터 가리기 방법

계약서, 재무제표 또는 환자 기록과 같은 기밀 정보를 보호하는 것은 현대 애플리케이션에 있어 절대 양보할 수 없는 요구사항입니다. 이 가이드에서는 GroupDocs.Redaction for .NET을 사용하여 **민감한 데이터를 가리는 방법**을 배우게 됩니다. SDK 설치부터 모든 문서 유형에 적용할 수 있는 재사용 가능한 XML 정책 정의까지 다룹니다.

## 빠른 답변
- **“create redaction policy”(정책 생성)란 무엇인가요?** 이는 GroupDocs.Redaction에 기밀 내용을 숨기거나 교체하도록 지시하는 규칙(텍스트, 정규식, 이미지 등)을 정의하는 과정입니다.  
- **어떤 라이브러리가 필요합니까?** GroupDocs.Redaction for .NET, NuGet을 통해 제공됩니다.  
- **라이선스가 필요합니까?** 개발에는 무료 체험판을 사용할 수 있으며, 운영 환경에서는 영구 라이선스가 필요합니다.  
- **정책을 재사용할 수 있나요?** 예—XML로 저장하면 나중에 로드하여 모든 문서에 적용할 수 있습니다.  
- **지원되는 .NET 버전은 무엇인가요?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## 레드액션 정책이란?

레드액션 정책은 제거하거나 교체해야 할 *무엇*과 교체된 내용이 어떻게 표시될지를 지정하는 규칙들의 모음입니다. 정책을 한 번 만들면 애플리케이션이 처리하는 모든 문서에 일관된 보안 표준을 적용할 수 있습니다.

## 레드액션 정책은 어떻게 작동하나요?

`Redactor` 엔진으로 문서를 로드하고 하나 이상의 레드액션 규칙을 첨부한 뒤 `Apply`를 호출합니다. 엔진은 문서를 스캔하여 일치하는 내용을 마스킹하고, 선택적으로 새로운 파일을 출력합니다. 동일한 규칙 집합을 XML로 내보낼 수 있어 코드를 다시 컴파일하지 않고도 정책을 재사용할 수 있습니다.

## 레드액션 정책을 만들 때 GroupDocs.Redaction을 사용하는 이유는?

GroupDocs.Redaction은 레드액션 정책의 생성, 관리 및 실행을 단순화하는 포괄적인 기능을 제공하여 다양한 문서 유형에 걸쳐 일관된 데이터 보호를 보장하고, 높은 성능과 기존 .NET 애플리케이션에 대한 손쉬운 통합을 제공함으로써 팀과 조직에 적합합니다.

- **광범위한 포맷 지원** – SDK는 PDF, DOCX, XLSX, PPTX 및 이미지 포맷을 포함한 30개 이상의 파일 형식을 처리하며, 전체 파일을 메모리에 로드하지 않고도 최대 2 GB까지 처리할 수 있습니다.  
- **프로그래밍 정밀도** – 숨겨야 할 데이터만을 대상으로 정확한 구문, 정규식 또는 사용자 정의 로직을 정의합니다.  
- **재사용 가능한 XML 정책** – 규칙을 한 번 내보내어 팀, 서비스 또는 마이크로서비스 간에 공유할 수 있습니다.  
- **성능 최적화 엔진** – 이 라이브러리는 일반 서버 하드웨어에서 수백 페이지 문서를 1초 미만에 처리하여 고처리량 파이프라인에 적합합니다.

## 사전 요구 사항
- .NET 런타임과 호환되는 GroupDocs.Redaction 라이브러리.  
- C#를 지원하는 Visual Studio, VS Code 또는 기타 IDE.  
- C# 및 .NET 프로젝트 구조에 대한 기본적인 이해.

## GroupDocs.Redaction for .NET 설정

먼저, 프로젝트에 라이브러리를 추가합니다.

**.NET CLI 사용**  
```bash
dotnet add package GroupDocs.Redaction
```  

**패키지 관리자 사용**  
```powershell
Install-Package GroupDocs.Redaction
```  

또는 NuGet 패키지 관리자 UI에서 “GroupDocs.Redaction”을 검색하고 거기서 설치합니다.

### 라이선스 획득
- 기능을 살펴보기 위해 **무료 체험**으로 시작합니다.  
- 장기 테스트를 위해 **임시 라이선스**를 요청하고, 이후 프로덕션 사용을 위해 정식 라이선스를 구매합니다.

### 기본 초기화
소스 파일에 네임스페이스를 추가합니다:

`Redactor` 클래스는 문서를 로드하고 레드액션 규칙을 적용하는 핵심 엔진입니다.  
```csharp
using GroupDocs.Redaction;
```  

`Redactor` 클래스는 GroupDocs.Redaction의 핵심 엔진으로, 문서를 로드하고 레드액션 규칙을 적용합니다.

## 단계별 레드액션 정책 만들기

아래는 레드액션 정책을 프로그래밍 방식으로 구축하고, 규칙을 구성하며, 문서에 적용하고, 최종적으로 정책을 XML 파일로 저장하여 향후 재사용할 수 있도록 하는 전체 워크스루이며, 여러 프로젝트와 문서 유형에 걸쳐 일관된 레드액션을 보장합니다.

### 단계 1: 문서 디렉터리 준비
```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
```  
*`"YOUR_DOCUMENT_DIRECTORY"`를 보호하려는 문서가 들어 있는 폴더 경로로 교체하세요.*

### 단계 2: 문서 로드
```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // Further code will go here
}
```  
`Redactor` 객체는 파일을 열고 그 수명 주기를 관리합니다.

### 단계 3: 레드액션 정의
ExactPhraseRedaction은 특정 구문을 교체하는 규칙을 정의하고, `RegexRedaction`은 정규식을 사용해 패턴을 매칭합니다.  
```csharp
var redactions = new List<Redaction>
{
    new ExactPhraseRedaction("Sensitive Phrase", new ReplacementOptions("[REDACTED]")),
    new RegexRedaction(@"\d{4}-\d{2}-\d{2}", new ReplacementOptions("[DATE REDACTED]"))
};
```  
여기서 두 개의 규칙을 생성합니다:  
1. **ExactPhraseRedaction** – 알려진 구문을 “[REDACTED]”로 교체합니다.  
2. **RegexRedaction** – `YYYY‑MM‑DD` 형식의 날짜를 찾아 “[DATE REDACTED]”로 교체합니다.

### 단계 4: 레드액션 적용
```csharp
redactor.Apply(redactions);
```  
정의된 모든 규칙이 열린 문서에 한 번에 실행됩니다.

### 단계 5: 정책을 XML 파일로 저장
```csharp
string policyFile = "policy.xml";
redactor.SavePolicy(policyFile, new SaveOptions());
```  
XML 파일은 레드액션 정의를 저장하여 코드를 다시 작성하지 않고도 동일한 정책을 재사용할 수 있게 합니다.

## 실용적인 적용 사례

- **법률 사무소**는 초안을 공유하기 전에 사건 번호와 고객 이름을 가릴 수 있습니다.  
- **재무 부서**는 보고서에서 계좌 번호나 거래 날짜를 마스킹합니다.  
- **보건 의료 제공자**는 환자 식별자를 제거하여 HIPAA 준수를 보장합니다.

## 성능 팁

- **한 번에 하나의 문서**만 열어 메모리 사용량을 낮게 유지합니다.  
- **효율적인 정규식**을 작성하세요; 처리 시간을 늘리는 과도하게 포괄적인 패턴은 피합니다.  
- 라이브러리를 **최신 상태**로 유지하여 성능 향상 및 새로운 레드액션 유형의 혜택을 받으세요.

## 일반적인 문제와 해결책

| Issue | Why it happens | How to fix |
|-------|----------------|------------|
| **디렉터리 준비 중 IO 예외** | 잘못된 경로나 쓰기 권한이 없음 | 폴더가 존재하고 애플리케이션에 읽기/쓰기 권한이 있는지 확인합니다. |
| **Regex가 예상 텍스트와 일치하지 않음** | 패턴이 너무 엄격하거나 이스케이프 문자가 누락됨 | 온라인 테스트 도구로 정규식을 테스트하고, 수량자나 특수 문자를 이스케이프하도록 조정합니다. |
| **정책 파일이 생성되지 않음** | `SavePolicy`가 레드액션 적용 전에 호출되었거나 잘못된 경로를 사용함 | 출력 디렉터리가 쓰기 가능한지 확인하고 `Apply` 후에 `SavePolicy`를 호출합니다. |

## 자주 묻는 질문

**Q: 프로그래밍 방식으로 정책을 만들지 않고 기존 XML 정책을 로드할 수 있나요?**  
A: 예—`redactor.LoadPolicy("policy.xml")`를 사용하여 이전에 저장된 정책을 가져옵니다.

**Q: GroupDocs.Redaction이 비밀번호로 보호된 PDF를 지원하나요?**  
A: 물론입니다. 비밀번호를 `Redactor` 생성자에 전달합니다: `new Redactor(sourceFile, "password")`.

**Q: 이미지나 메타데이터를 가릴 수 있나요?**  
A: SDK는 이러한 시나리오를 위해 `ImageRedaction` 및 `MetadataRedaction` 클래스를 제공합니다.

**Q: 수백 MB 규모의 대용량 문서는 어떻게 처리하나요?**  
A: 문서를 청크로 처리하거나 스트리밍 API를 사용해 메모리 사용량을 줄이세요; 엔진은 전체 파일을 RAM에 로드하지 않고도 최대 2 GB 파일을 처리할 수 있습니다.

**Q: 상업적 사용을 위한 라이선스 모델은 무엇인가요?**  
A: 프로덕션 배포에는 유료 라이선스가 필요하며, 개발 및 테스트에는 체험 라이선스로 충분합니다.

## 결론

이제 GroupDocs.Redaction for .NET을 사용해 모든 문서에 적용할 수 있는 완전하고 재사용 가능한 **레드액션 정책**을 갖추었습니다. 정책을 XML로 내보내면 향후 업데이트가 간편해지고 조직 전체에 일관된 데이터 보호를 보장합니다.

### 다음 단계
- `ImageRedaction` 또는 `MetadataRedaction`과 같은 추가 레드액션 유형을 실험해 보세요.  
- 정책 로드 로직을 문서 관리 워크플로에 통합하여 자동 레드액션을 구현합니다.  
- 고급 커스터마이징을 위해 **GroupDocs.Redaction** API 레퍼런스를 살펴보세요.

---

**마지막 업데이트:** 2026-10-06  
**테스트 환경:** GroupDocs.Redaction 5.8 for .NET  
**작성자:** GroupDocs  

**리소스**  
- [문서](https://docs.groupdocs.com/redaction/net/)  
- [API 레퍼런스](https://reference.groupdocs.com/redaction/net)  
- [다운로드](https://releases.groupdocs.com/redaction/net/)  
- [무료 지원 포럼](https://forum.groupdocs.com/c/redaction/33)  
- [임시 라이선스 신청](https://purchase.groupdocs.com/temporary-license/)

## 관련 튜토리얼

- [GroupDocs.Redaction .NET (C#)으로 민감한 데이터 가리기](/redaction/net/advanced-redaction/groupdocs-redaction-net-implement-iredactioncallback-csharp/)
- [GroupDocs.Redaction .NET을 사용한 문서 레드액션 구현&#58; 단계별 가이드](/redaction/net/getting-started/implement-document-redaction-groupdocs-redaction-net/)
- [GroupDocs.Redaction .NET으로 문서 가리기 – 완전 가이드](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)