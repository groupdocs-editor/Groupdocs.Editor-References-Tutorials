---
title: Salvar recursos HTML na pasta
linktitle: Salvar recursos HTML na pasta
second_title: API GroupDocs.Editor .NET
description: Aprenda como extrair recursos HTML de documentos usando Groupdocs.Editor for .NET. Este tutorial abrangente fornece orientação passo a passo para desenvolvedores.
weight: 13
url: /pt/net/document-editing/save-html-resources-to-folder/
type: docs
---
# Salvar recursos HTML na pasta

## Introdução
Groupdocs.Editor for .NET é uma ferramenta poderosa que permite aos desenvolvedores manipular e converter documentos em seus aplicativos .NET de maneira integrada. Se você precisa extrair recursos HTML de um documento ou realizar tarefas avançadas de edição, o Groupdocs.Editor simplifica o processo com sua API intuitiva e extensa documentação.
## Pré-requisitos
Antes de mergulhar no tutorial, certifique-se de ter os seguintes pré-requisitos:
1. Conhecimento básico de C# e .NET: Familiaridade com a linguagem de programação C# e o framework .NET é essencial para acompanhar os exemplos.
2.  Biblioteca Groupdocs.Editor for .NET: Baixe e instale a biblioteca Groupdocs.Editor for .NET do[local na rede Internet](https://releases.groupdocs.com/editor/net/).
3. Ambiente de desenvolvimento: Configure seu ambiente de desenvolvimento preferido, como Visual Studio ou qualquer outro IDE compatível.

## Importar namespaces
Para começar, importe os namespaces necessários em seu projeto C#:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.HtmlCss.Resources.Fonts;
using GroupDocs.Editor.HtmlCss.Resources.Images;
using GroupDocs.Editor.HtmlCss.Resources.Textual;
using GroupDocs.Editor.Options;
```
##Agora, vamos dividir o processo de salvar recursos HTML em uma pasta usando Groupdocs.Editor for .NET em várias etapas:
## Etapa 1: inicializar Groupdocs.Editor
```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```
 Primeiro, inicialize o`Editor`objeto fornecendo o caminho para seu documento de amostra. Neste exemplo, estamos usando um documento do Word, então especificamos`WordProcessingLoadOptions` como o tipo de documento.
## Etapa 2: editar o documento
```csharp
	using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
	{
```
 A seguir, crie um`EditableDocument` objeto chamando o`Edit` método do`Editor` objeto. Isso permite realizar operações de edição no documento.
## Etapa 3: extrair recursos
```csharp
		List<IImageResource> images = document.Images;
		List<FontResourceBase> fonts = document.Fonts;
		List<CssText> stylesheets = document.Css;
```
Extraia recursos como imagens, fontes e folhas de estilo do documento e armazene-os nas respectivas listas.
## Etapa 4: especificar a pasta de saída
```csharp
		string outputFolder = Constants.GetOutputDirectoryPath("Your Sample Document");
```
Defina a pasta de saída onde os recursos extraídos serão salvos. Você pode personalizar o caminho da pasta conforme sua necessidade.
## Etapa 5: Economize recursos
```csharp
		foreach (IImageResource oneImage in images)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} dimensions",
				oneImage.FilenameWithExtension, oneImage.Type.FormalName, oneImage.LinearDimensions);
			oneImage.Save(Path.Combine(outputFolder, oneImage.FilenameWithExtension));
		}
```
Percorra cada recurso de imagem, salve-o na pasta de saída e exiba informações relevantes, como nome do arquivo, tipo e dimensões.
```csharp
		foreach (FontResourceBase oneFont in fonts)
		{
			Console.WriteLine("Saving {0} of {1} type",
				oneFont.FilenameWithExtension, oneFont.Type.FormalName);
			oneFont.Save(Path.Combine(outputFolder, oneFont.FilenameWithExtension));
		}
```
Da mesma forma, salve cada recurso de fonte na pasta de saída.
```csharp
		foreach (CssText oneStylesheet in stylesheets)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} encoding",
				oneStylesheet.FilenameWithExtension, oneStylesheet.Type.FormalName, oneStylesheet.Encoding);
			oneStylesheet.Save(Path.Combine(outputFolder, oneStylesheet.FilenameWithExtension));
		}
	}
}
```
Por fim, salve cada folha de estilo na pasta de saída e conclua o processo de edição.

## Conclusão
Concluindo, Groupdocs.Editor for .NET fornece uma solução conveniente para gerenciar e manipular documentos programaticamente em aplicativos .NET. Seguindo este tutorial, você pode extrair facilmente recursos HTML de documentos e personalizar o processo de acordo com seus requisitos específicos.
## Perguntas frequentes
### O Groupdocs.Editor é compatível com outros formatos de documento além do Word?
Sim, o Groupdocs.Editor oferece suporte a uma ampla variedade de formatos de documentos, incluindo Excel, PowerPoint, PDF e muito mais.
### Posso integrar Groupdocs.Editor em meu aplicativo web?
Com certeza, Groupdocs.Editor oferece integração perfeita com aplicativos web desenvolvidos no framework .NET.
### O Groupdocs.Editor oferece suporte para serviços de armazenamento em nuvem?
Sim, Groupdocs.Editor oferece suporte à integração com serviços populares de armazenamento em nuvem, como Google Drive, Dropbox e Microsoft OneDrive.
### Existe um teste gratuito disponível para Groupdocs.Editor?
Sim, você pode aproveitar uma avaliação gratuita do Groupdocs.Editor no site.
### Como posso obter suporte técnico para Groupdocs.Editor?
Para assistência técnica e suporte da comunidade, você pode visitar o fórum Groupdocs.Editor.