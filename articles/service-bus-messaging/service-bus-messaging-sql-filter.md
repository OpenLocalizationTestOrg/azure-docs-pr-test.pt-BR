---
title: "Referência da sintaxe SQLFilter do Barramento de Serviços do Azure | Microsoft Docs"
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
ms.openlocfilehash: 3aaec8f9b6a3bbcf814f771405c3b589de6f7ae0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="sqlfilter-syntax"></a><span data-ttu-id="afbf7-103">Sintaxe SQLFilter</span><span class="sxs-lookup"><span data-stu-id="afbf7-103">SQLFilter syntax</span></span>

<span data-ttu-id="afbf7-104">Um *SqlFilter* é uma instância da [classe SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) e representa uma expressão de filtro baseada na linguagem SQL avaliada em uma [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="afbf7-104">A *SqlFilter* is an instance of the [SqlFilter class](/dotnet/api/microsoft.servicebus.messaging.sqlfilter), and represents a SQL language-based filter expression that is evaluated against a [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="afbf7-105">Um SqlFilter dá suporte a um subconjunto do padrão SQL-92.</span><span class="sxs-lookup"><span data-stu-id="afbf7-105">A SqlFilter supports a subset of the SQL-92 standard.</span></span>  
  
 <span data-ttu-id="afbf7-106">Este tópico lista detalhes sobre a gramática de SqlFilter.</span><span class="sxs-lookup"><span data-stu-id="afbf7-106">This topic lists details about SqlFilter grammar.</span></span>  
  
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
  
## <a name="arguments"></a><span data-ttu-id="afbf7-107">Argumentos</span><span class="sxs-lookup"><span data-stu-id="afbf7-107">Arguments</span></span>  
  
-   <span data-ttu-id="afbf7-108">`<scope>` é uma cadeia de caracteres opcional que indica o escopo do `<property_name>`.</span><span class="sxs-lookup"><span data-stu-id="afbf7-108">`<scope>` is an optional string indicating the scope of the `<property_name>`.</span></span> <span data-ttu-id="afbf7-109">Os valores válidos são `sys` ou `user`.</span><span class="sxs-lookup"><span data-stu-id="afbf7-109">Valid values are `sys` or `user`.</span></span> <span data-ttu-id="afbf7-110">O valor `sys` indica o escopo do sistema, em que `<property_name>` é um nome de propriedade pública da [classe BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="afbf7-110">The `sys` value indicates system scope where `<property_name>` is a public property name of the [BrokeredMessage class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="afbf7-111">`user` indica o escopo do usuário, em que `<property_name>` é uma chave de dicionário da [classe BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="afbf7-111">`user` indicates user scope where `<property_name>` is a key of the [BrokeredMessage class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dictionary.</span></span> <span data-ttu-id="afbf7-112">O escopo `user` será o escopo padrão se `<scope>` não for especificado.</span><span class="sxs-lookup"><span data-stu-id="afbf7-112">`user` scope is the default scope if `<scope>` is not specified.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="afbf7-113">Comentários</span><span class="sxs-lookup"><span data-stu-id="afbf7-113">Remarks</span></span>

<span data-ttu-id="afbf7-114">Uma tentativa de acessar uma propriedade inexistente do sistema é um erro, ao passo que uma tentativa de acessar uma propriedade de usuário inexistente não é um erro.</span><span class="sxs-lookup"><span data-stu-id="afbf7-114">An attempt to access a non-existent system property is an error, while an attempt to access a non-existent user property is not an error.</span></span> <span data-ttu-id="afbf7-115">Em vez disso, uma propriedade de usuário inexistente é internamente avaliada como um valor desconhecido.</span><span class="sxs-lookup"><span data-stu-id="afbf7-115">Instead, a non-existent user property is internally evaluated as an unknown value.</span></span> <span data-ttu-id="afbf7-116">Um valor desconhecido é tratado especialmente durante a avaliação de operador.</span><span class="sxs-lookup"><span data-stu-id="afbf7-116">An unknown value is treated specially during operator evaluation.</span></span>  
  
## <a name="propertyname"></a><span data-ttu-id="afbf7-117">property_name</span><span class="sxs-lookup"><span data-stu-id="afbf7-117">property_name</span></span>  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a><span data-ttu-id="afbf7-118">Argumentos</span><span class="sxs-lookup"><span data-stu-id="afbf7-118">Arguments</span></span>  

 <span data-ttu-id="afbf7-119">`<regular_identifier>` é uma cadeia de caracteres representada pela seguinte expressão regular:</span><span class="sxs-lookup"><span data-stu-id="afbf7-119">`<regular_identifier>` is a string represented by the following regular expression:</span></span>  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
<span data-ttu-id="afbf7-120">Essa gramática significa qualquer cadeia de caracteres que começa com uma letra e é seguida por um ou mais sublinhados/letras/dígitos.</span><span class="sxs-lookup"><span data-stu-id="afbf7-120">This grammar means any string that starts with a letter and is followed by one or more underscore/letter/digit.</span></span>  
  
<span data-ttu-id="afbf7-121">`[:IsLetter:]` significa qualquer caractere Unicode categorizado como uma letra do Unicode.</span><span class="sxs-lookup"><span data-stu-id="afbf7-121">`[:IsLetter:]` means any Unicode character that is categorized as a Unicode letter.</span></span> <span data-ttu-id="afbf7-122">`System.Char.IsLetter(c)` retorna `true` se `c` é uma letra do Unicode.</span><span class="sxs-lookup"><span data-stu-id="afbf7-122">`System.Char.IsLetter(c)` returns `true` if `c` is a Unicode letter.</span></span>  
  
<span data-ttu-id="afbf7-123">`[:IsDigit:]` significa qualquer caractere Unicode categorizado como um dígito decimal.</span><span class="sxs-lookup"><span data-stu-id="afbf7-123">`[:IsDigit:]` means any Unicode character that is categorized as a decimal digit.</span></span> <span data-ttu-id="afbf7-124">`System.Char.IsDigit(c)` retorna `true` se `c` é um dígito do Unicode.</span><span class="sxs-lookup"><span data-stu-id="afbf7-124">`System.Char.IsDigit(c)` returns `true` if `c` is a Unicode digit.</span></span>  
  
<span data-ttu-id="afbf7-125">Um `<regular_identifier>` não pode ser uma palavra-chave reservada.</span><span class="sxs-lookup"><span data-stu-id="afbf7-125">A `<regular_identifier>` cannot be a reserved keyword.</span></span>  
  
<span data-ttu-id="afbf7-126">`<delimited_identifier>` é qualquer cadeia de caracteres incluída em colchetes esquerdo/direito ([]).</span><span class="sxs-lookup"><span data-stu-id="afbf7-126">`<delimited_identifier>` is any string that is enclosed with left/right square brackets ([]).</span></span> <span data-ttu-id="afbf7-127">Um colchete direito é representado como dois colchetes direitos.</span><span class="sxs-lookup"><span data-stu-id="afbf7-127">A right square bracket is represented as two right square brackets.</span></span> <span data-ttu-id="afbf7-128">Estes são exemplos de `<delimited_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="afbf7-128">The following are examples of `<delimited_identifier>`:</span></span>  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
<span data-ttu-id="afbf7-129">`<quoted_identifier>` é qualquer cadeia de caracteres entre aspas duplas.</span><span class="sxs-lookup"><span data-stu-id="afbf7-129">`<quoted_identifier>` is any string that is enclosed with double quotation marks.</span></span> <span data-ttu-id="afbf7-130">Aspas duplas no identificador são representadas como duas aspas duplas.</span><span class="sxs-lookup"><span data-stu-id="afbf7-130">A double quotation mark in identifier is represented as two double quotation marks.</span></span> <span data-ttu-id="afbf7-131">Não é recomendável usar identificadores entre aspas, porque pode ser confundido facilmente por uma constante de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="afbf7-131">It is not recommended to use quoted identifiers because it can easily be confused with a string constant.</span></span> <span data-ttu-id="afbf7-132">Use um identificador delimitado, se possível.</span><span class="sxs-lookup"><span data-stu-id="afbf7-132">Use a delimited identifier if possible.</span></span> <span data-ttu-id="afbf7-133">Este é um exemplo de `<quoted_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="afbf7-133">The following is an example of `<quoted_identifier>`:</span></span>  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a><span data-ttu-id="afbf7-134">pattern</span><span class="sxs-lookup"><span data-stu-id="afbf7-134">pattern</span></span>  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="afbf7-135">Comentários</span><span class="sxs-lookup"><span data-stu-id="afbf7-135">Remarks</span></span>
  
<span data-ttu-id="afbf7-136">`<pattern>` deve ser uma expressão avaliada como uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="afbf7-136">`<pattern>` must be an expression that is evaluated as a string.</span></span> <span data-ttu-id="afbf7-137">Usado como um padrão para o operador LIKE.</span><span class="sxs-lookup"><span data-stu-id="afbf7-137">It is used as a pattern for the LIKE operator.</span></span>      <span data-ttu-id="afbf7-138">Pode conter os seguintes caracteres curinga:</span><span class="sxs-lookup"><span data-stu-id="afbf7-138">It can contain the following wildcard characters:</span></span>  
  
-   <span data-ttu-id="afbf7-139">`%`: qualquer cadeia de caracteres com zero ou mais caracteres.</span><span class="sxs-lookup"><span data-stu-id="afbf7-139">`%`:  Any string of zero or more characters.</span></span>  
  
-   <span data-ttu-id="afbf7-140">`_`: qualquer caractere único.</span><span class="sxs-lookup"><span data-stu-id="afbf7-140">`_`: Any single character.</span></span>  
  
## <a name="escapechar"></a><span data-ttu-id="afbf7-141">escape_char</span><span class="sxs-lookup"><span data-stu-id="afbf7-141">escape_char</span></span>  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="afbf7-142">Comentários</span><span class="sxs-lookup"><span data-stu-id="afbf7-142">Remarks</span></span>  

<span data-ttu-id="afbf7-143">`<escape_char>` deve ser uma expressão avaliada como uma cadeia de caracteres de comprimento 1.</span><span class="sxs-lookup"><span data-stu-id="afbf7-143">`<escape_char>` must be an expression that is evaluated as a string of length 1.</span></span> <span data-ttu-id="afbf7-144">Usado como um caractere de escape para o operador LIKE.</span><span class="sxs-lookup"><span data-stu-id="afbf7-144">It is used as an escape character for the LIKE operator.</span></span>  
  
 <span data-ttu-id="afbf7-145">Por exemplo, `property LIKE 'ABC\%' ESCAPE '\'` corresponde a `ABC%`, em vez de a uma cadeia de caracteres que começa com `ABC`.</span><span class="sxs-lookup"><span data-stu-id="afbf7-145">For example, `property LIKE 'ABC\%' ESCAPE '\'` matches `ABC%` rather than a string that starts with `ABC`.</span></span>  
  
## <a name="constant"></a><span data-ttu-id="afbf7-146">constante</span><span class="sxs-lookup"><span data-stu-id="afbf7-146">constant</span></span>  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a><span data-ttu-id="afbf7-147">Argumentos</span><span class="sxs-lookup"><span data-stu-id="afbf7-147">Arguments</span></span>  
  
-   <span data-ttu-id="afbf7-148">`<integer_constant>` é uma cadeia de números que não são incluídos em aspas e que não contêm pontos decimais.</span><span class="sxs-lookup"><span data-stu-id="afbf7-148">`<integer_constant>` is a string of numbers that are not enclosed in quotation marks and do not contain decimal points.</span></span> <span data-ttu-id="afbf7-149">Os valores são armazenados como `System.Int64` internamente e seguem o mesmo intervalo.</span><span class="sxs-lookup"><span data-stu-id="afbf7-149">The values are stored as `System.Int64` internally, and follow the same range.</span></span>  
  
     <span data-ttu-id="afbf7-150">Estes são exemplos de constantes longas:</span><span class="sxs-lookup"><span data-stu-id="afbf7-150">These are examples of long constants:</span></span>  
  
    ```  
    1894  
    2  
    ```  
  
-   <span data-ttu-id="afbf7-151">`<decimal_constant>` é uma cadeia de números que não são incluídos em aspas e que contêm um ponto decimal.</span><span class="sxs-lookup"><span data-stu-id="afbf7-151">`<decimal_constant>` is a string of numbers that are not enclosed in quotation marks, and contain a decimal point.</span></span> <span data-ttu-id="afbf7-152">Os valores são armazenados como `System.Double` internamente e seguem o mesmo intervalo e a mesma precisão.</span><span class="sxs-lookup"><span data-stu-id="afbf7-152">The values are stored as `System.Double` internally, and follow the same range/precision.</span></span>  
  
     <span data-ttu-id="afbf7-153">Em uma versão futura, esse número poderá ser armazenado em outro tipo de dados para dar suporte à semântica de número exato; portanto, você não deve se basear no fato de que o tipo de dados subjacente é `System.Double` para `<decimal_constant>`.</span><span class="sxs-lookup"><span data-stu-id="afbf7-153">In a future version, this number might be stored in a different data type to support exact number semantics, so you should not rely on the fact the underlying data type is `System.Double` for `<decimal_constant>`.</span></span>  
  
     <span data-ttu-id="afbf7-154">Estes são exemplos de constantes decimais:</span><span class="sxs-lookup"><span data-stu-id="afbf7-154">The following are examples of decimal constants:</span></span>  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   <span data-ttu-id="afbf7-155">`<approximate_number_constant>` é um número escrito em notação científica.</span><span class="sxs-lookup"><span data-stu-id="afbf7-155">`<approximate_number_constant>` is a number written in scientific notation.</span></span> <span data-ttu-id="afbf7-156">Os valores são armazenados como `System.Double` internamente e seguem o mesmo intervalo e a mesma precisão.</span><span class="sxs-lookup"><span data-stu-id="afbf7-156">The values are stored as `System.Double` internally, and follow the same range/precision.</span></span> <span data-ttu-id="afbf7-157">Estes são exemplos de constantes de número aproximado:</span><span class="sxs-lookup"><span data-stu-id="afbf7-157">The following are examples of approximate number constants:</span></span>  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a><span data-ttu-id="afbf7-158">boolean_constant</span><span class="sxs-lookup"><span data-stu-id="afbf7-158">boolean_constant</span></span>  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a><span data-ttu-id="afbf7-159">Comentários</span><span class="sxs-lookup"><span data-stu-id="afbf7-159">Remarks</span></span>  

<span data-ttu-id="afbf7-160">Constantes boolianas são representadas pelas palavras-chave **TRUE** ou **FALSE**.</span><span class="sxs-lookup"><span data-stu-id="afbf7-160">Boolean constants are represented by the keywords **TRUE** or **FALSE**.</span></span> <span data-ttu-id="afbf7-161">Os valores são armazenados como `System.Boolean`.</span><span class="sxs-lookup"><span data-stu-id="afbf7-161">The values are stored as `System.Boolean`.</span></span>  
  
## <a name="stringconstant"></a><span data-ttu-id="afbf7-162">string_constant</span><span class="sxs-lookup"><span data-stu-id="afbf7-162">string_constant</span></span>  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a><span data-ttu-id="afbf7-163">Comentários</span><span class="sxs-lookup"><span data-stu-id="afbf7-163">Remarks</span></span>  

<span data-ttu-id="afbf7-164">Constantes de cadeia de caracteres são incluídas em aspas simples e incluem caracteres Unicode válidos.</span><span class="sxs-lookup"><span data-stu-id="afbf7-164">String constants are enclosed in single quotation marks and include any valid Unicode characters.</span></span> <span data-ttu-id="afbf7-165">Uma aspa simples inserida em uma constante de cadeia de caracteres é representada como duas aspas simples.</span><span class="sxs-lookup"><span data-stu-id="afbf7-165">A single quotation mark embedded in a string constant is represented as two single quotation marks.</span></span>  
  
## <a name="function"></a><span data-ttu-id="afbf7-166">função</span><span class="sxs-lookup"><span data-stu-id="afbf7-166">function</span></span>  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a><span data-ttu-id="afbf7-167">Comentários</span><span class="sxs-lookup"><span data-stu-id="afbf7-167">Remarks</span></span>
  
<span data-ttu-id="afbf7-168">A função `newid()` retorna um **System.Guid** gerado pelo método `System.Guid.NewGuid()`.</span><span class="sxs-lookup"><span data-stu-id="afbf7-168">The `newid()` function returns a **System.Guid** generated by the `System.Guid.NewGuid()` method.</span></span>  
  
<span data-ttu-id="afbf7-169">A função `property(name)` retorna o valor da propriedade referenciada por `name`.</span><span class="sxs-lookup"><span data-stu-id="afbf7-169">The `property(name)` function returns the value of the property referenced by `name`.</span></span> <span data-ttu-id="afbf7-170">O valor `name` pode ser qualquer expressão válida que retorna um valor de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="afbf7-170">The `name` value can be any valid expression that returns a string value.</span></span>  
  
## <a name="considerations"></a><span data-ttu-id="afbf7-171">Considerações</span><span class="sxs-lookup"><span data-stu-id="afbf7-171">Considerations</span></span>
  
<span data-ttu-id="afbf7-172">Considere a seguinte semântica de [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter):</span><span class="sxs-lookup"><span data-stu-id="afbf7-172">Consider the following [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) semantics:</span></span>  
  
-   <span data-ttu-id="afbf7-173">Os nomes de propriedade não diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="afbf7-173">Property names are case-insensitive.</span></span>  
  
-   <span data-ttu-id="afbf7-174">Os operadores seguem a semântica de conversão implícita do C# sempre que possível.</span><span class="sxs-lookup"><span data-stu-id="afbf7-174">Operators follow C# implicit conversion semantics whenever possible.</span></span>  
  
-   <span data-ttu-id="afbf7-175">As propriedades do sistema são propriedades públicas expostas em instâncias de [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="afbf7-175">System properties are public properties exposed in [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) instances.</span></span>  
  
    <span data-ttu-id="afbf7-176">Considere a seguinte semântica de `IS [NOT] NULL`:</span><span class="sxs-lookup"><span data-stu-id="afbf7-176">Consider the following `IS [NOT] NULL` semantics:</span></span>  
  
    -   <span data-ttu-id="afbf7-177">`property IS NULL` é avaliado como `true` se a propriedade não existe ou se o valor da propriedade é `null`.</span><span class="sxs-lookup"><span data-stu-id="afbf7-177">`property IS NULL` is evaluated as `true` if either the property doesn't exist or the property's value is `null`.</span></span>  
  
### <a name="property-evaluation-semantics"></a><span data-ttu-id="afbf7-178">Semântica de avaliação da propriedade</span><span class="sxs-lookup"><span data-stu-id="afbf7-178">Property evaluation semantics</span></span>  
  
-   <span data-ttu-id="afbf7-179">Uma tentativa de avaliar uma propriedade do sistema inexistente gerará uma exceção [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception).</span><span class="sxs-lookup"><span data-stu-id="afbf7-179">An attempt to evaluate a non-existent system property throws a [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) exception.</span></span>  
  
-   <span data-ttu-id="afbf7-180">Uma propriedade que não existe internamente é avaliada como **desconhecida**.</span><span class="sxs-lookup"><span data-stu-id="afbf7-180">A property that does not exist is internally evaluated as **unknown**.</span></span>  
  
 <span data-ttu-id="afbf7-181">Avaliação desconhecida em operadores aritméticos:</span><span class="sxs-lookup"><span data-stu-id="afbf7-181">Unknown evaluation in arithmetic operators:</span></span>  
  
-   <span data-ttu-id="afbf7-182">Em operadores binários, se o lado esquerdo e/ou direito dos operandos for avaliado como **desconhecido**, o resultado será **desconhecido**.</span><span class="sxs-lookup"><span data-stu-id="afbf7-182">For binary operators, if either the left and/or right side of operands is evaluated as **unknown**, then the result is **unknown**.</span></span>  
  
-   <span data-ttu-id="afbf7-183">Em operadores unários, se um operando for avaliado como **desconhecido**, o resultado será **desconhecido**.</span><span class="sxs-lookup"><span data-stu-id="afbf7-183">For unary operators, if an operand is evaluated as **unknown**, then the result is **unknown**.</span></span>  
  
 <span data-ttu-id="afbf7-184">Avaliação desconhecida em operadores de comparação binária:</span><span class="sxs-lookup"><span data-stu-id="afbf7-184">Unknown evaluation in binary comparison operators:</span></span>  
  
-   <span data-ttu-id="afbf7-185">Se o lado esquerdo e/ou direito dos operandos for avaliado como **desconhecido**, o resultado será **desconhecido**.</span><span class="sxs-lookup"><span data-stu-id="afbf7-185">If either the left and/or right side of operands is evaluated as **unknown**, then the result is **unknown**.</span></span>  
  
 <span data-ttu-id="afbf7-186">Avaliação desconhecida em `[NOT] LIKE`:</span><span class="sxs-lookup"><span data-stu-id="afbf7-186">Unknown evaluation in `[NOT] LIKE`:</span></span>  
  
-   <span data-ttu-id="afbf7-187">Se um operando for avaliado como **desconhecido**, o resultado será **desconhecido**.</span><span class="sxs-lookup"><span data-stu-id="afbf7-187">If any operand is evaluated as **unknown**, then the result is **unknown**.</span></span>  
  
 <span data-ttu-id="afbf7-188">Avaliação desconhecida em `[NOT] IN`:</span><span class="sxs-lookup"><span data-stu-id="afbf7-188">Unknown evaluation in `[NOT] IN`:</span></span>  
  
-   <span data-ttu-id="afbf7-189">Se o operando esquerdo for avaliado como **desconhecido**, o resultado será **desconhecido**.</span><span class="sxs-lookup"><span data-stu-id="afbf7-189">If the left operand is evaluated as **unknown**, then the result is **unknown**.</span></span>  
  
 <span data-ttu-id="afbf7-190">Avaliação desconhecida no operador **AND**:</span><span class="sxs-lookup"><span data-stu-id="afbf7-190">Unknown evaluation in **AND** operator:</span></span>  
  
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
  
 <span data-ttu-id="afbf7-191">Avaliação desconhecida no operador **OR**:</span><span class="sxs-lookup"><span data-stu-id="afbf7-191">Unknown evaluation in **OR** operator:</span></span>  
  
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
  
### <a name="operator-binding-semantics"></a><span data-ttu-id="afbf7-192">Semântica de associação do operador</span><span class="sxs-lookup"><span data-stu-id="afbf7-192">Operator binding semantics</span></span>
  
-   <span data-ttu-id="afbf7-193">Operadores de comparação, como `>`, `>=`, `<`, `<=`, `!=` e `=` seguem a mesma semântica que a associação do operador do C# em promoções de tipo de dados e conversões implícitas.</span><span class="sxs-lookup"><span data-stu-id="afbf7-193">Comparison operators such as `>`, `>=`, `<`, `<=`, `!=`, and `=` follow the same semantics as the C# operator binding in data type promotions and implicit conversions.</span></span>  
  
-   <span data-ttu-id="afbf7-194">Operadores aritméticos, como `+`, `-`, `*`, `/` e `%` seguem a mesma semântica que a associação do operador do C# em promoções de tipo de dados e conversões implícitas.</span><span class="sxs-lookup"><span data-stu-id="afbf7-194">Arithmetic operators such as `+`, `-`, `*`, `/`, and `%` follow the same semantics as the C# operator binding in data type promotions and implicit conversions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="afbf7-195">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="afbf7-195">Next steps</span></span>

- [<span data-ttu-id="afbf7-196">Classe SQLFilter</span><span class="sxs-lookup"><span data-stu-id="afbf7-196">SQLFilter class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
- [<span data-ttu-id="afbf7-197">Classe SQLRuleAction</span><span class="sxs-lookup"><span data-stu-id="afbf7-197">SQLRuleAction class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)