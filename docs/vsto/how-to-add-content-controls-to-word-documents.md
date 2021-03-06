---
title: 'Como: adicionar controles Content a documentos do Word | Microsoft Docs'
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
- restricted permissions [Office development in Visual Studio]
- DropDownListContentControl, adding to documents
- BuildingBlockGalleryContentControl, adding to documents
- partial document protection [Office development in Visual Studio]
- RichTextContentControl, adding to documents
- Word [Office development in Visual Studio], partial document protection
- content controls [Office development in Visual Studio], protecting
- PictureContentControl, adding to documents
- GroupContentControl, adding to documents
- document protection [Office development in Visual Studio]
- PlainTextContentControl, adding to documents
- content controls [Office development in Visual Studio], adding
- ComboBoxContentControl, adding to documents
- DatePickerContentControl, adding to documents
- Word [Office development in Visual Studio], restricted permissions
author: TerryGLee
ms.author: tglee
manager: ghogen
ms.workload: office
ms.openlocfilehash: b1dd59fc777c012f92baaf96302f7cf031ad151c
ms.sourcegitcommit: f9fbf1f55f9ac14e4e5c6ae58c30dc1800ca6cda
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/10/2018
---
# <a name="how-to-add-content-controls-to-word-documents"></a>Como adicionar controles Content a documentos do Word
  Em projetos do Word em nível de documento, você pode adicionar controles de conteúdo para o documento em seu projeto em tempo de design ou em tempo de execução. Em projetos de suplemento do VSTO do Word, você pode adicionar controles de conteúdo para qualquer documento aberto em tempo de execução.  
  
 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]  
  
 Este tópico descreve as seguintes tarefas:  
  
-   [Adicionando controles de conteúdo em tempo de design](#designtime)  
  
-   [Adicionando controles de conteúdo em tempo de execução em um projeto no nível do documento](#runtimedoclevel)  
  
-   [Adicionando controles de conteúdo em tempo de execução em um projeto de suplemento do VSTO](#runtimeaddin)  
  
 Para obter informações sobre controles de conteúdo, consulte [controles Content](../vsto/content-controls.md).  
  
##  <a name="designtime"></a>Adicionando controles de conteúdo em tempo de Design  
 Há várias maneiras de adicionar controles de conteúdo para o documento em um projeto no nível do documento em tempo de design:  
  
-   Adicionar um controle de conteúdo do **controles Word** guia do **caixa de ferramentas**.  
  
-   Adicionar um controle de conteúdo para o documento da mesma forma você adicionaria um controle de conteúdo nativo no Word.  
  
-   Arraste um controle de conteúdo para o documento a partir de **fontes de dados** janela. Isso é útil quando você deseja associar o controle de dados quando o controle é criado. Para obter mais informações, consulte [como: preencher documentos com dados de objetos](../vsto/how-to-populate-documents-with-data-from-objects.md) e [como: preencher documentos com dados de um banco de dados](../vsto/how-to-populate-documents-with-data-from-a-database.md).  
  
 [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]  
  
#### <a name="to-add-a-content-control-to-a-document-by-using-the-toolbox"></a>Para adicionar um controle de conteúdo a um documento usando a caixa de ferramentas  
  
1.  O documento que está hospedada no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] designer, coloque o cursor onde você deseja adicionar o controle de conteúdo, ou selecione o texto que você deseja substituir o controle de conteúdo.  
  
2.  Abra o **caixa de ferramentas** e clique no **controles Word** guia.  
  
3.  Adicione o controle de uma das seguintes maneiras:  
  
    -   Clique duas vezes em um controle de conteúdo no **caixa de ferramentas**.  
  
         ou  
  
    -   Clique em um controle de conteúdo no **caixa de ferramentas** e, em seguida, pressione a tecla ENTER.  
  
         ou  
  
    -   Arraste um controle de conteúdo do **caixa de ferramentas** ao documento. O controle de conteúdo é adicionado na seleção atual do documento, não no local do ponteiro do mouse.  
  
> [!NOTE]  
>  Não é possível adicionar um <xref:Microsoft.Office.Tools.Word.GroupContentControl> usando o **caixa de ferramentas**. Você só pode adicionar um <xref:Microsoft.Office.Tools.Word.GroupContentControl> no Word, ou em tempo de execução.  
  
> [!NOTE]  
>  O Visual Studio não fornece um controle de conteúdo da caixa de seleção na caixa de ferramentas. Para adicionar um controle de conteúdo da caixa de seleção para o documento, você deve criar um <xref:Microsoft.Office.Tools.Word.ContentControl> objeto programaticamente. Para obter mais informações, consulte [controles de conteúdo](../vsto/content-controls.md).  
  
#### <a name="to-add-a-content-control-to-a-document-in-word"></a>Para adicionar um controle de conteúdo a um documento do Word  
  
1.  O documento que está hospedada no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] designer, coloque o cursor onde você deseja adicionar o controle de conteúdo, ou selecione o texto que você deseja substituir o controle de conteúdo.  
  
2.  Na faixa de opções, clique no **desenvolvedor** guia.  
  
    > [!NOTE]  
    >  Se o **desenvolvedor** guia não estiver visível, você deve primeiro mostrá-la. Para obter mais informações, consulte [como: Mostrar a guia Desenvolvedor na faixa de opções](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md).  
  
3.  No **controles** de grupo, clique no ícone para o controle de conteúdo que você deseja adicionar.  
  
##  <a name="runtimedoclevel"></a>Adicionando controles de conteúdo em tempo de execução em um projeto no nível do documento  
 Você pode adicionar controles de conteúdo por meio de programação para o documento em tempo de execução usando métodos do <xref:Microsoft.Office.Tools.Word.Document.Controls%2A> propriedade o `ThisDocument` classe em seu projeto. Cada método tem três sobrecargas que você pode usar para adicionar um controle de conteúdo das seguintes maneiras:  
  
-   Adicione um controle na seleção atual.  
  
-   Adicione um controle em um intervalo especificado.  
  
-   Adicione um controle baseado em um controle de conteúdo nativo no documento.  
  
 Criado dinamicamente conteúdo controles não são mantidos no documento quando o documento é fechado. No entanto, um controle de conteúdo nativo permanecerá no documento. Você pode recriar um controle de conteúdo baseado em um controle de conteúdo nativo na próxima vez em que o documento for aberto. Para obter mais informações, consulte [adicionando controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md).  
  
> [!NOTE]  
>  Para adicionar um controle de conteúdo da caixa de seleção para um documento em um projeto do Word 2010, você deve criar um <xref:Microsoft.Office.Tools.Word.ContentControl> objeto. Para obter mais informações, consulte [controles de conteúdo](../vsto/content-controls.md).  
  
#### <a name="to-add-a-content-control-at-the-current-selection"></a>Para adicionar um controle de conteúdo na seleção atual  
  
1.  Use um <xref:Microsoft.Office.Tools.Word.ControlCollection> método que tem o nome `Add` \< *classe de controle*> (onde *classe de controle* é o nome da classe do controle de conteúdo que você deseja adicionar como <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A>), e que tem um único parâmetro para o nome do novo controle.  
  
     O seguinte exemplo de código usa o <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A> método para adicionar um novo <xref:Microsoft.Office.Tools.Word.RichTextContentControl> para o início do documento. Para executar esse código, adicione o código para o `ThisDocument` classe em seu projeto e chame o `AddRichTextControlAtSelection` método do `ThisDocument_Startup` manipulador de eventos.  
  
     [!code-csharp[Trin_ContentControlReference#700](../vsto/codesnippet/CSharp/trin_wordcontentcontrolreference/RichText.cs#700)]
     [!code-vb[Trin_ContentControlReference#700](../vsto/codesnippet/VisualBasic/trin_contentcontrolreference/RichText.vb#700)]  
  
#### <a name="to-add-a-content-control-at-a-specified-range"></a>Para adicionar um controle de conteúdo em um intervalo especificado  
  
1.  Use um <xref:Microsoft.Office.Tools.Word.ControlCollection> método que tem o nome `Add` \< *classe de controle*> (onde *classe de controle* é o nome da classe de controle de conteúdo que você deseja adicionar como <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A>), e que tem um <xref:Microsoft.Office.Interop.Word.Range> parâmetro.  
  
     O seguinte exemplo de código usa o <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A> método para adicionar um novo <xref:Microsoft.Office.Tools.Word.RichTextContentControl> para o início do documento. Para executar esse código, adicione o código para o `ThisDocument` classe em seu projeto e chame o `AddRichTextControlAtRange` método do `ThisDocument_Startup` manipulador de eventos.  
  
     [!code-csharp[Trin_ContentControlReference#701](../vsto/codesnippet/CSharp/trin_wordcontentcontrolreference/RichText.cs#701)]
     [!code-vb[Trin_ContentControlReference#701](../vsto/codesnippet/VisualBasic/trin_contentcontrolreference/RichText.vb#701)]  
  
#### <a name="to-add-a-content-control-that-is-based-on-a-native-content-control"></a>Para adicionar um controle de conteúdo com base em um controle de conteúdo nativo  
  
1.  Use um <xref:Microsoft.Office.Tools.Word.ControlCollection> método que tem o nome `Add` \< *classe de controle*> (onde *classe de controle* é o nome da classe de controle de conteúdo que você deseja adicionar como <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A>), e que tem um parâmetro de Microsoft.Office.Interop.Word.ContentControl.  
  
     O seguinte exemplo de código usa o <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A> método para criar um novo <xref:Microsoft.Office.Tools.Word.RichTextContentControl> para cada controle RTF nativo no documento. Para executar esse código, adicione o código para o `ThisDocument` classe em seu projeto e chame o `CreateRichTextControlsFromNativeControls` método do `ThisDocument_Startup` manipulador de eventos.  
  
     [!code-csharp[Trin_ContentControlReference#702](../vsto/codesnippet/CSharp/trin_wordcontentcontrolreference/RichText.cs#702)]
     [!code-vb[Trin_ContentControlReference#702](../vsto/codesnippet/VisualBasic/trin_contentcontrolreference/RichText.vb#702)]  
  
##  <a name="runtimeaddin"></a>Adicionando controles de conteúdo em tempo de execução em um projeto de suplemento do VSTO  
 Você pode adicionar controles de conteúdo por meio de programação para qualquer documento aberto em tempo de execução usando um suplemento do VSTO. Para fazer isso, gerar um <xref:Microsoft.Office.Tools.Word.Document> hospedar o item com base em um documento aberto e usar os métodos do <xref:Microsoft.Office.Tools.Word.Document.Controls%2A> propriedade deste item de host. Cada método tem três sobrecargas que você pode usar para adicionar um controle de conteúdo das seguintes maneiras:  
  
-   Adicione um controle na seleção atual.  
  
-   Adicione um controle em um intervalo especificado.  
  
-   Adicione um controle baseado em um controle de conteúdo nativo no documento.  
  
 Criado dinamicamente conteúdo controles não são mantidos no documento quando o documento é fechado. No entanto, um controle de conteúdo nativo permanecerá no documento. Você pode recriar um controle de conteúdo baseado em um controle de conteúdo nativo na próxima vez em que o documento for aberto. Para obter mais informações, consulte [persistência de controles dinâmicos em documentos do Office](../vsto/persisting-dynamic-controls-in-office-documents.md).  
  
 Para obter mais informações sobre como gerar itens de host em projetos de suplemento do VSTO, consulte [Estendendo documentos do Word e pastas de trabalho do Excel no suplemento do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md).  
  
> [!NOTE]  
>  Para adicionar um controle de conteúdo da caixa de seleção para um documento, você deve criar um <xref:Microsoft.Office.Tools.Word.ContentControl> objeto. Para obter mais informações, consulte [controles de conteúdo](../vsto/content-controls.md).  
  
#### <a name="to-add-a-content-control-at-the-current-selection"></a>Para adicionar um controle de conteúdo na seleção atual  
  
1.  Use um <xref:Microsoft.Office.Tools.Word.ControlCollection> método que tem o nome `Add` \< *classe de controle*> (onde *classe de controle* é o nome da classe do controle de conteúdo que você deseja adicionar como <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A>), e que tem um único parâmetro para o nome do novo controle.  
  
     O seguinte exemplo de código usa o <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A> método para adicionar um novo <xref:Microsoft.Office.Tools.Word.RichTextContentControl> para o início do documento ativo. Para executar esse código, adicione o código para o `ThisAddIn` classe em seu projeto e chame o `AddRichTextControlAtSelection` método do `ThisAddIn_Startup` manipulador de eventos.  
  
     [!code-vb[Trin_WordAddInDynamicControls#1](../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb#1)]
     [!code-csharp[Trin_WordAddInDynamicControls#1](../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs#1)]  
  
#### <a name="to-add-a-content-control-at-a-specified-range"></a>Para adicionar um controle de conteúdo em um intervalo especificado  
  
1.  Use um <xref:Microsoft.Office.Tools.Word.ControlCollection> método que tem o nome `Add` \< *classe de controle*> (onde *classe de controle* é o nome da classe de controle de conteúdo que você deseja adicionar como <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A>), e que tem um <xref:Microsoft.Office.Interop.Word.Range> parâmetro.  
  
     O seguinte exemplo de código usa o <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A> método para adicionar um novo <xref:Microsoft.Office.Tools.Word.RichTextContentControl> para o início do documento ativo. Para executar esse código, adicione o código para o `ThisAddIn` classe em seu projeto e chame o `AddRichTextControlAtRange` método do `ThisAddIn_Startup` manipulador de eventos.  
  
     [!code-vb[Trin_WordAddInDynamicControls#2](../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb#2)]
     [!code-csharp[Trin_WordAddInDynamicControls#2](../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs#2)]  
  
#### <a name="to-add-a-content-control-that-is-based-on-a-native-content-control"></a>Para adicionar um controle de conteúdo com base em um controle de conteúdo nativo  
  
1.  Use um <xref:Microsoft.Office.Tools.Word.ControlCollection> método que tem o nome `Add` \< *classe de controle*> (onde *classe de controle* é o nome da classe de controle de conteúdo que você deseja adicionar como <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A>), e que tem um parâmetro de Microsoft.Office.Interop.Word.ContentControl.  
  
     O seguinte exemplo de código usa o <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A> método para criar um novo <xref:Microsoft.Office.Tools.Word.RichTextContentControl> para cada controle RTF nativo que está em um documento, depois que o documento é aberto. Para executar esse código, adicione o código para o `ThisAddIn` classe em seu projeto.  
  
     [!code-vb[Trin_WordAddInDynamicControls#3](../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb#3)]
     [!code-csharp[Trin_WordAddInDynamicControls#3](../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs#3)]  
  
     Para c#, você também deve anexar o `Application_DocumentOpen` manipulador de eventos para o <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentOpen> evento.  
  
     [!code-csharp[Trin_WordAddInDynamicControls#6](../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs#6)]  
  
## <a name="see-also"></a>Consulte também  
 [Automatizando o Word usando objetos estendidos](../vsto/automating-word-by-using-extended-objects.md)   
 [Itens de host e visão geral dos controles de Host](../vsto/host-items-and-host-controls-overview.md)   
 [Adicionando controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md)   
 [Limitações programáticas de itens de Host e controles de Host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)   
 [Suplementos de programação para o VSTO](../vsto/programming-vsto-add-ins.md)   
 [Programando personalizações no nível do documento](../vsto/programming-document-level-customizations.md)  
  