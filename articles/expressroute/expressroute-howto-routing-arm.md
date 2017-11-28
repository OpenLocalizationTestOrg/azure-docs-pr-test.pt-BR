---
title: 'Como tooconfigure roteamento (emparelhamento) para um circuito de rota expressa: Gerenciador de recursos: PowerShell: Azure | Microsoft Docs'
description: "Este artigo o orienta pelas etapas de saudação para criar e provisionar Olá privado, público e emparelhamento da Microsoft de um circuito de rota expressa. Este artigo também mostra como status de saudação toocheck, atualizar ou excluir emparelhamentos para o seu circuito."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0a036d51-77ae-4fee-9ddb-35f040fbdcdf
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: eb3ddf5c05a086ac3e22c64417e51381ef465921
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-using-powershell"></a><span data-ttu-id="dcc14-104">Criar e modificar o emparelhamento de um circuito do ExpressRoute usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="dcc14-104">Create and modify peering for an ExpressRoute circuit using PowerShell</span></span>

<span data-ttu-id="dcc14-105">Este artigo ajuda você a criar e gerenciar a configuração de roteamento para um circuito de rota expressa no modelo de implantação do Gerenciador de recursos do hello usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dcc14-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in hello Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="dcc14-106">Você também pode verificar status hello, update ou delete e desprovisionar emparelhamentos de um circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="dcc14-106">You can also check hello status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="dcc14-107">Se você quiser toouse toowork um método diferente com o circuito, selecione um artigo de saudação lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="dcc14-107">If you want toouse a different method toowork with your circuit, select an article from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="dcc14-108">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="dcc14-108">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="dcc14-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dcc14-109">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="dcc14-110">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="dcc14-110">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="dcc14-111">Vídeo – Emparelhamento privado</span><span class="sxs-lookup"><span data-stu-id="dcc14-111">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="dcc14-112">Vídeo – Emparelhamento público</span><span class="sxs-lookup"><span data-stu-id="dcc14-112">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="dcc14-113">Vídeo – Emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="dcc14-113">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="dcc14-114">PowerShell (clássico)</span><span class="sxs-lookup"><span data-stu-id="dcc14-114">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="dcc14-115">Pré-requisitos de configuração</span><span class="sxs-lookup"><span data-stu-id="dcc14-115">Configuration prerequisites</span></span>

* <span data-ttu-id="dcc14-116">Você precisará a versão mais recente de saudação do hello cmdlets do PowerShell do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="dcc14-116">You will need hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="dcc14-117">Para obter mais informações, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dcc14-117">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> 
* <span data-ttu-id="dcc14-118">Certifique-se de ter revisado Olá [pré-requisitos](expressroute-prerequisites.md) página hello [requisitos de roteamento](expressroute-routing.md) página e hello [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração de página.</span><span class="sxs-lookup"><span data-stu-id="dcc14-118">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md) page, hello [routing requirements](expressroute-routing.md) page, and hello [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="dcc14-119">Você deve ter um circuito do ExpressRoute ativo.</span><span class="sxs-lookup"><span data-stu-id="dcc14-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="dcc14-120">Siga as instruções de saudação muito[criar um circuito de rota expressa](expressroute-howto-circuit-arm.md) e ter o circuito Olá habilitado por seu provedor de conectividade antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="dcc14-120">Follow hello instructions too[Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="dcc14-121">Olá circuito de rota expressa deve estar em um estado habilitado e configurado para você toobe toorun capaz de saudação cmdlets neste artigo.</span><span class="sxs-lookup"><span data-stu-id="dcc14-121">hello ExpressRoute circuit must be in a provisioned and enabled state for you toobe able toorun hello cmdlets in this article.</span></span>

<span data-ttu-id="dcc14-122">Essas instruções se aplicam somente a toocircuits criado com provedores de serviço oferece serviços de conectividade de camada 2.</span><span class="sxs-lookup"><span data-stu-id="dcc14-122">These instructions only apply toocircuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="dcc14-123">Se você estiver usando um provedor de serviços que ofereça serviços gerenciados de Camada 3 (normalmente um IPVPN, como MPLS), seu provedor de conectividade configurará e gerenciará o roteamento para você.</span><span class="sxs-lookup"><span data-stu-id="dcc14-123">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dcc14-124">Estamos atualmente não anuncie emparelhamentos configurados pelos provedores de serviço por meio do portal de gerenciamento de serviços de saudação.</span><span class="sxs-lookup"><span data-stu-id="dcc14-124">We currently do not advertise peerings configured by service providers through hello service management portal.</span></span> <span data-ttu-id="dcc14-125">Estamos trabalhando para habilitar esse recurso em breve.</span><span class="sxs-lookup"><span data-stu-id="dcc14-125">We are working on enabling this capability soon.</span></span> <span data-ttu-id="dcc14-126">Verifique com seu provedor de serviços antes de configurar os emparelhamentos via protocolo BGP.</span><span class="sxs-lookup"><span data-stu-id="dcc14-126">Check with your service provider before configuring BGP peerings.</span></span>
> 
> 

<span data-ttu-id="dcc14-127">Você pode configurar um, dois ou todos os três emparelhamentos (privado e público do Azure e da Microsoft) para um circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="dcc14-127">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="dcc14-128">Você pode configurar emparelhamentos em qualquer ordem escolhida.</span><span class="sxs-lookup"><span data-stu-id="dcc14-128">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="dcc14-129">No entanto, você deve garantir que você conclua a configuração de saudação de cada um emparelhamento de cada vez.</span><span class="sxs-lookup"><span data-stu-id="dcc14-129">However, you must make sure that you complete hello configuration of each peering one at a time.</span></span> 

## <a name="azure-private-peering"></a><span data-ttu-id="dcc14-130">Emparelhamento privado do Azure</span><span class="sxs-lookup"><span data-stu-id="dcc14-130">Azure private peering</span></span>

<span data-ttu-id="dcc14-131">Esta seção ajuda você a criar, obter, atualizar e excluir Olá configuração emparelhamento particular do Azure para um circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="dcc14-131">This section helps you create, get, update, and delete hello Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-private-peering"></a><span data-ttu-id="dcc14-132">toocreate emparelhamento particular do Azure</span><span class="sxs-lookup"><span data-stu-id="dcc14-132">toocreate Azure private peering</span></span>

1. <span data-ttu-id="dcc14-133">Importe o módulo do PowerShell de saudação do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="dcc14-133">Import hello PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="dcc14-134">Você deve instalar o instalador do PowerShell mais recente saudação do [Galeria do PowerShell](http://www.powershellgallery.com/) e importar os módulos do Azure Resource Manager Olá na sessão do PowerShell Olá em ordem toostart usando os cmdlets de rota expressa hello.</span><span class="sxs-lookup"><span data-stu-id="dcc14-134">You must install hello latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import hello Azure Resource Manager modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="dcc14-135">Você precisará toorun PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="dcc14-135">You will need toorun PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM
  Install-AzureRM
  ```

  <span data-ttu-id="dcc14-136">Importe todos os módulos AzureRM.* Olá Olá conhecido intervalo de versão semântico.</span><span class="sxs-lookup"><span data-stu-id="dcc14-136">Import all of hello AzureRM.* modules within hello known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="dcc14-137">Você também pode importar um módulo selecione Olá conhecido intervalo de versão semântico.</span><span class="sxs-lookup"><span data-stu-id="dcc14-137">You can also just import a select module within hello known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network 
  ```

  <span data-ttu-id="dcc14-138">Entre na conta de tooyour.</span><span class="sxs-lookup"><span data-stu-id="dcc14-138">Sign in tooyour account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="dcc14-139">Selecione a assinatura de saudação desejado toocreate circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="dcc14-139">Select hello subscription you want toocreate ExpressRoute circuit.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="dcc14-140">Criar um circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="dcc14-140">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="dcc14-141">Siga Olá instruções toocreate um [circuito de rota expressa](expressroute-howto-circuit-arm.md) e fornecidos pelo provedor de conectividade de saudação.</span><span class="sxs-lookup"><span data-stu-id="dcc14-141">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="dcc14-142">Se seu provedor de conectividade oferece serviços gerenciados de camada 3, você pode solicitar sua tooenable de provedor de conectividade Azure privado de emparelhamento para você.</span><span class="sxs-lookup"><span data-stu-id="dcc14-142">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="dcc14-143">Nesse caso, você não precisará toofollow instruções listadas nas seções próximas hello.</span><span class="sxs-lookup"><span data-stu-id="dcc14-143">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="dcc14-144">No entanto, se seu provedor de conectividade não gerencia o roteamento para você, depois de criar o circuito, continue a configuração usando as próximas etapas hello.</span><span class="sxs-lookup"><span data-stu-id="dcc14-144">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="dcc14-145">Verifique toomake de circuito de rota expressa de saudação se ele está configurado e também está habilitado.</span><span class="sxs-lookup"><span data-stu-id="dcc14-145">Check hello ExpressRoute circuit toomake sure it is provisioned and also enabled.</span></span> <span data-ttu-id="dcc14-146">Use Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="dcc14-146">Use hello following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="dcc14-147">resposta de saudação é semelhante toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="dcc14-147">hello response is similar toohello following example:</span></span>

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                       "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. <span data-ttu-id="dcc14-148">Configure o emparelhamento particular do Azure para o circuito de saudação.</span><span class="sxs-lookup"><span data-stu-id="dcc14-148">Configure Azure private peering for hello circuit.</span></span> <span data-ttu-id="dcc14-149">Certifique-se de que você tenha Olá itens a seguir antes de prosseguir com as próximas etapas hello:</span><span class="sxs-lookup"><span data-stu-id="dcc14-149">Make sure that you have hello following items before you proceed with hello next steps:</span></span>

  * <span data-ttu-id="dcc14-150">Um /30 sub-rede para o link primário hello.</span><span class="sxs-lookup"><span data-stu-id="dcc14-150">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="dcc14-151">subrede Olá não deve fazer parte de qualquer espaço de endereço reservado para redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="dcc14-151">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="dcc14-152">Um /30 sub-rede para o link secundário hello.</span><span class="sxs-lookup"><span data-stu-id="dcc14-152">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="dcc14-153">subrede Olá não deve fazer parte de qualquer espaço de endereço reservado para redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="dcc14-153">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="dcc14-154">Um tooestablish de ID de VLAN válida esse emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="dcc14-154">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="dcc14-155">Certifique-se de que nenhum outro emparelhamento no circuito de saudação usa Olá a mesma ID de VLAN.</span><span class="sxs-lookup"><span data-stu-id="dcc14-155">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="dcc14-156">Número de AS para emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="dcc14-156">AS number for peering.</span></span> <span data-ttu-id="dcc14-157">Você pode usar um número de AS de 2 e de 4 bytes.</span><span class="sxs-lookup"><span data-stu-id="dcc14-157">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="dcc14-158">Você pode usar um número de AS privado para esse emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="dcc14-158">You can use a private AS number for this peering.</span></span> <span data-ttu-id="dcc14-159">Não use 65515.</span><span class="sxs-lookup"><span data-stu-id="dcc14-159">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="dcc14-160">**Opcional -** um hash MD5 se você escolher toouse um.</span><span class="sxs-lookup"><span data-stu-id="dcc14-160">**Optional -** An MD5 hash if you choose toouse one.</span></span>

  <span data-ttu-id="dcc14-161">Use hello Azure privado de emparelhamento para o circuito de tooconfigure de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="dcc14-161">Use hello following example tooconfigure Azure private peering for your circuit:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  <span data-ttu-id="dcc14-162">Se você escolher toouse um hash MD5, use Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="dcc14-162">If you choose toouse an MD5 hash, use hello following example:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200  -SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="dcc14-163">Especifique o número de AS como um ASN de emparelhamento, não um ASN de cliente.</span><span class="sxs-lookup"><span data-stu-id="dcc14-163">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  >

### <a name="tooview-azure-private-peering-details"></a><span data-ttu-id="dcc14-164">tooview privado emparelhamento detalhes do Azure</span><span class="sxs-lookup"><span data-stu-id="dcc14-164">tooview Azure private peering details</span></span>

<span data-ttu-id="dcc14-165">Você pode obter os detalhes de configuração usando Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="dcc14-165">You can get configuration details by using hello following example:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt
```

### <a name="tooupdate-azure-private-peering-configuration"></a><span data-ttu-id="dcc14-166">tooupdate configuração emparelhamento particular do Azure</span><span class="sxs-lookup"><span data-stu-id="dcc14-166">tooupdate Azure private peering configuration</span></span>

<span data-ttu-id="dcc14-167">Você pode atualizar qualquer parte da configuração de saudação usando Olá exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="dcc14-167">You can update any part of hello configuration using hello following example.</span></span> <span data-ttu-id="dcc14-168">Neste exemplo, Olá VLAN ID de circuito hello está sendo atualizado do too500 100.</span><span class="sxs-lookup"><span data-stu-id="dcc14-168">In this example, hello VLAN ID of hello circuit is being updated from 100 too500.</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-azure-private-peering"></a><span data-ttu-id="dcc14-169">toodelete emparelhamento particular do Azure</span><span class="sxs-lookup"><span data-stu-id="dcc14-169">toodelete Azure private peering</span></span>

<span data-ttu-id="dcc14-170">Você pode remover a configuração do emparelhamento executando Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="dcc14-170">You can remove your peering configuration by running hello following example:</span></span>

> [!WARNING]
> <span data-ttu-id="dcc14-171">Certifique-se de que todas as redes virtuais são desvinculadas do hello circuito de rota expressa antes de executar este exemplo.</span><span class="sxs-lookup"><span data-stu-id="dcc14-171">You must ensure that all virtual networks are unlinked from hello ExpressRoute circuit before running this example.</span></span> 
> 
> 

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="azure-public-peering"></a><span data-ttu-id="dcc14-172">Emparelhamento público do Azure</span><span class="sxs-lookup"><span data-stu-id="dcc14-172">Azure public peering</span></span>

<span data-ttu-id="dcc14-173">Esta seção ajuda você a criar, obter, atualizar e excluir Olá a configuração de emparelhamento pública do Azure para um circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="dcc14-173">This section helps you create, get, update, and delete hello Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-public-peering"></a><span data-ttu-id="dcc14-174">toocreate emparelhamento público do Azure</span><span class="sxs-lookup"><span data-stu-id="dcc14-174">toocreate Azure public peering</span></span>

1. <span data-ttu-id="dcc14-175">Importe o módulo do PowerShell de saudação do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="dcc14-175">Import hello PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="dcc14-176">Você deve instalar o instalador do PowerShell mais recente saudação do [Galeria do PowerShell](http://www.powershellgallery.com/) e importar os módulos do Azure Resource Manager Olá na sessão do PowerShell Olá em ordem toostart usando os cmdlets de rota expressa hello.</span><span class="sxs-lookup"><span data-stu-id="dcc14-176">You must install hello latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import hello Azure Resource Manager modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="dcc14-177">Você precisará toorun PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="dcc14-177">You will need toorun PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
```

  <span data-ttu-id="dcc14-178">Importe todos os módulos AzureRM.* Olá Olá conhecido intervalo de versão semântico.</span><span class="sxs-lookup"><span data-stu-id="dcc14-178">Import all of hello AzureRM.* modules within hello known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="dcc14-179">Você também pode importar um módulo selecione Olá conhecido intervalo de versão semântico.</span><span class="sxs-lookup"><span data-stu-id="dcc14-179">You can also just import a select module within hello known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network
```

  <span data-ttu-id="dcc14-180">Entre na conta de tooyour.</span><span class="sxs-lookup"><span data-stu-id="dcc14-180">Sign in tooyour account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="dcc14-181">Selecione a assinatura de saudação desejado toocreate circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="dcc14-181">Select hello subscription you want toocreate ExpressRoute circuit.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="dcc14-182">Criar um circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="dcc14-182">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="dcc14-183">Siga Olá instruções toocreate um [circuito de rota expressa](expressroute-howto-circuit-arm.md) e fornecidos pelo provedor de conectividade de saudação.</span><span class="sxs-lookup"><span data-stu-id="dcc14-183">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="dcc14-184">Se seu provedor de conectividade oferece serviços gerenciados de camada 3, você pode solicitar sua tooenable de provedor de conectividade Azure privado de emparelhamento para você.</span><span class="sxs-lookup"><span data-stu-id="dcc14-184">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="dcc14-185">Nesse caso, você não precisará toofollow instruções listadas nas seções próximas hello.</span><span class="sxs-lookup"><span data-stu-id="dcc14-185">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="dcc14-186">No entanto, se seu provedor de conectividade não gerencia o roteamento para você, depois de criar o circuito, continue a configuração usando as próximas etapas hello.</span><span class="sxs-lookup"><span data-stu-id="dcc14-186">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="dcc14-187">Verifique tooensure de circuito de rota expressa Olá provisionado e também está habilitado.</span><span class="sxs-lookup"><span data-stu-id="dcc14-187">Check hello ExpressRoute circuit tooensure it is provisioned and also enabled.</span></span> <span data-ttu-id="dcc14-188">Use Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="dcc14-188">Use hello following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="dcc14-189">resposta de saudação é semelhante toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="dcc14-189">hello response is similar toohello following example:</span></span>

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                      "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. <span data-ttu-id="dcc14-190">Configure o emparelhamento público do Azure para o circuito de saudação.</span><span class="sxs-lookup"><span data-stu-id="dcc14-190">Configure Azure public peering for hello circuit.</span></span> <span data-ttu-id="dcc14-191">Certifique-se de que você tenha Olá informações a seguir antes de você continuar.</span><span class="sxs-lookup"><span data-stu-id="dcc14-191">Make sure that you have hello following information before you proceed further.</span></span>

  * <span data-ttu-id="dcc14-192">Um /30 sub-rede para o link primário hello.</span><span class="sxs-lookup"><span data-stu-id="dcc14-192">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="dcc14-193">Precisa ser um prefixo IPv4 público válido.</span><span class="sxs-lookup"><span data-stu-id="dcc14-193">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="dcc14-194">Um /30 sub-rede para o link secundário hello.</span><span class="sxs-lookup"><span data-stu-id="dcc14-194">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="dcc14-195">Precisa ser um prefixo IPv4 público válido.</span><span class="sxs-lookup"><span data-stu-id="dcc14-195">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="dcc14-196">Um tooestablish de ID de VLAN válida esse emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="dcc14-196">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="dcc14-197">Certifique-se de que nenhum outro emparelhamento no circuito de saudação usa Olá a mesma ID de VLAN.</span><span class="sxs-lookup"><span data-stu-id="dcc14-197">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="dcc14-198">Número de AS para emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="dcc14-198">AS number for peering.</span></span> <span data-ttu-id="dcc14-199">Você pode usar um número de AS de 2 e de 4 bytes.</span><span class="sxs-lookup"><span data-stu-id="dcc14-199">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="dcc14-200">**Opcional -** um hash MD5 se você escolher toouse um.</span><span class="sxs-lookup"><span data-stu-id="dcc14-200">**Optional -** An MD5 hash if you choose toouse one.</span></span>

  <span data-ttu-id="dcc14-201">Executar hello Azure público de emparelhamento para o circuito de tooconfigure de exemplo a seguir</span><span class="sxs-lookup"><span data-stu-id="dcc14-201">Run hello following example tooconfigure Azure public peering for your circuit</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  <span data-ttu-id="dcc14-202">Se você escolher toouse um hash MD5, use Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="dcc14-202">If you choose toouse an MD5 hash, use hello following example:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100  -SharedKey "A1B2C3D4"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="dcc14-203">Especifique o número de AS como um ASN de emparelhamento, não um ASN de cliente.</span><span class="sxs-lookup"><span data-stu-id="dcc14-203">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  >

### <a name="tooview-azure-public-peering-details"></a><span data-ttu-id="dcc14-204">tooview público emparelhamento detalhes do Azure</span><span class="sxs-lookup"><span data-stu-id="dcc14-204">tooview Azure public peering details</span></span>

<span data-ttu-id="dcc14-205">Você pode obter os detalhes de configuração usando Olá cmdlet a seguir:</span><span class="sxs-lookup"><span data-stu-id="dcc14-205">You can get configuration details using hello following cmdlet:</span></span>

```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

  Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt
  ```

### <a name="tooupdate-azure-public-peering-configuration"></a><span data-ttu-id="dcc14-206">tooupdate configuração de emparelhamento pública do Azure</span><span class="sxs-lookup"><span data-stu-id="dcc14-206">tooupdate Azure public peering configuration</span></span>

<span data-ttu-id="dcc14-207">Você pode atualizar qualquer parte da configuração de saudação usando Olá exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="dcc14-207">You can update any part of hello configuration using hello following example.</span></span> <span data-ttu-id="dcc14-208">Neste exemplo, Olá VLAN ID de circuito hello está sendo atualizado do too600 200.</span><span class="sxs-lookup"><span data-stu-id="dcc14-208">In this example, hello VLAN ID of hello circuit is being updated from 200 too600.</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 600

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-azure-public-peering"></a><span data-ttu-id="dcc14-209">toodelete emparelhamento público do Azure</span><span class="sxs-lookup"><span data-stu-id="dcc14-209">toodelete Azure public peering</span></span>

<span data-ttu-id="dcc14-210">Você pode remover a configuração do emparelhamento executando Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="dcc14-210">You can remove your peering configuration by running hello following example:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="microsoft-peering"></a><span data-ttu-id="dcc14-211">Emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="dcc14-211">Microsoft peering</span></span>

<span data-ttu-id="dcc14-212">Esta seção ajuda você a criar, obter, atualizar e excluir a configuração de emparelhamento Microsoft hello por um circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="dcc14-212">This section helps you create, get, update, and delete hello Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dcc14-213">Emparelhamento da Microsoft de circuitos ExpressRoute que foram configurados anterior tooAugust 1, 2017 terá todos os prefixos de serviço anunciados através do emparelhamento da Microsoft hello, mesmo se os filtros de roteamento não estão definidos.</span><span class="sxs-lookup"><span data-stu-id="dcc14-213">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through hello Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="dcc14-214">Emparelhamento da Microsoft de circuitos de rota expressa configurados em ou após 1 de agosto de 2017 não terá quaisquer prefixos anunciados até que um filtro de rota é anexado toohello circuito.</span><span class="sxs-lookup"><span data-stu-id="dcc14-214">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span> <span data-ttu-id="dcc14-215">Para obter mais informações, consulte [Configurar um filtro de rota para o emparelhamento da Microsoft](how-to-routefilter-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="dcc14-215">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="toocreate-microsoft-peering"></a><span data-ttu-id="dcc14-216">toocreate emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="dcc14-216">toocreate Microsoft peering</span></span>

1. <span data-ttu-id="dcc14-217">Importe o módulo do PowerShell de saudação do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="dcc14-217">Import hello PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="dcc14-218">Você deve instalar o instalador do PowerShell mais recente saudação do [Galeria do PowerShell](http://www.powershellgallery.com/) e importar os módulos do Azure Resource Manager Olá na sessão do PowerShell Olá em ordem toostart usando os cmdlets de rota expressa hello.</span><span class="sxs-lookup"><span data-stu-id="dcc14-218">You must install hello latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import hello Azure Resource Manager modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="dcc14-219">Você precisará toorun PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="dcc14-219">You will need toorun PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
  ```

  <span data-ttu-id="dcc14-220">Importe todos os módulos AzureRM.* Olá Olá conhecido intervalo de versão semântico.</span><span class="sxs-lookup"><span data-stu-id="dcc14-220">Import all of hello AzureRM.* modules within hello known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="dcc14-221">Você também pode importar um módulo selecione Olá conhecido intervalo de versão semântico.</span><span class="sxs-lookup"><span data-stu-id="dcc14-221">You can also just import a select module within hello known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network
  ```

  <span data-ttu-id="dcc14-222">Entre na conta de tooyour.</span><span class="sxs-lookup"><span data-stu-id="dcc14-222">Sign in tooyour account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="dcc14-223">Selecione a assinatura de saudação desejado toocreate circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="dcc14-223">Select hello subscription you want toocreate ExpressRoute circuit.</span></span>

  ```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="dcc14-224">Criar um circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="dcc14-224">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="dcc14-225">Siga Olá instruções toocreate um [circuito de rota expressa](expressroute-howto-circuit-arm.md) e fornecidos pelo provedor de conectividade de saudação.</span><span class="sxs-lookup"><span data-stu-id="dcc14-225">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="dcc14-226">Se seu provedor de conectividade oferece serviços gerenciados de camada 3, você pode solicitar sua tooenable de provedor de conectividade Azure privado de emparelhamento para você.</span><span class="sxs-lookup"><span data-stu-id="dcc14-226">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="dcc14-227">Nesse caso, você não precisará toofollow instruções listadas nas seções próximas hello.</span><span class="sxs-lookup"><span data-stu-id="dcc14-227">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="dcc14-228">No entanto, se seu provedor de conectividade não gerencia o roteamento para você, depois de criar o circuito, continue a configuração usando as próximas etapas hello.</span><span class="sxs-lookup"><span data-stu-id="dcc14-228">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="dcc14-229">Verifique toomake de circuito de rota expressa de saudação se ele está configurado e também está habilitado.</span><span class="sxs-lookup"><span data-stu-id="dcc14-229">Check hello ExpressRoute circuit toomake sure it is provisioned and also enabled.</span></span> <span data-ttu-id="dcc14-230">Use Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="dcc14-230">Use hello following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="dcc14-231">resposta de saudação é semelhante toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="dcc14-231">hello response is similar toohello following example:</span></span>

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                       "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. <span data-ttu-id="dcc14-232">Configure o emparelhamento do circuito de saudação do Microsoft.</span><span class="sxs-lookup"><span data-stu-id="dcc14-232">Configure Microsoft peering for hello circuit.</span></span> <span data-ttu-id="dcc14-233">Certifique-se de que você tenha Olá seguintes informações antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="dcc14-233">Make sure that you have hello following information before you proceed.</span></span>

  * <span data-ttu-id="dcc14-234">Um /30 sub-rede para o link primário hello.</span><span class="sxs-lookup"><span data-stu-id="dcc14-234">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="dcc14-235">Este valor deve ser um prefixo IPv4 público válido próprio e registrado em um RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="dcc14-235">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="dcc14-236">Um /30 sub-rede para o link secundário hello.</span><span class="sxs-lookup"><span data-stu-id="dcc14-236">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="dcc14-237">Este valor deve ser um prefixo IPv4 público válido próprio e registrado em um RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="dcc14-237">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="dcc14-238">Um tooestablish de ID de VLAN válida esse emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="dcc14-238">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="dcc14-239">Certifique-se de que nenhum outro emparelhamento no circuito de saudação usa Olá a mesma ID de VLAN.</span><span class="sxs-lookup"><span data-stu-id="dcc14-239">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="dcc14-240">Número de AS para emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="dcc14-240">AS number for peering.</span></span> <span data-ttu-id="dcc14-241">Você pode usar um número de AS de 2 e de 4 bytes.</span><span class="sxs-lookup"><span data-stu-id="dcc14-241">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="dcc14-242">Anunciado prefixos: você deve fornecer uma lista de todos os prefixos planejar tooadvertise sobre a sessão BGP de saudação.</span><span class="sxs-lookup"><span data-stu-id="dcc14-242">Advertised prefixes: You must provide a list of all prefixes you plan tooadvertise over hello BGP session.</span></span> <span data-ttu-id="dcc14-243">Somente prefixos de endereços IP públicos são aceitos.</span><span class="sxs-lookup"><span data-stu-id="dcc14-243">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="dcc14-244">Se você planejar toosend um conjunto de prefixos, você pode enviar uma lista separada por vírgulas.</span><span class="sxs-lookup"><span data-stu-id="dcc14-244">If you plan toosend a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="dcc14-245">Esses prefixos devem ser registrado tooyou em um RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="dcc14-245">These prefixes must be registered tooyou in an RIR / IRR.</span></span>
  * <span data-ttu-id="dcc14-246">**Opcional -** cliente ASN: se você estiver prefixos de anúncios que não são registrado toohello emparelhamento como número, você pode especificar hello como número toowhich, eles são registrados.</span><span class="sxs-lookup"><span data-stu-id="dcc14-246">**Optional -** Customer ASN: If you are advertising prefixes that are not registered toohello peering AS number, you can specify hello AS number toowhich they are registered.</span></span>
  * <span data-ttu-id="dcc14-247">Nome de roteamento do registro: Você pode especificar Olá RIR / IRR no qual hello como número e prefixos estão registrados.</span><span class="sxs-lookup"><span data-stu-id="dcc14-247">Routing Registry Name: You can specify hello RIR / IRR against which hello AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="dcc14-248">**Opcional -** um hash MD5 se você escolher toouse um.</span><span class="sxs-lookup"><span data-stu-id="dcc14-248">**Optional -** An MD5 hash if you choose toouse one.</span></span>

   <span data-ttu-id="dcc14-249">Use Olá exemplo tooconfigure emparelhamento da Microsoft para o circuito a seguir:</span><span class="sxs-lookup"><span data-stu-id="dcc14-249">Use hello following example tooconfigure Microsoft peering for your circuit:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "123.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

### <a name="tooget-microsoft-peering-details"></a><span data-ttu-id="dcc14-250">tooget detalhes de emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="dcc14-250">tooget Microsoft peering details</span></span>

<span data-ttu-id="dcc14-251">Você pode obter os detalhes de configuração usando Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="dcc14-251">You can get configuration details using hello following example:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt
```

### <a name="tooupdate-microsoft-peering-configuration"></a><span data-ttu-id="dcc14-252">tooupdate configuração de emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="dcc14-252">tooupdate Microsoft peering configuration</span></span>

<span data-ttu-id="dcc14-253">Você pode atualizar qualquer parte da configuração de saudação usando Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="dcc14-253">You can update any part of hello configuration using hello following example:</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "124.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-microsoft-peering"></a><span data-ttu-id="dcc14-254">toodelete emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="dcc14-254">toodelete Microsoft peering</span></span>

<span data-ttu-id="dcc14-255">Você pode remover a configuração do emparelhamento executando Olá cmdlet a seguir:</span><span class="sxs-lookup"><span data-stu-id="dcc14-255">You can remove your peering configuration by running hello following cmdlet:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="next-steps"></a><span data-ttu-id="dcc14-256">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dcc14-256">Next steps</span></span>

<span data-ttu-id="dcc14-257">Próxima etapa, [vincular um circuito de rota expressa do tooan de VNet](expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="dcc14-257">Next step, [Link a VNet tooan ExpressRoute circuit](expressroute-howto-linkvnet-arm.md).</span></span>

* <span data-ttu-id="dcc14-258">Para saber mais sobre fluxos de trabalho do ExpressRoute, confira [Fluxos de trabalho do ExpressRoute](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="dcc14-258">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="dcc14-259">Para obter mais informações sobre o emparelhamento de circuito, veja [Circuitos e domínios de roteamento do ExpressRoute](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="dcc14-259">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="dcc14-260">Para saber mais sobre redes virtuais, confira [Visão geral da rede virtual](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dcc14-260">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>
