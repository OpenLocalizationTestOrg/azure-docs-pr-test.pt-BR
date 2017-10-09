---
title: aaaWorkflows para configurar um circuito de rota expressa | Microsoft Docs
description: "Esta página orientará fluxos de trabalho Olá para configurar emparelhamentos e o circuito de rota expressa"
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: 55e0418c-e0bf-44a7-9aa1-720076df9297
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: cherylmc
ms.openlocfilehash: 8e1dfc137401e0d6d53608ae6c8de0085e182eba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-workflows-for-circuit-provisioning-and-circuit-states"></a><span data-ttu-id="e81dc-103">Fluxos de trabalho do ExpressRoute para provisionamento e estados do circuito</span><span class="sxs-lookup"><span data-stu-id="e81dc-103">ExpressRoute workflows for circuit provisioning and circuit states</span></span>
<span data-ttu-id="e81dc-104">Esta página orienta você durante o provisionamento do serviço hello e roteamento fluxos de trabalho de configuração em um alto nível.</span><span class="sxs-lookup"><span data-stu-id="e81dc-104">This page walks you through hello service provisioning and routing configuration workflows at a high level.</span></span>

![](./media/expressroute-workflows/expressroute-circuit-workflow.png)

<span data-ttu-id="e81dc-105">Olá figura a seguir e as etapas correspondentes mostram tarefas Olá que siga na ordem toohave uma rota expressa circuito provisionado ponta a ponta.</span><span class="sxs-lookup"><span data-stu-id="e81dc-105">hello following figure and corresponding steps show hello tasks you must follow in order toohave an ExpressRoute circuit provisioned end-to-end.</span></span> 

1. <span data-ttu-id="e81dc-106">Use o PowerShell tooconfigure um circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="e81dc-106">Use PowerShell tooconfigure an ExpressRoute circuit.</span></span> <span data-ttu-id="e81dc-107">Siga as instruções de Olá Olá [circuitos ExpressRoute criar](expressroute-howto-circuit-classic.md) artigo para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="e81dc-107">Follow hello instructions in hello [Create ExpressRoute circuits](expressroute-howto-circuit-classic.md) article for more details.</span></span>
2. <span data-ttu-id="e81dc-108">Conectividade de ordem de provedor de serviços de saudação.</span><span class="sxs-lookup"><span data-stu-id="e81dc-108">Order connectivity from hello service provider.</span></span> <span data-ttu-id="e81dc-109">Esse processo varia.</span><span class="sxs-lookup"><span data-stu-id="e81dc-109">This process varies.</span></span> <span data-ttu-id="e81dc-110">Entre em contato com seu provedor de conectividade para obter mais detalhes sobre como tooorder conectividade.</span><span class="sxs-lookup"><span data-stu-id="e81dc-110">Contact your connectivity provider for more details about how tooorder connectivity.</span></span>
3. <span data-ttu-id="e81dc-111">Certifique-se de que circuito Olá foi provisionado com êxito verificando o circuito de rota expressa Olá estado por meio do PowerShell de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="e81dc-111">Ensure that hello circuit has been provisioned successfully by verifying hello ExpressRoute circuit provisioning state through PowerShell.</span></span> 
4. <span data-ttu-id="e81dc-112">Configure os domínios de roteamento.</span><span class="sxs-lookup"><span data-stu-id="e81dc-112">Configure routing domains.</span></span> <span data-ttu-id="e81dc-113">Se seu provedor de conectividade gerencia a camada 3 para você, ele configurará o roteamento para o circuito.</span><span class="sxs-lookup"><span data-stu-id="e81dc-113">If your connectivity provider manages Layer 3 for you, they will configure routing for your circuit.</span></span> <span data-ttu-id="e81dc-114">Se seu provedor de conectividade apenas oferece serviços de camada 2, você deve configurar o roteamento de acordo com as diretrizes descritas em Olá [requisitos de roteamento](expressroute-routing.md) e [configuração de roteamento](expressroute-howto-routing-classic.md) páginas.</span><span class="sxs-lookup"><span data-stu-id="e81dc-114">If your connectivity provider only offers Layer 2 services, you must configure routing per guidelines described in hello [routing requirements](expressroute-routing.md) and [routing configuration](expressroute-howto-routing-classic.md) pages.</span></span>
   
   * <span data-ttu-id="e81dc-115">Habilitar o emparelhamento particular do Azure - você deve habilitar esta tooVMs tooconnect emparelhamento / serviços implantados dentro das redes virtuais na nuvem.</span><span class="sxs-lookup"><span data-stu-id="e81dc-115">Enable Azure private peering - You must enable this peering tooconnect tooVMs / cloud services deployed within virtual networks.</span></span>
   * <span data-ttu-id="e81dc-116">Habilitar o emparelhamento público do Azure - você deve habilitar o emparelhamento público do Azure se desejar tooconnect tooAzure serviços hospedados em endereços IP públicos.</span><span class="sxs-lookup"><span data-stu-id="e81dc-116">Enable Azure public peering - You must enable Azure public peering if you wish tooconnect tooAzure services hosted on public IP addresses.</span></span> <span data-ttu-id="e81dc-117">Este é um requisito tooaccess recursos do Azure se você tiver escolhido o roteamento padrão de tooenable para emparelhamento particular do Azure.</span><span class="sxs-lookup"><span data-stu-id="e81dc-117">This is a requirement tooaccess Azure resources if you have chosen tooenable default routing for Azure private peering.</span></span>
   * <span data-ttu-id="e81dc-118">Habilitar o emparelhamento da Microsoft - você deve habilitar esta tooaccess Office 365 e Dynamics 365.</span><span class="sxs-lookup"><span data-stu-id="e81dc-118">Enable Microsoft peering - You must enable this tooaccess Office 365 and Dynamics 365.</span></span> 
     
     > [!IMPORTANT]
     > <span data-ttu-id="e81dc-119">Você deve garantir que você usar um proxy separado / borda tooconnect tooMicrosoft de Olá você utiliza para Olá da Internet.</span><span class="sxs-lookup"><span data-stu-id="e81dc-119">You must ensure that you use a separate proxy / edge tooconnect tooMicrosoft than hello one you use for hello Internet.</span></span> <span data-ttu-id="e81dc-120">Usando Olá mesmo borda da saudação da Internet e de rota expressa será fazer com que o serviço de roteamento assimétrico e causar falhas de conectividade para sua rede.</span><span class="sxs-lookup"><span data-stu-id="e81dc-120">Using hello same edge for both ExpressRoute and hello Internet will cause asymmetric routing and cause connectivity outages for your network.</span></span>
     > 
     > 
     
     ![](./media/expressroute-workflows/routing-workflow.png)
5. <span data-ttu-id="e81dc-121">Vinculando virtual redes tooExpressRoute circuitos - você pode vincular um circuito de rota expressa tooyour redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="e81dc-121">Linking virtual networks tooExpressRoute circuits - You can link virtual networks tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="e81dc-122">Siga as instruções [toolink VNets](expressroute-howto-linkvnet-arm.md) tooyour circuito.</span><span class="sxs-lookup"><span data-stu-id="e81dc-122">Follow instructions [toolink VNets](expressroute-howto-linkvnet-arm.md) tooyour circuit.</span></span> <span data-ttu-id="e81dc-123">Essas VNets pode ser Olá a mesma assinatura do Azure que o circuito de rota expressa hello, ou pode estar em uma assinatura diferente.</span><span class="sxs-lookup"><span data-stu-id="e81dc-123">These VNets can either be in hello same Azure subscription as hello ExpressRoute circuit, or can be in a different subscription.</span></span>

## <a name="expressroute-circuit-provisioning-states"></a><span data-ttu-id="e81dc-124">Estados de provisionamento de circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="e81dc-124">ExpressRoute circuit provisioning states</span></span>
<span data-ttu-id="e81dc-125">Cada circuito de ExpressRoute tem dois estados:</span><span class="sxs-lookup"><span data-stu-id="e81dc-125">Each ExpressRoute circuit has two states:</span></span>

* <span data-ttu-id="e81dc-126">Estado de provisionamento do provedor de serviço</span><span class="sxs-lookup"><span data-stu-id="e81dc-126">Service provider provisioning state</span></span>
* <span data-ttu-id="e81dc-127">Status</span><span class="sxs-lookup"><span data-stu-id="e81dc-127">Status</span></span>

<span data-ttu-id="e81dc-128">O status representa o estado de provisionamento da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e81dc-128">Status represents Microsoft's provisioning state.</span></span> <span data-ttu-id="e81dc-129">Essa propriedade é definida tooEnabled quando você criar um circuito de rota expressa</span><span class="sxs-lookup"><span data-stu-id="e81dc-129">This property is set tooEnabled when you create an Expressroute circuit</span></span>

<span data-ttu-id="e81dc-130">estado de provisionamento do provedor de conectividade de saudação representa o estado de saudação no lado do provedor de conectividade hello.</span><span class="sxs-lookup"><span data-stu-id="e81dc-130">hello connectivity provider provisioning state represents hello state on hello connectivity provider's side.</span></span> <span data-ttu-id="e81dc-131">Ele pode ser *Não Provisionado*, *Provisionando* ou *Provisionado*.</span><span class="sxs-lookup"><span data-stu-id="e81dc-131">It can either be *NotProvisioned*, *Provisioning*, or *Provisioned*.</span></span> <span data-ttu-id="e81dc-132">Olá circuito de rota expressa deve estar no estado provisionado para você toobe capaz de toouse-lo.</span><span class="sxs-lookup"><span data-stu-id="e81dc-132">hello ExpressRoute circuit must be in Provisioned state for you toobe able toouse it.</span></span>

### <a name="possible-states-of-an-expressroute-circuit"></a><span data-ttu-id="e81dc-133">Possíveis estados de um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="e81dc-133">Possible states of an ExpressRoute circuit</span></span>
<span data-ttu-id="e81dc-134">Esta seção lista estados possíveis de saudação para um circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="e81dc-134">This section lists out hello possible states for an ExpressRoute circuit.</span></span>

<span data-ttu-id="e81dc-135">**No momento da criação**</span><span class="sxs-lookup"><span data-stu-id="e81dc-135">**At creation time**</span></span>

<span data-ttu-id="e81dc-136">Você verá circuito de rota expressa Olá no hello estado a seguir assim que você executar o circuito de rota expressa Olá PowerShell cmdlet toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="e81dc-136">You will see hello ExpressRoute circuit in hello following state as soon as you run hello PowerShell cmdlet toocreate hello ExpressRoute circuit.</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="e81dc-137">**Quando o provedor de conectividade está em processo de saudação de provisionamento do circuito Olá**</span><span class="sxs-lookup"><span data-stu-id="e81dc-137">**When connectivity provider is in hello process of provisioning hello circuit**</span></span>

<span data-ttu-id="e81dc-138">Você verá circuito de rota expressa Olá no hello estado a seguir assim que você passe Olá toohello chave conectividade provedor e eles começaram a saudação processo de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="e81dc-138">You will see hello ExpressRoute circuit in hello following state as soon as you pass hello service key toohello connectivity provider and they have started hello provisioning process.</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled


<span data-ttu-id="e81dc-139">**Quando o provedor de conectividade concluiu Olá processo de provisionamento**</span><span class="sxs-lookup"><span data-stu-id="e81dc-139">**When connectivity provider has completed hello provisioning process**</span></span>

<span data-ttu-id="e81dc-140">Você verá Olá circuito de rota expressa em Olá estado a seguir como provedor de conectividade Olá concluiu Olá processo de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="e81dc-140">You will see hello ExpressRoute circuit in hello following state as soon as hello connectivity provider has completed hello provisioning process.</span></span>

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled

<span data-ttu-id="e81dc-141">Configurado e ativado é Olá somente circuito de saudação do estado pode estar para você toobe capaz de toouse.</span><span class="sxs-lookup"><span data-stu-id="e81dc-141">Provisioned and Enabled is hello only state hello circuit can be in for you toobe able toouse it.</span></span> <span data-ttu-id="e81dc-142">Se você estiver usando um provedor de camada 2, configure o roteamento para o circuito somente quando ele estiver nesse estado.</span><span class="sxs-lookup"><span data-stu-id="e81dc-142">If you are using a Layer 2 provider, you can configure routing for your circuit only when it is in this state.</span></span>

<span data-ttu-id="e81dc-143">**Quando o provedor de conectividade é desprovisionamento circuito Olá**</span><span class="sxs-lookup"><span data-stu-id="e81dc-143">**When connectivity provider is deprovisioning hello circuit**</span></span>

<span data-ttu-id="e81dc-144">Se você solicitou o circuito de rota expressa Olá serviço provedor toodeprovision hello, você verá circuito Olá definir toohello estado a seguir após provedor Olá Olá desprovisionamento de processo.</span><span class="sxs-lookup"><span data-stu-id="e81dc-144">If you requested hello service provider toodeprovision hello ExpressRoute circuit, you will see hello circuit set toohello following state after hello service provider has completed hello deprovisioning process.</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="e81dc-145">Você pode escolher habilitar toore se necessário, ou executar cmdlets do PowerShell toodelete circuito de saudação.</span><span class="sxs-lookup"><span data-stu-id="e81dc-145">You can choose toore-enable it if needed, or run PowerShell cmdlets toodelete hello circuit.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="e81dc-146">Se você executar Olá circuito PowerShell cmdlet toodelete hello quando Olá ServiceProviderProvisioningState é provisionamento ou provisionado Olá falhará.</span><span class="sxs-lookup"><span data-stu-id="e81dc-146">If you run hello PowerShell cmdlet toodelete hello circuit when hello ServiceProviderProvisioningState is Provisioning or Provisioned hello operation will fail.</span></span> <span data-ttu-id="e81dc-147">Trabalhe com seu circuito de rota expressa conectividade provedor toodeprovision Olá primeiro e, em seguida, excluir o circuito de saudação.</span><span class="sxs-lookup"><span data-stu-id="e81dc-147">Please work with your connectivity provider toodeprovision hello ExpressRoute circuit first and then delete hello circuit.</span></span> <span data-ttu-id="e81dc-148">A Microsoft continuará circuito de saudação toobill até que você execute Olá circuito de saudação de toodelete de cmdlet do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e81dc-148">Microsoft will continue toobill hello circuit until you run hello PowerShell cmdlet toodelete hello circuit.</span></span>
> 
> 

## <a name="routing-session-configuration-state"></a><span data-ttu-id="e81dc-149">Estado de configuração da sessão de roteamento</span><span class="sxs-lookup"><span data-stu-id="e81dc-149">Routing session configuration state</span></span>
<span data-ttu-id="e81dc-150">Olá estado de provisionamento do BGP permite que você saiba se foi habilitado privado Olá Olá Microsoft edge.</span><span class="sxs-lookup"><span data-stu-id="e81dc-150">hello BGP provisioning state lets you know if hello BGP session has been enabled on hello Microsoft edge.</span></span> <span data-ttu-id="e81dc-151">Olá estado deve ser habilitado para você toobe toouse capaz de saudação emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="e81dc-151">hello state must be enabled for you toobe able toouse hello peering.</span></span>

<span data-ttu-id="e81dc-152">É o estado da sessão BGP toocheck importante Olá especialmente para emparelhamento da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e81dc-152">It is important toocheck hello BGP session state especially for Microsoft peering.</span></span> <span data-ttu-id="e81dc-153">Adição toohello BGP estado de provisionamento, há outro estado chamado *anunciado estado prefixos públicos*.</span><span class="sxs-lookup"><span data-stu-id="e81dc-153">In addition toohello BGP provisioning state, there is another state called *advertised public prefixes state*.</span></span> <span data-ttu-id="e81dc-154">Olá anunciado estado prefixos públicos deve estar no *configurado* state, tanto para Olá toobe de sessão BGP para cima e para a roteamento toowork ponta a ponta.</span><span class="sxs-lookup"><span data-stu-id="e81dc-154">hello advertised public prefixes state must be in *configured* state, both for hello BGP session toobe up and for your routing toowork end-to-end.</span></span> 

<span data-ttu-id="e81dc-155">Se Olá anunciado estado prefixo público definido tooa *validação necessária* estado, sessão BGP de saudação não estiver habilitado, como Olá anunciado prefixos não correspondeu hello como número em qualquer um dos registros de roteamento hello.</span><span class="sxs-lookup"><span data-stu-id="e81dc-155">If hello advertised public prefix state is set tooa *validation needed* state, hello BGP session is not enabled, as hello advertised prefixes did not match hello AS number in any of hello routing registries.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="e81dc-156">Se Olá anunciado estado prefixos públicos *validação manual* de estado, você deve abrir um tíquete de suporte com [o suporte da Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) e fornecem evidências de que você possui endereços IP de saudação anunciado ao longo com hello associado número de sistema autônomo.</span><span class="sxs-lookup"><span data-stu-id="e81dc-156">If hello advertised public prefixes state is in *manual validation* state, you must open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) and provide evidence that you own hello IP addresses advertised along with hello associated Autonomous System number.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="e81dc-157">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e81dc-157">Next steps</span></span>
* <span data-ttu-id="e81dc-158">Configurar sua conexão do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e81dc-158">Configure your ExpressRoute connection.</span></span>
  
  * [<span data-ttu-id="e81dc-159">Criar um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="e81dc-159">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-arm.md)
  * [<span data-ttu-id="e81dc-160">Configurar o roteamento</span><span class="sxs-lookup"><span data-stu-id="e81dc-160">Configure routing</span></span>](expressroute-howto-routing-arm.md)
  * [<span data-ttu-id="e81dc-161">Vincular um circuito de rota expressa do tooan de rede virtual</span><span class="sxs-lookup"><span data-stu-id="e81dc-161">Link a VNet tooan ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)

