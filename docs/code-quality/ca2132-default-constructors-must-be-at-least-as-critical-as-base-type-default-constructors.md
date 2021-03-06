---
title: "CA2132: Os construtores padrão devem ser pelo menos críticos como construtores padrão do tipo base | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-code-analysis
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: CA2132
ms.assetid: e758afa1-8bde-442a-8a0a-bd1ea7b0ce4d
caps.latest.revision: "11"
author: gewarren
ms.author: gewarren
manager: ghogen
ms.workload: multiple
ms.openlocfilehash: 752103825a25c4352ccc21730b8d2b7265f8f41b
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="ca2132-default-constructors-must-be-at-least-as-critical-as-base-type-default-constructors"></a>CA2132: os construtores padrão devem ser pelo menos críticos como construtores padrão do tipo base
|||  
|-|-|  
|NomeDoTipo|DefaultConstructorsMustHaveConsistentTransparency|  
|CheckId|CA2132|  
|Categoria|Microsoft.Security|  
|Alteração Significativa|Quebra|  
  
> [!NOTE]
>  Esse aviso é aplicado somente ao código que está executando o CoreCLR (a versão do CLR que é específico para aplicativos Web do Silverlight).  
  
## <a name="cause"></a>Causa  
 O atributo de transparência do construtor padrão de uma classe derivada não é tão importante quanto a transparência da classe base.  
  
## <a name="rule-description"></a>Descrição da Regra  
 Tipos e membros que têm o <xref:System.Security.SecurityCriticalAttribute> não pode ser usado pelo código do aplicativo do Silverlight. Os tipos de segurança crítica e os membros só podem ser usados por código confiável no .NET Framework para a biblioteca de classes do Silverlight. Como uma construção pública ou protegida em uma classe derivada deve ter a mesma transparência maior que sua classe base, uma classe em um aplicativo não pode ser derivada de uma classe marcada como SecurityCritical.  
  
 Para o código de plataforma do CoreCLR, se um tipo base tem um construtor público ou protegido padrão não transparente, em seguida, o tipo derivado deve obedecer as regras de herança do construtor padrão. O tipo derivado também deve ter um construtor padrão e esse construtor deve ser pelo menos o construtor padrão crítico do tipo base.  
  
## <a name="how-to-fix-violations"></a>Como Corrigir Violações  
 Para corrigir a violação, remova o tipo ou não derivar de tipo não transparente de segurança.  
  
## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos  
 Não suprima avisos dessa regra. Violações desta regra pelo código do aplicativo resultará no CoreCLR se recusa a carregar o tipo com um <xref:System.TypeLoadException>.  
  
### <a name="code"></a>Código  
 [!code-csharp[FxCop.Security.CA2132.DefaultConstructorsMustHaveConsistentTransparency#1](../code-quality/codesnippet/CSharp/ca2132-default-constructors-must-be-at-least-as-critical-as-base-type-default-constructors_1.cs)]  
  
### <a name="comments"></a>Comentários