---
title: "Catálogo e o serviço de imagem | Documentos do Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 34990c37-ae98-4140-9b1e-a91c192220d9
caps.latest.revision: 37
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
ms.openlocfilehash: dddc60fe8fbc2bda78d9c72777af7f21c7b9378d
ms.lasthandoff: 02/22/2017

---
# <a name="image-service-and-catalog"></a>Catálogo e o serviço de imagem
Este guia contém diretrizes e práticas recomendadas para adotar o serviço de imagem do Visual Studio e o catálogo de imagem introduzido no Visual Studio 2015.  
  
 O serviço de imagem introduzido no Visual Studio 2015 permite aos desenvolvedores a obter as melhor imagens para o dispositivo e o tema escolhido do usuário para exibir a imagem, incluindo temas correto para o contexto no qual eles são exibidos. Adotar o serviço de imagem ajudará a eliminar pontos problemáticos importantes relacionados à manutenção de ativos, HDPI dimensionamento e temas.  
  
|||  
|-|-|  
|**Problemas de hoje**|**Soluções**|  
|Combinação de cor de plano de fundo|Combinação alfa interna|  
|Imagens de temas (alguns)|Metadados de tema|  
|Modo de alto contraste|Recursos de alto contraste alternativos|  
|Precisar de vários recursos para diferentes modos DPI|Recursos selecionáveis com fallback vetoriais|  
|Duplicar imagens|Um identificador por conceito de imagem|  
  
 Por que adotar o serviço de imagem?  
  
-   Obter sempre a imagem "perfeita pixel" mais recente do Visual Studio  
  
-   Você pode enviar e usar suas próprias imagens  
  
-   Não há necessidade de testar suas imagens out quando o Windows adiciona a nova escala de DPI  
  
-   Endereço antigos obstáculos de arquiteturas em suas implementações  
  
 As ferramentas de shell do Visual Studio antes e depois de usar o serviço de imagem:  
  
 ![Serviço de imagem antes e depois](../extensibility/media/image-service-before-and-after.png "serviço de imagem antes e depois")  
  
## <a name="how-it-works"></a>Como ele funciona  
 O serviço de imagem pode fornecer uma imagem de bitmap adequada para qualquer estrutura de interface do usuário com suporte:  
  
-   WPF: BitmapSource  
  
-   WinForms: System.Drawing.Bitmap  
  
-   Win32: HBITMAP  
  
 Diagrama de fluxo de serviço de imagem  
  
 ![Diagrama de fluxo do serviço de imagem](../extensibility/media/image-service-flow-diagram.png "diagrama de fluxo do serviço de imagem")  
  
 **Identificadores de imagem**  
  
 Um moniker imagem (ou o moniker de forma abreviada) é um par de ID GUID que identifica exclusivamente um ativo de imagem ou um ativo de lista de imagens na biblioteca de imagens.  
  
 **Monikers conhecidos**  
  
 O conjunto de identificadores de imagens contidas no catálogo de imagens do Visual Studio e publicamente consumível por qualquer componente do Visual Studio ou a extensão.  
  
 **Arquivos de manifesto de imagem**  
  
 Arquivos de imagem de manifesto (.imagemanifest) são arquivos XML que definem um conjunto de ativos de imagem, os identificadores que representam os ativos e a imagem real ou imagens que representam cada ativo. Manifestos de imagem podem definir imagens autônomo ou listas de imagens para suporte legado de interface do usuário. Além disso, há atributos que podem ser definidos no ativo ou nas imagens individuais por trás de cada ativo para alterar quando e como esses ativos são exibidos.  
  
 **Esquema de manifesto de imagem**  
  
 Um manifesto de imagem completa tem esta aparência:  
  
```xml  
<ImageManifest>  
      <!-- zero or one Symbols elements -->  
      <Symbols>  
        <!-- zero or more Import, Guid, ID, or String elements -->  
      </Symbols>  
      <!-- zero or one Images elements -->  
      <Images>  
        <!-- zero or more Image elements -->  
      </Images>  
      <!-- zero or one ImageLists elements -->  
      <ImageLists>  
        <!-- zero or more ImageList elements -->  
      </ImageLists>  
</ImageManifest>  
```  
  
 **Símbolos**  
  
 Como ajudam a legibilidade e a manutenção, o manifesto de imagem pode usar símbolos para valores de atributo. Símbolos são definidos assim:  
  
```xml  
<Symbols>  
      <Import Manifest="manifest" />  
      <Guid Name="ShellCommandGuid" Value="8ee4f65d-bab4-4cde-b8e7-ac412abbda8a" />  
      <ID Name="cmdidSaveAll" Value="1000" />  
      <String Name="AssemblyName" Value="Microsoft.VisualStudio.Shell.UI.Internal" />  
</Symbols>  
```  
  
|||  
|-|-|  
|**Subelemento**|**Definição**|  
|Importar|Importa os símbolos do arquivo de manifesto determinado para uso no manifesto do atual|  
|GUID|O símbolo representa um GUID e deve corresponder a formatação de GUID|  
|ID|O símbolo representa uma ID e deve ser um inteiro não negativo|  
|Cadeia de caracteres|O símbolo representa um valor de cadeia de caracteres arbitrária|  
  
 Os símbolos são referenciados usando a sintaxe $(symbol-name) e diferencia maiusculas de minúsculas:  
  
```xml  
<Image Guid="$(ShellCommandGuid)" ID="$(cmdidSaveAll)" >  
      <Source Uri="/$(AssemblyName);Component/Resources/image.xaml" />  
</Image>  
```  
  
 Alguns símbolos são predefinidos para todos os manifestos. Eles podem ser usados no atributo de Uri de \<fonte > ou \<importação > elemento para caminhos de referência na máquina local.  
  
|||  
|-|-|  
|**Símbolo**|**Descrição**|  
|CommonProgramFiles|O valor da variável de ambiente % CommonProgramFiles %|  
|LocalAppData|O valor da variável de ambiente % LocalAppData %|  
|ManifestFolder|A pasta que contém o arquivo de manifesto|  
|Meus documentos|O caminho completo da pasta Meus documentos do usuário atual|  
|ProgramFiles|O valor da variável de ambiente % ProgramFiles %|  
|Sistema|A pasta Windows\System32|  
|WinDir|O valor da variável de ambiente % WinDir %|  
  
 **Imagem**  
  
 O \<imagem > elemento define uma imagem que pode ser referenciada por um moniker. O GUID e ID juntos formam o moniker de imagem. O identificador de origem da imagem deve ser exclusivo entre a biblioteca de imagem inteira. Se mais de uma imagem tem um moniker determinado, o primeiro encontrado ao criar a biblioteca é aquele que é mantido.  
  
 Ele deve conter pelo menos uma fonte. Fontes de tamanho neutro dará os melhores resultados em uma ampla variedade de tamanhos, mas eles não são necessários. Se o serviço é solicitado para uma imagem de tamanho não definido na \<imagem > elemento e não há neutros em relação ao tamanho da fonte, o serviço será escolher a melhor fonte de tamanho específico e dimensioná-lo para o tamanho solicitado.  
  
```xml  
<Image Guid="guid" ID="int" AllowColorInversion="true/false">  
      <Source ... />  
      <!-- optional additional Source elements -->  
</Image>  
```  
  
|||  
|-|-|  
|**Atributo**|**Definição**|  
|GUID|[Obrigatório] A parte GUID do moniker imagem|  
|ID|[Obrigatório] A parte de identificação do moniker imagem|  
|AllowColorInversion|[Opcional, padrão Verdadeiro] Indica se a imagem pode ter suas cores invertidas programaticamente quando usada em um plano de fundo escuro.|  
  
 **Source**  
  
 O \<fonte > elemento define um ativo de origem única imagem (PNG e XAML).  
  
```xml  
<Source Uri="uri" Background="background">  
      <!-- optional NativeResource element -->  
 </Source>  
```  
  
|||  
|-|-|  
|**Atributo**|**Definição**|  
|URI|[Obrigatório] Um URI que define onde a imagem pode ser carregada do. Ele pode ser um dos seguintes:<br /><br /> -A [Pack URI](http://msdn.microsoft.com/en-US/library/aa970069\(v=vs.100\).aspx) usando o aplicativo: / / / autoridade<br />-Referência de recurso um componente absoluto<br />-Um caminho para um arquivo que contém um recurso nativo|  
|Informações preliminares|[Opcional] Indica o tipo de plano de fundo que a fonte destina-se a ser usado.<br /><br /> Ele pode ser um dos seguintes:<br /><br /> *Luz:* a fonte pode ser usada no plano de fundo claro.<br /><br /> *Escuro:*a fonte pode ser usada em um plano de fundo escuro.<br /><br /> *Alto contraste será:* a fonte pode ser usada em qualquer plano de fundo no modo de alto contraste.<br /><br /> *HighContrastLight:* a fonte pode ser usada no plano de fundo claro no modo de alto contraste.<br /><br /> *HighContrastDark:* a fonte pode ser usada em um plano de fundo escuro no modo de alto contraste.<br /><br /> Se o atributo de plano de fundo for omitido, a fonte pode ser usada em qualquer plano de fundo.<br /><br /> Se o plano de fundo é *luz*, *escuro*, *HighContrastLight*, ou *HighContrastDark*, as cores da fonte nunca são invertidas. Se o plano de fundo é omitido ou definido como *alto contraste será*, a inversão de cores da fonte é controlado pela imagem de **AllowColorInversion** atributo.|  
|||  
  
 Um \<fonte > elemento pode ter exatamente um dos seguintes subelementos opcionais:  
  
||||  
|-|-|-|  
|**Elemento**|**Atributos (todas obrigatórias)**|**Definição**|  
|\<Tamanho >|Valor|A fonte será usada para imagens de determinado tamanho (em unidades de dispositivo). A imagem será quadrada.|  
|\<SizeRange >|MinSize, MaxSize|Inclusive, a fonte será usada para imagens de MinSize para MaxSize (em unidades de dispositivo). A imagem será quadrada.|  
|\<Dimensões >|Largura, altura|A fonte será usada para imagens de determinada largura e altura (em unidades de dispositivo).|  
|\<DimensionRange >|MinWidth, MinHeight,<br /><br /> MaxWidth, MaxHeight|Inclusive, a fonte será usada para imagens da largura/altura mínima para a largura/altura máxima (em unidades de dispositivo).|  
  
 A \<fonte > elemento também pode ter um opcional \<NativeResource > subelemento, que define um \<fonte > que é carregado de um assembly nativo em vez de um assembly gerenciado.  
  
```xml  
<NativeResource Type="type" ID="int" />  
```  
  
|||  
|-|-|  
|**Atributo**|**Definição**|  
|Tipo|[Obrigatório] O tipo do recurso nativo, XAML ou PNG|  
|ID|[Obrigatório] A parte de identificação de inteiro do recurso nativo|  
  
 **ImageList**  
  
 O \<ImageList > elemento define uma coleção de imagens que podem ser retornadas em uma única faixa. A faixa é criada sob demanda, conforme necessário.  
  
```xml  
<ImageList>  
      <ContainedImage Guid="guid" ID="int" External="true/false" />  
      <!-- optional additional ContainedImage elements -->  
 </ImageList>  
```  
  
|||  
|-|-|  
|**Atributo**|**Definição**|  
|GUID|[Obrigatório] A parte GUID do moniker imagem|  
|ID|[Obrigatório] A parte de identificação do moniker imagem|  
|Externo|[Opcional, padrão é false] Indica se o identificador de origem de imagem faz referência a uma imagem no manifesto do atual.|  
  
 O moniker da imagem independente não precisa fazer referência a uma imagem definida no manifesto do atual. Se a imagem independente não pode ser encontrada na biblioteca de imagens, uma imagem de alocador de espaço em branco será usada em seu lugar.  
  
## <a name="using-the-image-service"></a>Usando o serviço de imagem  
  
### <a name="first-steps-managed"></a>Primeiras etapas (gerenciadas)  
 Para usar o serviço de imagem, você precisa adicionar referências a alguns ou todos os assemblies a seguir ao seu projeto:  
  
-   **Microsoft.VisualStudio.ImageCatalog.dll**  
  
    -   Necessário se você usar o catálogo de imagem interna KnownMonikers  
  
-   **Microsoft.VisualStudio.Imaging.dll**  
  
    -   Necessário se você usar **CrispImage** e **ImageThemingUtilities** na sua UI do WPF  
  
-   **Microsoft.VisualStudio.Imaging.Interop.14.0.DesignTime.dll**  
  
    -   Necessário se você usar o **ImageMoniker** e **ImageAttributes** tipos  
  
    -   **EmbedInteropTypes** deve ser definido como true  
  
-   **Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime**  
  
    -   Necessário se você usar o **IVsImageService2** tipo  
  
    -   **EmbedInteropTypes** deve ser definido como true  
  
-   **Microsoft.VisualStudio.Utilities.dll**  
  
    -   Necessário se você usar o **BrushToColorConverter** para o ImageThemingUtilities.** ImageBackgroundColor** em sua interface do usuário do WPF  
  
-   **Microsoft.VisualStudio.Shell. \<VSVersion >.0**  
  
    -   Necessário se você usar o **IVsUIObject** tipo  
  
-   **Microsoft.VisualStudio.Shell.Interop.10.0.dll**  
  
    -   Necessário se você usar os auxiliares WinForms relacionados à interface do usuário  
  
    -   **EmbedInteropTypes** deve ser definido como true  
  
### <a name="first-steps-native"></a>Primeiras etapas (nativo)  
 Para usar o serviço de imagem, você precisa incluir alguns ou todos os cabeçalhos a seguir ao seu projeto:  
  
-   **KnownImageIds.h**  
  
    -   Necessário se você usar o catálogo de imagem interna **KnownMonikers**, mas não é possível usar o **ImageMoniker** tipo, como ao retornar valores de **IVsHierarchy GetGuidProperty** ou **GetProperty** chamadas.  
  
-   **KnownMonikers.h**  
  
    -   Necessário se você usar o catálogo de imagem interna **KnownMonikers**.  
  
-   **ImageParameters140.h**  
  
    -   Necessário se você usar o **ImageMoniker** e **ImageAttributes** tipos.  
  
-   **VSShell140.h**  
  
    -   Necessário se você usar o **IVsImageService2** tipo.  
  
-   **ImageThemingUtilities.h**  
  
    -   Necessário se não for possível permitir que o serviço de imagem manipular temas para você.  
  
    -   Não use esse cabeçalho se o serviço de imagem pode manipular temas sua imagem.  
  
-   **VSUIDPIHelper.h**  
  
    -   Necessário se você usar os auxiliares DPI para obter o DPI atual.  
  
## <a name="how-do-i-write-new-wpf-ui"></a>Como escrever novo WPF UI?  
  
1.  Inicie ao adicionar as referências de assembly necessárias acima primeiras etapas seção ao seu projeto. Você não precisa adicionar todos eles, portanto, adicione apenas as referências que você precisa. (Observação: se você estiver usando ou ter acesso a **cores** em vez de **pincéis**, em seguida, você pode ignorar a referência ao **utilitários**, desde que você não precisar do conversor.)  
  
2.  Selecione a imagem desejada e obter o identificador de origem. Use um **KnownMoniker**, ou usar seu próprio se você tiver suas próprias imagens personalizadas e identificadores.  
  
3.  Adicionar **CrispImages** para o XAML. (Consulte o exemplo abaixo).  
  
4.  Definir o **ImageThemingUtilities.ImageBackgroundColor** propriedade em sua hierarquia de interface do usuário. (Isso deve ser definido no local onde a cor de plano de fundo é conhecida, não necessariamente no **CrispImage**.) (Consulte o exemplo abaixo).  
  
```xaml  
<Window  
  x:Class="WpfApplication.MainWindow"  
  xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
  xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
  xmlns:imaging="clr-namespace:Microsoft.VisualStudio.Imaging;assembly=Microsoft.VisualStudio.Imaging"  
  xmlns:theming="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Imaging"  
  xmlns:utilities="clr-namespace:Microsoft.Internal.VisualStudio.Imaging;assembly=Microsoft.VisualStudio.Imaging"  
  xmlns:catalog="clr-namespace:Microsoft.VisualStudio.Imaging;assembly=Microsoft.VisualStudio.ImageCatalog"  
  Title="MainWindow" Height="350" Width="525" UseLayoutRounding="True">  
  <Window.Resources>  
    <utilities:BrushToColorConverter x:Key="BrushToColorConverter"/>  
  </Window.Resources>  
  <StackPanel Background="White" VerticalAlignment="Center"   
    theming:ImageThemingUtilities.ImageBackgroundColor="{Binding Background, RelativeSource={RelativeSource Self}, Converter={StaticResource BrushToColorConverter}}">  
    <imaging:CrispImage Width="16" Height="16" Moniker="{x:Static catalog:KnownMonikers.MoveUp}" />  
  </StackPanel>  
</Window>  
```  
  
 **Como atualizar o existente WPF UI?**  
  
 Atualizar existente UI WPF é um processo relativamente simple que consiste em três etapas básicas:  
  
1.  Substituir tudo \<imagem > elementos na interface do usuário com \<CrispImage > elementos  
  
2.  Altere todos os atributos de fonte para atributos de Moniker  
  
    -   Se a imagem nunca é alterada e você estiver usando **KnownMonikers**, em seguida, vincular estaticamente dessa propriedade para o **KnownMoniker**. (Consulte o exemplo acima).  
  
    -   Se a imagem nunca é alterada e você estiver usando sua própria imagem personalizada, em seguida, estaticamente ligar para seu próprio identificador de origem.  
  
    -   Se a imagem pode ser alterado, associar o atributo do identificador de origem a uma propriedade de código que notifica sobre alterações de propriedade.  
  
3.  Em algum lugar na hierarquia de interface do usuário, defina **ImageThemingUtilities.ImageBackgroundColor** tornar a inversão de cores se funciona corretamente.  
  
    -   Isso pode exigir o uso do **BrushToColorConverter** classe. (Consulte o exemplo acima).  
  
## <a name="how-do-i-update-win32-ui"></a>Como atualizar o Win32 da interface do usuário?  
 Adicione o seguinte ao seu código onde for apropriado para substituir o carregamento bruto de imagens. Alternar valores para retornar HBITMAPs versus HICONs versus HIMAGELIST conforme necessário.  
  
 **O serviço de imagem**  
  
```cpp  
CComPtr<IVsImageService2> spImgSvc;  
CGlobalServiceProvider::HrQueryService(SID_SVsImageService, &spImgSvc);  
```  
  
 **Solicitando a imagem**  
  
```cpp  
ImageAttributes attr = { 0 };  
attr.StructSize      = sizeof(attributes);  
attr.Format          = DF_Win32;  
// IT_Bitmap for HBITMAP, IT_Icon for HICON, IT_ImageList for HIMAGELIST  
attr.ImageType       = IT_Bitmap;  
attr.LogicalWidth    = 16;  
attr.LogicalHeight   = 16;  
attr.Dpi             = VsUI::DpiHelper::GetDeviceDpiX();  
attr.Background      = 0xFFFFFFFF;  
// Desired RGBA color, if you don't use this, don't set IAF_Background below  
attr.Flags           = IAF_RequiredFlags | IAF_Background;  
  
CComPtr<IVsUIObject> spImg;  
// Replace this KnownMoniker with your desired ImageMoniker  
spImgSvc->GetImage(KnownMonikers::Blank, attributes, &spImg);  
  
```  
  
## <a name="how-do-i-update-winforms-ui"></a>Como atualizar o WinForms UI?  
 Adicione o seguinte ao seu código onde for apropriado para substituir o carregamento bruto de imagens. Alternar valores para retornar os Bitmaps e ícones conforme necessário.  
  
 **Útil com instrução**  
  
```c#  
using GelUtilities = Microsoft.Internal.VisualStudio.PlatformUI.Utilities;  
```  
  
 **O serviço de imagem**  
  
```c#  
// This or your preferred way of querying for Visual Studio services  
IVsImageService2 imageService = (IVsImageService2)Package.GetGlobalService(typeof(SVsImageService));  
  
```  
  
 **A imagem da solicitação**  
  
```c#  
ImageAttributes attributes = new ImageAttributes  
{  
    StructSize    = Marshal.SizeOf(typeof(ImageAttributes)),  
    // IT_Bitmap for Bitmap, IT_Icon for Icon  
    ImageType     = (uint)_UIImageType.IT_Bitmap,  
    Format        = (uint)_UIDataFormat.DF_WinForms,  
    LogicalWidth  = 16,  
    LogicalHeight = 16,  
    // Desired RGBA color, if you don't use this, don't set IAF_Background below  
    Background    = 0xFFFFFFFF,  
    Flags = (uint)_ImageAttributesFlags.IAF_RequiredFlags | _ImageAttributesFlags.IAF_Background,  
};  
  
// Replace this KnownMoniker with your desired ImageMoniker  
IVsUIObject uIObj = imageService.GetImage(KnownMonikers.Blank, attributes);  
  
Bitmap bitmap = (Bitmap)GelUtilities.GetObjectData(uiObj); // Use this if you need a bitmap  
// Icon icon = (Icon)GelUtilities.GetObjectData(uiObj); // Use this if you need an icon  
  
```  
  
## <a name="how-do-i-use-image-monikers-in-a-new-tool-window"></a>Como usar identificadores de imagem em uma nova janela de ferramenta?  
 O modelo de projeto do VSIX pacote foi atualizado para o Visual Studio 2015. Para criar uma nova janela de ferramenta, clique com botão direito no projeto do VSIX e selecione "Adicionar Novo Item..." (Ctrl + Shift + A). Sob o nó de extensibilidade para o idioma do projeto, selecione "Janela de ferramenta personalizada", nomeie a janela da ferramenta e pressione o botão "Adicionar".  
  
 Esses são os principais locais usar identificadores de origem em uma janela de ferramenta. Siga as instruções para cada:  
  
1.  Guia da janela de ferramenta quando as guias pequeno suficiente (também usada no seletor de janela Ctrl + Tab).  
  
     Adicione esta linha para o construtor da classe que deriva de **ToolWindowPane** tipo:  
  
    ```c#  
    // Replace this KnownMoniker with your desired ImageMoniker  
    this.BitmapImageMoniker = KnownMonikers.Blank;  
    ```  
  
2.  O comando para abrir a janela da ferramenta.  
  
     No arquivo. VSCT para o pacote, edite o botão de comando da janela de ferramenta:  
  
    ```xml  
    <Button guid="guidPackageCmdSet" id="CommandId" priority="0x0100" type="Button">  
      <Parent guid="guidSHLMainMenu" id="IDG_VS_WNDO_OTRWNDWS1"/>  
      <!-- Replace this KnownMoniker with your desired ImageMoniker -->  
      <Icon guid="ImageCatalogGuid" id="Blank" />  
      <!-- Add this -->  
      <CommandFlag>IconIsMoniker</CommandFlag>  
      <Strings>  
        <ButtonText>MyToolWindow</ButtonText>  
      </Strings>  
    </Button>  
    ```  
  
 **Como usar identificadores de imagem em uma janela de ferramenta existente?**  
  
 Atualizar uma janela de ferramenta existente para usar identificadores de imagem é semelhante para as etapas para criar uma nova janela de ferramenta.  
  
 Esses são os principais locais usar identificadores de origem em uma janela de ferramenta. Siga as instruções para cada:  
  
1.  Guia da janela de ferramenta quando as guias pequeno suficiente (também usada no seletor de janela Ctrl + Tab).  
  
    1.  Remover essas linhas (se houver) no construtor da classe que deriva de **ToolWindowPane** tipo:  
  
        ```c#  
        this.BitmapResourceID = <Value>;  
        this.BitmapIndex = <Value>;  
        ```  
  
    2.  Consulte a etapa &#1; o "Como faço para usar identificadores de imagem em uma nova janela de ferramenta?" seção acima.  
  
2.  O comando para abrir a janela da ferramenta.  
  
    -   Consulte a etapa &#2; o "Como faço para usar identificadores de imagem em uma nova janela de ferramenta?" seção acima.  
  
## <a name="how-do-i-use-image-monikers-in-a-vsct-file"></a>Como usar identificadores de imagem em um arquivo. VSCT?  
 Atualize o arquivo. VSCT conforme indicado pelas linhas comentadas abaixo:  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<CommandTable xmlns="http://schemas.microsoft.com/VisualStudio/2005-10-18/CommandTable" xmlns:xs="http://www.w3.org/2001/XMLSchema">  
  <!--  Include the definitions for images included in the VS image catalog -->  
  <Include href="KnownImageIds.vsct"/>  
  <Commands package="guidMyPackage">  
    <Buttons>  
      <Button guid="guidMyCommandSet" id="cmdidMyCommand" priority="0x0000" type="Button">  
        <!-- Add an Icon element, changing the attributes to match the image moniker you want to use.  
             In this case, we’re using the Guid for the VS image catalog.  
             Change the id attribute to be the ID of the desired image moniker. -->  
        <Icon guid="ImageCatalogGuid" id="OpenFolder" />  
        <CommandFlag>DynamicVisibility</CommandFlag>  
        <CommandFlag>DefaultInvisible</CommandFlag>  
        <CommandFlag>DefaultDisabled</CommandFlag>  
        <CommandFlag>CommandWellOnly</CommandFlag>  
        <CommandFlag>IconAndText</CommandFlag>  
        <!-- Add the IconIsMoniker CommandFlag -->  
        <CommandFlag>IconIsMoniker</CommandFlag>  
        <Strings>  
          <ButtonText>Quick Fixes...</ButtonText>  
          <CommandName>Show Quick Fixes</CommandName>  
          <CanonicalName>ShowQuickFixes</CanonicalName>  
          <LocCanonicalName>ShowQuickFixes</LocCanonicalName>  
        </Strings>  
      </Button>  
    </Buttons>  
  </Commands>  
  <!-- It is recommended that you remove <Bitmap> elements that are no longer used in the vsct file -->  
  <Symbols>  
    <GuidSymbol name="guidMyPackage"    value="{1491e936-6ffe-474e-8371-30e5920d8fdd}" />  
    <GuidSymbol name="guidMyCommandSet" value="{10347de4-69a9-47f4-a950-d3301f6d2bc7}">  
      <IDSymbol name="cmdidMyCommand" value="0x9437" />  
    </GuidSymbol>  
  </Symbols>  
</CommandTable>  
```  
  
 **E se meu arquivo VSCT também precisa ser lidos por versões mais antigas do Visual Studio?**  
  
 Versões anteriores do Visual Studio não reconhecer o **IconIsMoniker** sinalizador de comando. Você pode usar imagens do serviço de imagem em versões do Visual Studio que dão suporte a ela, mas continuam a usar imagens de estilo antigo em versões anteriores do Visual Studio. Para fazer isso, deixe o arquivo. VSCT inalterado (e, portanto, compatível com versões anteriores do Visual Studio) e criar um arquivo CSV (valores separados por vírgulas) que mapeia de pares de ID GUID definidos em um arquivo. VSCT \<Bitmaps > elemento pares de GUID/ID do moniker de imagem.  
  
 O formato de arquivo CSV de mapeamento é:  
  
```  
Icon guid, Icon id, Moniker guid, Moniker id  
b714fcf7-855e-4e4c-802a-1fd87144ccad,1,fda30684-682d-421c-8be4-650a2967058e,100  
b714fcf7-855e-4e4c-802a-1fd87144ccad,2,fda30684-682d-421c-8be4-650a2967058e,200  
```  
  
 O arquivo CSV é implantado com o pacote e o local é especificado pelo **IconMappingFilename** propriedade o **ProvideMenuResource** atributo de pacote:  
  
```c#  
[ProvideMenuResource("MyPackage.ctmenu", 1, IconMappingFilename="IconMappings.csv")]  
```  
  
 O **IconMappingFilename** um caminho relativo é implicitamente enraizado em $PackageFolder$ (como no exemplo acima) ou um caminho absoluto explicitamente enraizada em um diretório definido por uma variável de ambiente, como @"% UserProfile%\dir1\dir2\MyMappingFile.csv".  
  
## <a name="how-do-i-port-a-project-system"></a>Como posso portar um sistema de projeto?  
 **Como fornecer ImageMonikers para um projeto**  
  
1.  Implementar **VSHPROPID_SupportsIconMonikers** do projeto **IVsHierarchy**e retornar true.  
  
2.  Implementar o **VSHPROPID_IconMonikerImageList** (se o projeto original usado **VSHPROPID_IconImgList**) ou **VSHPROPID_IconMonikerGuid**, **VSHPROPID_IconMonikerId**, **VSHPROPID_OpenFolderIconMonikerGuid**, **VSHPROPID_OpenFolderIconMonikerId** (se o projeto original usado **VSHPROPID_IconHandle** e **VSHPROPID_OpenFolderIconHandle**).  
  
3.  Altere a implementação dos VSHPROPIDs originais para ícones para criar versões "herdadas" dos ícones se pontos de extensão solicitação-los. **IVsImageService2** fornece a funcionalidade necessária obter esses ícones  
  
 **Requisitos adicionais para VB / tipos de projeto c#**  
  
 Implementar apenas **VSHPROPID_SupportsIconMonikers** se você detectar que o projeto é o **flavor externo**. Caso contrário, o tipo externo real pode não suportar monikers de imagem na realidade, e seu tipo base pode efetivamente "Ocultar" imagens personalizadas.  
  
 **Como usar identificadores de imagem no CPS?**  
  
 Definindo imagens personalizadas no CPS (sistema de projeto comum) pode ser feito manualmente ou por meio de um modelo de item que vem com o SDK de extensibilidade do sistema de projeto.  
  
 **Usando o SDK de extensibilidade do sistema de projeto**  
  
 Siga as instruções em [fornecer ícones personalizados para o tipo de Item da tipo projeto](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/scenario/provide_custom_icons_for_the_project_or_item_type.md) para personalizar as imagens do CPS. Mais informações sobre o CPS podem ser encontradas em [documentação de extensibilidade do sistema do Visual Studio Project](https://github.com/Microsoft/VSProjectSystem)  
  
 **Usar ImageMonikers manualmente**  
  
1.  Implemente e exporte a **IProjectTreeModifier** interface no seu sistema de projeto.  
  
2.  Determinar qual **KnownMoniker** ou identificador de origem de imagem personalizada que deseja usar.  
  
3.  No **ApplyModifications** método, faça o seguinte em algum lugar no método antes de retornar a nova árvore, como o exemplo abaixo:  
  
    ```c#  
    // Replace this KnownMoniker with your desired ImageMoniker  
    tree = tree.SetIcon(KnownMonikers.Blank.ToProjectSystemType());  
    ```  
  
4.  Se você estiver criando uma nova árvore, você pode definir as imagens personalizadas, passando os monikers desejados no método NewTree, semelhante do exemplo abaixo:  
  
    ```c#  
    // Replace this KnownMoniker with your desired ImageMoniker  
    ProjectImageMoniker icon         = KnownMonikers.FolderClosed.ToProjectSystemType();  
    ProjectImageMoniker expandedIcon = KnownMonikers.FolderOpened.ToProjectSystemType();  
  
    return this.ProjectTreeFactory.Value.NewTree(/*caption*/<value>,  
                                                 /*filePath*/<value>,  
                                                 /*browseObjectProperties*/<value>,  
                                                 icon,  
                                                 expandedIcon);  
    ```  
  
## <a name="how-do-i-convert-from-a-real-image-strip-to-a-moniker-based-image-strip"></a>Como converter de uma faixa de imagem real para uma faixa de imagens baseadas em moniker?  
 **Preciso oferecer suporte à HIMAGELISTs**  
  
 Se houver uma faixa de imagem já existente para o código que você deseja atualizar para usar o serviço de imagem, mas é restritos por APIs que exigem a passagem de listas de imagens, você ainda pode obter os benefícios do serviço de imagem. Para criar uma faixa de imagens baseadas em moniker, siga as etapas abaixo para criar um manifesto de identificadores de origem existentes.  
  
1.  Execute o **ManifestFromResources** ferramenta, passando a faixa de imagens. Isso irá gerar um manifesto para a fita.  
  
    -   Recomendado: fornece um nome não padrão para o manifesto de acordo com seu uso.  
  
2.  Se você estiver usando apenas **KnownMonikers**, em seguida, faça o seguinte:  
  
    -   Substitua o \<imagens > seção de manifesto com \<imagens / >.  
  
    -   Remover todos o IDs de subimage (tudo com \<imagestrip nome > _ # #).  
  
    -   Recomendado: renomear o símbolo AssetsGuid e o símbolo de faixa de imagem de acordo com seu uso.  
  
    -   Substitua cada **ContainedImage**do GUID com $(ImageCatalogGuid), substitua cada **ContainedImage**do ID com $(\<moniker >) e adicione o atributo de externo = "true" para cada **ContainedImage**  
  
        -   \<Moniker > deve ser substituído com o **KnownMoniker** que corresponda à imagem, mas com a "KnownMonikers". removido do nome.  
  
    -   Adicionar <Import manifest="$(ManifestFolder)\\<Relativeinstall=""dir=""path=""></Relative><spanclass="notranslate">\>\Microsoft.VisualStudio.ImageCatalog.imagemanifest "/\> na parte superior do \<símbolos > seção.</Import>  
  
        -   O caminho relativo é determinado pelo local de implantação definido na configuração de criação para o manifesto.  
  
3.  Execute o **ManifestToCode** ferramenta para gerar wrappers para que o código existente tem um identificador de origem pode usar para consultar o serviço de imagem para a faixa de imagens.  
  
    -   Recomendado: fornece nomes não padrão para os wrappers e namespaces de acordo com seu uso.  
  
4.  Todas as adiciona, instalação de criação/implantação e outras alterações de código para trabalhar com o serviço de imagem e os novos arquivos.  
  
 Manifesto de exemplo incluindo imagens internas e externas para ver o que deve se parecer com:  
  
```xml  
<?xml version="1.0"?>  
<ImageManifest  
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
  xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
  xmlns="http://schemas.microsoft.com/VisualStudio/ImageManifestSchema/2014">  
  
  <Symbols>  
    <!-- This needs to be the relative path from your manifest to the ImageCatalog's manifest  
         where $(ManifestFolder) is the deployed location of this manifest. -->  
    <Import Manifest="$(ManifestFolder)\<RelPath>\Microsoft.VisualStudio.ImageCatalog.imagemanifest" />  
  
    <String Name="Resources" Value="/My.Assembly.Name;Component/Resources/ImageStrip" />  
    <Guid Name="ImageGuid" Value="{fb41b7ef-6587-480c-aa27-5b559d42cfc9}" />  
    <Guid Name="ImageStripGuid" Value="{9c84a570-d9a7-4052-a340-188fb276f973}" />  
    <ID Name="MyImage_0" Value="100" />  
    <ID Name="MyImage_1" Value="101" />  
    <ID Name="InternalList" Value="1001" />  
    <ID Name="ExternalList" Value="1002" />  
  </Symbols>  
  
  <Images>  
    <Image Guid="$(ImageGuid)" ID="$(MyImage_0)">  
      <Source Uri="$(Resources)/MyImage_0.png">  
        <Size Value="16" />  
      </Source>  
    </Image>  
    <Image Guid="$(ImageGuid)" ID="$(MyImage_1)">  
      <Source Uri="$(Resources)/MyImage_1.png">  
        <Size Value="16" />  
      </Source>  
    </Image>  
  </Images>  
  
  <ImageLists>  
    <ImageList Guid="$(ImageStripGuid)" ID="$(InternalList)">  
      <ContainedImage Guid="$(ImageGuid)" ID="$(MyImage_0)" />  
      <ContainedImage Guid="$(ImageGuid)" ID="$(MyImage_1)" />  
    </ImageList>  
    <ImageList Guid="$(ImageStripGuid)" ID="$(ExternalList)">  
      <ContainedImage Guid="$(ImageCatalogGuid)" ID="$(StatusError)" External="true" />  
      <ContainedImage Guid="$(ImageCatalogGuid)" ID="$(StatusWarning)" External="true" />  
      <ContainedImage Guid="$(ImageCatalogGuid)" ID="$(StatusInformation)" External="true" />  
    </ImageList>  
  </ImageLists>  
  
</ImageManifest>  
```  
  
 **Não preciso oferecer suporte a HIMAGELISTs**  
  
1.  Determinar o conjunto de **KnownMonikers** que correspondem às imagens em sua faixa de imagens ou criar seus próprios identificadores para as imagens em sua faixa de imagens.  
  
2.  Atualize qualquer mapeamento usada para obter a imagem no índice necessário na faixa de imagens para usar os identificadores em vez disso.  
  
3.  Atualize seu código para usar o serviço de imagem para solicitar monikers via o mapeamento atualizado. (Isso pode significar a atualização para **CrispImages** para código gerenciado, ou solicitar HBITMAPs ou HICONs do serviço de imagem e transmiti-los ao redor para código nativo.)  
  
## <a name="testing-your-images"></a>Teste suas imagens  
 Você pode usar a ferramenta Visualizador de biblioteca de imagens para testar seus manifestos de imagem para verificar se que tudo foi criado corretamente. Você pode encontrar a ferramenta no [SDK do Visual Studio 2015](http://msdn.microsoft.com/library/bb166441.aspx). Documentação para essa ferramenta e outros pode ser encontrada [aqui](http://aka.ms/VSImageThemeTools).  
  
## <a name="additional-resources"></a>Recursos adicionais  
  
### <a name="samples"></a>Exemplos  
 Vários dos exemplos do Visual Studio no GitHub foram atualizados para mostrar como usar o serviço de imagem como parte de vários pontos de extensibilidade do Visual Studio.  
  
 Verificar [http://github.com/Microsoft/VSSDK-Extensibility-Samples](http://github.com/Microsoft/VSSDK-Extensibility-Samples) para os exemplos mais recentes.  
  
### <a name="tooling"></a>Ferramentas  
 Um conjunto de ferramentas de suporte para o serviço de imagem foi criado para ajudar a criar/atualizar a interface do usuário que funciona com o serviço de imagem. Para obter mais informações sobre cada ferramenta, consulte a documentação que acompanha as ferramentas. As ferramentas são incluídas como parte do [SDK do Visual Studio 2015.](http://msdn.microsoft.com/library/bb166441.aspx)  
  
 **ManifestFromResources**  
  
 O manifesto da ferramenta de recursos usa uma lista de recursos de imagem (PNG ou XAML) e gera um arquivo de manifesto de imagem para usar essas imagens com o serviço de imagem.  
  
 **ManifestToCode**  
  
 O manifesto para a ferramenta de código usa um arquivo de manifesto de imagem e gera um arquivo invólucro para fazer referência os valores de manifesto em código (C++, c# ou VB) ou arquivos. VSCT.  
  
 **ImageLibraryViewer**  
  
 A ferramenta de Visualizador de imagem biblioteca pode carregar imagem manifestos e permite que o usuário para manipulá-los da mesma forma que seria o Visual Studio para verificar se que o manifesto foi criado corretamente. O usuário pode alterar o plano de fundo, tamanhos, configuração de DPI, alto contraste e outras configurações. Ele também exibe informações de carregamento para localizar erros nos manifestos e exibe informações de origem para cada imagem no manifesto.  
  
## <a name="faq"></a>Perguntas Frequentes  
  
-   Há dependências que você deve incluir ao carregar \<Include="Microsoft.VisualStudio.* de referência. Interop.14.0.DesignTime"/ >?  
  
    -   Definir EmbedInteropTypes = "true" em todas as DLLs de interoperabilidade.  
  
-   Como implantar um manifesto de imagem com minha extensão?  
  
    -   Adicione o arquivo .imagemanifest ao seu projeto.  
  
    -   Defina "Incluir no VSIX" como True.  
  
-   Estou atualizando meu sistema de projeto do CPS. O que aconteceu com **ImageName** e **StockIconService**?  
  
    -   o que eles foram removidos quando CPS foi atualizado para usar identificadores. Você não precisa chamar o **StockIconService**, basta transmitir o desejado **KnownMoniker** ao método ou propriedade usando o **ToProjectSystemType()** método de extensão em utilitários do CPS. Você pode encontrar um mapeamento de **ImageName** para **KnownMonikers** abaixo:  
  
        |||  
        |-|-|  
        |**ImageName**|**KnownMoniker**|  
        |ImageName.OfflineWebApp|KnownImageIds.Web|  
        |ImageName.WebReferencesFolder|KnownImageIds.Web|  
        |ImageName.OpenReferenceFolder|KnownImageIds.FolderOpened|  
        |ImageName.ReferenceFolder|KnownImageIds.Reference|  
        |ImageName.Reference|KnownImageIds.Reference|  
        |ImageName.SdlWebReference|KnownImageIds.WebReferenceFolder|  
        |ImageName.DiscoWebReference|KnownImageIds.DynamicDiscoveryDocument|  
        |ImageName.Folder|KnownImageIds.FolderClosed|  
        |ImageName.OpenFolder|KnownImageIds.FolderOpened|  
        |ImageName.ExcludedFolder|KnownImageIds.HiddenFolderClosed|  
        |ImageName.OpenExcludedFolder|KnownImageIds.HiddenFolderOpened|  
        |ImageName.ExcludedFile|KnownImageIds.HiddenFile|  
        |ImageName.DependentFile|KnownImageIds.GenerateFile|  
        |ImageName.MissingFile|KnownImageIds.DocumentWarning|  
        |ImageName.WindowsForm|KnownImageIds.WindowsForm|  
        |ImageName.WindowsUserControl|KnownImageIds.UserControl|  
        |ImageName.WindowsComponent|KnownImageIds.ComponentFile|  
        |ImageName.XmlSchema|KnownImageIds.XMLSchema|  
        |ImageName.XmlFile|KnownImageIds.XMLFile|  
        |ImageName.WebForm|KnownImageIds.Web|  
        |ImageName.WebService|KnownImageIds.WebService|  
        |ImageName.WebUserControl|KnownImageIds.WebUserControl|  
        |ImageName.WebCustomUserControl|KnownImageIds.WebCustomControl|  
        |ImageName.AspPage|KnownImageIds.ASPFile|  
        |ImageName.GlobalApplicationClass|KnownImageIds.SettingsFile|  
        |ImageName.WebConfig|KnownImageIds.ConfigurationFile|  
        |ImageName.HtmlPage|KnownImageIds.HTMLFile|  
        |ImageName.StyleSheet|KnownImageIds.StyleSheet|  
        |ImageName.ScriptFile|KnownImageIds.JSScript|  
        |ImageName.TextFile|KnownImageIds.Document|  
        |ImageName.SettingsFile|KnownImageIds.Settings|  
        |ImageName.Resources|KnownImageIds.DocumentGroup|  
        |ImageName.Bitmap|KnownImageIds.Image|  
        |ImageName.Icon|KnownImageIds.IconFile|  
        |ImageName.Image|KnownImageIds.Image|  
        |ImageName.ImageMap|KnownImageIds.ImageMapFile|  
        |ImageName.XWorld|KnownImageIds.XWorldFile|  
        |ImageName.Audio|KnownImageIds.Sound|  
        |ImageName.Video|KnownImageIds.Media|  
        |ImageName.Cab|KnownImageIds.CABProject|  
        |ImageName.Jar|KnownImageIds.JARFile|  
        |ImageName.DataEnvironment|KnownImageIds.DataTable|  
        |ImageName.PreviewFile|KnownImageIds.Report|  
        |ImageName.DanglingReference|KnownImageIds.ReferenceWarning|  
        |ImageName.XsltFile|KnownImageIds.XSLTransform|  
        |ImageName.Cursor|KnownImageIds.CursorFile|  
        |ImageName.AppDesignerFolder|KnownImageIds.Property|  
        |ImageName.Data|KnownImageIds.Database|  
        |ImageName.Application|KnownImageIds.Application|  
        |ImageName.DataSet|KnownImageIds.DatabaseGroup|  
        |ImageName.Pfx|KnownImageIds.Certificate|  
        |ImageName.Snk|KnownImageIds.Rule|  
        |ImageName.VisualBasicProject|KnownImageIds.VBProjectNode|  
        |ImageName.CSharpProject|KnownImageIds.CSProjectNode|  
        |ImageName.Empty|KnownImageIds.Blank|  
        |ImageName.MissingFolder|KnownImageIds.FolderOffline|  
        |ImageName.SharedImportReference|KnownImageIds.SharedProject|  
        |ImageName.SharedProjectCs|KnownImageIds.CSSharedProject|  
        |ImageName.SharedProjectVc|KnownImageIds.CPPSharedProject|  
        |ImageName.SharedProjectJs|KnownImageIds.JSSharedProject|  
        |ImageName.CSharpCodeFile|KnownImageIds.CSFileNode|  
        |ImageName.VisualBasicCodeFile|KnownImageIds.VBFileNode|  
  
    -   Estou atualizando meu provedor de lista de conclusão. O que **KnownMonikers** corresponder o antigo **StandardGlyphGroup** e **StandardGlyph** valores?  
  
        ||||  
        |-|-|-|  
        |GlyphGroupClass|GlyphItemPublic|ClassPublic|  
        |GlyphGroupClass|GlyphItemInternal|ClassInternal|  
        |GlyphGroupClass|GlyphItemFriend|ClassInternal|  
        |GlyphGroupClass|GlyphItemProtected|ClassProtected|  
        |GlyphGroupClass|GlyphItemPrivate|ClassPrivate|  
        |GlyphGroupClass|GlyphItemShortcut|ClassShortcut|  
        |GlyphGroupConstant|GlyphItemPublic|ClassPublic|  
        |GlyphGroupConstant|GlyphItemInternal|ClassInternal|  
        |GlyphGroupConstant|GlyphItemFriend|ClassInternal|  
        |GlyphGroupConstant|GlyphItemProtected|ClassProtected|  
        |GlyphGroupConstant|GlyphItemPrivate|ClassPrivate|  
        |GlyphGroupConstant|GlyphItemShortcut|ClassShortcut|  
        |GlyphGroupDelegate|GlyphItemPublic|DelegatePublic|  
        |GlyphGroupDelegate|GlyphItemInternal|DelegateInternal|  
        |GlyphGroupDelegate|GlyphItemFriend|DelegateInternal|  
        |GlyphGroupDelegate|GlyphItemProtected|DelegateProtected|  
        |GlyphGroupDelegate|GlyphItemPrivate|DelegatePrivate|  
        |GlyphGroupDelegate|GlyphItemShortcut|DelegateShortcut|  
        |GlyphGroupEnum|GlyphItemPublic|EnumerationPublic|  
        |GlyphGroupEnum|GlyphItemInternal|EnumerationInternal|  
        |GlyphGroupEnum|GlyphItemFriend|EnumerationInternal|  
        |GlyphGroupEnum|GlyphItemProtected|EnumerationProtected|  
        |GlyphGroupEnum|GlyphItemPrivate|EnumerationPrivate|  
        |GlyphGroupEnum|GlyphItemShortcut|EnumerationShortcut|  
        |GlyphGroupEnumMember|GlyphItemPublic|EnumerationMemberPublic|  
        |GlyphGroupEnumMember|GlyphItemInternal|EnumerationMemberInternal|  
        |GlyphGroupEnumMember|GlyphItemFriend|EnumerationMemberInternal|  
        |GlyphGroupEnumMember|GlyphItemProtected|EnumerationMemberProtected|  
        |GlyphGroupEnumMember|GlyphItemPrivate|EnumerationMemberPrivate|  
        |GlyphGroupEnumMember|GlyphItemShortcut|EnumerationMemberShortcut|  
        |GlyphGroupEvent|GlyphItemPublic|EventPublic|  
        |GlyphGroupEvent|GlyphItemInternal|EventInternal|  
        |GlyphGroupEvent|GlyphItemFriend|EventInternal|  
        |GlyphGroupEvent|GlyphItemProtected|EventProtected|  
        |GlyphGroupEvent|GlyphItemPrivate|EventPrivate|  
        |GlyphGroupEvent|GlyphItemShortcut|EventShortcut|  
        |GlyphGroupException|GlyphItemPublic|ExceptionPublic|  
        |GlyphGroupException|GlyphItemInternal|ExceptionInternal|  
        |GlyphGroupException|GlyphItemFriend|ExceptionInternal|  
        |GlyphGroupException|GlyphItemProtected|ExceptionProtected|  
        |GlyphGroupException|GlyphItemPrivate|ExceptionPrivate|  
        |GlyphGroupException|GlyphItemShortcut|ExceptionShortcut|  
        |GlyphGroupField|GlyphItemPublic|FieldPublic|  
        |GlyphGroupField|GlyphItemInternal|FieldInternal|  
        |GlyphGroupField|GlyphItemFriend|FieldInternal|  
        |GlyphGroupField|GlyphItemProtected|FieldProtected|  
        |GlyphGroupField|GlyphItemPrivate|FieldPrivate|  
        |GlyphGroupField|GlyphItemShortcut|FieldShortcut|  
        |GlyphGroupInterface|GlyphItemPublic|InterfacePublic|  
        |GlyphGroupInterface|GlyphItemInternal|InterfaceInternal|  
        |GlyphGroupInterface|GlyphItemFriend|InterfaceInternal|  
        |GlyphGroupInterface|GlyphItemProtected|InterfaceProtected|  
        |GlyphGroupInterface|GlyphItemPrivate|InterfacePrivate|  
        |GlyphGroupInterface|GlyphItemShortcut|InterfaceShortcut|  
        |GlyphGroupMacro|GlyphItemPublic|MacroPublic|  
        |GlyphGroupMacro|GlyphItemInternal|MacroInternal|  
        |GlyphGroupMacro|GlyphItemFriend|MacroInternal|  
        |GlyphGroupMacro|GlyphItemProtected|MacroProtected|  
        |GlyphGroupMacro|GlyphItemPrivate|MacroPrivate|  
        |GlyphGroupMacro|GlyphItemShortcut|MacroShortcut|  
        |GlyphGroupMap|GlyphItemPublic|MapPublic|  
        |GlyphGroupMap|GlyphItemInternal|MapInternal|  
        |GlyphGroupMap|GlyphItemFriend|MapInternal|  
        |GlyphGroupMap|GlyphItemProtected|MapProtected|  
        |GlyphGroupMap|GlyphItemPrivate|MapPrivate|  
        |GlyphGroupMap|GlyphItemShortcut|MapShortcut|  
        |GlyphGroupMapItem|GlyphItemPublic|MapItemPublic|  
        |GlyphGroupMapItem|GlyphItemInternal|MapItemInternal|  
        |GlyphGroupMapItem|GlyphItemFriend|MapItemInternal|  
        |GlyphGroupMapItem|GlyphItemProtected|MapItemProtected|  
        |GlyphGroupMapItem|GlyphItemPrivate|MapItemPrivate|  
        |GlyphGroupMapItem|GlyphItemShortcut|MapItemShortcut|  
        |GlyphGroupMethod|GlyphItemPublic|MethodPublic|  
        |GlyphGroupMethod|GlyphItemInternal|MethodInternal|  
        |GlyphGroupMethod|GlyphItemFriend|MethodInternal|  
        |GlyphGroupMethod|GlyphItemProtected|MethodProtected|  
        |GlyphGroupMethod|GlyphItemPrivate|MethodPrivate|  
        |GlyphGroupMethod|GlyphItemShortcut|MethodShortcut|  
        |GlyphGroupOverload|GlyphItemPublic|MethodPublic|  
        |GlyphGroupOverload|GlyphItemInternal|MethodInternal|  
        |GlyphGroupOverload|GlyphItemFriend|MethodInternal|  
        |GlyphGroupOverload|GlyphItemProtected|MethodProtected|  
        |GlyphGroupOverload|GlyphItemPrivate|MethodPrivate|  
        |GlyphGroupOverload|GlyphItemShortcut|MethodShortcut|  
        |GlyphGroupModule|GlyphItemPublic|ModulePublic|  
        |GlyphGroupModule|GlyphItemInternal|ModuleInternal|  
        |GlyphGroupModule|GlyphItemFriend|ModuleInternal|  
        |GlyphGroupModule|GlyphItemProtected|ModuleProtected|  
        |GlyphGroupModule|GlyphItemPrivate|ModulePrivate|  
        |GlyphGroupModule|GlyphItemShortcut|ModuleShortcut|  
        |GlyphGroupNamespace|GlyphItemPublic|NamespacePublic|  
        |GlyphGroupNamespace|GlyphItemInternal|NamespaceInternal|  
        |GlyphGroupNamespace|GlyphItemFriend|NamespaceInternal|  
        |GlyphGroupNamespace|GlyphItemProtected|NamespaceProtected|  
        |GlyphGroupNamespace|GlyphItemPrivate|NamespacePrivate|  
        |GlyphGroupNamespace|GlyphItemShortcut|NamespaceShortcut|  
        |GlyphGroupOperator|GlyphItemPublic|OperatorPublic|  
        |GlyphGroupOperator|GlyphItemInternal|OperatorInternal|  
        |GlyphGroupOperator|GlyphItemFriend|OperatorInternal|  
        |GlyphGroupOperator|GlyphItemProtected|OperatorProtected|  
        |GlyphGroupOperator|GlyphItemPrivate|OperatorPrivate|  
        |GlyphGroupOperator|GlyphItemShortcut|OperatorShortcut|  
        |GlyphGroupProperty|GlyphItemPublic|PropertyPublic|  
        |GlyphGroupProperty|GlyphItemInternal|PropertyInternal|  
        |GlyphGroupProperty|GlyphItemFriend|PropertyInternal|  
        |GlyphGroupProperty|GlyphItemProtected|PropertyProtected|  
        |GlyphGroupProperty|GlyphItemPrivate|PropertyPrivate|  
        |GlyphGroupProperty|GlyphItemShortcut|PropertyShortcut|  
        |GlyphGroupStruct|GlyphItemPublic|StructurePublic|  
        |GlyphGroupStruct|GlyphItemInternal|StructureInternal|  
        |GlyphGroupStruct|GlyphItemFriend|StructureInternal|  
        |GlyphGroupStruct|GlyphItemProtected|StructureProtected|  
        |GlyphGroupStruct|GlyphItemPrivate|StructurePrivate|  
        |GlyphGroupStruct|GlyphItemShortcut|StructureShortcut|  
        |GlyphGroupTemplate|GlyphItemPublic|TemplatePublic|  
        |GlyphGroupTemplate|GlyphItemInternal|TemplateInternal|  
        |GlyphGroupTemplate|GlyphItemFriend|TemplateInternal|  
        |GlyphGroupTemplate|GlyphItemProtected|TemplateProtected|  
        |GlyphGroupTemplate|GlyphItemPrivate|TemplatePrivate|  
        |GlyphGroupTemplate|GlyphItemShortcut|TemplateShortcut|  
        |GlyphGroupTypedef|GlyphItemPublic|TypeDefinitionPublic|  
        |GlyphGroupTypedef|GlyphItemInternal|TypeDefinitionInternal|  
        |GlyphGroupTypedef|GlyphItemFriend|TypeDefinitionInternal|  
        |GlyphGroupTypedef|GlyphItemProtected|TypeDefinitionProtected|  
        |GlyphGroupTypedef|GlyphItemPrivate|TypeDefinitionPrivate|  
        |GlyphGroupTypedef|GlyphItemShortcut|TypeDefinitionShortcut|  
        |GlyphGroupType|GlyphItemPublic|TypePublic|  
        |GlyphGroupType|GlyphItemInternal|TypeInternal|  
        |GlyphGroupType|GlyphItemFriend|TypeInternal|  
        |GlyphGroupType|GlyphItemProtected|TypeProtected|  
        |GlyphGroupType|GlyphItemPrivate|TypePrivate|  
        |GlyphGroupType|GlyphItemShortcut|TypeShortcut|  
        |GlyphGroupUnion|GlyphItemPublic|UnionPublic|  
        |GlyphGroupUnion|GlyphItemInternal|UnionInternal|  
        |GlyphGroupUnion|GlyphItemFriend|UnionInternal|  
        |GlyphGroupUnion|GlyphItemProtected|UnionProtected|  
        |GlyphGroupUnion|GlyphItemPrivate|UnionPrivate|  
        |GlyphGroupUnion|GlyphItemShortcut|UnionShortcut|  
        |GlyphGroupVariable|GlyphItemPublic|FieldPublic|  
        |GlyphGroupVariable|GlyphItemInternal|FieldInternal|  
        |GlyphGroupVariable|GlyphItemFriend|FieldInternal|  
        |GlyphGroupVariable|GlyphItemProtected|FieldProtected|  
        |GlyphGroupVariable|GlyphItemPrivate|FieldPrivate|  
        |GlyphGroupVariable|GlyphItemShortcut|FieldShortcut|  
        |GlyphGroupValueType|GlyphItemPublic|ValueTypePublic|  
        |GlyphGroupValueType|GlyphItemInternal|ValueTypeInternal|  
        |GlyphGroupValueType|GlyphItemFriend|ValueTypeInternal|  
        |GlyphGroupValueType|GlyphItemProtected|ValueTypeProtected|  
        |GlyphGroupValueType|GlyphItemPrivate|ValueTypePrivate|  
        |GlyphGroupValueType|GlyphItemShortcut|ValueTypeShortcut|  
        |GlyphGroupIntrinsic|GlyphItemPublic|ObjectPublic|  
        |GlyphGroupIntrinsic|GlyphItemInternal|ObjectInternal|  
        |GlyphGroupIntrinsic|GlyphItemFriend|ObjectInternal|  
        |GlyphGroupIntrinsic|GlyphItemProtected|ObjectProtected|  
        |GlyphGroupIntrinsic|GlyphItemPrivate|ObjectPrivate|  
        |GlyphGroupIntrinsic|GlyphItemShortcut|ObjectShortcut|  
        |GlyphGroupJSharpMethod|GlyphItemPublic|MethodPublic|  
        |GlyphGroupJSharpMethod|GlyphItemInternal|MethodInternal|  
        |GlyphGroupJSharpMethod|GlyphItemFriend|MethodInternal|  
        |GlyphGroupJSharpMethod|GlyphItemProtected|MethodProtected|  
        |GlyphGroupJSharpMethod|GlyphItemPrivate|MethodPrivate|  
        |GlyphGroupJSharpMethod|GlyphItemShortcut|MethodShortcut|  
        |GlyphGroupJSharpField|GlyphItemPublic|FieldPublic|  
        |GlyphGroupJSharpField|GlyphItemInternal|FieldInternal|  
        |GlyphGroupJSharpField|GlyphItemFriend|FieldInternal|  
        |GlyphGroupJSharpField|GlyphItemProtected|FieldProtected|  
        |GlyphGroupJSharpField|GlyphItemPrivate|FieldPrivate|  
        |GlyphGroupJSharpField|GlyphItemShortcut|FieldShortcut|  
        |GlyphGroupJSharpClass|GlyphItemPublic|ClassPublic|  
        |GlyphGroupJSharpClass|GlyphItemInternal|ClassInternal|  
        |GlyphGroupJSharpClass|GlyphItemFriend|ClassInternal|  
        |GlyphGroupJSharpClass|GlyphItemProtected|ClassProtected|  
        |GlyphGroupJSharpClass|GlyphItemPrivate|ClassPrivate|  
        |GlyphGroupJSharpClass|GlyphItemShortcut|ClassShortcut|  
        |GlyphGroupJSharpNamespace|GlyphItemPublic|NamespacePublic|  
        |GlyphGroupJSharpNamespace|GlyphItemInternal|NamespaceInternal|  
        |GlyphGroupJSharpNamespace|GlyphItemFriend|NamespaceInternal|  
        |GlyphGroupJSharpNamespace|GlyphItemProtected|NamespaceProtected|  
        |GlyphGroupJSharpNamespace|GlyphItemPrivate|NamespacePrivate|  
        |GlyphGroupJSharpNamespace|GlyphItemShortcut|NamespaceShortcut|  
        |GlyphGroupJSharpInterface|GlyphItemPublic|InterfacePublic|  
        |GlyphGroupJSharpInterface|GlyphItemInternal|InterfaceInternal|  
        |GlyphGroupJSharpInterface|GlyphItemFriend|InterfaceInternal|  
        |GlyphGroupJSharpInterface|GlyphItemProtected|InterfaceProtected|  
        |GlyphGroupJSharpInterface|GlyphItemPrivate|InterfacePrivate|  
        |GlyphGroupJSharpInterface|GlyphItemShortcut|InterfaceShortcut|  
        |GlyphGroupError||StatusError|  
        |GlyphBscFile||Arquivos de classes|  
        |GlyphAssembly||Referência|  
        |GlyphLibrary||Biblioteca|  
        |GlyphVBProject||VBProjectNode|  
        |GlyphCoolProject||CSProjectNode|  
        |GlyphCppProject||CPPProjectNode|  
        |GlyphDialogId||Caixa de Diálogo|  
        |GlyphOpenFolder||FolderOpened|  
        |GlyphClosedFolder||FolderClosed|  
        |GlyphArrow||GoToNext|  
        |GlyphCSharpFile||CSFileNode|  
        |GlyphCSharpExpansion||Trecho de código|  
        |GlyphKeyword||IntellisenseKeyword|  
        |GlyphInformation||StatusInformation|  
        |GlyphReference||ClassMethodReference|  
        |GlyphRecursion||Recursão|  
        |GlyphXmlItem||Marca|  
        |GlyphJSharpProject||DocumentCollection|  
        |GlyphJSharpDocument||Documento|  
        |GlyphForwardType||GoToNext|  
        |GlyphCallersGraph||Callto://|  
        |GlyphCallGraph||CallFrom|  
        |GlyphWarning||StatusWarning|  
        |GlyphMaybeReference||QuestionMark|  
        |GlyphMaybeCaller||Callto://|  
        |GlyphMaybeCall||CallFrom|  
        |GlyphExtensionMethod||ExtensionMethod|  
        |GlyphExtensionMethodInternal||ExtensionMethod|  
        |GlyphExtensionMethodFriend||ExtensionMethod|  
        |GlyphExtensionMethodProtected||ExtensionMethod|  
        |GlyphExtensionMethodPrivate||ExtensionMethod|  
        |GlyphExtensionMethodShortcut||ExtensionMethod|  
        |GlyphXmlAttribute||XmlAttribute|  
        |GlyphXmlChild||XmlElement|  
        |GlyphXmlDescendant||XmlDescendant|  
        |GlyphXmlNamespace||XmlNamespace|  
        |GlyphXmlAttributeQuestion||XmlAttributeLowConfidence|  
        |GlyphXmlAttributeCheck||XmlAttributeHighConfidence|  
        |GlyphXmlChildQuestion||XmlElementLowConfidence|  
        |GlyphXmlChildCheck||XmlElementHighConfidence|  
        |GlyphXmlDescendantQuestion||XmlDescendantLowConfidence|  
        |GlyphXmlDescendantCheck||XmlDescendantHighConfidence|  
        |GlyphCompletionWarning||IntellisenseWarning|