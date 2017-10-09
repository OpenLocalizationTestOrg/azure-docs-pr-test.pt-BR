---
title: "comunicação aaaService com hello ASP.NET Core | Microsoft Docs"
description: "Saiba como toouse ASP.NET Core em serviços confiáveis com e sem monitoração."
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
ms.openlocfilehash: 6e6a83ab04390150292f63de5d9b51d290284e50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-core-in-service-fabric-reliable-services"></a><span data-ttu-id="a0e1f-103">Núcleo do ASP.NET em Serviços Confiáveis do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a0e1f-103">ASP.NET Core in Service Fabric Reliable Services</span></span>

<span data-ttu-id="a0e1f-104">O Núcleo do ASP.NET é uma nova estrutura de software livre e plataforma cruzada para criar aplicativos modernos baseados em nuvem conectados à Internet, como aplicativos Web, aplicativos de IoT e back-ends móveis.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-104">ASP.NET Core is a new open-source and cross-platform framework for building modern cloud-based Internet-connected applications, such as web apps, IoT apps, and mobile backends.</span></span> 

<span data-ttu-id="a0e1f-105">Este artigo é uma toohosting guia detalhado ASP.NET Core services no serviço de malha serviços confiáveis usando Olá **Microsoft.ServiceFabric.AspNetCore.** * conjunto de pacotes do NuGet.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-105">This article is an in-depth guide toohosting ASP.NET Core services in Service Fabric Reliable Services using hello **Microsoft.ServiceFabric.AspNetCore.*** set of NuGet packages.</span></span>

<span data-ttu-id="a0e1f-106">Para obter um tutorial de introdução sobre o ASP.NET Core no Service Fabric, além de instruções sobre como configurar o ambiente de desenvolvimento, consulte [Criando um front-end da Web para seu aplicativo usando o ASP.NET Core](service-fabric-add-a-web-frontend.md).</span><span class="sxs-lookup"><span data-stu-id="a0e1f-106">For an introductory tutorial on ASP.NET Core in Service Fabric and instructions on getting your development environment set up, see [Building a web front-end for your application using ASP.NET Core](service-fabric-add-a-web-frontend.md).</span></span>

<span data-ttu-id="a0e1f-107">restante Olá deste artigo pressupõe que você já estiver familiarizado com o ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-107">hello rest of this article assumes you are already familiar with ASP.NET Core.</span></span> <span data-ttu-id="a0e1f-108">Se não, é recomendável ler Olá [conceitos básicos do ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/index).</span><span class="sxs-lookup"><span data-stu-id="a0e1f-108">If not, we recommend reading through hello [ASP.NET Core fundamentals](https://docs.microsoft.com/aspnet/core/fundamentals/index).</span></span>

## <a name="aspnet-core-in-hello-service-fabric-environment"></a><span data-ttu-id="a0e1f-109">ASP.NET Core no ambiente do Service Fabric Olá</span><span class="sxs-lookup"><span data-stu-id="a0e1f-109">ASP.NET Core in hello Service Fabric environment</span></span>

<span data-ttu-id="a0e1f-110">Enquanto os aplicativos ASP.NET Core podem ser executado no .NET Core ou em Olá em que completa do .NET Framework, os serviços do Service Fabric atualmente só pode executar Olá .NET Framework completo.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-110">While ASP.NET Core apps can run on .NET Core or on hello full .NET Framework, Service Fabric services currently can only run on hello full .NET Framework.</span></span> <span data-ttu-id="a0e1f-111">Isso significa que quando você criar um serviço do Service Fabric do ASP.NET Core, você deve direcionar ainda Olá .NET Framework completo.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-111">This means when you build an ASP.NET  Core Service Fabric service, you must still target hello full .NET Framework.</span></span>

<span data-ttu-id="a0e1f-112">O Núcleo do ASP.NET pode ser usado de duas maneiras diferentes no Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="a0e1f-112">ASP.NET Core can be used in two different ways in Service Fabric:</span></span>
 - <span data-ttu-id="a0e1f-113">**Hospedado como um executável convidado**.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-113">**Hosted as a guest executable**.</span></span> <span data-ttu-id="a0e1f-114">Isso é principalmente usado toorun ASP.NET Core aplicativos existentes na malha do serviço sem alterações de código.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-114">This is primarily used toorun existing ASP.NET Core applications on Service Fabric with no code changes.</span></span>
 - <span data-ttu-id="a0e1f-115">**Executar em um Serviço Confiável**.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-115">**Run inside a Reliable Service**.</span></span> <span data-ttu-id="a0e1f-116">Isso permite melhor integração com o tempo de execução do Service Fabric hello e permite que os serviços com monitoração de estado do ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-116">This allows better integration with hello Service Fabric runtime and allows stateful ASP.NET Core services.</span></span>

<span data-ttu-id="a0e1f-117">restante Olá este artigo explica como toouse ASP.NET Core dentro de um serviço confiável usando Olá componentes de integração do ASP.NET Core que vêm com hello SDK do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-117">hello rest of this article explains how toouse ASP.NET Core inside a Reliable Service using hello ASP.NET Core integration components that ship with hello Service Fabric SDK.</span></span> 

## <a name="service-fabric-service-hosting"></a><span data-ttu-id="a0e1f-118">Hospedagem de serviços do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a0e1f-118">Service Fabric service hosting</span></span>

<span data-ttu-id="a0e1f-119">No Service Fabric, uma ou mais instâncias e/ou réplicas do serviço são executadas em um *processo de host do serviço*, um arquivo executável que executa o código de serviço.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-119">In Service Fabric, one or more instances and/or replicas of your service run in a *service host process*, an executable file that runs your service code.</span></span> <span data-ttu-id="a0e1f-120">Como o autor de um serviço, possui processo de host de serviço hello e do Service Fabric ativa e monitora-lo para você.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-120">You, as a service author, own hello service host process and Service Fabric activates and monitors it for you.</span></span>

<span data-ttu-id="a0e1f-121">O ASP.NET tradicional (backup tooMVC 5) é firmemente acopladas tooIIS por meio de System.Web.dll.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-121">Traditional ASP.NET (up tooMVC 5) is tightly coupled tooIIS through System.Web.dll.</span></span> <span data-ttu-id="a0e1f-122">ASP.NET Core fornece uma separação entre o servidor de web hello e seu aplicativo da web.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-122">ASP.NET Core provides a separation between hello web server and your web application.</span></span> <span data-ttu-id="a0e1f-123">Isso permite toobe de aplicativos web portáveis entre diversos servidores web e também permite que toobe de servidores de web *auto-hospedado*, que significa que você pode iniciar um servidor web no seu próprio processo, como um processo de tooa contrário é de propriedade da web dedicado software de servidor como o IIS.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-123">This allows web applications toobe portable between different web servers and also allows web servers toobe *self-hosted*, which means you can start a web server in your own process, as opposed tooa process that is owned by dedicated web server software such as IIS.</span></span> 

<span data-ttu-id="a0e1f-124">Em ordem toocombine um serviço de malha do serviço e o ASP.NET, como um executável de convidado ou em um serviço confiável, você deve ser capaz de toostart ASP.NET dentro de seu processo de host de serviço.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-124">In order toocombine a Service Fabric service and ASP.NET, either as a guest executable or in a Reliable Service, you must be able toostart ASP.NET inside your service host process.</span></span> <span data-ttu-id="a0e1f-125">ASP.NET Core auto-hospedagem permite toodo isso.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-125">ASP.NET Core self-hosting allows you toodo this.</span></span>

## <a name="hosting-aspnet-core-in-a-reliable-service"></a><span data-ttu-id="a0e1f-126">Hospedando o Núcleo do ASP.NET em um Serviço Confiável</span><span class="sxs-lookup"><span data-stu-id="a0e1f-126">Hosting ASP.NET Core in a Reliable Service</span></span>
<span data-ttu-id="a0e1f-127">Normalmente, os aplicativos do ASP.NET Core auto-hospedado criam WebHost no ponto de entrada do aplicativo, como Olá `static void Main()` método `Program.cs`.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-127">Typically, self-hosted ASP.NET Core applications create a WebHost in an application's entry point, such as hello `static void Main()` method in `Program.cs`.</span></span> <span data-ttu-id="a0e1f-128">Nesse caso, o ciclo de vida de saudação de saudação WebHost é toohello associado de ciclo de vida do processo de saudação.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-128">In this case, hello lifecycle of hello WebHost is bound toohello lifecycle of hello process.</span></span>

![Hospedando o Núcleo do ASP.NET em um processo][0]

<span data-ttu-id="a0e1f-130">No entanto, ponto de entrada do aplicativo hello não Olá lugar certo toocreate WebHost em um serviço confiável, porque o ponto de entrada do aplicativo hello é usado somente tooregister um serviço digitar com tempo de execução do Service Fabric hello, para que ele pode criar instâncias de serviço tipo.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-130">However, hello application entry point is not hello right place toocreate a WebHost in a Reliable Service, because hello application entry point is only used tooregister a service type with hello Service Fabric runtime, so that it may create instances of that service type.</span></span> <span data-ttu-id="a0e1f-131">Olá WebHost deve ser criado em um serviço confiável em si.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-131">hello WebHost should be created in a Reliable Service itself.</span></span> <span data-ttu-id="a0e1f-132">No processo de host de serviço hello, instâncias de serviço e/ou réplicas podem passar por vários ciclos de vida.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-132">Within hello service host process, service instances and/or replicas can go through multiple lifecycles.</span></span> 

<span data-ttu-id="a0e1f-133">Uma instância de um serviço confiável é representada por sua classe de serviço derivando de `StatelessService` ou `StatefulService`.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-133">A Reliable Service instance is represented by your service class deriving from `StatelessService` or `StatefulService`.</span></span> <span data-ttu-id="a0e1f-134">pilha de comunicação de saudação para um serviço está contida em um `ICommunicationListener` implementação em sua classe de serviço.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-134">hello communication stack for a service is contained in an `ICommunicationListener` implementation in your service class.</span></span> <span data-ttu-id="a0e1f-135">Olá `Microsoft.ServiceFabric.Services.AspNetCore.*` pacotes do NuGet contenham implementações de `ICommunicationListener` que iniciar e gerenciar Olá ASP.NET Core WebHost para Kestrel ou WebListener em um serviço confiável.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-135">hello `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet packages contain implementations of `ICommunicationListener` that start and manage hello ASP.NET Core WebHost for either Kestrel or WebListener in a Reliable Service.</span></span>

![Hospedando o Núcleo do ASP.NET em um Serviço Confiável][1]

## <a name="aspnet-core-icommunicationlisteners"></a><span data-ttu-id="a0e1f-137">Núcleo do ASP.NET ICommunicationListeners</span><span class="sxs-lookup"><span data-stu-id="a0e1f-137">ASP.NET Core ICommunicationListeners</span></span>
<span data-ttu-id="a0e1f-138">Olá `ICommunicationListener` implementações para Kestrel e WebListener no hello `Microsoft.ServiceFabric.Services.AspNetCore.*` pacotes do NuGet têm padrões de uso semelhantes, mas executar o servidor de web específicos tooeach ações ligeiramente diferentes.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-138">hello `ICommunicationListener` implementations for Kestrel and WebListener in hello  `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet packages have similar use patterns but perform slightly different actions specific tooeach web server.</span></span> 

<span data-ttu-id="a0e1f-139">Ambos os ouvintes de comunicação fornecem um construtor que aceite Olá argumentos a seguir:</span><span class="sxs-lookup"><span data-stu-id="a0e1f-139">Both communication listeners provide a constructor that takes hello following arguments:</span></span>
 - <span data-ttu-id="a0e1f-140">**`ServiceContext serviceContext`**: Olá `ServiceContext` objeto que contém informações sobre Olá executando o serviço.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-140">**`ServiceContext serviceContext`**: hello `ServiceContext` object that contains information about hello running service.</span></span>
 - <span data-ttu-id="a0e1f-141">**`string endpointName`**: nome de saudação de um `Endpoint` configuração em ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-141">**`string endpointName`**: hello name of an `Endpoint` configuration in ServiceManifest.xml.</span></span> <span data-ttu-id="a0e1f-142">Isso é, principalmente, onde os ouvintes de comunicação Olá dois diferem: WebListener **requer** um `Endpoint` configuração, enquanto Kestrel não.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-142">This is primarily where hello two communication listeners differ: WebListener **requires** an `Endpoint` configuration, while Kestrel does not.</span></span>
 - <span data-ttu-id="a0e1f-143">**`Func<string, AspNetCoreCommunicationListener, IWebHost> build`**: um lambda que você implementa e no qual cria e retorna um `IWebHost`.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-143">**`Func<string, AspNetCoreCommunicationListener, IWebHost> build`**: a lambda that you implement in which you create and return an `IWebHost`.</span></span> <span data-ttu-id="a0e1f-144">Isso permite tooconfigure `IWebHost` hello como faz normalmente em um aplicativo do ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-144">This allows you tooconfigure `IWebHost` hello way you normally would in an ASP.NET Core application.</span></span> <span data-ttu-id="a0e1f-145">lambda Hello fornece uma URL que é gerada para você dependendo da integração do Service Fabric Olá opções use e hello `Endpoint` configuração que você fornecer.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-145">hello lambda provides a URL which is generated for you depending on hello Service Fabric integration options you use and hello `Endpoint` configuration you provide.</span></span> <span data-ttu-id="a0e1f-146">URL, em seguida, pode ser modificada ou usada como-é toostart Olá web server.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-146">That URL can then be modified or used as-is toostart hello web server.</span></span>

## <a name="service-fabric-integration-middleware"></a><span data-ttu-id="a0e1f-147">Middleware de integração do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a0e1f-147">Service Fabric integration middleware</span></span>
<span data-ttu-id="a0e1f-148">Olá `Microsoft.ServiceFabric.Services.AspNetCore` inclui o pacote NuGet Olá `UseServiceFabricIntegration` método de extensão no `IWebHostBuilder` que adiciona o middleware de reconhecimento de serviço do Fabric.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-148">hello `Microsoft.ServiceFabric.Services.AspNetCore` NuGet package includes hello `UseServiceFabricIntegration` extension method on `IWebHostBuilder` that adds Service Fabric-aware middleware.</span></span> <span data-ttu-id="a0e1f-149">Este middleware configura Olá Kestrel ou WebListener `ICommunicationListener` tooregister uma URL de serviço exclusivo com hello serviço de nomes de malha do serviço e, em seguida, valida os clientes tooensure de solicitações de cliente estão se conectando toohello certo de serviço.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-149">This middleware configures hello Kestrel or WebListener `ICommunicationListener` tooregister a unique service URL with hello Service Fabric Naming Service and then validates client requests tooensure clients are connecting toohello right service.</span></span> <span data-ttu-id="a0e1f-150">Isso é necessário em um ambiente de host compartilhado como Service Fabric, em que vários aplicativos web podem executar em Olá mesmo físico ou máquina virtual, mas não usam nomes de host exclusiva, tooprevent clientes conectem o serviço errada toohello por engano.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-150">This is necessary in a shared-host environment such as Service Fabric, where multiple web applications can run on hello same physical or virtual machine but do not use unique host names, tooprevent clients from mistakenly connecting toohello wrong service.</span></span> <span data-ttu-id="a0e1f-151">Este cenário é descrito mais detalhadamente na próxima seção, Olá.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-151">This scenario is described in more detail in hello next section.</span></span>

### <a name="a-case-of-mistaken-identity"></a><span data-ttu-id="a0e1f-152">Um caso de identidade incorreta</span><span class="sxs-lookup"><span data-stu-id="a0e1f-152">A case of mistaken identity</span></span>
<span data-ttu-id="a0e1f-153">Independentemente do protocolo, as réplicas de serviço escutam em uma combinação de IP:porta exclusiva.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-153">Service replicas, regardless of protocol, listen on a unique IP:port combination.</span></span> <span data-ttu-id="a0e1f-154">Após o início de uma réplica de serviço escuta em um ponto de extremidade IP: porta informa esse endereço de ponto de extremidade toohello serviço de nomenclatura do Service Fabric onde podem ser descoberto por clientes ou outros serviços.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-154">Once a service replica has started listening on an IP:port endpoint, it reports that endpoint address toohello Service Fabric Naming Service where it can be discovered by clients or other services.</span></span> <span data-ttu-id="a0e1f-155">Se os serviços usam portas atribuídas dinamicamente o aplicativo, uma réplica de serviço podem usar Coincidentemente Olá mesmo ponto de extremidade IP: porta de outro serviço que foi previamente no hello mesmo físico ou máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-155">If services use dynamically-assigned application ports, a service replica may coincidentally use hello same IP:port endpoint of another service that was previously on hello same physical or virtual machine.</span></span> <span data-ttu-id="a0e1f-156">Isso pode fazer com que um cliente toomistakely conectar serviço errada toohello.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-156">This can cause a client toomistakely connect toohello wrong service.</span></span> <span data-ttu-id="a0e1f-157">Isso pode acontecer se Olá a sequência de eventos a seguir ocorre:</span><span class="sxs-lookup"><span data-stu-id="a0e1f-157">This can happen if hello following sequence of events occur:</span></span>

 1. <span data-ttu-id="a0e1f-158">O serviço A escuta em 10.0.0.1:30000 via HTTP.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-158">Service A listens on 10.0.0.1:30000 over HTTP.</span></span> 
 2. <span data-ttu-id="a0e1f-159">O cliente resolve o serviço A e obtém o endereço 10.0.0.1:30000</span><span class="sxs-lookup"><span data-stu-id="a0e1f-159">Client resolves Service A and gets address 10.0.0.1:30000</span></span>
 3. <span data-ttu-id="a0e1f-160">Move tooa outro nó do serviço.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-160">Service A moves tooa different node.</span></span>
 4. <span data-ttu-id="a0e1f-161">Serviço B é colocado na 10.0.0.1 e Coincidentemente usa Olá a mesma porta 30000.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-161">Service B is placed on 10.0.0.1 and coincidentally uses hello same port 30000.</span></span>
 5. <span data-ttu-id="a0e1f-162">Cliente tenta tooconnect tooservice um com 10.0.0.1:30000 endereço em cache.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-162">Client attempts tooconnect tooservice A with cached address 10.0.0.1:30000.</span></span>
 6. <span data-ttu-id="a0e1f-163">Cliente está conectado com êxito tooservice B sem perceber que ele está conectado serviço errada toohello.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-163">Client is now successfully connected tooservice B not realizing it is connected toohello wrong service.</span></span>

<span data-ttu-id="a0e1f-164">Isso pode causar erros em momentos aleatórios que podem ser difícil toodiagnose.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-164">This can cause bugs at random times that can be difficult toodiagnose.</span></span> 

### <a name="using-unique-service-urls"></a><span data-ttu-id="a0e1f-165">Usando URLs de serviço exclusivas</span><span class="sxs-lookup"><span data-stu-id="a0e1f-165">Using unique service URLs</span></span>
<span data-ttu-id="a0e1f-166">Serviços de tooprevent isso, pode lançar um toohello Naming Service com um identificador exclusivo do ponto de extremidade e validar esse identificador exclusivo durante as solicitações de cliente.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-166">tooprevent this, services can post an endpoint toohello Naming Service with a unique identifier, and then validate that unique identifier during client requests.</span></span> <span data-ttu-id="a0e1f-167">Essa é uma ação cooperativa entre serviços em um ambiente confiável de locatário não hostil.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-167">This is a cooperative action between services in a non-hostile-tenant trusted environment.</span></span> <span data-ttu-id="a0e1f-168">Isso não fornece autenticação segura em um ambiente de locatário hostil.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-168">This does not provide secure service authentication in a hostile-tenant environment.</span></span>

<span data-ttu-id="a0e1f-169">Em um ambiente confiável, Olá middleware é adicionada pelo Olá `UseServiceFabricIntegration` método anexa automaticamente um endereço de toohello de identificador exclusivo que é lançado toohello Naming Service e valida esse identificador em cada solicitação.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-169">In a trusted environment, hello middleware that's added by hello `UseServiceFabricIntegration` method automatically appends a unique identifier toohello address that is posted toohello Naming Service and validates that identifier on each request.</span></span> <span data-ttu-id="a0e1f-170">Se o identificador de saudação não corresponder, Olá middleware imediatamente retorna uma resposta HTTP 410 não existe mais.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-170">If hello identifier does not match, hello middleware immediately returns an HTTP 410 Gone response.</span></span>

<span data-ttu-id="a0e1f-171">Os serviços que usam uma porta atribuída dinamicamente devem fazer uso desse middleware.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-171">Services that use a dynamically-assigned port should make use of this middleware.</span></span>

<span data-ttu-id="a0e1f-172">Os serviços que usam uma porta exclusiva fixa não têm esse problema em um ambiente cooperativo.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-172">Services that use a fixed unique port do not have this problem in a cooperative environment.</span></span> <span data-ttu-id="a0e1f-173">Uma porta exclusiva fixa é normalmente usada para externamente serviços que precisam de uma porta conhecida para tooconnect de aplicativos cliente para.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-173">A fixed unique port is typically used for externally-facing services that need a well-known port for client applications tooconnect to.</span></span> <span data-ttu-id="a0e1f-174">Por exemplo, a maioria dos aplicativos Web voltados para a Internet usará a porta 80 ou 443 para conexões do navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-174">For example, most Internet-facing web applications will use port 80 or 443 for web browser connections.</span></span> <span data-ttu-id="a0e1f-175">Nesse caso, identificador exclusivo da saudação não deve ser habilitado.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-175">In this case, hello unique identifier should not be enabled.</span></span>

<span data-ttu-id="a0e1f-176">Hello diagrama a seguir mostra o fluxo de solicitação Olá com middleware Olá habilitado:</span><span class="sxs-lookup"><span data-stu-id="a0e1f-176">hello following diagram shows hello request flow with hello middleware enabled:</span></span>

![Integração de núcleo do ASP.NET do Service Fabric][2]

<span data-ttu-id="a0e1f-178">Kestrel e WebListener `ICommunicationListener` implementações usam esse mecanismo em exatamente Olá mesma maneira.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-178">Both Kestrel and WebListener `ICommunicationListener` implementations use this mechanism in exactly hello same way.</span></span> <span data-ttu-id="a0e1f-179">Embora WebListener internamente pode diferenciar solicitações baseadas em caminhos de URL exclusivos usando Olá subjacente *http.sys* recurso, que é a funcionalidade de compartilhamento de porta *não* usado pelo Olá WebListener `ICommunicationListener` implementação porque isso resultará em códigos de status de erro HTTP 503 e HTTP 404 no cenário de saudação descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-179">Although WebListener can internally differentiate requests based on unique URL paths using hello underlying *http.sys* port sharing feature, that functionality is *not* used by hello WebListener `ICommunicationListener` implementation because that will result in HTTP 503 and HTTP 404 error status codes in hello scenario described earlier.</span></span> <span data-ttu-id="a0e1f-180">Que por sua vez torna muito difícil para os clientes toodetermine Olá intenção erro hello, como HTTP 503 e HTTP 404 já são utilizado tooindicate outros erros.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-180">That in turn makes it very difficult for clients toodetermine hello intent of hello error, as HTTP 503 and HTTP 404 are already commonly used tooindicate other errors.</span></span> <span data-ttu-id="a0e1f-181">Assim, os Kestrel e WebListener `ICommunicationListener` implementações padronizem Olá middleware fornecido pelo Olá `UseServiceFabricIntegration` método de extensão para que os clientes precisam apenas tooperform um ponto de extremidade de serviço resolver ação em respostas HTTP 410 novamente.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-181">Thus, both Kestrel and WebListener `ICommunicationListener` implementations standardize on hello middleware provided by hello `UseServiceFabricIntegration` extension method so that clients only need tooperform a service endpoint re-resolve action on HTTP 410 responses.</span></span>

## <a name="weblistener-in-reliable-services"></a><span data-ttu-id="a0e1f-182">WebListener em Serviços Confiáveis</span><span class="sxs-lookup"><span data-stu-id="a0e1f-182">WebListener in Reliable Services</span></span>
<span data-ttu-id="a0e1f-183">WebListener pode ser usado em um serviço confiável importando Olá **Microsoft.ServiceFabric.AspNetCore.WebListener** pacote NuGet.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-183">WebListener can be used in a Reliable Service by importing hello **Microsoft.ServiceFabric.AspNetCore.WebListener** NuGet package.</span></span> <span data-ttu-id="a0e1f-184">Este pacote contém `WebListenerCommunicationListener`, uma implementação de `ICommunicationListener`, que permite que você toocreate um host de Web ASP.NET Core dentro de um serviço confiável usando WebListener como servidor de web hello.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-184">This package contains `WebListenerCommunicationListener`, an implementation of `ICommunicationListener`, that allows you toocreate an ASP.NET Core WebHost inside a Reliable Service using WebListener as hello web server.</span></span>

<span data-ttu-id="a0e1f-185">WebListener se baseia no hello [Windows HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510(v=vs.85).aspx).</span><span class="sxs-lookup"><span data-stu-id="a0e1f-185">WebListener is built on hello [Windows HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510(v=vs.85).aspx).</span></span> <span data-ttu-id="a0e1f-186">Isso usa Olá *http.sys* driver de kernel usada pelo IIS tooprocess HTTP solicita e rotear tooprocesses-los executar aplicativos da web.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-186">This uses hello *http.sys* kernel driver used by IIS tooprocess HTTP requests and route them tooprocesses running web applications.</span></span> <span data-ttu-id="a0e1f-187">Isso permite que vários processos em Olá mesmos aplicativos de máquina virtual ou física de toohost web hello mesma porta, a ambiguidade removida por um caminho de URL exclusivo ou o nome do host.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-187">This allows multiple processes on hello same physical or virtual machine toohost web applications on hello same port, disambiguated by either a unique URL path or hostname.</span></span> <span data-ttu-id="a0e1f-188">Esses recursos são úteis na malha do serviço para hospedar vários sites em Olá mesmo cluster.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-188">These features are useful in Service Fabric for hosting multiple websites in hello same cluster.</span></span>

<span data-ttu-id="a0e1f-189">Olá diagrama a seguir ilustra como WebListener usa Olá *http.sys* driver de kernel no Windows para o compartilhamento de porta:</span><span class="sxs-lookup"><span data-stu-id="a0e1f-189">hello following diagram illustrates how WebListener uses hello *http.sys* kernel driver on Windows for port sharing:</span></span>

![http.sys][3]

### <a name="weblistener-in-a-stateless-service"></a><span data-ttu-id="a0e1f-191">WebListener em um serviço sem estado</span><span class="sxs-lookup"><span data-stu-id="a0e1f-191">WebListener in a stateless service</span></span>
<span data-ttu-id="a0e1f-192">toouse `WebListener` em um serviço sem monitoração de estado, substituir Olá `CreateServiceInstanceListeners` método e retornar um `WebListenerCommunicationListener` instância:</span><span class="sxs-lookup"><span data-stu-id="a0e1f-192">toouse `WebListener` in a stateless service, override hello `CreateServiceInstanceListeners` method and return a `WebListenerCommunicationListener` instance:</span></span>

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

### <a name="weblistener-in-a-stateful-service"></a><span data-ttu-id="a0e1f-193">WebListener em um serviço com estado</span><span class="sxs-lookup"><span data-stu-id="a0e1f-193">WebListener in a stateful service</span></span>

<span data-ttu-id="a0e1f-194">`WebListenerCommunicationListener`no momento não foi projetado para uso em serviços com monitoração de estado toocomplications vencimento com hello subjacente *http.sys* o recurso de compartilhamento de porta.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-194">`WebListenerCommunicationListener` is currently not designed for use in stateful services due toocomplications with hello underlying *http.sys* port sharing feature.</span></span> <span data-ttu-id="a0e1f-195">Para obter mais informações, consulte Olá na alocação de porta dinâmica com WebListener a seção seguinte.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-195">For more information, see hello following section on dynamic port allocation with WebListener.</span></span> <span data-ttu-id="a0e1f-196">Para os serviços com monitoração de estado, Kestrel é hello recomendado de servidor web.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-196">For stateful services, Kestrel is hello recommended web server.</span></span>

### <a name="endpoint-configuration"></a><span data-ttu-id="a0e1f-197">Configuração de ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="a0e1f-197">Endpoint configuration</span></span>

<span data-ttu-id="a0e1f-198">Um `Endpoint` configuração é necessária para servidores web que usam Olá Windows HTTP Server API, incluindo WebListener.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-198">An `Endpoint` configuration is required for web servers that use hello Windows HTTP Server API, including WebListener.</span></span> <span data-ttu-id="a0e1f-199">Servidores Web que usam Olá Windows HTTP Server API primeiro devem reservar a URL com *http.sys* (normalmente, isso é feito com hello [netsh](https://msdn.microsoft.com/library/windows/desktop/cc307236(v=vs.85).aspx) ferramenta).</span><span class="sxs-lookup"><span data-stu-id="a0e1f-199">Web servers that use hello Windows HTTP Server API must first reserve their URL with *http.sys* (this is normally accomplished with hello [netsh](https://msdn.microsoft.com/library/windows/desktop/cc307236(v=vs.85).aspx) tool).</span></span> <span data-ttu-id="a0e1f-200">Esta ação exige privilégios elevados que seus serviços não têm por padrão.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-200">This action requires elevated privileges that your services by default do not have.</span></span> <span data-ttu-id="a0e1f-201">Olá "http" ou "https" opções de saudação `Protocol` propriedade Olá `Endpoint` configuração no *ServiceManifest.xml* são usadas especificamente tooinstruct Olá tooregister de tempo de execução do Service Fabric uma URL com *http.sys* em seu nome usando Olá [ *curinga forte* ](https://msdn.microsoft.com/library/windows/desktop/aa364698(v=vs.85).aspx) prefixo de URL.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-201">hello "http" or "https" options for hello `Protocol` property of hello `Endpoint` configuration in *ServiceManifest.xml* are used specifically tooinstruct hello Service Fabric runtime tooregister a URL with *http.sys* on your behalf using hello [*strong wildcard*](https://msdn.microsoft.com/library/windows/desktop/aa364698(v=vs.85).aspx) URL prefix.</span></span>

<span data-ttu-id="a0e1f-202">Por exemplo, tooreserve `http://+:80` para um serviço, hello seguinte configuração deve ser usada em ServiceManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="a0e1f-202">For example, tooreserve `http://+:80` for a service, hello following configuration should be used in ServiceManifest.xml:</span></span>

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

<span data-ttu-id="a0e1f-203">E o nome do ponto de extremidade Olá deve ser passado toohello `WebListenerCommunicationListener` construtor:</span><span class="sxs-lookup"><span data-stu-id="a0e1f-203">And hello endpoint name must be passed toohello `WebListenerCommunicationListener` constructor:</span></span>

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

#### <a name="use-weblistener-with-a-static-port"></a><span data-ttu-id="a0e1f-204">Usar WebListener com uma porta estática</span><span class="sxs-lookup"><span data-stu-id="a0e1f-204">Use WebListener with a static port</span></span>
<span data-ttu-id="a0e1f-205">toouse uma porta estática com WebListener, forneça o número de porta de saudação em Olá `Endpoint` configuração:</span><span class="sxs-lookup"><span data-stu-id="a0e1f-205">toouse a static port with WebListener, provide hello port number in hello `Endpoint` configuration:</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

#### <a name="use-weblistener-with-a-dynamic-port"></a><span data-ttu-id="a0e1f-206">Usar WebListener com uma porta dinâmica</span><span class="sxs-lookup"><span data-stu-id="a0e1f-206">Use WebListener with a dynamic port</span></span>
<span data-ttu-id="a0e1f-207">toouse uma porta dinamicamente atribuída com WebListener, omita Olá `Port` propriedade Olá `Endpoint` configuração:</span><span class="sxs-lookup"><span data-stu-id="a0e1f-207">toouse a dynamically assigned port with WebListener, omit hello `Port` property in hello `Endpoint` configuration:</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" />
    </Endpoints>
  </Resources>
```

<span data-ttu-id="a0e1f-208">Observe que uma porta dinâmica alocada por uma configuração `Endpoint` fornece apenas uma porta *por processo de host*.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-208">Note that a dynamic port allocated by an `Endpoint` configuration only provides one port *per host process*.</span></span> <span data-ttu-id="a0e1f-209">Olá Service Fabric atual do modelo de hospedagem permite toobe vários para o instâncias e/ou réplicas do serviço hospedado no hello mesmo processo, que significa que cada um deles compartilharão Olá mesma porta quando alocados por meio do hello `Endpoint` configuração.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-209">hello current Service Fabric hosting model allows multiple service instances and/or replicas toobe hosted in hello same process, meaning that each one will share hello same port when allocated through hello `Endpoint` configuration.</span></span> <span data-ttu-id="a0e1f-210">Várias instâncias de WebListener podem compartilhar uma porta usando Olá subjacente *http.sys* porta compartilhamento de recurso, mas que não é suportada pelo `WebListenerCommunicationListener` devido complicações toohello ele apresenta solicitações do cliente.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-210">Multiple WebListener instances can share a port using hello underlying *http.sys* port sharing feature, but that is not supported by `WebListenerCommunicationListener` due toohello complications it introduces for client requests.</span></span> <span data-ttu-id="a0e1f-211">Para o uso de portas dinâmicas, Kestrel é hello recomendado de servidor web.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-211">For dynamic port usage, Kestrel is hello recommended web server.</span></span>

## <a name="kestrel-in-reliable-services"></a><span data-ttu-id="a0e1f-212">Kestrel em Serviços Confiáveis</span><span class="sxs-lookup"><span data-stu-id="a0e1f-212">Kestrel in Reliable Services</span></span>
<span data-ttu-id="a0e1f-213">Kestrel pode ser usado em um serviço confiável importando Olá **Microsoft.ServiceFabric.AspNetCore.Kestrel** pacote NuGet.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-213">Kestrel can be used in a Reliable Service by importing hello **Microsoft.ServiceFabric.AspNetCore.Kestrel** NuGet package.</span></span> <span data-ttu-id="a0e1f-214">Este pacote contém `KestrelCommunicationListener`, uma implementação de `ICommunicationListener`, que permite que você toocreate um host de Web ASP.NET Core dentro de um serviço confiável usando Kestrel como servidor de web hello.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-214">This package contains `KestrelCommunicationListener`, an implementation of `ICommunicationListener`, that allows you toocreate an ASP.NET Core WebHost inside a Reliable Service using Kestrel as hello web server.</span></span>

<span data-ttu-id="a0e1f-215">O Kestrel é um servidor Web de plataforma cruzada para o Núcleo do ASP.NET com base em libuv, uma biblioteca de E/S assíncrona de plataforma cruzada.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-215">Kestrel is a cross-platform web server for ASP.NET Core based on libuv, a cross-platform asynchronous I/O library.</span></span> <span data-ttu-id="a0e1f-216">Diferentemente do WebListener, o Kestrel usa um gerenciador de ponto de extremidade centralizado como *http.sys*.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-216">Unlike WebListener, Kestrel does not use a centralized endpoint manager such as *http.sys*.</span></span> <span data-ttu-id="a0e1f-217">Diferentemente do WebListener, Kestrel não dá suporte ao compartilhamento de porta entre vários processos.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-217">And unlike WebListener, Kestrel does not support port sharing between multiple processes.</span></span> <span data-ttu-id="a0e1f-218">Cada instância do Kestrel deve usar uma porta exclusiva.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-218">Each instance of Kestrel must use a unique port.</span></span>

![kestrel][4]

### <a name="kestrel-in-a-stateless-service"></a><span data-ttu-id="a0e1f-220">Kestrel em um serviço sem estado</span><span class="sxs-lookup"><span data-stu-id="a0e1f-220">Kestrel in a stateless service</span></span>
<span data-ttu-id="a0e1f-221">toouse `Kestrel` em um serviço sem monitoração de estado, substituir Olá `CreateServiceInstanceListeners` método e retornar um `KestrelCommunicationListener` instância:</span><span class="sxs-lookup"><span data-stu-id="a0e1f-221">toouse `Kestrel` in a stateless service, override hello `CreateServiceInstanceListeners` method and return a `KestrelCommunicationListener` instance:</span></span>

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

### <a name="kestrel-in-a-stateful-service"></a><span data-ttu-id="a0e1f-222">Kestrel em um serviço com estado</span><span class="sxs-lookup"><span data-stu-id="a0e1f-222">Kestrel in a stateful service</span></span>
<span data-ttu-id="a0e1f-223">toouse `Kestrel` em um serviço com monitoração de estado, substituir Olá `CreateServiceReplicaListeners` método e retornar um `KestrelCommunicationListener` instância:</span><span class="sxs-lookup"><span data-stu-id="a0e1f-223">toouse `Kestrel` in a stateful service, override hello `CreateServiceReplicaListeners` method and return a `KestrelCommunicationListener` instance:</span></span>

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

<span data-ttu-id="a0e1f-224">Neste exemplo, uma instância singleton do `IReliableStateManager` é fornecido o contêiner de injeção de dependência de WebHost toohello.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-224">In this example, a singleton instance of `IReliableStateManager` is provided toohello WebHost dependency injection container.</span></span> <span data-ttu-id="a0e1f-225">Isso não é estritamente necessário, mas permite que você toouse `IReliableStateManager` e coleções confiável em métodos de ação do controlador MVC.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-225">This is not strictly necessary, but it allows you toouse `IReliableStateManager` and Reliable Collections in your MVC controller action methods.</span></span>

<span data-ttu-id="a0e1f-226">Observe que uma `Endpoint` nome de configuração é **não** fornecido muito`KestrelCommunicationListener` em um serviço com monitoração de estado.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-226">Note that an `Endpoint` configuration name is **not** provided too`KestrelCommunicationListener` in a stateful service.</span></span> <span data-ttu-id="a0e1f-227">Isso é explicado mais detalhadamente Olá seção a seguir.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-227">This is explained in more detail in hello following section.</span></span>

### <a name="endpoint-configuration"></a><span data-ttu-id="a0e1f-228">Configuração de ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="a0e1f-228">Endpoint configuration</span></span>
<span data-ttu-id="a0e1f-229">Um `Endpoint` configuração não é necessário toouse Kestrel.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-229">An `Endpoint` configuration is not required toouse Kestrel.</span></span> 

<span data-ttu-id="a0e1f-230">Kestrel é um servidor web autônomo simples; Diferentemente de WebListener (ou HttpListener), não é necessário um `Endpoint` configuração no *ServiceManifest.xml* porque ele não requer toostarting anterior do registro de URL.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-230">Kestrel is a simple stand-alone web server; unlike WebListener (or HttpListener), it does not need an `Endpoint` configuration in *ServiceManifest.xml* because it does not require URL registration prior toostarting.</span></span> 

#### <a name="use-kestrel-with-a-static-port"></a><span data-ttu-id="a0e1f-231">Usar Kestrel com uma porta estática</span><span class="sxs-lookup"><span data-stu-id="a0e1f-231">Use Kestrel with a static port</span></span>
<span data-ttu-id="a0e1f-232">Uma porta estática pode ser configurada no hello `Endpoint` configuração do ServiceManifest.xml para uso com Kestrel.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-232">A static port can be configured in hello `Endpoint` configuration of ServiceManifest.xml for use with Kestrel.</span></span> <span data-ttu-id="a0e1f-233">Embora não seja estritamente necessário, há dois benefícios potenciais:</span><span class="sxs-lookup"><span data-stu-id="a0e1f-233">Although this is not strictly necessary, it provides two potential benefits:</span></span>
 1. <span data-ttu-id="a0e1f-234">Se a porta de saudação não está no intervalo de portas de aplicativo hello, ele é aberto através do firewall do sistema operacional Olá pela malha do serviço.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-234">If hello port does not fall in hello application port range, it is opened through hello OS firewall by Service Fabric.</span></span>
 2. <span data-ttu-id="a0e1f-235">Olá tooyou URL fornecida por meio de `KestrelCommunicationListener` usará essa porta.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-235">hello URL provided tooyou through `KestrelCommunicationListener` will use this port.</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

<span data-ttu-id="a0e1f-236">Se um `Endpoint` é configurado, seu nome deve ser passado para Olá `KestrelCommunicationListener` construtor:</span><span class="sxs-lookup"><span data-stu-id="a0e1f-236">If an `Endpoint` is configured, its name must be passed into hello `KestrelCommunicationListener` constructor:</span></span> 

```csharp
new KestrelCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) => ...
```

<span data-ttu-id="a0e1f-237">Se um `Endpoint` configuração não for usada, omitir o nome da saudação em Olá `KestrelCommunicationListener` construtor.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-237">If an `Endpoint` configuration is not used, omit hello name in hello `KestrelCommunicationListener` constructor.</span></span> <span data-ttu-id="a0e1f-238">Nesse caso, uma porta dinâmica será usada.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-238">In this case, a dynamic port will be used.</span></span> <span data-ttu-id="a0e1f-239">Consulte a próxima seção Olá para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-239">See hello next section for more information.</span></span>

#### <a name="use-kestrel-with-a-dynamic-port"></a><span data-ttu-id="a0e1f-240">Usar Kestrel com uma porta dinâmica</span><span class="sxs-lookup"><span data-stu-id="a0e1f-240">Use Kestrel with a dynamic port</span></span>
<span data-ttu-id="a0e1f-241">Kestrel não é possível usar a atribuição de porta automática de saudação do hello `Endpoint` configuração em ServiceManifest.xml, porque a atribuição automática de porta de um `Endpoint` configuração atribui uma porta exclusiva por *processo de host* , e um processo de host único pode conter várias instâncias de Kestrel.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-241">Kestrel cannot use hello automatic port assignment from hello `Endpoint` configuration in ServiceManifest.xml, because automatic port assignment from an `Endpoint` configuration assigns a unique port per *host process*, and a single host process can contain multiple Kestrel instances.</span></span> <span data-ttu-id="a0e1f-242">Como o Kestrel não dá suporte ao compartilhamento de porta, isso não funciona, pois cada instância do Kestrel deve ser aberta em uma porta exclusiva.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-242">Since Kestrel does not support port sharing, this does not work as each Kestrel instance must be opened on a unique port.</span></span>

<span data-ttu-id="a0e1f-243">atribuição de porta dinâmica toouse com Kestrel, basta omitir Olá `Endpoint` configuração em ServiceManifest.xml totalmente e não passe um toohello de nome de ponto de extremidade `KestrelCommunicationListener` construtor:</span><span class="sxs-lookup"><span data-stu-id="a0e1f-243">toouse dynamic port assignment with Kestrel, simply omit hello `Endpoint` configuration in ServiceManifest.xml entirely, and do not pass an endpoint name toohello `KestrelCommunicationListener` constructor:</span></span>

```csharp
new KestrelCommunicationListener(serviceContext, (url, listener) => ...
```

<span data-ttu-id="a0e1f-244">Nessa configuração, `KestrelCommunicationListener` automaticamente selecionará uma porta não utilizada do intervalo de portas de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-244">In this configuration, `KestrelCommunicationListener` will automatically select an unused port from hello application port range.</span></span>

## <a name="scenarios-and-configurations"></a><span data-ttu-id="a0e1f-245">Cenários e configurações</span><span class="sxs-lookup"><span data-stu-id="a0e1f-245">Scenarios and configurations</span></span>
<span data-ttu-id="a0e1f-246">Esta seção descreve os seguintes cenários de saudação e fornece Olá recomendado combinação de servidor web, configuração de porta, opções de integração do Service Fabric e configurações diversas tooachieve um serviço estejam funcionando adequadamente:</span><span class="sxs-lookup"><span data-stu-id="a0e1f-246">This section describes hello following scenarios and provides hello recommended combination of web server, port configuration, Service Fabric integration options, and miscellaneous settings tooachieve a properly functioning service:</span></span>
 - <span data-ttu-id="a0e1f-247">serviço sem estado do Núcleo do ASP.NET exposto externamente</span><span class="sxs-lookup"><span data-stu-id="a0e1f-247">Externally exposed ASP.NET Core stateless service</span></span>
 - <span data-ttu-id="a0e1f-248">Serviço do Núcleo do ASP.NET sem estado somente para uso interno</span><span class="sxs-lookup"><span data-stu-id="a0e1f-248">Internal-only ASP.NET Core stateless service</span></span>
 - <span data-ttu-id="a0e1f-249">serviço com estado do Núcleo do ASP.NET somente interno</span><span class="sxs-lookup"><span data-stu-id="a0e1f-249">Internal-only ASP.NET Core stateful service</span></span>

<span data-ttu-id="a0e1f-250">Um **exposta externamente** serviço é aquele que expõe um ponto de extremidade pode ser acessado de fora de cluster hello, normalmente por meio de um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-250">An **externally exposed** service is one that exposes an endpoint reachable from outside hello cluster, usually through a load balancer.</span></span>

<span data-ttu-id="a0e1f-251">Um **somente interno** o serviço é uma cujo ponto de extremidade só é acessível a partir do cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-251">An **internal-only** service is one whose endpoint is only reachable from within hello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="a0e1f-252">Serviço com monitoração de estado de pontos de extremidade geralmente não devem ser expostos toohello da Internet.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-252">Stateful service endpoints generally should not be exposed toohello Internet.</span></span> <span data-ttu-id="a0e1f-253">Clusters que estão por trás de balanceadores de carga que não têm reconhecimento de resolução de serviço de malha do serviço, como Olá balanceador de carga do Azure, poderá ser services com monitoração de estado tooexpose não é possível porque o balanceador de carga de saudação não ser capaz de toolocate e rotear o tráfego toohello réplica de serviço com monitoração de estado apropriado.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-253">Clusters that are behind load balancers that are unaware of Service Fabric service resolution, such as hello Azure Load Balancer, will be unable tooexpose stateful services because hello load balancer will not be able toolocate and route traffic toohello appropriate stateful service replica.</span></span> 

### <a name="externally-exposed-aspnet-core-stateless-services"></a><span data-ttu-id="a0e1f-254">Serviços sem monitoração de estado do Núcleo do ASP.NET expostos externamente</span><span class="sxs-lookup"><span data-stu-id="a0e1f-254">Externally exposed ASP.NET Core stateless services</span></span>
<span data-ttu-id="a0e1f-255">WebListener é hello recomendado de servidor web para serviços de front-end que expõem externos, voltados para Internet pontos de extremidade HTTP no Windows.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-255">WebListener is hello recommended web server for front-end services that expose external, Internet-facing HTTP endpoints on Windows.</span></span> <span data-ttu-id="a0e1f-256">Ele oferece melhor proteção contra ataques e suporte a recursos para os quais o Kestrel não tem suporte, como a Autenticação do Windows e o compartilhamento de portas.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-256">It provides better protection against attacks and supports features that Kestrel does not, such as Windows Authentication and port sharing.</span></span> 

<span data-ttu-id="a0e1f-257">Não há suporte para o Kestrel como um servidor de borda (para a Internet) no momento.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-257">Kestrel is not supported as an edge (Internet-facing) server at this time.</span></span> <span data-ttu-id="a0e1f-258">Deve ser usado um servidor proxy reverso como o IIS ou Nginx Olá de toohandle tráfego da Internet pública.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-258">A reverse proxy server such as IIS or Nginx must be used toohandle traffic from hello public Internet.</span></span>
 
<span data-ttu-id="a0e1f-259">Toohello exposto à Internet, um serviço sem monitoração de estado quando usar um ponto de extremidade estável e bem conhecido que pode ser acessado por meio de um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-259">When exposed toohello Internet, a stateless service should use a well-known and stable endpoint that is reachable through a load balancer.</span></span> <span data-ttu-id="a0e1f-260">Este é o URL Olá fornecerá toousers do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-260">This is hello URL you will provide toousers of your application.</span></span> <span data-ttu-id="a0e1f-261">é recomendável Olá a seguinte configuração:</span><span class="sxs-lookup"><span data-stu-id="a0e1f-261">hello following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="a0e1f-262">**Observações**</span><span class="sxs-lookup"><span data-stu-id="a0e1f-262">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a0e1f-263">Servidor Web</span><span class="sxs-lookup"><span data-stu-id="a0e1f-263">Web server</span></span> | <span data-ttu-id="a0e1f-264">WebListener</span><span class="sxs-lookup"><span data-stu-id="a0e1f-264">WebListener</span></span> | <span data-ttu-id="a0e1f-265">Se o serviço de saudação é apenas tooa exposto rede confiável, intranet, Kestrel pode ser usado.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-265">If hello service is only exposed tooa trusted network, such an intranet, Kestrel may be used.</span></span> <span data-ttu-id="a0e1f-266">Caso contrário, WebListener é a opção Olá preferido.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-266">Otherwise, WebListener is hello preferred option.</span></span> |
| <span data-ttu-id="a0e1f-267">Configuração de portas</span><span class="sxs-lookup"><span data-stu-id="a0e1f-267">Port configuration</span></span> | <span data-ttu-id="a0e1f-268">estático</span><span class="sxs-lookup"><span data-stu-id="a0e1f-268">static</span></span> | <span data-ttu-id="a0e1f-269">Uma porta estática conhecida deve ser configurada no hello `Endpoints` configuração do ServiceManifest.xml, como 80 para HTTP ou 443 para HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-269">A well-known static port should be configured in hello `Endpoints` configuration of ServiceManifest.xml, such as 80 for HTTP or 443 for HTTPS.</span></span> |
| <span data-ttu-id="a0e1f-270">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="a0e1f-270">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="a0e1f-271">Nenhum</span><span class="sxs-lookup"><span data-stu-id="a0e1f-271">None</span></span> | <span data-ttu-id="a0e1f-272">Olá `ServiceFabricIntegrationOptions.None` opção deve ser usada ao configurar o middleware de integração do Service Fabric para que o serviço de saudação não tentará toovalidate solicitações de entrada para um identificador exclusivo.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-272">hello `ServiceFabricIntegrationOptions.None` option should be used when configuring Service Fabric integration middleware so that hello service does not attempt toovalidate incoming requests for a unique identifier.</span></span> <span data-ttu-id="a0e1f-273">Os usuários externos do seu aplicativo não saberá Olá exclusivo informações de identificação usadas pelo middleware de saudação.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-273">External users of your application will not know hello unique identifying information used by hello middleware.</span></span> |
| <span data-ttu-id="a0e1f-274">Contagem de Instâncias</span><span class="sxs-lookup"><span data-stu-id="a0e1f-274">Instance Count</span></span> | <span data-ttu-id="a0e1f-275">-1</span><span class="sxs-lookup"><span data-stu-id="a0e1f-275">-1</span></span> | <span data-ttu-id="a0e1f-276">Em casos típicos de uso, a configuração de contagem de instância Olá deverá ser definida muito "-1" para que uma instância está disponível em todos os nós que recebe o tráfego de um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-276">In typical use cases, hello instance count setting should be set too"-1" so that an instance is available on all nodes that receive traffic from a load balancer.</span></span> |

<span data-ttu-id="a0e1f-277">Se vários serviços expostos externamente compartilharem Olá mesmo conjunto de nós, um caminho de URL exclusivo mas estável deve ser usado.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-277">If multiple externally exposed services share hello same set of nodes, a unique but stable URL path should be used.</span></span> <span data-ttu-id="a0e1f-278">Isso pode ser feito modificando Olá URL fornecida ao configurar IWebHost.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-278">This can be accomplished by modifying hello URL provided when configuring IWebHost.</span></span> <span data-ttu-id="a0e1f-279">Observe que isso se aplica somente a tooWebListener.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-279">Note this applies tooWebListener only.</span></span>

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

### <a name="internal-only-stateless-aspnet-core-service"></a><span data-ttu-id="a0e1f-280">Serviço do Núcleo do ASP.NET sem estado somente para uso interno</span><span class="sxs-lookup"><span data-stu-id="a0e1f-280">Internal-only stateless ASP.NET Core service</span></span>
<span data-ttu-id="a0e1f-281">Serviços sem monitoração de estado que só são chamados de dentro do cluster Olá devem usar URLs exclusivas e portas atribuídas dinamicamente tooensure cooperação entre vários serviços.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-281">Stateless services that are only called from within hello cluster should use unique URLs and dynamically assigned ports tooensure cooperation between multiple services.</span></span> <span data-ttu-id="a0e1f-282">é recomendável Olá a seguinte configuração:</span><span class="sxs-lookup"><span data-stu-id="a0e1f-282">hello following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="a0e1f-283">**Observações**</span><span class="sxs-lookup"><span data-stu-id="a0e1f-283">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a0e1f-284">Servidor Web</span><span class="sxs-lookup"><span data-stu-id="a0e1f-284">Web server</span></span> | <span data-ttu-id="a0e1f-285">Kestrel</span><span class="sxs-lookup"><span data-stu-id="a0e1f-285">Kestrel</span></span> | <span data-ttu-id="a0e1f-286">Embora WebListener pode ser usado para serviços sem monitoração de estado internos, Kestrel é Olá recomendado server tooallow várias tooshare de instâncias de serviço um host.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-286">Although WebListener may be used for internal stateless services, Kestrel is hello recommended server tooallow multiple service instances tooshare a host.</span></span>  |
| <span data-ttu-id="a0e1f-287">Configuração de portas</span><span class="sxs-lookup"><span data-stu-id="a0e1f-287">Port configuration</span></span> | <span data-ttu-id="a0e1f-288">atribuídas dinamicamente</span><span class="sxs-lookup"><span data-stu-id="a0e1f-288">dynamically assigned</span></span> | <span data-ttu-id="a0e1f-289">Várias réplicas de um serviço com estado podem compartilhar um processo de host ou o sistema operacional do host e, assim, precisarão de portas exclusivas.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-289">Multiple replicas of a stateful service may share a host process or host operating system and thus will need unique ports.</span></span> |
| <span data-ttu-id="a0e1f-290">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="a0e1f-290">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="a0e1f-291">UseUniqueServiceUrl</span><span class="sxs-lookup"><span data-stu-id="a0e1f-291">UseUniqueServiceUrl</span></span> | <span data-ttu-id="a0e1f-292">Com a atribuição de porta dinâmica, essa configuração impede o problema de identidade Olá enganado descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-292">With dynamic port assignment, this setting prevents hello mistaken identity issue described earlier.</span></span> |
| <span data-ttu-id="a0e1f-293">InstanceCount</span><span class="sxs-lookup"><span data-stu-id="a0e1f-293">InstanceCount</span></span> | <span data-ttu-id="a0e1f-294">qualquer</span><span class="sxs-lookup"><span data-stu-id="a0e1f-294">any</span></span> | <span data-ttu-id="a0e1f-295">a configuração de contagem de instância Olá pode ser definida como serviço de saudação do tooany valor toooperate necessário.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-295">hello instance count setting can be set tooany value necessary toooperate hello service.</span></span> |

### <a name="internal-only-stateful-aspnet-core-service"></a><span data-ttu-id="a0e1f-296">Somente interno serviço com estado do Núcleo do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="a0e1f-296">Internal-only stateful ASP.NET Core service</span></span>
<span data-ttu-id="a0e1f-297">Serviços com monitoração de estado que só são chamados de dentro do cluster Olá devem usar portas atribuídas dinamicamente tooensure cooperação entre vários serviços.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-297">Stateful services that are only called from within hello cluster should use dynamically assigned ports tooensure cooperation between multiple services.</span></span> <span data-ttu-id="a0e1f-298">é recomendável Olá a seguinte configuração:</span><span class="sxs-lookup"><span data-stu-id="a0e1f-298">hello following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="a0e1f-299">**Observações**</span><span class="sxs-lookup"><span data-stu-id="a0e1f-299">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a0e1f-300">Servidor Web</span><span class="sxs-lookup"><span data-stu-id="a0e1f-300">Web server</span></span> | <span data-ttu-id="a0e1f-301">Kestrel</span><span class="sxs-lookup"><span data-stu-id="a0e1f-301">Kestrel</span></span> | <span data-ttu-id="a0e1f-302">Olá `WebListenerCommunicationListener` não foi projetado para uso por serviços com monitoração de estado em que réplicas compartilham um processo de host.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-302">hello `WebListenerCommunicationListener` is not designed for use by stateful services in which replicas share a host process.</span></span> |
| <span data-ttu-id="a0e1f-303">Configuração de portas</span><span class="sxs-lookup"><span data-stu-id="a0e1f-303">Port configuration</span></span> | <span data-ttu-id="a0e1f-304">atribuídas dinamicamente</span><span class="sxs-lookup"><span data-stu-id="a0e1f-304">dynamically assigned</span></span> | <span data-ttu-id="a0e1f-305">Várias réplicas de um serviço com estado podem compartilhar um processo de host ou o sistema operacional do host e, assim, precisarão de portas exclusivas.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-305">Multiple replicas of a stateful service may share a host process or host operating system and thus will need unique ports.</span></span> |
| <span data-ttu-id="a0e1f-306">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="a0e1f-306">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="a0e1f-307">UseUniqueServiceUrl</span><span class="sxs-lookup"><span data-stu-id="a0e1f-307">UseUniqueServiceUrl</span></span> | <span data-ttu-id="a0e1f-308">Com a atribuição de porta dinâmica, essa configuração impede o problema de identidade Olá enganado descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="a0e1f-308">With dynamic port assignment, this setting prevents hello mistaken identity issue described earlier.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a0e1f-309">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a0e1f-309">Next steps</span></span>
[<span data-ttu-id="a0e1f-310">Depurar seu aplicativo do Service Fabric usando o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a0e1f-310">Debug your Service Fabric application by using Visual Studio</span></span>](service-fabric-debugging-your-application.md)

<!--Image references-->
[0]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-standalone.png
[1]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-servicefabric.png
[2]:./media/service-fabric-reliable-services-communication-aspnetcore/integration.png
[3]:./media/service-fabric-reliable-services-communication-aspnetcore/httpsys.png
[4]:./media/service-fabric-reliable-services-communication-aspnetcore/kestrel.png
