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
# <a name="get-started-creating-an-internet-facing-load-balancer-for-cloud-services"></a><span data-ttu-id="a6ec6-103">Introdução à criação de um balanceador de carga para a Internet para serviços de nuvem</span><span class="sxs-lookup"><span data-stu-id="a6ec6-103">Get started creating an Internet facing load balancer for cloud services</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a6ec6-104">Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="a6ec6-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="a6ec6-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a6ec6-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="a6ec6-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="a6ec6-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="a6ec6-107">Serviços de Nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="a6ec6-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="a6ec6-108">Antes de trabalhar com recursos do Azure, é importante toounderstand que o Azure atualmente tem dois modelos de implantação: Gerenciador de recursos do Azure e clássico.</span><span class="sxs-lookup"><span data-stu-id="a6ec6-108">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="a6ec6-109">Verifique se você entendeu [os modelos e as ferramentas de implantação](../azure-classic-rm.md) antes de trabalhar com qualquer recurso do Azure.</span><span class="sxs-lookup"><span data-stu-id="a6ec6-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="a6ec6-110">Você pode exibir a documentação de saudação para diferentes ferramentas clicando Olá guias na parte superior da saudação deste artigo.</span><span class="sxs-lookup"><span data-stu-id="a6ec6-110">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="a6ec6-111">Este artigo aborda o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="a6ec6-111">This article covers hello classic deployment model.</span></span> <span data-ttu-id="a6ec6-112">Você também pode [aprender a usar o Gerenciador de recursos do Azure de Balanceador de carga de toocreate um voltados à Internet de como](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="a6ec6-112">You can also [Learn how toocreate an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

<span data-ttu-id="a6ec6-113">Serviços de nuvem são automaticamente configurados com um balanceador de carga e podem ser personalizados por meio do modelo de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="a6ec6-113">Cloud services are automatically configured with a load balancer and can be customized via hello service model.</span></span>

## <a name="create-a-load-balancer-using-hello-service-definition-file"></a><span data-ttu-id="a6ec6-114">Criar um balanceador de carga usando o arquivo de definição de serviço Olá</span><span class="sxs-lookup"><span data-stu-id="a6ec6-114">Create a load balancer using hello service definition file</span></span>

<span data-ttu-id="a6ec6-115">Você pode aproveitar hello Azure SDK para .NET 2.5 tooupdate seu serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="a6ec6-115">You can leverage hello Azure SDK for .NET 2.5 tooupdate your cloud service.</span></span> <span data-ttu-id="a6ec6-116">Configurações de ponto de extremidade para serviços de nuvem são feitas no hello [definição de serviço](https://msdn.microsoft.com/library/azure/gg557553.aspx) arquivo. csdef.</span><span class="sxs-lookup"><span data-stu-id="a6ec6-116">Endpoint settings for cloud services are made in hello [service definition](https://msdn.microsoft.com/library/azure/gg557553.aspx) .csdef file.</span></span>

<span data-ttu-id="a6ec6-117">Olá exemplo a seguir mostra como um arquivo servicedefinition. csdef para uma implantação em nuvem é configurado:</span><span class="sxs-lookup"><span data-stu-id="a6ec6-117">hello following example shows how a servicedefinition.csdef file for a cloud deployment is configured:</span></span>

<span data-ttu-id="a6ec6-118">Verificando o trecho Olá Olá. csdef arquivo gerado por uma implantação de nuvem, você pode ver Olá externo de ponto de extremidade configurado toouse portas HTTP na porta 10000 e 10001 10002.</span><span class="sxs-lookup"><span data-stu-id="a6ec6-118">Checking hello snippet for hello .csdef file generated by a cloud deployment, you can see hello external endpoint configured toouse ports HTTP on port 10000, 10001, and 10002.</span></span>

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

## <a name="check-load-balancer-health-status-for-cloud-services"></a><span data-ttu-id="a6ec6-119">Verificar o status de integridade do balanceador de carga para serviços de nuvem</span><span class="sxs-lookup"><span data-stu-id="a6ec6-119">Check load balancer health status for cloud services</span></span>

<span data-ttu-id="a6ec6-120">Olá seguinte é um exemplo de um teste de integridade:</span><span class="sxs-lookup"><span data-stu-id="a6ec6-120">hello following is an example of a health probe:</span></span>

```xml
<LoadBalancerProbes>
    <LoadBalancerProbe name=“MyProbe” protocol=“http” path=“Probe.aspx” intervalInSeconds=“5” timeoutInSeconds=“100“ />
</LoadBalancerProbes>
```

<span data-ttu-id="a6ec6-121">Olá balanceador de carga combina informações de saudação do ponto de extremidade de saudação e informações de saudação de Olá investigação toocreate uma URL na forma de saudação de `http://{DIP of VM}:80/Probe.aspx` que pode ser usado tooquery Olá integridade do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="a6ec6-121">hello load balancer combines hello information of hello endpoint and hello information of hello probe toocreate a URL in hello form of `http://{DIP of VM}:80/Probe.aspx` that can be used tooquery hello health of hello service.</span></span>

<span data-ttu-id="a6ec6-122">serviço Hello detecta investigações periódicas de saudação mesmo endereço IP.</span><span class="sxs-lookup"><span data-stu-id="a6ec6-122">hello service detects periodic probes from hello same IP address.</span></span> <span data-ttu-id="a6ec6-123">Isso é a solicitação de investigação de integridade hello proveniente do host de saudação do nó de saudação onde a máquina virtual de hello está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="a6ec6-123">This is hello health probe request coming from hello host of hello node where hello virtual machine is running.</span></span> <span data-ttu-id="a6ec6-124">serviço de saudação tem toorespond com um código de status HTTP 200 para Olá carga balanceador tooassume que o serviço de saudação está íntegro.</span><span class="sxs-lookup"><span data-stu-id="a6ec6-124">hello service has toorespond with a HTTP 200 status code for hello load balancer tooassume that hello service is healthy.</span></span> <span data-ttu-id="a6ec6-125">Qualquer outro status do HTTP de código (por exemplo, 503) diretamente leva Olá a máquina virtual da rotação.</span><span class="sxs-lookup"><span data-stu-id="a6ec6-125">Any other HTTP status code (for example 503) directly takes hello virtual machine out of rotation.</span></span>

<span data-ttu-id="a6ec6-126">definição de investigação de saudação também controla a frequência de saudação do teste de saudação.</span><span class="sxs-lookup"><span data-stu-id="a6ec6-126">hello probe definition also controls hello frequency of hello probe.</span></span> <span data-ttu-id="a6ec6-127">Em nosso caso acima, o balanceador de carga Olá é sondando ponto de extremidade Olá cada 5 segundos.</span><span class="sxs-lookup"><span data-stu-id="a6ec6-127">In our case above, hello load balancer is probing hello endpoint every 5 secs.</span></span> <span data-ttu-id="a6ec6-128">Se nenhuma resposta positiva for recebida para 10 segundos (dois intervalos de teste), teste Olá será considerado inativo e máquina virtual de saudação é retirada da rotação.</span><span class="sxs-lookup"><span data-stu-id="a6ec6-128">If no positive answer is received for 10 secs (two probe intervals), hello probe is assumed down, and hello virtual machine is taken out of rotation.</span></span> <span data-ttu-id="a6ec6-129">Da mesma forma, se o serviço hello está fora da rotação e uma resposta positiva é recebida, o serviço de saudação é colocado de volta toorotation imediatamente.</span><span class="sxs-lookup"><span data-stu-id="a6ec6-129">Similarly, if hello service is out of rotation and a positive answer is received, hello service is put back toorotation right away.</span></span> <span data-ttu-id="a6ec6-130">Se o serviço de saudação está flutuando entre íntegro e não íntegro, balanceador de carga Olá pode decidir toodelay Olá nova Introdução Olá serviço back toorotation até que ele tenha sido íntegro para um número de testes.</span><span class="sxs-lookup"><span data-stu-id="a6ec6-130">If hello service is fluctuating between healthy and unhealthy, hello load balancer can decide toodelay hello re-introduction of hello service back toorotation until it has been healthy for a number of probes.</span></span>

<span data-ttu-id="a6ec6-131">Verifique o esquema de definição de serviço Olá para Olá [investigação de integridade](https://msdn.microsoft.com/library/azure/jj151530.aspx) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="a6ec6-131">Check hello service definition schema for hello [health probe](https://msdn.microsoft.com/library/azure/jj151530.aspx) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6ec6-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a6ec6-132">Next steps</span></span>

[<span data-ttu-id="a6ec6-133">Introdução à configuração de um balanceador de carga interno</span><span class="sxs-lookup"><span data-stu-id="a6ec6-133">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="a6ec6-134">Configurar um modo de distribuição do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="a6ec6-134">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="a6ec6-135">Definir configurações de tempo limite de TCP ocioso para o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="a6ec6-135">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

