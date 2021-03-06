---
title: "Uso de vários processadores para criar projetos | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: msbuild
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- multiple processors
- MSBuild, multiple processor systems
ms.assetid: 49fa36c9-8e14-44f5-8a2b-34146cf6807b
caps.latest.revision: 
author: Mikejo5000
ms.author: mikejo
manager: ghogen
ms.workload:
- multiple
ms.openlocfilehash: f8bf385b6ee34c532e70557c0f04754ba0c56bb9
ms.sourcegitcommit: 205d15f4558315e585c67f33d5335d5b41d0fcea
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="using-multiple-processors-to-build-projects"></a>Usando vários processadores para compilar projetos
MSBuild pode tirar proveito dos sistemas com vários processadores ou vários núcleos processadores. Um processo de compilação separado é criado para cada processador disponível. Por exemplo, se o sistema possui quatro processadores, então quatro processos de compilação são criados. [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] pode processar essas compilações simultaneamente e, portanto, em geral o tempo de compilação é reduzido. No entanto, a construção em paralelo apresenta algumas alterações em como os processos de compilação ocorrem. Este tópico aborda essas alterações.  
  
## <a name="project-to-project-references"></a>Referências Projeto para Projeto  
 Quando o [!INCLUDE[vstecmsbuildengine](../msbuild/includes/vstecmsbuildengine_md.md)] encontra uma referência de projeto para projeto (P2P) enquanto ela está usando paralelo compilações para compilar um projeto, ele cria a referência de apenas uma vez. Se dois projetos tiverem a mesma referência P2P, a referência não é reconstruída para cada projeto. Em vez disso, o mecanismo de compilação retorna a mesma referência P2P para ambos os projetos que dependem dele. As solicitações futuras na sessão para o mesmo destino recebem a mesma referência P2P.  
  
## <a name="cycle-detection"></a>Detecção do Ciclo  
 Ciclo de detecção funciona da mesma maneira que no [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 2.0, exceto que agora [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] pode relatar a detecção de ciclo em um momento diferente ou na compilação.  
  
## <a name="errors-and-exceptions-during-parallel-builds"></a>Erros e Exceções Durante Compilações Paralelas  
 Em compilações paralelas, erros e exceções podem ocorrer em momentos diferentes que fazem em uma compilação não paralelos e quando um projeto não será compilado, continuam as compilações do projeto. [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] não irá parar qualquer compilação do projeto que está criando em paralelo com aqueles que falharam. Outros projetos continuam a ser criados até que tenham êxito ou falha. No entanto, se <xref:Microsoft.Build.Framework.IBuildEngine.ContinueOnError%2A> foi habilitado, então nenhum build será interrompido, mesmo que ocorra um erro.  
  
## <a name="visual-c-project-vcproj-and-solution-sln-files"></a>Arquivos de Projeto do Visual C++ (.vcproj) e de Solução (.sln)  
 Ambos os arquivos de projetos [!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)] (.vcproj) e de solução (.sln) que podem ser passados para a [Tarefa MSBuild](../msbuild/msbuild-task.md). Para projetos [!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)], VCWrapperProject é chamado e então o projeto [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] interno é criado. Para [!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)] soluções, um SolutionWrapperProject é criado e, em seguida, interno [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] projeto é criado. Em ambos os casos, o projeto resultante será tratado o mesmo que qualquer outro projeto do [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)].  
  
## <a name="multi-process-execution"></a>Execução Multiprocesso  
 Quase todas as atividades relacionadas à compilação exigem o diretório atual para permanecer constante ao longo do processo de compilação para evitar erros de caminho. Portanto, projetos não podem ser executado em threads diferentes em [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] porque eles causaria vários diretórios a serem criados.  
  
 Para evitar esse problema, mas ainda permitir compilações para vários processadores, [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] usa "isolamento de processo." Usando o isolamento do processo, [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] pode criar no máximo `n` processos, onde `n` é igual ao número de processadores disponíveis no sistema. Por exemplo, se [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] compilações uma solução em um sistema com dois processadores, e somente dois processos de compilação são criados. Novamente, esses processos são usados para criar todos os projetos na solução.  
  
## <a name="see-also"></a>Consulte também  
 [Criação de vários projetos em paralelo](../msbuild/building-multiple-projects-in-parallel-with-msbuild.md)   
 [Tarefas](../msbuild/msbuild-tasks.md)