---
title: ': Findchildren | Microsoft Docs'
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-debug
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: C++
helpviewer_keywords: IDiaSession::findChildren method
ms.assetid: 5d19046f-f668-4aa9-8788-95cda9a98997
caps.latest.revision: "10"
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.workload: multiple
ms.openlocfilehash: 0cae2dd492fd11ff4a5d707ba95c571711358358
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="idiasessionfindchildren"></a>IDiaSession::findChildren
Recupera todos os filhos de um identificador do pai especificado que correspondem ao tipo e um símbolo.  
  
## <a name="syntax"></a>Sintaxe  
  
```C++  
HRESULT findChildren (   
   IDiaSymbol*       parent,  
   SymTagEnum        symtag,  
   LPCOLESTR         name,  
   DWORD             compareFlags,  
   IDiaEnumSymbols** ppResult  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `parent`  
 [in] Um [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) que representa o pai do objeto. Se este símbolo de pai é uma função, módulo ou bloco e seus filhos lexicais são retornados em `ppResult`. Se o símbolo de pai é um tipo, seus filhos de classe são retornados. Se esse parâmetro for `NULL`, em seguida, `symtag` deve ser definido como `SymTagExe` ou `SymTagNull`, que retorna o escopo global (.exe arquivo).  
  
 `symtag`  
 [in] Especifica a marca de símbolo de filhos a serem recuperados. Os valores são tirados de [SymTagEnum enumeração](../../debugger/debug-interface-access/symtagenum.md) enumeração. Definido como `SymTagNull` para recuperar todos os filhos.  
  
 `name`  
 [in] Especifica o nome dos filhos a serem recuperados. Definido como `NULL` para todos os filhos a serem recuperados.  
  
 `compareFlags`  
 [in] Especifica as opções de comparação aplicadas a correspondência de nomes. Os valores do [enumeração NameSearchOptions](../../debugger/debug-interface-access/namesearchoptions.md) enumeração pode ser usada sozinha ou em combinação.  
  
 `ppResult`  
 [out] Retorna um [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md) recuperado do objeto que contém a lista de símbolos de filho.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retorna `S_OK`; caso contrário, retorna um código de erro.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra como localizar variáveis locais de função `pFunc` esse nome de correspondência `szVarName`.  
  
```C++  
IDiaEnumSymbols* pEnum;  
pSession->findChildren( pFunc, SymTagData, szVarName, nsCaseSensitive, &pEnum );  
```  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral](../../debugger/debug-interface-access/overview-debug-interface-access-sdk.md)   
 [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)   
 [IDiaSession](../../debugger/debug-interface-access/idiasession.md)   
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)   
 [Enumeração NameSearchOptions](../../debugger/debug-interface-access/namesearchoptions.md)   
 [Enumeração SymTagEnum](../../debugger/debug-interface-access/symtagenum.md)