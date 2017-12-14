# <a name="create-an-ai-project-from-existing-code"></a>Criar um projeto IA com base no código existente

Depois de [instalar as Ferramentas do Visual Studio para IA](installation.md), é fácil colocar o código Python existente em um projeto do Visual Studio. 

> [!Important]
>
> O processo descrito aqui não move ou copia os arquivos de origem. Se você quiser trabalhar com uma cópia, basta primeiro duplicar a pasta.

1. Inicie o Visual Studio e selecione **Arquivo > Novo > Projeto**.

1. Na caixa de diálogo **Novo projeto**, pesquise "**Ferramentas do IA**", selecione o modelo "**Do código Python Existente**", dê ao projeto um nome e um local e selecione **OK**.

    ![Novo Projeto com base em um Código Existente, etapa 1](media\create-project-existing\new-ai-project.png)

1. No assistente exibido, defina o caminho como seu código existente, defina um filtro para tipos de arquivo e especifique os caminhos de pesquisa que seu projeto requer. Em seguida, selecione **OK**. Se você não souber o que são caminhos de pesquisa, deixe esse campo em branco.


![Novo Projeto com base em um Código Existente, etapa 2](media\create-project-existing\azurebatch-newproject.png)

> Se seu código existente fizer parte de um projeto do Azure Machine Learning, marque "**É a pasta do Azure Machine Learning**" para garantir a conversão bem-sucedida de importantes detalhes de configuração do Azure Machine Learning como qual conta de Experimentação, qual Espaço de trabalho, quais contextos computacionais a serem usados e mais.

1. Para definir um arquivo de inicialização, localize o arquivo no Gerenciador de Soluções, clique com o botão direito do mouse e selecione **Definir como Arquivo de Inicialização**.

8. Se desejar, execute o programa pressionando CTRL + F5 ou selecionando **Depurar > Iniciar Sem Depuração**. 

> [!div class="nextstepaction"]
> [Tutorial: trabalhando com o Python no Visual Studio](https://docs.microsoft.com/visualstudio/python/vs-tutorial-01-00)

## <a name="see-also"></a>Consulte também

- [Criando um ambiente para um interpretador Python existente](https://docs.microsoft.com/visualstudio/python/python-environments#creating-an-environment-for-an-existing-interpreter)