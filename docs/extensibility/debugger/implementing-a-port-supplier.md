---
title: Implementando um fornecedor de porta | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- debugging [Debugging SDK], implementing port suppliers
- port suppliers, implementing
ms.assetid: 6b8579df-58df-4c7f-8112-6015993e8765
caps.latest.revision: "11"
author: gregvanl
ms.author: gregvanl
manager: ghogen
ms.workload: vssdk
ms.openlocfilehash: aa70e2a6019a97c248e6d4b411dacc222be59a1f
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="implementing-a-port-supplier"></a>Implementando um fornecedor de porta
Um fornecedor de porta fornece portas de solicitação para o Gerenciador de sessão de depuração (SDM). Um fornecedor de porta deve ser implementado durante a depuração em uma máquina não DCOM ou quando um novo dispositivo precisa de suporte. Por exemplo, para fornecer a depuração para um telefone celular, você pode implementar um fornecedor de porta que fornece as portas que se conectam para o telefone celular (talvez por meio de IV ou uma conexão de célula) e enumera os processos e programas em execução no telefone.  
  
 Para depuração de programas em computadores baseados no Windows (incluindo a depuração remota), o Visual Studio fornece fornecedores de porta para nativo e processos de tempo de execução de linguagem comum (CLR), portanto, não há necessidade de implementar seu próprio fornecedor de porta nos casos.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Implementar e registrar um fornecedor de porta](../../extensibility/debugger/implementing-and-registering-a-port-supplier.md)  
 Discute como o SDM interage com o fornecedor de porta e as portas.  
  
 [Interfaces de fornecedor porta necessárias](../../extensibility/debugger/required-port-supplier-interfaces.md)  
 Documenta as interfaces que devem ser implementadas para obter um fornecedor de porta.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Conceitos do depurador](../../extensibility/debugger/debugger-concepts.md)  
 Descreve os principais conceitos de arquitetura de depuração.  
  
## <a name="see-also"></a>Consulte também  
 [Extensibilidade do depurador do Visual Studio](../../extensibility/debugger/visual-studio-debugger-extensibility.md)