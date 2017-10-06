---
title: "integridade de saudação aaaMonitor de recursos do Azure CDN | Microsoft Docs"
description: "Saiba como toomonitor Olá a integridade de seus recursos de CDN do Azure usando a integridade de recursos do Azure."
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
ms.openlocfilehash: 0a77e56d2fecae4bde6c83730c05375853a6638a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-hello-health-of-azure-cdn-resources"></a><span data-ttu-id="27dc0-103">Monitorar a integridade de recursos do Azure CDN Olá</span><span class="sxs-lookup"><span data-stu-id="27dc0-103">Monitor hello health of Azure CDN resources</span></span>
  
<span data-ttu-id="27dc0-104">A Azure CDN Resource Health é um subconjunto de [Azure Resource Health](../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="27dc0-104">Azure CDN Resource health is a subset of [Azure resource health](../resource-health/resource-health-overview.md).</span></span>  <span data-ttu-id="27dc0-105">Você pode usar a integridade do recurso do Azure integridade toomonitor Olá dos recursos CDN e receber problemas de tootroubleshoot orientação acionáveis.</span><span class="sxs-lookup"><span data-stu-id="27dc0-105">You can use Azure resource health toomonitor hello health of CDN resources and receive actionable guidance tootroubleshoot problems.</span></span>

>[!IMPORTANT] 
><span data-ttu-id="27dc0-106">Integridade de recursos do Azure CDN contas somente no momento para integridade de saudação de entrega do CDN global e recursos da API.</span><span class="sxs-lookup"><span data-stu-id="27dc0-106">Azure CDN resource health only currently accounts for hello health of global CDN delivery and API capabilities.</span></span>  <span data-ttu-id="27dc0-107">A integridade de recursos do Azure CDN não verifica a pontos de extremidade de CDN individuais.</span><span class="sxs-lookup"><span data-stu-id="27dc0-107">Azure CDN resource health does not verify individual CDN endpoints.</span></span>
>
><span data-ttu-id="27dc0-108">sinais de saudação de feed de integridade de recursos do Azure CDN podem ser up too15 minutos atrasados.</span><span class="sxs-lookup"><span data-stu-id="27dc0-108">hello signals that feed Azure CDN resource health may be up too15 minutes delayed.</span></span>

## <a name="how-toofind-azure-cdn-resource-health"></a><span data-ttu-id="27dc0-109">Como toofind integridade de recursos do Azure CDN</span><span class="sxs-lookup"><span data-stu-id="27dc0-109">How toofind Azure CDN resource health</span></span>

1. <span data-ttu-id="27dc0-110">Em Olá [portal do Azure](https://portal.azure.com), procurar tooyour perfil CDN.</span><span class="sxs-lookup"><span data-stu-id="27dc0-110">In hello [Azure portal](https://portal.azure.com), browse tooyour CDN profile.</span></span>

2. <span data-ttu-id="27dc0-111">Clique em Olá **configurações** botão.</span><span class="sxs-lookup"><span data-stu-id="27dc0-111">Click hello **Settings** button.</span></span>

    ![Botão Configurações](./media/cdn-resource-health/cdn-profile-settings.png)

3. <span data-ttu-id="27dc0-113">Em *Suporte + solução de problemas*, clique em **Integridade de recursos**.</span><span class="sxs-lookup"><span data-stu-id="27dc0-113">Under *Support + troubleshooting*, click **Resource health**.</span></span>

    ![Integridade de recursos de CDN](./media/cdn-resource-health/cdn-resource-health3.png)

>[!TIP] 
><span data-ttu-id="27dc0-115">Você também pode encontrar recursos CDN listados em Olá *integridade de recursos* lado a lado no hello *ajuda + suporte* folha.</span><span class="sxs-lookup"><span data-stu-id="27dc0-115">You can also find CDN resources listed in hello *Resource health* tile in hello *Help + support* blade.</span></span>  <span data-ttu-id="27dc0-116">Você pode obter rapidamente muito*ajuda + suporte* clicando hello dentro de um círculo **?**</span><span class="sxs-lookup"><span data-stu-id="27dc0-116">You can quickly get too*Help + support* by clicking hello circled **?**</span></span> <span data-ttu-id="27dc0-117">no hello canto superior direito do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="27dc0-117">in hello upper right corner of hello portal.</span></span>
>
> ![Ajuda + suporte](./media/cdn-resource-health/cdn-help-support.png)

## <a name="azure-cdn-specific-messages"></a><span data-ttu-id="27dc0-119">Mensagens específicas do Azure CDN</span><span class="sxs-lookup"><span data-stu-id="27dc0-119">Azure CDN-specific messages</span></span>

<span data-ttu-id="27dc0-120">Integridade de recursos CDN status tooAzure relacionados pode ser encontrada abaixo.</span><span class="sxs-lookup"><span data-stu-id="27dc0-120">Statuses related tooAzure CDN resource health can be found below.</span></span>

|<span data-ttu-id="27dc0-121">Mensagem</span><span class="sxs-lookup"><span data-stu-id="27dc0-121">Message</span></span> | <span data-ttu-id="27dc0-122">Ação recomendada</span><span class="sxs-lookup"><span data-stu-id="27dc0-122">Recommended Action</span></span> |
|---|---|
|<span data-ttu-id="27dc0-123">Você pode ter parado, removido ou configurado de forma errada um ou mais dos seus pontos de extremidade de CDN</span><span class="sxs-lookup"><span data-stu-id="27dc0-123">You may have stopped, removed, or misconfigured one or more of your CDN endpoints</span></span> | <span data-ttu-id="27dc0-124">Você pode ter parado, removido ou configurado de forma errada um ou mais dos seus pontos de extremidade de CDN.</span><span class="sxs-lookup"><span data-stu-id="27dc0-124">You may have stopped, removed, or misconfigured one or more of your CDN endpoints.</span></span>|
|<span data-ttu-id="27dc0-125">Infelizmente, Olá serviço de gerenciamento de CDN está disponível no momento</span><span class="sxs-lookup"><span data-stu-id="27dc0-125">We are sorry, hello CDN management service is currently unavailable</span></span> | <span data-ttu-id="27dc0-126">Marque aqui para atualizações de status; Se o problema persistir após Olá esperado tempo de resolução, contate o suporte.</span><span class="sxs-lookup"><span data-stu-id="27dc0-126">Check back here for status updates; If your problem persists after hello expected resolution time, contact support.</span></span>|
|<span data-ttu-id="27dc0-127">Infelizmente, os pontos de extremidade de CDN podem ser afetados por problemas existentes com alguns dos nossos provedores de CDN</span><span class="sxs-lookup"><span data-stu-id="27dc0-127">We're sorry, your CDN endpoints may be impacted by ongoing issues with some of our CDN providers</span></span> | <span data-ttu-id="27dc0-128">Marque aqui para atualizações de status; Usar toolearn de ferramenta de solução de problemas de saudação como tootest sua origem e o ponto de extremidade CDN; Se o problema persistir após Olá esperado tempo de resolução, contate o suporte.</span><span class="sxs-lookup"><span data-stu-id="27dc0-128">Check back here for status updates; Use hello Troubleshoot tool toolearn how tootest your origin and CDN endpoint; If your problem persists after hello expected resolution time, contact support.</span></span> |
|<span data-ttu-id="27dc0-129">Infelizmente, as alterações de configuração de ponto de extremidade de CDN estão sofrendo atrasos de propagação</span><span class="sxs-lookup"><span data-stu-id="27dc0-129">We're sorry, CDN endpoint configuration changes are experiencing propagation delays</span></span> | <span data-ttu-id="27dc0-130">Marque aqui para atualizações de status; Se as alterações de configuração não são totalmente propagadas em tempo de saudação esperado, contate o suporte.</span><span class="sxs-lookup"><span data-stu-id="27dc0-130">Check back here for status updates; If your configuration changes are not fully propagated in hello expected time, contact support.</span></span>|
|<span data-ttu-id="27dc0-131">Infelizmente, que estamos enfrentando problemas ao carregar o portal suplementar Olá</span><span class="sxs-lookup"><span data-stu-id="27dc0-131">We're sorry, we are experiencing issues loading hello supplemental portal</span></span> | <span data-ttu-id="27dc0-132">Marque aqui para atualizações de status; Se o problema persistir após Olá esperado tempo de resolução, contate o suporte.</span><span class="sxs-lookup"><span data-stu-id="27dc0-132">Check back here for status updates; If your problem persists after hello expected resolution time, contact support.</span></span>|
<span data-ttu-id="27dc0-133">Infelizmente, estamos tendo problemas com alguns dos nossos provedores de CDN</span><span class="sxs-lookup"><span data-stu-id="27dc0-133">We are sorry, we are experiencing issues with some of our CDN providers</span></span> | <span data-ttu-id="27dc0-134">Marque aqui para atualizações de status; Se o problema persistir após Olá esperado tempo de resolução, contate o suporte.</span><span class="sxs-lookup"><span data-stu-id="27dc0-134">Check back here for status updates; If your problem persists after hello expected resolution time, contact support.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="27dc0-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="27dc0-135">Next steps</span></span>

- [<span data-ttu-id="27dc0-136">Acesse a visão geral do Azure Resource Health</span><span class="sxs-lookup"><span data-stu-id="27dc0-136">Read an overview of Azure resource health</span></span>](../resource-health/resource-health-overview.md)
- [<span data-ttu-id="27dc0-137">Solucione problemas com a compactação de arquivo de CDN</span><span class="sxs-lookup"><span data-stu-id="27dc0-137">Troubleshoot issues with CDN compression</span></span>](./cdn-troubleshoot-compression.md)
- [<span data-ttu-id="27dc0-138">Solucione problemas com erros 404</span><span class="sxs-lookup"><span data-stu-id="27dc0-138">Troubleshoot issues with 404 errors</span></span>](./cdn-troubleshoot-endpoint.md)