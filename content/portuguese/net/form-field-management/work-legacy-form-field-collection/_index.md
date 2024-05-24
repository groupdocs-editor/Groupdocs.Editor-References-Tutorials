---
title: Trabalhar com coleção de campos de formulário herdados
linktitle: Trabalhar com coleção de campos de formulário herdados
second_title: API GroupDocs.Editor .NET
description: Aprenda como gerenciar campos de formulário legados usando GroupDocs.Editor for .NET com nosso guia detalhado. Perfeito para lidar com campos de texto, caixas de seleção, datas e muito mais.
type: docs
weight: 12
url: /pt/net/form-field-management/work-legacy-form-field-collection/
---
## Introdução
Bem-vindo a este guia abrangente sobre como trabalhar com coleções de campos de formulário legados usando GroupDocs.Editor for .NET. Esteja você lidando com campos de texto, caixas de seleção, campos de data ou menus suspensos, este tutorial orientará você em cada etapa para gerenciar esses campos com eficiência. Ao final deste guia, você terá um conhecimento sólido de como utilizar o GroupDocs.Editor para lidar com vários campos de formulário em seus documentos. Vamos mergulhar!
## Pré-requisitos
Antes de começarmos, certifique-se de ter os seguintes pré-requisitos:
- Visual Studio: qualquer versão recente funcionará.
- .NET Framework: certifique-se de ter o .NET Framework instalado.
-  GroupDocs.Editor para .NET: Baixe a versão mais recente[aqui](https://releases.groupdocs.com/editor/net/).
- Documento de amostra: um arquivo DOCX de amostra com campos de formulário para fins de teste.
## Importar namespaces
Para começar, importe os namespaces necessários em seu projeto. Esses namespaces são essenciais para acessar as classes e métodos necessários para manipular campos de formulário.
```csharp
using GroupDocs.Editor.Options;
using GroupDocs.Editor.Words.FieldManagement;
using System.IO;
```
## Etapa 1: obtenha o caminho do arquivo de entrada
Primeiro, você precisa especificar o caminho para o seu arquivo de entrada. Neste exemplo, usaremos um arquivo DOCX de amostra que contém vários campos de formulário.
```csharp
string inputFilePath = "path/to/your/sample_legacy_formfields.docx";
```
## Etapa 2: crie um fluxo a partir do caminho do arquivo
A seguir, crie um fluxo de arquivos para ler o conteúdo do seu documento. Este fluxo será usado para carregar o documento no GroupDocs.Editor.
```csharp
using (FileStream fs = File.OpenRead(inputFilePath))
{
    // O código adicional irá aqui
}
```
## Etapa 3: criar opções de carregamento para o documento
Antes de carregar o documento, crie opções de carregamento. Essas opções ajudarão a lidar com diferentes cenários, como documentos protegidos por senha.
```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
// Se o documento estiver protegido por senha, especifique a senha
loadOptions.Password = "your_password_here"; // Use uma senha real, se necessário
```
## Etapa 4: carregar o documento com instância do editor
Agora, carregue o documento na instância do Editor usando o fluxo de arquivo e as opções de carregamento que você criou anteriormente.
```csharp
using (Editor editor = new Editor(delegate { return fs; }, delegate { return loadOptions; }))
{
    // O código adicional irá aqui
}
```
## Etapa 5: leia a instância do FormFieldManager
Para gerenciar campos de formulário, acesse a instância FormFieldManager no Editor. Esta instância permitirá que você interaja com os campos do formulário em seu documento.
```csharp
FormFieldManager fieldManager = editor.FormFieldManager;
```
## Etapa 6: leia o FormFieldCollection
Recupere o FormFieldCollection do FormFieldManager. Esta coleção contém todos os campos do formulário presentes no documento.
```csharp
FormFieldCollection collection = fieldManager.FormFieldCollection;
```
## Etapa 7: iterar em cada campo do formulário
Percorra cada campo do formulário na coleção e identifique seu tipo. Dependendo do tipo, você pode extrair e manipular o valor do campo.
```csharp
foreach (var formField in collection)
{
    switch (formField.Type)
    {
        case FormFieldType.Text:
            TextFormField textFormField = collection.GetFormField<TextFormField>(formField.Name);
            Console.WriteLine($"TextFormField detected, name: {formField.Name}, value: {textFormField.Value}");
            break;
        case FormFieldType.CheckBox:
            CheckBoxForm checkBoxFormField = collection.GetFormField<CheckBoxForm>(formField.Name);
            Console.WriteLine($"CheckBoxForm detected, name: {formField.Name}, value: {checkBoxFormField.Value}");
            break;
        case FormFieldType.Date:
            DateFormField dateFormField = collection.GetFormField<DateFormField>(formField.Name);
            Console.WriteLine($"DateFormField detected, name: {formField.Name}, value: {dateFormField.Value}");
            break;
        case FormFieldType.Number:
            NumberFormField numberFormField = collection.GetFormField<NumberFormField>(formField.Name);
            Console.WriteLine($"NumberFormField detected, name: {formField.Name}, value: {numberFormField.Value}");
            break;
        case FormFieldType.DropDown:
            DropDownFormField dropDownFormField = collection.GetFormField<DropDownFormField>(formField.Name);
            Console.WriteLine($"DropDownFormField detected, name: {formField.Name}, value selected: {dropDownFormField.Value[dropDownFormField.SelectedIndex]}");
            break;
    }
}
```
## Etapa 8: Conclusão
Seguindo essas etapas, você pode gerenciar e interagir de forma eficaz com campos de formulário legados em seus documentos usando GroupDocs.Editor for .NET. Sejam campos de texto, caixas de seleção, datas, números ou menus suspensos, este guia fornece uma maneira clara e concisa de lidar com cada tipo.
## Conclusão
 Trabalhar com campos de formulário legados em documentos pode ser simples quando se usam as ferramentas certas. GroupDocs.Editor for .NET fornece uma solução robusta para gerenciar esses campos com eficiência. Seguindo este guia passo a passo, agora você poderá manipular vários campos de formulário em seus documentos com facilidade. Não se esqueça de explorar o[documentação](https://reference.groupdocs.com/editor/net/)para recursos e opções mais avançados.
## Perguntas frequentes
### 1. Posso usar o GroupDocs.Editor for .NET com documentos protegidos por senha?
Sim, você pode especificar a senha nas opções de carregamento para lidar com documentos protegidos por senha.
### 2. Como posso obter uma avaliação gratuita do GroupDocs.Editor for .NET?
 Você pode baixar uma avaliação gratuita em[aqui](https://releases.groupdocs.com/).
### 3. Existe algum suporte disponível para GroupDocs.Editor for .NET?
 Sim, você pode acessar o suporte[aqui](https://forum.groupdocs.com/c/editor/20).
### 4. Posso adquirir uma licença do GroupDocs.Editor for .NET?
 Sim, você pode comprar uma licença de[aqui](https://purchase.groupdocs.com/buy).
### 5. Onde posso encontrar a documentação do GroupDocs.Editor for .NET?
 documentação está disponível[aqui](https://reference.groupdocs.com/editor/net/).