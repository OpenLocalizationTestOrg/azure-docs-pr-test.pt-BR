---
title: aaaTroubleshoot balanceador de carga do Azure | Microsoft Docs
description: Solucionar problemas conhecidos com o Azure Load Balancer
services: load-balancer
documentationcenter: na
author: RamanDhillon
manager: timlt
editor: 
ms.assetid: 
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/10/2017
ms.author: kumud
ms.openlocfilehash: 56b73fcbf0bbf18cedfd113a280cfafa2a3dc9f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-load-balancer"></a>Solucionar problemas do Azure Load Balancer

Esta página fornece informações para solução de problemas comuns do Azure Load Balancer. Quando Olá conectividade do balanceador de carga não estiver disponível, os sintomas mais comuns de saudação são os seguintes: 
- Máquinas virtuais por trás do balanceador de carga não estão respondendo toohealth sondas de saudação 
- Máquinas virtuais atrás Olá balanceador de carga não estão respondendo toohello tráfego na porta Olá configurado

## <a name="symptom-vms-behind-hello-load-balancer-are-not-responding-toohealth-probes"></a>Sintoma: VMs por trás do balanceador de carga não estão respondendo toohealth sondas de saudação
Para tooparticipate de servidores de back-end de saudação no conjunto de Balanceador de carga hello, eles devem passar Olá investigação seleção. Para saber mais sobre investigações de integridade, confira [Noções básicas sobre investigações do Load Balancer](load-balancer-custom-probe-overview.md). 

pool de back-end de Balanceador de carga Olá VMs pode não estar respondendo toohello testes tooany vencimento de saudação motivos a seguir: 
- A VM do pool de back-end do Load Balancer não está em estado íntegro 
- VM não está escutando na porta de investigação de saudação pool de back-end do balanceador de carga 
- Firewall ou um grupo de segurança de rede está bloqueando a porta Olá Olá pool de back-end do balanceador de carga VMs 
- Outras configurações incorretas no Load Balancer

### <a name="cause-1-load-balancer-backend-pool-vm-is-unhealthy"></a>Causa 1: A VM do pool de back-end do Load Balancer não está em estado íntegro 

**Validação e resolução**

tooresolve esse problema, faça logon toohello participantes VMs e verifique se Olá estado da VM está íntegro e pode responder muito**PsPing** ou **TCPing** de outra VM no pool de saudação. Se Olá VM não está íntegro ou não é possível toorespond toohello investigação, você deve retificar o problema de saudação e obter Olá VM fazer tooa o estado íntegro antes de poder participar de balanceamento de carga.

### <a name="cause-2-load-balancer-backend-pool-vm-is-not-listening-on-hello-probe-port"></a>Causa 2: O pool de back-end do balanceador de carga VM não está escutando na porta de investigação de saudação
Se Olá VM está íntegro, mas não está respondendo a investigação de toohello, um motivo possível pode ser que a porta de investigação Olá não está aberta no hello participantes VM ou Olá VM não está escutando na porta.

**Validação e resolução**

1. Faça logon na máquina virtual de back-end toohello. 
2. Abra um prompt de comando e execute Olá toovalidate de comando, há um aplicativo de escuta na porta de investigação Olá a seguir:   
            netstat -an
3. Se o estado da porta Olá não está listado como **ESCUTA**, configurar a porta correta hello. 
4. Como alternativa, selecione outra porta, que esteja listada como **LISTENING**, e atualize adequadamente a configuração do Load Balancer.              

###<a name="cause-3-firewall-or-a-network-security-group-is-blocking-hello-port-on-hello-load-balancer-backend-pool-vms"></a>Causa 3: Firewall ou um grupo de segurança de rede está bloqueando o hello porta no pool de back-end de Balanceador de carga de saudação VMs  
Se o firewall Olá Olá que VM está bloqueando a porta de investigação hello, ou um ou mais grupos de segurança de rede configurados na sub-rede hello ou em uma saudação VM, não está permitindo que a porta de Olá Olá investigação tooreach, Olá VM é investigação de integridade toohello toorespond não é possível.          

**Validação e resolução**

* Se Olá firewall estiver habilitado, verifique se ele está configurado tooallow porta de investigação de saudação. Caso contrário, configure o tráfego de tooallow Olá firewall na porta de investigação de saudação e teste novamente. 
* Na lista de saudação de grupos de segurança de rede, verifique se o tráfego de entrada ou saída de saudação na porta de investigação de saudação tem interferência. 
* Além disso, verifique se um **Deny All** grupos de segurança de rede regra em Olá NIC de saudação VM ou Olá sub-rede que tem uma prioridade maior que a regra padrão de saudação que permite que os testes de balanceamento de carga & tráfego (grupos de segurança de rede devem permitir IP do balanceador de carga de 168.63.129.16). 
* Se qualquer uma dessas regras estão bloqueando o tráfego de investigação de hello, remova e reconfigure o tráfego de sondagem do hello regras tooallow hello.  
* Teste se Olá VM agora começou a responder sondas de integridade toohello. 

### <a name="cause-4-other-misconfigurations-in-load-balancer"></a>Causa 4: Outras configurações incorretas no Load Balancer
Se todos os Olá causas anteriores parecerem toobe validado e resolvidos corretamente e Olá VM ainda não responder toohello investigação de integridade, e manualmente testar a conectividade e coletar algumas conectividade de saudação rastreamentos toounderstand back-end.

**Validação e resolução**

* Use **Psping** uma saudação outras VMs em Olá resposta de porta de investigação de saudação do VNet tootest (exemplo:.\psping.exe -t 10.0.0.4:3389) e registre os resultados. 
* Use **TCPing** uma saudação outras VMs em Olá resposta de porta de investigação de saudação do VNet tootest (exemplo:.\tcping.exe 10.0.0.4 3389) e registre os resultados. 
* Se nenhuma resposta for recebida nesses testes de ping
    - Executar um simultâneas Netsh trace no pool de back-end de destino Olá VM e outra VM de teste de saudação mesmo VNet. Agora, executar um teste de PsPing por algum tempo, coletar alguns rastreamentos de rede e, em seguida, interromper o teste de saudação. 
    - Analisar a captura de rede hello e verificar se há uma consulta de ping de toohello relacionados ambos os pacotes de entrada e saída. 
        - Se não há pacotes de entrada são observados no pool de back-end Olá VM, há potencialmente a grupos de segurança de rede ou tráfego de bloqueio Olá UDR configuração incorreta. 
        - Se não há pacotes de saída é observado no pool de back-end Olá VM, Olá VM precisa toobe marcada para qualquer problema relacionado (para eample, porta de investigação Olá bloqueio de aplicativo). 
    - Verifique se os pacotes de teste de saudação estão sendo destino tooanother forçado (possivelmente por meio de configurações de UDR) antes de alcançar o balanceador de carga de saudação. Isso pode causar Olá tráfego toonever alcance Olá back-end VM. 
* Alterar tipo de investigação da saudação (por exemplo, HTTP tooTCP) e configure a porta correspondente Olá nos grupos de segurança de rede ACLs e firewall toovalidate se problema Olá com a configuração de saudação da resposta de investigação. Para saber mais sobre a configuração da investigação de integridade, confira [Endpoint Load Balancing health probe configuration](https://blogs.msdn.microsoft.com/mast/2016/01/26/endpoint-load-balancing-heath-probe-configuration-details/) (Configuração da investigação de integridade no balanceamento de carga do ponto de extremidade).

## <a name="symptom-vms-behind-load-balancer-are-not-responding-tootraffic-on-hello-configured-data-port"></a>Sintoma: As VMs por trás do balanceador de carga não estão respondendo tootraffic na porta de dados de saudação configurada

Se um pool de back-end VM está listado como íntegro e responde toohello investigações de integridade, mas ainda não está participando Olá balanceamento de carga ou não está respondendo toohello o tráfego de dados, pode ser devido a tooany de saudação motivos a seguir: 
* VM não está escutando na porta de dados de saudação do pool de back-end do balanceador de carga 
* Grupo de segurança de rede está bloqueando a porta Olá Olá pool de back-end do balanceador de carga VM  
* Acessando Olá Olá balanceador de carga de mesma VM e NIC 
* Acessando Olá Internet VIP do balanceador de carga de saudação participando do pool de back-end do balanceador de carga VM 

### <a name="cause-1-load-balancer-backend-pool-vm-is-not-listening-on-hello-data-port"></a>Causa 1: Pool de back-end do balanceador de carga VM não está escutando na porta de dados Olá 
Se uma VM não responder a tráfego de dados toohello, pode ser porque a porta de destino Olá não está aberta no hello participantes VM, ou, Olá VM não está escutando nessa porta. 

**Validação e resolução**

1. Faça logon na máquina virtual de back-end toohello. 
2. Abra um prompt de comando e execute Olá toovalidate de comando, há um aplicativo de escuta na porta de dados Olá a seguir:  
            netstat -an 
3. Se a porta Olá não está listada com o estado "Escutar", configure a porta de ouvinte adequado de saudação 
4. Se a porta hello está marcada como escutando, marque aplicativo de destino hello nessa porta de possíveis problemas. 

### <a name="cause-2-network-security-group-is-blocking-hello-port-on-hello-load-balancer-backend-pool-vm"></a>Causa 2: Grupo de segurança de rede está bloqueando a porta Olá Olá pool de back-end do balanceador de carga VM  

Se um ou mais grupos de segurança configurados na sub-rede hello ou em uma saudação VM de rede, está bloqueando Olá IP de origem ou a porta, VM hello é toorespond não é possível.

* Lista os grupos de segurança de rede Olá configurados no back-end Olá VM. Para obter mais informações, consulte:
    -  [Gerenciar grupos de segurança de rede usando Olá Portal](../virtual-network/virtual-network-manage-nsg-arm-portal.md)
    -  [Gerenciar grupos de segurança usando o PowerShell](../virtual-network/virtual-network-manage-nsg-arm-ps.md)
* Na lista de saudação de grupos de segurança de rede, verifique se:
    - tráfego de entrada ou saída Olá na porta de dados Olá tem interferência. 
    - um **Deny All** regra do grupo de segurança de rede em Olá NIC da sub-rede VM ou Olá Olá que tem uma prioridade mais alta regra saudação padrão que permite que o tráfego e investigações do balanceador de carga (grupos de segurança de rede devem permitir IP do balanceador de carga de 168.63.129.16, que é a porta de investigação) 
* Se qualquer uma das regras de saudação estão bloqueando o tráfego de hello, remova e reconfigure o tráfego de dados essas regras tooallow hello.  
* Teste se Olá VM agora começou investigações de integridade toohello toorespond.

### <a name="cause-3-accessing-hello-load-balancer-from-hello-same-vm-and-network-interface"></a>Causa 3: Acessando Olá balanceador de carga de saudação mesma interface de rede e máquinas virtuais 

Se seu aplicativo hospedado no back-end Olá VM de um balanceador de carga está tentando tooaccess outro aplicativo hospedado no hello mesmo back-end VM sobre Olá mesmo de Interface de rede, ele é um cenário sem suporte e falhará. 

**Resolução** pode resolver esse problema por meio de saudação métodos a seguir:
* Configure VMs de pool de back-end separadas por aplicativo. 
* Configure o aplicativo hello em VMs de NIC dupla para que cada aplicativo estava usando sua própria interface de rede e o endereço IP. 

### <a name="cause-4-accessing-hello-internal-load-balancer-vip-from-hello-participating-load-balancer-backend-pool-vm"></a>Causa 4: Acessando Olá VIP do balanceador de carga interno de saudação participando do pool de back-end do balanceador de carga VM

Se um VIP ILB está configurado dentro de uma rede virtual e um back-end de participante Olá VMs está tentando tooaccess Olá VIP do balanceador de carga interno, que resulta em falha. Esse é um cenário sem suporte.
**Resolução** avaliar Application Gateway ou outros toosupport de proxies (por exemplo, nginx ou haproxy) desse tipo de cenário. Para saber mais sobre o Gateway de Aplicativo, confira [Visão geral do Gateway de Aplicativo](../application-gateway/application-gateway-introduction.md)

## <a name="additional-network-captures"></a>Capturas de rede adicionais
Se você decidir tooopen um caso de suporte, colete Olá seguintes informações para uma resolução mais rápida. Escolha uma saudação de tooperform VM back-end único testes a seguir:
- Use o Psping uma saudação back-end VMs em Olá resposta de porta de investigação de saudação do VNet tootest (exemplo: psping 10.0.0.4:3389) e registre os resultados. 
- Use TCPing uma saudação back-end VMs em Olá resposta de porta de investigação de saudação do VNet tootest (exemplo: psping 10.0.0.4:3389) e registre os resultados.
- Se nenhuma resposta for recebida nesses testes de ping, executar um rastreamento Netsh simultâneo no back-end Olá VM e Olá redes VM de teste enquanto você execute PsPing e parar o rastreamento do Netsh hello. 
  
## <a name="next-steps"></a>Próximas etapas

Se hello etapas anteriores não resolverem o problema de saudação, abra um [tíquete de suporte](https://azure.microsoft.com/support/options/).

