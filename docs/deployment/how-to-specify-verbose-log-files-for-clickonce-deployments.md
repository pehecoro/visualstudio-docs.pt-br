---
title: "Como: especificar os arquivos de Log detalhados para implantações do ClickOnce | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-deployment
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- logs, ClickOnce deployment
- ClickOnce deployment, logging
ms.assetid: 0807a28d-2e40-4a51-ab10-308d808ded6b
caps.latest.revision: "9"
author: stevehoag
ms.author: shoag
manager: wpickett
ms.workload: multiple
ms.openlocfilehash: 6cac7764a941e88dd3901a3280e78717955e86b4
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-specify-verbose-log-files-for-clickonce-deployments"></a>Como especificar arquivos de log detalhados para implantações do ClickOnce
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]mantém os arquivos de log de atividades para todas as implantações. Esses logs de documento detalhes relativos ao instalar, inicializar, atualizando e desinstalando um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] implantação. Para aumentar o detalhe que [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] gravações a esses arquivos de log, use o Editor do registro (**regedit.exe**) para especificar o nível de detalhamento.  
  
> [!CAUTION]
>  Se você usar o Editor do Registro incorretamente, você poderá causar sérios problemas que talvez exijam a reinstalação do sistema operacional. Use o Editor do registro por seu próprio risco.  
  
 O procedimento a seguir descreve como especificar o nível de detalhamento para [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] arquivos de log para o usuário atual. Para reduzir o nível de detalhamento, remova esse valor do registro.  
  
### <a name="to-specify-verbose-log-files"></a>Para especificar os arquivos de log detalhado  
  
1.  Abra **Regedit.exe**.  
  
2.  Navegue até o nó `HKEY_CURRENT_USER\Software\Classes\Software\Microsoft\Windows\CurrentVersion\Deployment`.  
  
3.  Se necessário, crie um novo valor de cadeia de caracteres chamado `LogVerbosityLevel`.  
  
4.  Definir o `LogVerbosityLevel` valor `1`.  
  
## <a name="see-also"></a>Consulte também  
 [Solução de problemas de implantações ClickOnce](../deployment/troubleshooting-clickonce-deployments.md)