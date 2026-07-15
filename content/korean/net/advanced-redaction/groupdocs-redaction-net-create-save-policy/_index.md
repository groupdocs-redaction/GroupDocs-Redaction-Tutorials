---
date: '2026-03-30'
description: GroupDocs.Redaction을 사용하여 .NET에서 리다크션 정책을 만드는 방법을 배웁니다. 이 튜토리얼에서는 리다크션
  정책을 구축하고 적용하며 XML 파일로 저장하는 방법을 보여줍니다.
keywords:
- GroupDocs.Redaction .NET
- create redaction policy
- save XML policy
title: GroupDocs.Redaction .NET을 사용하여 레드랙션 정책 만들기 – 단계별 가이드
type: docs
url: /ko/net/advanced-redaction/groupdocs-redaction-net-create-save-policy/
weight: 1
---

# GroupDocs.Redaction .NET을 사용하여 마스킹 정책 만들기

현대 애플리케이션에서는 문서 내부의 기밀 데이터를 보호하는 것이 필수 보안 조치입니다. 계약서, 재무제표, 환자 기록 등을 다룰 때, 민감한 정보를 자동으로 가리거나 제거하는 **create redaction policy**가 필요합니다. 이 가이드에서는 라이브러리 설치, 마스킹 정의, 적용, 그리고 최종적으로 정책을 XML 파일로 저장하여 프로젝트 전반에 재사용하는 전체 과정을 단계별로 안내합니다.

## 빠른 답변
- **“create redaction policy”는 무엇을 의미합니까?** 이는 GroupDocs.Redaction에 기밀 내용을 숨기거나 교체하도록 지시하는 규칙(텍스트, 정규식, 이미지 등)을 정의하는 과정입니다.  
- **어떤 라이브러리가 필요합니까?** GroupDocs.Redaction for .NET (NuGet을 통해 제공됩니다).  
- **라이선스가 필요합니까?** 개발에는 무료 체험판을 사용할 수 있으며, 프로덕션에는 영구 라이선스가 필요합니다.  
- **정책을 재사용할 수 있습니까?** 예—XML로 저장하면 나중에 로드하여 모든 문서에 적용할 수 있습니다.  
- **지원되는 .NET 버전은 무엇입니까?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## Redaction Policy란?
Redaction policy는 제거하거나 교체해야 할 *what*과 교체 방식 *how*을 지정하는 규칙 모음입니다. 정책을 한 번 만들면 애플리케이션이 처리하는 모든 문서에 일관된 보안 표준을 적용할 수 있습니다.

## Redaction Policy를 만들기 위해 GroupDocs.Redaction을 사용하는 이유
- **전체 문서 형식 지원** – Word, PDF, Excel, PowerPoint 등  
- **프로그래밍 제어** – 정확한 구문, 정규식 또는 사용자 정의 로직을 정의합니다.  
- **재사용 가능한 XML 정책** – 규칙을 한 번 내보내어 팀이나 서비스 간에 공유할 수 있습니다.  
- **성능 최적화 엔진** – 대용량 파일을 효율적으로 처리하고 워크로드에 맞게 확장됩니다.

## 전제 조건
- **GroupDocs.Redaction** 라이브러리(.NET 런타임과 호환).  
- Visual Studio, VS Code 또는 C#을 지원하는 모든 IDE.  
- C# 및 .NET 프로젝트 구조에 대한 기본 지식.

## .NET용 GroupDocs.Redaction 설정
먼저, 라이브러리를 프로젝트에 추가합니다.

**.NET CLI 사용**
```bash
dotnet add package GroupDocs.Redaction
```

**패키지 관리자 사용**
```powershell
Install-Package GroupDocs.Redaction
```

또는 NuGet 패키지 관리자 UI에서 “GroupDocs.Redaction”을 검색하여 설치합니다.

### 라이선스 획득
- 기능을 살펴보기 위해 **free trial**로 시작합니다.  
- 확장 테스트를 위해 **temporary license**를 요청하고, 프로덕션 사용을 위해 정식 라이선스를 구매합니다.

### 기본 초기화
소스 파일에 네임스페이스를 추가합니다:

```csharp
using GroupDocs.Redaction;
```

## GroupDocs.Redaction .NET을 사용하여 Redaction Policy 만들기
다음은 Redaction Policy를 구축하고 지속하는 방법을 단계별로 보여주는 walkthrough입니다.

### 단계 1: 문서 디렉터리 준비
```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
```
*`"YOUR_DOCUMENT_DIRECTORY"`를 보호하려는 문서가 들어 있는 폴더로 교체하십시오.*

### 단계 2: 문서 로드
```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // Further code will go here
}
```
`Redactor` 객체가 파일을 열고 그 수명 주기를 관리합니다.

### 단계 3: 마스킹 정의
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

### 단계 4: 마스킹 적용
```csharp
redactor.Apply(redactions);
```
정의된 모든 규칙이 열린 문서에 한 번에 실행됩니다.

### 단계 5: 정책을 XML 파일로 저장
```csharp
string policyFile = "policy.xml";
redactor.SavePolicy(policyFile, new SaveOptions());
```
XML 파일은 마스킹 정의를 저장하여 코드를 다시 작성하지 않고도 동일한 정책을 재사용할 수 있게 합니다.

## 실용적인 적용 사례
- **법률 사무소**는 초안을 공유하기 전에 사건 번호와 고객 이름을 마스킹할 수 있습니다.  
- **재무 부서**는 보고서에서 계좌 번호나 거래 날짜를 마스킹합니다.  
- **헬스케어 제공자**는 환자 식별자를 제거하여 HIPAA 준수를 보장합니다.

## 성능 팁
- 메모리 사용량을 낮게 유지하려면 **한 번에 하나의 문서**를 엽니다.  
- **효율적인 정규식**을 작성하고, 처리 시간을 늘리는 과도하게 넓은 패턴을 피하십시오.  
- 성능 향상 및 새로운 마스킹 유형의 혜택을 받으려면 라이브러리를 **최신 상태**로 유지하십시오.

## 일반적인 문제와 해결책
| 문제 | 발생 원인 | 해결 방법 |
|-------|----------------|------------|
| **디렉터리 준비 중 IO 예외** | 잘못된 경로나 쓰기 권한 부족 | 폴더가 존재하는지 확인하고 애플리케이션에 읽기/쓰기 권한이 있는지 확인하십시오. |
| **Regex가 예상 텍스트와 일치하지 않음** | 패턴이 너무 엄격하거나 이스케이프 문자가 누락됨 | 온라인 테스트 도구로 regex를 테스트하고, 수량자를 조정하거나 특수 문자를 이스케이프하십시오. |
| **정책 파일이 생성되지 않음** | `SavePolicy`가 마스킹 적용 전에 호출되었거나 잘못된 경로를 사용함 | 출력 디렉터리가 쓰기 가능한지 확인하고 `Apply` 후에 `SavePolicy`를 호출하십시오. |

## 자주 묻는 질문
**Q: 기존 XML 정책을 프로그래밍 방식으로 만들지 않고 로드할 수 있나요?**  
A: 예—`redactor.LoadPolicy("policy.xml")`를 사용하여 이전에 저장된 정책을 가져옵니다.

**Q: GroupDocs.Redaction이 비밀번호로 보호된 PDF를 지원합니까?**  
A: 물론 지원합니다. 비밀번호를 `Redactor` 생성자에 전달하십시오: `new Redactor(sourceFile, "password")`.

**Q: 이미지나 메타데이터를 마스킹할 수 있나요?**  
A: 라이브러리는 이러한 시나리오를 위해 `ImageRedaction` 및 `MetadataRedaction` 클래스를 제공합니다.

**Q: 수백 MB 규모의 대용량 문서는 어떻게 처리합니까?**  
A: 문서를 청크로 처리하거나 스트리밍 API를 사용해 메모리 사용량을 줄이세요; OutOfMemory 오류가 발생하면 JVM 힙을 늘리는 것도 고려하십시오.

**Q: 상업적 사용을 위한 라이선스 모델은 무엇입니까?**  
A: 프로덕션 배포에는 유료 라이선스가 필요하며, 개발 및 테스트에는 체험 라이선스로 충분합니다.

## 결론
이제 GroupDocs.Redaction for .NET을 사용하여 모든 문서에 적용할 수 있는 완전하고 재사용 가능한 **redaction policy**를 보유하게 되었습니다. 정책을 XML로 내보내면 향후 업데이트가 간소화되고 조직 전체에 일관된 데이터 보호를 보장합니다.

### 다음 단계
- `ImageRedaction` 또는 `MetadataRedaction`과 같은 추가 마스킹 유형을 실험해 보세요.  
- 자동 마스킹을 위해 정책 로드 로직을 문서 관리 워크플로에 통합하십시오.  
- 고급 커스터마이징을 위해 **GroupDocs.Redaction** API 레퍼런스를 살펴보세요.

---

**마지막 업데이트:** 2026-03-30  
**테스트 환경:** GroupDocs.Redaction 5.8 for .NET  
**작성자:** GroupDocs  

**리소스**  
- [문서](https://docs.groupdocs.com/redaction/net/)  
- [API 레퍼런스](https://reference.groupdocs.com/redaction/net)  
- [다운로드](https://releases.groupdocs.com/redaction/net/)  
- [무료 지원 포럼](https://forum.groupdocs.com/c/redaction/33)  
- [임시 라이선스 신청](https://purchase.groupdocs.com/temporary-license/)