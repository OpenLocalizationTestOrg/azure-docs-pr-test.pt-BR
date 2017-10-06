---
title: "conexões de saída aaaUnderstanding no Azure | Microsoft Docs"
description: "Este artigo explica como o Azure permite toocommunicate de VMs com os serviços de Internet públicos."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
ms.assetid: 5f666f2a-3a63-405a-abcd-b2e34d40e001
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 5/31/2017
ms.author: kumud
ms.openlocfilehash: ffe59971b934a16c9f6f78e3b15869a0072320d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-outbound-connections-in-azure"></a>Entendendo as conexões de saída no Azure

Uma VM (Máquina Virtual) no Azure pode se comunicar com pontos de extremidade fora do Azure no espaço de endereço IP público. Quando uma máquina virtual inicia um destino de tooa do fluxo de saída no espaço de endereço IP público, o Azure mapeia privada IP endereço tooa endereço IP público da saudação VM e permite saudação do tráfego de retorno tooreach VM.

Azure fornece três métodos diferentes de conectividade de saída tooachieve. Cada método tem seus próprios recursos e restrições. Revise cada método cuidadosamente toochoose que atenda às suas necessidades.

| Cenário | Método | Observação |
| --- | --- | --- |
| VM autônoma (nenhum balanceador de carga, nenhum endereço IP público em nível de instância) |SNAT padrão |O Azure associa um endereço IP público para o SNAT |
| VM com balanceamento de carga (nenhum endereço IP público em nível de instância na VM) |SNAT usando Olá balanceador de carga |O Azure usa um endereço IP público de saudação balanceador de carga para SNAT |
| VM com endereço IP público em nível de instância (com ou sem o balanceador de carga) |SNAT não é usado |O Azure usa Olá IP público atribuído toohello VM |

Se você não quiser toocommunicate uma VM com pontos de extremidade fora do Azure no espaço de endereço IP público, você pode usar o acesso de tooblock de grupos de segurança de rede (NSG). Usar NSGs é abordado em mais detalhes em [Impedindo a conectividade pública](#preventing-public-connectivity).

## <a name="standalone-vm-with-no-instance-level-public-ip-address"></a>VM autônoma sem endereço IP público em nível de instância

Nesse cenário, a saudação VM não é parte de um pool de Balanceador de carga do Azure e não tem um endereço de instância nível pública IP (ILPIP) atribuído tooit. Quando Olá VM cria um fluxo de saída, Azure converte o endereço IP de origem particular de Olá do endereço IP do hello fluxo de saída tooa fonte pública. endereço IP público Olá usado para este fluxo de saída não é configurável e não contam para o limite de recurso IP público da assinatura hello. O Azure usa a tradução de endereço de rede de origem (SNAT) tooperform essa função. Portas efêmeras do endereço IP público de saudação são toodistinguish usado fluxos individuais originados por Olá VM. O SNAT aloca dinamicamente portas efêmeras quando os fluxos são criados. Nesse contexto, Olá efêmera portas usadas para SNAT são chamados tooas SNAT.

As portas SNAT são um recurso finito que pode ser esgotado. É importante toounderstand como eles são consumidos. Uma porta SNAT é consumida por fluxo tooa único endereço IP. Para toohello de vários fluxos mesmo endereço IP de destino, cada fluxo consome uma única porta SNAT. Isto garante que Olá fluxos são exclusivo quando foi originado Olá mesmo toohello de endereço IP público mesmo endereço IP de destino. Vários fluxos, cada endereço IP de destino diferente tooa consumir uma única porta SNAT por destino. o endereço IP de destino Olá torna Olá fluxos exclusivo.

Você pode usar [análise de Log para o balanceador de carga](load-balancer-monitor-log.md) e [toomonitor de logs de eventos de alerta para mensagens de esgotamento de porta SNAT](load-balancer-monitor-log.md#alert-event-log). Quando os recursos da porta SNAT acabam, os fluxos de saída falham até as portas SNAT serem lançadas por fluxos existentes. O Balanceador de Carga usa um tempo limite de ociosidade de 4 minutos para recuperar portas SNAT.

## <a name="load-balanced-vm-with-no-instance-level-public-ip-address"></a>VM com balanceamento de carga com nenhum endereço IP público em nível de instância

Nesse cenário, a saudação VM é parte de um pool de Balanceador de carga do Azure.  Olá VM não tem um endereço IP público atribuído tooit. Olá recursos do balanceador de carga deve ser configurado com um regra toolink Olá pública IP front-end com o pool de back-end de saudação.  Se você não concluir essa configuração, o comportamento de saudação é conforme descrito na seção de saudação acima para [Standalone VM com nenhum IP público de nível de instância](load-balancer-outbound-connections.md#standalone-vm-with-no-instance-level-public-ip-address).

Quando hello VM com balanceamento de carga cria um fluxo de saída, Azure converte o endereço IP de origem particular de saudação do hello fluxo de saída toohello endereço IP público de saudação frontend de Balanceador de carga público. O Azure usa a tradução de endereço de rede de origem (SNAT) tooperform essa função. Portas efêmeras do endereço IP do balanceador de carga Olá são toodistinguish usado fluxos individuais originados por Olá VM. O SNAT aloca dinamicamente portas efêmeras quando os fluxos de saída são criados. Nesse contexto, Olá efêmera portas usadas para SNAT são chamados tooas SNAT.

As portas SNAT são um recurso finito que pode ser esgotado. É importante toounderstand como eles são consumidos. Uma porta SNAT é consumida por fluxo tooa único endereço IP. Para toohello de vários fluxos mesmo endereço IP de destino, cada fluxo consome uma única porta SNAT. Isto garante que Olá fluxos são exclusivo quando foi originado Olá mesmo toohello de endereço IP público mesmo endereço IP de destino. Vários fluxos, cada endereço IP de destino diferente tooa consumir uma única porta SNAT por destino. o endereço IP de destino Olá torna Olá fluxos exclusivo.

Você pode usar [análise de Log para o balanceador de carga](load-balancer-monitor-log.md) e [toomonitor de logs de eventos de alerta para mensagens de esgotamento de porta SNAT](load-balancer-monitor-log.md#alert-event-log). Quando os recursos da porta SNAT acabam, os fluxos de saída falham até as portas SNAT serem lançadas por fluxos existentes. O Balanceador de Carga usa um tempo limite de ociosidade de 4 minutos para recuperar portas SNAT.

## <a name="vm-with-an-instance-level-public-ip-address-with-or-without-load-balancer"></a>VM com endereço IP público em nível de instância (com ou sem o Balanceador de Carga)

Nesse cenário, Olá VM tem uma instância de nível pública IP (ILPIP) atribuído tooit. Não importa se Olá VM é ou não de balanceamento de carga. Quando é usado um ILPIP, o SNAT (Conversão do Endereço de Rede de Origem) não é usado. Olá VM usa Olá ILPIP para todos os fluxos de saída. Se seu aplicativo inicia muitos fluxos de saída e você enfrentar esgotamento SNAT, você deve considerar atribuindo um tooavoid ILPIP restrições SNAT.

## <a name="discovering-hello-public-ip-used-by-a-given-vm"></a>Descobrindo Olá IP público usado por uma determinada VM

Há muitas maneiras de endereço IP de origem pública toodetermine saudação de uma conexão de saída. OpenDNS fornece um serviço que pode mostrar Olá endereço IP público da VM. Usando o comando nslookup de saudação, você pode enviar uma consulta DNS para resolução do hello nome myip.opendns.com toohello OpenDNS. Olá serviço retornará o endereço IP de origem Olá que foi usado toosend consulta de saudação. Quando você executar Olá consulta a seguir de sua VM, a resposta de saudação é Olá que IP público usado para a VM.

    nslookup myip.opendns.com resolver1.opendns.com

## <a name="preventing-public-connectivity"></a>Impedindo a conectividade pública

Às vezes, não é recomendável para uma VM toobe permitido toocreate um fluxo de saída ou pode haver um toomanage requisito quais destinos podem ser alcançados com fluxos de saída. Nesse caso, você usa [grupos de segurança de rede (NSG)](../virtual-network/virtual-networks-nsg.md) toomanage Olá destinos que Olá VM pode atingir. Quando você aplica um NSG tooa com balanceamento de carga VM, você precisa toopay atenção toohello [padrão marcas](../virtual-network/virtual-networks-nsg.md#default-tags) e [padrão regras](../virtual-network/virtual-networks-nsg.md#default-rules).

Certifique-se de que Olá VM pode receber solicitações de investigação de integridade do balanceador de carga do Azure. Se um NSG blocos integridade solicitações de sondagem de saudação marca do AZURE_LOADBALANCER padrão, a investigação de integridade da VM falha e Olá VM está marcado como. Balanceador de carga para envio de novos fluxos toothat VM.

## <a name="limitations"></a>Limitações

Se [vários endereços IP (públicos) estão associados com um balanceador de carga](load-balancer-multivip-overview.md), qualquer desses endereços IP públicos são um candidato para fluxos de saída.

O Azure usa um algoritmo toodetermine Olá número de SNAT portas disponíveis com base no tamanho de saudação do pool de saudação.  Isso não é configurável no momento.

É importante toorememember que Olá o número de portas SNAT disponíveis não converte diretamente toonumber de conexões. Consulte acima para obter informações específicas sobre quando e como portas SNAT são alocadas e toomanage esse recurso exhaustible.
