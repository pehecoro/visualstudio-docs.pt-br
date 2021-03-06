---
title: 'CA1502: Evitar complexidade excessiva | Microsoft Docs'
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-code-analysis
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- AvoidExcessiveComplexity
- CA1502
helpviewer_keywords:
- CA1502
- AvoidExcessiveComplexity
ms.assetid: d735454b-2f8f-47ce-907d-f7a5a5391221
caps.latest.revision: "30"
author: gewarren
ms.author: gewarren
manager: ghogen
ms.workload: multiple
ms.openlocfilehash: a643d71e334d7a9228afbb9ba95df2f4cbb558c0
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="ca1502-avoid-excessive-complexity"></a>CA1502: evitar complexidade excessiva
|||  
|-|-|  
|NomeDoTipo|AvoidExcessiveComplexity|  
|CheckId|CA1502|  
|Categoria|Microsoft.Maintainability|  
|Alteração Significativa|Não recentes|  
  
## <a name="cause"></a>Causa  
 Um método tem uma complexidade ciclomática excessiva.  
  
## <a name="rule-description"></a>Descrição da Regra  
 *A complexidade ciclomática* mede o número de caminhos independentes linearmente por meio do método, o que é determinado pelo número e a complexidade de ramificações condicionais. Uma complexidade ciclomática baixa geralmente indica um método fácil de entender, testar e manter. A complexidade ciclomática é calculada a partir de um gráfico de fluxo de controle do método e recebe da seguinte maneira:  
  
 a complexidade ciclomática = o número de bordas - o número de nós + 1  
  
 em que um nó representa um ponto de ramificação de lógica e uma borda representa uma linha entre os nós.  
  
 A regra relata uma violação quando a complexidade ciclomática é mais de 25.  
  
 Você pode aprender mais sobre as métricas de código em [medindo complexidade e facilidade de manutenção do código gerenciado](../code-quality/measuring-complexity-and-maintainability-of-managed-code.md),  
  
## <a name="how-to-fix-violations"></a>Como Corrigir Violações  
 Para corrigir uma violação desta regra, Refatore o método para reduzir sua complexidade ciclomática.  
  
## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos  
 É seguro suprimir um aviso de que essa regra se facilmente não pode ser reduzida a complexidade e o método é fácil de entender, testar e manter. Em particular, um método que contém um grande `switch` (`Select` em [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]) instrução é um candidato para exclusão. O risco de desestabilizar o código base tardia no ciclo de desenvolvimento ou apresentando uma alteração inesperada no comportamento de tempo de execução de código fornecido anteriormente pode compensar os benefícios de facilidade de manutenção de refatorar o código.  
  
## <a name="how-cyclomatic-complexity-is-calculated"></a>Como a complexidade ciclomática é calculada  
 A complexidade ciclomática é calculada adicionando 1 para o seguinte:  
  
-   Número de ramificações (como `if`, `while`, e `do`)  
  
-   Número de `case` instruções em um`switch`  
  
 Os exemplos a seguir mostram os métodos que possuem as complexidades de ciclomática variados.  
  
## <a name="example"></a>Exemplo  
 **Complexidade ciclomática igual a 1**  
  
 [!code-cpp[FxCop.Maintainability.AvoidExcessiveComplexity#1](../code-quality/codesnippet/CPP/ca1502-avoid-excessive-complexity_1.cpp)]
 [!code-vb[FxCop.Maintainability.AvoidExcessiveComplexity#1](../code-quality/codesnippet/VisualBasic/ca1502-avoid-excessive-complexity_1.vb)]
 [!code-csharp[FxCop.Maintainability.AvoidExcessiveComplexity#1](../code-quality/codesnippet/CSharp/ca1502-avoid-excessive-complexity_1.cs)]  
  
## <a name="example"></a>Exemplo  
 **Complexidade ciclomática igual 2**  
  
 [!code-cpp[FxCop.Maintainability.AvoidExcessiveComplexity#2](../code-quality/codesnippet/CPP/ca1502-avoid-excessive-complexity_2.cpp)]
 [!code-vb[FxCop.Maintainability.AvoidExcessiveComplexity#2](../code-quality/codesnippet/VisualBasic/ca1502-avoid-excessive-complexity_2.vb)]
 [!code-csharp[FxCop.Maintainability.AvoidExcessiveComplexity#2](../code-quality/codesnippet/CSharp/ca1502-avoid-excessive-complexity_2.cs)]  
  
## <a name="example"></a>Exemplo  
 **Complexidade ciclomática 3**  
  
 [!code-cpp[FxCop.Maintainability.AvoidExcessiveComplexity#3](../code-quality/codesnippet/CPP/ca1502-avoid-excessive-complexity_3.cpp)]
 [!code-vb[FxCop.Maintainability.AvoidExcessiveComplexity#3](../code-quality/codesnippet/VisualBasic/ca1502-avoid-excessive-complexity_3.vb)]
 [!code-csharp[FxCop.Maintainability.AvoidExcessiveComplexity#3](../code-quality/codesnippet/CSharp/ca1502-avoid-excessive-complexity_3.cs)]  
  
## <a name="example"></a>Exemplo  
 **Complexidade ciclomática de 8**  
  
 [!code-cpp[FxCop.Maintainability.AvoidExcessiveComplexity#4](../code-quality/codesnippet/CPP/ca1502-avoid-excessive-complexity_4.cpp)]
 [!code-vb[FxCop.Maintainability.AvoidExcessiveComplexity#4](../code-quality/codesnippet/VisualBasic/ca1502-avoid-excessive-complexity_4.vb)]
 [!code-csharp[FxCop.Maintainability.AvoidExcessiveComplexity#4](../code-quality/codesnippet/CSharp/ca1502-avoid-excessive-complexity_4.cs)]  
  
## <a name="related-rules"></a>Regras relacionadas  
 [CA1501: evitar herança excessiva](../code-quality/ca1501-avoid-excessive-inheritance.md)  
  
## <a name="see-also"></a>Consulte também  
 [Medindo complexidade e facilidade de manutenção do código gerenciado](../code-quality/measuring-complexity-and-maintainability-of-managed-code.md)