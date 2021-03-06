---
title: 'Como: criar um aplicativo de Console do fluxo de trabalho | Microsoft Docs'
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 51a2eea7-921c-49f1-b358-68afc27f1ee9
caps.latest.revision: "16"
author: ErikRe
ms.author: erikre
manager: erikre
ms.workload: multiple
ms.openlocfilehash: fcadbe113e92c761559161bdd8a7eba6e95937d3
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-create-a-workflow-console-application"></a>Como: Crie um aplicativo de console do fluxo de trabalho
[!INCLUDE[wf](../workflow-designer/includes/wf_md.md)] permite que você crie fluxos de trabalho para executar o sistema ou processos humanos. [!INCLUDE[wfd1](../workflow-designer/includes/wfd1_md.md)] fornece a superfície de design para criar esses fluxos de trabalho. [!INCLUDE[wfd2](../workflow-designer/includes/wfd2_md.md)] pode ser usado para criar fluxos de trabalho dentro de [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ou pode ser integrado em outros aplicativos que rehost o designer.  
  
 Este tópico descreve como usar [!INCLUDE[wfd2](../workflow-designer/includes/wfd2_md.md)] em [!INCLUDE[vs2010](../misc/includes/vs2010_md.md)] para criar um fluxo de trabalho em um aplicativo de console.  
  
### <a name="to-create-a-workflow-console-application"></a>Para criar um aplicativo de console do fluxo de trabalho  
  
1.  Inicie o [!INCLUDE[vs2010](../misc/includes/vs2010_md.md)].  
  
2.  Sobre o **arquivo** , aponte para **novo**e, em seguida, selecione **projeto...** .  
  
     A caixa de diálogo **Novo Projeto** é aberta.  
  
3.  No **modelos instalados** painel, selecione **fluxo de trabalho** do **Visual C#** ou **Visual Basic** agrupamentos, dependendo de sua idioma de preferência.  
  
4.  No painel central, selecione **aplicativo de Console do fluxo de trabalho**.  
  
5.  No **nome** , digite um nome descritivo para o seu projeto tornar mais fácil de identificar.  
  
6.  No **local** , digite o diretório no qual você deseja salvar o projeto ou clique em **procurar** para navegar até ele.  
  
7.  No **solução** , digite o nome para a nova solução. Clique em **Okey** para criar o aplicativo.  
  
    > [!NOTE]
    >  Se você quiser adicionar um aplicativo de console do fluxo de trabalho a uma solução existente, abra essa solução no [!INCLUDE[vs2010](../misc/includes/vs2010_md.md)], clique com botão direito da solução de **Solution Explorer**e selecione **adicionar**, em seguida,  **Novo projeto...**  para abrir o **novo projeto** caixa de diálogo. Continuar conforme descrito acima neste procedimento.  
  
8.  O modelo de projeto cria uma definição de fluxo de trabalho em XAML e a definição de aplicativo de console está no código-fonte. [!INCLUDE[wfd2](../workflow-designer/includes/wfd2_md.md)] abre e exibe a tela para o fluxo de trabalho que você criou.  
  
9. Para criar um fluxo de trabalho, arraste atividades ou outros itens de fluxo de trabalho do **caixa de ferramentas** à superfície de design do fluxo de trabalho.  
  
## <a name="see-also"></a>Consulte também  
 [Criando um projeto de fluxo de trabalho](../workflow-designer/creating-a-workflow-project.md)