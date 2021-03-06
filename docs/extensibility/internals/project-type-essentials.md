---
title: "Conceitos básicos do tipo de projeto | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: project types [Visual Studio SDK]
ms.assetid: 09991589-2300-430e-b6a4-7f2b95fe676f
caps.latest.revision: "11"
author: gregvanl
ms.author: gregvanl
manager: ghogen
ms.workload: vssdk
ms.openlocfilehash: 899d2758be1561d9b5fbda3280230333cc0ac8a3
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="project-type-essentials"></a>Conceitos básicos de tipo de projeto
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]inclui vários tipos de projeto para idiomas como [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] ou [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]. [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]também permite que você crie seus próprios tipos de projeto.  
  
 Se você quiser apenas para adicionar comandos personalizados, editores ou janelas de ferramentas para [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)], você pode fazer isso sem criar um novo tipo de projeto. Para mais informações, consulte os seguintes tópicos:  
  
-   [Comandos, menus e barras de ferramentas](../../extensibility/internals/commands-menus-and-toolbars.md)  
  
-   [Editor e extensões do serviço de linguagem](../../extensibility/editor-and-language-service-extensions.md)  
  
-   [Ampliar e personalizar janelas de ferramentas](../../extensibility/extending-and-customizing-tool-windows.md)  
  
 Da mesma forma, se você deseja personalizar o comportamento do fornecido [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] e [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] tipos de projeto, você pode fazer isso usando os subtipos de projeto. Para obter mais informações, consulte [subtipos de projeto](../../extensibility/internals/project-subtypes.md).  
  
 Você deve criar um novo tipo de projeto para projetos que são baseados em um idioma diferente de [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] e [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] se você deseja dar suporte a um ou mais dos seguintes:  
  
-   Build  
  
-   Implantação  
  
-   Várias configurações  
  
-   Controle do código-fonte  
  
-   Depuração  
  
-   Itens de projeto no Gerenciador de soluções  
  
-   O **Abrir projeto** ou **novo projeto** caixas de diálogo  
  
-   Aninhamento de projeto  
  
-   Para obter mais informações sobre os recursos de tipos de projetos, consulte o seguinte:  
  
-   Tipos de projeto são objetos em um VSPackage que implementam o conjunto de interfaces [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] espera. Se você estiver usando c# para desenvolver um tipo de projeto, as classes de projeto de estrutura de pacote gerenciado implementam as interfaces necessárias para você e permitem que você herdar dessa implementação. Para obter mais informações, consulte [usando a estrutura de pacote gerenciado para implementar um tipo de projeto (c#)](../../extensibility/internals/using-the-managed-package-framework-to-implement-a-project-type-csharp.md).  
  
-   Para os desenvolvedores do C++, as classes na biblioteca HierUtil funcionam de maneira semelhante. Para obter mais informações, consulte [não está em compilação: usando Classes de projeto HierUtil7 para implementar um tipo de projeto (C++)](http://msdn.microsoft.com/en-us/a5c16a09-94a2-46ef-87b5-35b815e2f346).  
  
-   Tipos de projeto podem dar suporte a dados diferentes de arquivos de código fonte típico que compila em um assembly .exe ou. dll. Por exemplo, [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] projetos de banco de dados contém referências aos arquivos de script e de consulta armazenados em disco e adicionar comandos a **Solution Explorer** para executar os scripts e consultas em um banco de dados, mas os projetos não oferecem suporte a Crie comportamento. Para obter mais informações, consulte [abrir e salvar itens de projeto](../../extensibility/internals/opening-and-saving-project-items.md).  
  
-   Não tem um tipo de projeto usar arquivos. Por exemplo, um tipo de projeto pode armazenar todos os seus dados em um banco de dados. [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]fornece controle completo sobre como eles mantêm dados de projetos e itens de projeto de tipos de projeto. Para obter mais informações, consulte [decisões de Design de tipo de projeto](../../extensibility/internals/project-type-design-decisions.md).  
  
-   Tipos de projeto devem fornecer um *fábrica de projeto*, que é um objeto que cria uma instância do projeto digite sempre que [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] é instruído a abrir ou criar um projeto com base nesse tipo de projeto. Para obter mais informações, consulte [criar projeto instâncias por usando fábricas de projeto](../../extensibility/internals/creating-project-instances-by-using-project-factories.md).  
  
-   Tipos de projeto devem fornecer modelos de projetos e itens de projeto. [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]usa os modelos quando os usuários criam novos projetos e adicionar novos itens a projetos existentes. Para obter mais informações, consulte [adicionando projeto e modelos de Item de projeto](../../extensibility/internals/adding-project-and-project-item-templates.md).  
  
-   Tipos de projeto podem dar suporte a várias configurações, como depuração e liberação. Os usuários podem alterar as configurações diferentes de um projeto por meio de páginas de propriedade que você fornecer. Para obter mais informações, consulte [gerenciar opções de configuração](../../extensibility/internals/managing-configuration-options.md).  
  
## <a name="see-also"></a>Consulte também  
 [Implantar tipos de projeto](../../extensibility/internals/deploying-project-types.md)