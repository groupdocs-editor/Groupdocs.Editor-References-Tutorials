---
date: '2026-04-11'
description: GroupDocs.Editor for .NET を使用して編集可能なドキュメントを作成し、効率的に HTML として保存する方法を学びましょう。
keywords:
- create editable document
- extract images from document
- save document as html
title: GroupDocs.Editor .NETで編集可能なドキュメントを作成する
type: docs
url: /ja/net/document-editing/groupdocs-editor-net-edit-manage-documents-guide/
weight: 1
---

# GroupDocs.Editor .NETで編集可能なドキュメントを作成する

今日のデジタル時代において、**編集可能なドキュメントの作成**は、あらゆるモダンなワークフローの重要な要件です。コラボレーティブエディタ、コンテンツ管理システム、または自動レポートツールを構築する場合でも、HTMLファイルをプログラムで編集・保存できることは膨大な時間を節約できます。このチュートリアルでは、**編集可能なドキュメント**インスタンスの作成方法、リソースの抽出方法、そしてGroupDocs.Editor for .NETを使用した**ドキュメントをHTMLとして保存**方法を示します。

## クイック回答
- **「編集可能なドキュメントの作成」とは何ですか？** それは、ソースファイルを GroupDocs.Editor の `EditableDocument` オブジェクトにロードし、プログラムで変更できるようにすることを意味します。  
- **HTMLに変換できるフォーマットは何ですか？** Word、Excel、PowerPoint、その他多数の Office フォーマットがサポートされています。  
- **ドキュメントから画像を抽出するには？** `EditableDocument.Images` コレクションを使用します。  
- **すべてのリソースを埋め込んだ単一のHTML文字列を生成できますか？** はい、`GetEmbeddedHtml()` を呼び出します。  
- **本番環境でライセンスが必要ですか？** 評価にはトライアルで動作しますが、商用利用には永続ライセンスが必要です。

## 「編集可能なドキュメントの作成」とは何か
編集可能なドキュメントを作成するとは、ソースファイル（例: .docx）を GroupDocs.Editor に読み込み、`EditableDocument` オブジェクトを取得することです。このオブジェクトはドキュメントのHTMLマークアップ、画像、フォント、CSS を公開し、コンテンツの編集、リソースの置換、またはウェブページへの埋め込みが可能になります。

## このタスクにGroupDocs.Editor .NETを使用する理由
- **フル機能API** – Word、Excel、PowerPoint などを処理します。  
- **リソース抽出** – 簡単なプロパティで画像、フォント、スタイルシートを取得します。  
- **埋め込みHTML生成** – すべてのリソースを含む単一のHTML文字列を生成し、メールやシングルページアプリに最適です。  
- **パフォーマンス重視** – 必要に応じてオブジェクトを速やかに破棄し、非同期パターンを使用します。

## 前提条件
Before implementing GroupDocs.Editor .NET features, ensure:
- **.NET 環境**: .NET アプリケーション用の開発環境を設定します。
- **ライブラリと依存関係**:
  - 以下の方法のいずれかで GroupDocs.Editor をインストールします:
    - **.NET CLI**
      ```bash
      dotnet add package GroupDocs.Editor
      ```
    - **Package Manager**
      ```powershell
      Install-Package GroupDocs.Editor
      ```
    - **NuGet Package Manager UI**: 最新バージョンを検索してインストールします。
- **知識の前提条件**: C# プログラミングと基本的なドキュメント処理の概念に慣れていることが推奨されます。

## .NET 用 GroupDocs.Editor の設定
### インストール手順
まず、プロジェクトに GroupDocs.Editor を設定します:
1. **.NET CLI でインストール**:
   ```bash
   dotnet add package GroupDocs.Editor
   ```
2. **Package Manager を使用**:
   - Package Manager コンソールを開き、以下を実行します:
     ```powershell
     Install-Package GroupDocs.Editor
     ```
3. **NuGet Package Manager UI**:
   - NuGet に移動し、"GroupDocs.Editor" を検索してインストールします。

### ライセンス取得
- **無料トライアル＆一時ライセンス**:
  [GroupDocs releases](https://releases.groupdocs.com/editor/net/) からダウンロードして無料トライアルを開始します。拡張テストには、[purchase page](https://purchase.groupdocs.com/temporary-license) で一時ライセンスを申請してください。

### 基本的な初期化と設定
アプリケーションで GroupDocs.Editor を初期化する方法は次のとおりです:
```csharp
using System;
using GroupDocs.Editor;

string inputFilePath = "YOUR_DOCUMENT_DIRECTORY"; // Replace with your actual document path
Editor editor = new Editor(inputFilePath, new WordProcessingLoadOptions());
```

## GroupDocs.Editor .NETで編集可能なドキュメントを作成する方法
### EditableDocument インスタンスの作成
**概要**: `EditableDocument` インスタンスを作成してドキュメントをロードおよび編集します。

#### ドキュメントのロード
```csharp
using GroupDocs.Editor.Options;

// Load your document with appropriate options
Editor editor = new Editor(inputFilePath, new WordProcessingLoadOptions());

// Create EditableDocument from the loaded file
EditableDocument beforeEdit = editor.Edit(new WordProcessingEditOptions());
```

## 埋め込みHTMLを生成する方法
### EditableDocument から埋め込みHTMLを生成する
**概要**: ドキュメント全体をスタイルシートとリソースを含む単一の埋め込みHTML文字列に変換します。
```csharp
using System.Collections.Generic;
using GroupDocs.Editor.HtmlCss.Resources;

// Generate embedded HTML
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```

## ドキュメントから画像を抽出する方法
### EditableDocument からリソースを抽出する
**概要**: ドキュメントから画像、フォント、CSS、その他のリソースを取得します。
```csharp
List<IImageResource> allImages = beforeEdit.Images;
List<FontResourceBase> allFonts = beforeEdit.Fonts;
List<CssText> allStylesheets = beforeEdit.Css;
List<IHtmlResource> allResources = beforeEdit.AllResources;
```

## ドキュメントからフォントを抽出する方法
*上記のコードブロックは、`beforeEdit.Fonts` を使用してフォントリソースを取得する方法も示しています。*

## 純粋なHTMLコンテンツを取得する方法
### EditableDocument からHTMLコンテンツを取得する
**概要**: 埋め込みリソースなしで純粋なHTMLコンテンツを抽出します。
```csharp
string htmlMarkup = beforeEdit.GetContent();
```

## HTMLコンテンツの外部リンクを調整する方法
### HTMLコンテンツの外部リンクを調整する
**概要**: カスタムプレフィックスを使用して画像、CSS、フォントの外部リンクを変更します。
```csharp
using System.Collections.Generic;

// Define custom handlers for resource URLs
string customImagesRequesthandlerUri = "http://example.com/ImagesHandler/id=";
string customCssRequesthandlerUri = "http://example.com/CssHandler/id=";

// Adjust HTML content with prefixed links
string prefixedHtmlMarkup = beforeEdit.GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri);
```

## ドキュメントをHTMLとして保存する方法
### EditableDocument をHTMLファイルとして保存する
**概要**: 編集したドキュメントをHTML形式でディスクに保存します。
```csharp
using System.IO;

string htmlFilePath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "document.html"); // Adjust the output path
beforeEdit.Save(htmlFilePath);
```

## EditableDocument の破棄とイベントハンドリング
**概要**: リソースの破棄を管理し、ドキュメントのライフサイクルに関連するイベントを処理します。
```csharp
Console.WriteLine("beforeEdit variable of EditableDocument type is {0} disposed", !beforeEdit.IsDisposed ? "not" : "already");

// Subscribe to the disposing event
EventHandler someMethod = delegate {
    Console.WriteLine("Disposing event was spotted!");
};
beforeEdit.Disposed += someMethod;
```

## HTMLコンテンツから編集可能なドキュメントを作成する方法
### HTMLコンテンツから EditableDocument を作成する
**概要**: 既存のHTMLコンテンツから `EditableDocument` インスタンスを再構築します。
```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);

// Dispose resources once done
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```

## 実用的な応用例
GroupDocs.Editor .NET は多くの実際のシナリオで活用できます:
- **Collaborative Editing**: 複数ユーザーによるシームレスなドキュメント編集を実現します。  
- **Web Publishing**: ドキュメントをウェブ向けフォーマットに変換し、オンライン閲覧やインタラクションを可能にします。  
- **Content Management Systems**: CMS プラットフォームと統合し、動的なコンテンツ更新を可能にします。  
- **Automated Report Generation**: さまざまなデータソースからレポート生成とフォーマットを自動化します。

## パフォーマンス上の考慮点
GroupDocs.Editor .NET のパフォーマンスを最適化するには:
- 使用後すぐにオブジェクトを破棄してメモリを効率的に管理します。  
- ファイルパスや URL を最適化してリソース読み込み時間を最小化します。  
- 適用可能な場合は非同期処理を使用し、アプリケーションの応答性を向上させます。

## よくある問題と解決策
- **大きなファイルはメモリ使用量が増加します** – 処理が完了したらすぐに `EditableDocument` オブジェクトを破棄します。  
- **変換後に画像リンクが切れる** – `GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri)` を呼び出す際に正しいリソースハンドラ URI を使用していることを確認します。  
- **生成されたHTMLにフォントが欠落しています** – ソースドキュメントが必要なフォントを埋め込んでいるか、サーバー上にフォントが存在するかを確認します。

## よくある質問

**Q: GroupDocs.Editor .NET はすべてのドキュメント形式に対応していますか？**  
A: GroupDocs.Editor は Word、Excel、PowerPoint など多数の形式をサポートしており、さまざまなユースケースで柔軟に利用できます。

**Q: GroupDocs.Editor を使用して大きなファイルを効率的に処理するには？**  
A: 利用可能な非同期 API を使用し、可能な場合はファイルをチャンクで処理し、常に `EditableDocument` と `Editor` オブジェクトを速やかに破棄してメモリを解放します。

**Q: GroupDocs.Editor をクラウドストレージソリューションと統合できますか？**  
A: はい、ファイルストリームを `Editor` コンストラクタに渡すことで、Azure Blob Storage、Amazon S3、Google Cloud Storage、その他任意のクラウドプロバイダーに接続できます。

**Q: GroupDocs.Editor のライセンスオプションは何ですか？**  
A: 無料トライアルで開始するか、評価用に一時ライセンスを申請できます。本番環境での導入には有料ライセンスが必要です。

**Q: 問題が発生した場合、どこでサポートを受けられますか？**  
A: [GroupDocs Support Forum](https://forum.groupdocs.com) で支援を受けられ、また直接 GroupDocs サポートチームに問い合わせることもできます。

---

**最終更新日:** 2026-04-11  
**テスト環境:** GroupDocs.Editor 23.12 for .NET  
**作者:** GroupDocs  

---