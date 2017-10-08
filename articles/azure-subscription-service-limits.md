---
title: assinatura aaaAzure limites e cotas | Microsoft Docs
description: "Fornece uma lista de assinaturas comuns do Azure e limites de serviço, cotas e restrições. Isso inclui informações sobre como tooincrease limita juntamente com os valores máximo."
services: 
documentationcenter: 
author: rothja
manager: jeffreyg
editor: 
tags: billing
ms.assetid: 60d848f9-ff26-496e-a5ec-ccf92ad7d125
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: byvinyal
ms.openlocfilehash: a754d56124520791254ab8f1729808f0750ff222
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-subscription-and-service-limits-quotas-and-constraints"></a><span data-ttu-id="64943-104">Assinatura do Azure e limite de serviços, cotas e restrições</span><span class="sxs-lookup"><span data-stu-id="64943-104">Azure subscription and service limits, quotas, and constraints</span></span>
<span data-ttu-id="64943-105">Este documento lista alguns dos limites Microsoft Azure mais comuns Olá que às vezes são chamados de cotas.</span><span class="sxs-lookup"><span data-stu-id="64943-105">This document lists some of hello most common Microsoft Azure limits, which are also sometimes called quotas.</span></span> <span data-ttu-id="64943-106">Esse documento não cobre atualmente todos os serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="64943-106">This document doesn't currently cover all Azure services.</span></span> <span data-ttu-id="64943-107">Ao longo do tempo, lista de saudação será expandida e atualizado toocover mais da plataforma de saudação.</span><span class="sxs-lookup"><span data-stu-id="64943-107">Over time, hello list will be expanded and updated toocover more of hello platform.</span></span>

<span data-ttu-id="64943-108">Visite [visão geral de preços do Azure](https://azure.microsoft.com/pricing/) toolearn mais informações sobre preços do Azure.</span><span class="sxs-lookup"><span data-stu-id="64943-108">Please visit [Azure Pricing Overview](https://azure.microsoft.com/pricing/) toolearn more about Azure pricing.</span></span> <span data-ttu-id="64943-109">Lá, você pode estimar os custos usando Olá [Calculadora de preços](https://azure.microsoft.com/pricing/calculator/) ou visitando Olá preços página de detalhes para um serviço (por exemplo, [VMs do Windows](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows)).</span><span class="sxs-lookup"><span data-stu-id="64943-109">There, you can estimate your costs using hello [Pricing Calculator](https://azure.microsoft.com/pricing/calculator/) or by visiting hello pricing details page for a service (for example, [Windows VMs](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows)).</span></span> <span data-ttu-id="64943-110">Para obter dicas toohelp gerenciar custos, consulte [impedir que inesperado custos com gerenciamento de custos e de cobrança do Azure](billing/billing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="64943-110">For tips toohelp manage your costs, see [Prevent unexpected costs with Azure billing and cost management](billing/billing-getting-started.md).</span></span>

> [!NOTE]
> <span data-ttu-id="64943-111">Se você quiser cota acima hello ou limite de saudação tooraise **limite padrão**, [abrir uma solicitação de suporte do cliente online sem custos](azure-supportability/resource-manager-core-quotas-request.md).</span><span class="sxs-lookup"><span data-stu-id="64943-111">If you want tooraise hello limit or quota above hello **Default Limit**, [open an online customer support request at no charge](azure-supportability/resource-manager-core-quotas-request.md).</span></span> <span data-ttu-id="64943-112">Hello limites não podem ser aumentados Olá **limite máximo** valor mostrado no hello tabelas a seguir.</span><span class="sxs-lookup"><span data-stu-id="64943-112">hello limits can't be raised above hello **Maximum Limit** value shown in hello following tables.</span></span> <span data-ttu-id="64943-113">Se não houver nenhum **limite máximo** coluna, em seguida, recursos de saudação não tem limites ajustáveis.</span><span class="sxs-lookup"><span data-stu-id="64943-113">If there is no **Maximum Limit** column, then hello resource doesn't have adjustable limits.</span></span> 
> 
> <span data-ttu-id="64943-114">As assinaturas de Avaliação Gratuita não estão qualificadas para os aumentos de cota ou limite.</span><span class="sxs-lookup"><span data-stu-id="64943-114">Free Trial subscriptions are not eligible for limit or quota increases.</span></span> <span data-ttu-id="64943-115">Se você tiver uma avaliação gratuita, você pode atualizar tooa [pré-pago](https://azure.microsoft.com/offers/ms-azr-0003p/) assinatura.</span><span class="sxs-lookup"><span data-stu-id="64943-115">If you have a Free Trial, you can upgrade tooa [Pay-As-You-Go](https://azure.microsoft.com/offers/ms-azr-0003p/) subscription.</span></span> <span data-ttu-id="64943-116">Para obter mais informações, consulte [atualizar avaliação gratuita do Azure tooPay-como-você-Go](billing/billing-upgrade-azure-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="64943-116">For more information, see [Upgrade Azure Free Trial tooPay-As-You-Go](billing/billing-upgrade-azure-subscription.md).</span></span>
> 

## <a name="limits-and-hello-azure-resource-manager"></a><span data-ttu-id="64943-117">Limites e hello Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="64943-117">Limits and hello Azure Resource Manager</span></span>
<span data-ttu-id="64943-118">Agora é possível toocombine vários recursos do Azure tooa único grupo de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="64943-118">It is now possible toocombine multiple Azure resources in tooa single Azure Resource Group.</span></span> <span data-ttu-id="64943-119">Ao usar grupos de recursos, limites que antes eram globais gerenciados em um nível regional com hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="64943-119">When using Resource Groups, limits that once were global become managed at a regional level with hello Azure Resource Manager.</span></span> <span data-ttu-id="64943-120">Para saber mais sobre os Grupos de Recursos do Azure, confira [Visão geral do Azure Resource Manager](azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="64943-120">For more information about Azure Resource Groups, see [Azure Resource Manager overview](azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="64943-121">Nos limites Olá abaixo, uma nova tabela foi adicionado tooreflect as diferenças nos limites ao usar o hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="64943-121">In hello limits below, a new table has been added tooreflect any differences in limits when using hello Azure Resource Manager.</span></span> <span data-ttu-id="64943-122">Por exemplo, há uma tabela de **Limites de Assinatura** e uma tabela de **Limites de Assinatura – Azure Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="64943-122">For example, there is a **Subscription Limits** table and a **Subscription Limits - Azure Resource Manager** table.</span></span> <span data-ttu-id="64943-123">Quando um limite se aplica a cenários de tooboth, é mostrada apenas na primeira tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="64943-123">When a limit applies tooboth scenarios, it is only shown in hello first table.</span></span> <span data-ttu-id="64943-124">A menos que indicado de outro modo, os limites são globais em todas as regiões.</span><span class="sxs-lookup"><span data-stu-id="64943-124">Unless otherwise indicated, limits are global across all regions.</span></span>

> [!NOTE]
> <span data-ttu-id="64943-125">É importante tooemphasize que cotas para recursos em grupos de recursos do Azure são por região acessível por sua assinatura e não por assinatura, como cotas de gerenciamento de serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="64943-125">It is important tooemphasize that quotas for resources in Azure Resource Groups are per-region accessible by your subscription, and are not per-subscription, as hello service management quotas are.</span></span> <span data-ttu-id="64943-126">Vamos usar cotas de núcleos como exemplo.</span><span class="sxs-lookup"><span data-stu-id="64943-126">Let's use core quotas as an example.</span></span> <span data-ttu-id="64943-127">Se você precisar toorequest aumentar a cota com suporte para núcleos, você precisa toodecide como muitos núcleos desejado toouse em quais regiões e, em seguida, fazer uma solicitação específica para o grupo de recursos do Azure principais cotas para valores hello e regiões em que você deseja.</span><span class="sxs-lookup"><span data-stu-id="64943-127">If you need toorequest a quota increase with support for cores, you need toodecide how many cores you want toouse in which regions, and then make a specific request for Azure Resource Group core quotas for hello amounts and regions that you want.</span></span> <span data-ttu-id="64943-128">Portanto, se você precisar toouse 30 núcleos na Europa Ocidental toorun seu aplicativo; Especificamente, você deve solicitar 30 núcleos na Europa Ocidental.</span><span class="sxs-lookup"><span data-stu-id="64943-128">Therefore, if you need toouse 30 cores in West Europe toorun your application there; you should specifically request 30 cores in West Europe.</span></span> <span data-ttu-id="64943-129">Mas você não terá uma cota de núcleos aumentam em qualquer outra região - somente Ocidental terá a cota de núcleo de 30 de saudação.</span><span class="sxs-lookup"><span data-stu-id="64943-129">But you will not have a core quota increase in any other region -- only West Europe will have hello 30-core quota.</span></span>
> <!-- -->
> <span data-ttu-id="64943-130">Como resultado, você pode achar útil tooconsider decidir o que suas cotas de grupo de recursos do Azure precisam toobe para sua carga de trabalho em qualquer uma região e solicitação que o valor em cada região na qual você estiver considerando a implantação.</span><span class="sxs-lookup"><span data-stu-id="64943-130">As a result, you may find it useful tooconsider deciding what your Azure Resource Group quotas need toobe for your workload in any one region, and request that amount in each region into which you are considering deployment.</span></span> <span data-ttu-id="64943-131">Consulte [Solucionando problemas de implantação](resource-manager-common-deployment-errors.md) para obter mais ajuda ao descobrir suas cotas atuais para regiões específicas.</span><span class="sxs-lookup"><span data-stu-id="64943-131">See [troubleshooting deployment issues](resource-manager-common-deployment-errors.md) for more help discovering your current quotas for specific regions.</span></span>
> 
> 

## <a name="service-specific-limits"></a><span data-ttu-id="64943-132">Limites específicos de serviço</span><span class="sxs-lookup"><span data-stu-id="64943-132">Service-specific limits</span></span>
* [<span data-ttu-id="64943-133">Active Directory</span><span class="sxs-lookup"><span data-stu-id="64943-133">Active Directory</span></span>](#active-directory-limits)
* [<span data-ttu-id="64943-134">Gerenciamento da API</span><span class="sxs-lookup"><span data-stu-id="64943-134">API Management</span></span>](#api-management-limits)
* [<span data-ttu-id="64943-135">Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="64943-135">App Service</span></span>](#app-service-limits)
* [<span data-ttu-id="64943-136">Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="64943-136">Application Gateway</span></span>](#application-gateway-limits)
* [<span data-ttu-id="64943-137">Application Insights</span><span class="sxs-lookup"><span data-stu-id="64943-137">Application Insights</span></span>](#application-insights-limits)
* [<span data-ttu-id="64943-138">Automação</span><span class="sxs-lookup"><span data-stu-id="64943-138">Automation</span></span>](#automation-limits)
* [<span data-ttu-id="64943-139">Banco de dados do Azure Cosmos</span><span class="sxs-lookup"><span data-stu-id="64943-139">Azure Cosmos DB</span></span>](#azure-cosmos-db-limits)
* [<span data-ttu-id="64943-140">Grade de Eventos do Azure</span><span class="sxs-lookup"><span data-stu-id="64943-140">Azure Event Grid</span></span>](#azure-event-grid-limits)
* [<span data-ttu-id="64943-141">Cache Redis do Azure</span><span class="sxs-lookup"><span data-stu-id="64943-141">Azure Redis Cache</span></span>](#azure-redis-cache-limits)
* [<span data-ttu-id="64943-142">RemoteApp do Azure</span><span class="sxs-lookup"><span data-stu-id="64943-142">Azure RemoteApp</span></span>](#azure-remoteapp-limits)
* [<span data-ttu-id="64943-143">Backup</span><span class="sxs-lookup"><span data-stu-id="64943-143">Backup</span></span>](#backup-limits)
* [<span data-ttu-id="64943-144">Batch</span><span class="sxs-lookup"><span data-stu-id="64943-144">Batch</span></span>](#batch-limits)
* [<span data-ttu-id="64943-145">Serviços do BizTalk</span><span class="sxs-lookup"><span data-stu-id="64943-145">BizTalk Services</span></span>](#biztalk-services-limits)
* [<span data-ttu-id="64943-146">CDN</span><span class="sxs-lookup"><span data-stu-id="64943-146">CDN</span></span>](#cdn-limits)
* [<span data-ttu-id="64943-147">Serviços de Nuvem</span><span class="sxs-lookup"><span data-stu-id="64943-147">Cloud Services</span></span>](#cloud-services-limits)
* [<span data-ttu-id="64943-148">Instâncias de Contêiner</span><span class="sxs-lookup"><span data-stu-id="64943-148">Container Instances</span></span>](#container-instances-limits)
* [<span data-ttu-id="64943-149">Fábrica de dados</span><span class="sxs-lookup"><span data-stu-id="64943-149">Data Factory</span></span>](#data-factory-limits)
* [<span data-ttu-id="64943-150">Análises Data Lake</span><span class="sxs-lookup"><span data-stu-id="64943-150">Data Lake Analytics</span></span>](#data-lake-analytics-limits)
* [<span data-ttu-id="64943-151">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="64943-151">Data Lake Store</span></span>](#data-lake-store-limits)
* [<span data-ttu-id="64943-152">DNS</span><span class="sxs-lookup"><span data-stu-id="64943-152">DNS</span></span>](#dns-limits)
* [<span data-ttu-id="64943-153">Hubs de Evento</span><span class="sxs-lookup"><span data-stu-id="64943-153">Event Hubs</span></span>](#event-hubs-limits)
* [<span data-ttu-id="64943-154">Hub IoT</span><span class="sxs-lookup"><span data-stu-id="64943-154">IoT Hub</span></span>](#iot-hub-limits)
* [<span data-ttu-id="64943-155">Cofre da Chave</span><span class="sxs-lookup"><span data-stu-id="64943-155">Key Vault</span></span>](#key-vault-limits)
* [<span data-ttu-id="64943-156">Log Analytics/Insights Operacionais</span><span class="sxs-lookup"><span data-stu-id="64943-156">Log Analytics / Operational Insights</span></span>](#log-analytics-limits)
* [<span data-ttu-id="64943-157">Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="64943-157">Media Services</span></span>](#media-services-limits)
* [<span data-ttu-id="64943-158">Engajamento Móvel</span><span class="sxs-lookup"><span data-stu-id="64943-158">Mobile Engagement</span></span>](#mobile-engagement-limits)
* [<span data-ttu-id="64943-159">Serviços Móveis</span><span class="sxs-lookup"><span data-stu-id="64943-159">Mobile Services</span></span>](#mobile-services-limits)
* [<span data-ttu-id="64943-160">Monitorar</span><span class="sxs-lookup"><span data-stu-id="64943-160">Monitor</span></span>](#monitor-limits)
* [<span data-ttu-id="64943-161">Autenticação Multifator</span><span class="sxs-lookup"><span data-stu-id="64943-161">Multi-Factor Authentication</span></span>](#multi-factor-authentication)
* [<span data-ttu-id="64943-162">Rede</span><span class="sxs-lookup"><span data-stu-id="64943-162">Networking</span></span>](#networking-limits)
* [<span data-ttu-id="64943-163">Observador de Rede</span><span class="sxs-lookup"><span data-stu-id="64943-163">Network Watcher</span></span>](#network-watcher-limits)
* [<span data-ttu-id="64943-164">Serviço de hub de notificação</span><span class="sxs-lookup"><span data-stu-id="64943-164">Notification Hub Service</span></span>](#notification-hub-service-limits)
* [<span data-ttu-id="64943-165">Grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="64943-165">Resource Group</span></span>](#resource-group-limits)
* [<span data-ttu-id="64943-166">Agendador</span><span class="sxs-lookup"><span data-stu-id="64943-166">Scheduler</span></span>](#scheduler-limits)
* [<span data-ttu-id="64943-167">Search</span><span class="sxs-lookup"><span data-stu-id="64943-167">Search</span></span>](#search-limits)
* [<span data-ttu-id="64943-168">Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="64943-168">Service Bus</span></span>](#service-bus-limits)
* [<span data-ttu-id="64943-169">Recuperação de Site</span><span class="sxs-lookup"><span data-stu-id="64943-169">Site Recovery</span></span>](#site-recovery-limits)
* [<span data-ttu-id="64943-170">Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="64943-170">SQL Database</span></span>](#sql-database-limits)
* [<span data-ttu-id="64943-171">Armazenamento</span><span class="sxs-lookup"><span data-stu-id="64943-171">Storage</span></span>](#storage-limits)
* [<span data-ttu-id="64943-172">Sistema StorSimple</span><span class="sxs-lookup"><span data-stu-id="64943-172">StorSimple System</span></span>](#storsimple-system-limits)
* [<span data-ttu-id="64943-173">Análise de fluxo</span><span class="sxs-lookup"><span data-stu-id="64943-173">Stream Analytics</span></span>](#stream-analytics-limits)
* [<span data-ttu-id="64943-174">Assinatura</span><span class="sxs-lookup"><span data-stu-id="64943-174">Subscription</span></span>](#subscription-limits)
* [<span data-ttu-id="64943-175">Gerenciador de Tráfego</span><span class="sxs-lookup"><span data-stu-id="64943-175">Traffic Manager</span></span>](#traffic-manager-limits)
* [<span data-ttu-id="64943-176">Máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="64943-176">Virtual Machines</span></span>](#virtual-machines-limits)
* [<span data-ttu-id="64943-177">Conjuntos de Escala de Máquina Virtual</span><span class="sxs-lookup"><span data-stu-id="64943-177">Virtual Machine Scale Sets</span></span>](#virtual-machine-scale-sets-limits)

### <a name="subscription-limits"></a><span data-ttu-id="64943-178">Limites de assinatura</span><span class="sxs-lookup"><span data-stu-id="64943-178">Subscription limits</span></span>
#### <a name="subscription-limits"></a><span data-ttu-id="64943-179">Limites de assinatura</span><span class="sxs-lookup"><span data-stu-id="64943-179">Subscription limits</span></span>
[!INCLUDE [azure-subscription-limits](../includes/azure-subscription-limits.md)]

#### <a name="subscription-limits---azure-resource-manager"></a><span data-ttu-id="64943-180">Limites de Assinatura – Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="64943-180">Subscription limits - Azure Resource Manager</span></span>
<span data-ttu-id="64943-181">Olá limites a seguir se aplicam ao usar o hello Azure Resource Manager e grupos de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="64943-181">hello following limits apply when using hello Azure Resource Manager and Azure Resource Groups.</span></span> <span data-ttu-id="64943-182">Limites que não foram alteradas com hello Azure Resource Manager não estão listados abaixo.</span><span class="sxs-lookup"><span data-stu-id="64943-182">Limits that have not changed with hello Azure Resource Manager are not listed below.</span></span> <span data-ttu-id="64943-183">Consulte a tabela anterior toohello para esses limites.</span><span class="sxs-lookup"><span data-stu-id="64943-183">Please refer toohello previous table for those limits.</span></span>

<span data-ttu-id="64943-184">Para obter informações sobre como lidar com limites de solicitações do Resource Manager, confira [Throttling Resource Manager requests](resource-manager-request-limits.md) (Limitando as solicitações do Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="64943-184">For information about handling limits on Resource Manager requests, see [Throttling Resource Manager requests](resource-manager-request-limits.md).</span></span>

[!INCLUDE [azure-subscription-limits-azure-resource-manager](../includes/azure-subscription-limits-azure-resource-manager.md)]

### <a name="resource-group-limits"></a><span data-ttu-id="64943-185">Limites do Grupo de Recursos</span><span class="sxs-lookup"><span data-stu-id="64943-185">Resource Group limits</span></span>
[!INCLUDE [azure-resource-groups-limits](../includes/azure-resource-groups-limits.md)]

### <a name="virtual-machines-limits"></a><span data-ttu-id="64943-186">Limites de Máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="64943-186">Virtual Machines limits</span></span>
#### <a name="virtual-machine-limits"></a><span data-ttu-id="64943-187">Limites de Máquina virtual</span><span class="sxs-lookup"><span data-stu-id="64943-187">Virtual Machine limits</span></span>
[!INCLUDE [azure-virtual-machines-limits](../includes/azure-virtual-machines-limits.md)]

#### <a name="virtual-machines-limits---azure-resource-manager"></a><span data-ttu-id="64943-188">Limites de Máquinas Virtuais – Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="64943-188">Virtual Machines limits - Azure Resource Manager</span></span>
<span data-ttu-id="64943-189">Olá limites a seguir se aplicam ao usar o hello Azure Resource Manager e grupos de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="64943-189">hello following limits apply when using hello Azure Resource Manager and Azure Resource Groups.</span></span> <span data-ttu-id="64943-190">Limites que não foram alteradas com hello Azure Resource Manager não estão listados abaixo.</span><span class="sxs-lookup"><span data-stu-id="64943-190">Limits that have not changed with hello Azure Resource Manager are not listed below.</span></span> <span data-ttu-id="64943-191">Consulte a tabela anterior toohello para esses limites.</span><span class="sxs-lookup"><span data-stu-id="64943-191">Please refer toohello previous table for those limits.</span></span>

[!INCLUDE [azure-virtual-machines-limits-azure-resource-manager](../includes/azure-virtual-machines-limits-azure-resource-manager.md)]

### <a name="virtual-machine-scale-sets-limits"></a><span data-ttu-id="64943-192">Limites de conjuntos de escala de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="64943-192">Virtual Machine Scale Sets limits</span></span>
[!INCLUDE [virtual-machine-scale-sets-limits](../includes/azure-virtual-machine-scale-sets-limits.md)]

### <a name="container-instances-limits"></a><span data-ttu-id="64943-193">Limites de Instâncias de Contêiner</span><span class="sxs-lookup"><span data-stu-id="64943-193">Container Instances Limits</span></span>
[!INCLUDE [container-instances-limits](../includes/container-instances-limits.md)]

### <a name="networking-limits"></a><span data-ttu-id="64943-194">Limites de rede</span><span class="sxs-lookup"><span data-stu-id="64943-194">Networking limits</span></span>
[!INCLUDE [expressroute-limits](../includes/expressroute-limits.md)]

#### <a name="networking-limits"></a><span data-ttu-id="64943-195">Limites de rede</span><span class="sxs-lookup"><span data-stu-id="64943-195">Networking limits</span></span>
[!INCLUDE [azure-virtual-network-limits](../includes/azure-virtual-network-limits.md)]

#### <a name="application-gateway-limits"></a><span data-ttu-id="64943-196">Limites do Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="64943-196">Application Gateway limits</span></span>
[!INCLUDE [application-gateway-limits](../includes/application-gateway-limits.md)]

#### <a name="network-watcher-limits"></a><span data-ttu-id="64943-197">Limites do Observador de Rede</span><span class="sxs-lookup"><span data-stu-id="64943-197">Network Watcher limits</span></span>
[!INCLUDE [network-watcher-limits](../includes/network-watcher-limits.md)]

#### <a name="traffic-manager-limits"></a><span data-ttu-id="64943-198">Limites do Gerenciador de Tráfego</span><span class="sxs-lookup"><span data-stu-id="64943-198">Traffic Manager limits</span></span>
[!INCLUDE [traffic-manager-limits](../includes/traffic-manager-limits.md)]

#### <a name="dns-limits"></a><span data-ttu-id="64943-199">Limites de DNS</span><span class="sxs-lookup"><span data-stu-id="64943-199">DNS limits</span></span>
[!INCLUDE [dns-limits](../includes/dns-limits.md)]

### <a name="storage-limits"></a><span data-ttu-id="64943-200">Limites de armazenamento</span><span class="sxs-lookup"><span data-stu-id="64943-200">Storage limits</span></span>
<span data-ttu-id="64943-201">Para obter mais detalhes sobre os limites da conta de armazenamento, veja [Metas de desempenho e escalabilidade do Armazenamento do Azure](storage/common/storage-scalability-targets.md).</span><span class="sxs-lookup"><span data-stu-id="64943-201">For additional details on storage account limits, see [Azure Storage Scalability and Performance Targets](storage/common/storage-scalability-targets.md).</span></span>
<!--like # storage accts --> 
#### <a name="storage-service-limits"></a><span data-ttu-id="64943-202">Limites de Serviço de Armazenamento</span><span class="sxs-lookup"><span data-stu-id="64943-202">Storage Service limits</span></span>
[!INCLUDE [azure-storage-limits](../includes/azure-storage-limits.md)]

<!-- conceptual info about disk limits -- applies toounmanaged and managed -->
#### <a name="virtual-machine-disk-limits"></a><span data-ttu-id="64943-203">Limites de disco de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="64943-203">Virtual machine disk limits</span></span> 
[!INCLUDE [azure-storage-limits-vm-disks](../includes/azure-storage-limits-vm-disks.md)]

<span data-ttu-id="64943-204">Consulte [Tamanhos de máquina virtual](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para saber mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="64943-204">See [Virtual machine sizes](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for additional details.</span></span>

#### <a name="managed-virtual-machine-disks"></a><span data-ttu-id="64943-205">Discos de máquina virtual gerenciados</span><span class="sxs-lookup"><span data-stu-id="64943-205">Managed virtual machine disks</span></span>

[!INCLUDE [azure-storage-limits-vm-disks-managed](../includes/azure-storage-limits-vm-disks-managed.md)]

#### <a name="unmanaged-virtual-machine-disks"></a><span data-ttu-id="64943-206">Discos de máquina virtual não gerenciados</span><span class="sxs-lookup"><span data-stu-id="64943-206">Unmanaged virtual machine disks</span></span>

[!INCLUDE [azure-storage-limits-vm-disks-standard](../includes/azure-storage-limits-vm-disks-standard.md)]

[!INCLUDE [azure-storage-limits-vm-disks-premium](../includes/azure-storage-limits-vm-disks-premium.md)]

#### <a name="storage-resource-provider-limits"></a><span data-ttu-id="64943-207">Limites de Provedor de Recursos de Armazenamento</span><span class="sxs-lookup"><span data-stu-id="64943-207">Storage Resource Provider limits</span></span>
[!INCLUDE [azure-storage-limits-azure-resource-manager](../includes/azure-storage-limits-azure-resource-manager.md)]

### <a name="cloud-services-limits"></a><span data-ttu-id="64943-208">Limites de Serviços de Nuvem</span><span class="sxs-lookup"><span data-stu-id="64943-208">Cloud Services limits</span></span>
[!INCLUDE [azure-cloud-services-limits](../includes/azure-cloud-services-limits.md)]

### <a name="app-service-limits"></a><span data-ttu-id="64943-209">Limites do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="64943-209">App Service limits</span></span>
<span data-ttu-id="64943-210">limites de serviço de aplicativo a seguir Olá incluem limites para aplicativos Web, aplicativos móveis, aplicativos de API e aplicativos lógicos.</span><span class="sxs-lookup"><span data-stu-id="64943-210">hello following App Service limits include limits for Web Apps, Mobile Apps, API Apps, and Logic Apps.</span></span>

[!INCLUDE [azure-websites-limits](../includes/azure-websites-limits.md)]

### <a name="scheduler-limits"></a><span data-ttu-id="64943-211">Limites do Agendador</span><span class="sxs-lookup"><span data-stu-id="64943-211">Scheduler limits</span></span>
[!INCLUDE [scheduler-limits-table](../includes/scheduler-limits-table.md)]

### <a name="batch-limits"></a><span data-ttu-id="64943-212">Limites de lote</span><span class="sxs-lookup"><span data-stu-id="64943-212">Batch limits</span></span>
[!INCLUDE [azure-batch-limits](../includes/azure-batch-limits.md)]

### <a name="biztalk-services-limits"></a><span data-ttu-id="64943-213">Limites dos Serviços BizTalk</span><span class="sxs-lookup"><span data-stu-id="64943-213">BizTalk Services limits</span></span>
<span data-ttu-id="64943-214">Olá tabela a seguir mostra os limites de saudação para serviços Biztalk do Azure.</span><span class="sxs-lookup"><span data-stu-id="64943-214">hello following table shows hello limits for Azure Biztalk Services.</span></span>

[!INCLUDE [biztalk-services-service-limits](../includes/biztalk-services-service-limits.md)]

### <a name="azure-cosmos-db-limits"></a><span data-ttu-id="64943-215">Limites do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="64943-215">Azure Cosmos DB limits</span></span>
<span data-ttu-id="64943-216">Banco de dados do Azure Cosmos é um banco de dados de escala global em qual taxa de transferência e o armazenamento pode ser dimensionado toohandle tudo o que seu aplicativo requer.</span><span class="sxs-lookup"><span data-stu-id="64943-216">Azure Cosmos DB is a global scale database in which throughput and storage can be scaled toohandle whatever your application requires.</span></span> <span data-ttu-id="64943-217">Se você tiver alguma dúvida sobre a escala hello Azure Cosmos DB fornece, envie um email tooaskcosmosdb@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="64943-217">If you have any questions about hello scale Azure Cosmos DB provides, please send email tooaskcosmosdb@microsoft.com.</span></span>

### <a name="mobile-engagement-limits"></a><span data-ttu-id="64943-218">Limites do Mobile Engagement </span><span class="sxs-lookup"><span data-stu-id="64943-218">Mobile Engagement limits</span></span>
[!INCLUDE [azure-mobile-engagement-limits](../includes/azure-mobile-engagement-limits.md)]

### <a name="search-limits"></a><span data-ttu-id="64943-219">Limites do Search</span><span class="sxs-lookup"><span data-stu-id="64943-219">Search limits</span></span>
<span data-ttu-id="64943-220">Camadas de preços determinam a capacidade de saudação e limites de seu serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="64943-220">Pricing tiers determine hello capacity and limits of your search service.</span></span> <span data-ttu-id="64943-221">Eles incluem:</span><span class="sxs-lookup"><span data-stu-id="64943-221">Tiers include:</span></span>

* <span data-ttu-id="64943-222">*Gratuito* serviço multilocatário, compartilhado com outros assinantes do Azure, destinado à avaliação e a pequenos projetos de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="64943-222">*Free* multi-tenant service, shared with other Azure subscribers, intended for evaluation and small development projects.</span></span>
* <span data-ttu-id="64943-223">*Básico* fornece recursos de computação dedicados para cargas de trabalho de produção em uma escala menor, com o backup de réplicas toothree para cargas de trabalho de consulta altamente disponível.</span><span class="sxs-lookup"><span data-stu-id="64943-223">*Basic* provides dedicated computing resources for production workloads at a smaller scale, with up toothree replicas for highly available query workloads.</span></span>
* <span data-ttu-id="64943-224">*Standard (S1, S2, S3, S3 de alta densidade)* para cargas de trabalho de produção maiores.</span><span class="sxs-lookup"><span data-stu-id="64943-224">*Standard (S1, S2, S3, S3 High Density)* is for larger production workloads.</span></span> <span data-ttu-id="64943-225">Vários níveis existem na camada padrão Olá para que você possa escolher uma configuração de recurso que melhor descreva seu perfil de carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="64943-225">Multiple levels exist within hello standard tier so that you can choose a resource configuration that best matches your workload profile.</span></span>

<span data-ttu-id="64943-226">**Limites por assinatura**</span><span class="sxs-lookup"><span data-stu-id="64943-226">**Limits per subscription**</span></span>

[!INCLUDE [azure-search-limits-per-subscription](../includes/azure-search-limits-per-subscription.md)]

<span data-ttu-id="64943-227">**Limites por serviço Search**</span><span class="sxs-lookup"><span data-stu-id="64943-227">**Limits per search service**</span></span>

[!INCLUDE [azure-search-limits-per-service](../includes/azure-search-limits-per-service.md)]

<span data-ttu-id="64943-228">toolearn mais sobre limites em um nível mais granular, como tamanho do documento, consultas por segundo, chaves, solicitações e respostas, consulte [limites na pesquisa do Azure do serviço](search/search-limits-quotas-capacity.md).</span><span class="sxs-lookup"><span data-stu-id="64943-228">toolearn more about limits on a more granular level, such as document size, queries per second, keys, requests, and responses, see [Service limits in Azure Search](search/search-limits-quotas-capacity.md).</span></span>

### <a name="media-services-limits"></a><span data-ttu-id="64943-229">Limites de Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="64943-229">Media Services limits</span></span>
[!INCLUDE [azure-mediaservices-limits](../includes/azure-mediaservices-limits.md)]

### <a name="cdn-limits"></a><span data-ttu-id="64943-230">Limites de CDN</span><span class="sxs-lookup"><span data-stu-id="64943-230">CDN limits</span></span>
[!INCLUDE [cdn-limits](../includes/cdn-limits.md)]

### <a name="mobile-services-limits"></a><span data-ttu-id="64943-231">Limites de Serviços Móveis</span><span class="sxs-lookup"><span data-stu-id="64943-231">Mobile Services limits</span></span>
[!INCLUDE [mobile-services-limits](../includes/mobile-services-limits.md)]

### <a name="monitor-limits"></a><span data-ttu-id="64943-232">Monitorar limites</span><span class="sxs-lookup"><span data-stu-id="64943-232">Monitor limits</span></span>
[!INCLUDE [monitoring-limits](../includes/monitoring-limits.md)]

### <a name="notification-hub-service-limits"></a><span data-ttu-id="64943-233">Limites de serviço de hub de notificação</span><span class="sxs-lookup"><span data-stu-id="64943-233">Notification Hub Service limits</span></span>
[!INCLUDE [notification-hub-limits](../includes/notification-hub-limits.md)]

### <a name="event-hubs-limits"></a><span data-ttu-id="64943-234">Limites de Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="64943-234">Event Hubs limits</span></span>
[!INCLUDE [azure-servicebus-limits](../includes/event-hubs-limits.md)]

### <a name="service-bus-limits"></a><span data-ttu-id="64943-235">Limites de Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="64943-235">Service Bus limits</span></span>
[!INCLUDE [azure-servicebus-limits](../includes/service-bus-quotas-table.md)]

### <a name="iot-hub-limits"></a><span data-ttu-id="64943-236">Limites do Hub IoT</span><span class="sxs-lookup"><span data-stu-id="64943-236">IoT Hub limits</span></span>
[!INCLUDE [azure-iothub-limits](../includes/iot-hub-limits.md)]

### <a name="data-factory-limits"></a><span data-ttu-id="64943-237">Limites de fábrica de dados</span><span class="sxs-lookup"><span data-stu-id="64943-237">Data Factory limits</span></span>
[!INCLUDE [azure-data-factory-limits](../includes/azure-data-factory-limits.md)]

### <a name="data-lake-analytics-limits"></a><span data-ttu-id="64943-238">Limites do Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="64943-238">Data Lake Analytics limits</span></span>
[!INCLUDE [azure-data-lake-analytics-limits](../includes/azure-data-lake-analytics-limits.md)]

### <a name="data-lake-store-limits"></a><span data-ttu-id="64943-239">Limites do Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="64943-239">Data Lake Store limits</span></span>
[!INCLUDE [azure-data-lake-store-limits](../includes/azure-data-lake-store-limits.md)]

### <a name="stream-analytics-limits"></a><span data-ttu-id="64943-240">Limites do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="64943-240">Stream Analytics limits</span></span>
[!INCLUDE [stream-analytics-limits-table](../includes/stream-analytics-limits-table.md)]

### <a name="active-directory-limits"></a><span data-ttu-id="64943-241">Limites do Active Directory</span><span class="sxs-lookup"><span data-stu-id="64943-241">Active Directory limits</span></span>
[!INCLUDE [AAD-service-limits](../includes/active-directory-service-limits-include.md)]

### <a name="azure-event-grid-limits"></a><span data-ttu-id="64943-242">Limites de Grade de Eventos do Azure</span><span class="sxs-lookup"><span data-stu-id="64943-242">Azure Event Grid limits</span></span>
[!INCLUDE [event-grid-limits](../includes/event-grid-limits.md)]

### <a name="azure-remoteapp-limits"></a><span data-ttu-id="64943-243">Limites do Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="64943-243">Azure RemoteApp limits</span></span>
[!INCLUDE [azure-remoteapp-limits](../includes/azure-remoteapp-limits.md)]

### <a name="storsimple-system-limits"></a><span data-ttu-id="64943-244">Limites do sistema StorSimple</span><span class="sxs-lookup"><span data-stu-id="64943-244">StorSimple System limits</span></span>
[!INCLUDE [storsimple-limits-table](../includes/storsimple-limits-table.md)]

### <a name="log-analytics-limits"></a><span data-ttu-id="64943-245">Limites do Log Analytics</span><span class="sxs-lookup"><span data-stu-id="64943-245">Log Analytics limits</span></span>
[!INCLUDE [operational-insights-limits](../includes/operational-insights-limits.md)]

### <a name="backup-limits"></a><span data-ttu-id="64943-246">Limites do Backup</span><span class="sxs-lookup"><span data-stu-id="64943-246">Backup limits</span></span>
[!INCLUDE [azure-backup-limits](../includes/azure-backup-limits.md)]

### <a name="site-recovery-limits"></a><span data-ttu-id="64943-247">Limites da Recuperação de Site</span><span class="sxs-lookup"><span data-stu-id="64943-247">Site Recovery limits</span></span>
[!INCLUDE [site-recovery-limits](../includes/site-recovery-limits.md)]

### <a name="application-insights-limits"></a><span data-ttu-id="64943-248">Limites do Application Insights</span><span class="sxs-lookup"><span data-stu-id="64943-248">Application Insights limits</span></span>
[!INCLUDE [application-insights-limits](../includes/application-insights-limits.md)]

### <a name="api-management-limits"></a><span data-ttu-id="64943-249">Limites de Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="64943-249">API Management limits</span></span>
[!INCLUDE [api-management-service-limits](../includes/api-management-service-limits.md)]

### <a name="azure-redis-cache-limits"></a><span data-ttu-id="64943-250">Limites do Cache Redis do Azure</span><span class="sxs-lookup"><span data-stu-id="64943-250">Azure Redis Cache limits</span></span>
[!INCLUDE [redis-cache-service-limits](../includes/redis-cache-service-limits.md)]

### <a name="key-vault-limits"></a><span data-ttu-id="64943-251">Limites do Cofre da Chave</span><span class="sxs-lookup"><span data-stu-id="64943-251">Key Vault limits</span></span>
[!INCLUDE [key-vault-limits](../includes/key-vault-limits.md)]

### <a name="multi-factor-authentication"></a><span data-ttu-id="64943-252">Autenticação Multifator</span><span class="sxs-lookup"><span data-stu-id="64943-252">Multi-Factor Authentication</span></span>
[!INCLUDE [azure-mfa-service-limits](../includes/azure-mfa-service-limits.md)]

### <a name="automation-limits"></a><span data-ttu-id="64943-253">Limites de automação</span><span class="sxs-lookup"><span data-stu-id="64943-253">Automation limits</span></span>
[!INCLUDE [automation-limits](../includes/azure-automation-service-limits.md)]

### <a name="sql-database-limits"></a><span data-ttu-id="64943-254">Limites de banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="64943-254">SQL Database limits</span></span>
<span data-ttu-id="64943-255">Para obter os limites do Banco de Dados SQL, veja [Limites de recurso de Banco de Dados SQL](sql-database/sql-database-resource-limits.md).</span><span class="sxs-lookup"><span data-stu-id="64943-255">For SQL Database limits, see [SQL Database Resource Limits](sql-database/sql-database-resource-limits.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="64943-256">Confira também</span><span class="sxs-lookup"><span data-stu-id="64943-256">See also</span></span>
[<span data-ttu-id="64943-257">Entendendo os limites e aumentos do Azure</span><span class="sxs-lookup"><span data-stu-id="64943-257">Understanding Azure Limits and Increases</span></span>](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/)

[<span data-ttu-id="64943-258">Tamanhos de máquinas virtuais e serviços de nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="64943-258">Virtual Machine and Cloud Service Sizes for Azure</span></span>](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="64943-259">Tamanhos dos serviços de nuvem</span><span class="sxs-lookup"><span data-stu-id="64943-259">Sizes for Cloud Services</span></span>](cloud-services/cloud-services-sizes-specs.md)

