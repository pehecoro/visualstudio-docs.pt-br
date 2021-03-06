---
title: 'Passo a passo: Criando um Item de projeto da coluna de Site com um modelo de projeto, parte 1 | Microsoft Docs'
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
- SharePoint project items, defining your own types
- project items [SharePoint development in Visual Studio], defining your own types
- SharePoint projects, creating custom templates
- SharePoint development in Visual Studio, defining new project item types
author: TerryGLee
ms.author: tglee
manager: ghogen
ms.workload: office
ms.openlocfilehash: 2266fc715322c024625e5f52f83805d0d582416b
ms.sourcegitcommit: f9fbf1f55f9ac14e4e5c6ae58c30dc1800ca6cda
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/10/2018
---
# <a name="walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1"></a>Instruções passo a passo: criando um item de projeto da coluna de site com um modelo de projeto, parte 1
  Projetos SharePoint são contêineres para um ou mais itens de projeto do SharePoint. Você pode estender o sistema de projeto do SharePoint no Visual Studio, criar seus próprios tipos de item de projeto do SharePoint e, em seguida, associá-los a um modelo de projeto. Neste passo a passo, você definirá um tipo de item de projeto para a criação de uma coluna de site e, em seguida, você criará um modelo de projeto que pode ser usado para criar um novo projeto que contém um item de projeto da coluna de site.  
  
 Este passo a passo demonstra as seguintes tarefas:  
  
-   Criando uma extensão do Visual Studio que define um novo tipo de item de projeto do SharePoint para uma coluna de site. O tipo de item de projeto inclui uma propriedade personalizada simple que aparece no **propriedades** janela.  
  
-   Criando um [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] modelo de projeto para o item de projeto.  
  
-   Criando um [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] pacote de extensão (VSIX) para implantar o modelo de projeto e o assembly de extensão.  
  
-   Depurando e testando o item de projeto.  
  
 Este é um passo a passo autônoma. Depois de concluir este passo a passo, você pode melhorar o item de projeto com a adição de um Assistente para o modelo de projeto. Para obter mais informações, consulte [passo a passo: Criando um Item de projeto da coluna de Site com um modelo de projeto, parte 2](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md).  
  
> [!NOTE]  
>  Você pode baixar um exemplo que contém os projetos concluídos, código e outros arquivos para este passo a passo no seguinte local: [http://go.microsoft.com/fwlink/?LinkId=191369](http://go.microsoft.com/fwlink/?LinkId=191369).  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisará dos seguintes componentes no computador de desenvolvimento para concluir este passo a passo:  
  
-   Edições com suporte do Microsoft Windows, SharePoint e [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]. Para obter mais informações, consulte [requisitos para desenvolver soluções do SharePoint](../sharepoint/requirements-for-developing-sharepoint-solutions.md).  
  
-   O [!INCLUDE[vssdk_current_long](../sharepoint/includes/vssdk-current-long-md.md)]. Este passo a passo usa o **projeto VSIX** modelo no SDK para criar um pacote do VSIX para implantar o item de projeto. Para obter mais informações, consulte [estendendo as ferramentas do SharePoint no Visual Studio](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md).  
  
 O conhecimento do conceito seguinte é útil, mas não necessário, para concluir o passo a passo:  
  
-   Colunas de site do SharePoint. Para obter mais informações, consulte [colunas](http://go.microsoft.com/fwlink/?LinkId=183547).  
  
-   Modelos de projeto no Visual Studio. Para obter mais informações, consulte [Criando modelos de item e de projeto](/visualstudio/ide/creating-project-and-item-templates).  
  
## <a name="creating-the-projects"></a>Criando os Projetos  
 Para concluir este passo a passo, você precisa criar três projetos:  
  
-   Um projeto do VSIX. Este projeto cria o pacote do VSIX para implantar o item de projeto da coluna de site e o modelo de projeto.  
  
-   Um projeto de modelo de projeto. Este projeto cria um modelo de projeto que pode ser usado para criar um novo projeto do SharePoint que contém o item de projeto da coluna de site.  
  
-   Um projeto de biblioteca de classe. Este projeto que implementa uma extensão do Visual Studio que define o comportamento do item de projeto de coluna de site.  
  
 Criando projetos para iniciar o passo a passo.  
  
#### <a name="to-create-the-vsix-project"></a>Para criar o projeto do VSIX  
  
1.  Inicie o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].  
  
2.  Na barra de menus, escolha **Arquivo**, **Novo**, **Projeto**.  
  
3.  Na parte superior do **novo projeto** caixa de diálogo caixa, certifique-se de que **.NET Framework 4.5** for escolhido na lista de versões do .NET Framework.  
  
4.  Expanda o **Visual Basic** ou **Visual C#** nós e, em seguida, escolha o **extensibilidade** nó.  
  
    > [!NOTE]  
    >  O **extensibilidade** nó estará disponível somente se você instalar o SDK do Visual Studio. Para obter mais informações, consulte a seção pré-requisitos neste tópico.  
  
5.  Na lista de modelos de projeto, escolha **projeto VSIX**.  
  
6.  No **nome** , digite **SiteColumnProjectItem**e, em seguida, escolha o **Okey** botão.  
  
     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]Adiciona o **SiteColumnProjectItem** projeto **Gerenciador de soluções**.  
  
#### <a name="to-create-the-project-template-project"></a>Para criar o projeto de modelo de projeto  
  
1.  Em **Solution Explorer**, abra o menu de atalho para o nó da solução, escolha **adicionar**e, em seguida, escolha **novo projeto**.  
  
2.  Na parte superior do **novo projeto** caixa de diálogo caixa, certifique-se de que **.NET Framework 4.5** for escolhido na lista de versões do .NET Framework.  
  
3.  Expanda o **Visual C#** ou **Visual Basic** nó e, em seguida, escolha o **extensibilidade** nó.  
  
4.  Na lista de modelos de projeto, escolha o **o modelo de projeto c#** ou **modelo de projeto do Visual Basic** modelo.  
  
5.  No **nome** , digite **SiteColumnProjectTemplate**e, em seguida, escolha o **Okey** botão.  
  
     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]Adiciona o **SiteColumnProjectTemplate** projeto à solução.  
  
6.  Exclua o arquivo de código Class1 do projeto.  
  
7.  Se você criou um projeto do Visual Basic, também exclua os seguintes arquivos do projeto:  
  
    -   MyApplication.Designer.vb  
  
    -   MyApplication.myapp  
  
    -   Resources.Designer.vb  
  
    -   Resx  
  
    -   Settings.Designer.vb  
  
    -   Settings  
  
#### <a name="to-create-the-extension-project"></a>Para criar o projeto de extensão  
  
1.  Em **Solution Explorer**, abra o menu de atalho para o nó da solução, escolha **adicionar**e, em seguida, escolha **novo projeto**.  
  
2.  Na parte superior do **novo projeto** caixa de diálogo caixa, certifique-se de que **.NET Framework 4.5** for escolhido na lista de versões do .NET Framework.  
  
3.  Expanda o **Visual C#** ou **Visual Basic** nós, escolha o **Windows** nó e, em seguida, escolha o **biblioteca de classes** modelo.  
  
4.  No **nome** , digite **ProjectItemTypeDefinition** e, em seguida, escolha o **Okey** botão.  
  
     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]Adiciona o **ProjectItemTypeDefinition** projeto à solução e abre o arquivo de código Class1 padrão.  
  
5.  Exclua o arquivo de código Class1 do projeto.  
  
## <a name="configuring-the-extension-project"></a>Configurando o projeto de extensão  
 Adicione arquivos de código e referências de assembly para configurar o projeto de extensão.  
  
#### <a name="to-configure-the-project"></a>Configurar o projeto  
  
1.  No projeto ProjectItemTypeDefinition, adicione um arquivo de código que é chamado **SiteColumnProjectItemTypeProvider**.  
  
2.  Na barra de menus, escolha **Projeto**, **Adicionar Referência**.  
  
3.  No **Gerenciador de referências - ProjectItemTypeDefinition** caixa de diálogo caixa, expanda o **Assemblies** nó, escolha o **Framework** nó e, em seguida, selecione o Caixa de seleção System.ComponentModel.Composition.  
  
4.  Escolha o **extensões** nó, selecione a caixa de seleção ao lado de assembly Microsoft.VisualStudio.SharePoint e, em seguida, escolha o **Okey** botão.  
  
## <a name="defining-the-new-sharepoint-project-item-type"></a>Definir o novo tipo de Item de projeto do SharePoint  
 Criar uma classe que implementa o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> interface para definir o comportamento do novo tipo de item de projeto. Implemente esta interface sempre que você deseja definir um novo tipo de item de projeto.  
  
#### <a name="to-define-the-new-sharepoint-project-item-type"></a>Para definir o novo tipo de item de projeto do SharePoint  
  
1.  No **SiteColumnProjectItemTypeProvider** arquivo de código, substitua o código padrão com o código a seguir e, em seguida, salve o arquivo.  
  
     [!code-csharp[SPExtensibility.ProjectItem.SiteColumn#1](../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projectitemtypedefinition/sitecolumnprojectitemtypeprovider.cs#1)]
     [!code-vb[SPExtensibility.ProjectItem.SiteColumn#1](../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projectitemtypedefinition/sitecolumnprojectitemtypeprovider.vb#1)]  
  
## <a name="creating-a-visual-studio-project-template"></a>Criando um modelo de projeto do Visual Studio  
 Criando um modelo de projeto, você deve habilitar outros desenvolvedores a criar projetos do SharePoint que contêm itens de projeto de coluna de site. Um modelo de projeto do SharePoint inclui arquivos que são necessários para todos os projetos no Visual Studio, como. csproj ou. vbproj,. vstemplate arquivos e arquivos que são específicos para projetos do SharePoint. Para obter mais informações, consulte [criando modelos de Item e modelos de projeto do SharePoint para itens de projeto](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md).  
  
 Neste procedimento, você deve criar um projeto vazio do SharePoint para gerar os arquivos que são específicos para projetos do SharePoint. Em seguida, adicionar esses arquivos ao projeto SiteColumnProjectTemplate para que eles estão incluídos no modelo que é gerado a partir deste projeto. Você também configurar o arquivo de projeto SiteColumnProjectTemplate para especificar onde o modelo de projeto aparece no **novo projeto** caixa de diálogo.  
  
#### <a name="to-create-the-files-for-the-project-template"></a>Para criar os arquivos para o modelo de projeto  
  
1.  Inicie uma segunda instância de [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] com credenciais administrativas.  
  
2.  Criar um projeto do SharePoint 2010 que é nomeado **BaseSharePointProject**.  
  
    > [!IMPORTANT]  
    >  No **Assistente de personalização do SharePoint**, não selecione a **implantar como uma solução de farm** botão de opção.  
  
3.  Adicionar um item de elemento vazio para o projeto e, em seguida, o nome do item **Field1**.  
  
4.  Salve o projeto e, em seguida, feche a segunda instância de [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].  
  
5.  Na instância do [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] que tem o SiteColumnProjectItem solução aberto, em **Solution Explorer**, abra o menu de atalho para o **SiteColumnProjectTemplate** nó do projeto, escolha  **Adicionar**e, em seguida, escolha **Item existente**.  
  
6.  No **Add Existing Item** caixa de diálogo, abra a lista de extensões de arquivo e, em seguida, escolha **todos os arquivos (\*.\*)** .  
  
7.  No diretório que contém o projeto BaseSharePointProject, selecione o arquivo key.snk e, em seguida, escolha o **adicionar** botão.  
  
    > [!NOTE]  
    >  Neste passo a passo, o modelo de projeto que você cria usa o mesmo arquivo de key.snk para assinar cada projeto que é criado usando o modelo. Para saber como expandir esse exemplo para criar um arquivo de key.snk diferente para cada instância de projeto, consulte [passo a passo: Criando um Item de projeto da coluna de Site com um modelo de projeto, parte 2](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md).  
  
8.  Repita as etapas 5 a 8 para adicionar os seguintes arquivos de subpastas especificadas no diretório BaseSharePointProject:  
  
    -   \Field1\Elements.XML  
  
    -   \Field1\SharePointProjectItem.spdata  
  
    -   \Features\Feature1\Feature1.Feature  
  
    -   \Features\Feature1\Feature1.Template.XML  
  
    -   \Package\Package.Package  
  
    -   \Package\Package.Template.XML  
  
     Adicionar esses arquivos diretamente para o projeto SiteColumnProjectTemplate; não recrie as subpastas Field1, recursos ou pacote no projeto. Para obter mais informações sobre esses arquivos, consulte [criando modelos de Item e modelos de projeto do SharePoint para itens de projeto](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md).  
  
#### <a name="to-configure-how-developers-discover-the-project-template-in-the-new-project-dialog-box"></a>Para configurar como os desenvolvedores de descobrir o modelo de projeto na caixa de diálogo Novo projeto  
  
1.  Em **Solution Explorer**, abra o menu de atalho para o **SiteColumnProjectTemplate** nó do projeto e escolha **descarregar projeto**. Se você for solicitado a salvar as alterações para todos os arquivos, escolha o **Sim** botão.  
  
2.  Abra o menu de atalho para o **SiteColumnProjectTemplate** novamente, o nó e, em seguida, escolha **Editar SiteColumnProjectTemplate.csproj** ou **SiteColumnProjectTemplate.vbproj editar**.  
  
3.  No arquivo de projeto, localize o seguinte `VSTemplate` elemento.  
  
    ```  
    <VSTemplate Include="SiteColumnProjectTemplate.vstemplate">  
    ```  
  
4.  Substitua este elemento XML a seguir.  
  
    ```  
    <VSTemplate Include="SiteColumnProjectTemplate.vstemplate">  
      <OutputSubPath>SharePoint\SharePoint14</OutputSubPath>  
    </VSTemplate>  
    ```  
  
     O `OutputSubPath` elemento Especifica pastas adicionais no caminho no qual o modelo de projeto é criado quando você compila o projeto. As pastas especificadas aqui Certifique-se de que o modelo de projeto estará disponível somente quando os clientes abrir o **novo projeto** caixa de diálogo caixa, expanda o **SharePoint** nó e, em seguida, escolha o **2010**  nó.  
  
5.  Salve e feche o arquivo.  
  
6.  Em **Solution Explorer**, abra o menu de atalho para o **SiteColumnProjectTemplate** do projeto e, em seguida, escolha **recarregar projeto**.  
  
## <a name="editing-the-project-template-files"></a>Editando os arquivos de modelo de projeto  
 No projeto SiteColumnProjectTemplate, edite os arquivos a seguir para definir o comportamento do modelo de projeto:  
  
-   AssemblyInfo.cs ou AssemblyInfo  
  
-   Elements  
  
-   SharePointProjectItem.spdata  
  
-   Feature1.Feature  
  
-   Pacote  
  
-   SiteColumnProjectTemplate.vstemplate  
  
-   ProjectTemplate.csproj ou ProjectTemplate.vbproj  
  
 Os procedimentos a seguir, você adicionará parâmetros substituíveis para alguns desses arquivos. Um parâmetro de substituição é um token que inicia e termina com o caractere de cifrão ($). Quando um usuário usa esse modelo de projeto para criar um projeto, o Visual Studio substitui automaticamente esses parâmetros no novo projeto com valores específicos. Para obter mais informações, consulte [parâmetros substituíveis](../sharepoint/replaceable-parameters.md).  
  
#### <a name="to-edit-the-assemblyinfocs-or-assemblyinfovb-file"></a>Para editar o arquivo AssemblyInfo.cs ou AssemblyInfo  
  
1.  No projeto SiteColumnProjectTemplate, abra o arquivo AssemblyInfo.cs ou AssemblyInfo. vb e, em seguida, adicione a seguinte instrução para a parte superior:  
  
    ```vb  
    Imports System.Security  
    ```  
  
    ```csharp  
    using System.Security;  
    ```  
  
     Quando o **solução em área restrita** propriedade de um projeto do SharePoint é definida como **True**, o Visual Studio adiciona o <xref:System.Security.AllowPartiallyTrustedCallersAttribute> ao arquivo de código AssemblyInfo. No entanto, o arquivo AssemblyInfo de código no modelo de projeto não importa o <xref:System.Security> namespace por padrão. Você deve adicionar esse **usando** ou **Imports** instrução para evitar erros de compilação.  
  
2.  Salve e feche o arquivo.  
  
#### <a name="to-edit-the-elementsxml-file"></a>Para editar o arquivo Elements  
  
1.  No projeto SiteColumnProjectTemplate, substitua o conteúdo do arquivo Elements XML a seguir.  
  
    ```  
    <?xml version="1.0" encoding="utf-8"?>  
    <Elements xmlns="http://schemas.microsoft.com/sharepoint/">  
      <Field ID="{$guid5$}"   
          Name="$safeprojectname$"   
          DisplayName="$projectname$"   
          Type="Text"   
          Group="Custom Columns">  
      </Field>  
    </Elements>  
    ```  
  
     O novo XML adiciona uma `Field` elemento que define o nome da coluna de site, seu tipo base e o grupo na qual a coluna de site na Galeria. Para obter mais informações sobre o conteúdo desse arquivo, consulte [esquema de definição de campo](http://go.microsoft.com/fwlink/?LinkId=184290).  
  
2.  Salve e feche o arquivo.  
  
#### <a name="to-edit-the-sharepointprojectitemspdata-file"></a>Para editar o arquivo SharePointProjectItem.spdata  
  
1.  No projeto SiteColumnProjectTemplate, substitua o conteúdo do arquivo SharePointProjectItem.spdata pelo XML a seguir.  
  
    ```  
    <?xml version="1.0" encoding="utf-8"?>  
    <ProjectItem Type="Contoso.SiteColumn" DefaultFile="Elements.xml"   
                 xmlns="http://schemas.microsoft.com/VisualStudio/2010/SharePointTools/SharePointProjectItemModel">  
      <Files>  
        <ProjectItemFile Source="Elements.xml" Target="$safeprojectname$\" Type="ElementManifest" />  
      </Files>   
    </ProjectItem>  
    ```  
  
     O novo XML faz as seguintes alterações para o arquivo:  
  
    -   Alterações de `Type` atributo do `ProjectItem` elemento para a mesma cadeia de caracteres que é passado para o <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemTypeAttribute> na definição de item de projeto (o `SiteColumnProjectItemTypeProvider` classe que você criou anteriormente neste passo a passo).  
  
    -   Remove o `SupportedTrustLevels` e `SupportedDeploymentScopes` atributos do `ProjectItem` elemento. Esses valores de atributo são desnecessários porque os níveis de confiança e escopos de implantação são especificados no `SiteColumnProjectItemTypeProvider` classe no projeto ProjectItemTypeDefinition.  
  
     Para obter mais informações sobre o conteúdo de arquivos. spdata, consulte [referência de esquema de Item de projeto do SharePoint](../sharepoint/sharepoint-project-item-schema-reference.md).  
  
2.  Salve e feche o arquivo.  
  
#### <a name="to-edit-the-feature1feature-file"></a>Para editar o arquivo Feature1.feature  
  
1.  No projeto SiteColumnProjectTemplate, substitua o conteúdo do arquivo Feature1.feature pelo XML a seguir.  
  
    ```  
    <?xml version="1.0" encoding="utf-8"?>  
    <feature xmlns:dm0="http://schemas.microsoft.com/VisualStudio/2008/DslTools/Core" dslVersion="1.0.0.0" Id="$guid4$" featureId="$guid4$"   
             imageUrl="" solutionId="00000000-0000-0000-0000-000000000000" title="Site Column Feature1" version=""  
             deploymentPath="$SharePoint.Project.FileNameWithoutExtension$_$SharePoint.Feature.FileNameWithoutExtension$"  
             xmlns="http://schemas.microsoft.com/VisualStudio/2008/SharePointTools/FeatureModel">  
      <projectItems>  
        <projectItemReference itemId="$guid2$" />  
      </projectItems>  
    </feature>  
    ```  
  
     O novo XML faz as seguintes alterações para o arquivo:  
  
    -   Altera os valores da `Id` e `featureId` atributos do `feature` elemento `$guid4$`.  
  
    -   Altera os valores da `itemId` atributo o `projectItemReference` elemento `$guid2$`.  
  
     Para obter mais informações sobre arquivos .feature, consulte [criando modelos de Item e modelos de projeto do SharePoint para itens de projeto](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md).  
  
2.  Salve e feche o arquivo.  
  
#### <a name="to-edit-the-packagepackage-file"></a>Para editar o arquivo de pacote  
  
1.  No projeto SiteColumnProjectTemplate, substitua o conteúdo do arquivo de pacote com o XML a seguir.  
  
    ```  
    <?xml version="1.0" encoding="utf-8"?>  
    <package xmlns:dm0="http://schemas.microsoft.com/VisualStudio/2008/DslTools/Core" dslVersion="1.0.0.0"   
             Id="$guid3$" solutionId="$guid3$" resetWebServer="false" name="$safeprojectname$"   
             xmlns="http://schemas.microsoft.com/VisualStudio/2008/SharePointTools/PackageModel">  
      <features>  
        <featureReference itemId="$guid4$" />  
      </features>  
    </package>  
    ```  
  
     O novo XML faz as seguintes alterações para o arquivo:  
  
    -   Altera os valores da `Id` e `solutionId` atributos do `package` elemento `$guid3$`.  
  
    -   Altera os valores da `itemId` atributo o `featureReference` elemento `$guid4$`.  
  
     Para obter mais informações sobre arquivos .package, consulte [criando modelos de Item e modelos de projeto do SharePoint para itens de projeto](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md).  
  
2.  Salve e feche o arquivo.  
  
#### <a name="to-edit-the-sitecolumnprojecttemplatevstemplate-file"></a>Para editar o arquivo SiteColumnProjectTemplate.vstemplate  
  
1.  No projeto SiteColumnProjectTemplate, substitua o conteúdo do arquivo SiteColumnProjectTemplate.vstemplate com uma das seções a seguir do XML.  
  
    -   Se você estiver criando um modelo de projeto do Visual c#, use o seguinte XML.  
  
    ```  
    <?xml version="1.0" encoding="utf-8"?>  
    <VSTemplate Version="3.0.0" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005" Type="Project">  
      <TemplateData>  
        <Name>Site Column</Name>  
        <Description>Creates a new site column in SharePoint</Description>  
        <FrameworkVersion>3.5</FrameworkVersion>  
        <ProjectType>CSharp</ProjectType>  
        <CreateNewFolder>true</CreateNewFolder>  
        <CreateInPlace>true</CreateInPlace>  
        <ProvideDefaultName>true</ProvideDefaultName>  
        <DefaultName>SiteColumn</DefaultName>  
        <LocationField>Enabled</LocationField>  
        <EnableLocationBrowseButton>true</EnableLocationBrowseButton>  
        <PromptForSaveOnCreation>true</PromptForSaveOnCreation>  
        <NumberOfParentCategoriesToRollUp>1</NumberOfParentCategoriesToRollUp>  
        <Icon>SiteColumnProjectTemplate.ico</Icon>  
        <SortOrder>1000</SortOrder>  
      </TemplateData>  
      <TemplateContent>  
        <Project TargetFileName="SharePointProject1.csproj" File="ProjectTemplate.csproj" ReplaceParameters="true">  
          <ProjectItem ReplaceParameters="true" TargetFileName="Properties\AssemblyInfo.cs">AssemblyInfo.cs</ProjectItem>  
          <ProjectItem ReplaceParameters="true" TargetFileName="Features\Feature1\Feature1.feature">Feature1.feature</ProjectItem>  
          <ProjectItem ReplaceParameters="true" TargetFileName="Features\Feature1\Feature1.Template.xml">Feature1.template.xml</ProjectItem>  
          <ProjectItem ReplaceParameters="true" TargetFileName="Package\Package.package">Package.package</ProjectItem>  
          <ProjectItem ReplaceParameters="true" TargetFileName="Package\Package.Template.xml">Package.Template.xml</ProjectItem>  
          <ProjectItem ReplaceParameters="true" TargetFileName="Field1\SharePointProjectItem.spdata">SharePointProjectItem.spdata</ProjectItem>  
          <ProjectItem ReplaceParameters="true" TargetFileName="Field1\Elements.xml" OpenInEditor="true">Elements.xml</ProjectItem>  
          <ProjectItem ReplaceParameters="false" TargetFileName="key.snk">key.snk</ProjectItem>  
        </Project>  
      </TemplateContent>  
    </VSTemplate>  
    ```  
  
    -   Se você estiver criando um modelo de projeto do Visual Basic, use o seguinte XML.  
  
    ```  
    <?xml version="1.0" encoding="utf-8"?>  
    <VSTemplate Version="3.0.0" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005" Type="Project">  
      <TemplateData>  
        <Name>Site Column</Name>  
        <Description>Creates a new site column in SharePoint</Description>  
        <FrameworkVersion>3.5</FrameworkVersion>  
        <ProjectType>VisualBasic</ProjectType>  
        <CreateNewFolder>true</CreateNewFolder>  
        <CreateInPlace>true</CreateInPlace>  
        <ProvideDefaultName>true</ProvideDefaultName>  
        <DefaultName>SiteColumn</DefaultName>  
        <LocationField>Enabled</LocationField>  
        <EnableLocationBrowseButton>true</EnableLocationBrowseButton>  
        <PromptForSaveOnCreation>true</PromptForSaveOnCreation>  
        <NumberOfParentCategoriesToRollUp>1</NumberOfParentCategoriesToRollUp>  
        <Icon>SiteColumnProjectTemplate.ico</Icon>  
        <SortOrder>1000</SortOrder>  
      </TemplateData>  
      <TemplateContent>  
        <Project TargetFileName="SharePointProject1.vbproj" File="ProjectTemplate.vbproj" ReplaceParameters="true">  
          <ProjectItem ReplaceParameters="true" TargetFileName="My Project\AssemblyInfo.vb">AssemblyInfo.vb</ProjectItem>  
          <ProjectItem ReplaceParameters="true" TargetFileName="Features\Feature1\Feature1.feature">Feature1.feature</ProjectItem>  
          <ProjectItem ReplaceParameters="true" TargetFileName="Features\Feature1\Feature1.Template.xml">Feature1.template.xml</ProjectItem>  
          <ProjectItem ReplaceParameters="true" TargetFileName="Package\Package.package">Package.package</ProjectItem>  
          <ProjectItem ReplaceParameters="true" TargetFileName="Package\Package.Template.xml">Package.Template.xml</ProjectItem>  
          <ProjectItem ReplaceParameters="true" TargetFileName="Field1\SharePointProjectItem.spdata">SharePointProjectItem.spdata</ProjectItem>  
          <ProjectItem ReplaceParameters="true" TargetFileName="Field1\Elements.xml" OpenInEditor="true">Elements.xml</ProjectItem>  
          <ProjectItem ReplaceParameters="false" TargetFileName="key.snk">key.snk</ProjectItem>  
        </Project>  
      </TemplateContent>  
    </VSTemplate>  
    ```  
  
     O novo XML faz as seguintes alterações para o arquivo:  
  
    -   Conjuntos de `Name` elemento ao valor **coluna Site**. (Esse nome é exibido no **novo projeto** caixa de diálogo).  
  
    -   Adiciona `ProjectItem` elementos para cada filethat do incluídos em cada instância de projeto.  
  
    -   Usa o namespace "http://schemas.microsoft.com/developer/vstemplate/2005". Outros arquivos de projeto nesta solução usam o namespace de "http://schemas.microsoft.com/developer/msbuild/2003". Portanto, as mensagens de aviso de esquema XML serão geradas, mas você pode ignorá-los neste passo a passo.  
  
     Para obter mais informações sobre o conteúdo dos arquivos. vstemplate, consulte [referência de esquema de modelo do Visual Studio](/visualstudio/extensibility/visual-studio-template-schema-reference).  
  
2.  Salve e feche o arquivo.  
  
#### <a name="to-edit-the-projecttemplatecsproj-or-projecttemplatevbproj-file"></a>Para editar o arquivo ProjectTemplate.csproj ou ProjectTemplate.vbproj  
  
1.  No projeto SiteColumnProjectTemplate, substitua o conteúdo do arquivo ProjectTemplate.csproj ou ProjectTemplate.vbproj arquivo com uma das seções a seguir do XML.  
  
    -   Se você estiver criando um modelo de projeto do Visual c#, use o seguinte XML.  
  
    ```  
    <?xml version="1.0" encoding="utf-8"?>  
    <Project ToolsVersion="4.0" DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
      <PropertyGroup>  
        <Configuration Condition=" '$(Configuration)' == '' ">Debug</Configuration>  
        <Platform Condition=" '$(Platform)' == '' ">AnyCPU</Platform>  
        <SchemaVersion>2.0</SchemaVersion>  
        <ProjectGuid>{$guid1$}</ProjectGuid>  
        <OutputType>Library</OutputType>  
        <AppDesignerFolder>Properties</AppDesignerFolder>  
        <RootNamespace>$safeprojectname$</RootNamespace>  
        <AssemblyName>$safeprojectname$</AssemblyName>  
        <TargetFrameworkVersion>v3.5</TargetFrameworkVersion>  
        <FileAlignment>512</FileAlignment>  
        <ProjectTypeGuids>{BB1F664B-9266-4fd6-B973-E1E44974B511};{14822709-B5A1-4724-98CA-57A101D1B079};{FAE04EC0-301F-11D3-BF4B-00C04F79EFBC}</ProjectTypeGuids>  
      </PropertyGroup>  
      <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Debug|AnyCPU' ">  
        <DebugSymbols>true</DebugSymbols>  
        <DebugType>full</DebugType>  
        <Optimize>false</Optimize>  
        <OutputPath>bin\Debug\</OutputPath>  
        <DefineConstants>DEBUG;TRACE</DefineConstants>  
        <ErrorReport>prompt</ErrorReport>  
        <WarningLevel>4</WarningLevel>  
        <UseVSHostingProcess>false</UseVSHostingProcess>  
      </PropertyGroup>  
      <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Release|AnyCPU' ">  
        <DebugType>pdbonly</DebugType>  
        <Optimize>true</Optimize>  
        <OutputPath>bin\Release\</OutputPath>  
        <DefineConstants>TRACE</DefineConstants>  
        <ErrorReport>prompt</ErrorReport>  
        <WarningLevel>4</WarningLevel>  
      </PropertyGroup>  
      <PropertyGroup>  
        <SignAssembly>true</SignAssembly>  
        <AssemblyOriginatorKeyFile>key.snk</AssemblyOriginatorKeyFile>  
      </PropertyGroup>  
      <ItemGroup>  
        <Reference Include="System" />  
        <Reference Include="System.Core" />  
        <Reference Include="System.Data" />  
        <Reference Include="System.Data.DataSetExtensions" />  
        <Reference Include="System.Web" />  
        <Reference Include="System.Xml" />  
        <Reference Include="System.Xml.Linq" />  
        <Reference Include="Microsoft.SharePoint" />  
        <Reference Include="Microsoft.SharePoint.Security" />  
      </ItemGroup>  
      <ItemGroup>  
        <Compile Include="Properties\AssemblyInfo.cs" />  
      </ItemGroup>  
      <ItemGroup>  
        <None Include="Field1\SharePointProjectItem.spdata">  
          <SharePointProjectItemId>{$guid2$}</SharePointProjectItemId>  
        </None>  
        <None Include="Field1\Elements.xml" />  
      </ItemGroup>  
      <ItemGroup>  
        <None Include="key.snk" />  
        <None Include="Package\Package.package">  
          <PackageId>{$guid3$}</PackageId>  
        </None>  
        <None Include="Package\Package.Template.xml">  
          <DependentUpon>Package.package</DependentUpon>  
        </None>  
        <None Include="Features\Feature1\Feature1.feature">  
          <FeatureId>{$guid4$}</FeatureId>  
        </None>  
        <None Include="Features\Feature1\Feature1.Template.xml">  
          <DependentUpon>Feature1.feature</DependentUpon>  
        </None>  
      </ItemGroup>  
      <Import Project="$(MSBuildToolsPath)\Microsoft.CSharp.targets" />  
      <Import Project="$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v10.0\SharePointTools\Microsoft.VisualStudio.SharePoint.targets" />  
    </Project>  
    ```  
  
    1.  Se você estiver criando um modelo de projeto do Visual Basic, use o seguinte XML.  
  
    ```  
    <?xml version="1.0" encoding="utf-8"?>  
    <Project ToolsVersion="4.0" DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
      <PropertyGroup>  
        <Configuration Condition=" '$(Configuration)' == '' ">Debug</Configuration>  
        <Platform Condition=" '$(Platform)' == '' ">AnyCPU</Platform>  
        <ProductVersion>  
        </ProductVersion>  
        <SchemaVersion>  
        </SchemaVersion>  
        <ProjectGuid>{$guid1$}</ProjectGuid>  
        <OutputType>Library</OutputType>  
        <RootNamespace>$safeprojectname$</RootNamespace>  
        <AssemblyName>$safeprojectname$</AssemblyName>  
        <TargetFrameworkVersion>v3.5</TargetFrameworkVersion>  
        <FileAlignment>512</FileAlignment>  
        <ProjectTypeGuids>{BB1F664B-9266-4fd6-B973-E1E44974B511};{D59BE175-2ED0-4C54-BE3D-CDAA9F3214C8};{F184B08F-C81C-45F6-A57F-5ABD9991F28F}</ProjectTypeGuids>  
        <OptionExplicit>On</OptionExplicit>  
        <OptionCompare>Binary</OptionCompare>  
        <OptionStrict>Off</OptionStrict>  
        <OptionInfer>On</OptionInfer>  
      </PropertyGroup>  
      <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Debug|AnyCPU' ">  
        <DebugSymbols>true</DebugSymbols>  
        <DebugType>full</DebugType>  
        <DefineDebug>true</DefineDebug>  
        <DefineTrace>true</DefineTrace>  
        <OutputPath>bin\Debug\</OutputPath>  
        <WarningLevel>4</WarningLevel>  
        <UseVSHostingProcess>false</UseVSHostingProcess>  
      </PropertyGroup>  
      <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Release|AnyCPU' ">  
        <DebugType>pdbonly</DebugType>  
        <DefineDebug>false</DefineDebug>  
        <DefineTrace>true</DefineTrace>  
        <Optimize>true</Optimize>  
        <OutputPath>bin\Release\</OutputPath>  
        <UseVSHostingProcess>false</UseVSHostingProcess>  
      </PropertyGroup>  
      <PropertyGroup>  
        <SignAssembly>true</SignAssembly>  
        <AssemblyOriginatorKeyFile>key.snk</AssemblyOriginatorKeyFile>  
      </PropertyGroup>  
      <ItemGroup>  
        <Reference Include="System" />  
        <Reference Include="System.Core" />  
        <Reference Include="System.Data" />  
        <Reference Include="System.Data.DataSetExtensions" />  
        <Reference Include="System.Xml" />  
        <Reference Include="System.Xml.Linq" />  
        <Reference Include="Microsoft.SharePoint" />  
        <Reference Include="Microsoft.SharePoint.Security" />  
      </ItemGroup>  
      <ItemGroup>  
        <Import Include="Microsoft.VisualBasic" />  
        <Import Include="System" />  
        <Import Include="System.Collections" />  
        <Import Include="System.Collections.Generic" />  
        <Import Include="System.Data" />  
        <Import Include="System.Diagnostics" />  
        <Import Include="System.Linq" />  
        <Import Include="System.Xml.Linq" />  
        <Import Include="Microsoft.SharePoint" />  
        <Import Include="Microsoft.SharePoint.Security" />  
      </ItemGroup>  
      <ItemGroup>  
        <Compile Include="My Project\AssemblyInfo.vb" />  
      </ItemGroup>  
      <ItemGroup>  
        <AppDesigner Include="My Project\" />  
      </ItemGroup>  
      <ItemGroup>  
        <None Include="Features\Feature1\Feature1.feature">  
          <FeatureId>{$guid4$}</FeatureId>  
        </None>  
        <None Include="Field1\SharePointProjectItem.spdata">  
          <SharePointProjectItemId>{$guid2$}</SharePointProjectItemId>  
        </None>  
        <None Include="key.snk" />  
        <None Include="Package\Package.package">  
          <PackageId>{$guid3$}</PackageId>  
        </None>  
        <None Include="Package\Package.Template.xml">  
          <DependentUpon>Package.package</DependentUpon>  
        </None>  
      </ItemGroup>  
      <ItemGroup>  
        <None Include="Features\Feature1\Feature1.Template.xml">  
          <DependentUpon>Feature1.feature</DependentUpon>  
        </None>  
        <None Include="Field1\Elements.xml" />  
      </ItemGroup>  
      <Import Project="$(MSBuildToolsPath)\Microsoft.VisualBasic.targets" />  
      <Import Project="$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v10.0\SharePointTools\Microsoft.VisualStudio.SharePoint.targets" />  
    </Project>  
    ```  
  
     O novo XML faz as seguintes alterações para o arquivo:  
  
    -   Usa o `TargetFrameworkVersion` elemento para especificar o .NET Framework 3.5, não 4.5.  
  
    -   Adiciona `SignAssembly` e `AssemblyOriginatorKeyFile` elementos para assinar a saída do projeto.  
  
    -   Adiciona `Reference` elementos para o assembly faz referência a esse uso de projetos do SharePoint.  
  
    -   Adiciona os elementos para cada arquivo padrão do projeto, como Elements e SharePointProjectItem.spdata.  
  
2.  Salve e feche o arquivo.  
  
## <a name="creating-a-vsix-package-to-deploy-the-project-template"></a>Criando um pacote do VSIX para implantar o modelo de projeto  
 Para implantar a extensão, use o projeto do VSIX no **SiteColumnProjectItem** solução para criar um pacote do VSIX. Primeiro, configure o pacote VSIX, modificando o arquivo source.extension.vsixmanifest que está incluído no projeto do VSIX. Em seguida, crie o pacote do VSIX por compilar a solução.  
  
#### <a name="to-configure-and-create-the-vsix-package"></a>Para configurar e criar o pacote VSIX  
  
1.  Em **Solution Explorer**, no **SiteColumnProjectItem** de projeto, abra o arquivo source.extension.vsixmanifest no editor de manifesto.  
  
     O arquivo source.extension.vsixmanifest é a base para o arquivo extension.vsixmanifest que necessitam de todos os pacotes VSIX. Para obter mais informações sobre esse arquivo, consulte [1.0 referência do esquema de extensão de VSIX](http://msdn.microsoft.com/en-us/76e410ec-b1fb-4652-ac98-4a4c52e09a2b).  
  
2.  No **nome do produto** , digite **coluna Site**.  
  
3.  No **autor** , digite **Contoso**.  
  
4.  No **descrição** , digite **do SharePoint de um projeto para a criação de colunas de site**.  
  
5.  Escolha o **ativos** guia e, em seguida, escolha o **novo** botão.  
  
     O **adicionar novo ativo** caixa de diálogo é aberta.  
  
6.  No **tipo** , escolha **Microsoft.VisualStudio.ProjectTemplate**.  
  
    > [!NOTE]  
    >  Esse valor corresponde do `ProjectTemplate` elemento no arquivo extension.vsixmanifest. Este elemento identifica a subpasta no pacote do VSIX que contém o modelo de projeto. Para obter mais informações, consulte [ProjectTemplate Element (esquema de VSX)](http://msdn.microsoft.com/en-us/87add64c-9dcd-495f-8815-209dab182cb1).  
  
7.  No **fonte** , escolha **um projeto na solução atual**.  
  
8.  No **projeto** lista e escolha **SiteColumnProjectTemplate**e, em seguida, escolha o **Okey** botão.  
  
9. Escolha o **novo** novamente.  
  
     O **adicionar novo ativo** caixa de diálogo é aberta.  
  
10. No **tipo** , escolha **Microsoft.VisualStudio.MefComponent**.  
  
    > [!NOTE]  
    >  Esse valor corresponde do `MefComponent` elemento no arquivo extension.vsixmanifest. Este elemento Especifica o nome de um assembly de extensão do pacote VSIX. Para obter mais informações, consulte [MEFComponent Element (esquema de VSX)](http://msdn.microsoft.com/en-us/8a813141-8b73-44c9-b80b-ca85bbac9551).  
  
11. No **fonte** , escolha **um projeto na solução atual**.  
  
12. No **projeto** , escolha **ProjectItemTypeDefinition**e, em seguida, escolha o **Okey** botão.  
  
13. Na barra de menus, escolha **criar**, **compilar solução**e, em seguida, certifique-se de que o projeto é compilado sem erros.  
  
## <a name="testing-the-project-template"></a>O modelo de projeto de teste  
 Agora você está pronto para testar o modelo de projeto. Primeiro, inicie a depuração da solução SiteColumnProjectItem na instância experimental do Visual Studio. Em seguida, teste o **coluna Site** projeto na instância experimental do Visual Studio. Por fim, compilar e executar o projeto do SharePoint para verificar se a coluna de site funciona conforme o esperado.  
  
#### <a name="to-start-debugging-the-solution"></a>Para iniciar a depuração da solução  
  
1.  Reinicie o Visual Studio com credenciais administrativas e, em seguida, abra a solução de SiteColumnProjectItem.  
  
2.  
  
3.  No arquivo de código SiteColumnProjectItemTypeProvider, adicionar um ponto de interrupção para a primeira linha do código no `InitializeType` método e, em seguida, escolha o **F5** tecla para iniciar a depuração.  
  
     Visual Studio instala a extensão para %UserProfile%\AppData\Local\Microsoft\VisualStudio\10.0Exp\Extensions\Contoso\Site Column\1.0 e inicia uma instância experimental do Visual Studio. Você testará o item de projeto nesta instância do Visual Studio.  
  
#### <a name="to-test-the-project-in-visual-studio"></a>Para testar o projeto no Visual Studio  
  
1.  Na instância experimental do Visual Studio, na barra de menus, escolha **arquivo**, **novo**, **projeto**.  
  
2.  Expanda o **Visual C#** ou **Visual Basic** nó (dependendo da linguagem que dá suporte a seu modelo de projeto), expanda o **SharePoint** nó e, em seguida, escolha o **2010** nó.  
  
3.  Na lista de modelos de projeto, escolha o **coluna Site** modelo.  
  
4.  No **nome** , digite **SiteColumnTest** e, em seguida, escolha o **Okey** botão.  
  
     Em **Solution Explorer**, um novo projeto é exibido com um item de projeto chamado **Field1**.  
  
5.  Verifique se que o código em outra instância do Visual Studio para no ponto de interrupção que você definiu anteriormente no `InitializeType` método e, em seguida, escolha o **F5** tecla para continuar a depuração do projeto.  
  
6.  Em **Solution Explorer**, escolha o **Field1** nó e, em seguida, escolha o **F4** chave.  
  
     O **propriedades** janela será aberta.  
  
7.  Na lista de propriedades, verifique se a propriedade **exemplo de propriedade** é exibida.  
  
#### <a name="to-test-the-site-column-in-sharepoint"></a>Para testar a coluna de site do SharePoint  
  
1.  Em **Solution Explorer**, escolha o **SiteColumnTest** nó.  
  
2.  No **propriedades** janela, na caixa de texto próxima ao **URL do Site** propriedade, digite **http://localhost**.  
  
     Esta etapa Especifica o local do SharePoint no computador de desenvolvimento que você deseja usar para depuração.  
  
    > [!NOTE]  
    >  O **URL do Site** propriedade é vazia por padrão porque o modelo de projeto da coluna de Site não fornece um Assistente para coletar este valor quando o projeto é criado. Para saber como adicionar um assistente que solicita que o desenvolvedor esse valor e, em seguida, define essa propriedade no novo projeto, consulte [passo a passo: Criando um Item de projeto da coluna de Site com um modelo de projeto, parte 2](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md).  
  
3.  Pressione a tecla **F5**.  
  
     A coluna de site é empacotada e implantada no site do SharePoint que é especificado no **URL do Site** propriedade do projeto. O navegador da web abre a página padrão deste site.  
  
    > [!NOTE]  
    >  Se o **desabilitado de depuração de Script** caixa de diálogo for exibida, escolha o **Sim** botão para continuar a depuração do projeto.  
  
4.  Sobre o **ações do Site** menu, escolha **configurações do Site**.  
  
5.  No **configurações de Site** página no **galerias** , escolha o **Site colunas** link.  
  
6.  Na lista de colunas de site, verifique se um **colunas personalizadas** grupo contém uma coluna denominada **SiteColumnTest**.  
  
7.  Feche o navegador da Web.  
  
## <a name="cleaning-up-the-development-computer"></a>Limpando o computador de desenvolvimento  
 Depois de concluir o teste do projeto, remova o modelo de projeto da instância experimental do Visual Studio.  
  
#### <a name="to-clean-up-the-development-computer"></a>Para limpar o computador de desenvolvimento  
  
1.  Na instância experimental do Visual Studio, na barra de menus, escolha **ferramentas**, **extensões e atualizações**.  
  
     A caixa de diálogo **Extensões e Atualizações** é aberta.  
  
2.  Na lista de extensões, escolha o **coluna Site** extensão e, em seguida, escolha o **desinstalação** botão.  
  
3.  Na caixa de diálogo que aparece, escolha o **Sim** botão para confirmar que você deseja desinstalar a extensão.  
  
4.  Escolha o **fechar** botão para concluir a desinstalação.  
  
5.  Feche ambas as instâncias do Visual Studio (a instância experimental e a instância do Visual Studio, em que a solução SiteColumnProjectItem estiver aberta).  
  
## <a name="next-steps"></a>Próximas etapas  
 Depois de concluir este passo a passo, você pode adicionar um Assistente para o modelo de projeto. Quando um usuário cria um projeto de coluna de Site, o assistente solicita que o usuário para a URL do site a ser usado para depuração e se a nova solução está em modo seguro e o assistente configura o novo projeto com essas informações. O assistente também coleta informações sobre a coluna (como o tipo de base e o grupo no qual a lista a coluna na Galeria de coluna de site) e adiciona informações ao arquivo Elements no novo projeto. Para obter mais informações, consulte [passo a passo: Criando um Item de projeto da coluna de Site com um modelo de projeto, parte 2](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md).  
  
## <a name="see-also"></a>Consulte também  
 [Passo a passo: Criando um Item de projeto da coluna de Site com um modelo de projeto, parte 2](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)   
 [Definindo tipos de Item de projeto do SharePoint personalizado](../sharepoint/defining-custom-sharepoint-project-item-types.md)   
 [Criando modelos de projeto e modelos de Item para itens de projeto do SharePoint](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)   
 [Salvando dados em extensões do sistema de projeto do SharePoint](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)   
 [Associando dados personalizados a extensões de Ferramentas do SharePoint](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)  
  
  