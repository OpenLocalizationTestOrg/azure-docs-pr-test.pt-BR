---
title: "aaaCreate seu primeiro microsserviço confiável do Azure em Java | Microsoft Docs"
description: "Introdução toocreating um aplicativo do Microsoft Azure Service Fabric com serviços com e sem monitoração de estado."
services: service-fabric
documentationcenter: java
author: vturecek
manager: timlt
editor: 
ms.assetid: 7831886f-7ec4-4aef-95c5-b2469a5b7b5d
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 577d96591797bbfe6be5c1094426b5f1435cca0f
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

Este artigo explica conceitos básicos de saudação dos serviços do Azure Service Fabric confiável e ajuda você a criar e implantar um aplicativo de serviço confiável simples escrito em Java. Este vídeo Microsoft Virtual Academy também mostra como toocreate um serviço confiável sem monitoração de estado:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965">  
<img src="./media/service-fabric-reliable-services-quick-start-java/ReliableServicesJavaVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="installation-and-setup"></a>Instalação e configuração
Antes de começar, certifique-se de que o ambiente de desenvolvimento do Service Fabric Olá configurado no seu computador.
Se você precisar tooset-lo, vá muito[guia de Introdução no Mac](service-fabric-get-started-mac.md) ou [guia de Introdução no Linux](service-fabric-get-started-linux.md).

## <a name="basic-concepts"></a>Conceitos básicos
tooget iniciado com serviços confiáveis, você só precisa toounderstand alguns conceitos básicos:

* **Tipo de serviço**: esta é sua implementação de serviço. Ele é definido pela classe Olá gravar que estende `StatelessService` e qualquer outro código ou dependências usadas neste documento, juntamente com um nome e um número de versão.
* **Serviço de instância nomeada**: toorun seu serviço, você cria instâncias nomeadas do seu tipo de serviço, bem como criar instâncias de objeto de um tipo de classe. Instâncias de serviço são, na verdade, as instâncias de objeto de sua classe de serviço que você escreve.
* **Host de serviço**: Olá denominado criar necessidade toorun dentro de um host de instâncias de serviço. host de serviço Olá é apenas um processo em que as instâncias do serviço podem executar.
* **Registro de serviço**: o registro reúne tudo. Olá service type deve ser registrado com hello Service Fabric em tempo de execução em um serviço de hospedar instâncias de toocreate Service Fabric tooallow-toorun.  

## <a name="create-a-stateless-service"></a>Criar um serviço sem estado
Comece criando um aplicativo de Service Fabric. Olá SDK do Service Fabric para Linux inclui um Yeoman scaffolding de saudação do gerador tooprovide para um aplicativo de malha do serviço com um serviço sem monitoração de estado. Inicie executando Olá Yeoman a seguir de comando:

```bash
$ yo azuresfjava
```

Siga Olá instruções toocreate um **serviço sem monitoração de estado confiável**. Para este tutorial, o aplicativo hello de nome "HelloWorldApplication" e Olá serviço "Olámundo". saudação de resultados inclui diretórios para Olá `HelloWorldApplication` e `HelloWorld`.

```bash
HelloWorldApplication/
├── build.gradle
├── HelloWorld
│   ├── build.gradle
│   └── src
│       └── statelessservice
│           ├── HelloWorldServiceHost.java
│           └── HelloWorldService.java
├── HelloWorldApplication
│   ├── ApplicationManifest.xml
│   └── HelloWorldPkg
│       ├── Code
│       │   ├── entryPoint.sh
│       │   └── _readme.txt
│       ├── Config
│       │   └── _readme.txt
│       ├── Data
│       │   └── _readme.txt
│       └── ServiceManifest.xml
├── install.sh
├── settings.gradle
└── uninstall.sh
```

## <a name="implement-hello-service"></a>Implementar o serviço de saudação
Abra **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**. Essa classe define o tipo de serviço hello e pode executar qualquer código. API do serviço de saudação oferece dois pontos de entrada para o seu código:

* Um método de ponto de entrada em aberto chamado `runAsync()`, em que você pode começar a executar qualquer carga de trabalho, incluindo cargas de trabalho de computação de longa duração.

```java
@Override
protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {
    ...
}
```

* Um ponto de entrada de comunicação no qual você pode conectar a pilha de comunicação de sua escolha. É onde você pode começar a receber solicitações de usuários e outros serviços.

```java
@Override
protected List<ServiceInstanceListener> createServiceInstanceListeners() {
    ...
}
```

Neste tutorial, vamos nos concentrar em Olá `runAsync()` método de ponto de entrada. É aqui que você pode começar imediatamente a executar seu código.

### <a name="runasync"></a>RunAsync
plataforma de saudação chama este método quando uma instância de um serviço é tooexecute inserida e pronto. Para um serviço sem monitoração de estado, que simplesmente significa que quando a instância do serviço de saudação é aberta. Um token de cancelamento é fornecido toocoordinate quando toobe fechado as necessidades de sua instância de serviço. Na malha do serviço, esse ciclo de abertura/fechamento de uma instância de serviço pode ocorrer muitas vezes em tempo de vida de saudação do serviço hello como um todo. Isso pode ocorrer por vários motivos, incluindo:

* sistema de saudação move suas instâncias de serviço de balanceamento de recursos.
* Ocorrem falhas no código.
* aplicativo Hello ou o sistema é atualizado.
* hardware subjacente Olá sofrer uma interrupção.

Essa orquestração é gerenciada pelo Service Fabric tookeep seu serviço altamente disponível e adequadamente equilibrado.

`runAsync()` não deve bloquear sincronicamente. A implementação de runAsync deve retornar um toocontinue de tempo de execução CompletableFuture tooallow hello. Se sua carga de trabalho precisa de uma tarefa demorada que deve ser feita dentro de tooimplement Olá CompletableFuture.

#### <a name="cancellation"></a>Cancelamento
O cancelamento da sua carga de trabalho é um esforço cooperativo orquestrado pelo Olá fornecido um token de cancelamento. sistema de Olá aguarda sua tarefa tooend (pela conclusão bem-sucedida, cancelamento ou falha) antes de ele prossegue. É importante toohonor Olá cancelamento token, concluir qualquer trabalho e sair `runAsync()` assim que possível quando o sistema Olá solicitações de cancelamento. Olá exemplo a seguir demonstra como um evento de cancelamento de toohandle:

```java
    @Override
    protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {

        // TODO: Replace hello following sample code with your own logic
        // or remove this runAsync override if it's not needed in your service.

        CompletableFuture.runAsync(() -> {
          long iterations = 0;
          while(true)
          {
            cancellationToken.throwIfCancellationRequested();
            logger.log(Level.INFO, "Working-{0}", ++iterations);

            try
            {
              Thread.sleep(1000);
            }
            catch (IOException ex) {}
          }
        });
    }
```

### <a name="service-registration"></a>Registro do serviço
Tipos de serviço devem ser registrados com o tempo de execução do hello Service Fabric. tipo de serviço de saudação é definido em Olá `ServiceManifest.xml` e sua classe de serviço implementa `StatelessService`. Registro de serviço é executado no ponto de entrada principal do processo de saudação. Neste exemplo, Olá o processo de ponto de entrada principal é `HelloWorldServiceHost.java`:

```java
public static void main(String[] args) throws Exception {
    try {
        ServiceRuntime.registerStatelessServiceAsync("HelloWorldType", (context) -> new HelloWorldService(), Duration.ofSeconds(10));
        logger.log(Level.INFO, "Registered stateless service type HelloWorldType.");
        Thread.sleep(Long.MAX_VALUE);
    }
    catch (Exception ex) {
        logger.log(Level.SEVERE, "Exception in registration:", ex);
        throw ex;
    }
}
```

## <a name="run-hello-application"></a>Executar o aplicativo hello

Olá Yeoman scaffolding inclui um gradle script toobuild Olá aplicativo e bash scripts toodeploy e remover o aplicativo. aplicativo de hello toorun, primeiro aplicativo hello de compilação com gradle:

```bash
$ gradle
```

Isso produz um pacote de aplicativos do Service Fabric que poderá ser implantado usando a CLI do Service Fabric.

### <a name="deploy-with-service-fabric-cli"></a>Implantar com a CLI do Service Fabric

script de install.sh de Olá contém Olá necessário CLI de malha do serviço comandos toodeploy Olá pacote de aplicativo. Execute o aplicativo de hello toodeploy install.sh script.

```bash
$ ./install.sh
```

## <a name="next-steps"></a>Próximas etapas

* [Introdução à CLI do Service Fabric](service-fabric-cli.md)
