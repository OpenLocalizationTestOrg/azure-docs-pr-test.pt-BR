---
title: "aaaQuery informações de desempenho para o banco de dados do SQL Azure | Microsoft Docs"
description: "Monitoramento do desempenho de consulta identifica Olá consumo da CPU a maioria das consultas para um banco de dados do SQL Azure."
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
ms.openlocfilehash: 01cca26f85193c679365585cd676449c9db00e1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-query-performance-insight"></a><span data-ttu-id="f8ef2-103">Visão do desempenho de consulta de Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="f8ef2-103">Azure SQL Database Query Performance Insight</span></span>
<span data-ttu-id="f8ef2-104">Gerenciamento e ajuste de desempenho de saudação de bancos de dados relacionais são uma tarefa desafiadora que requer conhecimento significativo e o investimento de tempo.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-104">Managing and tuning hello performance of relational databases is a challenging task that requires significant expertise and time investment.</span></span> <span data-ttu-id="f8ef2-105">Análise de desempenho de consulta permite que você toospend menos tempo Solucionando problemas de desempenho de banco de dados, fornecendo a seguir hello:</span><span class="sxs-lookup"><span data-stu-id="f8ef2-105">Query Performance Insight allows you toospend less time troubleshooting database performance by providing hello following:</span></span>

* <span data-ttu-id="f8ef2-106">Mais informações sobre o consumo de recursos de bancos de dados (DTU).</span><span class="sxs-lookup"><span data-stu-id="f8ef2-106">Deeper insight into your databases resource (DTU) consumption.</span></span> 
* <span data-ttu-id="f8ef2-107">principais consultas por contagem de duração/CPU/execução, que potencialmente podem ser ajustadas para melhorar o desempenho Hello.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-107">hello top queries by CPU/Duration/Execution count, which can potentially be tuned for improved performance.</span></span>
* <span data-ttu-id="f8ef2-108">Olá toodrill de capacidade para baixo em detalhes de saudação de uma consulta, exibir seu texto e o histórico de utilização de recursos.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-108">hello ability toodrill down into hello details of a query, view its text and history of resource utilization.</span></span> 
* <span data-ttu-id="f8ef2-109">Anotações de ajuste de desempenho que mostram as ações executadas [Advisor do Banco de Dados SQL Azure](sql-database-advisor.md)</span><span class="sxs-lookup"><span data-stu-id="f8ef2-109">Performance tuning annotations that show actions performed by [SQL Azure Database Advisor](sql-database-advisor.md)</span></span>  



## <a name="prerequisites"></a><span data-ttu-id="f8ef2-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f8ef2-110">Prerequisites</span></span>
* <span data-ttu-id="f8ef2-111">A Análise de Desempenho de Consultas exige a execução do [Repositório de Consultas](https://msdn.microsoft.com/library/dn817826.aspx) em seu banco de dados.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-111">Query Performance Insight requires that [Query Store](https://msdn.microsoft.com/library/dn817826.aspx) is active on your database.</span></span> <span data-ttu-id="f8ef2-112">Se o repositório de consultas não está em execução, o portal Olá solicita tooturn-la no.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-112">If Query Store is not running, hello portal prompts you tooturn it on.</span></span>

## <a name="permissions"></a><span data-ttu-id="f8ef2-113">Permissões</span><span class="sxs-lookup"><span data-stu-id="f8ef2-113">Permissions</span></span>
<span data-ttu-id="f8ef2-114">a seguir Olá [controle de acesso baseado em função](../active-directory/role-based-access-control-what-is.md) permissões são necessária toouse análise de desempenho de consulta:</span><span class="sxs-lookup"><span data-stu-id="f8ef2-114">hello following [role-based access control](../active-directory/role-based-access-control-what-is.md) permissions are required toouse Query Performance Insight:</span></span> 

* <span data-ttu-id="f8ef2-115">**Leitor**, **proprietário**, **Colaborador**, **Colaborador de banco de dados SQL**, ou **Colaborador do SQL Server** permissões são necessário tooview Olá maior consumo de recursos gráficos e consultas.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-115">**Reader**, **Owner**, **Contributor**, **SQL DB Contributor**, or **SQL Server Contributor** permissions are required tooview hello top resource consuming queries and charts.</span></span> 
* <span data-ttu-id="f8ef2-116">**Proprietário**, **Colaborador**, **Colaborador de banco de dados SQL**, ou **Colaborador do SQL Server** permissões são necessárias tooview texto da consulta.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-116">**Owner**, **Contributor**, **SQL DB Contributor**, or **SQL Server Contributor** permissions are required tooview query text.</span></span>

## <a name="using-query-performance-insight"></a><span data-ttu-id="f8ef2-117">Usando a Visão de Desempenho de Consulta</span><span class="sxs-lookup"><span data-stu-id="f8ef2-117">Using Query Performance Insight</span></span>
<span data-ttu-id="f8ef2-118">Análise de desempenho de consulta é fácil toouse:</span><span class="sxs-lookup"><span data-stu-id="f8ef2-118">Query Performance Insight is easy toouse:</span></span>

* <span data-ttu-id="f8ef2-119">Abra [portal do Azure](https://portal.azure.com/) e banco de dados de localização que você deseja tooexamine.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-119">Open [Azure portal](https://portal.azure.com/) and find database that you want tooexamine.</span></span> 
  * <span data-ttu-id="f8ef2-120">No menu do lado esquerdo, em suporte e solução de problemas, selecione "Análise de Desempenho de Consultas".</span><span class="sxs-lookup"><span data-stu-id="f8ef2-120">From left-hand side menu, under support and troubleshooting, select “Query Performance Insight”.</span></span>
* <span data-ttu-id="f8ef2-121">Na guia da primeira hello, examine a lista de saudação das principais consultas de consumo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-121">On hello first tab, review hello list of top resource-consuming queries.</span></span>
* <span data-ttu-id="f8ef2-122">Selecione uma consulta individual tooview seus detalhes.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-122">Select an individual query tooview its details.</span></span>
* <span data-ttu-id="f8ef2-123">Abra o [Advisor do Banco de Dados do SQL Azure](sql-database-advisor.md) e verifique se há alguma recomendação disponível.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-123">Open [SQL Azure Database Advisor](sql-database-advisor.md) and check if any recommendations are available.</span></span>
* <span data-ttu-id="f8ef2-124">Use os controles deslizantes ou ícones toochange observado o intervalo de zoom.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-124">Use sliders or zoom icons toochange observed interval.</span></span>
  
    ![painel de desempenho](./media/sql-database-query-performance/performance.png)

> [!NOTE]
> <span data-ttu-id="f8ef2-126">Algumas horas de dados precisa toobe capturado pelo repositório de consultas de análise de desempenho de consulta do banco de dados SQL tooprovide.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-126">A couple hours of data needs toobe captured by Query Store for SQL Database tooprovide query performance insights.</span></span> <span data-ttu-id="f8ef2-127">Se o banco de dados de saudação não tem atividades ou repositório de consultas não estava ativo durante um determinado período de tempo, gráficos de saudação estará vazios ao exibir o período de tempo.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-127">If hello database has no activity or Query Store was not active during a certain time period, hello charts will be empty when displaying that time period.</span></span> <span data-ttu-id="f8ef2-128">Você pode habilitar o Armazenamento de Consulta a qualquer momento se ele não estiver em execução.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-128">You may enable Query Store at any time if it is not running.</span></span>   
> 
> 

## <a name="review-top-cpu-consuming-queries"></a><span data-ttu-id="f8ef2-129">Examinar as consultas que mais consomem CPU</span><span class="sxs-lookup"><span data-stu-id="f8ef2-129">Review top CPU consuming queries</span></span>
<span data-ttu-id="f8ef2-130">Em Olá [portal](http://portal.azure.com) Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="f8ef2-130">In hello [portal](http://portal.azure.com) do hello following:</span></span>

1. <span data-ttu-id="f8ef2-131">Procurar tooa banco de dados SQL e clique em **todas as configurações** > **suporte + solução de problemas** > **análise de desempenho de consulta**.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-131">Browse tooa SQL database and click **All settings** > **Support + Troubleshooting** > **Query performance insight**.</span></span> 
   
    ![Análise de desempenho de consultas][1]
   
    <span data-ttu-id="f8ef2-133">Abre o modo de exibição do Hello principais consultas e principais consultas de consumo da CPU Olá são listadas.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-133">hello top queries view opens and hello top CPU consuming queries are listed.</span></span>
2. <span data-ttu-id="f8ef2-134">Clique em torno do gráfico de saudação para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-134">Click around hello chart for details.</span></span><br><span data-ttu-id="f8ef2-135">Hello linha superior mostra % DTU geral do banco de dados Olá, enquanto as barras Olá mostram % de CPU consumida por consultas de saudação selecionada durante o intervalo selecionado hello (por exemplo, se **semana passada** está selecionado cada barra representa um dia).</span><span class="sxs-lookup"><span data-stu-id="f8ef2-135">hello top line shows overall DTU% for hello database, while hello bars show CPU% consumed by hello selected queries during hello selected interval (for example, if **Past week** is selected each bar represents one day).</span></span>
   
    ![principais consultas][2]
   
    <span data-ttu-id="f8ef2-137">grade inferior de saudação representa informações agregadas para consultas de saudação visível.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-137">hello bottom grid represents aggregated information for hello visible queries.</span></span>
   
   * <span data-ttu-id="f8ef2-138">ID da consulta: identificador exclusivo da consulta no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-138">Query ID - unique identifier of query inside database.</span></span>
   * <span data-ttu-id="f8ef2-139">CPU por consulta durante o intervalo observável (depende da função de agregação).</span><span class="sxs-lookup"><span data-stu-id="f8ef2-139">CPU per query during observable interval (depends on aggregation function).</span></span>
   * <span data-ttu-id="f8ef2-140">Duração por consulta (depende da função de agregação).</span><span class="sxs-lookup"><span data-stu-id="f8ef2-140">Duration per query (depends on aggregation function).</span></span>
   * <span data-ttu-id="f8ef2-141">Número total de execuções para uma consulta específica.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-141">Total number of executions for a particular query.</span></span>
     
     <span data-ttu-id="f8ef2-142">Selecione ou desmarque tooinclude consultas individuais ou excluí-los do gráfico de saudação usando as caixas de seleção.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-142">Select or clear individual queries tooinclude or exclude them from hello chart using checkboxes.</span></span>
3. <span data-ttu-id="f8ef2-143">Se seus dados se torna obsoletos, clique em Olá **atualização** botão.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-143">If your data becomes stale, click hello **Refresh** button.</span></span>
4. <span data-ttu-id="f8ef2-144">Você pode usar os controles deslizantes e intervalo de observação de toochange de botões de zoom e investigar picos: ![configurações](./media/sql-database-query-performance/zoom.png)</span><span class="sxs-lookup"><span data-stu-id="f8ef2-144">You can use sliders and zoom buttons toochange observation interval and investigate spikes:  ![settings](./media/sql-database-query-performance/zoom.png)</span></span>
5. <span data-ttu-id="f8ef2-145">Opcionalmente, se você quiser uma exibição diferente, você pode selecionar a guia **Personalizar** e definir:</span><span class="sxs-lookup"><span data-stu-id="f8ef2-145">Optionally, if you want a different view, you can select **Custom** tab and set:</span></span>
   
   * <span data-ttu-id="f8ef2-146">Métrica (CPU, duração, contagem de execução)</span><span class="sxs-lookup"><span data-stu-id="f8ef2-146">Metric (CPU, duration, execution count)</span></span>
   * <span data-ttu-id="f8ef2-147">Intervalo de tempo (Últimas 24 horas, Última semana, Mês passado).</span><span class="sxs-lookup"><span data-stu-id="f8ef2-147">Time interval (Last 24 hours, Past week, Past month).</span></span> 
   * <span data-ttu-id="f8ef2-148">Número de consultas.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-148">Number of queries.</span></span>
   * <span data-ttu-id="f8ef2-149">Função de agregação.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-149">Aggregation function.</span></span>
     
     ![Configurações](./media/sql-database-query-performance/custom-tab.png)

## <a name="viewing-individual-query-details"></a><span data-ttu-id="f8ef2-151">Exibindo detalhes de uma consulta individual</span><span class="sxs-lookup"><span data-stu-id="f8ef2-151">Viewing individual query details</span></span>
<span data-ttu-id="f8ef2-152">detalhes da consulta tooview:</span><span class="sxs-lookup"><span data-stu-id="f8ef2-152">tooview query details:</span></span>

1. <span data-ttu-id="f8ef2-153">Clique em qualquer consulta na lista de saudação das principais consultas.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-153">Click any query in hello list of top queries.</span></span>
   
    ![detalhes](./media/sql-database-query-performance/details.png)
2. <span data-ttu-id="f8ef2-155">modo de exibição de detalhes de saudação é aberto e contagem de duração/consumo/execução Olá consultas de CPU é dividida ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-155">hello details view opens and hello queries CPU consumption/Duration/Execution count is broken down over time.</span></span>
3. <span data-ttu-id="f8ef2-156">Clique em torno do gráfico de saudação para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-156">Click around hello chart for details.</span></span>
   
   * <span data-ttu-id="f8ef2-157">Gráfico superior mostra a linha com o banco de dados DTU % geral e barras de saudação são % de CPU consumida pela consulta selecionada hello.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-157">Top chart shows line with overall database DTU%, and hello bars are CPU% consumed by hello selected query.</span></span>
   * <span data-ttu-id="f8ef2-158">Segundo gráfico mostra a duração total pela consulta selecionada hello.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-158">Second chart shows total duration by hello selected query.</span></span>
   * <span data-ttu-id="f8ef2-159">Gráfico de inferior mostra o número total de execuções pela consulta selecionada hello.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-159">Bottom chart shows total number of executions by hello selected query.</span></span>
     
     ![detalhes da consulta][3]
4. <span data-ttu-id="f8ef2-161">Opcionalmente, use os controles deslizantes, botões de zoom ou clique em **configurações** toocustomize como dados de consulta são exibidos ou toopick um período de tempo diferentes.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-161">Optionally, use sliders, zoom buttons or click **Settings** toocustomize how query data is displayed, or toopick a different time period.</span></span>

## <a name="review-top-queries-per-duration"></a><span data-ttu-id="f8ef2-162">Analise as principais consultas por duração</span><span class="sxs-lookup"><span data-stu-id="f8ef2-162">Review top queries per duration</span></span>
<span data-ttu-id="f8ef2-163">Na atualização recente de saudação de análise de desempenho de consulta, apresentamos duas novas métricas que podem ajudá-lo a identificar gargalos potenciais: contagem de duração e a execução.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-163">In hello recent update of Query Performance Insight, we introduced two new metrics that can help you identify potential bottlenecks: duration and execution count.</span></span><br>

<span data-ttu-id="f8ef2-164">Consultas de longa execução têm potencial de maior Olá para bloquear recursos mais longo, bloqueando outros usuários e limitar a escalabilidade.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-164">Long-running queries have hello greatest potential for locking resources longer, blocking other users, and limiting scalability.</span></span> <span data-ttu-id="f8ef2-165">Eles também são melhores candidatos Olá para otimização.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-165">They are also hello best candidates for optimization.</span></span><br>

<span data-ttu-id="f8ef2-166">tooidentify consultas de longa execução:</span><span class="sxs-lookup"><span data-stu-id="f8ef2-166">tooidentify long running queries:</span></span>

1. <span data-ttu-id="f8ef2-167">Abra a guia **Personalizar** na Análise de Desempenho de Consultas do banco de dados selecionado</span><span class="sxs-lookup"><span data-stu-id="f8ef2-167">Open **Custom** tab in Query Performance Insight for selected database</span></span>
2. <span data-ttu-id="f8ef2-168">Alterar as métricas toobe **duração**</span><span class="sxs-lookup"><span data-stu-id="f8ef2-168">Change metrics toobe **duration**</span></span>
3. <span data-ttu-id="f8ef2-169">Selecione o número de consultas e o intervalo de observação</span><span class="sxs-lookup"><span data-stu-id="f8ef2-169">Select number of queries and observation interval</span></span>
4. <span data-ttu-id="f8ef2-170">Selecione a função de agregação</span><span class="sxs-lookup"><span data-stu-id="f8ef2-170">Select aggregation function</span></span>
   
   * <span data-ttu-id="f8ef2-171">**Soma** adiciona todo o tempo de execução de consulta durante todo o intervalo de observação.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-171">**Sum** adds up all query execution time during whole observation interval.</span></span>
   * <span data-ttu-id="f8ef2-172">**Máximo** localiza consultas para as quais tempo de execução foi máximo no intervalo inteiro de observação.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-172">**Max** finds queries which execution time was maximum at whole observation interval.</span></span>
   * <span data-ttu-id="f8ef2-173">**AVG** localiza o tempo médio de execução de todas as execuções de consulta e exibir hello superior fora essas médias.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-173">**Avg** finds average execution time of all query executions and show you hello top out of these averages.</span></span> 
     
     ![duração da consulta][4]

## <a name="review-top-queries-per-execution-count"></a><span data-ttu-id="f8ef2-175">Analise as principais consultas por contagem de execução</span><span class="sxs-lookup"><span data-stu-id="f8ef2-175">Review top queries per execution count</span></span>
<span data-ttu-id="f8ef2-176">Um alto número de execuções pode não estar afetando o banco de dados propriamente dito e o uso de recursos pode ser baixo, mas o aplicativo pode ficar lento no geral.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-176">High number of executions might not be affecting database itself and resources usage can be low, but overall application might get slow.</span></span>

<span data-ttu-id="f8ef2-177">Em alguns casos, a contagem de execução muito alto pode levar tooincrease da rede viagens de ida e volta.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-177">In some cases, very high execution count may lead tooincrease of network round trips.</span></span> <span data-ttu-id="f8ef2-178">Viagens de ida e afetam o desempenho de forma significativa.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-178">Round trips significantly affect performance.</span></span> <span data-ttu-id="f8ef2-179">Eles são latência de toonetwork de assunto e latência de servidor toodownstream.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-179">They are subject toonetwork latency and toodownstream server latency.</span></span> 

<span data-ttu-id="f8ef2-180">Por exemplo, muitos sites controlados por dados muito acessar banco de dados de saudação para cada solicitação de usuário.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-180">For example, many data-driven Web sites heavily access hello database for every user request.</span></span> <span data-ttu-id="f8ef2-181">Durante a conexão pooling ajuda, hello aumentada tráfego de rede e a carga de processamento no servidor de banco de dados de saudação podem afetar desempenho.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-181">While connection pooling helps, hello increased network traffic and processing load on hello database server can adversely affect performance.</span></span>  <span data-ttu-id="f8ef2-182">Recomendação geral é tookeep round viagens tooan nível mínimo absoluto.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-182">General advice is tookeep round trips tooan absolute minimum.</span></span>

<span data-ttu-id="f8ef2-183">tooidentify executados com frequência as consultas de consultas ("tagarelas"):</span><span class="sxs-lookup"><span data-stu-id="f8ef2-183">tooidentify frequently executed queries (“chatty”) queries:</span></span>

1. <span data-ttu-id="f8ef2-184">Abra a guia **Personalizar** na Análise de Desempenho de Consultas do banco de dados selecionado</span><span class="sxs-lookup"><span data-stu-id="f8ef2-184">Open **Custom** tab in Query Performance Insight for selected database</span></span>
2. <span data-ttu-id="f8ef2-185">Alterar as métricas toobe **contagem de execução**</span><span class="sxs-lookup"><span data-stu-id="f8ef2-185">Change metrics toobe **execution count**</span></span>
3. <span data-ttu-id="f8ef2-186">Selecione o número de consultas e o intervalo de observação</span><span class="sxs-lookup"><span data-stu-id="f8ef2-186">Select number of queries and observation interval</span></span>
   
    ![contagem de execução da consulta][5]

## <a name="understanding-performance-tuning-annotations"></a><span data-ttu-id="f8ef2-188">Noções básicas sobre anotações de ajuste de desempenho</span><span class="sxs-lookup"><span data-stu-id="f8ef2-188">Understanding performance tuning annotations</span></span>
<span data-ttu-id="f8ef2-189">Ao explorar a carga de trabalho de análise de desempenho de consulta, você poderá notar ícones com uma linha vertical na parte superior do gráfico de saudação.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-189">While exploring your workload in Query Performance Insight, you might notice icons with vertical line on top of hello chart.</span></span><br>

<span data-ttu-id="f8ef2-190">Esses ícones são anotações; eles representam as ações que afetam o desempenho executadas pelo [Advisor do Banco de Dados SQL Azure](sql-database-advisor.md).</span><span class="sxs-lookup"><span data-stu-id="f8ef2-190">These icons are annotations; they represent performance affecting actions performed by [SQL Azure Database Advisor](sql-database-advisor.md).</span></span> <span data-ttu-id="f8ef2-191">Ao focalização anotação, você obtém informações básicas sobre a ação de saudação:</span><span class="sxs-lookup"><span data-stu-id="f8ef2-191">By hovering annotation, you get basic information about hello action:</span></span>

![anotação da consulta][6]

<span data-ttu-id="f8ef2-193">Se você quiser tooknow mais ou aplica a recomendação do orientador, clique o ícone de saudação.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-193">If you want tooknow more or apply advisor recommendation, click hello icon.</span></span> <span data-ttu-id="f8ef2-194">O ícone abrirá os detalhes da ação.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-194">It will open details of action.</span></span> <span data-ttu-id="f8ef2-195">Se for uma recomendação ativa, você pode aplicar imediatamente usando o comando.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-195">If it’s an active recommendation you can apply it straight away using command.</span></span>

![detalhes de anotação de consulta][7]

### <a name="multiple-annotations"></a><span data-ttu-id="f8ef2-197">Várias anotações.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-197">Multiple annotations.</span></span>
<span data-ttu-id="f8ef2-198">É possível que devido ao nível de zoom, anotações são tooeach fechar outros irá obter recolhidas em uma.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-198">It’s possible, that because of zoom level, annotations that are close tooeach other will get collapsed into one.</span></span> <span data-ttu-id="f8ef2-199">Isso será representado por um ícone especial, clicar nele irá abrirá uma nova folha onde a lista de anotações agrupadas será mostrada.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-199">This will be represented by special icon, clicking it will open new blade where list of grouped annotations will be shown.</span></span>
<span data-ttu-id="f8ef2-200">Correlacionando consultas e ações de ajuste de desempenho pode ajudar a toobetter a entender sua carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-200">Correlating queries and performance tuning actions can help toobetter understand your workload.</span></span> 

## <a name="optimizing-hello-query-store-configuration-for-query-performance-insight"></a><span data-ttu-id="f8ef2-201">Otimizando a configuração do repositório de consultas Olá para análise de desempenho de consulta</span><span class="sxs-lookup"><span data-stu-id="f8ef2-201">Optimizing hello Query Store configuration for Query Performance Insight</span></span>
<span data-ttu-id="f8ef2-202">Durante o uso de análise de desempenho de consulta, você pode encontrar hello mensagens do repositório de consultas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f8ef2-202">During your use of Query Performance Insight, you might encounter hello following Query Store messages:</span></span>

* <span data-ttu-id="f8ef2-203">"O Repositório de Consulta não está corretamente configurado neste banco de dados.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-203">"Query Store is not properly configured on this database.</span></span> <span data-ttu-id="f8ef2-204">Clique aqui toolearn mais."</span><span class="sxs-lookup"><span data-stu-id="f8ef2-204">Click here toolearn more."</span></span>
* <span data-ttu-id="f8ef2-205">"O Repositório de Consulta não está corretamente configurado neste banco de dados.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-205">"Query Store is not properly configured on this database.</span></span> <span data-ttu-id="f8ef2-206">Clique aqui toochange configurações".</span><span class="sxs-lookup"><span data-stu-id="f8ef2-206">Click here toochange settings."</span></span> 

<span data-ttu-id="f8ef2-207">Normalmente, essas mensagens aparecem ao repositório de consultas não é capaz de toocollect novos dados.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-207">These messages usually appear when Query Store is not able toocollect new data.</span></span> 

<span data-ttu-id="f8ef2-208">O primeiro caso ocorre quando o Repositório de Consultas está em estado somente leitura e os parâmetros são definidos de forma ideal.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-208">First case happens when Query Store is in Read-Only state and parameters are set optimally.</span></span> <span data-ttu-id="f8ef2-209">Você pode corrigir isso, aumentando o tamanho do Repositório de Consultas ou desmarcando o Repositório de Consultas.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-209">You can fix this by increasing size of Query Store or clearing Query Store.</span></span>

![botão qds][8]

<span data-ttu-id="f8ef2-211">O segundo caso acontece quando o Repositório de Consultas está Desligado ou parâmetros não estão definidos de forma ideal.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-211">Second case happens when Query Store is Off or parameters aren’t set optimally.</span></span> <br><span data-ttu-id="f8ef2-212">Você pode alterar Olá retenção e a captura de política e habilitar repositório de consultas, executando os comandos abaixo ou diretamente do portal:</span><span class="sxs-lookup"><span data-stu-id="f8ef2-212">You can change hello Retention and Capture policy and enable Query Store by executing commands below or directly from portal:</span></span>

![botão qds][9]

### <a name="recommended-retention-and-capture-policy"></a><span data-ttu-id="f8ef2-214">Política recomendada de retenção e captura</span><span class="sxs-lookup"><span data-stu-id="f8ef2-214">Recommended retention and capture policy</span></span>
<span data-ttu-id="f8ef2-215">Há dois tipos de política de retenção:</span><span class="sxs-lookup"><span data-stu-id="f8ef2-215">There are two types of retention policies:</span></span>

* <span data-ttu-id="f8ef2-216">Tamanho base - se conjunto tooAUTO ele limpará os dados automaticamente quando quase o tamanho máximo for atingido.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-216">Size based - if set tooAUTO it will clean data automatically when near max size is reached.</span></span>
* <span data-ttu-id="f8ef2-217">Tempo com base - por padrão, definirá too30 dias, que significa que, se o repositório de consultas será executado sem espaço, ele excluirá consultar informações mais de 30 dias</span><span class="sxs-lookup"><span data-stu-id="f8ef2-217">Time based - by default we will set it too30 days, which means, if Query Store will run out of space, it will delete query information older than 30 days</span></span>

<span data-ttu-id="f8ef2-218">A política de captura pode ser definida para:</span><span class="sxs-lookup"><span data-stu-id="f8ef2-218">Capture policy could be set to:</span></span>

* <span data-ttu-id="f8ef2-219">**Todas**: captura todas as consultas.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-219">**All** - Captures all queries.</span></span>
* <span data-ttu-id="f8ef2-220">**Automática**: consultas pouco frequentes e consultas com duração de execução e compilação insignificantes são ignoradas.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-220">**Auto** - Infrequent queries and queries with insignificant compile and execution duration are ignored.</span></span> <span data-ttu-id="f8ef2-221">Os limites da duração de contagem de execução, compilação e tempo de execução são determinados internamente.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-221">Thresholds for execution count, compile and runtime duration are internally determined.</span></span> <span data-ttu-id="f8ef2-222">Essa é a opção de padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-222">This is hello default option.</span></span>
* <span data-ttu-id="f8ef2-223">**Nenhuma** – o Repositório de Consultas interrompe a captura de novas consultas, porém, as estatísticas de tempo de execução para consultas já capturadas ainda são coletadas.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-223">**None** - Query Store stops capturing new queries, however runtime stats for already captured queries are still collected.</span></span>

<span data-ttu-id="f8ef2-224">É recomendável definir todas as políticas tooAUTO e limpar política too30 dias:</span><span class="sxs-lookup"><span data-stu-id="f8ef2-224">We recommend setting all policies tooAUTO and clean policy too30 days:</span></span>

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (SIZE_BASED_CLEANUP_MODE = AUTO);

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 30));

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (QUERY_CAPTURE_MODE = AUTO);

<span data-ttu-id="f8ef2-225">Aumente o tamanho do Repositório de Consultas.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-225">Increase size of Query Store.</span></span> <span data-ttu-id="f8ef2-226">Isso pode ser executada pelo banco de dados tooa conexão e emitindo a seguinte consulta:</span><span class="sxs-lookup"><span data-stu-id="f8ef2-226">This could be performed by connecting tooa database and issuing following query:</span></span>

    ALTER DATABASE [YourDB]
    SET QUERY_STORE (MAX_STORAGE_SIZE_MB = 1024);

<span data-ttu-id="f8ef2-227">Aplicar essas configurações, eventualmente, fará o repositório de consultas coleta consultas novas, no entanto, se você não quiser toowait você pode limpar o repositório de consultas.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-227">Applying these settings will eventually make Query Store collecting new queries, however if you don’t want toowait you can clear Query Store.</span></span> 

> [!NOTE]
> <span data-ttu-id="f8ef2-228">Executando consulta a seguir excluirá todas as informações atuais de saudação repositório de consultas.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-228">Executing following query will delete all current information in hello Query Store.</span></span> 
> 
> 

    ALTER DATABASE [YourDB] SET QUERY_STORE CLEAR;


## <a name="summary"></a><span data-ttu-id="f8ef2-229">Resumo</span><span class="sxs-lookup"><span data-stu-id="f8ef2-229">Summary</span></span>
<span data-ttu-id="f8ef2-230">Análise de desempenho de consulta ajuda a entender o impacto de saudação de sua carga de trabalho de consulta e como ele se relaciona toodatabase o consumo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-230">Query Performance Insight helps you understand hello impact of your query workload and how it relates toodatabase resource consumption.</span></span> <span data-ttu-id="f8ef2-231">Com esse recurso, você saiba mais sobre Olá consultas mais desgastantes e identificar facilmente Olá aqueles toofix antes de se tornarem um problema.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-231">With this feature, you will learn about hello top consuming queries, and easily identify hello ones toofix before they become a problem.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8ef2-232">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f8ef2-232">Next steps</span></span>
<span data-ttu-id="f8ef2-233">Para obter recomendações adicionais sobre como melhorar o desempenho de saudação do banco de dados SQL, clique em [recomendações](sql-database-advisor.md) em Olá **Query Performance Insight** folha.</span><span class="sxs-lookup"><span data-stu-id="f8ef2-233">For additional recommendations about improving hello performance of your SQL database, click [Recommendations](sql-database-advisor.md) on hello **Query Performance Insight** blade.</span></span>

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

