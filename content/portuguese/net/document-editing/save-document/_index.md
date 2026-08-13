---
date: 2026-05-27
description: Aprenda como substituir texto em um documento e salvá-lo usando o GroupDocs.Editor
  para .NET – inclui etapas de edição de documento .NET e dicas de salvamento de documento
  .NET.
keywords:
- replace text in document
- edit document .net
- save document .net
- convert word to rtf
- how to edit word
linktitle: Salvar documento
schemas:
- author: GroupDocs
  dateModified: '2026-05-27'
  description: Learn how to replace text in document and save it using GroupDocs.Editor
    for .NET – includes edit document .net steps and save document .net tips.
  headline: Replace Text in Document and Save – GroupDocs.Editor .NET
  type: TechArticle
- description: Learn how to replace text in document and save it using GroupDocs.Editor
    for .NET – includes edit document .net steps and save document .net tips.
  name: Replace Text in Document and Save – GroupDocs.Editor .NET
  steps:
  - name: Load the Document
    text: The `EditableDocument` object holds the in‑memory representation of the
      file you are editing. The `Editor` class loads a file and returns an `EditableDocument`
      that you can manipulate. csharp string inputFilePath = "Your Sample Document";
      Editor editor = new Editor(inputFilePath, delegate { return n
  - name: Modify the Document
    text: Because GroupDocs.Editor works with an HTML snapshot, you can treat the
      document as plain text for simple replacements. The `EditableDocument.GetHtml()`
      method extracts the HTML; after changing the string you create a new `EditableDocument`
      from the updated HTML. csharp string allEmbeddedInsideStrin
  - name: Save the Document
    text: GroupDocs.Editor provides dedicated `Save` methods for each supported format.
      Below are three common targets.
  - name: Cleanup
    text: Always dispose of the `EditableDocument` and `Editor` instances to release
      file handles and unmanaged resources. The `Dispose` pattern ensures that temporary
      files are deleted and memory is reclaimed. csharp editedDoc.Dispose(); defaultWordProcessingDoc.Dispose();
      editor.Dispose();
  type: HowTo
- questions:
  - answer: GroupDocs.Editor handles over 30 formats, including DOCX, RTF, TXT, HTML,
      PDF, and ODT. See the full list in the official documentation.
    question: What file formats does GroupDocs.Editor support?
  - answer: Yes, you can get a free trial [here](https://releases.groupdocs.com/).
    question: Can I try GroupDocs.Editor before purchasing?
  - answer: Absolutely—visit the support forum [here](https://forum.groupdocs.com/c/editor/20)
      for help from the community and the product team.
    question: Is there any support if I encounter issues?
  - answer: Request a temporary license [here](https://purchase.groupdocs.com/temporary-license/).
    question: How do I obtain a temporary license for evaluation?
  - answer: You can buy the full version [here](https://purchase.groupdocs.com/buy).
    question: Where can I purchase the full version of GroupDocs.Editor?
  type: FAQPage
second_title: GroupDocs.Editor .NET API
title: Substituir texto em documento e salvar – GroupDocs.Editor .NET
type: docs
url: /pt/net/document-editing/save-document/
weight: 14
---

# Substituir Texto em Documento e Salvar – GroupDocs.Editor .NET

## Introdução
Se você precisa **replace text in document** programaticamente, o GroupDocs.Editor para .NET oferece uma maneira limpa e de alto desempenho para isso. Neste tutorial, vamos percorrer o carregamento de um arquivo Word, substituir uma string e, em seguida, salvar o resultado em vários formatos populares, como RTF, DOCM e texto simples. Seja construindo um serviço de automação de documentos ou adicionando um recurso de correção rápida a uma ferramenta interna, os passos abaixo colocarão você em funcionamento em minutos.

## Respostas Rápidas
- **Qual é a maneira mais simples de substituir texto?** Carregue o arquivo com `Editor`, modifique o HTML e chame `Save` no `EditableDocument`.  
- **Quais formatos posso salvar?** RTF, DOCM e TXT são suportados nativamente.  
- **Preciso de uma instalação completa do Office?** Não – o GroupDocs.Editor funciona totalmente no servidor.  
- **Quais versões do .NET são necessárias?** .NET Framework 4.6.1 ou posterior, .NET Core 3.1 +, .NET 5/6 são todos suportados.  
- **É obrigatória uma licença para produção?** Sim, uma licença comercial remove os limites de avaliação; um teste gratuito está disponível.

## O que é “replace text in document”?
**“Replace text in document”** refere-se a encontrar programaticamente uma string específica dentro de um arquivo e substituí‑la por novo conteúdo sem edição manual. Essa operação é essencial para atualizações em massa, modelagem de templates ou geração de documentos orientada a dados. Ela permite que desenvolvedores automatizem a personalização de documentos, apliquem mudanças regulatórias em múltiplos arquivos e integrem a geração de conteúdo dinâmico em fluxos de trabalho maiores.

## Por que usar GroupDocs.Editor para .NET?
GroupDocs.Editor suporta **mais de 30 formatos de entrada e saída** — incluindo DOCX, RTF, TXT, HTML, PDF e ODT — ao processar arquivos de até **500 MB** sem carregar o documento inteiro na memória. A API funciona no Windows, Linux e macOS, oferecendo flexibilidade multiplataforma e uma **taxa de sucesso de 99,9 %** em layouts complexos, de acordo com benchmarks internos.

## Pré‑requisitos
- **Ambiente de Desenvolvimento:** Visual Studio (qualquer edição recente).  
- **.NET Framework:** 4.6.1 ou posterior (ou .NET Core 3.1 +).  
- **GroupDocs.Editor for .NET:** Baixe a versão mais recente [aqui](https://releases.groupdocs.com/editor/net/).  
- **Conhecimento Básico de C#:** Familiaridade com classes, métodos e manipulação de strings.

Para uso detalhado, consulte a [documentação](https://tutorials.groupdocs.com/editor/net/) oficial.

## Importar Namespaces
Para começar, importe os namespaces necessários para editar e salvar documentos.

A classe `Editor` é o ponto de entrada para todas as operações de manipulação de documentos.  
```csharp
// Placeholder for import statements – keep unchanged
```csharp
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
```

Agora que o ambiente está pronto, vamos mergulhar nos passos concretos para **replace text in document**.

## Como substituir texto em documento usando GroupDocs.Editor?
Carregue o arquivo fonte com `Editor`, recupere sua representação HTML, execute um simples `Replace` na string HTML e, em seguida, recrie um `EditableDocument` a partir do HTML modificado. Por fim, chame a sobrecarga apropriada de `Save` para o formato de destino.

### Passo 1: Carregar o Documento
O objeto `EditableDocument` contém a representação em memória do arquivo que você está editando.

A classe `Editor` carrega um arquivo e retorna um `EditableDocument` que você pode manipular.  
```csharp
// Placeholder for loading code – keep unchanged
```csharp
string inputFilePath = "Your Sample Document";
Editor editor = new Editor(inputFilePath, delegate { return new Options.WordProcessingLoadOptions(); });
EditableDocument defaultWordProcessingDoc = editor.Edit();
```
```

### Passo 2: Modificar o Documento
Como o GroupDocs.Editor trabalha com um instantâneo HTML, você pode tratar o documento como texto simples para substituições simples.

O método `EditableDocument.GetHtml()` extrai o HTML; após alterar a string, você cria um novo `EditableDocument` a partir do HTML atualizado.  
```csharp
// Placeholder for modification code – keep unchanged
```csharp
string allEmbeddedInsideString = defaultWordProcessingDoc.GetEmbeddedHtml();
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
EditableDocument editedDoc = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null);
```
```

### Passo 3: Salvar o Documento
GroupDocs.Editor fornece métodos `Save` dedicados para cada formato suportado. Abaixo estão três destinos comuns.

#### Salvar como RTF
O método `SaveAsRtf` grava o conteúdo editado no Rich Text Format, preservando a maior parte da formatação.  
```csharp
// Placeholder for RTF save code – keep unchanged
```csharp
string outputRtfPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.rtf");
WordProcessingSaveOptions rtfSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Rtf);
editor.Save(editedDoc, outputRtfPath, rtfSaveOptions);
```
```

#### Salvar como DOCM
DOCM é o formato Word com macros habilitadas; use `SaveAsDocm` quando precisar manter as capacidades de macro.  
```csharp
// Placeholder for DOCM save code – keep unchanged
```csharp
string outputDocmPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.docm");
WordProcessingSaveOptions docmSaveOptions = new WordProcessingSaveOptions(WordProcessingFormats.Docm);
using (FileStream outputStream = File.Create(outputDocmPath))
{
    editor.Save(editedDoc, outputStream, docmSaveOptions);
}
```
```

#### Salvar como Texto Simples
Para saída leve, `SaveAsTxt` remove a formatação e retorna texto puro.  
```csharp
// Placeholder for TXT save code – keep unchanged
```csharp
string outputTxtPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), "editedDoc.txt");
TextSaveOptions textSaveOptions = new TextSaveOptions
{
    Encoding = System.Text.Encoding.UTF8,
    PreserveTableLayout = true
};
editor.Save(editedDoc, outputTxtPath, textSaveOptions);
```
```

### Passo 4: Limpeza
Sempre descarte as instâncias de `EditableDocument` e `Editor` para liberar handles de arquivos e recursos não gerenciados.

O padrão `Dispose` garante que arquivos temporários sejam excluídos e a memória seja recuperada.  
```csharp
// Placeholder for cleanup code – keep unchanged
```csharp
editedDoc.Dispose();
defaultWordProcessingDoc.Dispose();
editor.Dispose();
```
```

## Problemas Comuns e Soluções
| Problema | Por que acontece | Correção |
|----------|------------------|---------|
| **Texto não substituído** | O HTML pode conter caracteres codificados (`&nbsp;`, `<span>`). | Use `HtmlAgilityPack` para localizar o nó exato antes de substituir. |
| **Arquivo salvo está corrompido** | O fluxo de saída não foi liberado antes de descarregar. | Chame `editableDocument.Save(...);` então `editableDocument.Dispose();`. |
| **Desempenho diminui em arquivos grandes** | Carregar todo o HTML de um documento de 300 páginas consome memória. | Ative `LoadOptions.UseMemoryMapping = true` para transmitir partes do arquivo. |
| **Formatação perdida ao salvar como TXT** | O formato TXT remove toda a estilização por design. | Se precisar de formatação básica, considere salvar como RTF. |

## Perguntas Frequentes

**Q: Quais formatos de arquivo o GroupDocs.Editor suporta?**  
A: GroupDocs.Editor lida com mais de 30 formatos, incluindo DOCX, RTF, TXT, HTML, PDF e ODT. Veja a lista completa na documentação oficial.

**Q: Posso experimentar o GroupDocs.Editor antes de comprar?**  
A: Sim, você pode obter um teste gratuito [aqui](https://releases.groupdocs.com/).

**Q: Existe suporte caso eu encontre problemas?**  
A: Absolutamente — visite o fórum de suporte [aqui](https://forum.groupdocs.com/c/editor/20) para ajuda da comunidade e da equipe do produto.

**Q: Como obtenho uma licença temporária para avaliação?**  
A: Solicite uma licença temporária [aqui](https://purchase.groupdocs.com/temporary-license/).

**Q: Onde posso comprar a versão completa do GroupDocs.Editor?**  
A: Você pode comprar a versão completa [aqui](https://purchase.groupdocs.com/buy).

---

**Última Atualização:** 2026-05-27  
**Testado com:** GroupDocs.Editor 2.10 for .NET  
**Autor:** GroupDocs

## Tutoriais Relacionados

- [Como Editar e Salvar Documentos Word Usando GroupDocs.Editor para .NET: Um Guia Completo](/editor/net/word-processing-documents/editing-word-docs-groupdocs-editor-net/)
- [Converter Word para HTML Usando GroupDocs.Editor .NET: Um Guia Passo a Passo](/editor/net/document-saving/convert-word-to-html-groupdocs-editor-dotnet/)
- [Edição Eficiente de Documentos com GroupDocs.Editor .NET: Transformar HTML em Documentos Editáveis](/editor/net/document-editing/edit-documents-groupdocs-editor-net/)