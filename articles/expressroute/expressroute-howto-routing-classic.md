---
title: "Como configurar o roteamento (emparelhamento) para um circuito do ExpressRoute: Azure: clássico | Microsoft Docs"
description: "Este artigo fornece uma orientação sobre as etapas de criação e de provisionamento do emparelhamento público, privado e da Microsoft de um circuito de ExpressRoute. Este artigo também mostra como verificar o status, atualizar ou excluir emparelhamentos de seu circuito."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: a4bd39d2-373a-467a-8b06-36cfcc1027d2
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 37713db70f3ae837edafc997b78b16b121d0a885
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-classic"></a><span data-ttu-id="aec05-104">Criar e modificar o emparelhamento de um circuito de ExpressRoute (clássico)</span><span class="sxs-lookup"><span data-stu-id="aec05-104">Create and modify peering for an ExpressRoute circuit (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="aec05-105">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="aec05-105">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="aec05-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="aec05-106">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="aec05-107">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="aec05-107">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="aec05-108">Vídeo – Emparelhamento privado</span><span class="sxs-lookup"><span data-stu-id="aec05-108">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="aec05-109">Vídeo – Emparelhamento público</span><span class="sxs-lookup"><span data-stu-id="aec05-109">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="aec05-110">Vídeo – Emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="aec05-110">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="aec05-111">PowerShell (clássico)</span><span class="sxs-lookup"><span data-stu-id="aec05-111">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

<span data-ttu-id="aec05-112">Este artigo fornece uma orientação pelas etapas de criação e de gerenciamento da configuração de roteamento de um circuito do ExpressRoute usando o PowerShell e o modelo de implantação clássico.</span><span class="sxs-lookup"><span data-stu-id="aec05-112">This article walks you through the steps to create and manage routing configuration for an ExpressRoute circuit using PowerShell and the classic deployment model.</span></span> <span data-ttu-id="aec05-113">As etapas a seguir também mostrarão a você como verificar o status, atualizar ou excluir e desprovisionar emparelhamentos de um circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="aec05-113">The steps below will also show you how to check the status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="aec05-114">**Sobre modelos de implantação do Azure**</span><span class="sxs-lookup"><span data-stu-id="aec05-114">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]


## <a name="configuration-prerequisites"></a><span data-ttu-id="aec05-115">Pré-requisitos de configuração</span><span class="sxs-lookup"><span data-stu-id="aec05-115">Configuration prerequisites</span></span>
* <span data-ttu-id="aec05-116">Você precisará da versão mais recente dos cmdlets do PowerShell do SM (Gerenciamento de Serviços) do Azure.</span><span class="sxs-lookup"><span data-stu-id="aec05-116">You will need the latest version of the Azure Service Management (SM) PowerShell cmdlets.</span></span> <span data-ttu-id="aec05-117">Para saber mais, confira [Getting started with Azure PowerShell cmdlets](/powershell/azure/overview) (Introdução aos cmdlets do Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="aec05-117">For more information, see [Getting started with Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>  
* <span data-ttu-id="aec05-118">Verifique se você leu a página de [pré-requisitos](expressroute-prerequisites.md), a página de [requisitos do roteamento](expressroute-routing.md) e a página [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração.</span><span class="sxs-lookup"><span data-stu-id="aec05-118">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md) page, the [routing requirements](expressroute-routing.md) page, and the [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="aec05-119">Você deve ter um circuito do ExpressRoute ativo.</span><span class="sxs-lookup"><span data-stu-id="aec05-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="aec05-120">Antes de continuar, siga as instruções para [criar um circuito do ExpressRoute](expressroute-howto-circuit-classic.md) e para que o circuito seja habilitado pelo provedor de conectividade.</span><span class="sxs-lookup"><span data-stu-id="aec05-120">Follow the instructions to [create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="aec05-121">O circuito do ExpressRoute deve estar em um estado provisionado e habilitado e para que você possa executar os cmdlets descritos abaixo.</span><span class="sxs-lookup"><span data-stu-id="aec05-121">The ExpressRoute circuit must be in a provisioned and enabled state for you to be able to run the cmdlets described below.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aec05-122">Estas instruções se aplicam apenas a circuitos criados com provedores de serviço que oferecem serviços de conectividade de Camada 2.</span><span class="sxs-lookup"><span data-stu-id="aec05-122">These instructions only apply to circuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="aec05-123">Se você estiver usando um provedor de serviços que oferece serviços gerenciados de Camada 3 (normalmente um IPVPN, como MPLS), seu provedor de conectividade configurará e gerenciará o roteamento para você.</span><span class="sxs-lookup"><span data-stu-id="aec05-123">If you are using a service provider offering managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

<span data-ttu-id="aec05-124">Você pode configurar um, dois ou todos os três emparelhamentos (privado e público do Azure e da Microsoft) para um circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="aec05-124">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="aec05-125">Você pode configurar emparelhamentos em qualquer ordem escolhida.</span><span class="sxs-lookup"><span data-stu-id="aec05-125">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="aec05-126">No entanto, você deve concluir a configuração de um emparelhamento por vez.</span><span class="sxs-lookup"><span data-stu-id="aec05-126">However, you must make sure that you complete the configuration of each peering one at a time.</span></span>


### <a name="log-in-to-your-azure-account-and-select-a-subscription"></a><span data-ttu-id="aec05-127">Entre em sua conta do Azure e selecione uma assinatura</span><span class="sxs-lookup"><span data-stu-id="aec05-127">Log in to your Azure account and select a subscription</span></span>
1. <span data-ttu-id="aec05-128">Abra o console do PowerShell com direitos elevados e conecte-se à sua conta.</span><span class="sxs-lookup"><span data-stu-id="aec05-128">Open your PowerShell console with elevated rights and connect to your account.</span></span> <span data-ttu-id="aec05-129">Use o exemplo a seguir para ajudar a se conectar:</span><span class="sxs-lookup"><span data-stu-id="aec05-129">Use the following example to help you connect:</span></span>

        Login-AzureRmAccount

2. <span data-ttu-id="aec05-130">Verificar as assinaturas da conta.</span><span class="sxs-lookup"><span data-stu-id="aec05-130">Check the subscriptions for the account.</span></span>

        Get-AzureRmSubscription

3. <span data-ttu-id="aec05-131">Se você tiver mais de uma assinatura, selecione a assinatura que deseja usar.</span><span class="sxs-lookup"><span data-stu-id="aec05-131">If you have more than one subscription, select the subscription that you want to use.</span></span>

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. <span data-ttu-id="aec05-132">Use o cmdlet a seguir para adicionar sua assinatura do Azure ao PowerShell para o modelo de implantação clássico.</span><span class="sxs-lookup"><span data-stu-id="aec05-132">Next, use the following cmdlet to add your Azure subscription to PowerShell for the classic deployment model.</span></span>

        Add-AzureAccount


## <a name="azure-private-peering"></a><span data-ttu-id="aec05-133">Emparelhamento privado do Azure</span><span class="sxs-lookup"><span data-stu-id="aec05-133">Azure private peering</span></span>
<span data-ttu-id="aec05-134">Esta seção fornece instruções sobre como criar, obter, atualizar e excluir a configuração de emparelhamento privado do Azure para um circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="aec05-134">This section provides instructions on how to create, get, update, and delete the Azure private peering configuration for an ExpressRoute circuit.</span></span> 

### <a name="to-create-azure-private-peering"></a><span data-ttu-id="aec05-135">Criar um emparelhamento privado do Azure</span><span class="sxs-lookup"><span data-stu-id="aec05-135">To create Azure private peering</span></span>
1. <span data-ttu-id="aec05-136">**Importe o módulo do PowerShell para o ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="aec05-136">**Import the PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="aec05-137">Para começar a usar os cmdlets do ExpressRoute, é necessário importar os módulos do Azure e do ExpressRoute para a sessão do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="aec05-137">You must import the Azure and ExpressRoute modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="aec05-138">Execute os seguintes comandos para importar os módulos do Azure e do ExpressRoute para a sessão do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="aec05-138">Run the following commands to import the Azure and ExpressRoute modules into the PowerShell session.</span></span>  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="aec05-139">**Criar um circuito do ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="aec05-139">**Create an ExpressRoute circuit.**</span></span>
   
    <span data-ttu-id="aec05-140">Siga as instruções para criar um [circuito do ExpressRoute](expressroute-howto-circuit-classic.md) e para que o circuito seja provisionado pelo provedor de conectividade.</span><span class="sxs-lookup"><span data-stu-id="aec05-140">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by the connectivity provider.</span></span> <span data-ttu-id="aec05-141">Caso seu provedor de conectividade ofereça serviços gerenciados de camada 3, solicite a ele a habilitação do emparelhamento privado do Azure.</span><span class="sxs-lookup"><span data-stu-id="aec05-141">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="aec05-142">Nesse caso, não será necessário seguir as instruções listadas nas seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="aec05-142">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="aec05-143">No entanto, se o seu provedor de conectividade não gerenciar o roteamento, após a criação do circuito, siga as instruções abaixo.</span><span class="sxs-lookup"><span data-stu-id="aec05-143">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow the instructions below.</span></span> 
3. <span data-ttu-id="aec05-144">**Verifique se o circuito do ExpressRoute foi provisionado.**</span><span class="sxs-lookup"><span data-stu-id="aec05-144">**Check the ExpressRoute circuit to ensure it is provisioned.**</span></span>
   
    <span data-ttu-id="aec05-145">Primeiro, verifique se o circuito do ExpressRoute está Provisionado e Habilitado.</span><span class="sxs-lookup"><span data-stu-id="aec05-145">You must first check to see if the ExpressRoute circuit is Provisioned and also Enabled.</span></span> <span data-ttu-id="aec05-146">Veja o exemplo abaixo.</span><span class="sxs-lookup"><span data-stu-id="aec05-146">See the example below.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="aec05-147">Verifique se o circuito aparece como Provisionado e Habilitado.</span><span class="sxs-lookup"><span data-stu-id="aec05-147">Make sure that the circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="aec05-148">Caso contrário, converse com seu provedor de conectividade para que o circuito fique com o status e o estado exigidos.</span><span class="sxs-lookup"><span data-stu-id="aec05-148">If it doesn't, work with your connectivity provider to get your circuit to the required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="aec05-149">**Configure o emparelhamento privado do Azure para o circuito.**</span><span class="sxs-lookup"><span data-stu-id="aec05-149">**Configure Azure private peering for the circuit.**</span></span>
   
    <span data-ttu-id="aec05-150">Verifique se você tem os seguintes itens antes de continuar com as próximas etapas:</span><span class="sxs-lookup"><span data-stu-id="aec05-150">Make sure that you have the following items before you proceed with the next steps:</span></span>
   
   * <span data-ttu-id="aec05-151">Uma sub-rede /30 para o link principal.</span><span class="sxs-lookup"><span data-stu-id="aec05-151">A /30 subnet for the primary link.</span></span> <span data-ttu-id="aec05-152">Ela não deve fazer parte de qualquer espaço de endereçamento reservado para redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="aec05-152">This must not be part of any address space reserved for virtual networks.</span></span>
   * <span data-ttu-id="aec05-153">Uma sub-rede /30 para o link secundário.</span><span class="sxs-lookup"><span data-stu-id="aec05-153">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="aec05-154">Ela não deve fazer parte de qualquer espaço de endereçamento reservado para redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="aec05-154">This must not be part of any address space reserved for virtual networks.</span></span>
   * <span data-ttu-id="aec05-155">Uma ID válida de VLAN para estabelecer esse emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="aec05-155">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="aec05-156">Verifique se nenhum outro emparelhamento no circuito usa a mesma ID de VLAN.</span><span class="sxs-lookup"><span data-stu-id="aec05-156">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
   * <span data-ttu-id="aec05-157">Número de AS para emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="aec05-157">AS number for peering.</span></span> <span data-ttu-id="aec05-158">Você pode usar um número de AS de 2 e de 4 bytes.</span><span class="sxs-lookup"><span data-stu-id="aec05-158">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="aec05-159">Você pode usar um número de AS privado para esse emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="aec05-159">You can use a private AS number for this peering.</span></span> <span data-ttu-id="aec05-160">Não use 65515.</span><span class="sxs-lookup"><span data-stu-id="aec05-160">Ensure that you are not using 65515.</span></span>
   * <span data-ttu-id="aec05-161">Um Hash MD5, se você optar por usar um.</span><span class="sxs-lookup"><span data-stu-id="aec05-161">An MD5 hash if you choose to use one.</span></span> <span data-ttu-id="aec05-162">**Isso é opcional**.</span><span class="sxs-lookup"><span data-stu-id="aec05-162">**This is optional**.</span></span>
     
    <span data-ttu-id="aec05-163">Você pode executar o seguinte cmdlet para configurar o emparelhamento privado do Azure para seu circuito.</span><span class="sxs-lookup"><span data-stu-id="aec05-163">You can run the following cmdlet to configure Azure private peering for your circuit.</span></span>
     
        <span data-ttu-id="aec05-164">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100</span><span class="sxs-lookup"><span data-stu-id="aec05-164">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100</span></span>
     
    <span data-ttu-id="aec05-165">Use o cmdlet abaixo se você optar por usar um hash MD5.</span><span class="sxs-lookup"><span data-stu-id="aec05-165">You can use the cmdlet below if you choose to use an MD5 hash.</span></span>
     
        <span data-ttu-id="aec05-166">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100 -SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="aec05-166">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100 -SharedKey "A1B2C3D4"</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="aec05-167">Especifique o número de AS como um ASN de emparelhamento, não um ASN de cliente.</span><span class="sxs-lookup"><span data-stu-id="aec05-167">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
     > 
     > 

### <a name="to-view-azure-private-peering-details"></a><span data-ttu-id="aec05-168">Para exibir detalhes sobre o emparelhamento privado do Azure</span><span class="sxs-lookup"><span data-stu-id="aec05-168">To view Azure private peering details</span></span>
<span data-ttu-id="aec05-169">Você pode obter detalhes de configuração usando o seguinte cmdlet</span><span class="sxs-lookup"><span data-stu-id="aec05-169">You can get configuration details using the following cmdlet</span></span>

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 100


### <a name="to-update-azure-private-peering-configuration"></a><span data-ttu-id="aec05-170">Atualizar a configuração de emparelhamento privado do Azure</span><span class="sxs-lookup"><span data-stu-id="aec05-170">To update Azure private peering configuration</span></span>
<span data-ttu-id="aec05-171">Você pode atualizar qualquer parte da configuração usando o cmdlet a seguir.</span><span class="sxs-lookup"><span data-stu-id="aec05-171">You can update any part of the configuration using the following cmdlet.</span></span> <span data-ttu-id="aec05-172">No exemplo abaixo, a ID de VLAN do circuito está sendo atualizada de 100 para 500.</span><span class="sxs-lookup"><span data-stu-id="aec05-172">In the example below, the VLAN ID of the circuit is being updated from 100 to 500.</span></span>

    Set-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 500 -SharedKey "A1B2C3D4"

### <a name="to-delete-azure-private-peering"></a><span data-ttu-id="aec05-173">Excluir um emparelhamento privado do Azure</span><span class="sxs-lookup"><span data-stu-id="aec05-173">To delete Azure private peering</span></span>
<span data-ttu-id="aec05-174">Você pode remover a configuração de emparelhamento executando o seguinte cmdlet.</span><span class="sxs-lookup"><span data-stu-id="aec05-174">You can remove your peering configuration by running the following cmdlet.</span></span>

> [!WARNING]
> <span data-ttu-id="aec05-175">Verifique se todas as redes virtuais estão desvinculadas do circuito do ExpressRoute antes de executar esse cmdlet.</span><span class="sxs-lookup"><span data-stu-id="aec05-175">You must ensure that all virtual networks are unlinked from the ExpressRoute circuit before running this cmdlet.</span></span> 
> 
> 

    Remove-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"


## <a name="azure-public-peering"></a><span data-ttu-id="aec05-176">Emparelhamento público do Azure</span><span class="sxs-lookup"><span data-stu-id="aec05-176">Azure public peering</span></span>
<span data-ttu-id="aec05-177">Esta seção fornece instruções sobre como criar, obter, atualizar e excluir a configuração de emparelhamento público do Azure para um circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="aec05-177">This section provides instructions on how to create, get, update and delete the Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-public-peering"></a><span data-ttu-id="aec05-178">Criar o emparelhamento público do Azure</span><span class="sxs-lookup"><span data-stu-id="aec05-178">To create Azure public peering</span></span>
1. <span data-ttu-id="aec05-179">**Importe o módulo do PowerShell para o ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="aec05-179">**Import the PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="aec05-180">Para começar a usar os cmdlets do ExpressRoute, é necessário importar os módulos do Azure e do ExpressRoute para a sessão do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="aec05-180">You must import the Azure and ExpressRoute modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="aec05-181">Execute os seguintes comandos para importar os módulos do Azure e do ExpressRoute para a sessão do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="aec05-181">Run the following commands to import the Azure and ExpressRoute modules into the PowerShell session.</span></span> 
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="aec05-182">**Criar um circuito do ExpressRoute**</span><span class="sxs-lookup"><span data-stu-id="aec05-182">**Create an ExpressRoute circuit**</span></span>
   
    <span data-ttu-id="aec05-183">Siga as instruções para criar um [circuito do ExpressRoute](expressroute-howto-circuit-classic.md) e para que o circuito seja provisionado pelo provedor de conectividade.</span><span class="sxs-lookup"><span data-stu-id="aec05-183">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by the connectivity provider.</span></span> <span data-ttu-id="aec05-184">Caso seu provedor de conectividade ofereça serviços gerenciados de camada 3, solicite a ele a habilitação do emparelhamento público do Azure.</span><span class="sxs-lookup"><span data-stu-id="aec05-184">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure public peering for you.</span></span> <span data-ttu-id="aec05-185">Nesse caso, não será necessário seguir as instruções listadas nas seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="aec05-185">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="aec05-186">No entanto, se o seu provedor de conectividade não gerenciar o roteamento, após a criação do circuito, siga as instruções abaixo.</span><span class="sxs-lookup"><span data-stu-id="aec05-186">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow the instructions below.</span></span>
3. <span data-ttu-id="aec05-187">**Verifique se o circuito do ExpressRoute foi provisionado**</span><span class="sxs-lookup"><span data-stu-id="aec05-187">**Check ExpressRoute circuit to ensure it is provisioned**</span></span>
   
    <span data-ttu-id="aec05-188">Primeiro, verifique se o circuito do ExpressRoute está Provisionado e Habilitado.</span><span class="sxs-lookup"><span data-stu-id="aec05-188">You must first check to see if the ExpressRoute circuit is Provisioned and also Enabled.</span></span> <span data-ttu-id="aec05-189">Veja o exemplo abaixo.</span><span class="sxs-lookup"><span data-stu-id="aec05-189">See the example below.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="aec05-190">Verifique se o circuito aparece como Provisionado e Habilitado.</span><span class="sxs-lookup"><span data-stu-id="aec05-190">Make sure that the circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="aec05-191">Caso contrário, converse com seu provedor de conectividade para que o circuito fique com o status e o estado exigidos.</span><span class="sxs-lookup"><span data-stu-id="aec05-191">If it doesn't, work with your connectivity provider to get your circuit to the required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="aec05-192">**Configure o emparelhamento público do Azure para o circuito**</span><span class="sxs-lookup"><span data-stu-id="aec05-192">**Configure Azure public peering for the circuit**</span></span>
   
    <span data-ttu-id="aec05-193">Tenha as informações a seguir antes de prosseguir:</span><span class="sxs-lookup"><span data-stu-id="aec05-193">Ensure that you have the following information before you proceed further.</span></span>
   
   * <span data-ttu-id="aec05-194">Uma sub-rede /30 para o link principal.</span><span class="sxs-lookup"><span data-stu-id="aec05-194">A /30 subnet for the primary link.</span></span> <span data-ttu-id="aec05-195">Precisa ser um prefixo IPv4 público válido.</span><span class="sxs-lookup"><span data-stu-id="aec05-195">This must be a valid public IPv4 prefix.</span></span>
   * <span data-ttu-id="aec05-196">Uma sub-rede /30 para o link secundário.</span><span class="sxs-lookup"><span data-stu-id="aec05-196">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="aec05-197">Precisa ser um prefixo IPv4 público válido.</span><span class="sxs-lookup"><span data-stu-id="aec05-197">This must be a valid public IPv4 prefix.</span></span>
   * <span data-ttu-id="aec05-198">Uma ID válida de VLAN para estabelecer esse emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="aec05-198">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="aec05-199">Verifique se nenhum outro emparelhamento no circuito usa a mesma ID de VLAN.</span><span class="sxs-lookup"><span data-stu-id="aec05-199">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
   * <span data-ttu-id="aec05-200">Número de AS para emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="aec05-200">AS number for peering.</span></span> <span data-ttu-id="aec05-201">Você pode usar um número de AS de 2 e de 4 bytes.</span><span class="sxs-lookup"><span data-stu-id="aec05-201">You can use both 2-byte and 4-byte AS numbers.</span></span>
   * <span data-ttu-id="aec05-202">Um Hash MD5, se você optar por usar um.</span><span class="sxs-lookup"><span data-stu-id="aec05-202">An MD5 hash if you choose to use one.</span></span> <span data-ttu-id="aec05-203">**Isso é opcional**.</span><span class="sxs-lookup"><span data-stu-id="aec05-203">**This is optional**.</span></span>
     
    <span data-ttu-id="aec05-204">Você pode executar o cmdlet a seguir a fim de configurar o emparelhamento público do Azure para seu circuito.</span><span class="sxs-lookup"><span data-stu-id="aec05-204">You can run the following cmdlet to configure Azure public peering for your circuit</span></span>
     
        <span data-ttu-id="aec05-205">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200</span><span class="sxs-lookup"><span data-stu-id="aec05-205">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200</span></span>
     
    <span data-ttu-id="aec05-206">Use o cmdlet abaixo se você optar por usar um hash MD5</span><span class="sxs-lookup"><span data-stu-id="aec05-206">You can use the cmdlet below if you choose to use an MD5 hash</span></span>
     
        <span data-ttu-id="aec05-207">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200 -SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="aec05-207">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200 -SharedKey "A1B2C3D4"</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="aec05-208">Especifique o número de AS como um ASN de emparelhamento e não um ASN de cliente.</span><span class="sxs-lookup"><span data-stu-id="aec05-208">Ensure that you specify your AS number as peering ASN and not customer ASN.</span></span>
     > 
     > 

### <a name="to-view-azure-public-peering-details"></a><span data-ttu-id="aec05-209">Para exibir detalhes sobre o emparelhamento público do Azure</span><span class="sxs-lookup"><span data-stu-id="aec05-209">To view Azure public peering details</span></span>
<span data-ttu-id="aec05-210">Você pode obter detalhes de configuração usando o seguinte cmdlet</span><span class="sxs-lookup"><span data-stu-id="aec05-210">You can get configuration details using the following cmdlet</span></span>

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 131.107.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 131.107.0.4/30
    State                          : Enabled
    VlanId                         : 200


### <a name="to-update-azure-public-peering-configuration"></a><span data-ttu-id="aec05-211">Atualizar a configuração de emparelhamento público do Azure</span><span class="sxs-lookup"><span data-stu-id="aec05-211">To update Azure public peering configuration</span></span>
<span data-ttu-id="aec05-212">Você pode atualizar qualquer parte da configuração usando o cmdlet a seguir</span><span class="sxs-lookup"><span data-stu-id="aec05-212">You can update any part of the configuration using the following cmdlet</span></span>

    Set-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 600 -SharedKey "A1B2C3D4"

<span data-ttu-id="aec05-213">No exemplo acima, a ID de VLAN do circuito está sendo atualizada de 200 para 600.</span><span class="sxs-lookup"><span data-stu-id="aec05-213">The VLAN ID of the circuit is being updated from 200 to 600 in the above example.</span></span>

### <a name="to-delete-azure-public-peering"></a><span data-ttu-id="aec05-214">Excluir o emparelhamento público do Azure</span><span class="sxs-lookup"><span data-stu-id="aec05-214">To delete Azure public peering</span></span>
<span data-ttu-id="aec05-215">Você pode remover a configuração de emparelhamento executando o seguinte cmdlet</span><span class="sxs-lookup"><span data-stu-id="aec05-215">You can remove your peering configuration by running the following cmdlet</span></span>

    Remove-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

## <a name="microsoft-peering"></a><span data-ttu-id="aec05-216">Emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="aec05-216">Microsoft peering</span></span>
<span data-ttu-id="aec05-217">Esta seção fornece instruções sobre como criar, obter, atualizar e excluir a configuração de emparelhamento da Microsoft para um circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="aec05-217">This section provides instructions on how to create, get, update and delete the Microsoft peering configuration for an ExpressRoute circuit.</span></span> 

### <a name="to-create-microsoft-peering"></a><span data-ttu-id="aec05-218">Criar emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="aec05-218">To create Microsoft peering</span></span>
1. <span data-ttu-id="aec05-219">**Importe o módulo do PowerShell para o ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="aec05-219">**Import the PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="aec05-220">Para começar a usar os cmdlets do ExpressRoute, é necessário importar os módulos do Azure e do ExpressRoute para a sessão do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="aec05-220">You must import the Azure and ExpressRoute modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="aec05-221">Execute os seguintes comandos para importar os módulos do Azure e do ExpressRoute para a sessão do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="aec05-221">Run the following commands to import the Azure and ExpressRoute modules into the PowerShell session.</span></span>  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="aec05-222">**Criar um circuito do ExpressRoute**</span><span class="sxs-lookup"><span data-stu-id="aec05-222">**Create an ExpressRoute circuit**</span></span>
   
    <span data-ttu-id="aec05-223">Siga as instruções para criar um [circuito do ExpressRoute](expressroute-howto-circuit-classic.md) e para que o circuito seja provisionado pelo provedor de conectividade.</span><span class="sxs-lookup"><span data-stu-id="aec05-223">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by the connectivity provider.</span></span> <span data-ttu-id="aec05-224">Caso seu provedor de conectividade ofereça serviços gerenciados de camada 3, solicite a ele a habilitação do emparelhamento privado do Azure.</span><span class="sxs-lookup"><span data-stu-id="aec05-224">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="aec05-225">Nesse caso, não será necessário seguir as instruções listadas nas seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="aec05-225">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="aec05-226">No entanto, se o seu provedor de conectividade não gerenciar o roteamento, após a criação do circuito, siga as instruções abaixo.</span><span class="sxs-lookup"><span data-stu-id="aec05-226">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow the instructions below.</span></span>
3. <span data-ttu-id="aec05-227">**Verifique se o circuito do ExpressRoute foi provisionado**</span><span class="sxs-lookup"><span data-stu-id="aec05-227">**Check ExpressRoute circuit to ensure it is provisioned**</span></span>
   
    <span data-ttu-id="aec05-228">Primeiro, verifique se o circuito do ExpressRoute está no estado Provisionado e Habilitado.</span><span class="sxs-lookup"><span data-stu-id="aec05-228">You must first check to see if the ExpressRoute circuit is in Provisioned and Enabled state.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="aec05-229">Verifique se o circuito aparece como Provisionado e Habilitado.</span><span class="sxs-lookup"><span data-stu-id="aec05-229">Make sure that the circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="aec05-230">Caso contrário, converse com seu provedor de conectividade para que o circuito fique com o status e o estado exigidos.</span><span class="sxs-lookup"><span data-stu-id="aec05-230">If it doesn't, work with your connectivity provider to get your circuit to the required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="aec05-231">**Configurar o emparelhamento da Microsoft para o circuito**</span><span class="sxs-lookup"><span data-stu-id="aec05-231">**Configure Microsoft peering for the circuit**</span></span>
   
    <span data-ttu-id="aec05-232">Você precisa ter as seguintes informações antes de continuar:</span><span class="sxs-lookup"><span data-stu-id="aec05-232">Make sure that you have the following information before you proceed.</span></span>
   
   * <span data-ttu-id="aec05-233">Uma sub-rede /30 para o link principal.</span><span class="sxs-lookup"><span data-stu-id="aec05-233">A /30 subnet for the primary link.</span></span> <span data-ttu-id="aec05-234">Este valor deve ser um prefixo IPv4 público válido próprio e registrado em um RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="aec05-234">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
   * <span data-ttu-id="aec05-235">Uma sub-rede /30 para o link secundário.</span><span class="sxs-lookup"><span data-stu-id="aec05-235">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="aec05-236">Este valor deve ser um prefixo IPv4 público válido próprio e registrado em um RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="aec05-236">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
   * <span data-ttu-id="aec05-237">Uma ID válida de VLAN para estabelecer esse emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="aec05-237">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="aec05-238">Verifique se nenhum outro emparelhamento no circuito usa a mesma ID de VLAN.</span><span class="sxs-lookup"><span data-stu-id="aec05-238">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
   * <span data-ttu-id="aec05-239">Número de AS para emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="aec05-239">AS number for peering.</span></span> <span data-ttu-id="aec05-240">Você pode usar um número de AS de 2 e de 4 bytes.</span><span class="sxs-lookup"><span data-stu-id="aec05-240">You can use both 2-byte and 4-byte AS numbers.</span></span>
   * <span data-ttu-id="aec05-241">Prefixos anunciados: forneça uma lista com todos os prefixos que você pretende anunciar na sessão BGP.</span><span class="sxs-lookup"><span data-stu-id="aec05-241">Advertised prefixes: You must provide a list of all prefixes you plan to advertise over the BGP session.</span></span> <span data-ttu-id="aec05-242">Somente prefixos de endereços IP públicos são aceitos.</span><span class="sxs-lookup"><span data-stu-id="aec05-242">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="aec05-243">Caso você planeje enviar um conjunto de prefixos, envie uma lista separada por vírgulas.</span><span class="sxs-lookup"><span data-stu-id="aec05-243">You can send a comma separated list if you plan to send a set of prefixes.</span></span> <span data-ttu-id="aec05-244">Esses prefixos devem ser registrados em seu nome em um RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="aec05-244">These prefixes must be registered to you in an RIR / IRR.</span></span>
   * <span data-ttu-id="aec05-245">ASN de cliente: se você estiver anunciando prefixos não registrados com o número AS de emparelhamento, especifique o número AS com o qual eles estão registrados.</span><span class="sxs-lookup"><span data-stu-id="aec05-245">Customer ASN: If you are advertising prefixes that are not registered to the peering AS number, you can specify the AS number to which they are registered.</span></span> <span data-ttu-id="aec05-246">**Isso é opcional**.</span><span class="sxs-lookup"><span data-stu-id="aec05-246">**This is optional**.</span></span>
   * <span data-ttu-id="aec05-247">Nome do registro de roteamento: você pode especificar o RIR/IRR com base no qual o número de AS e os prefixos estão registrados.</span><span class="sxs-lookup"><span data-stu-id="aec05-247">Routing Registry Name: You can specify the RIR / IRR against which the AS number and prefixes are registered.</span></span>
   * <span data-ttu-id="aec05-248">Um hash MD5, se você optar por usar um.</span><span class="sxs-lookup"><span data-stu-id="aec05-248">An MD5 hash, if you choose to use one.</span></span> <span data-ttu-id="aec05-249">**Isso é opcional.**</span><span class="sxs-lookup"><span data-stu-id="aec05-249">**This is optional.**</span></span>
     
    <span data-ttu-id="aec05-250">Execute o cmdlet a seguir para configurar o emparelhamento da Microsoft para seu circuito</span><span class="sxs-lookup"><span data-stu-id="aec05-250">You can run the following cmdlet to configure Microsoft pering for your circuit</span></span>
     
        <span data-ttu-id="aec05-251">New-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="aec05-251">New-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"</span></span>

### <a name="to-view-microsoft-peering-details"></a><span data-ttu-id="aec05-252">Para exibir detalhes de emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="aec05-252">To view Microsoft peering details</span></span>
<span data-ttu-id="aec05-253">Você pode obter detalhes de configuração usando o cmdlet a seguir.</span><span class="sxs-lookup"><span data-stu-id="aec05-253">You can get configuration details using the following cmdlet.</span></span>

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 123.0.0.0/30
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 2245
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : ARIN
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 300


### <a name="to-update-microsoft-peering-configuration"></a><span data-ttu-id="aec05-254">Atualizar a configuração de emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="aec05-254">To update Microsoft peering configuration</span></span>
<span data-ttu-id="aec05-255">Você pode atualizar qualquer parte da configuração usando o cmdlet a seguir.</span><span class="sxs-lookup"><span data-stu-id="aec05-255">You can update any part of the configuration using the following cmdlet.</span></span>

    Set-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"

### <a name="to-delete-microsoft-peering"></a><span data-ttu-id="aec05-256">Excluir emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="aec05-256">To delete Microsoft peering</span></span>
<span data-ttu-id="aec05-257">Você pode remover a configuração de emparelhamento executando o seguinte cmdlet.</span><span class="sxs-lookup"><span data-stu-id="aec05-257">You can remove your peering configuration by running the following cmdlet.</span></span>

    Remove-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

## <a name="next-steps"></a><span data-ttu-id="aec05-258">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="aec05-258">Next steps</span></span>
<span data-ttu-id="aec05-259">Em seguida, [Vincular uma Rede Virtual a um circuito do ExpressRoute](expressroute-howto-linkvnet-classic.md).</span><span class="sxs-lookup"><span data-stu-id="aec05-259">Next, [Link a VNet to an ExpressRoute circuit](expressroute-howto-linkvnet-classic.md).</span></span>

* <span data-ttu-id="aec05-260">Para obter mais informações sobre fluxos de trabalho, veja [Fluxos de trabalho do ExpressRoute](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="aec05-260">For more information about workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="aec05-261">Para obter mais informações sobre o emparelhamento de circuito, veja [Circuitos e domínios de roteamento do ExpressRoute](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="aec05-261">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>

