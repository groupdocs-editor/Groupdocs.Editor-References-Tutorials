---
title: Trabalhar com documentos XML
linktitle: Trabalhar com documentos XML
second_title: API GroupDocs.Editor .NET
description: Aprenda como editar documentos XML com eficiência usando GroupDocs.Editor for .NET com nosso guia passo a passo, cobrindo todas as etapas e opções essenciais.
weight: 20
url: /pt/net/document-processing/work-xml-documents/
---

# Trabalhar com documentos XML

## Introdução
No mundo digital de hoje, gerenciar e editar documentos XML de forma eficiente é crucial tanto para desenvolvedores quanto para empresas. GroupDocs.Editor for .NET oferece uma solução poderosa e versátil para editar arquivos XML programaticamente. Este tutorial irá guiá-lo através do processo de trabalho com documentos XML usando GroupDocs.Editor for .NET, detalhando cada etapa para torná-lo fácil e compreensível.
## Pré-requisitos
Antes de nos aprofundarmos nas etapas, vamos garantir que você tenha tudo de que precisa para começar.
1. Ambiente de desenvolvimento: certifique-se de ter um ambiente de desenvolvimento configurado. Visual Studio é altamente recomendado.
2. .NET Framework: GroupDocs.Editor for .NET oferece suporte a vários .NET frameworks. Certifique-se de que seu projeto seja direcionado a uma das versões suportadas.
3.  GroupDocs.Editor for .NET: Baixe e instale o GroupDocs.Editor for .NET a partir do[página de download](https://releases.groupdocs.com/editor/net/).
4.  Licença: Embora você possa usar uma licença temporária de[aqui](https://purchase.groupdocs.com/temporary-license/) , é recomendável adquirir uma licença completa para todas as funcionalidades do[página de compra](https://purchase.groupdocs.com/buy).
5. Arquivo XML de amostra: tenha um arquivo XML de amostra pronto que você gostaria de editar.
## Importar namespaces
Antes de começar com o código, você precisa importar os namespaces necessários. Isso permitirá que você acesse as funcionalidades fornecidas pelo GroupDocs.Editor for .NET.
```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.HtmlCss.Serialization;
using GroupDocs.Editor.Options;
```
## 1. Carregue o arquivo XML de entrada
A primeira etapa é carregar seu arquivo XML de entrada. Este servirá como o documento que você deseja editar.
```csharp
string inputFilePath = "Your Sample Document.xml";
```
## 2. Crie uma instância de editor
 Em seguida, crie uma instância do`Editor` aula. Esta classe é o componente principal que cuidará da edição do seu documento.
```csharp
using (Editor editor = new Editor(inputFilePath))
{
    // Continue com as etapas a seguir neste bloco de uso
}
```
## 3. Configure opções de edição de XML
Configure as opções de edição XML para atender às suas necessidades. Estas opções determinam como o conteúdo XML será processado.
```csharp
XmlEditOptions editOptions = new XmlEditOptions
{
    AttributeValuesQuoteType = QuoteType.DoubleQuote,
    RecognizeEmails = true,
    RecognizeUris = true,
    TrimTrailingWhitespaces = true
};
```
## 4. Crie uma instância de documento editável
 Gere um`EditableDocument` instância, que representa o documento XML em um formato editável.
```csharp
using (EditableDocument beforeEdit = editor.Edit(editOptions))
{
    // Prossiga com a edição do documento
}
```
## 5. Edite o conteúdo do documento
Agora você pode modificar o conteúdo do seu documento XML conforme necessário. Por exemplo, substituindo texto dentro do documento.
```csharp
string originalTextContent = beforeEdit.GetContent();
string updatedTextContent = originalTextContent.Replace("John", "Samuel");
List<IHtmlResource> allResources = beforeEdit.AllResources;
```
## 6. Crie um documento editável com conteúdo atualizado
 Depois de fazer as edições necessárias, crie um novo`EditableDocument` instância com o conteúdo atualizado.
```csharp
using (EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources))
{
    // Prepare-se para salvar o documento
}
```
## 7. Configure opções de salvamento para diferentes formatos
GroupDocs.Editor permite salvar o documento editado em vários formatos. Aqui configuraremos opções para salvar nos formatos DOCX e TXT.
```csharp
WordProcessingSaveOptions wordSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docx);
TextSaveOptions txtSaveOptions = new TextSaveOptions
{
    Encoding = System.Text.Encoding.UTF8
};
```
## 8. Prepare caminhos de saída
Especifique os caminhos onde os documentos editados serão salvos.
```csharp
string outputWordPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".docx");
string outputTxtPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".txt");
```
## 9. Salve o documento editado
Por fim, salve o documento editado nos caminhos especificados usando as opções de salvamento configuradas anteriormente.
```csharp
editor.Save(afterEdit, outputWordPath, wordSaveOptions);
editor.Save(afterEdit, outputTxtPath, txtSaveOptions);
```
## 10. Conclua o processo
Após a conclusão, imprima uma mensagem de confirmação no console.
```csharp
System.Console.WriteLine("WorkingWithXml routine has successfully finished");
```
## Conclusão
Trabalhar com documentos XML usando GroupDocs.Editor for .NET é simples e eficiente. Seguindo as etapas descritas neste guia, você pode facilmente carregar, editar e salvar arquivos XML de forma programática. Se você precisa fazer pequenas substituições de texto ou modificações extensas no conteúdo, o GroupDocs.Editor for .NET fornece as ferramentas e a flexibilidade necessárias para lidar com suas necessidades de edição de documentos.
## Perguntas frequentes
### O que é GroupDocs.Editor para .NET?
GroupDocs.Editor for .NET é uma biblioteca que permite aos desenvolvedores editar vários formatos de documentos, incluindo XML, programaticamente em aplicativos .NET.
### Posso usar o GroupDocs.Editor gratuitamente?
 GroupDocs.Editor oferece uma avaliação gratuita que você pode acessar[aqui](https://releases.groupdocs.com/). Para funcionalidade completa, você precisa adquirir uma licença.
### Como obtenho suporte para GroupDocs.Editor for .NET?
 Você pode obter suporte do[Fórum de suporte do GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).
### Em quais formatos de arquivo posso converter XML usando GroupDocs.Editor?
Você pode converter XML em vários formatos, incluindo DOCX e TXT, usando as opções de salvamento apropriadas.
### Existe uma licença temporária disponível para teste?
 Sim, você pode obter uma licença temporária para fins de teste em[aqui](https://purchase.groupdocs.com/temporary-license/).