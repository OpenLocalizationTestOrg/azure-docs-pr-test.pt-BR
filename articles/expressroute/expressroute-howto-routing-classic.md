---
title: "Como tooconfigure roteamento (emparelhamento) para um circuito de rota expressa: Azure: clássico | Microsoft Docs"
description: "Este artigo o orienta pelas etapas de saudação para criar e provisionar Olá privado, público e emparelhamento da Microsoft de um circuito de rota expressa. Este artigo também mostra como status de saudação toocheck, atualizar ou excluir emparelhamentos para o seu circuito."
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
ms.openlocfilehash: dc5bcc4b86c3bc965a88281b6c2a660f3bc58eb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-classic"></a><span data-ttu-id="9bf35-104">Criar e modificar o emparelhamento de um circuito de ExpressRoute (clássico)</span><span class="sxs-lookup"><span data-stu-id="9bf35-104">Create and modify peering for an ExpressRoute circuit (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9bf35-105">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="9bf35-105">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="9bf35-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9bf35-106">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="9bf35-107">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="9bf35-107">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="9bf35-108">Vídeo – Emparelhamento privado</span><span class="sxs-lookup"><span data-stu-id="9bf35-108">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="9bf35-109">Vídeo – Emparelhamento público</span><span class="sxs-lookup"><span data-stu-id="9bf35-109">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="9bf35-110">Vídeo – Emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="9bf35-110">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="9bf35-111">PowerShell (clássico)</span><span class="sxs-lookup"><span data-stu-id="9bf35-111">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

<span data-ttu-id="9bf35-112">Este artigo orienta Olá etapas toocreate e gerenciar a configuração de roteamento para um circuito de rota expressa usando o modelo de implantação clássico hello e PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9bf35-112">This article walks you through hello steps toocreate and manage routing configuration for an ExpressRoute circuit using PowerShell and hello classic deployment model.</span></span> <span data-ttu-id="9bf35-113">Olá estas etapas também mostra como status de saudação toocheck, atualizar, ou excluir e desprovisionar emparelhamentos de um circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="9bf35-113">hello steps below will also show you how toocheck hello status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="9bf35-114">**Sobre modelos de implantação do Azure**</span><span class="sxs-lookup"><span data-stu-id="9bf35-114">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]


## <a name="configuration-prerequisites"></a><span data-ttu-id="9bf35-115">Pré-requisitos de configuração</span><span class="sxs-lookup"><span data-stu-id="9bf35-115">Configuration prerequisites</span></span>
* <span data-ttu-id="9bf35-116">Você precisará a versão mais recente de saudação do hello cmdlets do PowerShell de gerenciamento de serviço do Azure (SM).</span><span class="sxs-lookup"><span data-stu-id="9bf35-116">You will need hello latest version of hello Azure Service Management (SM) PowerShell cmdlets.</span></span> <span data-ttu-id="9bf35-117">Para saber mais, confira [Getting started with Azure PowerShell cmdlets](/powershell/azure/overview) (Introdução aos cmdlets do Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="9bf35-117">For more information, see [Getting started with Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>  
* <span data-ttu-id="9bf35-118">Certifique-se de ter revisado Olá [pré-requisitos](expressroute-prerequisites.md) página hello [requisitos de roteamento](expressroute-routing.md) página e hello [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração de página.</span><span class="sxs-lookup"><span data-stu-id="9bf35-118">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md) page, hello [routing requirements](expressroute-routing.md) page, and hello [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="9bf35-119">Você deve ter um circuito do ExpressRoute ativo.</span><span class="sxs-lookup"><span data-stu-id="9bf35-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="9bf35-120">Siga as instruções de saudação muito[criar um circuito de rota expressa](expressroute-howto-circuit-classic.md) e ter o circuito Olá habilitado por seu provedor de conectividade antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="9bf35-120">Follow hello instructions too[create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="9bf35-121">Olá circuito de rota expressa deve estar no estado habilitado e configurado para você toobe toorun capaz de saudação cmdlets descritos abaixo.</span><span class="sxs-lookup"><span data-stu-id="9bf35-121">hello ExpressRoute circuit must be in a provisioned and enabled state for you toobe able toorun hello cmdlets described below.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9bf35-122">Essas instruções se aplicam somente a toocircuits criado com provedores de serviço oferece serviços de conectividade de camada 2.</span><span class="sxs-lookup"><span data-stu-id="9bf35-122">These instructions only apply toocircuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="9bf35-123">Se você estiver usando um provedor de serviços que oferece serviços gerenciados de Camada 3 (normalmente um IPVPN, como MPLS), seu provedor de conectividade configurará e gerenciará o roteamento para você.</span><span class="sxs-lookup"><span data-stu-id="9bf35-123">If you are using a service provider offering managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

<span data-ttu-id="9bf35-124">Você pode configurar um, dois ou todos os três emparelhamentos (privado e público do Azure e da Microsoft) para um circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9bf35-124">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="9bf35-125">Você pode configurar emparelhamentos em qualquer ordem escolhida.</span><span class="sxs-lookup"><span data-stu-id="9bf35-125">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="9bf35-126">No entanto, você deve garantir que você conclua a configuração de saudação de cada um emparelhamento de cada vez.</span><span class="sxs-lookup"><span data-stu-id="9bf35-126">However, you must make sure that you complete hello configuration of each peering one at a time.</span></span>


### <a name="log-in-tooyour-azure-account-and-select-a-subscription"></a><span data-ttu-id="9bf35-127">Faça logon no tooyour conta do Azure e selecione uma assinatura</span><span class="sxs-lookup"><span data-stu-id="9bf35-127">Log in tooyour Azure account and select a subscription</span></span>
1. <span data-ttu-id="9bf35-128">Abra o console do PowerShell com direitos elevados e conecte-se a conta de tooyour.</span><span class="sxs-lookup"><span data-stu-id="9bf35-128">Open your PowerShell console with elevated rights and connect tooyour account.</span></span> <span data-ttu-id="9bf35-129">Use Olá toohelp de exemplo que você se conectar a seguir:</span><span class="sxs-lookup"><span data-stu-id="9bf35-129">Use hello following example toohelp you connect:</span></span>

        Login-AzureRmAccount

2. <span data-ttu-id="9bf35-130">Verificar as assinaturas de saudação para conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="9bf35-130">Check hello subscriptions for hello account.</span></span>

        Get-AzureRmSubscription

3. <span data-ttu-id="9bf35-131">Se você tiver mais de uma assinatura, selecione a assinatura de saudação que você deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="9bf35-131">If you have more than one subscription, select hello subscription that you want toouse.</span></span>

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. <span data-ttu-id="9bf35-132">Em seguida, use Olá tooadd cmdlet a seguir tooPowerShell sua assinatura do Azure para o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="9bf35-132">Next, use hello following cmdlet tooadd your Azure subscription tooPowerShell for hello classic deployment model.</span></span>

        Add-AzureAccount


## <a name="azure-private-peering"></a><span data-ttu-id="9bf35-133">Emparelhamento privado do Azure</span><span class="sxs-lookup"><span data-stu-id="9bf35-133">Azure private peering</span></span>
<span data-ttu-id="9bf35-134">Esta seção fornece instruções sobre como toocreate, obter, atualizar e excluir Olá configuração emparelhamento particular do Azure para um circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="9bf35-134">This section provides instructions on how toocreate, get, update, and delete hello Azure private peering configuration for an ExpressRoute circuit.</span></span> 

### <a name="toocreate-azure-private-peering"></a><span data-ttu-id="9bf35-135">toocreate emparelhamento particular do Azure</span><span class="sxs-lookup"><span data-stu-id="9bf35-135">toocreate Azure private peering</span></span>
1. <span data-ttu-id="9bf35-136">**Importe o módulo do PowerShell de saudação do ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="9bf35-136">**Import hello PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="9bf35-137">Você deve importar os módulos do Azure e rota expressa Olá na sessão do PowerShell Olá em ordem toostart usando os cmdlets de rota expressa hello.</span><span class="sxs-lookup"><span data-stu-id="9bf35-137">You must import hello Azure and ExpressRoute modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="9bf35-138">A seguir Olá execução comandos módulos do Azure e rota expressa Olá tooimport na sessão do PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="9bf35-138">Run hello following commands tooimport hello Azure and ExpressRoute modules into hello PowerShell session.</span></span>  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="9bf35-139">**Criar um circuito do ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="9bf35-139">**Create an ExpressRoute circuit.**</span></span>
   
    <span data-ttu-id="9bf35-140">Siga Olá instruções toocreate um [circuito de rota expressa](expressroute-howto-circuit-classic.md) e fornecidos pelo provedor de conectividade de saudação.</span><span class="sxs-lookup"><span data-stu-id="9bf35-140">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by hello connectivity provider.</span></span> <span data-ttu-id="9bf35-141">Se seu provedor de conectividade oferece serviços gerenciados de camada 3, você pode solicitar sua tooenable de provedor de conectividade Azure privado de emparelhamento para você.</span><span class="sxs-lookup"><span data-stu-id="9bf35-141">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="9bf35-142">Nesse caso, você não precisará toofollow instruções listadas nas seções próximas hello.</span><span class="sxs-lookup"><span data-stu-id="9bf35-142">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="9bf35-143">No entanto, se seu provedor de conectividade não gerencia o roteamento para você, depois de criar o circuito, siga as instruções de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="9bf35-143">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow hello instructions below.</span></span> 
3. <span data-ttu-id="9bf35-144">**Verifique Olá tooensure de circuito de rota expressa que é provisionado.**</span><span class="sxs-lookup"><span data-stu-id="9bf35-144">**Check hello ExpressRoute circuit tooensure it is provisioned.**</span></span>
   
    <span data-ttu-id="9bf35-145">Primeiro, você deve verificar toosee se hello circuito de rota expressa é provisionado e também está habilitado.</span><span class="sxs-lookup"><span data-stu-id="9bf35-145">You must first check toosee if hello ExpressRoute circuit is Provisioned and also Enabled.</span></span> <span data-ttu-id="9bf35-146">Consulte o exemplo hello abaixo.</span><span class="sxs-lookup"><span data-stu-id="9bf35-146">See hello example below.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="9bf35-147">Certifique-se de que o circuito Olá mostra como provisionado e habilitado.</span><span class="sxs-lookup"><span data-stu-id="9bf35-147">Make sure that hello circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="9bf35-148">Se não estiver, trabalhe com seu tooget do provedor de conectividade seu circuito toohello necessária e o status.</span><span class="sxs-lookup"><span data-stu-id="9bf35-148">If it doesn't, work with your connectivity provider tooget your circuit toohello required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="9bf35-149">**Configure o emparelhamento particular do Azure para o circuito de saudação.**</span><span class="sxs-lookup"><span data-stu-id="9bf35-149">**Configure Azure private peering for hello circuit.**</span></span>
   
    <span data-ttu-id="9bf35-150">Certifique-se de que você tenha Olá itens a seguir antes de prosseguir com as próximas etapas hello:</span><span class="sxs-lookup"><span data-stu-id="9bf35-150">Make sure that you have hello following items before you proceed with hello next steps:</span></span>
   
   * <span data-ttu-id="9bf35-151">Um /30 sub-rede para o link primário hello.</span><span class="sxs-lookup"><span data-stu-id="9bf35-151">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="9bf35-152">Ela não deve fazer parte de qualquer espaço de endereçamento reservado para redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="9bf35-152">This must not be part of any address space reserved for virtual networks.</span></span>
   * <span data-ttu-id="9bf35-153">Um /30 sub-rede para o link secundário hello.</span><span class="sxs-lookup"><span data-stu-id="9bf35-153">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="9bf35-154">Ela não deve fazer parte de qualquer espaço de endereçamento reservado para redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="9bf35-154">This must not be part of any address space reserved for virtual networks.</span></span>
   * <span data-ttu-id="9bf35-155">Um tooestablish de ID de VLAN válida esse emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="9bf35-155">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="9bf35-156">Certifique-se de que nenhum outro emparelhamento no circuito de saudação usa Olá a mesma ID de VLAN.</span><span class="sxs-lookup"><span data-stu-id="9bf35-156">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
   * <span data-ttu-id="9bf35-157">Número de AS para emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="9bf35-157">AS number for peering.</span></span> <span data-ttu-id="9bf35-158">Você pode usar um número de AS de 2 e de 4 bytes.</span><span class="sxs-lookup"><span data-stu-id="9bf35-158">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="9bf35-159">Você pode usar um número de AS privado para esse emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="9bf35-159">You can use a private AS number for this peering.</span></span> <span data-ttu-id="9bf35-160">Não use 65515.</span><span class="sxs-lookup"><span data-stu-id="9bf35-160">Ensure that you are not using 65515.</span></span>
   * <span data-ttu-id="9bf35-161">Um hash MD5 se você escolher toouse um.</span><span class="sxs-lookup"><span data-stu-id="9bf35-161">An MD5 hash if you choose toouse one.</span></span> <span data-ttu-id="9bf35-162">**Isso é opcional**.</span><span class="sxs-lookup"><span data-stu-id="9bf35-162">**This is optional**.</span></span>
     
    <span data-ttu-id="9bf35-163">Você pode executar Olá tooconfigure cmdlet emparelhamento particular do Azure para o circuito a seguir.</span><span class="sxs-lookup"><span data-stu-id="9bf35-163">You can run hello following cmdlet tooconfigure Azure private peering for your circuit.</span></span>
     
        <span data-ttu-id="9bf35-164">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100</span><span class="sxs-lookup"><span data-stu-id="9bf35-164">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100</span></span>
     
    <span data-ttu-id="9bf35-165">Você pode usar o cmdlet de saudação abaixo se você escolher toouse um hash MD5.</span><span class="sxs-lookup"><span data-stu-id="9bf35-165">You can use hello cmdlet below if you choose toouse an MD5 hash.</span></span>
     
        <span data-ttu-id="9bf35-166">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100 -SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="9bf35-166">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100 -SharedKey "A1B2C3D4"</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="9bf35-167">Especifique o número de AS como um ASN de emparelhamento, não um ASN de cliente.</span><span class="sxs-lookup"><span data-stu-id="9bf35-167">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
     > 
     > 

### <a name="tooview-azure-private-peering-details"></a><span data-ttu-id="9bf35-168">tooview privado emparelhamento detalhes do Azure</span><span class="sxs-lookup"><span data-stu-id="9bf35-168">tooview Azure private peering details</span></span>
<span data-ttu-id="9bf35-169">Você pode obter os detalhes de configuração usando o cmdlet a seguir de saudação</span><span class="sxs-lookup"><span data-stu-id="9bf35-169">You can get configuration details using hello following cmdlet</span></span>

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


### <a name="tooupdate-azure-private-peering-configuration"></a><span data-ttu-id="9bf35-170">tooupdate configuração emparelhamento particular do Azure</span><span class="sxs-lookup"><span data-stu-id="9bf35-170">tooupdate Azure private peering configuration</span></span>
<span data-ttu-id="9bf35-171">Você pode atualizar qualquer parte da configuração de saudação usando Olá cmdlet a seguir.</span><span class="sxs-lookup"><span data-stu-id="9bf35-171">You can update any part of hello configuration using hello following cmdlet.</span></span> <span data-ttu-id="9bf35-172">O exemplo hello abaixo, Olá VLAN ID de circuito hello está sendo atualizado de 100 too500.</span><span class="sxs-lookup"><span data-stu-id="9bf35-172">In hello example below, hello VLAN ID of hello circuit is being updated from 100 too500.</span></span>

    Set-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 500 -SharedKey "A1B2C3D4"

### <a name="toodelete-azure-private-peering"></a><span data-ttu-id="9bf35-173">toodelete emparelhamento particular do Azure</span><span class="sxs-lookup"><span data-stu-id="9bf35-173">toodelete Azure private peering</span></span>
<span data-ttu-id="9bf35-174">Você pode remover a configuração do emparelhamento executando Olá cmdlet a seguir.</span><span class="sxs-lookup"><span data-stu-id="9bf35-174">You can remove your peering configuration by running hello following cmdlet.</span></span>

> [!WARNING]
> <span data-ttu-id="9bf35-175">Certifique-se de que todas as redes virtuais são desvinculadas do hello circuito de rota expressa antes de executar este cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9bf35-175">You must ensure that all virtual networks are unlinked from hello ExpressRoute circuit before running this cmdlet.</span></span> 
> 
> 

    Remove-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"


## <a name="azure-public-peering"></a><span data-ttu-id="9bf35-176">Emparelhamento público do Azure</span><span class="sxs-lookup"><span data-stu-id="9bf35-176">Azure public peering</span></span>
<span data-ttu-id="9bf35-177">Esta seção fornece instruções sobre como toocreate, obter, atualizar e excluir Olá a configuração de emparelhamento pública do Azure para um circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="9bf35-177">This section provides instructions on how toocreate, get, update and delete hello Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-public-peering"></a><span data-ttu-id="9bf35-178">toocreate emparelhamento público do Azure</span><span class="sxs-lookup"><span data-stu-id="9bf35-178">toocreate Azure public peering</span></span>
1. <span data-ttu-id="9bf35-179">**Importe o módulo do PowerShell de saudação do ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="9bf35-179">**Import hello PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="9bf35-180">Você deve importar os módulos do Azure e rota expressa Olá na sessão do PowerShell Olá em ordem toostart usando os cmdlets de rota expressa hello.</span><span class="sxs-lookup"><span data-stu-id="9bf35-180">You must import hello Azure and ExpressRoute modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="9bf35-181">A seguir Olá execução comandos módulos do Azure e rota expressa Olá tooimport na sessão do PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="9bf35-181">Run hello following commands tooimport hello Azure and ExpressRoute modules into hello PowerShell session.</span></span> 
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="9bf35-182">**Criar um circuito do ExpressRoute**</span><span class="sxs-lookup"><span data-stu-id="9bf35-182">**Create an ExpressRoute circuit**</span></span>
   
    <span data-ttu-id="9bf35-183">Siga Olá instruções toocreate um [circuito de rota expressa](expressroute-howto-circuit-classic.md) e fornecidos pelo provedor de conectividade de saudação.</span><span class="sxs-lookup"><span data-stu-id="9bf35-183">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by hello connectivity provider.</span></span> <span data-ttu-id="9bf35-184">Se seu provedor de conectividade oferece serviços gerenciados de camada 3, você pode solicitar sua tooenable de provedor de conectividade do Azure público de emparelhamento para você.</span><span class="sxs-lookup"><span data-stu-id="9bf35-184">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure public peering for you.</span></span> <span data-ttu-id="9bf35-185">Nesse caso, você não precisará toofollow instruções listadas nas seções próximas hello.</span><span class="sxs-lookup"><span data-stu-id="9bf35-185">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="9bf35-186">No entanto, se seu provedor de conectividade não gerencia o roteamento para você, depois de criar o circuito, siga as instruções de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="9bf35-186">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow hello instructions below.</span></span>
3. <span data-ttu-id="9bf35-187">**Verificar tooensure de circuito de rota expressa, que ela é provisionada**</span><span class="sxs-lookup"><span data-stu-id="9bf35-187">**Check ExpressRoute circuit tooensure it is provisioned**</span></span>
   
    <span data-ttu-id="9bf35-188">Primeiro, você deve verificar toosee se hello circuito de rota expressa é provisionado e também está habilitado.</span><span class="sxs-lookup"><span data-stu-id="9bf35-188">You must first check toosee if hello ExpressRoute circuit is Provisioned and also Enabled.</span></span> <span data-ttu-id="9bf35-189">Consulte o exemplo hello abaixo.</span><span class="sxs-lookup"><span data-stu-id="9bf35-189">See hello example below.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="9bf35-190">Certifique-se de que o circuito Olá mostra como provisionado e habilitado.</span><span class="sxs-lookup"><span data-stu-id="9bf35-190">Make sure that hello circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="9bf35-191">Se não estiver, trabalhe com seu tooget do provedor de conectividade seu circuito toohello necessária e o status.</span><span class="sxs-lookup"><span data-stu-id="9bf35-191">If it doesn't, work with your connectivity provider tooget your circuit toohello required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="9bf35-192">**Configurar o emparelhamento público do Azure para o circuito Olá**</span><span class="sxs-lookup"><span data-stu-id="9bf35-192">**Configure Azure public peering for hello circuit**</span></span>
   
    <span data-ttu-id="9bf35-193">Certifique-se de que você tenha Olá informações a seguir antes de você continuar.</span><span class="sxs-lookup"><span data-stu-id="9bf35-193">Ensure that you have hello following information before you proceed further.</span></span>
   
   * <span data-ttu-id="9bf35-194">Um /30 sub-rede para o link primário hello.</span><span class="sxs-lookup"><span data-stu-id="9bf35-194">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="9bf35-195">Precisa ser um prefixo IPv4 público válido.</span><span class="sxs-lookup"><span data-stu-id="9bf35-195">This must be a valid public IPv4 prefix.</span></span>
   * <span data-ttu-id="9bf35-196">Um /30 sub-rede para o link secundário hello.</span><span class="sxs-lookup"><span data-stu-id="9bf35-196">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="9bf35-197">Precisa ser um prefixo IPv4 público válido.</span><span class="sxs-lookup"><span data-stu-id="9bf35-197">This must be a valid public IPv4 prefix.</span></span>
   * <span data-ttu-id="9bf35-198">Um tooestablish de ID de VLAN válida esse emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="9bf35-198">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="9bf35-199">Certifique-se de que nenhum outro emparelhamento no circuito de saudação usa Olá a mesma ID de VLAN.</span><span class="sxs-lookup"><span data-stu-id="9bf35-199">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
   * <span data-ttu-id="9bf35-200">Número de AS para emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="9bf35-200">AS number for peering.</span></span> <span data-ttu-id="9bf35-201">Você pode usar um número de AS de 2 e de 4 bytes.</span><span class="sxs-lookup"><span data-stu-id="9bf35-201">You can use both 2-byte and 4-byte AS numbers.</span></span>
   * <span data-ttu-id="9bf35-202">Um hash MD5 se você escolher toouse um.</span><span class="sxs-lookup"><span data-stu-id="9bf35-202">An MD5 hash if you choose toouse one.</span></span> <span data-ttu-id="9bf35-203">**Isso é opcional**.</span><span class="sxs-lookup"><span data-stu-id="9bf35-203">**This is optional**.</span></span>
     
    <span data-ttu-id="9bf35-204">Você pode executar Olá após tooconfigure cmdlet emparelhamento público do Azure para o circuito</span><span class="sxs-lookup"><span data-stu-id="9bf35-204">You can run hello following cmdlet tooconfigure Azure public peering for your circuit</span></span>
     
        <span data-ttu-id="9bf35-205">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200</span><span class="sxs-lookup"><span data-stu-id="9bf35-205">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200</span></span>
     
    <span data-ttu-id="9bf35-206">Você pode usar o cmdlet de saudação abaixo se você escolher toouse um hash MD5</span><span class="sxs-lookup"><span data-stu-id="9bf35-206">You can use hello cmdlet below if you choose toouse an MD5 hash</span></span>
     
        <span data-ttu-id="9bf35-207">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200 -SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="9bf35-207">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200 -SharedKey "A1B2C3D4"</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="9bf35-208">Especifique o número de AS como um ASN de emparelhamento e não um ASN de cliente.</span><span class="sxs-lookup"><span data-stu-id="9bf35-208">Ensure that you specify your AS number as peering ASN and not customer ASN.</span></span>
     > 
     > 

### <a name="tooview-azure-public-peering-details"></a><span data-ttu-id="9bf35-209">tooview público emparelhamento detalhes do Azure</span><span class="sxs-lookup"><span data-stu-id="9bf35-209">tooview Azure public peering details</span></span>
<span data-ttu-id="9bf35-210">Você pode obter os detalhes de configuração usando o cmdlet a seguir de saudação</span><span class="sxs-lookup"><span data-stu-id="9bf35-210">You can get configuration details using hello following cmdlet</span></span>

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


### <a name="tooupdate-azure-public-peering-configuration"></a><span data-ttu-id="9bf35-211">tooupdate configuração de emparelhamento pública do Azure</span><span class="sxs-lookup"><span data-stu-id="9bf35-211">tooupdate Azure public peering configuration</span></span>
<span data-ttu-id="9bf35-212">Você pode atualizar qualquer parte da configuração de saudação usando Olá cmdlet a seguir</span><span class="sxs-lookup"><span data-stu-id="9bf35-212">You can update any part of hello configuration using hello following cmdlet</span></span>

    Set-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 600 -SharedKey "A1B2C3D4"

<span data-ttu-id="9bf35-213">Olá VLAN ID de circuito hello está sendo atualizado de 200 too600 em Olá exemplo acima.</span><span class="sxs-lookup"><span data-stu-id="9bf35-213">hello VLAN ID of hello circuit is being updated from 200 too600 in hello above example.</span></span>

### <a name="toodelete-azure-public-peering"></a><span data-ttu-id="9bf35-214">toodelete emparelhamento público do Azure</span><span class="sxs-lookup"><span data-stu-id="9bf35-214">toodelete Azure public peering</span></span>
<span data-ttu-id="9bf35-215">Você pode remover a configuração do emparelhamento executando Olá cmdlet a seguir</span><span class="sxs-lookup"><span data-stu-id="9bf35-215">You can remove your peering configuration by running hello following cmdlet</span></span>

    Remove-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

## <a name="microsoft-peering"></a><span data-ttu-id="9bf35-216">Emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="9bf35-216">Microsoft peering</span></span>
<span data-ttu-id="9bf35-217">Esta seção fornece instruções sobre como toocreate, obter, atualizar e excluir a configuração de emparelhamento Microsoft hello por um circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="9bf35-217">This section provides instructions on how toocreate, get, update and delete hello Microsoft peering configuration for an ExpressRoute circuit.</span></span> 

### <a name="toocreate-microsoft-peering"></a><span data-ttu-id="9bf35-218">toocreate emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="9bf35-218">toocreate Microsoft peering</span></span>
1. <span data-ttu-id="9bf35-219">**Importe o módulo do PowerShell de saudação do ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="9bf35-219">**Import hello PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="9bf35-220">Você deve importar os módulos do Azure e rota expressa Olá na sessão do PowerShell Olá em ordem toostart usando os cmdlets de rota expressa hello.</span><span class="sxs-lookup"><span data-stu-id="9bf35-220">You must import hello Azure and ExpressRoute modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="9bf35-221">A seguir Olá execução comandos módulos do Azure e rota expressa Olá tooimport na sessão do PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="9bf35-221">Run hello following commands tooimport hello Azure and ExpressRoute modules into hello PowerShell session.</span></span>  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="9bf35-222">**Criar um circuito do ExpressRoute**</span><span class="sxs-lookup"><span data-stu-id="9bf35-222">**Create an ExpressRoute circuit**</span></span>
   
    <span data-ttu-id="9bf35-223">Siga Olá instruções toocreate um [circuito de rota expressa](expressroute-howto-circuit-classic.md) e fornecidos pelo provedor de conectividade de saudação.</span><span class="sxs-lookup"><span data-stu-id="9bf35-223">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by hello connectivity provider.</span></span> <span data-ttu-id="9bf35-224">Se seu provedor de conectividade oferece serviços gerenciados de camada 3, você pode solicitar sua tooenable de provedor de conectividade Azure privado de emparelhamento para você.</span><span class="sxs-lookup"><span data-stu-id="9bf35-224">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="9bf35-225">Nesse caso, você não precisará toofollow instruções listadas nas seções próximas hello.</span><span class="sxs-lookup"><span data-stu-id="9bf35-225">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="9bf35-226">No entanto, se seu provedor de conectividade não gerencia o roteamento para você, depois de criar o circuito, siga as instruções de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="9bf35-226">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow hello instructions below.</span></span>
3. <span data-ttu-id="9bf35-227">**Verificar tooensure de circuito de rota expressa, que ela é provisionada**</span><span class="sxs-lookup"><span data-stu-id="9bf35-227">**Check ExpressRoute circuit tooensure it is provisioned**</span></span>
   
    <span data-ttu-id="9bf35-228">Primeiro, você deve verificar toosee se Olá circuito ExpressRoute está em estado provisionado e habilitado.</span><span class="sxs-lookup"><span data-stu-id="9bf35-228">You must first check toosee if hello ExpressRoute circuit is in Provisioned and Enabled state.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="9bf35-229">Certifique-se de que o circuito Olá mostra como provisionado e habilitado.</span><span class="sxs-lookup"><span data-stu-id="9bf35-229">Make sure that hello circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="9bf35-230">Se não estiver, trabalhe com seu tooget do provedor de conectividade seu circuito toohello necessária e o status.</span><span class="sxs-lookup"><span data-stu-id="9bf35-230">If it doesn't, work with your connectivity provider tooget your circuit toohello required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="9bf35-231">**Configurar o emparelhamento do circuito de saudação do Microsoft**</span><span class="sxs-lookup"><span data-stu-id="9bf35-231">**Configure Microsoft peering for hello circuit**</span></span>
   
    <span data-ttu-id="9bf35-232">Certifique-se de que você tenha Olá seguintes informações antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="9bf35-232">Make sure that you have hello following information before you proceed.</span></span>
   
   * <span data-ttu-id="9bf35-233">Um /30 sub-rede para o link primário hello.</span><span class="sxs-lookup"><span data-stu-id="9bf35-233">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="9bf35-234">Este valor deve ser um prefixo IPv4 público válido próprio e registrado em um RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="9bf35-234">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
   * <span data-ttu-id="9bf35-235">Um /30 sub-rede para o link secundário hello.</span><span class="sxs-lookup"><span data-stu-id="9bf35-235">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="9bf35-236">Este valor deve ser um prefixo IPv4 público válido próprio e registrado em um RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="9bf35-236">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
   * <span data-ttu-id="9bf35-237">Um tooestablish de ID de VLAN válida esse emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="9bf35-237">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="9bf35-238">Certifique-se de que nenhum outro emparelhamento no circuito de saudação usa Olá a mesma ID de VLAN.</span><span class="sxs-lookup"><span data-stu-id="9bf35-238">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
   * <span data-ttu-id="9bf35-239">Número de AS para emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="9bf35-239">AS number for peering.</span></span> <span data-ttu-id="9bf35-240">Você pode usar um número de AS de 2 e de 4 bytes.</span><span class="sxs-lookup"><span data-stu-id="9bf35-240">You can use both 2-byte and 4-byte AS numbers.</span></span>
   * <span data-ttu-id="9bf35-241">Anunciado prefixos: você deve fornecer uma lista de todos os prefixos planejar tooadvertise sobre a sessão BGP de saudação.</span><span class="sxs-lookup"><span data-stu-id="9bf35-241">Advertised prefixes: You must provide a list of all prefixes you plan tooadvertise over hello BGP session.</span></span> <span data-ttu-id="9bf35-242">Somente prefixos de endereços IP públicos são aceitos.</span><span class="sxs-lookup"><span data-stu-id="9bf35-242">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="9bf35-243">Você pode enviar uma lista separada por vírgulas se você planejar toosend um conjunto de prefixos.</span><span class="sxs-lookup"><span data-stu-id="9bf35-243">You can send a comma separated list if you plan toosend a set of prefixes.</span></span> <span data-ttu-id="9bf35-244">Esses prefixos devem ser registrado tooyou em um RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="9bf35-244">These prefixes must be registered tooyou in an RIR / IRR.</span></span>
   * <span data-ttu-id="9bf35-245">Cliente ASN: Se você estiver publicidade prefixos que não são registrado toohello emparelhamento como número, você pode especificar hello como número toowhich, que eles são registrados.</span><span class="sxs-lookup"><span data-stu-id="9bf35-245">Customer ASN: If you are advertising prefixes that are not registered toohello peering AS number, you can specify hello AS number toowhich they are registered.</span></span> <span data-ttu-id="9bf35-246">**Isso é opcional**.</span><span class="sxs-lookup"><span data-stu-id="9bf35-246">**This is optional**.</span></span>
   * <span data-ttu-id="9bf35-247">Nome de roteamento do registro: Você pode especificar Olá RIR / IRR no qual hello como número e prefixos estão registrados.</span><span class="sxs-lookup"><span data-stu-id="9bf35-247">Routing Registry Name: You can specify hello RIR / IRR against which hello AS number and prefixes are registered.</span></span>
   * <span data-ttu-id="9bf35-248">Um hash MD5, se você escolher toouse um.</span><span class="sxs-lookup"><span data-stu-id="9bf35-248">An MD5 hash, if you choose toouse one.</span></span> <span data-ttu-id="9bf35-249">**Isso é opcional.**</span><span class="sxs-lookup"><span data-stu-id="9bf35-249">**This is optional.**</span></span>
     
    <span data-ttu-id="9bf35-250">Você pode executar Olá após pering de Microsoft tooconfigure cmdlet para o circuito</span><span class="sxs-lookup"><span data-stu-id="9bf35-250">You can run hello following cmdlet tooconfigure Microsoft pering for your circuit</span></span>
     
        <span data-ttu-id="9bf35-251">New-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="9bf35-251">New-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"</span></span>

### <a name="tooview-microsoft-peering-details"></a><span data-ttu-id="9bf35-252">tooview detalhes de emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="9bf35-252">tooview Microsoft peering details</span></span>
<span data-ttu-id="9bf35-253">Você pode obter os detalhes de configuração usando Olá cmdlet a seguir.</span><span class="sxs-lookup"><span data-stu-id="9bf35-253">You can get configuration details using hello following cmdlet.</span></span>

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


### <a name="tooupdate-microsoft-peering-configuration"></a><span data-ttu-id="9bf35-254">tooupdate configuração de emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="9bf35-254">tooupdate Microsoft peering configuration</span></span>
<span data-ttu-id="9bf35-255">Você pode atualizar qualquer parte da configuração de saudação usando Olá cmdlet a seguir.</span><span class="sxs-lookup"><span data-stu-id="9bf35-255">You can update any part of hello configuration using hello following cmdlet.</span></span>

    Set-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"

### <a name="toodelete-microsoft-peering"></a><span data-ttu-id="9bf35-256">toodelete emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="9bf35-256">toodelete Microsoft peering</span></span>
<span data-ttu-id="9bf35-257">Você pode remover a configuração do emparelhamento executando Olá cmdlet a seguir.</span><span class="sxs-lookup"><span data-stu-id="9bf35-257">You can remove your peering configuration by running hello following cmdlet.</span></span>

    Remove-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

## <a name="next-steps"></a><span data-ttu-id="9bf35-258">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9bf35-258">Next steps</span></span>
<span data-ttu-id="9bf35-259">Em seguida, [vincular um circuito de rota expressa do tooan de VNet](expressroute-howto-linkvnet-classic.md).</span><span class="sxs-lookup"><span data-stu-id="9bf35-259">Next, [Link a VNet tooan ExpressRoute circuit](expressroute-howto-linkvnet-classic.md).</span></span>

* <span data-ttu-id="9bf35-260">Para obter mais informações sobre fluxos de trabalho, veja [Fluxos de trabalho do ExpressRoute](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="9bf35-260">For more information about workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="9bf35-261">Para obter mais informações sobre o emparelhamento de circuito, veja [Circuitos e domínios de roteamento do ExpressRoute](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="9bf35-261">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>

