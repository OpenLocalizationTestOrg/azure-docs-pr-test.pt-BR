---
title: Exemplos do Azure PowerShell | Microsoft Docs
description: Exemplos do Azure PowerShell
services: virtual-network
documentationcenter: virtual-network
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/24/2017
ms.author: georgewallace
ms.openlocfilehash: 0bca4fb6874bd265f0ae9faeb4219abeb4ffb6d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-powershell-samples-for-networking"></a><span data-ttu-id="b58e8-103">Exemplos do Azure PowerShell para rede</span><span class="sxs-lookup"><span data-stu-id="b58e8-103">Azure PowerShell Samples for networking</span></span>

<span data-ttu-id="b58e8-104">A tabela a seguir inclui links para scripts compilados usando Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b58e8-104">The following table includes links to scripts built using Azure PowerShell.</span></span>

| | |
|-|-|
|<span data-ttu-id="b58e8-105">**Conectividade entre recursos do Azure**</span><span class="sxs-lookup"><span data-stu-id="b58e8-105">**Connectivity between Azure resources**</span></span>||
| [<span data-ttu-id="b58e8-106">Criar uma rede virtual para aplicativos de várias camadas</span><span class="sxs-lookup"><span data-stu-id="b58e8-106">Create a virtual network for multi-tier applications</span></span>](./scripts/virtual-network-powershell-sample-multi-tier-application.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="b58e8-107">Cria uma rede virtual com sub-redes de front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="b58e8-107">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="b58e8-108">O tráfego para a sub-rede de front-end é limitado a HTTP, enquanto o tráfego para a sub-rede de back-end é limitado a SQL, porta 1433.</span><span class="sxs-lookup"><span data-stu-id="b58e8-108">Traffic to the front-end subnet is limited to HTTP, while traffic to the back-end subnet is limited to SQL, port 1433.</span></span> |
| [<span data-ttu-id="b58e8-109">Emparelhar duas redes virtuais</span><span class="sxs-lookup"><span data-stu-id="b58e8-109">Peer two virtual networks</span></span>](./scripts/virtual-network-powershell-sample-peer-two-virtual-networks.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="b58e8-110">Cria e conecta duas redes virtuais na mesma região.</span><span class="sxs-lookup"><span data-stu-id="b58e8-110">Creates and connects two virtual networks in the same region.</span></span> |
| [<span data-ttu-id="b58e8-111">Rotear o tráfego por meio de uma solução de virtualização de rede</span><span class="sxs-lookup"><span data-stu-id="b58e8-111">Route traffic through a network virtual appliance</span></span>](./scripts/virtual-network-powershell-sample-route-traffic-through-nva.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="b58e8-112">Cria uma rede virtual com sub-redes de front-end e back-end e uma VM capaz de rotear o tráfego entre as duas sub-redes.</span><span class="sxs-lookup"><span data-stu-id="b58e8-112">Creates a virtual network with front-end and back-end subnets and a VM that is able to route traffic between the two subnets.</span></span> |
| [<span data-ttu-id="b58e8-113">Filtrar o tráfego de entrada e saída de rede da VM</span><span class="sxs-lookup"><span data-stu-id="b58e8-113">Filter inbound and outbound VM network traffic</span></span>](./scripts/virtual-network-powershell-filter-network-traffic.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="b58e8-114">Cria uma rede virtual com sub-redes de front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="b58e8-114">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="b58e8-115">O tráfego de rede de entrada para a sub-rede de front-end é limitado a HTTP e HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b58e8-115">Inbound network traffic to the front-end subnet is limited to HTTP and HTTPS..</span></span> <span data-ttu-id="b58e8-116">O tráfego de saída para a Internet da sub-rede de back-end não é permitido.</span><span class="sxs-lookup"><span data-stu-id="b58e8-116">Outbound traffic to the Internet from the back-end subnet is not permitted.</span></span> |
|<span data-ttu-id="b58e8-117">**Direção do tráfego e balanceamento de carga**</span><span class="sxs-lookup"><span data-stu-id="b58e8-117">**Load balancing and traffic direction**</span></span>||
| [<span data-ttu-id="b58e8-118">Balancear o tráfego de VMs para alta disponibilidade</span><span class="sxs-lookup"><span data-stu-id="b58e8-118">Load balance traffic to VMs for high availability</span></span>](./scripts/load-balancer-windows-powershell-sample-nlb.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="b58e8-119">Cria várias máquinas virtuais em uma configuração altamente disponíveis e de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="b58e8-119">Creates several virtual machines in a highly available and load balanced configuration.</span></span> |
| [<span data-ttu-id="b58e8-120">Balanceamento de carga de vários sites em VMs</span><span class="sxs-lookup"><span data-stu-id="b58e8-120">Load balance multiple websites on VMs</span></span>](./scripts/load-balancer-windows-powershell-load-balance-multiple-websites-vm.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="b58e8-121">Cria duas VMs com várias configurações de IP, associadas a um conjunto de disponibilidade do Azure, acessível por meio de um Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="b58e8-121">Creates two VMs with multiple IP configurations, joined to an Azure Availability Set, accessible through an Azure Load Balancer.</span></span> |
| [<span data-ttu-id="b58e8-122">Direcionar o tráfego através de várias regiões para alta disponibilidade de aplicativos</span><span class="sxs-lookup"><span data-stu-id="b58e8-122">Direct traffic across multiple regions for high application availability</span></span>](./scripts/traffic-manager-powershell-websites-high-availability.md?toc=%2fazure%2fnetworking%2ftoc.json) |  <span data-ttu-id="b58e8-123">Cria dois planos de serviço de aplicativo, dois aplicativos web, um perfil do Gerenciador de tráfego e dois pontos de extremidade de Gerenciador de tráfego.</span><span class="sxs-lookup"><span data-stu-id="b58e8-123">Creates two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> |
| | |
