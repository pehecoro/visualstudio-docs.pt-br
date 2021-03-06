---
title: "Como: permitir a execução por trás de documentos com permissões restritas de código | Microsoft Docs"
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
helpviewer_keywords:
- Information Rights Management [Office development in Visual Studio]
- permissions [Office development in Visual Studio]
- IRM [Office development in Visual Studio]
- code [Office development in Visual Studio], running behind restricted documents
- documents [Office development in Visual Studio], restricted permissions
- Office documents [Office development in Visual Studio, restricted permissions
author: TerryGLee
ms.author: tglee
manager: ghogen
ms.workload: office
ms.openlocfilehash: 09336e72cc9e1e1bc0a407314d4fa9fd6bc2a2c9
ms.sourcegitcommit: f9fbf1f55f9ac14e4e5c6ae58c30dc1800ca6cda
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/10/2018
---
# <a name="how-to-permit-code-to-run-behind-documents-with-restricted-permissions"></a>Como permitir que o código execute documentos code-behind com permissões restritas
  Você pode usar o recurso de gerenciamento de direitos de informação (IRM) do Microsoft Office para restringir permissões para um documento ou a pasta de trabalho. Por padrão, o código por trás de um documento do Microsoft Office Word restrito ou pasta de trabalho do Microsoft Office Excel não é permitido para execução. Você pode alterar o padrão para que as extensões de código gerenciado podem acessar o modelo de objeto e sua solução funcione.  
  
 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]  
  
 Você deve ser o autor do documento ou pasta de trabalho ou ter acesso de controle total para ser capaz de alterar as configurações de permissão.  
  
### <a name="to-permit-code-to-run-behind-documents-with-restricted-permissions"></a>Para permitir que o código seja executado atrás de documentos com permissões restritas  
  
1.  Abra o documento ou a pasta de trabalho do Word ou Excel.  
  
2.  Clique o **arquivo** guia, aponte para **preparar**, aponte para **Restringir permissão**e, em seguida, clique em **acesso restrito**.  
  
    > [!NOTE]  
    >  No primeiro uso, você precisará instalar o cliente Windows Rights Management. Depois de instalar o cliente, talvez seja necessário repetir as etapas.  
  
3.  No **permissão** caixa de diálogo, selecione **Restringir permissão neste documento**e, em seguida, clique em **mais opções**.  
  
4.  Em **permissões adicionais para usuários**, selecione **acessar conteúdo de forma programática**.  
  
 Word ou Excel permitirá acesso programático ao modelo de objeto.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciamento de direitos de informação e visão geral de extensões de código gerenciado](../vsto/information-rights-management-and-managed-code-extensions-overview.md)   
 [Proteção de documento em soluções de nível de documento](../vsto/document-protection-in-document-level-solutions.md)   
 [Proteção por senha em documentos do Office](../vsto/password-protection-on-office-documents.md)   
 [Projetando e criando soluções do Office](../vsto/designing-and-creating-office-solutions.md)   
 [Protegendo soluções do Office](../vsto/securing-office-solutions.md)   
 [Implantando uma solução do Office](../vsto/deploying-an-office-solution.md)  
  
  