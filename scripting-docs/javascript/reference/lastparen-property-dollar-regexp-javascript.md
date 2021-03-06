---
title: Propriedade lastParen ($ +) (RegExp) (JavaScript) | Microsoft Docs
ms.custom: 
ms.date: 01/18/2017
ms.prod: windows-client-threshold
ms.reviewer: 
ms.suite: 
ms.technology: devlang-javascript
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: $+
dev_langs:
- JavaScript
- TypeScript
- DHTML
helpviewer_keywords: lastParen property ($+)
ms.assetid: 18aca591-a97a-48da-8b06-422346804b16
caps.latest.revision: "12"
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 059cfc6556873d770798eff59bf7415426526626
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
---
# <a name="lastparen-property--regexp-javascript"></a>Propriedade lastParen ($+) (RegExp) (JavaScript)
Retorna a último subcorrespondência entre parênteses de qualquer pesquisa de expressão regular, se houver. Somente leitura.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
RegExp.lastParen  
```  
  
## <a name="remarks"></a>Comentários  
 O objeto associado a essa propriedade é sempre global `RegExp` objeto.  
  
 O valor inicial de `lastParen` propriedade é uma cadeia de caracteres vazia. O valor de `lastParen` propriedade alterada sempre que uma correspondência é feita.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir ilustra o uso da propriedade `lastParen`:  
  
```JavaScript  
// Create the regular expression pattern.  
var re = new RegExp("d(b+)(d)","ig");  
var str = "cdbBdbsbdbdz";  
  
// Perform the search.  
var arr = re.exec(str);  
  
// Print the output.  
var s = ""   
s += "$1: " + RegExp.$1 + "<br />";  
s += "$2: " + RegExp.$2 + "<br />";  
s += "$3: " + RegExp.$3 + "<br />";  
s += "input: " + RegExp.input + "<br />";  
s += "lastMatch: " + RegExp.lastMatch + "<br />";  
s += "leftContext: " + RegExp.leftContext + "<br />";  
s += "rightContext: " + RegExp.rightContext + "<br />";   
s += "lastParen: " + RegExp.lastParen + "<br />";  
  
document.write(s);  
```  
  
## <a name="requirements"></a>Requisitos  
 [!INCLUDE[jsv55](../../javascript/reference/includes/jsv55-md.md)]  
  
 **Aplica-se a**: [objeto RegExp](../../javascript/reference/regexp-object-javascript.md)  
  
## <a name="see-also"></a>Consulte também  
 [US $1... $9 propriedades (RegExp)](../../javascript/reference/dollar-1-dot-dot-dot-dollar-9-properties-regexp-javascript.md)   
 [Propriedade Index (RegExp)](../../javascript/reference/index-property-regexp-javascript.md)   
 [Propriedade Input ($_) (RegExp)](../../javascript/reference/input-property-dollar-regexp-javascript.md)   
 [Propriedade lastIndex (RegExp)](../../javascript/reference/lastindex-property-regexp-javascript.md)   
 [Propriedade lastMatch ($&) (RegExp)](../../javascript/reference/lastmatch-property-dollar-regexp-javascript.md)   
 [Propriedade leftContext ($') (RegExp)](../../javascript/reference/leftcontext-property-dollar-grave-regexp-javascript.md)   
 [Propriedade rightContext ($') (RegExp)](../../javascript/reference/rightcontext-property-dollar-regexp-javascript.md)