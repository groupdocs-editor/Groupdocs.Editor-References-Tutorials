---
date: 2026-09-26
description: Aprenda como lidar com o prefixo CSS e extrair o conteúdo CSS usando
  o GroupDocs.Editor para .NET neste tutorial detalhado passo a passo.
keywords:
- handle css prefix
- extract css content
- edit document css
- prepend url to css
lastmod: 2026-09-26
linktitle: Manipular conteúdo CSS com prefixo
og_description: Descubra como lidar com o prefixo CSS e extrair o conteúdo CSS com
  o GroupDocs.Editor para .NET. Siga um guia passo a passo para prefixar URLs em recursos
  CSS e recuperar folhas de estilo.
og_image_alt: Developer guide showing css prefix handling with GroupDocs.Editor for
  .NET
og_title: Como lidar com o prefixo CSS no GroupDocs.Editor para .NET
schemas:
- author: GroupDocs
  dateModified: '2026-09-26'
  description: Learn how to handle css prefix and extract css content using GroupDocs.Editor
    for .NET in this detailed step‑by‑step tutorial.
  headline: How to handle css prefix in GroupDocs.Editor for .NET
  type: TechArticle
- questions:
  - answer: Yes, GroupDocs.Editor for .NET supports PDF, Word, Excel, PowerPoint,
      and many other formats.
    question: Can I use GroupDocs.Editor for .NET with other document formats?
  - answer: Absolutely! You can start your free trial on the [GroupDocs free trial
      page](https://releases.groupdocs.com/).
    question: Is there a free trial available for GroupDocs.Editor for .NET?
  - answer: You can obtain a temporary license from the [temporary license page](https://purchase.groupdocs.com/temporary-license/).
    question: How do I get a temporary license for GroupDocs.Editor for .NET?
  - answer: Detailed documentation is available on the [GroupDocs.Editor for .NET
      documentation site](https://tutorials.groupdocs.com/editor/net/).
    question: Where can I find detailed documentation for GroupDocs.Editor for .NET?
  - answer: You can get support through the [GroupDocs.Editor support forum](https://forum.groupdocs.com/c/editor/20).
    question: What support options are available for GroupDocs.Editor for .NET?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
tags:
- css handling
- GroupDocs.Editor
- .NET document processing
- css prefix
- api tutorial
title: Como lidar com o prefixo CSS no GroupDocs.Editor para .NET
type: docs
url: /pt/net/css-handling/handle-css-content-with-prefix/
weight: 11
---

# Como lidar com prefixo CSS no GroupDocs.Editor para .NET

Neste tutorial você aprenderá **como lidar com prefixo CSS** ao trabalhar com folhas de estilo dentro de um documento usando GroupDocs.Editor para .NET. Seja para adicionar um URL a imagens, fontes ou qualquer recurso externo, os passos abaixo mostram exatamente como **lidar com prefixo CSS** e também como **extrair conteúdo CSS** para processamento adicional. Ao final do guia, você será capaz de reescrever caminhos de recursos, recuperar as strings CSS brutas e integrá-las ao seu fluxo de trabalho web com confiança.

## Respostas rápidas
- **O que significa “handle css prefix”?** Adicionar um prefixo de URL personalizado aos recursos externos referenciados no CSS.  
- **Qual método da API retorna estilos CSS?** `EditableDocument.GetCssContent(...)`.  
- **Preciso de uma licença?** Uma licença de avaliação está disponível; uma licença comercial é necessária para produção.  
- **Quais versões do .NET são suportadas?** .NET Framework 4.5+ e .NET Core/5/6.  
- **Posso mudar o prefixo em tempo de execução?** Sim – basta passar uma string diferente para `GetCssContent`.

## O que é lidar com prefixo CSS?
O termo refere‑se à reescrita dos URLs de imagens, fontes ou qualquer ativo externo dentro de um arquivo CSS para que apontem para um local que você controla, como um CDN ou um servidor seguro. Ao prefixar um URL base consistente, você garante que cada recurso seja carregado corretamente quando o documento for renderizado em um navegador ou visualizador baseado na web.

## Por que usar o GroupDocs.Editor para extrair conteúdo CSS?
O GroupDocs.Editor pode ler o CSS original incorporado em documentos de processamento de texto, retornar as strings da folha de estilo bruta e permitir que você as manipule antes de renderizar ou salvar. Isso elimina a análise manual, garante fidelidade à representação interna do documento e suporta **30+ formatos de arquivo** ao processar arquivos de até **500 MB** sem carregar o arquivo inteiro na memória.

## Pré-requisitos
Antes de começarmos, certifique-se de que você tem os seguintes pré-requisitos em vigor:
- Visual Studio: Você precisará de uma instalação funcional do Visual Studio.  
- .NET Framework: Verifique se o .NET Framework está instalado.  
- GroupDocs.Editor for .NET: Você pode baixá‑lo na [página de download do GroupDocs.Editor for .NET](https://releases.groupdocs.com/editor/net/).  
- Documento de exemplo: Tenha um documento de exemplo pronto para edição.

## Importar namespaces
Primeiro, vamos importar os namespaces necessários para garantir que nosso código seja executado sem problemas. Esta etapa nos dá acesso às classes principais do GroupDocs.Editor.

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Editor.Options;
```

## Etapa 1: Inicializar o Editor
A classe `Editor` é o ponto de entrada para trabalhar com documentos no GroupDocs.Editor. Ela gerencia as operações de carregamento, edição e salvamento.  
A primeira etapa envolve criar uma instância de `Editor` com seu documento de exemplo. Isso configura o ambiente de edição.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```

## Etapa 2: Editar o documento
O objeto `EditableDocument` representa a versão editável do arquivo e expõe suas partes internas, como CSS, imagens e HTML.  
Em seguida, obtemos um objeto `EditableDocument`. Esse objeto permite que trabalhemos com o CSS interno do documento.

```csharp
    using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
    {
```

## Etapa 3: Definir prefixos externos
Defina os prefixos de URL para imagens e fontes. Esses prefixos serão adicionados a cada referência de imagem e fonte encontrada no CSS.

```csharp
        string externalImagesPrefix = "http://www.mywebsite.com/images/id=";
        string externalFontsPrefix = "http://www.mywebsite.com/fonts/id=";
```

## Etapa 4: Extrair conteúdo CSS com os prefixos
`GetCssContent` retorna uma coleção de strings de folhas de estilo CSS que já contêm os URLs prefixados que você forneceu.  
Chame `GetCssContent`, passando os prefixos que você acabou de definir. O método retorna uma lista de strings de folhas de estilo CSS que já contêm os URLs prefixados.

```csharp
        List<string> stylesheets = document.GetCssContent(externalImagesPrefix, externalFontsPrefix);
```

## Etapa 5: Exibir os resultados
Imprima o número de folhas de estilo encontradas e exiba cada folha de estilo. Isso ajuda a verificar se os prefixos foram aplicados corretamente.

```csharp
        Console.WriteLine("There are {0} stylesheets in the input document", stylesheets.Count);
        foreach (string css in stylesheets)
        {
            Console.WriteLine(css);
        }
    }
}
```

## Problemas comuns e soluções
- **Nenhuma folha de estilo retornada** – Certifique-se de que o documento de origem realmente contém CSS (por exemplo, um documento Word com tabelas estilizadas ou HTML incorporado).  
- **URLs incorretos** – Verifique se as strings de prefixo terminam com o delimitador apropriado (`/` ou `=`) para o roteamento do seu servidor.  
- **Preocupações de desempenho** – Para documentos muito grandes, considere processar as folhas de estilo em lotes para evitar alto uso de memória.

## Perguntas frequentes

**Q: Posso usar o GroupDocs.Editor para .NET com outros formatos de documento?**  
A: Sim, o GroupDocs.Editor para .NET suporta PDF, Word, Excel, PowerPoint e muitos outros formatos.

**Q: Existe uma versão de avaliação gratuita disponível para o GroupDocs.Editor para .NET?**  
A: Absolutamente! Você pode iniciar sua avaliação gratuita na [página de avaliação gratuita do GroupDocs](https://releases.groupdocs.com/).

**Q: Como obtenho uma licença temporária para o GroupDocs.Editor para .NET?**  
A: Você pode obter uma licença temporária na [página de licença temporária](https://purchase.groupdocs.com/temporary-license/).

**Q: Onde posso encontrar documentação detalhada para o GroupDocs.Editor para .NET?**  
A: Documentação detalhada está disponível no [site de documentação do GroupDocs.Editor para .NET](https://tutorials.groupdocs.com/editor/net/).

**Q: Quais opções de suporte estão disponíveis para o GroupDocs.Editor para .NET?**  
A: Você pode obter suporte através do [fórum de suporte do GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).

## Perguntas frequentes adicionais

**Q: Posso mudar o prefixo após extrair o CSS?**  
A: Sim. Chame `GetCssContent` novamente com uma string de prefixo diferente; o método sempre usa os valores que você passa em tempo de execução.

**Q: Isso funciona com documentos protegidos por senha?**  
A: Sim. Forneça a senha em `WordProcessingLoadOptions` ao criar a instância `Editor`.

**Q: É possível salvar o CSS modificado de volta no documento?**  
A: O GroupDocs.Editor atualmente fornece acesso somente leitura ao CSS. Para persistir as alterações, você precisaria substituir a folha de estilo original usando as APIs XML subjacentes do documento.

---

**Última atualização:** 2026-09-26  
**Testado com:** GroupDocs.Editor 23.12 para .NET  
**Autor:** GroupDocs

## Tutoriais relacionados

- [Extrair CSS externo de documentos Word usando GroupDocs.Editor .NET: Um Guia Abrangente](/editor/net/html-web-documents/extract-external-css-word-docs-groupdocs-editor-dotnet/)
- [Extrair e Prefixar HTML de documentos Word usando GroupDocs.Editor .NET](/editor/net/html-web-documents/groupdocs-editor-dotnet-extract-prefix-html-word-docs/)
- [Como extrair e modificar conteúdo HTML em documentos Word usando GroupDocs.Editor .NET](/editor/net/html-web-documents/extract-modify-html-content-word-docs-groupdocs-editor-net/)