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
# <a name="create-an-azure-iot-edge-module-with-java"></a>Como criar um módulo do Azure IoT Edge com Java

Este tutorial mostra como criar um módulo para Azure IoT Edge em Java.

Neste tutorial, vamos percorrer a instalação de ambiente e como toowrite uma [Bilitar](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) módulo de conversor de dados usando hello mais recente do Azure IoT borda Maven pacotes.

## <a name="prerequisites"></a>Pré-requisitos

Nesta seção, você configurará o ambiente para o desenvolvimento do módulo IoT Edge. Aplica-se tooboth *Windows de 64 bits* e *Linux de 64 bits (8 Ubuntu/Debian)* sistemas operacionais.

saudação de software a seguir é necessária:

* [Cliente Git](https://git-scm.com/downloads).
* [**x64** JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
* [Maven](https://maven.apache.org/install.html).

Abra uma linha de comando terminal janela e clone Olá repositório a seguir:

1. `git clone https://github.com/Azure-Samples/iot-edge-samples.git`.
2. `cd iot-edge-samples/java/simulated_ble`

## <a name="overall-architecture"></a>Arquitetura geral

plataforma de Azure IoT borda Olá muito adota Olá [arquitetura Von Neumann](https://en.wikipedia.org/wiki/Von_Neumann_architecture). Arquitetura do Azure IoT borda Olá toda o que significa é um sistema que processa a entrada e produz a saída. e cada módulo individual também é um pequeno subsistema de entrada e saída. Neste tutorial, apresentaremos Olá dois módulos a seguir:

1. Um módulo que recebe um sinal [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) simulado e o converte em uma mensagem com formatação [JSON](https://en.wikipedia.org/wiki/JSON).
2. Um módulo que imprime Olá recebida [JSON](https://en.wikipedia.org/wiki/JSON) mensagem.

Olá imagem a seguir exibe fluxo de dados típicos de ponta a ponta do Olá para este projeto:

![Fluxo de dados entre três módulos](media/iot-hub-iot-edge-create-module/dataflow.png "Entrada: módulo BLE simulado; Processador: módulo conversor; Saída: módulo de impressão")

## <a name="understanding-hello-code"></a>Entendendo o código Olá

### <a name="maven-project-structure"></a>Estrutura do projeto Maven

Como os pacotes de borda do Azure IoT são baseados em Maven, precisamos toocreate uma estrutura de projeto Maven típica, que contém um `pom.xml` arquivo.

Olá POM herda de saudação `com.microsoft.azure.gateway.gateway-module-base` pacote, que declara todas as dependências de saudação necessárias a um projeto de módulo que inclui os binários de tempo de execução de saudação, o caminho do arquivo de configuração de gateway de saudação e o comportamento de execução hello. Isso economiza muito tempo e eliminar Olá necessidade toowrite e reescrever centenas de linhas de código repetidamente.

Precisamos tooupdate o arquivo pom.xml declarando Olá necessário dependências/plug-ins e o nome de saudação do hello toobe de arquivo de configuração usado pelo nosso módulo, conforme mostrado no trecho de código a seguir de saudação.

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

### <a name="basic-understanding-of-an-azure-iot-edge-module"></a>Noções básicas sobre um módulo do Azure IoT Edge

É possível tratar um módulo do Azure IoT Edge como um processador de dados cujo trabalho é: receber a entrada, processá-la e produzir uma saída.

Olá entrada pode ser dados de hardware (como um detector de movimento), uma mensagem de outros módulos ou qualquer outro (como um número aleatório gerado periodicamente por um timer).

saída de Hello seja a entrada de toohello semelhante, pode ativar o comportamento de hardware (como Olá piscando LED), módulos de tooother uma mensagem ou nada (como o console de impressão toohello).

Os módulos comunicam entre si usando classe `com.microsoft.azure.gateway.messaging.Message`. Olá **conteúdo** de um `Message` é uma matriz de bytes que é capaz de representar qualquer tipo de dados que você deseja. **Propriedades** também estão disponíveis no hello `Message` e são simplesmente um mapeamento de cadeia de caracteres de cadeia de caracteres. Você pode pensar **propriedades** como cabeçalhos de saudação em uma solicitação HTTP ou Olá metadados de um arquivo.

Em ordem toodevelop um módulo de borda de IoT do Azure em Java, você precisa toocreate uma nova classe de módulo que herda de `com.microsoft.azure.gateway.core.GatewayModule` e implementar métodos abstratos Olá necessário `receive()` e `destroy()`. Neste ponto, você também pode escolher tooimplement Olá opcional `start()` ou `create()` métodos também. saudação de trecho de código a seguir mostra como tooget iniciada a criação de um módulo de borda de IoT do Azure.

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

### <a name="converter-module"></a>Módulo conversor

| Entrada                    | Processador                              | Saída                 | Arquivo de código-fonte            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| Mensagem de dados de temperatura | Análise e criação de uma nova mensagem JSON | Mensagem de JSON de estrutura | `ConverterModule.java` |

Este é um módulo típico do Azure IoT Edge. Ele aceita mensagens de temperatura de outros módulos (um módulo de hardware, ou, nesse caso, nosso módulo Bilitar simulado); e, em seguida, normaliza a mensagem de saudação do temperatura na mensagem JSON tooa estruturado (incluindo acrescentando a ID de mensagem de saudação, definindo a propriedade Olá de se precisamos tootrigger alerta de temperatura Olá e assim por diante).

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

### <a name="printer-module"></a>Módulo de impressão

| Entrada                          | Processador | Saída                     | Arquivo de código-fonte          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| Qualquer mensagem de outros módulos | N/D       | Olá tooconsole de mensagem de log | `PrinterModule.java` |

Este é um módulo de simple, auto-explicativos, que gera a janela do terminal Olá recebida mensagens toohello.

```java
@Override
public void receive(Message message) {
  System.out.println(message.toString());
}
```

### <a name="azure-iot-edge-configuration"></a>Configuração do Azure IoT Edge

a etapa final Olá antes da execução de módulos de saudação é tooconfigure hello Azure IoT borda e conexões de saudação tooestablish entre os módulos.

Primeiro é preciso toodeclare nosso carregador de Java (desde a Azure IoT borda carregadores de dá suporte a idiomas diferentes) que pode ser referenciado por seu `name` nas seções de saudação posteriormente.

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

Depois que podemos ter declarado nosso carregadores, também precisaremos toodeclare nossos módulos também. Carregadores de saudação toodeclaring semelhantes, eles também podem ser referenciados por seus `name` atributo. Ao declarar um módulo, precisamos de carregador de saudação do toospecify devem usar (que deve ser Olá um definimos antes) e Olá ponto de entrada (deve ser o nome de classe normalizado de saudação do nosso módulo) para cada módulo. Olá `simulated_device` é um módulo nativo incluído no pacote de tempo de execução do hello Azure IoT borda core. Você sempre deve incluir `args` em Olá JSON arquivo mesmo se ele for `null`.

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

Final de saudação de configuração Olá, estabelecemos conexões hello. Cada conexão é expressa por `source` e `sink`. Ambas fazem referência a um módulo predefinido. mensagem de saída de saudação de `source` módulo será encaminhado entrada toohello de `sink` módulo.

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

## <a name="running-hello-modules"></a>Módulos de saudação em execução

Use `mvn package` toobuild tudo em Olá `target/` pasta. `mvn clean package` também é recomendado para uma compilação limpa.

Use `mvn exec:exec` toorun hello Azure IoT borda e você deve observar que dados de temperatura hello e todas as propriedades de saudação são impressos toohello console a uma taxa fixa.

Se você quiser tooterminate Olá aplicativo, pressione `<Enter>` chave.

> [!IMPORTANT]
> Não é recomendável toouse Ctrl + C tooterminate Olá IoT borda aplicativos de gateway. Como isso pode causar Olá tooterminate de processo anormal.

