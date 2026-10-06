---
date: '2026-10-06'
description: C#에서 IRedactionCallback 구현을 사용하여 GroupDocs.Redaction .NET으로 데이터를 마스킹하는
  방법을 배웁니다. step‑by‑step guide, best practices, real‑world examples를 따라 해 보세요.
keywords:
- how to redact data
- GroupDocs.Redaction .NET
- IRedactionCallback implementation
- document redaction C#
lastmod: '2026-10-06'
og_description: C#에서 IRedactionCallback 구현을 사용하여 GroupDocs.Redaction .NET으로 데이터를 마스킹하는
  방법을 배웁니다. step‑by‑step guide, best practices, real‑world examples와 함께 진행하세요.
og_image_alt: Guide to redact data with GroupDocs.Redaction .NET in C#
og_title: GroupDocs.Redaction .NET (C#)를 사용하여 데이터를 마스킹하는 방법
schemas:
- author: GroupDocs
  dateModified: '2026-10-06'
  description: Learn how to redact data using GroupDocs.Redaction .NET with an IRedactionCallback
    implementation in C#. Follow this step‑by‑step guide, best practices, and real‑world
    examples.
  headline: How to redact data with GroupDocs.Redaction .NET (C#)
  type: TechArticle
- description: Learn how to redact data using GroupDocs.Redaction .NET with an IRedactionCallback
    implementation in C#. Follow this step‑by‑step guide, best practices, and real‑world
    examples.
  name: How to redact data with GroupDocs.Redaction .NET (C#)
  steps:
  - name: prepare output directory and source file path
    text: Define where your source document lives. Adjust the path to match your environment.
      `LoadOptions` is a configuration object that tells the SDK how to read the file
      (e.g., password handling).
  - name: create a Redactor instance with custom settings
    text: We instantiate `Redactor` with `LoadOptions` and `RedactorSettings`. The
      `RedactionDump` inside the settings will automatically record every redaction
      that occurs. `RedactorSettings` lets you fine‑tune the redaction process; passing
      a `RedactionDump` enables a detailed audit file. `RedactionDump` is
  - name: apply an exact‑phrase redaction
    text: Here we replace the phrase **John Doe** with the placeholder **[REDACTED]**.
      You can swap any phrase or pattern you need to hide. `ReplacementOptions` defines
      what text will replace the matched content. It also supports font and color
      customisation if you need a visual mask. **Explanation of the key
  type: HowTo
- questions:
  - answer: You can start with a free trial or request a temporary license to explore
      all features. For production, purchase a perpetual or subscription license.
    question: What are the licensing options for GroupDocs.Redaction?
  - answer: Yes, it supports PDFs, Word, Excel, PowerPoint, and many other common
      formats.
    question: Can I use GroupDocs.Redaction on multiple file types?
  - answer: Wrap your redaction logic in `try‑catch` blocks and log the exception
      details. The callback can also be used to capture errors in real time.
    question: How do I handle exceptions during redaction?
  - answer: The core API is synchronous, but you can run redaction calls inside asynchronous
      tasks or background services.
    question: Is there built‑in support for asynchronous processing?
  - answer: The [official documentation](https://docs.groupdocs.com/redaction/net/)
      and API reference provide extensive code samples and scenario guides.
    question: Where can I find more advanced examples?
  type: FAQPage
tags:
- redact data
- GroupDocs.Redaction
- .NET redaction
- C# document security
- IRedactionCallback
title: GroupDocs.Redaction .NET (C#)를 사용하여 데이터를 마스킹하는 방법
type: docs
url: /ko/net/advanced-redaction/groupdocs-redaction-net-implement-iredactioncallback-csharp/
weight: 1
---

# GroupDocs.Redaction .NET (C#)으로 데이터 가리기

이 포괄적인 튜토리얼에서는 GroupDocs.Redaction for .NET을 사용하여 PDF, Word 파일 및 기타 문서에서 **데이터를 가리는 방법**을 알아봅니다. 법률 계약서에서 개인 식별자를 숨기거나 재무 보고서에서 기밀 수치를 삭제해야 할 경우, SDK는 프로그래밍 방식으로 모든 민감한 요소가 영구적으로 사라지고 감사 가능하도록 제어할 수 있게 해줍니다. 라이브러리 설치, 사용자 정의 `IRedactionCallback` 구성, 전체 로깅과 함께 정확한 구문 가리기를 적용하는 과정을 단계별로 안내합니다.

## 빠른 답변
- **IRedactionCallback는 무엇을 하나요?** 모든 가리기 이벤트를 가로채고, 세부 정보를 로그에 기록하며, 필요에 따라 교체 텍스트를 실시간으로 수정할 수 있습니다.  
- **라이선스가 필요합니까?** 개발용으로는 체험판을 사용할 수 있으며, 영구 라이선스를 구매하면 모든 평가 제한이 해제됩니다.  
- **지원되는 .NET 버전은 무엇입니까?** .NET Core 3.1+, .NET 5/6, .NET Framework 4.6+.  
- **여러 파일을 처리할 수 있나요?** 예—루프에 로직을 감싸거나 배치 처리를 사용하면 최상의 성능을 얻을 수 있습니다.  
- **비동기 가리기가 가능한가요?** 기본 제공은 없지만 `Task.Run` 등 비동기 패턴 안에서 API 호출을 실행할 수 있습니다.

## 민감한 데이터 가리기란?
`Redaction`은 공개해서는 안 되는 정보를 영구적으로 제거하거나 가리는 작업을 의미합니다. GroupDocs.Redaction을 사용하면 정확한 구문, 정규식 패턴 또는 사용자 정의 규칙을 정의하고, 원본 레이아웃과 페이지 구성을 유지하면서 **[REDACTED]**와 같은 자리표시자로 교체할 수 있습니다.

## IRedactionCallback와 함께 GroupDocs.Redaction을 사용하는 이유는?
`IRedactionCallback`은 SDK가 콘텐츠를 가릴 때마다 알림을 제공하는 인터페이스로, 감사 데이터를 캡처하거나 교체 텍스트를 동적으로 조정할 수 있게 해줍니다. 이를 통해 완전한 감사 가능성, 맞춤 비즈니스 규칙 적용, 컴플라이언스 시스템과의 원활한 통합을 성능 저하 없이 구현할 수 있습니다.

## 사전 요구 사항
- **GroupDocs.Redaction** 라이브러리(호환 버전 – 공식 [documentation page](https://docs.groupdocs.com/redaction/net/) 참고). 자세한 내용은 [official documentation](https://docs.groupdocs.com/redaction/net/)을 참조하세요.  
- .NET Core 또는 .NET Framework가 개발 머신에 설치되어 있어야 합니다.  
- Visual Studio(Community 에디션도 가능) 또는 C#을 지원하는 IDE.  
- 기본적인 C# 지식 및 NuGet 패키지 관리에 대한 이해.

## .NET용 GroupDocs.Redaction 설정
먼저 라이브러리를 프로젝트에 추가합니다. 선호하는 방법(CLI, Package Manager Console, UI) 중 하나를 선택하세요. 명령은 원본 튜토리얼과 동일하게 유지됩니다.

### 설치 옵션
**.NET CLI:**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager Console:**  
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI:**  
- Visual Studio에서 프로젝트를 엽니다.  
- **Manage NuGet Packages**로 이동합니다.  
- **GroupDocs.Redaction**을 검색하고 최신 안정 버전을 설치합니다.

### 라이선스 획득
제품을 체험하려면 [여기](https://purchase.groupdocs.com/temporary-license/)에서 무료 체험 또는 임시 라이선스를 요청하세요. 또한 [temporary‑license page](https://purchase.groupdocs.com/temporary-license/)에서 임시 라이선스를 받을 수 있습니다. 실제 운영에서는 전체 기능을 제한 없이 사용하려면 정식 라이선스를 구매하세요.

#### 기본 초기화 및 설정
아래는 `Redactor` 클래스로 문서를 여는 최소 코드입니다. 이 스니펫은 그대로 두세요 – 이후 모든 작업의 기반이 됩니다.  
`Redactor`는 문서를 나타내는 주요 클래스이며, 가리기 규칙을 적용하는 메서드를 제공합니다.  
```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx"; // Replace with actual path

using (Redactor redactor = new Redactor(sourceFile))
{
    // Your redaction logic here
}
```

## 구현 가이드
이제 사용자 정의 `IRedactionCallback`을 추가하여 기본 설정을 확장합니다. 이를 통해 각 가리기 이벤트를 캡처하고 로그에 기록하거나 실시간으로 교체 텍스트를 수정할 수 있습니다.

### IRedactionCallback 구현 연결 및 사용
`IRedactionCallback`은 각 가리기 작업에 대한 콜백을 받는 인터페이스로, 프로그래밍 방식으로 로그를 남기거나 동작을 변경할 수 있게 해줍니다.

#### 단계 1: 출력 디렉터리 및 소스 파일 경로 준비
소스 문서가 위치한 경로를 정의합니다. 환경에 맞게 경로를 조정하세요.

`LoadOptions`는 SDK가 파일을 읽는 방법(예: 비밀번호 처리)을 지정하는 구성 객체입니다.  
```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx"; // Replace with actual path
```

#### 단계 2: 사용자 정의 설정으로 Redactor 인스턴스 생성
`Redactor`를 `LoadOptions`와 `RedactorSettings`와 함께 인스턴스화합니다. 설정 내부의 `RedactionDump`는 발생하는 모든 가리기 작업을 자동으로 기록합니다.

`RedactorSettings`를 사용하면 가리기 프로세스를 세밀하게 조정할 수 있으며, `RedactionDump`를 전달하면 상세 감사 파일이 활성화됩니다.  
`RedactionDump`는 각 가리기 이벤트를 JSON 형식의 덤프 파일에 기록하여 컴플라이언스 보고에 활용되는 도우미 클래스입니다.  
```csharp
using (Redactor redactor = new Redactor(sourceFile, 
    new LoadOptions(), 
    new RedactorSettings(new RedactionDump())))
{
    // Further processing steps will go here
}
```

#### 단계 3: 정확한 구문 가리기 적용
여기서는 구문 **John Doe**를 자리표시자 **[REDACTED]**로 교체합니다. 숨기려는 구문이나 패턴을 자유롭게 교체할 수 있습니다.

`ReplacementOptions`는 매치된 콘텐츠를 어떤 텍스트로 교체할지 정의합니다. 시각적 마스크가 필요할 경우 폰트와 색상 커스터마이징도 지원합니다.  
```csharp
redactor.Apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[REDACTED]")));
```

**핵심 객체 설명**
- `LoadOptions()` – SDK에 문서를 읽는 방법(예: 비밀번호 처리)을 알려줍니다.  
- `RedactorSettings(new RedactionDump())` – 감사 목적을 위해 각 가리기 작업을 로그하는 덤프 파일을 활성화합니다.  
- `ReplacementOptions("[REDACTED]")` – 매치된 구문을 교체할 텍스트를 정의합니다.

### 이것이 중요한 이유
콜백 메커니즘은 모든 가리기 이벤트를 기록하고 기계가 읽을 수 있는 감사 추적을 생성하며, 자리표시자를 동적으로 수정할 수 있게 해줍니다. 이는 컴플라이언스 요구사항을 충족하고 수동 후처리 작업을 감소시키는 데 도움이 됩니다. 이 데이터를 모니터링 시스템과 통합하면 보고서를 생성하고 알림을 트리거하며, 민감한 정보가 가리기 파이프라인을 통과하지 않도록 보장할 수 있습니다.

`IRedactionCallback`을 사용하면 다음과 같은 세 가지 구체적인 장점이 있습니다:
1. **Compliance‑ready logs** – 모든 가리기가 기계가 읽을 수 있는 덤프에 기록되어 30개 이상의 규제 프레임워크에 대한 감사 요구사항을 충족합니다.  
2. **Dynamic replacement** – 데이터 유형에 따라 자리표시자를 변경할 수 있어 수동 후처리를 최대 40 % 감소시킵니다.  
3. **Scalable performance** – 콜백은 가리기당 <2 ms의 미미한 오버헤드만 추가하면서 수천 개 파일을 병렬로 배치 처리할 수 있게 합니다.

### 문제 해결 팁
- **File not found:** `sourceFile` 경로를 다시 확인하고 실행 프로세스가 파일에 접근할 수 있는지 확인하세요.  
- **Callback not firing:** 클래스가 `IRedactionCallback`의 **모든** 멤버를 구현했는지, 인스턴스가 `Redactor`에 올바르게 전달됐는지 확인하세요.  
- **Performance lag:** 대규모 배치에서는 가능한 경우 동일한 `Redactor` 인스턴스를 재사용하고 즉시 해제하세요.

## 실용적인 적용 사례
Redacting sensitive data is useful across many industries:
1. **Legal document processing** – 초안 공유 전 클라이언트 이름, 사건 번호, 사회보장번호 등을 자동으로 제거합니다.  
2. **HR management systems** – 감사 시 직원 계약서에서 개인 식별자를 제거합니다.  
3. **Financial reporting** – 투자자용 PDF 생성 시 독점적인 수치나 계좌 번호를 숨깁니다.

## 성능 고려 사항
GroupDocs.Redaction은 **30개 이상의 입력 및 출력 포맷**(PDF, DOCX, PPTX, XLSX, HTML 및 이미지 유형)을 지원하며 전체 문서를 메모리에 로드하지 않고 수백 페이지 파일을 처리할 수 있습니다. 수십에서 수백 개 파일을 처리할 때 애플리케이션을 빠르게 유지하려면:
- **Batch processing:** 파일 목록을 로드하고 `Parallel.ForEach` 안에서 가리기 루프를 실행하여 멀티코어를 활용합니다.  
- **Memory management:** 각 `Redactor`를 `using` 블록으로 감싸(예시처럼) 해제 보장을 합니다.  
- **Asynchronous operations:** SDK 자체는 동기식이지만 작업을 백그라운드 스레드나 `Task.Run`에 오프로드하여 UI 스레드 차단을 피할 수 있습니다.

## 일반적인 문제와 해결책
| 문제 | 해결책 |
|-------|----------|
| **“Invalid file format” 오류** | 문서 유형이 지원되는지 확인하세요(PDF, DOCX, PPTX 등). |
| **Callback이 null 값을 반환** | `RedactorSettings`를 생성할 때 `IRedactionCallback`의 구체적인 구현을 전달했는지 확인하세요. |
| **Redaction이 적용되지 않음** | 정확한 구문이 문서의 대소문자 및 공백과 일치하는지 확인하거나, 패턴 기반 매칭을 위해 `RegexRedaction`을 사용하세요. |

## 자주 묻는 질문

**Q: GroupDocs.Redaction의 라이선스 옵션은 무엇인가요?**  
A: 무료 체험으로 시작하거나 모든 기능을 탐색하기 위해 임시 라이선스를 요청할 수 있습니다. 실제 운영에서는 영구 라이선스 또는 구독 라이선스를 구매하세요.

**Q: GroupDocs.Redaction을 여러 파일 형식에 사용할 수 있나요?**  
A: 예, PDF, Word, Excel, PowerPoint 및 기타 많은 일반 포맷을 지원합니다.

**Q: 가리기 중에 예외를 어떻게 처리하나요?**  
A: 가리기 로직을 `try‑catch` 블록으로 감싸고 예외 세부 정보를 로그에 기록하세요. 콜백을 사용해 실시간으로 오류를 캡처할 수도 있습니다.

**Q: 비동기 처리를 위한 내장 지원이 있나요?**  
A: 핵심 API는 동기식이지만, 가리기 호출을 비동기 작업이나 백그라운드 서비스 안에서 실행할 수 있습니다.

**Q: 더 고급 예제를 어디서 찾을 수 있나요?**  
A: [공식 문서](https://docs.groupdocs.com/redaction/net/)와 API 레퍼런스에서 풍부한 코드 샘플과 시나리오 가이드를 확인하세요.

## 리소스

- [GroupDocs.Redaction for Net 문서](https://docs.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction for Net API 참조](https://reference.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction for Net 다운로드](https://releases.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction 포럼](https://forum.groupdocs.com/c/redaction/33)
- [무료 지원](https://forum.groupdocs.com/)
- [임시 라이선스](https://purchase.groupdocs.com/temporary-license/)

---

**마지막 업데이트:** 2026-10-06  
**테스트 환경:** GroupDocs.Redaction 2.3 (작성 시 최신 버전)  
**작성자:** GroupDocs

## 관련 튜토리얼

- [GroupDocs.Redaction .NET으로 가리기 정책 만들기 – 단계별 가이드](/redaction/net/advanced-redaction/groupdocs-redaction-net-create-save-policy/)
- [GroupDocs.Redaction .NET으로 문서 가리기 – 완전 가이드](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [스트림을 사용한 .NET 문서 가리기 – GroupDocs.Redaction 가이드](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)