---
title: "mapeamento de aaaNetwork entre duas regiões do Azure no Azure Site Recovery | Microsoft Docs"
description: "O Azure Site Recovery coordena a replicação hello, failover e recuperação de máquinas virtuais e servidores físicos. Saiba mais sobre tooAzure de failover ou um datacenter secundário."
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: pratshar
ms.openlocfilehash: 4f80c44e3f94eaf446bc01a7041d91fe34aa78d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="network-mapping-between-two-azure-regions"></a>Mapeamento de rede entre duas regiões do Azure


Este artigo descreve como toomap Azure redes virtuais de duas regiões do Azure com o outro. Mapeamento de rede garante que, quando a máquina virtual replicada é criada no destino Olá região do Azure, é criado na rede virtual de saudação que é mapeada toovirtual rede de saudação da máquina virtual de origem.  

## <a name="prerequisites"></a>Pré-requisitos
Antes de mapear as redes, certifique-se de que você criou [redes virtuais do Azure](../virtual-network/virtual-networks-overview.md) em ambas as regiões do Azure de origem e de destino.

## <a name="map-networks"></a>Mapear redes

toomap uma rede virtual do Azure na rede virtual de tooanother de uma região do Azure em outra região, vá tooSite infra-estrutura de recuperação -> mapeamento de rede (para máquinas virtuais do Azure) e criar um mapeamento de rede.

![Mapeamento de rede](./media/site-recovery-network-mapping-azure-to-azure/network-mapping1.png)


Em Olá exemplo abaixo minha máquina virtual está em execução na região da Ásia Oriental e está sendo replicada tooSoutheast Ásia.

Selecione a rede de origem e destino hello e clique em toocreate Okey um mapeamento de rede da Ásia Oriental tooSoutheast Ásia.

![Mapeamento de rede](./media/site-recovery-network-mapping-azure-to-azure/network-mapping2.png)


Olá a mesma coisa toocreate um mapeamento de rede de tooEast Ásia Sudeste da Ásia.  
![Mapeamento de rede](./media/site-recovery-network-mapping-azure-to-azure/network-mapping3.png)


## <a name="mapping-network-when-enabling-replication"></a>Mapeamento de rede ao habilitar a replicação

Se o mapeamento de rede não for feito, quando você estiver replicando uma máquina virtual para Olá primeiro tempo formulário uma região do Azure tooanother, em seguida, você pode escolher rede de destino como parte da saudação mesmo processo. Recuperação de site cria mapeamentos de rede de região de tootarget de região de origem e de região de toosource da região de destino com base nessa seleção.   

![Mapeamento de rede](./media/site-recovery-network-mapping-azure-to-azure/network-mapping4.png)

Por padrão, a recuperação de Site cria uma rede na região de destino de saudação é a rede de origem toohello idênticos e adicionando '-asr' como um nome de toohello sufixo da rede de origem de saudação. Você pode escolher uma rede já criada, clicando em Personalizar.

![Mapeamento de rede](./media/site-recovery-network-mapping-azure-to-azure/network-mapping5.png)


Se o mapeamento de rede Olá já for feito, você não pode alterar a rede virtual de destino Olá durante a habilitação da replicação. toochange, modifique o mapeamento de rede existente.  

![Mapeamento de rede](./media/site-recovery-network-mapping-azure-to-azure/network-mapping6.png)

![Mapeamento de rede](./media/site-recovery-network-mapping-azure-to-azure/modify-network-mapping.png)

> [!IMPORTANT]
> Se você modificar um mapeamento de rede de 1 a região tooregion-2, verifique se que você modificar o mapeamento de rede de saudação de região 2 tooregion-1 também.
>
>


## <a name="subnet-selection"></a>Seleção de sub-rede
Subrede Olá virtual da máquina de destino é selecionada com base no nome de saudação da sub-rede de saudação de saudação da máquina virtual de origem. Se houver uma sub-rede de saudação mesmo nome da máquina virtual de origem de saudação disponível na rede de destino hello, em seguida, o que é escolhido para a máquina de virtual de destino hello. Se não houver nenhuma sub-rede com hello mesmo nome na rede de destino hello, em seguida, em ordem alfabética primeira sub-rede é escolhido como Olá sub-rede de destino. Você pode modificar essa sub-rede indo tooCompute e as configurações de rede da máquina virtual de saudação.

![Modificar sub-rede](./media/site-recovery-network-mapping-azure-to-azure/modify-subnet.png)


## <a name="ip-address"></a>Endereço IP

Endereço IP para cada interface de rede Olá Olá virtual da máquina de destino é escolhido da seguinte maneira:

### <a name="dhcp"></a>DHCP
Se a interface de rede Olá Olá da máquina virtual de origem estiver usando DHCP, a interface de rede da máquina de virtual de destino Olá também é definido como DHCP.

### <a name="static-ip"></a>IP Estático
Se a interface de rede Olá Olá da máquina virtual de origem estiver usando um IP estático, a interface de rede da máquina de virtual de destino Olá também será definido toouse IP estático. O IP estático é escolhido da seguinte maneira:

#### <a name="same-address-space"></a>Mesmo espaço de endereço

Se Olá fonte subrede e sub-rede de destino Olá tem Olá mesmo espaço de endereço, IP de destino é definido igual ao IP Olá Olá da interface de rede de saudação da máquina virtual de origem. Se o mesmo IP não estiver disponível, alguns outros IP disponível é definido como Olá IP de destino.

#### <a name="different-address-space"></a>Espaço de endereço diferente

Se Olá fonte subrede e sub-rede de destino Olá tiverem espaço de endereço diferente, IP de destino é definido como qualquer IP disponível na sub-rede de destino hello.

Você pode modificar o IP de destino de saudação em cada interface de rede indo tooCompute e as configurações de rede da máquina virtual de saudação.

## <a name="next-steps"></a>Próximas etapas

- Saiba mais sobre as [diretrizes de rede para replicação de VMs do Azure](site-recovery-azure-to-azure-networking-guidance.md).
