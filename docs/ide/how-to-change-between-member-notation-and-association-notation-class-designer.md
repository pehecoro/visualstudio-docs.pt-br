---
title: "Como alterar entre notação de membro e notação de associação (Designer de Classe) | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- notation, member
- association notation
- member notation
- notation, association
ms.assetid: 65881c5a-d251-4a36-ad0d-73d088436092
caps.latest.revision: 21
author: kempb
ms.author: kempb
manager: ghogen
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: 5db97d19b1b823388a465bba15d057b30ff0b3ce
ms.openlocfilehash: 30bacff7a117cd1e6bdf7a234652177cbc50b0f2
ms.lasthandoff: 02/22/2017

---
# <a name="how-to-change-between-member-notation-and-association-notation-class-designer"></a>Como alterar entre notação de membro e notação de associação (Designer de Classe)
No Designer de Classe, você pode alterar a maneira como o diagrama de classe representa um relacionamento de associação entre dois tipos de notação de membro para notação de associação e vice-versa. Membros exibidos como linhas de associação geralmente fornecem uma visualização útil de como os tipos estão relacionados.  
  
> [!NOTE]
>  Os relacionamentos de associação podem ser representados como um campo ou uma propriedade de membro. Para alterar notação de membro para notação de associação, um tipo deve ter um membro de outro tipo. Para alterar notação de associação para a notação de membro, os dois tipos devem estar conectados por uma linha de associação. Para obter mais informações, consulte [Como criar associações entre tipos (Designer de Classe)](../ide/how-to-create-associations-between-types-class-designer.md). Se o projeto contiver vários diagramas de classe, as alterações feitas na forma como um diagrama exibe os relacionamentos de associação afetarão somente esse diagrama. Para alterar a maneira como outro diagrama exibe os relacionamentos de associação, abra ou exiba esse diagrama e execute estas etapas.  
  
### <a name="to-change-member-notation-to-association-notation"></a>Para alterar de notação de membro para notação de associação  
  
1.  No nó do projeto no Gerenciador de Soluções, abra um arquivo de diagrama de classe (.cd).  
  
2.  Na forma de tipo no diagrama de classe, clique com o botão direito do mouse na propriedade do membro ou no campo que representa a associação e escolha **Mostrar como Associação**.  
  
    > [!TIP]
    >  Se não houver campos ou propriedades visíveis na forma de tipo, os compartimentos da forma poderão ser recolhidos. Para expandir a forma do tipo, clique duas vezes no nome do compartimento ou clique com o botão direito do mouse na forma de tipo e escolha **Expandir**.  
  
     O membro desaparece do compartimento na forma de tipo e uma linha de associação é exibida para conectar os dois tipos. A linha de associação é rotulada com o nome da propriedade ou do campo.  
  
### <a name="to-change-association-notation-to-member-notation"></a>Para alterar de notação de associação para notação de membro  
  
-   No diagrama de classe, clique com o botão direito do mouse na linha de associação e escolha **Mostrar como Propriedade** ou **Mostrar como Campo**, conforme apropriado.  
  
     A linha de associação desaparece e a propriedade é exibida no compartimento apropriado em sua forma de tipo no diagrama.  
  
## <a name="see-also"></a>Consulte também  
 [Como criar herança entre tipos (Designer de Classe)](../ide/how-to-create-inheritance-between-types-class-designer.md)   
 [Como exibir herança entre tipos (Designer de Classe)](../ide/how-to-view-inheritance-between-types-class-designer.md)   
 [Exibindo tipos e relacionamentos (Designer de Classe)](../ide/viewing-types-and-relationships-class-designer.md)   
 [Como visualizar uma associação de coleções (Designer de Classe)](../ide/how-to-visualize-a-collection-association-class-designer.md)