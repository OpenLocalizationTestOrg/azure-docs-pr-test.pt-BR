---
title: Configurar tempo limite de ociosidade do TCP do balanceador de carga | Microsoft Docs
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
ms.openlocfilehash: d040fe6580b8ae777aecc9dd385ed33861530c38
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-tcp-idle-timeout-settings-for-azure-load-balancer"></a><span data-ttu-id="2623a-103">Definir as configurações de tempo limite de ociosidade do TCP para o Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="2623a-103">Configure TCP idle timeout settings for Azure Load Balancer</span></span>

<span data-ttu-id="2623a-104">Em sua configuração padrão, o Azure Load Balancer tem uma configuração de tempo limite de ociosidade de quatro minutos.</span><span class="sxs-lookup"><span data-stu-id="2623a-104">In its default configuration, Azure Load Balancer has an idle timeout setting of 4 minutes.</span></span> <span data-ttu-id="2623a-105">Se um período de inatividade for maior que o valor de tempo limite, não haverá nenhuma garantia de que a sessão TCP ou HTTP seja mantida entre o cliente e o serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="2623a-105">If a period of inactivity is longer than the timeout value, there's no guarantee that the TCP or HTTP session is maintained between the client and your cloud service.</span></span>

<span data-ttu-id="2623a-106">Quando a conexão é fechada, seu aplicativo cliente pode recebe a seguinte mensagem de erro: "A conexão subjacente foi fechada: uma conexão que deveria ser mantida ativa foi fechada pelo servidor."</span><span class="sxs-lookup"><span data-stu-id="2623a-106">When the connection is closed, your client application may receive the following error message: "The underlying connection was closed: A connection that was expected to be kept alive was closed by the server."</span></span>

<span data-ttu-id="2623a-107">Uma prática comum é usar um TCP keep alive.</span><span class="sxs-lookup"><span data-stu-id="2623a-107">A common practice is to use a TCP keep-alive.</span></span> <span data-ttu-id="2623a-108">Essa prática mantém a conexão ativa por um período maior.</span><span class="sxs-lookup"><span data-stu-id="2623a-108">This practice keeps the connection active for a longer period.</span></span> <span data-ttu-id="2623a-109">Para obter mais informações, consulte estes [exemplos do .NET](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx).</span><span class="sxs-lookup"><span data-stu-id="2623a-109">For more information, see these [.NET examples](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx).</span></span> <span data-ttu-id="2623a-110">Com o keep alive habilitado, os pacotes são enviados durante os períodos de inatividade na conexão.</span><span class="sxs-lookup"><span data-stu-id="2623a-110">With keep-alive enabled, packets are sent during periods of inactivity on the connection.</span></span> <span data-ttu-id="2623a-111">Esses pacotes keep alive garantem que o valor de tempo limite de ociosidade nunca será atingido e a conexão será mantida por um longo período.</span><span class="sxs-lookup"><span data-stu-id="2623a-111">These keep-alive packets ensure that the idle timeout value is never reached and the connection is maintained for a long period.</span></span>

<span data-ttu-id="2623a-112">Essa configuração só funciona para conexões de entrada.</span><span class="sxs-lookup"><span data-stu-id="2623a-112">This setting works for inbound connections only.</span></span> <span data-ttu-id="2623a-113">Para evitar a perda da conexão, você deve configurar o TCP keep-alive com um intervalo menor do que a configuração de tempo limite de ociosidade ou aumentar o valor do tempo limite de ociosidade.</span><span class="sxs-lookup"><span data-stu-id="2623a-113">To avoid losing the connection, you must configure the TCP keep-alive with an interval less than the idle timeout setting or increase the idle timeout value.</span></span> <span data-ttu-id="2623a-114">Para dar suporte a esses cenários, adicionamos suporte para um tempo limite de ociosidade configurável.</span><span class="sxs-lookup"><span data-stu-id="2623a-114">To support such scenarios, we've added support for a configurable idle timeout.</span></span> <span data-ttu-id="2623a-115">Agora você pode defini-lo para uma duração entre quatro e 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="2623a-115">You can now set it for a duration of 4 to 30 minutes.</span></span>

<span data-ttu-id="2623a-116">O TCP keep alive funciona bem para cenários em que a vida útil da bateria não é uma restrição.</span><span class="sxs-lookup"><span data-stu-id="2623a-116">TCP keep-alive works well for scenarios where battery life is not a constraint.</span></span> <span data-ttu-id="2623a-117">Não é recomendável para aplicativos móveis.</span><span class="sxs-lookup"><span data-stu-id="2623a-117">It is not recommended for mobile applications.</span></span> <span data-ttu-id="2623a-118">Usar o TCP keep alive em um aplicativo móvel pode consumir a bateria do dispositivo mais rapidamente.</span><span class="sxs-lookup"><span data-stu-id="2623a-118">Using a TCP keep-alive in a mobile application can drain the device battery faster.</span></span>

![Tempo limite de TCP](./media/load-balancer-tcp-idle-timeout/image1.png)

<span data-ttu-id="2623a-120">As seções a seguir descrevem como alterar as configurações de tempo limite de ociosidade em máquinas virtuais e serviços de nuvem.</span><span class="sxs-lookup"><span data-stu-id="2623a-120">The following sections describe how to change idle timeout settings in virtual machines and cloud services.</span></span>

## <a name="configure-the-tcp-timeout-for-your-instance-level-public-ip-to-15-minutes"></a><span data-ttu-id="2623a-121">Configure o tempo limite de TCP para o IP Público em Nível de Instância para 15 minutos</span><span class="sxs-lookup"><span data-stu-id="2623a-121">Configure the TCP timeout for your instance-level public IP to 15 minutes</span></span>

```powershell
Set-AzurePublicIP -PublicIPName webip -VM MyVM -IdleTimeoutInMinutes 15
```

<span data-ttu-id="2623a-122">`IdleTimeoutInMinutes` é opcional.</span><span class="sxs-lookup"><span data-stu-id="2623a-122">`IdleTimeoutInMinutes` is optional.</span></span> <span data-ttu-id="2623a-123">Se não for definido, o tempo limite padrão será 4 minutos.</span><span class="sxs-lookup"><span data-stu-id="2623a-123">If it is not set, the default timeout is 4 minutes.</span></span> <span data-ttu-id="2623a-124">O intervalo de tempo limite aceitável é entre quatro e 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="2623a-124">The acceptable timeout range is 4 to 30 minutes.</span></span>

## <a name="set-the-idle-timeout-when-creating-an-azure-endpoint-on-a-virtual-machine"></a><span data-ttu-id="2623a-125">Defina o tempo limite de ociosidade durante a criação de um ponto de extremidade do Azure em uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="2623a-125">Set the idle timeout when creating an Azure endpoint on a virtual machine</span></span>

<span data-ttu-id="2623a-126">Para alterar a configuração de tempo limite para um ponto de extremidade, use o seguinte:</span><span class="sxs-lookup"><span data-stu-id="2623a-126">To change the timeout setting for an endpoint, use the following:</span></span>

```powershell
Get-AzureVM -ServiceName "mySvc" -Name "MyVM1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 8080 -IdleTimeoutInMinutes 15| Update-AzureVM
```

<span data-ttu-id="2623a-127">Para recuperar sua configuração de tempo limite de ociosidade, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="2623a-127">To retrieve your idle timeout configuration, use the following command:</span></span>

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

## <a name="set-the-tcp-timeout-on-a-load-balanced-endpoint-set"></a><span data-ttu-id="2623a-128">Defina o tempo limite do TCP em um conjunto do ponto de extremidade com balanceamento de carga</span><span class="sxs-lookup"><span data-stu-id="2623a-128">Set the TCP timeout on a load-balanced endpoint set</span></span>

<span data-ttu-id="2623a-129">Se os pontos de extremidade forem parte de um conjunto do ponto de extremidade com balanceamento de carga, o tempo limite do TCP deverá ser definido no conjunto de pontos de extremidade com balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="2623a-129">If endpoints are part of a load-balanced endpoint set, the TCP timeout must be set on the load-balanced endpoint set.</span></span> <span data-ttu-id="2623a-130">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="2623a-130">For example:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName "MyService" -LBSetName "LBSet1" -Protocol tcp -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 -IdleTimeoutInMinutes 15
```

## <a name="change-timeout-settings-for-cloud-services"></a><span data-ttu-id="2623a-131">Alterar as configurações de tempo limite para serviços de nuvem</span><span class="sxs-lookup"><span data-stu-id="2623a-131">Change timeout settings for cloud services</span></span>

<span data-ttu-id="2623a-132">É possível usar o SDK do Azure para atualizar seu serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="2623a-132">You can use the Azure SDK to update your cloud service.</span></span> <span data-ttu-id="2623a-133">Você pode fazer configurações de ponto de extremidade para serviços de nuvem no arquivo .csdef.</span><span class="sxs-lookup"><span data-stu-id="2623a-133">You make endpoint settings for cloud services in the .csdef file.</span></span> <span data-ttu-id="2623a-134">A atualização do tempo limite do TCP para a implantação de um serviço de nuvem exige uma atualização da implantação.</span><span class="sxs-lookup"><span data-stu-id="2623a-134">Updating the TCP timeout for deployment of a cloud service requires a deployment upgrade.</span></span> <span data-ttu-id="2623a-135">Uma exceção é se o tempo limite do TCP é especificado somente para um IP público.</span><span class="sxs-lookup"><span data-stu-id="2623a-135">An exception is if the TCP timeout is specified only for a public IP.</span></span> <span data-ttu-id="2623a-136">As configurações de IP público estão no arquivo .cscfg e podem ser atualizadas por intermédio da atualização e do upgrade da implantação.</span><span class="sxs-lookup"><span data-stu-id="2623a-136">Public IP settings are in the .cscfg file, and you can update them through deployment update and upgrade.</span></span>

<span data-ttu-id="2623a-137">As alterações do .csdef para as configurações do ponto de extremidade são:</span><span class="sxs-lookup"><span data-stu-id="2623a-137">The .csdef changes for endpoint settings are:</span></span>

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" idleTimeoutInMinutes="tcp-timeout" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="2623a-138">As alterações no .cscfg para a configuração de tempo limite em IPs públicos são:</span><span class="sxs-lookup"><span data-stu-id="2623a-138">The .cscfg changes for the timeout setting on public IPs are:</span></span>

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

## <a name="rest-api-example"></a><span data-ttu-id="2623a-139">Exemplo de API REST</span><span class="sxs-lookup"><span data-stu-id="2623a-139">REST API example</span></span>

<span data-ttu-id="2623a-140">Você pode configurar o tempo limite de ociosidade de TCP usando a API de Gerenciamento de Serviços.</span><span class="sxs-lookup"><span data-stu-id="2623a-140">You can configure the TCP idle timeout by using the service management API.</span></span> <span data-ttu-id="2623a-141">Certifique-se de que o cabeçalho `x-ms-version` esteja definido como a versão `2014-06-01` ou superior.</span><span class="sxs-lookup"><span data-stu-id="2623a-141">Make sure that the `x-ms-version` header is set to version `2014-06-01` or later.</span></span> <span data-ttu-id="2623a-142">Atualize a configuração dos pontos de extremidade de entrada com balanceamento de carga especificado em todas as máquinas virtuais em uma implantação.</span><span class="sxs-lookup"><span data-stu-id="2623a-142">Update the configuration of the specified load-balanced input endpoints on all virtual machines in a deployment.</span></span>

### <a name="request"></a><span data-ttu-id="2623a-143">Solicitação</span><span class="sxs-lookup"><span data-stu-id="2623a-143">Request</span></span>

    POST https://management.core.windows.net/<subscription-id>/services/hostedservices/<cloudservice-name>/deployments/<deployment-name>

### <a name="response"></a><span data-ttu-id="2623a-144">Response</span><span class="sxs-lookup"><span data-stu-id="2623a-144">Response</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="2623a-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2623a-145">Next steps</span></span>

[<span data-ttu-id="2623a-146">Visão geral do balanceador de carga interno</span><span class="sxs-lookup"><span data-stu-id="2623a-146">Internal load balancer overview</span></span>](load-balancer-internal-overview.md)

[<span data-ttu-id="2623a-147">Introdução à configuração de um balanceador de carga para a Internet</span><span class="sxs-lookup"><span data-stu-id="2623a-147">Get started configuring an Internet-facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="2623a-148">Configurar um modo de distribuição do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="2623a-148">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)
