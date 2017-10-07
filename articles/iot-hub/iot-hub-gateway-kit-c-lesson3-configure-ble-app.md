---
title: "Dispositivo SensorTag e Gateway do IoT do Azure - Lição 3: executar aplicativo de exemplo| Microsoft Docs"
description: Execute uma Bilitar de tooreceive de aplicativo de exemplo de dados de SensorTag Bilitar em seu hub IoT.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: bilitar aplicativo, aplicativo de monitor de sensor, coleta de dados de sensor, dados de sensores, toocloud de dados do sensor
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: b33e53a1-1df7-4412-ade1-45185aec5bef
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4a8acdeadd402ffc82d3b766e1ec03a77ddcebb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-run-a-ble-sample-application"></a>Configurar e executar um aplicativo de exemplo BLE

## <a name="what-you-will-do"></a>O que você fará

- Repositório de exemplo de saudação do clone. 
- Configure a conectividade de saudação entre SensorTag e NUC da Intel. 
- Use Olá CLI do Azure tooget seu hub IoT e SensorTag informações para um aplicativo de exemplo Bilitar (Bluetooth baixo consumo de energia). Configurar e executar o aplicativo de exemplo hello var. 

Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>O que você aprenderá

Neste artigo, você aprenderá:

- Como tooconfigure e execução hello Bilitar aplicativo de exemplo.

## <a name="what-you-need"></a>O que você precisa

Você deve ter concluído com sucesso

- [Criar um Hub IoT e registrar o SensorTag](iot-hub-gateway-kit-c-lesson2-register-device.md)

## <a name="clone-hello-sample-repository-toohello-host-computer"></a>Computador de host do clone Olá exemplo repositório toohello

repositório de exemplo hello tooclone, siga estas etapas no computador de host hello:

1. Abra uma janela de Prompt de comando no Windows ou um terminal no macOS ou Ubuntu.
2. Execute Olá comandos a seguir:

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="set-up-hello-connectivity-between-sensortag-and-intel-nuc"></a>Configurar a conectividade de saudação entre SensorTag e NUC Intel

tooset conectividade hello, siga estas etapas no computador de host hello:

1. Inicialize o arquivo de configuração de saudação executando Olá comandos a seguir:

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

2. Abra `config-gateway.json` no código do Visual Studio executando Olá comando a seguir:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

3. Olá a seguinte linha de código de localizar e substituir `[device hostname or IP address]` com nome de host ou endereço IP de saudação do NUC Intel.
   ![instantâneo do gateway de configuração](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)

4. Instale ferramentas de auxílio no Intel NUC executando Olá comando a seguir:

   ```bash
   gulp install-tools
   ```

5. Ative SensorTag pressionando o botão liga / desliga Olá Olá figura abaixo e Olá que LED verde deve piscar.

   ![ativar Sensor Tag](media/iot-hub-gateway-kit-lessons/lesson3/turn on_off sensortag.jpg)

6. Verificar dispositivos SensorTag executando Olá comandos a seguir:

   ```bash
   gulp discover-sensortag
   ```

7. Testar a conectividade de saudação entre hello SensorTag e Intel NUC executando Olá comando a seguir:

   ```bash
   gulp test-connectivity --mac {mac address}
   ```

   Substituir `{mac address}` com endereço MAC que você obteve na etapa anterior de saudação do hello.

## <a name="get-hello-connection-string-of-sensortag"></a>Obter cadeia de caracteres de conexão de saudação do SensorTag

Olá tooget cadeia de conexão de hub IoT do Azure de SensorTag, execute Olá comando no computador de host Olá a seguir:

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

`{IoT hub name}`é o nome do hub IoT Olá que você usou. Usar gateway iot como valor de saudação do `{resource group name}` e usar meudispositivo como valor de saudação do `{device id}` se você não alterar o valor de saudação na lição 2.

## <a name="configure-hello-ble-sample-application"></a>Configurar o aplicativo de exemplo hello Bilitar

tooconfigure e execução hello aplicativo de exemplo Bilitar, siga estas etapas no computador de host hello:

1. Abra `config-sensortag.json` no código do Visual Studio executando Olá comando a seguir:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![instantâneo da configuração da sensortag](media/iot-hub-gateway-kit-lessons/lesson3/config_sensortag.png)

2. Verifique Olá substituições no código Olá a seguir:
   - Substituir `[IoT hub name]` com o nome do hub IoT Olá que você usou.
   - Substituir `[IoT device connection string]` com a cadeia de caracteres de conexão de saudação do SensorTag que você obteve.
   - Substituir `[device_mac_address]` com hello endereço MAC de saudação SensorTag obtido.

3. Execute o aplicativo de exemplo hello var.

   Olá toorun aplicativo de exemplo Bilitar, siga estas etapas no computador de host hello:

   1. Ative a SensorTag.

   2. Implantar e executar o aplicativo de exemplo hello Bilitar em NUC Intel executando Olá comando a seguir:
   
      ```bash
      gulp run
      ```

## <a name="verify-that-hello-ble-sample-application-works"></a>Verifique se o aplicativo de exemplo hello Bilitar funciona

Agora, você verá uma saída semelhante Olá seguinte:

![Saída do aplicativo de exemplo BLE](media/iot-hub-gateway-kit-lessons/lesson3/BLE_running.png)

aplicativo de exemplo Hello mantém a coleta de dados de temperatura e enviou tooyour IoT hub. aplicativo de exemplo Hello encerra automaticamente após o envio de 40 segundos.

## <a name="summary"></a>Resumo

Você com êxito configurar conectividade Olá entre SensorTag e NUC Intel e executar um aplicativo de exemplo Bilitar que coleta e envia dados de SensorTag tooyour IoT hub. Você está pronto toolearn como tooverify que recebeu o hub IoT Olá dados.

## <a name="next-steps"></a>Próximas etapas
[Ler mensagens de seu Hub IoT](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)