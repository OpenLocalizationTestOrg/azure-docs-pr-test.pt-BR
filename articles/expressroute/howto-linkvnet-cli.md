---
title: 'Vincular uma rede virtual a um circuito ExpressRoute: CLI: Azure | Microsoft Docs'
description: "Este documento fornece uma visão geral de como vincular as redes virtuais (VNets) aos circuitos do ExpressRoute usando o modelo de implantação do Resource Manager e a CLI."
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
ms.openlocfilehash: 0ea696e796ec3a943bc028f56da417978b728b82
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2017
---
# <a name="connect-a-virtual-network-to-an-expressroute-circuit-using-cli"></a><span data-ttu-id="c232a-103">Conectar uma rede virtual a um circuito de ExpressRoute usando a CLI</span><span class="sxs-lookup"><span data-stu-id="c232a-103">Connect a virtual network to an ExpressRoute circuit using CLI</span></span>

<span data-ttu-id="c232a-104">Este artigo ajuda a vincular redes virtuais (VNets) aos circuitos de ExpressRoute do Azure usando a CLI.</span><span class="sxs-lookup"><span data-stu-id="c232a-104">This article helps you link virtual networks (VNets) to Azure ExpressRoute circuits using CLI.</span></span> <span data-ttu-id="c232a-105">Para vincular usando a CLI do Azure, as redes virtuais devem ser criadas usando o modelo de implantação do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c232a-105">To link using Azure CLI, the virtual networks must be created using the Resource Manager deployment model.</span></span> <span data-ttu-id="c232a-106">Elas podem estar na mesma assinatura ou fazer parte de outra assinatura.</span><span class="sxs-lookup"><span data-stu-id="c232a-106">They can either be in the same subscription, or part of another subscription.</span></span> <span data-ttu-id="c232a-107">Se quiser usar um método diferente para conectar sua VNet a um circuito de ExpressRoute, você poderá selecionar um artigo na lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="c232a-107">If you want to use a different method to connect your VNet to an ExpressRoute circuit, you can select an article from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c232a-108">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c232a-108">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="c232a-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c232a-109">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="c232a-110">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="c232a-110">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="c232a-111">Vídeo – Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c232a-111">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="c232a-112">PowerShell (clássico)</span><span class="sxs-lookup"><span data-stu-id="c232a-112">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="c232a-113">Pré-requisitos de configuração</span><span class="sxs-lookup"><span data-stu-id="c232a-113">Configuration prerequisites</span></span>

* <span data-ttu-id="c232a-114">Você precisa da versão mais recente da CLI (interface de linha de comando).</span><span class="sxs-lookup"><span data-stu-id="c232a-114">You need the latest version of the command-line interface (CLI).</span></span> <span data-ttu-id="c232a-115">Para obter mais informações, consulte [Instalar a CLI do Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c232a-115">For more information, see [Install Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="c232a-116">Leia os [pré-requisitos](expressroute-prerequisites.md), os [requisitos de roteamento](expressroute-routing.md) e os [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração.</span><span class="sxs-lookup"><span data-stu-id="c232a-116">You need to review the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="c232a-117">Você deve ter um circuito do ExpressRoute ativo.</span><span class="sxs-lookup"><span data-stu-id="c232a-117">You must have an active ExpressRoute circuit.</span></span> 
  * <span data-ttu-id="c232a-118">Siga as instruções para [criar um circuito do ExpressRoute](howto-circuit-cli.md) e para que o circuito seja habilitado pelo provedor de conectividade.</span><span class="sxs-lookup"><span data-stu-id="c232a-118">Follow the instructions to [create an ExpressRoute circuit](howto-circuit-cli.md) and have the circuit enabled by your connectivity provider.</span></span> 
  * <span data-ttu-id="c232a-119">Verifique se o emparelhamento privado do Azure está configurado para seu circuito.</span><span class="sxs-lookup"><span data-stu-id="c232a-119">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="c232a-120">Veja o artigo [Configurar roteamento](howto-routing-cli.md) para obter instruções sobre roteamento.</span><span class="sxs-lookup"><span data-stu-id="c232a-120">See the [configure routing](howto-routing-cli.md) article for routing instructions.</span></span> 
  * <span data-ttu-id="c232a-121">Verifique se o emparelhamento particular do Azure está configurado.</span><span class="sxs-lookup"><span data-stu-id="c232a-121">Ensure that Azure private peering is configured.</span></span> <span data-ttu-id="c232a-122">O emparelhamento via protocolo BGP entre sua rede e a Microsoft deve estar ativo para que você possa habilitar a conectividade de ponta a ponta.</span><span class="sxs-lookup"><span data-stu-id="c232a-122">The BGP peering between your network and Microsoft must be up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="c232a-123">Verifique se tem uma rede virtual e um gateway de rede virtual criados e totalmente provisionados.</span><span class="sxs-lookup"><span data-stu-id="c232a-123">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="c232a-124">Siga as instruções para [Configurar um gateway de rede virtual para ExpressRoute](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span><span class="sxs-lookup"><span data-stu-id="c232a-124">Follow the instructions to [Configure a virtual network gateway for ExpressRoute](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span></span> <span data-ttu-id="c232a-125">Certifique-se de usar `--gateway-type ExpressRoute`.</span><span class="sxs-lookup"><span data-stu-id="c232a-125">Be sure to use `--gateway-type ExpressRoute`.</span></span>

* <span data-ttu-id="c232a-126">Você pode vincular até 10 redes virtuais a um circuito do ExpressRoute padrão.</span><span class="sxs-lookup"><span data-stu-id="c232a-126">You can link up to 10 virtual networks to a standard ExpressRoute circuit.</span></span> <span data-ttu-id="c232a-127">Todas as redes virtuais deverão estar na mesma região geopolítica ao usar um circuito do ExpressRoute padrão.</span><span class="sxs-lookup"><span data-stu-id="c232a-127">All virtual networks must be in the same geopolitical region when using a standard ExpressRoute circuit.</span></span> 

* <span data-ttu-id="c232a-128">Se você tiver habilitado o complemento premium do ExpressRoute, você poderá vincular uma rede virtual fora da região geopolítica do circuito de ExpressRoute ou conectar um grande número de redes virtuais ao circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c232a-128">If you enable the ExpressRoute premium add-on, you can link a virtual network outside of the geopolitical region of the ExpressRoute circuit, or connect a larger number of virtual networks to your ExpressRoute circuit.</span></span> <span data-ttu-id="c232a-129">Para obter mais informações sobre o complemento premium, consulte as [Perguntas Frequentes](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="c232a-129">For more information about the premium add-on, see the [FAQ](expressroute-faqs.md).</span></span>

## <a name="connect-a-virtual-network-in-the-same-subscription-to-a-circuit"></a><span data-ttu-id="c232a-130">Conectar uma rede virtual na mesma assinatura a um circuito</span><span class="sxs-lookup"><span data-stu-id="c232a-130">Connect a virtual network in the same subscription to a circuit</span></span>

<span data-ttu-id="c232a-131">Você pode conectar um gateway de rede virtual a um circuito do ExpressRoute usando o exemplo.</span><span class="sxs-lookup"><span data-stu-id="c232a-131">You can connect a virtual network gateway to an ExpressRoute circuit by using the example.</span></span> <span data-ttu-id="c232a-132">Verifique se o gateway de rede virtual foi criado e se está pronto para vinculação antes de executar o comando.</span><span class="sxs-lookup"><span data-stu-id="c232a-132">Make sure that the virtual network gateway is created and is ready for linking before you run the command.</span></span>

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit
```

## <a name="connect-a-virtual-network-in-a-different-subscription-to-a-circuit"></a><span data-ttu-id="c232a-133">Conectar uma rede virtual em uma assinatura diferente a um circuito</span><span class="sxs-lookup"><span data-stu-id="c232a-133">Connect a virtual network in a different subscription to a circuit</span></span>

<span data-ttu-id="c232a-134">Você pode compartilhar um circuito do ExpressRoute entre várias assinaturas.</span><span class="sxs-lookup"><span data-stu-id="c232a-134">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="c232a-135">A figura abaixo mostra um esquema simples de como funciona o compartilhamento de circuitos do ExpressRoute entre várias assinaturas.</span><span class="sxs-lookup"><span data-stu-id="c232a-135">The figure below shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="c232a-136">Cada uma das nuvens menores dentro da nuvem grande é usada para representar assinaturas pertencentes a diferentes departamentos dentro de uma organização.</span><span class="sxs-lookup"><span data-stu-id="c232a-136">Each of the smaller clouds within the large cloud is used to represent subscriptions that belong to different departments within an organization.</span></span> <span data-ttu-id="c232a-137">Cada um dos departamentos dentro da organização pode usar sua própria assinatura para implantar seus serviços, mas pode compartilhar um único circuito do ExpressRoute para se conectar de volta à respectiva rede local.</span><span class="sxs-lookup"><span data-stu-id="c232a-137">Each of the departments within the organization can use their own subscription for deploying their services--but they can share a single ExpressRoute circuit to connect back to your on-premises network.</span></span> <span data-ttu-id="c232a-138">Um único departamento (neste exemplo: TI) pode ter o circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c232a-138">A single department (in this example: IT) can own the ExpressRoute circuit.</span></span> <span data-ttu-id="c232a-139">Outras assinaturas dentro da organização podem usar o circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c232a-139">Other subscriptions within the organization can use the ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="c232a-140">As cobranças por conectividade e largura de banda do circuito dedicado serão aplicadas ao proprietário do circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c232a-140">Connectivity and bandwidth charges for the dedicated circuit will be applied to the ExpressRoute Circuit Owner.</span></span> <span data-ttu-id="c232a-141">Todas as redes virtuais compartilham a mesma largura de banda.</span><span class="sxs-lookup"><span data-stu-id="c232a-141">All virtual networks share the same bandwidth.</span></span>
> 
> 

![Conectividade entre assinaturas](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="c232a-143">Administração – proprietários e usuários do circuito</span><span class="sxs-lookup"><span data-stu-id="c232a-143">Administration - Circuit Owners and Circuit Users</span></span>

<span data-ttu-id="c232a-144">O 'proprietário do circuito' é um usuário avançado autorizado do recurso de circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c232a-144">The 'Circuit Owner' is an authorized Power User of the ExpressRoute circuit resource.</span></span> <span data-ttu-id="c232a-145">O proprietário do circuito pode criar autorizações que podem ser resgatadas pelos 'usuários do circuito'.</span><span class="sxs-lookup"><span data-stu-id="c232a-145">The Circuit Owner can create authorizations that can be redeemed by 'Circuit Users'.</span></span> <span data-ttu-id="c232a-146">Usuários do circuito são proprietários de gateways de rede virtual que não estão na mesma assinatura que o circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c232a-146">Circuit Users are owners of virtual network gateways that are not within the same subscription as the ExpressRoute circuit.</span></span> <span data-ttu-id="c232a-147">Usuários do circuito podem resgatar autorizações (uma autorização por rede virtual).</span><span class="sxs-lookup"><span data-stu-id="c232a-147">Circuit Users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="c232a-148">O proprietário do circuito tem a capacidade de modificar e revogar autorizações a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="c232a-148">The Circuit Owner has the power to modify and revoke authorizations at any time.</span></span> <span data-ttu-id="c232a-149">Revogar uma autorização faz com que todas as conexões de links sejam excluídas da assinatura cujo acesso foi revogado.</span><span class="sxs-lookup"><span data-stu-id="c232a-149">When an authorization is revoked, all link connections are deleted from the subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="c232a-150">Operações do proprietário do circuito</span><span class="sxs-lookup"><span data-stu-id="c232a-150">Circuit Owner operations</span></span>

<span data-ttu-id="c232a-151">**Criar uma autorização**</span><span class="sxs-lookup"><span data-stu-id="c232a-151">**To create an authorization**</span></span>

<span data-ttu-id="c232a-152">O proprietário do circuito cria uma autorização, que por sua vez cria uma chave de autorização que pode ser usada por um usuário do circuito para conectar seus gateways de rede virtual ao circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c232a-152">The Circuit Owner creates an authorization, which creates an authorization key that can be used by a Circuit User to connect their virtual network gateways to the ExpressRoute circuit.</span></span> <span data-ttu-id="c232a-153">Uma autorização é válida apenas para uma conexão.</span><span class="sxs-lookup"><span data-stu-id="c232a-153">An authorization is valid for only one connection.</span></span>

<span data-ttu-id="c232a-154">O exemplo a seguir mostra como criar uma autorização:</span><span class="sxs-lookup"><span data-stu-id="c232a-154">The following example shows how to create an authorization:</span></span>

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization
```

<span data-ttu-id="c232a-155">A resposta para isso conterá a chave de autorização e o status:</span><span class="sxs-lookup"><span data-stu-id="c232a-155">The response contains the authorization key and status:</span></span>

```azurecli
"authorizationKey": "0a7f3020-541f-4b4b-844a-5fb43472e3d7",
"authorizationUseStatus": "Available",
"etag": "W/\"010353d4-8955-4984-807a-585c21a22ae0\"",
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/authorizations/MyAuthorization1",
"name": "MyAuthorization1",
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup"
```

<span data-ttu-id="c232a-156">**Examinar autorizações**</span><span class="sxs-lookup"><span data-stu-id="c232a-156">**To review authorizations**</span></span>

<span data-ttu-id="c232a-157">O proprietário do circuito pode examinar todas as autorizações emitidas em um circuito específico executando o seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="c232a-157">The Circuit Owner can review all authorizations that are issued on a particular circuit by running the following example:</span></span>

```azurecli
az network express-route auth list --circuit-name MyCircuit -g ExpressRouteResourceGroup
```

<span data-ttu-id="c232a-158">**Adicionar autorizações**</span><span class="sxs-lookup"><span data-stu-id="c232a-158">**To add authorizations**</span></span>

<span data-ttu-id="c232a-159">O proprietário do circuito pode adicionar autorizações usando o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="c232a-159">The Circuit Owner can add authorizations by using the following example:</span></span>

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

<span data-ttu-id="c232a-160">**Excluir autorizações**</span><span class="sxs-lookup"><span data-stu-id="c232a-160">**To delete authorizations**</span></span>

<span data-ttu-id="c232a-161">O proprietário do circuito pode revogar/excluir autorizações usando o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="c232a-161">The Circuit Owner can revoke/delete authorizations to the user by running the following example:</span></span>

```azurecli
az network express-route auth delete --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

### <a name="circuit-user-operations"></a><span data-ttu-id="c232a-162">Operações do usuário do circuito</span><span class="sxs-lookup"><span data-stu-id="c232a-162">Circuit User operations</span></span>

<span data-ttu-id="c232a-163">O usuário do circuito precisa da ID do par e de uma chave de autorização do proprietário do circuito.</span><span class="sxs-lookup"><span data-stu-id="c232a-163">The Circuit User needs the peer ID and an authorization key from the Circuit Owner.</span></span> <span data-ttu-id="c232a-164">A chave de autorização é um GUID.</span><span class="sxs-lookup"><span data-stu-id="c232a-164">The authorization key is a GUID.</span></span>

```azurecli
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

<span data-ttu-id="c232a-165">**Resgatar uma autorização de conexão**</span><span class="sxs-lookup"><span data-stu-id="c232a-165">**To redeem a connection authorization**</span></span>

<span data-ttu-id="c232a-166">O usuário de circuito pode executar o seguinte exemplo para resgatar uma autorização de vínculo:</span><span class="sxs-lookup"><span data-stu-id="c232a-166">The Circuit User can run the following example to redeem a link authorization:</span></span>

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit --authorization-key "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

<span data-ttu-id="c232a-167">**Liberar uma autorização de conexão**</span><span class="sxs-lookup"><span data-stu-id="c232a-167">**To release a connection authorization**</span></span>

<span data-ttu-id="c232a-168">É possível liberar uma autorização excluindo a conexão que vincula o circuito do ExpressRoute à rede virtual.</span><span class="sxs-lookup"><span data-stu-id="c232a-168">You can release an authorization by deleting the connection that links the ExpressRoute circuit to the virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c232a-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c232a-169">Next steps</span></span>

<span data-ttu-id="c232a-170">Para obter mais informações sobre o ExpressRoute, consulte [Perguntas Frequentes sobre ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="c232a-170">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>