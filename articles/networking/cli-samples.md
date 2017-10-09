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
# <a name="azure-cli-samples-for-networking"></a>Exemplos de CLI do Azure para rede

Olá, tabela a seguir inclui scripts de toobash links criados usando Olá CLI do Azure.

| | |
|-|-|
|**Conectividade entre recursos do Azure**||
| [Criar uma rede virtual para aplicativos de várias camadas](./scripts/virtual-network-cli-sample-multi-tier-application.md?toc=%2fazure%2fnetworking%2ftoc.json) | Cria uma rede virtual com sub-redes de front-end e back-end. Sub-rede front-end do tráfego toohello é tooHTTP limitada e SSH, enquanto o tráfego toohello sub-rede back-end é tooMySQL limitado, porta 3306. |
| [Emparelhar duas redes virtuais](./scripts/virtual-network-cli-sample-peer-two-virtual-networks.md?toc=%2fazure%2fnetworking%2ftoc.json) | Cria e conecta-se duas redes virtuais no hello mesma região. |
| [Rotear o tráfego por meio de uma solução de virtualização de rede](./scripts/virtual-network-cli-sample-route-traffic-through-nva.md?toc=%2fazure%2fnetworking%2ftoc.json) | Cria uma rede virtual com sub-redes de front-end e back-end e uma VM tooroute capaz de tráfego entre as sub-redes Olá dois. |
| [Filtrar o tráfego de entrada e saída de rede da VM](./scripts/virtual-network-filter-network-traffic.md?toc=%2fazure%2fnetworking%2ftoc.json) | Cria uma rede virtual com sub-redes de front-end e back-end. O tráfego de rede de entrada toohello front-end subrede é limitada tooHTTP, HTTPS e SSH. Toohello da Internet do tráfego de saída da sub-rede de back-end de saudação não é permitido. |
|**Direção do tráfego e balanceamento de carga**||
| [Carregar tooVMs de tráfego de balanceamento para alta disponibilidade](./scripts/load-balancer-linux-cli-sample-nlb.md?toc=%2fazure%2fnetworking%2ftoc.json) | Cria várias máquinas virtuais em uma configuração altamente disponíveis e de balanceamento de carga. |
| [Balanceamento de carga de vários sites em VMs](./scripts/load-balancer-linux-cli-load-balance-multiple-websites-vm.md?toc=%2fazure%2fnetworking%2ftoc.json) | Cria duas VMs com várias configurações de IP, unida tooan Azure conjunto de disponibilidade, acessível por meio de um balanceador de carga do Azure. |
| [Direcionar o tráfego através de várias regiões para alta disponibilidade de aplicativos](./scripts/traffic-manager-cli-websites-high-availability.md?toc=%2fazure%2fnetworking%2ftoc.json) |  Cria dois planos de serviço de aplicativo, dois aplicativos web, um perfil do Gerenciador de tráfego e dois pontos de extremidade de Gerenciador de tráfego. |
| | |
