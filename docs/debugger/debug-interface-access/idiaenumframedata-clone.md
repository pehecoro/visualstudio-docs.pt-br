---
title: Idiaenumframedata | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-debug
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: C++
helpviewer_keywords: IDiaEnumFrameData::Clone Method
ms.assetid: 28a17300-1626-422f-a17a-3a4d3872c37c
caps.latest.revision: "7"
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.workload: multiple
ms.openlocfilehash: 9c684eb3f9e18e331190e379ff167b8a296ef041
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="idiaenumframedataclone"></a>IDiaEnumFrameData::Clone
Cria um enumerador que contém o mesmo estado de enumeração do enumerador atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```C++  
HRESULT Clone(   
   IDiaEnumFrameData** ppenum  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 ppenum  
 [out] Retorna um [IDiaEnumFrameData](../../debugger/debug-interface-access/idiaenumframedata.md) objeto que contém uma duplicata do enumerador. O quadro de dados não estão duplicado, apenas o enumerador.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retorna `S_OK`; caso contrário, retorna um código de erro.  
  
## <a name="see-also"></a>Consulte também  
 [IDiaEnumFrameData](../../debugger/debug-interface-access/idiaenumframedata.md)