---
title: "Como: criar uma associação entre entidades | Microsoft Docs"
ms.custom: 
ms.date: 02/02/2017
ms.reviewer: 
ms.suite: 
ms.technology: office-development
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: AssociationGroupTool
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], create an assocation
- Business Data Connectivity service [SharePoint development in Visual Studio], associations between entities
- BDC [SharePoint development in Visual Studio], associations between entities
- Business Data Connectivity service [SharePoint development in Visual Studio], create an assocation
- Business Data Connectivity service [SharePoint development in Visual Studio], associate external content types
- Business Data Connectivity service [SharePoint development in Visual Studio], relate entities
- BDC [SharePoint development in Visual Studio], relate entities
- BDC [SharePoint development in Visual Studio], associate external content types
author: TerryGLee
ms.author: tglee
manager: ghogen
ms.workload: office
ms.openlocfilehash: 49b4d68a8d957462954c998d96e9309944cdb9f5
ms.sourcegitcommit: f9fbf1f55f9ac14e4e5c6ae58c30dc1800ca6cda
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/10/2018
---
# <a name="how-to-create-an-association-between-entities"></a>Como criar uma associação entre entidades
  Você pode definir relações entre entidades em seu modelo de conectividade de dados de negócios (BDC) ao criar associações. O Visual Studio gera os métodos que fornecem os consumidores do modelo com informações sobre cada associação. Esses métodos podem ser consumidos pelo web parts do SharePoint, listas ou aplicativos personalizados para exibir relações de dados em uma interface de usuário (IU).  
  
 Você pode criar dois tipos de associações no designer de BDC: associações de baseada em chave estrangeiras e associações sem chave estrangeiras. Para obter mais informações, consulte [criando uma associação entre entidades](../sharepoint/creating-an-association-between-entities.md).  
  
### <a name="to-create-an-association-between-entities"></a>Para criar uma associação entre entidades  
  
1.  No **BusinessDataConnectivity** guia do **caixa de ferramentas**, escolha o **associação** item.  
  
2.  No Designer de BDC, escolha a entidade de origem e, em seguida, escolha a entidade de destino.  
  
     O **Editor de associação** é exibida.  
  
3.  Se você quiser criar uma associação de baseada em chave estrangeira, selecione o **é a associação de chave estrangeira** caixa de seleção.  
  
    1.  No **ID da fonte de** coluna do **mapeamento de identificador** de tabela, escolha o identificador ao lado de cada descritor de tipo de correspondência que aparece no **campo** coluna.  
  
         Por exemplo, no **ID da fonte de** coluna, selecione `ContactID` lado a `ReadList.salesOrderList.SalesOrderList.SalesOrder.ContactID` descritor de tipo e o `ReadItem.salesOrder.SalesOrder.ContactID` descritor de tipo.  
  
4.  Se você quiser criar uma associação sem chave estrangeira, desmarque o **é a associação de chave estrangeira** caixa de seleção.  
  
5.  Escolha o botão **OK**.  
  
6.  No Designer de BDC, aparece uma linha que representa a associação entre a entidade de origem e a entidade de destino.  
  
     O Visual Studio adiciona um método de navegador de associação para a classe de serviço da entidade de destino e a classe de serviço da entidade de origem. Para obter mais informações sobre métodos de navegação de associação, consulte [suporte para operações](http://go.microsoft.com/fwlink/?LinkId=169286).  
  
7.  No método de navegador de associação da entidade de origem, adicione o código que retorna uma coleção de entidades de destino.  
  
8.  No método de navegador de associação da entidade de destino, adicione o código que retorna a entidade de origem relacionados.  
  
     Para obter exemplos de métodos de navegador de associação, consulte [criando uma associação entre entidades](../sharepoint/creating-an-association-between-entities.md).  
  
## <a name="see-also"></a>Consulte também  
 [Criando uma associação entre entidades](../sharepoint/creating-an-association-between-entities.md)   
 [Criando um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md)   
 [Como: adicionar um método Finder](../sharepoint/how-to-add-a-finder-method.md)   
 [Como: adicionar um método Finder específico](../sharepoint/how-to-add-a-specific-finder-method.md)   
 [Como: adicionar um método Creator](../sharepoint/how-to-add-a-creator-method.md)   
 [Como: adicionar um método Deleter](../sharepoint/how-to-add-a-deleter-method.md)   
 [Como: adicionar um método Updater](../sharepoint/how-to-add-an-updater-method.md)   
 [Visão geral de ferramentas de Design de modelo BDC](../sharepoint/bdc-model-design-tools-overview.md)   
 [Como: adicionar um parâmetro a um método](../sharepoint/how-to-add-a-parameter-to-a-method.md)   
 [Como: definir uma instância de método](../sharepoint/how-to-define-a-method-instance.md)   
 [Como: definir o descritor de tipo de um parâmetro](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)   
 [Instruções passo a passo: criando uma lista externa no SharePoint usando dados corporativos](../sharepoint/walkthrough-creating-an-external-list-in-sharepoint-by-using-business-data.md)  
  
  