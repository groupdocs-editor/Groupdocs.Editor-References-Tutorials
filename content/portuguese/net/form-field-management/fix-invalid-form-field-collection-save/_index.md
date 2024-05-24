---
title: Corrigir coleção de campos de formulário inválidos e salvar
linktitle: Corrigir coleção de campos de formulário inválidos e salvar
second_title: API GroupDocs.Editor .NET
description: Aprenda como corrigir campos de formulário inválidos em DOCX usando Groupdocs.Editor for .NET. Siga este guia para garantir que seus documentos estejam livres de erros e salvá-los com segurança.
type: docs
weight: 11
url: /pt/net/form-field-management/fix-invalid-form-field-collection-save/
---
## Introdução
Bem-vindo! Se você estiver trabalhando com campos de formulário em documentos e enfrentando problemas com coleções de campos de formulário inválidos, você está no lugar certo. Neste tutorial, veremos como corrigir campos de formulário inválidos e salvar seu documento usando Groupdocs.Editor for .NET. Iremos guiá-lo passo a passo pelo processo, garantindo que você tenha todos os detalhes necessários para que funcione perfeitamente. Vamos começar!
## Pré-requisitos
Antes de entrarmos no código, há algumas coisas que você precisa ter em mente:
-  Groupdocs.Editor para .NET: certifique-se de ter instalado a biblioteca Groupdocs.Editor para .NET. Você pode baixá-lo[aqui](https://releases.groupdocs.com/editor/net/).
- Ambiente de desenvolvimento: você deve ter um ambiente de desenvolvimento .NET configurado, como o Visual Studio.
- Conhecimento básico de C#: Este tutorial pressupõe que você tenha um conhecimento básico de programação C#.
## Importar namespaces
Primeiro, você precisa importar os namespaces necessários em seu projeto C#. Adicione as seguintes linhas no início do seu arquivo de código:
```csharp
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System;
using System.IO;
```
## Etapa 1: obtenha o caminho do arquivo de entrada
primeira etapa é especificar o caminho para o seu arquivo de entrada. Este arquivo deve ser um documento DOCX contendo campos de formulário.
```csharp
string inputFilePath = Constants.SampleLegacyFormFields_docx;
```
## Etapa 2: crie um fluxo a partir do caminho do arquivo
A seguir, crie um fluxo de arquivos para ler o documento de entrada. Isso permitirá que você carregue o documento no editor.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
```
## Etapa 3: criar opções de carregamento para o documento
Nesta etapa, você precisa criar opções de carregamento para o seu documento. Se o seu documento estiver protegido por senha, você poderá especificar a senha. Neste exemplo, o documento não está protegido, portanto a senha é ignorada.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
loadOptions.Password = "some_password_to_open_a_document";
```
## Etapa 4: carregue o documento na instância do editor
Agora, carregue o documento com as opções especificadas na instância do Editor. É aqui que ocorrerão as principais operações no documento.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
```
## Etapa 4.1: Leia a instância do FormFieldManager
 O`FormFieldManager` A instância é responsável por gerenciar os campos do formulário no documento. Você precisará ler esta instância para acessar e manipular os campos do formulário.
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
## Etapa 4.2: Leia o FormFieldCollection
 O`FormFieldCollection` contém todos os campos do formulário no documento. Você lerá esta coleção para verificar e corrigir campos de formulário inválidos.
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
## Etapa 4.3: correção automática de campos de formulário inválidos
Tente corrigir automaticamente quaisquer campos de formulário inválidos no documento. Esta é uma etapa preliminar para resolver questões óbvias.
```csharp
fieldManager.FixInvalidFormFieldNames(new InvalidFormField[0]);
collection = fieldManager.FormFieldCollection;
```
## Etapa 4.4: Verifique se há campos de formulário inválidos
Verifique se há algum campo de formulário inválido após a tentativa de correção automática.
```csharp
bool hasInvalidFormFields = fieldManager.HasInvalidFormFields();
Console.WriteLine("FormFieldCollection contains invalid items: {0}", hasInvalidFormFields);
```
## Etapa 4.4.1: Obtenha todos os nomes de campos de formulário inválidos
Recuperar os nomes de todos os campos de formulário inválidos. Esses nomes serão usados para corrigir os campos.
```csharp
var invalidFormFields = fieldManager.GetInvalidFormFieldNames();
```
## Etapa 4.4.2: Criar nomes exclusivos para campos inválidos
Para cada campo de formulário inválido, crie um nome exclusivo. Isso garante que não haja conflitos com nomes de campos de formulário existentes.
```csharp
foreach (var invalidItem in invalidFormFields)
{
    invalidItem.FixedName = string.Format("{0}_{1}", invalidItem.Name, Guid.NewGuid());
}
```
## Etapa 4.4.3: corrigir campos de formulário inválidos
Corrija os campos inválidos do formulário usando os nomes exclusivos criados na etapa anterior.
```csharp
fieldManager.FixInvalidFormFieldNames(invalidFormFields);
collection = fieldManager.FormFieldCollection;
```
## Etapa 5: criar opções para salvar documentos
Configure opções para salvar o documento. Isso inclui a especificação do formato e quaisquer configurações adicionais de salvamento.
```csharp
WordProcessingFormats docFormat = WordProcessingFormats.Docx;
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions(docFormat);
```
## Etapa 5.1: Otimizar o uso da memória
 Se o seu documento for grande e puder causar um`OutOfMemoryException`ative a opção de otimização de memória.
```csharp
saveOptions.OptimizeMemoryUsage = true;
```
## Etapa 5.2: Proteja o documento contra escrita
Para proteger o documento contra modificações, exceto nos campos do formulário, defina uma senha de proteção.
```csharp
saveOptions.Protection = new WordProcessingProtection(WordProcessingProtectionType.AllowOnlyFormFields, "write_password");
```
## Etapa 6: salve o documento
Finalmente, salve o documento com as opções de salvamento especificadas. Prepare um fluxo de memória para salvar o documento de saída.
```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    editor.Save(outputStream, saveOptions);
}
Console.WriteLine("FixInvalidFormFieldCollectionAndSave routine has successfully finished");
```
## Conclusão
 E aí está! Você corrigiu com sucesso campos de formulário inválidos e salvou seu documento usando Groupdocs.Editor for .NET. Este guia passo a passo deveria ter tornado o processo claro e gerenciável. Se você tiver algum problema ou tiver dúvidas, sinta-se à vontade para verificar o[documentação](https://reference.groupdocs.com/editor/net/) ou entre em contato com[apoiar](https://forum.groupdocs.com/c/editor/20).
## Perguntas frequentes
### E se meu documento estiver protegido por senha?
 Você pode especificar a senha no`WordProcessingLoadOptions` para abrir o documento.
### Como posso saber se existem campos de formulário inválidos?
 Use o`HasInvalidFormFields` método para verificar se há campos de formulário inválidos no documento.
### Posso corrigir campos de formulário sem alterar seus nomes?
É recomendado criar nomes exclusivos para campos de formulário inválidos para evitar conflitos.
### Em quais formatos posso salvar o documento?
 Você pode salvar o documento em vários formatos como DOCX, PDF e muito mais, definindo o apropriado`WordProcessingFormats`.
### Como posso otimizar o uso da memória enquanto salvo documentos grandes?
 Habilite o`OptimizeMemoryUsage` opção no`WordProcessingSaveOptions` para lidar com documentos grandes de forma eficiente.