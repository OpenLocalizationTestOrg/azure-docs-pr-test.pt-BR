---
title: Proxy reverso do Azure Service Fabric | Microsoft Docs
description: "Usar o proxy reverso do Service Fabric para comunicação com microsserviços de dentro e fora do cluster."
services: service-fabric
documentationcenter: .net
author: BharatNarasimman
manager: timlt
editor: vturecek
ms.assetid: 47f5c1c1-8fc8-4b80-a081-bc308f3655d3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 08/08/2017
ms.author: bharatn
ms.openlocfilehash: 7897458e9e4a0bbe185bd3f7b4c133c1b26769f9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="reverse-proxy-in-azure-service-fabric"></a><span data-ttu-id="d91c4-103">Proxy reverso no Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d91c4-103">Reverse proxy in Azure Service Fabric</span></span>
<span data-ttu-id="d91c4-104">O proxy reverso que está incorporado ao Azure Service Fabric endereça microsserviços no cluster do Service Fabric que expõe pontos de extremidade HTTP.</span><span class="sxs-lookup"><span data-stu-id="d91c4-104">The reverse proxy that's built into Azure Service Fabric addresses microservices in the Service Fabric cluster that exposes HTTP endpoints.</span></span>

## <a name="microservices-communication-model"></a><span data-ttu-id="d91c4-105">Modelo de comunicação de microsserviços</span><span class="sxs-lookup"><span data-stu-id="d91c4-105">Microservices communication model</span></span>
<span data-ttu-id="d91c4-106">Normalmente, os microsserviços no Service Fabric são executados em um subconjunto de máquinas virtuais no cluster e podem ser movidos de uma máquina virtual para outra por vários motivos.</span><span class="sxs-lookup"><span data-stu-id="d91c4-106">Microservices in Service Fabric typically run on a subset of virtual machines in the cluster and can move from one virtual machine to another for various reasons.</span></span> <span data-ttu-id="d91c4-107">Assim, os pontos de extremidade para microsserviços podem ser alterados dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="d91c4-107">So, the endpoints for microservices can change dynamically.</span></span> <span data-ttu-id="d91c4-108">O padrão típico para se comunicar com o microsserviço é o loop de resolução a seguir:</span><span class="sxs-lookup"><span data-stu-id="d91c4-108">The typical pattern to communicate to the microservice is the following resolve loop:</span></span>

1. <span data-ttu-id="d91c4-109">Resolva a localização do serviço inicialmente por meio do serviço de nomenclatura.</span><span class="sxs-lookup"><span data-stu-id="d91c4-109">Resolve the service location initially through the naming service.</span></span>
2. <span data-ttu-id="d91c4-110">Conecte-se ao serviço.</span><span class="sxs-lookup"><span data-stu-id="d91c4-110">Connect to the service.</span></span>
3. <span data-ttu-id="d91c4-111">Determine a causa de falhas de conexão e resolva novamente a localização do serviço quando necessário.</span><span class="sxs-lookup"><span data-stu-id="d91c4-111">Determine the cause of connection failures, and resolve the service location again when necessary.</span></span>

<span data-ttu-id="d91c4-112">Esse processo geralmente envolve a quebra automática de bibliotecas de comunicação de cliente em um loop de repetição que implementa as políticas de repetição e resolução de serviço.</span><span class="sxs-lookup"><span data-stu-id="d91c4-112">This process generally involves wrapping client-side communication libraries in a retry loop that implements the service resolution and retry policies.</span></span>
<span data-ttu-id="d91c4-113">Para obter mais informações, consulte [Conectar-se a serviços e se comunicar com eles](service-fabric-connect-and-communicate-with-services.md).</span><span class="sxs-lookup"><span data-stu-id="d91c4-113">For more information, see [Connect and communicate with services](service-fabric-connect-and-communicate-with-services.md).</span></span>

### <a name="communicating-by-using-the-reverse-proxy"></a><span data-ttu-id="d91c4-114">Comunicar-se usando o proxy reverso</span><span class="sxs-lookup"><span data-stu-id="d91c4-114">Communicating by using the reverse proxy</span></span>
<span data-ttu-id="d91c4-115">O proxy reverso do Service Fabric é executado em todos os nós no cluster.</span><span class="sxs-lookup"><span data-stu-id="d91c4-115">The reverse proxy in Service Fabric runs on all the nodes in the cluster.</span></span> <span data-ttu-id="d91c4-116">Ele executa o processo de resolução de todo o serviço em nome do cliente e, em seguida, encaminha a solicitação do cliente.</span><span class="sxs-lookup"><span data-stu-id="d91c4-116">It performs the entire service resolution process on a client's behalf and then forwards the client request.</span></span> <span data-ttu-id="d91c4-117">Portanto, clientes em execução no cluster podem simplesmente usar bibliotecas de comunicação HTTP do lado do cliente para se comunicar com o serviço de destino por meio do proxy reverso executado localmente no mesmo nó.</span><span class="sxs-lookup"><span data-stu-id="d91c4-117">So, clients that run on the cluster can use any client-side HTTP communication libraries to talk to the target service by using the reverse proxy that runs locally on the same node.</span></span>

![Comunicação interna][1]

## <a name="reaching-microservices-from-outside-the-cluster"></a><span data-ttu-id="d91c4-119">Alcançar microsserviços de fora do cluster</span><span class="sxs-lookup"><span data-stu-id="d91c4-119">Reaching microservices from outside the cluster</span></span>
<span data-ttu-id="d91c4-120">O modelo de comunicação externa padrão para microsserviços é um modelo de aceitação em que cada serviço não pode ser acessado diretamente de clientes externos.</span><span class="sxs-lookup"><span data-stu-id="d91c4-120">The default external communication model for microservices is an opt-in model where each service cannot be accessed directly from external clients.</span></span> <span data-ttu-id="d91c4-121">O [Azure Load Balancer](../load-balancer/load-balancer-overview.md), que é um limite de rede entre microsserviços e clientes externos, executa a conversão de endereços de rede e encaminha as solicitações externas para pontos de extremidade de IP:porta internos.</span><span class="sxs-lookup"><span data-stu-id="d91c4-121">[Azure Load Balancer](../load-balancer/load-balancer-overview.md), which is a network boundary between microservices and external clients, performs network address translation and forwards external requests to internal IP:port endpoints.</span></span> <span data-ttu-id="d91c4-122">Para tornar o ponto de extremidade do microsserviço diretamente acessível para clientes externos, você deve primeiro configurar o Load Balancer para encaminhar o tráfego para cada porta usada pelo serviço no cluster.</span><span class="sxs-lookup"><span data-stu-id="d91c4-122">To make a microservice's endpoint directly accessible to external clients, you must first configure Load Balancer to forward traffic to each port that the service uses in the cluster.</span></span> <span data-ttu-id="d91c4-123">Além disso, a maioria dos microsserviços, especialmente microsserviços com estado, não estão em todos os nós do cluster.</span><span class="sxs-lookup"><span data-stu-id="d91c4-123">Furthermore, most microservices, especially stateful microservices, don't live on all nodes of the cluster.</span></span> <span data-ttu-id="d91c4-124">Os microsserviços podem mover-se entre os nós no failover.</span><span class="sxs-lookup"><span data-stu-id="d91c4-124">The microservices can move between nodes on failover.</span></span> <span data-ttu-id="d91c4-125">Nesses casos, o Load Balancer não pode determinar efetivamente o local do nó de destino das réplicas para o qual encaminhar tráfego.</span><span class="sxs-lookup"><span data-stu-id="d91c4-125">In such cases, Load Balancer cannot effectively determine the location of the target node of the replicas to which it should forward traffic.</span></span>

### <a name="reaching-microservices-via-the-reverse-proxy-from-outside-the-cluster"></a><span data-ttu-id="d91c4-126">Acessar os microsserviços por meio do proxy reverso do Service Fabric de fora do cluster</span><span class="sxs-lookup"><span data-stu-id="d91c4-126">Reaching microservices via the reverse proxy from outside the cluster</span></span>
<span data-ttu-id="d91c4-127">Em vez de configurar a porta de um serviço individual no Load Balancer, você pode configurar apenas a porta do proxy reverso no Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="d91c4-127">Instead of configuring the port of an individual service in Load Balancer, you can configure just the port of the reverse proxy in Load Balancer.</span></span> <span data-ttu-id="d91c4-128">Isso permite que clientes fora do cluster alcancem serviços dentro do cluster por meio do proxy reverso sem configurações adicionais.</span><span class="sxs-lookup"><span data-stu-id="d91c4-128">This configuration lets clients outside the cluster reach services inside the cluster by using the reverse proxy without additional configuration.</span></span>

![Comunicação externa][0]

> [!WARNING]
> <span data-ttu-id="d91c4-130">Quando você configura a porta do proxy reverso no Load Balancer, todos os microsserviços no cluster que expõem um ponto de extremidade HTTP se tornam endereçáveis da parte externa do cluster.</span><span class="sxs-lookup"><span data-stu-id="d91c4-130">When you configure the reverse proxy's port in Load Balancer, all microservices in the cluster that expose an HTTP endpoint are addressable from outside the cluster.</span></span>
>
>


## <a name="uri-format-for-addressing-services-by-using-the-reverse-proxy"></a><span data-ttu-id="d91c4-131">Formato de URI para endereçamento de serviços por meio do proxy reverso</span><span class="sxs-lookup"><span data-stu-id="d91c4-131">URI format for addressing services by using the reverse proxy</span></span>
<span data-ttu-id="d91c4-132">O proxy reverso usa um formato de URI (Uniform Resource Identifier) específico para identificar a partição de serviço para a qual a solicitação de entrada deve ser encaminhada:</span><span class="sxs-lookup"><span data-stu-id="d91c4-132">The reverse proxy uses a specific uniform resource identifier (URI) format to identify the service partition to which the incoming request should be forwarded:</span></span>

```
http(s)://<Cluster FQDN | internal IP>:Port/<ServiceInstanceName>/<Suffix path>?PartitionKey=<key>&PartitionKind=<partitionkind>&ListenerName=<listenerName>&TargetReplicaSelector=<targetReplicaSelector>&Timeout=<timeout_in_seconds>
```

* <span data-ttu-id="d91c4-133">**http (s):** o proxy inverso pode ser configurado para aceitar o tráfego HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d91c4-133">**http(s):** The reverse proxy can be configured to accept HTTP or HTTPS traffic.</span></span> <span data-ttu-id="d91c4-134">Para o encaminhamento HTTPS, consulte [Conectar-se a um serviço seguro com o proxy reverso](service-fabric-reverseproxy-configure-secure-communication.md) após a configuração do proxy reverso para escutar o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d91c4-134">For HTTPS forwarding, refer to [Connect to a secure service with the reverse proxy](service-fabric-reverseproxy-configure-secure-communication.md) once you have reverse proxy setup to listen on HTTPS.</span></span>
* <span data-ttu-id="d91c4-135">**FQDN (nome de domínio totalmente qualificado) do cluster | IP interno:** para clientes externos, o proxy reverso pode ser configurado para que seja acessível por meio do domínio do cluster, por exemplo, mycluster.eastus.cloudapp.azure.com. Por padrão, o proxy reverso é executado em todos os nós.</span><span class="sxs-lookup"><span data-stu-id="d91c4-135">**Cluster fully qualified domain name (FQDN) | internal IP:** For external clients, you can configure the reverse proxy so that it is reachable through the cluster domain, such as mycluster.eastus.cloudapp.azure.com. By default, the reverse proxy runs on every node.</span></span> <span data-ttu-id="d91c4-136">Para o tráfego interno, o proxy reverso pode ser alcançado no localhost ou em qualquer IP de nó interno (por exemplo, 10.0.0.1).</span><span class="sxs-lookup"><span data-stu-id="d91c4-136">For internal traffic, the reverse proxy can be reached on localhost or on any internal node IP, such as 10.0.0.1.</span></span>
* <span data-ttu-id="d91c4-137">**Porta:** essa é a porta, como 19081, que foi especificada para o proxy reverso.</span><span class="sxs-lookup"><span data-stu-id="d91c4-137">**Port:** This is the port, such as 19081, that has been specified for the reverse proxy.</span></span>
* <span data-ttu-id="d91c4-138">**ServiceInstanceName:** esse é o nome totalmente qualificado da instância de serviço implantado que você está tentando alcançar sem o esquema "fabric:/".</span><span class="sxs-lookup"><span data-stu-id="d91c4-138">**ServiceInstanceName:** This is the fully-qualified name of the deployed service instance that you are trying to reach without the "fabric:/" scheme.</span></span> <span data-ttu-id="d91c4-139">Por exemplo, para alcançar o serviço *fabric:/myapp/myservice/*, você usaria *myapp/myservice*.</span><span class="sxs-lookup"><span data-stu-id="d91c4-139">For example, to reach the *fabric:/myapp/myservice/* service, you would use *myapp/myservice*.</span></span>

    <span data-ttu-id="d91c4-140">O nome da instância de serviço diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="d91c4-140">The service instance name is case-sensitive.</span></span> <span data-ttu-id="d91c4-141">O uso de maiúsculas e minúsculas diferentes no nome da instância de serviço da URL causa uma falha das solicitações com 404 (Não Encontrado).</span><span class="sxs-lookup"><span data-stu-id="d91c4-141">Using a different casing for the service instance name in the URL causes the requests to fail with 404 (Not Found).</span></span>
* <span data-ttu-id="d91c4-142">**Caminho de sufixo:** esse é o caminho de URL real, por exemplo, *myapi/values/add/3*, para o serviço ao qual você deseja se conectar.</span><span class="sxs-lookup"><span data-stu-id="d91c4-142">**Suffix path:** This is the actual URL path, such as *myapi/values/add/3*, for the service that you want to connect to.</span></span>
* <span data-ttu-id="d91c4-143">**PartitionKey:** para um serviço particionado, esta é a chave de partição computada da partição que você deseja alcançar.</span><span class="sxs-lookup"><span data-stu-id="d91c4-143">**PartitionKey:** For a partitioned service, this is the computed partition key of the partition that you want to reach.</span></span> <span data-ttu-id="d91c4-144">Observe que isso *não* é o GUID da ID da partição.</span><span class="sxs-lookup"><span data-stu-id="d91c4-144">Note that this is *not* the partition ID GUID.</span></span> <span data-ttu-id="d91c4-145">Esse parâmetro não é necessário para serviços usando o esquema de partição de singleton.</span><span class="sxs-lookup"><span data-stu-id="d91c4-145">This parameter is not required for services that use the singleton partition scheme.</span></span>
* <span data-ttu-id="d91c4-146">**PartitionKind:** o esquema de partição de serviço.</span><span class="sxs-lookup"><span data-stu-id="d91c4-146">**PartitionKind:** This is the service partition scheme.</span></span> <span data-ttu-id="d91c4-147">Isso pode ser 'Int64Range' ou 'Named'.</span><span class="sxs-lookup"><span data-stu-id="d91c4-147">This can be 'Int64Range' or 'Named'.</span></span> <span data-ttu-id="d91c4-148">Esse parâmetro não é necessário para serviços usando o esquema de partição de singleton.</span><span class="sxs-lookup"><span data-stu-id="d91c4-148">This parameter is not required for services that use the singleton partition scheme.</span></span>
* <span data-ttu-id="d91c4-149">**ListenerName** Os pontos de extremidade do serviço estão no formato {"Endpoints":{"Listener1":"Endpoint1","Listener2":"Endpoint2" ...}}.</span><span class="sxs-lookup"><span data-stu-id="d91c4-149">**ListenerName** The endpoints from the service are of the form {"Endpoints":{"Listener1":"Endpoint1","Listener2":"Endpoint2" ...}}.</span></span> <span data-ttu-id="d91c4-150">Quando o serviço expõe vários pontos de extremidade, isso identifica o ponto de extremidade ao qual solicitação do cliente deve ser encaminhada.</span><span class="sxs-lookup"><span data-stu-id="d91c4-150">When the service exposes multiple endpoints, this identifies the endpoint that the client request should be forwarded to.</span></span> <span data-ttu-id="d91c4-151">Isso poderá ser omitido se o serviço tiver somente um ouvinte.</span><span class="sxs-lookup"><span data-stu-id="d91c4-151">This can be omitted if the service has only one listener.</span></span>
* <span data-ttu-id="d91c4-152">**TargetReplicaSelector** Especifica como a réplica de destino ou a instância deve ser selecionada.</span><span class="sxs-lookup"><span data-stu-id="d91c4-152">**TargetReplicaSelector** This specifies how the target replica or instance should be selected.</span></span>
  * <span data-ttu-id="d91c4-153">Quando o serviço de destino tem monitoração de estado, TargetReplicaSelector pode ser um dos seguintes: 'PrimaryReplica', 'RandomSecondaryReplica' ou 'RandomReplica'.</span><span class="sxs-lookup"><span data-stu-id="d91c4-153">When the target service is stateful, the TargetReplicaSelector can be one of the following:  'PrimaryReplica', 'RandomSecondaryReplica', or 'RandomReplica'.</span></span> <span data-ttu-id="d91c4-154">Quando esse parâmetro não é especificado, o padrão é 'PrimaryReplica'.</span><span class="sxs-lookup"><span data-stu-id="d91c4-154">When this parameter is not specified, the default is 'PrimaryReplica'.</span></span>
  * <span data-ttu-id="d91c4-155">Quando o serviço de destino não tem monitoração de estado, o proxy reverso escolhe uma instância aleatória da partição de serviço para encaminhar a solicitação a ela.</span><span class="sxs-lookup"><span data-stu-id="d91c4-155">When the target service is stateless, reverse proxy picks a random instance of the service partition to forward the request to.</span></span>
* <span data-ttu-id="d91c4-156">**Tempo limite:** especifica o tempo limite da solicitação HTTP criada pelo proxy inverso para o serviço em nome da solicitação do cliente.</span><span class="sxs-lookup"><span data-stu-id="d91c4-156">**Timeout:**  This specifies the timeout for the HTTP request created by the reverse proxy to the service on behalf of the client request.</span></span> <span data-ttu-id="d91c4-157">O valor padrão é de 60 segundos.</span><span class="sxs-lookup"><span data-stu-id="d91c4-157">The default value is 60 seconds.</span></span> <span data-ttu-id="d91c4-158">Este é um parâmetro opcional.</span><span class="sxs-lookup"><span data-stu-id="d91c4-158">This is an optional parameter.</span></span>

### <a name="example-usage"></a><span data-ttu-id="d91c4-159">Exemplo de uso</span><span class="sxs-lookup"><span data-stu-id="d91c4-159">Example usage</span></span>
<span data-ttu-id="d91c4-160">Por exemplo, vamos pegar o serviço *fabric:/MyApp/MyService* que abre um ouvinte HTTP na URL a seguir:</span><span class="sxs-lookup"><span data-stu-id="d91c4-160">As an example, let's take the *fabric:/MyApp/MyService* service that opens an HTTP listener on the following URL:</span></span>

```
http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/
```

<span data-ttu-id="d91c4-161">A seguir estão os recursos para o serviço:</span><span class="sxs-lookup"><span data-stu-id="d91c4-161">Following are the resources for the service:</span></span>

* `/index.html`
* `/api/users/<userId>`

<span data-ttu-id="d91c4-162">Se o serviço usar o esquema de particionamento de singleton, os parâmetros de cadeia de consulta *PartitionKey* e *PartitionKind* não serão necessários e o serviço poderá ser acessado pelo uso do gateway da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="d91c4-162">If the service uses the singleton partitioning scheme, the *PartitionKey* and *PartitionKind* query string parameters are not required, and the service can be reached by using the gateway as:</span></span>

* <span data-ttu-id="d91c4-163">Externamente: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService`</span><span class="sxs-lookup"><span data-stu-id="d91c4-163">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService`</span></span>
* <span data-ttu-id="d91c4-164">Internamente: `http://localhost:19081/MyApp/MyService`</span><span class="sxs-lookup"><span data-stu-id="d91c4-164">Internally: `http://localhost:19081/MyApp/MyService`</span></span>

<span data-ttu-id="d91c4-165">Se o serviço usar o esquema de particionamento Int64 Uniforme, os parâmetros de cadeia de caracteres de consulta *PartitionKey* e *PartitionKind* deverão ser usados para acessar uma partição do serviço:</span><span class="sxs-lookup"><span data-stu-id="d91c4-165">If the service uses the Uniform Int64 partitioning scheme, the *PartitionKey* and *PartitionKind* query string parameters must be used to reach a partition of the service:</span></span>

* <span data-ttu-id="d91c4-166">Externamente: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="d91c4-166">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span></span>
* <span data-ttu-id="d91c4-167">Internamente: `http://localhost:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="d91c4-167">Internally: `http://localhost:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span></span>

<span data-ttu-id="d91c4-168">Para acessar os recursos expostos pelo serviço, basta coloca o caminho do recurso após o nome do serviço na URL:</span><span class="sxs-lookup"><span data-stu-id="d91c4-168">To reach the resources that the service exposes, simply place the resource path after the service name in the URL:</span></span>

* <span data-ttu-id="d91c4-169">Externamente: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService/index.html?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="d91c4-169">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService/index.html?PartitionKey=3&PartitionKind=Int64Range`</span></span>
* <span data-ttu-id="d91c4-170">Internamente: `http://localhost:19081/MyApp/MyService/api/users/6?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="d91c4-170">Internally: `http://localhost:19081/MyApp/MyService/api/users/6?PartitionKey=3&PartitionKind=Int64Range`</span></span>

<span data-ttu-id="d91c4-171">O gateway, em seguida, encaminhará essas solicitações para a URL do serviço:</span><span class="sxs-lookup"><span data-stu-id="d91c4-171">The gateway will then forward these requests to the service's URL:</span></span>

* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/index.html`
* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/api/users/6`

## <a name="special-handling-for-port-sharing-services"></a><span data-ttu-id="d91c4-172">Tratamento especial para os serviços de compartilhamento de porta</span><span class="sxs-lookup"><span data-stu-id="d91c4-172">Special handling for port-sharing services</span></span>
<span data-ttu-id="d91c4-173">O Gateway de Aplicativo do Azure tenta resolver um endereço de serviço novamente e repetir a solicitação quando um serviço não pode ser alcançado.</span><span class="sxs-lookup"><span data-stu-id="d91c4-173">Azure Application Gateway attempts to resolve a service address again and retry the request when a service cannot be reached.</span></span> <span data-ttu-id="d91c4-174">Este é um dos principais benefícios do Gateway de Aplicativo, pois o código do cliente não precisa implementar sua própria solução de serviço e resolver o loop.</span><span class="sxs-lookup"><span data-stu-id="d91c4-174">This is a major benefit of Application Gateway because client code does not need to implement its own service resolution and resolve loop.</span></span>

<span data-ttu-id="d91c4-175">Geralmente, quando um serviço não pode ser acessado, a instância de serviço ou a réplica foi movida para um nó diferente como parte de seu ciclo de vida normal.</span><span class="sxs-lookup"><span data-stu-id="d91c4-175">Generally, when a service cannot be reached, the service instance or replica has moved to a different node as part of its normal lifecycle.</span></span> <span data-ttu-id="d91c4-176">Quando isso acontece, o Gateway de Aplicativo pode receber um erro de conexão de rede que indica que um ponto de extremidade não está aberto no endereço resolvido originalmente.</span><span class="sxs-lookup"><span data-stu-id="d91c4-176">When this happens, Application Gateway might receive a network connection error indicating that an endpoint is no longer open on the originally resolved address.</span></span>

<span data-ttu-id="d91c4-177">No entanto, réplicas ou instâncias de serviço podem compartilhar um processo de host e uma porta quando hospedadas por um servidor Web baseado em http.sys, incluindo:</span><span class="sxs-lookup"><span data-stu-id="d91c4-177">However, replicas or service instances can share a host process and might also share a port when hosted by an http.sys-based web server, including:</span></span>

* [<span data-ttu-id="d91c4-178">System.Net.HttpListener</span><span class="sxs-lookup"><span data-stu-id="d91c4-178">System.Net.HttpListener</span></span>](https://msdn.microsoft.com/library/system.net.httplistener%28v=vs.110%29.aspx)
* [<span data-ttu-id="d91c4-179">WebListener de Núcleo ASP.NET</span><span class="sxs-lookup"><span data-stu-id="d91c4-179">ASP.NET Core WebListener</span></span>](https://docs.asp.net/latest/fundamentals/servers.html#weblistener)
* [<span data-ttu-id="d91c4-180">Katana</span><span class="sxs-lookup"><span data-stu-id="d91c4-180">Katana</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.OwinSelfHost/)

<span data-ttu-id="d91c4-181">Nessa situação, é provável que o servidor Web esteja disponível no processo de host e respondendo às solicitações, mas a instância de serviço resolvido ou a réplica não está mais disponível no host.</span><span class="sxs-lookup"><span data-stu-id="d91c4-181">In this situation, it is likely that the web server is available in the host process and responding to requests, but the resolved service instance or replica is no longer available on the host.</span></span> <span data-ttu-id="d91c4-182">Nesse caso, o gateway receberá uma resposta HTTP 404 do servidor Web.</span><span class="sxs-lookup"><span data-stu-id="d91c4-182">In this case, the gateway will receive an HTTP 404 response from the web server.</span></span> <span data-ttu-id="d91c4-183">Como resultado, um HTTP 404 tem dois significados distintos:</span><span class="sxs-lookup"><span data-stu-id="d91c4-183">Thus, an HTTP 404 has two distinct meanings:</span></span>

- <span data-ttu-id="d91c4-184">Caso n. 1: o endereço do serviço está correto, mas o recurso solicitado pelo usuário não existe.</span><span class="sxs-lookup"><span data-stu-id="d91c4-184">Case #1: The service address is correct, but the resource that the user requested does not exist.</span></span>
- <span data-ttu-id="d91c4-185">Caso n. 2: o endereço do serviço está incorreto e o recurso solicitado pelo usuário talvez exista em um nó diferente.</span><span class="sxs-lookup"><span data-stu-id="d91c4-185">Case #2: The service address is incorrect, and the resource that the user requested might exist on a different node.</span></span>

<span data-ttu-id="d91c4-186">No primeiro caso, ele é um HTTP 404 normal, que é considerado um erro de usuário.</span><span class="sxs-lookup"><span data-stu-id="d91c4-186">The first case is a normal HTTP 404, which is considered a user error.</span></span> <span data-ttu-id="d91c4-187">No entanto, no segundo caso, o usuário solicitou um recurso que existe.</span><span class="sxs-lookup"><span data-stu-id="d91c4-187">However, in the second case, the user has requested a resource that does exist.</span></span> <span data-ttu-id="d91c4-188">O Gateway de Aplicativo não pôde localizá-lo porque o serviço em si foi movido.</span><span class="sxs-lookup"><span data-stu-id="d91c4-188">Application Gateway was unable to locate it because the service itself has moved.</span></span> <span data-ttu-id="d91c4-189">O Gateway de Aplicativo precisa resolver o endereço novamente e repetir a solicitação.</span><span class="sxs-lookup"><span data-stu-id="d91c4-189">Application Gateway needs to resolve the address again and retry the request.</span></span>

<span data-ttu-id="d91c4-190">O Gateway de Aplicativo, portanto, precisa de uma maneira para distinguir entre esses dois casos.</span><span class="sxs-lookup"><span data-stu-id="d91c4-190">Application Gateway thus needs a way to distinguish between these two cases.</span></span> <span data-ttu-id="d91c4-191">Para fazer essa distinção, uma dica do servidor é necessária.</span><span class="sxs-lookup"><span data-stu-id="d91c4-191">To make that distinction, a hint from the server is required.</span></span>

* <span data-ttu-id="d91c4-192">Por padrão, o Gateway de Aplicativo assume caso nº 2 e tenta resolver mais uma vez e emitir novamente a solicitação.</span><span class="sxs-lookup"><span data-stu-id="d91c4-192">By default, Application Gateway assumes case #2 and attempts to resolve and issue the request again.</span></span>
* <span data-ttu-id="d91c4-193">Para indicar o caso n. 1 para o Gateway de Aplicativo, o serviço deve retornar o seguinte cabeçalho de resposta HTTP:</span><span class="sxs-lookup"><span data-stu-id="d91c4-193">To indicate case #1 to Application Gateway, the service should return the following HTTP response header:</span></span>

  `X-ServiceFabric : ResourceNotFound`

<span data-ttu-id="d91c4-194">Esse cabeçalho de resposta HTTP indica uma situação de HTTP 404 normal em que o recurso solicitado não existir e o Gateway de Aplicativo não tentará resolver novamente o endereço do serviço.</span><span class="sxs-lookup"><span data-stu-id="d91c4-194">This HTTP response header indicates a normal HTTP 404 situation in which the requested resource does not exist, and Application Gateway will not attempt to resolve the service address again.</span></span>

## <a name="setup-and-configuration"></a><span data-ttu-id="d91c4-195">Instalação e configuração</span><span class="sxs-lookup"><span data-stu-id="d91c4-195">Setup and configuration</span></span>

### <a name="enable-reverse-proxy-via-azure-portal"></a><span data-ttu-id="d91c4-196">Habilitar proxy reverso por meio do portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d91c4-196">Enable reverse proxy via Azure portal</span></span>

<span data-ttu-id="d91c4-197">Portal do Azure fornece uma opção para habilitar o proxy inverso ao criar um novo cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d91c4-197">Azure portal provides an option to enable Reverse proxy while creating a new Service Fabric cluster.</span></span>
<span data-ttu-id="d91c4-198">Em **cluster do Service Fabric criar**, etapa 2: configuração de Cluster, configuração do tipo de nó, selecione a caixa de seleção "Habilitar proxy reverso".</span><span class="sxs-lookup"><span data-stu-id="d91c4-198">Under **Create Service Fabric cluster**, Step 2: Cluster Configuration, Node type configuration, select the checkbox to "Enable reverse proxy".</span></span>
<span data-ttu-id="d91c4-199">Para configurar o proxy reverso seguro, o certificado SSL pode ser especificado na Etapa 3: Segurança, definir configurações de segurança de cluster, selecione a caixa de seleção "Incluir um certificado SSL para o proxy inverso" e insira os detalhes do certificado.</span><span class="sxs-lookup"><span data-stu-id="d91c4-199">For configuring secure reverse proxy, SSL certificate can be specified in Step 3: Security, Configure cluster security settings, select the checkbox to "Include a SSL certificate for reverse proxy" and enter the certificate details.</span></span>

### <a name="enable-reverse-proxy-via-azure-resource-manager-templates"></a><span data-ttu-id="d91c4-200">Habilitar proxy reverso, por meio de modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d91c4-200">Enable reverse proxy via Azure Resource Manager templates</span></span>

<span data-ttu-id="d91c4-201">O proxy reverso do Service Fabric pode ser habilitado para o cluster por meio do [modelo do Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="d91c4-201">You can use the [Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md) to enable the reverse proxy in Service Fabric for the cluster.</span></span>

<span data-ttu-id="d91c4-202">Consulte [Configurar proxy reverso HTTPS em um cluster seguro](https://github.com/ChackDan/Service-Fabric/tree/master/ARM Templates/ReverseProxySecureSample#configure-https-reverse-proxy-in-a-secure-cluster) para amostras de modelo do Azure Resource Manager para configurar o proxy reverso de segurança com um certificado e o tratamento da substituição de certificados.</span><span class="sxs-lookup"><span data-stu-id="d91c4-202">Refer to [Configure HTTPS Reverse Proxy in a secure cluster](https://github.com/ChackDan/Service-Fabric/tree/master/ARM Templates/ReverseProxySecureSample#configure-https-reverse-proxy-in-a-secure-cluster) for Azure Resource Manager template samples to configure secure reverse proxy with a certificate and handling certificate rollover.</span></span>

<span data-ttu-id="d91c4-203">Primeiro, você obtém o modelo para o cluster que deseja implantar.</span><span class="sxs-lookup"><span data-stu-id="d91c4-203">First, you get the template for the cluster that you want to deploy.</span></span> <span data-ttu-id="d91c4-204">Você pode usar os modelos de exemplo ou criar um modelo do Resource Manager personalizado.</span><span class="sxs-lookup"><span data-stu-id="d91c4-204">You can either use the sample templates or create a custom Resource Manager template.</span></span> <span data-ttu-id="d91c4-205">Em seguida, você pode habilitar o proxy reverso usando as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="d91c4-205">Then, you can enable the reverse proxy by using the following steps:</span></span>

1. <span data-ttu-id="d91c4-206">Defina uma porta para o proxy inverso na [seção Parâmetros](../azure-resource-manager/resource-group-authoring-templates.md) do modelo.</span><span class="sxs-lookup"><span data-stu-id="d91c4-206">Define a port for the reverse proxy in the [Parameters section](../azure-resource-manager/resource-group-authoring-templates.md) of the template.</span></span>

    ```json
    "SFReverseProxyPort": {
        "type": "int",
        "defaultValue": 19081,
        "metadata": {
            "description": "Endpoint for Service Fabric Reverse proxy"
        }
    },
    ```
2. <span data-ttu-id="d91c4-207">Especifique a porta para cada um dos objetos nodetype no **Cluster** [seção Tipo de recurso](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="d91c4-207">Specify the port for each of the nodetype objects in the **Cluster** [Resource type section](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

    <span data-ttu-id="d91c4-208">A porta é identificada pelo nome do parâmetro, reverseProxyEndpointPort.</span><span class="sxs-lookup"><span data-stu-id="d91c4-208">The port is identified by the parameter name, reverseProxyEndpointPort.</span></span>

    ```json
    {
        "apiVersion": "2016-09-01",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
       "nodeTypes": [
          {
           ...
           "reverseProxyEndpointPort": "[parameters('SFReverseProxyPort')]",
           ...
          },
        ...
        ],
        ...
    }
    ```
3. <span data-ttu-id="d91c4-209">Para resolver o proxy inverso de fora do cluster do Azure, configure as regras do Azure Load Balancer para a porta que você especificou na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="d91c4-209">To address the reverse proxy from outside the Azure cluster, set up the Azure Load Balancer rules for the port that you specified in step 1.</span></span>

    ```json
    {
        "apiVersion": "[variables('lbApiVersion')]",
        "type": "Microsoft.Network/loadBalancers",
        ...
        ...
        "loadBalancingRules": [
            ...
            {
                "name": "LBSFReverseProxyRule",
                "properties": {
                    "backendAddressPool": {
                        "id": "[variables('lbPoolID0')]"
                    },
                    "backendPort": "[parameters('SFReverseProxyPort')]",
                    "enableFloatingIP": "false",
                    "frontendIPConfiguration": {
                        "id": "[variables('lbIPConfig0')]"
                    },
                    "frontendPort": "[parameters('SFReverseProxyPort')]",
                    "idleTimeoutInMinutes": "5",
                    "probe": {
                        "id": "[concat(variables('lbID0'),'/probes/SFReverseProxyProbe')]"
                    },
                    "protocol": "tcp"
                }
            }
        ],
        "probes": [
            ...
            {
                "name": "SFReverseProxyProbe",
                "properties": {
                    "intervalInSeconds": 5,
                    "numberOfProbes": 2,
                    "port":     "[parameters('SFReverseProxyPort')]",
                    "protocol": "tcp"
                }
            }  
        ]
    }
    ```
4. <span data-ttu-id="d91c4-210">Para configurar certificados SSL na porta de proxy Inverso, adicione o certificado à propriedade ***reverseProxyCertificate*** na [seção Tipo de recurso](../resource-group-authoring-templates.md) do **Cluster**.</span><span class="sxs-lookup"><span data-stu-id="d91c4-210">To configure SSL certificates on the port for the reverse proxy, add the certificate to the ***reverseProxyCertificate*** property in the **Cluster** [Resource type section](../resource-group-authoring-templates.md).</span></span>

    ```json
    {
        "apiVersion": "2016-09-01",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        "dependsOn": [
            "[concat('Microsoft.Storage/storageAccounts/', parameters('supportLogStorageAccountName'))]"
        ],
        "properties": {
            ...
            "reverseProxyCertificate": {
                "thumbprint": "[parameters('sfReverseProxyCertificateThumbprint')]",
                "x509StoreName": "[parameters('sfReverseProxyCertificateStoreName')]"
            },
            ...
            "clusterState": "Default",
        }
    }
    ```

### <a name="supporting-a-reverse-proxy-certificate-thats-different-from-the-cluster-certificate"></a><span data-ttu-id="d91c4-211">Suporte um certificado de proxy reverso diferente do certificado de cluster</span><span class="sxs-lookup"><span data-stu-id="d91c4-211">Supporting a reverse proxy certificate that's different from the cluster certificate</span></span>
 <span data-ttu-id="d91c4-212">Se o certificado de proxy reverso é diferente do certificado que protege o cluster, o certificado especificado anteriormente deve ser instalado na máquina virtual e adicionado à ACL (lista de controle de acesso) para que o Service Fabric possa acessá-lo.</span><span class="sxs-lookup"><span data-stu-id="d91c4-212">If the reverse proxy certificate is different from the certificate that secures the cluster, then the previously specified certificate should be installed on the virtual machine and added to the access control list (ACL) so that Service Fabric can access it.</span></span> <span data-ttu-id="d91c4-213">Isso pode ser feito na [seção de Tipo de recurso](../resource-group-authoring-templates.md) **virtualMachineScaleSets**.</span><span class="sxs-lookup"><span data-stu-id="d91c4-213">This can be done in the **virtualMachineScaleSets** [Resource type section](../resource-group-authoring-templates.md).</span></span> <span data-ttu-id="d91c4-214">Para instalação, adicione o certificado ao osProfile.</span><span class="sxs-lookup"><span data-stu-id="d91c4-214">For installation, add that certificate to the osProfile.</span></span> <span data-ttu-id="d91c4-215">A seção de extensão do modelo pode atualizar o certificado na ACL.</span><span class="sxs-lookup"><span data-stu-id="d91c4-215">The extension section of the template can update the certificate in the ACL.</span></span>

  ```json
  {
    "apiVersion": "[variables('vmssApiVersion')]",
    "type": "Microsoft.Compute/virtualMachineScaleSets",
    ....
      "osProfile": {
          "adminPassword": "[parameters('adminPassword')]",
          "adminUsername": "[parameters('adminUsername')]",
          "computernamePrefix": "[parameters('vmNodeType0Name')]",
          "secrets": [
            {
              "sourceVault": {
                "id": "[parameters('sfReverseProxySourceVaultValue')]"
              },
              "vaultCertificates": [
                {
                  "certificateStore": "[parameters('sfReverseProxyCertificateStoreValue')]",
                  "certificateUrl": "[parameters('sfReverseProxyCertificateUrlValue')]"
                }
              ]
            }
          ]
        }
   ....
   "extensions": [
          {
              "name": "[concat(parameters('vmNodeType0Name'),'_ServiceFabricNode')]",
              "properties": {
                      "type": "ServiceFabricNode",
                      "autoUpgradeMinorVersion": false,
                      ...
                      "publisher": "Microsoft.Azure.ServiceFabric",
                      "settings": {
                        "clusterEndpoint": "[reference(parameters('clusterName')).clusterEndpoint]",
                        "nodeTypeRef": "[parameters('vmNodeType0Name')]",
                        "dataPath": "D:\\\\SvcFab",
                        "durabilityLevel": "Bronze",
                        "testExtension": true,
                        "reverseProxyCertificate": {
                          "thumbprint": "[parameters('sfReverseProxyCertificateThumbprint')]",
                          "x509StoreName": "[parameters('sfReverseProxyCertificateStoreValue')]"
                        },
                  },
                  "typeHandlerVersion": "1.0"
              }
          },
      ]
    }
  ```
> [!NOTE]
> <span data-ttu-id="d91c4-216">Ao usar certificados que são diferentes do certificado do cluster para habilitar o proxy reverso em um cluster existente, instale o certificado de proxy reverso e atualize a ACL no cluster antes de habilitar o proxy reverso.</span><span class="sxs-lookup"><span data-stu-id="d91c4-216">When you use certificates that are different from the cluster certificate to enable the reverse proxy on an existing cluster, install the reverse proxy certificate and update the ACL on the cluster before you enable the reverse proxy.</span></span> <span data-ttu-id="d91c4-217">Conclua a implantação do [modelo do Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) usando as configurações mencionadas acima antes de iniciar uma implantação para habilitar o proxy reverso usando as etapas 1 a 4.</span><span class="sxs-lookup"><span data-stu-id="d91c4-217">Complete the [Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md) deployment by using the settings mentioned previously before you start a deployment to enable the reverse proxy in steps 1-4.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d91c4-218">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d91c4-218">Next steps</span></span>
* <span data-ttu-id="d91c4-219">Confira um exemplo de comunicação HTTP entre serviços em um [projeto de exemplo no GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="d91c4-219">See an example of HTTP communication between services in a [sample project on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span></span>
* [<span data-ttu-id="d91c4-220">Encaminhamento para o serviço HTTP seguro com um proxy reverso</span><span class="sxs-lookup"><span data-stu-id="d91c4-220">Forwarding to secure HTTP service with the reverse proxy</span></span>](service-fabric-reverseproxy-configure-secure-communication.md)
* [<span data-ttu-id="d91c4-221">Comunicação remota de serviço com os Reliable Services</span><span class="sxs-lookup"><span data-stu-id="d91c4-221">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="d91c4-222">API Web que usa o OWIN nos Reliable Services</span><span class="sxs-lookup"><span data-stu-id="d91c4-222">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="d91c4-223">Comunicação WCF usando os Reliable Services</span><span class="sxs-lookup"><span data-stu-id="d91c4-223">WCF communication by using Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
* <span data-ttu-id="d91c4-224">Para obter outras opções de configuração de proxy reverso, consulte a seção ApplicationGateway/Http em [Personalizar as configurações de cluster do Service Fabric](service-fabric-cluster-fabric-settings.md).</span><span class="sxs-lookup"><span data-stu-id="d91c4-224">For additional reverse proxy configuration options, refer ApplicationGateway/Http section in [Customize Service Fabric cluster settings](service-fabric-cluster-fabric-settings.md).</span></span>

[0]: ./media/service-fabric-reverseproxy/external-communication.png
[1]: ./media/service-fabric-reverseproxy/internal-communication.png
