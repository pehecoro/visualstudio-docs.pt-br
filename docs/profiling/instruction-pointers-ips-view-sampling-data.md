---
title: "Exibição de IPs (ponteiros de instrução) – Dados de amostragem | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-debug
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Instruction Pointers view
ms.assetid: c7f647bb-c5a3-4708-9f9d-33c0fd6e2e96
caps.latest.revision: "11"
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.workload: multiple
ms.openlocfilehash: 76081a3c5beb67693f2aef9fcdbeaed908619b8f
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="instruction-pointers-ips-view---sampling-data"></a>Exibição de IPs (ponteiros de instrução) – Dados de amostragem
A exibição de IPs dos dados de amostragem lista os dados de desempenho das instruções de assembly que estavam diretamente em execução quando as amostras foram coletadas na criação de perfil.  
  
> [!NOTE]
>  Os recursos de segurança aprimorados no Windows 8 e no Windows Server 2012 exigiram alterações significativas na maneira como o criador de perfil do Visual Studio coleta dados nessas plataformas. Os aplicativos UWP também requerem novas técnicas de coleta. Consulte [Ferramentas de desempenho em aplicativos do Windows 8 e do Windows Server 2012](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md).  
  
|Column|Descrição|  
|------------|-----------------|  
|**ID do Processo**|A ID de processo (PID) da criação de perfil.|  
|**Nome do Processo**|O nome do processo.|  
|**Nome do Módulo**|O nome do módulo que contém a instrução.|  
|**Caminho do Módulo**|O caminho do módulo que contém a instrução.|  
|**Arquivo de Origem**|O arquivo de origem que contém a instrução.|  
|**Nome da Função**|O nome da função que contém a instrução.|  
|**Número de linha da função**|O número de linha do início dessa função no arquivo de origem.|  
|**Endereço da Função**|O endereço de memória inicial da função no binário carregado.|  
|**Início da Linha de Origem**|O número de linha inicial no arquivo de origem em que esse exemplo foi coletado.|  
|**Final da Linha de Origem**|O número de linha final no arquivo de origem em que esse exemplo foi coletado.|  
|**Início do Caractere de Origem**|O deslocamento do caractere inicial na linha do arquivo de origem em que esse exemplo foi coletado.|  
|**Final do Caractere de Origem**|O deslocamento do caractere final na linha do arquivo de origem em que esse exemplo foi coletado.|  
|**Endereço da Instrução**|O endereço da instrução no binário carregado.|  
|**Amostras Exclusivas**|O número total de amostras coletadas durante a execução da instrução.|  
|**% de Amostras Exclusivas**|O percentual de todas as amostras coletadas na criação de perfil durante a execução da instrução.|  
  
## <a name="see-also"></a>Consulte também  
 [Exibição de IPs (ponteiros de instrução) – Amostragem](../profiling/instruction-pointers-ips-view-dotnet-memory-sampling-data.md)