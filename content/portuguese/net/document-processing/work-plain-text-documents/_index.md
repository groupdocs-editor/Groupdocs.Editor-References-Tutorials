---
date: 2026-08-10
description: Aprenda a editar arquivos de plain text usando GroupDocs.Editor for .NET.
  O guia aborda como carregar um arquivo txt, remover espaços, definir text encoding
  e salvar o resultado.
keywords:
- edit plain text
- load txt file
- trim trailing spaces
- convert leading spaces
- set text encoding
lastmod: 2026-08-10
linktitle: Trabalhar com documentos de Plain Text
og_description: Aprenda a editar arquivos de plain text usando GroupDocs.Editor for
  .NET – carregue um arquivo txt, remova espaços finais, converta espaços iniciais,
  defina text encoding e salve de forma eficiente.
og_image_alt: Guide showing edit plain text workflow with GroupDocs.Editor for .NET
og_title: Edite documentos de plain text com GroupDocs.Editor for .NET
schemas:
- author: GroupDocs
  dateModified: '2026-08-10'
  description: Learn how to edit plain text files using GroupDocs.Editor for .NET.
    The guide covers loading a txt file, trimming spaces, setting text encoding, and
    saving the result.
  headline: Edit plain text documents with GroupDocs.Editor for .NET
  type: TechArticle
- description: Learn how to edit plain text files using GroupDocs.Editor for .NET.
    The guide covers loading a txt file, trimming spaces, setting text encoding, and
    saving the result.
  name: Edit plain text documents with GroupDocs.Editor for .NET
  steps:
  - name: Get a path to the input TXT file
    text: First, decide whether you’ll work with a physical file path or a memory
      stream. Using a path is the most straightforward approach for local development.
  - name: Create an Editor instance
    text: '`Editor` is the main class that loads a document and provides editing capabilities.'
  - name: Create TXT editing options
    text: '`TxtEditOptions` configures how plain‑text files are parsed and edited,
      allowing you to set encoding and space‑handling rules.'
  - name: Create an EditableDocument instance
    text: '`EditableDocument` represents the in‑memory version of the loaded document,
      including its text and any associated resources.'
  - name: Edit the document content
    text: Retrieve the original text, apply any string operations you need (e.g.,
      replace, trim, change case), and store the result back into the `EditableDocument`.
  - name: Create an EditableDocument with updated content
    text: After you’ve transformed the text, instantiate a new `EditableDocument`
      that contains the edited string and the original resource collection.
  - name: Create WordProcessing save options
    text: '`WordProcessingSaveOptions` defines settings for saving the document in
      a Word‑compatible format such as DOCX or DOCM.'
  - name: Create TXT saving options
    text: '`TxtSaveOptions` specifies how the edited plain‑text file should be written,
      including encoding, line‑ending preservation, and table layout handling.'
  - name: Prepare output paths
    text: Derive the output directory from the input file path, then build the full
      filenames for the DOCX and TXT results.
  - name: Save the edited document
    text: Finally, call `editor.Save` twice—once with the WordProcessing options and
      once with the TXT options—to produce both formats in a single operation.
  type: HowTo
- questions:
  - answer: The library supports 50+ formats, including DOCX, TXT, HTML, PDF, and
      markdown, allowing you to edit and convert between them seamlessly.
    question: What file formats does GroupDocs.Editor for .NET support?
  - answer: Download the trial from the [releases page](https://releases.groupdocs.com/).
    question: How can I get a free trial of GroupDocs.Editor for .NET?
  - answer: Yes, temporary licenses are available through the [GroupDocs purchase
      page](https://purchase.groupdocs.com/temporary-license/).
    question: Can I purchase a temporary license for testing?
  - answer: The official support forum is the best place – visit the [GroupDocs.Editor
      support forum](https://forum.groupdocs.com/c/editor/20).
    question: Where can I find support if I run into issues?
  - answer: Absolutely. The full reference is on the [GroupDocs.Editor documentation
      page](https://tutorials.groupdocs.com/editor/net/).
    question: Is there detailed documentation for advanced scenarios?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
tags:
- edit plain text
- GroupDocs.Editor
- C# document processing
- plain text editing
- txt file handling
title: Edite documentos de plain text com GroupDocs.Editor for .NET
type: docs
url: /pt/net/document-processing/work-plain-text-documents/
weight: 15
---

# Editar documentos de texto simples com GroupDocs.Editor para .NET

## Introdução
Se você precisa **editar texto simples** rápida e confiavelmente em uma aplicação .NET, o GroupDocs.Editor para .NET é a ferramenta que faz o trabalho pesado. Esta API suporta mais de 30 formatos de documento, pode lidar com arquivos de até 500 MB e permite manipular texto sem carregar o arquivo inteiro na memória. Neste tutorial você aprenderá como carregar um arquivo txt, remover espaços finais, converter espaços iniciais, definir a codificação correta e, finalmente, salvar o conteúdo editado de volta ao disco. Pronto para colocar a mão na massa? Vamos mergulhar!

## Respostas rápidas
- **Qual é o primeiro passo para editar um arquivo txt?** Carregue o arquivo com `Editor` usando o caminho ou stream que você tem.  
- **Posso mudar a codificação do arquivo enquanto edito?** Sim – o `TxtSaveOptions` permite especificar UTF‑8, UTF‑16 ou qualquer codificação personalizada.  
- **Como removo espaços extras no final de cada linha?** Recupere o texto, chame `TrimEnd()` em cada linha e escreva‑o de volta.  
- **O GroupDocs.Editor é gratuito para teste?** Um teste totalmente funcional de 30 dias está disponível na página de lançamentos.  
- **Quais versões do .NET são suportadas?** .NET Framework 4.6+, .NET Core 3.1+ e .NET 5/6/7.

## O que é editar texto simples?
**Editar texto simples** significa alterar programaticamente os caracteres dentro de um arquivo `.txt` simples — adicionando, removendo ou reformatando texto — enquanto preserva a codificação original do arquivo e o estilo de quebra de linha. Pode envolver tarefas como remover espaços em branco, normalizar quebras de linha, atualizar valores de configuração ou inserir conteúdo gerado. A operação deve manter o arquivo legível por qualquer editor de texto padrão e manter quaisquer metadados existentes, como marcadores BOM.

## Por que usar o GroupDocs.Editor para edição de texto simples?
O GroupDocs.Editor processa arquivos de forma streaming, o que significa que pode editar um arquivo de log de 300 MB usando menos de 50 MB de RAM. A biblioteca suporta **mais de 50 formatos de entrada e saída**, detecta automaticamente estilos de quebra de linha (CR, LF, CRLF) e fornece opções integradas para **remover espaços finais** e **converter espaços iniciais** sem a necessidade de escrever analisadores personalizados.

## Pré-requisitos
- **Ambiente de desenvolvimento .NET** – Visual Studio 2022 ou VS Code com a extensão C#.  
- **GroupDocs.Editor para .NET** – faça o download na página de lançamentos do [GroupDocs.Editor for .NET](https://releases.groupdocs.com/editor/net/) releases page.  
- **Conhecimento básico de C#** – você deve estar confortável com I/O de arquivos e manipulação de strings.  
- **Editor de texto (opcional)** – para inspecionar os arquivos fonte; VS Code é recomendado.  
- Para uso detalhado, veja a [documentação](https://tutorials.groupdocs.com/editor/net/).  
- Você também pode navegar na [página de lançamentos](https://releases.groupdocs.com/).

## Como editar texto simples passo a passo
Carregue o arquivo, edite seu conteúdo e salve‑o de volta – tudo em menos de dez linhas de código. As seções a seguir guiam você por cada etapa com explicações claras.

### Etapa 1: Obter um caminho para o arquivo TXT de entrada
Primeiro, decida se você trabalhará com um caminho de arquivo físico ou um stream de memória. Usar um caminho é a abordagem mais direta para desenvolvimento local.

```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

### Etapa 2: Criar uma instância do Editor
`Editor` é a classe principal que carrega um documento e fornece recursos de edição.

```csharp
string inputFilePath = "YourSampleDocument.txt";
```

### Etapa 3: Criar opções de edição TXT
`TxtEditOptions` configura como arquivos de texto simples são analisados e editados, permitindo definir a codificação e as regras de tratamento de espaços.

```csharp
using (Editor editor = new Editor(inputFilePath))
{
```

### Etapa 4: Criar uma instância de EditableDocument
`EditableDocument` representa a versão em memória do documento carregado, incluindo seu texto e quaisquer recursos associados.

```csharp
    TextEditOptions editOptions = new TextEditOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        RecognizeLists = true,
        LeadingSpaces = TextLeadingSpacesOptions.ConvertToIndent,
        TrailingSpaces = TextTrailingSpacesOptions.Trim
    };
```

### Etapa 5: Editar o conteúdo do documento
Recupere o texto original, aplique quaisquer operações de string necessárias (por exemplo, substituir, remover espaços, mudar maiúsculas/minúsculas) e armazene o resultado de volta no `EditableDocument`.

```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```

### Etapa 6: Criar um EditableDocument com conteúdo atualizado
Depois de transformar o texto, instancie um novo `EditableDocument` que contém a string editada e a coleção de recursos original.

```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("text", "EDITED text");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```

### Etapa 7: Criar opções de salvamento WordProcessing
`WordProcessingSaveOptions` define as configurações para salvar o documento em um formato compatível com Word, como DOCX ou DOCM.

```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```

### Etapa 8: Criar opções de salvamento TXT
`TxtSaveOptions` especifica como o arquivo de texto simples editado deve ser escrito, incluindo codificação, preservação de quebras de linha e tratamento de layout de tabelas.

```csharp
    WordProcessingSaveOptions wordSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm)
    {
        Locale = System.Globalization.CultureInfo.GetCultureInfo("en-GB")
    };
```

### Etapa 9: Preparar caminhos de saída
Derive o diretório de saída a partir do caminho do arquivo de entrada, então construa os nomes completos dos arquivos para os resultados DOCX e TXT.

```csharp
    TextSaveOptions txtSaveOptions = new TextSaveOptions
    {
        Encoding = System.Text.Encoding.UTF8,
        PreserveTableLayout = true
    };
```

### Etapa 10: Salvar o documento editado
Finalmente, chame `editor.Save` duas vezes — uma vez com as opções WordProcessing e outra com as opções TXT — para gerar ambos os formatos em uma única operação.

```csharp
    string outputWordPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".docm");
    string outputTxtPath = Path.Combine(Path.GetDirectoryName(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".txt");
```

## Problemas comuns e soluções
- **Espaços finais permanecem após a edição** – certifique‑se de que `TxtEditOptions.TrimTrailingSpaces` esteja definido como `true` antes de carregar o documento.  
- **Codificação incorreta no arquivo salvo** – verifique se `TxtSaveOptions.Encoding` corresponde à página de código desejada (por exemplo, `Encoding.UTF8`).  
- **Arquivos grandes causam OutOfMemoryException** – use a API de streaming (`Editor.Load(Stream)`) em vez de carregar a partir de um caminho de arquivo para manter o uso de memória baixo.  

## Perguntas frequentes

**Q: Quais formatos de arquivo o GroupDocs.Editor para .NET suporta?**  
A: A biblioteca suporta mais de 50 formatos, incluindo DOCX, TXT, HTML, PDF e markdown, permitindo editar e converter entre eles de forma contínua.

**Q: Como posso obter um teste gratuito do GroupDocs.Editor para .NET?**  
A: Baixe o teste na [página de lançamentos](https://releases.groupdocs.com/).

**Q: Posso comprar uma licença temporária para teste?**  
A: Sim, licenças temporárias estão disponíveis através da [página de compra do GroupDocs](https://purchase.groupdocs.com/temporary-license/).

**Q: Onde posso encontrar suporte se eu encontrar problemas?**  
A: O fórum oficial de suporte é o melhor lugar – visite o [fórum de suporte do GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).

**Q: Existe documentação detalhada para cenários avançados?**  
A: Absolutamente. A referência completa está na [página de documentação do GroupDocs.Editor](https://tutorials.groupdocs.com/editor/net/).

## Conclusão
Você agora domina como **editar texto simples** usando o GroupDocs.Editor para .NET — carregando um arquivo txt, removendo espaços, convertendo espaços iniciais, definindo a codificação correta e salvando o resultado em formatos TXT e DOCX. Essa capacidade permite automatizar a limpeza de arquivos de log, gerar arquivos de configuração on‑the‑fly ou construir pipelines personalizados de processamento de texto sem reinventar a roda. Explore recursos adicionais como processamento em lote e conversão de documentos visitando a documentação oficial.

---

**Last Updated:** 2026-08-10  
**Tested With:** GroupDocs.Editor 23.11 for .NET  
**Author:** GroupDocs  

---

```csharp
    editor.Save(afterEdit, outputWordPath, wordSaveOptions);
    editor.Save(afterEdit, outputTxtPath, txtSaveOptions);
}
System.Console.WriteLine("Document editing process completed successfully!");
```

## Tutoriais Relacionados

- [Document Loading Tutorials with GroupDocs.Editor for .NET](/editor/net/document-loading/)
- [Document Saving and Export Tutorials for GroupDocs.Editor .NET](/editor/net/document-saving/)
- [Plain Text and DSV Document Editing Tutorials for GroupDocs.Editor .NET](/editor/net/plain-text-dsv-documents/)