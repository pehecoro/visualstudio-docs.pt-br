---
title: "Método atEnd (Enumerator) (JavaScript) | Microsoft Docs"
ms.custom: 
ms.date: 01/18/2017
ms.prod: windows-client-threshold
ms.reviewer: 
ms.suite: 
ms.technology: devlang-javascript
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: atEnd
dev_langs:
- JavaScript
- TypeScript
- DHTML
helpviewer_keywords: atEnd method
ms.assetid: 326808fb-9a0f-428e-aff1-b11b237913f1
caps.latest.revision: "17"
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 7b5097d00c11ffafc314264f134aedda3981c8e2
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
---
# <a name="atend-method-enumerator-javascript"></a>Método atEnd (Enumerator) (JavaScript)
Retorna um valor booliano que indica se o enumerador está no final da coleção.  
  
> [!WARNING]
>  Esse objeto é compatível somente com o Internet Explorer.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
myEnum.atEnd()  
```  
  
## <a name="remarks"></a>Comentários  
 Obrigatório *myEnum* referência é qualquer `Enumerator` objeto.  
  
 O `atEnd` método **true** se o item atual é o último na coleção, a coleção está vazia ou o item atual não está definido. Caso contrário, retornará **false**.  
  
## <a name="example"></a>Exemplo  
 No código a seguir, o `atEnd` método é usado para determinar se foi atingido o final de uma lista de unidades:  
  
```JavaScript  
function ShowDrives()  
{  
    var s = "";  
    var bytesPerGB = 1024 * 1024 * 1024;  
  
    var fso = new ActiveXObject("Scripting.FileSystemObject");  
    var e = new Enumerator(fso.Drives);  
  
    e.moveFirst();  
    while (e.atEnd() == false)  
    {  
        var drv = e.item();  
  
        s += drv.Path + " - ";  
  
        if (drv.IsReady)  
        {  
            var freeGB = drv.FreeSpace / bytesPerGB;  
            var totalGB = drv.TotalSize / bytesPerGB;  
  
            s += freeGB.toFixed(3) + " GB free of ";  
            s += totalGB.toFixed(3) + " GB";  
        }  
        else  
        {  
            s += "Not Ready";  
        }  
  
        s += "<br />";  
  
        e.moveNext();  
    }  
    return(s);  
}  
```  
  
## <a name="requirements"></a>Requisitos  
 Tem suporte nos seguintes modos de documentos: Quirks, padrões do Internet Explorer 6, padrões do Internet Explorer 7, padrões do Internet Explorer 8, padrões do Internet Explorer 9 e padrões do Internet Explorer 10. Sem suporte nos aplicativos [!INCLUDE[win8_appname_long](../../javascript/includes/win8-appname-long-md.md)]. Consulte [Informações sobre versão](../../javascript/reference/javascript-version-information.md).  
  
 **Aplica-se a**: [objeto enumerador](../../javascript/reference/enumerator-object-javascript.md)  
  
## <a name="see-also"></a>Consulte também  
 [Método item (Enumerator)](../../javascript/reference/item-method-enumerator-javascript.md)   
 [Método moveFirst (Enumerator)](../../javascript/reference/movefirst-method-enumerator-javascript.md)   
 [Método moveNext (Enumerator)](../../javascript/reference/movenext-method-enumerator-javascript.md)   
 [Objeto Enumerator](../../javascript/reference/enumerator-object-javascript.md)