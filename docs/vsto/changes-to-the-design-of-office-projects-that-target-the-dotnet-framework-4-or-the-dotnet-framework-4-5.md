---
title: "Alterações na estrutura de projetos do Office como destino o .NET Framework 4 ou o .NET Framework 4.5 | Microsoft Docs"
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
- Office development in Visual Studio, what's new
- what's new [Office development in Visual Studio]
author: TerryGLee
ms.author: tglee
manager: ghogen
ms.workload: office
ms.openlocfilehash: 059d259b669e63c26759782010be7ff78691ffc3
ms.sourcegitcommit: f9fbf1f55f9ac14e4e5c6ae58c30dc1800ca6cda
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/10/2018
---
# <a name="changes-to-the-design-of-office-projects-that-target-the-net-framework-4-or-the-net-framework-45"></a>Alterações no design dos projetos do Office destinados ao .NET Framework 4 ou ao .NET Framework 4.5
  A partir do [!INCLUDE[vs_dev10_long](../sharepoint/includes/vs-dev10-long-md.md)], Visual Studio introduziu algumas alterações na estrutura de projetos do Office destinados a [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior. Se você estiver familiarizado com projetos do Office em versões anteriores do Visual Studio, você deve estar atento essas alterações antes de desenvolver projetos do Office que essas versões do .NET Framework 4.0 ou posterior. Por padrão, todos os projetos que você cria usando o Visual Studio 2013 ou posterior direcionam ao .NET Framework 4.0 ou posterior.  
  
 As seções a seguir descrevem essas alterações de design de projeto do Office.  
  
## <a name="understanding-the-interface-based-design-of-the-visual-studio-2010-tools-for-office-runtime"></a>Noções básicas sobre o Design baseado em Interface do Visual Studio 2010 Tools for Office Runtime  
 Ao desenvolver um projeto do Office que se destina a [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior, a maioria dos tipos que você use o Visual Studio 2010 Tools para Office Runtime é interfaces. Essa é uma alteração importante de versões anteriores do [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)], onde esses tipos são classes. Por exemplo, quando você seleciona o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior, o <xref:Microsoft.Office.Tools.Excel.Worksheet> e <xref:Microsoft.Office.Tools.Word.Document> tipos são interfaces em vez de classes. Para obter mais informações, consulte [Visual Studio Tools for Office Runtime Overview](../vsto/visual-studio-tools-for-office-runtime-overview.md).  
  
 Para todos os tipos que você pode instanciar diretamente nas versões anteriores do [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)], agora você usar os métodos do objeto Globals.Factory para obter instâncias desses tipos. Por exemplo, para obter um objeto que implementa o <xref:Microsoft.Office.Tools.Excel.SmartTag> interface, use o método Globals.Factory.CreateSmartTag. Para mais informações, consulte os seguintes tópicos:  
  
-   [Atualizando projetos do Excel e Word que você migrar para o .NET Framework 4 ou o .NET Framework 4.5](../vsto/updating-excel-and-word-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md)  
  
-   [Atualizando personalizações da faixa de opções em projetos do Office migrados para o .NET Framework 4 ou o .NET Framework 4.5](../vsto/updating-ribbon-customizations-in-office-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md)  
  
-   [Atualizando as regiões de formulário em projetos do Office migrados para o .NET Framework 4 ou o .NET Framework 4.5](../vsto/updating-form-regions-in-outlook-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md)  
  
### <a name="new-base-classes-in-office-projects"></a>Novas Classes Base em projetos do Office  
 O novo design com base em interface do Visual Studio 2010 Tools for Office Runtime afeta as classes geradas em projetos do Office, como `ThisDocument`, `ThisWorkbook`, e `ThisAddIn`. Em projetos do Office que o .NET Framework 3.5 e versões anteriores do framework de destino, essas classes geradas derivam de classes de [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] como Microsoft.Office.Tools.Word.Document, Microsoft.Office.Tools.Excel.Worksheet, e Microsoft.Office.Tools.AddIn. Em projetos direcionados a [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior, essas [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] classes agora são interfaces. Portanto as classes geradas em projetos do Office não podem derivar sua implementação deles. Em vez disso, as classes geradas derivam novas classes base, como <xref:Microsoft.Office.Tools.Word.DocumentBase>, <xref:Microsoft.Office.Tools.Excel.WorksheetBase>, e <xref:Microsoft.Office.Tools.AddInBase>. Para obter mais informações, consulte [Programando suplementos do VSTO](../vsto/programming-vsto-add-ins.md) e [personalizações de programação de nível de documento](../vsto/programming-document-level-customizations.md).  
  
 As classes de base não são parte do [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] redistribuível. Em vez disso, eles são definidos em assemblies de utilitários incluídos com o Visual Studio. Esses assemblies são copiados para a pasta de saída quando você compilar projetos do Office e deve ser implantados com sua solução. Para obter mais informações sobre os assemblies de utilitários, consulte [Assemblies no Visual Studio Tools for Office Runtime](../vsto/assemblies-in-the-visual-studio-tools-for-office-runtime.md).  
  
## <a name="breaking-changes-in-office-projects-that-are-retargeted-to-the-net-framework-4"></a>Alterações mais recentes em projetos do Office que são redirecionadas para o .NET Framework 4  
 A tabela a seguir lista as alterações de quebra principal que você pode encontrar em projetos do Office que são redirecionados para o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior. Para obter mais detalhes, consulte [Migrando soluções do Office para o .NET Framework 4 ou posterior](../vsto/migrating-office-solutions-to-the-dotnet-framework-4-or-later.md).  
  
|Alteração recente|Consequência|  
|---------------------|-----------------|  
|O <xref:System.Security.SecurityTransparentAttribute> não são mais usados ou tem suporte em projetos do Office.|Você deve remover esse atributo do arquivo AssemblyInfo código em projetos do Office que a atualização do Visual Studio 2008. Para obter mais informações, consulte [alterações necessárias para executar projetos do Office migrados para o .NET Framework 4 ou o .NET Framework 4.5](../vsto/required-changes-to-run-office-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md).|  
|O ExcelLocale1033Attribute não é usado ou tem suporte em projetos do Excel.|Você deve remover esse atributo do arquivo AssemblyInfo código em projetos do Excel. Para obter mais informações, consulte [Atualizando projetos do Excel e Word que você migrar para o .NET Framework 4 ou o .NET Framework 4.5](../vsto/updating-excel-and-word-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md).|  
|O modelo de programação de **faixa de opções (Visual Designer)** itens de projeto foi alterado.|Você deve modificar o arquivo de code-behind para todos os itens da faixa de opções em seu projeto. Você também deve modificar qualquer código que instancia os controles de faixa de opções em tempo de execução, que trata os eventos da faixa de opções ou define a posição de um componente de faixa de opções programaticamente. Para obter mais informações, consulte [atualizando personalizações da faixa de opções no Office projetos que você migrar para o .NET Framework 4 ou o .NET Framework 4.5](../vsto/updating-ribbon-customizations-in-office-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md).|  
|O modelo de programação de regiões de formulário do Outlook foi alterado.|Você deve modificar o arquivo de code-behind para qualquer regiões de formulário em seu projeto e qualquer código que instancia determinadas classes de região de formulário em tempo de execução. Para obter mais informações, consulte [Atualizando as regiões de formulário do Outlook projetos que você migrar para o .NET Framework 4 ou o .NET Framework 4.5](../vsto/updating-form-regions-in-outlook-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md).|  
|O modelo de programação de marcas inteligentes em projetos do Excel e Word foi alterado. As marcas inteligentes foram preteridas no [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)] e [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)].|Se sua solução usar marcas inteligentes, ocorrerão erros quando compilar o projeto. Como as marcas inteligentes foram preteridas no [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)] e [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)], você deve remover as marcas, antes de testar e depurar a solução no [!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)] ou posterior.|  
|A sintaxe dos métodos GetVstoObject e HasVstoObject foi alterada|Você deve passar o objeto Globals.Factory para esses métodos ao acessá-los em objetos nativos dos assemblies de interoperabilidade primários (PIAs), ou você pode acessar esses métodos no objeto que é retornado pela propriedade Globals.Factory em seu projeto. Para obter mais informações, consulte [Atualizando projetos do Excel e Word que você migrar para o .NET Framework 4 ou o .NET Framework 4.5](../vsto/updating-excel-and-word-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md).|  
|Os eventos de controles de conteúdo do Word são associados com delegados de novo.|Você deve modificar qualquer código que trata os eventos de controles de conteúdo do Word para especificar os delegados de novo. Para obter mais informações, consulte [Atualizando projetos do Excel e Word que você migrar para o .NET Framework 4 ou o .NET Framework 4.5](../vsto/updating-excel-and-word-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md).|  
|As classes OLEObject e OLEControl foram renomeadas.|Você deve modificar qualquer código que usa instâncias dessas classes para usar <xref:Microsoft.Office.Tools.Excel.ControlSite> ou <xref:Microsoft.Office.Tools.Word.ControlSite> objetos em vez disso. Para obter mais informações, consulte [Atualizando projetos do Excel e Word que você migrar para o .NET Framework 4 ou o .NET Framework 4.5](../vsto/updating-excel-and-word-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md).|  
|Classes de item de host, como `ThisWorkbook`, `Sheet`  *n* , `ThisDocument`, e `ThisAddIn`, deixará de fornecer um método Dispose que pode ser substituído.|Você precisa mover qualquer código de substituição do método Dispose para o manipulador de eventos de desligamento da classe de item de host, por exemplo, `ThisAddIn_Shutdown`e remova a substituição do método Dispose da classe de item de host.|  
  
## <a name="see-also"></a>Consulte também  
 [Migrando soluções do Office para o .NET Framework 4 ou posterior](../vsto/migrating-office-solutions-to-the-dotnet-framework-4-or-later.md)   
 [O que há de novo no desenvolvimento do Office](http://msdn.microsoft.com/en-us/bf054af2-c896-4723-aa15-6381145b14bb)   
 [Visão geral do tempo de execução das Ferramentas do Visual Studio para o Office](../vsto/visual-studio-tools-for-office-runtime-overview.md)  
  
  