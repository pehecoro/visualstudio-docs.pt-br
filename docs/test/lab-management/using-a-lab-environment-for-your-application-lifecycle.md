---
title: "Usar um ambiente de laboratório para suas operações de desenvolvimento | Microsoft Docs"
ms.custom: 
ms.date: 05/02/2017
ms.reviewer: 
ms.suite: 
ms.technology: vs-devops-test
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: lab environment, test lab
ms.author: gewarren
manager: ghogen
ms.workload: multiple
author: gewarren
ms.openlocfilehash: 227068197de1d953ae6f3729888a1b6d2dfc164c
ms.sourcegitcommit: 7ae502c5767a34dc35e760ff02032f4902c7c02b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2018
---
# <a name="use-a-lab-environment-for-your-devops"></a>Usar um ambiente de laboratório para suas operações de desenvolvimento

Um ambiente de laboratório é uma coleção de máquinas virtuais e físicas que você pode usar para desenvolver e testar aplicativos. Um ambiente de laboratório pode conter várias funções necessárias para testar aplicativos com camadas múltiplas, como estações de trabalho, servidores de Web e servidores de banco de dados. Além disso, você pode usar um fluxo de trabalho compilação-implantação-teste com seu ambiente de laboratório para automatizar o processo de compilação, implantação e execução de testes automatizados em seu aplicativo.

* **Usar um plano de teste para executar testes automáticos** − Você pode executar uma coleção de testes automatizados, chamados de *plano de teste* e exibir o processo usando.  
  
* **Usar um fluxo de trabalho compilar-implantar-testar** − Você pode usar um fluxo de trabalho compilar-implantar-testar para testar aplicativos com camadas múltiplas automaticamente. Um exemplo típico é um fluxo de trabalho que começa com uma compilação, implanta os arquivos de compilação nos computadores apropriados em um ambiente de laboratório, em seguida, executa testes automáticos. Além disso, você pode programar seu fluxo de trabalho para ser executado em intervalos específicos.  
  
* **Colecionar dados de diagnóstico de todos os computadores, até durante o teste manual** − Você pode colecionar dados de diagnóstico de vários computadores simultaneamente. Por exemplo, durante uma única execução de teste, você pode coletar IntelliTrace, impacto de teste e outras formas de dados de um servidor Web, um servidor de banco de dados e um cliente.  
  
Aqui estão exemplos de tipos comuns de ambientes de laboratório:  
  
| Topologia | Descrição |  
|---|---|  
|![Topologia apenas do servidor](../media/topology_backend.png)| Este ambiente de laboratório tem uma *topologia de servidor*, frequentemente usada para executar testes manuais em aplicativos de servidor e permite que os testadores usem seus próprios computadores cliente para verificar bugs no ambiente. Em uma topologia back-end, seu ambiente de laboratório contém apenas servidores. Ao usar esse tipo de topologia, geralmente você se conecta aos servidores no ambiente de laboratório usando um computador cliente que não é parte dele.|  
|![Ambiente de laboratório de nuvem](../media/topology_cloud.png)| Esse ambiente de laboratório fornece funcionalidades e recursos semelhantes que a _topologia de rede_, mas remove a necessidade de máquinas virtuais ou computadores físicos em execução em um ambiente local, o que pode reduzir o tempo de configuração, simplificar a manutenção e minimizar o custo. Configurar vários sites e máquinas virtuais, junto o serviço de rede personalizado, é rápido e fácil em um ambiente de nuvem como o Microsoft Azure. [Mais detalhes](#usebandrm).|  
|![Ambiente de laboratório de cliente-servidor](../media/topology_clientserver.png)| Este ambiente de laboratório te uma *topologia cliente/servidor*, frequentemente usada para testar um aplicativo com componentes de servidor e de cliente. Em uma topologia cliente/servidor, todos os computadores cliente e servidor usados para testar seu aplicativo estão em seu ambiente de laboratório. Quando você usa essa topologia, pode coletar dados de teste de cada computador que impacta seus testes.|  
  
Consulte [Vídeo: Gerenciando ambientes de laboratório para teste](http://go.microsoft.com/fwlink/?LinkID=252614).  
  
Técnicas comuns para configurar um ambiente de laboratório são: 
  
* **[Usar a nuvem com Team Services ou Team Foundation Server Build &amp; Release](#usebandrm)**

* **[Usar os recursos do Lab Management do Visual Studio do Microsoft Test Manager](#usemtmlm)**

<a name="usebandrm"></a>
## <a name="use-the-cloud-with-team-services-or-team-foundation-server-build-amp-release"></a>Usar a nuvem com Team Services ou Team Foundation Server Build &amp; Release

Você pode executar testes automatizados e a automação de compilar-implantar-testar usando os recursos de [Build &amp; Release](https://www.visualstudio.com/team-services/continuous-integration/) no TFS (Team Foundation Server) e Visual Studio Team Services. Alguns dos benefícios são:

* Não é necessário ter um Controlador de Build ou um Controlador de Teste.
* O Agente de Teste é instalado por meio de uma tarefa como parte do build ou da versão.
* É fácil personalizar as etapas de implantação. Você não está mais restrito a usar um único script. Você também pode aproveitar as várias tarefas que estão disponíveis no produto, bem como no Visual Studio Marketplace.
* Você não precisa manter conjuntos de testes. Você pode executar os testes diretamente dos binários.
* Você obtém uma experiência de relatório embutido avançada para os testes executados dentro de cada build ou versão.
* Você pode controlar quais ativos (versão, build, itens de trabalho, confirmações) atualmente estão implantadas e testadas em cada ambiente.
* Você pode personalizar e estender a automação para implantar facilmente em vários ambientes de teste e até mesmo na produção.
* Você pode agendar a automação para ocorrer sempre que houver um check-in ou confirmação ou em um momento específico todos os dias.

[Mais informações](use-build-or-rm-instead-of-lab-management.md).

<a name="usemtmlm"></a>
## <a name="use-the-visual-studio-lab-management-features-of-microsoft-test-manager"></a>Usar os recursos do Lab Management do Visual Studio do Microsoft Test Manager

Você pode criar e gerenciar ambientes de laboratório com os recursos do Lab Management do Visual Studio do Microsoft Test Manager ao usar o Visual Studio Enterprise ou o Visual Studio Test Professional.

O Lab Management instala automaticamente agentes de teste em cada computador do seu ambiente.  
  
Se utilizar o Lab Management junto ao System Center Virtual Machine Manager (SCVMM), você também pode obter esses benefícios ao usar ambientes de laboratório:  
  
* **Reproduzir rapidamente as configurações do computador** − Você pode armazenar as coleções das máquinas virtuais que são configuradas para recriar ambientes típicos de produção. Assim, você pode aplicar cada execução de teste em uma nova cópia de um ambiente armazenado.  
  
* **Reproduzir as condições exatas de um bug** – Quando uma execução de teste falha, você pode armazenar uma cópia do estado do seu ambiente de laboratório e acessá-la em seus resultados de compilação ou em um item de trabalho.  
  
* **Executar várias cópias de um ambiente de laboratório ao mesmo tempo** – Você pode executar várias cópias de seu ambiente de laboratório ao mesmo tempo sem conflitos de nome.  
  
### <a name="standard-environments-and-scvmm-environments"></a>Ambientes padrão e SCVMM

Há dois tipos de ambientes de laboratório que você pode criar com o Lab Management do Visual Studio: **ambientes padrão** e **ambientes do SCVMM**.
Entretanto, as capacidades de cada tipo de ambiente são diferentes.  
  
> **OBSERVAÇÃO**: o Lab Management **não** dá suporte ao SCVMM 2016. Para obter informações sobre SCVMM, consulte [Virtual Machine Manager](http://go.microsoft.com/fwlink/?LinkId=226332). 
  
**Ambientes padrão:** podem conter uma combinação de máquinas virtuais e físicas. Você também pode adicionar máquinas virtuais em um ambiente padrão que é gerenciado por estruturas de virtualização de terceiros. Além disso, ambientes padrão não precisam de recursos de servidor adicional, como um servidor SCVMM.  
  
**Ambientes SCVMM:** podem conter apenas computadores virtuais gerenciados pelo SCVMM (System Center Virtual Machine Manager), ou seja, as máquinas virtuais em ambientes SCVMM somente podem executar a estrutura de virtualização Hyper-V. Entretanto, ambientes SCVMM fornecem os seguintes recursos de automação e gerenciamento, que não estão disponíveis nos ambientes padrão:  
  
- **Instantâneos do ambiente:** instantâneos de ambiente contêm o estado de um ambiente de laboratório, para que você possa restaurar rapidamente um ambiente limpo ou salvar o estado de um ambiente que foi modificado. Você também pode usar um fluxo de trabalho compilar/implantar/testar para automatizar o processo de salvar e restaurar instantâneos de ambiente.  
  
- **Ambientes armazenados:** você pode armazenar uma cópia de um ambiente SCVMM e, em seguida, implantar várias cópias desse ambiente.  
  
- **Isolamento de rede:** o isolamento de rede permite executar simultaneamente várias cópias idênticas de um ambiente SCVMM sem conflitos com o nome do computador.  
  
- **Modelos de máquina virtual:** um modelo de máquina virtual é uma máquina virtual que teve seu nome e outros identificadores removidos. Quando um modelo de VM é implantado em um ambiente SCVMM, o Microsoft Test Manager gera novos identificadores. Isso permite implantar várias cópias de uma máquina virtual em um mesmo ambiente ou vários ambientes. Em seguida, executar as máquinas virtuais simultaneamente.  
  
- **Máquinas Virtuais Armazenadas:** Uma máquina virtual armazenada na sua biblioteca Projeto de Equipe que inclui identificadores únicos.  
  
Para obter mais informações sobre esses recursos, consulte [Diretrizes para criar e gerenciar ambientes do SCVMM](https://msdn.microsoft.com/en-gb/library/ee830480.aspx).  
  
Ambientes padrão e SCVMM oferecem suporte a vários dos mesmos recursos. No entanto, há duas diferenças importantes a se considerar. A tabela a seguir compara os recursos disponíveis para ambientes padrão e SCVMM.  
  
|Recurso|Ambiente SCVMM|Ambientes padrão|  
|----------------|------------------------|---------------------------|  
|**Teste**|||  
|Executar testes manuais|Com suporte|Com suporte|  
|Executar IU codificado e outros testes automáticos|Com suporte|Com suporte|  
|Arquivo com muitos bugs usando adaptadores de diagnóstico|Com suporte|Com suporte|  
|**Compilar implantação**|||  
|Fluxos de trabalho compilar/implantar/testar automáticos|Com suporte|Com suporte|  
|**Criação e gerenciamento de ambiente**|||  
|Usar máquinas físicas, além de virtuais|Sem suporte|Com suporte|  
|Usar máquinas virtuais de terceiros|Sem suporte|Com suporte|  
|Instalar automaticamente agentes de teste em computadores com ambiente de laboratório|Com suporte|Com suporte|  
|Salvar e implantar o estado de um ambiente de laboratório usando instantâneos de ambiente|Com suporte|Sem suporte|  
|Criar ambientes de laboratório a partir de modelos VM|Com suporte|Sem suporte|  
|Ambiente de início/parada/instantâneo|Com suporte|Sem suporte|  
|Conecte-se ao ambiente usando o Visualizador de Ambiente|Com suporte|Com suporte|  
|Executa várias cópias de um ambiente ao mesmo tempo usando isolamento de rede|Com suporte|Sem suporte|  
  
### <a name="lab-management-concepts"></a>Conceitos de Lab Management

Aqui estão alguns dos conceitos adicionais com que deve familiarizar-se antes de continuar:  
  
|Termo|Descrição|  
|----------|-----------------|  
|Centro de laboratório|A área do Microsoft Test Manager em que você cria e gerencia ambientes de laboratório.|  
|Laboratório do Projeto da Equipe|A coleção de ambientes de laboratório que foi configurada para que você possa conectar-se a ela e executar suas máquinas virtuais.|  
|Biblioteca Projeto de Equipe|Um arquivo de máquinas virtuais armazenadas, modelos e ambientes de laboratório armazenados foi importado em um grupo de hosts do seu projeto da equipe. Você pode usar os itens em sua biblioteca com ambientes SCVMM; entretanto, você não pode adicioná-los diretamente em um ambiente padrão. Você não pode executar os itens em sua biblioteca; ao invés disso, você os utiliza para implantar um novo ambiente.|  
|Ambiente implantado|Um ambiente de laboratório foi implantado pelo seu laboratório de projeto da equipe para que possa conectar-se a ele e executar seus computadores.|  

#### <a name="related-topics"></a>Tópicos relacionados

* [Planejar seu laboratório](https://msdn.microsoft.com/library/ff756575%28v=vs.140%29.aspx) 
* [Administrar seu laboratório](https://msdn.microsoft.com/library/dd936084%28v=vs.140%29.aspx) 
* [Configurar para ambientes SCVMM](https://msdn.microsoft.com/library/dd380687%28v=vs.140%29.aspx) 
* [Atualizar SCVMM 2008 R2 para SCVMM 2012](upgrade-scvmm-2008-r2-scvmm-2012.md) 
* [Gerenciar permissões](https://msdn.microsoft.com/library/dd380760%28v=vs.140%29.aspx) 
* [Alterar a configuração](https://msdn.microsoft.com/library/ee704508%28v=vs.140%29.aspx) 
* [Solução de problemas](https://msdn.microsoft.com/library/ee853230%28v=vs.140%29.aspx)
  
### <a name="set-up-environments"></a>Configurar ambientes

* [Ambientes de nuvem de Build &amp; Release](use-build-or-rm-instead-of-lab-management.md)
* [Ambientes de laboratório padrão](https://msdn.microsoft.com/en-gb/library/ee390842.aspx)
* [Ambientes SCVMM (virtuais)](https://msdn.microsoft.com/en-gb/library/ee943322.aspx)
* [Criando e usando um ambiente de rede isolado](https://msdn.microsoft.com/en-gb/library/ee518924.aspx)
  
## <a name="see-also"></a>Consulte também
  
* [Instalar e configurar agentes de teste](install-configure-test-agents.md)
* [Guia do Lab Management do Visual Studio](http://go.microsoft.com/fwlink/?LinkID=230951)  
* [Gerenciando ambientes de laboratório para teste](http://go.microsoft.com/fwlink/?LinkID=252614)  
* [Blog do Team Foundation Server + operações de desenvolvimento do Visual Studio](http://go.microsoft.com/fwlink/?LinkID=254496)  
