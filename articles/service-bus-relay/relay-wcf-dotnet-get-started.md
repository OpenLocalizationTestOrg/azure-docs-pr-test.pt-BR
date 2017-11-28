---
title: "Introdução às retransmissões WCF da Retransmissão do Azure no .NET | Microsoft Docs"
description: "Saiba como usar as retransmissões WCF da Retransmissão do Azure para conectar dois aplicativos hospedados em locais diferentes."
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
ms.openlocfilehash: 1af1ac78398d65e6a87f0d24d6198f3dfbc82ffd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-azure-relay-wcf-relays-with-net"></a><span data-ttu-id="c5b75-103">Como usar as retransmissões WCF da Retransmissão do Azure com .NET</span><span class="sxs-lookup"><span data-stu-id="c5b75-103">How to use Azure Relay WCF relays with .NET</span></span>
<span data-ttu-id="c5b75-104">Este artigo descreve como usar o serviço Retransmissão do Azure.</span><span class="sxs-lookup"><span data-stu-id="c5b75-104">This article describes how to use the Azure Relay service.</span></span> <span data-ttu-id="c5b75-105">Os exemplos são escritos em C# e usam a API da WCF (Windows Communication Foundation) com extensões contidas no assembly do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="c5b75-105">The samples are written in C# and use the Windows Communication Foundation (WCF) API with extensions contained in the Service Bus assembly.</span></span> <span data-ttu-id="c5b75-106">Para obter mais informações sobre a retransmissão do Azure, consulte a [Visão geral da Retransmissão do Azure](relay-what-is-it.md).</span><span class="sxs-lookup"><span data-stu-id="c5b75-106">For more information about Azure relay, see the [Azure Relay overview](relay-what-is-it.md).</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="what-is-wcf-relay"></a><span data-ttu-id="c5b75-107">O que é Retransmissão do WCF?</span><span class="sxs-lookup"><span data-stu-id="c5b75-107">What is WCF Relay?</span></span>

<span data-ttu-id="c5b75-108">O serviço [*Retransmissão do WCF*](relay-what-is-it.md) do Azure permite criar aplicativos híbridos que executam no datacenter do Azure e em seu próprio ambiente corporativo local.</span><span class="sxs-lookup"><span data-stu-id="c5b75-108">The Azure [*WCF Relay*](relay-what-is-it.md) service enables you to build hybrid applications that run in both an Azure datacenter and your own on-premises enterprise environment.</span></span> <span data-ttu-id="c5b75-109">O serviço de retransmissão facilita isso permitindo que você exponha com segurança os serviços do WCF (Windows Communication Foundation) que residem em uma rede corporativa à nuvem pública, sem precisar abrir uma conexão de firewall nem exigir alterações intrusivas em uma infraestrutura de rede corporativa.</span><span class="sxs-lookup"><span data-stu-id="c5b75-109">The relay service facilitates this by enabling you to securely expose Windows Communication Foundation (WCF) services that reside within a corporate enterprise network to the public cloud, without having to open a firewall connection, or requiring intrusive changes to a corporate network infrastructure.</span></span>

![Conceitos de retransmissão do WCF](./media/service-bus-dotnet-how-to-use-relay/sb-relay-01.png)

<span data-ttu-id="c5b75-111">A Retransmissão do Azure permite que você hospede serviços WCF em seu ambiente corporativo existente.</span><span class="sxs-lookup"><span data-stu-id="c5b75-111">Azure Relay enables you to host WCF services within your existing enterprise environment.</span></span> <span data-ttu-id="c5b75-112">Em seguida, você pode delegar a escuta de sessões e solicitações de entrada para esses serviços WCF ao serviço de retransmissão em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="c5b75-112">You can then delegate listening for incoming sessions and requests to these WCF services to the relay service running within Azure.</span></span> <span data-ttu-id="c5b75-113">Isso permite que você exponha esses serviços para o código do aplicativo em execução no Azure ou para usuários móveis ou ambientes de parceiros na extranet.</span><span class="sxs-lookup"><span data-stu-id="c5b75-113">This enables you to expose these services to application code running in Azure, or to mobile workers or extranet partner environments.</span></span> <span data-ttu-id="c5b75-114">A Retransmissão permite controlar com segurança quem pode acessar esses serviços em um nível refinado.</span><span class="sxs-lookup"><span data-stu-id="c5b75-114">Relay enables you to securely control who can access these services at a fine-grained level.</span></span> <span data-ttu-id="c5b75-115">Ele fornece uma maneira poderosa e segura de exibir a funcionalidade do aplicativo e os dados de suas soluções corporativas existentes e tira proveito disso na nuvem.</span><span class="sxs-lookup"><span data-stu-id="c5b75-115">It provides a powerful and secure way to expose application functionality and data from your existing enterprise solutions and take advantage of it from the cloud.</span></span>

<span data-ttu-id="c5b75-116">Este artigo aborda como usar a Retransmissão do Azure para criar um serviço Web do WCF, exposto usando uma associação de canal TCP, que implementa uma conversa segura entre duas entidades.</span><span class="sxs-lookup"><span data-stu-id="c5b75-116">This article discusses how to use Azure Relay to create a WCF web service, exposed using a TCP channel binding, that implements a secure conversation between two parties.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="get-the-service-bus-nuget-package"></a><span data-ttu-id="c5b75-117">Obtenha o pacote do NuGet do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="c5b75-117">Get the Service Bus NuGet package</span></span>
<span data-ttu-id="c5b75-118">O [pacote NuGet de Barramento de Serviço](https://www.nuget.org/packages/WindowsAzure.ServiceBus) é a maneira mais fácil de obter a API do Barramento de Serviço e configurar seu aplicativo com todas as dependências do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="c5b75-118">The [Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus) is the easiest way to get the Service Bus API and to configure your application with all of the Service Bus dependencies.</span></span> <span data-ttu-id="c5b75-119">Para instalar o pacote do NuGet em seu projeto, proceda da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="c5b75-119">To install the NuGet package in your project, do the following:</span></span>

1. <span data-ttu-id="c5b75-120">No Gerenciador de Soluções, clique com o botão direito do mouse em **Referências** e clique em **Gerenciar Pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="c5b75-120">In Solution Explorer, right-click **References**, then click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="c5b75-121">Procure "Barramento de Serviço" e selecione o item **Barramento de Serviço do Microsoft Azure** .</span><span class="sxs-lookup"><span data-stu-id="c5b75-121">Search for "Service Bus" and select the **Microsoft Azure Service Bus** item.</span></span> <span data-ttu-id="c5b75-122">Clique em **Instalar** para concluir a instalação e feche a seguinte caixa de diálogo:</span><span class="sxs-lookup"><span data-stu-id="c5b75-122">Click **Install** to complete the installation, then close the following dialog box:</span></span>
   
   ![](./media/service-bus-dotnet-how-to-use-relay/getting-started-multi-tier-13.png)

## <a name="expose-and-consume-a-soap-web-service-with-tcp"></a><span data-ttu-id="c5b75-123">Exponha e consuma um serviço Web SOAP com TCP</span><span class="sxs-lookup"><span data-stu-id="c5b75-123">Expose and consume a SOAP web service with TCP</span></span>
<span data-ttu-id="c5b75-124">Para expor um serviço Web SOAP WCF existente para consumo externo, você deve alterar as associações e endereços do serviço.</span><span class="sxs-lookup"><span data-stu-id="c5b75-124">To expose an existing WCF SOAP web service for external consumption, you must make changes to the service bindings and addresses.</span></span> <span data-ttu-id="c5b75-125">Isso pode exigir alterações em seu arquivo de configuração ou exigir alterações de código, dependendo de como você instalou e configurou seus serviços WCF.</span><span class="sxs-lookup"><span data-stu-id="c5b75-125">This may require changes to your configuration file or it could require code changes, depending on how you have set up and configured your WCF services.</span></span> <span data-ttu-id="c5b75-126">Observe que o WCF permite ter vários pontos de extremidade de rede no mesmo serviço e, portanto, você pode reter os pontos de extremidade internos existentes, ao mesmo tempo que adiciona pontos de extremidade de retransmissão para o acesso externo simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="c5b75-126">Note that WCF allows you to have multiple network endpoints over the same service, so you can retain the existing internal endpoints while adding relay endpoints for external access at the same time.</span></span>

<span data-ttu-id="c5b75-127">Nesta tarefa, você cria um serviço WCF simples e adiciona um ouvinte de retransmissão a ele.</span><span class="sxs-lookup"><span data-stu-id="c5b75-127">In this task, you build a simple WCF service and add a relay listener to it.</span></span> <span data-ttu-id="c5b75-128">Este exercício pressupõe alguma familiaridade com o Visual Studio e, portanto, não percorre todos os detalhes da criação de um projeto.</span><span class="sxs-lookup"><span data-stu-id="c5b75-128">This exercise assumes some familiarity with Visual Studio, and therefore does not walk through all the details of creating a project.</span></span> <span data-ttu-id="c5b75-129">Em vez disso, ele se concentra no código.</span><span class="sxs-lookup"><span data-stu-id="c5b75-129">Instead, it focuses on the code.</span></span>

<span data-ttu-id="c5b75-130">Antes de iniciar as etapas a seguir, conclua o seguinte procedimento para configurar seu ambiente:</span><span class="sxs-lookup"><span data-stu-id="c5b75-130">Before starting these steps, complete the following procedure to set up your environment:</span></span>

1. <span data-ttu-id="c5b75-131">No Visual Studio, crie um aplicativo de console que contenha dois projetos: “Cliente” e “Serviço” na solução.</span><span class="sxs-lookup"><span data-stu-id="c5b75-131">Within Visual Studio, create a console application that contains two projects, "Client" and "Service", within the solution.</span></span>
2. <span data-ttu-id="c5b75-132">Adicione o pacote NuGet do Barramento de Serviço aos dois projetos.</span><span class="sxs-lookup"><span data-stu-id="c5b75-132">Add the Service Bus NuGet package to both projects.</span></span> <span data-ttu-id="c5b75-133">Esse pacote adiciona todas as referências ao assembly necessárias para seus projetos.</span><span class="sxs-lookup"><span data-stu-id="c5b75-133">This package adds all the necessary assembly references to your projects.</span></span>

### <a name="how-to-create-the-service"></a><span data-ttu-id="c5b75-134">Como criar o serviço</span><span class="sxs-lookup"><span data-stu-id="c5b75-134">How to create the service</span></span>
<span data-ttu-id="c5b75-135">Primeiro, crie o serviço.</span><span class="sxs-lookup"><span data-stu-id="c5b75-135">First, create the service itself.</span></span> <span data-ttu-id="c5b75-136">Qualquer serviço WCF consiste em pelo menos três partes distintas:</span><span class="sxs-lookup"><span data-stu-id="c5b75-136">Any WCF service consists of at least three distinct parts:</span></span>

* <span data-ttu-id="c5b75-137">Definição de um contrato que descreve quais mensagens são trocadas e quais operações devem ser chamadas.</span><span class="sxs-lookup"><span data-stu-id="c5b75-137">Definition of a contract that describes what messages are exchanged and what operations are to be invoked.</span></span>
* <span data-ttu-id="c5b75-138">Implementação do contrato.</span><span class="sxs-lookup"><span data-stu-id="c5b75-138">Implementation of that contract.</span></span>
* <span data-ttu-id="c5b75-139">Host que hospeda o serviço WCF e exibe vários pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="c5b75-139">Host that hosts the WCF service and exposes several endpoints.</span></span>

<span data-ttu-id="c5b75-140">Os exemplos de código desta seção abordam cada um desses componentes.</span><span class="sxs-lookup"><span data-stu-id="c5b75-140">The code examples in this section address each of these components.</span></span>

<span data-ttu-id="c5b75-141">O contrato define uma única operação, `AddNumbers`, que adiciona dois números e retorna o resultado.</span><span class="sxs-lookup"><span data-stu-id="c5b75-141">The contract defines a single operation, `AddNumbers`, that adds two numbers and returns the result.</span></span> <span data-ttu-id="c5b75-142">A interface `IProblemSolverChannel` permite que o cliente gerencie mais facilmente o tempo de vida do proxy.</span><span class="sxs-lookup"><span data-stu-id="c5b75-142">The `IProblemSolverChannel` interface enables the client to more easily manage the proxy lifetime.</span></span> <span data-ttu-id="c5b75-143">A criação dessa interface é considerada uma prática recomendada.</span><span class="sxs-lookup"><span data-stu-id="c5b75-143">Creating such an interface is considered a best practice.</span></span> <span data-ttu-id="c5b75-144">É uma boa ideia colocar essa definição de contrato em um arquivo separado para que você possa fazer referência a ele nos dois projetos, "Cliente" e "Serviço", mas você também pode copiar o código nos dois projetos:</span><span class="sxs-lookup"><span data-stu-id="c5b75-144">It's a good idea to put this contract definition into a separate file so that you can reference that file from both your "Client" and "Service" projects, but you can also copy the code into both projects.</span></span>

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

<span data-ttu-id="c5b75-145">Com o contrato em vigor, a implementação ocorre da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="c5b75-145">With the contract in place, the implementation is as follows:</span></span>

```csharp
class ProblemSolver : IProblemSolver
{
    public int AddNumbers(int a, int b)
    {
        return a + b;
    }
}
```

### <a name="configure-a-service-host-programmatically"></a><span data-ttu-id="c5b75-146">Configure um host de serviço de forma programática</span><span class="sxs-lookup"><span data-stu-id="c5b75-146">Configure a service host programmatically</span></span>
<span data-ttu-id="c5b75-147">Com o contrato e a implementação estabelecidos, você agora pode hospedar o serviço.</span><span class="sxs-lookup"><span data-stu-id="c5b75-147">With the contract and implementation in place, you can now host the service.</span></span> <span data-ttu-id="c5b75-148">A hospedagem ocorre dentro de um objeto [System.ServiceModel.ServiceHost](https://msdn.microsoft.com/library/system.servicemodel.servicehost.aspx), que cuida do gerenciamento de instâncias do serviço e hospeda os pontos de extremidade que detectam as mensagens.</span><span class="sxs-lookup"><span data-stu-id="c5b75-148">Hosting occurs inside a [System.ServiceModel.ServiceHost](https://msdn.microsoft.com/library/system.servicemodel.servicehost.aspx) object, which takes care of managing instances of the service and hosts the endpoints that listen for messages.</span></span> <span data-ttu-id="c5b75-149">O código a seguir configura o serviço com um ponto de extremidade local normal e um ponto de extremidade de retransmissão para ilustrar a aparência, lado a lado, dos pontos de extremidade internos e externos.</span><span class="sxs-lookup"><span data-stu-id="c5b75-149">The following code configures the service with both a regular local endpoint and a relay endpoint to illustrate the appearance, side by side, of internal and external endpoints.</span></span> <span data-ttu-id="c5b75-150">Substitua a cadeia de caracteres *namespace* pelo nome do namespace e *yourKey* pela chave SAS obtida na etapa de configuração anterior.</span><span class="sxs-lookup"><span data-stu-id="c5b75-150">Replace the string *namespace* with your namespace name and *yourKey* with the SAS key that you obtained in the previous setup step.</span></span>

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

Console.WriteLine("Press ENTER to close");
Console.ReadLine();

sh.Close();
```

<span data-ttu-id="c5b75-151">No exemplo, você cria dois pontos de extremidade que estão na mesma implementação de contrato.</span><span class="sxs-lookup"><span data-stu-id="c5b75-151">In the example, you create two endpoints that are on the same contract implementation.</span></span> <span data-ttu-id="c5b75-152">Um é local e o outro é projetado por meio da Retransmissão do Azure.</span><span class="sxs-lookup"><span data-stu-id="c5b75-152">One is local and one is projected through Azure Relay.</span></span> <span data-ttu-id="c5b75-153">As principais diferenças entre eles são as associações; [NetTcpBinding](https://msdn.microsoft.com/library/system.servicemodel.nettcpbinding.aspx) para o local e [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding#microsoft_servicebus_nettcprelaybinding) para o ponto de extremidade de retransmissão e os endereços.</span><span class="sxs-lookup"><span data-stu-id="c5b75-153">The key differences between them are the bindings; [NetTcpBinding](https://msdn.microsoft.com/library/system.servicemodel.nettcpbinding.aspx) for the local one and [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding#microsoft_servicebus_nettcprelaybinding) for the relay endpoint and the addresses.</span></span> <span data-ttu-id="c5b75-154">O ponto de extremidade local tem um endereço de rede local com uma porta distinta.</span><span class="sxs-lookup"><span data-stu-id="c5b75-154">The local endpoint has a local network address with a distinct port.</span></span> <span data-ttu-id="c5b75-155">O ponto de extremidade de retransmissão tem um endereço do ponto de extremidade composto pela cadeia de caracteres `sb`, o nome do namespace e o caminho “solver”.</span><span class="sxs-lookup"><span data-stu-id="c5b75-155">The relay endpoint has an endpoint address composed of the string `sb`, your namespace name, and the path "solver."</span></span> <span data-ttu-id="c5b75-156">Isso resulta na identificação pelo URI `sb://[serviceNamespace].servicebus.windows.net/solver` do ponto de extremidade de serviço como um ponto de extremidade TCP (retransmissão) do Barramento de Serviço com um nome DNS externo totalmente qualificado.</span><span class="sxs-lookup"><span data-stu-id="c5b75-156">This results in the URI `sb://[serviceNamespace].servicebus.windows.net/solver`, identifying the service endpoint as a Service Bus (relay) TCP endpoint with a fully qualified external DNS name.</span></span> <span data-ttu-id="c5b75-157">Se você colocar o código substituindo os espaços reservados, na função `Main` do aplicativo **Serviço**, você terá um serviço funcional.</span><span class="sxs-lookup"><span data-stu-id="c5b75-157">If you place the code replacing the placeholders into the `Main` function of the **Service** application, you will have a functional service.</span></span> <span data-ttu-id="c5b75-158">Se desejar que o serviço ouça exclusivamente na retransmissão, remova a declaração de ponto de extremidade local.</span><span class="sxs-lookup"><span data-stu-id="c5b75-158">If you want your service to listen exclusively on the relay, remove the local endpoint declaration.</span></span>

### <a name="configure-a-service-host-in-the-appconfig-file"></a><span data-ttu-id="c5b75-159">Configure um host de serviço no arquivo App.config</span><span class="sxs-lookup"><span data-stu-id="c5b75-159">Configure a service host in the App.config file</span></span>
<span data-ttu-id="c5b75-160">Você também pode configurar o host usando o arquivo App.config.</span><span class="sxs-lookup"><span data-stu-id="c5b75-160">You can also configure the host using the App.config file.</span></span> <span data-ttu-id="c5b75-161">O serviço de hospedagem de código, nesse caso, é exibido no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="c5b75-161">The service hosting code in this case appears in the next example.</span></span>

```csharp
ServiceHost sh = new ServiceHost(typeof(ProblemSolver));
sh.Open();
Console.WriteLine("Press ENTER to close");
Console.ReadLine();
sh.Close();
```

<span data-ttu-id="c5b75-162">As definições de ponto de extremidade são movidas para o arquivo App.config.</span><span class="sxs-lookup"><span data-stu-id="c5b75-162">The endpoint definitions move into the App.config file.</span></span> <span data-ttu-id="c5b75-163">O pacote NuGet já adicionou uma série de definições ao arquivo App.config, que são as extensões de configuração necessárias para a Retransmissão do Azure.</span><span class="sxs-lookup"><span data-stu-id="c5b75-163">The NuGet package has already added a range of definitions to the App.config file, which are the required configuration extensions for Azure Relay.</span></span> <span data-ttu-id="c5b75-164">O seguinte exemplo de código, que é o equivalente exato do exemplo de código anterior, deve aparecer diretamente sob o elemento **system.serviceModel**.</span><span class="sxs-lookup"><span data-stu-id="c5b75-164">The following example, which is the exact equivalent of the previous code, should appear directly beneath the **system.serviceModel** element.</span></span> <span data-ttu-id="c5b75-165">Esse exemplo pressupõe que o namespace do projeto C# é chamado de **Serviço**.</span><span class="sxs-lookup"><span data-stu-id="c5b75-165">This code example assumes that your project C# namespace is named **Service**.</span></span>
<span data-ttu-id="c5b75-166">Substitua os espaços reservados pelo nome de namespace da retransmissão e pela chave de SAS.</span><span class="sxs-lookup"><span data-stu-id="c5b75-166">Replace the placeholders with your relay namespace name and SAS key.</span></span>

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

<span data-ttu-id="c5b75-167">Depois de fazer essas alterações, o serviço é iniciado como antes, mas com dois pontos de extremidade ativos: um local e um escutando na nuvem.</span><span class="sxs-lookup"><span data-stu-id="c5b75-167">After you make these changes, the service starts as it did before, but with two live endpoints: one local and one listening in the cloud.</span></span>

### <a name="create-the-client"></a><span data-ttu-id="c5b75-168">Crie o cliente</span><span class="sxs-lookup"><span data-stu-id="c5b75-168">Create the client</span></span>
#### <a name="configure-a-client-programmatically"></a><span data-ttu-id="c5b75-169">Configure um cliente de forma programática</span><span class="sxs-lookup"><span data-stu-id="c5b75-169">Configure a client programmatically</span></span>
<span data-ttu-id="c5b75-170">Para consumir o serviço, você pode construir um cliente WCF usando um objeto [ChannelFactory](https://msdn.microsoft.com/library/system.servicemodel.channelfactory.aspx).</span><span class="sxs-lookup"><span data-stu-id="c5b75-170">To consume the service, you can construct a WCF client using a [ChannelFactory](https://msdn.microsoft.com/library/system.servicemodel.channelfactory.aspx) object.</span></span> <span data-ttu-id="c5b75-171">O Barramento de Serviço usa um modelo de segurança baseado em token implementado com a SAS.</span><span class="sxs-lookup"><span data-stu-id="c5b75-171">Service Bus uses a token-based security model implemented using SAS.</span></span> <span data-ttu-id="c5b75-172">A classe [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) representa um provedor de token de segurança com métodos de fábrica internos que retornam alguns provedores de token conhecidos.</span><span class="sxs-lookup"><span data-stu-id="c5b75-172">The [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) class represents a security token provider with built-in factory methods that return some well-known token providers.</span></span> <span data-ttu-id="c5b75-173">O exemplo a seguir usa o método [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) para lidar com a aquisição do token SAS apropriado.</span><span class="sxs-lookup"><span data-stu-id="c5b75-173">The following example uses the [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) method to handle the acquisition of the appropriate SAS token.</span></span> <span data-ttu-id="c5b75-174">O nome e a chave são os obtidos no portal, conforme descrito na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="c5b75-174">The name and key are those obtained from the portal as described in the previous section.</span></span>

<span data-ttu-id="c5b75-175">Primeiro, faça referência ou copie o código do contrato `IProblemSolver` do serviço para o projeto cliente.</span><span class="sxs-lookup"><span data-stu-id="c5b75-175">First, reference or copy the `IProblemSolver` contract code from the service into your client project.</span></span>

<span data-ttu-id="c5b75-176">Em seguida, substitua o código do método `Main` do cliente, substituindo novamente o texto do espaço reservado pelo namespace de retransmissão e pela chave de SAS.</span><span class="sxs-lookup"><span data-stu-id="c5b75-176">Then, replace the code in the `Main` method of the client, again replacing the placeholder text with your relay namespace and SAS key.</span></span>

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

<span data-ttu-id="c5b75-177">Agora, você pode compilar o cliente e o serviço, executá-los (execute o serviço primeiro) e o cliente chama o serviço e imprime **9**.</span><span class="sxs-lookup"><span data-stu-id="c5b75-177">You can now build the client and the service, run them (run the service first), and the client calls the service and prints **9**.</span></span> <span data-ttu-id="c5b75-178">Você pode executar o cliente e o servidor em máquinas diferentes, até entre redes, e a comunicação ainda funcionará.</span><span class="sxs-lookup"><span data-stu-id="c5b75-178">You can run the client and server on different machines, even across networks, and the communication will still work.</span></span> <span data-ttu-id="c5b75-179">O código do cliente também pode ser executado na nuvem ou localmente.</span><span class="sxs-lookup"><span data-stu-id="c5b75-179">The client code can also run in the cloud or locally.</span></span>

#### <a name="configure-a-client-in-the-appconfig-file"></a><span data-ttu-id="c5b75-180">Configure um cliente no arquivo App.config</span><span class="sxs-lookup"><span data-stu-id="c5b75-180">Configure a client in the App.config file</span></span>
<span data-ttu-id="c5b75-181">O código a seguir mostra como configurar o cliente usando o arquivo App.config.</span><span class="sxs-lookup"><span data-stu-id="c5b75-181">The following code shows how to configure the client using the App.config file.</span></span>

```csharp
var cf = new ChannelFactory<IProblemSolverChannel>("solver");
using (var ch = cf.CreateChannel())
{
    Console.WriteLine(ch.AddNumbers(4, 5));
}
```

<span data-ttu-id="c5b75-182">As definições de ponto de extremidade são movidas para o arquivo App.config.</span><span class="sxs-lookup"><span data-stu-id="c5b75-182">The endpoint definitions move into the App.config file.</span></span> <span data-ttu-id="c5b75-183">O exemplo a seguir, que é o mesmo código listado anteriormente, deve aparecer diretamente sob o elemento `<system.serviceModel>`.</span><span class="sxs-lookup"><span data-stu-id="c5b75-183">The following example, which is the same as the code listed previously, should appear directly beneath the `<system.serviceModel>` element.</span></span> <span data-ttu-id="c5b75-184">Aqui, como antes, você deve substituir os espaços reservados pelo namespace de retransmissão e pela chave de SAS.</span><span class="sxs-lookup"><span data-stu-id="c5b75-184">Here, as before, you must replace the placeholders with your relay namespace and SAS key.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="c5b75-185">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c5b75-185">Next steps</span></span>
<span data-ttu-id="c5b75-186">Agora que você já sabe os conceitos básicos sobre a Retransmissão do Azure, siga estes links para saber mais.</span><span class="sxs-lookup"><span data-stu-id="c5b75-186">Now that you've learned the basics of Azure Relay, follow these links to learn more.</span></span>

* [<span data-ttu-id="c5b75-187">O que é Retransmissão do Azure?</span><span class="sxs-lookup"><span data-stu-id="c5b75-187">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="c5b75-188">Visão geral da arquitetura de Barramento de Serviço do Azure</span><span class="sxs-lookup"><span data-stu-id="c5b75-188">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* <span data-ttu-id="c5b75-189">Baixe exemplos de Barramento de Serviço das [amostras do Azure][Azure samples] ou confira a [visão geral de amostras do Barramento de Serviço][overview of Service Bus samples].</span><span class="sxs-lookup"><span data-stu-id="c5b75-189">Download Service Bus samples from [Azure samples][Azure samples] or see the [overview of Service Bus samples][overview of Service Bus samples].</span></span>

[Shared Access Signature Authentication with Service Bus]: ../service-bus-messaging/service-bus-shared-access-signature-authentication.md
[Azure samples]: https://code.msdn.microsoft.com/site/search?query=service%20bus&f%5B0%5D.Value=service%20bus&f%5B0%5D.Type=SearchText&ac=2
[overview of Service Bus samples]: ../service-bus-messaging/service-bus-samples.md
