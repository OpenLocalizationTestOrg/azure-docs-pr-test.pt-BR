---
title: "aaaConnect e se comunicar com os serviços do Azure Service Fabric | Microsoft Docs"
description: "Saiba como tooresolve, conecte-se e comunicar-se com os serviços do Service Fabric."
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
ms.openlocfilehash: b8b374a71d4c5d21f48a560a3a8c81b357fe418d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-and-communicate-with-services-in-service-fabric"></a><span data-ttu-id="78612-103">Conectar e se comunicar com serviços no Service Fabric</span><span class="sxs-lookup"><span data-stu-id="78612-103">Connect and communicate with services in Service Fabric</span></span>
<span data-ttu-id="78612-104">No Service Fabric, um serviço é executado em algum lugar em um cluster do Service Fabric, normalmente distribuído entre várias VMs.</span><span class="sxs-lookup"><span data-stu-id="78612-104">In Service Fabric, a service runs somewhere in a Service Fabric cluster, typically distributed across multiple VMs.</span></span> <span data-ttu-id="78612-105">Ele pode ser movido de tooanother de um só lugar, ao proprietário do serviço hello ou automaticamente pela malha do serviço.</span><span class="sxs-lookup"><span data-stu-id="78612-105">It can be moved from one place tooanother, either by hello service owner, or automatically by Service Fabric.</span></span> <span data-ttu-id="78612-106">Os serviços não são tooa estaticamente empatados determinado computador ou endereço.</span><span class="sxs-lookup"><span data-stu-id="78612-106">Services are not statically tied tooa particular machine or address.</span></span>

<span data-ttu-id="78612-107">Um aplicativo do Service Fabric geralmente é composto por vários serviços diferentes, em que cada serviço executa uma tarefa específica.</span><span class="sxs-lookup"><span data-stu-id="78612-107">A Service Fabric application is generally composed of many different services, where each service performs a specialized task.</span></span> <span data-ttu-id="78612-108">Esses serviços podem se comunicar com outro tooform uma função completa, como partes diferentes de renderização de um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="78612-108">These services may communicate with each other tooform a complete function, such as rendering different parts of a web application.</span></span> <span data-ttu-id="78612-109">Também há aplicativos que se conectam tooand se comunicar com serviços de cliente.</span><span class="sxs-lookup"><span data-stu-id="78612-109">There are also client applications that connect tooand communicate with services.</span></span> <span data-ttu-id="78612-110">Este documento aborda como tooset a comunicação com o e entre os serviços na malha do serviço.</span><span class="sxs-lookup"><span data-stu-id="78612-110">This document discusses how tooset up communication with and between your services in Service Fabric.</span></span>

<span data-ttu-id="78612-111">Este vídeo da Microsoft Virtual Academy também discute a comunicação de serviço: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=iYFCk76yC_6706218965"></span><span class="sxs-lookup"><span data-stu-id="78612-111">This Microsoft Virtual Academy video also discusses service communication: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=iYFCk76yC_6706218965"></span></span>  
<img src="./media/service-fabric-connect-and-communicate-with-services/CommunicationVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="bring-your-own-protocol"></a><span data-ttu-id="78612-112">Trazer seu próprio protocolo</span><span class="sxs-lookup"><span data-stu-id="78612-112">Bring your own protocol</span></span>
<span data-ttu-id="78612-113">Service Fabric ajuda a gerenciar a saudação do ciclo de vida dos serviços de, mas ele não tomar decisões sobre o que fazem seus serviços.</span><span class="sxs-lookup"><span data-stu-id="78612-113">Service Fabric helps manage hello lifecycle of your services but it does not make decisions about what your services do.</span></span> <span data-ttu-id="78612-114">Isso inclui a comunicação.</span><span class="sxs-lookup"><span data-stu-id="78612-114">This includes communication.</span></span> <span data-ttu-id="78612-115">Quando o serviço for aberto pelo serviço de malha, que é tooset de oportunidade do serviço a um ponto de extremidade para solicitações de entrada, usando qualquer pilha de comunicação ou protocolo desejado.</span><span class="sxs-lookup"><span data-stu-id="78612-115">When your service is opened by Service Fabric, that's your service's opportunity tooset up an endpoint for incoming requests, using whatever protocol or communication stack you want.</span></span> <span data-ttu-id="78612-116">O serviço escutará um endereço **IP:port** normal usando qualquer esquema de endereçamento, como um URI.</span><span class="sxs-lookup"><span data-stu-id="78612-116">Your service will listen on a normal **IP:port** address using any addressing scheme, such as a URI.</span></span> <span data-ttu-id="78612-117">Várias instâncias de serviço ou réplicas podem compartilhar um processo de host, caso em que eles serão necessário toouse diferentes portas ou use um mecanismo de compartilhamento de porta, como o driver de kernel HTTP. sys Olá no Windows.</span><span class="sxs-lookup"><span data-stu-id="78612-117">Multiple service instances or replicas may share a host process, in which case they will either need toouse different ports or use a port-sharing mechanism, such as hello http.sys kernel driver in Windows.</span></span> <span data-ttu-id="78612-118">Em ambos os casos, cada instância de serviço ou réplica em um processo de host deve ser endereçável exclusivamente.</span><span class="sxs-lookup"><span data-stu-id="78612-118">In either case, each service instance or replica in a host process must be uniquely addressable.</span></span>

![pontos de extremidade de serviço][1]

## <a name="service-discovery-and-resolution"></a><span data-ttu-id="78612-120">Resolução e descoberta de serviço</span><span class="sxs-lookup"><span data-stu-id="78612-120">Service discovery and resolution</span></span>
<span data-ttu-id="78612-121">Em um sistema distribuído, serviços podem mover de uma máquina tooanother ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="78612-121">In a distributed system, services may move from one machine tooanother over time.</span></span> <span data-ttu-id="78612-122">Isso pode ocorrer por vários motivos, incluindo balanceamento de recursos, atualizações, failovers ou escala horizontal. Isso significa alterar de endereços de ponto de extremidade de serviço como serviço de saudação move toonodes com endereços IP diferentes e pode abrir portas diferentes se o serviço Olá usa uma porta dinamicamente selecionada.</span><span class="sxs-lookup"><span data-stu-id="78612-122">This can happen for various reasons, including resource balancing, upgrades, failovers, or scale-out. This means service endpoint addresses change as hello service moves toonodes with different IP addresses, and may open on different ports if hello service uses a dynamically selected port.</span></span>

![Distribuição de serviços][7]

<span data-ttu-id="78612-124">Serviço de malha fornece uma detecção e resolução de serviço chamado hello Naming Service.</span><span class="sxs-lookup"><span data-stu-id="78612-124">Service Fabric provides a discovery and resolution service called hello Naming Service.</span></span> <span data-ttu-id="78612-125">Olá Naming Service mantém uma tabela que mapeia endereços de ponto de extremidade toohello escutam em instâncias de serviço chamado.</span><span class="sxs-lookup"><span data-stu-id="78612-125">hello Naming Service maintains a table that maps named service instances toohello endpoint addresses they listen on.</span></span> <span data-ttu-id="78612-126">Todas as instâncias de serviço nomeadas do Service Fabric têm nomes exclusivos representados como URIs, como por exemplo, `"fabric:/MyApplication/MyService"`.</span><span class="sxs-lookup"><span data-stu-id="78612-126">All named service instances in Service Fabric have unique names represented as URIs, for example, `"fabric:/MyApplication/MyService"`.</span></span> <span data-ttu-id="78612-127">nome de saudação do serviço de saudação não é alterado em tempo de vida de saudação do serviço Olá, é somente endereços de ponto de extremidade Olá que podem ser alterados quando mover serviços.</span><span class="sxs-lookup"><span data-stu-id="78612-127">hello name of hello service does not change over hello lifetime of hello service, it's only hello endpoint addresses that can change when services move.</span></span> <span data-ttu-id="78612-128">Isso é análogo toowebsites que têm URLs constantes mas onde pode alterar o endereço IP hello.</span><span class="sxs-lookup"><span data-stu-id="78612-128">This is analogous toowebsites that have constant URLs but where hello IP address may change.</span></span> <span data-ttu-id="78612-129">E tooDNS semelhante na web hello, que resolve endereços de tooIP de URLs de sites, o Service Fabric tem um registrador que mapeia o endereço de ponto de extremidade do serviço nomes tootheir.</span><span class="sxs-lookup"><span data-stu-id="78612-129">And similar tooDNS on hello web, which resolves website URLs tooIP addresses, Service Fabric has a registrar that maps service names tootheir endpoint address.</span></span>

![pontos de extremidade de serviço][2]

<span data-ttu-id="78612-131">Resolvendo e conectar-se tooservices envolvem Olá executadas em um loop de etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="78612-131">Resolving and connecting tooservices involves hello following steps run in a loop:</span></span>

* <span data-ttu-id="78612-132">**Resolver**: ponto de extremidade de saudação de Get que publicou um serviço de Olá Naming Service.</span><span class="sxs-lookup"><span data-stu-id="78612-132">**Resolve**: Get hello endpoint that a service has published from hello Naming Service.</span></span>
* <span data-ttu-id="78612-133">**Conecte-se**: conectar-se o serviço toohello sobre o protocolo usa nesse ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="78612-133">**Connect**: Connect toohello service over whatever protocol it uses on that endpoint.</span></span>
* <span data-ttu-id="78612-134">**Repita**: uma tentativa de conexão pode falhar por vários motivos, por exemplo, se o serviço Olá foi movido desde que o endereço de ponto de extremidade de saudação do hello última hora foi resolvido.</span><span class="sxs-lookup"><span data-stu-id="78612-134">**Retry**: A connection attempt may fail for any number of reasons, for example if hello service has moved since hello last time hello endpoint address was resolved.</span></span> <span data-ttu-id="78612-135">Nesse caso, Olá anteriores resolver e conecte-se etapas necessário toobe repetida e o ciclo se repete até que a conexão de saudação for bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="78612-135">In that case, hello preceding resolve and connect steps need toobe retried, and this cycle is repeated until hello connection succeeds.</span></span>

## <a name="connecting-tooother-services"></a><span data-ttu-id="78612-136">Conectando a serviços tooother</span><span class="sxs-lookup"><span data-stu-id="78612-136">Connecting tooother services</span></span>
<span data-ttu-id="78612-137">Serviços conectando tooeach outros dentro de um cluster geralmente pode acessar diretamente os pontos de extremidade de saudação de outros serviços porque nós Olá em um cluster em Olá mesma rede local.</span><span class="sxs-lookup"><span data-stu-id="78612-137">Services connecting tooeach other inside a cluster generally can directly access hello endpoints of other services because hello nodes in a cluster are on hello same local network.</span></span> <span data-ttu-id="78612-138">toomake é mais fácil tooconnect entre serviços, Service Fabric fornece serviços adicionais que usam Olá Naming Service.</span><span class="sxs-lookup"><span data-stu-id="78612-138">toomake is easier tooconnect between services, Service Fabric provides additional services that use hello Naming Service.</span></span> <span data-ttu-id="78612-139">Um serviço DNS e um serviço de proxy reverso.</span><span class="sxs-lookup"><span data-stu-id="78612-139">A DNS service and a reverse proxy service.</span></span>


### <a name="dns-service"></a><span data-ttu-id="78612-140">Serviço DNS</span><span class="sxs-lookup"><span data-stu-id="78612-140">DNS service</span></span>
<span data-ttu-id="78612-141">Como muitos serviços, especialmente em contêineres services, podem ter um nome de URL existente, capaz de tooresolve esses usando Olá protocolo DNS padrão (em vez de protocolo de serviço de nomes de saudação) é muito convenientes, especialmente no aplicativo "comparar e deslocar" cenários.</span><span class="sxs-lookup"><span data-stu-id="78612-141">Since many services, especially containerized services, can have an existing URL name, being able tooresolve these using hello standard DNS protocol (rather than hello Naming Service protocol) is very convenient, especially in application "lift and shift" scenarios.</span></span> <span data-ttu-id="78612-142">Isso é exatamente qual serviço DNS Olá faz.</span><span class="sxs-lookup"><span data-stu-id="78612-142">This is exactly what hello DNS service does.</span></span> <span data-ttu-id="78612-143">Ele permite que você toomap DNS nomes tooa nome do serviço e, portanto, resolver endereços IP do ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="78612-143">It enables you toomap DNS names tooa service name and hence resolve endpoint IP addresses.</span></span> 

<span data-ttu-id="78612-144">Como Olá mostrada no diagrama a seguir, Olá serviço DNS, em execução no cluster do Service Fabric hello, mapeia os nomes de tooservice de nomes DNS que são resolvidos pela Olá Naming Service tooreturn Olá ponto de extremidade endereços tooconnect para.</span><span class="sxs-lookup"><span data-stu-id="78612-144">As shown in hello following diagram, hello DNS service, running in hello Service Fabric cluster, maps DNS names tooservice names which are then resolved by hello Naming Service tooreturn hello endpoint addresses tooconnect to.</span></span> <span data-ttu-id="78612-145">nome DNS de saudação para serviço de saudação é fornecido no momento de saudação da criação.</span><span class="sxs-lookup"><span data-stu-id="78612-145">hello DNS name for hello service is provided at hello time of creation.</span></span> 

![pontos de extremidade de serviço][9]

<span data-ttu-id="78612-147">Para obter mais detalhes sobre como ver toouse Olá serviço DNS [serviço DNS no Azure Service Fabric](service-fabric-dnsservice.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="78612-147">For more details on how toouse hello DNS service see [DNS service in Azure Service Fabric](service-fabric-dnsservice.md) article.</span></span>

### <a name="reverse-proxy-service"></a><span data-ttu-id="78612-148">Serviço de proxy reverso</span><span class="sxs-lookup"><span data-stu-id="78612-148">Reverse proxy service</span></span>
<span data-ttu-id="78612-149">proxy reverso Olá endereços serviços em cluster Olá que expõe pontos de extremidade HTTP incluindo HTTPS.</span><span class="sxs-lookup"><span data-stu-id="78612-149">hello reverse proxy addresses services in hello cluster that exposes HTTP endpoints including HTTPS.</span></span> <span data-ttu-id="78612-150">proxy reverso Olá simplifica bastante a chamada de outros serviços e seus métodos fazendo com que um determinado formato de URI e identificadores Olá resolver, conecte-se, etapas de repetição necessárias para um serviço toocommunicate com outro usando Olá serviço de nomenclatura.</span><span class="sxs-lookup"><span data-stu-id="78612-150">hello reverse proxy greatly simplifies calling other services and their methods by having a specific URI format and handles hello resolve, connect, retry steps required for one service toocommunicate with another using hello Naming Serivce.</span></span> <span data-ttu-id="78612-151">Em outras palavras, ele oculta Olá Naming Service você ao chamar outros serviços, tornando isso tão simples quanto chamar uma URL.</span><span class="sxs-lookup"><span data-stu-id="78612-151">In other words, it hides hello Naming Service from you when calling other services by making this as simple as calling a URL.</span></span>

![pontos de extremidade de serviço][10]

<span data-ttu-id="78612-153">Para obter mais detalhes sobre como toouse Olá reverter o serviço de proxy, consulte [proxy no Azure Service Fabric reverso](service-fabric-reverseproxy.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="78612-153">For more details on how toouse hello reverse proxy service see [Reverse proxy in Azure Service Fabric](service-fabric-reverseproxy.md) article.</span></span>

## <a name="connections-from-external-clients"></a><span data-ttu-id="78612-154">Conexões de clientes externos</span><span class="sxs-lookup"><span data-stu-id="78612-154">Connections from external clients</span></span>
<span data-ttu-id="78612-155">Serviços conectando tooeach outros dentro de um cluster geralmente pode acessar diretamente os pontos de extremidade de saudação de outros serviços porque nós Olá em um cluster em Olá mesma rede local.</span><span class="sxs-lookup"><span data-stu-id="78612-155">Services connecting tooeach other inside a cluster generally can directly access hello endpoints of other services because hello nodes in a cluster are on hello same local network.</span></span> <span data-ttu-id="78612-156">Em alguns ambientes, entretanto, um cluster pode estar por trás de um balanceador de carga que encaminha o tráfego de entrada externo por meio de um conjunto limitado de portas.</span><span class="sxs-lookup"><span data-stu-id="78612-156">In some environments, however, a cluster may be behind a load balancer that routes external ingress traffic through a limited set of ports.</span></span> <span data-ttu-id="78612-157">Nesses casos, os serviços ainda podem se comunicar entre si e resolver endereços usando Olá Naming Service, mas etapas adicionais devem ser feitos tooallow clientes externos tooconnect tooservices.</span><span class="sxs-lookup"><span data-stu-id="78612-157">In these cases, services can still communicate with each other and resolve addresses using hello Naming Service, but extra steps must be taken tooallow external clients tooconnect tooservices.</span></span>

## <a name="service-fabric-in-azure"></a><span data-ttu-id="78612-158">Service Fabric no Azure</span><span class="sxs-lookup"><span data-stu-id="78612-158">Service Fabric in Azure</span></span>
<span data-ttu-id="78612-159">Um cluster do Service Fabric no Azure é colocado atrás de um Balanceador de Carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="78612-159">A Service Fabric cluster in Azure is placed behind an Azure Load Balancer.</span></span> <span data-ttu-id="78612-160">Cluster de toohello todos os tráfego externo deve passar pelo Balanceador de carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="78612-160">All external traffic toohello cluster must pass through hello load balancer.</span></span> <span data-ttu-id="78612-161">Olá balanceador de carga será automaticamente encaminhar tráfego entrada em um tooa porta aleatória *nó* com hello mesma porta aberta.</span><span class="sxs-lookup"><span data-stu-id="78612-161">hello load balancer will automatically forward traffic inbound on a given port tooa random *node* that has hello same port open.</span></span> <span data-ttu-id="78612-162">Olá balanceador de carga do Azure só conhece portas abertas em Olá *nós*, ele não sabe sobre a abertura de portas por indivíduo *serviços*.</span><span class="sxs-lookup"><span data-stu-id="78612-162">hello Azure Load Balancer only knows about ports open on hello *nodes*, it does not know about ports open by individual *services*.</span></span>

![Topologia do Balanceador de Carga do Azure e do Service Fabric][3]

<span data-ttu-id="78612-164">Por exemplo, no tráfego externo de ordem tooaccept na porta **80**, Olá coisas a seguir deve ser configurado:</span><span class="sxs-lookup"><span data-stu-id="78612-164">For example, in order tooaccept external traffic on port **80**, hello following things must be configured:</span></span>

1. <span data-ttu-id="78612-165">Escreva um serviço que escute na porta 80.</span><span class="sxs-lookup"><span data-stu-id="78612-165">Write a service that listens on port 80.</span></span> <span data-ttu-id="78612-166">Configurar a porta 80 em ServiceManifest.xml do serviço hello e abra um ouvinte no serviço hello, por exemplo, um servidor web auto-hospedado.</span><span class="sxs-lookup"><span data-stu-id="78612-166">Configure port 80 in hello service's ServiceManifest.xml and open a listener in hello service, for example, a self-hosted web server.</span></span>

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
2. <span data-ttu-id="78612-167">Criar um Cluster de malha do serviço no Azure e especifique a porta **80** como uma porta de ponto de extremidade personalizado para o tipo de nó Olá que irá hospedar o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="78612-167">Create a Service Fabric Cluster in Azure and specify port **80** as a custom endpoint port for hello node type that will host hello service.</span></span> <span data-ttu-id="78612-168">Se você tiver mais de um tipo de nó, você pode configurar um *restrição de posicionamento* em Olá serviço tooensure só é executado no tipo de nó de saudação que tem a porta do ponto de extremidade personalizado Olá aberta.</span><span class="sxs-lookup"><span data-stu-id="78612-168">If you have more than one node type, you can set up a *placement constraint* on hello service tooensure it only runs on hello node type that has hello custom endpoint port opened.</span></span>

    ![Abrir uma porta em um tipo de nó][4]
3. <span data-ttu-id="78612-170">Uma vez Olá cluster foi criado, configure hello Azure balanceador de carga no tráfego de tooforward de grupo de recursos do cluster Olá na porta 80.</span><span class="sxs-lookup"><span data-stu-id="78612-170">Once hello cluster has been created, configure hello Azure Load Balancer in hello cluster's Resource Group tooforward traffic on port 80.</span></span> <span data-ttu-id="78612-171">Ao criar um cluster por meio de saudação portal do Azure, isso é configurar automaticamente para cada porta do ponto de extremidade personalizado que foi configurada.</span><span class="sxs-lookup"><span data-stu-id="78612-171">When creating a cluster through hello Azure portal, this is set up automatically for each custom endpoint port that was configured.</span></span>

    ![Encaminhar o tráfego Olá balanceador de carga do Azure][5]
4. <span data-ttu-id="78612-173">Olá usa o balanceador de carga do Azure toodetermine uma investigação se ou não toosend tooa determinado nó de tráfego.</span><span class="sxs-lookup"><span data-stu-id="78612-173">hello Azure Load Balancer uses a probe toodetermine whether or not toosend traffic tooa particular node.</span></span> <span data-ttu-id="78612-174">Olá teste periodicamente verifica um ponto de extremidade em cada toodetermine de nó ou não o nó de saudação está respondendo.</span><span class="sxs-lookup"><span data-stu-id="78612-174">hello probe periodically checks an endpoint on each node toodetermine whether or not hello node is responding.</span></span> <span data-ttu-id="78612-175">Se a investigação de saudação falhar tooreceive uma resposta após um determinado número de vezes, balanceador de carga Olá interromperá o envio de nó de toothat de tráfego.</span><span class="sxs-lookup"><span data-stu-id="78612-175">If hello probe fails tooreceive a response after a configured number of times, hello load balancer stops sending traffic toothat node.</span></span> <span data-ttu-id="78612-176">Ao criar um cluster por meio de saudação portal do Azure, uma investigação é configurada automaticamente para cada porta do ponto de extremidade personalizado que foi configurada.</span><span class="sxs-lookup"><span data-stu-id="78612-176">When creating a cluster through hello Azure portal, a probe is automatically set up for each custom endpoint port that was configured.</span></span>

    ![Encaminhar o tráfego Olá balanceador de carga do Azure][8]

<span data-ttu-id="78612-178">É importante tooremember que hello balanceador de carga do Azure e investigação Olá só conhecem Olá *nós*, Olá não *serviços* em execução em nós de saudação.</span><span class="sxs-lookup"><span data-stu-id="78612-178">It's important tooremember that hello Azure Load Balancer and hello probe only know about hello *nodes*, not hello *services* running on hello nodes.</span></span> <span data-ttu-id="78612-179">Olá balanceador de carga do Azure sempre enviará tráfego toonodes que respondem a investigação de toohello, portanto deve ter cuidado tooensure serviços estão disponíveis em nós de saudação que são capazes de toorespond toohello investigação.</span><span class="sxs-lookup"><span data-stu-id="78612-179">hello Azure Load Balancer will always send traffic toonodes that respond toohello probe, so care must be taken tooensure services are available on hello nodes that are able toorespond toohello probe.</span></span>

## <a name="reliable-services-built-in-communication-api-options"></a><span data-ttu-id="78612-180">Reliable Services: Opções de API de comunicação interna</span><span class="sxs-lookup"><span data-stu-id="78612-180">Reliable Services: Built-in communication API options</span></span>
<span data-ttu-id="78612-181">estrutura de serviços confiáveis Olá é fornecido com várias opções de comunicação pré-criado.</span><span class="sxs-lookup"><span data-stu-id="78612-181">hello Reliable Services framework ships with several pre-built communication options.</span></span> <span data-ttu-id="78612-182">decisão Olá sobre os quais um funcionará melhor para você depende da escolha de saudação do hello programação modelo, estrutura de comunicação hello e Olá que os serviços são escritos na linguagem de programação.</span><span class="sxs-lookup"><span data-stu-id="78612-182">hello decision about which one will work best for you depends on hello choice of hello programming model, hello communication framework, and hello programming language that your services are written in.</span></span>

* <span data-ttu-id="78612-183">**Nenhum protocolo específico:** se você não tem uma opção específica do framework de comunicação, mas você deseja tooget algo em funcionamento rapidamente, Olá a opção ideal para você é [comunicação remota do serviço](service-fabric-reliable-services-communication-remoting.md), que permite chamadas de procedimento remoto fortemente tipado para serviços confiáveis e atores confiável.</span><span class="sxs-lookup"><span data-stu-id="78612-183">**No specific protocol:**  If you don't have a particular choice of communication framework, but you want tooget something up and running quickly, then hello ideal option for you is [service remoting](service-fabric-reliable-services-communication-remoting.md), which allows strongly-typed remote procedure calls for Reliable Services and Reliable Actors.</span></span> <span data-ttu-id="78612-184">Isso é mais fácil de hello e tooget de maneira mais rápida é iniciado com a comunicação de serviço.</span><span class="sxs-lookup"><span data-stu-id="78612-184">This is hello easiest and fastest way tooget started with service communication.</span></span> <span data-ttu-id="78612-185">A comunicação remota do serviço lida com a resolução de endereços de serviço, conexão, repetição e tratamento de erro.</span><span class="sxs-lookup"><span data-stu-id="78612-185">Service remoting handles resolution of service addresses, connection, retry, and error handling.</span></span> <span data-ttu-id="78612-186">Isso está disponível para aplicativos Java e C#.</span><span class="sxs-lookup"><span data-stu-id="78612-186">This is available for both C# and Java applications.</span></span>
* <span data-ttu-id="78612-187">**HTTP**: para comunicação independente de idioma, o HTTP fornece uma opção padrão do setor com ferramentas e servidores HTTP disponíveis em várias linguagens diferentes, tudo isso com suporte no Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="78612-187">**HTTP**: For language-agnostic communication, HTTP provides an industry-standard choice with tools and HTTP servers available in many different languages, all supported by Service Fabric.</span></span> <span data-ttu-id="78612-188">Os serviços podem usar qualquer pilha HTTP disponível, incluindo [API Web ASP.NET](service-fabric-reliable-services-communication-webapi.md) para aplicativos C#.</span><span class="sxs-lookup"><span data-stu-id="78612-188">Services can use any HTTP stack available, including [ASP.NET Web API](service-fabric-reliable-services-communication-webapi.md) for C# applications.</span></span> <span data-ttu-id="78612-189">Clientes gravados em c# podem aproveitar Olá `ICommunicationClient` e `ServicePartitionClient` classes, enquanto para Java, use Olá `CommunicationClient` e `FabricServicePartitionClient` classes, [para resolução de serviço, as conexões HTTP e loops de repetição](service-fabric-reliable-services-communication.md).</span><span class="sxs-lookup"><span data-stu-id="78612-189">Clients written in C# can leverage hello `ICommunicationClient` and `ServicePartitionClient` classes, whereas for Java, use hello `CommunicationClient` and `FabricServicePartitionClient` classes, [for service resolution, HTTP connections, and retry loops](service-fabric-reliable-services-communication.md).</span></span>
* <span data-ttu-id="78612-190">**WCF**: se você tiver um código que usa o WCF como sua estrutura de comunicação, você pode usar o hello `WcfCommunicationListener` para o lado do servidor de saudação e `WcfCommunicationClient` e `ServicePartitionClient` classes para cliente hello.</span><span class="sxs-lookup"><span data-stu-id="78612-190">**WCF**: If you have existing code that uses WCF as your communication framework, then you can use hello `WcfCommunicationListener` for hello server side and `WcfCommunicationClient` and `ServicePartitionClient` classes for hello client.</span></span> <span data-ttu-id="78612-191">No entanto, isso só está disponível para aplicativos C# em clusters baseados no Windows.</span><span class="sxs-lookup"><span data-stu-id="78612-191">This however is only available for C# applications on Windows based clusters.</span></span> <span data-ttu-id="78612-192">Para obter mais detalhes, consulte este artigo sobre [baseados em WCF e a implementação da pilha de comunicação Olá](service-fabric-reliable-services-communication-wcf.md).</span><span class="sxs-lookup"><span data-stu-id="78612-192">For more details, see this article about [WCF-based implementation of hello communication stack](service-fabric-reliable-services-communication-wcf.md).</span></span>

## <a name="using-custom-protocols-and-other-communication-frameworks"></a><span data-ttu-id="78612-193">Usando protocolos personalizados e outras estruturas de comunicação</span><span class="sxs-lookup"><span data-stu-id="78612-193">Using custom protocols and other communication frameworks</span></span>
<span data-ttu-id="78612-194">Os serviços poderão usar qualquer protocolo ou estrutura para comunicação, independentemente de esse ser um protocolo binário personalizado via soquetes TCP ou eventos de streaming por meio de [Hubs de Eventos do Azure](https://azure.microsoft.com/services/event-hubs/) ou [Hub IoT do Azure](https://azure.microsoft.com/services/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="78612-194">Services can use any protocol or framework for communication, whether its a custom binary protocol over TCP sockets, or streaming events through [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) or [Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/).</span></span> <span data-ttu-id="78612-195">Serviço de malha fornece APIs que você pode conectar sua pilha de comunicação, enquanto todos os Olá trabalhar toodiscover e conecte-se a comunicação é abstraída do você.</span><span class="sxs-lookup"><span data-stu-id="78612-195">Service Fabric provides communication APIs that you can plug your communication stack into, while all hello work toodiscover and connect is abstracted from you.</span></span> <span data-ttu-id="78612-196">Consulte este artigo sobre Olá [modelo de comunicação de serviço confiável](service-fabric-reliable-services-communication.md) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="78612-196">See this article about hello [Reliable Service communication model](service-fabric-reliable-services-communication.md) for more details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="78612-197">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="78612-197">Next steps</span></span>
<span data-ttu-id="78612-198">Saber mais sobre conceitos de saudação e APIs disponíveis no hello [modelo de comunicação de serviços confiáveis](service-fabric-reliable-services-communication.md), em seguida, se familiarizar rapidamente com [comunicação remota do serviço](service-fabric-reliable-services-communication-remoting.md) ou vá toolearn detalhada como toowrite um ouvinte de comunicação usando [API da Web com OWIN auto-host](service-fabric-reliable-services-communication-webapi.md).</span><span class="sxs-lookup"><span data-stu-id="78612-198">Learn more about hello concepts and APIs available in hello [Reliable Services communication model](service-fabric-reliable-services-communication.md), then get started quickly with [service remoting](service-fabric-reliable-services-communication-remoting.md) or go in-depth toolearn how toowrite a communication listener using [Web API with OWIN self-host](service-fabric-reliable-services-communication-webapi.md).</span></span>

[1]: ./media/service-fabric-connect-and-communicate-with-services/serviceendpoints.png
[2]: ./media/service-fabric-connect-and-communicate-with-services/namingservice.png
[3]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancertopology.png
[4]: ./media/service-fabric-connect-and-communicate-with-services/nodeport.png
[5]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerport.png
[7]: ./media/service-fabric-connect-and-communicate-with-services/distributedservices.png
[8]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerprobe.png
[9]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[10]: ./media/service-fabric-reverseproxy/internal-communication.png
