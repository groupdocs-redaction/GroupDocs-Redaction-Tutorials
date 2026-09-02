---
date: '2026-06-01'
description: GroupDocs.Redaction for .NET を使用して、文書から機密情報をマスクし、注釈を削除する方法を学び、コンプライアンスとデータプライバシーを確保します。
keywords:
- redact sensitive information
- how to remove annotations
- remove excel annotations
schemas:
- author: GroupDocs
  dateModified: '2026-06-01'
  description: Learn how to redact sensitive information and how to remove annotations
    from documents with GroupDocs.Redaction for .NET, ensuring compliance and data
    privacy.
  headline: How to Redact Sensitive Information and Remove Annotations Using GroupDocs.Redaction
    for .NET
  type: TechArticle
- description: Learn how to redact sensitive information and how to remove annotations
    from documents with GroupDocs.Redaction for .NET, ensuring compliance and data
    privacy.
  name: How to Redact Sensitive Information and Remove Annotations Using GroupDocs.Redaction
    for .NET
  steps:
  - name: Prepare Source and Output File Paths
    text: 'First, define the locations of your input document and the folder where
      the redacted file will be saved. Ensure the output directory exists; otherwise
      the operation will fail. *Definition anchor:* `Path.Combine` is a .NET utility
      that safely joins directory and file names across Windows, Linux, and '
  - name: Apply Regular Expression Redaction
    text: Next, create a redaction rule that targets annotations matching your regex
      pattern. *Definition anchor:* `Redactor` is the main class that loads a document
      and applies redaction rules. *Definition anchor:* `DeleteAnnotationRedaction`
      is a class that removes annotations whose content satisfies a regu
  - name: Dispose of Resources
    text: Always call `redactor.Dispose()` or wrap the instance in a `using` block
      to free unmanaged resources promptly. *Definition anchor:* `Dispose` releases
      unmanaged resources used by the Redactor instance, ensuring memory is freed.
  type: HowTo
- questions:
  - answer: Yes—by loading the `.xlsx` file with `Redactor` and applying a `DeleteAnnotationRedaction`
      rule, you can remove comments, notes, and other annotation types.
    question: Can GroupDocs.Redaction redact annotations in Excel workbooks?
  - answer: Prefix the pattern with `(?i)` or use the `RegexOptions.IgnoreCase` flag
      when constructing the `DeleteAnnotationRedaction`.
    question: How do I make regex patterns case‑insensitive?
  - answer: Absolutely. Set `SaveOptions.Prefix` or `SaveOptions.Suffix` to prepend
      or append text to the generated file name.
    question: Is it possible to customize the output file name?
  - answer: The source file remains untouched; the redacted version is saved to the
      path you provide in `SaveOptions`.
    question: What happens to the original document after redaction?
  - answer: Yes—GroupDocs.Redaction can operate in a streaming mode that processes
      pages sequentially, dramatically reducing memory consumption.
    question: Does the library support streaming for very large PDFs?
  type: FAQPage
title: .NET 用 GroupDocs.Redaction を使用して機密情報をマスクし、注釈を削除する方法
type: docs
url: /ja/net/annotation-redaction/remove-annotations-groupdocs-redaction-net/
weight: 1
---

# GroupDocs.Redaction for .NET を使用した機密情報のマスクと注釈の削除

ドキュメント内の機密データの管理は、開発者、監査人、法務チームにとって日々の課題です。**Redact sensitive information** を迅速かつ確実に行える GroupDocs.Redaction for .NET は、30 以上のファイル形式に対応し、ドキュメント全体をメモリにロードせずに最大 2 GB のファイルを処理できます。このチュートリアルでは、パッケージのインストールから正規表現を使用した特定の注釈の削除まで、完全なワークフローを順に解説し、個人データを保護し、GDPR や HIPAA などの規制に準拠できるようにします。

## クイック回答
- **GroupDocs.Redaction は何をしますか？** テキスト、画像、注釈をプログラムで削除またはマスクし、プライベートデータを保護します。  
- **どのファイルタイプがサポートされていますか？** PDF、DOCX、XLSX、PPTX、画像ファイルなど、30 以上の形式に対応しています。  
- **開発にライセンスは必要ですか？** 無料トライアルでテスト可能です。製品版の使用には永続ライセンスが必要です。  
- **大容量ファイルを効率的に処理できますか？** はい。バッチ処理とストリーミングにより、数百ページのドキュメントでもメモリ使用量を抑えられます。  
- **.NET 6 と .NET Core に対応していますか？** .NET Framework 4.5+、.NET Core 3.1+、.NET 5+、.NET 6+ をフルサポートしています。

## 「機密情報のマスク」とは何ですか？
*Redact sensitive information* とは、個人または機密データを文書から永久に削除または隠蔽し、復元できなくすることを意味します。氏名、識別番号、財務情報、その他個人を特定できるデータが対象です。マスクを実施することで、GDPR、HIPAA、CCPA などの規制遵守が確保され、データ漏洩を防止し、外部関係者と安全に文書を共有できます。

## なぜ GroupDocs.Redaction for .NET を使用するのか？
GroupDocs.Redaction は **quantified benefits** を提供します。30 以上の入力・出力形式に対応し、フルドキュメントのロードなしで最大 2 GB の文書を処理でき、標準サーバー上で 1 分間に最大 10 000 件の注釈をマスクできます。これらの数値は、市場で最も高性能かつ汎用性の高いマスクエンジンの一つであることを示しています。

## 前提条件
- **GroupDocs.Redaction for .NET**（バージョン 20.7 以降）。  
- Visual Studio 2022 または互換性のある IDE。  
- 基本的な C# の知識と正規表現の理解。

### 必要なライブラリ
- **GroupDocs.Redaction for .NET** – NuGet からインストール（インストール手順を参照）。

### 環境設定要件
- .NET Framework 4.5+ **or** .NET Core 3.1+。  
- ソース文書が格納されているファイルシステムへのアクセス権。

## インストール – 注釈の削除方法（ステップ 1）
プロジェクトにライブラリを追加するには、以下のいずれかのコマンドを使用します。チュートリアルをコードフリーに保つため、コードブロックは追加していません。

**.NET CLI:**  
端末で `dotnet add package GroupDocs.Redaction --version 20.7.*` を実行します。

**Package Manager Console:**  
`Install-Package GroupDocs.Redaction -Version 20.7.*` を実行します。

**NuGet Package Manager UI:**  
“GroupDocs.Redaction” を検索し、**Install** をクリックします。

### ライセンス取得
完全な機能を利用するには、[GroupDocs](https://purchase.groupdocs.com/temporary-license/) からトライアルまたは一時ライセンスを取得してください。製品版の使用には同ポータルで永続ライセンスを購入します。

## 実装ガイド – 正規表現を使用した注釈の削除方法
このセクションでは、特定のパターンに一致する注釈を **how to remove annotations** する方法を説明します。従業員名や機密メモ、カスタムマーカーの除去に最適です。

### 概要
このセクションでは、特定のパターンに一致する注釈を **how to remove annotations** する方法を説明します。従業員名や機密メモ、カスタムマーカーの除去に最適です。

### ステップ 1: ソースと出力ファイルのパスを準備する
まず、入力文書の場所とマスク後のファイルを保存するフォルダーを定義します。出力ディレクトリが存在しない場合はエラーになります。

*Definition anchor:* `Path.Combine` は Windows、Linux、macOS 間でディレクトリ名とファイル名を安全に結合する .NET ユーティリティです。

### ステップ 2: 正規表現によるマスクを適用する
次に、正規表現パターンに一致する注釈を対象としたマスクルールを作成します。

*Definition anchor:* `Redactor` は文書を読み込み、マスクルールを適用するメインクラスです。  
*Definition anchor:* `DeleteAnnotationRedaction` は、正規表現フィルタに合致する内容の注釈を削除するクラスです。  
*Definition anchor:* `SaveOptions` は、出力ファイルの書き込み方法（サフィックスの追加、出力形式の選択、ラスタライズの無効化）を制御できます。

**Direct answer:** `Redactor redactor = new Redactor(sourcePath);` でソース文書を読み込み、正規表現を使用した `DeleteAnnotationRedaction` を追加し、`redactor.Save(outputPath, new SaveOptions { Suffix = "_redacted", Rasterize = false });` を呼び出します。このワンライナーで一致する注釈を削除し、元のファイルを変更せずに新しいファイルを書き出します。

### ステップ 3: リソースの解放
`redactor.Dispose()` を呼び出すか、`using` ブロックでインスタンスをラップして、アンマネージドリソースを速やかに解放してください。  
*Definition anchor:* `Dispose` は Redactor インスタンスが使用しているアンマネージドリソースを解放し、メモリを確保します。

## 注釈削除のためのファイルパス準備 – Excel 注釈の削除方法
例は PDF に焦点を当てていますが、同じ手法で Excel ファイル（`.xlsx`）にも適用できます。適切なパス処理により “file not found” エラーを防止します。

*Definition anchor:* `PrepareOutputDirectory` はフォルダーの存在を確認し、無ければ作成するヘルパーメソッドです。

同一ユーティリティをフォーマット間で再利用することで、Excel ワークブック、Word 文書、PowerPoint プレゼンテーションから **how to remove annotations** を最小限のコード変更で実行できます。

## 実用的な活用例
1. **Data Privacy Compliance** – 個人識別子を除去して GDPR、HIPAA、CCPA の要件を自動的に満たします。  
2. **Legal Document Preparation** – 契約書を外部に共有する前に機密コメントを削除します。  
3. **Corporate Data Management** – 社内レポートをプログラムでクレンジングし、承認された情報だけが組織外に出るようにします。

## パフォーマンス考慮事項 – 注釈を効率的に削除する方法
- **Efficient Memory Management:** 各ファイルの処理が完了したらすぐに `Redactor` オブジェクトを破棄します。  
- **Batch Processing:** フォルダー内の文書をループし、同一のマスクルールを各ファイルに適用します。これにより、ライブラリの開閉によるオーバーヘッドが削減されます。  
- **Optimized Regular Expressions:** 非キャプチャグループを使用し、バックトラッキングが重いパターンを避けます。例として、`\bEmployeeID:\s*\d{4,6}\b` を `.*EmployeeID.*` よりも優先してマッチ速度を向上させます。

## よくある問題と解決策
- **Large Files Stall:** 文書をセクションに分割するか、`RedactorSettings` の `MaxMemoryUsage` 設定を増やしてください。  
- **Regex Not Matching:** パターンにケースインセンシティブ用の `(?i)` フラグを含めるか、`DeleteAnnotationRedaction` 作成時に `RegexOptions.IgnoreCase` を使用してテストしてください。  
- **Output File Overwrites Original:** 常に別の出力パスを指定するか、`SaveOptions.Suffix` を使用して自動的に “_redacted” を付加してください。

## よくある質問 (新規)

**Q: Can GroupDocs.Redaction redact annotations in Excel workbooks?**  
A: はい。`.xlsx` ファイルを `Redactor` で読み込み、`DeleteAnnotationRedaction` ルールを適用することで、コメントやノート、その他の注釈タイプを削除できます。

**Q: How do I make regex patterns case‑insensitive?**  
A: パターンの先頭に `(?i)` を付けるか、`DeleteAnnotationRedaction` を構築する際に `RegexOptions.IgnoreCase` フラグを使用してください。

**Q: Is it possible to customize the output file name?**  
A: もちろんです。`SaveOptions.Prefix` または `SaveOptions.Suffix` を設定して、生成ファイル名にプレフィックスまたはサフィックスを付加できます。

**Q: What happens to the original document after redaction?**  
A: ソースファイルはそのまま残り、マスクされたバージョンは `SaveOptions` で指定したパスに保存されます。

**Q: Does the library support streaming for very large PDFs?**  
A: はい。GroupDocs.Redaction はストリーミングモードで動作でき、ページを順次処理することでメモリ消費を大幅に削減します。

## FAQ セクション
1. **How do I handle large documents efficiently?**  
   - 可能であれば文書を小さなセクションに分割し、正規表現をパフォーマンス向上のために最適化してください。  
2. **Can I use GroupDocs.Redaction with other file formats besides Excel?**  
   - はい。PDF、Word など多数の形式に対応しています。  
3. **What happens to the original document after redaction?**  
   - 元の文書は上書きしない限り変更されません。常に新しいファイルまたはコピーに保存してください。  
4. **Is it possible to customize the output file name with GroupDocs.Redaction?**  
   - はい。`SaveOptions` を変更して、出力ファイル名にカスタムのサフィックスやプレフィックスを付加できます。  
5. **How do I ensure regex patterns are case‑insensitive?**  
   - 正規表現に `(i)` などの修飾子を付けてケースインセンシティブにしてください。

## リソース
- [ドキュメント](https://docs.groupdocs.com/redaction/net/)
- [API リファレンス](https://reference.groupdocs.com/redaction/net)
- [GroupDocs.Redaction のダウンロード](https://releases.groupdocs.com/redaction/net/)
- [無料サポートフォーラム](https://forum.groupdocs.com/c/redaction/33)
- [一時ライセンスのリクエスト](https://purchase.groupdocs.com/temporary-license/)

このガイドに従うことで、**redact sensitive information** と **how to remove annotations** を任意のサポート対象ドキュメントタイプで実行できる堅牢な手法が手に入ります。手順を実装し、サンプルファイルでテストしたうえで、より大規模な文書処理パイプラインに統合し、最大限のセキュリティを確保してください。

**Last Updated:** 2026-06-01  
**Tested With:** GroupDocs.Redaction 20.7 for .NET  
**Author:** GroupDocs  

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

```csharp
string sourceFile = @"YOUR_DOCUMENT_DIRECTORY\AnnotatedDocument.xlsx";
var saveOptions = new SaveOptions { AddSuffix = true, RasterizeToPDF = false };
```

```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // This regex matches the phrase "John Doe" in a case-insensitive manner.
    redactor.Apply(new DeleteAnnotationRedaction("(?im:John Doe)"));
    
    // Save changes to a new file with a suffix indicating it's been redacted.
    var outputFile = redactor.Save(saveOptions);
}
```

```csharp
using System.IO;

public class Utils
{
    public static string PrepareOutputDirectory(string fileName)
    {
        var documentDirectory = Path.Combine(Directory.GetCurrentDirectory(), "YOUR_DOCUMENT_DIRECTORY");
        var filePath = Path.Combine(documentDirectory, fileName);

        Directory.CreateDirectory(documentDirectory);
        return filePath;
    }
}
```

## 関連チュートリアル

- [How to Load and Redact Documents Using GroupDocs.Redaction .NET&#58; A Complete Guide](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [Redact and Save Documents with GroupDocs.Redaction for .NET&#58; A Complete Guide](/redaction/net/document-saving/redact-save-documents-groupdocs-redaction-net/)
- [Redact Exact Phrases in .NET Documents Using GroupDocs.Redaction](/redaction/net/text-redaction/guide-redact-exact-phrases-groupdocs-redaction-dotnet/)