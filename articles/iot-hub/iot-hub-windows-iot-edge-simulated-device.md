---
title: aaaSimulate um dispositivo com borda de IoT do Azure (Windows) | Microsoft Docs
description: Como toouse Azure IoT Edge no Windows toocreate um dispositivo simulado que envia telemetria por meio de um hub IoT de tooan de gateway de borda de IoT do Azure.
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 6a2aeda0-696a-4732-90e1-595d2e2fadc6
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: andbuc
ms.openlocfilehash: ddbe85eb956e9934e80e2e80e09f77b24cf54856
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-iot-edge-toosend-device-to-cloud-messages-with-a-simulated-device-windows"></a>Usar mensagens de dispositivo para a nuvem do Azure IoT borda toosend com um dispositivo simulado (Windows)

[!INCLUDE [iot-hub-iot-edge-simulated-selector](../../includes/iot-hub-iot-edge-simulated-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-windows](../../includes/iot-hub-iot-edge-install-build-windows.md)]

## <a name="how-toorun-hello-sample"></a>Como toorun Olá exemplo

Olá **build.cmd** script gera a saída no hello **criar** pasta em sua cópia local da saudação **iot borda** repositório. Essa saída inclui módulos de borda IoT quatro Olá usados neste exemplo.

Olá locais de script de compilação a:

* **logger.dll** em Olá **criar\\módulos\\agente\\depurar** pasta.
* **iothub.dll** em Olá **criar\\módulos\\hub IOT\\depurar** pasta.
* **identidade\_map.dll** em Olá **criar\\módulos\\identitymap\\depurar** pasta.
* **simulada\_device.dll** em Olá **criar\\módulos\\simulada\_dispositivo\\depurar** pasta.

Usar estes caminhos para Olá **caminho do módulo** valores conforme Olá arquivo de configurações de JSON a seguir:

Olá simulado\_dispositivo\_nuvem\_carregar\_processo de exemplo usa o arquivo de configuração de JSON Olá caminho tooa como um argumento de linha de comando. Olá seguinte arquivo JSON de exemplo é fornecido no repositório do SDK de saudação em **exemplos\\simulada\_dispositivo\_nuvem\_carregar\_exemplo\\src\\ simulada\_dispositivo\_nuvem\_carregar\_exemplo\_win.json**. Isso funciona de arquivo de configuração como está a menos que você modifique Olá compilar módulos de saudação do script tooplace IoT borda ou amostra executáveis em locais não padrão.

> [!NOTE]
> caminhos de módulo Hello são diretório relativo toohello onde Olá simulado\_dispositivo\_nuvem\_carregar\_sample.exe está localizado. arquivo de configuração de JSON de exemplo Hello padrões toowriting too'deviceCloudUploadGatewaylog.log' no diretório de trabalho atual.

Em um editor de texto, abra o arquivo hello **exemplos\\simulada\_dispositivo\_nuvem\_carregar\_exemplo\\src\\simulada\_dispositivo \_nuvem\_carregar\_win.json** em sua cópia local da saudação **iot borda** repositório. Esse arquivo configura os módulos de borda IoT Olá no gateway do exemplo hello:

* Olá **hub IOT** módulo se conecta tooyour IoT hub. Você configurá-lo de hub IoT do toosend dados tooyour. Especificamente, o conjunto Olá **IoTHubName** toohello o nome do seu hub IoT do valor e defina Olá **IoTHubSuffix** valor muito**devices.net azure**. Saudação de conjunto **transporte** tooone de valor de: **HTTP**, **AMQP**, ou **MQTT**. Atualmente, apenas **HTTP** compartilha uma conexão TCP para todas as mensagens de dispositivo. Se você definir o valor de saudação muito**AMQP**, ou **MQTT**, gateway Olá mantém um separado tooIoT de conexão de TCP Hub para cada dispositivo.
* Olá **mapeamento** módulo mapeia endereços MAC de saudação de suas ids de dispositivo simulado dispositivos tooyour Hub IoT. Verifique se **deviceId** valores correspondência Olá ids de Olá dois dispositivos adicionados tooyour IoT hub e que hello **deviceKey** valores contêm chaves Olá dos dois dispositivos.
* Olá **BLE1** e **BLE2** módulos são dispositivos de saudação simulada. Observe como endereços de MAC de módulo Olá correspondem endereços Olá Olá **mapeamento** módulo.
* Olá **agente** módulo registra o arquivo de tooa de atividade de gateway.
* Olá **caminho do módulo** valores mostrados no exemplo a seguir de saudação são diretório relativo toohello onde Olá simulado\_dispositivo\_nuvem\_carregar\_sample.exe está localizado.
* Olá **links** matriz na parte inferior de saudação do arquivo JSON de saudação conecta Olá **BLE1** e **BLE2** módulos toohello **mapeamento** módulo e hello **mapeamento** módulo toohello **hub IOT** módulo. Ela também garante que todas as mensagens são registradas por Olá **agente** módulo.

```json
{
    "modules" :
    [
      {
        "name": "IotHub",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "..\\..\\..\\modules\\iothub\\Debug\\iothub.dll"
          }
          },
          "args": {
            "IoTHubName": "<<insert here IoTHubName>>",
            "IoTHubSuffix": "<<insert here IoTHubSuffix>>",
            "Transport": "HTTP"
          }
        },
      {
        "name": "mapping",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "..\\..\\..\\modules\\identitymap\\Debug\\identity_map.dll"
          }
          },
          "args": [
            {
              "macAddress": "01:01:01:01:01:01",
              "deviceId": "<<insert here deviceId>>",
              "deviceKey": "<<insert here deviceKey>>"
            },
            {
              "macAddress": "02:02:02:02:02:02",
              "deviceId": "<<insert here deviceId>>",
              "deviceKey": "<<insert here deviceKey>>"
            }
          ]
        },
      {
        "name": "BLE1",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "..\\..\\..\\modules\\simulated_device\\Debug\\simulated_device.dll"
          }
          },
          "args": {
            "macAddress": "01:01:01:01:01:01"
          }
        },
      {
        "name": "BLE2",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "..\\..\\..\\modules\\simulated_device\\Debug\\simulated_device.dll"
          }
          },
          "args": {
            "macAddress": "02:02:02:02:02:02"
          }
        },
      {
        "name": "Logger",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "..\\..\\..\\modules\\logger\\Debug\\logger.dll"
          }
        },
        "args": {
          "filename": "deviceCloudUploadGatewaylog.log"
        }
      }
    ],
    "links" : [
        { "source" : "*", "sink" : "Logger" },
        { "source" : "BLE1", "sink" : "mapping" },
        { "source" : "BLE2", "sink" : "mapping" },
        { "source" : "mapping", "sink" : "IotHub" }
    ]
}
```

Salvar as alterações de saudação feitas toohello arquivo de configuração.

exemplo de hello toorun:

1. Em um prompt de comando, navegue toohello **criar** pasta em sua cópia local da saudação **iot borda** repositório.
2. Execute Olá comando a seguir:
   
    ```cmd
    samples\simulated_device_cloud_upload\Debug\simulated_device_cloud_upload_sample.exe ..\samples\simulated_device_cloud_upload\src\simulated_device_cloud_upload_win.json
    ```
3. Você pode usar o hello [explorer dispositivo] [ lnk-device-explorer] ou [Gerenciador de Hub IOT] [ lnk-iothub-explorer] ferramenta toomonitor mensagens de saudação que recebe do hub IoT de saudação gateway. Por exemplo, usando o Gerenciador de Hub IOT você pode monitorar mensagens de dispositivo para nuvem usando Olá comando a seguir:

    ```cmd
    iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
    ```

## <a name="next-steps"></a>Próximas etapas

toogain uma compreensão mais avançada de IoT borda e experiência com alguns exemplos de código, visite Olá tutoriais de desenvolvedor e recursos:

* [Enviar mensagens do dispositivo para a nuvem de um dispositivo físico com o IoT Edge][lnk-physical-device]
* [Azure IoT Edge][lnk-iot-edge]

toofurther explorar recursos de saudação do IoT Hub, consulte:

* [Guia do desenvolvedor do Hub IoT][lnk-devguide]
* [Proteger a sua solução de IoT da saudação de plano de fundo para cima][lnk-securing]

<!-- Links -->
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-physical-device]: iot-hub-iot-edge-physical-device.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md