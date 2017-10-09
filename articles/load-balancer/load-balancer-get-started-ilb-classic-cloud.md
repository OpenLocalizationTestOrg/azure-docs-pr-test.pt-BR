---
title: "aaaCreate um balanceador de carga interno para serviços de nuvem do Azure | Microsoft Docs"
description: "Saiba como o toocreate um interno balanceador usando o PowerShell no modelo de implantação clássico Olá de carga"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 57966056-0f46-4f95-a295-483ca1ad135d
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: fe7975bca7bec3248626b0ad0fad6823e278ade2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-for-cloud-services"></a>Introdução à criação de um balanceador de carga interno (clássico) para os serviços de nuvem

> [!div class="op_single_selector"]
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [CLI do Azure](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [Serviços de nuvem](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

> [!IMPORTANT]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../azure-resource-manager/resource-manager-deployment-model.md).  Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação. Saiba como muito[executar essas etapas usando o modelo do Gerenciador de recursos de saudação](load-balancer-get-started-ilb-arm-ps.md).

## <a name="configure-internal-load-balancer-for-cloud-services"></a>Configurar o balanceador de carga interno para os serviços de nuvem

Há suporte para o balanceador de carga interno tanto para máquinas virtuais quanto para serviços de nuvem. Um ponto de extremidade de Balanceador de carga interno criado em um serviço de nuvem que está fora de uma rede virtual regional estarão acessível apenas dentro de serviço de nuvem hello.

configuração de Balanceador de carga interno Olá tem toobe definido durante a criação de saudação de primeira implantação Olá no serviço de nuvem Olá, conforme mostrado no exemplo hello abaixo.

> [!IMPORTANT]
> Um pré-requisito toorun Olá etapas é toohave uma rede virtual já foi criada para implantação em nuvem hello. Você precisará Olá rede virtual nome e a sub-rede nome toocreate Olá balanceamento de carga interno.

### <a name="step-1"></a>Etapa 1

Abra o arquivo de configuração de serviço de saudação (. cscfg) para sua implantação de nuvem no Visual Studio e adicionar Olá seguir Olá de toocreate seção balanceamento de carga interno em Olá última "`</Role>`" item de configuração de rede hello.

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="name of hello load balancer">
        <FrontendIPConfiguration type="private" subnet="subnet-name" staticVirtualNetworkIPAddress="static-IP-address"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

Vamos adicionar valores Olá para o arquivo de configuração do hello rede tooshow qual será sua aparência. No exemplo hello, suponha que você criou uma rede virtual chamada "test_vnet" com um 10.0.0.0/24 sub-rede chamado test_subnet e um endereço IP estático 10.0.0.4. o balanceador de carga Olá será nomeado testLB.

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="testLB">
        <FrontendIPConfiguration type="private" subnet="test_subnet" staticVirtualNetworkIPAddress="10.0.0.4"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

Para obter mais informações sobre o esquema de Balanceador de carga hello, consulte [adicionar balanceador de carga](https://msdn.microsoft.com/library/azure/dn722411.aspx).

### <a name="step-2"></a>Etapa 2

Altere os pontos de extremidade Olá serviço definição (. csdef) arquivo tooadd toohello balanceamento de carga interno. momento Olá uma instância de função é criada, o arquivo de definição de serviço Olá adicionará toohello de instâncias de função hello balanceamento de carga interno.

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" loadBalancer="load-balancer-name" />
    </Endpoints>
</WorkerRole>
```

A seguir Olá mesmos valores de exemplo hello acima, vamos adicionar o arquivo de definição de serviço do hello valores toohello.

```xml
<WorkerRole name="WorkerRole1" vmsize="A7" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="endpoint1" protocol="http" localPort="80" port="80" loadBalancer="testLB" />
    </Endpoints>
</WorkerRole>
```

tráfego de rede Olá terão a carga balanceada utilizando o balanceador de carga testLB hello usando a porta 80 para solicitações de entrada, enviando tooworker instâncias de função também na porta 80.

## <a name="next-steps"></a>Próximas etapas

[Configurar um modo de distribuição do balanceador de carga usando a afinidade de IP de origem](load-balancer-distribution-mode.md)

[Definir configurações de tempo limite de TCP ocioso para o balanceador de carga](load-balancer-tcp-idle-timeout.md)

