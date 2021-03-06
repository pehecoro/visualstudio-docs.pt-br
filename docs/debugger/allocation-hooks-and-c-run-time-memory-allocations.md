---
title: "Ganchos de alocação e alocações de memória de tempo de execução do C | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-debug
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: vs.debug.hooks
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [C++], hook functions
- memory allocation, troubleshooting allocation hooks
- allocation hooks
- hooks, allocation
ms.assetid: cc34ee96-3d91-41bd-a019-aa3759139e7e
caps.latest.revision: "14"
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.workload: multiple
ms.openlocfilehash: b123e0e03f33f54e6d4fe82313c9a017e3baafff
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="allocation-hooks-and-c-run-time-memory-allocations"></a>Ganchos de alocação e alocações de memória de tempo de execução do C
Uma restrição muito importante em funções de gancho de alocação é que devem ignorar explicitamente blocos `_CRT_BLOCK` (as alocações de memória feitas internamente por funções da biblioteca em tempo de execução C) se fizerem chamadas às funções da biblioteca em tempo de execução C que alocam a memória interna. Os blocos `_CRT_BLOCK` podem ser ignorados incluindo o código como, por exemplo, o seguinte no início da função de gancho de alocação:  
  
```  
if ( nBlockUse == _CRT_BLOCK )  
    return( TRUE );  
```  
  
 Se seu gancho de alocação não ignorar blocos `_CRT_BLOCK`, qualquer função de biblioteca em tempo de execução C chamada em seu gancho pode interceptar o programa em um loop infinito. Por exemplo, `printf` faz uma alocação interna. Se seu código de gancho chama `printf`, em seguida, a alocação resultante fará com que o gancho ser chamado novamente, que chamará **printf** novamente, e assim por diante até que o estouro de pilha. Se você precisar reportar operações de alocação `_CRT_BLOCK`, uma maneira de evitar essa restrição é usar funções de API do Windows, em vez de funções de tempo de execução C, para formatação e saída. Como as APIs do Windows não usam o heap da biblioteca em tempo de execução C, elas não interceptarão seu gancho de alocação em um loop infinito.  
  
 Se você examinar os arquivos de origem da biblioteca de tempo de execução, você verá que a função, conectar-se a alocação padrão **CrtDefaultAllocHook** (que retorna simplesmente **TRUE**), está localizado em um arquivo separado de seu próprio, DBGHOOK. C. Se você quiser que o gancho de alocação a ser chamado até mesmo para as alocações feitas pelo código de inicialização do tempo de execução que é executado antes de seu aplicativo **principal** função, você pode substituir essa função padrão com uma de sua preferência, em vez de usando [crtsetallochook](/cpp/c-runtime-library/reference/crtsetallochook).  
  
## <a name="see-also"></a>Consulte também  
 [Gravação da função de gancho de depuração](../debugger/debug-hook-function-writing.md)   
