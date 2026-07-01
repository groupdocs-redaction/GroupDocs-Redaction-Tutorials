---
date: 2026-07-01
description: Java에서 OCR을 사용하여 스캔된 PDF를 편집하고, 민감한 데이터가 포함된 PDF를 제거하며, 이미지 기반 PDF를 GroupDocs.Redaction으로
  편집하는 방법을 배웁니다.
keywords:
- how to redact scanned pdf
- remove sensitive data pdf
- redact image based pdf
schemas:
- author: GroupDocs
  dateModified: '2026-07-01'
  description: Learn how to redact scanned PDF using OCR in Java, remove sensitive
    data PDF, and redact image based PDF with GroupDocs.Redaction.
  headline: How to Redact Scanned PDF with OCR – GroupDocs.Redaction Java
  type: TechArticle
- description: Learn how to redact scanned PDF using OCR in Java, remove sensitive
    data PDF, and redact image based PDF with GroupDocs.Redaction.
  name: How to Redact Scanned PDF with OCR – GroupDocs.Redaction Java
  steps:
  - name: Detect precise word coordinates on scanned pages.
    text: Detect precise word coordinates on scanned pages.
  - name: Apply regex patterns or custom rules across the entire document.
    text: Apply regex patterns or custom rules across the entire document.
  - name: Output a clean, searchable PDF that retains the original layout while guaranteeing
      data privacy.
    text: Output a clean, searchable PDF that retains the original layout while guaranteeing
      data privacy.
  type: HowTo
- questions:
  - answer: Yes. Open the document with its password, run OCR, then apply redaction
      before saving the protected file.
    question: Can I use secure pdf redaction with password‑protected PDFs?
  - answer: The on‑premise version runs entirely on your server, so no internet connection
      is required.
    question: Does Aspose OCR Java work offline?
  - answer: OCR accuracy drops with low resolution. Improve results by pre‑processing
      images (binarization, deskew) before feeding them to the OCR engine.
    question: How accurate is the redaction when the source is a low‑resolution scan?
  - answer: GroupDocs.Redaction offers a preview API that shows redaction rectangles
      on the PDF canvas, allowing you to confirm locations.
    question: Is it possible to preview redaction areas before committing?
  - answer: A full GroupDocs.Redaction license and a valid Aspose OCR Java license
      are required for commercial deployments.
    question: What licensing is needed for production?
  type: FAQPage
title: OCR을 사용하여 스캔된 PDF를 편집하는 방법 – GroupDocs.Redaction Java
type: docs
url: /ko/java/ocr-integration/
weight: 10
---

# 스캔된 PDF 가리기 방법

오늘날 데이터 프라이버시 환경에서 **스캔된 PDF 가리기**는 민감한 문서를 다루는 모든 애플리케이션에 있어 협상할 수 없는 요구 사항입니다. 개인 식별자, 재무 기록 또는 기밀 계약서를 보호하든, 이미지 기반 PDF에서 정보를 신뢰성 있게 삭제할 수 있는 솔루션이 필요합니다. 이 튜토리얼에서는 OCR 기반 가리기의 중요성을 보여주고, Java용 지원 OCR 엔진을 안내하며, GroupDocs.Redaction과 강력한 텍스트 인식 엔진을 결합한 즉시 사용 가능한 예제를 소개합니다.

## 빠른 답변
- **secure pdf redaction은 무엇을 달성하나요?** 민감한 텍스트를 영구적으로 제거하거나 가려서 복구하거나 읽을 수 없게 합니다.  
- **지원되는 OCR 엔진은 무엇인가요?** Aspose OCR (온프레미스 및 클라우드)와 Microsoft Azure Computer Vision이 완전히 호환됩니다.  
- **라이선스가 필요합니까?** 테스트에는 임시 라이선스면 충분하고, 프로덕션 사용에는 정식 라이선스가 필요합니다.  
- **스캔된 PDF를 가릴 수 있나요?** 예—OCR이 텍스트를 추출하면 GroupDocs.Redaction이 이미지 기반 PDF에서도 작동합니다.  
- **Java가 유일한 지원 언어인가요?** 이 개념은 모든 GroupDocs SDK에 적용되지만, 여기의 코드 예시는 Java 전용입니다.

## secure pdf redaction이란?
Secure pdf redaction은 PDF 파일에서 기밀 정보를 영구적으로 삭제하거나 가려서 숨겨진 텍스트가 OCR이나 복사‑붙여넣기 작업으로 복구되지 않도록 합니다. 단순히 텍스트를 가리는 시각적 가리기와 달리, 이 과정은 파일 구조에서 기본 데이터를 제거하여 고급 포렌식 도구를 사용해도 정보를 복구할 수 없게 보장합니다.

## OCR와 GroupDocs.Redaction을 결합하는 이유
OCR은 이미지 전용 페이지를 검색 가능한 텍스트로 변환하여 GroupDocs.Redaction이 정확한 단어 위치를 찾아 삭제할 수 있게 합니다. OCR을 통합하면 다음과 같은 이점을 얻을 수 있습니다:

1. 스캔된 페이지에서 정확한 단어 좌표를 감지합니다.  
2. 정규식 패턴이나 사용자 정의 규칙을 문서 전체에 적용합니다.  
3. 원본 레이아웃을 유지하면서 데이터 프라이버시를 보장하는 검색 가능한 PDF를 출력합니다.

정량적 혜택: GroupDocs.Redaction은 Aspose OCR과 결합했을 때 표준 4코어 서버에서 500 페이지 PDF를 30 초 미만에 처리할 수 있으며, Aspose OCR은 **30개 이상의 언어**를 지원하고 동일 하드웨어에서 **분당 100 페이지**를 인식합니다.

## 사용 가능한 튜토리얼

### [Java와 GroupDocs 및 Microsoft Azure OCR을 사용한 OCR 기반 가리기 구현](./ocr-redaction-groupdocs-java-setup/)
OCR 기반 가리기를 Java용 GroupDocs.Redaction으로 구현하는 방법을 배웁니다. 정확한 텍스트 인식 및 가리기로 데이터 프라이버시를 보장합니다.

### [Aspose OCR와 Java를 사용한 Secure PDF Redaction: GroupDocs.Redaction으로 정규식 패턴 구현](./aspose-ocr-java-pdf-redaction/)
Aspose OCR와 Java를 사용해 PDF에서 민감한 정보를 보호하는 방법을 배웁니다. GroupDocs.Redaction을 활용한 정규식 기반 가리기 가이드를 따라하세요.

## 추가 리소스

- [GroupDocs.Redaction for Java 문서](https://docs.groupdocs.com/redaction/java/)
- [GroupDocs.Redaction for Java API 레퍼런스](https://reference.groupdocs.com/redaction/java/)
- [GroupDocs.Redaction for Java 다운로드](https://releases.groupdocs.com/redaction/java/)
- [GroupDocs.Redaction 포럼](https://forum.groupdocs.com/c/redaction/33)
- [무료 지원](https://forum.groupdocs.com/)
- [임시 라이선스](https://purchase.groupdocs.com/temporary-license/)

## Aspose OCR Java로 secure pdf redaction 시작하기
Aspose OCR 엔진을 로드하고 각 페이지 이미지에 대해 실행한 뒤, 결과 텍스트를 GroupDocs.Redaction에 전달합니다. 이 두 단계 파이프라인을 통해 다음을 수행할 수 있습니다:

- 모든 스캔된 페이지에서 검색 가능한 텍스트를 추출합니다.  
- 정규식(예: SSN, 신용카드 번호)으로 민감한 패턴을 매칭합니다.  
- 최종 PDF에 영구적인 가리기 사각형을 적용합니다.

**Pro tip:** Aspose OCR Java에서 `setUseParallelProcessing(true)`를 활성화하면 다중 페이지 문서 처리 속도가 최대 40 % 가속됩니다. `setUseParallelProcessing(true)`는 OCR 엔진이 여러 페이지를 동시에 처리하도록 구성하여 멀티코어 서버에서 처리량을 향상시킵니다.

## GroupDocs.Redaction과 OCR을 사용해 스캔된 PDF 가리기
PDF를 `RedactionEngine`으로 로드합니다. `RedactionEngine`은 GroupDocs.Redaction Java의 핵심 클래스이며 PDF 문서를 로드하고 가리기 작업을 제공합니다. OCR을 실행해 텍스트 레이어를 얻고, 가리기 규칙을 정의한 뒤, 가려진 파일을 저장합니다. 전체 워크플로는 세 단계로 간결하게 완료되며, 전체 파일을 메모리에 로드하지 않고도 200 MB까지의 PDF를 처리할 수 있습니다.

## 일반적인 함정 및 문제 해결
- **OCR 후 텍스트가 누락됨:** OCR 언어가 올바르게 설정되었는지 확인하세요(예: `setLanguage("en")`).  
- **가리기가 적용되지 않음:** OCR 결과를 `RedactionOptions` 객체에 전달했는지 확인하세요; `RedactionOptions`는 가리기 사각형, 오버레이 색상, 원본 레이아웃 보존 여부 등을 설정합니다. 그렇지 않으면 GroupDocs는 문서를 이미지 전용으로 취급합니다.  
- **성능 병목:** 큰 PDF의 경우 페이지를 배치 처리하고 OCR 엔진 인스턴스를 재사용하여 페이지당 새 인스턴스를 생성하는 것을 피하세요.

## 자주 묻는 질문

**Q: 비밀번호로 보호된 PDF에서도 secure pdf redaction을 사용할 수 있나요?**  
A: 예. 문서를 비밀번호로 열고 OCR을 실행한 뒤, 보호된 파일을 저장하기 전에 가리기를 적용합니다.

**Q: Aspose OCR Java는 오프라인에서도 작동하나요?**  
A: 온프레미스 버전은 서버에서 완전히 실행되므로 인터넷 연결이 필요하지 않습니다.

**Q: 원본이 저해상도 스캔인 경우 가리기의 정확도는 어떨까요?**  
A: 저해상도에서는 OCR 정확도가 떨어집니다. 이미지 전처리(이진화, 기울기 보정)를 수행하면 결과가 개선됩니다.

**Q: 커밋하기 전에 가리기 영역을 미리 볼 수 있나요?**  
A: GroupDocs.Redaction은 PDF 캔버스에 가리기 사각형을 표시하는 프리뷰 API를 제공하여 위치를 확인할 수 있게 합니다.

**Q: 프로덕션에 필요한 라이선스는 무엇인가요?**  
A: 상업적 배포를 위해서는 전체 GroupDocs.Redaction 라이선스와 유효한 Aspose OCR Java 라이선스가 필요합니다.

**마지막 업데이트:** 2026-07-01  
**테스트 환경:** GroupDocs.Redaction 23.11 for Java, Aspose OCR Java 23.6  
**작성자:** GroupDocs

## 관련 튜토리얼

- [Aspose OCR와 Java를 사용한 PDF 가리기 - GroupDocs.Redaction으로 정규식 패턴 구현](/redaction/java/ocr-integration/aspose-ocr-java-pdf-redaction/)
- [GroupDocs.Redaction Java로 PDF 가리기 정책 만들기](/redaction/java/advanced-redaction/master-redaction-groupdocs-java-guide/)
- [GroupDocs.Redaction으로 Java 문서 가리기](/redaction/java/advanced-redaction/java-redaction-groupdocs-guide/)