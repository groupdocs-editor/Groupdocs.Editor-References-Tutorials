---
title: Definir licença medida
linktitle: Definir licença medida
second_title: API GroupDocs.Editor .NET
description: Aprenda como integrar e usar GroupDocs.Editor for .NET com nosso guia completo. Desbloqueie recursos avançados de edição de documentos em seus aplicativos .NET.
weight: 12
url: /pt/net/quick-start-guide/set-metered-license/
---

# Definir licença medida

## Introdução
Bem-vindo ao nosso guia passo a passo sobre como usar o GroupDocs.Editor for .NET! Quer você seja um desenvolvedor experiente ou esteja apenas começando, este tutorial o ajudará a aproveitar todo o potencial desta poderosa biblioteca. GroupDocs.Editor for .NET permite editar documentos de vários formatos em seus aplicativos .NET sem esforço. Vamos nos aprofundar e explorar como você pode começar a usar esta ferramenta robusta.
## Pré-requisitos
Antes de entrarmos nos detalhes técnicos, certifique-se de ter os seguintes pré-requisitos:
- Conhecimento básico de programação .NET: Familiaridade com C# e .NET Framework.
- Visual Studio instalado: certifique-se de ter a versão mais recente do Visual Studio instalada em sua máquina.
-  GroupDocs.Editor for .NET: Baixe a biblioteca do[página de download](https://releases.groupdocs.com/editor/net/).
-  Uma licença válida: Obtenha uma licença temporária ou completa do[Página de compra do GroupDocs](https://purchase.groupdocs.com/temporary-license/).
## Importar namespaces
Para usar o GroupDocs.Editor for .NET, você precisará importar os namespaces necessários em seu projeto. Esta etapa é crucial, pois configura seu projeto para utilizar as funcionalidades da biblioteca.
```csharp
using System;
using GroupDocs.Editor;
```
Vamos dividir cada exemplo em várias etapas para garantir que você possa acompanhar facilmente.
## Etapa 1: Instale GroupDocs.Editor para .NET
Primeiramente, você precisa instalar o GroupDocs.Editor for .NET em seu projeto. Você pode fazer isso por meio do NuGet Package Manager no Visual Studio.
### Instalar por meio do Gerenciador de Pacotes NuGet
1. Abra seu projeto no Visual Studio.
2.  Vá para`Tools` >`NuGet Package Manager` >`Manage NuGet Packages for Solution`.
3.  Procurar`GroupDocs.Editor`.
4.  Clique em`Install`.
Isso adicionará as referências necessárias ao seu projeto.
## Etapa 2: configurar uma licença limitada
Para desbloquear todos os recursos do GroupDocs.Editor, você precisará configurar uma licença limitada. Isso permite que você use a API sem quaisquer limitações.
### Configurando a licença medida
1.  Obtenha suas chaves públicas e privadas no[Página de compra do GroupDocs](https://purchase.groupdocs.com/temporary-license/).
2. Adicione o seguinte código ao seu projeto para definir a licença limitada:
```csharp
string publicKey = "*****";
string privateKey = "*****";
Metered metered = new Metered();
metered.SetMeteredKey(publicKey, privateKey);
Console.WriteLine("License set successfully.");
```
## Etapa 3: carregar e editar um documento
Agora que seu projeto está configurado e licenciado, vamos prosseguir para carregar e editar um documento.
### Carregando um documento
1. Adicione o seguinte código para carregar um documento:
```csharp
string filePath = "sample.docx";
Editor editor = new Editor(filePath);
Console.WriteLine("Document loaded successfully.");
```
### Editando o Documento
2. Para editar o documento, você precisa convertê-lo para um formato editável:
```csharp
EditableDocument editableDocument = editor.Edit();
string content = editableDocument.GetContent();
Console.WriteLine("Document converted to editable format.");
```
## Etapa 4: salve o documento editado
Depois de editar o documento, a etapa final é salvar as alterações.
### Salvando o documento
1. Converta o conteúdo editado de volta ao formato original:
```csharp
string updatedContent = "<html><body>Updated content</body></html>";
editableDocument = EditableDocument.FromMarkup(updatedContent, new WordProcessingSaveOptions());
editor.Save(editableDocument, "updated_sample.docx");
Console.WriteLine("Document saved successfully.");
```
## Conclusão
 Parabéns! Você integrou e usou com êxito o GroupDocs.Editor for .NET em seu aplicativo. Desde a instalação da biblioteca até a configuração de uma licença limitada e a edição de documentos, você cobriu todas as etapas essenciais. Esta ferramenta poderosa pode agilizar significativamente seus fluxos de trabalho de edição de documentos em seus aplicativos .NET. Para mais informações, consulte o[Documentação do GroupDocs.Editor para .NET](https://tutorials.groupdocs.com/editor/net/).
## Perguntas frequentes
### Como obtenho uma licença do GroupDocs.Editor?
 Você pode obter uma licença do[Página de compra do GroupDocs](https://purchase.groupdocs.com/buy) . Para obter uma licença temporária, visite[aqui](https://purchase.groupdocs.com/temporary-license/).
### Posso experimentar o GroupDocs.Editor gratuitamente?
 Sim, você pode baixar uma versão de avaliação gratuita no site[página de download](https://releases.groupdocs.com/) e solicite uma licença temporária.
### Quais formatos de documento são suportados pelo GroupDocs.Editor?
 GroupDocs.Editor suporta vários formatos, incluindo DOCX, PPTX, XLSX, TXT, HTML e muito mais. Para uma lista completa, verifique o[documentação](https://tutorials.groupdocs.com/editor/net/).
### Existe algum suporte da comunidade disponível para GroupDocs.Editor?
 Sim, você pode obter apoio da comunidade no[Fórum GroupDocs.Editor](https://forum.groupdocs.com/c/editor/20).
### Como posso começar a usar o GroupDocs.Editor para .NET?
 Siga nosso guia passo a passo para configurar a biblioteca, obter uma licença e começar a editar documentos. Para obter instruções detalhadas, visite o[documentação](https://tutorials.groupdocs.com/editor/net/).