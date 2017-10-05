---
title: "Recomendações de desempenho do Azure Advisor | Microsoft Docs"
description: "Use o Assistente para otimizar o desempenho das implantações do Azure."
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: 5fb86c60b2d1f258dde5636ff8854b6f30f7f1c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="advisor-performance-recommendations"></a><span data-ttu-id="501f1-103">Recomendações de desempenho do Advisor</span><span class="sxs-lookup"><span data-stu-id="501f1-103">Advisor Performance recommendations</span></span>

<span data-ttu-id="501f1-104">As recomendações de desempenho do Assistente do Azure ajudam a melhorar a velocidade e a capacidade de resposta dos aplicativos críticos para os negócios.</span><span class="sxs-lookup"><span data-stu-id="501f1-104">Azure Advisor performance recommendations help improve the speed and responsiveness of your business-critical applications.</span></span> <span data-ttu-id="501f1-105">Você pode obter recomendações de desempenho do Assistente na guia **Desempenho** do painel do Assistente.</span><span class="sxs-lookup"><span data-stu-id="501f1-105">You can get performance recommendations from Advisor on the **Performance** tab of the Advisor dashboard.</span></span>

![guia Desempenho do Advisor](./media/advisor-performance-recommendations/advisor-performance-tab.png)

## <a name="improve-database-performance-with-sql-db-advisor"></a><span data-ttu-id="501f1-107">Melhorar o desempenho do banco de dados com o Assistente do BD SQL</span><span class="sxs-lookup"><span data-stu-id="501f1-107">Improve database performance with SQL DB Advisor</span></span>

<span data-ttu-id="501f1-108">O Advisor fornece uma exibição consistente e consolidada de recomendações para todos os seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="501f1-108">Advisor provides you with a consistent, consolidated view of recommendations for all your Azure resources.</span></span> <span data-ttu-id="501f1-109">Ele se integra ao Advisor do Banco de Dados SQL para fornecer recomendações de melhoria de desempenho para o banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="501f1-109">It integrates with SQL Database Advisor to bring you recommendations for improving the performance of your SQL Azure database.</span></span> <span data-ttu-id="501f1-110">O Advisor do Banco de Dados SQL avalia o desempenho dos bancos de dados do SQL Azure analisando o histórico de uso.</span><span class="sxs-lookup"><span data-stu-id="501f1-110">SQL Database Advisor assesses the performance of your SQL Azure databases by analyzing your usage history.</span></span> <span data-ttu-id="501f1-111">Em seguida, ele oferece recomendações que são mais adequadas para execução da carga de trabalho típica do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="501f1-111">It then offers recommendations that are best suited for running the database’s typical workload.</span></span> 

> [!NOTE]
> <span data-ttu-id="501f1-112">Para obter recomendações, um banco de dados deve ter aproximadamente uma semana de uso e dentro dessa semana deve haver atividades consistentes.</span><span class="sxs-lookup"><span data-stu-id="501f1-112">To get recommendations, a database must have about a week of usage, and within that week there must be some consistent activity.</span></span> <span data-ttu-id="501f1-113">O Assistente do Banco de Dados SQL pode ser otimizado com mais facilidade para padrões de consulta consistentes do que para intermitências irregulares de atividade.</span><span class="sxs-lookup"><span data-stu-id="501f1-113">SQL Database Advisor can optimize more easily for consistent query patterns than for random bursts of activity.</span></span>

<span data-ttu-id="501f1-114">Para obter mais informações sobre o Assistente do Banco de Dados SQL, consulte [Assistente do Banco de Dados SQL](https://azure.microsoft.com/en-us/documentation/articles/sql-database-advisor/).</span><span class="sxs-lookup"><span data-stu-id="501f1-114">For more information about SQL Database Advisor, see [SQL Database Advisor](https://azure.microsoft.com/en-us/documentation/articles/sql-database-advisor/).</span></span>

![Recomendações do banco de dados SQL](./media/advisor-performance-recommendations/advisor-performance-sql.png)

## <a name="improve-redis-cache-performance-and-reliability"></a><span data-ttu-id="501f1-116">Melhorar o desempenho e a confiabilidade do Cache Redis</span><span class="sxs-lookup"><span data-stu-id="501f1-116">Improve Redis Cache performance and reliability</span></span>

<span data-ttu-id="501f1-117">O Assistente identifica as instâncias do Cache Redis nas quais o desempenho pode ser prejudicado por alto uso de memória, carga do servidor, largura de banda da rede ou grande número de conexões de cliente.</span><span class="sxs-lookup"><span data-stu-id="501f1-117">Advisor identifies Redis Cache instances where performance may be adversely affected by high memory usage, server load, network bandwidth, or a large number of client connections.</span></span> <span data-ttu-id="501f1-118">O Assistente também fornece recomendações de melhores práticas para ajudá-lo a evitar possíveis problemas.</span><span class="sxs-lookup"><span data-stu-id="501f1-118">Advisor also provides best practices recommendations to help you avoid potential issues.</span></span> <span data-ttu-id="501f1-119">Para saber mais sobre recomendações do Cache Redis, veja [Advisor do Cache Redis](https://azure.microsoft.com/en-us/documentation/articles/cache-configure/#redis-cache-advisor).</span><span class="sxs-lookup"><span data-stu-id="501f1-119">For more information about Redis Cache recommendations, see [Redis Cache Advisor](https://azure.microsoft.com/en-us/documentation/articles/cache-configure/#redis-cache-advisor).</span></span>


## <a name="improve-app-service-performance-and-reliability"></a><span data-ttu-id="501f1-120">Melhorar o desempenho e a confiabilidade do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="501f1-120">Improve App Service performance and reliability</span></span>

<span data-ttu-id="501f1-121">O Azure Advisor integra as práticas recomendadas para melhorar sua experiência com os Serviços de Aplicativos e descobrir recursos relevantes de plataforma.</span><span class="sxs-lookup"><span data-stu-id="501f1-121">Azure Advisor integrates best practices recommendations for improving your App Services experience and discovering relevant platform capabilities.</span></span> <span data-ttu-id="501f1-122">Os exemplos de recomendações dos Serviços de Aplicativos são:</span><span class="sxs-lookup"><span data-stu-id="501f1-122">Examples of App Services recommendations are:</span></span>
* <span data-ttu-id="501f1-123">Detecção de instâncias nas quais os recursos de memória ou de CPU são esgotados por tempos de execução de aplicativo com opções de mitigação.</span><span class="sxs-lookup"><span data-stu-id="501f1-123">Detection of instances where memory or CPU resources are exhausted by app runtimes with mitigation options.</span></span>
* <span data-ttu-id="501f1-124">Detecção de instâncias nas quais a disposição de recursos como aplicativos Web e bancos de dados pode melhorar o desempenho e reduzir custos.</span><span class="sxs-lookup"><span data-stu-id="501f1-124">Detection of instances where collocating resources like web apps and databases can improve performance and lower cost.</span></span> 

<span data-ttu-id="501f1-125">Para saber mais sobre recomendações de Serviços de Aplicativos, veja [Práticas recomendadas para o Serviço de Aplicativo do Azure](https://azure.microsoft.com/en-us/documentation/articles/app-service-best-practices/).</span><span class="sxs-lookup"><span data-stu-id="501f1-125">For more information about App Services recommendations, see [Best Practices for Azure App Service](https://azure.microsoft.com/en-us/documentation/articles/app-service-best-practices/).</span></span>
<span data-ttu-id="501f1-126">![Recomendações dos Serviços de Aplicativos](./media/advisor-performance-recommendations/advisor-performance-app-service.png)</span><span class="sxs-lookup"><span data-stu-id="501f1-126">![App Services recommendations](./media/advisor-performance-recommendations/advisor-performance-app-service.png)</span></span>

## <a name="how-to-access-performance-recommendations-in-advisor"></a><span data-ttu-id="501f1-127">Como acessar as recomendações de desempenho no Advisor</span><span class="sxs-lookup"><span data-stu-id="501f1-127">How to access Performance recommendations in Advisor</span></span>

1. <span data-ttu-id="501f1-128">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="501f1-128">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="501f1-129">No painel esquerdo, clique em **Mais serviços**.</span><span class="sxs-lookup"><span data-stu-id="501f1-129">In the left pane, click **More services**.</span></span>

3. <span data-ttu-id="501f1-130">No painel do menu de serviço, em **Monitoramento e Gerenciamento**, clique em **Assistente do Azure**.</span><span class="sxs-lookup"><span data-stu-id="501f1-130">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="501f1-131">O painel Assistente é exibido.</span><span class="sxs-lookup"><span data-stu-id="501f1-131">The Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="501f1-132">No painel do Assistente, clique na guia **Desempenho**.</span><span class="sxs-lookup"><span data-stu-id="501f1-132">On the Advisor dashboard, click the **Performance** tab.</span></span>

5. <span data-ttu-id="501f1-133">Selecione a assinatura para a qual você deseja receber recomendações e, em seguida, clique em **Obter recomendações**.</span><span class="sxs-lookup"><span data-stu-id="501f1-133">Select the subscription for which you want to receive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="501f1-134">Para acessar as recomendações do Assistente, você deve primeiro *registrar sua assinatura* no Assistente.</span><span class="sxs-lookup"><span data-stu-id="501f1-134">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="501f1-135">Uma assinatura é registrada quando um *Proprietário de assinatura* inicia o painel do Assistente e clica no botão **Obter recomendações**.</span><span class="sxs-lookup"><span data-stu-id="501f1-135">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="501f1-136">Essa é uma *operação única*.</span><span class="sxs-lookup"><span data-stu-id="501f1-136">This is a *one-time operation*.</span></span> <span data-ttu-id="501f1-137">Depois que a assinatura for registrada, você poderá acessar as recomendações do Assistente como *Proprietário*, *Colaborador* ou *Leitor* de uma assinatura, um grupo de recursos ou um recurso específico.</span><span class="sxs-lookup"><span data-stu-id="501f1-137">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="501f1-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="501f1-138">Next steps</span></span>

<span data-ttu-id="501f1-139">Para saber mais sobre as recomendações do Assistente, consulte:</span><span class="sxs-lookup"><span data-stu-id="501f1-139">To learn more about Advisor recommendations, see:</span></span>

* [<span data-ttu-id="501f1-140">Introdução ao Advisor</span><span class="sxs-lookup"><span data-stu-id="501f1-140">Introduction to Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="501f1-141">Introdução ao Advisor</span><span class="sxs-lookup"><span data-stu-id="501f1-141">Get started with Advisor</span></span>](advisor-get-started.md)
* [<span data-ttu-id="501f1-142">Recomendações de custo do Advisor</span><span class="sxs-lookup"><span data-stu-id="501f1-142">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="501f1-143">Recomendações de alta disponibilidade do Advisor</span><span class="sxs-lookup"><span data-stu-id="501f1-143">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)
* [<span data-ttu-id="501f1-144">Recomendações de segurança do Advisor</span><span class="sxs-lookup"><span data-stu-id="501f1-144">Advisor Security recommendations</span></span>](advisor-security-recommendations.md)

