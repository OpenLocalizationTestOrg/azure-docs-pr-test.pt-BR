---
title: "Introdução ao próximo salto no Observador de Rede do Azure | Microsoft Docs"
description: "Esta página fornece uma visão geral da capacidade do próximo salto do Observador de Rede"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: febf7bca-e0b7-41d5-838f-a5a40ebc5aac
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 5dd65d2418cae206965a13013dd990b916ad0733
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-next-hop-in-azure-network-watcher"></a><span data-ttu-id="9fd58-103">Introdução ao próximo salto no Observador de Rede do Azure</span><span class="sxs-lookup"><span data-stu-id="9fd58-103">Introduction to next hop in Azure Network Watcher</span></span>

<span data-ttu-id="9fd58-104">O tráfego de uma VM é enviado para um destino com base nas rotas efetivas associadas a uma NIC.</span><span class="sxs-lookup"><span data-stu-id="9fd58-104">Traffic from a VM is sent to a destination based on the effective routes associated with a NIC.</span></span> <span data-ttu-id="9fd58-105">O próximo salto obtém o tipo do próximo salto e o endereço IP de um pacote em uma máquina virtual específica e na NIC.</span><span class="sxs-lookup"><span data-stu-id="9fd58-105">Next hop gets the next hop type and IP address of a packet from a specific virtual machine and NIC.</span></span> <span data-ttu-id="9fd58-106">Isso ajuda a determinar se o pacote está sendo direcionado para o destino ou se o tráfego está tornando-se um buraco negro.</span><span class="sxs-lookup"><span data-stu-id="9fd58-106">This helps to determine if the packet is being directed to the destination or is the traffic being black holed.</span></span> <span data-ttu-id="9fd58-107">Uma configuração incorreta das rotas feita pelo usuário, onde um tráfego é direcionado para um caminho local ou um dispositivo virtual, pode levar a problemas de conectividade.</span><span class="sxs-lookup"><span data-stu-id="9fd58-107">An improper configuration of routes by the user, where a traffic is directed to an on-premises location or a virtual appliance, can lead to connectivity issues.</span></span> <span data-ttu-id="9fd58-108">O próximo salto também retorna a tabela de rotas associada ao próximo salto.</span><span class="sxs-lookup"><span data-stu-id="9fd58-108">Next hop also returns the route table associated with the next hop.</span></span> <span data-ttu-id="9fd58-109">Ao consultar um próximo salto, se a rota for especificada como sendo definida pelo usuário, ela será retornada.</span><span class="sxs-lookup"><span data-stu-id="9fd58-109">When querying a next hop if the route is defined as a user-defined route, that route will be returned.</span></span> <span data-ttu-id="9fd58-110">Caso contrário, o Próximo salto retornará a "Rota do Sistema".</span><span class="sxs-lookup"><span data-stu-id="9fd58-110">Otherwise Next hop returns "System Route".</span></span>

![visão geral do próximo salto][1]

<span data-ttu-id="9fd58-112">A seguir está uma lista dos tipos de próximos salto que podem ser retornados ao consultar o Próximo salto.</span><span class="sxs-lookup"><span data-stu-id="9fd58-112">The following is a list of the next hop types that can be returned when querying Next hop.</span></span>

* <span data-ttu-id="9fd58-113">Internet</span><span class="sxs-lookup"><span data-stu-id="9fd58-113">Internet</span></span>
* <span data-ttu-id="9fd58-114">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="9fd58-114">VirtualAppliance</span></span>
* <span data-ttu-id="9fd58-115">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="9fd58-115">VirtualNetworkGateway</span></span>
* <span data-ttu-id="9fd58-116">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="9fd58-116">VnetLocal</span></span>
* <span data-ttu-id="9fd58-117">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="9fd58-117">HyperNetGateway</span></span>
* <span data-ttu-id="9fd58-118">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="9fd58-118">VnetPeering</span></span>
* <span data-ttu-id="9fd58-119">Nenhum</span><span class="sxs-lookup"><span data-stu-id="9fd58-119">None</span></span>

### <a name="next-steps"></a><span data-ttu-id="9fd58-120">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9fd58-120">Next steps</span></span>

<span data-ttu-id="9fd58-121">Saiba como usar o próximo salto para localizar problemas de conectividade de rede visitando [Verificar o próximo salto em uma VM](network-watcher-check-next-hop-portal.md)</span><span class="sxs-lookup"><span data-stu-id="9fd58-121">Learn how to use next hop to find issues with network connectivity by visiting [Check the next hop on a VM](network-watcher-check-next-hop-portal.md)</span></span>

<!--Image references-->
[1]: ./media/network-watcher-next-hop-overview/figure1.png













