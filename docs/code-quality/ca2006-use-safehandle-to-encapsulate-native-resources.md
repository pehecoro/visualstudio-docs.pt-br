---
title: 'CA2006: Use SafeHandle para encapsular recursos nativos | Microsoft Docs'
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-code-analysis
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- CA2006
- UseSafeHandleToEncapsulateNativeResources
helpviewer_keywords:
- UseSafeHandleToEncapsulateNativeResources
- CA2006
ms.assetid: a71950bd-bcc1-463d-b1f2-5233bc451456
caps.latest.revision: "16"
author: gewarren
ms.author: gewarren
manager: ghogen
ms.workload: cplusplus
ms.openlocfilehash: d70c453e502dd0a7f4eda2e9247dbc3ec3229ebe
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="ca2006-use-safehandle-to-encapsulate-native-resources"></a>CA2006: use SafeHandle para encapsular recursos nativos
|||  
|-|-|  
|NomeDoTipo|UseSafeHandleToEncapsulateNativeResources|  
|CheckId|CA2006|  
|Categoria|Microsoft.Reliability|  
|Alteração Significativa|Não recentes|  
  
## <a name="cause"></a>Causa  
 O código gerenciado usa <xref:System.IntPtr> para acessar recursos nativos.  
  
## <a name="rule-description"></a>Descrição da Regra  
 O uso de `IntPtr` em código gerenciado pode indicar um problema potencial de segurança e confiabilidade. Todos os usos de `IntPtr` devem ser revisadas para determinar se o uso de um <xref:System.Runtime.InteropServices.SafeHandle> , ou uma tecnologia semelhante, é necessário em seu lugar. Problemas ocorrerá se o `IntPtr` representa algum recurso nativo, como memória, um identificador de arquivo ou um soquete que o código gerenciado é considerado próprio. Se o código gerenciado possui o recurso, ele também deve liberar os recursos nativos associados a ele, porque uma falha ao fazer isso causaria o vazamento de recursos.  
  
 Nesses cenários, problemas de segurança ou confiabilidade também existirá se o acesso multithread é permitido para o `IntPtr` e uma maneira de liberar o recurso que é representado pelo `IntPtr` é fornecido. Esses problemas que envolvem a reciclagem do `IntPtr` valor na versão de recurso ao uso simultâneo de recurso está sendo feito em outro thread. Isso pode causar condições de corrida em que um thread pode ler ou gravar dados que está associados com o recurso incorreto. Por exemplo, se seu tipo armazena um identificador de sistema operacional como um `IntPtr` e permite que os usuários chamar **fechar** e qualquer outro método que usa esse identificador simultaneamente e sem algum tipo de sincronização, seu código tem uma alça de reciclagem problema.  
  
 Esse identificador de reciclagem problema pode causar corrupção de dados e, frequentemente, uma vulnerabilidade de segurança. `SafeHandle`e sua classe irmão <xref:System.Runtime.InteropServices.CriticalHandle> fornecem um mecanismo para encapsular um identificador nativo para um recurso para que esses problemas de threads podem ser evitados. Além disso, você pode usar `SafeHandle` e sua classe irmão `CriticalHandle` para outros threads problemas, por exemplo, para controlar cuidadosamente o tempo de vida de objetos gerenciados que contêm uma cópia do identificador nativo em chamadas para métodos nativos. Nessa situação, geralmente, você pode remover chamadas para `GC.KeepAlive`. O que sobrecarga de desempenho feitas quando você usar `SafeHandle` e, em um nível menor, `CriticalHandle`, com frequência pode ser reduzido com cuidado design.  
  
## <a name="how-to-fix-violations"></a>Como Corrigir Violações  
 Converter `IntPtr` uso `SafeHandle` para gerenciar o acesso aos recursos nativos com segurança. Consulte o <xref:System.Runtime.InteropServices.SafeHandle> tópico de referência para obter exemplos.  
  
## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos  
 Você não deve suprimir este aviso.  
  
## <a name="see-also"></a>Consulte também  
 <xref:System.IDisposable>