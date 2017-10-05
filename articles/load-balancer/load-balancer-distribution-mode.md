---
title: "Configurar modo de distribuição do Balanceador de Carga | Microsoft Docs"
description: "Como configurar o modo de distribuição do balanceador de carga do Azure para dar suporte à afinidade de IP de origem"
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
ms.openlocfilehash: 4cb000c8ee1bb2e267dc0813dab23a77a46080ce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-the-distribution-mode-for-load-balancer"></a><span data-ttu-id="a38ec-103">Configurar modo de distribuição para o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="a38ec-103">Configure the distribution mode for load balancer</span></span>

## <a name="hash-based-distribution-mode"></a><span data-ttu-id="a38ec-104">Modo de distribuição baseado em hash</span><span class="sxs-lookup"><span data-stu-id="a38ec-104">Hash-based distribution mode</span></span>

<span data-ttu-id="a38ec-105">O algoritmo de distribuição padrão é um hash de 5 tuplas (IP de origem, porta de origem, IP de destino, porta de destino, tipo de protocolo) para mapear o tráfego até os servidores disponíveis.</span><span class="sxs-lookup"><span data-stu-id="a38ec-105">The default distribution algorithm is a 5-tuple (source IP, source port, destination IP, destination port, protocol type) hash to map traffic to available servers.</span></span> <span data-ttu-id="a38ec-106">Ele fornece permanência somente dentro de uma sessão de transporte.</span><span class="sxs-lookup"><span data-stu-id="a38ec-106">It provides stickiness only within a transport session.</span></span> <span data-ttu-id="a38ec-107">Os pacotes na mesma sessão serão direcionados para a mesma instância do DIP (IP de Datacenter) atrás do ponto de extremidade com balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="a38ec-107">Packets in the same session will be directed to the same datacenter IP (DIP) instance behind the load balanced endpoint.</span></span> <span data-ttu-id="a38ec-108">Quando o cliente inicia uma nova sessão por meio do mesmo IP de origem, a porta de origem é alterada e faz com que o tráfego vá para um ponto de extremidade DIP diferente.</span><span class="sxs-lookup"><span data-stu-id="a38ec-108">When the client starts a new session from the same source IP, the source port changes and causes the traffic to go to a different DIP endpoint.</span></span>

![balanceador de carga baseado em hash](./media/load-balancer-distribution-mode/load-balancer-distribution.png)

<span data-ttu-id="a38ec-110">Figura 1 – Distribuição das 5 tuplas</span><span class="sxs-lookup"><span data-stu-id="a38ec-110">Figure 1 - 5-tuple distribution</span></span>

## <a name="source-ip-affinity-mode"></a><span data-ttu-id="a38ec-111">Modo de afinidade de IP de origem</span><span class="sxs-lookup"><span data-stu-id="a38ec-111">Source IP affinity mode</span></span>

<span data-ttu-id="a38ec-112">Temos outro modo de distribuição chamado Afinidade de IP de origem (também conhecido como afinidade de sessão ou afinidade de IP do cliente).</span><span class="sxs-lookup"><span data-stu-id="a38ec-112">We have another distribution mode called Source IP Affinity (also known as session affinity or client IP affinity).</span></span> <span data-ttu-id="a38ec-113">O Azure Load Balancer pode ser configurado para usar 2 tuplas (IP de origem, IP de destino) ou 3 tuplas (IP de origem, IP de destino, Protocolo) para mapear o tráfego até os servidores disponíveis.</span><span class="sxs-lookup"><span data-stu-id="a38ec-113">Azure Load Balancer can be configured to use a 2-tuple (Source IP, Destination IP) or 3-tuple (Source IP, Destination IP, Protocol) to map traffic to the available servers.</span></span> <span data-ttu-id="a38ec-114">Ao usar a afinidade de IP de origem, as conexões iniciadas no mesmo computador cliente vão para o mesmo ponto de extremidade DIP.</span><span class="sxs-lookup"><span data-stu-id="a38ec-114">By using Source IP affinity, connections initiated from the same client computer goes to the same DIP endpoint.</span></span>

<span data-ttu-id="a38ec-115">O diagrama a seguir ilustra uma configuração de 2 tuplas.</span><span class="sxs-lookup"><span data-stu-id="a38ec-115">The following diagram illustrates a 2-tuple configuration.</span></span> <span data-ttu-id="a38ec-116">Observe como a tupla 2 é executada por meio do balanceador de carga para a VM1 (máquina virtual 1) cujo backup é feito pela VM2 e pela VM3.</span><span class="sxs-lookup"><span data-stu-id="a38ec-116">Notice how the 2-tuple runs through the load balancer to virtual machine 1 (VM1) which is then backed up by VM2 and VM3.</span></span>

![afinidade de sessão](./media/load-balancer-distribution-mode/load-balancer-session-affinity.png)

<span data-ttu-id="a38ec-118">Figura 2 – Distribuição das 2 tuplas</span><span class="sxs-lookup"><span data-stu-id="a38ec-118">Figure 2 - 2-tuple distribution</span></span>

<span data-ttu-id="a38ec-119">A afinidade de IP de origem resolve uma incompatibilidade entre o Azure Load Balancer e o Gateway RD (Área de Trabalho Remota).</span><span class="sxs-lookup"><span data-stu-id="a38ec-119">Source IP affinity solves an incompatibility between the Azure Load Balancer and Remote Desktop (RD) Gateway.</span></span> <span data-ttu-id="a38ec-120">Agora é possível criar um farm de gateway de Área de Trabalho Remota em um único serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="a38ec-120">Now you can build an RD gateway farm in a single cloud service.</span></span>

<span data-ttu-id="a38ec-121">Outro cenário de caso de uso é o upload de mídia em que o upload de dados ocorre por meio de UDP, mas o plano de controle é obtido por meio de TCP:</span><span class="sxs-lookup"><span data-stu-id="a38ec-121">Another use case scenario is media upload where the data upload happens through UDP but the control plane is achieved through TCP:</span></span>

* <span data-ttu-id="a38ec-122">Primeiro, um cliente inicia uma sessão TCP com o endereço público do balanceamento de carga e é direcionado para um DIP específico; esse canal permanece ativo para monitorar a integridade da conexão</span><span class="sxs-lookup"><span data-stu-id="a38ec-122">A client first initiates a TCP session to the load balanced public address, gets directed to a specific DIP, this channel is left active to monitor the connection health</span></span>
* <span data-ttu-id="a38ec-123">Uma nova sessão UDP no mesmo computador cliente é iniciada para o mesmo ponto de extremidade público de balanceamento de carga. A expectativa aqui é que essa conexão seja também direcionada para o mesmo ponto de extremidade DIP que a conexão TCP anterior, para que o carregamento da mídia possa ser executado em alta taxa de transferência enquanto mantém um canal de controle pelo TCP.</span><span class="sxs-lookup"><span data-stu-id="a38ec-123">A new UDP session from the same client computer is initiated to the same load balanced public endpoint, the expectation here is that this connection is also directed to the same DIP endpoint as the previous TCP connection so that media upload can be executed at high throughput while also maintaining a control channel through TCP.</span></span>

> [!NOTE]
> <span data-ttu-id="a38ec-124">Quando um conjunto de balanceamento de carga for alterado (removendo ou adicionando uma máquina virtual), a distribuição de solicitações de cliente será recalculada.</span><span class="sxs-lookup"><span data-stu-id="a38ec-124">When a load-balanced set changes (removing or adding a virtual machine), the distribution of client requests is recomputed.</span></span> <span data-ttu-id="a38ec-125">Não é possível depender de novas conexões de clientes existentes que terminam no mesmo servidor.</span><span class="sxs-lookup"><span data-stu-id="a38ec-125">You cannot depend on new connections from existing clients ending up at the same server.</span></span> <span data-ttu-id="a38ec-126">Além disso, o uso do modo de distribuição de afinidade do IP de origem pode causar uma distribuição desigual de tráfego.</span><span class="sxs-lookup"><span data-stu-id="a38ec-126">Additionally, using source IP affinity distribution mode may cause an unequal distribution of traffic.</span></span> <span data-ttu-id="a38ec-127">Clientes que executam proxies subjacentes podem ser vistos como um aplicativo cliente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="a38ec-127">Clients running behind proxies may be seen as one unique client application.</span></span>

## <a name="configuring-source-ip-affinity-settings-for-load-balancer"></a><span data-ttu-id="a38ec-128">Definindo configurações de afinidade de IP de origem para o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="a38ec-128">Configuring Source IP affinity settings for load balancer</span></span>

<span data-ttu-id="a38ec-129">Para máquinas virtuais, é possível usar o PowerShell para alterar as configurações de tempo limite:</span><span class="sxs-lookup"><span data-stu-id="a38ec-129">For virtual machines, you can use PowerShell to change timeout settings:</span></span>

<span data-ttu-id="a38ec-130">Adicione um ponto de extremidade do Azure a uma máquina virtual e defina o modo de distribuição do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="a38ec-130">Add an Azure endpoint to a Virtual Machine and set load balancer distribution mode</span></span>

```powershell
Get-AzureVM -ServiceName mySvc -Name MyVM1 | Add-AzureEndpoint -Name HttpIn -Protocol TCP -PublicPort 80 -LocalPort 8080 –LoadBalancerDistribution sourceIP | Update-AzureVM
```

<span data-ttu-id="a38ec-131">O LoadBalancerDistribution poderá ser definido como sourceIP para balanceamento de carga de 2 tuplas (IP de origem, IP de destino), sourceIPProtocol para balanceamento de carga de 3 tuplas (IP de destino, IP de origem, protocolo) ou nenhum se você quiser o comportamento padrão de balanceamento de carga de 5 tuplas.</span><span class="sxs-lookup"><span data-stu-id="a38ec-131">LoadBalancerDistribution can be set to sourceIP for 2-tuple (Source IP, Destination IP) load balancing, sourceIPProtocol for 3-tuple (Source IP, Destination IP, protocol) load balancing, or none if you want the default behavior of 5-tuple load balancing.</span></span>

<span data-ttu-id="a38ec-132">Use o seguinte para recuperar uma configuração de modo de distribuição do balanceador de carga do ponto de extremidade:</span><span class="sxs-lookup"><span data-stu-id="a38ec-132">Use the following to retrieve an endpoint load balancer distribution mode configuration:</span></span>

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

<span data-ttu-id="a38ec-133">Se o elemento LoadBalancerDistribution não estiver presente, o balanceador de carga do Azure usará o algoritmo padrão de tupla 5.</span><span class="sxs-lookup"><span data-stu-id="a38ec-133">If the LoadBalancerDistribution element is not present then the Azure Load balancer uses the default 5-tuple algorithm.</span></span>

### <a name="set-the-distribution-mode-on-a-load-balanced-endpoint-set"></a><span data-ttu-id="a38ec-134">Defina o modo de distribuição em um conjunto de pontos de extremidade com balanceamento de carga</span><span class="sxs-lookup"><span data-stu-id="a38ec-134">Set the Distribution mode on a load balanced endpoint set</span></span>

<span data-ttu-id="a38ec-135">Se os pontos de extremidade forem parte de um conjunto de pontos de extremidade de balanceamento de carga, o modo de distribuição deverá ser definido no conjunto de pontos de extremidade de balanceamento de carga:</span><span class="sxs-lookup"><span data-stu-id="a38ec-135">If endpoints are part of a load balanced endpoint set, the distribution mode must be set on the load balanced endpoint set:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName MyService -LBSetName LBSet1 -Protocol TCP -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 –LoadBalancerDistribution sourceIP
```

### <a name="cloud-service-configuration-to-change-distribution-mode"></a><span data-ttu-id="a38ec-136">Configuração de serviço de nuvem para alterar o modo de distribuição</span><span class="sxs-lookup"><span data-stu-id="a38ec-136">Cloud Service configuration to change distribution mode</span></span>

<span data-ttu-id="a38ec-137">É possível aproveitar o SDK do Azure para .NET 2.5 (a ser lançado em novembro) para atualizar seu serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="a38ec-137">You can leverage the Azure SDK for .NET 2.5 (to be released in November) to update your Cloud Service.</span></span> <span data-ttu-id="a38ec-138">Configurações de ponto de extremidade para serviços de nuvem são feitas na. csdef.</span><span class="sxs-lookup"><span data-stu-id="a38ec-138">Endpoint settings for Cloud Services are made in the .csdef.</span></span> <span data-ttu-id="a38ec-139">Para atualizar o modo de distribuição do balanceador de carga para uma implantação de serviços de nuvem, é necessária uma atualização da implantação.</span><span class="sxs-lookup"><span data-stu-id="a38ec-139">In order to update the load balancer distribution mode for a Cloud Services deployment, a deployment upgrade is required.</span></span>
<span data-ttu-id="a38ec-140">Aqui está um exemplo de alterações .csdef para configurações do ponto de extremidade:</span><span class="sxs-lookup"><span data-stu-id="a38ec-140">Here is an example of .csdef changes for endpoint settings:</span></span>

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

## <a name="api-example"></a><span data-ttu-id="a38ec-141">Exemplo de API</span><span class="sxs-lookup"><span data-stu-id="a38ec-141">API example</span></span>

<span data-ttu-id="a38ec-142">Você pode configurar a distribuição do balanceador de carga usando a API de gerenciamento de serviços.</span><span class="sxs-lookup"><span data-stu-id="a38ec-142">You can configure the load balancer distribution using the service management API.</span></span> <span data-ttu-id="a38ec-143">Certifique-se de adicionar o cabeçalho `x-ms-version` definido como a versão `2014-09-01` ou superior.</span><span class="sxs-lookup"><span data-stu-id="a38ec-143">Make sure to add the `x-ms-version` header is set to version `2014-09-01` or higher.</span></span>

### <a name="update-the-configuration-of-the-specified-load-balanced-set-in-a-deployment"></a><span data-ttu-id="a38ec-144">Atualize a configuração do conjunto de balanceamento de carga especificado em uma implantação</span><span class="sxs-lookup"><span data-stu-id="a38ec-144">Update the configuration of the specified load-balanced set in a deployment</span></span>

#### <a name="request-example"></a><span data-ttu-id="a38ec-145">Exemplo de solicitação</span><span class="sxs-lookup"><span data-stu-id="a38ec-145">Request example</span></span>

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

<span data-ttu-id="a38ec-146">O valor de LoadBalancerDistribution pode ser sourceIP para afinidade de 2 tuplas, sourceIPProtocol para afinidade de 3 tuplas ou nenhum (para nenhuma afinidade.</span><span class="sxs-lookup"><span data-stu-id="a38ec-146">The value of LoadBalancerDistribution can be sourceIP for 2-tuple affinity, sourceIPProtocol for 3-tuple affinity or none (for no affinity.</span></span> <span data-ttu-id="a38ec-147">por exemplo, 5 tuplas)</span><span class="sxs-lookup"><span data-stu-id="a38ec-147">i.e. 5-tuple)</span></span>

#### <a name="response"></a><span data-ttu-id="a38ec-148">Response</span><span class="sxs-lookup"><span data-stu-id="a38ec-148">Response</span></span>

    HTTP/1.1 202 Accepted
    Cache-Control: no-cache
    Content-Length: 0
    Server: 1.0.6198.146 (rd_rdfe_stable.141015-1306) Microsoft-HTTPAPI/2.0
    x-ms-servedbyregion: ussouth2
    x-ms-request-id: 9c7bda3e67c621a6b57096323069f7af
    Date: Thu, 16 Oct 2014 22:49:21 GMT

## <a name="next-steps"></a><span data-ttu-id="a38ec-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a38ec-149">Next Steps</span></span>

[<span data-ttu-id="a38ec-150">Visão geral do balanceador de carga interno</span><span class="sxs-lookup"><span data-stu-id="a38ec-150">Internal load balancer overview</span></span>](load-balancer-internal-overview.md)

[<span data-ttu-id="a38ec-151">Introdução à configuração de um balanceador de carga para a Internet</span><span class="sxs-lookup"><span data-stu-id="a38ec-151">Get started Configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="a38ec-152">Definir configurações de tempo limite de TCP ocioso para o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="a38ec-152">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
