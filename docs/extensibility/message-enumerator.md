---
title: Enumerador de mensagem | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- message enumerator
- source control plug-ins, message enumeration
ms.assetid: 4a4faa0d-d352-40ea-a21d-c09ea286a8e1
caps.latest.revision: "12"
author: gregvanl
ms.author: gregvanl
manager: ghogen
ms.workload: vssdk
ms.openlocfilehash: 6a24db9c50bd298f068c23af0b6bad5755ec252d
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="message-enumerator"></a>Enumerador de mensagem
Os seguintes sinalizadores são usados para o `TEXTOUTPROC` função, que é uma função de retorno de chamada que o IDE fornece quando ele chama o [SccOpenProject](../extensibility/sccopenproject-function.md) (consulte [LPTEXTOUTPROC](../extensibility/lptextoutproc.md) para obter detalhes sobre o retorno de chamada função).  
  
 Se o IDE é solicitado para cancelar o processo, ele poderá receber uma das mensagens de cancelamento. Nesse caso, a fonte de controlar o plug-in usa `SCC_MSG_STARTCANCEL` para solicitar o IDE para exibir o **Cancelar** botão. Depois disso, qualquer conjunto de mensagens normais pode ser enviado. Se qualquer um desses retorna `SCC_MSG_RTN_CANCEL`, em seguida, encerra a operação e retorna o plug-in. O plug-in também sonda `SCC_MSG_DOCANCEL` periodicamente para determinar se o usuário cancelou a operação. Quando terminar todas as operações ou se o usuário cancelou o plug-in envia `SCC_MSG_STOPCANCEL`. O `SCC_MSG_INFO`, SCC_MSG_WARNING, e os tipos SCC_MSG_ERROR são usados para mensagens que são exibidas na lista de rolagem de mensagens. `SCC_MSG_STATUS`é um tipo especial que indica que o texto deve aparecer em uma barra de status ou a área de exibição temporária. Ele não permanecem permanentemente na lista.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
enum {   
   SCC_MSG_RTN_CANCEL = -1,   
   SCC_MSG_RTN_OK = 0,   
   SCC_MSG_INFO = 1   
   SCC_MSG_WARNING,   
   SCC_MSG_ERROR,   
   SCC_MSG_STATUS,   
   SCC_MSG_DOCANCEL,   
   SCC_MSG_STARTCANCEL,   
   SCC_MSG_STOPCANCEL   
};  
```  
  
## <a name="members"></a>Membros  
 SCC_MSG_RTN_CANCEL  
 Retorno de chamada de retorno para indicar Cancelar.  
  
 SCC_MSG_RTN_OK  
 Retorno de retorno de chamada para continuar.  
  
 SCC_MSG_INFO  
 Mensagem é informativa.  
  
 SCC_MSG_WARNING  
 Mensagem é um aviso.  
  
 SCC_MSG_ERROR  
 Mensagem é um erro.  
  
 SCC_MSG_STATUS  
 Mensagem destina-se a barra de status.  
  
 SCC_MSG_DOCANCEL  
 Nenhum texto; IDE retorna `SCC_MSG_RTN_OK` ou `SCC_MSG_RTN_CANCEL`.  
  
 SCC_MSG_STARTCANCEL  
 Inicia um loop de cancelamento.  
  
 SCC_MSG_STOPCANCEL  
 Interrompe o loop de cancelamento.  
  
## <a name="see-also"></a>Consulte também  
 [Plug-ins de controle de origem](../extensibility/source-control-plug-ins.md)   
 [LPTEXTOUTPROC](../extensibility/lptextoutproc.md)