---
title: "Planejar a rede para replicação do Hyper-V em um site secundário com o Azure Site Recovery | Microsoft Docs"
description: "Este artigo aborda o planejamento de rede ao replicar VMs do Hyper-V para um site de VMM secundário do System Center com o Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 095f2d73-994e-4fc0-96f2-e03a7d72e492
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: raynew
ms.openlocfilehash: a1f3f6e6cba074647195e2b0cbcdc7b4f3dec475
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="step-3-plan-networking-for-hyper-v-vm-replication-to-a-secondary-vmm-site"></a>Etapa 3: planejar a rede para replicação de VM Hyper-V para um site secundário do VMM

Depois de revisar os pré-requisitos de implantação, leia este artigo para planejar a rede na replicação de VMs (máquinas virtuais) Hyper-V gerenciadas em nuvens do System Center Virtual Machine Manager (VMM) para um site secundário usando o [Azure Site Recovery](site-recovery-overview.md) no portal do Azure. 

Depois de ler este artigo, poste comentários na parte inferior ou no [Fórum dos Serviços de Recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="network-mapping-overview"></a>Visão geral de mapeamento de rede

Mapeamento de rede é usado ao replicar máquinas virtuais do Hyper-V (gerenciados no VMM) em um datacenter secundário. O mapeamento de rede mapeia entre as redes de VM em um servidor VMM de origem e as redes do Azure de destino. Mapeamento faz o seguinte:

- **Conexão de rede**— Conecta VMs a redes apropriadas após o failover. A máquina virtual de réplica será conectada à rede de destino mapeada para a rede de origem.
- **O posicionamento ideal**— Idealmente, coloca as máquinas virtuais de réplica nos servidores host Hyper-V. As máquinas virtuais de réplica serão colocadas em hosts que podem acessar as redes VM mapeadas.
- **Nenhum mapeamento de rede**— se você não configurar o mapeamento de rede, as máquinas virtuais replicadas não serão conectadas às redes VM após o failover.


### <a name="example"></a>Exemplo

A seguir, um exemplo para ilustrar esse mecanismo. Vamos usar uma organização com dois locais, Nova Iorque e Chicago.

**Localidade** | **Servidor VMM** | **Redes VM** | **Mapeado para**
---|---|---|---
Nova Iorque | VMM-NewYork| VMNetwork1-NewYork | Mapeado para VMNetwork1-Chicago
 |  | VMNetwork2-NewYork | Não mapeado
Chicago | VMM-Chicago| VMNetwork1-Chicago | Mapeado para VMNetwork1-NewYork
 | | VMNetwork1-Chicago | Não mapeado

Neste exemplo:

- Quando uma máquina virtual de réplica é criada para qualquer máquina virtual conectada a VMNetwork1-NewYork, ela é conectada a VMNetwork1-Chicago.
- Quando uma máquina virtual de réplica é criada para VMNetwork2-NewYork ou VMNetwork2-Chicago, ele não é conectada a nenhuma rede.

Veja como as nuvens do VMM são configuradas em nosso exemplo de organização e como as redes lógicas são associadas às nuvens.

#### <a name="cloud-protection-settings"></a>Configurações de proteção de nuvem

**Nuvem protegida** | **Protegendo a nuvem** | **Rede lógica (Nova Iorque)**  
---|---|---
GoldCloud1 | GoldCloud2 |
SilverCloud1| SilverCloud2 |
GoldCloud2 | <p>ND</p><p></p> | <p>LogicalNetwork1-NewYork</p><p>LogicalNetwork1-Chicago</p>
SilverCloud2 | <p>ND</p><p></p> | <p>LogicalNetwork1-NewYork</p><p>LogicalNetwork1-Chicago</p>

#### <a name="logical-and-vm-network-settings"></a>Configurações de rede lógica e de VM

**Localidade** | **Rede lógica** | **Rede VM associada**
---|---|---
Nova Iorque | LogicalNetwork1-NewYork | VMNetwork1-NewYork
Chicago | LogicalNetwork1-Chicago | VMNetwork1-Chicago
 | LogicalNetwork2Chicago | VMNetwork2-Chicago

#### <a name="target-network-settings"></a>Configurações de rede de destino

Com base nessas configurações, ao selecionar a rede VM de destino, a tabela a seguir mostra as opções disponíveis.

**Seleção** | **Nuvem protegida** | **Protegendo a nuvem** | **Rede de destino disponível**
---|---|---|---
VMNetwork1-Chicago | SilverCloud1 | SilverCloud2 | Disponível
 | GoldCloud1 | GoldCloud2 | Disponível
VMNetwork2-Chicago | SilverCloud1 | SilverCloud2 | Não disponível
 | GoldCloud1 | GoldCloud2 | Disponível


Se a rede de destino tiver várias sub-redes e uma delas tiver o mesmo nome que a sub-rede em que a máquina virtual de origem está localizada, a máquina virtual de réplica será conectada a essa sub-rede de destino após o failover. Se não houver uma sub-rede de destino com um nome correspondente, a máquina virtual será conectada à primeira sub-rede na rede.


#### <a name="failback-behavior"></a>Comportamento de failback

Para ver o que acontece no caso de failback (replicação inversa), vamos supor que a VMNetwork1-NewYork seja mapeada para VMNetwork1-Chicago, com as configurações a seguir.


**Máquina virtual** | **Conectado à rede VM**
---|---
VM1 | VMNetwork1-Rede
VM2 (réplica de VM1) | VMNetwork1-Chicago

Com essas configurações, vamos analisar o que acontece em alguns cenários possíveis.

**Cenário** | **Resultado**
---|---
Nenhuma alteração nas propriedades de rede de VM-2 após o failover. | A VM-1 permanece conectada à rede de origem.
As propriedades de rede de VM-2 são alteradas após o failover e ela é desconectada. | A VM-1 é desconectada.
As propriedades de rede de VM-2 são alteradas após o failover e ela é conectada à VMNetwork2-Chicago. | Se a VMNetwork2-Chicago não estiver mapeada, a VM-1 será desconectada.
O mapeamento de rede da VMNetwork1-Chicago é alterado. | A VM-1 será conectada à rede, agora mapeada para VMNetwork1-Chicago.



## <a name="prepare-for-network-mapping"></a>Prepare-se para o mapeamento de rede

1. Em servidores VMM de origem e destino, você deve ter uma rede lógica associada às nuvens de origem e destino. 
2. Nos servidores de origem e destino, você deve ter uma rede de VM vinculada à rede lógica.
3. As VMs em hosts Hyper-V no local de origem devem ser vinculadas à rede de VM de origem. Se você estiver usando apenas um único servidor VMM, poderá configurar o mapeamento entre as redes de VM no mesmo servidor.

Veja o que acontece quando você configura o mapeamento de rede durante a implantação do Site Recovery:

- Quando você configurar o mapeamento de rede e seleciona uma rede de VM de destino, as nuvens de origem do VMM que usam a rede de VM de origem serão exibidas juntamente com as redes de VM de destino disponíveis nas nuvens de destino.
- - Quando o mapeamento de rede é configurado corretamente e a replicação é habilitada, uma VM de origem será conectada à rede da VM de origem e sua réplica no local de destino será conectada à rede de VM mapeada.
- Se a rede de destino tiver várias sub-redes e uma delas tiver o mesmo nome que a sub-rede em que a máquina virtual de origem está localizada, a máquina virtual de réplica será conectada a essa sub-rede de destino após o failover. Se não houver uma sub-rede de destino com um nome correspondente, a VM será conectada à primeira sub-rede na rede.

## <a name="connect-to-vms-after-failover"></a>Conectar a VMs depois do failover

Ao planejar sua estratégia de replicação e failover, uma das principais questões é como se conectar à réplica após o failover. Há duas opções: 

- **Usar outro endereço IP**: você pode optar por usar outro endereço IP para a VM replicada. Nesse cenário, a VM obtém um novo endereço IP após o failover e uma atualização de DNS é necessária.
- **Manter o mesmo endereço IP**: você pode querer usar o mesmo endereço IP para a VM de réplica. Manter os mesmos endereços IP simplifica a recuperação, reduzindo problemas relacionados à rede após o failover. 

## <a name="retain-ip-addresses"></a>Reter os endereços IP

Se você deseja manter os endereços IP do site primário após o failover para o site secundário, pode fazer um failover de sub-rede completo e atualizar as rotas para indicar o novo local dos endereços IP ou, como alternativa, implantar uma sub-rede ampliada entre o site primário e o de recuperação.

### <a name="stretched-subnet"></a>Sub-rede ampliada

Em uma sub-rede ampliada, a sub-rede fica disponível simultaneamente nos sites primário e secundário. Se você mover um servidor e sua configuração IP (Camada 3) para o site secundário, a rede roteará o tráfego para o novo local automaticamente. 

Do ponto de vista da Camada 2 (camada de link de dados), você precisa de equipamento de rede que possa gerenciar uma VLAN ampliada. Além disso, a ampliação da VLAN estende o potencial domínio de falha estende-se para os dois sites, essencialmente tornando-se um ponto único de falha. Embora isso seja improvável, pode ocorrer uma tempestade de transmissão que não poderá ser isolada. 


### <a name="subnet-failover"></a>Failover da sub-rede

Você pode executar um failover de sub-rede para obter as vantagens da sub-rede ampliada, sem realmente ampliá-la. Nesta solução, uma sub-rede estará disponível no site de origem ou destino, mas não em ambos ao mesmo tempo. Para manter o espaço de endereço IP no caso de um failover, você pode organizar por meio de programação para a infra-estrutura do roteador mover as sub-redes de um site para outro. Quando ocorre o failover, as sub-redes se movem com as VMs associadas. A principal desvantagem é que, em caso de falha, você precisa mover toda a sub-rede.

### <a name="example"></a>Exemplo

Aqui está um exemplo de failover de sub-rede completo. O site principal tem aplicativos em execução na sub-rede 192.168.1.0/24. No failover, todas as VMs nessa sub-rede fazem failover para o site secundário e mantêm seus endereços IP. As rotas precisam ser modificadas para refletir o fato de que todas as máquinas virtuais VM que pertencem à sub-rede 192.168.1.0/24 agora foram movidas para o site secundário.

Os gráficos a seguir mostram as sub-redes antes e após o failover:

- Antes do failover, a sub-rede 192.168.0.1/24 está ativa no site de origem. Ela fica ativa no site secundário após o failover.
- As rotas entre o site primário e o site de recuperação, o terceiro site e o site primário, e o terceiro site e o site de recuperação precisarão ser modificadas devidamente.

**Antes do failover**

![Antes do failover](./media/vmm-to-vmm-walkthrough-network/network-design2.png)

**Após o failover**

![Após o failover](./media/vmm-to-vmm-walkthrough-network/network-design3.png)

Após o failover, eis o que acontece:

- A Recuperação de site aloca um endereço IP para cada interface de rede na VM a partir do pool de endereços IP estáticos na rede relevante para cada instância do VMM.
- Se o pool de endereços IP no site secundário é o mesmo que no site de origem, o Site Recovery aloca o mesmo endereço IP (da VM de origem) para a VM de réplica. O endereço IP está reservado no VMM, mas não está definido como o endereço IP de failover no host Hyper-V. O endereço IP de failover em um host do Hyper-V é definido logo antes do failover.
- Se o mesmo endereço IP não estiver disponível, o Site Recovery alocará outro endereço IP do pool.
- Se as VMs usam DHCP, o Site Recovery não gerencia os endereços IP. Você precisa verificar se o servidor DHCP no site secundário pode alocar o endereço do mesmo intervalo que o site de origem.

### <a name="validate-the-ip-address"></a>Validar o endereço IP

Depois de habilitar a proteção para uma VM, você pode usar o script de exemplo a seguir para verificar o endereço atribuído à VM. O mesmo endereço IP será definido como o endereço IP de failover e atribuído à VM no momento do failover:

    ```
    $vm = Get-SCVirtualMachine -Name <VM_NAME>
    $na = $vm[0].VirtualNetworkAdapters>
    $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
    $ip.address 
    ```

## <a name="changing-ip-addresses"></a>Alterando endereços IP

Neste cenário, os endereços IP das VMs que fazem failover são alterados. A desvantagem dessa solução é a manutenção necessária. Normalmente, o DNS será atualizado após a inicialização das VMs de réplica. As entradas DNS talvez precisem ser alteradas ou embaralhadas na rede, e as entradas em cache, atualizadas. Isso pode resultar em tempo de inatividade. O tempo de inatividade pode ser atenuado da seguinte maneira:

- Use valores TTL baixos para aplicativos de intranet.
- Use o script a seguir em um plano de recuperação do Site Recovery para atualizar o servidor DNS e garantir uma atualização em tempo hábil. O script não será necessário se você usar o registro DNS dinâmico.

    ```
    param(
    string]$Zone,
    [string]$name,
    [string]$IP
    )
    $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
    $newrecord = $record.clone()
    $newrecord.RecordData[0].IPv4Address  =  $IP
    Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord
    ```
    
### <a name="example"></a>Exemplo 

Vamos examinar um cenário no qual você está planejando usar endereços IP diferentes entre o site primário e o de recuperação. Neste exemplo, temos endereços IP diferentes em sites primários e secundários, e existe um terceiro site de onde os aplicativos hospedados no site primário ou de recuperação podem ser acessados.

- Antes do failover, os aplicativos são hospedados na sub-rede 192.168.1.0/24 no site primário e configurados para ficarem na sub-rede 172.16.1.0/24 no site secundário após um failover.
- Rotas de rede/conexões de VPN foram configuradas corretamente para que todos os três sites possam acessar um ao outro.
- Após o failover, os aplicativos serão restaurados na sub-rede de recuperação. Nesse cenário, não é necessário fazer o failover da sub-rede inteira, e nenhuma alteração é necessária para reconfigurar as rotas de rede ou VPN. O failover e algumas atualizações DNS manterão os aplicativos acessíveis.
- Se o DNS está configurado para permitir atualizações dinâmicas, as VMs farão o registro por conta própria usando o novo endereço IP na inicialização depois do failover.

**Antes do failover**

![IP diferente - antes do failover](./media/vmm-to-vmm-walkthrough-network/network-design10.png)

**Após o failover**

![IP diferente - após o failover](./media/vmm-to-vmm-walkthrough-network/network-design11.png)



## <a name="next-steps"></a>Próximas etapas

Vá para a [Etapa 4: preparar o VMM e o Hyper-V](vmm-to-vmm-walkthrough-vmm-hyper-v.md).


