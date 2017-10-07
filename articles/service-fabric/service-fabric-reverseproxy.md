---
title: proxy reverso do aaaAzure Service Fabric | Microsoft Docs
description: "Use proxy reverso do Service Fabric para toomicroservices de comunicação dentro e fora cluster de saudação."
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
ms.openlocfilehash: 0e7835a64ccd74293c7bdd8b41deae414c83dffa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="reverse-proxy-in-azure-service-fabric"></a><span data-ttu-id="2d7f9-103">Proxy reverso no Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="2d7f9-103">Reverse proxy in Azure Service Fabric</span></span>
<span data-ttu-id="2d7f9-104">proxy reverso de saudação que é criado no Azure Service Fabric endereços microservices no cluster do Service Fabric Olá que expõe pontos de extremidade HTTP.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-104">hello reverse proxy that's built into Azure Service Fabric addresses microservices in hello Service Fabric cluster that exposes HTTP endpoints.</span></span>

## <a name="microservices-communication-model"></a><span data-ttu-id="2d7f9-105">Modelo de comunicação de microsserviços</span><span class="sxs-lookup"><span data-stu-id="2d7f9-105">Microservices communication model</span></span>
<span data-ttu-id="2d7f9-106">Microservices na malha do serviço geralmente executado em um subconjunto de máquinas virtuais em cluster hello e pode mover de um tooanother de máquina virtual por vários motivos.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-106">Microservices in Service Fabric typically run on a subset of virtual machines in hello cluster and can move from one virtual machine tooanother for various reasons.</span></span> <span data-ttu-id="2d7f9-107">Portanto, os pontos de extremidade Olá microservices podem ser alterado dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-107">So, hello endpoints for microservices can change dynamically.</span></span> <span data-ttu-id="2d7f9-108">saudação padrão típico toocommunicate toohello microsserviço é a seguinte Olá resolver loop:</span><span class="sxs-lookup"><span data-stu-id="2d7f9-108">hello typical pattern toocommunicate toohello microservice is hello following resolve loop:</span></span>

1. <span data-ttu-id="2d7f9-109">Resolva o local de serviço Olá inicialmente por meio do serviço de nomeação de saudação.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-109">Resolve hello service location initially through hello naming service.</span></span>
2. <span data-ttu-id="2d7f9-110">Conecte-se o serviço de toohello.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-110">Connect toohello service.</span></span>
3. <span data-ttu-id="2d7f9-111">Determinar a causa de saudação de falhas de conexão e resolver o local do serviço Olá novamente quando necessário.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-111">Determine hello cause of connection failures, and resolve hello service location again when necessary.</span></span>

<span data-ttu-id="2d7f9-112">Esse processo geralmente envolve a quebra automática de bibliotecas de comunicação de cliente em um loop de repetição que implementa Olá serviço políticas de resolução e tente novamente.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-112">This process generally involves wrapping client-side communication libraries in a retry loop that implements hello service resolution and retry policies.</span></span>
<span data-ttu-id="2d7f9-113">Para obter mais informações, consulte [Conectar-se a serviços e se comunicar com eles](service-fabric-connect-and-communicate-with-services.md).</span><span class="sxs-lookup"><span data-stu-id="2d7f9-113">For more information, see [Connect and communicate with services](service-fabric-connect-and-communicate-with-services.md).</span></span>

### <a name="communicating-by-using-hello-reverse-proxy"></a><span data-ttu-id="2d7f9-114">A comunicação por proxy reverso Olá</span><span class="sxs-lookup"><span data-stu-id="2d7f9-114">Communicating by using hello reverse proxy</span></span>
<span data-ttu-id="2d7f9-115">proxy reverso de saudação na malha do serviço é executado em todos os nós Olá cluster hello.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-115">hello reverse proxy in Service Fabric runs on all hello nodes in hello cluster.</span></span> <span data-ttu-id="2d7f9-116">Ele executa o processo de resolução de todo o serviço de saudação em nome do cliente e, em seguida, encaminha a solicitação de saudação do cliente.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-116">It performs hello entire service resolution process on a client's behalf and then forwards hello client request.</span></span> <span data-ttu-id="2d7f9-117">Portanto, os clientes que executam no cluster de saudação podem usar qualquer serviço de destino do lado do cliente HTTP comunicação bibliotecas tootalk toohello usando proxy reverso hello, que é executado localmente no hello mesmo nó.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-117">So, clients that run on hello cluster can use any client-side HTTP communication libraries tootalk toohello target service by using hello reverse proxy that runs locally on hello same node.</span></span>

![Comunicação interna][1]

## <a name="reaching-microservices-from-outside-hello-cluster"></a><span data-ttu-id="2d7f9-119">Alcançar microservices do cluster de saudação externa</span><span class="sxs-lookup"><span data-stu-id="2d7f9-119">Reaching microservices from outside hello cluster</span></span>
<span data-ttu-id="2d7f9-120">modelo de comunicações externas saudação padrão para microservices é um modelo de aceitação em que cada serviço não pode ser acessado diretamente de clientes externos.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-120">hello default external communication model for microservices is an opt-in model where each service cannot be accessed directly from external clients.</span></span> <span data-ttu-id="2d7f9-121">[O balanceador de carga do Azure](../load-balancer/load-balancer-overview.md), que é um limite de rede entre microservices e clientes externos, faz a conversão de endereços de rede e externas encaminha solicitações de pontos de extremidade de IP: porta toointernal.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-121">[Azure Load Balancer](../load-balancer/load-balancer-overview.md), which is a network boundary between microservices and external clients, performs network address translation and forwards external requests toointernal IP:port endpoints.</span></span> <span data-ttu-id="2d7f9-122">toomake clientes de tooexternal acessíveis diretamente do ponto de extremidade do microsserviço, primeiro você deve configurar o balanceador de carga usa tooeach porta tooforward tráfego Olá serviço em cluster hello.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-122">toomake a microservice's endpoint directly accessible tooexternal clients, you must first configure Load Balancer tooforward traffic tooeach port that hello service uses in hello cluster.</span></span> <span data-ttu-id="2d7f9-123">Além disso, a maioria dos microservices, especialmente com monitoração de estado microservices, não em tempo real em todos os nós de cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-123">Furthermore, most microservices, especially stateful microservices, don't live on all nodes of hello cluster.</span></span> <span data-ttu-id="2d7f9-124">Olá microservices pode mover entre nós de failover.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-124">hello microservices can move between nodes on failover.</span></span> <span data-ttu-id="2d7f9-125">Nesses casos, balanceador de carga efetivamente não é possível determinar o local de saudação do nó de destino de saudação do hello réplicas toowhich encaminhar o tráfego.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-125">In such cases, Load Balancer cannot effectively determine hello location of hello target node of hello replicas toowhich it should forward traffic.</span></span>

### <a name="reaching-microservices-via-hello-reverse-proxy-from-outside-hello-cluster"></a><span data-ttu-id="2d7f9-126">Alcançar microservices via proxy reverso de saudação do cluster Olá externa</span><span class="sxs-lookup"><span data-stu-id="2d7f9-126">Reaching microservices via hello reverse proxy from outside hello cluster</span></span>
<span data-ttu-id="2d7f9-127">Em vez de configurar a porta de saudação de um serviço individual no balanceador de carga, você pode configurar apenas Olá porta proxy reverso Olá no balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-127">Instead of configuring hello port of an individual service in Load Balancer, you can configure just hello port of hello reverse proxy in Load Balancer.</span></span> <span data-ttu-id="2d7f9-128">Essa configuração permite que clientes fora do cluster Olá acessar serviços dentro do cluster hello usando proxy reverso de saudação sem configuração adicional.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-128">This configuration lets clients outside hello cluster reach services inside hello cluster by using hello reverse proxy without additional configuration.</span></span>

![Comunicação externa][0]

> [!WARNING]
> <span data-ttu-id="2d7f9-130">Quando você configura a porta do proxy inverso Olá no balanceador de carga, todos os microservices no cluster Olá que expor um ponto de extremidade HTTP são endereçáveis da fora Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-130">When you configure hello reverse proxy's port in Load Balancer, all microservices in hello cluster that expose an HTTP endpoint are addressable from outside hello cluster.</span></span>
>
>


## <a name="uri-format-for-addressing-services-by-using-hello-reverse-proxy"></a><span data-ttu-id="2d7f9-131">Formato URI para usar serviços usando o proxy reverso Olá</span><span class="sxs-lookup"><span data-stu-id="2d7f9-131">URI format for addressing services by using hello reverse proxy</span></span>
<span data-ttu-id="2d7f9-132">usos de proxy reverso Olá que uma determinado recurso uniforme identificador (URI) formato tooidentify Olá serviço partição toowhich Olá entrada solicitação deve ser encaminhada:</span><span class="sxs-lookup"><span data-stu-id="2d7f9-132">hello reverse proxy uses a specific uniform resource identifier (URI) format tooidentify hello service partition toowhich hello incoming request should be forwarded:</span></span>

```
http(s)://<Cluster FQDN | internal IP>:Port/<ServiceInstanceName>/<Suffix path>?PartitionKey=<key>&PartitionKind=<partitionkind>&ListenerName=<listenerName>&TargetReplicaSelector=<targetReplicaSelector>&Timeout=<timeout_in_seconds>
```

* <span data-ttu-id="2d7f9-133">**http (s):** proxy reverso Olá pode ser configurado tooaccept HTTP ou o tráfego HTTPS.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-133">**http(s):** hello reverse proxy can be configured tooaccept HTTP or HTTPS traffic.</span></span> <span data-ttu-id="2d7f9-134">Para encaminhamento de HTTPS, consulte muito[conectar o serviço seguro tooa com proxy reverso Olá](service-fabric-reverseproxy-configure-secure-communication.md) uma vez que toolisten de configuração de proxy reverso em HTTPS.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-134">For HTTPS forwarding, refer too[Connect tooa secure service with hello reverse proxy](service-fabric-reverseproxy-configure-secure-communication.md) once you have reverse proxy setup toolisten on HTTPS.</span></span>
* <span data-ttu-id="2d7f9-135">**Nome de domínio totalmente qualificado (FQDN) do cluster | IP interno:** para clientes externos, você pode configurar o proxy reverso Olá para que seja acessível por meio do domínio do cluster hello, como mycluster.eastus.cloudapp.azure.com. Por padrão, o proxy reverso Olá executa em cada nó.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-135">**Cluster fully qualified domain name (FQDN) | internal IP:** For external clients, you can configure hello reverse proxy so that it is reachable through hello cluster domain, such as mycluster.eastus.cloudapp.azure.com. By default, hello reverse proxy runs on every node.</span></span> <span data-ttu-id="2d7f9-136">Para o tráfego interno, proxy reverso Olá pode ser contatado no host local ou em qualquer nó interno de IP, como 10.0.0.1.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-136">For internal traffic, hello reverse proxy can be reached on localhost or on any internal node IP, such as 10.0.0.1.</span></span>
* <span data-ttu-id="2d7f9-137">**Porta:** é porta hello, como 19081, que foi especificada para o proxy inverso hello.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-137">**Port:** This is hello port, such as 19081, that has been specified for hello reverse proxy.</span></span>
* <span data-ttu-id="2d7f9-138">**ServiceInstanceName:** este é o nome totalmente qualificado de saudação da instância de serviço Olá implantado que você está tentando tooreach sem hello "fabric: /" esquema.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-138">**ServiceInstanceName:** This is hello fully-qualified name of hello deployed service instance that you are trying tooreach without hello "fabric:/" scheme.</span></span> <span data-ttu-id="2d7f9-139">Por exemplo, tooreach Olá *fabric: / myapp/myservice/* serviço, você usaria *myapp/myservice*.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-139">For example, tooreach hello *fabric:/myapp/myservice/* service, you would use *myapp/myservice*.</span></span>

    <span data-ttu-id="2d7f9-140">nome de instância de serviço Olá diferencia maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-140">hello service instance name is case-sensitive.</span></span> <span data-ttu-id="2d7f9-141">Usando diferenciam maiusculas de minúsculas para o nome de instância de serviço Olá Olá URL faz Olá solicitações toofail 404 (não encontrado).</span><span class="sxs-lookup"><span data-stu-id="2d7f9-141">Using a different casing for hello service instance name in hello URL causes hello requests toofail with 404 (Not Found).</span></span>
* <span data-ttu-id="2d7f9-142">**Caminho de sufixo:** este é o caminho da URL real hello, tais como *myapi/valores/adicionar/3*, para o serviço de saudação que você deseja tooconnect para.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-142">**Suffix path:** This is hello actual URL path, such as *myapi/values/add/3*, for hello service that you want tooconnect to.</span></span>
* <span data-ttu-id="2d7f9-143">**PartitionKey:** para um serviço particionado, isso é chave de partição computada de saudação da partição Olá que você deseja tooreach.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-143">**PartitionKey:** For a partitioned service, this is hello computed partition key of hello partition that you want tooreach.</span></span> <span data-ttu-id="2d7f9-144">Observe que isso *não* Olá GUID da ID de partição.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-144">Note that this is *not* hello partition ID GUID.</span></span> <span data-ttu-id="2d7f9-145">Esse parâmetro não é necessário para serviços que usam o esquema de partição singleton hello.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-145">This parameter is not required for services that use hello singleton partition scheme.</span></span>
* <span data-ttu-id="2d7f9-146">**PartitionKind:** este é o esquema de partição de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-146">**PartitionKind:** This is hello service partition scheme.</span></span> <span data-ttu-id="2d7f9-147">Isso pode ser 'Int64Range' ou 'Named'.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-147">This can be 'Int64Range' or 'Named'.</span></span> <span data-ttu-id="2d7f9-148">Esse parâmetro não é necessário para serviços que usam o esquema de partição singleton hello.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-148">This parameter is not required for services that use hello singleton partition scheme.</span></span>
* <span data-ttu-id="2d7f9-149">**ListenerName** são pontos de extremidade de saudação do serviço de saudação do formulário de saudação {"Pontos de extremidade": {"Listener1": "Endpoint1", "Listener2": "Endpoint2"...}}.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-149">**ListenerName** hello endpoints from hello service are of hello form {"Endpoints":{"Listener1":"Endpoint1","Listener2":"Endpoint2" ...}}.</span></span> <span data-ttu-id="2d7f9-150">Quando o serviço de saudação expõe vários pontos de extremidade, isso identifica o ponto de extremidade de saudação essa solicitação de cliente Olá deve ser encaminhada.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-150">When hello service exposes multiple endpoints, this identifies hello endpoint that hello client request should be forwarded to.</span></span> <span data-ttu-id="2d7f9-151">Isso pode ser omitido se serviço Olá tiver somente um ouvinte.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-151">This can be omitted if hello service has only one listener.</span></span>
* <span data-ttu-id="2d7f9-152">**TargetReplicaSelector** Especifica como a réplica de destino hello ou instância deve ser selecionada.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-152">**TargetReplicaSelector** This specifies how hello target replica or instance should be selected.</span></span>
  * <span data-ttu-id="2d7f9-153">Quando o serviço de destino Olá for com monitoração de estado, Olá TargetReplicaSelector pode ser uma das seguintes Olá: 'PrimaryReplica', 'RandomSecondaryReplica' ou 'RandomReplica'.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-153">When hello target service is stateful, hello TargetReplicaSelector can be one of hello following:  'PrimaryReplica', 'RandomSecondaryReplica', or 'RandomReplica'.</span></span> <span data-ttu-id="2d7f9-154">Quando esse parâmetro não for especificado, o padrão de saudação é 'PrimaryReplica'.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-154">When this parameter is not specified, hello default is 'PrimaryReplica'.</span></span>
  * <span data-ttu-id="2d7f9-155">Quando o serviço de destino Olá for sem monitoração de estado, o proxy reverso escolhe uma instância aleatória Olá partição tooforward Olá de solicitação do serviço para.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-155">When hello target service is stateless, reverse proxy picks a random instance of hello service partition tooforward hello request to.</span></span>
* <span data-ttu-id="2d7f9-156">**Tempo limite:** Isso especifica o tempo limite de saudação para solicitação HTTP de saudação criada pelo serviço de toohello de proxy reverso Olá em nome de solicitação de saudação do cliente.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-156">**Timeout:**  This specifies hello timeout for hello HTTP request created by hello reverse proxy toohello service on behalf of hello client request.</span></span> <span data-ttu-id="2d7f9-157">valor padrão de saudação é 60 segundos.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-157">hello default value is 60 seconds.</span></span> <span data-ttu-id="2d7f9-158">Este é um parâmetro opcional.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-158">This is an optional parameter.</span></span>

### <a name="example-usage"></a><span data-ttu-id="2d7f9-159">Exemplo de uso</span><span class="sxs-lookup"><span data-stu-id="2d7f9-159">Example usage</span></span>
<span data-ttu-id="2d7f9-160">Por exemplo, vamos Olá *fabric: / MyApp/MyService* serviço que abre um ouvinte de HTTP Olá URL a seguir:</span><span class="sxs-lookup"><span data-stu-id="2d7f9-160">As an example, let's take hello *fabric:/MyApp/MyService* service that opens an HTTP listener on hello following URL:</span></span>

```
http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/
```

<span data-ttu-id="2d7f9-161">Estes são recursos de saudação para o serviço de saudação:</span><span class="sxs-lookup"><span data-stu-id="2d7f9-161">Following are hello resources for hello service:</span></span>

* `/index.html`
* `/api/users/<userId>`

<span data-ttu-id="2d7f9-162">Se o serviço Olá usa singleton Olá esquema de particionamento, Olá *PartitionKey* e *PartitionKind* parâmetros de cadeia de caracteres de consulta não são necessários e Olá serviço pode ser acessado por meio do gateway hello como:</span><span class="sxs-lookup"><span data-stu-id="2d7f9-162">If hello service uses hello singleton partitioning scheme, hello *PartitionKey* and *PartitionKind* query string parameters are not required, and hello service can be reached by using hello gateway as:</span></span>

* <span data-ttu-id="2d7f9-163">Externamente: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService`</span><span class="sxs-lookup"><span data-stu-id="2d7f9-163">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService`</span></span>
* <span data-ttu-id="2d7f9-164">Internamente: `http://localhost:19081/MyApp/MyService`</span><span class="sxs-lookup"><span data-stu-id="2d7f9-164">Internally: `http://localhost:19081/MyApp/MyService`</span></span>

<span data-ttu-id="2d7f9-165">Se o serviço Olá usa Olá Int64 uniforme esquema de particionamento, Olá *PartitionKey* e *PartitionKind* parâmetros de cadeia de caracteres de consulta devem ser usado tooreach uma partição de serviço hello:</span><span class="sxs-lookup"><span data-stu-id="2d7f9-165">If hello service uses hello Uniform Int64 partitioning scheme, hello *PartitionKey* and *PartitionKind* query string parameters must be used tooreach a partition of hello service:</span></span>

* <span data-ttu-id="2d7f9-166">Externamente: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="2d7f9-166">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span></span>
* <span data-ttu-id="2d7f9-167">Internamente: `http://localhost:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="2d7f9-167">Internally: `http://localhost:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span></span>

<span data-ttu-id="2d7f9-168">recursos Olá tooreach Olá serviço expõe, simplesmente colocar o caminho do recurso Olá após nome do serviço Olá Olá URL:</span><span class="sxs-lookup"><span data-stu-id="2d7f9-168">tooreach hello resources that hello service exposes, simply place hello resource path after hello service name in hello URL:</span></span>

* <span data-ttu-id="2d7f9-169">Externamente: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService/index.html?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="2d7f9-169">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService/index.html?PartitionKey=3&PartitionKind=Int64Range`</span></span>
* <span data-ttu-id="2d7f9-170">Internamente: `http://localhost:19081/MyApp/MyService/api/users/6?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="2d7f9-170">Internally: `http://localhost:19081/MyApp/MyService/api/users/6?PartitionKey=3&PartitionKind=Int64Range`</span></span>

<span data-ttu-id="2d7f9-171">gateway Olá encaminhará, em seguida, a URL do serviço de toohello essas solicitações:</span><span class="sxs-lookup"><span data-stu-id="2d7f9-171">hello gateway will then forward these requests toohello service's URL:</span></span>

* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/index.html`
* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/api/users/6`

## <a name="special-handling-for-port-sharing-services"></a><span data-ttu-id="2d7f9-172">Tratamento especial para os serviços de compartilhamento de porta</span><span class="sxs-lookup"><span data-stu-id="2d7f9-172">Special handling for port-sharing services</span></span>
<span data-ttu-id="2d7f9-173">Gateway de aplicativo do Azure tenta tooresolve um serviço endereço novamente e repita a solicitação de saudação quando um serviço não pode ser alcançado.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-173">Azure Application Gateway attempts tooresolve a service address again and retry hello request when a service cannot be reached.</span></span> <span data-ttu-id="2d7f9-174">Isso é o principal benefício do Application Gateway porque o código do cliente não precisa tooimplement sua própria solução de serviço e resolver o loop.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-174">This is a major benefit of Application Gateway because client code does not need tooimplement its own service resolution and resolve loop.</span></span>

<span data-ttu-id="2d7f9-175">Em geral, quando um serviço não pode ser atingido, a instância do serviço hello ou réplica foi movido tooa outro nó como parte de seu ciclo de vida normal.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-175">Generally, when a service cannot be reached, hello service instance or replica has moved tooa different node as part of its normal lifecycle.</span></span> <span data-ttu-id="2d7f9-176">Quando isso acontece, o Application Gateway pode receber uma rede conexão erro indicando que um ponto de extremidade é que nenhum mais aberto em Olá originalmente resolvido endereço.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-176">When this happens, Application Gateway might receive a network connection error indicating that an endpoint is no longer open on hello originally resolved address.</span></span>

<span data-ttu-id="2d7f9-177">No entanto, réplicas ou instâncias de serviço podem compartilhar um processo de host e uma porta quando hospedadas por um servidor Web baseado em http.sys, incluindo:</span><span class="sxs-lookup"><span data-stu-id="2d7f9-177">However, replicas or service instances can share a host process and might also share a port when hosted by an http.sys-based web server, including:</span></span>

* [<span data-ttu-id="2d7f9-178">System.Net.HttpListener</span><span class="sxs-lookup"><span data-stu-id="2d7f9-178">System.Net.HttpListener</span></span>](https://msdn.microsoft.com/library/system.net.httplistener%28v=vs.110%29.aspx)
* [<span data-ttu-id="2d7f9-179">WebListener de Núcleo ASP.NET</span><span class="sxs-lookup"><span data-stu-id="2d7f9-179">ASP.NET Core WebListener</span></span>](https://docs.asp.net/latest/fundamentals/servers.html#weblistener)
* [<span data-ttu-id="2d7f9-180">Katana</span><span class="sxs-lookup"><span data-stu-id="2d7f9-180">Katana</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.OwinSelfHost/)

<span data-ttu-id="2d7f9-181">Nessa situação, é provável que o servidor web hello está disponível no processo do host hello e responder toorequests, mas Olá resolvido instância de serviço ou a réplica não está mais disponível no host de saudação.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-181">In this situation, it is likely that hello web server is available in hello host process and responding toorequests, but hello resolved service instance or replica is no longer available on hello host.</span></span> <span data-ttu-id="2d7f9-182">Nesse caso, gateway Olá receberá uma resposta HTTP 404 de servidor de web hello.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-182">In this case, hello gateway will receive an HTTP 404 response from hello web server.</span></span> <span data-ttu-id="2d7f9-183">Como resultado, um HTTP 404 tem dois significados distintos:</span><span class="sxs-lookup"><span data-stu-id="2d7f9-183">Thus, an HTTP 404 has two distinct meanings:</span></span>

- <span data-ttu-id="2d7f9-184">Caso #1: endereço do serviço hello está correto, mas o recurso Olá Olá usuário solicitado não existe.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-184">Case #1: hello service address is correct, but hello resource that hello user requested does not exist.</span></span>
- <span data-ttu-id="2d7f9-185">Caso #2: o endereço do serviço hello está incorreto e recurso Olá Olá usuário solicitado pode existir em um nó diferente.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-185">Case #2: hello service address is incorrect, and hello resource that hello user requested might exist on a different node.</span></span>

<span data-ttu-id="2d7f9-186">Olá primeiro é um HTTP 404 normal, que é considerada um erro do usuário.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-186">hello first case is a normal HTTP 404, which is considered a user error.</span></span> <span data-ttu-id="2d7f9-187">No entanto, no caso de segundo hello, Olá usuário solicitar um recurso que existe.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-187">However, in hello second case, hello user has requested a resource that does exist.</span></span> <span data-ttu-id="2d7f9-188">Application Gateway foi toolocate não é possível que porque o próprio serviço Olá foi movida.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-188">Application Gateway was unable toolocate it because hello service itself has moved.</span></span> <span data-ttu-id="2d7f9-189">Application Gateway necessidades tooresolve Olá endereço novamente e tente solicitar novamente hello.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-189">Application Gateway needs tooresolve hello address again and retry hello request.</span></span>

<span data-ttu-id="2d7f9-190">Application Gateway, portanto, precisa de um toodistinguish de maneira entre esses dois casos.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-190">Application Gateway thus needs a way toodistinguish between these two cases.</span></span> <span data-ttu-id="2d7f9-191">toomake que distinção, uma dica do servidor de saudação é necessária.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-191">toomake that distinction, a hint from hello server is required.</span></span>

* <span data-ttu-id="2d7f9-192">Por padrão, o Application Gateway assume caso #2 e tentar a solicitação de saudação tooresolve e emitir novamente.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-192">By default, Application Gateway assumes case #2 and attempts tooresolve and issue hello request again.</span></span>
* <span data-ttu-id="2d7f9-193">tooindicate caso &#1; tooApplication Gateway, o serviço de saudação deve retornar Olá cabeçalho de resposta HTTP a seguir:</span><span class="sxs-lookup"><span data-stu-id="2d7f9-193">tooindicate case #1 tooApplication Gateway, hello service should return hello following HTTP response header:</span></span>

  `X-ServiceFabric : ResourceNotFound`

<span data-ttu-id="2d7f9-194">Esse cabeçalho de resposta HTTP indica uma situação de HTTP 404 normal no qual Olá recurso solicitado não existe e o Application Gateway não tentará endereço do serviço Olá tooresolve novamente.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-194">This HTTP response header indicates a normal HTTP 404 situation in which hello requested resource does not exist, and Application Gateway will not attempt tooresolve hello service address again.</span></span>

## <a name="setup-and-configuration"></a><span data-ttu-id="2d7f9-195">Instalação e configuração</span><span class="sxs-lookup"><span data-stu-id="2d7f9-195">Setup and configuration</span></span>

### <a name="enable-reverse-proxy-via-azure-portal"></a><span data-ttu-id="2d7f9-196">Habilitar proxy reverso por meio do portal do Azure</span><span class="sxs-lookup"><span data-stu-id="2d7f9-196">Enable reverse proxy via Azure portal</span></span>

<span data-ttu-id="2d7f9-197">Portal do Azure fornece um proxy reverso de tooenable opção ao criar um novo cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-197">Azure portal provides an option tooenable Reverse proxy while creating a new Service Fabric cluster.</span></span>
<span data-ttu-id="2d7f9-198">Em **cluster do Service Fabric criar**, etapa 2: configuração de Cluster, configuração do tipo de nó, selecione caixa de seleção de saudação muito "Habilitar proxy reverso".</span><span class="sxs-lookup"><span data-stu-id="2d7f9-198">Under **Create Service Fabric cluster**, Step 2: Cluster Configuration, Node type configuration, select hello checkbox too"Enable reverse proxy".</span></span>
<span data-ttu-id="2d7f9-199">Para configurar o proxy reverso seguro, o certificado SSL pode ser especificado na etapa 3: segurança, definir configurações de segurança de cluster, Olá selecione caixa de seleção "Incluir um certificado SSL para o proxy inverso" e insira os detalhes do certificado de saudação muito.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-199">For configuring secure reverse proxy, SSL certificate can be specified in Step 3: Security, Configure cluster security settings, select hello checkbox too"Include a SSL certificate for reverse proxy" and enter hello certificate details.</span></span>

### <a name="enable-reverse-proxy-via-azure-resource-manager-templates"></a><span data-ttu-id="2d7f9-200">Habilitar proxy reverso, por meio de modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2d7f9-200">Enable reverse proxy via Azure Resource Manager templates</span></span>

<span data-ttu-id="2d7f9-201">Você pode usar o hello [modelo do Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) tooenable Olá proxy reverso na malha do serviço de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-201">You can use hello [Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md) tooenable hello reverse proxy in Service Fabric for hello cluster.</span></span>

<span data-ttu-id="2d7f9-202">Consulte também[configurar Proxy reverso HTTPS em um cluster seguro](https://github.com/ChackDan/Service-Fabric/tree/master/ARM Templates/ReverseProxySecureSample#configure-https-reverse-proxy-in-a-secure-cluster) para o Azure Resource Manager tooconfigure o proxy reverso seguro com a substituição de certificado do certificado e tratamento de amostras de modelo.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-202">Refer too[Configure HTTPS Reverse Proxy in a secure cluster](https://github.com/ChackDan/Service-Fabric/tree/master/ARM Templates/ReverseProxySecureSample#configure-https-reverse-proxy-in-a-secure-cluster) for Azure Resource Manager template samples tooconfigure secure reverse proxy with a certificate and handling certificate rollover.</span></span>

<span data-ttu-id="2d7f9-203">Primeiro, você obterá modelo Olá para cluster Olá que você deseja toodeploy.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-203">First, you get hello template for hello cluster that you want toodeploy.</span></span> <span data-ttu-id="2d7f9-204">Você pode usar modelos de exemplo hello ou criar um modelo personalizado do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-204">You can either use hello sample templates or create a custom Resource Manager template.</span></span> <span data-ttu-id="2d7f9-205">Em seguida, você pode habilitar o proxy reverso hello usando Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="2d7f9-205">Then, you can enable hello reverse proxy by using hello following steps:</span></span>

1. <span data-ttu-id="2d7f9-206">Definir uma porta de proxy reverso Olá em Olá [seção parâmetros](../azure-resource-manager/resource-group-authoring-templates.md) do modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-206">Define a port for hello reverse proxy in hello [Parameters section](../azure-resource-manager/resource-group-authoring-templates.md) of hello template.</span></span>

    ```json
    "SFReverseProxyPort": {
        "type": "int",
        "defaultValue": 19081,
        "metadata": {
            "description": "Endpoint for Service Fabric Reverse proxy"
        }
    },
    ```
2. <span data-ttu-id="2d7f9-207">Especifique a porta de saudação para cada um dos objetos de nodetype Olá Olá **Cluster** [seção de tipo de recurso](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="2d7f9-207">Specify hello port for each of hello nodetype objects in hello **Cluster** [Resource type section](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

    <span data-ttu-id="2d7f9-208">porta de saudação é identificada pelo nome do parâmetro hello, reverseProxyEndpointPort.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-208">hello port is identified by hello parameter name, reverseProxyEndpointPort.</span></span>

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
3. <span data-ttu-id="2d7f9-209">Olá tooaddress proxy reverso da saudação fora cluster do Azure, configurar as regras de Balanceador de carga do Azure Olá para a porta de saudação que você especificou na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-209">tooaddress hello reverse proxy from outside hello Azure cluster, set up hello Azure Load Balancer rules for hello port that you specified in step 1.</span></span>

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
4. <span data-ttu-id="2d7f9-210">certificados SSL de tooconfigure na porta de saudação de proxy reverso do hello, adicionar Olá certificado toohello ***reverseProxyCertificate*** propriedade Olá **Cluster** [seção de tipo de recurso](../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="2d7f9-210">tooconfigure SSL certificates on hello port for hello reverse proxy, add hello certificate toohello ***reverseProxyCertificate*** property in hello **Cluster** [Resource type section](../resource-group-authoring-templates.md).</span></span>

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

### <a name="supporting-a-reverse-proxy-certificate-thats-different-from-hello-cluster-certificate"></a><span data-ttu-id="2d7f9-211">Dando suporte a um certificado de proxy reverso que é diferente do certificado de cluster Olá</span><span class="sxs-lookup"><span data-stu-id="2d7f9-211">Supporting a reverse proxy certificate that's different from hello cluster certificate</span></span>
 <span data-ttu-id="2d7f9-212">Se o certificado de proxy reverso Olá for diferente do certificado de saudação que protege cluster hello, em seguida, Olá especificado anteriormente certificado deve ser instalado na máquina virtual de saudação e adicionado toohello lista de controle de acesso (ACL) para que possa Service Fabric acessá-lo.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-212">If hello reverse proxy certificate is different from hello certificate that secures hello cluster, then hello previously specified certificate should be installed on hello virtual machine and added toohello access control list (ACL) so that Service Fabric can access it.</span></span> <span data-ttu-id="2d7f9-213">Isso pode ser feito no hello **virtualMachineScaleSets** [seção de tipo de recurso](../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="2d7f9-213">This can be done in hello **virtualMachineScaleSets** [Resource type section](../resource-group-authoring-templates.md).</span></span> <span data-ttu-id="2d7f9-214">Para a instalação, adicione esse osProfile toohello de certificado.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-214">For installation, add that certificate toohello osProfile.</span></span> <span data-ttu-id="2d7f9-215">seção de extensões de saudação do modelo de saudação pode atualizar o certificado Olá Olá ACL.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-215">hello extension section of hello template can update hello certificate in hello ACL.</span></span>

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
> <span data-ttu-id="2d7f9-216">Quando você usa certificados que são diferentes da saudação cluster certificado tooenable Olá proxy reverso em um cluster existente, instalar certificado de proxy reverso hello e atualizar Olá ACL no cluster de saudação antes de habilitar o proxy reverso hello.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-216">When you use certificates that are different from hello cluster certificate tooenable hello reverse proxy on an existing cluster, install hello reverse proxy certificate and update hello ACL on hello cluster before you enable hello reverse proxy.</span></span> <span data-ttu-id="2d7f9-217">Olá completa [modelo do Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) implantação usando as configurações de saudação mencionadas anteriormente antes de iniciar um proxy reverso do tooenable Olá de implantação em etapas 1 a 4.</span><span class="sxs-lookup"><span data-stu-id="2d7f9-217">Complete hello [Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md) deployment by using hello settings mentioned previously before you start a deployment tooenable hello reverse proxy in steps 1-4.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2d7f9-218">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2d7f9-218">Next steps</span></span>
* <span data-ttu-id="2d7f9-219">Confira um exemplo de comunicação HTTP entre serviços em um [projeto de exemplo no GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="2d7f9-219">See an example of HTTP communication between services in a [sample project on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span></span>
* [<span data-ttu-id="2d7f9-220">O serviço HTTP toosecure de encaminhamento com proxy reverso Olá</span><span class="sxs-lookup"><span data-stu-id="2d7f9-220">Forwarding toosecure HTTP service with hello reverse proxy</span></span>](service-fabric-reverseproxy-configure-secure-communication.md)
* [<span data-ttu-id="2d7f9-221">Comunicação remota de serviço com os Reliable Services</span><span class="sxs-lookup"><span data-stu-id="2d7f9-221">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="2d7f9-222">API Web que usa o OWIN nos Reliable Services</span><span class="sxs-lookup"><span data-stu-id="2d7f9-222">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="2d7f9-223">Comunicação WCF usando os Reliable Services</span><span class="sxs-lookup"><span data-stu-id="2d7f9-223">WCF communication by using Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
* <span data-ttu-id="2d7f9-224">Para obter outras opções de configuração de proxy reverso, consulte a seção ApplicationGateway/Http em [Personalizar as configurações de cluster do Service Fabric](service-fabric-cluster-fabric-settings.md).</span><span class="sxs-lookup"><span data-stu-id="2d7f9-224">For additional reverse proxy configuration options, refer ApplicationGateway/Http section in [Customize Service Fabric cluster settings](service-fabric-cluster-fabric-settings.md).</span></span>

[0]: ./media/service-fabric-reverseproxy/external-communication.png
[1]: ./media/service-fabric-reverseproxy/internal-communication.png
