---
title: Editar coleção de campos de formulário
linktitle: Editar coleção de campos de formulário
second_title: API GroupDocs.Editor .NET
description: Aumente a eficiência da edição de documentos em projetos .NET com Groupdocs.Editor. Modifique coleções de campos de formulário sem problemas.
weight: 10
url: /pt/net/form-field-management/edit-form-field-collection/
---

# Editar coleção de campos de formulário

## Introdução
Groupdocs.Editor for .NET fornece aos desenvolvedores um conjunto robusto de recursos para trabalhar com vários formatos de documentos. Um desses recursos é a capacidade de editar perfeitamente coleções de campos de formulário em documentos. Esteja você atualizando campos de texto ou implementando proteções de documentos, o Groupdocs.Editor agiliza o processo, aumentando a eficiência e a produtividade.
## Pré-requisitos
Antes de se aprofundar no tutorial, certifique-se de ter os seguintes pré-requisitos:
1.  Pacote Groupdocs.Editor for .NET: Baixe e instale o pacote Groupdocs.Editor for .NET em[aqui](https://releases.groupdocs.com/editor/net/).
2. Documento de amostra: prepare um documento de amostra contendo campos de formulário para experimentação.
3. Compreensão básica de C#: Familiarize-se com os fundamentos da linguagem de programação C#.

## Importando Namespaces
Comece importando os namespaces necessários para acessar a funcionalidade Groupdocs.Editor em seu projeto C#.
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System.IO;
```
## Etapa 1: obter o caminho do arquivo de entrada
```csharp
string inputFilePath = Constants.SampleLegacyFormFields_docx;
```
Nesta etapa, defina o caminho para o arquivo de entrada que contém os campos do formulário que você pretende editar.
## Etapa 2: criar FileStream
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
{
    // Seu código aqui
}
```
 Criar uma`FileStream` do caminho do arquivo de entrada para acessar seu conteúdo.
## Etapa 3: criar opções de carregamento
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
loadOptions.Password = "some_password_to_open_a_document";
```
Configure opções de carregamento para o documento, como especificar uma senha para documentos protegidos por senha.
## Etapa 4: carregar o documento no editor
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
{
    // Seu código aqui
}
```
Carregue o documento na instância do Editor, utilizando o FileStream fornecido e as opções de carregamento.
## Etapa 5: acessar a coleção de campos do formulário
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
Recupere o FormFieldCollection da instância do Editor para manipulação adicional.
## Etapa 6: atualizar o campo do formulário
```csharp
TextFormField textField = collection.GetFormField<TextFormField>("Text1");
textField.LocaleId = 1029;
textField.Value = "new Value";
fieldManager.UpdateFormFiled(collection);
```
Atualize campos específicos do formulário conforme necessário. Neste exemplo, modificamos um campo de formulário de texto.
## Etapa 7: criar opções para salvar
```csharp
WordProcessingFormats docFormat = WordProcessingFormats.Docx;
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(docFormat);
saveOptions.OptimizeMemoryUsage = true;
saveOptions.Protection = new WordProcessingProtection(WordProcessingProtectionType.AllowOnlyFormFields, "write_password");
```
Configure opções de salvamento para o documento, especificando formato, otimização de memória e configurações de proteção de documento.
## Etapa 8: Salvar documento
```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    editor.Save(outputStream, saveOptions);
}
```
Salve o documento editado, direcionando a saída para um MemoryStream ou arquivo conforme sua necessidade.

## Conclusão
Groupdocs.Editor for .NET capacita os desenvolvedores a manipular perfeitamente coleções de campos de formulário em documentos, aumentando a eficiência do fluxo de trabalho. Seguindo este tutorial, você adquiriu as habilidades necessárias para aproveitar todo o potencial desta poderosa biblioteca em seus projetos .NET.

## Perguntas frequentes
### O Groupdocs.Editor é compatível com todos os formatos de documentos?
Groupdocs.Editor oferece suporte a uma ampla variedade de formatos de documentos, incluindo DOCX, XLSX, PPTX e muito mais. Consulte a documentação para obter uma lista abrangente.
### Posso proteger documentos usando Groupdocs.Editor?
Sim, Groupdocs.Editor permite aplicar vários mecanismos de proteção de documentos, incluindo proteção por senha e restrição de permissões de edição.
### Groupdocs.Editor oferece versões de teste para avaliação?
Sim, você pode acessar uma avaliação gratuita do Groupdocs.Editor para explorar seus recursos e capacidades antes de tomar uma decisão de compra.
### Com que frequência o Groupdocs.Editor é atualizado?
Groupdocs atualiza regularmente seus produtos para incorporar novos recursos, melhorias e correções de bugs, garantindo desempenho e confiabilidade ideais.
### O suporte técnico está disponível para usuários do Groupdocs.Editor?
Sim, o Groupdocs fornece suporte técnico dedicado para ajudar os usuários com quaisquer problemas ou dúvidas que possam encontrar ao usar o Groupdocs.Editor.