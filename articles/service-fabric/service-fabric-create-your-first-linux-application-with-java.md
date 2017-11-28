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
# <a name="create-your-first-java-service-fabric-reliable-actors-application-on-linux"></a><span data-ttu-id="50934-103">Crie seu primeiro aplicativo Java de Reliable Actors do Service Fabric no Linux</span><span class="sxs-lookup"><span data-stu-id="50934-103">Create your first Java Service Fabric Reliable Actors application on Linux</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="50934-104">C# - Windows</span><span class="sxs-lookup"><span data-stu-id="50934-104">C# - Windows</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
> * [<span data-ttu-id="50934-105">Java - Linux</span><span class="sxs-lookup"><span data-stu-id="50934-105">Java - Linux</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
> * [<span data-ttu-id="50934-106">C# - Linux</span><span class="sxs-lookup"><span data-stu-id="50934-106">C# - Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

<span data-ttu-id="50934-107">Este guia de início rápido ajuda a criar seu primeiro aplicativo Java do Azure Service Fabric em um ambiente de desenvolvimento Linux em alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="50934-107">This quick-start helps you create your first Azure Service Fabric Java application in a Linux development environment in just a few minutes.</span></span>  <span data-ttu-id="50934-108">Quando você terminar, você terá um aplicativo simples de serviço único Java em execução no cluster de desenvolvimento local hello.</span><span class="sxs-lookup"><span data-stu-id="50934-108">When you are finished, you'll have a simple Java single-service application running on hello local development cluster.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="50934-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="50934-109">Prerequisites</span></span>
<span data-ttu-id="50934-110">Antes de começar, instale Olá SDK do Service Fabric, Olá CLI de malha do serviço e a instalação de um cluster de desenvolvimento no seu [ambiente de desenvolvimento do Linux](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="50934-110">Before you get started, install hello Service Fabric SDK, hello Service Fabric CLI, and setup a development cluster in your [Linux development environment](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="50934-111">Se estiver usando o Mac OS X, você poderá [configurar um ambiente de desenvolvimento Linux em uma máquina virtual usando Vagrant](service-fabric-get-started-mac.md).</span><span class="sxs-lookup"><span data-stu-id="50934-111">If you are using Mac OS X, you can [set up a Linux development environment in a virtual machine using Vagrant](service-fabric-get-started-mac.md).</span></span>

<span data-ttu-id="50934-112">Você também pode tooinstall Olá [CLI de malha do serviço](service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="50934-112">You will also want tooinstall hello [Service Fabric CLI](service-fabric-cli.md).</span></span>

### <a name="install-and-set-up-hello-generators-for-java"></a><span data-ttu-id="50934-113">Instalar e configurar os geradores de saudação para Java</span><span class="sxs-lookup"><span data-stu-id="50934-113">Install and set up hello generators for Java</span></span>
<span data-ttu-id="50934-114">O Service Fabric fornece ferramentas de scaffolding que ajudarão a criar um aplicativo Java do Service Fabric no terminal usando gerador de modelos Yeoman.</span><span class="sxs-lookup"><span data-stu-id="50934-114">Service Fabric provides scaffolding tools which will help you create a Service Fabric Java application from terminal using Yeoman template generator.</span></span> <span data-ttu-id="50934-115">Siga as etapas de saudação abaixo tooensure que ter gerador de modelo yeoman Olá Service Fabric para Java trabalhando em seu computador.</span><span class="sxs-lookup"><span data-stu-id="50934-115">Please follow hello steps below tooensure you have hello Service Fabric yeoman template generator for Java working on your machine.</span></span>
1. <span data-ttu-id="50934-116">Instalar o nodejs e o NPM em seu computador</span><span class="sxs-lookup"><span data-stu-id="50934-116">Install nodejs and NPM on your machine</span></span>

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. <span data-ttu-id="50934-117">Instalar o gerador de modelos [Yeoman](http://yeoman.io/) em seu computador a partir do NPM</span><span class="sxs-lookup"><span data-stu-id="50934-117">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  sudo npm install -g yo
  ```
3. <span data-ttu-id="50934-118">Instalar o gerador de aplicativo de serviço do Fabric Yeo Java Olá do NPM</span><span class="sxs-lookup"><span data-stu-id="50934-118">Install hello Service Fabric Yeo Java application generator from NPM</span></span>

  ```bash
  sudo npm install -g generator-azuresfjava
  ```

## <a name="create-hello-application"></a><span data-ttu-id="50934-119">Criar um aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="50934-119">Create hello application</span></span>
<span data-ttu-id="50934-120">Um aplicativo de malha do serviço contém um ou mais serviços, cada um com uma função específica no fornecimento de funcionalidade do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="50934-120">A Service Fabric application contains one or more services, each with a specific role in delivering hello application's functionality.</span></span> <span data-ttu-id="50934-121">Gerador de saudação instalado na última seção de hello, torna fácil toocreate seu primeiro serviço e tooadd mais mais tarde.</span><span class="sxs-lookup"><span data-stu-id="50934-121">hello generator you installed in hello last section, makes it easy toocreate your first service and tooadd more later.</span></span>  <span data-ttu-id="50934-122">Você também pode criar, compilar e implantar aplicativos em Java do Service Fabric usando um plug-in para Eclipse.</span><span class="sxs-lookup"><span data-stu-id="50934-122">You can also create, build, and deploy Service Fabric Java applications using a plugin for Eclipse.</span></span> <span data-ttu-id="50934-123">Confira [Como criar e implantar seu primeiro aplicativo em Java usando o Eclipse](service-fabric-get-started-eclipse.md).</span><span class="sxs-lookup"><span data-stu-id="50934-123">See [Create and deploy your first Java application using Eclipse](service-fabric-get-started-eclipse.md).</span></span> <span data-ttu-id="50934-124">Para este início rápido, use Yeoman toocreate um aplicativo com um único serviço que armazena e obtém um valor do contador.</span><span class="sxs-lookup"><span data-stu-id="50934-124">For this quick start, use Yeoman toocreate an application with a single service that stores and gets a counter value.</span></span>

1. <span data-ttu-id="50934-125">Em um terminal, digite ``yo azuresfjava``.</span><span class="sxs-lookup"><span data-stu-id="50934-125">In a terminal, type ``yo azuresfjava``.</span></span>
2. <span data-ttu-id="50934-126">Nome do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="50934-126">Name your application.</span></span>
3. <span data-ttu-id="50934-127">Escolha o tipo de saudação do seu primeiro serviço e nomeie-o.</span><span class="sxs-lookup"><span data-stu-id="50934-127">Choose hello type of your first service and name it.</span></span> <span data-ttu-id="50934-128">Para este tutorial, escolha um serviço de ator confiável.</span><span class="sxs-lookup"><span data-stu-id="50934-128">For this tutorial, choose a Reliable Actor Service.</span></span> <span data-ttu-id="50934-129">Para obter mais informações sobre Olá outros tipos de serviços, consulte [visão geral do modelo de programação do Service Fabric](service-fabric-choose-framework.md).</span><span class="sxs-lookup"><span data-stu-id="50934-129">For more information about hello other types of services, see [Service Fabric programming model overview](service-fabric-choose-framework.md).</span></span>
   <span data-ttu-id="50934-130">![Gerador de Yeoman do Service Fabric para Java][sf-yeoman]</span><span class="sxs-lookup"><span data-stu-id="50934-130">![Service Fabric Yeoman generator for Java][sf-yeoman]</span></span>

## <a name="build-hello-application"></a><span data-ttu-id="50934-131">Criar um aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="50934-131">Build hello application</span></span>
<span data-ttu-id="50934-132">modelos de serviço do Fabric Yeoman Olá incluem um script de compilação para [Gradle](https://gradle.org/), que você pode usar o aplicativo hello toobuild Olá terminal.</span><span class="sxs-lookup"><span data-stu-id="50934-132">hello Service Fabric Yeoman templates include a build script for [Gradle](https://gradle.org/), which you can use toobuild hello application from hello terminal.</span></span>
<span data-ttu-id="50934-133">As dependências Java do Service Fabric são obtidas no Maven.</span><span class="sxs-lookup"><span data-stu-id="50934-133">Service Fabric Java dependencies get fetched from Maven.</span></span> <span data-ttu-id="50934-134">toobuild e o trabalho em aplicativos de serviço do Fabric Java Olá, é necessário tooensure que você tenha o JDK e Gradle instalado.</span><span class="sxs-lookup"><span data-stu-id="50934-134">toobuild and work on hello Service Fabric Java applications, you need tooensure that you have JDK and Gradle installed.</span></span> <span data-ttu-id="50934-135">Se ainda não estiver instalado, você poderá executar Olá tooinstall JDK(openjdk-8-jdk) e Gradle - a seguir</span><span class="sxs-lookup"><span data-stu-id="50934-135">If not yet installed, you can run hello following tooinstall JDK(openjdk-8-jdk) and Gradle -</span></span>

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

<span data-ttu-id="50934-136">toobuild e pacote de aplicativo hello, execute Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="50934-136">toobuild and package hello application, run hello following:</span></span>

  ```bash
  cd myapp
  gradle
  ```

## <a name="deploy-hello-application"></a><span data-ttu-id="50934-137">Implantar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="50934-137">Deploy hello application</span></span>
<span data-ttu-id="50934-138">Depois que o aplicativo hello é criado, você pode implantar cluster local toohello.</span><span class="sxs-lookup"><span data-stu-id="50934-138">Once hello application is built, you can deploy it toohello local cluster.</span></span>

1. <span data-ttu-id="50934-139">Conecte-se toohello cluster de malha do serviço local.</span><span class="sxs-lookup"><span data-stu-id="50934-139">Connect toohello local Service Fabric cluster.</span></span>

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. <span data-ttu-id="50934-140">Execute o script de instalação de Olá fornecido no hello modelo toocopy aplicativo hello pacote repositório de imagens do cluster toohello, registrar o tipo de aplicativo hello e criar uma instância do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="50934-140">Run hello install script provided in hello template toocopy hello application package toohello cluster's image store, register hello application type, and create an instance of hello application.</span></span>

    ```bash
    ./install.sh
    ```

<span data-ttu-id="50934-141">Implantando aplicativo de hello criado é Olá mesmo como qualquer outro aplicativo de malha do serviço.</span><span class="sxs-lookup"><span data-stu-id="50934-141">Deploying hello built application is hello same as any other Service Fabric application.</span></span> <span data-ttu-id="50934-142">Consulte a documentação de saudação em [gerenciar um aplicativo de malha do serviço com hello CLI de malha do serviço](service-fabric-application-lifecycle-sfctl.md) para obter instruções detalhadas.</span><span class="sxs-lookup"><span data-stu-id="50934-142">See hello documentation on [managing a Service Fabric application with hello Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md) for detailed instructions.</span></span>

<span data-ttu-id="50934-143">Comandos de toothese de parâmetros podem ser encontrados nos manifestos de saudação gerado dentro do pacote de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="50934-143">Parameters toothese commands can be found in hello generated manifests inside hello application package.</span></span>

<span data-ttu-id="50934-144">Depois que o aplicativo hello foi implantado, abra um navegador e navegue até [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) em [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="50934-144">Once hello application has been deployed, open a browser and navigate to [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) at [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span>
<span data-ttu-id="50934-145">Em seguida, expanda Olá **aplicativos** nó e observe que agora há uma entrada para o tipo de aplicativo e outro para Olá primeira instância desse tipo.</span><span class="sxs-lookup"><span data-stu-id="50934-145">Then, expand hello **Applications** node and note that there is now an entry for your application type and another for hello first instance of that type.</span></span>

## <a name="start-hello-test-client-and-perform-a-failover"></a><span data-ttu-id="50934-146">Inicie o cliente de teste hello e executar um failover</span><span class="sxs-lookup"><span data-stu-id="50934-146">Start hello test client and perform a failover</span></span>
<span data-ttu-id="50934-147">Atores não fazem nada por conta própria, eles exigem outro toosend de serviço ou cliente mensagens-los.</span><span class="sxs-lookup"><span data-stu-id="50934-147">Actors do not do anything on their own, they require another service or client toosend them messages.</span></span> <span data-ttu-id="50934-148">modelo de ator Olá inclui um script de teste simples que você pode usar toointeract com o serviço de ator hello.</span><span class="sxs-lookup"><span data-stu-id="50934-148">hello actor template includes a simple test script that you can use toointeract with hello actor service.</span></span>

1. <span data-ttu-id="50934-149">Execute script hello usando Olá inspecionar utilitário toosee Olá saída do serviço de ator hello.</span><span class="sxs-lookup"><span data-stu-id="50934-149">Run hello script using hello watch utility toosee hello output of hello actor service.</span></span>  <span data-ttu-id="50934-150">script de teste Olá chama Olá `setCountAsync()` as chamadas de método em Olá ator tooincrement um contador, Olá `getCountAsync()` método hello ator tooget Olá novo valor do contador e exibe esse valor toohello console.</span><span class="sxs-lookup"><span data-stu-id="50934-150">hello test script calls hello `setCountAsync()` method on hello actor tooincrement a counter, calls hello `getCountAsync()` method on hello actor tooget hello new counter value, and displays that value toohello console.</span></span>

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```

2. <span data-ttu-id="50934-151">No Service Fabric Explorer, localize Olá nó hospedagem Olá réplica primária para o serviço de ator hello.</span><span class="sxs-lookup"><span data-stu-id="50934-151">In Service Fabric Explorer, locate hello node hosting hello primary replica for hello actor service.</span></span> <span data-ttu-id="50934-152">Olá captura de tela abaixo, é o nó 3.</span><span class="sxs-lookup"><span data-stu-id="50934-152">In hello screenshot below, it is node 3.</span></span> <span data-ttu-id="50934-153">identificadores de réplica de serviço primário Olá operações leitura e gravação.</span><span class="sxs-lookup"><span data-stu-id="50934-153">hello primary service replica handles read and write operations.</span></span>  <span data-ttu-id="50934-154">As alterações no estado do serviço, em seguida, são replicadas toohello de réplicas secundárias, em execução em nós 0 e 1 na tela hello abaixo.</span><span class="sxs-lookup"><span data-stu-id="50934-154">Changes in service state are then replicated out toohello secondary replicas, running on nodes 0 and 1 in hello screen shot below.</span></span>

    ![Localizar a réplica primária Olá no Gerenciador do Service Fabric][sfx-primary]

3. <span data-ttu-id="50934-156">Em **nós**, clique no nó Olá encontrado na etapa anterior Olá, e selecione **desativar (reinicialização)** no menu de ações de saudação.</span><span class="sxs-lookup"><span data-stu-id="50934-156">In **Nodes**, click hello node you found in hello previous step, then select **Deactivate (restart)** from hello Actions menu.</span></span> <span data-ttu-id="50934-157">Essa ação reinicia nó Olá executando Olá serviço primário réplica e força uma tooone de failover de réplicas secundárias de saudação em execução em outro nó.</span><span class="sxs-lookup"><span data-stu-id="50934-157">This action restarts hello node running hello primary service replica and forces a failover tooone of hello secondary replicas running on another node.</span></span>  <span data-ttu-id="50934-158">Essa réplica secundária é promovida tooprimary, outra réplica secundária é criada em um nó diferente e começa a réplica primária Olá tootake operações de leitura/gravação.</span><span class="sxs-lookup"><span data-stu-id="50934-158">That secondary replica is promoted tooprimary, another secondary replica is created on a different node, and hello primary replica begins tootake read/write operations.</span></span> <span data-ttu-id="50934-159">Como o nó de saudação for reiniciado, assista a saída de saudação do cliente de teste de saudação e observe que esse contador Olá continua tooincrement apesar Olá failover.</span><span class="sxs-lookup"><span data-stu-id="50934-159">As hello node restarts, watch hello output from hello test client and note that hello counter continues tooincrement despite hello failover.</span></span>

## <a name="remove-hello-application"></a><span data-ttu-id="50934-160">Remover o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="50934-160">Remove hello application</span></span>
<span data-ttu-id="50934-161">Usar script de desinstalação Olá fornecido na instância de aplicativo hello modelo toodelete hello, cancelar o registro do pacote de aplicativo hello e remova o pacote de aplicativo de saudação do cluster de saudação repositório de imagens.</span><span class="sxs-lookup"><span data-stu-id="50934-161">Use hello uninstall script provided in hello template toodelete hello application instance, unregister hello application package, and remove hello application package from hello cluster's image store.</span></span>

```bash
./uninstall.sh
```

<span data-ttu-id="50934-162">No Gerenciador do Service Fabric ver que tipo de aplicativo e o aplicativo hello não aparecem mais na Olá **aplicativos** nó.</span><span class="sxs-lookup"><span data-stu-id="50934-162">In Service Fabric explorer you see that hello application and application type no longer appear in hello **Applications** node.</span></span>

## <a name="service-fabric-java-libraries-on-maven"></a><span data-ttu-id="50934-163">Bibliotecas Java do Service Fabric no Maven</span><span class="sxs-lookup"><span data-stu-id="50934-163">Service Fabric Java libraries on Maven</span></span>
<span data-ttu-id="50934-164">As bibliotecas Java do Service Fabric foram hospedadas no Maven.</span><span class="sxs-lookup"><span data-stu-id="50934-164">Service Fabric Java libraries have been hosted in Maven.</span></span> <span data-ttu-id="50934-165">Você pode adicionar dependências Olá Olá ``pom.xml`` ou ``build.gradle`` de bibliotecas do Java de malha do serviço de toouse projetos do **mavenCentral**.</span><span class="sxs-lookup"><span data-stu-id="50934-165">You can add hello dependencies in hello ``pom.xml`` or ``build.gradle`` of your projects toouse Service Fabric Java libraries from **mavenCentral**.</span></span>

### <a name="actors"></a><span data-ttu-id="50934-166">Atores</span><span class="sxs-lookup"><span data-stu-id="50934-166">Actors</span></span>

<span data-ttu-id="50934-167">Suporte Reliable Actor do Service Fabric para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="50934-167">Service Fabric Reliable Actor support for your application.</span></span>

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

### <a name="services"></a><span data-ttu-id="50934-168">Serviços</span><span class="sxs-lookup"><span data-stu-id="50934-168">Services</span></span>

<span data-ttu-id="50934-169">Suporte do Serviço sem Estado do Service Fabric para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="50934-169">Service Fabric Stateless Service support for your application.</span></span>

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

### <a name="others"></a><span data-ttu-id="50934-170">Outros</span><span class="sxs-lookup"><span data-stu-id="50934-170">Others</span></span>
#### <a name="transport"></a><span data-ttu-id="50934-171">Transporte</span><span class="sxs-lookup"><span data-stu-id="50934-171">Transport</span></span>

<span data-ttu-id="50934-172">Suporte da camada de transporte para aplicativo Java do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="50934-172">Transport layer support for Service Fabric Java application.</span></span> <span data-ttu-id="50934-173">Você não precisa tooexplicitly adicionar essa dependência tooyour Reliable Actor ou aplicativos de serviço, a menos que o programa na camada de transporte hello.</span><span class="sxs-lookup"><span data-stu-id="50934-173">You do not need tooexplicitly add this dependency tooyour Reliable Actor or Service applications, unless you program at hello transport layer.</span></span>

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

#### <a name="fabric-support"></a><span data-ttu-id="50934-174">Suporte do Fabric</span><span class="sxs-lookup"><span data-stu-id="50934-174">Fabric support</span></span>

<span data-ttu-id="50934-175">Suporte ao nível do sistema para o serviço de malha, que fala toonative Service Fabric runtime.</span><span class="sxs-lookup"><span data-stu-id="50934-175">System level support for Service Fabric, which talks toonative Service Fabric runtime.</span></span> <span data-ttu-id="50934-176">Você não precisa tooexplicitly adicionar essa dependência tooyour Reliable Actor ou aplicativos de serviço.</span><span class="sxs-lookup"><span data-stu-id="50934-176">You do not need tooexplicitly add this dependency tooyour Reliable Actor or Service applications.</span></span> <span data-ttu-id="50934-177">Isso é buscado automaticamente do Maven, quando você incluir Olá outras dependências acima.</span><span class="sxs-lookup"><span data-stu-id="50934-177">This gets fetched automatically from Maven, when you include hello other dependencies above.</span></span>

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

## <a name="migrating-old-service-fabric-java-applications-toobe-used-with-maven"></a><span data-ttu-id="50934-178">Migrando toobe antigo de aplicativos Java de malha do serviço usado com o Maven</span><span class="sxs-lookup"><span data-stu-id="50934-178">Migrating old Service Fabric Java applications toobe used with Maven</span></span>
<span data-ttu-id="50934-179">Podemos recentemente moveu bibliotecas Java de malha do serviço de repositório de tooMaven do Java SDK do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="50934-179">We have recently moved Service Fabric Java libraries from Service Fabric Java SDK tooMaven repository.</span></span> <span data-ttu-id="50934-180">Enquanto os novos aplicativos de saudação geradas usando Yeoman ou Eclipse, irá gerar projetos atualizados mais recente (que serão capaz de toowork com o Maven), você pode atualizar sua malha de serviço existente sem monitoração de estado ou aplicativos Java de ator, que estavam usando o serviço de saudação Malha Java SDK anterior, toouse dependências de Java de malha do serviço de saudação do Maven.</span><span class="sxs-lookup"><span data-stu-id="50934-180">While hello new applications you generate using Yeoman or Eclipse, will generate latest updated projects (which will be able toowork with Maven), you can update your existing Service Fabric stateless or actor Java applications, which were using hello Service Fabric Java SDK earlier, toouse hello Service Fabric Java dependencies from Maven.</span></span> <span data-ttu-id="50934-181">Siga as etapas de saudação mencionadas [aqui](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure seu aplicativo mais antigo funciona com o Maven.</span><span class="sxs-lookup"><span data-stu-id="50934-181">Please follow hello steps mentioned [here](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure your older application works with Maven.</span></span>

## <a name="next-steps"></a><span data-ttu-id="50934-182">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="50934-182">Next steps</span></span>

* [<span data-ttu-id="50934-183">Como criar seu primeiro aplicativo em Java do Service Fabric no Linux usando o Eclipse</span><span class="sxs-lookup"><span data-stu-id="50934-183">Create your first Service Fabric Java application on Linux using Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="50934-184">Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="50934-184">Learn more about Reliable Actors</span></span>](service-fabric-reliable-actors-introduction.md)
* [<span data-ttu-id="50934-185">Interagir com clusters de malha do serviço usando Olá CLI de malha do serviço</span><span class="sxs-lookup"><span data-stu-id="50934-185">Interact with Service Fabric clusters using hello Service Fabric CLI</span></span>](service-fabric-cli.md)
* <span data-ttu-id="50934-186">Saiba mais sobre as [opções de suporte do Service Fabric](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="50934-186">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>
* [<span data-ttu-id="50934-187">Introdução à CLI do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="50934-187">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-yeoman.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-java/sfx-primary.png
[sf-eclipse-templates]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-eclipse-templates.png
