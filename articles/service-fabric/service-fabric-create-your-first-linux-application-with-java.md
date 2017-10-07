---
title: "aaaCreate um aplicativo de Java do Azure Service Fabric atores confiável no Linux | Microsoft Docs"
description: "Saiba como toocreate e implantar um aplicativo de atores confiável Java Service Fabric em cinco minutos."
services: service-fabric
documentationcenter: java
author: rwike77
manager: timlt
editor: 
ms.assetid: 02b51f11-5d78-4c54-bb68-8e128677783e
ms.service: service-fabric
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/23/2017
ms.author: ryanwi
ms.openlocfilehash: 11496b767811c89969c65d1682d843448eb6a922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-java-service-fabric-reliable-actors-application-on-linux"></a>Crie seu primeiro aplicativo Java de Reliable Actors do Service Fabric no Linux
> [!div class="op_single_selector"]
> * [C# - Windows](service-fabric-create-your-first-application-in-visual-studio.md)
> * [Java - Linux](service-fabric-create-your-first-linux-application-with-java.md)
> * [C# - Linux](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

Este guia de início rápido ajuda a criar seu primeiro aplicativo Java do Azure Service Fabric em um ambiente de desenvolvimento Linux em alguns minutos.  Quando você terminar, você terá um aplicativo simples de serviço único Java em execução no cluster de desenvolvimento local hello.  

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar, instale Olá SDK do Service Fabric, Olá CLI de malha do serviço e a instalação de um cluster de desenvolvimento no seu [ambiente de desenvolvimento do Linux](service-fabric-get-started-linux.md). Se estiver usando o Mac OS X, você poderá [configurar um ambiente de desenvolvimento Linux em uma máquina virtual usando Vagrant](service-fabric-get-started-mac.md).

Você também pode tooinstall Olá [CLI de malha do serviço](service-fabric-cli.md).

### <a name="install-and-set-up-hello-generators-for-java"></a>Instalar e configurar os geradores de saudação para Java
O Service Fabric fornece ferramentas de scaffolding que ajudarão a criar um aplicativo Java do Service Fabric no terminal usando gerador de modelos Yeoman. Siga as etapas de saudação abaixo tooensure que ter gerador de modelo yeoman Olá Service Fabric para Java trabalhando em seu computador.
1. Instalar o nodejs e o NPM em seu computador

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. Instalar o gerador de modelos [Yeoman](http://yeoman.io/) em seu computador a partir do NPM

  ```bash
  sudo npm install -g yo
  ```
3. Instalar o gerador de aplicativo de serviço do Fabric Yeo Java Olá do NPM

  ```bash
  sudo npm install -g generator-azuresfjava
  ```

## <a name="create-hello-application"></a>Criar um aplicativo hello
Um aplicativo de malha do serviço contém um ou mais serviços, cada um com uma função específica no fornecimento de funcionalidade do aplicativo hello. Gerador de saudação instalado na última seção de hello, torna fácil toocreate seu primeiro serviço e tooadd mais mais tarde.  Você também pode criar, compilar e implantar aplicativos em Java do Service Fabric usando um plug-in para Eclipse. Confira [Como criar e implantar seu primeiro aplicativo em Java usando o Eclipse](service-fabric-get-started-eclipse.md). Para este início rápido, use Yeoman toocreate um aplicativo com um único serviço que armazena e obtém um valor do contador.

1. Em um terminal, digite ``yo azuresfjava``.
2. Nome do seu aplicativo.
3. Escolha o tipo de saudação do seu primeiro serviço e nomeie-o. Para este tutorial, escolha um serviço de ator confiável. Para obter mais informações sobre Olá outros tipos de serviços, consulte [visão geral do modelo de programação do Service Fabric](service-fabric-choose-framework.md).
   ![Gerador de Yeoman do Service Fabric para Java][sf-yeoman]

## <a name="build-hello-application"></a>Criar um aplicativo hello
modelos de serviço do Fabric Yeoman Olá incluem um script de compilação para [Gradle](https://gradle.org/), que você pode usar o aplicativo hello toobuild Olá terminal.
As dependências Java do Service Fabric são obtidas no Maven. toobuild e o trabalho em aplicativos de serviço do Fabric Java Olá, é necessário tooensure que você tenha o JDK e Gradle instalado. Se ainda não estiver instalado, você poderá executar Olá tooinstall JDK(openjdk-8-jdk) e Gradle - a seguir

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

toobuild e pacote de aplicativo hello, execute Olá seguinte:

  ```bash
  cd myapp
  gradle
  ```

## <a name="deploy-hello-application"></a>Implantar o aplicativo hello
Depois que o aplicativo hello é criado, você pode implantar cluster local toohello.

1. Conecte-se toohello cluster de malha do serviço local.

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. Execute o script de instalação de Olá fornecido no hello modelo toocopy aplicativo hello pacote repositório de imagens do cluster toohello, registrar o tipo de aplicativo hello e criar uma instância do aplicativo hello.

    ```bash
    ./install.sh
    ```

Implantando aplicativo de hello criado é Olá mesmo como qualquer outro aplicativo de malha do serviço. Consulte a documentação de saudação em [gerenciar um aplicativo de malha do serviço com hello CLI de malha do serviço](service-fabric-application-lifecycle-sfctl.md) para obter instruções detalhadas.

Comandos de toothese de parâmetros podem ser encontrados nos manifestos de saudação gerado dentro do pacote de aplicativo hello.

Depois que o aplicativo hello foi implantado, abra um navegador e navegue até [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) em [http://localhost:19080/Explorer](http://localhost:19080/Explorer).
Em seguida, expanda Olá **aplicativos** nó e observe que agora há uma entrada para o tipo de aplicativo e outro para Olá primeira instância desse tipo.

## <a name="start-hello-test-client-and-perform-a-failover"></a>Inicie o cliente de teste hello e executar um failover
Atores não fazem nada por conta própria, eles exigem outro toosend de serviço ou cliente mensagens-los. modelo de ator Olá inclui um script de teste simples que você pode usar toointeract com o serviço de ator hello.

1. Execute script hello usando Olá inspecionar utilitário toosee Olá saída do serviço de ator hello.  script de teste Olá chama Olá `setCountAsync()` as chamadas de método em Olá ator tooincrement um contador, Olá `getCountAsync()` método hello ator tooget Olá novo valor do contador e exibe esse valor toohello console.

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```

2. No Service Fabric Explorer, localize Olá nó hospedagem Olá réplica primária para o serviço de ator hello. Olá captura de tela abaixo, é o nó 3. identificadores de réplica de serviço primário Olá operações leitura e gravação.  As alterações no estado do serviço, em seguida, são replicadas toohello de réplicas secundárias, em execução em nós 0 e 1 na tela hello abaixo.

    ![Localizar a réplica primária Olá no Gerenciador do Service Fabric][sfx-primary]

3. Em **nós**, clique no nó Olá encontrado na etapa anterior Olá, e selecione **desativar (reinicialização)** no menu de ações de saudação. Essa ação reinicia nó Olá executando Olá serviço primário réplica e força uma tooone de failover de réplicas secundárias de saudação em execução em outro nó.  Essa réplica secundária é promovida tooprimary, outra réplica secundária é criada em um nó diferente e começa a réplica primária Olá tootake operações de leitura/gravação. Como o nó de saudação for reiniciado, assista a saída de saudação do cliente de teste de saudação e observe que esse contador Olá continua tooincrement apesar Olá failover.

## <a name="remove-hello-application"></a>Remover o aplicativo hello
Usar script de desinstalação Olá fornecido na instância de aplicativo hello modelo toodelete hello, cancelar o registro do pacote de aplicativo hello e remova o pacote de aplicativo de saudação do cluster de saudação repositório de imagens.

```bash
./uninstall.sh
```

No Gerenciador do Service Fabric ver que tipo de aplicativo e o aplicativo hello não aparecem mais na Olá **aplicativos** nó.

## <a name="service-fabric-java-libraries-on-maven"></a>Bibliotecas Java do Service Fabric no Maven
As bibliotecas Java do Service Fabric foram hospedadas no Maven. Você pode adicionar dependências Olá Olá ``pom.xml`` ou ``build.gradle`` de bibliotecas do Java de malha do serviço de toouse projetos do **mavenCentral**.

### <a name="actors"></a>Atores

Suporte Reliable Actor do Service Fabric para seu aplicativo.

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-actors-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-actors-preview:0.10.0'
  }
  ```

### <a name="services"></a>Serviços

Suporte do Serviço sem Estado do Service Fabric para seu aplicativo.

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-services-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-services-preview:0.10.0'
  }
  ```

### <a name="others"></a>Outros
#### <a name="transport"></a>Transporte

Suporte da camada de transporte para aplicativo Java do Service Fabric. Você não precisa tooexplicitly adicionar essa dependência tooyour Reliable Actor ou aplicativos de serviço, a menos que o programa na camada de transporte hello.

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-transport-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-transport-preview:0.10.0'
  }
  ```

#### <a name="fabric-support"></a>Suporte do Fabric

Suporte ao nível do sistema para o serviço de malha, que fala toonative Service Fabric runtime. Você não precisa tooexplicitly adicionar essa dependência tooyour Reliable Actor ou aplicativos de serviço. Isso é buscado automaticamente do Maven, quando você incluir Olá outras dependências acima.

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-preview:0.10.0'
  }
  ```

## <a name="migrating-old-service-fabric-java-applications-toobe-used-with-maven"></a>Migrando toobe antigo de aplicativos Java de malha do serviço usado com o Maven
Podemos recentemente moveu bibliotecas Java de malha do serviço de repositório de tooMaven do Java SDK do Service Fabric. Enquanto os novos aplicativos de saudação geradas usando Yeoman ou Eclipse, irá gerar projetos atualizados mais recente (que serão capaz de toowork com o Maven), você pode atualizar sua malha de serviço existente sem monitoração de estado ou aplicativos Java de ator, que estavam usando o serviço de saudação Malha Java SDK anterior, toouse dependências de Java de malha do serviço de saudação do Maven. Siga as etapas de saudação mencionadas [aqui](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure seu aplicativo mais antigo funciona com o Maven.

## <a name="next-steps"></a>Próximas etapas

* [Como criar seu primeiro aplicativo em Java do Service Fabric no Linux usando o Eclipse](service-fabric-get-started-eclipse.md)
* [Reliable Actors](service-fabric-reliable-actors-introduction.md)
* [Interagir com clusters de malha do serviço usando Olá CLI de malha do serviço](service-fabric-cli.md)
* Saiba mais sobre as [opções de suporte do Service Fabric](service-fabric-support.md)
* [Introdução à CLI do Service Fabric](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-yeoman.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-java/sfx-primary.png
[sf-eclipse-templates]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-eclipse-templates.png
