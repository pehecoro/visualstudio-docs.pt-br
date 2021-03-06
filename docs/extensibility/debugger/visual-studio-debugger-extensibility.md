---
title: Extensibilidade de depurador do Visual Studio | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- debugging [Visual Studio], Debugging SDK
- Debugging SDK
ms.assetid: c088b6a2-c3ad-446b-830d-9c6f41b2934b
caps.latest.revision: "32"
author: gregvanl
ms.author: gregvanl
manager: ghogen
ms.workload: vssdk
ms.openlocfilehash: c5b5943dc8087a22e1bdfb94ae6d0d10335c174a
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="visual-studio-debugger-extensibility"></a>Extensibilidade de depurador do Visual Studio
O Visual Studio inclui um depurador de código fonte totalmente interativo, fornecendo uma ferramenta poderosa e fácil de usar para rastrear bugs em seu programa. O depurador tem suporte completo Visual Basic, c#, C/C++ e JavaScript. No entanto, com o [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]que está disponível na [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=214453), outras linguagens de programação podem ter suporte no depurador com os mesmos recursos avançados.  
  
 O [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] depurador é comum front-end (ou seja, a interface do usuário) para os componentes de depuração são, por sua vez, específico do idioma que está sendo depurado. Para novos idiomas, tudo o que é necessário para suporte pelo [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] depurador é criar os componentes necessários do back-end, como um mecanismo de depuração (DE). É onde o [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] entram em ação.  
  
 O [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] inclui uma referência completa para todos os [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] elementos necessários para criar um novo DE. Além disso, há exemplos e tutoriais que ajudarão você a começar.  
  
 Para um exemplo de ponta a ponta de um sistema de projeto de idioma com suporte à depuração, consulte o [IronPython exemplo](http://msdn.microsoft.com/en-us/4c41695c-12c1-4670-b43b-d8d84c9e4089).  
  
 As seções a seguir descrevem como estender o depurador usando o [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)].  
  
## <a name="in-this-section"></a>Nesta seção  
 [Introdução](../../extensibility/debugger/getting-started-with-debugger-extensibility.md)  
 Descreve o que [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ofertas e como instalar o SDK de depuração.  
  
 [Criar um mecanismo de depuração personalizado](../../extensibility/debugger/creating-a-custom-debug-engine.md)  
 Documenta o processo DE personalizados, de preparação de seu programa para a desanexação DE um DE.  
  
 [Escrevendo um avaliador de expressão de CLR](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)  
 Explica como se você deve gravar um avaliador de expressão.  
  
 [Escolher uma estratégia de implementação do mecanismo de depuração](../../extensibility/debugger/choosing-a-debug-engine-implementation-strategy.md)  
 Descreve como implementar sua DE.  
  
 [Referência](../../extensibility/debugger/reference/reference-visual-studio-debugging-apis.md)  
 Documentos de [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] depuração da API.  
  
 [Amostras](../../extensibility/debugger/visual-studio-debugging-samples.md)  
 Contém links para uma amostra do avaliador de expressão comum idioma em tempo de execução e um exemplo de mecanismo de depuração.
