---
title: 'Vincular um circuito de rota expressa do tooan de rede virtual: CLI: Azure | Microsoft Docs'
description: "Este documento fornece uma visão geral de como toolink virtual redes circuitos de tooExpressRoute (VNets) usando o modelo de implantação do Gerenciador de recursos de saudação e a CLI."
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlit
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: anzaman,cherylmc
ms.openlocfilehash: 1251f016d9b94d3fee81de1df164cb085cbe9d78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit-using-cli"></a><span data-ttu-id="dfac6-103">Conecte-se a um circuito de rota expressa do tooan de rede virtual usando a CLI</span><span class="sxs-lookup"><span data-stu-id="dfac6-103">Connect a virtual network tooan ExpressRoute circuit using CLI</span></span>

<span data-ttu-id="dfac6-104">Este artigo ajuda você a vincular circuitos do ExpressRoute tooAzure redes virtuais (VNets) usando a CLI.</span><span class="sxs-lookup"><span data-stu-id="dfac6-104">This article helps you link virtual networks (VNets) tooAzure ExpressRoute circuits using CLI.</span></span> <span data-ttu-id="dfac6-105">toolink usando a CLI do Azure, redes virtuais Olá devem ser criadas usando o modelo de implantação do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="dfac6-105">toolink using Azure CLI, hello virtual networks must be created using hello Resource Manager deployment model.</span></span> <span data-ttu-id="dfac6-106">Eles podem ser em Olá mesma assinatura, ou parte de outra assinatura.</span><span class="sxs-lookup"><span data-stu-id="dfac6-106">They can either be in hello same subscription, or part of another subscription.</span></span> <span data-ttu-id="dfac6-107">Se você quiser toouse tooconnect um método diferente tooan sua rede virtual circuito de rota expressa, você pode selecionar um artigo Olá lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="dfac6-107">If you want toouse a different method tooconnect your VNet tooan ExpressRoute circuit, you can select an article from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="dfac6-108">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="dfac6-108">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="dfac6-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dfac6-109">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="dfac6-110">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="dfac6-110">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="dfac6-111">Vídeo – Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="dfac6-111">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="dfac6-112">PowerShell (clássico)</span><span class="sxs-lookup"><span data-stu-id="dfac6-112">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="dfac6-113">Pré-requisitos de configuração</span><span class="sxs-lookup"><span data-stu-id="dfac6-113">Configuration prerequisites</span></span>

* <span data-ttu-id="dfac6-114">Você precisa Olá a versão mais recente do hello interface de linha de comando (CLI).</span><span class="sxs-lookup"><span data-stu-id="dfac6-114">You need hello latest version of hello command-line interface (CLI).</span></span> <span data-ttu-id="dfac6-115">Para obter mais informações, consulte [Instalar a CLI do Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="dfac6-115">For more information, see [Install Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="dfac6-116">Você precisa Olá tooreview [pré-requisitos](expressroute-prerequisites.md), [requisitos de roteamento](expressroute-routing.md), e [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração.</span><span class="sxs-lookup"><span data-stu-id="dfac6-116">You need tooreview hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="dfac6-117">Você deve ter um circuito do ExpressRoute ativo.</span><span class="sxs-lookup"><span data-stu-id="dfac6-117">You must have an active ExpressRoute circuit.</span></span> 
  * <span data-ttu-id="dfac6-118">Siga as instruções de saudação muito[criar um circuito de rota expressa](howto-circuit-cli.md) e ter circuito Olá habilitado por seu provedor de conectividade.</span><span class="sxs-lookup"><span data-stu-id="dfac6-118">Follow hello instructions too[create an ExpressRoute circuit](howto-circuit-cli.md) and have hello circuit enabled by your connectivity provider.</span></span> 
  * <span data-ttu-id="dfac6-119">Verifique se o emparelhamento privado do Azure está configurado para seu circuito.</span><span class="sxs-lookup"><span data-stu-id="dfac6-119">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="dfac6-120">Consulte Olá [configurar o roteamento](howto-routing-cli.md) artigo para obter instruções de roteamentos.</span><span class="sxs-lookup"><span data-stu-id="dfac6-120">See hello [configure routing](howto-routing-cli.md) article for routing instructions.</span></span> 
  * <span data-ttu-id="dfac6-121">Verifique se o emparelhamento particular do Azure está configurado.</span><span class="sxs-lookup"><span data-stu-id="dfac6-121">Ensure that Azure private peering is configured.</span></span> <span data-ttu-id="dfac6-122">Olá emparelhamento via protocolo BGP entre sua rede e da Microsoft deve estar ativos para que você pode habilitar a conectividade de ponta a ponta.</span><span class="sxs-lookup"><span data-stu-id="dfac6-122">hello BGP peering between your network and Microsoft must be up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="dfac6-123">Verifique se tem uma rede virtual e um gateway de rede virtual criados e totalmente provisionados.</span><span class="sxs-lookup"><span data-stu-id="dfac6-123">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="dfac6-124">Siga as instruções de saudação muito[configurar um gateway de rede virtual para o ExpressRoute](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span><span class="sxs-lookup"><span data-stu-id="dfac6-124">Follow hello instructions too[Configure a virtual network gateway for ExpressRoute](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span></span> <span data-ttu-id="dfac6-125">Ser toouse se `--gateway-type ExpressRoute`.</span><span class="sxs-lookup"><span data-stu-id="dfac6-125">Be sure toouse `--gateway-type ExpressRoute`.</span></span>

* <span data-ttu-id="dfac6-126">Você pode vincular o circuito de rota expressa padrão do too10 redes virtuais tooa.</span><span class="sxs-lookup"><span data-stu-id="dfac6-126">You can link up too10 virtual networks tooa standard ExpressRoute circuit.</span></span> <span data-ttu-id="dfac6-127">Todas as redes virtuais devem estar em Olá mesma região geopolíticas ao usar um circuito de rota expressa padrão.</span><span class="sxs-lookup"><span data-stu-id="dfac6-127">All virtual networks must be in hello same geopolitical region when using a standard ExpressRoute circuit.</span></span> 

* <span data-ttu-id="dfac6-128">Se você habilitar o complemento do premium Olá rota expressa, você pode vincular uma rede virtual fora da região geopolíticas Olá Olá circuito de rota expressa ou conectar-se um grande número de redes virtuais tooyour circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="dfac6-128">If you enable hello ExpressRoute premium add-on, you can link a virtual network outside of hello geopolitical region of hello ExpressRoute circuit, or connect a larger number of virtual networks tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="dfac6-129">Para obter mais informações sobre o complemento do premium Olá, consulte Olá [perguntas frequentes sobre](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="dfac6-129">For more information about hello premium add-on, see hello [FAQ](expressroute-faqs.md).</span></span>

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a><span data-ttu-id="dfac6-130">Conectar uma rede virtual no hello mesmo circuito de tooa de assinatura</span><span class="sxs-lookup"><span data-stu-id="dfac6-130">Connect a virtual network in hello same subscription tooa circuit</span></span>

<span data-ttu-id="dfac6-131">Você pode se conectar a um circuito de rota expressa de tooan de gateway de rede virtual usando o exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="dfac6-131">You can connect a virtual network gateway tooan ExpressRoute circuit by using hello example.</span></span> <span data-ttu-id="dfac6-132">Verifique se esse gateway de rede virtual Olá é criado e está pronto para vinculação antes de executar o comando hello.</span><span class="sxs-lookup"><span data-stu-id="dfac6-132">Make sure that hello virtual network gateway is created and is ready for linking before you run hello command.</span></span>

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit
```

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a><span data-ttu-id="dfac6-133">Conectar uma rede virtual em um circuito de tooa assinatura diferente</span><span class="sxs-lookup"><span data-stu-id="dfac6-133">Connect a virtual network in a different subscription tooa circuit</span></span>

<span data-ttu-id="dfac6-134">Você pode compartilhar um circuito do ExpressRoute entre várias assinaturas.</span><span class="sxs-lookup"><span data-stu-id="dfac6-134">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="dfac6-135">a Figura Olá abaixo mostra um esquemático simples de como funciona o compartilhamento para circuitos ExpressRoute entre várias assinaturas.</span><span class="sxs-lookup"><span data-stu-id="dfac6-135">hello figure below shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="dfac6-136">Cada uma das nuvens menores de saudação dentro da nuvem grande Olá é toorepresent usadas assinaturas que pertencem a toodifferent departamentos dentro de uma organização.</span><span class="sxs-lookup"><span data-stu-id="dfac6-136">Each of hello smaller clouds within hello large cloud is used toorepresent subscriptions that belong toodifferent departments within an organization.</span></span> <span data-ttu-id="dfac6-137">Cada um dos departamentos hello dentro da organização Olá pode usar sua própria assinatura para implantar seus serviços – mas eles podem compartilhar uma única rede rota expressa circuito tooconnect tooyour back local.</span><span class="sxs-lookup"><span data-stu-id="dfac6-137">Each of hello departments within hello organization can use their own subscription for deploying their services--but they can share a single ExpressRoute circuit tooconnect back tooyour on-premises network.</span></span> <span data-ttu-id="dfac6-138">Um único departamento (neste exemplo: IT) pode ter o circuito de rota expressa hello.</span><span class="sxs-lookup"><span data-stu-id="dfac6-138">A single department (in this example: IT) can own hello ExpressRoute circuit.</span></span> <span data-ttu-id="dfac6-139">Outras assinaturas dentro da organização Olá podem usar o circuito de rota expressa hello.</span><span class="sxs-lookup"><span data-stu-id="dfac6-139">Other subscriptions within hello organization can use hello ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="dfac6-140">Encargos de largura de banda e conectividade para o circuito dedicado de saudação será aplicado toohello proprietário do circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="dfac6-140">Connectivity and bandwidth charges for hello dedicated circuit will be applied toohello ExpressRoute Circuit Owner.</span></span> <span data-ttu-id="dfac6-141">Todas as redes virtuais compartilham Olá mesma largura de banda.</span><span class="sxs-lookup"><span data-stu-id="dfac6-141">All virtual networks share hello same bandwidth.</span></span>
> 
> 

![Conectividade entre assinaturas](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="dfac6-143">Administração – proprietários e usuários do circuito</span><span class="sxs-lookup"><span data-stu-id="dfac6-143">Administration - Circuit Owners and Circuit Users</span></span>

<span data-ttu-id="dfac6-144">Olá proprietário do circuito é um usuário autorizado Power Olá recursos de circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="dfac6-144">hello 'Circuit Owner' is an authorized Power User of hello ExpressRoute circuit resource.</span></span> <span data-ttu-id="dfac6-145">Olá proprietário do circuito pode criar autorizações que podem ser trocadas por 'Usuários do circuito'.</span><span class="sxs-lookup"><span data-stu-id="dfac6-145">hello Circuit Owner can create authorizations that can be redeemed by 'Circuit Users'.</span></span> <span data-ttu-id="dfac6-146">Os usuários do circuito são proprietários da rede virtual gateways que não estão no hello mesma assinatura conforme Olá circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="dfac6-146">Circuit Users are owners of virtual network gateways that are not within hello same subscription as hello ExpressRoute circuit.</span></span> <span data-ttu-id="dfac6-147">Usuários do circuito podem resgatar autorizações (uma autorização por rede virtual).</span><span class="sxs-lookup"><span data-stu-id="dfac6-147">Circuit Users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="dfac6-148">Olá proprietário do circuito tem autorizações de toomodify e revoke power Olá a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="dfac6-148">hello Circuit Owner has hello power toomodify and revoke authorizations at any time.</span></span> <span data-ttu-id="dfac6-149">Quando uma autorização é revogada, todas as conexões de link são excluídas da assinatura Olá cujo acesso foi revogado.</span><span class="sxs-lookup"><span data-stu-id="dfac6-149">When an authorization is revoked, all link connections are deleted from hello subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="dfac6-150">Operações do proprietário do circuito</span><span class="sxs-lookup"><span data-stu-id="dfac6-150">Circuit Owner operations</span></span>

<span data-ttu-id="dfac6-151">**toocreate uma autorização**</span><span class="sxs-lookup"><span data-stu-id="dfac6-151">**toocreate an authorization**</span></span>

<span data-ttu-id="dfac6-152">Olá proprietário do circuito cria uma autorização, que cria uma chave de autorização que pode ser usado por um usuário do circuito tooconnect seu gateways de rede virtual toohello circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="dfac6-152">hello Circuit Owner creates an authorization, which creates an authorization key that can be used by a Circuit User tooconnect their virtual network gateways toohello ExpressRoute circuit.</span></span> <span data-ttu-id="dfac6-153">Uma autorização é válida apenas para uma conexão.</span><span class="sxs-lookup"><span data-stu-id="dfac6-153">An authorization is valid for only one connection.</span></span>

<span data-ttu-id="dfac6-154">Olá mostrado no exemplo a seguir como toocreate uma autorização:</span><span class="sxs-lookup"><span data-stu-id="dfac6-154">hello following example shows how toocreate an authorization:</span></span>

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization
```

<span data-ttu-id="dfac6-155">resposta de saudação contém o status e a chave de autorização de saudação:</span><span class="sxs-lookup"><span data-stu-id="dfac6-155">hello response contains hello authorization key and status:</span></span>

```azurecli
"authorizationKey": "0a7f3020-541f-4b4b-844a-5fb43472e3d7",
"authorizationUseStatus": "Available",
"etag": "W/\"010353d4-8955-4984-807a-585c21a22ae0\"",
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/authorizations/MyAuthorization1",
"name": "MyAuthorization1",
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup"
```

<span data-ttu-id="dfac6-156">**tooreview autorizações**</span><span class="sxs-lookup"><span data-stu-id="dfac6-156">**tooreview authorizations**</span></span>

<span data-ttu-id="dfac6-157">Olá proprietário do circuito pode revisar todas as autorizações que são emitidas em um circuito específico executando Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="dfac6-157">hello Circuit Owner can review all authorizations that are issued on a particular circuit by running hello following example:</span></span>

```azurecli
az network express-route auth list --circuit-name MyCircuit -g ExpressRouteResourceGroup
```

<span data-ttu-id="dfac6-158">**tooadd autorizações**</span><span class="sxs-lookup"><span data-stu-id="dfac6-158">**tooadd authorizations**</span></span>

<span data-ttu-id="dfac6-159">Olá proprietário do circuito pode adicionar autorizações usando Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="dfac6-159">hello Circuit Owner can add authorizations by using hello following example:</span></span>

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

<span data-ttu-id="dfac6-160">**toodelete autorizações**</span><span class="sxs-lookup"><span data-stu-id="dfac6-160">**toodelete authorizations**</span></span>

<span data-ttu-id="dfac6-161">Olá proprietário do circuito pode revogar/excluir autorizações toohello usuário executando Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="dfac6-161">hello Circuit Owner can revoke/delete authorizations toohello user by running hello following example:</span></span>

```azurecli
az network express-route auth delete --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

### <a name="circuit-user-operations"></a><span data-ttu-id="dfac6-162">Operações do usuário do circuito</span><span class="sxs-lookup"><span data-stu-id="dfac6-162">Circuit User operations</span></span>

<span data-ttu-id="dfac6-163">Olá usuários do circuito precisa Olá peer ID e uma chave de autorização do proprietário do circuito de saudação.</span><span class="sxs-lookup"><span data-stu-id="dfac6-163">hello Circuit User needs hello peer ID and an authorization key from hello Circuit Owner.</span></span> <span data-ttu-id="dfac6-164">chave de autorização de saudação é um GUID.</span><span class="sxs-lookup"><span data-stu-id="dfac6-164">hello authorization key is a GUID.</span></span>

```azurecli
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

<span data-ttu-id="dfac6-165">**tooredeem uma autorização de conexão**</span><span class="sxs-lookup"><span data-stu-id="dfac6-165">**tooredeem a connection authorization**</span></span>

<span data-ttu-id="dfac6-166">Olá usuários do circuito pode executar Olá tooredeem de exemplo a seguir uma autorização de link:</span><span class="sxs-lookup"><span data-stu-id="dfac6-166">hello Circuit User can run hello following example tooredeem a link authorization:</span></span>

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit --authorization-key "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

<span data-ttu-id="dfac6-167">**toorelease uma autorização de conexão**</span><span class="sxs-lookup"><span data-stu-id="dfac6-167">**toorelease a connection authorization**</span></span>

<span data-ttu-id="dfac6-168">Você pode liberar uma autorização Excluindo conexão Olá que vincula a rede virtual de toohello Olá de circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="dfac6-168">You can release an authorization by deleting hello connection that links hello ExpressRoute circuit toohello virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dfac6-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dfac6-169">Next steps</span></span>

<span data-ttu-id="dfac6-170">Para obter mais informações sobre a rota expressa, consulte Olá [perguntas Frequentes do ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="dfac6-170">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
