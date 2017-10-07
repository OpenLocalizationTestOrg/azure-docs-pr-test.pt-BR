---
title: "aaaFind próximo salto com Azure rede Inspetor de próximo salto - 2.0 do CLI do Azure | Microsoft Docs"
description: "Este artigo descreve como descobrir quais saudação do tipo de próximo salto é e usando o endereço ip do próximo salto usando a CLI do Azure."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 0700c274-3e0d-4dca-acfa-3ceac8990613
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 77c2bde51274bd5c64e7a2467f95139af620ca30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-azure-cli-20"></a><span data-ttu-id="74b89-103">Descobrir que tipo de próximo salto hello está usando o recurso de próximo salto Olá na observador de rede do Azure usando o Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="74b89-103">Find out what hello next hop type is using hello Next Hop capability in Azure Network Watcher using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="74b89-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="74b89-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="74b89-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="74b89-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="74b89-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="74b89-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="74b89-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="74b89-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="74b89-108">API REST do Azure</span><span class="sxs-lookup"><span data-stu-id="74b89-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="74b89-109">Próximo salto é um recurso do observador de rede que fornece a capacidade de saudação tipo hello de próximo salto e o endereço IP com base em uma máquina virtual especificada.</span><span class="sxs-lookup"><span data-stu-id="74b89-109">Next hop is a feature of Network Watcher that provides hello ability get hello next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="74b89-110">Esse recurso é útil para determinar se o tráfego que deixa uma máquina virtual atravessa um gateway, internet ou redes virtuais tooget tooits destino.</span><span class="sxs-lookup"><span data-stu-id="74b89-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks tooget tooits destination.</span></span>

<span data-ttu-id="74b89-111">Este artigo usa nossa próxima geração CLI para o modelo de implantação de gerenciamento de recursos do hello, 2.0 do CLI do Azure, que está disponível para Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="74b89-111">This article uses our next generation CLI for hello resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="74b89-112">Olá tooperform as etapas neste artigo, é necessário muito[instalar Olá Interface de linha de comando do Azure para Mac, Linux e Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="74b89-112">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="74b89-113">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="74b89-113">Before you begin</span></span>

<span data-ttu-id="74b89-114">Nesse cenário, você usará hello tipo de próximo salto do CLI do Azure toofind hello e endereço IP.</span><span class="sxs-lookup"><span data-stu-id="74b89-114">In this scenario, you will use hello Azure CLI toofind hello next hop type and IP address.</span></span>

<span data-ttu-id="74b89-115">Este cenário pressupõe que você já seguiu etapas Olá [criar um observador de rede](network-watcher-create.md) toocreate um observador de rede.</span><span class="sxs-lookup"><span data-stu-id="74b89-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="74b89-116">cenário de Olá também pressupõe que um grupo de recursos com uma máquina virtual válida existe toobe usado.</span><span class="sxs-lookup"><span data-stu-id="74b89-116">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="74b89-117">Cenário</span><span class="sxs-lookup"><span data-stu-id="74b89-117">Scenario</span></span>

<span data-ttu-id="74b89-118">cenário de saudação abordado neste artigo usa um recurso do observador de rede que localiza o tipo de próximo salto hello e endereço IP para um recurso de próximo salto.</span><span class="sxs-lookup"><span data-stu-id="74b89-118">hello scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out hello next hop type and IP address for a resource.</span></span> <span data-ttu-id="74b89-119">toolearn mais sobre o próximo nó, visite [visão geral próximo salto](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="74b89-119">toolearn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>


## <a name="get-next-hop"></a><span data-ttu-id="74b89-120">Obter o próximo salto</span><span class="sxs-lookup"><span data-stu-id="74b89-120">Get Next Hop</span></span>

<span data-ttu-id="74b89-121">tooget Olá próximo salto chamamos Olá `az network watcher show-next-hop` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="74b89-121">tooget hello next hop we call hello `az network watcher show-next-hop` cmdlet.</span></span> <span data-ttu-id="74b89-122">Passamos o grupo de recursos do hello cmdlet Olá observador de rede, Olá NetworkWatcher, a máquina virtual Id, endereço IP de origem e endereço IP de destino.</span><span class="sxs-lookup"><span data-stu-id="74b89-122">We pass hello cmdlet hello Network Watcher resource group, hello NetworkWatcher, virtual machine Id, source IP address, and destination IP address.</span></span> <span data-ttu-id="74b89-123">Neste exemplo, o endereço IP de destino Olá é tooa VM em outra rede virtual.</span><span class="sxs-lookup"><span data-stu-id="74b89-123">In this example, hello destination IP address is tooa VM in another virtual network.</span></span> <span data-ttu-id="74b89-124">Há um gateway de rede virtual entre duas redes virtuais de saudação.</span><span class="sxs-lookup"><span data-stu-id="74b89-124">There is a virtual network gateway between hello two virtual networks.</span></span>

<span data-ttu-id="74b89-125">Se você ainda não tiver ainda, instalar e configurar hello mais recente [2.0 do CLI do Azure](/cli/azure/install-az-cli2) e fazer logon na conta do Azure usando o tooan [logon az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="74b89-125">If you haven't yet, install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="74b89-126">Em seguida, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="74b89-126">Then run hello following command:</span></span>

```azurecli
az network watcher show-next-hop --resource-group <resourcegroupName> --vm <vmNameorID> --source-ip <source-ip> --dest-ip <destination-ip>

```

> [!NOTE]
<span data-ttu-id="74b89-127">Se Olá VM tiver várias NICs e encaminhamento de IP está habilitado em qualquer um dos Olá NICs, Olá, em seguida, o parâmetro NIC (-i nic id) deve ser especificado.</span><span class="sxs-lookup"><span data-stu-id="74b89-127">If hello VM has multiple NICs and IP forwarding is enabled on any of hello NICs, then hello NIC parameter (-i nic-id) must be specified.</span></span> <span data-ttu-id="74b89-128">Caso contrário, será opcional.</span><span class="sxs-lookup"><span data-stu-id="74b89-128">Otherwise it is optional.</span></span>

## <a name="review-results"></a><span data-ttu-id="74b89-129">Analisar resultados</span><span class="sxs-lookup"><span data-stu-id="74b89-129">Review results</span></span>

<span data-ttu-id="74b89-130">Ao concluir, resultados de saudação são fornecidos.</span><span class="sxs-lookup"><span data-stu-id="74b89-130">When complete, hello results are provided.</span></span> <span data-ttu-id="74b89-131">Olá próximo endereço IP será retornado, bem como o tipo de saudação do recurso é.</span><span class="sxs-lookup"><span data-stu-id="74b89-131">hello next hop IP address is returned as well as hello type of resource it is.</span></span>

```azurecli
{
    "nextHopIpAddress": null,
    "nextHopType": "Internet",
    "routeTableId": "System Route"
}
```

<span data-ttu-id="74b89-132">Hello lista a seguir mostra valores de NextHopType disponíveis no momento da saudação:</span><span class="sxs-lookup"><span data-stu-id="74b89-132">hello following list shows hello currently available NextHopType values:</span></span>

<span data-ttu-id="74b89-133">**Tipo do próximo salto**</span><span class="sxs-lookup"><span data-stu-id="74b89-133">**Next Hop Type**</span></span>

* <span data-ttu-id="74b89-134">Internet</span><span class="sxs-lookup"><span data-stu-id="74b89-134">Internet</span></span>
* <span data-ttu-id="74b89-135">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="74b89-135">VirtualAppliance</span></span>
* <span data-ttu-id="74b89-136">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="74b89-136">VirtualNetworkGateway</span></span>
* <span data-ttu-id="74b89-137">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="74b89-137">VnetLocal</span></span>
* <span data-ttu-id="74b89-138">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="74b89-138">HyperNetGateway</span></span>
* <span data-ttu-id="74b89-139">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="74b89-139">VnetPeering</span></span>
* <span data-ttu-id="74b89-140">Nenhum</span><span class="sxs-lookup"><span data-stu-id="74b89-140">None</span></span>

## <a name="next-steps"></a><span data-ttu-id="74b89-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="74b89-141">Next steps</span></span>

<span data-ttu-id="74b89-142">Saiba como tooreview as configurações de grupo de segurança de rede por meio de programação visitando [NSG auditoria com o observador de rede](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="74b89-142">Learn how tooreview your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>
