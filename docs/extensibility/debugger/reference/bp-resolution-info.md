---
title: BP_RESOLUTION_INFO | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: BP_RESOLUTION_INFO
helpviewer_keywords: BP_RESOLUTION_INFO structure
ms.assetid: ba0c162a-61e8-4a0b-811f-4c1d8a5d82f0
caps.latest.revision: "9"
author: gregvanl
ms.author: gregvanl
manager: ghogen
ms.workload: vssdk
ms.openlocfilehash: bc38c55ffab76923f81f2c2eb610ba18f23d701c
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="bpresolutioninfo"></a>BP_RESOLUTION_INFO
Descreve as informações de ponto de interrupção associado para um ponto de interrupção de código ou um ponto de interrupção de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef struct _BP_RESOLUTION_INFO {   
   BPRESI_FIELDS          dwFields;  
   BP_RESOLUTION_LOCATION bpResLocation;  
   IDebugProgram2*        pProgram;  
   IDebugThread2*         pThread;  
} BP_RESOLUTION_INFO;  
```  
  
```csharp  
public struct BP_RESOLUTION_INFO {   
   public uint                   dwFields;  
   public BP_RESOLUTION_LOCATION bpResLocation;  
   public IDebugProgram2         pProgram;  
   public IDebugThread2          pThread;  
};  
```  
  
## <a name="members"></a>Membros  
 `dwFields`  
 Uma coleção de sinalizadores do [BPRESI_FIELDS](../../../extensibility/debugger/reference/bpresi-fields.md) enumerações que especifica quais campos são preenchidas.  
  
 `bpResLocation`  
 O [BP_RESOLUTION_LOCATION](../../../extensibility/debugger/reference/bp-resolution-location.md) estrutura que especifica o local do ponto de interrupção no código ou dados.  
  
 `pProgram`  
 O [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) objeto que representa o aplicativo no qual ocorreu o erro de ponto de interrupção.  
  
 `pThread`  
 O [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md) objeto que representa o thread em que o aplicativo que contém o erro de ponto de interrupção está em execução.  
  
## <a name="remarks"></a>Comentários  
 Essa estrutura é retornada por [GetResolutionInfo](../../../extensibility/debugger/reference/idebugbreakpointresolution2-getresolutioninfo.md).  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Estruturas e uniões](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [GetResolutionInfo](../../../extensibility/debugger/reference/idebugbreakpointresolution2-getresolutioninfo.md)   
 [BPRESI_FIELDS](../../../extensibility/debugger/reference/bpresi-fields.md)   
 [BP_RESOLUTION_LOCATION](../../../extensibility/debugger/reference/bp-resolution-location.md)   
 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)   
 [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)