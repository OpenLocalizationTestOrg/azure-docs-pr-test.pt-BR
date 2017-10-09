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
# <a name="how-toouse-azure-relay-wcf-relays-with-net"></a>Como toouse Azure retransmissão WCF retransmissões com .NET
Este artigo descreve como toouse Olá serviço de retransmissão do Azure. exemplos de Olá são escritos em c# e usam o API do Windows Communication Foundation (WCF) Olá com extensões contidas Olá assembly do barramento de serviço. Para obter mais informações sobre a retransmissão do Azure, consulte Olá [visão geral do Azure retransmissão](relay-what-is-it.md).

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="what-is-wcf-relay"></a>O que é Retransmissão do WCF?

Hello Azure [ *retransmissão WCF* ](relay-what-is-it.md) serviço permite que aplicativos híbridos toobuild que são executados em um datacenter do Azure e seu próprio ambiente de empresa local. serviço de retransmissão Olá facilita isso, permitindo que você toosecurely expor serviços Windows Communication Foundation (WCF) que residem dentro de uma empresa corporativa rede toohello nuvem pública, sem tooopen uma conexão do firewall, ou exigindo infraestrutura de rede corporativa tooa alterações intrusiva.

![Conceitos de retransmissão do WCF](./media/service-bus-dotnet-how-to-use-relay/sb-relay-01.png)

Retransmissão do Azure permite que você toohost os serviços WCF em seu ambiente empresarial existente. Em seguida, você pode delegar aguardando entrada sessões e solicitações toothese WCF toohello retransmissão serviços estão em execução no Azure. Isso permite que você tooexpose esses serviços tooapplication o código em execução no Azure, ou operadores toomobile ou ambientes de extranet do parceiro. Retransmissão permite que você controle toosecurely quem pode acessar esses serviços em um nível granular. Ele fornece uma funcionalidade do aplicativo de maneira segura e eficiente tooexpose e dados de suas soluções empresariais existentes e tirar proveito da nuvem de saudação.

Este artigo aborda como toouse Azure retransmissão toocreate um serviço web WCF, exposta usando uma associação de canal TCP, que implementa uma conversa segura entre duas partes.

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="get-hello-service-bus-nuget-package"></a>Obter o pacote do NuGet do barramento de serviço Olá
Olá [pacote NuGet do barramento de serviço](https://www.nuget.org/packages/WindowsAzure.ServiceBus) é Olá mais fácil maneira tooget Olá API do barramento de serviço e tooconfigure seu aplicativo com todas as dependências de barramento de serviço hello. pacote do NuGet Olá tooinstall em seu projeto, Olá a seguir:

1. No Gerenciador de Soluções, clique com o botão direito do mouse em **Referências** e clique em **Gerenciar Pacotes NuGet**.
2. Pesquisa por "Service Bus" e selecione Olá **barramento de serviço do Microsoft Azure** item. Clique em **instalar** toocomplete Olá instalação e feche o hello caixa de diálogo a seguir:
   
   ![](./media/service-bus-dotnet-how-to-use-relay/getting-started-multi-tier-13.png)

## <a name="expose-and-consume-a-soap-web-service-with-tcp"></a>Exponha e consuma um serviço Web SOAP com TCP
tooexpose um serviço web de WCF SOAP existente para consumo externo, você deve fazer alterações toohello as associações de serviço e endereços. Isso pode exigir o arquivo de configuração tooyour alterações ou pode exigir alterações de código, dependendo de como você ter instalado e configurado seus serviços WCF. Observe que o WCF permite toohave vários pontos de extremidade de rede sobre Olá mesmo serviço, para que você possa reter Olá existente pontos de extremidade internos durante a adição de pontos de extremidade de retransmissão para uso externo acessarem Olá mesmo tempo.

Nesta tarefa, você cria um serviço WCF simples e adicionar um tooit de ouvinte de retransmissão. Este exercício presume familiaridade com o Visual Studio e, portanto, não percorrer todos os detalhes de saudação de criação de um projeto. Em vez disso, ele se concentra em código hello.

Antes de iniciar essas etapas, conclua Olá procedimento tooset seu ambiente a seguir:

1. No Visual Studio, crie um aplicativo de console que contém dois projetos, "Cliente" e "Serviço", na solução de saudação.
2. Adicione Olá NuGet do Service Bus pacote tooboth projetos. Esse pacote adiciona todos os projetos de tooyour Olá assembly necessárias referências.

### <a name="how-toocreate-hello-service"></a>Como toocreate Olá serviço
Primeiro, crie o próprio serviço de saudação. Qualquer serviço WCF consiste em pelo menos três partes distintas:

* Definição de um contrato que descreve quais mensagens são trocadas e quais operações são toobe invocado.
* Implementação do contrato.
* Host que hospeda o serviço do WCF hello e expõe vários pontos de extremidade.

exemplos de código Olá nesta seção abordam cada um desses componentes.

contrato de saudação define uma única operação, `AddNumbers`, que adiciona dois números e retorna o resultado de saudação. Olá `IProblemSolverChannel` interface habilita Olá cliente toomore gerenciar facilmente o tempo de vida de proxy de saudação. A criação dessa interface é considerada uma prática recomendada. É uma boa ideia tooput essa definição em um arquivo separado do contrato para que você pode fazer referência a esse arquivo de projetos "Cliente" e "Serviço", mas você também pode copiar o código de saudação em ambos os projetos.

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

Com o contrato de saudação em vigor, implementação Olá é o seguinte:

```csharp
class ProblemSolver : IProblemSolver
{
    public int AddNumbers(int a, int b)
    {
        return a + b;
    }
}
```

### <a name="configure-a-service-host-programmatically"></a>Configure um host de serviço de forma programática
Com o contrato de saudação e a implementação no lugar, agora você pode hospedar o serviço hello. Hospedagem ocorre dentro de um [ServiceHost](https://msdn.microsoft.com/library/system.servicemodel.servicehost.aspx) object, que cuida do gerenciamento de instâncias de serviço hello e hosts Olá pontos de extremidade que escutam as mensagens. Hello código a seguir configura o serviço de saudação com um ponto de extremidade local regular e uma aparência de saudação de tooillustrate de ponto de extremidade retransmissão lado a lado dos pontos de extremidade internos e externos. Substitua a cadeia de caracteres hello *namespace* com o nome do namespace e *yourKey* com a chave SAS Olá que você obteve na etapa de instalação anterior hello.

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

Exemplo hello, você criará dois pontos de extremidade que estão em Olá mesmo contrato de implementação. Um é local e o outro é projetado por meio da Retransmissão do Azure. Olá principais diferenças entre eles são associações de saudação; [NetTcpBinding](https://msdn.microsoft.com/library/system.servicemodel.nettcpbinding.aspx) para um local de saudação e [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding#microsoft_servicebus_nettcprelaybinding) para o ponto de extremidade de retransmissão hello e endereços de saudação. ponto de extremidade local Olá tem um endereço de rede local com uma porta distinto. ponto de extremidade de retransmissão Hello tem um endereço de ponto de extremidade composto de cadeia de caracteres hello `sb`, o nome do namespace e o caminho hello "solver." Isso resulta em Olá URI `sb://[serviceNamespace].servicebus.windows.net/solver`, identificando o ponto de extremidade de serviço hello como um ponto de extremidade TCP de barramento de serviço (retransmissão) com o nome DNS totalmente qualificado externo. Se você colocar código Olá substituindo espaços reservados de saudação em Olá `Main` função da saudação **Service** aplicativo, você terá um serviço funcional. Se você quiser toolisten seu serviço exclusivamente em retransmissão hello, remova a declaração de ponto de extremidade local do hello.

### <a name="configure-a-service-host-in-hello-appconfig-file"></a>Configurar um host de serviço no arquivo App. config de saudação
Você também pode configurar o host de saudação usando o arquivo App. config de saudação. serviço de saudação hospedagem de código nesse caso aparece no exemplo a seguir hello.

```csharp
ServiceHost sh = new ServiceHost(typeof(ProblemSolver));
sh.Open();
Console.WriteLine("Press ENTER tooclose");
Console.ReadLine();
sh.Close();
```

definições de ponto de extremidade de saudação mova para o arquivo App. config de saudação. pacote do NuGet Olá já adicionado um intervalo de toohello arquivo de definições de App. config, que são extensões de configuração Olá necessário para a retransmissão do Azure. Olá seguinte exemplo, a saudação exata equivalente do código anterior de saudação, devem aparecer diretamente sob Olá **System. ServiceModel** elemento. Esse exemplo pressupõe que o namespace do projeto C# é chamado de **Serviço**.
Substitua espaços reservados de saudação com seu nome de namespace de retransmissão e chave de SAS.

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

Depois de fazer essas alterações, o serviço de saudação iniciado como antes, mas com dois pontos de extremidade ao vivo: um local e um escutando na nuvem hello.

### <a name="create-hello-client"></a>Crie saudação do cliente
#### <a name="configure-a-client-programmatically"></a>Configure um cliente de forma programática
serviço de saudação tooconsume, você pode construir um cliente WCF usando um [ChannelFactory](https://msdn.microsoft.com/library/system.servicemodel.channelfactory.aspx) objeto. O Barramento de Serviço usa um modelo de segurança baseado em token implementado com a SAS. Olá [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) classe representa um provedor de token de segurança com métodos de fábrica de incorporados que retornam alguns provedores de token bem conhecidos. Olá, exemplo a seguir usa Olá [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) método toohandle Olá aquisição token SAS apropriado de saudação. chave e nome de saudação são aqueles obtidos no portal de saudação conforme descrito na seção anterior hello.

Primeiro, referência ou cópia Olá `IProblemSolver` código do serviço de saudação do contrato em seu projeto do cliente.

Em seguida, substitua o código Olá Olá `Main` método do cliente hello, novamente, substituindo texto de espaço reservado de saudação com a chave SAS e o namespace de retransmissão.

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

Agora você pode criar cliente hello e serviço hello, executá-los (execução de serviço Olá primeiro), saudação do cliente e chama o serviço de saudação imprime **9**. Você pode executar Olá cliente e servidor em computadores diferentes, mesmo em redes e comunicação Olá ainda funcionarão. código de cliente Olá também pode ser executado localmente ou na nuvem de saudação.

#### <a name="configure-a-client-in-hello-appconfig-file"></a>Configurar um cliente no arquivo App. config de saudação
saudação de código a seguir mostra como o cliente usando uma saudação tooconfigure Olá arquivo App. config.

```csharp
var cf = new ChannelFactory<IProblemSolverChannel>("solver");
using (var ch = cf.CreateChannel())
{
    Console.WriteLine(ch.AddNumbers(4, 5));
}
```

definições de ponto de extremidade de saudação mova para o arquivo App. config de saudação. Olá exemplo a seguir, que é Olá igual ao código Olá listado anteriormente deve aparecer diretamente sob Olá `<system.serviceModel>` elemento. Aqui, como antes, você deve substituir espaços reservados de saudação com a chave SAS e o namespace de retransmissão.

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

## <a name="next-steps"></a>Próximas etapas
Agora que você aprendeu as Noções básicas de saudação de retransmissão do Azure, siga essas toolearn links mais.

* [O que é Retransmissão do Azure?](relay-what-is-it.md)
* [Visão geral da arquitetura de Barramento de Serviço do Azure](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* Baixe os exemplos de barramento de serviço do [exemplos do Azure] [ Azure samples] ou consulte Olá [visão geral dos exemplos de barramento de serviço][overview of Service Bus samples].

[Shared Access Signature Authentication with Service Bus]: ../service-bus-messaging/service-bus-shared-access-signature-authentication.md
[Azure samples]: https://code.msdn.microsoft.com/site/search?query=service%20bus&f%5B0%5D.Value=service%20bus&f%5B0%5D.Type=SearchText&ac=2
[overview of Service Bus samples]: ../service-bus-messaging/service-bus-samples.md
