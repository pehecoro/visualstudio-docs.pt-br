---
title: "Limitações na depuração de WCF | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-debug
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging, WCF
- WCF, debugging limitations
ms.assetid: 8e0333c4-1ddc-4abe-8f1c-d19bf6a2a07a
caps.latest.revision: "30"
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.workload: multiple
ms.openlocfilehash: 14340ad3a19feb6340b836b1db8d71b3a8adcd83
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="limitations-on-wcf-debugging"></a>Limitações da depuração WCF
Há três modos de começar a depuração de um serviço WCF:  
  
-   Você está depurando um processo de cliente que chama um serviço. O depurador entra no serviço. O serviço não tem que estar na mesma solução que o aplicativo cliente.  
  
-   Você está depurando um processo de cliente que faz a solicitação para um serviço. O serviço deve fazer parte de sua solução.  
  
-   Você usa **anexar ao processo** para anexar a um serviço que está sendo executado. A depuração começa dentro do serviço.  
  
 Este tópico descreve limitações nesses cenários.  
  
## <a name="limitations-on-stepping-into-a-service"></a>Limitações para entrar em um serviço  
 Para entrar em um serviço de aplicativos cliente que você está depurando, as seguintes condições devem ser atendidas:  
  
-   O cliente deve chamar o serviço usando um objeto do cliente síncrono.  
  
-   A operação do contrato não pode ser unidirecional.  
  
-   Se o servidor for assíncrono, você não poderá exibir a pilha de chamadas completa enquanto estiver executando o código no serviço.  
  
-   A depuração deve estar habilitada com o seguinte código no arquivo app.config ou no Web.config:  
  
    ```  
    <system.web>  
      <compilation debug="true" />  
    </system.web>  
    ```  
  
     Esse código só precisa ser adicionado uma vez. Você pode adicionar esse código editando o arquivo. config ou anexando-se ao serviço usando **anexar ao processo**. Quando você usa **anexar ao processo** em um serviço, o código de depuração é automaticamente adicionado ao arquivo. config. Depois disso, você pode depurar e entrar no serviço sem precisar editar o arquivo .config.  
  
## <a name="limitations-on-stepping-out-of-a-service"></a>Limitações para sair de um serviço  
 Sair de um serviço e voltar para o cliente tem as mesmas restrições descritas para entrar em um serviço. Além disso, o depurador deve ser anexado ao cliente. Se você estiver depurando um cliente e entrando em um serviço, o depurador permanecerá anexado ao serviço. Isso é verdadeiro se você iniciou o cliente usando **iniciar depuração** ou conectados ao cliente usando **anexar ao processo**. Se você tiver começado a depurar anexando ao serviço, o depurador ainda não estará anexado ao cliente. Nesse caso, se você tiver para a etapa do serviço e de volta para o cliente, você deve primeiro usar **anexar ao processo** anexar manualmente ao cliente.  
  
## <a name="limitations-on-automatic-attach-to-a-service"></a>Limitações de anexar automaticamente a um serviço  
 Anexar automaticamente a um serviço tem as seguintes limitações:  
  
-   O serviço deve fazer parte da solução do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] que você está depurando.  
  
-   O serviço deve ser hospedado. Ele pode fazer parte de um projeto do site (Sistema de Arquivos e HTTP), projeto de aplicativo Web (Sistema de Arquivos e HTTP) ou projeto da biblioteca de serviço WCF. Os projetos da biblioteca de serviço WCF podem ser bibliotecas de serviço ou bibliotecas de serviço de fluxo de trabalho.  
  
-   O serviço deve ser chamado de um cliente WCF.  
  
-   A depuração deve estar habilitada com o seguinte código no arquivo app.config ou no Web.config:  
  
    ```  
    <system.web>  
      <compilation debug="true" />  
    <system.web>  
    ```  
  
## <a name="self-hosting"></a>Auto-hospedagem  
 Um *serviço auto-hospedado* é um serviço WCF que não é executado dentro do IIS, o Host de serviço do WCF, ou o [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] servidor de desenvolvimento. Para obter informações sobre como depurar um serviço auto-hospedado, consulte [como: depurar um serviço WCF de auto-hospedada](../debugger/how-to-debug-a-self-hosted-wcf-service.md).  
  
## <a name="self-hosting"></a>Auto-hospedagem  
 Para habilitar a depuração de [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] aplicativos 3.0 ou 3.5, [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 3.0 ou 3.5 deve ser instalado antes de [!INCLUDE[vs_dev10_long](../code-quality/includes/vs_dev10_long_md.md)] está instalado. Se [!INCLUDE[vs_dev10_long](../code-quality/includes/vs_dev10_long_md.md)] está instalada antes de [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 3.0 ou 3.5, ocorrerá um erro quando você tentar depurar um [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] aplicativo 3.0 ou 3.5. A mensagem de erro é "Não é possível entrar automaticamente no servidor". Para corrigir esse problema, use o Windows **painel de controle** > **programas e recursos** para reparar o [!INCLUDE[vs_dev10_long](../code-quality/includes/vs_dev10_long_md.md)] instalação.  
  
## <a name="see-also"></a>Consulte também  
 [Depurando serviços WCF](../debugger/debugging-wcf-services.md)   
 [Como depurar um serviço WCF auto-hospedado](../debugger/how-to-debug-a-self-hosted-wcf-service.md)