---
title: "Parâmetros opcionais em soluções do Office | Microsoft Docs"
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
- Office applications [Office development in Visual Studio], optional parameters
- Visual C# [Office development in Visual Studio], optional parameters
- Visual Basic [Office development in Visual Studio], optional parameters
- application development [Office development in Visual Studio], optional parameters
- missing field [Office development in Visual Studio]
- optional parameters [Office development in Visual Studio]
- parameters [Office development in Visual Studio], optional
author: TerryGLee
ms.author: tglee
manager: ghogen
ms.workload: office
ms.openlocfilehash: fe40b6bc0af9df294408079c8a27dfac42df97b0
ms.sourcegitcommit: f9fbf1f55f9ac14e4e5c6ae58c30dc1800ca6cda
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/10/2018
---
# <a name="optional-parameters-in-office-solutions"></a>Parâmetros opcionais em soluções do Office
  Muitos métodos nos modelos de objeto dos aplicativos do Microsoft Office aceitam parâmetros opcionais. Se você usar o Visual Basic para desenvolver uma solução do Office no Visual Studio, você não precisa passar um valor para parâmetros opcionais, como os valores padrão são usados automaticamente para cada parâmetro ausente. Na maioria dos casos, você também pode omitir os parâmetros opcionais em projetos do Visual c#. No entanto, você não pode omitir opcional **ref** parâmetros de `ThisDocument` classe em projetos de nível de documento do Word.  
  
 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]  
  
 Para obter mais informações sobre como trabalhar com parâmetros opcionais em projetos do Visual c# e Visual Basic, consulte [&#40; nome e argumentos opcionais C &#35; Guia de programação &#41; ](/dotnet/csharp/programming-guide/classes-and-structs/named-and-optional-arguments) e [parâmetros opcionais &#40; Visual Basic &#41; ](/dotnet/visual-basic/programming-guide/language-features/procedures/optional-parameters).  
  
> [!NOTE]  
>  Em versões anteriores do Visual Studio, você deve passar um valor para cada parâmetro opcional em projetos do Visual c#. Para sua conveniência, esses projetos incluem uma variável global chamada `missing` que você pode passar para um parâmetro opcional quando você deseja usar o valor padrão do parâmetro. Projetos Visual c# para o Office no Visual Studio ainda incluam o `missing` variável, mas você normalmente não é necessário usá-lo ao desenvolver soluções do Office em [!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)], exceto quando você chama métodos com opcional **ref** parâmetros de `ThisDocument` classe em projetos de nível de documento para Word.  
  
## <a name="example-in-excel"></a>Exemplo do Excel  
 O <xref:Microsoft.Office.Tools.Excel.Worksheet.CheckSpelling%2A> método tem muitos parâmetros opcionais. Você pode especificar valores para alguns parâmetros e aceitar o valor padrão de outras pessoas, conforme mostrado no exemplo de código a seguir. Este exemplo requer que um projeto no nível do documento com uma classe de planilha denominada `Sheet1`.  
  
 [!code-csharp[Trin_VstrefGeneralExcel#1](../vsto/codesnippet/CSharp/excelworkbook1/Sheet1.cs#1)]
 [!code-vb[Trin_VstrefGeneralExcel#1](../vsto/codesnippet/VisualBasic/excelworkbook1/Sheet1.vb#1)]  
  
## <a name="example-in-word"></a>Exemplo no Word  
 O <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> método tem muitos parâmetros opcionais. Você pode especificar valores para alguns parâmetros e aceitar o valor padrão de outras pessoas, conforme mostrado no exemplo de código a seguir.  
  
 [!code-vb[Trin_VstrefGeneralWord#1](../vsto/codesnippet/VisualBasic/worddocument1/ThisDocument.vb#1)]
 [!code-csharp[Trin_VstrefGeneralWord#1](../vsto/codesnippet/CSharp/worddocument1/ThisDocument.cs#1)]  
  
## <a name="using-optional-parameters-of-methods-in-the-thisdocument-class-in-visual-c-document-level-projects-for-word"></a>Usando parâmetros opcionais dos métodos na classe ThisDocument em projetos Visual c# no nível de documento para Word  
 O modelo de objeto do Word contém vários métodos com opcional **ref** parâmetros que aceitam <xref:System.Object> valores. No entanto, você não pode omitir opcional **ref** parâmetros dos métodos de gerado `ThisDocument` classe no Visual c# projetos no nível de documento para Word. Visual c# permite omitir opcional **ref** parâmetros apenas para os métodos das interfaces, não classes. Por exemplo, o exemplo de código a seguir não é compilado, porque você não pode omitir opcional **ref** parâmetros do <xref:Microsoft.Office.Tools.Word.DocumentBase.CheckSpelling%2A> método o `ThisDocument` classe.  
  
 [!code-csharp[Trin_VstrefGeneralWord#3](../vsto/codesnippet/CSharp/worddocument1/ThisDocument.cs#3)]  
  
 Quando você chama os métodos para o `ThisDocument` de classe, siga estas diretrizes:  
  
-   Para aceitar o valor padrão de um recurso opcional **ref** parâmetro, passe o `missing` variável para o parâmetro. O `missing` variável é definida automaticamente em projetos do Visual c# Office e é atribuído ao valor <xref:System.Type.Missing> no código de projeto gerado.  
  
-   Para especificar seu próprio valor para um recurso opcional **ref** parâmetro, declare um objeto que é atribuído ao valor que você deseja especificar e, em seguida, passar o objeto para o parâmetro.  
  
 O exemplo de código a seguir demonstra como chamar o <xref:Microsoft.Office.Tools.Word.DocumentBase.CheckSpelling%2A> método especificando um valor para o *ignoreUppercase* parâmetro e aceitar o valor padrão para os outros parâmetros.  
  
 [!code-csharp[Trin_VstrefGeneralWord#4](../vsto/codesnippet/CSharp/worddocument1/ThisDocument.cs#4)]  
  
 Se você quiser escrever código que omite opcional **ref** parâmetros de um método no `ThisDocument` classe, você pode também chamar o mesmo método no <xref:Microsoft.Office.Interop.Word.Document> objeto retornado pelo <xref:Microsoft.Office.Tools.Word.Document.InnerObject%2A> propriedade e omitir o parâmetros do método. Você pode fazer isso porque <xref:Microsoft.Office.Interop.Word.Document> é uma interface, em vez de uma classe.  
  
 [!code-csharp[Trin_VstrefGeneralWord#5](../vsto/codesnippet/CSharp/worddocument1/ThisDocument.cs#5)]  
  
 Para obter mais informações sobre parâmetros de tipo de valor e referência, consulte [passando argumentos por valor e por referência &#40; Visual Basic &#41; ](/dotnet/visual-basic/programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference) (para Visual Basic) e [passando parâmetros &#40; C &#35; Guia de programação &#41; ](/dotnet/csharp/programming-guide/classes-and-structs/passing-parameters).  
  
## <a name="see-also"></a>Consulte também  
 [Desenvolvendo soluções do Office](../vsto/developing-office-solutions.md)   
 [Escrevendo código em soluções do Office](../vsto/writing-code-in-office-solutions.md)  
  
  