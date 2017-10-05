---
title: "Vincular uma rede virtual a um circuito ExpressRoute: PowerShell: clássico: Azure| Microsoft Docs"
description: "Este documento fornece uma visão geral de como vincular as redes virtuais (VNets) aos circuitos de ExpressRoute usando o modelo de implantação clássico e o PowerShell."
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
ms.openlocfilehash: 8df8a4c6ff0897c821e13248e0494b17e1a4992d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-a-virtual-network-to-an-expressroute-circuit-using-powershell-classic"></a><span data-ttu-id="5dc01-103">Conectar uma rede virtual a um circuito do ExpressRoute usando o PowerShell (clássico)</span><span class="sxs-lookup"><span data-stu-id="5dc01-103">Connect a virtual network to an ExpressRoute circuit using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5dc01-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="5dc01-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="5dc01-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5dc01-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="5dc01-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="5dc01-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="5dc01-107">Vídeo – Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="5dc01-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="5dc01-108">PowerShell (clássico)</span><span class="sxs-lookup"><span data-stu-id="5dc01-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
>

<span data-ttu-id="5dc01-109">Este artigo o ajudará a vincular as redes virtuais (VNets) aos circuitos de Azure ExpressRoute usando o modelo de implantação clássico e o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5dc01-109">This article will help you link virtual networks (VNets) to Azure ExpressRoute circuits by using the classic deployment model and PowerShell.</span></span> <span data-ttu-id="5dc01-110">As redes virtuais podem estar na mesma assinatura ou fazer parte de outra assinatura.</span><span class="sxs-lookup"><span data-stu-id="5dc01-110">Virtual networks can either be in the same subscription or can be part of another subscription.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="5dc01-111">**Sobre modelos de implantação do Azure**</span><span class="sxs-lookup"><span data-stu-id="5dc01-111">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="configuration-prerequisites"></a><span data-ttu-id="5dc01-112">Pré-requisitos de configuração</span><span class="sxs-lookup"><span data-stu-id="5dc01-112">Configuration prerequisites</span></span>
1. <span data-ttu-id="5dc01-113">Você precisa da última versão dos módulos do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5dc01-113">You need the latest version of the Azure PowerShell modules.</span></span> <span data-ttu-id="5dc01-114">Baixe os módulos mais recente do PowerShell na seção PowerShell da [página Downloads do Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="5dc01-114">You can download the latest PowerShell modules from the PowerShell section of the [Azure Downloads page](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="5dc01-115">Siga as instruções em [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview) para obter orientações passo a passo sobre como configurar o computador para usar os módulos do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5dc01-115">Follow the instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) for step-by-step guidance on how to configure your computer to use the Azure PowerShell modules.</span></span>
2. <span data-ttu-id="5dc01-116">Leia os [pré-requisitos](expressroute-prerequisites.md), os [requisitos de roteamento](expressroute-routing.md) e os [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração.</span><span class="sxs-lookup"><span data-stu-id="5dc01-116">You need to review the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
3. <span data-ttu-id="5dc01-117">Você deve ter um circuito do ExpressRoute ativo.</span><span class="sxs-lookup"><span data-stu-id="5dc01-117">You must have an active ExpressRoute circuit.</span></span>
   * <span data-ttu-id="5dc01-118">Siga as instruções para [criar um circuito do ExpressRoute](expressroute-howto-circuit-classic.md) e para que o provedor de conectividade habilite o circuito.</span><span class="sxs-lookup"><span data-stu-id="5dc01-118">Follow the instructions to [create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have your connectivity provider enable the circuit.</span></span>
   * <span data-ttu-id="5dc01-119">Verifique se o emparelhamento privado do Azure está configurado para seu circuito.</span><span class="sxs-lookup"><span data-stu-id="5dc01-119">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="5dc01-120">Veja o artigo [Configurar roteamento](expressroute-howto-routing-classic.md) para obter instruções sobre roteamento.</span><span class="sxs-lookup"><span data-stu-id="5dc01-120">See the [Configure routing](expressroute-howto-routing-classic.md) article for routing instructions.</span></span>
   * <span data-ttu-id="5dc01-121">Verifique se o emparelhamento privado do Azure está configurado e se o emparelhamento BGP entre sua rede e a Microsoft está ativo para que você possa habilitar a conectividade de ponta a ponta.</span><span class="sxs-lookup"><span data-stu-id="5dc01-121">Ensure that Azure private peering is configured and the BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
   * <span data-ttu-id="5dc01-122">É necessário ter uma rede virtual e um gateway de rede virtual criados e totalmente provisionados.</span><span class="sxs-lookup"><span data-stu-id="5dc01-122">You must have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="5dc01-123">Siga as instruções para [configurar uma rede virtual para o ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span><span class="sxs-lookup"><span data-stu-id="5dc01-123">Follow the instructions to [configure a virtual network for ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span></span>

<span data-ttu-id="5dc01-124">Você pode vincular até 10 redes virtuais a um circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="5dc01-124">You can link up to 10 virtual networks to an ExpressRoute circuit.</span></span> <span data-ttu-id="5dc01-125">Todas as redes virtuais devem estar na mesma região geopolítica.</span><span class="sxs-lookup"><span data-stu-id="5dc01-125">All virtual networks must be in the same geopolitical region.</span></span> <span data-ttu-id="5dc01-126">É possível vincular um grande número de redes virtuais ao circuito do ExpressRoute ou vincular redes virtuais que estejam em outras regiões geopolíticas se você tiver habilitado o complemento premium do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="5dc01-126">You can link a larger number of virtual networks to your ExpressRoute circuit, or link virtual networks that are in other geopolitical regions if you enabled the ExpressRoute premium add-on.</span></span> <span data-ttu-id="5dc01-127">Confira as [perguntas frequentes](expressroute-faqs.md) para obter mais detalhes sobre o complemento premium.</span><span class="sxs-lookup"><span data-stu-id="5dc01-127">Check the [FAQ](expressroute-faqs.md) for more details on the premium add-on.</span></span>

## <a name="connect-a-virtual-network-in-the-same-subscription-to-a-circuit"></a><span data-ttu-id="5dc01-128">Conectar uma rede virtual na mesma assinatura a um circuito</span><span class="sxs-lookup"><span data-stu-id="5dc01-128">Connect a virtual network in the same subscription to a circuit</span></span>
<span data-ttu-id="5dc01-129">Você pode vincular uma rede virtual a um circuito do ExpressRoute usando o cmdlet a seguir.</span><span class="sxs-lookup"><span data-stu-id="5dc01-129">You can link a virtual network to an ExpressRoute circuit by using the following cmdlet.</span></span> <span data-ttu-id="5dc01-130">Verifique se o gateway de rede virtual foi criado e se está pronto para vinculação antes de executar o cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5dc01-130">Make sure that the virtual network gateway is created and is ready for linking before you run the cmdlet.</span></span>

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"
    Provisioned

## <a name="connect-a-virtual-network-in-a-different-subscription-to-a-circuit"></a><span data-ttu-id="5dc01-131">Conectar uma rede virtual em uma assinatura diferente a um circuito</span><span class="sxs-lookup"><span data-stu-id="5dc01-131">Connect a virtual network in a different subscription to a circuit</span></span>
<span data-ttu-id="5dc01-132">Você pode compartilhar um circuito do ExpressRoute entre várias assinaturas.</span><span class="sxs-lookup"><span data-stu-id="5dc01-132">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="5dc01-133">A figura a seguir mostra um esquema simples de como funciona o compartilhamento de circuitos do ExpressRoute entre várias assinaturas.</span><span class="sxs-lookup"><span data-stu-id="5dc01-133">The following figure shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="5dc01-134">Cada uma das nuvens menores dentro da nuvem grande é usada para representar assinaturas pertencentes a diferentes departamentos dentro de uma organização.</span><span class="sxs-lookup"><span data-stu-id="5dc01-134">Each of the smaller clouds within the large cloud is used to represent subscriptions that belong to different departments within an organization.</span></span> <span data-ttu-id="5dc01-135">Cada um dos departamentos dentro da organização pode usar sua própria assinatura para implantar seus serviços, mas os departamentos podem compartilhar um único circuito do ExpressRoute para se conectar de volta à respectiva rede local.</span><span class="sxs-lookup"><span data-stu-id="5dc01-135">Each of the departments within the organization can use their own subscription for deploying their services--but the departments can share a single ExpressRoute circuit to connect back to your on-premises network.</span></span> <span data-ttu-id="5dc01-136">Um único departamento (neste exemplo: TI) pode ter o circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="5dc01-136">A single department (in this example: IT) can own the ExpressRoute circuit.</span></span> <span data-ttu-id="5dc01-137">Outras assinaturas dentro da organização podem usar o circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="5dc01-137">Other subscriptions within the organization can use the ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="5dc01-138">As cobranças por conectividade e largura de banda do circuito dedicado serão aplicadas ao proprietário do circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="5dc01-138">Connectivity and bandwidth charges for the dedicated circuit will be applied to the ExpressRoute circuit owner.</span></span> <span data-ttu-id="5dc01-139">Todas as redes virtuais compartilham a mesma largura de banda.</span><span class="sxs-lookup"><span data-stu-id="5dc01-139">All virtual networks share the same bandwidth.</span></span>
> 
> 

![Conectividade entre assinaturas](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration"></a><span data-ttu-id="5dc01-141">Administração</span><span class="sxs-lookup"><span data-stu-id="5dc01-141">Administration</span></span>
<span data-ttu-id="5dc01-142">O *proprietário do circuito* é o administrador/coadministrador da assinatura na qual o circuito do ExpressRoute foi criado.</span><span class="sxs-lookup"><span data-stu-id="5dc01-142">The *circuit owner* is the administrator/coadministrator of the subscription in which the ExpressRoute circuit is created.</span></span> <span data-ttu-id="5dc01-143">O proprietário do circuito pode autorizar administradores/coadministradores de outras assinaturas, conhecidos como *usuários do circuito*, a usar o circuito dedicado que eles possuem.</span><span class="sxs-lookup"><span data-stu-id="5dc01-143">The circuit owner can authorize administrators/coadministrators of other subscriptions, referred to as *circuit users*, to use the dedicated circuit that they own.</span></span> <span data-ttu-id="5dc01-144">Os usuários do circuito autorizados a usar o circuito do ExpressRoute da organização podem vincular a rede virtual em sua assinatura ao circuito do ExpressRoute depois que são autorizados.</span><span class="sxs-lookup"><span data-stu-id="5dc01-144">Circuit users who are authorized to use the organization's ExpressRoute circuit can link the virtual network in their subscription to the ExpressRoute circuit after they are authorized.</span></span>

<span data-ttu-id="5dc01-145">O proprietário do circuito tem a capacidade de modificar e revogar autorizações a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="5dc01-145">The circuit owner has the power to modify and revoke authorizations at any time.</span></span> <span data-ttu-id="5dc01-146">Revogar uma autorização fará com que todos os links sejam excluídos da assinatura cujo acesso foi revogado.</span><span class="sxs-lookup"><span data-stu-id="5dc01-146">Revoking an authorization will result in all links being deleted from the subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="5dc01-147">Operações do proprietário do circuito</span><span class="sxs-lookup"><span data-stu-id="5dc01-147">Circuit owner operations</span></span>

<span data-ttu-id="5dc01-148">**Criando uma autorização**</span><span class="sxs-lookup"><span data-stu-id="5dc01-148">**Creating an authorization**</span></span>

<span data-ttu-id="5dc01-149">O proprietário do circuito autoriza os administradores de outras assinaturas a usar o circuito especificado.</span><span class="sxs-lookup"><span data-stu-id="5dc01-149">The circuit owner authorizes the administrators of other subscriptions to use the specified circuit.</span></span> <span data-ttu-id="5dc01-150">No exemplo a seguir, o administrador do circuito (TI da Contoso) habilita o administrador de outra assinatura (Desenvolvimento/Teste) a vincular até duas redes virtuais ao circuito.</span><span class="sxs-lookup"><span data-stu-id="5dc01-150">In the following example, the administrator of the circuit (Contoso IT) enables the administrator of another subscription (Dev-Test) to link up to two virtual networks to the circuit.</span></span> <span data-ttu-id="5dc01-151">O administrador de TI da Contoso habilita isso especificando a ID da Microsoft de Desenvolvimento/Teste.</span><span class="sxs-lookup"><span data-stu-id="5dc01-151">The Contoso IT administrator enables this by specifying the Dev-Test Microsoft ID.</span></span> <span data-ttu-id="5dc01-152">O cmdlet não envia um email para a ID da Microsoft especificada.</span><span class="sxs-lookup"><span data-stu-id="5dc01-152">The cmdlet doesn't send email to the specified Microsoft ID.</span></span> <span data-ttu-id="5dc01-153">O proprietário do circuito precisa notificar explicitamente o outro proprietário da assinatura de que a autorização foi concluída.</span><span class="sxs-lookup"><span data-stu-id="5dc01-153">The circuit owner needs to explicitly notify the other subscription owner that the authorization is complete.</span></span>

    New-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -Description "Dev-Test Links" -Limit 2 -MicrosoftIds 'devtest@contoso.com'

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : **********************************
    MicrosoftIds        : devtest@contoso.com
    Used                : 0

<span data-ttu-id="5dc01-154">**Examinando autorizações**</span><span class="sxs-lookup"><span data-stu-id="5dc01-154">**Reviewing authorizations**</span></span>

<span data-ttu-id="5dc01-155">O proprietário do circuito pode examinar todas as autorizações emitidas em um circuito específico executando o seguinte cmdlet:</span><span class="sxs-lookup"><span data-stu-id="5dc01-155">The circuit owner can review all authorizations that are issued on a particular circuit by running the following cmdlet:</span></span>

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


<span data-ttu-id="5dc01-156">**Atualizando autorizações**</span><span class="sxs-lookup"><span data-stu-id="5dc01-156">**Updating authorizations**</span></span>

<span data-ttu-id="5dc01-157">O proprietário do circuito pode modificar autorizações usando o seguinte cmdlet:</span><span class="sxs-lookup"><span data-stu-id="5dc01-157">The circuit owner can modify authorizations by using the following cmdlet:</span></span>

    Set-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -AuthorizationId "&&&&&&&&&&&&&&&&&&&&&&&&&&&&"-Limit 5

    Description         : Dev-Test Links
    Limit               : 5
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : devtest@contoso.com
    Used                : 0


<span data-ttu-id="5dc01-158">**Excluindo autorizações**</span><span class="sxs-lookup"><span data-stu-id="5dc01-158">**Deleting authorizations**</span></span>

<span data-ttu-id="5dc01-159">O proprietário do circuito pode revogar/excluir autorizações usando o seguinte cmdlet:</span><span class="sxs-lookup"><span data-stu-id="5dc01-159">The circuit owner can revoke/delete authorizations to the user by running the following cmdlet:</span></span>

    Remove-AzureDedicatedCircuitLinkAuthorization -ServiceKey "*****************************" -AuthorizationId "###############################"


### <a name="circuit-user-operations"></a><span data-ttu-id="5dc01-160">Operações do usuário do circuito</span><span class="sxs-lookup"><span data-stu-id="5dc01-160">Circuit user operations</span></span>

<span data-ttu-id="5dc01-161">**Examinando autorizações**</span><span class="sxs-lookup"><span data-stu-id="5dc01-161">**Reviewing authorizations**</span></span>

<span data-ttu-id="5dc01-162">O usuário do circuito pode examinar autorizações usando o seguinte cmdlet:</span><span class="sxs-lookup"><span data-stu-id="5dc01-162">The circuit user can review authorizations by using the following cmdlet:</span></span>

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

<span data-ttu-id="5dc01-163">**Resgatando autorizações de link**</span><span class="sxs-lookup"><span data-stu-id="5dc01-163">**Redeeming link authorizations**</span></span>

<span data-ttu-id="5dc01-164">O usuário de circuito pode executar o seguinte cmdlet para resgatar uma autorização de vínculo:</span><span class="sxs-lookup"><span data-stu-id="5dc01-164">The circuit user can run the following cmdlet to redeem a link authorization:</span></span>

    New-AzureDedicatedCircuitLink –servicekey "&&&&&&&&&&&&&&&&&&&&&&&&&&" –VnetName 'SalesVNET1'

    State VnetName
    ----- --------
    Provisioned SalesVNET1

<span data-ttu-id="5dc01-165">Execute este comando na assinatura recentemente vinculada para a rede virtual:</span><span class="sxs-lookup"><span data-stu-id="5dc01-165">Run this command in the newly linked subscription for the virtual network:</span></span>

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"

## <a name="next-steps"></a><span data-ttu-id="5dc01-166">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5dc01-166">Next steps</span></span>
<span data-ttu-id="5dc01-167">Para obter mais informações sobre o ExpressRoute, consulte [Perguntas Frequentes sobre ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="5dc01-167">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

