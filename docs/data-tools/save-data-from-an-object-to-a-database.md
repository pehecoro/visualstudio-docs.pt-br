---
title: Salvar dados de um objeto em um banco de dados | Microsoft Docs
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
- data [Visual Studio], saving
- data access [Visual Studio], objects
- saving data
ms.assetid: efd6135a-40cf-4b0d-8f8b-41a5aaea7057
caps.latest.revision: "9"
author: gewarren
ms.author: gewarren
manager: ghogen
ms.technology: vs-data-tools
ms.workload: data-storage
ms.openlocfilehash: e7078e6814abeb0db2afd2cffe698f923e530179
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="save-data-from-an-object-to-a-database"></a>Salvar dados de um objeto em um banco de dados
Você pode salvar os dados em objetos de um banco de dados, passando os valores de seu objeto para um dos métodos DBDirect do TableAdapter (por exemplo, `TableAdapter.Insert`). Para obter mais informações, consulte [TableAdapter](../data-tools/create-and-configure-tableadapters.md).  
  
 Para salvar dados de uma coleção de objetos, percorrer a coleção de objetos (por exemplo, um loop para Avançar) e enviar os valores para cada objeto no banco de dados usando um dos métodos DBDirect do TableAdapter.  
  
 Por padrão, os métodos DBDirect são criados em um TableAdapter que pode ser executado diretamente no banco de dados. Esses métodos podem ser chamados diretamente e não requerem <xref:System.Data.DataSet> ou <xref:System.Data.DataTable> objetos para reconciliar as alterações para enviar atualizações para um banco de dados.  
  
> [!NOTE]
>  Quando você estiver configurando um TableAdapter, a consulta principal deve fornecer informações suficientes para os métodos DBDirect a ser criado. Por exemplo, se um TableAdapter está configurado para consultar dados de uma tabela que não tem uma coluna de chave primária definida, ela não gera métodos DBDirect.  
  
|Método TableAdapter DBDirect|Descrição|  
|----------------------------------|-----------------|  
|`TableAdapter.Insert`|Adiciona novos registros de um banco de dados e permite que você transmitir valores de coluna individual como parâmetros de método.|  
|`TableAdapter.Update`|Atualizações de registros existentes em um banco de dados. O `Update` método usa valores da coluna original e novo como parâmetros de método. Os valores originais são usados para localizar o registro original e os novos valores são usados para atualizar esse registro.<br /><br /> O `TableAdapter.Update` método também é usado para acomodar as alterações em um conjunto de dados no banco de dados fazendo uma <xref:System.Data.DataSet>, <xref:System.Data.DataTable>, <xref:System.Data.DataRow>, ou uma matriz de <xref:System.Data.DataRow>s como parâmetros de método.|  
|`TableAdapter.Delete`|Exclui registros existentes do banco de dados com base em valores da coluna original passados como parâmetros de método.|  
  
### <a name="to-save-new-records-from-an-object-to-a-database"></a>Para salvar novos registros de um objeto em um banco de dados  
  
-   Criar os registros, passando os valores para o `TableAdapter.Insert` método.  
  
     O exemplo a seguir cria um novo registro de cliente no `Customers` tabela passando os valores a `currentCustomer` do objeto para o `TableAdapter.Insert` método.  
  
     [!code-csharp[VbRaddataSaving#23](../data-tools/codesnippet/CSharp/save-data-from-an-object-to-a-database_1.cs)]
     [!code-vb[VbRaddataSaving#23](../data-tools/codesnippet/VisualBasic/save-data-from-an-object-to-a-database_1.vb)]  
  
### <a name="to-update-existing-records-from-an-object-to-a-database"></a>Para atualizar registros existentes de um objeto para um banco de dados  
  
-   Modificar os registros chamando o `TableAdapter.Update` método, passando os novos valores para atualizar o registro e passando os valores originais para localizar o registro.  
  
    > [!NOTE]
    >  O objeto precisa manter os valores originais para passá-los para o `Update` método. Este exemplo usa as propriedades com um `orig` prefixo para armazenar os valores originais.  
  
     O exemplo a seguir atualiza um registro existente no `Customers` tabela passando os valores novos e originais no `Customer` o objeto para o `TableAdapter.Update` método.  
  
     [!code-csharp[VbRaddataSaving#24](../data-tools/codesnippet/CSharp/save-data-from-an-object-to-a-database_2.cs)]
     [!code-vb[VbRaddataSaving#24](../data-tools/codesnippet/VisualBasic/save-data-from-an-object-to-a-database_2.vb)]  
  
### <a name="to-delete-existing-records-from-a-database"></a>Para excluir registros existentes de um banco de dados  
  
-   Exclua os registros chamando o `TableAdapter.Delete` método e passar os valores originais para localizar o registro.  
  
    > [!NOTE]
    >  O objeto precisa manter os valores originais para passá-los para o `Delete` método. Este exemplo usa as propriedades com um `orig` prefixo para armazenar os valores originais.  
  
     O exemplo a seguir exclui um registro da `Customers` tabela passando os valores originais no `Customer` o objeto para o `TableAdapter.Delete` método.  
  
     [!code-csharp[VbRaddataSaving#25](../data-tools/codesnippet/CSharp/save-data-from-an-object-to-a-database_3.cs)]
     [!code-vb[VbRaddataSaving#25](../data-tools/codesnippet/VisualBasic/save-data-from-an-object-to-a-database_3.vb)]  
  
## <a name="net-framework-security"></a>Segurança do .NET Framework  
 Você deve ter permissão para executar a inserção selecionada, UPDATE ou DELETE na tabela no banco de dados.  
  
## <a name="see-also"></a>Consulte também  
 [Salvar dados de volta no banco de dados](../data-tools/save-data-back-to-the-database.md)