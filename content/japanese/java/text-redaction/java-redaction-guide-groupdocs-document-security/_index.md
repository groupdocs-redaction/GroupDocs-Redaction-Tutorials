---
date: '2026-08-20'
description: GroupDocs.Redaction を使用して Java ドキュメントのテキストをマスクする方法を学びます。exact‑phrase、regex、color
  replacement、annotation、metadata redaction をカバーし、セキュアなコンプライアンスを実現します。
keywords:
- how to redact text
- replace text with color
- GroupDocs.Redaction Java
- Java document security
- document redaction library
lastmod: '2026-08-20'
og_description: GroupDocs.Redaction を使用して Java ドキュメントのテキストをマスクする方法を学びます。exact‑phrase、regex、color
  replacement、annotation、metadata redaction をカバーします。
og_image_alt: Guide showing Java code redacting text with GroupDocs.Redaction
og_title: GroupDocs.Redaction を使用した Java ドキュメントのテキストのマスク方法
schemas:
- author: GroupDocs
  dateModified: '2026-08-20'
  description: Learn how to redact text in Java documents using GroupDocs.Redaction,
    covering exact‑phrase, regex, color replacement, annotation and metadata redaction
    for secure compliance.
  headline: How to redact text in Java documents with GroupDocs.Redaction
  type: TechArticle
- description: Learn how to redact text in Java documents using GroupDocs.Redaction,
    covering exact‑phrase, regex, color replacement, annotation and metadata redaction
    for secure compliance.
  name: How to redact text in Java documents with GroupDocs.Redaction
  steps:
  - name: '**Add the Maven dependency** (or include the JAR).'
    text: '**Add the Maven dependency** (or include the JAR).'
  - name: '**Configure your license** by calling `License.setLicense("path/to/license.lic")`
      early in your application.'
    text: '**Configure your license** by calling `License.setLicense("path/to/license.lic")`
      early in your application.'
  - name: '**Create a `Redactor` instance** pointing at the source document.'
    text: '**Create a `Redactor` instance** pointing at the source document.'
  - name: '**Initialize the Redactor** with the document you want to process:'
    text: '**Initialize the Redactor** with the document you want to process:'
  - name: '**Define the exact‑phrase rule** and apply it:'
    text: '**Define the exact‑phrase rule** and apply it:'
  - name: '**Save the redacted file** to your output folder:'
    text: '**Save the redacted file** to your output folder:'
  - name: 'Load the document:'
    text: 'Load the document:'
  - name: 'Create a regex rule and apply it:'
    text: 'Create a regex rule and apply it:'
  - name: 'Save the result:'
    text: 'Save the result:'
  - name: 'Load the document:'
    text: 'Load the document:'
  type: HowTo
- questions:
  - answer: Yes. Create each redaction object, call `redactor.apply()` for each, then
      save once.
    question: Can I combine multiple redaction rules in a single pass?
  - answer: Absolutely. Pass the password to the `Redactor` constructor that accepts
      a `LoadOptions` object.
    question: Does GroupDocs.Redaction support password‑protected files?
  - answer: You can call `redactor.preview()` to generate a temporary view that highlights
      the areas to be redacted.
    question: Is it possible to preview redactions before saving?
  - answer: DOCX, PDF, PPTX, XLSX, PNG, JPEG, BMP, and many more—over 30 formats in
      total.
    question: What file formats are supported?
  - answer: Use the metadata erasure feature, remove annotations, and apply exact‑phrase
      or regex redactions to all personal data fields.
    question: How do I ensure the redacted document complies with GDPR?
  type: FAQPage
tags:
- text redaction
- GroupDocs.Redaction
- Java document security
- regex redaction
- metadata removal
title: GroupDocs.Redaction を使用した Java ドキュメントのテキストのマスク方法
type: docs
url: /ja/java/text-redaction/java-redaction-guide-groupdocs-document-security/
weight: 1
---

# Java ドキュメントでテキストを赤塗りする方法（GroupDocs.Redaction）

最新のアプリケーションでは、PDF、Word ファイル、画像内のテキストを**赤塗りする方法**が、コンプライアンスやプライバシーの観点から頻繁に求められます。個人識別子を隠す、機密の注釈を削除する、メタデータを除去する必要がある場合でも、GroupDocs.Redaction for Java を使用すれば、**java document security** を実現するクリーンでプログラム的な方法が提供されます。このチュートリアルでは、ライブラリのセットアップから、Exact‑phrase、regex、color‑based、annotation、metadata の各赤塗りの適用まで、すべての必須ステップを順に説明し、バックエンドサービスに直接赤塗り機能を組み込む方法を示します。

## クイック回答
- **Java ドキュメントの赤塗りを扱うライブラリは何ですか？** GroupDocs.Redaction for Java。  
- **テキストを削除せずに色で置き換えることはできますか？** はい、 “replace text with color” 機能を使用します。  
- **本番環境で使用するにはライセンスが必要ですか？** フル機能を利用するには一時的または有料のライセンスが必要です。  
- **サポートされている Java バージョンは？** JDK 8 以上。  
- **ライブラリの追加方法は Maven だけですか？** Maven が推奨されますが、JAR を手動でダウンロードすることも可能です。

## Java における「テキストの赤塗り」とは何ですか？
**赤塗りは機密コンテンツを永久に削除または隠蔽し、復元できないようにします。** Java では、ファイルをロードし、隠す対象を定義し、赤塗りを適用して、サニタイズされたバージョンを保存します。これにより、下流の利用者はクリーンアップされたドキュメントのみを見ることができます。

## なぜ GroupDocs.Redaction for Java を使用するのか？
ファイルをロードし、ルールを定義すれば、SDK が重い処理を担当します。GroupDocs.Redaction は **30 以上のフォーマット**（DOCX、PDF、PPTX、XLSX、PNG、JPEG、BMP など）をサポートし、ストリームベースのアーキテクチャで大容量ドキュメントを処理します。Exact‑phrase、regex、color‑based、annotation、metadata の赤塗りを提供し、GDPR、HIPAA などの規制に対応する細かな制御が可能です。

## 前提条件
- **Java Development Kit (JDK) 8+** がマシンにインストールされていること。  
- **Maven** が依存管理に使用できること（または JAR を手動でダウンロード可能）。

### 必要なライブラリと依存関係
`pom.xml` に GroupDocs リポジトリと Redaction の依存関係を追加します:

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

公式リリースページから最新の JAR をダウンロードすることもできます: [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### ライセンス取得
本番環境で使用する場合は、一時的またはフルライセンスを取得してください。評価目的で無料トライアルが利用可能です。

## GroupDocs.Redaction for Java のセットアップ
1. **Maven 依存関係を追加**（または JAR を含める）。  
2. アプリケーション開始時に `License.setLicense("path/to/license.lic")` を呼び出して **ライセンスを設定** します。  
   `License` は GroupDocs Redaction のライセンスファイルをロードして適用するためのクラスです。  
3. ソースドキュメントを指す **`Redactor` インスタンスを作成** します。

**`Redactor` クラスは、メモリ効率の良い方法でドキュメントをロード、変更、保存するコアエンジンです。** `Redactor` オブジェクトを取得したら、結果を永続化する前に複数の赤塗りルールをチェーンできます。

これで赤塗りを開始する準備が整いました。

## 実装ガイド

### Exact phrase 赤塗り
特定のフレーズ（例：人物名）をプレースホルダー文字列に置き換えます。

#### Exact‑phrase 赤塗りはどのように機能しますか？
`ExactPhraseRedaction` は、特定の正確なテキスト文字列を削除または置換するルールを表します。ドキュメントをロードし、正確な文字列を対象とする `ExactPhraseRedaction` ルールを作成し、ルールを適用して出力を保存します。SDK はレイアウトを保持しながら一致したテキストを自動的に空白にします。

1. **Redactor を初期化** し、処理したいドキュメントを指定します:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. **Exact‑phrase ルールを定義** し、適用します:

```java
ExactPhraseRedaction redaction = new ExactPhraseRedaction(
    "John Doe", 
    new ReplacementOptions("[Client]"));

redactor.apply(redaction);
```

3. **赤塗りされたファイルを** 出力フォルダーに保存します:

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Redaction applied successfully.");
}
```

### 正規表現によるテキスト置換赤塗り
正規表現を使用してシリアル番号などのパターンを検出し、汎用トークンに置き換えます。

#### 置換付き正規表現赤塗りはどのように機能しますか？
`RegexRedaction` は、正規表現に基づいて一致するテキストを検索・変更するルールを定義します。パターンと置換文字列を含む `RegexRedaction` オブジェクトを提供します。エンジンはドキュメントを走査し、すべての一致を置換し、周囲の書式を保持します。

1. ドキュメントをロードします:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. 正規表現ルールを作成し、適用します:

```java
RegexRedaction redaction = new RegexRedaction(
    "Redaction",
    new ReplacementOptions("[Product]"));

redactor.apply(redaction);
```

3. 結果を保存します:

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Redaction applied successfully.");
}
```

### 正規表現によるカラー置換赤塗り
テキストを削除する代わりに、**テキストをカラーで置換** して視覚的に隠し、基になる文字は保持できます。

#### カラーベースの赤塗りは削除とどう違うのですか？
SDK は一致したテキストを選択した色で塗りつぶし、人間の目には読めなくしますが、ファイルストリーム内には残ります。下流処理のためにドキュメント構造を保持したい場合に有用です。

1. ドキュメントをロードします:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. 正規表現パターンを定義し、置換カラー（例：青）を設定します:

```java
RegexRedaction redaction = new RegexRedaction(
    "\d{2}\s*\d{2}[^\\d]*\d{6}", 
    new ReplacementOptions(Color.BLUE));

redactor.apply(redaction);
```

3. 更新されたファイルを保存します:

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Redaction applied successfully.");
}
```

### アノテーション削除赤塗り
ドキュメントからすべてのアノテーション（コメント、ハイライト等）を除去し、よりクリーンな最終版にします。

#### アノテーションを一括で削除するには？
`AnnotationRedaction` は、コメント、ハイライト、スタンプなどのアノテーションを削除するルールです。すべてのアノテーションタイプを対象とする `AnnotationRedaction` ルールを作成し、適用して変更を永続化します。

1. ファイルをロードします:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. アノテーション削除ルールを適用します:

```java
DeleteAnnotationRedaction redaction = new DeleteAnnotationRedaction();

redactor.apply(redaction);
```

3. 変更を永続化します:

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Annotations deleted successfully.");
}
```

### メタデータ消去赤塗り
プライバシー保護とコンプライアンス基準を満たすため、すべてのメタデータ（作成者、作成日、カスタムプロパティ）を削除します。

#### メタデータ消去はプライバシーをどのように保証しますか？
`MetadataRedaction` は、ドキュメントから組み込みおよびカスタムのメタデータフィールドをクリアします。`MetadataRedaction` ルールは組み込みとカスタムのメタデータフィールドを削除し、ファイルのプロパティバッグに隠れた識別子が残らないようにします。

1. ドキュメントを開きます:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

2. メタデータ消去ルールを適用します:

```java
EraseMetadataRedaction redaction = new EraseMetadataRedaction(MetadataFilters.All);

redactor.apply(redaction);
```

3. サニタイズされたドキュメントを保存します:

```java
if (redactor.save("YOUR_OUTPUT_DIRECTORY/redacted.docx")) {
    System.out.println("Metadata erased successfully.");
}
```

## 実用的な適用例（重要性）
- **法務文書の作成** – 相手方弁護士とドラフトを共有する前にクライアント名を赤塗りします。  
- **医療コンプライアンス** – 手動編集なしで HIPAA に準拠するために患者識別子を削除します。  
- **企業データ保護** – 社内レポート配布前に財務数値や機密情報を隠します。  

これらの手順を自動化することで、手作業の負担が減り、人為的ミスが排除され、数千ファイルにわたって一貫したコンプライアンスが確保されます。

## パフォーマンス上の考慮点
- **ロードではなくストリーム** – 大きなファイルの場合、`Redactor` の `InputStream` を受け取るコンストラクタを使用して、ドキュメント全体をメモリにロードしないようにします。  
- **正規表現パターンを事前コンパイル** して同じ赤塗りを繰り返し実行する際の CPU オーバーヘッドを最大 30 % 削減します。  
- **JVM ヒープを監視** – 赤塗りはメモリ集中的になる可能性があるため、マルチギガバイトのアーカイブをバッチ処理する際はヒープサイズ（`-Xmx2g`）の増加を検討してください。  

## よくある問題とトラブルシューティング
| 症状 | 考えられる原因 | 対策 |
|------|----------------|------|
| `apply` 後に変更がない | ドキュメントパスが間違っている、またはファイルがロックされている | ファイルパスを確認し、ドキュメントが他で開かれていないことを確認してください |
| 正規表現が一致しない | パターン構文エラー | オンラインテスターで正規表現をテストし、バックスラッシュを正しくエスケープしてください |
| カラー置換が見えない | 出力形式がテキストカラーをサポートしていない（例：プレーンテキスト） | スタイルを保持する DOCX や PDF などの形式を使用してください |
| 実行時にライセンスエラー | ライセンスファイルが欠如または無効 | `.lic` ファイルをアクセス可能なディレクトリに配置し、Redactor 使用前に `License.setLicense` を呼び出してください |

## よくある質問

**Q: 複数の赤塗りルールを一度に組み合わせて適用できますか？**  
A: はい。各赤塗りオブジェクトを作成し、各々に `redactor.apply()` を呼び出し、最後に一度だけ保存します。

**Q: GroupDocs.Redaction はパスワード保護されたファイルをサポートしていますか？**  
A: もちろんです。パスワードを `LoadOptions` オブジェクトを受け取る `Redactor` コンストラクタに渡します。

**Q: 保存前に赤塗りをプレビューできますか？**  
A: `redactor.preview()` を呼び出すことで、赤塗り対象領域をハイライトした一時的なビューを生成できます。

**Q: サポートされているファイル形式は何ですか？**  
A: DOCX、PDF、PPTX、XLSX、PNG、JPEG、BMP など、合計で 30 以上の形式がサポートされています。

**Q: 赤塗りされたドキュメントが GDPR に準拠していることをどう確認できますか？**  
A: メタデータ消去機能を使用し、アノテーションを削除し、すべての個人データフィールドに対して Exact‑phrase または regex 赤塗りを適用します。

## 結論
You now have a complete, end‑to‑end guide on **how to redact text** in Java documents using GroupDocs.Redaction. By following the steps for exact‑phrase, regex, color‑based, annotation, and metadata redactions, you can achieve robust **java document security** while keeping your code clean and maintainable. Integrate these snippets into your existing services, automate batch processing, and stay compliant with privacy regulations.

**Last Updated:** 2026-08-20  
**Tested with:** GroupDocs.Redaction 24.9 for Java  
**Author:** GroupDocs

## 関連チュートリアル

- [replace metadata text java – GroupDocs で安全な赤塗り](/redaction/java/metadata-redaction/java-redaction-metadata-text-replacement-guide/)
- [Java 用 GroupDocs.Redaction を使用した Word ドキュメントの画像赤塗り方法 – 包括的ガイド](/redaction/java/image-redaction/redact-images-word-docs-groupdocs-redaction-java/)
- [ファイルパスから GroupDocs Redaction Java ライセンスでドキュメントを赤塗りする方法 – ステップバイステップガイド](/redaction/java/licensing-configuration/implement-groupdocs-redaction-java-license-file-path/)