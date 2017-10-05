---
title: "Análise de desempenho de consultas para o Banco de dados SQL do Azure | Microsoft Docs"
description: O monitoramento do desempenho de consulta identifica as consultas que consumem mais CPU de um Banco de Dados SQL do Azure.
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: c2f580b2-3835-453f-89f5-140e02dd2ea7
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 1925d4ff8f5b16a0df56de987f8653cfd8441c52
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-sql-database-query-performance-insight"></a><span data-ttu-id="f4a75-103">Visão do desempenho de consulta de Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="f4a75-103">Azure SQL Database Query Performance Insight</span></span>
<span data-ttu-id="f4a75-104">Gerenciamento e ajuste do desempenho de bancos de dados relacionais são uma tarefa desafiadora que requer conhecimento significativo e investimento de tempo.</span><span class="sxs-lookup"><span data-stu-id="f4a75-104">Managing and tuning the performance of relational databases is a challenging task that requires significant expertise and time investment.</span></span> <span data-ttu-id="f4a75-105">A Análise de Desempenho de Consultas permite que você gaste menos tempo solucionando problemas de desempenho de banco de dados, fornecendo o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f4a75-105">Query Performance Insight allows you to spend less time troubleshooting database performance by providing the following:</span></span>

* <span data-ttu-id="f4a75-106">Mais informações sobre o consumo de recursos de bancos de dados (DTU).</span><span class="sxs-lookup"><span data-stu-id="f4a75-106">Deeper insight into your databases resource (DTU) consumption.</span></span> 
* <span data-ttu-id="f4a75-107">As principais consultas por contagem de CPU/Duração/Execução, que potencialmente podem ser ajustadas para melhorar o desempenho.</span><span class="sxs-lookup"><span data-stu-id="f4a75-107">The top queries by CPU/Duration/Execution count, which can potentially be tuned for improved performance.</span></span>
* <span data-ttu-id="f4a75-108">A capacidade de analisar os detalhes de uma consulta, exibir o texto e o histórico de utilização de recursos.</span><span class="sxs-lookup"><span data-stu-id="f4a75-108">The ability to drill down into the details of a query, view its text and history of resource utilization.</span></span> 
* <span data-ttu-id="f4a75-109">Anotações de ajuste de desempenho que mostram as ações executadas [Advisor do Banco de Dados SQL Azure](sql-database-advisor.md)</span><span class="sxs-lookup"><span data-stu-id="f4a75-109">Performance tuning annotations that show actions performed by [SQL Azure Database Advisor](sql-database-advisor.md)</span></span>  



## <a name="prerequisites"></a><span data-ttu-id="f4a75-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f4a75-110">Prerequisites</span></span>
* <span data-ttu-id="f4a75-111">A Análise de Desempenho de Consultas exige a execução do [Repositório de Consultas](https://msdn.microsoft.com/library/dn817826.aspx) em seu banco de dados.</span><span class="sxs-lookup"><span data-stu-id="f4a75-111">Query Performance Insight requires that [Query Store](https://msdn.microsoft.com/library/dn817826.aspx) is active on your database.</span></span> <span data-ttu-id="f4a75-112">Se o Repositório de Consultas não estiver em execução, o portal solicitará que você o ative.</span><span class="sxs-lookup"><span data-stu-id="f4a75-112">If Query Store is not running, the portal prompts you to turn it on.</span></span>

## <a name="permissions"></a><span data-ttu-id="f4a75-113">Permissões</span><span class="sxs-lookup"><span data-stu-id="f4a75-113">Permissions</span></span>
<span data-ttu-id="f4a75-114">As seguintes permissões de [controle de acesso baseado em função](../active-directory/role-based-access-control-what-is.md) são necessárias para usar a Visão do Desempenho de Consulta:</span><span class="sxs-lookup"><span data-stu-id="f4a75-114">The following [role-based access control](../active-directory/role-based-access-control-what-is.md) permissions are required to use Query Performance Insight:</span></span> 

* <span data-ttu-id="f4a75-115">As permissões **Leitor**, **Proprietário**, **Colaborador**, **Colaborador do Banco de Dados SQL** ou **Colaborador do SQL Server** são necessárias para exibir as consultas e gráficos que consomem mais recursos.</span><span class="sxs-lookup"><span data-stu-id="f4a75-115">**Reader**, **Owner**, **Contributor**, **SQL DB Contributor**, or **SQL Server Contributor** permissions are required to view the top resource consuming queries and charts.</span></span> 
* <span data-ttu-id="f4a75-116">As permissões **Proprietário**, **Colaborador**, **Colaborador do Banco de Dados SQL** ou **Colaborador do SQL Server** são necessárias para exibir o texto da consulta.</span><span class="sxs-lookup"><span data-stu-id="f4a75-116">**Owner**, **Contributor**, **SQL DB Contributor**, or **SQL Server Contributor** permissions are required to view query text.</span></span>

## <a name="using-query-performance-insight"></a><span data-ttu-id="f4a75-117">Usando a Visão de Desempenho de Consulta</span><span class="sxs-lookup"><span data-stu-id="f4a75-117">Using Query Performance Insight</span></span>
<span data-ttu-id="f4a75-118">A Visão do Desempenho de Consulta é fácil de usar:</span><span class="sxs-lookup"><span data-stu-id="f4a75-118">Query Performance Insight is easy to use:</span></span>

* <span data-ttu-id="f4a75-119">Abra o [portal do Azure](https://portal.azure.com/) e localize o banco de dados de localização que você deseja examinar.</span><span class="sxs-lookup"><span data-stu-id="f4a75-119">Open [Azure portal](https://portal.azure.com/) and find database that you want to examine.</span></span> 
  * <span data-ttu-id="f4a75-120">No menu do lado esquerdo, em suporte e solução de problemas, selecione "Análise de Desempenho de Consultas".</span><span class="sxs-lookup"><span data-stu-id="f4a75-120">From left-hand side menu, under support and troubleshooting, select “Query Performance Insight”.</span></span>
* <span data-ttu-id="f4a75-121">Na primeira guia, examine a lista das consultas que consomem mais recursos.</span><span class="sxs-lookup"><span data-stu-id="f4a75-121">On the first tab, review the list of top resource-consuming queries.</span></span>
* <span data-ttu-id="f4a75-122">Escolha uma consulta individual para exibir seus detalhes.</span><span class="sxs-lookup"><span data-stu-id="f4a75-122">Select an individual query to view its details.</span></span>
* <span data-ttu-id="f4a75-123">Abra o [Advisor do Banco de Dados do SQL Azure](sql-database-advisor.md) e verifique se há alguma recomendação disponível.</span><span class="sxs-lookup"><span data-stu-id="f4a75-123">Open [SQL Azure Database Advisor](sql-database-advisor.md) and check if any recommendations are available.</span></span>
* <span data-ttu-id="f4a75-124">Use os controles deslizantes ou os ícones de zoom para alterar o intervalo observado.</span><span class="sxs-lookup"><span data-stu-id="f4a75-124">Use sliders or zoom icons to change observed interval.</span></span>
  
    ![painel de desempenho](./media/sql-database-query-performance/performance.png)

> [!NOTE]
> <span data-ttu-id="f4a75-126">São necessárias duas horas de dados a serem capturados pelo Repositório de Consulta para fornecer as análises de desempenho de consultas no banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="f4a75-126">A couple hours of data needs to be captured by Query Store for SQL Database to provide query performance insights.</span></span> <span data-ttu-id="f4a75-127">Se o banco de dados não tem atividades ou o Armazenamento de Consulta não estava ativo durante um determinado período de tempo, os gráficos estarão vazios ao exibir o período de tempo.</span><span class="sxs-lookup"><span data-stu-id="f4a75-127">If the database has no activity or Query Store was not active during a certain time period, the charts will be empty when displaying that time period.</span></span> <span data-ttu-id="f4a75-128">Você pode habilitar o Armazenamento de Consulta a qualquer momento se ele não estiver em execução.</span><span class="sxs-lookup"><span data-stu-id="f4a75-128">You may enable Query Store at any time if it is not running.</span></span>   
> 
> 

## <a name="review-top-cpu-consuming-queries"></a><span data-ttu-id="f4a75-129">Examinar as consultas que mais consomem CPU</span><span class="sxs-lookup"><span data-stu-id="f4a75-129">Review top CPU consuming queries</span></span>
<span data-ttu-id="f4a75-130">No [portal](http://portal.azure.com) , faça o descrito a seguir:</span><span class="sxs-lookup"><span data-stu-id="f4a75-130">In the [portal](http://portal.azure.com) do the following:</span></span>

1. <span data-ttu-id="f4a75-131">Navegue até um banco de dados SQL e clique em **Todas as configurações** > **Suporte + Solução de problemas** > **Análise de desempenho de consultas**.</span><span class="sxs-lookup"><span data-stu-id="f4a75-131">Browse to a SQL database and click **All settings** > **Support + Troubleshooting** > **Query performance insight**.</span></span> 
   
    ![Análise de desempenho de consultas][1]
   
    <span data-ttu-id="f4a75-133">A exibição das principais consultas é aberta e as consultas que consomem mais CPU são listadas.</span><span class="sxs-lookup"><span data-stu-id="f4a75-133">The top queries view opens and the top CPU consuming queries are listed.</span></span>
2. <span data-ttu-id="f4a75-134">Clique em torno do gráfico para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="f4a75-134">Click around the chart for details.</span></span><br><span data-ttu-id="f4a75-135">A linha superior mostra a % de DTU geral do banco de dados, enquanto as barras mostram a % de CPU consumida pelas consultas selecionadas durante o intervalo escolhido (por exemplo, se **Semana passada** for escolhida, cada barra representará um dia).</span><span class="sxs-lookup"><span data-stu-id="f4a75-135">The top line shows overall DTU% for the database, while the bars show CPU% consumed by the selected queries during the selected interval (for example, if **Past week** is selected each bar represents one day).</span></span>
   
    ![principais consultas][2]
   
    <span data-ttu-id="f4a75-137">A grade inferior representa informações agregadas das consultas visíveis.</span><span class="sxs-lookup"><span data-stu-id="f4a75-137">The bottom grid represents aggregated information for the visible queries.</span></span>
   
   * <span data-ttu-id="f4a75-138">ID da consulta: identificador exclusivo da consulta no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="f4a75-138">Query ID - unique identifier of query inside database.</span></span>
   * <span data-ttu-id="f4a75-139">CPU por consulta durante o intervalo observável (depende da função de agregação).</span><span class="sxs-lookup"><span data-stu-id="f4a75-139">CPU per query during observable interval (depends on aggregation function).</span></span>
   * <span data-ttu-id="f4a75-140">Duração por consulta (depende da função de agregação).</span><span class="sxs-lookup"><span data-stu-id="f4a75-140">Duration per query (depends on aggregation function).</span></span>
   * <span data-ttu-id="f4a75-141">Número total de execuções para uma consulta específica.</span><span class="sxs-lookup"><span data-stu-id="f4a75-141">Total number of executions for a particular query.</span></span>
     
     <span data-ttu-id="f4a75-142">Marque ou desmarque as consultas individuais para incluir ou exclui-las do gráfico usando as caixas de seleção.</span><span class="sxs-lookup"><span data-stu-id="f4a75-142">Select or clear individual queries to include or exclude them from the chart using checkboxes.</span></span>
3. <span data-ttu-id="f4a75-143">Se os dados se tornarem obsoletos, clique no botão **Atualizar** .</span><span class="sxs-lookup"><span data-stu-id="f4a75-143">If your data becomes stale, click the **Refresh** button.</span></span>
4. <span data-ttu-id="f4a75-144">Você pode usar os controles deslizantes e os botões de zoom para alterar o intervalo de observação e investigar os picos: ![configurações](./media/sql-database-query-performance/zoom.png)</span><span class="sxs-lookup"><span data-stu-id="f4a75-144">You can use sliders and zoom buttons to change observation interval and investigate spikes:  ![settings](./media/sql-database-query-performance/zoom.png)</span></span>
5. <span data-ttu-id="f4a75-145">Opcionalmente, se você quiser uma exibição diferente, você pode selecionar a guia **Personalizar** e definir:</span><span class="sxs-lookup"><span data-stu-id="f4a75-145">Optionally, if you want a different view, you can select **Custom** tab and set:</span></span>
   
   * <span data-ttu-id="f4a75-146">Métrica (CPU, duração, contagem de execução)</span><span class="sxs-lookup"><span data-stu-id="f4a75-146">Metric (CPU, duration, execution count)</span></span>
   * <span data-ttu-id="f4a75-147">Intervalo de tempo (Últimas 24 horas, Última semana, Mês passado).</span><span class="sxs-lookup"><span data-stu-id="f4a75-147">Time interval (Last 24 hours, Past week, Past month).</span></span> 
   * <span data-ttu-id="f4a75-148">Número de consultas.</span><span class="sxs-lookup"><span data-stu-id="f4a75-148">Number of queries.</span></span>
   * <span data-ttu-id="f4a75-149">Função de agregação.</span><span class="sxs-lookup"><span data-stu-id="f4a75-149">Aggregation function.</span></span>
     
     ![Configurações](./media/sql-database-query-performance/custom-tab.png)

## <a name="viewing-individual-query-details"></a><span data-ttu-id="f4a75-151">Exibindo detalhes de uma consulta individual</span><span class="sxs-lookup"><span data-stu-id="f4a75-151">Viewing individual query details</span></span>
<span data-ttu-id="f4a75-152">Para exibir detalhes da consulta:</span><span class="sxs-lookup"><span data-stu-id="f4a75-152">To view query details:</span></span>

1. <span data-ttu-id="f4a75-153">Clique em qualquer consulta na lista de consultas principais.</span><span class="sxs-lookup"><span data-stu-id="f4a75-153">Click any query in the list of top queries.</span></span>
   
    ![detalhes](./media/sql-database-query-performance/details.png)
2. <span data-ttu-id="f4a75-155">A exibição de detalhes é aberta e o consumo de CPU/Duração/Contagem de execução de consultas é dividido ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="f4a75-155">The details view opens and the queries CPU consumption/Duration/Execution count is broken down over time.</span></span>
3. <span data-ttu-id="f4a75-156">Clique em torno do gráfico para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="f4a75-156">Click around the chart for details.</span></span>
   
   * <span data-ttu-id="f4a75-157">O gráfico superior mostra a linha com a % de DTU do banco de dados geral e as barras são a % de CPU consumida pela consulta selecionada.</span><span class="sxs-lookup"><span data-stu-id="f4a75-157">Top chart shows line with overall database DTU%, and the bars are CPU% consumed by the selected query.</span></span>
   * <span data-ttu-id="f4a75-158">O segundo gráfico mostra a duração total pela consulta selecionada.</span><span class="sxs-lookup"><span data-stu-id="f4a75-158">Second chart shows total duration by the selected query.</span></span>
   * <span data-ttu-id="f4a75-159">O gráfico na parte inferior mostra o número total de execuções pela consulta selecionada.</span><span class="sxs-lookup"><span data-stu-id="f4a75-159">Bottom chart shows total number of executions by the selected query.</span></span>
     
     ![detalhes da consulta][3]
4. <span data-ttu-id="f4a75-161">Opcionalmente, use os controles deslizantes, os botões de zoom ou clique em **Configurações** para personalizar a exibição dos dados de consumo de CPU ou escolher um período de tempo diferente.</span><span class="sxs-lookup"><span data-stu-id="f4a75-161">Optionally, use sliders, zoom buttons or click **Settings** to customize how query data is displayed, or to pick a different time period.</span></span>

## <a name="review-top-queries-per-duration"></a><span data-ttu-id="f4a75-162">Analise as principais consultas por duração</span><span class="sxs-lookup"><span data-stu-id="f4a75-162">Review top queries per duration</span></span>
<span data-ttu-id="f4a75-163">Na atualização recente da Análise de Desempenho de Consultas, apresentamos duas novas métricas que podem ajudar a identificar possíveis afunilamentos: duração e contagem de execução.</span><span class="sxs-lookup"><span data-stu-id="f4a75-163">In the recent update of Query Performance Insight, we introduced two new metrics that can help you identify potential bottlenecks: duration and execution count.</span></span><br>

<span data-ttu-id="f4a75-164">Consultas de longa execução tem o maior potencial para bloquear recursos por mais tempo, bloqueando outros usuários e limitando a escalabilidade.</span><span class="sxs-lookup"><span data-stu-id="f4a75-164">Long-running queries have the greatest potential for locking resources longer, blocking other users, and limiting scalability.</span></span> <span data-ttu-id="f4a75-165">Elas também são as melhores candidatas para otimização.</span><span class="sxs-lookup"><span data-stu-id="f4a75-165">They are also the best candidates for optimization.</span></span><br>

<span data-ttu-id="f4a75-166">Para identificar consultas de longa execução:</span><span class="sxs-lookup"><span data-stu-id="f4a75-166">To identify long running queries:</span></span>

1. <span data-ttu-id="f4a75-167">Abra a guia **Personalizar** na Análise de Desempenho de Consultas do banco de dados selecionado</span><span class="sxs-lookup"><span data-stu-id="f4a75-167">Open **Custom** tab in Query Performance Insight for selected database</span></span>
2. <span data-ttu-id="f4a75-168">Altere as métricas para **duração**</span><span class="sxs-lookup"><span data-stu-id="f4a75-168">Change metrics to be **duration**</span></span>
3. <span data-ttu-id="f4a75-169">Selecione o número de consultas e o intervalo de observação</span><span class="sxs-lookup"><span data-stu-id="f4a75-169">Select number of queries and observation interval</span></span>
4. <span data-ttu-id="f4a75-170">Selecione a função de agregação</span><span class="sxs-lookup"><span data-stu-id="f4a75-170">Select aggregation function</span></span>
   
   * <span data-ttu-id="f4a75-171">**Soma** adiciona todo o tempo de execução de consulta durante todo o intervalo de observação.</span><span class="sxs-lookup"><span data-stu-id="f4a75-171">**Sum** adds up all query execution time during whole observation interval.</span></span>
   * <span data-ttu-id="f4a75-172">**Máximo** localiza consultas para as quais tempo de execução foi máximo no intervalo inteiro de observação.</span><span class="sxs-lookup"><span data-stu-id="f4a75-172">**Max** finds queries which execution time was maximum at whole observation interval.</span></span>
   * <span data-ttu-id="f4a75-173">**Média** encontra a média de tempo de execução de todas as execuções de consulta e mostra a você as primeiras entre essas médias.</span><span class="sxs-lookup"><span data-stu-id="f4a75-173">**Avg** finds average execution time of all query executions and show you the top out of these averages.</span></span> 
     
     ![duração da consulta][4]

## <a name="review-top-queries-per-execution-count"></a><span data-ttu-id="f4a75-175">Analise as principais consultas por contagem de execução</span><span class="sxs-lookup"><span data-stu-id="f4a75-175">Review top queries per execution count</span></span>
<span data-ttu-id="f4a75-176">Um alto número de execuções pode não estar afetando o banco de dados propriamente dito e o uso de recursos pode ser baixo, mas o aplicativo pode ficar lento no geral.</span><span class="sxs-lookup"><span data-stu-id="f4a75-176">High number of executions might not be affecting database itself and resources usage can be low, but overall application might get slow.</span></span>

<span data-ttu-id="f4a75-177">Em alguns casos, a contagem de execução muito alta pode levar a um aumento das viagens de ida e volta na rede.</span><span class="sxs-lookup"><span data-stu-id="f4a75-177">In some cases, very high execution count may lead to increase of network round trips.</span></span> <span data-ttu-id="f4a75-178">Viagens de ida e afetam o desempenho de forma significativa.</span><span class="sxs-lookup"><span data-stu-id="f4a75-178">Round trips significantly affect performance.</span></span> <span data-ttu-id="f4a75-179">Elas estão sujeitas à latência de rede e à latência do servidor downstream.</span><span class="sxs-lookup"><span data-stu-id="f4a75-179">They are subject to network latency and to downstream server latency.</span></span> 

<span data-ttu-id="f4a75-180">Por exemplo, muitos sites orientados a dados acessam bastante o banco de dados para cada solicitação do usuário.</span><span class="sxs-lookup"><span data-stu-id="f4a75-180">For example, many data-driven Web sites heavily access the database for every user request.</span></span> <span data-ttu-id="f4a75-181">Apesar do pool de conexões ajudar, o maior tráfego de rede e a maior carga de processamento no servidor de banco de dados podem prejudicar o desempenho.</span><span class="sxs-lookup"><span data-stu-id="f4a75-181">While connection pooling helps, the increased network traffic and processing load on the database server can adversely affect performance.</span></span>  <span data-ttu-id="f4a75-182">A orientação geral é manter a menor quantidade possível de viagens de ida e volta.</span><span class="sxs-lookup"><span data-stu-id="f4a75-182">General advice is to keep round trips to an absolute minimum.</span></span>

<span data-ttu-id="f4a75-183">Para identificar consultas executadas com frequência, consultas ("tagarelas"):</span><span class="sxs-lookup"><span data-stu-id="f4a75-183">To identify frequently executed queries (“chatty”) queries:</span></span>

1. <span data-ttu-id="f4a75-184">Abra a guia **Personalizar** na Análise de Desempenho de Consultas do banco de dados selecionado</span><span class="sxs-lookup"><span data-stu-id="f4a75-184">Open **Custom** tab in Query Performance Insight for selected database</span></span>
2. <span data-ttu-id="f4a75-185">Altere as métricas para **contagem de execução**</span><span class="sxs-lookup"><span data-stu-id="f4a75-185">Change metrics to be **execution count**</span></span>
3. <span data-ttu-id="f4a75-186">Selecione o número de consultas e o intervalo de observação</span><span class="sxs-lookup"><span data-stu-id="f4a75-186">Select number of queries and observation interval</span></span>
   
    ![contagem de execução da consulta][5]

## <a name="understanding-performance-tuning-annotations"></a><span data-ttu-id="f4a75-188">Noções básicas sobre anotações de ajuste de desempenho</span><span class="sxs-lookup"><span data-stu-id="f4a75-188">Understanding performance tuning annotations</span></span>
<span data-ttu-id="f4a75-189">Ao explorar a carga de trabalho na Análise de Desempenho de Consultas, você pode notar ícones com uma linha vertical na parte superior do gráfico.</span><span class="sxs-lookup"><span data-stu-id="f4a75-189">While exploring your workload in Query Performance Insight, you might notice icons with vertical line on top of the chart.</span></span><br>

<span data-ttu-id="f4a75-190">Esses ícones são anotações; eles representam as ações que afetam o desempenho executadas pelo [Advisor do Banco de Dados SQL Azure](sql-database-advisor.md).</span><span class="sxs-lookup"><span data-stu-id="f4a75-190">These icons are annotations; they represent performance affecting actions performed by [SQL Azure Database Advisor](sql-database-advisor.md).</span></span> <span data-ttu-id="f4a75-191">Passando com o mouse sobre a anotação, você obtém informações básicas sobre a ação:</span><span class="sxs-lookup"><span data-stu-id="f4a75-191">By hovering annotation, you get basic information about the action:</span></span>

![anotação da consulta][6]

<span data-ttu-id="f4a75-193">Se você quiser saber mais ou aplicar a recomendação do Advisor, clique no ícone.</span><span class="sxs-lookup"><span data-stu-id="f4a75-193">If you want to know more or apply advisor recommendation, click the icon.</span></span> <span data-ttu-id="f4a75-194">O ícone abrirá os detalhes da ação.</span><span class="sxs-lookup"><span data-stu-id="f4a75-194">It will open details of action.</span></span> <span data-ttu-id="f4a75-195">Se for uma recomendação ativa, você pode aplicar imediatamente usando o comando.</span><span class="sxs-lookup"><span data-stu-id="f4a75-195">If it’s an active recommendation you can apply it straight away using command.</span></span>

![detalhes de anotação de consulta][7]

### <a name="multiple-annotations"></a><span data-ttu-id="f4a75-197">Várias anotações.</span><span class="sxs-lookup"><span data-stu-id="f4a75-197">Multiple annotations.</span></span>
<span data-ttu-id="f4a75-198">É possível, que por causa do nível de zoom, anotações que estão próximas umas às outras serão recolhidas em somente uma anotação.</span><span class="sxs-lookup"><span data-stu-id="f4a75-198">It’s possible, that because of zoom level, annotations that are close to each other will get collapsed into one.</span></span> <span data-ttu-id="f4a75-199">Isso será representado por um ícone especial, clicar nele irá abrirá uma nova folha onde a lista de anotações agrupadas será mostrada.</span><span class="sxs-lookup"><span data-stu-id="f4a75-199">This will be represented by special icon, clicking it will open new blade where list of grouped annotations will be shown.</span></span>
<span data-ttu-id="f4a75-200">Correlacionar consultas e ações de ajuste de desempenho pode ajudar a compreender melhor a sua carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="f4a75-200">Correlating queries and performance tuning actions can help to better understand your workload.</span></span> 

## <a name="optimizing-the-query-store-configuration-for-query-performance-insight"></a><span data-ttu-id="f4a75-201">Otimizando a configuração do Repositório de Consultas para Análise de Desempenho de Consultas</span><span class="sxs-lookup"><span data-stu-id="f4a75-201">Optimizing the Query Store configuration for Query Performance Insight</span></span>
<span data-ttu-id="f4a75-202">Durante o uso da Análise de Desempenho de Consultas, você poderá encontrar as seguintes mensagens do Repositório de Consultas:</span><span class="sxs-lookup"><span data-stu-id="f4a75-202">During your use of Query Performance Insight, you might encounter the following Query Store messages:</span></span>

* <span data-ttu-id="f4a75-203">"O Repositório de Consulta não está corretamente configurado neste banco de dados.</span><span class="sxs-lookup"><span data-stu-id="f4a75-203">"Query Store is not properly configured on this database.</span></span> <span data-ttu-id="f4a75-204">Clique aqui para saber mais."</span><span class="sxs-lookup"><span data-stu-id="f4a75-204">Click here to learn more."</span></span>
* <span data-ttu-id="f4a75-205">"O Repositório de Consulta não está corretamente configurado neste banco de dados.</span><span class="sxs-lookup"><span data-stu-id="f4a75-205">"Query Store is not properly configured on this database.</span></span> <span data-ttu-id="f4a75-206">Clique aqui para alterar as configurações."</span><span class="sxs-lookup"><span data-stu-id="f4a75-206">Click here to change settings."</span></span> 

<span data-ttu-id="f4a75-207">Normalmente, essas mensagens aparecem quando o Repositório de Consultas não está apto a coletar novos dados.</span><span class="sxs-lookup"><span data-stu-id="f4a75-207">These messages usually appear when Query Store is not able to collect new data.</span></span> 

<span data-ttu-id="f4a75-208">O primeiro caso ocorre quando o Repositório de Consultas está em estado somente leitura e os parâmetros são definidos de forma ideal.</span><span class="sxs-lookup"><span data-stu-id="f4a75-208">First case happens when Query Store is in Read-Only state and parameters are set optimally.</span></span> <span data-ttu-id="f4a75-209">Você pode corrigir isso, aumentando o tamanho do Repositório de Consultas ou desmarcando o Repositório de Consultas.</span><span class="sxs-lookup"><span data-stu-id="f4a75-209">You can fix this by increasing size of Query Store or clearing Query Store.</span></span>

![botão qds][8]

<span data-ttu-id="f4a75-211">O segundo caso acontece quando o Repositório de Consultas está Desligado ou parâmetros não estão definidos de forma ideal.</span><span class="sxs-lookup"><span data-stu-id="f4a75-211">Second case happens when Query Store is Off or parameters aren’t set optimally.</span></span> <br><span data-ttu-id="f4a75-212">Você pode alterar a política de Retenção e Captura e habilitar o Repositório de Consultas, executando os comandos a seguir ou diretamente do portal:</span><span class="sxs-lookup"><span data-stu-id="f4a75-212">You can change the Retention and Capture policy and enable Query Store by executing commands below or directly from portal:</span></span>

![botão qds][9]

### <a name="recommended-retention-and-capture-policy"></a><span data-ttu-id="f4a75-214">Política recomendada de retenção e captura</span><span class="sxs-lookup"><span data-stu-id="f4a75-214">Recommended retention and capture policy</span></span>
<span data-ttu-id="f4a75-215">Há dois tipos de política de retenção:</span><span class="sxs-lookup"><span data-stu-id="f4a75-215">There are two types of retention policies:</span></span>

* <span data-ttu-id="f4a75-216">Baseada em tamanho — se definida para AUTOMÁTICA, ela limpará os dados automaticamente quando o tamanho máximo estiver perto de ser atingido.</span><span class="sxs-lookup"><span data-stu-id="f4a75-216">Size based - if set to AUTO it will clean data automatically when near max size is reached.</span></span>
* <span data-ttu-id="f4a75-217">Baseada no tempo — por padrão, nós a definiremos para 30 dias, o que significa que, se o Repositório de Consultas ficar sem espaço, ele excluirá informações de consulta com mais de 30 dias</span><span class="sxs-lookup"><span data-stu-id="f4a75-217">Time based - by default we will set it to 30 days, which means, if Query Store will run out of space, it will delete query information older than 30 days</span></span>

<span data-ttu-id="f4a75-218">A política de captura pode ser definida para:</span><span class="sxs-lookup"><span data-stu-id="f4a75-218">Capture policy could be set to:</span></span>

* <span data-ttu-id="f4a75-219">**Todas**: captura todas as consultas.</span><span class="sxs-lookup"><span data-stu-id="f4a75-219">**All** - Captures all queries.</span></span>
* <span data-ttu-id="f4a75-220">**Automática**: consultas pouco frequentes e consultas com duração de execução e compilação insignificantes são ignoradas.</span><span class="sxs-lookup"><span data-stu-id="f4a75-220">**Auto** - Infrequent queries and queries with insignificant compile and execution duration are ignored.</span></span> <span data-ttu-id="f4a75-221">Os limites da duração de contagem de execução, compilação e tempo de execução são determinados internamente.</span><span class="sxs-lookup"><span data-stu-id="f4a75-221">Thresholds for execution count, compile and runtime duration are internally determined.</span></span> <span data-ttu-id="f4a75-222">Essa é a opção padrão.</span><span class="sxs-lookup"><span data-stu-id="f4a75-222">This is the default option.</span></span>
* <span data-ttu-id="f4a75-223">**Nenhuma** – o Repositório de Consultas interrompe a captura de novas consultas, porém, as estatísticas de tempo de execução para consultas já capturadas ainda são coletadas.</span><span class="sxs-lookup"><span data-stu-id="f4a75-223">**None** - Query Store stops capturing new queries, however runtime stats for already captured queries are still collected.</span></span>

<span data-ttu-id="f4a75-224">É recomendável definir todas as políticas para AUTOMÁTICA e a limpeza de políticas para 30 dias:</span><span class="sxs-lookup"><span data-stu-id="f4a75-224">We recommend setting all policies to AUTO and clean policy to 30 days:</span></span>

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (SIZE_BASED_CLEANUP_MODE = AUTO);

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 30));

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (QUERY_CAPTURE_MODE = AUTO);

<span data-ttu-id="f4a75-225">Aumente o tamanho do Repositório de Consultas.</span><span class="sxs-lookup"><span data-stu-id="f4a75-225">Increase size of Query Store.</span></span> <span data-ttu-id="f4a75-226">Essa ação pode ser realizada conectando-se a um banco de dados e emitindo a seguinte consulta:</span><span class="sxs-lookup"><span data-stu-id="f4a75-226">This could be performed by connecting to a database and issuing following query:</span></span>

    ALTER DATABASE [YourDB]
    SET QUERY_STORE (MAX_STORAGE_SIZE_MB = 1024);

<span data-ttu-id="f4a75-227">Aplicar essas configurações eventualmente fará o Repositório de Consultas coletar novas consultas, no entanto, se você não quiser esperar, você pode limpar o Repositório de Consultas.</span><span class="sxs-lookup"><span data-stu-id="f4a75-227">Applying these settings will eventually make Query Store collecting new queries, however if you don’t want to wait you can clear Query Store.</span></span> 

> [!NOTE]
> <span data-ttu-id="f4a75-228">A execução da consulta a seguir excluirá todas as informações atuais no Repositório de Consultas.</span><span class="sxs-lookup"><span data-stu-id="f4a75-228">Executing following query will delete all current information in the Query Store.</span></span> 
> 
> 

    ALTER DATABASE [YourDB] SET QUERY_STORE CLEAR;


## <a name="summary"></a><span data-ttu-id="f4a75-229">Resumo</span><span class="sxs-lookup"><span data-stu-id="f4a75-229">Summary</span></span>
<span data-ttu-id="f4a75-230">A Visão do Desempenho de Consulta ajuda a entender o impacto de sua carga de trabalho de consulta e como ela se relaciona com o consumo de recursos do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="f4a75-230">Query Performance Insight helps you understand the impact of your query workload and how it relates to database resource consumption.</span></span> <span data-ttu-id="f4a75-231">Com esse recurso, você saberá mais sobre as consultas que consomem mais recursos e identificará facilmente as que devem ser corrigidas antes que as mesmas se tornem um problema.</span><span class="sxs-lookup"><span data-stu-id="f4a75-231">With this feature, you will learn about the top consuming queries, and easily identify the ones to fix before they become a problem.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4a75-232">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f4a75-232">Next steps</span></span>
<span data-ttu-id="f4a75-233">Para obter recomendações adicionais sobre como aprimorar o desempenho do seu banco de dados SQL, clique em [Recomendações](sql-database-advisor.md) na folha **Análise de Desempenho de Consultas** .</span><span class="sxs-lookup"><span data-stu-id="f4a75-233">For additional recommendations about improving the performance of your SQL database, click [Recommendations](sql-database-advisor.md) on the **Query Performance Insight** blade.</span></span>

![Performance Advisor](./media/sql-database-query-performance/ia.png)

<!--Image references-->
[1]: ./media/sql-database-query-performance/tile.png
[2]: ./media/sql-database-query-performance/top-queries.png
[3]: ./media/sql-database-query-performance/query-details.png
[4]: ./media/sql-database-query-performance/top-duration.png
[5]: ./media/sql-database-query-performance/top-execution.png
[6]: ./media/sql-database-query-performance/annotation.png
[7]: ./media/sql-database-query-performance/annotation-details.png
[8]: ./media/sql-database-query-performance/qds-off.png
[9]: ./media/sql-database-query-performance/qds-button.png

