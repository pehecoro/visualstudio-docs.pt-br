---
title: "Como: recuperar o serviço de projeto do SharePoint | Microsoft Docs"
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
helpviewer_keywords: SharePoint project service
author: TerryGLee
ms.author: tglee
manager: ghogen
ms.workload: office
ms.openlocfilehash: b1abdf4a48d05285a7394469dd391caf48981f9f
ms.sourcegitcommit: f9fbf1f55f9ac14e4e5c6ae58c30dc1800ca6cda
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/10/2018
---
# <a name="how-to-retrieve-the-sharepoint-project-service"></a>Como recuperar o serviço de projeto do SharePoint
  Você pode acessar o serviço de projeto do SharePoint nos seguintes tipos de soluções:  
  
-   Uma extensão do sistema de projeto do SharePoint, como uma extensão de projeto, a extensão de item de projeto ou a definição de tipo de item de projeto. Para obter mais informações sobre esses tipos de extensões, consulte [estendendo o sistema de projeto do SharePoint](../sharepoint/extending-the-sharepoint-project-system.md).  
  
-   Uma extensão do **conexões do SharePoint** nó **Server Explorer**. Para obter mais informações sobre esses tipos de extensões, consulte [estendendo o nó de conexões do SharePoint no Gerenciador de servidores](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md).  
  
-   Outro tipo de extensão do Visual Studio, como um VSPackage.  
  
## <a name="retrieving-the-service-in-project-system-extensions"></a>Recuperando o serviço nas extensões do sistema de projeto  
 Em qualquer extensão do sistema de projeto do SharePoint, você pode acessar o serviço de projeto usando o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject.ProjectService%2A> propriedade de um <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject> objeto.  
  
 Você também pode recuperar o serviço de projeto usando os procedimentos a seguir.  
  
#### <a name="to-retrieve-the-service-in-a-project-extension"></a>Para recuperar o serviço em uma extensão de projeto  
  
1.  Na implementação do <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> interface, localize o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension.Initialize%2A> método.  
  
2.  Use o *projectService* parâmetro para acessar o serviço.  
  
     O exemplo de código a seguir demonstra como usar o serviço de projeto para gravar uma mensagem para o **saída** janela e **lista de erros** janela em uma extensão de projeto simples.  
  
     [!code-vb[SPExtensibility.ProjectService.FromProjectSystemExtensions#1](../sharepoint/codesnippet/VisualBasic/spextensibility.projectservice.fromprojectsystemextensions.getprojectservice/extension/extension.vb#1)]
     [!code-csharp[SPExtensibility.ProjectService.FromProjectSystemExtensions#1](../sharepoint/codesnippet/CSharp/spextensibility.projectservice.fromprojectsystemextensions.getprojectservice/extension/extension.cs#1)]  
  
     Para obter mais informações sobre a criação de extensões do projeto, consulte [como: criar uma extensão de projeto do SharePoint](../sharepoint/how-to-create-a-sharepoint-project-extension.md).  
  
#### <a name="to-retrieve-the-service-in-a-project-item-extension"></a>Para recuperar o serviço em uma extensão de item de projeto  
  
1.  Na implementação do <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension> interface, localize o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension.Initialize%2A> método.  
  
2.  Use o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemType.ProjectService%2A> propriedade o *projectItemType* parâmetro para recuperar o serviço.  
  
     O exemplo de código a seguir demonstra como usar o serviço de projeto para gravar uma mensagem para o **saída** janela e **lista de erros** janela em uma extensão simple do **dedefiniçãodelista** item de projeto.  
  
     [!code-vb[SPExtensibility.ProjectService.FromProjectSystemExtensions#2](../sharepoint/codesnippet/VisualBasic/spextensibility.projectservice.fromprojectsystemextensions.getprojectservice/extension/extension.vb#2)]
     [!code-csharp[SPExtensibility.ProjectService.FromProjectSystemExtensions#2](../sharepoint/codesnippet/CSharp/spextensibility.projectservice.fromprojectsystemextensions.getprojectservice/extension/extension.cs#2)]  
  
     Para obter mais informações sobre como criar extensões de item de projeto, consulte [como: criar uma extensão de Item de projeto do SharePoint](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md).  
  
#### <a name="to-retrieve-the-service-in-a-project-item-type-definition"></a>Para recuperar o serviço em uma definição de tipo de item de projeto  
  
1.  Na implementação do <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> interface, localize o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A> método.  
  
2.  Use o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition.ProjectService%2A> propriedade o *typeDefinition* parâmetro para recuperar o serviço.  
  
     O exemplo de código a seguir demonstra como usar o serviço de projeto para gravar uma mensagem para o **saída** janela e **lista de erros** janela em uma definição de tipo de item de projeto simples.  
  
     [!code-vb[SPExtensibility.ProjectService.FromProjectSystemExtensions#3](../sharepoint/codesnippet/VisualBasic/spextensibility.projectservice.fromprojectsystemextensions.getprojectservice/extension/extension.vb#3)]
     [!code-csharp[SPExtensibility.ProjectService.FromProjectSystemExtensions#3](../sharepoint/codesnippet/CSharp/spextensibility.projectservice.fromprojectsystemextensions.getprojectservice/extension/extension.cs#3)]  
  
     Para obter mais informações sobre como definir tipos de item de projeto, consulte [como: definir um tipo de Item de projeto do SharePoint](../sharepoint/how-to-define-a-sharepoint-project-item-type.md).  
  
## <a name="retrieving-the-service-in-server-explorer-extensions"></a>Recuperando o serviço nas extensões do Gerenciador de servidor  
 Em uma extensão do **conexões do SharePoint** nó **Server Explorer**, você pode acessar o serviço de projeto usando o <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode.ServiceProvider%2A> propriedade de um <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode> objeto.  
  
#### <a name="to-retrieve-the-service-in-a-server-explorer-extension"></a>Para recuperar o serviço em uma extensão do Gerenciador de servidores  
  
1.  Obter um <xref:System.IServiceProvider> de objeto o <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode.ServiceProvider%2A> propriedade de um <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode> objeto em sua extensão.  
  
2.  Use o <xref:System.IServiceProvider.GetService%2A> método para solicitar um <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService> objeto.  
  
     O exemplo de código a seguir demonstra como usar o serviço de projeto para gravar uma mensagem para o **saída** janela e **lista de erros** janela a partir de um menu de atalho que adiciona a extensão em nós lista **Gerenciador de servidores**.  
  
     [!code-vb[SPExtensibility.ProjectService.FromSPExplorerExtensions#1](../sharepoint/codesnippet/VisualBasic/spextensibility.projectservice.fromspexplorerextensions.getprojectservice/extension/extension.vb#1)]
     [!code-csharp[SPExtensibility.ProjectService.FromSPExplorerExtensions#1](../sharepoint/codesnippet/CSharp/spextensibility.projectservice.fromspexplorerextensions.getprojectservice/extension/extension.cs#1)]  
  
     Para obter mais informações sobre como estender o **conexões do SharePoint** nó **Server Explorer**, consulte [como: estender um nó SharePoint no Gerenciador de servidores](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md).  
  
## <a name="retrieving-the-service-in-other-visual-studio-extensions"></a>Recuperando o serviço em outras extensões do Visual Studio  
 Você pode recuperar o serviço de projeto em um VSPackage ou em qualquer extensão do Visual Studio que tem acesso a um <xref:EnvDTE80.DTE2> objeto no modelo de objeto de automação, como um Assistente de modelo de projeto que implementa o <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> interface.  
  
 Em um VSPackage, você pode solicitar uma <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService> objeto usando um dos seguintes métodos:  
  
-   O <xref:System.IServiceProvider.GetService%2A> método de um VSPackage gerenciado que deriva de <xref:Microsoft.VisualStudio.Shell.Package> classe. Para obter mais informações, consulte [como: obter um serviço](../extensibility/how-to-get-a-service.md).  
  
-   Estático <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> método. Para obter mais informações, consulte [GetGlobalService Use](../extensibility/internals/service-essentials.md#how-to-use-getglobalservice).  
  
 Em uma extensão do Visual Studio que tem acesso a um <xref:EnvDTE80.DTE2> objeto, você pode solicitar uma <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService> objeto usando o <xref:Microsoft.VisualStudio.Shell.ServiceProvider.GetService%2A> método de um <xref:Microsoft.VisualStudio.Shell.ServiceProvider> objeto. Para obter mais informações, consulte [obtendo um serviço do objeto DTE](../extensibility/how-to-get-a-service.md#getting-a-service-from-the-dte-object).  
  
## <a name="see-also"></a>Consulte também  
 [Usando o serviço de projeto do SharePoint](../sharepoint/using-the-sharepoint-project-service.md)   
 [Como: obter um serviço](../extensibility/how-to-get-a-service.md)   
 [Como usar assistentes com modelos do projeto](../extensibility/how-to-use-wizards-with-project-templates.md)  
  
  