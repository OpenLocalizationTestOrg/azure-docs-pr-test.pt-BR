---
title: "aaaConnect VMs do Linux em um serviço de nuvem | Microsoft Docs"
description: "Conecte máquinas virtuais Linux criadas com tooan de modelo de implantação clássico Olá serviço de nuvem do Azure ou rede virtual."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 2fd23055-6b34-4ef0-88a8-fc19e32fb3c9
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: cynthn
ms.openlocfilehash: 323baf04390d53ffb2810e24a24d175c08e60cd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-linux-virtual-machines-created-with-hello-classic-deployment-model-with-a-virtual-network-or-cloud-service"></a>Conectar máquinas virtuais Linux criadas com o modelo de implantação clássico Olá com um serviço de nuvem ou rede virtual
> [!IMPORTANT]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.

Máquinas virtuais Linux criadas com o modelo de implantação clássico Olá sempre são colocadas em um serviço de nuvem. serviço de nuvem Olá atua como um contêiner e fornece um nome DNS público exclusivo, um endereço IP público e um conjunto de pontos de extremidade tooaccess Olá virtual machine sobre Olá da Internet. serviço de nuvem Olá pode estar em uma rede virtual, mas que não é um requisito. Você também pode [Conectar máquinas virtuais do Windows a uma rede virtual ou serviço de nuvem](../../windows/classic/connect-vms.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Se um serviço de nuvem não estiver em uma rede virtual, ele será chamado de serviço de nuvem *autônomo* . máquinas virtuais de saudação em um serviço de nuvem autônomo se comunicar com outras máquinas virtuais usando Olá nomes DNS públicos de outras máquinas virtuais e tráfego de saudação percorram Olá da Internet. Se um serviço de nuvem está em uma rede virtual, máquinas virtuais de saudação em que o serviço de nuvem pode se comunicar com todas as outras máquinas virtuais na rede virtual Olá sem enviar qualquer tráfego por Olá da Internet.

Se você colocar Olá de suas máquinas virtuais no mesmo serviço de nuvem autônomo, você ainda pode usar o balanceamento de carga e conjuntos de disponibilidade. Para obter detalhes, consulte [máquinas virtuais de balanceamento de carga](../../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) e [gerenciar Olá disponibilidade das máquinas virtuais](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). No entanto, você não é possível organizar as máquinas virtuais de saudação em sub-redes ou conectar uma rede de local autônomo nuvem serviço tooyour. Aqui está um exemplo:

[!INCLUDE [virtual-machines-common-classic-connect-vms](../../../../includes/virtual-machines-common-classic-connect-vms.md)]

## <a name="next-steps"></a>Próximas etapas
Depois de criar uma máquina virtual, é uma boa ideia muito[adicionar um disco de dados](attach-disk.md) para seus serviços e cargas de trabalho tenham um toostore de dados local.
