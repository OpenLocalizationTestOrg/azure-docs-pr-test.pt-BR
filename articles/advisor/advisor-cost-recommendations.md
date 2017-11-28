---
title: "recomendações do Advisor custo aaaAzure | Microsoft Docs"
description: "Use o custo de saudação do Azure Advisor toooptimize das implantações do Azure."
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
ms.openlocfilehash: 50f70c33a17f550c8753795435cdfddd51e409f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-cost-recommendations"></a><span data-ttu-id="ed935-103">Recomendações de custo do Advisor</span><span class="sxs-lookup"><span data-stu-id="ed935-103">Advisor Cost recommendations</span></span>

<span data-ttu-id="ed935-104">O Advisor ajuda você a otimizar e a reduzir seus gastos gerais com o Azure, identificando recursos ociosos e subutilizados.</span><span class="sxs-lookup"><span data-stu-id="ed935-104">Advisor helps you optimize and reduce your overall Azure spend by identifying idle and underutilized resources.</span></span> <span data-ttu-id="ed935-105">Você pode obter as recomendações de saudação custo **custo** guia no painel de Supervisor hello.</span><span class="sxs-lookup"><span data-stu-id="ed935-105">You can get cost recommendations from hello **Cost** tab on hello Advisor dashboard.</span></span>

![Guia Custo do Assistente](./media/advisor-cost-recommendations/advisor-cost-tab2.png)

## <a name="optimize-virtual-machine-spend-by-resizing-underutilized-instances"></a><span data-ttu-id="ed935-107">Otimizar o gasto da máquina virtual redimensionando instâncias subutilizadas</span><span class="sxs-lookup"><span data-stu-id="ed935-107">Optimize virtual machine spend by resizing underutilized instances</span></span> 
<span data-ttu-id="ed935-108">Embora determinados cenários de aplicativo podem resultar em baixa utilização por design, você geralmente pode economizar dinheiro, gerenciando o tamanho de saudação e número de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="ed935-108">Although certain application scenarios can result in low utilization by design, you can often save money by managing hello size and number of your virtual machines.</span></span> <span data-ttu-id="ed935-109">O Assistente monitora o uso da máquina virtual durante 14 dias e, depois, identifica as máquinas virtuais com baixa utilização.</span><span class="sxs-lookup"><span data-stu-id="ed935-109">Advisor monitors your virtual machine usage for 14 days and then identifies low-utilization virtual machines.</span></span> <span data-ttu-id="ed935-110">As máquinas virtuais cuja utilização da CPU é de 5% ou menos e cujo uso de rede é de 7 MB ou menos durante quatro ou mais dias são consideradas máquinas virtuais de baixa utilização.</span><span class="sxs-lookup"><span data-stu-id="ed935-110">Virtual machines whose CPU utilization is 5 percent or less and network usage is 7 MB or less for four or more days are considered low-utilization virtual machines.</span></span>

<span data-ttu-id="ed935-111">Mostra Advisor Olá custo estimado de continuar toorun sua máquina virtual, para que você possa escolher tooshut-para baixo ou redimensioná-la.</span><span class="sxs-lookup"><span data-stu-id="ed935-111">Advisor shows you hello estimated cost of continuing toorun your virtual machine, so that you can choose tooshut it down or resize it.</span></span>  

![Recomendações de custo do Advisor para redimensionamento de máquinas virtuais](./media/advisor-cost-recommendations/advisor-cost-resizevms.png)

## <a name="use-a-cost-effective-solution-toomanage-performance-goals-of-multiple-sql-databases"></a><span data-ttu-id="ed935-113">Use as metas de desempenho de toomanage uma solução econômica de vários bancos de dados SQL</span><span class="sxs-lookup"><span data-stu-id="ed935-113">Use a cost effective solution toomanage performance goals of multiple SQL databases</span></span>
<span data-ttu-id="ed935-114">O Advisor identifica as instâncias do SQL Server que podem se beneficiar da criação de pools de banco de dados elástico.</span><span class="sxs-lookup"><span data-stu-id="ed935-114">Advisor identifies SQL server instances that can benefit from creating elastic database pools.</span></span> <span data-ttu-id="ed935-115">Pools de banco de dados Elástico fornecem uma solução simples e econômica toomanage metas de desempenho de saudação de vários bancos de dados que têm vários padrões de uso.</span><span class="sxs-lookup"><span data-stu-id="ed935-115">Elastic database pools provide a simple, cost-effective solution toomanage hello performance goals of multiple databases that have varying usage patterns.</span></span> <span data-ttu-id="ed935-116">Para obter mais informações sobre os pools elásticos do Azure, consulte [O que é um pool elástico do Azure?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/).</span><span class="sxs-lookup"><span data-stu-id="ed935-116">For more information about Azure elastic pools, see [What is an Azure Elastic pool?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/).</span></span>

![Recomendações de custo do Advisor para pools de banco de dados elástico](./media/advisor-cost-recommendations/advisor-cost-elasticdbpools.png)

## <a name="how-tooaccess-cost-recommendations-in-azure-advisor"></a><span data-ttu-id="ed935-118">Como tooaccess custo recomendações do Advisor do Azure</span><span class="sxs-lookup"><span data-stu-id="ed935-118">How tooaccess cost recommendations in Azure Advisor</span></span>

1. <span data-ttu-id="ed935-119">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ed935-119">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="ed935-120">No painel esquerdo do hello, clique em **mais serviços**.</span><span class="sxs-lookup"><span data-stu-id="ed935-120">In hello left pane, click **More services**.</span></span>

3. <span data-ttu-id="ed935-121">Em Olá serviço painel de menu em **monitoramento e gerenciamento**, clique em **Advisor Azure**.</span><span class="sxs-lookup"><span data-stu-id="ed935-121">In hello service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="ed935-122">Olá Advisor painel é exibido.</span><span class="sxs-lookup"><span data-stu-id="ed935-122">hello Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="ed935-123">No painel do Advisor hello, clique em Olá **custo** guia.</span><span class="sxs-lookup"><span data-stu-id="ed935-123">On hello Advisor dashboard, click hello **Cost** tab.</span></span>

5. <span data-ttu-id="ed935-124">Selecione a assinatura Olá para o qual você deseja tooreceive recomendações e, em seguida, clique em **obter recomendações**.</span><span class="sxs-lookup"><span data-stu-id="ed935-124">Select hello subscription for which you want tooreceive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="ed935-125">tooaccess as recomendações do Advisor, você deve primeiro *registrar sua assinatura* com o Supervisor.</span><span class="sxs-lookup"><span data-stu-id="ed935-125">tooaccess Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="ed935-126">Uma assinatura é registrada quando um *assinatura proprietário* inicia Olá Olá de painel de controle e clica Advisor **obter recomendações** botão.</span><span class="sxs-lookup"><span data-stu-id="ed935-126">A subscription is registered when a *subscription Owner* launches hello Advisor dashboard and clicks hello **Get recommendations** button.</span></span> <span data-ttu-id="ed935-127">Essa é uma *operação única*.</span><span class="sxs-lookup"><span data-stu-id="ed935-127">This is a *one-time operation*.</span></span> <span data-ttu-id="ed935-128">Depois de Olá assinatura está registrada, você pode acessar as recomendações do Advisor como *proprietário*, *Colaborador*, ou *leitor* para uma assinatura de um grupo de recursos, ou um recurso específico.</span><span class="sxs-lookup"><span data-stu-id="ed935-128">After hello subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ed935-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ed935-129">Next steps</span></span>

<span data-ttu-id="ed935-130">toolearn mais informações sobre recomendações do Advisor, consulte:</span><span class="sxs-lookup"><span data-stu-id="ed935-130">toolearn more about Advisor recommendations, see:</span></span>
* [<span data-ttu-id="ed935-131">Introdução tooAdvisor</span><span class="sxs-lookup"><span data-stu-id="ed935-131">Introduction tooAdvisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="ed935-132">Introdução</span><span class="sxs-lookup"><span data-stu-id="ed935-132">Get Started</span></span>](advisor-get-started.md)
* [<span data-ttu-id="ed935-133">Recomendações de desempenho do Advisor</span><span class="sxs-lookup"><span data-stu-id="ed935-133">Advisor Performance recommendations</span></span>](advisor-cost-recommendations.md)
* [<span data-ttu-id="ed935-134">Recomendações de alta disponibilidade do Advisor</span><span class="sxs-lookup"><span data-stu-id="ed935-134">Advisor High Availability recommendations</span></span>](advisor-cost-recommendations.md)
* [<span data-ttu-id="ed935-135">Recomendações de segurança do Advisor</span><span class="sxs-lookup"><span data-stu-id="ed935-135">Advisor Security recommendations</span></span>](advisor-cost-recommendations.md)
