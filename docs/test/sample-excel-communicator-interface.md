---
title: Interface de comunicador do Excel de amostra | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-devops-test
ms.tgt_pltfrm: 
ms.topic: article
ms.author: gewarren
manager: ghogen
ms.workload: multiple
author: gewarren
ms.openlocfilehash: dd7db85df6e63869550cea579a894defd7be39b2
ms.sourcegitcommit: 7ae502c5767a34dc35e760ff02032f4902c7c02b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2018
---
# <a name="sample-excel-communicator-interface"></a>Interface de comunicador do Excel de amostra
A interface `IExcelUICommunication` de amostra é usada no objeto `ExcelUICommunicator` no projeto `ExcelAddIn`.  
  
## <a name="iexceluicommunication-interface"></a>Interface IExcelUICommunication  
 Essa interface define os pontos de comunicação entre o `CodedUIExtension`, que é executado no processo de teste de IU codificado e o `ExcelCodedUIAddIn`, que é executado no processo [!INCLUDE[ofprexcel](../test/includes/ofprexcel_md.md)].  
  
 O assembly `ExcelCodedUIAddinHelper` tem uma classe `ExcelUICommunicator` que deriva dessa interface e usa o modelo de objeto do Excel para processar os métodos.  
  
 Alguns métodos obtém as informações solicitadas do Excel e, em seguida, criam e retornam uma das informações de objetos, como o objeto `CellInformation`.  
  
 Outros métodos usam um objeto de informações fornecidas, localizam o controle correspondente no Excel e realizam um processo no controle. Por exemplo, o método `ScrollIntoView` rola a Planilha para que a célula designada fique visível.  
  
## <a name="codeduiextensibilitysample-and-excelcodeduiaddinhelper-communication"></a>Comunicação CodedUIExtensibilitySample e ExcelCodedUIAddinHelper  
 O assembly `ExcelCodedUIAddinHelper` é executado no processo do Excel e tem a classe `UICommunicator` que implementa a interface `IExcelUITestCommunication` e obtém ou define as informações necessárias diretamente da interface do usuário do Excel.  
  
 O assembly `CodedUIExtensibilitySample` é executado no processo de teste de IU codificado do Visual Studio. Esse assembly tem a classe `Communicator` que abre um canal de comunicação remota do .NET e fornece uma propriedade `Instance` que usa a interface `IExcelUICommunication` para usar o objeto `UICommunicator` no assembly `ExcelCodedUIAddinHelper` para passar solicitações e objetos de informações, como um objeto `CellInformation` entre os dois assemblies.  
  
## <a name="see-also"></a>Consulte também  
 [Estendendo testes de IU codificados e gravações da ação para dar suporte ao Microsoft Excel](../test/extending-coded-ui-tests-and-action-recordings-to-support-microsoft-excel.md)   
 [Suplemento do Excel de amostra para testes de IU codificados](../test/sample-excel-add-in-for-coded-ui-testing.md)   
 [Extensão de teste de IU codificado de exemplo para Excel](../test/sample-coded-ui-test-extension-for-excel.md)
