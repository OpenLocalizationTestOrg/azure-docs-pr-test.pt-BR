---
title: failover de aaaTest (tooVMM VMM) no Azure Site Recovery | Microsoft Docs
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
ms.date: 06/05/2017
ms.author: pratshar
ms.openlocfilehash: 6b4f65ab692cbb0665102c4f51ea0694151cd3ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="test-failover-vmm-toovmm-in-site-recovery"></a>Testar o failover (tooVMM VMM) na recuperação de Site


Este artigo fornece informações e instruções sobre como fazer um failover de teste ou uma simulação de DR (recuperação de desastre) de VMs (máquinas virtuais) e servidores físicos protegidos com o Azure Site Recovery. Você usará um site gerenciado pelo System Center Virtual Machine Manager VMM locais como local de recuperação de saudação.

Executar um toovalidate de failover de teste sua estratégia de replicação ou executar uma análise de DR sem qualquer perda de dados ou o tempo de inatividade. Um failover de teste não tem nenhum impacto na replicação contínua hello ou em seu ambiente de produção. Execute-o em uma máquina virtual ou um [plano de recuperação](site-recovery-create-recovery-plans.md). Quando você estiver ativando um failover de teste, você precisa de rede de saudação toospecify Olá máquinas de virtuais de teste se conectar a. Você pode acompanhar o progresso de Olá Olá do failover de teste em Olá **trabalhos** página.  

Se você tiver comentários ou dúvidas, poste-as na parte inferior da saudação deste artigo ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prepare-hello-infrastructure-for-test-failover"></a>Preparar a infraestrutura de saudação para failover de teste
Se você quiser toorun um failover de teste usando uma rede existente, prepare o Active Directory, DHCP e DNS da rede.

Se você quiser toorun um failover de teste usando redes VM Olá opção toocreate automaticamente, adicione uma etapa manual antes de grupo-1 no plano de recuperação de saudação que vai toouse para failover de teste de saudação. Em seguida, adicione Olá toohello de recursos de infraestrutura criada automaticamente de rede antes de executar failover de teste de saudação.

### <a name="things-toonote"></a>Coisas toonote
Quando você estiver replicando tooa site secundário, de tipo de saudação da rede que Olá réplica máquina usa não precisa de um tipo de saudação toomatch da rede lógica usada para failover de teste, mas algumas combinações podem não funcionar. Se a réplica Olá usa DHCP e o isolamento de VLAN, a rede VM Olá para réplica Olá não precisa de um pool de endereços IP estáticos. Isso usando a virtualização de rede do Windows para o failover de teste Olá não funcionará porque não há pools de endereços estão disponíveis. 

Além disso, o failover de teste Olá não funcionará se a rede de réplica Olá usa sem isolamento e rede de teste Olá virtualização de rede do Windows. Isso ocorre porque a rede de não isolamento Olá não tem Olá sub-redes necessário toocreate uma rede de virtualização de rede do Windows.

Como máquinas virtuais de réplica são conectadas toomapped redes VM após o failover depende de como a rede VM de saudação é configurada no console do VMM hello.

#### <a name="vm-network-configured-with-no-isolation-or-vlan-isolation"></a>Rede VM configurada sem isolamento ou com isolamento de VLAN
Se DHCP estiver definido para a rede VM Olá, Olá máquina de virtual de réplica será conectada toohello ID de VLAN por meio das configurações de saudação que são especificados para o site de rede de saudação na rede lógica associada de saudação. máquina virtual de saudação receber o endereço IP do servidor DHCP disponível de saudação. 

Você não precisa toodefine um pool de endereços IP estáticos para a rede VM de destino hello. Se um pool de endereços IP estáticos é usado para a rede VM hello, Olá máquina de virtual de réplica é ID de VLAN de toohello conectado por meio das configurações de saudação que são especificados para o site de rede de saudação na rede lógica associada de saudação.

máquina virtual de saudação recebe seu endereço IP do pool de saudação que é definido para a rede VM de saudação de. Se um pool de endereços IP estáticos não está definido na rede VM de destino hello, a alocação de endereços IP falhará. Crie pool de endereços IP hello em ambos os servidores VMM com hello origem e de destino que você usará para proteção e recuperação.

#### <a name="vm-network-with-windows-network-virtualization"></a>Rede VM com Virtualização de Rede do Windows
Se uma rede VM é configurada com virtualização de rede do Windows, você deve definir um pool estático para a rede VM de destino hello, independentemente se a rede VM de origem Olá é configurado toouse DHCP ou um pool de endereços IP estáticos. 

Se você definir o DHCP, o servidor do VMM de destino Olá atua como um servidor DHCP e fornece um endereço IP do pool de saudação que é definido para a rede VM de destino de saudação. Se o uso de um pool de endereços IP estáticos é definido para o servidor de origem hello, o servidor do VMM de destino Olá aloca um endereço IP do pool de saudação. Em ambos os casos, a alocação de endereço IP falhará se um pool de endereços IP estáticos não for definido.


### <a name="prepare-dhcp"></a>Preparar o DHCP
Se as máquinas virtuais de saudação envolvidas no failover de teste usarem o DHCP, crie um servidor de teste DHCP na rede isolada de saudação para finalidade de saudação do failover de teste.

### <a name="prepare-active-directory"></a>Preparar o Active Directory
toorun um failover de teste para testes de aplicativos, você precisa de uma cópia do ambiente do Active Directory de produção de hello em seu ambiente de teste. Para obter mais informações, examine Olá [teste considerações de failover para o Active Directory](site-recovery-active-directory.md#test-failover-considerations).

### <a name="prepare-dns"></a>Preparar o DNS
Prepare um servidor DNS para failover de teste de saudação da seguinte maneira:

* **DHCP**: se as máquinas virtuais usar DHCP, endereço IP de saudação do teste Olá DNS deve ser atualizado no servidor de teste DHCP hello. Se você estiver usando um tipo de rede de virtualização de rede do Windows, o servidor do VMM Olá atua como servidor DHCP de saudação. Portanto, o endereço IP de saudação do DNS deve ser atualizado na rede de failover de teste de saudação. Nesse caso, máquinas virtuais de saudação se registram toohello relevante no servidor DNS.
* **Endereço estático**: se as máquinas virtuais usam um endereço IP estático, Olá endereço IP do servidor DNS deve ser atualizado no failover de teste de rede de teste de saudação. Talvez seja necessário tooupdate DNS com endereço IP Olá Olá máquinas de virtuais de teste. Você pode usar o hello script de exemplo a seguir para essa finalidade:

        Param(
        [string]$Zone,
        [string]$name,
        [string]$IP
        )
        $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
        $newrecord = $record.clone()
        $newrecord.RecordData[0].IPv4Address  =  $IP
        Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord



## <a name="run-a-test-failover"></a>Execute um teste de failover
Este procedimento descreve como toorun um failover de teste para a recuperação de um plano. Como alternativa, você pode executar o failover Olá para uma única máquina virtual em Olá **máquinas virtuais** guia.

![Folha Failover de teste](./media/site-recovery-test-failover-vmm-to-vmm/TestFailover.png)

1. Selecione **Planos de Recuperação** > *recoveryplan_name*. Clique em **Failover** > **Test Failover**.
1. Em Olá **Failover de teste** folha, especifique como máquinas virtuais devem ser conectados toonetworks após o failover de teste de saudação. Para obter mais informações, consulte Olá [opções de rede](#network-options-in-site-recovery).
1. Controlar o progresso de failover Olá **trabalhos** guia.
1. Após o failover estiver concluído, verifique se que máquinas virtuais de saudação iniciado com êxito.
1. Quando terminar, clique em **failover de teste de limpeza** no plano de recuperação de saudação. Em **notas**, gravar e salvar todas as observações associadas Olá failover de teste. Esta etapa exclui Olá virtual máquinas e redes que foram criadas durante o failover de teste.


## <a name="network-options-in-site-recovery"></a>Opções de rede na recuperação de site

Quando você executa um failover de teste, você será solicitado a tooselect as configurações de rede para máquinas de réplica de teste. Você tem várias opções.  

| **Opção de failover de teste** | **Descrição** | **Verificação do failover** | **Detalhes** |
| --- | --- | --- | --- |
| **O failover de local VMM secundário tooa – sem rede** |Não selecione uma rede VM. |O failover verifica se os computadores de teste são criados.<br/><br/>Olá máquina de virtual de teste é criada no host Olá onde Olá máquina de virtual de réplica existe. Nuvem toohello onde se encontra Olá máquina de virtual de réplica não será adicionada. |<p>máquina de failover de saudação não está conectado tooany rede.<br/><br/>máquina Olá pode ser conectado tooa rede VM após ele ter sido criado. |
| **O failover de local VMM secundário tooa – com a rede** |Selecione uma rede VM existente. |O failover verifica se as máquinas virtuais foram criadas. |Olá máquina de virtual de teste é criada no host Olá onde Olá máquina de virtual de réplica existe. Nuvem toohello onde se encontra Olá máquina de virtual de réplica não será adicionada.<br/><br/>Crie uma rede VM isolada da rede de produção.<br/><br/>Se você estiver usando uma rede baseada em VLAN, recomendamos criar uma rede lógica separada (não usada em produção) no VMM para essa finalidade. Esta rede lógica é usada toocreate redes VM para failovers de teste.<br/><br/>rede lógica Olá deve ser associado a pelo menos um dos adaptadores de rede de saudação de todos os servidores do Hyper-V Olá que estão hospedando as máquinas virtuais.<br/><br/>Para redes lógicas de VLAN, Olá sites de rede que você adicione a rede lógica toohello deve ser isolado.<br/><br/>Se você está estiver usando uma rede lógica baseada na Virtualização de Rede do Windows, o Azure Site Recovery criará automaticamente redes de VM isoladas. |
| **Falha ao longo do site secundário de VMM tooa - criar uma rede** |Uma rede de teste temporária é criada automaticamente com base na configuração de saudação que você especificar na **rede lógica** e seus sites de rede relacionados. |O failover verifica se as máquinas virtuais foram criadas. |Use esta opção se o plano de recuperação de saudação usa mais de uma rede VM. Se você estiver usando redes de virtualização de rede do Windows, essa opção pode criar automaticamente redes VM com hello mesmas configurações (sub-redes e pools de endereços IP) na rede de saudação do hello máquina de virtual de réplica. Essas redes de VM são limpos automaticamente após a conclusão do failover de teste de saudação.</p><p>Olá máquina de virtual de teste é criada no host Olá onde Olá máquina de virtual de réplica existe. Nuvem toohello onde se encontra Olá máquina de virtual de réplica não será adicionada. |

> [!TIP]
> Olá, endereço IP fornecido a máquina virtual de tooa durante o failover de teste é Olá deve receber o mesmo endereço IP que Olá a máquina virtual para um failover planejado ou não planejado (presumindo que o endereço IP de saudação está disponível na rede de failover de teste de saudação). Se hello mesmo endereço IP não está disponível na rede de failover de teste Olá, Olá VM recebe outro endereço IP que está disponível na rede de failover de teste de saudação.
>
>


## <a name="test-failover-tooa-production-network-on-a-recovery-site"></a>Rede de produção de tooa de failover de teste em um site de recuperação
Recomendamos que, ao fazer um failover de teste, você escolha uma rede diferente da rede do site de recuperação de produção fornecida no [mapeamento de rede](https://docs.microsoft.com/azure/site-recovery/site-recovery-network-mapping). Mas se você realmente deseja toovalidate conectividade de rede de ponta a ponta em uma máquina virtual de failover, observe Olá pontos a seguir:

* Verifique se a que máquina virtual primária Olá é desligada quando você está fazendo o failover de teste de saudação. Se você não fizer isso, duas máquinas virtuais com hello mesma identidade estará sendo executada em Olá mesmo de rede em Olá mesmo tempo. Essa situação pode levar tooundesired consequências.
* As alterações feitas toohello máquinas virtuais de failover de teste são perdidas quando você limpar Olá máquinas virtuais de teste. Essas alterações não são replicadas toohello back máquina de virtual primária.
* Essa maneira de realizar testes leva toodowntime para seu aplicativo de produção. Peça aos usuários do aplicativo hello não toouse aplicativo hello quando Olá DR drill está em andamento.  


## <a name="next-steps"></a>Próximas etapas
Depois de executar um failover de teste com êxito, você pode tentar um [failover](site-recovery-failover.md).
