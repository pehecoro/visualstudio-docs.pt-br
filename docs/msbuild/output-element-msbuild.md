---
title: Elemento Output (MSBuild) | Microsoft Docs
ms.custom: 
ms.date: 03/13/2017
ms.reviewer: 
ms.suite: 
ms.technology: msbuild
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#Output
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- <Output> Element [MSBuild]
- Output Element [MSBuild]
ms.assetid: 34bc7cd1-efd3-4b57-b691-4584eeb6a0e9
caps.latest.revision: 
author: Mikejo5000
ms.author: mikejo
manager: ghogen
ms.workload:
- multiple
ms.openlocfilehash: 3836c4d4235831f705c9ebbf9252311153d6b44b
ms.sourcegitcommit: 205d15f4558315e585c67f33d5335d5b41d0fcea
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="output-element-msbuild"></a>Elemento Output (MSBuild)
Armazena valores de saída da tarefa em itens e propriedades.  

 \<Project>  
 \<Target>  
 \<Task>  
 \<Output>  

## <a name="syntax"></a>Sintaxe  

```  
<Output TaskParameter="Parameter"  
    PropertyName="PropertyName"   
    Condition = "'String A' == 'String B'" />  
```  

## <a name="attributes-and-elements"></a>Atributos e elementos  
 As seções a seguir descrevem atributos, elementos filho e elementos pai.  

### <a name="attributes"></a>Atributos  

|Atributo|Descrição|  
|---------------|-----------------|  
|`TaskParameter`|Atributo obrigatório.<br /><br /> O nome do parâmetro de saída da tarefa.|  
|`PropertyName`|O atributo `PropertyName` ou `ItemName` é necessário.<br /><br /> A propriedade que recebe o valor do parâmetro de saída da tarefa. Seu projeto pode fazer referência à propriedade com a sintaxe `$(`*PropertyName*`)`. Esse nome de propriedade pode ser um novo nome de propriedade ou um nome que já esteja definido no projeto.<br /><br /> Este atributo não poderá ser usado se `ItemName` também estiver sendo usado.|  
|`ItemName`|O atributo `PropertyName` ou `ItemName` é necessário.<br /><br /> O item que recebe o valor do parâmetro de saída da tarefa. Seu projeto pode fazer referência ao item com a sintaxe `@(`*ItemName*`)`. O nome do item pode ser um novo nome de item ou um nome que já esteja definido no projeto.<br /><br /> Este atributo não poderá ser usado se `PropertyName` também estiver sendo usado.|  
|`Condition`|Atributo opcional.<br /><br /> Condição a ser avaliada. Para obter mais informações, consulte [Condições](../msbuild/msbuild-conditions.md).|  

### <a name="child-elements"></a>Elementos filho  
 nenhuma.  

### <a name="parent-elements"></a>Elementos pai  

|Elemento|Descrição|  
|-------------|-----------------|  
|[Tarefa](../msbuild/task-element-msbuild.md)|Cria e executa uma instância de uma tarefa [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)].|  

## <a name="example"></a>Exemplo  
 O exemplo de código a seguir mostra uma tarefa `Csc` executada dentro de um elemento `Target`. Os itens e as propriedades passados para os parâmetros da tarefa são declarados fora do escopo deste exemplo. O valor do parâmetro de saída `OutputAssembly` é armazenado no item `FinalAssemblyName` e o valor do parâmetro de saída `BuildSucceeded` é armazenado na propriedade `BuildWorked`. Para obter mais informações, consulte [Tarefas](../msbuild/msbuild-tasks.md).  

```xml  
<Target Name="Compile" DependsOnTargets="Resources">  
    <Csc  Sources="@(CSFile)"  
            TargetType="library"  
            Resources="@(CompiledResources)"  
            EmitDebugInformation="$(includeDebugInformation)"  
            References="@(Reference)"  
            DebugType="$(debuggingType)"  
            OutputAssembly="$(builtdir)\$(MSBuildProjectName).dll" >  
        <Output TaskParameter="OutputAssembly"  
                  ItemName="FinalAssemblyName" />  
        <Output TaskParameter="BuildSucceeded"  
                  PropertyName="BuildWorked" />  
    </Csc>  
</Target>  
```  

## <a name="see-also"></a>Consulte também  
 [Referência do esquema de arquivos de projeto](../msbuild/msbuild-project-file-schema-reference.md)   
 [Tarefas](../msbuild/msbuild-tasks.md)
