---
title: "CA2219: Não acione exceções em cláusulas de exceção | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-code-analysis
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- DoNotRaiseExceptionsInExceptionClauses
- CA2219
helpviewer_keywords:
- DoNotRaiseExceptionsInExceptionClauses
- CA2219
ms.assetid: 7b9b0bee-4e8e-49a4-8c40-52142b49061f
caps.latest.revision: "5"
author: gewarren
ms.author: gewarren
manager: ghogen
ms.workload: multiple
ms.openlocfilehash: 8c5a4ee1d4425b3967928171648453a631aea815
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="ca2219-do-not-raise-exceptions-in-exception-clauses"></a>CA2219: não acione exceções em cláusulas de exceção
|||  
|-|-|  
|NomeDoTipo|DoNotRaiseExceptionsInExceptionClauses|  
|CheckId|CA2219|  
|Categoria|Microsoft.Usage|  
|Alteração Significativa|Contínuo, interrompendo|  
  
## <a name="cause"></a>Causa  
 Uma exceção é gerada a partir de um `finally`, filtro ou cláusula de falha.  
  
## <a name="rule-description"></a>Descrição da Regra  
 Quando uma exceção é gerada em uma cláusula de exceção, ele aumenta muito a dificuldade de depuração.  
  
 Quando uma exceção é gerada em um `finally` ou cláusula de falha, a nova exceção oculta a exceção ativa, se presente. Isso torna o erro original difícil de detectar e depurar.  
  
 Quando uma exceção é gerada em uma cláusula de filtro, o tempo de execução silenciosamente captura a exceção e faz com que o filtro a ser avaliada como false. Não há nenhuma maneira de determinar a diferença entre a avaliação de filtro como false e uma exceção sendo lançar de um filtro. Isso torna difícil detectar e depurar erros na lógica do filtro.  
  
## <a name="how-to-fix-violations"></a>Como Corrigir Violações  
 Para corrigir essa violação desta regra, não explicitamente gere uma exceção de um `finally`, filtro ou cláusula de falha.  
  
## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos  
 Não suprima um aviso para essa regra. Não há nenhum cenário em que uma exceção gerada em uma cláusula de exceção fornece um benefício para o código de execução.  
  
## <a name="related-rules"></a>Regras relacionadas  
 [CA1065: não acionar exceções em locais inesperados](../code-quality/ca1065-do-not-raise-exceptions-in-unexpected-locations.md)  
  
## <a name="see-also"></a>Consulte também  
 [Avisos de design](../code-quality/design-warnings.md)