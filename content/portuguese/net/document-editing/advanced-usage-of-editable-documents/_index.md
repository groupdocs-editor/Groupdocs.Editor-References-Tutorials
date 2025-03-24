---
title: Uso avançado de documentos editáveis
linktitle: Uso avançado de documentos editáveis
second_title: API GroupDocs.Editor .NET
description: Aprenda o uso avançado do GroupDocs.Editor for .NET criando, editando e extraindo recursos de documentos de forma programática.
weight: 11
url: /pt/net/document-editing/advanced-usage-of-editable-documents/
---

# Uso avançado de documentos editáveis

## Introdução
Se você é um desenvolvedor .NET e deseja aprimorar seus recursos de edição de documentos, o GroupDocs.Editor for .NET oferece um poderoso conjunto de ferramentas. Este guia abrangente orientará você no uso avançado de documentos editáveis usando o GroupDocs.Editor, detalhando cada etapa para garantir que você possa aproveitar todo o seu potencial.
## Pré-requisitos
Antes de mergulhar nas funcionalidades avançadas, certifique-se de ter o seguinte:
- Visual Studio instalado em sua máquina de desenvolvimento.
- .NET Framework compatível com GroupDocs.Editor.
-  Biblioteca GroupDocs.Editor para .NET. Você pode[baixe aqui](https://releases.groupdocs.com/editor/net/).
-  Uma licença válida do GroupDocs.Editor. Você pode obter um[teste grátis](https://releases.groupdocs.com/) ou compre um[licença temporária](https://purchase.groupdocs.com/temporary-license/).
## Importar namespaces
Para começar, certifique-se de importar os namespaces necessários em seu projeto .NET:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```
## Etapa 1: Criando uma instância EditableDocument
 Primeiro, você precisa criar uma instância de`EditableDocument` carregando e editando um documento de entrada de um formato suportado.
```csharp
string inputFilePath = "YourSampleDocument.docx";
Editor editor = new Editor(inputFilePath, delegate { return new WordProcessingLoadOptions(); });
EditableDocument beforeEdit = editor.Edit(new WordProcessingEditOptions());
```
Nesta etapa, carregamos o documento de entrada e o preparamos para edição.
## Etapa 2: Extraindo Recursos de Documentos
 O`EditableDocument` contém vários recursos que podem ser extraídos e manipulados. Vamos decompô-los:
### Etapa 2.1: Extraia o documento inteiro como HTML
Você pode gerar uma única string que contém o documento inteiro com todos os seus recursos incorporados como HTML.
```csharp
string allAsHtmlInsideOneString = beforeEdit.GetEmbeddedHtml();
```
Essa string será bem grande, pois inclui folhas de estilo, imagens e fontes codificadas em base64.
### Etapa 2.2: extrair todas as imagens
Extraia todas as imagens do documento.
```csharp
List<IImageResource> allImages = beforeEdit.Images;
```
### Etapa 2.3: extrair todas as fontes
Extraia todas as fontes usadas no documento.
```csharp
List<FontResourceBase> allFonts = beforeEdit.Fonts;
```
### Etapa 2.4: extrair todas as folhas de estilo
Extraia todas as folhas de estilo em formato textual.
```csharp
List<CssText> allStylesheets = beforeEdit.Css;
```
### Etapa 2.5: Reúna todos os recursos
Reúna todos os recursos em uma chamada.
```csharp
List<IHtmlResource> allResources = beforeEdit.AllResources;
```
Isso inclui imagens, fontes e folhas de estilo.
### Etapa 2.6: Obtenha a marcação HTML
Obtenha a marcação HTML do documento sem recursos incorporados.
```csharp
string htmlMarkup = beforeEdit.GetContent();
```
## Etapa 3: Ajustando Links Externos
Às vezes, você precisa ajustar links externos para apontar para um manipulador de recursos personalizado. Veja como fazer isso:
### Etapa 3.1: preparar prefixos personalizados
Prepare prefixos que precederão links externos originais.
```csharp
string customImagesRequesthandlerUri = "http://exemplo.com/ImagesHandler/id=";
string customCssRequesthandlerUri = "http://exemplo.com/CssHandler/id=";
string customFontsRequesthandlerUri = "http://exemplo.com/FontsHandler/id=";
```
### Etapa 3.2: Gerar marcação HTML prefixada
Gere marcação HTML com links ajustados.
```csharp
string prefixedHtmlMarkup = beforeEdit.GetContent(customImagesRequesthandlerUri, customCssRequesthandlerUri);
```
### Etapa 3.3: Obtenha conteúdo HTML somente para o corpo
Alguns editores WYSIWYG lidam apenas com marcação HTML pura, sem cabeçalhos.
```csharp
string onlyBodyContent = beforeEdit.GetBodyContent();
```
### Etapa 3.4: Conteúdo somente corpo prefixado
Gere conteúdo somente de corpo com prefixos de imagem personalizados.
```csharp
string prefixedBodyContent = beforeEdit.GetBodyContent(customImagesRequesthandlerUri);
```
### Etapa 3.5: Extrair folhas de estilo
Extraia folhas de estilo usadas no documento.
```csharp
List<string> stylesheets = beforeEdit.GetCssContent();
```
### Etapa 3.6: Folhas de estilo prefixadas
Extraia folhas de estilo com prefixos personalizados.
```csharp
List<string> prefixedStylesheets = beforeEdit.GetCssContent(customImagesRequesthandlerUri, customFontsRequesthandlerUri);
```
## Etapa 4: salvar o documento como HTML
Salve o documento editado como um arquivo HTML, incluindo seus recursos.
```csharp
string htmlFilePath = Path.Combine("output", Path.GetFileNameWithoutExtension(inputFilePath) + ".html");
beforeEdit.Save(htmlFilePath);
```
Este método cria um diretório separado para recursos como folhas de estilo, imagens e fontes.
## Etapa 5: Descarte de EditableDocument
 Implementos EditableDocument`IDisposable` e fornece a capacidade de verificar se a instância foi descartada.
```csharp
Console.WriteLine("EditableDocument is {0} disposed", !beforeEdit.IsDisposed ? "not" : "already");
```
### Etapa 5.1 Tratamento do evento Dispose
Você também pode se inscrever no evento de descarte.
```csharp
EventHandler someMethod = delegate { Console.WriteLine("Disposing event was spotted!"); };
beforeEdit.Disposed += someMethod;
```
## Etapa 6: Criando EditableDocument a partir de HTML
Crie uma instância de EditableDocument a partir de um documento HTML.
### Etapa 6.1: do arquivo HTML
```csharp
EditableDocument afterEditFromFile = EditableDocument.FromFile(htmlFilePath, null);
```
### Etapa 6.2: Da marcação HTML
```csharp
EditableDocument afterEditFromMarkup = EditableDocument.FromMarkup(htmlMarkup, allResources);
```
Essas instâncias (afterEditFromFile e afterEditFromMarkup) são idênticas às originais (beforeEdit).
## Etapa 7: descarte manual
Descarte manualmente suas instâncias de EditableDocument.
```csharp
beforeEdit.Dispose();
afterEditFromFile.Dispose();
afterEditFromMarkup.Dispose();
editor.Dispose();
```
Isso garante a limpeza adequada dos recursos.
## Conclusão
GroupDocs.Editor for .NET fornece ferramentas robustas para edição de documentos programaticamente. Seguindo este guia passo a passo, você pode gerenciar com eficiência o conteúdo, os recursos e os formatos de saída do documento. Esteja você incorporando recursos, ajustando links externos ou convertendo documentos em HTML, o GroupDocs.Editor fornece a funcionalidade necessária para manipulação avançada de documentos.
## Perguntas frequentes
### Quais formatos o GroupDocs.Editor suporta?
GroupDocs.Editor suporta vários formatos, incluindo DOCX, XLSX, PPTX e muito mais.
### Posso usar o GroupDocs.Editor sem licença?
 Sim, você pode usá-lo com um[teste grátis](https://releases.groupdocs.com/) ou um[licença temporária](https://purchase.groupdocs.com/temporary-license/).
### Como extraio recursos específicos de um documento?
 Você pode extrair imagens, fontes e folhas de estilo usando os métodos fornecidos, como`Images`, `Fonts` , e`Css`.
### É possível ajustar links na saída HTML?
Sim, você pode ajustar links externos especificando prefixos personalizados para imagens, CSS e fontes.
### Como salvo um documento editado como um arquivo HTML?
 Use o`Save` método do`EditableDocument`class para salvar o documento como um arquivo HTML, incluindo seus recursos.