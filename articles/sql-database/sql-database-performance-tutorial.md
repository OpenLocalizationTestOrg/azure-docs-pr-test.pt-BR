---
title: desempenho aaaTroubleshoot problemas e otimizar seu banco de dados | Microsoft Docs
description: "Aplicar as recomendações de desempenho tooyour banco de dados SQL, bem como limpar como toogain insights sobre Olá desempenho das consultas de saudação em execução no banco de dados"
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
ms.openlocfilehash: e948d30ac74eecf45420d5d77ef55e3c0b6f3f47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-performance-issues-and-optimize-your-database"></a><span data-ttu-id="7bcc7-103">Solucionar problemas de desempenho e otimizar seu banco de dados</span><span class="sxs-lookup"><span data-stu-id="7bcc7-103">Troubleshoot performance issues and optimize your database</span></span>

<span data-ttu-id="7bcc7-104">Índices ausentes e consultas precárias são motivos comuns de um desempenho ruim do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="7bcc7-104">Missing indexes and poorly optimized queries are common reasons for poor database performance.</span></span> <span data-ttu-id="7bcc7-105">Neste tutorial, você aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="7bcc7-105">In this tutorial you learn to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="7bcc7-106">Revisar, aplicar e reverter recomendações de melhoria de desempenho</span><span class="sxs-lookup"><span data-stu-id="7bcc7-106">Review, apply and revert performance improvement recommendations</span></span>
> * <span data-ttu-id="7bcc7-107">Localizar consultas com alta utilização de recursos</span><span class="sxs-lookup"><span data-stu-id="7bcc7-107">Find queries with high resource utilization</span></span>
> * <span data-ttu-id="7bcc7-108">Localizar consultas de longa execução</span><span class="sxs-lookup"><span data-stu-id="7bcc7-108">Find long running queries</span></span>

> <span data-ttu-id="7bcc7-109">Você precisa de uma carga de trabalho contínua no banco de dados com problemas de desempenho – um tooreceive por exemplo uma recomendação de índice ausente.</span><span class="sxs-lookup"><span data-stu-id="7bcc7-109">You need a continuous workload on a database with performance issues – missing an index for example tooreceive a recommendation.</span></span>
>

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="7bcc7-110">Faça logon no toohello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7bcc7-110">Log in toohello Azure portal</span></span>

<span data-ttu-id="7bcc7-111">Faça logon no toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="7bcc7-111">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="review-and-apply-a-recommendation"></a><span data-ttu-id="7bcc7-112">Examinar e aplicar uma recomendação</span><span class="sxs-lookup"><span data-stu-id="7bcc7-112">Review and apply a recommendation</span></span>

<span data-ttu-id="7bcc7-113">Siga essas etapas tooapply uma recomendação do sistema de saudação do banco de dados:</span><span class="sxs-lookup"><span data-stu-id="7bcc7-113">Follow these steps tooapply a recommendation from hello system for your database:</span></span>

1. <span data-ttu-id="7bcc7-114">Clique em Olá **recomendações de desempenho** menu na folha do banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="7bcc7-114">Click hello **Performance recommendations** menu in hello database blade.</span></span>

    ![recomendação de desempenho](./media/sql-database-performance-tutorial/perf_recommendations.png)

2. <span data-ttu-id="7bcc7-116">Na lista de saudação de recomendações, selecione uma recomendação de ativa.</span><span class="sxs-lookup"><span data-stu-id="7bcc7-116">From hello list of recommendations, select an active recommendation.</span></span> <span data-ttu-id="7bcc7-117">Neste exemplo, Create Index.</span><span class="sxs-lookup"><span data-stu-id="7bcc7-117">In this example, Create Index.</span></span>

    ![selecionar recomendação](./media/sql-database-performance-tutorial/create_index.png)

3. <span data-ttu-id="7bcc7-119">Aplicar a recomendação de saudação clicando Olá **aplicar** botão.</span><span class="sxs-lookup"><span data-stu-id="7bcc7-119">Apply hello recommendation by clicking hello **Apply** button.</span></span> <span data-ttu-id="7bcc7-120">Opcionalmente, revise os detalhes de recomendação de saudação e consulte o script hello T-SQL muito a ser executado, basta clicar em **Exibir Script** botão.</span><span class="sxs-lookup"><span data-stu-id="7bcc7-120">Optionally, review hello recommendation details and see hello T-SQL script too be executed by clicking on **View Script** button.</span></span>

    ![aplicar recomendação](./media/sql-database-performance-tutorial/apply.png)

4. <span data-ttu-id="7bcc7-122">[Opcional] Habilite o ajuste automático para recomendações toobe aplicada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="7bcc7-122">[Optional] Enable automatic tuning for recommendations toobe applied automatically.</span></span>

    ![auto ajuste](./media/sql-database-performance-tutorial/auto_tuning.png)

## <a name="revert-a-recommendation"></a><span data-ttu-id="7bcc7-124">Reverter uma recomendação</span><span class="sxs-lookup"><span data-stu-id="7bcc7-124">Revert a recommendation</span></span>

<span data-ttu-id="7bcc7-125">Olá Database Advisor monitora cada recomendação implementada.</span><span class="sxs-lookup"><span data-stu-id="7bcc7-125">hello Database Advisor monitors every recommendation implemented.</span></span> <span data-ttu-id="7bcc7-126">Se uma recomendação não melhorar a carga de trabalho hello, ele será revertido automaticamente.</span><span class="sxs-lookup"><span data-stu-id="7bcc7-126">If a recommendation doesn't improve hello workload it will be automatically reverted.</span></span> <span data-ttu-id="7bcc7-127">É possível reverter manualmente uma recomendação, mas isso não será necessário na maioria dos casos.</span><span class="sxs-lookup"><span data-stu-id="7bcc7-127">Manually reverting a recommendation is possible, but not necessary in most cases.</span></span> <span data-ttu-id="7bcc7-128">toorevert uma recomendação:</span><span class="sxs-lookup"><span data-stu-id="7bcc7-128">toorevert a recommendation:</span></span>

1. <span data-ttu-id="7bcc7-129">Acesse o menu de recomendações de desempenho de toohello e selecione uma das recomendações de saudação aplicada.</span><span class="sxs-lookup"><span data-stu-id="7bcc7-129">Go toohello performance recommendations menu and select one of hello applied recommendations.</span></span>

    ![selecionar recomendação](./media/sql-database-performance-tutorial/select.png)

2. <span data-ttu-id="7bcc7-131">Na exibição de detalhes de saudação, clique em **Revert**.</span><span class="sxs-lookup"><span data-stu-id="7bcc7-131">In hello details view, click **Revert**.</span></span>

    ![reverter recomendação](./media/sql-database-performance-tutorial/revert.png)

## <a name="find-hello-query-that-consumes-hello-most-resources"></a><span data-ttu-id="7bcc7-133">Localizar a maioria dos recursos de consulta de saudação que consome Olá</span><span class="sxs-lookup"><span data-stu-id="7bcc7-133">Find hello query that consumes hello most resources</span></span>

<span data-ttu-id="7bcc7-134">Siga essas consultas de saudação etapas toofind consumindo Olá a maioria dos recursos:</span><span class="sxs-lookup"><span data-stu-id="7bcc7-134">Follow these steps toofind hello query consuming hello most resources:</span></span>

1. <span data-ttu-id="7bcc7-135">Clique em Olá **Query Performance Insight** menu na folha do banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="7bcc7-135">Click on hello **Query Performance Insight** menu in hello database blade.</span></span>

    ![informações de consulta](./media/sql-database-performance-tutorial/query_perf_insights.png)

2. <span data-ttu-id="7bcc7-137">Selecionar um tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="7bcc7-137">Select a resource type.</span></span>

    ![informações de consulta](./media/sql-database-performance-tutorial/select_resource_type.png)

3. <span data-ttu-id="7bcc7-139">Primeira consulta na tabela Olá Olá Select.</span><span class="sxs-lookup"><span data-stu-id="7bcc7-139">Select hello first query in hello table.</span></span>

    ![informações de consulta](./media/sql-database-performance-tutorial/select_query.png)

4. <span data-ttu-id="7bcc7-141">Examine os detalhes da consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="7bcc7-141">Review hello query details.</span></span>

    ![informações de consulta](./media/sql-database-performance-tutorial/query_details.png)

## <a name="find-hello-longest-running-query"></a><span data-ttu-id="7bcc7-143">Localizar a consulta de execução mais longa Olá</span><span class="sxs-lookup"><span data-stu-id="7bcc7-143">Find hello longest running query</span></span>

1. <span data-ttu-id="7bcc7-144">Vá tooQuery Performance Insight e selecione Olá **consultas de longa execução** guia.</span><span class="sxs-lookup"><span data-stu-id="7bcc7-144">Go tooQuery Performance Insight and select hello **Long running queries** tab.</span></span>

    ![informações de consulta](./media/sql-database-performance-tutorial/long_running.png)

3. <span data-ttu-id="7bcc7-146">Primeira consulta na tabela Olá Olá Select.</span><span class="sxs-lookup"><span data-stu-id="7bcc7-146">Select hello first query in hello table.</span></span>

    ![informações de consulta](./media/sql-database-performance-tutorial/select_first_query.png)

4. <span data-ttu-id="7bcc7-148">Examine os detalhes da consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="7bcc7-148">Review hello query details.</span></span>

    ![informações de consulta](./media/sql-database-performance-tutorial/review_query_details.png)



## <a name="next-steps"></a><span data-ttu-id="7bcc7-150">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7bcc7-150">Next steps</span></span> 
<span data-ttu-id="7bcc7-151">Índices ausentes e consultas precárias são motivos comuns de um desempenho ruim do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="7bcc7-151">Missing indexes and poorly optimized queries are common reasons for poor database performance.</span></span> <span data-ttu-id="7bcc7-152">Neste tutorial, você aprendeu a:</span><span class="sxs-lookup"><span data-stu-id="7bcc7-152">In this tutorial you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="7bcc7-153">Revisar, aplicar e reverter recomendações de melhoria de desempenho</span><span class="sxs-lookup"><span data-stu-id="7bcc7-153">Review, apply and revert performance improvement recommendations</span></span>
> * <span data-ttu-id="7bcc7-154">Localizar consultas com alta utilização de recursos</span><span class="sxs-lookup"><span data-stu-id="7bcc7-154">Find queries with high resource utilization</span></span>
> * <span data-ttu-id="7bcc7-155">Localizar consultas de longa execução</span><span class="sxs-lookup"><span data-stu-id="7bcc7-155">Find long running queries</span></span>

[<span data-ttu-id="7bcc7-156">Dicas de ajuste de desempenho do Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="7bcc7-156">SQL Database performance tuning tips</span></span>](https://docs.microsoft.com/azure/sql-database/sql-database-troubleshoot-performance)
