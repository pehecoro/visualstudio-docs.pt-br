---
title: "Visão geral do modelo de objeto do Visio | Microsoft Docs"
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
- Visio [Office development in Visual Studio], object model
- object models [Office development in Visual Studio], Office
- object models [Office development in Visual Studio], Visio
- objects [Office development in Visual Studio], Office object models
- Office object models
- Visio object model
author: TerryGLee
ms.author: tglee
manager: ghogen
ms.workload: office
ms.openlocfilehash: e829842f4e530b014a19f69c567a91dc49bd78e6
ms.sourcegitcommit: f9fbf1f55f9ac14e4e5c6ae58c30dc1800ca6cda
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/10/2018
---
# <a name="visio-object-model-overview"></a>Visão geral do modelo de objeto do Visio
  Para desenvolver soluções do Office para Microsoft Office Visio, você pode interagir com o modelo de objeto do Visio. Esse modelo de objeto consiste em classes e interfaces que são fornecidos no assembly de interoperabilidade primário do Visio e são definidos no namespace Microsoft.Office.Interop.Visio.  
  
 Este tópico fornece uma visão geral do modelo de objeto do Visio. Para obter informações sobre como usar o modelo de objeto do Visio para executar tarefas em projetos do Office, consulte os tópicos a seguir:  
  
-   [Trabalhando com documentos do Visio](../vsto/working-with-visio-documents.md)  
  
-   [Trabalhando com formas do Visio](../vsto/working-with-visio-shapes.md)  
  
## <a name="understanding-the-visio-object-model"></a>Noções básicas sobre o modelo de objeto do Visio  
 O Visio fornece muitos objetos com os quais você pode interagir. Esses objetos são organizados em uma hierarquia que segue rigorosamente a interface do usuário. Na parte superior da hierarquia é o [Microsoft.Office.Interop.Visio.Application](https://msdn.microsoft.com/library/office/ff766485.aspx) objeto. Este objeto representa a instância atual do Visio. O objeto Microsoft.Office.Interop.Visio.Application contém os objetos Microsoft.Office.Interop.Visio.Document e Microsoft.Office.Interop.Visio.Page, bem como o Microsoft.Office.Interop.Visio.Documents e Coleções de Microsoft.Office.Interop.Visio.Pages. Cada um desses objetos e coleções tem vários métodos e propriedades que você pode acessar para manipular e interagir com ele.  
  
 Para obter mais informações, consulte a documentação de referência do VBA [Microsoft.Office.Interop.Visio.Application](https://msdn.microsoft.com/library/office/ff766485.aspx), [Microsoft.Office.Interop.Visio.Document](https://msdn.microsoft.com/library/office/ff765575.aspx), e [ Microsoft.Office.Interop.Visio.Page](https://msdn.microsoft.com/library/office/ff767035.aspx) objetos e também o [Microsoft.Office.Interop.Visio.Documents](https://msdn.microsoft.com/library/office/ff768812.aspx) e [Microsoft.Office.Interop.Visio.Pages](https://msdn.microsoft.com/library/office/ff766165.aspx) coleções.  
  
 As seções a seguir descrevem brevemente os objetos de nível superior e como eles interagem entre si. Esses objetos incluem os seguintes objetos:  
  
-   Objeto de aplicativo  
  
-   Objeto de documento  
  
-   Objeto Page  
  
### <a name="application-object"></a>Objeto de aplicativo  
 O objeto Microsoft.Office.Interop.Visio.Application representa o aplicativo do Visio e é o pai de todos os outros objetos. Seus membros geralmente se aplicam para o Visio como um todo. Você pode usar as propriedades e métodos de objetos Microsoft.Office.Interop.Visio.ApplicationSettings e o Microsoft.Office.Interop.Visio.Application para controlar o ambiente do Visio.  
  
 Em projetos de suplemento do VSTO, você pode acessar o objeto Microsoft.Office.Interop.Visio.Application usando o `Application` campo o `ThisAddIn` classe. Para obter mais informações, consulte [Programando suplementos do VSTO](../vsto/programming-vsto-add-ins.md).  
  
### <a name="document-object"></a>Objeto de documento  
 O objeto Microsoft.Office.Interop.Visio.Document é central para programação do Visio. Representa um desenho, estêncil ou arquivo de modelo. Quando você abrir um documento do Visio ou cria um novo documento, você cria um novo objeto Microsoft.Office.Interop.Visio.Document, que é adicionado à coleção Microsoft.Office.Interop.Visio.Documents do objeto Microsoft.Office.Interop.Visio.Application .  
  
 O documento que tem o foco é chamado o documento ativo. Ele é representado pela propriedade Microsoft.Office.Interop.Visio.Application.ActiveDocument do objeto Microsoft.Office.Interop.Visio.Application.  
  
### <a name="page-object"></a>Objeto Page  
 O objeto Microsoft.Office.Interop.Visio.Page representa a área de desenho de uma página de primeiro plano ou um plano de fundo. Você pode usar a propriedade Microsoft.Office.Interop.Visio.Page.Background para determinar se uma página é uma página de primeiro plano ou segundo plano.  
  
 Para criar formas, você pode usar os métodos que incluem os métodos Microsoft.Office.Interop.Visio.Page.DrawSpline e Microsoft.Office.Interop.Visio.Page.DrawOval. Além disso, você pode recuperar os mestres de estênceis e coloque as formas em uma página usando os métodos Microsoft.Office.Interop.Visio.Page.Drop ou Microsoft.Office.Interop.Visio.Page.DropMany.  
  
## <a name="using-the-visio-object-model-documentation"></a>Usando a documentação do modelo de objeto do Visio  
 Para obter informações completas sobre o modelo de objeto do Visio, consulte a referência de modelo de objeto do Visio VBA. A referência de modelo de objeto VBA documenta o modelo de objeto do Visio como ele é exposto para o Visual Basic para código Applications (VBA). Para obter mais informações, consulte [referência de modelo de objeto do Visio 2010](http://go.microsoft.com/fwlink/?LinkId=199775).  
  
 Todos os objetos e membros na referência de modelo de objeto do VBA correspondem aos tipos e membros na assembly de interoperabilidade primária (PIA) do Visio. Por exemplo, o objeto de documento na referência de modelo de objeto do VBA corresponde ao tipo de Microsoft.Office.Interop.Visio.Document no PIA do Visio. Embora a referência de modelo de objeto VBA fornece exemplos de código para a maioria das propriedades, métodos e eventos, você deve converter o código VBA essa referência ao Visual Basic ou Visual c#, se você quiser usá-los em um projeto de suplemento do Visio VSTO que você cria usando Visual Studio.  
  
> [!NOTE]  
>  Neste momento, não há nenhuma documentação de referência para o assembly de interoperabilidade primária do Visio.  
  
 Para exemplos de código relacionadas e ferramentas adicionais para a criação de soluções do Visio, consulte [do Visio 2010 Software Development Kit](http://go.microsoft.com/fwlink/?LinkId=196501).  
  
### <a name="additional-types-in-primary-interop-assemblies"></a>Tipos adicionais de Assemblies de interoperabilidade primários  
 Você pode encontrar tipos em assemblies de interoperabilidade primários que não são visíveis para VBA devido às diferenças de implementação. VBA fornece uma exibição do modelo de objeto do Visio que inclui apenas os objetos e membros que você pode usar diretamente. Os assemblies de interoperabilidade primários expõem o mesmo modelo de objeto, mas eles também incluem outras interfaces, classes e membros que convertem os objetos no modelo de objeto COM para código gerenciado. Esses itens adicionais não se destinam a ser usado diretamente no seu código.  
  
 Para obter mais informações, consulte [visão geral de Classes e Interfaces de Assemblies de interoperabilidade primários do Office](http://go.microsoft.com/fwlink/?LinkId=189592) e [Assemblies de interoperabilidade primários do Office](../vsto/office-primary-interop-assemblies.md).  
  
## <a name="see-also"></a>Consulte também  
 [Soluções do Visio](../vsto/visio-solutions.md)   
 [Trabalhando com documentos do Visio](../vsto/working-with-visio-documents.md)   
 [Trabalhando com formas do Visio](../vsto/working-with-visio-shapes.md)  
  
  