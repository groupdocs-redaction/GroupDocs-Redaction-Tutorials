---
date: '2026-02-26'
description: GroupDocs.Redaction Java を使用してテキストをマスクし、正確なフレーズ置換とカスタム PDF 設定でラスタライズされた
  PDF として保存する方法を学びましょう。
keywords:
- GroupDocs.Redaction Java
- text redaction Java
- rasterized PDF conversion
title: GroupDocs.Redaction Javaでテキストを編集（マスク）する方法
type: docs
url: /ja/java/text-redaction/groupdocs-redaction-java-tutorial-text-redaction-rasterized-pdf/
weight: 1
---

# GroupDocs.Redaction Javaでテキストを赤字消去する方法

今日のデータ駆動型の世界では、ドキュメント内の**テキストを赤字消去する方法**は、開発者やコンプライアンス担当者にとって重要な関心事です。個人識別子や機密クライアント情報、内部プロジェクトコードを隠す必要がある場合でも、GroupDocs.Redaction for Java は正確なフレーズを検索し、セキュアなオーバーレイで置き換える信頼できる手段を提供します。このチュートリアルでは**ラスタライズされた PDF として保存する方法**も示し、各ページを画像ベースの PDF に変換してアーカイブ基準を満たします。

## クイック回答
- **赤字消去の主要クラスは何ですか？** `Redactor`  
- **フレーズをカラーオーバーレイで置き換えることはできますか？** Yes, using `ExactPhraseRedaction` and `ReplacementOptions`.  
- **ラスタライズされた PDF を生成するにはどうすればよいですか？** Enable rasterization via `SaveOptions.getRasterization().setEnabled(true)`.  
- **例で使用されている PDF コンプライアンスレベルはどれですか？** `PdfComplianceLevel.PdfA1a`.  
- **本番環境で使用するにはライセンスが必要ですか？** A valid GroupDocs.Redaction license is required for production deployments.

## Javaでの「テキストを赤字消去する方法」とは？
赤字消去は、ファイルから機密情報を永久に削除または隠蔽するプロセスです。GroupDocs.Redaction を使用すると、名前や ID などの正確なフレーズをプログラムで検索し、赤いオーバーレイ、黒いボックス、または任意のカスタムビジュアル要素で置き換えることができ、元のデータが復元できないようにします。

## Javaで GroupDocs.Redaction を使用する理由
- **Exact phrase matching** は偽陽性を排除します。  
- **Built‑in rasterization** を使用すると、長期保存向けの PDF/A 準拠の画像のみの PDF を作成できます。  
- **Cross‑format support** は DOCX、PDF、PPTX などで動作し、同じコードをさまざまな文書タイプに適用できます。  
- **Performance‑focused API** は大量の文書セットをバッチ処理しながら、メモリ使用量を低く抑えることができます。

## 前提条件
始める前に、以下が揃っていることを確認してください。

- **GroupDocs.Redaction for Java** (v24.9 以上)。  
- **Java Development Kit (JDK) 8+**。  
- IntelliJ IDEA、Eclipse、NetBeans などの IDE。  
- 依存関係管理のための Maven。

### 必要なライブラリと依存関係
- **GroupDocs.Redaction for Java** – `pom.xml` にリポジトリと依存関係を追加します（下記コードブロック参照）。  
- **Optional**: 任意の追加ロギングライブラリ。

### 知識の前提条件
- 基本的な Java 文法とファイル I/O。  
- Maven の `pom.xml` 構造に関する知識。

## GroupDocs.Redaction for Java のセットアップ
### Maven 設定
Add the repository and dependency to your `pom.xml` file:

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
または、最新バージョンを直接 [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) からダウンロードできます。

### ライセンス取得
- **Free Trial** – ライセンスキーなしで API を試用できます。  
- **Temporary License** – 長期評価のために使用できます。  
- **Full License** – 本番環境では必須です。

### 基本的な初期化と設定
Below is the minimal code to create a `Redactor` instance pointing at a sample DOCX file:

```java
import com.groupdocs.redaction.Redactor;

final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
```

## テキストを赤字消去する方法 – 正確なフレーズの例
### 手順 1: 必要なクラスのインポート
These imports give you access to the redaction engine and replacement options:

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.ReplacementOptions;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
```

### 手順 2: 赤字消去の作成と適用
The following snippet searches for the phrase **“John Doe”** and replaces it with a red overlay:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
try {
    RedactorChangeLog result = redactor.apply(new ExactPhraseRedaction(
        "John Doe", new ReplacementOptions(java.awt.Color.RED)));
    
    if (result.getStatus() != RedactionStatus.Failed) {
        // Successfully redacted the text
    }
} finally { 
    redactor.close(); 
}
```

**重要な理由:** `ReplacementOptions` は赤字消去のビジュアルスタイルを制御でき、隠されたコンテンツがコピー＆ペーストや OCR で復元できないようにします。

## ラスタライズされた PDF として保存する方法
### 手順 1: SaveOptions クラスのインポート
These classes let you configure PDF output, including rasterization and compliance levels:

```java
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.options.PdfComplianceLevel;
```

### 手順 2: 保存オプションの設定と適用
After redacting, you can export the document as a rasterized PDF. The example below rasterizes page 5 only and forces PDF/A‑1a compliance:

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
try {
    SaveOptions options = new SaveOptions();

    // Enable rasterization for converting pages into images.
    options.getRasterization().setEnabled(true);
    
    // Set the starting page and count for rasterization.
    options.getRasterization().setPageIndex(5);
    options.getRasterization().setPageCount(1);

    // Define PDF compliance level.
    options.getRasterization().setCompliance(PdfComplianceLevel.PdfA1a);

    // Append a suffix to avoid filename conflicts.
    options.setAddSuffix(true);

    // Save the document with these configurations.
    redactor.save(options);
} finally { 
    redactor.close(); 
}
```

**重要ポイント:** PDF をラスタライズすると**各ページが画像に変換され**、隠れたテキスト層が除去され、文書が改ざん防止になるため、法的アーカイブに最適です。

## 実用的な応用例
1. **Sensitive Data Redaction** – 契約書を共有する前に個人識別子を自動的に隠蔽します。  
2. **Document Archiving** – 完成したレポートを長期コンプライアンス向けにラスタライズされた PDF/A に変換します。  
3. **Bulk Content Update** – 数百のファイルにわたる古い用語を単一スクリプトで置き換えます。

## パフォーマンス上の考慮点
- **Close the `Redactor`** – 各操作後に `Redactor` を閉じてファイルハンドルとメモリを解放します。  
- **Batch Processing** – ファイルリストを読み込みループ処理し、可能な限り単一の `Redactor` インスタンスを再利用します。  
- **Monitor Resources** – 大規模な赤字消去中に CPU とヒープ使用量を監視するため、Java のプロファイリングツールを使用します。

## よくある質問
**Q: Maven プロジェクトに GroupDocs.Redaction をインストールするにはどうすればよいですか？**  
A: Maven Setup セクションに示したように、GroupDocs リポジトリと `groupdocs-redaction` 依存関係を `pom.xml` に追加します。

**Q: このライブラリで PDF ファイルのテキストを赤字消去できますか？**  
A: はい、GroupDocs.Redaction は PDF、DOCX、PPTX など多数のフォーマットをサポートしています。

**Q: 正確なフレーズが見つからなかった場合はどうなりますか？**  
A: `RedactorChangeLog` は `Failed` ステータスを返します。フレーズのスペルと大文字小文字を確認してください。

**Q: 非常に大きな文書を効率的に処理するにはどうすればよいですか？**  
A: 小さなページ範囲に分割して処理し、必要な箇所だけラスタライズを有効にし、常に `Redactor` を閉じてリソースを解放します。

**Q: 特定のページ範囲でラスタライズされた PDF を保存することは可能ですか？**  
A: もちろん可能です。`options.getRasterization().setPageIndex()` と `setPageCount()` を使用して、ラスタライズしたい正確なページを指定してください。

## 結論
これで、GroupDocs.Redaction Java を使用した **テキストを赤字消去する方法** と **ラスタライズされた PDF として保存する方法** の完全なエンドツーエンドガイドが手に入りました。これらの手順に従うことで、機密情報を保護し、コンプライアンス要件を満たし、プロダクション環境で高いパフォーマンスを維持できます。

**次のステップ**  
- [公式ドキュメント](https://docs.groupdocs.com/redaction/java/) を参照して API をさらに深く学びます。  
- 他の赤字消去タイプ（例: `RegexRedaction`、`ImageRedaction`）を試してみます。  
- [GroupDocs Support Forum](https://forum.groupdocs.com/c/redaction/33) でコミュニティに参加し、ヒントやベストプラクティスを共有します。

---

**最終更新日:** 2026-02-26  
**テスト環境:** GroupDocs.Redaction Java 24.9  
**作者:** GroupDocs