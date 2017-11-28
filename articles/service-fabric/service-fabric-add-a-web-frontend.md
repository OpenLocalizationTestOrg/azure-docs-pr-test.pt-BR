---
title: aaaCreate um front-end da web para seu aplicativo do Azure Service Fabric usando o ASP.NET Core | Microsoft Docs
description: "Expor web Service Fabric application toohello por meio de um projeto do ASP.NET Core e comunicação entre serviços por meio de comunicação remota do serviço."
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
ms.openlocfilehash: 0c4454d6cac4c2e343bd6e93e56d3d2f0ebfc4ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-web-service-front-end-for-your-application-using-aspnet-core"></a><span data-ttu-id="25010-103">Compilar um serviço Web front-end para seu aplicativo usando ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="25010-103">Build a web service front end for your application using ASP.NET Core</span></span>
<span data-ttu-id="25010-104">Por padrão, os serviços do Azure Service Fabric não fornecem uma web toohello de interface pública.</span><span class="sxs-lookup"><span data-stu-id="25010-104">By default, Azure Service Fabric services do not provide a public interface toohello web.</span></span> <span data-ttu-id="25010-105">tooexpose clientes de tooHTTP de funcionalidade do aplicativo, você tem toocreate web tooact como um ponto de entrada do projeto e comunicar-se de tooyour há serviços individuais.</span><span class="sxs-lookup"><span data-stu-id="25010-105">tooexpose your application's functionality tooHTTP clients, you have toocreate a web project tooact as an entry point and then communicate from there tooyour individual services.</span></span>

<span data-ttu-id="25010-106">Neste tutorial, podemos escolher onde é deixada no hello [criando seu primeiro aplicativo no Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md) tutorial e adicionar um serviço da web ASP.NET Core na frente do serviço de monitoração de estado do contador hello.</span><span class="sxs-lookup"><span data-stu-id="25010-106">In this tutorial, we pick up where we left off in hello [Creating your first application in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md) tutorial and add an ASP.NET Core web service in front of hello stateful counter service.</span></span> <span data-ttu-id="25010-107">Se ainda não tiver feito isso, volte e percorra esse tutorial primeiro.</span><span class="sxs-lookup"><span data-stu-id="25010-107">If you have not already done so, you should go back and step through that tutorial first.</span></span>

## <a name="set-up-your-environment-for-aspnet-core"></a><span data-ttu-id="25010-108">Configurar o ambiente para o ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="25010-108">Set up your environment for ASP.NET Core</span></span>

<span data-ttu-id="25010-109">É necessário o Visual Studio de 2017 toofollow junto com este tutorial.</span><span class="sxs-lookup"><span data-stu-id="25010-109">You need Visual Studio 2017 toofollow along with this tutorial.</span></span> <span data-ttu-id="25010-110">Qualquer edição será suficiente.</span><span class="sxs-lookup"><span data-stu-id="25010-110">Any edition will do.</span></span> 

 - [<span data-ttu-id="25010-111">Instalar o Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="25010-111">Install Visual Studio 2017</span></span>](https://www.visualstudio.com/)

<span data-ttu-id="25010-112">aplicativos do ASP.NET Core Service Fabric toodevelop, você deve ter Olá instaladas de cargas de trabalho a seguir:</span><span class="sxs-lookup"><span data-stu-id="25010-112">toodevelop ASP.NET Core Service Fabric applications, you should have hello following workloads installed:</span></span>
 - <span data-ttu-id="25010-113">**Desenvolvimento do Azure** (em *Web e Nuvem*)</span><span class="sxs-lookup"><span data-stu-id="25010-113">**Azure development** (under *Web & Cloud*)</span></span>
 - <span data-ttu-id="25010-114">**Desenvolvimento do ASP.NET e para a Web** (em *Web e Nuvem*)</span><span class="sxs-lookup"><span data-stu-id="25010-114">**ASP.NET and web development** (under *Web & Cloud*)</span></span>
 - <span data-ttu-id="25010-115">**Desenvolvimento de plataforma cruzada do .NET Core** (em *Outros Conjuntos de Ferramentas*)</span><span class="sxs-lookup"><span data-stu-id="25010-115">**.NET Core cross-platform development** (under *Other Toolsets*)</span></span>

>[!Note] 
><span data-ttu-id="25010-116">Olá ferramentas .NET Core para Visual Studio 2015 não serão mais sendo atualizadas, no entanto, se você ainda estiver usando o Visual Studio 2015, você precisa toohave [.NET Core VS 2015 Tooling Preview 2](https://www.microsoft.com/net/download/core) instalado.</span><span class="sxs-lookup"><span data-stu-id="25010-116">hello .NET Core tools for Visual Studio 2015 are no longer being updated, however if you are still using Visual Studio 2015, you need toohave [.NET Core VS 2015 Tooling Preview 2](https://www.microsoft.com/net/download/core) installed.</span></span>

## <a name="add-an-aspnet-core-service-tooyour-application"></a><span data-ttu-id="25010-117">Adicionar um aplicativo do ASP.NET Core serviço tooyour</span><span class="sxs-lookup"><span data-stu-id="25010-117">Add an ASP.NET Core service tooyour application</span></span>
<span data-ttu-id="25010-118">ASP.NET Core é uma estrutura de desenvolvimento de web leve e várias plataformas, você pode usar a interface da web modernos toocreate e APIs da web.</span><span class="sxs-lookup"><span data-stu-id="25010-118">ASP.NET Core is a lightweight, cross-platform web development framework that you can use toocreate modern web UI and web APIs.</span></span> 

<span data-ttu-id="25010-119">Vamos adicionar um aplicativo do ASP.NET Web API projeto tooour existente.</span><span class="sxs-lookup"><span data-stu-id="25010-119">Let's add an ASP.NET Web API project tooour existing application.</span></span>

1. <span data-ttu-id="25010-120">No Gerenciador de soluções, clique com botão direito **serviços** dentro Olá projeto de aplicativo e escolha **Adicionar > novo serviço do Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="25010-120">In Solution Explorer, right-click **Services** within hello application project and choose **Add > New Service Fabric Service**.</span></span>
   
    ![Adicionando um novo aplicativo de serviço tooan existente][vs-add-new-service]
2. <span data-ttu-id="25010-122">Em Olá **criar um serviço** escolha **ASP.NET Core** e dê a ele um nome.</span><span class="sxs-lookup"><span data-stu-id="25010-122">On hello **Create a Service** page, choose **ASP.NET Core** and give it a name.</span></span>
   
    ![Escolhendo um serviço web ASP.NET na caixa de diálogo Olá de novo serviço][vs-new-service-dialog]

3. <span data-ttu-id="25010-124">próxima página de saudação fornece um conjunto de ASP.NET Core modelos de projeto.</span><span class="sxs-lookup"><span data-stu-id="25010-124">hello next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="25010-125">Observe que esses são Olá mesmo opções que você veria se você criou um projeto do ASP.NET Core fora de um aplicativo de malha do serviço, com uma pequena quantidade de código adicional tooregister Olá serviço com tempo de execução do Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="25010-125">Note that these are hello same choices that you would see if you created an ASP.NET Core project outside of a Service Fabric application, with a small amount of additional code tooregister hello service with hello Service Fabric runtime.</span></span> <span data-ttu-id="25010-126">Neste tutorial, escolhemos **API Web**.</span><span class="sxs-lookup"><span data-stu-id="25010-126">For this tutorial, choose **Web API**.</span></span> <span data-ttu-id="25010-127">No entanto, você pode aplicar Olá mesmo conceitos toobuilding um aplicativo web completo.</span><span class="sxs-lookup"><span data-stu-id="25010-127">However, you can apply hello same concepts toobuilding a full web application.</span></span>
   
    ![Escolhendo o tipo de projeto do ASP.NET][vs-new-aspnet-project-dialog]
   
    <span data-ttu-id="25010-129">Depois de criar o projeto de API Web, você deverá ter dois serviços no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="25010-129">Once your Web API project is created, you should have two services in your application.</span></span> <span data-ttu-id="25010-130">Enquanto você continua toobuild seu aplicativo, você pode adicionar mais serviços em exatamente Olá mesma maneira.</span><span class="sxs-lookup"><span data-stu-id="25010-130">As you continue toobuild your application, you can add more services in exactly hello same way.</span></span> <span data-ttu-id="25010-131">Cada um pode seu próprio controle de versão e ser atualizado de forma independente.</span><span class="sxs-lookup"><span data-stu-id="25010-131">Each can be independently versioned and upgraded.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="25010-132">Executar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="25010-132">Run hello application</span></span>
<span data-ttu-id="25010-133">tooget uma ideia do que já fizemos, vamos implantar Olá novo aplicativo e execute uma olhada no comportamento padrão Olá Olá modelo de API da Web do ASP.NET Core fornece.</span><span class="sxs-lookup"><span data-stu-id="25010-133">tooget a sense of what we've done, let's deploy hello new application and take a look at hello default behavior that hello ASP.NET Core Web API template provides.</span></span>

1. <span data-ttu-id="25010-134">Pressione F5 no Visual Studio toodebug Olá aplicativo.</span><span class="sxs-lookup"><span data-stu-id="25010-134">Press F5 in Visual Studio toodebug hello app.</span></span>
2. <span data-ttu-id="25010-135">Quando a implantação for concluída, o Visual Studio inicia raiz de toohello um navegador de saudação serviço de API da Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="25010-135">When deployment is complete, Visual Studio launches a browser toohello root of hello ASP.NET Web API service.</span></span> <span data-ttu-id="25010-136">modelo de API da Web do ASP.NET Core Olá não fornece o comportamento padrão raiz Olá, então você deve ver um erro 404 no navegador de saudação.</span><span class="sxs-lookup"><span data-stu-id="25010-136">hello ASP.NET Core Web API template doesn't provide default behavior for hello root, so you should see a 404 error in hello browser.</span></span>
3. <span data-ttu-id="25010-137">Adicionar `/api/values` toohello local no navegador de saudação.</span><span class="sxs-lookup"><span data-stu-id="25010-137">Add `/api/values` toohello location in hello browser.</span></span> <span data-ttu-id="25010-138">Isso chama Olá `Get` método hello ValuesController no modelo de API da Web hello.</span><span class="sxs-lookup"><span data-stu-id="25010-138">This invokes hello `Get` method on hello ValuesController in hello Web API template.</span></span> <span data-ttu-id="25010-139">Ele retorna a resposta padrão Olá fornecida pelo modelo hello – uma matriz JSON que contém duas cadeias de caracteres:</span><span class="sxs-lookup"><span data-stu-id="25010-139">It returns hello default response that is provided by hello template--a JSON array that contains two strings:</span></span>
   
    ![Valores padrão retornados do modelo de API Web do ASP.NET Core][browser-aspnet-template-values]
   
    <span data-ttu-id="25010-141">Por fim de saudação do tutorial do hello, essa página mostrará valor mais recente do contador de saudação de nosso serviço com monitoração de estado, em vez de saudação cadeias de caracteres padrão.</span><span class="sxs-lookup"><span data-stu-id="25010-141">By hello end of hello tutorial, this page will show hello most recent counter value from our stateful service instead of hello default strings.</span></span>

## <a name="connect-hello-services"></a><span data-ttu-id="25010-142">Conectar os serviços de saudação</span><span class="sxs-lookup"><span data-stu-id="25010-142">Connect hello services</span></span>
<span data-ttu-id="25010-143">O Service Fabric fornece total flexibilidade na comunicação com Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="25010-143">Service Fabric provides complete flexibility in how you communicate with reliable services.</span></span> <span data-ttu-id="25010-144">Em um único aplicativo, você pode ter serviços acessíveis por meio de TCP, outros serviços acessíveis por meio de uma API REST HTTP e ainda outros serviços que são acessíveis por meio de soquetes da Web.</span><span class="sxs-lookup"><span data-stu-id="25010-144">Within a single application, you might have services that are accessible via TCP, other services that are accessible via an HTTP REST API, and still other services that are accessible via web sockets.</span></span> <span data-ttu-id="25010-145">Para obter informações sobre opções de saudação disponíveis e compensações de saudação envolvidas, consulte [se comunicar com serviços](service-fabric-connect-and-communicate-with-services.md).</span><span class="sxs-lookup"><span data-stu-id="25010-145">For background on hello options available and hello tradeoffs involved, see [Communicating with services](service-fabric-connect-and-communicate-with-services.md).</span></span> <span data-ttu-id="25010-146">Neste tutorial, usamos [serviço de comunicação remota do serviço de malha](service-fabric-reliable-services-communication-remoting.md), fornecido no hello SDK.</span><span class="sxs-lookup"><span data-stu-id="25010-146">In this tutorial, we use [Service Fabric Service Remoting](service-fabric-reliable-services-communication-remoting.md), provided in hello SDK.</span></span>

<span data-ttu-id="25010-147">Olá abordagem de comunicação remota do serviço (modelada em chamadas de procedimento remoto ou RPCs), você definirá uma interface tooact como contrato público de Olá para o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="25010-147">In hello Service Remoting approach (modeled on remote procedure calls or RPCs), you define an interface tooact as hello public contract for hello service.</span></span> <span data-ttu-id="25010-148">Em seguida, você deve usar toogenerate essa interface uma classe proxy para interagir com o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="25010-148">Then, you use that interface toogenerate a proxy class for interacting with hello service.</span></span>

### <a name="create-hello-remoting-interface"></a><span data-ttu-id="25010-149">Criar interface de comunicação remota Olá</span><span class="sxs-lookup"><span data-stu-id="25010-149">Create hello remoting interface</span></span>
<span data-ttu-id="25010-150">Vamos começar criando Olá interface tooact como Olá contrato entre o serviço com monitoração de estado hello e outros serviços nesse caso Olá projeto da web de ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="25010-150">Let's start by creating hello interface tooact as hello contract between hello stateful service and other services, in this case hello ASP.NET Core web project.</span></span> <span data-ttu-id="25010-151">Esta interface deve ser compartilhada por todos os serviços que usam as chamadas RPC toomake, portanto, criaremos em seu próprio projeto de biblioteca de classes.</span><span class="sxs-lookup"><span data-stu-id="25010-151">This interface must be shared by all services that use it toomake RPC calls, so we'll create it in its own Class Library project.</span></span>

1. <span data-ttu-id="25010-152">No Gerenciador de Soluções, clique com o botão direito do mouse na solução e escolha **Adicione** > **Novo Projeto**.</span><span class="sxs-lookup"><span data-stu-id="25010-152">In Solution Explorer, right-click your solution and choose **Add** > **New Project**.</span></span>

2. <span data-ttu-id="25010-153">Escolha Olá **Visual C#** entrada hello esquerda do painel de navegação e, em seguida, selecione Olá **biblioteca de classes** modelo.</span><span class="sxs-lookup"><span data-stu-id="25010-153">Choose hello **Visual C#** entry in hello left navigation pane and then select hello **Class Library** template.</span></span> <span data-ttu-id="25010-154">Certifique-se de que essa versão do .NET Framework hello está definido muito**4.5.2**.</span><span class="sxs-lookup"><span data-stu-id="25010-154">Ensure that hello .NET Framework version is set too**4.5.2**.</span></span>
   
    ![Criando um projeto de interface para o serviço com estado][vs-add-class-library-project]

3. <span data-ttu-id="25010-156">Instalar Olá **Microsoft.ServiceFabric.Services.Remoting** pacote NuGet.</span><span class="sxs-lookup"><span data-stu-id="25010-156">Install hello **Microsoft.ServiceFabric.Services.Remoting** NuGet package.</span></span> <span data-ttu-id="25010-157">Procurar **Microsoft.ServiceFabric.Services.Remoting** em Olá NuGet Gerenciador de pacote e instalá-lo para todos os projetos na solução de saudação que usam a comunicação remota do serviço, incluindo:</span><span class="sxs-lookup"><span data-stu-id="25010-157">Search for  **Microsoft.ServiceFabric.Services.Remoting** in hello NuGet package manager and install it for all projects in hello solution that use Service Remoting, including:</span></span>
   - <span data-ttu-id="25010-158">projeto de biblioteca de classes Olá que contém a interface do serviço Olá</span><span class="sxs-lookup"><span data-stu-id="25010-158">hello Class Library project that contains hello service interface</span></span>
   - <span data-ttu-id="25010-159">projeto de serviço de monitoração de estado de saudação</span><span class="sxs-lookup"><span data-stu-id="25010-159">hello Stateful Service project</span></span>
   - <span data-ttu-id="25010-160">Olá projeto de serviço web ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="25010-160">hello ASP.NET Core web service project</span></span>
   
    ![Adicionar o pacote do NuGet serviços Olá][vs-services-nuget-package]

4. <span data-ttu-id="25010-162">Na biblioteca de classes do hello, criar uma interface com um único método, `GetCountAsync`, e estender a interface de saudação do `Microsoft.ServiceFabric.Services.Remoting.IService`.</span><span class="sxs-lookup"><span data-stu-id="25010-162">In hello class library, create an interface with a single method, `GetCountAsync`, and extend hello interface from `Microsoft.ServiceFabric.Services.Remoting.IService`.</span></span> <span data-ttu-id="25010-163">interface de comunicação remota Olá deve derivar de tooindicate essa interface que é uma interface de comunicação remota do serviço.</span><span class="sxs-lookup"><span data-stu-id="25010-163">hello remoting interface must derive from this interface tooindicate that it is a Service Remoting interface.</span></span>
   
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

### <a name="implement-hello-interface-in-your-stateful-service"></a><span data-ttu-id="25010-164">Implementar interface Olá em seu serviço com monitoração de estado</span><span class="sxs-lookup"><span data-stu-id="25010-164">Implement hello interface in your stateful service</span></span>
<span data-ttu-id="25010-165">Agora que definimos interface Olá, é necessário tooimplement-lo no serviço com monitoração de estado hello.</span><span class="sxs-lookup"><span data-stu-id="25010-165">Now that we have defined hello interface, we need tooimplement it in hello stateful service.</span></span>

1. <span data-ttu-id="25010-166">Em seu serviço com monitoração de estado, adicione um projeto de biblioteca de classe toohello de referência que contém a interface hello.</span><span class="sxs-lookup"><span data-stu-id="25010-166">In your stateful service, add a reference toohello class library project that contains hello interface.</span></span>
   
    ![Adicionando um projeto de biblioteca de classes de toohello de referência no serviço com monitoração de estado Olá][vs-add-class-library-reference]
2. <span data-ttu-id="25010-168">Localize Olá classe que herda de `StatefulService`, como `MyStatefulService`e estendê-lo Olá tooimplement `ICounter` interface.</span><span class="sxs-lookup"><span data-stu-id="25010-168">Locate hello class that inherits from `StatefulService`, such as `MyStatefulService`, and extend it tooimplement hello `ICounter` interface.</span></span>
   
    ```c#
    using MyStatefulService.Interface;
   
    ...
   
    public class MyStatefulService : StatefulService, ICounter
    {        
         ...
    }
    ```
3. <span data-ttu-id="25010-169">Agora implementar Olá único método que é definido em Olá `ICounter` interface `GetCountAsync`.</span><span class="sxs-lookup"><span data-stu-id="25010-169">Now implement hello single method that is defined in hello `ICounter` interface, `GetCountAsync`.</span></span>
   
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

### <a name="expose-hello-stateful-service-using-a-service-remoting-listener"></a><span data-ttu-id="25010-170">Expor Olá serviço com monitoração de estado usando um ouvinte de comunicação remota do serviço</span><span class="sxs-lookup"><span data-stu-id="25010-170">Expose hello stateful service using a service remoting listener</span></span>
<span data-ttu-id="25010-171">Com hello `ICounter` interface implementada, a etapa final Olá é o canal de comunicação tooopen Olá comunicação remota do serviço.</span><span class="sxs-lookup"><span data-stu-id="25010-171">With hello `ICounter` interface implemented, hello final step is tooopen hello Service Remoting communication channel.</span></span> <span data-ttu-id="25010-172">Para serviços com estado, o Service Fabric fornece um método substituível chamado `CreateServiceReplicaListeners`.</span><span class="sxs-lookup"><span data-stu-id="25010-172">For stateful services, Service Fabric provides an overridable method called `CreateServiceReplicaListeners`.</span></span> <span data-ttu-id="25010-173">Com esse método, você pode especificar um ou mais ouvintes de comunicação, com base no tipo de saudação de comunicação que você deseja tooenable para seu serviço.</span><span class="sxs-lookup"><span data-stu-id="25010-173">With this method, you can specify one or more communication listeners, based on hello type of communication that you want tooenable for your service.</span></span>

> [!NOTE]
> <span data-ttu-id="25010-174">método equivalente Hello para abertura de um serviço de toostateless de canal de comunicação é chamado `CreateServiceInstanceListeners`.</span><span class="sxs-lookup"><span data-stu-id="25010-174">hello equivalent method for opening a communication channel toostateless services is called `CreateServiceInstanceListeners`.</span></span>

<span data-ttu-id="25010-175">Nesse caso, podemos substituir Olá `CreateServiceReplicaListeners` método e fornecer uma instância de `ServiceRemotingListener`, que cria um ponto de extremidade RPC que é chamado de clientes por meio de `ServiceProxy`.</span><span class="sxs-lookup"><span data-stu-id="25010-175">In this case, we replace hello existing `CreateServiceReplicaListeners` method and provide an instance of `ServiceRemotingListener`, which creates an RPC endpoint that is callable from clients through `ServiceProxy`.</span></span>  

<span data-ttu-id="25010-176">Olá `CreateServiceRemotingListener` método de extensão no hello `IService` interface permite que você tooeasily criar um `ServiceRemotingListener` com todas as configurações padrão.</span><span class="sxs-lookup"><span data-stu-id="25010-176">hello `CreateServiceRemotingListener` extension method on hello `IService` interface allows you tooeasily create a `ServiceRemotingListener` with all default settings.</span></span> <span data-ttu-id="25010-177">toouse esse método de extensão, certifique-se de ter Olá `Microsoft.ServiceFabric.Services.Remoting.Runtime` namespace importado.</span><span class="sxs-lookup"><span data-stu-id="25010-177">toouse this extension method, ensure you have hello `Microsoft.ServiceFabric.Services.Remoting.Runtime` namespace imported.</span></span> 

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


### <a name="use-hello-serviceproxy-class-toointeract-with-hello-service"></a><span data-ttu-id="25010-178">Use Olá ServiceProxy classe toointeract com o serviço de saudação</span><span class="sxs-lookup"><span data-stu-id="25010-178">Use hello ServiceProxy class toointeract with hello service</span></span>
<span data-ttu-id="25010-179">Nosso serviço com monitoração de estado está agora pronto tooreceive tráfego de outros serviços RPC.</span><span class="sxs-lookup"><span data-stu-id="25010-179">Our stateful service is now ready tooreceive traffic from other services over RPC.</span></span> <span data-ttu-id="25010-180">Portanto tudo o que permanece é adicionando Olá código toocommunicate com ele da saudação serviço web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="25010-180">So all that remains is adding hello code toocommunicate with it from hello ASP.NET web service.</span></span>

1. <span data-ttu-id="25010-181">No seu projeto do ASP.NET, adicionar uma biblioteca de classes de toohello de referência que contém Olá `ICounter` interface.</span><span class="sxs-lookup"><span data-stu-id="25010-181">In your ASP.NET project, add a reference toohello class library that contains hello `ICounter` interface.</span></span>

2. <span data-ttu-id="25010-182">Anteriormente você adicionou Olá **Microsoft.ServiceFabric.Services.Remoting** NuGet pacote toohello ASP.NET projeto.</span><span class="sxs-lookup"><span data-stu-id="25010-182">Earlier you added hello **Microsoft.ServiceFabric.Services.Remoting** NuGet package toohello ASP.NET project.</span></span> <span data-ttu-id="25010-183">Esse pacote fornece Olá `ServiceProxy` classe que você use toomake RPC chama o serviço de monitoração de estado de toohello.</span><span class="sxs-lookup"><span data-stu-id="25010-183">This package provides hello `ServiceProxy` class which you use toomake RPC calls toohello stateful service.</span></span> <span data-ttu-id="25010-184">Certifique-se de que instalar o pacote de NuGet em Olá projeto de serviço web ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="25010-184">Ensure this NuGet package is installed in hello ASP.NET Core web service project.</span></span>

4. <span data-ttu-id="25010-185">Em Olá **controladores** pasta, abra Olá `ValuesController` classe.</span><span class="sxs-lookup"><span data-stu-id="25010-185">In hello **Controllers** folder, open hello `ValuesController` class.</span></span> <span data-ttu-id="25010-186">Observe que Olá `Get` método atualmente apenas retorna uma matriz de cadeia de caracteres codificada de "value1" e "value2" – que coincide com o que vimos anteriormente no navegador de saudação.</span><span class="sxs-lookup"><span data-stu-id="25010-186">Note that hello `Get` method currently just returns a hard-coded string array of "value1" and "value2"--which matches what we saw earlier in hello browser.</span></span> <span data-ttu-id="25010-187">Substitua esta implementação Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="25010-187">Replace this implementation with hello following code:</span></span>
   
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
   
    <span data-ttu-id="25010-188">Olá primeira linha de código é chave Olá um.</span><span class="sxs-lookup"><span data-stu-id="25010-188">hello first line of code is hello key one.</span></span> <span data-ttu-id="25010-189">toocreate Olá ICounter serviço proxy de toohello com monitoração de estado, você precisa tooprovide duas informações: um nome de identificação e hello de partição do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="25010-189">toocreate hello ICounter proxy toohello stateful service, you need tooprovide two pieces of information: a partition ID and hello name of hello service.</span></span>
   
    <span data-ttu-id="25010-190">Você pode usar serviços com monitoração de estado do particionamento tooscale dividindo seu estado em diferentes segmentos, com base em uma chave que você define, como uma ID de cliente ou código postal.</span><span class="sxs-lookup"><span data-stu-id="25010-190">You can use partitioning tooscale stateful services by breaking up their state into different buckets, based on a key that you define, such as a customer ID or postal code.</span></span> <span data-ttu-id="25010-191">Em nosso aplicativo trivial, serviço com monitoração de estado Olá tem apenas uma partição, portanto chave Olá não importa.</span><span class="sxs-lookup"><span data-stu-id="25010-191">In our trivial application, hello stateful service only has one partition, so hello key doesn't matter.</span></span> <span data-ttu-id="25010-192">Qualquer chave que você fornecer levará toohello mesma partição.</span><span class="sxs-lookup"><span data-stu-id="25010-192">Any key that you provide will lead toohello same partition.</span></span> <span data-ttu-id="25010-193">toolearn mais sobre o particionamento de serviços, consulte [como toopartition serviços confiável do serviço do Fabric](service-fabric-concepts-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="25010-193">toolearn more about partitioning services, see [How toopartition Service Fabric Reliable Services](service-fabric-concepts-partitioning.md).</span></span>
   
    <span data-ttu-id="25010-194">nome do serviço Olá é um URI de malha de formulário Olá: /&lt;application_name&gt;/&lt;service_name&gt;.</span><span class="sxs-lookup"><span data-stu-id="25010-194">hello service name is a URI of hello form fabric:/&lt;application_name&gt;/&lt;service_name&gt;.</span></span>
   
    <span data-ttu-id="25010-195">Com esses dois tipos de informações, o Service Fabric pode identificar exclusivamente máquina Olá que solicitações devem ser enviadas para.</span><span class="sxs-lookup"><span data-stu-id="25010-195">With these two pieces of information, Service Fabric can uniquely identify hello machine that requests should be sent to.</span></span> <span data-ttu-id="25010-196">Olá `ServiceProxy` classe também perfeitamente manipula caso Olá onde Olá máquina que hospeda a partição de serviço com monitoração de estado de saudação falhar e outra máquina deve ser promovido tootake seu lugar.</span><span class="sxs-lookup"><span data-stu-id="25010-196">hello `ServiceProxy` class also seamlessly handles hello case where hello machine that hosts hello stateful service partition fails and another machine must be promoted tootake its place.</span></span> <span data-ttu-id="25010-197">Essa abstração torna a gravação Olá toodeal de código de cliente com outros serviços muito mais simples.</span><span class="sxs-lookup"><span data-stu-id="25010-197">This abstraction makes writing hello client code toodeal with other services significantly simpler.</span></span>
   
    <span data-ttu-id="25010-198">Assim que tivermos proxy Olá, podemos simplesmente chamar Olá `GetCountAsync` método e retorna seu resultado.</span><span class="sxs-lookup"><span data-stu-id="25010-198">Once we have hello proxy, we simply invoke hello `GetCountAsync` method and return its result.</span></span>

5. <span data-ttu-id="25010-199">Pressione F5 novamente toorun Olá modificou o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="25010-199">Press F5 again toorun hello modified application.</span></span> <span data-ttu-id="25010-200">Como antes, o Visual Studio automaticamente inicia raiz de toohello de navegador de saudação do projeto da web de saudação.</span><span class="sxs-lookup"><span data-stu-id="25010-200">As before, Visual Studio automatically launches hello browser toohello root of hello web project.</span></span> <span data-ttu-id="25010-201">Adicionar caminho de "api/valores" Olá, e você verá o valor de contador atual Olá retornado.</span><span class="sxs-lookup"><span data-stu-id="25010-201">Add hello "api/values" path, and you should see hello current counter value returned.</span></span>
   
    ![valor do contador com monitoração de estado de saudação exibida no navegador Olá][browser-aspnet-counter-value]
   
    <span data-ttu-id="25010-203">Atualize o navegador de saudação periodicamente toosee Olá contador valor atualização.</span><span class="sxs-lookup"><span data-stu-id="25010-203">Refresh hello browser periodically toosee hello counter value update.</span></span>

## <a name="kestrel-and-weblistener"></a><span data-ttu-id="25010-204">Kestrel e WebListener</span><span class="sxs-lookup"><span data-stu-id="25010-204">Kestrel and WebListener</span></span>

<span data-ttu-id="25010-205">Olá padrão ASP.NET web server Core, conhecido como Kestrel, for [atualmente não há suporte para o tratamento do tráfego de internet direto](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel).</span><span class="sxs-lookup"><span data-stu-id="25010-205">hello default ASP.NET Core web server, known as Kestrel, is [not currently supported for handling direct internet traffic](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel).</span></span> <span data-ttu-id="25010-206">Como resultado, hello modelo de serviço sem monitoração de estado do ASP.NET Core para Service Fabric usa [WebListener](https://docs.microsoft.com/aspnet/core/fundamentals/servers/weblistener) por padrão.</span><span class="sxs-lookup"><span data-stu-id="25010-206">As a result, hello ASP.NET Core stateless service template for Service Fabric uses [WebListener](https://docs.microsoft.com/aspnet/core/fundamentals/servers/weblistener) by default.</span></span> 

<span data-ttu-id="25010-207">toolearn mais sobre Kestrel e WebListener em serviços do Service Fabric, consulte muito[ASP.NET Core em serviços confiável do serviço do Fabric](service-fabric-reliable-services-communication-aspnetcore.md).</span><span class="sxs-lookup"><span data-stu-id="25010-207">toolearn more about Kestrel and WebListener in Service Fabric services, please refer too[ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md).</span></span>

## <a name="connecting-tooa-reliable-actor-service"></a><span data-ttu-id="25010-208">Conectar-se o serviço de Reliable Actor tooa</span><span class="sxs-lookup"><span data-stu-id="25010-208">Connecting tooa Reliable Actor service</span></span>
<span data-ttu-id="25010-209">Este tutorial se concentra em adicionar um front-end da Web que se comunique com um serviço com estado.</span><span class="sxs-lookup"><span data-stu-id="25010-209">This tutorial focused on adding a web front end that communicated with a stateful service.</span></span> <span data-ttu-id="25010-210">No entanto, você pode seguir um tooactors de tootalk modelo muito semelhantes.</span><span class="sxs-lookup"><span data-stu-id="25010-210">However, you can follow a very similar model tootalk tooactors.</span></span> <span data-ttu-id="25010-211">Quando você cria um projeto do Reliable Actor, o Visual Studio gera automaticamente um projeto de interface para você.</span><span class="sxs-lookup"><span data-stu-id="25010-211">When you create a Reliable Actor project, Visual Studio automatically generates an interface project for you.</span></span> <span data-ttu-id="25010-212">Você pode usar esse toogenerate interface um proxy de ator em Olá web projeto toocommunicate com ator hello.</span><span class="sxs-lookup"><span data-stu-id="25010-212">You can use that interface toogenerate an actor proxy in hello web project toocommunicate with hello actor.</span></span> <span data-ttu-id="25010-213">o canal de comunicação Olá é fornecido automaticamente.</span><span class="sxs-lookup"><span data-stu-id="25010-213">hello communication channel is provided automatically.</span></span> <span data-ttu-id="25010-214">Portanto, você não precisa toodo qualquer coisa que é equivalente tooestablishing um `ServiceRemotingListener` como você fez para o serviço com monitoração de estado Olá neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="25010-214">So you do not need toodo anything that is equivalent tooestablishing a `ServiceRemotingListener` like you did for hello stateful service in this tutorial.</span></span>

## <a name="how-web-services-work-on-your-local-cluster"></a><span data-ttu-id="25010-215">Como os serviços Web funcionam no cluster local</span><span class="sxs-lookup"><span data-stu-id="25010-215">How web services work on your local cluster</span></span>
<span data-ttu-id="25010-216">Em geral, você pode implantar exatamente Olá mesmo do Service Fabric application tooa com vários computadores de cluster que você implantou no cluster local e estar altamente seguro de que ele funciona conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="25010-216">In general, you can deploy exactly hello same Service Fabric application tooa multi-machine cluster that you deployed on your local cluster and be highly confident that it works as you expect.</span></span> <span data-ttu-id="25010-217">Isso ocorre porque o cluster local é simplesmente uma configuração de cinco nós que é recolhida tooa único computador.</span><span class="sxs-lookup"><span data-stu-id="25010-217">This is because your local cluster is simply a five-node configuration that is collapsed tooa single machine.</span></span>

<span data-ttu-id="25010-218">No entanto, quando se trata de tooweb serviços, há um nuance chave.</span><span class="sxs-lookup"><span data-stu-id="25010-218">When it comes tooweb services, however, there is one key nuance.</span></span> <span data-ttu-id="25010-219">Quando o cluster fica atrás de um balanceador de carga, como faz no Azure, você deve garantir que os serviços web são implantados em todos os computadores desde o balanceador de carga Olá simplesmente alternadas tráfego entre máquinas hello.</span><span class="sxs-lookup"><span data-stu-id="25010-219">When your cluster sits behind a load balancer, as it does in Azure, you must ensure that your web services are deployed on every machine since hello load balancer simply round-robins traffic across hello machines.</span></span> <span data-ttu-id="25010-220">Você pode fazer isso definindo Olá `InstanceCount` para valor especial de toohello do serviço de saudação de "-1".</span><span class="sxs-lookup"><span data-stu-id="25010-220">You can do this by setting hello `InstanceCount` for hello service toohello special value of "-1".</span></span>

<span data-ttu-id="25010-221">Por outro lado, quando você executa um serviço web localmente, você precisa tooensure que apenas uma instância do serviço de saudação está em execução.</span><span class="sxs-lookup"><span data-stu-id="25010-221">By contrast, when you run a web service locally, you need tooensure that only one instance of hello service is running.</span></span> <span data-ttu-id="25010-222">Caso contrário, execute em conflitos de vários processos que estão escutando Olá mesmo caminho e a porta.</span><span class="sxs-lookup"><span data-stu-id="25010-222">Otherwise, you run into conflicts from multiple processes that are listening on hello same path and port.</span></span> <span data-ttu-id="25010-223">Como resultado, contagem de instâncias de serviço Olá web deve ser definida muito "1" para implantações de locais.</span><span class="sxs-lookup"><span data-stu-id="25010-223">As a result, hello web service instance count should be set too"1" for local deployments.</span></span>

<span data-ttu-id="25010-224">toolearn como valores diferentes de tooconfigure para outro ambiente, consulte [gerenciar parâmetros do aplicativo para vários ambientes](service-fabric-manage-multiple-environment-app-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="25010-224">toolearn how tooconfigure different values for different environment, see [Managing application parameters for multiple environments](service-fabric-manage-multiple-environment-app-configuration.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="25010-225">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="25010-225">Next steps</span></span>
<span data-ttu-id="25010-226">Agora que você tem um front-end da Web configurado para o aplicativo com o ASP.NET Core, saiba mais sobre o [ASP.NET Core nos Reliable Services do Service Fabric](service-fabric-reliable-services-communication-aspnetcore.md) para obter uma compreensão detalhada de como o ASP.NET Core funciona com o Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="25010-226">Now that you have a web front end set up for your application with ASP.NET Core, learn more about [ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md) for an in-depth understanding of how ASP.NET Core works with Service Fabric.</span></span>

<span data-ttu-id="25010-227">Em seguida, [saber mais sobre a comunicação com serviços](service-fabric-connect-and-communicate-with-services.md) em geral tooget a conclusão de imagem do serviço como a comunicação funciona na malha do serviço.</span><span class="sxs-lookup"><span data-stu-id="25010-227">Next, [learn more about communicating with services](service-fabric-connect-and-communicate-with-services.md) in general tooget a complete picture of how service communication works in Service Fabric.</span></span>

<span data-ttu-id="25010-228">Depois de você ter um bom entendimento de como funciona a comunicação de serviço, [criar um cluster no Azure e implantar sua nuvem de toohello aplicativo](service-fabric-cluster-creation-via-portal.md).</span><span class="sxs-lookup"><span data-stu-id="25010-228">Once you have a good understanding of how service communication works, [create a cluster in Azure and deploy your application toohello cloud](service-fabric-cluster-creation-via-portal.md).</span></span>

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
