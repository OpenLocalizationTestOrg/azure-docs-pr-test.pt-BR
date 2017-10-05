---
title: "Conectar-se e comunicar-se com serviços no Azure Service Fabric | Microsoft Docs"
description: "Saiba como resolver, conectar-se e comunicar-se com serviços no Service Fabric."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: msfussell
ms.assetid: 7d1052ec-2c9f-443d-8b99-b75c97266e6c
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 5/9/2017
ms.author: vturecek
ms.openlocfilehash: 3e61ad19df34c6a57da43e26bd2ab9d7ecdbf98e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-and-communicate-with-services-in-service-fabric"></a><span data-ttu-id="7ce27-103">Conectar e se comunicar com serviços no Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7ce27-103">Connect and communicate with services in Service Fabric</span></span>
<span data-ttu-id="7ce27-104">No Service Fabric, um serviço é executado em algum lugar em um cluster do Service Fabric, normalmente distribuído entre várias VMs.</span><span class="sxs-lookup"><span data-stu-id="7ce27-104">In Service Fabric, a service runs somewhere in a Service Fabric cluster, typically distributed across multiple VMs.</span></span> <span data-ttu-id="7ce27-105">Ele pode ser movido de um local para outro, pelo proprietário do serviço ou automaticamente pelo Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7ce27-105">It can be moved from one place to another, either by the service owner, or automatically by Service Fabric.</span></span> <span data-ttu-id="7ce27-106">Os serviços não estão estaticamente vinculados a um determinado computador ou endereço.</span><span class="sxs-lookup"><span data-stu-id="7ce27-106">Services are not statically tied to a particular machine or address.</span></span>

<span data-ttu-id="7ce27-107">Um aplicativo do Service Fabric geralmente é composto por vários serviços diferentes, em que cada serviço executa uma tarefa específica.</span><span class="sxs-lookup"><span data-stu-id="7ce27-107">A Service Fabric application is generally composed of many different services, where each service performs a specialized task.</span></span> <span data-ttu-id="7ce27-108">Esses serviços podem se comunicar entre si para formar uma função completa, tal como partes diferentes de renderização de um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="7ce27-108">These services may communicate with each other to form a complete function, such as rendering different parts of a web application.</span></span> <span data-ttu-id="7ce27-109">Também existem aplicativos cliente que se conectam e se comunicam com os serviços.</span><span class="sxs-lookup"><span data-stu-id="7ce27-109">There are also client applications that connect to and communicate with services.</span></span> <span data-ttu-id="7ce27-110">Este documento aborda como configurar a comunicação com os serviços do Service Fabric e entre eles.</span><span class="sxs-lookup"><span data-stu-id="7ce27-110">This document discusses how to set up communication with and between your services in Service Fabric.</span></span>

<span data-ttu-id="7ce27-111">Este vídeo da Microsoft Virtual Academy também discute a comunicação de serviço: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=iYFCk76yC_6706218965"></span><span class="sxs-lookup"><span data-stu-id="7ce27-111">This Microsoft Virtual Academy video also discusses service communication: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=iYFCk76yC_6706218965"></span></span>  
<img src="./media/service-fabric-connect-and-communicate-with-services/CommunicationVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="bring-your-own-protocol"></a><span data-ttu-id="7ce27-112">Trazer seu próprio protocolo</span><span class="sxs-lookup"><span data-stu-id="7ce27-112">Bring your own protocol</span></span>
<span data-ttu-id="7ce27-113">O Service Fabric ajuda a gerenciar o ciclo de vida dos seus serviços, mas ele não tome decisões sobre o que seus serviços fazem.</span><span class="sxs-lookup"><span data-stu-id="7ce27-113">Service Fabric helps manage the lifecycle of your services but it does not make decisions about what your services do.</span></span> <span data-ttu-id="7ce27-114">Isso inclui a comunicação.</span><span class="sxs-lookup"><span data-stu-id="7ce27-114">This includes communication.</span></span> <span data-ttu-id="7ce27-115">Quando seu serviço é aberto pelo Service Fabric, que é a oportunidade do serviço de configurar um ponto de extremidade para solicitações de entrada, usando qualquer protocolo ou pilha de comunicação desejados.</span><span class="sxs-lookup"><span data-stu-id="7ce27-115">When your service is opened by Service Fabric, that's your service's opportunity to set up an endpoint for incoming requests, using whatever protocol or communication stack you want.</span></span> <span data-ttu-id="7ce27-116">O serviço escutará um endereço **IP:port** normal usando qualquer esquema de endereçamento, como um URI.</span><span class="sxs-lookup"><span data-stu-id="7ce27-116">Your service will listen on a normal **IP:port** address using any addressing scheme, such as a URI.</span></span> <span data-ttu-id="7ce27-117">Várias instâncias de serviço ou réplicas podem compartilhar um processo de host, quando então eles precisarão usar portas diferentes ou um mecanismo de compartilhamento de porta, como o driver do kernel http.sys no Windows.</span><span class="sxs-lookup"><span data-stu-id="7ce27-117">Multiple service instances or replicas may share a host process, in which case they will either need to use different ports or use a port-sharing mechanism, such as the http.sys kernel driver in Windows.</span></span> <span data-ttu-id="7ce27-118">Em ambos os casos, cada instância de serviço ou réplica em um processo de host deve ser endereçável exclusivamente.</span><span class="sxs-lookup"><span data-stu-id="7ce27-118">In either case, each service instance or replica in a host process must be uniquely addressable.</span></span>

![pontos de extremidade de serviço][1]

## <a name="service-discovery-and-resolution"></a><span data-ttu-id="7ce27-120">Resolução e descoberta de serviço</span><span class="sxs-lookup"><span data-stu-id="7ce27-120">Service discovery and resolution</span></span>
<span data-ttu-id="7ce27-121">Em um sistema distribuído, os serviços podem passar de um computador para outro ao com o passar do tempo.</span><span class="sxs-lookup"><span data-stu-id="7ce27-121">In a distributed system, services may move from one machine to another over time.</span></span> <span data-ttu-id="7ce27-122">Isso pode ocorrer por vários motivos, incluindo balanceamento de recursos, atualizações, failovers ou escala horizontal.</span><span class="sxs-lookup"><span data-stu-id="7ce27-122">This can happen for various reasons, including resource balancing, upgrades, failovers, or scale-out.</span></span> <span data-ttu-id="7ce27-123">Isso significa que os endereços de ponto de extremidade de serviço mudam conforme o serviço passa para nós com endereços IP diferentes, podendo abrir portas diferentes se o serviço usar uma porta dinâmica selecionada.</span><span class="sxs-lookup"><span data-stu-id="7ce27-123">This means service endpoint addresses change as the service moves to nodes with different IP addresses, and may open on different ports if the service uses a dynamically selected port.</span></span>

![Distribuição de serviços][7]

<span data-ttu-id="7ce27-125">O Service Fabric fornece um serviço de descoberta e resolução chamado Serviço de Nomenclatura.</span><span class="sxs-lookup"><span data-stu-id="7ce27-125">Service Fabric provides a discovery and resolution service called the Naming Service.</span></span> <span data-ttu-id="7ce27-126">O Serviço de Nomenclatura mantém uma tabela que mapeia instâncias do serviço nomeadas para os endereços de ponto de extremidade que elas escutam.</span><span class="sxs-lookup"><span data-stu-id="7ce27-126">The Naming Service maintains a table that maps named service instances to the endpoint addresses they listen on.</span></span> <span data-ttu-id="7ce27-127">Todas as instâncias de serviço nomeadas do Service Fabric têm nomes exclusivos representados como URIs, como por exemplo, `"fabric:/MyApplication/MyService"`.</span><span class="sxs-lookup"><span data-stu-id="7ce27-127">All named service instances in Service Fabric have unique names represented as URIs, for example, `"fabric:/MyApplication/MyService"`.</span></span> <span data-ttu-id="7ce27-128">O nome do serviço não é alterado com o tempo de vida do serviço, apenas os endereços de ponto de extremidade podem ser alterados quando ao mover os serviços.</span><span class="sxs-lookup"><span data-stu-id="7ce27-128">The name of the service does not change over the lifetime of the service, it's only the endpoint addresses that can change when services move.</span></span> <span data-ttu-id="7ce27-129">Isso é semelhante aos sites que têm URLs constantes, mas em que o endereço IP pode mudar.</span><span class="sxs-lookup"><span data-stu-id="7ce27-129">This is analogous to websites that have constant URLs but where the IP address may change.</span></span> <span data-ttu-id="7ce27-130">E assim como DNS na web, que resolve as URLs do site para endereços IP, o Service Fabric tem um registrador que mapeia nomes de serviço para seu endereço do ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="7ce27-130">And similar to DNS on the web, which resolves website URLs to IP addresses, Service Fabric has a registrar that maps service names to their endpoint address.</span></span>

![pontos de extremidade de serviço][2]

<span data-ttu-id="7ce27-132">Resolver e conectar-se aos serviços envolve as seguintes etapas executadas em um loop:</span><span class="sxs-lookup"><span data-stu-id="7ce27-132">Resolving and connecting to services involves the following steps run in a loop:</span></span>

* <span data-ttu-id="7ce27-133">**Resolver**: obter o ponto de extremidade que um serviço publicou do Serviço de Nomenclatura.</span><span class="sxs-lookup"><span data-stu-id="7ce27-133">**Resolve**: Get the endpoint that a service has published from the Naming Service.</span></span>
* <span data-ttu-id="7ce27-134">**Conectar**: conectar-se ao serviço por meio de qualquer protocolo usado no ponto de extremidade em questão.</span><span class="sxs-lookup"><span data-stu-id="7ce27-134">**Connect**: Connect to the service over whatever protocol it uses on that endpoint.</span></span>
* <span data-ttu-id="7ce27-135">**Tentar Novamente**: uma tentativa de conexão pode falhar por vários motivos, por exemplo, se o serviço foi movido desde a última vez que o endereço do ponto de extremidade foi resolvido.</span><span class="sxs-lookup"><span data-stu-id="7ce27-135">**Retry**: A connection attempt may fail for any number of reasons, for example if the service has moved since the last time the endpoint address was resolved.</span></span> <span data-ttu-id="7ce27-136">Nesse caso, as etapas resolver e conectar anteriores precisam ser repetidas e esse ciclo é repetido até que a conexão seja bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="7ce27-136">In that case, the preceding resolve and connect steps need to be retried, and this cycle is repeated until the connection succeeds.</span></span>

## <a name="connecting-to-other-services"></a><span data-ttu-id="7ce27-137">Conectando a outros serviços</span><span class="sxs-lookup"><span data-stu-id="7ce27-137">Connecting to other services</span></span>
<span data-ttu-id="7ce27-138">Geralmente, os serviços que se conectam entre si em um cluster podem acessar diretamente os pontos de extremidade de outros serviços, pois os nós de um cluster estão na mesma rede local.</span><span class="sxs-lookup"><span data-stu-id="7ce27-138">Services connecting to each other inside a cluster generally can directly access the endpoints of other services because the nodes in a cluster are on the same local network.</span></span> <span data-ttu-id="7ce27-139">Para facilitar a conexão entre serviços, o Service Fabric oferece serviços adicionais que usam o Serviço de Nomeação.</span><span class="sxs-lookup"><span data-stu-id="7ce27-139">To make is easier to connect between services, Service Fabric provides additional services that use the Naming Service.</span></span> <span data-ttu-id="7ce27-140">Um serviço DNS e um serviço de proxy reverso.</span><span class="sxs-lookup"><span data-stu-id="7ce27-140">A DNS service and a reverse proxy service.</span></span>


### <a name="dns-service"></a><span data-ttu-id="7ce27-141">Serviço DNS</span><span class="sxs-lookup"><span data-stu-id="7ce27-141">DNS service</span></span>
<span data-ttu-id="7ce27-142">Como muitos serviços, especialmente serviços em contêineres, podem ter um nome de URL existente, ter a capacidade de resolvê-los usando o protocolo DNS padrão (em vez do protocolo do Serviço de Nomeação) é muito conveniente, especialmente em cenários que usam o método lift-and-shift para aplicativos.</span><span class="sxs-lookup"><span data-stu-id="7ce27-142">Since many services, especially containerized services, can have an existing URL name, being able to resolve these using the standard DNS protocol (rather than the Naming Service protocol) is very convenient, especially in application "lift and shift" scenarios.</span></span> <span data-ttu-id="7ce27-143">Isso é exatamente o que o serviço DNS faz.</span><span class="sxs-lookup"><span data-stu-id="7ce27-143">This is exactly what the DNS service does.</span></span> <span data-ttu-id="7ce27-144">Ele permite mapear nomes DNS para um nome de serviço e, portanto, resolver endereços IP do ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="7ce27-144">It enables you to map DNS names to a service name and hence resolve endpoint IP addresses.</span></span> 

<span data-ttu-id="7ce27-145">Conforme mostrado no diagrama a seguir, o serviço DNS, em execução no cluster do Service Fabric, mapeia nomes DNS para nomes de serviço que são então resolvidos pelo Serviço de Nomeação para retornar os endereços de ponto de extremidade aos quais se conectar.</span><span class="sxs-lookup"><span data-stu-id="7ce27-145">As shown in the following diagram, the DNS service, running in the Service Fabric cluster, maps DNS names to service names which are then resolved by the Naming Service to return the endpoint addresses to connect to.</span></span> <span data-ttu-id="7ce27-146">O nome DNS do serviço é fornecido no momento da criação.</span><span class="sxs-lookup"><span data-stu-id="7ce27-146">The DNS name for the service is provided at the time of creation.</span></span> 

![pontos de extremidade de serviço][9]

<span data-ttu-id="7ce27-148">Para obter mais detalhes sobre como usar o serviço DNS, consulte o artigo [Serviço DNS no Azure Service Fabric](service-fabric-dnsservice.md).</span><span class="sxs-lookup"><span data-stu-id="7ce27-148">For more details on how to use the DNS service see [DNS service in Azure Service Fabric](service-fabric-dnsservice.md) article.</span></span>

### <a name="reverse-proxy-service"></a><span data-ttu-id="7ce27-149">Serviço de proxy reverso</span><span class="sxs-lookup"><span data-stu-id="7ce27-149">Reverse proxy service</span></span>
<span data-ttu-id="7ce27-150">O proxy reverso lida com os serviços no cluster que expõem pontos de extremidade HTTP, incluindo HTTPS.</span><span class="sxs-lookup"><span data-stu-id="7ce27-150">The reverse proxy addresses services in the cluster that exposes HTTP endpoints including HTTPS.</span></span> <span data-ttu-id="7ce27-151">O proxy reverso simplifica grande parte da chamada a outros serviços e seus métodos tendo um formato de URI específico e manipula as etapas de resolução, conexão e repetição necessárias para que um serviço se comunique com outro usando o Serviço de Nomeação.</span><span class="sxs-lookup"><span data-stu-id="7ce27-151">The reverse proxy greatly simplifies calling other services and their methods by having a specific URI format and handles the resolve, connect, retry steps required for one service to communicate with another using the Naming Serivce.</span></span> <span data-ttu-id="7ce27-152">Em outras palavras, ele oculta o Serviço de Nomeação de você ao chamar outros serviços, fazendo com que isso fique tão simples quanto chamar uma URL.</span><span class="sxs-lookup"><span data-stu-id="7ce27-152">In other words, it hides the Naming Service from you when calling other services by making this as simple as calling a URL.</span></span>

![pontos de extremidade de serviço][10]

<span data-ttu-id="7ce27-154">Para obter mais detalhes sobre como usar o serviço de proxy reverso, consulte o artigo [Proxy reverso do Azure Service Fabric](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="7ce27-154">For more details on how to use the reverse proxy service see [Reverse proxy in Azure Service Fabric](service-fabric-reverseproxy.md) article.</span></span>

## <a name="connections-from-external-clients"></a><span data-ttu-id="7ce27-155">Conexões de clientes externos</span><span class="sxs-lookup"><span data-stu-id="7ce27-155">Connections from external clients</span></span>
<span data-ttu-id="7ce27-156">Geralmente, os serviços que se conectam entre si em um cluster podem acessar diretamente os pontos de extremidade de outros serviços, pois os nós de um cluster estão na mesma rede local.</span><span class="sxs-lookup"><span data-stu-id="7ce27-156">Services connecting to each other inside a cluster generally can directly access the endpoints of other services because the nodes in a cluster are on the same local network.</span></span> <span data-ttu-id="7ce27-157">Em alguns ambientes, entretanto, um cluster pode estar por trás de um balanceador de carga que encaminha o tráfego de entrada externo por meio de um conjunto limitado de portas.</span><span class="sxs-lookup"><span data-stu-id="7ce27-157">In some environments, however, a cluster may be behind a load balancer that routes external ingress traffic through a limited set of ports.</span></span> <span data-ttu-id="7ce27-158">Nesses casos, os serviços ainda poderão se comunicar e resolver endereços usando o Serviço de Nomenclatura, porém, etapas adicionais deverão ser executadas para permitir que clientes externos se conectem aos serviços.</span><span class="sxs-lookup"><span data-stu-id="7ce27-158">In these cases, services can still communicate with each other and resolve addresses using the Naming Service, but extra steps must be taken to allow external clients to connect to services.</span></span>

## <a name="service-fabric-in-azure"></a><span data-ttu-id="7ce27-159">Service Fabric no Azure</span><span class="sxs-lookup"><span data-stu-id="7ce27-159">Service Fabric in Azure</span></span>
<span data-ttu-id="7ce27-160">Um cluster do Service Fabric no Azure é colocado atrás de um Balanceador de Carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="7ce27-160">A Service Fabric cluster in Azure is placed behind an Azure Load Balancer.</span></span> <span data-ttu-id="7ce27-161">Todo o tráfego externo para o cluster deve passar pelo balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="7ce27-161">All external traffic to the cluster must pass through the load balancer.</span></span> <span data-ttu-id="7ce27-162">O balanceador de carga encaminhará automaticamente o tráfego de entrada em uma determinada porta para um *nó* aleatório que abriu a mesma porta.</span><span class="sxs-lookup"><span data-stu-id="7ce27-162">The load balancer will automatically forward traffic inbound on a given port to a random *node* that has the same port open.</span></span> <span data-ttu-id="7ce27-163">O Azure Load Balancer só conhece as portas abertas nos *nós*, ele não conhece portas abertas por *serviços* individuais.</span><span class="sxs-lookup"><span data-stu-id="7ce27-163">The Azure Load Balancer only knows about ports open on the *nodes*, it does not know about ports open by individual *services*.</span></span>

![Topologia do Balanceador de Carga do Azure e do Service Fabric][3]

<span data-ttu-id="7ce27-165">Por exemplo, para aceitar o tráfego externo na porta **80**, configure os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="7ce27-165">For example, in order to accept external traffic on port **80**, the following things must be configured:</span></span>

1. <span data-ttu-id="7ce27-166">Escreva um serviço que escute na porta 80.</span><span class="sxs-lookup"><span data-stu-id="7ce27-166">Write a service that listens on port 80.</span></span> <span data-ttu-id="7ce27-167">Configure a porta 80 no ServiceManifest.xml do serviço e abra um ouvinte no serviço, por exemplo, um servidor Web auto-hospedado.</span><span class="sxs-lookup"><span data-stu-id="7ce27-167">Configure port 80 in the service's ServiceManifest.xml and open a listener in the service, for example, a self-hosted web server.</span></span>

    ```xml
    <Resources>
        <Endpoints>
            <Endpoint Name="WebEndpoint" Protocol="http" Port="80" />
        </Endpoints>
    </Resources>
    ```
    ```csharp
        class HttpCommunicationListener : ICommunicationListener
        {
            ...

            public Task<string> OpenAsync(CancellationToken cancellationToken)
            {
                EndpointResourceDescription endpoint =
                    serviceContext.CodePackageActivationContext.GetEndpoint("WebEndpoint");

                string uriPrefix = $"{endpoint.Protocol}://+:{endpoint.Port}/myapp/";

                this.httpListener = new HttpListener();
                this.httpListener.Prefixes.Add(uriPrefix);
                this.httpListener.Start();

                string publishUri = uriPrefix.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);
                return Task.FromResult(publishUri);
            }

            ...
        }

        class WebService : StatelessService
        {
            ...

            protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
            {
                return new[] { new ServiceInstanceListener(context => new HttpCommunicationListener(context))};
            }

            ...
        }
    ```
    ```java
        class HttpCommunicationlistener implements CommunicationListener {
            ...

            @Override
            public CompletableFuture<String> openAsync(CancellationToken arg0) {
                EndpointResourceDescription endpoint =
                    this.serviceContext.getCodePackageActivationContext().getEndpoint("WebEndpoint");
                try {
                    HttpServer server = com.sun.net.httpserver.HttpServer.create(new InetSocketAddress(endpoint.getPort()), 0);
                    server.start();

                    String publishUri = String.format("http://%s:%d/",
                        this.serviceContext.getNodeContext().getIpAddressOrFQDN(), endpoint.getPort());
                    return CompletableFuture.completedFuture(publishUri);
                } catch (IOException e) {
                    throw new RuntimeException(e);
                }
            }

            ...
        }

        class WebService extends StatelessService {
            ...

            @Override
            protected List<ServiceInstanceListener> createServiceInstanceListeners() {
                <ServiceInstanceListener> listeners = new ArrayList<ServiceInstanceListener>();
                listeners.add(new ServiceInstanceListener((context) -> new HttpCommunicationlistener(context)));
                return listeners;       
            }

            ...
        }
    ```
2. <span data-ttu-id="7ce27-168">Crie um Cluster do Service Fabric no Azure e especifique a porta **80** como uma porta de ponto de extremidade personalizado para o tipo de nó que vai hospedar o serviço.</span><span class="sxs-lookup"><span data-stu-id="7ce27-168">Create a Service Fabric Cluster in Azure and specify port **80** as a custom endpoint port for the node type that will host the service.</span></span> <span data-ttu-id="7ce27-169">Se você tiver mais de um tipo de nó, configure uma *restrição de posicionamento* no serviço para assegurar que ele só seja executado no tipo de nó que tem a porta de ponto de extremidade personalizado aberta.</span><span class="sxs-lookup"><span data-stu-id="7ce27-169">If you have more than one node type, you can set up a *placement constraint* on the service to ensure it only runs on the node type that has the custom endpoint port opened.</span></span>

    ![Abrir uma porta em um tipo de nó][4]
3. <span data-ttu-id="7ce27-171">Após o cluster ter sido criado, configure o Balanceador de Carga do Azure no Grupo de Recursos do cluster para encaminhar o tráfego na porta 80.</span><span class="sxs-lookup"><span data-stu-id="7ce27-171">Once the cluster has been created, configure the Azure Load Balancer in the cluster's Resource Group to forward traffic on port 80.</span></span> <span data-ttu-id="7ce27-172">Ao criar um cluster por meio do Portal do Azure, isso é configurado automaticamente para cada porta de ponto de extremidade personalizado que foi configurada.</span><span class="sxs-lookup"><span data-stu-id="7ce27-172">When creating a cluster through the Azure portal, this is set up automatically for each custom endpoint port that was configured.</span></span>

    ![Encaminhar o tráfego no Balanceador de Carga do Azure][5]
4. <span data-ttu-id="7ce27-174">O Balanceador de Carga do Azure usa uma investigação para determinar deve enviar ou não o tráfego para um nó específico.</span><span class="sxs-lookup"><span data-stu-id="7ce27-174">The Azure Load Balancer uses a probe to determine whether or not to send traffic to a particular node.</span></span> <span data-ttu-id="7ce27-175">A investigação verifica periodicamente um ponto de extremidade em cada nó para determinar se o nó está respondendo ou não.</span><span class="sxs-lookup"><span data-stu-id="7ce27-175">The probe periodically checks an endpoint on each node to determine whether or not the node is responding.</span></span> <span data-ttu-id="7ce27-176">Se a investigação não receber uma resposta após um número de vezes configurado, o balanceador de carga interromperá o envio de tráfego para esse nó.</span><span class="sxs-lookup"><span data-stu-id="7ce27-176">If the probe fails to receive a response after a configured number of times, the load balancer stops sending traffic to that node.</span></span> <span data-ttu-id="7ce27-177">Ao criar um cluster por meio do Portal do Azure, uma investigação é definida automaticamente para cada porta de ponto de extremidade personalizado que foi configurada.</span><span class="sxs-lookup"><span data-stu-id="7ce27-177">When creating a cluster through the Azure portal, a probe is automatically set up for each custom endpoint port that was configured.</span></span>

    ![Encaminhar o tráfego no Balanceador de Carga do Azure][8]

<span data-ttu-id="7ce27-179">É importante lembrar que o Azure Load Balancer e a investigação só conhecem os *nós*, não os *serviços* em execução nos nós.</span><span class="sxs-lookup"><span data-stu-id="7ce27-179">It's important to remember that the Azure Load Balancer and the probe only know about the *nodes*, not the *services* running on the nodes.</span></span> <span data-ttu-id="7ce27-180">O Balanceador de Carga do Azure sempre enviará tráfego para os nós que responderem à investigação, portanto tome cuidado para garantir que os serviços estão disponíveis em nós que podem responder à investigação.</span><span class="sxs-lookup"><span data-stu-id="7ce27-180">The Azure Load Balancer will always send traffic to nodes that respond to the probe, so care must be taken to ensure services are available on the nodes that are able to respond to the probe.</span></span>

## <a name="reliable-services-built-in-communication-api-options"></a><span data-ttu-id="7ce27-181">Reliable Services: Opções de API de comunicação interna</span><span class="sxs-lookup"><span data-stu-id="7ce27-181">Reliable Services: Built-in communication API options</span></span>
<span data-ttu-id="7ce27-182">A estrutura do Reliable Services vem com várias opções de comunicação predefinidas.</span><span class="sxs-lookup"><span data-stu-id="7ce27-182">The Reliable Services framework ships with several pre-built communication options.</span></span> <span data-ttu-id="7ce27-183">A decisão sobre qual uma funcionará melhor para você depende da escolha do modelo de programação, da estrutura de comunicação e da linguagem de programação em que os serviços são escritos.</span><span class="sxs-lookup"><span data-stu-id="7ce27-183">The decision about which one will work best for you depends on the choice of the programming model, the communication framework, and the programming language that your services are written in.</span></span>

* <span data-ttu-id="7ce27-184">**Nenhum protocolo específico:** se você não tiver uma preferência específica de estrutura de comunicação, mas desejar colocar algo em funcionamento rapidamente, a opção ideal para você será a [comunicação remota do serviço](service-fabric-reliable-services-communication-remoting.md), que possibilita chamadas de procedimento remoto fortemente tipadas para os Reliable Services e Reliable Actors.</span><span class="sxs-lookup"><span data-stu-id="7ce27-184">**No specific protocol:**  If you don't have a particular choice of communication framework, but you want to get something up and running quickly, then the ideal option for you is [service remoting](service-fabric-reliable-services-communication-remoting.md), which allows strongly-typed remote procedure calls for Reliable Services and Reliable Actors.</span></span> <span data-ttu-id="7ce27-185">Essa é a maneira mais fácil e rápida de começar a comunicação de serviço.</span><span class="sxs-lookup"><span data-stu-id="7ce27-185">This is the easiest and fastest way to get started with service communication.</span></span> <span data-ttu-id="7ce27-186">A comunicação remota do serviço lida com a resolução de endereços de serviço, conexão, repetição e tratamento de erro.</span><span class="sxs-lookup"><span data-stu-id="7ce27-186">Service remoting handles resolution of service addresses, connection, retry, and error handling.</span></span> <span data-ttu-id="7ce27-187">Isso está disponível para aplicativos Java e C#.</span><span class="sxs-lookup"><span data-stu-id="7ce27-187">This is available for both C# and Java applications.</span></span>
* <span data-ttu-id="7ce27-188">**HTTP**: para comunicação independente de idioma, o HTTP fornece uma opção padrão do setor com ferramentas e servidores HTTP disponíveis em várias linguagens diferentes, tudo isso com suporte no Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7ce27-188">**HTTP**: For language-agnostic communication, HTTP provides an industry-standard choice with tools and HTTP servers available in many different languages, all supported by Service Fabric.</span></span> <span data-ttu-id="7ce27-189">Os serviços podem usar qualquer pilha HTTP disponível, incluindo [API Web ASP.NET](service-fabric-reliable-services-communication-webapi.md) para aplicativos C#.</span><span class="sxs-lookup"><span data-stu-id="7ce27-189">Services can use any HTTP stack available, including [ASP.NET Web API](service-fabric-reliable-services-communication-webapi.md) for C# applications.</span></span> <span data-ttu-id="7ce27-190">Clientes escritos em C# podem aproveitar as classes `ICommunicationClient` e `ServicePartitionClient`, enquanto para Java, use as classes `CommunicationClient` e `FabricServicePartitionClient` [para resolução de serviço, conexões HTTP e loops de repetição](service-fabric-reliable-services-communication.md).</span><span class="sxs-lookup"><span data-stu-id="7ce27-190">Clients written in C# can leverage the `ICommunicationClient` and `ServicePartitionClient` classes, whereas for Java, use the `CommunicationClient` and `FabricServicePartitionClient` classes, [for service resolution, HTTP connections, and retry loops](service-fabric-reliable-services-communication.md).</span></span>
* <span data-ttu-id="7ce27-191">**WCF**: se você tiver um código existente que use WCF como estrutura de comunicação, poderá usar o `WcfCommunicationListener` para o lado do servidor e as classes `WcfCommunicationClient` e `ServicePartitionClient` para o cliente.</span><span class="sxs-lookup"><span data-stu-id="7ce27-191">**WCF**: If you have existing code that uses WCF as your communication framework, then you can use the `WcfCommunicationListener` for the server side and `WcfCommunicationClient` and `ServicePartitionClient` classes for the client.</span></span> <span data-ttu-id="7ce27-192">No entanto, isso só está disponível para aplicativos C# em clusters baseados no Windows.</span><span class="sxs-lookup"><span data-stu-id="7ce27-192">This however is only available for C# applications on Windows based clusters.</span></span> <span data-ttu-id="7ce27-193">Para obter mais detalhes, consulte este artigo sobre [implementação baseada no WCF da pilha de comunicação](service-fabric-reliable-services-communication-wcf.md).</span><span class="sxs-lookup"><span data-stu-id="7ce27-193">For more details, see this article about [WCF-based implementation of the communication stack](service-fabric-reliable-services-communication-wcf.md).</span></span>

## <a name="using-custom-protocols-and-other-communication-frameworks"></a><span data-ttu-id="7ce27-194">Usando protocolos personalizados e outras estruturas de comunicação</span><span class="sxs-lookup"><span data-stu-id="7ce27-194">Using custom protocols and other communication frameworks</span></span>
<span data-ttu-id="7ce27-195">Os serviços poderão usar qualquer protocolo ou estrutura para comunicação, independentemente de esse ser um protocolo binário personalizado via soquetes TCP ou eventos de streaming por meio de [Hubs de Eventos do Azure](https://azure.microsoft.com/services/event-hubs/) ou [Hub IoT do Azure](https://azure.microsoft.com/services/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="7ce27-195">Services can use any protocol or framework for communication, whether its a custom binary protocol over TCP sockets, or streaming events through [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) or [Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/).</span></span> <span data-ttu-id="7ce27-196">O Service Fabric fornece APIs de comunicação aos quais você pode conectar sua pilha de comunicação, enquanto todo o trabalho de descoberta e conexão é omitido.</span><span class="sxs-lookup"><span data-stu-id="7ce27-196">Service Fabric provides communication APIs that you can plug your communication stack into, while all the work to discover and connect is abstracted from you.</span></span> <span data-ttu-id="7ce27-197">Consulte este artigo sobre o [modelo de comunicação de serviço confiável](service-fabric-reliable-services-communication.md) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="7ce27-197">See this article about the [Reliable Service communication model](service-fabric-reliable-services-communication.md) for more details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ce27-198">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7ce27-198">Next steps</span></span>
<span data-ttu-id="7ce27-199">Saiba mais sobre os conceitos e as APIs disponíveis no [modelo de comunicação dos Reliable Services](service-fabric-reliable-services-communication.md) e começar rapidamente com a [comunicação remota do serviço](service-fabric-reliable-services-communication-remoting.md) ou aprofunde-se para aprender a escrever um ouvinte de comunicação usando [API da Web com auto-hospedagem de OWIN](service-fabric-reliable-services-communication-webapi.md).</span><span class="sxs-lookup"><span data-stu-id="7ce27-199">Learn more about the concepts and APIs available in the [Reliable Services communication model](service-fabric-reliable-services-communication.md), then get started quickly with [service remoting](service-fabric-reliable-services-communication-remoting.md) or go in-depth to learn how to write a communication listener using [Web API with OWIN self-host](service-fabric-reliable-services-communication-webapi.md).</span></span>

[1]: ./media/service-fabric-connect-and-communicate-with-services/serviceendpoints.png
[2]: ./media/service-fabric-connect-and-communicate-with-services/namingservice.png
[3]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancertopology.png
[4]: ./media/service-fabric-connect-and-communicate-with-services/nodeport.png
[5]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerport.png
[7]: ./media/service-fabric-connect-and-communicate-with-services/distributedservices.png
[8]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerprobe.png
[9]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[10]: ./media/service-fabric-reverseproxy/internal-communication.png
