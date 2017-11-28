---
title: "Referência da sintaxe SQLRuleAction no Azure | Microsoft Docs"
description: "Detalhes sobre a gramática de SQLRuleAction."
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
ms.date: 06/28/2017
ms.author: sethm
ms.openlocfilehash: 7379b7f58563675f28d77928d933c0d9c7992e71
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="sqlruleaction-syntax"></a><span data-ttu-id="ce2ab-103">Sintaxe SQLRuleAction</span><span class="sxs-lookup"><span data-stu-id="ce2ab-103">SQLRuleAction syntax</span></span>

<span data-ttu-id="ce2ab-104">Um *SqlRuleAction* é uma instância da classe [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) e representa um conjunto de ações gravadas na sintaxe baseada na linguagem SQL executada em uma [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="ce2ab-104">A *SqlRuleAction* is an instance of the [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) class, and represents set of actions written in SQL-language based syntax that is performed against a [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span>   
  
<span data-ttu-id="ce2ab-105">Este tópico lista os detalhes sobre a gramática de ação de regras do SQL.</span><span class="sxs-lookup"><span data-stu-id="ce2ab-105">This topic lists details about the SQL rule action grammar.</span></span>  
  
```  
<statements> ::=
    <statement> [, ...n]  
  
```  
  
```  
<statement> ::=
    <action> [;]
    Remarks
    -------
    Semicolon is optional.  
  
```  
  
```  
<action> ::=
    SET <property> = <expression>
    REMOVE <property>  
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
  
## <a name="arguments"></a><span data-ttu-id="ce2ab-106">Argumentos</span><span class="sxs-lookup"><span data-stu-id="ce2ab-106">Arguments</span></span>  
  
-   <span data-ttu-id="ce2ab-107">`<scope>` é uma cadeia de caracteres opcional que indica o escopo do `<property_name>`.</span><span class="sxs-lookup"><span data-stu-id="ce2ab-107">`<scope>` is an optional string indicating the scope of the `<property_name>`.</span></span> <span data-ttu-id="ce2ab-108">Os valores válidos são `sys` ou `user`.</span><span class="sxs-lookup"><span data-stu-id="ce2ab-108">Valid values are `sys` or `user`.</span></span> <span data-ttu-id="ce2ab-109">O valor `sys` indica o escopo do sistema, em que `<property_name>` é um nome de propriedade pública da [Classe BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="ce2ab-109">The `sys` value indicates system scope where `<property_name>` is a public property name of the [BrokeredMessage Class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="ce2ab-110">`user` indica o escopo do usuário, em que `<property_name>` é uma chave de dicionário da [Classe BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="ce2ab-110">`user` indicates user scope where `<property_name>` is a key of the [BrokeredMessage Class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dictionary.</span></span> <span data-ttu-id="ce2ab-111">O escopo `user` será o escopo padrão se `<scope>` não for especificado.</span><span class="sxs-lookup"><span data-stu-id="ce2ab-111">`user` scope is the default scope if `<scope>` is not specified.</span></span>  
  
### <a name="remarks"></a><span data-ttu-id="ce2ab-112">Comentários</span><span class="sxs-lookup"><span data-stu-id="ce2ab-112">Remarks</span></span>  

<span data-ttu-id="ce2ab-113">Uma tentativa de acessar uma propriedade inexistente do sistema é um erro, ao passo que uma tentativa de acessar uma propriedade de usuário inexistente não é um erro.</span><span class="sxs-lookup"><span data-stu-id="ce2ab-113">An attempt to access a non-existent system property is an error, while an attempt to access a non-existent user property is not an error.</span></span> <span data-ttu-id="ce2ab-114">Em vez disso, uma propriedade de usuário inexistente é internamente avaliada como um valor desconhecido.</span><span class="sxs-lookup"><span data-stu-id="ce2ab-114">Instead, a non-existent user property is internally evaluated as an unknown value.</span></span> <span data-ttu-id="ce2ab-115">Um valor desconhecido é tratado especialmente durante a avaliação de operador.</span><span class="sxs-lookup"><span data-stu-id="ce2ab-115">An unknown value is treated specially during operator evaluation.</span></span>  
  
## <a name="propertyname"></a><span data-ttu-id="ce2ab-116">property_name</span><span class="sxs-lookup"><span data-stu-id="ce2ab-116">property_name</span></span>  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a><span data-ttu-id="ce2ab-117">Argumentos</span><span class="sxs-lookup"><span data-stu-id="ce2ab-117">Arguments</span></span>  
 <span data-ttu-id="ce2ab-118">`<regular_identifier>` é uma cadeia de caracteres representada pela seguinte expressão regular:</span><span class="sxs-lookup"><span data-stu-id="ce2ab-118">`<regular_identifier>` is a string represented by the following regular expression:</span></span>  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
 <span data-ttu-id="ce2ab-119">Isso significa qualquer cadeia de caracteres que começa com uma letra e é seguida por um ou mais sublinhados/letras/dígitos.</span><span class="sxs-lookup"><span data-stu-id="ce2ab-119">This means any string that starts with a letter and is followed by one or more underscore/letter/digit.</span></span>  
  
 <span data-ttu-id="ce2ab-120">`[:IsLetter:]` significa qualquer caractere Unicode categorizado como uma letra do Unicode.</span><span class="sxs-lookup"><span data-stu-id="ce2ab-120">`[:IsLetter:]` means any Unicode character that is categorized as a Unicode letter.</span></span> <span data-ttu-id="ce2ab-121">`System.Char.IsLetter(c)` retorna `true` se `c` é uma letra do Unicode.</span><span class="sxs-lookup"><span data-stu-id="ce2ab-121">`System.Char.IsLetter(c)` returns `true` if `c` is a Unicode letter.</span></span>  
  
 <span data-ttu-id="ce2ab-122">`[:IsDigit:]` significa qualquer caractere Unicode categorizado como um dígito decimal.</span><span class="sxs-lookup"><span data-stu-id="ce2ab-122">`[:IsDigit:]` means any Unicode character that is categorized as a decimal digit.</span></span> <span data-ttu-id="ce2ab-123">`System.Char.IsDigit(c)` retorna `true` se `c` é um dígito do Unicode.</span><span class="sxs-lookup"><span data-stu-id="ce2ab-123">`System.Char.IsDigit(c)` returns `true` if `c` is a Unicode digit.</span></span>  
  
 <span data-ttu-id="ce2ab-124">Um `<regular_identifier>` não pode ser uma palavra-chave reservada.</span><span class="sxs-lookup"><span data-stu-id="ce2ab-124">A `<regular_identifier>` cannot be a reserved keyword.</span></span>  
  
 <span data-ttu-id="ce2ab-125">`<delimited_identifier>` é qualquer cadeia de caracteres incluída em colchetes esquerdo/direito ([]).</span><span class="sxs-lookup"><span data-stu-id="ce2ab-125">`<delimited_identifier>` is any string that is enclosed with left/right square brackets ([]).</span></span> <span data-ttu-id="ce2ab-126">Um colchete direito é representado como dois colchetes direitos.</span><span class="sxs-lookup"><span data-stu-id="ce2ab-126">A right square bracket is represented as two right square brackets.</span></span> <span data-ttu-id="ce2ab-127">Estes são exemplos de `<delimited_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="ce2ab-127">The following are examples of `<delimited_identifier>`:</span></span>  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
 <span data-ttu-id="ce2ab-128">`<quoted_identifier>` é qualquer cadeia de caracteres entre aspas duplas.</span><span class="sxs-lookup"><span data-stu-id="ce2ab-128">`<quoted_identifier>` is any string that is enclosed with double quotation marks.</span></span> <span data-ttu-id="ce2ab-129">Aspas duplas no identificador são representadas como duas aspas duplas.</span><span class="sxs-lookup"><span data-stu-id="ce2ab-129">A double quotation mark in identifier is represented as two double quotation marks.</span></span> <span data-ttu-id="ce2ab-130">Não é recomendável usar identificadores entre aspas, porque pode ser confundido facilmente por uma constante de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="ce2ab-130">It is not recommended to use quoted identifiers because it can easily be confused with a string constant.</span></span> <span data-ttu-id="ce2ab-131">Use um identificador delimitado, se possível.</span><span class="sxs-lookup"><span data-stu-id="ce2ab-131">Use a delimited identifier if possible.</span></span> <span data-ttu-id="ce2ab-132">Este é um exemplo de `<quoted_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="ce2ab-132">The following is an example of `<quoted_identifier>`:</span></span>  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a><span data-ttu-id="ce2ab-133">pattern</span><span class="sxs-lookup"><span data-stu-id="ce2ab-133">pattern</span></span>  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="ce2ab-134">Comentários</span><span class="sxs-lookup"><span data-stu-id="ce2ab-134">Remarks</span></span>
  
 <span data-ttu-id="ce2ab-135">`<pattern>` deve ser uma expressão avaliada como uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="ce2ab-135">`<pattern>` must be an expression that is evaluated as a string.</span></span> <span data-ttu-id="ce2ab-136">Usado como um padrão para o operador LIKE.</span><span class="sxs-lookup"><span data-stu-id="ce2ab-136">It is used as a pattern for the LIKE operator.</span></span>      <span data-ttu-id="ce2ab-137">Pode conter os seguintes caracteres curinga:</span><span class="sxs-lookup"><span data-stu-id="ce2ab-137">It can contain the following wildcard characters:</span></span>  
  
-   <span data-ttu-id="ce2ab-138">`%`: qualquer cadeia de caracteres com zero ou mais caracteres.</span><span class="sxs-lookup"><span data-stu-id="ce2ab-138">`%`:  Any string of zero or more characters.</span></span>  
  
-   <span data-ttu-id="ce2ab-139">`_`: qualquer caractere único.</span><span class="sxs-lookup"><span data-stu-id="ce2ab-139">`_`: Any single character.</span></span>  
  
## <a name="escapechar"></a><span data-ttu-id="ce2ab-140">escape_char</span><span class="sxs-lookup"><span data-stu-id="ce2ab-140">escape_char</span></span>  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="ce2ab-141">Comentários</span><span class="sxs-lookup"><span data-stu-id="ce2ab-141">Remarks</span></span>
  
 <span data-ttu-id="ce2ab-142">`<escape_char>` deve ser uma expressão avaliada como uma cadeia de caracteres de comprimento 1.</span><span class="sxs-lookup"><span data-stu-id="ce2ab-142">`<escape_char>` must be an expression that is evaluated as a string of length 1.</span></span> <span data-ttu-id="ce2ab-143">Usado como um caractere de escape para o operador LIKE.</span><span class="sxs-lookup"><span data-stu-id="ce2ab-143">It is used as an escape character for the LIKE operator.</span></span>  
  
 <span data-ttu-id="ce2ab-144">Por exemplo, `property LIKE 'ABC\%' ESCAPE '\'` corresponde a `ABC%`, em vez de a uma cadeia de caracteres que começa com `ABC`.</span><span class="sxs-lookup"><span data-stu-id="ce2ab-144">For example, `property LIKE 'ABC\%' ESCAPE '\'` matches `ABC%` rather than a string that starts with `ABC`.</span></span>  
  
## <a name="constant"></a><span data-ttu-id="ce2ab-145">constante</span><span class="sxs-lookup"><span data-stu-id="ce2ab-145">constant</span></span>  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a><span data-ttu-id="ce2ab-146">Argumentos</span><span class="sxs-lookup"><span data-stu-id="ce2ab-146">Arguments</span></span>  
  
-   <span data-ttu-id="ce2ab-147">`<integer_constant>` é uma cadeia de números que não são incluídos em aspas e que não contêm pontos decimais.</span><span class="sxs-lookup"><span data-stu-id="ce2ab-147">`<integer_constant>` is a string of numbers that are not enclosed in quotation marks and do not contain decimal points.</span></span> <span data-ttu-id="ce2ab-148">Os valores são armazenados como `System.Int64` internamente e seguem o mesmo intervalo.</span><span class="sxs-lookup"><span data-stu-id="ce2ab-148">The values are stored as `System.Int64` internally, and follow the same range.</span></span>  
  
     <span data-ttu-id="ce2ab-149">Estes são exemplos de constantes longas:</span><span class="sxs-lookup"><span data-stu-id="ce2ab-149">The following are examples of long constants:</span></span>  
  
    ```  
    1894  
    2  
    ```  
  
-   <span data-ttu-id="ce2ab-150">`<decimal_constant>` é uma cadeia de números que não são incluídos em aspas e que contêm um ponto decimal.</span><span class="sxs-lookup"><span data-stu-id="ce2ab-150">`<decimal_constant>` is a string of numbers that are not enclosed in quotation marks, and contain a decimal point.</span></span> <span data-ttu-id="ce2ab-151">Os valores são armazenados como `System.Double` internamente e seguem o mesmo intervalo e a mesma precisão.</span><span class="sxs-lookup"><span data-stu-id="ce2ab-151">The values are stored as `System.Double` internally, and follow the same range/precision.</span></span>  
  
     <span data-ttu-id="ce2ab-152">Em uma versão futura, esse número poderá ser armazenado em outro tipo de dados para dar suporte à semântica de número exato; portanto, você não deve se basear no fato de que o tipo de dados subjacente é `System.Double` para `<decimal_constant>`.</span><span class="sxs-lookup"><span data-stu-id="ce2ab-152">In a future version, this number might be stored in a different data type to support exact number semantics, so you should not rely on the fact the underlying data type is `System.Double` for `<decimal_constant>`.</span></span>  
  
     <span data-ttu-id="ce2ab-153">Estes são exemplos de constantes decimais:</span><span class="sxs-lookup"><span data-stu-id="ce2ab-153">The following are examples of decimal constants:</span></span>  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   <span data-ttu-id="ce2ab-154">`<approximate_number_constant>` é um número escrito em notação científica.</span><span class="sxs-lookup"><span data-stu-id="ce2ab-154">`<approximate_number_constant>` is a number written in scientific notation.</span></span> <span data-ttu-id="ce2ab-155">Os valores são armazenados como `System.Double` internamente e seguem o mesmo intervalo e a mesma precisão.</span><span class="sxs-lookup"><span data-stu-id="ce2ab-155">The values are stored as `System.Double` internally, and follow the same range/precision.</span></span> <span data-ttu-id="ce2ab-156">Estes são exemplos de constantes de número aproximado:</span><span class="sxs-lookup"><span data-stu-id="ce2ab-156">The following are examples of approximate number constants:</span></span>  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a><span data-ttu-id="ce2ab-157">boolean_constant</span><span class="sxs-lookup"><span data-stu-id="ce2ab-157">boolean_constant</span></span>  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a><span data-ttu-id="ce2ab-158">Comentários</span><span class="sxs-lookup"><span data-stu-id="ce2ab-158">Remarks</span></span>
  
<span data-ttu-id="ce2ab-159">Constantes boolianas são representadas pelas palavras-chave `TRUE` ou `FALSE`.</span><span class="sxs-lookup"><span data-stu-id="ce2ab-159">Boolean constants are represented by the keywords `TRUE` or `FALSE`.</span></span> <span data-ttu-id="ce2ab-160">Os valores são armazenados como `System.Boolean`.</span><span class="sxs-lookup"><span data-stu-id="ce2ab-160">The values are stored as `System.Boolean`.</span></span>  
  
## <a name="stringconstant"></a><span data-ttu-id="ce2ab-161">string_constant</span><span class="sxs-lookup"><span data-stu-id="ce2ab-161">string_constant</span></span>  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a><span data-ttu-id="ce2ab-162">Comentários</span><span class="sxs-lookup"><span data-stu-id="ce2ab-162">Remarks</span></span>
  
<span data-ttu-id="ce2ab-163">Constantes de cadeia de caracteres são incluídas em aspas simples e incluem caracteres Unicode válidos.</span><span class="sxs-lookup"><span data-stu-id="ce2ab-163">String constants are enclosed in single quotation marks and include any valid Unicode characters.</span></span> <span data-ttu-id="ce2ab-164">Uma aspa simples inserida em uma constante de cadeia de caracteres é representada como duas aspas simples.</span><span class="sxs-lookup"><span data-stu-id="ce2ab-164">A single quotation mark embedded in a string constant is represented as two single quotation marks.</span></span>  
  
## <a name="function"></a><span data-ttu-id="ce2ab-165">função</span><span class="sxs-lookup"><span data-stu-id="ce2ab-165">function</span></span>  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a><span data-ttu-id="ce2ab-166">Comentários</span><span class="sxs-lookup"><span data-stu-id="ce2ab-166">Remarks</span></span>  

<span data-ttu-id="ce2ab-167">A função `newid()` retorna um **System.Guid** gerado pelo método `System.Guid.NewGuid()`.</span><span class="sxs-lookup"><span data-stu-id="ce2ab-167">The `newid()` function returns a **System.Guid** generated by the `System.Guid.NewGuid()` method.</span></span>  
  
<span data-ttu-id="ce2ab-168">A função `property(name)` retorna o valor da propriedade referenciada por `name`.</span><span class="sxs-lookup"><span data-stu-id="ce2ab-168">The `property(name)` function returns the value of the property referenced by `name`.</span></span> <span data-ttu-id="ce2ab-169">O valor `name` pode ser qualquer expressão válida que retorna um valor de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="ce2ab-169">The `name` value can be any valid expression that returns a string value.</span></span>  
  
## <a name="considerations"></a><span data-ttu-id="ce2ab-170">Considerações</span><span class="sxs-lookup"><span data-stu-id="ce2ab-170">Considerations</span></span>

- <span data-ttu-id="ce2ab-171">SET é usado para criar uma nova propriedade ou atualizar o valor de uma propriedade existente.</span><span class="sxs-lookup"><span data-stu-id="ce2ab-171">SET is used to create a new property or update the value of an existing property.</span></span>
- <span data-ttu-id="ce2ab-172">REMOVE é usado para remover uma propriedade.</span><span class="sxs-lookup"><span data-stu-id="ce2ab-172">REMOVE is used to remove a property.</span></span>
- <span data-ttu-id="ce2ab-173">SET executa uma conversão implícita, se possível, quando o tipo de expressão e o tipo de propriedade existente são diferentes.</span><span class="sxs-lookup"><span data-stu-id="ce2ab-173">SET performs implicit conversion if possible when the expression type and the existing property type are different.</span></span>
- <span data-ttu-id="ce2ab-174">A ação falhará se propriedades do sistema inexistentes forem referenciadas.</span><span class="sxs-lookup"><span data-stu-id="ce2ab-174">Action fails if non-existent system properties were referenced.</span></span>
- <span data-ttu-id="ce2ab-175">A ação não falhará se propriedades de usuário inexistentes forem referenciadas.</span><span class="sxs-lookup"><span data-stu-id="ce2ab-175">Action does not fail if non-existent user properties were referenced.</span></span>
- <span data-ttu-id="ce2ab-176">Uma propriedade de usuário inexistente é avaliada como “Desconhecida” internamente, seguindo a mesma semântica de [SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) ao avaliar operadores.</span><span class="sxs-lookup"><span data-stu-id="ce2ab-176">A non-existent user property is evaluated as "Unknown" internally, following the same semantics as [SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) when evaluating operators.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce2ab-177">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ce2ab-177">Next steps</span></span>

- [<span data-ttu-id="ce2ab-178">Classe SQLRuleAction</span><span class="sxs-lookup"><span data-stu-id="ce2ab-178">SQLRuleAction class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)
- [<span data-ttu-id="ce2ab-179">Classe SQLFilter</span><span class="sxs-lookup"><span data-stu-id="ce2ab-179">SQLFilter class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
