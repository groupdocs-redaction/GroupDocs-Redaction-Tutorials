---
date: 2026-07-15
description: GroupDocs.Redaction for .NET를 사용하여 custom redaction handler를 만들고 새로운
  file format support를 추가하는 방법을 배웁니다.
keywords:
- create custom redaction handler
- add new file format
- GroupDocs.Redaction format handling
lastmod: 2026-07-15
og_description: GroupDocs.Redaction for .NET와 함께 custom redaction handler를 만들고 새로운
  file format support를 추가하세요. 형식 처리 확장을 위한 단계별 가이드를 확인하세요.
og_image_alt: Guide to creating a custom redaction handler in GroupDocs.Redaction
  for .NET
og_title: Custom Redaction Handler 만들기 – GroupDocs.Redaction .NET
schemas:
- author: GroupDocs
  dateModified: '2026-07-15'
  description: Learn how to create custom redaction handler and add new file format
    support using GroupDocs.Redaction for .NET.
  headline: Create Custom Redaction Handler in GroupDocs.Redaction .NET
  type: TechArticle
tags:
- redaction handler
- GroupDocs.Redaction
- .NET document processing
- custom format extension
title: GroupDocs.Redaction .NET에서 Custom Redaction Handler 만들기
type: docs
url: /ko/net/format-handling/
weight: 14
---

# GroupDocs.Redaction .NET에서 사용자 정의 레드랙션 핸들러 만들기

우리의 포맷 처리 튜토리얼을 통해 .NET 개발자를 위한 GroupDocs.Redaction 기능을 확장하세요. 이 허브에서는 **custom redaction handler**를 만들고 **new file format** 지원을 추가하는 방법, 일반 텍스트 문서 작업, 다양한 문서 유형을 프로그래밍 방식으로 처리하는 방법을 배웁니다. 이 가이드에는 바로 실행할 수 있는 C# 예제가 포함되어 있어 애플리케이션이 보호할 수 있는 파일 범위를 빠르게 확장할 수 있습니다.

## 빠른 개요

- **얻을 수 있는 것:** 제품 업데이트를 기다리지 않고 사용자 정의 콘텐츠 유형을 레드랙션하고 추가 파일 확장자를 지원할 수 있습니다.  
- **대상:** 엄격한 프라이버시 제어가 필요한 문서 중심 솔루션을 구축하는 .NET 개발자.  
- **전제 조건:** .NET 6+ (또는 .NET Framework 4.7.2+), 유효한 GroupDocs.Redaction 라이선스, 그리고 기본 C# 지식.  

## 사용자 정의 레드랙션 핸들러란 무엇인가요?

**custom redaction handler**는 GroupDocs.Redaction에 내장 패턴에 포함되지 않은 콘텐츠를 찾고, 해석하고, 레드랙션하는 방법을 알려주는 사용자 정의 구성 요소입니다. 이 핸들러를 구현하면 독점 데이터 포맷이나 고유 비즈니스 식별자를 완전히 제어할 수 있습니다.

## 사용자 정의 레드랙션 핸들러를 만드는 방법은?

**IRedactionHandler**는 사용자 정의 레드랙션 로직에 대한 계약을 정의하는 인터페이스입니다.  
**Redactor**는 레드랙션 작업을 관리하는 핵심 클래스입니다.  
**AddHandler**는 Redactor 인스턴스에 사용자 정의 핸들러를 등록합니다.  
**Redact**는 구성된 핸들러를 기반으로 레드랙션을 실행합니다.  

Redaction 엔진을 로드하고, 핸들러를 등록한 뒤 레드랙션 프로세스를 호출합니다 – 모두 세 단계로 간결하게 수행됩니다. 첫 번째로, 문서에서 사용자 정의 토큰을 스캔하는 로직을 포함한 `IRedactionHandler` 인터페이스를 구현합니다. 그 다음, `AddHandler`를 사용해 `Redactor` 인스턴스에 핸들러를 추가합니다. 마지막으로, `Redact`를 호출해 변경 사항을 적용합니다. 이 패턴은 PDF, 이미지 및 모든 지원 포맷에서 작동하며, 표준 패턴이 놓치는 데이터를 보호할 수 있게 해줍니다.

## 새 파일 포맷을 추가하는 방법은?

**SupportedFormats**는 Redaction 엔진이 인식하는 파일 확장자를 보관하는 컬렉션입니다. `SupportedFormats` 컬렉션을 확장하여 Redaction 엔진에 새 파일 확장자를 등록합니다. 입력 파일을 GroupDocs.Redaction이 처리할 수 있는 포맷으로 변환하는 파서를 제공하고, 해당 확장자를 파서에 매핑합니다. 등록이 완료되면 엔진은 새 포맷을 기존 네이티브 타입처럼 취급하여 전체적으로 원활한 레드랙션을 가능하게 합니다.

## 맞춤 포맷 처리를 위해 GroupDocs.Redaction을 사용하는 이유는?

GroupDocs.Redaction은 **70개 이상의 입력 및 출력 포맷**을 지원하며, 전체 문서를 메모리에 로드하지 않고 **2 GB**까지의 파일을 처리하여 엔터프라이즈 환경에서 고처리량 레드랙션을 제공합니다. 확장 가능한 아키텍처 덕분에 30분 이내에 사용자 정의 핸들러를 플러그인할 수 있어 개발 시간을 단축하고 타사 전처리 도구의 필요성을 없앱니다.

## 사용 가능한 튜토리얼

### [GroupDocs.Redaction .NET에서 파일 유형 확장: 사용자 정의 확장에 대한 단계별 가이드](./extend-groupdocs-redaction-net-custom-extensions/)
GroupDocs.Redaction for .NET을 사용하여 사용자 정의 확장으로 지원 파일 유형을 확장하는 방법을 배우고, 다양한 포맷에서 안전한 문서 레드랙션을 보장합니다.

### [GroupDocs.Redaction .NET으로 지원 파일 포맷 목록 구현](./groupdocs-redaction-net-supported-formats-listing/)
지원 파일 포맷을 나열하고, 문서 관리 시스템을 간소화하며, 성능을 최적화하기 위해 GroupDocs.Redaction .NET을 사용하는 방법을 배웁니다.

## 추가 리소스

- [GroupDocs.Redaction for Net 문서](https://docs.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction for Net API 참조](https://reference.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction for Net 다운로드](https://releases.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction 포럼](https://forum.groupdocs.com/c/redaction/33)
- [무료 지원](https://forum.groupdocs.com/)
- [임시 라이선스](https://purchase.groupdocs.com/temporary-license/)

---

**마지막 업데이트:** 2026-07-15  
**테스트 대상:** GroupDocs.Redaction 23.12 for .NET  
**작성자:** GroupDocs

## 관련 튜토리얼

- [GroupDocs.Redaction .NET에서 파일 유형 확장: 사용자 정의 확장에 대한 단계별 가이드](/redaction/net/format-handling/extend-groupdocs-redaction-net-custom-extensions/)
- [GroupDocs.Redaction .NET으로 지원 파일 포맷 목록 구현](/redaction/net/format-handling/groupdocs-redaction-net-supported-formats-listing/)
- [GroupDocs.Redaction .NET용 포맷 처리 튜토리얼](/redaction/net/format-handling/)