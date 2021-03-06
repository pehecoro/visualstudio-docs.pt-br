---
title: "Passo a passo: Associação de dados simples em um projeto no nível de documento | Microsoft Docs"
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
- data binding [Office development in Visual Studio], worksheet cell to Database field
- worksheets [Office development in Visual Studio], binding worksheet cell to Database field
- Database field [Office development in Visual Studio]
- data [Office development in Visual Studio], binding data
- simple data binding [Office development in Visual Studio]
author: TerryGLee
ms.author: tglee
manager: ghogen
ms.workload: office
ms.openlocfilehash: 95029c946939bf0918e15034625ad31c1e5897b9
ms.sourcegitcommit: f9fbf1f55f9ac14e4e5c6ae58c30dc1800ca6cda
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/10/2018
---
# <a name="walkthrough-simple-data-binding-in-a-document-level-project"></a>Instruções passo a passo: associação de dados simples em um projeto no nível do documento
  Este passo a passo demonstra os conceitos básicos de associação de dados em um projeto no nível do documento. Um único campo de dados em um banco de dados do SQL Server está associado a um intervalo nomeado no Microsoft Office Excel. Passo a passo também mostra como adicionar controles que permitem que você percorra todos os registros na tabela.  
  
 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]  
  
 Esta explicação passo a passo ilustra as seguintes tarefas:  
  
-   Criando uma fonte de dados para um projeto do Excel.  
  
-   Adicionando controles a uma planilha.  
  
-   Percorrer os registros do banco de dados.  
  
 [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes para concluir esta instrução passo a passo:  
  
-   [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]  
  
-   [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] ou [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)].  
  
-   Acesso a um servidor com o banco de dados de exemplo Northwind SQL Server.  
  
-   Permissões de leitura e gravação no banco de dados do SQL Server.  
  
## <a name="creating-a-new-project"></a>Criando um novo projeto  
 Nesta etapa, você criará um projeto de pasta de trabalho do Excel.  
  
#### <a name="to-create-a-new-project"></a>Para criar um novo projeto  
  
1.  Criar um projeto de pasta de trabalho do Excel com o nome **associação de dados simples meu**, usando o Visual Basic ou c#. Verifique se **criar um novo documento** está selecionado. Para obter mais informações, consulte [como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).  
  
 Visual Studio abre a nova pasta de trabalho do Excel no designer e adiciona o **Meus associação de dados simples** projeto **Gerenciador de soluções**.  
  
## <a name="creating-the-data-source"></a>Criando a Fonte de Dados  
 Use o **fontes de dados** janela para adicionar um conjunto de dados tipado ao seu projeto.  
  
#### <a name="to-create-the-data-source"></a>Para criar a fonte de dados  
  
1.  Se o **fontes de dados** janela não estiver visível, exibir, na barra de menus, escolhendo **exibição**, **outras janelas**, **fontes de dados**.  
  
2.  Escolha **adicionar nova fonte de dados** para iniciar o **Assistente de configuração de fonte de dados**.  
  
3.  Selecione **banco de dados** e, em seguida, clique em **próximo**.  
  
4.  Selecione uma conexão de dados para o banco de dados do SQL Server de exemplo Northwind, ou adicionar uma nova conexão usando o **nova Conexão** botão.  
  
5.  Depois que uma conexão foi selecionado ou criado, clique em **próximo**.  
  
6.  Desmarque a opção para salvar a conexão se estiver selecionada e clique **próximo**.  
  
7.  Expanda o **tabelas** nó o **objetos de banco de dados** janela.  
  
8.  Marque a caixa de seleção ao lado de **clientes** tabela.  
  
9. Clique em **Finalizar**.  
  
 O assistente adiciona o **clientes** de tabela para o **fontes de dados** janela. Ele também adiciona um conjunto de dados tipado ao seu projeto que está visível no **Gerenciador de soluções**.  
  
## <a name="adding-controls-to-the-worksheet"></a>Adicionando controles a planilha  
 Para este passo a passo, você precisa de dois intervalos nomeados e quatro botões na primeira planilha. Primeiro, adicione os dois intervalos nomeados do **fontes de dados** janela para que eles são vinculados automaticamente a fonte de dados. Em seguida, adicione os botões do **caixa de ferramentas**.  
  
#### <a name="to-add-two-named-ranges"></a>Para adicionar dois intervalos nomeados  
  
1.  Verifique o **Meus Binding.xlsx de dados simples** pasta de trabalho é aberta no designer do Visual Studio, com **Planilha1** exibida.  
  
2.  Abra o **fontes de dados** janela e expanda o **clientes** nó.  
  
3.  Selecione o **CompanyName** coluna e, em seguida, clique na seta suspensa exibida.  
  
4.  Selecione **NamedRange** na lista suspensa e, em seguida, arraste o **CompanyName** coluna para uma célula **A1**.  
  
     Um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle chamado `companyNameNamedRange` é criado na célula **A1**. Ao mesmo tempo, uma <xref:System.Windows.Forms.BindingSource> chamado `customersBindingSource`, um adaptador de tabela e um <xref:System.Data.DataSet> instância são adicionados ao projeto. O controle está vinculado a <xref:System.Windows.Forms.BindingSource>, que por sua vez é associado a <xref:System.Data.DataSet> instância.  
  
5.  Selecione o **CustomerID** coluna o **fontes de dados** janela e, em seguida, clique na seta suspensa exibida.  
  
6.  Clique em **NamedRange** na lista suspensa e, em seguida, arraste o **CustomerID** coluna para uma célula **B1**.  
  
7.  Outro <xref:Microsoft.Office.Tools.Excel.NamedRange> controle chamado `customerIDNamedRange` é criado na célula **B1**e vinculado para o <xref:System.Windows.Forms.BindingSource>.  
  
#### <a name="to-add-four-buttons"></a>Para adicionar os quatro botões  
  
1.  Do **controles comuns** guia do **caixa de ferramentas**, adicione um <xref:System.Windows.Forms.Button> controle a célula **A3** da planilha.  
  
     Esse botão é denominado `Button1`.  
  
2.  Adicione três botões mais para as seguintes células nesta ordem, para que os nomes são conforme mostrado:  
  
    |Célula|(Nome)|  
    |----------|--------------|  
    |B3|Button2|  
    |C3|Button3|  
    |D3|Button4|  
  
 A próxima etapa é adicionar o texto para os botões e no c# adicionar manipuladores de eventos.  
  
## <a name="initializing-the-controls"></a>Inicializando os controles  
 Definir o texto do botão e adicionar manipuladores de eventos durante o <xref:Microsoft.Office.Tools.Excel.Worksheet.Startup> evento.  
  
#### <a name="to-initialize-the-controls"></a>Para inicializar os controles  
  
1.  Em **Solution Explorer**, clique com botão direito **Sheet1.vb** ou **Sheet1.cs**e, em seguida, clique em **Exibir código** no menu de atalho.  
  
2.  Adicione o seguinte código para o `Sheet1_Startup` método para definir o texto de cada botão.  
  
     [!code-csharp[Trin_VstcoreDataExcel#2](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs#2)]
     [!code-vb[Trin_VstcoreDataExcel#2](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb#2)]  
  
3.  C# somente, adicionar manipuladores de eventos para o botão, clique em eventos para o `Sheet1_Startup` método.  
  
     [!code-csharp[Trin_VstcoreDataExcel#3](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs#3)]  
  
 Agora adicione código para manipular o <xref:System.Windows.Forms.Control.Click> eventos dos botões para que o usuário pode navegar entre os registros.  
  
## <a name="adding-code-to-enable-scrolling-through-the-records"></a>Adicionar código para habilitar a rolagem por meio de registros  
 Adicione código para o <xref:System.Windows.Forms.Control.Click> manipulador de eventos de cada botão para percorrer os registros.  
  
#### <a name="to-move-to-the-first-record"></a>Para mover para o primeiro registro  
  
1.  Adicionar um manipulador de eventos para o <xref:System.Windows.Forms.Control.Click> evento o `Button1` botão e, em seguida, adicione o seguinte código para mover para o primeiro registro:  
  
     [!code-csharp[Trin_VstcoreDataExcel#4](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs#4)]
     [!code-vb[Trin_VstcoreDataExcel#4](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb#4)]  
  
#### <a name="to-move-to-the-previous-record"></a>Para mover para o registro anterior  
  
1.  Adicionar um manipulador de eventos para o <xref:System.Windows.Forms.Control.Click> evento o `Button2` botão e, em seguida, adicione o seguinte código para mover a posição de volta em um:  
  
     [!code-csharp[Trin_VstcoreDataExcel#5](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs#5)]
     [!code-vb[Trin_VstcoreDataExcel#5](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb#5)]  
  
#### <a name="to-move-to-the-next-record"></a>Para mover para o próximo registro  
  
1.  Adicionar um manipulador de eventos para o <xref:System.Windows.Forms.Control.Click> evento o `Button3` botão e, em seguida, adicione o seguinte código para Avançar a posição em um:  
  
     [!code-csharp[Trin_VstcoreDataExcel#6](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs#6)]
     [!code-vb[Trin_VstcoreDataExcel#6](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb#6)]  
  
#### <a name="to-move-to-the-last-record"></a>Para mover para o último registro  
  
1.  Adicionar um manipulador de eventos para o <xref:System.Windows.Forms.Control.Click> evento o `Button4` botão e, em seguida, adicione o seguinte código para mover para o último registro:  
  
     [!code-csharp[Trin_VstcoreDataExcel#7](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs#7)]
     [!code-vb[Trin_VstcoreDataExcel#7](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb#7)]  
  
## <a name="testing-the-application"></a>Testando o aplicativo  
 Agora você pode testar sua pasta de trabalho para certificar-se de que você pode navegar entre os registros no banco de dados.  
  
#### <a name="to-test-your-workbook"></a>Para testar a sua pasta de trabalho  
  
1.  Pressione F5 para executar o projeto.  
  
2.  Confirme se o primeiro registro é exibido nas células **A1** e **B1**.  
  
3.  Clique o  **>**  (`Button3`) botão e confirme se o próximo registro aparece na célula **A1** e **B1**.  
  
4.  Clique nos outros botões de rolagem para confirmar que o registro é alterado conforme o esperado.  
  
## <a name="next-steps"></a>Próximas etapas  
 Este passo a passo mostra os fundamentos da associação de um intervalo nomeado para um campo em um banco de dados. Estas são algumas tarefas que podem vir a seguir:  
  
-   Armazenar em cache os dados para que possa ser usado offline. Para obter mais informações, consulte [como: dados de Cache para uso Offline ou em um servidor](../vsto/how-to-cache-data-for-use-offline-or-on-a-server.md).  
  
-   Associe células em várias colunas em uma tabela, em vez de para um campo. Para obter mais informações, consulte [passo a passo: associação de dados complexos em um projeto no nível de documento](../vsto/walkthrough-complex-data-binding-in-a-document-level-project.md).  
  
-   Use um <xref:System.Windows.Forms.BindingNavigator> controle para percorrer os registros. Para obter mais informações, consulte [Como navegar em dados com o controle BindingNavigator dos Windows Forms](/dotnet/framework/winforms/controls/bindingnavigator-control-overview-windows-forms).  
  
## <a name="see-also"></a>Consulte também  
 [Associando dados a controles em soluções do Office](../vsto/binding-data-to-controls-in-office-solutions.md)   
 [Dados em soluções do Office](../vsto/data-in-office-solutions.md)   
 [Instruções passo a passo: vinculação de dados complexa em um projeto no nível do documento](../vsto/walkthrough-complex-data-binding-in-a-document-level-project.md)  
  
  