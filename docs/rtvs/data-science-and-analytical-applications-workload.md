---
title: "Carga de trabalho para aplicativos de ciência de dados e análise no Visual Studio | Microsoft Docs"
description: "A carga de trabalho para Aplicativos de ciência de dados e análise no Visual Studio reúne Python, R, F# e suas respectivas distribuições de tempo de execução, incluindo Anaconda."
ms.custom: 
ms.date: 01/24/2018
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-r
- devlang-python
ms.tgt_pltfrm: 
ms.topic: landing-page
author: kraigb
ms.author: kraigb
manager: ghogen
ms.workload:
- data-science
ms.openlocfilehash: 3c84e2f3f79d49596ccd24f9f99da06eecc04351
ms.sourcegitcommit: 205d15f4558315e585c67f33d5335d5b41d0fcea
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="data-science-and-analytical-applications-workload"></a>Carga de trabalho para Aplicativos de ciência de dados e análise

A carga de trabalho de Aplicativos de Ciência de Dados e Analíticos, selecionada e instalada por meio do instalador do Visual Studio, reúne três linguagens e suas respectivas distribuições de tempo de execução:

- [R e Microsoft R Client](../rtvs/index.md)
- [Python e Anaconda](../python/overview-of-python-tools-for-visual-studio.md)
- [F# com o .NET Framework](/dotnet/fsharp/)

![Carga de trabalho para Aplicativos de ciência de dados e análise no Instalador do Visual Studio](media/data-science-workload.png)

R e Python são duas das linguagens de script principais usadas para ciência de dados. Essas duas linguagens são fáceis de aprender e compatíveis com um rico ecossistema de pacotes. Esses pacotes abordam uma ampla variedade de cenários, como aquisição de dados, limpeza, treinamento de modelo, implantação e criação de gráficos. O F# também é uma linguagem avançada do .NET que prima pela funcionalidade e é adequada a uma ampla variedade de tarefas de processamento de dados.

<!--Note link on the image because this one is large -->
[![Capturas de tela do Visual Studio com R, Python e F#](media/data-science-workload-screens.png)](media/data-science-workload-screens.png)

## <a name="workload-options"></a>Opções de carga de trabalho

Por padrão, a carga de trabalho instala as opções a seguir, que você pode modificar na seção de resumo da carga de trabalho no Instalador do Visual Studio:

- Suporte à linguagem F#
- Python:
  - Suporte da linguagem Python
  - [Anaconda3 de 64 bits](https://www.continuum.io) (Uma distribuição Python que inclui bibliotecas de ciência de dados abrangentes e um interpretador Python)
  - Suporte Web do Python
  - - Suporte do modelo Cookiecutter
- R:
  - Suporte à linguagem R
  - Suporte de tempo de execução para ferramentas de desenvolvimento do R
  - [Microsoft R Client](/machine-learning-server/r-client/what-is-microsoft-r-client) (O interpretador R totalmente compatível e com suporte da comunidade da Microsoft com bibliotecas ScaleR para computação mais rápida em nós únicos ou clusters. Você também pode usar qualquer R do [CRAN](https://cran.r-project.org/).)

Embora o F# seja incluído com várias outras cargas de trabalho e o Python tenha uma carga de trabalho própria, a carga de trabalho Aplicativos de Ciência de Dados e Analíticos é a única no momento que inclui o R. No entanto, você também pode instalar o R independentemente da carga de trabalho. Na guia **Componentes Individuais** do instalador, selecione as seguintes opções do R:

- **Atividades de desenvolvimento > suporte ao idioma do R**
- **Atividades de desenvolvimento > Microsoft R Client**
- **Compiladores, ferramentas de build e tempos de execução > Suporte de tempo de execução para ferramentas de desenvolvimento do R**

## <a name="sql-server-integration"></a>Integração ao SQL Server

O SQL Server é compatível com o uso do R e do Python para análises avançadas diretamente do SQL Server. O suporte ao R é incluído com o SQL Server 2016 e posterior; o suporte ao Python está disponível no SQL Server 2017 CTP 2.0 e posterior.

Aproveite as seguintes vantagens executando o código no local em que os dados já residem:

- **Eliminação da movimentação de dados**: em vez de mover dados do banco de dados para o aplicativo ou modelo, você pode compilar aplicativos R e Python no banco de dados. Essa funcionalidade elimina os obstáculos de segurança, de conformidade, de governança, de integridade, bem como um host de problemas semelhantes relacionados à movimentação de grandes quantidades de dados. Também consuma conjuntos de dados que não se ajustam à memória de um computador cliente.

- **Implantação fácil**: depois de preparar um modelo do R ou do Python, implantá-lo em produção é uma simples questão de inseri-los em um script do T-SQL. Os aplicativos cliente SQL codificados em qualquer linguagem poderão aproveitar os modelos e a inteligência por meio de uma chamada de procedimento armazenado. Não são necessárias integrações específicas ao R nem ao Python.

- **Desempenho e escala de nível empresarial**: você pode usar as funcionalidades avançadas do SQL Server, como os índices de repositório de tabelas e de colunas na memória com as APIs de alto desempenho escalonáveis nos pacotes RevoScaleR e RevoScalePy. A eliminação da movimentação de dados também significa que você evitará restrições de memória do cliente à medida que os dados aumentam ou que você deseja aumentar o desempenho do aplicativo.

- **Extensibilidade avançada**: você pode instalar e executar quaisquer pacotes de software livre do R ou do Python no SQL Server para compilar aplicativos de aprendizado profundo e de inteligência artificial em grandes quantidades de dados no SQL Server. A instalação de um pacote no SQL Server é tão simples quanto instalar um pacote no computador local.

- **Ampla disponibilidade sem custo adicional**: as integrações ao R e ao Python estão disponíveis em todas as edições do SQL Server 2017 e posterior, incluindo a edição Express. (O suporte ao R está disponível no SQL Server 2016 e posterior.)

Para aproveitar ao máximo a integração ao SQL Server, use o instalador do Visual Studio para instalar a carga de trabalho de **Processamento e armazenamento de dados** com a opção **SQL Server Data Tools**. A última opção habilita o SQL IntelliSense, o realce de sintaxe e a implantação.

![Carga de trabalho para Processamento e armazenamento de dados](media/data-storage-workload.png) &nbsp;&nbsp;&nbsp;&nbsp; ![Opções da carga de trabalho para Processamento e armazenamento de dados](media/data-storage-workload-options.png)

Para saber mais:

- [Trabalhando com o SQL Server e o R](../rtvs/sql-server.md)
- [Análises avançadas no banco de dados com o R no SQL Server 2016 (blog)](https://blogs.technet.microsoft.com/dataplatforminsider/2016/03/29/in-database-advanced-analytics-with-r-in-sql-server-2016/)
- [Python no SQL Server 2017: aprendizado de máquina avançado no banco de dados (blog)](https://blogs.technet.microsoft.com/dataplatforminsider/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/)

## <a name="additional-services-and-sdks"></a>SDKs e serviços adicionais

Além do que está diretamente na carga de trabalho aplicativos de ciência de dados e de análise, o serviço Azure Notebooks e o SDK do Azure para Python também são úteis para ciência de dados.

O SDK do Azure para Python facilita o consumo e gerenciamento de serviços do Microsoft Azure em aplicativos executados no Windows, Mac e Linux. Para obter mais informações, veja [SDK do Azure para Python](../python/azure-sdk-for-python.md)

O Azure Notebooks (atualmente em versão prévia) fornece acesso online gratuito aos blocos de anotações do Jupyter em execução na nuvem no Microsoft Azure. Como introdução, o serviço inclui blocos de anotações de exemplo em Python, em R e em F#. Acesse [notebooks.azure.com](https://notebooks.azure.com/).

<!--Note link on the image because this one is large -->
[![Capturas de tela Azure Notebooks com a introdução ao exemplo em R](media/data-science-workload-notebooks.png)](media/data-science-workload-notebooks.png)