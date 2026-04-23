---
date: 2026-03-06
description: Aprenda a lidar com conteúdo CSS com prefixo e extrair conteúdo CSS usando
  o GroupDocs.Editor para .NET neste tutorial detalhado passo a passo.
linktitle: Handle CSS Content with Prefix
second_title: GroupDocs.Editor .NET API
title: Manipular conteúdo CSS com prefixo
type: docs
url: /pt/net/css-handling/handle-css-content-with-prefix/
weight: 11
---

# Manipular Conteúdo CSS com Prefixo

Neste tutorial, você descobrirá **como manipular o prefixo CSS** ao trabalhar com folhas de estilo dentro de um documento usando GroupDocs.Editor para .NET. Se você precisar prefixar uma URL a imagens, fontes ou qualquer recurso externo, os passos abaixo mostram exatamente como **manipular o prefixo CSS** e também como **extrair o conteúdo CSS** para processamento adicional.

## Respostas Rápidas
- **O que significa “manipular o prefixo CSS”?** Adicionar um prefixo de URL personalizado aos recursos externos referenciados no CSS.
- **Qual método da API retorna estilos CSS?** `EditableDocument.GetCssContent(...)`.
- **Preciso de uma licença?** Uma licença de avaliação está disponível; uma licença comercial é necessária para produção.
- **Quais versões do .NET são suportadas?** .NET Framework 4.5+ e .NET Core/5/6.
- **Posso mudar o prefixo em tempo de execução?** Sim – basta passar uma string diferente para `GetCssContent`.

## O que é **manipular o prefixo CSS**?
Aplicar um prefixo aos recursos CSS reescreve os caminhos de imagens, fontes ou outros ativos para que apontem para um local que você controla (por exemplo, um CDN ou um servidor seguro). Isso é especialmente útil quando você exporta um documento e precisa que todas as referências externas sejam acessíveis a partir de uma aplicação web.

## Por que usar o GroupDocs.Editor para **extrair o conteúdo CSS**?
O GroupDocs.Editor pode ler o CSS original incorporado em documentos de processamento de texto, fornecer as strings brutas da folha de estilo e permitir que você as manipule antes de renderizar ou salvar. Isso elimina a necessidade de análise manual e garante que o CSS extraído corresponda à representação interna do documento.

## Pré-requisitos
Antes de começarmos, certifique‑se de que você tem os seguintes pré-requisitos configurados:
- Visual Studio: Você precisará de uma instalação funcional do Visual Studio.  
- .NET Framework: Certifique‑se de que o .NET Framework está instalado.  
- GroupDocs.Editor para .NET: Você pode baixá‑lo [aqui](https://releases.groupdocs.com/editor/net/).  
- Documento de Exemplo: Tenha um documento de exemplo pronto para edição.

## Importar Namespaces
Primeiro, vamos importar os namespaces necessários para garantir que nosso código seja executado sem problemas. Esta etapa nos dá acesso às classes principais do GroupDocs.Editor.

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Editor.Options;
```

## Etapa 1: Inicializar o Editor
A primeira etapa envolve criar uma instância de `Editor` com seu documento de exemplo. Isso configura o ambiente de edição.

```csharp
using (Editor editor = new Editor("Your Sample Document", delegate { return new WordProcessingLoadOptions(); }))
{
```

## Etapa 2: Editar o Documento
Em seguida, obtemos um objeto `EditableDocument`. Este objeto representa a versão editável do arquivo e permite que trabalhemos com suas partes internas.

```csharp
    using (EditableDocument document = editor.Edit(new WordProcessingEditOptions()))
    {
```

## Etapa 3: Definir Prefixos Externos
Defina os prefixos de URL para imagens e fontes. Esses prefixos serão adicionados a cada referência de imagem e fonte encontrada no CSS.

```csharp
        string externalImagesPrefix = "http://www.mywebsite.com/images/id=";
        string externalFontsPrefix = "http://www.mywebsite.com/fonts/id=";
```

## Etapa 4: **Extrair o conteúdo CSS** com os Prefixos
Chame `GetCssContent`, passando os prefixos que você acabou de definir. O método retorna uma lista de strings de folhas de estilo CSS que já contêm as URLs prefixadas.

```csharp
        List<string> stylesheets = document.GetCssContent(externalImagesPrefix, externalFontsPrefix);
```

## Etapa 5: Exibir os Resultados
Imprima o número de folhas de estilo encontradas e exiba cada folha de estilo. Isso ajuda a verificar se os prefixos foram aplicados corretamente.

```csharp
        Console.WriteLine("There are {0} stylesheets in the input document", stylesheets.Count);
        foreach (string css in stylesheets)
        {
            Console.WriteLine(css);
        }
    }
}
```

## Problemas Comuns e Soluções
- **Nenhuma folha de estilo retornada** – Certifique‑se de que o documento de origem realmente contém CSS (por exemplo, um documento Word com tabelas estilizadas ou HTML incorporado).  
- **URLs incorretas** – Verifique novamente se as strings de prefixo terminam com o delimitador apropriado (`/` ou `=`) para o roteamento do seu servidor.  
- **Preocupações de desempenho** – Para documentos muito grandes, considere processar as folhas de estilo em lotes para evitar alto uso de memória.

## Conclusão
Manipular o conteúdo CSS com um prefixo usando o GroupDocs.Editor para .NET é simples e poderoso. Seguindo estas etapas, você pode **manipular o prefixo CSS**, recuperar o CSS bruto via **extrair o conteúdo CSS**, e integrar perfeitamente recursos externos ao seu fluxo de trabalho web. Explore outros recursos do GroupDocs.Editor, como conversão HTML, extração de imagens e mesclagem de documentos, para obter ainda mais valor da API.

## Perguntas Frequentes
### Posso usar o GroupDocs.Editor para .NET com outros formatos de documento?
Sim, o GroupDocs.Editor para .NET suporta vários formatos de documento, incluindo PDF, Word, Excel e outros.

### Existe uma versão de avaliação gratuita disponível para o GroupDocs.Editor para .NET?
Com certeza! Você pode iniciar sua avaliação gratuita [aqui](https://releases.groupdocs.com/).

### Como obtenho uma licença temporária para o GroupDocs.Editor para .NET?
Você pode obter uma licença temporária [aqui](https://purchase.groupdocs.com/temporary-license/).

### Onde posso encontrar documentação detalhada para o GroupDocs.Editor para .NET?
Documentação detalhada está disponível [aqui](https://tutorials.groupdocs.com/editor/net/).

### Quais opções de suporte estão disponíveis para o GroupDocs.Editor para .NET?
Você pode obter suporte [aqui](https://forum.groupdocs.com/c/editor/20).

## Perguntas Frequentes Adicionais

**Q: Posso mudar o prefixo depois de extrair o CSS?**  
A: Sim. Chame `GetCssContent` novamente com uma string de prefixo diferente; o método sempre usa os valores que você passa em tempo de execução.

**Q: Isso funciona com documentos protegidos por senha?**  
A: Sim. Forneça a senha em `WordProcessingLoadOptions` ao criar a instância `Editor`.

**Q: É possível salvar o CSS modificado de volta no documento?**  
A: O GroupDocs.Editor atualmente fornece acesso somente leitura ao CSS. Para persistir as alterações, você precisaria substituir a folha de estilo original usando as APIs XML subjacentes do documento.

---

**Última atualização:** 2026-03-06  
**Testado com:** GroupDocs.Editor 23.12 for .NET  
**Autor:** GroupDocs