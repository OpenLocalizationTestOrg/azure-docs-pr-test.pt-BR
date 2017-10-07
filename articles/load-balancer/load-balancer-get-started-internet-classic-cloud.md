---
title: "aaaCreate um voltados para Internet balanceador de carga para serviços de nuvem do Azure | Microsoft Docs"
description: "Saiba como toocreate voltado para a Internet um balanceador de carga no modelo de implantação clássico para serviços de nuvem"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 0bb16f96-56a6-429f-88f5-0de2d0136756
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: d93cf76d417cbfc744cf07ba48c43a63cc14df69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-for-cloud-services"></a>Introdução à criação de um balanceador de carga para a Internet para serviços de nuvem

> [!div class="op_single_selector"]
> * [Portal clássico do Azure](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [CLI do Azure](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [Serviços de Nuvem do Azure](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> Antes de trabalhar com recursos do Azure, é importante toounderstand que o Azure atualmente tem dois modelos de implantação: Gerenciador de recursos do Azure e clássico. Verifique se você entendeu [os modelos e as ferramentas de implantação](../azure-classic-rm.md) antes de trabalhar com qualquer recurso do Azure. Você pode exibir a documentação de saudação para diferentes ferramentas clicando Olá guias na parte superior da saudação deste artigo. Este artigo aborda o modelo de implantação clássico hello. Você também pode [aprender a usar o Gerenciador de recursos do Azure de Balanceador de carga de toocreate um voltados à Internet de como](load-balancer-get-started-internet-arm-ps.md).

Serviços de nuvem são automaticamente configurados com um balanceador de carga e podem ser personalizados por meio do modelo de serviço hello.

## <a name="create-a-load-balancer-using-hello-service-definition-file"></a>Criar um balanceador de carga usando o arquivo de definição de serviço Olá

Você pode aproveitar hello Azure SDK para .NET 2.5 tooupdate seu serviço de nuvem. Configurações de ponto de extremidade para serviços de nuvem são feitas no hello [definição de serviço](https://msdn.microsoft.com/library/azure/gg557553.aspx) arquivo. csdef.

Olá exemplo a seguir mostra como um arquivo servicedefinition. csdef para uma implantação em nuvem é configurado:

Verificando o trecho Olá Olá. csdef arquivo gerado por uma implantação de nuvem, você pode ver Olá externo de ponto de extremidade configurado toouse portas HTTP na porta 10000 e 10001 10002.

```xml
<ServiceDefinition name=“Tenant“>
    <WorkerRole name=“FERole” vmsize=“Small“>
<Endpoints>
    <InputEndpoint name=“FE_External_Http” protocol=“http” port=“10000“ />
    <InputEndpoint name=“FE_External_Tcp“  protocol=“tcp“  port=“10001“ />
    <InputEndpoint name=“FE_External_Udp“  protocol=“udp“  port=“10002“ />

    <InputEndpointname=“HTTP_Probe” protocol=“http” port=“80” loadBalancerProbe=“MyProbe“ />

    <InstanceInputEndpoint name=“InstanceEP” protocol=“tcp” localPort=“80“>
        <AllocatePublicPortFrom>
            <FixedPortRange min=“10110” max=“10120“  />
        </AllocatePublicPortFrom>
    </InstanceInputEndpoint>
    <InternalEndpoint name=“FE_InternalEP_Tcp” protocol=“tcp“ />
</Endpoints>
    </WorkerRole>
</ServiceDefinition>
```

## <a name="check-load-balancer-health-status-for-cloud-services"></a>Verificar o status de integridade do balanceador de carga para serviços de nuvem

Olá seguinte é um exemplo de um teste de integridade:

```xml
<LoadBalancerProbes>
    <LoadBalancerProbe name=“MyProbe” protocol=“http” path=“Probe.aspx” intervalInSeconds=“5” timeoutInSeconds=“100“ />
</LoadBalancerProbes>
```

Olá balanceador de carga combina informações de saudação do ponto de extremidade de saudação e informações de saudação de Olá investigação toocreate uma URL na forma de saudação de `http://{DIP of VM}:80/Probe.aspx` que pode ser usado tooquery Olá integridade do serviço de saudação.

serviço Hello detecta investigações periódicas de saudação mesmo endereço IP. Isso é a solicitação de investigação de integridade hello proveniente do host de saudação do nó de saudação onde a máquina virtual de hello está sendo executado. serviço de saudação tem toorespond com um código de status HTTP 200 para Olá carga balanceador tooassume que o serviço de saudação está íntegro. Qualquer outro status do HTTP de código (por exemplo, 503) diretamente leva Olá a máquina virtual da rotação.

definição de investigação de saudação também controla a frequência de saudação do teste de saudação. Em nosso caso acima, o balanceador de carga Olá é sondando ponto de extremidade Olá cada 5 segundos. Se nenhuma resposta positiva for recebida para 10 segundos (dois intervalos de teste), teste Olá será considerado inativo e máquina virtual de saudação é retirada da rotação. Da mesma forma, se o serviço hello está fora da rotação e uma resposta positiva é recebida, o serviço de saudação é colocado de volta toorotation imediatamente. Se o serviço de saudação está flutuando entre íntegro e não íntegro, balanceador de carga Olá pode decidir toodelay Olá nova Introdução Olá serviço back toorotation até que ele tenha sido íntegro para um número de testes.

Verifique o esquema de definição de serviço Olá para Olá [investigação de integridade](https://msdn.microsoft.com/library/azure/jj151530.aspx) para obter mais informações.

## <a name="next-steps"></a>Próximas etapas

[Introdução à configuração de um balanceador de carga interno](load-balancer-get-started-ilb-arm-ps.md)

[Configurar um modo de distribuição do balanceador de carga](load-balancer-distribution-mode.md)

[Definir configurações de tempo limite de TCP ocioso para o balanceador de carga](load-balancer-tcp-idle-timeout.md)

