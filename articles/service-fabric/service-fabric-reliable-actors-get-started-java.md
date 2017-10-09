---
title: "aaaCreate sua primeira baseado em ator Azure microsserviço em Java | Microsoft Docs"
description: "Este tutorial orienta você pelas etapas de saudação de criar, depurar e implantar um serviço baseado em ator simples usando o serviço de malha Reliable Actors."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d31dc8ab-9760-4619-a641-facb8324c759
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/04/2017
ms.author: vturecek
ms.openlocfilehash: 24718a8d7034360c53597f139169580f1a6ce732
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

Este artigo explica as Noções básicas de saudação do Azure Service Fabric Reliable Actors e orienta você a criar e implantar um aplicativo simples de Reliable Actor em Java.

## <a name="installation-and-setup"></a>Instalação e configuração
Antes de começar, certifique-se de que o ambiente de desenvolvimento do Service Fabric Olá configurado no seu computador.
Se você precisar tooset-lo, vá muito[guia de Introdução no Mac](service-fabric-get-started-mac.md) ou [guia de Introdução no Linux](service-fabric-get-started-linux.md).

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

## <a name="create-an-actor-service"></a>Criar um serviço de ator
Comece criando um novo aplicativo de Service Fabric. Olá SDK do Service Fabric para Linux inclui um Yeoman scaffolding de saudação do gerador tooprovide para um aplicativo de malha do serviço com um serviço sem monitoração de estado. Inicie executando Olá Yeoman a seguir de comando:

```bash
$ yo azuresfjava
```

Siga Olá instruções toocreate um **serviço de ator confiável**. Neste tutorial, nomeie Olá aplicativo "HelloWorldActorApplication" e hello ator "HelloWorldActor". Olá scaffolding a seguir será criado:

```bash
HelloWorldActorApplication/
├── build.gradle
├── HelloWorldActor
│   ├── build.gradle
│   ├── settings.gradle
│   └── src
│       └── reliableactor
│           ├── HelloWorldActorHost.java
│           └── HelloWorldActorImpl.java
├── HelloWorldActorApplication
│   ├── ApplicationManifest.xml
│   └── HelloWorldActorPkg
│       ├── Code
│       │   ├── entryPoint.sh
│       │   └── _readme.txt
│       ├── Config
│       │   ├── _readme.txt
│       │   └── Settings.xml
│       ├── Data
│       │   └── _readme.txt
│       └── ServiceManifest.xml
├── HelloWorldActorInterface
│   ├── build.gradle
│   └── src
│       └── reliableactor
│           └── HelloWorldActor.java
├── HelloWorldActorTestClient
│   ├── build.gradle
│   ├── settings.gradle
│   ├── src
│   │   └── reliableactor
│   │       └── test
│   │           └── HelloWorldActorTestClient.java
│   └── testclient.sh
├── install.sh
├── settings.gradle
└── uninstall.sh
```

## <a name="reliable-actors-basic-building-blocks"></a>Blocos de construção básicos de Reliable Actors
conceitos básicos de saudação descritos anteriormente traduzem em Olá blocos de construção básicos de um serviço de Reliable Actor.

### <a name="actor-interface"></a>Interface do ator
Isso contém a definição de interface de saudação de ator hello. Essa interface define o contrato de ator de saudação que é compartilhado por clientes de Olá chamando ator hello, então, geralmente faz sentido toodefine-lo em um local que é separar da implementação de ator hello e pode ser compartilhado por vários outros e implementação de ator Olá serviços ou aplicativos cliente.

`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`:

```java
public interface HelloWorldActor extends Actor {
    @Readonly   
    CompletableFuture<Integer> getCountAsync();

    CompletableFuture<?> setCountAsync(int count);
}
```

### <a name="actor-service"></a>Serviço de ator
Contém a implementação do ator e o código de registro do ator. classe de ator Olá implementa a interface de ator do hello. É o local em que o ator faz seu trabalho.

`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`:

```java
@ActorServiceAttribute(name = "HelloWorldActor.HelloWorldActorService")
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
public class HelloWorldActorImpl extends ReliableActor implements HelloWorldActor {
    Logger logger = Logger.getLogger(this.getClass().getName());

    protected CompletableFuture<?> onActivateAsync() {
        logger.log(Level.INFO, "onActivateAsync");

        return this.stateManager().tryAddStateAsync("count", 0);
    }

    @Override
    public CompletableFuture<Integer> getCountAsync() {
        logger.log(Level.INFO, "Getting current count value");
        return this.stateManager().getStateAsync("count");
    }

    @Override
    public CompletableFuture<?> setCountAsync(int count) {
        logger.log(Level.INFO, "Setting current count value {0}", count);
        return this.stateManager().addOrUpdateStateAsync("count", count, (key, value) -> count > value ? count : value);
    }
}
```

### <a name="actor-registration"></a>Registro do ator
serviço de ator Olá deve ser registrado com um tipo de serviço em tempo de execução do Service Fabric hello. Em ordem para Olá toorun do serviço de ator suas instâncias de ator, seu tipo de ator também deve ser registrado com hello serviço de ator. Olá `ActorRuntime` método de registro executa essa tarefa para atores.

`HelloWorldActor/src/reliableactor/HelloWorldActorHost`:

```java
public class HelloWorldActorHost {

    public static void main(String[] args) throws Exception {

        try {
            ActorRuntime.registerActorAsync(HelloWorldActorImpl.class, (context, actorType) -> new ActorServiceImpl(context, actorType, ()-> new HelloWorldActorImpl()), Duration.ofSeconds(10));

            Thread.sleep(Long.MAX_VALUE);

        } catch (Exception e) {
            e.printStackTrace();
            throw e;
        }
    }
}
```

### <a name="test-client"></a>Cliente de teste
Este é um aplicativo de cliente de teste simples você pode executar separadamente de saudação do Service Fabric application tootest seu serviço de ator. Este é um exemplo de onde hello ActorProxy pode ser usado tooactivate e se comunicar com instâncias de ator. Ele não é implantado com seu serviço.

### <a name="hello-application"></a>aplicativo Hello
Por fim, pacotes de aplicativos Olá Olá serviço ator e qualquer outro serviço que você pode adicionar em Olá futura juntas para implantação. Ele contém Olá *ApplicationManifest.xml* e espaços reservados para o pacote de serviço de ator hello.

## <a name="run-hello-application"></a>Executar o aplicativo hello

Olá Yeoman scaffolding inclui um gradle script toobuild Olá aplicativo e bash scripts toodeploy e remover o aplicativo. aplicativo de hello toodeploy, primeiro aplicativo hello de compilação com gradle:

```bash
$ gradle
```

Isso produzirá um pacote de aplicativos do Service Fabric que poderá ser implantado usando ferramentas de CLI do Service Fabric.

### <a name="deploy-service-fabric-cli"></a>Implantar a CLI do Service Fabric

script de install.sh de Olá contém Olá necessário CLI de malha do serviço (sfctl) comandos toodeploy Olá pacote de aplicativo.
Execute o aplicativo de saudação do hello install.sh script toodeploy.

```bash
$ ./install.sh
```

## <a name="next-steps"></a>Próximas etapas

* [Introdução à CLI do Service Fabric](service-fabric-cli.md)
