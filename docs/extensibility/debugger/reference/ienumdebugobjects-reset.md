---
title: IEnumDebugObjects::Reset | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: IEnumDebugObjects::Reset
helpviewer_keywords: IEnumDebugObjects::Reset method
ms.assetid: 4a245e47-cc39-4177-b83d-083ea0e3190f
caps.latest.revision: "6"
author: gregvanl
ms.author: gregvanl
manager: ghogen
ms.workload: vssdk
ms.openlocfilehash: ad2044d73957bb5df7f3c7ebccb12e7c8bafc4e2
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="ienumdebugobjectsreset"></a>IEnumDebugObjects::Reset
Este método redefine a enumeração para o primeiro elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT Reset(void);  
```  
  
```csharp  
int Reset();  
```  
  
#### <a name="parameters"></a>Parâmetros  
 Nenhum  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retorna `S_OK`; caso contrário, retorna um código de erro.  
  
## <a name="remarks"></a>Comentários  
 Depois que este método é chamado, a próxima chamada para [próximo](../../../extensibility/debugger/reference/ienumdebugobjects-next.md) retorna o primeiro elemento da enumeração.  
  
## <a name="see-also"></a>Consulte também  
 [IEnumDebugObjects](../../../extensibility/debugger/reference/ienumdebugobjects.md)   
 [Avançar](../../../extensibility/debugger/reference/ienumdebugobjects-next.md)