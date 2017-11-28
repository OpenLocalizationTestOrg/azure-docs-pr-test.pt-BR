---
title: "aaaCommunication para funções em serviços de nuvem | Microsoft Docs"
description: "Instâncias de função em serviços de nuvem podem ter pontos de extremidade (http, https, tcp, udp) definidos para eles que se comunicam com hello fora ou entre outras instâncias de função."
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
ms.openlocfilehash: 1fb39215ceb8a3f0381ef5e108c1149de115ff8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-communication-for-role-instances-in-azure"></a><span data-ttu-id="7075d-103">Habilitar a comunicação para instâncias de função no Azure</span><span class="sxs-lookup"><span data-stu-id="7075d-103">Enable communication for role instances in azure</span></span>
<span data-ttu-id="7075d-104">As funções de serviço de nuvem se comunicam por meio de conexões internas e externas.</span><span class="sxs-lookup"><span data-stu-id="7075d-104">Cloud service roles communicate through internal and external connections.</span></span> <span data-ttu-id="7075d-105">As conexões externas são chamadas de **pontos de extremidade de entrada**, enquanto as conexões internas são chamadas de **pontos de extremidade internos**.</span><span class="sxs-lookup"><span data-stu-id="7075d-105">External connections are called **input endpoints** while internal connections are called **internal endpoints**.</span></span> <span data-ttu-id="7075d-106">Este tópico descreve como Olá toomodify [definição de serviço](cloud-services-model-and-package.md#csdef) toocreate pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="7075d-106">This topic describes how toomodify hello [service definition](cloud-services-model-and-package.md#csdef) toocreate endpoints.</span></span>

## <a name="input-endpoint"></a><span data-ttu-id="7075d-107">Ponto de extremidade de entrada</span><span class="sxs-lookup"><span data-stu-id="7075d-107">Input endpoint</span></span>
<span data-ttu-id="7075d-108">ponto de extremidade de entrada Hello é usado quando você deseja tooexpose toohello uma porta fora.</span><span class="sxs-lookup"><span data-stu-id="7075d-108">hello input endpoint is used when you want tooexpose a port toohello outside.</span></span> <span data-ttu-id="7075d-109">Especifique o tipo de protocolo hello e porta de saudação do ponto de extremidade de saudação que aplica-se para as duas portas de saudação interno e externo para o ponto de extremidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="7075d-109">You specify hello protocol type and hello port of hello endpoint which then applies for both hello external and internal ports for hello endpoint.</span></span> <span data-ttu-id="7075d-110">Se desejar, você pode especificar uma porta interna diferente para o ponto de extremidade de saudação com hello [localPort](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) atributo.</span><span class="sxs-lookup"><span data-stu-id="7075d-110">If you want, you can specify a different internal port for hello endpoint with hello [localPort](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) attribute.</span></span>

<span data-ttu-id="7075d-111">ponto de extremidade de entrada Hello pode usar Olá seguintes protocolos: **http, https, tcp, udp**.</span><span class="sxs-lookup"><span data-stu-id="7075d-111">hello input endpoint can use hello following protocols: **http, https, tcp, udp**.</span></span>

<span data-ttu-id="7075d-112">toocreate um ponto de extremidade de entrada, adicionar Olá **InputEndpoint** toohello de elemento filho **pontos de extremidade** elemento de função de um trabalho ou web.</span><span class="sxs-lookup"><span data-stu-id="7075d-112">toocreate an input endpoint, add hello **InputEndpoint** child element toohello **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
</Endpoints> 
```

## <a name="instance-input-endpoint"></a><span data-ttu-id="7075d-113">Ponto de extremidade de entrada de instância</span><span class="sxs-lookup"><span data-stu-id="7075d-113">Instance input endpoint</span></span>
<span data-ttu-id="7075d-114">Entrada pontos de extremidade de instância são pontos de extremidade tooinput semelhantes, mas permite mapear portas específicas de público para cada instância de função individuais usando o encaminhamento de porta no balanceador de carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="7075d-114">Instance input endpoints are similar tooinput endpoints but allows you map specific public-facing ports for each individual role instance by using port forwarding on hello load balancer.</span></span> <span data-ttu-id="7075d-115">Você pode especificar uma única porta voltada para o público ou um intervalo de portas.</span><span class="sxs-lookup"><span data-stu-id="7075d-115">You can specify a single public-facing port, or a range of ports.</span></span>

<span data-ttu-id="7075d-116">ponto de extremidade entrada Hello instância só pode usar **tcp** ou **udp** como protocolo de saudação.</span><span class="sxs-lookup"><span data-stu-id="7075d-116">hello instance input endpoint can only use **tcp** or **udp** as hello protocol.</span></span>

<span data-ttu-id="7075d-117">toocreate ponto de extremidade de entrada um instância, adicionar Olá **InstanceInputEndpoint** toohello de elemento filho **pontos de extremidade** elemento de função de um trabalho ou web.</span><span class="sxs-lookup"><span data-stu-id="7075d-117">toocreate an instance input endpoint, add hello **InstanceInputEndpoint** child element toohello **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InstanceInputEndpoint name="Endpoint2" protocol="tcp" localPort="10100">
    <AllocatePublicPortFrom>
      <FixedPortRange max="10109" min="10105" />
    </AllocatePublicPortFrom>
  </InstanceInputEndpoint>
</Endpoints>
```

## <a name="internal-endpoint"></a><span data-ttu-id="7075d-118">Ponto de extremidade interno</span><span class="sxs-lookup"><span data-stu-id="7075d-118">Internal endpoint</span></span>
<span data-ttu-id="7075d-119">Os pontos de extremidade internos estão disponíveis para a comunicação entre instâncias.</span><span class="sxs-lookup"><span data-stu-id="7075d-119">Internal endpoints are available for instance-to-instance communication.</span></span> <span data-ttu-id="7075d-120">Olá porta é opcional e se ele for omitido, uma porta dinâmica é atribuída toohello de ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="7075d-120">hello port is optional and if omitted, a dynamic port is assigned toohello endpoint.</span></span> <span data-ttu-id="7075d-121">Um intervalo de portas pode ser usado.</span><span class="sxs-lookup"><span data-stu-id="7075d-121">A port range can be used.</span></span> <span data-ttu-id="7075d-122">Há um limite de cinco pontos de extremidade internos por função.</span><span class="sxs-lookup"><span data-stu-id="7075d-122">There is a limit of five internal endpoints per role.</span></span>

<span data-ttu-id="7075d-123">ponto de extremidade interno Olá pode usar Olá seguintes protocolos: **http, tcp, udp, qualquer**.</span><span class="sxs-lookup"><span data-stu-id="7075d-123">hello internal endpoint can use hello following protocols: **http, tcp, udp, any**.</span></span>

<span data-ttu-id="7075d-124">toocreate um ponto de extremidade de entrada interno, adicionar Olá **InternalEndpoint** toohello de elemento filho **pontos de extremidade** elemento de função de um trabalho ou web.</span><span class="sxs-lookup"><span data-stu-id="7075d-124">toocreate an internal input endpoint, add hello **InternalEndpoint** child element toohello **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any" port="8999" />
</Endpoints> 
```

<span data-ttu-id="7075d-125">Você também pode usar um intervalo de portas.</span><span class="sxs-lookup"><span data-stu-id="7075d-125">You can also use a port range.</span></span>

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any">
    <FixedPortRange max="8995" min="8999" />
  </InternalEndpoint>
</Endpoints>
```


## <a name="worker-roles-vs-web-roles"></a><span data-ttu-id="7075d-126">Funções de trabalho versus Funções da Web</span><span class="sxs-lookup"><span data-stu-id="7075d-126">Worker roles vs. Web roles</span></span>
<span data-ttu-id="7075d-127">Há uma diferença mínima em relação aos pontos de extremidade quando você trabalha com as funções Web e de trabalho.</span><span class="sxs-lookup"><span data-stu-id="7075d-127">There is one minor difference with endpoints when working with both worker and web roles.</span></span> <span data-ttu-id="7075d-128">Olá função web deve ter pelo menos um ponto de extremidade de entrada único usando Olá **HTTP** protocolo.</span><span class="sxs-lookup"><span data-stu-id="7075d-128">hello web role must have at minimum a single input endpoint using hello **HTTP** protocol.</span></span>

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
  <!-- more endpoints may be declared after hello first InputEndPoint -->
</Endpoints>
```

## <a name="using-hello-net-sdk-tooaccess-an-endpoint"></a><span data-ttu-id="7075d-129">Usando o SDK .NET de saudação tooaccess um ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="7075d-129">Using hello .NET SDK tooaccess an endpoint</span></span>
<span data-ttu-id="7075d-130">Olá biblioteca gerenciada do Azure fornece métodos para toocommunicate de instâncias de função em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="7075d-130">hello Azure Managed Library provides methods for role instances toocommunicate at runtime.</span></span> <span data-ttu-id="7075d-131">Código em execução dentro de uma instância de função, você pode recuperar informações sobre a existência de saudação de outras instâncias de função e seus pontos de extremidade, bem como informações sobre a instância de função atual da saudação.</span><span class="sxs-lookup"><span data-stu-id="7075d-131">From code running within a role instance, you can retrieve information about hello existence of other role instances and their endpoints, as well as information about hello current role instance.</span></span>

> [!NOTE]
> <span data-ttu-id="7075d-132">Você só pode recuperar informações sobre instâncias de função que estejam sendo executadas em seu serviço de nuvem e que definam pelo menos um ponto de extremidade interno.</span><span class="sxs-lookup"><span data-stu-id="7075d-132">You can only retrieve information about role instances that are running in your cloud service and that define at least one internal endpoint.</span></span> <span data-ttu-id="7075d-133">Não é possível obter dados sobre instâncias de função que estejam sendo executadas em um serviço diferente.</span><span class="sxs-lookup"><span data-stu-id="7075d-133">You cannot obtain data about role instances running in a different service.</span></span>
> 
> 

<span data-ttu-id="7075d-134">Você pode usar o hello [instâncias](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) instâncias de tooretrieve de propriedade de uma função.</span><span class="sxs-lookup"><span data-stu-id="7075d-134">You can use hello [Instances](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) property tooretrieve instances of a role.</span></span> <span data-ttu-id="7075d-135">Primeiro use Olá [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) tooreturn uma função atual do toohello de referência da instância e, em seguida, usar o hello [função](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) propriedade tooreturn uma função de toohello de referência em si.</span><span class="sxs-lookup"><span data-stu-id="7075d-135">First use hello [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) tooreturn a reference toohello current role instance, and then use hello [Role](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) property tooreturn a reference toohello role itself.</span></span>

<span data-ttu-id="7075d-136">Quando você conectar instância de função tooa programaticamente por meio de saudação SDK .NET, é relativamente fácil tooaccess informações de ponto de extremidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="7075d-136">When you connect tooa role instance programmatically through hello .NET SDK, it's relatively easy tooaccess hello endpoint information.</span></span> <span data-ttu-id="7075d-137">Por exemplo, depois que você já conectou tooa ambiente de função específica, você pode obter a porta Olá de um ponto de extremidade específico com este código:</span><span class="sxs-lookup"><span data-stu-id="7075d-137">For example, after you've already connected tooa specific role environment, you can get hello port of a specific endpoint with this code:</span></span>

```csharp
int port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["StandardWeb"].IPEndpoint.Port;
```

<span data-ttu-id="7075d-138">Olá **instâncias** propriedade retorna uma coleção de **RoleInstance** objetos.</span><span class="sxs-lookup"><span data-stu-id="7075d-138">hello **Instances** property returns a collection of **RoleInstance** objects.</span></span> <span data-ttu-id="7075d-139">Essa coleção sempre contém a instância atual do hello.</span><span class="sxs-lookup"><span data-stu-id="7075d-139">This collection always contains hello current instance.</span></span> <span data-ttu-id="7075d-140">Se a função hello não definir um ponto de extremidade interno, a coleção de Olá inclui a instância atual do hello, mas nenhuma outra instância.</span><span class="sxs-lookup"><span data-stu-id="7075d-140">If hello role does not define an internal endpoint, hello collection includes hello current instance but no other instances.</span></span> <span data-ttu-id="7075d-141">número de saudação de instâncias de função na coleção de saudação sempre será 1 em caso de Olá onde nenhum ponto de extremidade interno é definido para a função hello.</span><span class="sxs-lookup"><span data-stu-id="7075d-141">hello number of role instances in hello collection will always be 1 in hello case where no internal endpoint is defined for hello role.</span></span> <span data-ttu-id="7075d-142">Se a função hello define um ponto de extremidade interno, suas instâncias serão detectáveis em tempo de execução e número de saudação de instâncias na coleção de saudação corresponderá toohello número de instâncias especificado para a função hello no arquivo de configuração do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="7075d-142">If hello role defines an internal endpoint, its instances are discoverable at runtime, and hello number of instances in hello collection will correspond toohello number of instances specified for hello role in hello service configuration file.</span></span>

> [!NOTE]
> <span data-ttu-id="7075d-143">Olá biblioteca gerenciada do Azure não fornece um meio de determinar a integridade de saudação de outras instâncias de função, mas você pode implementar essas avaliações de integridade se seu serviço precisar desta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="7075d-143">hello Azure Managed Library does not provide a means of determining hello health of other role instances, but you can implement such health assessments yourself if your service needs this functionality.</span></span> <span data-ttu-id="7075d-144">Você pode usar [diagnóstico do Azure](cloud-services-dotnet-diagnostics.md) tooobtain informações sobre a execução de instâncias de função.</span><span class="sxs-lookup"><span data-stu-id="7075d-144">You can use [Azure Diagnostics](cloud-services-dotnet-diagnostics.md) tooobtain information about running role instances.</span></span>
> 
> 

<span data-ttu-id="7075d-145">número da porta toodetermine Olá para um ponto de extremidade interno em uma instância de função, você pode usar o hello [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) tooreturn de propriedade endereços de um objeto de dicionário que contém nomes de ponto de extremidade e seu IP correspondente e portas.</span><span class="sxs-lookup"><span data-stu-id="7075d-145">toodetermine hello port number for an internal endpoint on a role instance, you can use hello [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) property tooreturn a Dictionary object that contains endpoint names and their corresponding IP addresses and ports.</span></span> <span data-ttu-id="7075d-146">Olá [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) propriedade retorna o endereço IP hello e a porta para um ponto de extremidade especificado.</span><span class="sxs-lookup"><span data-stu-id="7075d-146">hello [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) property returns hello IP address and port for a specified endpoint.</span></span> <span data-ttu-id="7075d-147">Olá **PublicIPEndpoint** propriedade retorna porta Olá para um ponto de extremidade com balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="7075d-147">hello **PublicIPEndpoint** property returns hello port for a load balanced endpoint.</span></span> <span data-ttu-id="7075d-148">parte do endereço IP de saudação do hello **PublicIPEndpoint** propriedade não é usada.</span><span class="sxs-lookup"><span data-stu-id="7075d-148">hello IP address portion of hello **PublicIPEndpoint** property is not used.</span></span>

<span data-ttu-id="7075d-149">Veja um exemplo que itera instâncias de função.</span><span class="sxs-lookup"><span data-stu-id="7075d-149">Here is an example that iterates role instances.</span></span>

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

<span data-ttu-id="7075d-150">Aqui está um exemplo de uma função de trabalho que obtém o ponto de extremidade de saudação exposto por meio da definição de serviço hello e começa a escuta de conexões.</span><span class="sxs-lookup"><span data-stu-id="7075d-150">Here is an example of a worker role that gets hello endpoint exposed through hello service definition and starts listening for connections.</span></span>

> [!WARNING]
> <span data-ttu-id="7075d-151">Este código só funcionará para um serviço implantado.</span><span class="sxs-lookup"><span data-stu-id="7075d-151">This code will only work for a deployed service.</span></span> <span data-ttu-id="7075d-152">Quando em execução no emulador de computação do Azure de saudação, elementos de configuração que criar pontos de extremidade de porta direta de serviço (**InstanceInputEndpoint** elementos) são ignorados.</span><span class="sxs-lookup"><span data-stu-id="7075d-152">When running in hello Azure Compute Emulator, service configuration elements that create direct port endpoints (**InstanceInputEndpoint** elements) are ignored.</span></span>
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

        // Bind socket listener toointernal endpoint and listen
        listener.Bind(myInternalEp);
        listener.Listen(10);
        Trace.TraceInformation("Listening on IP:{0},Port: {1}",
          myInternalEp.Address, myInternalEp.Port);

        while (true)
        {
          // Block hello thread and wait for a client request
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
      // Set hello maximum number of concurrent connections 
      ServicePointManager.DefaultConnectionLimit = 12;

      // For information on handling configuration changes
      // see hello MSDN topic at http://go.microsoft.com/fwlink/?LinkId=166357.
      return base.OnStart();
    }
  }
}
```

## <a name="network-traffic-rules-toocontrol-role-communication"></a><span data-ttu-id="7075d-153">Comunicação de função de toocontrol de regras de tráfego de rede</span><span class="sxs-lookup"><span data-stu-id="7075d-153">Network traffic rules toocontrol role communication</span></span>
<span data-ttu-id="7075d-154">Depois de definir pontos de extremidade internos, você pode adicionar toocontrol de regras (com base em pontos de extremidade de saudação que você criou) de tráfego de rede como instâncias de função podem se comunicar uns com os outros.</span><span class="sxs-lookup"><span data-stu-id="7075d-154">After you define internal endpoints, you can add network traffic rules (based on hello endpoints that you created) toocontrol how role instances can communicate with each other.</span></span> <span data-ttu-id="7075d-155">Olá diagrama a seguir mostra alguns cenários comuns para controlar a comunicação de função:</span><span class="sxs-lookup"><span data-stu-id="7075d-155">hello following diagram shows some common scenarios for controlling role communication:</span></span>

<span data-ttu-id="7075d-156">![Cenários de Regras de tráfego de rede](./media/cloud-services-enable-communication-role-instances/scenarios.png "Cenários de Regras de tráfego de rede")</span><span class="sxs-lookup"><span data-stu-id="7075d-156">![Network Traffic Rules Scenarios](./media/cloud-services-enable-communication-role-instances/scenarios.png "Network Traffic Rules Scenarios")</span></span>

<span data-ttu-id="7075d-157">Olá, exemplo de código a seguir mostra definições de função para funções hello mostradas no diagrama anterior hello.</span><span class="sxs-lookup"><span data-stu-id="7075d-157">hello following code example shows role definitions for hello roles shown in hello previous diagram.</span></span> <span data-ttu-id="7075d-158">Cada definição de função inclui pelo menos um ponto de extremidade interno definido:</span><span class="sxs-lookup"><span data-stu-id="7075d-158">Each role definition includes at least one internal endpoint defined:</span></span>

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
> <span data-ttu-id="7075d-159">A restrição de comunicação entre funções pode ocorrer com pontos de extremidade internos de portas fixas e atribuídas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="7075d-159">Restriction of communication between roles can occur with internal endpoints of both fixed and automatically assigned ports.</span></span>
> 
> 

<span data-ttu-id="7075d-160">Por padrão, após a definição de um ponto de extremidade interno, comunicação pode fluir de qualquer função toohello ponto de extremidade interno de uma função sem nenhuma restrição.</span><span class="sxs-lookup"><span data-stu-id="7075d-160">By default, after an internal endpoint is defined, communication can flow from any role toohello internal endpoint of a role without any restrictions.</span></span> <span data-ttu-id="7075d-161">comunicação toorestrict, você deve adicionar um **NetworkTrafficRules** elemento toohello **ServiceDefinition** elemento no arquivo de definição de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="7075d-161">toorestrict communication, you must add a **NetworkTrafficRules** element toohello **ServiceDefinition** element in hello service definition file.</span></span>

### <a name="scenario-1"></a><span data-ttu-id="7075d-162">Cenário 1</span><span class="sxs-lookup"><span data-stu-id="7075d-162">Scenario 1</span></span>
<span data-ttu-id="7075d-163">Permitir somente o tráfego de rede de **WebRole1** muito**WorkerRole1**.</span><span class="sxs-lookup"><span data-stu-id="7075d-163">Only allow network traffic from **WebRole1** too**WorkerRole1**.</span></span>

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

### <a name="scenario-2"></a><span data-ttu-id="7075d-164">Cenário 2</span><span class="sxs-lookup"><span data-stu-id="7075d-164">Scenario 2</span></span>
<span data-ttu-id="7075d-165">Permite apenas o tráfego de rede de **WebRole1** muito**WorkerRole1** e **WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="7075d-165">Only allows network traffic from **WebRole1** too**WorkerRole1** and **WorkerRole2**.</span></span>

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

### <a name="scenario-3"></a><span data-ttu-id="7075d-166">Cenário 3</span><span class="sxs-lookup"><span data-stu-id="7075d-166">Scenario 3</span></span>
<span data-ttu-id="7075d-167">Permite apenas o tráfego de rede de **WebRole1** muito**WorkerRole1**, e **WorkerRole1** muito**WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="7075d-167">Only allows network traffic from **WebRole1** too**WorkerRole1**, and **WorkerRole1** too**WorkerRole2**.</span></span>

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

### <a name="scenario-4"></a><span data-ttu-id="7075d-168">Cenário 4</span><span class="sxs-lookup"><span data-stu-id="7075d-168">Scenario 4</span></span>
<span data-ttu-id="7075d-169">Permite apenas o tráfego de rede de **WebRole1** muito**WorkerRole1**, **WebRole1** muito**WorkerRole2**, e  **WorkerRole1** muito**WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="7075d-169">Only allows network traffic from **WebRole1** too**WorkerRole1**, **WebRole1** too**WorkerRole2**, and **WorkerRole1** too**WorkerRole2**.</span></span>

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

<span data-ttu-id="7075d-170">Uma referência de esquema XML para elementos de saudação usado acima pode ser encontrada [aqui](https://msdn.microsoft.com/library/azure/gg557551.aspx).</span><span class="sxs-lookup"><span data-stu-id="7075d-170">An XML schema reference for hello elements used above can be found [here](https://msdn.microsoft.com/library/azure/gg557551.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7075d-171">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7075d-171">Next steps</span></span>
<span data-ttu-id="7075d-172">Leia mais sobre Olá serviço de nuvem [modelo](cloud-services-model-and-package.md).</span><span class="sxs-lookup"><span data-stu-id="7075d-172">Read more about hello Cloud Service [model](cloud-services-model-and-package.md).</span></span>

