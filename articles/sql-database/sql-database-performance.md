---
title: aaaMonitor e melhorar o desempenho - banco de dados do SQL Azure | Microsoft Docs
description: "saudação de que banco de dados SQL do Azure fornece desempenho ferramentas toohelp identificar áreas que podem melhorar o desempenho da consulta atual."
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
ms.openlocfilehash: 84b8a1bc62698a29deb49e765f208bd7e14d0870
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-improve-performance"></a><span data-ttu-id="8e69e-103">Monitorar e melhorar o desempenho</span><span class="sxs-lookup"><span data-stu-id="8e69e-103">Monitor and improve performance</span></span>
<span data-ttu-id="8e69e-104">O Banco de Dados SQL do Azure identifica possíveis problemas em seu banco de dados e recomenda ações que podem melhorar o desempenho de sua carga de trabalho, fornecendo ações de ajuste inteligente e recomendações.</span><span class="sxs-lookup"><span data-stu-id="8e69e-104">Azure SQL Database identifies potential problems in your database and recommends actions that can improve performance of your workload by providing intelligent tuning actions and recommendations.</span></span>

<span data-ttu-id="8e69e-105">tooreview o desempenho do banco de dados, use Olá **desempenho** lado a lado na página de visão geral de saudação ou navegue para baixo demais "Suporte + solução de problemas" seção:</span><span class="sxs-lookup"><span data-stu-id="8e69e-105">tooreview your database performance, use hello **Performance** tile on hello Overview page, or navigate down too"Support + troubleshooting" section:</span></span>

   ![Exibir Desempenho](./media/sql-database-performance/entries.png)

<span data-ttu-id="8e69e-107">Na seção hello "Suporte + solução de problemas", você pode usar o hello páginas a seguir:</span><span class="sxs-lookup"><span data-stu-id="8e69e-107">In hello "Support + troubleshooting" section, you can use hello following pages:</span></span>


1. <span data-ttu-id="8e69e-108">[Visão geral do desempenho](#performance-overview) toomonitor o desempenho do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="8e69e-108">[Performance overview](#performance-overview) toomonitor performance of your database.</span></span> 
2. <span data-ttu-id="8e69e-109">[Recomendações de desempenho](#performance-recommendations) toofind recomendações de desempenho que podem melhorar o desempenho da carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="8e69e-109">[Performance recommendations](#performance-recommendations) toofind performance recommendations that can improve performance of your workload.</span></span>
3. <span data-ttu-id="8e69e-110">[Análise de desempenho de consulta](#query-performance-insight) toofind principais consultas de consumo.</span><span class="sxs-lookup"><span data-stu-id="8e69e-110">[Query Performance Insight](#query-performance-insight) toofind top resource consuming queries.</span></span>
4. <span data-ttu-id="8e69e-111">[Ajuste automático](#automatic-tuning) toolet banco de dados do SQL Azure automaticamente otimizar seu banco de dados.</span><span class="sxs-lookup"><span data-stu-id="8e69e-111">[Automatic tuning](#automatic-tuning) toolet Azure SQL Database automatically optimize your database.</span></span>

## <a name="performance-overview"></a><span data-ttu-id="8e69e-112">Visão geral do desempenho</span><span class="sxs-lookup"><span data-stu-id="8e69e-112">Performance Overview</span></span>
<span data-ttu-id="8e69e-113">Essa exibição fornece um resumo do desempenho de seu banco de dados e lhe ajudará com ajustes e solução de problemas de desempenho.</span><span class="sxs-lookup"><span data-stu-id="8e69e-113">This view provides a summary of your database performance, and helps you with performance tuning and troubleshooting.</span></span> 

![Desempenho](./media/sql-database-performance/performance.png)

* <span data-ttu-id="8e69e-115">Olá **recomendações** lado a lado fornece uma análise de ajuste recomendações para seu banco de dados (a três principais recomendações são mostradas se há mais).</span><span class="sxs-lookup"><span data-stu-id="8e69e-115">hello **Recommendations** tile provides a breakdown of tuning recommendations for your database (top three recommendations are shown if there are more).</span></span> <span data-ttu-id="8e69e-116">Ao clicar nesse bloco você irá muito**[recomendações de desempenho](#performance-recommendations)**.</span><span class="sxs-lookup"><span data-stu-id="8e69e-116">Clicking this tile takes you too**[Performance recommendations](#performance-recommendations)**.</span></span> 
* <span data-ttu-id="8e69e-117">Olá **ajuste atividade** lado a lado fornece um resumo da saudação em andamento e concluída ajuste ações para o banco de dados, dando a você uma exibição rápida no histórico de saudação do ajuste de atividade.</span><span class="sxs-lookup"><span data-stu-id="8e69e-117">hello **Tuning activity** tile provides a summary of hello ongoing and completed tuning actions for your database, giving you a quick view into hello history of tuning activity.</span></span> <span data-ttu-id="8e69e-118">Clicar nesse bloco leva você toohello completo ajuste o modo de exibição de histórico para seu banco de dados.</span><span class="sxs-lookup"><span data-stu-id="8e69e-118">Clicking this tile takes you toohello full tuning history view for your database.</span></span>
* <span data-ttu-id="8e69e-119">Olá **auto-ajuste** bloco mostra Olá [autoajuste da configuração](sql-database-automatic-tuning-enable.md) para seu banco de dados (ajuste opções tooyour aplicadas automaticamente no banco de dados).</span><span class="sxs-lookup"><span data-stu-id="8e69e-119">hello **Auto-tuning** tile shows hello [auto-tuning configuration](sql-database-automatic-tuning-enable.md) for your database (tuning options that are automatically applied tooyour database).</span></span> <span data-ttu-id="8e69e-120">Clicar neste bloco abre a caixa de diálogo de configuração de automação hello.</span><span class="sxs-lookup"><span data-stu-id="8e69e-120">Clicking this tile opens hello automation configuration dialog.</span></span>
* <span data-ttu-id="8e69e-121">Olá **consultas de banco de dados** bloco mostra Olá resumo de desempenho de consulta de saudação do banco de dados (geral DTU uso e principais consultas de consumo).</span><span class="sxs-lookup"><span data-stu-id="8e69e-121">hello **Database queries** tile shows hello summary of hello query performance for your database (overall DTU usage and top resource consuming queries).</span></span> <span data-ttu-id="8e69e-122">Ao clicar nesse bloco você irá muito**[Query Performance Insight](#query-performance-insight)**.</span><span class="sxs-lookup"><span data-stu-id="8e69e-122">Clicking this tile takes you too**[Query Performance Insight](#query-performance-insight)**.</span></span>

## <a name="performance-recommendations"></a><span data-ttu-id="8e69e-123">Recomendações do desempenho</span><span class="sxs-lookup"><span data-stu-id="8e69e-123">Performance recommendations</span></span>
<span data-ttu-id="8e69e-124">Esta página fornece [recomendações de ajuste](sql-database-advisor.md) inteligente que podem melhorar o desempenho do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="8e69e-124">This page provides intelligent [tuning recommendations](sql-database-advisor.md) that can improve your database's performance.</span></span> <span data-ttu-id="8e69e-125">Olá tipos das recomendações a seguir é mostrado nesta página:</span><span class="sxs-lookup"><span data-stu-id="8e69e-125">hello following types of recommendations are shown on this page:</span></span>

* <span data-ttu-id="8e69e-126">Recomendações sobre quais índices toocreate ou drop.</span><span class="sxs-lookup"><span data-stu-id="8e69e-126">Recommendations on which indexes toocreate or drop.</span></span>
* <span data-ttu-id="8e69e-127">Recomendações quando problemas de esquema são identificados no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="8e69e-127">Recommendations when schema issues are identified in hello database.</span></span>
* <span data-ttu-id="8e69e-128">Recomendações quando consultas podem se beneficiar de consultas parametrizadas.</span><span class="sxs-lookup"><span data-stu-id="8e69e-128">Recommendations when queries can benefit from parameterized queries.</span></span>

![Desempenho](./media/sql-database-performance/recommendations.png)

<span data-ttu-id="8e69e-130">Você também pode encontrar o histórico completo de ajuste de ações que foram aplicadas no hello anterior.</span><span class="sxs-lookup"><span data-stu-id="8e69e-130">You can also find complete history of tuning actions that were applied in hello past.</span></span>

<span data-ttu-id="8e69e-131">Saiba como toofind um aplicar recomendações de desempenho [localizar e aplicar recomendações de desempenho](sql-database-advisor-portal.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="8e69e-131">Learn how toofind an apply performance recommendations in [Find and apply performance recommendations](sql-database-advisor-portal.md) article.</span></span>

## <a name="automatic-tuning"></a><span data-ttu-id="8e69e-132">Ajuste automático</span><span class="sxs-lookup"><span data-stu-id="8e69e-132">Automatic tuning</span></span>
<span data-ttu-id="8e69e-133">O Bancos de Dados SQL do Azure pode ajustar o desempenho do banco de dados automaticamente, aplicando as [recomendações de desempenho](sql-database-advisor.md).</span><span class="sxs-lookup"><span data-stu-id="8e69e-133">Azure SQL Databases can automatically tune database performance by applying [performance recommendations](sql-database-advisor.md).</span></span> <span data-ttu-id="8e69e-134">mais, leia toolearn [artigo ajuste automático](sql-database-automatic-tuning.md).</span><span class="sxs-lookup"><span data-stu-id="8e69e-134">toolearn more, read [Automatic tuning article](sql-database-automatic-tuning.md).</span></span> <span data-ttu-id="8e69e-135">tooenable, ler [como o ajuste automático tooenable](sql-database-automatic-tuning-enable.md).</span><span class="sxs-lookup"><span data-stu-id="8e69e-135">tooenable it, read [how tooenable automatic tuning](sql-database-automatic-tuning-enable.md).</span></span>

## <a name="query-performance-insight"></a><span data-ttu-id="8e69e-136">Análise de desempenho de consultas</span><span class="sxs-lookup"><span data-stu-id="8e69e-136">Query Performance Insight</span></span>
<span data-ttu-id="8e69e-137">[Análise de desempenho de consulta](sql-database-query-performance.md) permite que você toospend menos tempo Solucionando problemas de desempenho de banco de dados, fornecendo:</span><span class="sxs-lookup"><span data-stu-id="8e69e-137">[Query Performance Insight](sql-database-query-performance.md) allows you toospend less time troubleshooting database performance by providing:</span></span>

* <span data-ttu-id="8e69e-138">Mais informações sobre o consumo de recursos de bancos de dados (DTU).</span><span class="sxs-lookup"><span data-stu-id="8e69e-138">Deeper insight into your databases resource (DTU) consumption.</span></span> 
* <span data-ttu-id="8e69e-139">Olá principais consumidores de CPU consultas, que potencialmente podem ser ajustadas para melhorar o desempenho.</span><span class="sxs-lookup"><span data-stu-id="8e69e-139">hello top CPU consuming queries, which can potentially be tuned for improved performance.</span></span> 
* <span data-ttu-id="8e69e-140">Olá toodrill de capacidade para baixo em detalhes de saudação de uma consulta.</span><span class="sxs-lookup"><span data-stu-id="8e69e-140">hello ability toodrill down into hello details of a query.</span></span> 

  ![painel de desempenho](./media/sql-database-query-performance/performance.png)

<span data-ttu-id="8e69e-142">Encontre mais informações sobre esta página no artigo Olá  **[como toouse Query Performance Insight](sql-database-query-performance.md)**.</span><span class="sxs-lookup"><span data-stu-id="8e69e-142">Find more information about this page in hello article **[How toouse Query Performance Insight](sql-database-query-performance.md)**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8e69e-143">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="8e69e-143">Additional resources</span></span>
* [<span data-ttu-id="8e69e-144">Diretrizes de desempenho do Banco de Dados SQL do Azure para bancos de dados únicos</span><span class="sxs-lookup"><span data-stu-id="8e69e-144">Azure SQL Database performance guidance for single databases</span></span>](sql-database-performance-guidance.md)
* [<span data-ttu-id="8e69e-145">Quando um pool elástico deve ser usado?</span><span class="sxs-lookup"><span data-stu-id="8e69e-145">When should an elastic pool be used?</span></span>](sql-database-elastic-pool-guidance.md)

