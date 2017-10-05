---
title: "Localizar próximo salto com o Próximo Salto do Observador de Rede do Azure - Portal do Azure | Microsoft Docs"
description: "Este artigo descreve como você pode encontrar o que é o tipo do próximo salto e o endereço ip com o próximo salto usando o Portal do Azure"
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
ms.openlocfilehash: 5434b7972346821985c459fc4620805adb88676b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="find-out-what-the-next-hop-type-is-using-the-next-hop-capability-in-azure-network-watcher-using-the-portal"></a><span data-ttu-id="dd9e4-103">Descubra qual o tipo do próximo salto é usando o recurso de próximo salto no Observador de Rede do Azure usando o portal</span><span class="sxs-lookup"><span data-stu-id="dd9e4-103">Find out what the next hop type is using the Next Hop capability in Azure Network Watcher using the portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="dd9e4-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="dd9e4-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="dd9e4-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dd9e4-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="dd9e4-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="dd9e4-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="dd9e4-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="dd9e4-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="dd9e4-108">API REST do Azure</span><span class="sxs-lookup"><span data-stu-id="dd9e4-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="dd9e4-109">O Próximo salto é um recurso do Observador de Rede fornece o capacidade de obter o tipo do próximo salto e o endereço IP com base em uma máquina virtual especificada.</span><span class="sxs-lookup"><span data-stu-id="dd9e4-109">Next hop is a feature of Network Watcher that provides the ability get the next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="dd9e4-110">Esse recurso é útil para determinar se o tráfego deixar uma máquina virtual atravessa um gateway, internet ou redes virtuais para chegar ao seu destino.</span><span class="sxs-lookup"><span data-stu-id="dd9e4-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks to get to its destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="dd9e4-111">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="dd9e4-111">Before you begin</span></span>

<span data-ttu-id="dd9e4-112">Este cenário pressupõe que você seguiu as etapas em [Criação de um Observador de Rede](network-watcher-create.md) para criar um Observador de Rede.</span><span class="sxs-lookup"><span data-stu-id="dd9e4-112">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="dd9e4-113">O cenário também pressupõe que exista um grupo de recursos com uma máquina virtual válida a ser usada.</span><span class="sxs-lookup"><span data-stu-id="dd9e4-113">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="dd9e4-114">Cenário</span><span class="sxs-lookup"><span data-stu-id="dd9e4-114">Scenario</span></span>

<span data-ttu-id="dd9e4-115">O cenário abordado neste artigo usa o Próximo salto para localizar o tipo do próximo salto e o endereço IP de um recurso.</span><span class="sxs-lookup"><span data-stu-id="dd9e4-115">The scenario covered in this article uses Next hop to find out the next hop type and IP address for a resource.</span></span> <span data-ttu-id="dd9e4-116">Para saber mais sobre o Próximo Salto, visite [Visão geral do próximo salto](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dd9e4-116">To learn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

<span data-ttu-id="dd9e4-117">Neste cenário, você:</span><span class="sxs-lookup"><span data-stu-id="dd9e4-117">In this scenario, you will:</span></span>

* <span data-ttu-id="dd9e4-118">Recuperará o próximo salto de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="dd9e4-118">Retrieve the next hop from a virtual machine.</span></span>

## <a name="get-next-hop"></a><span data-ttu-id="dd9e4-119">Obter o próximo salto</span><span class="sxs-lookup"><span data-stu-id="dd9e4-119">Get Next Hop</span></span>

### <a name="step-1"></a><span data-ttu-id="dd9e4-120">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="dd9e4-120">Step 1</span></span>

<span data-ttu-id="dd9e4-121">Navegue até seu recurso Observador de Rede no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="dd9e4-121">Navigate to your Network Watcher resource in the Azure portal.</span></span>

### <a name="step-2"></a><span data-ttu-id="dd9e4-122">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="dd9e4-122">Step 2</span></span>

<span data-ttu-id="dd9e4-123">Clique em **Próximo salto** no painel de navegação, selecione a máquina virtual e a interface de rede, preencha o IP de origem e de destino e clique no botão **Próximo salto**.</span><span class="sxs-lookup"><span data-stu-id="dd9e4-123">Click **Next hop** in the navigation pane, select the virtual machine and network interface, fill out the source and destination IP, and click the **Next hop** button.</span></span>

> [!NOTE]
> <span data-ttu-id="dd9e4-124">O próximo salto exige a alocação do recurso de VM para ser executado.</span><span class="sxs-lookup"><span data-stu-id="dd9e4-124">Next hop requires that the VM resource is allocated to run.</span></span>

![visão geral de obtenção do próximo salto][1]

### <a name="step-3"></a><span data-ttu-id="dd9e4-126">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="dd9e4-126">Step 3</span></span>

<span data-ttu-id="dd9e4-127">Após a conclusão da tarefa, os resultados serão fornecidos.</span><span class="sxs-lookup"><span data-stu-id="dd9e4-127">Once the task is complete, the results are provided.</span></span> <span data-ttu-id="dd9e4-128">O endereço IP e o tipo de dispositivo do próximo salto são exibidos.</span><span class="sxs-lookup"><span data-stu-id="dd9e4-128">The IP address and type of device the next hop is, is displayed.</span></span> <span data-ttu-id="dd9e4-129">A tabela a seguir mostra os valores retornados disponíveis no portal.</span><span class="sxs-lookup"><span data-stu-id="dd9e4-129">The following table shows the available returned values in the portal.</span></span>

<span data-ttu-id="dd9e4-130">**Tipo do próximo salto**</span><span class="sxs-lookup"><span data-stu-id="dd9e4-130">**Next Hop Type**</span></span>

* <span data-ttu-id="dd9e4-131">Internet</span><span class="sxs-lookup"><span data-stu-id="dd9e4-131">Internet</span></span>
* <span data-ttu-id="dd9e4-132">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="dd9e4-132">VirtualAppliance</span></span>
* <span data-ttu-id="dd9e4-133">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="dd9e4-133">VirtualNetworkGateway</span></span>
* <span data-ttu-id="dd9e4-134">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="dd9e4-134">VnetLocal</span></span>
* <span data-ttu-id="dd9e4-135">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="dd9e4-135">HyperNetGateway</span></span>
* <span data-ttu-id="dd9e4-136">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="dd9e4-136">VnetPeering</span></span>
* <span data-ttu-id="dd9e4-137">Nenhum</span><span class="sxs-lookup"><span data-stu-id="dd9e4-137">None</span></span>

<span data-ttu-id="dd9e4-138">Se uma rota personalizada tiver sido usada para rotear esse tráfego, a UDR (rota definida pelo usuário) também será exibida com os resultados.</span><span class="sxs-lookup"><span data-stu-id="dd9e4-138">If a custom route was used to route this traffic, the User-defined route (UDR) is shown as well with the results.</span></span>

![resultados da obtenção do próximo salto][2]

## <a name="next-steps"></a><span data-ttu-id="dd9e4-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dd9e4-140">Next steps</span></span>

<span data-ttu-id="dd9e4-141">Aprenda a analisar as configurações de Grupo de Segurança de Rede por meio de programação visitando [NSG auditoria com o Observador de Rede](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="dd9e4-141">Learn how to review your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>

[1]: ./media/network-watcher-check-next-hop-portal/figure1.png
[2]: ./media/network-watcher-check-next-hop-portal/figure2.png














