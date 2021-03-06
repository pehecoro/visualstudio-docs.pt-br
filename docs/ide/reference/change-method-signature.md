---
title: "Refatorar uma assinatura de método no Visual Studio | Microsoft Docs"
ms.custom: 
ms.date: 01/26/2018
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-general
ms.topic: reference
author: gewarren
ms.author: gewarren
manager: ghogen
f1_keywords:
- vs.csharp.refactoring.remove
- vs.csharp.refactoring.reorder
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 8358e14ccf9570207b3e52a552990fd2a3a80d49
ms.sourcegitcommit: 205d15f4558315e585c67f33d5335d5b41d0fcea
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="change-a-method-signature-refactoring"></a>Refatoração Alterar uma assinatura de método

Esta refatoração aplica-se a:

- C#

- Visual Basic

**O quê:** permite remover ou alterar a ordem dos parâmetros do método.

**Quando:** você deseja mover ou remover um parâmetro de método que está sendo usado em uma variedade de locais.

**Por quê:** você pode manualmente remover e reordenar os parâmetros e, em seguida, localizar todas as chamadas para esse método e alterá-las uma por uma, mas isso poderia levar a erros.  Essa ferramenta de refatoração executará a tarefa automaticamente.

## <a name="how-to"></a>Como fazer

1. realce ou coloque o cursor do texto dentro do nome do método para modificar, ou um de seus usos:

   - C#:

    ![Código em C# realçado](media/changesignature-highlight-cs.png)

   - VB:

    ![Código em Visual Basic realçado](media/changesignature-highlight-vb.png)

1. Depois, siga um destes procedimentos:

   - **Teclado**
     - Pressione **Ctrl+R**, em seguida, **Ctrl+V**.  (Observe que o atalho de teclado pode ser diferente com base no perfil selecionado.)
     - Pressione **Ctrl +.** para disparar o menu **Ações Rápidas e Refatorações** e selecionar **Alterar Assinatura** no pop-up da janela Visualização.
   - **Mouse**
     - Selecione **Editar > Refatorar > Remover Parâmetros**.
     - Selecione **Editar > Refatorar > Reordenar Parâmetros**.
     - Clique com o botão direito do mouse no código, selecione o menu **Ações Rápidas e Refatorações** e selecione **Alterar Assinatura** no pop-up da janela Visualização.

1. Na caixa de diálogo **Alterar Assinatura** que aparecer, você pode usar os botões à direita para alterar a assinatura do método:

   ![Caixa de diálogo Alterar Assinatura](media/changesignature-dialog-cs.png)

   | Botão | Descrição
   | ------ | ---
   | **Para cima/baixo** | Mova o parâmetro selecionado para cima e para baixo na lista
   | **Removerr**  | Remova o parâmetro selecionado da lista
   | **Restaurar** | Restaurar o parâmetro selecionado e riscado na lista

   > [!TIP]
   > Use a caixa de seleção **Visualizar alterações de referência** para [ver qual será o resultado](../../ide/preview-changes.md) antes de confirmar as alterações.

1. Quando tiver terminado, pressione o botão **OK** para fazer as alterações.

   - C#:

    ![Resultado da alteração de assinatura – C#](media/changesignature-result-cs.png)

   - Visual Basic:

    ![Resultado da alteração de assinatura – Visual Basic](media/changesignature-result-vb.png)

## <a name="see-also"></a>Consulte também

[Refatoração](../refactoring-in-visual-studio.md)  
[Visualizar alterações](../../ide/preview-changes.md)