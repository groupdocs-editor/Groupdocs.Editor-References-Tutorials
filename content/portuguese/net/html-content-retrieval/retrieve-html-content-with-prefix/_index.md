---
title: Recuperar conteúdo HTML com prefixo
linktitle: Recuperar conteúdo HTML com prefixo
second_title: API GroupDocs.Editor .NET
description: Aprenda como recuperar conteúdo HTML de documentos usando GroupDocs.Editor for .NET com prefixos personalizados para imagens e folhas de estilo. Guia passo a passo incluído.
weight: 11
url: /pt/net/html-content-retrieval/retrieve-html-content-with-prefix/
---
## Introdução
Bem-vindo ao nosso tutorial passo a passo sobre como recuperar conteúdo HTML de um documento usando GroupDocs.Editor for .NET. Quer você seja um desenvolvedor experiente ou esteja apenas começando, este guia irá guiá-lo pelo processo de uma maneira fácil de seguir. Abordaremos tudo o que você precisa saber, desde a configuração do seu ambiente até a execução do código com sucesso. Vamos mergulhar!
## Pré-requisitos
Antes de começarmos, certifique-se de ter os seguintes pré-requisitos em vigor:
1.  GroupDocs.Editor for .NET: Baixe a versão mais recente do[página de download](https://releases.groupdocs.com/editor/net/).
2. Ambiente de desenvolvimento: Visual Studio ou qualquer outro ambiente de desenvolvimento .NET preferido.
3. Conhecimento básico de C#: A familiaridade com a programação C# o ajudará a acompanhar os exemplos.
4. Documento para editar: tenha um documento de amostra pronto para teste, como um documento do Word.
5. .NET Framework: certifique-se de ter o .NET Framework instalado em sua máquina.
Agora que você tem tudo pronto, vamos começar!
## Importar namespaces
Primeiro, você precisa importar os namespaces necessários em seu projeto C#. Esses namespaces fornecem as classes e os métodos necessários para trabalhar com GroupDocs.Editor for .NET.
```csharp
using System;
using GroupDocs.Editor.Options;
```
Com os namespaces importados, podemos prosseguir com a configuração do editor.
## Etapa 1: inicializar o editor
 Para começar, você precisa inicializar o`Editor`classe com seu documento. Esta etapa envolve especificar o documento que você deseja editar e fornecer as opções de carregamento necessárias.
```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
    // Outras etapas serão adicionadas aqui
}
```
 Neste exemplo, estamos carregando um documento do Word. Você pode substituir`"Your Sample Document"` com o caminho para o seu documento.
## Etapa 2: edite o documento
 A seguir, precisamos abrir o documento para edição. Isto é feito usando o`Edit` método do`Editor` aula, que exige`WordProcessingEditOptions` como argumento.
```csharp
using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
{
    // Outras etapas serão adicionadas aqui
}
```
 O`EditableDocument` instância representa o documento em um formato editável. Agora estamos prontos para recuperar o conteúdo HTML.
## Etapa 3: definir prefixos personalizados
Para adicionar prefixos personalizados para imagens e CSS, precisamos definir os prefixos como strings. Esta etapa garante que o conteúdo HTML terá os prefixos especificados para recursos externos.
```csharp
string externalImagesPrefix = "http://www.meuwebsite.com/images/id=";
string externalCssPrefix = "http://www.meusite.com/css/id=";
```
Você pode substituir os URLs pelos prefixos desejados. Esses prefixos serão usados na próxima etapa para personalizar a saída HTML.
## Etapa 4: recuperar conteúdo HTML
Agora que configuramos nossos prefixos, podemos recuperar o conteúdo HTML do documento. O`GetContent` método do`EditableDocument` class nos permite especificar a imagem e os prefixos CSS.
```csharp
string prefixedHtmlContent = document.GetContent(externalImagesPrefix, externalCssPrefix);
Console.WriteLine("HTML content of the input document with custom image and stylesheet prefixes: {0}", prefixedHtmlContent);
```
Este trecho de código busca o conteúdo HTML com os prefixos personalizados e o imprime no console. Você pode processar ou salvar ainda mais esse conteúdo HTML conforme necessário.
## Conclusão
E aí está! Seguindo essas etapas, você pode recuperar facilmente o conteúdo HTML de um documento usando GroupDocs.Editor for .NET, completo com prefixos personalizados para imagens e folhas de estilo. Essa ferramenta poderosa simplifica a manipulação de documentos, permitindo que você se concentre na integração perfeita da edição de documentos em seus aplicativos .NET.
 Para informações mais detalhadas, confira o[Documentação do GroupDocs.Editor para .NET](https://tutorials.groupdocs.com/editor/net/) . Se você tiver alguma dúvida ou precisar de mais assistência, sinta-se à vontade para entrar em contato pelo[Fórum de suporte](https://forum.groupdocs.com/c/editor/20).
## Perguntas frequentes
### Que tipos de documentos posso editar com GroupDocs.Editor for .NET?
GroupDocs.Editor suporta vários formatos de documentos, incluindo Word, Excel, PowerPoint, PDF e muito mais.
### Como faço para obter uma avaliação gratuita do GroupDocs.Editor for .NET?
 Você pode obter um teste gratuito no[Site GroupDocs](https://releases.groupdocs.com/).
### Posso personalizar ainda mais o conteúdo HTML?
Sim, você pode modificar o conteúdo HTML recuperado conforme necessário antes de renderizá-lo ou salvá-lo.
### É possível usar GroupDocs.Editor for .NET com outras linguagens .NET?
Sim, você pode usá-lo com qualquer linguagem compatível com .NET, como VB.NET ou F#.
### Como obtenho uma licença temporária do GroupDocs.Editor for .NET?
 Você pode obter uma licença temporária do[página de compra](https://purchase.groupdocs.com/temporary-license/).