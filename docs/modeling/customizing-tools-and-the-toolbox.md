---
title: Personalizando as ferramentas e a caixa de ferramentas | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.topic: article
f1_keywords:
- vs.dsltools.dsldesigner.selectiondialog
- vs.dsltools.dsldesigner.selecticondialog
- vs.dsltools.dsldesigner.selectcursordialog
helpviewer_keywords:
- Domain-Specific Language, toolbox
author: gewarren
ms.author: gewarren
manager: ghogen
ms.workload:
- multiple
ms.technology: vs-ide-modeling
ms.openlocfilehash: 160c1c27ab9d01dc76d6a5c76feb07179f7966b9
ms.sourcegitcommit: 205d15f4558315e585c67f33d5335d5b41d0fcea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="customizing-tools-and-the-toolbox"></a>Personalizando ferramentas e a caixa de ferramentas
É necessário definir os itens da caixa de ferramentas para os elementos que deseja disponibilizar para os usuários adicionarem aos seus modelos. Há dois tipos de ferramentas: ferramentas de elemento e ferramentas de conexão. No designer gerado, um usuário pode selecionar uma ferramenta do elemento para arrastar formas para o diagrama e pode selecionar uma ferramenta de conexão para desenhar links entre as formas. Em geral, as ferramentas do elemento permitem aos usuários adicionarem instâncias de classe de domínio aos seus modelos e as ferramentas de conexão permitem que eles adicionem instâncias de relações de domínio.  
  
 Neste tópico:  
  
-   [Como a caixa de ferramentas está definida](#ToolboxDef)  
  
-   [Personalizando ferramentas de elemento](#customizing)  
  
-   [Criando grupos de elementos de uma ferramenta](#groups)  
  
-   [Personalizando as ferramentas de Conexão](#connections)  
  
##  <a name="ToolboxDef"></a>Como a caixa de ferramentas está definida  
 No DSL Explorer, expanda o nó do Editor e o nó abaixo dele. Geralmente aparecerá uma hierarquia que lembra isto:  
  
```  
  
Editor  
     Toobox Tabs  
        MyDsl          //a tab  
           Tools  
               ExampleElement      // an element tool  
               ExampleRelationship // a connection tool  
  
```  
  
 Nessa parte do DSL Explorer, é possível:  
  
-   Criar novas guias. As guias definem o cabeçalho da seção na caixa de ferramentas.  
  
-   Criar novas ferramentas.  
  
-   Copie e cole ferramentas.  
  
-   Mova as ferramentas para cima ou para baixo na lista.  
  
-   Exclua guias e ferramentas.  
  
> [!IMPORTANT]
>  Para adicionar ou colar itens em um DSL Explorer, clique com o botão direito no avô do novo nó. Por exemplo, para adicionar uma ferramenta, clique na guia e não o **ferramentas** nó. Para adicionar uma guia, clique com botão direito do **Editor** nó.  
  
 O **ícone caixa de ferramentas** propriedade de cada ferramenta faz referência a um arquivo de bitmap de 16 x 16. Normalmente, esses arquivos são mantidos no **Dsl\Resources** pasta.  
  
 O **classe** propriedade de uma ferramenta do elemento se refere a uma classe concreta do domínio. Por padrão, a ferramenta criará instâncias dessa classe. No entanto, é possível escrever um código para a ferramenta criar grupos de elementos ou elementos de diferentes tipos.  
  
 O **Conexão construtor** propriedade de uma ferramenta de conexão se refere a um construtor de conexão, que define os tipos de elementos a ferramenta pode se conectar e quais relações cria entre eles. Os construtores de conexão são definidos como nós no DSL Explorer. Construtores de conexão são criados automaticamente ao definir relações de domínio, mas é possível escrever códigos para personalizá-los.  
  
#### <a name="to-add-a-tool-to-the-toolbox"></a>Para adicionar uma ferramenta à caixa de ferramentas  
  
1.  Normalmente, uma ferramenta de elemento é criada depois de ter criado uma classe de forma e a ter mapeado em uma classe de domínio.  
  
     Normalmente, uma ferramenta de conector é criada depois de ter criado uma classe de conector e a ter mapeado em uma relação de referência.  
  
2.  No Explorador de DSL, expanda o **Editor** nó e o **guias da caixa de ferramentas** nó.  
  
     Clique em um nó de guia da caixa de ferramentas e clique **adicionar nova ferramenta de elemento** ou **adicionar nova ferramenta de Conexão**.  
  
3.  Definir o **ícone caixa de ferramentas** propriedade para se referir a um bitmap de 16 x 16.  
  
     Se você quiser definir um novo ícone, crie um arquivo de bitmap no Gerenciador de soluções no **Dsl\Resources** pasta. O arquivo deve ter os seguintes valores de propriedade: **ação de compilação** = **conteúdo**; **Copiar para diretório de saída** = **não copiar**.  
  
4.  **Para uma ferramenta de elemento:** definir o **classe** propriedade da ferramenta para fazer referência a uma classe concreta do domínio que é mapeada para uma forma.  
  
     **Uma ferramenta de conector:** definir o **Conexão construtor** propriedade da ferramenta para um dos itens que são oferecidos na lista suspensa. Os construtores de conexão são criados automaticamente ao mapear um conector para uma relação de domínio. Se tiver criado recentemente um conector, normalmente selecionaria o construtor de conexão associado.  
  
5.  Para testar o DSL, pressione F5 ou CTRL+F5 e na instância experimental de [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)], abra um arquivo de modelo de amostra. A nova ferramenta deve aparecer na caixa de ferramentas. Arraste-a para o diagrama para verificar se ela criou um novo elemento.  
  
     Se a ferramenta não aparecer, pare o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] experimental. Nas janelas **iniciar** menu, executar **redefinir a instância Microsoft Visual Studio 2010 Experimental**. Sobre o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] **criar** menu, clique em **recompilar solução**. Em seguida, teste o DSL novamente.  
  
##  <a name="customizing"></a>Personalizando as ferramentas do elemento  
 Por padrão, a ferramenta criará uma única instância da classe especificada, mas é possível variar isso de duas maneiras:  
  
-   Defina as Diretivas de Mescla de Elemento em outras classes, permitindo-lhes aceitar novas instâncias dessa classe e permitindo-lhes criar links adicionais quando o novo elemento é criado. Por exemplo, é possível permitir ao usuário soltar um Comentário em outro elemento, criando dessa maneira um link de referência entre os dois.  
  
     Essas personalizações também afetam o que ocorre quando o usuário cola ou arrasta e solta um elemento.  
  
     Para obter mais informações, consulte [Personalizando o elemento de criação e a movimentação](../modeling/customizing-element-creation-and-movement.md).  
  
-   Escreva um código para personalizar a ferramenta para que ela possa criar grupos de elementos. A ferramenta é inicializada por métodos no ToolboxHelper.cs que podem ser substituídos. Para obter mais informações, consulte [criando grupos de elementos de uma ferramenta](#groups).  
  
##  <a name="groups"></a>Criando grupos de elementos de uma ferramenta  
 Cada ferramenta do elemento contém um protótipo de elementos que ela deve criar. Por padrão, cada ferramenta do elemento cria um único elemento, mas também é possível criar um grupo de objetos relacionados a uma ferramenta. Para isso, é necessário inicializar a ferramenta com um <xref:Microsoft.VisualStudio.Modeling.ElementGroupPrototype> que contém os itens relacionados.  
  
 O exemplo a seguir é tomado de um DSL no qual há um Transistor de tipo. Cada Transistor possui três Terminais nomeados. A ferramenta do elemento dos Transistores armazena um protótipo contendo quatro elementos de modelo e três links de relacionamento. Quando o usuário arrasta a ferramenta no diagrama, o protótipo é instalado e conectado à raiz do modelo.  
  
 Esse código substitui um método que é definido em **Dsl\GeneratedCode\ToolboxHelper.cs**.  
  
 Para obter mais informações sobre como personalizar o modelo usando o código do programa, consulte [navegar e atualizar um modelo no código do programa](../modeling/navigating-and-updating-a-model-in-program-code.md).  
  
```  
using Microsoft.VisualStudio.Modeling;  
using Microsoft.VisualStudio.Modeling.Diagrams;  
  
  public partial class CircuitsToolboxHelper  
  {  
    /// <summary>  
    /// Toolbox initialization, called for each element tool on the toolbox.  
    /// This version deals with each Component subtype separately.  
    /// </summary>  
    /// <param name="store"></param>  
    /// <param name="domainClassId">Identifies the domain class this tool should instantiate.</param>  
    /// <returns>prototype of the object or group of objects to be created by tool</returns>  
    protected override ElementGroupPrototype CreateElementToolPrototype(Store store, Guid domainClassId)  
    {  
        if (domainClassId == Transistor.DomainClassId)  
        {  
            Transistor transistor = new Transistor(store);  
  
            transistor.Base = new ComponentTerminal(store);  
            transistor.Collector = new ComponentTerminal(store);  
            transistor.Emitter = new ComponentTerminal(store);  
  
            transistor.Base.Name = "base";  
            transistor.Collector.Name = "collector";  
            transistor.Emitter.Name = "emitter";  
  
            // Create an ElementGroup for the Toolbox.  
            ElementGroup elementGroup = new ElementGroup(store.DefaultPartition);  
            elementGroup.AddGraph(transistor, true);  
            // AddGraph includes the embedded parts  
  
            return elementGroup.CreatePrototype();  
        }  
        else  
        {  
            return base.CreateElementToolPrototype(store, domainClassId);  
}  }    }  
  
```  
  
##  <a name="connections"></a>Personalizando as ferramentas de Conexão  
 Normalmente, é criada uma ferramenta de elemento ao criar uma nova classe do conector. Como alternativa, é possível sobrecarregar uma ferramenta permitindo que os tipos das duas extremidades determinem o tipo de relação. Por exemplo, é possível definir uma ferramenta de conexão que poderia criar relações pessoa-pessoa e relações pessoa-cidade.  
  
 As ferramentas de conexão invocam os construtores de conexão. Use construtores de conexão para especificar como os usuários podem conectar elementos no designer gerado. Os construtores de conexão especificam os elementos que podem ser conectados e o tipo de link que é criada entre eles.  
  
 Ao criar uma relação de referência entre as classes de domínio, um construtor de conexão é criado automaticamente. É possível usar esse construtor de conexão ao mapear uma ferramenta de conexão. Para obter mais informações sobre como criar ferramentas de conexão, consulte [Configurando a caixa de ferramentas](../modeling/customizing-tools-and-the-toolbox.md).  
  
 É possível modificar o construtor de conexão padrão para que ele possa lidar com uma variedade de diferentes tipos de fonte e destino e criar diferentes tipos de relações.  
  
 Também é possível escrever códigos personalizados para os construtores de conexão especificarem as classes de fonte e de destino para a conexão, definir o tipo de conexão a ser feita e tomar outras ações associadas com a criação de uma conexão.  
  
### <a name="the-structure-of-connection-builders"></a>A estrutura dos construtores de conexão  
 Os construtores de conexão contêm um ou mais diretivas de conexão de link, que especificam a relação de domínio e os elementos de fonte e de destino. Por exemplo, no modelo de tarefa de fluxo de solução, você pode ver o **CommentReferencesSubjectsBuilder** no **DSL Explorer**. Este construtor de conexão contém um link conecte-se a diretiva chamada **CommentReferencesSubjects**, que é mapeado para a relação de domínio **CommentReferencesSubjects**. Essa diretiva de conexão de link contém uma diretiva da função de fonte que indica a classe de domínio `Comment` e uma diretiva de função de destino que indica a classe de domínio `FlowElement`.  
  
### <a name="using-connection-builders-to-restrict-source-and-target-roles"></a>Uso dos construtores de conexão para restringir as funções da fonte e do destino  
 É possível usar os construtores de conexão para restringir a ocorrência de determinadas classes na função de fonte ou de destino de uma determinada relação de domínio. Por exemplo, você pode ter uma classe de domínio de base que tenha uma relação de domínio com outra classe de domínio, mas pode não desejar que todas as classes derivadas da classe base tenham as mesmas funções nessa relação. A solução de fluxo de tarefas, há quatro classes concretas domínio (**StartPoint**, **ponto de extremidade**, **MergeBranch**, e **sincronização**) que herda diretamente da classe abstrata domínio **FlowElement**, e dois concreto classes de domínio (**tarefa** e **ObjectInState**) que herde indiretamente a partir dele. Também há um **fluxo** relação leva de referência **FlowElement** classes de domínio em sua função de origem e a função de destino. No entanto, uma instância de um **ponto de extremidade** classe de domínio não deve ser a origem de uma instância de um **fluxo** relação, nem deve a uma instância de um **StartPoint** classe ser o destino de uma instância de um **fluxo** relação. O **FlowBuilder** o construtor de conexão tem um link conecte-se a diretiva chamada **fluxo** que especifica quais classes de domínio podem executar a função de origem (**tarefa**,  **MergeBranch**, **StartPoint**, e **sincronização**) e que pode executar a função de destino (**MergeBranch**,  **Ponto de extremidade**, e **sincronização**).  
  
### <a name="connection-builders-with-multiple-link-connect-directives"></a>Construtores de conexão com diversas diretivas de conexão de link  
 É possível adicionar mais de uma diretiva de conexão de link a um construtor de conexão. Isso pode ajudar a ocultar algumas das complexidades do modelo de domínio de usuários e manter o **caixa de ferramentas** de ficando muito cheio. É possível adicionar diretivas de conexão de link de várias relações de domínio diferentes a um único construtor de conexão. No entanto, é necessário combinar as relações de domínio quando elas realizam aproximadamente a mesma função.  
  
 Na solução de fluxo de tarefas, o **fluxo** ferramenta de conexão é usada para desenhar instâncias de ambos o **fluxo** e **FluxoObjeto** relações de domínio. O **FlowBuilder** tem construtor de conexão, além do **fluxo** link conecte-se a diretiva descrita anteriormente, dois link conecte-se diretivas denominadas **FluxoObjeto**. Essas diretivas especificam que uma instância de um **FluxoObjeto** relação pode ser desenhada entre instâncias do **ObjectInState** classe de domínio ou de uma instância de um **ObjectInState**  a uma instância de um **tarefa**, mas não entre duas instâncias de um **tarefa**, ou de uma instância de um **tarefa** a uma instância de um **ObjectInState**. No entanto, uma instância de um **fluxo** relação pode ser desenhada entre duas instâncias de um **tarefa**. Se você compilar e executar a solução de fluxo de tarefa, você pode ver que desenho um **fluxo** de uma instância de um **ObjectInState** para uma instância de um **tarefa** cria uma instância de um **FluxoObjeto**, mas desenho uma **fluxo** entre duas instâncias de um **tarefa** cria uma instância de um **fluxo**.  
  
### <a name="custom-code-for-connection-builders"></a>Código personalizado para construtores de conexão  
 Existem quatro caixas de seleção na interface do usuário que definem diferentes tipos de personalização dos construtores de conexão:  
  
-   o **personalizado aceitar** caixa de seleção em uma diretiva de função de origem ou de destino  
  
-   o **de conexão personalizada** caixa de seleção em uma diretiva de função de origem ou de destino  
  
-   o **usa conectar personalizado** caixa de seleção em uma diretiva de conexão  
  
-   o **personalizado é** propriedade do construtor de conexão  
  
 É necessário fornecer algum código de programa para fazer essas personalizações. Para descobrir qual código é necessário fornecer, verifique uma dessas caixas, clique em Transformar Todos os Modelos e, em seguida, construa sua solução. O resultado será um relatório de erro. Clique duas vezes no relatório de erro para visualizar um comentário que explique qual código deve ser adicionado.  
  
> [!NOTE]
>  Para adicionar o código personalizado, crie uma definição de classe parcial em um arquivo de código separado dos arquivos de códigos nas pastas GeneratedCode. Para evitar a perda de seu trabalho, é necessário que os arquivos de códigos gerados não sejam editados. Para obter mais informações, consulte [substituir e estender as Classes geradas pelo](../modeling/overriding-and-extending-the-generated-classes.md).  
  
#### <a name="creating-custom-connection-code"></a>Criação de uma conexão personalizada  
 Em cada link de conectar-se a diretiva, o **diretivas de função de origem** guia define de que tipos que você podem arrastar. Da mesma forma, o **diretivas de função de destino** guia define para quais tipos, você podem arrastar. Para cada tipo, você pode especificar se deseja permitir a conexão (para esse link se conectar a diretiva) definindo o **personalizado aceitar** sinalizador e, em seguida, fornecendo o código extra.  
  
 Também é possível personalizar o que ocorre quando a conexão é feita. Por exemplo, é possível personalizar apenas o caso onde o arrasto ocorre para ou de uma determinada classe, todos os casos que um diretiva de conexão de link regula ou o construtor de conexão FlowBuilder todo. Para cada uma dessas opções, é possível ajustar sinalizadores personalizados no nível apropriado. Quando transformar todos os modelos e tentar compilar a solução, as mensagens de erro irão direcioná-lo para os comentários que estão no código gerado. Esses comentários identificam o que deve ser fornecido.  
  
 No exemplo de Diagrama de Componentes, o construtor de conexão da relação do domínio de Conexão é personalizado para restringir as conexões que podem ser feitas entre as portas. As ilustrações a seguir mostram que é possível fazer conexões somente a partir dos elementos da `OutPort` para os elementos `InPort`, mas é possível aninhar os componentes dentro uns aos outros.   
  
 **Conexão recebidas por um OutPort de um componente aninhado**  
  
 ![Construtor Conexão](../modeling/media/connectionbuilder_3.png "ConnectionBuilder_3")  
  
 Portanto, pode ser desejável especificar que uma conexão pode vir de um componente aninhado para uma OutPort. Para especificar tal uma conexão, defina **usa personalizado aceitar** no **InPort** tipo como função de origem e o **OutPort** tipo como função de destino no **DSL detalhes**  janela conforme mostrado nas ilustrações a seguir:  
  
 **Link conecte-se a diretiva no Explorer DSL**  
  
 ![Imagem do construtor de Conexão](../modeling/media/connectionbuilder_4a.png "ConnectionBuilder_4a")  
  
 **Link conecte-se a diretiva na janela de detalhes DSL**  
  
 ![](../modeling/media/connectionbuilder_4b.png "ConnectionBuilder_4b")  
  
 É necessário fornecer métodos na classe ConnectionBuilder:  
  
```  
  public partial class ConnectionBuilder  
  {  
    /// <summary>  
    /// OK if this component has children  
    /// </summary>  
    private static bool CanAcceptInPortAsSource(InPort candidate)  
    {  
       return candidate.Component.Children.Count > 0;  
    }  
  
    /// <summary>  
    /// Only if source is on parent of target.  
    /// </summary>  
    private static bool CanAcceptInPortAndInPortAsSourceAndTarget                (InPort sourceInPort, InPort targetInPort)  
    {  
      return sourceInPort.Component == targetInPort.Component.Parent;  
    }  
// And similar for OutPorts...  
```  
  
 Para obter mais informações sobre como personalizar o modelo usando o código do programa, consulte [navegar e atualizar um modelo no código do programa](../modeling/navigating-and-updating-a-model-in-program-code.md).  
  
 É possível usar códigos semelhantes, por exemplo, para impedir que os usuários criem loops com links pai-filho. Essas restrições são consideradas restrições 'rígidas', porque os usuários não podem violar a qualquer momento. Você também pode criar as verificações de validação 'suave' que os usuários podem ignorar temporariamente criando configurações inválidas que eles não é possível salvar.  
  
### <a name="good-practice-in-defining-connection-builders"></a>Boas práticas na definição dos construtores de conexão  
 É necessário definir um construtor de conexão para criar diferentes tipos de relações, apenas se elas estão relacionadas conceitualmente. No exemplo de fluxo de tarefas, é possível usar o mesmo construtor para criar fluxos entre tarefas e também entre tarefas e objetos. No entanto, seria confuso usar o mesmo construtor para criar relações entre tarefas e comentários.  
  
 Se um construtor de conexão for definido para vários tipos de relações, é necessário garantir que ele não possa corresponder a mais de um tipo do mesmo par de objetos de fonte e de destino. Caso contrário, os resultados seriam imprevisíveis.  
  
 Usar código personalizado para aplicar restrições 'rígidas', mas você deve considerar se os usuários devem poder temporariamente fazer conexões inválidas. Se o devem, é possível modificar as restrições para que as conexões não são validadas até que os usuários tentem salvar as alterações.  
  
## <a name="see-also"></a>Consulte também  
 [Personalizando a criação de elemento e de movimentação](../modeling/customizing-element-creation-and-movement.md)   
 [Personalizar o comportamento de cópia](../modeling/customizing-copy-behavior.md)   
 [Como: adicionar um manipulador de arrastar e soltar](../modeling/how-to-add-a-drag-and-drop-handler.md)   
 [Navegar e atualizar um modelo no código do programa](../modeling/navigating-and-updating-a-model-in-program-code.md)   
 [Exemplo de diagramas de circuito DSL](http://code.msdn.microsoft.com/Visualization-Modeling-SDK-763778e8)