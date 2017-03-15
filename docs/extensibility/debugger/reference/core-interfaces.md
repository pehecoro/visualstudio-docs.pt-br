---
title: Principais Interfaces | Documentos do Microsoft
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- debugging [Debugging SDK], core interfaces
ms.assetid: 666b9116-8550-4bdd-bc15-55fc57de87df
caps.latest.revision: 24
ms.author: gregvanl
manager: ghogen
translation.priority.mt:
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
translationtype: Machine Translation
ms.sourcegitcommit: 5db97d19b1b823388a465bba15d057b30ff0b3ce
ms.openlocfilehash: 8c91ed91339d1d2529a1e10fee453ea5526c1b41
ms.lasthandoff: 02/22/2017

---
# <a name="core-interfaces"></a>Interfaces de núcleo
As seguintes interfaces são interfaces principais para estender o depurador, usando o [!INCLUDE[vsipsdk](../../../extensibility/includes/vsipsdk_md.md)].  
  
## <a name="discussion"></a>Discussão  
 Essas interfaces são usadas principalmente para criar o mecanismo de depuração (DE). Elas são organizadas aqui por categorias:  
  
-   [Pontos de interrupção](#Breakpoints)  
  
-   [Contextos](#Contexts)  
  
-   [Server Core](#CoreServer)  
  
-   [Os mecanismos de depuração](#DebugEngines)  
  
-   [Documentos](#Documents)  
  
-   [Eventos](#Events)  
  
-   [Expressões](#Expressions)  
  
-   [Memória](#Memory)  
  
-   [Módulos](#Modules)  
  
-   [Portas](#Ports)  
  
-   [Processos](#Processes)  
  
-   [Programas](#Programs)  
  
-   [Propriedades](#Properties)  
  
-   [Quadros de pilha](#StackFrames)  
  
-   [Threads](#Threads)  
  
-   [Visualizadores de tipo](#TypeVisualizers)  
  
 As entidades que podem implementar as interfaces são:  
  
-   Debug Engine (DE)  
  
-   Fornecedor de porta (PS)  
  
-   Avaliador de expressão (EE)  
  
-   Visual Studio (VS)  
  
##  <a name="a-namebreakpointsa-breakpoints"></a><a name="Breakpoints"></a>Pontos de interrupção  
 Essas interfaces são relacionadas para a implementação e o rastreamento de pontos de interrupção.  
  
|Interface|Implementado por|Descrição|  
|---------------|--------------------|-----------------|  
|[IDebugBoundBreakpoint2](../../../extensibility/debugger/reference/idebugboundbreakpoint2.md)|DE|Representa um ponto de interrupção associado a um local de memória.|  
|[IDebugBreakpointBoundEvent2](../../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)|DE|Enviado por DE quando um ponto de interrupção é associado a um local de memória.|  
|[IDebugBreakpointChecksumRequest2](../../../extensibility/debugger/reference/idebugbreakpointchecksumrequest2.md)|VS|Representa uma soma de verificação de documento para uma solicitação de ponto de interrupção.|  
|[IDebugBreakpointErrorEvent2](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)|DE|Enviado por DE quando um ponto de interrupção não pode ser vinculado a um local de memória.|  
|[IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md)|DE|Enviado por DE quando um ponto de interrupção é atingido.|  
|[IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md)|VS|Representa uma solicitação para um ponto de interrupção; usado na criação de um ponto de interrupção pendente.|  
|[IDebugBreakpointRequest3](../../../extensibility/debugger/reference/idebugbreakpointrequest3.md)|VS|Representa uma solicitação para um ponto de interrupção; usado na criação de um ponto de interrupção pendente.|  
|[IDebugBreakpointResolution2](../../../extensibility/debugger/reference/idebugbreakpointresolution2.md)|DE|Representa as informações usadas para vincular a um ponto de interrupção.|  
|[IDebugBreakpointUnboundEvent2](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2.md)|DE|Enviado por DE quando um ponto de interrupção é desvinculado de um local de memória.|  
|[IDebugErrorBreakpoint2](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)|DE|Representa um ponto de interrupção inválido (retornado por `IDebugBreakpointErrorEvent2`).|  
|[IDebugErrorBreakpointResolution2](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2.md)|DE|Representa as informações de resolução sobre um ponto de interrupção inválido.|  
|[IDebugFunctionPosition2](../../../extensibility/debugger/reference/idebugfunctionposition2.md)|DE|Representa uma posição em uma função em que um ponto de interrupção está definido.|  
|[IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)|DE|Representa um ponto de interrupção será vinculado; usado na criação de um ponto de interrupção associado.|  
|[IEnumDebugBoundBreakpoints2](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2.md)|DE|Representa uma enumeração sobre um conjunto de pontos de interrupção associados.|  
|[IEnumDebugErrorBreakpoints2](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2.md)|DE|Representa uma enumeração sobre um conjunto de pontos de interrupção que não pôde ser associado a um local da memória.|  
  
##  <a name="a-namecontextsa-contexts"></a><a name="Contexts"></a>Contextos  
 Estas interfaces representam vários tipos de contextos dentro do programa que está sendo depurado.  
  
|Interface|Implementado por|Descrição|  
|---------------|--------------------|-----------------|  
|[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)|DE|Representa a posição inicial de uma instrução de código.|  
|[IDebugCodeContext3](../../../extensibility/debugger/reference/idebugcodecontext3.md)|DE|Estende o [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) interface para habilitar a recuperação das interfaces do módulo e o processo.|  
|[IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)|VS, DE|Representa uma posição em um documento.|  
|[IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md)|DE|Representa o contexto no qual avaliar uma expressão.|  
|[IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)|DE|Representa o local inicial na memória de uma coleção de bytes.|  
|[IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)|DE|Representa um contexto do quadro de pilha em um ponto de interrupção ou exceção.|  
|[IDebugStackFrame3](../../../extensibility/debugger/reference/idebugstackframe3.md)|DE|Representa um contexto do quadro de pilha em um ponto de interrupção ou exceção.|  
|[IEnumDebugCodeContexts2](../../../extensibility/debugger/reference/ienumdebugcodecontexts2.md)|DE|Representa uma enumeração sobre um conjunto de contextos de código.|  
  
##  <a name="a-namecoreservera-core-server"></a><a name="CoreServer"></a>Server Core  
 Estas interfaces representam o computador no qual um programa está sendo depurado. Eles são implementados por [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] , mas pode ser chamado pelos mecanismos de depuração.  
  
|Interface|Implementado por|Descrição|  
|---------------|--------------------|-----------------|  
|[IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)|VS|Fornece acesso a portas e fornecedores de porta, bem como informações sobre o computador.|  
|[IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)|VS|Representa uma [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md) que dá suporte a depuração remota.|  
  
##  <a name="a-namedebugenginesa-debug-engines"></a><a name="DebugEngines"></a>Os mecanismos de depuração  
 Estas interfaces representam os mecanismos de depuração e seus eventos associados.  
  
|Interface|Implementado por|Descrição|  
|---------------|--------------------|-----------------|  
|[IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)|DE|Representa um mecanismo de depuração personalizada.|  
|[IDebugEngine3](../../../extensibility/debugger/reference/idebugengine3.md)|DE|Representa um mecanismo de depuração personalizada que oferece suporte ao carregamento de símbolos, JustMyCode e exceções.|  
|[IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md)|DE|Enviado por cada nova instância DE para indicar que ele está pronto para lidar com tarefas de depuração.|  
|[IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)|DE|Representa um mecanismo de depuração personalizada que dá suporte a programas de inicialização.|  
|[IDebugProgramEngines2](../../../extensibility/debugger/reference/idebugprogramengines2.md)|DE, PS|Representa um nó de programa que lida com vários mecanismos de depuração.|  
|[IDebugQueryEngine2](../../../extensibility/debugger/reference/idebugqueryengine2.md)|DE|Fornece uma maneira para o SDM obter uma interface para o mecanismo de depuração de um thread, o programa ou o quadro de pilha.|  
  
##  <a name="a-namedocumentsa-documents"></a><a name="Documents"></a>Documentos  
 Estas interfaces representam documentos (arquivos de origem) e seus elementos associados.  
  
|Interface|Implementado por|Descrição|  
|---------------|--------------------|-----------------|  
|[IDebugActivateDocumentEvent2](../../../extensibility/debugger/reference/idebugactivatedocumentevent2.md)|DE|Enviado por DE solicitar um documento a ser aberto.|  
|[IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md)|DE|Representa um fluxo de instruções desmontadas de um documento.|  
|[IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)|VS, DE|Representa um documento fornecido pelo DE, especificando um nome e uma classe CLSID (identificador).|  
|[IDebugDocumentChecksum2](../../../extensibility/debugger/reference/idebugdocumentchecksum2.md)|DE, EE|Representa uma soma de verificação para um documento de depuração e permite passar a soma de verificação entre componentes.|  
|[IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)|VS, DE|Representa um contexto de documento, uma posição dentro de um documento correspondente a um determinado contexto de instrução e código.|  
|[IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md)|VS, DE|Representa uma posição geral dentro de um documento.|  
|[IDebugDocumentPositionOffset2](../../../extensibility/debugger/reference/idebugdocumentpositionoffset2.md)|VS|Representa uma posição em um arquivo de origem como um deslocamento de caractere.|  
|[IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md)|VS, DE|Representa um documento de texto fornecido pelo DE (derivado de [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)), fornecendo o texto real.|  
|[IDebugDocumentTextEvents2](../../../extensibility/debugger/reference/idebugdocumenttextevents2.md)|DE|Enviado por DE especificar alterações em um arquivo de origem que está na memória.|  
  
##  <a name="a-nameeventsa-events"></a><a name="Events"></a>Eventos  
 Estas interfaces representam todos os eventos que são enviados entre DE e o Gerenciador de sessão de depuração (SDM).  
  
|Interface|Implementado por|Descrição|  
|---------------|--------------------|-----------------|  
|[IDebugActivateDocumentEvent2](../../../extensibility/debugger/reference/idebugactivatedocumentevent2.md)|DE|Enviado por DE solicitar um documento a ser aberto.|  
|[IDebugBeforeSymbolSearchEvent2](../../../extensibility/debugger/reference/idebugbeforesymbolsearchevent2.md)|DE|O mecanismo de depuração (DE) envia essa interface para o Gerenciador de sessão de depuração (SDM) para definir o status barra mensagem durante cargas de símbolo.|  
|[IDebugBreakEvent2](../../../extensibility/debugger/reference/idebugbreakevent2.md)|DE|Enviado por DE quando uma quebra no programa foi concluída.|  
|[IDebugBreakpointBoundEvent2](../../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)|DE|Enviado por DE quando um ponto de interrupção está associado.|  
|[IDebugBreakpointErrorEvent2](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)|DE|Enviado por DE quando um ponto de interrupção não pode ser associado.|  
|[IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md)|DE|Enviado por DE quando um ponto de interrupção é atingido.|  
|[IDebugBreakpointUnboundEvent2](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2.md)|DE|Enviado por DE quando um ponto de interrupção é desvinculado.|  
|[IDebugCanStopEvent2](../../../extensibility/debugger/reference/idebugcanstopevent2.md)|DE|Enviados por DE para determinar se deve parar em um local específico.|  
|[IDebugDocumentTextEvents2](../../../extensibility/debugger/reference/idebugdocumenttextevents2.md)|DE|Enviado por DE especificar alterações em um arquivo de origem que está na memória.|  
|[IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md)|DE|Enviado por cada nova instância DE para indicar que ele está pronto para lidar com tarefas de depuração.|  
|[IDebugEntryPointEvent2](../../../extensibility/debugger/reference/idebugentrypointevent2.md)|DE|Enviado por DE para indicar que o programa que está sendo depurado está pronto para executar a primeira instrução.|  
|[IDebugErrorEvent2](../../../extensibility/debugger/reference/idebugerrorevent2.md)|DE|Uma interface que é usada por outras interfaces de evento, que podem retornar um erro, para fornecer mensagens de erro legível.|  
|[IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)|DE, PS|Interface base do qual todos os outros eventos interfaces são derivadas.|  
|[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)|VS|Representa uma interface implementada pelo SDM para que os eventos (expressados em objetos que implementam uma interface de evento específico) são enviados.|  
|[IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md)|DE|Enviado por DE quando ocorreu uma exceção no programa que está sendo depurado.|  
|[IDebugExpressionEvaluationCompleteEvent2](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)|DE|Enviado por DE quando uma avaliação de expressão assíncrona for concluída.|  
|IDebugFindSymbolEvent2||OBSOLETO. NÃO USE.|  
|[IDebugInterceptExceptionCompleteEvent2](../../../extensibility/debugger/reference/idebuginterceptexceptioncompleteevent2.md)|DE|Enviado por DE quando o processamento de uma exceção interceptado foi concluído.|  
|[IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md)|DE|Enviado por DE quando um programa for carregado.|  
|[IDebugMessageEvent2](../../../extensibility/debugger/reference/idebugmessageevent2.md)|DE|Enviado por ter a exibição IDE DE uma mensagem informativa para o usuário.|  
|[IDebugModuleLoadEvent2](../../../extensibility/debugger/reference/idebugmoduleloadevent2.md)|DE|Enviado por DE quando um módulo é carregado ou descarregado.|  
|[IDebugNoSymbolsEvent2](../../../extensibility/debugger/reference/idebugnosymbolsevent2.md)|DE|Sinais de [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] da interface do usuário para avisar o usuário que símbolos não pôde ser localizados para o executável iniciado do depurador.|  
|[IDebugOutputStringEvent2](../../../extensibility/debugger/reference/idebugoutputstringevent2.md)|DE|Enviada por ter a exibição IDE DE uma cadeia de caracteres arbitrária.|  
|[IDebugPortEvents2](../../../extensibility/debugger/reference/idebugportevents2.md)|VS, DE|Enviado por uma porta para se comunicar eventos de porta para qualquer ouvinte.|  
|[IDebugProcessCreateEvent2](../../../extensibility/debugger/reference/idebugprocesscreateevent2.md)|DE, PS|Enviado pela porta ou DE quando um processo tiver sido criado.|  
|[IDebugProcessDestroyEvent2](../../../extensibility/debugger/reference/idebugprocessdestroyevent2.md)|DE, PS|Enviado pela porta ou DE quando um processo foi destruído.|  
|[IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)|DE, PS|Enviado pela porta ou DE quando um programa tiver sido criado.|  
|[IDebugProgramDestroyEvent2](../../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)|DE, PS|Enviado pela porta ou DE quando um programa foi destruído.|  
|[IDebugProgramDestroyEventFlags2](../../../extensibility/debugger/reference/idebugprogramdestroyeventflags2.md)|DE|Permite que um mecanismo de depuração substituir o comportamento padrão da [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] UI ao encerrar uma sessão de depuração.|  
|[IDebugProgramNameChangedEvent2](../../../extensibility/debugger/reference/idebugprogramnamechangedevent2.md)|DE|Enviado do mecanismo de depuração (DE) para o Gerenciador de sessão de depuração (SDM) quando altera o nome de um programa.|  
|[IDebugPropertyCreateEvent2](../../../extensibility/debugger/reference/idebugpropertycreateevent2.md)|DE|Enviado por DE quando uma nova propriedade (representado pelo `IDebugProperty2` interface) foi criado.|  
|[IDebugPropertyDestroyEvent2](../../../extensibility/debugger/reference/idebugpropertydestroyevent2.md)|DE|Enviado por DE quando uma propriedade foi destruída.|  
|[IDebugReturnValueEvent2](../../../extensibility/debugger/reference/idebugreturnvalueevent2.md)|DE|Enviado pelo DE quando a revisão de ou em uma função para que o valor de retorno pode ser exibido corretamente.|  
|[IDebugSettingsCallback2](../../../extensibility/debugger/reference/idebugsettingscallback2.md)|VS|Habilita o mecanismos para ler as configurações de métrica de depuração remotamente.|  
|[IDebugStepCompleteEvent2](../../../extensibility/debugger/reference/idebugstepcompleteevent2.md)|DE|Enviado por DE quando uma etapa em, acima ou fora de uma instrução foi concluída.|  
|[IDebugSymbolSearchEvent2](../../../extensibility/debugger/reference/idebugsymbolsearchevent2.md)|DE|Enviada por DE para indicar o êxito ou falha de carregamento de símbolos para um módulo.|  
|[IDebugThreadCreateEvent2](../../../extensibility/debugger/reference/idebugthreadcreateevent2.md)|DE|Enviado por DE quando um thread foi criado.|  
|[IDebugThreadDestroyEvent2](../../../extensibility/debugger/reference/idebugthreaddestroyevent2.md)|DE|Enviado por DE quando um thread foi destruído.|  
|[IDebugThreadNameChangedEvent2](../../../extensibility/debugger/reference/idebugthreadnamechangedevent2.md)|DE|Enviado por DE quando um thread mudou seu nome.|  
  
##  <a name="a-nameexpressionsa-expressions"></a><a name="Expressions"></a>Expressões  
 Estas interfaces representam expressões sejam avaliadas em um determinado contexto.  
  
|Interface|Implementado por|Descrição|  
|---------------|--------------------|-----------------|  
|[IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md)|DE|Representa uma expressão a ser avaliada. Obtido o [IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md) interface.|  
|[IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md)|DE|Representa um contexto no qual uma expressão é avaliada. Obtido o [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md) interface.|  
|[IDebugExpressionEvaluationCompleteEvent2](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)|DE|Enviado por DE quando uma avaliação de expressão assíncrona for concluída.|  
  
##  <a name="a-namememorya-memory"></a><a name="Memory"></a>Memória  
 Estas interfaces representam sequências de bytes de memória.  
  
|Interface|Implementado por|Descrição|  
|---------------|--------------------|-----------------|  
|[IDebugMemoryBytes2](../../../extensibility/debugger/reference/idebugmemorybytes2.md)|DE|Representa uma sequência de bytes de memória que pode ser lido ou gravado.|  
|[IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)|DE|Representa um local na memória de uma sequência de bytes.|  
  
##  <a name="a-namemodulesa-modules"></a><a name="Modules"></a>Módulos  
 Estas interfaces representam um módulo, que corresponde a um arquivo executável ou. Arquivo DLL.  
  
|Interface|Implementado por|Descrição|  
|---------------|--------------------|-----------------|  
|[IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)|DE|Representa um único executável ou DLL.|  
|[IDebugModule3](../../../extensibility/debugger/reference/idebugmodule3.md)|DE|Representa uma [IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md) que dá suporte a símbolos.|  
|[IDebugModuleLoadEvent2](../../../extensibility/debugger/reference/idebugmoduleloadevent2.md)|DE|Enviado por DE quando um módulo é carregado ou descarregado.|  
|[IDebugSourceServerModule](../../../extensibility/debugger/reference/idebugsourceservermodule.md)|DE|Representa as informações do servidor de origem que estão contidas em um arquivo PDB.|  
|[IEnumDebugModules2](../../../extensibility/debugger/reference/ienumdebugmodules2.md)|DE|Representa uma enumeração sobre um conjunto de módulos que são conhecidos por um [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md).|  
  
##  <a name="a-nameportsa-ports"></a><a name="Ports"></a>Portas  
 Estas interfaces representam portas e fornecedores de porta.  
  
|Interface|Implementado por|Descrição|  
|---------------|--------------------|-----------------|  
|[IDebugDefaultPort2](../../../extensibility/debugger/reference/idebugdefaultport2.md)|VS, PS|Representa a porta padrão no computador local.|  
|[IDebugFirewallConfigurationCallback2](../../../extensibility/debugger/reference/idebugfirewallconfigurationcallback2.md)|VS|Permite que um mecanismo de depuração que usa DCOM para perguntar a [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] interface do usuário para certificar-se de que o firewall não bloqueará a depuração remota.|  
|[IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)|VS, PS|Representa uma porta.|  
|[IDebugPortEvents2](../../../extensibility/debugger/reference/idebugportevents2.md)|PS|Enviado por uma porta para se comunicar eventos de porta para qualquer ouvinte.|  
|[IDebugPortEx2](../../../extensibility/debugger/reference/idebugportex2.md)|PS|Representa uma porta pode iniciar e encerrar processos.|  
|[IDebugPortNotify2](../../../extensibility/debugger/reference/idebugportnotify2.md)|PS|Usado para registrar e cancelar o registro de programas com uma porta; permite que a porta controlar programas atualmente sendo depurado.|  
|[IDebugPortPicker](../../../extensibility/debugger/reference/idebugportpicker.md)|PS|Representa uma interface do usuário personalizada para selecionar a porta.|  
|[IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md)|VS|Representa uma solicitação para uma porta na qual uma nova porta será criada ou localizada.|  
|[IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)|PS|Representa um fornecedor de portas.|  
|[IDebugPortSupplier3](../../../extensibility/debugger/reference/idebugportsupplier3.md)|PS|Representa um fornecedor de portas que podem persistir (Salvar em disco) informações sobre as portas que ele criou.|  
|[IDebugPortSupplierDescription2](../../../extensibility/debugger/reference/idebugportsupplierdescription2.md)|PS|Permite que o [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] interface do usuário para exibir o texto dentro de **transportar informações** seção o **anexar ao processo** caixa de diálogo.|  
|[IDebugWindowsComputerPort2](../../../extensibility/debugger/reference/idebugwindowscomputerport2.md)|VS|Permite consultas para obter informações sobre o computador de destino.|  
|[IEnumDebugPorts2](../../../extensibility/debugger/reference/ienumdebugports2.md)|VS, PS|Representa uma enumeração sobre um conjunto de portas.|  
|[IEnumDebugPortSuppliers2](../../../extensibility/debugger/reference/ienumdebugportsuppliers2.md)|VS|Representa uma enumeração sobre um conjunto de fornecedores de porta.|  
  
##  <a name="a-nameprocessesa-processes"></a><a name="Processes"></a>Processos  
 Estas interfaces representam processos, um único executável que contém um ou mais programas.  
  
|Interface|Implementado por|Descrição|  
|---------------|--------------------|-----------------|  
|[IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)|PS, DE|Representa um processo em execução em um computador.|  
|[IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)|PS, DE|Representa um processo ativamente dá suporte à depuração (usado para substituir a etapa, continuar e executar métodos no [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) interface).|  
|[IDebugProcessCreateEvent2](../../../extensibility/debugger/reference/idebugprocesscreateevent2.md)|DE, PS|Enviado pela porta ou DE quando um processo tiver sido criado.|  
|[IDebugProcessDestroyEvent2](../../../extensibility/debugger/reference/idebugprocessdestroyevent2.md)|DE, PS|Enviado pela porta ou DE quando um processo foi destruído.|  
|[IDebugProcessEx2](../../../extensibility/debugger/reference/idebugprocessex2.md)|PS|Representa um processo que deve controlar qual sessão anexado a ele.|  
|[IEnumDebugProcesses2](../../../extensibility/debugger/reference/ienumdebugprocesses2.md)|PS|Representa uma enumeração de um conjunto de processos em uma porta.|  
  
##  <a name="a-nameprogramsa-programs"></a><a name="Programs"></a>Programas  
 Estas interfaces representam programas, unidades lógicas de execução que não necessariamente correspondem a um executável físico ou módulo.  
  
|Interface|Implementado por|Descrição|  
|---------------|--------------------|-----------------|  
|[IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)|DE|Representa uma [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) que precisa para trabalhar em conjunto com outros programas sendo depurados ao mesmo tempo.|  
|[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)|DE, PS|Representa uma unidade lógica de execução.|  
|[IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)|DE, PS|Enviado pela porta ou DE quando um programa tiver sido criado.|  
|[IDebugProgramDestroyEvent2](../../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)|DE, PS|Enviado pela porta ou DE quando um programa foi destruído.|  
|[IDebugProgramEngines2](../../../extensibility/debugger/reference/idebugprogramengines2.md)|DE, PS|Representa uma [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) que podem ser tratados por vários mecanismos de depuração.|  
|[IDebugProgramEx2](../../../extensibility/debugger/reference/idebugprogramex2.md)|PS|Representa uma [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) que deve ser capaz de controlar qual sessão anexado a ele.|  
|[IDebugProgramHost2](../../../extensibility/debugger/reference/idebugprogramhost2.md)|DE, PS|Representa uma [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) que pode retornar informações sobre o processo no qual ele está em execução.|  
|[IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)|DE, PS|Representa um programa que pode ser depurado.|  
|[IDebugProgramNodeAttach2](../../../extensibility/debugger/reference/idebugprogramnodeattach2.md)|DE, PS|Permite que um nó de programa ser notificado de uma tentativa de anexar o programa associado.|  
|[IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md)|DE|Fornece uma maneira para o SDM consultar um DE sobre os programas controlados por essa DE.|  
|[IDebugProgramPublisher2](../../../extensibility/debugger/reference/idebugprogrampublisher2.md)|VS|Usado por DEs para registrar programas com o SDM para mostrar que estão sendo depurados.|  
|[IDebugProviderProgramNode2](../../../extensibility/debugger/reference/idebugproviderprogramnode2.md)|DE, PS|Representa uma [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) que pode realizar marshaling de interfaces entre limites de thread ou processo.|  
|[IEnumDebugPrograms2](../../../extensibility/debugger/reference/ienumdebugprograms2.md)|DE, PS|Representa uma enumeração de um conjunto de programas.|  
  
##  <a name="a-namepropertiesa-properties"></a><a name="Properties"></a> Propriedades  
 Estas interfaces representam propriedades, um valor associado a um contexto específico, geralmente o resultado de uma avaliação de expressão.  
  
|Interface|Implementado por|Descrição|  
|---------------|--------------------|-----------------|  
|[IDebugCustomViewer](../../../extensibility/debugger/reference/idebugcustomviewer.md)|EE|Representa uma [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) que pode exibir seu valor de forma personalizada.|  
|[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)|DE|Representa um valor de um quadro de pilha, documento ou o resultado de uma avaliação de expressão.|  
|[IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)|DE|Representa uma [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) que dá suporte a cadeias de caracteres longas arbitrariamente.|  
|[IDebugPropertyCreateEvent2](../../../extensibility/debugger/reference/idebugpropertycreateevent2.md)|DE|Enviado por DE quando uma nova propriedade (representado pelo [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) interface) foi criado.|  
|[IDebugPropertyDestroyEvent2](../../../extensibility/debugger/reference/idebugpropertydestroyevent2.md)|DE|Enviado por DE quando uma propriedade foi destruída.|  
|[IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)|DE|Representa uma referência a uma propriedade que pode existir fora de algum quadro de pilha específico.|  
|[IEnumDebugPropertyInfo2](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)|DE|Representa uma enumeração sobre um conjunto de [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) estruturas que descrevem variáveis, registros, parâmetros e expressões.|  
|[IEnumDebugReferenceInfo2](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2.md)|DE|Representa uma enumeração sobre um conjunto de [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md) estruturas.|  
  
##  <a name="a-namestackframesa-stack-frames"></a><a name="StackFrames"></a>Quadros de pilha  
 Estas interfaces representam um quadro de pilha, um contexto no qual um ponto de interrupção ou exceção ocorreu.  
  
|Interface|Implementado por|Descrição|  
|---------------|--------------------|-----------------|  
|[IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)|DE|Representa um contexto no qual um ponto de interrupção ou exceção ocorreu.|  
|[IDebugStackFrame3](../../../extensibility/debugger/reference/idebugstackframe3.md)|DE|Representa uma [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md) que pode manipular interceptadas exceções.|  
|[IEnumCodePaths2](../../../extensibility/debugger/reference/ienumcodepaths2.md)|DE|Representa uma enumeração sobre o conjunto de [CODE_PATH](../../../extensibility/debugger/reference/code-path.md) estruturas que especificam a função chamar sequência usada para chegar a um quadro de pilhas específico.|  
|[IEnumDebugFrameInfo2](../../../extensibility/debugger/reference/ienumdebugframeinfo2.md)|DE|Representa uma enumeração sobre um conjunto de [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md) estruturas que descrevem os quadros de pilha.|  
  
##  <a name="a-namethreadsa-threads"></a><a name="Threads"></a>Threads  
 Estas interfaces representam threads e seus eventos associados.  
  
|Interface|Implementado por|Descrição|  
|---------------|--------------------|-----------------|  
|[IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)|DE|Representa um segmento de execução.|  
|[IDebugThreadCreateEvent2](../../../extensibility/debugger/reference/idebugthreadcreateevent2.md)|DE|Enviado por DE quando um thread foi criado.|  
|[IDebugThreadDestroyEvent2](../../../extensibility/debugger/reference/idebugthreaddestroyevent2.md)|DE|Enviado por DE quando um thread foi destruído.|  
|[IDebugThreadNameChangedEvent2](../../../extensibility/debugger/reference/idebugthreadnamechangedevent2.md)|DE|Enviado por DE quando um thread mudou seu nome.|  
|[IEnumDebugThreads2](../../../extensibility/debugger/reference/ienumdebugthreads2.md)|DE|Representa uma enumeração sobre um conjunto de threads.|  
  
##  <a name="a-nametypevisualizersa-type-visualizers"></a><a name="TypeVisualizers"></a>Visualizadores de tipo  
 Essas interfaces fornecem suporte para visualizadores de tipo. Essas interfaces são normalmente implementadas por um avaliador de expressão.  
  
|Interface|Implementado por|Descrição|  
|---------------|--------------------|-----------------|  
|[IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)|EE|Representa uma matriz de bytes a serem apresentados em um visualizador de tipo.|  
|[IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)|EE|Fornece métodos para obter acesso a dados a serem passados para um visualizador de tipo.|  
|[IPropertyProxyProvider](../../../extensibility/debugger/reference/ipropertyproxyprovider.md)|EE|Representa uma propriedade que fornece acesso a [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md) implementações.|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API](../../../extensibility/debugger/reference/api-reference-visual-studio-debugging.md)   
 [Criando um mecanismo de depuração personalizado](../../../extensibility/debugger/creating-a-custom-debug-engine.md)