---
title: "Visão geral de comunicação de serviços aaaReliable | Microsoft Docs"
description: "Visão geral de comunicação de serviços confiáveis Olá modelo, incluindo ouvintes de abertura em serviços, resolvendo os pontos de extremidade e comunicação entre serviços."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: BharatNarasimman
ms.assetid: 36217988-420e-409d-b0a4-e0e875b6eac8
ms.service: service-fabric
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 04/07/2017
ms.author: vturecek
ms.openlocfilehash: 93a7017b50df0822969daa5ad78302c73e8ba641
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-reliable-services-communication-apis"></a>Como toouse Olá APIs de comunicação de serviços confiáveis
O Service Fabric do Azure como uma plataforma é totalmente independente quanto às comunicações entre serviços. Todos os protocolos e pilhas são aceitáveis, de tooHTTP UDP. É o toohello toochoose de desenvolvedor de serviço como serviços devem se comunicar. estrutura de aplicativo de serviços confiáveis Olá fornece comunicação interna de pilhas, bem como as APIs que você pode usar toobuild os componentes personalizados de comunicação.

## <a name="set-up-service-communication"></a>Configurar a comunicação de serviço
Olá confiável API de serviços usa uma interface simples para comunicação de serviço. tooopen um ponto de extremidade para seu serviço, basta implementar essa interface:

```csharp

public interface ICommunicationListener
{
    Task<string> OpenAsync(CancellationToken cancellationToken);

    Task CloseAsync(CancellationToken cancellationToken);

    void Abort();
}

```

```java
public interface CommunicationListener {
    CompletableFuture<String> openAsync(CancellationToken cancellationToken);

    CompletableFuture<?> closeAsync(CancellationToken cancellationToken);

    void abort();
}
```

Você pode adicionar a implementação do ouvinte de comunicação, retornando-a em uma substituição do método de classe com base no serviço.

Para serviços sem estado:

```csharp
class MyStatelessService : StatelessService
{
    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        ...
    }
    ...
}
```
```java
public class MyStatelessService extends StatelessService {

    @Override
    protected List<ServiceInstanceListener> createServiceInstanceListeners() {
        ...
    }
    ...
}
```

Para serviços com estado:

> [!NOTE]
> Ainda não há suporte para Reliable Services com monitoração de estado em Java.
>
>

```csharp
class MyStatefulService : StatefulService
{
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
        ...
    }
    ...
}
```

Em ambos os casos, você deve retornar uma coleção de ouvintes. Isso permite que seu serviço toolisten em vários pontos de extremidade, potencialmente usando protocolos diferentes, usando vários ouvintes. Por exemplo, você pode ter um ouvinte HTTP e um ouvinte WebSocket separado. Cada ouvinte obtém um nome e a coleção resultante de saudação do *nome: endereço* pares são representados como um objeto JSON quando um cliente solicita endereços de escuta Olá para uma instância de serviço ou uma partição.

Em um serviço sem monitoração de estado, a substituição de saudação retorna uma coleção de ServiceInstanceListeners. Um `ServiceInstanceListener` contém uma função toocreate uma `ICommunicationListener(C#) / CommunicationListener(Java)` e concede a ele um nome. Para os serviços com monitoração de estado, a substituição de saudação retorna uma coleção de ServiceReplicaListeners. Isso é um pouco diferente de sua contraparte sem monitoração de estado, pois um `ServiceReplicaListener` tem uma opção tooopen um `ICommunicationListener` em réplicas secundárias. Você pode usar vários ouvintes de comunicação em um serviço, além de especificar aqueles que aceitem solicitações em réplicas secundárias e os que escutam apenas em réplicas primárias.

Por exemplo, você pode ter um ServiceRemotingListener que faz chamadas RPC apenas em réplicas primárias e um segundo ouvinte personalizado que faz solicitações de leitura em réplicas secundárias sobre HTTP:

```csharp
protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new[]
    {
        new ServiceReplicaListener(context =>
            new MyCustomHttpListener(context),
            "HTTPReadonlyEndpoint",
            true),

        new ServiceReplicaListener(context =>
            this.CreateServiceRemotingListener(context),
            "rpcPrimaryEndpoint",
            false)
    };
}
```

> [!NOTE]
> Ao se criar vários ouvintes para um serviço, cada ouvinte **deve** receber um nome exclusivo.
>
>

Finalmente, descreva os pontos de extremidade de saudação que são necessários para o serviço Olá Olá [manifesto do serviço](service-fabric-application-model.md) na seção de saudação em pontos de extremidade.

```xml
<Resources>
    <Endpoints>
      <Endpoint Name="WebServiceEndpoint" Protocol="http" Port="80" />
      <Endpoint Name="OtherServiceEndpoint" Protocol="tcp" Port="8505" />
    <Endpoints>
</Resources>

```

ouvinte de comunicação Olá pode acessar os recursos de ponto de extremidade Olá alocados tooit de saudação `CodePackageActivationContext` em Olá `ServiceContext`. Olá pode, em seguida, iniciar o ouvinte escuta solicitações de quando ele é aberto.

```csharp
var codePackageActivationContext = serviceContext.CodePackageActivationContext;
var port = codePackageActivationContext.GetEndpoint("ServiceEndpoint").Port;

```
```java
CodePackageActivationContext codePackageActivationContext = serviceContext.getCodePackageActivationContext();
int port = codePackageActivationContext.getEndpoint("ServiceEndpoint").getPort();

```

> [!NOTE]
> Recursos de ponto de extremidade são o pacote de serviço inteiro toohello comuns e são alocados pela malha do serviço quando o pacote de serviço Olá é ativado. Várias réplicas de serviço hospedadas no hello pode compartilhar a mesma ServiceHost Olá mesma porta. Isso significa que esse ouvinte de comunicação Olá deve dar suporte a compartilhamento de porta. Olá recomendado maneira de fazer isso é para Olá comunicação ouvinte toouse Olá partição ID e a ID de instância/réplica ao gerar o endereço de escuta hello.
>
>

### <a name="service-address-registration"></a>Registro de endereço do serviço
Um serviço de sistema chamado hello *Naming Service* é executado em clusters de malha do serviço. Olá, serviço de nomes é um registrador para serviços e seus endereços de cada instância ou a réplica de serviço hello está escutando. Olá quando `OpenAsync(C#) / openAsync(Java)` método de um `ICommunicationListener(C#) / CommunicationListener(Java)` for concluído, o retorno de valor é registrado no hello Naming Service. Isso retorna o valor que obtém Olá publicado no serviço de nomes é uma cadeia de caracteres cujo valor pode ser qualquer coisa alguma. Esse valor de cadeia de caracteres é o que os clientes verão quando eles solicitam um endereço para o serviço de saudação do hello Naming Service.

```csharp
public Task<string> OpenAsync(CancellationToken cancellationToken)
{
    EndpointResourceDescription serviceEndpoint = serviceContext.CodePackageActivationContext.GetEndpoint("ServiceEndpoint");
    int port = serviceEndpoint.Port;

    this.listeningAddress = string.Format(
                CultureInfo.InvariantCulture,
                "http://+:{0}/",
                port);

    this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

    this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

    // hello string returned here will be published in hello Naming Service.
    return Task.FromResult(this.publishAddress);
}
```
```java
public CompletableFuture<String> openAsync(CancellationToken cancellationToken)
{
    EndpointResourceDescription serviceEndpoint = serviceContext.getCodePackageActivationContext.getEndpoint("ServiceEndpoint");
    int port = serviceEndpoint.getPort();

    this.publishAddress = String.format("http://%s:%d/", FabricRuntime.getNodeContext().getIpAddressOrFQDN(), port);

    this.webApp = new WebApp(port);
    this.webApp.start();

    /* hello string returned here will be published in hello Naming Service.
     */
    return CompletableFuture.completedFuture(this.publishAddress);
}
```

Serviço de malha fornece APIs que permitem que os clientes e outros serviços toothen peça para este endereço por nome de serviço. Isso é importante porque o endereço do serviço Olá não é estático. Os serviços são movidos em torno de cluster Olá para fins de disponibilidade e balanceamento de recursos. Esse é o mecanismo de saudação que permite que clientes tooresolve Olá endereço para um serviço de escuta.

> [!NOTE]
> Para uma passo a passo completa de como toowrite um ouvinte de comunicação, consulte [serviços de API da Web do serviço do Fabric com OWIN auto-hospedagem](service-fabric-reliable-services-communication-webapi.md) para c#, enquanto para Java, você pode escrever sua própria implementação do servidor HTTP, consulte EchoServer aplicativo exemplo em https://github.com/Azure-Samples/service-fabric-java-getting-started.
>
>

## <a name="communicating-with-a-service"></a>Comunicando-se com um serviço
Olá confiável API de serviços fornece Olá clientes toowrite de bibliotecas que se comunicam com os serviços a seguir.

### <a name="service-endpoint-resolution"></a>Resolução de ponto de extremidade de serviço
Olá primeira etapa toocommunication com um serviço é tooresolve um endereço de ponto de extremidade de partição hello ou instância de serviço Olá para que deseja tootalk. Olá `ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` classe de utilitário é uma primitiva básico que ajuda os clientes a determinar o ponto de extremidade de saudação de um serviço em tempo de execução. Na terminologia de malha do serviço, o processo de Olá de determinar o ponto de extremidade de saudação de um serviço é chamado tooas Olá *resolução do ponto de extremidade de serviço*.

tooconnect tooservices dentro de um cluster, ServicePartitionResolver pode ser criado usando as configurações padrão. Isso é recomendada o uso para a maioria das situações de saudação:

```csharp
ServicePartitionResolver resolver = ServicePartitionResolver.GetDefault();
```
```java
FabricServicePartitionResolver resolver = FabricServicePartitionResolver.getDefault();
```

tooconnect tooservices em um cluster diferente, um ServicePartitionResolver pode ser criado com um conjunto de pontos de extremidade de gateway do cluster. Observe que os pontos de extremidade do gateway são diferentes apenas pontos de extremidade de conexão toohello mesmo cluster. Por exemplo:

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```

Como alternativa, `ServicePartitionResolver` pode receber uma função para a criação de um `FabricClient` toouse internamente:

```csharp
public delegate FabricClient CreateFabricClientDelegate();
```
```java
public FabricServicePartitionResolver(CreateFabricClient createFabricClient) {
...
}

public interface CreateFabricClient {
    public FabricClient getFabricClient();
}
```

`FabricClient`é objeto Olá toocommunicate usado com cluster do Service Fabric Olá para várias operações de gerenciamento no cluster hello. Isso é útil quando você quiser mais controle sobre como um resolvedor de partição de serviço interage com o cluster. `FabricClient`armazena em cache internamente e é geralmente caro toocreate, portanto, é importante tooreuse `FabricClient` instâncias tanto quanto possíveis.

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver(() => CreateMyFabricClient());
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver(() -> new CreateFabricClientImpl());
```

Um método de resolução é usada tooretrieve Olá endereço de um serviço ou uma partição de serviço para serviços particionadas.

```csharp
ServicePartitionResolver resolver = ServicePartitionResolver.GetDefault();

ResolvedServicePartition partition =
    await resolver.ResolveAsync(new Uri("fabric:/MyApp/MyService"), new ServicePartitionKey(), cancellationToken);
```
```java
FabricServicePartitionResolver resolver = FabricServicePartitionResolver.getDefault();

CompletableFuture<ResolvedServicePartition> partition =
    resolver.resolveAsync(new URI("fabric:/MyApp/MyService"), new ServicePartitionKey());
```

Um endereço de serviço pode ser resolvido facilmente usando um ServicePartitionResolver, mas é mais trabalhoso tooensure Olá resolvido endereço pode ser usado corretamente. O cliente precisa toodetect se a tentativa de conexão Olá falhou devido a um erro transitório e pode ser repetida (por exemplo, serviço movido ou está temporariamente indisponível), ou um erro permanente (por exemplo, o serviço foi excluído ou hello recurso solicitado não existe mais). Instâncias de serviço ou réplicas podem se mover de nó toonode a qualquer momento por vários motivos. endereço do serviço Olá resolvido por meio de ServicePartitionResolver pode ficar obsoleto pelo tempo de saudação que tooconnect tentativas de código do cliente. Nesse caso novamente cliente Olá precisa de resolução toore Olá endereço. Fornecendo Olá anterior `ResolvedServicePartition` indica que Olá resolvedor necessidades tootry novamente, em vez de simplesmente recuperar um endereço armazenado em cache.

Normalmente, o código de cliente Olá necessário trabalhar com hello ServicePartitionResolver não diretamente. Ele é criado e repassado toocommunication fábricas de cliente em Olá confiável API de serviços. fábricas de saudação usam resolvedor Olá internamente toogenerate um objeto cliente que pode ser usado toocommunicate com os serviços.

### <a name="communication-clients-and-factories"></a>Fábricas e clientes de comunicação
biblioteca de fábrica de comunicação Olá implementa um padrão típico de repetição de tratamento de falhas que facilita tentando novamente conexões tooresolved pontos de extremidade. biblioteca de fábrica Olá fornece mecanismo de repetição Olá enquanto você fornece manipuladores de erro hello.

`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`Define a interface base hello, implementada por uma fábrica de cliente de comunicação que produz os clientes que podem se comunicar tooa serviço de malha do serviço. Olá implementação de saudação que communicationclientfactory depende Olá pilha de comunicação usada pelo serviço de malha do serviço de Olá onde o cliente Olá quer toocommunicate. Olá confiável API de serviços fornece um `CommunicationClientFactoryBase<TCommunicationClient>`. Isso fornece uma implementação básica da interface de CommunicationClientFactory hello e executa tarefas que são comuns pilhas de comunicação de saudação tooall. (Essas tarefas incluem o uso de um ponto de extremidade de serviço do ServicePartitionResolver toodetermine Olá). Os clientes normalmente implementar Olá abstrata CommunicationClientFactoryBase classe toohandle lógica de pilha de comunicação toohello específico.

cliente de comunicação Olá apenas recebe um endereço e usa tooconnect tooa service. cliente Olá pode usar qualquer protocolo ele deseja.

```csharp
class MyCommunicationClient : ICommunicationClient
{
    public ResolvedServiceEndpoint Endpoint { get; set; }

    public string ListenerName { get; set; }

    public ResolvedServicePartition ResolvedServicePartition { get; set; }
}
```
```java
public class MyCommunicationClient implements CommunicationClient {

    private ResolvedServicePartition resolvedServicePartition;
    private String listenerName;
    private ResolvedServiceEndpoint endPoint;

    /*
     * Getters and Setters
     */
}
```

fábrica de saudação do cliente é basicamente responsável pela criação de clientes de comunicação. Para clientes que não mantêm uma conexão persistente, como um cliente HTTP, fábrica Olá só precisa toocreate e cliente Olá retorno. Outros protocolos que mantêm uma conexão persistente, como alguns protocolos binários, também devem ser validados pelo Olá fábrica toodetermine se conexão Olá precisa toobe criado novamente.  

```csharp
public class MyCommunicationClientFactory : CommunicationClientFactoryBase<MyCommunicationClient>
{
    protected override void AbortClient(MyCommunicationClient client)
    {
    }

    protected override Task<MyCommunicationClient> CreateClientAsync(string endpoint, CancellationToken cancellationToken)
    {
    }

    protected override bool ValidateClient(MyCommunicationClient clientChannel)
    {
    }

    protected override bool ValidateClient(string endpoint, MyCommunicationClient client)
    {
    }
}
```
```java
public class MyCommunicationClientFactory extends CommunicationClientFactoryBase<MyCommunicationClient> {

    @Override
    protected boolean validateClient(MyCommunicationClient clientChannel) {
    }

    @Override
    protected boolean validateClient(String endpoint, MyCommunicationClient client) {
    }

    @Override
    protected CompletableFuture<MyCommunicationClient> createClientAsync(String endpoint) {
    }

    @Override
    protected void abortClient(MyCommunicationClient client) {
    }
}
```

Por fim, um manipulador de exceção é responsável por determinar quais tootake ação quando ocorre uma exceção. Exceções são categorizadas como **repetíveis** e **não repetíveis**.

* **Sem nova tentativa** exceções simplesmente obtenham relançadas toohello back chamador.
* Exceções **repetíveis** são categorizadas novamente em **transitórias** e **não transitórias**.
  * **Transitório** exceções são aqueles que simplesmente pode ser repetida sem resolver novamente o endereço de ponto de extremidade de serviço hello. Isso incluirá os problemas de rede temporários ou respostas de erro de serviço que não sejam aqueles que indicam o endereço do ponto de extremidade de serviço de saudação não existe.
  * **Não transitório** exceções são aqueles que exigem um ponto de extremidade de serviço de Olá endereço toobe resolvido novamente. Elas incluem exceções que indicam o ponto de extremidade de serviço de saudação não pôde ser alcançado, indicando que o serviço Olá moveu tooa outro nó.

Olá `TryHandleException` toma uma decisão sobre uma determinada exceção. Se ele **não sabe** que toomake decisões sobre uma exceção, ele deverá retornar **false**. Se ele **saber** que toomake de decisão, deve definir o resultado de saudação adequadamente e retornar **true**.

```csharp
class MyExceptionHandler : IExceptionHandler
{
    public bool TryHandleException(ExceptionInformation exceptionInformation, OperationRetrySettings retrySettings, out ExceptionHandlingResult result)
    {
        // if exceptionInformation.Exception is known and is transient (can be retried without re-resolving)
        result = new ExceptionHandlingRetryResult(exceptionInformation.Exception, true, retrySettings, retrySettings.DefaultMaxRetryCount);
        return true;


        // if exceptionInformation.Exception is known and is not transient (indicates a new service endpoint address must be resolved)
        result = new ExceptionHandlingRetryResult(exceptionInformation.Exception, false, retrySettings, retrySettings.DefaultMaxRetryCount);
        return true;

        // if exceptionInformation.Exception is unknown (let hello next IExceptionHandler attempt toohandle it)
        result = null;
        return false;
    }
}
```
```java
public class MyExceptionHandler implements ExceptionHandler {

    @Override
    public ExceptionHandlingResult handleException(ExceptionInformation exceptionInformation, OperationRetrySettings retrySettings) {        

        /* if exceptionInformation.getException() is known and is transient (can be retried without re-resolving)
         */
        result = new ExceptionHandlingRetryResult(exceptionInformation.getException(), true, retrySettings, retrySettings.getDefaultMaxRetryCount());
        return true;


        /* if exceptionInformation.getException() is known and is not transient (indicates a new service endpoint address must be resolved)
         */
        result = new ExceptionHandlingRetryResult(exceptionInformation.getException(), false, retrySettings, retrySettings.getDefaultMaxRetryCount());
        return true;

        /* if exceptionInformation.getException() is unknown (let hello next ExceptionHandler attempt toohandle it)
         */
        result = null;
        return false;

    }
}
```
### <a name="putting-it-all-together"></a>Juntando as peças
Com um `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`, e `IExceptionHandler(C#) / ExceptionHandler(Java)` criadas em torno de um protocolo de comunicação, um `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` encapsula todos juntos e fornece tratamento de falhas de saudação e loop de resolução de endereço de partição de serviço em torno desses componentes.

```csharp
private MyCommunicationClientFactory myCommunicationClientFactory;
private Uri myServiceUri;

var myServicePartitionClient = new ServicePartitionClient<MyCommunicationClient>(
    this.myCommunicationClientFactory,
    this.myServiceUri,
    myPartitionKey);

var result = await myServicePartitionClient.InvokeWithRetryAsync(async (client) =>
   {
      // Communicate with hello service using hello client.
   },
   CancellationToken.None);

```
```java
private MyCommunicationClientFactory myCommunicationClientFactory;
private URI myServiceUri;

FabricServicePartitionClient myServicePartitionClient = new FabricServicePartitionClient<MyCommunicationClient>(
    this.myCommunicationClientFactory,
    this.myServiceUri,
    myPartitionKey);

CompletableFuture<?> result = myServicePartitionClient.invokeWithRetryAsync(client -> {
      /* Communicate with hello service using hello client.
       */
   });

```

## <a name="next-steps"></a>Próximas etapas
* Confira um exemplo de comunicação HTTP entre serviços em um [projeto de exemplo C# no GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) ou [Projeto de exemplo Java no GitHub](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog).
* [Comunicação remota de serviço com os Reliable Services](service-fabric-reliable-services-communication-remoting.md)
* [API Web que usa o OWIN nos Reliable Services](service-fabric-reliable-services-communication-webapi.md)
* [Comunicação WCF usando os Reliable Services](service-fabric-reliable-services-communication-wcf.md)
