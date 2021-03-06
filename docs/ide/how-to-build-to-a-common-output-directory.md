---
title: "Como compilar um diretório de saída comum | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-general
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- output directory
- builds [Visual Studio], common directory
- common directory
ms.assetid: 1fcc2c48-07cb-4c4f-9556-36945e7dfc4e
caps.latest.revision: "7"
author: gewarren
ms.author: gewarren
manager: ghogen
ms.workload: multiple
ms.openlocfilehash: f45831618e7d685da1f50ae634770ef735a6ff78
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-build-to-a-common-output-directory"></a>Como compilar um diretório de saída comum
Por padrão, [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] compila cada projeto em uma solução em sua própria pasta dentro da solução. É possível alterar os caminhos de saída do build dos seus projetos para forçar todas as saídas a serem colocadas na mesma pasta.  
  
### <a name="to-place-all-solution-outputs-in-a-common-directory"></a>Para colocar todas as saídas de solução em um diretório comum  
  
1.  Clique em um projeto na solução.  
  
2.  No menu **Projeto**, clique em **Propriedades**.  
  
3.  Dependendo do tipo de projeto, clique na guia **Compilar** ou na guia **Build** e defina o **Caminho de saída** para uma pasta usar para todos os projetos na solução.  
  
4.  Repita as etapas 1 a 3 para todos os projetos na solução.  
  
## <a name="see-also"></a>Consulte também  
 [Compilando e criando](../ide/compiling-and-building-in-visual-studio.md)   
 [Como alterar o diretório de saída do build](../ide/how-to-change-the-build-output-directory.md)