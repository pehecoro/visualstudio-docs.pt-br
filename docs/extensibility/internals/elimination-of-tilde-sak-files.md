---
title: "Eliminação de ~ SAK arquivos | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- temporary files
- ~sak files
- source control plug-ins, ~SAK files
ms.assetid: 5277b5fa-073b-4bd1-8ba1-9dc913aa3c50
caps.latest.revision: "15"
author: gregvanl
ms.author: gregvanl
manager: ghogen
ms.workload: vssdk
ms.openlocfilehash: 8d72a42c89cc775b9312d301a052ee102d977728
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="elimination-of-sak-files"></a>Eliminação de ~ SAK arquivos
No código-fonte controle plug-in API 1.2, o ~ arquivos SAK foram substituídos por sinalizadores de recursos e novas funções que detecta se um plug-in de controle de origem dá suporte a arquivo MSSCCPRJ e check-outs compartilhados.  
  
## <a name="sak-files"></a>~ Arquivos de SAK  
 Visual Studio .NET 2003 criou arquivos temporários prefixados com ~ SAK. Esses arquivos são usados para determinar se um plug-in de controle de origem dá suporte a:  
  
-   MSSCCPRJ. Arquivos SCC.  
  
-   Vários checkouts (compartilhados).  
  
 Para plug-ins que dão suporte a funções avançadas fornecidas a fonte de controle de plug-in API 1.2, o IDE pode detectar esses recursos sem criar os arquivos temporários com o uso de novos recursos, sinalizadores e funções, detalhadas nas seções a seguir.  
  
## <a name="new-capability-flags"></a>Novo sinalizadores de recursos  
 `SCC_CAP_SCCFILE`  
  
 `SCC_CAP_MULTICHECKOUT`  
  
## <a name="new-functions"></a>Novas funções  
 [SccWillCreateSccFile](../../extensibility/sccwillcreatesccfile-function.md)  
  
 [SccIsMultiCheckoutEnabled](../../extensibility/sccismulticheckoutenabled-function.md)  
  
 Se um plug-in de controle de origem dá suporte a vários check-outs (compartilhados), ele declara o `SCC_CAP_MULTICHECKOUT` capacidade e implementa o `SccIsMultiCheckOutEnabled` função. Essa função é chamada sempre que ocorre uma operação de check-out em qualquer um dos projetos de controle do código-fonte.  
  
 Se um plug-in de controle de origem tiver suporte para a criação e uso de um MSSCCPRJ. Arquivos SCC, ele declara o `SCC_CAP_SCCFILE` capacidade e implementa o [SccWillCreateSccFile](../../extensibility/sccwillcreatesccfile-function.md). Essa função é chamada com uma lista de arquivos. A função retorna `TRUE/FALSE` para cada arquivo indicar se o Visual Studio deve usar um MSSCCPRJ. Arquivos SCC para ele. Se o plug-in de controle de origem decidir não oferecer suporte a esses novos recursos e funções, poderá usar a seguinte chave do registro para desabilitar a criação desses arquivos:  
  
 [HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0\SourceControl] "DoNotCreateTemporaryFilesInSourceControl" = DWORD: 00000001  
  
> [!NOTE]
>  Se essa chave do registro é definida como DWORD: 00000000, é equivalente à chave sendo inexistente e Visual Studio ainda tenta criar arquivos temporários. No entanto, se a chave do registro é definida como DWORD: 00000001, Visual Studio não tentará criar arquivos temporários. Em vez disso, ele pressupõe que o plug-in de controle de origem não oferece suporte a MSSCCPRJ. Arquivos SCC e não dá suporte a check-outs compartilhados.  
  
## <a name="see-also"></a>Consulte também  
 [Novidades na Versão 1.2 da API do plug-in de controle de código-fonte](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)