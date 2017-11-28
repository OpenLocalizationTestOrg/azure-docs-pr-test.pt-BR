---
title: "Vincular um circuito de rota expressa do tooan de rede virtual: PowerShell: clássico: Azure | Microsoft Docs"
description: "Este documento fornece uma visão geral de como toolink virtual redes circuitos de tooExpressRoute (VNets) usando o modelo de implantação clássico hello e PowerShell."
services: expressroute
documentationcenter: na
author: ganesr
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: 9b53fd72-9b6b-4844-80b9-4e1d54fd0c17
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/28/2017
ms.author: ganesr
ms.openlocfilehash: 6b8a01dcd4bbb9618ec3dd438cf0107538fb2a7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit-using-powershell-classic"></a><span data-ttu-id="38b43-103">Conecte-se a um circuito de rota expressa do tooan de rede virtual usando o PowerShell (clássico)</span><span class="sxs-lookup"><span data-stu-id="38b43-103">Connect a virtual network tooan ExpressRoute circuit using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="38b43-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="38b43-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="38b43-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="38b43-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="38b43-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="38b43-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="38b43-107">Vídeo – Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="38b43-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="38b43-108">PowerShell (clássico)</span><span class="sxs-lookup"><span data-stu-id="38b43-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
>

<span data-ttu-id="38b43-109">Este artigo o ajudará a vincular circuitos do ExpressRoute tooAzure redes virtuais (VNets) usando o modelo de implantação clássico hello e PowerShell.</span><span class="sxs-lookup"><span data-stu-id="38b43-109">This article will help you link virtual networks (VNets) tooAzure ExpressRoute circuits by using hello classic deployment model and PowerShell.</span></span> <span data-ttu-id="38b43-110">Redes virtuais podem ser em Olá a mesma assinatura ou pode fazer parte de outra assinatura.</span><span class="sxs-lookup"><span data-stu-id="38b43-110">Virtual networks can either be in hello same subscription or can be part of another subscription.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="38b43-111">**Sobre modelos de implantação do Azure**</span><span class="sxs-lookup"><span data-stu-id="38b43-111">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="configuration-prerequisites"></a><span data-ttu-id="38b43-112">Pré-requisitos de configuração</span><span class="sxs-lookup"><span data-stu-id="38b43-112">Configuration prerequisites</span></span>
1. <span data-ttu-id="38b43-113">Você precisa Olá a versão mais recente dos módulos do PowerShell do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="38b43-113">You need hello latest version of hello Azure PowerShell modules.</span></span> <span data-ttu-id="38b43-114">Você pode baixar módulos do PowerShell mais recentes de saudação do hello seção PowerShell Olá [página Downloads do Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="38b43-114">You can download hello latest PowerShell modules from hello PowerShell section of hello [Azure Downloads page](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="38b43-115">Siga as instruções de saudação em [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para obter orientação passo a passo sobre como tooconfigure os módulos do computador toouse hello Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="38b43-115">Follow hello instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for step-by-step guidance on how tooconfigure your computer toouse hello Azure PowerShell modules.</span></span>
2. <span data-ttu-id="38b43-116">Você precisa Olá tooreview [pré-requisitos](expressroute-prerequisites.md), [requisitos de roteamento](expressroute-routing.md), e [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração.</span><span class="sxs-lookup"><span data-stu-id="38b43-116">You need tooreview hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
3. <span data-ttu-id="38b43-117">Você deve ter um circuito do ExpressRoute ativo.</span><span class="sxs-lookup"><span data-stu-id="38b43-117">You must have an active ExpressRoute circuit.</span></span>
   * <span data-ttu-id="38b43-118">Siga as instruções de saudação muito[criar um circuito de rota expressa](expressroute-howto-circuit-classic.md) e ter seu provedor de conectividade habilitar circuito hello.</span><span class="sxs-lookup"><span data-stu-id="38b43-118">Follow hello instructions too[create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have your connectivity provider enable hello circuit.</span></span>
   * <span data-ttu-id="38b43-119">Verifique se o emparelhamento privado do Azure está configurado para seu circuito.</span><span class="sxs-lookup"><span data-stu-id="38b43-119">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="38b43-120">Consulte Olá [Configurar roteamento](expressroute-howto-routing-classic.md) artigo para obter instruções de roteamentos.</span><span class="sxs-lookup"><span data-stu-id="38b43-120">See hello [Configure routing](expressroute-howto-routing-classic.md) article for routing instructions.</span></span>
   * <span data-ttu-id="38b43-121">Certifique-se de que o emparelhamento particular do Azure está configurado e Olá emparelhamento via protocolo BGP entre sua rede e a Microsoft está ativo para que você pode habilitar a conectividade de ponta a ponta.</span><span class="sxs-lookup"><span data-stu-id="38b43-121">Ensure that Azure private peering is configured and hello BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
   * <span data-ttu-id="38b43-122">É necessário ter uma rede virtual e um gateway de rede virtual criados e totalmente provisionados.</span><span class="sxs-lookup"><span data-stu-id="38b43-122">You must have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="38b43-123">Siga as instruções de saudação muito[configurar uma rede virtual para o ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span><span class="sxs-lookup"><span data-stu-id="38b43-123">Follow hello instructions too[configure a virtual network for ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span></span>

<span data-ttu-id="38b43-124">Você pode vincular o too10 redes virtuais tooan circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="38b43-124">You can link up too10 virtual networks tooan ExpressRoute circuit.</span></span> <span data-ttu-id="38b43-125">Todas as redes virtuais devem estar em Olá mesma região geopolíticas.</span><span class="sxs-lookup"><span data-stu-id="38b43-125">All virtual networks must be in hello same geopolitical region.</span></span> <span data-ttu-id="38b43-126">Você pode vincular um número maior de redes virtuais tooyour circuito de rota expressa ou vincular redes virtuais que estão em outras regiões geopolíticas se você habilitou o complemento do premium Olá rota expressa.</span><span class="sxs-lookup"><span data-stu-id="38b43-126">You can link a larger number of virtual networks tooyour ExpressRoute circuit, or link virtual networks that are in other geopolitical regions if you enabled hello ExpressRoute premium add-on.</span></span> <span data-ttu-id="38b43-127">Verificar Olá [perguntas frequentes sobre](expressroute-faqs.md) para obter mais detalhes sobre o complemento do premium Olá.</span><span class="sxs-lookup"><span data-stu-id="38b43-127">Check hello [FAQ](expressroute-faqs.md) for more details on hello premium add-on.</span></span>

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a><span data-ttu-id="38b43-128">Conectar uma rede virtual no hello mesmo circuito de tooa de assinatura</span><span class="sxs-lookup"><span data-stu-id="38b43-128">Connect a virtual network in hello same subscription tooa circuit</span></span>
<span data-ttu-id="38b43-129">Você pode vincular um circuito de rota expressa do tooan de rede virtual usando Olá cmdlet a seguir.</span><span class="sxs-lookup"><span data-stu-id="38b43-129">You can link a virtual network tooan ExpressRoute circuit by using hello following cmdlet.</span></span> <span data-ttu-id="38b43-130">Verifique se esse gateway de rede virtual Olá é criado e está pronto para vinculação antes de executar o cmdlet hello.</span><span class="sxs-lookup"><span data-stu-id="38b43-130">Make sure that hello virtual network gateway is created and is ready for linking before you run hello cmdlet.</span></span>

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"
    Provisioned

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a><span data-ttu-id="38b43-131">Conectar uma rede virtual em um circuito de tooa assinatura diferente</span><span class="sxs-lookup"><span data-stu-id="38b43-131">Connect a virtual network in a different subscription tooa circuit</span></span>
<span data-ttu-id="38b43-132">Você pode compartilhar um circuito do ExpressRoute entre várias assinaturas.</span><span class="sxs-lookup"><span data-stu-id="38b43-132">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="38b43-133">Olá figura a seguir mostra um esquemático simples de como funciona o compartilhamento para circuitos ExpressRoute entre várias assinaturas.</span><span class="sxs-lookup"><span data-stu-id="38b43-133">hello following figure shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="38b43-134">Cada uma das nuvens menores de saudação dentro da nuvem grande Olá é toorepresent usadas assinaturas que pertencem a toodifferent departamentos dentro de uma organização.</span><span class="sxs-lookup"><span data-stu-id="38b43-134">Each of hello smaller clouds within hello large cloud is used toorepresent subscriptions that belong toodifferent departments within an organization.</span></span> <span data-ttu-id="38b43-135">Cada um dos departamentos hello dentro da organização Olá pode usar sua própria assinatura para implantar seus serviços – mas departamentos Olá pode compartilhar uma única rede rota expressa circuito tooconnect tooyour back local.</span><span class="sxs-lookup"><span data-stu-id="38b43-135">Each of hello departments within hello organization can use their own subscription for deploying their services--but hello departments can share a single ExpressRoute circuit tooconnect back tooyour on-premises network.</span></span> <span data-ttu-id="38b43-136">Um único departamento (neste exemplo: IT) pode ter o circuito de rota expressa hello.</span><span class="sxs-lookup"><span data-stu-id="38b43-136">A single department (in this example: IT) can own hello ExpressRoute circuit.</span></span> <span data-ttu-id="38b43-137">Outras assinaturas dentro da organização Olá podem usar o circuito de rota expressa hello.</span><span class="sxs-lookup"><span data-stu-id="38b43-137">Other subscriptions within hello organization can use hello ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="38b43-138">Encargos de largura de banda e conectividade para o circuito dedicado de saudação será proprietário do circuito de rota expressa toohello aplicado.</span><span class="sxs-lookup"><span data-stu-id="38b43-138">Connectivity and bandwidth charges for hello dedicated circuit will be applied toohello ExpressRoute circuit owner.</span></span> <span data-ttu-id="38b43-139">Todas as redes virtuais compartilham Olá mesma largura de banda.</span><span class="sxs-lookup"><span data-stu-id="38b43-139">All virtual networks share hello same bandwidth.</span></span>
> 
> 

![Conectividade entre assinaturas](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration"></a><span data-ttu-id="38b43-141">Administração</span><span class="sxs-lookup"><span data-stu-id="38b43-141">Administration</span></span>
<span data-ttu-id="38b43-142">Olá *proprietário do circuito* é Olá administrador/coadministrator de assinatura de saudação na qual Olá rota expressa circuito é criado.</span><span class="sxs-lookup"><span data-stu-id="38b43-142">hello *circuit owner* is hello administrator/coadministrator of hello subscription in which hello ExpressRoute circuit is created.</span></span> <span data-ttu-id="38b43-143">Olá proprietário do circuito pode autorizar os administradores/coadministrators de outras assinaturas, chamado tooas *circuito usuários*, Olá toouse dedicado circuito que eles possuem.</span><span class="sxs-lookup"><span data-stu-id="38b43-143">hello circuit owner can authorize administrators/coadministrators of other subscriptions, referred tooas *circuit users*, toouse hello dedicated circuit that they own.</span></span> <span data-ttu-id="38b43-144">Usuários circuito pode de circuito de rota expressa toouse autorizados Olá organização vincular a rede virtual de saudação em seu toohello assinatura circuito de rota expressa depois que eles são autorizados.</span><span class="sxs-lookup"><span data-stu-id="38b43-144">Circuit users who are authorized toouse hello organization's ExpressRoute circuit can link hello virtual network in their subscription toohello ExpressRoute circuit after they are authorized.</span></span>

<span data-ttu-id="38b43-145">proprietário do circuito Olá tem autorizações de toomodify e revoke power Olá a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="38b43-145">hello circuit owner has hello power toomodify and revoke authorizations at any time.</span></span> <span data-ttu-id="38b43-146">Revogar uma autorização resultará em todos os links sejam excluídos da assinatura Olá cujo acesso foi revogado.</span><span class="sxs-lookup"><span data-stu-id="38b43-146">Revoking an authorization will result in all links being deleted from hello subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="38b43-147">Operações do proprietário do circuito</span><span class="sxs-lookup"><span data-stu-id="38b43-147">Circuit owner operations</span></span>

<span data-ttu-id="38b43-148">**Criando uma autorização**</span><span class="sxs-lookup"><span data-stu-id="38b43-148">**Creating an authorization**</span></span>

<span data-ttu-id="38b43-149">Olá, proprietário do circuito autoriza os administradores de saudação de outras assinaturas toouse Olá especificado circuito.</span><span class="sxs-lookup"><span data-stu-id="38b43-149">hello circuit owner authorizes hello administrators of other subscriptions toouse hello specified circuit.</span></span> <span data-ttu-id="38b43-150">Em Olá exemplo a seguir, administrador de saudação do circuito hello (TI da Contoso) habilita administrador Olá de outro toolink de assinatura (desenvolvimento de teste), o circuito de toohello tootwo redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="38b43-150">In hello following example, hello administrator of hello circuit (Contoso IT) enables hello administrator of another subscription (Dev-Test) toolink up tootwo virtual networks toohello circuit.</span></span> <span data-ttu-id="38b43-151">administrador de TI da Contoso Olá permite isso especificando a ID de teste de desenvolvimento Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="38b43-151">hello Contoso IT administrator enables this by specifying hello Dev-Test Microsoft ID.</span></span> <span data-ttu-id="38b43-152">Olá cmdlet não envia email toohello especificado o ID da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="38b43-152">hello cmdlet doesn't send email toohello specified Microsoft ID.</span></span> <span data-ttu-id="38b43-153">proprietário do circuito Olá precisa tooexplicitly notificar Olá outro proprietário da assinatura que Olá autorização é concluído.</span><span class="sxs-lookup"><span data-stu-id="38b43-153">hello circuit owner needs tooexplicitly notify hello other subscription owner that hello authorization is complete.</span></span>

    New-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -Description "Dev-Test Links" -Limit 2 -MicrosoftIds 'devtest@contoso.com'

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : **********************************
    MicrosoftIds        : devtest@contoso.com
    Used                : 0

<span data-ttu-id="38b43-154">**Examinando autorizações**</span><span class="sxs-lookup"><span data-stu-id="38b43-154">**Reviewing authorizations**</span></span>

<span data-ttu-id="38b43-155">proprietário do circuito Olá pode revisar todas as autorizações que são emitidas em um circuito específico executando Olá cmdlet a seguir:</span><span class="sxs-lookup"><span data-stu-id="38b43-155">hello circuit owner can review all authorizations that are issued on a particular circuit by running hello following cmdlet:</span></span>

    Get-AzureDedicatedCircuitLinkAuthorization -ServiceKey: "**************************"

    Description         : EngineeringTeam
    Limit               : 3
    LinkAuthorizationId : ####################################
    MicrosoftIds        : engadmin@contoso.com
    Used                : 1

    Description         : MarketingTeam
    Limit               : 1
    LinkAuthorizationId : @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
    MicrosoftIds        : marketingadmin@contoso.com
    Used                : 0

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : salesadmin@contoso.com
    Used                : 2


<span data-ttu-id="38b43-156">**Atualizando autorizações**</span><span class="sxs-lookup"><span data-stu-id="38b43-156">**Updating authorizations**</span></span>

<span data-ttu-id="38b43-157">proprietário do circuito Olá pode modificar autorizações usando Olá cmdlet a seguir:</span><span class="sxs-lookup"><span data-stu-id="38b43-157">hello circuit owner can modify authorizations by using hello following cmdlet:</span></span>

    Set-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -AuthorizationId "&&&&&&&&&&&&&&&&&&&&&&&&&&&&"-Limit 5

    Description         : Dev-Test Links
    Limit               : 5
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : devtest@contoso.com
    Used                : 0


<span data-ttu-id="38b43-158">**Excluindo autorizações**</span><span class="sxs-lookup"><span data-stu-id="38b43-158">**Deleting authorizations**</span></span>

<span data-ttu-id="38b43-159">proprietário do circuito Olá pode revogar/excluir autorizações toohello usuário executando Olá cmdlet a seguir:</span><span class="sxs-lookup"><span data-stu-id="38b43-159">hello circuit owner can revoke/delete authorizations toohello user by running hello following cmdlet:</span></span>

    Remove-AzureDedicatedCircuitLinkAuthorization -ServiceKey "*****************************" -AuthorizationId "###############################"


### <a name="circuit-user-operations"></a><span data-ttu-id="38b43-160">Operações do usuário do circuito</span><span class="sxs-lookup"><span data-stu-id="38b43-160">Circuit user operations</span></span>

<span data-ttu-id="38b43-161">**Examinando autorizações**</span><span class="sxs-lookup"><span data-stu-id="38b43-161">**Reviewing authorizations**</span></span>

<span data-ttu-id="38b43-162">usuários do circuito Olá poderá examinar autorizações usando Olá cmdlet a seguir:</span><span class="sxs-lookup"><span data-stu-id="38b43-162">hello circuit user can review authorizations by using hello following cmdlet:</span></span>

    Get-AzureAuthorizedDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : ContosoIT
    Location                         : Washington DC
    MaximumAllowedLinks              : 2
    ServiceKey                       : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled
    UsedLinks                        : 0

<span data-ttu-id="38b43-163">**Resgatando autorizações de link**</span><span class="sxs-lookup"><span data-stu-id="38b43-163">**Redeeming link authorizations**</span></span>

<span data-ttu-id="38b43-164">usuários do circuito Olá podem executar Olá tooredeem cmdlet a seguir uma autorização de link:</span><span class="sxs-lookup"><span data-stu-id="38b43-164">hello circuit user can run hello following cmdlet tooredeem a link authorization:</span></span>

    New-AzureDedicatedCircuitLink –servicekey "&&&&&&&&&&&&&&&&&&&&&&&&&&" –VnetName 'SalesVNET1'

    State VnetName
    ----- --------
    Provisioned SalesVNET1

<span data-ttu-id="38b43-165">Execute este comando em assinatura Olá recentemente vinculado para rede virtual hello:</span><span class="sxs-lookup"><span data-stu-id="38b43-165">Run this command in hello newly linked subscription for hello virtual network:</span></span>

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"

## <a name="next-steps"></a><span data-ttu-id="38b43-166">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="38b43-166">Next steps</span></span>
<span data-ttu-id="38b43-167">Para obter mais informações sobre a rota expressa, consulte Olá [perguntas Frequentes do ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="38b43-167">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

