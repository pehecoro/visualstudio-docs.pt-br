---
title: "Trechos de código com Ferramentas do R para Visual Studio | Microsoft Docs"
description: "Os trechos de código para R no Visual Studio fornecem atalhos para inserir rapidamente os blocos de código de comprimento arbitrário, ajudando a evitar a necessidade de digitar novamente códigos semelhantes."
ms.custom: 
ms.date: 01/24/2018
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-r
dev_langs:
- R
ms.tgt_pltfrm: 
ms.topic: article
author: kraigb
ms.author: kraigb
manager: ghogen
ms.workload:
- data-science
ms.openlocfilehash: d8628b2712c52aae614223b702344bb0b548e306
ms.sourcegitcommit: 205d15f4558315e585c67f33d5335d5b41d0fcea
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="code-snippets"></a>Trechos de código

Os trechos de código no Visual Studio fornecem atalhos para inserir rapidamente os blocos de código de comprimento arbitrário, ajudando a evitar a necessidade de digitar novamente códigos semelhantes. As RTVS (Ferramentas do R para Visual Studio) adicionam dezenas de trechos do R úteis na coleção do Visual Studio.

Para inserir um trecho, digite o nome abreviado do trecho (o IntelliSense é fornecido), em seguida, pressione Tab para inserir.

Alguns exemplos simples:

- digite `=` e, em seguida, pressione Tab e as RTVS o expandirão para o operador de atribuição `<-`.
- digite `>` e, em seguida, pressione Tab e as RTVS o expandirão para o operador de pipe `%>%`.

Trechos de código podem ser muito mais do que apenas preenchimento de caracteres. Um trecho de código para ler um arquivo .CSV com a função `read.csv`, por exemplo, pode poupar você de precisar lembrar dos nomes ou parâmetros:

![Animação do uso de um trecho de código para inserir uma chamada de read.csv](media/code-snippet-expansion.gif)

Nesse caso, à medida que você digita `readc`, o IntelliSense exibe uma lista de conclusão. Selecionar essa conclusão no menu suspenso e pressionar Tab seleciona `readc` e pressionar Tab novamente expande o trecho de código. (Por esse motivo, a expansão de trecho de código geralmente é considerada como "digitar o trecho e pressionar a tecla Tab duas vezes"). Na maioria dos casos, a primeira Tab preenche a seleção do IntelliSense e a segunda Tab dispara a expansão.

Para ver todos os trechos disponíveis, abra a caixa de diálogo **Ferramentas > Gerenciador de Trechos de Código...** (Ctrl + K, B) e selecione **R** para **Linguagem**. Expanda os grupos e selecione trechos individuais para ver uma descrição e o texto de atalho:

![Caixa de diálogo de trechos de código para R](media/code-snippet-dialog.png)

Para criar trechos de código personalizados, siga as instruções em [Instruções passo a passo: criando um trecho de código](../ide/walkthrough-creating-a-code-snippet.md). Por fim, um trecho de código é apenas um arquivo XML. Por exemplo, o código a seguir é o trecho de código para a operação de pipe (atalho `>`):

```xml
<?xml version="1.0" encoding="utf-8" ?>
<CodeSnippets  xmlns="http://schemas.microsoft.com/VisualStudio/2005/CodeSnippet">
  <CodeSnippet Format="1.0.0">
    <Header>
      <Title>Dplyr pipe</Title>
      <Shortcut>&gt;</Shortcut>
      <Description>Code snippet for '%&gt;%' operator</Description>
      <Author>Microsoft Corporation</Author>
      <SnippetTypes>
        <SnippetType>Expansion</SnippetType>
       </SnippetTypes>
    </Header>
    <Snippet>
      <Code Language="R">
        <![CDATA[ %>% $end$]]>
      </Code>
    </Snippet>
  </CodeSnippet>
</CodeSnippets>
```

Os arquivos XML de todos os trechos de código são instalados com as RTVS; o campo **Local** no **Gerenciador de trechos de código** fornece o caminho. Você também pode encontrá-los no código-fonte das RTVS no GitHub em [src/Package/Impl/Snippets](https://github.com/Microsoft/RTVS/tree/master/src/Package/Impl/Snippets).
