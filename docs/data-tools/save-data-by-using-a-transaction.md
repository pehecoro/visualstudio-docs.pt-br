---
title: "Como: salvar dados usando uma transação | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- saving data, using transactions
- System.Transactions namespace
- transactions, saving data
- data [Visual Studio], saving
ms.assetid: 8b835e8f-34a3-413d-9bb5-ebaeb87f1198
caps.latest.revision: "13"
author: gewarren
ms.author: gewarren
manager: ghogen
ms.technology: vs-data-tools
ms.workload: data-storage
ms.openlocfilehash: 9f2373e3a851899d139360caf0f6bb8b6ab0efa5
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-save-data-by-using-a-transaction"></a>Como: salvar dados usando uma transação
Salvar dados em uma transação usando o <xref:System.Transactions> namespace. Use o <xref:System.Transactions.TransactionScope> objeto participe de uma transação que é gerenciada automaticamente para você.  
  
Projetos não são criados com uma referência ao assembly System. Transactions, portanto você precisa adicionar manualmente uma referência para projetos que usam transações.  
  
A maneira mais fácil para implementar uma transação é criar uma instância de um <xref:System.Transactions.TransactionScope> do objeto em um `using` instrução. (Para obter mais informações, consulte [instrução Using](/dotnet/visual-basic/language-reference/statements/using-statement), e [usando a instrução](/dotnet/csharp/language-reference/keywords/using-statement).) O código que é executado dentro do `using` participa da transação.  
  
Para confirmar a transação, chame o <xref:System.Transactions.TransactionScope.Complete%2A> bloquear o método como a última instrução em uso.  
  
Para reverter a transação, lançar uma exceção antes de chamar o <xref:System.Transactions.TransactionScope.Complete%2A> método.  
  
## <a name="to-add-a-reference-to-the-systemtransactionsdll"></a>Para adicionar uma referência para o System.Transactions.dll  
  
1.  Sobre o **projeto** menu, selecione **adicionar referência**.  
  
2.  Sobre o **.NET** guia (**do SQL Server** guia para projetos do SQL Server), selecione **System. Transactions**e, em seguida, selecione **Okey**.  
  
     Uma referência para System.Transactions.dll é adicionada ao projeto.  
  
## <a name="to-save-data-in-a-transaction"></a>Para salvar dados em uma transação  
  
-   Adicione código para salvar dados em uso instrução que contém a transação. O código a seguir mostra como criar e instanciar uma <xref:System.Transactions.TransactionScope> objeto no uso de uma instrução:  
  
     [!code-vb[VbRaddataSaving#11](../data-tools/codesnippet/VisualBasic/save-data-by-using-a-transaction_1.vb)]
     [!code-csharp[VbRaddataSaving#11](../data-tools/codesnippet/CSharp/save-data-by-using-a-transaction_1.cs)]  
  
## <a name="see-also"></a>Consulte também
[Salvar dados de volta no banco de dados](../data-tools/save-data-back-to-the-database.md)  
[Passo a passo: salvar dados em uma transação](../data-tools/save-data-in-a-transaction.md)  