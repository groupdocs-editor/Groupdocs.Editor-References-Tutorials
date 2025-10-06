---
title: Trabalhe com planilhas com várias guias
linktitle: Trabalhe com planilhas com várias guias
second_title: API GroupDocs.Editor .NET
description: Aprenda como trabalhar com planilhas com várias guias no .NET usando GroupDocs.Editor. Guia passo a passo, exemplos de código e práticas recomendadas incluídas.
weight: 17
url: /pt/net/document-processing/work-multi-tab-spreadsheets/
type: docs
---
# Trabalhe com planilhas com várias guias

## Introdução
Lidar com planilhas com várias guias pode ser uma tarefa e tanto, especialmente quando você precisa manipular ou extrair dados de planilhas diferentes no mesmo documento. Se você trabalha com .NET e procura uma solução robusta, GroupDocs.Editor for .NET é uma excelente escolha. Neste tutorial, orientaremos você no processo de trabalho com planilhas com várias guias usando GroupDocs.Editor for .NET. Abordaremos tudo, desde a configuração do seu ambiente até salvar cada guia como um arquivo separado.
## Pré-requisitos
Antes de mergulhar no tutorial, certifique-se de ter os seguintes pré-requisitos em vigor:
1. Visual Studio: certifique-se de ter o Visual Studio instalado em sua máquina.
2. .NET Framework: GroupDocs.Editor for .NET oferece suporte a .NET Framework 4.0 ou superior.
3. GroupDocs.Editor for .NET: Baixe e instale a biblioteca GroupDocs.Editor for .NET. Você pode obtê-lo no[página de download](https://releases.groupdocs.com/editor/net/).
4.  Licença: Embora você possa usar um[licença temporária](https://purchase.groupdocs.com/temporary-license/) para experimentar a biblioteca, é recomendável adquirir uma licença completa para uso em produção.
## Importar namespaces
Antes de começarmos a codificar, você precisa importar os namespaces necessários. Adicione as seguintes diretivas using ao topo do seu arquivo .cs:
```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
## 1. Obtenha um caminho para o arquivo de entrada
Primeiro, você precisa especificar o caminho para o arquivo da planilha de entrada. Este arquivo deve ser um XLSX (OOXML) com múltiplas abas.
```csharp
string inputFilePath = "Your Sample Document";
```
## 2. Carregue a planilha na instância do editor
 A seguir, você carregará a planilha em um`Editor` instância. Isso é feito usando um fluxo de arquivos e especificando as opções de carregamento apropriadas para uma planilha.
```csharp
using (FileStream inputStream = File.OpenRead(inputFilePath))
{
    using (Editor editor = new Editor(delegate { return inputStream; }, delegate { return new SpreadsheetLoadOptions(); }))
    {
        // Outras etapas irão aqui
    }
}
```
## 3. Crie um EditableDocument na primeira guia
 Para editar ou manipular uma aba específica, você precisa criar um`EditableDocument` instância para essa guia. A guia é especificada usando um índice baseado em 0.
```csharp
SpreadsheetEditOptions editOptions1 = new SpreadsheetEditOptions();
editOptions1.WorksheetIndex = 0; // Primeira guia
EditableDocument firstTabBeforeEdit = editor.Edit(editOptions1);
```
## 4. Crie um EditableDocument na segunda guia
 Da mesma forma, crie um`EditableDocument` para a segunda guia.
```csharp
SpreadsheetEditOptions editOptions2 = new SpreadsheetEditOptions();
editOptions2.WorksheetIndex = 1; // Segunda guia
EditableDocument secondTabBeforeEdit = editor.Edit(editOptions2);
```
## 5. Salve a primeira guia em um documento separado
Agora salve a primeira guia como um documento separado. Especifique o formato de salvamento e o caminho de saída.
```csharp
SpreadsheetSaveOptions saveOptions1 = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
string outputFilename1 = Path.GetFileNameWithoutExtension(inputFilePath) + "_tab1.xlsm";
string outputPath1 = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename1);
editor.Save(firstTabBeforeEdit, outputPath1, saveOptions1);
```
## 6. Salve a segunda guia em um documento separado
Repita o processo para a segunda aba, mas desta vez salve-a em um formato diferente.
```csharp
SpreadsheetSaveOptions saveOptions2 = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsb);
string outputFilename2 = Path.GetFileNameWithoutExtension(inputFilePath) + "_tab2.xlsb";
string outputPath2 = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename2);
editor.Save(secondTabBeforeEdit, outputPath2, saveOptions2);
```
## 7. Descarte instâncias de EditableDocument
 Por fim, certifique-se de descartar adequadamente o`EditableDocument` instâncias para liberar recursos.
```csharp
firstTabBeforeEdit.Dispose();
secondTabBeforeEdit.Dispose();
```

## Conclusão
Seguindo essas etapas, você pode trabalhar facilmente com planilhas com várias guias no .NET usando GroupDocs.Editor. Esta poderosa biblioteca simplifica o processo de edição e salvamento de diferentes planilhas em uma planilha, tornando suas tarefas de desenvolvimento mais gerenciáveis. Esteja você lidando com manipulação complexa de dados ou edições simples, o GroupDocs.Editor for .NET fornece as ferramentas necessárias para realizar o trabalho com eficiência.
## Perguntas frequentes
### O que é GroupDocs.Editor para .NET?
GroupDocs.Editor for .NET é uma poderosa API de edição de documentos que permite aos desenvolvedores carregar, editar e salvar documentos de vários formatos em aplicativos .NET.
### Posso experimentar o GroupDocs.Editor for .NET antes de comprar?
 Sim, você pode usar um[teste grátis](https://releases.groupdocs.com/) ou solicite um[licença temporária](https://purchase.groupdocs.com/temporary-license/) para avaliar o produto.
### Quais formatos de arquivo são suportados pelo GroupDocs.Editor for .NET?
GroupDocs.Editor oferece suporte a uma ampla variedade de formatos, incluindo DOCX, XLSX, PPTX, PDF e muitos mais.
### Como obtenho suporte para GroupDocs.Editor for .NET?
 Você pode obter suporte visitando o[Fórum de suporte](https://forum.groupdocs.com/c/editor/20).
### Onde posso comprar uma licença completa do GroupDocs.Editor for .NET?
 Você pode adquirir uma licença completa no site[página de compra](https://purchase.groupdocs.com/buy).