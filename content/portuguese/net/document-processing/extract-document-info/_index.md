---
title: Extrair informações do documento
linktitle: Extrair informações do documento
second_title: API GroupDocs.Editor .NET
description: Aprenda como extrair informações de documentos usando GroupDocs.Editor for .NET com nosso tutorial passo a passo detalhado. Perfeito para gerenciar vários tipos de documentos.
type: docs
weight: 10
url: /pt/net/document-processing/extract-document-info/
---
## Introdução
Bem-vindo a este tutorial abrangente sobre como extrair informações de documentos usando GroupDocs.Editor for .NET. Neste guia, orientaremos você no processo passo a passo, garantindo que você entenda cada parte de forma clara e concisa. Quer você seja um desenvolvedor experiente ou esteja apenas começando, este tutorial o ajudará a integrar perfeitamente o GroupDocs.Editor aos seus projetos .NET para gerenciar e manipular documentos com eficiência.
## Pré-requisitos
Antes de mergulhar no código, vamos garantir que você tenha tudo o que precisa:
- Conhecimento básico de C#: Compreender os fundamentos da programação C# é essencial.
- Visual Studio: certifique-se de ter o Visual Studio instalado.
-  GroupDocs.Editor for .NET: você precisará da biblioteca GroupDocs.Editor for .NET. Você pode baixá-lo no[página de download](https://releases.groupdocs.com/editor/net/).
## Importar namespaces
Para começar, você precisará importar os namespaces necessários. Isso permite acessar as classes e métodos necessários para manipular documentos.
```csharp
using System;
using GroupDocs.Editor.Metadata;
```
## Etapa 1: carregue seu documento
Primeiro, você precisa carregar o documento do qual deseja extrair informações. Isso pode ser feito fornecendo o caminho do arquivo para o documento.
```csharp
string docxInputFilePath = "YourSampleDocument.docx";
Editor editorDocx = new Editor(docxInputFilePath);
```
## Etapa 2: recuperar informações do documento
 A seguir, você recuperará as informações do documento usando o`GetDocumentInfo` método. Este método não requer nenhuma opção de carregamento específica se você não tiver certeza sobre o formato do documento.
```csharp
IDocumentInfo infoDocx = editorDocx.GetDocumentInfo(null);
```
## Etapa 3: determinar o tipo de documento
Agora, você precisa verificar o tipo de documento com o qual está lidando. Isso é crucial porque determina como você lidará com o documento.
```csharp
bool isSpreadsheet = infoDocx is SpreadsheetDocumentInfo;
bool isText = infoDocx is TextualDocumentInfo;
bool isWordProcessing = infoDocx is WordProcessingDocumentInfo;
Console.WriteLine($"Is '{docxInputFilePath}' a Spreadsheet: {isSpreadsheet}");
Console.WriteLine($"Is '{docxInputFilePath}' a Textual document: {isText}");
Console.WriteLine($"Is '{docxInputFilePath}' a WordProcessing document: {isWordProcessing}");
```
## Etapa 4: extrair informações detalhadas
Se o documento for um documento de processamento de texto, você poderá extrair informações detalhadas, como formato, extensão, contagem de páginas, tamanho e se está criptografado.
```csharp
if (isWordProcessing)
{
    WordProcessingDocumentInfo casted = (WordProcessingDocumentInfo)infoDocx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Page count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```
## Etapa 5: Repita para diferentes tipos de documentos
Repita as mesmas etapas para outros tipos de documentos, como planilhas e documentos textuais.
```csharp
string xlsxInputFilePath = "YourSampleDocument.xlsx";
Editor editorXlsx = new Editor(xlsxInputFilePath);
IDocumentInfo infoXlsx = editorXlsx.GetDocumentInfo(null);
bool isXlsxSpreadsheet = infoXlsx is SpreadsheetDocumentInfo;
Console.WriteLine($"Is '{xlsxInputFilePath}' a Spreadsheet: {isXlsxSpreadsheet}");
if (isXlsxSpreadsheet)
{
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo)infoXlsx;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Tabs count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```
## Etapa 6: lidar com documentos protegidos por senha
Ao lidar com documentos protegidos por senha, você deve primeiro tentar abri-los sem senha, depois com a senha incorreta e, por fim, com a senha correta.
```csharp
string xlsInputFilePath = "YourSampleDocument.xls";
Editor editorXls = new Editor(xlsInputFilePath);
try
{
    IDocumentInfo infoXls = editorXls.GetDocumentInfo(null);
}
catch (PasswordRequiredException)
{
    Console.WriteLine("This document is password-protected.");
}
try
{
    IDocumentInfo infoXls = editorXls.GetDocumentInfo("incorrect_password");
}
catch (IncorrectPasswordException)
{
    Console.WriteLine("The provided password is incorrect.");
}
IDocumentInfo infoXlsValid = editorXls.GetDocumentInfo("correct_password");
bool isXlsSpreadsheet = infoXlsValid is SpreadsheetDocumentInfo;
Console.WriteLine($"Password-protected document is a Spreadsheet: {isXlsSpreadsheet}");
if (isXlsSpreadsheet)
{
    SpreadsheetDocumentInfo casted = (SpreadsheetDocumentInfo)infoXlsValid;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Tabs count: {casted.PageCount}; Size: {casted.Size} bytes; Is encrypted: {casted.IsEncrypted}");
}
```
## Etapa 7: lidar com documentos baseados em texto
```csharp
string xmlInputFilePath = "YourSampleDocument.xml";
Editor editorXml = new Editor(xmlInputFilePath);
IDocumentInfo infoXml = editorXml.GetDocumentInfo(null);
bool isXmlText = infoXml is TextualDocumentInfo;
Console.WriteLine($"Is '{xmlInputFilePath}' a Textual document: {isXmlText}");
if (isXmlText)
{
    TextualDocumentInfo casted = (TextualDocumentInfo)infoXml;
    Console.WriteLine($"Format: {casted.Format.Name}; Extension: {casted.Format.Extension}; Encoding: {casted.Encoding}; Size: {casted.Size} bytes");
}
```
## Etapa 8: descartar recursos
Por fim, certifique-se de descartar todos os recursos para evitar vazamentos de memória.
```csharp
editorDocx.Dispose();
editorXlsx.Dispose();
editorXls.Dispose();
editorXml.Dispose();
Console.WriteLine("ExtractingDocumentInfo routine has successfully finished");
```
## Conclusão
Parabéns! Agora você aprendeu como extrair informações de documentos usando GroupDocs.Editor for .NET. Esta poderosa biblioteca simplifica o gerenciamento e a manipulação de documentos, permitindo lidar perfeitamente com vários tipos de documentos. Esteja você lidando com documentos de processamento de texto, planilhas ou baseados em texto, o GroupDocs.Editor oferece uma solução robusta.
## Perguntas frequentes
### Que tipos de documentos o GroupDocs.Editor pode manipular?
GroupDocs.Editor pode lidar com vários tipos de documentos, incluindo processamento de texto, planilhas e documentos baseados em texto.
### O GroupDocs.Editor pode gerenciar documentos protegidos por senha?
Sim, o GroupDocs.Editor pode gerenciar documentos protegidos por senha. Ele pode identificar e abrir esses documentos com a senha correta.
### É necessário descartar os objetos do Editor?
Sim, é crucial descartar objetos Editor para liberar recursos e evitar vazamentos de memória.
### Posso extrair informações detalhadas sobre o formato e tamanho do documento?
Absolutamente! GroupDocs.Editor permite extrair informações detalhadas, incluindo formato, extensão, tamanho, contagem de páginas e status de criptografia.
### Onde posso obter suporte se encontrar problemas?
 Você pode obter suporte do[Fórum de suporte do GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).