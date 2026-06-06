---
date: 2026-06-06
description: Aprenda como **criar documentos editáveis** a partir de arquivos CSV
  e TSV usando GroupDocs.Editor for .NET. Este guia também mostra como **ler texto
  delimitado em C#** e **editar CSV em .NET** de forma eficiente no Visual Studio.
keywords:
- create editable document
- read delimited text c#
- edit csv .net
- parse delimited values c#
linktitle: Trabalhar com Valores Delimitados Separados (DSV) – criar documento editável
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to **create editable document** objects from CSV and TSV
    files using GroupDocs.Editor for .NET. This guide also shows how to **read delimited
    text C#** and **edit CSV .NET** efficiently in Visual Studio.
  headline: Work with Delimited Separated Values (DSV) – create editable document
  type: TechArticle
- questions:
  - answer: Yes, the API streams data and can handle files larger than 1 GB without
      loading the entire document into memory.
    question: Can I use GroupDocs.Editor for .NET to edit large CSV files?
  - answer: Absolutely – any single‑character delimiter (e.g., pipe `|`, semicolon
      `;`) is supported as long as you specify it in `DelimitedTextEditOptions`.
    question: Does GroupDocs.Editor for .NET support other DSV formats besides CSV
      and TSV?
  - answer: Yes, you can set the `Encoding` property in `DelimitedTextSaveOptions`
      to UTF‑8, UTF‑16, ISO‑8859‑1, or any .NET `Encoding` you require.
    question: Is it possible to customize the encoding when saving DSV files?
  - answer: Yes – after editing, simply use `SpreadsheetSaveOptions` to export the
      content as an `.xlsx` workbook.
    question: Can I convert a CSV file to an Excel spreadsheet using GroupDocs.Editor
      for .NET?
  - answer: Detailed API references and code samples are available **[here](https://tutorials.groupdocs.com/editor/net/)**.
    question: Where can I find more documentation on GroupDocs.Editor for .NET?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Trabalhar com Valores Delimitados Separados (DSV) – criar documento editável
type: docs
url: /pt/net/document-processing/work-dsv/
weight: 12
---

# Trabalhar com Valores Separados por Delimitador (DSV) – criar documento editável

Se você é um desenvolvedor .NET que precisa **create editable document** objetos a partir de valores separados por delimitador (DSV) como CSV ou TSV, você está no lugar certo. Nas primeiras 100 palavras explicaremos por que o GroupDocs.Editor para .NET é a forma mais confiável de **read delimited text C#**, editá‑lo e, em seguida, salvá‑lo novamente sem perder a formatação. Você sairá com um fluxo de trabalho completo, pronto para copiar‑e‑colar, que se encaixa naturalmente em qualquer solução Visual Studio.

## Respostas Rápidas
- **Qual biblioteca lida melhor com edição de CSV em .NET?** GroupDocs.Editor for .NET.
- **Posso editar arquivos CSV grandes no Visual Studio?** Sim – a API transmite dados e evita carregar o arquivo inteiro na memória.
- **Preciso de licença para uso em produção?** É necessária uma licença comercial; uma avaliação gratuita está disponível.
- **Quais formatos posso gerar após a edição?** CSV, TSV e formatos de planilha compatíveis com Excel.
- **A API é compatível com .NET 6+?** Absolutamente – suporta .NET Framework 4.5+, .NET Core 3.1+, .NET 5 e .NET 6.

## O que é “create editable document” no contexto do GroupDocs.Editor?
**Create editable document** significa gerar uma instância `EditableDocument` que representa uma versão mutável de um arquivo fonte (CSV, TSV, etc.) na memória. Esse objeto permite ler, modificar e salvar novamente o conteúdo usando a mesma API. Ele fornece métodos para recuperar o texto do documento, aplicar alterações e salvá‑lo em vários formatos, garantindo que o alinhamento de colunas e as aspas sejam preservados.

## Por que usar o GroupDocs.Editor para manipulação de DSV?
GroupDocs.Editor processa **mais de 50 formatos de entrada e saída**, incluindo CSV, TSV e planilhas compatíveis com Excel, mantendo o uso de memória abaixo de 10 MB para arquivos de até 500 MB. Ele também preserva o alinhamento de colunas, regras de aspas e codificações personalizadas automaticamente, o que elimina a necessidade de lógica de análise manual.

## Pré‑requisitos
Antes de começarmos, certifique‑se de que você tem o seguinte instalado:

- **Visual Studio** (qualquer edição recente) – você desenvolverá e depurará diretamente dentro da IDE.
- **GroupDocs.Editor for .NET** – baixe o pacote mais recente **[aqui](https://releases.groupdocs.com/editor/net/)**.
- **Conhecimento básico de C#** – o tutorial assume que você pode criar um projeto console ou ASP.NET e adicionar pacotes NuGet.

## Importar Namespaces
As classes `Editor`, `EditableDocument` e de opções residem no namespace `GroupDocs.Editor`.  

A classe `DelimitedTextEditOptions` é o ponto de entrada para definir o delimitador (vírgula, tabulação, etc.) e outras regras de análise.

```csharp
using System.Collections.Generic;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.HtmlCss.Resources;
using GroupDocs.Editor.Options;
```

## Como criar documento editável a partir de um arquivo CSV?
Carregue o CSV fonte com `Editor` e chame o método `Edit`, passando uma instância `DelimitedTextEditOptions` que especifica um delimitador de vírgula. O método retorna um `EditableDocument` que você pode manipular na memória. Esse padrão de duas etapas—load → edit—cobre cenários de **read delimited text C#** e garante que a estrutura original do arquivo seja mantida.

## Etapa 1: Obter um caminho para o arquivo DSV de entrada
Primeiro, você precisa especificar o caminho absoluto ou relativo para o arquivo DSV fonte. Para demonstração, usaremos um CSV simples localizado na pasta `Data` do projeto.

```csharp
string inputFilePath = "Your Sample Document";
```

## Etapa 2: Criar uma instância do Editor
`Editor` é a classe central que orquestra o carregamento, edição e salvamento. Instanciá‑la com um objeto `FileInfo` lhe dá controle total sobre o ciclo de vida do arquivo.

```csharp
using (Editor editor = new Editor(inputFilePath))
{
```

## Etapa 3: Criar opções de edição DSV
`DelimitedTextEditOptions` informa ao editor como interpretar o arquivo. Você pode definir o delimitador, se a primeira linha contém cabeçalhos e a codificação de caracteres.

```csharp
    Options.DelimitedTextEditOptions editOptions = new DelimitedTextEditOptions(",");
    editOptions.ConvertDateTimeData = false;
    editOptions.ConvertNumericData = true;
    editOptions.TreatConsecutiveDelimitersAsOne = true;
```

## Etapa 4: Criar instância de EditableDocument
`EditableDocument` representa uma versão mutável em memória do arquivo fonte. Chamar `Editor.Edit` com as opções retorna um `EditableDocument`. Esse objeto contém o texto do arquivo em uma string mutável, pronto para qualquer operação **parse delimited values C#** que você precisar.

```csharp
    EditableDocument beforeEdit = editor.Edit(editOptions);
```

## Etapa 5: Editar o conteúdo do documento
`GetDocumentText()` devolve o texto atual do documento editável como uma string. Recupere o texto original via `EditableDocument.GetDocumentText()`, execute suas modificações (por exemplo, substituir o valor de uma coluna) e armazene o resultado em uma nova string. É aqui que você **edit CSV .NET** sem tocar em fluxos de arquivo de baixo nível.

```csharp
    string originalTextContent = beforeEdit.GetContent();
    string updatedTextContent = originalTextContent.Replace("SsangYong", "Chevrolet").Replace("Kyron", "Camaro");
    List<IHtmlResource> allResources = beforeEdit.AllResources;
```

## Etapa 6: Criar EditableDocument com conteúdo atualizado
Envolva a string modificada novamente em um `EditableDocument`. Esta etapa finaliza as alterações e prepara o objeto para ser salvo em qualquer formato suportado.

```csharp
    EditableDocument afterEdit = EditableDocument.FromMarkup(updatedTextContent, allResources);
```

## Etapa 7: Criar opções de salvamento CSV
`DelimitedTextSaveOptions` especifica como gravar o conteúdo editado de volta em um arquivo CSV. Quando estiver pronto para persistir as alterações, configure `DelimitedTextSaveOptions`. Você pode especificar o mesmo delimitador, um diferente ou até mudar o estilo de terminação de linha.

```csharp
    Options.DelimitedTextSaveOptions csvSaveOptions = new DelimitedTextSaveOptions(",");
    csvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

## Etapa 8: Criar opções de salvamento TSV
Se precisar de uma versão separada por tabulação, basta mudar o delimitador para `\t`. O mesmo `EditableDocument` pode ser salvo várias vezes com opções diferentes.

```csharp
    Options.DelimitedTextSaveOptions tsvSaveOptions = new DelimitedTextSaveOptions("\t");
    tsvSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

## Etapa 9: Criar opções de salvamento de planilha
`SpreadsheetSaveOptions` configura a exportação do documento para formatos compatíveis com Excel, como .xlsx. O GroupDocs.Editor também permite exportar os dados editados para um formato compatível com Excel (`.xlsx`). A classe `SpreadsheetSaveOptions` lida automaticamente com tipos de colunas, fórmulas e estilos de célula.

```csharp
    Options.SpreadsheetSaveOptions cellsSaveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
```

## Etapa 10: Preparar caminhos de salvamento
Defina caminhos de saída distintos para cada formato. Usar convenções de nomenclatura claras (por exemplo, `output.csv`, `output.tsv`, `output.xlsx`) ajuda a manter seu projeto organizado.

```csharp
    string outputCsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".csv");
    string outputTsvPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".tsv");
    string outputCellsPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), Path.GetFileNameWithoutExtension(inputFilePath) + ".xlsm");
```

## Etapa 11: Salvar o documento editado
`Save()` grava o documento no disco usando as opções de salvamento fornecidas. Chame `EditableDocument.Save` com as opções apropriadas para cada formato de destino. A API grava o arquivo diretamente no disco, preservando a codificação original, a menos que você a sobrescreva.

```csharp
    editor.Save(afterEdit, outputCsvPath, csvSaveOptions);
    editor.Save(afterEdit, outputTsvPath, tsvSaveOptions);
    editor.Save(afterEdit, outputCellsPath, cellsSaveOptions);
```

## Etapa 12: Dispor instâncias de EditableDocument
Tanto `Editor` quanto `EditableDocument` implementam `IDisposable`. Dispor deles libera manipuladores de arquivos e recursos não gerenciados, o que é crucial ao processar muitos arquivos em um trabalho em lote.

```csharp
    beforeEdit.Dispose();
    afterEdit.Dispose();
}
System.Console.WriteLine("WorkingWithDsv routine has successfully finished");
```

## Problemas comuns e soluções
| Problema | Por que acontece | Correção |
|----------|------------------|----------|
| **Aspas extras inesperadas** | O analisador CSV padrão pode tratar vírgulas incorporadas como delimitadores. | Defina `EscapeMode = EscapeMode.DoubleQuote` em `DelimitedTextEditOptions`. |
| **Pico de memória em arquivo grande** | Carregar um arquivo de 500 MB sem streaming. | Use `Editor.Load` com `LoadOptions` que habilitam carregamento preguiçoso. |
| **Incompatibilidade de codificação** | O arquivo fonte usa UTF‑16, mas as opções padrão são UTF‑8. | Defina explicitamente `Encoding = Encoding.Unicode` nas opções de salvamento. |

## Perguntas Frequentes

**Q: Posso usar o GroupDocs.Editor para .NET para editar arquivos CSV grandes?**  
A: Sim, a API transmite dados e pode lidar com arquivos maiores que 1 GB sem carregar o documento inteiro na memória.

**Q: O GroupDocs.Editor para .NET suporta outros formatos DSV além de CSV e TSV?**  
A: Absolutamente – qualquer delimitador de um único caractere (por exemplo, pipe `|`, ponto‑e‑vírgula `;`) é suportado, desde que você o especifique em `DelimitedTextEditOptions`.

**Q: É possível personalizar a codificação ao salvar arquivos DSV?**  
A: Sim, você pode definir a propriedade `Encoding` em `DelimitedTextSaveOptions` para UTF‑8, UTF‑16, ISO‑8859‑1 ou qualquer `Encoding` .NET que precisar.

**Q: Posso converter um arquivo CSV para uma planilha Excel usando o GroupDocs.Editor para .NET?**  
A: Sim – após a edição, basta usar `SpreadsheetSaveOptions` para exportar o conteúdo como uma pasta de trabalho `.xlsx`.

**Q: Onde posso encontrar mais documentação sobre o GroupDocs.Editor para .NET?**  
A: Referências detalhadas da API e exemplos de código estão disponíveis **[aqui](https://tutorials.groupdocs.com/editor/net/)**.

**Última atualização:** 2026-06-06  
**Testado com:** GroupDocs.Editor 23.10 para .NET  
**Autor:** GroupDocs

## Tutoriais Relacionados

- [Tutoriais de edição de documentos de texto simples e DSV para GroupDocs.Editor .NET](/editor/net/plain-text-dsv-documents/)
- [Domine o GroupDocs.Editor .NET para edição eficiente de documentos CSV e conversão](/editor/net/plain-text-dsv-documents/groupdocs-editor-net-csv-editing-guide/)
- [Domínio do carregamento de documentos em .NET com GroupDocs.Editor: Um guia abrangente](/editor/net/document-loading/groupdocs-editor-net-document-loading-guide/)