---
title: "aaaGet iniciado com retransmissões do WCF de retransmissão do Azure no .NET | Microsoft Docs"
description: "Saiba como toouse Azure retransmissão WCF retransmite tooconnect dois aplicativos hospedados em diferentes locais."
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 5493281a-c2e5-49f2-87ee-9d3ffb782c75
ms.service: service-bus-relay
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: a652617fc2e9b7c8d62d39fa914f77df6e3a1771
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-relay-wcf-relays-with-net"></a><span data-ttu-id="fa67a-103">Como toouse Azure retransmissão WCF retransmissões com .NET</span><span class="sxs-lookup"><span data-stu-id="fa67a-103">How toouse Azure Relay WCF relays with .NET</span></span>
<span data-ttu-id="fa67a-104">Este artigo descreve como toouse Olá serviço de retransmissão do Azure.</span><span class="sxs-lookup"><span data-stu-id="fa67a-104">This article describes how toouse hello Azure Relay service.</span></span> <span data-ttu-id="fa67a-105">exemplos de Olá são escritos em c# e usam o API do Windows Communication Foundation (WCF) Olá com extensões contidas Olá assembly do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="fa67a-105">hello samples are written in C# and use hello Windows Communication Foundation (WCF) API with extensions contained in hello Service Bus assembly.</span></span> <span data-ttu-id="fa67a-106">Para obter mais informações sobre a retransmissão do Azure, consulte Olá [visão geral do Azure retransmissão](relay-what-is-it.md).</span><span class="sxs-lookup"><span data-stu-id="fa67a-106">For more information about Azure relay, see hello [Azure Relay overview](relay-what-is-it.md).</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="what-is-wcf-relay"></a><span data-ttu-id="fa67a-107">O que é Retransmissão do WCF?</span><span class="sxs-lookup"><span data-stu-id="fa67a-107">What is WCF Relay?</span></span>

<span data-ttu-id="fa67a-108">Hello Azure [ *retransmissão WCF* ](relay-what-is-it.md) serviço permite que aplicativos híbridos toobuild que são executados em um datacenter do Azure e seu próprio ambiente de empresa local.</span><span class="sxs-lookup"><span data-stu-id="fa67a-108">hello Azure [*WCF Relay*](relay-what-is-it.md) service enables you toobuild hybrid applications that run in both an Azure datacenter and your own on-premises enterprise environment.</span></span> <span data-ttu-id="fa67a-109">serviço de retransmissão Olá facilita isso, permitindo que você toosecurely expor serviços Windows Communication Foundation (WCF) que residem dentro de uma empresa corporativa rede toohello nuvem pública, sem tooopen uma conexão do firewall, ou exigindo infraestrutura de rede corporativa tooa alterações intrusiva.</span><span class="sxs-lookup"><span data-stu-id="fa67a-109">hello relay service facilitates this by enabling you toosecurely expose Windows Communication Foundation (WCF) services that reside within a corporate enterprise network toohello public cloud, without having tooopen a firewall connection, or requiring intrusive changes tooa corporate network infrastructure.</span></span>

![Conceitos de retransmissão do WCF](./media/service-bus-dotnet-how-to-use-relay/sb-relay-01.png)

<span data-ttu-id="fa67a-111">Retransmissão do Azure permite que você toohost os serviços WCF em seu ambiente empresarial existente.</span><span class="sxs-lookup"><span data-stu-id="fa67a-111">Azure Relay enables you toohost WCF services within your existing enterprise environment.</span></span> <span data-ttu-id="fa67a-112">Em seguida, você pode delegar aguardando entrada sessões e solicitações toothese WCF toohello retransmissão serviços estão em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="fa67a-112">You can then delegate listening for incoming sessions and requests toothese WCF services toohello relay service running within Azure.</span></span> <span data-ttu-id="fa67a-113">Isso permite que você tooexpose esses serviços tooapplication o código em execução no Azure, ou operadores toomobile ou ambientes de extranet do parceiro.</span><span class="sxs-lookup"><span data-stu-id="fa67a-113">This enables you tooexpose these services tooapplication code running in Azure, or toomobile workers or extranet partner environments.</span></span> <span data-ttu-id="fa67a-114">Retransmissão permite que você controle toosecurely quem pode acessar esses serviços em um nível granular.</span><span class="sxs-lookup"><span data-stu-id="fa67a-114">Relay enables you toosecurely control who can access these services at a fine-grained level.</span></span> <span data-ttu-id="fa67a-115">Ele fornece uma funcionalidade do aplicativo de maneira segura e eficiente tooexpose e dados de suas soluções empresariais existentes e tirar proveito da nuvem de saudação.</span><span class="sxs-lookup"><span data-stu-id="fa67a-115">It provides a powerful and secure way tooexpose application functionality and data from your existing enterprise solutions and take advantage of it from hello cloud.</span></span>

<span data-ttu-id="fa67a-116">Este artigo aborda como toouse Azure retransmissão toocreate um serviço web WCF, exposta usando uma associação de canal TCP, que implementa uma conversa segura entre duas partes.</span><span class="sxs-lookup"><span data-stu-id="fa67a-116">This article discusses how toouse Azure Relay toocreate a WCF web service, exposed using a TCP channel binding, that implements a secure conversation between two parties.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="get-hello-service-bus-nuget-package"></a><span data-ttu-id="fa67a-117">Obter o pacote do NuGet do barramento de serviço Olá</span><span class="sxs-lookup"><span data-stu-id="fa67a-117">Get hello Service Bus NuGet package</span></span>
<span data-ttu-id="fa67a-118">Olá [pacote NuGet do barramento de serviço](https://www.nuget.org/packages/WindowsAzure.ServiceBus) é Olá mais fácil maneira tooget Olá API do barramento de serviço e tooconfigure seu aplicativo com todas as dependências de barramento de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="fa67a-118">hello [Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus) is hello easiest way tooget hello Service Bus API and tooconfigure your application with all of hello Service Bus dependencies.</span></span> <span data-ttu-id="fa67a-119">pacote do NuGet Olá tooinstall em seu projeto, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="fa67a-119">tooinstall hello NuGet package in your project, do hello following:</span></span>

1. <span data-ttu-id="fa67a-120">No Gerenciador de Soluções, clique com o botão direito do mouse em **Referências** e clique em **Gerenciar Pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="fa67a-120">In Solution Explorer, right-click **References**, then click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="fa67a-121">Pesquisa por "Service Bus" e selecione Olá **barramento de serviço do Microsoft Azure** item.</span><span class="sxs-lookup"><span data-stu-id="fa67a-121">Search for "Service Bus" and select hello **Microsoft Azure Service Bus** item.</span></span> <span data-ttu-id="fa67a-122">Clique em **instalar** toocomplete Olá instalação e feche o hello caixa de diálogo a seguir:</span><span class="sxs-lookup"><span data-stu-id="fa67a-122">Click **Install** toocomplete hello installation, then close hello following dialog box:</span></span>
   
   ![](./media/service-bus-dotnet-how-to-use-relay/getting-started-multi-tier-13.png)

## <a name="expose-and-consume-a-soap-web-service-with-tcp"></a><span data-ttu-id="fa67a-123">Exponha e consuma um serviço Web SOAP com TCP</span><span class="sxs-lookup"><span data-stu-id="fa67a-123">Expose and consume a SOAP web service with TCP</span></span>
<span data-ttu-id="fa67a-124">tooexpose um serviço web de WCF SOAP existente para consumo externo, você deve fazer alterações toohello as associações de serviço e endereços.</span><span class="sxs-lookup"><span data-stu-id="fa67a-124">tooexpose an existing WCF SOAP web service for external consumption, you must make changes toohello service bindings and addresses.</span></span> <span data-ttu-id="fa67a-125">Isso pode exigir o arquivo de configuração tooyour alterações ou pode exigir alterações de código, dependendo de como você ter instalado e configurado seus serviços WCF.</span><span class="sxs-lookup"><span data-stu-id="fa67a-125">This may require changes tooyour configuration file or it could require code changes, depending on how you have set up and configured your WCF services.</span></span> <span data-ttu-id="fa67a-126">Observe que o WCF permite toohave vários pontos de extremidade de rede sobre Olá mesmo serviço, para que você possa reter Olá existente pontos de extremidade internos durante a adição de pontos de extremidade de retransmissão para uso externo acessarem Olá mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="fa67a-126">Note that WCF allows you toohave multiple network endpoints over hello same service, so you can retain hello existing internal endpoints while adding relay endpoints for external access at hello same time.</span></span>

<span data-ttu-id="fa67a-127">Nesta tarefa, você cria um serviço WCF simples e adicionar um tooit de ouvinte de retransmissão.</span><span class="sxs-lookup"><span data-stu-id="fa67a-127">In this task, you build a simple WCF service and add a relay listener tooit.</span></span> <span data-ttu-id="fa67a-128">Este exercício presume familiaridade com o Visual Studio e, portanto, não percorrer todos os detalhes de saudação de criação de um projeto.</span><span class="sxs-lookup"><span data-stu-id="fa67a-128">This exercise assumes some familiarity with Visual Studio, and therefore does not walk through all hello details of creating a project.</span></span> <span data-ttu-id="fa67a-129">Em vez disso, ele se concentra em código hello.</span><span class="sxs-lookup"><span data-stu-id="fa67a-129">Instead, it focuses on hello code.</span></span>

<span data-ttu-id="fa67a-130">Antes de iniciar essas etapas, conclua Olá procedimento tooset seu ambiente a seguir:</span><span class="sxs-lookup"><span data-stu-id="fa67a-130">Before starting these steps, complete hello following procedure tooset up your environment:</span></span>

1. <span data-ttu-id="fa67a-131">No Visual Studio, crie um aplicativo de console que contém dois projetos, "Cliente" e "Serviço", na solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="fa67a-131">Within Visual Studio, create a console application that contains two projects, "Client" and "Service", within hello solution.</span></span>
2. <span data-ttu-id="fa67a-132">Adicione Olá NuGet do Service Bus pacote tooboth projetos.</span><span class="sxs-lookup"><span data-stu-id="fa67a-132">Add hello Service Bus NuGet package tooboth projects.</span></span> <span data-ttu-id="fa67a-133">Esse pacote adiciona todos os projetos de tooyour Olá assembly necessárias referências.</span><span class="sxs-lookup"><span data-stu-id="fa67a-133">This package adds all hello necessary assembly references tooyour projects.</span></span>

### <a name="how-toocreate-hello-service"></a><span data-ttu-id="fa67a-134">Como toocreate Olá serviço</span><span class="sxs-lookup"><span data-stu-id="fa67a-134">How toocreate hello service</span></span>
<span data-ttu-id="fa67a-135">Primeiro, crie o próprio serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="fa67a-135">First, create hello service itself.</span></span> <span data-ttu-id="fa67a-136">Qualquer serviço WCF consiste em pelo menos três partes distintas:</span><span class="sxs-lookup"><span data-stu-id="fa67a-136">Any WCF service consists of at least three distinct parts:</span></span>

* <span data-ttu-id="fa67a-137">Definição de um contrato que descreve quais mensagens são trocadas e quais operações são toobe invocado.</span><span class="sxs-lookup"><span data-stu-id="fa67a-137">Definition of a contract that describes what messages are exchanged and what operations are toobe invoked.</span></span>
* <span data-ttu-id="fa67a-138">Implementação do contrato.</span><span class="sxs-lookup"><span data-stu-id="fa67a-138">Implementation of that contract.</span></span>
* <span data-ttu-id="fa67a-139">Host que hospeda o serviço do WCF hello e expõe vários pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="fa67a-139">Host that hosts hello WCF service and exposes several endpoints.</span></span>

<span data-ttu-id="fa67a-140">exemplos de código Olá nesta seção abordam cada um desses componentes.</span><span class="sxs-lookup"><span data-stu-id="fa67a-140">hello code examples in this section address each of these components.</span></span>

<span data-ttu-id="fa67a-141">contrato de saudação define uma única operação, `AddNumbers`, que adiciona dois números e retorna o resultado de saudação.</span><span class="sxs-lookup"><span data-stu-id="fa67a-141">hello contract defines a single operation, `AddNumbers`, that adds two numbers and returns hello result.</span></span> <span data-ttu-id="fa67a-142">Olá `IProblemSolverChannel` interface habilita Olá cliente toomore gerenciar facilmente o tempo de vida de proxy de saudação.</span><span class="sxs-lookup"><span data-stu-id="fa67a-142">hello `IProblemSolverChannel` interface enables hello client toomore easily manage hello proxy lifetime.</span></span> <span data-ttu-id="fa67a-143">A criação dessa interface é considerada uma prática recomendada.</span><span class="sxs-lookup"><span data-stu-id="fa67a-143">Creating such an interface is considered a best practice.</span></span> <span data-ttu-id="fa67a-144">É uma boa ideia tooput essa definição em um arquivo separado do contrato para que você pode fazer referência a esse arquivo de projetos "Cliente" e "Serviço", mas você também pode copiar o código de saudação em ambos os projetos.</span><span class="sxs-lookup"><span data-stu-id="fa67a-144">It's a good idea tooput this contract definition into a separate file so that you can reference that file from both your "Client" and "Service" projects, but you can also copy hello code into both projects.</span></span>

```csharp
using System.ServiceModel;

[ServiceContract(Namespace = "urn:ps")]
interface IProblemSolver
{
    [OperationContract]
    int AddNumbers(int a, int b);
}

interface IProblemSolverChannel : IProblemSolver, IClientChannel {}
```

<span data-ttu-id="fa67a-145">Com o contrato de saudação em vigor, implementação Olá é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="fa67a-145">With hello contract in place, hello implementation is as follows:</span></span>

```csharp
class ProblemSolver : IProblemSolver
{
    public int AddNumbers(int a, int b)
    {
        return a + b;
    }
}
```

### <a name="configure-a-service-host-programmatically"></a><span data-ttu-id="fa67a-146">Configure um host de serviço de forma programática</span><span class="sxs-lookup"><span data-stu-id="fa67a-146">Configure a service host programmatically</span></span>
<span data-ttu-id="fa67a-147">Com o contrato de saudação e a implementação no lugar, agora você pode hospedar o serviço hello.</span><span class="sxs-lookup"><span data-stu-id="fa67a-147">With hello contract and implementation in place, you can now host hello service.</span></span> <span data-ttu-id="fa67a-148">Hospedagem ocorre dentro de um [ServiceHost](https://msdn.microsoft.com/library/system.servicemodel.servicehost.aspx) object, que cuida do gerenciamento de instâncias de serviço hello e hosts Olá pontos de extremidade que escutam as mensagens.</span><span class="sxs-lookup"><span data-stu-id="fa67a-148">Hosting occurs inside a [System.ServiceModel.ServiceHost](https://msdn.microsoft.com/library/system.servicemodel.servicehost.aspx) object, which takes care of managing instances of hello service and hosts hello endpoints that listen for messages.</span></span> <span data-ttu-id="fa67a-149">Hello código a seguir configura o serviço de saudação com um ponto de extremidade local regular e uma aparência de saudação de tooillustrate de ponto de extremidade retransmissão lado a lado dos pontos de extremidade internos e externos.</span><span class="sxs-lookup"><span data-stu-id="fa67a-149">hello following code configures hello service with both a regular local endpoint and a relay endpoint tooillustrate hello appearance, side by side, of internal and external endpoints.</span></span> <span data-ttu-id="fa67a-150">Substitua a cadeia de caracteres hello *namespace* com o nome do namespace e *yourKey* com a chave SAS Olá que você obteve na etapa de instalação anterior hello.</span><span class="sxs-lookup"><span data-stu-id="fa67a-150">Replace hello string *namespace* with your namespace name and *yourKey* with hello SAS key that you obtained in hello previous setup step.</span></span>

```csharp
ServiceHost sh = new ServiceHost(typeof(ProblemSolver));

sh.AddServiceEndpoint(
   typeof (IProblemSolver), new NetTcpBinding(),
   "net.tcp://localhost:9358/solver");

sh.AddServiceEndpoint(
   typeof(IProblemSolver), new NetTcpRelayBinding(),
   ServiceBusEnvironment.CreateServiceUri("sb", "namespace", "solver"))
    .Behaviors.Add(new TransportClientEndpointBehavior {
          TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", "<yourKey>")});

sh.Open();

Console.WriteLine("Press ENTER tooclose");
Console.ReadLine();

sh.Close();
```

<span data-ttu-id="fa67a-151">Exemplo hello, você criará dois pontos de extremidade que estão em Olá mesmo contrato de implementação.</span><span class="sxs-lookup"><span data-stu-id="fa67a-151">In hello example, you create two endpoints that are on hello same contract implementation.</span></span> <span data-ttu-id="fa67a-152">Um é local e o outro é projetado por meio da Retransmissão do Azure.</span><span class="sxs-lookup"><span data-stu-id="fa67a-152">One is local and one is projected through Azure Relay.</span></span> <span data-ttu-id="fa67a-153">Olá principais diferenças entre eles são associações de saudação; [NetTcpBinding](https://msdn.microsoft.com/library/system.servicemodel.nettcpbinding.aspx) para um local de saudação e [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding#microsoft_servicebus_nettcprelaybinding) para o ponto de extremidade de retransmissão hello e endereços de saudação.</span><span class="sxs-lookup"><span data-stu-id="fa67a-153">hello key differences between them are hello bindings; [NetTcpBinding](https://msdn.microsoft.com/library/system.servicemodel.nettcpbinding.aspx) for hello local one and [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding#microsoft_servicebus_nettcprelaybinding) for hello relay endpoint and hello addresses.</span></span> <span data-ttu-id="fa67a-154">ponto de extremidade local Olá tem um endereço de rede local com uma porta distinto.</span><span class="sxs-lookup"><span data-stu-id="fa67a-154">hello local endpoint has a local network address with a distinct port.</span></span> <span data-ttu-id="fa67a-155">ponto de extremidade de retransmissão Hello tem um endereço de ponto de extremidade composto de cadeia de caracteres hello `sb`, o nome do namespace e o caminho hello "solver."</span><span class="sxs-lookup"><span data-stu-id="fa67a-155">hello relay endpoint has an endpoint address composed of hello string `sb`, your namespace name, and hello path "solver."</span></span> <span data-ttu-id="fa67a-156">Isso resulta em Olá URI `sb://[serviceNamespace].servicebus.windows.net/solver`, identificando o ponto de extremidade de serviço hello como um ponto de extremidade TCP de barramento de serviço (retransmissão) com o nome DNS totalmente qualificado externo.</span><span class="sxs-lookup"><span data-stu-id="fa67a-156">This results in hello URI `sb://[serviceNamespace].servicebus.windows.net/solver`, identifying hello service endpoint as a Service Bus (relay) TCP endpoint with a fully qualified external DNS name.</span></span> <span data-ttu-id="fa67a-157">Se você colocar código Olá substituindo espaços reservados de saudação em Olá `Main` função da saudação **Service** aplicativo, você terá um serviço funcional.</span><span class="sxs-lookup"><span data-stu-id="fa67a-157">If you place hello code replacing hello placeholders into hello `Main` function of hello **Service** application, you will have a functional service.</span></span> <span data-ttu-id="fa67a-158">Se você quiser toolisten seu serviço exclusivamente em retransmissão hello, remova a declaração de ponto de extremidade local do hello.</span><span class="sxs-lookup"><span data-stu-id="fa67a-158">If you want your service toolisten exclusively on hello relay, remove hello local endpoint declaration.</span></span>

### <a name="configure-a-service-host-in-hello-appconfig-file"></a><span data-ttu-id="fa67a-159">Configurar um host de serviço no arquivo App. config de saudação</span><span class="sxs-lookup"><span data-stu-id="fa67a-159">Configure a service host in hello App.config file</span></span>
<span data-ttu-id="fa67a-160">Você também pode configurar o host de saudação usando o arquivo App. config de saudação.</span><span class="sxs-lookup"><span data-stu-id="fa67a-160">You can also configure hello host using hello App.config file.</span></span> <span data-ttu-id="fa67a-161">serviço de saudação hospedagem de código nesse caso aparece no exemplo a seguir hello.</span><span class="sxs-lookup"><span data-stu-id="fa67a-161">hello service hosting code in this case appears in hello next example.</span></span>

```csharp
ServiceHost sh = new ServiceHost(typeof(ProblemSolver));
sh.Open();
Console.WriteLine("Press ENTER tooclose");
Console.ReadLine();
sh.Close();
```

<span data-ttu-id="fa67a-162">definições de ponto de extremidade de saudação mova para o arquivo App. config de saudação.</span><span class="sxs-lookup"><span data-stu-id="fa67a-162">hello endpoint definitions move into hello App.config file.</span></span> <span data-ttu-id="fa67a-163">pacote do NuGet Olá já adicionado um intervalo de toohello arquivo de definições de App. config, que são extensões de configuração Olá necessário para a retransmissão do Azure.</span><span class="sxs-lookup"><span data-stu-id="fa67a-163">hello NuGet package has already added a range of definitions toohello App.config file, which are hello required configuration extensions for Azure Relay.</span></span> <span data-ttu-id="fa67a-164">Olá seguinte exemplo, a saudação exata equivalente do código anterior de saudação, devem aparecer diretamente sob Olá **System. ServiceModel** elemento.</span><span class="sxs-lookup"><span data-stu-id="fa67a-164">hello following example, which is hello exact equivalent of hello previous code, should appear directly beneath hello **system.serviceModel** element.</span></span> <span data-ttu-id="fa67a-165">Esse exemplo pressupõe que o namespace do projeto C# é chamado de **Serviço**.</span><span class="sxs-lookup"><span data-stu-id="fa67a-165">This code example assumes that your project C# namespace is named **Service**.</span></span>
<span data-ttu-id="fa67a-166">Substitua espaços reservados de saudação com seu nome de namespace de retransmissão e chave de SAS.</span><span class="sxs-lookup"><span data-stu-id="fa67a-166">Replace hello placeholders with your relay namespace name and SAS key.</span></span>

```xml
<services>
    <service name="Service.ProblemSolver">
        <endpoint contract="Service.IProblemSolver"
                  binding="netTcpBinding"
                  address="net.tcp://localhost:9358/solver"/>
        <endpoint contract="Service.IProblemSolver"
                  binding="netTcpRelayBinding"
                  address="sb://<namespaceName>.servicebus.windows.net/solver"
                  behaviorConfiguration="sbTokenProvider"/>
    </service>
</services>
<behaviors>
    <endpointBehaviors>
        <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
                <tokenProvider>
                    <sharedAccessSignature keyName="RootManageSharedAccessKey" key="<yourKey>" />
                </tokenProvider>
            </transportClientEndpointBehavior>
        </behavior>
    </endpointBehaviors>
</behaviors>
```

<span data-ttu-id="fa67a-167">Depois de fazer essas alterações, o serviço de saudação iniciado como antes, mas com dois pontos de extremidade ao vivo: um local e um escutando na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="fa67a-167">After you make these changes, hello service starts as it did before, but with two live endpoints: one local and one listening in hello cloud.</span></span>

### <a name="create-hello-client"></a><span data-ttu-id="fa67a-168">Crie saudação do cliente</span><span class="sxs-lookup"><span data-stu-id="fa67a-168">Create hello client</span></span>
#### <a name="configure-a-client-programmatically"></a><span data-ttu-id="fa67a-169">Configure um cliente de forma programática</span><span class="sxs-lookup"><span data-stu-id="fa67a-169">Configure a client programmatically</span></span>
<span data-ttu-id="fa67a-170">serviço de saudação tooconsume, você pode construir um cliente WCF usando um [ChannelFactory](https://msdn.microsoft.com/library/system.servicemodel.channelfactory.aspx) objeto.</span><span class="sxs-lookup"><span data-stu-id="fa67a-170">tooconsume hello service, you can construct a WCF client using a [ChannelFactory](https://msdn.microsoft.com/library/system.servicemodel.channelfactory.aspx) object.</span></span> <span data-ttu-id="fa67a-171">O Barramento de Serviço usa um modelo de segurança baseado em token implementado com a SAS.</span><span class="sxs-lookup"><span data-stu-id="fa67a-171">Service Bus uses a token-based security model implemented using SAS.</span></span> <span data-ttu-id="fa67a-172">Olá [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) classe representa um provedor de token de segurança com métodos de fábrica de incorporados que retornam alguns provedores de token bem conhecidos.</span><span class="sxs-lookup"><span data-stu-id="fa67a-172">hello [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) class represents a security token provider with built-in factory methods that return some well-known token providers.</span></span> <span data-ttu-id="fa67a-173">Olá, exemplo a seguir usa Olá [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) método toohandle Olá aquisição token SAS apropriado de saudação.</span><span class="sxs-lookup"><span data-stu-id="fa67a-173">hello following example uses hello [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) method toohandle hello acquisition of hello appropriate SAS token.</span></span> <span data-ttu-id="fa67a-174">chave e nome de saudação são aqueles obtidos no portal de saudação conforme descrito na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="fa67a-174">hello name and key are those obtained from hello portal as described in hello previous section.</span></span>

<span data-ttu-id="fa67a-175">Primeiro, referência ou cópia Olá `IProblemSolver` código do serviço de saudação do contrato em seu projeto do cliente.</span><span class="sxs-lookup"><span data-stu-id="fa67a-175">First, reference or copy hello `IProblemSolver` contract code from hello service into your client project.</span></span>

<span data-ttu-id="fa67a-176">Em seguida, substitua o código Olá Olá `Main` método do cliente hello, novamente, substituindo texto de espaço reservado de saudação com a chave SAS e o namespace de retransmissão.</span><span class="sxs-lookup"><span data-stu-id="fa67a-176">Then, replace hello code in hello `Main` method of hello client, again replacing hello placeholder text with your relay namespace and SAS key.</span></span>

```csharp
var cf = new ChannelFactory<IProblemSolverChannel>(
    new NetTcpRelayBinding(),
    new EndpointAddress(ServiceBusEnvironment.CreateServiceUri("sb", "<namespaceName>", "solver")));

cf.Endpoint.Behaviors.Add(new TransportClientEndpointBehavior
            { TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey","<yourKey>") });

using (var ch = cf.CreateChannel())
{
    Console.WriteLine(ch.AddNumbers(4, 5));
}
```

<span data-ttu-id="fa67a-177">Agora você pode criar cliente hello e serviço hello, executá-los (execução de serviço Olá primeiro), saudação do cliente e chama o serviço de saudação imprime **9**.</span><span class="sxs-lookup"><span data-stu-id="fa67a-177">You can now build hello client and hello service, run them (run hello service first), and hello client calls hello service and prints **9**.</span></span> <span data-ttu-id="fa67a-178">Você pode executar Olá cliente e servidor em computadores diferentes, mesmo em redes e comunicação Olá ainda funcionarão.</span><span class="sxs-lookup"><span data-stu-id="fa67a-178">You can run hello client and server on different machines, even across networks, and hello communication will still work.</span></span> <span data-ttu-id="fa67a-179">código de cliente Olá também pode ser executado localmente ou na nuvem de saudação.</span><span class="sxs-lookup"><span data-stu-id="fa67a-179">hello client code can also run in hello cloud or locally.</span></span>

#### <a name="configure-a-client-in-hello-appconfig-file"></a><span data-ttu-id="fa67a-180">Configurar um cliente no arquivo App. config de saudação</span><span class="sxs-lookup"><span data-stu-id="fa67a-180">Configure a client in hello App.config file</span></span>
<span data-ttu-id="fa67a-181">saudação de código a seguir mostra como o cliente usando uma saudação tooconfigure Olá arquivo App. config.</span><span class="sxs-lookup"><span data-stu-id="fa67a-181">hello following code shows how tooconfigure hello client using hello App.config file.</span></span>

```csharp
var cf = new ChannelFactory<IProblemSolverChannel>("solver");
using (var ch = cf.CreateChannel())
{
    Console.WriteLine(ch.AddNumbers(4, 5));
}
```

<span data-ttu-id="fa67a-182">definições de ponto de extremidade de saudação mova para o arquivo App. config de saudação.</span><span class="sxs-lookup"><span data-stu-id="fa67a-182">hello endpoint definitions move into hello App.config file.</span></span> <span data-ttu-id="fa67a-183">Olá exemplo a seguir, que é Olá igual ao código Olá listado anteriormente deve aparecer diretamente sob Olá `<system.serviceModel>` elemento.</span><span class="sxs-lookup"><span data-stu-id="fa67a-183">hello following example, which is hello same as hello code listed previously, should appear directly beneath hello `<system.serviceModel>` element.</span></span> <span data-ttu-id="fa67a-184">Aqui, como antes, você deve substituir espaços reservados de saudação com a chave SAS e o namespace de retransmissão.</span><span class="sxs-lookup"><span data-stu-id="fa67a-184">Here, as before, you must replace hello placeholders with your relay namespace and SAS key.</span></span>

```xml
<client>
    <endpoint name="solver" contract="Service.IProblemSolver"
              binding="netTcpRelayBinding"
              address="sb://<namespaceName>.servicebus.windows.net/solver"
              behaviorConfiguration="sbTokenProvider"/>
</client>
<behaviors>
    <endpointBehaviors>
        <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
                <tokenProvider>
                    <sharedAccessSignature keyName="RootManageSharedAccessKey" key="<yourKey>" />
                </tokenProvider>
            </transportClientEndpointBehavior>
        </behavior>
    </endpointBehaviors>
</behaviors>
```

## <a name="next-steps"></a><span data-ttu-id="fa67a-185">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fa67a-185">Next steps</span></span>
<span data-ttu-id="fa67a-186">Agora que você aprendeu as Noções básicas de saudação de retransmissão do Azure, siga essas toolearn links mais.</span><span class="sxs-lookup"><span data-stu-id="fa67a-186">Now that you've learned hello basics of Azure Relay, follow these links toolearn more.</span></span>

* [<span data-ttu-id="fa67a-187">O que é Retransmissão do Azure?</span><span class="sxs-lookup"><span data-stu-id="fa67a-187">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="fa67a-188">Visão geral da arquitetura de Barramento de Serviço do Azure</span><span class="sxs-lookup"><span data-stu-id="fa67a-188">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* <span data-ttu-id="fa67a-189">Baixe os exemplos de barramento de serviço do [exemplos do Azure] [ Azure samples] ou consulte Olá [visão geral dos exemplos de barramento de serviço][overview of Service Bus samples].</span><span class="sxs-lookup"><span data-stu-id="fa67a-189">Download Service Bus samples from [Azure samples][Azure samples] or see hello [overview of Service Bus samples][overview of Service Bus samples].</span></span>

[Shared Access Signature Authentication with Service Bus]: ../service-bus-messaging/service-bus-shared-access-signature-authentication.md
[Azure samples]: https://code.msdn.microsoft.com/site/search?query=service%20bus&f%5B0%5D.Value=service%20bus&f%5B0%5D.Type=SearchText&ac=2
[overview of Service Bus samples]: ../service-bus-messaging/service-bus-samples.md
