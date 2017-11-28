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
# <a name="create-an-azure-iot-edge-module-with-nodejs"></a><span data-ttu-id="4ac5f-103">Criar um módulo do Azure IoT Edge com o Node.js</span><span class="sxs-lookup"><span data-stu-id="4ac5f-103">Create an Azure IoT Edge Module with Node.js</span></span>

<span data-ttu-id="4ac5f-104">Este tutorial mostra como toocreate um módulo de Azure IoT borda em JS.</span><span class="sxs-lookup"><span data-stu-id="4ac5f-104">This tutorial showcases how toocreate a module for Azure IoT Edge in JS.</span></span>

<span data-ttu-id="4ac5f-105">Neste tutorial, nós o conduziremos por meio da configuração do ambiente e como toowrite uma [Bilitar](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) módulo de conversor de dados usando hello mais recente do Azure IoT borda NPM pacotes.</span><span class="sxs-lookup"><span data-stu-id="4ac5f-105">In this tutorial, we walk through environment setup and how toowrite a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using hello latest Azure IoT Edge NPM packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4ac5f-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4ac5f-106">Prerequisites</span></span>

<span data-ttu-id="4ac5f-107">Nesta seção, você configura o ambiente para o desenvolvimento de módulos do IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="4ac5f-107">In this section, you set up your environment for IoT Edge module development.</span></span> <span data-ttu-id="4ac5f-108">Aplica-se tooboth *Windows de 64 bits* e *Linux de 64 bits (Ubuntu) 14 +* sistemas operacionais.</span><span class="sxs-lookup"><span data-stu-id="4ac5f-108">It applies tooboth *64-bit Windows* and *64-bit Linux (Ubuntu 14+)* operating systems.</span></span>

<span data-ttu-id="4ac5f-109">saudação de software a seguir é necessária:</span><span class="sxs-lookup"><span data-stu-id="4ac5f-109">hello following software is required:</span></span>
* <span data-ttu-id="4ac5f-110">[Cliente Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="4ac5f-110">[Git Client](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="4ac5f-111">[Node LTS](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="4ac5f-111">[Node LTS](https://nodejs.org).</span></span>
* <span data-ttu-id="4ac5f-112">`npm install -g yo`.</span><span class="sxs-lookup"><span data-stu-id="4ac5f-112">`npm install -g yo`.</span></span>
* `npm install -g generator-az-iot-gw-module`

## <a name="architecture"></a><span data-ttu-id="4ac5f-113">Arquitetura</span><span class="sxs-lookup"><span data-stu-id="4ac5f-113">Architecture</span></span>

<span data-ttu-id="4ac5f-114">plataforma de Azure IoT borda Olá muito adota Olá [arquitetura Von Neumann](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span><span class="sxs-lookup"><span data-stu-id="4ac5f-114">hello Azure IoT Edge platform heavily adopts hello [Von Neumann architecture](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span></span> <span data-ttu-id="4ac5f-115">Arquitetura do Azure IoT borda Olá toda o que significa é um sistema que processa a entrada e produz a saída. e cada módulo individual também é um pequeno subsistema de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="4ac5f-115">Which means that hello entire Azure IoT Edge architecture is a system that processes input and produces output; and that each individual module is also a tiny input-output subsystem.</span></span> <span data-ttu-id="4ac5f-116">Neste tutorial, apresentamos Olá dois módulos a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ac5f-116">In this tutorial, we introduce hello following two modules:</span></span>

1. <span data-ttu-id="4ac5f-117">Um módulo que recebe um sinal [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) simulado e converte-o em uma mensagem [JSON](https://en.wikipedia.org/wiki/JSON) formatada.</span><span class="sxs-lookup"><span data-stu-id="4ac5f-117">A module that receives a simulated [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) signal and converts it into a formatted [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>
2. <span data-ttu-id="4ac5f-118">Um módulo que imprime Olá recebida [JSON](https://en.wikipedia.org/wiki/JSON) mensagem.</span><span class="sxs-lookup"><span data-stu-id="4ac5f-118">A module that prints hello received [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>

<span data-ttu-id="4ac5f-119">Olá imagem a seguir exibe tooend Olá final típico fluxo de dados para este projeto:</span><span class="sxs-lookup"><span data-stu-id="4ac5f-119">hello following image displays hello typical end tooend dataflow for this project:</span></span>

<span data-ttu-id="4ac5f-120">![Fluxo de dados entre três módulos](media/iot-hub-iot-edge-create-module/dataflow.png "Entrada: módulo BLE simulado; Processador: módulo conversor; Saída: módulo de impressão")</span><span class="sxs-lookup"><span data-stu-id="4ac5f-120">![Dataflow between three modules](media/iot-hub-iot-edge-create-module/dataflow.png "Input: Simulated BLE Module; Processor: Converter Module; Output: Printer Module")</span></span>

## <a name="set-up-hello-environment"></a><span data-ttu-id="4ac5f-121">Configurar o ambiente de saudação</span><span class="sxs-lookup"><span data-stu-id="4ac5f-121">Set up hello environment</span></span>
<span data-ttu-id="4ac5f-122">Abaixo mostramos como tooquickly configurar o ambiente toostart toowrite primeiro módulo conversor Bilitar com JS.</span><span class="sxs-lookup"><span data-stu-id="4ac5f-122">Below we show you how tooquickly set up environment toostart toowrite your first BLE converter module with JS.</span></span>

### <a name="create-module-project"></a><span data-ttu-id="4ac5f-123">Criar projeto de módulo</span><span class="sxs-lookup"><span data-stu-id="4ac5f-123">Create module project</span></span>
1. <span data-ttu-id="4ac5f-124">Abra uma janela de linha de comando e execute `yo az-iot-gw-module`.</span><span class="sxs-lookup"><span data-stu-id="4ac5f-124">Open a command-line window, run `yo az-iot-gw-module`.</span></span>
2. <span data-ttu-id="4ac5f-125">Siga as etapas de saudação na inicialização do hello tela toofinish saudação do seu projeto de módulo.</span><span class="sxs-lookup"><span data-stu-id="4ac5f-125">Follow hello steps on hello screen toofinish hello initialization of your module project.</span></span>

### <a name="project-structure"></a><span data-ttu-id="4ac5f-126">Estrutura do projeto</span><span class="sxs-lookup"><span data-stu-id="4ac5f-126">Project structure</span></span>
<span data-ttu-id="4ac5f-127">Um projeto de módulo JS consiste Olá componentes a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ac5f-127">A JS module project consists of hello following components:</span></span>

<span data-ttu-id="4ac5f-128">`modules`-Olá personalizado arquivos de origem do módulo JS.</span><span class="sxs-lookup"><span data-stu-id="4ac5f-128">`modules` - hello customized JS module source files.</span></span> <span data-ttu-id="4ac5f-129">Substituir saudação padrão `sensor.js` e `printer.js` com seus próprios arquivos de módulo.</span><span class="sxs-lookup"><span data-stu-id="4ac5f-129">Replace hello default `sensor.js` and `printer.js` with your own module files.</span></span>

<span data-ttu-id="4ac5f-130">`app.js`-instância de borda Olá do toostart de arquivo de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="4ac5f-130">`app.js` - hello entry file toostart hello Edge instance.</span></span>

<span data-ttu-id="4ac5f-131">`gw.config.json`-Olá configuração arquivo toocustomize Olá módulos toobe carregado pela borda.</span><span class="sxs-lookup"><span data-stu-id="4ac5f-131">`gw.config.json` - hello configuration file toocustomize hello modules toobe loaded by Edge.</span></span>

<span data-ttu-id="4ac5f-132">`package.json`-Olá informações de metadados de projeto de módulo.</span><span class="sxs-lookup"><span data-stu-id="4ac5f-132">`package.json` - hello metadata information for module project.</span></span>

<span data-ttu-id="4ac5f-133">`README.md`-Olá documentação básica para o projeto de módulo.</span><span class="sxs-lookup"><span data-stu-id="4ac5f-133">`README.md` - hello basic documentation for module project.</span></span>


### <a name="package-file"></a><span data-ttu-id="4ac5f-134">Arquivo de pacote</span><span class="sxs-lookup"><span data-stu-id="4ac5f-134">Package file</span></span>

<span data-ttu-id="4ac5f-135">Isso `package.json` declara todas as informações de metadados de Olá necessárias a um projeto de módulo que inclui Olá dependências de nome, versão, entrada, scripts, tempo de execução e desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="4ac5f-135">This `package.json` declares all hello metadata information needed by a module project that includes hello name, version, entry, scripts, runtime, and development dependencies.</span></span>

<span data-ttu-id="4ac5f-136">Seguindo o trecho de código mostra como tooconfigure para conversor Bilitar exemplo de projeto.</span><span class="sxs-lookup"><span data-stu-id="4ac5f-136">Following code snippet shows how tooconfigure for BLE converter sample project.</span></span>
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


### <a name="entry-file"></a><span data-ttu-id="4ac5f-137">Arquivo de entrada</span><span class="sxs-lookup"><span data-stu-id="4ac5f-137">Entry file</span></span>
<span data-ttu-id="4ac5f-138">Olá `app.js` define Olá maneira tooinitialize Olá borda instância.</span><span class="sxs-lookup"><span data-stu-id="4ac5f-138">hello `app.js` defines hello way tooinitialize hello edge instance.</span></span> <span data-ttu-id="4ac5f-139">Aqui não precisamos toomake qualquer alteração.</span><span class="sxs-lookup"><span data-stu-id="4ac5f-139">Here we don't need toomake any change.</span></span>

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

### <a name="interface-of-module"></a><span data-ttu-id="4ac5f-140">Interface do módulo</span><span class="sxs-lookup"><span data-stu-id="4ac5f-140">Interface of module</span></span>
<span data-ttu-id="4ac5f-141">É possível tratar um módulo do Azure IoT Edge como um processador de dados cujo trabalho é: receber a entrada, processá-la e produzir uma saída.</span><span class="sxs-lookup"><span data-stu-id="4ac5f-141">You can treat an Azure IoT Edge module as a data processor whose job is to: receive input, process it, and produce output.</span></span>

<span data-ttu-id="4ac5f-142">Olá entrada pode ser dados de hardware (como um detector de movimento), uma mensagem de outros módulos ou qualquer outro (como um número aleatório gerado periodicamente por um timer).</span><span class="sxs-lookup"><span data-stu-id="4ac5f-142">hello input might be data from hardware (like a motion detector), a message from other modules, or anything else (like a random number generated periodically by a timer).</span></span>

<span data-ttu-id="4ac5f-143">saída de Hello seja a entrada de toohello semelhante, pode ativar o comportamento de hardware (como Olá piscando LED), módulos de tooother uma mensagem ou nada (como o console de impressão toohello).</span><span class="sxs-lookup"><span data-stu-id="4ac5f-143">hello output is similar toohello input, it could trigger hardware behavior (like hello blinking LED), a message tooother modules, or anything else (like printing toohello console).</span></span>

<span data-ttu-id="4ac5f-144">Os módulos se comunicam usando o objeto `message`.</span><span class="sxs-lookup"><span data-stu-id="4ac5f-144">Modules communicate with each other using `message` object.</span></span> <span data-ttu-id="4ac5f-145">Olá **conteúdo** de um `message` é uma matriz de bytes que é capaz de representar qualquer tipo de dados que você deseja.</span><span class="sxs-lookup"><span data-stu-id="4ac5f-145">hello **content** of a `message` is a byte array that is capable of representing any kind of data you like.</span></span> <span data-ttu-id="4ac5f-146">**Propriedades** também estão disponíveis no hello `message` e são simplesmente um mapeamento de cadeia de caracteres de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="4ac5f-146">**Properties** are also available in hello `message` and are simply a string-to-string mapping.</span></span> <span data-ttu-id="4ac5f-147">Você pode pensar **propriedades** como cabeçalhos de saudação em uma solicitação HTTP ou Olá metadados de um arquivo.</span><span class="sxs-lookup"><span data-stu-id="4ac5f-147">You may think of **properties** as hello headers in an HTTP request, or hello metadata of a file.</span></span>

<span data-ttu-id="4ac5f-148">Em ordem toodevelop um módulo de Azure IoT borda JS, é necessário toocreate um novo objeto de módulo que implementa os métodos de saudação necessário `receive()`.</span><span class="sxs-lookup"><span data-stu-id="4ac5f-148">In order toodevelop an Azure IoT Edge module in JS, you need toocreate a new module object that implements hello required methods `receive()`.</span></span> <span data-ttu-id="4ac5f-149">Neste ponto, você também pode escolher tooimplement Olá opcional `create()` ou `start()`, ou `destroy()` métodos também.</span><span class="sxs-lookup"><span data-stu-id="4ac5f-149">At this point, you may also choose tooimplement hello optional `create()` or `start()`, or `destroy()` methods as well.</span></span> <span data-ttu-id="4ac5f-150">saudação de trecho de código a seguir mostra que Olá a estrutura do objeto de módulo JS.</span><span class="sxs-lookup"><span data-stu-id="4ac5f-150">hello following code snippet shows you hello scaffolding of JS module object.</span></span>

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

### <a name="converter-module"></a><span data-ttu-id="4ac5f-151">Módulo conversor</span><span class="sxs-lookup"><span data-stu-id="4ac5f-151">Converter module</span></span>
| <span data-ttu-id="4ac5f-152">Entrada</span><span class="sxs-lookup"><span data-stu-id="4ac5f-152">Input</span></span>                    | <span data-ttu-id="4ac5f-153">Processador</span><span class="sxs-lookup"><span data-stu-id="4ac5f-153">Processor</span></span>                              | <span data-ttu-id="4ac5f-154">Saída</span><span class="sxs-lookup"><span data-stu-id="4ac5f-154">Output</span></span>                 | <span data-ttu-id="4ac5f-155">Arquivo de código-fonte</span><span class="sxs-lookup"><span data-stu-id="4ac5f-155">Source File</span></span>            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| <span data-ttu-id="4ac5f-156">Mensagem de dados de temperatura</span><span class="sxs-lookup"><span data-stu-id="4ac5f-156">Temperature data message</span></span> | <span data-ttu-id="4ac5f-157">Análise e criação de uma nova mensagem JSON</span><span class="sxs-lookup"><span data-stu-id="4ac5f-157">Parse and construct a new JSON message</span></span> | <span data-ttu-id="4ac5f-158">Mensagem de JSON de estrutura</span><span class="sxs-lookup"><span data-stu-id="4ac5f-158">Structure JSON message</span></span> | `converter.js` |

<span data-ttu-id="4ac5f-159">Este é um módulo típico do Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="4ac5f-159">This module is a typical Azure IoT Edge module.</span></span> <span data-ttu-id="4ac5f-160">Ele aceita mensagens de temperatura de outros módulos (um módulo de hardware, ou, nesse caso, nosso módulo Bilitar simulado); e, em seguida, normaliza a mensagem de saudação do temperatura na mensagem JSON tooa estruturado (incluindo acrescentando a ID de mensagem de saudação, definindo a propriedade Olá de se precisamos tootrigger alerta de temperatura Olá e assim por diante).</span><span class="sxs-lookup"><span data-stu-id="4ac5f-160">It accepts temperature messages from other modules (a hardware module, or in this case our simulated BLE module); and then normalizes hello temperature message in tooa structured JSON message (including appending hello message ID, setting hello property of whether we need tootrigger hello temperature alert, and so on).</span></span>

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

### <a name="printer-module"></a><span data-ttu-id="4ac5f-161">Módulo de impressão</span><span class="sxs-lookup"><span data-stu-id="4ac5f-161">Printer module</span></span>
| <span data-ttu-id="4ac5f-162">Entrada</span><span class="sxs-lookup"><span data-stu-id="4ac5f-162">Input</span></span>                          | <span data-ttu-id="4ac5f-163">Processador</span><span class="sxs-lookup"><span data-stu-id="4ac5f-163">Processor</span></span> | <span data-ttu-id="4ac5f-164">Saída</span><span class="sxs-lookup"><span data-stu-id="4ac5f-164">Output</span></span>                     | <span data-ttu-id="4ac5f-165">Arquivo de código-fonte</span><span class="sxs-lookup"><span data-stu-id="4ac5f-165">Source File</span></span>          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| <span data-ttu-id="4ac5f-166">Qualquer mensagem de outros módulos</span><span class="sxs-lookup"><span data-stu-id="4ac5f-166">Any message from other modules</span></span> | <span data-ttu-id="4ac5f-167">N/D</span><span class="sxs-lookup"><span data-stu-id="4ac5f-167">N/A</span></span>       | <span data-ttu-id="4ac5f-168">Olá tooconsole de mensagem de log</span><span class="sxs-lookup"><span data-stu-id="4ac5f-168">Log hello message tooconsole</span></span> | `printer.js` |

<span data-ttu-id="4ac5f-169">Esse módulo é simples, auto-explicativos, que gera a janela do terminal de toohello Olá recebida mensagens (propriedade, conteúdo).</span><span class="sxs-lookup"><span data-stu-id="4ac5f-169">This module is simple, self-explanatory, which outputs hello received messages(property, content) toohello terminal window.</span></span>

```javascript
receive: function (message) {
  let properties = JSON.stringify(message.properties);
  let content = Buffer.from(message.content).toString('utf8');

  console.log(`printer.receive.properties - ${properties}`);
  console.log(`printer.receive.content - ${content}\n`);
}
```

### <a name="configuration"></a><span data-ttu-id="4ac5f-170">Configuração</span><span class="sxs-lookup"><span data-stu-id="4ac5f-170">Configuration</span></span>
<span data-ttu-id="4ac5f-171">a etapa final Olá antes da execução de módulos de saudação é tooconfigure hello Azure IoT borda e conexões de saudação tooestablish entre os módulos.</span><span class="sxs-lookup"><span data-stu-id="4ac5f-171">hello final step before running hello modules is tooconfigure hello Azure IoT Edge and tooestablish hello connections between modules.</span></span>

<span data-ttu-id="4ac5f-172">Primeiro, precisamos toodeclare nosso `node` carregador (desde a Azure IoT borda carregadores de dá suporte a idiomas diferentes) que pode ser referenciado por seu `name` nas seções de saudação posteriormente.</span><span class="sxs-lookup"><span data-stu-id="4ac5f-172">First we need toodeclare our `node` loader (since Azure IoT Edge supports loaders of different languages) which could be referenced by its `name` in hello sections afterward.</span></span>

```json
"loaders": [
  {
    "type": "node",
    "name": "node"
  }
]
```

<span data-ttu-id="4ac5f-173">Depois que podemos ter declarado nosso carregadores, é preciso também toodeclare nosso módulos também.</span><span class="sxs-lookup"><span data-stu-id="4ac5f-173">Once we have declared our loaders, we also need toodeclare our modules as well.</span></span> <span data-ttu-id="4ac5f-174">Carregadores de saudação toodeclaring semelhantes, eles também podem ser referenciados por seus `name` atributo.</span><span class="sxs-lookup"><span data-stu-id="4ac5f-174">Similar toodeclaring hello loaders, they can also be referenced by their `name` attribute.</span></span> <span data-ttu-id="4ac5f-175">Ao declarar um módulo, precisamos de carregador de saudação do toospecify devem usar (que deve ser Olá um definimos antes) e Olá ponto de entrada (deve ser o nome de classe normalizado de saudação do nosso módulo) para cada módulo.</span><span class="sxs-lookup"><span data-stu-id="4ac5f-175">When declaring a module, we need toospecify hello loader it should use (which should be hello one we defined before) and hello entry-point (should be hello normalized class name of our module) for each module.</span></span> <span data-ttu-id="4ac5f-176">Olá `simulated_device` é um módulo nativo incluído no pacote de tempo de execução do hello Azure IoT borda core.</span><span class="sxs-lookup"><span data-stu-id="4ac5f-176">hello `simulated_device` module is a native module that is included in hello Azure IoT Edge core runtime package.</span></span> <span data-ttu-id="4ac5f-177">Incluir `args` em Olá JSON arquivo mesmo se ele for `null`.</span><span class="sxs-lookup"><span data-stu-id="4ac5f-177">Include `args` in hello JSON file even if it is `null`.</span></span>

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

<span data-ttu-id="4ac5f-178">Final de saudação de configuração Olá, estabelecemos conexões hello.</span><span class="sxs-lookup"><span data-stu-id="4ac5f-178">At hello end of hello configuration, we establish hello connections.</span></span> <span data-ttu-id="4ac5f-179">Cada conexão é expressa por `source` e `sink`.</span><span class="sxs-lookup"><span data-stu-id="4ac5f-179">Each connection is expressed by `source` and `sink`.</span></span> <span data-ttu-id="4ac5f-180">Ambas fazem referência a um módulo predefinido.</span><span class="sxs-lookup"><span data-stu-id="4ac5f-180">They should both reference a pre-defined module.</span></span> <span data-ttu-id="4ac5f-181">mensagem de saída de saudação de `source` módulo é encaminhado a entrada de toohello de `sink` módulo.</span><span class="sxs-lookup"><span data-stu-id="4ac5f-181">hello output message of `source` module is forwarded toohello input of `sink` module.</span></span>

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

## <a name="running-hello-modules"></a><span data-ttu-id="4ac5f-182">Módulos de saudação em execução</span><span class="sxs-lookup"><span data-stu-id="4ac5f-182">Running hello modules</span></span>
1. `npm install`
2. `npm start`

<span data-ttu-id="4ac5f-183">Se você quiser tooterminate Olá aplicativo, pressione `<Enter>` chave.</span><span class="sxs-lookup"><span data-stu-id="4ac5f-183">If you want tooterminate hello application, press `<Enter>` key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4ac5f-184">Não é recomendável toouse Ctrl + C tooterminate Olá IoT borda aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4ac5f-184">It is not recommended toouse Ctrl + C tooterminate hello IoT Edge application.</span></span> <span data-ttu-id="4ac5f-185">Como dessa maneira pode causar Olá tooterminate de processo anormal.</span><span class="sxs-lookup"><span data-stu-id="4ac5f-185">As this way may cause hello process tooterminate abnormally.</span></span>
