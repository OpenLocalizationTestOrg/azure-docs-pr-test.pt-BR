---
title: "Solução de problemas de falhas de alocação de VM do Windows | Microsoft Docs"
description: "Solucionar problemas de falhas de alocação ao criar, reiniciar ou redimensionar uma VM do Windows no Azure"
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue,azure-resource-manager,azure-service-management
ms.assetid: bb939e23-77fc-4948-96f7-5037761c30e8
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: cjiang
ms.openlocfilehash: 57925b5a75fd8bcf2a9450025b5dc51eb552353f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-allocation-failures-when-you-create-restart-or-resize-windows-vms-in-azure"></a>Solucionar problemas de falhas de alocação ao criar, reiniciar ou redimensionar VMs do Windows no Azure
Quando você cria uma VM, reinicia VMs paradas (desalocadas) ou redimensiona uma VM, o Microsoft Azure aloca recursos de computação para sua assinatura. Eventualmente, você pode receber mensagens de erro durante a execução dessas operações, antes de alcançar os limites da assinatura do Azure. Este artigo explica as causas das falhas de alocação mais comuns e sugere possíveis correções. As informações também poderão ser úteis caso você pretenda implantar serviços. Também é possível [solucionar problemas de falhas de alocação ao criar, reiniciar ou redimensionar VMs do Linux no Azure](../linux/allocation-failure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

[!INCLUDE [virtual-machines-common-allocation-failure](../../../includes/virtual-machines-common-allocation-failure.md)]

