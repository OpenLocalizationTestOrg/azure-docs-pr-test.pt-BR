---
title: "exemplos de aaaQuery para padrões de uso comuns no Stream Analytics | Microsoft Docs"
description: "Padrões de consulta comuns do Azure Stream Analytics"
keywords: exemplos de consulta
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jenniehubbard
editor: cgronlun
ms.assetid: 6b9a7d00-fbcc-42f6-9cbb-8bbf0bbd3d0e
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/08/2017
ms.author: jenniehubbard
ms.openlocfilehash: c8f7a8ac661eaf0281f4140b02c42141b73040fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="query-examples-for-common-stream-analytics-usage-patterns"></a><span data-ttu-id="85248-104">Exemplos de consulta para padrões de uso do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="85248-104">Query examples for common Stream Analytics usage patterns</span></span>
## <a name="introduction"></a><span data-ttu-id="85248-105">Introdução</span><span class="sxs-lookup"><span data-stu-id="85248-105">Introduction</span></span>
<span data-ttu-id="85248-106">As consultas no Azure Stream Analytics são expressas em uma linguagem de consulta parecida com o SQL.</span><span class="sxs-lookup"><span data-stu-id="85248-106">Queries in Azure Stream Analytics are expressed in a SQL-like query language.</span></span> <span data-ttu-id="85248-107">Essas consultas estão documentadas em Olá [referência de linguagem de consulta do Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx) guia.</span><span class="sxs-lookup"><span data-stu-id="85248-107">These queries are documented in hello [Stream Analytics query language reference](https://msdn.microsoft.com/library/azure/dn834998.aspx) guide.</span></span> <span data-ttu-id="85248-108">Este artigo descreve soluções tooseveral padrões comuns de consulta, com base em cenários do mundo real.</span><span class="sxs-lookup"><span data-stu-id="85248-108">This article outlines solutions tooseveral common query patterns, based on real-world scenarios.</span></span> <span data-ttu-id="85248-109">É um trabalho em andamento e continua toobe atualizado com novos padrões de forma contínua.</span><span class="sxs-lookup"><span data-stu-id="85248-109">It is a work in progress and continues toobe updated with new patterns on an ongoing basis.</span></span>

## <a name="query-example-convert-data-types"></a><span data-ttu-id="85248-110">Exemplo de consulta: converter tipos de dados</span><span class="sxs-lookup"><span data-stu-id="85248-110">Query example: Convert data types</span></span>
<span data-ttu-id="85248-111">**Descrição**: definir tipos de saudação de propriedades no fluxo de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="85248-111">**Description**: Define hello types of properties on hello input stream.</span></span>
<span data-ttu-id="85248-112">Por exemplo, Olá carro são as novidades no fluxo de entrada hello como cadeias de caracteres e o peso precisa toobe convertido muito**INT** tooperform **soma** -o.</span><span class="sxs-lookup"><span data-stu-id="85248-112">For example, hello car weight is coming on hello input stream as strings and needs toobe converted too**INT** tooperform **SUM** it up.</span></span>

<span data-ttu-id="85248-113">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="85248-113">**Input**:</span></span>

| <span data-ttu-id="85248-114">Faça</span><span class="sxs-lookup"><span data-stu-id="85248-114">Make</span></span> | <span data-ttu-id="85248-115">Hora</span><span class="sxs-lookup"><span data-stu-id="85248-115">Time</span></span> | <span data-ttu-id="85248-116">Peso</span><span class="sxs-lookup"><span data-stu-id="85248-116">Weight</span></span> |
| --- | --- | --- |
| <span data-ttu-id="85248-117">Honda</span><span class="sxs-lookup"><span data-stu-id="85248-117">Honda</span></span> |<span data-ttu-id="85248-118">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-118">2015-01-01T00:00:01.0000000Z</span></span> |<span data-ttu-id="85248-119">"1000"</span><span class="sxs-lookup"><span data-stu-id="85248-119">"1000"</span></span> |
| <span data-ttu-id="85248-120">Honda</span><span class="sxs-lookup"><span data-stu-id="85248-120">Honda</span></span> |<span data-ttu-id="85248-121">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-121">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="85248-122">"2000"</span><span class="sxs-lookup"><span data-stu-id="85248-122">"2000"</span></span> |

<span data-ttu-id="85248-123">**Saída**:</span><span class="sxs-lookup"><span data-stu-id="85248-123">**Output**:</span></span>

| <span data-ttu-id="85248-124">Faça</span><span class="sxs-lookup"><span data-stu-id="85248-124">Make</span></span> | <span data-ttu-id="85248-125">Peso</span><span class="sxs-lookup"><span data-stu-id="85248-125">Weight</span></span> |
| --- | --- |
| <span data-ttu-id="85248-126">Honda</span><span class="sxs-lookup"><span data-stu-id="85248-126">Honda</span></span> |<span data-ttu-id="85248-127">3000</span><span class="sxs-lookup"><span data-stu-id="85248-127">3000</span></span> |

<span data-ttu-id="85248-128">**Solução**:</span><span class="sxs-lookup"><span data-stu-id="85248-128">**Solution**:</span></span>

    SELECT
        Make,
        SUM(CAST(Weight AS BIGINT)) AS Weight
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

<span data-ttu-id="85248-129">**Explicação**: Use um **CAST** instrução Olá **peso** campo toospecify seu tipo de dados.</span><span class="sxs-lookup"><span data-stu-id="85248-129">**Explanation**: Use a **CAST** statement in hello **Weight** field toospecify its data type.</span></span> <span data-ttu-id="85248-130">Consulte lista de saudação de tipos de dados com suporte no [tipos de dados (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835065.aspx).</span><span class="sxs-lookup"><span data-stu-id="85248-130">See hello list of supported data types in [Data types (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835065.aspx).</span></span>

## <a name="query-example-use-likenot-like-toodo-pattern-matching"></a><span data-ttu-id="85248-131">Exemplo de consulta: Use Like ou não como correspondência de padrão de toodo</span><span class="sxs-lookup"><span data-stu-id="85248-131">Query example: Use Like/Not like toodo pattern matching</span></span>
<span data-ttu-id="85248-132">**Descrição**: Verifique se o valor de um campo em eventos de saudação corresponde a um determinado padrão.</span><span class="sxs-lookup"><span data-stu-id="85248-132">**Description**: Check that a field value on hello event matches a certain pattern.</span></span>
<span data-ttu-id="85248-133">Por exemplo, verificar o resultado Olá retorna placas que começam com A e terminar com 9.</span><span class="sxs-lookup"><span data-stu-id="85248-133">For example, check that hello result returns license plates that start with A and end with 9.</span></span>

<span data-ttu-id="85248-134">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="85248-134">**Input**:</span></span>

| <span data-ttu-id="85248-135">Faça</span><span class="sxs-lookup"><span data-stu-id="85248-135">Make</span></span> | <span data-ttu-id="85248-136">PlacaDeCarro</span><span class="sxs-lookup"><span data-stu-id="85248-136">LicensePlate</span></span> | <span data-ttu-id="85248-137">Hora</span><span class="sxs-lookup"><span data-stu-id="85248-137">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="85248-138">Honda</span><span class="sxs-lookup"><span data-stu-id="85248-138">Honda</span></span> |<span data-ttu-id="85248-139">ABC-123</span><span class="sxs-lookup"><span data-stu-id="85248-139">ABC-123</span></span> |<span data-ttu-id="85248-140">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-140">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="85248-141">Toyota</span><span class="sxs-lookup"><span data-stu-id="85248-141">Toyota</span></span> |<span data-ttu-id="85248-142">AAA-999</span><span class="sxs-lookup"><span data-stu-id="85248-142">AAA-999</span></span> |<span data-ttu-id="85248-143">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-143">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="85248-144">Nissan</span><span class="sxs-lookup"><span data-stu-id="85248-144">Nissan</span></span> |<span data-ttu-id="85248-145">ABC-369</span><span class="sxs-lookup"><span data-stu-id="85248-145">ABC-369</span></span> |<span data-ttu-id="85248-146">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-146">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="85248-147">**Saída**:</span><span class="sxs-lookup"><span data-stu-id="85248-147">**Output**:</span></span>

| <span data-ttu-id="85248-148">Faça</span><span class="sxs-lookup"><span data-stu-id="85248-148">Make</span></span> | <span data-ttu-id="85248-149">PlacaDeCarro</span><span class="sxs-lookup"><span data-stu-id="85248-149">LicensePlate</span></span> | <span data-ttu-id="85248-150">Hora</span><span class="sxs-lookup"><span data-stu-id="85248-150">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="85248-151">Toyota</span><span class="sxs-lookup"><span data-stu-id="85248-151">Toyota</span></span> |<span data-ttu-id="85248-152">AAA-999</span><span class="sxs-lookup"><span data-stu-id="85248-152">AAA-999</span></span> |<span data-ttu-id="85248-153">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-153">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="85248-154">Nissan</span><span class="sxs-lookup"><span data-stu-id="85248-154">Nissan</span></span> |<span data-ttu-id="85248-155">ABC-369</span><span class="sxs-lookup"><span data-stu-id="85248-155">ABC-369</span></span> |<span data-ttu-id="85248-156">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-156">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="85248-157">**Solução**:</span><span class="sxs-lookup"><span data-stu-id="85248-157">**Solution**:</span></span>

    SELECT
        *
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LicensePlate LIKE 'A%9'

<span data-ttu-id="85248-158">**Explicação**: Olá Use **como** saudação do instrução toocheck **LicensePlate** valor do campo.</span><span class="sxs-lookup"><span data-stu-id="85248-158">**Explanation**: Use hello **LIKE** statement toocheck hello **LicensePlate** field value.</span></span> <span data-ttu-id="85248-159">Ele deve começar com um A, ter uma cadeia de caracteres com nenhum ou mais caracteres, e terminar com 9.</span><span class="sxs-lookup"><span data-stu-id="85248-159">It should start with an A, then have any string of zero or more characters, and then end with a 9.</span></span> 

## <a name="query-example-specify-logic-for-different-casesvalues-case-statements"></a><span data-ttu-id="85248-160">Exemplo de consulta: especifique a lógica para casos/valores diferentes (instruções CASE)</span><span class="sxs-lookup"><span data-stu-id="85248-160">Query example: Specify logic for different cases/values (CASE statements)</span></span>
<span data-ttu-id="85248-161">**Descrição**: forneça um cálculo diferente para um campo com base em um critério específico.</span><span class="sxs-lookup"><span data-stu-id="85248-161">**Description**: Provide a different computation for a field, based on a particular criterion.</span></span>
<span data-ttu-id="85248-162">Por exemplo, forneça uma descrição de cadeia de caracteres para quantos carros de saudação mesmo fazer passado, com um caso especial para 1.</span><span class="sxs-lookup"><span data-stu-id="85248-162">For example, provide a string description for how many cars of hello same make passed, with a special case for 1.</span></span>

<span data-ttu-id="85248-163">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="85248-163">**Input**:</span></span>

| <span data-ttu-id="85248-164">Faça</span><span class="sxs-lookup"><span data-stu-id="85248-164">Make</span></span> | <span data-ttu-id="85248-165">Hora</span><span class="sxs-lookup"><span data-stu-id="85248-165">Time</span></span> |
| --- | --- |
| <span data-ttu-id="85248-166">Honda</span><span class="sxs-lookup"><span data-stu-id="85248-166">Honda</span></span> |<span data-ttu-id="85248-167">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-167">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="85248-168">Toyota</span><span class="sxs-lookup"><span data-stu-id="85248-168">Toyota</span></span> |<span data-ttu-id="85248-169">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-169">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="85248-170">Toyota</span><span class="sxs-lookup"><span data-stu-id="85248-170">Toyota</span></span> |<span data-ttu-id="85248-171">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-171">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="85248-172">**Saída**:</span><span class="sxs-lookup"><span data-stu-id="85248-172">**Output**:</span></span>

| <span data-ttu-id="85248-173">CarrosPassaram</span><span class="sxs-lookup"><span data-stu-id="85248-173">CarsPassed</span></span> | <span data-ttu-id="85248-174">Hora</span><span class="sxs-lookup"><span data-stu-id="85248-174">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="85248-175">1 Honda</span><span class="sxs-lookup"><span data-stu-id="85248-175">1 Honda</span></span> |<span data-ttu-id="85248-176">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-176">2015-01-01T00:00:10.0000000Z</span></span> |
| <span data-ttu-id="85248-177">2 Toyotas</span><span class="sxs-lookup"><span data-stu-id="85248-177">2 Toyotas</span></span> |<span data-ttu-id="85248-178">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-178">2015-01-01T00:00:10.0000000Z</span></span> |

<span data-ttu-id="85248-179">**Solução**:</span><span class="sxs-lookup"><span data-stu-id="85248-179">**Solution**:</span></span>

    SELECT
        CASE
            WHEN COUNT(*) = 1 THEN CONCAT('1 ', Make)
            ELSE CONCAT(CAST(COUNT(*) AS NVARCHAR(MAX)), ' ', Make, 's')
        END AS CarsPassed,
        System.TimeStamp AS Time
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

<span data-ttu-id="85248-180">**Explicação**: Olá **caso** cláusula nos permite tooprovide uma computação diferente, com base em alguns critérios (no nosso caso, a contagem de saudação de carros Olá na janela de agregação de saudação).</span><span class="sxs-lookup"><span data-stu-id="85248-180">**Explanation**: hello **CASE** clause allows us tooprovide a different computation, based on some criteria (in our case, hello count of hello cars in hello aggregate window).</span></span>

## <a name="query-example-send-data-toomultiple-outputs"></a><span data-ttu-id="85248-181">Exemplo de consulta: enviar dados toomultiple saídas</span><span class="sxs-lookup"><span data-stu-id="85248-181">Query example: Send data toomultiple outputs</span></span>
<span data-ttu-id="85248-182">**Descrição**: enviar dados toomultiple destinos de um único trabalho de saída.</span><span class="sxs-lookup"><span data-stu-id="85248-182">**Description**: Send data toomultiple output targets from a single job.</span></span>
<span data-ttu-id="85248-183">Por exemplo, analisar os dados de um alerta de limite e armazenamento de tooblob todos os eventos de arquivos.</span><span class="sxs-lookup"><span data-stu-id="85248-183">For example, analyze data for a threshold-based alert and archive all events tooblob storage.</span></span>

<span data-ttu-id="85248-184">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="85248-184">**Input**:</span></span>

| <span data-ttu-id="85248-185">Faça</span><span class="sxs-lookup"><span data-stu-id="85248-185">Make</span></span> | <span data-ttu-id="85248-186">Hora</span><span class="sxs-lookup"><span data-stu-id="85248-186">Time</span></span> |
| --- | --- |
| <span data-ttu-id="85248-187">Honda</span><span class="sxs-lookup"><span data-stu-id="85248-187">Honda</span></span> |<span data-ttu-id="85248-188">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-188">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="85248-189">Honda</span><span class="sxs-lookup"><span data-stu-id="85248-189">Honda</span></span> |<span data-ttu-id="85248-190">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-190">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="85248-191">Toyota</span><span class="sxs-lookup"><span data-stu-id="85248-191">Toyota</span></span> |<span data-ttu-id="85248-192">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-192">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="85248-193">Toyota</span><span class="sxs-lookup"><span data-stu-id="85248-193">Toyota</span></span> |<span data-ttu-id="85248-194">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-194">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="85248-195">Toyota</span><span class="sxs-lookup"><span data-stu-id="85248-195">Toyota</span></span> |<span data-ttu-id="85248-196">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-196">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="85248-197">**Saída1**:</span><span class="sxs-lookup"><span data-stu-id="85248-197">**Output1**:</span></span>

| <span data-ttu-id="85248-198">Faça</span><span class="sxs-lookup"><span data-stu-id="85248-198">Make</span></span> | <span data-ttu-id="85248-199">Hora</span><span class="sxs-lookup"><span data-stu-id="85248-199">Time</span></span> |
| --- | --- |
| <span data-ttu-id="85248-200">Honda</span><span class="sxs-lookup"><span data-stu-id="85248-200">Honda</span></span> |<span data-ttu-id="85248-201">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-201">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="85248-202">Honda</span><span class="sxs-lookup"><span data-stu-id="85248-202">Honda</span></span> |<span data-ttu-id="85248-203">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-203">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="85248-204">Toyota</span><span class="sxs-lookup"><span data-stu-id="85248-204">Toyota</span></span> |<span data-ttu-id="85248-205">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-205">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="85248-206">Toyota</span><span class="sxs-lookup"><span data-stu-id="85248-206">Toyota</span></span> |<span data-ttu-id="85248-207">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-207">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="85248-208">Toyota</span><span class="sxs-lookup"><span data-stu-id="85248-208">Toyota</span></span> |<span data-ttu-id="85248-209">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-209">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="85248-210">**Saída2**:</span><span class="sxs-lookup"><span data-stu-id="85248-210">**Output2**:</span></span>

| <span data-ttu-id="85248-211">Faça</span><span class="sxs-lookup"><span data-stu-id="85248-211">Make</span></span> | <span data-ttu-id="85248-212">Hora</span><span class="sxs-lookup"><span data-stu-id="85248-212">Time</span></span> | <span data-ttu-id="85248-213">Contagem</span><span class="sxs-lookup"><span data-stu-id="85248-213">Count</span></span> |
| --- | --- | --- |
| <span data-ttu-id="85248-214">Toyota</span><span class="sxs-lookup"><span data-stu-id="85248-214">Toyota</span></span> |<span data-ttu-id="85248-215">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-215">2015-01-01T00:00:10.0000000Z</span></span> |<span data-ttu-id="85248-216">3</span><span class="sxs-lookup"><span data-stu-id="85248-216">3</span></span> |

<span data-ttu-id="85248-217">**Solução**:</span><span class="sxs-lookup"><span data-stu-id="85248-217">**Solution**:</span></span>

    SELECT
        *
    INTO
        ArchiveOutput
    FROM
        Input TIMESTAMP BY Time

    SELECT
        Make,
        System.TimeStamp AS Time,
        COUNT(*) AS [Count]
    INTO
        AlertOutput
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)
    HAVING
        [Count] >= 3

<span data-ttu-id="85248-218">**Explicação**: Olá **INTO** cláusula informa Stream Analytics que hello gera toowrite Olá dados toofrom essa instrução.</span><span class="sxs-lookup"><span data-stu-id="85248-218">**Explanation**: hello **INTO** clause tells Stream Analytics which of hello outputs toowrite hello data toofrom this statement.</span></span>
<span data-ttu-id="85248-219">Olá primeira consulta é uma passagem de dados Olá recebemos saída tooan que chamamos **ArchiveOutput**.</span><span class="sxs-lookup"><span data-stu-id="85248-219">hello first query is a pass-through of hello data we received tooan output that we named **ArchiveOutput**.</span></span>
<span data-ttu-id="85248-220">consulta de segundo de saudação faz algumas agregação simple e filtragem e envia os resultados de saudação tooa sistema downstream de alertas.</span><span class="sxs-lookup"><span data-stu-id="85248-220">hello second query does some simple aggregation and filtering, and it sends hello results tooa downstream alerting system.</span></span>

<span data-ttu-id="85248-221">Observe que você também pode reutilizar os resultados de saudação de expressões de tabela comuns Olá (CTEs) (como **WITH** instruções) em várias declarações de saída.</span><span class="sxs-lookup"><span data-stu-id="85248-221">Note that you can also reuse hello results of hello common table expressions (CTEs) (such as **WITH** statements) in multiple output statements.</span></span> <span data-ttu-id="85248-222">Essa opção tem Olá benefício adicional de abertura menos fonte de entrada toohello leitores.</span><span class="sxs-lookup"><span data-stu-id="85248-222">This option has hello added benefit of opening fewer readers toohello input source.</span></span>
<span data-ttu-id="85248-223">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="85248-223">For example:</span></span> 

    WITH AllRedCars AS (
        SELECT
            *
        FROM
            Input TIMESTAMP BY Time
        WHERE
            Color = 'red'
    )
    SELECT * INTO HondaOutput FROM AllRedCars WHERE Make = 'Honda'
    SELECT * INTO ToyotaOutput FROM AllRedCars WHERE Make = 'Toyota'

## <a name="query-example-count-unique-values"></a><span data-ttu-id="85248-224">Exemplo de consulta: contar valores exclusivos</span><span class="sxs-lookup"><span data-stu-id="85248-224">Query example: Count unique values</span></span>
<span data-ttu-id="85248-225">**Descrição**: contar Olá número exclusivo de valores de campo que aparecem no fluxo hello dentro de uma janela de tempo.</span><span class="sxs-lookup"><span data-stu-id="85248-225">**Description**: Count hello number of unique field values that appear in hello stream within a time window.</span></span>
<span data-ttu-id="85248-226">Por exemplo, quantas exclusivas faz de carros passados pelo pedágio Olá em uma janela de 2 segundos?</span><span class="sxs-lookup"><span data-stu-id="85248-226">For example, how many unique makes of cars passed through hello toll booth in a 2-second window?</span></span>

<span data-ttu-id="85248-227">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="85248-227">**Input**:</span></span>

| <span data-ttu-id="85248-228">Faça</span><span class="sxs-lookup"><span data-stu-id="85248-228">Make</span></span> | <span data-ttu-id="85248-229">Hora</span><span class="sxs-lookup"><span data-stu-id="85248-229">Time</span></span> |
| --- | --- |
| <span data-ttu-id="85248-230">Honda</span><span class="sxs-lookup"><span data-stu-id="85248-230">Honda</span></span> |<span data-ttu-id="85248-231">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-231">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="85248-232">Honda</span><span class="sxs-lookup"><span data-stu-id="85248-232">Honda</span></span> |<span data-ttu-id="85248-233">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-233">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="85248-234">Toyota</span><span class="sxs-lookup"><span data-stu-id="85248-234">Toyota</span></span> |<span data-ttu-id="85248-235">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-235">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="85248-236">Toyota</span><span class="sxs-lookup"><span data-stu-id="85248-236">Toyota</span></span> |<span data-ttu-id="85248-237">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-237">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="85248-238">Toyota</span><span class="sxs-lookup"><span data-stu-id="85248-238">Toyota</span></span> |<span data-ttu-id="85248-239">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-239">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="85248-240">**Saída:**</span><span class="sxs-lookup"><span data-stu-id="85248-240">**Output:**</span></span>

| <span data-ttu-id="85248-241">Contagem</span><span class="sxs-lookup"><span data-stu-id="85248-241">Count</span></span> | <span data-ttu-id="85248-242">Hora</span><span class="sxs-lookup"><span data-stu-id="85248-242">Time</span></span> |
| --- | --- |
| <span data-ttu-id="85248-243">2</span><span class="sxs-lookup"><span data-stu-id="85248-243">2</span></span> |<span data-ttu-id="85248-244">2015-01-01T00:00:02.000Z</span><span class="sxs-lookup"><span data-stu-id="85248-244">2015-01-01T00:00:02.000Z</span></span> |
| <span data-ttu-id="85248-245">1</span><span class="sxs-lookup"><span data-stu-id="85248-245">1</span></span> |<span data-ttu-id="85248-246">2015-01-01T00:00:04.000Z</span><span class="sxs-lookup"><span data-stu-id="85248-246">2015-01-01T00:00:04.000Z</span></span> |

<span data-ttu-id="85248-247">**Solução:**</span><span class="sxs-lookup"><span data-stu-id="85248-247">**Solution:**</span></span>

````
SELECT
     COUNT(DISTINCT Make) AS CountMake,
     System.TIMESTAMP AS TIME
FROM Input TIMESTAMP BY TIME
GROUP BY 
     TumblingWindow(second, 2)
````


<span data-ttu-id="85248-248">**Explicação:**
**COUNT (DISTINCT Verifique)** retorna Olá número de valores distintos em Olá **fazer** coluna dentro de uma janela de tempo.</span><span class="sxs-lookup"><span data-stu-id="85248-248">**Explanation:**
**COUNT(DISTINCT Make)** returns hello number of distinct values in hello **Make** column within a time window.</span></span>

## <a name="query-example-determine-if-a-value-has-changed"></a><span data-ttu-id="85248-249">Exemplo de consulta: determinar se um valor foi alterado</span><span class="sxs-lookup"><span data-stu-id="85248-249">Query example: Determine if a value has changed</span></span>
<span data-ttu-id="85248-250">**Descrição**: examinar um toodetermine valor anterior, se for diferente do valor atual de saudação.</span><span class="sxs-lookup"><span data-stu-id="85248-250">**Description**: Look at a previous value toodetermine if it is different than hello current value.</span></span>
<span data-ttu-id="85248-251">Por exemplo, está carro anterior Olá Olá Olá de estrada pedágio que mesmo fazer como car atual Olá?</span><span class="sxs-lookup"><span data-stu-id="85248-251">For example, is hello previous car on hello toll road hello same make as hello current car?</span></span>

<span data-ttu-id="85248-252">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="85248-252">**Input**:</span></span>

| <span data-ttu-id="85248-253">Faça</span><span class="sxs-lookup"><span data-stu-id="85248-253">Make</span></span> | <span data-ttu-id="85248-254">Hora</span><span class="sxs-lookup"><span data-stu-id="85248-254">Time</span></span> |
| --- | --- |
| <span data-ttu-id="85248-255">Honda</span><span class="sxs-lookup"><span data-stu-id="85248-255">Honda</span></span> |<span data-ttu-id="85248-256">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-256">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="85248-257">Toyota</span><span class="sxs-lookup"><span data-stu-id="85248-257">Toyota</span></span> |<span data-ttu-id="85248-258">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-258">2015-01-01T00:00:02.0000000Z</span></span> |

<span data-ttu-id="85248-259">**Saída**:</span><span class="sxs-lookup"><span data-stu-id="85248-259">**Output**:</span></span>

| <span data-ttu-id="85248-260">Faça</span><span class="sxs-lookup"><span data-stu-id="85248-260">Make</span></span> | <span data-ttu-id="85248-261">Hora</span><span class="sxs-lookup"><span data-stu-id="85248-261">Time</span></span> |
| --- | --- |
| <span data-ttu-id="85248-262">Toyota</span><span class="sxs-lookup"><span data-stu-id="85248-262">Toyota</span></span> |<span data-ttu-id="85248-263">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-263">2015-01-01T00:00:02.0000000Z</span></span> |

<span data-ttu-id="85248-264">**Solução**:</span><span class="sxs-lookup"><span data-stu-id="85248-264">**Solution**:</span></span>

    SELECT
        Make,
        Time
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(minute, 1)) <> Make

<span data-ttu-id="85248-265">**Explicação**: Use **LATÊNCIA** toopeek em Olá fluxo volta um evento de entrada e obter Olá **fazer** valor.</span><span class="sxs-lookup"><span data-stu-id="85248-265">**Explanation**: Use **LAG** toopeek into hello input stream one event back and get hello **Make** value.</span></span> <span data-ttu-id="85248-266">Em seguida, comparar toohello **fazer** valor em Olá atual e saída saudação do evento, se eles forem diferentes.</span><span class="sxs-lookup"><span data-stu-id="85248-266">Then compare it toohello **Make** value on hello current event and output hello event if they are different.</span></span>

## <a name="query-example-find-hello-first-event-in-a-window"></a><span data-ttu-id="85248-267">Exemplo de consulta: localizar Olá primeiro evento em uma janela</span><span class="sxs-lookup"><span data-stu-id="85248-267">Query example: Find hello first event in a window</span></span>
<span data-ttu-id="85248-268">**Descrição**: localizar Olá primeiro carro em cada intervalo de 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="85248-268">**Description**: Find hello first car in every 10-minute interval.</span></span>

<span data-ttu-id="85248-269">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="85248-269">**Input**:</span></span>

| <span data-ttu-id="85248-270">PlacaDeCarro</span><span class="sxs-lookup"><span data-stu-id="85248-270">LicensePlate</span></span> | <span data-ttu-id="85248-271">Faça</span><span class="sxs-lookup"><span data-stu-id="85248-271">Make</span></span> | <span data-ttu-id="85248-272">Hora</span><span class="sxs-lookup"><span data-stu-id="85248-272">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="85248-273">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="85248-273">DXE 5291</span></span> |<span data-ttu-id="85248-274">Honda</span><span class="sxs-lookup"><span data-stu-id="85248-274">Honda</span></span> |<span data-ttu-id="85248-275">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-275">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="85248-276">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="85248-276">YZK 5704</span></span> |<span data-ttu-id="85248-277">Ford</span><span class="sxs-lookup"><span data-stu-id="85248-277">Ford</span></span> |<span data-ttu-id="85248-278">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-278">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="85248-279">RMV 8282</span><span class="sxs-lookup"><span data-stu-id="85248-279">RMV 8282</span></span> |<span data-ttu-id="85248-280">Honda</span><span class="sxs-lookup"><span data-stu-id="85248-280">Honda</span></span> |<span data-ttu-id="85248-281">2015-07-27T00:05:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-281">2015-07-27T00:05:01.0000000Z</span></span> |
| <span data-ttu-id="85248-282">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="85248-282">YHN 6970</span></span> |<span data-ttu-id="85248-283">Toyota</span><span class="sxs-lookup"><span data-stu-id="85248-283">Toyota</span></span> |<span data-ttu-id="85248-284">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-284">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="85248-285">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="85248-285">VFE 1616</span></span> |<span data-ttu-id="85248-286">Toyota</span><span class="sxs-lookup"><span data-stu-id="85248-286">Toyota</span></span> |<span data-ttu-id="85248-287">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-287">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="85248-288">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="85248-288">QYF 9358</span></span> |<span data-ttu-id="85248-289">Honda</span><span class="sxs-lookup"><span data-stu-id="85248-289">Honda</span></span> |<span data-ttu-id="85248-290">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-290">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="85248-291">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="85248-291">MDR 6128</span></span> |<span data-ttu-id="85248-292">BMW</span><span class="sxs-lookup"><span data-stu-id="85248-292">BMW</span></span> |<span data-ttu-id="85248-293">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-293">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="85248-294">**Saída**:</span><span class="sxs-lookup"><span data-stu-id="85248-294">**Output**:</span></span>

| <span data-ttu-id="85248-295">PlacaDeCarro</span><span class="sxs-lookup"><span data-stu-id="85248-295">LicensePlate</span></span> | <span data-ttu-id="85248-296">Faça</span><span class="sxs-lookup"><span data-stu-id="85248-296">Make</span></span> | <span data-ttu-id="85248-297">Hora</span><span class="sxs-lookup"><span data-stu-id="85248-297">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="85248-298">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="85248-298">DXE 5291</span></span> |<span data-ttu-id="85248-299">Honda</span><span class="sxs-lookup"><span data-stu-id="85248-299">Honda</span></span> |<span data-ttu-id="85248-300">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-300">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="85248-301">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="85248-301">QYF 9358</span></span> |<span data-ttu-id="85248-302">Honda</span><span class="sxs-lookup"><span data-stu-id="85248-302">Honda</span></span> |<span data-ttu-id="85248-303">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-303">2015-07-27T00:12:02.0000000Z</span></span> |

<span data-ttu-id="85248-304">**Solução**:</span><span class="sxs-lookup"><span data-stu-id="85248-304">**Solution**:</span></span>

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) = 1

<span data-ttu-id="85248-305">Agora vamos alterar Olá problema e localizar Olá primeiro carro de um determinado fazer em cada intervalo de 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="85248-305">Now let’s change hello problem and find hello first car of a particular make in every 10-minute interval.</span></span>

| <span data-ttu-id="85248-306">PlacaDeCarro</span><span class="sxs-lookup"><span data-stu-id="85248-306">LicensePlate</span></span> | <span data-ttu-id="85248-307">Faça</span><span class="sxs-lookup"><span data-stu-id="85248-307">Make</span></span> | <span data-ttu-id="85248-308">Hora</span><span class="sxs-lookup"><span data-stu-id="85248-308">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="85248-309">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="85248-309">DXE 5291</span></span> |<span data-ttu-id="85248-310">Honda</span><span class="sxs-lookup"><span data-stu-id="85248-310">Honda</span></span> |<span data-ttu-id="85248-311">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-311">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="85248-312">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="85248-312">YZK 5704</span></span> |<span data-ttu-id="85248-313">Ford</span><span class="sxs-lookup"><span data-stu-id="85248-313">Ford</span></span> |<span data-ttu-id="85248-314">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-314">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="85248-315">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="85248-315">YHN 6970</span></span> |<span data-ttu-id="85248-316">Toyota</span><span class="sxs-lookup"><span data-stu-id="85248-316">Toyota</span></span> |<span data-ttu-id="85248-317">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-317">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="85248-318">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="85248-318">QYF 9358</span></span> |<span data-ttu-id="85248-319">Honda</span><span class="sxs-lookup"><span data-stu-id="85248-319">Honda</span></span> |<span data-ttu-id="85248-320">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-320">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="85248-321">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="85248-321">MDR 6128</span></span> |<span data-ttu-id="85248-322">BMW</span><span class="sxs-lookup"><span data-stu-id="85248-322">BMW</span></span> |<span data-ttu-id="85248-323">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-323">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="85248-324">**Solução**:</span><span class="sxs-lookup"><span data-stu-id="85248-324">**Solution**:</span></span>

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) OVER (PARTITION BY Make) = 1

## <a name="query-example-find-hello-last-event-in-a-window"></a><span data-ttu-id="85248-325">Exemplo de consulta: localizar Olá último evento em uma janela</span><span class="sxs-lookup"><span data-stu-id="85248-325">Query example: Find hello last event in a window</span></span>
<span data-ttu-id="85248-326">**Descrição**: carro de última encontrar hello em cada intervalo de 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="85248-326">**Description**: Find hello last car in every 10-minute interval.</span></span>

<span data-ttu-id="85248-327">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="85248-327">**Input**:</span></span>

| <span data-ttu-id="85248-328">PlacaDeCarro</span><span class="sxs-lookup"><span data-stu-id="85248-328">LicensePlate</span></span> | <span data-ttu-id="85248-329">Faça</span><span class="sxs-lookup"><span data-stu-id="85248-329">Make</span></span> | <span data-ttu-id="85248-330">Hora</span><span class="sxs-lookup"><span data-stu-id="85248-330">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="85248-331">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="85248-331">DXE 5291</span></span> |<span data-ttu-id="85248-332">Honda</span><span class="sxs-lookup"><span data-stu-id="85248-332">Honda</span></span> |<span data-ttu-id="85248-333">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-333">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="85248-334">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="85248-334">YZK 5704</span></span> |<span data-ttu-id="85248-335">Ford</span><span class="sxs-lookup"><span data-stu-id="85248-335">Ford</span></span> |<span data-ttu-id="85248-336">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-336">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="85248-337">RMV 8282</span><span class="sxs-lookup"><span data-stu-id="85248-337">RMV 8282</span></span> |<span data-ttu-id="85248-338">Honda</span><span class="sxs-lookup"><span data-stu-id="85248-338">Honda</span></span> |<span data-ttu-id="85248-339">2015-07-27T00:05:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-339">2015-07-27T00:05:01.0000000Z</span></span> |
| <span data-ttu-id="85248-340">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="85248-340">YHN 6970</span></span> |<span data-ttu-id="85248-341">Toyota</span><span class="sxs-lookup"><span data-stu-id="85248-341">Toyota</span></span> |<span data-ttu-id="85248-342">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-342">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="85248-343">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="85248-343">VFE 1616</span></span> |<span data-ttu-id="85248-344">Toyota</span><span class="sxs-lookup"><span data-stu-id="85248-344">Toyota</span></span> |<span data-ttu-id="85248-345">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-345">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="85248-346">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="85248-346">QYF 9358</span></span> |<span data-ttu-id="85248-347">Honda</span><span class="sxs-lookup"><span data-stu-id="85248-347">Honda</span></span> |<span data-ttu-id="85248-348">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-348">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="85248-349">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="85248-349">MDR 6128</span></span> |<span data-ttu-id="85248-350">BMW</span><span class="sxs-lookup"><span data-stu-id="85248-350">BMW</span></span> |<span data-ttu-id="85248-351">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-351">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="85248-352">**Saída**:</span><span class="sxs-lookup"><span data-stu-id="85248-352">**Output**:</span></span>

| <span data-ttu-id="85248-353">PlacaDeCarro</span><span class="sxs-lookup"><span data-stu-id="85248-353">LicensePlate</span></span> | <span data-ttu-id="85248-354">Faça</span><span class="sxs-lookup"><span data-stu-id="85248-354">Make</span></span> | <span data-ttu-id="85248-355">Hora</span><span class="sxs-lookup"><span data-stu-id="85248-355">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="85248-356">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="85248-356">VFE 1616</span></span> |<span data-ttu-id="85248-357">Toyota</span><span class="sxs-lookup"><span data-stu-id="85248-357">Toyota</span></span> |<span data-ttu-id="85248-358">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-358">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="85248-359">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="85248-359">MDR 6128</span></span> |<span data-ttu-id="85248-360">BMW</span><span class="sxs-lookup"><span data-stu-id="85248-360">BMW</span></span> |<span data-ttu-id="85248-361">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-361">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="85248-362">**Solução**:</span><span class="sxs-lookup"><span data-stu-id="85248-362">**Solution**:</span></span>

    WITH LastInWindow AS
    (
        SELECT 
            MAX(Time) AS LastEventTime
        FROM 
            Input TIMESTAMP BY Time
        GROUP BY 
            TumblingWindow(minute, 10)
    )
    SELECT 
        Input.LicensePlate,
        Input.Make,
        Input.Time
    FROM
        Input TIMESTAMP BY Time 
        INNER JOIN LastInWindow
        ON DATEDIFF(minute, Input, LastInWindow) BETWEEN 0 AND 10
        AND Input.Time = LastInWindow.LastEventTime

<span data-ttu-id="85248-363">**Explicação**: há duas etapas na consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="85248-363">**Explanation**: There are two steps in hello query.</span></span> <span data-ttu-id="85248-364">Olá primeiro localiza uma saudação mais recente carimbo de hora no windows 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="85248-364">hello first one finds hello latest time stamp in 10-minute windows.</span></span> <span data-ttu-id="85248-365">junções de etapa segundo Olá Olá resultados de consulta de primeira Olá Olá original fluxo toofind Olá eventos que correspondem a última carimbos de hora Olá em cada janela.</span><span class="sxs-lookup"><span data-stu-id="85248-365">hello second step joins hello results of hello first query with hello original stream toofind hello events that match hello last time stamps in each window.</span></span> 

## <a name="query-example-detect-hello-absence-of-events"></a><span data-ttu-id="85248-366">Exemplo de consulta: detectarem Olá ausência de eventos</span><span class="sxs-lookup"><span data-stu-id="85248-366">Query example: Detect hello absence of events</span></span>
<span data-ttu-id="85248-367">**Descrição**: confirme se um fluxo não tem um valor correspondente a determinado critério.</span><span class="sxs-lookup"><span data-stu-id="85248-367">**Description**: Check that a stream has no value that matches a certain criterion.</span></span>
<span data-ttu-id="85248-368">Por exemplo, 2 carros consecutivos de saudação que mesmo fazer inseriu road de pedágio hello dentro Olá últimos 90 segundos?</span><span class="sxs-lookup"><span data-stu-id="85248-368">For example, have 2 consecutive cars from hello same make entered hello toll road within hello last 90 seconds?</span></span>

<span data-ttu-id="85248-369">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="85248-369">**Input**:</span></span>

| <span data-ttu-id="85248-370">Faça</span><span class="sxs-lookup"><span data-stu-id="85248-370">Make</span></span> | <span data-ttu-id="85248-371">PlacaDeCarro</span><span class="sxs-lookup"><span data-stu-id="85248-371">LicensePlate</span></span> | <span data-ttu-id="85248-372">Hora</span><span class="sxs-lookup"><span data-stu-id="85248-372">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="85248-373">Honda</span><span class="sxs-lookup"><span data-stu-id="85248-373">Honda</span></span> |<span data-ttu-id="85248-374">ABC-123</span><span class="sxs-lookup"><span data-stu-id="85248-374">ABC-123</span></span> |<span data-ttu-id="85248-375">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-375">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="85248-376">Honda</span><span class="sxs-lookup"><span data-stu-id="85248-376">Honda</span></span> |<span data-ttu-id="85248-377">AAA-999</span><span class="sxs-lookup"><span data-stu-id="85248-377">AAA-999</span></span> |<span data-ttu-id="85248-378">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-378">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="85248-379">Toyota</span><span class="sxs-lookup"><span data-stu-id="85248-379">Toyota</span></span> |<span data-ttu-id="85248-380">DEF-987</span><span class="sxs-lookup"><span data-stu-id="85248-380">DEF-987</span></span> |<span data-ttu-id="85248-381">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-381">2015-01-01T00:00:03.0000000Z</span></span> |
| <span data-ttu-id="85248-382">Honda</span><span class="sxs-lookup"><span data-stu-id="85248-382">Honda</span></span> |<span data-ttu-id="85248-383">GHI-345</span><span class="sxs-lookup"><span data-stu-id="85248-383">GHI-345</span></span> |<span data-ttu-id="85248-384">2015-01-01T00:00:04.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-384">2015-01-01T00:00:04.0000000Z</span></span> |

<span data-ttu-id="85248-385">**Saída**:</span><span class="sxs-lookup"><span data-stu-id="85248-385">**Output**:</span></span>

| <span data-ttu-id="85248-386">Faça</span><span class="sxs-lookup"><span data-stu-id="85248-386">Make</span></span> | <span data-ttu-id="85248-387">Hora</span><span class="sxs-lookup"><span data-stu-id="85248-387">Time</span></span> | <span data-ttu-id="85248-388">PlacaDoCarroAtual</span><span class="sxs-lookup"><span data-stu-id="85248-388">CurrentCarLicensePlate</span></span> | <span data-ttu-id="85248-389">PlacaDoPrimeiroCarro</span><span class="sxs-lookup"><span data-stu-id="85248-389">FirstCarLicensePlate</span></span> | <span data-ttu-id="85248-390">HoraDoPrimeiroCarro</span><span class="sxs-lookup"><span data-stu-id="85248-390">FirstCarTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="85248-391">Honda</span><span class="sxs-lookup"><span data-stu-id="85248-391">Honda</span></span> |<span data-ttu-id="85248-392">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-392">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="85248-393">AAA-999</span><span class="sxs-lookup"><span data-stu-id="85248-393">AAA-999</span></span> |<span data-ttu-id="85248-394">ABC-123</span><span class="sxs-lookup"><span data-stu-id="85248-394">ABC-123</span></span> |<span data-ttu-id="85248-395">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-395">2015-01-01T00:00:01.0000000Z</span></span> |

<span data-ttu-id="85248-396">**Solução**:</span><span class="sxs-lookup"><span data-stu-id="85248-396">**Solution**:</span></span>

    SELECT
        Make,
        Time,
        LicensePlate AS CurrentCarLicensePlate,
        LAG(LicensePlate, 1) OVER (LIMIT DURATION(second, 90)) AS FirstCarLicensePlate,
        LAG(Time, 1) OVER (LIMIT DURATION(second, 90)) AS FirstCarTime
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(second, 90)) = Make

<span data-ttu-id="85248-397">**Explicação**: Use **LATÊNCIA** toopeek em Olá fluxo volta um evento de entrada e obter Olá **fazer** valor.</span><span class="sxs-lookup"><span data-stu-id="85248-397">**Explanation**: Use **LAG** toopeek into hello input stream one event back and get hello **Make** value.</span></span> <span data-ttu-id="85248-398">Compare-toohello **fazer** valor no evento atual hello e eventos de saudação de saída se eles são Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="85248-398">Compare it toohello **MAKE** value in hello current event, and then output hello event if they are hello same.</span></span> <span data-ttu-id="85248-399">Você também pode usar **LATÊNCIA** tooget dados sobre o carro anterior hello.</span><span class="sxs-lookup"><span data-stu-id="85248-399">You can also use **LAG** tooget data about hello previous car.</span></span>

## <a name="query-example-detect-hello-duration-between-events"></a><span data-ttu-id="85248-400">Exemplo de consulta: detectar duração Olá entre eventos</span><span class="sxs-lookup"><span data-stu-id="85248-400">Query example: Detect hello duration between events</span></span>
<span data-ttu-id="85248-401">**Descrição**: localizar duração de saudação de um determinado evento.</span><span class="sxs-lookup"><span data-stu-id="85248-401">**Description**: Find hello duration of a given event.</span></span> <span data-ttu-id="85248-402">Por exemplo, dada uma sequência de cliques da web, determine gasto em um recurso de tempo de saudação.</span><span class="sxs-lookup"><span data-stu-id="85248-402">For example, given a web clickstream, determine hello time spent on a feature.</span></span>

<span data-ttu-id="85248-403">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="85248-403">**Input**:</span></span>  

| <span data-ttu-id="85248-404">Usuário</span><span class="sxs-lookup"><span data-stu-id="85248-404">User</span></span> | <span data-ttu-id="85248-405">Recurso</span><span class="sxs-lookup"><span data-stu-id="85248-405">Feature</span></span> | <span data-ttu-id="85248-406">Evento</span><span class="sxs-lookup"><span data-stu-id="85248-406">Event</span></span> | <span data-ttu-id="85248-407">Hora</span><span class="sxs-lookup"><span data-stu-id="85248-407">Time</span></span> |
| --- | --- | --- | --- |
| user@location.com |<span data-ttu-id="85248-408">RightMenu</span><span class="sxs-lookup"><span data-stu-id="85248-408">RightMenu</span></span> |<span data-ttu-id="85248-409">Iniciar</span><span class="sxs-lookup"><span data-stu-id="85248-409">Start</span></span> |<span data-ttu-id="85248-410">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-410">2015-01-01T00:00:01.0000000Z</span></span> |
| user@location.com |<span data-ttu-id="85248-411">RightMenu</span><span class="sxs-lookup"><span data-stu-id="85248-411">RightMenu</span></span> |<span data-ttu-id="85248-412">End</span><span class="sxs-lookup"><span data-stu-id="85248-412">End</span></span> |<span data-ttu-id="85248-413">2015-01-01T00:00:08.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-413">2015-01-01T00:00:08.0000000Z</span></span> |

<span data-ttu-id="85248-414">**Saída**:</span><span class="sxs-lookup"><span data-stu-id="85248-414">**Output**:</span></span>  

| <span data-ttu-id="85248-415">Usuário</span><span class="sxs-lookup"><span data-stu-id="85248-415">User</span></span> | <span data-ttu-id="85248-416">Recurso</span><span class="sxs-lookup"><span data-stu-id="85248-416">Feature</span></span> | <span data-ttu-id="85248-417">Duração</span><span class="sxs-lookup"><span data-stu-id="85248-417">Duration</span></span> |
| --- | --- | --- |
| user@location.com |<span data-ttu-id="85248-418">RightMenu</span><span class="sxs-lookup"><span data-stu-id="85248-418">RightMenu</span></span> |<span data-ttu-id="85248-419">7</span><span class="sxs-lookup"><span data-stu-id="85248-419">7</span></span> |

<span data-ttu-id="85248-420">**Solução**:</span><span class="sxs-lookup"><span data-stu-id="85248-420">**Solution**:</span></span>

````
    SELECT
        [user], feature, DATEDIFF(second, LAST(Time) OVER (PARTITION BY [user], feature LIMIT DURATION(hour, 1) WHEN Event = 'start'), Time) as duration
    FROM input TIMESTAMP BY Time
    WHERE
        Event = 'end'
````

<span data-ttu-id="85248-421">**Explicação**: Olá Use **último** função tooretrieve Olá última **tempo** valor quando o tipo de evento Olá foi **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="85248-421">**Explanation**: Use hello **LAST** function tooretrieve hello last **TIME** value when hello event type was **Start**.</span></span> <span data-ttu-id="85248-422">Olá **último** função usa **PARTITION BY [usuário]** tooindicate que Olá resultado é calculado por usuário exclusivo.</span><span class="sxs-lookup"><span data-stu-id="85248-422">hello **LAST** function uses **PARTITION BY [user]** tooindicate that hello result is computed per unique user.</span></span> <span data-ttu-id="85248-423">consulta de saudação tem um limite máximo de 1 hora de diferença de tempo de saudação entre **iniciar** e **parar** eventos, mas pode ser configurado conforme necessário **(limite DURATION(hour, 1)**.</span><span class="sxs-lookup"><span data-stu-id="85248-423">hello query has a 1-hour maximum threshold for hello time difference between **Start** and **Stop** events, but is configurable as needed **(LIMIT DURATION(hour, 1)**.</span></span>

## <a name="query-example-detect-hello-duration-of-a-condition"></a><span data-ttu-id="85248-424">Exemplo de consulta: detectar duração de saudação de uma condição</span><span class="sxs-lookup"><span data-stu-id="85248-424">Query example: Detect hello duration of a condition</span></span>
<span data-ttu-id="85248-425">**Descrição**: descubra por quanto tempo uma condição durou.</span><span class="sxs-lookup"><span data-stu-id="85248-425">**Description**: Find out how long a condition occurred.</span></span>
<span data-ttu-id="85248-426">Por exemplo, suponha que um bug resultou no peso incorreto de todos os carros (acima de 9.000 quilos).</span><span class="sxs-lookup"><span data-stu-id="85248-426">For example, suppose that a bug resulted in all cars having an incorrect weight (above 20,000 pounds).</span></span> <span data-ttu-id="85248-427">Queremos toocompute duração de saudação do bug hello.</span><span class="sxs-lookup"><span data-stu-id="85248-427">We want toocompute hello duration of hello bug.</span></span>

<span data-ttu-id="85248-428">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="85248-428">**Input**:</span></span>

| <span data-ttu-id="85248-429">Faça</span><span class="sxs-lookup"><span data-stu-id="85248-429">Make</span></span> | <span data-ttu-id="85248-430">Hora</span><span class="sxs-lookup"><span data-stu-id="85248-430">Time</span></span> | <span data-ttu-id="85248-431">Peso</span><span class="sxs-lookup"><span data-stu-id="85248-431">Weight</span></span> |
| --- | --- | --- |
| <span data-ttu-id="85248-432">Honda</span><span class="sxs-lookup"><span data-stu-id="85248-432">Honda</span></span> |<span data-ttu-id="85248-433">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-433">2015-01-01T00:00:01.0000000Z</span></span> |<span data-ttu-id="85248-434">2000</span><span class="sxs-lookup"><span data-stu-id="85248-434">2000</span></span> |
| <span data-ttu-id="85248-435">Toyota</span><span class="sxs-lookup"><span data-stu-id="85248-435">Toyota</span></span> |<span data-ttu-id="85248-436">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-436">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="85248-437">25000</span><span class="sxs-lookup"><span data-stu-id="85248-437">25000</span></span> |
| <span data-ttu-id="85248-438">Honda</span><span class="sxs-lookup"><span data-stu-id="85248-438">Honda</span></span> |<span data-ttu-id="85248-439">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-439">2015-01-01T00:00:03.0000000Z</span></span> |<span data-ttu-id="85248-440">26000</span><span class="sxs-lookup"><span data-stu-id="85248-440">26000</span></span> |
| <span data-ttu-id="85248-441">Toyota</span><span class="sxs-lookup"><span data-stu-id="85248-441">Toyota</span></span> |<span data-ttu-id="85248-442">2015-01-01T00:00:04.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-442">2015-01-01T00:00:04.0000000Z</span></span> |<span data-ttu-id="85248-443">25000</span><span class="sxs-lookup"><span data-stu-id="85248-443">25000</span></span> |
| <span data-ttu-id="85248-444">Honda</span><span class="sxs-lookup"><span data-stu-id="85248-444">Honda</span></span> |<span data-ttu-id="85248-445">2015-01-01T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-445">2015-01-01T00:00:05.0000000Z</span></span> |<span data-ttu-id="85248-446">26000</span><span class="sxs-lookup"><span data-stu-id="85248-446">26000</span></span> |
| <span data-ttu-id="85248-447">Toyota</span><span class="sxs-lookup"><span data-stu-id="85248-447">Toyota</span></span> |<span data-ttu-id="85248-448">2015-01-01T00:00:06.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-448">2015-01-01T00:00:06.0000000Z</span></span> |<span data-ttu-id="85248-449">25000</span><span class="sxs-lookup"><span data-stu-id="85248-449">25000</span></span> |
| <span data-ttu-id="85248-450">Honda</span><span class="sxs-lookup"><span data-stu-id="85248-450">Honda</span></span> |<span data-ttu-id="85248-451">2015-01-01T00:00:07.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-451">2015-01-01T00:00:07.0000000Z</span></span> |<span data-ttu-id="85248-452">26000</span><span class="sxs-lookup"><span data-stu-id="85248-452">26000</span></span> |
| <span data-ttu-id="85248-453">Toyota</span><span class="sxs-lookup"><span data-stu-id="85248-453">Toyota</span></span> |<span data-ttu-id="85248-454">2015-01-01T00:00:08.0000000Z</span><span class="sxs-lookup"><span data-stu-id="85248-454">2015-01-01T00:00:08.0000000Z</span></span> |<span data-ttu-id="85248-455">2000</span><span class="sxs-lookup"><span data-stu-id="85248-455">2000</span></span> |

<span data-ttu-id="85248-456">**Saída**:</span><span class="sxs-lookup"><span data-stu-id="85248-456">**Output**:</span></span>

| <span data-ttu-id="85248-457">FalhaInicial</span><span class="sxs-lookup"><span data-stu-id="85248-457">StartFault</span></span> | <span data-ttu-id="85248-458">FalhaFinal</span><span class="sxs-lookup"><span data-stu-id="85248-458">EndFault</span></span> |
| --- | --- |
| <span data-ttu-id="85248-459">2015-01-01T00:00:02.000Z</span><span class="sxs-lookup"><span data-stu-id="85248-459">2015-01-01T00:00:02.000Z</span></span> |<span data-ttu-id="85248-460">2015-01-01T00:00:07.000Z</span><span class="sxs-lookup"><span data-stu-id="85248-460">2015-01-01T00:00:07.000Z</span></span> |

<span data-ttu-id="85248-461">**Solução**:</span><span class="sxs-lookup"><span data-stu-id="85248-461">**Solution**:</span></span>

````
    WITH SelectPreviousEvent AS
    (
    SELECT
    *,
        LAG([time]) OVER (LIMIT DURATION(hour, 24)) as previousTime,
        LAG([weight]) OVER (LIMIT DURATION(hour, 24)) as previousWeight
    FROM input TIMESTAMP BY [time]
    )

    SELECT 
        LAG(time) OVER (LIMIT DURATION(hour, 24) WHEN previousWeight < 20000 ) [StartFault],
        previousTime [EndFault]
    FROM SelectPreviousEvent
    WHERE
        [weight] < 20000
        AND previousWeight > 20000
````

<span data-ttu-id="85248-462">**Explicação**: Use **LATÊNCIA** tooview fluxo de entrada hello por 24 horas e procurar instâncias onde **StartFault** e **StopFault** são incluídas por Olá Peso < 20000.</span><span class="sxs-lookup"><span data-stu-id="85248-462">**Explanation**: Use **LAG** tooview hello input stream for 24 hours and look for instances where **StartFault** and **StopFault** are spanned by hello weight < 20000.</span></span>

## <a name="query-example-fill-missing-values"></a><span data-ttu-id="85248-463">Exemplo de consulta: preencher valores ausentes</span><span class="sxs-lookup"><span data-stu-id="85248-463">Query example: Fill missing values</span></span>
<span data-ttu-id="85248-464">**Descrição**: para o fluxo de saudação de eventos que têm valores ausentes, produzir um fluxo de eventos com intervalos regulares.</span><span class="sxs-lookup"><span data-stu-id="85248-464">**Description**: For hello stream of events that have missing values, produce a stream of events with regular intervals.</span></span>
<span data-ttu-id="85248-465">Por exemplo, gera um evento a cada 5 segundos que informa o ponto de dados Olá visto mais recentemente.</span><span class="sxs-lookup"><span data-stu-id="85248-465">For example, generate an event every 5 seconds that reports hello most recently seen data point.</span></span>

<span data-ttu-id="85248-466">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="85248-466">**Input**:</span></span>

| <span data-ttu-id="85248-467">t</span><span class="sxs-lookup"><span data-stu-id="85248-467">t</span></span> | <span data-ttu-id="85248-468">value</span><span class="sxs-lookup"><span data-stu-id="85248-468">value</span></span> |
| --- | --- |
| <span data-ttu-id="85248-469">"2014-01-01T06:01:00"</span><span class="sxs-lookup"><span data-stu-id="85248-469">"2014-01-01T06:01:00"</span></span> |<span data-ttu-id="85248-470">1</span><span class="sxs-lookup"><span data-stu-id="85248-470">1</span></span> |
| <span data-ttu-id="85248-471">"2014-01-01T06:01:05"</span><span class="sxs-lookup"><span data-stu-id="85248-471">"2014-01-01T06:01:05"</span></span> |<span data-ttu-id="85248-472">2</span><span class="sxs-lookup"><span data-stu-id="85248-472">2</span></span> |
| <span data-ttu-id="85248-473">"2014-01-01T06:01:10"</span><span class="sxs-lookup"><span data-stu-id="85248-473">"2014-01-01T06:01:10"</span></span> |<span data-ttu-id="85248-474">3</span><span class="sxs-lookup"><span data-stu-id="85248-474">3</span></span> |
| <span data-ttu-id="85248-475">"2014-01-01T06:01:15"</span><span class="sxs-lookup"><span data-stu-id="85248-475">"2014-01-01T06:01:15"</span></span> |<span data-ttu-id="85248-476">4</span><span class="sxs-lookup"><span data-stu-id="85248-476">4</span></span> |
| <span data-ttu-id="85248-477">"2014-01-01T06:01:30"</span><span class="sxs-lookup"><span data-stu-id="85248-477">"2014-01-01T06:01:30"</span></span> |<span data-ttu-id="85248-478">5</span><span class="sxs-lookup"><span data-stu-id="85248-478">5</span></span> |
| <span data-ttu-id="85248-479">"2014-01-01T06:01:35"</span><span class="sxs-lookup"><span data-stu-id="85248-479">"2014-01-01T06:01:35"</span></span> |<span data-ttu-id="85248-480">6</span><span class="sxs-lookup"><span data-stu-id="85248-480">6</span></span> |

<span data-ttu-id="85248-481">**(10 primeiras linhas) de saída**:</span><span class="sxs-lookup"><span data-stu-id="85248-481">**Output (first 10 rows)**:</span></span>

| <span data-ttu-id="85248-482">windowend</span><span class="sxs-lookup"><span data-stu-id="85248-482">windowend</span></span> | <span data-ttu-id="85248-483">lastevent.t</span><span class="sxs-lookup"><span data-stu-id="85248-483">lastevent.t</span></span> | <span data-ttu-id="85248-484">lastevent.value</span><span class="sxs-lookup"><span data-stu-id="85248-484">lastevent.value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="85248-485">2014-01-01T14:01:00.000Z</span><span class="sxs-lookup"><span data-stu-id="85248-485">2014-01-01T14:01:00.000Z</span></span> |<span data-ttu-id="85248-486">2014-01-01T14:01:00.000Z</span><span class="sxs-lookup"><span data-stu-id="85248-486">2014-01-01T14:01:00.000Z</span></span> |<span data-ttu-id="85248-487">1</span><span class="sxs-lookup"><span data-stu-id="85248-487">1</span></span> |
| <span data-ttu-id="85248-488">2014-01-01T14:01:05.000Z</span><span class="sxs-lookup"><span data-stu-id="85248-488">2014-01-01T14:01:05.000Z</span></span> |<span data-ttu-id="85248-489">2014-01-01T14:01:05.000Z</span><span class="sxs-lookup"><span data-stu-id="85248-489">2014-01-01T14:01:05.000Z</span></span> |<span data-ttu-id="85248-490">2</span><span class="sxs-lookup"><span data-stu-id="85248-490">2</span></span> |
| <span data-ttu-id="85248-491">2014-01-01T14:01:10.000Z</span><span class="sxs-lookup"><span data-stu-id="85248-491">2014-01-01T14:01:10.000Z</span></span> |<span data-ttu-id="85248-492">2014-01-01T14:01:10.000Z</span><span class="sxs-lookup"><span data-stu-id="85248-492">2014-01-01T14:01:10.000Z</span></span> |<span data-ttu-id="85248-493">3</span><span class="sxs-lookup"><span data-stu-id="85248-493">3</span></span> |
| <span data-ttu-id="85248-494">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="85248-494">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="85248-495">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="85248-495">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="85248-496">4</span><span class="sxs-lookup"><span data-stu-id="85248-496">4</span></span> |
| <span data-ttu-id="85248-497">2014-01-01T14:01:20.000Z</span><span class="sxs-lookup"><span data-stu-id="85248-497">2014-01-01T14:01:20.000Z</span></span> |<span data-ttu-id="85248-498">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="85248-498">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="85248-499">4</span><span class="sxs-lookup"><span data-stu-id="85248-499">4</span></span> |
| <span data-ttu-id="85248-500">2014-01-01T14:01:25.000Z</span><span class="sxs-lookup"><span data-stu-id="85248-500">2014-01-01T14:01:25.000Z</span></span> |<span data-ttu-id="85248-501">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="85248-501">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="85248-502">4</span><span class="sxs-lookup"><span data-stu-id="85248-502">4</span></span> |
| <span data-ttu-id="85248-503">2014-01-01T14:01:30.000Z</span><span class="sxs-lookup"><span data-stu-id="85248-503">2014-01-01T14:01:30.000Z</span></span> |<span data-ttu-id="85248-504">2014-01-01T14:01:30.000Z</span><span class="sxs-lookup"><span data-stu-id="85248-504">2014-01-01T14:01:30.000Z</span></span> |<span data-ttu-id="85248-505">5</span><span class="sxs-lookup"><span data-stu-id="85248-505">5</span></span> |
| <span data-ttu-id="85248-506">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="85248-506">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="85248-507">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="85248-507">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="85248-508">6</span><span class="sxs-lookup"><span data-stu-id="85248-508">6</span></span> |
| <span data-ttu-id="85248-509">2014-01-01T14:01:40.000Z</span><span class="sxs-lookup"><span data-stu-id="85248-509">2014-01-01T14:01:40.000Z</span></span> |<span data-ttu-id="85248-510">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="85248-510">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="85248-511">6</span><span class="sxs-lookup"><span data-stu-id="85248-511">6</span></span> |
| <span data-ttu-id="85248-512">2014-01-01T14:01:45.000Z</span><span class="sxs-lookup"><span data-stu-id="85248-512">2014-01-01T14:01:45.000Z</span></span> |<span data-ttu-id="85248-513">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="85248-513">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="85248-514">6</span><span class="sxs-lookup"><span data-stu-id="85248-514">6</span></span> |

<span data-ttu-id="85248-515">**Solução**:</span><span class="sxs-lookup"><span data-stu-id="85248-515">**Solution**:</span></span>

    SELECT
        System.Timestamp AS windowEnd,
        TopOne() OVER (ORDER BY t DESC) AS lastEvent
    FROM
        input TIMESTAMP BY t
    GROUP BY HOPPINGWINDOW(second, 300, 5)


<span data-ttu-id="85248-516">**Explicação**: esta consulta gera eventos de 5 segundos e saídas Olá último evento recebido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="85248-516">**Explanation**: This query generates events every 5 seconds and outputs hello last event that was received previously.</span></span> <span data-ttu-id="85248-517">Olá [janela Hopping](https://msdn.microsoft.com/library/dn835041.aspx "Hopping janela — Azure Stream Analytics") duração determina quanto consulta Olá back parece evento mais recente do toofind hello (300 segundos, neste exemplo).</span><span class="sxs-lookup"><span data-stu-id="85248-517">hello [Hopping window](https://msdn.microsoft.com/library/dn835041.aspx "Hopping window--Azure Stream Analytics") duration determines how far back hello query looks toofind hello latest event (300 seconds in this example).</span></span>

## <a name="get-help"></a><span data-ttu-id="85248-518">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="85248-518">Get help</span></span>
<span data-ttu-id="85248-519">Para obter mais assistência, experimente nosso [fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="85248-519">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="85248-520">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="85248-520">Next steps</span></span>
* [<span data-ttu-id="85248-521">Introdução tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="85248-521">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="85248-522">Introdução ao uso do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="85248-522">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="85248-523">Dimensionar trabalhos do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="85248-523">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="85248-524">Referência de Linguagem de Consulta do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="85248-524">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="85248-525">Referência da API REST do Gerenciamento do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="85248-525">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

