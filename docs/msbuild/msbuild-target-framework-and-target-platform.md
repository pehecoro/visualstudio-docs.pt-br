---
title: Estrutura de destino e plataforma de destino do MSBuild | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: msbuild
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: df6517c5-edd6-4cc4-97ad-b3cdfc78e799
caps.latest.revision: 
author: Mikejo5000
ms.author: mikejo
manager: ghogen
ms.workload:
- multiple
ms.openlocfilehash: d001e708553e2a4b0ed8ad9ae78eddf5e0b9a0a8
ms.sourcegitcommit: 205d15f4558315e585c67f33d5335d5b41d0fcea
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="msbuild-target-framework-and-target-platform"></a>Estrutura de destino e plataforma de destino do MSBuild
Um projeto pode ser compilado para executar tanto em uma *estrutura de destino*, que é uma versão específica do .NET Framework, quanto em uma *plataforma de destino*, que é uma arquitetura de software específico.  Por exemplo, você pode direcionar um aplicativo para execução no .NET Framework 2.0 em uma plataforma de 32 bits compatível com a família de processadores 802x86 ("x86"). A combinação de estrutura de destino e plataforma de destino é conhecida como o *contexto de destino*.  
  
## <a name="target-framework-and-profile"></a>Perfil e a estrutura de destino  
 Uma estrutura de destino é a versão específica do [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] no qual seu projeto é criado para ser executado. A especificação de uma estrutura de destino é necessária porque ela habilita funcionalidades do compilador e referências do assembly são exclusivas para essa versão da estrutura.  
  
 Atualmente, as seguintes versões do .NET Framework estão disponíveis para uso:  
  
-   O [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] 2.0 (incluído no Visual Studio 2005)  
  
-   O [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] 3.0 (incluído no [!INCLUDE[wiprlhext](../debugger/includes/wiprlhext_md.md)])  
  
-   O [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] 3.5 (incluído no [!INCLUDE[vs_orcas_long](../debugger/includes/vs_orcas_long_md.md)])  
  
-   O [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] 4 (incluído no Visual Studio 2010)  
  
-   O [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] 4.5 (incluído no [!INCLUDE[vs_dev11_long](../data-tools/includes/vs_dev11_long_md.md)])  
  
-   O [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] 4.5.1 (incluído no [!INCLUDE[vs_dev12](../extensibility/includes/vs_dev12_md.md)])  
  
-   O [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] 4.5.2  
  
-   O [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] 4.6 (incluído no [!INCLUDE[vs_dev14](../misc/includes/vs_dev14_md.md)])  
  
 As versões do .NET Framework são diferentes entre si na lista de assemblies que cada uma torna disponível para fazer referência. Por exemplo, você não pode compilar aplicativos Windows Presentation Foundation (WPF) a menos que seu projeto seja direcionado para o .NET Framework versão 3.0 ou superior.  
  
 A estrutura de destino é especificada na propriedade `TargetFrameworkVersion` no arquivo de projeto. Você pode alterar a estrutura de destino para um projeto usando as páginas de propriedades do projeto no IDE (ambiente de desenvolvimento integrado) do Visual Studio. Para obter mais informações, consulte [Como definir uma versão do .NET Framework como destino](../ide/how-to-target-a-version-of-the-dotnet-framework.md). Os valores disponíveis para `TargetFrameworkVersion` são `v2.0`, `v3.0`, `v3.5`, `v4.0`, `v4.5`, `v4.5.1`, `v4.5.2` e `v4.6`.  
  
```xml  
<TargetFrameworkVersion>v4.0</TargetFrameworkVersion>  
```  
  
 Um *perfil de destino* é um subconjunto de uma estrutura de destino. Por exemplo, o .NET Framework 4 Client Profile não inclui referências aos assemblies do MSBuild.  
  
 O perfil de destino é especificada na propriedade `TargetFrameworkProfile` em um arquivo de projeto. Você pode alterar o perfil de destino usando o controle de estrutura de destino nas páginas de propriedades do projeto no IDE. Para obter mais informações, consulte [Como definir uma versão do .NET Framework como destino](../ide/how-to-target-a-version-of-the-dotnet-framework.md).  
  
```xml  
<TargetFrameworkVersion>v4.0</TargetFrameworkVersion>  
<TargetFrameworkProfile>Client</TargetFrameworkProfile>  
```  
  
## <a name="target-platform"></a>Plataforma de Destino  
 A *plataforma* é a combinação de hardware e software que define um ambiente de tempo de execução específico. Por exemplo,  
  
-   `x86` designa um sistema operacional Windows de 32 bits em execução em um processador Intel 80x86 ou equivalente.  
  
-   `Xbox` designa a plataforma Microsoft Xbox 360.  
  
 Uma *plataforma de destino* é a plataforma específica na qual seu projeto é criado para ser executado. A plataforma de destino é especificada na propriedade de build `Platform` em um arquivo de projeto. Você pode alterar a plataforma de destino usando as páginas de propriedades do projeto ou **Gerenciador de Configurações** no IDE.  
  
```xml  
<PropertyGroup>  
   <Platform>x86</Platform>  
</PropertyGroup>  
  
```  
  
 Uma *configuração de destino* é um subconjunto de uma plataforma de destino. Por exemplo, a configuração `x86``Debug` não inclui a maioria das otimizações de código. A configuração de destino é especificada na propriedade de build `Configuration` em um arquivo de projeto. Você pode alterar a configuração de destino usando as páginas de propriedades do projeto ou **Gerenciador de Configurações**.  
  
```xml  
<PropertyGroup>  
   <Platform>x86</Platform>  
   <Configuration>Debug</Configuration>  
<PropertyGroup>  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Multiplataforma](../msbuild/msbuild-multitargeting-overview.md)