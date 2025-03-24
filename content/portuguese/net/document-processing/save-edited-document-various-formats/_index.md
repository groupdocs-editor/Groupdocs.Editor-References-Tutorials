---
title: Salvar documento editado em vários formatos
linktitle: Salvar documento editado em vários formatos
second_title: API GroupDocs.Editor .NET
description: Aprenda como salvar documentos editados em vários formatos usando GroupDocs.Editor for .NET neste guia passo a passo abrangente.
weight: 11
url: /pt/net/document-processing/save-edited-document-various-formats/
---

# Salvar documento editado em vários formatos

## Introdução
Você deseja salvar documentos editados em vários formatos usando GroupDocs.Editor for .NET? Você veio ao lugar certo! Este guia completo irá orientá-lo durante todo o processo, desde a configuração do seu ambiente até salvar o documento editado em vários formatos. Vamos mergulhar e tornar a edição e salvamento de documentos muito fácil!
## Pré-requisitos
Antes de começarmos, certifique-se de ter o seguinte:
1.  GroupDocs.Editor for .NET - Baixe a versão mais recente em[aqui](https://releases.groupdocs.com/editor/net/).
2. Ambiente de Desenvolvimento - Visual Studio ou qualquer outro IDE compatível com .NET.
3. .NET Framework - Certifique-se de ter o .NET Framework 4.6.1 ou superior instalado.
4. Documento de amostra - Um documento de amostra de processamento de texto para trabalhar.
5. Conhecimento básico de C# - É necessária familiaridade com programação C#.
## Importar namespaces
Para começar, certifique-se de importar os namespaces necessários para o seu projeto C#. Isso é crucial para acessar a funcionalidade GroupDocs.Editor.
```csharp
using System;
using GroupDocs.Editor.Metadata;
```
Vamos dividir o processo em etapas gerenciáveis. Acompanhe com atenção para garantir que você entendeu cada parte.
## Etapa 1: Obtenha um caminho para o arquivo de entrada
Primeiro, você precisa especificar o caminho para o arquivo de entrada do WordProcessing. Este arquivo será carregado e editado.
```csharp
string inputFilePath = "Your Sample Document";
```
## Etapa 2: criar opções de carregamento para o documento
A seguir, crie opções de carregamento específicas para documentos do WordProcessing. Essas opções ajudarão a personalizar a forma como o documento é carregado.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
```
## Etapa 3: carregue o documento com opções
 Agora, carregue o documento em um`Editor` instância usando as opções de carregamento especificadas.
```csharp
using (Editor editor = new Editor(inputFilePath, delegate { return loadOptions; }))
```
## Etapa 4: criar opções de edição
Prepare opções de edição para o documento. Estas opções determinarão como o documento será aberto para edição.
```csharp
WordProcessingEditOptions editOptions = new WordProcessingEditOptions();
```
## Etapa 5: abra o documento para edição
 Abra o documento para edição criando um`EditableDocument`instância. Esta instância permitirá que você faça alterações no documento.
```csharp
using (EditableDocument beforeEdit = editor.Edit(editOptions))
```
## Etapa 6: edite o conteúdo do documento
Agora é hora de editar o conteúdo do documento. Primeiro, obtenha o documento como uma única string codificada em base64.
```csharp
string allEmbeddedInsideString = beforeEdit.GetEmbeddedHtml();
```
Por exemplo, vamos modificar o subtítulo do documento.
```csharp
string allEmbeddedInsideStringEdited = allEmbeddedInsideString.Replace("Subtitle", "Edited subtitle");
```
## Etapa 7: Crie um novo documento editável a partir do conteúdo editado
 Crie um novo`EditableDocument` instância do conteúdo e recursos editados.
```csharp
using (EditableDocument afterEdit = EditableDocument.FromMarkup(allEmbeddedInsideStringEdited, null))
```
## Etapa 8: salve o documento em vários formatos
Por fim, repita todos os formatos de processamento de texto compatíveis e salve o documento editado em cada formato.
```csharp
foreach (WordProcessingFormats oneFormat in WordProcessingFormats.All)
{
    // Prepare opções para salvar
    WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(oneFormat);
    // Preparar caminho para salvar
    string savePath = Path.Combine("OutputDirectory", "MultipleOutFormats." + saveOptions.OutputFormat.Extension);
    // Salve o documento
    editor.Save(afterEdit, savePath, saveOptions);
}
```
## Mensagem de conclusão
Para finalizar, você pode imprimir uma mensagem indicando que o processo foi concluído com sucesso.
```csharp
Console.WriteLine("SavingEditedDocumentToAllFormats routine has successfully finished");
```
## Conclusão
Parabéns! Você aprendeu como salvar documentos editados em vários formatos usando GroupDocs.Editor for .NET. Esta ferramenta poderosa facilita a manipulação e salvamento de documentos em vários formatos com apenas algumas linhas de código. Lembre-se de que as principais etapas envolvem carregar o documento, editar o conteúdo e salvá-lo nos formatos desejados.
## Perguntas frequentes
### O que é GroupDocs.Editor para .NET?
GroupDocs.Editor for .NET é uma API poderosa que permite editar documentos em vários formatos usando aplicativos .NET.
### Posso usar o GroupDocs.Editor gratuitamente?
 Sim, você pode usá-lo com uma avaliação gratuita. Baixe[aqui](https://releases.groupdocs.com/).
### Quais formatos são suportados pelo GroupDocs.Editor?
GroupDocs.Editor oferece suporte a uma ampla variedade de formatos, incluindo DOCX, PDF, HTML e muitos mais.
### Como obtenho uma licença temporária do GroupDocs.Editor?
 Você pode obter uma licença temporária[aqui](https://purchase.groupdocs.com/temporary-license/).
### Onde posso encontrar mais documentação e suporte?
 Documentação detalhada está disponível[aqui](https://tutorials.groupdocs.com/editor/net/) , e você pode obter suporte[aqui](https://forum.groupdocs.com/c/editor/20).