---
title: IDebugReference2::SetValueAsReference | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: IDebugReference2::SetValueAsReference
helpviewer_keywords: IDebugReference2::SetValueAsReference
ms.assetid: 94a545d2-16b9-45e9-b2e7-4e49ff90aad0
caps.latest.revision: "10"
author: gregvanl
ms.author: gregvanl
manager: ghogen
ms.workload: vssdk
ms.openlocfilehash: 0de3b3330bac567e1db09025c8d701b0f431d525
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="idebugreference2setvalueasreference"></a>IDebugReference2::SetValueAsReference
Define o valor de uma referência de outra referência. Reservado para uso futuro.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SetValueAsReference (   
   IDebugReference2** rgpArgs,  
   DWORD              dwArgCount,  
   IDebugReference2*  pValue,  
   DWORD              dwTimeout  
);  
```  
  
```cpp  
int SetValueAsReference (   
   IDebugReference2[] rgpArgs,  
   uint               dwArgCount,  
   IDebugReference2   pValue,  
   uint               dwTimeout  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `rgpArgs`  
 [in] Uma matriz de [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) objetos usados para determinar como definir o valor de referência.  
  
 `dwArgCount`  
 [in] O número de referências na matriz.  
  
 `pValue`  
 [in] Um [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) objeto do qual definir o valor da propriedade.  
  
 `dwTimeout`  
 [in] Tempo máximo, em milissegundos, de espera antes de retornar desse método. Use `INFINITE` aguardar indefinidamente.  
  
## <a name="return-value"></a>Valor de retorno  
 Sempre retorna `E_NOTIMPL`.  
  
## <a name="see-also"></a>Consulte também  
 [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)