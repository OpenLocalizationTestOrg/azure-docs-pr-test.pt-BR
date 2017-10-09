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
# <a name="sqlfilter-syntax"></a><span data-ttu-id="08654-103">Sintaxe SQLFilter</span><span class="sxs-lookup"><span data-stu-id="08654-103">SQLFilter syntax</span></span>

<span data-ttu-id="08654-104">Um *SqlFilter* é uma instância da saudação [SqlFilter classe](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)e representa uma expressão de filtro com base em linguagem SQL que é avaliada em relação a um [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="08654-104">A *SqlFilter* is an instance of hello [SqlFilter class](/dotnet/api/microsoft.servicebus.messaging.sqlfilter), and represents a SQL language-based filter expression that is evaluated against a [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="08654-105">Um SqlFilter oferece suporte a um subconjunto do padrão de saudação SQL-92.</span><span class="sxs-lookup"><span data-stu-id="08654-105">A SqlFilter supports a subset of hello SQL-92 standard.</span></span>  
  
 <span data-ttu-id="08654-106">Este tópico lista detalhes sobre a gramática de SqlFilter.</span><span class="sxs-lookup"><span data-stu-id="08654-106">This topic lists details about SqlFilter grammar.</span></span>  
  
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
  
## <a name="arguments"></a><span data-ttu-id="08654-107">Argumentos</span><span class="sxs-lookup"><span data-stu-id="08654-107">Arguments</span></span>  
  
-   <span data-ttu-id="08654-108">`<scope>`é uma cadeia de caracteres opcional que indica o escopo Olá Olá `<property_name>`.</span><span class="sxs-lookup"><span data-stu-id="08654-108">`<scope>` is an optional string indicating hello scope of hello `<property_name>`.</span></span> <span data-ttu-id="08654-109">Os valores válidos são `sys` ou `user`.</span><span class="sxs-lookup"><span data-stu-id="08654-109">Valid values are `sys` or `user`.</span></span> <span data-ttu-id="08654-110">Olá `sys` valor indica o escopo do sistema onde `<property_name>` é um nome de propriedade pública da saudação [classe BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="08654-110">hello `sys` value indicates system scope where `<property_name>` is a public property name of hello [BrokeredMessage class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="08654-111">`user`indica o escopo do usuário onde `<property_name>` é uma chave de saudação [classe BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dicionário.</span><span class="sxs-lookup"><span data-stu-id="08654-111">`user` indicates user scope where `<property_name>` is a key of hello [BrokeredMessage class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dictionary.</span></span> <span data-ttu-id="08654-112">`user`escopo é o escopo padrão de saudação se `<scope>` não for especificado.</span><span class="sxs-lookup"><span data-stu-id="08654-112">`user` scope is hello default scope if `<scope>` is not specified.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="08654-113">Comentários</span><span class="sxs-lookup"><span data-stu-id="08654-113">Remarks</span></span>

<span data-ttu-id="08654-114">Uma tentativa de tooaccess uma propriedade do sistema não existente é um erro, enquanto uma propriedade de usuário tentativa tooaccess não existente não é um erro.</span><span class="sxs-lookup"><span data-stu-id="08654-114">An attempt tooaccess a non-existent system property is an error, while an attempt tooaccess a non-existent user property is not an error.</span></span> <span data-ttu-id="08654-115">Em vez disso, uma propriedade de usuário inexistente é internamente avaliada como um valor desconhecido.</span><span class="sxs-lookup"><span data-stu-id="08654-115">Instead, a non-existent user property is internally evaluated as an unknown value.</span></span> <span data-ttu-id="08654-116">Um valor desconhecido é tratado especialmente durante a avaliação de operador.</span><span class="sxs-lookup"><span data-stu-id="08654-116">An unknown value is treated specially during operator evaluation.</span></span>  
  
## <a name="propertyname"></a><span data-ttu-id="08654-117">property_name</span><span class="sxs-lookup"><span data-stu-id="08654-117">property_name</span></span>  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a><span data-ttu-id="08654-118">Argumentos</span><span class="sxs-lookup"><span data-stu-id="08654-118">Arguments</span></span>  

 <span data-ttu-id="08654-119">`<regular_identifier>`é uma cadeia de caracteres representada por Olá seguinte expressão regular:</span><span class="sxs-lookup"><span data-stu-id="08654-119">`<regular_identifier>` is a string represented by hello following regular expression:</span></span>  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
<span data-ttu-id="08654-120">Essa gramática significa qualquer cadeia de caracteres que começa com uma letra e é seguida por um ou mais sublinhados/letras/dígitos.</span><span class="sxs-lookup"><span data-stu-id="08654-120">This grammar means any string that starts with a letter and is followed by one or more underscore/letter/digit.</span></span>  
  
<span data-ttu-id="08654-121">`[:IsLetter:]` significa qualquer caractere Unicode categorizado como uma letra do Unicode.</span><span class="sxs-lookup"><span data-stu-id="08654-121">`[:IsLetter:]` means any Unicode character that is categorized as a Unicode letter.</span></span> <span data-ttu-id="08654-122">`System.Char.IsLetter(c)` retorna `true` se `c` é uma letra do Unicode.</span><span class="sxs-lookup"><span data-stu-id="08654-122">`System.Char.IsLetter(c)` returns `true` if `c` is a Unicode letter.</span></span>  
  
<span data-ttu-id="08654-123">`[:IsDigit:]` significa qualquer caractere Unicode categorizado como um dígito decimal.</span><span class="sxs-lookup"><span data-stu-id="08654-123">`[:IsDigit:]` means any Unicode character that is categorized as a decimal digit.</span></span> <span data-ttu-id="08654-124">`System.Char.IsDigit(c)` retorna `true` se `c` é um dígito do Unicode.</span><span class="sxs-lookup"><span data-stu-id="08654-124">`System.Char.IsDigit(c)` returns `true` if `c` is a Unicode digit.</span></span>  
  
<span data-ttu-id="08654-125">Um `<regular_identifier>` não pode ser uma palavra-chave reservada.</span><span class="sxs-lookup"><span data-stu-id="08654-125">A `<regular_identifier>` cannot be a reserved keyword.</span></span>  
  
<span data-ttu-id="08654-126">`<delimited_identifier>` é qualquer cadeia de caracteres incluída em colchetes esquerdo/direito ([]).</span><span class="sxs-lookup"><span data-stu-id="08654-126">`<delimited_identifier>` is any string that is enclosed with left/right square brackets ([]).</span></span> <span data-ttu-id="08654-127">Um colchete direito é representado como dois colchetes direitos.</span><span class="sxs-lookup"><span data-stu-id="08654-127">A right square bracket is represented as two right square brackets.</span></span> <span data-ttu-id="08654-128">Olá, estes são exemplos de `<delimited_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="08654-128">hello following are examples of `<delimited_identifier>`:</span></span>  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
<span data-ttu-id="08654-129">`<quoted_identifier>` é qualquer cadeia de caracteres entre aspas duplas.</span><span class="sxs-lookup"><span data-stu-id="08654-129">`<quoted_identifier>` is any string that is enclosed with double quotation marks.</span></span> <span data-ttu-id="08654-130">Aspas duplas no identificador são representadas como duas aspas duplas.</span><span class="sxs-lookup"><span data-stu-id="08654-130">A double quotation mark in identifier is represented as two double quotation marks.</span></span> <span data-ttu-id="08654-131">Não é recomendável toouse identificadores entre aspas porque ele pode facilmente ser confundido com uma constante de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="08654-131">It is not recommended toouse quoted identifiers because it can easily be confused with a string constant.</span></span> <span data-ttu-id="08654-132">Use um identificador delimitado, se possível.</span><span class="sxs-lookup"><span data-stu-id="08654-132">Use a delimited identifier if possible.</span></span> <span data-ttu-id="08654-133">Olá, a seguir é um exemplo de `<quoted_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="08654-133">hello following is an example of `<quoted_identifier>`:</span></span>  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a><span data-ttu-id="08654-134">pattern</span><span class="sxs-lookup"><span data-stu-id="08654-134">pattern</span></span>  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="08654-135">Comentários</span><span class="sxs-lookup"><span data-stu-id="08654-135">Remarks</span></span>
  
<span data-ttu-id="08654-136">`<pattern>` deve ser uma expressão avaliada como uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="08654-136">`<pattern>` must be an expression that is evaluated as a string.</span></span> <span data-ttu-id="08654-137">Ele é usado como um padrão de saudação operador LIKE.</span><span class="sxs-lookup"><span data-stu-id="08654-137">It is used as a pattern for hello LIKE operator.</span></span>      <span data-ttu-id="08654-138">Ele pode conter Olá caracteres curinga a seguir:</span><span class="sxs-lookup"><span data-stu-id="08654-138">It can contain hello following wildcard characters:</span></span>  
  
-   <span data-ttu-id="08654-139">`%`: qualquer cadeia de caracteres com zero ou mais caracteres.</span><span class="sxs-lookup"><span data-stu-id="08654-139">`%`:  Any string of zero or more characters.</span></span>  
  
-   <span data-ttu-id="08654-140">`_`: qualquer caractere único.</span><span class="sxs-lookup"><span data-stu-id="08654-140">`_`: Any single character.</span></span>  
  
## <a name="escapechar"></a><span data-ttu-id="08654-141">escape_char</span><span class="sxs-lookup"><span data-stu-id="08654-141">escape_char</span></span>  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="08654-142">Comentários</span><span class="sxs-lookup"><span data-stu-id="08654-142">Remarks</span></span>  

<span data-ttu-id="08654-143">`<escape_char>` deve ser uma expressão avaliada como uma cadeia de caracteres de comprimento 1.</span><span class="sxs-lookup"><span data-stu-id="08654-143">`<escape_char>` must be an expression that is evaluated as a string of length 1.</span></span> <span data-ttu-id="08654-144">Ele é usado como um caractere de escape para Olá operador LIKE.</span><span class="sxs-lookup"><span data-stu-id="08654-144">It is used as an escape character for hello LIKE operator.</span></span>  
  
 <span data-ttu-id="08654-145">Por exemplo, `property LIKE 'ABC\%' ESCAPE '\'` corresponde a `ABC%`, em vez de a uma cadeia de caracteres que começa com `ABC`.</span><span class="sxs-lookup"><span data-stu-id="08654-145">For example, `property LIKE 'ABC\%' ESCAPE '\'` matches `ABC%` rather than a string that starts with `ABC`.</span></span>  
  
## <a name="constant"></a><span data-ttu-id="08654-146">constante</span><span class="sxs-lookup"><span data-stu-id="08654-146">constant</span></span>  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a><span data-ttu-id="08654-147">Argumentos</span><span class="sxs-lookup"><span data-stu-id="08654-147">Arguments</span></span>  
  
-   <span data-ttu-id="08654-148">`<integer_constant>` é uma cadeia de números que não são incluídos em aspas e que não contêm pontos decimais.</span><span class="sxs-lookup"><span data-stu-id="08654-148">`<integer_constant>` is a string of numbers that are not enclosed in quotation marks and do not contain decimal points.</span></span> <span data-ttu-id="08654-149">Olá valores são armazenados como `System.Int64` internamente, e siga Olá mesmo intervalo.</span><span class="sxs-lookup"><span data-stu-id="08654-149">hello values are stored as `System.Int64` internally, and follow hello same range.</span></span>  
  
     <span data-ttu-id="08654-150">Estes são exemplos de constantes longas:</span><span class="sxs-lookup"><span data-stu-id="08654-150">These are examples of long constants:</span></span>  
  
    ```  
    1894  
    2  
    ```  
  
-   <span data-ttu-id="08654-151">`<decimal_constant>` é uma cadeia de números que não são incluídos em aspas e que contêm um ponto decimal.</span><span class="sxs-lookup"><span data-stu-id="08654-151">`<decimal_constant>` is a string of numbers that are not enclosed in quotation marks, and contain a decimal point.</span></span> <span data-ttu-id="08654-152">Olá valores são armazenados como `System.Double` internamente e siga Olá mesmo intervalo/precisão.</span><span class="sxs-lookup"><span data-stu-id="08654-152">hello values are stored as `System.Double` internally, and follow hello same range/precision.</span></span>  
  
     <span data-ttu-id="08654-153">Em uma versão futura, esse número pode ser armazenado em uma dados diferentes tipo toosupport número semântica exata, portanto você não deve confiar Olá fatos Olá subjacente tipo de dados é `System.Double` para `<decimal_constant>`.</span><span class="sxs-lookup"><span data-stu-id="08654-153">In a future version, this number might be stored in a different data type toosupport exact number semantics, so you should not rely on hello fact hello underlying data type is `System.Double` for `<decimal_constant>`.</span></span>  
  
     <span data-ttu-id="08654-154">Olá seguem exemplos de constantes decimais:</span><span class="sxs-lookup"><span data-stu-id="08654-154">hello following are examples of decimal constants:</span></span>  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   <span data-ttu-id="08654-155">`<approximate_number_constant>` é um número escrito em notação científica.</span><span class="sxs-lookup"><span data-stu-id="08654-155">`<approximate_number_constant>` is a number written in scientific notation.</span></span> <span data-ttu-id="08654-156">Olá valores são armazenados como `System.Double` internamente e siga Olá mesmo intervalo/precisão.</span><span class="sxs-lookup"><span data-stu-id="08654-156">hello values are stored as `System.Double` internally, and follow hello same range/precision.</span></span> <span data-ttu-id="08654-157">Olá seguem exemplos de constantes de número aproximados de:</span><span class="sxs-lookup"><span data-stu-id="08654-157">hello following are examples of approximate number constants:</span></span>  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a><span data-ttu-id="08654-158">boolean_constant</span><span class="sxs-lookup"><span data-stu-id="08654-158">boolean_constant</span></span>  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a><span data-ttu-id="08654-159">Comentários</span><span class="sxs-lookup"><span data-stu-id="08654-159">Remarks</span></span>  

<span data-ttu-id="08654-160">Constantes booleanas são representados por palavras-chave de saudação **TRUE** ou **FALSE**.</span><span class="sxs-lookup"><span data-stu-id="08654-160">Boolean constants are represented by hello keywords **TRUE** or **FALSE**.</span></span> <span data-ttu-id="08654-161">Olá valores são armazenados como `System.Boolean`.</span><span class="sxs-lookup"><span data-stu-id="08654-161">hello values are stored as `System.Boolean`.</span></span>  
  
## <a name="stringconstant"></a><span data-ttu-id="08654-162">string_constant</span><span class="sxs-lookup"><span data-stu-id="08654-162">string_constant</span></span>  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a><span data-ttu-id="08654-163">Comentários</span><span class="sxs-lookup"><span data-stu-id="08654-163">Remarks</span></span>  

<span data-ttu-id="08654-164">Constantes de cadeia de caracteres são incluídas em aspas simples e incluem caracteres Unicode válidos.</span><span class="sxs-lookup"><span data-stu-id="08654-164">String constants are enclosed in single quotation marks and include any valid Unicode characters.</span></span> <span data-ttu-id="08654-165">Uma aspa simples inserida em uma constante de cadeia de caracteres é representada como duas aspas simples.</span><span class="sxs-lookup"><span data-stu-id="08654-165">A single quotation mark embedded in a string constant is represented as two single quotation marks.</span></span>  
  
## <a name="function"></a><span data-ttu-id="08654-166">função</span><span class="sxs-lookup"><span data-stu-id="08654-166">function</span></span>  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a><span data-ttu-id="08654-167">Comentários</span><span class="sxs-lookup"><span data-stu-id="08654-167">Remarks</span></span>
  
<span data-ttu-id="08654-168">Olá `newid()` função retorna um **GUID** gerado pelo Olá `System.Guid.NewGuid()` método.</span><span class="sxs-lookup"><span data-stu-id="08654-168">hello `newid()` function returns a **System.Guid** generated by hello `System.Guid.NewGuid()` method.</span></span>  
  
<span data-ttu-id="08654-169">Olá `property(name)` função retorna o valor de saudação da propriedade Olá referenciado pelo `name`.</span><span class="sxs-lookup"><span data-stu-id="08654-169">hello `property(name)` function returns hello value of hello property referenced by `name`.</span></span> <span data-ttu-id="08654-170">Olá `name` valor pode ser qualquer expressão válida que retorna um valor de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="08654-170">hello `name` value can be any valid expression that returns a string value.</span></span>  
  
## <a name="considerations"></a><span data-ttu-id="08654-171">Considerações</span><span class="sxs-lookup"><span data-stu-id="08654-171">Considerations</span></span>
  
<span data-ttu-id="08654-172">Considere o seguinte Olá [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) semântica:</span><span class="sxs-lookup"><span data-stu-id="08654-172">Consider hello following [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) semantics:</span></span>  
  
-   <span data-ttu-id="08654-173">Os nomes de propriedade não diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="08654-173">Property names are case-insensitive.</span></span>  
  
-   <span data-ttu-id="08654-174">Os operadores seguem a semântica de conversão implícita do C# sempre que possível.</span><span class="sxs-lookup"><span data-stu-id="08654-174">Operators follow C# implicit conversion semantics whenever possible.</span></span>  
  
-   <span data-ttu-id="08654-175">As propriedades do sistema são propriedades públicas expostas em instâncias de [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="08654-175">System properties are public properties exposed in [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) instances.</span></span>  
  
    <span data-ttu-id="08654-176">Considere o seguinte Olá `IS [NOT] NULL` semântica:</span><span class="sxs-lookup"><span data-stu-id="08654-176">Consider hello following `IS [NOT] NULL` semantics:</span></span>  
  
    -   <span data-ttu-id="08654-177">`property IS NULL`é avaliado como `true` se qualquer uma das propriedades de saudação não existe ou Olá o valor da propriedade é `null`.</span><span class="sxs-lookup"><span data-stu-id="08654-177">`property IS NULL` is evaluated as `true` if either hello property doesn't exist or hello property's value is `null`.</span></span>  
  
### <a name="property-evaluation-semantics"></a><span data-ttu-id="08654-178">Semântica de avaliação da propriedade</span><span class="sxs-lookup"><span data-stu-id="08654-178">Property evaluation semantics</span></span>  
  
-   <span data-ttu-id="08654-179">Um tooevaluate de tentativa de uma propriedade inexistente sistema gera um [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) exceção.</span><span class="sxs-lookup"><span data-stu-id="08654-179">An attempt tooevaluate a non-existent system property throws a [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) exception.</span></span>  
  
-   <span data-ttu-id="08654-180">Uma propriedade que não existe internamente é avaliada como **desconhecida**.</span><span class="sxs-lookup"><span data-stu-id="08654-180">A property that does not exist is internally evaluated as **unknown**.</span></span>  
  
 <span data-ttu-id="08654-181">Avaliação desconhecida em operadores aritméticos:</span><span class="sxs-lookup"><span data-stu-id="08654-181">Unknown evaluation in arithmetic operators:</span></span>  
  
-   <span data-ttu-id="08654-182">Operadores binários, se o hello esquerda e/ou o lado direito dos operandos é avaliado como **desconhecido**, Olá resultado será **desconhecido**.</span><span class="sxs-lookup"><span data-stu-id="08654-182">For binary operators, if either hello left and/or right side of operands is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
-   <span data-ttu-id="08654-183">Operadores unários, se um operando é avaliado como **desconhecido**, Olá resultado será **desconhecido**.</span><span class="sxs-lookup"><span data-stu-id="08654-183">For unary operators, if an operand is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
 <span data-ttu-id="08654-184">Avaliação desconhecida em operadores de comparação binária:</span><span class="sxs-lookup"><span data-stu-id="08654-184">Unknown evaluation in binary comparison operators:</span></span>  
  
-   <span data-ttu-id="08654-185">Se o hello esquerda e/ou o lado direito dos operandos é avaliado como **desconhecido**, Olá resultado será **desconhecido**.</span><span class="sxs-lookup"><span data-stu-id="08654-185">If either hello left and/or right side of operands is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
 <span data-ttu-id="08654-186">Avaliação desconhecida em `[NOT] LIKE`:</span><span class="sxs-lookup"><span data-stu-id="08654-186">Unknown evaluation in `[NOT] LIKE`:</span></span>  
  
-   <span data-ttu-id="08654-187">Se qualquer operando é avaliado como **desconhecido**, Olá resultado será **desconhecido**.</span><span class="sxs-lookup"><span data-stu-id="08654-187">If any operand is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
 <span data-ttu-id="08654-188">Avaliação desconhecida em `[NOT] IN`:</span><span class="sxs-lookup"><span data-stu-id="08654-188">Unknown evaluation in `[NOT] IN`:</span></span>  
  
-   <span data-ttu-id="08654-189">Se a saudação à esquerda é avaliada como **desconhecido**, Olá resultado será **desconhecido**.</span><span class="sxs-lookup"><span data-stu-id="08654-189">If hello left operand is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
 <span data-ttu-id="08654-190">Avaliação desconhecida no operador **AND**:</span><span class="sxs-lookup"><span data-stu-id="08654-190">Unknown evaluation in **AND** operator:</span></span>  
  
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
  
 <span data-ttu-id="08654-191">Avaliação desconhecida no operador **OR**:</span><span class="sxs-lookup"><span data-stu-id="08654-191">Unknown evaluation in **OR** operator:</span></span>  
  
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
  
### <a name="operator-binding-semantics"></a><span data-ttu-id="08654-192">Semântica de associação do operador</span><span class="sxs-lookup"><span data-stu-id="08654-192">Operator binding semantics</span></span>
  
-   <span data-ttu-id="08654-193">Operadores de comparação como `>`, `>=`, `<`, `<=`, `!=`, e `=` siga Olá mesmo promoções e conversões implícitas de tipo de semântica de operador Olá c# de associação de dados.</span><span class="sxs-lookup"><span data-stu-id="08654-193">Comparison operators such as `>`, `>=`, `<`, `<=`, `!=`, and `=` follow hello same semantics as hello C# operator binding in data type promotions and implicit conversions.</span></span>  
  
-   <span data-ttu-id="08654-194">Operadores aritméticos, como `+`, `-`, `*`, `/`, e `%` siga Olá mesmo promoções e conversões implícitas de tipo de semântica de operador Olá c# de associação de dados.</span><span class="sxs-lookup"><span data-stu-id="08654-194">Arithmetic operators such as `+`, `-`, `*`, `/`, and `%` follow hello same semantics as hello C# operator binding in data type promotions and implicit conversions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08654-195">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="08654-195">Next steps</span></span>

- [<span data-ttu-id="08654-196">Classe SQLFilter</span><span class="sxs-lookup"><span data-stu-id="08654-196">SQLFilter class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
- [<span data-ttu-id="08654-197">Classe SQLRuleAction</span><span class="sxs-lookup"><span data-stu-id="08654-197">SQLRuleAction class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)