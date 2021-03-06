---
title: InvokeDelegate | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: reference
f1_keywords:
- InvokeDelegate Designer
- System.Activities.Statements.InvokeDelegate.UI
ms.assetid: 289a7498-5127-453f-beb5-05f05b80d26f
caps.latest.revision: "3"
ms.author: sdanie
manager: erikre
ms.workload: multiple
ms.openlocfilehash: 56b132403d51a591a8832c1417bec73bde442266
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="invokedelegate"></a>InvokeDelegate
O **InvokeDelegate** designer é usado para criar e configurar um <xref:System.Activities.Statements.InvokeDelegate> atividade.  
  
## <a name="the-invokedelegate-activity"></a>A atividade de InvokeDelegate  
 <xref:System.Activities.Statements.InvokeDelegate> chama um delegate público.  
  
### <a name="using-the-invokedelegate-activity-designer"></a>Usando o designer de atividade de InvokeDelegate  
 O **InvokeDelegate** designer de atividade pode ser encontrado no **primitivos** categoria do **caixa de ferramentas**, que é acessado clicando o **dacaixadeferramentas** guia [!INCLUDE[wfd2](../workflow-designer/includes/wfd2_md.md)] (como alternativa, selecione **barra de ferramentas** do **exibição** menu ou CTRL + ALT + X.)  
  
 O **InvokeDelegate** designer de atividades pode ser arrastado o **caixa de ferramentas** e removidos no [!INCLUDE[wfd2](../workflow-designer/includes/wfd2_md.md)] superfície onde nunca atividades geralmente são colocados, tais como dentro um <xref:System.Activities.Statements.Sequence>. Isso cria uma atividade de <xref:System.Activities.Statements.InvokeDelegate> com <xref:System.Activities.Activity.DisplayName%2A> padrão de InvokeDelegate. O <xref:System.Activities.Activity.DisplayName%2A> pode ser editado no cabeçalho do **InvokeDelegate** designer de atividade ou o **DisplayName** caixa da grade de propriedade.  
  
### <a name="the-invokedelegate-properties"></a>As propriedades de InvokeDelegate  
 A tabela a seguir mostra as propriedades de <xref:System.Activities.Statements.InvokeDelegate> e descreve como elas são usadas no designer. Essas propriedades podem ser editadas na grade de propriedade e alguns podem ser editados na superfície do designer de [!INCLUDE[wfd2](../workflow-designer/includes/wfd2_md.md)].  
  
|Nome da Propriedade|Necessária|Uso|  
|-------------------|--------------|-----------|  
|<xref:System.Activities.Activity.DisplayName%2A>|False|O nome amigável de atividade de <xref:System.Activities.Statements.InvokeDelegate> . O valor padrão é InvokeDelegate.<br /><br /> Embora não seja necessário <xref:System.Activities.Activity.DisplayName%2A> restrita, é uma prática recomendada usar um.|  
|<xref:System.Activities.Statements.InvokeDelegate.Delegate%2A>|verdadeiro|O nome de <xref:System.Activities.ActivityDelegate> a ser chamado quando a atividade executar. Esta propriedade pode ser editada na superfície de designer. Esta é uma propriedade imperativa.|  
|<xref:System.Activities.Statements.InvokeDelegate.DelegateArguments%2A>|False|A coleção de argumento de representante chamado. As chaves são os nomes dos objetos de parâmetro no <xref:System.Activities.ActivityDelegate> e os valores são os argumentos cujas expressões são avaliadas e atribuídos aos objetos de parâmetro correspondente. Na grade de propriedades, clique no botão reticências a **DelegateArguments** campo, ele exibe o **DelegateArguments** caixa de diálogo para permitir que você defina essa propriedade. Clique o **criar argumento** campo para adicionar os argumentos.|  
  
## <a name="see-also"></a>Consulte também  
 [Como definir e consumir delegados de atividade no Designer de Fluxo de Trabalho](../workflow-designer/how-to-define-and-consume-activity-delegates-in-the-workflow-designer.md)