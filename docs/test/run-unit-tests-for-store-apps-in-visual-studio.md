---
title: Executar testes de unidade no Visual Studio | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-devops-test
ms.tgt_pltfrm: 
ms.topic: article
ms.author: gewarren
manager: ghogen
ms.workload:
- uwp
author: gewarren
ms.openlocfilehash: c06ad430664f1e6cd5010e4af5d8d28efa1f8d25
ms.sourcegitcommit: ba29e4d37db92ec784d4acf9c6e120cf0ea677e9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2018
---
# <a name="run-unit-tests-in-visual-studio"></a>Executar testes de unidade no Visual Studio

Este tópico descreve como executar testes de unidade usando o Gerenciador de Testes no Microsoft Visual Studio.

##  <a name="BKMK_Unit_test_frameworks_and_test_projects"></a> Estruturas de teste de unidade e projetos de teste

O Visual Studio inclui as estruturas de teste de unidade da Microsoft para código gerenciado e código C++ nativo. O Gerenciador de Testes pode executar testes de vários projetos de teste em uma solução e de classes de teste que fazem parte dos projetos de código de produção. Os projetos de teste podem ser qualquer combinação de Visual C++ ou estruturas de teste de unidade Visual C# e Visual Basic. Quando o código em teste é escrito para o .NET Framework, o projeto de teste pode ser escrito em qualquer linguagem do .NET Framework, independentemente do idioma de código de destino. Projetos de código C/C++ nativos devem ser testados usando uma estrutura de teste de unidade C++.

##  <a name="BKMK_Running_tests_in_Test_Explorer"></a> Executando testes no Gerenciador de Testes  
 Quando você compila o projeto de teste, os testes são exibidos no Gerenciador de Testes. Se o Gerenciador de Testes não estiver visível, escolha **Teste** no menu do Visual Studio, escolha **Windows** e, em seguida, escolha **Gerenciador de Testes**.  
  
 ![Gerenciador de testes de unidade](../test/media/ute_failedpassednotrunsummary.png "UTE_FailedPassedNotRunSummary")  
  
 Conforme você executa, grava e executa novamente os testes, o Gerenciador de Testes exibe os resultados nos grupos padrão de **Testes com Falha**, **Testes Aprovados**, **Testes Ignorados** e **Testes Não Executados**. Você pode alterar a forma como o Gerenciador de Testes agrupa seus testes.  
  
 Você pode executar a maior parte do trabalho de encontrar, organizar e executar testes usando a barra de ferramentas do Gerenciador de Testes.  
  
 ![Executar testes na barra de ferramentas do Gerenciador de Testes](../test/media/ute_toolbar.png "UTE_ToolBar")  
  
###  <a name="BKMK_Running_tests"></a> Executando testes  
 Você pode executar todos os testes na solução, todos os testes em um grupo ou um conjunto de testes que você selecionar. Realize um dos seguintes procedimentos:  
  
-   Para executar todos os testes em uma solução, escolha **Executar Todos**.  
  
-   Para executar todos os testes em um grupo padrão, escolha **Executar...** e, em seguida, escolha o grupo no menu.  
  
-   Selecione os testes individuais que deseja executar, abra o menu de atalho para um teste selecionado e escolha **Executar Testes Selecionados**.  
  
 A barra de aprovação/reprovação na parte superior da janela do Gerenciador de Testes é animada conforme os testes são executados. Na conclusão da execução de teste, a barra de aprovação/reprovação ficará verde se todos os testes forem aprovados ou vermelha se algum deles for reprovado.  
  
##  <a name="BKMK_Viewing_test_results"></a> Exibindo resultados de teste  
 Conforme você executa, grava e executa novamente os testes, o Gerenciador de Testes exibe os resultados em grupos **Testes com falha**, **Testes Aprovados**, **Testes Ignorados** e **Testes Não Executados**. O painel de detalhes na parte inferior do Gerenciador de Testes exibe um resumo da execução de teste.  
  
###  <a name="BKMK_Viewing_test_details"></a> Exibindo detalhes do teste  
 Para exibir os detalhes de um teste individual, selecione o teste.  
  
 O painel de detalhes de teste exibe as seguintes informações:  
  
-   O nome do arquivo de origem e o número de linha do método de teste.  
  
-   O status do teste.  
  
-   O tempo decorrido que o método de teste levou para ser executado.  
  
 Se o teste falhar, o painel de detalhes também exibe:  
  
-   A mensagem retornada pela estrutura de teste de unidade para o teste.  
  
-   O rastreamento de pilha no momento em que o teste falhou.  
  
###  <a name="BKMK_Viewing_the_source_code_of_a_test_method"></a> Exibindo o código-fonte de um método de teste  
 Para exibir o código-fonte para um método de teste no editor do Visual Studio, selecione o teste e, em seguida, escolha **Abrir teste** no menu de atalho (teclado: F12).  
  
##  <a name="BKMK_Organizing_the_test_list"></a> Organizando a lista de testes  
  
###  <a name="BKMK_Grouping_tests"></a> Agrupando testes  
 Por padrão, o Gerenciador de Testes exibe os testes como nós filhos de **Testes Reprovados**, **Testes Aprovados**, **Testes Ignorados** e **Testes Não Executados**.  
  
|||  
|-|-|  
|![Botão do grupo do Gerenciador de Testes](../test/media/ute_groupby_btn.png "UTE_GroupBy_btn")|Para agrupar os testes pelo tempo necessário para executá-los, abra a lista **Agrupar por** e escolha **Duração**. Escolha **Resultado do Teste** para mudar para o agrupamento original.|  
  
###  <a name="BKMK_Searching_and_filtering_the_test_list"></a> Pesquisando e filtrando a lista de testes  
 Quando você tiver um grande número de testes, poderá digitar na caixa de pesquisa do Gerenciador de Testes para filtrar a lista por cadeia de caracteres especificada. Você pode restringir o filtro a tipos específicos de cadeias de caracteres escolhendo na lista de filtros antes de inserir a cadeia de caracteres de pesquisa.  
  
 ![Categorias de filtro de pesquisa](../test/media/ute_searchfilter.png "UTE_SearchFilter")  
  
##  <a name="BKMK_Debugging_unit_tests"></a> Depurando testes de unidade  
 Você pode usar o Gerenciador de Testes para iniciar uma sessão de depuração para os testes. Passar pelo código com o depurador do Visual Studio permite-lhe navegar facilmente entre os testes de unidade e o projeto sendo testado. Para iniciar a depuração:  
  
1.  No editor do Visual Studio, defina um ponto de interrupção em um ou mais métodos de teste que deseje depurar.  
  
    > [!NOTE]
    > Como os métodos de teste podem ser executados em qualquer ordem, defina pontos de interrupção em todos os métodos de teste que deseje depurar.  
  
2.  No Gerenciador de Testes, selecione os métodos de teste e escolha **Depurar Testes Selecionados** no menu de atalho.  
  
 Para obter mais informações sobre o depurador, consulte [Depuração no Visual Studio](../debugger/debugging-in-visual-studio.md).
