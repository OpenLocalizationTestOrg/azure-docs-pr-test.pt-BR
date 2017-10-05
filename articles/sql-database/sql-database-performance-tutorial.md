---
title: Solucionar problemas de desempenho e otimizar seu banco de dados | Microsoft Docs
description: "Aplicar recomendações de desempenho para o banco de dados SQL, bem como aprender a obter informações sobre o desempenho das consultas em execução no seu banco de dados"
metakeywords: azure sql database performance monitoring recommendation
services: sql-database
documentationcenter: 
manager: jhubbard
author: jan-eng
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,monitor & tune
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: janeng
ms.openlocfilehash: f9ae96cdc80c347593f229cb2fce3f2d4d8e7caf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-performance-issues-and-optimize-your-database"></a><span data-ttu-id="e1d9b-103">Solucionar problemas de desempenho e otimizar seu banco de dados</span><span class="sxs-lookup"><span data-stu-id="e1d9b-103">Troubleshoot performance issues and optimize your database</span></span>

<span data-ttu-id="e1d9b-104">Índices ausentes e consultas precárias são motivos comuns de um desempenho ruim do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e1d9b-104">Missing indexes and poorly optimized queries are common reasons for poor database performance.</span></span> <span data-ttu-id="e1d9b-105">Neste tutorial, você aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="e1d9b-105">In this tutorial you learn to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="e1d9b-106">Revisar, aplicar e reverter recomendações de melhoria de desempenho</span><span class="sxs-lookup"><span data-stu-id="e1d9b-106">Review, apply and revert performance improvement recommendations</span></span>
> * <span data-ttu-id="e1d9b-107">Localizar consultas com alta utilização de recursos</span><span class="sxs-lookup"><span data-stu-id="e1d9b-107">Find queries with high resource utilization</span></span>
> * <span data-ttu-id="e1d9b-108">Localizar consultas de longa execução</span><span class="sxs-lookup"><span data-stu-id="e1d9b-108">Find long running queries</span></span>

> <span data-ttu-id="e1d9b-109">Você precisa de uma carga de trabalho contínua em um banco de dados com problemas de desempenho – por exemplo, para receber uma recomendação de índice ausente.</span><span class="sxs-lookup"><span data-stu-id="e1d9b-109">You need a continuous workload on a database with performance issues – missing an index for example to receive a recommendation.</span></span>
>

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="e1d9b-110">Faça logon no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e1d9b-110">Log in to the Azure portal</span></span>

<span data-ttu-id="e1d9b-111">Faça logon no [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e1d9b-111">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="review-and-apply-a-recommendation"></a><span data-ttu-id="e1d9b-112">Examinar e aplicar uma recomendação</span><span class="sxs-lookup"><span data-stu-id="e1d9b-112">Review and apply a recommendation</span></span>

<span data-ttu-id="e1d9b-113">Siga estas etapas para aplicar uma recomendação do sistema ao banco de dados:</span><span class="sxs-lookup"><span data-stu-id="e1d9b-113">Follow these steps to apply a recommendation from the system for your database:</span></span>

1. <span data-ttu-id="e1d9b-114">Clique no menu **Recomendações de desempenho** na folha do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e1d9b-114">Click the **Performance recommendations** menu in the database blade.</span></span>

    ![recomendação de desempenho](./media/sql-database-performance-tutorial/perf_recommendations.png)

2. <span data-ttu-id="e1d9b-116">Na lista de recomendações, selecione uma recomendação ativa.</span><span class="sxs-lookup"><span data-stu-id="e1d9b-116">From the list of recommendations, select an active recommendation.</span></span> <span data-ttu-id="e1d9b-117">Neste exemplo, Create Index.</span><span class="sxs-lookup"><span data-stu-id="e1d9b-117">In this example, Create Index.</span></span>

    ![selecionar recomendação](./media/sql-database-performance-tutorial/create_index.png)

3. <span data-ttu-id="e1d9b-119">Aplique a recomendação clicando no botão **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="e1d9b-119">Apply the recommendation by clicking the **Apply** button.</span></span> <span data-ttu-id="e1d9b-120">Opcionalmente, examine os detalhes de recomendação e veja o script T-SQL a ser executado clicando no botão **Exibir Script**.</span><span class="sxs-lookup"><span data-stu-id="e1d9b-120">Optionally, review the recommendation details and see the T-SQL script to  be executed by clicking on **View Script** button.</span></span>

    ![aplicar recomendação](./media/sql-database-performance-tutorial/apply.png)

4. <span data-ttu-id="e1d9b-122">[Opcional] Habilite o ajuste automático para que as recomendações sejam aplicadas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e1d9b-122">[Optional] Enable automatic tuning for recommendations to be applied automatically.</span></span>

    ![auto ajuste](./media/sql-database-performance-tutorial/auto_tuning.png)

## <a name="revert-a-recommendation"></a><span data-ttu-id="e1d9b-124">Reverter uma recomendação</span><span class="sxs-lookup"><span data-stu-id="e1d9b-124">Revert a recommendation</span></span>

<span data-ttu-id="e1d9b-125">O Assistente do Banco de Dados monitora todas as recomendações implementadas.</span><span class="sxs-lookup"><span data-stu-id="e1d9b-125">The Database Advisor monitors every recommendation implemented.</span></span> <span data-ttu-id="e1d9b-126">Se uma recomendação não melhorar a carga de trabalho, ela será automaticamente revertida.</span><span class="sxs-lookup"><span data-stu-id="e1d9b-126">If a recommendation doesn't improve the workload it will be automatically reverted.</span></span> <span data-ttu-id="e1d9b-127">É possível reverter manualmente uma recomendação, mas isso não será necessário na maioria dos casos.</span><span class="sxs-lookup"><span data-stu-id="e1d9b-127">Manually reverting a recommendation is possible, but not necessary in most cases.</span></span> <span data-ttu-id="e1d9b-128">Para reverter uma recomendação:</span><span class="sxs-lookup"><span data-stu-id="e1d9b-128">To revert a recommendation:</span></span>

1. <span data-ttu-id="e1d9b-129">Vá para o menu de recomendações de desempenho e selecione uma das recomendações aplicadas.</span><span class="sxs-lookup"><span data-stu-id="e1d9b-129">Go to the performance recommendations menu and select one of the applied recommendations.</span></span>

    ![selecionar recomendação](./media/sql-database-performance-tutorial/select.png)

2. <span data-ttu-id="e1d9b-131">Na exibição de detalhes, clique em **Reverter**.</span><span class="sxs-lookup"><span data-stu-id="e1d9b-131">In the details view, click **Revert**.</span></span>

    ![reverter recomendação](./media/sql-database-performance-tutorial/revert.png)

## <a name="find-the-query-that-consumes-the-most-resources"></a><span data-ttu-id="e1d9b-133">Localizar a consulta que consome mais recursos</span><span class="sxs-lookup"><span data-stu-id="e1d9b-133">Find the query that consumes the most resources</span></span>

<span data-ttu-id="e1d9b-134">Siga estas etapas para localizar a consulta que consome mais recursos:</span><span class="sxs-lookup"><span data-stu-id="e1d9b-134">Follow these steps to find the query consuming the most resources:</span></span>

1. <span data-ttu-id="e1d9b-135">Clique no menu **Análise de Desempenho de Consultas** na folha do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e1d9b-135">Click on the **Query Performance Insight** menu in the database blade.</span></span>

    ![informações de consulta](./media/sql-database-performance-tutorial/query_perf_insights.png)

2. <span data-ttu-id="e1d9b-137">Selecionar um tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="e1d9b-137">Select a resource type.</span></span>

    ![informações de consulta](./media/sql-database-performance-tutorial/select_resource_type.png)

3. <span data-ttu-id="e1d9b-139">Selecione a primeira consulta na tabela.</span><span class="sxs-lookup"><span data-stu-id="e1d9b-139">Select the first query in the table.</span></span>

    ![informações de consulta](./media/sql-database-performance-tutorial/select_query.png)

4. <span data-ttu-id="e1d9b-141">Examine os detalhes da consulta.</span><span class="sxs-lookup"><span data-stu-id="e1d9b-141">Review the query details.</span></span>

    ![informações de consulta](./media/sql-database-performance-tutorial/query_details.png)

## <a name="find-the-longest-running-query"></a><span data-ttu-id="e1d9b-143">Localizar a consulta mais longa em execução</span><span class="sxs-lookup"><span data-stu-id="e1d9b-143">Find the longest running query</span></span>

1. <span data-ttu-id="e1d9b-144">Vá para a Análise de Desempenho de Consultas e selecione a guia **Consultas de longa execução**.</span><span class="sxs-lookup"><span data-stu-id="e1d9b-144">Go to Query Performance Insight and select the **Long running queries** tab.</span></span>

    ![informações de consulta](./media/sql-database-performance-tutorial/long_running.png)

3. <span data-ttu-id="e1d9b-146">Selecione a primeira consulta na tabela.</span><span class="sxs-lookup"><span data-stu-id="e1d9b-146">Select the first query in the table.</span></span>

    ![informações de consulta](./media/sql-database-performance-tutorial/select_first_query.png)

4. <span data-ttu-id="e1d9b-148">Examine os detalhes da consulta.</span><span class="sxs-lookup"><span data-stu-id="e1d9b-148">Review the query details.</span></span>

    ![informações de consulta](./media/sql-database-performance-tutorial/review_query_details.png)



## <a name="next-steps"></a><span data-ttu-id="e1d9b-150">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e1d9b-150">Next steps</span></span> 
<span data-ttu-id="e1d9b-151">Índices ausentes e consultas precárias são motivos comuns de um desempenho ruim do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e1d9b-151">Missing indexes and poorly optimized queries are common reasons for poor database performance.</span></span> <span data-ttu-id="e1d9b-152">Neste tutorial, você aprendeu a:</span><span class="sxs-lookup"><span data-stu-id="e1d9b-152">In this tutorial you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="e1d9b-153">Revisar, aplicar e reverter recomendações de melhoria de desempenho</span><span class="sxs-lookup"><span data-stu-id="e1d9b-153">Review, apply and revert performance improvement recommendations</span></span>
> * <span data-ttu-id="e1d9b-154">Localizar consultas com alta utilização de recursos</span><span class="sxs-lookup"><span data-stu-id="e1d9b-154">Find queries with high resource utilization</span></span>
> * <span data-ttu-id="e1d9b-155">Localizar consultas de longa execução</span><span class="sxs-lookup"><span data-stu-id="e1d9b-155">Find long running queries</span></span>

[<span data-ttu-id="e1d9b-156">Dicas de ajuste de desempenho do Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="e1d9b-156">SQL Database performance tuning tips</span></span>](https://docs.microsoft.com/azure/sql-database/sql-database-troubleshoot-performance)
