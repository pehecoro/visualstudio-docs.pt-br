---
title: Usar marcadores de texto com a API herdado | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: editors [Visual Studio SDK], legacy - text markers
ms.assetid: 937a0b19-1216-45d5-a7ad-4fe1d6f73097
caps.latest.revision: "16"
author: gregvanl
ms.author: gregvanl
manager: ghogen
ms.workload: vssdk
ms.openlocfilehash: 98c889bc1bc128a941f726348781a633799475de
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="using-text-markers-with-the-legacy-api"></a>Usar marcadores de texto com a API herdado
Um marcador de texto é um intervalo flutuante de texto em um buffer que pode afetar a exibição e o comportamento de uma região de texto. Marcadores de incluem os pontos de interrupção, indicadores, sublinhados ondulados e regiões de somente leitura. Marcadores de texto são basicamente diferentes das cores de sintaxe. Cores de sintaxe é uma maneira rápida de se comunicar a sintaxe de linguagem que está associada uma região do texto. Cores de sintaxe geral é solicitado ao Windows redesenha a tela, quando a velocidade é importante. Cores de sintaxe altera somente a cor do texto. Marcadores de texto podem alterar muitas outras propriedades de texto. Marcadores de texto podem "flutuar" e aplicar um comportamento especial e cores.  
  
 Devido à sobrecarga de desempenho associada com marcadores de texto, não crie muitos marcadores para seus buffers de texto. Cada marcador é atualizado toda vez que um usuário edita o conteúdo do buffer.  
  
> [!NOTE]
>  Os usuários podem alterar a cor de um tipo de marcador visíveis, mas não sua forma e estilo. Para obter mais informações, consulte [fontes e cores, ambiente, caixa de diálogo Opções](../ide/reference/fonts-and-colors-environment-options-dialog-box.md).  
  
## <a name="related-topics"></a>Tópicos relacionados  
  
|Título|Descrição|  
|-----------|-----------------|  
|[Como: adicionar marcadores de texto padrão](../extensibility/how-to-add-standard-text-markers.md)|Descreve como adicionar um tipo de marcador de texto padrão fornecido pelo [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] editor de núcleo para uma exibição de texto.|  
|[Como: implementar marcadores de erro](../extensibility/how-to-implement-error-markers.md)|Descreve como implementar uma instância do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] marcador que é usado para indicar erros usando um sublinhado vermelho ondulado.|  
|[Como: criar marcadores de texto personalizado](../extensibility/how-to-create-custom-text-markers.md)|Descreve como criar e adicionar um tipo de marcador de texto personalizado a um modo de exibição de texto.|  
|[Como: usar marcadores de texto](../extensibility/how-to-use-text-markers.md)|Explica como adicionar marcadores de texto.|  
|[Dentro do Editor de núcleo](../extensibility/inside-the-core-editor.md)|Descreve os recursos do editor de núcleo e fornece detalhes sobre como personalizar o editor de núcleo.|  
|[Recursos do Editor](http://msdn.microsoft.com/en-us/bdac940d-1f14-4019-a01f-fd0bb3dc7198)|Descreve os recursos disponíveis no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] editor de núcleo.|  
  
## <a name="reference"></a>Referência  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsPackageDefinedTextMarkerType>  
 Fornece um mecanismo uniforme para obter informações sobre um tipo de marcador de texto específico, se predefinidos pelo editor ou registrados por um VSPackage.  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLineMarker>  
 Fornece acesso a e ajusta a posição de um marcador de texto em um buffer de texto, usando coordenadas bidimensionais.  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarker>  
 Fornece métodos para gerenciar marcadores de texto.  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient>  
 Fornece retornos de chamada de [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] IDE e outros processos que são usados para ajustar um marcador de texto.  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClientAdvanced>  
 Estende a funcionalidade que está disponível por meio de <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient> interface fornecendo adicionais retornos de chamada.  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClientEx>  
 Estende a funcionalidade que está disponível por meio de <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient> interface fornecendo adicionais retornos de chamada.  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerColorSet>  
 Permite que um tipo de marcador determinar se outros tipos de marcador compartilham o mesmo conjunto de cores.  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerContextProvider>  
 Fornece o contexto para marcadores de texto no editor de núcleo. Para cada tipo de marcador de texto que está no editor de núcleo, o IDE criará uma separada <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerContextProvider> objeto.  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerGlyphDropHandler>  
 Um manipulador que é fornecido para marcadores cujos glifos dão suporte à edição de arrastar e soltar. Um glifo é um ícone que indica a posição de um marcador.  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerTypeProvider>  
 Retorna um <xref:Microsoft.VisualStudio.TextManager.Interop.IVsPackageDefinedTextMarkerType> interface de um serviço que fornece um texto de marcadores a outros VSPackages.  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextStreamMarker>  
 Fornece acesso a e ajusta a posição de um marcador de texto em um buffer de texto, usando coordenadas unidimensionais. Se for possível, não use esta interface.