---
title: aaaAzure exemplos do PowerShell | Microsoft Docs
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
ms.openlocfilehash: 130a6e755691b46a9549cad5acaa5bde4fe38e95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-powershell-samples-for-networking"></a><span data-ttu-id="85fdc-103">Exemplos do Azure PowerShell para rede</span><span class="sxs-lookup"><span data-stu-id="85fdc-103">Azure PowerShell Samples for networking</span></span>

<span data-ttu-id="85fdc-104">Olá tabela a seguir inclui links tooscripts criados usando o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="85fdc-104">hello following table includes links tooscripts built using Azure PowerShell.</span></span>

| | |
|-|-|
|<span data-ttu-id="85fdc-105">**Conectividade entre recursos do Azure**</span><span class="sxs-lookup"><span data-stu-id="85fdc-105">**Connectivity between Azure resources**</span></span>||
| [<span data-ttu-id="85fdc-106">Criar uma rede virtual para aplicativos de várias camadas</span><span class="sxs-lookup"><span data-stu-id="85fdc-106">Create a virtual network for multi-tier applications</span></span>](./scripts/virtual-network-powershell-sample-multi-tier-application.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="85fdc-107">Cria uma rede virtual com sub-redes de front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="85fdc-107">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="85fdc-108">Sub-rede front-end do tráfego toohello tooHTTP limitado, ao tráfego toohello sub-rede back-end é tooSQL limitada, a porta 1433.</span><span class="sxs-lookup"><span data-stu-id="85fdc-108">Traffic toohello front-end subnet is limited tooHTTP, while traffic toohello back-end subnet is limited tooSQL, port 1433.</span></span> |
| [<span data-ttu-id="85fdc-109">Emparelhar duas redes virtuais</span><span class="sxs-lookup"><span data-stu-id="85fdc-109">Peer two virtual networks</span></span>](./scripts/virtual-network-powershell-sample-peer-two-virtual-networks.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="85fdc-110">Cria e conecta-se duas redes virtuais no hello mesma região.</span><span class="sxs-lookup"><span data-stu-id="85fdc-110">Creates and connects two virtual networks in hello same region.</span></span> |
| [<span data-ttu-id="85fdc-111">Rotear o tráfego por meio de uma solução de virtualização de rede</span><span class="sxs-lookup"><span data-stu-id="85fdc-111">Route traffic through a network virtual appliance</span></span>](./scripts/virtual-network-powershell-sample-route-traffic-through-nva.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="85fdc-112">Cria uma rede virtual com sub-redes de front-end e back-end e uma VM tooroute capaz de tráfego entre as sub-redes Olá dois.</span><span class="sxs-lookup"><span data-stu-id="85fdc-112">Creates a virtual network with front-end and back-end subnets and a VM that is able tooroute traffic between hello two subnets.</span></span> |
| [<span data-ttu-id="85fdc-113">Filtrar o tráfego de entrada e saída de rede da VM</span><span class="sxs-lookup"><span data-stu-id="85fdc-113">Filter inbound and outbound VM network traffic</span></span>](./scripts/virtual-network-powershell-filter-network-traffic.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="85fdc-114">Cria uma rede virtual com sub-redes de front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="85fdc-114">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="85fdc-115">O tráfego de rede de entrada toohello front-end subrede é limitada tooHTTP e HTTPS.</span><span class="sxs-lookup"><span data-stu-id="85fdc-115">Inbound network traffic toohello front-end subnet is limited tooHTTP and HTTPS..</span></span> <span data-ttu-id="85fdc-116">Toohello da Internet do tráfego de saída da sub-rede de back-end de saudação não é permitido.</span><span class="sxs-lookup"><span data-stu-id="85fdc-116">Outbound traffic toohello Internet from hello back-end subnet is not permitted.</span></span> |
|<span data-ttu-id="85fdc-117">**Direção do tráfego e balanceamento de carga**</span><span class="sxs-lookup"><span data-stu-id="85fdc-117">**Load balancing and traffic direction**</span></span>||
| [<span data-ttu-id="85fdc-118">Carregar tooVMs de tráfego de balanceamento para alta disponibilidade</span><span class="sxs-lookup"><span data-stu-id="85fdc-118">Load balance traffic tooVMs for high availability</span></span>](./scripts/load-balancer-windows-powershell-sample-nlb.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="85fdc-119">Cria várias máquinas virtuais em uma configuração altamente disponíveis e de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="85fdc-119">Creates several virtual machines in a highly available and load balanced configuration.</span></span> |
| [<span data-ttu-id="85fdc-120">Balanceamento de carga de vários sites em VMs</span><span class="sxs-lookup"><span data-stu-id="85fdc-120">Load balance multiple websites on VMs</span></span>](./scripts/load-balancer-windows-powershell-load-balance-multiple-websites-vm.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="85fdc-121">Cria duas VMs com várias configurações de IP, unida tooan Azure conjunto de disponibilidade, acessível por meio de um balanceador de carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="85fdc-121">Creates two VMs with multiple IP configurations, joined tooan Azure Availability Set, accessible through an Azure Load Balancer.</span></span> |
| [<span data-ttu-id="85fdc-122">Direcionar o tráfego através de várias regiões para alta disponibilidade de aplicativos</span><span class="sxs-lookup"><span data-stu-id="85fdc-122">Direct traffic across multiple regions for high application availability</span></span>](./scripts/traffic-manager-powershell-websites-high-availability.md?toc=%2fazure%2fnetworking%2ftoc.json) |  <span data-ttu-id="85fdc-123">Cria dois planos de serviço de aplicativo, dois aplicativos web, um perfil do Gerenciador de tráfego e dois pontos de extremidade de Gerenciador de tráfego.</span><span class="sxs-lookup"><span data-stu-id="85fdc-123">Creates two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> |
| | |
