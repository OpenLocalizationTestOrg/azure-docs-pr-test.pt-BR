---
title: "Dispositivo simulado e Gateway do IoT do Azure - Lição 3: executar aplicativo de exemplo| Microsoft Docs"
description: Executar um dispositivo simulado exemplo aplicativo toosend temperatura tooyour IoT hub de dados
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: dados toocloud
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
ms.openlocfilehash: bc2c97919e95e4e3977a8b6ac75162bf2b5017be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-run-a-simulated-device-sample-app"></a>Configurar e executar um aplicativo de exemplo do dispositivo simulado

## <a name="what-you-will-do"></a>O que você fará

- Repositório de exemplo de saudação do clone.
- Use Olá CLI do Azure tooget seu hub IoT e informações de dispositivo lógico para o aplicativo de exemplo do dispositivo simulado. Configurar e executar o aplicativo de exemplo do dispositivo Olá simulada.

Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>O que você aprenderá

Neste artigo, você aprenderá:

- Como tooconfigure e hello execução simulado aplicativo de exemplo do dispositivo.

## <a name="what-you-need"></a>O que você precisa

Você deve ter concluído com sucesso

- [Criar um Hub IoT e registrar seu dispositivo](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)

## <a name="clone-hello-sample-repository-toohello-host-computer"></a>Computador de host do clone Olá exemplo repositório toohello

repositório de exemplo hello tooclone, siga estas etapas no computador de host hello:

1. Abra um Prompt de Comando no Windows ou um terminal no macOS ou Ubuntu.
2. Execute Olá comandos a seguir:

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="configure-hello-simulated-device-and-your-nuc"></a>Configurar dispositivo simulado hello e seu NUC

1. Arquivo de configuração de saudação abrir `config.json` no código do Visual Studio executando Olá comando a seguir:

   ```bash
   code config.json
   ```

2. Substitua `"has_sensortag": true` por `"has_sensortag": false`

   ![Configurar que você não tem um dispositivo de TI SensorTag](media/iot-hub-gateway-kit-lessons/lesson3/config_no_sensortag.png)

3. Inicialize o arquivo de configuração de saudação executando Olá comandos a seguir:

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

4. Abra `config-gateway.json` no código do Visual Studio executando Olá comando a seguir:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

5. Olá a seguinte linha de código de localizar e substituir `[device hostname or IP address]` com o nome de host ou endereço IP de saudação NUC Intel.
   ![instantâneo do gateway de configuração](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)

## <a name="get-hello-connection-string-of-your-iot-hub-logical-device"></a>Obter cadeia de caracteres de conexão de saudação do seu dispositivo lógico de hub IoT

Olá tooget cadeia de conexão de hub IoT do Azure do seu dispositivo lógico, execute Olá comando no computador de host Olá a seguir:

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

`{IoT hub name}`é o nome do hub IoT Olá que você usou. Usar gateway iot como valor de saudação do `{resource group name}` e usar meudispositivo como valor de saudação do `{device id}` se você não alterar o valor de saudação na lição 2.

## <a name="configure-hello-simulated-device-cloud-upload-sample-application"></a>Configurar o aplicativo de exemplo de carregamento do hello simulado dispositivo nuvem

tooconfigure e na nuvem de dispositivo de execução Olá simulado carregar o aplicativo de exemplo, siga estas etapas no computador de host hello:

1. Abra `config-sensortag.json` no código do Visual Studio executando Olá comando a seguir:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![instantâneo da configuração da sensortag](media/iot-hub-gateway-kit-lessons/lesson3/config_simulated_device.png)

2. Verifique Olá substituições no código Olá a seguir:
   - Substituir `[IoT hub name]` com o nome do hub IoT hello.
   - Substituir `[IoT device connection string]` com a cadeia de caracteres de conexão de saudação do seu dispositivo lógico de hub IoT.

3. Execute o aplicativo hello.

   Implantar e executar o aplicativo hello executando Olá comando a seguir:

   ```bash
   gulp run
   ```

## <a name="verify-hello-sample-application-works"></a>Verifique se o aplicativo de exemplo hello funciona

Agora você deve ver a saída como Olá seguinte:

![saída do aplicativo de exemplo de dispositivo simulado](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_simudev.png)

aplicativo Hello envia hub IoT de temperatura dados tooyour, que tem duração de 40 segundos.

## <a name="summary"></a>Resumo

Você configurou com êxito e execução Olá simulados dispositivo nuvem carregar aplicativo de exemplo que envia o hub de IoT tooyour dados com dispositivo simulado.

## <a name="next-steps"></a>Próximas etapas
[Ler mensagens de seu Hub IoT](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)