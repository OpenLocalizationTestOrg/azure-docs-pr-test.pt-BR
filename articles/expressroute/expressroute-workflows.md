---
title: "Fluxos de trabalho para a configuração de um circuito da ExpressRoute | Microsoft Docs"
description: "Esta página fornece uma orientação pelos fluxos de trabalho de configuração de emparelhamentos e circuito de ExpressRoute"
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
ms.openlocfilehash: cba1b2cfee379e7d2b079bcb3089981ef1044d66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="expressroute-workflows-for-circuit-provisioning-and-circuit-states"></a><span data-ttu-id="5acd0-103">Fluxos de trabalho do ExpressRoute para provisionamento e estados do circuito</span><span class="sxs-lookup"><span data-stu-id="5acd0-103">ExpressRoute workflows for circuit provisioning and circuit states</span></span>
<span data-ttu-id="5acd0-104">Esta página fornece uma orientação de alto nível pelos fluxos de trabalho de provisionamento do serviço e de configuração do roteamento.</span><span class="sxs-lookup"><span data-stu-id="5acd0-104">This page walks you through the service provisioning and routing configuration workflows at a high level.</span></span>

![](./media/expressroute-workflows/expressroute-circuit-workflow.png)

<span data-ttu-id="5acd0-105">A figura e as etapas correspondentes a seguir mostram as tarefas que você deve executar para provisionar um circuito do ExpressRoute de ponta a ponta.</span><span class="sxs-lookup"><span data-stu-id="5acd0-105">The following figure and corresponding steps show the tasks you must follow in order to have an ExpressRoute circuit provisioned end-to-end.</span></span> 

1. <span data-ttu-id="5acd0-106">Use o PowerShell para configurar um circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="5acd0-106">Use PowerShell to configure an ExpressRoute circuit.</span></span> <span data-ttu-id="5acd0-107">Siga as instruções no artigo [Criar circuitos do ExpressRoute](expressroute-howto-circuit-classic.md) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="5acd0-107">Follow the instructions in the [Create ExpressRoute circuits](expressroute-howto-circuit-classic.md) article for more details.</span></span>
2. <span data-ttu-id="5acd0-108">Solicite conectividade do provedor de serviço.</span><span class="sxs-lookup"><span data-stu-id="5acd0-108">Order connectivity from the service provider.</span></span> <span data-ttu-id="5acd0-109">Esse processo varia.</span><span class="sxs-lookup"><span data-stu-id="5acd0-109">This process varies.</span></span> <span data-ttu-id="5acd0-110">Entre em contato com o provedor de conectividade para obter mais detalhes sobre a solicitação de conectividade.</span><span class="sxs-lookup"><span data-stu-id="5acd0-110">Contact your connectivity provider for more details about how to order connectivity.</span></span>
3. <span data-ttu-id="5acd0-111">Confira se o circuito foi provisionado com sucesso verificando o estado de provisionamento do circuito do ExpressRoute por meio do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5acd0-111">Ensure that the circuit has been provisioned successfully by verifying the ExpressRoute circuit provisioning state through PowerShell.</span></span> 
4. <span data-ttu-id="5acd0-112">Configure os domínios de roteamento.</span><span class="sxs-lookup"><span data-stu-id="5acd0-112">Configure routing domains.</span></span> <span data-ttu-id="5acd0-113">Se seu provedor de conectividade gerencia a camada 3 para você, ele configurará o roteamento para o circuito.</span><span class="sxs-lookup"><span data-stu-id="5acd0-113">If your connectivity provider manages Layer 3 for you, they will configure routing for your circuit.</span></span> <span data-ttu-id="5acd0-114">Se o seu provedor de conectividade oferecer somente os serviços de Camada 2, configure o roteamento de acordo com as diretrizes descritas nas páginas [requisitos de roteamento](expressroute-routing.md) e [configuração de roteamento](expressroute-howto-routing-classic.md).</span><span class="sxs-lookup"><span data-stu-id="5acd0-114">If your connectivity provider only offers Layer 2 services, you must configure routing per guidelines described in the [routing requirements](expressroute-routing.md) and [routing configuration](expressroute-howto-routing-classic.md) pages.</span></span>
   
   * <span data-ttu-id="5acd0-115">Habilitar o emparelhamento privado do Azure - Você deve habilitar esse emparelhamento para se conectar a VMs/serviços de nuvem implantados dentro das redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="5acd0-115">Enable Azure private peering - You must enable this peering to connect to VMs / cloud services deployed within virtual networks.</span></span>
   * <span data-ttu-id="5acd0-116">Habilitar o emparelhamento público do Azure - Você deve habilitar o emparelhamento público do Azure se quiser se conectar aos serviços do Azure hospedados em endereços IP públicos.</span><span class="sxs-lookup"><span data-stu-id="5acd0-116">Enable Azure public peering - You must enable Azure public peering if you wish to connect to Azure services hosted on public IP addresses.</span></span> <span data-ttu-id="5acd0-117">Esse é um requisito para acessar os recursos do Azure se você tiver optado por habilitar o roteamento padrão para emparelhamento privado do Azure.</span><span class="sxs-lookup"><span data-stu-id="5acd0-117">This is a requirement to access Azure resources if you have chosen to enable default routing for Azure private peering.</span></span>
   * <span data-ttu-id="5acd0-118">Habilitar o emparelhamento da Microsoft – você deve habilitar isso para acessar o Office 365 e o Dynamics 365.</span><span class="sxs-lookup"><span data-stu-id="5acd0-118">Enable Microsoft peering - You must enable this to access Office 365 and Dynamics 365.</span></span> 
     
     > [!IMPORTANT]
     > <span data-ttu-id="5acd0-119">Use um proxy/borda diferente da usada para a Internet para se conectar à Microsoft.</span><span class="sxs-lookup"><span data-stu-id="5acd0-119">You must ensure that you use a separate proxy / edge to connect to Microsoft than the one you use for the Internet.</span></span> <span data-ttu-id="5acd0-120">Usar a mesma borda para o ExpressRoute e para a Internet causará o roteamento assimétrico e falhas de conectividade em sua rede.</span><span class="sxs-lookup"><span data-stu-id="5acd0-120">Using the same edge for both ExpressRoute and the Internet will cause asymmetric routing and cause connectivity outages for your network.</span></span>
     > 
     > 
     
     ![](./media/expressroute-workflows/routing-workflow.png)
5. <span data-ttu-id="5acd0-121">Vinculando redes virtuais aos circuitos do ExpressRoute - Você pode vincular redes virtuais ao circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="5acd0-121">Linking virtual networks to ExpressRoute circuits - You can link virtual networks to your ExpressRoute circuit.</span></span> <span data-ttu-id="5acd0-122">Siga as instruções [para vincular redes virtuais](expressroute-howto-linkvnet-arm.md) ao seu circuito.</span><span class="sxs-lookup"><span data-stu-id="5acd0-122">Follow instructions [to link VNets](expressroute-howto-linkvnet-arm.md) to your circuit.</span></span> <span data-ttu-id="5acd0-123">Essas redes virtuais podem estar na mesma assinatura do Azure que o circuito do ExpressRoute ou podem estar em uma assinatura diferente.</span><span class="sxs-lookup"><span data-stu-id="5acd0-123">These VNets can either be in the same Azure subscription as the ExpressRoute circuit, or can be in a different subscription.</span></span>

## <a name="expressroute-circuit-provisioning-states"></a><span data-ttu-id="5acd0-124">Estados de provisionamento de circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="5acd0-124">ExpressRoute circuit provisioning states</span></span>
<span data-ttu-id="5acd0-125">Cada circuito de ExpressRoute tem dois estados:</span><span class="sxs-lookup"><span data-stu-id="5acd0-125">Each ExpressRoute circuit has two states:</span></span>

* <span data-ttu-id="5acd0-126">Estado de provisionamento do provedor de serviço</span><span class="sxs-lookup"><span data-stu-id="5acd0-126">Service provider provisioning state</span></span>
* <span data-ttu-id="5acd0-127">Status</span><span class="sxs-lookup"><span data-stu-id="5acd0-127">Status</span></span>

<span data-ttu-id="5acd0-128">O status representa o estado de provisionamento da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="5acd0-128">Status represents Microsoft's provisioning state.</span></span> <span data-ttu-id="5acd0-129">Essa propriedade é definida como Habilitada quando você cria um circuito de ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="5acd0-129">This property is set to Enabled when you create an Expressroute circuit</span></span>

<span data-ttu-id="5acd0-130">O estado de provisionamento do provedor de conectividade representa o estado no lado do provedor de conectividade.</span><span class="sxs-lookup"><span data-stu-id="5acd0-130">The connectivity provider provisioning state represents the state on the connectivity provider's side.</span></span> <span data-ttu-id="5acd0-131">Ele pode ser *Não Provisionado*, *Provisionando* ou *Provisionado*.</span><span class="sxs-lookup"><span data-stu-id="5acd0-131">It can either be *NotProvisioned*, *Provisioning*, or *Provisioned*.</span></span> <span data-ttu-id="5acd0-132">O circuito do ExpressRoute deverá estar no estado Provisionado para que possa usá-lo.</span><span class="sxs-lookup"><span data-stu-id="5acd0-132">The ExpressRoute circuit must be in Provisioned state for you to be able to use it.</span></span>

### <a name="possible-states-of-an-expressroute-circuit"></a><span data-ttu-id="5acd0-133">Possíveis estados de um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="5acd0-133">Possible states of an ExpressRoute circuit</span></span>
<span data-ttu-id="5acd0-134">Esta seção lista os possíveis estados de um circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="5acd0-134">This section lists out the possible states for an ExpressRoute circuit.</span></span>

<span data-ttu-id="5acd0-135">**No momento da criação**</span><span class="sxs-lookup"><span data-stu-id="5acd0-135">**At creation time**</span></span>

<span data-ttu-id="5acd0-136">Você verá o circuito do ExpressRoute no seguinte estado assim que executar o cmdlet do PowerShell para criar um circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="5acd0-136">You will see the ExpressRoute circuit in the following state as soon as you run the PowerShell cmdlet to create the ExpressRoute circuit.</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="5acd0-137">**Quando o provedor de conectividade estiver no processo de provisionamento do circuito**</span><span class="sxs-lookup"><span data-stu-id="5acd0-137">**When connectivity provider is in the process of provisioning the circuit**</span></span>

<span data-ttu-id="5acd0-138">Você verá o circuito do ExpressRoute no estado a seguir assim que passar a chave de serviço para o provedor de conectividade, e ele tiver iniciado o processo de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="5acd0-138">You will see the ExpressRoute circuit in the following state as soon as you pass the service key to the connectivity provider and they have started the provisioning process.</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled


<span data-ttu-id="5acd0-139">**Quando o provedor de conectividade tiver concluído o processo de provisionamento**</span><span class="sxs-lookup"><span data-stu-id="5acd0-139">**When connectivity provider has completed the provisioning process**</span></span>

<span data-ttu-id="5acd0-140">Você verá o circuito do ExpressRoute no seguinte estado assim que o provedor de conectividade tiver concluído o processo de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="5acd0-140">You will see the ExpressRoute circuit in the following state as soon as the connectivity provider has completed the provisioning process.</span></span>

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled

<span data-ttu-id="5acd0-141">Provisionado e Habilitado são os únicos estados nos quais o circuito pode estar para você poder usá-lo.</span><span class="sxs-lookup"><span data-stu-id="5acd0-141">Provisioned and Enabled is the only state the circuit can be in for you to be able to use it.</span></span> <span data-ttu-id="5acd0-142">Se você estiver usando um provedor de camada 2, configure o roteamento para o circuito somente quando ele estiver nesse estado.</span><span class="sxs-lookup"><span data-stu-id="5acd0-142">If you are using a Layer 2 provider, you can configure routing for your circuit only when it is in this state.</span></span>

<span data-ttu-id="5acd0-143">**Quando o provedor de conectividade estiver desprovisionando o circuito**</span><span class="sxs-lookup"><span data-stu-id="5acd0-143">**When connectivity provider is deprovisioning the circuit**</span></span>

<span data-ttu-id="5acd0-144">Se você tiver solicitado ao provedor de serviços o desprovisionamento do circuito do ExpressRoute, verá o circuito definido com o estado a seguir, após o provedor de serviços ter concluído o processo de desprovisionamento.</span><span class="sxs-lookup"><span data-stu-id="5acd0-144">If you requested the service provider to deprovision the ExpressRoute circuit, you will see the circuit set to the following state after the service provider has completed the deprovisioning process.</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="5acd0-145">Você pode optar por habilitá-lo novamente se for necessário, ou executar cmdlets do PowerShell para excluir o circuito.</span><span class="sxs-lookup"><span data-stu-id="5acd0-145">You can choose to re-enable it if needed, or run PowerShell cmdlets to delete the circuit.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="5acd0-146">Se você executar o cmdlet do PowerShell para excluir o circuito quando a ServiceProviderProvisioningState for Provisionando ou Provisionado, a operação falhará.</span><span class="sxs-lookup"><span data-stu-id="5acd0-146">If you run the PowerShell cmdlet to delete the circuit when the ServiceProviderProvisioningState is Provisioning or Provisioned the operation will fail.</span></span> <span data-ttu-id="5acd0-147">Trabalhe com seu provedor de conectividade para desprovisionar o circuito de ExpressRoute primeiro e, em seguida, exclua o circuito.</span><span class="sxs-lookup"><span data-stu-id="5acd0-147">Please work with your connectivity provider to deprovision the ExpressRoute circuit first and then delete the circuit.</span></span> <span data-ttu-id="5acd0-148">A Microsoft continuará a cobrar pelo circuito até que você execute o cmdlet do PowerShell para exclui-lo.</span><span class="sxs-lookup"><span data-stu-id="5acd0-148">Microsoft will continue to bill the circuit until you run the PowerShell cmdlet to delete the circuit.</span></span>
> 
> 

## <a name="routing-session-configuration-state"></a><span data-ttu-id="5acd0-149">Estado de configuração da sessão de roteamento</span><span class="sxs-lookup"><span data-stu-id="5acd0-149">Routing session configuration state</span></span>
<span data-ttu-id="5acd0-150">O estado de provisionamento BGP permite que você saiba se a sessão BGP foi habilitada na borda da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="5acd0-150">The BGP provisioning state lets you know if the BGP session has been enabled on the Microsoft edge.</span></span> <span data-ttu-id="5acd0-151">O estado deve ser habilitado para que você possa usar o emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="5acd0-151">The state must be enabled for you to be able to use the peering.</span></span>

<span data-ttu-id="5acd0-152">É importante verificar o estado da sessão BGP, especialmente para o emparelhamento da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="5acd0-152">It is important to check the BGP session state especially for Microsoft peering.</span></span> <span data-ttu-id="5acd0-153">Além do estado de provisionamento BGP, há outro estado chamado *estado de prefixos públicos anunciados*.</span><span class="sxs-lookup"><span data-stu-id="5acd0-153">In addition to the BGP provisioning state, there is another state called *advertised public prefixes state*.</span></span> <span data-ttu-id="5acd0-154">O estado de prefixos públicos anunciados deve ser *configurado* , tanto para que a sessão BGP fique ativa quanto para o roteamento funcionar completamente.</span><span class="sxs-lookup"><span data-stu-id="5acd0-154">The advertised public prefixes state must be in *configured* state, both for the BGP session to be up and for your routing to work end-to-end.</span></span> 

<span data-ttu-id="5acd0-155">Se o estado de prefixo público anunciado for definido como *validação necessária* , a sessão BGP não estará habilitada, pois os prefixos anunciados não corresponderam ao número AS em qualquer um dos registros do roteamento.</span><span class="sxs-lookup"><span data-stu-id="5acd0-155">If the advertised public prefix state is set to a *validation needed* state, the BGP session is not enabled, as the advertised prefixes did not match the AS number in any of the routing registries.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="5acd0-156">Se o estado de prefixos públicos anunciados for *validação manual* , será necessário abrir um tíquete de suporte com o [suporte da Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) e fornecer provas de que você possui os endereços IP anunciados juntamente com o número do Sistema Autônomo associado.</span><span class="sxs-lookup"><span data-stu-id="5acd0-156">If the advertised public prefixes state is in *manual validation* state, you must open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) and provide evidence that you own the IP addresses advertised along with the associated Autonomous System number.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="5acd0-157">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5acd0-157">Next steps</span></span>
* <span data-ttu-id="5acd0-158">Configurar sua conexão do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="5acd0-158">Configure your ExpressRoute connection.</span></span>
  
  * [<span data-ttu-id="5acd0-159">Criar um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="5acd0-159">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-arm.md)
  * [<span data-ttu-id="5acd0-160">Configurar o roteamento</span><span class="sxs-lookup"><span data-stu-id="5acd0-160">Configure routing</span></span>](expressroute-howto-routing-arm.md)
  * [<span data-ttu-id="5acd0-161">Vincular uma rede virtual a um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="5acd0-161">Link a VNet to an ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)

