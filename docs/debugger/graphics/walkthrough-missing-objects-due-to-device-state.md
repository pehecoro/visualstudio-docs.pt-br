---
title: 'Passo a passo: Objetos ausentes devido ao estado do dispositivo | Microsoft Docs'
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-debug
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1b0d2bbd-0729-4aa5-8308-70c5bf1468c5
caps.latest.revision: "22"
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.workload: multiple
ms.openlocfilehash: c036ccc3865c7ea97c37eda31d802bfc5acbd5a8
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="walkthrough-missing-objects-due-to-device-state"></a>Instruções passo a passo: objetos ausentes devido ao estado do dispositivo
Este passo a passo demonstra como usar [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] diagnóstico de gráficos para investigar um objeto que está ausente devido à configurada incorretamente o estado do dispositivo.  
  
 Este passo a passo demonstra como:  
  
-   Use o **lista de eventos de gráfico** para localizar possíveis fontes do problema.  
  
-   Use o **estágios de Pipeline gráficos** janela para verificar o efeito do `DrawIndexed` chamadas à API do Direct3D.  
  
-   Use o **histórico de Pixel gráfico** janela para localizar o problema mais especificamente.  
  
-   Inspecione o estado do dispositivo para potenciais problemas ou configurações incorretas.  
  
## <a name="scenario"></a>Cenário  
 Um dos motivos que os objetos podem não aparecer em que eles são esperados em um aplicativo 3D é um erro de configuração de dispositivo de gráficos que faz com que os objetos a serem excluídos da renderização — por exemplo, quando a ordem de contorno causa triângulos a ser removido em erro , ou quando a função de teste de profundidade faz todos os pixels no objeto sejam rejeitadas.  
  
 No cenário descrito neste passo a passo, você atingiu apenas a primeira etapa no desenvolvimento de seu aplicativo 3D e está pronto para testá-lo pela primeira vez. No entanto, quando você executa o aplicativo, apenas a interface do usuário é renderizada na tela. Usando o diagnóstico de gráficos, você capturar o problema em um arquivo de log do gráfico para que você pode depurar o aplicativo. O problema é semelhante a no aplicativo:  
  
 ![O aplicativo antes de corrigir o problema](media/vsg_walkthru1_firstview.png "vsg_walkthru1_firstview")  
  
 Para obter informações sobre como detectar os problemas de gráficos em um log de gráficos, consulte [capturando informações de gráficos](capturing-graphics-information.md).  
  
## <a name="investigation"></a>Investigação  
 Usando as ferramentas de diagnóstico de gráficos, você pode carregar o arquivo de log do gráfico para inspecionar os quadros que foram capturados durante o teste.  
  
#### <a name="to-examine-a-frame-in-a-graphics-log"></a>Para examinar um quadro em um log de gráficos  
  
1.  Em [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)], carregar um log de elementos gráficos que contém um quadro que exibe o modelo ausente. Uma nova guia de diagnóstico de gráficos aparece no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]. Na parte superior dessa guia é a saída de destino de renderização do quadro selecionado. Na parte inferior é parte de **lista quadro**, que exibe cada quadro capturado como uma imagem em miniatura.  
  
2.  No **lista quadro**, selecione um quadro que demonstra que o modelo não será exibido. O destino de renderização é atualizado para refletir o quadro selecionado. Nesse cenário, os gráficos de log guia esta aparência:  
  
     ![A lista de visualização e o quadro de framebuffer do guia .vsglog](media/vsg_walkthru1_experiment.png "vsg_walkthru1_experiment")  
  
 Depois de selecionar um quadro que demonstra o problema, você pode usar o **lista de eventos de gráfico** para diagnosticar a ele. O **lista de eventos de gráfico** contém todas as chamadas de API do Direct3D que foi feita para renderizar o quadro ativo, por exemplo, chamadas de API para configurar o estado do dispositivo, para criar e atualizar buffers e desenhar objetos que aparecem no quadro. Muitos tipos de chamadas são interessantes porque não há normalmente (mas nem sempre) uma alteração correspondente no destino de renderização quando o aplicativo está funcionando conforme o esperado, por exemplo desenhar, expedição, cópia ou desmarque chamadas. Chamadas de desenho são especialmente interessantes porque cada um deles representa geometria que o aplicativo renderizado (chamadas de expedição também podem processar a geometria).  
  
#### <a name="to-ensure-that-draw-calls-are-being-made"></a>Para garantir que estão sendo feitas chamadas de desenho  
  
1.  Abra o **lista de eventos de gráfico** janela. Sobre o **diagnóstico de gráficos** barra de ferramentas, escolha **lista de eventos**.  
  
2.  Inspecione o **lista de eventos de gráfico** para desenhar chamadas. Para facilitar essa tarefa, digite "Desenhar" no **pesquisa** caixa no canto superior direito do **lista de eventos de gráfico** janela. Isso filtra a lista para que ele contém apenas os eventos que têm "Desenhar" nos títulos. Nesse cenário, você descobre que várias chamadas de desenho foram feitas:  
  
     ![Lista de eventos de gráfico mostrando os eventos capturados](media/vsg_walkthru1_.png "vsg_walkthru1_")  
  
 Depois de confirmar que estão sendo feitas chamadas de desenho, você pode determinar qual delas corresponde à geometria ausente. Como você sabe que a geometria ausente não desenhada para o destino de renderização (neste caso), você pode usar o **estágios de Pipeline gráficos** janela para determinar qual desenhar chamada corresponde à geometria ausente. O **estágios de Pipeline gráficos** janela mostra a geometria que foi enviada para cada chamada de desenho, independentemente de seu efeito sobre o destino de renderização. Como você percorrer as chamadas de desenho, que os estágios de pipeline são atualizados para mostrar a geometria que está associada essa chamada, e a saída de destino de renderização é atualizada para mostrar o estado de destino de renderização depois que a chamada foi concluída.  
  
#### <a name="to-find-the-draw-call-for-the-missing-geometry"></a>Para localizar a chamada de desenho de geometria ausente  
  
1.  Abra o **estágios de Pipeline gráficos** janela. Sobre o **diagnóstico de gráficos** barra de ferramentas, escolha **estágios do Pipeline**.  
  
2.  Percorrer cada chamada de desenho ao observar o **estágios de Pipeline gráficos** janela para o modelo ausente. O **Assembler de entrada** estágio mostra os dados de modelo bruto. O **sombreador de vértice** estágio mostra os dados transformados do modelo. O **sombreador de Pixel** estágio mostra a saída do sombreador de pixel. O **fusão de saída** estágio mostra o destino de renderização mesclada dessa chamada draw e todas as chamadas de desenho anterior.  
  
3.  Interrompa quando você atingiu a chamada de desenho que corresponde ao modelo ausente. Nesse cenário, o **estágios de Pipeline gráficos** janela indica que a geometria foi processada, mas não apareceu no destino de renderização:  
  
     ![Visualizador de pipeline mostrando o objeto ausente](media/vsg_walkthru1_pipeline.png "vsg_walkthru1_pipeline")  
  
 Depois de confirmar que o aplicativo renderizado a geometria ausente e localize a chamada de desenho correspondente, você pode selecionar uma parte da saída de destino de renderização que deve mostrar a geometria ausente e, em seguida, use o **histórico de Pixel gráfico** janela para descobrir por que os pixels foram excluídos. O histórico de pixel contém uma lista de todas as chamadas de desenho que podem ter tido um efeito em um determinado pixel. Cada desenho chamar o **histórico de Pixel gráfico** janela é identificada por um número que também é exibido no **lista de eventos de gráfico** janela. Isso ajuda você a confirmar que o pixel deve exibir a geometria ausente e para descobrir por que o pixel foi excluído  
  
#### <a name="to-determine-why-the-pixel-was-excluded"></a>Para determinar o motivo pelo qual o pixel foi excluído  
  
1.  Abra o **histórico de Pixel gráfico** janela. Sobre o **diagnóstico de gráficos** barra de ferramentas, escolha **histórico de Pixel**.  
  
2.  Com base no **sombreador de Pixel** miniatura, selecione um pixel de framebuffer de saída que deve conter uma parte da geometria ausente. Nesse cenário, a saída do sombreador de pixel deve abranger mais de um destino de renderização; Depois que um pixel é selecionado, o **histórico de Pixel gráfico** janela tem esta aparência:  
  
     ![Janela de histórico de pixel mostrando relacionados desenhar chamadas](media/vsg_walkthru1_hist1.png "vsg_walkthru1_hist1")  
  
3.  Confirme se o pixel de destino de renderização selecionado contém uma parte da geometria correspondendo o número da chamada de desenho que você está verificando (da **lista de eventos de gráfico** janela) para uma das chamadas de desenho no **gráficos Histórico de pixel** janela. Se nenhuma das chamadas no **histórico de Pixel gráfico** correspondência de janela a chamada de desenho que você está verificando, repita essas etapas (exceto a etapa 1) até encontrar uma correspondência. Nesse cenário, a chamada de desenho correspondente tem esta aparência:  
  
     ![Janela de histórico de pixel mostrando informações de fragmento](media/vsg_walkthru1_hist2.png "vsg_walkthru1_hist2")  
  
4.  Quando você encontrar uma correspondência, expanda a chamada de desenho correspondente no **histórico de Pixel gráfico** janela e confirme que o pixel foi excluído. Cada desenho chamar o **histórico de Pixel gráfico** janela corresponde a um ou mais primitivos geométricos (pontos, linhas ou triângulos) que se cruzam que pixel como resultado da geometria do objeto correspondente. Cada interseção tal pode contribuir para a cor final do pixel. Um primitivo que foi excluído porque ele falhou no teste de profundidade é representado por um ícone que mostra a letra Z ao longo de uma seta que se incline para baixo da esquerda para a direita.  
  
5.  Expanda um primitivo excluído para examinar o estado que fez com que ele seja excluído. No **fusão de saída** grupo, mova o ponteiro sobre o **resultado**. Uma dica de ferramenta indica por que o primitivo foi excluído. Nesse cenário, a análise revela que o primitivo foi excluído porque ele falhou no teste de profundidade e, portanto, não contribuiu para a cor final do pixel.  
  
 Depois de determinar que a geometria não aparecer porque seus primitivos de falha no teste de profundidade, você pode suspeitar que esse problema está relacionado ao estado do dispositivo configurado incorretamente. Estado do dispositivo e outros Direct3D objeto de dados podem ser examinados usando o **tabela de objetos gráficos**.  
  
#### <a name="to-examine-device-state"></a>Para examinar o estado do dispositivo  
  
1.  Abra o **tabela de objetos gráficos** janela. Sobre o **diagnóstico de gráficos** barra de ferramentas, escolha **objeto tabela**.  
  
2.  Localize o **dispositivo D3D10** objeto o **tabela de objetos gráficos**e, em seguida, abra o **dispositivo D3D10** objeto. Um novo **dispositivo d3d10** guia é aberta no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]. Para facilitar essa tarefa, você pode classificar o **tabela de objetos gráficos** por **tipo**:  
  
     ![Tabela de objetos gráficos e estado do dispositivo relacionados](media/vsg_walkthru1_objtable.png "vsg_walkthru1_objtable")  
  
3.  Examine o estado do dispositivo que é exibido no **dispositivo d3d10** guia problemas potenciais. Como a geometria não aparece porque seus primitivos de falha no teste de profundidade, você pode se concentrar no estado do dispositivo, como estêncil de profundidade, o que afeta o teste de profundidade. Nesse cenário, o **descrição de estêncil de profundidade** (em **saída o estado de fusão**) contém um valor comum para o **função profundidade** membro, `D3D10_COMPARISON_GREATER`:  
  
     ![Janela de dispositivo D3D10 mostrando informações de estêncil de profundidade](media/vsg_walkthru1_devicestate.png "vsg_walkthru1_devicestate")  
  
 Depois de determinar que a causa do problema de renderização pode ser uma função de profundidade configuradas incorretamente, pode usar essas informações junto com seu conhecimento sobre o código para localizar onde a função de profundidade foi definida incorretamente e, em seguida, corrija o problema. Se você estiver familiarizado com o código, você pode procurar o problema usando as dicas que você coletou enquanto você estava depurando — por exemplo, com base no **descrição de estêncil de profundidade** neste cenário, você pode pesquisar o código de palavras como "profundidade" ou "GREATER". Depois de corrigir o código, recriá-lo e executar o aplicativo novamente para descobrir se o problema de renderização é resolvido:  
  
 ![Depois de corrigir o problema de aplicativo](media/vsg_walkthru1_finalview.png "vsg_walkthru1_finalview")