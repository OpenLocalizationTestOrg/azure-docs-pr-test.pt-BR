---
title: aaaAzure CLI exemplos | Microsoft Docs
description: Exemplos de CLI do Azure
services: virtual-network
documentationcenter: virtual-network
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 04/25/2017
ms.author: kumud
ms.openlocfilehash: 8001b7e72480cfd0122325f7fb81c32aaad072d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples-for-networking"></a><span data-ttu-id="38741-103">Exemplos de CLI do Azure para rede</span><span class="sxs-lookup"><span data-stu-id="38741-103">Azure CLI Samples for networking</span></span>

<span data-ttu-id="38741-104">Olá, tabela a seguir inclui scripts de toobash links criados usando Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="38741-104">hello following table includes links toobash scripts built using hello Azure CLI.</span></span>

| | |
|-|-|
|<span data-ttu-id="38741-105">**Conectividade entre recursos do Azure**</span><span class="sxs-lookup"><span data-stu-id="38741-105">**Connectivity between Azure resources**</span></span>||
| [<span data-ttu-id="38741-106">Criar uma rede virtual para aplicativos de várias camadas</span><span class="sxs-lookup"><span data-stu-id="38741-106">Create a virtual network for multi-tier applications</span></span>](./scripts/virtual-network-cli-sample-multi-tier-application.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="38741-107">Cria uma rede virtual com sub-redes de front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="38741-107">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="38741-108">Sub-rede front-end do tráfego toohello é tooHTTP limitada e SSH, enquanto o tráfego toohello sub-rede back-end é tooMySQL limitado, porta 3306.</span><span class="sxs-lookup"><span data-stu-id="38741-108">Traffic toohello front-end subnet is limited tooHTTP and SSH, while traffic toohello back-end subnet is limited tooMySQL, port 3306.</span></span> |
| [<span data-ttu-id="38741-109">Emparelhar duas redes virtuais</span><span class="sxs-lookup"><span data-stu-id="38741-109">Peer two virtual networks</span></span>](./scripts/virtual-network-cli-sample-peer-two-virtual-networks.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="38741-110">Cria e conecta-se duas redes virtuais no hello mesma região.</span><span class="sxs-lookup"><span data-stu-id="38741-110">Creates and connects two virtual networks in hello same region.</span></span> |
| [<span data-ttu-id="38741-111">Rotear o tráfego por meio de uma solução de virtualização de rede</span><span class="sxs-lookup"><span data-stu-id="38741-111">Route traffic through a network virtual appliance</span></span>](./scripts/virtual-network-cli-sample-route-traffic-through-nva.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="38741-112">Cria uma rede virtual com sub-redes de front-end e back-end e uma VM tooroute capaz de tráfego entre as sub-redes Olá dois.</span><span class="sxs-lookup"><span data-stu-id="38741-112">Creates a virtual network with front-end and back-end subnets and a VM that is able tooroute traffic between hello two subnets.</span></span> |
| [<span data-ttu-id="38741-113">Filtrar o tráfego de entrada e saída de rede da VM</span><span class="sxs-lookup"><span data-stu-id="38741-113">Filter inbound and outbound VM network traffic</span></span>](./scripts/virtual-network-filter-network-traffic.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="38741-114">Cria uma rede virtual com sub-redes de front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="38741-114">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="38741-115">O tráfego de rede de entrada toohello front-end subrede é limitada tooHTTP, HTTPS e SSH.</span><span class="sxs-lookup"><span data-stu-id="38741-115">Inbound network traffic toohello front-end subnet is limited tooHTTP, HTTPS and SSH.</span></span> <span data-ttu-id="38741-116">Toohello da Internet do tráfego de saída da sub-rede de back-end de saudação não é permitido.</span><span class="sxs-lookup"><span data-stu-id="38741-116">Outbound traffic toohello Internet from hello back-end subnet is not permitted.</span></span> |
|<span data-ttu-id="38741-117">**Direção do tráfego e balanceamento de carga**</span><span class="sxs-lookup"><span data-stu-id="38741-117">**Load balancing and traffic direction**</span></span>||
| [<span data-ttu-id="38741-118">Carregar tooVMs de tráfego de balanceamento para alta disponibilidade</span><span class="sxs-lookup"><span data-stu-id="38741-118">Load balance traffic tooVMs for high availability</span></span>](./scripts/load-balancer-linux-cli-sample-nlb.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="38741-119">Cria várias máquinas virtuais em uma configuração altamente disponíveis e de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="38741-119">Creates several virtual machines in a highly available and load balanced configuration.</span></span> |
| [<span data-ttu-id="38741-120">Balanceamento de carga de vários sites em VMs</span><span class="sxs-lookup"><span data-stu-id="38741-120">Load balance multiple websites on VMs</span></span>](./scripts/load-balancer-linux-cli-load-balance-multiple-websites-vm.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="38741-121">Cria duas VMs com várias configurações de IP, unida tooan Azure conjunto de disponibilidade, acessível por meio de um balanceador de carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="38741-121">Creates two VMs with multiple IP configurations, joined tooan Azure Availability Set, accessible through an Azure Load Balancer.</span></span> |
| [<span data-ttu-id="38741-122">Direcionar o tráfego através de várias regiões para alta disponibilidade de aplicativos</span><span class="sxs-lookup"><span data-stu-id="38741-122">Direct traffic across multiple regions for high application availability</span></span>](./scripts/traffic-manager-cli-websites-high-availability.md?toc=%2fazure%2fnetworking%2ftoc.json) |  <span data-ttu-id="38741-123">Cria dois planos de serviço de aplicativo, dois aplicativos web, um perfil do Gerenciador de tráfego e dois pontos de extremidade de Gerenciador de tráfego.</span><span class="sxs-lookup"><span data-stu-id="38741-123">Creates two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> |
| | |
