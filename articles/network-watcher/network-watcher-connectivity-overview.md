---
title: "seleção de tooconnectivity aaaIntroduction no Inspetor de rede do Azure | Microsoft Docs"
description: "Esta página fornece uma visão geral da saudação capacidade de conectividade do observador de rede"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/11/2017
ms.author: gwallace
ms.openlocfilehash: 52fc4547f167cea2992a046859dc0550d136e80d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooconnectivity-check-in-azure-network-watcher"></a>Introdução tooconnectivity seleção no Inspetor de rede do Azure

Olá recurso de conectividade do observador de rede fornece Olá recurso toocheck uma conexão TCP direta de uma máquina virtual tooa máquina virtual (VM), o nome de domínio totalmente qualificado (FQDN), URI, ou o endereço IPv4. Os cenários de rede são complexos, são implementados usando Grupos de Segurança de Rede, firewalls, rotas definidas pelo usuário e recursos fornecidos pelo Azure. Configurações complexas tornam a solução de problemas de conectividade desafiadora. Observador de rede ajuda a reduzir Olá toofind tempo e detectar problemas de conectividade. resultados de saudação retornados podem fornecer informações sobre se um problema de conectividade é devido a plataforma de tooa ou um problema de configuração do usuário. A conectividade pode ser verificada com o [PowerShell](network-watcher-connectivity-powershell.md), a [CLI do Azure](network-watcher-connectivity-cli.md) e a [API REST](network-watcher-connectivity-rest.md).

> [!IMPORTANT]
> A verificação de conectividade requer uma extensão de máquina virtual `AzureNetworkWatcherExtension`. Para instalar a extensão de saudação em uma VM do Windows, visite [extensão de máquina virtual do agente do Inspetor de rede do Azure para Windows](../virtual-machines/windows/extensions-nwa.md) e para a visita de VM do Linux [extensão de máquina virtual do agente do Inspetor de rede do Azure para Linux](../virtual-machines/linux/extensions-nwa.md).

## <a name="response"></a>Resposta

Olá, a tabela a seguir mostra as propriedades de saudação retornadas quando uma verificação de conectividade concluiu a execução.

|Propriedade  |Descrição  |
|---------|---------|
|ConnectionStatus     | status de saudação de verificação de conectividade de saudação. Os resultados possíveis são **Acessível** e **Inacessível**.        |
|AvgLatencyInMs     | Latência média durante a verificação de conectividade de saudação em milissegundos. (Exibido somente se a verificação de status estiver acessível)        |
|MinLatencyInMs     | Verificação de latência mínima durante a conectividade de saudação em milissegundos. (Exibido somente se a verificação de status estiver acessível)        |
|MaxLatencyInMs     | Latência máxima durante conectividade Olá verificação em milissegundos. (Exibido somente se a verificação de status estiver acessível)        |
|ProbesSent     | Número de investigações enviada durante a verificação de saudação. O valor máximo é de 100.        |
|ProbesFailed     | Número de testes que falharam durante a verificação de saudação. O valor máximo é de 100.        |
|Hops     | Salto pelo caminho de nó de origem toodestination.        |
|Hops[].Type     | Tipo de recurso. Os valores possíveis são **Source**, **VirtualAppliance**, **VnetLocal** e **Internet**.        |
|Hops[].Id | Identificador exclusivo do nó de saudação.|
|Hops[].Address | Endereço IP de salto hello.|
|Hops[].ResourceId | ResourceID do salto Olá se salto Olá é um recurso do Azure. Se for um recurso de Internet, ResourceID será **Internet**. |
|Hops[].NextHopIds | Identificador exclusivo de saudação do próximo salto de saudação tomado.|
|Hops[].Issues | Uma coleção dos problemas encontrados durante a verificação de saudação a esse salto. Se não houver nenhum problema, o valor de saudação é em branco.|
|Hops[].Issues[].Origin | No nó de atual de hello, onde o problema ocorreu. Os valores possíveis são:<br/> **Entrada** -se no link de saudação do atual-salto anterior toohello de salto Olá<br/>**Saída** -se no link de saudação do next-hop atual toohello de salto Olá<br/>**Local** -problema é salto atual hello.|
|Hops[].Issues[].Severity | severidade Olá Olá problema detectado. Os valores possíveis são **Erro** e **Aviso**. |
|Hops[].Issues[].Type |tipo de saudação do problema encontrado. Os valores possíveis são: <br/>**CPU**<br/>**Memória**<br/>**GuestFirewall**<br/>**DnsResolution**<br/>**NetworkSecurityRule**<br/>**UserDefinedRoute** |
|Hops[].Issues[].Context |Detalhes sobre o problema de saudação encontrado.|
|Hops[].Issues[].Context[].key |Chave do par chave-valor de saudação retornado.|
|Hops[].Issues[].Context[].value |O valor do par chave-valor de saudação retornado.|

a seguir Olá é um exemplo de um problema encontrado em um nó.

```json
"Issues": [
    {
        "Origin": "Outbound",
        "Severity": "Error",
        "Type": "NetworkSecurityRule",
        "Context": [
            {
                "key": "RuleName",
                "value": "UserRule_Port80"
            }
        ]
    }
]
```
## <a name="fault-types"></a>Tipos de Falha

verificação de conectividade Olá retorna tipos de falhas sobre conexão hello. Olá tabela a seguir fornece uma lista de tipos de falhas atual hello retornadas.

|Tipo  |Descrição  |
|---------|---------|
|CPU     | Alta utilização da CPU.       |
|Memória     | Alta utilização de memória.       |
|GuestFirewall     | O tráfego é bloqueado devido a configuração de firewall tooa máquina virtual.        |
|DNSResolution     | Falha na resolução DNS para o endereço de destino hello.        |
|NetworkSecurityRule    | O tráfego é bloqueado por uma Regra NSG (a Regra é retornada)        |
|UserDefinedRoute|O tráfego é descartado devido definida pelo usuário de tooa ou rota do sistema. |

### <a name="next-steps"></a>Próximas etapas

Saiba como recursos de tooa tooverify conectividade visitando: [Verifique a conectividade com o observador de rede do Azure](network-watcher-connectivity-powershell.md).

<!--Image references-->
[1]: ./media/network-watcher-next-hop-overview/figure1.png

