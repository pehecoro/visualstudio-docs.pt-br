---
title: "Erro: Falha de autenticação Kerberos | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-debug
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: vs.debug.error.callback_kerberos_auth_failed
dev_langs:
- CSharp
- VB
- FSharp
- C++
ms.assetid: c18053f9-9074-4bc3-a8bf-13e4acbea921
caps.latest.revision: "7"
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 37dc0626a1f96d20aa7cf1cb4a3ca2d811d391b4
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2017
---
# <a name="error-kerberos-authentication-failed"></a>Erro: falha na autenticação Kerberos
Ao tentar fazer a depuração remota, você poderá receber a seguinte mensagem de erro:  
  
```  
Error: The Visual Studio Remote Debugger on the target computer cannot connect back to this computer. Kerberos authentication failed.  
```  
  
 Esse erro ocorre quando o Monitor de Depuração Remota do Visual Studio está sendo executado sob a conta Serviço de Rede ou Sistema Local. Em uma dessas contas, o depurador remoto deve estabelecer uma conexão de autenticação de Kerberos para se comunicar de volta com o computador host do depurador do Visual Studio.  
  
 A autenticação Kerberos não está disponível nestas condições:  
  
-   O computador de destino ou o computador host do depurador está em um grupo de trabalho, em vez de em um domínio  
  
     \- ou -  
  
-   Kerberos foi desabilitado no controlador de domínio.  
  
 Se a autenticação Kerberos não estiver disponível, alterar a conta usada para executar o Monitor de Depuração Remota do Visual Studio. Para o procedimento, consulte [erro: serviço de depurador remoto a do Visual Studio no computador de destino não pode se conectar novamente a esse computador](../debugger/error-the-visual-studio-remote-debugger-service-on-the-target-computer-cannot-connect-back-to-this-computer.md).  
  
 Se ambos os computadores estiverem conectados ao mesmo domínio e você ainda receber essa mensagem, verifique se o DNS no computador de destino está resolvendo corretamente o nome do computador host do depurador. Consulte o procedimento a seguir.  
  
### <a name="to-verify-that-dns-on-the-target-computer-is-correctly-resolving-the-debugger-host-computer-name"></a>Para verificar se o DNS no computador de destino está resolvendo corretamente o nome do computador host do depurador  
  
1.  No computador de destino, abra o **iniciar** , aponte para **Acessórios** e, em seguida, clique em **Prompt de comando**.  
  
2.  No **Prompt de comando** , digite:  
  
    ```  
    ping <debugger_host_computer_name>  
    ```  
  
3.  A primeira linha da resposta `ping` mostra o nome completo do computador e o endereço IP retornados pelo DNS para o computador especificado.  
  
4.  No computador de host do depurador, abra um **Prompt de comando** janela e execute `ipconfig`.  
  
5.  Compare os valores de endereço IP.  
  
## <a name="see-also"></a>Consulte também  
 [Erros de depuração remota e solução de problemas](../debugger/remote-debugging-errors-and-troubleshooting.md)   
 [Depuração remota](../debugger/remote-debugging.md)