---
title: "Criar um balanceador de carga voltado para a Internet dos serviços de nuvem do Azure| Microsoft Docs"
description: "Saiba como criar um balanceador de carga para a Internet no modelo de implantação clássico para serviços de nuvem"
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
ms.openlocfilehash: 1ceaafebcaebecb04314c7da62c69b2e9b5ba39a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-for-cloud-services"></a><span data-ttu-id="6d46a-103">Introdução à criação de um balanceador de carga para a Internet para serviços de nuvem</span><span class="sxs-lookup"><span data-stu-id="6d46a-103">Get started creating an Internet facing load balancer for cloud services</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="6d46a-104">Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="6d46a-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="6d46a-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6d46a-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="6d46a-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="6d46a-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="6d46a-107">Serviços de Nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="6d46a-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="6d46a-108">Antes de trabalhar com os recursos do Azure, é importante entender que, no momento, o Azure apresenta dois modelos de implantação: Azure Resource Manager e clássico.</span><span class="sxs-lookup"><span data-stu-id="6d46a-108">Before you work with Azure resources, it's important to understand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="6d46a-109">Verifique se você entendeu [os modelos e as ferramentas de implantação](../azure-classic-rm.md) antes de trabalhar com qualquer recurso do Azure.</span><span class="sxs-lookup"><span data-stu-id="6d46a-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="6d46a-110">Você pode exibir a documentação para ferramentas diferentes clicando nas guias na parte superior deste artigo.</span><span class="sxs-lookup"><span data-stu-id="6d46a-110">You can view the documentation for different tools by clicking the tabs at the top of this article.</span></span> <span data-ttu-id="6d46a-111">Este artigo aborda o modelo de implantação clássico.</span><span class="sxs-lookup"><span data-stu-id="6d46a-111">This article covers the classic deployment model.</span></span> <span data-ttu-id="6d46a-112">Também é possível [Saber como criar um balanceador de carga para a Internet usando o Gerenciador de Recursos do Azure](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="6d46a-112">You can also [Learn how to create an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

<span data-ttu-id="6d46a-113">Serviços de nuvem são automaticamente configurados com um balanceador de carga e podem ser personalizados por meio do modelo de serviço.</span><span class="sxs-lookup"><span data-stu-id="6d46a-113">Cloud services are automatically configured with a load balancer and can be customized via the service model.</span></span>

## <a name="create-a-load-balancer-using-the-service-definition-file"></a><span data-ttu-id="6d46a-114">Criar um balanceador de carga usando o arquivo de definição de serviço</span><span class="sxs-lookup"><span data-stu-id="6d46a-114">Create a load balancer using the service definition file</span></span>

<span data-ttu-id="6d46a-115">Você pode aproveitar o SDK do Azure para .NET 2.5 para atualizar seu serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="6d46a-115">You can leverage the Azure SDK for .NET 2.5 to update your cloud service.</span></span> <span data-ttu-id="6d46a-116">As configurações de ponto de extremidade para serviços de nuvem são feitas no arquivo .csdef da [definição de serviço](https://msdn.microsoft.com/library/azure/gg557553.aspx).</span><span class="sxs-lookup"><span data-stu-id="6d46a-116">Endpoint settings for cloud services are made in the [service definition](https://msdn.microsoft.com/library/azure/gg557553.aspx) .csdef file.</span></span>

<span data-ttu-id="6d46a-117">O exemplo a seguir mostra como um arquivo servicedefinition.csdef é configurado para uma implantação na nuvem:</span><span class="sxs-lookup"><span data-stu-id="6d46a-117">The following example shows how a servicedefinition.csdef file for a cloud deployment is configured:</span></span>

<span data-ttu-id="6d46a-118">Ao verificar o trecho de código do arquivo .csdef gerado por uma implantação na nuvem, você pode ver o ponto de extremidade externo configurado para usar portas HTTP na porta 10000, 10001 e 10002.</span><span class="sxs-lookup"><span data-stu-id="6d46a-118">Checking the snippet for the .csdef file generated by a cloud deployment, you can see the external endpoint configured to use ports HTTP on port 10000, 10001, and 10002.</span></span>

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

## <a name="check-load-balancer-health-status-for-cloud-services"></a><span data-ttu-id="6d46a-119">Verificar o status de integridade do balanceador de carga para serviços de nuvem</span><span class="sxs-lookup"><span data-stu-id="6d46a-119">Check load balancer health status for cloud services</span></span>

<span data-ttu-id="6d46a-120">A seguir, um exemplo de como criar uma investigação:</span><span class="sxs-lookup"><span data-stu-id="6d46a-120">The following is an example of a health probe:</span></span>

```xml
<LoadBalancerProbes>
    <LoadBalancerProbe name=“MyProbe” protocol=“http” path=“Probe.aspx” intervalInSeconds=“5” timeoutInSeconds=“100“ />
</LoadBalancerProbes>
```

<span data-ttu-id="6d46a-121">O balanceador de carga combina as informações do ponto de extremidade e as informações de investigação para criar uma URL na forma de `http://{DIP of VM}:80/Probe.aspx`, que podem ser usadas para consultar a integridade do serviço.</span><span class="sxs-lookup"><span data-stu-id="6d46a-121">The load balancer combines the information of the endpoint and the information of the probe to create a URL in the form of `http://{DIP of VM}:80/Probe.aspx` that can be used to query the health of the service.</span></span>

<span data-ttu-id="6d46a-122">O serviço detecta as investigações periódicas do mesmo endereço IP.</span><span class="sxs-lookup"><span data-stu-id="6d46a-122">The service detects periodic probes from the same IP address.</span></span> <span data-ttu-id="6d46a-123">Esta é a solicitação de investigação de integridade proveniente do host do nó no qual a máquina virtual está sendo executada.</span><span class="sxs-lookup"><span data-stu-id="6d46a-123">This is the health probe request coming from the host of the node where the virtual machine is running.</span></span> <span data-ttu-id="6d46a-124">O serviço deve responder com um código de status HTTP 200 para que o balanceador de carga presuma que o serviço esteja íntegro.</span><span class="sxs-lookup"><span data-stu-id="6d46a-124">The service has to respond with a HTTP 200 status code for the load balancer to assume that the service is healthy.</span></span> <span data-ttu-id="6d46a-125">Qualquer outro código de status HTTP (por exemplo, 503) leva diretamente à máquina virtual da rotação.</span><span class="sxs-lookup"><span data-stu-id="6d46a-125">Any other HTTP status code (for example 503) directly takes the virtual machine out of rotation.</span></span>

<span data-ttu-id="6d46a-126">A definição da investigação também controla a frequência da investigação.</span><span class="sxs-lookup"><span data-stu-id="6d46a-126">The probe definition also controls the frequency of the probe.</span></span> <span data-ttu-id="6d46a-127">No caso acima, o balanceador de carga está investigando o ponto de extremidade a cada 5 segundos.</span><span class="sxs-lookup"><span data-stu-id="6d46a-127">In our case above, the load balancer is probing the endpoint every 5 secs.</span></span> <span data-ttu-id="6d46a-128">Se nenhuma resposta positiva for recebida em 10 segundos (dois intervalos de investigação), a investigação será considerada inativa e a máquina virtual sairá da rotação.</span><span class="sxs-lookup"><span data-stu-id="6d46a-128">If no positive answer is received for 10 secs (two probe intervals), the probe is assumed down, and the virtual machine is taken out of rotation.</span></span> <span data-ttu-id="6d46a-129">Da mesma forma, se o serviço estiver fora de rotação e uma resposta positiva for recebida, o serviço será colocado de volta à rotação imediatamente.</span><span class="sxs-lookup"><span data-stu-id="6d46a-129">Similarly, if the service is out of rotation and a positive answer is received, the service is put back to rotation right away.</span></span> <span data-ttu-id="6d46a-130">Se o serviço estiver flutuando entre íntegro e não íntegro, o balanceador de carga pode optar por atrasar a reintrodução do serviço na rotação até que ele esteja íntegro para um número de investigações.</span><span class="sxs-lookup"><span data-stu-id="6d46a-130">If the service is fluctuating between healthy and unhealthy, the load balancer can decide to delay the re-introduction of the service back to rotation until it has been healthy for a number of probes.</span></span>

<span data-ttu-id="6d46a-131">Verifique o esquema de definição de serviço para a [investigação de integridade](https://msdn.microsoft.com/library/azure/jj151530.aspx) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="6d46a-131">Check the service definition schema for the [health probe](https://msdn.microsoft.com/library/azure/jj151530.aspx) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d46a-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6d46a-132">Next steps</span></span>

[<span data-ttu-id="6d46a-133">Introdução à configuração de um balanceador de carga interno</span><span class="sxs-lookup"><span data-stu-id="6d46a-133">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="6d46a-134">Configurar um modo de distribuição do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="6d46a-134">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="6d46a-135">Definir configurações de tempo limite de TCP ocioso para o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="6d46a-135">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

