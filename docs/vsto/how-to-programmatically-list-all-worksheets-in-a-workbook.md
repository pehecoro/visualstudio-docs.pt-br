---
title: 'Como: programaticamente lista todas as planilhas em uma pasta de trabalho | Microsoft Docs'
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
- workbooks, listing worksheets
- worksheets, listing
author: TerryGLee
ms.author: tglee
manager: ghogen
ms.workload: office
ms.openlocfilehash: 7909e82b57d9d0d06217bfd252aa923d5aee2b20
ms.sourcegitcommit: f9fbf1f55f9ac14e4e5c6ae58c30dc1800ca6cda
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/10/2018
---
# <a name="how-to-programmatically-list-all-worksheets-in-a-workbook"></a>Como listar todas as planilhas em uma pasta de trabalho programaticamente
  O <xref:Microsoft.Office.Interop.Excel.Workbook> classe fornece um <xref:Microsoft.Office.Interop.Excel.Worksheets> objeto. Este objeto contém uma coleção de todos os <xref:Microsoft.Office.Interop.Excel.Worksheet> objetos na pasta de trabalho.  
  
 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]  
  
### <a name="to-list-all-existing-worksheets-in-a-workbook-in-a-document-level-customization"></a>Para listar todas as planilhas existentes em uma pasta de trabalho em uma personalização no nível do documento  
  
1.  Iterar por meio de <xref:Microsoft.Office.Interop.Excel.Worksheets> coleta e envia o nome de cada planilha em uma célula de deslocamento de um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle.  
  
     [!code-csharp[Trin_VstcoreExcelAutomation#21](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#21)]
     [!code-vb[Trin_VstcoreExcelAutomation#21](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#21)]  
  
### <a name="to-list-all-existing-worksheets-in-a-workbook-in-a-vsto-add-in"></a>Para listar todas as planilhas existentes em uma pasta de trabalho em um suplemento do VSTO  
  
1.  Iterar por meio de <xref:Microsoft.Office.Interop.Excel.Worksheets> coleta e envia o nome de cada planilha em uma célula de deslocamento de um <xref:Microsoft.Office.Interop.Excel.Range> objeto.  
  
     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#13](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#13)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#13](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#13)]  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhando com planilhas](../vsto/working-with-worksheets.md)   
 [Como: adicionar novas planilhas a pastas de trabalho programaticamente](../vsto/how-to-programmatically-add-new-worksheets-to-workbooks.md)   
 [Como: programaticamente mover planilhas em pastas de trabalho](../vsto/how-to-programmatically-move-worksheets-within-workbooks.md)   
 [Acesso global a objetos em projetos do Office](../vsto/global-access-to-objects-in-office-projects.md)  
  
  