---
title: Trabalhar com valores separados delimitados (DSV)
linktitle: Trabalhar com valores separados delimitados (DSV)
second_title: API GroupDocs.Editor .NET
description: Aprenda como editar arquivos CSV e TSV usando GroupDocs.Editor for .NET com este guia passo a passo. Melhore seus projetos .NET sem esforço.
weight: 12
url: /pt/net/document-processing/work-dsv/
---
## Introdução
Se você é um desenvolvedor que trabalha com valores separados delimitados (DSV), como arquivos CSV ou TSV, sabe que editar esses arquivos programaticamente pode ser uma tarefa difícil. No entanto, com GroupDocs.Editor for .NET, esta tarefa torna-se significativamente mais simples e eficiente. Neste tutorial, orientaremos você sobre como usar o GroupDocs.Editor for .NET para ler, editar e salvar arquivos DSV. Dividiremos o processo em etapas fáceis de seguir, tornando-o simples para você implementar em seus projetos.
## Pré-requisitos
Antes de mergulharmos no tutorial, certifique-se de ter os seguintes pré-requisitos:
- Visual Studio: certifique-se de ter o Visual Studio instalado em sua máquina.
-  GroupDocs.Editor for .NET: você precisará baixar e referenciar a biblioteca GroupDocs.Editor for .NET. Você pode baixá-lo[aqui](https://releases.groupdocs.com/editor/net/).
- Compreensão básica de C#: este tutorial pressupõe que você tenha uma compreensão básica de desenvolvimento em C# e .NET.
## Importar namespaces
Primeiro, você precisa importar os namespaces necessários para o seu projeto. Esses namespaces fornecem as classes e os métodos necessários para trabalhar com GroupDocs.Editor for .NET.
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

## Etapa 1: Obtenha um caminho para o arquivo DSV de entrada
Primeiro, você precisa especificar o caminho para o arquivo DSV de entrada. Neste exemplo, assumiremos que é um arquivo CSV.
```csharp
string inputFilePath = "Your Sample Document";
```
## Etapa 2: crie uma instância de editor
 Crie uma instância do`Editor` aula. Esta instância será usada para carregar e manipular o arquivo DSV.
```csharp
using (Editor editor = new Editor(inputFilePath))
{
```
## Etapa 3: criar opções de edição de DSV
 Em seguida, crie uma instância de`DelimitedTextEditOptions` e especifique o delimitador para o arquivo DSV. Aqui, usamos uma vírgula como delimitador.
```csharp
    Options.DelimitedTextEditOptions editOptions = new DelimitedTextEditOptions(",");
    editOptions.ConvertDateTimeData = false;
    editOptions.ConvertNumericData = true;
    editOptions.TreatConsecutiveDelimitersAsOne = true;
```
## Etapa 4: crie uma instância EditableDocument
 Criar um`EditableDocument` instância usando o`Editor.Edit` método. Isso prepara o documento para edição.
```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```
## Etapa 5: edite o conteúdo do documento
Recupere o conteúdo do texto original e faça as modificações necessárias. Para fins de demonstração, vamos substituir algum texto.
```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("SsangYong", "Chevrolet").Replace("Kyron", "Camaro");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## Etapa 6: crie um EditableDocument com conteúdo atualizado
 Crie um novo`EditableDocument` com o conteúdo atualizado.
```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```
## Etapa 7: criar opções para salvar CSV
Especifique as opções de salvamento para o formato CSV, incluindo o delimitador e a codificação.
```csharp
    Options.DelimitedTextSaveOptions csvSaveOptions = new DelimitedTextSaveOptions(",");
    csvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```
## Etapa 8: criar opções de salvamento de TSV
Da mesma forma, especifique as opções de salvamento para o formato TSV.
```csharp
    Options.DelimitedTextSaveOptions tsvSaveOptions = new DelimitedTextSaveOptions("\t");
    tsvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```
## Etapa 9: criar opções para salvar planilhas
Se você precisar salvar o documento como uma planilha, crie as opções de salvamento correspondentes.
```csharp
    Options.SpreadsheetSaveOptions cellsSaveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
```
## Etapa 10: preparar caminhos para salvar
Defina os caminhos onde os arquivos editados serão salvos.
```csharp
    string outputCsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".csv");
    string outputTsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".tsv");
    string outputCellsPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".xlsm");
```
## Etapa 11: salve o documento editado
Salve o documento editado nos caminhos especificados em diferentes formatos.
```csharp
    editor.Save(afterEdit, outputCsvPath, csvSaveOptions);
    editor.Save(afterEdit, outputTsvPath, tsvSaveOptions);
    editor.Save(afterEdit, outputCellsPath, cellsSaveOptions);
```
## Etapa 12: descartar instâncias de EditableDocument
 Finalmente, certifique-se de descartar o`EditableDocument` instâncias para liberar recursos.
```csharp
    beforeEdit.Dispose();
    afterEdit.Dispose();
}
System.Console.WriteLine("WorkingWithDsv routine has successfully finished");
```
## Conclusão
edição de arquivos DSV usando GroupDocs.Editor for .NET é um processo simples que envolve a criação de uma instância do editor, configuração de opções de edição, modificação do conteúdo e salvamento das alterações. Este guia passo a passo deve ajudá-lo a integrar essa funcionalidade em seus aplicativos .NET com facilidade. Esteja você trabalhando com CSV, TSV ou outros formatos DSV, o GroupDocs.Editor for .NET oferece uma solução robusta e flexível.
## Perguntas frequentes
### Posso usar o GroupDocs.Editor for .NET para editar arquivos CSV grandes?
Sim, o GroupDocs.Editor for .NET é capaz de lidar com arquivos CSV grandes com eficiência.
### O GroupDocs.Editor for .NET oferece suporte a outros formatos DSV além de CSV e TSV?
Sim, ele oferece suporte a vários formatos DSV, desde que você especifique o delimitador apropriado.
### É possível personalizar a codificação ao salvar arquivos DSV?
Com certeza, você pode especificar a codificação desejada nas opções de salvamento.
### Posso converter um arquivo CSV em uma planilha do Excel usando GroupDocs.Editor for .NET?
Sim, você pode salvar um arquivo CSV como uma planilha do Excel usando as opções de salvamento apropriadas.
### Onde posso encontrar mais documentação sobre GroupDocs.Editor for .NET?
 Você pode encontrar documentação detalhada[aqui](https://tutorials.groupdocs.com/editor/net/)