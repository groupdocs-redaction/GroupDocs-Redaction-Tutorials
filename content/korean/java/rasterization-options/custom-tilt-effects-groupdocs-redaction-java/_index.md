---
date: '2026-06-01'
description: GroupDocs.Redaction for Java와 함께 tilt effect를 사용하는 방법을 배우고, 단계별 코드, 성능
  팁 및 사용자 정의 옵션을 포함합니다.
keywords:
- how to use tilt
- custom tilt effects
- GroupDocs.Redaction Java
- document rasterization
schemas:
- author: GroupDocs
  dateModified: '2026-06-01'
  description: Learn how to use tilt effect with GroupDocs.Redaction for Java, including
    step‑by‑step code, performance tips, and customization options.
  headline: How to Use Tilt Effect with GroupDocs.Redaction Java
  type: TechArticle
- description: Learn how to use tilt effect with GroupDocs.Redaction for Java, including
    step‑by‑step code, performance tips, and customization options.
  name: How to Use Tilt Effect with GroupDocs.Redaction Java
  steps:
  - name: Initialize Redactor and Save Options
    text: First, create a `Redactor` instance pointing at your source file, then prepare
      `SaveOptions` that will hold the rasterization configuration.
  - name: Configure Tilt Effect Settings
    text: Enable rasterization and define the tilt angle boundaries. The `AdvancedRasterizationOptions.Tilt`
      object lets you set `minAngle` and `maxAngle` in degrees, controlling how much
      each page can rotate.
  - name: Save Document with Tilt Effect
    text: Run the redaction process and output the rasterized, tilted document. The
      `save` call writes each page as an image (PNG by default) while applying the
      random tilt you specified.
  type: HowTo
- questions:
  - answer: It redacts sensitive content while preserving document layout and also
      supports advanced rasterization features like the tilt effect.
    question: What is GroupDocs.Redaction Java used for?
  - answer: By enabling rasterization and adding the `Tilt` advanced option with `minAngle`
      and `maxAngle` parameters, as shown in the code samples.
    question: How do I apply a tilt effect in my document using GroupDocs?
  - answer: Yes, a free trial is available. For production use, obtain a temporary
      or permanent license.
    question: Can I use GroupDocs.Redaction for free?
  - answer: It enhances visual appeal, adds a creative touch, and can help differentiate
      marketing or presentation materials.
    question: What are the benefits of using a tilt effect in documents?
  - answer: Very large files may increase processing time and memory usage; proper
      resource allocation mitigates this.
    question: Are there any limitations to applying custom effects with GroupDocs.Redaction
      Java?
  type: FAQPage
title: GroupDocs.Redaction Java와 Tilt Effect 사용 방법
type: docs
url: /ko/java/rasterization-options/custom-tilt-effects-groupdocs-redaction-java/
weight: 1
---

# GroupDocs.Redaction Java에서 Tilt 효과 사용 방법

In this tutorial you’ll discover **tilt 사용 방법** to give your rasterized documents a dynamic, hand‑held look, why the effect matters for modern presentations, and exactly which settings you need in GroupDocs.Redaction for Java. We’ll walk through the whole process—from installing the library to fine‑tuning performance—so you can apply the tilt effect confidently in real projects.

## 빠른 답변
- **Tilt 효과는 무엇을 하나요?** 정의된 범위 내에서 무작위 각도로 각 래스터화된 페이지를 회전시켜 동적인 약간 기울어진 모습을 만듭니다.  
- **어떤 라이브러리가 이 기능을 제공하나요?** GroupDocs.Redaction for Java (version 24.9 or newer).  
- **라이선스가 필요합니까?** 무료 체험판으로 평가할 수 있으며, 프로덕션에서는 영구 라이선스 또는 임시 라이선스가 필요합니다.  
- **메모리를 많이 사용하나요?** CPU 오버헤드가 약간 추가되지만, 적절한 메모리 설정으로 대용량 파일에서도 효율적으로 유지됩니다.  
- **각도 범위를 사용자 정의할 수 있나요?** 예 – 래스터화 옵션에서 `minAngle` 및 `maxAngle` 매개변수를 사용합니다.

## 맞춤 Tilt 효과란 무엇인가요?

맞춤 Tilt 효과는 문서의 각 페이지를 이미지로 변환하는 동안 적용되는 시각적 변환입니다. 최소 및 최대 각도를 지정하면 래스터라이저가 페이지를 무작위로 기울여 최종 출력에 예술적이고 “손에 들고 보는” 느낌을 줍니다. 이 효과는 표준 PDF의 딱딱하고 완벽하게 정렬된 모습을 깨고 개성을 더하고 싶을 때 특히 유용합니다.

## GroupDocs.Redaction에서 맞춤 Tilt 효과를 적용하는 이유는?

GroupDocs.Redaction은 **70개 이상의 입력 및 출력 형식**에 대한 래스터화를 지원하며 전체 파일을 메모리에 로드하지 않고 **2,000페이지**까지의 PDF를 처리할 수 있습니다. 내장된 tilt 옵션을 활용하면 타사 이미지 라이브러리를 피하고 통합 복잡성을 줄이며 전체 워크플로를 단일 검증된 SDK 안에 유지할 수 있습니다.

- **참여도:** 기울어진 페이지는 독자의 시선을 끌어 프레젠테이션이나 마케팅 브로셔에 적합합니다.  
- **브랜딩:** 원본 콘텐츠를 변경하지 않고 고유한 시각적 서명을 추가합니다.  
- **유연성:** 각도 범위를 제어하여 미묘하거나 극적인 기울기를 구현할 수 있습니다.  
- **통합:** 이 효과는 GroupDocs.Redaction의 래스터화 파이프라인에 내장되어 있어 외부 이미지 처리 도구가 필요하지 않습니다.

## 필수 조건

- Java 8 이상 설치.  
- Maven(또는 다른 빌드 도구)로 종속성을 관리합니다.  
- GroupDocs.Redaction 24.9 이상(본 튜토리얼은 최신 릴리스를 사용).  
- Java 파일 처리에 대한 기본적인 이해.

## GroupDocs.Redaction for Java 설정

### 설치 정보

**Maven**

Include GroupDocs.Redaction in your Maven project by adding the following repository and dependency to your `pom.xml` file:

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

**직접 다운로드**

또는 최신 버전을 직접 [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/)에서 다운로드하십시오.

#### 라이선스 획득

GroupDocs.Redaction을 완전히 활용하려면:

- **무료 체험** – 비용 없이 핵심 기능을 탐색합니다.  
- **임시 라이선스** – [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/)를 통해 제한된 기간의 키를 요청하여 전체 평가를 진행합니다.  
- **구매** – 프로덕션 사용을 위한 영구 라이선스를 획득합니다.

### 기본 초기화 및 설정

`Redactor` 클래스는 GroupDocs.Redaction에서 모든 리다크션 및 래스터화 작업의 진입점입니다. 문서 로드, 처리 및 저장을 관리하며 리소스를 자동으로 해제합니다.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;

// Set the path to your document directory
String documentPath = "YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX";

// Initialize a Redactor with the specified document
Redactor redactor = new Redactor(documentPath);
```

## 래스터화 중 맞춤 Tilt 효과 적용 방법

소스 파일을 로드하고, 래스터화를 활성화하고, 원하는 tilt 범위를 설정한 다음 변환된 문서를 저장합니다—몇 단계만으로 가능합니다. 이 개요는 전체 워크플로를 설명하므로 어떤 객체를 생성하고, 어떤 옵션을 구성하며, 상세 코드를 살펴보기 전에 저장 작업을 어떻게 호출하는지 정확히 알 수 있습니다.

### 단계별 구현

#### Step 1: Redactor 초기화 및 Save Options 설정

먼저, 소스 파일을 가리키는 `Redactor` 인스턴스를 생성하고, 래스터화 구성을 보관할 `SaveOptions`를 준비합니다.

```java
import com.groupdocs.redaction.options.AdvancedRasterizationOptions;
import java.util.HashMap;

Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
SaveOptions saveOptions = new SaveOptions();
```

#### Step 2: Tilt 효과 설정 구성

래스터화를 활성화하고 tilt 각도 경계를 정의합니다. `AdvancedRasterizationOptions.Tilt` 객체를 사용하여 `minAngle` 및 `maxAngle`를 도 단위로 설정하고 각 페이지가 회전할 수 있는 정도를 제어합니다.

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

#### Step 3: Tilt 효과와 함께 문서 저장

리다크션 프로세스를 실행하고 래스터화된 기울어진 문서를 출력합니다. `save` 호출은 지정한 무작위 tilt를 적용하면서 각 페이지를 이미지(PNG 기본)로 저장합니다.

```java
redactor.save("OUTPUT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX_scan", saveOptions);
```

### 매개변수 설명

- `minAngle` – 페이지에 적용될 수 있는 최소 회전(도).  
- `maxAngle` – 허용되는 최대 회전(도). 이러한 값을 조정하여 미묘하거나 뚜렷한 기울기를 구현합니다.

#### 문제 해결 팁

- JVM이 소스 및 출력 디렉터리에 쓸 수 있는지 확인하십시오.  
- GroupDocs.Redaction 24.9 이상 버전을 사용하고 있는지 확인하십시오; 이전 버전에는 `Tilt` 옵션이 없습니다.  
- 출력이 과도하게 왜곡되면 `maxAngle` 값을 낮추십시오.

## 실제 적용 사례

1. **창의적인 문서 프레젠테이션** – 슬라이드 데크나 클라이언트 제안서에 동적인 모습을 추가합니다.  
2. **마케팅 자료** – 브로셔와 전단지를 보다 손수 만든 느낌으로 만듭니다.  
3. **디지털 아카이브** – 온라인 전시를 위해 역사적 스캔에 미묘하고 스타일화된 외관을 부여합니다.

## 성능 고려 사항

### 성능 최적화

- **메모리 관리:** 멀티 페이지 PDF를 처리할 때 충분한 힙 공간(`-Xmx2g` 이상)을 할당합니다.  
- **I/O 효율성:** 가능한 경우 파일을 배치 처리하고 단일 `Redactor` 인스턴스를 재사용합니다.

### Java 메모리 관리 모범 사례

- `System.gc()`를 드물게 호출하고 JVM의 가비지 컬렉터에 의존하십시오.  
- 스트림을 즉시 닫으십시오(GroupDocs.Redaction이 대부분의 정리를 내부적으로 처리합니다).

## 일반적인 문제 및 해결책

| 문제 | 가능한 원인 | 해결책 |
|-------|--------------|----------|
| Tilt가 적용되지 않음 | 래스터화 비활성화 | Ensure `saveOptions.getRasterization().setEnabled(true);` |
| 출력 파일이 비어 있음 | 잘못된 출력 경로 | 디렉터리가 존재하고 쓰기 권한이 있는지 확인하십시오 |
| 예상치 못한 각도 | `minAngle` > `maxAngle` | 값을 교환하여 `minAngle` ≤ `maxAngle`가 되도록 하십시오 |

## 자주 묻는 질문

**Q: GroupDocs.Redaction Java는 무엇에 사용되나요?**  
A: 민감한 콘텐츠를 리다크션하면서 문서 레이아웃을 보존하고 tilt 효과와 같은 고급 래스터화 기능도 지원합니다.

**Q: GroupDocs를 사용하여 문서에 tilt 효과를 적용하려면 어떻게 해야 하나요?**  
A: 코드 샘플에 표시된 대로 래스터화를 활성화하고 `minAngle` 및 `maxAngle` 매개변수가 포함된 `Tilt` 고급 옵션을 추가합니다.

**Q: GroupDocs.Redaction을 무료로 사용할 수 있나요?**  
A: 예, 무료 체험판을 이용할 수 있습니다. 프로덕션 사용을 위해서는 임시 또는 영구 라이선스를 획득하십시오.

**Q: 문서에 tilt 효과를 사용하면 어떤 이점이 있나요?**  
A: 시각적 매력을 높이고 창의적인 터치를 추가하며 마케팅 또는 프레젠테이션 자료를 차별화하는 데 도움이 됩니다.

**Q: GroupDocs.Redaction Java에서 맞춤 효과를 적용하는 데 제한 사항이 있나요?**  
A: 매우 큰 파일은 처리 시간과 메모리 사용량을 증가시킬 수 있지만 적절한 리소스 할당으로 이를 완화할 수 있습니다.

## 리소스
- [GroupDocs Redaction 문서](https://docs.groupdocs.com/redaction/java/)
- [API 레퍼런스](https://reference.groupdocs.com/redaction/java)
- [GroupDocs.Redaction for Java 다운로드](https://releases.groupdocs.com/redaction/java/)
- [GitHub 저장소](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
- [무료 지원 포럼](https://forum.groupdocs.com/c/redaction/33)
- [임시 라이선스 신청](https://purchase.groupdocs.com/temporary-license/)

---

**마지막 업데이트:** 2026-06-01  
**테스트 환경:** GroupDocs.Redaction 24.9 for Java  
**작성자:** GroupDocs  

---

## 관련 튜토리얼

- [GroupDocs.Redaction Java용 래스터화 옵션 튜토리얼](/redaction/java/rasterization-options/)
- [Java에서 맞춤 노이즈 래스터화: GroupDocs.Redaction으로 민감한 정보 보호](/redaction/java/rasterization-options/java-groupdocs-redaction-custom-noise-rasterization/)
- [Java용 groupdocs redaction 사용 방법: Word 문서 사전 래스터화](/redaction/java/rasterization-options/groupdocs-redaction-java-pre-rasterization-word-docs/)