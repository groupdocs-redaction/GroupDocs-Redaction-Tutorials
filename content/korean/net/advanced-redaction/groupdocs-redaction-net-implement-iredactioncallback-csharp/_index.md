---
date: '2026-03-30'
description: GroupDocs.Redaction .NET와 C#의 IRedactionCallback 구현을 사용하여 민감한 데이터를 마스킹하는
  방법을 배우세요. 단계별 가이드, 모범 사례 및 실제 예제.
keywords:
- GroupDocs.Redaction .NET
- Implementing IRedactionCallback
- secure document redaction
title: GroupDocs.Redaction .NET (C#)으로 민감한 데이터 가리기
type: docs
url: /ko/net/advanced-redaction/groupdocs-redaction-net-implement-iredactioncallback-csharp/
weight: 1
---

# GroupDocs.Redaction .NET (C#)으로 민감한 데이터 가리기

오늘날 디지털 환경에서 법률, 재무 또는 인사 문서에서 **민감한 데이터를 가리기**는 협상할 수 없는 요구사항입니다. 외부 검토를 위해 계약서를 준비하거나 공개 전에 보고서를 정리하든, 단 하나의 개인 식별자를 놓치면 규정 위반이 발생할 수 있습니다. .NET용 GroupDocs.Redaction은 모든 기밀 정보를 정확히 원하는 방식으로 사라지게 하는 강력하고 프로그래밍 가능한 방법을 제공합니다. 이 튜토리얼에서는 `IRedactionCallback` 구현을 연결하는 과정을 살펴보며, 가리기 워크플로를 사용자 정의하고 모든 단계에 대한 완전한 제어를 유지할 수 있습니다.

## 빠른 답변
- **IRedactionCallback는 무엇을 하나요?** 가리기 이벤트를 가로채고, 로그를 남기며, 실시간으로 동작을 수정할 수 있게 해줍니다.  
- **라이선스가 필요합니까?** 개발용으로는 체험판을 사용할 수 있으며, 영구 라이선스를 구매하면 모든 평가 제한이 해제됩니다.  
- **지원되는 .NET 버전은 무엇인가요?** .NET Core 3.1+, .NET 5/6, 그리고 .NET Framework 4.6+.  
- **여러 파일을 처리할 수 있나요?** 예—루프에 로직을 감싸거나 배치 처리를 사용하면 최고의 성능을 얻을 수 있습니다.  
- **비동기 가리기가 가능한가요?** 기본 제공은 아니지만 `Task.Run` 등 비동기 패턴 안에서 API 호출을 실행할 수 있습니다.

## 민감한 데이터를 가리기란?
가리기는 공개되어서는 안 되는 정보를 영구적으로 제거하거나 가리는 과정입니다. GroupDocs.Redaction을 사용하면 정확한 구문, 패턴 또는 사용자 정의 규칙을 정의하고, 원본 문서 레이아웃을 유지하면서 자리표시자(예: **[REDACTED]**)로 교체할 수 있습니다.

## IRedactionCallback와 함께 GroupDocs.Redaction을 사용하는 이유
- **전체 감사 가능성:** 콜백은 수행된 모든 가리기에 대한 상세 로그를 제공합니다.  
- **맞춤 처리:** 텍스트를 교체하고, 외부 서비스를 트리거하거나, 비즈니스 규칙을 동적으로 적용할 수 있습니다.  
- **확장 가능한 성능:** 콜백을 배치 처리와 결합하면 수천 개의 파일을 효율적으로 처리할 수 있습니다.

## 사전 요구 사항
Before we dive in, make sure you have:

- **GroupDocs.Redaction** 라이브러리(호환 버전 – 공식 [documentation page](https://docs.groupdocs.com/redaction/net/)를 참조).  
- 개발 머신에 .NET Core 또는 .NET Framework가 설치되어 있어야 합니다.  
- Visual Studio(Community 에디션도 가능) 또는 C#을 지원하는 IDE가 필요합니다.  
- 기본 C# 지식과 NuGet 패키지 관리에 대한 이해가 필요합니다.

## .NET용 GroupDocs.Redaction 설정
먼저 라이브러리를 프로젝트에 추가합니다. 선호하는 방법(CLI, Package Manager Console, UI) 중 하나를 선택하십시오. 명령은 원본 튜토리얼과 동일하게 유지됩니다.

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
제품을 체험하려면 [here](https://purchase.groupdocs.com/temporary-license/)에서 무료 체험 또는 임시 라이선스를 요청하십시오. 실제 사용을 위해서는 모든 기능을 제한 없이 이용할 수 있는 정식 라이선스를 구매하십시오.

#### 기본 초기화 및 설정
다음은 `Redactor` 클래스로 문서를 열기 위해 필요한 최소 코드입니다. 이 스니펫은 변경하지 마세요 – 이후 모든 작업의 기반이 됩니다.

```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx"; // Replace with actual path

using (Redactor redactor = new Redactor(sourceFile))
{
    // Your redaction logic here
}
```

## 구현 가이드
이제 기본 설정에 사용자 정의 `IRedactionCallback`을 추가하여 확장합니다. 이를 통해 각 가리기 이벤트를 캡처하고 로그에 기록하거나 실시간으로 교체 텍스트를 수정할 수 있습니다.

### IRedactionCallback 구현 연결 및 사용
다음 단계에서는 파일 경로 준비부터 정확한 구문 가리기 적용까지 전체 워크플로를 보여줍니다.

#### 단계 1: 출력 디렉터리 및 소스 파일 경로 준비
소스 문서가 위치한 경로를 정의합니다. 환경에 맞게 경로를 조정하십시오.

```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx"; // Replace with actual path
```

#### 단계 2: 사용자 정의 설정으로 Redactor 인스턴스 생성
`Redactor`를 `LoadOptions`와 `RedactorSettings`로 인스턴스화합니다. 설정 내부의 `RedactionDump`는 발생하는 모든 가리기를 자동으로 기록합니다.

```csharp
using (Redactor redactor = new Redactor(sourceFile, 
    new LoadOptions(), 
    new RedactorSettings(new RedactionDump())))
{
    // Further processing steps will go here
}
```

#### 단계 3: 정확한 구문 가리기 적용
여기서는 구문 **John Doe**를 자리표시자 **[REDACTED]**로 교체합니다. 숨겨야 할 구문이나 패턴은 자유롭게 교체할 수 있습니다.

```csharp
redactor.Apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[REDACTED]")));
```

**핵심 객체 설명:**  
- `LoadOptions()` – SDK에 문서를 어떻게 읽을지 알려줍니다(예: 비밀번호 처리).  
- `RedactorSettings(new RedactionDump())` – 감사 목적을 위해 각 가리기를 로그하는 덤프 파일을 활성화합니다.  
- `ReplacementOptions("[REDACTED]")` – 일치하는 구문을 교체할 텍스트를 정의합니다.

### 이것이 중요한 이유
`IRedactionCallback`를 사용하면 다음과 같은 사용자 정의 로직을 연결할 수 있습니다:
- 가리기 세부 정보를 컴플라이언스 데이터베이스에 전송합니다.  
- 단순 구문 교체로 다루지 못하는 추가 메타데이터를 마스킹합니다.  
- 콘텐츠 유형에 따라 교체 텍스트를 동적으로 선택합니다.

### 문제 해결 팁
- **File not found:** `sourceFile` 경로를 다시 확인하고 파일이 실행 프로세스에서 접근 가능한지 확인하십시오.  
- **Callback not firing:** 클래스가 `IRedactionCallback`의 **all** 멤버를 구현했는지, 그리고 인스턴스가 `Redactor`에 올바르게 전달되었는지 확인하십시오.  
- **Performance lag:** 대량 배치의 경우 가능한 한 동일한 `Redactor` 인스턴스를 재사용하고 즉시 해제하십시오.

## 실용적인 적용 사례
민감한 데이터 가리기는 다양한 산업에서 유용합니다:
1. **Legal Document Processing** – 초안 공유 전에 클라이언트 이름, 사건 번호, 사회보장번호 등을 자동으로 제거합니다.  
2. **HR Management Systems** – 감사 중에 직원 계약서에서 개인 식별자를 제거합니다.  
3. **Financial Reporting** – 투자자용 PDF를 생성할 때 독점적인 수치나 계좌 번호를 숨깁니다.

## 성능 고려 사항
수십 개 또는 수백 개의 파일을 처리할 때 애플리케이션이 빠르게 동작하도록 하려면:
- **Batch Processing:** 파일 목록을 로드하고 `Parallel.ForEach` 내부에서 가리기 루프를 실행하여 멀티코어를 활용합니다.  
- **Memory Management:** 각 `Redactor`를 `using` 블록으로 감싸(예시와 같이) 해제가 보장되도록 합니다.  
- **Asynchronous Operations:** SDK 자체는 동기식이지만 작업을 백그라운드 스레드나 `Task.Run`에 오프로드하여 UI 스레드 차단을 방지할 수 있습니다.

## 일반적인 문제와 해결책
| 문제 | 해결책 |
|-------|----------|
| **“Invalid file format” error** | 문서 유형이 지원되는지 확인하십시오(PDF, DOCX, PPTX 등). |
| **Callback receives null values** | `RedactorSettings`를 구성할 때 `IRedactionCallback`의 구체적인 구현을 전달하고 있는지 확인하십시오. |
| **Redaction not applied** | 정확한 구문이 문서의 대소문자 및 공백과 일치하는지 확인하거나, 패턴 기반 매칭을 위해 `RegexRedaction`을 사용하십시오. |

## 자주 묻는 질문
**Q: GroupDocs.Redaction의 라이선스 옵션은 무엇인가요?**  
A: 무료 체험으로 시작하거나 모든 기능을 탐색하기 위해 임시 라이선스를 요청할 수 있습니다. 실제 사용을 위해서는 영구 라이선스 또는 구독 라이선스를 구매하십시오.

**Q: GroupDocs.Redaction을 여러 파일 형식에 사용할 수 있나요?**  
A: 예, PDF, Word, Excel, PowerPoint 등 다양한 일반 형식을 지원합니다.

**Q: 가리기 중 예외를 어떻게 처리합니까?**  
A: `try‑catch` 블록으로 가리기 로직을 감싸고 예외 세부 정보를 로그에 기록하십시오. 콜백을 사용하여 실시간으로 오류를 포착할 수도 있습니다.

**Q: 비동기 처리를 위한 기본 지원이 있나요?**  
A: 핵심 API는 동기식이지만 비동기 작업이나 백그라운드 서비스 내에서 가리기 호출을 실행할 수 있습니다.

**Q: 더 고급 예제를 어디서 찾을 수 있나요?**  
A: [공식 문서](https://docs.groupdocs.com/redaction/net/)와 API 레퍼런스에서 풍부한 코드 샘플과 시나리오 가이드를 제공합니다.

## 리소스
- [GroupDocs.Redaction for Net 문서](https://docs.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction for Net API 레퍼런스](https://reference.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction for Net 다운로드](https://releases.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction 포럼](https://forum.groupdocs.com/c/redaction/33)
- [무료 지원](https://forum.groupdocs.com/)
- [임시 라이선스](https://purchase.groupdocs.com/temporary-license/)

---

**마지막 업데이트:** 2026-03-30  
**테스트 환경:** GroupDocs.Redaction 2.3 (latest at time of writing)  
**작성자:** GroupDocs