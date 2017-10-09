---
title: aaaIntroduction toonext salto observador de rede do Azure | Microsoft Docs
description: "Esta página fornece uma visão geral Olá observador de rede de recurso do próximo salto"
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
ms.openlocfilehash: 916af736d0d52abadeafed746f0f8a0173b11033
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toonext-hop-in-azure-network-watcher"></a><span data-ttu-id="788e3-103">Salto toonext Introdução observador de rede do Azure</span><span class="sxs-lookup"><span data-stu-id="788e3-103">Introduction toonext hop in Azure Network Watcher</span></span>

<span data-ttu-id="788e3-104">O tráfego de uma VM é enviado tooa destino com base nas rotas efetiva de saudação associadas a uma NIC.</span><span class="sxs-lookup"><span data-stu-id="788e3-104">Traffic from a VM is sent tooa destination based on hello effective routes associated with a NIC.</span></span> <span data-ttu-id="788e3-105">Próximo salto obtém o tipo de próximo salto hello e endereço IP de um pacote de uma máquina virtual específica e a NIC.</span><span class="sxs-lookup"><span data-stu-id="788e3-105">Next hop gets hello next hop type and IP address of a packet from a specific virtual machine and NIC.</span></span> <span data-ttu-id="788e3-106">Isso ajuda a toodetermine se hello pacote está sendo direcionado toohello destino ou é holed de tráfego Olá sendo preto.</span><span class="sxs-lookup"><span data-stu-id="788e3-106">This helps toodetermine if hello packet is being directed toohello destination or is hello traffic being black holed.</span></span> <span data-ttu-id="788e3-107">Uma configuração incorreta de rotas por usuário hello, onde um tráfego é direcionado tooan no local ou um dispositivo virtual, pode levar a problemas de tooconnectivity.</span><span class="sxs-lookup"><span data-stu-id="788e3-107">An improper configuration of routes by hello user, where a traffic is directed tooan on-premises location or a virtual appliance, can lead tooconnectivity issues.</span></span> <span data-ttu-id="788e3-108">Próximo salto também retorna a tabela de rotas Olá associada próximo salto de saudação.</span><span class="sxs-lookup"><span data-stu-id="788e3-108">Next hop also returns hello route table associated with hello next hop.</span></span> <span data-ttu-id="788e3-109">Ao consultar um próximo salto se rota de saudação é definida como uma rota definida pelo usuário, essa rota será retornada.</span><span class="sxs-lookup"><span data-stu-id="788e3-109">When querying a next hop if hello route is defined as a user-defined route, that route will be returned.</span></span> <span data-ttu-id="788e3-110">Caso contrário, o Próximo salto retornará a "Rota do Sistema".</span><span class="sxs-lookup"><span data-stu-id="788e3-110">Otherwise Next hop returns "System Route".</span></span>

![visão geral do próximo salto][1]

<span data-ttu-id="788e3-112">a seguir Olá é uma lista de saudação tipos de próximo salto que podem ser retornados ao consultar o próximo salto.</span><span class="sxs-lookup"><span data-stu-id="788e3-112">hello following is a list of hello next hop types that can be returned when querying Next hop.</span></span>

* <span data-ttu-id="788e3-113">Internet</span><span class="sxs-lookup"><span data-stu-id="788e3-113">Internet</span></span>
* <span data-ttu-id="788e3-114">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="788e3-114">VirtualAppliance</span></span>
* <span data-ttu-id="788e3-115">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="788e3-115">VirtualNetworkGateway</span></span>
* <span data-ttu-id="788e3-116">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="788e3-116">VnetLocal</span></span>
* <span data-ttu-id="788e3-117">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="788e3-117">HyperNetGateway</span></span>
* <span data-ttu-id="788e3-118">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="788e3-118">VnetPeering</span></span>
* <span data-ttu-id="788e3-119">Nenhum</span><span class="sxs-lookup"><span data-stu-id="788e3-119">None</span></span>

### <a name="next-steps"></a><span data-ttu-id="788e3-120">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="788e3-120">Next steps</span></span>

<span data-ttu-id="788e3-121">Saiba como toouse próximo salto toofind problemas de conectividade de rede visitando [seleção Olá próximo salto em uma máquina virtual](network-watcher-check-next-hop-portal.md)</span><span class="sxs-lookup"><span data-stu-id="788e3-121">Learn how toouse next hop toofind issues with network connectivity by visiting [Check hello next hop on a VM](network-watcher-check-next-hop-portal.md)</span></span>

<!--Image references-->
[1]: ./media/network-watcher-next-hop-overview/figure1.png













