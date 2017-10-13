---
title: "Conectar VMs Linux em um serviço de nuvem | Microsoft Docs"
description: "Conectar máquinas virtuais Linux criadas com o modelo clássico de implantação a um serviço de nuvem ou de rede virtual do Azure."
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
ms.openlocfilehash: e222645509640b104410f87e4bcd22834c8d9ec1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-linux-virtual-machines-created-with-the-classic-deployment-model-with-a-virtual-network-or-cloud-service"></a>Conectar máquinas virtuais Linux criadas com o modelo clássico de implantação com um serviço de nuvem ou de rede virtual
> [!IMPORTANT]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md). Este artigo aborda o uso do modelo de implantação Clássica. A Microsoft recomenda que a maioria das implantações novas use o modelo do Gerenciador de Recursos.

As máquinas virtuais Linux criadas com o modelo de implantação clássico sempre são colocadas em um serviço de nuvem. O serviço de nuvem funciona como um contêiner e fornece um nome DNS público exclusivo, um endereço IP público e um conjunto de pontos de extremidade para acessar a máquina virtual pela Internet. O serviço de nuvem pode estar em uma rede virtual, mas isso não é um requisito. Você também pode [Conectar máquinas virtuais do Windows a uma rede virtual ou serviço de nuvem](../../windows/classic/connect-vms.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Se um serviço de nuvem não estiver em uma rede virtual, ele será chamado de serviço de nuvem *autônomo* . As máquinas virtuais em um serviço de nuvem autônomo se comunicam com outras máquinas virtuais usando os nomes DNS públicos de outras máquinas virtuais, e o tráfego viaja pela Internet. Se um serviço de nuvem estiver em uma rede virtual, as máquinas virtuais no serviço de nuvem podem se comunicar com todas as outras máquinas virtuais na rede virtual sem enviar tráfego pela Internet.

Ao colocar as máquinas virtuais no mesmo serviço de nuvem autônomo, você ainda pode usar o balanceamento de carga e os conjuntos de disponibilidade. Para obter detalhes, confira [Máquinas virtuais de balanceamento de carga](../../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) e [Gerenciar a disponibilidade de máquinas virtuais](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). No entanto, você não pode organizar as máquinas virtuais em sub-redes ou conectar um serviço de nuvem autônomo à sua rede local. Aqui está um exemplo:

[!INCLUDE [virtual-machines-common-classic-connect-vms](../../../../includes/virtual-machines-common-classic-connect-vms.md)]

## <a name="next-steps"></a>Próximas etapas
Após criar uma máquina virtual, é uma boa ideia [adicionar um disco de dados](attach-disk.md) para que seus serviços e cargas de trabalho tenham um local para armazenar dados.
