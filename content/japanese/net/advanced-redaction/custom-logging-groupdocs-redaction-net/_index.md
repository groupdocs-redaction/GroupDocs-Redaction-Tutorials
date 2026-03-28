---
date: '2026-03-28'
description: GroupDocs.Redaction for .NETでカスタムロガー（C#）を実装する方法を学び、詳細なカスタムロギングとコンプライアンスレポートの作成を容易にします。
keywords:
- custom logger c#
- custom logging .net
- save redacted document
- log warnings c#
title: .NET 用 GroupDocs.Redaction でカスタムロガー C# を実装する
type: docs
url: /ja/net/advanced-redaction/custom-logging-groupdocs-redaction-net/
weight: 1
---

# GroupDocs.Redaction for .NET でカスタムロガー C# を実装する

文書の赤字処理を効率的に管理することは重要です、特に機密情報を扱う場合はなおさらです。このガイドでは、GroupDocs.Redaction for .NET を使用して **カスタムロガー C# の実装方法** を学び、ロギング、エラーハンドリング、監査トレイルを完全に制御できるようにします。

## クイック回答
- **カスタムロガー C# は何をしますか？** 赤字処理中にエラー、警告、情報メッセージをキャプチャします。  
- **ILogger インターフェイスを提供するライブラリはどれですか？** GroupDocs.Redaction for .NET。  
- **ラスタライズせずに赤字処理された文書を保存できますか？** はい – `redactor.Save(..., new Options.RasterizationOptions { Enabled = false })` を使用します。  
- **本番環境で使用するにはライセンスが必要ですか？** 本番環境ではフルライセンスが必要です。評価用にトライアルが利用可能です。  
- **このアプローチは .NET Core / .NET 6+ と互換性がありますか？** もちろんです – 同じ API が .NET Framework と .NET Core/5/6 で動作します。

## カスタムロガー C# とは？
**カスタムロガー C#** は、GroupDocs.Redaction が提供する `ILogger` インターフェイスを実装したクラスです。コンソール、ファイル、データベース、外部監視システムなど、必要な場所へログメッセージをルーティングでき、赤字処理ワークフローを明確に把握できます。

## GroupDocs.Redaction でカスタムロギング .NET を使用する理由
- **コンプライアンスと監査:** 詳細なログは規制要件を満たします。  
- **エラーの可視性:** `LogError` と `LogWarning` は問題に対する即時フィードバックを提供します。  
- **統合の柔軟性:** 既存の .NET ロギングフレームワーク（Serilog、NLog など）へログを転送できます。  

## 前提条件
- **GroupDocs.Redaction for .NET** がインストールされていること（下記インストール手順を参照）。  
- .NET 開発環境（Visual Studio、VS Code、または CLI）。  
- 基本的な C# の知識とファイルストリームの理解。  

## インストール

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**パッケージマネージャー**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet パッケージマネージャー UI**  
**"GroupDocs.Redaction"** を検索し、最新バージョンをインストールしてください。

## ライセンス取得
- **無料トライアル:** 一時的なライセンスで API をテストします。  
- **一時ライセンス:** 限定期間でフル機能にアクセスできます。  
- **購入:** 本番展開用の永続ライセンスを取得します。  

## ステップバイステップガイド

### 手順 1: カスタムロガークラスを定義する（警告ログ C#）
`ILogger` を実装するクラスを作成します。このクラスはエラー、警告、情報メッセージをキャプチャします。

```csharp
using System;
using GroupDocs.Redaction;

class CustomLogger : ILogger
{
    public bool HasErrors { get; private set; }

    // Log errors encountered during processing.
    public void LogError(string message)
    {
        Console.WriteLine("Error: " + message);
        HasErrors = true;
    }

    // Log warnings that may not be critical but need attention.
    public void LogWarning(string message)
    {
        Console.WriteLine("Warning: " + message);
    }

    // Log informational messages for tracking normal operations.
    public void LogInfo(string message)
    {
        Console.WriteLine("Info: " + message);
    }
}
```

**説明:** `HasErrors` フラグは処理を継続するかどうかの判断に役立ちます。3 つのメソッドは、ほとんどの赤字処理シナリオで必要となる 3 つのログレベルに対応しています。

### 手順 2: ファイルパスを準備し、ソース文書を開く
```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
string outputFile = Utils.GetOutputFile(sourceFile);
```

**重要性:** ユーティリティメソッドを使用するとコードが整理され、**赤字処理された文書を保存**する前に出力フォルダーが存在することが保証されます。

### 手順 3: カスタムロガーを使用して赤字処理を適用する
```csharp
using (Stream stream = File.Open(sourceFile, FileMode.Open, FileAccess.ReadWrite))
{
    var logger = new CustomLogger();
    
    using (Redactor redactor = new Redactor(stream, new LoadOptions(), new RedactorSettings(logger)))
    {
        // Apply a redaction to the document.
        redactor.Apply(new DeleteAnnotationRedaction());
        
        if (!logger.HasErrors)
        {
            using (Stream streamOut = File.Open(outputFile, FileMode.OpenOrCreate, FileAccess.ReadWrite))
            {
                // Save changes without rasterizing the output.
                redactor.Save(streamOut, new Options.RasterizationOptions { Enabled = false });
            }
        }
    }
}
```

**説明:**  
1. `Redactor` は `RedactorSettings(logger)` でインスタンス化され、`CustomLogger` と連携します。  
2. 赤字処理を適用した後、コードは `logger.HasErrors` をチェックします。エラーがなければ文書が保存され、ラスタライズなしで **赤字処理された文書を保存** するロジックを示しています。

### 一般的な落とし穴とトラブルシューティング
- **ログ出力がない:** 各 `Log*` メソッドが正しくオーバーライドされているか確認してください。  
- **ファイルアクセス例外:** アプリケーションがソースと出力パスの両方に対して読み取り/書き込み権限を持っていることを確認してください。  
- **ロガーが接続されていない:** `RedactorSettings(logger)` パラメータは必須です。省略するとカスタムロギングが無効になります。

## 実用的な応用例
1. **コンプライアンスレポート:** ログエントリを CSV またはデータベースにエクスポートして監査トレイルを作成します。  
2. **エラートラッキング:** `LogError` 出力をスキャンして問題のあるファイルを迅速に特定します。  
3. **ワークフロー自動化:** `LogWarning` が呼び出されたときに、下流プロセス（例: コンプライアンス担当者への通知）をトリガーします。

## パフォーマンス上の考慮点
- **ストリームを速やかに破棄** してメモリを解放します。特に大量バッチ処理時に重要です。  
- **CPU とメモリを監視** しながら大量の赤字処理を行います。ロガーの同期に注意しつつ、並列処理を検討してください。  
- **最新情報を入手:** GroupDocs.Redaction の新しいバージョンは、パフォーマンス最適化や追加のロギングフックが含まれることが多いです。

## 結論
**カスタムロガー C#** を実装することで、赤字処理パイプラインの各ステップを細かく把握でき、コンプライアンス基準の遵守や問題のデバッグが容易になります。このアプローチは GroupDocs.Redaction for .NET とシームレスに連携し、既存の任意の .NET ロギングフレームワークと統合するよう拡張可能です。

---

## よくある質問

**Q: GroupDocs.Redaction でカスタムロギングを行う目的は何ですか？**  
A: カスタムロギングは、コンプライアンス、エラートラッキング、ワークフロー最適化のために赤字処理を追跡・管理するのに役立ちます。

**Q: カスタムロガーでエラーを処理するにはどうすればよいですか？**  
A: `CustomLogger` クラスで `LogError` を実装します。`HasErrors` フラグにより、必要に応じて処理を中止できます。

**Q: カスタムロギングを他のシステムと統合できますか？**  
A: はい、ロガーメソッドを拡張することで、CRM、ERP、または集中監視ツールにログメッセージを転送できます。

**Q: カスタムロギング実装時の一般的な落とし穴は何ですか？**  
A: メソッド実装の誤り、`RedactorSettings(logger)` の欠如、ファイル権限の問題が最も頻繁に発生します。

**Q: カスタムロギングは文書の赤字処理ワークフローをどのように改善しますか？**  
A: 詳細なログはリアルタイムの可視性を提供し、トラブルシューティングを簡素化し、監査要件を満たします。

## リソース
- **ドキュメンテーション:** [GroupDocs.Redaction .NET Documentation](https://docs.groupdocs.com/redaction/net/)  
- **API リファレンス:** [GroupDocs.Redaction API Reference](https://reference.groupdocs.com/redaction/net)  
- **ダウンロード:** [GroupDocs.Redaction for .NET](https://downloads.groupdocs.com/redaction/net)  

---

**最終更新日:** 2026-03-28  
**テスト環境:** GroupDocs.Redaction 23.11 for .NET  
**作者:** GroupDocs  

---