---
title: "Visão geral do modelo de objeto do Word | Microsoft Docs"
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
- Word object model
- Word [Office development in Visual Studio], object model
- object models [Office development in Visual Studio], Office
- object models [Office development in Visual Studio], Word
- objects [Office development in Visual Studio], Office object models
- Office object models
author: TerryGLee
ms.author: tglee
manager: ghogen
ms.workload: office
ms.openlocfilehash: a6f9163543272d784b0f8347acf275f74023ccf8
ms.sourcegitcommit: f9fbf1f55f9ac14e4e5c6ae58c30dc1800ca6cda
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/10/2018
---
# <a name="word-object-model-overview"></a>Visão geral do modelo de objeto do Word
  Ao desenvolver soluções do Word no Visual Studio, você interage com o modelo de objeto do Word. Esse modelo de objeto consiste em classes e interfaces que são fornecidos no assembly de interoperabilidade primário para o Word e são definidos no <xref:Microsoft.Office.Interop.Word> namespace.  
  
 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]  
  
 Este tópico fornece uma visão geral sobre o modelo de objeto do Word. Para obter recursos onde você pode aprender mais sobre todo o modelo de objeto do Word, consulte [usando a documentação de modelo de objeto do Word](#WordOMDocumentation).  
  
 Para obter informações sobre como usar o modelo de objeto do Word para realizar tarefas específicas, consulte os tópicos a seguir:  
  
-   [Trabalhando com documentos](../vsto/working-with-documents.md)  
  
-   [Trabalhando com texto em documentos](../vsto/working-with-text-in-documents.md)  
  
-   [Trabalhando com tabelas](../vsto/working-with-tables.md)  
  
##  <a name="understanding"></a>Noções básicas sobre o modelo de objeto do Word  
 O Word fornece centenas de objetos com o qual você pode interagir. Esses objetos são organizados em uma hierarquia que segue rigorosamente a interface do usuário. Na parte superior da hierarquia é o <xref:Microsoft.Office.Interop.Word.Application> objeto. Esse objeto representa a instância atual do Word. O <xref:Microsoft.Office.Interop.Word.Application> objeto contém o <xref:Microsoft.Office.Interop.Word.Document>, <xref:Microsoft.Office.Interop.Word.Selection>, <xref:Microsoft.Office.Interop.Word.Bookmark>, e <xref:Microsoft.Office.Interop.Word.Range> objetos. Cada um desses objetos tem vários métodos e propriedades que você pode acessar para manipular e interagir com o objeto.  
  
 A ilustração a seguir mostra uma exibição desses objetos na hierarquia de modelo de objeto do Word.  
  
 ![Gráfico de modelo de objeto do Word](../vsto/media/wrwordobjectmodel.gif "gráfico do modelo de objeto do Word")  
  
 A princípio, os objetos aparecem se sobreponham. Por exemplo, o <xref:Microsoft.Office.Interop.Word.Document> e <xref:Microsoft.Office.Interop.Word.Selection> objetos são os dois membros do <xref:Microsoft.Office.Interop.Word.Application> objeto, mas o <xref:Microsoft.Office.Interop.Word.Document> objeto também é um membro do <xref:Microsoft.Office.Interop.Word.Selection> objeto. Tanto o <xref:Microsoft.Office.Interop.Word.Document> e <xref:Microsoft.Office.Interop.Word.Selection> objetos contêm <xref:Microsoft.Office.Interop.Word.Bookmark> e <xref:Microsoft.Office.Interop.Word.Range> objetos. A sobreposição existe porque há várias maneiras que você pode acessar o mesmo tipo de objeto. Por exemplo, aplicar formatação a uma <xref:Microsoft.Office.Interop.Word.Range> objeto; mas você talvez queira acessar o intervalo da seleção atual, de um parágrafo específico, de uma seção ou de todo o documento.  
  
 As seções a seguir descrevem brevemente os objetos de nível superior e como eles interagem entre si. Esses objetos incluem os seguintes cinco:  
  
-   Objeto de aplicativo  
  
-   Objeto de documento  
  
-   Objeto de seleção  
  
-   Objeto de intervalo  
  
-   Objeto de indicador  
  
 O modelo de objeto do Word, além de projetos do Office no Visual Studio fornecem *itens de host* e *hospedar controles* que estende alguns objetos no modelo de objeto do Word. Itens de host e controles de host se comportam como os objetos de palavra, eles estendem, mas eles também têm funcionalidade adicional, como recursos de associação de dados e eventos extras. Para obter mais informações, consulte [automatizando o Word usando objetos estendidos](../vsto/automating-word-by-using-extended-objects.md) e [itens de Host e visão geral dos controles de Host](../vsto/host-items-and-host-controls-overview.md).  
  
### <a name="application-object"></a>Objeto de aplicativo  
 O <xref:Microsoft.Office.Interop.Word.Application> objeto representa o aplicativo Word e é o pai de todos os outros objetos. Seus membros geralmente se aplicam a palavra como um todo. Você pode usar suas propriedades e métodos para controlar o ambiente do Word.  
  
 Em projetos de suplemento do VSTO, você pode acessar o <xref:Microsoft.Office.Interop.Word.Application> objeto usando o `Application` campo o `ThisAddIn` classe. Para obter mais informações, consulte [Programando suplementos do VSTO](../vsto/programming-vsto-add-ins.md).  
  
 Em projetos de nível de documento, você pode acessar o <xref:Microsoft.Office.Interop.Word.Application> objeto usando o <xref:Microsoft.Office.Tools.Word.Document.Application%2A> propriedade o `ThisDocument` classe.  
  
### <a name="document-object"></a>Objeto de documento  
 O <xref:Microsoft.Office.Interop.Word.Document> objeto é central para programação do Word. Representa um documento e todo seu conteúdo. Quando você abre um documento ou cria um novo documento, você cria um novo <xref:Microsoft.Office.Interop.Word.Document> objeto, que é adicionado para o <xref:Microsoft.Office.Interop.Word.Documents> coleção do <xref:Microsoft.Office.Interop.Word.Application> objeto. O documento que tem o foco é chamado o documento ativo. Ele é representado pelo <xref:Microsoft.Office.Interop.Word._Application.ActiveDocument%2A> propriedade o <xref:Microsoft.Office.Interop.Word.Application> objeto.  
  
 As ferramentas de desenvolvimento do Office no Visual Studio estendem o <xref:Microsoft.Office.Interop.Word.Document> objeto fornecendo o <xref:Microsoft.Office.Tools.Word.Document> tipo. Esse tipo é um *item de host* que fornece acesso a todos os recursos de um <xref:Microsoft.Office.Interop.Word.Document> e o adiciona eventos adicionais e a capacidade de adicionar controles gerenciados.  
  
 Quando você cria um projeto no nível do documento, você pode acessar <xref:Microsoft.Office.Tools.Word.Document> membros usando o gerado `ThisDocument` classe em seu projeto. Você pode acessar membros do <xref:Microsoft.Office.Tools.Word.Document> item de host usando o **Me** ou **isso** palavras-chave no código a `ThisDocument` classe ou usando `Globals.ThisDocument` do código fora o `ThisDocument` classe. Para obter mais informações, consulte [personalizações de programação de nível de documento](../vsto/programming-document-level-customizations.md). Por exemplo, para selecionar o primeiro parágrafo no documento, use o código a seguir.  
  
 [!code-vb[Trin_VstcoreWordAutomation#120](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#120)]
 [!code-csharp[Trin_VstcoreWordAutomation#120](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#120)]  
  
 Em projetos de suplemento do VSTO, você pode gerar <xref:Microsoft.Office.Tools.Word.Document> itens de host em tempo de execução. Você pode usar o item de host gerado para adicionar controles para o documento associado. Para obter mais informações, consulte [Estendendo documentos do Word e pastas de trabalho do Excel no suplemento do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md).  
  
### <a name="selection-object"></a>Objeto de seleção  
 O <xref:Microsoft.Office.Interop.Word.Selection> objeto representa a área selecionada no momento. Quando você executar uma operação na interface do usuário de palavra, como texto em negrito, selecione, ou realce o texto e, em seguida, aplique a formatação. O <xref:Microsoft.Office.Interop.Word.Selection> objeto está sempre presente em um documento. Se nada estiver selecionado, ele representa o ponto de inserção. Além disso, uma seleção pode abranger vários blocos de texto que não são contíguos.  
  
### <a name="range-object"></a>Objeto de intervalo  
 O <xref:Microsoft.Office.Interop.Word.Range> objeto representa uma área contígua em um documento e é definido por uma posição de caractere inicial e uma posição de caractere final. Você não está limitado a um único <xref:Microsoft.Office.Interop.Word.Range> objeto. Você pode definir vários <xref:Microsoft.Office.Interop.Word.Range> objetos no mesmo documento. Um <xref:Microsoft.Office.Interop.Word.Range> objeto tem as seguintes características:  
  
-   Ele pode consistir de apenas o ponto de inserção, um intervalo de texto ou o documento inteiro.  
  
-   Ele inclui caracteres não imprimíveis como espaços, caracteres de tabulação e marcas de parágrafo.  
  
-   É a área representada pela seleção atual ou pode representar uma área diferente da seleção atual.  
  
-   Não é visível em um documento, ao contrário de uma seleção, que está sempre visível.  
  
-   Ele não será salvo com um documento e existe somente enquanto o código está sendo executado.  
  
 Quando você insere texto no final de um intervalo, o Word expande o intervalo para incluir o texto inserido automaticamente.  
  
### <a name="content-control-objects"></a>Objetos de controle de conteúdo  
 A <xref:Microsoft.Office.Interop.Word.ContentControl> fornece uma maneira de controlar a entrada e a apresentação de texto e outros tipos de conteúdo de documentos do Word. Um <xref:Microsoft.Office.Interop.Word.ContentControl> pode exibir vários tipos diferentes de interface do usuário que são otimizados para uso em documentos do Word, como um controle rich text, um seletor de data ou uma caixa de combinação. Você também pode usar um <xref:Microsoft.Office.Interop.Word.ContentControl> para impedir que os usuários editem seções do documento ou modelo.  
  
 O Visual Studio estende o <xref:Microsoft.Office.Interop.Word.ContentControl> objeto em vários controles de host diferente. Enquanto o <xref:Microsoft.Office.Interop.Word.ContentControl> objeto pode exibir qualquer um dos diferentes tipos de interface do usuário que estão disponíveis para controles de conteúdo, o Visual Studio fornece um tipo diferente para cada controle de conteúdo. Por exemplo, você pode usar um <xref:Microsoft.Office.Tools.Word.RichTextContentControl> criar um controle rich text, ou você pode usar um <xref:Microsoft.Office.Tools.Word.DatePickerContentControl> para criar um seletor de data. Esses controles de host se comportam como nativo <xref:Microsoft.Office.Interop.Word.ContentControl>, mas eles têm eventos adicionais e recursos de associação de dados. Para obter mais informações, consulte [controles de conteúdo](../vsto/content-controls.md).  
  
### <a name="bookmark-object"></a>Objeto de indicador  
 O <xref:Microsoft.Office.Interop.Word.Bookmark> objeto representa uma área contígua em um documento, com uma posição inicial e uma posição final. Você pode usar indicadores para marcar um local em um documento, ou como um contêiner para texto em um documento. Um <xref:Microsoft.Office.Interop.Word.Bookmark> objeto pode consistir de ponto de inserção ou ser tão grande quanto o documento inteiro. Um <xref:Microsoft.Office.Interop.Word.Bookmark> tem as seguintes características que defini-lo separadamente do <xref:Microsoft.Office.Interop.Word.Range> objeto:  
  
-   Você pode nomear o indicador em tempo de design.  
  
-   <xref:Microsoft.Office.Interop.Word.Bookmark>objetos são salvos com o documento e, portanto, não são excluídos quando o código de execução é interrompida ou o documento é fechado.  
  
-   Indicadores podem ser ocultados ou tornar visíveis pela configuração o <xref:Microsoft.Office.Interop.Word.View.ShowBookmarks%2A> propriedade o <xref:Microsoft.Office.Interop.Word.View> do objeto para **false** ou **true**.  
  
 O Visual Studio estende o <xref:Microsoft.Office.Interop.Word.Bookmark> objeto fornecendo o <xref:Microsoft.Office.Tools.Word.Bookmark> controle de host. O <xref:Microsoft.Office.Tools.Word.Bookmark> controle de host se comporta como um nativo <xref:Microsoft.Office.Interop.Word.Bookmark>, mas tem eventos adicionais e recursos de associação de dados. Você pode associar dados a um controle de indicador em um documento da mesma maneira que você associar dados a um controle de caixa de texto em um Windows Form. Para obter mais informações, consulte [indicador controle](../vsto/bookmark-control.md).  
  
##  <a name="WordOMDocumentation"></a>Usando a documentação de modelo de objeto do Word  
 Para obter informações completas sobre o modelo de objeto do Word, você pode consultar para a referência de assembly de interoperabilidade primária (PIA) do Word e do Visual Basic para referência de modelo de objeto Applications (VBA).  
  
### <a name="primary-interop-assembly-reference"></a>Referência de Assembly de interoperabilidade primária  
 A documentação de referência do Word PIA descreve os tipos no assembly de interoperabilidade primário para o Word. Esta documentação está disponível no seguinte local: [referência de Assembly de interoperabilidade do Word 2010 primário](http://go.microsoft.com/fwlink/?LinkId=189588).  
  
 Para obter mais informações sobre o design de PIA a palavra, como as diferenças entre classes e interfaces no PIA e como os eventos em que o PIA são implementados, consulte [visão geral de Classes e Interfaces de Assemblies de interoperabilidade primários do Office](http://go.microsoft.com/fwlink/?LinkId=189592).  
  
### <a name="vba-object-model-reference"></a>Referência de modelo de objeto do VBA  
 A referência de modelo de objeto VBA documenta o modelo de objeto do Word como ele é exposto ao código do VBA. Para obter mais informações, consulte [referência de modelo de objeto do Word 2010](http://go.microsoft.com/fwlink/?LinkId=199772).  
  
 Todos os objetos e membros na referência de modelo de objeto do VBA correspondem aos tipos e membros no PIA do Word. Por exemplo, o objeto de documento na referência de modelo de objeto do VBA corresponde do <xref:Microsoft.Office.Interop.Word.Document> objeto o PIA do Word. Embora a referência de modelo de objeto VBA fornece exemplos de código para a maioria das propriedades, métodos e eventos, você deve converter o código de VBA nesta referência do Visual Basic ou Visual c# se você quiser usá-los em uma palavra de projeto que você cria usando o Visual Studio.  
  
## <a name="see-also"></a>Consulte também  
 [Assemblies de interoperabilidade primários do Office](../vsto/office-primary-interop-assemblies.md)   
 [Automatizando o Word usando objetos estendidos](../vsto/automating-word-by-using-extended-objects.md)   
 [Trabalhando com documentos](../vsto/working-with-documents.md)   
 [Trabalhando com texto em documentos](../vsto/working-with-text-in-documents.md)   
 [Trabalhando com tabelas](../vsto/working-with-tables.md)   
 [Itens de host e visão geral dos controles de Host](../vsto/host-items-and-host-controls-overview.md)   
 [Limitações programáticas de itens de Host e controles de Host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)   
 [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)  
  
  