---
title: "Passo a passo: Associando controles de conteúdo a partes XML personalizadas | Microsoft Docs"
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
- PlainTextContentControl, binding to a custom XML part
- custom XML parts, binding to content controls
- content controls [Office development in Visual Studio], data binding
- data binding [Office development in Visual Studio], content controls
- DropDownListContentControl, binding items to a custom XML part
- DatePickerContentControl, binding to a custom XML part
author: TerryGLee
ms.author: tglee
manager: ghogen
ms.workload: office
ms.openlocfilehash: 1a8c8eff138e2c736750040dc896e610975c25ab
ms.sourcegitcommit: f9fbf1f55f9ac14e4e5c6ae58c30dc1800ca6cda
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/10/2018
---
# <a name="walkthrough-binding-content-controls-to-custom-xml-parts"></a>Instruções passo a passo: associando controles de conteúdo a partes XML personalizadas
  Este passo a passo demonstra como associar controles de conteúdo em uma personalização de nível de documento para Word para dados XML que são armazenados no documento.  
  
 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]  
  
 Word permite que você armazene dados XML, chamados *partes XML personalizadas*, em um documento. Você pode controlar a exibição de dados vinculando controles de conteúdo para os elementos em uma parte XML personalizada. O documento de exemplo neste passo a passo exibe informações de funcionários que são armazenadas em uma parte XML personalizada. Quando você abrir o documento, os controles de conteúdo exibem os valores dos elementos XML. As alterações que fizer no texto nos controles de conteúdo são salvos na parte XML personalizada.  
  
 Esta explicação passo a passo ilustra as seguintes tarefas:  
  
-   Adicionando controles de conteúdo para o documento do Word em um projeto no nível de documento em tempo de design.  
  
-   Criando um arquivo de dados XML e um esquema XML que define os elementos para associar a controles de conteúdo.  
  
-   Anexando o esquema XML para o documento em tempo de design.  
  
-   Adicionando o conteúdo do arquivo XML a uma parte XML personalizada no documento em tempo de execução.  
  
-   Associando os controles de conteúdo a elementos na parte XML personalizada.  
  
-   Associando um <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> para um conjunto de valores que são definidos no esquema XML.  
  
 [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes para concluir esta instrução passo a passo:  
  
-   [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]  
  
-   Microsoft Word.  
  
## <a name="creating-a-new-word-document-project"></a>Criar um novo projeto de documento do Word  
 Crie um documento do Word que você usará no passo a passo.  
  
#### <a name="to-create-a-new-word-document-project"></a>Para criar um novo projeto de documento do Word  
  
1.  Criar um projeto de documento do Word com o nome **EmployeeControls**. Crie um novo documento para a solução. Para obter mais informações, consulte [como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).  
  
     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]Abre um novo documento do Word no designer e adiciona o **EmployeeControls** projeto **Gerenciador de soluções**.  
  
## <a name="adding-content-controls-to-the-document"></a>Adicionando controles de conteúdo do documento  
 Crie uma tabela que contém três tipos diferentes de controles de conteúdo em que o usuário pode exibir ou editar informações sobre o funcionário.  
  
#### <a name="to-add-content-controls-to-the-document"></a>Para adicionar controles de conteúdo do documento  
  
1.  No documento do Word que está hospedado no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] designer, na faixa de opções, escolha o **inserir** guia.  
  
2.  No **tabelas** de grupo, escolha **tabela**e insira uma tabela com 2 colunas e 3 linhas.  
  
3.  Digite o texto na primeira coluna, para que ele se parece com a seguinte coluna:  
  
    ||  
    |-|  
    |**Nome do funcionário**|  
    |**Data de contratação**|  
    |**Título**|  
  
4.  Na segunda coluna da tabela, escolha a primeira linha (lado **nome de funcionário**).  
  
5.  Na faixa de opções, escolha o **desenvolvedor** guia.  
  
    > [!NOTE]  
    >  Se o **desenvolvedor** guia não estiver visível, você deve primeiro mostrá-la. Para obter mais informações, consulte [como: Mostrar a guia Desenvolvedor na faixa de opções](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md).  
  
6.  No **controles** de grupo, escolha o **texto** botão ![PlainTextContentControl](../vsto/media/plaintextcontrol.gif "PlainTextContentControl") para adicionar um <xref:Microsoft.Office.Tools.Word.PlainTextContentControl>para a primeira célula.  
  
7.  Na segunda coluna da tabela, escolha a segunda linha (lado **data de contratação**).  
  
8.  No **controles** de grupo, escolha o **seletor de data** botão ![DatePickerContentControl](../vsto/media/datepicker.gif "DatePickerContentControl") para adicionar um <xref:Microsoft.Office.Tools.Word.DatePickerContentControl> segunda célula.  
  
9. Na segunda coluna da tabela, selecione a terceira linha (lado **título**).  
  
10. No **controles** de grupo, escolha o **lista suspensa** botão ![DropDownListContentControl](../vsto/media/dropdownlist.gif "DropDownListContentControl") para adicionar um <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> até a última célula.  
  
 Que é a interface do usuário para este projeto. Se você executar o projeto agora, pode digitar o texto na primeira linha e selecione uma data na segunda linha. A próxima etapa é conectar os dados que você deseja exibir o documento em um arquivo XML.  
  
## <a name="creating-the-xml-data-file"></a>Criando o arquivo de dados XML  
 Normalmente, você obterá os dados XML para armazenar em uma parte XML personalizada de uma fonte externa, como um arquivo ou um banco de dados. Neste passo a passo, você deve criar um arquivo XML que contém os dados de funcionário, marcados por elementos que você associará aos controles de conteúdo do documento. Para disponibilizar os dados em tempo de execução, inserir o arquivo XML como um recurso no assembly de personalização.  
  
#### <a name="to-create-the-data-file"></a>Para criar o arquivo de dados  
  
1.  No menu **Projeto**, escolha **Adicionar Novo Item**.  
  
     A caixa de diálogo **Adicionar Novo Item** é exibida.  
  
2.  No **modelos** painel, selecione **arquivo XML**.  
  
3.  Nomeie o arquivo **funcionários**e, em seguida, escolha o **adicionar** botão.  
  
     O **funcionários** arquivo é aberto no Editor de códigos.  
  
4.  Substitua o conteúdo do **funcionários** arquivo com o texto a seguir.  
  
    ```  
    <?xml version="1.0" encoding="utf-8" ?>  
    <employees xmlns="http://schemas.microsoft.com/vsto/samples">  
      <employee>  
        <name>Karina Leal</name>  
        <hireDate>1999-04-01</hireDate>  
        <title>Manager</title>  
      </employee>  
    </employees>  
    ```  
  
5.  Em **Solution Explorer**, escolha o **funcionários** arquivo.  
  
6.  No **propriedades** janela, selecione o **ação de compilação** propriedade e, em seguida, altere o valor para **recurso inserido**.  
  
     Essa etapa incorpora o arquivo XML como um recurso no assembly quando você compilar o projeto. Isso permite que você acesse o conteúdo do arquivo XML em tempo de execução.  
  
## <a name="creating-an-xml-schema"></a>Criando um esquema XML  
 Se você deseja associar um controle de conteúdo a um único elemento em uma parte XML personalizada, você não precisa usar um esquema XML. No entanto, para associar o <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> para um conjunto de valores, você deve criar um esquema XML que valida o arquivo de dados XML que você criou anteriormente. O esquema XML define os valores possíveis para a `title` elemento. Você associará a <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> para este elemento este passo a passo.  
  
#### <a name="to-create-an-xml-schema"></a>Para criar um esquema XML  
  
1.  No menu **Projeto**, escolha **Adicionar Novo Item**.  
  
     A caixa de diálogo **Adicionar Novo Item** é exibida.  
  
2.  No **modelos** painel, selecione **esquema XML**.  
  
3.  Nome do esquema **XSD** e escolha o **adicionar** botão.  
  
     O designer de esquema é aberto.  
  
4.  Em **Solution Explorer**, abra o menu de atalho para **XSD**e, em seguida, escolha **Exibir código**.  
  
5.  Substitua o conteúdo do **XSD** arquivo com o esquema a seguir.  
  
    ```  
    <?xml version="1.0" encoding="utf-8" ?>  
    <xs:schema xmlns="http://schemas.microsoft.com/vsto/samples"   
        targetNamespace="http://schemas.microsoft.com/vsto/samples"  
        xmlns:xs="http://www.w3.org/2001/XMLSchema"  
        elementFormDefault="qualified">  
      <xs:element name="employees" type="EmployeesType"></xs:element>  
      <xs:complexType name="EmployeesType">  
        <xs:all>  
          <xs:element name="employee" type="EmployeeType"/>  
        </xs:all>  
      </xs:complexType>  
      <xs:complexType name="EmployeeType">  
        <xs:sequence>  
          <xs:element name="name" type="xs:string" minOccurs="1" maxOccurs="1"/>  
          <xs:element name="hireDate" type="xs:date" minOccurs="1" maxOccurs="1"/>  
          <xs:element name="title" type="TitleType" minOccurs="1" maxOccurs="1"/>  
        </xs:sequence>  
      </xs:complexType>  
      <xs:simpleType name="TitleType">  
        <xs:restriction base="xs:string">  
          <xs:enumeration value ="Engineer"/>  
          <xs:enumeration value ="Designer"/>  
          <xs:enumeration value ="Manager"/>  
        </xs:restriction>  
      </xs:simpleType>  
    </xs:schema>  
    ```  
  
6.  No **arquivo** menu, clique em **Salvar tudo** para salvar suas alterações para o **funcionários** e **XSD** arquivos.  
  
## <a name="attaching-the-xml-schema-to-the-document"></a>Anexar o esquema XML no documento  
 Você deve anexar o esquema XML para o documento para associar o <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> para os valores válidos do `title` elemento.  
  
#### <a name="to-attach-the-xml-schema-to-the-document-includeword15shortvstoincludesword-15-short-mdmd"></a>Para anexar o esquema XML para o documento ([!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)])  
  
1.  Ativar **EmployeeControls.docx** no designer.  
  
2.  Na faixa de opções, escolha o **desenvolvedor** guia e, em seguida, escolha o **Add-Ins** botão.  
  
3.  No **modelos e suplementos** caixa de diálogo caixa, escolha o **esquema XML** guia e, em seguida, escolha o **adicionar esquema** botão.  
  
4.  Navegue até o **XSD** esquema criado anteriormente, que está localizado no diretório do projeto e, em seguida, escolha o **abrir** botão.  
  
5.  Escolha o **Okey** no botão de **configurações do esquema** caixa de diálogo.  
  
6.  Escolha o **Okey** para fechar o **modelos e suplementos** caixa de diálogo.  
  
#### <a name="to-attach-the-xml-schema-to-the-document-word-2010"></a>Para anexar o esquema XML para o documento (Word 2010)  
  
1.  Ativar **EmployeeControls.docx** no designer.  
  
2.  Na faixa de opções, escolha o **desenvolvedor** guia.  
  
3.  No **XML** de grupo, escolha o **esquema** botão.  
  
4.  No **modelos e suplementos** caixa de diálogo caixa, escolha o **esquema XML** guia e, em seguida, escolha o **adicionar esquema** botão.  
  
5.  Navegue até o **XSD** esquema que você criou anteriormente, que está localizada no diretório do projeto e escolha o **abrir** botão.  
  
6.  Escolha o **Okey** no botão de **configurações do esquema** caixa de diálogo.  
  
7.  Escolha o **Okey** para fechar o **modelos e suplementos** caixa de diálogo.  
  
     O **estrutura XML** é aberto o painel de tarefas.  
  
8.  Fechar o **estrutura XML** painel de tarefas.  
  
## <a name="adding-a-custom-xml-part-to-the-document"></a>Adicionando uma parte XML personalizada para o documento  
 Antes de associar os controles de conteúdo para os elementos no arquivo XML, você deve adicionar o conteúdo do arquivo XML para uma nova parte XML personalizada no documento.  
  
#### <a name="to-add-a-custom-xml-part-to-the-document"></a>Para adicionar uma parte XML personalizada para o documento  
  
1.  Em **Solution Explorer**, abra o menu de atalho para **ThisDocument.cs** ou **ThisDocument. vb**e, em seguida, escolha **Exibir código**.  
  
2.  Adicione as seguintes declarações para o `ThisDocument` classe. Esse código declara vários objetos que você usará para adicionar uma parte XML personalizada para o documento.  
  
     [!code-csharp[Trin_ContentControlXmlPartWalkthrough#1](../vsto/codesnippet/CSharp/EmployeeControls/ThisDocument.cs#1)]
     [!code-vb[Trin_ContentControlXmlPartWalkthrough#1](../vsto/codesnippet/VisualBasic/EmployeeControls/ThisDocument.vb#1)]  
  
3.  Adicione o seguinte método à classe `ThisDocument`. Esse método obtém o conteúdo do arquivo de dados XML que será inserido como um recurso no assembly e retorna o conteúdo como uma cadeia de caracteres XML.  
  
     [!code-csharp[Trin_ContentControlXmlPartWalkthrough#3](../vsto/codesnippet/CSharp/EmployeeControls/ThisDocument.cs#3)]
     [!code-vb[Trin_ContentControlXmlPartWalkthrough#3](../vsto/codesnippet/VisualBasic/EmployeeControls/ThisDocument.vb#3)]  
  
4.  Adicione o seguinte método à classe `ThisDocument`. O `AddCustomXmlPart` método cria uma nova parte XML personalizada que contém uma cadeia de caracteres XML que é passada para o método.  
  
     Para garantir que a parte XML personalizada é criada apenas uma vez, o método cria o XML personalizado parte apenas se uma parte XML personalizada com um GUID correspondente não já existe no documento. Na primeira vez que esse método é chamado, ele salva o valor da <xref:Microsoft.Office.Core._CustomXMLPart.Id%2A> propriedade para o `employeeXMLPartID` cadeia de caracteres. O valor da `employeeXMLPartID` cadeia de caracteres é persistida no documento porque ele foi declarado usando a <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> atributo.  
  
     [!code-csharp[Trin_ContentControlXmlPartWalkthrough#4](../vsto/codesnippet/CSharp/EmployeeControls/ThisDocument.cs#4)]
     [!code-vb[Trin_ContentControlXmlPartWalkthrough#4](../vsto/codesnippet/VisualBasic/EmployeeControls/ThisDocument.vb#4)]  
  
## <a name="binding-the-content-controls-to-elements-in-the-custom-xml-part"></a>Associando os controles de conteúdo a elementos na parte XML personalizada  
 Associe cada controle de conteúdo a um elemento na parte XML personalizada usando o **XMLMapping** propriedade de cada controle de conteúdo.  
  
#### <a name="to-bind-the-content-controls-to-elements-in-the-custom-xml-part"></a>Para vincular os controles de conteúdo a elementos na parte XML personalizada  
  
1.  Adicione o seguinte método à classe `ThisDocument`. Esse método associa cada controle de conteúdo a um elemento na parte XML personalizada e define o formato de exibição da data de <xref:Microsoft.Office.Tools.Word.DatePickerContentControl>.  
  
     [!code-csharp[Trin_ContentControlXmlPartWalkthrough#5](../vsto/codesnippet/CSharp/EmployeeControls/ThisDocument.cs#5)]
     [!code-vb[Trin_ContentControlXmlPartWalkthrough#5](../vsto/codesnippet/VisualBasic/EmployeeControls/ThisDocument.vb#5)]  
  
## <a name="running-your-code-when-the-document-is-opened"></a>Executar o código quando o documento é aberto.  
 Criar a parte XML personalizada e associar os controles personalizados para os dados quando o documento é aberto.  
  
#### <a name="to-run-your-code-when-the-document-is-opened"></a>Para executar seu código, quando o documento é aberto.  
  
1.  Adicione o seguinte código para o `ThisDocument_Startup` método o `ThisDocument` classe. Esse código obtém a cadeia de caracteres de XML de **funcionários** arquivo, adiciona a cadeia de caracteres XML para uma nova parte XML personalizada no documento e associa os controles de conteúdo para elementos na parte XML personalizada.  
  
     [!code-csharp[Trin_ContentControlXmlPartWalkthrough#2](../vsto/codesnippet/CSharp/EmployeeControls/ThisDocument.cs#2)]
     [!code-vb[Trin_ContentControlXmlPartWalkthrough#2](../vsto/codesnippet/VisualBasic/EmployeeControls/ThisDocument.vb#2)]  
  
## <a name="testing-the-project"></a>O projeto de teste  
 Quando você abrir o documento, os controles de conteúdo exibem dados de elementos na parte XML personalizada. Você pode clicar no <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> para selecionar um dos três valores válidos para o `title` elemento, que são definidos no **XSD** arquivo. Se você editar os dados em qualquer um dos controles de conteúdo, os novos valores são salvos na parte XML personalizada no documento.  
  
#### <a name="to-test-the-content-controls"></a>Para testar os controles de conteúdo  
  
1.  Pressione F5 para executar o projeto.  
  
2.  Verifique se a tabela no documento se parece com a tabela a seguir. Cada uma das cadeias de caracteres na segunda coluna é obtida de um elemento na parte XML personalizada no documento.  
  
    |||  
    |-|-|  
    |**Nome do funcionário**|**Karina Leal**|  
    |**Data de contratação**|**1 de abril de 1999**|  
    |**Título**|**Gerenciador de**|  
  
3.  Escolha a célula à direita do **nome de funcionário** da célula e digite um nome diferente.  
  
4.  Escolha a célula à direita do **data de contratação** célula e selecione uma data diferente no seletor de data.  
  
5.  Escolha a célula à direita do **título** célula e selecione um novo item na lista suspensa.  
  
6.  Salve e feche o documento.  
  
7.  No Explorador de arquivos, abra a pasta de \bin\Debug sob o local do seu projeto.  
  
8.  Abra o menu de atalho para **EmployeeControls.docx** e, em seguida, escolha **Renomear**.  
  
9. Nomeie o arquivo **EmployeeControls.docx.zip**.  
  
     O **EmployeeControls.docx** documento é salvo no formato XML aberto. Renomeando este documento com a extensão de nome de arquivo. zip, você pode examinar o conteúdo do documento. Para obter mais informações sobre Open XML, consulte o artigo técnico [apresentando formatos XML abertos do Office (2007)](http://msdn.microsoft.com/en-us/96018532-f62c-4da7-bbff-16b96a483fbf).  
  
10. Abra o **EmployeeControls.docx.zip** arquivo.  
  
11. Abra o **customXml** pasta.  
  
12. Abra o menu de atalho para **item2.xml** e, em seguida, escolha **abrir**.  
  
     Este arquivo contém a parte XML personalizada que você adicionou ao documento.  
  
13. Verifique o `name`, `hireDate`, e `title` elementos contêm os novos valores que você inseriu em controles de conteúdo do documento.  
  
14. Fechar o **item2.xml** arquivo.  
  
## <a name="next-steps"></a>Próximas etapas  
 Você pode aprender mais sobre como usar os controles de conteúdo com estes tópicos:  
  
-   Use todos os controles de conteúdo disponíveis para criar um modelo. Para obter mais informações, consulte [passo a passo: Criando um modelo por usando controles de conteúdo](../vsto/walkthrough-creating-a-template-by-using-content-controls.md).  
  
-   Modifique os dados em partes XML personalizadas enquanto o documento é fechado. Na próxima vez que o usuário abre o documento, os controles de conteúdo que estão associados aos elementos XML exibirá os novos dados.  
  
-   Use controles de conteúdo para proteger partes de um documento. Para obter mais informações, consulte [como: proteger partes de documentos por controles de conteúdo usando](../vsto/how-to-protect-parts-of-documents-by-using-content-controls.md).  
  
## <a name="see-also"></a>Consulte também  
 [Automatizando o Word usando objetos estendidos](../vsto/automating-word-by-using-extended-objects.md)   
 [Controles de conteúdo](../vsto/content-controls.md)   
 [Como: adicionar controles Content a documentos do Word](../vsto/how-to-add-content-controls-to-word-documents.md)   
 [Como: proteger partes de documentos usando controles de conteúdo](../vsto/how-to-protect-parts-of-documents-by-using-content-controls.md)   
 [Itens de host e visão geral dos controles de Host](../vsto/host-items-and-host-controls-overview.md)   
 [Limitações programáticas de itens de Host e controles de Host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)   
 [Adicionando controles a documentos do Office no tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md)  
  
  