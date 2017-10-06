---
title: "aaaCreate um módulo do Azure IoT borda com Node. js | Microsoft Docs"
description: "Este tutorial mostra como toowrite uma BELA dados conversor usando módulo Olá pacotes mais recentes do Azure IoT borda NPM e Yeoman gerador."
services: iot-hub
author: sushi
manager: timlt
ms.service: iot-hub
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: js
ms.topic: article
ms.date: 06/28/2017
ms.author: sushi
ms.openlocfilehash: d3e696b5a310377ffb8e99998ff0714bf7c0bb41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-iot-edge-module-with-nodejs"></a>Criar um módulo do Azure IoT Edge com o Node.js

Este tutorial mostra como toocreate um módulo de Azure IoT borda em JS.

Neste tutorial, nós o conduziremos por meio da configuração do ambiente e como toowrite uma [Bilitar](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) módulo de conversor de dados usando hello mais recente do Azure IoT borda NPM pacotes.

## <a name="prerequisites"></a>Pré-requisitos

Nesta seção, você configura o ambiente para o desenvolvimento de módulos do IoT Edge. Aplica-se tooboth *Windows de 64 bits* e *Linux de 64 bits (Ubuntu) 14 +* sistemas operacionais.

saudação de software a seguir é necessária:
* [Cliente Git](https://git-scm.com/downloads).
* [Node LTS](https://nodejs.org).
* `npm install -g yo`.
* `npm install -g generator-az-iot-gw-module`

## <a name="architecture"></a>Arquitetura

plataforma de Azure IoT borda Olá muito adota Olá [arquitetura Von Neumann](https://en.wikipedia.org/wiki/Von_Neumann_architecture). Arquitetura do Azure IoT borda Olá toda o que significa é um sistema que processa a entrada e produz a saída. e cada módulo individual também é um pequeno subsistema de entrada e saída. Neste tutorial, apresentamos Olá dois módulos a seguir:

1. Um módulo que recebe um sinal [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) simulado e converte-o em uma mensagem [JSON](https://en.wikipedia.org/wiki/JSON) formatada.
2. Um módulo que imprime Olá recebida [JSON](https://en.wikipedia.org/wiki/JSON) mensagem.

Olá imagem a seguir exibe tooend Olá final típico fluxo de dados para este projeto:

![Fluxo de dados entre três módulos](media/iot-hub-iot-edge-create-module/dataflow.png "Entrada: módulo BLE simulado; Processador: módulo conversor; Saída: módulo de impressão")

## <a name="set-up-hello-environment"></a>Configurar o ambiente de saudação
Abaixo mostramos como tooquickly configurar o ambiente toostart toowrite primeiro módulo conversor Bilitar com JS.

### <a name="create-module-project"></a>Criar projeto de módulo
1. Abra uma janela de linha de comando e execute `yo az-iot-gw-module`.
2. Siga as etapas de saudação na inicialização do hello tela toofinish saudação do seu projeto de módulo.

### <a name="project-structure"></a>Estrutura do projeto
Um projeto de módulo JS consiste Olá componentes a seguir:

`modules`-Olá personalizado arquivos de origem do módulo JS. Substituir saudação padrão `sensor.js` e `printer.js` com seus próprios arquivos de módulo.

`app.js`-instância de borda Olá do toostart de arquivo de entrada hello.

`gw.config.json`-Olá configuração arquivo toocustomize Olá módulos toobe carregado pela borda.

`package.json`-Olá informações de metadados de projeto de módulo.

`README.md`-Olá documentação básica para o projeto de módulo.


### <a name="package-file"></a>Arquivo de pacote

Isso `package.json` declara todas as informações de metadados de Olá necessárias a um projeto de módulo que inclui Olá dependências de nome, versão, entrada, scripts, tempo de execução e desenvolvimento.

Seguindo o trecho de código mostra como tooconfigure para conversor Bilitar exemplo de projeto.
```json
{
  "name": "converter",
  "version": "1.0.0",
  "description": "BLE data converter sample for Azure IoT Edge.",
  "repository": {
    "type": "git",
    "url": "https://github.com/Azure-Samples/iot-edge-samples"
  },
  "main": "app.js",
  "scripts": {
    "start": "node app.js"
  },
  "author": "Microsoft Corporation",
  "license": "MIT",
  "dependencies": {
  },
  "devDependencies": {
    "azure-iot-gateway": "~1.1.3"
  }
}
```


### <a name="entry-file"></a>Arquivo de entrada
Olá `app.js` define Olá maneira tooinitialize Olá borda instância. Aqui não precisamos toomake qualquer alteração.

```javascript
(function() {
  'use strict';

  const Gateway = require('azure-iot-gateway');
  let config_path = './gw.config.json';

  // node app.js
  if (process.argv.length < 2) {
    throw 'Calling pattern should be node app.js.';
  }

  const gw = new Gateway(config_path);
  gw.run();
})();
```

### <a name="interface-of-module"></a>Interface do módulo
É possível tratar um módulo do Azure IoT Edge como um processador de dados cujo trabalho é: receber a entrada, processá-la e produzir uma saída.

Olá entrada pode ser dados de hardware (como um detector de movimento), uma mensagem de outros módulos ou qualquer outro (como um número aleatório gerado periodicamente por um timer).

saída de Hello seja a entrada de toohello semelhante, pode ativar o comportamento de hardware (como Olá piscando LED), módulos de tooother uma mensagem ou nada (como o console de impressão toohello).

Os módulos se comunicam usando o objeto `message`. Olá **conteúdo** de um `message` é uma matriz de bytes que é capaz de representar qualquer tipo de dados que você deseja. **Propriedades** também estão disponíveis no hello `message` e são simplesmente um mapeamento de cadeia de caracteres de cadeia de caracteres. Você pode pensar **propriedades** como cabeçalhos de saudação em uma solicitação HTTP ou Olá metadados de um arquivo.

Em ordem toodevelop um módulo de Azure IoT borda JS, é necessário toocreate um novo objeto de módulo que implementa os métodos de saudação necessário `receive()`. Neste ponto, você também pode escolher tooimplement Olá opcional `create()` ou `start()`, ou `destroy()` métodos também. saudação de trecho de código a seguir mostra que Olá a estrutura do objeto de módulo JS.

```javascript
'use strict';

module.exports = {
  broker: null,
  configuration: null,

  create: function (broker, configuration) {
    // Default implementation.
    this.broker = broker;
    this.configuration = configuration;

    return true;
  },

  start: function () {
    // Produce
  },

  receive: function (message) {
    // Consume
  },

  destroy: function () {
  }
};
```

### <a name="converter-module"></a>Módulo conversor
| Entrada                    | Processador                              | Saída                 | Arquivo de código-fonte            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| Mensagem de dados de temperatura | Análise e criação de uma nova mensagem JSON | Mensagem de JSON de estrutura | `converter.js` |

Este é um módulo típico do Azure IoT Edge. Ele aceita mensagens de temperatura de outros módulos (um módulo de hardware, ou, nesse caso, nosso módulo Bilitar simulado); e, em seguida, normaliza a mensagem de saudação do temperatura na mensagem JSON tooa estruturado (incluindo acrescentando a ID de mensagem de saudação, definindo a propriedade Olá de se precisamos tootrigger alerta de temperatura Olá e assim por diante).

```javascript
receive: function (message) {
  // Initialize hello messageCount in global object at first time.
  if (!global.messageCount) {
    global.messageCount = 0;
  }

  // Read hello content and properties objects from message.
  let rawContent = JSON.parse(Buffer.from(message.content).toString('utf8'));
  let rawProperties = message.properties;

  // Generate new properties object.
  let newProperties = {
    source: rawProperties.source,
    macAddress: rawProperties.macAddress,
    temperatureAlert: rawContent.temperature > 30 ? 'true' : 'false'
  };

  // Generate new content object.
  let newContent = {
    deviceId: 'Intel NUC Gateway',
    messageId: ++global.messageCount,
    temperature: rawContent.temperature
  };

  // Publish hello new message toobroker.
  this.broker.publish(
    {
      properties: newProperties,
      content: new Uint8Array(Buffer.from(JSON.stringify(newContent), 'utf8'))
    }
  );
},
```

### <a name="printer-module"></a>Módulo de impressão
| Entrada                          | Processador | Saída                     | Arquivo de código-fonte          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| Qualquer mensagem de outros módulos | N/D       | Olá tooconsole de mensagem de log | `printer.js` |

Esse módulo é simples, auto-explicativos, que gera a janela do terminal de toohello Olá recebida mensagens (propriedade, conteúdo).

```javascript
receive: function (message) {
  let properties = JSON.stringify(message.properties);
  let content = Buffer.from(message.content).toString('utf8');

  console.log(`printer.receive.properties - ${properties}`);
  console.log(`printer.receive.content - ${content}\n`);
}
```

### <a name="configuration"></a>Configuração
a etapa final Olá antes da execução de módulos de saudação é tooconfigure hello Azure IoT borda e conexões de saudação tooestablish entre os módulos.

Primeiro, precisamos toodeclare nosso `node` carregador (desde a Azure IoT borda carregadores de dá suporte a idiomas diferentes) que pode ser referenciado por seu `name` nas seções de saudação posteriormente.

```json
"loaders": [
  {
    "type": "node",
    "name": "node"
  }
]
```

Depois que podemos ter declarado nosso carregadores, é preciso também toodeclare nosso módulos também. Carregadores de saudação toodeclaring semelhantes, eles também podem ser referenciados por seus `name` atributo. Ao declarar um módulo, precisamos de carregador de saudação do toospecify devem usar (que deve ser Olá um definimos antes) e Olá ponto de entrada (deve ser o nome de classe normalizado de saudação do nosso módulo) para cada módulo. Olá `simulated_device` é um módulo nativo incluído no pacote de tempo de execução do hello Azure IoT borda core. Incluir `args` em Olá JSON arquivo mesmo se ele for `null`.

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
      "name": "node",
      "entrypoint": {
        "main.path": "modules/converter.js"
      }
    },
    "args": null
  },
  {
    "name": "printer",
    "loader": {
      "name": "node",
      "entrypoint": {
        "main.path": "modules/printer.js"
      }
    },
    "args": null
  }
]
```

Final de saudação de configuração Olá, estabelecemos conexões hello. Cada conexão é expressa por `source` e `sink`. Ambas fazem referência a um módulo predefinido. mensagem de saída de saudação de `source` módulo é encaminhado a entrada de toohello de `sink` módulo.

```json
"links": [
  {
    "source": "simulated_device",
    "sink": "converter"
  },
  {
    "source": "converter",
    "sink": "printer"
  }
]
```

## <a name="running-hello-modules"></a>Módulos de saudação em execução
1. `npm install`
2. `npm start`

Se você quiser tooterminate Olá aplicativo, pressione `<Enter>` chave.

> [!IMPORTANT]
> Não é recomendável toouse Ctrl + C tooterminate Olá IoT borda aplicativo. Como dessa maneira pode causar Olá tooterminate de processo anormal.
