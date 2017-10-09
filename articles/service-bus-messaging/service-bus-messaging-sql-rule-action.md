---
title: "referência de sintaxe aaaSQLRuleAction no Azure | Microsoft Docs"
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
ms.openlocfilehash: 8ef281f942847bcc535b83a5ffb30d03539734f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sqlruleaction-syntax"></a><span data-ttu-id="a8307-103">Sintaxe SQLRuleAction</span><span class="sxs-lookup"><span data-stu-id="a8307-103">SQLRuleAction syntax</span></span>

<span data-ttu-id="a8307-104">Um *SqlRuleAction* é uma instância da saudação [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) classe e representa o conjunto de ações gravadas na linguagem SQL com base em sintaxe é executada em um [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="a8307-104">A *SqlRuleAction* is an instance of hello [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) class, and represents set of actions written in SQL-language based syntax that is performed against a [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span>   
  
<span data-ttu-id="a8307-105">Este tópico lista detalhes sobre Olá gramática de ação de regra SQL.</span><span class="sxs-lookup"><span data-stu-id="a8307-105">This topic lists details about hello SQL rule action grammar.</span></span>  
  
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
  
## <a name="arguments"></a><span data-ttu-id="a8307-106">Argumentos</span><span class="sxs-lookup"><span data-stu-id="a8307-106">Arguments</span></span>  
  
-   <span data-ttu-id="a8307-107">`<scope>`é uma cadeia de caracteres opcional que indica o escopo Olá Olá `<property_name>`.</span><span class="sxs-lookup"><span data-stu-id="a8307-107">`<scope>` is an optional string indicating hello scope of hello `<property_name>`.</span></span> <span data-ttu-id="a8307-108">Os valores válidos são `sys` ou `user`.</span><span class="sxs-lookup"><span data-stu-id="a8307-108">Valid values are `sys` or `user`.</span></span> <span data-ttu-id="a8307-109">Olá `sys` valor indica o escopo do sistema onde `<property_name>` é um nome de propriedade pública da saudação [classe BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="a8307-109">hello `sys` value indicates system scope where `<property_name>` is a public property name of hello [BrokeredMessage Class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="a8307-110">`user`indica o escopo do usuário onde `<property_name>` é uma chave de saudação [classe BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dicionário.</span><span class="sxs-lookup"><span data-stu-id="a8307-110">`user` indicates user scope where `<property_name>` is a key of hello [BrokeredMessage Class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dictionary.</span></span> <span data-ttu-id="a8307-111">`user`escopo é o escopo padrão de saudação se `<scope>` não for especificado.</span><span class="sxs-lookup"><span data-stu-id="a8307-111">`user` scope is hello default scope if `<scope>` is not specified.</span></span>  
  
### <a name="remarks"></a><span data-ttu-id="a8307-112">Comentários</span><span class="sxs-lookup"><span data-stu-id="a8307-112">Remarks</span></span>  

<span data-ttu-id="a8307-113">Uma tentativa de tooaccess uma propriedade do sistema não existente é um erro, enquanto uma propriedade de usuário tentativa tooaccess não existente não é um erro.</span><span class="sxs-lookup"><span data-stu-id="a8307-113">An attempt tooaccess a non-existent system property is an error, while an attempt tooaccess a non-existent user property is not an error.</span></span> <span data-ttu-id="a8307-114">Em vez disso, uma propriedade de usuário inexistente é internamente avaliada como um valor desconhecido.</span><span class="sxs-lookup"><span data-stu-id="a8307-114">Instead, a non-existent user property is internally evaluated as an unknown value.</span></span> <span data-ttu-id="a8307-115">Um valor desconhecido é tratado especialmente durante a avaliação de operador.</span><span class="sxs-lookup"><span data-stu-id="a8307-115">An unknown value is treated specially during operator evaluation.</span></span>  
  
## <a name="propertyname"></a><span data-ttu-id="a8307-116">property_name</span><span class="sxs-lookup"><span data-stu-id="a8307-116">property_name</span></span>  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a><span data-ttu-id="a8307-117">Argumentos</span><span class="sxs-lookup"><span data-stu-id="a8307-117">Arguments</span></span>  
 <span data-ttu-id="a8307-118">`<regular_identifier>`é uma cadeia de caracteres representada por Olá seguinte expressão regular:</span><span class="sxs-lookup"><span data-stu-id="a8307-118">`<regular_identifier>` is a string represented by hello following regular expression:</span></span>  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
 <span data-ttu-id="a8307-119">Isso significa qualquer cadeia de caracteres que começa com uma letra e é seguida por um ou mais sublinhados/letras/dígitos.</span><span class="sxs-lookup"><span data-stu-id="a8307-119">This means any string that starts with a letter and is followed by one or more underscore/letter/digit.</span></span>  
  
 <span data-ttu-id="a8307-120">`[:IsLetter:]` significa qualquer caractere Unicode categorizado como uma letra do Unicode.</span><span class="sxs-lookup"><span data-stu-id="a8307-120">`[:IsLetter:]` means any Unicode character that is categorized as a Unicode letter.</span></span> <span data-ttu-id="a8307-121">`System.Char.IsLetter(c)` retorna `true` se `c` é uma letra do Unicode.</span><span class="sxs-lookup"><span data-stu-id="a8307-121">`System.Char.IsLetter(c)` returns `true` if `c` is a Unicode letter.</span></span>  
  
 <span data-ttu-id="a8307-122">`[:IsDigit:]` significa qualquer caractere Unicode categorizado como um dígito decimal.</span><span class="sxs-lookup"><span data-stu-id="a8307-122">`[:IsDigit:]` means any Unicode character that is categorized as a decimal digit.</span></span> <span data-ttu-id="a8307-123">`System.Char.IsDigit(c)` retorna `true` se `c` é um dígito do Unicode.</span><span class="sxs-lookup"><span data-stu-id="a8307-123">`System.Char.IsDigit(c)` returns `true` if `c` is a Unicode digit.</span></span>  
  
 <span data-ttu-id="a8307-124">Um `<regular_identifier>` não pode ser uma palavra-chave reservada.</span><span class="sxs-lookup"><span data-stu-id="a8307-124">A `<regular_identifier>` cannot be a reserved keyword.</span></span>  
  
 <span data-ttu-id="a8307-125">`<delimited_identifier>` é qualquer cadeia de caracteres incluída em colchetes esquerdo/direito ([]).</span><span class="sxs-lookup"><span data-stu-id="a8307-125">`<delimited_identifier>` is any string that is enclosed with left/right square brackets ([]).</span></span> <span data-ttu-id="a8307-126">Um colchete direito é representado como dois colchetes direitos.</span><span class="sxs-lookup"><span data-stu-id="a8307-126">A right square bracket is represented as two right square brackets.</span></span> <span data-ttu-id="a8307-127">Olá, estes são exemplos de `<delimited_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="a8307-127">hello following are examples of `<delimited_identifier>`:</span></span>  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
 <span data-ttu-id="a8307-128">`<quoted_identifier>` é qualquer cadeia de caracteres entre aspas duplas.</span><span class="sxs-lookup"><span data-stu-id="a8307-128">`<quoted_identifier>` is any string that is enclosed with double quotation marks.</span></span> <span data-ttu-id="a8307-129">Aspas duplas no identificador são representadas como duas aspas duplas.</span><span class="sxs-lookup"><span data-stu-id="a8307-129">A double quotation mark in identifier is represented as two double quotation marks.</span></span> <span data-ttu-id="a8307-130">Não é recomendável toouse identificadores entre aspas porque ele pode facilmente ser confundido com uma constante de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="a8307-130">It is not recommended toouse quoted identifiers because it can easily be confused with a string constant.</span></span> <span data-ttu-id="a8307-131">Use um identificador delimitado, se possível.</span><span class="sxs-lookup"><span data-stu-id="a8307-131">Use a delimited identifier if possible.</span></span> <span data-ttu-id="a8307-132">Olá, a seguir é um exemplo de `<quoted_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="a8307-132">hello following is an example of `<quoted_identifier>`:</span></span>  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a><span data-ttu-id="a8307-133">pattern</span><span class="sxs-lookup"><span data-stu-id="a8307-133">pattern</span></span>  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="a8307-134">Comentários</span><span class="sxs-lookup"><span data-stu-id="a8307-134">Remarks</span></span>
  
 <span data-ttu-id="a8307-135">`<pattern>` deve ser uma expressão avaliada como uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="a8307-135">`<pattern>` must be an expression that is evaluated as a string.</span></span> <span data-ttu-id="a8307-136">Ele é usado como um padrão de saudação operador LIKE.</span><span class="sxs-lookup"><span data-stu-id="a8307-136">It is used as a pattern for hello LIKE operator.</span></span>      <span data-ttu-id="a8307-137">Ele pode conter Olá caracteres curinga a seguir:</span><span class="sxs-lookup"><span data-stu-id="a8307-137">It can contain hello following wildcard characters:</span></span>  
  
-   <span data-ttu-id="a8307-138">`%`: qualquer cadeia de caracteres com zero ou mais caracteres.</span><span class="sxs-lookup"><span data-stu-id="a8307-138">`%`:  Any string of zero or more characters.</span></span>  
  
-   <span data-ttu-id="a8307-139">`_`: qualquer caractere único.</span><span class="sxs-lookup"><span data-stu-id="a8307-139">`_`: Any single character.</span></span>  
  
## <a name="escapechar"></a><span data-ttu-id="a8307-140">escape_char</span><span class="sxs-lookup"><span data-stu-id="a8307-140">escape_char</span></span>  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="a8307-141">Comentários</span><span class="sxs-lookup"><span data-stu-id="a8307-141">Remarks</span></span>
  
 <span data-ttu-id="a8307-142">`<escape_char>` deve ser uma expressão avaliada como uma cadeia de caracteres de comprimento 1.</span><span class="sxs-lookup"><span data-stu-id="a8307-142">`<escape_char>` must be an expression that is evaluated as a string of length 1.</span></span> <span data-ttu-id="a8307-143">Ele é usado como um caractere de escape para Olá operador LIKE.</span><span class="sxs-lookup"><span data-stu-id="a8307-143">It is used as an escape character for hello LIKE operator.</span></span>  
  
 <span data-ttu-id="a8307-144">Por exemplo, `property LIKE 'ABC\%' ESCAPE '\'` corresponde a `ABC%`, em vez de a uma cadeia de caracteres que começa com `ABC`.</span><span class="sxs-lookup"><span data-stu-id="a8307-144">For example, `property LIKE 'ABC\%' ESCAPE '\'` matches `ABC%` rather than a string that starts with `ABC`.</span></span>  
  
## <a name="constant"></a><span data-ttu-id="a8307-145">constante</span><span class="sxs-lookup"><span data-stu-id="a8307-145">constant</span></span>  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a><span data-ttu-id="a8307-146">Argumentos</span><span class="sxs-lookup"><span data-stu-id="a8307-146">Arguments</span></span>  
  
-   <span data-ttu-id="a8307-147">`<integer_constant>` é uma cadeia de números que não são incluídos em aspas e que não contêm pontos decimais.</span><span class="sxs-lookup"><span data-stu-id="a8307-147">`<integer_constant>` is a string of numbers that are not enclosed in quotation marks and do not contain decimal points.</span></span> <span data-ttu-id="a8307-148">Olá valores são armazenados como `System.Int64` internamente, e siga Olá mesmo intervalo.</span><span class="sxs-lookup"><span data-stu-id="a8307-148">hello values are stored as `System.Int64` internally, and follow hello same range.</span></span>  
  
     <span data-ttu-id="a8307-149">Olá seguem exemplos de constantes de tempo:</span><span class="sxs-lookup"><span data-stu-id="a8307-149">hello following are examples of long constants:</span></span>  
  
    ```  
    1894  
    2  
    ```  
  
-   <span data-ttu-id="a8307-150">`<decimal_constant>` é uma cadeia de números que não são incluídos em aspas e que contêm um ponto decimal.</span><span class="sxs-lookup"><span data-stu-id="a8307-150">`<decimal_constant>` is a string of numbers that are not enclosed in quotation marks, and contain a decimal point.</span></span> <span data-ttu-id="a8307-151">Olá valores são armazenados como `System.Double` internamente e siga Olá mesmo intervalo/precisão.</span><span class="sxs-lookup"><span data-stu-id="a8307-151">hello values are stored as `System.Double` internally, and follow hello same range/precision.</span></span>  
  
     <span data-ttu-id="a8307-152">Em uma versão futura, esse número pode ser armazenado em uma dados diferentes tipo toosupport número semântica exata, portanto você não deve confiar Olá fatos Olá subjacente tipo de dados é `System.Double` para `<decimal_constant>`.</span><span class="sxs-lookup"><span data-stu-id="a8307-152">In a future version, this number might be stored in a different data type toosupport exact number semantics, so you should not rely on hello fact hello underlying data type is `System.Double` for `<decimal_constant>`.</span></span>  
  
     <span data-ttu-id="a8307-153">Olá seguem exemplos de constantes decimais:</span><span class="sxs-lookup"><span data-stu-id="a8307-153">hello following are examples of decimal constants:</span></span>  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   <span data-ttu-id="a8307-154">`<approximate_number_constant>` é um número escrito em notação científica.</span><span class="sxs-lookup"><span data-stu-id="a8307-154">`<approximate_number_constant>` is a number written in scientific notation.</span></span> <span data-ttu-id="a8307-155">Olá valores são armazenados como `System.Double` internamente e siga Olá mesmo intervalo/precisão.</span><span class="sxs-lookup"><span data-stu-id="a8307-155">hello values are stored as `System.Double` internally, and follow hello same range/precision.</span></span> <span data-ttu-id="a8307-156">Olá seguem exemplos de constantes de número aproximados de:</span><span class="sxs-lookup"><span data-stu-id="a8307-156">hello following are examples of approximate number constants:</span></span>  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a><span data-ttu-id="a8307-157">boolean_constant</span><span class="sxs-lookup"><span data-stu-id="a8307-157">boolean_constant</span></span>  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a><span data-ttu-id="a8307-158">Comentários</span><span class="sxs-lookup"><span data-stu-id="a8307-158">Remarks</span></span>
  
<span data-ttu-id="a8307-159">Constantes booleanas são representados por palavras-chave de saudação `TRUE` ou `FALSE`.</span><span class="sxs-lookup"><span data-stu-id="a8307-159">Boolean constants are represented by hello keywords `TRUE` or `FALSE`.</span></span> <span data-ttu-id="a8307-160">Olá valores são armazenados como `System.Boolean`.</span><span class="sxs-lookup"><span data-stu-id="a8307-160">hello values are stored as `System.Boolean`.</span></span>  
  
## <a name="stringconstant"></a><span data-ttu-id="a8307-161">string_constant</span><span class="sxs-lookup"><span data-stu-id="a8307-161">string_constant</span></span>  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a><span data-ttu-id="a8307-162">Comentários</span><span class="sxs-lookup"><span data-stu-id="a8307-162">Remarks</span></span>
  
<span data-ttu-id="a8307-163">Constantes de cadeia de caracteres são incluídas em aspas simples e incluem caracteres Unicode válidos.</span><span class="sxs-lookup"><span data-stu-id="a8307-163">String constants are enclosed in single quotation marks and include any valid Unicode characters.</span></span> <span data-ttu-id="a8307-164">Uma aspa simples inserida em uma constante de cadeia de caracteres é representada como duas aspas simples.</span><span class="sxs-lookup"><span data-stu-id="a8307-164">A single quotation mark embedded in a string constant is represented as two single quotation marks.</span></span>  
  
## <a name="function"></a><span data-ttu-id="a8307-165">função</span><span class="sxs-lookup"><span data-stu-id="a8307-165">function</span></span>  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a><span data-ttu-id="a8307-166">Comentários</span><span class="sxs-lookup"><span data-stu-id="a8307-166">Remarks</span></span>  

<span data-ttu-id="a8307-167">Olá `newid()` função retorna um **GUID** gerado pelo Olá `System.Guid.NewGuid()` método.</span><span class="sxs-lookup"><span data-stu-id="a8307-167">hello `newid()` function returns a **System.Guid** generated by hello `System.Guid.NewGuid()` method.</span></span>  
  
<span data-ttu-id="a8307-168">Olá `property(name)` função retorna o valor de saudação da propriedade Olá referenciado pelo `name`.</span><span class="sxs-lookup"><span data-stu-id="a8307-168">hello `property(name)` function returns hello value of hello property referenced by `name`.</span></span> <span data-ttu-id="a8307-169">Olá `name` valor pode ser qualquer expressão válida que retorna um valor de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="a8307-169">hello `name` value can be any valid expression that returns a string value.</span></span>  
  
## <a name="considerations"></a><span data-ttu-id="a8307-170">Considerações</span><span class="sxs-lookup"><span data-stu-id="a8307-170">Considerations</span></span>

- <span data-ttu-id="a8307-171">O conjunto é usado toocreate um novo valor de saudação de propriedade ou atualização de uma propriedade existente.</span><span class="sxs-lookup"><span data-stu-id="a8307-171">SET is used toocreate a new property or update hello value of an existing property.</span></span>
- <span data-ttu-id="a8307-172">REMOVER é uma propriedade de tooremove usado.</span><span class="sxs-lookup"><span data-stu-id="a8307-172">REMOVE is used tooremove a property.</span></span>
- <span data-ttu-id="a8307-173">SET executa a conversão implícita se possível quando o tipo de expressão hello e tipo de propriedade existente Olá são diferentes.</span><span class="sxs-lookup"><span data-stu-id="a8307-173">SET performs implicit conversion if possible when hello expression type and hello existing property type are different.</span></span>
- <span data-ttu-id="a8307-174">A ação falhará se propriedades do sistema inexistentes forem referenciadas.</span><span class="sxs-lookup"><span data-stu-id="a8307-174">Action fails if non-existent system properties were referenced.</span></span>
- <span data-ttu-id="a8307-175">A ação não falhará se propriedades de usuário inexistentes forem referenciadas.</span><span class="sxs-lookup"><span data-stu-id="a8307-175">Action does not fail if non-existent user properties were referenced.</span></span>
- <span data-ttu-id="a8307-176">Uma propriedade de usuário inexistente é avaliada como "Desconhecido", internamente, seguinte Olá a mesma semântica de [SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) ao avaliar a operadores.</span><span class="sxs-lookup"><span data-stu-id="a8307-176">A non-existent user property is evaluated as "Unknown" internally, following hello same semantics as [SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) when evaluating operators.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8307-177">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a8307-177">Next steps</span></span>

- [<span data-ttu-id="a8307-178">Classe SQLRuleAction</span><span class="sxs-lookup"><span data-stu-id="a8307-178">SQLRuleAction class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)
- [<span data-ttu-id="a8307-179">Classe SQLFilter</span><span class="sxs-lookup"><span data-stu-id="a8307-179">SQLFilter class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
