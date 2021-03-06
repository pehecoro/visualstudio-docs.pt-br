---
title: 'Como: adicionar um novo Item a um projeto de fluxo de trabalho | Microsoft Docs'
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 5c6180ca-af10-4513-b0cb-7d478fd84eab
caps.latest.revision: "14"
author: ErikRe
ms.author: erikre
manager: erikre
ms.workload: multiple
ms.openlocfilehash: e2031f084b11f9879fd94f5d2e454e0966ed3787
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-add-a-new-item-to-a-workflow-project"></a>Como: Adicionar um novo item em um fluxo de trabalho Projeto
Depois de criar um projeto de fluxo de trabalho, você pode adicionar atividades de fluxo de trabalho, designer, e outros itens de [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] familiares ao seu projeto.  
  
 A tabela a seguir lista os itens de [!INCLUDE[wf](../workflow-designer/includes/wf_md.md)] que você pode adicionar a um projeto de fluxo de trabalho.  
  
|Nome|Descrição|  
|----------|-----------------|  
|Atividade|Uma atividade a ser composta de outras atividades. Selecionar este item adiciona o mesmo arquivo XAML para o projeto que você obteria ao selecionar o **biblioteca de atividades** modelo para um novo projeto. [!INCLUDE[crabout](../test/includes/crabout_md.md)]Neste procedimento, consulte [como: criar uma biblioteca de atividades](../workflow-designer/how-to-create-an-activity-library.md).|  
|Designer de Activity|Um designer para personalizar a experiência em tempo de design de uma atividade. Selecionar este item adiciona os mesmos arquivos ao projeto que você obteria ao selecionar o **biblioteca do Designer de atividade** modelo para um novo projeto. [!INCLUDE[crabout](../test/includes/crabout_md.md)]Neste procedimento, consulte [como: criar uma biblioteca do Designer de atividade](../workflow-designer/how-to-create-an-activity-designer-library.md).|  
|Atividade do código|Uma atividade com a lógica de execução gravar no código. Um arquivo de código-fonte com uma substituição do método de <xref:System.Activities.CodeActivity.Execute%2A> é gerado para você.|  
|WCF Serviço de Fluxo de Trabalho|Um serviço de [!INCLUDE[indigo2](../workflow-designer/includes/indigo2_md.md)] compilado usando atividades de fluxo de trabalho. Selecionar este item adiciona os mesmos arquivos ao projeto que você obteria ao selecionar o **aplicativo de serviço de fluxo de trabalho WCF** modelo para um novo projeto. [!INCLUDE[crabout](../test/includes/crabout_md.md)]Neste procedimento, consulte [como: criar um aplicativo de serviço de fluxo de trabalho WCF](../workflow-designer/how-to-create-a-wcf-workflow-service-application.md).|  
  
### <a name="to-add-a-new-item-to-a-workflow-project"></a>Para adicionar um novo item em um fluxo de trabalho projeto  
  
1.  Sobre o **projeto** menu, clique em **Adicionar Novo Item...** .  
  
     O **adicionar um novo Item** caixa de diálogo é aberta.  
  
2.  No **modelos instalados** painel, selecione **fluxo de trabalho** grupo.  
  
3.  Selecione um dos quatro itens. A tabela anterior lista as seleções disponíveis.  
  
4.  Digite um nome apropriado para o item de **nome** caixa na parte inferior da caixa de diálogo.  
  
5.  Clique em **adicionar** para adicionar o item ao projeto de fluxo de trabalho atual.  
  
## <a name="see-also"></a>Consulte também  
 [Criando um projeto de fluxo de trabalho](../workflow-designer/creating-a-workflow-project.md)