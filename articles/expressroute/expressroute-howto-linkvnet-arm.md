---
title: 'Vincular um circuito de rota expressa do tooan de rede virtual: PowerShell: Azure | Microsoft Docs'
description: "Este documento fornece uma visão geral de como toolink virtual redes circuitos de tooExpressRoute (VNets) usando o modelo de implantação do Gerenciador de recursos de saudação e PowerShell."
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
ms.openlocfilehash: e75a9f6b42fa8e1a579e4f19882ec99b277b545f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="e2922-103">Conectar uma rede virtual de tooan circuito de rota expressa</span><span class="sxs-lookup"><span data-stu-id="e2922-103">Connect a virtual network tooan ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e2922-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e2922-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="e2922-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e2922-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="e2922-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="e2922-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="e2922-107">Vídeo – Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e2922-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="e2922-108">PowerShell (clássico)</span><span class="sxs-lookup"><span data-stu-id="e2922-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
>

<span data-ttu-id="e2922-109">Este artigo ajuda você a vincular circuitos do ExpressRoute tooAzure redes virtuais (VNets) usando o modelo de implantação do Gerenciador de recursos de saudação e PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e2922-109">This article helps you link virtual networks (VNets) tooAzure ExpressRoute circuits by using hello Resource Manager deployment model and PowerShell.</span></span> <span data-ttu-id="e2922-110">Redes virtuais podem ser em Olá mesma assinatura ou parte de outra assinatura.</span><span class="sxs-lookup"><span data-stu-id="e2922-110">Virtual networks can either be in hello same subscription or part of another subscription.</span></span> <span data-ttu-id="e2922-111">Este artigo mostra como vincular tooupdate uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="e2922-111">This article also shows you how tooupdate a virtual network link.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="e2922-112">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="e2922-112">Before you begin</span></span>
* <span data-ttu-id="e2922-113">Instale a versão mais recente Olá dos módulos do PowerShell do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e2922-113">Install hello latest version of hello Azure PowerShell modules.</span></span> <span data-ttu-id="e2922-114">Para obter mais informações, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e2922-114">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="e2922-115">Saudação de revisão [pré-requisitos](expressroute-prerequisites.md), [requisitos de roteamento](expressroute-routing.md), e [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração.</span><span class="sxs-lookup"><span data-stu-id="e2922-115">Review hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="e2922-116">Você deve ter um circuito do ExpressRoute ativo.</span><span class="sxs-lookup"><span data-stu-id="e2922-116">You must have an active ExpressRoute circuit.</span></span> 
  * <span data-ttu-id="e2922-117">Siga as instruções de saudação muito[criar um circuito de rota expressa](expressroute-howto-circuit-arm.md) e ter circuito Olá habilitado por seu provedor de conectividade.</span><span class="sxs-lookup"><span data-stu-id="e2922-117">Follow hello instructions too[create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have hello circuit enabled by your connectivity provider.</span></span> 
  * <span data-ttu-id="e2922-118">Verifique se o emparelhamento privado do Azure está configurado para seu circuito.</span><span class="sxs-lookup"><span data-stu-id="e2922-118">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="e2922-119">Consulte Olá [configurar o roteamento](expressroute-howto-routing-arm.md) artigo para obter instruções de roteamentos.</span><span class="sxs-lookup"><span data-stu-id="e2922-119">See hello [configure routing](expressroute-howto-routing-arm.md) article for routing instructions.</span></span> 
  * <span data-ttu-id="e2922-120">Certifique-se de que o emparelhamento particular do Azure está configurado e Olá emparelhamento via protocolo BGP entre sua rede e a Microsoft está ativo para que você pode habilitar a conectividade de ponta a ponta.</span><span class="sxs-lookup"><span data-stu-id="e2922-120">Ensure that Azure private peering is configured and hello BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="e2922-121">Verifique se tem uma rede virtual e um gateway de rede virtual criados e totalmente provisionados.</span><span class="sxs-lookup"><span data-stu-id="e2922-121">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="e2922-122">Siga as instruções de saudação muito[criar um gateway de rede virtual para o ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="e2922-122">Follow hello instructions too[create a virtual network gateway for ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="e2922-123">Um gateway de rede virtual para a rota expressa usa Olá GatewayType 'ExpressRoute', não VPN.</span><span class="sxs-lookup"><span data-stu-id="e2922-123">A virtual network gateway for ExpressRoute uses hello GatewayType 'ExpressRoute', not VPN.</span></span>

* <span data-ttu-id="e2922-124">Você pode vincular o circuito de rota expressa padrão do too10 redes virtuais tooa.</span><span class="sxs-lookup"><span data-stu-id="e2922-124">You can link up too10 virtual networks tooa standard ExpressRoute circuit.</span></span> <span data-ttu-id="e2922-125">Todas as redes virtuais devem estar em Olá mesma região geopolíticas ao usar um circuito de rota expressa padrão.</span><span class="sxs-lookup"><span data-stu-id="e2922-125">All virtual networks must be in hello same geopolitical region when using a standard ExpressRoute circuit.</span></span> 

* <span data-ttu-id="e2922-126">Você pode vincular uma rede virtual fora da região geopolíticas Olá Olá circuito de rota expressa ou conectar-se um grande número de redes virtuais tooyour circuito de rota expressa se você habilitou o complemento do premium Olá rota expressa.</span><span class="sxs-lookup"><span data-stu-id="e2922-126">You can link a virtual networks outside of hello geopolitical region of hello ExpressRoute circuit, or connect a larger number of virtual networks tooyour ExpressRoute circuit if you enabled hello ExpressRoute premium add-on.</span></span> <span data-ttu-id="e2922-127">Verificar Olá [perguntas frequentes sobre](expressroute-faqs.md) para obter mais detalhes sobre o complemento do premium Olá.</span><span class="sxs-lookup"><span data-stu-id="e2922-127">Check hello [FAQ](expressroute-faqs.md) for more details on hello premium add-on.</span></span>


## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a><span data-ttu-id="e2922-128">Conectar uma rede virtual no hello mesmo circuito de tooa de assinatura</span><span class="sxs-lookup"><span data-stu-id="e2922-128">Connect a virtual network in hello same subscription tooa circuit</span></span>
<span data-ttu-id="e2922-129">Você pode se conectar a um gateway de rede virtual tooan circuito de rota expressa usando Olá cmdlet a seguir.</span><span class="sxs-lookup"><span data-stu-id="e2922-129">You can connect a virtual network gateway tooan ExpressRoute circuit by using hello following cmdlet.</span></span> <span data-ttu-id="e2922-130">Verifique se esse gateway de rede virtual Olá é criado e está pronto para vinculação antes de executar o cmdlet hello:</span><span class="sxs-lookup"><span data-stu-id="e2922-130">Make sure that hello virtual network gateway is created and is ready for linking before you run hello cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "MyRG" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $circuit.Id -ConnectionType ExpressRoute
```

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a><span data-ttu-id="e2922-131">Conectar uma rede virtual em um circuito de tooa assinatura diferente</span><span class="sxs-lookup"><span data-stu-id="e2922-131">Connect a virtual network in a different subscription tooa circuit</span></span>
<span data-ttu-id="e2922-132">Você pode compartilhar um circuito do ExpressRoute entre várias assinaturas.</span><span class="sxs-lookup"><span data-stu-id="e2922-132">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="e2922-133">Olá figura a seguir mostra um esquemático simples de como funciona o compartilhamento para circuitos ExpressRoute entre várias assinaturas.</span><span class="sxs-lookup"><span data-stu-id="e2922-133">hello following figure shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="e2922-134">Cada uma das nuvens menores de saudação dentro da nuvem grande Olá é toorepresent usadas assinaturas que pertencem a toodifferent departamentos dentro de uma organização.</span><span class="sxs-lookup"><span data-stu-id="e2922-134">Each of hello smaller clouds within hello large cloud is used toorepresent subscriptions that belong toodifferent departments within an organization.</span></span> <span data-ttu-id="e2922-135">Cada um dos departamentos hello dentro da organização Olá pode usar sua própria assinatura para implantar seus serviços – mas eles podem compartilhar uma única rede rota expressa circuito tooconnect tooyour back local.</span><span class="sxs-lookup"><span data-stu-id="e2922-135">Each of hello departments within hello organization can use their own subscription for deploying their services--but they can share a single ExpressRoute circuit tooconnect back tooyour on-premises network.</span></span> <span data-ttu-id="e2922-136">Um único departamento (neste exemplo: IT) pode ter o circuito de rota expressa hello.</span><span class="sxs-lookup"><span data-stu-id="e2922-136">A single department (in this example: IT) can own hello ExpressRoute circuit.</span></span> <span data-ttu-id="e2922-137">Outras assinaturas dentro da organização Olá podem usar o circuito de rota expressa hello.</span><span class="sxs-lookup"><span data-stu-id="e2922-137">Other subscriptions within hello organization can use hello ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="e2922-138">Encargos de largura de banda e conectividade para Olá circuito de rota expressa será o proprietário da assinatura toohello aplicado.</span><span class="sxs-lookup"><span data-stu-id="e2922-138">Connectivity and bandwidth charges for hello ExpressRoute circuit will be applied toohello subscription owner.</span></span> <span data-ttu-id="e2922-139">Todas as redes virtuais compartilham Olá mesma largura de banda.</span><span class="sxs-lookup"><span data-stu-id="e2922-139">All virtual networks share hello same bandwidth.</span></span>
> 
> 

![Conectividade entre assinaturas](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)


### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="e2922-141">Administração – proprietários e usuários do circuito</span><span class="sxs-lookup"><span data-stu-id="e2922-141">Administration - circuit owners and circuit users</span></span>

<span data-ttu-id="e2922-142">Olá 'proprietário do circuito' é um usuário autorizado Power Olá recursos de circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="e2922-142">hello 'circuit owner' is an authorized Power User of hello ExpressRoute circuit resource.</span></span> <span data-ttu-id="e2922-143">proprietário do circuito Olá pode criar autorizações que podem ser trocadas por 'usuários do circuito'.</span><span class="sxs-lookup"><span data-stu-id="e2922-143">hello circuit owner can create authorizations that can be redeemed by 'circuit users'.</span></span> <span data-ttu-id="e2922-144">Os usuários do circuito são proprietários da rede virtual gateways que não estão no hello mesma assinatura conforme Olá circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="e2922-144">Circuit users are owners of virtual network gateways that are not within hello same subscription as hello ExpressRoute circuit.</span></span> <span data-ttu-id="e2922-145">Usuários do circuito podem resgatar autorizações (uma autorização por rede virtual).</span><span class="sxs-lookup"><span data-stu-id="e2922-145">Circuit users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="e2922-146">proprietário do circuito Olá tem autorizações de toomodify e revoke power Olá a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="e2922-146">hello circuit owner has hello power toomodify and revoke authorizations at any time.</span></span> <span data-ttu-id="e2922-147">Revogando uma resulta de autorização em todas as conexões de link que está sendo excluídas da assinatura de saudação cujo acesso foi revogado.</span><span class="sxs-lookup"><span data-stu-id="e2922-147">Revoking an authorization results in all link connections being deleted from hello subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="e2922-148">Operações do proprietário do circuito</span><span class="sxs-lookup"><span data-stu-id="e2922-148">Circuit owner operations</span></span>

<span data-ttu-id="e2922-149">**toocreate uma autorização**</span><span class="sxs-lookup"><span data-stu-id="e2922-149">**toocreate an authorization**</span></span>

<span data-ttu-id="e2922-150">proprietário do circuito Olá cria uma autorização.</span><span class="sxs-lookup"><span data-stu-id="e2922-150">hello circuit owner creates an authorization.</span></span> <span data-ttu-id="e2922-151">Isso resulta na criação de saudação de uma chave de autorização que pode ser usado por um tooconnect de usuário do circuito seu gateways de rede virtual toohello circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="e2922-151">This results in hello creation of an authorization key that can be used by a circuit user tooconnect their virtual network gateways toohello ExpressRoute circuit.</span></span> <span data-ttu-id="e2922-152">Uma autorização é válida apenas para uma conexão.</span><span class="sxs-lookup"><span data-stu-id="e2922-152">An authorization is valid for only one connection.</span></span>

<span data-ttu-id="e2922-153">Olá trecho a seguir cmdlet mostra como toocreate uma autorização:</span><span class="sxs-lookup"><span data-stu-id="e2922-153">hello following cmdlet snippet shows how toocreate an authorization:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$auth1 = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
```


<span data-ttu-id="e2922-154">Olá resposta toothis conterá o status e a chave de autorização de saudação:</span><span class="sxs-lookup"><span data-stu-id="e2922-154">hello response toothis will contain hello authorization key and status:</span></span>

    Name                   : MyAuthorization1
    Id                     : /subscriptions/&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/CrossSubTest/authorizations/MyAuthorization1
    Etag                   : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& 
    AuthorizationKey       : ####################################
    AuthorizationUseStatus : Available
    ProvisioningState      : Succeeded



<span data-ttu-id="e2922-155">**tooreview autorizações**</span><span class="sxs-lookup"><span data-stu-id="e2922-155">**tooreview authorizations**</span></span>

<span data-ttu-id="e2922-156">proprietário do circuito Olá pode revisar todas as autorizações que são emitidas em um circuito específico executando Olá cmdlet a seguir:</span><span class="sxs-lookup"><span data-stu-id="e2922-156">hello circuit owner can review all authorizations that are issued on a particular circuit by running hello following cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

<span data-ttu-id="e2922-157">**tooadd autorizações**</span><span class="sxs-lookup"><span data-stu-id="e2922-157">**tooadd authorizations**</span></span>

<span data-ttu-id="e2922-158">proprietário do circuito Olá pode adicionar autorizações usando Olá cmdlet a seguir:</span><span class="sxs-lookup"><span data-stu-id="e2922-158">hello circuit owner can add authorizations by using hello following cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization2"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

<span data-ttu-id="e2922-159">**toodelete autorizações**</span><span class="sxs-lookup"><span data-stu-id="e2922-159">**toodelete authorizations**</span></span>

<span data-ttu-id="e2922-160">proprietário do circuito Olá pode revogar/excluir autorizações toohello usuário executando Olá cmdlet a seguir:</span><span class="sxs-lookup"><span data-stu-id="e2922-160">hello circuit owner can revoke/delete authorizations toohello user by running hello following cmdlet:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitAuthorization -Name "MyAuthorization2" -ExpressRouteCircuit $circuit
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit
```    

### <a name="circuit-user-operations"></a><span data-ttu-id="e2922-161">Operações do usuário do circuito</span><span class="sxs-lookup"><span data-stu-id="e2922-161">Circuit user operations</span></span>

<span data-ttu-id="e2922-162">usuários do circuito Olá precisa Olá peer ID e uma chave de autorização do proprietário do circuito hello.</span><span class="sxs-lookup"><span data-stu-id="e2922-162">hello circuit user needs hello peer ID and an authorization key from hello circuit owner.</span></span> <span data-ttu-id="e2922-163">chave de autorização de saudação é um GUID.</span><span class="sxs-lookup"><span data-stu-id="e2922-163">hello authorization key is a GUID.</span></span>

<span data-ttu-id="e2922-164">ID de mesmo nível pode ser verificada de saudação comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e2922-164">Peer ID can be checked from hello following command:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

<span data-ttu-id="e2922-165">**tooredeem uma autorização de conexão**</span><span class="sxs-lookup"><span data-stu-id="e2922-165">**tooredeem a connection authorization**</span></span>

<span data-ttu-id="e2922-166">usuários do circuito Olá podem executar Olá tooredeem cmdlet a seguir uma autorização de link:</span><span class="sxs-lookup"><span data-stu-id="e2922-166">hello circuit user can run hello following cmdlet tooredeem a link authorization:</span></span>

```powershell
$id = "/subscriptions/********************************/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/MyCircuit"    
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "RemoteResourceGroup" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $id -ConnectionType ExpressRoute -AuthorizationKey "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

<span data-ttu-id="e2922-167">**toorelease uma autorização de conexão**</span><span class="sxs-lookup"><span data-stu-id="e2922-167">**toorelease a connection authorization**</span></span>

<span data-ttu-id="e2922-168">Você pode liberar uma autorização Excluindo conexão Olá que vincula a rede virtual de toohello Olá de circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e2922-168">You can release an authorization by deleting hello connection that links hello ExpressRoute circuit toohello virtual network.</span></span>

## <a name="modify-a-virtual-network-connection"></a><span data-ttu-id="e2922-169">Modificar uma conexão de rede virtual</span><span class="sxs-lookup"><span data-stu-id="e2922-169">Modify a virtual network connection</span></span>
<span data-ttu-id="e2922-170">Você pode atualizar determinadas propriedades de uma conexão de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="e2922-170">You can update certain properties of a virtual network connection.</span></span> 

<span data-ttu-id="e2922-171">**peso de conexão Olá tooupdate**</span><span class="sxs-lookup"><span data-stu-id="e2922-171">**tooupdate hello connection weight**</span></span>

<span data-ttu-id="e2922-172">Sua rede virtual pode ser conectado toomultiple circuitos do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e2922-172">Your virtual network can be connected toomultiple ExpressRoute circuits.</span></span> <span data-ttu-id="e2922-173">Você pode receber o mesmo prefixo de saudação de mais de um circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="e2922-173">You may receive hello same prefix from more than one ExpressRoute circuit.</span></span> <span data-ttu-id="e2922-174">toochoose o tráfego de toosend conexão destinado a esse prefixo, você pode alterar *RoutingWeight* de uma conexão.</span><span class="sxs-lookup"><span data-stu-id="e2922-174">toochoose which connection toosend traffic destined for this prefix, you can change *RoutingWeight* of a connection.</span></span> <span data-ttu-id="e2922-175">O tráfego será enviado na conexão Olá com hello mais alto *RoutingWeight*.</span><span class="sxs-lookup"><span data-stu-id="e2922-175">Traffic will be sent on hello connection with hello highest *RoutingWeight*.</span></span>

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "MyVirtualNetworkConnection" -ResourceGroupName "MyRG"
$connection.RoutingWeight = 100
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection
```

<span data-ttu-id="e2922-176">Olá intervalo de *RoutingWeight* é too32000 0.</span><span class="sxs-lookup"><span data-stu-id="e2922-176">hello range of *RoutingWeight* is 0 too32000.</span></span> <span data-ttu-id="e2922-177">valor padrão de saudação é 0.</span><span class="sxs-lookup"><span data-stu-id="e2922-177">hello default value is 0.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2922-178">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e2922-178">Next steps</span></span>
<span data-ttu-id="e2922-179">Para obter mais informações sobre a rota expressa, consulte Olá [perguntas Frequentes do ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="e2922-179">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
