---
title: IDiaStackWalkHelper | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-debug
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: C++
helpviewer_keywords: IDiaStackWalkHelper2 interface
ms.assetid: d66e5c84-565d-494e-8486-f91db9a34548
caps.latest.revision: "15"
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.workload: multiple
ms.openlocfilehash: 6cbd88bbe3e8a752721047ee80d847e72cf115b9
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="idiastackwalkhelper"></a>IDiaStackWalkHelper
Facilita a movimentação de pilha usando o arquivo de banco de dados (. PDB) de depuração do programa.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
IDiaStackWalkHelper: IUnknown  
  
```  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem VTable  
 A tabela a seguir mostra os métodos de `IDiaStackWalkHelper`:  
  
|Método|Descrição|  
|------------|-----------------|  
|[IDiaStackWalkHelper::get_registerValue](../../debugger/debug-interface-access/idiastackwalkhelper-get-registervalue.md)|Recupera o valor de um registro.|  
|[IDiaStackWalkHelper::put_registerValue](../../debugger/debug-interface-access/idiastackwalkhelper-put-registervalue.md)|Define o valor de um registro.|  
|[IDiaStackWalkHelper::readMemory](../../debugger/debug-interface-access/idiastackwalkhelper-readmemory.md)|Lê um bloco de dados de imagem do arquivo executável na memória.|  
|[IDiaStackWalkHelper::searchForReturnAddress](../../debugger/debug-interface-access/idiastackwalkhelper-searchforreturnaddress.md)|Pesquisa o quadro de pilha especificada para o endereço de retorno de função mais próximo.|  
|[IDiaStackWalkHelper::searchForReturnAddressStart](../../debugger/debug-interface-access/idiastackwalkhelper-searchforreturnaddressstart.md)|Pesquisa o quadro de pilha especificada para um endereço de retorno ou próximo o endereço de pilha especificada.|  
|[IDiaStackWalkHelper::frameForVA](../../debugger/debug-interface-access/idiastackwalkhelper-frameforva.md)|Recupera o quadro de pilha contém o endereço virtual especificado.|  
|[IDiaStackWalkHelper::symbolForVA](../../debugger/debug-interface-access/idiastackwalkhelper-symbolforva.md)|Recupera o símbolo que contém o endereço virtual especificado. **Observação:** símbolo deve ter o tipo `SymTagFunctionType` (um valor da [SymTagEnum enumeração](../../debugger/debug-interface-access/symtagenum.md) enumeração).|  
|[IDiaStackWalkHelper::pdataForVA](../../debugger/debug-interface-access/idiastackwalkhelper-pdataforva.md)|Retorna o bloco de dados PDATA associado ao endereço virtual especificado.|  
|[IDiaStackWalkHelper::imageForVA](../../debugger/debug-interface-access/idiastackwalkhelper-imageforva.md)|Recupera o endereço virtual inicial de um executável, dado um endereço virtual em algum lugar no espaço de memória do executável.|  
  
## <a name="remarks"></a>Comentários  
 Essa interface é chamada pelo código do DIA para obter informações sobre o executável para construir uma lista de quadros de pilha durante a execução do programa.  
  
## <a name="notes-for-callers"></a>Observações para chamadores  
 Um aplicativo cliente implementa essa interface para dar suporte à movimentação de pilha durante a execução do programa. Uma instância desta interface é passada para o [IDiaStackWalker::getEnumFrames](../../debugger/debug-interface-access/idiastackwalker-getenumframes.md) ou [IDiaStackWalker::getEnumFrames2](../../debugger/debug-interface-access/idiastackwalker-getenumframes2.md) métodos.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: Dia2.h  
  
 Biblioteca: diaguids.lib  
  
 DLL: msdia80.dll  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces (SDK de acesso à Interface de depuração)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)   
 [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)   
 [Enumeração SymTagEnum](../../debugger/debug-interface-access/symtagenum.md)   
 [IDiaStackWalker::getEnumFrames](../../debugger/debug-interface-access/idiastackwalker-getenumframes.md)   
 [IDiaStackWalker::getEnumFrames2](../../debugger/debug-interface-access/idiastackwalker-getenumframes2.md)