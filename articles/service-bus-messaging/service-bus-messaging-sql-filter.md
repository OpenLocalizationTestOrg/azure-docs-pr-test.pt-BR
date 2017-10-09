---
title: "referência de sintaxe SQLFilter do barramento de serviço do aaaAzure | Microsoft Docs"
description: "Detalhes sobre a gramática de SQLFilter."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/27/2017
ms.author: sethm
ms.openlocfilehash: ea49d42e343a6b324eb34c7831ff6be2855346e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sqlfilter-syntax"></a>Sintaxe SQLFilter

Um *SqlFilter* é uma instância da saudação [SqlFilter classe](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)e representa uma expressão de filtro com base em linguagem SQL que é avaliada em relação a um [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage). Um SqlFilter oferece suporte a um subconjunto do padrão de saudação SQL-92.  
  
 Este tópico lista detalhes sobre a gramática de SqlFilter.  
  
```  
<predicate ::=  
      { NOT <predicate> }  
      | <predicate> AND <predicate>  
      | <predicate> OR <predicate>  
      | <expression> { = | <> | != | > | >= | < | <= } <expression>  
      | <property> IS [NOT] NULL  
      | <expression> [NOT] IN ( <expression> [, ...n] )  
      | <expression> [NOT] LIKE <pattern> [ESCAPE <escape_char>]  
      | EXISTS ( <property> )  
      | ( <predicate> )  
  
```  
  
```  
<expression> ::=  
      <constant>   
      | <function>  
      | <property>  
      | <expression> { + | - | * | / | % } <expression>  
      | { + | - } <expression>  
      | ( <expression> )  
  
```  
  
```  
<property> :=   
       [<scope> .] <property_name>  
  
```  
  
## <a name="arguments"></a>Argumentos  
  
-   `<scope>`é uma cadeia de caracteres opcional que indica o escopo Olá Olá `<property_name>`. Os valores válidos são `sys` ou `user`. Olá `sys` valor indica o escopo do sistema onde `<property_name>` é um nome de propriedade pública da saudação [classe BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage). `user`indica o escopo do usuário onde `<property_name>` é uma chave de saudação [classe BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dicionário. `user`escopo é o escopo padrão de saudação se `<scope>` não for especificado.  
  
## <a name="remarks"></a>Comentários

Uma tentativa de tooaccess uma propriedade do sistema não existente é um erro, enquanto uma propriedade de usuário tentativa tooaccess não existente não é um erro. Em vez disso, uma propriedade de usuário inexistente é internamente avaliada como um valor desconhecido. Um valor desconhecido é tratado especialmente durante a avaliação de operador.  
  
## <a name="propertyname"></a>property_name  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a>Argumentos  

 `<regular_identifier>`é uma cadeia de caracteres representada por Olá seguinte expressão regular:  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
Essa gramática significa qualquer cadeia de caracteres que começa com uma letra e é seguida por um ou mais sublinhados/letras/dígitos.  
  
`[:IsLetter:]` significa qualquer caractere Unicode categorizado como uma letra do Unicode. `System.Char.IsLetter(c)` retorna `true` se `c` é uma letra do Unicode.  
  
`[:IsDigit:]` significa qualquer caractere Unicode categorizado como um dígito decimal. `System.Char.IsDigit(c)` retorna `true` se `c` é um dígito do Unicode.  
  
Um `<regular_identifier>` não pode ser uma palavra-chave reservada.  
  
`<delimited_identifier>` é qualquer cadeia de caracteres incluída em colchetes esquerdo/direito ([]). Um colchete direito é representado como dois colchetes direitos. Olá, estes são exemplos de `<delimited_identifier>`:  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
`<quoted_identifier>` é qualquer cadeia de caracteres entre aspas duplas. Aspas duplas no identificador são representadas como duas aspas duplas. Não é recomendável toouse identificadores entre aspas porque ele pode facilmente ser confundido com uma constante de cadeia de caracteres. Use um identificador delimitado, se possível. Olá, a seguir é um exemplo de `<quoted_identifier>`:  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a>pattern  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a>Comentários
  
`<pattern>` deve ser uma expressão avaliada como uma cadeia de caracteres. Ele é usado como um padrão de saudação operador LIKE.      Ele pode conter Olá caracteres curinga a seguir:  
  
-   `%`: qualquer cadeia de caracteres com zero ou mais caracteres.  
  
-   `_`: qualquer caractere único.  
  
## <a name="escapechar"></a>escape_char  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a>Comentários  

`<escape_char>` deve ser uma expressão avaliada como uma cadeia de caracteres de comprimento 1. Ele é usado como um caractere de escape para Olá operador LIKE.  
  
 Por exemplo, `property LIKE 'ABC\%' ESCAPE '\'` corresponde a `ABC%`, em vez de a uma cadeia de caracteres que começa com `ABC`.  
  
## <a name="constant"></a>constante  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a>Argumentos  
  
-   `<integer_constant>` é uma cadeia de números que não são incluídos em aspas e que não contêm pontos decimais. Olá valores são armazenados como `System.Int64` internamente, e siga Olá mesmo intervalo.  
  
     Estes são exemplos de constantes longas:  
  
    ```  
    1894  
    2  
    ```  
  
-   `<decimal_constant>` é uma cadeia de números que não são incluídos em aspas e que contêm um ponto decimal. Olá valores são armazenados como `System.Double` internamente e siga Olá mesmo intervalo/precisão.  
  
     Em uma versão futura, esse número pode ser armazenado em uma dados diferentes tipo toosupport número semântica exata, portanto você não deve confiar Olá fatos Olá subjacente tipo de dados é `System.Double` para `<decimal_constant>`.  
  
     Olá seguem exemplos de constantes decimais:  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   `<approximate_number_constant>` é um número escrito em notação científica. Olá valores são armazenados como `System.Double` internamente e siga Olá mesmo intervalo/precisão. Olá seguem exemplos de constantes de número aproximados de:  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a>boolean_constant  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a>Comentários  

Constantes booleanas são representados por palavras-chave de saudação **TRUE** ou **FALSE**. Olá valores são armazenados como `System.Boolean`.  
  
## <a name="stringconstant"></a>string_constant  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a>Comentários  

Constantes de cadeia de caracteres são incluídas em aspas simples e incluem caracteres Unicode válidos. Uma aspa simples inserida em uma constante de cadeia de caracteres é representada como duas aspas simples.  
  
## <a name="function"></a>função  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a>Comentários
  
Olá `newid()` função retorna um **GUID** gerado pelo Olá `System.Guid.NewGuid()` método.  
  
Olá `property(name)` função retorna o valor de saudação da propriedade Olá referenciado pelo `name`. Olá `name` valor pode ser qualquer expressão válida que retorna um valor de cadeia de caracteres.  
  
## <a name="considerations"></a>Considerações
  
Considere o seguinte Olá [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) semântica:  
  
-   Os nomes de propriedade não diferenciam maiúsculas de minúsculas.  
  
-   Os operadores seguem a semântica de conversão implícita do C# sempre que possível.  
  
-   As propriedades do sistema são propriedades públicas expostas em instâncias de [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).  
  
    Considere o seguinte Olá `IS [NOT] NULL` semântica:  
  
    -   `property IS NULL`é avaliado como `true` se qualquer uma das propriedades de saudação não existe ou Olá o valor da propriedade é `null`.  
  
### <a name="property-evaluation-semantics"></a>Semântica de avaliação da propriedade  
  
-   Um tooevaluate de tentativa de uma propriedade inexistente sistema gera um [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) exceção.  
  
-   Uma propriedade que não existe internamente é avaliada como **desconhecida**.  
  
 Avaliação desconhecida em operadores aritméticos:  
  
-   Operadores binários, se o hello esquerda e/ou o lado direito dos operandos é avaliado como **desconhecido**, Olá resultado será **desconhecido**.  
  
-   Operadores unários, se um operando é avaliado como **desconhecido**, Olá resultado será **desconhecido**.  
  
 Avaliação desconhecida em operadores de comparação binária:  
  
-   Se o hello esquerda e/ou o lado direito dos operandos é avaliado como **desconhecido**, Olá resultado será **desconhecido**.  
  
 Avaliação desconhecida em `[NOT] LIKE`:  
  
-   Se qualquer operando é avaliado como **desconhecido**, Olá resultado será **desconhecido**.  
  
 Avaliação desconhecida em `[NOT] IN`:  
  
-   Se a saudação à esquerda é avaliada como **desconhecido**, Olá resultado será **desconhecido**.  
  
 Avaliação desconhecida no operador **AND**:  
  
```  
+---+---+---+---+  
|AND| T | F | U |  
+---+---+---+---+  
| T | T | F | U |  
+---+---+---+---+  
| F | F | F | F |  
+---+---+---+---+  
| U | U | F | U |  
+---+---+---+---+  
```  
  
 Avaliação desconhecida no operador **OR**:  
  
```  
+---+---+---+---+  
|OR | T | F | U |  
+---+---+---+---+  
| T | T | T | T |  
+---+---+---+---+  
| F | T | F | U |  
+---+---+---+---+  
| U | T | U | U |  
+---+---+---+---+  
```  
  
### <a name="operator-binding-semantics"></a>Semântica de associação do operador
  
-   Operadores de comparação como `>`, `>=`, `<`, `<=`, `!=`, e `=` siga Olá mesmo promoções e conversões implícitas de tipo de semântica de operador Olá c# de associação de dados.  
  
-   Operadores aritméticos, como `+`, `-`, `*`, `/`, e `%` siga Olá mesmo promoções e conversões implícitas de tipo de semântica de operador Olá c# de associação de dados.

## <a name="next-steps"></a>Próximas etapas

- [Classe SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
- [Classe SQLRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)