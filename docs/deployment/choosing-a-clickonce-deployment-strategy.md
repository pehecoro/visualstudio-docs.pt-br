---
title: "Escolhendo uma estratégia de implantação do ClickOnce | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-deployment
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, strategies
- deploying applications, ClickOnce
ms.assetid: 98bcab65-ab8b-4ed1-9adc-fdacf92b8106
caps.latest.revision: "19"
author: stevehoag
ms.author: shoag
manager: wpickett
ms.workload: multiple
ms.openlocfilehash: fffb73fac64aad880531fb8ea51904fb5ac71b16
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="choosing-a-clickonce-deployment-strategy"></a>Escolhendo uma estratégia de implantação do ClickOnce
Há três estratégias diferentes para implantar um aplicativo [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]; a estratégia escolhida depende principalmente do tipo de aplicativo que você está implantando. As três estratégias de implantação são as seguintes:  
  
-   Instalação da Web ou de um compartilhamento de rede  
  
-   Instalação de um CD  
  
-   Iniciação do aplicativo da Web ou de um compartilhamento de rede  
  
    > [!NOTE]
    >  Além de selecionar uma estratégia de implantação, talvez você também deseje selecionar uma estratégia para fornecer atualizações do aplicativo. Para obter mais informações, consulte [escolhendo uma estratégia de atualização do ClickOnce](../deployment/choosing-a-clickonce-update-strategy.md).  
  
## <a name="install-from-the-web-or-a-network-share"></a>Instalação da Web ou de um compartilhamento de rede  
 Quando você usa essa estratégia, o aplicativo é implantado em um servidor Web ou compartilhamento de arquivos de rede. Quando um usuário final desejar instalar o aplicativo, ele clicará em um ícone em uma página da Web ou clicará duas vezes em um ícone no compartilhamento de arquivos. O aplicativo é baixado e, em seguida, instalado e iniciado no computador do usuário final. Itens são adicionados para o **iniciar** menu e **adicionar ou remover programas** na **painel de controle**.  
  
 Como essa estratégia depende de conectividade de rede, ela funcionará melhor para aplicativos que serão implantados para usuários com acesso a uma rede local ou a uma conexão com a Internet de alta velocidade.  
  
 Se você implantar o aplicativo da Web, poderá passar argumentos para o aplicativo quando ele for ativado por meio de uma URL. Para obter mais informações, consulte [como: recuperar informações de cadeia de caracteres de consulta em um aplicativo ClickOnce Online](../deployment/how-to-retrieve-query-string-information-in-an-online-clickonce-application.md). Você não poderá passar argumentos para um aplicativo ativado ao usar qualquer um dos outros métodos descritos neste documento.  
  
 Para habilitar essa estratégia de implantação no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)], clique em **da Web** ou **compartilhamento de arquivo ou caminho de UNC de um** no **como instalado** página do Assistente de publicação.  
  
 Essa é a estratégia de implantação padrão.  
  
## <a name="install-from-a-cd"></a>Instalação de um CD  
 Ao usar essa estratégia, seu aplicativo será implantado em mídia removível como um CD-ROM ou DVD. Assim como acontece com a opção anterior, quando o usuário optar por instalar o aplicativo, ele é instalado e iniciado e itens são adicionados ao **iniciar** menu e **adicionar ou remover programas** na **controle Painel**.  
  
 Essa estratégia funcionará melhor para aplicativos que serão implantados para usuários sem conectividade de rede persistente ou com conexões de baixa largura de banda. Como o aplicativo é instalado de mídia removível, nenhuma conexão de rede é necessária para instalação; no entanto, conectividade de rede ainda é necessária para atualizações do aplicativo.  
  
 Para habilitar essa estratégia de implantação no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)], clique em **de um CD-ROM ou DVD-ROM** no **como instalado** página do Assistente de publicação.  
  
 Para habilitar manualmente essa estratégia de implantação, altere o **deploymentProvider** marca no manifesto de implantação. (No Visual Studio, essa propriedade é exposta como **URL de instalação** no **publicar** página no Designer de projeto. É no Mage.exe **local iniciar**.)  
  
## <a name="start-the-application-from-the-web-or-a-network-share"></a>Iniciação do aplicativo da Web ou de um compartilhamento de rede  
 Esta estratégia é como a primeira, exceto que o aplicativo se comporta como um aplicativo Web. Quando o usuário clica em um link em uma página da Web (ou clica duas vezes em um ícone no compartilhamento de arquivos), o aplicativo é iniciado. Quando os usuários fechem o aplicativo, ele não está mais disponível no computador local; nada é adicionado a **iniciar** menu ou **adicionar ou remover programas** na **painel de controle**.  
  
> [!NOTE]
>  Tecnicamente, o aplicativo será baixado e instalado em um cache de aplicativos no computador local, exatamente como um aplicativo Web é baixado no cache da Web. Como no cache da Web, os arquivos serão eventualmente removidos do cache de aplicativos. No entanto, a percepção do usuário é que o aplicativo está sendo executado da Web ou do compartilhamento de arquivos.  
  
 Essa estratégia funciona melhor para aplicativos que são usados com pouca frequência, por exemplo, uma ferramenta de benefícios de funcionários que é normalmente executada apenas uma vez por ano.  
  
 Para habilitar essa estratégia de implantação no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)], clique em **não instalam o aplicativo** no **instalar ou executar da Web** página do Assistente de publicação.  
  
 Para habilitar essa estratégia de implantação, manualmente, altere o **instalar** marca no manifesto de implantação. (O valor pode ser **true** ou **false**. Em Mage.exe, use o **Online somente** opção o **tipo de aplicativo** lista.)  
  
## <a name="web-browser-support"></a>Suporte a navegadores da Web  
 Os aplicativos destinados ao .NET Framework 3.5 podem ser instalados usando qualquer navegador.  
  
 Os aplicativos destinados ao .NET Framework 2.0 exigem o Internet Explorer.  
  
## <a name="see-also"></a>Consulte também  
 [Segurança e implantação do ClickOnce](../deployment/clickonce-security-and-deployment.md)   
 [Escolhendo uma estratégia de atualização do ClickOnce](../deployment/choosing-a-clickonce-update-strategy.md)   
 [Como publicar um Aplicativo ClickOnce usando o Assistente de Publicação](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)   
 [Protegendo aplicativos ClickOnce](../deployment/securing-clickonce-applications.md)