---
title: "comunicação aaaService com hello ASP.NET Web API | Microsoft Docs"
description: "Saiba como comunicação de serviço tooimplement passo a passo usando Olá API da Web ASP.NET com OWIN auto-hospedagem em Olá confiável API de serviços."
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
ms.openlocfilehash: 3fb18fcb141ada0d79a0acda3dccbc7fb044346d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-service-fabric-web-api-services-with-owin-self-hosting"></a><span data-ttu-id="dfe93-103">Introdução aos serviços de API Web do Service Fabric com auto-hospedagem OWIN</span><span class="sxs-lookup"><span data-stu-id="dfe93-103">Get started: Service Fabric Web API services with OWIN self-hosting</span></span>
<span data-ttu-id="dfe93-104">Malha do Azure do serviço coloca power Olá em suas mãos ao decidir como deseja que seu toocommunicate serviços com usuários e entre si.</span><span class="sxs-lookup"><span data-stu-id="dfe93-104">Azure Service Fabric puts hello power in your hands when you're deciding how you want your services toocommunicate with users and with each other.</span></span> <span data-ttu-id="dfe93-105">Este tutorial se concentra na implementação da comunicação de serviço usando a API Web ASP.NET com auto-hospedagem OWIN (Open Web Interface for .NET) na API dos Reliable Services do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="dfe93-105">This tutorial focuses on implementing service communication using ASP.NET Web API with Open Web Interface for .NET (OWIN) self-hosting in Service Fabric's Reliable Services API.</span></span> <span data-ttu-id="dfe93-106">Será examinarmos profundamente Olá comunicação de serviços confiáveis conectável API.</span><span class="sxs-lookup"><span data-stu-id="dfe93-106">We'll delve deeply into hello Reliable Services pluggable communication API.</span></span> <span data-ttu-id="dfe93-107">Também usaremos API da Web em um exemplo passo a passo tooshow você como tooset a um ouvinte de comunicação personalizados.</span><span class="sxs-lookup"><span data-stu-id="dfe93-107">We'll also use Web API in a step-by-step example tooshow you how tooset up a custom communication listener.</span></span>

## <a name="introduction-tooweb-api-in-service-fabric"></a><span data-ttu-id="dfe93-108">Introdução tooWeb API no serviço de malha</span><span class="sxs-lookup"><span data-stu-id="dfe93-108">Introduction tooWeb API in Service Fabric</span></span>
<span data-ttu-id="dfe93-109">API da Web do ASP.NET é uma estrutura popular e avançada para a criação de APIs de HTTP na parte superior de saudação do .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="dfe93-109">ASP.NET Web API is a popular and powerful framework for building HTTP APIs on top of hello .NET Framework.</span></span> <span data-ttu-id="dfe93-110">Se você não ainda estiver familiarizado com o framework hello, consulte [guia de Introdução ao ASP.NET Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) toolearn mais.</span><span class="sxs-lookup"><span data-stu-id="dfe93-110">If you're not already familiar with hello framework, see [Getting started with ASP.NET Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) toolearn more.</span></span>

<span data-ttu-id="dfe93-111">API da Web no serviço de malha é Olá mesmo ASP.NET Web API você conhece e adora.</span><span class="sxs-lookup"><span data-stu-id="dfe93-111">Web API in Service Fabric is hello same ASP.NET Web API you know and love.</span></span> <span data-ttu-id="dfe93-112">Olá diferença é como você *host* um aplicativo de API da Web.</span><span class="sxs-lookup"><span data-stu-id="dfe93-112">hello difference is in how you *host* a Web API application.</span></span> <span data-ttu-id="dfe93-113">Você não usará o IIS (Serviços de Informações da Internet) da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="dfe93-113">You won't be using Microsoft Internet Information Services (IIS).</span></span> <span data-ttu-id="dfe93-114">toobetter entender a diferença Olá, vamos dividi-lo em duas partes:</span><span class="sxs-lookup"><span data-stu-id="dfe93-114">toobetter understand hello difference, let's break it into two parts:</span></span>

1. <span data-ttu-id="dfe93-115">aplicativo de API da Web Hello (incluindo controladores e modelos)</span><span class="sxs-lookup"><span data-stu-id="dfe93-115">hello Web API application (including controllers and models)</span></span>
2. <span data-ttu-id="dfe93-116">host de saudação (servidor web hello, geralmente IIS)</span><span class="sxs-lookup"><span data-stu-id="dfe93-116">hello host (hello web server, usually IIS)</span></span>

<span data-ttu-id="dfe93-117">O aplicativo de API Web, em si, não muda.</span><span class="sxs-lookup"><span data-stu-id="dfe93-117">A Web API application itself doesn't change.</span></span> <span data-ttu-id="dfe93-118">Ele não é diferente de aplicativos de API da Web que você pode ter escrito em Olá anterior, e você deve ser toosimply capaz de mover grande parte do código do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dfe93-118">It's no different from Web API applications you may have written in hello past, and you should be able toosimply move over most of your application code.</span></span> <span data-ttu-id="dfe93-119">Mas se você foi hospedando no IIS, onde você hospedar o aplicativo hello pode ser um pouco diferente do que você está acostumado.</span><span class="sxs-lookup"><span data-stu-id="dfe93-119">But if you've been hosting on IIS, where you host hello application may be a little different from what you're used to.</span></span> <span data-ttu-id="dfe93-120">Antes de entrarmos toohello parte de hospedagem, vamos começar com algo mais familiar: Olá aplicativo de API da Web.</span><span class="sxs-lookup"><span data-stu-id="dfe93-120">Before we get toohello hosting part, let's start with something more familiar: hello Web API application.</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="dfe93-121">Criar um aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="dfe93-121">Create hello application</span></span>
<span data-ttu-id="dfe93-122">Comece criando um novo aplicativo do Service Fabric com um único serviço sem estado no Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="dfe93-122">Start by creating a new Service Fabric application with a single stateless service in Visual Studio 2015.</span></span>

<span data-ttu-id="dfe93-123">Um modelo do Visual Studio para um serviço sem monitoração de estado usando a API da Web é tooyou disponível.</span><span class="sxs-lookup"><span data-stu-id="dfe93-123">A Visual Studio template for a stateless service using Web API is available tooyou.</span></span> <span data-ttu-id="dfe93-124">Neste tutorial, vamos criar um projeto de API da Web do zero que resulta no que você obteria se você selecionasse esse modelo.</span><span class="sxs-lookup"><span data-stu-id="dfe93-124">In this tutorial, we'll build a Web API project from scratch that results in what you'd get if you selected this template.</span></span>

<span data-ttu-id="dfe93-125">Selecione um toolearn de projeto de serviço sem monitoração de estado em branco como toobuild um projeto de API da Web do zero, ou você pode iniciar com o serviço sem monitoração de estado de saudação modelo API da Web e simplesmente acompanhar.</span><span class="sxs-lookup"><span data-stu-id="dfe93-125">Select a blank Stateless Service project toolearn how toobuild a Web API project from scratch, or you can start with hello stateless service Web API template and simply follow along.</span></span>  

<span data-ttu-id="dfe93-126">Olá primeira etapa é toopull em alguns pacotes do NuGet para a API da Web.</span><span class="sxs-lookup"><span data-stu-id="dfe93-126">hello first step is toopull in some NuGet packages for Web API.</span></span> <span data-ttu-id="dfe93-127">pacote de saudação queremos toouse é Microsoft.AspNet.WebApi.OwinSelfHost.</span><span class="sxs-lookup"><span data-stu-id="dfe93-127">hello package we want toouse is Microsoft.AspNet.WebApi.OwinSelfHost.</span></span> <span data-ttu-id="dfe93-128">Este pacote inclui todos os pacotes necessários de API da Web hello e Olá *host* pacotes.</span><span class="sxs-lookup"><span data-stu-id="dfe93-128">This package includes all hello necessary Web API packages and hello *host* packages.</span></span> <span data-ttu-id="dfe93-129">Isso será importante mais tarde.</span><span class="sxs-lookup"><span data-stu-id="dfe93-129">This will be important later.</span></span>

<span data-ttu-id="dfe93-130">Depois que os pacotes de saudação foram instalados, você pode começar a criação de estrutura de projeto de API da Web básica hello.</span><span class="sxs-lookup"><span data-stu-id="dfe93-130">After hello packages have been installed, you can begin building out hello basic Web API project structure.</span></span> <span data-ttu-id="dfe93-131">Se você tiver usado um API da Web, a estrutura do projeto Olá deve ser bastante familiar.</span><span class="sxs-lookup"><span data-stu-id="dfe93-131">If you've used Web API, hello project structure should look very familiar.</span></span> <span data-ttu-id="dfe93-132">Comece adicionando um diretório `Controllers` e um controlador de valores simples:</span><span class="sxs-lookup"><span data-stu-id="dfe93-132">Start by adding a `Controllers` directory and a simple values controller:</span></span>

<span data-ttu-id="dfe93-133">**ValuesController.cs**</span><span class="sxs-lookup"><span data-stu-id="dfe93-133">**ValuesController.cs**</span></span>

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

<span data-ttu-id="dfe93-134">Em seguida, adicione uma classe de inicialização em Olá Olá projeto raiz tooregister roteamento formatadores e qualquer outra configuração.</span><span class="sxs-lookup"><span data-stu-id="dfe93-134">Next, add a Startup class at hello project root tooregister hello routing, formatters, and any other configuration setup.</span></span> <span data-ttu-id="dfe93-135">Isso também é onde o API da Web conecta-se em toohello *host*, que será revisto novamente mais tarde.</span><span class="sxs-lookup"><span data-stu-id="dfe93-135">This is also where Web API plugs in toohello *host*, which will be revisited again later.</span></span> 

<span data-ttu-id="dfe93-136">**Startup.cs**</span><span class="sxs-lookup"><span data-stu-id="dfe93-136">**Startup.cs**</span></span>

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

<span data-ttu-id="dfe93-137">Isso é tudo para parte do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="dfe93-137">That's it for hello application part.</span></span> <span data-ttu-id="dfe93-138">Neste ponto, criamos apenas Olá API da Web projeto layout básico.</span><span class="sxs-lookup"><span data-stu-id="dfe93-138">At this point, we've set up just hello basic Web API project layout.</span></span> <span data-ttu-id="dfe93-139">Até agora, não deve ser muito diferente de projetos Web API que você pode ter escrito em Olá anterior ou de modelo de API da Web básico hello.</span><span class="sxs-lookup"><span data-stu-id="dfe93-139">So far, it shouldn't look much different from Web API projects you may have written in hello past or from hello basic Web API template.</span></span> <span data-ttu-id="dfe93-140">Sua lógica de negócios fica em modelos e controladores hello como de costume.</span><span class="sxs-lookup"><span data-stu-id="dfe93-140">Your business logic goes in hello controllers and models as usual.</span></span>

<span data-ttu-id="dfe93-141">Agora o que fazemos com a hospedagem para que possamos executá-la de fato?</span><span class="sxs-lookup"><span data-stu-id="dfe93-141">Now what do we do about hosting so that we can actually run it?</span></span>

## <a name="service-hosting"></a><span data-ttu-id="dfe93-142">Hospedagem do serviço</span><span class="sxs-lookup"><span data-stu-id="dfe93-142">Service hosting</span></span>
<span data-ttu-id="dfe93-143">No Service Fabric, seu serviço é executado em um *processo de host do serviço*, um arquivo executável que executa o código do serviço.</span><span class="sxs-lookup"><span data-stu-id="dfe93-143">In Service Fabric, your service runs in a *service host process*, an executable file that runs your service code.</span></span> <span data-ttu-id="dfe93-144">Quando você escreve um serviço usando Olá confiável API de serviços, o seu projeto de serviço apenas compila tooan arquivo executável que registra o tipo de serviço e execute seu código.</span><span class="sxs-lookup"><span data-stu-id="dfe93-144">When you write a service by using hello Reliable Services API, your service project just compiles tooan executable file that registers your service type and runs your code.</span></span> <span data-ttu-id="dfe93-145">Isso se aplica à maioria dos casos em que você escreve um serviço no Service Fabric no .NET.</span><span class="sxs-lookup"><span data-stu-id="dfe93-145">This is true in most cases when you write a service on Service Fabric in .NET.</span></span> <span data-ttu-id="dfe93-146">Quando você abrir Program.cs no projeto de serviço sem monitoração de estado hello, você verá:</span><span class="sxs-lookup"><span data-stu-id="dfe93-146">When you open Program.cs in hello stateless service project, you should see:</span></span>

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

<span data-ttu-id="dfe93-147">Se isso se parece anormalmente com o aplicativo de console de tooa de ponto de entrada hello, isso ocorre porque é.</span><span class="sxs-lookup"><span data-stu-id="dfe93-147">If that looks suspiciously like hello entry point tooa console application, that's because it is.</span></span>

<span data-ttu-id="dfe93-148">Mais detalhes sobre o processo de host do serviço de hello e registro de serviço estão além do escopo deste artigo hello.</span><span class="sxs-lookup"><span data-stu-id="dfe93-148">Further details about hello service host process and service registration are beyond hello scope of this article.</span></span> <span data-ttu-id="dfe93-149">Mas é importante tooknow para agora que *seu código de serviço está em execução em seu próprio processo*.</span><span class="sxs-lookup"><span data-stu-id="dfe93-149">But it's important tooknow for now that *your service code is running in its own process*.</span></span>

## <a name="self-host-web-api-with-an-owin-host"></a><span data-ttu-id="dfe93-150">Auto-hospedar a API Web com um host OWIN</span><span class="sxs-lookup"><span data-stu-id="dfe93-150">Self-host Web API with an OWIN host</span></span>
<span data-ttu-id="dfe93-151">Considerando que o código do aplicativo de API da Web é hospedado em seu próprio processo, como associá-lo tooa servidor de web?</span><span class="sxs-lookup"><span data-stu-id="dfe93-151">Given that your Web API application code is hosted in its own process, how do you hook it up tooa web server?</span></span> <span data-ttu-id="dfe93-152">Digite [OWIN](http://owin.org/).</span><span class="sxs-lookup"><span data-stu-id="dfe93-152">Enter [OWIN](http://owin.org/).</span></span> <span data-ttu-id="dfe93-153">OWIN é simplesmente um contrato entre aplicativos web do .NET e servidores web.</span><span class="sxs-lookup"><span data-stu-id="dfe93-153">OWIN is simply a contract between .NET web applications and web servers.</span></span> <span data-ttu-id="dfe93-154">Tradicionalmente quando ASP.NET (backup tooMVC 5) é usado, o aplicativo de web de saudação é firmemente acopladas tooIIS por meio de System. Web.</span><span class="sxs-lookup"><span data-stu-id="dfe93-154">Traditionally when ASP.NET (up tooMVC 5) is used, hello web application is tightly coupled tooIIS through System.Web.</span></span> <span data-ttu-id="dfe93-155">No entanto, a API da Web implementa OWIN, portanto você pode escrever um aplicativo web que é separado do servidor da web hello que o hospeda.</span><span class="sxs-lookup"><span data-stu-id="dfe93-155">However, Web API implements OWIN, so you can write a web application that is decoupled from hello web server that hosts it.</span></span> <span data-ttu-id="dfe93-156">Por isso, você pode usar um servidor Web OWIN *auto-hospedado* que pode ser iniciado em seu próprio processo.</span><span class="sxs-lookup"><span data-stu-id="dfe93-156">Because of this, you can use a *self-hosted* OWIN web server that you can start in your own process.</span></span> <span data-ttu-id="dfe93-157">Isso se ajusta perfeitamente com o modelo de host de malha do serviço do hello que acabamos de descrever.</span><span class="sxs-lookup"><span data-stu-id="dfe93-157">This fits perfectly with hello Service Fabric hosting model we just described.</span></span>

<span data-ttu-id="dfe93-158">Neste artigo, vamos usar Katana como host do OWIN Olá para Olá aplicativo de API da Web.</span><span class="sxs-lookup"><span data-stu-id="dfe93-158">In this article, we'll use Katana as hello OWIN host for hello Web API application.</span></span> <span data-ttu-id="dfe93-159">Katana é uma implementação de host do código-fonte aberto OWIN criada em [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx) e Olá Windows [HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx).</span><span class="sxs-lookup"><span data-stu-id="dfe93-159">Katana is an open-source OWIN host implementation built on [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx) and hello Windows [HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="dfe93-160">toolearn mais sobre Katana, vá toohello [Katana site](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana).</span><span class="sxs-lookup"><span data-stu-id="dfe93-160">toolearn more about Katana, go toohello [Katana site](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana).</span></span> <span data-ttu-id="dfe93-161">Para uma visão geral de como toouse Katana tooself host da Web API, consulte [OWIN de uso tooSelf Host ASP.NET Web API 2](http://www.asp.net/web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api).</span><span class="sxs-lookup"><span data-stu-id="dfe93-161">For a quick overview of how toouse Katana tooself-host Web API, see [Use OWIN tooSelf-Host ASP.NET Web API 2](http://www.asp.net/web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api).</span></span>
> 
> 

## <a name="set-up-hello-web-server"></a><span data-ttu-id="dfe93-162">Configurar o servidor de web Olá</span><span class="sxs-lookup"><span data-stu-id="dfe93-162">Set up hello web server</span></span>
<span data-ttu-id="dfe93-163">Olá confiável API de serviços fornece um ponto de entrada de comunicação em que você pode conectar pilhas de comunicação que permitem que os usuários e o serviço de toohello de tooconnect de clientes:</span><span class="sxs-lookup"><span data-stu-id="dfe93-163">hello Reliable Services API provides a communication entry point where you can plug in communication stacks that allow users and clients tooconnect toohello service:</span></span>

```csharp

protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}

```

<span data-ttu-id="dfe93-164">servidor web de saudação (e qualquer pilha de comunicação que você usar Olá futura, como WebSockets) devem usar Olá ICommunicationListener interface toointegrate corretamente com o sistema de saudação.</span><span class="sxs-lookup"><span data-stu-id="dfe93-164">hello web server (and any other communication stack you use in hello future, such as WebSockets) should use hello ICommunicationListener interface toointegrate correctly with hello system.</span></span> <span data-ttu-id="dfe93-165">motivos Olá se tornará mais aparentes na Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="dfe93-165">hello reasons for this will become more apparent in hello following steps.</span></span>

<span data-ttu-id="dfe93-166">Primeiro, crie uma classe chamada OwinCommunicationListener que implementa ICommunicationListener:</span><span class="sxs-lookup"><span data-stu-id="dfe93-166">First, create a class called OwinCommunicationListener that implements ICommunicationListener:</span></span>

<span data-ttu-id="dfe93-167">**OwinCommunicationListener.cs**</span><span class="sxs-lookup"><span data-stu-id="dfe93-167">**OwinCommunicationListener.cs**</span></span>

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

<span data-ttu-id="dfe93-168">interface de ICommunicationListener Olá fornece três toomanage de métodos um ouvinte de comunicação para seu serviço:</span><span class="sxs-lookup"><span data-stu-id="dfe93-168">hello ICommunicationListener interface provides three methods toomanage a communication listener for your service:</span></span>

* <span data-ttu-id="dfe93-169">*OpenAsync*.</span><span class="sxs-lookup"><span data-stu-id="dfe93-169">*OpenAsync*.</span></span> <span data-ttu-id="dfe93-170">Começar a ouvir solicitações.</span><span class="sxs-lookup"><span data-stu-id="dfe93-170">Start listening for requests.</span></span>
* <span data-ttu-id="dfe93-171">*CloseAsync*.</span><span class="sxs-lookup"><span data-stu-id="dfe93-171">*CloseAsync*.</span></span> <span data-ttu-id="dfe93-172">Parar de ouvir solicitações, concluir todas as solicitações em andamento e desligar normalmente.</span><span class="sxs-lookup"><span data-stu-id="dfe93-172">Stop listening for requests, finish any in-flight requests, and shut down gracefully.</span></span>
* <span data-ttu-id="dfe93-173">*Anular*.</span><span class="sxs-lookup"><span data-stu-id="dfe93-173">*Abort*.</span></span> <span data-ttu-id="dfe93-174">Cancelar tudo e parar imediatamente.</span><span class="sxs-lookup"><span data-stu-id="dfe93-174">Cancel everything and stop immediately.</span></span>

<span data-ttu-id="dfe93-175">tooget iniciado, adicionar membros de classe particular para escuta de saudação coisas, será preciso toofunction.</span><span class="sxs-lookup"><span data-stu-id="dfe93-175">tooget started, add private class members for things hello listener will need toofunction.</span></span> <span data-ttu-id="dfe93-176">Esses serão inicializados pelo construtor hello e usados mais tarde, quando você configura o hello escutando URL.</span><span class="sxs-lookup"><span data-stu-id="dfe93-176">These will be initialized through hello constructor and used later when you set up hello listening URL.</span></span>

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

## <a name="implement-openasync"></a><span data-ttu-id="dfe93-177">Implementar o OpenAsync</span><span class="sxs-lookup"><span data-stu-id="dfe93-177">Implement OpenAsync</span></span>
<span data-ttu-id="dfe93-178">tooset servidor de web hello, você precisa de duas informações:</span><span class="sxs-lookup"><span data-stu-id="dfe93-178">tooset up hello web server, you need two pieces of information:</span></span>

* <span data-ttu-id="dfe93-179">*Um prefixo de caminho de URL*.</span><span class="sxs-lookup"><span data-stu-id="dfe93-179">*A URL path prefix*.</span></span> <span data-ttu-id="dfe93-180">Embora seja opcional, é bom para você tooset esse backup agora para que você com segurança pode hospedar vários serviços web em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dfe93-180">Although this is optional, it's good for you tooset this up now so that you can safely host multiple web services in your application.</span></span>
* <span data-ttu-id="dfe93-181">*Uma porta*.</span><span class="sxs-lookup"><span data-stu-id="dfe93-181">*A port*.</span></span>

<span data-ttu-id="dfe93-182">Antes de obter uma porta para o servidor de web hello, é importante entender que o Service Fabric fornece uma camada de aplicativo que atua como um buffer entre seu aplicativo e o sistema operacional subjacente Olá que ele é executado em.</span><span class="sxs-lookup"><span data-stu-id="dfe93-182">Before you get a port for hello web server, it's important that you understand that Service Fabric provides an application layer that acts as a buffer between your application and hello underlying operating system that it runs on.</span></span> <span data-ttu-id="dfe93-183">Dessa forma, o Service Fabric fornece uma maneira tooconfigure *pontos de extremidade* para seus serviços.</span><span class="sxs-lookup"><span data-stu-id="dfe93-183">As such, Service Fabric provides a way tooconfigure *endpoints* for your services.</span></span> <span data-ttu-id="dfe93-184">Service Fabric garante que os pontos de extremidade estão disponíveis para seu serviço toouse.</span><span class="sxs-lookup"><span data-stu-id="dfe93-184">Service Fabric ensures that endpoints are available for your service toouse.</span></span> <span data-ttu-id="dfe93-185">Dessa forma, você não tem tooconfigure-las por conta própria Olá subjacente do ambiente de sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="dfe93-185">This way, you don't have tooconfigure them yourself in hello underlying OS environment.</span></span> <span data-ttu-id="dfe93-186">Facilmente, você pode hospedar seu aplicativo de serviço de malha em ambientes diferentes sem ter que toomake qualquer aplicativo tooyour de alterações.</span><span class="sxs-lookup"><span data-stu-id="dfe93-186">You can easily host your Service Fabric application in different environments without having toomake any changes tooyour application.</span></span> <span data-ttu-id="dfe93-187">(Por exemplo, você pode hospedar Olá mesmo aplicativo no Azure ou em seu próprio datacenter.)</span><span class="sxs-lookup"><span data-stu-id="dfe93-187">(For example, you can host hello same application in Azure or in your own datacenter.)</span></span>

<span data-ttu-id="dfe93-188">Configure um ponto de extremidade de HTTP em PackageRoot\ServiceManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="dfe93-188">Configure an HTTP endpoint in PackageRoot\ServiceManifest.xml:</span></span>

```xml
<Resources>
    <Endpoints>
        <Endpoint Name="ServiceEndpoint" Type="Input" Protocol="http" Port="8281" />
    </Endpoints>
</Resources>

```

<span data-ttu-id="dfe93-189">Esta etapa é importante porque o processo de host de serviço Olá é executado sob credenciais restritas (serviço de rede no Windows).</span><span class="sxs-lookup"><span data-stu-id="dfe93-189">This step is important because hello service host process runs under restricted credentials (Network Service on Windows).</span></span> <span data-ttu-id="dfe93-190">Isso significa que seu serviço não terá acesso tooset um ponto de extremidade HTTP por conta própria.</span><span class="sxs-lookup"><span data-stu-id="dfe93-190">This means that your service won't have access tooset up an HTTP endpoint on its own.</span></span> <span data-ttu-id="dfe93-191">Usando a configuração de ponto de extremidade Olá, Service Fabric sabe tooset a lista de controle de acesso (ACL) Olá para Olá URL Olá serviço escutará.</span><span class="sxs-lookup"><span data-stu-id="dfe93-191">By using hello endpoint configuration, Service Fabric knows tooset up hello proper access control list (ACL) for hello URL that hello service will listen on.</span></span> <span data-ttu-id="dfe93-192">Serviço de malha também fornece um local padrão tooconfigure pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="dfe93-192">Service Fabric also provides a standard place tooconfigure endpoints.</span></span>

<span data-ttu-id="dfe93-193">Em OwinCommunicationListener.cs, você pode começar a implementar o OpenAsync.</span><span class="sxs-lookup"><span data-stu-id="dfe93-193">Back in OwinCommunicationListener.cs, you can start implementing OpenAsync.</span></span> <span data-ttu-id="dfe93-194">Isso é onde você iniciar o servidor de web hello.</span><span class="sxs-lookup"><span data-stu-id="dfe93-194">This is where you start hello web server.</span></span> <span data-ttu-id="dfe93-195">Primeiro, obter informações de ponto de extremidade hello e criar URL Olá que serviço Olá escutará.</span><span class="sxs-lookup"><span data-stu-id="dfe93-195">First, get hello endpoint information and create hello URL that hello service will listen on.</span></span> <span data-ttu-id="dfe93-196">Olá URL será diferente dependendo se o ouvinte de saudação é usado em um serviço sem monitoração de estado ou de um serviço com monitoração de estado.</span><span class="sxs-lookup"><span data-stu-id="dfe93-196">hello URL will be different depending on whether hello listener is used in a stateless service or a stateful service.</span></span> <span data-ttu-id="dfe93-197">Para um serviço com monitoração de estado, o ouvinte Olá precisa toocreate um único endereço para cada réplica de serviço com monitoração de estado ele escuta em.</span><span class="sxs-lookup"><span data-stu-id="dfe93-197">For a stateful service, hello listener needs toocreate a unique address for every stateful service replica it listens on.</span></span> <span data-ttu-id="dfe93-198">Para serviços sem monitoração de estado, o endereço de saudação pode ser muito mais simples.</span><span class="sxs-lookup"><span data-stu-id="dfe93-198">For stateless services, hello address can be much simpler.</span></span> 

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

<span data-ttu-id="dfe93-199">Observe que "http://+" é usado aqui.</span><span class="sxs-lookup"><span data-stu-id="dfe93-199">Note that "http://+" is used here.</span></span> <span data-ttu-id="dfe93-200">Isso é toomake-se de que o servidor web hello está escutando em todos os endereços disponíveis, incluindo localhost, o FQDN e o IP da máquina de saudação.</span><span class="sxs-lookup"><span data-stu-id="dfe93-200">This is toomake sure that hello web server is listening on all available addresses, including localhost, FQDN, and hello machine IP.</span></span>

<span data-ttu-id="dfe93-201">Olá OpenAsync implementação é um dos motivos mais importantes hello, por que o servidor de web hello (ou qualquer pilha de comunicação) é implementada como um ICommunicationListener, em vez de apenas com ele aberto diretamente do `RunAsync()` no serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="dfe93-201">hello OpenAsync implementation is one of hello most important reasons why hello web server (or any communication stack) is implemented as an ICommunicationListener, rather than just having it open directly from `RunAsync()` in hello service.</span></span> <span data-ttu-id="dfe93-202">valor de retorno de saudação do OpenAsync é endereço Olá Olá servidor web está escutando.</span><span class="sxs-lookup"><span data-stu-id="dfe93-202">hello return value from OpenAsync is hello address that hello web server is listening on.</span></span> <span data-ttu-id="dfe93-203">Quando esse endereço é retornado toohello sistema, ele registra o endereço Olá com serviço Olá.</span><span class="sxs-lookup"><span data-stu-id="dfe93-203">When this address is returned toohello system, it registers hello address with hello service.</span></span> <span data-ttu-id="dfe93-204">Serviço de malha fornece uma API que permite que os clientes e outros serviços toothen peça para este endereço por nome de serviço.</span><span class="sxs-lookup"><span data-stu-id="dfe93-204">Service Fabric provides an API that allows clients and other services toothen ask for this address by service name.</span></span> <span data-ttu-id="dfe93-205">Isso é importante porque o endereço do serviço Olá não é estático.</span><span class="sxs-lookup"><span data-stu-id="dfe93-205">This is important because hello service address is not static.</span></span> <span data-ttu-id="dfe93-206">Os serviços são movidos em torno de cluster Olá para fins de disponibilidade e balanceamento de recursos.</span><span class="sxs-lookup"><span data-stu-id="dfe93-206">Services are moved around in hello cluster for resource balancing and availability purposes.</span></span> <span data-ttu-id="dfe93-207">Esse é o mecanismo de saudação que permite que os clientes tooresolve Olá endereço para um serviço de escuta.</span><span class="sxs-lookup"><span data-stu-id="dfe93-207">This is hello mechanism that allows clients tooresolve hello listening address for a service.</span></span>

<span data-ttu-id="dfe93-208">Com isso em mente, OpenAsync inicia Olá web server e retorna endereço Olá que ele está escutando.</span><span class="sxs-lookup"><span data-stu-id="dfe93-208">With that in mind, OpenAsync starts hello web server and returns hello address that it's listening on.</span></span> <span data-ttu-id="dfe93-209">Observe que escuta "http://+", mas antes de OpenAsync retorna o endereço de hello, Olá "+" é substituído pelo Olá IP ou FQDN do nó hello está em.</span><span class="sxs-lookup"><span data-stu-id="dfe93-209">Note that it listens on "http://+", but before OpenAsync returns hello address, hello "+" is replaced with hello IP or FQDN of hello node it is currently on.</span></span> <span data-ttu-id="dfe93-210">endereço de saudação que é retornado por esse método é o que está registrado no sistema de saudação.</span><span class="sxs-lookup"><span data-stu-id="dfe93-210">hello address that is returned by this method is what's registered with hello system.</span></span> <span data-ttu-id="dfe93-211">Também é o que os clientes e outros serviços veem quando eles solicitam um endereço do serviço.</span><span class="sxs-lookup"><span data-stu-id="dfe93-211">It's also what clients and other services see when they ask for a service's address.</span></span> <span data-ttu-id="dfe93-212">Para clientes toocorrectly conectar tooit, eles precisam de um IP ou o FQDN real no endereço hello.</span><span class="sxs-lookup"><span data-stu-id="dfe93-212">For clients toocorrectly connect tooit, they need an actual IP or FQDN in hello address.</span></span>

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
        this.eventSource.Message("Web server failed tooopen endpoint {0}. {1}", this.endpointName, ex.ToString());

        this.StopWebServer();

        throw;
    }
}

```

<span data-ttu-id="dfe93-213">Observe que isso faz referência a classe de inicialização de saudação que foi passado toohello OwinCommunicationListener no construtor de saudação.</span><span class="sxs-lookup"><span data-stu-id="dfe93-213">Note that this references hello Startup class that was passed in toohello OwinCommunicationListener in hello constructor.</span></span> <span data-ttu-id="dfe93-214">Esta instância de inicialização é usada pelo Olá web server toobootstrap Olá aplicativo de API da Web.</span><span class="sxs-lookup"><span data-stu-id="dfe93-214">This startup instance is used by hello web server toobootstrap hello Web API application.</span></span>

<span data-ttu-id="dfe93-215">Olá `ServiceEventSource.Current.Message()` linha aparecerá na janela de eventos de diagnóstico hello mais tarde, quando você executa Olá aplicativo tooconfirm que o servidor web hello foi iniciado com êxito.</span><span class="sxs-lookup"><span data-stu-id="dfe93-215">hello `ServiceEventSource.Current.Message()` line will appear in hello Diagnostic Events window later, when you run hello application tooconfirm that hello web server has started successfully.</span></span>

## <a name="implement-closeasync-and-abort"></a><span data-ttu-id="dfe93-216">Implementar CloseAsync e Abort</span><span class="sxs-lookup"><span data-stu-id="dfe93-216">Implement CloseAsync and Abort</span></span>
<span data-ttu-id="dfe93-217">Finalmente, implemente CloseAsync e anulação de servidor de web toostop hello.</span><span class="sxs-lookup"><span data-stu-id="dfe93-217">Finally, implement both CloseAsync and Abort toostop hello web server.</span></span> <span data-ttu-id="dfe93-218">servidor de web Hello pode ser interrompida com a eliminação de identificador de servidor de saudação que foi criado durante OpenAsync.</span><span class="sxs-lookup"><span data-stu-id="dfe93-218">hello web server can be stopped by disposing hello server handle that was created during OpenAsync.</span></span>

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

<span data-ttu-id="dfe93-219">Neste exemplo de implementação, CloseAsync e anular simplesmente parar servidor de web de saudação.</span><span class="sxs-lookup"><span data-stu-id="dfe93-219">In this implementation example, both CloseAsync and Abort simply stop hello web server.</span></span> <span data-ttu-id="dfe93-220">Você pode optar por tooperform um desligamento mais normalmente coordenado saudação do servidor de web em CloseAsync.</span><span class="sxs-lookup"><span data-stu-id="dfe93-220">You may opt tooperform a more gracefully coordinated shutdown of hello web server in CloseAsync.</span></span> <span data-ttu-id="dfe93-221">Por exemplo, desligamento Olá podia aguardar toobe de solicitações em andamento, concluído antes de retornar de saudação.</span><span class="sxs-lookup"><span data-stu-id="dfe93-221">For example, hello shutdown could wait for in-flight requests toobe completed before hello return.</span></span>

## <a name="start-hello-web-server"></a><span data-ttu-id="dfe93-222">Iniciar o servidor de web Olá</span><span class="sxs-lookup"><span data-stu-id="dfe93-222">Start hello web server</span></span>
<span data-ttu-id="dfe93-223">Você agora está pronto toocreate e retorna uma instância de servidor de web OwinCommunicationListener toostart hello.</span><span class="sxs-lookup"><span data-stu-id="dfe93-223">You're now ready toocreate and return an instance of OwinCommunicationListener toostart hello web server.</span></span> <span data-ttu-id="dfe93-224">Olá a classe de serviço (WebService.cs), em Substituir Olá `CreateServiceInstanceListeners()` método:</span><span class="sxs-lookup"><span data-stu-id="dfe93-224">Back in hello Service class (WebService.cs), override hello `CreateServiceInstanceListeners()` method:</span></span>

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

<span data-ttu-id="dfe93-225">Isso é onde Olá API da Web *aplicativo* e Olá OWIN *host* finalmente atender.</span><span class="sxs-lookup"><span data-stu-id="dfe93-225">This is where hello Web API *application* and hello OWIN *host* finally meet.</span></span> <span data-ttu-id="dfe93-226">host de saudação (OwinCommunicationListener) é fornecido como uma instância de saudação *aplicativo* (API da Web) por meio de saudação classe de inicialização.</span><span class="sxs-lookup"><span data-stu-id="dfe93-226">hello host (OwinCommunicationListener) is given an instance of hello *application* (Web API) via hello Startup class.</span></span> <span data-ttu-id="dfe93-227">O Service Fabric gerencia seu ciclo de vida.</span><span class="sxs-lookup"><span data-stu-id="dfe93-227">Service Fabric then manages its lifecycle.</span></span> <span data-ttu-id="dfe93-228">Esse mesmo padrão normalmente pode ser seguido com qualquer pilha de comunicação.</span><span class="sxs-lookup"><span data-stu-id="dfe93-228">This same pattern can typically be followed with any communication stack.</span></span>

## <a name="put-it-all-together"></a><span data-ttu-id="dfe93-229">Colocar tudo isso junto</span><span class="sxs-lookup"><span data-stu-id="dfe93-229">Put it all together</span></span>
<span data-ttu-id="dfe93-230">Neste exemplo, você não precisa toodo tudo em Olá `RunAsync()` método, portanto essa substituição simplesmente pode ser removida.</span><span class="sxs-lookup"><span data-stu-id="dfe93-230">In this example, you don't need toodo anything in hello `RunAsync()` method, so that override can simply be removed.</span></span>

<span data-ttu-id="dfe93-231">implementação de serviço final Olá deve ser bem simple.</span><span class="sxs-lookup"><span data-stu-id="dfe93-231">hello final service implementation should be very simple.</span></span> <span data-ttu-id="dfe93-232">Ele só precisa de ouvinte de comunicação Olá toocreate:</span><span class="sxs-lookup"><span data-stu-id="dfe93-232">It only needs toocreate hello communication listener:</span></span>

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

<span data-ttu-id="dfe93-233">Olá completa `OwinCommunicationListener` classe:</span><span class="sxs-lookup"><span data-stu-id="dfe93-233">hello complete `OwinCommunicationListener` class:</span></span>

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
                this.eventSource.Message("Web server failed tooopen endpoint {0}. {1}", this.endpointName, ex.ToString());

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

<span data-ttu-id="dfe93-234">Agora que você colocou todas as partes da saudação em vigor, o projeto deve parecer com um aplicativo de API da Web típico com pontos de entrada da API de serviços confiável e um host OWIN.</span><span class="sxs-lookup"><span data-stu-id="dfe93-234">Now that you have put all hello pieces in place, your project should look like a typical Web API application with Reliable Services API entry points and an OWIN host.</span></span>

## <a name="run-and-connect-through-a-web-browser"></a><span data-ttu-id="dfe93-235">Execução e conexão por meio de um navegador da Web</span><span class="sxs-lookup"><span data-stu-id="dfe93-235">Run and connect through a web browser</span></span>
<span data-ttu-id="dfe93-236">[Configure seu ambiente de desenvolvimento](service-fabric-get-started.md), caso ainda não tenha feito isso.</span><span class="sxs-lookup"><span data-stu-id="dfe93-236">If you haven't done so, [set up your development environment](service-fabric-get-started.md).</span></span>

<span data-ttu-id="dfe93-237">Agora você pode criar e implantar seu serviço.</span><span class="sxs-lookup"><span data-stu-id="dfe93-237">You can now build and deploy your service.</span></span> <span data-ttu-id="dfe93-238">Pressione **F5** no Visual Studio toobuild e implantar o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="dfe93-238">Press **F5** in Visual Studio toobuild and deploy hello application.</span></span> <span data-ttu-id="dfe93-239">Na janela de eventos de diagnóstico hello, você verá uma mensagem que indica que o servidor web hello aberto em http://localhost:8281 /.</span><span class="sxs-lookup"><span data-stu-id="dfe93-239">In hello Diagnostic Events window, you should see a message that indicates that hello web server opened on http://localhost:8281/.</span></span>

> [!NOTE]
> <span data-ttu-id="dfe93-240">Se a porta de saudação já foi aberta por outro processo no seu computador, você verá um erro aqui.</span><span class="sxs-lookup"><span data-stu-id="dfe93-240">If hello port has already been opened by another process on your machine, you may see an error here.</span></span> <span data-ttu-id="dfe93-241">Isso indica que esse ouvinte Olá não pôde ser aberto.</span><span class="sxs-lookup"><span data-stu-id="dfe93-241">This indicates that hello listener couldn't be opened.</span></span> <span data-ttu-id="dfe93-242">Se esse for o caso de Olá, tente usar uma porta diferente para a configuração de ponto de extremidade de saudação em ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="dfe93-242">If that's hello case, try using a different port for hello endpoint configuration in ServiceManifest.xml.</span></span>
> 
> 

<span data-ttu-id="dfe93-243">Quando o serviço de saudação estiver em execução, abra um navegador e navegue muito[http://localhost:8281/api/valores](http://localhost:8281/api/values) tootest-lo.</span><span class="sxs-lookup"><span data-stu-id="dfe93-243">Once hello service is running, open a browser and navigate too[http://localhost:8281/api/values](http://localhost:8281/api/values) tootest it.</span></span>

## <a name="scale-it-out"></a><span data-ttu-id="dfe93-244">Escalar horizontalmente</span><span class="sxs-lookup"><span data-stu-id="dfe93-244">Scale it out</span></span>
<span data-ttu-id="dfe93-245">Dimensionar aplicativos web sem monitoração de estado geralmente significa adicionando mais máquinas e girando Olá web apps neles.</span><span class="sxs-lookup"><span data-stu-id="dfe93-245">Scaling out stateless web apps typically means adding more machines and spinning up hello web apps on them.</span></span> <span data-ttu-id="dfe93-246">Mecanismo de orquestração do Service Fabric pode fazer isso para você sempre que novos nós forem adicionados tooa cluster.</span><span class="sxs-lookup"><span data-stu-id="dfe93-246">Service Fabric's orchestration engine can do this for you whenever new nodes are added tooa cluster.</span></span> <span data-ttu-id="dfe93-247">Quando você cria instâncias de um serviço sem monitoração de estado, você pode especificar o número de saudação de instâncias que você deseja toocreate.</span><span class="sxs-lookup"><span data-stu-id="dfe93-247">When you create instances of a stateless service, you can specify hello number of instances you want toocreate.</span></span> <span data-ttu-id="dfe93-248">Malha do serviço coloca esse número de instâncias em nós de cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="dfe93-248">Service Fabric places that number of instances on nodes in hello cluster.</span></span> <span data-ttu-id="dfe93-249">E torna-se de que não toocreate mais de uma instância em qualquer nó.</span><span class="sxs-lookup"><span data-stu-id="dfe93-249">And it makes sure not toocreate more than one instance on any one node.</span></span> <span data-ttu-id="dfe93-250">Você também pode instruir tooalways Service Fabric cria uma instância em todos os nós especificando **-1** para contagem de instâncias de saudação.</span><span class="sxs-lookup"><span data-stu-id="dfe93-250">You can also instruct Service Fabric tooalways create an instance on every node by specifying **-1** for hello instance count.</span></span> <span data-ttu-id="dfe93-251">Isso garante que sempre que você adicionar nós tooscale-out do seu cluster, uma instância do serviço sem monitoração de estado será criada em novos nós de saudação.</span><span class="sxs-lookup"><span data-stu-id="dfe93-251">This guarantees that whenever you add nodes tooscale out your cluster, an instance of your stateless service will be created on hello new nodes.</span></span> <span data-ttu-id="dfe93-252">Esse valor é uma propriedade de instância de serviço hello, para que ele é definido quando você cria uma instância de serviço.</span><span class="sxs-lookup"><span data-stu-id="dfe93-252">This value is a property of hello service instance, so it is set when you create a service instance.</span></span> <span data-ttu-id="dfe93-253">Você pode fazer isso usando o PowerShell:</span><span class="sxs-lookup"><span data-stu-id="dfe93-253">You can do this through PowerShell:</span></span>

```powershell

New-ServiceFabricService -ApplicationName "fabric:/WebServiceApplication" -ServiceName "fabric:/WebServiceApplication/WebService" -ServiceTypeName "WebServiceType" -Stateless -PartitionSchemeSingleton -InstanceCount -1

```

<span data-ttu-id="dfe93-254">Ou ao definir um serviço padrão em um projeto de serviço sem estado do Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="dfe93-254">You can also do this when you define a default service in a Visual Studio stateless service project:</span></span>

```xml

<DefaultServices>
  <Service Name="WebService">
    <StatelessService ServiceTypeName="WebServiceType" InstanceCount="-1">
      <SingletonPartition />
    </StatelessService>
  </Service>
</DefaultServices>

```

<span data-ttu-id="dfe93-255">Para obter mais informações sobre como o aplicativo toocreate e instâncias de serviço, consulte [implantar um aplicativo](service-fabric-deploy-remove-applications.md).</span><span class="sxs-lookup"><span data-stu-id="dfe93-255">For more information on how toocreate application and service instances, see [Deploy an application](service-fabric-deploy-remove-applications.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="dfe93-256">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dfe93-256">Next steps</span></span>
[<span data-ttu-id="dfe93-257">Depurar seu aplicativo do Service Fabric usando o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dfe93-257">Debug your Service Fabric application by using Visual Studio</span></span>](service-fabric-debugging-your-application.md)

