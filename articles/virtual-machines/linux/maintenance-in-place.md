---
title: "aaaVM preservação de manutenção para VMs do Windows no Azure | Microsoft Docs"
description: "Migração de VMs no local para atualizações para preservar a memória."
services: virtual-machines-windows
documentationcenter: 
author: 
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: 
ms.openlocfilehash: 544a2dcca52bb3ac51d341bceaf4ba3e7c71fd82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="vm-preserving-maintenance-in-place-vm-migration"></a><span data-ttu-id="6f30f-103">Manutenção para preservar VMs (migração de VMs no local)</span><span class="sxs-lookup"><span data-stu-id="6f30f-103">VM preserving maintenance (In-place VM migration)</span></span>

<span data-ttu-id="6f30f-104">Embora maioria Olá das atualizações não tenham toohosted nenhum impacto VMs, há casos em que atualizações toocomponents ou serviços resultam em interferência mínima toorunning VMs (sem a reinicialização completa da máquina virtual de saudação).</span><span class="sxs-lookup"><span data-stu-id="6f30f-104">While hello majority of updates have no impact toohosted VMs, there are cases where updates toocomponents or services result in minimal interference toorunning VMs (without a full reboot of hello virtual machine).</span></span>

<span data-ttu-id="6f30f-105">Essas atualizações são realizadas com tecnologia que permite a migração dinâmica, também nomeada de "atualização que preservam a memória".</span><span class="sxs-lookup"><span data-stu-id="6f30f-105">These updates are accomplished with technology that enables in-place live migration, also called "memory-preserving update".</span></span> <span data-ttu-id="6f30f-106">Ao atualizar host Olá, máquina virtual de saudação é colocada em um estado "pausado", preservando memória RAM, Olá enquanto hello (por exemplo, o sistema operacional subjacente) do ambiente de hospedagem aplica patches e atualizações necessárias hello.</span><span class="sxs-lookup"><span data-stu-id="6f30f-106">When updating hello host, hello virtual machine is placed into a “paused” state, preserving hello memory in RAM, while hello hosting environment (e.g. the underlying operating system) applies hello necessary updates and patches.</span></span>
<span data-ttu-id="6f30f-107">máquina virtual de saudação é retomada dentro de 30 segundos de em pausa.</span><span class="sxs-lookup"><span data-stu-id="6f30f-107">hello virtual machine is then resumed within 30 seconds of being paused.</span></span>
<span data-ttu-id="6f30f-108">Depois de retomar, Olá relógio da máquina virtual de saudação é sincronizado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="6f30f-108">After resuming, hello clock of hello virtual machine is automatically synchronized.</span></span>

<span data-ttu-id="6f30f-109">Nem todas as atualizações podem ser implantadas por meio desse mecanismo, mas determinado período pequena pausa, implantar as atualizações na forma consideravelmente reduz máquinas de toovirtual de impacto.</span><span class="sxs-lookup"><span data-stu-id="6f30f-109">Not all updates can be deployed by using this mechanism, but given the short pause period, deploying updates in this way greatly reduces impact toovirtual machines.</span></span>

<span data-ttu-id="6f30f-110">Atualizações de múltiplas instâncias (VMs em um conjunto de disponibilidade) são aplicadas em um domínio de atualização por vez.</span><span class="sxs-lookup"><span data-stu-id="6f30f-110">Multi-instance updates (VMs in an availability set) are applied one update domain at a time.</span></span>

<span data-ttu-id="6f30f-111">Alguns aplicativos podem ser afetados por essas atualizações mais do que outros.</span><span class="sxs-lookup"><span data-stu-id="6f30f-111">Some applications may be impacted by these updates more than others.</span></span> <span data-ttu-id="6f30f-112">Aplicativos que executam o processamento de eventos em tempo real, streaming de mídia ou transcodificação ou alta taxa de transferência de rede cenários, por exemplo, não podem ser projetado tootolerate 30 segundo intervalo.</span><span class="sxs-lookup"><span data-stu-id="6f30f-112">Applications that perform real-time event processing, media streaming or transcoding, or high throughput networking scenarios, for example, may not be designed tootolerate a 30 second pause.</span></span> <span data-ttu-id="6f30f-113">Aplicativos em execução em uma máquina virtual poderá obter informações sobre atualizações futuras Olá chamada [eventos agendados](../virtual-machines-scheduled-events.md) API de saudação [Azure metadados de serviço](../virtual-machines-instancemetadataservice-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6f30f-113">Applications running in a virtual machine can learn about upcoming updates by calling hello [Scheduled Events](../virtual-machines-scheduled-events.md) API of hello [Azure Metadata Service](../virtual-machines-instancemetadataservice-overview.md).</span></span>
