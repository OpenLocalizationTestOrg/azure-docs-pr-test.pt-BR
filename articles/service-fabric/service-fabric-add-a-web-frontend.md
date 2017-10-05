---
title: Criar um front-end da Web para seu aplicativo do Azure Service Fabric usando ASP.NET Core | Microsoft Docs
description: "Exponha seu aplicativo do Service Fabric na Web usando um projeto de ASP.NET Core a e comunicação entre serviços via Service Remoting."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: vturecek
ms.openlocfilehash: b19aaa652f2c15573ded632ca1348e1a6752f080
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="build-a-web-service-front-end-for-your-application-using-aspnet-core"></a><span data-ttu-id="16af0-103">Compilar um serviço Web front-end para seu aplicativo usando ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="16af0-103">Build a web service front end for your application using ASP.NET Core</span></span>
<span data-ttu-id="16af0-104">Por padrão, os serviços do Azure Service Fabric não fornecem uma interface pública para a Web.</span><span class="sxs-lookup"><span data-stu-id="16af0-104">By default, Azure Service Fabric services do not provide a public interface to the web.</span></span> <span data-ttu-id="16af0-105">Para expor a funcionalidade do aplicativo para clientes HTTP, você precisa criar um projeto Web para atuar como um ponto de entrada e, depois, se comunicar nele com os serviços individuais.</span><span class="sxs-lookup"><span data-stu-id="16af0-105">To expose your application's functionality to HTTP clients, you have to create a web project to act as an entry point and then communicate from there to your individual services.</span></span>

<span data-ttu-id="16af0-106">Neste tutorial, continuamos de onde paramos no tutorial [Criando seu primeiro aplicativo no Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md) e adicionamos um serviço Web do ASP.NET Core antes do serviço de contador com estado.</span><span class="sxs-lookup"><span data-stu-id="16af0-106">In this tutorial, we pick up where we left off in the [Creating your first application in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md) tutorial and add an ASP.NET Core web service in front of the stateful counter service.</span></span> <span data-ttu-id="16af0-107">Se ainda não tiver feito isso, volte e percorra esse tutorial primeiro.</span><span class="sxs-lookup"><span data-stu-id="16af0-107">If you have not already done so, you should go back and step through that tutorial first.</span></span>

## <a name="set-up-your-environment-for-aspnet-core"></a><span data-ttu-id="16af0-108">Configurar o ambiente para o ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="16af0-108">Set up your environment for ASP.NET Core</span></span>

<span data-ttu-id="16af0-109">É necessário o Visual Studio 2017 para acompanhar este tutorial.</span><span class="sxs-lookup"><span data-stu-id="16af0-109">You need Visual Studio 2017 to follow along with this tutorial.</span></span> <span data-ttu-id="16af0-110">Qualquer edição será suficiente.</span><span class="sxs-lookup"><span data-stu-id="16af0-110">Any edition will do.</span></span> 

 - [<span data-ttu-id="16af0-111">Instalar o Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="16af0-111">Install Visual Studio 2017</span></span>](https://www.visualstudio.com/)

<span data-ttu-id="16af0-112">Para desenvolver aplicativos ASP.NET Core do Service Fabric, você deve ter as seguintes cargas de trabalho instaladas:</span><span class="sxs-lookup"><span data-stu-id="16af0-112">To develop ASP.NET Core Service Fabric applications, you should have the following workloads installed:</span></span>
 - <span data-ttu-id="16af0-113">**Desenvolvimento do Azure** (em *Web e Nuvem*)</span><span class="sxs-lookup"><span data-stu-id="16af0-113">**Azure development** (under *Web & Cloud*)</span></span>
 - <span data-ttu-id="16af0-114">**Desenvolvimento do ASP.NET e para a Web** (em *Web e Nuvem*)</span><span class="sxs-lookup"><span data-stu-id="16af0-114">**ASP.NET and web development** (under *Web & Cloud*)</span></span>
 - <span data-ttu-id="16af0-115">**Desenvolvimento de plataforma cruzada do .NET Core** (em *Outros Conjuntos de Ferramentas*)</span><span class="sxs-lookup"><span data-stu-id="16af0-115">**.NET Core cross-platform development** (under *Other Toolsets*)</span></span>

>[!Note] 
><span data-ttu-id="16af0-116">As ferramentas do .NET Core para Visual Studio 2015 não estão sendo mais atualizadas. No entanto, se você ainda estiver usando o Visual Studio 2015, precisará ter as [Ferramentas do .NET Core VS 2015 Versão Prévia 2](https://www.microsoft.com/net/download/core) instaladas.</span><span class="sxs-lookup"><span data-stu-id="16af0-116">The .NET Core tools for Visual Studio 2015 are no longer being updated, however if you are still using Visual Studio 2015, you need to have [.NET Core VS 2015 Tooling Preview 2](https://www.microsoft.com/net/download/core) installed.</span></span>

## <a name="add-an-aspnet-core-service-to-your-application"></a><span data-ttu-id="16af0-117">Adicionar um serviço ASP.NET Core ao seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="16af0-117">Add an ASP.NET Core service to your application</span></span>
<span data-ttu-id="16af0-118">O ASP.NET Core é uma estrutura de desenvolvimento Web leve entre plataformas que permite a criação de uma interface do usuário Web e APIs Web modernas.</span><span class="sxs-lookup"><span data-stu-id="16af0-118">ASP.NET Core is a lightweight, cross-platform web development framework that you can use to create modern web UI and web APIs.</span></span> 

<span data-ttu-id="16af0-119">Vamos adicionar um projeto de API Web do ASP.NET a nosso aplicativo existente.</span><span class="sxs-lookup"><span data-stu-id="16af0-119">Let's add an ASP.NET Web API project to our existing application.</span></span>

1. <span data-ttu-id="16af0-120">No Gerenciador de Soluções, clique com o botão direito do mouse em **Serviços** no projeto de aplicativo e escolha **Adicionar > Novo Serviço do Fabric Service**.</span><span class="sxs-lookup"><span data-stu-id="16af0-120">In Solution Explorer, right-click **Services** within the application project and choose **Add > New Service Fabric Service**.</span></span>
   
    ![Adicionando um novo serviço a um aplicativo existente][vs-add-new-service]
2. <span data-ttu-id="16af0-122">Na página **Criar um Serviço**, escolha **ASP.NET Core** e dê um nome a ele.</span><span class="sxs-lookup"><span data-stu-id="16af0-122">On the **Create a Service** page, choose **ASP.NET Core** and give it a name.</span></span>
   
    ![Escolhendo um serviço Web ASP.NET no diálogo Novo serviço][vs-new-service-dialog]

3. <span data-ttu-id="16af0-124">A próxima página fornece um conjunto de modelos de projeto do ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="16af0-124">The next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="16af0-125">Observe que essas são as mesmas opções que você veria se você tivesse criado um projeto do ASP.NET Core fora de um aplicativo do Service Fabric, com uma pequena quantidade de código adicional para registrar o serviço com o tempo de execução do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="16af0-125">Note that these are the same choices that you would see if you created an ASP.NET Core project outside of a Service Fabric application, with a small amount of additional code to register the service with the Service Fabric runtime.</span></span> <span data-ttu-id="16af0-126">Neste tutorial, escolhemos **API Web**.</span><span class="sxs-lookup"><span data-stu-id="16af0-126">For this tutorial, choose **Web API**.</span></span> <span data-ttu-id="16af0-127">No entanto, você pode aplicar os mesmos conceitos para compilar um aplicativo Web completo.</span><span class="sxs-lookup"><span data-stu-id="16af0-127">However, you can apply the same concepts to building a full web application.</span></span>
   
    ![Escolhendo o tipo de projeto do ASP.NET][vs-new-aspnet-project-dialog]
   
    <span data-ttu-id="16af0-129">Depois de criar o projeto de API Web, você deverá ter dois serviços no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="16af0-129">Once your Web API project is created, you should have two services in your application.</span></span> <span data-ttu-id="16af0-130">Durante a criação do aplicativo, você pode adicionar mais serviços exatamente da mesma forma.</span><span class="sxs-lookup"><span data-stu-id="16af0-130">As you continue to build your application, you can add more services in exactly the same way.</span></span> <span data-ttu-id="16af0-131">Cada um pode seu próprio controle de versão e ser atualizado de forma independente.</span><span class="sxs-lookup"><span data-stu-id="16af0-131">Each can be independently versioned and upgraded.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="16af0-132">Executar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="16af0-132">Run the application</span></span>
<span data-ttu-id="16af0-133">Para ter uma ideia do que fizemos, vamos implantar o novo aplicativo e examinar o comportamento padrão apresentado pelo modelo de API Web do ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="16af0-133">To get a sense of what we've done, let's deploy the new application and take a look at the default behavior that the ASP.NET Core Web API template provides.</span></span>

1. <span data-ttu-id="16af0-134">Pressione F5 no Visual Studio para depurar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="16af0-134">Press F5 in Visual Studio to debug the app.</span></span>
2. <span data-ttu-id="16af0-135">Quando a implantação for concluída, o Visual Studio iniciará um navegador na raiz do serviço de API Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="16af0-135">When deployment is complete, Visual Studio launches a browser to the root of the ASP.NET Web API service.</span></span> <span data-ttu-id="16af0-136">O modelo da API Web ASP.NET Core não fornece um comportamento padrão para a raiz; portanto, você deverá receber um erro 404 no navegador.</span><span class="sxs-lookup"><span data-stu-id="16af0-136">The ASP.NET Core Web API template doesn't provide default behavior for the root, so you should see a 404 error in the browser.</span></span>
3. <span data-ttu-id="16af0-137">Adicione `/api/values` ao local no navegador.</span><span class="sxs-lookup"><span data-stu-id="16af0-137">Add `/api/values` to the location in the browser.</span></span> <span data-ttu-id="16af0-138">Isso invocará o método `Get` no ValuesController no modelo de API Web.</span><span class="sxs-lookup"><span data-stu-id="16af0-138">This invokes the `Get` method on the ValuesController in the Web API template.</span></span> <span data-ttu-id="16af0-139">Ele retorna a resposta padrão fornecida pelo modelo – uma matriz JSON que contém duas cadeias de caracteres:</span><span class="sxs-lookup"><span data-stu-id="16af0-139">It returns the default response that is provided by the template--a JSON array that contains two strings:</span></span>
   
    ![Valores padrão retornados do modelo de API Web do ASP.NET Core][browser-aspnet-template-values]
   
    <span data-ttu-id="16af0-141">Ao final do tutorial, esta página mostrará o valor mais recente do contador de nosso serviço com estado, em vez das cadeias de caracteres padrão.</span><span class="sxs-lookup"><span data-stu-id="16af0-141">By the end of the tutorial, this page will show the most recent counter value from our stateful service instead of the default strings.</span></span>

## <a name="connect-the-services"></a><span data-ttu-id="16af0-142">Conectar os serviços</span><span class="sxs-lookup"><span data-stu-id="16af0-142">Connect the services</span></span>
<span data-ttu-id="16af0-143">O Service Fabric fornece total flexibilidade na comunicação com Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="16af0-143">Service Fabric provides complete flexibility in how you communicate with reliable services.</span></span> <span data-ttu-id="16af0-144">Em um único aplicativo, você pode ter serviços acessíveis por meio de TCP, outros serviços acessíveis por meio de uma API REST HTTP e ainda outros serviços que são acessíveis por meio de soquetes da Web.</span><span class="sxs-lookup"><span data-stu-id="16af0-144">Within a single application, you might have services that are accessible via TCP, other services that are accessible via an HTTP REST API, and still other services that are accessible via web sockets.</span></span> <span data-ttu-id="16af0-145">Para saber mais sobre as opções disponíveis e as compensações envolvidas, confira [Comunicação com os serviços](service-fabric-connect-and-communicate-with-services.md).</span><span class="sxs-lookup"><span data-stu-id="16af0-145">For background on the options available and the tradeoffs involved, see [Communicating with services](service-fabric-connect-and-communicate-with-services.md).</span></span> <span data-ttu-id="16af0-146">Neste tutorial, usamos a [Comunicação Remota do Serviço do Service Fabric](service-fabric-reliable-services-communication-remoting.md), fornecida no SDK.</span><span class="sxs-lookup"><span data-stu-id="16af0-146">In this tutorial, we use [Service Fabric Service Remoting](service-fabric-reliable-services-communication-remoting.md), provided in the SDK.</span></span>

<span data-ttu-id="16af0-147">Na abordagem da Comunicação Remota do Serviço (modelada em chamadas de procedimento remoto ou RPCs), você define uma interface para atuar como o contrato público do serviço.</span><span class="sxs-lookup"><span data-stu-id="16af0-147">In the Service Remoting approach (modeled on remote procedure calls or RPCs), you define an interface to act as the public contract for the service.</span></span> <span data-ttu-id="16af0-148">Em seguida, você usa essa interface para gerar uma classe proxy para interação com o serviço.</span><span class="sxs-lookup"><span data-stu-id="16af0-148">Then, you use that interface to generate a proxy class for interacting with the service.</span></span>

### <a name="create-the-remoting-interface"></a><span data-ttu-id="16af0-149">Criar a interface de comunicação remota</span><span class="sxs-lookup"><span data-stu-id="16af0-149">Create the remoting interface</span></span>
<span data-ttu-id="16af0-150">Vamos começar criando a interface para atuar como o contrato entre o serviço com estado e outros serviços, neste caso, o projeto Web ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="16af0-150">Let's start by creating the interface to act as the contract between the stateful service and other services, in this case the ASP.NET Core web project.</span></span> <span data-ttu-id="16af0-151">Essa interface deve ser compartilhada por todos os serviços que a usam para fazer chamadas RPC. Portanto, nós a criaremos em seu próprio projeto de Biblioteca de Classes.</span><span class="sxs-lookup"><span data-stu-id="16af0-151">This interface must be shared by all services that use it to make RPC calls, so we'll create it in its own Class Library project.</span></span>

1. <span data-ttu-id="16af0-152">No Gerenciador de Soluções, clique com o botão direito do mouse na solução e escolha **Adicione** > **Novo Projeto**.</span><span class="sxs-lookup"><span data-stu-id="16af0-152">In Solution Explorer, right-click your solution and choose **Add** > **New Project**.</span></span>

2. <span data-ttu-id="16af0-153">Escolha a entrada do **Visual C#** no painel de navegação esquerdo e selecione o modelo **Biblioteca de Classes**.</span><span class="sxs-lookup"><span data-stu-id="16af0-153">Choose the **Visual C#** entry in the left navigation pane and then select the **Class Library** template.</span></span> <span data-ttu-id="16af0-154">Verifique se a versão do .NET Framework está definida como **4.5.2**.</span><span class="sxs-lookup"><span data-stu-id="16af0-154">Ensure that the .NET Framework version is set to **4.5.2**.</span></span>
   
    ![Criando um projeto de interface para o serviço com estado][vs-add-class-library-project]

3. <span data-ttu-id="16af0-156">Instale o pacote NuGet **Microsoft.ServiceFabric.Services.Remoting**.</span><span class="sxs-lookup"><span data-stu-id="16af0-156">Install the **Microsoft.ServiceFabric.Services.Remoting** NuGet package.</span></span> <span data-ttu-id="16af0-157">Pesquise **Microsoft.ServiceFabric.Services.Remoting** no gerenciador de pacotes NuGet e instale-o para todos os projetos na solução que usam a Comunicação Remota do Serviço, incluindo:</span><span class="sxs-lookup"><span data-stu-id="16af0-157">Search for  **Microsoft.ServiceFabric.Services.Remoting** in the NuGet package manager and install it for all projects in the solution that use Service Remoting, including:</span></span>
   - <span data-ttu-id="16af0-158">O projeto de Biblioteca de Classes que contém a interface do serviço</span><span class="sxs-lookup"><span data-stu-id="16af0-158">The Class Library project that contains the service interface</span></span>
   - <span data-ttu-id="16af0-159">O projeto de Serviço com Estado</span><span class="sxs-lookup"><span data-stu-id="16af0-159">The Stateful Service project</span></span>
   - <span data-ttu-id="16af0-160">O projeto de serviço Web ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="16af0-160">The ASP.NET Core web service project</span></span>
   
    ![Adicionar o pacote NuGet de serviços][vs-services-nuget-package]

4. <span data-ttu-id="16af0-162">Na biblioteca de classes, crie uma interface com um único método, `GetCountAsync` e estenda a interface por meio do `Microsoft.ServiceFabric.Services.Remoting.IService`.</span><span class="sxs-lookup"><span data-stu-id="16af0-162">In the class library, create an interface with a single method, `GetCountAsync`, and extend the interface from `Microsoft.ServiceFabric.Services.Remoting.IService`.</span></span> <span data-ttu-id="16af0-163">A interface de comunicação remota deve derivar dessa interface para indicar que ela é uma interface da Comunicação Remota do Serviço.</span><span class="sxs-lookup"><span data-stu-id="16af0-163">The remoting interface must derive from this interface to indicate that it is a Service Remoting interface.</span></span>
   
    ```c#
    using Microsoft.ServiceFabric.Services.Remoting;
    using System.Threading.Tasks;
        
    ...

    namespace MyStatefulService.Interface
    {
        public interface ICounter: IService
        {
            Task<long> GetCountAsync();
        }
    }
    ```

### <a name="implement-the-interface-in-your-stateful-service"></a><span data-ttu-id="16af0-164">Implemente a interface em seu serviço com estado</span><span class="sxs-lookup"><span data-stu-id="16af0-164">Implement the interface in your stateful service</span></span>
<span data-ttu-id="16af0-165">Agora que definimos a interface, precisamos implementá-la no serviço com estado.</span><span class="sxs-lookup"><span data-stu-id="16af0-165">Now that we have defined the interface, we need to implement it in the stateful service.</span></span>

1. <span data-ttu-id="16af0-166">Em seu serviço com estado, adicione uma referência ao projeto de biblioteca de classes que contém a interface.</span><span class="sxs-lookup"><span data-stu-id="16af0-166">In your stateful service, add a reference to the class library project that contains the interface.</span></span>
   
    ![Adicionando uma referência ao projeto de biblioteca de classes ao serviço com estado][vs-add-class-library-reference]
2. <span data-ttu-id="16af0-168">Localize a classe que herda de `StatefulService`, como `MyStatefulService`, e a estenda para implementar a interface `ICounter`.</span><span class="sxs-lookup"><span data-stu-id="16af0-168">Locate the class that inherits from `StatefulService`, such as `MyStatefulService`, and extend it to implement the `ICounter` interface.</span></span>
   
    ```c#
    using MyStatefulService.Interface;
   
    ...
   
    public class MyStatefulService : StatefulService, ICounter
    {        
         ...
    }
    ```
3. <span data-ttu-id="16af0-169">Agora, implemente o método único definido na interface `ICounter`, `GetCountAsync`.</span><span class="sxs-lookup"><span data-stu-id="16af0-169">Now implement the single method that is defined in the `ICounter` interface, `GetCountAsync`.</span></span>
   
    ```c#
    public async Task<long> GetCountAsync()
    {
        var myDictionary = 
            await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
   
        using (var tx = this.StateManager.CreateTransaction())
        {          
            var result = await myDictionary.TryGetValueAsync(tx, "Counter");
            return result.HasValue ? result.Value : 0;
        }
    }
    ```

### <a name="expose-the-stateful-service-using-a-service-remoting-listener"></a><span data-ttu-id="16af0-170">Expor o serviço com estado usando um ouvinte de comunicação remota do serviço</span><span class="sxs-lookup"><span data-stu-id="16af0-170">Expose the stateful service using a service remoting listener</span></span>
<span data-ttu-id="16af0-171">Com a interface `ICounter` implementada, a etapa final é abrir o canal de comunicação da Comunicação Remota do Serviço.</span><span class="sxs-lookup"><span data-stu-id="16af0-171">With the `ICounter` interface implemented, the final step is to open the Service Remoting communication channel.</span></span> <span data-ttu-id="16af0-172">Para serviços com estado, o Service Fabric fornece um método substituível chamado `CreateServiceReplicaListeners`.</span><span class="sxs-lookup"><span data-stu-id="16af0-172">For stateful services, Service Fabric provides an overridable method called `CreateServiceReplicaListeners`.</span></span> <span data-ttu-id="16af0-173">Com esse método, você pode especificar um ou mais ouvintes de comunicação, com base no tipo de comunicação que você deseja habilitar para o serviço.</span><span class="sxs-lookup"><span data-stu-id="16af0-173">With this method, you can specify one or more communication listeners, based on the type of communication that you want to enable for your service.</span></span>

> [!NOTE]
> <span data-ttu-id="16af0-174">O método equivalente para abrir um canal de comunicação para serviços sem estado é chamado `CreateServiceInstanceListeners`.</span><span class="sxs-lookup"><span data-stu-id="16af0-174">The equivalent method for opening a communication channel to stateless services is called `CreateServiceInstanceListeners`.</span></span>

<span data-ttu-id="16af0-175">Nesse caso, substituímos o método `CreateServiceReplicaListeners` existente e fornecemos uma instância do `ServiceRemotingListener`, que cria um ponto de extremidade RPC que pode ser chamado por clientes por meio do `ServiceProxy`.</span><span class="sxs-lookup"><span data-stu-id="16af0-175">In this case, we replace the existing `CreateServiceReplicaListeners` method and provide an instance of `ServiceRemotingListener`, which creates an RPC endpoint that is callable from clients through `ServiceProxy`.</span></span>  

<span data-ttu-id="16af0-176">O método de extensão `CreateServiceRemotingListener` na interface `IService` permite que você crie facilmente um `ServiceRemotingListener` com todas as configurações padrão.</span><span class="sxs-lookup"><span data-stu-id="16af0-176">The `CreateServiceRemotingListener` extension method on the `IService` interface allows you to easily create a `ServiceRemotingListener` with all default settings.</span></span> <span data-ttu-id="16af0-177">Para usar esse método de extensão, verifique se você importou o namespace `Microsoft.ServiceFabric.Services.Remoting.Runtime`.</span><span class="sxs-lookup"><span data-stu-id="16af0-177">To use this extension method, ensure you have the `Microsoft.ServiceFabric.Services.Remoting.Runtime` namespace imported.</span></span> 

```c#
using Microsoft.ServiceFabric.Services.Remoting.Runtime;

...

protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new List<ServiceReplicaListener>()
    {
        new ServiceReplicaListener(
            (context) =>
                this.CreateServiceRemotingListener(context))
    };
}
```


### <a name="use-the-serviceproxy-class-to-interact-with-the-service"></a><span data-ttu-id="16af0-178">Usar a classe ServiceProxy para interagir com o serviço</span><span class="sxs-lookup"><span data-stu-id="16af0-178">Use the ServiceProxy class to interact with the service</span></span>
<span data-ttu-id="16af0-179">Agora, nosso serviço com estado está pronto para receber o tráfego de outros serviços na RPC.</span><span class="sxs-lookup"><span data-stu-id="16af0-179">Our stateful service is now ready to receive traffic from other services over RPC.</span></span> <span data-ttu-id="16af0-180">Assim, tudo o que resta é adicionar o código para se comunicar com ele a partir do serviço Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="16af0-180">So all that remains is adding the code to communicate with it from the ASP.NET web service.</span></span>

1. <span data-ttu-id="16af0-181">Em seu projeto ASP.NET, adicione uma referência à biblioteca de classes que contém a interface `ICounter` .</span><span class="sxs-lookup"><span data-stu-id="16af0-181">In your ASP.NET project, add a reference to the class library that contains the `ICounter` interface.</span></span>

2. <span data-ttu-id="16af0-182">Anteriormente, você adicionou o pacote NuGet **Microsoft.ServiceFabric.Services.Remoting** ao projeto ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="16af0-182">Earlier you added the **Microsoft.ServiceFabric.Services.Remoting** NuGet package to the ASP.NET project.</span></span> <span data-ttu-id="16af0-183">Esse pacote fornece a classe `ServiceProxy`, que você usa para fazer chamadas RPC ao serviço com estado.</span><span class="sxs-lookup"><span data-stu-id="16af0-183">This package provides the `ServiceProxy` class which you use to make RPC calls to the stateful service.</span></span> <span data-ttu-id="16af0-184">Verifique se o pacote NuGet está instalado no projeto de serviço Web ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="16af0-184">Ensure this NuGet package is installed in the ASP.NET Core web service project.</span></span>

4. <span data-ttu-id="16af0-185">Na pasta **Controladores**, abra a classe `ValuesController`.</span><span class="sxs-lookup"><span data-stu-id="16af0-185">In the **Controllers** folder, open the `ValuesController` class.</span></span> <span data-ttu-id="16af0-186">Observe que o método `Get` atualmente retorna somente uma matriz de cadeia de caracteres codificados "value1" e "value2", que coincide com o que vimos anteriormente no navegador.</span><span class="sxs-lookup"><span data-stu-id="16af0-186">Note that the `Get` method currently just returns a hard-coded string array of "value1" and "value2"--which matches what we saw earlier in the browser.</span></span> <span data-ttu-id="16af0-187">Substitua essa implementação pelo seguinte código:</span><span class="sxs-lookup"><span data-stu-id="16af0-187">Replace this implementation with the following code:</span></span>
   
    ```c#
    using MyStatefulService.Interface;
    using Microsoft.ServiceFabric.Services.Client;
    using Microsoft.ServiceFabric.Services.Remoting.Client;
   
    ...

    [HttpGet]
    public async Task<IEnumerable<string>> Get()
    {
        ICounter counter =
            ServiceProxy.Create<ICounter>(new Uri("fabric:/MyApplication/MyStatefulService"), new ServicePartitionKey(0));
   
        long count = await counter.GetCountAsync();
   
        return new string[] { count.ToString() };
    }
    ```
   
    <span data-ttu-id="16af0-188">A primeira linha de código é a principal.</span><span class="sxs-lookup"><span data-stu-id="16af0-188">The first line of code is the key one.</span></span> <span data-ttu-id="16af0-189">Para criar o proxy ICounter para o serviço com estado, você precisa fornecer duas informações: uma ID de partição e o nome do serviço.</span><span class="sxs-lookup"><span data-stu-id="16af0-189">To create the ICounter proxy to the stateful service, you need to provide two pieces of information: a partition ID and the name of the service.</span></span>
   
    <span data-ttu-id="16af0-190">Você pode usar o particionamento para dimensionar serviços com estado dividindo seu estado em diferentes recipientes com base em uma chave definida por você, como ID de cliente ou CEP.</span><span class="sxs-lookup"><span data-stu-id="16af0-190">You can use partitioning to scale stateful services by breaking up their state into different buckets, based on a key that you define, such as a customer ID or postal code.</span></span> <span data-ttu-id="16af0-191">Em nosso aplicativo comum, o serviço com estado tem somente uma partição, portanto, a chave não importa.</span><span class="sxs-lookup"><span data-stu-id="16af0-191">In our trivial application, the stateful service only has one partition, so the key doesn't matter.</span></span> <span data-ttu-id="16af0-192">Qualquer chave que você fornecer levará até a mesma partição.</span><span class="sxs-lookup"><span data-stu-id="16af0-192">Any key that you provide will lead to the same partition.</span></span> <span data-ttu-id="16af0-193">Confira [Como particionar Reliable Services do Service Fabric](service-fabric-concepts-partitioning.md)para saber mais sobre como particionar seu serviço.</span><span class="sxs-lookup"><span data-stu-id="16af0-193">To learn more about partitioning services, see [How to partition Service Fabric Reliable Services](service-fabric-concepts-partitioning.md).</span></span>
   
    <span data-ttu-id="16af0-194">O nome do serviço é um URI de malha:/&lt;application_name&gt;/&lt;service_name&gt;.</span><span class="sxs-lookup"><span data-stu-id="16af0-194">The service name is a URI of the form fabric:/&lt;application_name&gt;/&lt;service_name&gt;.</span></span>
   
    <span data-ttu-id="16af0-195">Com esses dois tipos de informação, o Service Fabric pode identificar exclusivamente o computador para o qual as solicitações devem ser enviadas.</span><span class="sxs-lookup"><span data-stu-id="16af0-195">With these two pieces of information, Service Fabric can uniquely identify the machine that requests should be sent to.</span></span> <span data-ttu-id="16af0-196">A classe `ServiceProxy` também cuidará da situação no caso de a máquina que hospeda a partição do serviço com estado falhar e outra máquina tiver que ser promovida em seu lugar.</span><span class="sxs-lookup"><span data-stu-id="16af0-196">The `ServiceProxy` class also seamlessly handles the case where the machine that hosts the stateful service partition fails and another machine must be promoted to take its place.</span></span> <span data-ttu-id="16af0-197">Essa abstração torna a escrita de código do cliente para lidar com outros serviço bem mais simples.</span><span class="sxs-lookup"><span data-stu-id="16af0-197">This abstraction makes writing the client code to deal with other services significantly simpler.</span></span>
   
    <span data-ttu-id="16af0-198">Assim que tivermos o proxy, podemos simplesmente chamar o método `GetCountAsync` e retornar seu resultado.</span><span class="sxs-lookup"><span data-stu-id="16af0-198">Once we have the proxy, we simply invoke the `GetCountAsync` method and return its result.</span></span>

5. <span data-ttu-id="16af0-199">Pressione F5 novamente para executar o aplicativo modificado.</span><span class="sxs-lookup"><span data-stu-id="16af0-199">Press F5 again to run the modified application.</span></span> <span data-ttu-id="16af0-200">Como antes, o Visual Studio inicia o navegador automaticamente na raiz do projeto Web.</span><span class="sxs-lookup"><span data-stu-id="16af0-200">As before, Visual Studio automatically launches the browser to the root of the web project.</span></span> <span data-ttu-id="16af0-201">Adicione o caminho "api/values" e você deve ver o valor atual do contador retornado.</span><span class="sxs-lookup"><span data-stu-id="16af0-201">Add the "api/values" path, and you should see the current counter value returned.</span></span>
   
    ![O valor do contador com estado exibido no navegador][browser-aspnet-counter-value]
   
    <span data-ttu-id="16af0-203">Atualize o navegador periodicamente para ver o valor do contador de atualização.</span><span class="sxs-lookup"><span data-stu-id="16af0-203">Refresh the browser periodically to see the counter value update.</span></span>

## <a name="kestrel-and-weblistener"></a><span data-ttu-id="16af0-204">Kestrel e WebListener</span><span class="sxs-lookup"><span data-stu-id="16af0-204">Kestrel and WebListener</span></span>

<span data-ttu-id="16af0-205">O servidor Web do ASP.NET Core padrão, conhecido como Kestrel, [não tem suporte no momento para lidar com o tráfego direto da Internet](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel).</span><span class="sxs-lookup"><span data-stu-id="16af0-205">The default ASP.NET Core web server, known as Kestrel, is [not currently supported for handling direct internet traffic](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel).</span></span> <span data-ttu-id="16af0-206">Como resultado, o modelo de serviço sem estado do ASP.NET Core do Service Fabric usa o [WebListener](https://docs.microsoft.com/aspnet/core/fundamentals/servers/weblistener) por padrão.</span><span class="sxs-lookup"><span data-stu-id="16af0-206">As a result, the ASP.NET Core stateless service template for Service Fabric uses [WebListener](https://docs.microsoft.com/aspnet/core/fundamentals/servers/weblistener) by default.</span></span> 

<span data-ttu-id="16af0-207">Para saber mais sobre Kestrel e WebListener nos serviços do Service Fabric, consulte [ASP.NET Core em Serviços Confiáveis do Service Fabric](service-fabric-reliable-services-communication-aspnetcore.md).</span><span class="sxs-lookup"><span data-stu-id="16af0-207">To learn more about Kestrel and WebListener in Service Fabric services, please refer to [ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md).</span></span>

## <a name="connecting-to-a-reliable-actor-service"></a><span data-ttu-id="16af0-208">Conectando-se a um serviço do Reliable Actor</span><span class="sxs-lookup"><span data-stu-id="16af0-208">Connecting to a Reliable Actor service</span></span>
<span data-ttu-id="16af0-209">Este tutorial se concentra em adicionar um front-end da Web que se comunique com um serviço com estado.</span><span class="sxs-lookup"><span data-stu-id="16af0-209">This tutorial focused on adding a web front end that communicated with a stateful service.</span></span> <span data-ttu-id="16af0-210">No entanto, você pode seguir um modelo muito semelhante ao conversar com atores.</span><span class="sxs-lookup"><span data-stu-id="16af0-210">However, you can follow a very similar model to talk to actors.</span></span> <span data-ttu-id="16af0-211">Quando você cria um projeto do Reliable Actor, o Visual Studio gera automaticamente um projeto de interface para você.</span><span class="sxs-lookup"><span data-stu-id="16af0-211">When you create a Reliable Actor project, Visual Studio automatically generates an interface project for you.</span></span> <span data-ttu-id="16af0-212">Você pode usar essa interface para gerar um proxy de ator no projeto Web para se comunicar com o ator.</span><span class="sxs-lookup"><span data-stu-id="16af0-212">You can use that interface to generate an actor proxy in the web project to communicate with the actor.</span></span> <span data-ttu-id="16af0-213">O canal de comunicação é fornecido automaticamente.</span><span class="sxs-lookup"><span data-stu-id="16af0-213">The communication channel is provided automatically.</span></span> <span data-ttu-id="16af0-214">Assim, não é necessário fazer nada equivalente a estabelecer um `ServiceRemotingListener` , como foi feito para o serviço com estado neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="16af0-214">So you do not need to do anything that is equivalent to establishing a `ServiceRemotingListener` like you did for the stateful service in this tutorial.</span></span>

## <a name="how-web-services-work-on-your-local-cluster"></a><span data-ttu-id="16af0-215">Como os serviços Web funcionam no cluster local</span><span class="sxs-lookup"><span data-stu-id="16af0-215">How web services work on your local cluster</span></span>
<span data-ttu-id="16af0-216">Em geral, você pode implantar exatamente o mesmo aplicativo do Service Fabric em um cluster com vários computadores implantados no cluster local e ter a certeza de que ele funciona como esperado.</span><span class="sxs-lookup"><span data-stu-id="16af0-216">In general, you can deploy exactly the same Service Fabric application to a multi-machine cluster that you deployed on your local cluster and be highly confident that it works as you expect.</span></span> <span data-ttu-id="16af0-217">Isso ocorre porque o cluster local é simplesmente uma configuração de cinco nós recolhidos em um único computador.</span><span class="sxs-lookup"><span data-stu-id="16af0-217">This is because your local cluster is simply a five-node configuration that is collapsed to a single machine.</span></span>

<span data-ttu-id="16af0-218">No entanto, quando se trata de serviços Web, há uma nuance essencial.</span><span class="sxs-lookup"><span data-stu-id="16af0-218">When it comes to web services, however, there is one key nuance.</span></span> <span data-ttu-id="16af0-219">Quando o cluster fica atrás de um balanceador de carga, como é o caso no Azure, você deve garantir que os serviços Web são implantados em todos os computadores, já que o balanceador de carga simplesmente faz round-robin com o tráfego entre os computadores.</span><span class="sxs-lookup"><span data-stu-id="16af0-219">When your cluster sits behind a load balancer, as it does in Azure, you must ensure that your web services are deployed on every machine since the load balancer simply round-robins traffic across the machines.</span></span> <span data-ttu-id="16af0-220">Isso pode ser feito configurando `InstanceCount` do serviço para o valor especial “-1”.</span><span class="sxs-lookup"><span data-stu-id="16af0-220">You can do this by setting the `InstanceCount` for the service to the special value of "-1".</span></span>

<span data-ttu-id="16af0-221">Por outro lado, quando você executa um serviço Web localmente, você precisa garantir que apenas uma instância de serviço esteja em execução.</span><span class="sxs-lookup"><span data-stu-id="16af0-221">By contrast, when you run a web service locally, you need to ensure that only one instance of the service is running.</span></span> <span data-ttu-id="16af0-222">Caso contrário, você terá conflitos de vários processos que estão escutando o mesmo caminho e a mesma porta.</span><span class="sxs-lookup"><span data-stu-id="16af0-222">Otherwise, you run into conflicts from multiple processes that are listening on the same path and port.</span></span> <span data-ttu-id="16af0-223">Como resultado, a contagem de instâncias de serviço Web deve ser definida como "1" para implantações locais.</span><span class="sxs-lookup"><span data-stu-id="16af0-223">As a result, the web service instance count should be set to "1" for local deployments.</span></span>

<span data-ttu-id="16af0-224">Para saber como configurar valores diferentes para um ambiente diferente, confira [Gerenciar parâmetros de aplicativo para vários ambientes](service-fabric-manage-multiple-environment-app-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="16af0-224">To learn how to configure different values for different environment, see [Managing application parameters for multiple environments](service-fabric-manage-multiple-environment-app-configuration.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="16af0-225">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="16af0-225">Next steps</span></span>
<span data-ttu-id="16af0-226">Agora que você tem um front-end da Web configurado para o aplicativo com o ASP.NET Core, saiba mais sobre o [ASP.NET Core nos Reliable Services do Service Fabric](service-fabric-reliable-services-communication-aspnetcore.md) para obter uma compreensão detalhada de como o ASP.NET Core funciona com o Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="16af0-226">Now that you have a web front end set up for your application with ASP.NET Core, learn more about [ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md) for an in-depth understanding of how ASP.NET Core works with Service Fabric.</span></span>

<span data-ttu-id="16af0-227">Em seguida, [saiba mais sobre a comunicação com os serviços](service-fabric-connect-and-communicate-with-services.md) em geral para ter uma ideia completo de como a comunicação do serviço funciona no Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="16af0-227">Next, [learn more about communicating with services](service-fabric-connect-and-communicate-with-services.md) in general to get a complete picture of how service communication works in Service Fabric.</span></span>

<span data-ttu-id="16af0-228">Assim que você tiver uma boa compreensão de como a comunicação do serviço funciona, [cria um cluster no Azure e implanta o aplicativo na nuvem](service-fabric-cluster-creation-via-portal.md).</span><span class="sxs-lookup"><span data-stu-id="16af0-228">Once you have a good understanding of how service communication works, [create a cluster in Azure and deploy your application to the cloud](service-fabric-cluster-creation-via-portal.md).</span></span>

<!-- Image References -->

[vs-add-new-service]: ./media/service-fabric-add-a-web-frontend/vs-add-new-service.png
[vs-new-service-dialog]: ./media/service-fabric-add-a-web-frontend/vs-new-service-dialog.png
[vs-new-aspnet-project-dialog]: ./media/service-fabric-add-a-web-frontend/vs-new-aspnet-project-dialog.png
[browser-aspnet-template-values]: ./media/service-fabric-add-a-web-frontend/browser-aspnet-template-values.png
[vs-add-class-library-project]: ./media/service-fabric-add-a-web-frontend/vs-add-class-library-project.png
[vs-add-class-library-reference]: ./media/service-fabric-add-a-web-frontend/vs-add-class-library-reference.png
[vs-services-nuget-package]: ./media/service-fabric-add-a-web-frontend/vs-services-nuget-package.png
[browser-aspnet-counter-value]: ./media/service-fabric-add-a-web-frontend/browser-aspnet-counter-value.png
[vs-create-platform]: ./media/service-fabric-add-a-web-frontend/vs-create-platform.png


<!-- external links -->
[dotnetcore-install]: https://www.microsoft.com/net/core#windows
