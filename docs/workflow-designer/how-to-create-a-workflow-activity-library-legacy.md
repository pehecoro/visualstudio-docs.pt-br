---
title: 'Como: criar uma biblioteca de atividades de fluxo de trabalho (legados) | Microsoft Docs'
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- workflows, activity library projects
- workflow activity libraries
- projects, workflow activity libraries
ms.assetid: fb5aa940-2ae8-4b52-b52c-51c20861a7b4
caps.latest.revision: "8"
author: ErikRe
ms.author: erikre
manager: erikre
ms.workload: multiple
ms.openlocfilehash: 35b21f8d85e1634f954d98df47de9e335280ab31
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-create-a-workflow-activity-library-legacy"></a>Como: Crie uma biblioteca de atividade de fluxo de trabalho (o legados)
Siga estas etapas para criar um projeto de biblioteca de atividade de fluxo de trabalho usando [!INCLUDE[wfd1](../workflow-designer/includes/wfd1_md.md)] herdado fornecido por [!INCLUDE[vs2010](../misc/includes/vs2010_md.md)]. Use [!INCLUDE[wfd2](../workflow-designer/includes/wfd2_md.md)] herdado quando você precisa definir como alvo [!INCLUDE[netfx35_long](../workflow-designer/includes/netfx35_long_md.md)] ou [!INCLUDE[vstecwinfx](../workflow-designer/includes/vstecwinfx_md.md)].  
  
### <a name="to-create-a-workflow-activity-library-project"></a>Para criar um projeto de biblioteca de atividade de fluxo de trabalho  
  
1.  Inicie o Visual Studio.  
  
2.  Sobre o **arquivo** , aponte para **novo**e, em seguida, selecione **projeto**.  
  
     A caixa de diálogo **Novo Projeto** é aberta.  
  
3.  Selecione o **.NET Framework 3.0** opção ou **.NET Framework 3.5** opção no menu suspenso na parte superior da lista da **novo projeto** janela para acessar o designer herdado.  
  
    > [!NOTE]
    >  A opção padrão na [!INCLUDE[vs2010](../misc/includes/vs2010_md.md)] é **.NET Framework 4**. Essa opção é usada criar aplicativos de [!INCLUDE[wf](../workflow-designer/includes/wf_md.md)] que direcionam [!INCLUDE[netfx40_short](../workflow-designer/includes/netfx40_short_md.md)] e usa o designer herdado.  
  
4.  No **tipos de projeto** painel, selecione Visual c# ou Visual Basic (em **outras linguagens**) e, em seguida, selecione **fluxo de trabalho**.  
  
5.  No **modelos** painel, selecione **biblioteca de atividades de fluxo de trabalho**.  
  
6.  No **nome** , digite um nome descritivo para o seu projeto tornar mais fácil de identificar.  
  
7.  No **local** , digite o diretório no qual você deseja salvar o projeto ou clique em **procurar** para navegar até ele.  
  
     Se você desejar um diretório da solução para o projeto, selecione o **criar diretório para solução** caixa de seleção e insira um nome no **nome da solução** caixa.  
  
8.  Clique em **OK**.  
  
## <a name="see-also"></a>Consulte também  
 [Criando projetos de fluxo de trabalho herdado](../workflow-designer/creating-legacy-workflow-projects.md)   
 [Usando o Designer de atividade herdado](../workflow-designer/using-the-legacy-activity-designer.md)   
 [Atividades de fluxo de trabalho herdados](../workflow-designer/legacy-workflow-activities.md)   
 [Desenvolvimento de atividades de fluxo de trabalho](http://msdn.microsoft.com/en-us/19876dfc-dfa5-4d52-b1f5-1d087474cc52)   
 [Atividades do Windows Workflow Foundation](http://msdn.microsoft.com/en-us/192c4c1e-afb6-4f58-ab11-2b5bbbc2d2c0)