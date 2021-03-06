---
title: Propriedade Constructor (WeakMap) | Microsoft Docs
ms.custom: 
ms.date: 01/18/2017
ms.prod: windows-client-threshold
ms.reviewer: 
ms.suite: 
ms.technology: devlang-javascript
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 1e3f9333-ce75-4d32-9b14-fbe81fd73dfb
caps.latest.revision: "3"
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 5c7340e1e5eeff9a80e231cf1aa49443adc94e72
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
---
# <a name="constructor-property-weakmap"></a>Propriedade constructor (WeakMap)
Especifica a função que cria um `WeakMap` objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```JavaScript  
weakmap.constructor  
```  
  
## <a name="remarks"></a>Comentários  
 Obrigatório `weakmap` é o nome do `WeakMap` objeto.  
  
 A propriedade `constructor` é um membro do protótipo de cada objeto que tenha um protótipo. Isso inclui todos os objetos JavaScript intrínsecos, exceto os objetos `Global` e `Math`. A propriedade `constructor` contém uma referência para a função que constrói instâncias daquele objeto específico.  
  
## <a name="requirements"></a>Requisitos  
 [!INCLUDE[jsv11](../../javascript/reference/includes/jsv11-md.md)]