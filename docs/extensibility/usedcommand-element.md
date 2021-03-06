---
title: Elemento UsedCommand | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- UsedCommands element (VSCT XML schema)
- VSCT XML schema elements, UsedCommands
ms.assetid: 99cd05d3-644a-42ff-b289-8458cd1b20c0
caps.latest.revision: "10"
author: gregvanl
ms.author: gregvanl
manager: ghogen
ms.workload: vssdk
ms.openlocfilehash: 06375b45e21e0b83c62f2509d666b786479ff2b4
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="usedcommand-element"></a>Elemento UsedCommand
Permite que um VSPackage acessar um comando que é definido em outro arquivo. VSCT. Por exemplo, se seu VSPackage usa o padrão de **cópia** comando, que é definido como o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] shell, você pode adicionar o comando a um menu ou barra de ferramentas sem implementá-lo novamente.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
<UsedCommand guid="guidMyCommandGroup" id="MyCommand" />  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  
 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|GUID|Necessário. O GUID do par de ID de GUID que identifica o comando.|  
|id|Necessário. A ID do par de ID de GUID que identifica o comando.|  
|Condição|Opcional. Consulte [atributos condicionais](../extensibility/vsct-xml-schema-conditional-attributes.md).|  
  
### <a name="child-elements"></a>Elementos filho  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|Nenhum||  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[Elemento UsedCommands](../extensibility/usedcommands-element.md)|Agrupa elementos de UsedCommand e outros UsedCommands agrupamentos.|  
  
## <a name="remarks"></a>Comentários  
 Adicionando um comando para o `<UsedCommands>` elemento, um VSPackage informa o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] que o VSPackage exige que o comando de ambiente. Você deve adicionar um `<UsedCommand>` elemento para qualquer comando que o pacote requer que não pode ser incluído em todas as versões e as configurações do Visual Studio. Por exemplo, se seu pacote chama um comando que é específico para o Visual C++, o comando não será disponibilizado para usuários do Visual Web Developer, a menos que você incluir um `<UsedCommand>` elemento para o comando.  
  
## <a name="example"></a>Exemplo  
  
```  
<UsedCommands>  
  <UsedCommand guid="guidVSStd97" id="cmdidCut"/>  
  <UsedCommand guid="guidVSStd97" id="cmdidCopy"/>  
  <UsedCommand guid="guidVSStd97" id="cmdidPaste"/>  
</UsedCommands>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Elemento UsedCommands](../extensibility/usedcommands-element.md)   
 [Arquivos da tabela de comandos do Visual Studio (.Vsct)](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)