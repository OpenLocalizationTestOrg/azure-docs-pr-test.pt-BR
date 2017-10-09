---
title: 'Vincular um circuito de rota expressa do tooan de rede virtual: portal do Azure | Microsoft Docs'
description: "Este documento fornece uma visão geral de como toolink virtual redes circuitos de tooExpressRoute (VNets)."
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f5cb5441-2fba-46d9-99a5-d1d586e7bda4
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: cherylmc
ms.openlocfilehash: 8bedcb11df7e30281fd439afdfb76cc67626a8f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="8285f-103">Conectar uma rede virtual de tooan circuito de rota expressa</span><span class="sxs-lookup"><span data-stu-id="8285f-103">Connect a virtual network tooan ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8285f-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="8285f-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="8285f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8285f-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="8285f-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="8285f-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="8285f-107">Vídeo – Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="8285f-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="8285f-108">PowerShell (clássico)</span><span class="sxs-lookup"><span data-stu-id="8285f-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
> 

<span data-ttu-id="8285f-109">Este artigo ajuda você a vincular circuitos do ExpressRoute tooAzure redes virtuais (VNets) usando o modelo de implantação do Gerenciador de recursos de saudação e Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8285f-109">This article helps you link virtual networks (VNets) tooAzure ExpressRoute circuits by using hello Resource Manager deployment model and hello Azure portal.</span></span> <span data-ttu-id="8285f-110">Redes virtuais podem ser na Olá mesma assinatura, ou eles podem fazer parte de outra assinatura.</span><span class="sxs-lookup"><span data-stu-id="8285f-110">Virtual networks can either be in hello same subscription, or they can be part of another subscription.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8285f-111">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="8285f-111">Before you begin</span></span>
* <span data-ttu-id="8285f-112">Saudação de revisão [pré-requisitos](expressroute-prerequisites.md), [requisitos de roteamento](expressroute-routing.md), e [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração.</span><span class="sxs-lookup"><span data-stu-id="8285f-112">Review hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="8285f-113">Você deve ter um circuito do ExpressRoute ativo.</span><span class="sxs-lookup"><span data-stu-id="8285f-113">You must have an active ExpressRoute circuit.</span></span>
  
  * <span data-ttu-id="8285f-114">Siga as instruções de saudação muito[criar um circuito de rota expressa](expressroute-howto-circuit-portal-resource-manager.md) e ter circuito Olá habilitado por seu provedor de conectividade.</span><span class="sxs-lookup"><span data-stu-id="8285f-114">Follow hello instructions too[create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have hello circuit enabled by your connectivity provider.</span></span>
  * <span data-ttu-id="8285f-115">Verifique se o emparelhamento privado do Azure está configurado para seu circuito.</span><span class="sxs-lookup"><span data-stu-id="8285f-115">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="8285f-116">Consulte Olá [Configurar roteamento](expressroute-howto-routing-portal-resource-manager.md) artigo para obter instruções de roteamentos.</span><span class="sxs-lookup"><span data-stu-id="8285f-116">See hello [Configure routing](expressroute-howto-routing-portal-resource-manager.md) article for routing instructions.</span></span>
  * <span data-ttu-id="8285f-117">Certifique-se de que o emparelhamento particular do Azure está configurado e Olá emparelhamento via protocolo BGP entre sua rede e a Microsoft está ativo para que você pode habilitar a conectividade de ponta a ponta.</span><span class="sxs-lookup"><span data-stu-id="8285f-117">Ensure that Azure private peering is configured and hello BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="8285f-118">Verifique se tem uma rede virtual e um gateway de rede virtual criados e totalmente provisionados.</span><span class="sxs-lookup"><span data-stu-id="8285f-118">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="8285f-119">Siga as instruções de saudação muito[criar um gateway de rede virtual para o ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="8285f-119">Follow hello instructions too[create a virtual network gateway for ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="8285f-120">Um gateway de rede virtual para a rota expressa usa Olá GatewayType 'ExpressRoute', não VPN.</span><span class="sxs-lookup"><span data-stu-id="8285f-120">A virtual network gateway for ExpressRoute uses hello GatewayType 'ExpressRoute', not VPN.</span></span>

* <span data-ttu-id="8285f-121">Você pode vincular o circuito de rota expressa padrão do too10 redes virtuais tooa.</span><span class="sxs-lookup"><span data-stu-id="8285f-121">You can link up too10 virtual networks tooa standard ExpressRoute circuit.</span></span> <span data-ttu-id="8285f-122">Todas as redes virtuais devem estar em Olá mesma região geopolíticas ao usar um circuito de rota expressa padrão.</span><span class="sxs-lookup"><span data-stu-id="8285f-122">All virtual networks must be in hello same geopolitical region when using a standard ExpressRoute circuit.</span></span> 
* <span data-ttu-id="8285f-123">Você pode vincular uma rede virtual fora da região geopolíticas Olá Olá circuito de rota expressa ou conectar-se um grande número de redes virtuais tooyour circuito de rota expressa se você habilitou o complemento do premium Olá rota expressa.</span><span class="sxs-lookup"><span data-stu-id="8285f-123">You can link a virtual network outside of hello geopolitical region of hello ExpressRoute circuit, or connect a larger number of virtual networks tooyour ExpressRoute circuit if you enabled hello ExpressRoute premium add-on.</span></span> <span data-ttu-id="8285f-124">Verificar Olá [perguntas frequentes sobre](expressroute-faqs.md) para obter mais detalhes sobre o complemento do premium Olá.</span><span class="sxs-lookup"><span data-stu-id="8285f-124">Check hello [FAQ](expressroute-faqs.md) for more details on hello premium add-on.</span></span>
* <span data-ttu-id="8285f-125">Você pode [exibir um vídeo](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit) antes de toobetter início entender as etapas de saudação.</span><span class="sxs-lookup"><span data-stu-id="8285f-125">You can [view a video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit) before beginning toobetter understand hello steps.</span></span>

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a><span data-ttu-id="8285f-126">Conectar uma rede virtual no hello mesmo circuito de tooa de assinatura</span><span class="sxs-lookup"><span data-stu-id="8285f-126">Connect a virtual network in hello same subscription tooa circuit</span></span>

### <a name="toocreate-a-connection"></a><span data-ttu-id="8285f-127">toocreate uma conexão</span><span class="sxs-lookup"><span data-stu-id="8285f-127">toocreate a connection</span></span>

> [!NOTE]
> <span data-ttu-id="8285f-128">Informações de configuração de BGP não aparecerá se o provedor de camada 3 Olá configurado seu emparelhamentos.</span><span class="sxs-lookup"><span data-stu-id="8285f-128">BGP configuration information will not show up if hello layer 3 provider configured your peerings.</span></span> <span data-ttu-id="8285f-129">Se o circuito está em um estado de provisionamento, você deve ser capaz de toocreate conexões.</span><span class="sxs-lookup"><span data-stu-id="8285f-129">If your circuit is in a provisioned state, you should be able toocreate connections.</span></span>
>

1. <span data-ttu-id="8285f-130">Certifique-se de que o circuito de ExpressRoute e emparelhamento privado do Azure foram configurados com êxito.</span><span class="sxs-lookup"><span data-stu-id="8285f-130">Ensure that your ExpressRoute circuit and Azure private peering have been configured successfully.</span></span> <span data-ttu-id="8285f-131">Siga as instruções de saudação em [criar um circuito ExpressRoute](expressroute-howto-circuit-arm.md) e [Configurar roteamento](expressroute-howto-routing-arm.md).</span><span class="sxs-lookup"><span data-stu-id="8285f-131">Follow hello instructions in [Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and [Configure routing](expressroute-howto-routing-arm.md).</span></span> <span data-ttu-id="8285f-132">O circuito de rota expressa deve ter aparência Olá a imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="8285f-132">Your ExpressRoute circuit should look like hello following image:</span></span>

    ![Captura de tela de circuito do ExpressRoute](./media/expressroute-howto-linkvnet-portal-resource-manager/routing1.png)
   
2. <span data-ttu-id="8285f-134">Agora você pode começar o provisionamento de uma conexão toolink seu gateway de rede virtual tooyour circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="8285f-134">You can now start provisioning a connection toolink your virtual network gateway tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="8285f-135">Clique em **Conexão** > **adicionar** tooopen Olá **Adicionar conexão** folha e, em seguida, configure os valores de saudação.</span><span class="sxs-lookup"><span data-stu-id="8285f-135">Click **Connection** > **Add** tooopen hello **Add connection** blade, and then configure hello values.</span></span>

    ![Adicionar a captura de tela de conexão](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub1.png)  

3. <span data-ttu-id="8285f-137">Depois que a conexão tiver sido configurado com êxito, seu objeto de conexão mostrará informações Olá para conexão hello.</span><span class="sxs-lookup"><span data-stu-id="8285f-137">After your connection has been successfully configured, your connection object will show hello information for hello connection.</span></span>

     ![Captura de tela de objeto de conexão](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub2.png)

### <a name="toodelete-a-connection"></a><span data-ttu-id="8285f-139">toodelete uma conexão</span><span class="sxs-lookup"><span data-stu-id="8285f-139">toodelete a connection</span></span>
<span data-ttu-id="8285f-140">Você pode excluir uma conexão selecionando Olá **excluir** ícone na folha de saudação para sua conexão.</span><span class="sxs-lookup"><span data-stu-id="8285f-140">You can delete a connection by selecting hello **Delete** icon on hello blade for your connection.</span></span>

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a><span data-ttu-id="8285f-141">Conectar uma rede virtual em um circuito de tooa assinatura diferente</span><span class="sxs-lookup"><span data-stu-id="8285f-141">Connect a virtual network in a different subscription tooa circuit</span></span>
<span data-ttu-id="8285f-142">Você pode compartilhar um circuito do ExpressRoute entre várias assinaturas.</span><span class="sxs-lookup"><span data-stu-id="8285f-142">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="8285f-143">a Figura Olá abaixo mostra um esquemático simples de como funciona o compartilhamento para circuitos ExpressRoute entre várias assinaturas.</span><span class="sxs-lookup"><span data-stu-id="8285f-143">hello figure below shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

![Conectividade entre assinaturas](./media/expressroute-howto-linkvnet-portal-resource-manager/cross-subscription.png)

- <span data-ttu-id="8285f-145">Cada uma das nuvens menores de saudação dentro da nuvem grande Olá é toorepresent usadas assinaturas que pertencem a toodifferent departamentos dentro de uma organização.</span><span class="sxs-lookup"><span data-stu-id="8285f-145">Each of hello smaller clouds within hello large cloud is used toorepresent subscriptions that belong toodifferent departments within an organization.</span></span>
- <span data-ttu-id="8285f-146">Cada um dos departamentos hello dentro da organização Olá pode usar sua própria assinatura para implantar seus serviços, mas eles podem compartilhar uma única rede rota expressa circuito tooconnect tooyour back local.</span><span class="sxs-lookup"><span data-stu-id="8285f-146">Each of hello departments within hello organization can use their own subscription for deploying their services, but they can share a single ExpressRoute circuit tooconnect back tooyour on-premises network.</span></span>
- <span data-ttu-id="8285f-147">Um único departamento (neste exemplo: IT) pode ter o circuito de rota expressa hello.</span><span class="sxs-lookup"><span data-stu-id="8285f-147">A single department (in this example: IT) can own hello ExpressRoute circuit.</span></span> <span data-ttu-id="8285f-148">Outras assinaturas dentro da organização Olá podem usar o circuito de rota expressa hello.</span><span class="sxs-lookup"><span data-stu-id="8285f-148">Other subscriptions within hello organization can use hello ExpressRoute circuit.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8285f-149">Encargos de largura de banda e conectividade para o circuito dedicado de saudação será proprietário do circuito de rota expressa toohello aplicado.</span><span class="sxs-lookup"><span data-stu-id="8285f-149">Connectivity and bandwidth charges for hello dedicated circuit will be applied toohello ExpressRoute circuit owner.</span></span> <span data-ttu-id="8285f-150">Todas as redes virtuais compartilham Olá mesma largura de banda.</span><span class="sxs-lookup"><span data-stu-id="8285f-150">All virtual networks share hello same bandwidth.</span></span>
    > 
    >

### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="8285f-151">Administração – proprietários e usuários do circuito</span><span class="sxs-lookup"><span data-stu-id="8285f-151">Administration - circuit owners and circuit users</span></span>

<span data-ttu-id="8285f-152">Olá 'proprietário do circuito' é um usuário autorizado Power Olá recursos de circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="8285f-152">hello 'circuit owner' is an authorized Power User of hello ExpressRoute circuit resource.</span></span> <span data-ttu-id="8285f-153">proprietário do circuito Olá pode criar autorizações que podem ser trocadas por 'usuários do circuito'.</span><span class="sxs-lookup"><span data-stu-id="8285f-153">hello circuit owner can create authorizations that can be redeemed by 'circuit users'.</span></span> <span data-ttu-id="8285f-154">Os usuários do circuito são proprietários da rede virtual gateways que não estão no hello mesma assinatura conforme Olá circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="8285f-154">Circuit users are owners of virtual network gateways that are not within hello same subscription as hello ExpressRoute circuit.</span></span> <span data-ttu-id="8285f-155">Usuários do circuito podem resgatar autorizações (uma autorização por rede virtual).</span><span class="sxs-lookup"><span data-stu-id="8285f-155">Circuit users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="8285f-156">proprietário do circuito Olá tem autorizações de toomodify e revoke power Olá a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="8285f-156">hello circuit owner has hello power toomodify and revoke authorizations at any time.</span></span> <span data-ttu-id="8285f-157">Revogando uma resulta de autorização em todas as conexões de link que está sendo excluídas da assinatura de saudação cujo acesso foi revogado.</span><span class="sxs-lookup"><span data-stu-id="8285f-157">Revoking an authorization results in all link connections being deleted from hello subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="8285f-158">Operações do proprietário do circuito</span><span class="sxs-lookup"><span data-stu-id="8285f-158">Circuit owner operations</span></span>

<span data-ttu-id="8285f-159">**toocreate uma autorização de conexão**</span><span class="sxs-lookup"><span data-stu-id="8285f-159">**toocreate a connection authorization**</span></span>

<span data-ttu-id="8285f-160">proprietário do circuito Olá cria uma autorização.</span><span class="sxs-lookup"><span data-stu-id="8285f-160">hello circuit owner creates an authorization.</span></span> <span data-ttu-id="8285f-161">Isso resulta na criação de saudação de uma chave de autorização que pode ser usado por um tooconnect de usuário do circuito seu gateways de rede virtual toohello circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="8285f-161">This results in hello creation of an authorization key that can be used by a circuit user tooconnect their virtual network gateways toohello ExpressRoute circuit.</span></span> <span data-ttu-id="8285f-162">Uma autorização é válida apenas para uma conexão.</span><span class="sxs-lookup"><span data-stu-id="8285f-162">An authorization is valid for only one connection.</span></span>

1. <span data-ttu-id="8285f-163">Na folha de rota expressa hello, clique em **autorizações** e, em seguida, digite um **nome** para autorização hello e clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="8285f-163">In hello ExpressRoute blade, Click **Authorizations** and then type a **name** for hello authorization and click **Save**.</span></span>

    ![Autorizações](./media/expressroute-howto-linkvnet-portal-resource-manager/authorization.png)

2. <span data-ttu-id="8285f-165">Depois de salvo, configuração de saudação copiar Olá **ID de recurso** e hello **chave de autorização**.</span><span class="sxs-lookup"><span data-stu-id="8285f-165">Once hello configuration is saved, copy hello **Resource ID** and hello **Authorization Key**.</span></span>

    ![Chave de autorização](./media/expressroute-howto-linkvnet-portal-resource-manager/authkey.png)

<span data-ttu-id="8285f-167">**toodelete uma autorização de conexão**</span><span class="sxs-lookup"><span data-stu-id="8285f-167">**toodelete a connection authorization**</span></span>

<span data-ttu-id="8285f-168">Você pode excluir uma conexão selecionando Olá **excluir** ícone na folha de saudação para sua conexão.</span><span class="sxs-lookup"><span data-stu-id="8285f-168">You can delete a connection by selecting hello **Delete** icon on hello blade for your connection.</span></span>

### <a name="circuit-user-operations"></a><span data-ttu-id="8285f-169">Operações do usuário do circuito</span><span class="sxs-lookup"><span data-stu-id="8285f-169">Circuit user operations</span></span>

<span data-ttu-id="8285f-170">usuários do circuito Olá precisa Olá ID de recurso e uma chave de autorização do proprietário do circuito hello.</span><span class="sxs-lookup"><span data-stu-id="8285f-170">hello circuit user needs hello resource ID and an authorization key from hello circuit owner.</span></span> 

<span data-ttu-id="8285f-171">**tooredeem uma autorização de conexão**</span><span class="sxs-lookup"><span data-stu-id="8285f-171">**tooredeem a connection authorization**</span></span>

1.  <span data-ttu-id="8285f-172">Clique em Olá **+ novo** botão.</span><span class="sxs-lookup"><span data-stu-id="8285f-172">Click hello **+New** button.</span></span>

    ![Clique em Novo](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection1.png)

2.  <span data-ttu-id="8285f-174">Procurar **"Conexão"** em Olá Marketplace, selecione-o e clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="8285f-174">Search for **"Connection"** in hello Marketplace, select it, and click **Create**.</span></span>

    ![Pesquisar conexão](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection2.png)

3.  <span data-ttu-id="8285f-176">Verifique se Olá **o tipo de Conexão** está definido muito "Rota expressa".</span><span class="sxs-lookup"><span data-stu-id="8285f-176">Make sure hello **Connection type** is set too"ExpressRoute".</span></span>


4.  <span data-ttu-id="8285f-177">Preencha os detalhes de saudação, clique em **Okey** na folha de Noções básicas de saudação.</span><span class="sxs-lookup"><span data-stu-id="8285f-177">Fill in hello details, then click **OK** in hello Basics blade.</span></span>

    ![Folha de Noções básicas](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection3.png)

5.  <span data-ttu-id="8285f-179">Em Olá **configurações** folha, selecione Olá **gateway de rede Virtual** e verifique Olá **resgatar autorização** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="8285f-179">In hello **Settings** blade, Select hello **Virtual network gateway** and check hello **Redeem authorization** check box.</span></span>

6.  <span data-ttu-id="8285f-180">Digite hello **chave de autorização** e hello **par circuito URI** e dê um nome de conexão de saudação.</span><span class="sxs-lookup"><span data-stu-id="8285f-180">Enter hello **Authorization key** and hello **Peer circuit URI** and give hello connection a name.</span></span> <span data-ttu-id="8285f-181">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="8285f-181">Click **OK**.</span></span>

    ![Folha de configurações](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection4.png)

7. <span data-ttu-id="8285f-183">Revise as informações de Olá Olá **resumo** folha e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="8285f-183">Review hello information in hello **Summary** blade and click **OK**.</span></span>


<span data-ttu-id="8285f-184">**toorelease uma autorização de conexão**</span><span class="sxs-lookup"><span data-stu-id="8285f-184">**toorelease a connection authorization**</span></span>

<span data-ttu-id="8285f-185">Você pode liberar uma autorização Excluindo conexão Olá que vincula a rede virtual de toohello Olá de circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="8285f-185">You can release an authorization by deleting hello connection that links hello ExpressRoute circuit toohello virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8285f-186">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8285f-186">Next steps</span></span>
<span data-ttu-id="8285f-187">Para obter mais informações sobre a rota expressa, consulte Olá [perguntas Frequentes do ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="8285f-187">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
