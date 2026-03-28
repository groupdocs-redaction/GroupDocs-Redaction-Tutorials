---
date: '2026-03-28'
description: GroupDocs.Redaction for .NET에서 C# 맞춤 로거를 구현하는 방법을 배우고, 상세한 맞춤 로깅과 보다
  쉬운 규정 준수 보고를 가능하게 합니다.
keywords:
- custom logger c#
- custom logging .net
- save redacted document
- log warnings c#
title: GroupDocs.Redaction for .NET에서 C# 사용자 정의 로거 구현
type: docs
url: /ko/net/advanced-redaction/custom-logging-groupdocs-redaction-net/
weight: 1
---

# GroupDocs.Redaction for .NET에서 사용자 정의 로거 c# 구현

문서 레드액션을 효율적으로 관리하는 것은 특히 민감한 정보를 다룰 때 중요합니다. 이 가이드에서는 GroupDocs.Redaction for .NET과 함께 **custom logger c#를 구현하는 방법**을 배우게 되며, 로깅, 오류 처리 및 감사 추적에 대한 완전한 제어를 제공합니다.

## 빠른 답변
- **custom logger c#는 무엇을 하나요?** 레드액션 중 오류, 경고 및 정보 메시지를 캡처합니다.  
- **ILogger 인터페이스를 제공하는 라이브러리는?** GroupDocs.Redaction for .NET.  
- **레드액션된 문서를 래스터화 없이 저장할 수 있나요?** 예 – `redactor.Save(..., new Options.RasterizationOptions { Enabled = false })`를 사용합니다.  
- **프로덕션 사용에 라이선스가 필요합니까?** 프로덕션에는 정식 라이선스가 필요하며, 평가용 트라이얼을 사용할 수 있습니다.  
- **이 접근 방식이 .NET Core / .NET 6+와 호환되나요?** 물론입니다 – 동일한 API가 .NET Framework와 .NET Core/5/6 모두에서 작동합니다.

## custom logger c#란 무엇인가?
**custom logger c#**는 GroupDocs.Redaction에서 제공하는 `ILogger` 인터페이스를 구현하는 클래스입니다. 콘솔, 파일, 데이터베이스 또는 외부 모니터링 시스템 등 필요한 곳으로 로그 메시지를 전달할 수 있으며, 레드액션 워크플로우를 명확히 파악할 수 있게 해줍니다.

## GroupDocs.Redaction와 함께 custom logging .net을 사용하는 이유?
- **규정 준수 및 감사:** 상세 로그가 규제 요구사항을 충족합니다.  
- **오류 가시성:** `LogError`와 `LogWarning`은 문제에 대한 즉각적인 피드백을 제공합니다.  
- **통합 유연성:** 기존 .NET 로깅 프레임워크(Serilog, NLog 등)로 로그를 전달할 수 있습니다.

## 사전 요구 사항
- **GroupDocs.Redaction for .NET**이 설치되어 있음(아래 설치 섹션 참고).  
- .NET 개발 환경(Visual Studio, VS Code 또는 CLI).  
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
- **무료 체험:** 임시 라이선스로 API를 테스트합니다.  
- **임시 라이선스:** 제한된 기간 동안 전체 기능에 접근합니다.  
- **구매:** 프로덕션 배포를 위한 영구 라이선스를 획득합니다.

## 단계별 가이드

### 1단계: 사용자 정의 로거 클래스 정의 (log warnings c#)
`ILogger`를 구현하는 클래스를 생성합니다. 이 클래스는 오류, 경고 및 정보 메시지를 캡처합니다.

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

**설명:** `HasErrors` 플래그는 처리를 계속할지 여부를 결정하는 데 도움이 됩니다. 세 메서드는 대부분의 레드액션 시나리오에서 필요한 세 가지 로그 레벨에 해당합니다.

### 2단계: 파일 경로 준비 및 원본 문서 열기
```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
string outputFile = Utils.GetOutputFile(sourceFile);
```

**왜 중요한가:** 유틸리티 메서드를 사용하면 코드가 깔끔해지고, **레드액션된 문서 저장**을 시도하기 전에 출력 폴더가 존재하는지 확인할 수 있습니다.

### 3단계: 사용자 정의 로거를 사용하여 레드액션 적용
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

**설명:**  
1. `Redactor`는 `RedactorSettings(logger)`로 인스턴스화되어 `CustomLogger`와 연결됩니다.  
2. 레드액션을 적용한 후 코드가 `logger.HasErrors`를 확인합니다. 오류가 없으면 문서를 저장합니다—래스터화 없이 **레드액션된 문서 저장** 로직을 보여줍니다.

### 일반적인 함정 및 문제 해결
- **로그 출력 누락:** 각 `Log*` 메서드가 올바르게 오버라이드되었는지 확인합니다.  
- **파일 접근 예외:** 애플리케이션이 원본 및 출력 경로에 대한 읽기/쓰기 권한을 가지고 있는지 확인합니다.  
- **로거 연결 안 됨:** `RedactorSettings(logger)` 매개변수가 필수이며, 이를 생략하면 사용자 정의 로깅이 비활성화됩니다.

## 실용적인 적용 사례
1. **규정 준수 보고:** 로그 항목을 CSV 또는 데이터베이스로 내보내어 감사 추적을 만듭니다.  
2. **오류 추적:** `LogError` 출력을 스캔하여 문제 파일을 빠르게 찾습니다.  
3. **워크플로 자동화:** `LogWarning`이 호출될 때 하위 프로세스(예: 컴플라이언스 담당자 알림)를 트리거합니다.

## 성능 고려 사항
- **스트림을 즉시 해제**하여 메모리를 해제합니다. 특히 대량 배치를 처리할 때 중요합니다.  
- **CPU 및 메모리 모니터링**을 대량 레드액션 중에 수행하고, 로거 동기화를 신중히 하여 병렬 처리 고려합니다.  
- **업데이트 유지:** 최신 GroupDocs.Redaction 버전은 종종 성능 최적화 및 추가 로깅 훅을 포함합니다.

## 결론
**custom logger c#**를 구현하면 레드액션 파이프라인의 모든 단계에 대한 세밀한 통찰을 얻을 수 있어 규정 준수 기준을 충족하고 문제를 디버깅하기가 쉬워집니다. 여기서 제시한 접근 방식은 GroupDocs.Redaction for .NET과 원활히 작동하며, 이미 사용 중인 모든 .NET 로깅 프레임워크와 통합하도록 확장할 수 있습니다.

---

## 자주 묻는 질문

**Q: GroupDocs.Redaction와 함께 custom logging을 사용하는 목적은 무엇인가요?**  
A: custom logging은 규정 준수, 오류 추적 및 워크플로 최적화를 위해 레드액션을 추적하고 관리하는 데 도움이 됩니다.

**Q: custom logger를 사용하여 오류를 어떻게 처리하나요?**  
A: `CustomLogger` 클래스에서 `LogError`를 구현하고, `HasErrors` 플래그를 사용해 필요 시 처리를 중단할 수 있습니다.

**Q: custom logging을 다른 시스템과 통합할 수 있나요?**  
A: 예, 로거 메서드를 확장하여 로그 메시지를 CRM, ERP 또는 중앙 모니터링 도구로 전달할 수 있습니다.

**Q: custom logging 구현 시 흔히 발생하는 함정은 무엇인가요?**  
A: 메서드 구현 오류, `RedactorSettings(logger)` 누락, 파일 권한 문제 등이 가장 흔합니다.

**Q: custom logging이 문서 레드액션 워크플로를 어떻게 개선하나요?**  
A: 상세 로그는 실시간 가시성을 제공하고, 문제 해결을 간소화하며, 감사 요구사항을 충족합니다.

## 리소스

- **문서:** [GroupDocs.Redaction .NET Documentation](https://docs.groupdocs.com/redaction/net/)  
- **API 레퍼런스:** [GroupDocs.Redaction API Reference](https://reference.groupdocs.com/redaction/net)  
- **다운로드:** [GroupDocs.Redaction for .NET](https://downloads.groupdocs.com/redaction/net)

---

**마지막 업데이트:** 2026-03-28  
**테스트 환경:** GroupDocs.Redaction 23.11 for .NET  
**작성자:** GroupDocs