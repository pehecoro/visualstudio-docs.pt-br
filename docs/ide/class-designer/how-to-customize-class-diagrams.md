---
title: Como personalizar diagramas de classe (Designer de Classe) | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-general
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- class diagrams, customizing
- shapes, removing type from class diagrams
- type shapes, removing from class diagrams
- class diagrams, removing type shapes
ms.assetid: e9030aea-c77d-4cc1-b8f6-b6ca469b692d
caps.latest.revision: "29"
author: gewarren
ms.author: gewarren
manager: ghogen
ms.workload: multiple
ms.openlocfilehash: ab6776ccdf8f3abe98190855ec41dc226677db61
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-customize-class-diagrams-class-designer"></a>Como personalizar diagramas de classe (Designer de Classe)
É possível alterar como os diagramas de classes exibem informações. Você pode personalizar o diagrama inteiro ou os tipos individuais na superfície de design.  
  
Por exemplo, é possível ajustar o nível de zoom de um diagrama de classes inteiro, alterar como os membros de tipo individual são agrupados e classificados, ocultar ou mostrar relações, bem como mover tipos individuais ou em conjunto para qualquer lugar no diagrama.  
  
> [!NOTE]
>  Personalizar a maneira como as formas aparecem no diagrama não altera o código subjacente dos tipos representados no diagrama.  
  
As seções que contêm membros de tipo, como a seção Propriedades em uma classe, são chamadas de compartimentos. Você pode ocultar ou mostrar compartimentos individuais e membros de tipo.  
  
**Neste tópico**  
  
-   [Ampliar e reduzir o diagrama de classe](how-to-customize-class-diagrams.md#ZoomInOut)  
  
-   [Personalizar o agrupamento e a classificação dos membros de tipo](how-to-customize-class-diagrams.md#CustomizeGroupingSorting)  
  
-   [Ocultar compartimentos em um tipo](how-to-customize-class-diagrams.md#HideCompartments)  
  
-   [Ocultar membros individuais em um tipo](how-to-customize-class-diagrams.md#HideMembers)  
  
-   [Mostrar compartimentos e membros ocultos em um tipo](how-to-customize-class-diagrams.md#DisplayHiddenCompartmentsAndMemberrs)  
  
-   [Ocultar relações](how-to-customize-class-diagrams.md#HideAssociationAndInheritance)  
  
-   [Mostrar relações ocultas](how-to-customize-class-diagrams.md#DisplayAssociationAndInheritance)  
  
-   [Remover uma forma de um diagrama de classe](how-to-customize-class-diagrams.md#RemoveCodeAndShape)  
  
-   [Excluir uma forma de tipo e seu código subjacente](how-to-customize-class-diagrams.md#DeleteTypeShapeAndCode)  
  
##  <a name="ZoomInOut"></a> Ampliar e reduzir o diagrama de classe  
  
1.  Abra e selecione um arquivo de diagrama de classes no Designer de Classe.  
  
2.  Na barra de ferramentas do Designer de Classe, clique no botão **Ampliar** ou **Reduzir** para alterar o nível de zoom da superfície do designer.  
  
     ou  
  
     Especifique um determinado valor de zoom. É possível usar a lista suspensa **Aplicar Zoom** ou digitar um nível de zoom válido (o intervalo válido é entre 10% e 400%).  
  
    > [!NOTE]
    >  Alterar o nível de zoom não afeta a escala de impressão do seu diagrama de classes.  
  
##  <a name="CustomizeGroupingSorting"></a> Personalizar o agrupamento e a classificação dos membros de tipo  
  
1.  Abra e selecione um arquivo de diagrama de classes no Designer de Classe.  
  
2.  Clique com o botão direito do mouse em uma área vazia na superfície de design e aponte para **Membros do Grupo**.  
  
3.  Selecione uma das opções disponíveis:  
  
    1.  **Agrupar por Tipo** separa membros de tipo individuais em uma lista agrupada de Propriedades, Métodos, Eventos e Campos. Os grupos individuais dependem da definição das entidades: por exemplo, uma classe não exibirá nenhum grupo de eventos se ainda não houver eventos definidos para essa classe.  
  
    2.  **Agrupar por Acesso** separa membros de tipo individuais em uma lista agrupada com base nos modificadores de acesso do membro. Por exemplo, Público ou Privado.  
  
    3.  **Classificar em Ordem Alfabética** exibe os itens que compõem uma entidade como uma única lista alfabetizada. A lista é classificada em ordem crescente.  
  
##  <a name="HideCompartments"></a> Ocultar compartimentos em um tipo  
  
1.  Abra e selecione um arquivo de diagrama de classes no designer de classe.  
  
2.  Clique com o botão direito do mouse na categoria do membro no tipo que você deseja personalizar (por exemplo, selecione o nó **Métodos** em uma classe).  
  
3.  Clique em **Ocultar Compartimento**.  
  
     O compartimento selecionado desaparece do contêiner de tipo.  
  
##  <a name="HideMembers"></a> Ocultar membros individuais em um tipo  
  
1.  Abra e selecione um arquivo de diagrama de classes no Designer de Classe.  
  
2.  Clique com o botão direito do mouse no membro do tipo que deseja ocultar.  
  
3.  Clique em **Ocultar**.  
  
     O membro selecionado desaparece do contêiner de tipo.  
  
##  <a name="DisplayHiddenCompartmentsAndMemberrs"></a> Mostrar compartimentos e membros ocultos em um tipo  
  
1.  Abra e selecione um arquivo de diagrama de classes no Designer de Classe.  
  
2.  Clique com o botão direito do mouse no nome do tipo com o compartimento oculto.  
  
3.  Clique em **Mostrar Todos os Membros**.  
  
     Todos os membros e compartimentos ocultos aparecem no contêiner de tipo.  
  
##  <a name="HideAssociationAndInheritance"></a> Ocultar relações  
  
1.  Abra e selecione um arquivo de diagrama de classes no Designer de Classe.  
  
2.  Clique com o botão direito do mouse na linha de herança ou associação que deseja ocultar.  
  
3.  Clique em **Ocultar** para linhas de associação e em **Ocultar Linha de Herança** para linhas de herança.  
  
4.  Clique em **Mostrar Todos os Membros**.  
  
     Todos os membros e compartimentos ocultos aparecem no contêiner de tipo.  
  
##  <a name="DisplayAssociationAndInheritance"></a> Mostrar relações ocultas  
  
1.  Abra e selecione um arquivo de diagrama de classes no Designer de Classe.  
  
2.  Clique com o botão direito do mouse no tipo com a associação ou a herança oculta.  
  
 Clique em **Mostrar Todos os Membros** para linhas de associação e em **Mostrar Classe Base** ou **Mostrar Classes Derivadas** para linhas de herança.  
  
##  <a name="RemoveCodeAndShape"></a> Remover uma forma de um diagrama de classe  
Você pode remover uma forma de tipo do diagrama de classes sem afetar o código subjacente do tipo. Remover formas de tipo de um diagrama de classes afeta somente esse diagrama: o código subjacente que define o tipo e outros diagramas que exibem o tipo não são afetados.  
  
1.  No diagrama de classes, selecione a forma de tipo que deseja remover do diagrama.  
  
2.  No menu **Editar**, escolha **Remover do Diagrama**.  
  
     A forma de tipo e todas as linhas de associação ou herança conectadas à forma não aparecem mais no diagrama.  
  
##  <a name="DeleteTypeShapeAndCode"></a> Excluir uma forma de tipo e seu código subjacente  
  
1.  Clique com o botão direito do mouse na forma, na superfície de design.  
  
2.  Selecione **Excluir Código** no menu de contexto.  
  
     A forma é removida do diagrama e seu código subjacente é excluído do projeto.  
  
## <a name="see-also"></a>Consulte também
[Trabalhando com diagramas de classe](working-with-class-diagrams.md)   
[Como alternar entre notação de membro e de associação](how-to-change-between-member-notation-and-association-notation.md)   
[Como exibir tipos existentes](how-to-view-existing-types.md)   
[Exibindo tipos e relações](viewing-types-and-relationships.md)