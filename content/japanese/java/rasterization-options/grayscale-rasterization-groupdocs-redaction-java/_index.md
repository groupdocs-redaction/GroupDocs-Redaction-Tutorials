---
date: '2026-05-17'
description: GroupDocs.Redaction for Java を使用して PDF をグレースケールにラスタライズする方法を学び、グレースケールフィルタを適用し、ドキュメントを安全かつ高品質に保ちます。
keywords:
- how to rasterize pdf
- java pdf to image
- apply grayscale filter pdf
schemas:
- author: GroupDocs
  dateModified: '2026-05-17'
  description: Learn how to rasterize PDF to grayscale using GroupDocs.Redaction for
    Java, apply a grayscale filter, and keep your documents secure and high‑quality.
  headline: How to rasterize PDF to grayscale with GroupDocs.Redaction Java – Secure
    and Optimize Your Documents
  type: TechArticle
- questions:
  - answer: In GroupDocs.Redaction, the grayscale option is tied to rasterization,
      which ensures consistent results and adds a security layer.
    question: Can I convert documents to grayscale without rasterization?
  - answer: All major formats supported by GroupDocs.Redaction—including DOCX, PDF,
      XLSX, PPTX, RTF, and more than 100 others—can be rasterized and converted to
      grayscale.
    question: What document formats support grayscale rasterization?
  - answer: Yes. Text‑heavy files may grow, while image‑heavy files might shrink.
      DPI settings have the biggest impact.
    question: Will rasterization affect the file size of my documents?
  - answer: No. Rasterization is one‑way; keep a backup of the original if you need
      to revert.
    question: Is it possible to reverse the grayscale rasterization process?
  - answer: Use a higher DPI (300 + for print quality) and choose PDF as the output
      format for best archival results.
    question: How can I optimize the quality of grayscale rasterized documents?
  type: FAQPage
title: GroupDocs.Redaction Java を使用して PDF をグレースケールにラスタライズする方法 – ドキュメントを安全に最適化
type: docs
url: /ja/java/rasterization-options/grayscale-rasterization-groupdocs-redaction-java/
weight: 1
---

# PDF をグレースケールにラスタライズする方法（GroupDocs.Redaction Java）

PDF をグレースケールに **ラスタライズ** したい場合、ドキュメントを安全に保ち、プロフェッショナルな外観で、アーカイブしやすくしたい場合は、ここが最適です。このチュートリアルでは、カラフルな DOCX、PDF、またはその他のサポートされているファイルを、GroupDocs.Redaction for Java を使用してクリーンなグレースケールのラスタライズ版に変換する正確な手順を解説します。ラスタライズがセキュリティ層を追加する理由、ライブラリの設定方法、リソースの効率的な管理方法を、フレンドリーなステップバイステップ形式で理解できます。

## クイック回答
- **グレースケール ラスタライズは何をするのですか？** 各ページを高解像度の画像に変換し、グレースケールフィルタを適用してすべての色情報を除去します。  
- **なぜ GroupDocs.Redaction を使用するのですか？** 1つの使いやすい API で、編集削除（レダクション）セキュリティとラスタライズオプションを統合します。  
- **サポートされているフォーマットは何ですか？** DOCX、PDF、XLSX、PPTX、RTF など、100 以上のフォーマットに対応しています。  
- **ライセンスは必要ですか？** 本番環境では有効な GroupDocs.Redaction ライセンスが必要です。テスト用に無料トライアルが利用可能です。  
- **必要な Java バージョンは？** JDK 8 以上です。

## PDF をグレースケールにラスタライズする方法

`new Redactor("path/to/file")` でソースドキュメントを読み込み、`RasterizationOptions` でラスタライズを有効にし、グレースケールの高度オプションを追加して `save()` を呼び出します—変換は数行のコードで完了します。このアプローチにより、すべてのページが画像ベースの白黒 PDF になり、テキスト選択ができなくなり、統一された印刷準備済みの外観が保証されます。

## **create grayscale pdf** とは何ですか？

グレースケール PDF を作成することは、元のドキュメントのすべての視覚要素を灰色の濃淡に変換することを意味します。その結果、サイズが小さく、印刷に適したファイルとなり、色に関する注意散漫を排除し、コンテンツが画像ベースになることで微妙なセキュリティ効果も得られます。

## GroupDocs.Redaction でグレースケール ラスタライズを使用する理由

ラスタライズは各ページを画像に変換するため、テキストのコピーや編集ができず、ビジュアル出力がプリンターやビューアー間で一貫します。GroupDocs.Redaction は **100 以上の入力および出力フォーマット**（DOCX、XLSX、PPTX、HTML、画像形式など）をサポートしているため、実質的にあらゆるドキュメントに同じワークフローを適用できます。

## 前提条件

- Java Development Kit (JDK) 8 以上。`java -version` で確認してください。  
- IDE（IntelliJ IDEA、Eclipse、NetBeans のいずれか）を使用すると、コーディングとデバッグが容易になります。  
- Maven または Gradle を使用して GroupDocs.Redaction for Java を追加します。  
- サンプルドキュメント（例：複数ページの DOCX）を用意し、安全に実験できるようにします。  
- ラスタライズ出力用に十分なディスク容量を確保してください（ラスタファイルは元ファイルより大きくなることがあります）。

## パッケージのインポート

以下のインポートは、サンプルに必要なコア Redactor とラスタライズクラスを取り込みます。

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.options.RasterizationOptions;
import com.groupdocs.redaction.options.AdvancedRasterizationOptions;
```

## 手順 1: Redactor オブジェクトの初期化

`Redactor` クラスは GroupDocs.Redaction のすべてのドキュメント処理操作のエントリーポイントです。インスタンスを作成すると、ドキュメントの読み込み、編集、保存が可能になります。

```java
final Redactor redactor = new Redactor(Constants.MULTIPAGE_SAMPLE_DOCX);
```

`Constants.MULTIPAGE_SAMPLE_DOCX` を、グレースケール PDF に変換したいファイルへのパスに置き換えてください。

## 手順 2: 保存オプションの設定

`SaveOptions` クラスは、処理されたドキュメントがディスクに書き込まれる方法（フォーマットやファイル名など）を定義します。

```java
SaveOptions so = new SaveOptions();
so.setRedactedFileSuffix("_scan");
```

出力ファイルは `yourfile_scan.pdf` という名前になります（または後で指定したフォーマット）。

## 手順 3: ラスタライズの有効化

`RasterizationOptions` オブジェクトは、保存前に各ページを画像ベースでレンダリングすることを可能にします。

```java
so.getRasterization().setEnabled(true);
```

## 手順 4: グレースケール変換の適用

`AdvancedRasterizationOptions.Grayscale` は、ラスタライズされた画像が灰色の濃淡のみを使用するよう強制するフラグです。

```java
so.getRasterization().addAdvancedOption(AdvancedRasterizationOptions.Grayscale);
```

## 手順 5: ドキュメント変換の実行

`save()` を呼び出すと、全処理パイプラインが実行され、出力ファイルが書き込まれます。

```java
redactor.save(so);
```

この行が実行された後、ディスク上に完全にラスタライズされ、グレースケール化された新しいファイルが `_scan` サフィックス付きで作成されます。

## 手順 6: 適切なリソース管理

`close()` メソッドはネイティブリソースを解放し、一時ファイルを削除します。

```java
finally { redactor.close(); }
```

最新の Java では、try‑with‑resources パターンを使用して `Redactor` を自動的にクローズすることもできます。

```java
try (Redactor redactor = new Redactor(Constants.MULTIPAGE_SAMPLE_DOCX)) {
    // Your processing code here
}
// Automatic cleanup happens here
```

どちらのアプローチも安全ですが、後者の方が簡潔です。

## 詳細設定オプション

### 品質またはサイズのための DPI 調整

DPI を高くすると画像が鮮明になり（印刷に適しています）、低くするとファイルサイズが小さくなります。一般的なバランスは、画面表示用に 150 DPI、印刷用 PDF に 300 DPI です。

```java
saveOptions.getRasterization().setDpi(300); // High quality for printing
// or
saveOptions.getRasterization().setDpi(150); // Balanced quality and size
```

### 出力フォーマットの選択

ラスタライズ結果を PDF、TIFF、PNG などの特定のコンテナフォーマットに強制的に設定できます。PDF は最も広く使用されているアーカイブフォーマットです。

```java
saveOptions.setRasterizationFormat(RasterizationFormat.PDF);
```

## 一般的なユースケース

- **法的文書のアーカイブ** – 編集できない不変のグレースケール PDF を作成します。  
- **印刷準備済みレポート** – 大量印刷時に一貫した白黒出力を保証します。  
- **コンプライアンスワークフロー** – レダクションとグレースケール ラスタライズを組み合わせ、厳格なデータプライバシー規制に対応します。

## 一般的な問題と解決策

| 問題 | 発生理由 | 対策 |
|------|----------|------|
| 出力ファイルが予想より大きい | DPI が高すぎるか画像圧縮が無効 | DPI を下げる（例: 150）または `RasterizationOptions` で圧縮を有効にする。 |
| テキストがぼやけている | 元のフォントサイズに対して DPI が不足している | DPI を 300 以上に上げる。 |
| 大きなドキュメントで `OutOfMemoryError` が発生する | ドキュメント全体がメモリにロードされるため | ストリーミング API を使用するか、サポートされていればページ単位でバッチ処理する。 |
| グレースケールが適用されない | 高度オプションが正しく追加されていない | `addAdvancedOption(AdvancedRasterizationOptions.Grayscale)` が `save()` の前に呼び出されていることを確認する。 |

## よくある質問

**Q: ラスタライズせずにドキュメントをグレースケールに変換できますか？**  
A: GroupDocs.Redaction では、グレースケールオプションはラスタライズに結び付いており、結果の一貫性とセキュリティ層を提供します。

**Q: どのドキュメントフォーマットがグレースケール ラスタライズをサポートしていますか？**  
A: GroupDocs.Redaction がサポートするすべての主要フォーマット（DOCX、PDF、XLSX、PPTX、RTF など 100 以上）をラスタライズしてグレースケールに変換できます。

**Q: ラスタライズはドキュメントのファイルサイズに影響しますか？**  
A: はい。テキストが多いファイルはサイズが増加し、画像が多いファイルは縮小することがあります。DPI 設定が最も大きな影響を与えます。

**Q: グレースケール ラスタライズのプロセスを逆にすることは可能ですか？**  
A: できません。ラスタライズは一方向であり、元に戻す必要がある場合は元のバックアップを保持してください。

**Q: グレースケール ラスタライズされたドキュメントの品質を最適化するにはどうすればよいですか？**  
A: 高い DPI（印刷品質なら 300 以上）を使用し、アーカイブに最適な PDF を出力フォーマットとして選択してください。

## 結論

これで、GroupDocs.Redaction for Java を使用して **PDF をグレースケールにラスタライズ** する完全な本番向け手順が手に入りました。ラスタライズを有効にし、グレースケールの高度オプションを追加し、リソースを適切に管理することで、コンプライアンス基準を満たし、どのビューアでも一貫した外観を保つ安全で印刷に適したドキュメントを作成できます。

---

**Last Updated:** 2026-05-17  
**Tested With:** GroupDocs.Redaction 23.11 for Java  
**Author:** GroupDocs  

---

## ターゲットキーワード:

**Primary Keyword (HIGHEST PRIORITY):**
how to rasterize pdf

**Secondary Keywords (SUPPORTING):**
java pdf to image, apply grayscale filter pdf

## 関連チュートリアル

- [GroupDocs.Redaction Java 用 ラスタライズオプションチュートリアル](/redaction/java/rasterization-options/)
- [Java 用 GroupDocs Redaction の使用方法: Word ドキュメントの事前ラスタライズ](/redaction/java/rasterization-options/groupdocs-redaction-java-pre-rasterization-word-docs/)
- [Java のカスタムノイズラスタライズ&#58; GroupDocs.Redaction で機密情報を保護](/redaction/java/rasterization-options/java-groupdocs-redaction-custom-noise-rasterization/)