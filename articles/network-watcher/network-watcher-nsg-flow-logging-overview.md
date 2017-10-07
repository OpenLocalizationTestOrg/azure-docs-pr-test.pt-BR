---
title: "log de tooflow aaaIntroduction para grupos de segurança de rede com o observador de rede do Azure | Microsoft Docs"
description: "Esta página explica como o fluxo NSG toouse registra um recurso do observador de rede do Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 47d91341-16f1-45ac-85a5-e5a640f5d59e
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: da85e946147b14717144cb47d1c742057c6dfa24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooflow-logging-for-network-security-groups"></a>Registro em log tooflow de Introdução para grupos de segurança de rede

Logs de fluxo de grupo de segurança de rede são um recurso do observador de rede que permite que você tooview informações sobre o tráfego IP de entrada e saída por meio de um grupo de segurança de rede. Esses logs de fluxo são gravados no formato json e mostram saídas fluxos de entrada em uma base por regra, Olá fluxo de saudação do NIC se aplica, 5-tupla informações sobre o fluxo de saudação (protocolo IP de origem/destino, porta de origem/destino) e se hello tráfego foi permitido ou negado.

![visão geral dos logs de fluxo][1]

Enquanto o fluxo de logs de grupos de segurança de rede de destino, elas não são exibidas Olá mesmo como Olá outros logs. Logs de fluxo são armazenados apenas dentro de uma conta de armazenamento e o seguinte caminho de log Olá conforme mostrado no exemplo a seguir de saudação:

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

Olá mesmas políticas de retenção como visto em outros logs aplicam logs de tooflow. Logs de tem uma política de retenção pode ser definida de dias de too365 de 1 dia. Se uma política de retenção não for definida, Olá logs são mantidos indefinidamente.

## <a name="log-file"></a>Arquivo de log

Os logs de fluxo têm várias propriedades. Olá lista a seguir é uma lista de propriedades de saudação que são retornados dentro do log de fluxo NSG hello:

* **tempo** - hora em que o evento Olá foi registrado
* **systemId** - a ID do recurso Grupo de Segurança da Rede.
* **categoria** -categoria de saudação do evento Olá, é sempre ser NetworkSecurityGroupFlowEvent
* **ResourceID** -Olá Id de saudação NSG recurso
* **operationName** - é sempre NetworkSecurityGroupFlowEvents
* **propriedades** -uma coleção de propriedades de fluxo de saudação
    * **Versão** -número de versão do esquema de evento do fluxo de Log Olá
    * **flows** - uma coleção de fluxos. Essa propriedade tem várias entradas para diferentes regras
        * **regra** -regra para qual Olá fluxos são listados
            * **flows** - uma coleção de fluxos
                * **Mac** -Olá endereço MAC de hello NIC para Olá VM em que o fluxo de saudação foi coletado
                * **flowTuples** -uma cadeia de caracteres que contém várias propriedades de tupla de fluxo de saudação em formato separado por vírgulas
                    * **Carimbo de hora** -este valor é o carimbo de hora de saudação do quando fluxo Olá ocorreu no formato de ÉPOCA do UNIX
                    * **IP de origem** - Olá IP de origem
                    * **Destino IP** -Olá IP de destino
                    * **Porta de origem** - Olá porta de origem
                    * **Porta de destino** -Olá porta de destino
                    * **Protocolo** -Olá protocolo de fluxo de saudação. Os valores válidos são **T** para TCP e **U** para UDP
                    * **Fluxo de tráfego** -Olá a direção do fluxo de tráfego de saudação. Os valores válidos são **I** para entrada e **O** para saída.
                    * **Traffic** - se o tráfego foi permitido ou negado. Os valores válidos são **A** para permitido e **D** para negado.


a seguir Olá é um exemplo de um fluxo de log. Como você pode ver, há vários registros que siga a lista de propriedades de saudação descrita em Olá anterior seção. 

> [!NOTE]
> Os valores na propriedade de flowTuples Olá são uma lista separada por vírgulas.
 
```json
{
    "records": 
    [
        
        {
             "time": "2017-02-16T22:00:32.8950000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282421,42.119.146.95,10.1.0.4,51529,5358,T,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282370,163.28.66.17,10.1.0.4,61771,3389,T,I,A","1487282393,5.39.218.34,10.1.0.4,58596,3389,T,I,A","1487282393,91.224.160.154,10.1.0.4,61540,3389,T,I,A","1487282423,13.76.89.229,10.1.0.4,53163,3389,T,I,A"]}]}]}
        }
        ,
        {
             "time": "2017-02-16T22:01:32.8960000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282481,195.78.210.194,10.1.0.4,53,1732,U,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282435,61.129.251.68,10.1.0.4,57776,3389,T,I,A","1487282454,84.25.174.170,10.1.0.4,59085,3389,T,I,A","1487282477,77.68.9.50,10.1.0.4,65078,3389,T,I,A"]}]}]}
        }
        ,
        {
             "time": "2017-02-16T22:02:32.9040000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282492,175.182.69.29,10.1.0.4,28918,5358,T,I,D","1487282505,71.6.216.55,10.1.0.4,8080,8080,T,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282512,91.224.160.154,10.1.0.4,59046,3389,T,I,A"]}]}]}
        }
        ,
        ...
```

## <a name="next-steps"></a>Próximas etapas

Saiba como tooenable fluxo registra visitando [log habilitando fluxo](network-watcher-nsg-flow-logging-portal.md).

Saiba mais sobre o log de NSG visitando [Log Analytics para os grupos de segurança da rede (NSGs)](../virtual-network/virtual-network-nsg-manage-log.md).

Descubra se o tráfego é permitido ou negado em uma VM visitando [Examinar o tráfego com a verificação de fluxo de IP](network-watcher-check-ip-flow-verify-portal.md)

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-overview/figure1.png

