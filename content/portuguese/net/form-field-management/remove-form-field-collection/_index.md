---
title: Remover coleção de campos de formulário
linktitle: Remover coleção de campos de formulário
second_title: API GroupDocs.Editor .NET
description: Aprenda como remover campos de formulário de documentos do Word usando GroupDocs.Editor for .NET com este guia passo a passo. Ideal para desenvolvedores.
weight: 13
url: /pt/net/form-field-management/remove-form-field-collection/
---

# Remover coleção de campos de formulário

## Introdução
Você deseja gerenciar campos de formulário em seus documentos de maneira programática? GroupDocs.Editor for .NET oferece uma solução poderosa para manipular e manipular campos de formulário em vários formatos de documentos. Neste tutorial, orientaremos você nas etapas para remover coleções de campos de formulário de um documento do Word usando esta biblioteca robusta. 
## Pré-requisitos
Antes de mergulharmos no código, vamos garantir que você tenha tudo configurado para uma experiência tranquila:
1. GroupDocs.Editor for .NET: certifique-se de ter baixado e instalado o GroupDocs.Editor for .NET. Se não, você pode baixá-lo[aqui](https://releases.groupdocs.com/editor/net/).
2. Ambiente de desenvolvimento: você precisará de um ambiente de desenvolvimento como o Visual Studio.
3. .NET Framework: certifique-se de ter o .NET Framework instalado em sua máquina.
4.  Documento de amostra: tenha um documento do Word de amostra (por exemplo,`SampleLegacyFormFields.docx`) com campos de formulário que você deseja manipular.

## Importar namespaces
Para começar, você precisa importar os namespaces necessários em seu projeto .NET. Isso permitirá que você acesse as funcionalidades do GroupDocs.Editor.
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System.IO;
```
## Etapa 1: carregue o documento
Primeiro, você precisará carregar o documento que deseja editar. Vamos decompô-lo:
### Etapa 1.1: Obtenha o caminho para o arquivo de entrada
 Você precisa especificar o caminho para o seu arquivo de entrada. Para este exemplo, usaremos um arquivo de amostra chamado`SampleLegacyFormFields.docx`.
```csharp
string inputFilePath = "path/to/SampleLegacyFormFields.docx";
```
### Etapa 1.2: Crie um FileStream a partir do caminho
 A seguir, crie um`FileStream` para ler o documento.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
{
    // Continue para as próximas etapas deste bloco using.
}
```
## Etapa 2: definir opções de carregamento
Ao carregar o documento, pode ser necessário especificar opções de carregamento, especialmente se o documento estiver protegido por senha.
### Etapa 2.1: Criar opções de carregamento
 Crie uma instância de`WordProcessingLoadOptions`.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
```
### Etapa 2.2: Especifique a senha (se necessário)
Se o seu documento estiver protegido por senha, você poderá especificar a senha.
```csharp
loadOptions.Password = "some_password_to_open_a_document";
```
## Etapa 3: carregue o documento no editor
 Agora, carregue o documento no`Editor` instância usando o`FileStream` e`LoadOptions`.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
{
    // Continue para as próximas etapas deste bloco using.
}
```
## Etapa 4: acessar e gerenciar campos de formulário
Com o documento carregado, agora você pode acessar e manipular os campos do formulário.
### Etapa 4.1: Leia o FormFieldManager
 Recuperar o`FormFieldManager` de`Editor` instância.
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
### Etapa 4.2: Acesse FormFieldCollection
 Pegue o`FormFieldCollection` que contém todos os campos do formulário no documento.
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
### Etapa 4.3: Remover um campo de formulário de texto específico
Para remover um campo de formulário de texto específico, localize-o pelo nome e remova-o.
```csharp
TextFormField textField = collection.GetFormField<TextFormField>("Text1");
fieldManager.RemoveFormFiled(textField);
```
### Etapa 4.4: Remover vários campos do formulário
Você também pode remover vários campos do formulário de uma vez, especificando seus nomes.
```csharp
textField = collection.GetFormField<TextFormField>("Text7");
CheckBoxForm checkBoxForm = collection.GetFormField<CheckBoxForm>("Check2");
fieldManager.RemoveFormFields(new IFormField[] { textField, checkBoxForm });
```
## Etapa 5: salve o documento modificado
Após modificar os campos do formulário, você precisa salvar o documento.
### Etapa 5.1: Criar opções para salvar
Especifique o formato e salve as opções para o documento de saída.
```csharp
WordProcessingFormats docFormat = WordProcessingFormats.Docx;
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(docFormat);
```
### Etapa 5.2: Otimizar o uso da memória
Se estiver lidando com documentos grandes, talvez você queira otimizar o uso da memória.
```csharp
saveOptions.OptimizeMemoryUsage = true;
```
### Etapa 5.3: Definir proteção (se necessário)
Você pode proteger o documento contra edições posteriores definindo uma senha de gravação.
```csharp
saveOptions.Protection = new WordProcessingProtection(WordProcessingProtectionType.AllowOnlyFormFields, "write_password");
```
### Etapa 5.4: Salvar o documento
 Finalmente, salve o documento usando um`MemoryStream`.
```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    editor.Save(outputStream, saveOptions);
}
```

## Conclusão
Parabéns! Você removeu com êxito campos de formulário de um documento do Word usando GroupDocs.Editor for .NET. Essa poderosa biblioteca facilita a manipulação programática do conteúdo do documento, economizando tempo e esforço.
## Perguntas frequentes
### Posso usar o GroupDocs.Editor for .NET com outros formatos de documentos?
Sim, o GroupDocs.Editor for .NET oferece suporte a vários formatos de documentos, incluindo PDF, HTML e muito mais.
### É possível adicionar campos de formulário usando GroupDocs.Editor for .NET?
Sim, você pode adicionar, modificar e remover campos de formulário programaticamente.
### E se meu documento for muito grande?
Você pode ativar a otimização de memória nas opções de salvamento para lidar com documentos grandes com eficiência.
### Posso usar o GroupDocs.Editor for .NET em um aplicativo da web?
Absolutamente! GroupDocs.Editor for .NET pode ser integrado a aplicativos da web para processamento de documentos no servidor.
### Onde posso obter suporte se encontrar problemas?
 Você pode visitar o[Fórum de suporte](https://forum.groupdocs.com/c/editor/20) para obter assistência com quaisquer problemas.