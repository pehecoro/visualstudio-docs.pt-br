---
title: "Instalar interpretadores e bibliotecas Python no Serviço de Aplicativo do Azure | Microsoft Docs"
description: "Como instalar um interpretador e bibliotecas Python no Serviço de Aplicativo do Azure, e configurar os aplicativos Web para fazer referência corretamente a esse interpretador."
ms.custom: 
ms.date: 09/13/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-python
dev_langs:
- python
ms.tgt_pltfrm: 
ms.topic: article
author: kraigb
ms.author: kraigb
manager: ghogen
ms.workload:
- python
- data-science
- azure
ms.openlocfilehash: bc9317615edbf49e35aa0ac3d2ff079beab20df5
ms.sourcegitcommit: 205d15f4558315e585c67f33d5335d5b41d0fcea
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="managing-python-on-azure-app-service"></a>Gerenciando o Python no Serviço de Aplicativo do Azure

O [Serviço de Aplicativo do Azure](https://azure.microsoft.com/services/app-service/) é uma oferta de plataforma como serviço para aplicativos Web, quer eles sejam sites acessados por meio de um navegador, APIs REST usadas por seus próprios clientes ou processamento disparado por evento. O Serviço de Aplicativo dá suporte total ao uso do Python para implementar aplicativos.

O suporte personalizável ao Python no Serviço de Aplicativo do Azure é fornecido como um conjunto de *extensões de site* do Serviço de Aplicativo e cada um contém uma versão específica do tempo de execução do Python. Assim, você pode instalar qualquer pacote desejado diretamente no ambiente, conforme descrito neste tópico. Ao personalizar o ambiente no próprio Serviço de Aplicativo, você não precisa manter pacotes em seus projetos de aplicativo Web ou carregá-los com o código do aplicativo.

> [!Tip]
> Embora o Serviço de Aplicativo tenha o Python 2.7 e o Python 3.4 instalados em pastas raiz no servidor por padrão, você não pode personalizar ou instalar pacotes nesses ambientes, nem deve depender da presença deles. Em vez disso, você deve confiar em uma extensão de site que você controle, conforme descrito neste tópico.

> [!Important]
> Os processos descritos aqui estão sujeitos a alterações e especialmente a aperfeiçoamento. As alterações são anunciadas no [blog Python Engineering at Microsoft](https://blogs.msdn.microsoft.com/pythonengineering/) (Engenharia do Pyhton na Microsoft).

## <a name="choosing-a-python-version-through-the-azure-portal"></a>Escolhendo uma versão do Python por meio do Portal do Azure

1. Crie um Serviço de Aplicativo para seu aplicativo Web no Portal do Azure.
1. Na página do Serviço de Aplicativo, role até a seção **Ferramentas de Desenvolvimento**, selecione **Extensões** e, em seguida, selecione **+ Adicionar**.
1. Role para baixo na lista para a extensão que contém a versão do Python que você deseja:

    ![Portal do Azure mostrando extensões do Python](media/python-on-azure-extensions.png)

    > [!Tip]
    > Se você precisar de uma versão mais antiga do Python e ela não estiver listada nas extensões de site, ainda poderá instalá-la por meio do Azure Resource Manager, conforme descrito na próxima seção.

1. Selecione a extensão, aceite os termos legais e selecione **OK**.
1. Uma notificação será exibida no portal quando a instalação for concluída.

## <a name="choosing-a-python-version-through-the-azure-resource-manager"></a>Escolhendo uma versão do Python por meio do Azure Resource Manager

Se você estiver implantando um Serviço de Aplicativo com um modelo do Azure Resource Manager, adicione a extensão de site como um recurso. A extensão é exibida como um recurso aninhado com o tipo `siteextensions` e o nome de [siteextensions.net](https://www.siteextensions.net/packages?q=Tags%3A%22python%22).

Por exemplo, depois de adicionar uma referência a `python361x64` (Python 3.6.1 x64), o modelo poderá ficar parecido com o seguinte (algumas propriedades foram omitidas):

```json
"resources": [
  {
    "apiVersion": "2015-08-01",
    "name": "[parameters('siteName')]",
    "type": "Microsoft.Web/sites",

    // ...

    "resources": [
      {
        "apiVersion": "2015-08-01",
        "name": "python361x64",
        "type": "siteextensions",
        "properties": { },
        "dependsOn": [
          "[resourceId('Microsoft.Web/sites', parameters('siteName'))]"
        ]
      },
      // ...
    ]
  }
```

## <a name="setting-webconfig-to-point-to-the-python-interpreter"></a>Configurando o web.config para apontar para o interpretador do Python

Depois de instalar a extensão de site (por meio do portal ou de um modelo do Azure Resource Manager), você aponta o arquivo `web.config` do seu aplicativo para o interpretador do Python. O arquivo `web.config` instrui o servidor Web do IIS (7+) em execução no Serviço de Aplicativo sobre como ele deve tratar as solicitações do Python, sendo por meio de FastCGI ou de HttpPlatform.

Comece localizando o caminho completo para o `python.exe` da extensão de site e, em seguida, crie e modifique o arquivo `web.config` apropriado.

### <a name="finding-the-path-to-pythonexe"></a>Localizando o caminho para python.exe

Uma extensão de site do Python é instalada no servidor em `d:\home` em uma pasta apropriada para a versão e arquitetura do Python (exceto no caso de algumas versões mais antigas). Por exemplo, o Python 3.6.1 x64 é instalado em `d:\home\python361x64`. Assim, o caminho completo para o interpretador do Python é `d:\home\python361x64\python.exe`.

Para ver o caminho específico no Serviço de Aplicativo, selecione **Extensões** na página do Serviço de Aplicativo e, em seguida, selecione a extensão na lista.

![Lista de extensão no Serviço de Aplicativo do Azure](media/python-on-azure-extension-list.png)

Essa ação abre a página de descrição da extensão que contém o caminho:

![Detalhes de extensão no Serviço de Aplicativo do Azure](media/python-on-azure-extension-detail.png)

Se tiver problemas para ver o caminho para a extensão, você poderá encontrá-la manualmente usando o console:

1. Na página do Serviço de Aplicativo, selecione **Ferramentas de Desenvolvimento > Console**.
1. Digite o comando `ls ../home` ou `dir ..\home` para ver as pastas de extensões de nível superior, como `Python361x64`.
1. Digite um comando como `ls ../home/python361x64` ou `dir ..\home\python361x64` para verificar se ela contém `python.exe` e outros arquivos de interpretador.

### <a name="configuring-the-fastcgi-handler"></a>Configurando o manipulador do FastCGI

O FastCGI é uma interface que funciona no nível da solicitação. O IIS recebe conexões de entrada e encaminha cada solicitação para um aplicativo WSGI em execução em um ou mais processos Python persistentes. O [pacote wfastcgi](https://pypi.io/project/wfastcgi) é pré-instalado e configurado com cada extensão de site do Python, portanto você pode habilitá-lo facilmente incluindo o código em `web.config` como mostrado abaixo para um aplicativo Web com base na estrutura Bottle. Observe que os caminhos completos para `python.exe` e `wfastcgi.py` são colocados na chave `PythonHandler`:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <appSettings>
    <add key="PYTHONPATH" value="D:\home\site\wwwroot"/>
    <!-- The handler here is specific to Bottle; other frameworks vary. -->
    <add key="WSGI_HANDLER" value="app.wsgi_app()"/>
    <add key="WSGI_LOG" value="D:\home\LogFiles\wfastcgi.log"/>
  </appSettings>
  <system.webServer>
    <handlers>
      <add name="PythonHandler" path="*" verb="*" modules="FastCgiModule"
           scriptProcessor="D:\home\Python361x64\python.exe|D:\home\Python361x64\wfastcgi.py"
           resourceType="Unspecified" requireAccess="Script"/>
    </handlers>
  </system.webServer>
</configuration>
```

As `<appSettings>` definidas aqui estão disponíveis para seu aplicativo como variáveis de ambiente:

- O valor de `PYTHONPATH` pode ser estendido livremente, mas deve incluir a raiz do seu aplicativo.
- `WSGI_HANDLER` deve apontar para um aplicativo WSGI importável do seu aplicativo.
- `WSGI_LOG` é opcional, mas recomendado para depuração do seu aplicativo. 

Consulte [Publicar no Azure](publishing-python-web-applications-to-azure-from-visual-studio.md) para obter detalhes adicionais sobre conteúdos de `web.config` para aplicativos Web de Bottle, Flask e Django.

### <a name="configuring-the-httpplatform-handler"></a>Configurando o manipulador HttpPlatform

O módulo HttpPlatform passa conexões de soquete diretamente para um processo de Python autônomo. Essa passagem permite que você execute qualquer servidor Web que desejar, mas requer um script de inicialização que executa um servidor Web local. Você especifica o script no elemento `<httpPlatform>` do `web.config`, em que o atributo `processPath` aponta para o interpretador do Python da extensão de site e o atributo `arguments` aponta para seu script e os argumentos que você quiser fornecer:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.webServer>
    <handlers>
      <add name="PythonHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified"/>
    </handlers>
    <httpPlatform processPath="D:\home\Python361x64\python.exe"
                  arguments="D:\home\site\wwwroot\runserver.py --port %HTTP_PLATFORM_PORT%"
                  stdoutLogEnabled="true"
                  stdoutLogFile="D:\home\LogFiles\python.log"
                  startupTimeLimit="60"
                  processesPerApplication="16">
      <environmentVariables>
        <environmentVariable name="SERVER_PORT" value="%HTTP_PLATFORM_PORT%" />
      </environmentVariables>
    </httpPlatform>
  </system.webServer>
</configuration>
```

A variável de ambiente `HTTP_PLATFORM_PORT` mostrada aqui contém a porta que o servidor local deve escutar para as conexões do localhost. Este exemplo também mostra como criar outra variável de ambiente, se desejado, nesse caso `SERVER_PORT`.

## <a name="installing-packages"></a>Instalando pacotes

O interpretador do Python instalado por meio de uma extensão de site é apenas uma parte do seu ambiente do Python. Você provavelmente precisará instalar pacotes diferentes nesse mesmo ambiente.

Para instalar pacotes diretamente no ambiente do servidor, use um dos seguintes métodos:

| Métodos | Uso |
| --- | --- |
| [Console do Kudu do Serviço de Aplicativo do Azure](#azure-app-service-kudu-console) | Instala pacotes interativamente. Os pacotes devem ser Python puro ou publicar em wheels. |
| [API REST do Kudu](#kudu-rest-api) | Pode ser usada para automatizar a instalação de pacote.  Os pacotes devem ser Python puro ou publicar em wheels. |
| Pacote com aplicativo | Instala pacotes diretamente em seu projeto e, em seguida, implanta-os no Serviço de Aplicativo como se fizessem parte do seu aplicativo. Dependendo de quantas dependências você tem e da frequência com que você os atualiza, esse método pode ser a maneira mais fácil de dar início à implantação. Esteja ciente de que as bibliotecas devem corresponder à versão do Python no servidor, caso contrário, você verá erros obscuros após a implantação. Assim, como as versões do Python nas extensões de site do Serviço de Aplicativo são exatamente as mesmas que as versões lançadas em python.org, você pode obter uma versão compatível para desenvolvimento local facilmente. |
| Ambientes virtuais | Sem suporte. Em vez disso, use o agrupamento e defina a variável de ambiente `PYTHONPATH` para apontar para o local dos pacotes. |

### <a name="azure-app-service-kudu-console"></a>Console do Kudu do Serviço de Aplicativo do Azure

O [console Kudu](https://github.com/projectkudu/kudu/wiki/Kudu-console) fornece acesso de linha de comando com privilégios elevados e direto para o servidor do Serviço de Aplicativo e seu sistema de arquivos. Isso é uma ferramenta valiosa de depuração e também permite operações de CLI, como instalação de pacotes.

1. Abra o Kudu na sua página do Serviço de Aplicativo no Portal do Azure, selecionando **Ferramentas de Desenvolvimento > Ferramentas Avançadas** e, em seguida, selecionando **Ir**. Essa ação navega até uma URL que é a mesmo que a URL base do Serviço de Aplicativo, exceto pelo `.scm` inserido. Por exemplo, se a URL base for `https://vspython-test.azurewebsites.net/`, o Kudu será `https://vspython-test.scm.azurewebsites.net/` (que você poderá adicionar aos favoritos):

    ![O console do Kudu para o Serviço de Aplicativo do Azure](media/python-on-azure-console01.png)

1. Selecione **Console de depuração > CMD** para abrir o console, no qual você pode navegar em sua instalação do Python e ver quais bibliotecas já estão lá.

1. Para instalar um único pacote:

    a. Navegue até a pasta da instalação do Python em que você deseja instalar o pacote, como `d:\home\python361x64`.

    b. Use `python.exe -m pip install <package_name>` para instalar um pacote.

    ![Exemplo de instalação do Bottle por meio do console do Kudu para o Serviço de Aplicativo do Azure](media/python-on-azure-console02.png)

1. Se você já implantou um `requirements.txt` para seu aplicativo no servidor, instale todos esses requisitos da seguinte maneira:

    a. Navegue até a pasta da instalação do Python em que você deseja instalar o pacote, como `d:\home\python361x64`.

    b. Execute o comando `python.exe -m pip install --upgrade -r d:\home\site\wwwroot\requirements.txt`.

    O uso do `requirements.txt` é recomendado porque é fácil reproduzir seu conjunto de pacote exato localmente e no servidor. Lembre-se visitar o console depois de implantar as alterações no `requirements.txt` e execute o comando novamente.

> [!Note]
> Não há compilador de C no Serviço de Aplicativo, portanto você precisa instalar o wheel para todos os pacotes com módulos de extensão nativos. Muitos pacotes populares fornecem suas próprias rodas. Para pacotes que não o fazem, use `pip wheel <package_name>` em seu computador de desenvolvimento local e, em seguida, carregue a roda para seu site. Para obter um exemplo, veja [Gerenciar os pacotes necessários](managing-python-environments-in-visual-studio.md#managing-required-packages-requirementstxt).

### <a name="kudu-rest-api"></a>API REST do Kudu

Em vez de usar o console de Kudu por meio do portal do Azure, você pode executar comandos remotamente por meio da API REST do Kudu postando o comando para `https://yoursite.scm.azurewebsites.net/api/command`. Por exemplo, para instalar o pacote `bottle`, poste o seguinte JSON para `/api/command`:

```json
{
    "command": 'python.exe -m pip install bottle',
    "dir": '\home\python361x64'
}
```

Para obter informações sobre comandos e autenticação, consulte a [Documentação do Kudu](https://github.com/projectkudu/kudu/wiki/REST-API).

Você também pode ver as credenciais usando o comando `az webapp deployment list-publishing-profiles` através da CLI do Azure (consulte [az webapp deployment](/cli/azure/webapp/deployment?view=azure-cli-latest#az_webapp_deployment_list_publishing_profiles)). Há uma biblioteca auxiliar para publicar comandos de Kudu disponível no [GitHub](https://github.com/lmazuel/azure-webapp-publish/blob/master/azure_webapp_publish/kudu.py#L42).
