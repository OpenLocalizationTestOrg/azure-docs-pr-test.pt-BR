---
title: "aaaConnect e se comunicar com os serviços do Azure Service Fabric | Microsoft Docs"
description: "Saiba como tooresolve, conecte-se e comunicar-se com os serviços do Service Fabric."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: msfussell
ms.assetid: 7d1052ec-2c9f-443d-8b99-b75c97266e6c
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 5/9/2017
ms.author: vturecek
ms.openlocfilehash: b8b374a71d4c5d21f48a560a3a8c81b357fe418d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-and-communicate-with-services-in-service-fabric"></a>Conectar e se comunicar com serviços no Service Fabric
No Service Fabric, um serviço é executado em algum lugar em um cluster do Service Fabric, normalmente distribuído entre várias VMs. Ele pode ser movido de tooanother de um só lugar, ao proprietário do serviço hello ou automaticamente pela malha do serviço. Os serviços não são tooa estaticamente empatados determinado computador ou endereço.

Um aplicativo do Service Fabric geralmente é composto por vários serviços diferentes, em que cada serviço executa uma tarefa específica. Esses serviços podem se comunicar com outro tooform uma função completa, como partes diferentes de renderização de um aplicativo web. Também há aplicativos que se conectam tooand se comunicar com serviços de cliente. Este documento aborda como tooset a comunicação com o e entre os serviços na malha do serviço.

Este vídeo da Microsoft Virtual Academy também discute a comunicação de serviço: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=iYFCk76yC_6706218965">  
<img src="./media/service-fabric-connect-and-communicate-with-services/CommunicationVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="bring-your-own-protocol"></a>Trazer seu próprio protocolo
Service Fabric ajuda a gerenciar a saudação do ciclo de vida dos serviços de, mas ele não tomar decisões sobre o que fazem seus serviços. Isso inclui a comunicação. Quando o serviço for aberto pelo serviço de malha, que é tooset de oportunidade do serviço a um ponto de extremidade para solicitações de entrada, usando qualquer pilha de comunicação ou protocolo desejado. O serviço escutará um endereço **IP:port** normal usando qualquer esquema de endereçamento, como um URI. Várias instâncias de serviço ou réplicas podem compartilhar um processo de host, caso em que eles serão necessário toouse diferentes portas ou use um mecanismo de compartilhamento de porta, como o driver de kernel HTTP. sys Olá no Windows. Em ambos os casos, cada instância de serviço ou réplica em um processo de host deve ser endereçável exclusivamente.

![pontos de extremidade de serviço][1]

## <a name="service-discovery-and-resolution"></a>Resolução e descoberta de serviço
Em um sistema distribuído, serviços podem mover de uma máquina tooanother ao longo do tempo. Isso pode ocorrer por vários motivos, incluindo balanceamento de recursos, atualizações, failovers ou escala horizontal. Isso significa alterar de endereços de ponto de extremidade de serviço como serviço de saudação move toonodes com endereços IP diferentes e pode abrir portas diferentes se o serviço Olá usa uma porta dinamicamente selecionada.

![Distribuição de serviços][7]

Serviço de malha fornece uma detecção e resolução de serviço chamado hello Naming Service. Olá Naming Service mantém uma tabela que mapeia endereços de ponto de extremidade toohello escutam em instâncias de serviço chamado. Todas as instâncias de serviço nomeadas do Service Fabric têm nomes exclusivos representados como URIs, como por exemplo, `"fabric:/MyApplication/MyService"`. nome de saudação do serviço de saudação não é alterado em tempo de vida de saudação do serviço Olá, é somente endereços de ponto de extremidade Olá que podem ser alterados quando mover serviços. Isso é análogo toowebsites que têm URLs constantes mas onde pode alterar o endereço IP hello. E tooDNS semelhante na web hello, que resolve endereços de tooIP de URLs de sites, o Service Fabric tem um registrador que mapeia o endereço de ponto de extremidade do serviço nomes tootheir.

![pontos de extremidade de serviço][2]

Resolvendo e conectar-se tooservices envolvem Olá executadas em um loop de etapas a seguir:

* **Resolver**: ponto de extremidade de saudação de Get que publicou um serviço de Olá Naming Service.
* **Conecte-se**: conectar-se o serviço toohello sobre o protocolo usa nesse ponto de extremidade.
* **Repita**: uma tentativa de conexão pode falhar por vários motivos, por exemplo, se o serviço Olá foi movido desde que o endereço de ponto de extremidade de saudação do hello última hora foi resolvido. Nesse caso, Olá anteriores resolver e conecte-se etapas necessário toobe repetida e o ciclo se repete até que a conexão de saudação for bem-sucedida.

## <a name="connecting-tooother-services"></a>Conectando a serviços tooother
Serviços conectando tooeach outros dentro de um cluster geralmente pode acessar diretamente os pontos de extremidade de saudação de outros serviços porque nós Olá em um cluster em Olá mesma rede local. toomake é mais fácil tooconnect entre serviços, Service Fabric fornece serviços adicionais que usam Olá Naming Service. Um serviço DNS e um serviço de proxy reverso.


### <a name="dns-service"></a>Serviço DNS
Como muitos serviços, especialmente em contêineres services, podem ter um nome de URL existente, capaz de tooresolve esses usando Olá protocolo DNS padrão (em vez de protocolo de serviço de nomes de saudação) é muito convenientes, especialmente no aplicativo "comparar e deslocar" cenários. Isso é exatamente qual serviço DNS Olá faz. Ele permite que você toomap DNS nomes tooa nome do serviço e, portanto, resolver endereços IP do ponto de extremidade. 

Como Olá mostrada no diagrama a seguir, Olá serviço DNS, em execução no cluster do Service Fabric hello, mapeia os nomes de tooservice de nomes DNS que são resolvidos pela Olá Naming Service tooreturn Olá ponto de extremidade endereços tooconnect para. nome DNS de saudação para serviço de saudação é fornecido no momento de saudação da criação. 

![pontos de extremidade de serviço][9]

Para obter mais detalhes sobre como ver toouse Olá serviço DNS [serviço DNS no Azure Service Fabric](service-fabric-dnsservice.md) artigo.

### <a name="reverse-proxy-service"></a>Serviço de proxy reverso
proxy reverso Olá endereços serviços em cluster Olá que expõe pontos de extremidade HTTP incluindo HTTPS. proxy reverso Olá simplifica bastante a chamada de outros serviços e seus métodos fazendo com que um determinado formato de URI e identificadores Olá resolver, conecte-se, etapas de repetição necessárias para um serviço toocommunicate com outro usando Olá serviço de nomenclatura. Em outras palavras, ele oculta Olá Naming Service você ao chamar outros serviços, tornando isso tão simples quanto chamar uma URL.

![pontos de extremidade de serviço][10]

Para obter mais detalhes sobre como toouse Olá reverter o serviço de proxy, consulte [proxy no Azure Service Fabric reverso](service-fabric-reverseproxy.md) artigo.

## <a name="connections-from-external-clients"></a>Conexões de clientes externos
Serviços conectando tooeach outros dentro de um cluster geralmente pode acessar diretamente os pontos de extremidade de saudação de outros serviços porque nós Olá em um cluster em Olá mesma rede local. Em alguns ambientes, entretanto, um cluster pode estar por trás de um balanceador de carga que encaminha o tráfego de entrada externo por meio de um conjunto limitado de portas. Nesses casos, os serviços ainda podem se comunicar entre si e resolver endereços usando Olá Naming Service, mas etapas adicionais devem ser feitos tooallow clientes externos tooconnect tooservices.

## <a name="service-fabric-in-azure"></a>Service Fabric no Azure
Um cluster do Service Fabric no Azure é colocado atrás de um Balanceador de Carga do Azure. Cluster de toohello todos os tráfego externo deve passar pelo Balanceador de carga de saudação. Olá balanceador de carga será automaticamente encaminhar tráfego entrada em um tooa porta aleatória *nó* com hello mesma porta aberta. Olá balanceador de carga do Azure só conhece portas abertas em Olá *nós*, ele não sabe sobre a abertura de portas por indivíduo *serviços*.

![Topologia do Balanceador de Carga do Azure e do Service Fabric][3]

Por exemplo, no tráfego externo de ordem tooaccept na porta **80**, Olá coisas a seguir deve ser configurado:

1. Escreva um serviço que escute na porta 80. Configurar a porta 80 em ServiceManifest.xml do serviço hello e abra um ouvinte no serviço hello, por exemplo, um servidor web auto-hospedado.

    ```xml
    <Resources>
        <Endpoints>
            <Endpoint Name="WebEndpoint" Protocol="http" Port="80" />
        </Endpoints>
    </Resources>
    ```
    ```csharp
        class HttpCommunicationListener : ICommunicationListener
        {
            ...

            public Task<string> OpenAsync(CancellationToken cancellationToken)
            {
                EndpointResourceDescription endpoint =
                    serviceContext.CodePackageActivationContext.GetEndpoint("WebEndpoint");

                string uriPrefix = $"{endpoint.Protocol}://+:{endpoint.Port}/myapp/";

                this.httpListener = new HttpListener();
                this.httpListener.Prefixes.Add(uriPrefix);
                this.httpListener.Start();

                string publishUri = uriPrefix.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);
                return Task.FromResult(publishUri);
            }

            ...
        }

        class WebService : StatelessService
        {
            ...

            protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
            {
                return new[] { new ServiceInstanceListener(context => new HttpCommunicationListener(context))};
            }

            ...
        }
    ```
    ```java
        class HttpCommunicationlistener implements CommunicationListener {
            ...

            @Override
            public CompletableFuture<String> openAsync(CancellationToken arg0) {
                EndpointResourceDescription endpoint =
                    this.serviceContext.getCodePackageActivationContext().getEndpoint("WebEndpoint");
                try {
                    HttpServer server = com.sun.net.httpserver.HttpServer.create(new InetSocketAddress(endpoint.getPort()), 0);
                    server.start();

                    String publishUri = String.format("http://%s:%d/",
                        this.serviceContext.getNodeContext().getIpAddressOrFQDN(), endpoint.getPort());
                    return CompletableFuture.completedFuture(publishUri);
                } catch (IOException e) {
                    throw new RuntimeException(e);
                }
            }

            ...
        }

        class WebService extends StatelessService {
            ...

            @Override
            protected List<ServiceInstanceListener> createServiceInstanceListeners() {
                <ServiceInstanceListener> listeners = new ArrayList<ServiceInstanceListener>();
                listeners.add(new ServiceInstanceListener((context) -> new HttpCommunicationlistener(context)));
                return listeners;       
            }

            ...
        }
    ```
2. Criar um Cluster de malha do serviço no Azure e especifique a porta **80** como uma porta de ponto de extremidade personalizado para o tipo de nó Olá que irá hospedar o serviço de saudação. Se você tiver mais de um tipo de nó, você pode configurar um *restrição de posicionamento* em Olá serviço tooensure só é executado no tipo de nó de saudação que tem a porta do ponto de extremidade personalizado Olá aberta.

    ![Abrir uma porta em um tipo de nó][4]
3. Uma vez Olá cluster foi criado, configure hello Azure balanceador de carga no tráfego de tooforward de grupo de recursos do cluster Olá na porta 80. Ao criar um cluster por meio de saudação portal do Azure, isso é configurar automaticamente para cada porta do ponto de extremidade personalizado que foi configurada.

    ![Encaminhar o tráfego Olá balanceador de carga do Azure][5]
4. Olá usa o balanceador de carga do Azure toodetermine uma investigação se ou não toosend tooa determinado nó de tráfego. Olá teste periodicamente verifica um ponto de extremidade em cada toodetermine de nó ou não o nó de saudação está respondendo. Se a investigação de saudação falhar tooreceive uma resposta após um determinado número de vezes, balanceador de carga Olá interromperá o envio de nó de toothat de tráfego. Ao criar um cluster por meio de saudação portal do Azure, uma investigação é configurada automaticamente para cada porta do ponto de extremidade personalizado que foi configurada.

    ![Encaminhar o tráfego Olá balanceador de carga do Azure][8]

É importante tooremember que hello balanceador de carga do Azure e investigação Olá só conhecem Olá *nós*, Olá não *serviços* em execução em nós de saudação. Olá balanceador de carga do Azure sempre enviará tráfego toonodes que respondem a investigação de toohello, portanto deve ter cuidado tooensure serviços estão disponíveis em nós de saudação que são capazes de toorespond toohello investigação.

## <a name="reliable-services-built-in-communication-api-options"></a>Reliable Services: Opções de API de comunicação interna
estrutura de serviços confiáveis Olá é fornecido com várias opções de comunicação pré-criado. decisão Olá sobre os quais um funcionará melhor para você depende da escolha de saudação do hello programação modelo, estrutura de comunicação hello e Olá que os serviços são escritos na linguagem de programação.

* **Nenhum protocolo específico:** se você não tem uma opção específica do framework de comunicação, mas você deseja tooget algo em funcionamento rapidamente, Olá a opção ideal para você é [comunicação remota do serviço](service-fabric-reliable-services-communication-remoting.md), que permite chamadas de procedimento remoto fortemente tipado para serviços confiáveis e atores confiável. Isso é mais fácil de hello e tooget de maneira mais rápida é iniciado com a comunicação de serviço. A comunicação remota do serviço lida com a resolução de endereços de serviço, conexão, repetição e tratamento de erro. Isso está disponível para aplicativos Java e C#.
* **HTTP**: para comunicação independente de idioma, o HTTP fornece uma opção padrão do setor com ferramentas e servidores HTTP disponíveis em várias linguagens diferentes, tudo isso com suporte no Service Fabric. Os serviços podem usar qualquer pilha HTTP disponível, incluindo [API Web ASP.NET](service-fabric-reliable-services-communication-webapi.md) para aplicativos C#. Clientes gravados em c# podem aproveitar Olá `ICommunicationClient` e `ServicePartitionClient` classes, enquanto para Java, use Olá `CommunicationClient` e `FabricServicePartitionClient` classes, [para resolução de serviço, as conexões HTTP e loops de repetição](service-fabric-reliable-services-communication.md).
* **WCF**: se você tiver um código que usa o WCF como sua estrutura de comunicação, você pode usar o hello `WcfCommunicationListener` para o lado do servidor de saudação e `WcfCommunicationClient` e `ServicePartitionClient` classes para cliente hello. No entanto, isso só está disponível para aplicativos C# em clusters baseados no Windows. Para obter mais detalhes, consulte este artigo sobre [baseados em WCF e a implementação da pilha de comunicação Olá](service-fabric-reliable-services-communication-wcf.md).

## <a name="using-custom-protocols-and-other-communication-frameworks"></a>Usando protocolos personalizados e outras estruturas de comunicação
Os serviços poderão usar qualquer protocolo ou estrutura para comunicação, independentemente de esse ser um protocolo binário personalizado via soquetes TCP ou eventos de streaming por meio de [Hubs de Eventos do Azure](https://azure.microsoft.com/services/event-hubs/) ou [Hub IoT do Azure](https://azure.microsoft.com/services/iot-hub/). Serviço de malha fornece APIs que você pode conectar sua pilha de comunicação, enquanto todos os Olá trabalhar toodiscover e conecte-se a comunicação é abstraída do você. Consulte este artigo sobre Olá [modelo de comunicação de serviço confiável](service-fabric-reliable-services-communication.md) para obter mais detalhes.

## <a name="next-steps"></a>Próximas etapas
Saber mais sobre conceitos de saudação e APIs disponíveis no hello [modelo de comunicação de serviços confiáveis](service-fabric-reliable-services-communication.md), em seguida, se familiarizar rapidamente com [comunicação remota do serviço](service-fabric-reliable-services-communication-remoting.md) ou vá toolearn detalhada como toowrite um ouvinte de comunicação usando [API da Web com OWIN auto-host](service-fabric-reliable-services-communication-webapi.md).

[1]: ./media/service-fabric-connect-and-communicate-with-services/serviceendpoints.png
[2]: ./media/service-fabric-connect-and-communicate-with-services/namingservice.png
[3]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancertopology.png
[4]: ./media/service-fabric-connect-and-communicate-with-services/nodeport.png
[5]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerport.png
[7]: ./media/service-fabric-connect-and-communicate-with-services/distributedservices.png
[8]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerprobe.png
[9]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[10]: ./media/service-fabric-reverseproxy/internal-communication.png
