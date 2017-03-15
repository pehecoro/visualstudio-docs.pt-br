---
title: "PublicSymbol | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "vs-ide-debug"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "C++"
helpviewer_keywords: 
  - "símbolo de dados [C++]"
  - "Símbolo PublicSymbol"
  - "funções globais [C++], como símbolos públicos"
ms.assetid: f8d33007-302d-4549-9dad-47fb33ea60b7
caps.latest.revision: 17
caps.handback.revision: 17
author: "mikejo5000"
ms.author: "mikejo"
manager: "ghogen"
---
# PublicSymbol
[!INCLUDE[vs2017banner](../../code-quality/includes/vs2017banner.md)]

Quando o arquivo. exe é criado, cada símbolo público \(com um mínimo, global de cada função e dados símbolo\) é fornecido um `SymTagPublicSymbol` marca.  
  
## Propriedades  
 A tabela a seguir mostra as propriedades que são válidas para este tipo de símbolo.  
  
|Propriedade|Tipo de dados|Descrição|  
|-----------------|-------------------|---------------|  
|[IDiaSymbol::get\_addressOffset](../../debugger/debug-interface-access/idiasymbol-get-addressoffset.md)|`DWORD`|Deslocamento de parte do local. Para obter detalhes, consulte a [Enumeração LocationType](../../debugger/debug-interface-access/locationtype.md).|  
|[IDiaSymbol::get\_addressSection](../../debugger/debug-interface-access/idiasymbol-get-addresssection.md)|`DWORD`|Parte da seção de local; Para obter detalhes, consulte a [Enumeração LocationType](../../debugger/debug-interface-access/locationtype.md).|  
|[IDiaSymbol::get\_code](../../debugger/debug-interface-access/idiasymbol-get-code.md)|`BOOL`|`TRUE`Se o local do símbolo está no código.|  
|[IDiaSymbol::get\_function](../Topic/IDiaSymbol::get_function.md)|`BOOL`|`TRUE`Se o símbolo é uma função.|  
|[IDiaSymbol::get\_length](../../debugger/debug-interface-access/idiasymbol-get-length.md)|`ULONGLONG`|Comprimento deste símbolo em bytes.|  
|[IDiaSymbol::get\_lexicalParent](../../debugger/debug-interface-access/idiasymbol-get-lexicalparent.md)|`IDiaSymbol*`|Símbolo de escopo global.|  
|[IDiaSymbol::get\_lexicalParentId](../../debugger/debug-interface-access/idiasymbol-get-lexicalparentid.md)|`DWORD`|ID do símbolo pai lexical.|  
|[IDiaSymbol::get\_locationType](../Topic/IDiaSymbol::get_locationType.md)|`DWORD`|Símbolos públicos têm locais de estáticos; Para obter detalhes, consulte [Locais de símbolos](../../debugger/debug-interface-access/symbol-locations.md).|  
|[IDiaSymbol::get\_managed](../../debugger/debug-interface-access/idiasymbol-get-managed.md)|`BOOL`|`TRUE`Se o local do símbolo é código gerenciado.|  
|[IDiaSymbol::get\_msil](../../debugger/debug-interface-access/idiasymbol-get-msil.md)|`BOOL`|`TRUE`Se o local do símbolo é código Microsoft Intermediate Language \(MSIL\).|  
|[IDiaSymbol::get\_name](../Topic/IDiaSymbol::get_name.md)|`BSTR`|O nome totalmente decorado do símbolo.|  
|[IDiaSymbol::get\_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|`DWORD`|ID de índice do símbolo.|  
|[IDiaSymbol::get\_relativeVirtualAddress](../../debugger/debug-interface-access/idiasymbol-get-relativevirtualaddress.md)|`DWORD`|Posição relativa do símbolo em seu bloco.|  
|[IDiaSymbol::get\_symTag](../Topic/IDiaSymbol::get_symTag.md)|`DWORD`|Retorna `SymTagPublicSymbol` \(uma da [Enumeração SymTagEnum](../../debugger/debug-interface-access/symtagenum.md) valores\).|  
|[IDiaSymbol::get\_undecoratedName](../../debugger/debug-interface-access/idiasymbol-get-undecoratedname.md)|`BSTR`|O nome não decorado do símbolo.|  
|[IDiaSymbol::get\_undecoratedNameEx](../../debugger/debug-interface-access/idiasymbol-get-undecoratednameex.md)|`BSTR`|Parte ou todo o nome não decorado do símbolo.|  
  
## Consulte também  
 [Hierarquia lexical de tipos de símbolos](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)   
 [Enumeração LocationType](../../debugger/debug-interface-access/locationtype.md)   
 [Locais de símbolos](../../debugger/debug-interface-access/symbol-locations.md)