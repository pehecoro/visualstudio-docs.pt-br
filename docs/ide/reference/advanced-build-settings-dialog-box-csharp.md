---
title: "Caixa de diálogo Configurações de Build Avançadas (C#) | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- cs.AdvancedBuildSettings
helpviewer_keywords:
- Build options [C#], advanced
ms.assetid: 141f2dee-1563-4ce6-ba37-32920b082519
caps.latest.revision: 13
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
ms.sourcegitcommit: 5658ecf52637a38bc3c2a5ad9e85b2edebf7d445
ms.openlocfilehash: 82ec5d2db35da72beb017e15d1c271f751b5f56b
ms.lasthandoff: 02/22/2017

---
# <a name="advanced-build-settings-dialog-box-c"></a>Caixa de diálogo Configurações de Build Avançadas (C#)
Use a caixa de diálogo **Configurações de Build Avançadas** do **Designer de Projeto** para especificar as propriedades de configuração de build avançadas do projeto. Essa caixa de diálogo se aplica somente a projetos [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)].  
  
## <a name="general"></a>Geral  
 As opções a seguir permitem definir configurações gerais avançadas.  
  
 **Versão da Linguagem**  
 Especifica a versão da linguagem a ser usada. O conjunto de recursos é diferente em cada versão e, portanto, essa opção pode ser usada para forçar o compilador a permitir somente um subconjunto dos recursos implementados ou permitir somente os recursos compatíveis com um padrão existente. Essa configuração tem as seguintes opções:  
  
-   **ISO-1**  
  
     Tem como destino os recursos padrão ISO-1.  
  
-   **default**  
  
     Define a versão atual como destino.  
  
 Para obter mais informações, consulte [/langversion (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/langversion-compiler-option).  
  
 **Relatório de erros do compilador interno**  
 Especifica se os erros do compilador são relatados à Microsoft. Se for definido como **prompt** (o padrão), você receberá um prompt se ocorrer um erro interno do compilador, fornecendo a opção de enviar um relatório de erro eletronicamente à Microsoft. Se for definido como **send**, um relatório de erros será enviado automaticamente. Se for definido como **queue**, relatórios de erros serão colocados na fila. Se for definido como **none**, o erro será relatado somente na saída de texto do compilador. Para obter mais informações, consulte [/errorreport (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/errorreport-compiler-option).  
  
 **Verificar estouro/estouro negativo aritmético**  
 Especifica se uma instrução de aritmética de inteiros que não está no escopo das palavras-chave [marcadas](/dotnet/csharp/language-reference/keywords/checked) ou [desmarcadas](/dotnet/csharp/language-reference/keywords/unchecked) e que resulta em um valor fora do intervalo do tipo de dados causará uma exceção de tempo de execução. Para obter mais informações, consulte [/checked (opções do compilador do C#)](/dotnet/csharp/language-reference/compiler-options/checked-compiler-option).  
  
 **Não referenciar mscorlib.dll**  
 Especifica se mscorlib.dll será importado para o programa, definindo todo o namespace <xref:System>. Marque essa caixa se desejar definir ou criar seus próprios objetos e namespace <xref:System>. Para obter mais informações, consulte [/nostdlib (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/nostdlib-compiler-option).  
  
## <a name="output"></a>Saída  
 As opções a seguir permitem especificar opções de saída avançadas.  
  
 **Informações de Depuração**  
 Especifica o tipo de informações de depuração geradas pelo compilador. Para obter informações sobre como configurar o desempenho de depuração de um aplicativo, consulte [Facilitando a depuração de uma imagem](http://msdn.microsoft.com/Library/7d90ea7a-150f-4f97-98a7-f9c26541b9a3). Essa configuração tem as seguintes opções:  
  
-   **none**  
  
     Especifica que nenhuma informação de depuração será gerada  
  
-   **full**  
  
     Permite anexar um depurador ao programa em execução.  
  
-   **pdbonly**  
  
     Permite a depuração de código-fonte quando o programa é iniciado no depurador, mas apenas exibirá o assembler quando o programa em execução estiver anexado ao depurador.  
  
 Para obter mais informações, consulte [/debug (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/debug-compiler-option).  
  
 **Alinhamento de Arquivo**  
 Especifica o tamanho das seções no arquivo de saída. Os valores válidos são **512**, **1024**, **2048**, **4096** e **8192**. Esses valores são medidos em bytes. Cada seção será alinhada em um limite que é um múltiplo desse valor, afetando o tamanho do arquivo de saída. Para obter mais informações, consulte [/filealign (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/filealign-compiler-option).  
  
 **Endereço Básico de DLL**  
 Especifica o endereço básico preferencial no qual uma DLL será carregada. O endereço básico padrão para uma DLL é definido pelo Common Language Runtime de [!INCLUDE[dnprdnshort](../../code-quality/includes/dnprdnshort_md.md)]. Para obter mais informações, consulte [/baseaddress (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/baseaddress-compiler-option).  
  
## <a name="see-also"></a>Consulte também  
 [Opções do compilador do C#](/dotnet/csharp/language-reference/compiler-options/index)   
 [Página de Build, Designer de Projeto (C#)](../../ide/reference/build-page-project-designer-csharp.md)