---
title: "Como: adicionar atividades à caixa de ferramentas | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: b3a8a785-5928-457a-8a50-30267e29503d
caps.latest.revision: "16"
author: ErikRe
ms.author: erikre
manager: erikre
ms.workload: multiple
ms.openlocfilehash: aff3172f5f01612923e72ad76f85205af0c31a72
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-add-activities-to-the-toolbox"></a>Como: Adicione atividades a caixa de ferramentas
As atividades podem ser adicionadas para o **caixa de ferramentas** em sua solução de várias maneiras diferentes. Você pode adicioná-los do seu projeto atual, referênciá-los de um projeto diferente, ou referênciá-los de um conjunto diferente.  
  
### <a name="to-add-an-activity-from-within-your-current-project"></a>Para adicionar uma atividade do seu projeto atual  
  
1.  Adicionar uma nova atividade personalizado ao seu projeto atual de fluxo de trabalho. [!INCLUDE[crabout](../test/includes/crabout_md.md)]Adicionar uma nova atividade personalizada ao seu projeto, consulte [como: adicionar um novo Item a um projeto de fluxo de trabalho](../workflow-designer/how-to-add-a-new-item-to-a-workflow-project.md).  
  
2.  Adicione lógica personalizada para a atividade.  
  
3.  Compile o projeto. Se a compilação for bem-sucedida, uma nova categoria no **caixa de ferramentas** chamado "\<*nome do projeto*>" com a atividade personalizada incluída nessa categoria é exibida.  
  
    > [!NOTE]
    >  Se a caixa de ferramentas é reiniciada, as atividades personalizados serão removidas, mesmo se a solução é compilado novamente. Para preencher novamente a caixa de ferramentas com atividades personalizados depois que redefinido, reinicie [!INCLUDE[vs2010](../misc/includes/vs2010_md.md)].  
  
    > [!NOTE]
    >  A caixa de ferramentas só pode mostrar uma atividade de um determinado nome. Se duas atividades diferentes assemblies com o mesmo nome de classe, somente um exibirá.  
  
    > [!NOTE]
    >  O domínio de aplicativo é compartilhado entre instâncias do editor; se as variáveis estáticas são usados, serão compartilhados entre instâncias do editor também. Se esse não é o comportamento desejado, um serviço deve ser usado para controlar instâncias variáveis. Consulte [usando o contexto de edição de ModelItem](/dotnet/framework/windows-workflow-foundation/using-the-modelitem-editing-context) para obter informações sobre como usar serviços dentro do designer.  
  
### <a name="to-add-an-activity-from-within-a-different-project"></a>Para adicionar uma atividade de dentro de um projeto diferente  
  
1.  Abra uma solução que contém pelo menos um projeto de fluxo de trabalho e um projeto personalizado de biblioteca de atividade ou outro projeto de fluxo de trabalho que define uma atividade personalizado.  
  
2.  Criar ambos os projetos. Se as compilações foram bem-sucedidas, uma nova categoria no **caixa de ferramentas** chamado "\<*nome do projeto*>" com a atividade personalizada incluída nessa categoria é exibida.  
  
### <a name="to-add-an-activity-to-the-toolbox-from-an-assembly"></a>Para adicionar uma atividade à caixa de ferramentas de um assembly  
  
1.  Abra uma solução de fluxo de trabalho.  
  
2.  Do **ferramentas** menu, selecione **escolher itens da caixa de ferramentas...** .  
  
3.  No **escolher itens da caixa de ferramentas** caixa de diálogo, selecione o **componentes do System. Activities** guia e clique em **procurar...**  para navegar para o assembly que contém a atividade personalizada que você deseja adicionar.  
  
4.  Selecione o assembly e clique em **Okey**. O componente personalizado de atividade é adicionado à lista de componentes e automaticamente selecionado.  
  
    1.  Clique em **Okey** para fechar a caixa de diálogo.  
  
5.  Para exibir a caixa de ferramentas, selecione **caixa de ferramentas** do **exibição** menu.  
  
6.  A atividade personalizada aparece no **caixa de ferramentas** sob a categoria que estava em foco antes que o item foi adicionado. Por exemplo, se o **geral** selecionada na categoria de **caixa de ferramentas** antes de adicionar o item de caixa de ferramentas, a atividade aparece sob o **geral** categoria.  
  
## <a name="see-also"></a>Consulte também  
 [Usando o Designer de Fluxo de Trabalho](../workflow-designer/using-the-workflow-designer.md)