---
title: "modo de distribuição do balanceador de carga aaaConfigure | Microsoft Docs"
description: "Como tooconfigure Azure carregar afinidade IP de origem do balanceador distribuição modo toosupport"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: 7df27a4d-67a8-47d6-b73e-32c0c6206e6e
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: e745240b733ffc07928d8ed0ae097785ad4f412e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-distribution-mode-for-load-balancer"></a>Configurar o modo de distribuição Olá balanceador de carga

## <a name="hash-based-distribution-mode"></a>Modo de distribuição baseado em hash

algoritmo de distribuição de padrão de saudação é uma tupla 5 (fonte de IP, porta de origem, IP de destino, porta de destino, o tipo de protocolo) servidores de tooavailable toomap tráfego de hash. Ele fornece permanência somente dentro de uma sessão de transporte. Pacotes de saudação mesma sessão será direcionado toohello instância mesmo datacenter IP (DIP) por trás do ponto de extremidade de balanceamento de carga de saudação. Quando Olá cliente inicia uma nova sessão de Olá mesmo IP de origem, porta de origem Olá altera e faz com que o hello tráfego toogo tooa DIP ponto de extremidade diferente.

![balanceador de carga baseado em hash](./media/load-balancer-distribution-mode/load-balancer-distribution.png)

Figura 1 – Distribuição das 5 tuplas

## <a name="source-ip-affinity-mode"></a>Modo de afinidade de IP de origem

Temos outro modo de distribuição chamado Afinidade de IP de origem (também conhecido como afinidade de sessão ou afinidade de IP do cliente). O balanceador de carga do Azure pode ser configurado toouse uma tupla de 2 (IP de origem, IP de destino) ou (protocolo IP de origem, IP de destino) de tupla de 3 toomap tráfego toohello os servidores disponíveis. Usando a afinidade de IP de origem, conexões iniciadas da saudação mesmo computador cliente vai toohello mesmo ponto de extremidade DIP.

Olá diagrama a seguir ilustra uma configuração de 2 tuplas. Observe como tupla de 2 Olá Olá carga balanceador toovirtual máquina 1 (VM1) que é feita backup da VM2 e VM3 executa.

![afinidade de sessão](./media/load-balancer-distribution-mode/load-balancer-session-affinity.png)

Figura 2 – Distribuição das 2 tuplas

Afinidade IP de origem resolve uma incompatibilidade entre o Gateway de área de trabalho remota (RD) e Olá balanceador de carga do Azure. Agora é possível criar um farm de gateway de Área de Trabalho Remota em um único serviço de nuvem.

Outro cenário de caso de uso é o carregamento de mídia onde Olá carregamento de dados ocorre através de UDP, mas o plano de controle Olá é obtido por meio de TCP:

* Um cliente inicia uma sessão TCP endereço público com balanceamento de carga de toohello primeiro, obtém tooa direcionado DIP específico, esse canal é integridade de conexão Olá esquerdo toomonitor active
* Uma nova sessão UDP de saudação mesmo computador cliente é iniciado toohello ponto de extremidade público com balanceamento de carga de mesma, a expectativa de saudação aqui é que essa conexão também é direcionado toohello mesmo ponto de extremidade DIP como conexão de TCP anterior Olá para que o carregamento de mídia pode ser executado com alta taxa de transferência enquanto também mantém um canal de controle por meio de TCP.

> [!NOTE]
> Quando um conjunto de balanceamento de carga é alterado (remoção ou adição de uma máquina virtual), distribuição de saudação de solicitações de cliente é recalculada. Você não pode depender de novas conexões de clientes existentes que terminam em Olá mesmo servidor. Além disso, o uso do modo de distribuição de afinidade do IP de origem pode causar uma distribuição desigual de tráfego. Clientes que executam proxies subjacentes podem ser vistos como um aplicativo cliente exclusivo.

## <a name="configuring-source-ip-affinity-settings-for-load-balancer"></a>Definindo configurações de afinidade de IP de origem para o balanceador de carga

Para máquinas virtuais, você pode usar as configurações de tempo limite de toochange do PowerShell:

Adicionar uma máquina Virtual de tooa do ponto de extremidade do Azure e definir o modo de distribuição do balanceador de carga

```powershell
Get-AzureVM -ServiceName mySvc -Name MyVM1 | Add-AzureEndpoint -Name HttpIn -Protocol TCP -PublicPort 80 -LocalPort 8080 –LoadBalancerDistribution sourceIP | Update-AzureVM
```

LoadBalancerDistribution pode ser definido toosourceIP 2 tuplas (IP de origem, IP de destino) para balanceamento de carga, sourceIPProtocol para balanceamento de carga de tupla de 3 (protocolo IP de origem, IP de destino), ou nenhum se desejar que o comportamento padrão de saudação do balanceamento de carga de 5 tuplas.

Use Olá tooretrieve uma configuração de modo de distribuição do balanceador de carga do ponto de extremidade a seguir:

    PS C:\> Get-AzureVM –ServiceName MyService –Name MyVM | Get-AzureEndpoint

    VERBOSE: 6:43:50 PM - Completed Operation: Get Deployment
    LBSetName : MyLoadBalancedSet
    LocalPort : 80
    Name : HTTP
    Port : 80
    Protocol : tcp
    Vip : 65.52.xxx.xxx
    ProbePath :
    ProbePort : 80
    ProbeProtocol : tcp
    ProbeIntervalInSeconds : 15
    ProbeTimeoutInSeconds : 31
    EnableDirectServerReturn : False
    Acl : {}
    InternalLoadBalancerName :
    IdleTimeoutInMinutes : 15
    LoadBalancerDistribution : sourceIP

Se Olá LoadBalancerDistribution elemento não estiver presente balanceador de carga do Azure Olá usa o algoritmo de 5 tuplas saudação padrão.

### <a name="set-hello-distribution-mode-on-a-load-balanced-endpoint-set"></a>Definir o modo de distribuição de saudação em um conjunto de ponto de extremidade com balanceamento de carga

Se os pontos de extremidade são parte de um conjunto de ponto de extremidade com balanceamento de carga, o modo de distribuição Olá deve ser definido no conjunto de ponto de extremidade com balanceamento de carga hello:

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName MyService -LBSetName LBSet1 -Protocol TCP -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 –LoadBalancerDistribution sourceIP
```

### <a name="cloud-service-configuration-toochange-distribution-mode"></a>Modo de distribuição de toochange de configuração de serviço de nuvem

Você pode aproveitar hello Azure SDK para .NET 2.5 (toobe lançada em novembro) tooupdate seu serviço de nuvem. Configurações de ponto de extremidade para serviços de nuvem são feitas no. csdef de saudação. Em ordem tooupdate Olá carga balanceador modo de distribuição para uma implantação de serviços de nuvem, é necessária uma atualização de implantação.
Aqui está um exemplo de alterações .csdef para configurações do ponto de extremidade:

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" loadBalancerDistribution="sourceIP" />
    </Endpoints>
</WorkerRole>
<NetworkConfiguration>
    <VirtualNetworkSite name="VNet"/>
    <AddressAssignments>
<InstanceAddress roleName="VMRolePersisted">
    <PublicIPs>
    <PublicIP name="public-ip-name" idleTimeoutInMinutes="timeout-in-minutes"/>
    </PublicIPs>
</InstanceAddress>
    </AddressAssignments>
</NetworkConfiguration>
```

## <a name="api-example"></a>Exemplo de API

Você pode configurar a distribuição de Balanceador de carga hello usando a API de gerenciamento do serviço de saudação. Verifique se Olá de tooadd `x-ms-version` cabeçalho é definido tooversion `2014-09-01` ou superior.

### <a name="update-hello-configuration-of-hello-specified-load-balanced-set-in-a-deployment"></a>Atualizar o conjunto de configuração de saudação especificada com balanceamento de carga de saudação em uma implantação

#### <a name="request-example"></a>Exemplo de solicitação

    POST https://management.core.windows.net/<subscription-id>/services/hostedservices/<cloudservice-name>/deployments/<deployment-name>?comp=UpdateLbSet   x-ms-version: 2014-09-01
    Content-Type: application/xml

    <LoadBalancedEndpointList xmlns="http://schemas.microsoft.com/windowsazure" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
      <InputEndpoint>
        <LoadBalancedEndpointSetName> endpoint-set-name </LoadBalancedEndpointSetName>
        <LocalPort> local-port-number </LocalPort>
        <Port> external-port-number </Port>
        <LoadBalancerProbe>
          <Port> port-assigned-to-probe </Port>
          <Protocol> probe-protocol </Protocol>
          <IntervalInSeconds> interval-of-probe </IntervalInSeconds>
          <TimeoutInSeconds> timeout-for-probe </TimeoutInSeconds>
        </LoadBalancerProbe>
        <Protocol> endpoint-protocol </Protocol>
        <EnableDirectServerReturn> enable-direct-server-return </EnableDirectServerReturn>
        <IdleTimeoutInMinutes>idle-time-out</IdleTimeoutInMinutes>
        <LoadBalancerDistribution>sourceIP</LoadBalancerDistribution>
      </InputEndpoint>
    </LoadBalancedEndpointList>

valor de saudação do LoadBalancerDistribution pode ser sourceIP para afinidade de tupla de 2, sourceIPProtocol para afinidade de tupla de 3 ou none (nenhuma afinidade de. por exemplo, 5 tuplas)

#### <a name="response"></a>Response

    HTTP/1.1 202 Accepted
    Cache-Control: no-cache
    Content-Length: 0
    Server: 1.0.6198.146 (rd_rdfe_stable.141015-1306) Microsoft-HTTPAPI/2.0
    x-ms-servedbyregion: ussouth2
    x-ms-request-id: 9c7bda3e67c621a6b57096323069f7af
    Date: Thu, 16 Oct 2014 22:49:21 GMT

## <a name="next-steps"></a>Próximas etapas

[Visão geral do balanceador de carga interno](load-balancer-internal-overview.md)

[Introdução à configuração de um balanceador de carga para a Internet](load-balancer-get-started-internet-arm-ps.md)

[Definir configurações de tempo limite de TCP ocioso para o balanceador de carga](load-balancer-tcp-idle-timeout.md)
