---
title: IEnumDebugFields | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: IEnumDebugFields
helpviewer_keywords: IEnumDebugFields interface
ms.assetid: 403c2a51-3ba5-431f-a1dd-2f3b2046c00c
caps.latest.revision: "6"
author: gregvanl
ms.author: gregvanl
manager: ghogen
ms.workload: vssdk
ms.openlocfilehash: 9e930a9e78fb1d91bc5738256e0555f3949829c5
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="ienumdebugfields"></a>IEnumDebugFields
Essa interface representa uma coleção de objetos que implementam o [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) interface.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IEnumDebugFields : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 Essa interface é implementada pelo provedor de símbolo para fornecer conjuntos de objetos que implementam o [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) interface. Observe que isso não é uma enumeração COM padrão devido à presença do [GetCount](../../../extensibility/debugger/reference/ienumdebugfields-getcount.md) método.  
  
## <a name="notes-for-callers"></a>Observações para chamadores  
 Essa interface é retornada por [GetMethodFieldsByName](../../../extensibility/debugger/reference/idebugsymbolprovider-getmethodfieldsbyname.md) e [GetNamespacesUsedAtAddress](../../../extensibility/debugger/reference/idebugsymbolprovider-getnamespacesusedataddress.md).  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
 Essa interface implementa os métodos a seguir.  
  
|Método|Descrição|  
|------------|-----------------|  
|[Avançar](../../../extensibility/debugger/reference/ienumdebugfields-next.md)|Recupera o próximo conjunto de [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) objetos a partir da enumeração.|  
|[Skip](../../../extensibility/debugger/reference/ienumdebugfields-skip.md)|Ignora um número especificado de entradas.|  
|[Redefinir](../../../extensibility/debugger/reference/ienumdebugfields-reset.md)|Redefine a enumeração para a primeira entrada.|  
|[Clone](../../../extensibility/debugger/reference/ienumdebugfields-clone.md)|Recupera uma cópia da enumeração atual.|  
|[GetCount](../../../extensibility/debugger/reference/ienumdebugfields-getcount.md)|Recupera o número de entradas na enumeração.|  
  
## <a name="remarks"></a>Comentários  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: sh.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces de provedor de símbolo](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)   
 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)   
 [GetMethodFieldsByName](../../../extensibility/debugger/reference/idebugsymbolprovider-getmethodfieldsbyname.md)   
 [GetNamespacesUsedAtAddress](../../../extensibility/debugger/reference/idebugsymbolprovider-getnamespacesusedataddress.md)