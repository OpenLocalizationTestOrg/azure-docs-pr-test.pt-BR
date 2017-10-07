---
title: "aaaSet pontos de extremidade em uma VM do Linux clássica | Microsoft Docs"
description: "Saiba mais sobre o tooset pontos de extremidade para uma VM do Linux no hello comunicação tooallow de portal clássico do Azure com uma máquina virtual do Linux no Azure"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: f3749738-1109-4a1d-8635-40e4bd220e91
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: cynthn
ms.openlocfilehash: 1c959d10dd1e20228fa4a20e1cc0205c1d12f185
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-endpoints-on-a-linux-classic-virtual-machine-in-azure"></a>Como tooset pontos de extremidade em uma máquina virtual clássica do Linux no Azure
Todas as máquinas virtuais Linux criadas no Azure usando o modelo de implantação clássico Olá podem se comunicar automaticamente por um canal de rede privada com outras máquinas virtuais no hello que mesmo serviço ou de rede virtual na nuvem. No entanto, os computadores Olá Internet ou outras redes virtuais requerem pontos de extremidade toodirect Olá rede de entrada tráfego tooa máquina virtual. Este artigo também está disponível para [máquinas virtuais do Windows](../../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

> [!IMPORTANT]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.

Em Olá **Gerenciador de recursos de** modelo de implantação, pontos de extremidade são configurados usando **grupos de segurança de rede (NSGs)**. Para saber mais, consulte [Abrir portas e pontos de extremidade](../nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Quando você cria uma máquina virtual Linux em Olá portal do Azure, um ponto de extremidade para o Secure Shell (SSH) é normalmente criado para você automaticamente. Você pode configurar pontos de extremidade adicionais durante a criação de máquina virtual de hello, ou posteriormente, conforme necessário.

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a>Próximas etapas
* Você também pode criar um ponto de extremidade VM usando Olá [Interface de linha de comando do Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2). Executar Olá **criar ponto de extremidade de vm do azure** comando.
* Se você criou uma máquina virtual no modelo de implantação do Gerenciador de recursos de saudação, você pode usar Olá CLI do Azure no Gerenciador de recursos de modo muito[criar grupos de segurança de rede](../../../virtual-network/virtual-networks-create-nsg-arm-cli.md) toocontrol tráfego toohello VM.
