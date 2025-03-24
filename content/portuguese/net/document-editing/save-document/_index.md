---
title: Salvar documento
linktitle: Salvar documento
second_title: API GroupDocs.Editor .NET
description: Edite e salve documentos sem esforço usando GroupDocs.Editor for .NET. Este guia passo a passo simplifica o processo para desenvolvedores.
weight: 14
url: /pt/net/document-editing/save-document/
---

# Salvar documento

## Introdução
Você deseja editar e salvar documentos sem esforço usando GroupDocs.Editor for .NET? Você está no lugar certo! Este tutorial irá guiá-lo passo a passo pelo processo, garantindo que você possa gerenciar facilmente seus documentos. Quer você seja um desenvolvedor experiente ou iniciante, nosso guia fornecerá todas as informações necessárias para começar.
## Pré-requisitos
Antes de mergulhar no tutorial, certifique-se de ter os seguintes pré-requisitos em vigor:
- Ambiente de Desenvolvimento: Visual Studio instalado em sua máquina.
- .NET Framework: certifique-se de ter o .NET Framework 4.6.1 ou posterior.
-  GroupDocs.Editor para .NET: Baixe a versão mais recente[aqui](https://releases.groupdocs.com/editor/net/).
- Conhecimento básico de C#: Familiaridade com programação C# é essencial.
## Importar namespaces
Para usar GroupDocs.Editor em seu projeto .NET, você precisa importar os namespaces necessários. Veja como você faz isso:
```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
Agora que configuramos nosso ambiente e importamos os namespaces necessários, vamos nos aprofundar nas etapas necessárias para carregar, editar e salvar um documento usando GroupDocs.Editor for .NET.
## Etapa 1: carregue o documento
Primeiro precisamos carregar o documento que queremos editar. GroupDocs.Editor torna esse processo simples. Veja como você pode fazer isso:

```csharp
string inputFilePath = "Your Sample Document";
Editor editor = new Editor(inputFilePath, delegate { return new Options.WordProcessingLoadOptions(); });
EditableDocument defaultWordProcessingDoc = editor.Edit();
```
 Nesta etapa, especificamos o caminho para o documento que queremos editar e criamos uma instância do`Editor` aula. O`Edit` método é então chamado para carregar o documento em um`EditableDocument` objeto.
## Etapa 2: modificar o documento
Com o documento carregado, é hora de fazer algumas modificações. Como não temos um editor WYSIWYG anexado, simularemos o processo de edição em código.

```csharp
string allEmbeddedInsideString = defaultWordProcessingDoc.GetEmbeddedHtml();
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
EditableDocument editedDoc = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null);
```
 Aqui, recuperamos o conteúdo HTML incorporado do documento, realizamos uma simples substituição de texto e criamos um novo`EditableDocument`instância do HTML modificado.
## Etapa 3: salve o documento
Após editar o documento, a etapa final é salvá-lo. GroupDocs.Editor oferece várias opções para salvar o documento em diferentes formatos.
## Salvar como RTF
```csharp
string outputRtfPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.rtf");
WordProcessingSaveOptions rtfSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Rtf);
editor.Save(editedDoc, outputRtfPath, rtfSaveOptions);
```
## Salvar como DOCM
```csharp
string outputDocmPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.docm");
WordProcessingSaveOptions docmSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm);
using (FileStream outputStream = File.Create(outputDocmPath))
{
    editor.Save(editedDoc, outputStream, docmSaveOptions);
}
```
## Salvar como texto simples
```csharp
string outputTxtPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.txt");
TextSaveOptions textSaveOptions = new TextSaveOptions
{
    Encoding = System.Text.Encoding.UTF8,
    PreserveTableLayout = true
};
editor.Save(editedDoc, outputTxtPath, textSaveOptions);
```
## Etapa 4: limpeza
 Finalmente, é crucial descartar o`EditableDocument` e`Editor` instâncias para liberar recursos.
```csharp
editedDoc.Dispose();
defaultWordProcessingDoc.Dispose();
editor.Dispose();
```
Seguindo essas etapas, você pode carregar, editar e salvar documentos com eficiência usando GroupDocs.Editor for .NET. Esta ferramenta poderosa oferece flexibilidade e facilidade de uso, facilitando o gerenciamento de documentos.
## Conclusão
Editar e salvar documentos programaticamente nunca foi tão fácil com GroupDocs.Editor for .NET. Este guia orientou você durante todo o processo, desde carregar um documento até salvá-lo em vários formatos. Com o GroupDocs.Editor, você tem uma solução versátil e robusta ao seu alcance, simplificando o processo de edição de documentos.
## Perguntas frequentes
### Quais formatos de arquivo o GroupDocs.Editor suporta?
GroupDocs.Editor suporta vários formatos de arquivo, incluindo DOCX, RTF, TXT e muitos mais. Para uma lista completa, confira o[documentação](https://tutorials.groupdocs.com/editor/net/).
### Posso experimentar o GroupDocs.Editor antes de comprar?
 Sim, você pode obter um[teste grátis](https://releases.groupdocs.com/) para testar os recursos do GroupDocs.Editor.
### Existe algum suporte disponível se eu tiver problemas?
 Absolutamente! Você pode visitar o[Fórum de suporte](https://forum.groupdocs.com/c/editor/20) para obter assistência com quaisquer problemas que você encontrar.
### Como posso obter uma licença temporária?
 Você pode solicitar um[licença temporária](https://purchase.groupdocs.com/temporary-license/) para fins de avaliação.
### Onde posso comprar a versão completa do GroupDocs.Editor?
 Você pode comprar a versão completa[aqui](https://purchase.groupdocs.com/buy).