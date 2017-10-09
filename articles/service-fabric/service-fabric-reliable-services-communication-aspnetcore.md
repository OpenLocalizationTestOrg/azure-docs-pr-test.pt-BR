---
title: "comunicação aaaService com hello ASP.NET Core | Microsoft Docs"
description: "Saiba como toouse ASP.NET Core em serviços confiáveis com e sem monitoração."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 8aa4668d-cbb6-4225-bd2d-ab5925a868f2
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 05/02/2017
ms.author: vturecek
ms.openlocfilehash: 6e6a83ab04390150292f63de5d9b51d290284e50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-core-in-service-fabric-reliable-services"></a>Núcleo do ASP.NET em Serviços Confiáveis do Service Fabric

O Núcleo do ASP.NET é uma nova estrutura de software livre e plataforma cruzada para criar aplicativos modernos baseados em nuvem conectados à Internet, como aplicativos Web, aplicativos de IoT e back-ends móveis. 

Este artigo é uma toohosting guia detalhado ASP.NET Core services no serviço de malha serviços confiáveis usando Olá **Microsoft.ServiceFabric.AspNetCore.** * conjunto de pacotes do NuGet.

Para obter um tutorial de introdução sobre o ASP.NET Core no Service Fabric, além de instruções sobre como configurar o ambiente de desenvolvimento, consulte [Criando um front-end da Web para seu aplicativo usando o ASP.NET Core](service-fabric-add-a-web-frontend.md).

restante Olá deste artigo pressupõe que você já estiver familiarizado com o ASP.NET Core. Se não, é recomendável ler Olá [conceitos básicos do ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/index).

## <a name="aspnet-core-in-hello-service-fabric-environment"></a>ASP.NET Core no ambiente do Service Fabric Olá

Enquanto os aplicativos ASP.NET Core podem ser executado no .NET Core ou em Olá em que completa do .NET Framework, os serviços do Service Fabric atualmente só pode executar Olá .NET Framework completo. Isso significa que quando você criar um serviço do Service Fabric do ASP.NET Core, você deve direcionar ainda Olá .NET Framework completo.

O Núcleo do ASP.NET pode ser usado de duas maneiras diferentes no Service Fabric:
 - **Hospedado como um executável convidado**. Isso é principalmente usado toorun ASP.NET Core aplicativos existentes na malha do serviço sem alterações de código.
 - **Executar em um Serviço Confiável**. Isso permite melhor integração com o tempo de execução do Service Fabric hello e permite que os serviços com monitoração de estado do ASP.NET Core.

restante Olá este artigo explica como toouse ASP.NET Core dentro de um serviço confiável usando Olá componentes de integração do ASP.NET Core que vêm com hello SDK do Service Fabric. 

## <a name="service-fabric-service-hosting"></a>Hospedagem de serviços do Service Fabric

No Service Fabric, uma ou mais instâncias e/ou réplicas do serviço são executadas em um *processo de host do serviço*, um arquivo executável que executa o código de serviço. Como o autor de um serviço, possui processo de host de serviço hello e do Service Fabric ativa e monitora-lo para você.

O ASP.NET tradicional (backup tooMVC 5) é firmemente acopladas tooIIS por meio de System.Web.dll. ASP.NET Core fornece uma separação entre o servidor de web hello e seu aplicativo da web. Isso permite toobe de aplicativos web portáveis entre diversos servidores web e também permite que toobe de servidores de web *auto-hospedado*, que significa que você pode iniciar um servidor web no seu próprio processo, como um processo de tooa contrário é de propriedade da web dedicado software de servidor como o IIS. 

Em ordem toocombine um serviço de malha do serviço e o ASP.NET, como um executável de convidado ou em um serviço confiável, você deve ser capaz de toostart ASP.NET dentro de seu processo de host de serviço. ASP.NET Core auto-hospedagem permite toodo isso.

## <a name="hosting-aspnet-core-in-a-reliable-service"></a>Hospedando o Núcleo do ASP.NET em um Serviço Confiável
Normalmente, os aplicativos do ASP.NET Core auto-hospedado criam WebHost no ponto de entrada do aplicativo, como Olá `static void Main()` método `Program.cs`. Nesse caso, o ciclo de vida de saudação de saudação WebHost é toohello associado de ciclo de vida do processo de saudação.

![Hospedando o Núcleo do ASP.NET em um processo][0]

No entanto, ponto de entrada do aplicativo hello não Olá lugar certo toocreate WebHost em um serviço confiável, porque o ponto de entrada do aplicativo hello é usado somente tooregister um serviço digitar com tempo de execução do Service Fabric hello, para que ele pode criar instâncias de serviço tipo. Olá WebHost deve ser criado em um serviço confiável em si. No processo de host de serviço hello, instâncias de serviço e/ou réplicas podem passar por vários ciclos de vida. 

Uma instância de um serviço confiável é representada por sua classe de serviço derivando de `StatelessService` ou `StatefulService`. pilha de comunicação de saudação para um serviço está contida em um `ICommunicationListener` implementação em sua classe de serviço. Olá `Microsoft.ServiceFabric.Services.AspNetCore.*` pacotes do NuGet contenham implementações de `ICommunicationListener` que iniciar e gerenciar Olá ASP.NET Core WebHost para Kestrel ou WebListener em um serviço confiável.

![Hospedando o Núcleo do ASP.NET em um Serviço Confiável][1]

## <a name="aspnet-core-icommunicationlisteners"></a>Núcleo do ASP.NET ICommunicationListeners
Olá `ICommunicationListener` implementações para Kestrel e WebListener no hello `Microsoft.ServiceFabric.Services.AspNetCore.*` pacotes do NuGet têm padrões de uso semelhantes, mas executar o servidor de web específicos tooeach ações ligeiramente diferentes. 

Ambos os ouvintes de comunicação fornecem um construtor que aceite Olá argumentos a seguir:
 - **`ServiceContext serviceContext`**: Olá `ServiceContext` objeto que contém informações sobre Olá executando o serviço.
 - **`string endpointName`**: nome de saudação de um `Endpoint` configuração em ServiceManifest.xml. Isso é, principalmente, onde os ouvintes de comunicação Olá dois diferem: WebListener **requer** um `Endpoint` configuração, enquanto Kestrel não.
 - **`Func<string, AspNetCoreCommunicationListener, IWebHost> build`**: um lambda que você implementa e no qual cria e retorna um `IWebHost`. Isso permite tooconfigure `IWebHost` hello como faz normalmente em um aplicativo do ASP.NET Core. lambda Hello fornece uma URL que é gerada para você dependendo da integração do Service Fabric Olá opções use e hello `Endpoint` configuração que você fornecer. URL, em seguida, pode ser modificada ou usada como-é toostart Olá web server.

## <a name="service-fabric-integration-middleware"></a>Middleware de integração do Service Fabric
Olá `Microsoft.ServiceFabric.Services.AspNetCore` inclui o pacote NuGet Olá `UseServiceFabricIntegration` método de extensão no `IWebHostBuilder` que adiciona o middleware de reconhecimento de serviço do Fabric. Este middleware configura Olá Kestrel ou WebListener `ICommunicationListener` tooregister uma URL de serviço exclusivo com hello serviço de nomes de malha do serviço e, em seguida, valida os clientes tooensure de solicitações de cliente estão se conectando toohello certo de serviço. Isso é necessário em um ambiente de host compartilhado como Service Fabric, em que vários aplicativos web podem executar em Olá mesmo físico ou máquina virtual, mas não usam nomes de host exclusiva, tooprevent clientes conectem o serviço errada toohello por engano. Este cenário é descrito mais detalhadamente na próxima seção, Olá.

### <a name="a-case-of-mistaken-identity"></a>Um caso de identidade incorreta
Independentemente do protocolo, as réplicas de serviço escutam em uma combinação de IP:porta exclusiva. Após o início de uma réplica de serviço escuta em um ponto de extremidade IP: porta informa esse endereço de ponto de extremidade toohello serviço de nomenclatura do Service Fabric onde podem ser descoberto por clientes ou outros serviços. Se os serviços usam portas atribuídas dinamicamente o aplicativo, uma réplica de serviço podem usar Coincidentemente Olá mesmo ponto de extremidade IP: porta de outro serviço que foi previamente no hello mesmo físico ou máquina virtual. Isso pode fazer com que um cliente toomistakely conectar serviço errada toohello. Isso pode acontecer se Olá a sequência de eventos a seguir ocorre:

 1. O serviço A escuta em 10.0.0.1:30000 via HTTP. 
 2. O cliente resolve o serviço A e obtém o endereço 10.0.0.1:30000
 3. Move tooa outro nó do serviço.
 4. Serviço B é colocado na 10.0.0.1 e Coincidentemente usa Olá a mesma porta 30000.
 5. Cliente tenta tooconnect tooservice um com 10.0.0.1:30000 endereço em cache.
 6. Cliente está conectado com êxito tooservice B sem perceber que ele está conectado serviço errada toohello.

Isso pode causar erros em momentos aleatórios que podem ser difícil toodiagnose. 

### <a name="using-unique-service-urls"></a>Usando URLs de serviço exclusivas
Serviços de tooprevent isso, pode lançar um toohello Naming Service com um identificador exclusivo do ponto de extremidade e validar esse identificador exclusivo durante as solicitações de cliente. Essa é uma ação cooperativa entre serviços em um ambiente confiável de locatário não hostil. Isso não fornece autenticação segura em um ambiente de locatário hostil.

Em um ambiente confiável, Olá middleware é adicionada pelo Olá `UseServiceFabricIntegration` método anexa automaticamente um endereço de toohello de identificador exclusivo que é lançado toohello Naming Service e valida esse identificador em cada solicitação. Se o identificador de saudação não corresponder, Olá middleware imediatamente retorna uma resposta HTTP 410 não existe mais.

Os serviços que usam uma porta atribuída dinamicamente devem fazer uso desse middleware.

Os serviços que usam uma porta exclusiva fixa não têm esse problema em um ambiente cooperativo. Uma porta exclusiva fixa é normalmente usada para externamente serviços que precisam de uma porta conhecida para tooconnect de aplicativos cliente para. Por exemplo, a maioria dos aplicativos Web voltados para a Internet usará a porta 80 ou 443 para conexões do navegador da Web. Nesse caso, identificador exclusivo da saudação não deve ser habilitado.

Hello diagrama a seguir mostra o fluxo de solicitação Olá com middleware Olá habilitado:

![Integração de núcleo do ASP.NET do Service Fabric][2]

Kestrel e WebListener `ICommunicationListener` implementações usam esse mecanismo em exatamente Olá mesma maneira. Embora WebListener internamente pode diferenciar solicitações baseadas em caminhos de URL exclusivos usando Olá subjacente *http.sys* recurso, que é a funcionalidade de compartilhamento de porta *não* usado pelo Olá WebListener `ICommunicationListener` implementação porque isso resultará em códigos de status de erro HTTP 503 e HTTP 404 no cenário de saudação descrito anteriormente. Que por sua vez torna muito difícil para os clientes toodetermine Olá intenção erro hello, como HTTP 503 e HTTP 404 já são utilizado tooindicate outros erros. Assim, os Kestrel e WebListener `ICommunicationListener` implementações padronizem Olá middleware fornecido pelo Olá `UseServiceFabricIntegration` método de extensão para que os clientes precisam apenas tooperform um ponto de extremidade de serviço resolver ação em respostas HTTP 410 novamente.

## <a name="weblistener-in-reliable-services"></a>WebListener em Serviços Confiáveis
WebListener pode ser usado em um serviço confiável importando Olá **Microsoft.ServiceFabric.AspNetCore.WebListener** pacote NuGet. Este pacote contém `WebListenerCommunicationListener`, uma implementação de `ICommunicationListener`, que permite que você toocreate um host de Web ASP.NET Core dentro de um serviço confiável usando WebListener como servidor de web hello.

WebListener se baseia no hello [Windows HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510(v=vs.85).aspx). Isso usa Olá *http.sys* driver de kernel usada pelo IIS tooprocess HTTP solicita e rotear tooprocesses-los executar aplicativos da web. Isso permite que vários processos em Olá mesmos aplicativos de máquina virtual ou física de toohost web hello mesma porta, a ambiguidade removida por um caminho de URL exclusivo ou o nome do host. Esses recursos são úteis na malha do serviço para hospedar vários sites em Olá mesmo cluster.

Olá diagrama a seguir ilustra como WebListener usa Olá *http.sys* driver de kernel no Windows para o compartilhamento de porta:

![http.sys][3]

### <a name="weblistener-in-a-stateless-service"></a>WebListener em um serviço sem estado
toouse `WebListener` em um serviço sem monitoração de estado, substituir Olá `CreateServiceInstanceListeners` método e retornar um `WebListenerCommunicationListener` instância:

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    return new ServiceInstanceListener[]
    {
        new ServiceInstanceListener(serviceContext =>
            new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
                new WebHostBuilder()
                    .UseWebListener()
                    .ConfigureServices(
                        services => services
                            .AddSingleton<StatelessServiceContext>(serviceContext))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build()))
    };
}
```

### <a name="weblistener-in-a-stateful-service"></a>WebListener em um serviço com estado

`WebListenerCommunicationListener`no momento não foi projetado para uso em serviços com monitoração de estado toocomplications vencimento com hello subjacente *http.sys* o recurso de compartilhamento de porta. Para obter mais informações, consulte Olá na alocação de porta dinâmica com WebListener a seção seguinte. Para os serviços com monitoração de estado, Kestrel é hello recomendado de servidor web.

### <a name="endpoint-configuration"></a>Configuração de ponto de extremidade

Um `Endpoint` configuração é necessária para servidores web que usam Olá Windows HTTP Server API, incluindo WebListener. Servidores Web que usam Olá Windows HTTP Server API primeiro devem reservar a URL com *http.sys* (normalmente, isso é feito com hello [netsh](https://msdn.microsoft.com/library/windows/desktop/cc307236(v=vs.85).aspx) ferramenta). Esta ação exige privilégios elevados que seus serviços não têm por padrão. Olá "http" ou "https" opções de saudação `Protocol` propriedade Olá `Endpoint` configuração no *ServiceManifest.xml* são usadas especificamente tooinstruct Olá tooregister de tempo de execução do Service Fabric uma URL com *http.sys* em seu nome usando Olá [ *curinga forte* ](https://msdn.microsoft.com/library/windows/desktop/aa364698(v=vs.85).aspx) prefixo de URL.

Por exemplo, tooreserve `http://+:80` para um serviço, hello seguinte configuração deve ser usada em ServiceManifest.xml:

```xml
<ServiceManifest ... >
    ...
    <Resources>
        <Endpoints>
            <Endpoint Name="ServiceEndpoint" Protocol="http" Port="80" />
        </Endpoints>
    </Resources>

</ServiceManifest>
```

E o nome do ponto de extremidade Olá deve ser passado toohello `WebListenerCommunicationListener` construtor:

```csharp
 new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
 {
     return new WebHostBuilder()
         .UseWebListener()
         .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
         .UseUrls(url)
         .Build();
 })
```

#### <a name="use-weblistener-with-a-static-port"></a>Usar WebListener com uma porta estática
toouse uma porta estática com WebListener, forneça o número de porta de saudação em Olá `Endpoint` configuração:

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

#### <a name="use-weblistener-with-a-dynamic-port"></a>Usar WebListener com uma porta dinâmica
toouse uma porta dinamicamente atribuída com WebListener, omita Olá `Port` propriedade Olá `Endpoint` configuração:

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" />
    </Endpoints>
  </Resources>
```

Observe que uma porta dinâmica alocada por uma configuração `Endpoint` fornece apenas uma porta *por processo de host*. Olá Service Fabric atual do modelo de hospedagem permite toobe vários para o instâncias e/ou réplicas do serviço hospedado no hello mesmo processo, que significa que cada um deles compartilharão Olá mesma porta quando alocados por meio do hello `Endpoint` configuração. Várias instâncias de WebListener podem compartilhar uma porta usando Olá subjacente *http.sys* porta compartilhamento de recurso, mas que não é suportada pelo `WebListenerCommunicationListener` devido complicações toohello ele apresenta solicitações do cliente. Para o uso de portas dinâmicas, Kestrel é hello recomendado de servidor web.

## <a name="kestrel-in-reliable-services"></a>Kestrel em Serviços Confiáveis
Kestrel pode ser usado em um serviço confiável importando Olá **Microsoft.ServiceFabric.AspNetCore.Kestrel** pacote NuGet. Este pacote contém `KestrelCommunicationListener`, uma implementação de `ICommunicationListener`, que permite que você toocreate um host de Web ASP.NET Core dentro de um serviço confiável usando Kestrel como servidor de web hello.

O Kestrel é um servidor Web de plataforma cruzada para o Núcleo do ASP.NET com base em libuv, uma biblioteca de E/S assíncrona de plataforma cruzada. Diferentemente do WebListener, o Kestrel usa um gerenciador de ponto de extremidade centralizado como *http.sys*. Diferentemente do WebListener, Kestrel não dá suporte ao compartilhamento de porta entre vários processos. Cada instância do Kestrel deve usar uma porta exclusiva.

![kestrel][4]

### <a name="kestrel-in-a-stateless-service"></a>Kestrel em um serviço sem estado
toouse `Kestrel` em um serviço sem monitoração de estado, substituir Olá `CreateServiceInstanceListeners` método e retornar um `KestrelCommunicationListener` instância:

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    return new ServiceInstanceListener[]
    {
        new ServiceInstanceListener(serviceContext =>
            new KestrelCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
                new WebHostBuilder()
                    .UseKestrel()
                    .ConfigureServices(
                        services => services
                            .AddSingleton<StatelessServiceContext>(serviceContext))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.UseUniqueServiceUrl)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build();
            ))
    };
}
```

### <a name="kestrel-in-a-stateful-service"></a>Kestrel em um serviço com estado
toouse `Kestrel` em um serviço com monitoração de estado, substituir Olá `CreateServiceReplicaListeners` método e retornar um `KestrelCommunicationListener` instância:

```csharp
protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new ServiceReplicaListener[]
    {
        new ServiceReplicaListener(serviceContext =>
            new KestrelCommunicationListener(serviceContext, (url, listener) =>
                new WebHostBuilder()
                    .UseKestrel()
                    .ConfigureServices(
                         services => services
                             .AddSingleton<StatefulServiceContext>(serviceContext)
                             .AddSingleton<IReliableStateManager>(this.StateManager))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.UseUniqueServiceUrl)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build();
            ))
    };
}
```

Neste exemplo, uma instância singleton do `IReliableStateManager` é fornecido o contêiner de injeção de dependência de WebHost toohello. Isso não é estritamente necessário, mas permite que você toouse `IReliableStateManager` e coleções confiável em métodos de ação do controlador MVC.

Observe que uma `Endpoint` nome de configuração é **não** fornecido muito`KestrelCommunicationListener` em um serviço com monitoração de estado. Isso é explicado mais detalhadamente Olá seção a seguir.

### <a name="endpoint-configuration"></a>Configuração de ponto de extremidade
Um `Endpoint` configuração não é necessário toouse Kestrel. 

Kestrel é um servidor web autônomo simples; Diferentemente de WebListener (ou HttpListener), não é necessário um `Endpoint` configuração no *ServiceManifest.xml* porque ele não requer toostarting anterior do registro de URL. 

#### <a name="use-kestrel-with-a-static-port"></a>Usar Kestrel com uma porta estática
Uma porta estática pode ser configurada no hello `Endpoint` configuração do ServiceManifest.xml para uso com Kestrel. Embora não seja estritamente necessário, há dois benefícios potenciais:
 1. Se a porta de saudação não está no intervalo de portas de aplicativo hello, ele é aberto através do firewall do sistema operacional Olá pela malha do serviço.
 2. Olá tooyou URL fornecida por meio de `KestrelCommunicationListener` usará essa porta.

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

Se um `Endpoint` é configurado, seu nome deve ser passado para Olá `KestrelCommunicationListener` construtor: 

```csharp
new KestrelCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) => ...
```

Se um `Endpoint` configuração não for usada, omitir o nome da saudação em Olá `KestrelCommunicationListener` construtor. Nesse caso, uma porta dinâmica será usada. Consulte a próxima seção Olá para obter mais informações.

#### <a name="use-kestrel-with-a-dynamic-port"></a>Usar Kestrel com uma porta dinâmica
Kestrel não é possível usar a atribuição de porta automática de saudação do hello `Endpoint` configuração em ServiceManifest.xml, porque a atribuição automática de porta de um `Endpoint` configuração atribui uma porta exclusiva por *processo de host* , e um processo de host único pode conter várias instâncias de Kestrel. Como o Kestrel não dá suporte ao compartilhamento de porta, isso não funciona, pois cada instância do Kestrel deve ser aberta em uma porta exclusiva.

atribuição de porta dinâmica toouse com Kestrel, basta omitir Olá `Endpoint` configuração em ServiceManifest.xml totalmente e não passe um toohello de nome de ponto de extremidade `KestrelCommunicationListener` construtor:

```csharp
new KestrelCommunicationListener(serviceContext, (url, listener) => ...
```

Nessa configuração, `KestrelCommunicationListener` automaticamente selecionará uma porta não utilizada do intervalo de portas de aplicativo hello.

## <a name="scenarios-and-configurations"></a>Cenários e configurações
Esta seção descreve os seguintes cenários de saudação e fornece Olá recomendado combinação de servidor web, configuração de porta, opções de integração do Service Fabric e configurações diversas tooachieve um serviço estejam funcionando adequadamente:
 - serviço sem estado do Núcleo do ASP.NET exposto externamente
 - Serviço do Núcleo do ASP.NET sem estado somente para uso interno
 - serviço com estado do Núcleo do ASP.NET somente interno

Um **exposta externamente** serviço é aquele que expõe um ponto de extremidade pode ser acessado de fora de cluster hello, normalmente por meio de um balanceador de carga.

Um **somente interno** o serviço é uma cujo ponto de extremidade só é acessível a partir do cluster de saudação.

> [!NOTE]
> Serviço com monitoração de estado de pontos de extremidade geralmente não devem ser expostos toohello da Internet. Clusters que estão por trás de balanceadores de carga que não têm reconhecimento de resolução de serviço de malha do serviço, como Olá balanceador de carga do Azure, poderá ser services com monitoração de estado tooexpose não é possível porque o balanceador de carga de saudação não ser capaz de toolocate e rotear o tráfego toohello réplica de serviço com monitoração de estado apropriado. 

### <a name="externally-exposed-aspnet-core-stateless-services"></a>Serviços sem monitoração de estado do Núcleo do ASP.NET expostos externamente
WebListener é hello recomendado de servidor web para serviços de front-end que expõem externos, voltados para Internet pontos de extremidade HTTP no Windows. Ele oferece melhor proteção contra ataques e suporte a recursos para os quais o Kestrel não tem suporte, como a Autenticação do Windows e o compartilhamento de portas. 

Não há suporte para o Kestrel como um servidor de borda (para a Internet) no momento. Deve ser usado um servidor proxy reverso como o IIS ou Nginx Olá de toohandle tráfego da Internet pública.
 
Toohello exposto à Internet, um serviço sem monitoração de estado quando usar um ponto de extremidade estável e bem conhecido que pode ser acessado por meio de um balanceador de carga. Este é o URL Olá fornecerá toousers do seu aplicativo. é recomendável Olá a seguinte configuração:

|  |  | **Observações** |
| --- | --- | --- |
| Servidor Web | WebListener | Se o serviço de saudação é apenas tooa exposto rede confiável, intranet, Kestrel pode ser usado. Caso contrário, WebListener é a opção Olá preferido. |
| Configuração de portas | estático | Uma porta estática conhecida deve ser configurada no hello `Endpoints` configuração do ServiceManifest.xml, como 80 para HTTP ou 443 para HTTPS. |
| ServiceFabricIntegrationOptions | Nenhum | Olá `ServiceFabricIntegrationOptions.None` opção deve ser usada ao configurar o middleware de integração do Service Fabric para que o serviço de saudação não tentará toovalidate solicitações de entrada para um identificador exclusivo. Os usuários externos do seu aplicativo não saberá Olá exclusivo informações de identificação usadas pelo middleware de saudação. |
| Contagem de Instâncias | -1 | Em casos típicos de uso, a configuração de contagem de instância Olá deverá ser definida muito "-1" para que uma instância está disponível em todos os nós que recebe o tráfego de um balanceador de carga. |

Se vários serviços expostos externamente compartilharem Olá mesmo conjunto de nós, um caminho de URL exclusivo mas estável deve ser usado. Isso pode ser feito modificando Olá URL fornecida ao configurar IWebHost. Observe que isso se aplica somente a tooWebListener.

 ```csharp
 new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
 {
     url += "/MyUniqueServicePath";
 
     return new WebHostBuilder()
         .UseWebListener()
         ...
         .UseUrls(url)
         .Build();
 })
 ```

### <a name="internal-only-stateless-aspnet-core-service"></a>Serviço do Núcleo do ASP.NET sem estado somente para uso interno
Serviços sem monitoração de estado que só são chamados de dentro do cluster Olá devem usar URLs exclusivas e portas atribuídas dinamicamente tooensure cooperação entre vários serviços. é recomendável Olá a seguinte configuração:

|  |  | **Observações** |
| --- | --- | --- |
| Servidor Web | Kestrel | Embora WebListener pode ser usado para serviços sem monitoração de estado internos, Kestrel é Olá recomendado server tooallow várias tooshare de instâncias de serviço um host.  |
| Configuração de portas | atribuídas dinamicamente | Várias réplicas de um serviço com estado podem compartilhar um processo de host ou o sistema operacional do host e, assim, precisarão de portas exclusivas. |
| ServiceFabricIntegrationOptions | UseUniqueServiceUrl | Com a atribuição de porta dinâmica, essa configuração impede o problema de identidade Olá enganado descrito anteriormente. |
| InstanceCount | qualquer | a configuração de contagem de instância Olá pode ser definida como serviço de saudação do tooany valor toooperate necessário. |

### <a name="internal-only-stateful-aspnet-core-service"></a>Somente interno serviço com estado do Núcleo do ASP.NET
Serviços com monitoração de estado que só são chamados de dentro do cluster Olá devem usar portas atribuídas dinamicamente tooensure cooperação entre vários serviços. é recomendável Olá a seguinte configuração:

|  |  | **Observações** |
| --- | --- | --- |
| Servidor Web | Kestrel | Olá `WebListenerCommunicationListener` não foi projetado para uso por serviços com monitoração de estado em que réplicas compartilham um processo de host. |
| Configuração de portas | atribuídas dinamicamente | Várias réplicas de um serviço com estado podem compartilhar um processo de host ou o sistema operacional do host e, assim, precisarão de portas exclusivas. |
| ServiceFabricIntegrationOptions | UseUniqueServiceUrl | Com a atribuição de porta dinâmica, essa configuração impede o problema de identidade Olá enganado descrito anteriormente. |

## <a name="next-steps"></a>Próximas etapas
[Depurar seu aplicativo do Service Fabric usando o Visual Studio](service-fabric-debugging-your-application.md)

<!--Image references-->
[0]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-standalone.png
[1]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-servicefabric.png
[2]:./media/service-fabric-reliable-services-communication-aspnetcore/integration.png
[3]:./media/service-fabric-reliable-services-communication-aspnetcore/httpsys.png
[4]:./media/service-fabric-reliable-services-communication-aspnetcore/kestrel.png
