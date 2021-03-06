---
title: Criando personalizado T4 processadores de diretivas do modelo de texto | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.topic: article
helpviewer_keywords:
- text templates, custom directive processors
author: gewarren
ms.author: gewarren
manager: ghogen
ms.workload:
- multiple
ms.technology: vs-ide-modeling
ms.openlocfilehash: 305eb97d18e8513a92637cd92b1f28798677f314
ms.sourcegitcommit: 205d15f4558315e585c67f33d5335d5b41d0fcea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="creating-custom-t4-text-template-directive-processors"></a>Criando processadores de diretiva de modelo de texto T4 personalizados
O *processo de transformação de modelo de texto* leva um *modelo de texto* arquivo como entrada e produz um arquivo de texto como a saída. O *mecanismo de transformação de modelo de texto* controla o processo e o mecanismo interage com um host de transformação de modelo de texto e o modelo de texto de um ou mais *processadores de diretivas* para concluir o processo. Para obter mais informações, consulte [o processo de transformação de modelo de texto](../modeling/the-text-template-transformation-process.md).  
  
 Para criar um processador de diretriz personalizado, é preciso criar uma classe herdada de <xref:Microsoft.VisualStudio.TextTemplating.DirectiveProcessor> ou de <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor>.  
  
 A diferença entre os dois é que <xref:Microsoft.VisualStudio.TextTemplating.DirectiveProcessor> implementa a interface mínima que é necessária para obter os parâmetros do usuário e para gerar o código que produz o arquivo de saída do modelo. <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor>implementa o padrão de design requer/fornece. <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor>lida com dois parâmetros especiais, `requires` e `provides`.  Por exemplo, um processador de diretiva pode aceitar um nome de arquivo do usuário, abra e ler o arquivo e, em seguida, armazenar o texto do arquivo em uma variável denominada `fileText`. Uma subclasse do <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor> classe pode levar a um nome de arquivo do usuário como o valor da `requires` parâmetro e o nome da variável para armazenar o texto como o valor da `provides` parâmetro. Este processador seria abrir e ler o arquivo e, em seguida, armazenar o texto do arquivo na variável especificada.  
  
 Antes de chamar um processador de diretiva de um modelo de texto em [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)], você deve registrá-lo.  
  
 Para obter mais informações sobre como adicionar a chave do registro, consulte [Implantando um processador de diretiva personalizada](../modeling/deploying-a-custom-directive-processor.md).  
  
## <a name="custom-directives"></a>Diretivas personalizadas  
 Uma diretiva personalizada tem esta aparência:  
  
 `<#@ MyDirective Processor="MyDirectiveProcessor" parameter1="value1" ... #>`  
  
 Você pode usar um processador de diretiva personalizado quando quiser acessar dados externos ou recursos de um modelo de texto.  
  
 Modelos de texto diferentes podem compartilhar a funcionalidade que fornece um único processador de diretiva, para que processadores de diretivas fornecem uma maneira de código fator para reutilização. O interno `include` diretiva é semelhante, porque você pode usá-lo para incluir o código e compartilhá-lo entre modelos de texto diferente. A diferença é que nenhuma funcionalidade que o `include` diretiva fornece é fixo e não aceita parâmetros. Se você quiser fornecer funcionalidade comum para um modelo de texto e permitir que o modelo para passar parâmetros, você deve criar um processador de diretiva.  
  
 Alguns exemplos de processadores de diretivas personalizadas podem ser:  
  
-   Um processador de diretiva para retornar dados de um banco de dados que aceita um nome de usuário e senha como parâmetros.  
  
-   Um processador de diretiva para abrir e ler um arquivo que aceita o nome do arquivo como um parâmetro.  
  
### <a name="principal-parts-of-a-custom-directive-processor"></a>Entidade de partes de um processador de diretiva  
 Para desenvolver um processador de diretiva, você deve criar uma classe que herda do <xref:Microsoft.VisualStudio.TextTemplating.DirectiveProcessor> ou <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor>.  
  
 O mais importante `DirectiveProcessor` são os métodos que você deve implementar.  
  
-   `bool IsDirectiveSupported(string directiveName)`-Retorno `true` se o processador de diretiva pode lidar com a diretiva nomeada.  
  
-   `void ProcessDirective (string directiveName, IDictionary<string, string> arguments)`-O mecanismo de modelo chama esse método para cada ocorrência de uma diretiva no modelo. O processador deve salvar os resultados.  
  
 Depois de todas as chamadas para ProcessDirective (), o mecanismo de modelagem chamará esses métodos:  
  
-   `string[] GetReferencesForProcessingRun()`-Retorna os nomes dos assemblies que exige que o código de modelo.  
  
-   `string[] GetImportsForProcessingRun()`-Retorna os namespaces que podem ser usados no código de modelo.  
  
-   `string GetClassCodeForProcessingRun()`-Retorna o código de métodos, propriedades e outras declarações que pode usar o código de modelo. A maneira mais fácil de fazer isso é criar uma cadeia de caracteres que contém o código c# ou Visual Basic. Para fazer com que o processador de diretiva capaz de ser chamado de um modelo que usa qualquer linguagem CLR, você pode construir as instruções de como uma árvore CodeDom e, em seguida, retornar o resultado da serialização de árvore no idioma usado pelo modelo.  
  
-   Para obter mais informações, consulte [passo a passo: Criando um processador de diretiva personalizada](../modeling/walkthrough-creating-a-custom-directive-processor.md).  
  
## <a name="in-this-section"></a>Nesta seção  
 [Implantando um processador de diretiva personalizada](../modeling/deploying-a-custom-directive-processor.md)  
 Explica como registrar um processador de diretiva.  
  
 [Passo a passo: criando um processador de diretiva personalizado](../modeling/walkthrough-creating-a-custom-directive-processor.md)  
 Descreve como criar um processador de diretiva, como registrar e testar o processador de diretiva e como formatar o arquivo de saída como HTML.