---
date: '2026-02-11'
description: GroupDocs.Redaction for Java를 사용하여 문서에 맞춤 기울이기 효과를 적용하는 방법을 단계별 코드와 성능
  팁과 함께 배워보세요.
keywords:
- custom tilt effects
- GroupDocs.Redaction Java
- document rasterization
title: GroupDocs.Redaction Java로 사용자 정의 기울기 효과 적용
type: docs
url: /ko/java/rasterization-options/custom-tilt-effects-groupdocs-redaction-java/
weight: 1
---

# GroupDocs.Redaction Java로 사용자 정의 기울기 효과 적용

문서를 래스터화하는 동안 **사용자 정의 기울기 효과**를 적용하여 시각적 매력을 높이면 보고서, 마케팅 자료 또는 보관 스캔이 돋보이게 할 수 있습니다. 이 튜토리얼에서는 이 효과가 왜 중요한지, GroupDocs.Redaction for Java와 함께 어떻게 구성하는지, 그리고 성능을 원활하게 유지하기 위한 실용적인 팁을 알아봅니다.

## 빠른 답변
- **Tilt 효과는 무엇을 하나요?** 정의된 범위 내에서 무작위 각도로 각 래스터화된 페이지를 회전시켜 동적이고 약간 기울어진 모습을 만듭니다.  
- **어떤 라이브러리가 이 기능을 제공하나요?** GroupDocs.Redaction for Java (버전 24.9 또는 최신).  
- **라이선스가 필요합니까?** 무료 체험으로 평가할 수 있으며, 프로덕션에서는 영구 라이선스 또는 임시 라이선스가 필요합니다.  
- **메모리를 많이 사용하나요?** 약간의 CPU 오버헤드가 추가되지만, 적절한 메모리 설정을 통해 대용량 파일에서도 효율적으로 동작합니다.  
- **각도 범위를 사용자 정의할 수 있나요?** 예 – 래스터화 옵션에서 `minAngle` 및 `maxAngle` 매개변수를 사용합니다.

## 사용자 정의 기울기 효과란?

사용자 정의 기울기 효과는 문서의 각 페이지를 이미지로 변환하는 동안 적용되는 시각적 변환입니다. 최소 및 최대 각도를 지정하면 래스터라이저가 페이지를 무작위로 기울여 최종 출력에 예술적이고 “손에 들고 본 듯한” 느낌을 부여합니다.

## GroupDocs.Redaction에서 사용자 정의 기울기 효과를 적용하는 이유

- **Engagement:** 기울어진 페이지는 독자의 시선을 끌어 프레젠테이션이나 마케팅 브로셔에 적합합니다.  
- **Branding:** 원본 콘텐츠를 변경하지 않고 고유한 시각적 서명을 추가합니다.  
- **Flexibility:** 각도 범위를 제어하여 미묘하거나 극적인 기울기를 구현할 수 있습니다.  
- **Integration:** 이 효과는 GroupDocs.Redaction의 래스터화 파이프라인에 내장되어 있어 외부 이미지 처리 도구가 필요하지 않습니다.

## 사전 요구 사항

- Java 8 이상 설치.  
- Maven(또는 다른 빌드 도구)으로 종속성 관리.  
- GroupDocs.Redaction 24.9 또는 최신 버전(튜토리얼은 최신 릴리스를 사용).  
- Java 파일 처리에 대한 기본 지식.

## GroupDocs.Redaction for Java 설정

### 설치 정보

**Maven**

`pom.xml` 파일에 다음 저장소와 종속성을 추가하여 Maven 프로젝트에 GroupDocs.Redaction을 포함합니다:

```xml
<repositories>
   <repository>
      <id>repository.groupdocs.com</id>
      <name>GroupDocs Repository</name>
      <url>https://releases.groupdocs.com/redaction/java/</url>
   </repository>
</repositories>

<dependencies>
   <dependency>
      <groupId>com.groupdocs</groupId>
      <artifactId>groupdocs-redaction</artifactId>
      <version>24.9</version>
   </dependency>
</dependencies>
```

**Direct Download**

또는 최신 버전을 [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/)에서 직접 다운로드합니다.

#### 라이선스 획득

GroupDocs.Redaction을 완전히 활용하려면:

- **Free Trial** – 비용 없이 핵심 기능을 탐색합니다.  
- **Temporary License** – [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/)를 통해 기간 제한 키를 요청하여 전체 평가를 수행합니다.  
- **Purchase** – 프로덕션 사용을 위한 영구 라이선스를 획득합니다.

### 기본 초기화 및 설정

시작하려면 필요한 클래스를 import하고 소스 문서를 가리키는 `Redactor` 인스턴스를 생성합니다:

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;

// Set the path to your document directory
String documentPath = "YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX";

// Initialize a Redactor with the specified document
Redactor redactor = new Redactor(documentPath);
```

## 래스터화 중 사용자 정의 기울기 효과 적용 방법

### 기능 개요

GroupDocs.Redaction을 사용하면 래스터화를 활성화하고 기울기 효과와 같은 고급 옵션을 주입할 수 있습니다. `AdvancedRasterizationOptions.Tilt`를 구성하여 각 페이지에 적용되는 각도 범위를 제어합니다.

### 단계별 구현

#### 단계 1: Redactor 초기화 및 저장 옵션 설정

```java
import com.groupdocs.redaction.options.AdvancedRasterizationOptions;
import java.util.HashMap;

Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
SaveOptions saveOptions = new SaveOptions();
```

#### 단계 2: 기울기 효과 설정 구성

래스터화를 활성화하고 기울기 각도 경계를 정의합니다:

```java
saveOptions.getRasterization().setEnabled(true);
HashMap<String, String> tiltSettings = new HashMap<>();
tiltSettings.put("minAngle", "15"); // Set the minimum angle for the tilt effect
	tiltSettings.put("maxAngle", "30"); // Set the maximum angle for the tilt effect

saveOptions.getRasterization().addAdvancedOption(
    AdvancedRasterizationOptions.Tilt, 
    tiltSettings
);
```

#### 단계 3: 기울기 효과와 함께 문서 저장

레드랙션 프로세스를 실행하고 래스터화된 기울어진 문서를 출력합니다:

```java
redactor.save("OUTPUT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX_scan", saveOptions);
```

### 매개변수 설명

- **minAngle** – 페이지에 적용될 수 있는 최소 회전 각도(도).  
- **maxAngle** – 허용되는 최대 회전 각도(도).  
이 값을 조정하여 미묘하거나 뚜렷한 기울기를 구현합니다.

#### 문제 해결 팁

- 소스 및 출력 디렉터리가 JVM에 의해 쓰기 가능한지 확인합니다.  
- GroupDocs.Redaction 24.9 또는 최신 버전을 사용하고 있는지 확인합니다; 이전 버전에는 `Tilt` 옵션이 없습니다.  
- 출력이 과도하게 왜곡된 경우 `maxAngle` 값을 낮춥니다.

## 실용적인 적용 사례

1. **Creative Document Presentation** – 슬라이드 덱이나 클라이언트 제안서에 동적인 외관을 추가합니다.  
2. **Marketing Materials** – 브로셔와 전단지를 보다 손수 만든 느낌으로 만듭니다.  
3. **Digital Archives** – 역사적 스캔에 미묘하고 스타일리시한 외관을 부여하여 온라인 전시용으로 활용합니다.

## 성능 고려 사항

### 성능 최적화

- **Memory Management:** 다중 페이지 PDF를 처리할 때 충분한 힙 공간(`-Xmx2g` 이상)을 할당합니다.  
- **I/O Efficiency:** 파일을 배치 처리하고 가능한 경우 단일 `Redactor` 인스턴스를 재사용합니다.

### Java 메모리 관리 모범 사례

- `System.gc()` 호출은 최소화하고 JVM의 가비지 컬렉터에 의존합니다.  
- 스트림을 즉시 닫습니다(GroupDocs.Redaction이 대부분의 정리를 내부적으로 처리합니다).

## 일반적인 문제 및 해결책

| 문제 | 가능한 원인 | 해결책 |
|-------|--------------|----------|
| Tilt 적용되지 않음 | 래스터화 비활성화 | `saveOptions.getRasterization().setEnabled(true);`를 확인합니다. |
| 출력 파일 비어 있음 | 잘못된 출력 경로 | 디렉터리가 존재하고 쓰기 권한이 있는지 확인합니다. |
| 예상치 못한 각도 | `minAngle` > `maxAngle` | `minAngle` ≤ `maxAngle`가 되도록 값을 교환합니다. |

## 자주 묻는 질문

**Q: GroupDocs.Redaction Java는 무엇에 사용되나요?**  
A: 민감한 콘텐츠를 레드랙션하면서 문서 레이아웃을 유지하고, 기울기 효과와 같은 고급 래스터화 기능도 지원합니다.

**Q: GroupDocs를 사용해 문서에 기울기 효과를 적용하려면 어떻게 해야 하나요?**  
A: 래스터화를 활성화하고 코드 샘플에 표시된 대로 `minAngle` 및 `maxAngle` 매개변수를 사용하여 `Tilt` 고급 옵션을 추가합니다.

**Q: GroupDocs.Redaction을 무료로 사용할 수 있나요?**  
A: 예, 무료 체험판을 사용할 수 있습니다. 프로덕션 사용을 위해서는 임시 또는 영구 라이선스를 획득해야 합니다.

**Q: 문서에 기울기 효과를 사용하면 어떤 이점이 있나요?**  
A: 시각적 매력을 높이고 창의적인 터치를 추가하며, 마케팅 또는 프레젠테이션 자료를 차별화하는 데 도움이 됩니다.

**Q: GroupDocs.Redaction Java로 사용자 정의 효과를 적용하는 데 제한 사항이 있나요?**  
A: 매우 큰 파일은 처리 시간과 메모리 사용량을 증가시킬 수 있으며, 적절한 리소스 할당으로 이를 완화할 수 있습니다.

## 리소스
- [GroupDocs Redaction 문서](https://docs.groupdocs.com/redaction/java/)
- [API 레퍼런스](https://reference.groupdocs.com/redaction/java)
- [GroupDocs.Redaction for Java 다운로드](https://releases.groupdocs.com/redaction/java/)
- [GitHub 저장소](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
- [무료 지원 포럼](https://forum.groupdocs.com/c/redaction/33)
- [임시 라이선스 신청](https://purchase.groupdocs.com/temporary-license/)

---

**마지막 업데이트:** 2026-02-11  
**테스트 환경:** GroupDocs.Redaction 24.9 for Java  
**작성자:** GroupDocs