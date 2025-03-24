---
title: Criar documento
linktitle: Criar documento
second_title: API GroupDocs.Editor .NET
description: Aprenda como editar documentos do Word, Excel, PowerPoint, Ebook e e-mail usando GroupDocs.Editor for .NET com este tutorial passo a passo abrangente.
weight: 10
url: /pt/net/document-editing/create-document/
---
## Introdução
Você está cansado do incômodo de editar diferentes tipos de documentos de forma programática? GroupDocs.Editor for .NET está aqui para simplificar o processo. Esta ferramenta poderosa permite aos desenvolvedores editar vários formatos de documentos, como Word, Excel, PowerPoint, E-books e e-mails com facilidade. Neste tutorial, nos aprofundaremos em como usar o GroupDocs.Editor for .NET para criar e editar documentos. Dividiremos o processo em etapas fáceis de seguir, tornando-o acessível mesmo se você for novo nisso.
## Pré-requisitos
Antes de começarmos, certifique-se de ter o seguinte:
- Visual Studio instalado em sua máquina.
- .NET Framework (4.0 ou superior).
-  Biblioteca GroupDocs.Editor para .NET. Você pode baixá-lo em[aqui](https://releases.groupdocs.com/editor/net/).
- Conhecimento básico de programação C#.
## Importar namespaces
Primeiro, vamos importar os namespaces necessários. Isso tornará as classes e métodos necessários acessíveis em nosso aplicativo.
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using System.IO;
```
## Etapa 1: configurando o stream
Para começar, precisamos configurar um fluxo de memória que atuará como nosso espaço reservado para o conteúdo do documento.
```csharp
Stream memoryStream = Stream.Null;
```
## Etapa 2: Função de retorno de chamada para salvar o documento
A seguir, defina uma função de retorno de chamada que salvará o novo fluxo de documentos. Esta função é essencial para lidar com o resultado do processo de edição de documentos.
```csharp
void SaveNewDocument(Stream resultStream)
{
    memoryStream = resultStream;
}
```
## Etapa 3: Criando e editando um documento de processamento de texto
 Agora, vamos criar e editar um documento Word. Começaremos criando um novo`Editor` instância para documentos do WordProcessing e edite-a com opções padrão.
### Criar e editar com opções padrão
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    EditableDocument defaultWordProcessingDoc = editor.Edit();
}
```
### Crie e edite com opções personalizadas
Para obter mais controle, podemos especificar opções como desabilitar paginação e extrair fontes incorporadas.
```csharp
using (Editor editor = new Editor(SaveNewDocument, WordProcessingFormats.Docx))
{
    WordProcessingEditOptions wordProcessingEditOptions = new WordProcessingEditOptions
    {
        EnablePagination = false,
        EnableLanguageInformation = true,
        FontExtraction = FontExtractionOptions.ExtractAllEmbedded
    };
    EditableDocument editableWordProcessingDocument = editor.Edit(wordProcessingEditOptions);
}
```
## Etapa 4: Criando e editando um documento de planilha
Da mesma forma, podemos criar e editar um documento Excel. Veja como você faz isso.
### Criar e editar com opções padrão
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    EditableDocument defaultEditableSpreadsheetDocument = editor.Edit();
}
```
### Crie e edite com opções personalizadas
 Para direcionar planilhas específicas ou excluir planilhas ocultas, usamos`SpreadsheetEditOptions`.
```csharp
using (Editor editor = new Editor(SaveNewDocument, SpreadsheetFormats.Xlsx))
{
    SpreadsheetEditOptions spreadsheetEditOptions = new SpreadsheetEditOptions
    {
        WorksheetIndex = 0,
        ExcludeHiddenWorksheets = true
    };
    EditableDocument editableSpreadsheetDocument = editor.Edit(spreadsheetEditOptions);
}
```
## Etapa 5: Criando e editando um documento de apresentação
Apresentações em PowerPoint também são suportadas. Vamos ver como lidar com eles.
### Criar e editar com opções padrão
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    EditableDocument defaultEditablePresentationDocument = editor.Edit();
}
```
### Crie e edite com opções personalizadas
Você pode personalizar suas edições especificando opções como qual slide mostrar e se deseja incluir slides ocultos.
```csharp
using (Editor editor = new Editor(SaveNewDocument, PresentationFormats.Pptx))
{
    PresentationEditOptions presentationEditOptions = new PresentationEditOptions
    {
        ShowHiddenSlides = false,
        SlideNumber = 0
    };
    EditableDocument editablePresentationDocument = editor.Edit(presentationEditOptions);
}
```
## Etapa 6: Criação e edição de um documento de e-book
GroupDocs.Editor também permite editar formatos de Ebook como EPUB. Veja como você pode lidar com isso.
### Criar e editar com opções padrão
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EditableDocument defaultEditableEbookDocument = editor.Edit();
}
```
### Crie e edite com opções personalizadas
Personalize a edição do seu e-book ativando ou desativando a paginação e as informações de idioma.
```csharp
using (Editor editor = new Editor(SaveNewDocument, EBookFormats.Epub))
{
    EbookEditOptions ebookEditOptions = new EbookEditOptions
    {
        EnablePagination = false,
        EnableLanguageInformation = true
    };
    EditableDocument editableEbookDocument = editor.Edit(ebookEditOptions);
}
```
## Etapa 7: Criando e editando um documento de e-mail
Por fim, veremos como editar documentos de e-mail. Isso inclui formatos como EML.
### Criar e editar com opções padrão
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EditableDocument defaultEditableEmailDocument = editor.Edit();
}
```
### Crie e edite com opções personalizadas
Especifique opções de saída de mensagens de correio para controlar o processo de edição.
```csharp
using (Editor editor = new Editor(SaveNewDocument, EmailFormats.Eml))
{
    EmailEditOptions emailEditOptions = new EmailEditOptions
    {
        MailMessageOutput = MailMessageOutput.All
    };
    EditableDocument editableEmailDocument = editor.Edit(emailEditOptions);
}
```
## Etapa 8: Finalizando o Processo
Depois de editar os documentos, é crucial descartar adequadamente o fluxo de memória para liberar recursos.
```csharp
memoryStream.Dispose();
System.Console.WriteLine("CreateDocument routine has successfully finished");
```
## Conclusão
GroupDocs.Editor for .NET é uma ferramenta versátil e poderosa que pode simplificar a tarefa de edição de vários tipos de documentos programaticamente. Seguindo este guia passo a passo, você pode criar e editar documentos com facilidade, sejam eles arquivos de processamento de texto, planilhas, apresentações, e-books ou e-mails. Mergulhe na documentação do GroupDocs.Editor para recursos mais avançados e opções de personalização.
## Perguntas frequentes
### Que tipos de documentos posso editar com GroupDocs.Editor for .NET?
Você pode editar uma ampla variedade de documentos, incluindo processamento de texto, planilhas, apresentações, e-books e e-mails.
### É possível personalizar as opções de edição?
Sim, o GroupDocs.Editor for .NET permite ampla personalização por meio de várias opções de edição específicas para cada tipo de documento.
### Como lidar com a saída dos documentos editados?
Você pode usar uma função de retorno de chamada para salvar o fluxo de documentos editado no local desejado.
### Preciso de uma licença para usar o GroupDocs.Editor for .NET?
 Sim, você pode obter uma licença de[aqui](https://purchase.groupdocs.com/buy). Também existe a opção de licença temporária.
### Onde posso encontrar documentação mais detalhada?
 A documentação detalhada está disponível no site[Página de documentação do GroupDocs.Editor para .NET](https://tutorials.groupdocs.com/editor/net/).