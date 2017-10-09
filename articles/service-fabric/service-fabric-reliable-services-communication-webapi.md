---
title: "comunicação aaaService com hello ASP.NET Web API | Microsoft Docs"
description: "Saiba como comunicação de serviço tooimplement passo a passo usando Olá API da Web ASP.NET com OWIN auto-hospedagem em Olá confiável API de serviços."
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
ms.date: 02/10/2017
ms.author: vturecek
redirect_url: /azure/service-fabric/service-fabric-reliable-services-communication-aspnetcore
ms.openlocfilehash: 3fb18fcb141ada0d79a0acda3dccbc7fb044346d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-service-fabric-web-api-services-with-owin-self-hosting"></a>Introdução aos serviços de API Web do Service Fabric com auto-hospedagem OWIN
Malha do Azure do serviço coloca power Olá em suas mãos ao decidir como deseja que seu toocommunicate serviços com usuários e entre si. Este tutorial se concentra na implementação da comunicação de serviço usando a API Web ASP.NET com auto-hospedagem OWIN (Open Web Interface for .NET) na API dos Reliable Services do Service Fabric. Será examinarmos profundamente Olá comunicação de serviços confiáveis conectável API. Também usaremos API da Web em um exemplo passo a passo tooshow você como tooset a um ouvinte de comunicação personalizados.

## <a name="introduction-tooweb-api-in-service-fabric"></a>Introdução tooWeb API no serviço de malha
API da Web do ASP.NET é uma estrutura popular e avançada para a criação de APIs de HTTP na parte superior de saudação do .NET Framework. Se você não ainda estiver familiarizado com o framework hello, consulte [guia de Introdução ao ASP.NET Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) toolearn mais.

API da Web no serviço de malha é Olá mesmo ASP.NET Web API você conhece e adora. Olá diferença é como você *host* um aplicativo de API da Web. Você não usará o IIS (Serviços de Informações da Internet) da Microsoft. toobetter entender a diferença Olá, vamos dividi-lo em duas partes:

1. aplicativo de API da Web Hello (incluindo controladores e modelos)
2. host de saudação (servidor web hello, geralmente IIS)

O aplicativo de API Web, em si, não muda. Ele não é diferente de aplicativos de API da Web que você pode ter escrito em Olá anterior, e você deve ser toosimply capaz de mover grande parte do código do aplicativo. Mas se você foi hospedando no IIS, onde você hospedar o aplicativo hello pode ser um pouco diferente do que você está acostumado. Antes de entrarmos toohello parte de hospedagem, vamos começar com algo mais familiar: Olá aplicativo de API da Web.

## <a name="create-hello-application"></a>Criar um aplicativo hello
Comece criando um novo aplicativo do Service Fabric com um único serviço sem estado no Visual Studio 2015.

Um modelo do Visual Studio para um serviço sem monitoração de estado usando a API da Web é tooyou disponível. Neste tutorial, vamos criar um projeto de API da Web do zero que resulta no que você obteria se você selecionasse esse modelo.

Selecione um toolearn de projeto de serviço sem monitoração de estado em branco como toobuild um projeto de API da Web do zero, ou você pode iniciar com o serviço sem monitoração de estado de saudação modelo API da Web e simplesmente acompanhar.  

Olá primeira etapa é toopull em alguns pacotes do NuGet para a API da Web. pacote de saudação queremos toouse é Microsoft.AspNet.WebApi.OwinSelfHost. Este pacote inclui todos os pacotes necessários de API da Web hello e Olá *host* pacotes. Isso será importante mais tarde.

Depois que os pacotes de saudação foram instalados, você pode começar a criação de estrutura de projeto de API da Web básica hello. Se você tiver usado um API da Web, a estrutura do projeto Olá deve ser bastante familiar. Comece adicionando um diretório `Controllers` e um controlador de valores simples:

**ValuesController.cs**

```csharp
using System.Collections.Generic;
using System.Web.Http;

namespace WebService.Controllers
{
    public class ValuesController : ApiController
    {
        // GET api/values 
        public IEnumerable<string> Get()
        {
            return new string[] { "value1", "value2" };
        }

        // GET api/values/5 
        public string Get(int id)
        {
            return "value";
        }

        // POST api/values 
        public void Post([FromBody]string value)
        {
        }

        // PUT api/values/5 
        public void Put(int id, [FromBody]string value)
        {
        }

        // DELETE api/values/5 
        public void Delete(int id)
        {
        }
    }
}

```

Em seguida, adicione uma classe de inicialização em Olá Olá projeto raiz tooregister roteamento formatadores e qualquer outra configuração. Isso também é onde o API da Web conecta-se em toohello *host*, que será revisto novamente mais tarde. 

**Startup.cs**

```csharp
using System.Web.Http;
using Owin;

namespace WebService
{
    public static class Startup
    {
        public static void ConfigureApp(IAppBuilder appBuilder)
        {
            // Configure Web API for self-host. 
            HttpConfiguration config = new HttpConfiguration();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );

            appBuilder.UseWebApi(config);
        }
    }
}
```

Isso é tudo para parte do aplicativo hello. Neste ponto, criamos apenas Olá API da Web projeto layout básico. Até agora, não deve ser muito diferente de projetos Web API que você pode ter escrito em Olá anterior ou de modelo de API da Web básico hello. Sua lógica de negócios fica em modelos e controladores hello como de costume.

Agora o que fazemos com a hospedagem para que possamos executá-la de fato?

## <a name="service-hosting"></a>Hospedagem do serviço
No Service Fabric, seu serviço é executado em um *processo de host do serviço*, um arquivo executável que executa o código do serviço. Quando você escreve um serviço usando Olá confiável API de serviços, o seu projeto de serviço apenas compila tooan arquivo executável que registra o tipo de serviço e execute seu código. Isso se aplica à maioria dos casos em que você escreve um serviço no Service Fabric no .NET. Quando você abrir Program.cs no projeto de serviço sem monitoração de estado hello, você verá:

```csharp
using System;
using System.Diagnostics;
using System.Threading;
using Microsoft.ServiceFabric.Services.Runtime;

internal static class Program
{
    private static void Main()
    {
        try
        {
            ServiceRuntime.RegisterServiceAsync("WebServiceType",
                context => new WebService(context)).GetAwaiter().GetResult();

            ServiceEventSource.Current.ServiceTypeRegistered(Process.GetCurrentProcess().Id, typeof(WebService).Name);

            // Prevents this host process from terminating so services keeps running. 
            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ServiceEventSource.Current.ServiceHostInitializationFailed(e.ToString());
            throw;
        }
    }
}

```

Se isso se parece anormalmente com o aplicativo de console de tooa de ponto de entrada hello, isso ocorre porque é.

Mais detalhes sobre o processo de host do serviço de hello e registro de serviço estão além do escopo deste artigo hello. Mas é importante tooknow para agora que *seu código de serviço está em execução em seu próprio processo*.

## <a name="self-host-web-api-with-an-owin-host"></a>Auto-hospedar a API Web com um host OWIN
Considerando que o código do aplicativo de API da Web é hospedado em seu próprio processo, como associá-lo tooa servidor de web? Digite [OWIN](http://owin.org/). OWIN é simplesmente um contrato entre aplicativos web do .NET e servidores web. Tradicionalmente quando ASP.NET (backup tooMVC 5) é usado, o aplicativo de web de saudação é firmemente acopladas tooIIS por meio de System. Web. No entanto, a API da Web implementa OWIN, portanto você pode escrever um aplicativo web que é separado do servidor da web hello que o hospeda. Por isso, você pode usar um servidor Web OWIN *auto-hospedado* que pode ser iniciado em seu próprio processo. Isso se ajusta perfeitamente com o modelo de host de malha do serviço do hello que acabamos de descrever.

Neste artigo, vamos usar Katana como host do OWIN Olá para Olá aplicativo de API da Web. Katana é uma implementação de host do código-fonte aberto OWIN criada em [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx) e Olá Windows [HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx).

> [!NOTE]
> toolearn mais sobre Katana, vá toohello [Katana site](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana). Para uma visão geral de como toouse Katana tooself host da Web API, consulte [OWIN de uso tooSelf Host ASP.NET Web API 2](http://www.asp.net/web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api).
> 
> 

## <a name="set-up-hello-web-server"></a>Configurar o servidor de web Olá
Olá confiável API de serviços fornece um ponto de entrada de comunicação em que você pode conectar pilhas de comunicação que permitem que os usuários e o serviço de toohello de tooconnect de clientes:

```csharp

protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}

```

servidor web de saudação (e qualquer pilha de comunicação que você usar Olá futura, como WebSockets) devem usar Olá ICommunicationListener interface toointegrate corretamente com o sistema de saudação. motivos Olá se tornará mais aparentes na Olá etapas a seguir.

Primeiro, crie uma classe chamada OwinCommunicationListener que implementa ICommunicationListener:

**OwinCommunicationListener.cs**

```csharp
using Microsoft.Owin.Hosting;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Owin;
using System;
using System.Fabric;
using System.Globalization;
using System.Threading;
using System.Threading.Tasks;

namespace WebService
{
    internal class OwinCommunicationListener : ICommunicationListener
    {
        public void Abort()
        {
        }

        public Task CloseAsync(CancellationToken cancellationToken)
        {
        }

        public Task<string> OpenAsync(CancellationToken cancellationToken)
        {
        }
    }
}
```

interface de ICommunicationListener Olá fornece três toomanage de métodos um ouvinte de comunicação para seu serviço:

* *OpenAsync*. Começar a ouvir solicitações.
* *CloseAsync*. Parar de ouvir solicitações, concluir todas as solicitações em andamento e desligar normalmente.
* *Anular*. Cancelar tudo e parar imediatamente.

tooget iniciado, adicionar membros de classe particular para escuta de saudação coisas, será preciso toofunction. Esses serão inicializados pelo construtor hello e usados mais tarde, quando você configura o hello escutando URL.

```csharp
internal class OwinCommunicationListener : ICommunicationListener
{
    private readonly ServiceEventSource eventSource;
    private readonly Action<IAppBuilder> startup;
    private readonly ServiceContext serviceContext;
    private readonly string endpointName;
    private readonly string appRoot;

    private IDisposable webApp;
    private string publishAddress;
    private string listeningAddress;

    public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName)
        : this(startup, serviceContext, eventSource, endpointName, null)
    {
    }

    public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName, string appRoot)
    {
        if (startup == null)
        {
            throw new ArgumentNullException(nameof(startup));
        }

        if (serviceContext == null)
        {
            throw new ArgumentNullException(nameof(serviceContext));
        }

        if (endpointName == null)
        {
            throw new ArgumentNullException(nameof(endpointName));
        }

        if (eventSource == null)
        {
            throw new ArgumentNullException(nameof(eventSource));
        }

        this.startup = startup;
        this.serviceContext = serviceContext;
        this.endpointName = endpointName;
        this.eventSource = eventSource;
        this.appRoot = appRoot;
    }


    ...

```

## <a name="implement-openasync"></a>Implementar o OpenAsync
tooset servidor de web hello, você precisa de duas informações:

* *Um prefixo de caminho de URL*. Embora seja opcional, é bom para você tooset esse backup agora para que você com segurança pode hospedar vários serviços web em seu aplicativo.
* *Uma porta*.

Antes de obter uma porta para o servidor de web hello, é importante entender que o Service Fabric fornece uma camada de aplicativo que atua como um buffer entre seu aplicativo e o sistema operacional subjacente Olá que ele é executado em. Dessa forma, o Service Fabric fornece uma maneira tooconfigure *pontos de extremidade* para seus serviços. Service Fabric garante que os pontos de extremidade estão disponíveis para seu serviço toouse. Dessa forma, você não tem tooconfigure-las por conta própria Olá subjacente do ambiente de sistema operacional. Facilmente, você pode hospedar seu aplicativo de serviço de malha em ambientes diferentes sem ter que toomake qualquer aplicativo tooyour de alterações. (Por exemplo, você pode hospedar Olá mesmo aplicativo no Azure ou em seu próprio datacenter.)

Configure um ponto de extremidade de HTTP em PackageRoot\ServiceManifest.xml:

```xml
<Resources>
    <Endpoints>
        <Endpoint Name="ServiceEndpoint" Type="Input" Protocol="http" Port="8281" />
    </Endpoints>
</Resources>

```

Esta etapa é importante porque o processo de host de serviço Olá é executado sob credenciais restritas (serviço de rede no Windows). Isso significa que seu serviço não terá acesso tooset um ponto de extremidade HTTP por conta própria. Usando a configuração de ponto de extremidade Olá, Service Fabric sabe tooset a lista de controle de acesso (ACL) Olá para Olá URL Olá serviço escutará. Serviço de malha também fornece um local padrão tooconfigure pontos de extremidade.

Em OwinCommunicationListener.cs, você pode começar a implementar o OpenAsync. Isso é onde você iniciar o servidor de web hello. Primeiro, obter informações de ponto de extremidade hello e criar URL Olá que serviço Olá escutará. Olá URL será diferente dependendo se o ouvinte de saudação é usado em um serviço sem monitoração de estado ou de um serviço com monitoração de estado. Para um serviço com monitoração de estado, o ouvinte Olá precisa toocreate um único endereço para cada réplica de serviço com monitoração de estado ele escuta em. Para serviços sem monitoração de estado, o endereço de saudação pode ser muito mais simples. 

```csharp
public Task<string> OpenAsync(CancellationToken cancellationToken)
{
    var serviceEndpoint = this.serviceContext.CodePackageActivationContext.GetEndpoint(this.endpointName);
    var protocol = serviceEndpoint.Protocol;
    int port = serviceEndpoint.Port;

    if (this.serviceContext is StatefulServiceContext)
    {
        StatefulServiceContext statefulServiceContext = this.serviceContext as StatefulServiceContext;

        this.listeningAddress = string.Format(
            CultureInfo.InvariantCulture,
            "{0}://+:{1}/{2}{3}/{4}/{5}",
            protocol,
            port,
            string.IsNullOrWhiteSpace(this.appRoot)
                ? string.Empty
                : this.appRoot.TrimEnd('/') + '/',
            statefulServiceContext.PartitionId,
            statefulServiceContext.ReplicaId,
            Guid.NewGuid());
    }
    else if (this.serviceContext is StatelessServiceContext)
    {
        this.listeningAddress = string.Format(
            CultureInfo.InvariantCulture,
            "{0}://+:{1}/{2}",
            protocol,
            port,
            string.IsNullOrWhiteSpace(this.appRoot)
                ? string.Empty
                : this.appRoot.TrimEnd('/') + '/');
    }
    else
    {
        throw new InvalidOperationException();
    }

    ...

```

Observe que "http://+" é usado aqui. Isso é toomake-se de que o servidor web hello está escutando em todos os endereços disponíveis, incluindo localhost, o FQDN e o IP da máquina de saudação.

Olá OpenAsync implementação é um dos motivos mais importantes hello, por que o servidor de web hello (ou qualquer pilha de comunicação) é implementada como um ICommunicationListener, em vez de apenas com ele aberto diretamente do `RunAsync()` no serviço de saudação. valor de retorno de saudação do OpenAsync é endereço Olá Olá servidor web está escutando. Quando esse endereço é retornado toohello sistema, ele registra o endereço Olá com serviço Olá. Serviço de malha fornece uma API que permite que os clientes e outros serviços toothen peça para este endereço por nome de serviço. Isso é importante porque o endereço do serviço Olá não é estático. Os serviços são movidos em torno de cluster Olá para fins de disponibilidade e balanceamento de recursos. Esse é o mecanismo de saudação que permite que os clientes tooresolve Olá endereço para um serviço de escuta.

Com isso em mente, OpenAsync inicia Olá web server e retorna endereço Olá que ele está escutando. Observe que escuta "http://+", mas antes de OpenAsync retorna o endereço de hello, Olá "+" é substituído pelo Olá IP ou FQDN do nó hello está em. endereço de saudação que é retornado por esse método é o que está registrado no sistema de saudação. Também é o que os clientes e outros serviços veem quando eles solicitam um endereço do serviço. Para clientes toocorrectly conectar tooit, eles precisam de um IP ou o FQDN real no endereço hello.

```csharp
    ...

    this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

    try
    {
        this.eventSource.Message("Starting web server on " + this.listeningAddress);

        this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

        this.eventSource.Message("Listening on " + this.publishAddress);

        return Task.FromResult(this.publishAddress);
    }
    catch (Exception ex)
    {
        this.eventSource.Message("Web server failed tooopen endpoint {0}. {1}", this.endpointName, ex.ToString());

        this.StopWebServer();

        throw;
    }
}

```

Observe que isso faz referência a classe de inicialização de saudação que foi passado toohello OwinCommunicationListener no construtor de saudação. Esta instância de inicialização é usada pelo Olá web server toobootstrap Olá aplicativo de API da Web.

Olá `ServiceEventSource.Current.Message()` linha aparecerá na janela de eventos de diagnóstico hello mais tarde, quando você executa Olá aplicativo tooconfirm que o servidor web hello foi iniciado com êxito.

## <a name="implement-closeasync-and-abort"></a>Implementar CloseAsync e Abort
Finalmente, implemente CloseAsync e anulação de servidor de web toostop hello. servidor de web Hello pode ser interrompida com a eliminação de identificador de servidor de saudação que foi criado durante OpenAsync.

```csharp
public Task CloseAsync(CancellationToken cancellationToken)
{
    this.eventSource.Message("Closing web server on endpoint {0}", this.endpointName);

    this.StopWebServer();

    return Task.FromResult(true);
}

public void Abort()
{
    this.eventSource.Message("Aborting web server on endpoint {0}", this.endpointName);

    this.StopWebServer();
}

private void StopWebServer()
{
    if (this.webApp != null)
    {
        try
        {
            this.webApp.Dispose();
        }
        catch (ObjectDisposedException)
        {
            // no-op
        }
    }
}
```

Neste exemplo de implementação, CloseAsync e anular simplesmente parar servidor de web de saudação. Você pode optar por tooperform um desligamento mais normalmente coordenado saudação do servidor de web em CloseAsync. Por exemplo, desligamento Olá podia aguardar toobe de solicitações em andamento, concluído antes de retornar de saudação.

## <a name="start-hello-web-server"></a>Iniciar o servidor de web Olá
Você agora está pronto toocreate e retorna uma instância de servidor de web OwinCommunicationListener toostart hello. Olá a classe de serviço (WebService.cs), em Substituir Olá `CreateServiceInstanceListeners()` método:

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    var endpoints = Context.CodePackageActivationContext.GetEndpoints()
                           .Where(endpoint => endpoint.Protocol == EndpointProtocol.Http || endpoint.Protocol == EndpointProtocol.Https)
                           .Select(endpoint => endpoint.Name);

    return endpoints.Select(endpoint => new ServiceInstanceListener(
        serviceContext => new OwinCommunicationListener(Startup.ConfigureApp, serviceContext, ServiceEventSource.Current, endpoint), endpoint));
}
```

Isso é onde Olá API da Web *aplicativo* e Olá OWIN *host* finalmente atender. host de saudação (OwinCommunicationListener) é fornecido como uma instância de saudação *aplicativo* (API da Web) por meio de saudação classe de inicialização. O Service Fabric gerencia seu ciclo de vida. Esse mesmo padrão normalmente pode ser seguido com qualquer pilha de comunicação.

## <a name="put-it-all-together"></a>Colocar tudo isso junto
Neste exemplo, você não precisa toodo tudo em Olá `RunAsync()` método, portanto essa substituição simplesmente pode ser removida.

implementação de serviço final Olá deve ser bem simple. Ele só precisa de ouvinte de comunicação Olá toocreate:

```csharp
using System;
using System.Collections.Generic;
using System.Fabric;
using System.Fabric.Description;
using System.Linq;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

namespace WebService
{
    internal sealed class WebService : StatelessService
    {
        public WebService(StatelessServiceContext context)
            : base(context)
        { }

        protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
        {
            var endpoints = Context.CodePackageActivationContext.GetEndpoints()
                                   .Where(endpoint => endpoint.Protocol == EndpointProtocol.Http || endpoint.Protocol == EndpointProtocol.Https)
                                   .Select(endpoint => endpoint.Name);

            return endpoints.Select(endpoint => new ServiceInstanceListener(
                serviceContext => new OwinCommunicationListener(Startup.ConfigureApp, serviceContext, ServiceEventSource.Current, endpoint), endpoint));
        }
    }
}
```

Olá completa `OwinCommunicationListener` classe:

```csharp
using System;
using System.Diagnostics;
using System.Fabric;
using System.Globalization;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.Owin.Hosting;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Owin;

namespace WebService
{
    internal class OwinCommunicationListener : ICommunicationListener
    {
        private readonly ServiceEventSource eventSource;
        private readonly Action<IAppBuilder> startup;
        private readonly ServiceContext serviceContext;
        private readonly string endpointName;
        private readonly string appRoot;

        private IDisposable webApp;
        private string publishAddress;
        private string listeningAddress;

        public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName)
            : this(startup, serviceContext, eventSource, endpointName, null)
        {
        }

        public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName, string appRoot)
        {
            if (startup == null)
            {
                throw new ArgumentNullException(nameof(startup));
            }

            if (serviceContext == null)
            {
                throw new ArgumentNullException(nameof(serviceContext));
            }

            if (endpointName == null)
            {
                throw new ArgumentNullException(nameof(endpointName));
            }

            if (eventSource == null)
            {
                throw new ArgumentNullException(nameof(eventSource));
            }

            this.startup = startup;
            this.serviceContext = serviceContext;
            this.endpointName = endpointName;
            this.eventSource = eventSource;
            this.appRoot = appRoot;
        }

        public Task<string> OpenAsync(CancellationToken cancellationToken)
        {
            var serviceEndpoint = this.serviceContext.CodePackageActivationContext.GetEndpoint(this.endpointName);
            var protocol = serviceEndpoint.Protocol;
            int port = serviceEndpoint.Port;

            if (this.serviceContext is StatefulServiceContext)
            {
                StatefulServiceContext statefulServiceContext = this.serviceContext as StatefulServiceContext;

                this.listeningAddress = string.Format(
                    CultureInfo.InvariantCulture,
                    "{0}://+:{1}/{2}{3}/{4}/{5}",
                    protocol,
                    port,
                    string.IsNullOrWhiteSpace(this.appRoot)
                        ? string.Empty
                        : this.appRoot.TrimEnd('/') + '/',
                    statefulServiceContext.PartitionId,
                    statefulServiceContext.ReplicaId,
                    Guid.NewGuid());
            }
            else if (this.serviceContext is StatelessServiceContext)
            {
                this.listeningAddress = string.Format(
                    CultureInfo.InvariantCulture,
                    "{0}://+:{1}/{2}",
                    protocol,
                    port,
                    string.IsNullOrWhiteSpace(this.appRoot)
                        ? string.Empty
                        : this.appRoot.TrimEnd('/') + '/');
            }
            else
            {
                throw new InvalidOperationException();
            }

            this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

            try
            {
                this.eventSource.Message("Starting web server on " + this.listeningAddress);

                this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

                this.eventSource.Message("Listening on " + this.publishAddress);

                return Task.FromResult(this.publishAddress);
            }
            catch (Exception ex)
            {
                this.eventSource.Message("Web server failed tooopen endpoint {0}. {1}", this.endpointName, ex.ToString());

                this.StopWebServer();

                throw;
            }
        }

        public Task CloseAsync(CancellationToken cancellationToken)
        {
            this.eventSource.Message("Closing web server on endpoint {0}", this.endpointName);

            this.StopWebServer();

            return Task.FromResult(true);
        }

        public void Abort()
        {
            this.eventSource.Message("Aborting web server on endpoint {0}", this.endpointName);

            this.StopWebServer();
        }

        private void StopWebServer()
        {
            if (this.webApp != null)
            {
                try
                {
                    this.webApp.Dispose();
                }
                catch (ObjectDisposedException)
                {
                    // no-op
                }
            }
        }
    }
}
```

Agora que você colocou todas as partes da saudação em vigor, o projeto deve parecer com um aplicativo de API da Web típico com pontos de entrada da API de serviços confiável e um host OWIN.

## <a name="run-and-connect-through-a-web-browser"></a>Execução e conexão por meio de um navegador da Web
[Configure seu ambiente de desenvolvimento](service-fabric-get-started.md), caso ainda não tenha feito isso.

Agora você pode criar e implantar seu serviço. Pressione **F5** no Visual Studio toobuild e implantar o aplicativo hello. Na janela de eventos de diagnóstico hello, você verá uma mensagem que indica que o servidor web hello aberto em http://localhost:8281 /.

> [!NOTE]
> Se a porta de saudação já foi aberta por outro processo no seu computador, você verá um erro aqui. Isso indica que esse ouvinte Olá não pôde ser aberto. Se esse for o caso de Olá, tente usar uma porta diferente para a configuração de ponto de extremidade de saudação em ServiceManifest.xml.
> 
> 

Quando o serviço de saudação estiver em execução, abra um navegador e navegue muito[http://localhost:8281/api/valores](http://localhost:8281/api/values) tootest-lo.

## <a name="scale-it-out"></a>Escalar horizontalmente
Dimensionar aplicativos web sem monitoração de estado geralmente significa adicionando mais máquinas e girando Olá web apps neles. Mecanismo de orquestração do Service Fabric pode fazer isso para você sempre que novos nós forem adicionados tooa cluster. Quando você cria instâncias de um serviço sem monitoração de estado, você pode especificar o número de saudação de instâncias que você deseja toocreate. Malha do serviço coloca esse número de instâncias em nós de cluster de saudação. E torna-se de que não toocreate mais de uma instância em qualquer nó. Você também pode instruir tooalways Service Fabric cria uma instância em todos os nós especificando **-1** para contagem de instâncias de saudação. Isso garante que sempre que você adicionar nós tooscale-out do seu cluster, uma instância do serviço sem monitoração de estado será criada em novos nós de saudação. Esse valor é uma propriedade de instância de serviço hello, para que ele é definido quando você cria uma instância de serviço. Você pode fazer isso usando o PowerShell:

```powershell

New-ServiceFabricService -ApplicationName "fabric:/WebServiceApplication" -ServiceName "fabric:/WebServiceApplication/WebService" -ServiceTypeName "WebServiceType" -Stateless -PartitionSchemeSingleton -InstanceCount -1

```

Ou ao definir um serviço padrão em um projeto de serviço sem estado do Visual Studio:

```xml

<DefaultServices>
  <Service Name="WebService">
    <StatelessService ServiceTypeName="WebServiceType" InstanceCount="-1">
      <SingletonPartition />
    </StatelessService>
  </Service>
</DefaultServices>

```

Para obter mais informações sobre como o aplicativo toocreate e instâncias de serviço, consulte [implantar um aplicativo](service-fabric-deploy-remove-applications.md).

## <a name="next-steps"></a>Próximas etapas
[Depurar seu aplicativo do Service Fabric usando o Visual Studio](service-fabric-debugging-your-application.md)

