---
title: "Dispositivo simulado e Gateway do IoT do Azure - Lição 3: executar aplicativo de exemplo| Microsoft Docs"
description: Executar um aplicativo de exemplo do dispositivo simulado para enviar dados de temperatura para o Hub IoT
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: dados para a nuvem
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 5d051d99-9749-4150-b3c8-573b0bda9c52
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 7df2d730c38a9f715e0fd57b4d436724a5727760
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-and-run-a-simulated-device-sample-app"></a>Configurar e executar um aplicativo de exemplo do dispositivo simulado

## <a name="what-you-will-do"></a>O que você fará

- Clone o repositório de exemplo.
- Use a CLI do Azure para obter as informações de dispositivo lógico e do seu Hub IoT para o aplicativo de exemplo do dispositivo simulado. Configure e execute o aplicativo de exemplo do dispositivo simulado.

Se você tiver problemas, procure as soluções na [página de solução de problemas](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>O que você aprenderá

Neste artigo, você aprenderá:

- Como configurar e executar o aplicativo de exemplo do dispositivo simulado.

## <a name="what-you-need"></a>O que você precisa

Você deve ter concluído com sucesso

- [Criar um Hub IoT e registrar seu dispositivo](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)

## <a name="clone-the-sample-repository-to-the-host-computer"></a>Clonar o repositório de exemplo para o computador host

Para clonar o repositório de exemplo, siga estas etapas no computador host:

1. Abra um Prompt de Comando no Windows ou um terminal no macOS ou Ubuntu.
2. Execute os seguintes comandos:

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="configure-the-simulated-device-and-your-nuc"></a>Configurar o dispositivo simulado e sua NUC

1. Abra o arquivo de configuração `config.json` no Visual Studio Code executando o seguinte comando:

   ```bash
   code config.json
   ```

2. Substitua `"has_sensortag": true` por `"has_sensortag": false`

   ![Configurar que você não tem um dispositivo de TI SensorTag](media/iot-hub-gateway-kit-lessons/lesson3/config_no_sensortag.png)

3. Inicialize o arquivo de configuração executando os seguintes comandos:

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

4. Abra `config-gateway.json` no Visual Studio Code executando o seguinte comando:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

5. Localize a seguinte linha de código e substitua `[device hostname or IP address]` pelo nome de host ou endereço IP da NUC da Intel.
   ![instantâneo do gateway de configuração](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)

## <a name="get-the-connection-string-of-your-iot-hub-logical-device"></a>Obter a cadeia de conexão do dispositivo lógico de Hub IoT

Para obter a cadeia de conexão do Hub IoT do Azure do dispositivo lógico, execute o seguinte comando no computador host:

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

`{IoT hub name}` é o nome do hub IoT usado. Use o gateway IoT como o valor de `{resource group name}` e use mydevice como o valor de `{device id}` se você não tiver alterado o valor na Lição 2.

## <a name="configure-the-simulated-device-cloud-upload-sample-application"></a>Configurar o aplicativo de exemplo de upload de nuvem de dispositivo simulado

Para configurar e executar o aplicativo de exemplo de upload de nuvem de dispositivo simulado, siga estas etapas no computador host:

1. Abra `config-sensortag.json` no Visual Studio Code executando o seguinte comando:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![instantâneo da configuração da sensortag](media/iot-hub-gateway-kit-lessons/lesson3/config_simulated_device.png)

2. Faça as seguintes substituições no código:
   - Substitua `[IoT hub name]` pelo nome do Hub IoT.
   - Substitua `[IoT device connection string]` pela cadeia de conexão do dispositivo lógico do Hub IoT.

3. Execute o aplicativo.

   Implantar e executar o aplicativo executando o seguinte comando:

   ```bash
   gulp run
   ```

## <a name="verify-the-sample-application-works"></a>Verificar se o aplicativo de exemplo funciona

Você verá agora uma saída semelhante à mostrada a seguir:

![saída do aplicativo de exemplo de dispositivo simulado](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_simudev.png)

O aplicativo envia dados de temperatura ao seu Hub IoT, o que dura 40 segundos.

## <a name="summary"></a>Resumo

Você configurou e executou com êxito o aplicativo de exemplo de upload de nuvem de dispositivo simulado que envia dados ao seu Hub IoT com dispositivo simulado.

## <a name="next-steps"></a>Próximas etapas
[Ler mensagens de seu Hub IoT](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)