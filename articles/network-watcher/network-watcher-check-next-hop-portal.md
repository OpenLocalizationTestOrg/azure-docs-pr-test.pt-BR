---
title: "aaaFind próximo salto com Azure rede Inspetor de próximo salto - portal do Azure | Microsoft Docs"
description: "Este artigo descreve como descobrir quais saudação do tipo de próximo salto é e endereço ip usando próximo salto Olá portal do Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 7b459dcf-4077-424e-a774-f7bfa34c5975
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: b64a2a5275c15aa8bdb10601de4ae1504a9ab551
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-hello-portal"></a><span data-ttu-id="2b396-103">Descobrir que tipo de próximo salto Olá está usando o recurso de próximo salto Olá no Inspetor de rede do Azure usando o portal de saudação</span><span class="sxs-lookup"><span data-stu-id="2b396-103">Find out what hello next hop type is using hello Next Hop capability in Azure Network Watcher using hello portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="2b396-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="2b396-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="2b396-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2b396-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="2b396-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="2b396-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="2b396-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="2b396-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="2b396-108">API REST do Azure</span><span class="sxs-lookup"><span data-stu-id="2b396-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="2b396-109">Próximo salto é um recurso do observador de rede que fornece a capacidade de saudação tipo hello de próximo salto e o endereço IP com base em uma máquina virtual especificada.</span><span class="sxs-lookup"><span data-stu-id="2b396-109">Next hop is a feature of Network Watcher that provides hello ability get hello next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="2b396-110">Esse recurso é útil para determinar se o tráfego que deixa uma máquina virtual atravessa um gateway, internet ou redes virtuais tooget tooits destino.</span><span class="sxs-lookup"><span data-stu-id="2b396-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks tooget tooits destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2b396-111">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="2b396-111">Before you begin</span></span>

<span data-ttu-id="2b396-112">Este cenário pressupõe que você já seguiu etapas Olá [criar um observador de rede](network-watcher-create.md) toocreate um observador de rede.</span><span class="sxs-lookup"><span data-stu-id="2b396-112">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="2b396-113">cenário de Olá também pressupõe que um grupo de recursos com uma máquina virtual válida existe toobe usado.</span><span class="sxs-lookup"><span data-stu-id="2b396-113">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="2b396-114">Cenário</span><span class="sxs-lookup"><span data-stu-id="2b396-114">Scenario</span></span>

<span data-ttu-id="2b396-115">cenário de saudação abordado neste artigo usa toofind de próximo salto tipo hello de próximo salto e o endereço IP de um recurso.</span><span class="sxs-lookup"><span data-stu-id="2b396-115">hello scenario covered in this article uses Next hop toofind out hello next hop type and IP address for a resource.</span></span> <span data-ttu-id="2b396-116">toolearn mais sobre o próximo nó, visite [visão geral próximo salto](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2b396-116">toolearn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

<span data-ttu-id="2b396-117">Neste cenário, você:</span><span class="sxs-lookup"><span data-stu-id="2b396-117">In this scenario, you will:</span></span>

* <span data-ttu-id="2b396-118">Recupere o próximo salto de saudação de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2b396-118">Retrieve hello next hop from a virtual machine.</span></span>

## <a name="get-next-hop"></a><span data-ttu-id="2b396-119">Obter o próximo salto</span><span class="sxs-lookup"><span data-stu-id="2b396-119">Get Next Hop</span></span>

### <a name="step-1"></a><span data-ttu-id="2b396-120">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="2b396-120">Step 1</span></span>

<span data-ttu-id="2b396-121">Navegue tooyour recurso observador de rede Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2b396-121">Navigate tooyour Network Watcher resource in hello Azure portal.</span></span>

### <a name="step-2"></a><span data-ttu-id="2b396-122">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="2b396-122">Step 2</span></span>

<span data-ttu-id="2b396-123">Clique em **do próximo salto** no painel de navegação do hello, Olá selecione máquina de virtual e interface de rede, preencha Olá IP de origem e de destino e, em seguida, clique em Olá **do próximo salto** botão.</span><span class="sxs-lookup"><span data-stu-id="2b396-123">Click **Next hop** in hello navigation pane, select hello virtual machine and network interface, fill out hello source and destination IP, and click hello **Next hop** button.</span></span>

> [!NOTE]
> <span data-ttu-id="2b396-124">Próximo salto requer que o recurso VM hello está alocado toorun.</span><span class="sxs-lookup"><span data-stu-id="2b396-124">Next hop requires that hello VM resource is allocated toorun.</span></span>

![visão geral de obtenção do próximo salto][1]

### <a name="step-3"></a><span data-ttu-id="2b396-126">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="2b396-126">Step 3</span></span>

<span data-ttu-id="2b396-127">Após a conclusão da tarefa hello, resultados de saudação são fornecidos.</span><span class="sxs-lookup"><span data-stu-id="2b396-127">Once hello task is complete, hello results are provided.</span></span> <span data-ttu-id="2b396-128">Olá endereço IP e o tipo de próximo salto saudação do dispositivo é, é exibida.</span><span class="sxs-lookup"><span data-stu-id="2b396-128">hello IP address and type of device hello next hop is, is displayed.</span></span> <span data-ttu-id="2b396-129">Olá tabela a seguir mostra os valores retornados disponíveis Olá no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b396-129">hello following table shows hello available returned values in hello portal.</span></span>

<span data-ttu-id="2b396-130">**Tipo do próximo salto**</span><span class="sxs-lookup"><span data-stu-id="2b396-130">**Next Hop Type**</span></span>

* <span data-ttu-id="2b396-131">Internet</span><span class="sxs-lookup"><span data-stu-id="2b396-131">Internet</span></span>
* <span data-ttu-id="2b396-132">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="2b396-132">VirtualAppliance</span></span>
* <span data-ttu-id="2b396-133">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="2b396-133">VirtualNetworkGateway</span></span>
* <span data-ttu-id="2b396-134">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="2b396-134">VnetLocal</span></span>
* <span data-ttu-id="2b396-135">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="2b396-135">HyperNetGateway</span></span>
* <span data-ttu-id="2b396-136">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="2b396-136">VnetPeering</span></span>
* <span data-ttu-id="2b396-137">Nenhum</span><span class="sxs-lookup"><span data-stu-id="2b396-137">None</span></span>

<span data-ttu-id="2b396-138">Se uma rota personalizada foi usado tooroute esse tráfego de rota definidas pelo usuário da saudação (UDR) também é exibido com resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b396-138">If a custom route was used tooroute this traffic, hello User-defined route (UDR) is shown as well with hello results.</span></span>

![resultados da obtenção do próximo salto][2]

## <a name="next-steps"></a><span data-ttu-id="2b396-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2b396-140">Next steps</span></span>

<span data-ttu-id="2b396-141">Saiba como tooreview as configurações de grupo de segurança de rede por meio de programação visitando [NSG auditoria com o observador de rede](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="2b396-141">Learn how tooreview your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>

[1]: ./media/network-watcher-check-next-hop-portal/figure1.png
[2]: ./media/network-watcher-check-next-hop-portal/figure2.png














