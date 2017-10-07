---
title: "aaaPlan de rede para o Hyper-V replicação tooa VMM site secundário com o Azure Site Recovery | Microsoft Docs"
description: "Este artigo descreve o planejamento da rede ao replicar máquinas virtuais do Hyper-V tooa System Center VMM site secundário com o Azure Site Recovery."
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
ms.openlocfilehash: 5934db4a661a2c697a1a799c3848852250ddb451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-networking-for-hyper-v-vm-replication-tooa-secondary-vmm-site"></a>Etapa 3: Planejar a rede VM do Hyper-V replicação tooa secundário site do VMM

Depois de revisar os pré-requisitos de implantação, leia este tooplan artigo rede ao replicar máquinas de virtuais de Hyper-V (VMs) gerenciadas em nuvens do System Center Virtual Machine Manager (VMM), usando o site secundário tooa [doAzureSiteRecovery](site-recovery-overview.md) em Olá portal do Azure. 

Depois de ler este artigo, postar os comentários na parte inferior do hello, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="network-mapping-overview"></a>Visão geral de mapeamento de rede

Mapeamento de rede é usado ao replicar o datacenter secundário de tooa de VMs Hyper-V (gerenciados no VMM). O mapeamento de rede mapeia entre as redes de VM em um servidor VMM de origem e as redes do Azure de destino. Mapeamento Olá a seguir:

- **Conexão de rede**— conecta VMs tooappropriate redes após o failover. VM de réplica Olá será conectado toohello rede de destino que é a rede de origem mapeado toohello.
- **O posicionamento ideal**— ideal casas Olá máquinas virtuais de réplica nos servidores de host do Hyper-V. Máquinas virtuais de réplica são colocadas em hosts que podem Olá acesso redes VM mapeadas.
- **Nenhum mapeamento de rede**— se você não configurar o mapeamento de rede, máquinas virtuais de réplica não será conectada tooany redes VM após o failover.


### <a name="example"></a>Exemplo

Aqui está um exemplo tooillustrate esse mecanismo. Vamos usar uma organização com dois locais, Nova Iorque e Chicago.

**Localidade** | **Servidor VMM** | **Redes VM** | **Mapeado para**
---|---|---|---
Nova Iorque | VMM-NewYork| VMNetwork1-NewYork | TooVMNetwork1 mapeada-Chicago
 |  | VMNetwork2-NewYork | Não mapeado
Chicago | VMM-Chicago| VMNetwork1-Chicago | TooVMNetwork1-NewYork mapeada
 | | VMNetwork1-Chicago | Não mapeado

Neste exemplo:

- Quando uma máquina virtual de réplica é criada para qualquer máquina virtual que está conectada tooVMNetwork1-NewYork, ela será conectado tooVMNetwork1-Chicago.
- Quando uma máquina virtual de réplica é criada para VMNetwork2-NewYork ou VMNetwork2-Chicago, ele não será conectado tooany rede.

Aqui está como nuvens do VMM são configurados em nossa organização de exemplo e redes lógicas de saudação associados Olá nuvens.

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

Com base nessas configurações, quando você seleciona a rede VM de destino hello, Olá a tabela a seguir mostra opções Olá que estarão disponíveis.

**Seleção** | **Nuvem protegida** | **Protegendo a nuvem** | **Rede de destino disponível**
---|---|---|---
VMNetwork1-Chicago | SilverCloud1 | SilverCloud2 | Disponível
 | GoldCloud1 | GoldCloud2 | Disponível
VMNetwork2-Chicago | SilverCloud1 | SilverCloud2 | Não disponível
 | GoldCloud1 | GoldCloud2 | Disponível


Se a rede de destino Olá tem várias sub-redes e uma dessas sub-redes Olá mesmo nome como Olá sub-rede na qual Olá máquina virtual de origem está localizada, em seguida, Olá máquina virtual de réplica será conectada toothat sub-rede de destino após o failover. Se não houver nenhuma sub-rede de destino com um nome correspondente, Olá máquina de virtual será conectado toohello primeira sub-rede na rede de saudação.


#### <a name="failback-behavior"></a>Comportamento de failback

toosee o que acontece no caso de saudação de failback (replicação inversa), vamos supor que a VMNetwork1-NewYork é mapeado tooVMNetwork1-Chicago, com hello configurações a seguir.


**Máquina virtual** | **Rede tooVM conectado**
---|---
VM1 | VMNetwork1-Rede
VM2 (réplica de VM1) | VMNetwork1-Chicago

Com essas configurações, vamos analisar o que acontece em alguns cenários possíveis.

**Cenário** | **Resultado**
---|---
Nenhuma alteração nas propriedades de rede Olá de VM-2 após o failover. | VM-1 permanece conectado toohello rede de origem.
As propriedades de rede de VM-2 são alteradas após o failover e ela é desconectada. | A VM-1 é desconectada.
Propriedades de rede de VM-2 são alteradas depois do failover e é conectado tooVMNetwork2-Chicago. | Se a VMNetwork2-Chicago não estiver mapeada, a VM-1 será desconectada.
O mapeamento de rede da VMNetwork1-Chicago é alterado. | VM-1 será conectado toohello de rede mapeada agora tooVMNetwork1-Chicago.



## <a name="prepare-for-network-mapping"></a>Prepare-se para o mapeamento de rede

1. Nos servidores VMM de origem e destino da saudação, você deve ter uma rede lógica associada Olá nuvens de origem e destino. 
2. Em servidores de origem e destino hello, você deve ter uma rede lógica do VM rede toohello vinculado.
3. Máquinas virtuais em hosts Hyper-V no local de origem Olá devem ser vinculado toohello rede VM de origem. Se você estiver usando apenas um único servidor VMM, você pode configurar o mapeamento entre redes VM em Olá mesmo servidor.

Veja o que acontece quando você configura o mapeamento de rede durante a implantação do Site Recovery:

- Quando você configurar o mapeamento de rede e selecione uma rede VM de destino, nuvens de origem do VMM Olá que usam a rede VM de origem Olá serão exibidas, juntamente com redes VM de destino disponíveis Olá em nuvens de destino hello.
- - Quando o mapeamento for configurado corretamente e a replicação está habilitada, uma VM de origem será conectado tooits rede VM de origem e a réplica no local de destino hello será conectada tooits mapeado rede VM.
- Se a rede de destino Olá tem várias sub-redes e uma dessas sub-redes Olá mesmo nome como Olá sub-rede na qual Olá máquina virtual de origem está localizada, em seguida, Olá máquina virtual de réplica será conectada toothat sub-rede de destino após o failover. Se não houver nenhuma sub-rede de destino com um nome correspondente, Olá VM será conectado toohello primeira sub-rede na rede de saudação.

## <a name="connect-toovms-after-failover"></a>Conectar tooVMs após o failover

Ao planejar sua estratégia de failover e replicação, uma das perguntas mais importantes Olá é como tooconnect toohello réplica após o failover. Há duas opções: 

- **Use um endereço IP diferente**: você pode selecionar toouse um endereço IP diferente para Olá replicadas VM. No hello cenário VM obtém um novo endereço IP após o failover, e é necessária uma atualização DNS.
- **Reter Olá mesmo endereço IP**: talvez você queira toouse Olá mesmo endereço IP para a VM de réplica hello. Olá mantendo mesmos endereços IP simplifica recuperação hello, reduzindo problemas relacionados à rede após o failover. 

## <a name="retain-ip-addresses"></a>Reter os endereços IP

Se você quiser tooretain endereços IP de saudação do site primário do hello após o site secundário do toohello de failover, você pode fazer um failover de sub-rede completa e atualizar rotas tooindicate Olá novo local de endereços IP hello ou alternativa implantar uma sub-rede ampliada entre hello primário e Olá locais de recuperação.

### <a name="stretched-subnet"></a>Sub-rede ampliada

Em uma sub-rede ampliada, Olá sub-rede é disponível simultaneamente em ambos os locais primário e secundário de saudação. Se você mover um servidor e seu site secundário do toohello de configuração de IP (camada 3), rede Olá roteará novo local do hello tráfego toohello automaticamente. 

Do ponto de vista da Camada 2 (camada de link de dados), você precisa de equipamento de rede que possa gerenciar uma VLAN ampliada. Além disso, por Olá Alongar VLAN, domínio de falha potencial Olá estende tooboth sites, essencialmente se tornar um ponto único de falha. Embora isso seja improvável, pode ocorrer uma tempestade de transmissão que não poderá ser isolada. 


### <a name="subnet-failover"></a>Failover da sub-rede

Você pode executar uma saudação de tooobtain de failover de sub-rede benefícios da sub-rede Olá ampliada, sem realmente alongando-lo. Nesta solução, uma sub-rede estarão disponível no site de origem ou destino hello, mas não em ambos ao mesmo tempo. toomaintain Olá espaço de endereço IP no evento de saudação de um failover, você pode organizar programaticamente para Olá roteador infraestrutura toomove Olá subredes de tooanother de um site. Após quando ocorre o failover, sub-redes moveria com hello associados VMs. Olá principal desvantagem é na saudação de uma falha, você tem subrede inteira toomove hello.

### <a name="example"></a>Exemplo

Aqui está um exemplo de failover de sub-rede completo. site primário Olá tem aplicativos executados na sub-rede 192.168.1.0/24. No failover, Olá todas as máquinas virtuais nesta sub-rede falharem em um site secundário toohello e manter seus endereços IP. Rotas necessidade toobe modificado fatos de saudação tooreflect que todas as máquinas de virtuais VM Olá pertencentes toosubnet 192.168.1.0/24 agora moveu site secundário toohello.

Olá gráficos a seguir mostram as sub-redes de saudação antes e após o failover:

- Antes do failover, sub-rede 192.168.0.1/24 está ativo no site de origem hello, ficar ativo no site secundário Olá após o failover.
- Olá rotas entre o site primário e site de recuperação de site de terceiro e site primário e site de terceiro e o site de recuperação terá toobe modificado da maneira apropriada.

**Antes do failover**

![Antes do failover](./media/vmm-to-vmm-walkthrough-network/network-design2.png)

**Após o failover**

![Após o failover](./media/vmm-to-vmm-walkthrough-network/network-design3.png)

Após o failover, eis o que acontece:

- Recuperação de site alocará um endereço IP para cada interface de rede no hello VM, de saudação endereço IP estático na rede relevante hello, para cada instância do VMM.
- Se Olá pool de endereços IP no site secundário Olá é Olá mesmo que no site de origem hello, recuperação de Site aloca Olá mesmo IP endereço (de VM de origem Olá) toohello VM réplica. endereço IP de saudação é reservado no VMM, mas ele não está definido como o endereço IP de failover Olá no host do Hyper-V hello. endereço IP de failover de saudação em um host Hyper-v é definido apenas antes do failover de saudação.
- Se hello mesmo endereço IP não estiver disponível, o Site Recovery aloca outro endereço IP disponível do pool de saudação.
- Se as VMs usam DHCP, recuperação de Site não gerencia endereços IP de saudação. Você precisa toocheck que Olá DHCP server no site secundário Olá pode alocar o endereço da saudação mesmo intervalo como site de origem hello.

### <a name="validate-hello-ip-address"></a>Validar endereço IP Olá

Depois de habilitar a proteção para uma máquina virtual, você pode usar o seguinte exemplo script tooverify Olá endereço atribuído toohello VM. Olá mesmo endereço IP será definido como o endereço IP de failover hello e atribuído toohello VM em tempo de saudação de failover:

    ```
    $vm = Get-SCVirtualMachine -Name <VM_NAME>
    $na = $vm[0].VirtualNetworkAdapters>
    $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
    $ip.address 
    ```

## <a name="changing-ip-addresses"></a>Alterando endereços IP

Nesse cenário, os endereços IP de saudação de VMs que fazem failover são alterados. Olá desvantagem dessa solução é manutenção necessária-Olá. Normalmente, o DNS será atualizado após a inicialização das VMs de réplica. Entradas DNS podem precisar toobe alterado ou fluster na rede e atualizadas de entradas em cache. Isso pode resultar em tempo de inatividade. O tempo de inatividade pode ser atenuado da seguinte maneira:

- Use valores TTL baixos para aplicativos de intranet.
- Use Olá seguinte script em um plano de recuperação do Site Recovery, tooupdate Olá DNS server tooensure uma atualização em tempo hábil. Script hello não é necessário se você usar o registro DNS dinâmico.

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

Vamos examinar um cenário no qual você está planejando toouse diferentes endereços IP em Olá primário e os locais de recuperação de saudação. Neste exemplo, temos endereços IP diferentes em sites primários e secundários, e lá; o site de s uma terceira de quais aplicativos hospedados no site primário ou de recuperação de saudação pode ser acessado.

- Antes do failover, os aplicativos são 192.168.1.0/24 sub-rede hospedado no site primário Olá e são toobe configurado na sub-rede 172.16.1.0/24 no site secundário Olá após um failover.
- Rotas de rede/conexões de VPN foram configuradas corretamente para que todos os três sites possam acessar um ao outro.
- Após o failover, aplicativos serão restaurados na sub-rede de recuperação hello. Neste cenário há toofail sem necessidade por sub-rede inteira Olá, e nenhuma alteração necessária tooreconfigure VPN rotas de rede. saudação failover e algumas atualizações DNS, certifique-se de que os aplicativos permaneçam acessíveis.
- Se o DNS está configurado tooallow as atualizações dinâmicas, Olá VMs registrará por conta própria usando o novo endereço IP hello, quando eles são iniciados depois do failover.

**Antes do failover**

![IP diferente - antes do failover](./media/vmm-to-vmm-walkthrough-network/network-design10.png)

**Após o failover**

![IP diferente - após o failover](./media/vmm-to-vmm-walkthrough-network/network-design11.png)



## <a name="next-steps"></a>Próximas etapas

Vá muito[etapa 4: preparar VMM e Hyper-V](vmm-to-vmm-walkthrough-vmm-hyper-v.md).


