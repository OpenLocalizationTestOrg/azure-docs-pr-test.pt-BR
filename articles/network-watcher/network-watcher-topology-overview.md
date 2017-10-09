---
title: tootopology aaaIntroduction no Inspetor de rede do Azure | Microsoft Docs
description: "Esta página fornece uma visão geral dos recursos de topologia de rede Inspetor Olá"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e753a435-38e0-482b-846b-121cb547555c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 7fa1c5518e4a25a5db999d898a9ee19fd0121db7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tootopology-in-azure-network-watcher"></a><span data-ttu-id="ac30b-103">Introdução tootopology no Inspetor de rede do Azure</span><span class="sxs-lookup"><span data-stu-id="ac30b-103">Introduction tootopology in Azure Network Watcher</span></span>

<span data-ttu-id="ac30b-104">A topologia retorna um gráfico de recursos de rede em uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="ac30b-104">Topology returns a graph of network resources in a virtual network.</span></span> <span data-ttu-id="ac30b-105">gráfico de saudação mostra interconexão de saudação entre Olá recursos toorepresent Olá final tooend a conectividade de rede.</span><span class="sxs-lookup"><span data-stu-id="ac30b-105">hello graph depicts hello interconnection between hello resources toorepresent hello end tooend network connectivity.</span></span>

![visão geral da topologia][1]

<span data-ttu-id="ac30b-107">No portal de saudação topologia retorna objetos de recurso de saudação em um acordo de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="ac30b-107">In hello portal, Topology returns hello resource objects on a per virtual network basis.</span></span> <span data-ttu-id="ac30b-108">relações de saudação estão representadas por linhas entre recursos Olá recursos fora da região do observador de rede hello, mesmo que no recurso Olá o grupo não será exibido.</span><span class="sxs-lookup"><span data-stu-id="ac30b-108">hello relationships are depicted by lines between hello resources Resources outside of hello Network Watcher region, even if in hello resource group will not be displayed.</span></span> <span data-ttu-id="ac30b-109">recursos Olá retornados na exibição de portal Olá são um subconjunto Olá de componentes de rede que são mostrados.</span><span class="sxs-lookup"><span data-stu-id="ac30b-109">hello resources returned in hello portal view are a subset of hello networking components that are graphed.</span></span> <span data-ttu-id="ac30b-110">lista completa de saudação de toosee de recursos de rede que você pode usar [PowerShell](network-watcher-topology-powershell.md) ou [REST](network-watcher-topology-rest.md)</span><span class="sxs-lookup"><span data-stu-id="ac30b-110">toosee hello full list of networking resources you can use [PowerShell](network-watcher-topology-powershell.md) or [REST](network-watcher-topology-rest.md)</span></span>

> [!NOTE]
> <span data-ttu-id="ac30b-111">Uma instância do observador de rede é necessária em cada região que você deseja toorun topologia na.</span><span class="sxs-lookup"><span data-stu-id="ac30b-111">An instance of Network Watcher is required in each region that you want toorun Topology on.</span></span>

<span data-ttu-id="ac30b-112">Como recursos são retornados conexão Olá entre eles são modeladas em duas relações.</span><span class="sxs-lookup"><span data-stu-id="ac30b-112">As resources are returned hello connection between them are modeled under two relationships.</span></span>

- <span data-ttu-id="ac30b-113">**Confinamento** - Exemplo: uma rede virtual contém uma sub-rede que contém uma NIC</span><span class="sxs-lookup"><span data-stu-id="ac30b-113">**Containment** - Example: Virtual Network contains a Subnet which contains a NIC</span></span>
- <span data-ttu-id="ac30b-114">**Associados** - Exemplo: uma NIC está associada a uma VM</span><span class="sxs-lookup"><span data-stu-id="ac30b-114">**Associated** - Example: A NIC is associated with a VM</span></span>

### <a name="next-steps"></a><span data-ttu-id="ac30b-115">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ac30b-115">Next steps</span></span>

<span data-ttu-id="ac30b-116">Saiba como toouse PowerShell tooretrieve Olá topologia exibir visitando [topologia do observador de rede com o PowerShell](network-watcher-topology-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="ac30b-116">Learn how toouse PowerShell tooretrieve hello Topology view by visiting [Network Watcher topology with PowerShell](network-watcher-topology-powershell.md)</span></span>

<!--Image references-->

[1]: ./media/network-watcher-topology-overview/topology.png
