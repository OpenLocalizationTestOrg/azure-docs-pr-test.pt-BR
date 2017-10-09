---
title: Verifique se aaaIntroduction tooIP fluxo no Inspetor de rede do Azure | Microsoft Docs
description: "Esta página fornece uma visão geral de rede IP de Inspetor de hello fluxo Verifique a capacidade"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: d352fb2d-4b4f-4ac4-9c2e-1cfccf0e7e03
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: b648a4816a7ffdc6ca54462944b574e2395e8298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooip-flow-verify-in-azure-network-watcher"></a><span data-ttu-id="86e84-103">Fluxo de tooIP Introdução verificar em observador de rede do Azure</span><span class="sxs-lookup"><span data-stu-id="86e84-103">Introduction tooIP flow verify in Azure Network Watcher</span></span>

<span data-ttu-id="86e84-104">Fluxo IP verificar verifica se um pacote é permitido ou negado tooor de uma máquina virtual com base nas informações de 5 tuplas.</span><span class="sxs-lookup"><span data-stu-id="86e84-104">IP flow verify checks if a packet is allowed or denied tooor from a virtual machine based on 5-tuple information.</span></span> <span data-ttu-id="86e84-105">Essas informações consistem em direção, protocolo, IP local, IP remoto, porta local e porta remota.</span><span class="sxs-lookup"><span data-stu-id="86e84-105">This information consists of direction, protocol, local IP, remote IP, local port, and remote port.</span></span> <span data-ttu-id="86e84-106">Se o pacote de saudação é negado por um grupo de segurança, nome de saudação de regra Olá negado pacote de saudação é retornado.</span><span class="sxs-lookup"><span data-stu-id="86e84-106">If hello packet is denied by a security group, hello name of hello rule that denied hello packet is returned.</span></span> <span data-ttu-id="86e84-107">Enquanto qualquer IP de origem ou de destino pode ser escolhido, esse recurso ajuda os administradores a diagnosticar rapidamente toohello ou problemas de conectividade de internet e de ou toohello ambiente de local.</span><span class="sxs-lookup"><span data-stu-id="86e84-107">While any source or destination IP can be chosen, this feature helps administrators quickly diagnose connectivity issues from or toohello internet and from or toohello on-premises environment.</span></span>

<span data-ttu-id="86e84-108">A verificação de fluxo de IP tem como alvo uma interface de rede de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="86e84-108">IP flow verify targets a network interface of a virtual machine.</span></span> <span data-ttu-id="86e84-109">Fluxo de tráfego é verificado com base em tooor de configurações de saudação configurada desta interface de rede.</span><span class="sxs-lookup"><span data-stu-id="86e84-109">Traffic flow is then verified based on hello configured settings tooor from that network interface.</span></span> <span data-ttu-id="86e84-110">Esse recurso é útil para confirmar se uma regra em um grupo de segurança de rede está bloqueando tooor de tráfego de entrada ou de saída de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="86e84-110">This capability is useful in confirming if a rule in a Network Security Group is blocking ingress or egress traffic tooor from a virtual machine.</span></span>

<span data-ttu-id="86e84-111">Verifique se uma instância do observador de rede necessidades toobe criado em todas as regiões que você planeje toorun fluxo IP.</span><span class="sxs-lookup"><span data-stu-id="86e84-111">An instance of Network Watcher needs toobe created in all regions that you plan toorun IP flow verify.</span></span> <span data-ttu-id="86e84-112">Observador de rede é um serviço regional e só pode ser executado com base nos recursos em Olá mesma região.</span><span class="sxs-lookup"><span data-stu-id="86e84-112">Network Watcher is a regional service and can only be ran against resources in hello same region.</span></span> <span data-ttu-id="86e84-113">Isso não afeta a saudação resultados do fluxo IP de verificar como rota Olá associada Olá que NIC ainda será retornada.</span><span class="sxs-lookup"><span data-stu-id="86e84-113">This does not affect hello results of IP flow verify as hello route associated with hello NIC will still be returned.</span></span>

![1][1]

## <a name="next-steps"></a><span data-ttu-id="86e84-115">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="86e84-115">Next steps</span></span>

<span data-ttu-id="86e84-116">Visite Olá toolearn do artigo a seguir se um pacote é permitido ou negado para uma máquina virtual por meio do portal hello.</span><span class="sxs-lookup"><span data-stu-id="86e84-116">Visit hello following article toolearn if a packet is allowed or denied for a specific virtual machine through hello portal.</span></span> [<span data-ttu-id="86e84-117">Verifique se o tráfego é permitido em uma VM com IP fluxo verificar usando o portal de saudação</span><span class="sxs-lookup"><span data-stu-id="86e84-117">Check if traffic is allowed on a VM with IP Flow Verify using hello portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)

[1]: ./media/network-watcher-ip-flow-verify-overview/figure1.png












