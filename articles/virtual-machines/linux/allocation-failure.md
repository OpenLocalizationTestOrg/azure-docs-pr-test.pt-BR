---
title: "aaaTroubleshooting VM Linux falhas de alocação | Microsoft Docs"
description: "Solucionar problemas de falhas de alocação ao criar, reiniciar ou redimensionar uma VM do Linux no Azure"
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue,azure-resourece-manager,azure-service-management
ms.assetid: 1ef41144-6dd6-4a56-b180-9d8b3d05eae7
ms.service: virtual-machines-linux
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2016
ms.author: cjiang
ms.openlocfilehash: 502fbb406b0b4acf086c2586795f69a44cc1a004
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-allocation-failures-when-you-create-restart-or-resize-linux-vms-in-azure"></a>Solucionar problemas de falhas de alocação ao criar, reiniciar ou redimensionar VMs do Linux no Azure
Quando você cria uma VM, reiniciar paradas VMs (desalocadas) ou redimensiona uma VM, o Microsoft Azure aloca recursos de computação tooyour assinatura. Ocasionalmente, você poderá receber erros ao executar essas operações – mesmo antes de atingir Olá limites de assinatura do Azure. Este artigo explica as causas de saudação de alguns Olá comuns de falhas de alocação e sugere possíveis correções. informações de saudação também podem ser útil ao planejar a implantação Olá dos seus serviços. Também é possível [solucionar problemas de falhas de alocação ao criar, reiniciar ou redimensionar VMs do Windows no Azure](../windows/allocation-failure.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

[!INCLUDE [virtual-machines-common-allocation-failure](../../../includes/virtual-machines-common-allocation-failure.md)]

