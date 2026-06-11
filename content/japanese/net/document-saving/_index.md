---
date: 2026-06-11
description: GroupDocs.Redaction for .NET を使用して、編集済みファイルのエクスポート方法、出力フォルダーの設定、ラスタライズされた
  PDF の作成、ストリームへの保存方法を学びます。
keywords:
- how to export redacted
- configure output folder
- create rasterized pdf
- save rasterized pdf
- convert redacted to pdf
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to export redacted files, configure output folders, create
    rasterized PDFs, and save to streams using GroupDocs.Redaction for .NET.
  headline: How to Export Redacted Documents with GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to export redacted files, configure output folders, create
    rasterized PDFs, and save to streams using GroupDocs.Redaction for .NET.
  name: How to Export Redacted Documents with GroupDocs.Redaction .NET
  steps:
  - name: Install the NuGet Package
    text: 'Add the latest GroupDocs.Redaction package to your project:'
  - name: Load the Document and Define Redactions
    text: Create a `Redactor` instance, load the file, and specify the regions you
      want to hide. The `Redactor` class provides the core functionality for loading
      documents and applying redaction rules.
  - name: Choose the Export Method
    text: '#### Export in Original Format'
  type: HowTo
- questions:
  - answer: Yes, GroupDocs.Redaction can convert most input types to PDF, DOCX, XLSX,
      PPTX, or rasterized PDF, covering over 30 formats.
    question: Can I export to a format that wasn’t originally supported?
  - answer: By rendering each page as a flat image, any hidden text layers are removed,
      making it impossible to extract the original content.
    question: How does rasterization protect redacted data?
  - answer: Absolutely – you can call `Apply` repeatedly or pass a collection of `RedactionOptions`
      to process many patterns in one pass. `RedactionOptions` defines the settings
      for a single redaction operation, such as region and replacement type.
    question: Is it possible to chain multiple redaction rules?
  - answer: The `Redactor` implements `IDisposable`; wrap it in a `using` block or
      call `Dispose()` to release file handles promptly. `IDisposable` is an interface
      that provides a mechanism for releasing unmanaged resources.
    question: Do I need to close the Redactor object?
  - answer: GroupDocs.Redaction is validated on .NET Framework 4.6+, .NET Core 3.1+,
      and .NET 5/6/7.
    question: What .NET runtimes are officially tested?
  type: FAQPage
title: GroupDocs.Redaction .NET を使用した編集済みドキュメントのエクスポート方法
type: docs
url: /ja/net/document-saving/
weight: 3
---

# GroupDocs.Redaction .NET を使用した編集済みドキュメントのエクスポート方法

この包括的なガイドでは、GroupDocs.Redaction for .NET を使用して **編集済みコンテンツのエクスポート方法** を安全かつ効率的に学びます。元のファイル形式を保持したい場合、ドキュメントをラスタライズ PDF としてロックダウンしたい場合、または結果をメモリ上に直接ストリームしたい場合でも、明快で会話調の説明と実践的なヒントとともにすべてのオプションをご案内します。このチュートリアルの最後までに、コンプライアンス重視のシナリオに最適なエクスポート戦略を選択できるようになります。

## クイック回答
- **どのフォーマットにエクスポートできますか？** GroupDocs.Redaction がサポートする 30 以上のネイティブフォーマットに加え、最大のセキュリティを提供するラスタライズ PDF も利用可能です。  
- **ストリーミングにライセンスは必要ですか？** はい、本番環境でのストリーミングには有効な GroupDocs.Redaction ライセンスが必要です。  
- **カスタム出力フォルダーを設定できますか？** もちろんです – `OutputPath` プロパティまたは `SaveOptions` を使用して構成できます。  
- **ラスタライズは大容量ファイルでも安全ですか？** ファイル全体をメモリに読み込むことなく、最大 500 ページのドキュメントを処理できます。  
- **対応している .NET バージョンは？** .NET Framework 4.6+、.NET Core 3.1+、.NET 5/6/7。

## GroupDocs.Redaction とは？
GroupDocs.Redaction は、PDF、Word、Excel、PowerPoint、画像など多数のフォーマットから機密情報をプログラムで削除またはマスクする .NET ライブラリです。編集領域の定義、ポリシーの適用、最終的なクリーンドキュメントのエクスポートを行う高レベル API を提供し、任意の .NET アプリケーションに編集機能を簡単に統合できます。

## なぜ編集済みドキュメントをラスタライズ PDF としてエクスポートするのか？
ラスタライズ PDF は各ページをフラットな画像に変換し、後から抽出可能な隠れたテキスト層を排除します。この形式は、編集済みコンテンツが復元できないことを保証し、GDPR や HIPAA などの厳格な規制基準を満たします。GroupDocs.Redaction は最大 300 dpi のラスタライズ PDF を生成でき、視覚的忠実度を保ちつつセキュリティを確保します。

## 編集済みドキュメントをエクスポートする方法
ソースファイルを読み込み、編集ルールを適用した後、適切な保存メソッドを呼び出します – 元の形式で保存する場合は `Save`、画像のみの PDF にする場合は `SaveAsRasterizedPdf`、メモリ内で処理する場合は `SaveToStream` を使用します。以下にステップバイステップのワークフローを示します。各メソッドは、編集済みコンテンツを永続的に除去しながら希望の出力形式を保持します。

### 手順 1: NuGet パッケージをインストール
プロジェクトに最新の GroupDocs.Redaction パッケージを追加します：

```bash
dotnet add package GroupDocs.Redaction
```

### 手順 2: ドキュメントを読み込み、編集範囲を定義
`Redactor` インスタンスを作成し、ファイルを読み込んで非表示にしたい領域を指定します。`Redactor` クラスはドキュメントの読み込みと編集ルールの適用のコア機能を提供します。

```csharp
using GroupDocs.Redaction;
using GroupDocs.Redaction.Options;

// Load the document
var redactor = Redactor.Create("SensitiveReport.docx");

// Define a redaction for a specific text pattern
redactor.Apply(new RedactionOptions
{
    SearchPattern = "SSN: \\d{3}-\\d{2}-\\d{4}",
    RedactionColor = System.Drawing.Color.Black,
    RedactionType = RedactionType.Image
});
```

### 手順 3: エクスポート方法を選択
#### 元のフォーマットでエクスポート
```csharp
redactor.Save("RedactedReport.docx");
```

#### ラスタライズ PDF としてエクスポート
```csharp
var rasterOptions = new RasterizationOptions { Dpi = 300 };
redactor.SaveAsRasterizedPdf("RedactedReport.pdf", rasterOptions);
```

#### メモリストリームへエクスポート（Web API に最適）
```csharp
using var stream = new MemoryStream();
redactor.Save(stream, SaveOptions.CreatePdf());
stream.Position = 0; // Reset for reading
```

`Save` メソッドは編集済みドキュメントを元の形式のファイルとして書き出します。`SaveAsRasterizedPdf` は各ページを画像としてレンダリングした PDF を作成し、隠れたテキストを除去します。`SaveToStream` は編集済みファイルをメモリストリームとして返し、Web 応答に適しています。

## 出力フォルダーの設定方法
`Redactor` の `OutputPath` プロパティを設定するか、目的のディレクトリを含むカスタム `SaveOptions` オブジェクトを渡します。`OutputPath` は `Redactor` のプロパティで、出力ファイルが書き込まれるディレクトリを指定します。`SaveOptions` を使用すると、出力フォルダーを含むさまざまな保存パラメータをカスタマイズできます。これにより、すべてのエクスポートファイルが予測可能な場所に配置され、バッチ処理パイプラインが簡素化されます。ドキュメントタイプごとにサブフォルダーを指定して作業領域を整理することも可能です。

```csharp
var options = SaveOptions.CreatePdf();
options.OutputPath = @"C:\RedactedOutputs\";
redactor.Save(options);
```

## よくある問題と解決策
- **Redaction not applied:** 編集が適用されない場合は、検索パターンがドキュメントテキストと完全に一致しているか確認してください。必要に応じて `RegexOptions.IgnoreCase` を使用します。`RegexOptions` は正規表現のマッチ動作（大文字小文字の区別など）を制御する列挙型です。  
- **Large files cause memory pressure:** 大容量ファイルでメモリ負荷が高くなる場合は、`SaveToStream` を使用してストリーミングモードを有効にし、`Save` を全体ドキュメントに対して呼び出さないようにします。  
- **Rasterized PDF looks blurry:** ラスタライズ PDF がぼやけて見える場合は、`RasterizationOptions` の DPI（例: 300–600）を上げて画像品質を向上させます。`RasterizationOptions` では DPI や画像形式など、ラスタライズ PDF 出力のパラメータを設定できます。

## よくある質問

**Q: 元々サポートされていないフォーマットへエクスポートできますか？**  
A: はい、GroupDocs.Redaction はほとんどの入力タイプを PDF、DOCX、XLSX、PPTX、またはラスタライズ PDF に変換でき、30 以上のフォーマットに対応しています。

**Q: ラスタライズは編集済みデータをどのように保護しますか？**  
A: 各ページをフラットな画像としてレンダリングすることで、隠れたテキスト層が除去され、元のコンテンツを抽出できなくなります。

**Q: 複数の編集ルールを連鎖させることは可能ですか？**  
A: もちろんです – `Apply` を繰り返し呼び出すか、`RedactionOptions` のコレクションを渡して一括で多数のパターンを処理できます。`RedactionOptions` は単一の編集操作（領域や置換タイプなど）の設定を定義します。

**Q: Redactor オブジェクトを閉じる必要がありますか？**  
A: `Redactor` は `IDisposable` を実装しています。`using` ブロックでラップするか、`Dispose()` を呼び出してファイルハンドルを速やかに解放してください。`IDisposable` はアンマネージドリソースの解放メカニズムを提供するインターフェイスです。

**Q: 公式にテストされている .NET ランタイムはどれですか？**  
A: GroupDocs.Redaction は .NET Framework 4.6+、.NET Core 3.1+、および .NET 5/6/7 で検証されています。

## 追加リソース

### 利用可能なチュートリアル

- [GroupDocs.Redaction for .NET を使用したラスタライズ PDF としてドキュメントを保存する方法：完全ガイド](./groupdocs-redaction-net-rasterized-pdfs/)
- [GroupDocs.Redaction を使用した .NET の出力ディレクトリ実装：包括的ガイド](./implement-output-directory-groupdocs-redaction-dotnet/)
- [GroupDocs.Redaction for .NET を使用したドキュメントの編集と保存：完全ガイド](./redact-save-documents-groupdocs-redaction-net/)
- [GroupDocs.Redaction .NET を使用して元の形式で編集済みドキュメントを保存する方法](./save-redacted-docs-original-format-groupdocs-redaction-net/)
- [ストリームを使用した .NET の安全なドキュメント編集：GroupDocs.Redaction ガイド](./secure-document-redaction-net-streams-groupdocs-redaction/)

### 便利なリンク

- [GroupDocs.Redaction for Net Documentation](https://docs.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction for Net API Reference](https://reference.groupdocs.com/redaction/net/)
- [Download GroupDocs.Redaction for Net](https://releases.groupdocs.com/redaction/net/)
- [GroupDocs.Redaction Forum](https://forum.groupdocs.com/c/redaction/33)
- [Free Support](https://forum.groupdocs.com/)
- [Temporary License](https://purchase.groupdocs.com/temporary-license/)

---

**最終更新日:** 2026-06-11  
**テスト環境:** GroupDocs.Redaction 23.11 for .NET  
**作者:** GroupDocs  

## 関連チュートリアル

- [GroupDocs.Redaction .NET を使用して元の形式で編集済みドキュメントを保存する方法](/redaction/net/document-saving/save-redacted-docs-original-format-groupdocs-redaction-net/)
- [GroupDocs.Redaction for .NET を使用したラスタライズ PDF としてドキュメントを保存する方法：完全ガイド](/redaction/net/document-saving/groupdocs-redaction-net-rasterized-pdfs/)
- [ストリームを使用した .NET の安全なドキュメント編集：GroupDocs.Redaction ガイド](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)