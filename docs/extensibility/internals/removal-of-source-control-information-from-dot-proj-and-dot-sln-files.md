---
title: "Remoção de informações de controle de origem. PROJ e. Arquivos sln | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: source control plug-ins, .sln and .proj files
ms.assetid: 7b06883f-35de-41e2-9a9e-d3edba236f17
caps.latest.revision: "14"
author: gregvanl
ms.author: gregvanl
manager: ghogen
ms.workload: vssdk
ms.openlocfilehash: 4131e3d5139911c6a1bb9b44d8d8acaefa6cb632
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="removal-of-source-control-information-from-proj-and-sln-files"></a>Remoção de informações de controle de origem. PROJ e. Arquivos sln
Na versão 1.2 da API de plug-in de controle de origem SCC informações são armazenadas em um MSSCCPRJ. Arquivos SCC. A vantagem do MSSCCPRJ. Arquivos SCC é que as informações de SCC é não na origem - controlada, como nos arquivos. proj. e. sln.  
  
## <a name="version-12-changes"></a>Alterações da versão 1.2  
 Na origem plug-ins de controle que usam a API de plug-in de controle de origem versão 1.1, informações sobre o controle de origem são armazenadas no projeto (. proj) e arquivos de solução (. sln). O local do banco de dados das informações de controle de origem é especificado pelo AuxPath e o local específico no banco de dados é especificado pelo Project. Esse comportamento pode causar problemas após a ramificação, bifurcação ou operações de cópia porque o NomeDoProjeto normalmente seriam inválido após qualquer uma dessas operações.  
  
 Na API do plug-in de controle de origem versão 1.1, o IDE usada ~ arquivos SAK para detectar se um plug-in com suporte a MSSCCPRJ. Método SCC armazenar informações de controle de origem. A API de plug-in de controle de origem versão 1.2 fornece uma nova funcionalidade para detectar o suporte para MSSCCPRJ. Arquivos SCC sem usar um ~ arquivo SAK. Para obter mais informações, consulte [eliminação de ~ SAK arquivos](../../extensibility/internals/elimination-of-tilde-sak-files.md).  
  
## <a name="see-also"></a>Consulte também  
 [Novidades na Versão 1.2 da API do plug-in de controle de código-fonte](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)