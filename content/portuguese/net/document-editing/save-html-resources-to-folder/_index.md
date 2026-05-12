---
date: 2026-05-12
description: Aprenda a extrair fontes e outros recursos HTML de documentos usando
  o GroupDocs.Editor para .NET. Guia passo a passo para desenvolvedores .NET.
keywords:
- how to extract fonts
- GroupDocs.Editor .NET
- extract HTML resources
linktitle: Salvar recursos HTML em pasta
schemas:
- author: GroupDocs
  dateModified: '2026-05-12'
  description: Learn how to extract fonts and other HTML resources from documents
    using GroupDocs.Editor for .NET. Step‑by‑step guide for .NET developers.
  headline: How to Extract Fonts and Save HTML Resources to Folder
  type: TechArticle
- description: Learn how to extract fonts and other HTML resources from documents
    using GroupDocs.Editor for .NET. Step‑by‑step guide for .NET developers.
  name: How to Extract Fonts and Save HTML Resources to Folder
  steps:
  - name: '**Basic Knowledge of C# and .NET** – Familiarity with C# programming language
      and .NET framework is essential to follow along with the examples.'
    text: '**Basic Knowledge of C# and .NET** – Familiarity with C# programming language
      and .NET framework is essential to follow along with the examples.'
  - name: '**GroupDocs.Editor for .NET Library** – Download and install GroupDocs.Editor
      for .NET library from the [website](https://releases.groupdocs.com/editor/net/).'
    text: '**GroupDocs.Editor for .NET Library** – Download and install GroupDocs.Editor
      for .NET library from the [website](https://releases.groupdocs.com/editor/net/).'
  - name: '**Development Environment** – Set up your preferred development environment
      such as Visual Studio or any other compatible IDE.'
    text: '**Development Environment** – Set up your preferred development environment
      such as Visual Studio or any other compatible IDE.'
  type: HowTo
- questions:
  - answer: Yes, it supports Excel, PowerPoint, PDF, HTML, and over 50 additional
      formats for both editing and resource extraction.
    question: Is GroupDocs.Editor compatible with other document formats besides Word?
  - answer: Absolutely. The API works seamlessly with ASP.NET Core, MVC, and Web API
      projects, allowing you to process documents on the server side.
    question: Can I integrate GroupDocs.Editor into a web application?
  - answer: Yes, it includes built‑in connectors for Google Drive, Dropbox, OneDrive,
      and Amazon S3, enabling direct loading and saving of documents in the cloud.
    question: Does GroupDocs.Editor provide cloud storage integration?
  - answer: A fully functional 30‑day trial can be downloaded from the GroupDocs website
      without any credit‑card requirement.
    question: Is there a free trial available for GroupDocs.Editor?
  - answer: You can reach the GroupDocs support team via the official forum, submit
      a ticket through the customer portal, or consult the detailed API documentation.
    question: How can I get technical support for extraction issues?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Como extrair fontes e salvar recursos HTML em pasta
type: docs
url: /pt/net/document-editing/save-html-resources-to-folder/
weight: 13
---

# Como Extrair Fontes e Salvar Recursos HTML em Pasta

## Introdução
GroupDocs.Editor for .NET permite que você **como extrair fontes** e outros recursos de um documento ao convertê-lo para HTML. Em algumas linhas de C# você pode extrair imagens, folhas de estilo e arquivos de fontes, e então armazená-los em uma pasta de sua escolha. Este tutorial orienta você por todo o fluxo de trabalho, desde a inicialização do editor até a gravação de cada recurso no disco.

## Respostas Rápidas
- **O que significa “como extrair fontes”?** É o processo de recuperar arquivos de fontes incorporados de um documento fonte durante a conversão para HTML.  
- **Qual biblioteca lida com isso?** GroupDocs.Editor for .NET fornece uma API dedicada para extrair fontes, imagens e folhas de estilo.  
- **Preciso de uma licença?** Um teste gratuito está disponível; uma licença comercial é necessária para uso em produção.  
- **Quais versões do .NET são suportadas?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.  
- **Posso direcionar para uma pasta personalizada?** Sim, você especifica qualquer caminho gravável ao salvar os recursos extraídos.

## O que é “como extrair fontes”?
**Como extrair fontes** refere‑se à recuperação dos arquivos de fontes originais incorporados em um documento fonte (por exemplo, DOCX, PPTX) para que possam ser referenciados pelo HTML gerado. Isso garante que o texto seja renderizado exatamente como pretendido nos navegadores, sem depender de fontes do sistema.

## Por que usar o GroupDocs.Editor para extração de recursos HTML?
GroupDocs.Editor suporta **mais de 50 formatos de entrada e saída** — incluindo DOCX, PPTX, PDF e HTML — e pode processar documentos com **até 300 páginas** sem carregar o arquivo inteiro na memória. Sua API extrai fontes, imagens e CSS em uma única passagem, reduzindo o tempo de desenvolvimento em até **70 %** comparado ao parsing manual.

## Pré‑requisitos
Antes de mergulhar no tutorial, certifique‑se de que você possui os seguintes pré‑requisitos:
1. **Conhecimento básico de C# e .NET** – Familiaridade com a linguagem de programação C# e o framework .NET é essencial para acompanhar os exemplos.  
2. **Biblioteca GroupDocs.Editor for .NET** – Baixe e instale a biblioteca GroupDocs.Editor for .NET a partir do [site](https://releases.groupdocs.com/editor/net/).  
3. **Ambiente de desenvolvimento** – Configure seu ambiente de desenvolvimento preferido, como Visual Studio ou qualquer outra IDE compatível.

## Importar Namespaces
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

## Como extrair fontes e salvar recursos HTML em uma pasta?
Carregue seu documento fonte com `Editor editor = new Editor("sample.docx", new WordProcessingLoadOptions());` e então chame `editor.Save("output.html", SaveOptions.Html);`. Após a operação de salvamento, a coleção `Resources` contém todos os recursos extraídos — incluindo fontes — que você pode percorrer e gravar no disco. Essa abordagem de passo único lida automaticamente tanto com a conversão quanto com a extração de recursos.

## Etapa 1: Inicializar o GroupDocs.Editor
`Editor` é a classe central que orquestra o carregamento, a conversão e a extração de recursos do documento. Ela representa uma única sessão de documento na memória.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```
Primeiro, inicialize o objeto `Editor` fornecendo o caminho para seu documento de exemplo. Neste exemplo, estamos usando um documento Word, portanto especificamos `WordProcessingLoadOptions` como o tipo de documento.

## Etapa 2: Editar Documento
`EditableDocument` é a representação editável retornada pelo método `Edit`, permitindo que você manipule o documento antes de salvá‑lo.

```csharp
	using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
	{
```
Em seguida, crie um objeto `EditableDocument` chamando o método `Edit` do objeto `Editor`. Isso permite que você execute operações de edição no documento.

## Etapa 3: Extrair Recursos
`Resources` é uma coleção que agrupa os recursos extraídos — imagens, fontes e folhas de estilo — em listas separadas para fácil manipulação.

```csharp
		List<IImageResource> images = document.Images;
		List<FontResourceBase> fonts = document.Fonts;
		List<CssText> stylesheets = document.Css;
```
Extraia recursos como imagens, fontes e folhas de estilo do documento e armazene‑os nas listas correspondentes.

## Etapa 4: Especificar Pasta de Saída
`outputFolder` é uma string que define onde os arquivos extraídos serão gravados. Você pode apontá‑la para qualquer diretório gravável no servidor ou na máquina local.

```csharp
		string outputFolder = Constants.GetOutputDirectoryPath("Your Sample Document");
```
Defina a pasta de saída onde os recursos extraídos serão salvos. Você pode personalizar o caminho da pasta conforme sua necessidade.

## Etapa 5: Salvar Recursos
`SaveResource` é uma rotina auxiliar que grava um único recurso binário (imagem, fonte ou folha de estilo) no sistema de arquivos.

```csharp
		foreach (IImageResource oneImage in images)
		{
			Console.WriteLine("Saving {0} of {1} type and {2} dimensions",
				oneImage.FilenameWithExtension, oneImage.Type.FormalName, oneImage.LinearDimensions);
			oneImage.Save(Path.Combine(outputFolder, oneImage.FilenameWithExtension));
		}
```
Percorra cada recurso de imagem, salve‑o na pasta de saída e exiba informações relevantes como nome do arquivo, tipo e dimensões.

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
Finalmente, salve cada folha de estilo na pasta de saída e conclua o processo de edição.

## Problemas Comuns e Soluções
- **Fontes ausentes após a conversão** – Certifique‑se de que o documento fonte realmente incorpora as fontes; caso contrário, o GroupDocs.Editor só pode referenciar fontes do sistema.  
- **Erros de acesso negado** – Verifique se o processo da aplicação tem permissões de gravação na pasta de saída alvo.  
- **Documentos grandes causam alto uso de memória** – Use `LoadOptions` com `LoadMode = LoadMode.Stream` para transmitir arquivos grandes em vez de carregá‑los totalmente na memória.

## Perguntas Frequentes

**Q: O GroupDocs.Editor é compatível com outros formatos de documento além do Word?**  
A: Sim, ele suporta Excel, PowerPoint, PDF, HTML e mais de 50 formatos adicionais tanto para edição quanto para extração de recursos.

**Q: Posso integrar o GroupDocs.Editor em uma aplicação web?**  
A: Absolutamente. A API funciona perfeitamente com projetos ASP.NET Core, MVC e Web API, permitindo processar documentos no lado do servidor.

**Q: O GroupDocs.Editor oferece integração com armazenamento em nuvem?**  
A: Sim, inclui conectores integrados para Google Drive, Dropbox, OneDrive e Amazon S3, permitindo o carregamento e salvamento direto de documentos na nuvem.

**Q: Existe um teste gratuito disponível para o GroupDocs.Editor?**  
A: Um teste totalmente funcional de 30 dias pode ser baixado no site da GroupDocs sem necessidade de cartão de crédito.

**Q: Como posso obter suporte técnico para problemas de extração?**  
A: Você pode entrar em contato com a equipe de suporte da GroupDocs através do fórum oficial, enviar um ticket pelo portal do cliente ou consultar a documentação detalhada da API.

---

**Última atualização:** 2026-05-12  
**Testado com:** GroupDocs.Editor 23.11 for .NET  
**Autor:** GroupDocs

## Tutoriais Relacionados

- [Edição Eficiente de Documentos com GroupDocs.Editor .NET: Transformar HTML em Documentos Editáveis](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)
- [Extrair e Salvar Recursos DOCX com Eficiência Usando GroupDocs.Editor .NET - Guia Completo](/editor/net/document-saving/efficient-extract-save-docx-resources-groupdocs-editor-net/)
- [Dominar a Edição e Conversão de Documentos com GroupDocs.Editor .NET: Um Guia Completo](/editor/net/document-editing/groupdocs-editor-net-mastering-document-editing/)