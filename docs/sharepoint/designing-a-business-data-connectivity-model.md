---
title: Criando um modelo de conectividade de dados corporativos | Microsoft Docs
ms.custom: 
ms.date: 02/02/2017
ms.reviewer: 
ms.suite: 
ms.technology: office-development
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], designing a model
- Business Data Connectivity service [SharePoint development in Visual Studio], designing a model
author: TerryGLee
ms.author: tglee
manager: ghogen
ms.workload: office
ms.openlocfilehash: fe3de196219091478a30ff07d6c2f5916d423f15
ms.sourcegitcommit: f9fbf1f55f9ac14e4e5c6ae58c30dc1800ca6cda
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/10/2018
---
# <a name="designing-a-business-data-connectivity-model"></a>Criando um modelo de Conectividade de Dados Corporativos
  Você pode desenvolver um modelo para o serviço de conectividade de dados de negócios (BDC) com a adição de entidades e os métodos para um arquivo de modelo. Uma entidade descreve uma coleção de campos de dados. Por exemplo, uma entidade pode representar uma tabela em um banco de dados. Um método executa uma tarefa, como adicionar, excluir ou atualizar dados representados pelas entidades. Para obter mais informações, consulte [Integrando dados corporativos no SharePoint](../sharepoint/integrating-business-data-into-sharepoint.md).  
  
## <a name="adding-entities"></a>Adicionando entidades  
 Você pode adicionar uma entidade, arrastar ou copiar um **entidade** do Visual Studio **caixa de ferramentas** para o Designer BDC. Para obter mais informações, consulte [como: adicionar uma entidade para um modelo](../sharepoint/how-to-add-an-entity-to-a-model.md).  
  
 Defina os campos da entidade em uma classe. Por exemplo, você pode adicionar um campo chamado `Address` para um `Customer` classe. Você pode adicionar uma nova classe ao projeto ou usar uma classe existente criada usando outras ferramentas, como o Object Relational Designer (O/R Designer). O nome da entidade e o nome da classe que representa a entidade não precisa corresponder. Se relacionam a classe para a entidade quando você define os métodos em seu modelo.  
  
## <a name="adding-methods"></a>Adição de métodos  
 O serviço BDC chama métodos em seu modelo quando os usuários exibirem, adicionam, atualizam ou excluir informações em uma lista ou Web Part com base no seu modelo. Você deve adicionar um método para cada tarefa que o usuário pode executar o modelo. Criar métodos selecionando qualquer um dos cinco tipos de método básico do **detalhes de método BDC** janela. A tabela a seguir descreve os cinco métodos básicos de um modelo BDC.  
  
|Método|Descrição|  
|------------|-----------------|  
|Localizador|Retorna uma coleção de instâncias da entidade. Chamado quando o usuário abre a lista ou a Web Part. Para obter mais informações, consulte [como: adicionar um método Finder](../sharepoint/how-to-add-a-finder-method.md).|  
|Localizador Específico|Retorna uma instância de entidade específica. Chamado quando um usuário exibe os detalhes de um item específico em uma lista. Para obter mais informações, consulte [como: adicionar um método Finder específico](../sharepoint/how-to-add-a-specific-finder-method.md).|  
|Criador|Adiciona novos dados à fonte de dados de uma entidade. Chamado quando os usuários escolhem o **Novo Item** botão na faixa de opções de uma lista com base no modelo. Para obter mais informações, consulte [como: adicionar um método Creator](../sharepoint/how-to-add-a-creator-method.md).|  
|Atualizador|Modifica os dados em uma lista. Chamado quando os usuários atualizar informações em uma lista. Para obter mais informações, consulte [como: adicionar um método Updater](../sharepoint/how-to-add-an-updater-method.md).|  
|Excluir|Remove os dados. Chamado quando os usuários excluem um item da lista. Para obter mais informações, consulte [como: adicionar um método Deleter](../sharepoint/how-to-add-a-deleter-method.md).|  
  
## <a name="defining-method-parameters"></a>Definindo parâmetros de método  
 Quando você cria um método, o Visual Studio adiciona os parâmetros de entrada e saídos que são apropriados para o tipo de método. Esses parâmetros são apenas espaços reservados. Na maioria dos casos, você deve modificar os parâmetros para que eles transmitir ou retornam o tipo correto de dados. Por exemplo, por padrão, um método Finder retorna uma cadeia de caracteres. Na maioria dos casos, você deseja modificar o parâmetro de retorno do método Finder para que ela retorna uma coleção de entidades. Você pode fazer isso, modificando o descritor do tipo do parâmetro. Um descritor de tipo é uma coleção de atributos que descreve o tipo de dados de um parâmetro. Para obter mais informações, consulte [como: definir o descritor de tipo de um parâmetro](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md).  
  
 O Visual Studio permite que você copie descritores de tipo entre os parâmetros do modelo. Por exemplo, você pode definir um descritor de tipo nomeado `CustomerTD` para o parâmetro de retorno de `GetCustomer` método. Você pode copiar o `CustomerTD` tipo de descritor no **Explorer BDC**e, em seguida, cole esse descritor de tipo para o parâmetro de entrada do `CreateCustomer` método. Isso impede que você precisar definir o descritor do mesmo tipo, mais de uma vez.  
  
##  <a name="MethodInstances"></a>Instâncias de método  
 Quando você cria um método, o Visual Studio adiciona uma instância de método padrão. Uma instância de método é uma referência a um método, mais os valores padrão para os parâmetros. Um único método pode ter várias instâncias de método. Cada instância é uma combinação de assinatura de método e um conjunto de valores padrão. Para obter mais informações, consulte [como: definir o descritor de tipo de um parâmetro](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md).  
  
 Quando você executar o projeto, as instâncias de método aparecem em uma lista suspensa acima da lista do SharePoint. Os usuários podem escolher as instâncias de método para exibir os dados.  
  
 Para adicionar valores padrão para a instância de método, você precisa modificar o XML do modelo diretamente. Para obter mais informações, consulte [DefaultValue](http://go.microsoft.com/fwlink/?LinkID=169279).  
  
## <a name="adding-filter-descriptors"></a>Adicionando descritores de filtros  
 Os consumidores do modelo talvez queira recuperar instâncias de uma entidade que correspondem a alguns critérios. Para habilitar essa funcionalidade, você pode adicionar um descritor de filtro a um método. Descritores de filtros permitem que os consumidores de modelo filtrar conjuntos de resultados do método passando valores para métodos antes de serem executados. Para obter mais informações, consulte [como: adicionar parâmetros de filtro para operações em instâncias de limite do sistema externo](http://go.microsoft.com/fwlink/?LinkID=169267).  
  
 O SharePoint fornece vários recursos que permitem aos usuários fornecer valores de filtro. Por exemplo, Web Parts de dados de negócios fornecer uma caixa de texto de filtro. Os usuários podem limitar os dados em uma lista digitando um valor na caixa de texto. Para obter mais informações sobre como adicionar um descritor de filtro a um método, consulte [como: adicionar um descritor de filtro a um método Finder](../sharepoint/how-to-add-a-filter-descriptor-to-a-finder-method.md).  
  
### <a name="filter-descriptor-properties"></a>Propriedades do descritor de filtro  
 Você deve definir o valor da **descritor de tipo associada**, **nome**, e **tipo** propriedades de um descritor de filtro. Todas as outras propriedades são opcionais.  
  
 O **descritor de tipo associada** propriedade relaciona o descritor de filtro para um parâmetro de entrada. Quando um usuário fornece um valor de filtro, o serviço BDC passa o valor para o método usando o parâmetro de entrada.  
  
 O **tipo** propriedade descreve o padrão de filtragem que você deseja usar. No SharePoint, o padrão de filtragem que você selecionar afetará o texto que aparece na Interface do usuário (UI). Por exemplo, para um padrão de filtragem de comparador, o texto **é igual a** aparece como um controle acima de uma Web Part de dados de negócios. Para obter mais informações sobre cada padrão de filtragem, consulte [tipos de filtros com suporte pelo BDC](http://go.microsoft.com/fwlink/?LinkId=169287).  
  
 Para obter mais informações sobre as propriedades de um descritor de filtro, consulte [FilterDescriptor](http://go.microsoft.com/fwlink/?LinkID=169280).  
  
### <a name="providing-default-values"></a>Fornecer valores padrão  
 Em alguns casos, o usuário não pode fornecer um valor de filtro. Você pode fornecer um valor padrão, adicionando um valor padrão para a instância de método ou definindo o valor padrão no código do seu método. Para obter mais informações sobre como adicionar um valor padrão para a instância de método, consulte [MethodInstance](http://go.microsoft.com/fwlink/?LinkID=169282). Para obter um exemplo de como definir o valor padrão de um parâmetro de entrada no código do seu método, consulte [como: adicionar um descritor de filtro a um método Finder](../sharepoint/how-to-add-a-filter-descriptor-to-a-finder-method.md).  
  
## <a name="validating-the-model"></a>Validação do modelo  
 Você pode validar seu modelo durante o desenvolvimento. O Visual Studio identifica problemas que podem impedir que o modelo se comportando conforme o esperado. Esses problemas aparecem no Visual Studio **lista de erros**.  
  
 Você pode validar um modelo, abrindo o menu de atalho para o Designer BDC e, em seguida, escolhendo **validar**. Se o modelo contiver erros, eles aparecem no **lista de erros**. Rapidamente, você pode mover o cursor para o código que contém um erro, clique duas vezes o erro na lista. Como alternativa, você pode escolher as chaves F8 ou Shift + F8 repetidamente para a etapa para frente ou para trás ao longo de erros na lista.  
  
 Erros de validação podem ocorrer quando as regras do modelo forem violadas, de alguma forma. Por exemplo, se o **IsCollection** propriedade de um descritor de tipo está definida como **true**, mas nenhum descritor de tipo filho existe, ocorrerá um erro de validação. Talvez você precise se referem às regras de um modelo BDC para entender alguns erros que aparecem no Visual Studio **lista de erros**. Para obter mais informações sobre as regras de um modelo BDC, consulte [BDCMetadata esquema](http://go.microsoft.com/fwlink/?LinkID=169275).  
  
## <a name="debugging-the-solution-that-contains-the-model"></a>A solução que contém o modelo de depuração  
 Como você faria para depurar qualquer código no Visual Studio, você pode depurar seu código. Para depurar seu código, definir pontos de interrupção em qualquer lugar no seu código e, em seguida, iniciar o depurador. O Visual Studio abrirá o site do SharePoint. No SharePoint, crie uma lista ou a Web Part que usa dados de sua empresa. Em seguida, você pode depurar seu código. Para obter mais informações sobre como depurar projetos do SharePoint, consulte [Solucionando problemas de soluções do SharePoint](../sharepoint/troubleshooting-sharepoint-solutions.md).  
  
 Você também pode depurar código em assemblies personalizados que você adicionar ao projeto. No entanto, para depurar código em um assembly personalizado, você deve adicionar o assembly para o pacote de solução. Para obter mais informações, consulte [como: adicionar e remover Assemblies adicionais](../sharepoint/how-to-add-and-remove-additional-assemblies.md).  
  
 Para obter mais informações sobre como adicionar um assembly personalizado ao seu projeto, consulte [como: incluir um Assembly personalizado em um recurso BDC](../sharepoint/how-to-include-a-custom-assembly-in-a-bdc-feature.md).  
  
### <a name="configuring-bdc-security"></a>Configurando a segurança BDC  
 Você talvez precise modificar configurações de segurança do SharePoint para poder depurar sua solução. Para modificar essas configurações, abra o aplicativo de serviço de conectividade de dados de negócios no site do SharePoint 2010 Central Administration. No **definir permissões do repositório de metadados** caixa de diálogo, adicione sua conta de usuário e, em seguida, selecione qualquer uma das seguintes opções:  
  
|Tarefa|Opção|  
|----------|------------|  
|Para implantar modelos para o serviço de catálogo de dados corporativos.|Editar|  
|Para criar listas e Web Parts usando externos tipos de conteúdo (entidades) em seu modelo.|Selecionável em clientes|  
|Para criar, ler, atualizar e excluir dados de entidade.|Executar|  
  
 Para obter mais informações sobre essas configurações, consulte [gerenciamento de serviços de conectividade de dados corporativos](http://go.microsoft.com/fwlink/?LinkID=178883).  
  
 Você também pode definir permissões de segurança para modelos individuais ou tipos de conteúdo externo. Para obter mais informações sobre como definir as permissões de segurança de um modelo, consulte [gerenciamento de modelo BDC](http://go.microsoft.com/fwlink/?LinkID=178884). Para obter mais informações sobre como definir as permissões de segurança de um tipo de conteúdo externo, consulte [gerenciamento de tipo de conteúdo externo](http://go.microsoft.com/fwlink/?LinkID=178885).  
  
> [!NOTE]  
>  Use essas configurações para depurar uma solução no servidor do SharePoint local. Para obter mais informações sobre como definir configurações de segurança BDC no servidor do SharePoint de produção, consulte [visão geral de segurança de serviços corporativos de conectividade de dados](http://go.microsoft.com/fwlink/?LinkID=178886).  
  
### <a name="retracting-models-that-become-corrupt"></a>Cancelamento de modelos que se tornam corrompidos  
 Na primeira vez que você iniciar o depurador, o Visual Studio implanta o modelo inteiro no SharePoint. Para cada período depois disso, o Visual Studio atualiza o modelo no SharePoint com as alterações que você fizer entre implantações.  
  
 Pode haver situações em que você deseja que o Visual Studio para cancelar o modelo do SharePoint completamente. Por exemplo, um modelo pode ser corrompido.  Para reimplantar o modelo no SharePoint, defina o **atualização Incremental** propriedade do modelo para **False**, e, em seguida, iniciar o depurador. O **atualização Incremental** propriedade aparece no **propriedades** janela quando você seleciona o nó que representa o modelo no **Explorer BDC**. Por padrão, o nome do modelo é **BdcModel1**.  
  
### <a name="changing-identifier-names-of-entities-in-the-model"></a>Alterando os nomes de identificador de entidades no modelo  
 Se você alterar o nome de um identificador depois de implantar o modelo, você poderá receber um erro de implantação. Você não pode resolver esse erro, definindo o **atualização Incremental** propriedade do modelo para **False**. Você deve cancelar o modelo manualmente e, em seguida, implante a solução novamente. Para obter mais informações, consulte [Solucionando problemas de soluções do SharePoint](../sharepoint/troubleshooting-sharepoint-solutions.md). Você pode evitar esse erro, definindo o **atualização Incremental** propriedade **False** antes de implantar o modelo inicialmente.  
  
## <a name="locating-documentation-for-bdc-model-elements"></a>Localizando a documentação para os elementos de modelo BDC  
 O Visual Studio adiciona um elemento XML para o modelo para cada entidade, método ou outro item que você criar. Atributos do elemento aparecem como propriedades de **propriedades** janela. Para obter informações sobre os elementos e atributos que o Visual Studio gera ao criar o modelo, consulte [BDCMetadata esquema](http://go.microsoft.com/fwlink/?LinkID=169275).  
  
## <a name="related-topics"></a>Tópicos relacionados  
  
|Título|Descrição|  
|-----------|-----------------|  
|[Visão geral de ferramentas de design do modelo BDC](../sharepoint/bdc-model-design-tools-overview.md)|Descreve as ferramentas que você pode usar para criar visualmente um modelo para o catálogo de dados corporativos.|  
|[Como adicionar uma entidade a um modelo](../sharepoint/how-to-add-an-entity-to-a-model.md)|Mostra como adicionar tipos de conteúdo externos ou entidades, para o modelo.|  
|[Como adicionar um método Finder](../sharepoint/how-to-add-a-finder-method.md)|Mostra como adicionar um método que permite aos usuários exibir uma lista de entidades em uma lista ou Web Part.|  
|[Como adicionar um método Finder específico](../sharepoint/how-to-add-a-specific-finder-method.md)|Mostra como adicionar um método que permite aos usuários exibir os detalhes de uma entidade específica.|  
|[Como adicionar um método Creator](../sharepoint/how-to-add-a-creator-method.md)|Mostra como adicionar um método que permite aos usuários adicionar registros a uma fonte de dados diretamente de uma lista ou a Web Part.|  
|[Como adicionar um método Deleter](../sharepoint/how-to-add-a-deleter-method.md)|Mostra como adicionar um método que permite que os usuários a remover dados de uma fonte de dados usando as opções de Interface de usuário (UI) de uma lista ou Web Part.|  
|[Como adicionar um método Updater](../sharepoint/how-to-add-an-updater-method.md)|Mostra como adicionar um método que permite aos usuários alterar os registros de dados em uma fonte de dados diretamente de uma lista ou a Web Part.|  
|[Como adicionar um parâmetro a um método](../sharepoint/how-to-add-a-parameter-to-a-method.md)|Mostra como usar a janela de detalhes de método no Visual Studio para adicionar parâmetros de entrada e de retorno para um método.|  
|[Como definir o descritor de tipo de um parâmetro](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)|Mostra como definir tipos de dados do parâmetro no modelo.|  
|[Como definir uma instância de método](../sharepoint/how-to-define-a-method-instance.md)|Mostra como criar uma instância de um método que executa o BDC.|  
|[Como adicionar um descritor de filtro a um método Finder](../sharepoint/how-to-add-a-filter-descriptor-to-a-finder-method.md)|Mostra como habilitar usuários limitar o número de instâncias retornado por um método Finder.|  
|[Criando uma associação entre entidades](../sharepoint/creating-an-association-between-entities.md)|Descreve como você pode definir relações entre entidades no modelo. Web Parts de dados de negócios, a lista externa e aplicativos personalizados podem exibir essas relações de dados em uma interface de usuário (IU).|  
|[Como: criar uma associação entre entidades](../sharepoint/how-to-create-an-association-between-entities.md)|Mostra como definir relações entre entidades no modelo.|  
|[Instruções passo a passo: criando uma lista externa no SharePoint usando dados corporativos](../sharepoint/walkthrough-creating-an-external-list-in-sharepoint-by-using-business-data.md)|Fornece instruções passo a passo que mostram como criar e testar um modelo que exibe os contatos em uma lista externa do SharePoint.|  
|[Integrando dados corporativos ao SharePoint](../sharepoint/integrating-business-data-into-sharepoint.md)|Fornece uma visão geral de criação e design de modelos para o serviço de catálogo de dados corporativos.|  
  
  