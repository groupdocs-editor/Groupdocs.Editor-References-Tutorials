---
title: フォームフィールドコレクションを削除する
linktitle: フォームフィールドコレクションを削除する
second_title: GroupDocs.Editor .NET API
description: このステップバイステップ ガイドでは、GroupDocs.Editor for .NET を使用して Word 文書からフォーム フィールドを削除する方法を学習します。開発者に最適です。
type: docs
weight: 13
url: /ja/net/form-field-management/remove-form-field-collection/
---
## 導入
ドキュメント内のフォーム フィールドをプログラムで管理したいとお考えですか? GroupDocs.Editor for .NET は、さまざまなドキュメント形式のフォーム フィールドを処理および操作するための強力なソリューションを提供します。このチュートリアルでは、この強力なライブラリを使用して Word ドキュメントからフォーム フィールド コレクションを削除する手順を説明します。 
## 前提条件
コードに進む前に、スムーズなエクスペリエンスのためにすべてが設定されていることを確認しましょう。
1. GroupDocs.Editor for .NET: GroupDocs.Editor for .NETをダウンロードしてインストールしたことを確認してください。まだの場合は、ダウンロードできます。[ここ](https://releases.groupdocs.com/editor/net/).
2. 開発環境: Visual Studio などの開発環境が必要です。
3. .NET Framework: マシンに .NET Framework がインストールされていることを確認します。
4. サンプル文書: サンプルのWord文書（例：`SampleLegacyFormFields.docx`) を、操作するフォーム フィールドと関連付けます。

## 名前空間のインポート
開始するには、.NET プロジェクトに必要な名前空間をインポートする必要があります。これにより、GroupDocs.Editor の機能にアクセスできるようになります。
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System.IO;
```
## ステップ1: ドキュメントを読み込む
まず、編集したいドキュメントを読み込む必要があります。詳しく見ていきましょう。
### ステップ 1.1: 入力ファイルへのパスを取得する
入力ファイルへのパスを指定する必要があります。この例では、サンプルファイルを使用します。`SampleLegacyFormFields.docx`.
```csharp
string inputFilePath = "path/to/SampleLegacyFormFields.docx";
```
### ステップ 1.2: パスから FileStream を作成する
次に、`FileStream`文書を読む。
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
{
    //この using ブロック内の次の手順に進みます。
}
```
## ステップ2: 読み込みオプションを設定する
ドキュメントを読み込むときに、特にドキュメントがパスワードで保護されている場合は、読み込みオプションを指定する必要がある場合があります。
### ステップ 2.1: ロード オプションを作成する
インスタンスを作成する`WordProcessingLoadOptions`.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
```
### ステップ 2.2: パスワードを指定する (必要な場合)
ドキュメントがパスワードで保護されている場合は、パスワードを指定できます。
```csharp
loadOptions.Password = "some_password_to_open_a_document";
```
## ステップ3: ドキュメントをエディターに読み込む
次に、ドキュメントを`Editor`インスタンスを使用して`FileStream`そして`LoadOptions`.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
{
    //この using ブロック内の次の手順に進みます。
}
```
## ステップ4: フォームフィールドにアクセスして管理する
ドキュメントが読み込まれると、フォーム フィールドにアクセスして操作できるようになります。
### ステップ4.1: FormFieldManagerの読み取り
取得する`FormFieldManager`から`Editor`実例。
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
### ステップ 4.2: FormFieldCollection にアクセスする
入手`FormFieldCollection`ドキュメント内のすべてのフォーム フィールドが含まれます。
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
### ステップ4.3: 特定のテキストフォームフィールドを削除する
特定のテキスト フォーム フィールドを削除するには、そのフィールドを名前で検索して削除します。
```csharp
TextFormField textField = collection.GetFormField<TextFormField>("Text1");
fieldManager.RemoveFormFiled(textField);
```
### ステップ4.4: 複数のフォームフィールドを削除する
名前を指定して複数のフォーム フィールドを一度に削除することもできます。
```csharp
textField = collection.GetFormField<TextFormField>("Text7");
CheckBoxForm checkBoxForm = collection.GetFormField<CheckBoxForm>("Check2");
fieldManager.RemoveFormFields(new IFormField[] { textField, checkBoxForm });
```
## ステップ5: 変更したドキュメントを保存する
フォーム フィールドを変更したら、ドキュメントを保存する必要があります。
### ステップ5.1: 保存オプションを作成する
出力ドキュメントの形式と保存オプションを指定します。
```csharp
WordProcessingFormats docFormat = WordProcessingFormats.Docx;
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(docFormat);
```
### ステップ5.2: メモリ使用量を最適化する
大きなドキュメントを扱う場合は、メモリ使用量を最適化することをお勧めします。
```csharp
saveOptions.OptimizeMemoryUsage = true;
```
### ステップ 5.3: 保護を設定する (必要な場合)
書き込みパスワードを設定することで、ドキュメントをそれ以上編集できないように保護できます。
```csharp
saveOptions.Protection = new WordProcessingProtection(WordProcessingProtectionType.AllowOnlyFormFields, "write_password");
```
### ステップ5.4: ドキュメントを保存する
最後に、`MemoryStream`.
```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    editor.Save(outputStream, saveOptions);
}
```

## 結論
おめでとうございます! GroupDocs.Editor for .NET を使用して、Word 文書からフォーム フィールドを正常に削除できました。この強力なライブラリを使用すると、プログラムで文書の内容を簡単に操作できるため、時間と労力を節約できます。
## よくある質問
### GroupDocs.Editor for .NET を他のドキュメント形式で使用できますか?
はい、GroupDocs.Editor for .NET は、PDF、HTML など、さまざまなドキュメント形式をサポートしています。
### GroupDocs.Editor for .NET を使用してフォーム フィールドを追加することは可能ですか?
はい、プログラムでフォーム フィールドを追加、変更、削除できます。
### ドキュメントが非常に大きい場合はどうなりますか?
保存オプションでメモリ最適化を有効にすると、大きなドキュメントを効率的に処理できます。
### GroupDocs.Editor for .NET を Web アプリケーションで使用できますか?
もちろんです! GroupDocs.Editor for .NET は、サーバー側でのドキュメント処理のために Web アプリケーションに統合できます。
### 問題が発生した場合、どこでサポートを受けることができますか?
訪問することができます[サポートフォーラム](https://forum.groupdocs.com/c/editor/20)問題が発生した場合のサポートについては、