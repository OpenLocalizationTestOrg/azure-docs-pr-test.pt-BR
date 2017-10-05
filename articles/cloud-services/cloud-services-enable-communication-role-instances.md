---
title: "Comunicação para funções nos Serviços de Nuvem | Microsoft Docs"
description: "As instâncias de função nos Serviços de Nuvem podem ter pontos de extremidade (http, https, tcp, udp) definidos que se comunicam com a parte externa ou entre outras instâncias de função."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 7008a083-acbe-4fb8-ae60-b837ef971ca1
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/14/2016
ms.author: adegeo
ms.openlocfilehash: 8e171d56bb67c971337fa383014988074ec828b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-communication-for-role-instances-in-azure"></a><span data-ttu-id="0e370-103">Habilitar a comunicação para instâncias de função no Azure</span><span class="sxs-lookup"><span data-stu-id="0e370-103">Enable communication for role instances in azure</span></span>
<span data-ttu-id="0e370-104">As funções de serviço de nuvem se comunicam por meio de conexões internas e externas.</span><span class="sxs-lookup"><span data-stu-id="0e370-104">Cloud service roles communicate through internal and external connections.</span></span> <span data-ttu-id="0e370-105">As conexões externas são chamadas de **pontos de extremidade de entrada**, enquanto as conexões internas são chamadas de **pontos de extremidade internos**.</span><span class="sxs-lookup"><span data-stu-id="0e370-105">External connections are called **input endpoints** while internal connections are called **internal endpoints**.</span></span> <span data-ttu-id="0e370-106">Este tópico descreve como modificar a [definição de serviço](cloud-services-model-and-package.md#csdef) para criar pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="0e370-106">This topic describes how to modify the [service definition](cloud-services-model-and-package.md#csdef) to create endpoints.</span></span>

## <a name="input-endpoint"></a><span data-ttu-id="0e370-107">Ponto de extremidade de entrada</span><span class="sxs-lookup"><span data-stu-id="0e370-107">Input endpoint</span></span>
<span data-ttu-id="0e370-108">O ponto de extremidade de entrada é usado quando você deseja expor uma porta para o exterior.</span><span class="sxs-lookup"><span data-stu-id="0e370-108">The input endpoint is used when you want to expose a port to the outside.</span></span> <span data-ttu-id="0e370-109">Você especifica o tipo de protocolo e a porta do ponto de extremidade e então o aplica às portas externa e interna do ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="0e370-109">You specify the protocol type and the port of the endpoint which then applies for both the external and internal ports for the endpoint.</span></span> <span data-ttu-id="0e370-110">Se desejar, você pode especificar uma porta interna diferente para o ponto de extremidade com o atributo [localPort](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) .</span><span class="sxs-lookup"><span data-stu-id="0e370-110">If you want, you can specify a different internal port for the endpoint with the [localPort](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) attribute.</span></span>

<span data-ttu-id="0e370-111">O ponto de extremidade de entrada pode usar os seguintes protocolos: **http, https, tcp, udp**.</span><span class="sxs-lookup"><span data-stu-id="0e370-111">The input endpoint can use the following protocols: **http, https, tcp, udp**.</span></span>

<span data-ttu-id="0e370-112">Para criar um ponto de extremidade de entrada, adicione o elemento filho **InputEndpoint** ao elemento **Endpoints** de uma função Web ou de trabalho.</span><span class="sxs-lookup"><span data-stu-id="0e370-112">To create an input endpoint, add the **InputEndpoint** child element to the **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
</Endpoints> 
```

## <a name="instance-input-endpoint"></a><span data-ttu-id="0e370-113">Ponto de extremidade de entrada de instância</span><span class="sxs-lookup"><span data-stu-id="0e370-113">Instance input endpoint</span></span>
<span data-ttu-id="0e370-114">Os pontos de extremidade de entrada de instância são semelhantes aos pontos de extremidade de entrada, mas permitem que você mapeie portas voltadas para o público específicas para cada instância de função individual usando o encaminhamento de porta no balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="0e370-114">Instance input endpoints are similar to input endpoints but allows you map specific public-facing ports for each individual role instance by using port forwarding on the load balancer.</span></span> <span data-ttu-id="0e370-115">Você pode especificar uma única porta voltada para o público ou um intervalo de portas.</span><span class="sxs-lookup"><span data-stu-id="0e370-115">You can specify a single public-facing port, or a range of ports.</span></span>

<span data-ttu-id="0e370-116">O ponto de extremidade de entrada de instância só pode usar **tcp** ou **udp** como o protocolo.</span><span class="sxs-lookup"><span data-stu-id="0e370-116">The instance input endpoint can only use **tcp** or **udp** as the protocol.</span></span>

<span data-ttu-id="0e370-117">Para criar um ponto de extremidade de entrada de instância, adicione o elemento filho **InstanceInputEndpoint** ao elemento **Endpoints** de uma função Web ou de trabalho.</span><span class="sxs-lookup"><span data-stu-id="0e370-117">To create an instance input endpoint, add the **InstanceInputEndpoint** child element to the **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InstanceInputEndpoint name="Endpoint2" protocol="tcp" localPort="10100">
    <AllocatePublicPortFrom>
      <FixedPortRange max="10109" min="10105" />
    </AllocatePublicPortFrom>
  </InstanceInputEndpoint>
</Endpoints>
```

## <a name="internal-endpoint"></a><span data-ttu-id="0e370-118">Ponto de extremidade interno</span><span class="sxs-lookup"><span data-stu-id="0e370-118">Internal endpoint</span></span>
<span data-ttu-id="0e370-119">Os pontos de extremidade internos estão disponíveis para a comunicação entre instâncias.</span><span class="sxs-lookup"><span data-stu-id="0e370-119">Internal endpoints are available for instance-to-instance communication.</span></span> <span data-ttu-id="0e370-120">A porta é opcional e, se for omitida, uma porta dinâmica será atribuída ao ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="0e370-120">The port is optional and if omitted, a dynamic port is assigned to the endpoint.</span></span> <span data-ttu-id="0e370-121">Um intervalo de portas pode ser usado.</span><span class="sxs-lookup"><span data-stu-id="0e370-121">A port range can be used.</span></span> <span data-ttu-id="0e370-122">Há um limite de cinco pontos de extremidade internos por função.</span><span class="sxs-lookup"><span data-stu-id="0e370-122">There is a limit of five internal endpoints per role.</span></span>

<span data-ttu-id="0e370-123">O ponto de extremidade interno pode usar os seguintes protocolos: **http, tcp, udp, any**.</span><span class="sxs-lookup"><span data-stu-id="0e370-123">The internal endpoint can use the following protocols: **http, tcp, udp, any**.</span></span>

<span data-ttu-id="0e370-124">Para criar um ponto de extremidade de entrada interno, adicione o elemento filho **InternalEndpoint** ao elemento **Endpoints** de uma função Web ou de trabalho.</span><span class="sxs-lookup"><span data-stu-id="0e370-124">To create an internal input endpoint, add the **InternalEndpoint** child element to the **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any" port="8999" />
</Endpoints> 
```

<span data-ttu-id="0e370-125">Você também pode usar um intervalo de portas.</span><span class="sxs-lookup"><span data-stu-id="0e370-125">You can also use a port range.</span></span>

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any">
    <FixedPortRange max="8995" min="8999" />
  </InternalEndpoint>
</Endpoints>
```


## <a name="worker-roles-vs-web-roles"></a><span data-ttu-id="0e370-126">Funções de trabalho versus Funções da Web</span><span class="sxs-lookup"><span data-stu-id="0e370-126">Worker roles vs. Web roles</span></span>
<span data-ttu-id="0e370-127">Há uma diferença mínima em relação aos pontos de extremidade quando você trabalha com as funções Web e de trabalho.</span><span class="sxs-lookup"><span data-stu-id="0e370-127">There is one minor difference with endpoints when working with both worker and web roles.</span></span> <span data-ttu-id="0e370-128">A função Web deve ter pelo menos um ponto de extremidade de entrada único usando o protocolo **HTTP** .</span><span class="sxs-lookup"><span data-stu-id="0e370-128">The web role must have at minimum a single input endpoint using the **HTTP** protocol.</span></span>

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
  <!-- more endpoints may be declared after the first InputEndPoint -->
</Endpoints>
```

## <a name="using-the-net-sdk-to-access-an-endpoint"></a><span data-ttu-id="0e370-129">Usando o SDK do .NET para acessar um ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="0e370-129">Using the .NET SDK to access an endpoint</span></span>
<span data-ttu-id="0e370-130">A Biblioteca Gerenciada do Azure fornece métodos para que instâncias de função se comuniquem no tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="0e370-130">The Azure Managed Library provides methods for role instances to communicate at runtime.</span></span> <span data-ttu-id="0e370-131">A partir da execução de código em uma instância de função, você poderá recuperar informações sobre a existência de outras instâncias de função e de seus pontos de extremidade, bem como informações sobre a instância de função atual.</span><span class="sxs-lookup"><span data-stu-id="0e370-131">From code running within a role instance, you can retrieve information about the existence of other role instances and their endpoints, as well as information about the current role instance.</span></span>

> [!NOTE]
> <span data-ttu-id="0e370-132">Você só pode recuperar informações sobre instâncias de função que estejam sendo executadas em seu serviço de nuvem e que definam pelo menos um ponto de extremidade interno.</span><span class="sxs-lookup"><span data-stu-id="0e370-132">You can only retrieve information about role instances that are running in your cloud service and that define at least one internal endpoint.</span></span> <span data-ttu-id="0e370-133">Não é possível obter dados sobre instâncias de função que estejam sendo executadas em um serviço diferente.</span><span class="sxs-lookup"><span data-stu-id="0e370-133">You cannot obtain data about role instances running in a different service.</span></span>
> 
> 

<span data-ttu-id="0e370-134">Você pode usar a propriedade [Instances](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) para recuperar instâncias de uma função.</span><span class="sxs-lookup"><span data-stu-id="0e370-134">You can use the [Instances](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) property to retrieve instances of a role.</span></span> <span data-ttu-id="0e370-135">Primeiro use [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) para retornar uma referência à instância de função atual e use a propriedade [Role](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) para retornar uma referência à função propriamente dita.</span><span class="sxs-lookup"><span data-stu-id="0e370-135">First use the [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) to return a reference to the current role instance, and then use the [Role](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) property to return a reference to the role itself.</span></span>

<span data-ttu-id="0e370-136">Quando você se conecta a uma instância de função programaticamente por meio do SDK do .NET, é relativamente fácil de acessar as informações do ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="0e370-136">When you connect to a role instance programmatically through the .NET SDK, it's relatively easy to access the endpoint information.</span></span> <span data-ttu-id="0e370-137">Por exemplo, depois que você tiver se conectado a um ambiente de função específico, poderá obter a porta de um ponto de extremidade específico com este código:</span><span class="sxs-lookup"><span data-stu-id="0e370-137">For example, after you've already connected to a specific role environment, you can get the port of a specific endpoint with this code:</span></span>

```csharp
int port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["StandardWeb"].IPEndpoint.Port;
```

<span data-ttu-id="0e370-138">A propriedade **Instances** retorna uma coleção de objetos **RoleInstance**.</span><span class="sxs-lookup"><span data-stu-id="0e370-138">The **Instances** property returns a collection of **RoleInstance** objects.</span></span> <span data-ttu-id="0e370-139">Esta coleção sempre contém a instância atual.</span><span class="sxs-lookup"><span data-stu-id="0e370-139">This collection always contains the current instance.</span></span> <span data-ttu-id="0e370-140">Se a função não definir um ponto de extremidade interno, a coleção incluirá a instância atual, mas nenhuma outra instância.</span><span class="sxs-lookup"><span data-stu-id="0e370-140">If the role does not define an internal endpoint, the collection includes the current instance but no other instances.</span></span> <span data-ttu-id="0e370-141">O número de instâncias de função na coleção sempre será 1 quando nenhum ponto de extremidade interno for definido para a função.</span><span class="sxs-lookup"><span data-stu-id="0e370-141">The number of role instances in the collection will always be 1 in the case where no internal endpoint is defined for the role.</span></span> <span data-ttu-id="0e370-142">Se a função definir um ponto de extremidade interno, suas instâncias serão descobríveis no tempo de execução e o número de instâncias na coleção corresponderá ao número de instâncias especificadas para a função no arquivo de configuração de serviço.</span><span class="sxs-lookup"><span data-stu-id="0e370-142">If the role defines an internal endpoint, its instances are discoverable at runtime, and the number of instances in the collection will correspond to the number of instances specified for the role in the service configuration file.</span></span>

> [!NOTE]
> <span data-ttu-id="0e370-143">A Biblioteca Gerenciada do Azure não oferece um meio de determinar a integridade de outras instâncias de função, mas você pode implementar essas avaliações de integridade caso o serviço precise dessa funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="0e370-143">The Azure Managed Library does not provide a means of determining the health of other role instances, but you can implement such health assessments yourself if your service needs this functionality.</span></span> <span data-ttu-id="0e370-144">Você pode usar o [Diagnóstico do Azure](cloud-services-dotnet-diagnostics.md) para obter informações sobre  as instâncias de função em execução.</span><span class="sxs-lookup"><span data-stu-id="0e370-144">You can use [Azure Diagnostics](cloud-services-dotnet-diagnostics.md) to obtain information about running role instances.</span></span>
> 
> 

<span data-ttu-id="0e370-145">Para determinar o número da porta de um ponto de extremidade interno em uma instância de função, você poderá usar a propriedade [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) para retornar um objeto de Dicionário que contenha nomes de ponto de extremidade e seus endereços IP e portas correspondentes.</span><span class="sxs-lookup"><span data-stu-id="0e370-145">To determine the port number for an internal endpoint on a role instance, you can use the [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) property to return a Dictionary object that contains endpoint names and their corresponding IP addresses and ports.</span></span> <span data-ttu-id="0e370-146">A propriedade [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) retorna o endereço IP e a porta de um ponto de extremidade especificado.</span><span class="sxs-lookup"><span data-stu-id="0e370-146">The [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) property returns the IP address and port for a specified endpoint.</span></span> <span data-ttu-id="0e370-147">A propriedade **PublicIPEndpoint** retorna a porta de um ponto de extremidade com balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="0e370-147">The **PublicIPEndpoint** property returns the port for a load balanced endpoint.</span></span> <span data-ttu-id="0e370-148">A parte do endereço IP da propriedade **PublicIPEndpoint** não é usada.</span><span class="sxs-lookup"><span data-stu-id="0e370-148">The IP address portion of the **PublicIPEndpoint** property is not used.</span></span>

<span data-ttu-id="0e370-149">Veja um exemplo que itera instâncias de função.</span><span class="sxs-lookup"><span data-stu-id="0e370-149">Here is an example that iterates role instances.</span></span>

```csharp
foreach (RoleInstance roleInst in RoleEnvironment.CurrentRoleInstance.Role.Instances)
{
    Trace.WriteLine("Instance ID: " + roleInst.Id);
    foreach (RoleInstanceEndpoint roleInstEndpoint in roleInst.InstanceEndpoints.Values)
    {
        Trace.WriteLine("Instance endpoint IP address and port: " + roleInstEndpoint.IPEndpoint);
    }
}
```

<span data-ttu-id="0e370-150">Veja um exemplo de função de trabalho que expõe o ponto de extremidade por meio da definição de serviço e começa a escutar conexões.</span><span class="sxs-lookup"><span data-stu-id="0e370-150">Here is an example of a worker role that gets the endpoint exposed through the service definition and starts listening for connections.</span></span>

> [!WARNING]
> <span data-ttu-id="0e370-151">Este código só funcionará para um serviço implantado.</span><span class="sxs-lookup"><span data-stu-id="0e370-151">This code will only work for a deployed service.</span></span> <span data-ttu-id="0e370-152">Quando executados no Emulador de Computação do Azure, os elementos de configuração de serviço que criam pontos de extremidade de porta direta (elementos**InstanceInputEndpoint** ) são ignorados.</span><span class="sxs-lookup"><span data-stu-id="0e370-152">When running in the Azure Compute Emulator, service configuration elements that create direct port endpoints (**InstanceInputEndpoint** elements) are ignored.</span></span>
> 
> 

```csharp
using System;
using System.Diagnostics;
using System.Linq;
using System.Net;
using System.Net.Sockets;
using System.Threading;
using Microsoft.WindowsAzure;
using Microsoft.WindowsAzure.Diagnostics;
using Microsoft.WindowsAzure.ServiceRuntime;
using Microsoft.WindowsAzure.StorageClient;

namespace WorkerRole1
{
  public class WorkerRole : RoleEntryPoint
  {
    public override void Run()
    {
      try
      {
        // Initialize method-wide variables
        var epName = "Endpoint1";
        var roleInstance = RoleEnvironment.CurrentRoleInstance;

        // Identify direct communication port
        var myPublicEp = roleInstance.InstanceEndpoints[epName].PublicIPEndpoint;
        Trace.TraceInformation("IP:{0}, Port:{1}", myPublicEp.Address, myPublicEp.Port);

        // Identify public endpoint
        var myInternalEp = roleInstance.InstanceEndpoints[epName].IPEndpoint;

        // Create socket listener
        var listener = new Socket(
          myInternalEp.AddressFamily, SocketType.Stream, ProtocolType.Tcp);

        // Bind socket listener to internal endpoint and listen
        listener.Bind(myInternalEp);
        listener.Listen(10);
        Trace.TraceInformation("Listening on IP:{0},Port: {1}",
          myInternalEp.Address, myInternalEp.Port);

        while (true)
        {
          // Block the thread and wait for a client request
          Socket handler = listener.Accept();
          Trace.TraceInformation("Client request received.");

          // Define body of socket handler
          var handlerThread = new Thread(
            new ParameterizedThreadStart(h =>
            {
              var socket = h as Socket;
              Trace.TraceInformation("Local:{0} Remote{1}",
                socket.LocalEndPoint, socket.RemoteEndPoint);

              // Shut down and close socket
              socket.Shutdown(SocketShutdown.Both);
              socket.Close();
            }
          ));

          // Start socket handler on new thread
          handlerThread.Start(handler);
        }
      }
      catch (Exception e)
      {
        Trace.TraceError("Caught exception in run. Details: {0}", e);
      }
    }

    public override bool OnStart()
    {
      // Set the maximum number of concurrent connections 
      ServicePointManager.DefaultConnectionLimit = 12;

      // For information on handling configuration changes
      // see the MSDN topic at http://go.microsoft.com/fwlink/?LinkId=166357.
      return base.OnStart();
    }
  }
}
```

## <a name="network-traffic-rules-to-control-role-communication"></a><span data-ttu-id="0e370-153">Regras de tráfego de rede para controlar a comunicação de função</span><span class="sxs-lookup"><span data-stu-id="0e370-153">Network traffic rules to control role communication</span></span>
<span data-ttu-id="0e370-154">Depois de definir pontos de extremidade internos, você poderá adicionar regras de tráfego de rede (com base nos pontos de extremidade que você criou) para controlar como as instâncias de função podem se comunicar umas com os outras.</span><span class="sxs-lookup"><span data-stu-id="0e370-154">After you define internal endpoints, you can add network traffic rules (based on the endpoints that you created) to control how role instances can communicate with each other.</span></span> <span data-ttu-id="0e370-155">O diagrama a seguir mostra alguns cenários comuns para o controle da comunicação de função:</span><span class="sxs-lookup"><span data-stu-id="0e370-155">The following diagram shows some common scenarios for controlling role communication:</span></span>

<span data-ttu-id="0e370-156">![Cenários de Regras de tráfego de rede](./media/cloud-services-enable-communication-role-instances/scenarios.png "Cenários de Regras de tráfego de rede")</span><span class="sxs-lookup"><span data-stu-id="0e370-156">![Network Traffic Rules Scenarios](./media/cloud-services-enable-communication-role-instances/scenarios.png "Network Traffic Rules Scenarios")</span></span>

<span data-ttu-id="0e370-157">O exemplo de código a seguir mostra as definições de função das funções mostradas no diagrama anterior.</span><span class="sxs-lookup"><span data-stu-id="0e370-157">The following code example shows role definitions for the roles shown in the previous diagram.</span></span> <span data-ttu-id="0e370-158">Cada definição de função inclui pelo menos um ponto de extremidade interno definido:</span><span class="sxs-lookup"><span data-stu-id="0e370-158">Each role definition includes at least one internal endpoint defined:</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WebRole name="WebRole1" vmsize="Medium">
    <Sites>
      <Site name="Web">
        <Bindings>
          <Binding name="HttpIn" endpointName="HttpIn" />
        </Bindings>
      </Site>
    </Sites>
    <Endpoints>
      <InputEndpoint name="HttpIn" protocol="http" port="80" />
      <InternalEndpoint name="InternalTCP1" protocol="tcp" />
    </Endpoints>
  </WebRole>
  <WorkerRole name="WorkerRole1">
    <Endpoints>
      <InternalEndpoint name="InternalTCP2" protocol="tcp" />
    </Endpoints>
  </WorkerRole>
  <WorkerRole name="WorkerRole2">
    <Endpoints>
      <InternalEndpoint name="InternalTCP3" protocol="tcp" />
      <InternalEndpoint name="InternalTCP4" protocol="tcp" />
    </Endpoints>
  </WorkerRole>
</ServiceDefinition>
```

> [!NOTE]
> <span data-ttu-id="0e370-159">A restrição de comunicação entre funções pode ocorrer com pontos de extremidade internos de portas fixas e atribuídas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="0e370-159">Restriction of communication between roles can occur with internal endpoints of both fixed and automatically assigned ports.</span></span>
> 
> 

<span data-ttu-id="0e370-160">Por padrão, após a definição de um ponto de extremidade interno, a comunicação poderá fluir de qualquer função para o ponto de extremidade interno de uma função sem qualquer restrição.</span><span class="sxs-lookup"><span data-stu-id="0e370-160">By default, after an internal endpoint is defined, communication can flow from any role to the internal endpoint of a role without any restrictions.</span></span> <span data-ttu-id="0e370-161">Para restringir a comunicação, você deverá adicionar um elemento **NetworkTrafficRules** ao elemento **ServiceDefinition** no arquivo de definição de serviço.</span><span class="sxs-lookup"><span data-stu-id="0e370-161">To restrict communication, you must add a **NetworkTrafficRules** element to the **ServiceDefinition** element in the service definition file.</span></span>

### <a name="scenario-1"></a><span data-ttu-id="0e370-162">Cenário 1</span><span class="sxs-lookup"><span data-stu-id="0e370-162">Scenario 1</span></span>
<span data-ttu-id="0e370-163">Permita apenas o tráfego de rede de **WebRole1** para **WorkerRole1**.</span><span class="sxs-lookup"><span data-stu-id="0e370-163">Only allow network traffic from **WebRole1** to **WorkerRole1**.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP2" roleName="WorkerRole1"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
</ServiceDefinition>
```

### <a name="scenario-2"></a><span data-ttu-id="0e370-164">Cenário 2</span><span class="sxs-lookup"><span data-stu-id="0e370-164">Scenario 2</span></span>
<span data-ttu-id="0e370-165">Permita apenas o tráfego de rede de **WebRole1** para **WorkerRole1** e **WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="0e370-165">Only allows network traffic from **WebRole1** to **WorkerRole1** and **WorkerRole2**.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP2" roleName="WorkerRole1"/>
        <RoleEndpoint endpointName="InternalTCP3" roleName="WorkerRole2"/>
      </Destinations>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
</ServiceDefinition>
```

### <a name="scenario-3"></a><span data-ttu-id="0e370-166">Cenário 3</span><span class="sxs-lookup"><span data-stu-id="0e370-166">Scenario 3</span></span>
<span data-ttu-id="0e370-167">Permita apenas o tráfego de rede de **WebRole1** para **WorkerRole1** e de **WorkerRole1** para **WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="0e370-167">Only allows network traffic from **WebRole1** to **WorkerRole1**, and **WorkerRole1** to **WorkerRole2**.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP2" roleName="WorkerRole1"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP3" roleName="WorkerRole2"/>
      </Destinations>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WorkerRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
</ServiceDefinition>
```

### <a name="scenario-4"></a><span data-ttu-id="0e370-168">Cenário 4</span><span class="sxs-lookup"><span data-stu-id="0e370-168">Scenario 4</span></span>
<span data-ttu-id="0e370-169">Permita apenas o tráfego de rede de **WebRole1** para **WorkerRole1**, de **WebRole1** para **WorkerRole2** e de **WorkerRole1** para **WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="0e370-169">Only allows network traffic from **WebRole1** to **WorkerRole1**, **WebRole1** to **WorkerRole2**, and **WorkerRole1** to **WorkerRole2**.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP2" roleName="WorkerRole1"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo >
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP3" roleName="WorkerRole2"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WorkerRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo >
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP4" roleName="WorkerRole2"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
</ServiceDefinition>
```

<span data-ttu-id="0e370-170">Veja uma referência de esquema XML para os elementos usados acima [aqui](https://msdn.microsoft.com/library/azure/gg557551.aspx).</span><span class="sxs-lookup"><span data-stu-id="0e370-170">An XML schema reference for the elements used above can be found [here](https://msdn.microsoft.com/library/azure/gg557551.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e370-171">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0e370-171">Next steps</span></span>
<span data-ttu-id="0e370-172">Leia mais sobre o [modelo](cloud-services-model-and-package.md)de Serviço de Nuvem.</span><span class="sxs-lookup"><span data-stu-id="0e370-172">Read more about the Cloud Service [model](cloud-services-model-and-package.md).</span></span>

