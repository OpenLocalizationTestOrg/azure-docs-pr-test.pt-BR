---
title: "aaaCreate um módulo de borda IoT do Azure com Java | Microsoft Docs"
description: "Este tutorial mostra como toowrite uma BELA dados conversor usando módulo Olá pacotes de Azure IoT borda Maven mais recentes."
services: iot-hub
author: junyi
manager: timlt
ms.service: iot-hub
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 06/28/2017
ms.author: junyi
ms.openlocfilehash: abb560933d13d133ae9a1da08b503d5735b230e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-iot-edge-module-with-java"></a><span data-ttu-id="1b1a8-103">Como criar um módulo do Azure IoT Edge com Java</span><span class="sxs-lookup"><span data-stu-id="1b1a8-103">Create an Azure IoT Edge Module with Java</span></span>

<span data-ttu-id="1b1a8-104">Este tutorial mostra como criar um módulo para Azure IoT Edge em Java.</span><span class="sxs-lookup"><span data-stu-id="1b1a8-104">This tutorial showcases how one might build a module for Azure IoT Edge in Java.</span></span>

<span data-ttu-id="1b1a8-105">Neste tutorial, vamos percorrer a instalação de ambiente e como toowrite uma [Bilitar](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) módulo de conversor de dados usando hello mais recente do Azure IoT borda Maven pacotes.</span><span class="sxs-lookup"><span data-stu-id="1b1a8-105">In this tutorial, we will walk through environment setup and how toowrite a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using hello latest Azure IoT Edge Maven packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b1a8-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1b1a8-106">Prerequisites</span></span>

<span data-ttu-id="1b1a8-107">Nesta seção, você configurará o ambiente para o desenvolvimento do módulo IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="1b1a8-107">In this section, you will set up your environment for IoT Edge module development.</span></span> <span data-ttu-id="1b1a8-108">Aplica-se tooboth *Windows de 64 bits* e *Linux de 64 bits (8 Ubuntu/Debian)* sistemas operacionais.</span><span class="sxs-lookup"><span data-stu-id="1b1a8-108">It applies tooboth *64-bit Windows* and *64-bit Linux (Ubuntu/Debian 8)* operating systems.</span></span>

<span data-ttu-id="1b1a8-109">saudação de software a seguir é necessária:</span><span class="sxs-lookup"><span data-stu-id="1b1a8-109">hello following software is required:</span></span>

* <span data-ttu-id="1b1a8-110">[Cliente Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="1b1a8-110">[Git Client](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="1b1a8-111">[**x64** JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="1b1a8-111">[**x64** JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="1b1a8-112">[Maven](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="1b1a8-112">[Maven](https://maven.apache.org/install.html).</span></span>

<span data-ttu-id="1b1a8-113">Abra uma linha de comando terminal janela e clone Olá repositório a seguir:</span><span class="sxs-lookup"><span data-stu-id="1b1a8-113">Open a command-line terminal window and clone hello following repository:</span></span>

1. <span data-ttu-id="1b1a8-114">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span><span class="sxs-lookup"><span data-stu-id="1b1a8-114">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span></span>
2. `cd iot-edge-samples/java/simulated_ble`

## <a name="overall-architecture"></a><span data-ttu-id="1b1a8-115">Arquitetura geral</span><span class="sxs-lookup"><span data-stu-id="1b1a8-115">Overall architecture</span></span>

<span data-ttu-id="1b1a8-116">plataforma de Azure IoT borda Olá muito adota Olá [arquitetura Von Neumann](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span><span class="sxs-lookup"><span data-stu-id="1b1a8-116">hello Azure IoT Edge platform heavily adopts hello [Von Neumann architecture](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span></span> <span data-ttu-id="1b1a8-117">Arquitetura do Azure IoT borda Olá toda o que significa é um sistema que processa a entrada e produz a saída. e cada módulo individual também é um pequeno subsistema de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="1b1a8-117">Which means that hello entire Azure IoT Edge architecture is a system which processes input and produces output; and that each individual module is also a tiny input-output subsystem.</span></span> <span data-ttu-id="1b1a8-118">Neste tutorial, apresentaremos Olá dois módulos a seguir:</span><span class="sxs-lookup"><span data-stu-id="1b1a8-118">In this tutorial, we will introduce hello following two modules:</span></span>

1. <span data-ttu-id="1b1a8-119">Um módulo que recebe um sinal [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) simulado e o converte em uma mensagem com formatação [JSON](https://en.wikipedia.org/wiki/JSON).</span><span class="sxs-lookup"><span data-stu-id="1b1a8-119">A module which receives a simulated [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) signal and converts it into a formatted [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>
2. <span data-ttu-id="1b1a8-120">Um módulo que imprime Olá recebida [JSON](https://en.wikipedia.org/wiki/JSON) mensagem.</span><span class="sxs-lookup"><span data-stu-id="1b1a8-120">A module which prints hello received [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>

<span data-ttu-id="1b1a8-121">Olá imagem a seguir exibe fluxo de dados típicos de ponta a ponta do Olá para este projeto:</span><span class="sxs-lookup"><span data-stu-id="1b1a8-121">hello following image displays hello typical end-to-end dataflow for this project:</span></span>

<span data-ttu-id="1b1a8-122">![Fluxo de dados entre três módulos](media/iot-hub-iot-edge-create-module/dataflow.png "Entrada: módulo BLE simulado; Processador: módulo conversor; Saída: módulo de impressão")</span><span class="sxs-lookup"><span data-stu-id="1b1a8-122">![Dataflow between three modules](media/iot-hub-iot-edge-create-module/dataflow.png "Input: Simulated BLE Module; Processor: Converter Module; Output: Printer Module")</span></span>

## <a name="understanding-hello-code"></a><span data-ttu-id="1b1a8-123">Entendendo o código Olá</span><span class="sxs-lookup"><span data-stu-id="1b1a8-123">Understanding hello code</span></span>

### <a name="maven-project-structure"></a><span data-ttu-id="1b1a8-124">Estrutura do projeto Maven</span><span class="sxs-lookup"><span data-stu-id="1b1a8-124">Maven project structure</span></span>

<span data-ttu-id="1b1a8-125">Como os pacotes de borda do Azure IoT são baseados em Maven, precisamos toocreate uma estrutura de projeto Maven típica, que contém um `pom.xml` arquivo.</span><span class="sxs-lookup"><span data-stu-id="1b1a8-125">Since Azure IoT Edge packages are based on Maven, we need toocreate a typical Maven project structure, which contains a `pom.xml` file.</span></span>

<span data-ttu-id="1b1a8-126">Olá POM herda de saudação `com.microsoft.azure.gateway.gateway-module-base` pacote, que declara todas as dependências de saudação necessárias a um projeto de módulo que inclui os binários de tempo de execução de saudação, o caminho do arquivo de configuração de gateway de saudação e o comportamento de execução hello.</span><span class="sxs-lookup"><span data-stu-id="1b1a8-126">hello POM inherits from hello `com.microsoft.azure.gateway.gateway-module-base` package, which declares all of hello dependencies needed by a module project which includes hello runtime binaries, hello gateway configuration file path, and hello execution behavior.</span></span> <span data-ttu-id="1b1a8-127">Isso economiza muito tempo e eliminar Olá necessidade toowrite e reescrever centenas de linhas de código repetidamente.</span><span class="sxs-lookup"><span data-stu-id="1b1a8-127">This saves us lots of time and eliminate hello need toowrite and rewrite hundreds of lines of code over and over again.</span></span>

<span data-ttu-id="1b1a8-128">Precisamos tooupdate o arquivo pom.xml declarando Olá necessário dependências/plug-ins e o nome de saudação do hello toobe de arquivo de configuração usado pelo nosso módulo, conforme mostrado no trecho de código a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="1b1a8-128">We need tooupdate the pom.xml file by declaring hello required dependencies/plugins and hello name of hello configuration file toobe used by our module as shown in hello following code snippet.</span></span>

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <!-- Inherit from parent -->
  <parent>
    <groupId>com.microsoft.azure.gateway</groupId>
    <artifactId>gateway-module-base</artifactId>
    <version>1.0.1</version>
  </parent>
  
  <groupId>com.microsoft.azure.gateway</groupId>
  <artifactId>ble-converter</artifactId>
  <version>1.0</version>
  <packaging>jar</packaging>

  <!-- Set hello filename of hello Azure IoT Edge configuration located
       under ./src/main/resources/gateway/ which is used in parent -->
  <properties>
    <gw.config.fileName>gw-config.json</gw.config.fileName>
  </properties>

  <!-- Re-declare dependencies used in parent -->
  <dependencies>
    <dependency>
      <groupId>com.microsoft.azure.gateway</groupId>
      <artifactId>gateway-java-binding</artifactId>
    </dependency>
    <dependency>
      <groupId>${dependency.runtime.group}</groupId>
      <artifactId>${dependency.runtime.name}</artifactId>
    </dependency>
  </dependencies>

  <!-- Re-declare plugins used in parent -->
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-dependency-plugin</artifactId>
      </plugin>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-resources-plugin</artifactId>
      </plugin>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-shade-plugin</artifactId>
      </plugin>
      <plugin>
        <groupId>org.codehaus.mojo</groupId>
        <artifactId>exec-maven-plugin</artifactId>
      </plugin>
    </plugins>
  </build>
</project>
```

### <a name="basic-understanding-of-an-azure-iot-edge-module"></a><span data-ttu-id="1b1a8-129">Noções básicas sobre um módulo do Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="1b1a8-129">Basic understanding of an Azure IoT Edge module</span></span>

<span data-ttu-id="1b1a8-130">É possível tratar um módulo do Azure IoT Edge como um processador de dados cujo trabalho é: receber a entrada, processá-la e produzir uma saída.</span><span class="sxs-lookup"><span data-stu-id="1b1a8-130">You can treat an Azure IoT Edge module as a data processor whose job is to: receive input, process it, and produce output.</span></span>

<span data-ttu-id="1b1a8-131">Olá entrada pode ser dados de hardware (como um detector de movimento), uma mensagem de outros módulos ou qualquer outro (como um número aleatório gerado periodicamente por um timer).</span><span class="sxs-lookup"><span data-stu-id="1b1a8-131">hello input might be data from hardware (like a motion detector), a message from other modules, or anything else (like a random number generated periodically by a timer).</span></span>

<span data-ttu-id="1b1a8-132">saída de Hello seja a entrada de toohello semelhante, pode ativar o comportamento de hardware (como Olá piscando LED), módulos de tooother uma mensagem ou nada (como o console de impressão toohello).</span><span class="sxs-lookup"><span data-stu-id="1b1a8-132">hello output is similar toohello input, it could trigger hardware behavior (like hello blinking LED), a message tooother modules, or anything else (like printing toohello console).</span></span>

<span data-ttu-id="1b1a8-133">Os módulos comunicam entre si usando classe `com.microsoft.azure.gateway.messaging.Message`.</span><span class="sxs-lookup"><span data-stu-id="1b1a8-133">Modules communicate with each other using `com.microsoft.azure.gateway.messaging.Message` class.</span></span> <span data-ttu-id="1b1a8-134">Olá **conteúdo** de um `Message` é uma matriz de bytes que é capaz de representar qualquer tipo de dados que você deseja.</span><span class="sxs-lookup"><span data-stu-id="1b1a8-134">hello **Content** of a `Message` is a byte array which is capable of representing any kind of data you like.</span></span> <span data-ttu-id="1b1a8-135">**Propriedades** também estão disponíveis no hello `Message` e são simplesmente um mapeamento de cadeia de caracteres de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="1b1a8-135">**Properties** are also available in hello `Message` and are simply a string-to-string mapping.</span></span> <span data-ttu-id="1b1a8-136">Você pode pensar **propriedades** como cabeçalhos de saudação em uma solicitação HTTP ou Olá metadados de um arquivo.</span><span class="sxs-lookup"><span data-stu-id="1b1a8-136">You may think of **Properties** as hello headers in an HTTP request, or hello metadata of a file.</span></span>

<span data-ttu-id="1b1a8-137">Em ordem toodevelop um módulo de borda de IoT do Azure em Java, você precisa toocreate uma nova classe de módulo que herda de `com.microsoft.azure.gateway.core.GatewayModule` e implementar métodos abstratos Olá necessário `receive()` e `destroy()`.</span><span class="sxs-lookup"><span data-stu-id="1b1a8-137">In order toodevelop an Azure IoT Edge module in Java, you need toocreate a new module class which inherits from `com.microsoft.azure.gateway.core.GatewayModule` and implement hello required abstract methods `receive()` and `destroy()`.</span></span> <span data-ttu-id="1b1a8-138">Neste ponto, você também pode escolher tooimplement Olá opcional `start()` ou `create()` métodos também.</span><span class="sxs-lookup"><span data-stu-id="1b1a8-138">At this point, you may also choose tooimplement hello optional `start()` or `create()` methods as well.</span></span> <span data-ttu-id="1b1a8-139">saudação de trecho de código a seguir mostra como tooget iniciada a criação de um módulo de borda de IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="1b1a8-139">hello following code snippet shows you how tooget started authoring an Azure IoT Edge module.</span></span>

```java
import com.microsoft.azure.gateway.core.Broker;
import com.microsoft.azure.gateway.core.GatewayModule;
import com.microsoft.azure.gateway.messaging.Message;

public class MyEdgeModule extends GatewayModule {
  public MyEdgeModule(long address, Broker broker, String configuration) {
    /* Let hello GatewayModule do hello dirty work of initialization. It's also
       a good time tooparse your own configuration defined in Azure IoT Edge
       configuration file (typically ./src/main/resources/gateway/gw-config.json) */
    super(address, broker, configuration);
  }

  @Override
  public void start() {
    /* Acquire hello resources you need. If you don't
       need any resources, you may omit this method. */
  }

  @Override
  public void destroy() {
    /* It's time toorelease all resources. This method is required. */
  }

  @Override
  public void receive(Message message) {
    /* Logic tooprocess hello input message. This method is required. */
    // ...
    /* Use publish() method toodo hello output. You are
       allowed toopublish your new Message instance. */
    this.publish(message);
  }
}
```

### <a name="converter-module"></a><span data-ttu-id="1b1a8-140">Módulo conversor</span><span class="sxs-lookup"><span data-stu-id="1b1a8-140">Converter module</span></span>

| <span data-ttu-id="1b1a8-141">Entrada</span><span class="sxs-lookup"><span data-stu-id="1b1a8-141">Input</span></span>                    | <span data-ttu-id="1b1a8-142">Processador</span><span class="sxs-lookup"><span data-stu-id="1b1a8-142">Processor</span></span>                              | <span data-ttu-id="1b1a8-143">Saída</span><span class="sxs-lookup"><span data-stu-id="1b1a8-143">Output</span></span>                 | <span data-ttu-id="1b1a8-144">Arquivo de código-fonte</span><span class="sxs-lookup"><span data-stu-id="1b1a8-144">Source File</span></span>            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| <span data-ttu-id="1b1a8-145">Mensagem de dados de temperatura</span><span class="sxs-lookup"><span data-stu-id="1b1a8-145">Temperature data message</span></span> | <span data-ttu-id="1b1a8-146">Análise e criação de uma nova mensagem JSON</span><span class="sxs-lookup"><span data-stu-id="1b1a8-146">Parse and construct a new JSON message</span></span> | <span data-ttu-id="1b1a8-147">Mensagem de JSON de estrutura</span><span class="sxs-lookup"><span data-stu-id="1b1a8-147">Structure JSON message</span></span> | `ConverterModule.java` |

<span data-ttu-id="1b1a8-148">Este é um módulo típico do Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="1b1a8-148">This module is a typical Azure IoT Edge module.</span></span> <span data-ttu-id="1b1a8-149">Ele aceita mensagens de temperatura de outros módulos (um módulo de hardware, ou, nesse caso, nosso módulo Bilitar simulado); e, em seguida, normaliza a mensagem de saudação do temperatura na mensagem JSON tooa estruturado (incluindo acrescentando a ID de mensagem de saudação, definindo a propriedade Olá de se precisamos tootrigger alerta de temperatura Olá e assim por diante).</span><span class="sxs-lookup"><span data-stu-id="1b1a8-149">It accepts temperature messages from other modules (a hardware module, or in this case our simulated BLE module); and then normalizes hello temperature message in tooa structured JSON message (including appending hello message ID, setting hello property of whether we need tootrigger hello temperature alert, and so on).</span></span>

```java
@Override
public void receive(Message message) {
  try {
    JSONObject messageFromBle = new JSONObject(new String(message.getContent()));
    double temperature = messageFromBle.getDouble("temperature");
    Map<String, String> inputProperties = message.getProperties();

    HashMap<String, String> properties = new HashMap<>();
    properties.put("source", inputProperties.get("source"));
    properties.put("macAddress", inputProperties.get("macAddress"));
    properties.put("temperatureAlert", temperature > 30 ? "true" : "false");

    String content = String.format(
        "{ \"deviceId\": \"Intel NUC Gateway\", \"messageId\": %d, \"temperature\": %f }",
        ++this.messageCount, temperature);

    this.publish(new Message(content.getBytes(), properties));
  } catch (Exception ex) {
    ex.printStackTrace();
  }
}
```

### <a name="printer-module"></a><span data-ttu-id="1b1a8-150">Módulo de impressão</span><span class="sxs-lookup"><span data-stu-id="1b1a8-150">Printer module</span></span>

| <span data-ttu-id="1b1a8-151">Entrada</span><span class="sxs-lookup"><span data-stu-id="1b1a8-151">Input</span></span>                          | <span data-ttu-id="1b1a8-152">Processador</span><span class="sxs-lookup"><span data-stu-id="1b1a8-152">Processor</span></span> | <span data-ttu-id="1b1a8-153">Saída</span><span class="sxs-lookup"><span data-stu-id="1b1a8-153">Output</span></span>                     | <span data-ttu-id="1b1a8-154">Arquivo de código-fonte</span><span class="sxs-lookup"><span data-stu-id="1b1a8-154">Source File</span></span>          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| <span data-ttu-id="1b1a8-155">Qualquer mensagem de outros módulos</span><span class="sxs-lookup"><span data-stu-id="1b1a8-155">Any message from other modules</span></span> | <span data-ttu-id="1b1a8-156">N/D</span><span class="sxs-lookup"><span data-stu-id="1b1a8-156">N/A</span></span>       | <span data-ttu-id="1b1a8-157">Olá tooconsole de mensagem de log</span><span class="sxs-lookup"><span data-stu-id="1b1a8-157">Log hello message tooconsole</span></span> | `PrinterModule.java` |

<span data-ttu-id="1b1a8-158">Este é um módulo de simple, auto-explicativos, que gera a janela do terminal Olá recebida mensagens toohello.</span><span class="sxs-lookup"><span data-stu-id="1b1a8-158">This is a simple, self-explanatory, module which outputs hello received messages toohello terminal window.</span></span>

```java
@Override
public void receive(Message message) {
  System.out.println(message.toString());
}
```

### <a name="azure-iot-edge-configuration"></a><span data-ttu-id="1b1a8-159">Configuração do Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="1b1a8-159">Azure IoT Edge configuration</span></span>

<span data-ttu-id="1b1a8-160">a etapa final Olá antes da execução de módulos de saudação é tooconfigure hello Azure IoT borda e conexões de saudação tooestablish entre os módulos.</span><span class="sxs-lookup"><span data-stu-id="1b1a8-160">hello final step before running hello modules is tooconfigure hello Azure IoT Edge and tooestablish hello connections between modules.</span></span>

<span data-ttu-id="1b1a8-161">Primeiro é preciso toodeclare nosso carregador de Java (desde a Azure IoT borda carregadores de dá suporte a idiomas diferentes) que pode ser referenciado por seu `name` nas seções de saudação posteriormente.</span><span class="sxs-lookup"><span data-stu-id="1b1a8-161">First we need toodeclare our Java loader (since Azure IoT Edge supports loaders of different languages) which could be referenced by its `name` in hello sections afterward.</span></span>

```json
"loaders": [{
  "type": "java",
  "name": "java",
  "configuration": {
    "jvm.options": {
      "library.path": "./"
    }
  }
}]
```

<span data-ttu-id="1b1a8-162">Depois que podemos ter declarado nosso carregadores, também precisaremos toodeclare nossos módulos também.</span><span class="sxs-lookup"><span data-stu-id="1b1a8-162">Once we have declared our loaders, we will also need toodeclare our modules as well.</span></span> <span data-ttu-id="1b1a8-163">Carregadores de saudação toodeclaring semelhantes, eles também podem ser referenciados por seus `name` atributo.</span><span class="sxs-lookup"><span data-stu-id="1b1a8-163">Similar toodeclaring hello loaders, they can also be referenced by their `name` attribute.</span></span> <span data-ttu-id="1b1a8-164">Ao declarar um módulo, precisamos de carregador de saudação do toospecify devem usar (que deve ser Olá um definimos antes) e Olá ponto de entrada (deve ser o nome de classe normalizado de saudação do nosso módulo) para cada módulo.</span><span class="sxs-lookup"><span data-stu-id="1b1a8-164">When declaring a module, we need toospecify hello loader it should use (which should be hello one we defined before) and hello entry-point (should be hello normalized class name of our module) for each module.</span></span> <span data-ttu-id="1b1a8-165">Olá `simulated_device` é um módulo nativo incluído no pacote de tempo de execução do hello Azure IoT borda core.</span><span class="sxs-lookup"><span data-stu-id="1b1a8-165">hello `simulated_device` module is a native module which is included in hello Azure IoT Edge core runtime package.</span></span> <span data-ttu-id="1b1a8-166">Você sempre deve incluir `args` em Olá JSON arquivo mesmo se ele for `null`.</span><span class="sxs-lookup"><span data-stu-id="1b1a8-166">You should always include `args` in hello JSON file even if it is `null`.</span></span>

```json
"modules": [
  {
    "name": "simulated_device",
    "loader": {
      "name": "native",
      "entrypoint": {
        "module.path": "simulated_device"
      }
    },
    "args": {
      "macAddress": "01:02:03:03:02:01",
      "messagePeriod": 500
    }
  },
  {
    "name": "converter",
    "loader": {
      "name": "java",
      "entrypoint": {
        "class.name": "com/microsoft/azure/gateway/ConverterModule",
        "class.path": "./ble-converter-1.0-with-deps.jar"
      }
    },
    "args": null
  },
  {
    "name": "print",
    "loader": {
      "name": "java",
      "entrypoint": {
        "class.name": "com/microsoft/azure/gateway/PrinterModule",
        "class.path": "./ble-converter-1.0-with-deps.jar"
      }
    },
    "args": null
  }
]
```

<span data-ttu-id="1b1a8-167">Final de saudação de configuração Olá, estabelecemos conexões hello.</span><span class="sxs-lookup"><span data-stu-id="1b1a8-167">At hello end of hello configuration, we establish hello connections.</span></span> <span data-ttu-id="1b1a8-168">Cada conexão é expressa por `source` e `sink`.</span><span class="sxs-lookup"><span data-stu-id="1b1a8-168">Each connection is expressed by `source` and `sink`.</span></span> <span data-ttu-id="1b1a8-169">Ambas fazem referência a um módulo predefinido.</span><span class="sxs-lookup"><span data-stu-id="1b1a8-169">They should both reference a pre-defined module.</span></span> <span data-ttu-id="1b1a8-170">mensagem de saída de saudação de `source` módulo será encaminhado entrada toohello de `sink` módulo.</span><span class="sxs-lookup"><span data-stu-id="1b1a8-170">hello output message of `source` module will be forwarded toohello input of `sink` module.</span></span>

```json
"links": [
  {
    "source": "simulated_device",
    "sink": "converter"
  },
  {
    "source": "converter",
    "sink": "print"
  }
]
```

## <a name="running-hello-modules"></a><span data-ttu-id="1b1a8-171">Módulos de saudação em execução</span><span class="sxs-lookup"><span data-stu-id="1b1a8-171">Running hello modules</span></span>

<span data-ttu-id="1b1a8-172">Use `mvn package` toobuild tudo em Olá `target/` pasta.</span><span class="sxs-lookup"><span data-stu-id="1b1a8-172">Use `mvn package` toobuild everything into hello `target/` folder.</span></span> <span data-ttu-id="1b1a8-173">`mvn clean package` também é recomendado para uma compilação limpa.</span><span class="sxs-lookup"><span data-stu-id="1b1a8-173">`mvn clean package` is also recommended for a clean build.</span></span>

<span data-ttu-id="1b1a8-174">Use `mvn exec:exec` toorun hello Azure IoT borda e você deve observar que dados de temperatura hello e todas as propriedades de saudação são impressos toohello console a uma taxa fixa.</span><span class="sxs-lookup"><span data-stu-id="1b1a8-174">Use `mvn exec:exec` toorun hello Azure IoT Edge and you should observe that hello temperature data and all hello properties are printed toohello console at a fixed rate.</span></span>

<span data-ttu-id="1b1a8-175">Se você quiser tooterminate Olá aplicativo, pressione `<Enter>` chave.</span><span class="sxs-lookup"><span data-stu-id="1b1a8-175">If you want tooterminate hello application, press `<Enter>` key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1b1a8-176">Não é recomendável toouse Ctrl + C tooterminate Olá IoT borda aplicativos de gateway.</span><span class="sxs-lookup"><span data-stu-id="1b1a8-176">It is not recommended toouse Ctrl + C tooterminate hello IoT Edge gateway application.</span></span> <span data-ttu-id="1b1a8-177">Como isso pode causar Olá tooterminate de processo anormal.</span><span class="sxs-lookup"><span data-stu-id="1b1a8-177">As this may cause hello process tooterminate abnormally.</span></span>

