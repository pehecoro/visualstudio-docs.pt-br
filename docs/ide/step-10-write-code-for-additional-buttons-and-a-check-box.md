---
title: "Etapa 10: escrever código para botões adicionais e uma caixa de seleção | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-acquisition
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 185cf370-ab39-4ac0-b6bc-601d5b95a4a2
caps.latest.revision: "21"
author: TerryGLee
ms.author: tglee
manager: ghogen
ms.workload: multiple
ms.openlocfilehash: 1196d229f69d1ffbfaae2c891ca03d1a58aedfdd
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="step-10-write-code-for-additional-buttons-and-a-check-box"></a>Etapa 10: Escrever código para botões adicionais e uma caixa de seleção
Agora você está pronto para concluir os outros quatro métodos. Você pode copiar e colar esse código, mas se deseja saber a maioria deste tutorial, digite o código e use o IntelliSense.  
  
 Este código adiciona funcionalidades aos botões que você adicionou anteriormente. Sem esse código, os botões não fazem nada. Os botões usam o código em seus eventos de `Click` (e na caixa de seleção usa o evento de `CheckChanged`) para fazer coisas diferentes quando você ativa os controles. Por exemplo, o evento `clearButton_Click`, que é ativado quando você escolhe o botão **Limpar a imagem**, apaga a imagem atual configurando sua propriedade `Image` como `null` (ou `nothing`). Cada evento no código inclui comentários que explicam o que o código faz.  
  
 ![link para vídeo](../data-tools/media/playvideo.gif "PlayVideo")Para uma versão em vídeo deste tópico, consulte o [Tutorial 1: criar um Visualizador de Imagens no Visual Basic – Vídeo 5](http://go.microsoft.com/fwlink/?LinkId=205216) ou o [Tutorial 1: criar um Visualizador de Imagens em C# – Vídeo 5](http://go.microsoft.com/fwlink/?LinkId=205206). Esses vídeos usam uma versão anterior do Visual Studio, portanto, existem pequenas diferenças em alguns comandos de menu e em outros elementos da interface do usuário. No entanto, os conceitos e procedimentos funcionam de maneiras semelhantes na versão atual do Visual Studio.  
  
> [!NOTE]
>  Como prática recomendada: Comente sempre o seu código. Os comentários são informações para uma pessoa ler e vale a pena tornar seu código mais legível. Todo em uma linha de comentário será ignorado pelo programa. No Visual C#, você comenta uma linha digitando duas barras no início (//) e no Visual Basic, você comenta uma linha iniciando-a com aspas simples (').  
  
### <a name="to-write-code-for-additional-buttons-and-a-check-box"></a>Para escrever códigos para botões adicionais e uma caixa de seleção  
  
-   Adicione o seguinte código ao seu arquivo de código Form1 (Form1.cs ou Form1.vb). Escolha a guia **VB** para exibir o código do Visual Basic.  
  
     [!code-vb[VbExpressTutorial1Step9_10#2](../ide/codesnippet/VisualBasic/step-10-write-code-for-additional-buttons-and-a-check-box_1.vb)]
     [!code-csharp[VbExpressTutorial1Step9_10#2](../ide/codesnippet/CSharp/step-10-write-code-for-additional-buttons-and-a-check-box_1.cs)]  
  
### <a name="to-continue-or-review"></a>Para continuar ou revisar  
  
-   Para ir para a próxima etapa do tutorial, consulte [Etapa 11: executar o programa e experimentar outros recursos](../ide/step-11-run-your-program-and-try-other-features.md).  
  
-   Para retornar à etapa anterior do tutorial, consulte [Etapa 9: examinar, comentar e testar o código](../ide/step-9-review-comment-and-test-your-code.md).