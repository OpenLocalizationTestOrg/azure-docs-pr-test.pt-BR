---
title: tempo limite de ociosidade TCP de Balanceador de carga aaaConfigure | Microsoft Docs
description: Configurar tempo limite de ociosidade do TCP do balanceador de carga
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: 4625c6a8-5725-47ce-81db-4fa3bd055891
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 2bf0704b891f708e0a5bd7aa827441930f51cfaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-tcp-idle-timeout-settings-for-azure-load-balancer"></a>Definir as configurações de tempo limite de ociosidade do TCP para o Azure Load Balancer

Em sua configuração padrão, o Azure Load Balancer tem uma configuração de tempo limite de ociosidade de quatro minutos. Se um período de inatividade é maior que o valor de tempo limite de hello, não há nenhuma garantia de que Olá TCP ou sessão HTTP é mantido entre cliente hello e seu serviço de nuvem.

Quando a conexão de saudação for fechada, seu aplicativo cliente pode receber Olá a seguinte mensagem de erro: "hello subjacente a conexão foi fechada: uma conexão que deveria toobe mantida ativa foi fechada pelo servidor de saudação."

Uma prática comum é toouse um TCP keep-alive. Essa prática mantém a conexão Olá ativo por um período maior. Para obter mais informações, consulte estes [exemplos do .NET](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx). Com keep-alive habilitado, os pacotes são enviados durante períodos de inatividade da conexão hello. Esses pacotes keep-alive Certifique-se de que o valor de tempo limite de ociosidade Olá nunca é alcançado e conexão Olá é mantida por um longo período.

Essa configuração só funciona para conexões de entrada. tooavoid perder a conexão de hello, configure Olá TCP keep-alive com um intervalo menor do que Olá tempo limite de ociosidade configuração ou aumente Olá tempo limite de ociosidade valor. toosupport nesses cenários, adicionamos suporte para um tempo limite de ociosidade configurável. Agora você pode defini-lo por um período de 4 minutos too30.

O TCP keep alive funciona bem para cenários em que a vida útil da bateria não é uma restrição. Não é recomendável para aplicativos móveis. Usando um TCP keep-alive em um aplicativo móvel pode drenar bateria do dispositivo hello mais rapidamente.

![Tempo limite de TCP](./media/load-balancer-tcp-idle-timeout/image1.png)

Olá seções a seguir descreve como toochange ocioso configurações de tempo limite em máquinas virtuais e serviços de nuvem.

## <a name="configure-hello-tcp-timeout-for-your-instance-level-public-ip-too15-minutes"></a>Configurar o tempo limite TCP de saudação para seu minutos do nível de instância públicos IP too15

```powershell
Set-AzurePublicIP -PublicIPName webip -VM MyVM -IdleTimeoutInMinutes 15
```

`IdleTimeoutInMinutes` é opcional. Se não for definida, o tempo limite padrão de saudação é 4 minutos. intervalo de tempo limite aceitável de saudação é 4 too30 minutos.

## <a name="set-hello-idle-timeout-when-creating-an-azure-endpoint-on-a-virtual-machine"></a>Definir tempo limite de ociosidade Olá durante a criação de um ponto de extremidade do Azure em uma máquina virtual

toochange Olá tempo limite de configuração para um ponto de extremidade, use Olá seguinte:

```powershell
Get-AzureVM -ServiceName "mySvc" -Name "MyVM1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 8080 -IdleTimeoutInMinutes 15| Update-AzureVM
```

tooretrieve sua configuração de tempo limite de ociosidade, use Olá comando a seguir:

    PS C:\> Get-AzureVM -ServiceName "MyService" -Name "MyVM" | Get-AzureEndpoint
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

## <a name="set-hello-tcp-timeout-on-a-load-balanced-endpoint-set"></a>Definir tempo limite TCP de saudação em um conjunto de ponto de extremidade com balanceamento de carga

Se os pontos de extremidade são parte de um conjunto de ponto de extremidade com balanceamento de carga, tempo limite TCP de saudação deve ser definido no conjunto de ponto de extremidade com balanceamento de carga de saudação. Por exemplo:

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName "MyService" -LBSetName "LBSet1" -Protocol tcp -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 -IdleTimeoutInMinutes 15
```

## <a name="change-timeout-settings-for-cloud-services"></a>Alterar as configurações de tempo limite para serviços de nuvem

Você pode usar o hello Azure SDK tooupdate seu serviço de nuvem. Você pode fazer configurações de ponto de extremidade para serviços de nuvem no arquivo. csdef de saudação. Atualizar o tempo limite TCP de saudação para implantação de um serviço de nuvem requer uma atualização de implantação. Uma exceção é se o tempo limite TCP de saudação for especificado apenas para um IP público. Configurações de IP público estão no arquivo. cscfg de saudação e pode atualizá-los por meio de atualização e a atualização de implantação.

Olá. csdef alterações para as configurações de ponto de extremidade são:

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" idleTimeoutInMinutes="tcp-timeout" />
    </Endpoints>
</WorkerRole>
```

Olá. cscfg alterações de configuração de tempo limite de saudação em IPs públicos são:

```xml
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

## <a name="rest-api-example"></a>Exemplo de API REST

Você pode configurar o tempo limite de ociosidade TCP hello usando a API de gerenciamento do serviço de saudação. Certifique-se de que Olá `x-ms-version` cabeçalho é definido tooversion `2014-06-01` ou posterior. Configuração de saudação de atualização de saudação especificado pontos de extremidade de entrada com balanceamento de carga em todas as máquinas virtuais em uma implantação.

### <a name="request"></a>Solicitação

    POST https://management.core.windows.net/<subscription-id>/services/hostedservices/<cloudservice-name>/deployments/<deployment-name>

### <a name="response"></a>Response

```xml
<LoadBalancedEndpointList xmlns="http://schemas.microsoft.com/windowsazure" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
    <InputEndpoint>
    <LoadBalancedEndpointSetName>endpoint-set-name</LoadBalancedEndpointSetName>
    <LocalPort>local-port-number</LocalPort>
    <Port>external-port-number</Port>
    <LoadBalancerProbe>
        <Path>path-of-probe</Path>
        <Port>port-assigned-to-probe</Port>
        <Protocol>probe-protocol</Protocol>
        <IntervalInSeconds>interval-of-probe</IntervalInSeconds>
        <TimeoutInSeconds>timeout-for-probe</TimeoutInSeconds>
    </LoadBalancerProbe>
    <LoadBalancerName>name-of-internal-loadbalancer</LoadBalancerName>
    <Protocol>endpoint-protocol</Protocol>
    <IdleTimeoutInMinutes>15</IdleTimeoutInMinutes>
    <EnableDirectServerReturn>enable-direct-server-return</EnableDirectServerReturn>
    <EndpointACL>
        <Rules>
        <Rule>
            <Order>priority-of-the-rule</Order>
            <Action>permit-rule</Action>
            <RemoteSubnet>subnet-of-the-rule</RemoteSubnet>
            <Description>description-of-the-rule</Description>
        </Rule>
        </Rules>
    </EndpointACL>
    </InputEndpoint>
</LoadBalancedEndpointList>
```

## <a name="next-steps"></a>Próximas etapas

[Visão geral do balanceador de carga interno](load-balancer-internal-overview.md)

[Introdução à configuração de um balanceador de carga para a Internet](load-balancer-get-started-internet-arm-ps.md)

[Configurar um modo de distribuição do balanceador de carga](load-balancer-distribution-mode.md)
