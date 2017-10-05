---
title: Simular um dispositivo com Azure IoT Edge (Linux) | Microsoft Docs
description: Como usar o Azure IoT Edge no Linux para criar um dispositivo simulado que envie telemetria por meio de um gateway do IoT Edge para um hub IoT.
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
ms.openlocfilehash: 5349960373ae6815862c5f79a69dd6d5d9d624ab
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-iot-edge-to-send-device-to-cloud-messages-with-a-simulated-device-linux"></a><span data-ttu-id="1b4ba-103">Use o Azure IoT Edge para enviar mensagens do dispositivo para a nuvem com um dispositivo simulado (Linux)</span><span class="sxs-lookup"><span data-stu-id="1b4ba-103">Use Azure IoT Edge to send device-to-cloud messages with a simulated device (Linux)</span></span>

[!INCLUDE [iot-hub-iot-edge-simulated-selector](../../includes/iot-hub-iot-edge-simulated-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-linux](../../includes/iot-hub-iot-edge-install-build-linux.md)]

## <a name="how-to-run-the-sample"></a><span data-ttu-id="1b4ba-104">Como executar a amostra</span><span class="sxs-lookup"><span data-stu-id="1b4ba-104">How to run the sample</span></span>

<span data-ttu-id="1b4ba-105">O script **build.sh** gera sua saída na pasta **build** na cópia local do repositório **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="1b4ba-105">The **build.sh** script generates its output in the **build** folder in your local copy of the **iot-edge** repository.</span></span> <span data-ttu-id="1b4ba-106">Essa saída inclui os quatro módulos do IoT Edge usados neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="1b4ba-106">This output includes the four IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="1b4ba-107">O script da build coloca:</span><span class="sxs-lookup"><span data-stu-id="1b4ba-107">The build script places the:</span></span>

* <span data-ttu-id="1b4ba-108">**liblogger.so** na pasta **build/modules/logger**.</span><span class="sxs-lookup"><span data-stu-id="1b4ba-108">**liblogger.so** in the **build/modules/logger** folder.</span></span>
* <span data-ttu-id="1b4ba-109">**libiothub.so** na pasta **build/modules/iothub**.</span><span class="sxs-lookup"><span data-stu-id="1b4ba-109">**libiothub.so** in the **build/modules/iothub** folder.</span></span>
* <span data-ttu-id="1b4ba-110">**lib\_identity\_map.so** na pasta **build/modules/identitymap**.</span><span class="sxs-lookup"><span data-stu-id="1b4ba-110">**lib\_identity\_map.so** in the **build/modules/identitymap** folder.</span></span>
* <span data-ttu-id="1b4ba-111">**libsimulated\_device.so** na pasta **build/modules/simulated\_device**.</span><span class="sxs-lookup"><span data-stu-id="1b4ba-111">**libsimulated\_device.so** in the **build/modules/simulated\_device** folder.</span></span>

<span data-ttu-id="1b4ba-112">Use esses caminhos para os valores de **caminho do módulo**, conforme mostrado no seguinte arquivo de configurações do JSON:</span><span class="sxs-lookup"><span data-stu-id="1b4ba-112">Use these paths for the **module path** values as shown in the following JSON settings file:</span></span>

<span data-ttu-id="1b4ba-113">O processo de exemplo \_device\_cloud\_upload\_ leva o caminho até um arquivo de configuração JSON como um argumento na linha de comando.</span><span class="sxs-lookup"><span data-stu-id="1b4ba-113">The simulated\_device\_cloud\_upload\_sample process takes the path to a JSON configuration file as a command-line argument.</span></span> <span data-ttu-id="1b4ba-114">O arquivo JSON de exemplo a seguir é fornecido no repositório do SDK em **samples\\simulated\_device\_cloud\_upload\_sample\\src\\simulated\_device\_cloud\_upload\_sample\_lin.json**.</span><span class="sxs-lookup"><span data-stu-id="1b4ba-114">The following example JSON file is provided in the SDK repository at **samples\\simulated\_device\_cloud\_upload\_sample\\src\\simulated\_device\_cloud\_upload\_sample\_lin.json**.</span></span> <span data-ttu-id="1b4ba-115">Este arquivo de configuração funciona da forma como está, a menos que você tenha modificado o script de build para colocar os módulos ou os executáveis de exemplo do IoT Edge em locais não padrão.</span><span class="sxs-lookup"><span data-stu-id="1b4ba-115">This configuration file works as is unless you modify the build script to place the IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="1b4ba-116">Os caminhos de módulo são referentes ao diretório de onde você executa o executável\_device\_cloud\_upload\_ de exemplo; não é o diretório onde o executável está localizado.</span><span class="sxs-lookup"><span data-stu-id="1b4ba-116">The module paths are relative to the directory from where you run the simulated\_device\_cloud\_upload\_sample executable, not the directory where the executable is located.</span></span> <span data-ttu-id="1b4ba-117">O arquivo de configuração JSON de exemplo, por padrão, grava 'deviceCloudUploadGatewaylog.log' no diretório de trabalho atual.</span><span class="sxs-lookup"><span data-stu-id="1b4ba-117">The sample JSON configuration file defaults to writing to 'deviceCloudUploadGatewaylog.log' in your current working directory.</span></span>

<span data-ttu-id="1b4ba-118">Em um editor de texto, abra o arquivo **samples/simulated\_device\_cloud\_upload\_sample/src/simulated\_device\_cloud\_upload\_lin.json** na sua cópia local do repositório **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="1b4ba-118">In a text editor, open the file **samples/simulated\_device\_cloud\_upload\_sample/src/simulated\_device\_cloud\_upload\_lin.json** in your local copy of the **iot-edge** repository.</span></span> <span data-ttu-id="1b4ba-119">Este arquivo configura os módulos do IoT Edge no gateway de exemplo:</span><span class="sxs-lookup"><span data-stu-id="1b4ba-119">This file configures the IoT Edge modules in the sample gateway:</span></span>

* <span data-ttu-id="1b4ba-120">O módulo **IoTHub** se conecta ao seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="1b4ba-120">The **IoTHub** module connects to your IoT hub.</span></span> <span data-ttu-id="1b4ba-121">Você o configura para enviar dados ao Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="1b4ba-121">You configure it to send data to your IoT hub.</span></span> <span data-ttu-id="1b4ba-122">Especificamente, defina o valor de **IoTHubName** como o nome de seu hub IoT e defina o valor de **IoTHubSuffix** como **azure-devices.net**.</span><span class="sxs-lookup"><span data-stu-id="1b4ba-122">Specifically, set the **IoTHubName** value to the name of your IoT hub and set the **IoTHubSuffix** value to **azure-devices.net**.</span></span> <span data-ttu-id="1b4ba-123">Defina o valor de **Transporte** como um destes: **HTTP**, **AMQP** ou **MQTT**.</span><span class="sxs-lookup"><span data-stu-id="1b4ba-123">Set the **Transport** value to one of: **HTTP**, **AMQP**, or **MQTT**.</span></span> <span data-ttu-id="1b4ba-124">Atualmente, apenas **HTTP** compartilha uma conexão TCP para todas as mensagens de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1b4ba-124">Currently, only **HTTP** shares one TCP connection for all device messages.</span></span> <span data-ttu-id="1b4ba-125">Se você definir o valor como **AMQP** ou **MQTT**, o gateway manterá uma conexão TCP separada para o Hub IoT para cada dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1b4ba-125">If you set the value to **AMQP**, or **MQTT**, the gateway maintains a separate TCP connection to IoT Hub for each device.</span></span>
* <span data-ttu-id="1b4ba-126">O módulo **mapping** mapeia os endereços MAC dos dispositivos simulados para as IDs de dispositivo do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="1b4ba-126">The **mapping** module maps the MAC addresses of your simulated devices to your IoT Hub device ids.</span></span> <span data-ttu-id="1b4ba-127">Verifique se os valores de **deviceId** correspondem às IDs dos dois dispositivos que você adicionou ao hub IoT e se os valores de **deviceKey** contêm as chaves dos dois dispositivos.</span><span class="sxs-lookup"><span data-stu-id="1b4ba-127">Make sure that **deviceId** values match the ids of the two devices you added to your IoT hub, and that the **deviceKey** values contain the keys of your two devices.</span></span>
* <span data-ttu-id="1b4ba-128">Os módulos **BLE1** e **BLE2** são os dispositivos simulados.</span><span class="sxs-lookup"><span data-stu-id="1b4ba-128">The **BLE1** and **BLE2** modules are the simulated devices.</span></span> <span data-ttu-id="1b4ba-129">Observe como os endereços MAC deles correspondem aos endereços no módulo **mapping**.</span><span class="sxs-lookup"><span data-stu-id="1b4ba-129">Note how their MAC addresses match the addresses in the **mapping** module.</span></span>
* <span data-ttu-id="1b4ba-130">O módulo **Logger** registra a atividade de gateway em um arquivo.</span><span class="sxs-lookup"><span data-stu-id="1b4ba-130">The **Logger** module logs your gateway activity to a file.</span></span>
* <span data-ttu-id="1b4ba-131">Os valores de **caminho do módulo** mostrados no exemplo presumem que você executa o exemplo da pasta **build** na sua cópia local do repositório **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="1b4ba-131">The **module path** values shown in the example assume that you run the sample from the **build** folder in your local copy of the **iot-edge** repository.</span></span>
* <span data-ttu-id="1b4ba-132">A matriz **links** na parte inferior do arquivo JSON conecta os módulos **BLE1** e **BLE2** ao módulo **mapping**, e o **mapping** ao módulo **IoTHub**.</span><span class="sxs-lookup"><span data-stu-id="1b4ba-132">The **links** array at the bottom of the JSON file connects the **BLE1** and **BLE2** modules to the **mapping** module, and the **mapping** module to the **IoTHub** module.</span></span> <span data-ttu-id="1b4ba-133">Ela também garante que todas as mensagens são registradas pelo módulo **Logger** .</span><span class="sxs-lookup"><span data-stu-id="1b4ba-133">It also ensures that all messages are logged by the **Logger** module.</span></span>

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

<span data-ttu-id="1b4ba-134">Salve as alterações feitas no arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="1b4ba-134">Save the changes you made to the configuration file.</span></span>

<span data-ttu-id="1b4ba-135">Para executar a amostra:</span><span class="sxs-lookup"><span data-stu-id="1b4ba-135">To run the sample:</span></span>

1. <span data-ttu-id="1b4ba-136">No shell, navegue até a pasta **iot-edge/build**.</span><span class="sxs-lookup"><span data-stu-id="1b4ba-136">In your shell, navigate to the **iot-edge/build** folder.</span></span>
2. <span data-ttu-id="1b4ba-137">Execute o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="1b4ba-137">Run the following command:</span></span>
   
    ```sh
    ./samples/simulated_device_cloud_upload/simulated_device_cloud_upload_sample ../samples/simulated_device_cloud_upload/src/simulated_device_cloud_upload_lin.json
    ```
3. <span data-ttu-id="1b4ba-138">É possível usar o [gerenciador de dispositivo][lnk-device-explorer] ou a ferramenta [iothub-explorer][lnk-iothub-explorer] para monitorar as mensagens que o Hub IoT recebe do gateway.</span><span class="sxs-lookup"><span data-stu-id="1b4ba-138">You can use the [device explorer][lnk-device-explorer] or [iothub-explorer][lnk-iothub-explorer] tool to monitor the messages that IoT hub receives from the gateway.</span></span> <span data-ttu-id="1b4ba-139">Por exemplo, usando o iothub-explorer, você pode monitorar as mensagens de dispositivo para nuvem usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="1b4ba-139">For example, using iothub-explorer you can monitor device-to-cloud messages using the following command:</span></span>

    ```sh
    iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
    ```

## <a name="next-steps"></a><span data-ttu-id="1b4ba-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1b4ba-140">Next steps</span></span>

<span data-ttu-id="1b4ba-141">Para compreender de maneira mais avançada o Azure IoT Edge e experimentar alguns exemplos de código, acesse os seguintes recursos e tutoriais para desenvolvedores:</span><span class="sxs-lookup"><span data-stu-id="1b4ba-141">To gain a more advanced understanding of Azure IoT Edge and experiment with some code examples, visit the following developer tutorials and resources:</span></span>

* <span data-ttu-id="1b4ba-142">[Enviar mensagens do dispositivo para a nuvem de um dispositivo físico com o Azure IoT Edge][lnk-physical-device]</span><span class="sxs-lookup"><span data-stu-id="1b4ba-142">[Send device-to-cloud messages from a physical device with Azure IoT Edge][lnk-physical-device]</span></span>
* <span data-ttu-id="1b4ba-143">[Azure IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="1b4ba-143">[Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="1b4ba-144">Para explorar melhor as funcionalidades do Hub IoT, consulte:</span><span class="sxs-lookup"><span data-stu-id="1b4ba-144">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="1b4ba-145">[Guia do desenvolvedor do Hub IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="1b4ba-145">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="1b4ba-146">[Proteger sua solução de IoT desde o início][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="1b4ba-146">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

<!-- Links -->
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-physical-device]: iot-hub-iot-edge-physical-device.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md
