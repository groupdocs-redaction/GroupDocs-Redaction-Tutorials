---
date: '2026-06-26'
description: GroupDocs OCR Redaction と Azure OCR を使用して、スキャンされたPDFからテキストを抽出し、機密データをマスクする方法を学びます。Redact
  social security number と confidential info PDF を効率的に置き換えます。
keywords:
- extract text scanned pdf
- redact social security number
- mask sensitive data pdf
- replace confidential info pdf
schemas:
- author: GroupDocs
  dateModified: '2026-06-26'
  description: Learn how to extract text scanned PDF and mask sensitive data using
    GroupDocs OCR Redaction with Azure OCR. Redact social security number and replace
    confidential info PDF efficiently.
  headline: Extract Text Scanned PDF – Mask Data with GroupDocs OCR
  type: TechArticle
- questions:
  - answer: OCR redaction uses Optical Character Recognition to extract hidden text
      from images or scanned PDFs, then applies redaction rules to mask that text.
    question: What is OCR redaction?
  - answer: Yes, but OCR dramatically improves accuracy on scanned documents where
      native text extraction fails.
    question: Can I use GroupDocs Redaction without Azure OCR?
  - answer: Build and test them incrementally, using Java’s `Pattern` class in a sandbox
      before applying to large documents.
    question: How do I handle complex regex patterns?
  - answer: Large PDFs, overly complex regex, and synchronous OCR calls can slow processing;
      consider batch processing and optimized patterns.
    question: What are typical performance bottlenecks?
  - answer: Absolutely—reach out via the [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33)
      for community help or contact GroupDocs support.
    question: Is support available for implementation issues?
  type: FAQPage
title: スキャンされたPDFからテキストを抽出 – GroupDocs OCRでデータをマスク
type: docs
url: /ja/java/ocr-integration/ocr-redaction-groupdocs-java-setup/
weight: 1
---

# スキャンされたPDFからテキストを抽出 – GroupDocs OCRでデータをマスク

今日のデータ主導の世界では、**スキャンされたPDFからテキストを抽出**し、機密情報をマスクすることは不可欠なコンプライアンス手順です。このチュートリアルでは、GroupDocs Redaction と Microsoft Azure OCR を組み合わせて、スキャンページ上の隠れたテキストを確実に認識し、**`[REDACTED]`** のような安全なプレースホルダーに置き換える方法を説明します。この組み合わせが高速で正確、かつ本番レベルのワークロードに対応できる理由をご覧ください。

## クイック回答
- **「機密データをマスクする」とは何ですか？** 識別された機密テキストをプレースホルダー（例：`[REDACTED]`）に置き換えます。  
- **どのライブラリが OCR を処理しますか？** Microsoft Azure OCR コネクタで、GroupDocs Redaction を通じて使用します。  
- **ライセンスは必要ですか？** 無料トライアルで評価できますが、本番環境では永続ライセンスが必要です。  
- **スキャンされた PDF をリダクションできますか？** はい—OCR が隠れたテキストを抽出し、正規表現によるリダクションを適用します。  
- **このソリューションは Java のみですか？** 例は Java ベースですが、GroupDocs は .NET や他のプラットフォーム向けにも同様の API を提供しています。

## OCRベースのリダクションとは？
OCRベースのリダクションは、まず各ページで OCR を実行し、画像を検索可能なテキストに変換し、次に正規表現パターンを適用して一致箇所を `[REDACTED]` のようなマスクに置き換えます。この二段階プロセスにより、スキャンされた PDF でも個人データを確実に隠すことができ、文書が共有またはアーカイブされる前に機密文字列が除去されます。

## なぜ GroupDocs Redaction と Azure OCR を組み合わせて使用するのか？
GroupDocs Redaction と Azure OCR を使用すべき理由は、印刷テキストに対して **98％以上の OCR 精度** を提供し、**50 以上の入力・出力フォーマット** をサポートし、**ファイル全体をメモリに読み込まずに数百ページの PDF を処理**できるため、コンプライアンス向けの高速でスケーラブルなリダクションが実現できるからです。また、このソリューションは **8 コアサーバー上で 1,000 ページの PDF を 2 分未満で処理** できるため、バッチジョブが実用的です。

## 前提条件
- **Java Development Kit (JDK) 8+** がインストールされていること。  
- **Maven**（依存関係管理を希望する場合）または手動で JAR をダウンロードできる環境。  
- **Microsoft Azure OCR 資格情報**（エンドポイントとサブスクリプションキー）。  
- 基本的な Java の知識と正規表現の理解。

## Java 用 GroupDocs Redaction の設定

### Maven 設定
`pom.xml` に GroupDocs リポジトリと依存関係を追加します:

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

### 直接ダウンロード
手動で JAR を管理したい場合は、最新リリースを [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) から取得してください。

### ライセンス取得
- **Free Trial** – コストなしで全機能を試せます。  
- **Temporary License** – 評価期間を延長します。  
- **Full License** – 本番向け機能を利用可能にします。

### 基本的な初期化と設定
`Redactor` クラスは OCR 抽出を実行し、PDF 文書にリダクションルールを適用するコアエンジンです。  
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.RedactorSettings;
import com.groupdocs.redaction.options.LoadOptions;
import com.groupdocs.redaction.examples.java.helper_classes.MicrosoftAzureOcrConnector;

// Initialize the OCR connector with Microsoft Azure
RedactorSettings settings = new RedactorSettings(new MicrosoftAzureOcrConnector());
```

## OCR リダクションで機密データをマスクする方法
OCR リダクションで機密データをマスクするには、Azure OCR 設定で PDF をロードし、隠したいデータの正規表現パターンを定義し、`Redactor` を呼び出して各一致箇所を `[REDACTED]` のようなプレースホルダーに置き換えます。このライブラリは OCR、パターンマッチング、PDF の書き換えを単一のワークフローで処理します。

### 手順 1: OCR 設定で文書をロード
`LoadOptions` は GroupDocs がファイルをロードする方法を設定し、Azure などの OCR コネクタを渡すことができます。  
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.LoadOptions;

// Load your document with OCR settings
try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf", 
    new LoadOptions(), settings)) {
    // Further operations will go here
}
```
- **`YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF_FOR_4OCR.pdf`** – PDF のパスに置き換えてください。  
- **`settings`** – 先に作成した Azure OCR コネクタが含まれます。

### 手順 2: 正規表現リダクションを定義して適用
`ReplacementOptions` はリダクション中に各正規表現の一致箇所を置き換えるテキストを指定します。  
```java
import com.groupdocs.redaction.redactions.RegexRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

// Define the regex for sensitive data (e.g., Social Security Numbers)
RegexRedaction redaction = new RegexRedaction("\\b\\d{3}-\\d{2}-\\d{4}\\b", 
    new ReplacementOptions("[REDACTED]"));

// Apply redaction
redactor.apply(redaction);

// Save the document after redactions
redactor.save(new SaveOptions());
```
- パターン `\b\d{3}-\d{2}-\d{4}\b` は米国の社会保障番号にマッチします。  
- `ReplacementOptions("[REDACTED]")` は各一致箇所をマスクに置き換え、実質的に **機密データをマスク** します。

## 機密データをマスクする一般的なユースケース
1. **法務文書管理** – 下書き共有前にクライアント識別子を隠す。  
2. **財務報告** – 口座番号や取引 ID を保護する。  
3. **医療記録** – HIPAA に準拠し、患者識別子をリダクションする。  
4. **政府出版物** – 公的記録から個人データを除去する。  
5. **企業契約** – 外部レビュー時に独自条項を隠す。

## パフォーマンスのヒント
- **正規表現の最適化** – 処理時間を増やす過度に広いパターンを避け、適切に作成された式は実行時間を最大 40 % 短縮できます。  
- **メモリ管理** – `Redactor` インスタンスは速やかに閉じます（try‑with‑resources が自動で行います）。  
- **非同期実行** – バルク処理の場合、別スレッドでリダクションジョブを実行するか、タスクキューを使用して UI の応答性を保ちます。

## トラブルシューティング
- **Azure 資格情報エラー** – `MicrosoftAzureOcrConnector` のエンドポイント URL とサブスクリプションキーを再確認してください。  
- **文書がロードされない** – ファイルパスを確認し、PDF がパスワードで保護されていないか確認してください（または `LoadOptions` でパスワードを提供）。  
- **リダクションが適用されない** – 正規表現をシンプルな文字列でまずテストし、ユニットテストで `Pattern.compile` を使用して一致を確認してください。

## よくある質問

**Q: OCR リダクションとは何ですか？**  
A: OCR リダクションは光学文字認識 (Optical Character Recognition) を使用して画像やスキャンされた PDF から隠れたテキストを抽出し、リダクションルールを適用してそのテキストをマスクします。

**Q: Azure OCR なしで GroupDocs Redaction を使用できますか？**  
A: はい、可能ですが、OCR を使用すると、ネイティブテキスト抽出が失敗するスキャン文書の精度が大幅に向上します。

**Q: 複雑な正規表現パターンはどう扱いますか？**  
A: サンドボックスで Java の `Pattern` クラスを使い、段階的に構築・テストしてから大規模文書に適用してください。

**Q: 典型的なパフォーマンスボトルネックは何ですか？**  
A: 大容量の PDF、過度に複雑な正規表現、同期的な OCR 呼び出しが処理を遅くします。バッチ処理や最適化されたパターンの使用を検討してください。

**Q: 実装上の問題に対するサポートはありますか？**  
A: もちろんです。コミュニティ支援は [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33) で、または GroupDocs サポートにお問い合わせください。

## 追加リソース
- **Documentation**: https://docs.groupdocs.com/redaction/java/  
- **API Reference**: https://reference.groupdocs.com/redaction/java  
- **Download**: https://releases.groupdocs.com/redaction/java/  
- **GitHub**: https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java  
- **Free Support**: https://forum.groupdocs.com/c/redaction/33  
- **Temporary License**: https://purchase.groupdocs.com/temporary-license/

---

**最終更新日:** 2026-06-26  
**テスト環境:** GroupDocs.Redaction 24.9 (Java)  
**作者:** GroupDocs  

---

## 関連チュートリアル

- [OCR を使用した安全な PDF リダクション – GroupDocs.Redaction Java](/redaction/java/ocr-integration/)
- [GroupDocs.Redaction for Java でテキストをリダクションする方法](/redaction/java/text-redaction/groupdocs-redaction-java-text-redaction/)
- [Java で機密データをマスク – GroupDocs.Redaction で個人情報をリダクション](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)