---
title: 'Etapa 11: executar o programa e experimentar outros recursos | Microsoft Docs'
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-acquisition
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 656614d0-4fe7-4a67-8edc-c10919377d09
caps.latest.revision: "12"
author: TerryGLee
ms.author: tglee
manager: ghogen
ms.workload: multiple
ms.openlocfilehash: c53c542741cc64c0d60a94116acf7de4ff7f61ab
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="step-11-run-your-program-and-try-other-features"></a>Etapa 11: executar o programa e experimentar outros recursos
O programa é concluído e pronto para ser executado. Você pode executar o programa e definir a cor do plano de fundo de PictureBox. Para saber mais, tente melhorar o programa alterando a cor do formulário, personalizando os botões e a caixa de seleção, e modificando as propriedades do formulário.  
  
 Para baixar uma versão concluída do exemplo, consulte [Exemplo de tutorial completo do Visualizador de Imagens](http://code.msdn.microsoft.com/Complete-Picture-Viewer-7d91d3a8).  
  
 ![link para vídeo](../data-tools/media/playvideo.gif "PlayVideo")Para uma versão em vídeo deste tópico, consulte o [Tutorial 1: criar um Visualizador de Imagens no Visual Basic – Vídeo 5](http://go.microsoft.com/fwlink/?LinkId=205216) ou o [Tutorial 1: criar um Visualizador de Imagens em C# – Vídeo 5](http://go.microsoft.com/fwlink/?LinkId=205206). Esses vídeos usam uma versão anterior do Visual Studio, portanto, existem pequenas diferenças em alguns comandos de menu e em outros elementos da interface do usuário. No entanto, os conceitos e procedimentos funcionam de maneiras semelhantes na versão atual do Visual Studio.  
  
### <a name="to-run-your-program-and-set-the-background-color"></a>Para executar o programa e definir a cor do plano de fundo  
  
1.  Selecione F5 ou, na barra de menus, selecione **Depurar**, **Iniciar Depuração**.  
  
2.  Antes de abrir uma imagem, clique no botão **Definir a cor da tela de fundo**. A caixa de diálogo **Cor** é aberta.  
  
     ![Caixa de diálogo de cor](../ide/media/express_colordialog.png "Express_ColorDialog")  
Caixa de diálogo Cor  
  
3.  Escolha uma cor para definir a cor do plano de fundo de PictureBox. Examine cuidadosamente o método `backgroundButton_Click()` para compreender como ele funciona.  
  
    > [!NOTE]
    >  Você pode carregar uma imagem da Internet colando sua URL na caixa de diálogo **Abrir Arquivo**. Tente localizar uma imagem com um plano de fundo transparente, para que sua cor do plano de fundo seja exibida.  
  
4.  Escolha o botão **Limpar a imagem** para certificar-se de que ela desaparece. Em seguida, sai do programa escolhendo o botão **Fechar**.  
  
### <a name="to-try-other-features"></a>Para testar outros recursos  
  
-   Altere a cor do formulário e os botões usando a propriedade **BackColor**.  
  
-   Personalize seus botões e sua caixa de seleção usando as propriedades **Font** e **ForeColor**.  
  
-   Altere as propriedades **FormBorderStyle** e **ControlBox** do formulário.  
  
-   Use as propriedades **AcceptButton** e **CancelButton** do formulário de modo que os botões sejam escolhidos automaticamente quando o usuário escolher as teclas ENTER ou ESC. Faça o programa abrir a caixa de diálogo **Abrir Arquivo** quando o usuário escolher ENTER e fechar a caixa quando o usuário escolher ESC.  
  
### <a name="to-continue-or-review"></a>Para continuar ou revisar  
  
-   Para aprender sobre programação no Visual Studio, consulte [Conceitos de Programação](http://msdn.microsoft.com/Library/65c12cca-af4f-4017-886e-2dbc00a189d6).  
  
-   Para saber mais sobre o Visual Basic, consulte [Desenvolvendo aplicativos com o Visual Basic](/dotnet/visual-basic/developing-apps/index).  
  
-   Para saber mais sobre o Visual [Introdução à linguagem C# e ao .NET Framework](/dotnet/csharp/getting-started/introduction-to-the-csharp-language-and-the-net-framework).  
  
-   Para ir para o próximo tutorial, consulte [Tutorial 2: criar um teste de matemática temporizado](../ide/tutorial-2-create-a-timed-math-quiz.md).  
  
-   Para retornar à etapa anterior do tutorial, consulte [Etapa 10: escrever código para botões adicionais e uma caixa de seleção](../ide/step-10-write-code-for-additional-buttons-and-a-check-box.md).