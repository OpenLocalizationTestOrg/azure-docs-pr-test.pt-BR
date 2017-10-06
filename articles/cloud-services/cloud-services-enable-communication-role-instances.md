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
# <a name="enable-communication-for-role-instances-in-azure"></a>Habilitar a comunicação para instâncias de função no Azure
As funções de serviço de nuvem se comunicam por meio de conexões internas e externas. As conexões externas são chamadas de **pontos de extremidade de entrada**, enquanto as conexões internas são chamadas de **pontos de extremidade internos**. Este tópico descreve como Olá toomodify [definição de serviço](cloud-services-model-and-package.md#csdef) toocreate pontos de extremidade.

## <a name="input-endpoint"></a>Ponto de extremidade de entrada
ponto de extremidade de entrada Hello é usado quando você deseja tooexpose toohello uma porta fora. Especifique o tipo de protocolo hello e porta de saudação do ponto de extremidade de saudação que aplica-se para as duas portas de saudação interno e externo para o ponto de extremidade de saudação. Se desejar, você pode especificar uma porta interna diferente para o ponto de extremidade de saudação com hello [localPort](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) atributo.

ponto de extremidade de entrada Hello pode usar Olá seguintes protocolos: **http, https, tcp, udp**.

toocreate um ponto de extremidade de entrada, adicionar Olá **InputEndpoint** toohello de elemento filho **pontos de extremidade** elemento de função de um trabalho ou web.

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
</Endpoints> 
```

## <a name="instance-input-endpoint"></a>Ponto de extremidade de entrada de instância
Entrada pontos de extremidade de instância são pontos de extremidade tooinput semelhantes, mas permite mapear portas específicas de público para cada instância de função individuais usando o encaminhamento de porta no balanceador de carga de saudação. Você pode especificar uma única porta voltada para o público ou um intervalo de portas.

ponto de extremidade entrada Hello instância só pode usar **tcp** ou **udp** como protocolo de saudação.

toocreate ponto de extremidade de entrada um instância, adicionar Olá **InstanceInputEndpoint** toohello de elemento filho **pontos de extremidade** elemento de função de um trabalho ou web.

```xml
<Endpoints>
  <InstanceInputEndpoint name="Endpoint2" protocol="tcp" localPort="10100">
    <AllocatePublicPortFrom>
      <FixedPortRange max="10109" min="10105" />
    </AllocatePublicPortFrom>
  </InstanceInputEndpoint>
</Endpoints>
```

## <a name="internal-endpoint"></a>Ponto de extremidade interno
Os pontos de extremidade internos estão disponíveis para a comunicação entre instâncias. Olá porta é opcional e se ele for omitido, uma porta dinâmica é atribuída toohello de ponto de extremidade. Um intervalo de portas pode ser usado. Há um limite de cinco pontos de extremidade internos por função.

ponto de extremidade interno Olá pode usar Olá seguintes protocolos: **http, tcp, udp, qualquer**.

toocreate um ponto de extremidade de entrada interno, adicionar Olá **InternalEndpoint** toohello de elemento filho **pontos de extremidade** elemento de função de um trabalho ou web.

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any" port="8999" />
</Endpoints> 
```

Você também pode usar um intervalo de portas.

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any">
    <FixedPortRange max="8995" min="8999" />
  </InternalEndpoint>
</Endpoints>
```


## <a name="worker-roles-vs-web-roles"></a>Funções de trabalho versus Funções da Web
Há uma diferença mínima em relação aos pontos de extremidade quando você trabalha com as funções Web e de trabalho. Olá função web deve ter pelo menos um ponto de extremidade de entrada único usando Olá **HTTP** protocolo.

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
  <!-- more endpoints may be declared after hello first InputEndPoint -->
</Endpoints>
```

## <a name="using-hello-net-sdk-tooaccess-an-endpoint"></a>Usando o SDK .NET de saudação tooaccess um ponto de extremidade
Olá biblioteca gerenciada do Azure fornece métodos para toocommunicate de instâncias de função em tempo de execução. Código em execução dentro de uma instância de função, você pode recuperar informações sobre a existência de saudação de outras instâncias de função e seus pontos de extremidade, bem como informações sobre a instância de função atual da saudação.

> [!NOTE]
> Você só pode recuperar informações sobre instâncias de função que estejam sendo executadas em seu serviço de nuvem e que definam pelo menos um ponto de extremidade interno. Não é possível obter dados sobre instâncias de função que estejam sendo executadas em um serviço diferente.
> 
> 

Você pode usar o hello [instâncias](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) instâncias de tooretrieve de propriedade de uma função. Primeiro use Olá [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) tooreturn uma função atual do toohello de referência da instância e, em seguida, usar o hello [função](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) propriedade tooreturn uma função de toohello de referência em si.

Quando você conectar instância de função tooa programaticamente por meio de saudação SDK .NET, é relativamente fácil tooaccess informações de ponto de extremidade de saudação. Por exemplo, depois que você já conectou tooa ambiente de função específica, você pode obter a porta Olá de um ponto de extremidade específico com este código:

```csharp
int port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["StandardWeb"].IPEndpoint.Port;
```

Olá **instâncias** propriedade retorna uma coleção de **RoleInstance** objetos. Essa coleção sempre contém a instância atual do hello. Se a função hello não definir um ponto de extremidade interno, a coleção de Olá inclui a instância atual do hello, mas nenhuma outra instância. número de saudação de instâncias de função na coleção de saudação sempre será 1 em caso de Olá onde nenhum ponto de extremidade interno é definido para a função hello. Se a função hello define um ponto de extremidade interno, suas instâncias serão detectáveis em tempo de execução e número de saudação de instâncias na coleção de saudação corresponderá toohello número de instâncias especificado para a função hello no arquivo de configuração do serviço de saudação.

> [!NOTE]
> Olá biblioteca gerenciada do Azure não fornece um meio de determinar a integridade de saudação de outras instâncias de função, mas você pode implementar essas avaliações de integridade se seu serviço precisar desta funcionalidade. Você pode usar [diagnóstico do Azure](cloud-services-dotnet-diagnostics.md) tooobtain informações sobre a execução de instâncias de função.
> 
> 

número da porta toodetermine Olá para um ponto de extremidade interno em uma instância de função, você pode usar o hello [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) tooreturn de propriedade endereços de um objeto de dicionário que contém nomes de ponto de extremidade e seu IP correspondente e portas. Olá [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) propriedade retorna o endereço IP hello e a porta para um ponto de extremidade especificado. Olá **PublicIPEndpoint** propriedade retorna porta Olá para um ponto de extremidade com balanceamento de carga. parte do endereço IP de saudação do hello **PublicIPEndpoint** propriedade não é usada.

Veja um exemplo que itera instâncias de função.

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

Aqui está um exemplo de uma função de trabalho que obtém o ponto de extremidade de saudação exposto por meio da definição de serviço hello e começa a escuta de conexões.

> [!WARNING]
> Este código só funcionará para um serviço implantado. Quando em execução no emulador de computação do Azure de saudação, elementos de configuração que criar pontos de extremidade de porta direta de serviço (**InstanceInputEndpoint** elementos) são ignorados.
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

## <a name="network-traffic-rules-toocontrol-role-communication"></a>Comunicação de função de toocontrol de regras de tráfego de rede
Depois de definir pontos de extremidade internos, você pode adicionar toocontrol de regras (com base em pontos de extremidade de saudação que você criou) de tráfego de rede como instâncias de função podem se comunicar uns com os outros. Olá diagrama a seguir mostra alguns cenários comuns para controlar a comunicação de função:

![Cenários de Regras de tráfego de rede](./media/cloud-services-enable-communication-role-instances/scenarios.png "Cenários de Regras de tráfego de rede")

Olá, exemplo de código a seguir mostra definições de função para funções hello mostradas no diagrama anterior hello. Cada definição de função inclui pelo menos um ponto de extremidade interno definido:

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
> A restrição de comunicação entre funções pode ocorrer com pontos de extremidade internos de portas fixas e atribuídas automaticamente.
> 
> 

Por padrão, após a definição de um ponto de extremidade interno, comunicação pode fluir de qualquer função toohello ponto de extremidade interno de uma função sem nenhuma restrição. comunicação toorestrict, você deve adicionar um **NetworkTrafficRules** elemento toohello **ServiceDefinition** elemento no arquivo de definição de serviço hello.

### <a name="scenario-1"></a>Cenário 1
Permitir somente o tráfego de rede de **WebRole1** muito**WorkerRole1**.

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

### <a name="scenario-2"></a>Cenário 2
Permite apenas o tráfego de rede de **WebRole1** muito**WorkerRole1** e **WorkerRole2**.

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

### <a name="scenario-3"></a>Cenário 3
Permite apenas o tráfego de rede de **WebRole1** muito**WorkerRole1**, e **WorkerRole1** muito**WorkerRole2**.

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

### <a name="scenario-4"></a>Cenário 4
Permite apenas o tráfego de rede de **WebRole1** muito**WorkerRole1**, **WebRole1** muito**WorkerRole2**, e  **WorkerRole1** muito**WorkerRole2**.

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

Uma referência de esquema XML para elementos de saudação usado acima pode ser encontrada [aqui](https://msdn.microsoft.com/library/azure/gg557551.aspx).

## <a name="next-steps"></a>Próximas etapas
Leia mais sobre Olá serviço de nuvem [modelo](cloud-services-model-and-package.md).

