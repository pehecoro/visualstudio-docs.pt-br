---
title: "Criando regiões de formulário do Outlook | Microsoft Docs"
ms.custom: 
ms.date: 02/02/2017
ms.reviewer: 
ms.suite: 
ms.technology: office-development
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: MICROSOFT.OFFICE.TOOLS.OUTLOOK.FORMREGION
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- form regions [Office development in Visual Studio]
- form regions [Office development in Visual Studio], creating
- Outlook [Office development in Visual Studio], form regions
author: TerryGLee
ms.author: tglee
manager: ghogen
ms.workload: office
ms.openlocfilehash: 86f325784fdd175b5b449eb4d55d920a3f9df2d4
ms.sourcegitcommit: f9fbf1f55f9ac14e4e5c6ae58c30dc1800ca6cda
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/10/2018
---
# <a name="creating-outlook-form-regions"></a>Criando regiões de formulário do Outlook
  Você pode usar regiões de formulário para personalizar formulários do Microsoft Office Outlook. Visual Studio fornece ferramentas avançadas que tornam mais fácil para você criar, desenvolver e depurar regiões de formulário.  
  
 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]  
  
 Este tópico fornece as seguintes informações:  
  
-   [Vantagens de usar regiões de formulário](#Enhance)  
  
-   [Adicionando uma região de formulário do Outlook ao seu projeto](#Adding)  
  
-   [Usando o Designer de região de formulário](#UsingFormRegionDesigner)  
  
-   [Usando uma região de formulário projetada no Outlook](#UsingFormRegionDesignedOutlook)  
  
-   [Adicionando código personalizado a uma região de formulário](#AddingCustomCode)  
  
-   [Criar o projeto](#Building)  
  
-   [Depuração de uma região de formulário](#Debugging)  
  
-   [Implantando uma região de formulário](#Deploying)  
  
##  <a name="Enhance"></a>Vantagens de usar regiões de formulário  
 Regiões de formulário oferecem muitos aprimoramentos sobre desenvolvimento de formulários do Outlook tradicional:  
  
-   Personalize a página padrão de qualquer formato padrão.  
  
-   Adicione até 12 páginas extras para qualquer formato padrão.  
  
-   Substituem ou aprimoram a qualquer formato padrão.  
  
-   Exibir a interface do usuário personalizada no painel de leitura e em inspetores.  
  
 Para obter mais informações, consulte [personalizar páginas de formulário e regiões de formulário](http://msdn.microsoft.com/library/office/ff869060.aspx).  
  
##  <a name="Adding"></a>Adicionando uma região de formulário do Outlook ao seu projeto  
 Você pode usar o **nova região de formulário do Outlook** Assistente para criar uma nova região de formulário ou importar uma região de formulário projetada no Outlook. Além disso, se você tiver uma região de formulário que você usou em outro projeto de suplemento do VSTO do Outlook, você pode reutilizar sua região de formulário existente.  
  
###  <a name="CreatingFormRegion"></a>Criando uma nova região de formulário usando o Assistente  
 Para criar uma região de formulário, adicione um **região de formulário do Outlook** item a um projeto de suplemento do VSTO do Outlook. Isso inicia o **nova região de formulário do Outlook** assistente.  
  
 Use o Assistente para indicar se você deseja criar uma nova região de formulário ou importar uma região de formulário projetada no Outlook. Para obter mais informações sobre como criar uma nova região de formulário, consulte [usando o Designer de região de formulário](#UsingFormRegionDesigner). Para obter mais informações sobre como usar uma região de formulário projetada no Outlook, consulte [importando uma região de formulário projetada no Outlook](#UsingFormRegionDesignedOutlook).  
  
 Use o Assistente para especificar o tipo de região de formulário que você deseja criar. A tabela a seguir descreve cada tipo de região de formulário.  
  
|Tipo de região|Descrição|  
|-----------------|-----------------|  
|Separado|Adiciona a região do formulário como uma nova página em um formulário do Outlook.|  
|Adjacentes|Anexa a região do formulário à parte inferior da página padrão de um formulário do Outlook.|  
|Substituição|Adiciona a região do formulário como uma nova página que substitui a página padrão de um formulário do Outlook.|  
|Substituir tudo|Substitui todo o formulário do Outlook pela região do formulário.|  
  
 Você também pode usar o Assistente para especificar as condições de exibição e selecione o tipo de formulário para estender. Para obter mais informações, consulte [como: adicionar uma região de formulário a um projeto de suplemento do Outlook](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md).  
  
 As seleções feitas no assistente afetam as opções que estão disponíveis em outras páginas do assistente. Por exemplo, se você selecionar **Adjoining** ou **separada** no **criar uma nova região de formulário do Outlook** página, em seguida, o **título** e **Descrição** campos não estão disponíveis no **fornecer um texto descritivo e selecione suas preferências de exibição** página. Isso ocorre porque o Outlook não usa esses campos ao exibir uma região de formulário adjacente ou separado.  
  
#### <a name="form-region-files"></a>Arquivos de região de formulário  
 Quando você concluir o **nova região de formulário do Outlook** assistente, o Visual Studio adiciona automaticamente os arquivos a seguir ao seu projeto:  
  
-   Um arquivo de código de região de formulário. Este arquivo tem o nome que você especificar para o **região de formulário do Outlook** item o **Adicionar Novo Item** caixa de diálogo. Adicione código para tratar eventos de região de formulário para este arquivo.  
  
-   Um arquivo de código de designer de região de formulário. Este arquivo contém o código gerado pelo designer de região de formulário e não deve ser editado diretamente.  
  
-   Um arquivo de armazenamento de formulário do Outlook (. ofs).  
  
    > [!NOTE]  
    >  Esse arquivo só é adicionado ao projeto, se você importar uma região de formulário projetada no Outlook.  
  
#### <a name="form-region-factory-class"></a>Classe de fábrica de região de formulário  
 O arquivo de código de região de formulário contém uma classe parcial que implementa o <xref:Microsoft.Office.Tools.Outlook.IFormRegionFactory> interface. Esta é a classe de fábrica de região de formulário. A classe de fábrica de região de formulário é responsável pela criação de novas instâncias da região de formulário.  
  
 Você pode encontrar essa classe expandindo o **fábrica de região de formulário** região.  
  
 O **nova região de formulário do Outlook** assistente adiciona atributos para essa classe que especifique o nome interno da região de formulário e as classes de mensagem que exibem a região do formulário. Você pode modificar esses atributos manualmente depois que o arquivo foi adicionado ao projeto.  
  
 A maioria da classe de fábrica de região de formulário é implementado no arquivo de designer de região de formulário. No entanto, o `FormRegionInitializing` manipulador de eventos é exposto no arquivo de código de região de formulário. Você pode usar este manipulador de eventos para especificar se o Outlook deve exibir a região do formulário. Para obter mais informações, consulte [manipulando eventos de região de formulário](#HandlingFormRegionEvents).  
  
###  <a name="AddingExistingFormRegion"></a>Adicionando uma região de formulário existente ao seu projeto  
 Se você tiver uma região de formulário do Outlook usado em outro projeto do Outlook, você pode reutilizá-lo em seu projeto de suplemento do VSTO Outlook atual usando o **Add Existing Item** caixa de diálogo.  
  
 A região do formulário existente deve ter um arquivo de código (. cs ou. vb); Você não pode adicionar arquivos de armazenamento de formulário do Outlook (. ofs) usando o **Add Existing Item** caixa de diálogo. No entanto, você pode criar uma nova região de formulário importando um arquivo de armazenamento de formulário do Outlook. Para obter mais informações, consulte [como: adicionar uma região de formulário a um projeto de suplemento do Outlook](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md).  
  
##  <a name="UsingFormRegionDesigner"></a>Usando o Designer de região de formulário  
 O designer de região de formulário ajuda você a criar o layout e a aparência de uma região de formulário. Arraste os controles gerenciados para a superfície do designer, clique duas vezes em controles para abrir os manipuladores de eventos e definir propriedades **propriedades** janela.  
  
> [!NOTE]  
>  Você pode encontrar as propriedades que afetam a maneira como a região de formulário aparece no Outlook sob o **manifesto** nó o **propriedades** janela.  
  
 O designer de região de formulário está disponível apenas se você selecionar **cria uma nova região de formulário** no **selecione como você deseja criar a região do formulário** página do **nova região de formulário do Outlook** Assistente.  
  
 Há três maneiras de abrir o designer de região de formulário:  
  
-   Em **Solution Explorer**, clique duas vezes no arquivo de código de região de formulário.  
  
-   Em **Solution Explorer**, com o botão direito do arquivo de código de região de formulário e, em seguida, clique em **Designer de exibição**.  
  
-   Em **Solution Explorer**, selecione o arquivo de código de região de formulário e, em seguida, no **exibição** menu, clique em **Designer**.  
  
 O suporte de designer de região de formulário apenas controles gerenciados. Não é possível adicionar controles nativos do Outlook.  
  
##  <a name="UsingFormRegionDesignedOutlook"></a>Importando uma região de formulário projetada no Outlook  
 Quando você cria no Outlook, você pode adicionar controles nativos do Outlook para a região do formulário. Controles nativos do Outlook permitem associar dados do Outlook no tempo de design. No entanto, você não pode usar o designer de região de formulário para adicionar controles gerenciados ou alterar o design da região de formulário.  
  
 Você pode importar regiões de formulário para um projeto de suplemento do VSTO Outlook usando o **nova região de formulário do Outlook** assistente. Sobre o **selecione como você deseja criar a região de formulário** , selecione **importar um arquivo de armazenamento de formulário do Outlook (. ofs)**. Em seguida, você pode navegar para o local de um arquivo de armazenamento de formulário do Outlook (. ofs). (O outlook salva regiões de formulário como arquivos. ofs).  
  
 O **nova região de formulário do Outlook** assistente copia o arquivo. ofs para o diretório do projeto e adiciona as referências de controle para o arquivo de designer de região de formulário. Em seguida, você pode manipular eventos de controle no arquivo de código de região de formulário.  
  
 Para lidar com eventos em um projeto do Visual Basic, selecione um evento da lista de nomes de método na parte superior do Editor de códigos.  
  
 Para manipular eventos em um projeto c#, inscrever-se para eventos de controle de <xref:Microsoft.Office.Tools.Outlook.FormRegionControl.FormRegionShowing> método. Para obter mais informações, consulte [como: inscrever-se e cancelar a assinatura de eventos &#40; C &#35; Guia de programação &#41; ](/dotnet/csharp/programming-guide/events/how-to-subscribe-to-and-unsubscribe-from-events).  
  
 Você pode alterar as propriedades da região de formulário no `InitializeManifest` método da classe de fábrica de região de formulário.  
  
> [!NOTE]  
>  Para importar uma região de formulário, você deve estar trabalhando em um projeto que tem como destino a mesma versão do Outlook que você instalou no computador de desenvolvimento. Por exemplo, se você tiver o Outlook 2010 instalado, a importação de um formulário região só funcionará em um projeto foi criado usando o **suplemento do Outlook 2010** modelo de projeto.  
  
### <a name="updating-an-imported-form-regions-design"></a>Atualizando o Design de uma região formulário importado  
 Você pode adicionar, remover ou alterar os controles na região de formulário. Antes de fazer isso, faça backup de qualquer código que você adicionou ao arquivo de código de região de formulário. Em seguida, abra o arquivo. ofs no Outlook, modificar a região do formulário e, em seguida, salve as alterações. Use o **nova região de formulário do Outlook** Assistente para importar o arquivo. ofs modificado. Você pode colar o código para o novo arquivo de código de região de formulário.  
  
##  <a name="AddingCustomCode"></a>Adicionando código personalizado a uma região de formulário  
 O <xref:Microsoft.Office.Tools.Outlook> namespace fornece acesso para classes que representam a região do formulário, o item do Outlook que exibe a região de formulário e outros itens úteis. O **região de formulário do Outlook** item automaticamente adiciona uma referência a esse assembly no projeto e insere as **usando** ou **importações** instrução na parte superior das arquivo de código de região de formulário.  
  
 Você pode usar propriedades, métodos e classes no namespace Microsoft.Office.Interop.Outlook para realizar a maior parte das tarefas de programação do Outlook. Para obter mais informações sobre o modelo de objeto do Outlook, consulte [visão geral de modelo de objeto do Outlook](../vsto/outlook-object-model-overview.md). Para obter exemplos de tarefas típicas que usar o modelo de objeto do Outlook, consulte [soluções do Outlook](../vsto/outlook-solutions.md).  
  
###  <a name="HandlingFormRegionEvents"></a>Manipulação de eventos de região de formulário  
 O **região de formulário do Outlook** item adiciona automaticamente os manipuladores de eventos de três a seguir para o arquivo de código de região de formulário.  
  
|evento|Descrição|  
|-----------|-----------------|  
|FormRegionInitializing|Ocorre antes que a região de formulário seja inicializada. Você pode verificar as condições em que este manipulador de eventos para determinar se o Outlook deve exibir a região do formulário. Para obter mais informações, consulte [como: evitar que o Outlook exiba uma região de formulário](../vsto/how-to-prevent-outlook-from-displaying-a-form-region.md).|  
|FormRegionShowing|Ocorre após uma instância da região do formulário ser criada, mas antes da região do formulário ser exibida.|  
|FormRegionClosed|Ocorre antes da região do formulário ser fechada.|  
  
##  <a name="Building"></a>Criar o projeto  
 Quando você compila um projeto de suplemento do VSTO do Outlook que contém uma região de formulário, o Visual Studio adiciona as informações a seguir no registro:  
  
-   Uma chave para cada classe de mensagem que está associado uma ou mais regiões de formulário.  
  
-   Uma entrada para cada região de formulário e um valor que representa o nome do suplemento do VSTO do Outlook.  
  
 Outlook usa essas informações para carregar as regiões de formulário.  
  
##  <a name="Debugging"></a>Depuração de uma região de formulário  
 Você pode depurar um Outlook VSTO suplemento que contém uma região de formulário, exatamente como você faria para depurar outras [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] projetos. Quando você inicia o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] depurador, o Visual Studio inicia automaticamente o Outlook.  
  
 Para exibir a região de formulário, você deve abrir o item apropriado do Outlook. Por exemplo, se uma região de formulário adjacente é anexada à parte inferior de um item de email, abra um item de email.  
  
##  <a name="Deploying"></a>Implantando uma região de formulário  
 Regiões de formulário são implantados automaticamente com o Add-in do Outlook VSTO associado. Portanto, não é necessário realizar tarefas especiais para implantar uma região de formulário. Para obter mais informações sobre a implantação de suplementos do VSTO, consulte [implantar uma solução Office](../vsto/deploying-an-office-solution.md).  
  
## <a name="related-topics"></a>Tópicos relacionados  
  
|Título|Descrição|  
|-----------|-----------------|  
|[Diretrizes para criar regiões de formulário do Outlook](../vsto/guidelines-for-creating-outlook-form-regions.md)|Fornece informações que podem ajudá-lo a otimizar as regiões de formulário e evitar problemas potenciais.|  
|[Como adicionar uma região do formulário a um projeto de suplemento do Outlook](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)|Mostra como criar uma região de formulário para estender um formulário personalizado ou padrão do Microsoft Office Outlook usando o **nova região de formulário do Outlook** assistente.|  
|[Associando uma região do formulário a uma classe de mensagem do Outlook](../vsto/associating-a-form-region-with-an-outlook-message-class.md)|Explica como especificar quais itens do Microsoft Office Outlook exibem uma região de formulário, associando a região de formulário com a classe de mensagem de cada item.|  
|[Instruções passo a passo: criando uma região do formulário do Outlook](../vsto/walkthrough-designing-an-outlook-form-region.md)|Mostra como criar uma região de formulário personalizado que aparece como uma nova página na janela do Inspetor de um item de contato.|  
|[Instruções passo a passo: importando uma região do formulário projetada no Outlook](../vsto/walkthrough-importing-a-form-region-that-is-designed-in-outlook.md)|Mostra como criar uma região de formulário do Microsoft Office Outlook e, em seguida, importe a região de formulário para um projeto de suplemento do VSTO do Outlook usando o **nova região de formulário do Outlook** assistente.|  
|[Acessando uma região do formulário no tempo de execução](../vsto/accessing-a-form-region-at-run-time.md)|Descreve como escrever código para mostrar, ocultar ou modificar controles em uma região de formulário e permitir que os usuários executar o código de outras áreas no seu projeto usando o `Globals` classe.|  
|[Como evitar que o Outlook exiba uma região do formulário](../vsto/how-to-prevent-outlook-from-displaying-a-form-region.md)|Mostra como impedir que o Microsoft Office Outlook exiba uma região de formulário para um determinado item.|  
|Mostra como acessar o item do Outlook no qual uma região de formulário é exibido.|  
|[Personalizar ações em regiões de formulário do Outlook](../vsto/custom-actions-in-outlook-form-regions.md)|Descreve como habilitar usuários responder a um item do Outlook.|  
  
  