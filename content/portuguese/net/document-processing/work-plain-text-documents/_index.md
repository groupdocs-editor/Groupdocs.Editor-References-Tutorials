---
title: Trabalhe com documentos de texto simples
linktitle: Trabalhe com documentos de texto simples
second_title: API GroupDocs.Editor .NET
description: Aprenda a editar documentos de texto simples usando GroupDocs.Editor for .NET com nosso guia passo a passo. Simplifique seu processo de edição de documentos .NET.
weight: 15
url: /pt/net/document-processing/work-plain-text-documents/
type: docs
---
# Trabalhe com documentos de texto simples

## Introdução
Você deseja agilizar seu processo de edição de documentos em .NET? Não procure mais, GroupDocs.Editor para .NET! Esta API poderosa permite editar uma ampla variedade de formatos de documentos com facilidade. Neste tutorial, orientaremos você no processo de trabalho com documentos de texto simples usando GroupDocs.Editor for .NET. Ao final, você estará preparado para lidar com a edição de documentos de texto como um profissional. Pronto para mergulhar? Vamos começar!
## Pré-requisitos
Antes de começarmos, há algumas coisas que você precisa ter em mente:
- Ambiente de desenvolvimento .NET: certifique-se de ter um ambiente de desenvolvimento .NET funcional configurado. Visual Studio é uma escolha popular.
-  GroupDocs.Editor para .NET: Baixe e instale o[GroupDocs.Editor para .NET](https://releases.groupdocs.com/editor/net/).
- Conhecimento básico de C#: A familiaridade com a linguagem de programação C# o ajudará a acompanhar os exemplos.
- Editor de texto: Qualquer editor de texto serve, embora o Visual Studio Code seja recomendado por seus recursos e facilidade de uso.
## Importar namespaces
Para começar a usar o GroupDocs.Editor for .NET, você precisa importar os namespaces necessários para o seu projeto. Isso garante que todas as classes e métodos necessários estejam disponíveis para uso.
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```
Vamos dividir o processo em etapas gerenciáveis. Acompanhe enquanto orientamos você em cada etapa da edição de documentos de texto simples usando GroupDocs.Editor for .NET.
## Etapa 1: Obtenha um caminho para o arquivo TXT de entrada
Primeiro, você precisa especificar o caminho para o arquivo TXT de entrada. Pode ser um caminho para um arquivo local ou um fluxo contendo o conteúdo do arquivo.
```csharp
string inputFilePath = "YourSampleDocument.txt";
```
## Etapa 2: crie uma instância de editor
 Em seguida, crie uma instância do`Editor` aula. Esta classe é responsável por carregar e editar documentos. Nenhuma opção de carregamento é necessária neste estágio.
```csharp
using (Editor editor = new Editor(inputFilePath))
{
```
## Etapa 3: criar opções de edição de TXT
Agora, crie as opções de edição do TXT. Estas opções permitem especificar como o conteúdo do texto deve ser processado durante a edição.
```csharp
    TextEditOptions editOptions = new TextEditOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        RecognizeLists = true,
        LeadingSpaces = TextLeadingSpacesOptions.ConvertToIndent,
        TrailingSpaces = TextTrailingSpacesOptions.Trim
    };
```
## Etapa 4: crie uma instância EditableDocument
 Com as opções de edição definidas, crie um`EditableDocument` instância. Isso representa o documento em um formato editável.
```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```
## Etapa 5: edite o conteúdo do documento
Recupere o conteúdo do texto original e faça as edições desejadas. Neste exemplo, substituiremos a palavra “texto” por “Texto EDITADO”.
```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("text", "EDITED text");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## Etapa 6: crie um EditableDocument com conteúdo atualizado
 Depois de fazer as edições necessárias, crie um novo`EditableDocument` com o conteúdo atualizado e os recursos originais.
```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```
## Etapa 7: criar opções para salvar o processamento de texto
Prepare as opções de salvamento para o formato WordProcessing. Este exemplo usa o formato DOCM e especifica o código do idioma.
```csharp
    WordProcessingSaveOptions wordSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm)
    {
        Locale = System.Globalization.CultureInfo.GetCultureInfo("en-GB")
    };
```
## Etapa 8: criar opções de salvamento de TXT
Da mesma forma, crie as opções de salvamento para o formato TXT. Certifique-se de que a codificação esteja definida como UTF-8 e preserve o layout da tabela.
```csharp
    TextSaveOptions txtSaveOptions = new TextSaveOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        PreserveTableLayout = true
    };
```
## Etapa 9: preparar caminhos de saída
Prepare os caminhos para salvar os arquivos DOCX e TXT resultantes. Use o caminho do arquivo de entrada para determinar o diretório de saída e os nomes dos arquivos.
```csharp
    string outputWordPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".docm");
    string outputTxtPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".txt");
```
## Etapa 10: salve o documento editado
Por fim, salve o documento editado nos formatos DOCX e TXT usando as opções de salvamento especificadas.
```csharp
    editor.Save(afterEdit, outputWordPath, wordSaveOptions);
    editor.Save(afterEdit, outputTxtPath, txtSaveOptions);
}
System.Console.WriteLine("Document editing process completed successfully!");
```
## Conclusão
 Parabéns! Você editou com êxito um documento de texto simples usando GroupDocs.Editor for .NET. Esta ferramenta poderosa simplifica a edição de documentos, facilitando a integração em seus aplicativos .NET. Esteja você lidando com arquivos de texto simples ou formatos de documentos complexos, o GroupDocs.Editor tem o que você precisa. Explore mais recursos e capacidades visitando o[Documentação do GroupDocs.Editor](https://tutorials.groupdocs.com/editor/net/).
## Perguntas frequentes
### Quais formatos de arquivo o GroupDocs.Editor for .NET suporta?
 GroupDocs.Editor for .NET oferece suporte a uma ampla variedade de formatos de arquivo, incluindo DOCX, TXT, HTML e muito mais. Verifica a[documentação](https://tutorials.groupdocs.com/editor/net/) para obter uma lista completa.
### Como posso obter uma avaliação gratuita do GroupDocs.Editor for .NET?
 Você pode baixar uma versão de avaliação gratuita do GroupDocs.Editor for .NET no site[página de lançamentos](https://releases.groupdocs.com/).
### Posso adquirir uma licença temporária do GroupDocs.Editor for .NET?
Sim, você pode obter uma licença temporária do[Página de compra do GroupDocs](https://purchase.groupdocs.com/temporary-license/).
### Onde posso obter suporte para GroupDocs.Editor for .NET?
 O suporte está disponível através do[Fórum de suporte do GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).
### Existe documentação detalhada disponível para GroupDocs.Editor for .NET?
 Sim, a documentação detalhada está disponível no site[Página de documentação do GroupDocs.Editor](https://tutorials.groupdocs.com/editor/net/).