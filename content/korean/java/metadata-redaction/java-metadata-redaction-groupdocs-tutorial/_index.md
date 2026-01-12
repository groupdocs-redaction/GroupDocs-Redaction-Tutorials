---
date: '2026-01-08'
description: GroupDocs.Redaction을 사용하여 Java에서 MetadataSearchRedaction을 활용하고, 민감한 문서
  메타데이터를 안전하게 삭제하는 방법을 배우세요.
keywords:
- metadata redaction Java
- GroupDocs Redaction tutorial
- secure document metadata
title: Java와 GroupDocs에서 MetadataSearchRedaction 사용 방법
type: docs
url: /ko/java/metadata-redaction/java-metadata-redaction-groupdocs-tutorial/
weight: 1
---

# Java와 GroupDocs에서 MetadataSearchRedaction 사용 방법

이 포괄적인 가이드에서는 GroupDocs.Redaction for Java를 사용하여 Word, PDF 및 기타 문서 형식에서 회사 이름과 같은 기밀 메타데이터를 제거하는 **MetadataSearchRedaction 사용 방법**을 알아봅니다. 튜토리얼이 끝날 때쯤에는 메타데이터 레드랙션을 모든 Java 기반 워크플로에 통합하여 민감한 정보를 안전하게 보호할 수 있게 됩니다.

## 빠른 답변
- **MetadataSearchRedaction은 무엇을 하나요?** 특정 메타데이터 필드를 검색하고 해당 값을 사용자 정의 텍스트로 교체합니다.  
- **필요한 라이브러리는?** GroupDocs.Redaction for Java (v24.9 이상).  
- **라이선스가 필요합니까?** 평가용으로는 무료 체험판을 사용할 수 있으며, 프로덕션에서는 정식 라이선스가 필요합니다.  
- **원본 파일 형식을 유지할 수 있나요?** 예—`SaveOptions`를 사용하여 원본 형식을 보존합니다.  
- **이 접근 방식은 스레드‑안전합니까?** 각 `Redactor` 인스턴스가 독립적이므로 문서를 병렬로 처리할 수 있습니다.

## MetadataSearchRedaction이란?
`MetadataSearchRedaction`은 특정 메타데이터 속성(예: *Company*, *Author*)을 대상으로 하여 그 내용을 플레이스홀더로 교체할 수 있는 특수 레드랙션 클래스입니다. 외부 파트너와 문서를 공유하기 전에 기업 데이터를 익명화해야 할 때 이상적입니다.

## 메타데이터 레드랙션에 MetadataSearchRedaction을 사용하는 이유
- **정밀도** – 지정한 필드만 레드랙션하고 문서의 나머지는 그대로 둡니다.  
- **규정 준수** – 숨겨진 식별자를 제거하여 GDPR, HIPAA 등 개인정보 보호 규정을 충족하는 데 도움을 줍니다.  
- **자동화 준비** – 배치 처리 파이프라인이나 마이크로서비스에 매끄럽게 통합됩니다.

## 사전 요구 사항
- **GroupDocs.Redaction for Java** ≥ 24.9.  
- Java 8 이상 설치되어 있어야 합니다.  
- IntelliJ IDEA 또는 Eclipse와 같은 IDE (선택 사항이지만 권장).  
- Maven에 대한 기본 지식(또는 JAR를 수동으로 추가할 수 있는 능력).

## GroupDocs.Redaction for Java 설정
`pom.xml`에 저장소와 의존성을 추가합니다. 이 단계는 Maven이 라이브러리를 자동으로 다운로드하도록 보장합니다.

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

*또는 공식 릴리스 페이지에서 JAR를 직접 다운로드할 수도 있습니다:*  
[GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/)

### 라이선스 획득
- **무료 체험** – 모든 기능을 체험할 수 있는 체험 라이선스를 다운로드합니다.  
- **임시 라이선스** – 장기 테스트에 사용합니다.  
- **정식 라이선스** – 프로덕션 배포에 필요합니다.

## 기본 초기화
처리하려는 문서를 가리키는 `Redactor` 인스턴스를 생성합니다.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

## 구현 가이드

### 단계 1: 필요한 클래스 가져오기
이러한 import 문을 통해 레드랙션 엔진, 저장 옵션 및 메타데이터 유틸리티에 접근할 수 있습니다.

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.redactions.MetadataFilters;
import com.groupdocs.redaction.redactions.MetadataSearchRedaction;
```

### 단계 2: Redactor 초기화
`Redactor`를 소스 파일 경로와 함께 인스턴스화합니다.

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

### 단계 3: 메타데이터 검색 및 레드랙션 구성
`MetadataSearchRedaction`을 생성하여 정확히 **"Company Ltd."** 문자열을 찾고 이를 **"--company--"** 로 교체합니다. `setFilter` 호출은 작업을 *Company* 메타데이터 필드에만 제한합니다.

```java
MetadataSearchRedaction redaction = new MetadataSearchRedaction("Company Ltd.", "--company--");
redaction.setFilter(MetadataFilters.Company);
```

### 단계 4: 레드랙션 적용
열린 문서에 레드랙션을 실행합니다.

```java
redactor.apply(redaction);
```

### 단계 5: 사용자 지정 옵션으로 저장
`SaveOptions`를 구성하여 레드랙션된 파일에 “_Redacted” 접미사가 붙고 원본 형식이 유지되도록 합니다.

```java
SaveOptions tmp0 = new SaveOptions();
tmp0.setAddSuffix(true);  // Adds "_Redacted" to file name
	tmp0.setRasterizeToPDF(false);  // Keeps original format

redactor.save(tmp0);
```

### 단계 6: 리소스 해제
네이티브 리소스를 해제하고 메모리 누수를 방지하기 위해 항상 `Redactor`를 닫아야 합니다.

```java
finally {
    redactor.close();
}
```

## 일반적인 문제와 해결책
- **FileNotFoundException** – `Redactor`에 전달하는 경로를 다시 확인하십시오. 절대 경로나 `Paths.get(...)`를 사용하면 신뢰성이 높아집니다.  
- **변경 사항이 없음** – 대상 메타데이터 필드에 실제로 검색 문자열이 포함되어 있는지 확인하십시오; 메타데이터는 기본적으로 대소문자를 구분합니다.  
- **대용량 파일에서 메모리 부족 오류** – 문서를 작은 배치로 처리하고 각 파일 처리 후 즉시 `redactor.close()`를 호출하십시오.

## 실용적인 적용 사례
1. **법률 문서** – 계약서를 제3자에게 보내기 전에 고객 회사 이름을 제거합니다.  
2. **재무 보고** – 감사 파일의 내부 식별자를 익명화합니다.  
3. **협업 프로젝트** – 외부 벤더와 초안을 공유할 때 독점 정보를 보호합니다.

## 성능 고려 사항
- **메모리 관리** – 라이브러리는 전체 문서를 메모리에 보관하므로 각 파일 처리 후 `Redactor`를 닫는 것이 필수적입니다.  
- **배치 처리** – 대량 처리 상황에서는 파일 컬렉션을 순회하면서 단일 `SaveOptions` 인스턴스를 재사용합니다.  
- **업데이트 유지** – 새로운 릴리스는 성능 개선 및 버그 수정을 포함하므로 항상 최신 안정 버전을 목표로 합니다.

## 결론
이제 **MetadataSearchRedaction을 사용하는 방법**을 알고 있으므로 GroupDocs.Redaction for Java를 이용해 문서에서 회사 메타데이터를 안전하게 제거할 수 있습니다. 이러한 단계를 문서 처리 파이프라인에 통합하여 규정을 준수하고 민감한 정보를 보호하십시오.

**다음 단계**
- *Author* 또는 *Creator*와 같은 다른 메타데이터 필드를 실험해 보세요.  
- 텍스트 또는 이미지 레드랙션과 메타데이터 레드랙션을 결합하여 전체 커버리지를 제공하는 솔루션을 만들세요.

## FAQ 섹션
1. **GroupDocs.Redaction for Java란?**  
   - Java 애플리케이션을 사용해 문서의 텍스트, 메타데이터 및 이미지를 레드랙션할 수 있는 강력한 라이브러리입니다.  
2. **라이선스를 구매하지 않고 GroupDocs.Redaction을 사용할 수 있나요?**  
   - 예, 하지만 제한이 있습니다. 무료 체험판이나 임시 라이선스를 통해 테스트 목적의 전체 기능에 접근할 수 있습니다.  
3. **레드랙션 중에 문서 형식이 유지되도록 하려면 어떻게 해야 하나요?**  
   - `SaveOptions`를 사용해 PDF로 래스터화하지 않는 등 요구 사항을 지정합니다.  
4. **GroupDocs.Redaction으로 레드랙션할 수 있는 문서 유형은 무엇인가요?**  
   - Word, Excel, PowerPoint, PDF 등 다양한 형식을 지원합니다.  
5. **문제 발생 시 지원을 어디서 받을 수 있나요?**  
   - [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33)에서 도움을 받을 수 있습니다.

## 자주 묻는 질문
**Q: MetadataSearchRedaction이 암호화된 문서에서도 작동하나요?**  
A: 예. 비밀번호 매개변수를 받는 `Redactor` 생성자를 사용해 적절한 비밀번호로 문서를 로드하면 됩니다.

**Q: 하나의 실행에서 여러 메타데이터 레드랙션을 연쇄적으로 적용할 수 있나요?**  
A: 물론입니다. 여러 `MetadataSearchRedaction` 객체를 생성하고 서로 다른 필터를 설정한 뒤 저장하기 전에 순차적으로 적용하면 됩니다.

**Q: 저장하기 전에 레드랙션을 미리 볼 수 있나요?**  
A: `redactor.getRedactions()`를 호출하면 보류 중인 레드랙션 목록을 가져와 프로그램matically 확인할 수 있습니다.

## 리소스
- **Documentation**: [GroupDocs Documentation](https://docs.groupdocs.com/redaction/java/)에서 자세한 가이드를 확인하세요.  
- **API Reference**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java)에서 전체 API 레퍼런스를 확인하십시오.  
- **Download Library**: [GroupDocs Downloads](https://releases.groupdocs.com/redaction/java/)에서 최신 릴리스를 다운로드합니다.  
- **Source Code**: [GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)에서 코드를 확인하고 기여할 수 있습니다.  
- **Support**: [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33)에서 무료 지원 채널을 통해 도움을 받으세요.

---

**마지막 업데이트:** 2026-01-08  
**테스트 환경:** GroupDocs.Redaction 24.9 for Java  
**작성자:** GroupDocs  

---