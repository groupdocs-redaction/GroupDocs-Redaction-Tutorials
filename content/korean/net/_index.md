---
additionalTitle: GroupDocs API References
date: 2026-10-06
description: GroupDocs.Redaction for .NET를 사용하여 PDF 페이지를 마스킹하고, PDF 주석을 제거하며, Excel
  셀을 마스킹하는 방법을 배워보세요 – 문서 마스킹을 위한 안전하고 크로스 플랫폼 API입니다.
keywords:
- how to redact pdf
- remove pdf annotations
- redact excel cells
- redact pdf pages
- load pdf from stream
lastmod: 2026-10-06
linktitle: GroupDocs.Redaction for .NET 튜토리얼
og_description: GroupDocs.Redaction for .NET를 사용하여 PDF 페이지를 빠르게 마스킹하는 방법. 이 API는 PDF
  주석을 제거하고, Excel 셀을 마스킹하며, 30개 이상의 형식에서 민감한 데이터를 보호합니다.
og_image_alt: Guide to redact PDF pages using GroupDocs.Redaction for .NET
og_title: PDF 페이지 마스킹 방법 – GroupDocs.Redaction for .NET
schemas:
- author: GroupDocs
  dateModified: '2026-10-06'
  description: Learn how to redact PDF pages, remove PDF annotations, and redact Excel
    cells using GroupDocs.Redaction for .NET – a secure, cross‑platform API for document
    redaction.
  headline: How to redact PDF pages with GroupDocs.Redaction for .NET
  type: TechArticle
- description: Learn how to redact PDF pages, remove PDF annotations, and redact Excel
    cells using GroupDocs.Redaction for .NET – a secure, cross‑platform API for document
    redaction.
  name: How to redact PDF pages with GroupDocs.Redaction for .NET
  steps:
  - name: load the PDF
    text: You can open a file from disk, a memory stream, or a remote source. The
      API accepts both a file path string and a `Stream` object, which is ideal for
      web services that receive uploads.
  - name: define the pages to redact
    text: Pass a list of zero‑based page indexes or a range string such as `"1-3,5"`
      to the `RemovePages` method. The library validates the range and throws a clear
      exception if a page does not exist.
  - name: save the sanitized document
    text: Call `Save` with the desired output format. You can keep the original PDF,
      export to a rasterized PDF, or stream the result directly to the client response.
  type: HowTo
- questions:
  - answer: Yes, the library removes the specified pages while preserving page numbering,
      bookmarks, and cross‑references for the remaining content.
    question: Can I redact PDF pages without affecting the rest of the document’s
      layout?
  - answer: Absolutely. Use `Redactor.RemoveAnnotations()` to strip all annotation
      objects in a single call.
    question: Is it possible to redact PDF annotations only?
  - answer: Load the workbook with `Redactor.LoadExcel(path)`, then call `Redactor.RedactCell(sheetName,
      cellAddress, RedactionMode.Blackout)` and save.
    question: How do I redact Excel cells directly?
  - answer: Yes, you can pass any `System.IO.Stream` to the `Load` method, which is
      ideal for processing files uploaded via ASP.NET Core controllers.
    question: Does GroupDocs.Redaction support loading PDFs from a stream?
  - answer: Metered licensing lets you pay per‑redaction operation, scaling cost‑effectively
      with usage spikes.
    question: What licensing model is recommended for high‑volume production use?
  type: FAQPage
tags:
- pdf redaction
- groupdocs.redaction
- .net document security
- redact pdf pages
title: GroupDocs.Redaction for .NET를 사용하여 PDF 페이지를 마스킹하는 방법
type: docs
url: /ko/net/
weight: 10
---

# GroupDocs.Redaction for .NET을 사용하여 PDF 페이지를 가리키는 방법

빠르고 신뢰할 수 있게 **PDF 페이지를 가리키는** 작업이 필요하다면, GroupDocs.Redaction for .NET은 30개 이상의 파일 형식에서 민감한 콘텐츠를 제거하는 전체 기능을 갖춘 크로스 플랫폼 API를 제공합니다. 규정 준수 기반 워크플로, 문서 관리 포털, 또는 프라이버시 우선 애플리케이션을 구축하든, 이 라이브러리는 문서 구조를 유지하면서 기밀 데이터를 영구적으로 삭제할 수 있게 해줍니다.

**GroupDocs.Redaction for .NET은 30개 이상의 문서 형식에서 민감한 콘텐츠를 영구적으로 제거할 수 있는 .NET 라이브러리입니다.** 고용량 처리를 지원하며, 전체 문서를 메모리에 로드하지 않고 수백 페이지 파일을 처리할 수 있고, 텍스트를 이미지로 변환하는 래스터화 옵션을 제공하여 추가 보안을 제공합니다.

{{% alert color="primary" %}}
GroupDocs.Redaction for .NET은 .NET 애플리케이션에서 보안 문서 가리키기를 구현하기 위한 포괄적인 튜토리얼 및 예제 모음을 제공합니다. 기본 텍스트 교체부터 고급 메타데이터 정화까지, 이 자료들은 문서에서 민감한 정보를 가리키는 필수 기술을 다룹니다. PDF, Word, Excel, PowerPoint 및 이미지 등 다양한 문서 형식에서 개인 데이터를 영구적으로 제거하는 방법을 정확한 제어와 기밀 콘텐츠의 완전한 제거와 함께 배울 수 있습니다. 단계별 가이드를 통해 표준 및 고급 가리키기 기능을 마스터하여 규정 준수 요구 사항을 충족하고 민감한 정보를 효과적으로 보호할 수 있습니다.
{{% /alert %}}

## 빠른 답변
- **GroupDocs.Redaction이 전체 PDF 페이지를 가리킬 수 있나요?** 예, 단일 API 호출로 단일 페이지 또는 페이지 범위를 삭제할 수 있습니다.  
- **PDF 주석 제거를 지원하나요?** 물론입니다 – 주석, 댓글 및 마크업을 한 번에 제거할 수 있습니다.  
- **PDF로 변환하지 않고 Excel 셀을 가릴 수 있나요?** 예, 라이브러리는 Excel 워크시트를 직접 대상으로 합니다.  
- **스트림에서 PDF를 로드하는 것이 지원되나요?** API는 `Stream` 객체를 받아 메모리 내 처리를 가능하게 합니다.  
- **어떤 .NET 버전과 호환되나요?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## PDF 컨텍스트에서 가리키기란 무엇인가요?
가리키기는 문서에서 민감한 콘텐츠를 영구적으로 제거하거나 가려서 나중에 복구되거나 볼 수 없도록 하는 것입니다. PDF 파일에서는 가리키기가 텍스트, 이미지, 주석 또는 전체 페이지를 대상으로 할 수 있으며, 결과는 원래 레이아웃을 유지하는 정제된 파일이 됩니다.

## 왜 GroupDocs.Redaction for .NET을 사용해야 하나요?
GroupDocs.Redaction for .NET은 대용량 문서를 처리하면서 민감한 데이터를 완전히 제거하는 견고하고 고성능 솔루션을 제공합니다. 내장된 래스터화, 광범위한 형식 지원 및 상세한 감사 로그를 제공하여 규정 준수 기반 애플리케이션 및 엔터프라이즈 환경에 이상적입니다.

- **30개 이상의 지원 형식** – PDF, DOCX, XLSX, PPTX, HTML 및 일반 이미지 형식을 포함합니다.  
- **확장 가능한 성능** – 일반 서버에서 500페이지 PDF를 5초 미만으로 처리하며, 전체 파일을 RAM에 로드하지 않습니다.  
- **내장 래스터화** – 가리키기된 페이지를 이미지로 변환하여 숨겨진 텍스트가 남지 않도록 보장합니다.  
- **규정 준수 준비** – 감사 로그를 통해 GDPR, HIPAA 및 PCI‑DSS 요구 사항을 충족합니다.

## 전제 조건
- .NET Framework 4.5+ **또는** .NET Core 3.1+가 개발 머신에 설치되어 있어야 합니다.  
- 유효한 GroupDocs.Redaction 라이선스(평가용 체험판 제공).  
- 처리하려는 PDF, Excel 또는 Word 파일에 대한 접근 권한.

## PDF 페이지를 단계별로 가리키는 방법

Redactor는 GroupDocs.Redaction의 핵심 클래스이며, 문서를 로드, 수정 및 저장합니다. RemovePages는 로드된 문서에서 지정된 페이지를 제거합니다.

PDF를 로드하고, 제거하려는 페이지를 정의한 뒤, 가리키기를 적용하고 결과를 저장합니다. 다음 직접 답변은 핵심 패턴을 설명합니다:

`Redactor.Load(streamOrPath)`로 대상 PDF를 로드하고, `Redactor.RemovePages(pageNumbers)`를 호출하여 원하지 않는 페이지를 삭제한 뒤, 마지막으로 `Redactor.Save(outputPath)`를 호출합니다 – 이 세 단계 흐름은 대부분의 문서에서 1초 미만에 페이지를 가리킵니다.

### 단계 1: PDF 로드
디스크, 메모리 스트림 또는 원격 소스에서 파일을 열 수 있습니다. API는 파일 경로 문자열과 `Stream` 객체를 모두 허용하므로 업로드를 받는 웹 서비스에 이상적입니다.

### 단계 2: 가리키기할 페이지 정의
`RemovePages` 메서드에 0부터 시작하는 페이지 인덱스 목록이나 `"1-3,5"`와 같은 범위 문자열을 전달합니다. 라이브러리는 범위를 검증하고 페이지가 존재하지 않을 경우 명확한 예외를 발생시킵니다.

### 단계 3: 정제된 문서 저장
원하는 출력 형식으로 `Save`를 호출합니다. 원본 PDF를 유지하거나, 래스터화된 PDF로 내보내거나, 결과를 클라이언트 응답으로 직접 스트리밍할 수 있습니다.

## 일반적인 문제와 해결책
- **Issue:** 가리키기가 작동하는 것처럼 보이지만 원본 텍스트가 여전히 검색 가능합니다.  
  **Solution:** 저장하기 전에 래스터화를 활성화(`Redactor.Rasterize = true`)하면 페이지가 이미지로 변환되어 숨겨진 텍스트 레이어가 제거됩니다.  

- **Issue:** 큰 PDF 파일이 OutOfMemory 예외를 발생시킵니다.  
  **Solution:** `Redactor.Load(stream, loadOptions => loadOptions.EnableMemoryOptimization = true)`를 사용하여 파일을 청크 단위로 처리합니다.  

- **Issue:** 주석이 제거되지 않습니다.  
  **Solution:** 문서를 로드한 후 `Redactor.RemoveAnnotations()`를 호출하십시오; 이 메서드는 댓글, 강조 표시 및 양식 필드를 제거합니다.

## 자주 묻는 질문

**Q: PDF 페이지를 문서 레이아웃에 영향을 주지 않고 가릴 수 있나요?**  
A: 예, 라이브러리는 지정된 페이지를 제거하면서 남은 콘텐츠의 페이지 번호, 북마크 및 교차 참조를 유지합니다.

**Q: PDF 주석만 가릴 수 있나요?**  
A: 물론입니다. `Redactor.RemoveAnnotations()`를 사용하면 한 번에 모든 주석 객체를 제거할 수 있습니다.

**Q: Excel 셀을 직접 가리키려면 어떻게 해야 하나요?**  
A: `Redactor.LoadExcel(path)`로 워크북을 로드한 뒤, `Redactor.RedactCell(sheetName, cellAddress, RedactionMode.Blackout)`를 호출하고 저장합니다.

**Q: GroupDocs.Redaction이 스트림에서 PDF 로드를 지원하나요?**  
A: 예, `System.IO.Stream`을 `Load` 메서드에 전달할 수 있으며, 이는 ASP.NET Core 컨트롤러를 통해 업로드된 파일을 처리하는 데 이상적입니다.

**Q: 대량 프로덕션 사용에 권장되는 라이선스 모델은 무엇인가요?**  
A: 사용량 기반 라이선스는 가리키기 작업당 비용을 지불하도록 하여 사용량 급증에 따라 비용 효율적으로 확장할 수 있습니다.

**마지막 업데이트:** 2026-10-06  
**테스트 환경:** GroupDocs.Redaction 23.10 for .NET  
**작성자:** GroupDocs  

### GroupDocs.Redaction for .NET 튜토리얼 – PDF 페이지를 가리키는 방법

### [시작하기 튜토리얼](./getting-started/)

GroupDocs.Redaction을 처음 사용하는 경우 여기서 시작하십시오. 이 튜토리얼은 설치, 라이선스 및 .NET에서 첫 번째 가리키기 프로젝트를 만드는 과정을 안내합니다. 문서를 열고, 간단한 가리키기 규칙을 정의하고, 정제된 파일을 저장하는 방법을 확인할 수 있습니다.

### [고급 가리키기 기술](./advanced-redaction/)

맞춤형 가리키기 핸들러, 정책, 콜백 및 AI 지원 가리키기를 통해 더 깊이 파고들 수 있습니다. 이 가이드는 **PDF 페이지를 가리키는** 유연한 파이프라인을 구축하고 복잡한 문서 구조를 처리하며, 머신러닝 모델을 통합하여 더 스마트한 콘텐츠 감지를 수행하는 방법을 보여줍니다.

### [주석 가리키기 튜토리얼](./annotation-redaction/)

주석에는 종종 기밀 메모가 포함됩니다. PDF, Word 파일 및 기타 지원 형식에서 주석, 댓글 및 검토 마크업을 찾고, 수정하거나 완전히 제거하는 방법을 배우십시오.

### [문서 정보 튜토리얼](./document-information/)

문서 메타데이터를 이해하는 것이 보안 가리키기의 첫 단계입니다. 이 튜토리얼은 문서 속성을 검색하고, 지원되는 형식을 열거하며, 가리키기를 적용하기 전에 미리보기 이미지를 생성하는 방법을 설명합니다.

### [문서 로딩 튜토리얼](./document-loading/)

문서는 디스크, 스트림 또는 인증 레이어 뒤에 존재할 수 있습니다. 로컬 파일, 메모리 스트림 및 비밀번호로 보호된 문서를 안전하게 로드하는 모범 사례를 배우십시오.

### [문서 저장 튜토리얼](./document-saving/)

가리키기 후에는 정제된 파일을 저장해야 합니다. 이 가이드는 원본 형식으로 저장하고, 래스터화된 PDF로 내보내며, 결과를 클라이언트 측 애플리케이션으로 직접 스트리밍하는 방법을 다룹니다.

### [형식 처리 튜토리얼](./format-handling/)

GroupDocs.Redaction은 다양한 형식을 지원합니다. 다양한 파일 유형을 다루는 방법, 맞춤형 형식 핸들러를 만들고, 라이브러리를 확장하여 특수 문서 표준을 다루는 방법을 살펴보십시오.

### [이미지 가리키기 튜토리얼](./image-redaction/)

이미지는 민감한 시각 데이터를 숨길 수 있습니다. 특정 이미지 영역을 가리키고, 삽입된 사진을 제거하며, 이미지 메타데이터를 정리하여 숨겨진 정보가 남지 않도록 하는 방법을 배우십시오.

### [라이선스 및 구성 튜토리얼](./licensing-configuration/)

적절한 라이선스는 프로덕션 사용에 중요합니다. 이 튜토리얼은 라이선스를 적용하고, 런타임 설정을 구성하며, 확장 가능한 배포를 위해 사용량 기반 라이선스를 구현하는 방법을 보여줍니다.

### [메타데이터 가리키기 튜토리얼](./metadata-redaction/)

메타데이터는 종종 기밀 정보를 누출합니다. 이 가이드를 따라 PDF, Word, Excel 및 PowerPoint 파일에서 문서 속성, 숨겨진 댓글 및 기타 메타데이터를 제거하십시오.

### [OCR 통합 튜토리얼](./ocr-integration/)

스캔된 PDF 또는 이미지와 작업할 때 OCR이 필수적입니다. OCR 엔진을 통합하고, 검색 가능한 텍스트를 추출한 뒤, 민감한 정보가 포함된 **PDF 페이지를 가리키는** 방법을 배우십시오.

### [페이지 가리키기 튜토리얼](./page-redaction/)

때때로 전체 페이지를 제거해야 할 때가 있습니다. 이 튜토리얼은 단일 페이지, 페이지 범위 삭제 및 콘텐츠 기반 조건부 페이지 제거 방법을 보여줍니다.

### [PDF 전용 가리키기 튜토리얼](./pdf-specific-redaction/)

PDF는 레이어, 주석 및 양식 필드와 같은 고유한 기능을 가지고 있습니다. 콘텐츠 필터링 및 문서 무결성 유지 등을 포함한 PDF 전용 가리키기 기술을 마스터하십시오.

### [래스터화 옵션 튜토리얼](./rasterization-options/)

래스터화된 PDF는 콘텐츠를 이미지로 변환하여 데이터 추출을 불가능하게 합니다. 노이즈, 기울기, 그레이스케일 및 테두리를 구성하는 방법을 배우고, 최대 보안을 위해 **래스터화된 PDF** 파일을 저장하는 방법을 알아보십시오.

### [스프레드시트 가리키기 튜토리얼](./spreadsheet-redaction/)

Excel 스프레드시트에는 종종 기밀 셀이 포함됩니다. 이 가이드는 **Excel 셀을 가리키는** 방법, 수식을 숨기고, 민감한 워크시트를 보호하는 방법을 보여줍니다.

### [텍스트 가리키기 튜토리얼](./text-redaction/)

텍스트는 보호해야 할 가장 일반적인 데이터 유형입니다. 정확한 구문 일치, 정규식 가리키기 및 대소문자 구분 검색에 대한 단계별 지침을 따르고, **Word 텍스트를 효율적으로 가리키는** 방법을 포함합니다.

## 관련 튜토리얼
- [주석 제거 방법 – GroupDocs.Redaction .NET용 주석 가리키기 튜토리얼](/redaction/net/annotation-redaction/)
- [GroupDocs.Redaction for .NET을 사용하여 PDF 마지막 페이지 제거 방법](/redaction/net/page-redaction/remove-last-page-pdf-groupdocs-redaction-net/)
- [GroupDocs.Redaction for .NET으로 PDF를 가리키고 래스터화된 PDF로 저장하는 방법](/redaction/net/document-saving/groupdocs-redaction-net-rasterized-pdfs/)