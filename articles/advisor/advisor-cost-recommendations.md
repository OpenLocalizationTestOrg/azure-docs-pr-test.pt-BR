---
title: "Recomendações de custo do Azure Advisor | Microsoft Docs"
description: "Use o Azure Advisor para otimizar o custo de suas implantações do Azure."
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
ms.openlocfilehash: 5eef2116f238b477fa8de46ce7b25728c393739c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="advisor-cost-recommendations"></a><span data-ttu-id="87040-103">Recomendações de custo do Advisor</span><span class="sxs-lookup"><span data-stu-id="87040-103">Advisor Cost recommendations</span></span>

<span data-ttu-id="87040-104">O Advisor ajuda você a otimizar e a reduzir seus gastos gerais com o Azure, identificando recursos ociosos e subutilizados.</span><span class="sxs-lookup"><span data-stu-id="87040-104">Advisor helps you optimize and reduce your overall Azure spend by identifying idle and underutilized resources.</span></span> <span data-ttu-id="87040-105">Você pode obter recomendações de custo na guia **Custo** no painel do Assistente.</span><span class="sxs-lookup"><span data-stu-id="87040-105">You can get cost recommendations from the **Cost** tab on the Advisor dashboard.</span></span>

![Guia Custo do Assistente](./media/advisor-cost-recommendations/advisor-cost-tab2.png)

## <a name="optimize-virtual-machine-spend-by-resizing-underutilized-instances"></a><span data-ttu-id="87040-107">Otimizar o gasto da máquina virtual redimensionando instâncias subutilizadas</span><span class="sxs-lookup"><span data-stu-id="87040-107">Optimize virtual machine spend by resizing underutilized instances</span></span> 
<span data-ttu-id="87040-108">Embora alguns cenários de aplicativos possam resultar na baixa utilização por design, normalmente, é possível economizar dinheiro gerenciando o tamanho e o número de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="87040-108">Although certain application scenarios can result in low utilization by design, you can often save money by managing the size and number of your virtual machines.</span></span> <span data-ttu-id="87040-109">O Assistente monitora o uso da máquina virtual durante 14 dias e, depois, identifica as máquinas virtuais com baixa utilização.</span><span class="sxs-lookup"><span data-stu-id="87040-109">Advisor monitors your virtual machine usage for 14 days and then identifies low-utilization virtual machines.</span></span> <span data-ttu-id="87040-110">As máquinas virtuais cuja utilização da CPU é de 5% ou menos e cujo uso de rede é de 7 MB ou menos durante quatro ou mais dias são consideradas máquinas virtuais de baixa utilização.</span><span class="sxs-lookup"><span data-stu-id="87040-110">Virtual machines whose CPU utilization is 5 percent or less and network usage is 7 MB or less for four or more days are considered low-utilization virtual machines.</span></span>

<span data-ttu-id="87040-111">O Assistente mostra o custo estimado da continuação da execução da máquina virtual, de forma que você possa optar por desligá-la ou redimensioná-la.</span><span class="sxs-lookup"><span data-stu-id="87040-111">Advisor shows you the estimated cost of continuing to run your virtual machine, so that you can choose to shut it down or resize it.</span></span>  

![Recomendações de custo do Advisor para redimensionamento de máquinas virtuais](./media/advisor-cost-recommendations/advisor-cost-resizevms.png)

## <a name="use-a-cost-effective-solution-to-manage-performance-goals-of-multiple-sql-databases"></a><span data-ttu-id="87040-113">Usar uma solução econômica para gerenciar as metas de desempenho de vários bancos de dados SQL</span><span class="sxs-lookup"><span data-stu-id="87040-113">Use a cost effective solution to manage performance goals of multiple SQL databases</span></span>
<span data-ttu-id="87040-114">O Advisor identifica as instâncias do SQL Server que podem se beneficiar da criação de pools de banco de dados elástico.</span><span class="sxs-lookup"><span data-stu-id="87040-114">Advisor identifies SQL server instances that can benefit from creating elastic database pools.</span></span> <span data-ttu-id="87040-115">Pools de banco de dados elástico fornecem uma solução simples e econômica para gerenciar as metas de desempenho de vários bancos de dados que têm padrões de uso variáveis.</span><span class="sxs-lookup"><span data-stu-id="87040-115">Elastic database pools provide a simple, cost-effective solution to manage the performance goals of multiple databases that have varying usage patterns.</span></span> <span data-ttu-id="87040-116">Para obter mais informações sobre os pools elásticos do Azure, consulte [O que é um pool elástico do Azure?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/).</span><span class="sxs-lookup"><span data-stu-id="87040-116">For more information about Azure elastic pools, see [What is an Azure Elastic pool?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/).</span></span>

![Recomendações de custo do Advisor para pools de banco de dados elástico](./media/advisor-cost-recommendations/advisor-cost-elasticdbpools.png)

## <a name="how-to-access-cost-recommendations-in-azure-advisor"></a><span data-ttu-id="87040-118">Como acessar as recomendações de custo no Azure Advisor</span><span class="sxs-lookup"><span data-stu-id="87040-118">How to access cost recommendations in Azure Advisor</span></span>

1. <span data-ttu-id="87040-119">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="87040-119">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="87040-120">No painel esquerdo, clique em **Mais serviços**.</span><span class="sxs-lookup"><span data-stu-id="87040-120">In the left pane, click **More services**.</span></span>

3. <span data-ttu-id="87040-121">No painel do menu de serviço, em **Monitoramento e Gerenciamento**, clique em **Assistente do Azure**.</span><span class="sxs-lookup"><span data-stu-id="87040-121">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="87040-122">O painel Assistente é exibido.</span><span class="sxs-lookup"><span data-stu-id="87040-122">The Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="87040-123">No painel do Assistente, clique na guia **Custo**.</span><span class="sxs-lookup"><span data-stu-id="87040-123">On the Advisor dashboard, click the **Cost** tab.</span></span>

5. <span data-ttu-id="87040-124">Selecione a assinatura para a qual você deseja receber recomendações e, em seguida, clique em **Obter recomendações**.</span><span class="sxs-lookup"><span data-stu-id="87040-124">Select the subscription for which you want to receive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="87040-125">Para acessar as recomendações do Assistente, você deve primeiro *registrar sua assinatura* no Assistente.</span><span class="sxs-lookup"><span data-stu-id="87040-125">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="87040-126">Uma assinatura é registrada quando um *Proprietário de assinatura* inicia o painel do Assistente e clica no botão **Obter recomendações**.</span><span class="sxs-lookup"><span data-stu-id="87040-126">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="87040-127">Essa é uma *operação única*.</span><span class="sxs-lookup"><span data-stu-id="87040-127">This is a *one-time operation*.</span></span> <span data-ttu-id="87040-128">Depois que a assinatura for registrada, você poderá acessar as recomendações do Assistente como *Proprietário*, *Colaborador* ou *Leitor* de uma assinatura, um grupo de recursos ou um recurso específico.</span><span class="sxs-lookup"><span data-stu-id="87040-128">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="87040-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="87040-129">Next steps</span></span>

<span data-ttu-id="87040-130">Para saber mais sobre as recomendações do Assistente, consulte:</span><span class="sxs-lookup"><span data-stu-id="87040-130">To learn more about Advisor recommendations, see:</span></span>
* [<span data-ttu-id="87040-131">Introdução ao Advisor</span><span class="sxs-lookup"><span data-stu-id="87040-131">Introduction to Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="87040-132">Introdução</span><span class="sxs-lookup"><span data-stu-id="87040-132">Get Started</span></span>](advisor-get-started.md)
* [<span data-ttu-id="87040-133">Recomendações de desempenho do Advisor</span><span class="sxs-lookup"><span data-stu-id="87040-133">Advisor Performance recommendations</span></span>](advisor-cost-recommendations.md)
* [<span data-ttu-id="87040-134">Recomendações de alta disponibilidade do Advisor</span><span class="sxs-lookup"><span data-stu-id="87040-134">Advisor High Availability recommendations</span></span>](advisor-cost-recommendations.md)
* [<span data-ttu-id="87040-135">Recomendações de segurança do Advisor</span><span class="sxs-lookup"><span data-stu-id="87040-135">Advisor Security recommendations</span></span>](advisor-cost-recommendations.md)
