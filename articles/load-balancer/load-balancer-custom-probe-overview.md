---
title: testes personalizadas do balanceador de aaaLoad e monitorar o status de integridade | Microsoft Docs
description: "Saiba como toouse personalizado sondas para instâncias do balanceador de carga do Azure toomonitor por trás do balanceador de carga"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 46b152c5-6a27-4bfc-bea3-05de9ce06a57
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 3dfcfcd2d5cffa58b160cb38d63acffbd997d452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-load-balancer-probes"></a>Entender as investigações do balanceador de carga

O balanceador de carga do Azure oferece integridade de saudação do hello recurso toomonitor das instâncias de servidor por meio de testes. Quando um teste falha toorespond, balanceador de carga para enviar a nova instância não íntegro toohello de conexões. as conexões existentes Olá não são afetadas e novas conexões são enviadas toohealthy instâncias.

Funções do serviço de nuvem (funções de trabalho e da Web) usam um agente convidado para o monitoramento de investigação. As investigações personalizadas de TCP ou HTTP devem ser configuradas quando você usa máquinas virtuais por trás de um Balanceador de Carga.

## <a name="understand-probe-count-and-timeout"></a>Noções básicas sobre contagem da investigação e tempo limite

O comportamento de investigação depende do seguinte:

* número de saudação de investigações bem-sucedida que permitem um toobe instância rotulada como.
* número de saudação de testes com falha que causam um toobe instância rotulada como desativado.

valor de tempo limite e a frequência de saudação definido em SuccessFailCount determinar se uma instância é confirmada toobe em execução ou não está em execução. No hello portal do Azure, tempo limite de saudação é definida tootwo vezes Olá valor de frequência de saudação.

configuração de teste de saudação de todas as instâncias do serviço de balanceamento de carga para um ponto de extremidade (ou seja, um conjunto com balanceamento de carga) deve ser Olá mesmo. Isso significa que você não pode ter uma configuração de teste diferentes para cada instância de função ou máquina virtual no hello mesmo hospedado serviço para uma combinação de ponto de extremidade específico. Por exemplo, cada instância deve ter portas locais e tempos limite idênticos.

> [!IMPORTANT]
> Uma investigação do balanceador de carga usa o endereço IP de saudação 168.63.129.16. Este endereço IP público facilita a recursos de plataforma de toointernal de comunicação para Olá colocar seu-proprietário-IP cenário de rede Virtual do Azure. endereço IP público 168.63.129.16 virtual Olá é usado em todas as regiões e não será alterado. Recomendamos que você permita esse endereço IP em todas as políticas de firewall local. Ele não deve ser considerado um risco de segurança porque uma mensagem desse endereço de origem pode apenas Olá interno plataforma Windows Azure. Se você não fizer isso, haverá um comportamento inesperado em uma variedade de cenários de como configurar Olá mesmo intervalo de endereços IP de 168.63.129.16 e ter duplicado endereços IP.

## <a name="learn-about-hello-types-of-probes"></a>Saiba mais sobre os tipos de saudação de testes

### <a name="guest-agent-probe"></a>Investigação do agente convidado

Essa investigação só está disponível para os Serviços de Nuvem do Azure. Balanceador de carga utiliza o agente de convidado Olá Olá máquina de virtual e, em seguida, escuta e responde com uma resposta HTTP 200 Okey somente quando hello instância está no estado pronto do hello (ou seja, não em outro estado como ocupado, Reciclando ou parando).

Para obter mais informações, consulte [Configurando Olá arquivo de definição serviço (csdef) para investigações de integridade](https://msdn.microsoft.com/library/azure/ee758710.aspx) ou [começar a criar um balanceador de carga para serviços de nuvem voltados para Internet](load-balancer-get-started-internet-classic-cloud.md#check-load-balancer-health-status-for-cloud-services).

### <a name="what-makes-a-guest-agent-probe-mark-an-instance-as-unhealthy"></a>O que faz uma investigação de agente convidado marcar uma instância como não íntegra?

Se o agente convidado Olá falhar toorespond com HTTP 200 Okey, marcas de Balanceador de carga Olá Olá instância como sem resposta e deixa de enviar a instância de toothat de tráfego. o balanceador de carga Olá continua a instância de saudação do tooping. Se o agente de convidado Olá responder com HTTP 200, o balanceador de carga Olá envia instância de toothat tráfego novamente.

Quando você usa uma função web, código de site Olá será executado normalmente em w3wp.exe, que não é monitorada por Olá malha do Azure ou o agente convidado. Isso significa que falhas no w3wp.exe (por exemplo, respostas HTTP 500) não será relatado toohello agente de convidado e o balanceador de carga Olá não terão essa instância fora de rotação.

### <a name="http-custom-probe"></a>Investigação personalizada do HTTP

investigação de Balanceador de carga de HTTP personalizada Olá substitui saudação padrão convidado investigação de agente, que significa que você pode criar seu próprios integridade do lógica personalizada toodetermine Olá Olá da instância de função. o balanceador de carga Olá sondas de seu ponto de extremidade a cada 15 segundos, por padrão. instância de saudação é considerada toobe na rotação do balanceador de carga Olá se ele responde com HTTP 200 dentro do período de tempo limite da saudação (31 segundos por padrão).

Isso pode ser útil se você quiser tooimplement instâncias de tooremove sua própria lógica de rotação do balanceador de carga. Por exemplo, você pode decidir tooremove uma instância se ele estiver acima de 90% de CPU e retorna um status de 200 não. Se você tiver funções da web que usam w3wp.exe, isso também significa você obter automática de monitoramento do seu site, porque falhas no código do site retornará uma sonda do balanceador de carga toohello status de 200 não.

> [!NOTE]
> investigação personalizada do Hello HTTP dá suporte a caminhos relativos e somente ao protocolo HTTP. Não há suporte para HTTPS.

### <a name="what-makes-an-http-custom-probe-mark-an-instance-as-unhealthy"></a>O que faz uma investigação personalizada HTTP marcar uma instância como não íntegra?

* Olá aplicativo HTTP retorna um código de resposta HTTP diferente de 200 (por exemplo, 403, 404 ou 500). Isso é uma confirmação positiva que Olá aplicativo instância deve ser retirada de serviço imediatamente.
* Olá HTTP servidor não responder em todos os após o período de tempo limite de saudação. Dependendo do valor de tempo limite de saudação é definido, isso pode significar que teste várias solicitações go sem resposta antes de investigação de saudação é marcada como não está em execução (ou seja, antes de SuccessFailCount testes são enviados).
* servidor de saudação fecha a conexão Olá por meio de uma redefinição TCP.

### <a name="tcp-custom-probe"></a>Investigação personalizada do TCP

Testes TCP iniciam uma conexão executando um handshake de três vias com a porta Olá definido.

### <a name="what-makes-a-tcp-custom-probe-mark-an-instance-as-unhealthy"></a>O que faz uma investigação personalizada TCP marcar uma instância como não íntegra?

* Olá TCP servidor não responder em todos os após o período de tempo limite de saudação. Quando o teste de saudação estiver marcado como não está em execução depende do número de saudação do teste com falha solicitações que foram configurado toogo sem resposta antes de marcar Olá investigação como não está em execução.
* investigação de saudação recebe um TCP redefinir Olá da instância de função.

Para saber mais sobre como configurar uma investigação de integridade HTTP ou uma investigação de TCP, confira [Introdução à criação de um balanceador de carga para a Internet no Resource Manager usando o PowerShell](load-balancer-get-started-internet-arm-ps.md).

## <a name="add-healthy-instances-back-into-load-balancer-rotation"></a>Adicionar instâncias íntegras de volta à rotação do balanceador de carga

Testes TCP e HTTP são considerados íntegros e marcar a instância de função hello como Íntegro quando:

* o balanceador de carga Olá obtém uma investigação positivo Olá primeiro tempo Olá que VM é inicializado.
* número Olá SuccessFailCount (descrito anteriormente) define o valor de saudação do bem-sucedida investigações que são necessário toomark instância de função hello como íntegro. Se uma instância de função foi removida, o número de Olá de investigações bem-sucedida, sucessivas deve igual a ou exceder o valor Olá SuccessFailCount toomark Olá da instância de função como em execução.

> [!NOTE]
> Se a integridade de saudação de uma instância de função está flutuando, balanceador de carga Olá aguarda mais tempo antes de colocar a instância de função hello novamente em estado íntegro hello. Isso é feito por meio de usuário de saudação tooprotect política e a infraestrutura de saudação.

## <a name="use-log-analytics-for-load-balancer"></a>Usar análise de log para o Balanceador de Carga

Você pode usar [de análise de log para o balanceador de carga](load-balancer-monitor-log.md) toocheck na contagem de status e a investigação de integridade de investigação do hello. Registro em log pode ser usado com as estatísticas de tooprovide Power BI ou o Azure Operational Insights sobre o status de integridade do balanceador de carga.
