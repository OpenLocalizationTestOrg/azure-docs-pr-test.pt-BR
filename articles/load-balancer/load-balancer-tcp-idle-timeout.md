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
# <a name="configure-tcp-idle-timeout-settings-for-azure-load-balancer"></a><span data-ttu-id="ce451-103">Definir as configurações de tempo limite de ociosidade do TCP para o Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="ce451-103">Configure TCP idle timeout settings for Azure Load Balancer</span></span>

<span data-ttu-id="ce451-104">Em sua configuração padrão, o Azure Load Balancer tem uma configuração de tempo limite de ociosidade de quatro minutos.</span><span class="sxs-lookup"><span data-stu-id="ce451-104">In its default configuration, Azure Load Balancer has an idle timeout setting of 4 minutes.</span></span> <span data-ttu-id="ce451-105">Se um período de inatividade é maior que o valor de tempo limite de hello, não há nenhuma garantia de que Olá TCP ou sessão HTTP é mantido entre cliente hello e seu serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="ce451-105">If a period of inactivity is longer than hello timeout value, there's no guarantee that hello TCP or HTTP session is maintained between hello client and your cloud service.</span></span>

<span data-ttu-id="ce451-106">Quando a conexão de saudação for fechada, seu aplicativo cliente pode receber Olá a seguinte mensagem de erro: "hello subjacente a conexão foi fechada: uma conexão que deveria toobe mantida ativa foi fechada pelo servidor de saudação."</span><span class="sxs-lookup"><span data-stu-id="ce451-106">When hello connection is closed, your client application may receive hello following error message: "hello underlying connection was closed: A connection that was expected toobe kept alive was closed by hello server."</span></span>

<span data-ttu-id="ce451-107">Uma prática comum é toouse um TCP keep-alive.</span><span class="sxs-lookup"><span data-stu-id="ce451-107">A common practice is toouse a TCP keep-alive.</span></span> <span data-ttu-id="ce451-108">Essa prática mantém a conexão Olá ativo por um período maior.</span><span class="sxs-lookup"><span data-stu-id="ce451-108">This practice keeps hello connection active for a longer period.</span></span> <span data-ttu-id="ce451-109">Para obter mais informações, consulte estes [exemplos do .NET](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx).</span><span class="sxs-lookup"><span data-stu-id="ce451-109">For more information, see these [.NET examples](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx).</span></span> <span data-ttu-id="ce451-110">Com keep-alive habilitado, os pacotes são enviados durante períodos de inatividade da conexão hello.</span><span class="sxs-lookup"><span data-stu-id="ce451-110">With keep-alive enabled, packets are sent during periods of inactivity on hello connection.</span></span> <span data-ttu-id="ce451-111">Esses pacotes keep-alive Certifique-se de que o valor de tempo limite de ociosidade Olá nunca é alcançado e conexão Olá é mantida por um longo período.</span><span class="sxs-lookup"><span data-stu-id="ce451-111">These keep-alive packets ensure that hello idle timeout value is never reached and hello connection is maintained for a long period.</span></span>

<span data-ttu-id="ce451-112">Essa configuração só funciona para conexões de entrada.</span><span class="sxs-lookup"><span data-stu-id="ce451-112">This setting works for inbound connections only.</span></span> <span data-ttu-id="ce451-113">tooavoid perder a conexão de hello, configure Olá TCP keep-alive com um intervalo menor do que Olá tempo limite de ociosidade configuração ou aumente Olá tempo limite de ociosidade valor.</span><span class="sxs-lookup"><span data-stu-id="ce451-113">tooavoid losing hello connection, you must configure hello TCP keep-alive with an interval less than hello idle timeout setting or increase hello idle timeout value.</span></span> <span data-ttu-id="ce451-114">toosupport nesses cenários, adicionamos suporte para um tempo limite de ociosidade configurável.</span><span class="sxs-lookup"><span data-stu-id="ce451-114">toosupport such scenarios, we've added support for a configurable idle timeout.</span></span> <span data-ttu-id="ce451-115">Agora você pode defini-lo por um período de 4 minutos too30.</span><span class="sxs-lookup"><span data-stu-id="ce451-115">You can now set it for a duration of 4 too30 minutes.</span></span>

<span data-ttu-id="ce451-116">O TCP keep alive funciona bem para cenários em que a vida útil da bateria não é uma restrição.</span><span class="sxs-lookup"><span data-stu-id="ce451-116">TCP keep-alive works well for scenarios where battery life is not a constraint.</span></span> <span data-ttu-id="ce451-117">Não é recomendável para aplicativos móveis.</span><span class="sxs-lookup"><span data-stu-id="ce451-117">It is not recommended for mobile applications.</span></span> <span data-ttu-id="ce451-118">Usando um TCP keep-alive em um aplicativo móvel pode drenar bateria do dispositivo hello mais rapidamente.</span><span class="sxs-lookup"><span data-stu-id="ce451-118">Using a TCP keep-alive in a mobile application can drain hello device battery faster.</span></span>

![Tempo limite de TCP](./media/load-balancer-tcp-idle-timeout/image1.png)

<span data-ttu-id="ce451-120">Olá seções a seguir descreve como toochange ocioso configurações de tempo limite em máquinas virtuais e serviços de nuvem.</span><span class="sxs-lookup"><span data-stu-id="ce451-120">hello following sections describe how toochange idle timeout settings in virtual machines and cloud services.</span></span>

## <a name="configure-hello-tcp-timeout-for-your-instance-level-public-ip-too15-minutes"></a><span data-ttu-id="ce451-121">Configurar o tempo limite TCP de saudação para seu minutos do nível de instância públicos IP too15</span><span class="sxs-lookup"><span data-stu-id="ce451-121">Configure hello TCP timeout for your instance-level public IP too15 minutes</span></span>

```powershell
Set-AzurePublicIP -PublicIPName webip -VM MyVM -IdleTimeoutInMinutes 15
```

<span data-ttu-id="ce451-122">`IdleTimeoutInMinutes` é opcional.</span><span class="sxs-lookup"><span data-stu-id="ce451-122">`IdleTimeoutInMinutes` is optional.</span></span> <span data-ttu-id="ce451-123">Se não for definida, o tempo limite padrão de saudação é 4 minutos.</span><span class="sxs-lookup"><span data-stu-id="ce451-123">If it is not set, hello default timeout is 4 minutes.</span></span> <span data-ttu-id="ce451-124">intervalo de tempo limite aceitável de saudação é 4 too30 minutos.</span><span class="sxs-lookup"><span data-stu-id="ce451-124">hello acceptable timeout range is 4 too30 minutes.</span></span>

## <a name="set-hello-idle-timeout-when-creating-an-azure-endpoint-on-a-virtual-machine"></a><span data-ttu-id="ce451-125">Definir tempo limite de ociosidade Olá durante a criação de um ponto de extremidade do Azure em uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="ce451-125">Set hello idle timeout when creating an Azure endpoint on a virtual machine</span></span>

<span data-ttu-id="ce451-126">toochange Olá tempo limite de configuração para um ponto de extremidade, use Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="ce451-126">toochange hello timeout setting for an endpoint, use hello following:</span></span>

```powershell
Get-AzureVM -ServiceName "mySvc" -Name "MyVM1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 8080 -IdleTimeoutInMinutes 15| Update-AzureVM
```

<span data-ttu-id="ce451-127">tooretrieve sua configuração de tempo limite de ociosidade, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="ce451-127">tooretrieve your idle timeout configuration, use hello following command:</span></span>

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

## <a name="set-hello-tcp-timeout-on-a-load-balanced-endpoint-set"></a><span data-ttu-id="ce451-128">Definir tempo limite TCP de saudação em um conjunto de ponto de extremidade com balanceamento de carga</span><span class="sxs-lookup"><span data-stu-id="ce451-128">Set hello TCP timeout on a load-balanced endpoint set</span></span>

<span data-ttu-id="ce451-129">Se os pontos de extremidade são parte de um conjunto de ponto de extremidade com balanceamento de carga, tempo limite TCP de saudação deve ser definido no conjunto de ponto de extremidade com balanceamento de carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce451-129">If endpoints are part of a load-balanced endpoint set, hello TCP timeout must be set on hello load-balanced endpoint set.</span></span> <span data-ttu-id="ce451-130">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="ce451-130">For example:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName "MyService" -LBSetName "LBSet1" -Protocol tcp -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 -IdleTimeoutInMinutes 15
```

## <a name="change-timeout-settings-for-cloud-services"></a><span data-ttu-id="ce451-131">Alterar as configurações de tempo limite para serviços de nuvem</span><span class="sxs-lookup"><span data-stu-id="ce451-131">Change timeout settings for cloud services</span></span>

<span data-ttu-id="ce451-132">Você pode usar o hello Azure SDK tooupdate seu serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="ce451-132">You can use hello Azure SDK tooupdate your cloud service.</span></span> <span data-ttu-id="ce451-133">Você pode fazer configurações de ponto de extremidade para serviços de nuvem no arquivo. csdef de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce451-133">You make endpoint settings for cloud services in hello .csdef file.</span></span> <span data-ttu-id="ce451-134">Atualizar o tempo limite TCP de saudação para implantação de um serviço de nuvem requer uma atualização de implantação.</span><span class="sxs-lookup"><span data-stu-id="ce451-134">Updating hello TCP timeout for deployment of a cloud service requires a deployment upgrade.</span></span> <span data-ttu-id="ce451-135">Uma exceção é se o tempo limite TCP de saudação for especificado apenas para um IP público.</span><span class="sxs-lookup"><span data-stu-id="ce451-135">An exception is if hello TCP timeout is specified only for a public IP.</span></span> <span data-ttu-id="ce451-136">Configurações de IP público estão no arquivo. cscfg de saudação e pode atualizá-los por meio de atualização e a atualização de implantação.</span><span class="sxs-lookup"><span data-stu-id="ce451-136">Public IP settings are in hello .cscfg file, and you can update them through deployment update and upgrade.</span></span>

<span data-ttu-id="ce451-137">Olá. csdef alterações para as configurações de ponto de extremidade são:</span><span class="sxs-lookup"><span data-stu-id="ce451-137">hello .csdef changes for endpoint settings are:</span></span>

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" idleTimeoutInMinutes="tcp-timeout" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="ce451-138">Olá. cscfg alterações de configuração de tempo limite de saudação em IPs públicos são:</span><span class="sxs-lookup"><span data-stu-id="ce451-138">hello .cscfg changes for hello timeout setting on public IPs are:</span></span>

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

## <a name="rest-api-example"></a><span data-ttu-id="ce451-139">Exemplo de API REST</span><span class="sxs-lookup"><span data-stu-id="ce451-139">REST API example</span></span>

<span data-ttu-id="ce451-140">Você pode configurar o tempo limite de ociosidade TCP hello usando a API de gerenciamento do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce451-140">You can configure hello TCP idle timeout by using hello service management API.</span></span> <span data-ttu-id="ce451-141">Certifique-se de que Olá `x-ms-version` cabeçalho é definido tooversion `2014-06-01` ou posterior.</span><span class="sxs-lookup"><span data-stu-id="ce451-141">Make sure that hello `x-ms-version` header is set tooversion `2014-06-01` or later.</span></span> <span data-ttu-id="ce451-142">Configuração de saudação de atualização de saudação especificado pontos de extremidade de entrada com balanceamento de carga em todas as máquinas virtuais em uma implantação.</span><span class="sxs-lookup"><span data-stu-id="ce451-142">Update hello configuration of hello specified load-balanced input endpoints on all virtual machines in a deployment.</span></span>

### <a name="request"></a><span data-ttu-id="ce451-143">Solicitação</span><span class="sxs-lookup"><span data-stu-id="ce451-143">Request</span></span>

    POST https://management.core.windows.net/<subscription-id>/services/hostedservices/<cloudservice-name>/deployments/<deployment-name>

### <a name="response"></a><span data-ttu-id="ce451-144">Response</span><span class="sxs-lookup"><span data-stu-id="ce451-144">Response</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="ce451-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ce451-145">Next steps</span></span>

[<span data-ttu-id="ce451-146">Visão geral do balanceador de carga interno</span><span class="sxs-lookup"><span data-stu-id="ce451-146">Internal load balancer overview</span></span>](load-balancer-internal-overview.md)

[<span data-ttu-id="ce451-147">Introdução à configuração de um balanceador de carga para a Internet</span><span class="sxs-lookup"><span data-stu-id="ce451-147">Get started configuring an Internet-facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="ce451-148">Configurar um modo de distribuição do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="ce451-148">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)
