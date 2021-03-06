---
title: Estender seu DSL usando MEF | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.topic: article
author: gewarren
ms.author: gewarren
manager: ghogen
ms.workload:
- multiple
ms.technology: vs-ide-modeling
ms.openlocfilehash: 735de60d18bc5cbca7dc2ba509372d81622038be
ms.sourcegitcommit: 205d15f4558315e585c67f33d5335d5b41d0fcea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="extend-your-dsl-by-using-mef"></a>Estender a DSL usando MEF
Você pode estender sua linguagem específica de domínio (DSL) usando o Managed Extensibility Framework (MEF). Você ou outros desenvolvedores poderão gravar extensões para o DSL sem alterar a definição de DSL e o código do programa. Essas extensões incluem comandos de menu, manipuladores de arrastar e soltar e validação. Os usuários poderão instalar o DSL e opcionalmente instalar extensões para ele.  
  
 Além disso, quando você habilita o MEF em seu DSL, é mais fácil para que você escreva alguns dos recursos do seu DSL, mesmo se eles são criados junto com o DSL.  
  
 Para obter mais informações sobre o MEF, consulte [Managed Extensibility Framework (MEF)](/dotnet/framework/mef/index).  
  
### <a name="to-enable-your-dsl-to-be-extended-by-mef"></a>Para habilitar o DSL a ser estendido por MEF  
  
1.  Criar uma nova pasta chamada **MefExtension** dentro de **DslPackage** projeto. Adicione os seguintes arquivos para ele:  
  
     Nome do arquivo:`CommandExtensionVSCT.tt`  
  
    > [!IMPORTANT]
    >  O GUID do conjunto de neste arquivo para ser o mesmo que o CommandSetId de GUID que é definido em DslPackage\GeneratedCode\Constants.tt  
  
    ```  
    <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>  
    <#  
    // CmdSet Guid must be defined before master template is included  
    // This Guid must be kept synchronized with the CommandSetId Guid in Constants.tt  
    Guid guidCmdSet = new Guid ("00000000-0000-0000-0000-000000000000");  
    string menuidCommandsExtensionBaseId="0x4000";  
    #>  
    <#@ include file="DslPackage\CommandExtensionVSCT.tt" #>  
    ```  
  
     Nome do arquivo:`CommandExtensionRegistrar.tt`  
  
    ```  
    <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>  
    <#@ include file="DslPackage\CommandExtensionRegistrar.tt" #>  
    ```  
  
     Nome do arquivo:`ValidationExtensionEnablement.tt`  
  
    ```  
    <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>  
    <#@ include file="DslPackage\ValidationExtensionEnablement.tt" #>  
    ```  
  
     Nome do arquivo:`ValidationExtensionRegistrar.tt`  
  
     Se você adicionar esse arquivo, você deve habilitar a validação em seu DSL usando pelo menos uma das opções na **EditorValidation** no Gerenciador de DSL.  
  
    ```  
    <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>  
    <#@ include file="DslPackage\ValidationExtensionRegistrar.tt" #>  
    ```  
  
     Nome do arquivo:`PackageExtensionEnablement.tt`  
  
    ```  
    <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>  
    <#@ include file="DslPackage\PackageExtensionEnablement.tt" #>  
    ```  
  
2.  Criar uma nova pasta chamada **MefExtension** dentro de **Dsl** projeto. Adicione os seguintes arquivos para ele:  
  
     Nome do arquivo:`DesignerExtensionMetaDataAttribute.tt`  
  
    ```  
    <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>  
    <#@ include file="Dsl\DesignerExtensionMetadataAttribute.tt" #>  
    ```  
  
     Nome do arquivo:`GestureExtensionEnablement.tt`  
  
    ```  
    <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>  
    <#@ include file="Dsl\GestureExtensionEnablement.tt" #>  
    ```  
  
     Nome do arquivo:`GestureExtensionController.tt`  
  
    ```  
    <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>  
    <#@ include file="Dsl\GestureExtensionController.tt" #>  
    ```  
  
3.  Adicione a seguinte linha ao arquivo existente denominada **DslPackage\Commands.vsct**:  
  
    ```  
    <Include href="MefExtension\CommandExtensionVSCT.vsct"/>  
    ```  
  
     Inserir a linha após existente `<Include>` diretiva.  
  
4.  `Open DslDefinition.dsl.`  
  
5.  No Explorador de DSL, selecione **Editor\Validation**.  
  
6.  Na janela Propriedades, certifique-se de que pelo menos uma das propriedades nomeadas **usa...**  é `true`.  
  
7.  Na barra de ferramentas do Gerenciador de soluções, clique em **transformar todos os modelos de**.  
  
     Arquivos da subsidiária aparecem abaixo de cada um dos arquivos que você adicionou.  
  
8.  Compilar e executar a solução para verificar se ele ainda está funcionando.  
  
 O DSL agora está habilitado para MEF. Você pode gravar comandos de menu, manipuladores de gestos e restrições de validação como extensões MEF. Você pode escrever essas extensões em sua solução DSL junto com outros códigos personalizados. Além disso, você ou outros desenvolvedores podem gravar separada [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] extensões que estendem sua DSL.  
  
## <a name="creating-an-extension-for-a-mef-enabled-dsl"></a>Criando uma extensão para uma DSL MEF habilitado  
 Se você tem acesso a uma DSL habilitado MEF criado por você ou outra pessoa, você pode escrever extensões para ele. As extensões podem ser usadas para adicionar comandos de menu, manipuladores de gestos ou restrições de validação. Para criar essas extensões, você deve usar um [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] solução de extensão (VSIX). A solução tem duas partes: um projeto de biblioteca de classe que cria o assembly de código e um projeto do VSIX que empacota o assembly.  
  
#### <a name="to-create-a-dsl-extension-vsix"></a>Para criar uma extensão DSL VSIX  
  
1.  Crie um novo projeto de biblioteca de classe. Para fazer isso, no **novo projeto** caixa de diálogo, selecione **Visual Basic** ou **Visual C#** e, em seguida, selecione **biblioteca de classes**.  
  
2.  No novo projeto de biblioteca de classe, adicione uma referência ao assembly de DSL.  
  
    -   Este assembly geralmente tem um nome que termina com ". DSL.dll".  
  
    -   Se você tiver acesso ao projeto DSL, você pode encontrar o arquivo de assembly no diretório do **Dsl\bin\\\***  
  
    -   Se você tiver acesso ao arquivo VSIX DSL, você pode encontrar o assembly, alterando a extensão de nome de arquivo do arquivo VSIX para. zip". Descompacte o arquivo. zip.  
  
3.  Adicione referências aos assemblies do .NET a seguir:  
  
    -   Microsoft.VisualStudio.Modeling.Sdk.11.0.dll  
  
    -   Microsoft.VisualStudio.Modeling.Sdk.Diagrams.11.0.dll  
  
    -   Microsoft.VisualStudio.Modeling.Sdk.Shell.11.0.dll  
  
    -   System.ComponentModel.Composition.dll  
  
    -   System.Windows.Forms.dll  
  
4.  Crie um projeto do VSIX na mesma solução. Para fazer isso, no **novo projeto** caixa de diálogo caixa, expanda **Visual Basic** ou **Visual C#**, clique em **extensibilidade**e, em seguida, selecione  **Projeto VSIX**.  
  
5.  No Gerenciador de soluções, clique com botão direito do projeto VSIX e, em seguida, clique em **definir como projeto de inicialização**.  
  
6.  No novo projeto, abra **source.extension.vsixmanifest**.  
  
7.  Clique em **adicionar conteúdo**. Na caixa de diálogo, defina **tipo de conteúdo** para **MEF componente**, e **projeto de origem** ao seu projeto de biblioteca de classe.  
  
8.  Adicione uma referência VSIX ao DSL.  
  
    1.  Em **source.extension.vsixmanifest**, clique em **adicionar referência**  
  
    2.  Na caixa de diálogo, clique em **adicionar carga** e, em seguida, localize o arquivo VSIX de DSL. O arquivo VSIX é criado na solução DSL, em **DslPackage\bin\\\***.  
  
         Isso permite que os usuários a instalar o DSL e sua extensão ao mesmo tempo. Se o usuário já tiver instalado o DSL, somente sua extensão será instalado.  
  
9. Revisar e atualizar os outros campos de **source.extension.vsixmanifest**. Clique em **selecione edições** e verifique o correto [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] edições são definidas.  
  
10. Adicione código ao projeto de biblioteca de classe. Use os exemplos na próxima seção como um guia.  
  
     Você pode adicionar qualquer número de classes de validação, gesto e comando.  
  
11. Para testar a extensão, pressione **F5**. Na instância experimental do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)], crie ou abra um arquivo de exemplo de DSL.  
  
## <a name="writing-mef-extensions-for-dsls"></a>Escrevendo extensões MEF para DSLs  
 Você pode escrever extensões no projeto de código de assembly de uma solução de extensão DSL separado. Você também pode usar MEF em seu projeto DslPackage, como uma maneira conveniente de escrever código de validação, comandos e gestos como parte de DSL.  
  
### <a name="menu-commands"></a>Comandos de menu  
 Para escrever um comando de menu, definir uma classe que implementa <xref:Microsoft.VisualStudio.Modeling.ExtensionEnablement.ICommandExtension> e a classe com o atributo que é definido em seu DSL, chamado de prefixo *YourDsl*`CommandExtension`. Você pode gravar mais de uma classe de comando de menu.  
  
 `QueryStatus()`é chamado sempre que o usuário clica o diagrama. Ele deve inspecionar a seleção atual e definir `command.Enabled` para indicar quando o comando é aplicável.  
  
```  
using System.ComponentModel.Composition;  
using System.Linq;  
using Company.MyDsl; // My DSL  
using Company.MyDsl.ExtensionEnablement; // My DSL  
using Microsoft.VisualStudio.Modeling; // Transactions  
using Microsoft.VisualStudio.Modeling.Diagrams.ExtensionEnablement; // IVsSelectionContext  
using Microsoft.VisualStudio.Modeling.ExtensionEnablement; // ICommandExtension  
  
namespace MyMefExtension  
{  
  // Defined in Dsl\MefExtension\DesignerExtensionMetaDataAttribute.cs:  
  [MyDslCommandExtension]   
  public class MyCommandClass : ICommandExtension  
  {   
    /// <summary>  
    /// Provides access to current document and selection.  
    /// </summary>  
    [Import]  
    IVsSelectionContext SelectionContext { get; set; }  
  
    /// <summary>  
    /// Called when the user selects this command.  
    /// </summary>  
    /// <param name="command"></param>  
    public void Execute(IMenuCommand command)  
    {  
      // Transaction is required if you want to update elements.  
      using (Transaction t = SelectionContext.CurrentStore  
              .TransactionManager.BeginTransaction("fix names"))  
      {  
        foreach (ExampleShape shape in SelectionContext.CurrentSelection)  
        {  
          ExampleElement element = shape.ModelElement as ExampleElement;  
          element.Name = element.Name + " !";  
        }  
        t.Commit();  
      }  
    }  
  
    /// <summary>  
    /// Called when the user right-clicks the diagram.  
    /// Determines whether the command should appear.  
    /// This method should set command.Enabled and command.Visible.  
    /// </summary>  
    /// <param name="command"></param>  
    public void QueryStatus(IMenuCommand command)  
    {  
      command.Enabled =  
        command.Visible = (SelectionContext.CurrentSelection.OfType<ExampleShape>().Count() > 0);  
    }  
  
    /// <summary>  
    /// Called when the user right-clicks the diagram.  
    /// Determines the text of the command in the menu.  
    /// </summary>  
    public string Text  
    {  
      get { return "My menu command"; }  
    }  
  }  
}  
  
```  
  
### <a name="gesture-handlers"></a>Manipuladores de gesto  
 Um manipulador de gestos pode lidar com objetos arrastados para o diagrama de qualquer lugar, dentro ou fora de [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]. O exemplo a seguir permite que o usuário arraste os arquivos do Windows Explorer para o diagrama. Ele cria os elementos que contêm os nomes de arquivo.  
  
 Você pode escrever manipuladores para lidar com arrasta de outros modelos DSL e modelos UML. Para obter mais informações, consulte [como: adicionar um manipulador de arrastar e soltar](../modeling/how-to-add-a-drag-and-drop-handler.md).  
  
```  
  
using System.ComponentModel.Composition;  
using System.Linq;  
using Company.MyDsl;  
using Company.MyDsl.ExtensionEnablement;  
using Microsoft.VisualStudio.Modeling; // Transactions  
using Microsoft.VisualStudio.Modeling.Diagrams;  
using Microsoft.VisualStudio.Modeling.Diagrams.ExtensionEnablement;   
using Microsoft.VisualStudio.Modeling.ExtensionEnablement;   
  
namespace MefExtension  
{  
  [MyDslGestureExtension]  
  class MyGestureExtension : IGestureExtension  
  {  
    public void OnDoubleClick(ShapeElement targetElement, DiagramPointEventArgs diagramPointEventArgs)  
    {  
      System.Windows.Forms.MessageBox.Show("double click!");  
    }  
  
    /// <summary>  
    /// Called when the user drags anything over the diagram.  
    /// Return true if the dragged object can be dropped on the current target.  
    /// </summary>  
    /// <param name="targetMergeElement">The shape or diagram that the mouse is currently over</param>  
    /// <param name="diagramDragEventArgs">Data about the dragged element.</param>  
    /// <returns></returns>  
    public bool CanDragDrop(ShapeElement targetMergeElement, DiagramDragEventArgs diagramDragEventArgs)  
    {  
      // This handler only allows items to be dropped onto the diagram:  
      return targetMergeElement is MefDsl2Diagram &&  
      // And only accepts files dragged from Windows Explorer:  
        diagramDragEventArgs.Data.GetFormats().Contains("FileNameW");  
    }  
  
    /// <summary>  
    /// Called when the user drops an item onto the diagram.  
    /// </summary>  
    /// <param name="targetDropElement"></param>  
    /// <param name="diagramDragEventArgs"></param>  
    public void OnDragDrop(ShapeElement targetDropElement, DiagramDragEventArgs diagramDragEventArgs)  
    {  
      MefDsl2Diagram diagram = targetDropElement as MefDsl2Diagram;  
      if (diagram == null) return;  
  
      // This handler only accepts files dragged from Windows Explorer:  
      string[] draggedFileNames = diagramDragEventArgs.Data.GetData("FileNameW") as string[];  
      if (draggedFileNames == null || draggedFileNames.Length == 0) return;   
  
      using (Transaction t = diagram.Store.TransactionManager.BeginTransaction("file names"))  
      {  
        // Create an element to represent each file:  
        foreach (string fileName in draggedFileNames)  
        {  
          ExampleElement element = new ExampleElement(diagram.ModelElement.Partition);  
          element.Name = fileName;  
  
          // This method of adding the new element allows the position  
          // of the shape to be specified:            
          ElementGroup group = new ElementGroup(element);  
          diagram.ElementOperations.MergeElementGroupPrototype(  
            diagram, group.CreatePrototype(), PointD.ToPointF(diagramDragEventArgs.MousePosition));  
        }  
        t.Commit();  
      }  
    }  
  }  
}  
  
```  
  
### <a name="validation-constraints"></a>Restrições de validação  
 Métodos de validação são marcados pelo `ValidationExtension` atributo que é gerado pelo DSL e também pelo <xref:Microsoft.VisualStudio.Modeling.Validation.ValidationMethodAttribute>. O método pode aparecer em qualquer classe que não está marcado por um atributo.  
  
 Para obter mais informações, consulte [validação em uma linguagem específica do domínio](../modeling/validation-in-a-domain-specific-language.md).  
  
```  
using Company.MyDsl;  
using Company.MyDsl.ExtensionEnablement;  
using Microsoft.VisualStudio.Modeling.Validation;  
  
namespace MefExtension  
{  
  class MyValidationExtension // Can be any class.  
  {  
    // SAMPLE VALIDATION METHOD.  
    // All validation methods have the following attributes.  
  
    // Specific to the extended DSL:  
    [MyDslValidationExtension]   
  
    // Determines when validation is applied:  
    [ValidationMethod(  
       ValidationCategories.Save  
     | ValidationCategories.Open  
     | ValidationCategories.Menu)]  
  
    /// <summary>  
    /// When validation is executed, this method is invoked  
    /// for every element in the model that is an instance  
    /// of the second parameter type.  
    /// </summary>  
    /// <param name="context">For reporting errors</param>  
    /// <param name="elementToValidate"></param>  
    private void ValidateClassNames  
      (ValidationContext context,  
       // Type determines to what elements this will be applied:  
       ExampleElement elementToValidate)  
    {   
      // Write code here to test values and links.  
      if (elementToValidate.Name.IndexOf(' ') >= 0)  
      {  
        // Log any unacceptable values:  
        context.LogError(  
          // Description:  
          "Name must not contain spaces"   
          // Error code unique to this type of error:  
          , "MyDsl001"   
          // Element to highlight when user double-clicks error:  
          , elementToValidate);   
} } } }  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Envio de extensões do Visual Studio](../extensibility/shipping-visual-studio-extensions.md)   
 [Managed Extensibility Framework (MEF)](/dotnet/framework/mef/index)   
 [Como: adicionar um manipulador de arrastar e soltar](../modeling/how-to-add-a-drag-and-drop-handler.md)   
 [Validação em uma linguagem específica de domínio](../modeling/validation-in-a-domain-specific-language.md)