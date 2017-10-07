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
# <a name="vm-preserving-maintenance-in-place-vm-migration"></a>Manutenção para preservar VMs (migração de VMs no local)

Embora maioria Olá das atualizações não tenham toohosted nenhum impacto VMs, há casos em que atualizações toocomponents ou serviços resultam em interferência mínima toorunning VMs (sem a reinicialização completa da máquina virtual de saudação).

Essas atualizações são realizadas com tecnologia que permite a migração dinâmica, também nomeada de "atualização que preservam a memória". Ao atualizar host Olá, máquina virtual de saudação é colocada em um estado "pausado", preservando memória RAM, Olá enquanto hello (por exemplo, o sistema operacional subjacente) do ambiente de hospedagem aplica patches e atualizações necessárias hello.
máquina virtual de saudação é retomada dentro de 30 segundos de em pausa.
Depois de retomar, Olá relógio da máquina virtual de saudação é sincronizado automaticamente.

Nem todas as atualizações podem ser implantadas por meio desse mecanismo, mas determinado período pequena pausa, implantar as atualizações na forma consideravelmente reduz máquinas de toovirtual de impacto.

Atualizações de múltiplas instâncias (VMs em um conjunto de disponibilidade) são aplicadas em um domínio de atualização por vez.

Alguns aplicativos podem ser afetados por essas atualizações mais do que outros. Aplicativos que executam o processamento de eventos em tempo real, streaming de mídia ou transcodificação ou alta taxa de transferência de rede cenários, por exemplo, não podem ser projetado tootolerate 30 segundo intervalo. Aplicativos em execução em uma máquina virtual poderá obter informações sobre atualizações futuras Olá chamada [eventos agendados](../virtual-machines-scheduled-events.md) API de saudação [Azure metadados de serviço](../virtual-machines-instancemetadataservice-overview.md).
