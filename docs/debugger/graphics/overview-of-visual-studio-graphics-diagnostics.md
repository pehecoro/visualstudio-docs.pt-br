---
title: "Visão geral do diagnóstico de gráficos do Visual Studio | Microsoft Docs"
ms.custom: 
ms.date: 02/09/2017
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-debug
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ddd429d9-ac70-4ac4-9e69-299c6ea2df09
caps.latest.revision: "29"
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 0f713a1ced59ea1ed0eaf01a3d9630aa96e4c6bf
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2017
---
# <a name="overview-of-visual-studio-graphics-diagnostics"></a>Visão geral do diagnóstico de gráficos do Visual Studio
O Visual Studio *diagnóstico de gráficos* é um conjunto de ferramentas para gravação e, em seguida, analisando problemas de desempenho e a renderização em aplicativos do Direct3D. Diagnóstico de gráficos pode ser usado em aplicativos que estão em execução localmente no seu PC com Windows, em um emulador de dispositivo do Windows ou em um computador remoto ou o dispositivo.  
  
## <a name="using-graphics-diagnostics-to-debug-rendering-problems"></a>Usando o Diagnóstico de Gráficos para depurar problemas de renderização  
 Depurar problemas de renderização em um aplicativo cheio de recursos gráficos não é tão simples quanto iniciar um depurador e percorrer alguns códigos. Em cada quadro, centenas de milhares de pixels exclusivos são produzidos, cada um de acordo com um conjunto complexo de estados, dados, parâmetros e códigos, e dentre eles, talvez apenas alguns pixels exibirão o problema que você está tentando diagnosticar. Para complicar ainda mais, o código que gera cada pixel é executado em hardware especializado que processa centenas de pixels paralelamente. As ferramentas e técnicas tradicionais de depuração (cujo aproveitamento é difícil mesmo no código em thread bastante simples) são ineficazes quando se deparam com grandes quantidades de dados.  
  
 As ferramentas de Diagnóstico de Gráficos no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] foram desenvolvidas para ajudar a localizar problemas de renderização, a começar pelos artefatos visuais que indicam o problema e rastreiam de volta para a origem do problema focando apenas o código de sombreador, os estágios de pipeline, as chamadas de desenho e o estado do dispositivo que são relevantes, no próprio código-fonte do aplicativo.  
  
## <a name="directx-version-compatibility"></a>Compatibilidade de versão do DirectX  
 Diagnóstico de gráficos oferece suporte a aplicativos que usam o Direct3D 10 ou superior e fornece suporte limitado para aplicativos que usam o Direct2D. Ele não oferece suporte a aplicativos que usam versões anteriores do Direct3D, DirectDraw ou outras APIs gráficas.  
  
### <a name="windows-10-and-direct3d-12"></a>Windows 10 e Direct3D 12  
 Windows 10 introduzido *Direct3D 12*, que é substancialmente diferente do Direct3D 10 e 11 Direct3D. Essas diferenças que DirectX volte para o alinhamento com hardware gráfico moderno e liberando seu pleno potencial, mas também trazer grandes alterações de API e colocar maior responsabilidade no programador para gerenciar a contenção e tempos de vida do recurso. Apesar das diferenças, o diagnóstico de gráficos com Direct3D 12 mantém paridade de recursos com o diagnóstico de gráficos com 11.2 Direct3D.
  
 Windows 10 também mantém o suporte para versões anteriores do Direct3D e jogos e aplicativos que dependem delas. Diagnóstico de gráficos no Visual Studio continua a dar suporte a Direct3D 10 e 11 Direct3D no Windows 10, bem como no Windows 8.1.  
  
### <a name="windows-81-and-direct3d-112"></a>Windows 8.1 e Direct3D 11.2  
 No [!INCLUDE[win81](../includes/win81_md.md)], o DirectX 11.2 apresenta novos recursos que incluem suporte para capturar informações gráficas ao longo do tempo de execução. [!INCLUDE[win81](../includes/win81_md.md)]usa a captura de novo com base em tempo de execução — conhecido como *captura robusta*— exclusivamente para todas as versões do DirectX que [!INCLUDE[win81](../includes/win81_md.md)] oferece suporte. A captura robusta também oferece suporte a novos recursos do Direct3D 11.2.  
  
### <a name="limited-direct2d-support"></a>Suporte limitado ao Direct2D  
 Como Direct2D é uma API de modo de usuário é criada sobre Direct3D, você pode usar o diagnóstico de gráficos para ajudar a depurar problemas de renderização em aplicativos que usam o Direct2D. No entanto, como apenas os eventos do Direct3D subjacentes são gravados, em vez de eventos do Direct2D de nível mais alto, os eventos do Direct2D não aparecerão na Lista de Eventos de Gráficos. Além disso, como a relação entre os eventos do Direct2D e os eventos resultantes do Direct3D nem sempre é clara, usar o Diagnóstico de Gráficos para depurar problemas de renderização em aplicativos que usam o Direct2D não é algo simples. Ainda assim, você pode usar o Diagnóstico de Gráficos para obter informações sobre problemas de renderização de nível baixo em aplicativos que usam o Direct2D.  
  
## <a name="graphics-diagnostics-features-in-visual-studio"></a>Recursos de diagnóstico de gráficos do Visual Studio  
 Diagnóstico de gráficos tem uma interface dedicada - janela analisador de gráficos - para diagnosticar problemas de processamento, mas também adiciona algumas ferramentas de interface do Visual Studio.  
  
### <a name="the-graphics-toolbar-visual-studio"></a>A barra de ferramentas de gráficos (Visual Studio)  
 A barra de ferramentas de gráficos fornece acesso rápido aos comandos de diagnóstico de gráficos.  
  
 O **iniciar diagnóstico** botão executa o aplicativo com o diagnóstico de gráficos. Quando um aplicativo está em execução com o diagnóstico de gráficos, o **capturar o próximo quadro renderizado** botão é habilitado.  
  
### <a name="diagnostics-capture-interface"></a>Captura de diagnóstico de interface  
 Quando você executa seu aplicativo com o diagnóstico de gráficos, o Visual Studio exibe uma interface de sessão de diagnóstico que você pode usar para capturar os quadros e que também exibe a carga de CPU e GPU atual. A carga da CPU e GPU é exibida para ajudá-lo a identificar os quadros que talvez você queira capturar devido a suas características de desempenho, em vez de erros de processamento.  
  
 Não é a única maneira de capturar quadros embora. Você também pode capturar quadros usando a interface de captura programática ou usando o programa de captura de linha de comando, dxcap.exe.  
  
 Consulte [capturando informações de gráficos](capturing-graphics-information.md) para obter mais informações.  
  
### <a name="gpu-usage"></a>Uso de GPU  
 Diagnóstico de gráficos também pode analisar o desempenho do seu aplicativo Direct3D. Porque os dados de criação de perfil seria afetada por gravação de detalhes de eventos de elementos gráficos, ela é separada da captura de quadros a serem usados examinado com o analisador de gráficos.  
  
 Consulte [uso de GPU](gpu-usage.md) para obter mais informações.  
  
### <a name="directx-control-panel"></a>Painel de controle do DirectX  
 O painel de controle do DirectX é um componente do DirectX que você pode usar para alterar o comportamento do DirectX. Por exemplo, é possível habilitar a versão de depuração dos componentes de tempo de execução do DirectX, selecionar os tipos de mensagem de depuração que são relatados e impedir que determinados recursos de hardware gráfico sejam usados para emular um hardware menos capaz. Esse nível de controle sobre o DirectX pode ajudar você a depurar e testar seu aplicativo DirectX. É possível acessar o painel de controle do DirectX do Visual Studio.  
  
#### <a name="to-open-the-directx-control-panel"></a>Para abrir o painel de controle do DirectX  
  
-   Na barra de menus, escolha **depurar**, **gráficos**, **painel de controle do DirectX**.  
  
## <a name="graphics-analyzer"></a>Analisador de gráficos  
 O analisador de gráficos do Visual Studio é uma interface dedicada para examinar os problemas de desempenho e a renderização em quadros que você já tiver capturados. Analisador de gráficos, você encontrará várias ferramentas para ajudá-lo a explorar e compreender o comportamento de renderização do seu aplicativo. Cada ferramenta expõe um tipo diferente de informações sobre o quadro que está sendo inspecionado, e as ferramentas são projetadas para ser usado em conjunto para intuitivamente estreitos na origem de um problema de processamento, a partir de sua aparência no framebuffer.  
  
 Esta ilustração mostra um layout típico de ferramentas no analisador de gráficos.  
  
 ![Todos os elementos gráficos janelas do depurador](media/graphicsdebuggerwindows.png "GraphicsDebuggerWindows")  
  
### <a name="the-graphics-toolbar-graphics-analyzer"></a>A barra de ferramentas de gráficos (Analisador de gráficos)  
 A barra de ferramentas de gráficos fornece acesso rápido a janelas de ferramenta Analisador de gráficos.  
  
 ![A barra de ferramentas de gráficos no modo de diagnóstico de gráficos](media/vsg_toolbar.png "vsg_toolbar")  
  
### <a name="graphics-log-document"></a>Documento de log de gráficos  
 Dentro do analisador de gráficos, o documento de log do gráfico é a janela da ferramenta mais importante. Esta janela representa todos os quadros capturados executando seu aplicativo com o diagnóstico de gráficos. A partir daqui, você pode selecionar um quadro diferente para examinar ou selecione um pixel específico que você deseja examinar com a ferramenta de histórico de Pixel. A imagem de framebuffer exibida neste documento são alterados para refletir o evento selecionado no momento, para que você possa ver como o framebuffer é afetada ao longo do tempo.  
  
 O [gráficos Log documento](graphics-log-document.md) é também o ponto de entrada para a ferramenta de análise de quadros, que ajuda você a entender o desempenho de um quadro alterando o modo como determinados aspectos de renderização são configurados e fornecendo os resultados da avaliação de desempenho para Compare com o original.  
  
### <a name="event-list"></a>Lista de eventos  
 Eventos de gráficos marcam cada chamada à API do Direct3D e eventos definidos pelo usuário.  
  
 O [lista de eventos](graphics-event-list.md) mostra todos os eventos de gráficos que foram registrados durante o período em que você está analisando. Para ajudá-lo a encontrar o que é importante, a lista de eventos pode ser exibida hierarquicamente — com recentes alterações de estado sob o subsequentes desenhar chamada — ou como uma linha do tempo. Além disso, eventos são codificados por cores com base em fila que pertencem a e você pode filtrar a lista para incluir somente os eventos que você está interessado.  
  
 Quando você seleciona um evento na lista, o restante das ferramentas de análise de gráficos refletem o estado do quadro no momento do evento. Dessa forma, você pode ver o efeito de qualquer evento na GPU. Por exemplo, você pode ver o efeito imediato de qualquer desenho chamar framebuffer, mesmo que ele se torna obscurecido por chamadas subsequentes de desenho. Alguns eventos também têm hiperlinks que você pode seguir para ver mais detalhes sobre seus parâmetros ou objetos de recurso relacionado.  
  
### <a name="pipeline-stages"></a>Estágios de pipeline  
 Cada chamada de desenho em seu aplicativo passa pelo pipeline gráfica fornecido pelo Direct3D. Em cada estágio no pipeline, saída do estágio anterior é transformada por um pequeno programa, chamada um sombreador e, em seguida, passada para o próximo estágio até finalmente é renderizado na tela. Muitos erros de processamento ocorrerem no limite entre estágios do pipeline quando o formato de saída é diferente do que o próximo estágio esperado, ou quando qualquer um estágio simplesmente produz resultados incorretos. Normalmente, você somente obtém os resultados finais que você vê na tela e você não pode determinar facilmente onde no pipeline ocorreu o erro.  
  
 O [estágios do Pipeline](graphics-pipeline-stages.md) janela visualiza o resultado de cada estágio de forma independente, para que você possa determinar mais facilmente qual estágio um problema de renderização aparece primeiro no. Depois de determinar qual estágio ou seja, você pode iniciar a depuração de seu sombreador à direita da janela estágios de Pipeline.  
  
### <a name="graphics-state"></a>Estado gráfico  
 Operações de renderização dependem muito do estado é normalmente espalhado por vários objetos. Muitos tipos de problemas de processamento são causados por estado configuradas incorretamente.  
  
 O [estado](graphics-state.md) janela coleta as informações de estado relevantes para cada chamada de desenho junto em um único local para que seja mais fácil localizar e também realça as alterações de estado que ocorreram desde a última desenha chamada.  
  
### <a name="pixel-history"></a>Histórico de pixels  
 Cenas complexas, não é incomum um pixel ser sombreados várias vezes em uma única estrutura. Às vezes, a cor do anterior é substituídos apenas, mas outras vezes as cores são combinadas para obter efeitos como transparência. Quando o resultado da combinação de conjunto não tem a aparência de direito facilmente não pode determinar se é porque uma das cores estava incorreta ou se houver um problema com a maneira como eles foram combinados. Outras vezes, um objeto pode parecer estar ausentes porque sua contribuição para o pixel foi rejeitada por alguma razão.  
  
 O [histórico de Pixel](graphics-pixel-history.md) janela visualiza o histórico de sombreador completa de cada pixel no quadro, incluindo contribuições rejeitadas. Para contribuições que não foram rejeitadas, ele exibe os resultados brutos do sombreador e como cada nova cor foi combinado com a anterior. Com essas informações, é muito mais fácil de localizar a origem dos erros em pixels que resultados de sombreador de mesclagem, ou quando um objeto renderizado está ausente porque sua contribuição para o pixel incorretamente foi rejeitada.  
  
### <a name="event-call-stack"></a>Pilha de chamadas  
 Código do sombreador não é a única fonte de problemas de processamento em um aplicativo Direct3D, às vezes, o código-fonte do aplicativo transmite o parâmetro errado ou não configurar Direct3D algo errado. Um tipo de erro que o recurso discutido anteriormente, o histórico de Pixel pode ajudá-lo a encontrar é quando um objeto renderizado está ausente, porque todos os seus pixels foram rejeitados. Esse tipo de erro geralmente ocorre quando você configurado incorretamente uma configuração, como aquele que controla como o teste de profundidade é executado e você pode encontrar geralmente o erro em algum lugar na pilha de chamadas do objeto ausente desenhar chamada.  
  
 O [pilha de chamadas do evento](graphics-event-call-stack.md) janela exibe a pilha de chamadas completa de todos os eventos de gráfico na lista de eventos e código-fonte mesmo permite que você pode ir para o seu aplicativo se as informações de depuração está disponível. Isso é uma ferramenta poderosa para o seguinte erro de onde ele é inicialmente exibido, na GPU para onde foi originado no código-fonte do seu aplicativo.  
  
### <a name="object-table"></a>Tabela de objeto  
 Todos os quadros processa seu aplicativo provavelmente é apoiado por centenas ou mesmo milhares de objetos de recurso. Esses podem incluir buffers back e renderizar destinos, texturas, buffers de vértice, buffers de índice, buffers gerais — quase tudo o que lembra Direct3D é um objeto.  
  
 O [objeto tabela](graphics-object-table.md) exibe todos os objetos existentes no momento do evento de gráfico selecionado na listam de eventos. Como a maioria dos objetos em um aplicativo típico texturas, a lista de eventos é otimizada para mostrar os detalhes relevantes para imagens em um relance. A coluna de tipo informa que tipo de objeto está em cada linha e a coluna de formato mais mostra o subtipo ou a versão do objeto. Outros detalhes também são mostrados. Alguns objetos também têm hiperlinks que você pode seguir para exibir o objeto com um visualizador mais especializado, como texturas (você pode exibir a textura como uma imagem) ou (você pode escolher como o Visualizador de buffer analisa e exibe os bytes do buffer bruto definindo o buffer de buffers formato).  
  
### <a name="frame-analysis"></a>Análise de quadro  
 Gráficos do seu aplicativo não precisam ser correto apenas - precisam ser muito rápidos. Mesmo em dispositivos menos eficiente, como laptops com gráficos integrados ou telefones celulares. E ainda precisam ser muito grande.  
  
 O [análise de quadros](graphics-frame-analysis.md) ferramenta explora otimizações de desempenho potencial automaticamente alterando o modo como o aplicativo usa Direct3D e fornecendo os resultados de padrão de referência para comparação. Por exemplo, a análise de quadros pode habilitar o mapeamento de mip em cada textura, que pode revelar texturas que poderiam se beneficiar do mapeamento de mip, mas atualmente não tem habilitado. Em um hardware que oferece suporte a análise de quadros também apresenta informações coletadas dos contadores de desempenho da GPU — esse nível de informações pode identificar problemas de desempenho do nível de hardware, como o grande número de compartimentos de busca de textura ou erros de cache.  
  
 Mas a análise de quadros praticamente não vai fast - é obter o desempenho mais que tempo dando a menor quantidade de qualidade visual. Às vezes, um efeito caro ótimo aparência em uma tela grande não faz o mesmo impacto quando exibido na tela pequena de um telefone, onde um efeito mais simples pode apenas como uma boa aparência sem esgotar a bateria. As alterações automáticas e avaliações de desempenho que fornece análise de gráficos podem ajudá-lo a encontrar o equilíbrio que é ideal para seu aplicativo em uma variedade de dispositivos.  
  
## <a name="see-also"></a>Consulte também  
 [Ferramenta de captura de linha de comando](command-line-capture-tool.md)   
 [Depurador HLSL](hlsl-shader-debugger.md)