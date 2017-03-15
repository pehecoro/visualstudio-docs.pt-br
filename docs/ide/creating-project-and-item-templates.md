---
title: Criando modelos de projeto e de item | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- templates [Visual Studio], projects
- item templates, about item templates
- templates [Visual Studio], item
- Visual Studio templates, item
- Visual Studio templates, about templates
- project templates [Visual Studio], about project templates
- Visual Studio templates, project
- templates [Visual Studio], about templates
ms.assetid: a6ce501a-699b-4e3e-ade8-c81895645c20
caps.latest.revision: 9
author: kempb
ms.author: kempb
manager: ghogen
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: 5db97d19b1b823388a465bba15d057b30ff0b3ce
ms.openlocfilehash: a1bd01618f24637c608e82d5c23042c764fe1be8
ms.lasthandoff: 02/22/2017

---
# <a name="creating-project-and-item-templates"></a>Criando modelos de projeto e de item
Modelos de projeto e de item do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] fornecem stubs reutilizáveis que oferecem aos usuários uma estrutura e código básico que eles podem usar para suas próprias finalidades.  
  
## <a name="visual-studio-templates"></a>Modelos do Visual Studio  
 Alguns modelos de itens e de projetos predefinidos são instalados quando você instala o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]. Os modelos da Biblioteca de Classes e de Aplicativo do Windows Forms [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] e [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] disponíveis na caixa de diálogo **Novo Projeto** são exemplos de modelos de projeto. Os modelos de item instalados estão disponíveis na caixa de diálogo **Adicionar Novo Item** e incluem itens como arquivos de código, arquivos XML, páginas HTML e folhas de estilo.  
  
 Esses modelos fornecem um ponto de partida para que os usuários comecem a criar projetos ou expandam projetos atuais. Os modelos de projeto fornecem os arquivos que são necessários para um tipo de projeto específico, incluem referências de assembly padrão e definem opções de compilador e propriedades de projeto padrão. Os modelos de item podem variar em complexidade, de apenas um arquivo vazio que tem a extensão de nome de arquivo correta a um item com vários arquivos que contém, por exemplo, arquivos de código-fonte com código de stub, arquivos de informações do designer e recursos inseridos.  
  
 Além dos modelos instalados nas caixas de diálogo **Novo Projeto** e **Adicionar Novo Item**, você pode criar seus próprios modelos ou baixar e usar modelos criados pela comunidade. Para obter mais informações, consulte [Como criar modelos de projeto](../ide/how-to-create-project-templates.md) e [Como criar modelos de item](../ide/how-to-create-item-templates.md).  
  
## <a name="contents-of-a-template"></a>Conteúdo de um modelo  
 Todos os projetos de item e modelo, sejam eles instalados com o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ou criados por você, funcionam usando os mesmos princípios e têm conteúdo semelhante. Todos os modelos contêm os seguintes itens:  
  
-   Os arquivos a serem criados quando o modelo é usado. Isso inclui arquivos de código-fonte, recursos inseridos, arquivos de projeto e assim por diante.  
  
-   Um arquivo .vstemplate. Esse arquivo contém os metadados que fornecem ao [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] as informações necessárias para exibir o modelo nas caixas de seleção **Novo Projeto** e **Adicionar Novo Item** e criar um projeto ou item com base no modelo. Para obter mais informações sobre arquivos .vstemplate, consulte [Parâmetros de modelo](../ide/template-parameters.md).  
  
 Quando esses arquivos são compactados em um arquivo .zip e colocados na pasta correta, o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] os exibe automaticamente. Modelos de projeto aparecem na seção **Meus Modelos** da caixa de diálogo **Novo Projeto** e modelos de item são exibidos na caixa de diálogo **Adicionar Novo Item**. Para obter mais informações sobre as pastas de modelos, consulte [Como localizar e organizar modelos](../ide/how-to-locate-and-organize-project-and-item-templates.md).  
  
## <a name="starter-kits"></a>Kits de Início  
 Kits de início são modelos avançados que podem ser compartilhados com outros membros da comunidade. Um kit de início inclui exemplos de código que são compilados, documentação e outros recursos para ajudar os usuários a aprenderem novas ferramentas e técnicas de programação enquanto que compilam aplicativos úteis e reais. Os conteúdos e procedimentos básicos dos Kits de início são idênticos aos dos modelos. Para obter mais informações, consulte [Como criar kits de início](../ide/how-to-create-starter-kits.md).  
  
## <a name="see-also"></a>Consulte também  
 [Como criar modelos de projeto](../ide/how-to-create-project-templates.md)   
 [Como criar modelos de item](../ide/how-to-create-item-templates.md)   
 [Parâmetros de modelo](../ide/template-parameters.md)   
 [Personalizando modelos](../ide/customizing-project-and-item-templates.md)   
 [Como criar kits de início](../ide/how-to-create-starter-kits.md)