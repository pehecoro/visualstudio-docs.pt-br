---
title: "Substituir uma variável temporária pelo seu valor no Visual Studio | Microsoft Docs"
ms.custom: 
ms.date: 01/26/2018
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-general
ms.topic: reference
author: gewarren
ms.author: gewarren
manager: ghogen
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: b66236847e597aeddb4e6f09c27e64e717fdb7d9
ms.sourcegitcommit: 205d15f4558315e585c67f33d5335d5b41d0fcea
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="inline-a-temporary-variable-refactoring"></a>Refatoração Embutir uma variável temporária

Esta refatoração aplica-se a:

- C#

- Visual Basic

**O quê:** permite que você remova uma variável temporária e substitua-a pelo seu valor.

**Quando:** o uso da variável temporária dificulta o entendimento do código.

**Por quê:** remover uma variável temporária pode facilitar a leitura do código.

## <a name="how-to"></a>Como fazer

1. realce ou coloque o cursor do texto dentro de uma variável temporária para ser embutida:

   - C#:

    ![Código realçado – C#](media/inline-highlight-cs.png)

   - Visual Basic:

    ![Código realçado – Visual Basic](media/inline-highlight-vb.png)

1. Depois, siga um destes procedimentos:

   - **Teclado**
     - Pressione **Ctrl +.** para acionar o menu **Ações e Refatorações Rápidas**.
   - **Mouse**
     - Clique com o botão direito do mouse no código e selecione o menu **Ações e Refatorações Rápidas**.

1. Selecione **Variável temporária embutida** no pop-up da janela Visualização.

   A variável é removida e seus usos são substituídos pelo valor da variável.

   - C#:

    ![Resultado embutido – C#](media/inline-result-cs.png)

   - Visual Basic:

    ![Resultado embutido – Visual Basic](media/inline-result-vb.png)

## <a name="see-also"></a>Consulte também

[Refatoração](../refactoring-in-visual-studio.md)