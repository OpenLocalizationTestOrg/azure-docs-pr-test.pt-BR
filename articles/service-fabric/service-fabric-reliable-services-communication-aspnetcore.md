---
title: "Comunicação de serviço com o Núcleo do ASP.NET | Microsoft Docs"
description: "Aprenda a usar o Núcleo do ASP.NET em Serviços Confiáveis com e sem estado."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 8aa4668d-cbb6-4225-bd2d-ab5925a868f2
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 05/02/2017
ms.author: vturecek
ms.openlocfilehash: 8ac4d409f7363e8b4ae98be659a627ac8db8d787
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="aspnet-core-in-service-fabric-reliable-services"></a><span data-ttu-id="90791-103">Núcleo do ASP.NET em Serviços Confiáveis do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="90791-103">ASP.NET Core in Service Fabric Reliable Services</span></span>

<span data-ttu-id="90791-104">O Núcleo do ASP.NET é uma nova estrutura de software livre e plataforma cruzada para criar aplicativos modernos baseados em nuvem conectados à Internet, como aplicativos Web, aplicativos de IoT e back-ends móveis.</span><span class="sxs-lookup"><span data-stu-id="90791-104">ASP.NET Core is a new open-source and cross-platform framework for building modern cloud-based Internet-connected applications, such as web apps, IoT apps, and mobile backends.</span></span> 

<span data-ttu-id="90791-105">Este artigo é um guia detalhado de hospedagem de serviços do ASP.NET Core nos Reliable Services do Service Fabric usando o conjunto **Microsoft.ServiceFabric.AspNetCore.*** de pacotes NuGet.</span><span class="sxs-lookup"><span data-stu-id="90791-105">This article is an in-depth guide to hosting ASP.NET Core services in Service Fabric Reliable Services using the **Microsoft.ServiceFabric.AspNetCore.*** set of NuGet packages.</span></span>

<span data-ttu-id="90791-106">Para obter um tutorial de introdução sobre o ASP.NET Core no Service Fabric, além de instruções sobre como configurar o ambiente de desenvolvimento, consulte [Criando um front-end da Web para seu aplicativo usando o ASP.NET Core](service-fabric-add-a-web-frontend.md).</span><span class="sxs-lookup"><span data-stu-id="90791-106">For an introductory tutorial on ASP.NET Core in Service Fabric and instructions on getting your development environment set up, see [Building a web front-end for your application using ASP.NET Core](service-fabric-add-a-web-frontend.md).</span></span>

<span data-ttu-id="90791-107">O restante deste artigo pressupõe que você já esteja familiarizado com o ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="90791-107">The rest of this article assumes you are already familiar with ASP.NET Core.</span></span> <span data-ttu-id="90791-108">Se não estiver, recomendamos ler os [Conceitos básicos do ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/index).</span><span class="sxs-lookup"><span data-stu-id="90791-108">If not, we recommend reading through the [ASP.NET Core fundamentals](https://docs.microsoft.com/aspnet/core/fundamentals/index).</span></span>

## <a name="aspnet-core-in-the-service-fabric-environment"></a><span data-ttu-id="90791-109">ASP.NET Core no ambiente do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="90791-109">ASP.NET Core in the Service Fabric environment</span></span>

<span data-ttu-id="90791-110">Embora os aplicativos do Núcleo do ASP.NET possam ser executados no Núcleo do .NET ou no .NET Framework completo, os serviços do Service Fabric atualmente só podem ser executados no .NET Framework completo.</span><span class="sxs-lookup"><span data-stu-id="90791-110">While ASP.NET Core apps can run on .NET Core or on the full .NET Framework, Service Fabric services currently can only run on the full .NET Framework.</span></span> <span data-ttu-id="90791-111">Isso significa que, ao criar um serviço do Service Fabric no ASP.NET Core, você ainda deve ter como destino o .NET Framework completo.</span><span class="sxs-lookup"><span data-stu-id="90791-111">This means when you build an ASP.NET  Core Service Fabric service, you must still target the full .NET Framework.</span></span>

<span data-ttu-id="90791-112">O Núcleo do ASP.NET pode ser usado de duas maneiras diferentes no Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="90791-112">ASP.NET Core can be used in two different ways in Service Fabric:</span></span>
 - <span data-ttu-id="90791-113">**Hospedado como um executável convidado**.</span><span class="sxs-lookup"><span data-stu-id="90791-113">**Hosted as a guest executable**.</span></span> <span data-ttu-id="90791-114">Isso é usado principalmente para executar aplicativos do Núcleo do ASP.NET existentes no Service Fabric sem alterações de código.</span><span class="sxs-lookup"><span data-stu-id="90791-114">This is primarily used to run existing ASP.NET Core applications on Service Fabric with no code changes.</span></span>
 - <span data-ttu-id="90791-115">**Executar em um Serviço Confiável**.</span><span class="sxs-lookup"><span data-stu-id="90791-115">**Run inside a Reliable Service**.</span></span> <span data-ttu-id="90791-116">Isso permite uma melhor integração com o tempo de execução do Service Fabric e permite os serviços de Núcleo do ASP.NET com monitoração de estado.</span><span class="sxs-lookup"><span data-stu-id="90791-116">This allows better integration with the Service Fabric runtime and allows stateful ASP.NET Core services.</span></span>

<span data-ttu-id="90791-117">O restante deste artigo explica como usar o Núcleo do ASP.NET em um Serviço Confiável usando os componentes de integração de Núcleo do ASP.NET que são fornecidos com o SDK do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="90791-117">The rest of this article explains how to use ASP.NET Core inside a Reliable Service using the ASP.NET Core integration components that ship with the Service Fabric SDK.</span></span> 

## <a name="service-fabric-service-hosting"></a><span data-ttu-id="90791-118">Hospedagem de serviços do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="90791-118">Service Fabric service hosting</span></span>

<span data-ttu-id="90791-119">No Service Fabric, uma ou mais instâncias e/ou réplicas do serviço são executadas em um *processo de host do serviço*, um arquivo executável que executa o código de serviço.</span><span class="sxs-lookup"><span data-stu-id="90791-119">In Service Fabric, one or more instances and/or replicas of your service run in a *service host process*, an executable file that runs your service code.</span></span> <span data-ttu-id="90791-120">Como autor do serviço, você é responsável pelo processo de host do serviço, e o Service Fabric o ativa e monitora para você.</span><span class="sxs-lookup"><span data-stu-id="90791-120">You, as a service author, own the service host process and Service Fabric activates and monitors it for you.</span></span>

<span data-ttu-id="90791-121">O ASP.NET tradicional (até 5 MVC) está estreitamente relacionado ao IIS por meio de System.Web.dll.</span><span class="sxs-lookup"><span data-stu-id="90791-121">Traditional ASP.NET (up to MVC 5) is tightly coupled to IIS through System.Web.dll.</span></span> <span data-ttu-id="90791-122">O Núcleo do ASP.NET fornece uma separação entre o servidor Web e o aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="90791-122">ASP.NET Core provides a separation between the web server and your web application.</span></span> <span data-ttu-id="90791-123">Isso permite a portabilidade de aplicativos Web entre diferentes servidores Web e  permite também que os servidores Web sejam *auto-hospedados*, o que significa que você pode iniciar um servidor Web em seu próprio processo, em vez de um processo que pertence ao software do servidor Web dedicado, como o IIS.</span><span class="sxs-lookup"><span data-stu-id="90791-123">This allows web applications to be portable between different web servers and also allows web servers to be *self-hosted*, which means you can start a web server in your own process, as opposed to a process that is owned by dedicated web server software such as IIS.</span></span> 

<span data-ttu-id="90791-124">Para combinar um serviço do Service Fabric ao ASP.NET, como um executável de convidado ou em um Serviço Confiável, você deve poder iniciar o ASP.NET no processo de host de serviço.</span><span class="sxs-lookup"><span data-stu-id="90791-124">In order to combine a Service Fabric service and ASP.NET, either as a guest executable or in a Reliable Service, you must be able to start ASP.NET inside your service host process.</span></span> <span data-ttu-id="90791-125">A hospedagem interna do Núcleo do ASP.NET permite que você faça isso.</span><span class="sxs-lookup"><span data-stu-id="90791-125">ASP.NET Core self-hosting allows you to do this.</span></span>

## <a name="hosting-aspnet-core-in-a-reliable-service"></a><span data-ttu-id="90791-126">Hospedando o Núcleo do ASP.NET em um Serviço Confiável</span><span class="sxs-lookup"><span data-stu-id="90791-126">Hosting ASP.NET Core in a Reliable Service</span></span>
<span data-ttu-id="90791-127">Normalmente, aplicativos do Núcleo do ASP.NET auto-hospedados criam um WebHost no ponto de entrada do aplicativo, como o método `static void Main()` em `Program.cs`.</span><span class="sxs-lookup"><span data-stu-id="90791-127">Typically, self-hosted ASP.NET Core applications create a WebHost in an application's entry point, such as the `static void Main()` method in `Program.cs`.</span></span> <span data-ttu-id="90791-128">Nesse caso, o ciclo de vida do WebHost está associado ao ciclo de vida do processo.</span><span class="sxs-lookup"><span data-stu-id="90791-128">In this case, the lifecycle of the WebHost is bound to the lifecycle of the process.</span></span>

![Hospedando o Núcleo do ASP.NET em um processo][0]

<span data-ttu-id="90791-130">No entanto, o ponto de entrada do aplicativo não é o lugar certo para criar um WebHost em um serviço confiável, pois o ponto de entrada do aplicativo só é usado para registrar um tipo de serviço com o tempo de execução do Service Fabric, para que possa criar instâncias desse tipo de serviço.</span><span class="sxs-lookup"><span data-stu-id="90791-130">However, the application entry point is not the right place to create a WebHost in a Reliable Service, because the application entry point is only used to register a service type with the Service Fabric runtime, so that it may create instances of that service type.</span></span> <span data-ttu-id="90791-131">O WebHost deve ser criado em um Serviço Confiável em si.</span><span class="sxs-lookup"><span data-stu-id="90791-131">The WebHost should be created in a Reliable Service itself.</span></span> <span data-ttu-id="90791-132">No processo de host do serviço, instâncias de serviço e/ou réplicas podem passar por vários ciclos de vida.</span><span class="sxs-lookup"><span data-stu-id="90791-132">Within the service host process, service instances and/or replicas can go through multiple lifecycles.</span></span> 

<span data-ttu-id="90791-133">Uma instância de um serviço confiável é representada por sua classe de serviço derivando de `StatelessService` ou `StatefulService`.</span><span class="sxs-lookup"><span data-stu-id="90791-133">A Reliable Service instance is represented by your service class deriving from `StatelessService` or `StatefulService`.</span></span> <span data-ttu-id="90791-134">A pilha de comunicação para um serviço está contida em uma implementação `ICommunicationListener` em sua classe de serviço.</span><span class="sxs-lookup"><span data-stu-id="90791-134">The communication stack for a service is contained in an `ICommunicationListener` implementation in your service class.</span></span> <span data-ttu-id="90791-135">Os pacotes `Microsoft.ServiceFabric.Services.AspNetCore.*` do NuGet contêm implementações de `ICommunicationListener` que iniciam e gerenciam o WebHost de Núcleo do ASP.NET para Kestrel ou WebListener em um Serviço Confiável.</span><span class="sxs-lookup"><span data-stu-id="90791-135">The `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet packages contain implementations of `ICommunicationListener` that start and manage the ASP.NET Core WebHost for either Kestrel or WebListener in a Reliable Service.</span></span>

![Hospedando o Núcleo do ASP.NET em um Serviço Confiável][1]

## <a name="aspnet-core-icommunicationlisteners"></a><span data-ttu-id="90791-137">Núcleo do ASP.NET ICommunicationListeners</span><span class="sxs-lookup"><span data-stu-id="90791-137">ASP.NET Core ICommunicationListeners</span></span>
<span data-ttu-id="90791-138">As implementações `ICommunicationListener` para Kestrel e WebListener nos pacotes `Microsoft.ServiceFabric.Services.AspNetCore.*` do NuGet têm padrões de uso semelhantes, mas executam ações específicas ligeiramente diferentes para cada servidor Web.</span><span class="sxs-lookup"><span data-stu-id="90791-138">The `ICommunicationListener` implementations for Kestrel and WebListener in the  `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet packages have similar use patterns but perform slightly different actions specific to each web server.</span></span> 

<span data-ttu-id="90791-139">Ambos os ouvintes de comunicação fornecem um construtor que usa os seguintes argumentos:</span><span class="sxs-lookup"><span data-stu-id="90791-139">Both communication listeners provide a constructor that takes the following arguments:</span></span>
 - <span data-ttu-id="90791-140">**`ServiceContext serviceContext`**: o objeto `ServiceContext` que contém informações sobre o serviço em execução.</span><span class="sxs-lookup"><span data-stu-id="90791-140">**`ServiceContext serviceContext`**: The `ServiceContext` object that contains information about the running service.</span></span>
 - <span data-ttu-id="90791-141">**`string endpointName`**: o nome de uma configuração `Endpoint` em ServiceManifest.XML.</span><span class="sxs-lookup"><span data-stu-id="90791-141">**`string endpointName`**: the name of an `Endpoint` configuration in ServiceManifest.xml.</span></span> <span data-ttu-id="90791-142">É principalmente onde os dois ouvintes de comunicação diferem: o WebListener **requer** uma configuração `Endpoint`, enquanto o Kestrel não a requer.</span><span class="sxs-lookup"><span data-stu-id="90791-142">This is primarily where the two communication listeners differ: WebListener **requires** an `Endpoint` configuration, while Kestrel does not.</span></span>
 - <span data-ttu-id="90791-143">**`Func<string, AspNetCoreCommunicationListener, IWebHost> build`**: um lambda que você implementa e no qual cria e retorna um `IWebHost`.</span><span class="sxs-lookup"><span data-stu-id="90791-143">**`Func<string, AspNetCoreCommunicationListener, IWebHost> build`**: a lambda that you implement in which you create and return an `IWebHost`.</span></span> <span data-ttu-id="90791-144">Isso permite que você configure `IWebHost` da maneira como faria normalmente em um aplicativo do Núcleo do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="90791-144">This allows you to configure `IWebHost` the way you normally would in an ASP.NET Core application.</span></span> <span data-ttu-id="90791-145">O lambda fornece uma URL que é gerada para você, dependendo das opções de integração do Service Fabric que você usar e da configuração `Endpoint` que você fornecer.</span><span class="sxs-lookup"><span data-stu-id="90791-145">The lambda provides a URL which is generated for you depending on the Service Fabric integration options you use and the `Endpoint` configuration you provide.</span></span> <span data-ttu-id="90791-146">Essa URL pode então ser modificada ou usada como está para iniciar o servidor Web.</span><span class="sxs-lookup"><span data-stu-id="90791-146">That URL can then be modified or used as-is to start the web server.</span></span>

## <a name="service-fabric-integration-middleware"></a><span data-ttu-id="90791-147">Middleware de integração do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="90791-147">Service Fabric integration middleware</span></span>
<span data-ttu-id="90791-148">O pacote do NuGet `Microsoft.ServiceFabric.Services.AspNetCore` inclui o método de extensão `UseServiceFabricIntegration` no `IWebHostBuilder` que adiciona o middleware com reconhecimento do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="90791-148">The `Microsoft.ServiceFabric.Services.AspNetCore` NuGet package includes the `UseServiceFabricIntegration` extension method on `IWebHostBuilder` that adds Service Fabric-aware middleware.</span></span> <span data-ttu-id="90791-149">Esse middleware configura o `ICommunicationListener` do Kestrel ou o WebListener para registrar uma URL de serviço exclusivo no Serviço de Nomenclatura do Service Fabric e valida solicitações do cliente para assegurar que os clientes se conectem ao serviço certo.</span><span class="sxs-lookup"><span data-stu-id="90791-149">This middleware configures the Kestrel or WebListener `ICommunicationListener` to register a unique service URL with the Service Fabric Naming Service and then validates client requests to ensure clients are connecting to the right service.</span></span> <span data-ttu-id="90791-150">Isso é necessário em um ambiente de host compartilhado como o Service Fabric, em que vários aplicativos Web podem ser executados na mesma máquina física ou virtual, mas não usam nomes de host exclusivos, para impedir que os clientes se conectem ao serviço errado por engano.</span><span class="sxs-lookup"><span data-stu-id="90791-150">This is necessary in a shared-host environment such as Service Fabric, where multiple web applications can run on the same physical or virtual machine but do not use unique host names, to prevent clients from mistakenly connecting to the wrong service.</span></span> <span data-ttu-id="90791-151">Esse cenário é descrito em mais detalhes na próxima seção.</span><span class="sxs-lookup"><span data-stu-id="90791-151">This scenario is described in more detail in the next section.</span></span>

### <a name="a-case-of-mistaken-identity"></a><span data-ttu-id="90791-152">Um caso de identidade incorreta</span><span class="sxs-lookup"><span data-stu-id="90791-152">A case of mistaken identity</span></span>
<span data-ttu-id="90791-153">Independentemente do protocolo, as réplicas de serviço escutam em uma combinação de IP:porta exclusiva.</span><span class="sxs-lookup"><span data-stu-id="90791-153">Service replicas, regardless of protocol, listen on a unique IP:port combination.</span></span> <span data-ttu-id="90791-154">Depois que uma réplica de serviço começa a escutar em um ponto de extremidade IP:porta, ela relata esse endereço do ponto de extremidade para o Serviço de Nomenclatura do Service Fabric, onde pode ser descoberto por clientes ou por outros serviços.</span><span class="sxs-lookup"><span data-stu-id="90791-154">Once a service replica has started listening on an IP:port endpoint, it reports that endpoint address to the Service Fabric Naming Service where it can be discovered by clients or other services.</span></span> <span data-ttu-id="90791-155">Se os serviços usarem portas de aplicativos atribuídas dinamicamente, uma réplica de serviço poderá usar coincidentemente o mesmo ponto de extremidade IP:porta que outro serviço que estava anteriormente na mesma máquina física ou virtual.</span><span class="sxs-lookup"><span data-stu-id="90791-155">If services use dynamically-assigned application ports, a service replica may coincidentally use the same IP:port endpoint of another service that was previously on the same physical or virtual machine.</span></span> <span data-ttu-id="90791-156">Isso pode fazer com que um cliente se conecte incorretamente ao serviço errado.</span><span class="sxs-lookup"><span data-stu-id="90791-156">This can cause a client to mistakely connect to the wrong service.</span></span> <span data-ttu-id="90791-157">Isso poderá acontecer se a seguinte sequência de eventos ocorrer:</span><span class="sxs-lookup"><span data-stu-id="90791-157">This can happen if the following sequence of events occur:</span></span>

 1. <span data-ttu-id="90791-158">O serviço A escuta em 10.0.0.1:30000 via HTTP.</span><span class="sxs-lookup"><span data-stu-id="90791-158">Service A listens on 10.0.0.1:30000 over HTTP.</span></span> 
 2. <span data-ttu-id="90791-159">O cliente resolve o serviço A e obtém o endereço 10.0.0.1:30000</span><span class="sxs-lookup"><span data-stu-id="90791-159">Client resolves Service A and gets address 10.0.0.1:30000</span></span>
 3. <span data-ttu-id="90791-160">O Serviço A move-se para um nó diferente.</span><span class="sxs-lookup"><span data-stu-id="90791-160">Service A moves to a different node.</span></span>
 4. <span data-ttu-id="90791-161">O serviço B é colocado em 10.0.0.1 e usa coincidentemente a mesma porta 30000.</span><span class="sxs-lookup"><span data-stu-id="90791-161">Service B is placed on 10.0.0.1 and coincidentally uses the same port 30000.</span></span>
 5. <span data-ttu-id="90791-162">O cliente tenta se conectar ao serviço A com o endereço de cache 10.0.0.1:30000.</span><span class="sxs-lookup"><span data-stu-id="90791-162">Client attempts to connect to service A with cached address 10.0.0.1:30000.</span></span>
 6. <span data-ttu-id="90791-163">Agora o cliente é conectado com êxito ao serviço B sem perceber que está conectado ao serviço errado.</span><span class="sxs-lookup"><span data-stu-id="90791-163">Client is now successfully connected to service B not realizing it is connected to the wrong service.</span></span>

<span data-ttu-id="90791-164">Isso pode causar bugs em momentos aleatórios, que podem ser difíceis de diagnosticar.</span><span class="sxs-lookup"><span data-stu-id="90791-164">This can cause bugs at random times that can be difficult to diagnose.</span></span> 

### <a name="using-unique-service-urls"></a><span data-ttu-id="90791-165">Usando URLs de serviço exclusivas</span><span class="sxs-lookup"><span data-stu-id="90791-165">Using unique service URLs</span></span>
<span data-ttu-id="90791-166">Para evitar isso, os serviços podem postar um ponto de extremidade para o Serviço de Nomenclatura com um identificador exclusivo e validar esse identificador exclusivo durante as solicitações do cliente.</span><span class="sxs-lookup"><span data-stu-id="90791-166">To prevent this, services can post an endpoint to the Naming Service with a unique identifier, and then validate that unique identifier during client requests.</span></span> <span data-ttu-id="90791-167">Essa é uma ação cooperativa entre serviços em um ambiente confiável de locatário não hostil.</span><span class="sxs-lookup"><span data-stu-id="90791-167">This is a cooperative action between services in a non-hostile-tenant trusted environment.</span></span> <span data-ttu-id="90791-168">Isso não fornece autenticação segura em um ambiente de locatário hostil.</span><span class="sxs-lookup"><span data-stu-id="90791-168">This does not provide secure service authentication in a hostile-tenant environment.</span></span>

<span data-ttu-id="90791-169">Em um ambiente confiável, o middleware adicionado pelo método `UseServiceFabricIntegration` anexa automaticamente um identificador exclusivo ao endereço que é postado para o Serviço de Nomes e valida esse identificador em cada solicitação.</span><span class="sxs-lookup"><span data-stu-id="90791-169">In a trusted environment, the middleware that's added by the `UseServiceFabricIntegration` method automatically appends a unique identifier to the address that is posted to the Naming Service and validates that identifier on each request.</span></span> <span data-ttu-id="90791-170">Se o identificador não for correspondente, o middleware retornará imediatamente uma resposta HTTP 410 Não existe mais.</span><span class="sxs-lookup"><span data-stu-id="90791-170">If the identifier does not match, the middleware immediately returns an HTTP 410 Gone response.</span></span>

<span data-ttu-id="90791-171">Os serviços que usam uma porta atribuída dinamicamente devem fazer uso desse middleware.</span><span class="sxs-lookup"><span data-stu-id="90791-171">Services that use a dynamically-assigned port should make use of this middleware.</span></span>

<span data-ttu-id="90791-172">Os serviços que usam uma porta exclusiva fixa não têm esse problema em um ambiente cooperativo.</span><span class="sxs-lookup"><span data-stu-id="90791-172">Services that use a fixed unique port do not have this problem in a cooperative environment.</span></span> <span data-ttu-id="90791-173">Uma porta exclusiva fixa é normalmente usada para serviços voltados para o exterior que precisam de uma porta conhecida para que os aplicativos cliente se conectem.</span><span class="sxs-lookup"><span data-stu-id="90791-173">A fixed unique port is typically used for externally-facing services that need a well-known port for client applications to connect to.</span></span> <span data-ttu-id="90791-174">Por exemplo, a maioria dos aplicativos Web voltados para a Internet usará a porta 80 ou 443 para conexões do navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="90791-174">For example, most Internet-facing web applications will use port 80 or 443 for web browser connections.</span></span> <span data-ttu-id="90791-175">Nesse caso, o identificador exclusivo não deve ser habilitado.</span><span class="sxs-lookup"><span data-stu-id="90791-175">In this case, the unique identifier should not be enabled.</span></span>

<span data-ttu-id="90791-176">O diagrama a seguir mostra o fluxo de solicitação com o middleware habilitado:</span><span class="sxs-lookup"><span data-stu-id="90791-176">The following diagram shows the request flow with the middleware enabled:</span></span>

![Integração de núcleo do ASP.NET do Service Fabric][2]

<span data-ttu-id="90791-178">As implementações `ICommunicationListener` do Kestrel e do WebListener usam esse mecanismo exatamente da mesma maneira.</span><span class="sxs-lookup"><span data-stu-id="90791-178">Both Kestrel and WebListener `ICommunicationListener` implementations use this mechanism in exactly the same way.</span></span> <span data-ttu-id="90791-179">Embora o WebListener possa diferenciar internamente as solicitações com base em caminhos de URL exclusivos usando o recurso subjacente de compartilhamento de porta *HTTP. sys*, essa funcionalidade *não* é usada pela implementação `ICommunicationListener` do WebListener, pois isso resultará em códigos de status de erro HTTP 503 e HTTP 404 no cenário descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="90791-179">Although WebListener can internally differentiate requests based on unique URL paths using the underlying *http.sys* port sharing feature, that functionality is *not* used by the WebListener `ICommunicationListener` implementation because that will result in HTTP 503 and HTTP 404 error status codes in the scenario described earlier.</span></span> <span data-ttu-id="90791-180">Por sua vez, isso torna muito difícil para os clientes determinar a intenção do erro, pois HTTP 503 e HTTP 404 já são usados normalmente para indicar outros erros.</span><span class="sxs-lookup"><span data-stu-id="90791-180">That in turn makes it very difficult for clients to determine the intent of the error, as HTTP 503 and HTTP 404 are already commonly used to indicate other errors.</span></span> <span data-ttu-id="90791-181">Dessa forma, as implementações `ICommunicationListener` do Kestrel e do WebListener são padronizadas com o middleware fornecido pelo método de extensão `UseServiceFabricIntegration` para que os clientes só precisem executar uma ação de nova resolução de ponto de extremidade de serviço em respostas HTTP 410.</span><span class="sxs-lookup"><span data-stu-id="90791-181">Thus, both Kestrel and WebListener `ICommunicationListener` implementations standardize on the middleware provided by the `UseServiceFabricIntegration` extension method so that clients only need to perform a service endpoint re-resolve action on HTTP 410 responses.</span></span>

## <a name="weblistener-in-reliable-services"></a><span data-ttu-id="90791-182">WebListener em Serviços Confiáveis</span><span class="sxs-lookup"><span data-stu-id="90791-182">WebListener in Reliable Services</span></span>
<span data-ttu-id="90791-183">O WebListener pode ser usado em um Serviço Confiável importando o pacote **Microsoft.ServiceFabric.AspNetCore.WebListener** do NuGet.</span><span class="sxs-lookup"><span data-stu-id="90791-183">WebListener can be used in a Reliable Service by importing the **Microsoft.ServiceFabric.AspNetCore.WebListener** NuGet package.</span></span> <span data-ttu-id="90791-184">Esse pacote contém o `WebListenerCommunicationListener`, uma implementação do `ICommunicationListener`, que permite que você crie um WebHost de Núcleo do ASP.NET em um serviço confiável usando o WebListener como o servidor Web.</span><span class="sxs-lookup"><span data-stu-id="90791-184">This package contains `WebListenerCommunicationListener`, an implementation of `ICommunicationListener`, that allows you to create an ASP.NET Core WebHost inside a Reliable Service using WebListener as the web server.</span></span>

<span data-ttu-id="90791-185">O WebListener se baseia na [API do Windows HTTP Server](https://msdn.microsoft.com/library/windows/desktop/aa364510(v=vs.85).aspx).</span><span class="sxs-lookup"><span data-stu-id="90791-185">WebListener is built on the [Windows HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510(v=vs.85).aspx).</span></span> <span data-ttu-id="90791-186">Isso usa o driver de kernel *http.sys* usado pelo IIS para processar solicitações HTTP e roteá-las para processos que executam os aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="90791-186">This uses the *http.sys* kernel driver used by IIS to process HTTP requests and route them to processes running web applications.</span></span> <span data-ttu-id="90791-187">Isso permite que vários processos na mesma máquina física ou virtual hospedem aplicativos Web na mesma porta, sem ambiguidade graças a um caminho de URL ou nome do host exclusivo.</span><span class="sxs-lookup"><span data-stu-id="90791-187">This allows multiple processes on the same physical or virtual machine to host web applications on the same port, disambiguated by either a unique URL path or hostname.</span></span> <span data-ttu-id="90791-188">Esses recursos são úteis no Service Fabric para hospedar vários sites no mesmo cluster.</span><span class="sxs-lookup"><span data-stu-id="90791-188">These features are useful in Service Fabric for hosting multiple websites in the same cluster.</span></span>

<span data-ttu-id="90791-189">O diagrama a seguir ilustra como o WebListener usa o driver de kernel *http.sys* no Windows para o compartilhamento de porta:</span><span class="sxs-lookup"><span data-stu-id="90791-189">The following diagram illustrates how WebListener uses the *http.sys* kernel driver on Windows for port sharing:</span></span>

![http.sys][3]

### <a name="weblistener-in-a-stateless-service"></a><span data-ttu-id="90791-191">WebListener em um serviço sem estado</span><span class="sxs-lookup"><span data-stu-id="90791-191">WebListener in a stateless service</span></span>
<span data-ttu-id="90791-192">Para usar `WebListener` em um serviço sem estado, substitua o método `CreateServiceInstanceListeners` e retorne uma instância `WebListenerCommunicationListener`:</span><span class="sxs-lookup"><span data-stu-id="90791-192">To use `WebListener` in a stateless service, override the `CreateServiceInstanceListeners` method and return a `WebListenerCommunicationListener` instance:</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    return new ServiceInstanceListener[]
    {
        new ServiceInstanceListener(serviceContext =>
            new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
                new WebHostBuilder()
                    .UseWebListener()
                    .ConfigureServices(
                        services => services
                            .AddSingleton<StatelessServiceContext>(serviceContext))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build()))
    };
}
```

### <a name="weblistener-in-a-stateful-service"></a><span data-ttu-id="90791-193">WebListener em um serviço com estado</span><span class="sxs-lookup"><span data-stu-id="90791-193">WebListener in a stateful service</span></span>

<span data-ttu-id="90791-194">O `WebListenerCommunicationListener` no momento não é projetado para uso em serviços com estado, devido a complicações com o recurso de compartilhamento de porta subjacente, *http.sys*.</span><span class="sxs-lookup"><span data-stu-id="90791-194">`WebListenerCommunicationListener` is currently not designed for use in stateful services due to complications with the underlying *http.sys* port sharing feature.</span></span> <span data-ttu-id="90791-195">Para obter mais informações, confira a seção a seguir sobre a alocação de porta dinâmica com o WebListener.</span><span class="sxs-lookup"><span data-stu-id="90791-195">For more information, see the following section on dynamic port allocation with WebListener.</span></span> <span data-ttu-id="90791-196">Para serviços com estado, o Kestrel é o servidor Web recomendado.</span><span class="sxs-lookup"><span data-stu-id="90791-196">For stateful services, Kestrel is the recommended web server.</span></span>

### <a name="endpoint-configuration"></a><span data-ttu-id="90791-197">Configuração de ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="90791-197">Endpoint configuration</span></span>

<span data-ttu-id="90791-198">Uma configuração `Endpoint` é necessária para servidores Web que usam a API do Windows HTTP Server, incluindo o WebListener.</span><span class="sxs-lookup"><span data-stu-id="90791-198">An `Endpoint` configuration is required for web servers that use the Windows HTTP Server API, including WebListener.</span></span> <span data-ttu-id="90791-199">Servidores Web que usam a API do Windows HTTP Server primeiro devem reservar a URL com *http.sys* (isso normalmente é feito com a ferramenta [netsh](https://msdn.microsoft.com/library/windows/desktop/cc307236(v=vs.85).aspx)).</span><span class="sxs-lookup"><span data-stu-id="90791-199">Web servers that use the Windows HTTP Server API must first reserve their URL with *http.sys* (this is normally accomplished with the [netsh](https://msdn.microsoft.com/library/windows/desktop/cc307236(v=vs.85).aspx) tool).</span></span> <span data-ttu-id="90791-200">Esta ação exige privilégios elevados que seus serviços não têm por padrão.</span><span class="sxs-lookup"><span data-stu-id="90791-200">This action requires elevated privileges that your services by default do not have.</span></span> <span data-ttu-id="90791-201">As opções "http" ou "https" para a propriedade `Protocol` da configuração `Endpoint` em *ServiceManifest.xml* são usadas especificamente para instruir o tempo de execução do Service Fabric a registrar uma URL com *http.sys* em seu nome usando o prefixo de URL [*curinga forte*](https://msdn.microsoft.com/library/windows/desktop/aa364698(v=vs.85).aspx).</span><span class="sxs-lookup"><span data-stu-id="90791-201">The "http" or "https" options for the `Protocol` property of the `Endpoint` configuration in *ServiceManifest.xml* are used specifically to instruct the Service Fabric runtime to register a URL with *http.sys* on your behalf using the [*strong wildcard*](https://msdn.microsoft.com/library/windows/desktop/aa364698(v=vs.85).aspx) URL prefix.</span></span>

<span data-ttu-id="90791-202">Por exemplo, para reservar `http://+:80` para um serviço, a seguinte configuração deve ser usada em ServiceManifest.XML:</span><span class="sxs-lookup"><span data-stu-id="90791-202">For example, to reserve `http://+:80` for a service, the following configuration should be used in ServiceManifest.xml:</span></span>

```xml
<ServiceManifest ... >
    ...
    <Resources>
        <Endpoints>
            <Endpoint Name="ServiceEndpoint" Protocol="http" Port="80" />
        </Endpoints>
    </Resources>

</ServiceManifest>
```

<span data-ttu-id="90791-203">E o nome do ponto de extremidade deve ser passado para o construtor `WebListenerCommunicationListener`:</span><span class="sxs-lookup"><span data-stu-id="90791-203">And the endpoint name must be passed to the `WebListenerCommunicationListener` constructor:</span></span>

```csharp
 new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
 {
     return new WebHostBuilder()
         .UseWebListener()
         .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
         .UseUrls(url)
         .Build();
 })
```

#### <a name="use-weblistener-with-a-static-port"></a><span data-ttu-id="90791-204">Usar WebListener com uma porta estática</span><span class="sxs-lookup"><span data-stu-id="90791-204">Use WebListener with a static port</span></span>
<span data-ttu-id="90791-205">Para usar uma porta estática com o WebListener, forneça o número da porta na configuração `Endpoint`:</span><span class="sxs-lookup"><span data-stu-id="90791-205">To use a static port with WebListener, provide the port number in the `Endpoint` configuration:</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

#### <a name="use-weblistener-with-a-dynamic-port"></a><span data-ttu-id="90791-206">Usar WebListener com uma porta dinâmica</span><span class="sxs-lookup"><span data-stu-id="90791-206">Use WebListener with a dynamic port</span></span>
<span data-ttu-id="90791-207">Para usar uma porta atribuída dinamicamente com o WebListener, omita a propriedade `Port` na configuração `Endpoint`:</span><span class="sxs-lookup"><span data-stu-id="90791-207">To use a dynamically assigned port with WebListener, omit the `Port` property in the `Endpoint` configuration:</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" />
    </Endpoints>
  </Resources>
```

<span data-ttu-id="90791-208">Observe que uma porta dinâmica alocada por uma configuração `Endpoint` fornece apenas uma porta *por processo de host*.</span><span class="sxs-lookup"><span data-stu-id="90791-208">Note that a dynamic port allocated by an `Endpoint` configuration only provides one port *per host process*.</span></span> <span data-ttu-id="90791-209">O modelo de hospedagem do Service Fabric atual permite que várias instâncias de serviço e/ou réplicas sejam hospedadas no mesmo processo, o que significa que cada uma delas compartilhará a mesma porta quando for alocada por meio da configuração `Endpoint`.</span><span class="sxs-lookup"><span data-stu-id="90791-209">The current Service Fabric hosting model allows multiple service instances and/or replicas to be hosted in the same process, meaning that each one will share the same port when allocated through the `Endpoint` configuration.</span></span> <span data-ttu-id="90791-210">Várias instâncias do WebListener podem compartilhar uma porta usando o recurso subjacente de compartilhamento de porta *http.sys*, mas não há suporte para isso no `WebListenerCommunicationListener` devido às complicações introduzidas para solicitações do cliente.</span><span class="sxs-lookup"><span data-stu-id="90791-210">Multiple WebListener instances can share a port using the underlying *http.sys* port sharing feature, but that is not supported by `WebListenerCommunicationListener` due to the complications it introduces for client requests.</span></span> <span data-ttu-id="90791-211">Para o uso de portas dinâmicas, o Kestrel é o servidor Web recomendado.</span><span class="sxs-lookup"><span data-stu-id="90791-211">For dynamic port usage, Kestrel is the recommended web server.</span></span>

## <a name="kestrel-in-reliable-services"></a><span data-ttu-id="90791-212">Kestrel em Serviços Confiáveis</span><span class="sxs-lookup"><span data-stu-id="90791-212">Kestrel in Reliable Services</span></span>
<span data-ttu-id="90791-213">O Kestrel pode ser usado em um Serviço Confiável importando o pacote **Microsoft.ServiceFabric.AspNetCore.Kestrel** do NuGet.</span><span class="sxs-lookup"><span data-stu-id="90791-213">Kestrel can be used in a Reliable Service by importing the **Microsoft.ServiceFabric.AspNetCore.Kestrel** NuGet package.</span></span> <span data-ttu-id="90791-214">Esse pacote contém o `KestrelCommunicationListener`, uma implementação do `ICommunicationListener`, que permite que você crie um WebHost de Núcleo do ASP.NET em um serviço confiável usando o Kestrel como o servidor Web.</span><span class="sxs-lookup"><span data-stu-id="90791-214">This package contains `KestrelCommunicationListener`, an implementation of `ICommunicationListener`, that allows you to create an ASP.NET Core WebHost inside a Reliable Service using Kestrel as the web server.</span></span>

<span data-ttu-id="90791-215">O Kestrel é um servidor Web de plataforma cruzada para o Núcleo do ASP.NET com base em libuv, uma biblioteca de E/S assíncrona de plataforma cruzada.</span><span class="sxs-lookup"><span data-stu-id="90791-215">Kestrel is a cross-platform web server for ASP.NET Core based on libuv, a cross-platform asynchronous I/O library.</span></span> <span data-ttu-id="90791-216">Diferentemente do WebListener, o Kestrel usa um gerenciador de ponto de extremidade centralizado como *http.sys*.</span><span class="sxs-lookup"><span data-stu-id="90791-216">Unlike WebListener, Kestrel does not use a centralized endpoint manager such as *http.sys*.</span></span> <span data-ttu-id="90791-217">Diferentemente do WebListener, Kestrel não dá suporte ao compartilhamento de porta entre vários processos.</span><span class="sxs-lookup"><span data-stu-id="90791-217">And unlike WebListener, Kestrel does not support port sharing between multiple processes.</span></span> <span data-ttu-id="90791-218">Cada instância do Kestrel deve usar uma porta exclusiva.</span><span class="sxs-lookup"><span data-stu-id="90791-218">Each instance of Kestrel must use a unique port.</span></span>

![kestrel][4]

### <a name="kestrel-in-a-stateless-service"></a><span data-ttu-id="90791-220">Kestrel em um serviço sem estado</span><span class="sxs-lookup"><span data-stu-id="90791-220">Kestrel in a stateless service</span></span>
<span data-ttu-id="90791-221">Para usar `Kestrel` em um serviço sem estado, substitua o método `CreateServiceInstanceListeners` e retorne uma instância `KestrelCommunicationListener`:</span><span class="sxs-lookup"><span data-stu-id="90791-221">To use `Kestrel` in a stateless service, override the `CreateServiceInstanceListeners` method and return a `KestrelCommunicationListener` instance:</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    return new ServiceInstanceListener[]
    {
        new ServiceInstanceListener(serviceContext =>
            new KestrelCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
                new WebHostBuilder()
                    .UseKestrel()
                    .ConfigureServices(
                        services => services
                            .AddSingleton<StatelessServiceContext>(serviceContext))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.UseUniqueServiceUrl)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build();
            ))
    };
}
```

### <a name="kestrel-in-a-stateful-service"></a><span data-ttu-id="90791-222">Kestrel em um serviço com estado</span><span class="sxs-lookup"><span data-stu-id="90791-222">Kestrel in a stateful service</span></span>
<span data-ttu-id="90791-223">Para usar `Kestrel` em um serviço com estado, substitua o método `CreateServiceReplicaListeners` e retorne uma instância `KestrelCommunicationListener`:</span><span class="sxs-lookup"><span data-stu-id="90791-223">To use `Kestrel` in a stateful service, override the `CreateServiceReplicaListeners` method and return a `KestrelCommunicationListener` instance:</span></span>

```csharp
protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new ServiceReplicaListener[]
    {
        new ServiceReplicaListener(serviceContext =>
            new KestrelCommunicationListener(serviceContext, (url, listener) =>
                new WebHostBuilder()
                    .UseKestrel()
                    .ConfigureServices(
                         services => services
                             .AddSingleton<StatefulServiceContext>(serviceContext)
                             .AddSingleton<IReliableStateManager>(this.StateManager))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.UseUniqueServiceUrl)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build();
            ))
    };
}
```

<span data-ttu-id="90791-224">Neste exemplo, uma instância única de `IReliableStateManager` é fornecida ao contêiner de injeção de dependência do WebHost.</span><span class="sxs-lookup"><span data-stu-id="90791-224">In this example, a singleton instance of `IReliableStateManager` is provided to the WebHost dependency injection container.</span></span> <span data-ttu-id="90791-225">Isso não é estritamente necessário, mas permite que você use `IReliableStateManager` e Coleções Confiáveis em seus métodos de ação do controlador MVC.</span><span class="sxs-lookup"><span data-stu-id="90791-225">This is not strictly necessary, but it allows you to use `IReliableStateManager` and Reliable Collections in your MVC controller action methods.</span></span>

<span data-ttu-id="90791-226">Observe que um nome de configuração `Endpoint` **não** é fornecido para `KestrelCommunicationListener` em um serviço com estado.</span><span class="sxs-lookup"><span data-stu-id="90791-226">Note that an `Endpoint` configuration name is **not** provided to `KestrelCommunicationListener` in a stateful service.</span></span> <span data-ttu-id="90791-227">Isso será explicado mais detalhadamente na seção a seguir.</span><span class="sxs-lookup"><span data-stu-id="90791-227">This is explained in more detail in the following section.</span></span>

### <a name="endpoint-configuration"></a><span data-ttu-id="90791-228">Configuração de ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="90791-228">Endpoint configuration</span></span>
<span data-ttu-id="90791-229">Uma configuração `Endpoint` não é necessária para usar o Kestrel.</span><span class="sxs-lookup"><span data-stu-id="90791-229">An `Endpoint` configuration is not required to use Kestrel.</span></span> 

<span data-ttu-id="90791-230">O Kestrel é um servidor Web autônomo simples. Diferentemente do WebListener (ou HttpListener), ele não precisa de uma configuração `Endpoint` em *ServiceManifest.XML* porque não requer o registro de URL antes de iniciar.</span><span class="sxs-lookup"><span data-stu-id="90791-230">Kestrel is a simple stand-alone web server; unlike WebListener (or HttpListener), it does not need an `Endpoint` configuration in *ServiceManifest.xml* because it does not require URL registration prior to starting.</span></span> 

#### <a name="use-kestrel-with-a-static-port"></a><span data-ttu-id="90791-231">Usar Kestrel com uma porta estática</span><span class="sxs-lookup"><span data-stu-id="90791-231">Use Kestrel with a static port</span></span>
<span data-ttu-id="90791-232">Uma porta estática pode ser configurada na configuração do `Endpoint` de ServiceManifest.XML para uso com Kestrel.</span><span class="sxs-lookup"><span data-stu-id="90791-232">A static port can be configured in the `Endpoint` configuration of ServiceManifest.xml for use with Kestrel.</span></span> <span data-ttu-id="90791-233">Embora não seja estritamente necessário, há dois benefícios potenciais:</span><span class="sxs-lookup"><span data-stu-id="90791-233">Although this is not strictly necessary, it provides two potential benefits:</span></span>
 1. <span data-ttu-id="90791-234">Se a porta não estiver no intervalo de portas do aplicativo, ela será aberta por meio do firewall do sistema operacional pelo Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="90791-234">If the port does not fall in the application port range, it is opened through the OS firewall by Service Fabric.</span></span>
 2. <span data-ttu-id="90791-235">A URL fornecida através de `KestrelCommunicationListener` usará essa porta.</span><span class="sxs-lookup"><span data-stu-id="90791-235">The URL provided to you through `KestrelCommunicationListener` will use this port.</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

<span data-ttu-id="90791-236">Se um `Endpoint` for configurado, o nome deverá ser passado para o construtor `KestrelCommunicationListener`:</span><span class="sxs-lookup"><span data-stu-id="90791-236">If an `Endpoint` is configured, its name must be passed into the `KestrelCommunicationListener` constructor:</span></span> 

```csharp
new KestrelCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) => ...
```

<span data-ttu-id="90791-237">Se uma configuração `Endpoint` não for usada, omita o nome no construtor `KestrelCommunicationListener`.</span><span class="sxs-lookup"><span data-stu-id="90791-237">If an `Endpoint` configuration is not used, omit the name in the `KestrelCommunicationListener` constructor.</span></span> <span data-ttu-id="90791-238">Nesse caso, uma porta dinâmica será usada.</span><span class="sxs-lookup"><span data-stu-id="90791-238">In this case, a dynamic port will be used.</span></span> <span data-ttu-id="90791-239">Para obter mais informações, confira a próxima seção.</span><span class="sxs-lookup"><span data-stu-id="90791-239">See the next section for more information.</span></span>

#### <a name="use-kestrel-with-a-dynamic-port"></a><span data-ttu-id="90791-240">Usar Kestrel com uma porta dinâmica</span><span class="sxs-lookup"><span data-stu-id="90791-240">Use Kestrel with a dynamic port</span></span>
<span data-ttu-id="90791-241">O Kestrel não pode usar a atribuição automática de porta da configuração `Endpoint` em ServiceManifest.XML, pois a atribuição automática de porta de uma configuração `Endpoint` atribui uma porta exclusiva por *processo de host*, e um processo de host único pode conter várias instâncias do Kestrel.</span><span class="sxs-lookup"><span data-stu-id="90791-241">Kestrel cannot use the automatic port assignment from the `Endpoint` configuration in ServiceManifest.xml, because automatic port assignment from an `Endpoint` configuration assigns a unique port per *host process*, and a single host process can contain multiple Kestrel instances.</span></span> <span data-ttu-id="90791-242">Como o Kestrel não dá suporte ao compartilhamento de porta, isso não funciona, pois cada instância do Kestrel deve ser aberta em uma porta exclusiva.</span><span class="sxs-lookup"><span data-stu-id="90791-242">Since Kestrel does not support port sharing, this does not work as each Kestrel instance must be opened on a unique port.</span></span>

<span data-ttu-id="90791-243">Para usar a atribuição de porta dinâmica com o Kestrel, basta omitir a configuração `Endpoint` em ServiceManifest.xml e não passar um nome de ponto de extremidade para o construtor `KestrelCommunicationListener`:</span><span class="sxs-lookup"><span data-stu-id="90791-243">To use dynamic port assignment with Kestrel, simply omit the `Endpoint` configuration in ServiceManifest.xml entirely, and do not pass an endpoint name to the `KestrelCommunicationListener` constructor:</span></span>

```csharp
new KestrelCommunicationListener(serviceContext, (url, listener) => ...
```

<span data-ttu-id="90791-244">Nessa configuração, `KestrelCommunicationListener` selecionará automaticamente uma porta não utilizada do intervalo de portas de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="90791-244">In this configuration, `KestrelCommunicationListener` will automatically select an unused port from the application port range.</span></span>

## <a name="scenarios-and-configurations"></a><span data-ttu-id="90791-245">Cenários e configurações</span><span class="sxs-lookup"><span data-stu-id="90791-245">Scenarios and configurations</span></span>
<span data-ttu-id="90791-246">Esta seção descreve os cenários a seguir e fornece a combinação recomendada de servidor Web, configuração de porta, opções de integração do Service Fabric e diversos parâmetros para obter um serviço corretamente funcional:</span><span class="sxs-lookup"><span data-stu-id="90791-246">This section describes the following scenarios and provides the recommended combination of web server, port configuration, Service Fabric integration options, and miscellaneous settings to achieve a properly functioning service:</span></span>
 - <span data-ttu-id="90791-247">serviço sem estado do Núcleo do ASP.NET exposto externamente</span><span class="sxs-lookup"><span data-stu-id="90791-247">Externally exposed ASP.NET Core stateless service</span></span>
 - <span data-ttu-id="90791-248">Serviço do Núcleo do ASP.NET sem estado somente para uso interno</span><span class="sxs-lookup"><span data-stu-id="90791-248">Internal-only ASP.NET Core stateless service</span></span>
 - <span data-ttu-id="90791-249">serviço com estado do Núcleo do ASP.NET somente interno</span><span class="sxs-lookup"><span data-stu-id="90791-249">Internal-only ASP.NET Core stateful service</span></span>

<span data-ttu-id="90791-250">Um serviço **exposto externamente** é aquele que expõe um ponto de extremidade acessível de fora do cluster, geralmente por meio de um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="90791-250">An **externally exposed** service is one that exposes an endpoint reachable from outside the cluster, usually through a load balancer.</span></span>

<span data-ttu-id="90791-251">Um serviço **somente interno** é aquele cujo ponto de extremidade só é acessível por meio do cluster.</span><span class="sxs-lookup"><span data-stu-id="90791-251">An **internal-only** service is one whose endpoint is only reachable from within the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="90791-252">Os pontos de extremidade de serviço com estado geralmente não devem ser expostos à Internet.</span><span class="sxs-lookup"><span data-stu-id="90791-252">Stateful service endpoints generally should not be exposed to the Internet.</span></span> <span data-ttu-id="90791-253">Clusters que estiverem por trás de balanceadores de carga que não estiverem cientes da resolução de serviços do Service Fabric, como o Azure Load Balancer, não poderão expor serviços com estado, pois o balanceador de carga não poderá localizar e rotear o tráfego para a réplica de serviço com estado apropriada.</span><span class="sxs-lookup"><span data-stu-id="90791-253">Clusters that are behind load balancers that are unaware of Service Fabric service resolution, such as the Azure Load Balancer, will be unable to expose stateful services because the load balancer will not be able to locate and route traffic to the appropriate stateful service replica.</span></span> 

### <a name="externally-exposed-aspnet-core-stateless-services"></a><span data-ttu-id="90791-254">Serviços sem monitoração de estado do Núcleo do ASP.NET expostos externamente</span><span class="sxs-lookup"><span data-stu-id="90791-254">Externally exposed ASP.NET Core stateless services</span></span>
<span data-ttu-id="90791-255">O WebListener é o servidor Web recomendado para serviços de front-end que expõem pontos de extremidade HTTP externos para a Internet no Windows.</span><span class="sxs-lookup"><span data-stu-id="90791-255">WebListener is the recommended web server for front-end services that expose external, Internet-facing HTTP endpoints on Windows.</span></span> <span data-ttu-id="90791-256">Ele oferece melhor proteção contra ataques e suporte a recursos para os quais o Kestrel não tem suporte, como a Autenticação do Windows e o compartilhamento de portas.</span><span class="sxs-lookup"><span data-stu-id="90791-256">It provides better protection against attacks and supports features that Kestrel does not, such as Windows Authentication and port sharing.</span></span> 

<span data-ttu-id="90791-257">Não há suporte para o Kestrel como um servidor de borda (para a Internet) no momento.</span><span class="sxs-lookup"><span data-stu-id="90791-257">Kestrel is not supported as an edge (Internet-facing) server at this time.</span></span> <span data-ttu-id="90791-258">Um servidor proxy reverso como o IIS ou Nginx deve ser usado para tratar do tráfego da Internet pública.</span><span class="sxs-lookup"><span data-stu-id="90791-258">A reverse proxy server such as IIS or Nginx must be used to handle traffic from the public Internet.</span></span>
 
<span data-ttu-id="90791-259">Quando exposto à Internet, um serviço sem estado deve usar um ponto de extremidade conhecido e estável que possa ser acessado por meio de um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="90791-259">When exposed to the Internet, a stateless service should use a well-known and stable endpoint that is reachable through a load balancer.</span></span> <span data-ttu-id="90791-260">Essa é a URL que você fornecerá aos usuários do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="90791-260">This is the URL you will provide to users of your application.</span></span> <span data-ttu-id="90791-261">Recomenda-se a seguinte configuração:</span><span class="sxs-lookup"><span data-stu-id="90791-261">The following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="90791-262">**Observações**</span><span class="sxs-lookup"><span data-stu-id="90791-262">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="90791-263">Servidor Web</span><span class="sxs-lookup"><span data-stu-id="90791-263">Web server</span></span> | <span data-ttu-id="90791-264">WebListener</span><span class="sxs-lookup"><span data-stu-id="90791-264">WebListener</span></span> | <span data-ttu-id="90791-265">Se o serviço for exposto somente para uma rede confiável, como uma intranet, o Kestrel poderá ser usado.</span><span class="sxs-lookup"><span data-stu-id="90791-265">If the service is only exposed to a trusted network, such an intranet, Kestrel may be used.</span></span> <span data-ttu-id="90791-266">Caso contrário, o WebListener é a opção preferencial.</span><span class="sxs-lookup"><span data-stu-id="90791-266">Otherwise, WebListener is the preferred option.</span></span> |
| <span data-ttu-id="90791-267">Configuração de portas</span><span class="sxs-lookup"><span data-stu-id="90791-267">Port configuration</span></span> | <span data-ttu-id="90791-268">estático</span><span class="sxs-lookup"><span data-stu-id="90791-268">static</span></span> | <span data-ttu-id="90791-269">Uma porta estática conhecida deve ser configurada na configuração do `Endpoints` de ServiceManifest.XML, como 80 para HTTP ou 443 para HTTPS.</span><span class="sxs-lookup"><span data-stu-id="90791-269">A well-known static port should be configured in the `Endpoints` configuration of ServiceManifest.xml, such as 80 for HTTP or 443 for HTTPS.</span></span> |
| <span data-ttu-id="90791-270">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="90791-270">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="90791-271">Nenhum</span><span class="sxs-lookup"><span data-stu-id="90791-271">None</span></span> | <span data-ttu-id="90791-272">A opção `ServiceFabricIntegrationOptions.None` deve ser usada quando a configuração de middleware de integração do Service Fabric para o serviço não tentar validar as solicitações de entrada para um identificador exclusivo.</span><span class="sxs-lookup"><span data-stu-id="90791-272">The `ServiceFabricIntegrationOptions.None` option should be used when configuring Service Fabric integration middleware so that the service does not attempt to validate incoming requests for a unique identifier.</span></span> <span data-ttu-id="90791-273">Os usuários externos do aplicativo não saberão as informações de identificação exclusivas usadas pelo middleware.</span><span class="sxs-lookup"><span data-stu-id="90791-273">External users of your application will not know the unique identifying information used by the middleware.</span></span> |
| <span data-ttu-id="90791-274">Contagem de Instâncias</span><span class="sxs-lookup"><span data-stu-id="90791-274">Instance Count</span></span> | <span data-ttu-id="90791-275">-1</span><span class="sxs-lookup"><span data-stu-id="90791-275">-1</span></span> | <span data-ttu-id="90791-276">Em casos de uso típicos, a configuração de contagem de instâncias deve ser definida como "-1" para que uma instância esteja disponível em todos os nós que recebem o tráfego de um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="90791-276">In typical use cases, the instance count setting should be set to "-1" so that an instance is available on all nodes that receive traffic from a load balancer.</span></span> |

<span data-ttu-id="90791-277">Se vários serviços expostos externamente compartilharem o mesmo conjunto de nós, deverá ser usado um caminho de URL exclusivo e estável.</span><span class="sxs-lookup"><span data-stu-id="90791-277">If multiple externally exposed services share the same set of nodes, a unique but stable URL path should be used.</span></span> <span data-ttu-id="90791-278">Isso pode ser feito modificando a URL fornecida ao configurar IWebHost.</span><span class="sxs-lookup"><span data-stu-id="90791-278">This can be accomplished by modifying the URL provided when configuring IWebHost.</span></span> <span data-ttu-id="90791-279">Observe que isso se aplica somente ao WebListener.</span><span class="sxs-lookup"><span data-stu-id="90791-279">Note this applies to WebListener only.</span></span>

 ```csharp
 new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
 {
     url += "/MyUniqueServicePath";
 
     return new WebHostBuilder()
         .UseWebListener()
         ...
         .UseUrls(url)
         .Build();
 })
 ```

### <a name="internal-only-stateless-aspnet-core-service"></a><span data-ttu-id="90791-280">Serviço do Núcleo do ASP.NET sem estado somente para uso interno</span><span class="sxs-lookup"><span data-stu-id="90791-280">Internal-only stateless ASP.NET Core service</span></span>
<span data-ttu-id="90791-281">Os serviços sem monitoração de estado que são chamados apenas de dentro do cluster devem usar URLs exclusivas e portas atribuídas dinamicamente para garantir a cooperação entre vários serviços.</span><span class="sxs-lookup"><span data-stu-id="90791-281">Stateless services that are only called from within the cluster should use unique URLs and dynamically assigned ports to ensure cooperation between multiple services.</span></span> <span data-ttu-id="90791-282">Recomenda-se a seguinte configuração:</span><span class="sxs-lookup"><span data-stu-id="90791-282">The following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="90791-283">**Observações**</span><span class="sxs-lookup"><span data-stu-id="90791-283">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="90791-284">Servidor Web</span><span class="sxs-lookup"><span data-stu-id="90791-284">Web server</span></span> | <span data-ttu-id="90791-285">Kestrel</span><span class="sxs-lookup"><span data-stu-id="90791-285">Kestrel</span></span> | <span data-ttu-id="90791-286">Embora o WebListener possa ser usado para serviços internos sem estado, o Kestrel é o servidor recomendado para permitir que várias instâncias do serviço compartilhem um host.</span><span class="sxs-lookup"><span data-stu-id="90791-286">Although WebListener may be used for internal stateless services, Kestrel is the recommended server to allow multiple service instances to share a host.</span></span>  |
| <span data-ttu-id="90791-287">Configuração de portas</span><span class="sxs-lookup"><span data-stu-id="90791-287">Port configuration</span></span> | <span data-ttu-id="90791-288">atribuídas dinamicamente</span><span class="sxs-lookup"><span data-stu-id="90791-288">dynamically assigned</span></span> | <span data-ttu-id="90791-289">Várias réplicas de um serviço com estado podem compartilhar um processo de host ou o sistema operacional do host e, assim, precisarão de portas exclusivas.</span><span class="sxs-lookup"><span data-stu-id="90791-289">Multiple replicas of a stateful service may share a host process or host operating system and thus will need unique ports.</span></span> |
| <span data-ttu-id="90791-290">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="90791-290">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="90791-291">UseUniqueServiceUrl</span><span class="sxs-lookup"><span data-stu-id="90791-291">UseUniqueServiceUrl</span></span> | <span data-ttu-id="90791-292">Com a atribuição dinâmica de portas essa configuração impede o problema de confusão de identidade descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="90791-292">With dynamic port assignment, this setting prevents the mistaken identity issue described earlier.</span></span> |
| <span data-ttu-id="90791-293">InstanceCount</span><span class="sxs-lookup"><span data-stu-id="90791-293">InstanceCount</span></span> | <span data-ttu-id="90791-294">qualquer</span><span class="sxs-lookup"><span data-stu-id="90791-294">any</span></span> | <span data-ttu-id="90791-295">A configuração de contagem de instâncias pode ser definida como qualquer valor necessário para operar o serviço.</span><span class="sxs-lookup"><span data-stu-id="90791-295">The instance count setting can be set to any value necessary to operate the service.</span></span> |

### <a name="internal-only-stateful-aspnet-core-service"></a><span data-ttu-id="90791-296">Somente interno serviço com estado do Núcleo do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="90791-296">Internal-only stateful ASP.NET Core service</span></span>
<span data-ttu-id="90791-297">Os serviços com monitoração de estado que são chamados apenas de dentro do cluster devem usar portas atribuídas dinamicamente para garantir a cooperação entre vários serviços.</span><span class="sxs-lookup"><span data-stu-id="90791-297">Stateful services that are only called from within the cluster should use dynamically assigned ports to ensure cooperation between multiple services.</span></span> <span data-ttu-id="90791-298">Recomenda-se a seguinte configuração:</span><span class="sxs-lookup"><span data-stu-id="90791-298">The following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="90791-299">**Observações**</span><span class="sxs-lookup"><span data-stu-id="90791-299">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="90791-300">Servidor Web</span><span class="sxs-lookup"><span data-stu-id="90791-300">Web server</span></span> | <span data-ttu-id="90791-301">Kestrel</span><span class="sxs-lookup"><span data-stu-id="90791-301">Kestrel</span></span> | <span data-ttu-id="90791-302">O `WebListenerCommunicationListener` não foi projetado para uso pelos serviços com monitoração de estado em que réplicas compartilham um processo de host.</span><span class="sxs-lookup"><span data-stu-id="90791-302">The `WebListenerCommunicationListener` is not designed for use by stateful services in which replicas share a host process.</span></span> |
| <span data-ttu-id="90791-303">Configuração de portas</span><span class="sxs-lookup"><span data-stu-id="90791-303">Port configuration</span></span> | <span data-ttu-id="90791-304">atribuídas dinamicamente</span><span class="sxs-lookup"><span data-stu-id="90791-304">dynamically assigned</span></span> | <span data-ttu-id="90791-305">Várias réplicas de um serviço com estado podem compartilhar um processo de host ou o sistema operacional do host e, assim, precisarão de portas exclusivas.</span><span class="sxs-lookup"><span data-stu-id="90791-305">Multiple replicas of a stateful service may share a host process or host operating system and thus will need unique ports.</span></span> |
| <span data-ttu-id="90791-306">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="90791-306">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="90791-307">UseUniqueServiceUrl</span><span class="sxs-lookup"><span data-stu-id="90791-307">UseUniqueServiceUrl</span></span> | <span data-ttu-id="90791-308">Com a atribuição dinâmica de portas essa configuração impede o problema de confusão de identidade descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="90791-308">With dynamic port assignment, this setting prevents the mistaken identity issue described earlier.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="90791-309">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="90791-309">Next steps</span></span>
[<span data-ttu-id="90791-310">Depurar seu aplicativo do Service Fabric usando o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="90791-310">Debug your Service Fabric application by using Visual Studio</span></span>](service-fabric-debugging-your-application.md)

<!--Image references-->
[0]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-standalone.png
[1]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-servicefabric.png
[2]:./media/service-fabric-reliable-services-communication-aspnetcore/integration.png
[3]:./media/service-fabric-reliable-services-communication-aspnetcore/httpsys.png
[4]:./media/service-fabric-reliable-services-communication-aspnetcore/kestrel.png
