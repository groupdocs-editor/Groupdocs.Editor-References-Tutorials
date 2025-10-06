---
title: Trabalhe com planilhas protegidas por senha
linktitle: Trabalhe com planilhas protegidas por senha
second_title: API GroupDocs.Editor .NET
description: Aprenda como lidar com planilhas protegidas por senha usando GroupDocs.Editor for .NET. Este guia detalhado orienta você na abertura e no salvamento de arquivos Excel seguros.
weight: 18
url: /pt/net/document-processing/work-password-protected-spreadsheets/
type: docs
---
# Trabalhe com planilhas protegidas por senha

## Introdução
Você está lutando para gerenciar planilhas protegidas por senha em seus aplicativos .NET? Se sim, você está no lugar certo! Neste guia abrangente, orientaremos você no processo de uso do GroupDocs.Editor for .NET para lidar com planilhas protegidas por senha com eficiência. Ao final deste tutorial, você estará bem equipado para abrir, editar e salvar arquivos criptografados do Excel com facilidade.
## Pré-requisitos
Antes de mergulhar no código, vamos garantir que você tenha tudo o que precisa para acompanhar:
- Conhecimento básico de C#: Este tutorial pressupõe que você esteja familiarizado com programação C#.
- .NET Framework: certifique-se de ter o .NET framework instalado em sua máquina de desenvolvimento.
-  GroupDocs.Editor for .NET: Baixe e instale GroupDocs.Editor for .NET em[aqui](https://releases.groupdocs.com/editor/net/).
## Importar namespaces
Para começar, você precisará importar os namespaces necessários em seu projeto C#. Esses namespaces fornecem acesso às funcionalidades do GroupDocs.Editor.
```csharp
using System;
using System.IO;
using GroupDocs.Editor.Formats;
using GroupDocs.Editor.Options;
```
## Etapa 1: Obtenha um caminho para o arquivo de entrada
Primeiro, você precisará de um caminho para o arquivo de entrada. Para este exemplo, usaremos um arquivo Excel de amostra (`Your Sample Document`) que é protegido por senha.
```csharp
string inputFilePath = "Your Sample Document";
```
## Etapa 2: tentativa de abrir o documento sem senha
Vamos ver o que acontece se tentarmos abrir o documento sem fornecer uma senha.
```csharp
Editor editor = new Editor(inputFilePath);
try
{
    editor.Edit();
}
catch (GroupDocs.Editor.PasswordRequiredException)
{
    Console.WriteLine("Cannot edit the document because it is password-protected. A password is required.");
}
editor.Dispose();
```
## Etapa 3: tente especificar uma senha incorreta
Agora, especificaremos uma senha incorreta para demonstrar como o editor responde.
```csharp
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
loadOptions.Password = "incorrect_password";
editor = new Editor(inputFilePath, delegate { return loadOptions; });
try
{
    editor.Edit();
}
catch (GroupDocs.Editor.IncorrectPasswordException)
{
    Console.WriteLine("Cannot edit the document because the specified password is incorrect.");
}
editor.Dispose();
```
## Etapa 4: abra o arquivo com a senha correta
Vamos fornecer a senha correta e abrir o arquivo com sucesso.
```csharp
loadOptions.Password = "excel_password";
loadOptions.OptimizeMemoryUsage = true;
editor = new Editor(inputFilePath, delegate { return loadOptions; });
```
## Etapa 5: criar e ajustar opções de edição
Para editar a planilha, precisamos criar e ajustar as opções de edição.
```csharp
SpreadsheetEditOptions editOptions = new SpreadsheetEditOptions();
```
## Etapa 6: Crie um documento editável intermediário
 A seguir, criamos um intermediário`EditableDocument` que nos permite fazer alterações na planilha.
```csharp
using (EditableDocument beforeEdit = editor.Edit(editOptions))
{
    // Etapa 7: criar opções para salvar
    SpreadsheetFormats xlsmFormat = SpreadsheetFormats.Xlsm;
    SpreadsheetSaveOptions saveOptions = new SpreadsheetSaveOptions(SpreadsheetFormats.Xlsm);
    // Etapa 7.1: Definir nova senha de abertura
    saveOptions.Password = "new password";
    // Etapa 7.2: Definir proteção contra gravação
    saveOptions.WorksheetProtection = new WorksheetProtection(WorksheetProtectionType.All, "write password");
    // Etapa 8: salve o documento sem modificação
    //Etapa 8.1: Preparar o nome e o caminho do arquivo de saída
    string outputFilename = Path.GetFileNameWithoutExtension(inputFilePath) + "." + xlsmFormat.Extension;
    string outputPath = Path.Combine(Constants.GetOutputDirectoryPath(inputFilePath), outputFilename);
    // Etapa 8.2: Criar fluxo de saída
    using (FileStream outputStream = File.Create(outputPath))
    {
        // Etapa 8.3: Salvar
        editor.Save(beforeEdit, outputStream, saveOptions);
    }
}
// Etapa 9: descartar a instância do editor
editor.Dispose();
Console.WriteLine("Successfully handled the password-protected spreadsheet. Editor instance has been disposed: {0}", editor.IsDisposed ? "Yes" : "No");
```
## Conclusão
Parabéns! Você aprendeu com sucesso como lidar com planilhas protegidas por senha usando GroupDocs.Editor for .NET. Desde a tentativa de abrir o documento sem senha até salvá-lo com novas configurações de proteção, você cobriu todas as etapas essenciais. Esse conhecimento sem dúvida aumentará sua capacidade de gerenciar documentos seguros em seus aplicativos .NET.
## Perguntas frequentes
### O que é GroupDocs.Editor para .NET?
GroupDocs.Editor for .NET é uma poderosa API de edição de documentos que permite aos desenvolvedores carregar, editar e salvar uma variedade de formatos de documentos em aplicativos .NET.
### Como posso obter uma licença temporária do GroupDocs.Editor?
 Você pode obter uma licença temporária em[aqui](https://purchase.groupdocs.com/temporary-license/) para avaliar as características do produto.
### É possível otimizar o uso de memória ao editar documentos grandes?
 Sim, você pode ativar a otimização de memória configurando o`OptimizeMemoryUsage` propriedade para`true`nas opções de carregamento.
### Posso definir senhas diferentes para abrir e gravar em uma planilha?
Absolutamente! Você pode definir senhas separadas para abrir o documento e para proteção contra gravação usando as opções de salvamento.
### Onde posso encontrar documentação mais detalhada?
 Você pode acessar a documentação abrangente do GroupDocs.Editor for .NET[aqui](https://tutorials.groupdocs.com/editor/net/).