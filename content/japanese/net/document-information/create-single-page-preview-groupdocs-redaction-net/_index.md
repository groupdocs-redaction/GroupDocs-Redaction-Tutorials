---
date: '2026-06-06'
description: GroupDocs.Redaction for .NET を使用してページを PNG に変換し、PDF ページをプレビューする方法を学びます。ステップバイステップのガイド、コードスニペット、実践的なヒントを掲載。
keywords:
- convert page to png
- how to preview pdf
- GroupDocs.Redaction .NET
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to convert page to PNG and preview PDF pages with GroupDocs.Redaction
    for .NET. Step‑by‑step guide, code snippets, and real‑world tips.
  headline: Convert Page to PNG Using GroupDocs.Redaction .NET
  type: TechArticle
- questions:
  - answer: Yes, provide the password when initializing `RedactionEngine` and the
      preview will be created normally.
    question: Can I generate previews for password‑protected PDFs?
  - answer: Set `options.PreviewFormat = PreviewFormat.Jpeg` before calling the preview
      method.
    question: How do I change the output format from PNG to JPEG?
  - answer: Absolutely – assign an array of page numbers to `options.PageNumbers`
      (e.g., `new[] {0, 2, 4}`).
    question: Is it possible to preview multiple pages at once?
  - answer: Increase `options.Width` and `options.Height` to a higher resolution;
      the library scales the image accordingly.
    question: What should I do if the preview image is blurry?
  - answer: Yes, GroupDocs.Redaction .NET is cross‑platform and runs inside Docker
      containers that support .NET Core.
    question: Does this work on Linux containers?
  type: FAQPage
title: GroupDocs.Redaction .NET を使用してページを PNG に変換
type: docs
url: /ja/net/document-information/create-single-page-preview-groupdocs-redaction-net/
weight: 1
---

# GroupDocs.Redaction .NET を使用したページの PNG 変換

大きなドキュメントから単一ページのプレビューを作成することは、必要な情報だけを共有したいときに一般的な要件です。このチュートリアルでは、GroupDocs.Redaction for .NET を使用して **ページを PNG に変換する方法** を学び、プレビュー出力を設定し、結果をアプリケーションに統合する方法を紹介します。前提条件、インストール、コード設定、実用的なヒントを順に説明し、数分で単一ページの PNG プレビューを生成できるようにします。

## クイック回答
- **1ページだけの PNG プレビューを生成できますか？** はい、`PreviewOptions` を使用してページ番号とフォーマットを指定します。  
- **GroupDocs.Redaction がプレビューでサポートするフォーマットはどれですか？** PNG がデフォルトですが、JPEG と BMP も利用可能です。  
- **開発にライセンスは必要ですか？** 無料トライアルはテストに使用できますが、商用利用には本番ライセンスが必要です。  
- **.NET Core と .NET Framework でも動作しますか？** はい、ライブラリは .NET Standard 2.0+ を対象としています。  
- **大きなファイルでもメモリ効率は良いですか？** はい、API はページをストリーミングし、ドキュメント全体の読み込みを回避します。

## ページを PNG に変換するとは？
**convert page to PNG** は、サポートされているドキュメント（PDF、DOCX、PPTX など）から単一ページを抽出し、そのページを Portable Network Graphics（PNG）画像としてレンダリングすることを指します。生成された画像は元のページのレイアウト、フォント、グラフィックを保持し、ドキュメントの残りを隠したまま明確なスナップショットを共有できます。

## なぜ単一ページのプレビューを使用するのか？
単一ページの PNG プレビューを生成することで、帯域幅が削減され、読み込み時間が短縮され、必要な部分だけを公開することで機密コンテンツを保護できます。GroupDocs.Redaction は、一般的なサーバーハードウェア上で 300 ページの PDF を 0.5 秒未満で 200 KB の PNG にレンダリングでき、Web ポータルやレポートツールに最適です。

## 前提条件
- **GroupDocs.Redaction for .NET** – ドキュメントの赤字処理とプレビュー生成を行うコアライブラリです。  
- **System.IO** – ファイル操作用の標準 .NET 名前空間です。  
- .NET Core 3.1+ または .NET Framework 4.6.1+（.NET Standard 2.0 をサポートするプラットフォーム）  
- 基本的な C# の知識と NuGet パッケージ管理に関する知識が必要です。

## GroupDocs.Redaction for .NET の設定

### インストール情報

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```bash
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
- Visual Studio でプロジェクトを開きます。  
- **Manage NuGet Packages** を選択します。  
- **GroupDocs.Redaction** を検索し、最新の安定版をインストールします。

### ライセンス取得手順
ライブラリを実行するには有効なライセンスが必要です。無料トライアルで開始するか、一時キーをリクエストできます。

1. 一時ライセンスをリクエストするには、[GroupDocs website](https://purchase.groupdocs.com/temporary-license) にアクセスしてください。  
2. メールで送られた手順に従い、ライセンスファイルをプロジェクトに追加します。

### 基本的な初期化と設定
`RedactionEngine` クラスは、プレビュー生成を含むすべての操作のエントリーポイントです。  
```csharp
using GroupDocs.Redaction;

var redactor = new Redactor("path/to/your/document");
```  

## 実装ガイド

### 概要
このセクションでは、`PreviewOptions` を設定しプレビュー API を呼び出すことで **ページを PNG に変換** する方法を示します。このアプローチは PDF、DOCX、PPTX など、GroupDocs.Redaction がサポートする多くのフォーマットで機能します。

### 手順 1: 環境の準備
ソースファイルのパスと出力フォルダーを設定します。`Path.Combine` を使用してプラットフォームに依存しないパスを構築します。  
```csharp
// Define the directory and file name for output.
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
```  

### 手順 2: プレビューオプションの設定
`PreviewOptions` では、ページ番号、画像サイズ、出力フォーマットを定義できます。このクラスはプレビュー生成の設定ハブです。  
```csharp
int testPageNumber = 1;
string previewFileName = Utils.GetOutputFileByName(sourceFile, $"preview_page{testPageNumber}");

// Initialize the Redactor with the source file.
using (Redactor redactor = new Redactor(sourceFile))
{
    PreviewOptions options = new PreviewOptions(pageNumber => File.OpenWrite(previewFileName));

    // Set dimensions and format for the preview image.
    options.Width = 480;
    options.Height = 640;
    options.PageNumbers = new int[] { testPageNumber };
    options.PreviewFormat = PreviewOptions.PreviewFormats.PNG;

    // Generate and save the page preview.
    redactor.GeneratePreview(options);
}
```  

#### キー設定の説明
- **Width & Height** – ターゲットの表示解像度に合わせてこれらの値を調整します。  
- **PageNumbers** – レンダリングしたい正確なページインデックス（0 ベース）の配列を指定します。  
- **PreviewFormat** – デフォルトは PNG です。より小さいファイルにしたい場合は `PreviewFormat.Jpeg` に切り替えます。

### トラブルシューティングのヒント
PNG が生成されない場合は：

- ソースファイルのパスが正しく、ファイルにアクセス可能であることを確認してください。  
- 任意の API メソッドを呼び出す前にライセンスファイルがロードされていることを確認してください。  
- `PreviewOptions.PageNumbers` に有効なページインデックスが含まれていることを確認してください（例: 最初のページは `0`）。

## 実用的な活用例
単一ページの PNG プレビューの作成は、さまざまなシナリオで有用です：

1. **Client Presentations** – 関連するスライドまたは契約条項のみを表示します。  
2. **Internal Reviews** – 完全なドキュメントを開かずに迅速な視覚チェックを可能にします。  
3. **Content Summaries** – メールやダッシュボードにページスナップショットを埋め込み、即座にコンテキストを提供します。

この機能を CMS や CRM と統合すると、アップロードされたドキュメントのサムネイル生成を自動化でき、ユーザーエクスペリエンスが向上します。

## パフォーマンス上の考慮点
- **Memory Management** – 使用後に `RedactionEngine` インスタンスを破棄してリソースを解放します。  
- **Asynchronous Execution** – UI アプリケーションでは `await engine.GeneratePreviewAsync(...)` を使用してインターフェイスの応答性を保ちます。  
- **Library Updates** – GroupDocs.Redaction は **30 以上の入力および出力フォーマット** をサポートし、ファイル全体をメモリに読み込まずに最大 500 ページのドキュメントを処理します。パフォーマンス向上のためにパッケージを常に最新に保ってください。

## 結論
これで、**ページを PNG に変換** し、GroupDocs.Redaction for .NET を使用して単一ページのプレビューを生成する完全な本番対応の方法が手に入りました。上記の手順に従うことで、任意の .NET アプリケーションに高品質な PNG スナップショットを埋め込み、ドキュメント共有を強化しながらセキュリティとパフォーマンスを維持できます。

## よくある質問

**Q: パスワード保護された PDF のプレビューを生成できますか？**  
A: はい、`RedactionEngine` の初期化時にパスワードを提供すれば、プレビューは通常通り作成されます。

**Q: 出力フォーマットを PNG から JPEG に変更するには？**  
A: プレビュー メソッドを呼び出す前に `options.PreviewFormat = PreviewFormat.Jpeg` を設定します。

**Q: 複数ページを同時にプレビューできますか？**  
A: もちろんです。`options.PageNumbers` にページ番号の配列を割り当てます（例: `new[] {0, 2, 4}`）。

**Q: プレビュー画像がぼやけている場合はどうすればよいですか？**  
A: `options.Width` と `options.Height` を高解像度に増やしてください。ライブラリはそれに応じて画像をスケーリングします。

**Q: Linux コンテナでも動作しますか？**  
A: はい、GroupDocs.Redaction .NET はクロスプラットフォームで、.NET Core をサポートする Docker コンテナ内で動作します。

## リソース
- [ドキュメント](https://docs.groupdocs.com/redaction/net/)  
- [API リファレンス](https://reference.groupdocs.com/redaction/net)  
- [最新バージョンのダウンロード](https://releases.groupdocs.com/redaction/net/)  
- [無料サポートフォーラム](https://forum.groupdocs.com/c/redaction/33)  
- [一時ライセンス取得](https://purchase.groupdocs.com/temporary-license)

---

**最終更新日:** 2026-06-06  
**テスト環境:** GroupDocs.Redaction 5.6 for .NET  
**作者:** GroupDocs

## 関連チュートリアル

- [ドキュメントセキュリティのマスター: GroupDocs.Redaction .NET で Word 文書をラスタライズおよび赤字処理](/redaction/net/rasterization-options/secure-word-docs-rasterize-redact-net/)
- [GroupDocs.Redaction .NET を使用して PDF のページを削除する方法: 包括的ガイド](/redaction/net/page-redaction/delete-pages-pdf-groupdocs-redaction-net/)
- [GroupDocs.Redaction .NET を使用したドキュメント赤字処理の実装: ステップバイステップガイド](/redaction/net/getting-started/implement-document-redaction-groupdocs-redaction-net/)