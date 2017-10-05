---
title: 'Vincular uma rede virtual a um circuito ExpressRoute: portal do Azure | Microsoft Docs'
description: "Este documento apresenta uma visão geral de como vincular redes virtuais (VNets) a circuitos do ExpressRoute."
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
ms.openlocfilehash: 595c30ab5d9adc6061ad753d952adf894ba80b2f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-a-virtual-network-to-an-expressroute-circuit"></a><span data-ttu-id="f2aaa-103">Conectar uma rede virtual a um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="f2aaa-103">Connect a virtual network to an ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f2aaa-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f2aaa-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="f2aaa-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f2aaa-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="f2aaa-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="f2aaa-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="f2aaa-107">Vídeo – Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f2aaa-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="f2aaa-108">PowerShell (clássico)</span><span class="sxs-lookup"><span data-stu-id="f2aaa-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
> 

<span data-ttu-id="f2aaa-109">Este artigo ajuda você a vincular as redes virtuais (VNets) aos circuitos do Azure ExpressRoute usando o modelo de implantação do Resource Manager e o Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-109">This article helps you link virtual networks (VNets) to Azure ExpressRoute circuits by using the Resource Manager deployment model and the Azure portal.</span></span> <span data-ttu-id="f2aaa-110">As redes virtuais podem estar na mesma assinatura ou fazer parte de outra assinatura.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-110">Virtual networks can either be in the same subscription, or they can be part of another subscription.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f2aaa-111">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="f2aaa-111">Before you begin</span></span>
* <span data-ttu-id="f2aaa-112">Analise os [pré-requisitos](expressroute-prerequisites.md), os [requisitos de roteamento](expressroute-routing.md) e os [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-112">Review the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="f2aaa-113">Você deve ter um circuito do ExpressRoute ativo.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-113">You must have an active ExpressRoute circuit.</span></span>
  
  * <span data-ttu-id="f2aaa-114">Siga as instruções para [criar um circuito do ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) e para que o circuito seja habilitado pelo provedor de conectividade.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-114">Follow the instructions to [create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have the circuit enabled by your connectivity provider.</span></span>
  * <span data-ttu-id="f2aaa-115">Verifique se o emparelhamento privado do Azure está configurado para seu circuito.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-115">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="f2aaa-116">Veja o artigo [Configurar roteamento](expressroute-howto-routing-portal-resource-manager.md) para obter instruções sobre roteamento.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-116">See the [Configure routing](expressroute-howto-routing-portal-resource-manager.md) article for routing instructions.</span></span>
  * <span data-ttu-id="f2aaa-117">Verifique se o emparelhamento privado do Azure está configurado e se o emparelhamento BGP entre sua rede e a Microsoft está ativo para que você possa habilitar a conectividade de ponta a ponta.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-117">Ensure that Azure private peering is configured and the BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="f2aaa-118">Verifique se tem uma rede virtual e um gateway de rede virtual criados e totalmente provisionados.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-118">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="f2aaa-119">Siga as instruções para [criar um gateway de rede virtual para ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="f2aaa-119">Follow the instructions to [create a virtual network gateway for ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="f2aaa-120">Um gateway de rede virtual para ExpressRoute usa o GatewayType “ExpressRoute”, não VPN.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-120">A virtual network gateway for ExpressRoute uses the GatewayType 'ExpressRoute', not VPN.</span></span>

* <span data-ttu-id="f2aaa-121">Você pode vincular até 10 redes virtuais a um circuito de ExpressRoute padrão.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-121">You can link up to 10 virtual networks to a standard ExpressRoute circuit.</span></span> <span data-ttu-id="f2aaa-122">Todas as redes virtuais deverão estar na mesma região geopolítica ao usar um circuito de ExpressRoute padrão.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-122">All virtual networks must be in the same geopolitical region when using a standard ExpressRoute circuit.</span></span> 
* <span data-ttu-id="f2aaa-123">Você poderá vincular uma rede virtual fora da região geopolítica do circuito do ExpressRoute ou conectar um grande número de redes virtuais ao circuito do ExpressRoute, se tiver habilitado o complemento premium do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-123">You can link a virtual network outside of the geopolitical region of the ExpressRoute circuit, or connect a larger number of virtual networks to your ExpressRoute circuit if you enabled the ExpressRoute premium add-on.</span></span> <span data-ttu-id="f2aaa-124">Confira as [perguntas frequentes](expressroute-faqs.md) para obter mais detalhes sobre o complemento premium.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-124">Check the [FAQ](expressroute-faqs.md) for more details on the premium add-on.</span></span>
* <span data-ttu-id="f2aaa-125">Você pode [exibir um vídeo](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit) antes de começar para entender melhor as etapas.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-125">You can [view a video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit) before beginning to better understand the steps.</span></span>

## <a name="connect-a-virtual-network-in-the-same-subscription-to-a-circuit"></a><span data-ttu-id="f2aaa-126">Conectar uma rede virtual na mesma assinatura a um circuito</span><span class="sxs-lookup"><span data-stu-id="f2aaa-126">Connect a virtual network in the same subscription to a circuit</span></span>

### <a name="to-create-a-connection"></a><span data-ttu-id="f2aaa-127">Para criar uma conexão</span><span class="sxs-lookup"><span data-stu-id="f2aaa-127">To create a connection</span></span>

> [!NOTE]
> <span data-ttu-id="f2aaa-128">As informações de configuração do BGP não aparecerão se o provedor de camada 3 tiver configurado seus emparelhamentos.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-128">BGP configuration information will not show up if the layer 3 provider configured your peerings.</span></span> <span data-ttu-id="f2aaa-129">Se o circuito estiver no estado de provisionamento, você poderá criar conexões.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-129">If your circuit is in a provisioned state, you should be able to create connections.</span></span>
>

1. <span data-ttu-id="f2aaa-130">Certifique-se de que o circuito de ExpressRoute e emparelhamento privado do Azure foram configurados com êxito.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-130">Ensure that your ExpressRoute circuit and Azure private peering have been configured successfully.</span></span> <span data-ttu-id="f2aaa-131">Siga as instruções nos artigos [Criar um circuito do ExpressRoute](expressroute-howto-circuit-arm.md) e [Configurar o roteamento](expressroute-howto-routing-arm.md).</span><span class="sxs-lookup"><span data-stu-id="f2aaa-131">Follow the instructions in [Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and [Configure routing](expressroute-howto-routing-arm.md).</span></span> <span data-ttu-id="f2aaa-132">O circuito do ExpressRoute deve se parecer com a imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="f2aaa-132">Your ExpressRoute circuit should look like the following image:</span></span>

    ![Captura de tela de circuito do ExpressRoute](./media/expressroute-howto-linkvnet-portal-resource-manager/routing1.png)
   
2. <span data-ttu-id="f2aaa-134">Agora, você pode começar a provisionar uma conexão para vincular seu gateway de rede virtual ao circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-134">You can now start provisioning a connection to link your virtual network gateway to your ExpressRoute circuit.</span></span> <span data-ttu-id="f2aaa-135">Clique em **Conexão** > **Adicionar** para abrir a folha **Adicionar conexão** e, em seguida, configure os valores.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-135">Click **Connection** > **Add** to open the **Add connection** blade, and then configure the values.</span></span>

    ![Adicionar a captura de tela de conexão](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub1.png)  

3. <span data-ttu-id="f2aaa-137">Depois que sua conexão foi configurada com êxito, seu objeto de conexão mostrará as informações para a conexão.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-137">After your connection has been successfully configured, your connection object will show the information for the connection.</span></span>

     ![Captura de tela de objeto de conexão](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub2.png)

### <a name="to-delete-a-connection"></a><span data-ttu-id="f2aaa-139">Para excluir uma conexão</span><span class="sxs-lookup"><span data-stu-id="f2aaa-139">To delete a connection</span></span>
<span data-ttu-id="f2aaa-140">Você pode excluir uma conexão selecionando o ícone **Excluir** na folha de sua conexão.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-140">You can delete a connection by selecting the **Delete** icon on the blade for your connection.</span></span>

## <a name="connect-a-virtual-network-in-a-different-subscription-to-a-circuit"></a><span data-ttu-id="f2aaa-141">Conectar uma rede virtual em uma assinatura diferente a um circuito</span><span class="sxs-lookup"><span data-stu-id="f2aaa-141">Connect a virtual network in a different subscription to a circuit</span></span>
<span data-ttu-id="f2aaa-142">Você pode compartilhar um circuito do ExpressRoute entre várias assinaturas.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-142">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="f2aaa-143">A figura abaixo mostra um esquema simples de como funciona o compartilhamento de circuitos do ExpressRoute entre várias assinaturas.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-143">The figure below shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

![Conectividade entre assinaturas](./media/expressroute-howto-linkvnet-portal-resource-manager/cross-subscription.png)

- <span data-ttu-id="f2aaa-145">Cada uma das nuvens menores dentro da nuvem grande é usada para representar assinaturas pertencentes a diferentes departamentos dentro de uma organização.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-145">Each of the smaller clouds within the large cloud is used to represent subscriptions that belong to different departments within an organization.</span></span>
- <span data-ttu-id="f2aaa-146">Cada um dos departamentos dentro da organização pode usar sua própria assinatura para implantar seus serviços, mas pode compartilhar um único circuito do ExpressRoute para se conectar de volta à respectiva rede local.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-146">Each of the departments within the organization can use their own subscription for deploying their services, but they can share a single ExpressRoute circuit to connect back to your on-premises network.</span></span>
- <span data-ttu-id="f2aaa-147">Um único departamento (neste exemplo: TI) pode ter o circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-147">A single department (in this example: IT) can own the ExpressRoute circuit.</span></span> <span data-ttu-id="f2aaa-148">Outras assinaturas dentro da organização podem usar o circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-148">Other subscriptions within the organization can use the ExpressRoute circuit.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f2aaa-149">As cobranças por conectividade e largura de banda do circuito dedicado serão aplicadas ao proprietário do circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-149">Connectivity and bandwidth charges for the dedicated circuit will be applied to the ExpressRoute circuit owner.</span></span> <span data-ttu-id="f2aaa-150">Todas as redes virtuais compartilham a mesma largura de banda.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-150">All virtual networks share the same bandwidth.</span></span>
    > 
    >

### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="f2aaa-151">Administração – proprietários e usuários do circuito</span><span class="sxs-lookup"><span data-stu-id="f2aaa-151">Administration - circuit owners and circuit users</span></span>

<span data-ttu-id="f2aaa-152">O “proprietário do circuito” é um usuário avançado autorizado do recurso de circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-152">The 'circuit owner' is an authorized Power User of the ExpressRoute circuit resource.</span></span> <span data-ttu-id="f2aaa-153">O proprietário do circuito pode criar autorizações que podem ser resgatadas pelos ‘usuários do circuito’.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-153">The circuit owner can create authorizations that can be redeemed by 'circuit users'.</span></span> <span data-ttu-id="f2aaa-154">Usuários do circuito são proprietários de gateways de rede virtual que não estão na mesma assinatura que o circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-154">Circuit users are owners of virtual network gateways that are not within the same subscription as the ExpressRoute circuit.</span></span> <span data-ttu-id="f2aaa-155">Usuários do circuito podem resgatar autorizações (uma autorização por rede virtual).</span><span class="sxs-lookup"><span data-stu-id="f2aaa-155">Circuit users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="f2aaa-156">O proprietário do circuito tem a capacidade de modificar e revogar autorizações a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-156">The circuit owner has the power to modify and revoke authorizations at any time.</span></span> <span data-ttu-id="f2aaa-157">Revogar uma autorização faz com que todas as conexões de links sejam excluídas da assinatura cujo acesso foi revogado.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-157">Revoking an authorization results in all link connections being deleted from the subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="f2aaa-158">Operações do proprietário do circuito</span><span class="sxs-lookup"><span data-stu-id="f2aaa-158">Circuit owner operations</span></span>

<span data-ttu-id="f2aaa-159">**Criar uma autorização de conexão**</span><span class="sxs-lookup"><span data-stu-id="f2aaa-159">**To create a connection authorization**</span></span>

<span data-ttu-id="f2aaa-160">O proprietário do circuito cria uma autorização.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-160">The circuit owner creates an authorization.</span></span> <span data-ttu-id="f2aaa-161">Isso resulta na criação de uma chave de autorização que pode ser usada por um usuário do circuito para conectar seus gateways de rede virtual ao circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-161">This results in the creation of an authorization key that can be used by a circuit user to connect their virtual network gateways to the ExpressRoute circuit.</span></span> <span data-ttu-id="f2aaa-162">Uma autorização é válida apenas para uma conexão.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-162">An authorization is valid for only one connection.</span></span>

1. <span data-ttu-id="f2aaa-163">Na folha ExpressRoute, clique em **Autorizações** e, em seguida, digite um **nome** para a autorização e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-163">In the ExpressRoute blade, Click **Authorizations** and then type a **name** for the authorization and click **Save**.</span></span>

    ![Autorizações](./media/expressroute-howto-linkvnet-portal-resource-manager/authorization.png)

2. <span data-ttu-id="f2aaa-165">Após a gravação da configuração, copie a **ID do Recurso** e a **Chave de Autorização**.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-165">Once the configuration is saved, copy the **Resource ID** and the **Authorization Key**.</span></span>

    ![Chave de autorização](./media/expressroute-howto-linkvnet-portal-resource-manager/authkey.png)

<span data-ttu-id="f2aaa-167">**Excluir uma autorização de conexão**</span><span class="sxs-lookup"><span data-stu-id="f2aaa-167">**To delete a connection authorization**</span></span>

<span data-ttu-id="f2aaa-168">Você pode excluir uma conexão selecionando o ícone **Excluir** na folha de sua conexão.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-168">You can delete a connection by selecting the **Delete** icon on the blade for your connection.</span></span>

### <a name="circuit-user-operations"></a><span data-ttu-id="f2aaa-169">Operações do usuário do circuito</span><span class="sxs-lookup"><span data-stu-id="f2aaa-169">Circuit user operations</span></span>

<span data-ttu-id="f2aaa-170">O usuário do circuito precisa da ID do recurso e de uma chave de autorização do proprietário do circuito.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-170">The circuit user needs the resource ID and an authorization key from the circuit owner.</span></span> 

<span data-ttu-id="f2aaa-171">**Resgatar uma autorização de conexão**</span><span class="sxs-lookup"><span data-stu-id="f2aaa-171">**To redeem a connection authorization**</span></span>

1.  <span data-ttu-id="f2aaa-172">Clique no botão **+Novo**.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-172">Click the **+New** button.</span></span>

    ![Clique em Novo](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection1.png)

2.  <span data-ttu-id="f2aaa-174">Pesquise **“Conexão”** no Marketplace, selecione-a e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-174">Search for **"Connection"** in the Marketplace, select it, and click **Create**.</span></span>

    ![Pesquisar conexão](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection2.png)

3.  <span data-ttu-id="f2aaa-176">Verifique se o **Tipo de conexão** está definido como "ExpressRoute".</span><span class="sxs-lookup"><span data-stu-id="f2aaa-176">Make sure the **Connection type** is set to "ExpressRoute".</span></span>


4.  <span data-ttu-id="f2aaa-177">Preencha os detalhes e clique em **OK** na folha Conceitos básicos.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-177">Fill in the details, then click **OK** in the Basics blade.</span></span>

    ![Folha de Noções básicas](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection3.png)

5.  <span data-ttu-id="f2aaa-179">Na folha **Configurações**, selecione **Gateway de rede virtual** e marque a caixa de seleção **Resgatar autorização**.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-179">In the **Settings** blade, Select the **Virtual network gateway** and check the **Redeem authorization** check box.</span></span>

6.  <span data-ttu-id="f2aaa-180">Insira a **Chave de autorização** e o **URI do circuito par** e nomeie a conexão.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-180">Enter the **Authorization key** and the **Peer circuit URI** and give the connection a name.</span></span> <span data-ttu-id="f2aaa-181">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-181">Click **OK**.</span></span>

    ![Folha de configurações](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection4.png)

7. <span data-ttu-id="f2aaa-183">Examine as informações na folha **Resumo** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-183">Review the information in the **Summary** blade and click **OK**.</span></span>


<span data-ttu-id="f2aaa-184">**Liberar uma autorização de conexão**</span><span class="sxs-lookup"><span data-stu-id="f2aaa-184">**To release a connection authorization**</span></span>

<span data-ttu-id="f2aaa-185">É possível liberar uma autorização excluindo a conexão que vincula o circuito do ExpressRoute à rede virtual.</span><span class="sxs-lookup"><span data-stu-id="f2aaa-185">You can release an authorization by deleting the connection that links the ExpressRoute circuit to the virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2aaa-186">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f2aaa-186">Next steps</span></span>
<span data-ttu-id="f2aaa-187">Para obter mais informações sobre o ExpressRoute, consulte [Perguntas Frequentes sobre ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="f2aaa-187">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
