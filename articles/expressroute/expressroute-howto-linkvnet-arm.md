---
title: 'Vincular uma rede virtual a um circuito ExpressRoute: PowerShell: Azure| Microsoft Docs'
description: "Este documento fornece uma visão geral de como vincular as redes virtuais (VNets) aos circuitos de ExpressRoute usando o modelo de implantação do Gerenciador de Recursos e do PowerShell."
services: expressroute
documentationcenter: na
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: daacb6e5-705a-456f-9a03-c4fc3f8c1f7e
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: ganesr
ms.openlocfilehash: 8c2f3036f754a98090ab860f95900416690ebf83
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-a-virtual-network-to-an-expressroute-circuit"></a><span data-ttu-id="93ebb-103">Conectar uma rede virtual a um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="93ebb-103">Connect a virtual network to an ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="93ebb-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="93ebb-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="93ebb-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="93ebb-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="93ebb-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="93ebb-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="93ebb-107">Vídeo – Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="93ebb-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="93ebb-108">PowerShell (clássico)</span><span class="sxs-lookup"><span data-stu-id="93ebb-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
>

<span data-ttu-id="93ebb-109">Este artigo ajuda a vincular as VNets (redes virtuais) aos circuitos do Azure ExpressRoute usando o modelo de implantação do Resource Manager e PowerShell.</span><span class="sxs-lookup"><span data-stu-id="93ebb-109">This article helps you link virtual networks (VNets) to Azure ExpressRoute circuits by using the Resource Manager deployment model and PowerShell.</span></span> <span data-ttu-id="93ebb-110">As redes virtuais podem estar na mesma assinatura ou fazer parte de outra assinatura.</span><span class="sxs-lookup"><span data-stu-id="93ebb-110">Virtual networks can either be in the same subscription or part of another subscription.</span></span> <span data-ttu-id="93ebb-111">Este artigo mostra como atualizar um link de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="93ebb-111">This article also shows you how to update a virtual network link.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="93ebb-112">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="93ebb-112">Before you begin</span></span>
* <span data-ttu-id="93ebb-113">Instale a versão mais recente dos módulos do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="93ebb-113">Install the latest version of the Azure PowerShell modules.</span></span> <span data-ttu-id="93ebb-114">Para saber mais, consulte [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview):</span><span class="sxs-lookup"><span data-stu-id="93ebb-114">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="93ebb-115">Analise os [pré-requisitos](expressroute-prerequisites.md), os [requisitos de roteamento](expressroute-routing.md) e os [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração.</span><span class="sxs-lookup"><span data-stu-id="93ebb-115">Review the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="93ebb-116">Você deve ter um circuito do ExpressRoute ativo.</span><span class="sxs-lookup"><span data-stu-id="93ebb-116">You must have an active ExpressRoute circuit.</span></span> 
  * <span data-ttu-id="93ebb-117">Siga as instruções para [criar um circuito do ExpressRoute](expressroute-howto-circuit-arm.md) e para que o circuito seja habilitado pelo provedor de conectividade.</span><span class="sxs-lookup"><span data-stu-id="93ebb-117">Follow the instructions to [create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have the circuit enabled by your connectivity provider.</span></span> 
  * <span data-ttu-id="93ebb-118">Verifique se o emparelhamento privado do Azure está configurado para seu circuito.</span><span class="sxs-lookup"><span data-stu-id="93ebb-118">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="93ebb-119">Veja o artigo [Configurar roteamento](expressroute-howto-routing-arm.md) para obter instruções sobre roteamento.</span><span class="sxs-lookup"><span data-stu-id="93ebb-119">See the [configure routing](expressroute-howto-routing-arm.md) article for routing instructions.</span></span> 
  * <span data-ttu-id="93ebb-120">Verifique se o emparelhamento privado do Azure está configurado e se o emparelhamento BGP entre sua rede e a Microsoft está ativo para que você possa habilitar a conectividade de ponta a ponta.</span><span class="sxs-lookup"><span data-stu-id="93ebb-120">Ensure that Azure private peering is configured and the BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="93ebb-121">Verifique se tem uma rede virtual e um gateway de rede virtual criados e totalmente provisionados.</span><span class="sxs-lookup"><span data-stu-id="93ebb-121">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="93ebb-122">Siga as instruções para [criar um gateway de rede virtual para ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="93ebb-122">Follow the instructions to [create a virtual network gateway for ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="93ebb-123">Um gateway de rede virtual para ExpressRoute usa o GatewayType “ExpressRoute”, não VPN.</span><span class="sxs-lookup"><span data-stu-id="93ebb-123">A virtual network gateway for ExpressRoute uses the GatewayType 'ExpressRoute', not VPN.</span></span>

* <span data-ttu-id="93ebb-124">Você pode vincular até 10 redes virtuais a um circuito de ExpressRoute padrão.</span><span class="sxs-lookup"><span data-stu-id="93ebb-124">You can link up to 10 virtual networks to a standard ExpressRoute circuit.</span></span> <span data-ttu-id="93ebb-125">Todas as redes virtuais deverão estar na mesma região geopolítica ao usar um circuito de ExpressRoute padrão.</span><span class="sxs-lookup"><span data-stu-id="93ebb-125">All virtual networks must be in the same geopolitical region when using a standard ExpressRoute circuit.</span></span> 

* <span data-ttu-id="93ebb-126">Você poderá vincular uma rede virtual fora da região geopolítica do circuito do ExpressRoute ou conectar um grande número de redes virtuais ao circuito de ExpressRoute, se tiver habilitado o complemento premium do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="93ebb-126">You can link a virtual networks outside of the geopolitical region of the ExpressRoute circuit, or connect a larger number of virtual networks to your ExpressRoute circuit if you enabled the ExpressRoute premium add-on.</span></span> <span data-ttu-id="93ebb-127">Confira as [perguntas frequentes](expressroute-faqs.md) para obter mais detalhes sobre o complemento premium.</span><span class="sxs-lookup"><span data-stu-id="93ebb-127">Check the [FAQ](expressroute-faqs.md) for more details on the premium add-on.</span></span>


## <a name="connect-a-virtual-network-in-the-same-subscription-to-a-circuit"></a><span data-ttu-id="93ebb-128">Conectar uma rede virtual na mesma assinatura a um circuito</span><span class="sxs-lookup"><span data-stu-id="93ebb-128">Connect a virtual network in the same subscription to a circuit</span></span>
<span data-ttu-id="93ebb-129">Você pode vincular um gateway de rede virtual a um circuito do ExpressRoute usando o cmdlet a seguir.</span><span class="sxs-lookup"><span data-stu-id="93ebb-129">You can connect a virtual network gateway to an ExpressRoute circuit by using the following cmdlet.</span></span> <span data-ttu-id="93ebb-130">Verifique se o gateway de rede virtual foi criado e se está pronto para vinculação antes de executar o cmdlet:</span><span class="sxs-lookup"><span data-stu-id="93ebb-130">Make sure that the virtual network gateway is created and is ready for linking before you run the cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "MyRG" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $circuit.Id -ConnectionType ExpressRoute
```

## <a name="connect-a-virtual-network-in-a-different-subscription-to-a-circuit"></a><span data-ttu-id="93ebb-131">Conectar uma rede virtual em uma assinatura diferente a um circuito</span><span class="sxs-lookup"><span data-stu-id="93ebb-131">Connect a virtual network in a different subscription to a circuit</span></span>
<span data-ttu-id="93ebb-132">Você pode compartilhar um circuito do ExpressRoute entre várias assinaturas.</span><span class="sxs-lookup"><span data-stu-id="93ebb-132">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="93ebb-133">A figura a seguir mostra um esquema simples de como funciona o compartilhamento de circuitos do ExpressRoute entre várias assinaturas.</span><span class="sxs-lookup"><span data-stu-id="93ebb-133">The following figure shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="93ebb-134">Cada uma das nuvens menores dentro da nuvem grande é usada para representar assinaturas pertencentes a diferentes departamentos dentro de uma organização.</span><span class="sxs-lookup"><span data-stu-id="93ebb-134">Each of the smaller clouds within the large cloud is used to represent subscriptions that belong to different departments within an organization.</span></span> <span data-ttu-id="93ebb-135">Cada um dos departamentos dentro da organização pode usar sua própria assinatura para implantar seus serviços, mas pode compartilhar um único circuito do ExpressRoute para se conectar de volta à respectiva rede local.</span><span class="sxs-lookup"><span data-stu-id="93ebb-135">Each of the departments within the organization can use their own subscription for deploying their services--but they can share a single ExpressRoute circuit to connect back to your on-premises network.</span></span> <span data-ttu-id="93ebb-136">Um único departamento (neste exemplo: TI) pode ter o circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="93ebb-136">A single department (in this example: IT) can own the ExpressRoute circuit.</span></span> <span data-ttu-id="93ebb-137">Outras assinaturas dentro da organização podem usar o circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="93ebb-137">Other subscriptions within the organization can use the ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="93ebb-138">As cobranças por conectividade e largura de banda pelo circuito ExpressRoute serão aplicadas ao proprietário da assinatura.</span><span class="sxs-lookup"><span data-stu-id="93ebb-138">Connectivity and bandwidth charges for the ExpressRoute circuit will be applied to the subscription owner.</span></span> <span data-ttu-id="93ebb-139">Todas as redes virtuais compartilham a mesma largura de banda.</span><span class="sxs-lookup"><span data-stu-id="93ebb-139">All virtual networks share the same bandwidth.</span></span>
> 
> 

![Conectividade entre assinaturas](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)


### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="93ebb-141">Administração – proprietários e usuários do circuito</span><span class="sxs-lookup"><span data-stu-id="93ebb-141">Administration - circuit owners and circuit users</span></span>

<span data-ttu-id="93ebb-142">O “proprietário do circuito” é um usuário avançado autorizado do recurso de circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="93ebb-142">The 'circuit owner' is an authorized Power User of the ExpressRoute circuit resource.</span></span> <span data-ttu-id="93ebb-143">O proprietário do circuito pode criar autorizações que podem ser resgatadas pelos ‘usuários do circuito’.</span><span class="sxs-lookup"><span data-stu-id="93ebb-143">The circuit owner can create authorizations that can be redeemed by 'circuit users'.</span></span> <span data-ttu-id="93ebb-144">Usuários do circuito são proprietários de gateways de rede virtual que não estão na mesma assinatura que o circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="93ebb-144">Circuit users are owners of virtual network gateways that are not within the same subscription as the ExpressRoute circuit.</span></span> <span data-ttu-id="93ebb-145">Usuários do circuito podem resgatar autorizações (uma autorização por rede virtual).</span><span class="sxs-lookup"><span data-stu-id="93ebb-145">Circuit users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="93ebb-146">O proprietário do circuito tem a capacidade de modificar e revogar autorizações a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="93ebb-146">The circuit owner has the power to modify and revoke authorizations at any time.</span></span> <span data-ttu-id="93ebb-147">Revogar uma autorização faz com que todas as conexões de links sejam excluídas da assinatura cujo acesso foi revogado.</span><span class="sxs-lookup"><span data-stu-id="93ebb-147">Revoking an authorization results in all link connections being deleted from the subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="93ebb-148">Operações do proprietário do circuito</span><span class="sxs-lookup"><span data-stu-id="93ebb-148">Circuit owner operations</span></span>

<span data-ttu-id="93ebb-149">**Criar uma autorização**</span><span class="sxs-lookup"><span data-stu-id="93ebb-149">**To create an authorization**</span></span>

<span data-ttu-id="93ebb-150">O proprietário do circuito cria uma autorização.</span><span class="sxs-lookup"><span data-stu-id="93ebb-150">The circuit owner creates an authorization.</span></span> <span data-ttu-id="93ebb-151">Isso resulta na criação de uma chave de autorização que pode ser usada por um usuário do circuito para conectar seus gateways de rede virtual ao circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="93ebb-151">This results in the creation of an authorization key that can be used by a circuit user to connect their virtual network gateways to the ExpressRoute circuit.</span></span> <span data-ttu-id="93ebb-152">Uma autorização é válida apenas para uma conexão.</span><span class="sxs-lookup"><span data-stu-id="93ebb-152">An authorization is valid for only one connection.</span></span>

<span data-ttu-id="93ebb-153">O seguinte trecho de cmdlet mostra como criar uma autorização:</span><span class="sxs-lookup"><span data-stu-id="93ebb-153">The following cmdlet snippet shows how to create an authorization:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$auth1 = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
```


<span data-ttu-id="93ebb-154">A resposta para isso conterá a chave de autorização e o status:</span><span class="sxs-lookup"><span data-stu-id="93ebb-154">The response to this will contain the authorization key and status:</span></span>

    Name                   : MyAuthorization1
    Id                     : /subscriptions/&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/CrossSubTest/authorizations/MyAuthorization1
    Etag                   : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& 
    AuthorizationKey       : ####################################
    AuthorizationUseStatus : Available
    ProvisioningState      : Succeeded



<span data-ttu-id="93ebb-155">**Examinar autorizações**</span><span class="sxs-lookup"><span data-stu-id="93ebb-155">**To review authorizations**</span></span>

<span data-ttu-id="93ebb-156">O proprietário do circuito pode examinar todas as autorizações emitidas em um circuito específico executando o seguinte cmdlet:</span><span class="sxs-lookup"><span data-stu-id="93ebb-156">The circuit owner can review all authorizations that are issued on a particular circuit by running the following cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

<span data-ttu-id="93ebb-157">**Adicionar autorizações**</span><span class="sxs-lookup"><span data-stu-id="93ebb-157">**To add authorizations**</span></span>

<span data-ttu-id="93ebb-158">O proprietário do circuito pode adicionar autorizações usando o cmdlet a seguir.</span><span class="sxs-lookup"><span data-stu-id="93ebb-158">The circuit owner can add authorizations by using the following cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization2"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

<span data-ttu-id="93ebb-159">**Excluir autorizações**</span><span class="sxs-lookup"><span data-stu-id="93ebb-159">**To delete authorizations**</span></span>

<span data-ttu-id="93ebb-160">O proprietário do circuito pode revogar/excluir autorizações usando o seguinte cmdlet:</span><span class="sxs-lookup"><span data-stu-id="93ebb-160">The circuit owner can revoke/delete authorizations to the user by running the following cmdlet:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitAuthorization -Name "MyAuthorization2" -ExpressRouteCircuit $circuit
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit
```    

### <a name="circuit-user-operations"></a><span data-ttu-id="93ebb-161">Operações do usuário do circuito</span><span class="sxs-lookup"><span data-stu-id="93ebb-161">Circuit user operations</span></span>

<span data-ttu-id="93ebb-162">O usuário do circuito precisa da ID do par e de uma chave de autorização do proprietário do circuito.</span><span class="sxs-lookup"><span data-stu-id="93ebb-162">The circuit user needs the peer ID and an authorization key from the circuit owner.</span></span> <span data-ttu-id="93ebb-163">A chave de autorização é um GUID.</span><span class="sxs-lookup"><span data-stu-id="93ebb-163">The authorization key is a GUID.</span></span>

<span data-ttu-id="93ebb-164">É possível verificar a ID de Par com o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="93ebb-164">Peer ID can be checked from the following command:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

<span data-ttu-id="93ebb-165">**Resgatar uma autorização de conexão**</span><span class="sxs-lookup"><span data-stu-id="93ebb-165">**To redeem a connection authorization**</span></span>

<span data-ttu-id="93ebb-166">O usuário de circuito pode executar o seguinte cmdlet para resgatar uma autorização de vínculo:</span><span class="sxs-lookup"><span data-stu-id="93ebb-166">The circuit user can run the following cmdlet to redeem a link authorization:</span></span>

```powershell
$id = "/subscriptions/********************************/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/MyCircuit"    
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "RemoteResourceGroup" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $id -ConnectionType ExpressRoute -AuthorizationKey "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

<span data-ttu-id="93ebb-167">**Liberar uma autorização de conexão**</span><span class="sxs-lookup"><span data-stu-id="93ebb-167">**To release a connection authorization**</span></span>

<span data-ttu-id="93ebb-168">É possível liberar uma autorização excluindo a conexão que vincula o circuito do ExpressRoute à rede virtual.</span><span class="sxs-lookup"><span data-stu-id="93ebb-168">You can release an authorization by deleting the connection that links the ExpressRoute circuit to the virtual network.</span></span>

## <a name="modify-a-virtual-network-connection"></a><span data-ttu-id="93ebb-169">Modificar uma conexão de rede virtual</span><span class="sxs-lookup"><span data-stu-id="93ebb-169">Modify a virtual network connection</span></span>
<span data-ttu-id="93ebb-170">Você pode atualizar determinadas propriedades de uma conexão de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="93ebb-170">You can update certain properties of a virtual network connection.</span></span> 

<span data-ttu-id="93ebb-171">**Atualizar o peso da conexão**</span><span class="sxs-lookup"><span data-stu-id="93ebb-171">**To update the connection weight**</span></span>

<span data-ttu-id="93ebb-172">Sua rede virtual pode ser conectada a vários circuitos do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="93ebb-172">Your virtual network can be connected to multiple ExpressRoute circuits.</span></span> <span data-ttu-id="93ebb-173">Você pode receber o mesmo prefixo de mais de um circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="93ebb-173">You may receive the same prefix from more than one ExpressRoute circuit.</span></span> <span data-ttu-id="93ebb-174">Para escolher à qual conexão enviar o tráfego destinado a esse prefixo, você pode alterar *RoutingWeight* de uma conexão.</span><span class="sxs-lookup"><span data-stu-id="93ebb-174">To choose which connection to send traffic destined for this prefix, you can change *RoutingWeight* of a connection.</span></span> <span data-ttu-id="93ebb-175">O tráfego será enviado na conexão com o *RoutingWeight* mais alto.</span><span class="sxs-lookup"><span data-stu-id="93ebb-175">Traffic will be sent on the connection with the highest *RoutingWeight*.</span></span>

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "MyVirtualNetworkConnection" -ResourceGroupName "MyRG"
$connection.RoutingWeight = 100
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection
```

<span data-ttu-id="93ebb-176">O intervalo de *RoutingWeight* é de 0 a 32.000.</span><span class="sxs-lookup"><span data-stu-id="93ebb-176">The range of *RoutingWeight* is 0 to 32000.</span></span> <span data-ttu-id="93ebb-177">O valor padrão é 0.</span><span class="sxs-lookup"><span data-stu-id="93ebb-177">The default value is 0.</span></span>

## <a name="next-steps"></a><span data-ttu-id="93ebb-178">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="93ebb-178">Next steps</span></span>
<span data-ttu-id="93ebb-179">Para obter mais informações sobre o ExpressRoute, consulte [Perguntas Frequentes sobre ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="93ebb-179">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
