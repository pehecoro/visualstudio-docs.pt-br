---
title: ': Get_isnaked | Microsoft Docs'
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-debug
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: C++
helpviewer_keywords: IDiaSymbol::get_isNaked method
ms.assetid: b16629dc-8e17-476b-9c7b-58e7277c61ed
caps.latest.revision: "7"
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.workload: multiple
ms.openlocfilehash: 018c1398f268b28e5bd547bfbcf69335cc973cf4
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="idiasymbolgetisnaked"></a>IDiaSymbol::get_isNaked
Recupera um sinalizador que especifica se a função tem o [naked](/cpp/cpp/naked-cpp) atributo (ou seja, a função não possui nenhum código de prólogo ou epílogo adicionado pelo compilador).  
  
## <a name="syntax"></a>Sintaxe  
  
```C++  
HRESULT get_isNaked(  
   BOOL *pFlag  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pFlag`  
 [out] Retorna `TRUE` se a função tem o `naked` atributo; caso contrário, retornará `FALSE`.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retorna `S_OK`; caso contrário, retorna `S_FALSE` ou um código de erro.  
  
> [!NOTE]
>  Um valor de retorno `S_FALSE` significa que a propriedade não está disponível para o símbolo.  
  
## <a name="requirements"></a>Requisitos  
  
|Requisito|Descrição|  
|-----------------|-----------------|  
|Cabeçalho:|dia2.h|  
|Versão:|V DIA SDK 8.0|  
  
## <a name="see-also"></a>Consulte também  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)   
 [Chamadas de função naked](/cpp/cpp/naked-function-calls)