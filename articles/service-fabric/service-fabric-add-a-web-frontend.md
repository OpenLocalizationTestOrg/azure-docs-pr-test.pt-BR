---
title: aaaCreate um front-end da web para seu aplicativo do Azure Service Fabric usando o ASP.NET Core | Microsoft Docs
description: "Expor web Service Fabric application toohello por meio de um projeto do ASP.NET Core e comunicação entre serviços por meio de comunicação remota do serviço."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: vturecek
ms.openlocfilehash: 0c4454d6cac4c2e343bd6e93e56d3d2f0ebfc4ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-web-service-front-end-for-your-application-using-aspnet-core"></a>Compilar um serviço Web front-end para seu aplicativo usando ASP.NET Core
Por padrão, os serviços do Azure Service Fabric não fornecem uma web toohello de interface pública. tooexpose clientes de tooHTTP de funcionalidade do aplicativo, você tem toocreate web tooact como um ponto de entrada do projeto e comunicar-se de tooyour há serviços individuais.

Neste tutorial, podemos escolher onde é deixada no hello [criando seu primeiro aplicativo no Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md) tutorial e adicionar um serviço da web ASP.NET Core na frente do serviço de monitoração de estado do contador hello. Se ainda não tiver feito isso, volte e percorra esse tutorial primeiro.

## <a name="set-up-your-environment-for-aspnet-core"></a>Configurar o ambiente para o ASP.NET Core

É necessário o Visual Studio de 2017 toofollow junto com este tutorial. Qualquer edição será suficiente. 

 - [Instalar o Visual Studio 2017](https://www.visualstudio.com/)

aplicativos do ASP.NET Core Service Fabric toodevelop, você deve ter Olá instaladas de cargas de trabalho a seguir:
 - **Desenvolvimento do Azure** (em *Web e Nuvem*)
 - **Desenvolvimento do ASP.NET e para a Web** (em *Web e Nuvem*)
 - **Desenvolvimento de plataforma cruzada do .NET Core** (em *Outros Conjuntos de Ferramentas*)

>[!Note] 
>Olá ferramentas .NET Core para Visual Studio 2015 não serão mais sendo atualizadas, no entanto, se você ainda estiver usando o Visual Studio 2015, você precisa toohave [.NET Core VS 2015 Tooling Preview 2](https://www.microsoft.com/net/download/core) instalado.

## <a name="add-an-aspnet-core-service-tooyour-application"></a>Adicionar um aplicativo do ASP.NET Core serviço tooyour
ASP.NET Core é uma estrutura de desenvolvimento de web leve e várias plataformas, você pode usar a interface da web modernos toocreate e APIs da web. 

Vamos adicionar um aplicativo do ASP.NET Web API projeto tooour existente.

1. No Gerenciador de soluções, clique com botão direito **serviços** dentro Olá projeto de aplicativo e escolha **Adicionar > novo serviço do Service Fabric**.
   
    ![Adicionando um novo aplicativo de serviço tooan existente][vs-add-new-service]
2. Em Olá **criar um serviço** escolha **ASP.NET Core** e dê a ele um nome.
   
    ![Escolhendo um serviço web ASP.NET na caixa de diálogo Olá de novo serviço][vs-new-service-dialog]

3. próxima página de saudação fornece um conjunto de ASP.NET Core modelos de projeto. Observe que esses são Olá mesmo opções que você veria se você criou um projeto do ASP.NET Core fora de um aplicativo de malha do serviço, com uma pequena quantidade de código adicional tooregister Olá serviço com tempo de execução do Service Fabric hello. Neste tutorial, escolhemos **API Web**. No entanto, você pode aplicar Olá mesmo conceitos toobuilding um aplicativo web completo.
   
    ![Escolhendo o tipo de projeto do ASP.NET][vs-new-aspnet-project-dialog]
   
    Depois de criar o projeto de API Web, você deverá ter dois serviços no aplicativo. Enquanto você continua toobuild seu aplicativo, você pode adicionar mais serviços em exatamente Olá mesma maneira. Cada um pode seu próprio controle de versão e ser atualizado de forma independente.

## <a name="run-hello-application"></a>Executar o aplicativo hello
tooget uma ideia do que já fizemos, vamos implantar Olá novo aplicativo e execute uma olhada no comportamento padrão Olá Olá modelo de API da Web do ASP.NET Core fornece.

1. Pressione F5 no Visual Studio toodebug Olá aplicativo.
2. Quando a implantação for concluída, o Visual Studio inicia raiz de toohello um navegador de saudação serviço de API da Web ASP.NET. modelo de API da Web do ASP.NET Core Olá não fornece o comportamento padrão raiz Olá, então você deve ver um erro 404 no navegador de saudação.
3. Adicionar `/api/values` toohello local no navegador de saudação. Isso chama Olá `Get` método hello ValuesController no modelo de API da Web hello. Ele retorna a resposta padrão Olá fornecida pelo modelo hello – uma matriz JSON que contém duas cadeias de caracteres:
   
    ![Valores padrão retornados do modelo de API Web do ASP.NET Core][browser-aspnet-template-values]
   
    Por fim de saudação do tutorial do hello, essa página mostrará valor mais recente do contador de saudação de nosso serviço com monitoração de estado, em vez de saudação cadeias de caracteres padrão.

## <a name="connect-hello-services"></a>Conectar os serviços de saudação
O Service Fabric fornece total flexibilidade na comunicação com Reliable Services. Em um único aplicativo, você pode ter serviços acessíveis por meio de TCP, outros serviços acessíveis por meio de uma API REST HTTP e ainda outros serviços que são acessíveis por meio de soquetes da Web. Para obter informações sobre opções de saudação disponíveis e compensações de saudação envolvidas, consulte [se comunicar com serviços](service-fabric-connect-and-communicate-with-services.md). Neste tutorial, usamos [serviço de comunicação remota do serviço de malha](service-fabric-reliable-services-communication-remoting.md), fornecido no hello SDK.

Olá abordagem de comunicação remota do serviço (modelada em chamadas de procedimento remoto ou RPCs), você definirá uma interface tooact como contrato público de Olá para o serviço de saudação. Em seguida, você deve usar toogenerate essa interface uma classe proxy para interagir com o serviço de saudação.

### <a name="create-hello-remoting-interface"></a>Criar interface de comunicação remota Olá
Vamos começar criando Olá interface tooact como Olá contrato entre o serviço com monitoração de estado hello e outros serviços nesse caso Olá projeto da web de ASP.NET Core. Esta interface deve ser compartilhada por todos os serviços que usam as chamadas RPC toomake, portanto, criaremos em seu próprio projeto de biblioteca de classes.

1. No Gerenciador de Soluções, clique com o botão direito do mouse na solução e escolha **Adicione** > **Novo Projeto**.

2. Escolha Olá **Visual C#** entrada hello esquerda do painel de navegação e, em seguida, selecione Olá **biblioteca de classes** modelo. Certifique-se de que essa versão do .NET Framework hello está definido muito**4.5.2**.
   
    ![Criando um projeto de interface para o serviço com estado][vs-add-class-library-project]

3. Instalar Olá **Microsoft.ServiceFabric.Services.Remoting** pacote NuGet. Procurar **Microsoft.ServiceFabric.Services.Remoting** em Olá NuGet Gerenciador de pacote e instalá-lo para todos os projetos na solução de saudação que usam a comunicação remota do serviço, incluindo:
   - projeto de biblioteca de classes Olá que contém a interface do serviço Olá
   - projeto de serviço de monitoração de estado de saudação
   - Olá projeto de serviço web ASP.NET Core
   
    ![Adicionar o pacote do NuGet serviços Olá][vs-services-nuget-package]

4. Na biblioteca de classes do hello, criar uma interface com um único método, `GetCountAsync`, e estender a interface de saudação do `Microsoft.ServiceFabric.Services.Remoting.IService`. interface de comunicação remota Olá deve derivar de tooindicate essa interface que é uma interface de comunicação remota do serviço.
   
    ```c#
    using Microsoft.ServiceFabric.Services.Remoting;
    using System.Threading.Tasks;
        
    ...

    namespace MyStatefulService.Interface
    {
        public interface ICounter: IService
        {
            Task<long> GetCountAsync();
        }
    }
    ```

### <a name="implement-hello-interface-in-your-stateful-service"></a>Implementar interface Olá em seu serviço com monitoração de estado
Agora que definimos interface Olá, é necessário tooimplement-lo no serviço com monitoração de estado hello.

1. Em seu serviço com monitoração de estado, adicione um projeto de biblioteca de classe toohello de referência que contém a interface hello.
   
    ![Adicionando um projeto de biblioteca de classes de toohello de referência no serviço com monitoração de estado Olá][vs-add-class-library-reference]
2. Localize Olá classe que herda de `StatefulService`, como `MyStatefulService`e estendê-lo Olá tooimplement `ICounter` interface.
   
    ```c#
    using MyStatefulService.Interface;
   
    ...
   
    public class MyStatefulService : StatefulService, ICounter
    {        
         ...
    }
    ```
3. Agora implementar Olá único método que é definido em Olá `ICounter` interface `GetCountAsync`.
   
    ```c#
    public async Task<long> GetCountAsync()
    {
        var myDictionary = 
            await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
   
        using (var tx = this.StateManager.CreateTransaction())
        {          
            var result = await myDictionary.TryGetValueAsync(tx, "Counter");
            return result.HasValue ? result.Value : 0;
        }
    }
    ```

### <a name="expose-hello-stateful-service-using-a-service-remoting-listener"></a>Expor Olá serviço com monitoração de estado usando um ouvinte de comunicação remota do serviço
Com hello `ICounter` interface implementada, a etapa final Olá é o canal de comunicação tooopen Olá comunicação remota do serviço. Para serviços com estado, o Service Fabric fornece um método substituível chamado `CreateServiceReplicaListeners`. Com esse método, você pode especificar um ou mais ouvintes de comunicação, com base no tipo de saudação de comunicação que você deseja tooenable para seu serviço.

> [!NOTE]
> método equivalente Hello para abertura de um serviço de toostateless de canal de comunicação é chamado `CreateServiceInstanceListeners`.

Nesse caso, podemos substituir Olá `CreateServiceReplicaListeners` método e fornecer uma instância de `ServiceRemotingListener`, que cria um ponto de extremidade RPC que é chamado de clientes por meio de `ServiceProxy`.  

Olá `CreateServiceRemotingListener` método de extensão no hello `IService` interface permite que você tooeasily criar um `ServiceRemotingListener` com todas as configurações padrão. toouse esse método de extensão, certifique-se de ter Olá `Microsoft.ServiceFabric.Services.Remoting.Runtime` namespace importado. 

```c#
using Microsoft.ServiceFabric.Services.Remoting.Runtime;

...

protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new List<ServiceReplicaListener>()
    {
        new ServiceReplicaListener(
            (context) =>
                this.CreateServiceRemotingListener(context))
    };
}
```


### <a name="use-hello-serviceproxy-class-toointeract-with-hello-service"></a>Use Olá ServiceProxy classe toointeract com o serviço de saudação
Nosso serviço com monitoração de estado está agora pronto tooreceive tráfego de outros serviços RPC. Portanto tudo o que permanece é adicionando Olá código toocommunicate com ele da saudação serviço web ASP.NET.

1. No seu projeto do ASP.NET, adicionar uma biblioteca de classes de toohello de referência que contém Olá `ICounter` interface.

2. Anteriormente você adicionou Olá **Microsoft.ServiceFabric.Services.Remoting** NuGet pacote toohello ASP.NET projeto. Esse pacote fornece Olá `ServiceProxy` classe que você use toomake RPC chama o serviço de monitoração de estado de toohello. Certifique-se de que instalar o pacote de NuGet em Olá projeto de serviço web ASP.NET Core.

4. Em Olá **controladores** pasta, abra Olá `ValuesController` classe. Observe que Olá `Get` método atualmente apenas retorna uma matriz de cadeia de caracteres codificada de "value1" e "value2" – que coincide com o que vimos anteriormente no navegador de saudação. Substitua esta implementação Olá código a seguir:
   
    ```c#
    using MyStatefulService.Interface;
    using Microsoft.ServiceFabric.Services.Client;
    using Microsoft.ServiceFabric.Services.Remoting.Client;
   
    ...

    [HttpGet]
    public async Task<IEnumerable<string>> Get()
    {
        ICounter counter =
            ServiceProxy.Create<ICounter>(new Uri("fabric:/MyApplication/MyStatefulService"), new ServicePartitionKey(0));
   
        long count = await counter.GetCountAsync();
   
        return new string[] { count.ToString() };
    }
    ```
   
    Olá primeira linha de código é chave Olá um. toocreate Olá ICounter serviço proxy de toohello com monitoração de estado, você precisa tooprovide duas informações: um nome de identificação e hello de partição do serviço de saudação.
   
    Você pode usar serviços com monitoração de estado do particionamento tooscale dividindo seu estado em diferentes segmentos, com base em uma chave que você define, como uma ID de cliente ou código postal. Em nosso aplicativo trivial, serviço com monitoração de estado Olá tem apenas uma partição, portanto chave Olá não importa. Qualquer chave que você fornecer levará toohello mesma partição. toolearn mais sobre o particionamento de serviços, consulte [como toopartition serviços confiável do serviço do Fabric](service-fabric-concepts-partitioning.md).
   
    nome do serviço Olá é um URI de malha de formulário Olá: /&lt;application_name&gt;/&lt;service_name&gt;.
   
    Com esses dois tipos de informações, o Service Fabric pode identificar exclusivamente máquina Olá que solicitações devem ser enviadas para. Olá `ServiceProxy` classe também perfeitamente manipula caso Olá onde Olá máquina que hospeda a partição de serviço com monitoração de estado de saudação falhar e outra máquina deve ser promovido tootake seu lugar. Essa abstração torna a gravação Olá toodeal de código de cliente com outros serviços muito mais simples.
   
    Assim que tivermos proxy Olá, podemos simplesmente chamar Olá `GetCountAsync` método e retorna seu resultado.

5. Pressione F5 novamente toorun Olá modificou o aplicativo. Como antes, o Visual Studio automaticamente inicia raiz de toohello de navegador de saudação do projeto da web de saudação. Adicionar caminho de "api/valores" Olá, e você verá o valor de contador atual Olá retornado.
   
    ![valor do contador com monitoração de estado de saudação exibida no navegador Olá][browser-aspnet-counter-value]
   
    Atualize o navegador de saudação periodicamente toosee Olá contador valor atualização.

## <a name="kestrel-and-weblistener"></a>Kestrel e WebListener

Olá padrão ASP.NET web server Core, conhecido como Kestrel, for [atualmente não há suporte para o tratamento do tráfego de internet direto](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel). Como resultado, hello modelo de serviço sem monitoração de estado do ASP.NET Core para Service Fabric usa [WebListener](https://docs.microsoft.com/aspnet/core/fundamentals/servers/weblistener) por padrão. 

toolearn mais sobre Kestrel e WebListener em serviços do Service Fabric, consulte muito[ASP.NET Core em serviços confiável do serviço do Fabric](service-fabric-reliable-services-communication-aspnetcore.md).

## <a name="connecting-tooa-reliable-actor-service"></a>Conectar-se o serviço de Reliable Actor tooa
Este tutorial se concentra em adicionar um front-end da Web que se comunique com um serviço com estado. No entanto, você pode seguir um tooactors de tootalk modelo muito semelhantes. Quando você cria um projeto do Reliable Actor, o Visual Studio gera automaticamente um projeto de interface para você. Você pode usar esse toogenerate interface um proxy de ator em Olá web projeto toocommunicate com ator hello. o canal de comunicação Olá é fornecido automaticamente. Portanto, você não precisa toodo qualquer coisa que é equivalente tooestablishing um `ServiceRemotingListener` como você fez para o serviço com monitoração de estado Olá neste tutorial.

## <a name="how-web-services-work-on-your-local-cluster"></a>Como os serviços Web funcionam no cluster local
Em geral, você pode implantar exatamente Olá mesmo do Service Fabric application tooa com vários computadores de cluster que você implantou no cluster local e estar altamente seguro de que ele funciona conforme o esperado. Isso ocorre porque o cluster local é simplesmente uma configuração de cinco nós que é recolhida tooa único computador.

No entanto, quando se trata de tooweb serviços, há um nuance chave. Quando o cluster fica atrás de um balanceador de carga, como faz no Azure, você deve garantir que os serviços web são implantados em todos os computadores desde o balanceador de carga Olá simplesmente alternadas tráfego entre máquinas hello. Você pode fazer isso definindo Olá `InstanceCount` para valor especial de toohello do serviço de saudação de "-1".

Por outro lado, quando você executa um serviço web localmente, você precisa tooensure que apenas uma instância do serviço de saudação está em execução. Caso contrário, execute em conflitos de vários processos que estão escutando Olá mesmo caminho e a porta. Como resultado, contagem de instâncias de serviço Olá web deve ser definida muito "1" para implantações de locais.

toolearn como valores diferentes de tooconfigure para outro ambiente, consulte [gerenciar parâmetros do aplicativo para vários ambientes](service-fabric-manage-multiple-environment-app-configuration.md).

## <a name="next-steps"></a>Próximas etapas
Agora que você tem um front-end da Web configurado para o aplicativo com o ASP.NET Core, saiba mais sobre o [ASP.NET Core nos Reliable Services do Service Fabric](service-fabric-reliable-services-communication-aspnetcore.md) para obter uma compreensão detalhada de como o ASP.NET Core funciona com o Service Fabric.

Em seguida, [saber mais sobre a comunicação com serviços](service-fabric-connect-and-communicate-with-services.md) em geral tooget a conclusão de imagem do serviço como a comunicação funciona na malha do serviço.

Depois de você ter um bom entendimento de como funciona a comunicação de serviço, [criar um cluster no Azure e implantar sua nuvem de toohello aplicativo](service-fabric-cluster-creation-via-portal.md).

<!-- Image References -->

[vs-add-new-service]: ./media/service-fabric-add-a-web-frontend/vs-add-new-service.png
[vs-new-service-dialog]: ./media/service-fabric-add-a-web-frontend/vs-new-service-dialog.png
[vs-new-aspnet-project-dialog]: ./media/service-fabric-add-a-web-frontend/vs-new-aspnet-project-dialog.png
[browser-aspnet-template-values]: ./media/service-fabric-add-a-web-frontend/browser-aspnet-template-values.png
[vs-add-class-library-project]: ./media/service-fabric-add-a-web-frontend/vs-add-class-library-project.png
[vs-add-class-library-reference]: ./media/service-fabric-add-a-web-frontend/vs-add-class-library-reference.png
[vs-services-nuget-package]: ./media/service-fabric-add-a-web-frontend/vs-services-nuget-package.png
[browser-aspnet-counter-value]: ./media/service-fabric-add-a-web-frontend/browser-aspnet-counter-value.png
[vs-create-platform]: ./media/service-fabric-add-a-web-frontend/vs-create-platform.png


<!-- external links -->
[dotnetcore-install]: https://www.microsoft.com/net/core#windows
