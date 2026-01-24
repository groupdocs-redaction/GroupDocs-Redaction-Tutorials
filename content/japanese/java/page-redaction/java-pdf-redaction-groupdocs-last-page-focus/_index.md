---
date: '2026-01-24'
description: GroupDocs.Redaction for Java を使用して PDF を編集（赤線処理）する方法を学び、プライバシーとコンプライアンスを確保するために最終ページの特定領域を対象にします。
keywords:
- Java PDF Redaction
- GroupDocs.Redaction
- PDF Area Redaction
title: Java と GroupDocs.Redaction を使用した PDF のマスク方法：最終ページと特定領域を対象に
type: docs
url: /ja/java/page-redaction/java-pdf-redaction-groupdocs-last-page-focus/
weight: 1
---

# Java と GroupDocs.Redaction を使用した PDF の赤字処理: 最終ページと特定領域を対象にする

このチュートリアルでは、Java 用 GroupDocs.Redaction ライブラリを使って **PDF を赤字処理する** 方法を紹介します。最終ページと正確な矩形領域に焦点を当てます。機密データを法的契約書で保護したり、配布前にレポートをサニタイズしたりする場合でも、以下の手順でコンプライアンスに準拠した赤字処理を簡単に実現できます。

## Quick Answers
- **使用するライブラリは？** GroupDocs.Redaction for Java。  
- **最終ページだけを対象にできるか？** はい、`PageRangeFilter` と `PageSeekOrigin.End` を使用します。  
- **特定の領域はどう定義するか？** 座標とサイズを受け取る `PageAreaFilter` を使用します。  
- **ライセンスは必要か？** テスト用にはトライアルまたは一時ライセンスが必要です。  
- **Java 17 に対応しているか？** 完全対応 – ライブラリは最新の JDK バージョンをサポートしています。

## PDF の赤字処理なツールです。

## 前提条件

作業を始める前に降）インストール済み  
   - IntelliJ IDEA や Eclipse などの IDE  

2. **環境設定**  
   - Maven が依存関係管理に設定済み  

3. **基本知識**  
   - Java の構文とファイル操作に慣れていること  

## GroupDocs.Redaction for Java のセットアップ

Maven で追加するか、JAR を直接ダウンロードしてプロジェクトに組み込めます。

### Maven 設定
`pom.xml` に以下を追加して GroupDocs.Redaction を依存関係として含めます。

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
あるいは、[GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/) から最新バージョンを取得してください。

#### ライセンス取得手順
- **無料トライアル:** ライセンスキーなしで API をテストできます。  
- **一時ライセンス:** 開発中にフル機能を利用できる期間限定キーです。  
- **購入:** 本番環境向けに永続ライセンスを取得します。

### 基本的な初期化
処理対象の PDF を指す `Redactor` インスタンスを作成します。

```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_PDF");
```

## PDF の赤字処理 – 最終ページで領域ベースの赤字処理を実装する方法

以下は、最終ページの特定矩形領域だけを **PDF を赤字処理する** 方法をステップバイステップで示したサンプルです。

### 機能 1: PDF ページ上の特定領域を赤字処理する

**概要:** 最終ページの選択した領域内のテキストだけをマスクし、文書の他の部分はそのまま残します。

#### 手順 1: PDF ドキュメントをロードする
```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_PDF");
```

#### 手順 2: ドキュメントのページ情報を取得する
```java
IDocumentInfo info = redactor.getDocumentInfo();
PageInfo lastPage = info.getPages().get(info.getPageCount() - 1);
```

#### 手順 3: 赤字処理の置換オプションを定義する
```java
ReplacementOptions options = new ReplacementOptions("[secret]");
```

#### 手順 4: 赤字処理対象領域を指定するフィルタを設定する
```java
options.setFilters(new RedactionFilter[] {
    new PageRangeFilter(PageSeekOrigin.End, 0, 1),
    new PageAreaFilter(
        new java.awt.Point(0, lastPage.getHeight() / 2),
        new java.awt.Dimension(lastPage.getWidth(), lastPage.getHeight() / 2)
    )
});
```

#### 手順 5: 赤字処理を適用する
```java
RedactorChangeLog result = redactor.apply(new ExactPhraseRedaction("bibliography", false, options));
```

#### 手順 6: 赤字処理が成功したか確認し、変更を保存する
```java
if (result.getStatus() != RedactionStatus.Failed) {
    redactor.save("YOUR_OUTPUT_DIRECTORY/redacted_output.pdf");
}
```

#### 手順 7: リソース解放のため Redactor を閉じる
```java
redactor.close();
```

### 機能 2: ページ範囲フィルタによる赤字処理

**概要:** 複数ページの契約書などで、特定ページ（例: 最終ページ）のみを対象に赤字処理したい場合に使用します。

#### 手順 1: PDF ドキュメントをロードする
```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_PDF");
```

#### 手順 2: ドキュメントのページ情報を取得する
```java
IDocumentInfo info = redactor.getDocumentInfo();
```

#### 手順 3: 特定ページを対象とするページ範囲フィルタを定義する
```java
PageRangeFilter pageRangeFilter = new PageRangeFilter(PageSeekOrigin.End, 0, 1);
```

### 機能 3: PDF ページ上の領域ベース赤字処理

**概要:** 正確な矩形を指定して、ピクセル単位で隠したい部分をコントロールできます。

#### 手順 1: PDF ドキュメントをロードする
```java
final Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_PDF");
```

#### 手順 2: ドキュメントのページ情報を取得する
```java
IDocumentInfo info = redactor.getDocumentInfo();
PageInfo lastPage = info.getPages().get(info.getPageCount() - 1);
```

#### 手順 3: ページのどの部分を赤字処理するか指定する領域フィルタを定義する
```java
PageAreaFilter areaFilter = new PageAreaFilter(
    new java.awt.Point(0, lastPage.getHeight() / 2),
    new java.awt.Dimension(lastPage.getWidth(), lastPage.getHeight() / 2)
);
```

#### 手順 4: リソース解放のため Redactor を閉じる
```java
redactor.close();
```

## 実務での活用例

- **法務文書のサニタイズ:** クライアント名や事件番号をドラフト共有前に除去。  
- **財務報告書:** 四半期報告書の口座番号や個人識別子をマスク。  
- **医療記録:** 研究用に PDF をエクスポートする際に PHI を隠す。  
- **リリース前レビュー:** 開発中のセクションを非表示にし、レビュー担当者に残りの文書を見せる。  

## パフォーマンス向上のヒント

- **Redactor インスタンスを再利用:** バッチ処理で多数の PDF を扱う場合、`Redactor` オブジェクトを1つだけ保持し、ファイル間でリセットして使用します。  
- **速やかな破棄:** `close()` を必ず呼び出してネイティブリソースを解放します。  
- **サンプルで検証:** フィルタのジオメトリが正しいか小さなテストファイルで確認してから本番に拡張します。  

## よくある問題と解決策

| Issue | Cause | Fix |
|-------|-------|-----|
| No output file created | `result.getStatus()` returned `Failed` | コンソールの例外詳細を確認し、置換テキストが有効かつフィルタが正しく定義されていることを確認してください。 |
| Redaction covers the whole page | Incorrect `PageAreaFilter` dimensions | `lastPage.getHeight()` と `lastPage.getWidth()` の値を確認し、`Point` と `Dimension` を適切に調整してください。 |
| License error | Missing or expired license key | 本番環境に移行する前に、トライアルまたは一時ライセンスを適用してください。 |

## FAQ

**Q: テキストだけでなく画像やグラフィックも赤字処理できますか？**  
A: はい。`ExactImageRedaction` を使用するか、テキストと画像のフィルタを組み合わせてビジュアル要素をマスクできます。

**Q: 赤字処理は編集機能を持つ PDF ビューアでも残りますか？**  
A: 完全に残ります。 パスワード保護された PDF を赤字処理するには？**  
A: パスワードを含む `LoadOptions` オポートされている Java バージョンは？**  
A:8 から Java 21 まで、LTS リリースを含むすべてのバージョンをサポートしています。

## 結論

これで **Java と GroupDocs.Redaction を使用した囲フィルタと領域フィルタを活用すれば、機密データを外部に漏らすことなく、文書全体の整合性を保ったまま正確に削除できます。さまざまなフィルタを試し、既存のドキュメントパイプラインに組み込んで、データプライバシー規制に確実に準拠しましょう。

---

**最終更新日:** 2026-01-24  
**テスト環境:** GroupDocs.Redaction 24.9  
**作者:** GroupDocs