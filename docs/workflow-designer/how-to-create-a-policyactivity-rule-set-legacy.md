---
title: 'Como: criar uma regra de PolicyActivity definida (herdado) | Microsoft Docs'
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- PolicyActivity activity, creating rule sets
- Rule Set Editor dialog box
- PolicyActivity activity, selecting rule sets
- Select Rule Set dialog box
- rule sets, creating for PolicyActivity
ms.assetid: f272489d-3342-4511-8b59-6a0fd7a42d70
caps.latest.revision: "4"
author: ErikRe
ms.author: erikre
manager: erikre
ms.workload: multiple
ms.openlocfilehash: 1b57fe5f33bdbc4dfb7ab76856bdd80a3246ea9e
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-create-a-policyactivity-rule-set-legacy"></a>Como: Criar uma regra de PolicyActivity definida (o legados)
Este tópico descreve como criar um conjunto de regras de atividade de política usando o novas [!INCLUDE[wfd1](../workflow-designer/includes/wfd1_md.md)] que direciona [!INCLUDE[netfx35_long](../workflow-designer/includes/netfx35_long_md.md)] ou [!INCLUDE[vstecwinfx](../workflow-designer/includes/vstecwinfx_md.md)].  
  
 Após você ter arrastado um **política** item de atividade do **caixa de ferramentas** à superfície de design de fluxo de trabalho, você deve selecionar uma regra existente ou criar uma nova regra definida para o [PolicyActivity ](http://go.microsoft.com/fwlink?LinkID=65019) atividade. Selecione uma regra existente, definida por meio do [Selecionar regra de caixa de diálogo conjunto (herdado)](../workflow-designer/select-rule-set-dialog-box-legacy.md) e criar conjuntos de regras usando o [definir Editor de caixa de diálogo regra (herdado)](../workflow-designer/rule-set-editor-dialog-box-legacy.md).  
  
> [!NOTE]
>  Você pode abrir o [definir Editor de caixa de diálogo regra (herdado)](../workflow-designer/rule-set-editor-dialog-box-legacy.md) caixa de diálogo diretamente clicando duas vezes em um [PolicyActivity](http://go.microsoft.com/fwlink?LinkID=65019) atividade na superfície de design de fluxo de trabalho.  
  
### <a name="to-select-or-create-a-rule-set-for-a-policyactivity-activity"></a>Para selecionar ou criar uma regra definida para uma atividade de PolicyActivity  
  
1.  Clique com botão direito do [PolicyActivity](http://go.microsoft.com/fwlink?LinkID=65019)e, em seguida, clique em **propriedades** para abrir o **propriedades** janela.  
  
2.  Clique o **RuleSetReference** propriedade.  
  
3.  Realize um dos seguintes procedimentos:  
  
    -   Clique o **RuleSetReference** reticências **[...]** e, em seguida, selecione uma conjunto de regras existente a [Selecionar regra de caixa de diálogo conjunto (herdado)](../workflow-designer/select-rule-set-dialog-box-legacy.md). Então vá para a etapa 10.  
  
         -ou-  
  
    -   Digite um nome para um conjunto de regras. Clique o **RuleSetReference** reticências **[...]** e, em seguida, selecione **editar** no [Selecionar regra de caixa de diálogo conjunto (herdado)](../workflow-designer/select-rule-set-dialog-box-legacy.md).  
  
         -ou-  
  
    -   Digite um nome para um conjunto de regras. Expanda o **RuleSetReference** propriedade e selecione as reticências **[...]**  no **definição de conjunto de regras** propriedade.  
  
         O [definir Editor de caixa de diálogo regra (herdado)](../workflow-designer/rule-set-editor-dialog-box-legacy.md) é aberto.  
  
4.  No [definir Editor de caixa de diálogo regra (herdado)](../workflow-designer/rule-set-editor-dialog-box-legacy.md), clique em **Adicionar regra** para adicionar uma nova regra para o conjunto de regras.  
  
5.  Insira o **nome**, **prioridade**, e **reavaliação** propriedades, ou mantenha os valores padrão.  
  
6.  Digite o texto para o **condição**.  
  
7.  Digite o texto para o **ações, em seguida,** e **ações Else**.  
  
8.  Clique em **Adicionar regra** novamente para adicionar outra regra.  
  
9. Ao terminar, clique em **OK**.  
  
## <a name="see-also"></a>Consulte também  
 [PolicyActivity](http://go.microsoft.com/fwlink?LinkID=65019)   
 [Caixa de diálogo Definir selecione regra (herdado)](../workflow-designer/select-rule-set-dialog-box-legacy.md)   
 [Conjunto de regras de caixa de diálogo do Editor (legados)](../workflow-designer/rule-set-editor-dialog-box-legacy.md)   
 [Usando a atividade de política](http://go.microsoft.com/fwlink?LinkID=65004)   
 [Atividades de fluxo de trabalho herdadas](../workflow-designer/legacy-workflow-activities.md)