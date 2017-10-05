---
title: Monitorar a integridade dos recursos da CDN do Azure | Microsoft Docs
description: Saiba como monitorar a Azure CDN Resource Health usando o Azure Resource Health.
services: cdn
documentationcenter: .net
author: zhangmanling
manager: zhangmanling
editor: 
ms.assetid: bf23bd89-35b2-4aca-ac7f-68ee02953f31
ms.service: cdn
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 37fe208f5087f318e665e76825127854b4a11c98
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-the-health-of-azure-cdn-resources"></a><span data-ttu-id="cfdd5-103">Monitorar a integridade dos recursos da CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="cfdd5-103">Monitor the health of Azure CDN resources</span></span>
  
<span data-ttu-id="cfdd5-104">A Azure CDN Resource Health é um subconjunto de [Azure Resource Health](../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cfdd5-104">Azure CDN Resource health is a subset of [Azure resource health](../resource-health/resource-health-overview.md).</span></span>  <span data-ttu-id="cfdd5-105">Você pode usar a Azure  Resource Health para monitorar a integridade dos recursos CDN e receber as diretrizes de ações para solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="cfdd5-105">You can use Azure resource health to monitor the health of CDN resources and receive actionable guidance to troubleshoot problems.</span></span>

>[!IMPORTANT] 
><span data-ttu-id="cfdd5-106">A integridade de recursos do Azure CDN considera no momento somente a integridade da distribuição de CDN global e recursos de API.</span><span class="sxs-lookup"><span data-stu-id="cfdd5-106">Azure CDN resource health only currently accounts for the health of global CDN delivery and API capabilities.</span></span>  <span data-ttu-id="cfdd5-107">A integridade de recursos do Azure CDN não verifica a pontos de extremidade de CDN individuais.</span><span class="sxs-lookup"><span data-stu-id="cfdd5-107">Azure CDN resource health does not verify individual CDN endpoints.</span></span>
>
><span data-ttu-id="cfdd5-108">Os sinais que alimentam a Azure CDN Resource Health podem ter atraso de até 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="cfdd5-108">The signals that feed Azure CDN resource health may be up to 15 minutes delayed.</span></span>

## <a name="how-to-find-azure-cdn-resource-health"></a><span data-ttu-id="cfdd5-109">Como localizar a Azure CDN Resource Health</span><span class="sxs-lookup"><span data-stu-id="cfdd5-109">How to find Azure CDN resource health</span></span>

1. <span data-ttu-id="cfdd5-110">No [Portal do Azure](https://portal.azure.com), navegue para seu perfil CDN.</span><span class="sxs-lookup"><span data-stu-id="cfdd5-110">In the [Azure portal](https://portal.azure.com), browse to your CDN profile.</span></span>

2. <span data-ttu-id="cfdd5-111">Clique no botão **Configurações** .</span><span class="sxs-lookup"><span data-stu-id="cfdd5-111">Click the **Settings** button.</span></span>

    ![Botão Configurações](./media/cdn-resource-health/cdn-profile-settings.png)

3. <span data-ttu-id="cfdd5-113">Em *Suporte + solução de problemas*, clique em **Integridade de recursos**.</span><span class="sxs-lookup"><span data-stu-id="cfdd5-113">Under *Support + troubleshooting*, click **Resource health**.</span></span>

    ![Integridade de recursos de CDN](./media/cdn-resource-health/cdn-resource-health3.png)

>[!TIP] 
><span data-ttu-id="cfdd5-115">Você também pode encontrar recursos de CDN listados no bloco *Integridade de recursos* na folha *Ajuda + suporte*.</span><span class="sxs-lookup"><span data-stu-id="cfdd5-115">You can also find CDN resources listed in the *Resource health* tile in the *Help + support* blade.</span></span>  <span data-ttu-id="cfdd5-116">Você pode ir rapidamente até *Ajuda + suporte* clicando no **?** circulado</span><span class="sxs-lookup"><span data-stu-id="cfdd5-116">You can quickly get to *Help + support* by clicking the circled **?**</span></span> <span data-ttu-id="cfdd5-117">no canto superior direito do portal.</span><span class="sxs-lookup"><span data-stu-id="cfdd5-117">in the upper right corner of the portal.</span></span>
>
> ![Ajuda + suporte](./media/cdn-resource-health/cdn-help-support.png)

## <a name="azure-cdn-specific-messages"></a><span data-ttu-id="cfdd5-119">Mensagens específicas do Azure CDN</span><span class="sxs-lookup"><span data-stu-id="cfdd5-119">Azure CDN-specific messages</span></span>

<span data-ttu-id="cfdd5-120">Os estados de integridade de recursos do Azure CDN podem ser encontrados abaixo.</span><span class="sxs-lookup"><span data-stu-id="cfdd5-120">Statuses related to Azure CDN resource health can be found below.</span></span>

|<span data-ttu-id="cfdd5-121">Mensagem</span><span class="sxs-lookup"><span data-stu-id="cfdd5-121">Message</span></span> | <span data-ttu-id="cfdd5-122">Ação recomendada</span><span class="sxs-lookup"><span data-stu-id="cfdd5-122">Recommended Action</span></span> |
|---|---|
|<span data-ttu-id="cfdd5-123">Você pode ter parado, removido ou configurado de forma errada um ou mais dos seus pontos de extremidade de CDN</span><span class="sxs-lookup"><span data-stu-id="cfdd5-123">You may have stopped, removed, or misconfigured one or more of your CDN endpoints</span></span> | <span data-ttu-id="cfdd5-124">Você pode ter parado, removido ou configurado de forma errada um ou mais dos seus pontos de extremidade de CDN.</span><span class="sxs-lookup"><span data-stu-id="cfdd5-124">You may have stopped, removed, or misconfigured one or more of your CDN endpoints.</span></span>|
|<span data-ttu-id="cfdd5-125">Infelizmente, o serviço de gerenciamento de CDN está indisponível no momento</span><span class="sxs-lookup"><span data-stu-id="cfdd5-125">We are sorry, the CDN management service is currently unavailable</span></span> | <span data-ttu-id="cfdd5-126">Regresse aqui para ver atualizações de estado; se o problema persistir após o tempo de resolução esperado, contate o suporte.</span><span class="sxs-lookup"><span data-stu-id="cfdd5-126">Check back here for status updates; If your problem persists after the expected resolution time, contact support.</span></span>|
|<span data-ttu-id="cfdd5-127">Infelizmente, os pontos de extremidade de CDN podem ser afetados por problemas existentes com alguns dos nossos provedores de CDN</span><span class="sxs-lookup"><span data-stu-id="cfdd5-127">We're sorry, your CDN endpoints may be impacted by ongoing issues with some of our CDN providers</span></span> | <span data-ttu-id="cfdd5-128">Regresse aqui para ver atualizações de estado; use a ferramenta de solução de problemas para saber como testar a origem e o ponto de extremidade de CDN. Se o problema persistir após o tempo de resolução esperado, contate o suporte.</span><span class="sxs-lookup"><span data-stu-id="cfdd5-128">Check back here for status updates; Use the Troubleshoot tool to learn how to test your origin and CDN endpoint; If your problem persists after the expected resolution time, contact support.</span></span> |
|<span data-ttu-id="cfdd5-129">Infelizmente, as alterações de configuração de ponto de extremidade de CDN estão sofrendo atrasos de propagação</span><span class="sxs-lookup"><span data-stu-id="cfdd5-129">We're sorry, CDN endpoint configuration changes are experiencing propagation delays</span></span> | <span data-ttu-id="cfdd5-130">Regresse aqui para ver atualizações de estado; se as alterações de configuração não forem totalmente propagadas no tempo esperado, contate o suporte.</span><span class="sxs-lookup"><span data-stu-id="cfdd5-130">Check back here for status updates; If your configuration changes are not fully propagated in the expected time, contact support.</span></span>|
|<span data-ttu-id="cfdd5-131">Infelizmente, estamos tendo problemas ao carregar o portal suplementar</span><span class="sxs-lookup"><span data-stu-id="cfdd5-131">We're sorry, we are experiencing issues loading the supplemental portal</span></span> | <span data-ttu-id="cfdd5-132">Regresse aqui para ver atualizações de estado; se o problema persistir após o tempo de resolução esperado, contate o suporte.</span><span class="sxs-lookup"><span data-stu-id="cfdd5-132">Check back here for status updates; If your problem persists after the expected resolution time, contact support.</span></span>|
<span data-ttu-id="cfdd5-133">Infelizmente, estamos tendo problemas com alguns dos nossos provedores de CDN</span><span class="sxs-lookup"><span data-stu-id="cfdd5-133">We are sorry, we are experiencing issues with some of our CDN providers</span></span> | <span data-ttu-id="cfdd5-134">Regresse aqui para ver atualizações de estado; se o problema persistir após o tempo de resolução esperado, contate o suporte.</span><span class="sxs-lookup"><span data-stu-id="cfdd5-134">Check back here for status updates; If your problem persists after the expected resolution time, contact support.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="cfdd5-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cfdd5-135">Next steps</span></span>

- [<span data-ttu-id="cfdd5-136">Acesse a visão geral do Azure Resource Health</span><span class="sxs-lookup"><span data-stu-id="cfdd5-136">Read an overview of Azure resource health</span></span>](../resource-health/resource-health-overview.md)
- [<span data-ttu-id="cfdd5-137">Solucione problemas com a compactação de arquivo de CDN</span><span class="sxs-lookup"><span data-stu-id="cfdd5-137">Troubleshoot issues with CDN compression</span></span>](./cdn-troubleshoot-compression.md)
- [<span data-ttu-id="cfdd5-138">Solucione problemas com erros 404</span><span class="sxs-lookup"><span data-stu-id="cfdd5-138">Troubleshoot issues with 404 errors</span></span>](./cdn-troubleshoot-endpoint.md)