---
title: Gerenciamento de componente | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- installation [Visual Studio SDK], components
- installation [Visual Studio SDK], file management
ms.assetid: 029bffa2-6841-4caa-a41a-442467e1aedc
caps.latest.revision: "13"
author: gregvanl
ms.author: gregvanl
manager: ghogen
ms.workload: vssdk
ms.openlocfilehash: 398986499732a36819808b07f05f7d6b46787a94
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="component-management"></a>Gerenciamento de componentes
Unidades de tarefas do Windows Installer são chamadas de componentes do Windows Installer (às vezes chamados de WICs ou apenas componentes). Um GUID que identifica cada WIC, que é a unidade básica de instalação e para instalações que usam o Windows Installer de contagem de referência.  
  
 Embora você possa usar vários produtos para criar o instalador de seu VSPackage, essa discussão assume o uso de arquivos do Windows Installer (. msi). Ao criar o instalador, você deve gerenciar corretamente a implantação de arquivos para que a contagem de referência correto ocorre em todos os momentos. Consequentemente, versões diferentes do produto não interferir ou quebra entre si em uma combinação de instalar e desinstalar cenários.  
  
 No Windows Installer, a contagem de referência ocorre no nível do componente. Você deve organizar cuidadosamente os recursos — arquivos, entradas do registro e assim por diante – em componentes. Existem outros níveis de organização, como produtos, recursos e módulos — que pode ajudar em cenários diferentes. Para obter mais informações, consulte [Noções básicas do Windows Installer](../../extensibility/internals/windows-installer-basics.md).  
  
## <a name="guidelines-of-authoring-setup-for-side-by-side-installation"></a>Diretrizes de criação de instalação lado a lado  
  
-   Arquivos de autor e chaves do registro que são compartilhadas entre versões em seus próprios componentes.  
  
     Isso permite que você facilmente consumi-los na próxima versão. Por exemplo, as bibliotecas de tipos que são registradas globalmente, arquivo extensões, outros itens registrados em HKEY_CLASSES_ROOT e assim por diante.  
  
-   Grupo de componentes compartilhados em módulos de mesclagem separada.  
  
     Isso ajuda a você criar corretamente para lado a lado no futuro.  
  
-   Instale arquivos compartilhados e chaves do registro usando os mesmos componentes do Windows Installer por meio de versões.  
  
     Se você usar um componente diferente, arquivos e entradas do registro são desinstaladas quando um VSPackage com controle de versão é desinstalado, mas o VSPackage outro ainda está instalado.  
  
-   Não misture os itens compartilhados e com controle de versão no mesmo componente.  
  
     Isso torna impossível instalar itens compartilhados em um local global e itens com controle de versão a isoladas locais.  
  
-   Não tem chaves do registro compartilhado que apontam para arquivos com controle de versão.  
  
     Se você fizer isso, as chaves compartilhadas serão substituídas quando outro VSPackage com controle de versão está instalada. Depois de remover a segunda versão, o arquivo ao qual a chave está apontando será excluído.  
  
## <a name="see-also"></a>Consulte também  
 [Escolhendo entre VSPackages compartilhados e com controle de versão](../../extensibility/choosing-between-shared-and-versioned-vspackages.md)   
 [Cenários de configuração do VSPackage](../../extensibility/internals/vspackage-setup-scenarios.md)