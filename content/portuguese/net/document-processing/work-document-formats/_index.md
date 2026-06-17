---
date: 2026-06-06
description: Aprenda como listar os formatos de documento suportados e determinar
  a extensão do formato de arquivo usando o GroupDocs.Editor para .NET. Guia passo
  a passo com trechos de código, respostas rápidas e perguntas frequentes.
keywords:
- list supported document formats
- determine file format extension
- GroupDocs.Editor .NET
- document editing API
- supported formats guide
linktitle: Listar formatos de documento suportados
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to list supported document formats and determine file format
    extension using GroupDocs.Editor for .NET. Step‑by‑step guide with code snippets,
    quick answers, and FAQs.
  headline: List Supported Document Formats with GroupDocs.Editor .NET
  type: TechArticle
- description: Learn how to list supported document formats and determine file format
    extension using GroupDocs.Editor for .NET. Step‑by‑step guide with code snippets,
    quick answers, and FAQs.
  name: List Supported Document Formats with GroupDocs.Editor .NET
  steps:
  - name: '**.NET development environment** – Visual Studio 2022 or any IDE that supports
      .NET 6+.'
    text: '**.NET development environment** – Visual Studio 2022 or any IDE that supports
      .NET 6+.'
  - name: '**GroupDocs.Editor for .NET library** – download from the [GroupDocs releases
      page](https://releases.groupdocs.com/editor/net/).'
    text: '**GroupDocs.Editor for .NET library** – download from the [GroupDocs releases
      page](https://releases.groupdocs.com/editor/net/).'
  - name: '**Temporary license** – obtain a [temporary license](https://purchase.groupdocs.com/temporary-license/)
      for unrestricted access.'
    text: '**Temporary license** – obtain a [temporary license](https://purchase.groupdocs.com/temporary-license/)
      for unrestricted access.'
  - name: '**Basic C# knowledge** – familiarity with namespaces, `using` statements,
      and console output.'
    text: '**Basic C# knowledge** – familiarity with namespaces, `using` statements,
      and console output.'
  - name: '**Loop Through Formats:** We iterate over all available Word‑processing
      formats.'
    text: '**Loop Through Formats:** We iterate over all available Word‑processing
      formats.'
  - name: '**Output Format Details:** For each format we print its friendly name and
      default file extension.'
    text: '**Output Format Details:** For each format we print its friendly name and
      default file extension.'
  - name: '**Loop Through Formats:** The same looping logic applies to presentations.'
    text: '**Loop Through Formats:** The same looping logic applies to presentations.'
  - name: '**Output Format Details:** The name and extension are displayed for each
      format.'
    text: '**Output Format Details:** The name and extension are displayed for each
      format.'
  - name: '**Parse Format:** `FromExtension` converts the `.xlsm` extension into its
      internal `SpreadsheetFormat` enum.'
    text: '**Parse Format:** `FromExtension` converts the `.xlsm` extension into its
      internal `SpreadsheetFormat` enum.'
  - name: '**Output Format:** The parsed format’s name is printed, confirming the
      mapping.'
    text: '**Output Format:** The parsed format’s name is printed, confirming the
      mapping.'
  type: HowTo
- questions:
  - answer: '`DocumentFormatInfo` provides metadata about supported file types, while
      `SaveOptions` configures how a document is written back to disk (format, compression,
      etc.).'
    question: What is the difference between `DocumentFormatInfo` and `SaveOptions`?
  - answer: Yes—use `DocumentFormatInfo.FromExtension("yourExt")`; if the extension
      isn’t recognized, the method returns `null`.
    question: Can I list formats for a custom file extension?
  - answer: Absolutely. Pass the password to the `Editor` constructor via `EditorSettings`
      to open encrypted documents.
    question: Does GroupDocs.Editor support password‑protected files?
  - answer: Over **30 input and output formats**, spanning Word, Excel, PowerPoint,
      HTML, and plain text.
    question: How many formats does GroupDocs.Editor actually support?
  - answer: Use the `GetEditableWordProcessingFormats()` (or Spreadsheet/Presentation
      equivalents) to retrieve formats that allow full edit capabilities.
    question: Is there a way to restrict the list to only editable formats?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Listar formatos de documento suportados com GroupDocs.Editor .NET
type: docs
url: /pt/net/document-processing/work-document-formats/
weight: 13
---

# Lista de Formatos de Documento Suportados

Bem‑vindo ao nosso tutorial abrangente sobre **como listar formatos de documento suportados** com o GroupDocs.Editor para .NET. Seja você desenvolvendo um aplicativo web centrado em documentos ou uma ferramenta desktop de nível empresarial, saber exatamente quais formatos você pode editar ou converter é essencial. Neste guia, você descobrirá como enumerar formatos, analisar extensões e editar documentos — tudo com explicações claras e amigáveis e trechos de código prontos para execução.

## Respostas Rápidas
- **Como listar todos os formatos suportados?** Use `DocumentFormatInfo.GetSupportedWordProcessingFormats()` (ou os equivalentes para Presentation/Spreadsheet) e itere a coleção.  
- **Posso determinar um formato a partir de uma extensão de arquivo?** Sim — chame `DocumentFormatInfo.FromExtension(".docx")`.  
- **Quais tipos de arquivo o GroupDocs.Editor suporta?** Mais de 30 formatos de entrada e saída, incluindo DOCX, XLSX, PPTX, HTML e texto simples.  
- **Preciso de uma licença para listar formatos?** Uma licença temporária desbloqueia a API completa; caso contrário, uma avaliação funciona com recursos limitados.  
- **Quais versões do .NET são compatíveis?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.

## O que é “listar formatos de documento suportados”?
A expressão refere‑se a recuperar programaticamente a coleção de tipos de arquivo que o GroupDocs.Editor pode abrir, editar e salvar. Essa operação permite que você crie menus suspensos de UI dinâmicos ou valide uploads de usuários antes do processamento, garantindo que apenas arquivos compatíveis sejam enviados ao editor para manipulação posterior.

## Por que listar formatos de documento suportados?
O GroupDocs.Editor **suporta mais de 30 formatos de entrada e saída** e pode lidar com arquivos de até **2 GB** sem carregar o documento inteiro na memória. Conhecer a lista exata evita erros em tempo de execução, melhora a experiência do usuário e permite aplicar regras de negócio, como “permitir apenas documentos do Office editáveis”. Também ajuda a apresentar aos usuários somente os formatos que sua aplicação realmente suporta.

## Pré-requisitos
Antes de começar, certifique‑se de que você tem:

1. **Ambiente de desenvolvimento .NET** – Visual Studio 2022 ou qualquer IDE que suporte .NET 6+.  
2. **Biblioteca GroupDocs.Editor para .NET** – faça o download na [página de lançamentos do GroupDocs](https://releases.groupdocs.com/editor/net/).  
3. **Licença temporária** – obtenha uma [licença temporária](https://purchase.groupdocs.com/temporary-license/) para acesso irrestrito.  
4. **Conhecimento básico de C#** – familiaridade com namespaces, declarações `using` e saída de console.

## Como Listar Formatos de Documento Suportados?
Carregue a coleção de formatos suportados e imprima o nome e a extensão de cada formato. Esse padrão de duas etapas funciona para documentos de Processamento de Texto, Planilha e Apresentação. Ao iterar a coleção, você pode preencher dinamicamente elementos de UI, como menus suspensos, garantindo que os usuários só possam selecionar formatos que o editor realmente manipula.

```csharp
// No actual code block – placeholder retained from original tutorial
```csharp
using System;
using GroupDocs.Editor.Options;
```
```

### Listando Formatos de Processamento de Texto
`Formats.WordProcessingFormats` é uma enumeração que descreve cada tipo de arquivo de processamento de texto reconhecido pelo editor. A propriedade `All` devolve uma coleção desses objetos de formato.

```csharp
```csharp
foreach (Formats.WordProcessingFormats oneFormat in Formats.WordProcessingFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
```

**Explicação:**  
1. **Iterar pelos Formatos:** Iteramos sobre todos os formatos de processamento de texto disponíveis.  
2. **Exibir Detalhes do Formato:** Para cada formato imprimimos seu nome amigável e a extensão de arquivo padrão.

### Listando Formatos de Apresentação
`Formats.PresentationFormats` funciona da mesma forma para arquivos de apresentações, expondo cada tipo de apresentação suportado através da coleção `All`.

```csharp
```csharp
foreach (Formats.PresentationFormats oneFormat in Formats.PresentationFormats.All)
{
    Console.WriteLine("Name is {0}, extension is {1}", oneFormat.Name, oneFormat.Extension);
}
```
```

**Explicação:**  
1. **Iterar pelos Formatos:** A mesma lógica de iteração se aplica às apresentações.  
2. **Exibir Detalhes do Formato:** O nome e a extensão são exibidos para cada formato.

## Como Determinar a Extensão do Formato de Arquivo?
Às vezes você tem apenas o nome de um arquivo e precisa inferir o `DocumentFormat` correspondente. O GroupDocs.Editor oferece um helper estático simples que mapeia uma extensão de arquivo para sua representação interna de formato, permitindo validar ou converter arquivos antes de carregá‑los no editor.

### Analisando Formatos de Planilha
`Formats.SpreadsheetFormats.FromExtension` converte uma string de extensão de arquivo no valor enum correspondente ao formato de planilha.

```csharp
```csharp
Formats.SpreadsheetFormats expectedXlsm = Formats.SpreadsheetFormats.FromExtension(".xlsm");
Console.WriteLine("Parsed Spreadsheet format is {0}", expectedXlsm.Name);
```
```

**Explicação:**  
1. **Analisar Formato:** `FromExtension` converte a extensão `.xlsm` para seu enum interno `SpreadsheetFormat`.  
2. **Exibir Formato:** O nome do formato analisado é impresso, confirmando o mapeamento.

### Analisando Formatos Textuais
De forma semelhante, `Formats.TextualFormats.FromExtension` resolve extensões de arquivos textuais como HTML ou TXT.

```csharp
```csharp
Formats.TextualFormats expectedHtml = Formats.TextualFormats.FromExtension("html");
Console.WriteLine("Parsed Textual format is {0}", expectedHtml.Name);
```
```

**Explicação:**  
1. **Analisar Formato:** O método `FromExtension` resolve a extensão `html` para um `TextFormat`.  
2. **Exibir Formato:** O nome do formato textual é exibido, útil para editores baseados na web.

## Como Editar Documentos Após Identificar os Formatos?
Depois de conhecer o formato, carregar e editar um documento segue um padrão consistente. Primeiro você cria uma instância de `Editor` com o caminho do arquivo fonte, então chama `Edit()` para obter um `EditableDocument`. A partir daí você pode ler, modificar e, finalmente, salvar o conteúdo usando as `SaveOptions` apropriadas.

### Carregando um Documento
`Editor` é a classe principal que encapsula todas as operações de edição para um determinado arquivo.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/document.docx"))
{
    // Further steps will be covered here.
}
```
```

**Explicação:**  
1. **Inicializar Editor:** Crie uma instância de `Editor`, passando o caminho completo do arquivo alvo.  
2. **Padrão Dispose:** A instrução `using` garante que todos os recursos não gerenciados sejam liberados prontamente.

### Extraindo Conteúdo
`EditableDocument.GetContent()` devolve o texto bruto do documento (ou HTML para editores baseados na web), que você pode exibir ou manipular.

```csharp
```csharp
using (EditableDocument editableDocument = editor.Edit())
{
    string content = editableDocument.GetContent();
    Console.WriteLine(content);
}
```
```

**Explicação:**  
1. **Método Edit:** `Edit()` devolve um objeto `EditableDocument`.  
2. **Obter Conteúdo:** `GetContent()` extrai o texto bruto do documento (ou HTML para editores baseados na web).  
3. **Exibir Conteúdo:** O conteúdo é escrito no console para verificação.

### Salvando Alterações
`SaveOptions` informa ao editor como e em qual formato gravar o documento editado de volta ao armazenamento.

```csharp
```csharp
using (EditableDocument editableDocument = editor.Edit())
{
    // Modify content here
    SaveOptions saveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docx);
    editor.Save(editableDocument, "path/to/save/document.docx", saveOptions);
}
```
```

**Explicação:**  
1. **Método Edit:** Reobtenha o `EditableDocument` após as modificações.  
2. **Modificar Conteúdo:** Aplique suas alterações à string (não mostrada aqui).  
3. **Opções de Salvamento:** Configure `SaveOptions` com o formato de saída desejado.  
4. **Salvar Documento:** Persista o arquivo editado de volta ao disco.

## Como Trabalhar com Diferentes Tipos de Documento?
O GroupDocs.Editor abstrai o manuseio de Word, Planilha e Apresentação por trás da mesma superfície de API, facilitando a troca de contextos sem precisar aprender um novo conjunto de classes para cada família de documentos.

### Editando Documentos de Planilha
`SpreadsheetSaveOptions` define como uma planilha é gravada, incluindo formato e configurações opcionais de compressão.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/spreadsheet.xlsx"))
{
    using (EditableDocument editableDocument = editor.Edit())
    {
        string content = editableDocument.GetContent();
        Console.WriteLine(content);
        // Modify content here
        SaveOptions saveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsx);
        editor.Save(editableDocument, "path/to/save/spreadsheet.xlsx", saveOptions);
    }
}
```
```

**Explicação:**  
1. **Inicializar Editor:** Passe o caminho de um arquivo de planilha ao construtor `Editor`.  
2. **Método Edit:** Recupere um `EditableDocument`.  
3. **Obter Conteúdo:** Imprima a representação CSV da planilha (ou HTML).  
4. **Modificar Conteúdo:** Aplique quaisquer alterações ao nível de célula que precisar.  
5. **Opções de Salvamento:** Escolha o `SpreadsheetSaveOptions` apropriado.  
6. **Salvar Documento:** Grave a planilha atualizada de volta ao armazenamento.

### Editando Documentos de Apresentação
`PresentationSaveOptions` controla o formato de saída para apresentações, permitindo preservar ou alterar o tipo de arquivo original.

```csharp
```csharp
using (Editor editor = new Editor("path/to/your/presentation.pptx"))
{
    using (EditableDocument editableDocument = editor.Edit())
    {
        string content = editableDocument.GetContent();
        Console.WriteLine(content);
        // Modify content here
        SaveOptions saveOptions = new PresentationSaveOptions(PresentationFormats.Pptx);
        editor.Save(editableDocument, "path/to/save/presentation.pptx", saveOptions);
    }
}
```
```

**Explicação:**  
1. **Inicializar Editor:** Carregue um arquivo PowerPoint via `Editor`.  
2. **Método Edit:** Obtenha um `EditableDocument`.  
3. **Obter Conteúdo:** Extraia o HTML dos slides ou texto simples.  
4. **Modificar Conteúdo:** Atualize títulos, marcadores ou imagens.  
5. **Opções de Salvamento:** Use `PresentationSaveOptions` para definir o formato de saída.  
6. **Salvar Documento:** Persista a apresentação editada.

## Problemas Comuns e Soluções
- **Erro “Formato não suportado”**: Verifique se está usando a versão mais recente do GroupDocs.Editor; ela adiciona suporte a novos formatos do Office regularmente.  
- **Consumo de memória com arquivos grandes**: Habilite o modo streaming definindo `EditorSettings.EnableStreaming = true` antes de carregar o documento.  
- **Licença não aplicada**: Certifique‑se de que o arquivo de licença temporária esteja colocado na raiz da aplicação ou carregado via `License license = new License(); license.SetLicense("path/to/license.lic");`.

## Perguntas Frequentes

**Q: Qual é a diferença entre `DocumentFormatInfo` e `SaveOptions`?**  
A: `DocumentFormatInfo` fornece metadados sobre os tipos de arquivo suportados, enquanto `SaveOptions` configura como um documento é gravado de volta ao disco (formato, compressão, etc.).

**Q: Posso listar formatos para uma extensão de arquivo personalizada?**  
A: Sim — use `DocumentFormatInfo.FromExtension("yourExt")`; se a extensão não for reconhecida, o método retorna `null`.

**Q: O GroupDocs.Editor suporta arquivos protegidos por senha?**  
A: Absolutamente. Passe a senha ao construtor `Editor` via `EditorSettings` para abrir documentos criptografados.

**Q: Quantos formatos o GroupDocs.Editor realmente suporta?**  
A: Mais de **30 formatos de entrada e saída**, abrangendo Word, Excel, PowerPoint, HTML e texto simples.

**Q: Existe uma maneira de restringir a lista apenas a formatos editáveis?**  
A: Use `GetEditableWordProcessingFormats()` (ou os equivalentes para Spreadsheet/Presentation) para obter formatos que permitem recursos completos de edição.

## Recursos Adicionais
- Baixe a biblioteca na [página de lançamentos do GroupDocs](https://releases.groupdocs.com/editor/net/).  
- Obtenha uma [licença temporária](https://purchase.groupdocs.com/temporary-license/) para acesso total aos recursos.  
- Experimente o produto com um [teste gratuito](https://releases.groupdocs.com/).  
- Explore exemplos de uso detalhados na [documentação do GroupDocs.Editor](https://tutorials.groupdocs.com/editor/net/).  
- Obtenha ajuda da comunidade no [fórum de suporte](https://forum.groupdocs.com/c/editor/20).

## Conclusão
Seguindo este guia, você agora sabe como **listar formatos de documento suportados**, **determinar o formato de um arquivo a partir de sua extensão** e **editar documentos** nos tipos Word, Planilha e Apresentação usando o GroupDocs.Editor para .NET. Incorpore esses trechos em seus próprios projetos para criar aplicações robustas e conscientes de formatos, que encantam os usuários finais e reduzem erros em tempo de execução.

**Última atualização:** 2026-06-06  
**Testado com:** GroupDocs.Editor 23.9 for .NET  
**Autor:** GroupDocs

## Tutoriais Relacionados

- [Dominando o Carregamento de Documentos em .NET com GroupDocs.Editor: Um Guia Abrangente](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)
- [Domínio da Edição de Documentos em .NET com GroupDocs.Editor: Um Guia Abrangente](/editor/net/document-editing/master-document-editing-dotnet-groupdocs-editor/)
- [Converter Word para HTML Usando GroupDocs.Editor .NET: Um Guia Passo a Passo](/editor/net/document-saving/convert-word-to-html-groupdocs-editor-dotnet/)