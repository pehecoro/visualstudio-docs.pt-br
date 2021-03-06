---
title: "Caixa de diálogo ambiguidade resolver | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-debug
ms.tgt_pltfrm: 
ms.topic: reference
f1_keywords: vs.debug.Disambig
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Resolve Ambiguity dialog box
- debugger, Resolve Ambiguity dialog box
- debugging [C++], resolving ambiguity
ms.assetid: d9f47455-a116-4c84-8bad-2dfbf4d77f74
caps.latest.revision: "7"
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.workload: multiple
ms.openlocfilehash: 62b41d5345d1a17781e4e9490abedbd0c169f393
ms.sourcegitcommit: 9e6ff74da1afd8bd2f0e69387ce81f2a74619182
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/04/2018
---
# <a name="resolve-ambiguity-dialog-box"></a>Caixa de diálogo Resolver Ambiguidade
A caixa de diálogo `Resolve Ambiguity` aparece quando o depurador não pode escolher o local para exibir. Por exemplo, se você estiver usando modelos C++, poderá criar várias funções de um único modelo da função. Se o depurador para em um local de origem no modelo, e você escolher `Go To Disassembly`, o depurador tem várias opções. Cada função criada do modelo tem seu próprio código de desmontagem, e o depurador não sabe qual código você deseja exibir. A caixa de diálogo `Resolve Ambiguity` permite que você selecione o local desejado de uma lista de todos os locais correspondentes.  
  
 `Choose the specific location`  
 Lista todos os lugares que correspondem ao comando.  
  
 `Address`  
 Mostra os endereços de memória para cada função.  
  
 `Function`  
 Mostra o nome de cada função.  
  
 `Module`  
 Mostra o módulo (EXE ou DLL) que contém o código de objeto para a função.  
  
## <a name="see-also"></a>Consulte também  
 [Expressões no depurador](../debugger/expressions-in-the-debugger.md)