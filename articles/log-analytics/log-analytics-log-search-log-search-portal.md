---
title: "portal de pesquisa de Log de saudação aaaUsing na análise de Log do Azure | Microsoft Docs"
description: "Este artigo inclui um tutorial que descreve como toocreate pesquisas de log e analisar dados armazenados em seu espaço de trabalho de análise de Log usando o portal de pesquisa de Log de saudação.  tutorial de saudação inclui executar algumas consultas simples tooreturn diferentes tipos de dados e analisar os resultados."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: 2e6633d548bb508edc0c650d11d2c32fc6ee536c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-log-searches-in-azure-log-analytics-using-hello-log-search-portal"></a><span data-ttu-id="d8cdb-104">Criar pesquisas de log na análise de Log do Azure usando o portal de pesquisa de Log de saudação</span><span class="sxs-lookup"><span data-stu-id="d8cdb-104">Create log searches in Azure Log Analytics using hello Log Search portal</span></span>

> [!NOTE]
> <span data-ttu-id="d8cdb-105">Este artigo descreve o portal de pesquisa de Log de saudação na análise de Log do Azure usando Olá nova linguagem de consulta.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-105">This article describes hello Log Search portal in Azure Log Analytics using hello new query language.</span></span>  <span data-ttu-id="d8cdb-106">Você pode saber mais sobre a nova linguagem de saudação e obter Olá procedimento tooupgrade seu espaço de trabalho em [atualizar sua pesquisa de log de toonew de espaço de trabalho do Azure Log Analytics](log-analytics-log-search-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="d8cdb-106">You can learn more about hello new language and get hello procedure tooupgrade your workspace at [Upgrade your Azure Log Analytics workspace toonew log search](log-analytics-log-search-upgrade.md).</span></span>  
>
> <span data-ttu-id="d8cdb-107">Se o espaço de trabalho não tiver sido atualizado toohello nova linguagem de consulta, você deve referir-se muito[localizar os dados usando pesquisas de log na análise de Log](log-analytics-log-searches.md) para obter informações sobre a versão atual de saudação do portal de pesquisa de Log de saudação.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-107">If your workspace hasn't been upgraded toohello new query language, you should refer too[Find data using log searches in Log Analytics](log-analytics-log-searches.md) for information on hello current version of hello Log Search portal.</span></span>

<span data-ttu-id="d8cdb-108">Este artigo inclui um tutorial que descreve como toocreate pesquisas de log e analisar dados armazenados em seu espaço de trabalho de análise de Log usando o portal de pesquisa de Log de saudação.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-108">This article includes a tutorial that describes how toocreate log searches and analyze data stored in your Log Analytics workspace using hello Log Search portal.</span></span>  <span data-ttu-id="d8cdb-109">tutorial de saudação inclui executar algumas consultas simples tooreturn diferentes tipos de dados e analisar os resultados.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-109">hello tutorial includes running some simple queries tooreturn different types of data and analyzing results.</span></span>  <span data-ttu-id="d8cdb-110">Ele se concentra nos recursos no portal de pesquisa de Log de saudação para modificar Olá consulta em vez de modificá-la diretamente.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-110">It focuses on features in hello Log Search portal for modifying hello query rather than modifying it directly.</span></span>  <span data-ttu-id="d8cdb-111">Para obter detalhes sobre a edição direta consulta hello, consulte Olá [referência de linguagem de consulta](https://go.microsoft.com/fwlink/?linkid=856079).</span><span class="sxs-lookup"><span data-stu-id="d8cdb-111">For details on directly editing hello query, see hello [Query Language reference](https://go.microsoft.com/fwlink/?linkid=856079).</span></span>

<span data-ttu-id="d8cdb-112">pesquisas de toocreate no portal do Advanced Analytics Olá em vez do portal de pesquisa de Log hello, consulte [guia de Introdução com hello Portal da análise de](https://go.microsoft.com/fwlink/?linkid=856587).</span><span class="sxs-lookup"><span data-stu-id="d8cdb-112">toocreate searches in hello Advanced Analytics portal instead of hello Log Search portal, see [Getting Started with hello Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856587).</span></span>  <span data-ttu-id="d8cdb-113">Ambos os portais usam Olá consulta mesmo idioma tooaccess Olá mesmos dados no espaço de trabalho de análise de Log de saudação.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-113">Both portals use hello same query language tooaccess hello same data in hello Log Analytics workspace.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d8cdb-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d8cdb-114">Prerequisites</span></span>
<span data-ttu-id="d8cdb-115">Este tutorial presume que você já tem um espaço de trabalho de análise de Log pelo menos uma origem conectada que gera dados para Olá tooanalyze de consultas.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-115">This tutorial assumes that you already have a Log Analytics workspace with at least one connected source that generates data for hello queries tooanalyze.</span></span>  

- <span data-ttu-id="d8cdb-116">Se você não tiver um espaço de trabalho, você pode criar uma livre usando o procedimento Olá [começar com um espaço de trabalho de análise de Log](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d8cdb-116">If you don't have a workspace, you can create a free one using hello procedure at [Get started with a Log Analytics workspace](log-analytics-get-started.md).</span></span>
- <span data-ttu-id="d8cdb-117">Conecte-se pelo menos uma [agente do Windows](log-analytics-windows-agents.md) ou um [agente Linux](log-analytics-linux-agents.md) toohello espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-117">Connect least one [Windows agent](log-analytics-windows-agents.md) or one [Linux agent](log-analytics-linux-agents.md) toohello workspace.</span></span>  

## <a name="open-hello-log-search-portal"></a><span data-ttu-id="d8cdb-118">Portal de pesquisa de Log aberto Olá</span><span class="sxs-lookup"><span data-stu-id="d8cdb-118">Open hello Log Search portal</span></span>
<span data-ttu-id="d8cdb-119">Comece abrindo o portal de pesquisa de Log de saudação.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-119">Start by opening hello Log Search portal.</span></span>  <span data-ttu-id="d8cdb-120">Você pode acessá-lo no portal do OMS hello ou Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-120">You can access it in either hello Azure portal or hello OMS portal.</span></span>

1. <span data-ttu-id="d8cdb-121">Olá Abrir portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-121">Open hello Azure portal.</span></span>
2. <span data-ttu-id="d8cdb-122">Navegue tooLog análise e selecione seu espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-122">Navigate tooLog Analytics and select your workspace.</span></span>
3. <span data-ttu-id="d8cdb-123">Selecione **pesquisa de Log** toostay em hello Azure portal ou inicie Olá portal do OMS selecionando **Portal do OMS** e clicando no botão de pesquisa de Log de saudação.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-123">Either select **Log Search** toostay in hello Azure portal or launch hello OMS portal by selecting **OMS Portal** and then clicking hello Log Search button.</span></span>

![Botão Pesquisar Log](media/log-analytics-log-search-log-search-portal/log-search-button.png)

## <a name="create-a-simple-search"></a><span data-ttu-id="d8cdb-125">Crie uma pesquisa simples</span><span class="sxs-lookup"><span data-stu-id="d8cdb-125">Create a simple search</span></span>
<span data-ttu-id="d8cdb-126">Olá tooretrieve de maneira mais rápida toowork alguns dados com é uma consulta simples que retorna todos os registros na tabela.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-126">hello quickest way tooretrieve some data toowork with is a simple query that returns all records in table.</span></span>  <span data-ttu-id="d8cdb-127">Se você tiver qualquer Windows ou Linux clientes conectados tooyour espaço de trabalho, em seguida, você terá dados em hello ou evento (Windows) ou tabela de Syslog (Linux).</span><span class="sxs-lookup"><span data-stu-id="d8cdb-127">If you have any Windows or Linux clients connected tooyour workspace, then you'll have data in either hello Event (Windows) or Syslog (Linux) table.</span></span>

<span data-ttu-id="d8cdb-128">Digite uma saudação consultas na caixa de pesquisa Olá a seguir e clique botão de pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-128">Type one hello following queries in hello search box and click hello search button.</span></span>  

```
Event
```
```
Syslog
```

<span data-ttu-id="d8cdb-129">Dados são retornados na exibição de lista padrão Olá, e você pode ver o número total de registros foram retornados.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-129">Data is returned in hello default list view, and you can see how many total records were returned.</span></span>

![Consulta simples](media/log-analytics-log-search-log-search-portal/log-search-portal-01.png)

<span data-ttu-id="d8cdb-131">Somente hello primeiro algumas propriedades de cada registro são exibidas.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-131">Only hello first few properties of each record are displayed.</span></span>  <span data-ttu-id="d8cdb-132">Clique em **Mostrar mais** toodisplay todas as propriedades de um registro específico.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-132">Click **show more** toodisplay all properties for a particular record.</span></span>

![Detalhes do registro](media/log-analytics-log-search-log-search-portal/log-search-portal-02.png)

## <a name="set-hello-time-scope"></a><span data-ttu-id="d8cdb-134">Definir o escopo de tempo de saudação</span><span class="sxs-lookup"><span data-stu-id="d8cdb-134">Set hello time scope</span></span>
<span data-ttu-id="d8cdb-135">Cada registro coletado pela análise de Log tem um **TimeGenerated** propriedade que contém Olá data e hora que esse registro Olá foi criado.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-135">Every record collected by Log Analytics has a **TimeGenerated** property that contains hello date and time that hello record was created.</span></span>  <span data-ttu-id="d8cdb-136">Uma consulta no portal de pesquisa de Log de saudação retorna somente os registros com um **TimeGenerated** no escopo de tempo de saudação que é exibido no lado esquerdo da tela hello de saudação.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-136">A query in hello Log Search portal only returns records with a **TimeGenerated** within hello time scope that's displayed on hello left side of hello screen.</span></span>  

<span data-ttu-id="d8cdb-137">Você pode alterar o filtro de tempo de saudação selecionando o menu suspenso de saudação ou modificando o controle deslizante de saudação.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-137">You can change hello time filter either by selecting hello dropdown or by modifying hello slider.</span></span>  <span data-ttu-id="d8cdb-138">controle deslizante de saudação exibe um gráfico de barras que mostra o número relativo de saudação de registros para cada segmento de tempo dentro do intervalo de saudação.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-138">hello slider displays a bar graph that shows hello relative number of records for each time segment within hello range.</span></span>  <span data-ttu-id="d8cdb-139">Este segmento irá variar dependendo de intervalo de saudação.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-139">This segment will vary depending on hello range.</span></span>

<span data-ttu-id="d8cdb-140">escopo de tempo padrão Olá é **1 dia**.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-140">hello default time scope is **1 day**.</span></span>  <span data-ttu-id="d8cdb-141">Alterar esse valor também**7 dias**, e deve aumentar o número total de saudação de registros.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-141">Change this value too**7 days**, and hello total number of records should increase.</span></span>

![Escopo de data e hora](media/log-analytics-log-search-log-search-portal/log-search-portal-03.png)

## <a name="filter-results-of-hello-query"></a><span data-ttu-id="d8cdb-143">Filtrar resultados de consulta Olá</span><span class="sxs-lookup"><span data-stu-id="d8cdb-143">Filter results of hello query</span></span>
<span data-ttu-id="d8cdb-144">Em Olá lado esquerdo da tela hello é o painel de filtro de saudação que permite que você tooadd toohello consulta de filtragem sem modificá-lo diretamente.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-144">On hello left side of hello screen is hello filter pane which allows you tooadd filtering toohello query without modifying it directly.</span></span>  <span data-ttu-id="d8cdb-145">Várias propriedades de saudação registros retornados são exibidas com seus valores de dez principais com sua contagem de registro.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-145">Several properties of hello records returned are displayed with their top ten values with their record count.</span></span>

<span data-ttu-id="d8cdb-146">Se você estiver trabalhando com **evento**, selecione Olá caixa de seleção próxima muito**erro** em **EVENTLEVELNAME**.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-146">If you're working with **Event**, select hello checkbox next too**Error** under **EVENTLEVELNAME**.</span></span>   <span data-ttu-id="d8cdb-147">Se você estiver trabalhando com **Syslog**, selecione Olá caixa de seleção próxima muito**err** em **SEVERITYLEVEL**.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-147">If you're working with **Syslog**, select hello checkbox next too**err** under **SEVERITYLEVEL**.</span></span>  <span data-ttu-id="d8cdb-148">Isso altera a consulta Olá tooone de Olá Olá toolimit a seguir resulta tooerror eventos.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-148">This changes hello query tooone of hello following toolimit hello results tooerror events.</span></span>

```
Event | where (EventLevelName == "Error")
```
```
Syslog | where (SeverityLevel == "err")
```

![Filter](media/log-analytics-log-search-log-search-portal/log-search-portal-04.png)

<span data-ttu-id="d8cdb-150">Painel de filtro de toohello adicionar propriedades selecionando **adicionar toofilters** Olá propriedade no menu de um dos registros de saudação.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-150">Add properties toohello filter pane by selecting **Add toofilters** from hello property menu on one of hello records.</span></span>

![Adicionar menu toofilter](media/log-analytics-log-search-log-search-portal/log-search-portal-02a.png)

<span data-ttu-id="d8cdb-152">Você pode definir Olá mesmo filtro selecionando **filtro** no menu de propriedade de saudação de um registro com o valor de saudação desejado toofilter.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-152">You can set hello same filter by selecting **Filter** from hello property menu for a record with hello value you want toofilter.</span></span>  

<span data-ttu-id="d8cdb-153">Você só tiver Olá **filtro** opção para propriedades com seu nome em azul.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-153">You only have hello **Filter** option for properties with their name in blue.</span></span>  <span data-ttu-id="d8cdb-154">Estes são campos *pesquisáveis* que estão indexados para as condições de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-154">These are *searchable* fields which are indexed for search conditions.</span></span>  <span data-ttu-id="d8cdb-155">Os campos em cinza são *pesquisável de texto livre* campos que têm apenas Olá **Mostrar referências** opção.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-155">Fields in grey are *free text searchable* fields which only have hello **Show references** option.</span></span>  <span data-ttu-id="d8cdb-156">Esta opção retorna registros que possuem esse valor em qualquer propriedade.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-156">This option returns records that have that value in any property.</span></span>

![Menu de filtro](media/log-analytics-log-search-log-search-portal/log-search-portal-01a.png)

<span data-ttu-id="d8cdb-158">Você pode agrupar resultados de saudação em uma única propriedade selecionando Olá **Agrupar por** opção no menu de registro de saudação.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-158">You can group hello results on a single property by selecting hello **Group by** option in hello record menu.</span></span>  <span data-ttu-id="d8cdb-159">Isso adicionará uma [resumir](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) consulta tooyour de operador que exibe os resultados de saudação em um gráfico.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-159">This will add a [summarize](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) operator tooyour query that displays hello results in a chart.</span></span>  <span data-ttu-id="d8cdb-160">Você pode agrupar em mais de uma propriedade, mas você precisaria consulta de saudação tooedit diretamente.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-160">You can group on more than one property, but you would need tooedit hello query directly.</span></span>  <span data-ttu-id="d8cdb-161">Saudação de Avançar Olá Olá selecione menu Registro **computador** propriedade e selecione **Group by 'Computer'**.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-161">Select hello record menu next hello hello **Computer** property and select **Group by 'Computer'**.</span></span>  

![Agrupar por computador](media/log-analytics-log-search-log-search-portal/log-search-portal-10.png)

## <a name="work-with-results"></a><span data-ttu-id="d8cdb-163">Trabalhar com os resultados</span><span class="sxs-lookup"><span data-stu-id="d8cdb-163">Work with results</span></span>
<span data-ttu-id="d8cdb-164">portal de pesquisa de Log de saudação tem uma variedade de recursos para trabalhar com os resultados de saudação de uma consulta.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-164">hello Log Search portal has a variety of features for working with hello results of a query.</span></span>  <span data-ttu-id="d8cdb-165">Você pode classificar, filtrar e agrupar resultados de dados de saudação do tooanalyze sem modificar a consulta real hello.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-165">You can sort, filter, and group results tooanalyze hello data without modifying hello actual query.</span></span>  <span data-ttu-id="d8cdb-166">Os resultados de uma consulta não são classificados por padrão.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-166">Results of a query are not sorted by default.</span></span>

<span data-ttu-id="d8cdb-167">saudação de tooview dados em formato de tabela que fornece opções adicionais de filtragem e classificação, clique em **tabela**.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-167">tooview hello data in table form which provides additional options for filtering and sorting, click **Table**.</span></span>  

![Exibição da tabela](media/log-analytics-log-search-log-search-portal/log-search-portal-05.png)

<span data-ttu-id="d8cdb-169">Clique em seta Olá por um detalhes de saudação tooview registro para o registro.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-169">Click hello arrow by a record tooview hello details for that record.</span></span>

![Classificar resultados](media/log-analytics-log-search-log-search-portal/log-search-portal-06.png)

<span data-ttu-id="d8cdb-171">Classifique em qualquer campo, clicando no cabeçalho de coluna.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-171">Sort on any field by clicking on its column header.</span></span>

![Classificar resultados](media/log-analytics-log-search-log-search-portal/log-search-portal-07.png)

<span data-ttu-id="d8cdb-173">Filtrar resultados de saudação em um valor específico na coluna Olá clicando no botão Filtrar hello e fornecer uma condição de filtro.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-173">Filter hello results on a specific value in hello column by clicking hello filter button and providing a filter condition.</span></span>

![Resultados do filtro](media/log-analytics-log-search-log-search-portal/log-search-portal-08.png)

<span data-ttu-id="d8cdb-175">Arrastando seu superior de toohello do cabeçalho de coluna dos resultados da saudação de grupo em uma coluna.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-175">Group on a column by dragging its column header toohello top of hello results.</span></span>  <span data-ttu-id="d8cdb-176">Você pode agrupar em vários campos arrastando a parte superior de toohello várias colunas.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-176">You can group on multiple fields by dragging multiple columns toohello top.</span></span>

![Resultados de grupo](media/log-analytics-log-search-log-search-portal/log-search-portal-09.png)



## <a name="work-with-performance-data"></a><span data-ttu-id="d8cdb-178">Trabalhe com dados de desempenho</span><span class="sxs-lookup"><span data-stu-id="d8cdb-178">Work with performance data</span></span>
<span data-ttu-id="d8cdb-179">Dados de desempenho para os agentes do Windows e Linux são armazenados no espaço de trabalho de análise de Log de saudação em Olá **Perf** tabela.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-179">Performance data for both Windows and Linux agents is stored in hello Log Analytics workspace in hello **Perf** table.</span></span>  <span data-ttu-id="d8cdb-180">Os registros de desempenho são semelhante a qualquer outro registro e é possível gravar uma consulta simples que retorna todos os registros de desempenho, assim como eventos.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-180">Performance records look just like any other record, and we can write a simple query that returns all performance records just like with events.</span></span>

```
Perf
```

![Dados de desempenho](media/log-analytics-log-search-log-search-portal/log-search-portal-11.png)

<span data-ttu-id="d8cdb-182">Retornando milhões de registros para todos contadores e objetos de desempenho, porém, não é muito útil.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-182">Returning millions of records for all performance objects and counters though isn't very useful.</span></span>  <span data-ttu-id="d8cdb-183">Você pode usar o hello mesmos métodos usados acima dados de saudação toofilter ou simplesmente digite Olá seguinte consulta diretamente na caixa de pesquisa de log de saudação.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-183">You can use hello same methods you used above toofilter hello data or just type hello following query directly into hello log search box.</span></span>  <span data-ttu-id="d8cdb-184">Isso retorna somente os registros de utilização do processador para computadores Windows e Linux.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-184">This returns only processor utilization records for both Windows and Linux computers.</span></span>

```
Perf | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time")
```

![Utilização do processador](media/log-analytics-log-search-log-search-portal/log-search-portal-12.png)

<span data-ttu-id="d8cdb-186">Isso limita o contador específico da saudação dados tooa, mas ela ainda não colocá-la em um formulário que é particularmente útil.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-186">This limits hello data tooa particular counter, but it still doesn't put it in a form that's particularly useful.</span></span>  <span data-ttu-id="d8cdb-187">Você pode exibir dados de saudação em um gráfico de linhas, mas primeiro é necessário toogroup-lo por computador e TimeGenerated.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-187">You can display hello data in a line chart, but first need toogroup it by Computer and TimeGenerated.</span></span>  <span data-ttu-id="d8cdb-188">toogroup em vários campos, você precisa de consulta de saudação do toomodify diretamente, para modificar a seguir Olá consulta toohello.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-188">toogroup on multiple fields, you need toomodify hello query directly, so modify hello query toohello following.</span></span>  <span data-ttu-id="d8cdb-189">Isso usa Olá [avg](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) função hello **CounterValue** valor médio da propriedade toocalculate Olá cada hora.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-189">This uses hello [avg](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) function on hello **CounterValue** property toocalculate hello average value over each hour.</span></span>

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated
```

![Gráfico de dados de desempenho](media/log-analytics-log-search-log-search-portal/log-search-portal-13.png)

<span data-ttu-id="d8cdb-191">Agora que os dados de saudação adequadamente são agrupados, você pode exibi-lo em um gráfico de visual adicionando Olá [renderizar](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator) operador.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-191">Now that hello data is suitably grouped, you can display it in a visual chart by adding hello [render](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator) operator.</span></span>  

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated | render timechart
```

![Gráfico de Linhas](media/log-analytics-log-search-log-search-portal/log-search-portal-14.png)

## <a name="next-steps"></a><span data-ttu-id="d8cdb-193">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d8cdb-193">Next steps</span></span>

- <span data-ttu-id="d8cdb-194">Saiba mais sobre a linguagem de consulta de análise de Log de saudação em [guia de Introdução com hello Portal da análise de](https://go.microsoft.com/fwlink/?linkid=856079).</span><span class="sxs-lookup"><span data-stu-id="d8cdb-194">Learn more about hello Log Analytics query language at [Getting Started with hello Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856079).</span></span>
- <span data-ttu-id="d8cdb-195">Percorrer um tutorial usando Olá [portal Advanced Analytics](https://go.microsoft.com/fwlink/?linkid=856587) que permite a você toorun Olá mesmo consultas e acesso Olá mesmos dados que o portal de pesquisa de Log de saudação.</span><span class="sxs-lookup"><span data-stu-id="d8cdb-195">Walk through a tutorial using hello [Advanced Analytics portal](https://go.microsoft.com/fwlink/?linkid=856587) which allows you toorun hello same queries and access hello same data as hello Log Search portal.</span></span>
