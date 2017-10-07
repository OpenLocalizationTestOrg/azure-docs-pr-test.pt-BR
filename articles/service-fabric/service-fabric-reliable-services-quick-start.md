---
title: "aaaCreate seu primeiro aplicativo de malha do serviço em c# | Microsoft Docs"
description: "Introdução toocreating um aplicativo do Microsoft Azure Service Fabric com serviços com e sem monitoração de estado."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d9b44d75-e905-468e-b867-2190ce97379a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/06/2017
ms.author: vturecek
ms.openlocfilehash: e95e67cc84be1b83c936b250cae9112ddc77b963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-reliable-services"></a>Introdução aos Reliable Services
> [!div class="op_single_selector"]
> * [C# em Windows](service-fabric-reliable-services-quick-start.md)
> * [Java no Linux](service-fabric-reliable-services-quick-start-java.md)
> 
> 

Um aplicativo do Service Fabric do Azure contém um ou mais serviços que executam seu código. Este guia mostra como toocreate com e sem monitoração aplicativos do Service Fabric com [serviços confiáveis](service-fabric-reliable-services-introduction.md).  Este vídeo Microsoft Virtual Academy também mostra como toocreate um serviço confiável sem monitoração de estado:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=s39AO76yC_7206218965">  
<img src="./media/service-fabric-reliable-services-quick-start/ReliableServicesVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="basic-concepts"></a>Conceitos básicos
tooget iniciado com serviços confiáveis, você só precisa toounderstand alguns conceitos básicos:

* **Tipo de serviço**: esta é sua implementação de serviço. Ele é definido pela classe Olá gravar que estende `StatelessService` e qualquer outro código ou dependências usadas neste documento, juntamente com um nome e um número de versão.
* **Serviço de instância nomeada**: toorun seu serviço, você cria instâncias nomeadas do seu tipo de serviço, bem como criar instâncias de objeto de um tipo de classe. Uma instância de serviço tem um nome na forma de saudação de um URI usando hello "fabric: /" esquema, como "fabric: / MyApp/MyService".
* **Host de serviço**: Olá denominado instâncias de serviço que você criar necessidade toorun dentro de um processo de host. host de serviço Olá é apenas um processo em que as instâncias do serviço podem executar.
* **Registro de serviço**: o registro reúne tudo. Olá service type deve ser registrado com hello Service Fabric em tempo de execução em um serviço de hospedar instâncias de toocreate Service Fabric tooallow-toorun.  

## <a name="create-a-stateless-service"></a>Criar um serviço sem estado
Um serviço sem monitoração de estado é um tipo de serviço que está sendo norma Olá em aplicativos de nuvem. Ele é considerado sem monitoração de estado como serviço Olá em si não contêm dados que precisa toobe armazenadas de forma confiável ou altamente disponível. Se uma instância de um serviço sem estado for desligada, todo seu estado interno será perdido. Esse tipo de serviço, o estado deve ser repositório externo tooan persistente, como tabelas do Azure ou um banco de dados SQL, para que ele toobe feitas confiável e altamente disponível.

Inicie o Visual Studio 2015 ou 2017 como administrador e crie um novo projeto de aplicativo do Service Fabric chamado *HelloWorld*:

![Use Olá novo projeto caixa de diálogo caixa toocreate um novo aplicativo de serviço de malha](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject.png)

Em seguida, crie um projeto de serviço sem estado chamado *HelloWorldStateless*:

![Na segunda caixa de diálogo hello, criar um projeto de serviço sem monitoração de estado](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject2.png)

Agora, sua solução contém dois projetos:

* *HelloWorld*. Isso é hello *aplicativo* projeto que contém o *serviços*. Ele também contém o manifesto do aplicativo hello que descreve o aplicativo hello, bem como um número de scripts do PowerShell que ajudam você a toodeploy seu aplicativo.
* *HelloWorldStateless*. Esse é o projeto de serviço de saudação. Ele contém a implementação de serviço sem monitoração de estado de saudação.

## <a name="implement-hello-service"></a>Implementar o serviço de saudação
Olá abrir **HelloWorldStateless.cs** arquivo no projeto de serviço de saudação. No Service Fabric, um serviço pode executar qualquer lógica de negócios. API do serviço de saudação oferece dois pontos de entrada para o seu código:

* Um método de ponto de entrada em aberto chamado *RunAsync*, em que você pode começar a executar qualquer carga de trabalho, incluindo cargas de trabalho de computação de longa duração.

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    ...
}
```

* Um ponto de entrada de comunicação em que você pode conectar a pilha de comunicação de sua escolha como o ASP.NET Core. É onde você pode começar a receber solicitações de usuários e outros serviços.

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}
```

Neste tutorial, vamos nos concentrar em Olá `RunAsync()` método de ponto de entrada. É aqui que você pode começar imediatamente a executar seu código.
modelo de projeto de saudação inclui um exemplo da implementação de `RunAsync()` que incrementa uma contagem sem interrupção.

> [!NOTE]
> Para obter detalhes sobre como toowork com uma comunicação de pilha, consulte [serviços de API da Web do serviço do Fabric com auto-hospedagem OWIN](service-fabric-reliable-services-communication-webapi.md)
> 
> 

### <a name="runasync"></a>RunAsync
```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace hello following sample code with your own logic
    //       or remove this RunAsync override if it's not needed in your service.

    long iterations = 0;

    while (true)
    {
        cancellationToken.ThrowIfCancellationRequested();

        ServiceEventSource.Current.ServiceMessage(this, "Working-{0}", ++iterations);

        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
}
```

plataforma de saudação chama este método quando uma instância de um serviço é tooexecute inserida e pronto. Para um serviço sem monitoração de estado, que simplesmente significa que quando a instância do serviço de saudação é aberta. Um token de cancelamento é fornecido toocoordinate quando toobe fechado as necessidades de sua instância de serviço. Na malha do serviço, esse ciclo de abertura/fechamento de uma instância de serviço pode ocorrer muitas vezes em tempo de vida de saudação do serviço hello como um todo. Isso pode ocorrer por vários motivos, incluindo:

* sistema de saudação move suas instâncias de serviço de balanceamento de recursos.
* Ocorrem falhas no código.
* aplicativo Hello ou o sistema é atualizado.
* hardware subjacente Olá sofrer uma interrupção.

Essa orquestração é gerenciada pelo Olá sistema tookeep seu serviço altamente disponível e adequadamente equilibrado.

`RunAsync()` não deve bloquear sincronicamente. Sua implementação de RunAsync deve retornar uma tarefa ou await em qualquer toocontinue de tempo de execução operações demoradas ou bloqueio tooallow hello. Observe que, no hello `while(true)` loop no exemplo anterior de saudação, retornando uma tarefa `await Task.Delay()` é usado. Se sua carga de trabalho deve bloquear sincronicamente, agende uma nova tarefa com `Task.Run()` na sua implementação `RunAsync`.

O cancelamento da sua carga de trabalho é um esforço cooperativo orquestrado pelo Olá fornecido um token de cancelamento. sistema Olá aguardará para sua tarefa tooend (pela conclusão bem-sucedida, cancelamento ou falha) antes de ele prossegue. É importante toohonor Olá cancelamento token, concluir qualquer trabalho e sair `RunAsync()` assim que possível quando o sistema Olá solicitações de cancelamento.

Neste exemplo de serviço sem monitoração de estado, a contagem de saudação é armazenada em uma variável local. Mas porque este é um serviço sem monitoração de estado, valor Olá armazenado existe somente para Olá atual do ciclo de vida da sua instância de serviço. Quando o serviço Olá move ou reinicia, o valor de saudação é perdido.

## <a name="create-a-stateful-service"></a>Criar um serviço com estado
O Service Fabric introduz um novo tipo de serviço que é com estado. Um serviço com monitoração de estado pode manter o estado confiável no serviço de saudação em si, colocalizado com o código de saudação que ele está em uso. Estado é feito altamente disponível pela malha do serviço sem Olá necessidade toopersist estado tooan repositório de externo.

tooconvert um valor do contador de toohighly sem monitoração de estado persistente e disponível, mesmo quando o serviço de saudação move ou for reiniciado, você precisa um serviço com monitoração de estado.

Em Olá mesmo *HelloWorld* aplicativo, você pode adicionar um novo serviço clicando nas referências de serviços Olá no projeto de aplicativo hello e selecionando **Adicionar -> novo serviço do Service Fabric**.

![Adicionar um serviço tooyour aplicativo do Service Fabric](media/service-fabric-reliable-services-quick-start/hello-stateful-NewService.png)

Selecione **Serviço com Estado** e dê o nome de *HelloWorldStateful*. Clique em **OK**.

![Usar toocreate de caixa de diálogo do hello novo projeto um novo serviço de monitoração de estado do Service Fabric](media/service-fabric-reliable-services-quick-start/hello-stateful-NewProject.png)

Seu aplicativo agora deve ter dois serviços: Olá serviço sem monitoração de estado *HelloWorldStateless* e o serviço com monitoração de estado Olá *HelloWorldStateful*.

Um serviço com monitoração de estado tem Olá mesmo pontos de entrada como um serviço sem monitoração de estado. Olá principal diferença é a disponibilidade de saudação de um *provedor de estado* que pode armazenar o estado confiável. Service Fabric vem com uma implementação de provedor de estado chamada [coleções confiável](service-fabric-reliable-services-reliable-collections.md), que permite que você crie estruturas de dados replicados por meio de saudação Gerenciador de estado confiável. Por padrão, um serviço confiável com estado usa esse provedor de estado.

Abra **HelloWorldStateful.cs** na *HelloWorldStateful*, que contém a saudação RunAsync método a seguir:

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace hello following sample code with your own logic
    //       or remove this RunAsync override if it's not needed in your service.

    var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");

    while (true)
    {
        cancellationToken.ThrowIfCancellationRequested();

        using (var tx = this.StateManager.CreateTransaction())
        {
            var result = await myDictionary.TryGetValueAsync(tx, "Counter");

            ServiceEventSource.Current.ServiceMessage(this, "Current Counter Value: {0}",
                result.HasValue ? result.Value.ToString() : "Value does not exist.");

            await myDictionary.AddOrUpdateAsync(tx, "Counter", 0, (key, value) => ++value);

            // If an exception is thrown before calling CommitAsync, hello transaction aborts, all changes are
            // discarded, and nothing is saved toohello secondary replicas.
            await tx.CommitAsync();
        }

        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
```

### <a name="runasync"></a>RunAsync
`RunAsync()` opera da mesma forma em serviços com e sem estado. No entanto, em um serviço com monitoração de estado, plataforma Olá executa trabalho adicional em seu nome antes de executar `RunAsync()`. Esse trabalho pode incluir garantindo que o Gerenciador de estado confiável hello e coleções confiável são toouse pronto.

### <a name="reliable-collections-and-hello-reliable-state-manager"></a>Coleções e Olá confiável Gerenciador de estado confiável
```csharp
var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
```

[IReliableDictionary](https://msdn.microsoft.com/library/dn971511.aspx) é uma implementação de dicionário que você pode usar tooreliably o estado do repositório no serviço de saudação. Com o Service Fabric e coleções confiável, você pode armazenar dados diretamente em seu serviço sem necessidade de saudação de um repositório persistente externo. As Coleções Confiáveis tornam os dados altamente disponíveis. O Service Fabric consegue isso criando e gerenciando várias *réplicas* do seu serviço para você. Ele também fornece uma API que abstrai complexidades Olá longe de gerenciar suas transições de estado e as réplicas.

As Reliable Collections podem armazenar qualquer tipo .NET, incluindo tipos personalizados, com algumas limitações:

* Service Fabric torna seu estado altamente disponível pelo *replicando* disco toolocal de dados de armazenamento de estado entre nós e coleções confiável em cada réplica. Isso significa que tudo o que é armazenado nas Coleções Confiáveis deve ser *serializável*. Por padrão, use coleções confiável [DataContract](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractattribute%28v=vs.110%29.aspx) para serialização, portanto, é importante toomake-se de que seus tipos são [Olá serializador de contrato de dados com suporte](https://msdn.microsoft.com/library/ms731923%28v=vs.110%29.aspx) quando você usa o padrão de saudação serializador.
* Os objetos são replicados para alta disponibilidade quando você confirma uma transação nas Reliable Collections. Objetos armazenados nas Reliable Collections são mantidos na memória local do serviço. Isso significa que você tenha um objeto de toohello referência local.
  
   É importante que você não modificar as instâncias locais desses objetos sem executar uma operação de atualização na coleção de saudação confiável em uma transação. Isso ocorre porque as alterações toolocal instâncias de objetos não serão replicadas automaticamente. Você deve inserir novamente o objeto de saudação no dicionário de saudação ou usar uma saudação *atualizar* métodos no dicionário de saudação.

Gerenciador de estado confiável de saudação gerencia coleções confiável para você. Você pode simplesmente pedir Olá confiável Gerenciador de estado para um conjunto confiável por nome a qualquer momento e em qualquer lugar em seu serviço. Olá Gerenciador de estado confiável garante que você obtenha uma referência de volta. Não recomendamos salvar referências tooreliable instâncias de coleção em variáveis de membro de classe ou propriedades. Deve ter especial cuidado tooensure Olá referência é definida em todos os momentos tooan instância Olá ciclo de vida do serviço. Olá Gerenciador de estado confiável trata esse trabalho para você, e é otimizado para visitas a repetição.

### <a name="transactional-and-asynchronous-operations"></a>Operações transacionais e assíncronas
```C#
using (ITransaction tx = this.StateManager.CreateTransaction())
{
    var result = await myDictionary.TryGetValueAsync(tx, "Counter-1");

    await myDictionary.AddOrUpdateAsync(tx, "Counter-1", 0, (k, v) => ++v);

    await tx.CommitAsync();
}
```

Coleções confiáveis têm muitos Olá mesmas operações que seus `System.Collections.Generic` e `System.Collections.Concurrent` equivalentes, exceto LINQ. As operações nas Coleções Confiáveis são assíncronas. Isso ocorre porque as operações de gravação com coleções confiável executam tooreplicate de operações de e/s e manter dados toodisk.

As operações de Coleção Confiável são *transacionais*, de modo que você pode manter o estado consistente entre várias Coleções Confiáveis e operações. Por exemplo, você pode remover da fila um item de trabalho de uma fila confiável, executar uma operação sobre ele e salvar o resultado de saudação em um dicionário confiável, tudo em uma única transação. Isso é tratado como uma operação atômica, e garante que toda a operação Olá terá êxito ou saudação de toda a operação será revertida. Se ocorrer um erro após a remoção da fila item hello, mas antes de salvar o resultado de hello, transação inteira Olá é revertida e item Olá permanece na fila de saudação para processamento.

## <a name="run-hello-application"></a>Executar o aplicativo hello
Agora retornamos toohello *HelloWorld* aplicativo. Agora você pode criar e implantar seus serviços. Quando você pressiona **F5**, seu aplicativo estará cluster local tooyour construído e implantado.

Depois de iniciar a execução de serviços hello, você pode exibir hello gerado eventos de rastreamento de eventos para Windows (ETW) em um **eventos de diagnóstico** janela. Observe que os eventos de saudação exibidos são de serviço sem monitoração de estado hello e o serviço de monitoração de estado Olá no aplicativo hello. Você pode pausar Fluxo Olá clicando Olá **pausar** botão. Você pode examinar os detalhes de saudação de uma mensagem expandindo essa mensagem.

> [!NOTE]
> Antes de executar o aplicativo hello, certifique-se de que você tenha um cluster de desenvolvimento local em execução. Check-out Olá [guia de Introdução](service-fabric-get-started.md) para obter informações sobre como configurar seu ambiente local.
> 
> 

![Exibir Eventos de Diagnóstico no Visual Studio](media/service-fabric-reliable-services-quick-start/hello-stateful-Output.png)

## <a name="next-steps"></a>Próximas etapas
[Depurar seu aplicativo do Service Fabric usando o Visual Studio](service-fabric-debugging-your-application.md)

[Introdução aos serviços de API Web do Service Fabric com auto-hospedagem OWIN](service-fabric-reliable-services-communication-webapi.md)

[Saiba mais sobre as Reliable Collections](service-fabric-reliable-services-reliable-collections.md)

[Implantar um aplicativo](service-fabric-deploy-remove-applications.md)

[Atualização de aplicativo](service-fabric-application-upgrade.md)

[Referência do desenvolvedor para Reliable Services](https://msdn.microsoft.com/library/azure/dn706529.aspx)

