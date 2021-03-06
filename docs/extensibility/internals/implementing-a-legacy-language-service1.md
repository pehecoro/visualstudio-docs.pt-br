---
title: Implementando um Service1 de idioma herdado | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: language services, managed
ms.assetid: df638f24-166d-4b80-be82-c9c39ca7a556
caps.latest.revision: "18"
author: gregvanl
ms.author: gregvanl
manager: ghogen
ms.workload: vssdk
ms.openlocfilehash: 304d99c1ddd5fdfddba0c4df88fc4eeeb9dcb7ac
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="implementing-a-legacy-language-service"></a>Implementar um serviço de linguagem herdado
Você pode usar classes do framework de pacote gerenciado (MPF) para implementar um serviço de linguagem herdada que dá suporte a uma ampla variedade de recursos, como o realce de sintaxe, a correspondência de chaves e a conclusão do IntelliSense.  
  
 Os serviços de idioma herdados são implementados como parte de um VSPackage, mas a maneira mais recente para implementar recursos de serviço de linguagem é usar extensões MEF. Para obter mais informações sobre a nova maneira de implementar um serviço de idioma, consulte [Editor e extensões de serviço de linguagem](../../extensibility/editor-and-language-service-extensions.md).  
  
> [!NOTE]
>  É recomendável que você comece a usar o novo editor de API assim que possível. Isso melhorar o desempenho do seu serviço de linguagem e permitem que você aproveite os novos recursos do editor.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Visão geral do serviço de linguagem herdado](../../extensibility/internals/legacy-language-service-overview.md)  
 Uma visão geral dos recursos de serviço de linguagem com suporte no MPF.  
  
 [Implementar um serviço de linguagem herdado](../../extensibility/internals/implementing-a-legacy-language-service2.md)  
 Descreve o que é necessário para implementar um serviço de idioma usando MPF.  
  
 [Registrar um serviço de linguagem herdado](../../extensibility/internals/registering-a-legacy-language-service1.md)  
 Descreve as etapas necessárias para registrar um serviço de linguagem baseada em MPF com [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)].  
  
 [Analisador e scanner do serviço de linguagem herdado](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)  
 Descreve os analisadores de dois são necessários para implementar todos os recursos de um serviço de linguagem usando MPF.  
  
 [Passo a passo: Criar um serviço de linguagem herdado](../../extensibility/internals/walkthrough-creating-a-legacy-language-service.md)  
 Fornece as etapas básicas necessárias para implementar um serviço de linguagem MPF em um VSPackage.  
  
 [Passo a passo: Obter uma lista de trechos de código instalados (implementação herdada)](../../extensibility/internals/walkthrough-getting-a-list-of-installed-code-snippets-legacy-implementation.md)  
 Demonstra as técnicas de recuperar uma lista de trechos de código instalado.  
  
 [Recursos de serviço de linguagem herdada](../../extensibility/internals/legacy-language-service-features1.md)  
 Fornece links para tópicos que o que deve ser feito para implementar todos os recursos de um serviço de linguagem usando MPF de detalhes.