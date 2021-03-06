---
title: Personalizando campos de imagem e texto | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.topic: article
author: gewarren
ms.author: gewarren
manager: ghogen
ms.workload:
- multiple
ms.technology: vs-ide-modeling
ms.openlocfilehash: f577669c685d6f42b73c80f947e8edad0c7b9088
ms.sourcegitcommit: 205d15f4558315e585c67f33d5335d5b41d0fcea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="customizing-text-and-image-fields"></a>Personalizando campos de texto e imagem
Quando você define um decorador de texto em uma forma, ele é representado por um campo de texto. Para obter exemplos de inicialização de campos de texto e outros ShapeFields, inspecione Dsl\GeneratedCode\Shapes.cs em sua solução DSL.  
  
 Um campo de texto é um objeto que gerencia uma área dentro de uma forma, como o espaço atribuído para um rótulo. Uma instância do campo de texto é compartilhada entre várias formas da mesma classe. A instância de TextField não armazena o texto do rótulo separadamente para cada instância do: em vez disso, o `GetDisplayText(ShapeElement)` assume a forma como um parâmetro de método e pode procurar o texto dependente do estado atual da forma e o elemento de modelo.  
  
## <a name="how-the-appearance-of-a-text-field-is-determined"></a>Como a aparência de um campo de texto é determinada  
 O `DoPaint()` método é chamado para exibir o campo na tela. Você pode substituir o padrão `DoPaint(),` ou você pode substituir alguns dos métodos que ele chama. A seguinte versão simplificada dos métodos padrão pode ajudá-lo a entender como substituir o comportamento padrão:  
  
```  
// Simplified version:  
public override void DoPaint(DiagramPaintEventArgs e, ShapeElement parentShape)  
{   
  string text = GetDisplayText(shape);   
  StringFormat format = GetStringFormat(parentShape);  
  Brush brush = GetTextBrush(e.View, shape);  
  using (Font font = GetFont(shape))  
  {  
    e.Graphics.DrawString(text, font, brush, format);  
  }  
}  
// StringFormat determines whether the string is centered etc.  
// To customize statically for all instances of this shape field,   
// assign to DefaultStringFormat.  
// To customize dynamically or per shape, override this:    
public virtual StringFormat GetStringFormat(ShapeElement shape)  
{ return DefaultStringFormat; }  
  
// Override to customize the displayed string:  
public virtual string GetDisplayText(ShapeElement shape)  
{ return this.GetValue(shape).ToString(); }  
  
// Brush determines the text color.  
// To change the brush for every field, change the shape's styleset.   
// To customize to a brush in the style set, override GetTextBrushId.  
// To change the brush to non-standard color, override this.  
// Should take account of whether selected.   
public virtual Brush GetTextBrush(DiagramClientView view, ShapeElement shape)  
{ return shape.StyleSet.GetBrush(this.GetTextBrushId(view, shape)); }  
  
// Brush ID selects a brush from a StyleSet.  
// Either return a member of DiagramBrushes   
// or add your own brush to the shape or application's styleset.  
// Override this to change dynamically or per instance.  
// To change statically, just assign to default values.   
public virtual StyleSetResourceId GetTextBrushId(DiagramClientView view, ShapeElement shape)  
{ return IsSelected(view, shape) ? (view.Focused ? DefaultSelectedTextBrushId  
: DefaultInactiveSelectedTextBrushId ) : DefaultTextBrushId ;  
}  
  
// Font determines the shape and size of the text.  
// To change the font for every field, change the shape's styleset.   
// To customize to a font in the style set, override GetFontId.  
// To change the font to a non-standard font, override this.   
public virtual Font GetFont(ShapeElement shape)  
{ return shape.StyleSet.GetFont(GetFontId(shape)); }  
  
// Selects a font from a styleset.  
// Either return a member of DiagramFonts or   
// add your own font to the shape or application's styleset.  
// To change statically for all instances of this field,   
// assign to DefaultFontId.  
// To change per shape or dynamically, override this.   
public virtual StyleSetResourceId GetFontId(ShapeElement parentShape)  
{ return DefaultFontId; }  
  
```  
  
 Há vários outros pares de `Get` métodos e `Default` propriedades, como `DefaultMultipleLine/GetMultipleLine()`. Você pode atribuir um valor para a propriedade padrão para alterar o valor para todas as instâncias do campo de forma. Para fazer com que o valor variam de instância de uma forma para outra ou dependente do estado da forma ou o elemento de modelo, substitua o `Get` método.  
  
## <a name="static-customizations"></a>Personalizações estáticas  
 Se você quiser alterar todas as instâncias deste campo de forma, primeiro, descubra se você pode definir a propriedade na definição de DSL. Por exemplo, você pode definir o tamanho da fonte e estilo na janela Propriedades.  
  
 Se não, em seguida, substituir o `InitializeShapeFields` método de classe de forma e atribuir um valor apropriado `Default...` propriedade do campo de texto.  
  
> [!WARNING]
>  Para substituir `InitializeShapeFields()`, você deve definir o **gera duplo derivado** propriedade da classe de forma a `true` na definição de DSL.  
  
 Neste exemplo, uma forma tem um campo de texto que será usado para comentários do usuário. Queremos usar a fonte padrão de comentário. Como é uma fonte padrão do conjunto de estilo, podemos definir a id de fonte padrão:  
  
```  
  
 partial class ExampleShape  
{   protected override void InitializeShapeFields(IList<ShapeField> shapeFields)  
    {  
      // Fields set up according to DSL Definition:  
      base.InitializeShapeFields(shapeFields);  
      // Find and update comment field:  
      TextField commentField = ShapeElement.FindShapeField(shapeFields, "CommentDecorator") as TextField;  
      // Use the standard font for comments:  
      commentField.DefaultFontId = DiagramFonts.CommentText;  
  
```  
  
## <a name="dynamic-customizations"></a>Personalizações dinâmicas  
 Para tornar a aparência variar dependem do estado de uma forma ou o elemento de modelo, derive sua subclasse de `TextField` e substitua um ou mais `Get...` métodos. Você também deve substituir o método de InitializeShapeFields da forma e substituir a instância do campo de texto com uma instância de sua classe.  
  
 O exemplo a seguir faz com que a fonte de um campo de texto dependente do estado de uma propriedade de domínio booliano da forma elemento de modelo.  
  
 Para executar esse código de exemplo, crie uma nova solução DSL usando o modelo de idioma mínimo. Adicionar uma propriedade de domínio booliano `AlternateState` para a classe de domínio ExampleElement. Adicione um decorador de ícone para a classe ExampleShape e defina sua imagem para um arquivo de bitmap. Clique em **transformar todos os modelos**. Adicionar um novo arquivo de código no projeto DSL e insira o código a seguir.  
  
 Para testar o código, pressione F5 e, na solução de depuração, abra um diagrama de exemplo. O estado padrão do ícone deve aparecer. Selecione a forma e na janela Propriedades, altere o valor da **AlternateState** propriedade. A fonte do nome do elemento deve ser alterada.  
  
```  
using Microsoft.VisualStudio.Modeling;  
using Microsoft.VisualStudio.Modeling.Diagrams;  
...  
  
  partial class ExampleShape  
  {  
    /// <summary>  
    /// Compose a list of the fields in this shape.  
    /// Called once for each shape class.  
    /// </summary>  
    protected override void InitializeShapeFields(IList<ShapeField> shapeFields)  
    {  
      // Fields set up according to DSL Definition:  
      base.InitializeShapeFields(shapeFields);  
      // Replace the text field for NameDecorator:  
      TextField oldField = ShapeElement.FindShapeField(shapeFields, "NameDecorator") as TextField;  
      shapeFields.Remove(oldField);  
      // Replace with my text field based on DSL Definition values:  
      MyTextField newField = new MyTextField(oldField);  
      shapeFields.Add(newField);  
    }  
  }  
  /// <summary>  
  /// Dynamic font depends on state of model element.  
  /// </summary>  
  public class MyTextField : TextField  
  {  
    public MyTextField(TextField prototype)  
      : base(prototype.Name)  
    {  
      DefaultText = prototype.DefaultText;  
      DefaultFocusable = prototype.DefaultFocusable;  
      DefaultAutoSize = prototype.DefaultAutoSize;  
      AnchoringBehavior.MinimumHeightInLines = prototype.AnchoringBehavior.MinimumHeightInLines;  
      AnchoringBehavior.MinimumWidthInCharacters = prototype.AnchoringBehavior.MinimumWidthInCharacters;  
      DefaultAccessibleState = prototype.DefaultAccessibleState;  
    }  
  
    public override System.Drawing.Font GetFont(ShapeElement parentShape)  
    {  
      // Access the Boolean domain property of the model element:  
      if ((parentShape.ModelElement as ExampleElement).AlternateState)  
        return new System.Drawing.Font("Callisto", 14.0f,  
               System.Drawing.FontStyle.Italic |   
               System.Drawing.FontStyle.Bold);  
      else  
        return base.GetFont(parentShape);  
    }  
  
  }  
  
```  
  
## <a name="style-sets"></a>Conjuntos de estilo  
 O exemplo anterior mostra como você pode alterar o campo de texto para qualquer fonte que está disponível. No entanto, é um método preferível para alterá-lo para um de um conjunto de estilos que está associado com a forma ou com o aplicativo. Para fazer isso, você deve substituir <xref:Microsoft.VisualStudio.Modeling.Diagrams.TextField.GetFontId%2A> ou GetTextBrushId().  
  
 Como alternativa, considere alterar o conjunto de estilos de forma, substituindo <xref:Microsoft.VisualStudio.Modeling.Diagrams.ShapeElement.InitializeResources%2A>. Isso tem o efeito de alterar as fontes e pincéis para todos os campos de forma.  
  
## <a name="customizing-image-fields"></a>Personalizando campos de imagem  
 Quando você define um decorador de imagem em uma forma, e quando você define uma forma de imagem, a área na qual a forma é exibida é gerenciada por um ImageField. Para obter exemplos de inicialização de ImageFields e outros ShapeFields, inspecione Dsl\GeneratedCode\Shapes.cs em sua solução DSL.  
  
 Um ImageField é um objeto que gerencia uma área dentro de uma forma, como o espaço atribuído a um decorador. Uma instância de ImageField é compartilhada entre várias formas da mesma classe de forma. A instância de ImageField não armazena uma imagem separada para cada forma: em vez disso, o `GetDisplayImage(ShapeElement)` método assume a forma como um parâmetro e podem consultar a imagem dependem do estado atual da forma e o elemento de modelo.  
  
 Se você quiser um comportamento especial, como uma imagem de variável, você pode criar sua própria classe derivada de ImageField.  
  
#### <a name="to-create-a-subclass-of-imagefield"></a>Para criar uma subclasse de ImageField  
  
1.  Definir o **gera duplo derivado** propriedade da classe em sua definição de DSL forma pai.  
  
2.  Substituir o `InitializeShapeFields` método de sua classe de forma.  
  
    -   Criar um novo arquivo de código no projeto DSL e gravar uma definição de classe parcial para a classe de forma. Substitua a definição de método existe.  
  
3.  Inspecione o código de `InitializeShapeFields` em DSL\GeneratedCode\Shapes.cs.  
  
     O método de substituição, chame o método base e, em seguida, criar uma instância de sua própria classe do campo de imagem. Use esta opção para substituir o campo de imagem regular no `shapeFields` lista.  
  
## <a name="dynamic-icons"></a>Ícones dinâmicos  
 Este exemplo faz um ícone dependem do estado da forma elemento de modelo.  
  
> [!WARNING]
>  Este exemplo demonstra como fazer um decorador de imagem dinâmica. Mas se você quiser alternar entre uma ou duas imagens dependendo do estado de uma variável de modelo, é mais simples criar vários decoradores de imagem, localizá-los na mesma posição na forma e, em seguida, defina o filtro de visibilidade depender dos valores específicos do modelo variável. Para definir o filtro, selecione o mapa de formas na definição de DSL, abra a janela de detalhes de DSL e clique na guia decoradores.  
  
 Para executar esse código de exemplo, crie uma nova solução DSL usando o modelo de idioma mínimo. Adicionar uma propriedade de domínio booliano `AlternateState` para a classe de domínio ExampleElement. Adicione um decorador de ícone para a classe ExampleShape e defina sua imagem para um arquivo de bitmap. Clique em **transformar todos os modelos**. Adicionar um novo arquivo de código no projeto DSL e insira o código a seguir.  
  
 Para testar o código, pressione F5 e, na solução de depuração, abra um diagrama de exemplo. O estado padrão do ícone deve aparecer. Selecione a forma e na janela Propriedades, altere o valor da **AlternateState** propriedade. O ícone aparecerão girado por meio de 90 graus, em que a forma.  
  
```csharp  
using Microsoft.VisualStudio.Modeling;  
using Microsoft.VisualStudio.Modeling.Diagrams;  
...  
partial class ExampleShape  
{  
    /// <summary>  
    /// Compose a list of the fields in this shape.  
    /// Called once for each shape class.  
    /// </summary>  
    /// <param name="shapeFields"></param>  
    protected override void InitializeShapeFields(IList<ShapeField> shapeFields)  
    {  
      // Fields set up according to DSL Definition:  
      base.InitializeShapeFields(shapeFields);  
  
      // Replace the image field:  
      ShapeField oldField = ShapeElement.FindShapeField(shapeFields, "IconDecorator");  
      shapeFields.Remove(oldField);  
      // Must keep the same name:  
      MyImageField newField = new MyImageField(oldField.Name);  
      shapeFields.Add(newField);  
      newField.DefaultImage = (oldField as ImageField).DefaultImage.Clone() as System.Drawing.Image;  
    }  
  }  
  
  public class MyImageField : ImageField  
  {  
    public MyImageField(string tag) : base(tag) { }  
  
    /// <summary>  
    /// Get the image for this field in the given shape.  
    /// </summary>  
    public override System.Drawing.Image GetDisplayImage(ShapeElement parentShape)  
    {  
      ExampleElement element = parentShape.ModelElement as ExampleElement;  
      if (element.AlternateState == true)  
        return AlternateImage;  
      else  
        return base.GetDisplayImage(parentShape);  
    }  
  
    private System.Drawing.Image alternateImage;  
    public System.Drawing.Image AlternateImage  
    {  
      get  
      {  
        if (alternateImage == null)  
        {  
          // Alternate image is a copy of the default, rotated by 90 degrees:  
          alternateImage = this.DefaultImage.Clone() as System.Drawing.Image;  
          alternateImage.RotateFlip(System.Drawing.RotateFlipType.Rotate90FlipNone);  
        }  
        return alternateImage;  
      }  
    }  
  }  
}  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Definindo as formas e conectores](../modeling/defining-shapes-and-connectors.md)   
 [Definindo uma imagem de plano de fundo em um diagrama](../modeling/setting-a-background-image-on-a-diagram.md)   
 [Navegar e atualizar um modelo no código do programa](../modeling/navigating-and-updating-a-model-in-program-code.md)   
 [Escrevendo código para personalizar uma linguagem específica de domínio](../modeling/writing-code-to-customise-a-domain-specific-language.md)