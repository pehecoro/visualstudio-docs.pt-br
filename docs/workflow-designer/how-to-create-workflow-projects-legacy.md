---
title: 'Como: criar projetos de fluxo de trabalho (legados) | Microsoft Docs'
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- workflow projects, creating
- projects, workflow
ms.assetid: 32299555-662c-469d-a90d-89f4700dc78c
caps.latest.revision: "6"
author: ErikRe
ms.author: erikre
manager: erikre
ms.workload: multiple
ms.openlocfilehash: 1f3dd415646f9205794ed51572ed9dbcfc5b45b5
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-create-workflow-projects-legacy"></a>Como: Criar projetos de fluxo de trabalho (o legados)
Siga estas etapas para criar um projeto de [!INCLUDE[wf](../workflow-designer/includes/wf_md.md)] que tem como alvo [!INCLUDE[netfx35_long](../workflow-designer/includes/netfx35_long_md.md)] ou [!INCLUDE[vstecwinfx](../workflow-designer/includes/vstecwinfx_md.md)]. Este procedimento usa [!INCLUDE[wfd1](../workflow-designer/includes/wfd1_md.md)] herdado fornecido por [!INCLUDE[vs2010](../misc/includes/vs2010_md.md)].  
  
### <a name="to-create-a-workflow-project"></a>Para criar um projeto de fluxo de trabalho  
  
1.  Inicie o [!INCLUDE[vs_current_long](../misc/includes/vs_current_long_md.md)].  
  
2.  Sobre o **arquivo** , aponte para **novo**e, em seguida, selecione **projeto**.  
  
     A caixa de diálogo **Novo Projeto** é aberta.  
  
3.  Selecione o **.NET Framework 3.0** opção ou **.NET Framework 3.5** opção no menu suspenso na parte superior da lista da **novo projeto** janela para acessar o designer herdado.  
  
    > [!NOTE]
    >  A opção padrão na [!INCLUDE[vs2010](../misc/includes/vs2010_md.md)] é **.NET Framework 4**. Essa opção é usada criar aplicativos de [!INCLUDE[wf](../workflow-designer/includes/wf_md.md)] que direcionam [!INCLUDE[netfx40_short](../workflow-designer/includes/netfx40_short_md.md)] e usa o designer herdado.  
  
4.  No **tipos de projeto** painel, selecione os projetos do Visual c# ou Visual Basic e, em seguida, selecione **fluxo de trabalho**.  
  
5.  No **modelos** painel, selecione um dos modelos de projeto instalado:  
  
    -   Aplicativo de console sequencial de fluxo de trabalho  
  
    -   Sequencial biblioteca de fluxo de trabalho  
  
    -   Biblioteca de atividade de fluxo de trabalho  
  
    -   Aplicativo de console do fluxo de trabalho do computador de estado  
  
    -   Biblioteca de fluxo de trabalho do computador de estado  
  
    -   Fluxo de trabalho vazio Projeto  
  
6.  No **nome** , digite um nome descritivo para o seu projeto tornar mais fácil de identificar.  
  
7.  No **local** , digite o diretório no qual você deseja salvar o projeto ou clique em **procurar** para navegar até o diretório.  
  
     Se você desejar um diretório da solução para o projeto, selecione o **criar diretório para solução** caixa de seleção e insira um nome no **nome da solução** caixa.  
  
8.  Clique em **OK**.  
  
## <a name="see-also"></a>Consulte também  
 [Criando projetos herdados de fluxo de trabalho](../workflow-designer/creating-legacy-workflow-projects.md)