---
title: 従量制ライセンスの設定
linktitle: 従量制ライセンスの設定
second_title: GroupDocs.Editor .NET API
description: 包括的なガイドを使用して、GroupDocs.Editor for .NET を統合して使用する方法を学習します。.NET アプリケーション内で強力なドキュメント編集機能を活用できます。
weight: 12
url: /ja/net/quick-start-guide/set-metered-license/
---

# 従量制ライセンスの設定

## 導入
GroupDocs.Editor for .NET の使用に関するステップバイステップ ガイドへようこそ。熟練した開発者でも、初心者でも、このチュートリアルは、この強力なライブラリの潜在能力を最大限に活用するのに役立ちます。GroupDocs.Editor for .NET を使用すると、.NET アプリケーション内でさまざまな形式のドキュメントを簡単に編集できます。この強力なツールを使い始める方法を詳しく見ていきましょう。
## 前提条件
技術的な詳細に入る前に、次の前提条件を満たしていることを確認してください。
- .NET プログラミングの基礎知識: C# および .NET Framework に精通していること。
- Visual Studio がインストールされている: マシンに最新バージョンの Visual Studio がインストールされていることを確認します。
-  GroupDocs.Editor for .NET: ライブラリを以下からダウンロードしてください。[ダウンロードページ](https://releases.groupdocs.com/editor/net/).
- 有効なライセンス：一時ライセンスまたはフルライセンスを[GroupDocs 購入ページ](https://purchase.groupdocs.com/temporary-license/).
## 名前空間のインポート
GroupDocs.Editor for .NET を使用するには、プロジェクトに必要な名前空間をインポートする必要があります。この手順は、ライブラリの機能を利用するためにプロジェクトを設定するため、非常に重要です。
```csharp
using System;
using GroupDocs.Editor;
```
簡単に理解できるように、各例を複数のステップに分解してみましょう。
## ステップ 1: GroupDocs.Editor for .NET をインストールする
まず最初に、プロジェクトに GroupDocs.Editor for .NET をインストールする必要があります。これは、Visual Studio の NuGet パッケージ マネージャーを使用して実行できます。
### NuGet パッケージ マネージャー経由でインストールする
1. Visual Studio でプロジェクトを開きます。
2. へ移動`Tools`>`NuGet Package Manager`>`Manage NuGet Packages for Solution`.
3. 検索する`GroupDocs.Editor`.
4. クリック`Install`.
これにより、プロジェクトに必要な参照が追加されます。
## ステップ2: 従量制ライセンスを設定する
GroupDocs.Editor の全機能を利用するには、従量制ライセンスを設定する必要があります。これにより、API を制限なく使用できるようになります。
### 従量制ライセンスの設定
1. 公開鍵と秘密鍵を以下から入手してください。[GroupDocs 購入ページ](https://purchase.groupdocs.com/temporary-license/).
2. 従量制ライセンスを設定するには、プロジェクトに次のコードを追加します。
```csharp
string publicKey = "*****";
string privateKey = "*****";
Metered metered = new Metered();
metered.SetMeteredKey(publicKey, privateKey);
Console.WriteLine("License set successfully.");
```
## ステップ3: ドキュメントを読み込んで編集する
プロジェクトの設定とライセンス取得が完了したら、ドキュメントの読み込みと編集に移りましょう。
### ドキュメントの読み込み
1. ドキュメントを読み込むには、次のコードを追加します。
```csharp
string filePath = "sample.docx";
Editor editor = new Editor(filePath);
Console.WriteLine("Document loaded successfully.");
```
### ドキュメントの編集
2. ドキュメントを編集するには、編集可能な形式に変換する必要があります。
```csharp
EditableDocument editableDocument = editor.Edit();
string content = editableDocument.GetContent();
Console.WriteLine("Document converted to editable format.");
```
## ステップ4: 編集したドキュメントを保存する
ドキュメントを編集したら、最後の手順として変更を保存します。
### ドキュメントを保存する
1. 編集したコンテンツを元の形式に戻します。
```csharp
string updatedContent = "<html><body>Updated content</body></html>";
editableDocument = EditableDocument.FromMarkup(updatedContent, new WordProcessingSaveOptions());
editor.Save(editableDocument, "updated_sample.docx");
Console.WriteLine("Document saved successfully.");
```
## 結論
おめでとうございます。GroupDocs.Editor for .NET をアプリケーションに統合して使用できました。ライブラリのインストールから従量制ライセンスの設定、ドキュメントの編集まで、重要な手順をすべて網羅しました。この強力なツールにより、.NET アプリケーション内でのドキュメント編集ワークフローが大幅に効率化されます。詳細については、[.NET ドキュメント用の GroupDocs.Editor](https://tutorials.groupdocs.com/editor/net/).
## よくある質問
### GroupDocs.Editor ライセンスを取得するにはどうすればよいですか?
ライセンスは、[GroupDocs 購入ページ](https://purchase.groupdocs.com/buy)一時ライセンスについては、[ここ](https://purchase.groupdocs.com/temporary-license/).
### GroupDocs.Editor を無料で試すことはできますか?
はい、無料トライアルは以下からダウンロードできます。[ダウンロードページ](https://releases.groupdocs.com/)一時ライセンスを申請します。
### GroupDocs.Editor ではどのようなドキュメント形式がサポートされていますか?
 GroupDocs.EditorはDOCX、PPTX、XLSX、TXT、HTMLなど、さまざまな形式をサポートしています。完全なリストについては、[ドキュメンテーション](https://tutorials.groupdocs.com/editor/net/).
### GroupDocs.Editor にはコミュニティ サポートがありますか?
はい、コミュニティのサポートを受けることができます[GroupDocs.Editor フォーラム](https://forum.groupdocs.com/c/editor/20).
### GroupDocs.Editor for .NET を使い始めるにはどうすればよいですか?
ライブラリの設定、ライセンスの取得、ドキュメントの編集を開始するには、ステップバイステップのガイドに従ってください。詳細な手順については、[ドキュメンテーション](https://tutorials.groupdocs.com/editor/net/).