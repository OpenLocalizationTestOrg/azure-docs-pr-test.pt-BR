---
title: "as funções definidas pelo usuário aaaAzure Stream Analytics JavaScript | Microsoft Docs"
description: "Executar o mecanismo de consulta avançada com funções definidas pelo usuário do JavaScript"
keywords: "javascript, funções definidas pelo usuário, udf"
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 28eeb8f6437c23989e8887687b950361fed4414c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-javascript-user-defined-functions"></a><span data-ttu-id="04485-104">Funções definidas pelo usuário do JavaScript do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="04485-104">Azure Stream Analytics JavaScript user-defined functions</span></span>
<span data-ttu-id="04485-105">O Stream Analytics do Azure dá suporte a funções definidas pelo usuário gravadas em JavaScript.</span><span class="sxs-lookup"><span data-stu-id="04485-105">Azure Stream Analytics supports user-defined functions written in JavaScript.</span></span> <span data-ttu-id="04485-106">Com um conjunto avançado de saudação do **cadeia de caracteres**, **RegExp**, **matemática**, **matriz**, e **data** métodos que Transformações de dados complexos com trabalhos do Stream Analytics fornece JavaScript, se tornam mais fácil toocreate.</span><span class="sxs-lookup"><span data-stu-id="04485-106">With hello rich set of **String**, **RegExp**, **Math**, **Array**, and **Date** methods that JavaScript provides, complex data transformations with Stream Analytics jobs become easier toocreate.</span></span>

## <a name="javascript-user-defined-functions"></a><span data-ttu-id="04485-107">Funções definidas pelo usuário de JavaScript</span><span class="sxs-lookup"><span data-stu-id="04485-107">JavaScript user-defined functions</span></span>
<span data-ttu-id="04485-108">As funções definidas pelo usuário de JavaScript dão suporte a funções escalares sem monitoração de estado somente para computação que não requerem conectividade externa.</span><span class="sxs-lookup"><span data-stu-id="04485-108">JavaScript user-defined functions support stateless, compute-only scalar functions that do not require external connectivity.</span></span> <span data-ttu-id="04485-109">Olá retornar o valor de uma função só pode ser um valor escalar (único).</span><span class="sxs-lookup"><span data-stu-id="04485-109">hello return value of a function can only be a scalar (single) value.</span></span> <span data-ttu-id="04485-110">Depois de adicionar um trabalho de tooa de função definida pelo usuário de JavaScript, você pode usar função hello em qualquer lugar na consulta hello, como uma função escalar interna.</span><span class="sxs-lookup"><span data-stu-id="04485-110">After you add a JavaScript user-defined function tooa job, you can use hello function anywhere in hello query, like a built-in scalar function.</span></span>

<span data-ttu-id="04485-111">Aqui estão alguns cenários nos quais as funções definidas pelo usuário JavaScript podem ser úteis:</span><span class="sxs-lookup"><span data-stu-id="04485-111">Here are some scenarios where you might find JavaScript user-defined functions useful:</span></span>
* <span data-ttu-id="04485-112">Análise e manipulação de cadeia de caracteres com funções de expressão regular, por exemplo, **Regexp_Replace()** e **Regexp_Extract()**</span><span class="sxs-lookup"><span data-stu-id="04485-112">Parsing and manipulating strings that have regular expression functions, for example, **Regexp_Replace()** and **Regexp_Extract()**</span></span>
* <span data-ttu-id="04485-113">Decodificação e codificação de dados, por exemplo, conversão de binário em hexadecimal</span><span class="sxs-lookup"><span data-stu-id="04485-113">Decoding and encoding data, for example, binary-to-hex conversion</span></span>
* <span data-ttu-id="04485-114">Executando cálculos matemáticos com funções **Matemáticas** do JavaScript</span><span class="sxs-lookup"><span data-stu-id="04485-114">Performing mathematic computations with JavaScript **Math** functions</span></span>
* <span data-ttu-id="04485-115">Executando operações de matriz como classificar, juntar, localizar e preencher</span><span class="sxs-lookup"><span data-stu-id="04485-115">Performing array operations like sort, join, find, and fill</span></span>

<span data-ttu-id="04485-116">Aqui estão ações que não podem ser realizadas com uma função definida pelo usuário do JavaScript no Stream Analytics:</span><span class="sxs-lookup"><span data-stu-id="04485-116">Here are some things that you cannot do with a JavaScript user-defined function in Stream Analytics:</span></span>
* <span data-ttu-id="04485-117">Chamar pontos de extremidade REST externos, por exemplo, executando pesquisa inversa de IP ou extração de dados de referência de uma fonte externa</span><span class="sxs-lookup"><span data-stu-id="04485-117">Call out external REST endpoints, for example, performing reverse IP lookup or pulling reference data from an external source</span></span>
* <span data-ttu-id="04485-118">Executar serialização ou desserialização de formato de evento personalizado em entradas/saídas</span><span class="sxs-lookup"><span data-stu-id="04485-118">Perform custom event format serialization or deserialization on inputs/outputs</span></span>
* <span data-ttu-id="04485-119">Criar agregações personalizadas</span><span class="sxs-lookup"><span data-stu-id="04485-119">Create custom aggregates</span></span>

<span data-ttu-id="04485-120">Embora funções como **Date.GetDate()** ou **Math** não são bloqueadas na definição de funções hello, evite usá-los.</span><span class="sxs-lookup"><span data-stu-id="04485-120">Although functions like **Date.GetDate()** or **Math.random()** are not blocked in hello functions definition, you should avoid using them.</span></span> <span data-ttu-id="04485-121">Essas funções **não** retorno Olá mesmo resultado sempre que você chamá-las e Olá serviço Azure Stream Analytics não manter um diário de chamadas de função e retornou resultados.</span><span class="sxs-lookup"><span data-stu-id="04485-121">These functions **do not** return hello same result every time you call them, and hello Azure Stream Analytics service does not keep a journal of function invocations and returned results.</span></span> <span data-ttu-id="04485-122">Se uma função retorna resultados diferentes em Olá mesmos eventos, capacidade de repetição não é garantida quando um trabalho for reiniciado por você ou pelo serviço de análise de fluxo de saudação.</span><span class="sxs-lookup"><span data-stu-id="04485-122">If a function returns different result on hello same events, repeatability is not guaranteed when a job is restarted by you or by hello Stream Analytics service.</span></span>

## <a name="add-a-javascript-user-defined-function-in-hello-azure-portal"></a><span data-ttu-id="04485-123">Adicionar uma função definida pelo usuário do JavaScript no hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="04485-123">Add a JavaScript user-defined function in hello Azure portal</span></span>
<span data-ttu-id="04485-124">toocreate uma função JavaScript simples de definida pelo usuário, em um trabalho de análise de fluxo existente, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="04485-124">toocreate a simple JavaScript user-defined function under an existing Stream Analytics job, do these steps:</span></span>

1.  <span data-ttu-id="04485-125">Em Olá portal do Azure, localize o trabalho do Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="04485-125">In hello Azure portal, find your Stream Analytics job.</span></span>
2.  <span data-ttu-id="04485-126">Em **TOPOLOGIA DO TRABALHO**, selecione sua função.</span><span class="sxs-lookup"><span data-stu-id="04485-126">Under **JOB TOPOLOGY**, select your function.</span></span> <span data-ttu-id="04485-127">Uma lista vazia de funções é exibida.</span><span class="sxs-lookup"><span data-stu-id="04485-127">An empty list of functions appears.</span></span>
3.  <span data-ttu-id="04485-128">toocreate uma nova função definida pelo usuário, selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="04485-128">toocreate a new user-defined function, select **Add**.</span></span>
4.  <span data-ttu-id="04485-129">Em Olá **nova função** folha, para **tipo de função**, selecione **JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="04485-129">On hello **New Function** blade, for **Function Type**, select **JavaScript**.</span></span> <span data-ttu-id="04485-130">Um modelo de função padrão aparece no editor de saudação.</span><span class="sxs-lookup"><span data-stu-id="04485-130">A default function template appears in hello editor.</span></span>
5.  <span data-ttu-id="04485-131">Para Olá **alias UDF**, digite **hex2Int**e alterar a implementação da função hello da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="04485-131">For hello **UDF alias**, enter **hex2Int**, and change hello function implementation as follows:</span></span>

    ```
    // Convert Hex value toointeger.
    function main(hexValue) {
        return parseInt(hexValue, 16);
    }
    ```

6.  <span data-ttu-id="04485-132">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="04485-132">Select **Save**.</span></span> <span data-ttu-id="04485-133">A função aparece na lista de saudação de funções.</span><span class="sxs-lookup"><span data-stu-id="04485-133">Your function appears in hello list of functions.</span></span>
7.  <span data-ttu-id="04485-134">Selecione Olá novo **hex2Int** de função e verifique a definição da função hello.</span><span class="sxs-lookup"><span data-stu-id="04485-134">Select hello new **hex2Int** function, and check hello function definition.</span></span> <span data-ttu-id="04485-135">Todas as funções têm um **UDF** alias de função do prefixo toohello adicionado.</span><span class="sxs-lookup"><span data-stu-id="04485-135">All functions have a **UDF** prefix added toohello function alias.</span></span> <span data-ttu-id="04485-136">É necessário muito*incluir Olá prefixo* quando você chama a função hello em sua consulta de análise de fluxo.</span><span class="sxs-lookup"><span data-stu-id="04485-136">You need too*include hello prefix* when you call hello function in your Stream Analytics query.</span></span> <span data-ttu-id="04485-137">Nesse caso, você chama **UDF.hex2Int**.</span><span class="sxs-lookup"><span data-stu-id="04485-137">In this case, you call **UDF.hex2Int**.</span></span>

## <a name="call-a-javascript-user-defined-function-in-a-query"></a><span data-ttu-id="04485-138">Chamar uma função definida pelo usuário do JavaScript em uma consulta</span><span class="sxs-lookup"><span data-stu-id="04485-138">Call a JavaScript user-defined function in a query</span></span>

1. <span data-ttu-id="04485-139">Em Olá editor de consultas, em **trabalho topologia**, selecione **consulta**.</span><span class="sxs-lookup"><span data-stu-id="04485-139">In hello query editor, under **JOB TOPOLOGY**, select **Query**.</span></span>
2.  <span data-ttu-id="04485-140">Editar a consulta e, em seguida, chamar hello-função definida pelo usuário, como este:</span><span class="sxs-lookup"><span data-stu-id="04485-140">Edit your query, and then call hello user-defined function, like this:</span></span>

    ```
    SELECT
        time,
        UDF.hex2Int(offset) AS IntOffset
    INTO
        output
    FROM
        InputStream
    ```

3.  <span data-ttu-id="04485-141">arquivo de dados de exemplo tooupload hello, com o botão direito Olá trabalho entrada.</span><span class="sxs-lookup"><span data-stu-id="04485-141">tooupload hello sample data file, right-click hello job input.</span></span>
4.  <span data-ttu-id="04485-142">tootest sua consulta, selecione **teste**.</span><span class="sxs-lookup"><span data-stu-id="04485-142">tootest your query, select **Test**.</span></span>


## <a name="supported-javascript-objects"></a><span data-ttu-id="04485-143">Objetos JavaScript com suporte</span><span class="sxs-lookup"><span data-stu-id="04485-143">Supported JavaScript objects</span></span>
<span data-ttu-id="04485-144">As funções definidas pelo usuário do JavaScript do Stream Analytics do Azure dão suporte a objetos JavaScript internos e padrão.</span><span class="sxs-lookup"><span data-stu-id="04485-144">Azure Stream Analytics JavaScript user-defined functions support standard, built-in JavaScript objects.</span></span> <span data-ttu-id="04485-145">Para obter uma lista desses objetos, consulte [Objetos Globais](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects).</span><span class="sxs-lookup"><span data-stu-id="04485-145">For a list of these objects, see [Global Objects](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects).</span></span>

### <a name="stream-analytics-and-javascript-type-conversion"></a><span data-ttu-id="04485-146">Conversão de tipo do Stream Analytics e JavaScript</span><span class="sxs-lookup"><span data-stu-id="04485-146">Stream Analytics and JavaScript type conversion</span></span>

<span data-ttu-id="04485-147">Há diferenças nos tipos de saudação que dão suporte a linguagem de consulta do Stream Analytics hello e JavaScript.</span><span class="sxs-lookup"><span data-stu-id="04485-147">There are differences in hello types that hello Stream Analytics query language and JavaScript support.</span></span> <span data-ttu-id="04485-148">Esta tabela lista os mapeamentos de conversão de saudação entre hello dois:</span><span class="sxs-lookup"><span data-stu-id="04485-148">This table lists hello conversion mappings between hello two:</span></span>

<span data-ttu-id="04485-149">Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="04485-149">Stream Analytics</span></span> | <span data-ttu-id="04485-150">JavaScript</span><span class="sxs-lookup"><span data-stu-id="04485-150">JavaScript</span></span>
--- | ---
<span data-ttu-id="04485-151">bigint</span><span class="sxs-lookup"><span data-stu-id="04485-151">bigint</span></span> | <span data-ttu-id="04485-152">Número (JavaScript apenas pode representar inteiros de tooprecisely 2 ^ 53)</span><span class="sxs-lookup"><span data-stu-id="04485-152">Number (JavaScript can only represent integers up tooprecisely 2^53)</span></span>
<span data-ttu-id="04485-153">Datetime</span><span class="sxs-lookup"><span data-stu-id="04485-153">DateTime</span></span> | <span data-ttu-id="04485-154">Data (o JavaScript dá suporte somente a milissegundos)</span><span class="sxs-lookup"><span data-stu-id="04485-154">Date (JavaScript only supports milliseconds)</span></span>
<span data-ttu-id="04485-155">double</span><span class="sxs-lookup"><span data-stu-id="04485-155">double</span></span> | <span data-ttu-id="04485-156">Número</span><span class="sxs-lookup"><span data-stu-id="04485-156">Number</span></span>
<span data-ttu-id="04485-157">nvarchar(MAX)</span><span class="sxs-lookup"><span data-stu-id="04485-157">nvarchar(MAX)</span></span> | <span data-ttu-id="04485-158">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="04485-158">String</span></span>
<span data-ttu-id="04485-159">Registro</span><span class="sxs-lookup"><span data-stu-id="04485-159">Record</span></span> | <span data-ttu-id="04485-160">Objeto</span><span class="sxs-lookup"><span data-stu-id="04485-160">Object</span></span>
<span data-ttu-id="04485-161">Matriz</span><span class="sxs-lookup"><span data-stu-id="04485-161">Array</span></span> | <span data-ttu-id="04485-162">Matriz</span><span class="sxs-lookup"><span data-stu-id="04485-162">Array</span></span>
<span data-ttu-id="04485-163">NULO</span><span class="sxs-lookup"><span data-stu-id="04485-163">NULL</span></span> | <span data-ttu-id="04485-164">Nulo</span><span class="sxs-lookup"><span data-stu-id="04485-164">Null</span></span>


<span data-ttu-id="04485-165">Aqui estão as conversões de JavaScript para Stream Analytics:</span><span class="sxs-lookup"><span data-stu-id="04485-165">Here are JavaScript-to-Stream Analytics conversions:</span></span>


<span data-ttu-id="04485-166">JavaScript</span><span class="sxs-lookup"><span data-stu-id="04485-166">JavaScript</span></span> | <span data-ttu-id="04485-167">Análise de fluxo</span><span class="sxs-lookup"><span data-stu-id="04485-167">Stream Analytics</span></span>
--- | ---
<span data-ttu-id="04485-168">Número</span><span class="sxs-lookup"><span data-stu-id="04485-168">Number</span></span> | <span data-ttu-id="04485-169">Bigint (se o número de saudação é round e entre longa. MinValue e long. MaxValue; Caso contrário, é double)</span><span class="sxs-lookup"><span data-stu-id="04485-169">Bigint (if hello number is round and between long.MinValue and long.MaxValue; otherwise, it's double)</span></span>
<span data-ttu-id="04485-170">Data</span><span class="sxs-lookup"><span data-stu-id="04485-170">Date</span></span> | <span data-ttu-id="04485-171">DateTime</span><span class="sxs-lookup"><span data-stu-id="04485-171">DateTime</span></span>
<span data-ttu-id="04485-172">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="04485-172">String</span></span> | <span data-ttu-id="04485-173">nvarchar(MAX)</span><span class="sxs-lookup"><span data-stu-id="04485-173">nvarchar(MAX)</span></span>
<span data-ttu-id="04485-174">Objeto</span><span class="sxs-lookup"><span data-stu-id="04485-174">Object</span></span> | <span data-ttu-id="04485-175">Registro</span><span class="sxs-lookup"><span data-stu-id="04485-175">Record</span></span>
<span data-ttu-id="04485-176">Matriz</span><span class="sxs-lookup"><span data-stu-id="04485-176">Array</span></span> | <span data-ttu-id="04485-177">Matriz</span><span class="sxs-lookup"><span data-stu-id="04485-177">Array</span></span>
<span data-ttu-id="04485-178">Null, Undefined</span><span class="sxs-lookup"><span data-stu-id="04485-178">Null, Undefined</span></span> | <span data-ttu-id="04485-179">NULO</span><span class="sxs-lookup"><span data-stu-id="04485-179">NULL</span></span>
<span data-ttu-id="04485-180">Qualquer outro tipo (por exemplo, uma função ou um erro)</span><span class="sxs-lookup"><span data-stu-id="04485-180">Any other type (for example, a function or error)</span></span> | <span data-ttu-id="04485-181">Sem suporte (resulta em erro de tempo de execução)</span><span class="sxs-lookup"><span data-stu-id="04485-181">Not supported (results in runtime error)</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="04485-182">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="04485-182">Troubleshooting</span></span>
<span data-ttu-id="04485-183">Erros de tempo de execução do JavaScript são considerados fatais e são apresentados por meio do log de atividades de saudação.</span><span class="sxs-lookup"><span data-stu-id="04485-183">JavaScript runtime errors are considered fatal, and are surfaced through hello Activity log.</span></span> <span data-ttu-id="04485-184">tooretrieve Olá login, Olá portal do Azure, vá tooyour trabalho e selecione **log de atividades**.</span><span class="sxs-lookup"><span data-stu-id="04485-184">tooretrieve hello log, in hello Azure portal, go tooyour job and select **Activity log**.</span></span>


## <a name="other-javascript-user-defined-function-patterns"></a><span data-ttu-id="04485-185">Outros padrões de função definida pelo usuário do JavaScript</span><span class="sxs-lookup"><span data-stu-id="04485-185">Other JavaScript user-defined function patterns</span></span>

### <a name="write-nested-json-toooutput"></a><span data-ttu-id="04485-186">Gravar toooutput aninhada de JSON</span><span class="sxs-lookup"><span data-stu-id="04485-186">Write nested JSON toooutput</span></span>
<span data-ttu-id="04485-187">Se você tiver uma etapa de processamento de acompanhamento que usa um trabalho de análise de fluxo de saída como entrada, e requer um formato JSON, você pode escrever um toooutput de cadeia de caracteres JSON.</span><span class="sxs-lookup"><span data-stu-id="04485-187">If you have a follow-up processing step that uses a Stream Analytics job output as input, and it requires a JSON format, you can write a JSON string toooutput.</span></span> <span data-ttu-id="04485-188">Olá próximo exemplo chama Olá **JSON.stringify()** toopack todos os pares de nome/valor de saudação de entrada e, em seguida, gravação-los como um valor de cadeia de caracteres único na saída de função.</span><span class="sxs-lookup"><span data-stu-id="04485-188">hello next example calls hello **JSON.stringify()** function toopack all name/value pairs of hello input, and then write them as a single string value in output.</span></span>

<span data-ttu-id="04485-189">**Definição de funções definidas pelo usuário de JavaScript:**</span><span class="sxs-lookup"><span data-stu-id="04485-189">**JavaScript user-defined function definition:**</span></span>

```
function main(x) {
return JSON.stringify(x);
}
```

<span data-ttu-id="04485-190">**Consulta de exemplo:**</span><span class="sxs-lookup"><span data-stu-id="04485-190">**Sample query:**</span></span>
```
SELECT
    DataString,
    DataValue,
    HexValue,
    UDF.json_stringify(input) As InputEvent
INTO
    output
FROM
    input PARTITION BY PARTITIONID
```

## <a name="get-help"></a><span data-ttu-id="04485-191">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="04485-191">Get help</span></span>
<span data-ttu-id="04485-192">Para obter ajuda adicional, experimente nosso [Fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="04485-192">For additional help, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="04485-193">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="04485-193">Next steps</span></span>
* [<span data-ttu-id="04485-194">Introdução tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="04485-194">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="04485-195">Introdução ao uso do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="04485-195">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="04485-196">Dimensionar trabalhos do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="04485-196">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="04485-197">Referência de linguagem de consulta do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="04485-197">Azure Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="04485-198">Referência da API REST do gerenciamento do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="04485-198">Azure Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
