---
title: DataKind | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-debug
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: C++
helpviewer_keywords: DataKind enumeration
ms.assetid: b64be708-22d6-4360-99e7-8f4e6b196de7
caps.latest.revision: "8"
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.workload: multiple
ms.openlocfilehash: 7fecbec475aee44efd9a91a24ec933dbbbcb17e9
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="datakind"></a>DataKind
Indica o escopo específico de um valor de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```C++  
enum DataKind {   
   DataIsUnknown,  
   DataIsLocal,  
   DataIsStaticLocal,  
   DataIsParam,  
   DataIsObjectPtr,  
   DataIsFileStatic,  
   DataIsGlobal,  
   DataIsMember,  
   DataIsStaticMember,  
   DataIsConstant  
};  
```  
  
## <a name="elements"></a>Elementos  
 DataIsUnknown  
 Símbolo de dados não pode ser determinado.  
  
 DataIsLocal  
 Item de dados é uma variável local.  
  
 DataIsStaticLocal  
 Item de dados é uma variável local estática.  
  
 DataIsParam  
 Item de dados é um parâmetro formal.  
  
 DataIsObjectPtr  
 Item de dados é um ponteiro de objeto (`this`).  
  
 DataIsFileStatic  
 Item de dados é uma variável de escopo de arquivo.  
  
 DataIsGlobal  
 Item de dados é uma variável global.  
  
 DataIsMember  
 Item de dados é uma variável de membro de objeto.  
  
 DataIsStaticMember  
 Item de dados é uma variável de classe estática.  
  
 DataIsConstant  
 Item de dados é um valor constante.  
  
## <a name="remarks"></a>Comentários  
 Os valores nesta enumeração são retornados pelo [: Get_datakind](../../debugger/debug-interface-access/idiasymbol-get-datakind.md) método.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: cvconst.h  
  
## <a name="see-also"></a>Consulte também  
 [Enumerações e estruturas](../../debugger/debug-interface-access/enumerations-and-structures.md)   
 [IDiaSymbol::get_dataKind](../../debugger/debug-interface-access/idiasymbol-get-datakind.md)