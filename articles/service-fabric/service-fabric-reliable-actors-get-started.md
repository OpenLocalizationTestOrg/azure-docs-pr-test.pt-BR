---
title: "aaaCreate sua primeira baseado em ator Azure microsserviço em c# | Microsoft Docs"
description: "Este tutorial orienta você pelas etapas de saudação de criar, depurar e implantar um serviço baseado em ator simples usando o serviço de malha Reliable Actors."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d4aebe72-1551-4062-b1eb-54d83297f139
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: ab4f75bef0adb6e70f0ead587475b3fb51e6e6a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-reliable-actors"></a>Introdução aos Reliable Actors
> [!div class="op_single_selector"]
> * [C# em Windows](service-fabric-reliable-actors-get-started.md)
> * [Java no Linux](service-fabric-reliable-actors-get-started-java.md)
> 
> 

Este artigo explica as Noções básicas de saudação do Azure Service Fabric Reliable Actors e orienta você por criar, depurar e implantar um aplicativo de Reliable Actor simples no Visual Studio.

## <a name="installation-and-setup"></a>Instalação e configuração
Antes de começar, certifique-se de que você tenha o ambiente de desenvolvimento do Service Fabric Olá configurado no seu computador.
Se você precisar tooset-lo, consulte as instruções detalhadas em [como tooset ambiente de desenvolvimento Olá](service-fabric-get-started.md).

## <a name="basic-concepts"></a>Conceitos básicos
tooget iniciado com atores confiável, você só precisa toounderstand alguns conceitos básicos:

* **Serviço do ator**. Confiáveis atores são empacotados em serviços confiáveis que podem ser implantados na infraestrutura de malha do serviço de saudação. As instâncias de ator são ativadas em uma instância de serviço nomeado.
* **Registro do ator**. Como com serviços confiáveis, um serviço de Reliable Actor deve toobe registrado com o tempo de execução do hello Service Fabric. Além disso, o tipo de ator Olá precisa toobe registrado com o tempo de execução do hello ator.
* **Interface do Ator**. interface de ator Olá é usado toodefine uma interface pública fortemente tipada de um ator. No hello terminologia do modelo confiável ator, interface de ator Olá define Olá tipos de mensagens que Olá ator podem entender e processar. interface de ator Olá é usado por outros atores e aplicativos cliente muito "enviam" (de forma assíncrona) ator de toohello de mensagens. Os Reliable Actors pode implantar várias interfaces.
* **Classe ActorProxy**. Olá ActorProxy classe é usada pelo cliente aplicativos tooinvoke Olá métodos expostos pela interface de ator hello. Olá ActorProxy classe fornece dois recursos importantes:
  
  * A resolução de nome: é toolocate capaz de ator de saudação em cluster hello (localizar o nó de saudação do cluster de saudação onde ele está hospedado).
  * Tratamento de falha: pode repetir invocações de método e resolver o local de ator Olá após novamente, por exemplo, uma falha que exija Olá ator toobe realocado tooanother nó no cluster hello.

Olá, seguindo as regras que pertencem a interfaces tooactor é vale a pena mencionar:

* Métodos da interface de ator não podem ser sobrecarregados.
* Métodos da interface de ator não podem ter parâmetros de saída, de referência e opcionais.
* Não há suporte para interfaces genéricas.

## <a name="create-a-new-project-in-visual-studio"></a>Criar um novo projeto no Visual Studio
Inicie o Visual Studio 2015 ou 2017 como administrador e crie um novo projeto de aplicativo do Service Fabric:

![Ferramentas do Service Fabric para Visual Studio – novo projeto][1]

Na próxima caixa de diálogo hello, você pode escolher o tipo de saudação do projeto que você deseja toocreate.

![Modelos de projeto do Service Fabric][5]

Para o projeto de HelloWorld Olá, vamos usar o serviço do Service Fabric Reliable Actors hello.

Depois que você criou a solução hello, você deve ver Olá estrutura a seguir:

![Estrutura de projeto do Service Fabric][2]

## <a name="reliable-actors-basic-building-blocks"></a>Blocos de construção básicos de Reliable Actors
Uma solução comum do Reliable Actors é composta por três projetos:

* **projeto de aplicativo Hello (MyActorApplication)**. Esse é o projeto de saudação que todos os serviços de saudação juntos para implantação de pacotes. Ele contém Olá *ApplicationManifest.xml* e scripts do PowerShell para gerenciar o aplicativo hello.
* **projeto de interface de saudação (MyActor.Interfaces)**. Esse é o projeto de saudação que contém a definição de interface de saudação de ator hello. No projeto de MyActor.Interfaces hello, você pode definir interfaces Olá que serão usados por atores Olá na solução de saudação. As interfaces de ator podem ser definidas em qualquer projeto com qualquer nome, mas interface Olá define o contrato de ator de saudação que é compartilhado por clientes de saudação chamando ator hello, então, geralmente faz sentido toodefine e implementação de ator Olá-lo em um assembly separar da implementação de ator hello e pode ser compartilhado por vários outros projetos.

```csharp
public interface IMyActor : IActor
{
    Task<string> HelloWorld();
}
```

* **projeto de serviço de ator Hello (MyActor)**. Isso é Olá projeto usado toodefine Olá Service Fabric serviço ator de saudação toohost contínuo. Ele contém a implementação de saudação de ator hello. Uma implementação de ator é uma classe que deriva do tipo base Olá `Actor` e implementa Olá interfaces que são definidos no projeto de MyActor.Interfaces hello. Uma classe de ator também deve implementar um construtor que aceite um `ActorService` instância e um `ActorId` e os passa toohello base `Actor` classe. Isso possibilita a injeção de dependência do construtor de dependências de plataforma.

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<string> HelloWorld()
    {
        return Task.FromResult("Hello world!");
    }
}
```

serviço de ator Olá deve ser registrado com um tipo de serviço em tempo de execução do Service Fabric hello. Em ordem para Olá toorun do serviço de ator suas instâncias de ator, seu tipo de ator também deve ser registrado com hello serviço de ator. Olá `ActorRuntime` método de registro executa essa tarefa para atores.

```csharp
internal static class Program
{
    private static void Main()
    {
        try
        {
            ActorRuntime.RegisterActorAsync<MyActor>(
                (context, actorType) => new ActorService(context, actorType, () => new MyActor())).GetAwaiter().GetResult();

            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ActorEventSource.Current.ActorHostInitializationFailed(e.ToString());
            throw;
        }
    }
}

```

Se você iniciar um novo projeto no Visual Studio e você tiver apenas uma definição de ator, registro de saudação é incluído por padrão no código de saudação que o Visual Studio gera. Se você definir outros atores no serviço Olá, você precisa de registro de ator Olá tooadd usando:

```csharp
 ActorRuntime.RegisterActorAsync<MyOtherActor>();

```

> [!TIP]
> Olá atores de malha do serviço de tempo de execução emite alguns [eventos e contadores de desempenho relacionam métodos tooactor](service-fabric-reliable-actors-diagnostics.md#actor-method-events-and-performance-counters). Eles são úteis para diagnóstico e monitoramento de desempenho.
> 
> 

## <a name="debugging"></a>Depurando
ferramentas do Hello Service Fabric para Visual Studio oferece suporte à depuração no computador local. Você pode iniciar uma sessão de depuração, atingindo Olá a tecla F5. O Visual Studio cria (se necessário) pacotes. Também implanta o aplicativo hello no cluster de malha do serviço local hello e anexa o depurador hello.

Durante o processo de implantação Olá, você pode ver o progresso Olá no hello **saída** janela.

![Janela de saída de depuração do Service Fabric][3]

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre [como Reliable Actors usar plataforma do Service Fabric Olá](service-fabric-reliable-actors-platform.md).

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject.PNG
[2]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-projectstructure.PNG
[3]: ./media/service-fabric-reliable-actors-get-started/debugging-output.PNG
[4]: ./media/service-fabric-reliable-actors-get-started/vs-context-menu.png
[5]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject1.PNG
