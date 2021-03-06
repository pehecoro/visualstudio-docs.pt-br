---
title: "Usando o Gerenciador de texto para monitorar as configurações globais | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - monitor global settings
- editors [Visual Studio SDK], legacy - text manager
ms.assetid: 023e7671-cf65-419c-9bc1-3c4ee92aa436
caps.latest.revision: "14"
author: gregvanl
ms.author: gregvanl
manager: ghogen
ms.workload: vssdk
ms.openlocfilehash: 00716142e7f91d01fbc81c5d25b378065cb44f92
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="using-the-text-manager-to-monitor-global-settings"></a>Usando o Gerenciador de texto para monitorar as configurações globais
Se você implementar um editor de núcleo, você deve monitorar as alterações feitas em configurações globais, porque essas alterações podem afetar sua instância do editor. Você pode controlar as alterações de escuta para eventos gerados pelo Gerenciador de texto. Por exemplo, quando você especificar uma preferência global para a aparência ou o comportamento de um componente no editor de núcleo, como seu objeto de dados de documento, o Gerenciador de texto armazena essas informações e comunica-se a todos os clientes afetados.  
  
## <a name="text-manager-functions"></a>Funções do Gerenciador de texto  
 O Gerenciador de texto gera eventos para um número de configurações, incluindo o seguinte:  
  
-   Se um buffer está sob controle do código fonte  
  
-   Como registrar para notificações de alteração de arquivo  
  
-   Como manter o controle de quais modos de exibição estão associados a determinado buffers  
  
-   Preferências de coloração de texto  
  
-   Guia versus preferências de espaço  
  
 As preferências que são exclusivas para um determinado idioma não são gerenciadas pelo Gerenciador de texto. Essas configurações devem ser gerenciadas por cada serviço de linguagem.  
  
 Notificação de eventos para o Gerenciador de texto é fornecida pelo <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextManagerEvents> interface. Implementar essa interface no cliente do objeto para manipular eventos gerou o Gerenciador de texto. Você pode registrar esses eventos usando o <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer> interface no Gerenciador de texto.  
  
## <a name="see-also"></a>Consulte também  
 [Dentro do Editor de núcleo](../extensibility/inside-the-core-editor.md)   
 [Recursos do Editor](http://msdn.microsoft.com/en-us/bdac940d-1f14-4019-a01f-fd0bb3dc7198)