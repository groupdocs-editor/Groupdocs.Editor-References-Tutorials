---
title: Carregar documento
linktitle: Carregar documento
second_title: API GroupDocs.Editor .NET
description: Aprenda como editar documentos programaticamente com GroupDocs.Editor for .NET. Guia passo a passo para carregar documentos, lidar com arquivos protegidos por senha e muito mais.
weight: 13
url: /pt/net/document-editing/load-document/
---

# Carregar documento

## Introdução
Editar documentos programaticamente pode ser uma tarefa difícil, especialmente se você estiver lidando com diferentes formatos de arquivo e estruturas complexas. Felizmente, o GroupDocs.Editor for .NET facilita essa tarefa, fornecendo uma API robusta e fácil de usar para editar uma ampla variedade de tipos de documentos. Neste tutorial, orientaremos você em tudo o que você precisa para começar a usar o GroupDocs.Editor for .NET, incluindo os pré-requisitos, como importar namespaces e um guia passo a passo detalhado para carregar documentos usando vários métodos.
## Pré-requisitos
Antes de começarmos, certifique-se de ter os seguintes pré-requisitos configurados:
- Visual Studio: certifique-se de ter o Visual Studio instalado em sua máquina.
- .NET Framework: GroupDocs.Editor for .NET oferece suporte a .NET Framework 2.0 ou posterior. Certifique-se de que seu projeto tenha como alvo uma estrutura compatível.
-  GroupDocs.Editor for .NET: Baixe a versão mais recente do[página de download](https://releases.groupdocs.com/editor/net/).
- Conhecimento básico de C#: É necessária familiaridade com programação C# e .NET para acompanhar este tutorial.
## Importar namespaces
Para começar a usar o GroupDocs.Editor for .NET, você precisa importar os namespaces necessários para o seu projeto. Adicione o seguinte usando diretivas na parte superior do seu arquivo C#:
```csharp
using GroupDocs.Editor.Options;
using System.IO;
```
Esses namespaces fornecerão acesso às classes e métodos necessários para tarefas de edição de documentos.
## Etapa 1: carregar o documento de um caminho de arquivo
Carregar um documento a partir de um caminho de arquivo é simples. Este método é ideal para documentos armazenados localmente em sua máquina.

```csharp
string inputPath = "Your Sample Document";
// Carregar documento como arquivo via caminho e sem opções de carregamento
Editor editor1 = new Editor(inputPath);
// Descarte recursos
editor1.Dispose();
System.Console.WriteLine("Document loaded successfully from file path.");
```
## Etapa 2: carregar documento com opções de carregamento
Às vezes, pode ser necessário carregar documentos que requerem tratamento especial, como arquivos protegidos por senha. Nesses casos, você pode usar opções de carregamento.

```csharp
string inputPath = "Your Sample Document";
//Crie opções de carregamento para documentos do Word
WordProcessingLoadOptions wordLoadOptions = new WordProcessingLoadOptions();
wordLoadOptions.Password = "some password";
// Carregar documento como arquivo via caminho e com opções de carregamento
Editor editor2 = new Editor(inputPath, delegate { return wordLoadOptions; });
// Descarte recursos
editor2.Dispose();
System.Console.WriteLine("Password-protected document loaded successfully.");
```
## Etapa 3: carregar o documento de um fluxo de bytes
Carregar um documento de um fluxo de bytes é útil quando você precisa processar documentos que não estão armazenados como arquivos, como aqueles recuperados de um banco de dados ou serviço da web.

```csharp
FileStream inputStream = File.OpenRead("Your Sample Document");
// Carregar documento como conteúdo do fluxo de bytes e sem opções de carregamento
Editor editor3 = new Editor(delegate { return inputStream; });
// Descarte recursos
editor3.Dispose();
System.Console.WriteLine("Document loaded successfully from byte stream.");
```
## Etapa 4: carregar documento com opções de carregamento de um fluxo de bytes
Para documentos que exigem tratamento especial quando carregados a partir de um fluxo de bytes, você pode combinar o carregamento do fluxo de bytes com opções de carregamento.

```csharp
FileStream inputStream = File.OpenRead("Your Sample Document");
// Crie opções de carregamento para planilhas
SpreadsheetLoadOptions sheetLoadOptions = new SpreadsheetLoadOptions();
sheetLoadOptions.OptimizeMemoryUsage = true;
// Carregar documento como conteúdo do fluxo de bytes e com opções de carregamento
Editor editor4 = new Editor(delegate { return inputStream; }, delegate { return sheetLoadOptions; });
// Descarte recursos
editor4.Dispose();
System.Console.WriteLine("Spreadsheet document loaded successfully with load options.");
```
## Conclusão
Parabéns! Você aprendeu como carregar documentos usando GroupDocs.Editor for .NET de várias maneiras. Esteja você lidando com arquivos locais, documentos protegidos por senha ou fluxos de bytes, o GroupDocs.Editor oferece uma solução flexível e poderosa para suas necessidades de edição de documentos. Lembre-se de sempre descartar recursos para garantir desempenho e gerenciamento de recursos ideais em seus aplicativos.
## Perguntas frequentes
### Quais formatos de arquivo são suportados pelo GroupDocs.Editor for .NET?
 GroupDocs.Editor oferece suporte a uma ampla variedade de formatos de arquivo, incluindo DOCX, XLSX, PPTX, HTML e muitos mais. Para obter uma lista completa, consulte o[documentação](https://tutorials.groupdocs.com/editor/net/).
### Como lidar com documentos protegidos por senha?
 Você pode usar opções de carregamento como`WordProcessingLoadOptions` para especificar a senha ao carregar documentos protegidos por senha.
### Posso usar GroupDocs.Editor em um aplicativo da web?
Sim, o GroupDocs.Editor pode ser usado em aplicativos da web. Certifique-se de lidar adequadamente com fluxos de arquivos e descarte de recursos para evitar vazamentos de memória.
### Onde posso obter uma licença temporária para GroupDocs.Editor?
 Você pode obter uma licença temporária do[página de licença temporária](https://purchase.groupdocs.com/temporary-license/).
### Existe suporte disponível se eu encontrar problemas?
 Sim, o GroupDocs fornece suporte por meio de seus[Fórum de suporte](https://forum.groupdocs.com/c/editor/20).