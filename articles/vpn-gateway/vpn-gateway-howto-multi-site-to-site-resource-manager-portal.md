---
title: "Adicionar várias tooa de conexões de gateway Site a Site VPN VNet: Portal do Azure: o Gerenciador de recursos | Microsoft Docs"
description: "Adicionar vários S2S conexões tooa gateway VPN de site que tem uma conexão existente"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f3e8b165-f20a-42ab-afbb-bf60974bb4b1
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/20/2017
ms.author: cherylmc
ms.openlocfilehash: b8c9ff454967f509dcef725f8bcec8564fad9b00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-site-to-site-connection-tooa-vnet-with-an-existing-vpn-gateway-connection"></a><span data-ttu-id="24f0c-103">Adicionar um tooa de conexão Site a Site VNet com uma conexão de gateway VPN existente</span><span class="sxs-lookup"><span data-stu-id="24f0c-103">Add a Site-to-Site connection tooa VNet with an existing VPN gateway connection</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="24f0c-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="24f0c-104">Azure portal</span></span>](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="24f0c-105">PowerShell (clássico)</span><span class="sxs-lookup"><span data-stu-id="24f0c-105">PowerShell (classic)</span></span>](vpn-gateway-multi-site.md)
>
> 

<span data-ttu-id="24f0c-106">Este artigo orienta você a usar o hello tooadd portal do Azure Site a Site (S2S) conexões tooa gateway VPN que tenha uma conexão existente.</span><span class="sxs-lookup"><span data-stu-id="24f0c-106">This article walks you through using hello Azure portal tooadd Site-to-Site (S2S) connections tooa VPN gateway that has an existing connection.</span></span> <span data-ttu-id="24f0c-107">Esse tipo de conexão geralmente é chamado tooas uma configuração de "multissite".</span><span class="sxs-lookup"><span data-stu-id="24f0c-107">This type of connection is often referred tooas a "multi-site" configuration.</span></span> <span data-ttu-id="24f0c-108">Você pode adicionar uma conexão de S2S tooa VNet que já tem uma conexão S2S, uma conexão ponto a Site ou uma conexão de rede virtual a rede.</span><span class="sxs-lookup"><span data-stu-id="24f0c-108">You can add a S2S connection tooa VNet that already has a S2S connection, Point-to-Site connection, or VNet-to-VNet connection.</span></span> <span data-ttu-id="24f0c-109">Existem algumas limitações ao adicionar conexões.</span><span class="sxs-lookup"><span data-stu-id="24f0c-109">There are some limitations when adding connections.</span></span> <span data-ttu-id="24f0c-110">Verificar Olá [antes de começar](#before) seção tooverify este artigo antes de iniciar a configuração.</span><span class="sxs-lookup"><span data-stu-id="24f0c-110">Check hello [Before you begin](#before) section in this article tooverify before you start your configuration.</span></span> 

<span data-ttu-id="24f0c-111">Este artigo se aplica a tooVNets criado usando o modelo de implantação do Gerenciador de recursos de saudação que têm um gateway VPN RouteBased.</span><span class="sxs-lookup"><span data-stu-id="24f0c-111">This article applies tooVNets created using hello Resource Manager deployment model that have a RouteBased VPN gateway.</span></span> <span data-ttu-id="24f0c-112">Essas etapas não se aplicam a configurações de conexão coexistentes tooExpressRoute/Site a Site.</span><span class="sxs-lookup"><span data-stu-id="24f0c-112">These steps do not apply tooExpressRoute/Site-to-Site coexisting connection configurations.</span></span> <span data-ttu-id="24f0c-113">Confira [Conexões coexistentes ExpressRoute/S2S](../expressroute/expressroute-howto-coexist-resource-manager.md) para obter informações sobre conexões coexistentes.</span><span class="sxs-lookup"><span data-stu-id="24f0c-113">See [ExpressRoute/S2S coexisting connections](../expressroute/expressroute-howto-coexist-resource-manager.md) for information about coexisting connections.</span></span>

### <a name="deployment-models-and-methods"></a><span data-ttu-id="24f0c-114">Modelos e métodos de implantação</span><span class="sxs-lookup"><span data-stu-id="24f0c-114">Deployment models and methods</span></span>
[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

<span data-ttu-id="24f0c-115">Atualizamos esta tabela conforme novos artigos e ferramentas adicionais ficam disponíveis para esta configuração.</span><span class="sxs-lookup"><span data-stu-id="24f0c-115">We update this table as new articles and additional tools become available for this configuration.</span></span> <span data-ttu-id="24f0c-116">Quando um artigo está disponível, vinculamos diretamente tooit desta tabela.</span><span class="sxs-lookup"><span data-stu-id="24f0c-116">When an article is available, we link directly tooit from this table.</span></span>

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <span data-ttu-id="24f0c-117"><a name="before"></a>Antes de começar</span><span class="sxs-lookup"><span data-stu-id="24f0c-117"><a name="before"></a>Before you begin</span></span>
<span data-ttu-id="24f0c-118">Verifique se Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="24f0c-118">Verify hello following items:</span></span>

* <span data-ttu-id="24f0c-119">Você não está criando uma conexão ExpressRoute/S2S coexistente.</span><span class="sxs-lookup"><span data-stu-id="24f0c-119">You are not creating an ExpressRoute/S2S coexisting connection.</span></span>
* <span data-ttu-id="24f0c-120">Você tem uma rede virtual que foi criada usando o modelo de implantação do Gerenciador de recursos de saudação com uma conexão existente.</span><span class="sxs-lookup"><span data-stu-id="24f0c-120">You have a virtual network that was created using hello Resource Manager deployment model with an existing connection.</span></span>
* <span data-ttu-id="24f0c-121">Olá o gateway de rede virtual para sua rede virtual é RouteBased.</span><span class="sxs-lookup"><span data-stu-id="24f0c-121">hello virtual network gateway for your VNet is RouteBased.</span></span> <span data-ttu-id="24f0c-122">Se você tiver um gateway PolicyBased VPN, você deve excluir gateway de rede virtual hello e criar um novo gateway VPN como RouteBased.</span><span class="sxs-lookup"><span data-stu-id="24f0c-122">If you have a PolicyBased VPN gateway, you must delete hello virtual network gateway and create a new VPN gateway as RouteBased.</span></span>
* <span data-ttu-id="24f0c-123">Nenhum dos intervalos de endereços de saudação sobrepor para qualquer Olá VNets esta rede está se conectando.</span><span class="sxs-lookup"><span data-stu-id="24f0c-123">None of hello address ranges overlap for any of hello VNets that this VNet is connecting to.</span></span>
* <span data-ttu-id="24f0c-124">Você tem o dispositivo VPN compatível e alguém que é capaz de tooconfigure-lo.</span><span class="sxs-lookup"><span data-stu-id="24f0c-124">You have compatible VPN device and someone who is able tooconfigure it.</span></span> <span data-ttu-id="24f0c-125">Confira [Sobre dispositivos VPN](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="24f0c-125">See [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span> <span data-ttu-id="24f0c-126">Se você não estiver familiarizado com a configuração de seu dispositivo VPN ou não estiver familiarizado com os intervalos de endereços IP de saudação localizados em sua configuração de rede local, será necessário toocoordinate com alguém que possa fornecer os detalhes para você.</span><span class="sxs-lookup"><span data-stu-id="24f0c-126">If you aren't familiar with configuring your VPN device, or are unfamiliar with hello IP address ranges located in your on-premises network configuration, you need toocoordinate with someone who can provide those details for you.</span></span>
* <span data-ttu-id="24f0c-127">Você possui um endereço IP público voltado para o exterior para seu dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="24f0c-127">You have an externally facing public IP address for your VPN device.</span></span> <span data-ttu-id="24f0c-128">Esse endereço IP não pode estar localizado atrás de um NAT.</span><span class="sxs-lookup"><span data-stu-id="24f0c-128">This IP address cannot be located behind a NAT.</span></span>

## <span data-ttu-id="24f0c-129"><a name="part1"></a>Parte 1 - Configurar uma conexão</span><span class="sxs-lookup"><span data-stu-id="24f0c-129"><a name="part1"></a>Part 1 - Configure a connection</span></span>
1. <span data-ttu-id="24f0c-130">Em um navegador, navegue toohello [portal do Azure](http://portal.azure.com) e, se necessário, entre com sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="24f0c-130">From a browser, navigate toohello [Azure portal](http://portal.azure.com) and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="24f0c-131">Clique em **todos os recursos** e localize seu **gateway de rede virtual** da lista de saudação de recursos e clique nele.</span><span class="sxs-lookup"><span data-stu-id="24f0c-131">Click **All resources** and locate your **virtual network gateway** from hello list of resources and click it.</span></span>
3. <span data-ttu-id="24f0c-132">Em Olá **gateway de rede Virtual** folha, clique em **conexões**.</span><span class="sxs-lookup"><span data-stu-id="24f0c-132">On hello **Virtual network gateway** blade, click **Connections**.</span></span>
   
    <span data-ttu-id="24f0c-133">![Folha Conexões](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/connectionsblade.png "Folha Conexões")</span><span class="sxs-lookup"><span data-stu-id="24f0c-133">![Connections blade](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/connectionsblade.png "Connections blade")</span></span><br>
4. <span data-ttu-id="24f0c-134">Em Olá **conexões** folha, clique em **+ adicionar**.</span><span class="sxs-lookup"><span data-stu-id="24f0c-134">On hello **Connections** blade, click **+Add**.</span></span>
   
    <span data-ttu-id="24f0c-135">![Botão de conexão adicionar](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addbutton.png "adicionar botão de conexão")</span><span class="sxs-lookup"><span data-stu-id="24f0c-135">![Add connection button](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addbutton.png "Add connection button")</span></span><br>
5. <span data-ttu-id="24f0c-136">Em Olá **Adicionar conexão** folha, preencha Olá campos a seguir:</span><span class="sxs-lookup"><span data-stu-id="24f0c-136">On hello **Add connection** blade, fill out hello following fields:</span></span>
   
   * <span data-ttu-id="24f0c-137">**Nome:** Olá nome toogive toohello site criar conexão Olá para.</span><span class="sxs-lookup"><span data-stu-id="24f0c-137">**Name:** hello name you want toogive toohello site you are creating hello connection to.</span></span>
   * <span data-ttu-id="24f0c-138">**Tipo de conexão:** selecione **Site a site (IPsec)**.</span><span class="sxs-lookup"><span data-stu-id="24f0c-138">**Connection type:** Select **Site-to-site (IPsec)**.</span></span>
     
     <span data-ttu-id="24f0c-139">![Adicionar folha de conexão](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addconnectionblade.png "Adicionar folha de conexão")</span><span class="sxs-lookup"><span data-stu-id="24f0c-139">![Add connection blade](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addconnectionblade.png "Add connection blade")</span></span><br>

## <span data-ttu-id="24f0c-140"><a name="part2"></a>Parte 2 - Adicionar um gateway de rede local</span><span class="sxs-lookup"><span data-stu-id="24f0c-140"><a name="part2"></a>Part 2 - Add a local network gateway</span></span>
1. <span data-ttu-id="24f0c-141">Clique em **Gateway de rede Local** ***Escolher um gateway de rede local***.</span><span class="sxs-lookup"><span data-stu-id="24f0c-141">Click **Local network gateway** ***Choose a local network gateway***.</span></span> <span data-ttu-id="24f0c-142">Isso abrirá o hello **gateway de rede local Choose** folha.</span><span class="sxs-lookup"><span data-stu-id="24f0c-142">This will open hello **Choose local network gateway** blade.</span></span>
   
    <span data-ttu-id="24f0c-143">![Gateway de rede local Choose](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/chooselng.png "escolher gateway de rede local")</span><span class="sxs-lookup"><span data-stu-id="24f0c-143">![Choose local network gateway](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/chooselng.png "Choose local network gateway")</span></span><br>
2. <span data-ttu-id="24f0c-144">Clique em **criar novo** tooopen Olá **criar gateway de rede local** folha.</span><span class="sxs-lookup"><span data-stu-id="24f0c-144">Click **Create new** tooopen hello **Create local network gateway** blade.</span></span>
   
    <span data-ttu-id="24f0c-145">![Criar folha de gateway de rede local](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/createlngblade.png "criar gateway de rede local")</span><span class="sxs-lookup"><span data-stu-id="24f0c-145">![Create local network gateway blade](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/createlngblade.png "Create local network gateway")</span></span><br>
3. <span data-ttu-id="24f0c-146">Em Olá **criar gateway de rede local** folha, preencha Olá campos a seguir:</span><span class="sxs-lookup"><span data-stu-id="24f0c-146">On hello **Create local network gateway** blade, fill out hello following fields:</span></span>
   
   * <span data-ttu-id="24f0c-147">**Nome:** nome hello você deseja que o recurso de gateway de rede local toogive toohello.</span><span class="sxs-lookup"><span data-stu-id="24f0c-147">**Name:** hello name you want toogive toohello local network gateway resource.</span></span>
   * <span data-ttu-id="24f0c-148">**Endereço IP:** Olá endereço IP público do dispositivo VPN Olá no site de saudação que você deseja tooconnect para.</span><span class="sxs-lookup"><span data-stu-id="24f0c-148">**IP address:** hello public IP address of hello VPN device on hello site that you want tooconnect to.</span></span>
   * <span data-ttu-id="24f0c-149">**Espaço de endereço:** espaço de endereço de saudação que você deseja toobe roteadas toohello novo site de rede local.</span><span class="sxs-lookup"><span data-stu-id="24f0c-149">**Address space:** hello address space that you want toobe routed toohello new local network site.</span></span>
4. <span data-ttu-id="24f0c-150">Clique em **Okey** em Olá **criar gateway de rede local** alterações de saudação toosave folha.</span><span class="sxs-lookup"><span data-stu-id="24f0c-150">Click **OK** on hello **Create local network gateway** blade toosave hello changes.</span></span>

## <span data-ttu-id="24f0c-151"><a name="part3"></a>Parte 3 - Adicionar chave compartilhada hello e criar conexão Olá</span><span class="sxs-lookup"><span data-stu-id="24f0c-151"><a name="part3"></a>Part 3 - Add hello shared key and create hello connection</span></span>
1. <span data-ttu-id="24f0c-152">Em Olá **Adicionar conexão** folha, adicionar Olá chave compartilhada que você deseja toouse toocreate sua conexão.</span><span class="sxs-lookup"><span data-stu-id="24f0c-152">On hello **Add connection** blade, add hello shared key that you want toouse toocreate your connection.</span></span> <span data-ttu-id="24f0c-153">Você pode obter chave compartilhada de saudação do seu dispositivo VPN, ou criar uma aqui e, em seguida, configure a saudação de toouse do dispositivo VPN mesma chave compartilhada.</span><span class="sxs-lookup"><span data-stu-id="24f0c-153">You can either get hello shared key from your VPN device, or make one up here and then configure your VPN device toouse hello same shared key.</span></span> <span data-ttu-id="24f0c-154">Olá importante coisa é que as chaves de saudação são exatamente Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="24f0c-154">hello important thing is that hello keys are exactly hello same.</span></span>
   
    <span data-ttu-id="24f0c-155">![Chave compartilhada](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/sharedkey.png "Chave compartilhada")</span><span class="sxs-lookup"><span data-stu-id="24f0c-155">![Shared key](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/sharedkey.png "Shared key")</span></span><br>
2. <span data-ttu-id="24f0c-156">Na parte inferior de saudação da folha de saudação, clique em **Okey** toocreate conexão de saudação.</span><span class="sxs-lookup"><span data-stu-id="24f0c-156">At hello bottom of hello blade, click **OK** toocreate hello connection.</span></span>

## <span data-ttu-id="24f0c-157"><a name="part4"></a>Parte 4 - Verifique se a conexão de VPN Olá</span><span class="sxs-lookup"><span data-stu-id="24f0c-157"><a name="part4"></a>Part 4 - Verify hello VPN connection</span></span>


[!INCLUDE [vpn-gateway-verify-connection-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="24f0c-158">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="24f0c-158">Next steps</span></span>

<span data-ttu-id="24f0c-159">Quando a conexão for concluída, você pode adicionar máquinas virtuais tooyour as redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="24f0c-159">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="24f0c-160">Consulte as máquinas virtuais de saudação [aprendizado](https://azure.microsoft.com/documentation/learning-paths/virtual-machines) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="24f0c-160">See hello virtual machines [learning path](https://azure.microsoft.com/documentation/learning-paths/virtual-machines) for more information.</span></span>
