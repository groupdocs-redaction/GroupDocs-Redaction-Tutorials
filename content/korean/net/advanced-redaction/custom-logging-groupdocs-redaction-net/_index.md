---
date: '2026-10-01'
description: GroupDocs.Redaction for .NET에서 custom logger c#를 구현하는 방법을 배우고, 상세한 custom
  logging을 가능하게 하며, 규정 준수 보고를 더 쉽게 할 수 있습니다.
keywords:
- custom logger c#
- implement custom logger
- save redacted document
- custom logger .net core
- log warnings c#
lastmod: '2026-10-01'
og_description: GroupDocs.Redaction for .NET에서 custom logger c#를 구현하여 상세 로그를 캡처하고,
  래스터화 없이 편집된 문서를 저장하며, 규정 준수 요구사항을 충족합니다.
og_image_alt: Guide showing how to add a custom logger to GroupDocs.Redaction in a
  .NET application
og_title: GroupDocs.Redaction for .NET에서 custom logger c# 구현
schemas:
- author: GroupDocs
  dateModified: '2026-10-01'
  description: Learn how to implement a custom logger c# in GroupDocs.Redaction for
    .NET, enabling detailed custom logging .net and easier compliance reporting.
  headline: Implement custom logger c# in GroupDocs.Redaction for .NET
  type: TechArticle
- description: Learn how to implement a custom logger c# in GroupDocs.Redaction for
    .NET, enabling detailed custom logging .net and easier compliance reporting.
  name: Implement custom logger c# in GroupDocs.Redaction for .NET
  steps:
  - name: Define a custom logger class (log warnings c#)
    text: The `CustomLogger` class implements `ILogger`. CustomLogger is a user‑defined
      class that implements the `ILogger` interface to capture redaction events. **Definition
      anchor:** `CustomLogger` is a user‑defined implementation of the `ILogger` interface
      that records redaction events. **Explanation:** T
  - name: Prepare file paths and open the source document
    text: '**Definition anchor:** `Redactor` is the primary class in GroupDocs.Redaction
      that performs redaction operations on a PDF document. **Why this matters:**
      Using utility methods keeps your code clean and guarantees the output folder
      exists before you attempt to **save redacted document**.'
  - name: Apply redactions while using the custom logger
    text: '**Direct answer:** The redaction workflow starts by creating a `Redactor`
      instance with `RedactorSettings(logger)`, then applying redaction objects, checking
      `logger.HasErrors`, and finally calling `redactor.Save` with rasterization disabled.
      This pattern ensures every step is logged and that you on'
  type: HowTo
- questions:
  - answer: Custom logging captures detailed redaction events, satisfies audit requirements,
      and simplifies troubleshooting by exposing errors and warnings in real time.
    question: What is the purpose of custom logging with GroupDocs.Redaction?
  - answer: Implement `LogError` in your `CustomLogger` class; the `HasErrors` flag
      lets you abort processing if a critical issue is detected.
    question: How do I handle errors using a custom logger?
  - answer: Yes—you can forward log messages to CRM, ERP, or centralized monitoring
      tools by extending the logger methods.
    question: Can custom logging be integrated with other systems?
  - answer: Missing method overrides, forgetting to pass `RedactorSettings(logger)`,
      and insufficient file permissions are the most frequent issues.
    question: What are common pitfalls when implementing custom logging?
  - answer: Detailed logs provide real‑time visibility, streamline debugging, and
      generate the audit trails required by regulations such as GDPR and HIPAA.
    question: How does custom logging improve document redaction workflows?
  type: FAQPage
tags:
- custom logger
- GroupDocs.Redaction
- .NET logging
- document redaction
title: GroupDocs.Redaction for .NET에서 custom logger c# 구현
type: docs
url: /ko/net/advanced-redaction/custom-logging-groupdocs-redaction-net/
weight: 1
---

# GroupDocs.Redaction for .NET에서 사용자 정의 로거 c# 구현

문서 레드액션을 효율적으로 관리하는 것은 특히 민감한 정보를 다룰 때 중요합니다. 이 가이드에서는 GroupDocs.Redaction for .NET을 사용하여 **custom logger c# 구현 방법**을 배우게 되며, 로깅, 오류 처리 및 감사 추적을 완벽히 제어할 수 있습니다. 튜토리얼이 끝날 때까지 경고, 오류 및 정보 메시지를 캡처하고, 로거를 기존 .NET 로깅 프레임워크와 통합하며, 레드액션된 문서를 래스터화 없이 저장할 수 있게 됩니다.

## 빠른 답변
- **custom logger c#는 무엇을 하나요?** 레드액션 중에 오류, 경고 및 정보 메시지를 캡처하여 검색 가능한 감사 추적을 제공합니다.  
- **ILogger 인터페이스를 제공하는 라이브러리는 무엇인가요?** GroupDocs.Redaction for .NET이 `ILogger` 인터페이스를 제공합니다.  
- **레드액션된 문서를 래스터화 없이 저장할 수 있나요?** 예 – `redactor.Save(..., new Options.RasterizationOptions { Enabled = false })`를 호출합니다.  
- **프로덕션 사용에 라이선스가 필요합니까?** 프로덕션에는 정식 라이선스가 필요하며, 평가용으로 체험 라이선스를 사용할 수 있습니다.  
- **이 접근 방식이 .NET Core / .NET 6+와 호환되나요?** 물론입니다 – 동일한 API가 .NET Framework, .NET Core, .NET 5 및 .NET 6 전반에서 작동합니다.

## custom logger c#란 무엇인가요?

**custom logger c#**는 GroupDocs.Redaction에서 제공하는 `ILogger` 인터페이스를 구현하는 클래스입니다. 콘솔, 파일, 데이터베이스 또는 외부 모니터링 시스템 등 필요한 곳으로 로그 메시지를 전달할 수 있게 하며, 전체 레드액션 워크플로우를 명확히 파악할 수 있습니다.

## GroupDocs.Redaction과 함께 .net 사용자 정의 로깅을 사용하는 이유는?

규제 감사 요구를 충족하고 문제 해결 속도를 높이는 상세하고 검색 가능한 로그로 레드액션 프로세스를 강화하세요. GroupDocs.Redaction은 **70개 이상의 입력 및 출력 형식**을 지원하며 전체 파일을 메모리에 로드하지 않고도 최대 500페이지 문서를 처리할 수 있으므로, 잘 설계된 로거는 거의 부하를 추가하지 않으면서도 귀중한 가시성을 제공합니다.

## 전제 조건
- GroupDocs.Redaction for .NET이 설치됨 (**Installation** 섹션을 아래에서 참조).  
- .NET 개발 환경 (Visual Studio, VS Code 또는 .NET CLI).  
- 기본 C# 지식 및 파일 스트림에 대한 이해.  

## 설치

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
**"GroupDocs.Redaction"**을 검색하고 최신 버전을 설치합니다.

## 라이선스 획득
- **Free trial:** 임시 라이선스로 API를 테스트합니다.  
- **Temporary license:** 제한된 기간 동안 전체 기능에 접근합니다.  
- **Purchase:** 프로덕션 배포를 위한 영구 라이선스를 획득합니다.

## 단계별 가이드

### .NET Core에서 custom logger를 구현하는 방법은?

`CustomLogger` 클래스를 .NET Core 프로젝트에 로드하고 `RedactorSettings`에 연결합니다. 로거는 .NET Framework, .NET 5 및 .NET 6에서도 동일하게 작동하므로 모든 플랫폼에서 동일한 코드를 공유할 수 있습니다.

### 단계 1: 사용자 정의 로거 클래스 정의 (log warnings c#)

`CustomLogger` 클래스는 `ILogger`를 구현합니다.  
CustomLogger는 레드액션 이벤트를 캡처하기 위해 `ILogger` 인터페이스를 구현하는 사용자 정의 클래스입니다.  
```csharp
using System;
using GroupDocs.Redaction;

class CustomLogger : ILogger
{
    public bool HasErrors { get; private set; }

    // Log errors encountered during processing.
    public void LogError(string message)
    {
        Console.WriteLine("Error: " + message);
        HasErrors = true;
    }

    // Log warnings that may not be critical but need attention.
    public void LogWarning(string message)
    {
        Console.WriteLine("Warning: " + message);
    }

    // Log informational messages for tracking normal operations.
    public void LogInfo(string message)
    {
        Console.WriteLine("Info: " + message);
    }
}
```  

**Definition anchor:** `CustomLogger`는 레드액션 이벤트를 기록하는 `ILogger` 인터페이스의 사용자 정의 구현입니다.  
**Explanation:** `HasErrors` 플래그는 처리를 계속할지 여부를 결정하는 데 도움이 됩니다. 세 메서드는 대부분의 레드액션 시나리오에서 필요한 세 가지 로그 레벨에 해당합니다.

### 단계 2: 파일 경로를 준비하고 소스 문서를 엽니다

```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
string outputFile = Utils.GetOutputFile(sourceFile);
```  

**Definition anchor:** `Redactor`는 PDF 문서에 레드액션 작업을 수행하는 GroupDocs.Redaction의 주요 클래스입니다.  
**Why this matters:** 유틸리티 메서드를 사용하면 코드가 깔끔해지고 **레드액션된 문서 저장**을 시도하기 전에 출력 폴더가 존재함을 보장합니다.

### 단계 3: 사용자 정의 로거를 사용하면서 레드액션 적용

```csharp
using (Stream stream = File.Open(sourceFile, FileMode.Open, FileAccess.ReadWrite))
{
    var logger = new CustomLogger();
    
    using (Redactor redactor = new Redactor(stream, new LoadOptions(), new RedactorSettings(logger)))
    {
        // Apply a redaction to the document.
        redactor.Apply(new DeleteAnnotationRedaction());
        
        if (!logger.HasErrors)
        {
            using (Stream streamOut = File.Open(outputFile, FileMode.OpenOrCreate, FileAccess.ReadWrite))
            {
                // Save changes without rasterizing the output.
                redactor.Save(streamOut, new Options.RasterizationOptions { Enabled = false });
            }
        }
    }
}
```  

**Direct answer:** 레드액션 워크플로우는 `RedactorSettings(logger)`를 사용하여 `Redactor` 인스턴스를 생성하고, 레드액션 객체를 적용한 뒤 `logger.HasErrors`를 확인하며, 마지막으로 래스터화를 비활성화한 상태로 `redactor.Save`를 호출하는 것으로 시작합니다. 이 패턴은 모든 단계가 로그에 기록되고 오류가 없을 때만 깨끗한 문서를 저장하도록 보장합니다.  

**설명:**  
1. `Redactor`는 `RedactorSettings(logger)`로 인스턴스화되어 `CustomLogger`와 연결됩니다.  
2. 레드액션을 적용한 후, 코드는 `logger.HasErrors`를 확인합니다. 오류가 없으면 문서를 저장합니다—래스터화 없이 **save redacted document** 로직을 보여줍니다.

## 일반적인 함정 및 문제 해결
- **Missing log output:** 각 `Log*` 메서드가 올바르게 오버라이드되었는지 확인합니다.  
- **File access exceptions:** 애플리케이션이 소스 및 출력 경로 모두에 대한 읽기/쓰기 권한을 가지고 있는지 확인합니다.  
- **Logger not wired:** `RedactorSettings(logger)` 매개변수는 필수이며, 이를 생략하면 사용자 정의 로깅이 비활성화됩니다.

## 실용적인 적용 사례
1. **Compliance reporting:** 로그 항목을 CSV 또는 데이터베이스로 내보내어 감사 추적을 생성합니다.  
2. **Error tracking:** `LogError` 출력을 스캔하여 문제 파일을 빠르게 찾습니다.  
3. **Workflow automation:** `LogWarning`가 호출될 때 하위 프로세스(예: 컴플라이언스 담당자 알림)를 트리거합니다.

## 성능 고려 사항
- **Dispose streams promptly** 메모리를 해제하기 위해 스트림을 즉시 폐기합니다, 특히 대량 배치를 처리할 때.  
- **Monitor CPU & memory** 대량 레드액션 중에 CPU 및 메모리를 모니터링하고, 로거 동기화를 신중히 하여 문서를 병렬 처리하는 것을 고려합니다.  
- **Stay updated:** 최신 GroupDocs.Redaction 버전은 종종 성능 최적화 및 추가 로깅 훅을 포함합니다.

## 결론

**custom logger c#**를 구현하면 레드액션 파이프라인의 모든 단계에 대한 세밀한 인사이트를 얻을 수 있어 규정 준수 표준을 충족하고 문제를 디버깅하기가 쉬워집니다. 여기 제시된 접근 방식은 GroupDocs.Redaction for .NET과 원활히 작동하며, 이미 사용 중인 모든 .NET 로깅 프레임워크와 통합하도록 확장할 수 있습니다.

---

## 자주 묻는 질문

**Q:** GroupDocs.Redaction에서 사용자 정의 로깅의 목적은 무엇인가요?  
A: 사용자 정의 로깅은 상세한 레드액션 이벤트를 캡처하고, 감사 요구 사항을 충족하며, 실시간으로 오류와 경고를 노출함으로써 문제 해결을 단순화합니다.

**Q:** 사용자 정의 로거를 사용하여 오류를 처리하려면 어떻게 해야 하나요?  
A: `CustomLogger` 클래스에서 `LogError`를 구현합니다; `HasErrors` 플래그를 사용하면 심각한 문제가 감지될 경우 처리를 중단할 수 있습니다.

**Q:** 사용자 정의 로깅을 다른 시스템과 통합할 수 있나요?  
A: 예—로거 메서드를 확장하여 로그 메시지를 CRM, ERP 또는 중앙 모니터링 도구로 전달할 수 있습니다.

**Q:** 사용자 정의 로깅 구현 시 흔히 발생하는 함정은 무엇인가요?  
A: 메서드 오버라이드 누락, `RedactorSettings(logger)` 전달을 잊음, 파일 권한 부족이 가장 흔한 문제입니다.

**Q:** 사용자 정의 로깅이 문서 레드액션 워크플로우를 어떻게 개선하나요?  
A: 상세한 로그는 실시간 가시성을 제공하고, 디버깅을 효율화하며, GDPR 및 HIPAA와 같은 규정에서 요구하는 감사 추적을 생성합니다.

## 리소스

- **Documentation:** [GroupDocs.Redaction .NET Documentation](https://docs.groupdocs.com/redaction/net/)  
- **API reference:** [GroupDocs.Redaction API Reference](https://reference.groupdocs.com/redaction/net)  
- **Download:** [GroupDocs.Redaction for .NET](https://downloads.groupdocs.com/redaction/net)

---

**마지막 업데이트:** 2026-10-01  
**테스트 환경:** GroupDocs.Redaction 23.11 for .NET  
**작성자:** GroupDocs  

---

## 관련 튜토리얼

- [GroupDocs.Redaction for .NET으로 문서 로드하는 방법](/redaction/net/document-loading/)  
- [GroupDocs.Redaction .NET으로 레드액션된 문서 내보내는 방법](/redaction/net/document-saving/)  
- [GroupDocs.Redaction .NET을 사용한 문서 레드액션 구현&#58; 단계별 가이드](/redaction/net/getting-started/implement-document-redaction-groupdocs-redaction-net/)