---
title: Propriedade prototype (objeto) (JavaScript) | Microsoft Docs
ms.custom: 
ms.date: 01/18/2017
ms.prod: windows-client-threshold
ms.reviewer: 
ms.suite: 
ms.technology: devlang-javascript
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: Prototype
dev_langs:
- JavaScript
- TypeScript
- DHTML
helpviewer_keywords:
- inheritance, objects
- Prototype property
ms.assetid: 9fc434a1-5995-4fcb-a4e8-00e7f615aaa2
caps.latest.revision: "11"
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a73d213b6b17f5046eb1f4c498aeb223f942f2d8
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
---
# <a name="prototype-property-object-javascript"></a>Propriedade prototype (objeto) (JavaScript)
Retorna uma referência ao protótipo para uma classe de objetos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
objectName.prototype  
```  
  
## <a name="remarks"></a>Comentários  
 O argumento `objectName` é o nome de um objeto.  
  
 Use a propriedade `prototype` para fornecer um conjunto básico de funcionalidades para uma classe de objetos. Novas instâncias de um objeto "herdam" o comportamento do protótipo atribuído a ele.  
  
 Por exemplo, para adicionar um método ao objeto `Array` que retorna o valor do maior elemento da matriz, declare a função, adicione-a a `Array.prototype` e use-a.  
  
```JavaScript  
function array_max( ){  
    var i, max = this[0];  
    for (i = 1; i < this.length; i++)  
    {  
    if (max < this[i])  
    max = this[i];  
    }  
    return max;  
}  
Array.prototype.max = array_max;  
var myArray = new Array(7, 1, 3, 11, 25, 9  
);  
document.write(myArray.max());  
  
// Output:  
// 25  
  
```  
  
 Todos os intrínseco [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] objetos têm um `prototype` propriedade é somente leitura. Propriedades e métodos que podem ser adicionados ao protótipo, mas o objeto não pode ser atribuído um protótipo diferente. No entanto, objetos definidos pelo usuário podem ser atribuídos um novo protótipo.  
  
 As listas de método e propriedade para cada objeto intrínseco nesta referência de linguagem indicam quais são parte do protótipo do objeto e quais não são.  
  
## <a name="requirements"></a>Requisitos  
 [!INCLUDE[jsv2](../../javascript/reference/includes/jsv2-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Propriedade constructor (Object)](../../javascript/reference/constructor-property-object-javascript.md)