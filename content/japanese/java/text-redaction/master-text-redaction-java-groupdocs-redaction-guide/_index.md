---
date: '2026-03-01'
description: GroupDocs.Redaction を使用して Java で正規表現によるテキストの赤字処理方法を学びましょう。このステップバイステップのチュートリアルでは、正規表現の適用方法、保存オプションの設定、機密データの保護方法を示します。
keywords:
- text redaction in Java
- regex text redaction
- GroupDocs.Redaction
title: Java で GroupDocs.Redaction を使用してテキストを編集（マスク）する方法：完全ガイド
type: docs
url: /ja/java/text-redaction/master-text-redaction-java-groupdocs-redaction-guide/
weight: 1
---

# JavaでGroupDocs.Redactionを使用してテキストを赤字化する方法：完全ガイド

今日の急速に変化するデジタル世界では、ドキュメント内の**テキストを赤字化する方法**は多くの開発者が直面する課題です。個人データの保護、規制への準拠、あるいは単にドラフトを整理する場合でも、本ガイドでは GroupDocs.Redaction for Java を使用して**正規表現を適用する方法**による赤字化を迅速かつ安全に行う手順を紹介します。

ライブラリのセットアップ、正規表現パターンの作成、保存オプションの設定、そして赤字化が重要になる実際のユースケースまで、すべてを網羅します。

## クイック回答
- **GroupDocs.Redaction の主な目的は何ですか？** 多数のドキュメント形式で機密テキストを検出しマスクする信頼性の高い API を提供します。  
- **赤字化に正規表現を適用するにはどうすればよいですか？** パターンを指定して `RegexRedaction` オブジェクトを作成し、`Redactor.apply()` メソッドに渡します。  
- **ライセンスは必要ですか？** 開発には無料トライアルで十分です。製品環境では有料ライセンスがすべての機能を解放します。  
- **PDF と DOCX の両方を赤字化できますか？** はい。GroupDocs.Redaction は PDF、DOCX、PPTX などをサポートしています。  
- **パフォーマンスを向上させる最善の方法は何ですか？** `Redactor` インスタンスは速やかに閉じ、正規表現パターンはできるだけシンプルに保ちます。

## テキスト赤字化とは何か、そしてなぜ重要なのか
テキスト赤字化は、ドキュメントから機密情報を永久に削除または隠すプロセスです。これにより、社会保障番号、医療記録、財務情報などの機密データが不正アクセスや閲覧から保護されます。

## テキスト赤字化に正規表現を使用する理由
正規表現を使用すると、電話番号やクレジットカード番号など、さまざまなデータ形式にマッチする柔軟なパターンを定義できます。GroupDocs.Redaction と組み合わせることで、隠す対象を正確にコントロールしながら、実装を簡潔に保てます。

## 前提条件
- **Java Development Kit (JDK)** がインストールされていること（Java 8 以上）。  
- Java の構文と正規表現に関する基本的な知識。  
- **IntelliJ IDEA** や **Eclipse** などの IDE があり、コードの実行とデバッグができること。  

## Java 用 GroupDocs.Redaction のセットアップ
まず、ライブラリをプロジェクトに追加します。

### Maven 設定
Maven を使用している場合は、`pom.xml` に以下を挿入してください。

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
あるいは、最新の JAR を [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) からダウンロードします。

### 基本的な初期化
ライブラリが利用可能になったら、ドキュメントの赤字化を開始できます。

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

## Java で正規表現を使用してテキストを赤字化する方法
以下は、**テキストを赤字化する方法**を正規表現パターンで実現するステップバイステップの解説です。

### 機能 1: 正規表現テキスト赤字化
**概要**: この機能はコアな `RegexRedaction` ワークフローを示します。

#### ステップ 3.1: 必要なクラスのインポート
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.redactions.RegexRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;
```

#### ステップ 3.2: Redactor の初期化と正規表現パターンの適用
```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
try {
    // Define a regex pattern to find sequences of numbers and apply a replacement color.
    // The pattern: Two digits, optional whitespace, two more digits, non-digit characters,
    // followed by six digits.
    redactor.apply(new RegexRedaction("\\d{2}\\s*\\d{2}[^\\d]*\\d{6}", 
        new ReplacementOptions(java.awt.Color.BLUE)));
```

- **正規表現の説明**: このパターンは特定の形式（例：日付や ID 番号）に続く数値シーケンスにマッチします。`ReplacementOptions` は青いオーバーレイで赤字化領域を示します。

#### ステップ 3.3: 保存オプションの設定
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

- **保存オプション**: サフィックスを追加すると、どのファイルが処理されたかが明確になり、元の形式を保持することで不要な変換を防げます。

#### トラブルシューティングのヒント
- 正規表現が隠したいデータを正確にキャプチャしているか確認してください。  
- ファイルパスを再確認し、アプリケーションに読み書き権限があることを確認してください。  

### 機能 2: 保存オプションの構成
**概要**: 赤字化後の出力ファイルを細かく調整します。

#### ステップ 3.4: 保存設定のカスタマイズ
```java
import com.groupdocs.redaction.options.SaveOptions;

SaveOptions saveOptions = new SaveOptions();
saveOptions.setAddSuffix(true);  // Indicates processing by adding a suffix
saveOptions.setRasterizeToPDF(false);  // Keeps original format intact
```

- **重要な設定**: このスニペットは出力ファイル名の管理と元のドキュメント構造の保持に役立ちます。

## 実用的な応用例
**テキストを赤字化する方法**が不可欠な実世界のシナリオ：

1. **法務文書** – 外部顧問とドラフトを共有する前にクライアント識別子を隠す。  
2. **医療記録** – 患者名、ID、健康番号をマスクし、HIPAA 準拠を維持する。  
3. **財務報告書** – 四半期サマリー配布時に機密口座番号を削除する。  

## パフォーマンスに関する考慮事項
- **メモリ管理**: 常に `Redactor` インスタンス（`redactor.close()`）を閉じてリソースを解放します。  
- **効率的な正規表現**: シンプルなパターンは高速に実行されます。可能な限り過度に複雑な表現は避けてください。  
- **バッチ処理**: 大量のドキュメントセットの場合、ファイルをバッチで処理してメモリ使用量を予測可能に保ちます。

## よくある問題と解決策
| 問題 | 解決策 |
|-------|----------|
| **正規表現が過剰にマッチする** | オンライン正規表現テスターでパターンをテストし、文字クラスを絞り込んでください。 |
| **出力ファイル名の競合** | `setAddSuffix(true)` を使用するか、`saveOptions.setOutputPath()` でカスタム出力パスを指定してください。 |
| **大きな PDF でのメモリリーク** | PDF をページ単位で処理するか、JVM ヒープサイズを増やします（`-Xmx2g`）。 |

## よくある質問

**Q: SaveOptions の `setAddSuffix(true)` の目的は何ですか？**  
A: 出力ファイル名に自動的にサフィックス（例：`_redacted`）を付加し、どのファイルが処理されたかが一目で分かるようにします。

**Q: 数字以外の正規表現パターンでテキスト赤字化はできますか？**  
A: もちろん可能です。メールアドレス、電話番号、カスタム ID など、任意の有効な Java 正規表現を `RegexRedaction` に渡すことで対象を指定できます。

**Q: 赤字化中にエラーが発生した場合の対処方法は？**  
A: 赤字化ロジックを try‑catch ブロックで囲み、例外をログに記録し、finally 節で必ず `Redactor` を閉じてリソースを解放してください。

**Q: PDF の赤字化はサポートされていますか？**  
A: はい。GroupDocs.Redaction は PDF、DOCX、PPTX など多数のフォーマットに対応しています。

**Q: 大規模な赤字化プロジェクトのベストプラクティスは？**  
A: バッチ処理を活用し、正規表現パターンはシンプルに保ち、プロファイリングツールでメモリ使用量を監視してください。

## リソース
- **ドキュメント**: [GroupDocs Redaction Documentation](https://docs.groupdocs.com/redaction/java/)  
- **API リファレンス**: [GroupDocs API Reference](https://apireference.groupdocs.com/redaction/java)

---

**最終更新日:** 2026-03-01  
**テスト環境:** GroupDocs.Redaction 24.9 for Java  
**作者:** GroupDocs