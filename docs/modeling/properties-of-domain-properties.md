---
title: "As propriedades de domínio | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.topic: article
helpviewer_keywords:
- Domain-Specific Language, domain properties
author: gewarren
ms.author: gewarren
manager: ghogen
ms.workload:
- multiple
ms.technology: vs-ide-modeling
ms.openlocfilehash: 7d964eb9f0dcabdb8050074121d094245aca9bb7
ms.sourcegitcommit: 205d15f4558315e585c67f33d5335d5b41d0fcea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="properties-of-domain-properties"></a>Propriedades de propriedades de domínio
Um *propriedade domínio* é um recurso de um elemento de modelo que pode conter um valor. Por exemplo, a classe de domínio `Person` poderia ter as propriedades `Name` e `BirthDate`. Em Definição de DSL, as propriedades de domínio são listadas na caixa de classe de domínio no diagrama e sob a classe de domínio no Gerenciador de DSL. Para obter mais informações, consulte [como definir uma linguagem específica do domínio](../modeling/how-to-define-a-domain-specific-language.md).  
  
> [!NOTE]
>  A palavra "propriedade" possui dois usos. Um *propriedade domínio* é um recurso que você pode definir em uma classe de domínio. Por outro lado, muitos elementos de uma DSL têm *propriedades*, que são listados no **propriedades** janela na definição de DSL. Por exemplo, cada propriedade de domínio tem um conjunto de propriedades, que são descritas neste tópico.  
  
 No momento da execução, quando um usuário cria instâncias da classe de domínio, os valores das propriedades de domínio podem ser vistos na janela Propriedades e exibidos nas formas.  
  
 A maioria das propriedades de domínio é implementada como propriedades CLR comuns. No entanto, do ponto de vista da programação, as propriedades de domínio têm funcionalidade mais rica do que as propriedades de programa comuns:  
  
-   Você pode definir regras e eventos que monitoram o estado de uma propriedade. Para obter mais informações, consulte [respondendo a e propagando alterações](../modeling/responding-to-and-propagating-changes.md).  
  
-   As transações ajudam a impedir estados inconsistentes. Para obter mais informações, consulte [navegar e atualizar um modelo no código do programa](../modeling/navigating-and-updating-a-model-in-program-code.md).  
  
 Quando você seleciona uma Propriedade de Domínio em um diagrama ou no Gerenciador de DSL, pode ver os itens a seguir na janela Propriedades. Para obter mais informações sobre como usar esses itens, consulte [personalizar e estender uma linguagem específica do domínio](../modeling/customizing-and-extending-a-domain-specific-language.md).  
  
|Propriedade|Descrição|Valor padrão|  
|--------------|-----------------|-------------------|  
|**Descrição**|A descrição usada para documentar a interface do usuário (IU) do designer gerado.|\<none>|  
|**Nome de exibição**|O nome que será exibido no designer gerado para essa propriedade de domínio. Ele pode conter espaços e pontuação, por exemplo "Título da Música".|\<none>|  
|**Provedor de nomes de elemento**|Só será aplicável se você tiver configurado `Is Element Name` como `true`. Você pode escrever código que fornece um nome para um novo elemento de uma classe de domínio, substituindo o comportamento padrão.<br /><br /> Em um arquivo de código no projeto DSL, crie uma classe derivada de <xref:Microsoft.VisualStudio.Modeling.ElementNameProvider>.<br /><br /> Depois, no Gerenciador de DSL, clique com o botão direito do mouse na raiz do DSL e clique em Adicionar Tipo Externo. Insira o nome da sua classe.<br /><br /> Escolha essa propriedade de domínio novamente e escolha o nome da classe na lista suspensa.|\<none>|  
|**Modificador de acesso de getter**|O nível de acesso da classe de domínio (`public` ou `internal`). Controla o escopo no qual o código do programa pode acessar a propriedade.|`public`|  
|**Palavra-chave de ajuda**|A palavra-chave opcional usada para indexar a ajuda F1 desta propriedade de domínio.|\<none>|  
|**É navegável**|Se `True`, a propriedade de domínio será exibida para o usuário na janela de propriedades quando modelos deste DSL forem abertos.<br /><br /> Se `False`, a propriedade de domínio ficará oculta na interface do usuário.<br /><br /> Se você quiser tornar a propriedade de domínio visíveis, mas somente leitura, defina **é somente leitura da interface do usuário**.|`True`|  
|**É o nome do elemento**|Se `True`, esta propriedade de domínio será exibida como o nome do seu elemento modelo no Gerenciador de DSL.<br /><br /> Novos elementos do modelo receberão um valor padrão único para esta propriedade. Se você quiser controlar como esses valores são gerados, defina **provedor de nomes de elemento**.|`False`|  
|**Interface de usuário somente leitura**|Se `True`, o valor da propriedade de domínio não poderá ser alterada usando a IU. Ele ainda pode ser definido por programas e estará visível na janela Propriedades.<br /><br /> Se você deseja ocultar a propriedade de domínio do usuário, defina **é navegável**. Se você quiser controlar o acesso por programas, defina **modificador de acesso de Setter**.|`False`|  
|**Tipo**|O tipo da propriedade de domínio (`Normal`, `Calculated` ou `CustomStorage`). Para obter mais informações, consulte [calculado e as propriedades de armazenamento personalizado](../modeling/calculated-and-custom-storage-properties.md).|`Normal`|  
|**Nome**|O nome da propriedade do domínio. Ele deve ser um identificador válido, por exemplo **SongTitle**.|\<none>|  
|**Observações**|Notas informais associadas a esta propriedade de domínio.|\<none>|  
|**Modificador de acesso de setter**|O modificador de acesso do setter. Controla o escopo no qual o código do programa pode definir a propriedade.|`public`|  
|**Tipo**|O tipo de propriedade. Para adicionar à lista de tipos disponíveis, clique com botão direito a raiz de DSL no explorer DSL e clique em **Adicionar tipo externo**.|`String`|  
  
## <a name="see-also"></a>Consulte também  
 [Glossário de ferramentas de linguagem específica de domínio](http://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)