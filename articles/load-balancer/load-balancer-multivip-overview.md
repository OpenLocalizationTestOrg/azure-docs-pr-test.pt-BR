---
title: aaaMultiple VIP de Balanceador de carga do Azure | Microsoft Docs
description: "Visão geral de Vários VIPs no Azure Load Balancer"
services: load-balancer
documentationcenter: na
author: chkuhtz
manager: narayan
editor: 
ms.assetid: 748e50cd-3087-4c2e-a9e1-ac0ecce4f869
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/11/2016
ms.author: chkuhtz
ms.openlocfilehash: e186e1248e7d187e7efd0668dc3244465ce3e156
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="multiple-vips-for-azure-load-balancer"></a>Múltiplos VIPs para o Azure Load Balancer

O balanceador de carga do Azure permite balancear os serviços tooload em várias portas, vários endereços IP ou ambos. Você pode usar fluxos de balanceamento de carga públicos e internos balanceador definições tooload em um conjunto de máquinas virtuais.

Este artigo descreve os conceitos básicos de saudação dessa capacidade, conceitos importantes e restrições. Se você pretender serviços tooexpose apenas um endereço IP, você pode encontrar instruções simplificadas para [pública](load-balancer-get-started-internet-portal.md) ou [interno](load-balancer-get-started-ilb-arm-portal.md) configurações de Balanceador de carga. Adicionar vários VIPs é a configuração de VIP único tooa incremental. Com os conceitos de saudação neste artigo, você pode expandir uma configuração simplificada a qualquer momento.

Quando você define um Azure Load Balancer, uma configuração front-end e back-end são conectadas às regras. Olá, referenciada pela regra de saudação de investigação de integridade é usado toodetermine como novos fluxos são enviados nó tooa no pool de back-end de saudação. Olá front-end é definido por um IP Virtual (VIP), que é uma tupla de 3 consiste de um endereço IP (público ou interno), um protocolo de transporte (UDP ou TCP) e um número de porta. Um DIP é que um endereço IP em uma NIC virtual do Azure anexados tooa VM no pool de back-end de saudação.

Olá, a tabela a seguir contém alguns exemplos de configurações de front-end:

| VIP | Endereço IP | protocol | porta |
| --- | --- | --- | --- |
| 1 |65.52.0.1 |TCP |80 |
| 2 |65.52.0.1 |TCP |*8080* |
| 3 |65.52.0.1 |*UDP* |80 |
| 4 |*65.52.0.2* |TCP |80 |

tabela de saudação mostra quatro front-ends diferentes. Os front-ends 1, 2 e 3 são um único VIP com várias regras. Olá mesmo endereço IP é usado, mas Olá porta ou protocolo é diferente para cada front-end. Front-ends #1 e &#4; são um exemplo de vários VIPs, onde hello mesma porta e protocolo de front-end são reutilizadas em vários VIPs.

O balanceador de carga do Azure fornece flexibilidade na definição de regras de balanceamento de carga de saudação. Uma regra declara como um endereço e porta de front-end Olá é mapeada toohello endereço de destino e a porta no hello back-end. Se as portas de back-end são reutilizadas em regras dependem Olá tipo de regra de saudação. Cada tipo de regra tem requisitos específicos que podem afetar a configuração do host o design da investigação. Há dois tipos de regras:

1. reutilização de regra padrão de saudação com nenhuma porta de back-end
2. regra de IP flutuante Olá em que as portas de back-end são reutilizadas

O balanceador de carga do Azure permite que você toomix os dois tipos de regra no Olá a mesma configuração de Balanceador de carga. Balanceador de carga Olá pode usá-los simultaneamente para uma determinada VM, ou qualquer combinação, desde que você concorde com restrições de saudação da regra de saudação. Que tipo de regra que você escolher depende de requisitos de saudação de seu aplicativo e Olá complexidade de dar suporte a essa configuração. Você deve avaliar quais tipos de regras são melhores para seu cenário.

Iniciando com o comportamento padrão de saudação, exploraremos esses cenários ainda mais.

## <a name="rule-type-1-no-backend-port-reuse"></a>Tipo de regra 1: nenhuma reutilização de porta de back-end

![Ilustração de vários VIPs](./media/load-balancer-multivip-overview/load-balancer-multivip.png)

Nesse cenário, front-end Olá VIPs são configurados da seguinte maneira:

| VIP | Endereço IP | protocol | porta |
| --- | --- | --- | --- |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) 1 |65.52.0.1 |TCP |80 |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) 2 |*65.52.0.2* |TCP |80 |

Olá DIP é destino Olá Olá fluxo de entrada. No pool de back-end hello, cada VM expõe serviço Olá desejado em uma porta exclusiva em um DIP. Esse serviço é associado a saudação front-end por meio de uma definição de regra.

Definimos duas regras:

| Regra | Mapear front-end | pool de toobackend |
| --- | --- | --- |
| 1 |![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) VIP1:80 |![back-end](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) DIP1:80, ![back-end](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) DIP2:80 |
| 2 |![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) VIP2:80 |![back-end](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) DIP1:81, ![back-end](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) DIP2:81 |

mapeamento completo de saudação no balanceador de carga do Azure agora é o seguinte:

| Regra | Endereço IP VIP | protocol | porta | Destino | porta |
| --- | --- | --- | --- | --- | --- |
| ![Regra](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) 1 |65.52.0.1 |TCP |80 |Endereço IP DIP |80 |
| ![Regra](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) 2 |65.52.0.2 |TCP |80 |Endereço IP DIP |81 |

Cada regra deve produzir um fluxo com uma combinação exclusiva de endereço IP de destino e porta de destino. Por porta de destino Olá variáveis de fluxo de saudação, várias regras podem fornecer fluxos toohello DIP mesmo em portas diferentes.

Investigações de integridade são sempre direcionado toohello DIP de uma VM. Você deve garantir que sua investigação reflete a integridade de saudação do hello VM.

## <a name="rule-type-2-backend-port-reuse-by-using-floating-ip"></a>Tipo de regra 2: reutilização de porta de back-end usando o IP Flutuante

O balanceador de carga do Azure fornece flexibilidade de Olá tooreuse porta de front-end de saudação entre vários VIPs independentemente do tipo de regra de saudação usado. Além disso, alguns cenários de aplicativo preferem ou exigem Olá mesmo toobe usado por várias instâncias do aplicativo em uma única VM no pool de back-end de saudação da porta. Exemplos comuns de reutilização de porta incluem clusters de alta disponibilidade, dispositivos virtuais de rede e exposição de vários pontos de extremidade TLS sem nova criptografia.

Se você quiser tooreuse porta de back-end de saudação em várias regras, você deve habilitar o IP flutuante na definição de regra de saudação.

IP Flutuante é uma parte do que é conhecido como DSR (retorno de servidor direto). O DSR é formado por duas partes: uma topologia de fluxo e um esquema de mapeamento de endereço IP. Em um nível de plataforma, o Azure Load Balancer sempre opera em uma topologia de fluxo de DSR, independentemente de o IP Flutuante estar habilitado ou não. Isso significa que parte de saída de saudação de um fluxo é sempre tooflow corretamente regravada toohello diretamente back origem.

Com o tipo de regra padrão hello, o Azure expõe uma esquema de mapeamento de endereço IP para facilitar o uso de balanceamento de carga tradicional. Habilitação de IP flutuante altera Olá tooallow de esquema de mapeamento de endereço IP para obter flexibilidade adicional como explicado abaixo.

Olá diagrama a seguir ilustra essa configuração:

![Ilustração de vários VIPs](./media/load-balancer-multivip-overview/load-balancer-multivip-dsr.png)

Para este cenário, todas as VMs no pool de back-end Olá tem três interfaces de rede:

* DIP: uma NIC Virtual associada Olá VM (configuração de IP do recurso NIC do Azure)
* VIP1: uma interface de loopback no sistema operacional convidado que está configurado com o endereço IP do VIP1
* VIP2: uma interface de loopback no sistema operacional convidado que está configurado com o endereço IP do VIP2

> [!IMPORTANT]
> configuração de saudação de interfaces lógicas Olá é executada no sistema operacional convidado de saudação. Essa configuração não é executada ou gerenciada pelo Azure. Sem essa configuração, as regras de saudação não funcionará. As definições de teste de integridade Olá DIP da saudação VM em vez de Olá VIP lógico. Portanto, seu serviço deve fornecer as respostas de teste em uma porta DIP que refletem o status de saudação do serviço de saudação oferecido no VIP lógico hello.

Vamos supor que Olá mesma configuração de front-end, como no cenário anterior hello:

| VIP | Endereço IP | protocol | porta |
| --- | --- | --- | --- |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) 1 |65.52.0.1 |TCP |80 |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) 2 |*65.52.0.2* |TCP |80 |

Definimos duas regras:

| Regra | Mapear front-end | pool de toobackend |
| --- | --- | --- |
| 1 |![Regra](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) VIP1:80 |![back-end](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) VIP1:80 (na VM1 e VM2) |
| 2 |![Regra](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) VIP2:80 |![back-end](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) VIP2:80 (na VM1 e VM2) |

Olá a tabela a seguir mostra o mapeamento de conclusão Olá no balanceador de carga de saudação:

| Regra | Endereço IP VIP | protocol | porta | Destino | porta |
| --- | --- | --- | --- | --- | --- |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) 1 |65.52.0.1 |TCP |80 |mesmo que o VIP (65.52.0.1) |mesmo que o VIP (80) |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) 2 |65.52.0.2 |TCP |80 |mesmo que o VIP (65.52.0.2) |mesmo que o VIP (80) |

destino de saudação do hello fluxo de entrada é o endereço de saudação VIP na interface de loopback Olá Olá VM. Cada regra deve produzir um fluxo com uma combinação exclusiva de endereço IP de destino e porta de destino. Por variados Olá endereço IP de destino do fluxo de saudação de reutilização de porta é possível em Olá mesma VM. O serviço é exposto toohello balanceador de carga vinculando-o endereço IP e a porta de interface de loopback do respectivos Olá toohello do VIP.

Observe que este exemplo não alterar a porta de destino hello. Embora esse seja um cenário de IP flutuante, balanceador de carga do Azure também oferece suporte a definição de uma porta de destino regra toorewrite Olá back-end e toomake-diferente da porta de destino do hello front-end.

Olá tipo de regra de IP flutuante é a base de saudação de vários padrões de configuração de Balanceador de carga. Um exemplo que está disponível no momento é hello [AlwaysOn do SQL com vários ouvintes](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md) configuração. Ao longo do tempo, documentaremos mais esses cenários.

## <a name="limitations"></a>Limitações

* Há suporte para várias configurações de VIP apenas com VMs de IaaS.
* Com a regra de IP flutuante hello, seu aplicativo deve usar Olá DIP para fluxos de saída. Se seu aplicativo associa toohello VIP endereço configurado na interface de loopback Olá no sistema operacional convidado de hello, em seguida, SNAT não é fluxo de saída de hello toorewrite disponíveis e fluxo Olá falha.
* Endereços IP públicos têm um efeito sobre a cobrança. Para saber mais, confira [Preços de endereço IP](https://azure.microsoft.com/pricing/details/ip-addresses/)
* Limites de assinatura são aplicados. Para saber mais, confira [Limites de serviço](../azure-subscription-service-limits.md#networking-limits) .
