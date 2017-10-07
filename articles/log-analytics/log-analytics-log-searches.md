---
title: "dados de aaaFind com pesquisas de log na análise de Log do Azure | Microsoft Docs"
description: "Pesquisas de log permitem toocombine e correlacionam dados de computador de várias fontes em seu ambiente."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: 0d7b6712-1722-423b-a60f-05389cde3625
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: bwren
ms.openlocfilehash: 1161857a0027f05726492417362cb24a8fe21ef8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="find-data-using-log-searches-in-log-analytics"></a><span data-ttu-id="91195-103">Localizar dados usando as pesquisas de logs no Log Analytics</span><span class="sxs-lookup"><span data-stu-id="91195-103">Find data using log searches in Log Analytics</span></span>

>[!NOTE]
> <span data-ttu-id="91195-104">Este artigo descreve as pesquisas de log usando a linguagem de consulta atual Olá na análise de Log.</span><span class="sxs-lookup"><span data-stu-id="91195-104">This article describes log searches using hello current query language in Log Analytics.</span></span>  <span data-ttu-id="91195-105">Se o seu espaço de trabalho tiver sido atualizado toohello [linguagem de consulta de análise de Log novo](log-analytics-log-search-upgrade.md), em seguida, você deve referir-se muito[log Noções básicas sobre pesquisa na análise de Log (novo)](log-analytics-log-search-new.md).</span><span class="sxs-lookup"><span data-stu-id="91195-105">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you should refer too[Understanding log searches in Log Analytics (new)](log-analytics-log-search-new.md).</span></span>


<span data-ttu-id="91195-106">Saudação de núcleo da análise de Log é recurso de pesquisa de log de saudação que permite que você toocombine e correlacionar dados de várias fontes em seu ambiente de máquina.</span><span class="sxs-lookup"><span data-stu-id="91195-106">At hello core of Log Analytics is hello log search feature which allows you toocombine and correlate any machine data from multiple sources within your environment.</span></span> <span data-ttu-id="91195-107">As soluções também são alimentadas pela toobring de pesquisa de log, você as métricas que giram em torno de uma área de problema específica.</span><span class="sxs-lookup"><span data-stu-id="91195-107">Solutions are also powered by log search toobring you metrics pivoted around a particular problem area.</span></span>

<span data-ttu-id="91195-108">Na página de pesquisa hello, você pode criar uma consulta e, em seguida, quando você pesquisa, você pode filtrar os resultados de saudação usando controles da faceta.</span><span class="sxs-lookup"><span data-stu-id="91195-108">On hello Search page, you can create a query, and then when you search, you can filter hello results by using facet controls.</span></span> <span data-ttu-id="91195-109">Você também pode criar consultas avançadas tootransform, filtrar e relatar seus resultados.</span><span class="sxs-lookup"><span data-stu-id="91195-109">You can also create advanced queries tootransform, filter, and report on your results.</span></span>

<span data-ttu-id="91195-110">As consultas de pesquisa de log comuns aparecem na maioria das páginas de solução.</span><span class="sxs-lookup"><span data-stu-id="91195-110">Common log search queries appear on most solution pages.</span></span> <span data-ttu-id="91195-111">Em todo o console do OMS hello, você pode clicar em blocos ou fazer uma busca de itens tooother tooview detalhes sobre o item de saudação usando a pesquisa de log.</span><span class="sxs-lookup"><span data-stu-id="91195-111">Throughout hello OMS console, you can click tiles or drill in tooother items tooview details about hello item by using log search.</span></span>

<span data-ttu-id="91195-112">Neste tutorial, examinaremos exemplos toocover todas as Noções básicas de hello quando você usar a pesquisa de log.</span><span class="sxs-lookup"><span data-stu-id="91195-112">In this tutorial, we'll walk through examples toocover all hello basics when you use log search.</span></span>

<span data-ttu-id="91195-113">Vamos começar com exemplos práticos, simples e desenvolvê-los para que você pode obter um entendimento dos casos de uso prático sobre insights de saudação do toouse Olá sintaxe tooextract de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="91195-113">We'll start with simple, practical examples and then build on them so that you can get an understanding of practical use cases about how toouse hello syntax tooextract hello insights you want from hello data.</span></span>

<span data-ttu-id="91195-114">Depois que você estiver familiarizado com as técnicas de pesquisa, você pode examinar Olá [referência de pesquisa de log de análise de Log](log-analytics-search-reference.md).</span><span class="sxs-lookup"><span data-stu-id="91195-114">After you've familiar with search techniques, you can review hello [Log Analytics log search reference](log-analytics-search-reference.md).</span></span>

## <a name="use-basic-filters"></a><span data-ttu-id="91195-115">Usar filtros básicos</span><span class="sxs-lookup"><span data-stu-id="91195-115">Use basic filters</span></span>
<span data-ttu-id="91195-116">Olá primeiro tooknow faz Olá primeira parte de uma consulta de pesquisa, antes de qualquer "|" caractere de barra vertical, é sempre uma *filtro*.</span><span class="sxs-lookup"><span data-stu-id="91195-116">hello first thing tooknow is that hello first part of a search query, before any "|" vertical pipe character, is always a *filter*.</span></span> <span data-ttu-id="91195-117">Você pode pensar nela como uma cláusula WHERE em TSQL: ela determina *que* subconjunto de dados toopull fora do repositório de dados do OMS hello.</span><span class="sxs-lookup"><span data-stu-id="91195-117">You can think of it as a WHERE clause in TSQL--it determines *what* subset of data toopull out of hello OMS data store.</span></span> <span data-ttu-id="91195-118">Pesquisar no repositório de dados de saudação é se basicamente de especificar as características de saudação dos dados de saudação que você deseja tooextract, portanto, é natural que uma consulta deva começar com hello cláusula WHERE.</span><span class="sxs-lookup"><span data-stu-id="91195-118">Searching in hello data store is largely about specifying hello characteristics of hello data that you want tooextract, so it is natural that a query would start with hello WHERE clause.</span></span>

<span data-ttu-id="91195-119">Olá filtros mais básicos que você pode usar são *palavras-chave*, como 'error' ou 'tempo limite' ou um nome de computador.</span><span class="sxs-lookup"><span data-stu-id="91195-119">hello most basic filters you can use are *keywords*, such as ‘error’ or ‘timeout’, or a computer name.</span></span> <span data-ttu-id="91195-120">Esses tipos de consultas simples normalmente retornam diversas formas de dados dentro de saudação mesmo conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="91195-120">These types of simple queries generally return diverse shapes of data within hello same result set.</span></span> <span data-ttu-id="91195-121">Isso ocorre porque a análise de Log tem diferentes *tipos* dos dados no sistema de saudação.</span><span class="sxs-lookup"><span data-stu-id="91195-121">This is because Log Analytics has different *types* of data in hello system.</span></span>

### <a name="tooconduct-a-simple-search"></a><span data-ttu-id="91195-122">tooconduct uma pesquisa simples</span><span class="sxs-lookup"><span data-stu-id="91195-122">tooconduct a simple search</span></span>
1. <span data-ttu-id="91195-123">No portal do OMS hello, clique em **pesquisa de Log**.</span><span class="sxs-lookup"><span data-stu-id="91195-123">In hello OMS portal, click **Log Search**.</span></span>  
    <span data-ttu-id="91195-124">![pesquisar bloco](./media/log-analytics-log-searches/oms-overview-log-search.png)</span><span class="sxs-lookup"><span data-stu-id="91195-124">![search tile](./media/log-analytics-log-searches/oms-overview-log-search.png)</span></span>
2. <span data-ttu-id="91195-125">No campo de consulta hello, digite `error` e, em seguida, clique em **pesquisa**.</span><span class="sxs-lookup"><span data-stu-id="91195-125">In hello query field, type `error` and then click **Search**.</span></span>  
    <span data-ttu-id="91195-126">![pesquisar erro](./media/log-analytics-log-searches/oms-search-error.png)</span><span class="sxs-lookup"><span data-stu-id="91195-126">![search error](./media/log-analytics-log-searches/oms-search-error.png)</span></span>  
    <span data-ttu-id="91195-127">Por exemplo, a consulta Olá para `error` na Olá a imagem a seguir retornou 100.000 **evento** registros (coletados pelo gerenciamento de logs), 18 **ConfigurationAlert** (gerados pela configuração de registros Avaliação) e 12 **ConfigurationChange** registros (capturados pelo Olá controle de alterações).</span><span class="sxs-lookup"><span data-stu-id="91195-127">For example, hello query for `error` in hello following image returned 100,000 **Event** records (collected by Log Management), 18 **ConfigurationAlert** records (generated by Configuration Assessment) and 12 **ConfigurationChange** records (captured by hello Change Tracking).</span></span>   
    <span data-ttu-id="91195-128">![pesquisar resultados](./media/log-analytics-log-searches/oms-search-results01.png)</span><span class="sxs-lookup"><span data-stu-id="91195-128">![search results](./media/log-analytics-log-searches/oms-search-results01.png)</span></span>  

<span data-ttu-id="91195-129">Esses filtros não são realmente tipos/classes de objeto.</span><span class="sxs-lookup"><span data-stu-id="91195-129">These filters are not really object types/classes.</span></span> <span data-ttu-id="91195-130">*Tipo* é uma marca ou uma propriedade ou uma cadeia de caracteres/nome/categoria, que é anexado tooa parte dos dados.</span><span class="sxs-lookup"><span data-stu-id="91195-130">*Type* is just a tag, or a property, or a string/name/category, that is attached tooa piece of data.</span></span> <span data-ttu-id="91195-131">Alguns documentos no sistema de saudação são marcados como **Type: ConfigurationAlert** e alguns são marcados como **tipo: desempenho**, ou **Type: Event**, e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="91195-131">Some documents in hello system are tagged as **Type:ConfigurationAlert** and some are tagged as **Type:Perf**, or **Type:Event**, and so on.</span></span> <span data-ttu-id="91195-132">Cada resultado da pesquisa, documento, registro ou entrada exibe todas as propriedades de saudação bruto e seus valores para cada uma dessas partes de dados, e você pode usar esses toospecify de nomes de campo no filtro de saudação quando desejar que somente os registros Olá tooretrieve onde o campo Olá tiver aquele valor.</span><span class="sxs-lookup"><span data-stu-id="91195-132">Each search result, document, record, or entry displays all hello raw properties and their values for each of those pieces of data, and you can use those field names toospecify in hello filter when you want tooretrieve only hello records where hello field has that given value.</span></span>

<span data-ttu-id="91195-133">*Type* é realmente apenas um campo que existe em todos os registros; ele não é diferente de qualquer outro campo.</span><span class="sxs-lookup"><span data-stu-id="91195-133">*Type* is really just a field that all records have, it is not different from any other field.</span></span> <span data-ttu-id="91195-134">Isso foi estabelecido com base no valor de saudação do campo de tipo de saudação.</span><span class="sxs-lookup"><span data-stu-id="91195-134">This was established based on hello value of hello Type field.</span></span> <span data-ttu-id="91195-135">Esse registro terá uma forma diferente.</span><span class="sxs-lookup"><span data-stu-id="91195-135">That record will have a different shape or form.</span></span> <span data-ttu-id="91195-136">Por acaso, **tipo = Perf**, ou **tipo = evento** também é Olá sintaxe que você precisa toolearn tooquery para dados de desempenho ou eventos.</span><span class="sxs-lookup"><span data-stu-id="91195-136">Incidentally, **Type=Perf**, or **Type=Event** is also hello syntax that you need toolearn tooquery for performance data or events.</span></span>

<span data-ttu-id="91195-137">Você pode usar dois pontos (:) ou um sinal de igual (=) após o nome do campo hello e antes do valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="91195-137">You can use either a colon (:) or an equal sign (=) after hello field name and before hello value.</span></span> <span data-ttu-id="91195-138">**Type: Event** e **tipo = evento** são equivalentes em significado, você pode escolher Olá estilo desejado.</span><span class="sxs-lookup"><span data-stu-id="91195-138">**Type:Event** and **Type=Event** are equivalent in meaning, you can choose hello style you prefer.</span></span>

<span data-ttu-id="91195-139">Portanto, se hello, digite = Perf registros têm um campo chamado 'CounterName', em seguida, você pode escrever uma consulta semelhante `Type=Perf CounterName="% Processor Time"`.</span><span class="sxs-lookup"><span data-stu-id="91195-139">So, if hello Type=Perf records have a field called 'CounterName', then you can write a query resembling `Type=Perf CounterName="% Processor Time"`.</span></span>

<span data-ttu-id="91195-140">Isso lhe dará apenas dados de desempenho de saudação onde o nome do contador de desempenho de saudação é "% Processor Time".</span><span class="sxs-lookup"><span data-stu-id="91195-140">This will give you only hello performance data where hello performance counter name is "% Processor Time".</span></span>

### <a name="toosearch-for-processor-time-performance-data"></a><span data-ttu-id="91195-141">toosearch para dados de desempenho de tempo do processador</span><span class="sxs-lookup"><span data-stu-id="91195-141">toosearch for processor time performance data</span></span>
* <span data-ttu-id="91195-142">No campo de consulta de pesquisa hello, digite`Type=Perf CounterName="% Processor Time"`</span><span class="sxs-lookup"><span data-stu-id="91195-142">In hello search query field, type `Type=Perf CounterName="% Processor Time"`</span></span>

<span data-ttu-id="91195-143">Você também pode ser mais específico e usar **InstanceName = _ 'Total'** na consulta hello, que é um contador de desempenho do Windows.</span><span class="sxs-lookup"><span data-stu-id="91195-143">You can also be more specific and use **InstanceName=_'Total'** in hello query, which is a Windows performance counter.</span></span> <span data-ttu-id="91195-144">Você também pode selecionar uma faceta e outro **field:value**.</span><span class="sxs-lookup"><span data-stu-id="91195-144">You can also select a facet and another **field:value**.</span></span> <span data-ttu-id="91195-145">filtro de saudação é adicionado automaticamente tooyour filtro na barra de consulta hello.</span><span class="sxs-lookup"><span data-stu-id="91195-145">hello filter is automatically added tooyour filter in hello query bar.</span></span> <span data-ttu-id="91195-146">Você pode ver isso em Olá a imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="91195-146">You can see this in hello following image.</span></span> <span data-ttu-id="91195-147">Ela mostra onde tooclick tooadd **InstanceName: total'** toohello consulta sem digitar nada.</span><span class="sxs-lookup"><span data-stu-id="91195-147">It shows you where tooclick tooadd **InstanceName:’_Total’** toohello query without typing anything.</span></span>

![pesquisar faceta](./media/log-analytics-log-searches/oms-search-facet.png)

<span data-ttu-id="91195-149">A sua consulta agora se torna `Type=Perf CounterName="% Processor Time" InstanceName="_Total"`</span><span class="sxs-lookup"><span data-stu-id="91195-149">Your query now becomes `Type=Perf CounterName="% Processor Time" InstanceName="_Total"`</span></span>

<span data-ttu-id="91195-150">Neste exemplo, você não tem toospecify **tipo = Perf** tooget toothis resultados.</span><span class="sxs-lookup"><span data-stu-id="91195-150">In this example, you don't have toospecify **Type=Perf** tooget toothis result.</span></span> <span data-ttu-id="91195-151">Como Olá campos CounterName e InstanceName existem somente para registros do tipo = Perf, consulta Olá é específica o suficiente tooreturn Olá mesmos resultados como Olá anterior, mais longa:</span><span class="sxs-lookup"><span data-stu-id="91195-151">Because hello fields CounterName and InstanceName only exist for records of Type=Perf, hello query is specific enough tooreturn hello same results as hello longer, previous one:</span></span>

```
CounterName="% Processor Time" InstanceName="_Total"
```

<span data-ttu-id="91195-152">Isso ocorre porque todos os filtros de saudação na consulta Olá são avaliados como estando em *e* uns com os outros.</span><span class="sxs-lookup"><span data-stu-id="91195-152">This is because all hello filters in hello query are evaluated as being in *AND* with each other.</span></span> <span data-ttu-id="91195-153">Efetivamente, hello mais campos você adicionar toohello critérios, você obtém menor, mais específicos e refinados são os resultados.</span><span class="sxs-lookup"><span data-stu-id="91195-153">Effectively, hello more fields you add toohello criteria, you get less, more specific and refined results.</span></span>

<span data-ttu-id="91195-154">Por exemplo, a consulta de saudação `Type=Event EventLog="Windows PowerShell"` é idêntico muito`Type=Event AND EventLog="Windows PowerShell"`.</span><span class="sxs-lookup"><span data-stu-id="91195-154">For example, hello query `Type=Event EventLog="Windows PowerShell"` is identical too`Type=Event AND EventLog="Windows PowerShell"`.</span></span> <span data-ttu-id="91195-155">Retorna todos os eventos que foram registrados no e coletados do log de eventos do Windows PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="91195-155">It returns all events that were logged in and collected from hello Windows PowerShell event log.</span></span> <span data-ttu-id="91195-156">Se você adicionar um filtro várias vezes selecionando repetidamente Olá mesma faceta, em seguida, problema de saudação é apenas superficial: ele pode sobrecarregar a barra de pesquisa hello, mas ainda retorna Olá mesmos resultados porque o operador AND implícito de saudação sempre está lá.</span><span class="sxs-lookup"><span data-stu-id="91195-156">If you add a filter multiple times by repeatedly selecting hello same facet, then hello issue is purely cosmetic--it might clutter hello Search bar, but it still returns hello same results because hello implicit AND operator is always there.</span></span>

<span data-ttu-id="91195-157">Você pode facilmente reverter o operador AND implícito de saudação usando um operador NOT explicitamente.</span><span class="sxs-lookup"><span data-stu-id="91195-157">You can easily reverse hello implicit AND operator by using a NOT operator explicitly.</span></span> <span data-ttu-id="91195-158">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="91195-158">For example:</span></span>

<span data-ttu-id="91195-159">`Type:Event NOT(EventLog:"Windows PowerShell")`ou seu equivalente `Type=Event EventLog!="Windows PowerShell"` retornar todos os eventos de todos os outros logs que não são de log do Windows PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="91195-159">`Type:Event NOT(EventLog:"Windows PowerShell")` or its equivalent `Type=Event EventLog!="Windows PowerShell"` return all events from all other logs that are NOT hello Windows PowerShell log.</span></span>

<span data-ttu-id="91195-160">Você pode usar outro operador booliano, como 'OR'.</span><span class="sxs-lookup"><span data-stu-id="91195-160">Or, you can use other Boolean operator such as ‘OR’.</span></span> <span data-ttu-id="91195-161">consulta a seguir de saudação retorna registros para qual Olá no log de eventos é um sistema ou aplicativo.</span><span class="sxs-lookup"><span data-stu-id="91195-161">hello following query returns records for which hello EventLog is either Application OR System.</span></span>

```
EventLog=Application OR EventLog=System
```

<span data-ttu-id="91195-162">Usando Olá acima de consulta, você obterá as entradas para ambos os logs em Olá mesmo conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="91195-162">Using hello above query, you’ll get entries for both logs in hello same result set.</span></span>

<span data-ttu-id="91195-163">No entanto, se você remover hello ou deixando Olá AND implícito no lugar, em seguida, hello consulta a seguir não produzirá resultados porque não existe uma entrada de log de eventos que pertença tooBOTH logs.</span><span class="sxs-lookup"><span data-stu-id="91195-163">However, if you remove hello OR by leaving hello implicit AND in place, then hello following query will not produce any results because there isn’t an event log entry that belongs tooBOTH logs.</span></span> <span data-ttu-id="91195-164">Cada entrada de log de eventos foi escrita tooonly um dos dois logs de saudação.</span><span class="sxs-lookup"><span data-stu-id="91195-164">Each event log entry was written tooonly one of hello two logs.</span></span>

```
EventLog=Application EventLog=System
```


## <a name="use-additional-filters"></a><span data-ttu-id="91195-165">Usar filtros adicionais</span><span class="sxs-lookup"><span data-stu-id="91195-165">Use additional filters</span></span>
<span data-ttu-id="91195-166">Olá, consulta a seguir retorna entradas de logs de evento 2 para todos os computadores de saudação que enviaram dados.</span><span class="sxs-lookup"><span data-stu-id="91195-166">hello following query returns entries for 2 event logs for all hello computers that have sent data.</span></span>

```
EventLog=Application OR EventLog=System
```

![pesquisar resultados](./media/log-analytics-log-searches/oms-search-results03.png)

<span data-ttu-id="91195-168">A seleção de um dos campos de saudação ou filtros restringirá Olá consulta tooa computador específico, excluindo todos os outros.</span><span class="sxs-lookup"><span data-stu-id="91195-168">Selecting one of hello fields or filters will narrow hello query tooa specific computer, excluding all other ones.</span></span> <span data-ttu-id="91195-169">consulta resultante Olá seria semelhante a seguir hello.</span><span class="sxs-lookup"><span data-stu-id="91195-169">hello resulting query would resemble hello following.</span></span>

```
EventLog=Application OR EventLog=System Computer=SERVER1.contoso.com
```

<span data-ttu-id="91195-170">Que é o equivalente toohello seguinte, por causa de saudação and implícito.</span><span class="sxs-lookup"><span data-stu-id="91195-170">Which is equivalent toohello following, because of hello implicit AND.</span></span>

```
EventLog=Application OR EventLog=System AND Computer=SERVER1.contoso.com
```

<span data-ttu-id="91195-171">Cada consulta é avaliada na ordem explícita de saudação.</span><span class="sxs-lookup"><span data-stu-id="91195-171">Each query is evaluated in hello following explicit order.</span></span> <span data-ttu-id="91195-172">Parênteses de saudação de observação.</span><span class="sxs-lookup"><span data-stu-id="91195-172">Note hello parenthesis.</span></span>

```
(EventLog=Application OR EventLog=System) AND Computer=SERVER1.contoso.com
```

<span data-ttu-id="91195-173">Assim como campo de log de eventos do hello, você pode recuperar dados apenas para um conjunto de computadores específicos adicionando ou.</span><span class="sxs-lookup"><span data-stu-id="91195-173">Just like hello event log field, you can retrieve data only for a set of specific computers by adding OR.</span></span> <span data-ttu-id="91195-174">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="91195-174">For example:</span></span>

```
(EventLog=Application OR EventLog=System) AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com OR Computer=SERVER3.contoso.com)
```

<span data-ttu-id="91195-175">Da mesma forma, este Olá retorno da consulta a seguir **% tempo de CPU** Olá selecionada apenas dois computadores.</span><span class="sxs-lookup"><span data-stu-id="91195-175">Similarly, this hello following query return **% CPU Time** for hello selected two computers only.</span></span>

```
CounterName="% Processor Time"  AND InstanceName="_Total" AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com)
```

### <a name="field-types"></a><span data-ttu-id="91195-176">Tipos de campo</span><span class="sxs-lookup"><span data-stu-id="91195-176">Field types</span></span>
<span data-ttu-id="91195-177">Ao criar filtros, você deve compreender as diferenças de saudação ao trabalhar com tipos diferentes de campos retornados pelas pesquisas de log.</span><span class="sxs-lookup"><span data-stu-id="91195-177">When creating filters, you should understand hello differences in working with different types of fields returned by log searches.</span></span>

<span data-ttu-id="91195-178">**Campos de pesquisa** aparecem em azul nos resultados da pesquisa.</span><span class="sxs-lookup"><span data-stu-id="91195-178">**Searchable fields** show in blue in search results.</span></span>  <span data-ttu-id="91195-179">Você pode usar os campos de pesquisa no campo de toohello específico de condições de pesquisa como seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="91195-179">You can use searchable fields in search conditions specific toohello field such as hello following:</span></span>

```
Type: Event EventLevelName: "Error"
Type: SecurityEvent Computer:Contains("contoso.com")
Type: Event EventLevelName IN {"Error","Warning"}
```

<span data-ttu-id="91195-180">**Campos de pesquisa de texto livre** são mostrados em cinza nos resultados da pesquisa.</span><span class="sxs-lookup"><span data-stu-id="91195-180">**Free text searchable fields** are shown in grey in search results.</span></span>  <span data-ttu-id="91195-181">Eles não podem ser usados com o campo de toohello específico de condições de pesquisa como campos de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="91195-181">They cannot be used with search conditions specific toohello field like searchable fields.</span></span>  <span data-ttu-id="91195-182">Eles apenas são pesquisados ao executar uma consulta em todos os campos, como a seguir hello.</span><span class="sxs-lookup"><span data-stu-id="91195-182">They are only searched when performing a query across all fields such as hello following.</span></span>

```
"Error"
Type: Event "Exception"
```


### <a name="boolean-operators"></a><span data-ttu-id="91195-183">Operadores boolianos</span><span class="sxs-lookup"><span data-stu-id="91195-183">Boolean operators</span></span>
<span data-ttu-id="91195-184">Com campos numéricos e de datetime, você pode procurar por valores usando *maior que*, *menor que* e *menor ou igual*.</span><span class="sxs-lookup"><span data-stu-id="91195-184">With datetime and numeric fields, you can search for values using *greater than*, *lesser than*, and *lesser than or equal*.</span></span> <span data-ttu-id="91195-185">Você pode usar operadores simples como >, <>, =, < =,! = na barra de pesquisa de consulta hello.</span><span class="sxs-lookup"><span data-stu-id="91195-185">You can use simple operators such as >, < , >=, <= , != in hello query search bar.</span></span>

<span data-ttu-id="91195-186">Você pode consultar um log de eventos específico para um período de tempo específico.</span><span class="sxs-lookup"><span data-stu-id="91195-186">You can query a specific event log for a specific period of time.</span></span> <span data-ttu-id="91195-187">Por exemplo, Olá últimas 24 horas é indicada com hello mnemônico expressão a seguir.</span><span class="sxs-lookup"><span data-stu-id="91195-187">For example, hello last 24 hours is expressed with hello following mnemonic expression.</span></span>

```
EventLog=System TimeGenerated>NOW-24HOURS
```


#### <a name="toosearch-using-a-boolean-operator"></a><span data-ttu-id="91195-188">toosearch usando um operador booliano</span><span class="sxs-lookup"><span data-stu-id="91195-188">toosearch using a boolean operator</span></span>
* <span data-ttu-id="91195-189">No campo de consulta de pesquisa hello, digite`EventLog=System TimeGenerated>NOW-24HOURS`</span><span class="sxs-lookup"><span data-stu-id="91195-189">In hello search query field, type `EventLog=System TimeGenerated>NOW-24HOURS`</span></span>  
    <span data-ttu-id="91195-190">![pesquisar com booliano](./media/log-analytics-log-searches/oms-search-boolean.png)</span><span class="sxs-lookup"><span data-stu-id="91195-190">![search with boolean](./media/log-analytics-log-searches/oms-search-boolean.png)</span></span>

<span data-ttu-id="91195-191">Embora você possa controlar Olá graficamente o intervalo de tempo e a maioria das vezes, você poderá toodo, há vantagens tooincluding um filtro de tempo diretamente na consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="91195-191">Although you can control hello time interval graphically, and most times you might want toodo that, there are advantages tooincluding a time filter directly into hello query.</span></span> <span data-ttu-id="91195-192">Por exemplo, isso funciona muito bem com painéis em você pode substituir o tempo de saudação para cada bloco, independentemente de saudação *global* seletor de tempo na página do painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="91195-192">For example, this works great with dashboards where you can override hello time for each tile, regardless of hello *global* time selector on hello dashboard page.</span></span> <span data-ttu-id="91195-193">Para saber mais, confira [Assuntos de tempo no Painel](http://cloudadministrator.wordpress.com/2014/10/19/system-center-advisor-restarted-time-matters-in-dashboard-part-6/).</span><span class="sxs-lookup"><span data-stu-id="91195-193">For more information, see [Time Matters in Dashboard](http://cloudadministrator.wordpress.com/2014/10/19/system-center-advisor-restarted-time-matters-in-dashboard-part-6/).</span></span>

<span data-ttu-id="91195-194">Ao filtrar por tempo, tenha em mente que você obter resultados de saudação *interseção* de saudação dois períodos de tempo: Olá especificada no portal do OMS hello (S1) e Olá especificado na consulta de saudação (S2).</span><span class="sxs-lookup"><span data-stu-id="91195-194">When filtering by time, keep in mind that you get results for hello *intersection* of hello two time periods: hello one specified in hello OMS portal (S1) and hello one specified in hello query (S2).</span></span>

![interseção](./media/log-analytics-log-searches/oms-search-intersection.png)

<span data-ttu-id="91195-196">Isso significa que, se hello períodos de tempo não se cruzarem, por exemplo no portal do OMS Olá em que você escolhe **esta semana** e na consulta Olá onde você define **última semana**, não haverá nenhuma interseção e você não receba todos os resultados.</span><span class="sxs-lookup"><span data-stu-id="91195-196">This means, if hello time periods don’t intersect, for example in hello OMS portal where you choose **This week** and in hello query where you define **last week**, then there is no intersection and you won't receive any results.</span></span>

<span data-ttu-id="91195-197">Operadores de comparação usados para o campo de TimeGenerated Olá também são úteis em outras situações.</span><span class="sxs-lookup"><span data-stu-id="91195-197">Comparison operators used for hello TimeGenerated field are also useful in other situations.</span></span> <span data-ttu-id="91195-198">Por exemplo, com campos numéricos.</span><span class="sxs-lookup"><span data-stu-id="91195-198">For example, with numeric fields.</span></span>

<span data-ttu-id="91195-199">Por exemplo, considerando que os alertas de avaliação de configuração têm Olá valores de severidade a seguir:</span><span class="sxs-lookup"><span data-stu-id="91195-199">For example, given that Configuration Assessment’s alerts have hello following severity values:</span></span>

* <span data-ttu-id="91195-200">0 = Informações</span><span class="sxs-lookup"><span data-stu-id="91195-200">0 = Information</span></span>
* <span data-ttu-id="91195-201">1= Aviso</span><span class="sxs-lookup"><span data-stu-id="91195-201">1 = Warning</span></span>
* <span data-ttu-id="91195-202">2 = Crítico</span><span class="sxs-lookup"><span data-stu-id="91195-202">2 = Critical</span></span>

<span data-ttu-id="91195-203">Você pode consultar alertas de avisos e críticos e também excluir os informativos com hello consulta a seguir:</span><span class="sxs-lookup"><span data-stu-id="91195-203">You can query for both warning and critical alerts and also exclude informational ones with hello following query:</span></span>

```
Type=ConfigurationAlert  Severity>=1
```


<span data-ttu-id="91195-204">Você também pode usar consultas de intervalo.</span><span class="sxs-lookup"><span data-stu-id="91195-204">You can also use range queries.</span></span> <span data-ttu-id="91195-205">Isso significa que você pode fornecer o intervalo de início e término hello dos valores em uma sequência.</span><span class="sxs-lookup"><span data-stu-id="91195-205">This means that you can provide hello beginning and end range of values in a sequence.</span></span> <span data-ttu-id="91195-206">Por exemplo, se você deseja os eventos do log de eventos do Operations Manager Olá onde hello EventID é too2100 maior que ou igual, mas não é maior que 2199, em seguida, Olá consulta a seguir retornaria esses resultados.</span><span class="sxs-lookup"><span data-stu-id="91195-206">For example, if you want events from hello Operations Manager event log where hello EventID is greater than or equal too2100 but not greater than 2199, then hello following query would return them.</span></span>

```
Type=Event EventLog="Operations Manager" EventID:[2100..2199]
```


> [!NOTE]
> <span data-ttu-id="91195-207">sintaxe de intervalo de saudação, você deve usar é o separador de valor de campo de dois-pontos (:) hello e *não* Olá sinal de igual (=).</span><span class="sxs-lookup"><span data-stu-id="91195-207">hello range syntax you must use is hello colon (:) field:value separator and *not* hello equal sign (=).</span></span> <span data-ttu-id="91195-208">Inclua a fim de Olá inferior e superior do intervalo de saudação entre colchetes e separe-as com dois pontos (.).</span><span class="sxs-lookup"><span data-stu-id="91195-208">Enclose hello lower and upper end of hello range in square brackets and separate them with two periods (..).</span></span>
>
>

## <a name="manipulate-search-results"></a><span data-ttu-id="91195-209">Manipular resultados da pesquisa</span><span class="sxs-lookup"><span data-stu-id="91195-209">Manipulate search results</span></span>
<span data-ttu-id="91195-210">Quando você estiver procurando por dados, você deseja toorefine a consulta de pesquisa e ter um bom nível de controle sobre os resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="91195-210">When you're searching for data, you'll want toorefine your search query and have a good level of control over hello results.</span></span> <span data-ttu-id="91195-211">Quando os resultados são recuperados, você pode aplicar comandos tootransform-los.</span><span class="sxs-lookup"><span data-stu-id="91195-211">When results are retrieved, you can apply commands tootransform them.</span></span>

<span data-ttu-id="91195-212">Comandos em pesquisas de análise de Log *deve* vir após o caractere de barra vertical (|) do hello.</span><span class="sxs-lookup"><span data-stu-id="91195-212">Commands in Log Analytics searches *must* follow after hello vertical pipe character (|).</span></span> <span data-ttu-id="91195-213">Um filtro sempre deve ser Olá primeira parte de uma cadeia de caracteres de consulta.</span><span class="sxs-lookup"><span data-stu-id="91195-213">A filter must always be hello first part of a query string.</span></span> <span data-ttu-id="91195-214">Ele define Olá conjunto de dados que você está trabalhando e "canaliza" esses resultados em um comando.</span><span class="sxs-lookup"><span data-stu-id="91195-214">It defines hello data set you're working with and then "pipes" those results into a command.</span></span> <span data-ttu-id="91195-215">Você pode usar comandos do hello pipe tooadd adicionais.</span><span class="sxs-lookup"><span data-stu-id="91195-215">You can then use hello pipe tooadd additional commands.</span></span> <span data-ttu-id="91195-216">Isso é vagamente semelhante pipeline do Windows PowerShell de toohello.</span><span class="sxs-lookup"><span data-stu-id="91195-216">This is loosely similar toohello Windows PowerShell pipeline.</span></span>

<span data-ttu-id="91195-217">Em geral, a saudação linguagem de pesquisa de análise de Log tenta toofollow toomake de estilo e as diretrizes do PowerShell it semelhante toohello IT profissionais e a curva de aprendizado tooease hello.</span><span class="sxs-lookup"><span data-stu-id="91195-217">In general, hello Log Analytics search language tries toofollow PowerShell style and guidelines toomake it similar toohello IT pros, and tooease hello learning curve.</span></span>

<span data-ttu-id="91195-218">Comandos têm nomes de verbos para que você possa perceber facilmente o que eles fazem.</span><span class="sxs-lookup"><span data-stu-id="91195-218">Commands have names of verbs so you can easily tell what they do.</span></span>  

### <a name="sort"></a><span data-ttu-id="91195-219">Classificar</span><span class="sxs-lookup"><span data-stu-id="91195-219">Sort</span></span>
<span data-ttu-id="91195-220">comando de classificação Olá permite Olá toodefine ordem por um ou vários campos de classificação.</span><span class="sxs-lookup"><span data-stu-id="91195-220">hello sort command allows you toodefine hello sorting order by one or multiple fields.</span></span> <span data-ttu-id="91195-221">Mesmo se você não usá-lo, por padrão, a ordem imposta é decrescente por tempo.</span><span class="sxs-lookup"><span data-stu-id="91195-221">Even if you don’t use it, by default, a time descending order is enforced.</span></span> <span data-ttu-id="91195-222">resultados mais recentes de saudação são sempre na parte superior da saudação dos resultados da pesquisa.</span><span class="sxs-lookup"><span data-stu-id="91195-222">hello most recent results are always at hello top of search results.</span></span> <span data-ttu-id="91195-223">Isso significa que quando você executa uma pesquisa com `Type=Event EventID=1234` , o que realmente é executado para você é:</span><span class="sxs-lookup"><span data-stu-id="91195-223">This means that when you run a search, with `Type=Event EventID=1234` what really is executed for you is:</span></span>

```
Type=Event EventID=1234 **| Sort TimeGenerated desc**
```

<span data-ttu-id="91195-224">Isso ocorre porque é o tipo de saudação da experiência que conhecer nos logs.</span><span class="sxs-lookup"><span data-stu-id="91195-224">That's because it is hello type of experience you are familiar with in logs.</span></span> <span data-ttu-id="91195-225">Por exemplo, no Visualizador de eventos do Windows hello.</span><span class="sxs-lookup"><span data-stu-id="91195-225">For example, in hello Windows Event Viewer.</span></span>

<span data-ttu-id="91195-226">Você pode usar classificar resultados de maneira Olá toochange são retornados.</span><span class="sxs-lookup"><span data-stu-id="91195-226">You can use Sort toochange hello way results are returned.</span></span> <span data-ttu-id="91195-227">Olá exemplos a seguir mostram como isso funciona.</span><span class="sxs-lookup"><span data-stu-id="91195-227">hello following examples show how this works.</span></span>

```
Type=Event EventID=1234 | Sort TimeGenerated asc
```

```
Type=Event EventID=1234 | Sort Computer asc
```

```
Type=Event EventID=1234 | Sort Computer asc,TimeGenerated desc
```


<span data-ttu-id="91195-228">Olá exemplos simples acima mostram como os comandos funcionam: eles alteram a forma Olá de resultados Olá Olá filtro retornado.</span><span class="sxs-lookup"><span data-stu-id="91195-228">hello simple examples above show you how commands work--they change hello shape of hello results that hello filter returned.</span></span>

### <a name="limit-and-top"></a><span data-ttu-id="91195-229">Limite e superior</span><span class="sxs-lookup"><span data-stu-id="91195-229">Limit and top</span></span>
<span data-ttu-id="91195-230">Outro comando menos conhecido é LIMITE.</span><span class="sxs-lookup"><span data-stu-id="91195-230">Another less known command is LIMIT.</span></span> <span data-ttu-id="91195-231">O limite é um verbo do tipo do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="91195-231">Limit is a PowerShell-like verb.</span></span> <span data-ttu-id="91195-232">Limite é o comando superior toohello funcionalmente idênticos.</span><span class="sxs-lookup"><span data-stu-id="91195-232">Limit is functionally identical toohello TOP command.</span></span> <span data-ttu-id="91195-233">Olá consultas a seguir retornam Olá mesmos resultados.</span><span class="sxs-lookup"><span data-stu-id="91195-233">hello following queries return hello same results.</span></span>

```
Type=Event EventID=600 | Limit 1
```

```
Type=Event EventID=600 | Top 1
```


#### <a name="toosearch-using-top"></a><span data-ttu-id="91195-234">toosearch usando top</span><span class="sxs-lookup"><span data-stu-id="91195-234">toosearch using top</span></span>
* <span data-ttu-id="91195-235">No campo de consulta de pesquisa hello, digite`Type=Event EventID=600 | Top 1` </span><span class="sxs-lookup"><span data-stu-id="91195-235">In hello search query field, type `Type=Event EventID=600 | Top 1` </span></span>  
    <span data-ttu-id="91195-236">![pesquisar superior](./media/log-analytics-log-searches/oms-search-top.png)</span><span class="sxs-lookup"><span data-stu-id="91195-236">![search top](./media/log-analytics-log-searches/oms-search-top.png)</span></span>

<span data-ttu-id="91195-237">Imagem de saudação acima, há 358 mil registros com EventID = 600.</span><span class="sxs-lookup"><span data-stu-id="91195-237">In hello image above, there are 358 thousand records with EventID=600.</span></span> <span data-ttu-id="91195-238">Olá campos, facetas e filtros de saudação à esquerda sempre mostram informações sobre Olá resultados retornados *pela parte de filtro Olá* de consulta de saudação, que faz parte de saudação antes de qualquer caractere de pipe.</span><span class="sxs-lookup"><span data-stu-id="91195-238">hello fields, facets, and filters on hello left always show information about hello results returned *by hello filter portion* of hello query, which is hello part before any pipe character.</span></span> <span data-ttu-id="91195-239">Olá **resultados** painel somente retorna o resultado de saudação 1 mais recente, pois o comando de exemplo hello moldou e transformou os resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="91195-239">hello **Results** pane only returns hello most recent 1 result, because hello example command shaped and transformed hello results.</span></span>

### <a name="select"></a><span data-ttu-id="91195-240">Selecionar</span><span class="sxs-lookup"><span data-stu-id="91195-240">Select</span></span>
<span data-ttu-id="91195-241">comando SELECT Olá se comporta como Select-Object no PowerShell.</span><span class="sxs-lookup"><span data-stu-id="91195-241">hello SELECT command behaves like Select-Object in PowerShell.</span></span> <span data-ttu-id="91195-242">Ele retorna resultados filtrados que não têm todas as suas propriedades originais.</span><span class="sxs-lookup"><span data-stu-id="91195-242">It returns filtered results that do not have all of their original properties.</span></span> <span data-ttu-id="91195-243">Em vez disso, ele seleciona somente as propriedades de saudação que você especificar.</span><span class="sxs-lookup"><span data-stu-id="91195-243">Instead, it selects only hello properties that you specify.</span></span>

#### <a name="toorun-a-search-using-hello-select-command"></a><span data-ttu-id="91195-244">toorun uma pesquisa usando o comando select Olá</span><span class="sxs-lookup"><span data-stu-id="91195-244">toorun a search using hello select command</span></span>
1. <span data-ttu-id="91195-245">Na pesquisa, digite `Type=Event` e clique em **Pesquisar**.</span><span class="sxs-lookup"><span data-stu-id="91195-245">In Search, type `Type=Event` and then click **Search**.</span></span>
2. <span data-ttu-id="91195-246">Clique em **+ Mostrar mais** em uma saudação resultados tooview tem todas as propriedades de Olá Olá resultados.</span><span class="sxs-lookup"><span data-stu-id="91195-246">Click **+ show more** in one of hello results tooview all hello properties that hello results have.</span></span>
3. <span data-ttu-id="91195-247">Selecione alguns deles explicitamente e hello alterações de consulta muito`Type=Event | Select Computer,EventID,RenderedDescription`.</span><span class="sxs-lookup"><span data-stu-id="91195-247">Select some of those explicitly, and hello query changes too`Type=Event | Select Computer,EventID,RenderedDescription`.</span></span>  
    <span data-ttu-id="91195-248">![pesquisar selecionar](./media/log-analytics-log-searches/oms-search-select.png)</span><span class="sxs-lookup"><span data-stu-id="91195-248">![search select](./media/log-analytics-log-searches/oms-search-select.png)</span></span>

<span data-ttu-id="91195-249">Esse comando é particularmente útil quando você deseja toocontrol saída de pesquisa e escolhe apenas as partes de saudação de dados que realmente importam para exploração, que geralmente não é registro completo de saudação.</span><span class="sxs-lookup"><span data-stu-id="91195-249">This command is particularly useful when you want toocontrol search output and choose only hello portions of data that really matter for your exploration, which often isn’t hello full record.</span></span> <span data-ttu-id="91195-250">Isso também é útil quando os registros de tipos diferentes têm *algumas* propriedades em comum, mas não *todas*.</span><span class="sxs-lookup"><span data-stu-id="91195-250">This is also useful when records of different types have *some* common properties, but not *all* of their properties are common.</span></span> <span data-ttu-id="91195-251">Você pode gerar uma saída mais naturalmente parecida com uma tabela ou funciona bem quando exportada tooa arquivo CSV e processada no Excel.</span><span class="sxs-lookup"><span data-stu-id="91195-251">The, you can generate output that looks more naturally like a table, or work well when exported tooa CSV file and then massaged in Excel.</span></span>

## <a name="use-hello-measure-command"></a><span data-ttu-id="91195-252">Use o comando de medida Olá</span><span class="sxs-lookup"><span data-stu-id="91195-252">Use hello measure command</span></span>
<span data-ttu-id="91195-253">MEDIDA é um dos comandos de hello mais versáteis em pesquisas de análise de Log.</span><span class="sxs-lookup"><span data-stu-id="91195-253">MEASURE is one of hello most versatile commands in Log Analytics searches.</span></span> <span data-ttu-id="91195-254">Ele permite que você tooapply estatística *funções* tooyour dados e agregue os resultados agrupados por um determinado campo.</span><span class="sxs-lookup"><span data-stu-id="91195-254">It allows you tooapply statistical *functions* tooyour data and aggregate results grouped by a given field.</span></span> <span data-ttu-id="91195-255">Há várias funções estatísticas que têm suporte de Medida.</span><span class="sxs-lookup"><span data-stu-id="91195-255">There are multiple statistical functions that Measure supports.</span></span>

### <a name="measure-count"></a><span data-ttu-id="91195-256">Contagem de medida()</span><span class="sxs-lookup"><span data-stu-id="91195-256">Measure count()</span></span>
<span data-ttu-id="91195-257">Olá toowork de primeira função estatística com, e uma das toounderstand mais simples de saudação é Olá *contagem* função.</span><span class="sxs-lookup"><span data-stu-id="91195-257">hello first statistical function toowork with, and one of hello simplest toounderstand is hello *count()* function.</span></span>

<span data-ttu-id="91195-258">Os resultados de qualquer consulta de pesquisa, como `Type=Event`, mostram filtros também chamados de facetas Olá lado esquerdo de resultados da pesquisa.</span><span class="sxs-lookup"><span data-stu-id="91195-258">Results from any search query such as `Type=Event`, show filters also called facets on hello left side of search results.</span></span> <span data-ttu-id="91195-259">Olá filtros mostram uma distribuição de valores por um determinado campo para resultados Olá Olá pesquisa executada.</span><span class="sxs-lookup"><span data-stu-id="91195-259">hello filters show a distribution of values by a given field for hello results in hello search executed.</span></span>

![pesquisar contagem de medida](./media/log-analytics-log-searches/oms-search-measure-count01.png)

<span data-ttu-id="91195-261">Por exemplo, Olá imagem anteriormente, você verá Olá **computador** campo e ele mostra que, em Olá quase 739 mil eventos resultados hello, há 68 valores exclusivos e distintos para Olá **computador** campo nesses registros.</span><span class="sxs-lookup"><span data-stu-id="91195-261">For example, in hello image above you'll see hello **Computer** field and it shows that within hello almost 739 thousand events in hello results, there are 68 unique and distinct values for hello **Computer** field in those records.</span></span> <span data-ttu-id="91195-262">Olá bloco mostra somente Olá 5 principais, que são Olá 5 valores mais comuns que são escritos em Olá **computador** campos), classificados pelo número de saudação de documentos que contêm esse valor específico nesse campo.</span><span class="sxs-lookup"><span data-stu-id="91195-262">hello tile only shows hello top 5, which are hello most common 5 values that are written in hello **Computer** fields), sorted by hello number of documents that contain that specific value in that field.</span></span> <span data-ttu-id="91195-263">Na imagem hello, você pode ver que, dentre os quase 369 mil eventos, 90 mil vêm de computador Olá OpsInsights04.contoso.com 83 mil do computador de DB03.contoso.com Olá e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="91195-263">In hello image you can see that – among those almost 369 thousand events – 90 thousand come from hello OpsInsights04.contoso.com computer, 83 thousand from hello DB03.contoso.com computer, and so on.</span></span>

<span data-ttu-id="91195-264">Se quiser toosee todos os valores, como Olá bloco mostra somente Olá apenas 5 principais?</span><span class="sxs-lookup"><span data-stu-id="91195-264">What if you want toosee all values, since hello tile only shows only hello top 5?</span></span>

<span data-ttu-id="91195-265">Que é quais medidas Olá comando pode fazer com a função de contagem () do hello.</span><span class="sxs-lookup"><span data-stu-id="91195-265">That’s what hello measure command can do with hello count() function.</span></span> <span data-ttu-id="91195-266">Essa função não usa nenhum parâmetro.</span><span class="sxs-lookup"><span data-stu-id="91195-266">This function doesn't use any parameters.</span></span> <span data-ttu-id="91195-267">Você simplesmente especifica Olá campo pelo qual você deseja toogroup por – Olá **computador** campo nesse caso:</span><span class="sxs-lookup"><span data-stu-id="91195-267">You just specify hello field by which you want toogroup by – hello **Computer** field in this case:</span></span>

`Type=Event | Measure count() by Computer`

![pesquisar contagem de medida](./media/log-analytics-log-searches/oms-search-measure-count-computer.png)

<span data-ttu-id="91195-269">No entanto, **Computer** é somente um campo usado *em* cada porção de dados — nenhum banco de dados relacional está envolvido e não há nenhum objeto **Computer** separado em lugar algum.</span><span class="sxs-lookup"><span data-stu-id="91195-269">However, **Computer** is just a field used *in* each piece of data – there are no relational databases involved and there is no separate **Computer** object anywhere.</span></span> <span data-ttu-id="91195-270">Olá apenas valores *na* Olá dados podem descrever qual entidade gerou, além de várias outras características e aspectos dos dados hello –, portanto, Olá termo *faceta*.</span><span class="sxs-lookup"><span data-stu-id="91195-270">Just hello values *in* hello data can describe which entity generated them, and a number of other characteristics and aspects of hello data – hence hello term *facet*.</span></span> <span data-ttu-id="91195-271">No entanto, você pode também agrupar por outros campos.</span><span class="sxs-lookup"><span data-stu-id="91195-271">However, you can just as well group by other fields.</span></span> <span data-ttu-id="91195-272">Como resultados de Olá originais de quase 739 mil eventos que foram canalizados para o comando de medida Olá também têm um campo chamado **EventID**, você pode aplicar Olá mesmo toogroup técnica por esse campo e obter uma contagem de eventos por EventID:</span><span class="sxs-lookup"><span data-stu-id="91195-272">Because hello original results of almost 739 thousand events that are piped into hello measure command also have a field called **EventID**, you can apply hello same technique toogroup by that field and get a count of events by EventID:</span></span>

```
Type=Event | Measure count() by EventID
```

<span data-ttu-id="91195-273">Se você não estiver interessado na contagem de registro real Olá que contêm um valor específico, mas em vez disso, se você desejar apenas uma lista de saudação os valores, você pode adicionar uma *selecione* comando final Olá-lo e simplesmente selecione Olá primeira coluna:</span><span class="sxs-lookup"><span data-stu-id="91195-273">If you're not interested in hello actual record count that contain a specific value, but instead if you only want a list of hello values themselves, you can add a *Select* command at hello end of it and just select hello first column:</span></span>

```
Type=Event | Measure count() by EventID | Select EventID
```

<span data-ttu-id="91195-274">Em seguida, você pode obter resultados mais complexos e classificar previamente os resultados de saudação consulta hello, ou você pode simplesmente clicar Olá colunas na grade de saudação muito.</span><span class="sxs-lookup"><span data-stu-id="91195-274">Then you can get more intricate and pre-sort hello results in hello query, or you can just click hello columns in hello grid, too.</span></span>

```
Type=Event | Measure count() by EventID | Select EventID | Sort EventID asc
```

#### <a name="toosearch-using-measure-count"></a><span data-ttu-id="91195-275">toosearch usando contagem de medida</span><span class="sxs-lookup"><span data-stu-id="91195-275">toosearch using measure count</span></span>
* <span data-ttu-id="91195-276">No campo de consulta de pesquisa hello, digite`Type=Event | Measure count() by EventID`</span><span class="sxs-lookup"><span data-stu-id="91195-276">In hello search query field, type `Type=Event | Measure count() by EventID`</span></span>
* <span data-ttu-id="91195-277">Acrescentar `| Select EventID` toohello final da consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="91195-277">Append `| Select EventID` toohello end of hello query.</span></span>
* <span data-ttu-id="91195-278">Por fim, acrescente `| Sort EventID asc` toohello final da consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="91195-278">Finally, append `| Sort EventID asc` toohello end of hello query.</span></span>

<span data-ttu-id="91195-279">Há algumas toonotice de pontos importantes e a enfatizar:</span><span class="sxs-lookup"><span data-stu-id="91195-279">There are a couple important points toonotice and emphasize:</span></span>

<span data-ttu-id="91195-280">Primeiro, Olá resultados não são resultados brutos originais do hello mais.</span><span class="sxs-lookup"><span data-stu-id="91195-280">First, hello results you see are not hello original raw results anymore.</span></span> <span data-ttu-id="91195-281">Em vez disso, eles são resultados agregados: essencialmente, grupos de resultados.</span><span class="sxs-lookup"><span data-stu-id="91195-281">Instead, they are aggregated results – essentially groups of results.</span></span> <span data-ttu-id="91195-282">Isso não é um problema, mas você deve entender o que você está interagindo com uma forma muito diferente de dados que é diferente da saudação forma bruta original que é criada em Olá rapidamente como resultado da função de agregação/estatística hello.</span><span class="sxs-lookup"><span data-stu-id="91195-282">This isn't a problem, but you should understand that you're interacting with a very different shape of data that differs from hello original raw shape that gets created on hello fly as a result of hello aggregation/statistical function.</span></span>

<span data-ttu-id="91195-283">Segundo, **medidas de contagem** atualmente retorna apenas Olá top 100 resultados distintos.</span><span class="sxs-lookup"><span data-stu-id="91195-283">Second, **Measure count** currently returns only hello top 100 distinct results.</span></span> <span data-ttu-id="91195-284">Esse limite não se aplica toohello outras funções estatísticas.</span><span class="sxs-lookup"><span data-stu-id="91195-284">This limit does not apply toohello other statistical functions.</span></span> <span data-ttu-id="91195-285">Assim, você geralmente precisará toouse um toosearch primeiro do filtro mais preciso para itens específicos antes de aplicar contagem de medida.</span><span class="sxs-lookup"><span data-stu-id="91195-285">So, you'll usually need toouse a more precise filter first toosearch for specific items before you apply measure count().</span></span>

## <a name="use-hello-max-and-min-functions-with-hello-measure-command"></a><span data-ttu-id="91195-286">Usar as funções máx e mín Olá com o comando de medida Olá</span><span class="sxs-lookup"><span data-stu-id="91195-286">Use hello max and min functions with hello measure command</span></span>
<span data-ttu-id="91195-287">Há várias situações em que**Measure Max()** e **Measure Min()** são úteis.</span><span class="sxs-lookup"><span data-stu-id="91195-287">There are various scenarios where **Measure Max()** and **Measure Min()** are useful.</span></span> <span data-ttu-id="91195-288">No entanto, já que elas são opostas, vamos exemplificar Máx() e você pode testar Mín() por conta própria.</span><span class="sxs-lookup"><span data-stu-id="91195-288">However, since each function is opposite of each other, we'll illustrate Max() and you can experiment with Min() on your own.</span></span>

<span data-ttu-id="91195-289">Se você consultar eventos de segurança, eles têm uma propriedade de **nível** que pode variar.</span><span class="sxs-lookup"><span data-stu-id="91195-289">If you query for security events, they have a **Level** property that can vary.</span></span> <span data-ttu-id="91195-290">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="91195-290">For example:</span></span>

```
Type=SecurityEvent
```

![pesquisar início da contagem de medida](./media/log-analytics-log-searches/oms-search-measure-max01.png)

<span data-ttu-id="91195-292">Se você quiser valor mais alto de saudação tooview de segurança Olá todos os eventos de um mesmo computador, grupo de saudação por campo, você pode usar</span><span class="sxs-lookup"><span data-stu-id="91195-292">If you want tooview hello highest value for all of hello security events given a common Computer, hello group by field, you can use</span></span>

```
Type=ConfigurationAlert | Measure Max(Level) by Computer
```

![pesquisar medir máxima computador](./media/log-analytics-log-searches/oms-search-measure-max02.png)

<span data-ttu-id="91195-294">Ela exibirá isso para computadores de saudação que tinham **nível** registros, a maioria deles ter pelo menos 8, o nível muitas tinham um nível de 16.</span><span class="sxs-lookup"><span data-stu-id="91195-294">It will display that for hello computers that had **Level** records, most of them have at least level 8, many had a level of 16.</span></span>

```
Type=ConfigurationAlert | Measure Max(Severity) by Computer
```

![pesquisar tempo máximo gerado computador](./media/log-analytics-log-searches/oms-search-measure-max03.png)

<span data-ttu-id="91195-296">Essa função funciona bem com números, mas também funciona com campos de data e hora.</span><span class="sxs-lookup"><span data-stu-id="91195-296">This function works well with numbers, but it also works with DateTime fields.</span></span> <span data-ttu-id="91195-297">É útil toocheck para Olá última ou carimbo de hora mais recente de qualquer parte dos dados indexados para cada computador.</span><span class="sxs-lookup"><span data-stu-id="91195-297">It is useful toocheck for hello last or most recent time stamp for any piece of data indexed for each computer.</span></span> <span data-ttu-id="91195-298">Por exemplo: quando os eventos de segurança mais recentes da saudação foi relatados para cada máquina?</span><span class="sxs-lookup"><span data-stu-id="91195-298">For example: When was hello most recent security event reported for each machine?</span></span>

```
Type=ConfigurationChange | Measure Max(TimeGenerated) by Computer
```

## <a name="use-hello-avg-function-with-hello-measure-command"></a><span data-ttu-id="91195-299">Use a função de média de saudação com o comando de medida Olá</span><span class="sxs-lookup"><span data-stu-id="91195-299">Use hello avg function with hello measure command</span></span>
<span data-ttu-id="91195-300">Olá função estatística Méd (), usada com medidas permite que você toocalculate Olá valor médio alguns campos e grupo resultados por Olá mesmo ou outro campo.</span><span class="sxs-lookup"><span data-stu-id="91195-300">hello Avg() statistical function used with measure allows you toocalculate hello average value for some field, and group results by hello same or other field.</span></span> <span data-ttu-id="91195-301">Isso é útil em muitos casos, como dados de desempenho.</span><span class="sxs-lookup"><span data-stu-id="91195-301">This is useful in a variety of cases, such as performance data.</span></span>

<span data-ttu-id="91195-302">Vamos começar com os dados de desempenho.</span><span class="sxs-lookup"><span data-stu-id="91195-302">We'll start with performance data.</span></span> <span data-ttu-id="91195-303">Observe que o OMS atualmente coleta contadores de desempenho para computadores Windows e Linux.</span><span class="sxs-lookup"><span data-stu-id="91195-303">Note that OMS currently collects performance counters for both Windows and Linux machines.</span></span>

<span data-ttu-id="91195-304">toosearch para *todos os* dados de desempenho, consulta mais básica Olá é:</span><span class="sxs-lookup"><span data-stu-id="91195-304">toosearch for *all* performance data, hello most basic query is:</span></span>

```
Type=Perf
```

![pesquisar média início](./media/log-analytics-log-searches/oms-search-avg01.png)

<span data-ttu-id="91195-306">Olá primeira coisa que você pode notar é que a análise de Log mostra três perspectivas: lista, que mostra que mostra os registros reais Olá atrás de gráficos Olá; Tabela, que mostra uma exibição tabular dos dados do contador de desempenho; e métricas, que mostra gráficos para Olá contadores de desempenho.</span><span class="sxs-lookup"><span data-stu-id="91195-306">hello first thing you'll notice is that Log Analytics shows you three perspectives: List, which shows you which shows hello actual records behind hello charts; Table, which shows a tabular view of performance counter data; and Metrics, which shows charts for hello performance counters.</span></span>

<span data-ttu-id="91195-307">Imagem de saudação acima, há dois conjuntos de campos marcados que indicam a seguir hello:</span><span class="sxs-lookup"><span data-stu-id="91195-307">In hello image above, there are two sets of fields marked that indicate hello following:</span></span>

* <span data-ttu-id="91195-308">Olá primeiro conjunto identifica o nome de contador de desempenho do Windows, o nome do objeto e o nome da instância no filtro de consulta hello.</span><span class="sxs-lookup"><span data-stu-id="91195-308">hello first set identifies Windows Performance Counter Name, Object Name, and Instance Name in hello query filter.</span></span> <span data-ttu-id="91195-309">Esses são os campos de saudação que provavelmente serão mais comumente usados como facetas/filtros</span><span class="sxs-lookup"><span data-stu-id="91195-309">These are hello fields you probably will most commonly use as facets/filters</span></span>
* <span data-ttu-id="91195-310">**CounterValue** é o valor real de saudação do contador de saudação.</span><span class="sxs-lookup"><span data-stu-id="91195-310">**CounterValue** is hello actual value of hello counter.</span></span> <span data-ttu-id="91195-311">Neste exemplo, o valor de saudação é *75*.</span><span class="sxs-lookup"><span data-stu-id="91195-311">In this example, hello value is *75*.</span></span>
* <span data-ttu-id="91195-312">**TimeGenerated** é 12:51, no formato de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="91195-312">**TimeGenerated** is 12:51, in 24-hour time format.</span></span>

<span data-ttu-id="91195-313">Aqui está um modo de exibição das métricas de saudação em um gráfico.</span><span class="sxs-lookup"><span data-stu-id="91195-313">Here's a view of hello metrics in a graph.</span></span>

![pesquisar média início](./media/log-analytics-log-searches/oms-search-avg02.png)

<span data-ttu-id="91195-315">Depois de ler sobre a forma de registro de desempenho hello e ler sobre outras técnicas de pesquisa, você pode usar esse tipo de dados numéricos medida tooaggregate Avg ().</span><span class="sxs-lookup"><span data-stu-id="91195-315">After reading about hello Perf record shape, and having read about other search techniques, you can use measure Avg() tooaggregate this type of numerical data.</span></span>

<span data-ttu-id="91195-316">Eis um exemplo simples:</span><span class="sxs-lookup"><span data-stu-id="91195-316">Here's a simple example:</span></span>

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" | Measure Avg(CounterValue) by Computer
```

![pesquisar média valordeexemplo](./media/log-analytics-log-searches/oms-search-avg03.png)

<span data-ttu-id="91195-318">Neste exemplo, você pode selecionar contador de desempenho de tempo Total de CPU hello e média por computador.</span><span class="sxs-lookup"><span data-stu-id="91195-318">In this example, you select hello CPU Total Time performance counter and average by Computer.</span></span> <span data-ttu-id="91195-319">Se você quiser toonarrow inativo saudação de tooonly seus resultados últimas 6 horas, você pode usar o controle de filtro de tempo de saudação ou especificar em sua consulta, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="91195-319">If you want toonarrow down your results tooonly hello last 6 hours, you can either use hello time filter control or specify in your query as follows:</span></span>

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer
```

### <a name="toosearch-using-hello-avg-function-with-hello-measure-command"></a><span data-ttu-id="91195-320">toosearch usando a função de média de saudação com o comando de medida Olá</span><span class="sxs-lookup"><span data-stu-id="91195-320">toosearch using hello avg function with hello measure command</span></span>
* <span data-ttu-id="91195-321">Na caixa de consulta de pesquisa hello, digite `Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer`.</span><span class="sxs-lookup"><span data-stu-id="91195-321">In hello Search query box, type `Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer`.</span></span>

<span data-ttu-id="91195-322">Você pode agregar e correlacionar dados *entre* computadores.</span><span class="sxs-lookup"><span data-stu-id="91195-322">You can aggregate and correlate data *across* computers.</span></span> <span data-ttu-id="91195-323">Por exemplo, imagine que você tenha um conjunto de hosts em algum tipo de farm onde cada nó é igual tooany outro e que apenas fazer todas as Olá mesmo tipo de trabalho e a carga deve ser balanceada por aproximação.</span><span class="sxs-lookup"><span data-stu-id="91195-323">For example, imagine that you have a set of hosts in some sort of farm where each node is equal tooany other one and they just do all hello same type of work and load should be roughly balanced.</span></span> <span data-ttu-id="91195-324">Você pode obter seus contadores que todos sigam com hello seguinte consulta e obtenha as médias para toda a farm hello.</span><span class="sxs-lookup"><span data-stu-id="91195-324">You could get their counters all in one go with hello following query and get averages for hello entire farm.</span></span> <span data-ttu-id="91195-325">Você pode iniciar escolhendo computadores Olá com hello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="91195-325">You can start by choosing hello computers with hello following example:</span></span>

```
Type=Perf AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

<span data-ttu-id="91195-326">Agora que você tiver computadores hello, você só deseja tooselect dois indicadores chave de desempenho (KPIs): % de uso de CPU e % espaço livre em disco.</span><span class="sxs-lookup"><span data-stu-id="91195-326">Now that you have hello computers, you also only want tooselect two key performance indicators (KPIs): % CPU Usage and % Free Disk Space.</span></span> <span data-ttu-id="91195-327">Portanto, se torna parte da consulta hello:</span><span class="sxs-lookup"><span data-stu-id="91195-327">So, that part of hello query becomes:</span></span>

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS
```

<span data-ttu-id="91195-328">Agora você pode adicionar computadores e contadores com hello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="91195-328">Now you can add computers and counters with hello following example:</span></span>

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

<span data-ttu-id="91195-329">Como você tem uma seleção muito específica, Olá **medir Méd ()** comando pode retornar Olá média não por computador, mas pelo farm hello, simplesmente agrupando por CounterName.</span><span class="sxs-lookup"><span data-stu-id="91195-329">Because you have a very specific selection, hello **measure Avg()** command can return hello average not by computer, but across hello farm, simply by grouping by CounterName.</span></span> <span data-ttu-id="91195-330">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="91195-330">For example:</span></span>

```
Type=Perf  InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03") | Measure Avg(CounterValue) by CounterName
```

<span data-ttu-id="91195-331">Isso dá a você uma visualização compacta útil de alguns dos KPIs do seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="91195-331">This gives you a useful compact view of a couple of your environment's KPIs.</span></span>

![pesquisar média agrupamento](./media/log-analytics-log-searches/oms-search-avg04.png)

<span data-ttu-id="91195-333">Facilmente, você pode usar consultas de pesquisa de saudação em um painel.</span><span class="sxs-lookup"><span data-stu-id="91195-333">You can easily use hello search query in a dashboard.</span></span> <span data-ttu-id="91195-334">Por exemplo, você pode salvar consulta de pesquisa de saudação e criar um painel de chamado *Web Farm KPIs*.</span><span class="sxs-lookup"><span data-stu-id="91195-334">For example, you could save hello search query and create a dashboard from it named *Web Farm KPIs*.</span></span> <span data-ttu-id="91195-335">toolearn mais sobre como usar os painéis, consulte [criar um painel personalizado em análise de Log](log-analytics-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="91195-335">toolearn more about using dashboards, see [Create a custom dashboard in Log Analytics](log-analytics-dashboards.md).</span></span>

![pesquisar média painel](./media/log-analytics-log-searches/oms-search-avg05.png)

### <a name="use-hello-sum-function-with-hello-measure-command"></a><span data-ttu-id="91195-337">Usar a função de soma de saudação com o comando de medida Olá</span><span class="sxs-lookup"><span data-stu-id="91195-337">Use hello sum function with hello measure command</span></span>
<span data-ttu-id="91195-338">função de soma de saudação é funções tooother semelhantes de comando de medida hello.</span><span class="sxs-lookup"><span data-stu-id="91195-338">hello sum function is similar tooother functions of hello measure command.</span></span> <span data-ttu-id="91195-339">Você pode ver um exemplo sobre como toouse Olá a função de soma em [pesquisa de Logs do IIS W3C no Insights operacionais do Microsoft Azure](http://blogs.msdn.com/b/dmuscett/archive/2014/09/20/w3c-iis-logs-search-in-system-center-advisor-limited-preview.aspx).</span><span class="sxs-lookup"><span data-stu-id="91195-339">You can see an example about how toouse hello sum function at [W3C IIS Logs Search in Microsoft Azure Operational Insights](http://blogs.msdn.com/b/dmuscett/archive/2014/09/20/w3c-iis-logs-search-in-system-center-advisor-limited-preview.aspx).</span></span>

<span data-ttu-id="91195-340">Você pode usar Máx() e Mín() com números, datetimes e cadeias de caracteres de texto.</span><span class="sxs-lookup"><span data-stu-id="91195-340">You can use Max() and Min() with numbers, date times and text strings.</span></span> <span data-ttu-id="91195-341">Com cadeias de caracteres de texto, eles são classificados em ordem alfabética e você obtém a primeira e a última.</span><span class="sxs-lookup"><span data-stu-id="91195-341">With text strings, they are sorted alphabetically and you get first and last.</span></span>

<span data-ttu-id="91195-342">No entanto, você não pode usar Soma() com algo diferente de campos numéricos.</span><span class="sxs-lookup"><span data-stu-id="91195-342">However, you cannot use Sum() with anything other than numerical fields.</span></span> <span data-ttu-id="91195-343">Isso também se aplica a tooAvg().</span><span class="sxs-lookup"><span data-stu-id="91195-343">This also applies tooAvg().</span></span>

### <a name="use-hello-percentile-function-with-hello-measure-command"></a><span data-ttu-id="91195-344">Use a função de percentil de saudação com o comando de medida Olá</span><span class="sxs-lookup"><span data-stu-id="91195-344">Use hello percentile function with hello measure command</span></span>
<span data-ttu-id="91195-345">função de percentil Hello é semelhante tooAvg() e SUM () em que você só pode ser usada para campos numéricos.</span><span class="sxs-lookup"><span data-stu-id="91195-345">hello percentile function is similar tooAvg() and Sum() in that you can only use it for numerical fields.</span></span> <span data-ttu-id="91195-346">Você pode usar qualquer percentil entre 1 too99 em um campo numérico.</span><span class="sxs-lookup"><span data-stu-id="91195-346">You can use any percentile between 1 too99 on a numeric field.</span></span> <span data-ttu-id="91195-347">Você também pode usar os comandos **percentile** e **pct**.</span><span class="sxs-lookup"><span data-stu-id="91195-347">You can also use both **percentile** and **pct** commands.</span></span> <span data-ttu-id="91195-348">Veja alguns exemplos:</span><span class="sxs-lookup"><span data-stu-id="91195-348">Here are few examples:</span></span>  

```
Type:Perf CounterName:"DiskTransers/sec" |measure percentile95(CurrentValue) by Computer
```
```
Type:Perf ObjectName=LogicalDisk CounterName="Current Disk Queue Length" Computer="MyComputerName" | measure pct65(CurrentValue) by InstanceName
```

## <a name="use-hello-where-command"></a><span data-ttu-id="91195-349">Use Olá onde comando</span><span class="sxs-lookup"><span data-stu-id="91195-349">Use hello where command</span></span>
<span data-ttu-id="91195-350">Olá onde o comando funciona como um filtro, mas ele pode ser aplicado no filtro de toofurther pipeline Olá agregado resultados que foram produzidos pelo comando medir, como tooraw contrário resultados filtrados no início de saudação de uma consulta.</span><span class="sxs-lookup"><span data-stu-id="91195-350">hello where command works like a filter, but it can be applied in hello pipeline toofurther filter aggregated results that have been produced by a Measure command – as opposed tooraw results that are filtered at hello beginning of a query.</span></span>

<span data-ttu-id="91195-351">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="91195-351">For example:</span></span>

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer
```

<span data-ttu-id="91195-352">Você pode adicionar outro pipe "|" hello e caractere em que o comando tooonly obter computadores cuja média de CPU é acima de 80%, com hello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="91195-352">You can add another pipe "|" character and hello Where command tooonly get computers whose average CPU is above 80%, with hello following example:</span></span>

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer | Where AVGCPU>80
```

<span data-ttu-id="91195-353">Se você estiver familiarizado com o Microsoft System Center - Operations Manager, você pode pensar Olá onde o comando em termos de pacote de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="91195-353">If you're familiar with Microsoft System Center - Operations Manager, you can think of hello where command in management pack terms.</span></span> <span data-ttu-id="91195-354">Se uma regra de exemplo hello, Olá primeira parte da consulta Olá seria hello e fonte de dados Olá onde o comando seria a detecção de condição hello.</span><span class="sxs-lookup"><span data-stu-id="91195-354">If hello example were a rule, hello first part of hello query would be hello data source and hello where command would be hello condition detection.</span></span>

<span data-ttu-id="91195-355">Você pode usar a consulta hello como um bloco em **meu painel**, como um monitor de classificações, toosee ao computador CPUs são utilizadas em excesso.</span><span class="sxs-lookup"><span data-stu-id="91195-355">You can use hello query as a tile in **My Dashboard**, as a monitor of sorts, toosee when computer CPUs are over-utilized.</span></span> <span data-ttu-id="91195-356">toolearn mais sobre painéis, consulte [criar um painel personalizado em análise de Log](log-analytics-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="91195-356">toolearn more about dashboards, see [Create a custom dashboard in Log Analytics](log-analytics-dashboards.md).</span></span> <span data-ttu-id="91195-357">Você também pode criar e usar painéis utilizando o aplicativo móvel hello.</span><span class="sxs-lookup"><span data-stu-id="91195-357">You can also create and use dashboards using hello mobile app.</span></span> <span data-ttu-id="91195-358">Para saber mais, veja [Aplicativo móvel do OMS ](http://www.windowsphone.com/en-us/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865).</span><span class="sxs-lookup"><span data-stu-id="91195-358">For more information, see [OMS Mobile App ](http://www.windowsphone.com/en-us/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865).</span></span> <span data-ttu-id="91195-359">Olá dois blocos inferiores da saudação imagem a seguir, você pode ver Olá monitor exibindo uma lista e como um número.</span><span class="sxs-lookup"><span data-stu-id="91195-359">In hello bottom two tiles of hello following image, you can see hello monitor displayed a list and as a number.</span></span> <span data-ttu-id="91195-360">Essencialmente, você sempre deseja Olá número toobe zero e Olá lista toobe vazio.</span><span class="sxs-lookup"><span data-stu-id="91195-360">Essentially, you always want hello number toobe zero and hello list toobe empty.</span></span> <span data-ttu-id="91195-361">Caso contrário, isso indica uma condição de alerta.</span><span class="sxs-lookup"><span data-stu-id="91195-361">Otherwise, it indicates an alert condition.</span></span> <span data-ttu-id="91195-362">Se necessário, você pode usar tootake uma olhada em quais computadores estão sob pressão.</span><span class="sxs-lookup"><span data-stu-id="91195-362">If needed, you can use it tootake a look at which machines are under pressure.</span></span>

![painel móvel](./media/log-analytics-log-searches/oms-search-mobile.png)

## <a name="use-hello-in-operator"></a><span data-ttu-id="91195-364">Saudação de uso no operador</span><span class="sxs-lookup"><span data-stu-id="91195-364">Use hello in operator</span></span>
<span data-ttu-id="91195-365">Olá *na* operador, juntamente com *NOT IN* permite que você toouse subpesquisas, que são as pesquisas que incluem outra pesquisa como um argumento.</span><span class="sxs-lookup"><span data-stu-id="91195-365">hello *IN* operator, along with *NOT IN* allows you toouse subsearches, which are searches that include another search as an argument.</span></span> <span data-ttu-id="91195-366">Elas estão contidas em chaves {} dentro de outra pesquisa *primária* ou *externa*.</span><span class="sxs-lookup"><span data-stu-id="91195-366">They are contained in braces {} within another *primary* or *outer* search.</span></span> <span data-ttu-id="91195-367">resultado de saudação de uma subpesquisa, muitas vezes uma lista de resultados distintos, em seguida, é usado como um argumento em sua pesquisa primária.</span><span class="sxs-lookup"><span data-stu-id="91195-367">hello result of a subsearch, often a list of distinct results, is then used as an argument in its primary search.</span></span>

<span data-ttu-id="91195-368">Você pode usar subpesquisas toomatch subconjuntos de dados que você não pode descrever diretamente em uma expressão de pesquisa, mas que podem ser gerados por uma pesquisa.</span><span class="sxs-lookup"><span data-stu-id="91195-368">You can use subsearches toomatch subsets of your data that you cannot describe directly in a search expression, but which can be generated from a search.</span></span> <span data-ttu-id="91195-369">Por exemplo, se você estiver interessado em usar um toofind de pesquisa todos os eventos de *computadores com atualizações de segurança ausentes*, em seguida, você precisa toodesign uma subpesquisa que identifique primeiro *computadores com atualizações de segurança ausentes*  antes de encontrar eventos que pertencem toothose hosts.</span><span class="sxs-lookup"><span data-stu-id="91195-369">For example, if you’re interested in using one search toofind all events from *computers missing security updates*, then you need toodesign a subsearch that first identifies that *computers missing security updates* before it finds events belonging toothose hosts.</span></span>

<span data-ttu-id="91195-370">Portanto, você pode expressar *atualizações de segurança de computadores atualmente com ausentes necessárias* com hello consulta a seguir:</span><span class="sxs-lookup"><span data-stu-id="91195-370">So, you could express *computers currently missing required security updates* with hello following query:</span></span>

```
Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer
```    

![Exemplo de pesquisa IN](./media/log-analytics-log-searches/oms-search-in01-revised.png)

<span data-ttu-id="91195-372">Uma vez que a lista de saudação, você pode usar a pesquisa de saudação como uma lista de saudação do toofeed de pesquisa interna de computadores em uma pesquisa (primária) externa que procurará por eventos para esses computadores.</span><span class="sxs-lookup"><span data-stu-id="91195-372">Once you have hello list, you can use hello search as an inner search toofeed hello list of computers into an outer (primary) search that will look for events for those computers.</span></span> <span data-ttu-id="91195-373">Você pode fazer isso envolve a pesquisa interna Olá em chaves e alimentar os resultados como valores possíveis para um filtro/campo na pesquisa externa hello, usando o operador de IN hello.</span><span class="sxs-lookup"><span data-stu-id="91195-373">You do this by enclosing hello inner search in braces and feeding its results as possible values for a filter/field in hello outer search using hello IN operator.</span></span> <span data-ttu-id="91195-374">Olá consulta seria semelhante a:</span><span class="sxs-lookup"><span data-stu-id="91195-374">hello query would resemble:</span></span>

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer}
```
![Exemplo de pesquisa IN](./media/log-analytics-log-searches/oms-search-in02-revised.png)

<span data-ttu-id="91195-376">Também o tempo de saudação do aviso de filtro usado na pesquisa interna Olá porque Olá avaliação de atualização do sistema tira um instantâneo de todos os computadores a cada 24 horas.</span><span class="sxs-lookup"><span data-stu-id="91195-376">Also notice hello time filter used in hello inner search because hello System Update Assessment takes a snapshot of all computers every 24 hours.</span></span> <span data-ttu-id="91195-377">Você pode fazer consulta interna hello mais simples e precisa apenas procurando por um dia.</span><span class="sxs-lookup"><span data-stu-id="91195-377">You can make hello inner query more lightweight and precise by only searching for a day.</span></span> <span data-ttu-id="91195-378">pesquisa externa Olá usa em vez disso, seleção de tempo de saudação na interface de usuário hello, recuperando os eventos de saudação últimos 7 dias.</span><span class="sxs-lookup"><span data-stu-id="91195-378">hello outer search instead uses hello time selection in hello user interface, retrieving events from hello last 7 days.</span></span> <span data-ttu-id="91195-379">Confira [Operadores boolianos](#boolean-operators) para saber mais sobre operadores de tempo.</span><span class="sxs-lookup"><span data-stu-id="91195-379">See [Boolean operators](#boolean-operators) for more information about time operators.</span></span>

<span data-ttu-id="91195-380">Porque você só use Olá os resultados de pesquisa interna de saudação como um valor de filtro para Olá externa, você ainda poderá aplicar comandos na pesquisa externa hello.</span><span class="sxs-lookup"><span data-stu-id="91195-380">Because you really only use hello results of hello inner search as a filter value for hello outer one, you can still apply commands in hello outer search.</span></span> <span data-ttu-id="91195-381">Por exemplo, você ainda pode Olá grupo acima eventos com outro comando de medida:</span><span class="sxs-lookup"><span data-stu-id="91195-381">For example, you can still group hello above events with another measure command:</span></span>

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer} | measure count() by Source
```

![Exemplo de pesquisa IN](./media/log-analytics-log-searches/oms-search-in03-revised.png)

<span data-ttu-id="91195-383">Em geral, convém tooexecute sua consulta interna rapidamente porque a análise de Log tem tempos limite do lado do serviço para ele e também tooreturn uma pequena quantidade de resultados.</span><span class="sxs-lookup"><span data-stu-id="91195-383">Generally, you want your inner query tooexecute quickly because Log Analytics has service-side timeouts for it and also tooreturn a small amount of results.</span></span> <span data-ttu-id="91195-384">Se a consulta interna Olá retorna mais resultados, lista de resultados de saudação é truncada, o que poderia potencialmente fazer Olá pesquisa externa tooreturn resultados incorretos.</span><span class="sxs-lookup"><span data-stu-id="91195-384">If hello inner query returns more results, hello result list gets truncated, which could potentially cause hello outer search tooreturn incorrect results.</span></span>

<span data-ttu-id="91195-385">Outra regra é que a pesquisa de saudação interna atualmente precisa tooprovide *agregados* resultados.</span><span class="sxs-lookup"><span data-stu-id="91195-385">Another rule is that hello inner search currently needs tooprovide *aggregated* results.</span></span> <span data-ttu-id="91195-386">Em outras palavras, ela deve conter um comando *measure*. Atualmente, você não pode alimentar uma pesquisa externa com resultados brutos.</span><span class="sxs-lookup"><span data-stu-id="91195-386">In other words, it must contain a *measure* command; you cannot currently feed raw results into an outer search.</span></span>

<span data-ttu-id="91195-387">Além disso, pode haver apenas um operador IN e ele deve ser Olá último filtro na consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="91195-387">Also, there can be only one IN operator and it must be hello last filter in hello query.</span></span> <span data-ttu-id="91195-388">Vários operadores IN não podem ser ou – isso basicamente impede a execução de várias subpesquisas: Olá importante ponto é que apenas uma pesquisa interna/subpesquisa é possível para cada pesquisa externa.</span><span class="sxs-lookup"><span data-stu-id="91195-388">Multiple IN operators cannot be OR’d – this essentially prevents running multiple subsearches: hello important point is that only one sub/inner search is possible for each outer search.</span></span>

<span data-ttu-id="91195-389">Mesmo com esses limites, o IN permite vários tipos de pesquisas correlacionadas e permite que você toodefine toogroups algo semelhante, como computadores, usuários ou arquivos – quaisquer campos Olá em seus dados contêm.</span><span class="sxs-lookup"><span data-stu-id="91195-389">Even with these limits, IN enables many kinds of correlated searches, and allows you toodefine something similar toogroups such as computers, users, or files – whatever hello fields in your data contain.</span></span> <span data-ttu-id="91195-390">Veja mais alguns exemplos:</span><span class="sxs-lookup"><span data-stu-id="91195-390">Here are more examples:</span></span>

<span data-ttu-id="91195-391">**Todas as atualizações ausentes em computadores em que a configuração de Atualização Automática está desabilitada**</span><span class="sxs-lookup"><span data-stu-id="91195-391">**All updates missing from computers where Automatic Update setting is disabled**</span></span>

```
Type=Update UpdateState=Needed Optional=false Computer IN {Type=UpdateSummary WindowsUpdateSetting=Manual | measure count() by Computer} | measure count() by KBID
```

<span data-ttu-id="91195-392">**Todos os eventos de erro de computadores que estejam executando o SQL Server (=onde a Avaliação do SQL foi executada)**</span><span class="sxs-lookup"><span data-stu-id="91195-392">**All error events from computers running SQL Server (=where SQL Assessment has run)**</span></span>

```
Type=Event EventLevelName=error Computer IN {Type=SQLAssessmentRecommendation | measure count() by Computer}
```

<span data-ttu-id="91195-393">**Todos os eventos de segurança a partir de computadores que sejam Controladores de Domínio (= onde a Avaliação do AD foi executada)**</span><span class="sxs-lookup"><span data-stu-id="91195-393">**All security events from computers that are Domain Controllers (=where AD Assessment has run)**</span></span>

```
Type=SecurityEvent Computer IN { Type=ADAssessmentRecommendation | measure count() by Computer }
```

<span data-ttu-id="91195-394">**Que outras contas fizerem logon nos toohello mesmos computadores em que a conta BACONLAND\jochan fez logon?**</span><span class="sxs-lookup"><span data-stu-id="91195-394">**Which other accounts have logged on toohello same computers where account BACONLAND\jochan has logged on?**</span></span>

```
Type=SecurityEvent EventID=4624   Account!="BACONLAND\\jochan" Computer IN { Type=SecurityEvent EventID=4624   Account="BACONLAND\\jochan" | measure count() by Computer } | measure count() by Account
```

## <a name="use-hello-distinct-command"></a><span data-ttu-id="91195-395">Use o comando distinto Olá</span><span class="sxs-lookup"><span data-stu-id="91195-395">Use hello distinct command</span></span>
<span data-ttu-id="91195-396">Como Olá nome sugere, esse comando fornece uma lista de valores distintos para um campo.</span><span class="sxs-lookup"><span data-stu-id="91195-396">As hello name suggests, this command provides a list of distinct values for a field.</span></span> <span data-ttu-id="91195-397">É surpreendentemente simples, mas muito útil.</span><span class="sxs-lookup"><span data-stu-id="91195-397">It's surprisingly simple but quite useful.</span></span> <span data-ttu-id="91195-398">Olá que mesmo também pode ser obtido com o comando de contagem de medida, assim como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="91195-398">hello same could be achieved with measure count() command as well, as shown below.</span></span>

```
Type=Event | Measure count() by Computer
```

![Exemplo de comando de pesquisa DISTINCT](./media/log-analytics-log-searches/oms-search-distinct01-revised.png)

<span data-ttu-id="91195-400">No entanto, se você estiver interessado em apenas uma lista de valores distintos e não Olá contagem de documentos que tenham que valores, em seguida, DISTINCT pode fornecer tooread limpa e fáceis de saída e sintaxes mais curtas, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="91195-400">However, if all you're interested in is just a list of distinct values and not hello count of documents that have that values, then DISTINCT can provide cleaner and easier tooread output, and shorter syntax, as shown below.</span></span>

```
Type=Event | Distinct Computer
```
![Exemplo de comando de pesquisa DISTINCT](./media/log-analytics-log-searches/oms-search-distinct02-revised.png)

## <a name="use-hello-countdistinct-function-with-hello-measure-command"></a><span data-ttu-id="91195-402">Use a função de countdistinct de saudação com o comando de medida Olá</span><span class="sxs-lookup"><span data-stu-id="91195-402">Use hello countdistinct function with hello measure command</span></span>
<span data-ttu-id="91195-403">função countdistinct de saudação conta o número de saudação de valores distintos dentro de cada grupo.</span><span class="sxs-lookup"><span data-stu-id="91195-403">hello countdistinct function counts hello number of distinct values within each group.</span></span> <span data-ttu-id="91195-404">Por exemplo, pode ser usado toocount Olá número de computadores exclusivos de relatório para cada tipo:</span><span class="sxs-lookup"><span data-stu-id="91195-404">For example, it could be used toocount hello number of unique computers reporting for each Type:</span></span>

```
* | measure countdistinct(Computer) by Type
```

![OMS-countdistinct](./media/log-analytics-log-searches/oms-countdistinct.png)

## <a name="use-hello-measure-interval-command"></a><span data-ttu-id="91195-406">Use o comando de intervalo de medida Olá</span><span class="sxs-lookup"><span data-stu-id="91195-406">Use hello measure interval command</span></span>
<span data-ttu-id="91195-407">Com a coleta de dados de desempenho em tempo real, você pode coletar e visualizar qualquer contador de desempenho no Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="91195-407">With near real-time performance data collection, you can collect and visualize any performance counter in Log Analytics.</span></span> <span data-ttu-id="91195-408">Basta inserir consulta de saudação **tipo: desempenho** retornará milhares de gráficos de métricas com base no número de saudação de contadores e servidores em seu ambiente de análise de Log.</span><span class="sxs-lookup"><span data-stu-id="91195-408">Simply entering hello query **Type:Perf** will return thousands of metric graphs based on hello number of counters and servers in your Log Analytics environment.</span></span> <span data-ttu-id="91195-409">Com a agregação de métrica sob demanda, você pode examinar Olá métricas gerais no ambiente em um alto nível e mergulho no dados mais granulares, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="91195-409">With on-demand metric aggregation, you can look at hello overall metrics in your environment at a high level, and deep dive into more granular data as you need to.</span></span>

<span data-ttu-id="91195-410">Digamos que você deseja tooknow novidades Olá média de CPU em todos os computadores.</span><span class="sxs-lookup"><span data-stu-id="91195-410">Let’s say that you want tooknow what is hello average CPU across all your computers.</span></span> <span data-ttu-id="91195-411">Olhando Olá média de CPU para cada computador pode não ser útil porque os resultados podem obter amenizados. toolook para obter mais detalhes, você pode agregar o resultado em um menor tempo de blocos de janela e aparência em uma série de tempo entre diferentes dimensões.</span><span class="sxs-lookup"><span data-stu-id="91195-411">Looking at hello average CPU for every computer might not be helpful because results may get smoothed out. toolook into more details, you can aggregate your result in a smaller time window chunks, and look into a time series across different dimensions.</span></span> <span data-ttu-id="91195-412">Por exemplo, você pode executar média por hora de saudação do uso de CPU em todos os computadores da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="91195-412">For example, you can perform hello hourly average of CPU usage across all your computers as follows:</span></span>

```
Type:Perf CounterName="% Processor Time" InstanceName="_Total" | measure avg(CounterValue) by Computer Interval 1HOUR
```

![intervalo médio de medidas](./media/log-analytics-log-searches/oms-measure-avg-interval.png)

<span data-ttu-id="91195-414">Por padrão, esses resultados serão exibidos em um gráfico de linhas interativo com várias séries.</span><span class="sxs-lookup"><span data-stu-id="91195-414">By default these results will be displayed in a multi-series interactive line chart.</span></span>  <span data-ttu-id="91195-415">Esse gráfico oferece suporte à alternância de séries (com o redimensionamento do eixo y), ao zoom e à focalização.</span><span class="sxs-lookup"><span data-stu-id="91195-415">This chart supports series toggling (with y-axis rescaling), zooming, and hovering.</span></span>  <span data-ttu-id="91195-416">opção de exibição de tabela Olá ainda está disponível para exibir dados brutos hello, se necessário.</span><span class="sxs-lookup"><span data-stu-id="91195-416">hello table display option is still available for viewing hello raw data if necessary.</span></span>

<span data-ttu-id="91195-417">Você também pode agrupar por outros campos.</span><span class="sxs-lookup"><span data-stu-id="91195-417">You can also group by other fields.</span></span> <span data-ttu-id="91195-418">Neste exemplo, vou analisar todos os contadores de % Olá para um computador específico e desejo tooknow novidades percentuais de saudação 70 por hora de cada contador:</span><span class="sxs-lookup"><span data-stu-id="91195-418">In this example, I am looking at all hello % counters for one specific computer, and I want tooknow what is hello hourly 70 percentiles of every counter:</span></span>

```
Type:Perf Computer=beefpatty4 CounterName=%* InstanceName=_Total | measure percentile70(CounterValue) by CounterName Interval 1HOUR
```
<span data-ttu-id="91195-419">Toonote de uma coisa é que essas consultas não estão limitado tooperformance contadores.</span><span class="sxs-lookup"><span data-stu-id="91195-419">One thing toonote is that these queries are not limited tooperformance counters.</span></span> <span data-ttu-id="91195-420">Você pode aplicá-los tooany métrica.</span><span class="sxs-lookup"><span data-stu-id="91195-420">You can apply them tooany metric.</span></span> <span data-ttu-id="91195-421">Neste exemplo, examinarei os logs do IIS W3C.</span><span class="sxs-lookup"><span data-stu-id="91195-421">In this example, I’m looking at W3C IIS logs.</span></span> <span data-ttu-id="91195-422">Quero tooknow o que é o tempo máximo de saudação que ele assume um intervalo de 5 minutos para cada solicitação de processamento:</span><span class="sxs-lookup"><span data-stu-id="91195-422">I want tooknow what is hello maximum time it takes over a 5-minute interval for processing each request:</span></span>

```
Type:W3CIISLog | measure max(TimeTaken) by csMethod Interval 5MINUTES
```

### <a name="use-multiple-aggregates-in-one-query"></a><span data-ttu-id="91195-423">Usar várias agregações em uma consulta</span><span class="sxs-lookup"><span data-stu-id="91195-423">Use multiple aggregates in one query</span></span>
<span data-ttu-id="91195-424">Você pode especificar várias cláusulas agregadas em um comando de medida.</span><span class="sxs-lookup"><span data-stu-id="91195-424">You can specify multiple aggregate clauses in a measure command.</span></span>  <span data-ttu-id="91195-425">Cada uma delas pode ter um alias de forma independente.</span><span class="sxs-lookup"><span data-stu-id="91195-425">Each one can be aliased independently.</span></span>  <span data-ttu-id="91195-426">Se não for especificado um resultante de saudação do alias nome do campo será a função de agregação de saudação que foi usada (ou seja, "avg(CounterValue)" para avg(CounterValue)).</span><span class="sxs-lookup"><span data-stu-id="91195-426">If it is not given an alias hello resulting field name will be hello aggregate function that was used (i.e. "avg(CounterValue)" for avg(CounterValue)).</span></span>

 ```
Type=WireData | measure avg(ReceivedBytes), avg(SentBytes) by Direction interval 1hour
```
![OMS-multiaggregates1](./media/log-analytics-log-searches/oms-multiaggregates1.png)

<span data-ttu-id="91195-428">Veja outro exemplo:</span><span class="sxs-lookup"><span data-stu-id="91195-428">Here is another example:</span></span>

 ```
* | measure countdistinct(Computer) as Computers, count() as TotalRecords by Type
```


## <a name="next-steps"></a><span data-ttu-id="91195-429">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="91195-429">Next steps</span></span>
<span data-ttu-id="91195-430">Para obter outras informações sobre pesquisas de log, veja:</span><span class="sxs-lookup"><span data-stu-id="91195-430">For additional information about log searches, see:</span></span>

* <span data-ttu-id="91195-431">Use [campos personalizados na análise de Log](log-analytics-custom-fields.md) tooextend pesquisas de log.</span><span class="sxs-lookup"><span data-stu-id="91195-431">Use [Custom fields in Log Analytics](log-analytics-custom-fields.md) tooextend log searches.</span></span>
* <span data-ttu-id="91195-432">Saudação de revisão [referência de pesquisa de log de análise de Log](log-analytics-search-reference.md) tooview todos Olá Pesquisar campos e facetas disponíveis na análise de Log.</span><span class="sxs-lookup"><span data-stu-id="91195-432">Review hello [Log Analytics log search reference](log-analytics-search-reference.md) tooview all of hello search fields and facets available in Log Analytics.</span></span>
