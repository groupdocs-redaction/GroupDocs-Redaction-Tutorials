---
date: '2026-10-01'
description: JavaでGroupDocs Redactionを使用して、著者メタデータを削除し、編集済み文書ファイルを保存する方法を学びます。
keywords:
- remove author metadata
- save redacted document
- groupdocs metadata removal
lastmod: '2026-10-01'
og_description: JavaでGroupDocs Redactionを使用して、著者メタデータを削除し、編集済み文書ファイルを保存する方法を学びます。ステップバイステップのガイドに従ってください。
og_image_alt: Guide showing Java code to remove author metadata using GroupDocs Redaction
og_title: JavaでGroupDocsを使用して著者メタデータを削除する方法
schemas:
- author: GroupDocs
  dateModified: '2026-10-01'
  description: Learn how to remove author metadata and save redacted document files
    in Java using GroupDocs Redaction.
  headline: How to remove author metadata in Java with GroupDocs
  type: TechArticle
- description: Learn how to remove author metadata and save redacted document files
    in Java using GroupDocs Redaction.
  name: How to remove author metadata in Java with GroupDocs
  steps:
  - name: '**Legal documents** – Redact author information before sending contracts
      to opposing counsel.'
    text: '**Legal documents** – Redact author information before sending contracts
      to opposing counsel.'
  - name: '**Corporate reports** – Remove manager names when publishing quarterly
      results to shareholders.'
    text: '**Corporate reports** – Remove manager names when publishing quarterly
      results to shareholders.'
  - name: '**Project files** – Clean up internal project documentation before archiving
      or uploading to a public repository.'
    text: '**Project files** – Clean up internal project documentation before archiving
      or uploading to a public repository.'
  type: HowTo
- questions:
  - answer: It removes selected metadata fields from a document.
    question: What does EraseMetadataRedaction do?
  - answer: GroupDocs.Redaction for Java.
    question: Which library provides this feature?
  - answer: A free trial works for testing; a permanent license is required for production.
    question: Do I need a license?
  - answer: Yes, combine filters with a logical OR.
    question: Can I target multiple fields at once?
  - answer: Redactor instances are not shared across threads; create a new instance
      per operation.
    question: Is the process thread‑safe?
  type: FAQPage
tags:
- metadata redaction
- GroupDocs
- Java document processing
title: JavaでGroupDocsを使用して著者メタデータを削除する方法
type: docs
url: /ja/java/metadata-redaction/groupdocs-redaction-java-metadata-implementation/
weight: 1
---

# JavaでGroupDocsを使用して著者メタデータを削除する方法

今日のデジタル環境では、文書内に隠された機密情報を保護することは必須の実践です。**著者メタデータの削除**は、個人や企業の識別子が偶然に漏洩するのを防ぎます。このチュートリアルでは、GroupDocs.Redaction for Java の `EraseMetadataRedaction` を使用して、Word ファイルから *Author* や *Manager* などのフィールドを削除し、**編集済み文書**のコピーを安全に保存して共有やアーカイブに利用する方法をステップバイステップで示します。

## クイック回答
- **EraseMetadataRedaction は何をしますか？** 文書から選択されたメタデータフィールドを削除します。  
- **この機能を提供するライブラリはどれですか？** GroupDocs.Redaction for Java。  
- **ライセンスは必要ですか？** 無料トライアルはテストに使用できますが、実稼働には永続ライセンスが必要です。  
- **�数のフィールドを同時に対象にできますか？** はい、論理 OR でフィルタを組み合わせます。  
- **このプロセスはスレッドセーフですか？** Redactor インスタンスはスレッド間で共有されません。操作ごとに新しいインスタンスを作成してください。

## EraseMetadataRedaction とは何ですか？
`EraseMetadataRedaction` は、削除すべきメタデータエントリを指定できる組み込みのレダクションクラスです。GroupDocs.Redaction がサポートする幅広い文書形式で動作し、隠された作成情報が漏洩しないようにします。Author、Manager といった標準プロパティだけでなく、カスタムメタデータフィールドも対象にでき、包括的なプライバシー保護を提供します。

## GroupDocs で EraseMetadataRedaction を使用する理由
GroupDocs.Redaction は **100 以上の入力・出力フォーマット** をサポートし、ファイル全体をメモリに読み込まずに最大 500 ページの文書を処理できます。このクラスを使用すると、GDPR、HIPAA、または社内コンプライアンス要件を満たす単一の高性能 API が得られ、コードベースをシンプルに保てます。

## 前提条件
- Java 8 以上がインストールされていること。  
- Maven（または手動で JAR を追加できる環境）。  
- GroupDocs.Redaction for Java（バージョン 24.9 以降）。  
- 有効な GroupDocs のトライアルまたは永続ライセンス。

## GroupDocs.Redaction for Java のセットアップ

### Maven インストール
**pom.xml** に GroupDocs リポジトリと依存関係を追加します：

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

### ライセンス取得
GroupDocs ポータルから無料トライアルまたは一時ライセンスを取得してください。ライセンスファイルはアプリケーションが読み込める場所（例：クラスパスのルート）に配置する必要があります。

### 基本的な初期化と設定
以下は DOCX ファイル用に `Redactor` インスタンスを作成する最小限の例です：

```java
import com.groupdocs.redaction.Redactor;

String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
Redactor redactor = new Redactor(filePath);
```

## Java で EraseMetadataRedaction を使用する方法
以下のセクションでは、実装を明確で実行可能な手順に分解しています。

### 機能: 特定のメタデータ項目をクリーンアップ

#### 概要
`EraseMetadataRedaction` を使用して **Author** と **Manager** のメタデータフィールドを削除します。これは、内部レポートを外部パートナーと共有する際の一般的な要件です。

#### 手順実装

##### 1️⃣ Redactor オブジェクトの初期化
`Redactor` は文書をロードし、レダクションオブジェクトを適用し、結果を書き出すコアクラスです。処理する各ファイルごとに新しいインスタンスを作成してください：

```java
import com.groupdocs.redaction.Redactor;

String inputFilePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
final Redactor redactor = new Redactor(inputFilePath);
```

##### 2️⃣ EraseMetadataRedaction の適用
`MetadataFilters` は Author や Manager などの一般的なメタデータキー用の事前定義フィルタを提供します。  
`EraseMetadataRedaction` は提供された `MetadataFilters` に一致するメタデータエントリを削除します。ビット単位の OR (`|`) を使用して `Author` と `Manager` フィルタを組み合わせることで、1 回の呼び出しで両方のフィールドが削除されます：

```java
import com.groupdocs.redaction.redactions.EraseMetadataRedaction;
import com.groupdocs.redaction.MetadataFilters;

try {
    redactor.apply(new EraseMetadataRedaction(MetadataFilters.Author | MetadataFilters.Manager));
} finally {
    redactor.close();
}
```

##### 3️⃣ 保存オプションの設定
`SaveOptions` では出力ファイル名、フォーマット、その他の保存パラメータを指定できます。  
`SaveOptions` で出力ファイル名、フォーマット、文書を PDF にラスタライズするかどうかを制御できます。サフィックスを追加することで元のファイルをそのままに保ちます：

```java
import com.groupdocs.redaction.options.SaveOptions;

SaveOptions saveOptions = new SaveOptions();
saveOptions.setAddSuffix(true); // Adds "_Redacted" to the file name
saveOptions.setRasterizeToPDF(false);

redactor.save(saveOptions);
```

## 一般的なユースケース
1. **法務文書** – 契約書を相手方の弁護士に送る前に著者情報をレダクトします。  
2. **企業レポート** – 四半期業績を株主に公開する際にマネージャー名を削除します。  
3. **プロジェクトファイル** – アーカイブやパブリックリポジトリへのアップロード前に内部プロジェクト文書をクリーンアップします。

## トラブルシューティングのヒント
- **ファイルが見つかりません** – `inputFilePath` のパスが実在するファイルを指しているか、アプリケーションに読み取り権限があるか確認してください。  
- **メタデータフィールドが欠如** – すべての文書タイプが同じメタデータキーを保持しているわけではありません。まず Office で文書のプロパティを確認してください。  
- **ライセンスエラー** – `Redactor` インスタンスを作成する前にライセンスファイルが正しくロードされていることを確認してください。

## パフォーマンス上の考慮点
- `Redactor` オブジェクトは速やかに閉じ（`finally` ブロック参照）、ネイティブリソースを解放してください。  
- PDF プレビューが必要でない限り、大きな文書のラスタライズは避けてください。ラスタライズは 300 ページのファイルで CPU とメモリ使用量が最大 3 倍に増加する可能性があります。

## よくある質問

**Q1: メタデータレダクションとは何ですか？**  
A1: メタデータレダクションは、隠された文書プロパティ（著者、マネージャー、カスタムタグなど）を削除し、機密情報が偶然に漏洩するのを防ぐことです。

**Q2: GroupDocs.Redaction を他のファイルタイプでも使用できますか？**  
A2: はい、ライブラリは PDF、DOCX、PPTX、XLSX など多数のフォーマットをサポートしており、合計で 100 以上の形式に対応しています。

**Q3: レダクション中のエラーはどう処理すべきですか？**  
A3: `apply` 呼び出しを try‑catch ブロックで囲み、必ず `finally` 節で `Redactor` を閉じてリソースを解放してください。

**Q4: カスタムメタデータフィールドをレダクトできますか？**  
A5: もちろんです。`MetadataFilters.Custom("YourFieldName")` を使用して、文書に保存された任意のカスタムプロパティを対象にできます。

**Q5: GroupDocs.Redaction を使用する際のベストプラクティスは何ですか？**  
A5:  
- アプリケーション起動時にライセンスを早めにロードする。  
- `Redactor` オブジェクトは速やかに閉じる。  
- `SaveOptions` でサフィックスを付け、元のファイルをそのままに保つ。  
- バッチ処理を行う前に、文書のコピーでレダクションをテストする。

**Q6: EraseMetadataRedaction はバッチ操作をサポートしていますか？**  
A6: ファイルパスのコレクションをループし、各ファイルごとに新しい `Redactor` を作成して同じレダクションロジックを適用できます。

**Q7: EraseMetadataRedaction を他のレダクションタイプと組み合わせられますか？**  
A7: はい、保存前に複数のレダクションオブジェクト（例: テキストレダクションの後にメタデータレダクション）をチェーンできます。

## リソース

- **ドキュメント**: [GroupDocs Redaction Java Docs](https://docs.groupdocs.com/redaction/java/)  
- **API リファレンス**: [GroupDocs API Reference](https://reference.groupdocs.com/redaction/java)  
- **ダウンロード**: [Latest Releases](https://releases.groupdocs.com/redaction/java/)  
- **GitHub**: [GroupDocs GitHub Repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- **無料サポート**: [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)  
- **一時ライセンス**: [Acquire a Temporary License](https://purchase.groupdocs.com/temporary-license)

---

**最終更新日:** 2026-10-01  
**テスト環境:** GroupDocs.Redaction 24.9 for Java  
**作者:** GroupDocs

## 関連チュートリアル

- [Groupdocs Redaction Java ドキュメントメタデータ抽出](/redaction/java/metadata-redaction/groupdocs-redaction-java-document-metadata-extraction/)  
- [GroupDocs.Redaction を使用した Java のメタデータ削除方法](/redaction/java/metadata-redaction/metadata-redaction-groupdocs-java-guide/)  
- [Groupdocs Redaction Java を使用した文書情報取得](/redaction/java/document-information/retrieve-document-info-using-groupdocs-redaction-java/)