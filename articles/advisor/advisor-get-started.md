---
title: "Introdução ao Azure Advisor | Microsoft Docs"
description: "Introdução ao Azure Advisor."
services: advisor
documentationcenter: NA
author: manbeenkohli
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/10/2017
ms.author: makohli
ms.openlocfilehash: a662841bebda460d4225e080f16705b3f16fdc46
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-advisor"></a><span data-ttu-id="d2b87-103">Introdução ao Azure Advisor</span><span class="sxs-lookup"><span data-stu-id="d2b87-103">Get started with Azure Advisor</span></span>

<span data-ttu-id="d2b87-104">Saiba como acessar o Assistente por meio do portal do Azure e obter, implementar, pesquisar e atualizar recomendações.</span><span class="sxs-lookup"><span data-stu-id="d2b87-104">Learn how to access Advisor through the Azure portal, get recommendations, implement recommendations, search for recommendations, and refresh recommendations.</span></span>

## <a name="get-advisor-recommendations"></a><span data-ttu-id="d2b87-105">Obter recomendações do Advisor</span><span class="sxs-lookup"><span data-stu-id="d2b87-105">Get Advisor recommendations</span></span>

1. <span data-ttu-id="d2b87-106">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d2b87-106">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="d2b87-107">No painel esquerdo, clique em **Mais serviços**.</span><span class="sxs-lookup"><span data-stu-id="d2b87-107">In the left pane, click **More services**.</span></span>

3. <span data-ttu-id="d2b87-108">No painel do menu de serviço, em **Monitoramento e Gerenciamento**, clique em **Assistente do Azure**.</span><span class="sxs-lookup"><span data-stu-id="d2b87-108">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="d2b87-109">O painel Assistente é exibido.</span><span class="sxs-lookup"><span data-stu-id="d2b87-109">The Advisor dashboard is displayed.</span></span>

   ![Acessar o Azure Advisor usando o Portal do Azure](./media/advisor-overview/advisor-azure-portal-menu.png) 

4. <span data-ttu-id="d2b87-111">No painel do Assistente, selecione a assinatura para a qual você deseja receber recomendações.</span><span class="sxs-lookup"><span data-stu-id="d2b87-111">On the Advisor dashboard, select the subscription for which you want to receive recommendations.</span></span>  
<span data-ttu-id="d2b87-112">O painel do Advisor exibe recomendações personalizadas para uma assinatura selecionada.</span><span class="sxs-lookup"><span data-stu-id="d2b87-112">The Advisor dashboard displays personalized recommendations for a selected subscription.</span></span> 

5. <span data-ttu-id="d2b87-113">Para obter recomendações para uma categoria específica, clique em uma das guias: **Alta Disponibilidade**, **Segurança**, **Desempenho** ou **Custo**.</span><span class="sxs-lookup"><span data-stu-id="d2b87-113">To get recommendations for a particular category, click one of the tabs: **High Availability**, **Security**, **Performance**, or **Cost**.</span></span>
 
> [!NOTE]
> <span data-ttu-id="d2b87-114">Para acessar as recomendações do Assistente, você deve primeiro *registrar sua assinatura* no Assistente.</span><span class="sxs-lookup"><span data-stu-id="d2b87-114">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="d2b87-115">Uma assinatura é registrada quando um *Proprietário de assinatura* inicia o painel do Assistente e clica no botão **Obter recomendações**.</span><span class="sxs-lookup"><span data-stu-id="d2b87-115">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="d2b87-116">Essa é uma *operação única*.</span><span class="sxs-lookup"><span data-stu-id="d2b87-116">This is a *one-time operation*.</span></span> <span data-ttu-id="d2b87-117">Depois que a assinatura for registrada, você poderá acessar as recomendações do Assistente como *Proprietário*, *Colaborador* ou *Leitor* de uma assinatura, um grupo de recursos ou um recurso específico.</span><span class="sxs-lookup"><span data-stu-id="d2b87-117">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

  ![Painel do Azure Advisor](./media/advisor-overview/advisor-all-tab.png)

## <a name="get-advisor-recommendation-details-and-implement-a-solution"></a><span data-ttu-id="d2b87-119">Obter detalhes da recomendação do Assistente e implementar uma recomendação</span><span class="sxs-lookup"><span data-stu-id="d2b87-119">Get Advisor recommendation details, and implement a solution</span></span>

<span data-ttu-id="d2b87-120">A folha **Recomendação** do Assistente oferece mais informações sobre a recomendação.</span><span class="sxs-lookup"><span data-stu-id="d2b87-120">The **Recommendation** blade in Advisor offers additional information about the recommendation.</span></span> 

1. <span data-ttu-id="d2b87-121">Entre no [portal do Azure](https://portal.azure.com) e inicie o [Assistente do Azure](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="d2b87-121">Sign in to the [Azure portal](https://portal.azure.com), and then start [Azure Advisor](https://aka.ms/azureadvisordashboard).</span></span>

2. <span data-ttu-id="d2b87-122">No painel **Recomendações do Assistente**, clique em **Obter recomendações**.</span><span class="sxs-lookup"><span data-stu-id="d2b87-122">On the **Advisor recommendations** dashboard, click **Get recommendations**.</span></span>

3. <span data-ttu-id="d2b87-123">Na lista de recomendações, clique em uma recomendação que você deseja examinar com detalhes.</span><span class="sxs-lookup"><span data-stu-id="d2b87-123">In the list of recommendations, click a recommendation that you want to review in detail.</span></span>  
<span data-ttu-id="d2b87-124">A folha **Recomendação** é exibida.</span><span class="sxs-lookup"><span data-stu-id="d2b87-124">The **Recommendation** blade is displayed.</span></span>

4. <span data-ttu-id="d2b87-125">Na folha **Recomendações**, examine as informações sobre as ações que você pode executar para resolver um possível problema ou aproveite uma oportunidade de economia de custo.</span><span class="sxs-lookup"><span data-stu-id="d2b87-125">On the **Recommendations** blade, review information about actions that you can perform to resolve a potential issue, or take advantage of a cost-saving opportunity.</span></span> 
  
  ![A folha Recomendação do Assistente](./media/advisor-overview/advisor-recommendation-action-example.png)

## <a name="search-for-advisor-recommendations"></a><span data-ttu-id="d2b87-127">Procurar recomendações do Advisor</span><span class="sxs-lookup"><span data-stu-id="d2b87-127">Search for Advisor recommendations</span></span>

<span data-ttu-id="d2b87-128">Procure recomendações sobre uma assinatura ou grupo de recursos específico.</span><span class="sxs-lookup"><span data-stu-id="d2b87-128">You can search for recommendations for a particular subscription or resource group.</span></span> <span data-ttu-id="d2b87-129">Você também pode procurar recomendações por status.</span><span class="sxs-lookup"><span data-stu-id="d2b87-129">You can also search for recommendations by status.</span></span>

1. <span data-ttu-id="d2b87-130">Entre no [portal do Azure](https://portal.azure.com) e inicie o [Assistente do Azure](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="d2b87-130">Sign in to the [Azure portal](https://portal.azure.com), and then start [Azure Advisor](https://aka.ms/azureadvisordashboard).</span></span>

2. <span data-ttu-id="d2b87-131">Procure recomendações filtrando por assinaturas, grupos de recursos e status da recomendação (**Ativa** ou **Adiada**).</span><span class="sxs-lookup"><span data-stu-id="d2b87-131">Search for recommendations by filtering for subscriptions, resource groups, and recommendation status (**Active** or **Snoozed**).</span></span>

3. <span data-ttu-id="d2b87-132">Para exibir uma lista de recomendações do Assistente com base nos critérios do filtro de pesquisa, clique em **Obter recomendações**.</span><span class="sxs-lookup"><span data-stu-id="d2b87-132">To display a list of Advisor recommendations that are based on your search-filter criteria, click **Get recommendations**.</span></span>

  ![Critérios do filtro de pesquisa do Assistente](./media/advisor-get-started/advisor-search.png)

## <a name="snooze-or-dismiss-advisor-recommendations"></a><span data-ttu-id="d2b87-134">Adiar ou descartar as recomendações do Assistente</span><span class="sxs-lookup"><span data-stu-id="d2b87-134">Snooze or dismiss Advisor recommendations</span></span>

1. <span data-ttu-id="d2b87-135">Entre no [portal do Azure](https://portal.azure.com) e inicie o [Assistente do Azure](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="d2b87-135">Sign in to the [Azure portal](https://portal.azure.com), and then start [Azure Advisor](https://aka.ms/azureadvisordashboard).</span></span>

2. <span data-ttu-id="d2b87-136">Clique em **Obter recomendações** e, na lista de recomendações, clique em uma recomendação.</span><span class="sxs-lookup"><span data-stu-id="d2b87-136">Click **Get recommendations**, and then, in the list of recommendations, click a recommendation.</span></span>

3. <span data-ttu-id="d2b87-137">Na folha **Recomendação**, clique em **Adiar**.</span><span class="sxs-lookup"><span data-stu-id="d2b87-137">On the **Recommendation** blade, click **Snooze**.</span></span>  

   ![Exemplo de ação de recomendação do Advisor](./media/advisor-get-started/advisor-snooze.png)

4. <span data-ttu-id="d2b87-139">Especifique uma hora de adiamento ou selecione **Nunca** para descartar a recomendação.</span><span class="sxs-lookup"><span data-stu-id="d2b87-139">Specify a snooze time period, or select **Never** to dismiss the recommendation.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d2b87-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d2b87-140">Next steps</span></span>

<span data-ttu-id="d2b87-141">Para saber mais sobre o Assistente, consulte:</span><span class="sxs-lookup"><span data-stu-id="d2b87-141">To learn more about Advisor, see:</span></span>
* [<span data-ttu-id="d2b87-142">Introdução ao Azure Advisor</span><span class="sxs-lookup"><span data-stu-id="d2b87-142">Introduction to Azure Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="d2b87-143">Recomendações de alta disponibilidade do Advisor</span><span class="sxs-lookup"><span data-stu-id="d2b87-143">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)
* [<span data-ttu-id="d2b87-144">Recomendações de segurança do Advisor</span><span class="sxs-lookup"><span data-stu-id="d2b87-144">Advisor Security recommendations</span></span>](advisor-security-recommendations.md)
-  [<span data-ttu-id="d2b87-145">Recomendações de desempenho do Advisor</span><span class="sxs-lookup"><span data-stu-id="d2b87-145">Advisor Performance recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="d2b87-146">Recomendações de custo do Advisor</span><span class="sxs-lookup"><span data-stu-id="d2b87-146">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)
