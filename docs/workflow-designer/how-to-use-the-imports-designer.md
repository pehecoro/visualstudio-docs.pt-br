---
title: "Como: usar o Designer de importações | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: reference
f1_keywords:
- System.Activities.Presentation.View.ImportDesigner.UI
ms.assetid: 61328ab6-9b66-4e12-8630-22e30ee8c9d1
caps.latest.revision: 
author: ErikRe
ms.author: erikre
manager: erikre
ms.workload:
- multiple
ms.openlocfilehash: cfa65ee24b99fd81712ec88e45f44bb2ed42c21a
ms.sourcegitcommit: d6327b978661c0a745bf4b59f32d8171607803a3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2018
---
# <a name="how-to-use-the-imports-designer"></a>Como: Use o designer imports
O designer imports permite que você inserir em namespaces para os tipos que você usará em suas expressões. Assim como o **importa** ou **usando** palavras-chave no Visual Basic e c#, especificando namespaces no designer de importações permitem que você simplesmente digite um nome de tipo em uma expressão em vez de um totalmente qualificado nome do tipo de versão.  
  
 O designer imports reage a alterações na interface do usuário e as alterações feitas quando o fluxo de trabalho é salvo. Quando o fluxo de trabalho é salvo, namespaces podem ser adicionados automaticamente ao designer imports. Eles incluem o seguinte:  
  
-   Namespaces para alguns tipos usados em declarações de variável e argumento.  
  
-   Namespaces para alguns tipos usados em expressões.  
  
-   Algumas outras namespaces necessárias para serializar o fluxo de trabalho (por exemplo, namespaces usadas por atividades personalizados soltas no fluxo de trabalho).  
  
 Quando o fluxo de trabalho é salvo, você pode notar que algumas namespaces que você excluiu manualmente que são adicionados automaticamente ao designer imports devido à lógica descrita na lista anterior.  
  
### <a name="to-add-a-namespace-to-the-list-of-imported-namespaces"></a>Para adicionar um namespace à lista de namespaces importados  
  
1.  Abra um aplicativo de serviço do fluxo de trabalho WCF, um aplicativo de console de fluxo de trabalho, ou um projeto de biblioteca de atividade em [!INCLUDE[vs2010](../misc/includes/vs2010_md.md)] ou em um aplicativo de fluxo de trabalho rehosted.  
  
2.  Clique em **Imports** na parte inferior da tela principal. O designer imports aparecerá.  
  
3.  Insira ou selecione em um namespace do controle de lista suspensa na parte superior do designer imports.  
  
     Enquanto você digita, uma lista de namespaces válidas que correspondem aos caracteres tipados aparece.  
  
4.  Pressione **Enter** para adicionar o namespace para a lista.  
  
5.  Se você quiser remover um espaço para nome da lista, selecione o namespace e, em seguida, pressione a **excluir** chave em seu teclado. Observe que um namespace só pode ser excluída se o namespace não é válido por algum motivo, por exemplo se o assembly que contém o namespace não é referenciado pelo projeto.