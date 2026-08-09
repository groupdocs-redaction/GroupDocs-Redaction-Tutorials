---
date: '2026-08-09'
description: GroupDocs.Redaction Java API を使用して、Excel スプレッドシート内の個人データを非表示にし、メールアドレスをマスクする方法を学びます。
keywords:
- how to hide personal data
- mask email addresses excel
- GroupDocs.Redaction Java
- Excel redaction tutorial
lastmod: '2026-08-09'
og_description: GroupDocs.Redaction Java API を使用して、Excel ファイル内の個人データを非表示にし、メールアドレスをマスクする手順をステップバイステップで紹介します
  – GDPR コンプライアンスに対応した迅速で安全なソリューションです。
og_image_alt: Guide showing Java code that redacts email addresses in an Excel spreadsheet
og_title: GroupDocs Java を使用して Excel で個人データを非表示にする方法
schemas:
- author: GroupDocs
  dateModified: '2026-08-09'
  description: Learn how to hide personal data and mask email addresses in Excel spreadsheets
    using the GroupDocs.Redaction Java API.
  headline: How to hide personal data in Excel with GroupDocs Java
  type: TechArticle
- description: Learn how to hide personal data and mask email addresses in Excel spreadsheets
    using the GroupDocs.Redaction Java API.
  name: How to hide personal data in Excel with GroupDocs Java
  steps:
  - name: '**Partner data exchange** – Automatically strip customer emails before
      sending spreadsheets to vendors.'
    text: '**Partner data exchange** – Automatically strip customer emails before
      sending spreadsheets to vendors.'
  - name: '**Internal audit preparation** – Anonymize employee data during compliance
      reviews.'
    text: '**Internal audit preparation** – Anonymize employee data during compliance
      reviews.'
  - name: '**Scheduled reporting** – Embed the redaction step into nightly batch jobs
      that generate distribution‑ready reports.'
    text: '**Scheduled reporting** – Embed the redaction step into nightly batch jobs
      that generate distribution‑ready reports.'
  type: HowTo
- questions:
  - answer: Extend the pattern to include additional allowed characters (e.g., “+”
      or “_”) and test against a larger sample set, then re‑run the redaction.
    question: My regex still misses some corporate email formats. What should I do?
  - answer: Yes. Create a separate `CellFilter` for each column and invoke `redactor.apply`
      for each filter sequentially.
    question: Can I redact more than one column in a single pass?
  - answer: The library processes sheets incrementally, so files up to several gigabytes
      can be redacted as long as you enable streaming and close the `Redactor` after
      each file.
    question: Is GroupDocs.Redaction able to handle Excel files larger than 1 GB?
  - answer: Inspect the `RedactorChangeLog` returned by `apply`; a non‑failed status
      indicates success, while any errors are listed with line numbers and cell references.
    question: How do I capture redaction results or errors?
  - answer: Absolutely. Build the placeholder string dynamically (e.g., `"[redacted:"
      + UUID.randomUUID() + "]"`) and pass it to `ReplacementOptions`.
    question: Can I use a custom placeholder that includes a unique token per row?
  type: FAQPage
tags:
- hide personal data
- GroupDocs.Redaction
- Java Excel processing
- data privacy
title: GroupDocs Java を使用して Excel で個人データを非表示にする方法
url: /ja/java/spreadsheet-redaction/redact-emails-excel-groupdocs-redaction-java/
weight: 1
---

# GroupDocs Java を使用して Excel の個人データを非表示にする方法

このガイドでは、GroupDocs.Redaction Java API を使用して Excel ワークブック内の個人データ、特にメールアドレスを**非表示にする方法**を学びます。GDPR、CCPA、または社内プライバシーポリシーへの準拠が必要な場合でも、ここで示すアプローチにより、リダクションを安全に自動化し、元のファイルはそのままにして、配布用のクリーンなバージョンを生成できます。

## 簡潔な回答
- **「個人データを非表示にする」とは何ですか？** ファイルから個人を特定できる情報（PII）を永続的にマスクまたは削除し、読み取れなくなることを意味します。  
- **リダクションを実行するライブラリはどれですか？** GroupDocs.Redaction for Java。  
- **サンプルを実行するのにライセンスは必要ですか？** テストには無料トライアルで動作しますが、商用利用には本番向けライセンスが必要です。  
- **プレースホルダーのテキストをカスタマイズできますか？** はい。メールアドレスを「[redacted email]」のような任意の文字列に置き換えることができます。  
- **この方法は大規模なスプレッドシートに適していますか？** はい。「Performance considerations」セクションのパフォーマンスに関するヒントに従えば適用できます。

## 個人データを非表示にするとは何ですか？
**個人データを非表示にする** は、名前、電話番号、メールアドレスなど、個人を直接または間接的に特定できる情報を不可逆的に削除またはマスクすることを指します。このプロセスにより、生成されたファイルから対象者を再特定できなくなります。

## Java 用 GroupDocs.Redaction を使用する理由は？
GroupDocs.Redaction は **30 以上の入力および出力フォーマット** をサポートし、**最大 500,000 行** のワークブックをファイル全体をメモリに読み込むことなく処理でき、従来のファイル解析ソリューションと比較して **メモリ使用量を最大 80 % 削減** します。これらの定量的な利点により、エンタープライズ向けデータプライバシーパイプラインの最適な選択肢となります。

## 前提条件
- Java Development Kit (JDK) 8 以上。  
- Maven ビルドファイルの基本的な知識。  
- GroupDocs.Redaction Java ライブラリへのアクセス（Maven または公式リリースページからダウンロード可能）。

## Java 用 GroupDocs.Redaction の設定

### Maven プロジェクトに GroupDocs.Redaction を追加するには？
`pom.xml` ファイルに GroupDocs リポジトリと Redaction の依存関係を追加します（[GroupDocs.Redaction releases](https://releases.groupdocs.com/redaction/java/) を参照）。その後、`mvn clean install` を実行してアーティファクトを取得します。

```text
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
```

### GroupDocs.Redaction のライセンスを取得するには？
GroupDocs は 3 つのライセンスオプションを提供しています（[GroupDocs’ website](https://purchase.groupdocs.com/temporary-license/) を参照）。

- **Free trial** – 機能制限付きの評価で、クレジットカードは不要です。  
- **Temporary license** – GroupDocs のウェブサイトから取得できる 30 日間の評価キーです。  
- **Full license** – 販売ポータルで購入できる永続的な本番用ライセンスです。

```text
```java
import com.groupdocs.redaction.Redactor;

public class RedactEmails {
    public static void main(String[] args) {
        // Initialize the redactor with your document path
        try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_XLSX")) {
            // Your redaction logic will go here
        }
    }
}
```
```

## 実装ガイド

### Excel ファイル用の Redactor インスタンスを作成するには？
`Redactor` クラスはドキュメントを読み込み、リダクション操作を提供する主要エントリーポイントです。  
ソースワークブックを指す `Redactor` オブジェクトをインスタンス化します。`Redactor` クラスはすべてのリダクション操作のエントリーポイントであり、元のファイルをディスク上に残しながら、ファイルを管理されたメモリ構造にロードします。

```text
```java
import com.groupdocs.redaction.Redactor;

public class RedactEmails {
    public static void main(String[] args) {
        try (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_XLSX")) {
            // Proceed to the next steps for redaction
        }
    }
}
```
```

### リダクションを単一のワークシートと列に限定するには？
`CellFilter` クラスを使用すると、リダクション対象となるワークシートと列を指定できます。`CellFilter` を使用して対象シート名と列インデックスを設定します。`CellFilter` クラスはリダクションエンジンが評価する前にセルをフィルタリングし、意図したセルだけが処理されるようにします。

```text
```java
import com.groupdocs.redaction.redactions.CellFilter;

// Create and configure the filter
CellFilter filter = new CellFilter();
filter.setColumnIndex(1); // Targeting the second column (index starts at 0)
filter.setWorkSheetName("Customers"); // Specify the worksheet name
```
```

### ほとんどのメールアドレスにマッチする正規表現パターンを定義するには？
`java.util.regex` の `Pattern` クラスは、テキストマッチに使用されるコンパイル済み正規表現を表します。一般的なメール形式をキャプチャする正規表現で `Pattern` オブジェクトを作成します。以下のパターンは、RFC‑5322 に準拠したアドレスの大部分にマッチし、形式が不正な文字列は無視します。

```text
```java
import java.util.regex.Pattern;

// Define regex pattern for matching emails
Pattern expression = Pattern.compile("^\\w+([-+.']\\w+)*@\\w+([-.]\\w+)*\\.\\w+([-.]\\w+)*$");
```
```

### リダクションを適用し、メールアドレスをプレースホルダーに置き換えるには？
`ReplacementOptions` クラスは、マッチしたコンテンツをどのように置き換えるか（プレースホルダーのテキストなど）を定義します。フィルタ、パターン、`ReplacementOptions` インスタンスを組み合わせます。`ReplacementOptions` クラスを使用すると、各リダクションされたセルに表示される正確なプレースホルダー文字列を設定できます。

```text
```java
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.RedactorChangeLog;
import com.groupdocs.redaction.redactions.CellColumnRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

// Apply redaction
RedactorChangeLog result = redactor.apply(new CellColumnRedaction(filter, expression, new ReplacementOptions("[customer email]")));

// Save changes if successful
if (result.getStatus() != RedactionStatus.Failed) {
    SaveOptions saveOptions = new SaveOptions();
    saveOptions.setAddSuffix(true); // Add a suffix to the saved file name
    redactor.save(saveOptions);
}
```
```

## 一般的な落とし穴とトラブルシューティング
- **Regex does not catch all cases** – 正規表現がすべてのケースを捕捉できない場合は、データの代表的なサンプルでテストし、必要に応じて文字クラスを調整してください。  
- **Incorrect column index** – 列インデックスは 0 から始まることを覚えておいてください。列 B はインデックス 1 です。  
- **Worksheet name case‑sensitivity** – Excel に表示されている正確なシート名を使用してください。「Customers」≠「customers」。  
- **Resource leaks** – `Redactor` を try‑with‑resources ブロックでラップ（上記参照）し、ネイティブリソースが速やかに解放されるようにしてください。

## Excel で個人データを非表示にする理由は？
Excel で個人データを非表示にすると、個人を特定できる情報がすべて除去され、ファイルから個人を追跡できなくなります。これによりプライバシーが保護され、規制要件を満たし、外部関係者とスプレッドシートを共有したりデータを公開したりする際の偶発的な漏洩を防止します。

- **Regulatory compliance** – GDPR、CCPA、業界固有のプライバシー要件を満たします。  
- **Risk mitigation** – 外部パートナーとファイルを共有する際の PII の偶発的な露出を防止します。  
- **Audit readiness** – アーカイブされたデータセットから機密値を永続的に除去し、クリーンで不変な監査トレイルを維持します。

## 実用的な活用例
1. **Partner data exchange** – ベンダーにスプレッドシートを送る前に顧客のメールアドレスを自動的に除去します。  
2. **Internal audit preparation** – コンプライアンスレビュー時に従業員データを匿名化します。  
3. **Scheduled reporting** – 配布可能なレポートを生成する夜間バッチジョブにリダクションステップを組み込みます。

## パフォーマンスに関する考慮事項
- **Batch processing** – 複数ファイルで単一の `Redactor` インスタンスを再利用し、JVM のオーバーヘッドを削減します。  
- **Memory management** – API はシートを1つずつ処理します。100 MB を超えるワークブックの場合は、行をチャンクに分けて処理し、ヒープ使用量を低く保ちます。  
- **Large datasets** – 10 万行超のファイルを扱う場合は、ストリーミングモード（バージョン 24.9 で利用可能）を有効にし、メモリ消費を 200 MB 未満に抑えます。

## よくある質問
**Q: 正規表現がまだ一部の企業メール形式を捕捉できません。どうすればよいですか？**  
A: パターンに追加の許可文字（例: “+” や “_”）を含めるよう拡張し、より大きなサンプルセットでテストした後、リダクションを再実行してください。

**Q: 1 回の処理で複数の列をリダクションできますか？**  
A: はい。各列ごとに別々の `CellFilter` を作成し、各フィルタに対して順番に `redactor.apply` を呼び出します。

**Q: GroupDocs.Redaction は 1 GB を超える Excel ファイルを処理できますか？**  
A: ライブラリはシートをインクリメンタルに処理するため、ストリーミングを有効にし、各ファイル処理後に `Redactor` を閉じることで、数ギガバイトまでのファイルをリダクションできます。

**Q: リダクション結果やエラーを取得するには？**  
A: `apply` が返す `RedactorChangeLog` を確認してください。失敗でないステータスは成功を示し、エラーがある場合は行番号とセル参照と共に一覧表示されます。

**Q: 行ごとにユニークなトークンを含むカスタムプレースホルダーを使用できますか？**  
A: もちろん可能です。プレースホルダー文字列を動的に構築（例: `"[redacted:" + UUID.randomUUID() + "]"`）し、`ReplacementOptions` に渡してください。

## 追加リソース
- [ドキュメント](https://docs.groupdocs.com/redaction/java/)
- [API リファレンス](https://reference.groupdocs.com/redaction/java)
- [GroupDocs.Redaction のダウンロード](https://releases.groupdocs.com/redaction/java/)
- [GitHub リポジトリ](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
- [無料サポートフォーラム](https://forum.groupdocs.com/c/redaction/33)
- [一時ライセンス情報](https://purchase.groupdocs.com/temporary-license/)

---

**最終更新日:** 2026-08-09  
**テスト環境:** GroupDocs.Redaction 24.9 for Java  
**作者:** GroupDocs

## 関連チュートリアル
- [スプレッドシートでデータをフィルタリングする方法 – GroupDocs.Redaction Java](/redaction/java/spreadsheet-redaction/)
- [機密データをマスクする Java – GroupDocs.Redaction で個人情報をリダクト](/redaction/java/advanced-redaction/master-document-redaction-java-groupdocs-redaction/)
- [機密データをマスクする Java – GroupDocs.Redaction ガイド](/redaction/java/getting-started/)