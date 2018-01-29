---
title: "Configurar o endereçamento IP para se conectar após o failover para o Azure com o Azure Site Recovery | Microsoft Docs"
description: "Descreve como configurar o endereçamento IP para se conectar a VMs do Azure após o failover do local com o Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: prateek9us
manager: carmonm
editor: 
ms.assetid: f02cdbea-0940-48bf-9fa5-f38d9e584fae
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 11/14/2017
ms.author: pratshar
ms.openlocfilehash: 5519a965d9828cfa1e73ba12f8acd1d509a36a66
ms.sourcegitcommit: 9a61faf3463003375a53279e3adce241b5700879
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2017
---
# <a name="set-up-ip-addressing-to-connect-after-failover-to-azure"></a>Configurar o endereçamento IP para se conectar após o failover para o Azure

Esse artigo explica os requisitos de rede para se conectar a VMs do Azure, depois de usar o serviço [Azure Site Recovery](site-recovery-overview.md) para replicação e failover para o Azure.

Neste artigo, você aprenderá sobre:

> [!div class="checklist"]
> * Os métodos de conexão que você pode usar
> * Como usar um endereço IP diferente para VMs do Azure replicadas
> * Como manter os endereços IP para VMs do Azure após o failover

## <a name="connecting-to-replica-vms"></a>Conectando-se a VMs de réplica

Ao planejar sua estratégia de replicação e failover, uma das principais questões é como se conectar à VM do Azure após o failover. Há algumas opções ao criar sua estratégia de rede para VMs de réplica do Azure:

- **Usar outro endereço IP**: Você pode optar por usar outro intervalo de endereços IP para a rede da VM replicada do Azure. Nesse cenário, a VM obtém um novo endereço IP após o failover e uma atualização de DNS é necessária.
- **Manter o mesmo endereço IP**: Talvez você deseje usar o mesmo intervalo de endereços IP do site primário local para a rede do Azure após o failover. Manter os mesmos endereços IP simplifica a recuperação, reduzindo problemas relacionados à rede após o failover. No entanto, quando você estiver replicando para o Azure, precisará atualizar as rotas com o novo local dos endereços IP após o failover. 

## <a name="retaining-ip-addresses"></a>Retenção de endereços IP

O Site Recovery fornece a capacidade de manter endereços IP fixos durante o failover para o Azure, com um failover de sub-rede.

- Com o failover de sub-rede, uma sub-rede específica está presente no Site 1 ou Site 2, mas nunca em ambos os sites ao mesmo tempo.
- Para manter o espaço de endereço IP no caso de um failover, de forma programática, faça com que a infraestrutura do roteador mova as sub-redes de um site para outro.
- Durante o failover, as sub-redes são movidas com as VMs protegidas associadas. A principal desvantagem é que, em caso de falha, você precisa mover toda a sub-rede.


### <a name="failover-example"></a>Exemplo de failover

Vejamos um exemplo para o failover para o Azure usando uma organização fictícia, chamada Woodgrove Bank.

- O Woodgrove Bank hospeda seus aplicativos de negócios em um site local. Eles hospedam seus aplicativos móveis no Azure.
- Há conectividade VPN site a site entre a rede de borda local deles e a rede virtual do Azure. Devido a essa conexão VPN, a rede virtual no Azure aparece como uma extensão da rede local.
- O Woodgrove deseja replicar as cargas de trabalho locais para o Azure com o Site Recovery.
 - O Woodgrove tem aplicativos que dependem de endereços IP embutidos em código, então eles precisam manter endereços IP para seus aplicativos após o failover para o Azure.
 - Recursos em execução no Azure usam o intervalo de endereços IP 172.16.1.0/24, 172.16.2.0/24.

![Antes do failover da sub-rede](./media/site-recovery-network-design/network-design7.png)

**Infraestrutura antes do failover**


Para que o Woodgrove consiga replicar suas VMs para o Azure, ao mesmo tempo que mantém os endereços IP, veja o que a empresa precisa fazer:


1. Crie rede virtual do Azure, na qual as VMs do Azure serão criadas depois do failover de máquinas locais. Ela deve ser uma extensão da rede local, de forma que os aplicativos possam fazer failover de forma ininterrupta.
2. Antes do failover, no Site Recovery, eles atribuem o mesmo endereço IP nas propriedades do computador. Após o failover, o Site Recovery atribui esse endereço à VM do Azure.
3. Após o failover ser executado e as VMs do Azure serem criadas com o mesmo endereço IP, eles se conectarão à rede usando uma [conexão de VNet para VNet](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md). Essa ação pode ser inserida em um script.
4. Eles precisam modificar rotas de modo a refletir que 192.168.1.0/24 agora foi movido para o Azure.


**Infraestrutura após o failover**

![Após o failover da sub-rede](./media/site-recovery-network-design/network-design9.png)

#### <a name="site-to-site-connection"></a>Conexão site a site

Além da conexão de VNet a VNet, após o failover, o Woodgrove pode configurar a conectividade VPN site a site:
- Quando você configura uma conexão site a site, na rede do Azure, você só poderá rotear o tráfego para a localização local (rede local) se o intervalo de endereços IP for diferente do intervalo de endereços IP local. Isso ocorre porque o Azure não dá suporte a sub-redes ampliadas. Portanto, se você tiver uma sub-rede 192.168.1.0/24 local, não poderá adicionar uma rede local 192.168.1.0/24 à rede do Azure. Isso é esperado, porque o Azure não reconhece que não há nenhuma VM ativa na sub-rede e que a sub-rede está sendo criada apenas para fins de recuperação de desastre.
- Para poder encaminhar o tráfego de rede corretamente para fora de uma rede do Azure, as sub-redes na rede e a rede local não devem entrar em conflito.




## <a name="assigning-new-ip-addresses"></a>Atribuindo novos endereços IP

Esta [postagem no blog](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) explica como configurar a infraestrutura de rede do Azure quando você não precisa reter os endereços IP após o failover. Ela começa com uma descrição do aplicativo, explica como configurar a rede local e no Azure e termina com informações sobre como executar failovers. 

## <a name="next-steps"></a>Próximas etapas
[Executar um failover](site-recovery-failover.md)




