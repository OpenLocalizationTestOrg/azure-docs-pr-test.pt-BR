---
title: 'Como configurar o roteamento (emparelhamento) para um circuito do ExpressRoute: Resource Manager: PowerShell: Azure | Microsoft Docs'
description: "Este artigo fornece uma orientação sobre as etapas de criação e de provisionamento do emparelhamento público, privado e da Microsoft de um circuito do ExpressRoute. Este artigo também mostra como verificar o status, atualizar ou excluir emparelhamentos de seu circuito."
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
ms.openlocfilehash: af68955b78239832e413e1b59e033d7d3da8d599
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-using-powershell"></a><span data-ttu-id="9d7a1-104">Criar e modificar o emparelhamento de um circuito do ExpressRoute usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="9d7a1-104">Create and modify peering for an ExpressRoute circuit using PowerShell</span></span>

<span data-ttu-id="9d7a1-105">Esse artigo ajuda você a criar e gerenciar a configuração de roteamento de um circuito do ExpressRoute no modelo de implantação do Resource Manager usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in the Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="9d7a1-106">Você também pode verificar o status, atualizar ou excluir e desprovisionar emparelhamentos de um circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-106">You can also check the status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="9d7a1-107">Se quiser usar um método diferente para trabalhar com seu circuito, selecione um artigo na lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="9d7a1-107">If you want to use a different method to work with your circuit, select an article from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9d7a1-108">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="9d7a1-108">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="9d7a1-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9d7a1-109">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="9d7a1-110">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="9d7a1-110">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="9d7a1-111">Vídeo – Emparelhamento privado</span><span class="sxs-lookup"><span data-stu-id="9d7a1-111">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="9d7a1-112">Vídeo – Emparelhamento público</span><span class="sxs-lookup"><span data-stu-id="9d7a1-112">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="9d7a1-113">Vídeo – Emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="9d7a1-113">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="9d7a1-114">PowerShell (clássico)</span><span class="sxs-lookup"><span data-stu-id="9d7a1-114">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="9d7a1-115">Pré-requisitos de configuração</span><span class="sxs-lookup"><span data-stu-id="9d7a1-115">Configuration prerequisites</span></span>

* <span data-ttu-id="9d7a1-116">Você precisará da versão mais recente dos cmdlets do PowerShell do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-116">You will need the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="9d7a1-117">Para saber mais, consulte [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview):</span><span class="sxs-lookup"><span data-stu-id="9d7a1-117">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> 
* <span data-ttu-id="9d7a1-118">Verifique se você leu a página de [pré-requisitos](expressroute-prerequisites.md), a página de [requisitos do roteamento](expressroute-routing.md) e a página [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-118">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md) page, the [routing requirements](expressroute-routing.md) page, and the [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="9d7a1-119">Você deve ter um circuito do ExpressRoute ativo.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="9d7a1-120">Antes de continuar, siga as instruções para [criar um circuito do ExpressRoute](expressroute-howto-circuit-arm.md) e para que o circuito seja habilitado pelo provedor de conectividade.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-120">Follow the instructions to [Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="9d7a1-121">O circuito do ExpressRoute deve estar em um estado provisionado e habilitado para que você possa executar os cmdlets neste artigo.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-121">The ExpressRoute circuit must be in a provisioned and enabled state for you to be able to run the cmdlets in this article.</span></span>

<span data-ttu-id="9d7a1-122">Estas instruções se aplicam apenas a circuitos criados com provedores de serviço que oferecem serviços de conectividade de Camada 2.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-122">These instructions only apply to circuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="9d7a1-123">Se você estiver usando um provedor de serviços que ofereça serviços gerenciados de Camada 3 (normalmente um IPVPN, como MPLS), seu provedor de conectividade configurará e gerenciará o roteamento para você.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-123">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9d7a1-124">Atualmente, não anunciamos emparelhamentos configurados pelos provedores de serviço por meio do portal de gerenciamento de serviço.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-124">We currently do not advertise peerings configured by service providers through the service management portal.</span></span> <span data-ttu-id="9d7a1-125">Estamos trabalhando para habilitar esse recurso em breve.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-125">We are working on enabling this capability soon.</span></span> <span data-ttu-id="9d7a1-126">Verifique com seu provedor de serviços antes de configurar os emparelhamentos via protocolo BGP.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-126">Check with your service provider before configuring BGP peerings.</span></span>
> 
> 

<span data-ttu-id="9d7a1-127">Você pode configurar um, dois ou todos os três emparelhamentos (privado e público do Azure e da Microsoft) para um circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-127">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="9d7a1-128">Você pode configurar emparelhamentos em qualquer ordem escolhida.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-128">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="9d7a1-129">No entanto, você deve concluir a configuração de um emparelhamento por vez.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-129">However, you must make sure that you complete the configuration of each peering one at a time.</span></span> 

## <a name="azure-private-peering"></a><span data-ttu-id="9d7a1-130">Emparelhamento privado do Azure</span><span class="sxs-lookup"><span data-stu-id="9d7a1-130">Azure private peering</span></span>

<span data-ttu-id="9d7a1-131">Esta seção ajuda você a criar, obter, atualizar e excluir a configuração de emparelhamento privado do Azure para um circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-131">This section helps you create, get, update, and delete the Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-private-peering"></a><span data-ttu-id="9d7a1-132">Criar um emparelhamento privado do Azure</span><span class="sxs-lookup"><span data-stu-id="9d7a1-132">To create Azure private peering</span></span>

1. <span data-ttu-id="9d7a1-133">Importe o módulo do PowerShell para ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-133">Import the PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="9d7a1-134">Instale o instalador do PowerShell mais recente da [Galeria do PowerShell](http://www.powershellgallery.com/) e importe os módulos do Gerenciador de Recursos do Azure na sessão do PowerShell para começar a usar os cmdlets do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-134">You must install the latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import the Azure Resource Manager modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="9d7a1-135">Você precisará executar o PowerShell como Administrador.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-135">You will need to run PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM
  Install-AzureRM
  ```

  <span data-ttu-id="9d7a1-136">Importe todos os módulos AzureRM.* dentro do intervalo de versão semântico conhecido.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-136">Import all of the AzureRM.* modules within the known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="9d7a1-137">Você também pode importar apenas um módulo selecionado dentro do intervalo de versão semântico conhecido.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-137">You can also just import a select module within the known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network 
  ```

  <span data-ttu-id="9d7a1-138">Entre na sua conta.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-138">Sign in to your account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="9d7a1-139">Selecionar a assinatura na qual você deseja criar um circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-139">Select the subscription you want to create ExpressRoute circuit.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="9d7a1-140">Criar um circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-140">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="9d7a1-141">Siga as instruções para criar um [circuito do ExpressRoute](expressroute-howto-circuit-arm.md) e para que o circuito seja provisionado pelo provedor de conectividade.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-141">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by the connectivity provider.</span></span>

  <span data-ttu-id="9d7a1-142">Caso seu provedor de conectividade ofereça serviços gerenciados de camada 3, solicite a ele a habilitação do emparelhamento privado do Azure.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-142">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="9d7a1-143">Nesse caso, não será necessário seguir as instruções listadas nas seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-143">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="9d7a1-144">No entanto, se o seu provedor de conectividade não gerenciar o roteamento, após a criação do circuito, continue a configuração executando as próximas etapas.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-144">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>
3. <span data-ttu-id="9d7a1-145">Verifique se o circuito do ExpressRoute está provisionado e habilitado.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-145">Check the ExpressRoute circuit to make sure it is provisioned and also enabled.</span></span> <span data-ttu-id="9d7a1-146">Use o seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="9d7a1-146">Use the following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="9d7a1-147">A resposta é semelhante ao seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="9d7a1-147">The response is similar to the following example:</span></span>

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
4. <span data-ttu-id="9d7a1-148">Configure o emparelhamento privado do Azure para o circuito.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-148">Configure Azure private peering for the circuit.</span></span> <span data-ttu-id="9d7a1-149">Verifique se você tem os seguintes itens antes de continuar com as próximas etapas:</span><span class="sxs-lookup"><span data-stu-id="9d7a1-149">Make sure that you have the following items before you proceed with the next steps:</span></span>

  * <span data-ttu-id="9d7a1-150">Uma sub-rede /30 para o link principal.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-150">A /30 subnet for the primary link.</span></span> <span data-ttu-id="9d7a1-151">A sub-rede não deve fazer parte de nenhum espaço de endereçamento reservado para redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-151">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="9d7a1-152">Uma sub-rede /30 para o link secundário.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-152">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="9d7a1-153">A sub-rede não deve fazer parte de nenhum espaço de endereçamento reservado para redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-153">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="9d7a1-154">Uma ID válida de VLAN para estabelecer esse emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-154">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="9d7a1-155">Verifique se nenhum outro emparelhamento no circuito usa a mesma ID de VLAN.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-155">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="9d7a1-156">Número de AS para emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-156">AS number for peering.</span></span> <span data-ttu-id="9d7a1-157">Você pode usar um número de AS de 2 e de 4 bytes.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-157">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="9d7a1-158">Você pode usar um número de AS privado para esse emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-158">You can use a private AS number for this peering.</span></span> <span data-ttu-id="9d7a1-159">Não use 65515.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-159">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="9d7a1-160">**Opcional –** Um hash MD5 se você optar por usar um.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-160">**Optional -** An MD5 hash if you choose to use one.</span></span>

  <span data-ttu-id="9d7a1-161">Use o seguinte exemplo para configurar o emparelhamento privado do Azure para seu circuito:</span><span class="sxs-lookup"><span data-stu-id="9d7a1-161">Use the following example to configure Azure private peering for your circuit:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  <span data-ttu-id="9d7a1-162">Se você optar por usar um hash MD5, use o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="9d7a1-162">If you choose to use an MD5 hash, use the following example:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200  -SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="9d7a1-163">Especifique o número de AS como um ASN de emparelhamento, não um ASN de cliente.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-163">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  >

### <a name="to-view-azure-private-peering-details"></a><span data-ttu-id="9d7a1-164">Para exibir detalhes sobre o emparelhamento privado do Azure</span><span class="sxs-lookup"><span data-stu-id="9d7a1-164">To view Azure private peering details</span></span>

<span data-ttu-id="9d7a1-165">Você pode obter detalhes de configuração usando o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="9d7a1-165">You can get configuration details by using the following example:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt
```

### <a name="to-update-azure-private-peering-configuration"></a><span data-ttu-id="9d7a1-166">Atualizar a configuração de emparelhamento privado do Azure</span><span class="sxs-lookup"><span data-stu-id="9d7a1-166">To update Azure private peering configuration</span></span>

<span data-ttu-id="9d7a1-167">Você pode atualizar qualquer parte da configuração usando o exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-167">You can update any part of the configuration using the following example.</span></span> <span data-ttu-id="9d7a1-168">Neste exemplo, a ID da VLAN do circuito está sendo atualizada de 100 para 500.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-168">In this example, the VLAN ID of the circuit is being updated from 100 to 500.</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="to-delete-azure-private-peering"></a><span data-ttu-id="9d7a1-169">Excluir um emparelhamento privado do Azure</span><span class="sxs-lookup"><span data-stu-id="9d7a1-169">To delete Azure private peering</span></span>

<span data-ttu-id="9d7a1-170">Você pode remover a configuração de emparelhamento executando o seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="9d7a1-170">You can remove your peering configuration by running the following example:</span></span>

> [!WARNING]
> <span data-ttu-id="9d7a1-171">Verifique se todas as redes virtuais estão desvinculadas do circuito do ExpressRoute antes de executar esse exemplo.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-171">You must ensure that all virtual networks are unlinked from the ExpressRoute circuit before running this example.</span></span> 
> 
> 

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="azure-public-peering"></a><span data-ttu-id="9d7a1-172">Emparelhamento público do Azure</span><span class="sxs-lookup"><span data-stu-id="9d7a1-172">Azure public peering</span></span>

<span data-ttu-id="9d7a1-173">Esta seção ajuda você a criar, obter, atualizar e excluir a configuração de emparelhamento público do Azure para um circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-173">This section helps you create, get, update, and delete the Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-public-peering"></a><span data-ttu-id="9d7a1-174">Criar o emparelhamento público do Azure</span><span class="sxs-lookup"><span data-stu-id="9d7a1-174">To create Azure public peering</span></span>

1. <span data-ttu-id="9d7a1-175">Importe o módulo do PowerShell para ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-175">Import the PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="9d7a1-176">Instale o instalador do PowerShell mais recente da [Galeria do PowerShell](http://www.powershellgallery.com/) e importe os módulos do Gerenciador de Recursos do Azure na sessão do PowerShell para começar a usar os cmdlets do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-176">You must install the latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import the Azure Resource Manager modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="9d7a1-177">Você precisará executar o PowerShell como Administrador.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-177">You will need to run PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
```

  <span data-ttu-id="9d7a1-178">Importe todos os módulos AzureRM.* dentro do intervalo de versão semântico conhecido.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-178">Import all of the AzureRM.* modules within the known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="9d7a1-179">Você também pode importar apenas um módulo selecionado dentro do intervalo de versão semântico conhecido.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-179">You can also just import a select module within the known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network
```

  <span data-ttu-id="9d7a1-180">Entre na sua conta.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-180">Sign in to your account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="9d7a1-181">Selecionar a assinatura na qual você deseja criar um circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-181">Select the subscription you want to create ExpressRoute circuit.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="9d7a1-182">Criar um circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-182">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="9d7a1-183">Siga as instruções para criar um [circuito do ExpressRoute](expressroute-howto-circuit-arm.md) e para que o circuito seja provisionado pelo provedor de conectividade.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-183">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by the connectivity provider.</span></span>

  <span data-ttu-id="9d7a1-184">Caso seu provedor de conectividade ofereça serviços gerenciados de camada 3, solicite a ele a habilitação do emparelhamento privado do Azure.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-184">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="9d7a1-185">Nesse caso, não será necessário seguir as instruções listadas nas seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-185">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="9d7a1-186">No entanto, se o seu provedor de conectividade não gerenciar o roteamento, após a criação do circuito, continue a configuração executando as próximas etapas.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-186">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>
3. <span data-ttu-id="9d7a1-187">Verifique se o circuito do ExpressRoute está provisionado e habilitado.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-187">Check the ExpressRoute circuit to ensure it is provisioned and also enabled.</span></span> <span data-ttu-id="9d7a1-188">Use o seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="9d7a1-188">Use the following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="9d7a1-189">A resposta é semelhante ao seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="9d7a1-189">The response is similar to the following example:</span></span>

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
4. <span data-ttu-id="9d7a1-190">Configure o emparelhamento público do Azure para o circuito.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-190">Configure Azure public peering for the circuit.</span></span> <span data-ttu-id="9d7a1-191">Verifique se você tem as informações a seguir antes de prosseguir.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-191">Make sure that you have the following information before you proceed further.</span></span>

  * <span data-ttu-id="9d7a1-192">Uma sub-rede /30 para o link principal.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-192">A /30 subnet for the primary link.</span></span> <span data-ttu-id="9d7a1-193">Precisa ser um prefixo IPv4 público válido.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-193">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="9d7a1-194">Uma sub-rede /30 para o link secundário.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-194">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="9d7a1-195">Precisa ser um prefixo IPv4 público válido.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-195">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="9d7a1-196">Uma ID válida de VLAN para estabelecer esse emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-196">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="9d7a1-197">Verifique se nenhum outro emparelhamento no circuito usa a mesma ID de VLAN.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-197">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="9d7a1-198">Número de AS para emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-198">AS number for peering.</span></span> <span data-ttu-id="9d7a1-199">Você pode usar um número de AS de 2 e de 4 bytes.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-199">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="9d7a1-200">**Opcional –** Um hash MD5 se você optar por usar um.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-200">**Optional -** An MD5 hash if you choose to use one.</span></span>

  <span data-ttu-id="9d7a1-201">Executar o seguinte exemplo para configurar o emparelhamento público do Azure para seu circuito</span><span class="sxs-lookup"><span data-stu-id="9d7a1-201">Run the following example to configure Azure public peering for your circuit</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  <span data-ttu-id="9d7a1-202">Se você optar por usar um hash MD5, use o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="9d7a1-202">If you choose to use an MD5 hash, use the following example:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100  -SharedKey "A1B2C3D4"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="9d7a1-203">Especifique o número de AS como um ASN de emparelhamento, não um ASN de cliente.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-203">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  >

### <a name="to-view-azure-public-peering-details"></a><span data-ttu-id="9d7a1-204">Para exibir detalhes sobre o emparelhamento público do Azure</span><span class="sxs-lookup"><span data-stu-id="9d7a1-204">To view Azure public peering details</span></span>

<span data-ttu-id="9d7a1-205">Você pode obter detalhes de configuração usando o seguinte cmdlet:</span><span class="sxs-lookup"><span data-stu-id="9d7a1-205">You can get configuration details using the following cmdlet:</span></span>

```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

  Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt
  ```

### <a name="to-update-azure-public-peering-configuration"></a><span data-ttu-id="9d7a1-206">Atualizar a configuração de emparelhamento público do Azure</span><span class="sxs-lookup"><span data-stu-id="9d7a1-206">To update Azure public peering configuration</span></span>

<span data-ttu-id="9d7a1-207">Você pode atualizar qualquer parte da configuração usando o exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-207">You can update any part of the configuration using the following example.</span></span> <span data-ttu-id="9d7a1-208">Neste exemplo, a ID da VLAN do circuito está sendo atualizada de 200 para 600.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-208">In this example, the VLAN ID of the circuit is being updated from 200 to 600.</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 600

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="to-delete-azure-public-peering"></a><span data-ttu-id="9d7a1-209">Excluir o emparelhamento público do Azure</span><span class="sxs-lookup"><span data-stu-id="9d7a1-209">To delete Azure public peering</span></span>

<span data-ttu-id="9d7a1-210">Você pode remover a configuração de emparelhamento executando o seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="9d7a1-210">You can remove your peering configuration by running the following example:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="microsoft-peering"></a><span data-ttu-id="9d7a1-211">Emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="9d7a1-211">Microsoft peering</span></span>

<span data-ttu-id="9d7a1-212">Esta seção ajuda você a criar, obter, atualizar e excluir a configuração de emparelhamento da Microsoft para um circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-212">This section helps you create, get, update, and delete the Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9d7a1-213">O emparelhamento da Microsoft de circuitos do ExpressRoute configurados antes de 1º de agosto de 2017 terá todos os prefixos de serviço anunciados através do emparelhamento da Microsoft, mesmo que os filtros de rota não estejam definidos.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-213">Microsoft peering of ExpressRoute circuits that were configured prior to August 1, 2017 will have all service prefixes advertised through the Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="9d7a1-214">O emparelhamento da Microsoft de circuitos de ExpressRoute configurados em ou após 1º de agosto de 2017 não terá nenhum prefixo anunciado até que um filtro de rota seja anexado ao circuito.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-214">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached to the circuit.</span></span> <span data-ttu-id="9d7a1-215">Para obter mais informações, consulte [Configurar um filtro de rota para o emparelhamento da Microsoft](how-to-routefilter-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="9d7a1-215">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="to-create-microsoft-peering"></a><span data-ttu-id="9d7a1-216">Criar emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="9d7a1-216">To create Microsoft peering</span></span>

1. <span data-ttu-id="9d7a1-217">Importe o módulo do PowerShell para ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-217">Import the PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="9d7a1-218">Instale o instalador do PowerShell mais recente da [Galeria do PowerShell](http://www.powershellgallery.com/) e importe os módulos do Gerenciador de Recursos do Azure na sessão do PowerShell para começar a usar os cmdlets do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-218">You must install the latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import the Azure Resource Manager modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="9d7a1-219">Você precisará executar o PowerShell como Administrador.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-219">You will need to run PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
  ```

  <span data-ttu-id="9d7a1-220">Importe todos os módulos AzureRM.* dentro do intervalo de versão semântico conhecido.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-220">Import all of the AzureRM.* modules within the known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="9d7a1-221">Você também pode importar apenas um módulo selecionado dentro do intervalo de versão semântico conhecido.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-221">You can also just import a select module within the known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network
  ```

  <span data-ttu-id="9d7a1-222">Entre na sua conta.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-222">Sign in to your account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="9d7a1-223">Selecionar a assinatura na qual você deseja criar um circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-223">Select the subscription you want to create ExpressRoute circuit.</span></span>

  ```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="9d7a1-224">Criar um circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-224">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="9d7a1-225">Siga as instruções para criar um [circuito do ExpressRoute](expressroute-howto-circuit-arm.md) e para que o circuito seja provisionado pelo provedor de conectividade.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-225">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by the connectivity provider.</span></span>

  <span data-ttu-id="9d7a1-226">Caso seu provedor de conectividade ofereça serviços gerenciados de camada 3, solicite a ele a habilitação do emparelhamento privado do Azure.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-226">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="9d7a1-227">Nesse caso, não será necessário seguir as instruções listadas nas seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-227">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="9d7a1-228">No entanto, se o seu provedor de conectividade não gerenciar o roteamento, após a criação do circuito, continue a configuração executando as próximas etapas.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-228">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>
3. <span data-ttu-id="9d7a1-229">Verifique se o circuito do ExpressRoute está provisionado e habilitado.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-229">Check the ExpressRoute circuit to make sure it is provisioned and also enabled.</span></span> <span data-ttu-id="9d7a1-230">Use o seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="9d7a1-230">Use the following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="9d7a1-231">A resposta é semelhante ao seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="9d7a1-231">The response is similar to the following example:</span></span>

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
4. <span data-ttu-id="9d7a1-232">Configurar o emparelhamento da Microsoft para o circuito.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-232">Configure Microsoft peering for the circuit.</span></span> <span data-ttu-id="9d7a1-233">Você precisa ter as seguintes informações antes de continuar:</span><span class="sxs-lookup"><span data-stu-id="9d7a1-233">Make sure that you have the following information before you proceed.</span></span>

  * <span data-ttu-id="9d7a1-234">Uma sub-rede /30 para o link principal.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-234">A /30 subnet for the primary link.</span></span> <span data-ttu-id="9d7a1-235">Este valor deve ser um prefixo IPv4 público válido próprio e registrado em um RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-235">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="9d7a1-236">Uma sub-rede /30 para o link secundário.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-236">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="9d7a1-237">Este valor deve ser um prefixo IPv4 público válido próprio e registrado em um RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-237">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="9d7a1-238">Uma ID válida de VLAN para estabelecer esse emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-238">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="9d7a1-239">Verifique se nenhum outro emparelhamento no circuito usa a mesma ID de VLAN.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-239">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="9d7a1-240">Número de AS para emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-240">AS number for peering.</span></span> <span data-ttu-id="9d7a1-241">Você pode usar um número de AS de 2 e de 4 bytes.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-241">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="9d7a1-242">Prefixos anunciados: forneça uma lista com todos os prefixos que você pretende anunciar na sessão BGP.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-242">Advertised prefixes: You must provide a list of all prefixes you plan to advertise over the BGP session.</span></span> <span data-ttu-id="9d7a1-243">Somente prefixos de endereços IP públicos são aceitos.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-243">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="9d7a1-244">Caso você planeje enviar um conjunto de prefixos, poderá enviar uma lista separada por vírgulas.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-244">If you plan to send a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="9d7a1-245">Esses prefixos devem ser registrados em seu nome em um RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-245">These prefixes must be registered to you in an RIR / IRR.</span></span>
  * <span data-ttu-id="9d7a1-246">**Opcional –** ASN de cliente: se você estiver anunciando prefixos não registrados com o número AS de emparelhamento, especifique o número AS com o qual eles estão registrados.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-246">**Optional -** Customer ASN: If you are advertising prefixes that are not registered to the peering AS number, you can specify the AS number to which they are registered.</span></span>
  * <span data-ttu-id="9d7a1-247">Nome do registro de roteamento: você pode especificar o RIR/IRR com base no qual o número de AS e os prefixos estão registrados.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-247">Routing Registry Name: You can specify the RIR / IRR against which the AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="9d7a1-248">**Opcional –** Um hash MD5 se você optar por usar um.</span><span class="sxs-lookup"><span data-stu-id="9d7a1-248">**Optional -** An MD5 hash if you choose to use one.</span></span>

   <span data-ttu-id="9d7a1-249">Use o exemplo a seguir para configurar o emparelhamento da Microsoft para seu circuito:</span><span class="sxs-lookup"><span data-stu-id="9d7a1-249">Use the following example to configure Microsoft peering for your circuit:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "123.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

### <a name="to-get-microsoft-peering-details"></a><span data-ttu-id="9d7a1-250">Obter detalhes de emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="9d7a1-250">To get Microsoft peering details</span></span>

<span data-ttu-id="9d7a1-251">Você pode obter detalhes de configuração usando o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="9d7a1-251">You can get configuration details using the following example:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt
```

### <a name="to-update-microsoft-peering-configuration"></a><span data-ttu-id="9d7a1-252">Atualizar a configuração de emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="9d7a1-252">To update Microsoft peering configuration</span></span>

<span data-ttu-id="9d7a1-253">Você pode atualizar qualquer parte da configuração usando o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="9d7a1-253">You can update any part of the configuration using the following example:</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "124.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="to-delete-microsoft-peering"></a><span data-ttu-id="9d7a1-254">Excluir emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="9d7a1-254">To delete Microsoft peering</span></span>

<span data-ttu-id="9d7a1-255">Você pode remover a configuração de emparelhamento executando o seguinte cmdlet:</span><span class="sxs-lookup"><span data-stu-id="9d7a1-255">You can remove your peering configuration by running the following cmdlet:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="next-steps"></a><span data-ttu-id="9d7a1-256">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9d7a1-256">Next steps</span></span>

<span data-ttu-id="9d7a1-257">A próxima etapa será [Vincular uma Rede Virtual a um circuito do ExpressRoute](expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="9d7a1-257">Next step, [Link a VNet to an ExpressRoute circuit](expressroute-howto-linkvnet-arm.md).</span></span>

* <span data-ttu-id="9d7a1-258">Para saber mais sobre fluxos de trabalho do ExpressRoute, confira [Fluxos de trabalho do ExpressRoute](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="9d7a1-258">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="9d7a1-259">Para obter mais informações sobre o emparelhamento de circuito, veja [Circuitos e domínios de roteamento do ExpressRoute](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="9d7a1-259">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="9d7a1-260">Para saber mais sobre redes virtuais, confira [Visão geral da rede virtual](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9d7a1-260">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>
