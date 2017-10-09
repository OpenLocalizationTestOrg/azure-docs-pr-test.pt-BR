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
# <a name="configure-hello-distribution-mode-for-load-balancer"></a><span data-ttu-id="bc28a-103">Configurar o modo de distribuição Olá balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="bc28a-103">Configure hello distribution mode for load balancer</span></span>

## <a name="hash-based-distribution-mode"></a><span data-ttu-id="bc28a-104">Modo de distribuição baseado em hash</span><span class="sxs-lookup"><span data-stu-id="bc28a-104">Hash-based distribution mode</span></span>

<span data-ttu-id="bc28a-105">algoritmo de distribuição de padrão de saudação é uma tupla 5 (fonte de IP, porta de origem, IP de destino, porta de destino, o tipo de protocolo) servidores de tooavailable toomap tráfego de hash.</span><span class="sxs-lookup"><span data-stu-id="bc28a-105">hello default distribution algorithm is a 5-tuple (source IP, source port, destination IP, destination port, protocol type) hash toomap traffic tooavailable servers.</span></span> <span data-ttu-id="bc28a-106">Ele fornece permanência somente dentro de uma sessão de transporte.</span><span class="sxs-lookup"><span data-stu-id="bc28a-106">It provides stickiness only within a transport session.</span></span> <span data-ttu-id="bc28a-107">Pacotes de saudação mesma sessão será direcionado toohello instância mesmo datacenter IP (DIP) por trás do ponto de extremidade de balanceamento de carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="bc28a-107">Packets in hello same session will be directed toohello same datacenter IP (DIP) instance behind hello load balanced endpoint.</span></span> <span data-ttu-id="bc28a-108">Quando Olá cliente inicia uma nova sessão de Olá mesmo IP de origem, porta de origem Olá altera e faz com que o hello tráfego toogo tooa DIP ponto de extremidade diferente.</span><span class="sxs-lookup"><span data-stu-id="bc28a-108">When hello client starts a new session from hello same source IP, hello source port changes and causes hello traffic toogo tooa different DIP endpoint.</span></span>

![balanceador de carga baseado em hash](./media/load-balancer-distribution-mode/load-balancer-distribution.png)

<span data-ttu-id="bc28a-110">Figura 1 – Distribuição das 5 tuplas</span><span class="sxs-lookup"><span data-stu-id="bc28a-110">Figure 1 - 5-tuple distribution</span></span>

## <a name="source-ip-affinity-mode"></a><span data-ttu-id="bc28a-111">Modo de afinidade de IP de origem</span><span class="sxs-lookup"><span data-stu-id="bc28a-111">Source IP affinity mode</span></span>

<span data-ttu-id="bc28a-112">Temos outro modo de distribuição chamado Afinidade de IP de origem (também conhecido como afinidade de sessão ou afinidade de IP do cliente).</span><span class="sxs-lookup"><span data-stu-id="bc28a-112">We have another distribution mode called Source IP Affinity (also known as session affinity or client IP affinity).</span></span> <span data-ttu-id="bc28a-113">O balanceador de carga do Azure pode ser configurado toouse uma tupla de 2 (IP de origem, IP de destino) ou (protocolo IP de origem, IP de destino) de tupla de 3 toomap tráfego toohello os servidores disponíveis.</span><span class="sxs-lookup"><span data-stu-id="bc28a-113">Azure Load Balancer can be configured toouse a 2-tuple (Source IP, Destination IP) or 3-tuple (Source IP, Destination IP, Protocol) toomap traffic toohello available servers.</span></span> <span data-ttu-id="bc28a-114">Usando a afinidade de IP de origem, conexões iniciadas da saudação mesmo computador cliente vai toohello mesmo ponto de extremidade DIP.</span><span class="sxs-lookup"><span data-stu-id="bc28a-114">By using Source IP affinity, connections initiated from hello same client computer goes toohello same DIP endpoint.</span></span>

<span data-ttu-id="bc28a-115">Olá diagrama a seguir ilustra uma configuração de 2 tuplas.</span><span class="sxs-lookup"><span data-stu-id="bc28a-115">hello following diagram illustrates a 2-tuple configuration.</span></span> <span data-ttu-id="bc28a-116">Observe como tupla de 2 Olá Olá carga balanceador toovirtual máquina 1 (VM1) que é feita backup da VM2 e VM3 executa.</span><span class="sxs-lookup"><span data-stu-id="bc28a-116">Notice how hello 2-tuple runs through hello load balancer toovirtual machine 1 (VM1) which is then backed up by VM2 and VM3.</span></span>

![afinidade de sessão](./media/load-balancer-distribution-mode/load-balancer-session-affinity.png)

<span data-ttu-id="bc28a-118">Figura 2 – Distribuição das 2 tuplas</span><span class="sxs-lookup"><span data-stu-id="bc28a-118">Figure 2 - 2-tuple distribution</span></span>

<span data-ttu-id="bc28a-119">Afinidade IP de origem resolve uma incompatibilidade entre o Gateway de área de trabalho remota (RD) e Olá balanceador de carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="bc28a-119">Source IP affinity solves an incompatibility between hello Azure Load Balancer and Remote Desktop (RD) Gateway.</span></span> <span data-ttu-id="bc28a-120">Agora é possível criar um farm de gateway de Área de Trabalho Remota em um único serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="bc28a-120">Now you can build an RD gateway farm in a single cloud service.</span></span>

<span data-ttu-id="bc28a-121">Outro cenário de caso de uso é o carregamento de mídia onde Olá carregamento de dados ocorre através de UDP, mas o plano de controle Olá é obtido por meio de TCP:</span><span class="sxs-lookup"><span data-stu-id="bc28a-121">Another use case scenario is media upload where hello data upload happens through UDP but hello control plane is achieved through TCP:</span></span>

* <span data-ttu-id="bc28a-122">Um cliente inicia uma sessão TCP endereço público com balanceamento de carga de toohello primeiro, obtém tooa direcionado DIP específico, esse canal é integridade de conexão Olá esquerdo toomonitor active</span><span class="sxs-lookup"><span data-stu-id="bc28a-122">A client first initiates a TCP session toohello load balanced public address, gets directed tooa specific DIP, this channel is left active toomonitor hello connection health</span></span>
* <span data-ttu-id="bc28a-123">Uma nova sessão UDP de saudação mesmo computador cliente é iniciado toohello ponto de extremidade público com balanceamento de carga de mesma, a expectativa de saudação aqui é que essa conexão também é direcionado toohello mesmo ponto de extremidade DIP como conexão de TCP anterior Olá para que o carregamento de mídia pode ser executado com alta taxa de transferência enquanto também mantém um canal de controle por meio de TCP.</span><span class="sxs-lookup"><span data-stu-id="bc28a-123">A new UDP session from hello same client computer is initiated toohello same load balanced public endpoint, hello expectation here is that this connection is also directed toohello same DIP endpoint as hello previous TCP connection so that media upload can be executed at high throughput while also maintaining a control channel through TCP.</span></span>

> [!NOTE]
> <span data-ttu-id="bc28a-124">Quando um conjunto de balanceamento de carga é alterado (remoção ou adição de uma máquina virtual), distribuição de saudação de solicitações de cliente é recalculada.</span><span class="sxs-lookup"><span data-stu-id="bc28a-124">When a load-balanced set changes (removing or adding a virtual machine), hello distribution of client requests is recomputed.</span></span> <span data-ttu-id="bc28a-125">Você não pode depender de novas conexões de clientes existentes que terminam em Olá mesmo servidor.</span><span class="sxs-lookup"><span data-stu-id="bc28a-125">You cannot depend on new connections from existing clients ending up at hello same server.</span></span> <span data-ttu-id="bc28a-126">Além disso, o uso do modo de distribuição de afinidade do IP de origem pode causar uma distribuição desigual de tráfego.</span><span class="sxs-lookup"><span data-stu-id="bc28a-126">Additionally, using source IP affinity distribution mode may cause an unequal distribution of traffic.</span></span> <span data-ttu-id="bc28a-127">Clientes que executam proxies subjacentes podem ser vistos como um aplicativo cliente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="bc28a-127">Clients running behind proxies may be seen as one unique client application.</span></span>

## <a name="configuring-source-ip-affinity-settings-for-load-balancer"></a><span data-ttu-id="bc28a-128">Definindo configurações de afinidade de IP de origem para o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="bc28a-128">Configuring Source IP affinity settings for load balancer</span></span>

<span data-ttu-id="bc28a-129">Para máquinas virtuais, você pode usar as configurações de tempo limite de toochange do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="bc28a-129">For virtual machines, you can use PowerShell toochange timeout settings:</span></span>

<span data-ttu-id="bc28a-130">Adicionar uma máquina Virtual de tooa do ponto de extremidade do Azure e definir o modo de distribuição do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="bc28a-130">Add an Azure endpoint tooa Virtual Machine and set load balancer distribution mode</span></span>

```powershell
Get-AzureVM -ServiceName mySvc -Name MyVM1 | Add-AzureEndpoint -Name HttpIn -Protocol TCP -PublicPort 80 -LocalPort 8080 –LoadBalancerDistribution sourceIP | Update-AzureVM
```

<span data-ttu-id="bc28a-131">LoadBalancerDistribution pode ser definido toosourceIP 2 tuplas (IP de origem, IP de destino) para balanceamento de carga, sourceIPProtocol para balanceamento de carga de tupla de 3 (protocolo IP de origem, IP de destino), ou nenhum se desejar que o comportamento padrão de saudação do balanceamento de carga de 5 tuplas.</span><span class="sxs-lookup"><span data-stu-id="bc28a-131">LoadBalancerDistribution can be set toosourceIP for 2-tuple (Source IP, Destination IP) load balancing, sourceIPProtocol for 3-tuple (Source IP, Destination IP, protocol) load balancing, or none if you want hello default behavior of 5-tuple load balancing.</span></span>

<span data-ttu-id="bc28a-132">Use Olá tooretrieve uma configuração de modo de distribuição do balanceador de carga do ponto de extremidade a seguir:</span><span class="sxs-lookup"><span data-stu-id="bc28a-132">Use hello following tooretrieve an endpoint load balancer distribution mode configuration:</span></span>

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

<span data-ttu-id="bc28a-133">Se Olá LoadBalancerDistribution elemento não estiver presente balanceador de carga do Azure Olá usa o algoritmo de 5 tuplas saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="bc28a-133">If hello LoadBalancerDistribution element is not present then hello Azure Load balancer uses hello default 5-tuple algorithm.</span></span>

### <a name="set-hello-distribution-mode-on-a-load-balanced-endpoint-set"></a><span data-ttu-id="bc28a-134">Definir o modo de distribuição de saudação em um conjunto de ponto de extremidade com balanceamento de carga</span><span class="sxs-lookup"><span data-stu-id="bc28a-134">Set hello Distribution mode on a load balanced endpoint set</span></span>

<span data-ttu-id="bc28a-135">Se os pontos de extremidade são parte de um conjunto de ponto de extremidade com balanceamento de carga, o modo de distribuição Olá deve ser definido no conjunto de ponto de extremidade com balanceamento de carga hello:</span><span class="sxs-lookup"><span data-stu-id="bc28a-135">If endpoints are part of a load balanced endpoint set, hello distribution mode must be set on hello load balanced endpoint set:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName MyService -LBSetName LBSet1 -Protocol TCP -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 –LoadBalancerDistribution sourceIP
```

### <a name="cloud-service-configuration-toochange-distribution-mode"></a><span data-ttu-id="bc28a-136">Modo de distribuição de toochange de configuração de serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="bc28a-136">Cloud Service configuration toochange distribution mode</span></span>

<span data-ttu-id="bc28a-137">Você pode aproveitar hello Azure SDK para .NET 2.5 (toobe lançada em novembro) tooupdate seu serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="bc28a-137">You can leverage hello Azure SDK for .NET 2.5 (toobe released in November) tooupdate your Cloud Service.</span></span> <span data-ttu-id="bc28a-138">Configurações de ponto de extremidade para serviços de nuvem são feitas no. csdef de saudação.</span><span class="sxs-lookup"><span data-stu-id="bc28a-138">Endpoint settings for Cloud Services are made in hello .csdef.</span></span> <span data-ttu-id="bc28a-139">Em ordem tooupdate Olá carga balanceador modo de distribuição para uma implantação de serviços de nuvem, é necessária uma atualização de implantação.</span><span class="sxs-lookup"><span data-stu-id="bc28a-139">In order tooupdate hello load balancer distribution mode for a Cloud Services deployment, a deployment upgrade is required.</span></span>
<span data-ttu-id="bc28a-140">Aqui está um exemplo de alterações .csdef para configurações do ponto de extremidade:</span><span class="sxs-lookup"><span data-stu-id="bc28a-140">Here is an example of .csdef changes for endpoint settings:</span></span>

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

## <a name="api-example"></a><span data-ttu-id="bc28a-141">Exemplo de API</span><span class="sxs-lookup"><span data-stu-id="bc28a-141">API example</span></span>

<span data-ttu-id="bc28a-142">Você pode configurar a distribuição de Balanceador de carga hello usando a API de gerenciamento do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="bc28a-142">You can configure hello load balancer distribution using hello service management API.</span></span> <span data-ttu-id="bc28a-143">Verifique se Olá de tooadd `x-ms-version` cabeçalho é definido tooversion `2014-09-01` ou superior.</span><span class="sxs-lookup"><span data-stu-id="bc28a-143">Make sure tooadd hello `x-ms-version` header is set tooversion `2014-09-01` or higher.</span></span>

### <a name="update-hello-configuration-of-hello-specified-load-balanced-set-in-a-deployment"></a><span data-ttu-id="bc28a-144">Atualizar o conjunto de configuração de saudação especificada com balanceamento de carga de saudação em uma implantação</span><span class="sxs-lookup"><span data-stu-id="bc28a-144">Update hello configuration of hello specified load-balanced set in a deployment</span></span>

#### <a name="request-example"></a><span data-ttu-id="bc28a-145">Exemplo de solicitação</span><span class="sxs-lookup"><span data-stu-id="bc28a-145">Request example</span></span>

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

<span data-ttu-id="bc28a-146">valor de saudação do LoadBalancerDistribution pode ser sourceIP para afinidade de tupla de 2, sourceIPProtocol para afinidade de tupla de 3 ou none (nenhuma afinidade de.</span><span class="sxs-lookup"><span data-stu-id="bc28a-146">hello value of LoadBalancerDistribution can be sourceIP for 2-tuple affinity, sourceIPProtocol for 3-tuple affinity or none (for no affinity.</span></span> <span data-ttu-id="bc28a-147">por exemplo, 5 tuplas)</span><span class="sxs-lookup"><span data-stu-id="bc28a-147">i.e. 5-tuple)</span></span>

#### <a name="response"></a><span data-ttu-id="bc28a-148">Response</span><span class="sxs-lookup"><span data-stu-id="bc28a-148">Response</span></span>

    HTTP/1.1 202 Accepted
    Cache-Control: no-cache
    Content-Length: 0
    Server: 1.0.6198.146 (rd_rdfe_stable.141015-1306) Microsoft-HTTPAPI/2.0
    x-ms-servedbyregion: ussouth2
    x-ms-request-id: 9c7bda3e67c621a6b57096323069f7af
    Date: Thu, 16 Oct 2014 22:49:21 GMT

## <a name="next-steps"></a><span data-ttu-id="bc28a-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bc28a-149">Next Steps</span></span>

[<span data-ttu-id="bc28a-150">Visão geral do balanceador de carga interno</span><span class="sxs-lookup"><span data-stu-id="bc28a-150">Internal load balancer overview</span></span>](load-balancer-internal-overview.md)

[<span data-ttu-id="bc28a-151">Introdução à configuração de um balanceador de carga para a Internet</span><span class="sxs-lookup"><span data-stu-id="bc28a-151">Get started Configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="bc28a-152">Definir configurações de tempo limite de TCP ocioso para o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="bc28a-152">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
