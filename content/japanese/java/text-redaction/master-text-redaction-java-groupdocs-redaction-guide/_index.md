---
date: '2026-08-20'
description: JavaでGroupDocs.Redactionを使用し、regexでテキストをマスクする方法をご紹介します。このステップバイステップのチュートリアルでは、regexの適用方法、save
  optionsの設定方法、そしてsensitive dataの保護方法を解説します。
keywords:
- how to redact text
- mask credit card numbers
- remove social security numbers
- redact pdf java
lastmod: '2026-08-20'
og_description: JavaでGroupDocs.Redactionを使用してテキストをマスクする方法を学びます。このガイドでは、regexによるマスク、save‑optionの設定、そしてsensitive
  dataの保護に関するperformance tipsを解説します。
og_image_alt: Guide showing Java code to redact text using GroupDocs.Redaction
og_title: JavaでGroupDocs.Redactionを使用してテキストをマスクする方法
schemas:
- author: GroupDocs
  dateModified: '2026-08-20'
  description: Discover how to redact text using regex in Java with GroupDocs.Redaction.
    This step‑by‑step tutorial shows you how to apply regex, configure save options,
    and protect sensitive data.
  headline: 'How to redact text in Java with GroupDocs.Redaction: A complete guide'
  type: TechArticle
- description: Discover how to redact text using regex in Java with GroupDocs.Redaction.
    This step‑by‑step tutorial shows you how to apply regex, configure save options,
    and protect sensitive data.
  name: 'How to redact text in Java with GroupDocs.Redaction: A complete guide'
  steps:
  - name: import required classes
    text: 'The following imports give you access to the redaction API:'
  - name: initialize redactor and apply regex pattern
    text: '`RegexRedaction` represents a redaction rule based on a regular‑expression
      pattern. The pattern you provide determines which text fragments are replaced.
      - **Regex explanation**: The pattern `\b\d{3}-\d{2}-\d{4}\b` matches U.S. Social
      Security numbers (three digits, a dash, two digits, a dash, four '
  - name: configure save options
    text: '`SaveOptions` controls how the redacted file is written. Adding a suffix
      makes it clear which files have been processed, while preserving the original
      format avoids unwanted conversion. - **Save options**: `setAddSuffix(true)`
      automatically appends “_redacted” to the output filename, preventing acci'
  - name: customize additional save settings
    text: 'You can further tailor the output—such as preserving metadata or flattening
      annotations—by adjusting the `SaveOptions` object. - **Key configuration**:
      Setting `setPreserveMetadata(true)` retains original document properties, which
      is often required for compliance audits.'
  type: HowTo
- questions:
  - answer: It automatically appends a suffix (e.g., `_redacted`) to the output filename,
      making it obvious which files have been processed.
    question: What is the purpose of `setAddSuffix(true)` in SaveOptions?
  - answer: Absolutely. Any valid Java regular expression can be supplied to `RegexRedaction`
      to target emails, phone numbers, custom IDs, etc.
    question: Can I use regex patterns other than numbers for text redaction?
  - answer: Wrap the redaction logic in a try‑catch block, log the exception, and
      always close the `Redactor` in a finally clause to release resources.
    question: How should I handle errors during redaction?
  - answer: Yes. GroupDocs.Redaction works with PDF, DOCX, PPTX, and many other formats.
    question: Is PDF redaction supported?
  - answer: Use batch processing, keep regex patterns simple, and monitor memory usage
      with profiling tools.
    question: What are best practices for large‑scale redaction projects?
  type: FAQPage
tags:
- text redaction
- GroupDocs.Redaction
- Java document processing
- regex redaction
- PDF redaction
title: JavaでGroupDocs.Redactionを使用してテキストをマスクする方法：完全ガイド
type: docs
url: /ja/java/text-redaction/master-text-redaction-java-groupdocs-redaction-guide/
weight: 1
---

# JavaでGroupDocs.Redactionを使用してテキストを編集する方法：完全ガイド

今日の急速に変化するデジタル世界では、ドキュメント内の**テキストを編集する方法**は多くの開発者が直面する課題です。個人データの保護、規制への準拠、または単にドラフトを整理する場合でも、本ガイドではJava向けGroupDocs.Redactionを使用して**正規表現ベースの編集を迅速かつ安全に適用する方法**を解説します。編集が重要な理由、ライブラリの設定方法、そして高性能処理のベストプラクティスを学べます。

## 簡単な回答
- **GroupDocs.Redactionの主な目的は何ですか？** 50以上のドキュメント形式で機密テキストを検出しマスクする信頼性の高い API を提供します。  
- **正規表現で編集を適用するにはどうすればよいですか？** パターンを指定して `RegexRedaction` オブジェクトを作成し、`Redactor.apply()` メソッドに渡します。  
- **ライセンスは必要ですか？** 開発には無料トライアルが使用でき、製品環境では有料ライセンスで全機能が利用可能になります。  
- **PDFだけでなくDOCXファイルも編集できますか？** はい、GroupDocs.RedactionはPDF、DOCX、PPTXなど多数の形式をサポートしています。  
- **パフォーマンスを向上させる最善の方法は何ですか？** `Redactor` インスタンスは速やかに閉じ、正規表現パターンはシンプルに保ち、ファイルはバッチ処理します。

## テキスト編集とは何か、そしてなぜ重要なのか
テキスト編集は、ドキュメントから機密情報を永久に削除または隠蔽し、社会保障番号、クレジットカード情報、医療記録などの機密データが不正な者に復元または閲覧されないようにします。元の文字を上書きしたりマスクに置き換えることで、隠された内容がコピー＆ペーストや OCR ツールで抽出できなくなります。これによりプライバシー規制への準拠が確保され、個人が身元盗難やデータ漏洩から保護されます。

## テキスト編集に正規表現を使用する理由は？
正規表現を使用すると、電話番号やクレジットカード番号など、さまざまなデータ形式にマッチする柔軟なパターンを定義できます。GroupDocs.Redaction と組み合わせて正規表現を使用すれば、隠す対象を正確に制御でき、実装を簡潔かつ保守しやすくなります。

## 前提条件
- **Java Development Kit (JDK)** がインストールされていること（Java 8 以上）。  
- Java の構文と正規表現に関する基本的な知識。  
- コードの実行とデバッグができる **IntelliJ IDEA** や **Eclipse** などの IDE。  

## Java向けGroupDocs.Redactionの設定
まず、ライブラリをプロジェクトに追加します。

### Maven の設定
Maven を使用している場合は、以下を `pom.xml` に挿入してください：

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
あるいは、最新の JAR を [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) からダウンロードしてください。

### 基本的な初期化
`Redactor` はドキュメントを開き、編集ルールを適用し、出力を書き込むコアクラスです。

ライブラリが利用可能になったら、ドキュメントの編集を開始できます：

```java
// Import the necessary classes from GroupDocs.Redaction
import com.groupdocs.redaction.Redactor;

public class RedactionExample {
    public static void main(String[] args) {
        // Initialize the redactor with your document path
        final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
        // Ensure you close resources after operations
        try { /* Your code here */ } finally { redactor.close(); }
    }
}
```

## Javaで正規表現を使用してテキストを編集する方法は？
このプロセスは、ソースファイルを `Redactor` インスタンスにロードし、マッチパターンを定義した `RegexRedaction` ルールを作成し、`redactor.apply()` でルールを適用し、最後に `SaveOptions` を使用して変更後のドキュメントを保存することです。これらの手順に従うことで、サポートされているすべての形式で機密文字列を確実に検出しマスクできます。

`Redactor` クラスはドキュメントを開き、編集ルールを適用し、出力ファイルを書き込むコアコンポーネントです。内部でリソースを管理するため、処理後はメモリ解放のために必ず閉じる必要があります。

### ステップ 1: 必要なクラスをインポート
以下のインポートにより、編集 API にアクセスできます：

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.redactions.RegexRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;
```

### ステップ 2: Redactor を初期化し、正規表現パターンを適用
`RegexRedaction` は正規表現パターンに基づく編集ルールを表します。指定したパターンにより、どのテキスト断片が置換されるかが決まります。

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
try {
    // Define a regex pattern to find sequences of numbers and apply a replacement color.
    // The pattern: Two digits, optional whitespace, two more digits, non-digit characters,
    // followed by six digits.
    redactor.apply(new RegexRedaction("\\d{2}\\s*\\d{2}[^\\d]*\\d{6}", 
        new ReplacementOptions(java.awt.Color.BLUE)));
```

- **正規表現の説明**: パターン `\b\d{3}-\d{2}-\d{4}\b` は米国の社会保障番号（3 桁、ハイフン、2 桁、ハイフン、4 桁）にマッチします。`ReplacementOptions` を使用すると、黒の実体オーバーレイまたはカスタムテキストマスクを選択できます。

### ステップ 3: 保存オプションを設定
`SaveOptions` は編集後のファイルの書き込み方法を制御します。サフィックスを追加することで、どのファイルが処理されたかが明確になり、元の形式を保持することで不要な変換を防ぎます。

```java
    // Configure save options
    SaveOptions saveOptions = new SaveOptions();
    saveOptions.setAddSuffix(true);  // Adds suffix to indicate processing
    saveOptions.setRasterizeToPDF(false);  // Preserves original format

    // Save the redacted document
    redactor.save(saveOptions);
} finally {
    redactor.close();  // Always close resources to prevent memory leaks
}
```

- **保存オプション**: `setAddSuffix(true)` は出力ファイル名に自動的に “_redacted” を付加し、誤って上書きすることを防ぎます。

### ステップ 4: 追加の保存設定をカスタマイズ
`SaveOptions` オブジェクトを調整することで、メタデータの保持や注釈のフラット化など、出力をさらに細かくカスタマイズできます。

```java
import com.groupdocs.redaction.options.SaveOptions;

SaveOptions saveOptions = new SaveOptions();
saveOptions.setAddSuffix(true);  // Indicates processing by adding a suffix
saveOptions.setRasterizeToPDF(false);  // Keeps original format intact
```

- **重要な設定**: `setPreserveMetadata(true)` を設定すると、元のドキュメントプロパティが保持され、コンプライアンス監査でよく求められます。

## 実用的な適用例
**テキストを編集する方法** が不可欠な実際のシナリオ：

1. **法務文書** – 外部顧問とドラフトを共有する前にクライアント識別子を隠す。  
2. **医療記録** – 患者名、ID、健康番号をマスクして HIPAA に準拠する。  
3. **財務報告書** – 四半期サマリー配布時に機密の口座番号を削除する。  

## パフォーマンス上の考慮点
- **メモリ管理**: 常に `redactor.close()` を呼び出してファイルハンドルとネイティブリソースを解放します。  
- **効率的な正規表現**: シンプルなパターンは高速に動作します。可能な限りアトミックグループを使用して過剰なバックトラッキングを回避してください。  
- **バッチ処理**: 大量のドキュメントセットでは、ヒープ使用量を予測可能に保つために 20〜50 件ずつバッチで処理します。  

## 一般的な問題と解決策
| 問題 | 解決策 |
|-------|----------|
| **正規表現がマッチしすぎる** | オンライン正規表現テスターでパターンをテストし、文字クラスを絞り込んでください。 |
| **出力ファイル名の競合** | `setAddSuffix(true)` を使用するか、`saveOptions.setOutputPath()` でカスタム出力パスを指定してください。 |
| **大きな PDF でのメモリリーク** | PDF をページ単位で処理するか、JVM ヒープサイズを増やします（`-Xmx2g`）。 |

## よくある質問

**Q: SaveOptions の `setAddSuffix(true)` の目的は何ですか？**  
A: 出力ファイル名にサフィックス（例: `_redacted`）を自動的に付加し、どのファイルが処理されたかが明確になります。

**Q: テキスト編集に数字以外の正規表現パターンを使用できますか？**  
A: もちろんです。メールアドレス、電話番号、カスタム ID など、任意の有効な Java 正規表現を `RegexRedaction` に渡して対象にできます。

**Q: 編集中にエラーが発生した場合、どのように対処すべきですか？**  
A: 編集ロジックを try‑catch ブロックで囲み、例外をログに記録し、finally 節で必ず `Redactor` を閉じてリソースを解放してください。

**Q: PDF の編集はサポートされていますか？**  
A: はい。GroupDocs.Redaction は PDF、DOCX、PPTX など多数の形式で動作します。

**Q: 大規模な編集プロジェクトのベストプラクティスは何ですか？**  
A: バッチ処理を使用し、正規表現パターンはシンプルに保ち、プロファイリングツールでメモリ使用量を監視してください。

## 追加リソース
- **ドキュメント**: [GroupDocs Redaction Documentation](https://docs.groupdocs.com/redaction/java/)  
- **API リファレンス**: [GroupDocs API Reference](https://apireference.groupdocs.com/redaction/java)

---

**最終更新日:** 2026-08-20  
**テスト環境:** GroupDocs.Redaction 24.9 for Java  
**作者:** GroupDocs

## 関連チュートリアル

- [機密データをマスクする Java – GroupDocs.Redaction ガイド](/redaction/java/getting-started/)
- [機密データをマスクする Java – GroupDocs.Redaction で個人情報を編集](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)
- [Aspose OCR と Java で PDF を編集する方法 - GroupDocs.Redaction を使用した正規表現パターンの実装](/redaction/java/ocr-integration/aspose-ocr-java-pdf-redaction/)