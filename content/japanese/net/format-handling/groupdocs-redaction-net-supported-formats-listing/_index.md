---
date: '2026-07-20'
description: GroupDocs.Redaction .NET を使用してフォーマットを一覧表示する方法を学び、機能をドキュメントワークフローに統合し、パフォーマンスを向上させましょう。
keywords:
- how to list formats
- GroupDocs.Redaction supported formats
- .NET document processing
lastmod: '2026-07-20'
og_description: GroupDocs.Redaction .NET を使用してフォーマットを一覧表示する方法を見つけ、ステップバイステップのガイドをご覧いただき、.NET
  アプリケーションで最適なパフォーマンスを得るためのヒントをご提供します。
og_image_alt: Guide showing how to list supported file formats with GroupDocs.Redaction
  in a .NET project
og_title: GroupDocs.Redaction .NET でフォーマットを一覧表示する方法
schemas:
- author: GroupDocs
  dateModified: '2026-07-20'
  description: Learn how to list formats using GroupDocs.Redaction .NET, integrate
    the feature into your document workflow, and improve performance.
  headline: How to List Formats with GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to list formats using GroupDocs.Redaction .NET, integrate
    the feature into your document workflow, and improve performance.
  name: How to List Formats with GroupDocs.Redaction .NET
  steps:
  - name: '**Document Management Systems** – Validate uploads against the supported
      list to prevent processing failures.'
    text: '**Document Management Systems** – Validate uploads against the supported
      list to prevent processing failures.'
  - name: '**Content Security** – Apply redaction rules only to file types that the
      engine can safely modify.'
    text: '**Content Security** – Apply redaction rules only to file types that the
      engine can safely modify.'
  - name: '**Batch Processing Pipelines** – Filter large file batches before invoking
      redaction, saving CPU and memory.'
    text: '**Batch Processing Pipelines** – Filter large file batches before invoking
      redaction, saving CPU and memory.'
  - name: '**How do I install GroupDocs.Redaction for .NET?**'
    text: '**How do I install GroupDocs.Redaction for .NET?**'
  - name: '**What are some common issues when retrieving supported formats?**'
    text: '**What are some common issues when retrieving supported formats?**'
  - name: '**Can I use this feature with non‑.NET applications?**'
    text: '**Can I use this feature with non‑.NET applications?**'
  - name: '**How can I optimise performance when using GroupDocs.Redaction?**'
    text: '**How can I optimise performance when using GroupDocs.Redaction?**'
  - name: '**What file types does GroupDocs.Redaction support?**'
    text: '**What file types does GroupDocs.Redaction support?**'
  type: HowTo
- questions:
  - answer: Yes, `FileType.GetSupportedFileFormats()` is static and does not require
      a `Redactor` object.
    question: Can I retrieve the format list without initializing a Redactor instance?
  - answer: The method returns all formats that the library can both read and write;
      each `FileType` includes a `CanRead` and `CanWrite` flag.
    question: Does the list include both input and output formats?
  - answer: GroupDocs releases format updates with each library version; checking
      the list at runtime ensures you always have the latest set.
    question: How often is the supported format list updated?
  - answer: Yes, filter the collection where `format.Extension == ".pdf"` or where
      `format.Name.Contains("PDF")`.
    question: Is there a way to filter only PDF‑compatible formats?
  - answer: The method requires .NET Core 3.1 or later; earlier runtimes are not supported.
    question: Will this approach work on .NET Core 2.1?
  type: FAQPage
tags:
- how to list formats
- GroupDocs.Redaction
- .NET file handling
title: GroupDocs.Redaction .NET でフォーマットを一覧表示する方法
type: docs
url: /ja/net/format-handling/groupdocs-redaction-net-supported-formats-listing/
weight: 1
---

# GroupDocs.Redaction .NET でフォーマットを一覧表示する方法

文書中心のアプリケーションを構築する開発者にとって、さまざまな文書タイプを管理することは日常的な現実です。このチュートリアルでは、GroupDocs.Redaction .NET が扱える **フォーマットの一覧表示方法** を学び、処理前にファイルを検証し、ユーザーに正確なオプションを提示し、ワークフローを効率的に保つことができます。

## はじめに

効率的な文書処理は、ライブラリが正確にサポートしているファイルタイプを把握することから始まります。GroupDocs.Redaction はこの情報を取得するための組み込みメソッドを提供しており、動的な UI 要素の構築、検証ルールの適用、ランタイムエラーの回避が可能です。以下では、インストールから実用的なコードスニペット、パフォーマンスのヒントまで、必要なすべてを紹介します。

### クイック回答
- **“how to list formats” とは何ですか？** これは、GroupDocs.Redaction が処理できるファイル拡張子のコレクションを取得することを指します。  
- **ライセンスは必要ですか？** はい、製品環境で使用するには有効な GroupDocs.Redaction ライセンスが必要です。  
- **サポートされている .NET バージョンはどれですか？** .NET Framework 4.6 以上、.NET Core 3.1 以上、.NET 5/6/7。  
- **利用可能なフォーマットは何件ですか？** 標準で 30 以上の入力および出力フォーマットがサポートされています。  
- **特別な設定は必要ですか？** 標準的なライブラリの初期化以外に追加設定は不要です。

## “how to list formats” とは何か

これは、ライブラリの FileType API を呼び出して、各エントリにファイル拡張子と人間が読める名前が含まれるコレクションを取得することを意味します。開発者はこのコレクションを反復処理して検証ルールを構築したり、UI のドロップダウンを埋めたり、サポートされているタイプをログに記録したりでき、互換性のある文書のみが処理されるようにします。

## GroupDocs.Redaction でフォーマットを一覧表示する理由

GroupDocs.Redaction は **30 以上** の異なるファイルタイプ（PDF、DOCX、PPTX、画像フォーマットなど）をサポートしており、サードパーティのコンバータを使用せずにほとんどのエンタープライズ文書を処理できます。これらのフォーマットをプログラムで一覧表示することで、推測を排除し、サポートチケットを減らし、互換性のあるファイルだけが処理パイプラインに入ることを保証します。

## 前提条件

- **GroupDocs.Redaction for .NET** – 公式サイトから最新パッケージをダウンロードします。  
- **.NET Framework または .NET Core** – 開発環境と互換性があります。  
- **Visual Studio**（または C# 対応の任意の IDE）。  
- C# 構文の基本的な知識。

## GroupDocs.Redaction for .NET のセットアップ

### .NET CLI
`dotnet add package GroupDocs.Redaction`

### パッケージマネージャー
`Install-Package GroupDocs.Redaction`

### NuGet パッケージマネージャー UI
- **“GroupDocs.Redaction”** を検索し、最新バージョンをインストールします。

### ライセンス取得
GroupDocs は無料トライアル、評価用の一時ライセンス、またはフル購入オプションを提供しています。適切なライセンスファイルを取得するには、GroupDocs のウェブサイトをご覧ください。

### 基本的な初期化とセットアップ
After adding the package, reference the namespace and create a `Redactor` instance:

```csharp
using GroupDocs.Redaction;

// Initialize with a license file (replace path as needed)
Redactor redactor = new Redactor("path/to/license/file.lic");
```

## 実装ガイド

### GroupDocs.Redaction .NET でフォーマットを一覧表示するには？
ライブラリをロードし、静的ヘルパーを呼び出して結果をソートします。これにより、わずか 2 行のコードで使用可能なコレクションが得られます。`FileType.GetSupportedFileFormats()` を使用して、各フォーマットの拡張子と表示名を含む `IEnumerable<FileType>` を取得し、拡張子で並べ替えて UI に適した一覧を作成します。

### サポートされているファイルフォーマットの取得

#### 概要
目的は、GroupDocs.Redaction が扱えるファイルタイプの一覧を取得し、検証ロジック、UI のドロップダウン、またはロギング機構への統合を容易にすることです。

#### 手順実装

**1. サポートされているファイルタイプの取得**  
`FileType.GetSupportedFileFormats()` はライブラリが認識するすべてのフォーマットを返します。このメソッドは `GroupDocs.Redaction.FileType` クラスの一部で、ファイル拡張子やフレンドリーネームなどのメタデータをカプセル化しています。

**2. サポートされているファイルタイプの表示**  
コレクションを反復処理し、各フォーマットの拡張子と説明を出力します。インラインコード例:

```csharp
var formats = FileType.GetSupportedFileFormats()
                      .OrderBy(f => f.Extension);

foreach (var format in formats)
{
    Console.WriteLine($"{format.Extension} – {format.Name}");
}
```

このスニペットは “.pdf – Portable Document Format” のように整然としたリストを出力し、UI 要素への入力に最適です。

### トラブルシューティングのヒント
- **Missing Package** – 必要に応じて NuGet パッケージ参照を確認し、パッケージを復元してください。  
- **Incorrect License Path** – ライセンスファイルが出力ディレクトリにコピーされていること、または絶対パスを指定していることを確認してください。  
- **Unsupported Extension** – フォーマットが一覧にない場合は、最新のライブラリバージョンを使用しているか確認してください。新しいリリースでは追加のフォーマットがサポートされています。

## 実用的な活用例

サポートされているファイルフォーマットを理解することで、さまざまな実務シナリオが実現します。

1. **Document Management Systems** – アップロードをサポートリストと照合して検証し、処理失敗を防止します。  
2. **Content Security** – エンジンが安全に変更できるファイルタイプにのみ赤字ルールを適用します。  
3. **Batch Processing Pipelines** – 赤字処理を呼び出す前に大量のファイルバッチをフィルタリングし、CPU とメモリを節約します。

## パフォーマンス上の考慮点

- **Memory Footprint** – フォーマットの一覧取得は軽量な操作であり、ドキュメントをメモリに読み込むことはありません。  
- **Batch Operations** – 数百のファイルを処理する際は、フォーマットリストを一度取得して再利用し、冗長な呼び出しを回避します。  
- **Thread Safety** – `FileType.GetSupportedFileFormats()` はスレッドセーフで、同期なしで並列タスクから呼び出すことができます。

## 結論

これで、GroupDocs.Redaction .NET を使用した **フォーマットの一覧表示** の完全かつ本番環境向けのアプローチが手に入りました。この機能を統合することで、検証を強化し、ユーザーエクスペリエンスを向上させ、文書パイプラインを堅牢に保つことができます。

### 次のステップ
- `Redactor` API を調査し、ファイルタイプに基づく赤字ルールを適用します。  
- フォーマットリストをフロントエンドのドロップダウンと組み合わせ、シームレスなファイル選択を実現します。  
- パフォーマンスガイドを確認し、大規模バッチジョブを最適化します。

## よくある質問

**Q: Redactor インスタンスを初期化せずにフォーマットリストを取得できますか？**  
A: はい、`FileType.GetSupportedFileFormats()` は静的メソッドで、`Redactor` オブジェクトは不要です。

**Q: リストには入力フォーマットと出力フォーマットの両方が含まれますか？**  
A: このメソッドは、ライブラリが読み書き可能なすべてのフォーマットを返します。各 `FileType` には `CanRead` と `CanWrite` フラグが含まれます。

**Q: サポートされているフォーマットリストはどのくらいの頻度で更新されますか？**  
A: GroupDocs は各ライブラリバージョンでフォーマットの更新を行います。実行時にリストを確認することで、常に最新のセットを取得できます。

**Q: PDF 互換のフォーマットだけをフィルタリングする方法はありますか？**  
A: はい、`format.Extension == ".pdf"` または `format.Name.Contains("PDF")` でコレクションをフィルタリングします。

**Q: このアプローチは .NET Core 2.1 で動作しますか？**  
A: このメソッドは .NET Core 3.1 以降が必要で、以前のランタイムはサポートされていません。

## FAQ セクション

1. **GroupDocs.Redaction for .NET をインストールするには？**  
   CLI コマンド `dotnet add package GroupDocs.Redaction` を使用するか、NuGet パッケージマネージャー UI からインストールします。  

2. **サポートされているフォーマット取得時の一般的な問題は何ですか？**  
   すべての依存関係が復元されていること、正しい名前空間（`GroupDocs.Redaction`）を参照していることを確認してください。  

3. **この機能を .NET 以外のアプリケーションで使用できますか？**  
   本チュートリアルは .NET に焦点を当てていますが、GroupDocs は Java、Python、その他のプラットフォーム向けに同様の API を提供しています。  

4. **GroupDocs.Redaction 使用時のパフォーマンスを最適化するには？**  
   フォーマットリストを再利用し、互換性のみを確認する場合は全文書の読み込みを避け、バッチジョブ中のメモリ使用量を監視します。  

5. **GroupDocs.Redaction がサポートするファイルタイプは何ですか？**  
   ライブラリは PDF、DOCX、PPTX、XLSX、BMP、PNG、JPEG などを含む 30 以上のフォーマットをサポートしています。全リストは `FileType.GetSupportedFileFormats()` で確認できます。

## リソース

- [ドキュメント](https://docs.groupdocs.com/redaction/net/)
- [API リファレンス](https://reference.groupdocs.com/redaction/net)
- [GroupDocs.Redaction のダウンロード](https://releases.groupdocs.com/redaction/net/)
- [無料サポートフォーラム](https://forum.groupdocs.com/c/redaction/33)
- [一時ライセンス](https://purchase.groupdocs.com/temporary-license/)

---

**最終更新日:** 2026-07-20  
**テスト環境:** GroupDocs.Redaction 4.2.0 for .NET  
**作者:** GroupDocs  

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

```csharp
using GroupDocs.Redaction;
// Initialize the Redactor with file path
Redactor redactor = new Redactor("sample.pdf");
```

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using GroupDocs.Redaction;

// Step 1: Use GroupDocs.Redaction API to fetch all supported formats.
IEnumerable<FileType> supportedFileTypes = FileType.GetSupportedFileFormats().OrderBy(f => f.Extension);
```

```csharp
// Step 2: Loop through the list of file types and print details.
foreach (FileType fileType in supportedFileTypes)
{
    Console.WriteLine($"{fileType.Extension} - {fileType.FileFormatName}");
}
```

## 関連チュートリアル

- [GroupDocs.Redaction .NET のフォーマット処理チュートリアル](/redaction/net/format-handling/)
- [GroupDocs.Redaction for .NET のドキュメントロードチュートリアル](/redaction/net/document-loading/)
- [GroupDocs.Redaction .NET のドキュメント保存チュートリアル](/redaction/net/document-saving/)