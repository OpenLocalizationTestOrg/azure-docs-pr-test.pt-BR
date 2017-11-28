---
title: 'Excluir um gateway de rede virtual: Portal do Azure: Resource Manager | Microsoft Docs'
description: "Exclua um gateway de rede virtual usando o portal do Azure no modelo de implantação do Resource Manager."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: 
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: cherylmc
ms.openlocfilehash: 1d289c09465cb8d5e4bfa569441dffcbf562b3bf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="delete-a-virtual-network-gateway-using-the-portal"></a><span data-ttu-id="f4bd9-103">Exclua um gateway de rede virtual usando o portal</span><span class="sxs-lookup"><span data-stu-id="f4bd9-103">Delete a virtual network gateway using the portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f4bd9-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f4bd9-104">Azure portal</span></span>](vpn-gateway-delete-vnet-gateway-portal.md)
> * [<span data-ttu-id="f4bd9-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f4bd9-105">PowerShell</span></span>](vpn-gateway-delete-vnet-gateway-powershell.md)
> * [<span data-ttu-id="f4bd9-106">PowerShell (clássico)</span><span class="sxs-lookup"><span data-stu-id="f4bd9-106">PowerShell (classic)</span></span>](vpn-gateway-delete-vnet-gateway-classic-powershell.md)

<span data-ttu-id="f4bd9-107">Há duas abordagens diferentes que podem ser executadas quando você deseja excluir um gateway de rede virtual de uma configuração de Gateway de VPN.</span><span class="sxs-lookup"><span data-stu-id="f4bd9-107">There are a couple of different approaches you can take when you want to delete a virtual network gateway for a VPN gateway configuration.</span></span>

- <span data-ttu-id="f4bd9-108">Se você desejar excluir tudo e recomeçar, por exemplo, no caso de um ambiente de teste, poderá excluir o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f4bd9-108">If you want to delete everything and start over, as in the case of a test environment, you can delete the resource group.</span></span> <span data-ttu-id="f4bd9-109">Quando você exclui um grupo de recursos, isso exclui todos os recursos dentro do grupo.</span><span class="sxs-lookup"><span data-stu-id="f4bd9-109">When you delete a resource group, it deletes all the resources within the group.</span></span> <span data-ttu-id="f4bd9-110">Esse método é recomendado somente se você não deseja manter os recursos no grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f4bd9-110">This is method is only recommended if you don't want to keep any of the resources in the resource group.</span></span> <span data-ttu-id="f4bd9-111">Você não pode excluir seletivamente apenas alguns recursos usando essa abordagem.</span><span class="sxs-lookup"><span data-stu-id="f4bd9-111">You can't selectively delete only a few resources using this approach.</span></span>

- <span data-ttu-id="f4bd9-112">Se você quiser manter alguns dos recursos no seu grupo de recursos, a exclusão de um gateway de rede virtual se tornará um pouco mais complicada.</span><span class="sxs-lookup"><span data-stu-id="f4bd9-112">If you want to keep some of the resources in your resource group, deleting a virtual network gateway becomes slightly more complicated.</span></span> <span data-ttu-id="f4bd9-113">Antes de poder excluir o gateway de rede virtual, primeiro você deve excluir todos os recursos que são dependentes do gateway.</span><span class="sxs-lookup"><span data-stu-id="f4bd9-113">Before you can delete the virtual network gateway, you must first delete any resources that are dependent on the gateway.</span></span> <span data-ttu-id="f4bd9-114">As etapas a que seguir dependem do tipo de conexões que você criou e os recursos dependentes de cada conexão.</span><span class="sxs-lookup"><span data-stu-id="f4bd9-114">The steps you follow depend on the type of connections that you created and the dependent resources for each connection.</span></span>

## <a name="delete-a-vpn-gateway"></a><span data-ttu-id="f4bd9-115">Excluir um gateway de VPN</span><span class="sxs-lookup"><span data-stu-id="f4bd9-115">Delete a VPN gateway</span></span>

<span data-ttu-id="f4bd9-116">Para excluir um gateway de rede virtual, exclua cada recurso pertencente ao gateway de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="f4bd9-116">To delete a virtual network gateway, you must first delete each resource that pertains to the virtual network gateway.</span></span> <span data-ttu-id="f4bd9-117">Os recursos devem ser excluídos em uma determinada ordem devido a dependências.</span><span class="sxs-lookup"><span data-stu-id="f4bd9-117">Resources must be deleted in a certain order due to dependencies.</span></span>

[!INCLUDE [delete gateway](../../includes/vpn-gateway-delete-vnet-gateway-portal-include.md)]

<span data-ttu-id="f4bd9-118">Nesse momento, o gateway de rede virtual é excluído.</span><span class="sxs-lookup"><span data-stu-id="f4bd9-118">At this point, the virtual network gateway is deleted.</span></span> <span data-ttu-id="f4bd9-119">As próximas etapas ajudam a excluir quaisquer recursos que não são mais utilizados.</span><span class="sxs-lookup"><span data-stu-id="f4bd9-119">The next steps help you delete any resources that are no longer being used.</span></span>

### <a name="to-delete-the-local-network-gateway"></a><span data-ttu-id="f4bd9-120">Para excluir o gateway de rede local</span><span class="sxs-lookup"><span data-stu-id="f4bd9-120">To delete the local network gateway</span></span>

1. <span data-ttu-id="f4bd9-121">Em **Todos os recursos**, localize os gateways de rede locais que estavam associados a cada conexão.</span><span class="sxs-lookup"><span data-stu-id="f4bd9-121">In **All resources**, locate the local network gateways that were associated with each connection.</span></span>
2. <span data-ttu-id="f4bd9-122">Na folha **Visão geral** do gateway de rede local, clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="f4bd9-122">On the **Overview** blade for the local network gateway, click **Delete**.</span></span>

### <a name="to-delete-the-public-ip-address-resource-for-the-gateway"></a><span data-ttu-id="f4bd9-123">Para excluir o recurso de endereço IP público para o gateway</span><span class="sxs-lookup"><span data-stu-id="f4bd9-123">To delete the Public IP address resource for the gateway</span></span>

1. <span data-ttu-id="f4bd9-124">Em **Todos os recursos**, localize o recurso de endereço IP público que estava associado ao gateway.</span><span class="sxs-lookup"><span data-stu-id="f4bd9-124">In **All resources**, locate the Public IP address resource that was associated to the gateway.</span></span> <span data-ttu-id="f4bd9-125">Se o gateway de rede virtual estava ativo-ativo, você verá dois endereços IP públicos.</span><span class="sxs-lookup"><span data-stu-id="f4bd9-125">If the virtual network gateway was active-active, you will see two Public IP addresses.</span></span> 
2. <span data-ttu-id="f4bd9-126">Na página **Visão geral** para o endereço IP público, clique em **Excluir** e, em seguida, em **Sim** para confirmar.</span><span class="sxs-lookup"><span data-stu-id="f4bd9-126">On the **Overview** page for the Public IP address, click **Delete**, then **Yes** to confirm.</span></span>

### <a name="to-delete-the-gateway-subnet"></a><span data-ttu-id="f4bd9-127">Para excluir a sub-rede de gateway</span><span class="sxs-lookup"><span data-stu-id="f4bd9-127">To delete the gateway subnet</span></span>

1. <span data-ttu-id="f4bd9-128">Em **Todos os recursos**, localize a rede virtual.</span><span class="sxs-lookup"><span data-stu-id="f4bd9-128">In **All resources**, locate the virtual network.</span></span> 
2. <span data-ttu-id="f4bd9-129">Na folha **Sub-redes**, clique em **GatewaySubnet** e, em seguida, clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="f4bd9-129">On the **Subnets** blade, click the **GatewaySubnet**, then click **Delete**.</span></span> 
3. <span data-ttu-id="f4bd9-130">Clique em **Sim** para confirmar que deseja excluir a sub-rede do gateway.</span><span class="sxs-lookup"><span data-stu-id="f4bd9-130">Click **Yes** to confirm that you want to delete the gateway subnet.</span></span>

## <span data-ttu-id="f4bd9-131"><a name="deleterg"></a>Excluir um Gateway de VPN por meio da exclusão do grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="f4bd9-131"><a name="deleterg"></a>Delete a VPN gateway by deleting the resource group</span></span>

<span data-ttu-id="f4bd9-132">Se você não estiver preocupado em manter nenhum de seus recursos no grupo de recursos e apenas desejar recomeçar, poderá excluir um grupo de recursos inteiro.</span><span class="sxs-lookup"><span data-stu-id="f4bd9-132">If you are not concerned about keeping any of your resources in the resource group and you just want to start over, you can delete an entire resource group.</span></span> <span data-ttu-id="f4bd9-133">Essa é uma maneira rápida de remover tudo.</span><span class="sxs-lookup"><span data-stu-id="f4bd9-133">This is a quick way to remove everything.</span></span> <span data-ttu-id="f4bd9-134">As próximas etapas se aplicam somente ao modelo de implantação do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f4bd9-134">The following steps apply only to the Resource Manager deployment model.</span></span>

1. <span data-ttu-id="f4bd9-135">Em **Todos os recursos**, localize o grupo de recursos e clique para abrir a folha.</span><span class="sxs-lookup"><span data-stu-id="f4bd9-135">In **All resources**, locate the resource group and click to open the blade.</span></span>
2. <span data-ttu-id="f4bd9-136">Clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="f4bd9-136">Click **Delete**.</span></span> <span data-ttu-id="f4bd9-137">Na folha Excluir, exiba os recursos afetados.</span><span class="sxs-lookup"><span data-stu-id="f4bd9-137">On the Delete blade, view the affected resources.</span></span> <span data-ttu-id="f4bd9-138">Certifique-se de que deseja excluir todos esses recursos.</span><span class="sxs-lookup"><span data-stu-id="f4bd9-138">Make sure that you want to delete all of these resources.</span></span> <span data-ttu-id="f4bd9-139">Se não, use as etapas em [Excluir um Gateway de VPN](#deletegw) na parte superior deste artigo.</span><span class="sxs-lookup"><span data-stu-id="f4bd9-139">If not, use the steps in [Delete a VPN gateway](#deletegw) at the top of this article.</span></span>
3. <span data-ttu-id="f4bd9-140">Para continuar, digite o nome do grupo de recursos que você deseja excluir e, em seguida, clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="f4bd9-140">To proceed, type the name of the resource group that you want to delete, then click **Delete**.</span></span>