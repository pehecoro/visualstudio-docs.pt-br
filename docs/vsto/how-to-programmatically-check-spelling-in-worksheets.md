---
title: 'Como: verificar a ortografia em planilhas programaticamente | Microsoft Docs'
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
- spellchecking
- spelling checker, worksheets
- worksheets, checking spelling
- spelling, checking in worksheets
author: TerryGLee
ms.author: tglee
manager: ghogen
ms.workload: office
ms.openlocfilehash: ed71e56c72a35f891e797b4c930e5ade9e83e332
ms.sourcegitcommit: f9fbf1f55f9ac14e4e5c6ae58c30dc1800ca6cda
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/10/2018
---
# <a name="how-to-programmatically-check-spelling-in-worksheets"></a>Como verificar a ortografia em planilhas programaticamente
  Programaticamente, você pode verificar a ortografia de palavras em uma planilha. O **ortografia** caixa de diálogo aparece automaticamente se há quaisquer palavras escritas de forma incorreta na planilha.  
  
 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]  
  
### <a name="to-check-spelling-in-a-worksheet-in-a-document-level-customization"></a>Para verificar a ortografia em uma planilha em uma personalização no nível do documento  
  
1.  Chamar o <xref:Microsoft.Office.Tools.Excel.Worksheet.CheckSpelling%2A> método da planilha.  
  
     [!code-csharp[Trin_VstcoreExcelAutomation#45](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#45)]
     [!code-vb[Trin_VstcoreExcelAutomation#45](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#45)]  
  
### <a name="to-check-spelling-in-a-worksheet-in-an-vsto-add-in"></a>Para verificar a ortografia em uma planilha em um suplemento do VSTO  
  
1.  Chamar o <xref:Microsoft.Office.Interop.Excel._Worksheet.CheckSpelling%2A> método da planilha ativa.  
  
     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#22](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#22)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#22](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#22)]  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhando com planilhas](../vsto/working-with-worksheets.md)   
 [Como: executar cálculos do Excel](../vsto/how-to-programmatically-run-excel-calculations-programmatically.md)   
 [Controle NamedRange](../vsto/namedrange-control.md)   
 [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)  
  
  