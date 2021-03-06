---
title: Cores de sintaxe no editores personalizados | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: editors [Visual Studio SDK], custom - syntax coloring
ms.assetid: 74900b9a-baef-432a-8231-4568fb5e19ad
caps.latest.revision: "12"
author: gregvanl
ms.author: gregvanl
manager: ghogen
ms.workload: vssdk
ms.openlocfilehash: 8c40538b34c23e88b2c680db170b9d46b7b40f62
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="syntax-coloring-in-custom-editors"></a>Cores de sintaxe no editores personalizados
Editores do Visual Studio SDK de ambiente, incluindo o editor de núcleo, usam os serviços de idioma para identificar itens sintáticos específicos e exibi-los com cores especificadas para um modo de exibição do documento fornecido.  
  
## <a name="colorization-requirements"></a>Requisitos de colorização  
 Todos os editores de implementação colorizador do serviço de um idioma devem:  
  
1.  Usar um objeto que implementa <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> para gerenciar o texto a ser coloridos e um objeto que implementa <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> para fornecer uma exibição de documento do texto.  
  
2.  Obter uma interface para um serviço de linguagem específica ao consultar o provedor de serviços do VSPackage usando o GUID de identificação do serviço de idiomas.  
  
3.  Chamar o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer.SetLanguageServiceID%2A> método do objeto que implementa <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>. Esse método associa o serviço de linguagem com o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> implementação o VSPackage usa para gerenciar o texto a ser coloridos.  
  
## <a name="core-editor-usage-of-a-language-services-colorizer"></a>Uso de Editor de núcleo de colorizador de um serviço de idioma  
 Quando um serviço de idioma com uma colorizador é obtido por uma instância do editor de núcleo, a análise e renderização de texto por colorizador de um serviço de linguagem ocorre automaticamente sem a necessidade de intervenção adicional de sua parte.  
  
 O IDE transparente:  
  
-   Chama o colorizador conforme necessário para analisar e analisar o texto como ele é adicionado ou modificado na implementação de <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>.  
  
-   Garante que a exibição fornecida pela exibição do documento fornecida pelo <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> implementação é atualizada e pintada novamente usando as informações retornadas pelo colorizador.  
  
## <a name="non-core-editor-usage-of-a-language-services-colorizer"></a>Uso do Editor não essenciais de colorizador de um serviço de idioma  
 Instâncias do editor não-core também podem usar o serviço de coloração de sintaxe de um serviço de linguagem, mas eles explicitamente devem recuperar e aplicar colorizador do serviço e redesenhar seus entre exibições de documento.  
  
 Para fazer isso requer um editor não essenciais para:  
  
1.  Obter o objeto de colorizador do serviço de um idioma (que implementa `T:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer` e <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer2>). O VSPackage faz isso chamando o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetColorizer%2A> método na interface do serviço de linguagem.  
  
2.  Chamar o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> método solicitar coloridos de um determinado intervalo de texto.  
  
     O <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> método retorna uma matriz de valores, uma para cada letra no texto span sendo coloridos. Ele também identifica o trecho de texto como um tipo específico de item pode ser colorido, como um comentário, a palavra-chave ou o tipo de dados.  
  
3.  Use as informações de colorização retornadas por <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> para redesenhar e exibir seu texto.  
  
> [!NOTE]
>  Além de usar colorizador do serviço de um idioma, um VSPackage pode optar por usar o mecanismo de cores de texto para fins gerais do SDK de ambiente do Visual Studio. Para obter mais informações sobre esse mecanismo, consulte [usando fontes e cores](../extensibility/using-fonts-and-colors.md).  
  
## <a name="see-also"></a>Consulte também  
 [Cores de sintaxe em um serviço de linguagem herdado](../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)   
 [Implementando a coloração de sintaxe](../extensibility/internals/implementing-syntax-coloring.md)   
 [Como: usar itens pode ser coloridos internos](../extensibility/internals/how-to-use-built-in-colorable-items.md)   
 [Itens de coloração personalizados](../extensibility/internals/custom-colorable-items.md)