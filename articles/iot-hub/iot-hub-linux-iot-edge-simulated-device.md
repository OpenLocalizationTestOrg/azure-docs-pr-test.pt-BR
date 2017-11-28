---
title: aaaSimulate um dispositivo com borda de IoT do Azure (Linux) | Microsoft Docs
description: Como toouse Azure IoT borda em Linux toocreate um dispositivo simulado que envia a telemetria por meio de uma borda de IoT hub do gateway tooan IoT.
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 11e7bf28-ee3d-48d6-a386-eb506c7a31cf
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: andbuc
ms.openlocfilehash: 168fb8eda8671d02c63073bdf36dfcd88b397fe2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-iot-edge-toosend-device-to-cloud-messages-with-a-simulated-device-linux"></a><span data-ttu-id="3fca1-103">Usar mensagens de dispositivo para a nuvem do Azure IoT borda toosend com um dispositivo simulado (Linux)</span><span class="sxs-lookup"><span data-stu-id="3fca1-103">Use Azure IoT Edge toosend device-to-cloud messages with a simulated device (Linux)</span></span>

[!INCLUDE [iot-hub-iot-edge-simulated-selector](../../includes/iot-hub-iot-edge-simulated-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-linux](../../includes/iot-hub-iot-edge-install-build-linux.md)]

## <a name="how-toorun-hello-sample"></a><span data-ttu-id="3fca1-104">Como toorun Olá exemplo</span><span class="sxs-lookup"><span data-stu-id="3fca1-104">How toorun hello sample</span></span>

<span data-ttu-id="3fca1-105">Olá **build.sh** script gera a saída no hello **criar** pasta em sua cópia local da saudação **iot borda** repositório.</span><span class="sxs-lookup"><span data-stu-id="3fca1-105">hello **build.sh** script generates its output in hello **build** folder in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="3fca1-106">Essa saída inclui módulos de borda IoT quatro Olá usados neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="3fca1-106">This output includes hello four IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="3fca1-107">Olá locais de script de compilação a:</span><span class="sxs-lookup"><span data-stu-id="3fca1-107">hello build script places the:</span></span>

* <span data-ttu-id="3fca1-108">**liblogger.SO** em Olá **build/módulos/agente** pasta.</span><span class="sxs-lookup"><span data-stu-id="3fca1-108">**liblogger.so** in hello **build/modules/logger** folder.</span></span>
* <span data-ttu-id="3fca1-109">**libiothub.SO** em Olá **build/módulos/hub IOT** pasta.</span><span class="sxs-lookup"><span data-stu-id="3fca1-109">**libiothub.so** in hello **build/modules/iothub** folder.</span></span>
* <span data-ttu-id="3fca1-110">**lib\_identidade\_map.so** em Olá **build/módulos/identitymap** pasta.</span><span class="sxs-lookup"><span data-stu-id="3fca1-110">**lib\_identity\_map.so** in hello **build/modules/identitymap** folder.</span></span>
* <span data-ttu-id="3fca1-111">**libsimulated\_device.so** em Olá **build/módulos/simulados\_dispositivo** pasta.</span><span class="sxs-lookup"><span data-stu-id="3fca1-111">**libsimulated\_device.so** in hello **build/modules/simulated\_device** folder.</span></span>

<span data-ttu-id="3fca1-112">Usar estes caminhos para Olá **caminho do módulo** valores conforme Olá arquivo de configurações de JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="3fca1-112">Use these paths for hello **module path** values as shown in hello following JSON settings file:</span></span>

<span data-ttu-id="3fca1-113">Olá simulado\_dispositivo\_nuvem\_carregar\_processo de exemplo usa o arquivo de configuração de JSON Olá caminho tooa como um argumento de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="3fca1-113">hello simulated\_device\_cloud\_upload\_sample process takes hello path tooa JSON configuration file as a command-line argument.</span></span> <span data-ttu-id="3fca1-114">Olá seguinte arquivo JSON de exemplo é fornecido no repositório do SDK de saudação em **exemplos\\simulada\_dispositivo\_nuvem\_carregar\_exemplo\\src\\ simulada\_dispositivo\_nuvem\_carregar\_exemplo\_lin.json**.</span><span class="sxs-lookup"><span data-stu-id="3fca1-114">hello following example JSON file is provided in hello SDK repository at **samples\\simulated\_device\_cloud\_upload\_sample\\src\\simulated\_device\_cloud\_upload\_sample\_lin.json**.</span></span> <span data-ttu-id="3fca1-115">Isso funciona de arquivo de configuração como está a menos que você modifique Olá compilar módulos de saudação do script tooplace IoT borda ou amostra executáveis em locais não padrão.</span><span class="sxs-lookup"><span data-stu-id="3fca1-115">This configuration file works as is unless you modify hello build script tooplace hello IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="3fca1-116">caminhos de módulo Olá são relativo toohello diretório de onde você executa Olá simulado\_dispositivo\_nuvem\_carregar\_executável de exemplo, não Olá diretório executável hello.</span><span class="sxs-lookup"><span data-stu-id="3fca1-116">hello module paths are relative toohello directory from where you run hello simulated\_device\_cloud\_upload\_sample executable, not hello directory where hello executable is located.</span></span> <span data-ttu-id="3fca1-117">arquivo de configuração de JSON de exemplo Hello padrões toowriting too'deviceCloudUploadGatewaylog.log' no diretório de trabalho atual.</span><span class="sxs-lookup"><span data-stu-id="3fca1-117">hello sample JSON configuration file defaults toowriting too'deviceCloudUploadGatewaylog.log' in your current working directory.</span></span>

<span data-ttu-id="3fca1-118">Em um editor de texto, abra o arquivo hello **exemplos/simulados\_dispositivo\_nuvem\_carregar\_exemplo/src/simulados\_dispositivo\_nuvem\_carregar\_lin.json** em sua cópia local da saudação **iot borda** repositório.</span><span class="sxs-lookup"><span data-stu-id="3fca1-118">In a text editor, open hello file **samples/simulated\_device\_cloud\_upload\_sample/src/simulated\_device\_cloud\_upload\_lin.json** in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="3fca1-119">Esse arquivo configura os módulos de borda IoT Olá no gateway do exemplo hello:</span><span class="sxs-lookup"><span data-stu-id="3fca1-119">This file configures hello IoT Edge modules in hello sample gateway:</span></span>

* <span data-ttu-id="3fca1-120">Olá **hub IOT** módulo se conecta tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="3fca1-120">hello **IoTHub** module connects tooyour IoT hub.</span></span> <span data-ttu-id="3fca1-121">Você configurá-lo de hub IoT do toosend dados tooyour.</span><span class="sxs-lookup"><span data-stu-id="3fca1-121">You configure it toosend data tooyour IoT hub.</span></span> <span data-ttu-id="3fca1-122">Especificamente, o conjunto Olá **IoTHubName** toohello o nome do seu hub IoT do valor e defina Olá **IoTHubSuffix** valor muito**devices.net azure**.</span><span class="sxs-lookup"><span data-stu-id="3fca1-122">Specifically, set hello **IoTHubName** value toohello name of your IoT hub and set hello **IoTHubSuffix** value too**azure-devices.net**.</span></span> <span data-ttu-id="3fca1-123">Saudação de conjunto **transporte** tooone de valor de: **HTTP**, **AMQP**, ou **MQTT**.</span><span class="sxs-lookup"><span data-stu-id="3fca1-123">Set hello **Transport** value tooone of: **HTTP**, **AMQP**, or **MQTT**.</span></span> <span data-ttu-id="3fca1-124">Atualmente, apenas **HTTP** compartilha uma conexão TCP para todas as mensagens de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3fca1-124">Currently, only **HTTP** shares one TCP connection for all device messages.</span></span> <span data-ttu-id="3fca1-125">Se você definir o valor de saudação muito**AMQP**, ou **MQTT**, gateway Olá mantém um separado tooIoT de conexão de TCP Hub para cada dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3fca1-125">If you set hello value too**AMQP**, or **MQTT**, hello gateway maintains a separate TCP connection tooIoT Hub for each device.</span></span>
* <span data-ttu-id="3fca1-126">Olá **mapeamento** módulo mapeia endereços MAC de saudação de suas ids de dispositivo simulado dispositivos tooyour Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="3fca1-126">hello **mapping** module maps hello MAC addresses of your simulated devices tooyour IoT Hub device ids.</span></span> <span data-ttu-id="3fca1-127">Verifique se **deviceId** valores correspondência Olá ids de Olá dois dispositivos adicionados tooyour IoT hub e que hello **deviceKey** valores contêm chaves Olá dos dois dispositivos.</span><span class="sxs-lookup"><span data-stu-id="3fca1-127">Make sure that **deviceId** values match hello ids of hello two devices you added tooyour IoT hub, and that hello **deviceKey** values contain hello keys of your two devices.</span></span>
* <span data-ttu-id="3fca1-128">Olá **BLE1** e **BLE2** módulos são dispositivos de saudação simulada.</span><span class="sxs-lookup"><span data-stu-id="3fca1-128">hello **BLE1** and **BLE2** modules are hello simulated devices.</span></span> <span data-ttu-id="3fca1-129">Observe como os endereços de seu MAC correspondência Olá endereços Olá **mapeamento** módulo.</span><span class="sxs-lookup"><span data-stu-id="3fca1-129">Note how their MAC addresses match hello addresses in hello **mapping** module.</span></span>
* <span data-ttu-id="3fca1-130">Olá **agente** módulo registra o arquivo de tooa de atividade de gateway.</span><span class="sxs-lookup"><span data-stu-id="3fca1-130">hello **Logger** module logs your gateway activity tooa file.</span></span>
* <span data-ttu-id="3fca1-131">Olá **caminho do módulo** valores mostrados no exemplo hello presumem que você execute o exemplo hello da saudação **criar** pasta em sua cópia local da saudação **iot borda** repositório.</span><span class="sxs-lookup"><span data-stu-id="3fca1-131">hello **module path** values shown in hello example assume that you run hello sample from hello **build** folder in your local copy of hello **iot-edge** repository.</span></span>
* <span data-ttu-id="3fca1-132">Olá **links** matriz na parte inferior de saudação do arquivo JSON de saudação conecta Olá **BLE1** e **BLE2** módulos toohello **mapeamento** módulo e hello **mapeamento** módulo toohello **hub IOT** módulo.</span><span class="sxs-lookup"><span data-stu-id="3fca1-132">hello **links** array at hello bottom of hello JSON file connects hello **BLE1** and **BLE2** modules toohello **mapping** module, and hello **mapping** module toohello **IoTHub** module.</span></span> <span data-ttu-id="3fca1-133">Ela também garante que todas as mensagens são registradas por Olá **agente** módulo.</span><span class="sxs-lookup"><span data-stu-id="3fca1-133">It also ensures that all messages are logged by hello **Logger** module.</span></span>

```json
{
    "modules": [
        {
            "name": "IotHub",
          "loader": {
            "name": "native",
            "entrypoint": {
              "module.path": "./modules/iothub/libiothub.so"
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
              "module.path": "./modules/identitymap/libidentity_map.so"
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
              "module.path": "./modules/simulated_device/libsimulated_device.so"
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
              "module.path": "./modules/simulated_device/libsimulated_device.so"
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
              "module.path": "./modules/logger/liblogger.so"
            }
            },
            "args": {
              "filename": "deviceCloudUploadGatewaylog.log"
            }
          }
    ],
    "links": [
        {
            "source": "*",
            "sink": "Logger"
        },
        {
            "source": "BLE1",
            "sink": "mapping"
        },
        {
            "source": "BLE2",
            "sink": "mapping"
        },
        {
            "source": "mapping",
            "sink": "IotHub"
        }
    ]
}
```

<span data-ttu-id="3fca1-134">Salvar as alterações de saudação feitas toohello arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="3fca1-134">Save hello changes you made toohello configuration file.</span></span>

<span data-ttu-id="3fca1-135">exemplo de hello toorun:</span><span class="sxs-lookup"><span data-stu-id="3fca1-135">toorun hello sample:</span></span>

1. <span data-ttu-id="3fca1-136">No shell, navegar toohello **build a borda/iot** pasta.</span><span class="sxs-lookup"><span data-stu-id="3fca1-136">In your shell, navigate toohello **iot-edge/build** folder.</span></span>
2. <span data-ttu-id="3fca1-137">Execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="3fca1-137">Run hello following command:</span></span>
   
    ```sh
    ./samples/simulated_device_cloud_upload/simulated_device_cloud_upload_sample ../samples/simulated_device_cloud_upload/src/simulated_device_cloud_upload_lin.json
    ```
3. <span data-ttu-id="3fca1-138">Você pode usar o hello [explorer dispositivo] [ lnk-device-explorer] ou [Gerenciador de Hub IOT] [ lnk-iothub-explorer] ferramenta toomonitor mensagens de saudação que recebe do hub IoT de saudação gateway.</span><span class="sxs-lookup"><span data-stu-id="3fca1-138">You can use hello [device explorer][lnk-device-explorer] or [iothub-explorer][lnk-iothub-explorer] tool toomonitor hello messages that IoT hub receives from hello gateway.</span></span> <span data-ttu-id="3fca1-139">Por exemplo, usando o Gerenciador de Hub IOT você pode monitorar mensagens de dispositivo para nuvem usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="3fca1-139">For example, using iothub-explorer you can monitor device-to-cloud messages using hello following command:</span></span>

    ```sh
    iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
    ```

## <a name="next-steps"></a><span data-ttu-id="3fca1-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3fca1-140">Next steps</span></span>

<span data-ttu-id="3fca1-141">toogain uma compreensão mais avançada de borda de IoT do Azure e experiência com alguns exemplos de código, visite Olá tutoriais de desenvolvedor e recursos:</span><span class="sxs-lookup"><span data-stu-id="3fca1-141">toogain a more advanced understanding of Azure IoT Edge and experiment with some code examples, visit hello following developer tutorials and resources:</span></span>

* <span data-ttu-id="3fca1-142">[Enviar mensagens do dispositivo para a nuvem de um dispositivo físico com o Azure IoT Edge][lnk-physical-device]</span><span class="sxs-lookup"><span data-stu-id="3fca1-142">[Send device-to-cloud messages from a physical device with Azure IoT Edge][lnk-physical-device]</span></span>
* <span data-ttu-id="3fca1-143">[Azure IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="3fca1-143">[Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="3fca1-144">toofurther explorar recursos de saudação do IoT Hub, consulte:</span><span class="sxs-lookup"><span data-stu-id="3fca1-144">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="3fca1-145">[Guia do desenvolvedor do Hub IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="3fca1-145">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="3fca1-146">[Proteger a sua solução de IoT da saudação de plano de fundo para cima][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="3fca1-146">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

<!-- Links -->
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-physical-device]: iot-hub-iot-edge-physical-device.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md
