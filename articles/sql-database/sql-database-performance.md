---
title: Monitorar e melhorar o desempenho - Banco de Dados SQL do Azure | Microsoft Docs
description: "O Banco de Dados SQL do Azure fornece ferramentas de desempenho para ajudá-lo a identificar áreas em que é possível melhorar o desempenho de consulta atual."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: a60b75ac-cf27-4d73-8322-ee4d4c448aa2
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/19/2016
ms.author: sstein
ms.openlocfilehash: 522b932ab055978c52f085dbaa36095bb6b77962
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-and-improve-performance"></a><span data-ttu-id="03a93-103">Monitorar e melhorar o desempenho</span><span class="sxs-lookup"><span data-stu-id="03a93-103">Monitor and improve performance</span></span>
<span data-ttu-id="03a93-104">O Banco de Dados SQL do Azure identifica possíveis problemas em seu banco de dados e recomenda ações que podem melhorar o desempenho de sua carga de trabalho, fornecendo ações de ajuste inteligente e recomendações.</span><span class="sxs-lookup"><span data-stu-id="03a93-104">Azure SQL Database identifies potential problems in your database and recommends actions that can improve performance of your workload by providing intelligent tuning actions and recommendations.</span></span>

<span data-ttu-id="03a93-105">Para analisar o desempenho do seu banco de dados, use o bloco **Desempenho** na página Visão Geral ou navegue até a seção "Suporte + solução de problemas":</span><span class="sxs-lookup"><span data-stu-id="03a93-105">To review your database performance, use the **Performance** tile on the Overview page, or navigate down to "Support + troubleshooting" section:</span></span>

   ![Exibir Desempenho](./media/sql-database-performance/entries.png)

<span data-ttu-id="03a93-107">Na seção "Suporte + solução de problemas" é possível utilizar as seguintes páginas:</span><span class="sxs-lookup"><span data-stu-id="03a93-107">In the "Support + troubleshooting" section, you can use the following pages:</span></span>


1. <span data-ttu-id="03a93-108">[Visão geral de desempenho](#performance-overview) para monitorar o desempenho do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="03a93-108">[Performance overview](#performance-overview) to monitor performance of your database.</span></span> 
2. <span data-ttu-id="03a93-109">[Recomendações de desempenho](#performance-recommendations) para localizar as recomendações de desempenho que podem melhorar o desempenho da carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="03a93-109">[Performance recommendations](#performance-recommendations) to find performance recommendations that can improve performance of your workload.</span></span>
3. <span data-ttu-id="03a93-110">[Análise de desempenho de consultas](#query-performance-insight) para localizar as principais consultas de consumo de recursos.</span><span class="sxs-lookup"><span data-stu-id="03a93-110">[Query Performance Insight](#query-performance-insight) to find top resource consuming queries.</span></span>
4. <span data-ttu-id="03a93-111">[Ajuste automático](#automatic-tuning) para permitir que o Banco de Dados SQL do Azure otimize seu banco de dados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="03a93-111">[Automatic tuning](#automatic-tuning) to let Azure SQL Database automatically optimize your database.</span></span>

## <a name="performance-overview"></a><span data-ttu-id="03a93-112">Visão geral do desempenho</span><span class="sxs-lookup"><span data-stu-id="03a93-112">Performance Overview</span></span>
<span data-ttu-id="03a93-113">Essa exibição fornece um resumo do desempenho de seu banco de dados e lhe ajudará com ajustes e solução de problemas de desempenho.</span><span class="sxs-lookup"><span data-stu-id="03a93-113">This view provides a summary of your database performance, and helps you with performance tuning and troubleshooting.</span></span> 

![Desempenho](./media/sql-database-performance/performance.png)

* <span data-ttu-id="03a93-115">O bloco **Recomendações** fornece uma divisão das recomendações de ajuste para seu banco de dados (as três principais recomendações serão exibidas, se existirem mais).</span><span class="sxs-lookup"><span data-stu-id="03a93-115">The **Recommendations** tile provides a breakdown of tuning recommendations for your database (top three recommendations are shown if there are more).</span></span> <span data-ttu-id="03a93-116">Ao clicar nesse bloco, será direcionado para **[Recomendações de desempenho](#performance-recommendations)**.</span><span class="sxs-lookup"><span data-stu-id="03a93-116">Clicking this tile takes you to **[Performance recommendations](#performance-recommendations)**.</span></span> 
* <span data-ttu-id="03a93-117">O bloco **Atividade de ajuste** fornece um resumo das atividades de ajuste em andamento e concluídas para o banco de dados, oferecendo uma visão rápida do histórico de atividades de ajuste.</span><span class="sxs-lookup"><span data-stu-id="03a93-117">The **Tuning activity** tile provides a summary of the ongoing and completed tuning actions for your database, giving you a quick view into the history of tuning activity.</span></span> <span data-ttu-id="03a93-118">Clicar nesse bloco leva você para a exibição do histórico completo de ajustes do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="03a93-118">Clicking this tile takes you to the full tuning history view for your database.</span></span>
* <span data-ttu-id="03a93-119">O bloco **Ajuste automático** mostra a[configuração de ajuste automático](sql-database-automatic-tuning-enable.md) para o banco de dados (opções de ajuste que são aplicadas automaticamente ao banco de dados).</span><span class="sxs-lookup"><span data-stu-id="03a93-119">The **Auto-tuning** tile shows the [auto-tuning configuration](sql-database-automatic-tuning-enable.md) for your database (tuning options that are automatically applied to your database).</span></span> <span data-ttu-id="03a93-120">Clicar nesse bloco abre a caixa de diálogo de configuração de automação.</span><span class="sxs-lookup"><span data-stu-id="03a93-120">Clicking this tile opens the automation configuration dialog.</span></span>
* <span data-ttu-id="03a93-121">O bloco **Consultas de banco de dados** mostra o resumo do desempenho de consulta do banco de dados (uso geral de DTU e consultas com maior consumo de recursos).</span><span class="sxs-lookup"><span data-stu-id="03a93-121">The **Database queries** tile shows the summary of the query performance for your database (overall DTU usage and top resource consuming queries).</span></span> <span data-ttu-id="03a93-122">Ao clicar nesse bloco, será direcionado para **[Análise de Desempenho de Consultas](#query-performance-insight)**.</span><span class="sxs-lookup"><span data-stu-id="03a93-122">Clicking this tile takes you to **[Query Performance Insight](#query-performance-insight)**.</span></span>

## <a name="performance-recommendations"></a><span data-ttu-id="03a93-123">Recomendações de desempenho</span><span class="sxs-lookup"><span data-stu-id="03a93-123">Performance recommendations</span></span>
<span data-ttu-id="03a93-124">Esta página fornece [recomendações de ajuste](sql-database-advisor.md) inteligente que podem melhorar o desempenho do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="03a93-124">This page provides intelligent [tuning recommendations](sql-database-advisor.md) that can improve your database's performance.</span></span> <span data-ttu-id="03a93-125">Os seguintes tipos de recomendações são mostrados nesta página:</span><span class="sxs-lookup"><span data-stu-id="03a93-125">The following types of recommendations are shown on this page:</span></span>

* <span data-ttu-id="03a93-126">Recomendações sobre quais índices criar ou soltar.</span><span class="sxs-lookup"><span data-stu-id="03a93-126">Recommendations on which indexes to create or drop.</span></span>
* <span data-ttu-id="03a93-127">Recomendações quando problemas de esquema são identificados no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="03a93-127">Recommendations when schema issues are identified in the database.</span></span>
* <span data-ttu-id="03a93-128">Recomendações quando consultas podem se beneficiar de consultas parametrizadas.</span><span class="sxs-lookup"><span data-stu-id="03a93-128">Recommendations when queries can benefit from parameterized queries.</span></span>

![Desempenho](./media/sql-database-performance/recommendations.png)

<span data-ttu-id="03a93-130">Você também pode encontrar o histórico completo de ajuste de ações que foram aplicadas no passado.</span><span class="sxs-lookup"><span data-stu-id="03a93-130">You can also find complete history of tuning actions that were applied in the past.</span></span>

<span data-ttu-id="03a93-131">Saiba como localizar recomendações de desempenho de aplicativo no artigo [Localizar e aplicar recomendações de desempenho](sql-database-advisor-portal.md).</span><span class="sxs-lookup"><span data-stu-id="03a93-131">Learn how to find an apply performance recommendations in [Find and apply performance recommendations](sql-database-advisor-portal.md) article.</span></span>

## <a name="automatic-tuning"></a><span data-ttu-id="03a93-132">Ajuste automático</span><span class="sxs-lookup"><span data-stu-id="03a93-132">Automatic tuning</span></span>
<span data-ttu-id="03a93-133">O Bancos de Dados SQL do Azure pode ajustar o desempenho do banco de dados automaticamente, aplicando as [recomendações de desempenho](sql-database-advisor.md).</span><span class="sxs-lookup"><span data-stu-id="03a93-133">Azure SQL Databases can automatically tune database performance by applying [performance recommendations](sql-database-advisor.md).</span></span> <span data-ttu-id="03a93-134">Para saber mais, leia o artigo de [Ajuste automático](sql-database-automatic-tuning.md).</span><span class="sxs-lookup"><span data-stu-id="03a93-134">To learn more, read [Automatic tuning article](sql-database-automatic-tuning.md).</span></span> <span data-ttu-id="03a93-135">Para habilitá-lo, leia [como habilitar o ajuste automático](sql-database-automatic-tuning-enable.md).</span><span class="sxs-lookup"><span data-stu-id="03a93-135">To enable it, read [how to enable automatic tuning](sql-database-automatic-tuning-enable.md).</span></span>

## <a name="query-performance-insight"></a><span data-ttu-id="03a93-136">Análise de Desempenho de Consultas</span><span class="sxs-lookup"><span data-stu-id="03a93-136">Query Performance Insight</span></span>
<span data-ttu-id="03a93-137">[Análise de Desempenho de Consultas](sql-database-query-performance.md) permite que você gaste menos tempo solucionando problemas de desempenho de banco de dados, fornecendo o seguinte:</span><span class="sxs-lookup"><span data-stu-id="03a93-137">[Query Performance Insight](sql-database-query-performance.md) allows you to spend less time troubleshooting database performance by providing:</span></span>

* <span data-ttu-id="03a93-138">Mais informações sobre o consumo de recursos de bancos de dados (DTU).</span><span class="sxs-lookup"><span data-stu-id="03a93-138">Deeper insight into your databases resource (DTU) consumption.</span></span> 
* <span data-ttu-id="03a93-139">As consultas que mais consomem CPU, que potencialmente podem ser ajustadas para melhorar o desempenho.</span><span class="sxs-lookup"><span data-stu-id="03a93-139">The top CPU consuming queries, which can potentially be tuned for improved performance.</span></span> 
* <span data-ttu-id="03a93-140">A capacidade de fazer drill down nos detalhes de uma consulta.</span><span class="sxs-lookup"><span data-stu-id="03a93-140">The ability to drill down into the details of a query.</span></span> 

  ![painel de desempenho](./media/sql-database-query-performance/performance.png)

<span data-ttu-id="03a93-142">Localize mais informações sobre essa página no artigo  **[Como usar a Análise de Desempenho de Consultas](sql-database-query-performance.md)**.</span><span class="sxs-lookup"><span data-stu-id="03a93-142">Find more information about this page in the article **[How to use Query Performance Insight](sql-database-query-performance.md)**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="03a93-143">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="03a93-143">Additional resources</span></span>
* [<span data-ttu-id="03a93-144">Diretrizes de desempenho do Banco de Dados SQL do Azure para bancos de dados únicos</span><span class="sxs-lookup"><span data-stu-id="03a93-144">Azure SQL Database performance guidance for single databases</span></span>](sql-database-performance-guidance.md)
* [<span data-ttu-id="03a93-145">Quando um pool elástico deve ser usado?</span><span class="sxs-lookup"><span data-stu-id="03a93-145">When should an elastic pool be used?</span></span>](sql-database-elastic-pool-guidance.md)

