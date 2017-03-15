---
title: "Usar parâmetros de linha de comando para instalar o Visual Studio | Microsoft Docs"
ms.custom: 
ms.date: 02/14/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-install
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- command-line parameters
- switches
- command prompt
ms.assetid: 480f3cb4-d873-434e-a8bf-82cff7401cf2
author: TerryGLee
ms.author: tglee
manager: ghogen
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: d4d1bd45ce697017480b3f63d0c7feb5ab20d2d6
ms.openlocfilehash: 18a3d03663ac96e0751d4a420244b835be7146bf
ms.lasthandoff: 02/22/2017

---
# <a name="use-command-line-parameters-to-install-visual-studio-2017-rc"></a>Usar parâmetros de linha de comando para instalar o Visual Studio 2017 RC
Quando você instala o Visual Studio 2017 RC em um prompt de comando, você pode usar os parâmetros de linha de comando a seguir (também conhecidos como opções).  

## <a name="list-of-command-line-parameters"></a>Lista de parâmetros de linha de comando  
 Parâmetros de linha de comando do Visual Studio não diferenciam maiúsculas de minúsculas.  

| **Comando de linha de comando** | **Descrição** |
| ----------------------- | --------------- |  
| ```modify``` | Modifica um produto instalado. |
| ```update``` | Atualiza um produto instalado. |
| ```repair``` | Repara um produto instalado. |
| ```uninstall``` | Desinstala um produto instalado. |

Se nenhum comando for especificado, ele instalará o produto.

| **Opção de linha de comando** | **Descrição** |
| ----------------------- | --------------- |  
| ```--installPath <dir>``` | O diretório de instalação no qual a instância deverá agir. Para o comando de instalação, é onde a instância será instalada. Para outros comandos, é onde a instância instalada anteriormente foi instalada. |
| ```--productId <id>``` | A ID do produto para a instância que será instalada. Isso é necessário para o comando de instalação, ignorado para outros comandos se --installPath está especificado. |
| ```--layout <dir>``` | Opcional: especifica um diretório para criar um cache de instalação offline. A seleção dessa opção também adicionará implicitamente a opção “-wait”. |
| ```--lang <language-locale>``` *[&#60;localidade de idioma&#62; ...]* | Opcional: instalar e desinstalar pacotes de recursos com os idiomas especificados. |
| ```--add <workload or component ID>``` *[&#60;ID do componente ou carga de trabalho&#62; ...]* | Opcional: uma ou mais IDs de componente ou carga de trabalho para adicionar. Os componentes obrigatórios do artefato são instalados, mas não os componentes recomendados ou opcionais. É possível controlar os componentes adicionais globalmente usando “--includeRecommended” e/ou “--includeOptional”. Para um controle mais refinado, é possível acrescentar “;includeRecommended” e/ou “;includeOptional” à artifactId (por exemplo, “--add Workload1;includeRecommended” ou “--add Workload2;includeOptional;includeRecommended”). |
| ```--remove <workload or component ID>``` *[&#60;ID do componente ou carga de trabalho&#62; ...]* | Opcional: uma ou mais IDs de componente ou carga de trabalho para remover. |
| ```--all``` | Opcional: se deseja instalar todas as cargas de trabalho e componentes de um produto. |
| ```--allWorkloads``` | Opcional: instala todas as cargas de trabalho e seus componentes obrigatórios, mas nenhum componente recomendado ou opcional. |
| ```--includeRecommended``` | Opcional: inclui os componentes recomendados para quaisquer cargas de trabalho que estão instalados, mas não os componentes opcionais. As cargas de trabalho são especificadas com --allWorkloads ou --add. |
| ```--includeOptional``` | Opcional: inclui os componentes opcionais para quaisquer cargas de trabalho que estão instalados, mas não os componentes recomendados. As cargas de trabalho são especificadas com --allWorkloads ou --add.  |
| ```--quiet, -q``` | Opcional: não exibir nenhuma interface do usuário ao executar a instalação. |
| ```--passive, -p``` | Opcional: exibir a interface do usuário, mas não solicitar nenhuma interação do usuário. |
| ```--norestart``` | Opcional: se estiver presente, comandos com --passive ou --quiet não reiniciarão automaticamente o computador (se necessário). Isso será ignorado se nem --passive tampouco --quiet forem especificados.  |
| ```--locale <language-locale>``` | Opcional: alterar o idioma de exibição da interface do usuário para o instalador. A configuração será mantida. |
| ```--nickname <name>``` | Opcional: define o apelido a atribuir a um produto instalado. O apelido não pode ter mais de 10 caracteres.  |
| ```--help, --?, -h, -?``` | Exibir o uso do parâmetro. |

>Observação: ao especificar várias cargas de trabalho e vários componentes, é necessário repetir a opção de linha de comando `--add` ou `--remove` para cada item.

| **Opção de linha de comando avançada** | **Descrição** |
| ----------------------- | --------------- |  
| ```--channelId <id>``` | Opcional: a ID do canal para a instância que será instalada. Isso é necessário para o comando de instalação, ignorado para outros comandos se --installPath está especificado. |
| ```--channelUri <uri>``` | Opcional: o URI do manifesto do canal. Isso pode ser usado para o comando de instalação e é ignorado para outros comandos. |
| ```--installChannelUri <uri>``` | Opcional: o URI do manifesto do canal a ser usado para a instalação. O URI especificado pelo --channelUri (que deve ser especificado quando --installChannelUri é especificado) será usado para detectar atualizações. Se as atualizações não forem desejadas, --channelUri deverá ser especificado sem um argumento. Isso pode ser usado para o comando de instalação e é ignorado para outros comandos. |
| ```--installCatalogUri <uri>``` | Opcional: o URI do manifesto do catálogo a ser usado para a instalação. Se especificado, o gerente de canal tentará baixar o manifesto do catálogo desse URI antes de usar o URI no manifesto do canal de instalação. Esse parâmetro é usado para dar suporte a instalação offline, em que o cache de layout será criado com o catálogo de produtos que já foi baixado. Isso pode ser usado para o comando de instalação e é ignorado para outros comandos. |
| ```--in <path>``` | Opcional: o URI ou o caminho para um arquivo de resposta.  |
| ```--addProductLang <language-locale>``` | Opcional: define o idioma de um artefato (grupo, carga de trabalho ou componente) que será instalado. Ele pode aparecer várias vezes na linha de comando. É opcional para a instalação e modificação de comandos, ignorado para a atualização, reparo e desinstalação de comandos. Se não estiver presente, a instalação usará a localidade do computador. |
| ```--removeProductLang <language-locale>``` | Opcional: isso define o idioma de um artefato (grupo, carga de trabalho ou componente) a ser removido. Ele pode aparecer várias vezes na linha de comando. É opcional para a instalação e modificação de comandos, ignorado para a atualização, reparo e desinstalação de comandos. |
| ```--wait``` | Opcional: o processo aguardará até que a instalação seja concluída antes de retornar um código de saída. Isso é útil ao automatizar instalações em que é necessário aguardar a conclusão da instalação para tratar o código de retorno da instalação. |
| ```--productKey``` | Opcional: isso define a chave do produto (Product Key) a ser usada para um produto instalado. Ela é composta por 25 caracteres alfanuméricos, no formato “xxxxx-xxxxx-xxxxx-xxxxx-xxxxx” ou “xxxxxxxxxxxxxxxxxxxxxxxxx”. |
## <a name="list-of-workload-ids-and-component-ids"></a>Lista de IDs de carga de trabalho e IDs de componente
Para obter uma lista de IDs de componente e de carga de trabalho classificadas por produto do Visual Studio, consulte nossa página [Visual Studio 2017 Workload and Component IDs (IDs de componente e de carga de trabalho do Visual Studio 2017)](https://aka.ms/vs2017componentids).

> [!WARNING]
> O parâmetro --layout falhará se o nome do arquivo .exe de instalação incluir numerais. Para resolver esse problema, é necessário remover os numerais do nome do arquivo – por exemplo, renomeie *vs_community__198521760.1486960229.exe* como ***vs_community.exe***.

## <a name="list-of-language-locales"></a>Lista de localidades de idioma
| **Localidade de idioma** | **Linguagem** |
| ----------------------- | --------------- |  
| cs-CZ | Tcheco |
| de-DE | Alemão |
| pt-BR | Inglês |
| es-ES | Espanhol |
| cs-CZ | Tcheco |
| fr-FR | Francês |
| it-IT | Italiano |
| ja-JP | Japonês |
| ko-KR | Coreano |
| pl-PL | Polonês |
| pt-BR | Português - Brasil |
| ru-RU | Russo |
| tr-TR | Turco |
| zh-CN | Chinês – Simplificado |
| zh-TW | Chinês – Tradicional |



> [!IMPORTANT]
> Embora o Visual Studio 2017 RC, de modo geral, tenha suporte para uso em um ambiente de produção, as cargas de trabalho e componentes que estão marcados como "Visualização" na interface do usuário da instalação não têm suporte para uso em ambiente de produção.

## <a name="see-also"></a>Consulte também

 * [Instalar o Visual Studio](install-visual-studio.md)
 * [Criar uma instalação offline do Visual Studio 2017 RC](create-an-offline-installation-of-visual-studio.md)
 * [Relatar um problema com o Visual Studio](../ide/how-to-report-a-problem-with-visual-studio-2017.md)
