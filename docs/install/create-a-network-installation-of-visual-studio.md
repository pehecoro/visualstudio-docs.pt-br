---
title: "Criar uma instalação baseada em rede do Visual Studio | Microsoft Docs"
description: "Descreve como criar um ponto de instalação de rede para implantação do Visual Studio em uma empresa"
ms.date: 10/17/2017
ms.reviewer: 
ms.suite: 
ms.technology: vs-acquisition
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- '{{PLACEHOLDER}}'
- '{{PLACEHOLDER}}'
ms.assetid: 4CABFD20-962E-482C-8A76-E4012052F701
author: timsneath
ms.author: tglee
manager: ghogen
ms.workload: multiple
ms.openlocfilehash: f5e6c5a94ac4c875922d2da09e9171f4929035f8
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="create-a-network-installation-of-visual-studio-2017"></a>Criar uma instalação de rede do Visual Studio 2017

Normalmente, um administrador corporativo cria um ponto de instalação de rede para implantação em estações de trabalho cliente. Criamos o Visual Studio de 2017 para permitir que você armazene em cache os arquivos para a instalação inicial juntamente com todas as atualizações de produto para uma única pasta. (Esse processo também é referido como _criação de um layout_.) Fizemos isso para que as estações de trabalho cliente pudessem usar o mesmo local de rede para gerenciar sua instalação, mesmo que elas ainda não tivessem sido atualizadas para a atualização de serviço mais recente.

 > [!NOTE]
 > Se você tiver várias edições do Visual Studio em uso em sua empresa (por exemplo, o Visual Studio Professional e o Visual Studio Enteprise), precisará criar um compartilhamento de instalação de rede separado para cada edição.

## <a name="download-the-visual-studio-bootstrapper"></a>Baixar o bootstrapper do Visual Studio

**Baixe** a edição do Visual Studio desejada. Lembre-se de clicar em **Salvar** e, em seguida, clique em **Abrir pasta**.

O executável de instalação &mdash; ou para ser mais específico, um arquivo bootstrapper &mdash; deverá corresponder a um dos listados a seguir.

|Edição | Baixar|
|-------------|-----------------------|
|Visual Studio Enterprise | [**vs_enterprise.exe**](https://aka.ms/vs/15/release/vs_enterprise.exe) |
|Visual Studio Professional | [**vs_professional.exe**](https://aka.ms/vs/15/release/vs_professional.exe) |
|Comunidade Visual Studio | [**vs_community.exe**](https://aka.ms/vs/15/release/vs_community.exe) |

Outros bootstrappers com suporte incluem [vs_buildtools.exe](https://aka.ms/vs/15/release/vs_buildtools.exe), [vs_feedbackclient.exe](https://aka.ms/vs/15/release/vs_feedbackclient.exe), [vs_teamexplorer.exe](https://aka.ms/vs/15/release/vs_teamexplorer.exe), [vs_testagent.exe](https://aka.ms/vs/15/release/vs_testagent.exe), [vs_testcontroller.exe](https://aka.ms/vs/15/release/vs_testcontroller.exe) e [vs_testprofessional.exe](https://aka.ms/vs/15/release/vs_testprofessional.exe).

## <a name="create-an-offline-installation-folder"></a>Criar uma pasta de instalação offline

É preciso ter uma conexão com a Internet para concluir esta etapa. Para criar uma instalação offline com todos os idiomas e recursos, use um dos comandos dos exemplos a seguir.

   > [!IMPORTANT]
   > Um layout completo do Visual Studio 2017 exige, pelo menos, 35 GB de espaço em disco e pode demorar um pouco para ser baixado.  Confira a seção [Personalizando o layout da rede](#customizing-the-network-layout) para obter detalhes sobre como criar um layout com os componentes que deseja instalar.

   > [!TIP]
   > Lembre-se de executar o comando no diretório de Download. Normalmente, isso é `C:\Users\<username>\Downloads` em um computador que executa o Windows 10.

- Para o Visual Studio Enterprise, execute:

  ```vs_enterprise.exe --layout c:\vs2017offline```

- Para o Visual Studio Professional, execute:

  ```vs_professional.exe --layout c:\vs2017offline```

- Para o Visual Studio Community, execute:

  ```vs_community.exe --layout c:\vs2017offline```

## <a name="modify-the-responsejson-file"></a>Modificar o arquivo response.json

Você pode modificar response.json para definir valores padrão que serão usados quando a instalação for executada.  Por exemplo, você pode configurar o arquivo `response.json` para selecionar um conjunto específico de cargas de trabalho selecionadas automaticamente.
Confira [Automatizar a instalação do Visual Studio com um arquivo de resposta](automated-installation-with-response-file.md) para obter detalhes.

## <a name="copy-the-layout-to-a-network-share"></a>Copiar o layout para um compartilhamento de rede

Hospede o layout em um compartilhamento de rede para que ele possa ser executado de outros computadores.
* Exemplo:<br>
```xcopy /e c:\vs2017offline \\server\products\VS2017```

## <a name="customizing-the-network-layout"></a>Personalização do layout de rede

Há várias opções que você pode usar para personalizar o layout de rede. Você pode criar um layout parcial que contém apenas um conjunto específico de [localidades de idiomas](use-command-line-parameters-to-install-visual-studio.md#list-of-language-locales), [cargas de trabalho, componentes e suas dependências recomendadas ou opcionais](workload-and-component-ids.md). Isso poderá ser útil se você souber que só pretende implantar um subconjunto de cargas de trabalho em estações de trabalho cliente. Parâmetros de linha de comando típicos para personalizar o layout incluem:

* ```--add``` para especificar [IDs de componente ou carga de trabalho](workload-and-component-ids.md).  Se `--add` for usado, somente as cargas de trabalho e os componentes especificados com `--add` serão baixados.  Se `--add` não for usado, todas as cargas de trabalho e todos os componentes serão baixados.
* ```--includeRecommended``` para incluir todos os componentes recomendados para as IDs de carga de trabalho especificadas
* ```--includeOptional``` para incluir todos os componentes recomendados e opcionais para as IDs de carga de trabalho especificadas.
* ```--lang``` para especificar [localidades de idiomas](use-command-line-parameters-to-install-visual-studio.md#list-of-language-locales).

Aqui estão alguns exemplos de como criar um layout personalizado parcial.

* Para baixar todas as cargas de trabalho e todos os componentes para um único idioma, execute: <br>```vs_enterprise.exe --layout C:\vs2017offline --lang en-US```
* Para baixar todas as cargas de trabalho e todos os componentes para vários idiomas, execute: <br>```vs_enterprise.exe --layout C:\vs2017offline --lang en-US de-DE ja-JP```
* Para baixar uma carga de trabalho para todos os idiomas, execute <br> ```vs_enterprise.exe --layout C:\vs2017offline --add Microsoft.VisualStudio.Workload.Azure --includeRecommended```
* Para baixar duas cargas de trabalho e um componente opcional para três idiomas, execute: <br>```vs_enterprise.exe --layout C:\vs2017offline --add Microsoft.VisualStudio.Workload.Azure --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Component.GitHub.VisualStudio --includeRecommended --lang en-US de-DE ja-JP ```
* Para baixar duas cargas de trabalho e todos os seus componentes recomendados, execute: <br>```vs_enterprise.exe --layout C:\vs2017offline --add Microsoft.VisualStudio.Workload.Azure --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Component.GitHub.VisualStudio --includeRecommended ```
* Para baixar duas cargas de trabalho e todos os seus componentes opcionais e recomendados, execute: <br>```vs_enterprise.exe --layout C:\vs2017offline --add Microsoft.VisualStudio.Workload.Azure --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Component.GitHub.VisualStudio --includeOptional ```

### <a name="new-in-153"></a>Novidade no 15.3

Quando você executa um comando de layout, as opções que você especifica são salvas (por exemplo, as cargas de trabalho e os idiomas). Comandos de layout subsequentes incluirão todas as opções anteriores.  Aqui está um exemplo de um layout com uma carga de trabalho apenas para inglês:

```vs_enterprise.exe --layout c:\VS2017Layout --add Microsoft.VisualStudio.Workload.ManagedDesktop --lang en-US```

Quando você quer atualizar o layout para uma versão mais recente, não é necessário especificar nenhum parâmetro de linha de comando adicional. As configurações anteriores são salvas e usadas por quaisquer comandos de layout subsequentes nesta pasta de layout.  O comando seguinte atualizará o layout parcial existente.

```vs_enterprise.exe --layout c:\VS2017Layout```

Você pode consultar aqui um exemplo de como adicionar uma carga de trabalho adicional. Nesse caso, vamos adicionar a carga de trabalho do Azure e um idioma traduzido.  Agora, tanto a Área de Trabalho Gerenciada quanto o Azure são incluídos neste layout.  Os recursos de idioma para inglês e alemão estão incluídos para todas essas cargas de trabalho. O layout é atualizado para a versão mais recente disponível.

```vs_enterprise.exe --layout c:\VS2017Layout --add Microsoft.VisualStudio.Workload.Azure --lang de-DE```

Se você deseja atualizar um layout existente para um layout completo, use a opção --all, conforme mostrado no exemplo a seguir.

```vs_enterprise.exe --layout c:\VS2017Layout --all```


## <a name="deploying-from-a-network-installation"></a>Implantação de uma instalação de rede

Os administradores podem implantar o Visual Studio em estações de trabalho cliente como parte de um script de instalação. Ou, os usuários que têm direitos de administrador podem executar a instalação diretamente do compartilhamento para instalar o Visual Studio em seu computador.

- Os usuários podem instalar executando: <br>```\\server\products\VS2017\vs_enterprise.exe```
- Os administradores podem fazer a instalação em um modo autônomo executando: <br>```\\server\products\VS2017\vs_enterprise.exe --quiet --wait --norestart```

> [!TIP]
> Quando executada como parte de um arquivo em lotes, a opção `--wait` garante que o processo `vs_enterprise.exe` aguarde até que a instalação seja concluída antes de ela retornar um código de saída. Isso é útil se um administrador corporativo deseja executar ações adicionais em uma instalação concluída (por exemplo, para [aplicar uma chave do produto (Product Key) a uma instalação bem-sucedida](automatically-apply-product-keys-when-deploying-visual-studio.md)), mas precisa aguardar a conclusão da instalação para obter o código de retorno dessa instalação.  Se você não usar `--wait`, o processo `vs_enterprise.exe` será encerrado antes que a instalação seja concluída e retornará um código de saída impreciso, que não representará o estado da operação de instalação.

Quando você instala com base em um layout, o conteúdo instalado é adquirido do layout. No entanto, se você selecionar um componente que não está no layout, ele será adquirido da Internet.  Se você quiser impedir que a instalação do Visual Studio baixe qualquer conteúdo que está ausente em seu layout, use a opção `--noWeb`.  Se `--noWeb` for usado e o layout não tiver qualquer conteúdo selecionado a ser instalado, a configuração falhará.  

### <a name="error-codes"></a>Códigos de erro

Se você tiver usado o parâmetro `--wait`, dependendo do resultado da operação, a variável de ambiente `%ERRORLEVEL%` será definida como um dos seguintes valores:

  | **Value** | **Result** |
  | --------- | ---------- |
  | 0 | A operação foi concluída com êxito |
  | 3010 | A operação foi concluída com êxito, mas a instalação requer a reinicialização antes de ser usada |
  | Outros | Condição de falha ocorreu. Verifique os logs para obter mais informações |

## <a name="updating-a-network-install-layout"></a>Atualização de um layout de instalação de rede

Quando atualizações de produto se tornam disponíveis, pode-se [atualizar o layout de instalação de rede](update-a-network-installation-of-visual-studio.md) para incorporar pacotes atualizados.

## <a name="how-to-create-a-layout-for-a-previous-visual-studio-2017-release"></a>Como criar um layout para uma versão anterior do Visual Studio 2017

> [!NOTE]
> Os bootstrappers do Visual Studio 2017 disponíveis em [VisualStudio.com](http://www.visualstudio.com) baixarão e instalarão a versão mais recente do Visual Studio 2017 disponível sempre que forem executados. Se você baixar um bootstrapper Visual Studio hoje e executá-lo daqui a seis meses, ele instalará a versão Visual Studio 2017 disponível nesse momento posterior. Se você criar um layout, a instalação do Visual Studio por meio desse layout instalará a versão específica do Visual Studio que existe no layout. Mesmo que uma versão mais recente exista online, você obterá a versão do Visual Studio que está no layout.

Se você precisar criar um layout para uma versão anterior do Visual Studio 2017, acesse https://my.visualstudio.com e baixe versões "corrigidas" de bootstrappers do Visual Studio 2017.

### <a name="how-to-get-support-for-your-offline-installer"></a>Como obter suporte para o instalador offline

Caso tenha um problema com a instalação offline, gostaríamos de saber a respeito. A melhor maneira de fazer isso é usando a ferramenta [Relatar um Problema](../ide/how-to-report-a-problem-with-visual-studio-2017.md). Ao usar essa ferramenta, é possível enviar-nos a telemetria e os logs necessários para nos ajudar a diagnosticar e corrigir o problema.

Também temos outras opções de suporte disponíveis. Para obter uma lista delas, consulte nossa página [Fale conosco](../ide/how-to-report-a-problem-with-visual-studio-2017.md).

## <a name="get-support"></a>Obter suporte
Às vezes, as coisas podem dar errado. Caso a instalação do Visual Studio falhe, confira a página [Solução de problemas de instalação e atualização do Visual Studio 2017](troubleshooting-installation-issues.md). Se nenhuma das etapas de solução de problemas ajudar, entre em contato conosco por meio de um chat ao vivo para obter ajuda com a instalação (somente em inglês). Para saber mais detalhes, confira a [página de suporte do Visual Studio](https://www.visualstudio.com/vs/support/#talktous).

Aqui estão algumas outras opções de suporte:
* Você pode nos relatar problemas do produto por meio da ferramenta [Relatar um Problema](../ide/how-to-report-a-problem-with-visual-studio-2017.md), exibida no Instalador do Visual Studio e no IDE do Visual Studio.
* Você pode compartilhar uma sugestão de produto conosco no [UserVoice](https://visualstudio.uservoice.com/forums/121579).
* É possível acompanhar os problemas do produto na [Comunidade de Desenvolvedores do Visual Studio](https://developercommunity.visualstudio.com/), além de fazer perguntas e encontrar respostas.
* Você pode também interagir conosco e com outros desenvolvedores do Visual Studio por meio das [conversas sobre o Visual Studio na comunidade do Gitter](https://gitter.im/Microsoft/VisualStudio).  (Esta opção requer uma conta do [GitHub](https://github.com/).)

## <a name="see-also"></a>Consulte também
* [Instalar o Visual Studio](install-visual-studio.md)
* [Guia do administrador do Visual Studio](visual-studio-administrator-guide.md)
* [Usar parâmetros de linha de comando para instalar o Visual Studio](use-command-line-parameters-to-install-visual-studio.md)
* [Carga de trabalho do Visual Studio e IDs do componente](workload-and-component-ids.md)
