---
title: "Elemento de caixa de combinação | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Combos element (VSCT XML schema)
- VSCT XML schema elements, Combos
ms.assetid: 392e3063-f0a0-4130-9583-23bd2aa3fa36
caps.latest.revision: "11"
author: gregvanl
ms.author: gregvanl
manager: ghogen
ms.workload: vssdk
ms.openlocfilehash: 9980232a7927bf1ae2df9d5f6329a57a031d3f56
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="combo-element"></a>Elemento de caixa de combinação
Define os comandos que aparecem em uma caixa de combinação. Há quatro tipos de caixas de combinação, da seguinte maneira: DropDownCombo, DynamicCombo, IndexCombo e MRUCombo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
<combo guid="guidMyCommandSet" id="MyCommand" defaultWidth="20" idCommandList="MyCommandListID" priority="0x102" type="DropDownCombo">  
  <Parent>... </Parent  
  <CommandFlag>... </CommandFlag>  
  <Strings>... </Strings>  
</combo>  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  
 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|GUID|Necessário. GUID do identificador de comando GUID ID.|  
|id|Necessário. ID do identificador de comando GUID ID.|  
|defaultWidth|Necessário. Um inteiro que especifica a largura de pixel da caixa de combinação.|  
|idCommandList|Necessário. Uma ID que é enviada para o destino do comando ativo para recuperar a lista de itens a serem exibidos na caixa de combinação. A ID será no mesmo escopo GUID como o controle.|  
|priority|Opcional. Um valor numérico que especifica a prioridade.|  
|tipo|Opcional. Um valor enumerado que especifica o tipo de botão.<br /><br /> Se não especificado, usa o botão.<br /><br /> DropDownCombo<br /> O VSPackage é responsável por preencher o conteúdo desta caixa de combinação. O usuário não é possível digitar nada na caixa de texto nesse menu suspenso.<br /><br /> DynamicCombo<br /> O VSPackage é responsável por preencher o conteúdo dessa caixa de combinação. O usuário pode editar essa combinação e também selecionar itens nele.<br /><br /> IndexCombo<br /> O mesmo que DynamicCombo, exceto que ele gera o índice do item em vez de seu texto.<br /><br /> MRUCombo<br /> Preenchido pelo ambiente de desenvolvimento integrado (IDE) em nome o VSPackage.  O usuário pode editar nessa caixa de combinação. O IDE lembra-se até as último 16 entradas por caixa de combinação.<br /><br /> Quando o usuário seleciona algo na caixa de combinação ou insere algo novo, o IDE notifica o VSPackage apropriado.|  
|Condição|Opcional. Consulte [atributos condicionais](../extensibility/vsct-xml-schema-conditional-attributes.md).|  
  
### <a name="child-elements"></a>Elementos filho  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|Pai|Opcional. O elemento pai do botão.|  
|CommandFlag|Necessário. Consulte [comando sinalizador elemento](../extensibility/command-flag-element.md). Os valores válidos de CommandFlag para um botão são da seguinte maneira.<br /><br /> -CaseSensitive<br /><br /> -CommandWellOnly<br /><br /> -DefaultDisabled<br /><br /> -DefaultInvisible<br /><br /> -DynamicVisibility<br /><br /> -Filtragem<br /><br /> -IconAndText<br /><br /> -NoAutoComplete<br /><br /> -NoButtonCustomize<br /><br /> -NoCustomize<br /><br /> -NoKeyCustomize<br /><br /> -StretchHorizontally|  
|Cadeias de caracteres|Necessário. Consulte [cadeias de caracteres de elemento](../extensibility/strings-element.md). O elemento de ButtonText filho deve ser definido.|  
|Anotação|Comentário opcional.|  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[Elemento Commands](../extensibility/commands-element.md)|Representa a coleção de comandos na barra de ferramentas VSPackage.|  
  
## <a name="example"></a>Exemplo  
  
```  
<Combo guid="guidWidgetPackage" id="cmdidInsertOptions"  
  defaultWidth="100" idCommandList="cmdidGetInsertOptionsList">  
  <CommandFlag>DynamicVisibility</CommandFlag>  
  <Strings>  
    <ButtonText>Select Insert Options</ButtonText>  
  </Strings>  
</Combo>  
  
<Combo guid="guidWidgetPackage" id="cmdidInsertOptions"  
  priority="0x0500" type="DropDownCombo" defaultWidth="100"  
  idCommandList="cmdidGetInsertOptionsList">  
  <Parent guid="cmdSetGuidWidgetCommands" id="groupIDFileEdit">  
  <CommandFlag>DynamicVisibility</CommandFlag>  
  <Strings>  
    <ButtonText>Select Insert Options</ButtonText>  
  </Strings>  
</Combo>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Arquivos da tabela de comandos do Visual Studio (.Vsct)](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)