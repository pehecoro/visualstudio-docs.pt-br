---
title: "Como: fornecem automação para Windows | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- automation [Visual Studio SDK], tool windows
- tool windows, automation
ms.assetid: 512ab2a4-7987-4912-8f40-8804bf66f829
caps.latest.revision: "10"
author: gregvanl
ms.author: gregvanl
manager: ghogen
ms.workload: vssdk
ms.openlocfilehash: 17cf60573b6feb9fd317116eec4639dbf88f6089
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-provide-automation-for-windows"></a>Como: fornecem automação para Windows
Você pode fornecer automação para o documento e janelas de ferramenta. Fornecimento de automação é recomendável sempre que você deseja disponibilizar os objetos de automação em uma janela, e o ambiente ainda não fornece um objeto de automação prontas, como ocorre com uma lista de tarefas.  
  
## <a name="automation-for-tool-windows"></a>Automação de janelas de ferramentas  
 O ambiente fornece automação em uma janela de ferramenta, retornando um padrão <xref:EnvDTE.Window> objeto conforme explicado no procedimento a seguir:  
  
#### <a name="to-provide-automation-for-tool-windows"></a>Para fornecer a automação para janelas de ferramentas  
  
1.  Chamar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A> método através do ambiente com <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID> como `VSFPROPID` para obter o `Window` objeto.  
  
2.  Quando um chamador solicita um objeto de automação de VSPackage específico para sua janela de ferramenta por meio de <xref:EnvDTE.Window.Object%2A>, as chamadas de ambiente `QueryInterface` para `IExtensibleObject`, <xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibleObject>, ou o `IDispatch` interfaces. Ambos `IExtensibleObject` e `IVsExtensibleObject` fornecem um <xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibleObject.GetAutomationObject%2A> método.  
  
3.  Quando o ambiente, em seguida, chama o `GetAutomationObject` método passando `NULL`, responder, passando fazer seu objeto VSPackage específico.  
  
4.  Se chamar `QueryInterface` para `IExtensibleObject` e `IVsExtensibleObject` falhar, então o ambiente chama `QueryInterface` para `IDispatch`.  
  
## <a name="automation-for-document-windows"></a>Automação de janelas de documento  
 Um padrão <xref:EnvDTE.Document> objeto também está disponível no ambiente, embora um editor pode ter sua própria implementação do `T:EnvDTE.Document` objeto implementando `IExtensibleObject` interface e responder a `GetAutomationObject`.  
  
 Além disso, um editor pode fornecer um objeto de automação VSPackage específico, recuperado por meio de <xref:EnvDTE.Document.Object%2A> método Implementando o `IVsExtensibleObject` ou `IExtensibleObject` interfaces. O [VSSDK exemplos](http://aka.ms/vs2015sdksamples) contribui com um objeto de automação específica do documento RTF.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibleObject>