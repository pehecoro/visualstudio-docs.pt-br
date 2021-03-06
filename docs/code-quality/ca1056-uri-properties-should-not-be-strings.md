---
title: "CA1056: As propriedades URI não devem ser cadeias de caracteres | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-code-analysis
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- UriPropertiesShouldNotBeStrings
- CA1056
helpviewer_keywords:
- UriPropertiesShouldNotBeStrings
- CA1056
ms.assetid: fdc99d29-0904-4a65-baa8-4f76833c953e
caps.latest.revision: "12"
author: gewarren
ms.author: gewarren
manager: ghogen
ms.workload: multiple
ms.openlocfilehash: cdfcce6ff0c9526508b5cf4088968a1a8081c822
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="ca1056-uri-properties-should-not-be-strings"></a>CA1056: as propriedades de URI não devem ser cadeias de caracteres
|||  
|-|-|  
|NomeDoTipo|UriPropertiesShouldNotBeStrings|  
|CheckId|CA1056|  
|Categoria|Microsoft.Design|  
|Alteração Significativa|Quebra|  
  
## <a name="cause"></a>Causa  
 Um tipo declara uma propriedade de cadeia de caracteres cujo nome contém "uri", "Uri", "urn", "Urn", "url" ou "Url".  
  
## <a name="rule-description"></a>Descrição da Regra  
 Essa regra divide o nome da propriedade em tokens com base na convenção de maiusculas e minúsculas de Pascal e verifica se cada token é igual a "uri", "Uri", "urn", "Urn", "url" ou "Url". Se houver uma correspondência, a regra pressupõe que a propriedade representa um identificador de recurso uniforme (URI). Uma representação de cadeia de caracteres de um URI está propensa a erros de análise e de codificação, e pode resultar em vulnerabilidades de segurança. O <xref:System.Uri?displayProperty=fullName> classe fornece esses serviços de forma segura e protegida.  
  
## <a name="how-to-fix-violations"></a>Como Corrigir Violações  
 Para corrigir uma violação desta regra, altere a propriedade para um <xref:System.Uri> tipo.  
  
## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos  
 É seguro suprimir um aviso de que essa regra se a propriedade não representa um URI.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra um tipo `ErrorProne`, que violam essa regra e um tipo, `SaferWay`, que atende a regra.  
  
 [!code-csharp[FxCop.Design.UriNotString#1](../code-quality/codesnippet/CSharp/ca1056-uri-properties-should-not-be-strings_1.cs)]
 [!code-vb[FxCop.Design.UriNotString#1](../code-quality/codesnippet/VisualBasic/ca1056-uri-properties-should-not-be-strings_1.vb)]
 [!code-cpp[FxCop.Design.UriNotString#1](../code-quality/codesnippet/CPP/ca1056-uri-properties-should-not-be-strings_1.cpp)]  
  
## <a name="related-rules"></a>Regras relacionadas  
 [CA1054: os parâmetros de URI não devem ser cadeias de caracteres](../code-quality/ca1054-uri-parameters-should-not-be-strings.md)  
  
 [CA1055: os valores de retorno de URI não devem ser cadeias de caracteres](../code-quality/ca1055-uri-return-values-should-not-be-strings.md)  
  
 [CA2234: passar objetos System.Uri em vez de cadeias de caracteres](../code-quality/ca2234-pass-system-uri-objects-instead-of-strings.md)  
  
 [CA1057: as sobrecargas de URI da cadeia de caracteres chamam sobrecargas System.Uri](../code-quality/ca1057-string-uri-overloads-call-system-uri-overloads.md)