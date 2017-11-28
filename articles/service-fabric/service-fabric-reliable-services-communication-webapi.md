---
title: "Comunicação de serviço com a API Web ASP.NET | Microsoft Docs"
description: "Saiba como implementar passo a passo a comunicação de serviço usando a API Web ASP.NET com auto-hospedagem OWIN na API dos Reliable Services."
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
ms.date: 02/10/2017
ms.author: vturecek
redirect_url: /azure/service-fabric/service-fabric-reliable-services-communication-aspnetcore
ms.openlocfilehash: 73b7e1c0cb93ae7c54780a3aab837b0e5bcdb0a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-service-fabric-web-api-services-with-owin-self-hosting"></a><span data-ttu-id="e238c-103">Introdução aos serviços de API Web do Service Fabric com auto-hospedagem OWIN</span><span class="sxs-lookup"><span data-stu-id="e238c-103">Get started: Service Fabric Web API services with OWIN self-hosting</span></span>
<span data-ttu-id="e238c-104">Com o Service Fabric, você decide como deseja que seus serviços se comuniquem com os usuários e entre si.</span><span class="sxs-lookup"><span data-stu-id="e238c-104">Azure Service Fabric puts the power in your hands when you're deciding how you want your services to communicate with users and with each other.</span></span> <span data-ttu-id="e238c-105">Este tutorial se concentra na implementação da comunicação de serviço usando a API Web ASP.NET com auto-hospedagem OWIN (Open Web Interface for .NET) na API dos Reliable Services do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e238c-105">This tutorial focuses on implementing service communication using ASP.NET Web API with Open Web Interface for .NET (OWIN) self-hosting in Service Fabric's Reliable Services API.</span></span> <span data-ttu-id="e238c-106">Vamos abordar detalhadamente a API de comunicação conectável dos Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="e238c-106">We'll delve deeply into the Reliable Services pluggable communication API.</span></span> <span data-ttu-id="e238c-107">Também usaremos a API Web em um exemplo passo a passo para mostrar a você como configurar um ouvinte de comunicação personalizado.</span><span class="sxs-lookup"><span data-stu-id="e238c-107">We'll also use Web API in a step-by-step example to show you how to set up a custom communication listener.</span></span>

## <a name="introduction-to-web-api-in-service-fabric"></a><span data-ttu-id="e238c-108">Introdução à API Web no Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e238c-108">Introduction to Web API in Service Fabric</span></span>
<span data-ttu-id="e238c-109">O API Web ASP.NET é uma estrutura popular e poderosa para criar APIs HTTP sobre o .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="e238c-109">ASP.NET Web API is a popular and powerful framework for building HTTP APIs on top of the .NET Framework.</span></span> <span data-ttu-id="e238c-110">Se você não ainda estiver familiarizado com a estrutura, confira [Getting started with ASP.NET Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="e238c-110">If you're not already familiar with the framework, see [Getting started with ASP.NET Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) to learn more.</span></span>

<span data-ttu-id="e238c-111">A API Web na Malha de Serviço é o mesma API Web ASP.NET que você conhece e adora.</span><span class="sxs-lookup"><span data-stu-id="e238c-111">Web API in Service Fabric is the same ASP.NET Web API you know and love.</span></span> <span data-ttu-id="e238c-112">A diferença está em como você *hospeda* um aplicativo de API Web.</span><span class="sxs-lookup"><span data-stu-id="e238c-112">The difference is in how you *host* a Web API application.</span></span> <span data-ttu-id="e238c-113">Você não usará o IIS (Serviços de Informações da Internet) da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e238c-113">You won't be using Microsoft Internet Information Services (IIS).</span></span> <span data-ttu-id="e238c-114">Para compreender melhor a diferença, vamos dividir isso em duas partes:</span><span class="sxs-lookup"><span data-stu-id="e238c-114">To better understand the difference, let's break it into two parts:</span></span>

1. <span data-ttu-id="e238c-115">O aplicativo de API Web (incluindo controladores e modelos)</span><span class="sxs-lookup"><span data-stu-id="e238c-115">The Web API application (including controllers and models)</span></span>
2. <span data-ttu-id="e238c-116">O host (o servidor web, geralmente IIS)</span><span class="sxs-lookup"><span data-stu-id="e238c-116">The host (the web server, usually IIS)</span></span>

<span data-ttu-id="e238c-117">O aplicativo de API Web, em si, não muda.</span><span class="sxs-lookup"><span data-stu-id="e238c-117">A Web API application itself doesn't change.</span></span> <span data-ttu-id="e238c-118">Ele não é diferente dos aplicativos de API Web que você possa ter desenvolvido no passado, e você poderá simplesmente mover a maioria dos códigos do aplicativo diretamente.</span><span class="sxs-lookup"><span data-stu-id="e238c-118">It's no different from Web API applications you may have written in the past, and you should be able to simply move over most of your application code.</span></span> <span data-ttu-id="e238c-119">Mas, se você usava a hospedagem no IIS, onde você hospedará o aplicativo pode ser um pouco diferente do que você estava acostumado.</span><span class="sxs-lookup"><span data-stu-id="e238c-119">But if you've been hosting on IIS, where you host the application may be a little different from what you're used to.</span></span> <span data-ttu-id="e238c-120">Antes de adentrarmos na parte de hospedagem, vamos começar com algo mais familiar: o aplicativo de API Web.</span><span class="sxs-lookup"><span data-stu-id="e238c-120">Before we get to the hosting part, let's start with something more familiar: the Web API application.</span></span>

## <a name="create-the-application"></a><span data-ttu-id="e238c-121">Criar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="e238c-121">Create the application</span></span>
<span data-ttu-id="e238c-122">Comece criando um novo aplicativo do Service Fabric com um único serviço sem estado no Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="e238c-122">Start by creating a new Service Fabric application with a single stateless service in Visual Studio 2015.</span></span>

<span data-ttu-id="e238c-123">Existe um modelo do Visual Studio para um serviço sem estado usando a API Web à sua disposição.</span><span class="sxs-lookup"><span data-stu-id="e238c-123">A Visual Studio template for a stateless service using Web API is available to you.</span></span> <span data-ttu-id="e238c-124">Neste tutorial, vamos criar um projeto de API da Web do zero que resulta no que você obteria se você selecionasse esse modelo.</span><span class="sxs-lookup"><span data-stu-id="e238c-124">In this tutorial, we'll build a Web API project from scratch that results in what you'd get if you selected this template.</span></span>

<span data-ttu-id="e238c-125">Selecione um projeto de serviço sem estado em branco para aprender a criar um projeto de API Web do zero. Você também pode começar com o modelo de API Web do serviço sem estado e simplesmente acompanhá-lo.</span><span class="sxs-lookup"><span data-stu-id="e238c-125">Select a blank Stateless Service project to learn how to build a Web API project from scratch, or you can start with the stateless service Web API template and simply follow along.</span></span>  

<span data-ttu-id="e238c-126">A primeira etapa é obter alguns pacotes NuGet para o API Web.</span><span class="sxs-lookup"><span data-stu-id="e238c-126">The first step is to pull in some NuGet packages for Web API.</span></span> <span data-ttu-id="e238c-127">O pacote que queremos usar é o Microsoft.AspNet.WebApi.OwinSelfHost.</span><span class="sxs-lookup"><span data-stu-id="e238c-127">The package we want to use is Microsoft.AspNet.WebApi.OwinSelfHost.</span></span> <span data-ttu-id="e238c-128">Esse pacote inclui todos os pacotes de API Web necessários e os pacotes de *hospedagem* .</span><span class="sxs-lookup"><span data-stu-id="e238c-128">This package includes all the necessary Web API packages and the *host* packages.</span></span> <span data-ttu-id="e238c-129">Isso será importante mais tarde.</span><span class="sxs-lookup"><span data-stu-id="e238c-129">This will be important later.</span></span>

<span data-ttu-id="e238c-130">Depois que os pacotes tiverem sido instalados, você poderá começar a criar a estrutura do projeto básico de API Web.</span><span class="sxs-lookup"><span data-stu-id="e238c-130">After the packages have been installed, you can begin building out the basic Web API project structure.</span></span> <span data-ttu-id="e238c-131">Se você usou o API Web, a estrutura do projeto deve ser bastante familiar.</span><span class="sxs-lookup"><span data-stu-id="e238c-131">If you've used Web API, the project structure should look very familiar.</span></span> <span data-ttu-id="e238c-132">Comece adicionando um diretório `Controllers` e um controlador de valores simples:</span><span class="sxs-lookup"><span data-stu-id="e238c-132">Start by adding a `Controllers` directory and a simple values controller:</span></span>

<span data-ttu-id="e238c-133">**ValuesController.cs**</span><span class="sxs-lookup"><span data-stu-id="e238c-133">**ValuesController.cs**</span></span>

```csharp
using System.Collections.Generic;
using System.Web.Http;

namespace WebService.Controllers
{
    public class ValuesController : ApiController
    {
        // GET api/values 
        public IEnumerable<string> Get()
        {
            return new string[] { "value1", "value2" };
        }

        // GET api/values/5 
        public string Get(int id)
        {
            return "value";
        }

        // POST api/values 
        public void Post([FromBody]string value)
        {
        }

        // PUT api/values/5 
        public void Put(int id, [FromBody]string value)
        {
        }

        // DELETE api/values/5 
        public void Delete(int id)
        {
        }
    }
}

```

<span data-ttu-id="e238c-134">Em seguida, adicione uma classe de Inicialização à raiz do projeto para registrar o roteamento, formatadores e qualquer outra configuração.</span><span class="sxs-lookup"><span data-stu-id="e238c-134">Next, add a Startup class at the project root to register the routing, formatters, and any other configuration setup.</span></span> <span data-ttu-id="e238c-135">Este também é o local onde o API Web se conecta ao *host*, que será revisto novamente mais tarde.</span><span class="sxs-lookup"><span data-stu-id="e238c-135">This is also where Web API plugs in to the *host*, which will be revisited again later.</span></span> 

<span data-ttu-id="e238c-136">**Startup.cs**</span><span class="sxs-lookup"><span data-stu-id="e238c-136">**Startup.cs**</span></span>

```csharp
using System.Web.Http;
using Owin;

namespace WebService
{
    public static class Startup
    {
        public static void ConfigureApp(IAppBuilder appBuilder)
        {
            // Configure Web API for self-host. 
            HttpConfiguration config = new HttpConfiguration();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );

            appBuilder.UseWebApi(config);
        }
    }
}
```

<span data-ttu-id="e238c-137">Isso é tudo para a parte do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e238c-137">That's it for the application part.</span></span> <span data-ttu-id="e238c-138">Nesse ponto, configuramos apenas o layout do projeto básico de API Web.</span><span class="sxs-lookup"><span data-stu-id="e238c-138">At this point, we've set up just the basic Web API project layout.</span></span> <span data-ttu-id="e238c-139">Até agora, esse processo não parece muito diferente dos projetos de API Web que você possa ter desenvolvido no passado ou do modelo básico de API Web.</span><span class="sxs-lookup"><span data-stu-id="e238c-139">So far, it shouldn't look much different from Web API projects you may have written in the past or from the basic Web API template.</span></span> <span data-ttu-id="e238c-140">A lógica de negócios vai para os controladores e modelos como de costume.</span><span class="sxs-lookup"><span data-stu-id="e238c-140">Your business logic goes in the controllers and models as usual.</span></span>

<span data-ttu-id="e238c-141">Agora o que fazemos com a hospedagem para que possamos executá-la de fato?</span><span class="sxs-lookup"><span data-stu-id="e238c-141">Now what do we do about hosting so that we can actually run it?</span></span>

## <a name="service-hosting"></a><span data-ttu-id="e238c-142">Hospedagem do serviço</span><span class="sxs-lookup"><span data-stu-id="e238c-142">Service hosting</span></span>
<span data-ttu-id="e238c-143">No Service Fabric, seu serviço é executado em um *processo de host do serviço*, um arquivo executável que executa o código do serviço.</span><span class="sxs-lookup"><span data-stu-id="e238c-143">In Service Fabric, your service runs in a *service host process*, an executable file that runs your service code.</span></span> <span data-ttu-id="e238c-144">Quando você escreve um serviço usando a API dos Reliable Services, seu projeto de serviço é compilado em um arquivo executável que registra o tipo de serviço e executa o código.</span><span class="sxs-lookup"><span data-stu-id="e238c-144">When you write a service by using the Reliable Services API, your service project just compiles to an executable file that registers your service type and runs your code.</span></span> <span data-ttu-id="e238c-145">Isso se aplica à maioria dos casos em que você escreve um serviço no Service Fabric no .NET.</span><span class="sxs-lookup"><span data-stu-id="e238c-145">This is true in most cases when you write a service on Service Fabric in .NET.</span></span> <span data-ttu-id="e238c-146">Ao abrir o Program.cs no projeto de serviço sem estado, você deverá ver:</span><span class="sxs-lookup"><span data-stu-id="e238c-146">When you open Program.cs in the stateless service project, you should see:</span></span>

```csharp
using System;
using System.Diagnostics;
using System.Threading;
using Microsoft.ServiceFabric.Services.Runtime;

internal static class Program
{
    private static void Main()
    {
        try
        {
            ServiceRuntime.RegisterServiceAsync("WebServiceType",
                context => new WebService(context)).GetAwaiter().GetResult();

            ServiceEventSource.Current.ServiceTypeRegistered(Process.GetCurrentProcess().Id, typeof(WebService).Name);

            // Prevents this host process from terminating so services keeps running. 
            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ServiceEventSource.Current.ServiceHostInitializationFailed(e.ToString());
            throw;
        }
    }
}

```

<span data-ttu-id="e238c-147">Se parecer anormalmente o ponto de entrada para um aplicativo de console, é porque é.</span><span class="sxs-lookup"><span data-stu-id="e238c-147">If that looks suspiciously like the entry point to a console application, that's because it is.</span></span>

<span data-ttu-id="e238c-148">Neste artigo, não entraremos em mais detalhes sobre o processo de host do serviço e o registro do serviço.</span><span class="sxs-lookup"><span data-stu-id="e238c-148">Further details about the service host process and service registration are beyond the scope of this article.</span></span> <span data-ttu-id="e238c-149">Mas é importante saber, por enquanto, que *o código de serviço está em execução em seu próprio processo*.</span><span class="sxs-lookup"><span data-stu-id="e238c-149">But it's important to know for now that *your service code is running in its own process*.</span></span>

## <a name="self-host-web-api-with-an-owin-host"></a><span data-ttu-id="e238c-150">Auto-hospedar a API Web com um host OWIN</span><span class="sxs-lookup"><span data-stu-id="e238c-150">Self-host Web API with an OWIN host</span></span>
<span data-ttu-id="e238c-151">Uma vez que o código do aplicativo de API Web está hospedado em seu próprio processo, como você o conecta a um servidor Web?</span><span class="sxs-lookup"><span data-stu-id="e238c-151">Given that your Web API application code is hosted in its own process, how do you hook it up to a web server?</span></span> <span data-ttu-id="e238c-152">Digite [OWIN](http://owin.org/).</span><span class="sxs-lookup"><span data-stu-id="e238c-152">Enter [OWIN](http://owin.org/).</span></span> <span data-ttu-id="e238c-153">OWIN é simplesmente um contrato entre aplicativos web do .NET e servidores web.</span><span class="sxs-lookup"><span data-stu-id="e238c-153">OWIN is simply a contract between .NET web applications and web servers.</span></span> <span data-ttu-id="e238c-154">Normalmente, quando o ASP.NET (até o MVC 5) é usado, o aplicativo Web é rigidamente associado ao IIS por meio do System.Web.</span><span class="sxs-lookup"><span data-stu-id="e238c-154">Traditionally when ASP.NET (up to MVC 5) is used, the web application is tightly coupled to IIS through System.Web.</span></span> <span data-ttu-id="e238c-155">No entanto, a API Web implementa o OWIN para que você possa escrever um aplicativo Web que seja dissociado do servidor Web que o hospeda.</span><span class="sxs-lookup"><span data-stu-id="e238c-155">However, Web API implements OWIN, so you can write a web application that is decoupled from the web server that hosts it.</span></span> <span data-ttu-id="e238c-156">Por isso, você pode usar um servidor Web OWIN *auto-hospedado* que pode ser iniciado em seu próprio processo.</span><span class="sxs-lookup"><span data-stu-id="e238c-156">Because of this, you can use a *self-hosted* OWIN web server that you can start in your own process.</span></span> <span data-ttu-id="e238c-157">Isso se ajusta perfeitamente com o modelo de hospedagem do Service Fabric que acabamos de descrever.</span><span class="sxs-lookup"><span data-stu-id="e238c-157">This fits perfectly with the Service Fabric hosting model we just described.</span></span>

<span data-ttu-id="e238c-158">Neste artigo, vamos usar Katana como host OWIN para o aplicativo API Web.</span><span class="sxs-lookup"><span data-stu-id="e238c-158">In this article, we'll use Katana as the OWIN host for the Web API application.</span></span> <span data-ttu-id="e238c-159">Katana é uma implementação de host do OWIN de software livre baseada em [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx) e na [API de Servidor HTTP](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx) do Windows.</span><span class="sxs-lookup"><span data-stu-id="e238c-159">Katana is an open-source OWIN host implementation built on [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx) and the Windows [HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="e238c-160">Para saber mais sobre o Katana, acesse o [site do Katana](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana).</span><span class="sxs-lookup"><span data-stu-id="e238c-160">To learn more about Katana, go to the [Katana site](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana).</span></span> <span data-ttu-id="e238c-161">Para obter uma visão geral rápida de como usar o Katana para a auto-hospedagem da API Web, confira [Use OWIN to Self-Host ASP.NET Web API 2](http://www.asp.net/web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api)(Usar o OWIN para auto-hospedar a API Web ASP.NET).</span><span class="sxs-lookup"><span data-stu-id="e238c-161">For a quick overview of how to use Katana to self-host Web API, see [Use OWIN to Self-Host ASP.NET Web API 2](http://www.asp.net/web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api).</span></span>
> 
> 

## <a name="set-up-the-web-server"></a><span data-ttu-id="e238c-162">Configuração do servidor Web</span><span class="sxs-lookup"><span data-stu-id="e238c-162">Set up the web server</span></span>
<span data-ttu-id="e238c-163">A API dos Reliable Services fornece um ponto de entrada de comunicação no qual você pode conectar pilhas de comunicação que permitem aos usuários e clientes se conectarem ao serviço:</span><span class="sxs-lookup"><span data-stu-id="e238c-163">The Reliable Services API provides a communication entry point where you can plug in communication stacks that allow users and clients to connect to the service:</span></span>

```csharp

protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}

```

<span data-ttu-id="e238c-164">O servidor Web (e qualquer outra pilha de comunicação que você possa usar no futuro, como WebSockets) deve usar a interface ICommunicationListener para se integrar corretamente ao sistema.</span><span class="sxs-lookup"><span data-stu-id="e238c-164">The web server (and any other communication stack you use in the future, such as WebSockets) should use the ICommunicationListener interface to integrate correctly with the system.</span></span> <span data-ttu-id="e238c-165">As razões para isso ficarão mais evidentes nas etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="e238c-165">The reasons for this will become more apparent in the following steps.</span></span>

<span data-ttu-id="e238c-166">Primeiro, crie uma classe chamada OwinCommunicationListener que implementa ICommunicationListener:</span><span class="sxs-lookup"><span data-stu-id="e238c-166">First, create a class called OwinCommunicationListener that implements ICommunicationListener:</span></span>

<span data-ttu-id="e238c-167">**OwinCommunicationListener.cs**</span><span class="sxs-lookup"><span data-stu-id="e238c-167">**OwinCommunicationListener.cs**</span></span>

```csharp
using Microsoft.Owin.Hosting;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Owin;
using System;
using System.Fabric;
using System.Globalization;
using System.Threading;
using System.Threading.Tasks;

namespace WebService
{
    internal class OwinCommunicationListener : ICommunicationListener
    {
        public void Abort()
        {
        }

        public Task CloseAsync(CancellationToken cancellationToken)
        {
        }

        public Task<string> OpenAsync(CancellationToken cancellationToken)
        {
        }
    }
}
```

<span data-ttu-id="e238c-168">A interface ICommunicationListener fornece três métodos para gerenciar um ouvinte de comunicação para seu serviço:</span><span class="sxs-lookup"><span data-stu-id="e238c-168">The ICommunicationListener interface provides three methods to manage a communication listener for your service:</span></span>

* <span data-ttu-id="e238c-169">*OpenAsync*.</span><span class="sxs-lookup"><span data-stu-id="e238c-169">*OpenAsync*.</span></span> <span data-ttu-id="e238c-170">Começar a ouvir solicitações.</span><span class="sxs-lookup"><span data-stu-id="e238c-170">Start listening for requests.</span></span>
* <span data-ttu-id="e238c-171">*CloseAsync*.</span><span class="sxs-lookup"><span data-stu-id="e238c-171">*CloseAsync*.</span></span> <span data-ttu-id="e238c-172">Parar de ouvir solicitações, concluir todas as solicitações em andamento e desligar normalmente.</span><span class="sxs-lookup"><span data-stu-id="e238c-172">Stop listening for requests, finish any in-flight requests, and shut down gracefully.</span></span>
* <span data-ttu-id="e238c-173">*Anular*.</span><span class="sxs-lookup"><span data-stu-id="e238c-173">*Abort*.</span></span> <span data-ttu-id="e238c-174">Cancelar tudo e parar imediatamente.</span><span class="sxs-lookup"><span data-stu-id="e238c-174">Cancel everything and stop immediately.</span></span>

<span data-ttu-id="e238c-175">Para começar, adicione membros de classe privada para coisas de que o ouvinte precisa para funcionar.</span><span class="sxs-lookup"><span data-stu-id="e238c-175">To get started, add private class members for things the listener will need to function.</span></span> <span data-ttu-id="e238c-176">Eles serão inicializados por meio do construtor e usados posteriormente quando você configurar a URL de escuta.</span><span class="sxs-lookup"><span data-stu-id="e238c-176">These will be initialized through the constructor and used later when you set up the listening URL.</span></span>

```csharp
internal class OwinCommunicationListener : ICommunicationListener
{
    private readonly ServiceEventSource eventSource;
    private readonly Action<IAppBuilder> startup;
    private readonly ServiceContext serviceContext;
    private readonly string endpointName;
    private readonly string appRoot;

    private IDisposable webApp;
    private string publishAddress;
    private string listeningAddress;

    public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName)
        : this(startup, serviceContext, eventSource, endpointName, null)
    {
    }

    public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName, string appRoot)
    {
        if (startup == null)
        {
            throw new ArgumentNullException(nameof(startup));
        }

        if (serviceContext == null)
        {
            throw new ArgumentNullException(nameof(serviceContext));
        }

        if (endpointName == null)
        {
            throw new ArgumentNullException(nameof(endpointName));
        }

        if (eventSource == null)
        {
            throw new ArgumentNullException(nameof(eventSource));
        }

        this.startup = startup;
        this.serviceContext = serviceContext;
        this.endpointName = endpointName;
        this.eventSource = eventSource;
        this.appRoot = appRoot;
    }


    ...

```

## <a name="implement-openasync"></a><span data-ttu-id="e238c-177">Implementar o OpenAsync</span><span class="sxs-lookup"><span data-stu-id="e238c-177">Implement OpenAsync</span></span>
<span data-ttu-id="e238c-178">Para configurar o servidor Web, você precisa de duas informações:</span><span class="sxs-lookup"><span data-stu-id="e238c-178">To set up the web server, you need two pieces of information:</span></span>

* <span data-ttu-id="e238c-179">*Um prefixo de caminho de URL*.</span><span class="sxs-lookup"><span data-stu-id="e238c-179">*A URL path prefix*.</span></span> <span data-ttu-id="e238c-180">Embora seja opcional, é bom configurar isso agora para que você possa hospedar com segurança vários serviços Web em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e238c-180">Although this is optional, it's good for you to set this up now so that you can safely host multiple web services in your application.</span></span>
* <span data-ttu-id="e238c-181">*Uma porta*.</span><span class="sxs-lookup"><span data-stu-id="e238c-181">*A port*.</span></span>

<span data-ttu-id="e238c-182">Antes de obter uma porta para o servidor Web, é importante compreender que o Service Fabric fornece uma camada de aplicativo que age como um buffer entre seu aplicativo e o sistema operacional subjacente em que ele é executado.</span><span class="sxs-lookup"><span data-stu-id="e238c-182">Before you get a port for the web server, it's important that you understand that Service Fabric provides an application layer that acts as a buffer between your application and the underlying operating system that it runs on.</span></span> <span data-ttu-id="e238c-183">Dessa forma, a Malha de Serviços fornece uma maneira de configurar *pontos de extremidade* para seus serviços.</span><span class="sxs-lookup"><span data-stu-id="e238c-183">As such, Service Fabric provides a way to configure *endpoints* for your services.</span></span> <span data-ttu-id="e238c-184">O Service Fabric garante que os pontos de extremidade estejam disponíveis para o serviço a ser usado.</span><span class="sxs-lookup"><span data-stu-id="e238c-184">Service Fabric ensures that endpoints are available for your service to use.</span></span> <span data-ttu-id="e238c-185">Dessa forma, você não precisa configurá-los no ambiente do sistema operacional subjacente.</span><span class="sxs-lookup"><span data-stu-id="e238c-185">This way, you don't have to configure them yourself in the underlying OS environment.</span></span> <span data-ttu-id="e238c-186">Você pode hospedar facilmente seu aplicativo do Service Fabric em diferentes ambientes sem a necessidade de fazer alterações nele.</span><span class="sxs-lookup"><span data-stu-id="e238c-186">You can easily host your Service Fabric application in different environments without having to make any changes to your application.</span></span> <span data-ttu-id="e238c-187">(Por exemplo, é possível hospedar o mesmo aplicativo no Azure ou em seu próprio datacenter.)</span><span class="sxs-lookup"><span data-stu-id="e238c-187">(For example, you can host the same application in Azure or in your own datacenter.)</span></span>

<span data-ttu-id="e238c-188">Configure um ponto de extremidade de HTTP em PackageRoot\ServiceManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="e238c-188">Configure an HTTP endpoint in PackageRoot\ServiceManifest.xml:</span></span>

```xml
<Resources>
    <Endpoints>
        <Endpoint Name="ServiceEndpoint" Type="Input" Protocol="http" Port="8281" />
    </Endpoints>
</Resources>

```

<span data-ttu-id="e238c-189">Essa etapa é importante porque o processo de host do serviço é executado com credenciais restritas (Serviço de Rede no Windows).</span><span class="sxs-lookup"><span data-stu-id="e238c-189">This step is important because the service host process runs under restricted credentials (Network Service on Windows).</span></span> <span data-ttu-id="e238c-190">Isso significa que o serviço não terá acesso para configurar um ponto de extremidade HTTP por si só.</span><span class="sxs-lookup"><span data-stu-id="e238c-190">This means that your service won't have access to set up an HTTP endpoint on its own.</span></span> <span data-ttu-id="e238c-191">Ao usar a configuração de ponto de extremidade, o Service Fabric sabe como definir a ACL (lista de controle de acesso) apropriada para a URL na qual o serviço escutará.</span><span class="sxs-lookup"><span data-stu-id="e238c-191">By using the endpoint configuration, Service Fabric knows to set up the proper access control list (ACL) for the URL that the service will listen on.</span></span> <span data-ttu-id="e238c-192">O Service Fabric também fornece um local padrão para configurar pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="e238c-192">Service Fabric also provides a standard place to configure endpoints.</span></span>

<span data-ttu-id="e238c-193">Em OwinCommunicationListener.cs, você pode começar a implementar o OpenAsync.</span><span class="sxs-lookup"><span data-stu-id="e238c-193">Back in OwinCommunicationListener.cs, you can start implementing OpenAsync.</span></span> <span data-ttu-id="e238c-194">É onde você inicia o servidor Web.</span><span class="sxs-lookup"><span data-stu-id="e238c-194">This is where you start the web server.</span></span> <span data-ttu-id="e238c-195">Primeiro, obtenha as informações do ponto de extremidade e crie a URL que o serviço escutará.</span><span class="sxs-lookup"><span data-stu-id="e238c-195">First, get the endpoint information and create the URL that the service will listen on.</span></span> <span data-ttu-id="e238c-196">A URL será diferente dependendo do ouvinte ser usado em um serviço sem estado ou com estado.</span><span class="sxs-lookup"><span data-stu-id="e238c-196">The URL will be different depending on whether the listener is used in a stateless service or a stateful service.</span></span> <span data-ttu-id="e238c-197">Para um serviço com estado, o ouvinte deve criar um endereço exclusivo para cada réplica de serviço com estado que ele escuta.</span><span class="sxs-lookup"><span data-stu-id="e238c-197">For a stateful service, the listener needs to create a unique address for every stateful service replica it listens on.</span></span> <span data-ttu-id="e238c-198">Para serviços sem estado, o endereço pode ser muito mais simples.</span><span class="sxs-lookup"><span data-stu-id="e238c-198">For stateless services, the address can be much simpler.</span></span> 

```csharp
public Task<string> OpenAsync(CancellationToken cancellationToken)
{
    var serviceEndpoint = this.serviceContext.CodePackageActivationContext.GetEndpoint(this.endpointName);
    var protocol = serviceEndpoint.Protocol;
    int port = serviceEndpoint.Port;

    if (this.serviceContext is StatefulServiceContext)
    {
        StatefulServiceContext statefulServiceContext = this.serviceContext as StatefulServiceContext;

        this.listeningAddress = string.Format(
            CultureInfo.InvariantCulture,
            "{0}://+:{1}/{2}{3}/{4}/{5}",
            protocol,
            port,
            string.IsNullOrWhiteSpace(this.appRoot)
                ? string.Empty
                : this.appRoot.TrimEnd('/') + '/',
            statefulServiceContext.PartitionId,
            statefulServiceContext.ReplicaId,
            Guid.NewGuid());
    }
    else if (this.serviceContext is StatelessServiceContext)
    {
        this.listeningAddress = string.Format(
            CultureInfo.InvariantCulture,
            "{0}://+:{1}/{2}",
            protocol,
            port,
            string.IsNullOrWhiteSpace(this.appRoot)
                ? string.Empty
                : this.appRoot.TrimEnd('/') + '/');
    }
    else
    {
        throw new InvalidOperationException();
    }

    ...

```

<span data-ttu-id="e238c-199">Observe que "http://+" é usado aqui.</span><span class="sxs-lookup"><span data-stu-id="e238c-199">Note that "http://+" is used here.</span></span> <span data-ttu-id="e238c-200">Isso é para garantir que o servidor Web esteja escutando em todos os endereços disponíveis, incluindo localhost, FQDN e o IP da máquina.</span><span class="sxs-lookup"><span data-stu-id="e238c-200">This is to make sure that the web server is listening on all available addresses, including localhost, FQDN, and the machine IP.</span></span>

<span data-ttu-id="e238c-201">A implementação do OpenAsync é um dos motivos mais importantes pelos quais o servidor Web (ou qualquer pilha de comunicação) é implementado como um ICommunicationListener, em vez de apenas tê-lo aberto diretamente do `RunAsync()` no serviço.</span><span class="sxs-lookup"><span data-stu-id="e238c-201">The OpenAsync implementation is one of the most important reasons why the web server (or any communication stack) is implemented as an ICommunicationListener, rather than just having it open directly from `RunAsync()` in the service.</span></span> <span data-ttu-id="e238c-202">O valor de retorno de OpenAsync é o endereço que o servidor Web está escutando.</span><span class="sxs-lookup"><span data-stu-id="e238c-202">The return value from OpenAsync is the address that the web server is listening on.</span></span> <span data-ttu-id="e238c-203">Quando esse endereço é retornado ao sistema, ele registra o endereço com o serviço.</span><span class="sxs-lookup"><span data-stu-id="e238c-203">When this address is returned to the system, it registers the address with the service.</span></span> <span data-ttu-id="e238c-204">O Service Fabric fornece uma API que permite a clientes e outros serviços pedir esse endereço pelo nome do serviço.</span><span class="sxs-lookup"><span data-stu-id="e238c-204">Service Fabric provides an API that allows clients and other services to then ask for this address by service name.</span></span> <span data-ttu-id="e238c-205">Isso é importante porque o endereço do serviço não é estático.</span><span class="sxs-lookup"><span data-stu-id="e238c-205">This is important because the service address is not static.</span></span> <span data-ttu-id="e238c-206">Os serviços são movimentados no cluster para fins de disponibilidade e balanceamento de recursos.</span><span class="sxs-lookup"><span data-stu-id="e238c-206">Services are moved around in the cluster for resource balancing and availability purposes.</span></span> <span data-ttu-id="e238c-207">Esse é o mecanismo que permite aos clientes resolver o endereço de escuta de um serviço.</span><span class="sxs-lookup"><span data-stu-id="e238c-207">This is the mechanism that allows clients to resolve the listening address for a service.</span></span>

<span data-ttu-id="e238c-208">Com isso em mente, o OpenAsync inicia o servidor Web e retorna o endereço em que está escutando.</span><span class="sxs-lookup"><span data-stu-id="e238c-208">With that in mind, OpenAsync starts the web server and returns the address that it's listening on.</span></span> <span data-ttu-id="e238c-209">Observe que ele escuta em "http://+", mas antes de o OpenAsync retornar o endereço, o "+" é substituído pelo IP ou FQDN do nó em que ele está no momento.</span><span class="sxs-lookup"><span data-stu-id="e238c-209">Note that it listens on "http://+", but before OpenAsync returns the address, the "+" is replaced with the IP or FQDN of the node it is currently on.</span></span> <span data-ttu-id="e238c-210">O endereço retornado por esse método é o que está registrado no sistema.</span><span class="sxs-lookup"><span data-stu-id="e238c-210">The address that is returned by this method is what's registered with the system.</span></span> <span data-ttu-id="e238c-211">Também é o que os clientes e outros serviços veem quando eles solicitam um endereço do serviço.</span><span class="sxs-lookup"><span data-stu-id="e238c-211">It's also what clients and other services see when they ask for a service's address.</span></span> <span data-ttu-id="e238c-212">Para que os clientes se conectem corretamente a ele, eles precisam de um IP ou FQDN real no endereço.</span><span class="sxs-lookup"><span data-stu-id="e238c-212">For clients to correctly connect to it, they need an actual IP or FQDN in the address.</span></span>

```csharp
    ...

    this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

    try
    {
        this.eventSource.Message("Starting web server on " + this.listeningAddress);

        this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

        this.eventSource.Message("Listening on " + this.publishAddress);

        return Task.FromResult(this.publishAddress);
    }
    catch (Exception ex)
    {
        this.eventSource.Message("Web server failed to open endpoint {0}. {1}", this.endpointName, ex.ToString());

        this.StopWebServer();

        throw;
    }
}

```

<span data-ttu-id="e238c-213">Observe que isso faz referência à classe Startup que foi passada para OwinCommunicationListener no construtor.</span><span class="sxs-lookup"><span data-stu-id="e238c-213">Note that this references the Startup class that was passed in to the OwinCommunicationListener in the constructor.</span></span> <span data-ttu-id="e238c-214">Essa instância de inicialização é usada pelo servidor Web para inicializar o aplicativo de API Web.</span><span class="sxs-lookup"><span data-stu-id="e238c-214">This startup instance is used by the web server to bootstrap the Web API application.</span></span>

<span data-ttu-id="e238c-215">A linha `ServiceEventSource.Current.Message()` aparecerá na janela de Eventos de Diagnóstico mais tarde, quando você executar o aplicativo para confirmar que o servidor Web foi iniciado com êxito.</span><span class="sxs-lookup"><span data-stu-id="e238c-215">The `ServiceEventSource.Current.Message()` line will appear in the Diagnostic Events window later, when you run the application to confirm that the web server has started successfully.</span></span>

## <a name="implement-closeasync-and-abort"></a><span data-ttu-id="e238c-216">Implementar CloseAsync e Abort</span><span class="sxs-lookup"><span data-stu-id="e238c-216">Implement CloseAsync and Abort</span></span>
<span data-ttu-id="e238c-217">Finalmente, implemente o CloseAsync e o Abort para interromper o servidor Web.</span><span class="sxs-lookup"><span data-stu-id="e238c-217">Finally, implement both CloseAsync and Abort to stop the web server.</span></span> <span data-ttu-id="e238c-218">O servidor Web pode ser interrompido eliminando-se o indicador de servidor que foi criado durante o OpenAsync.</span><span class="sxs-lookup"><span data-stu-id="e238c-218">The web server can be stopped by disposing the server handle that was created during OpenAsync.</span></span>

```csharp
public Task CloseAsync(CancellationToken cancellationToken)
{
    this.eventSource.Message("Closing web server on endpoint {0}", this.endpointName);

    this.StopWebServer();

    return Task.FromResult(true);
}

public void Abort()
{
    this.eventSource.Message("Aborting web server on endpoint {0}", this.endpointName);

    this.StopWebServer();
}

private void StopWebServer()
{
    if (this.webApp != null)
    {
        try
        {
            this.webApp.Dispose();
        }
        catch (ObjectDisposedException)
        {
            // no-op
        }
    }
}
```

<span data-ttu-id="e238c-219">Nesse exemplo de implementação, CloseAsync e Abort simplesmente interrompem o servidor Web.</span><span class="sxs-lookup"><span data-stu-id="e238c-219">In this implementation example, both CloseAsync and Abort simply stop the web server.</span></span> <span data-ttu-id="e238c-220">Você pode optar por executar um desligamento mais coordenado do servidor Web no CloseAsync.</span><span class="sxs-lookup"><span data-stu-id="e238c-220">You may opt to perform a more gracefully coordinated shutdown of the web server in CloseAsync.</span></span> <span data-ttu-id="e238c-221">Por exemplo, o desligamento pode aguardar que as solicitações em andamento sejam concluídas antes de retornar.</span><span class="sxs-lookup"><span data-stu-id="e238c-221">For example, the shutdown could wait for in-flight requests to be completed before the return.</span></span>

## <a name="start-the-web-server"></a><span data-ttu-id="e238c-222">Inicie o servidor Web.</span><span class="sxs-lookup"><span data-stu-id="e238c-222">Start the web server</span></span>
<span data-ttu-id="e238c-223">Agora você está pronto para criar e retornar uma instância de OwinCommunicationListener para iniciar o servidor web.</span><span class="sxs-lookup"><span data-stu-id="e238c-223">You're now ready to create and return an instance of OwinCommunicationListener to start the web server.</span></span> <span data-ttu-id="e238c-224">De volta à classe de serviço (WebService.cs), substitua o método `CreateServiceInstanceListeners()`:</span><span class="sxs-lookup"><span data-stu-id="e238c-224">Back in the Service class (WebService.cs), override the `CreateServiceInstanceListeners()` method:</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    var endpoints = Context.CodePackageActivationContext.GetEndpoints()
                           .Where(endpoint => endpoint.Protocol == EndpointProtocol.Http || endpoint.Protocol == EndpointProtocol.Https)
                           .Select(endpoint => endpoint.Name);

    return endpoints.Select(endpoint => new ServiceInstanceListener(
        serviceContext => new OwinCommunicationListener(Startup.ConfigureApp, serviceContext, ServiceEventSource.Current, endpoint), endpoint));
}
```

<span data-ttu-id="e238c-225">É nesse ponto que o *aplicativo* de API Web e o *host* OWIN finalmente se encontram.</span><span class="sxs-lookup"><span data-stu-id="e238c-225">This is where the Web API *application* and the OWIN *host* finally meet.</span></span> <span data-ttu-id="e238c-226">O host (OwinCommunicationListener) recebe uma instância do *aplicativo* (API Web) por meio da classe de Inicialização.</span><span class="sxs-lookup"><span data-stu-id="e238c-226">The host (OwinCommunicationListener) is given an instance of the *application* (Web API) via the Startup class.</span></span> <span data-ttu-id="e238c-227">O Service Fabric gerencia seu ciclo de vida.</span><span class="sxs-lookup"><span data-stu-id="e238c-227">Service Fabric then manages its lifecycle.</span></span> <span data-ttu-id="e238c-228">Esse mesmo padrão normalmente pode ser seguido com qualquer pilha de comunicação.</span><span class="sxs-lookup"><span data-stu-id="e238c-228">This same pattern can typically be followed with any communication stack.</span></span>

## <a name="put-it-all-together"></a><span data-ttu-id="e238c-229">Colocar tudo isso junto</span><span class="sxs-lookup"><span data-stu-id="e238c-229">Put it all together</span></span>
<span data-ttu-id="e238c-230">Neste exemplo, você não precisa fazer nada no método `RunAsync()` , de forma que a substituição pode ser simplesmente removida.</span><span class="sxs-lookup"><span data-stu-id="e238c-230">In this example, you don't need to do anything in the `RunAsync()` method, so that override can simply be removed.</span></span>

<span data-ttu-id="e238c-231">A implementação do serviço final deve ser muito simples.</span><span class="sxs-lookup"><span data-stu-id="e238c-231">The final service implementation should be very simple.</span></span> <span data-ttu-id="e238c-232">Ele só precisa criar o ouvinte de comunicação:</span><span class="sxs-lookup"><span data-stu-id="e238c-232">It only needs to create the communication listener:</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Fabric;
using System.Fabric.Description;
using System.Linq;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

namespace WebService
{
    internal sealed class WebService : StatelessService
    {
        public WebService(StatelessServiceContext context)
            : base(context)
        { }

        protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
        {
            var endpoints = Context.CodePackageActivationContext.GetEndpoints()
                                   .Where(endpoint => endpoint.Protocol == EndpointProtocol.Http || endpoint.Protocol == EndpointProtocol.Https)
                                   .Select(endpoint => endpoint.Name);

            return endpoints.Select(endpoint => new ServiceInstanceListener(
                serviceContext => new OwinCommunicationListener(Startup.ConfigureApp, serviceContext, ServiceEventSource.Current, endpoint), endpoint));
        }
    }
}
```

<span data-ttu-id="e238c-233">A classe `OwinCommunicationListener` completa:</span><span class="sxs-lookup"><span data-stu-id="e238c-233">The complete `OwinCommunicationListener` class:</span></span>

```csharp
using System;
using System.Diagnostics;
using System.Fabric;
using System.Globalization;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.Owin.Hosting;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Owin;

namespace WebService
{
    internal class OwinCommunicationListener : ICommunicationListener
    {
        private readonly ServiceEventSource eventSource;
        private readonly Action<IAppBuilder> startup;
        private readonly ServiceContext serviceContext;
        private readonly string endpointName;
        private readonly string appRoot;

        private IDisposable webApp;
        private string publishAddress;
        private string listeningAddress;

        public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName)
            : this(startup, serviceContext, eventSource, endpointName, null)
        {
        }

        public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName, string appRoot)
        {
            if (startup == null)
            {
                throw new ArgumentNullException(nameof(startup));
            }

            if (serviceContext == null)
            {
                throw new ArgumentNullException(nameof(serviceContext));
            }

            if (endpointName == null)
            {
                throw new ArgumentNullException(nameof(endpointName));
            }

            if (eventSource == null)
            {
                throw new ArgumentNullException(nameof(eventSource));
            }

            this.startup = startup;
            this.serviceContext = serviceContext;
            this.endpointName = endpointName;
            this.eventSource = eventSource;
            this.appRoot = appRoot;
        }

        public Task<string> OpenAsync(CancellationToken cancellationToken)
        {
            var serviceEndpoint = this.serviceContext.CodePackageActivationContext.GetEndpoint(this.endpointName);
            var protocol = serviceEndpoint.Protocol;
            int port = serviceEndpoint.Port;

            if (this.serviceContext is StatefulServiceContext)
            {
                StatefulServiceContext statefulServiceContext = this.serviceContext as StatefulServiceContext;

                this.listeningAddress = string.Format(
                    CultureInfo.InvariantCulture,
                    "{0}://+:{1}/{2}{3}/{4}/{5}",
                    protocol,
                    port,
                    string.IsNullOrWhiteSpace(this.appRoot)
                        ? string.Empty
                        : this.appRoot.TrimEnd('/') + '/',
                    statefulServiceContext.PartitionId,
                    statefulServiceContext.ReplicaId,
                    Guid.NewGuid());
            }
            else if (this.serviceContext is StatelessServiceContext)
            {
                this.listeningAddress = string.Format(
                    CultureInfo.InvariantCulture,
                    "{0}://+:{1}/{2}",
                    protocol,
                    port,
                    string.IsNullOrWhiteSpace(this.appRoot)
                        ? string.Empty
                        : this.appRoot.TrimEnd('/') + '/');
            }
            else
            {
                throw new InvalidOperationException();
            }

            this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

            try
            {
                this.eventSource.Message("Starting web server on " + this.listeningAddress);

                this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

                this.eventSource.Message("Listening on " + this.publishAddress);

                return Task.FromResult(this.publishAddress);
            }
            catch (Exception ex)
            {
                this.eventSource.Message("Web server failed to open endpoint {0}. {1}", this.endpointName, ex.ToString());

                this.StopWebServer();

                throw;
            }
        }

        public Task CloseAsync(CancellationToken cancellationToken)
        {
            this.eventSource.Message("Closing web server on endpoint {0}", this.endpointName);

            this.StopWebServer();

            return Task.FromResult(true);
        }

        public void Abort()
        {
            this.eventSource.Message("Aborting web server on endpoint {0}", this.endpointName);

            this.StopWebServer();
        }

        private void StopWebServer()
        {
            if (this.webApp != null)
            {
                try
                {
                    this.webApp.Dispose();
                }
                catch (ObjectDisposedException)
                {
                    // no-op
                }
            }
        }
    }
}
```

<span data-ttu-id="e238c-234">Agora que você juntou todas as peças, seu projeto deve se parecer com um típico aplicativo de API Web, com pontos de entrada API dos Reliable Services e um host OWIN.</span><span class="sxs-lookup"><span data-stu-id="e238c-234">Now that you have put all the pieces in place, your project should look like a typical Web API application with Reliable Services API entry points and an OWIN host.</span></span>

## <a name="run-and-connect-through-a-web-browser"></a><span data-ttu-id="e238c-235">Execução e conexão por meio de um navegador da Web</span><span class="sxs-lookup"><span data-stu-id="e238c-235">Run and connect through a web browser</span></span>
<span data-ttu-id="e238c-236">[Configure seu ambiente de desenvolvimento](service-fabric-get-started.md), caso ainda não tenha feito isso.</span><span class="sxs-lookup"><span data-stu-id="e238c-236">If you haven't done so, [set up your development environment](service-fabric-get-started.md).</span></span>

<span data-ttu-id="e238c-237">Agora você pode criar e implantar seu serviço.</span><span class="sxs-lookup"><span data-stu-id="e238c-237">You can now build and deploy your service.</span></span> <span data-ttu-id="e238c-238">Pressione **F5** no Visual Studio para compilar e implantar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e238c-238">Press **F5** in Visual Studio to build and deploy the application.</span></span> <span data-ttu-id="e238c-239">Na janela Eventos de Diagnóstico, você deverá ver uma mensagem indicando que o servidor Web foi aberto em http://localhost:8281/.</span><span class="sxs-lookup"><span data-stu-id="e238c-239">In the Diagnostic Events window, you should see a message that indicates that the web server opened on http://localhost:8281/.</span></span>

> [!NOTE]
> <span data-ttu-id="e238c-240">Se a porta já tiver sido aberta por outro processo em seu computador, você poderá ver um erro aqui.</span><span class="sxs-lookup"><span data-stu-id="e238c-240">If the port has already been opened by another process on your machine, you may see an error here.</span></span> <span data-ttu-id="e238c-241">Isso indica que o ouvinte não pôde ser aberto.</span><span class="sxs-lookup"><span data-stu-id="e238c-241">This indicates that the listener couldn't be opened.</span></span> <span data-ttu-id="e238c-242">Se esse for o caso, tente usar outra porta na configuração do ponto de extremidade em ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="e238c-242">If that's the case, try using a different port for the endpoint configuration in ServiceManifest.xml.</span></span>
> 
> 

<span data-ttu-id="e238c-243">Quando o serviço estiver em execução, abra um navegador e navegue para [http://localhost:8281/api/values](http://localhost:8281/api/values) para testá-lo.</span><span class="sxs-lookup"><span data-stu-id="e238c-243">Once the service is running, open a browser and navigate to [http://localhost:8281/api/values](http://localhost:8281/api/values) to test it.</span></span>

## <a name="scale-it-out"></a><span data-ttu-id="e238c-244">Escalar horizontalmente</span><span class="sxs-lookup"><span data-stu-id="e238c-244">Scale it out</span></span>
<span data-ttu-id="e238c-245">Escalar horizontalmente aplicativos Web sem estado, normalmente, significa adicionar mais computadores e fazer um rodízio de aplicativos Web neles.</span><span class="sxs-lookup"><span data-stu-id="e238c-245">Scaling out stateless web apps typically means adding more machines and spinning up the web apps on them.</span></span> <span data-ttu-id="e238c-246">O mecanismo de orquestração da Malha de Serviço pode fazer isso para você sempre que novos nós forem adicionados a um cluster.</span><span class="sxs-lookup"><span data-stu-id="e238c-246">Service Fabric's orchestration engine can do this for you whenever new nodes are added to a cluster.</span></span> <span data-ttu-id="e238c-247">Ao criar instâncias de um serviço sem estado, você pode especificar o número de instâncias que deseja criar.</span><span class="sxs-lookup"><span data-stu-id="e238c-247">When you create instances of a stateless service, you can specify the number of instances you want to create.</span></span> <span data-ttu-id="e238c-248">O Service Fabric coloca esse número de instâncias em nós no cluster.</span><span class="sxs-lookup"><span data-stu-id="e238c-248">Service Fabric places that number of instances on nodes in the cluster.</span></span> <span data-ttu-id="e238c-249">Isso garante que não se crie mais de uma instância em algum nó.</span><span class="sxs-lookup"><span data-stu-id="e238c-249">And it makes sure not to create more than one instance on any one node.</span></span> <span data-ttu-id="e238c-250">Você também pode orientar o Service Fabric a sempre criar uma instância em cada nó, especificando **-1** para a contagem de instâncias.</span><span class="sxs-lookup"><span data-stu-id="e238c-250">You can also instruct Service Fabric to always create an instance on every node by specifying **-1** for the instance count.</span></span> <span data-ttu-id="e238c-251">Isso garante que sempre que você adicionar nós para escalar horizontalmente o cluster, uma instância do seu serviço sem estado será criada em novos nós.</span><span class="sxs-lookup"><span data-stu-id="e238c-251">This guarantees that whenever you add nodes to scale out your cluster, an instance of your stateless service will be created on the new nodes.</span></span> <span data-ttu-id="e238c-252">Esse valor é uma propriedade da instância do serviço, de modo que ele é definido quando você cria uma instância de serviço.</span><span class="sxs-lookup"><span data-stu-id="e238c-252">This value is a property of the service instance, so it is set when you create a service instance.</span></span> <span data-ttu-id="e238c-253">Você pode fazer isso usando o PowerShell:</span><span class="sxs-lookup"><span data-stu-id="e238c-253">You can do this through PowerShell:</span></span>

```powershell

New-ServiceFabricService -ApplicationName "fabric:/WebServiceApplication" -ServiceName "fabric:/WebServiceApplication/WebService" -ServiceTypeName "WebServiceType" -Stateless -PartitionSchemeSingleton -InstanceCount -1

```

<span data-ttu-id="e238c-254">Ou ao definir um serviço padrão em um projeto de serviço sem estado do Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="e238c-254">You can also do this when you define a default service in a Visual Studio stateless service project:</span></span>

```xml

<DefaultServices>
  <Service Name="WebService">
    <StatelessService ServiceTypeName="WebServiceType" InstanceCount="-1">
      <SingletonPartition />
    </StatelessService>
  </Service>
</DefaultServices>

```

<span data-ttu-id="e238c-255">Para obter mais informações sobre como criar aplicativos e instâncias de serviço, confira [Implantar um aplicativo](service-fabric-deploy-remove-applications.md).</span><span class="sxs-lookup"><span data-stu-id="e238c-255">For more information on how to create application and service instances, see [Deploy an application](service-fabric-deploy-remove-applications.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e238c-256">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e238c-256">Next steps</span></span>
[<span data-ttu-id="e238c-257">Depurar seu aplicativo do Service Fabric usando o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e238c-257">Debug your Service Fabric application by using Visual Studio</span></span>](service-fabric-debugging-your-application.md)

