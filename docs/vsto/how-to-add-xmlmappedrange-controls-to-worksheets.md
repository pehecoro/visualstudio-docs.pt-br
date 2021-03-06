---
title: 'Como: adicionar controles XMLMappedRange a planilhas | Microsoft Docs'
ms.custom: 
ms.date: 02/02/2017
ms.reviewer: 
ms.suite: 
ms.technology: office-development
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- XMLMappedRange control, adding to worksheets
- controls [Office development in Visual Studio], adding to worksheets
author: TerryGLee
ms.author: tglee
manager: ghogen
ms.workload: office
ms.openlocfilehash: 90050da5f5105ab3be4c42bedb1751d9f1664958
ms.sourcegitcommit: f9fbf1f55f9ac14e4e5c6ae58c30dc1800ca6cda
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/10/2018
---
# <a name="how-to-add-xmlmappedrange-controls-to-worksheets"></a>Como adicionar controles XMLMappedRange a planilhas
  Quando você mapear um elemento XML para uma célula no Microsoft Office Excel, o Visual Studio adiciona automaticamente um <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> controle à sua planilha.  
  
 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]  
  
> [!NOTE]  
>  O <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> controle não está disponível no **caixa de ferramentas** ou **fontes de dados** janela. Além disso, você não pode criar <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> controla programaticamente.  
  
### <a name="to-add-an-xmlmappedrange-control-to-a-worksheet"></a>Para adicionar um controle XMLMappedRange a uma planilha  
  
1.  Abra a pasta de trabalho do Excel no designer do Visual Studio.  
  
2.  Abra a planilha em que você deseja adicionar o controle.  
  
3.  Sobre o **desenvolvedor** , clique em **fonte**.  
  
    > [!NOTE]  
    >  Se o **desenvolvedor** guia não estiver visível na faixa de opções, você deve habilitá-lo. Para obter mais informações, consulte [como: Mostrar a guia Desenvolvedor na faixa de opções](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md).  
  
     O **origem XML** será exibido o painel de tarefas.  
  
4.  No **origem XML** painel de tarefas, clique em **mapas XML**.  
  
5.  No **mapas XML** caixa de diálogo, clique em **adicionar**.  
  
     O **origem XML** caixa de diálogo é exibida.  
  
6.  Selecione um esquema XML a partir de **origem XML** caixa de diálogo e clique em **abrir**.  
  
     O esquema é adicionado para o **mapas XML** caixa de diálogo.  
  
7.  No **mapas XML** caixa de diálogo, clique em **Okey**.  
  
8.  Arraste um elemento do **origem XML** painel de tarefas para uma célula na planilha.  
  
     Um <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> é criado e adicionado ao projeto.  
  
    > [!NOTE]  
    >  Se você arrastar um elemento pai do **origem XML** painel de tarefas, uma <xref:Microsoft.Office.Tools.Excel.ListObject> controle é criado.  
  
## <a name="see-also"></a>Consulte também  
 [Controle XmlMappedRange](../vsto/xmlmappedrange-control.md)   
 [Automatizando o Excel usando objetos estendidos](../vsto/automating-excel-by-using-extended-objects.md)   
 [Itens de host e visão geral dos controles de Host](../vsto/host-items-and-host-controls-overview.md)   
 [Limitações programáticas de itens de Host e controles de Host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)   
 [Como mapear esquemas para planilhas dentro do Visual Studio](../vsto/how-to-map-schemas-to-worksheets-inside-visual-studio.md)  
  
  